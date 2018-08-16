### Port
The ```PORT``` object SHALL be used to describe the status of the ports on a specific ```Host```. The ```Port``` object MUST be placed inside of one of the two ISO Model Layer 4 categories of the ```Host``` object. If attribute values are not known, they MUST NOT be included unless specified otherwise in the description below. See Port.md file for further usage for the ```Host``` object.


The ```Port``` object has the following attributes defined:
* ```type```* - MUST be the type of object. In this case, ```Port```.
* ```port```* - MUST be the integer between 0 - 65535 that describes which port is open on this ```Host```
* ```state```* - MUST be the openness state of the port. Options: ```closed```, ```open```, ```filtered```. Typically, ```closed``` ports SHOULD NOT be reported.
* ```services``` - MUST be a list of ```Service``` object(s) that describes the service(s) behind this port

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
