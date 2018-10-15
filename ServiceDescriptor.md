### ServiceDescriptor

The `ServiceDescriptor` object SHALL be used to describe a specific attribute or configuration of the `Service` object. There MAY be several `ServiceDescriptor` objects to a single [`Service`](Service.md) object. Since the `ServiceDescriptor` object is the object in which the specifics about programs are to be stored, it is impossible for the authors of this standard to construct a `ServiceDescriptor` object for each and every use case. As a result, community sourcing of this attribute is needed. There will be several `ServiceDescriptor` definitions in the `ServiceDescriptors` folder for basic use (HTTP(s) paths, HTTPS certs, and CSP Definitions) but more will be added as needed. If attribute values are not known, they MUST NOT be included unless specified otherwise in the description below or in another ServiceDescriptor spec doc.

`ServiceDescriptor` objects SHOULD be returned in the context of a `Host > Port > Service`. However they MAY be returned by themselves. As such, `ServiceDescritors` SHOULD contain information to help identifiy which `Host`, `Port`, and `Service` to which they belong.


The `ServiceDescriptor` object has the following attributes defined:
* `type`* - MUST be the type of object. In this case, `ServiceDescriptor`
* `name`* - MUST be a descriptive name of what data this `ServiceDescriptor` is describing
* Additional elements dynamic to service being described. See `ServiceDescriptors` folder for futher details.

\* Required attributes

Please note, the below example also includes a `Service` object for context. 
```
{"type":"Service","protocol":"http","banner":"Apache 1.0","serviceDescriptors":{"Directories":[{"type":"ServiceDescriptor","name":"Directories","path":"/test","screenshot":"/root/screenshots/screenshot.jpg","code":"200","content-type":"text/html","length":"1024"}]}}
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
