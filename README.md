# [DRAFT] Recon.JSON - A JSON-based Recon Data Standard
Recon.JSON is a project dedicated to creating a flexible and consistent JSON format across popular recon tools. Recon.JSON's format (obviously) is a valid JSON structure. This structure is designed to hold information about Hosts. Hosts objects are described by the set of attributes and other types defined in the standard below. Additions can be requested via the protocol in the "Contributing" section. 

## Structure
A file the conforms to the ReconJSON standard MUST have the ```.json``` extension. Any name for the file is permitted. 
The internal structure of a ReconJSON file MUST be as follows:
```
[
{"type":"Host"},
{"type":"Host"},
{"type":"Host"},
{"type":"Host"}
]
```
The first line of a ReconJSON file MUST be a left bracket ```[``` (ASCII 91) and the last line MUST be a right bracket ```]``` (ASCII 93). In between these backets MUST be one or more ```Host``` objects. These objects MUST be collapsed JSON objects stored on a single line. These lines MUST be seperated by a comma ```,``` (ASCII 44) and a single linefeed character ```\n``` (ASCII 10). The ```Host``` object on the last line MUST NOT have a trailing comma ```,``` (ASCII 44), but MUST have a trailing linefeed character ```\n``` (ASCII 10).

This format is pure JSON, with the ```Host``` objects collapsed into a single line. The reasoning behind this decision is to provide a file that can easily be parsed by programming languages' JSON libraries while also producing a file that is grep-able and one which a simple ```wc -l``` command will immediately convey the correct number of hosts to the user (number of lines - 2). 

Each ```Host``` object defined in this section MUST follow the standard defined in the ```Host``` section of this document. 

### Host
The ```Host``` object SHALL be used to describe a specific profile of a computer. There MAY be multiple ```Host``` objects to a single device, or multiple devices to a single ```Host``` as is seen fit by the user. See Host.md file for futher usage for the ```Host``` object. If attribute values are not known, they MUST NOT be included unless specified otherwise in the description below.

The ```Host``` object has the following attributes defined:
* ```type```* - MUST be the type of object. In this case, ```Host```
* ```fqdn``` - MUST be the FQDN (Fully Qualified Domain Name) that resolves to this ```Host```
* ```ip```* - MUST be the IPv4 or IPv6 address to route to this ```Host```
* ```domain``` - MUST be the [second-level domain](https://en.wikipedia.org/wiki/Second-level_domain) for this ```Host```
* ```company``` - MUST be the company which owns this ```Host``` 
* ```dns``` - MUST be the ```DNS``` object(s) that describe(s) this ```Host```
* ```ports``` - MUST be the ```Port``` object(s) that describe(s) this ```Host```. The ```Port``` object(s) MUST be sorted by ISO Model Layer 4 protocol into either the ```tcp``` or the ```udp``` categories. If either of the ```tcp``` or ```udp``` categories are empty, they MUST still be included. However, if both ```tcp``` and ```udp```  are empty, the ```ports``` attribute MUST be excluded.

\* Required attributes

Example:
```
[
{"type":"Host","fqdn":"example.acme.com","ip":"192.168.0.1","domain":"acme.com","company":"Acme","dns":{...},"ports":{"tcp":[],"udp":[]}}
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
The ```DNS``` object SHALL be used to describe the DNS configuration of a specific ```Host```. If attribute values are not known, they MUST NOT be included unless specified otherwise in the description below.


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
	"Host":[
		{"type":"Host","fqdn":"example.acme.com","ip":"192.168.0.1","domain":"acme.com","company":"Acme","dns":{"type":"DNS","A":["192.168.0.1", "192.168.0.2"],"AAAA":["fe80::1"],"CNAME":["ex.acme.com"],"PTR":["ex.acme.com"],"MX":["example-acme-com.mail.protection.outlook.com"],"NS":["nameserver.acme.com"],TXT":["txtRecordString"]}}
	]
}

```

Pretty Printed:

```
{
	"Host":[
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
	]
}
```


### Port
The ```PORT``` object SHALL be used to describe the status of the ports on a specific ```Host```. The ```Port``` object MUST be placed inside of one of the two ISO Model Layer 4 categories of the ```Host``` object. If attribute values are not known, they MUST NOT be included unless specified otherwise in the description below. 


The ```Port``` object has the following attributes defined:
* ```type```* - MUST be the type of object. In this case, ```Port```.
* ```port```* - MUST be the integer between 0 - 65535 that describes which port is open on this ```Host```
* ```state```* - MUST be the openness state of the port. Options: ```closed```, ```open```, ```filtered```. Typically, ```closed``` ports SHOULD NOT be reported.
* ```protocol``` - MUST be the ISO Model Layer 7 protocol thought to be communicating on this port
* ```banner``` - MUST be the banner grabbed from the service behind this port
* ```service``` - MUST be the ```Service``` object that describes the service behind this port

\* Required attributes

 Example:
 ```
 {
	"Host":[
		{"type":"Host","fqdn":"example.acme.com","ip":"192.168.0.1","domain":"acme.com","company":"Acme","ports":{"tcp":[{"type":"Port","port":"22","state":"open","protocol":"ssh","banner":"SSH-2.0-OpenSSH_7.2p2 Ubuntu-4ubuntu2.4"},{"type":"Port","port":"80","state":"open","protocol":"http","service":{"type":"Service","protocol":"http","content":["path":"/test","screenshot":"/root/screenshots/screenshot.jpg","code":"200","content-type":"text/html","length":"1024"]}}],"udp":[]}}
	]
}
```


 Pretty Printed:
 ```
 {
	"Host":[
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
						"state":"open",
						"protocol":"ssh",
						"banner":"SSH-2.0-OpenSSH_7.2p2 Ubuntu-4ubuntu2.4"
					},
					{
						"type":"Port",
						"port":"80",
						"state":"open",
						"protocol":"http",
						"service":{
								"type":"Service",
								"protocol":"http"
								"content":[
									"path":"/test",
									"screenshot":"/root/screenshots/screenshot.jpg",
									"code":"200",
									"content-type":"text/html",
									"length":"1024"
								]
							} 
					}
				],
				"udp":[]
			}
		}
	]
}
```
## Contributing
If you note any issues with Recon.JSON or would like to request an attribute or object be added to the standard, please submit an issue per the templates in the [docs](https://github.com/Rhynorater/reconjson/tree/master/docs) folder. Before submiting any issues please use Github's Issue Search feature to check if there is a similar issue already submitted. 
