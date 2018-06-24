# Recon.json - A JSON-based Recon Standard
Recon.json is a project dedicated to creating a flexible and consistent JSON format across popular recon tools. Recon.json's format (obviously) is a valid JSON structure. This structure is designed to hold information about Hosts. Hosts objects are described by the set of attributes and other types defined in the standard below. Additions can be requested via the protocol in the "Additions" section. 

## Structure
The output of a tool that utilizes Recon.json format should hold the following structure:
```
{
  "Host":[

    ]
}
```
Each JSON object should be placed inside the ```Host``` definition to show that the following objects are Hosts. Each other object type will be used to describe the ```Host``` object. 

### Host
The ```Host``` object has the following attributes defined:
* ```subdomain``` - The FQDN (Fully Qualified Domain Name) that resolves to this ```Host```
* ```ipv4``` - The IPv4 address to route to this ```Host```
* ```ipv6``` - The IPv6 address to route to this ```Host```
* ```domain``` - The [second-level-domain](https://en.wikipedia.org/wiki/Second-level_domain) for this ```Host```
* ```company``` - The company which owns this assets 
* ```dns``` - The ```DNS``` object(s) that describe(s) this host
* ```ports``` - The ```Port``` object(s) that describe(s) this host

Example:
```
{
	"Host":[
		{
			"subdomain":"example.acme.com",
			"ip":"192.168.0.1",
			"domain":"acme.com",
			"company":"Acme",
			"dns":{...},
			"port":{...}
		}
	]
}

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
* ```80``` (key) - The integer between 0 - 65535 that describes which port is open
* ```state```(value) - The openness state of the port. Options: ```closed```, ```open```, ```filtered```
* ```protocol```(value) - The protocol thought to be communicating on this port
* ```banner``` (value) - The banner grabbed from this service
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
			"port":{
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
