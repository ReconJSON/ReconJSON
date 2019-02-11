### serviceDescriptor

The `serviceDescriptor` object SHALL be used to describe a specific attribute or configuration of the [`Service`](Service.md) object. There MAY be several `serviceDescriptor` objects to a single [`Service`](Service.md) object. Since the `serviceDescriptor` object is the object in which the specifics about programs are to be stored, it is impossible for the authors of this standard to construct a `serviceDescriptor` object for each and every use case. As a result, community sourcing of this attribute is needed. There will be several `serviceDescriptor` definitions in the `ServiceDescriptors` folder for basic use (HTTP(s) paths, HTTPS certs, and CSP Definitions) but more will be added as needed. If attribute values are not known, they MUST NOT be included unless specified otherwise in the description below or in another serviceDescriptor spec doc.

`serviceDescriptor` objects SHOULD be returned in the context of a `host > port > service`. However they MAY be returned by themselves. As such, `ServiceDescritors` SHOULD contain information to help identifiy which `host`, `port`, and `service` to which they belong.


The `serviceDescriptor` object has the following attributes defined:
* `type`* - MUST be the type of object. In this case, `serviceDescriptor`
* `name`* - MUST be a descriptive name of what data this `serviceDescriptor` is describing
* Additional elements dynamic to service being described. See `serviceDescriptors` folder for futher details.

\* Required attributes

Please note, the below example also includes a `service` object for context. 
```
{"type":"service","protocol":"http","banner":"Apache 1.0","serviceDescriptors":{"Directories":[{"type":"serviceDescriptor","name":"Directories","path":"/test","screenshot":"/root/screenshots/screenshot.jpg","code":"200","content-type":"text/html","length":"1024"}]}}
```

Pretty Printed:
```
{
    "type":"service",
    "protocol":"http",
    "banner":"Apache 1.0",
    "serviceDescriptors":{
        "paths":[
            {
                "type":"serviceDescriptor",
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
