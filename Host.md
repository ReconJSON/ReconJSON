### Host

The `Host` object SHALL be used to describe a specific profile of a computer. There MAY be multiple `Host` objects to a single device, or multiple devices to a single `Host` as is seen fit by the user. If attribute values are not known, they MUST NOT be included unless specified otherwise in the description below.

The `Host` object has the following attributes defined:
* `type`* - MUST be the type of object. In this case, `Host`
* `fqdn`** - MUST be the FQDN (Fully Qualified Domain Name) that resolves to this `Host`
* `ip`** - MUST be the IPv4 or IPv6 address to route to this `Host`
* `domain` - MUST be the [second-level domain](https://en.wikipedia.org/wiki/Second-level_domain) for this `Host`
* `company` - MUST be the company which owns this `Host` 
* `dns` - MUST be the [`DNS`](DNS.md) object(s) that describe(s) this `Host`
* `ports` - MUST be a map (key-value pair) with two keys: `tcp` and `udp`. These two keys MUST have values which are also maps (key-value pairs) which correlate a single number between 0-65535 (representing a port) to a [`Service`](Service.md) object (NOTE: Since JSON doesn't allow numbers to be keys, a string representation of the number must be used). If a port is closed, then it SHOULD NOT have an entry in the key-value pair under its respective `tcp` or `udp` designation. However, in the circumstance that data needs to be stored on a port that was open and is now closed, the [`Service`](Service.md) object's `active` attribute should be used to delimit that the port is closed. If a port is open, but no [`Service`](Service.md) object has been constructed, it should be left with a blank object `{}`. Otherwise, the port's value pair MUST point to its respective [`Service`](Service.md) object. 

\* Required attributes  
\*\* At least one of these attributes is required  
  
Example:

```
[
{"type":"Host","fqdn":"example.acme.com","ip":"192.168.0.1","domain":"acme.com","company":"Acme","dns":{...},"ports":{"tcp":{"80":{},"443":{"type":"Service","protocol":"https"}},"udp":{...}}}
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
            "tcp":{
                "80":{},
                "443":{"type":"Service", "protocol":"https"}
                },
            "udp":{...}
        }
    }
]
```
