### httpUrl
The ```httpUrl``` ServiceDescriptor SHALL be used to describe a single directory or file on a webserver. The ```httpUrl``` object MUST be placed inside a list of element and correlated to the key ```httpUrls``` in the ```serviceDescriptors``` attribute of a ```Service``` object. If attribute values are not known, they MUST NOT be included unless specified otherwise in the description below.

The ```httpUrl``` object has the following attributes defined:
* ```type```* - MUST be the type of object. In this case, ```httpUrl```
* ```name```* - MUST be a descriptive name of what data this ```ServiceDescriptor``` is describing
* ```path```* - MUST be the path requested where path is defined by RFC 3986 section 3.3
* ```verb```* - MUST be the the HTTP Verb used in the request to this path.
* ```paramsContentType``` - MUST be the format in which the `params` field is stored. The value of this field MUST be one of the following: application/x-www-form-urlencoded, multipart/form-data, application/json, or application/xml. 
* ```params``` - MUST be any HTTP parameters sent along with this request. The format of the data stored in this field is described by `paramsContentType`. 
* ```screenshot``` - MUST be the path to an image file that represents the contents of this endpoint
* ```code``` - MUST be the HTTP Status code returned by either a GET request (by default) or the HTTP Verb described in the ```verb``` attribute. This attribute MUST be an integer. 
* ```contentType``` - MUST be the content-type returned by either a GET request (by default) or the HTTP Verb described in the ```verb``` attribute
* ```length``` - MUST be the length of the request returned by either a GET request (by default) or the HTTP Verb described in the ```verb``` attribute. This attribute MUST be an integer. 
* ```headers``` - MUST be a map of relevant headers not included above
* ```file``` - MUST be the file requested by the path above
* ```fileExt``` - MUST be the file extention of the file requested by the path above. This MUST not contain the . (dot). For example, a valid entry would be ```php``` not ```.php```
* ```hash``` - MUST be a map of hashtype to hash of this endpoint's content. This can be used to determine if the contents have changed or for forensic analysis

\* Required attributes

Example:
```
{"type":"Service","protocol":"http","banner":"Apache 1.0","serviceDescriptors":{"httpUrls":[{"type":"ServiceDescriptor","name":"httpUrl","path":"/testing/test.php","screenshot":"/root/screenshots/screenshot.jpg","code":200,"content-type":"text/html","length":1024,"verb":"POST","headers":{"Server":"Apache"},"file":"test.php","fileExt":"php","hash":"8eab2974f483d66532d8e44120877c14"}]}}
```


Pretty Printed:
```
{
	"type":"Service",
	"protocol":"http",
	"banner":"Apache 1.0",
	"serviceDescriptors":{
		"httpUrls":[
			{
				"type":"ServiceDescriptor",
				"name":"httpUrl",
				"path":"/testing/test.php",
				"screenshot":"/root/screenshots/screenshot.jpg",
				"code":200,
				"content-type":"text/html",
				"length":1024,
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
