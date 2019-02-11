### service

The `service` object SHALL be used to describe a specific program running on a port. There MAY only be one [`service`](Service.md) object per port in the [`Host`](Host.md) object's `port` attribute. `service` objects MAY have child objects called `serviceDescriptor`(s). These objects are defined in more detail in the `ServiceDescriptor.md` file, but they are generally used to give program specific information. If attribute values are not known, they MUST NOT be included unless specified otherwise in the description below.  

The `service` object has the following attributes defined:
* `type`* - MUST be the type of object. In this case, `service`
* `active` - MUST be the Boolean variable representing whether this service is active or not. `true` for active, `false` for inactive. If this value is not set, the service SHOULD be assumed to be be active.
* `protocol` - MUST be the protocol by which this `service` communicates	
* `banner` - MUST be the banner that identifies this `service`
* `serviceDescriptors` - MUST be a key-value pairing of the `name` of a certain `serviceDescriptor` IN THE SINGULAR to a list of these objects. This allows a user to quickly access only the `serviceDescriptor` desired.

\* Required attributes

Example:
```
{"type":"service","protocol":"http","banner":"Apache 1.0","serviceDescriptors":{"httpUrl":[{"type":"serviceDescriptor","path":"/test","screenshot":"/root/screenshots/screenshot.jpg","code":"200","content-type":"text/html","length":"1024"}]}}
```

Pretty Printed:
```
{
    "type":"service",
    "protocol":"http",
    "banner":"Apache 1.0",
    "serviceDescriptors":{
        "httpUrl":[
            {
                "type":"serviceDescriptor",
                "name":"httpUrl",
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
