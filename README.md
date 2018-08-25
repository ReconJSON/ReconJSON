# [DRAFT] ReconJSON - A JSON-based Recon Data Standard
ReconJSON is a project dedicated to creating a flexible and consistent JSON format across popular recon tools. ReconJSON's format (obviously) is a valid JSON structure. This structure is designed to hold information about Hosts. Hosts objects are described by the set of attributes and other types defined in the standard below. Additions can be requested via the protocol in the "Contributing" section. 

## Structure
A file the conforms to the ReconJSON standard MUST have the `.json` extension. Any name for the file is permitted. 
The internal structure of a ReconJSON file MUST be as follows:

```
[
{"type":"Host"},
{"type":"Host"},
{"type":"Host"},
{"type":"Host"}
]
```

The first line of a ReconJSON file MUST be a left bracket `[` (ASCII 91) and the last line MUST be a right bracket `]` (ASCII 93). In between these brackets MUST be one or more `Host` objects. These objects MUST be collapsed JSON objects stored on a single line. These lines MUST be separated by a comma `,` (ASCII 44) and a single linefeed character `\n` (ASCII 10). The `Host` object on the last line MUST NOT have a trailing comma `,` (ASCII 44), but MUST have a trailing linefeed character `\n` (ASCII 10).

This format is pure JSON, with the `Host` objects collapsed into a single line. The reasoning behind this decision is to provide a file that can easily be parsed by programming languages' JSON libraries while also producing a file that is grep-able and one which a simple `wc -l` command will immediately convey the correct number of hosts to the user (number of lines - 2). 

Each `Host` object defined in this section MUST follow the standard defined in the `Host` section of this document. 

### Host

The `Host` object SHALL be used to describe a specific profile of a computer. There MAY be multiple `Host` objects to a single device, or multiple devices to a single `Host` as is seen fit by the user. If attribute values are not known, they MUST NOT be included unless specified otherwise in the description below. See [Host.md](Host.md) file for further usage for the `Host` object.

