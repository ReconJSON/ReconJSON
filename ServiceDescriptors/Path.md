### Path
The ```Path``` ServiceDescriptor SHALL be used to describe a single directory or file on a webserver. The ```Path``` object MUST be placed inside a list of element and correlated to the key ```Paths``` in the ```serviceDescriptors``` attribute of a ```Service``` object. If attribute values are not known, they MUST NOT be included unless specified otherwise in the description below.

The ```Path``` object has the following attributes defined:
* ```type```* - MUST be the type of object. In this case, ```Path```
* ```name```* - MUST be a descriptive name of what data this ```ServiceDescriptor``` is describing
* ```path```* - MUST be the path requested where path is defined by RFC 3986 section 3.3
* ```screenshot``` - MUST be the path to an image file that represents the contents of this endpoint
* ```code``` - MUST be the HTTP Status code returned by either a GET request (by default) or the HTTP Verb described in the ```verb``` attribute
* ```contentType``` - MUST be the content-type returned by either a GET request (by default) or the HTTP Verb described in the ```verb``` attribute
* ```length``` - MUST be the length of the request returned by either a GET request (by default) or the HTTP Verb described in the ```verb``` attribute
* ```verb``` - MUST be the the HTTP Verb used in the request to this path. By default this value SHOULD be assumed to be ```GET```. However, ```GET``` MAY also be specified if so desired.
* ```headers``` - MUST be a map of relevant headers not included above
* ```file``` - MUST be the file requested by the path above
* ```fileExt``` - MUST be the file extention of the file requested by the path above. This MUST not contain the . (dot). For example, a valid entry would be ```php``` not ```.php```
* ```hash``` - MUST be a map of hashtype to hash of this endpoint's content. This can be used to determine if the contents have changed or for forensic analysis

\* Required attributes

Example:
```
{"type":"Service","protocol":"http","banner":"Apache 1.0","serviceDescriptors":{"Paths":[{"type":"ServiceDescriptor","name":"Path","path":"/testing/test.php","screenshot":"/root/screenshots/screenshot.jpg","code":"200","content-type":"text/html","length":"1024","verb":"POST","headers":{"Server":"Apache"},"file":"test.php","fileExt":"php","hash":"8eab2974f483d66532d8e44120877c14"}]}}
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
				"path":"/testing/test.php",
				"screenshot":"/root/screenshots/screenshot.jpg",
				"code":"200",
				"content-type":"text/html",
				"length":"1024",
				"verb":"POST",
				"headers":{"Server":"Apache"},
				"file":"test.php",
				"fileExt":"php",
				"hash":"8eab2974f483d66532d8e44120877c14"

			}
		]
	}
}
```