### httpCsp

The `httpCsp` `ServiceDescriptor` SHALL be used to describe the Content Security Policy for a specific HTTP service. The `httpsCsp` `ServiceDescriptor` MUST be placed inside a list of element and correlated to the key `httpsCsps` in the `serviceDescriptors` attribute of a `Service` object. If attribute values are not known, they MUST NOT be included unless specified otherwise in the description below. 

The `httpCsp` object has the following attributes defined:
* `type`* - MUST be the type of object. In this case, `ServiceDescriptor`.
* `name`* - MUST be the name of `ServiceDescriptor`. In this case, `httpCsp`.
* `location`* - MUST be the location where the CSP was found. Must be either `http header` or `meta tag`.

The other attributes of this object are simply all supported CSP Directives, as listed [in the spec](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy#Directives), as the key, and the policies of the respective CSP Directives as the values. 

Example (`Host` and `Service` objects ommitted for brevity):
```
{"type":"ServiceDescriptor","protocol":"https","banner":"Apache 1.0","serviceDescriptors":{"httpsCsps":[{"type":"ServiceDescriptor","name":"httpCsp","location":"http-header","script-src":"'self' https://","object-src":"'none'"}]}}
```


Pretty Printed:
```
{
    "type":"ServiceDescriptor",
    "protocol":"https",
    "banner":"Apache 1.0",
    "serviceDescriptors":{
        "httpsCsps":[
            {
                "type":"ServiceDescriptor",
                "name":"httpCsp",
                "location":"http-header",
                "script-src":"'self' https:",
                "object-src": "'none'"
            }
        ]
    }
}
```
