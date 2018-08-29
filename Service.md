### Service
The ```Service``` object SHALL be used to describe a specific program running on a ```Port``` object. There MAY be several ```Service``` objects to a single ```Port``` object. ```Service``` objects MAY have child objects called ```ServiceDescriptor```(s). These objects are defined in more detail in the ```ServiceDescriptor.md``` file, but they are generally used to give program specific information. If attribute values are not known, they MUST NOT be included unless specified otherwise in the description below.  

The ```Service``` object has the following attributes defined:
* ```type```* - MUST be the type of object. In this case, ```Service```
* ```protocol``` - MUST be the protocol by which this ```Service``` communicates	
* ```banner``` - MUST be the banner that identifies this ```Service```
* ```serviceDescriptors``` - MUST be a key-value pairing of the ```name``` of a certain ```ServiceDescriptor``` IN THE PLURAL to a list of these objects (even if there is only one ServiceDescriptor). This allows a user to quickly access only the ```ServiceDescriptor``` desired.

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
		"Paths":[
			{
				"type":"ServiceDescriptor",
				"name":"Path",
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
