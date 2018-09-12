### httpsCert

The `httpsCert` `ServiceDescriptor` SHALL be used to describe HTTPS (X.509) (pre-)cerficates. The `httpsCert` `ServiceDescriptor` strongly SHOULD be placed inside a list of element and correlated to the key `httpsCerts` in the `serviceDescriptors` attribute of a `Service` object. HOWEVER, it MAY be returned in list format if it is impossible to correlate the certificate with a `Host` object. If attribute values are not known, they MUST NOT be included unless specified otherwise in the description below. 

The `httpsCert` object has the following attributes defined:
* `type`* - MUST be the type of object. In this case, `ServiceDescriptor`.
* `name`* - MUST be the name of `ServiceDescriptor`. In this case, `httpsCert`.
* `certType`* - MUST be the type of X.509 certificate: either `cert` or `precert`.
* `data`* -	The raw X.509 (pre-)certificate, encoded in base64.
* `dnsNames` - MUST be a list of strings representing the DNS identifiers for the cert from both the Subject CN and the DNS SANs.
* `issuer` - MUST be the distinguished name of the certificate's issuer.
* `sha256` - MUST be the hex-encoded SHA-256 digest of the raw X.509 (pre-)certificate.
* `pubkeySha256` - MUST be the hex-encoded SHA-256 digest of the Subject Public Key Info.
* `notBefore` - MUST be the not before date, in RFC3339 format (e.g. 2016-06-16T00:00:00-00:00) .
* `notAfter` - MUST be the not after date, in RFC3339 format (e.g. 2016-06-16T00:00:00-00:00).
* `logs` - A list of key-value pairs describing the Certificate Transparency logs containing this (pre-)certificate. Example: `{"id":"7ku9t3XOYLrhQmkfq+GeZqMPfl+wctiDAMR7iXqo/cs=","index":385319610,"timestamp":"2018-08-16T00:20:43.850-00:00"}`.
    * `id` - The ID of the Certificate Transparency log, encoded in base64.
    * `index` - The 0-based index of the (pre-)certificate's entry in the log.
    * `timestamp` - The time at which the (pre-)certificate was submitted to this log, in RFC3339 format (e.g. 2017-05-04T13:39:21.071-00:00).

\* Required attributes

Shout out to CertSpotter for making this definition a lot easier with [the CertSpotter API](https://sslmate.com/certspotter/api).

Example (`Host` and `Port` Objects ommitted for brevity):
```
{"type":"ServiceDescriptor","protocol":"https","banner":"Apache 1.0","serviceDescriptors":{"httpsCert":[{"type":"ServiceDescriptor","name":"httpsCerts","certType":"cert","dnsNames":["poc.rhynorater.com"],"issuer":"C=US, O=Let's Encrypt, CN=Let's Encrypt Authority X3","sha256":"aeb46e0cbf44f8065aac6bd5d3f07f3b5f62075e6840aaeb40b8959f9f6c0a2d","pubkeySha256":"d7f806a84a8d52023f8be0cb7981de753a669bfa1980ac8ef1e7b5992c0dff80","notBefore":"2018-08-12T23:47:38-00:00","notAfter":"2018-11-10T23:47:38-00:00","logs":[{"id":"7ku9t3XOYLrhQmkfq+GeZqMPfl+wctiDAMR7iXqo/cs=","index":385319610,"timestamp":"2018-08-16T00:20:43.850-00:00"},{"id":"pLkJkLQYWBSHuxOizGdwCjw1mAT5G9+443fNDsgN3BA=","index":346479511,"timestamp":"2018-08-16T00:03:21.975-00:00"},{"id":"pFASaQVaFVReYhGrN7wQP2KuVXakXksXFEU+GyIQaiU=","index":333727869,"timestamp":"2018-08-13T00:47:39.051-00:00"}],"data":"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"}]}}
```


Pretty Printed:
```
{
    "type":"ServiceDescriptor",
    "protocol":"https",
    "banner":"Apache 1.0",
    "serviceDescriptors":{
        "httpsCerts":[
            {
                "type":"ServiceDescriptor",
                "name":"httpsCert",
                "certType":"cert",
                "dnsNames":["poc.rhynorater.com"],
                "issuer":"C=US, O=Let's Encrypt, CN=Let's Encrypt Authority X3",
                "sha256":"aeb46e0cbf44f8065aac6bd5d3f07f3b5f62075e6840aaeb40b8959f9f6c0a2d",
                "pubkeySha256":"d7f806a84a8d52023f8be0cb7981de753a669bfa1980ac8ef1e7b5992c0dff80",
                "notBefore":"2018-08-12T23:47:38-00:00",
                "notAfter":"2018-11-10T23:47:38-00:00",
                "logs":[{"id":"7ku9t3XOYLrhQmkfq+GeZqMPfl+wctiDAMR7iXqo/cs=","index":385319610,"timestamp":"2018-08-16T00:20:43.850-00:00"},{"id":"pLkJkLQYWBSHuxOizGdwCjw1mAT5G9+443fNDsgN3BA=","index":346479511,"timestamp":"2018-08-16T00:03:21.975-00:00"},{"id":"pFASaQVaFVReYhGrN7wQP2KuVXakXksXFEU+GyIQaiU=","index":333727869,"timestamp":"2018-08-13T00:47:39.051-00:00"}],
                "data":"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"

            }
        ]
    }
}
```
