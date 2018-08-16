### DNS
The ```DNS``` object SHALL be used to describe the DNS configuration of a specific ```Host```. If attribute values are not known, they MUST NOT be included unless specified otherwise in the description below. See DNS.md file for futher usage for the ```Host``` object.


The ```DNS``` object has the following attributes defined:
* ```type```* - MUST be the type of object. In this case, ```DNS```.
* ```A``` - MUST be the list of IPv4 addresses that resolve from an A record lookup of this ```Host```s FQDN 
* ```AAAA``` - MUST be the list of IPv4 addresses that resolve from an AAAA record lookup of this ```Host```'s FQDN
* ```CNAME``` - MUST be the list of FQDNs that resolve from a CNAME record lookup of this ```Host```'s FQDN
* ```PTR``` - MUST be the list of FQDNs that resolve from a PTR record lookup of this ```Host```'s IP
* ```MX``` - MUST be the list of FQDNs that resolve from an MX record lookup of this ```Hosts```'s FQDN
* ```NS``` - MUST be the list of FQDNs that resolve from a NS record lookup of this ```Hosts```'s FQDN
* ```TXT``` - MUST be the list of strings that resolve from a TXT record lookup of this ```Hosts```'s FQDN

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
