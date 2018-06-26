# [DRAFT] Recon.JSON - A JSON-based Recon Data Standard
Recon.JSON is a project dedicated to creating a flexible and consistent JSON format across popular recon tools. Recon.JSON's format (obviously) is a valid JSON structure. This structure is designed to hold information about Hosts. Hosts objects are described by the set of attributes and other types defined in the standard below. Additions can be requested via the protocol in the "Contributing" section. 

## Structure
The structure of a ReconJSON file MUST be as follows:
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
The ```Host``` object SHALL be used to describe a specific profile of a computer. There MAY be multiple ```Host``` objects to a single device, or multiple devices to a single ```Host``` as is seen fit by the user. See Host.md file for futher usage for the ```Host``` object. 

The ```Host``` object has the following attributes defined:
* ```type``` - The type of object. In this case, ```Host```
* ```fqdn``` - The FQDN (Fully Qualified Domain Name) that resolves to this ```Host```
* ```ip``` - The IPv4 or IPv6 address to route to this ```Host```
* ```domain``` - The [second-level domain](https://en.wikipedia.org/wiki/Second-level_domain) for this ```Host```
* ```company``` - The company which owns this ```Host``` 
* ```dns``` - The ```DNS``` object(s) that describe(s) this ```Host```
* ```ports``` - The ```Port``` object(s) that describe(s) this ```Host```

Example:
```
[
{"type":"Host","fqdn":"example.acme.com","ip":"192.168.0.1","domain":"acme.com","company":"Acme","dns":{...},"ports":{...}}
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
		"ports":{...}
	}
]
```
### DNS



The ```DNS``` object has the following attributes defined:
* ```A``` - The list of ipv4 addresses that are associated with this ```Host```'s FQDN
* ```AAAA``` - The list of ipv6 addresses that are associated with this ```Host```'s FQDN
* ```CNAME``` - The list of FQDNs associated with this ```Host```

Example:
```
{
	"Host":[
		{
			"subdomain":"example.acme.com",
			"ip":"192.168.0.1",
			"domain":"acme.com",
			"company":"Acme",
			"dns":{
				"A":["192.168.0.1", "192.168.0.2"],
				"AAAA":["fe80::1"],
				"CNAME":["ex.acme.com"]
			},
		}
	]
}
```


### Port
The ```Port``` object has the following attributes defined:
* ```80``` (key) - The integer between 0 - 65535 that describes which port is open on this ```Host```
* ```state``` (value - key) - The openness state of the port. Options: ```closed```, ```open```, ```filtered```
* ```protocol``` (value - key) - The protocol thought to be communicating on this port
* ```banner``` (value - key) - The banner grabbed from this service
* ```content``` (value - key) - On certain services (80, 443, 8080, 8443) the content attribute can contain directory listings associated with this service
    * ```path``` (value - value) - The URI to this content
    * ```code``` (value - value) - The HTTP Status Code returned when this content was requested
    * ```content-type``` (value - value) - The HTTP Content Type returned when this content was requested
    * ```length``` (value - value) - The length, in bytes, returned when this content was requested
 
 Example:
 ```
 {
	"Host":[
		{
			"subdomain":"example.acme.com",
			"ip":"192.168.0.1",
			"domain":"acme.com",
			"company":"Acme",
			"ports":{
				"22":{
					"state":"open",
					"protocol":"ssh",
					"banner":"SSH-2.0-OpenSSH_7.2p2 Ubuntu-4ubuntu2.4"
				},
				"80":{
					"state":"open",
					"protocol":"http",
					"screenshot":"/root/screenshots/screenshot.jpg",
					"content":[
						{
							"path":"/test",
							"code":"200",
							"content-type":"text/html",
							"length":"1024"
						} 
					]
				}
			}
		}
	]
}
```
## Contributing
If you note any issues with Recon.JSON or would like to request an attribute or object be added to the standard, please submit an issue per the templates in the [docs](https://github.com/Rhynorater/reconjson/tree/master/docs) folder. Before submiting any issues please use Github's Issue Search feature to check if there is a similar issue already submitted. 
