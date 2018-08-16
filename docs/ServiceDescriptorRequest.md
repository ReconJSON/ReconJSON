### ServiceDescriptor Request
[Please fill in here the details of what your ServiceDescriptor is describing. When writing these sections, please use the verbiage described in RFC 2119.]
Example:
The ```PORT``` object SHALL be used to describe the status of the ports on a specific ```Host```. The ```Port``` object MUST be placed inside of one of the two ISO Model Layer 4 categories of the ```Host``` object. If attribute values are not known, they MUST NOT be included unless specified otherwise in the description below.

[Please fill in here the details of each attribute for this object. When writing these sections, please use the verbiage described in RFC 2119.]
Example:

The ```Port``` object has the following attributes defined:
* ```type```* - MUST be the type of object. In this case, ```Port```.
* ```port```* - MUST be the integer between 0 - 65535 that describes which port is open on this ```Host```
* ```state```* - MUST be the openness state of the port. Options: ```closed```, ```open```, ```filtered```. Typically, ```closed``` ports SHOULD NOT be reported.
* ```protocol``` - MUST be the ISO Model Layer 7 protocol thought to be communicating on this port
* ```services``` - MUST be a list of ```Service``` object(s) that describes the service(s) behind this port

\* Required attributes

[Please give example usages of the objects bot in JSONLines form and pretty-printed JSON]

Example:
```
{
		{"type":"Host","fqdn":"example.acme.com","ip":"192.168.0.1","domain":"acme.com","company":"Acme","ports":{"tcp":[{"type":"Port","port":"22","state":"open","protocol":"ssh","banner":"SSH-2.0-OpenSSH_7.2p2 Ubuntu-4ubuntu2.4"},{"type":"Port","port":"80","state":"open","protocol":"http","service":{"type":"Service","protocol":"http","content":["path":"/test","screenshot":"/root/screenshots/screenshot.jpg","code":"200","content-type":"text/html","length":"1024"]}}],"udp":[]}}
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
			"ports":{
				"tcp":[
					{
						"type":"Port",
						"port":"22"
						"state":"open",
						"protocol":"ssh"
					},
					{
						"type":"Port",
						"port":"80",
						"state":"open",
						"protocol":"http",
						"services":[...]
					}
				],
				"udp":[]
			}
		}
}
```