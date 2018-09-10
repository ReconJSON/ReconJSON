### Host

The `Host` object SHALL be used to describe a specific profile of a computer. There MAY be multiple `Host` objects to a single device, or multiple devices to a single `Host` as is seen fit by the user. If attribute values are not known, they MUST NOT be included unless specified otherwise in the description below.

The `Host` object has the following attributes defined:
* `type`* - MUST be the type of object. In this case, `Host`
* `fqdn`** - MUST be the FQDN (Fully Qualified Domain Name) that resolves to this `Host`
* `ip`** - MUST be the IPv4 or IPv6 address to route to this `Host`
* `domain` - MUST be the [second-level domain](https://en.wikipedia.org/wiki/Second-level_domain) for this `Host`
* `company` - MUST be the company which owns this `Host` 
* `dns` - MUST be the `DNS` object(s) that describe(s) this `Host`
* `ports` - MUST be the `Port` object(s) that describe(s) this `Host`. The `Port` object(s) MUST be sorted by ISO Model Layer 4 protocol into either the `tcp` or the `udp` categories. If either of the `tcp` or `udp` categories are empty, they MUST still be included. However, if both `tcp` and `udp`  are empty, the `ports` attribute MUST be excluded.

\* Required attributes  
\*\* At least one of these attributes is required  
  
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