The `Host` object has the following attributes defined:
* `type`* - MUST be the type of object. In this case, `Host`
* `fqdn` - MUST be the FQDN (Fully Qualified Domain Name) that resolves to this `Host`
* `ip`* - MUST be the IPv4 or IPv6 address to route to this `Host`
* `domain` - MUST be the [second-level domain](https://en.wikipedia.org/wiki/Second-level_domain) for this `Host`
* `company` - MUST be the company which owns this `Host`
* `dns` - MUST be the `DNS` object(s) that describe(s) this `Host`
* `ports` - MUST be the `Port` object(s) that describe(s) this `Host`. The `Port` object(s) MUST be sorted by ISO Model Layer 4 protocol into either the `tcp` or the `udp` categories. If either of the `tcp` or `udp` categories are empty, they MUST still be included. However, if both `tcp` and `udp`  are empty, the `ports` attribute MUST be excluded.

\* Required attributes

Example:

```
[
{"type":"Host","fqdn":"example.acme.com","ip":"192.168.0.1","domain":"acme.com","company":"Acme","dns":{...},"ports":{"tcp":[...],"udp":[...]}}
]
```

Pretty Printed:

```
[
  {
    "type":"Host",
    "fqdn":"example.acme.com",
    "ip":"192.168.0.1",
    "domain":"acme.com",
    "company":"Acme",
    "dns":{...},
    "ports":{
      "tcp":[...],
      "udp":[...]
    }
  }
]
```

### DNS

The `DNS` object SHALL be used to describe the DNS configuration of a specific `Host`. If attribute values are not known, they MUST NOT be included unless specified otherwise in the description below. See [DNS.md](DNS.md) file for further usage for the `Host` object.

The `DNS` object has the following attributes defined:
* `type`* - MUST be the type of object. In this case, `DNS`.
* `A` - MUST be the list of IPv4 addresses that resolve from an A record lookup of this `Host`s FQDN 
* `AAAA` - MUST be the list of IPv6 addresses that resolve from an AAAA record lookup of this `Host`'s FQDN
* `CNAME` - MUST be the list of FQDNs that resolve from a CNAME record lookup of this `Host`'s FQDN
* `PTR` - MUST be the list of FQDNs that resolve from a PTR record lookup of this `Host`'s IP
* `MX` - MUST be the list of FQDNs that resolve from an MX record lookup of this `Hosts`'s FQDN
* `NS` - MUST be the list of FQDNs that resolve from a NS record lookup of this `Hosts`'s FQDN
* `TXT` - MUST be the list of strings that resolve from a TXT record lookup of this `Hosts`'s FQDN

\* Required attributes

Example:

```
{
  {"type":"Host","fqdn":"example.acme.com","ip":"192.168.0.1","domain":"acme.com","company":"Acme","dns":{"type":"DNS","A":["192.168.0.1", "192.168.0.2"],"AAAA":["fe80::1"],"CNAME":["ex.acme.com"],"PTR":["ex.acme.com"],"MX":["example-acme-com.mail.protection.outlook.com"],"NS":["nameserver.acme.com"],TXT":["txtRecordString"]}}
}
```

Pretty Printed:

```
{
  {
    "type":"Host",
    "fqdn":"example.acme.com",
    "ip":"192.168.0.1",
    "domain":"acme.com",
    "company":"Acme",
    "dns":{
      "type":"DNS",
      "A":["192.168.0.1", "192.168.0.2"],
      "AAAA":["fe80::1"],
      "CNAME":["ex.acme.com"],
      "PTR":["ex.acme.com"],
      "MX":["example-acme-com.mail.protection.outlook.com"],
      "NS":["nameserver.acme.com"],
      "TXT":["txtRecordString"]
    },
  }
}
```

### Port

The `PORT` object SHALL be used to describe the status of the ports on a specific `Host`. The `Port` object MUST be placed inside of one of the two ISO Model Layer 4 categories of the `Host` object. If attribute values are not known, they MUST NOT be included unless specified otherwise in the description below. See [Port.md](Port.md) file for further usage for the `Host` object.

The `Port` object has the following attributes defined:
* `type`* - MUST be the type of object. In this case, `Port`.
* `port`* - MUST be the integer between 0 - 65535 that describes which port is open on this `Host`
* `state`* - MUST be the openness state of the port. Options: `closed`, `open`, `filtered`. Typically, `closed` ports SHOULD NOT be reported.
* `services` - MUST be a list of `Service` object(s) that describes the service(s) behind this port

\* Required attributes

Example:

```
{{"type":"Host","fqdn":"example.acme.com","ip":"192.168.0.1","domain":"acme.com","company":"Acme","ports":{"tcp":[{"type":"Port","port":"22","state":"open"},{"type":"Port","port":"80","state":"open","services":[...]}],"udp":[]}}}
```

Pretty Printed:

```
{
  {
    "type":"Host",
    "fqdn":"example.acme.com",
    "ip":"192.168.0.1",
    "domain":"acme.com",
    "company":"Acme",
    "ports":{
      "tcp":[
        {
          "type":"Port",
          "port":"22"
          "state":"open"
        },
        {
          "type":"Port",
          "port":"80",
          "state":"open",
          "services":[...]
        }
      ],
      "udp":[]
    }
  }
}
```

### Service

The `Service` object SHALL be used to describe a specific program running on a `Port` object. There MAY be several `Service` objects to a single `Port` object. `Service` objects MAY have child objects called `ServiceDescriptor`(s). These objects are defined in more detail in the [ServiceDescriptor.md](ServiceDescriptor.md) file, but they are generally used to give program specific information. If attribute values are not known, they MUST NOT be included unless specified otherwise in the description below. See [Service.md](Service.md) file for further usage for the `Host` object.     

The `Service` object has the following attributes defined:
* `type`* - MUST be the type of object. In this case, `Service`
* `protocol` - MUST be the protocol by which this `Service` communicates	
* `banner` - MUST be the banner that identifies this `Service`
* `serviceDescriptors` - MUST be a map of the `name` of a certain `ServiceDescriptor` to a list of these objects. This allows a user to quickly access only the `ServiceDescriptor` desired

\* Required attributes

Example:

```
{"type":"Service","protocol":"http","banner":"Apache 1.0","serviceDescriptors":{"Directories":[{"type":"ServiceDescriptor","path":"/test","screenshot":"/root/screenshots/screenshot.jpg","code":"200","content-type":"text/html","length":"1024"}]}}
```

Pretty Printed:

```
{
  "type":"Service",
  "protocol":"http",
  "banner":"Apache 1.0",
  "serviceDescriptors":{
    "Directories":[
      {
        "type":"ServiceDescriptor",
        "path":"/test",
        "screenshot":"/root/screenshots/screenshot.jpg",
        "code":"200",
        "content-type":"text/html",
        "length":"1024"
      }
    ]
  }
}
```

### ServiceDescriptor

The `ServiceDescriptor` object SHALL be used to describe a specific attribute or configuration of the `Service` object. There MAY be several `ServiceDescriptor` objects to a single `Service` object. Since the `ServiceDescriptor` object is the object in which the specifics about programs are to be stored, it is impossible for the authors of this standard to construct a `ServiceDescriptor` object for each and every use case. As a result, community sourcing of this attribute is needed. There will be several `ServiceDescriptor` definitions in the `ServiceDescriptors` folder for basic use (HTTP(s) directories, HTTPS certs, and CSP Definitions) but more will be added as needed. If attribute values are not known, they MUST NOT be included unless specified otherwise in the description below or in another ServiceDescriptor spec doc. See [ServiceDescriptor.md](ServiceDescriptor.md) file for further usage for the `Host` object.

The `ServiceDescriptor` object has the following attributes defined:

* `type`* - MUST be the type of object. In this case, `ServiceDescriptor`
* `name`* - MUST be a descriptive name of what data this `ServiceDescriptor` is describing
* Additional elements dynamic to service being described. See `ServiceDescriptors` folder for further details.

\* Required attributes

Please note, the below example also includes a `Service` object for context:

```
{"type":"Service","protocol":"http","banner":"Apache 1.0","serviceDescriptors":{"Directories":[{"type":"ServiceDescriptor","name":"Directories","path":"/test","screenshot":"/root/screenshots/screenshot.jpg","code":"200","content-type":"text/html","length":"1024"}]}}
```

Please note, the below example also includes a `Service` object for context:

```
{
  "type":"Service",
  "protocol":"http",
  "banner":"Apache 1.0",
  "serviceDescriptors":{
    "Directories":[
      {
        "type":"ServiceDescriptor",
        "name":"Directories"
        "path":"/test",
        "screenshot":"/root/screenshots/screenshot.jpg",
        "code":"200",
        "content-type":"text/html",
        "length":"1024"
      }
    ]
  }
}
```

## Contributing

If you note any issues with ReconJSON or would like to request an attribute or object be added to the standard, please submit an issue per the templates in the [docs](docs/) folder. Before submiting any issues please use Github's Issue Search feature to check if there is a similar issue already submitted.
