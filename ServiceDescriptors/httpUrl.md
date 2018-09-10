### httpUrl
The ```httpUrl``` `ServiceDescriptor` SHALL be used to describe a single directory or file on a webserver. The ```httpUrl``` object strongly SHOULD be placed inside a list of element and correlated to the key ```httpUrls``` in the ```serviceDescriptors``` attribute of a ```Service``` object. If attribute values are not known, they MUST NOT be included unless specified otherwise in the description below. The `httpUrl` `ServiceDescriptor` MAY be used to describe both HTTPS and HTTP protocol.

Both the `host` and `scheme` fields SHOULD be derived from the context (`Host` object and `Service` object respectively). However, if there is a case where a tool wishes to return only the ServiceDescriptor `httpUrl` then they may be used to describe the `Host` and `Service` to which this `httpUrl` belongs. 

The ```httpUrl``` object has the following attributes defined:
* ```type```* - MUST be the type of object. In this case, ```httpUrl```
* ```name```* - MUST be a descriptive name of what data this ```ServiceDescriptor``` is describing
* ```path```* - MUST be the relative path requested where path is defined by RFC 3986 section 4.2. MUST start with a slash.
* ```verb```* - MUST be the the HTTP Verb used in the request to this path.
* ```paramsContentType``` - MUST be the format in which the `params` field is stored. The value of this field MUST be one of the following: application/x-www-form-urlencoded, multipart/form-data, application/json, or application/xml. 
* ```params``` - MUST be any HTTP parameters sent along with this request. The format of the data stored in this field is described by `paramsContentType`. MUST NOT start with a `?` if placed in a GET request - this is a part of the structure not the parameter itself.
* ```screenshot``` - MUST be the path to an image file that represents the contents of this endpoint.
* ```host``` - MUST be the fully qualfied domain name that such that `host` + `path` defines the endpoint described. The scheme MUST NOT be included.
* ```scheme``` - MUST be either `http` or `https`. 
* ```code``` - MUST be the HTTP Status code returned by the HTTP Verb described in the ```verb``` attribute. This attribute MUST be an integer. 
* ```contentType``` - MUST be the content-type returned by  the HTTP Verb described in the ```verb``` attribute
* ```length``` - MUST be the length of the request returned by the HTTP Verb described in the ```verb``` attribute. This attribute MUST be an integer. 
* ```headers``` - MUST be a map of relevant headers not included above.
* ```file``` - MUST be the file requested by the path above.
* ```fileExt``` - MUST be the file extention of the file requested by the path above. This MUST not contain the . (dot). For example, a valid entry would be ```php``` not ```.php```.
* ```hash``` - MUST be a map of hashtype to hash of this endpoint's content. This can be used to determine if the contents have changed or for forensic analysis.
* `data` - Must be the path to the file containing the data returned in the body of this request. 

\* Required attributes

Example:
```
{"type":"Service","protocol":"http","banner":"Apache 1.0","serviceDescriptors":{"httpUrls":[{"type":"ServiceDescriptor","name":"httpUrl","path":"/testing/test.php","screenshot":"/root/screenshots/screenshot.jpg","code":200,"content-type":"text/html","length":1024,"verb":"POST","headers":{"Server":"Apache"},"file":"test.php","fileExt":"php","hash":{"md5":"8eab2974f483d66532d8e44120877c14"}}]}}
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
				"paramsContentType":"application/x-www-form-urlencoded",
				"params":"name=John&date=1-1-2018",
				"content-type":"text/html",
				"length":1024,
				"verb":"POST",
				"headers":{"Server":"Apache"},
				"file":"test.php",
				"fileExt":"php",
				"hash":{"md5":"8eab2974f483d66532d8e44120877c14"},
				"data":"/root/files/test-1-1-2018.php"

			}
		]
	}
}
```
