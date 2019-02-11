# serviceDescriptors

The ReconJSON standard defines a ```serviceDescriptor``` object as follows:

> The serviceDescriptor object SHALL be used to describe a specific attribute or configuration of the Service object.There MAY be several serviceDescriptor objects to a single Service object. Since the serviceDescriptor object is the object in which the specifics about programs are to be stored, it is impossible for the authors of this standard to construct a serviceDescriptor object for each and every use case. As a result, community sourcing of this attribute is needed.

The `serviceDescriptor` objects SHOULD be contributed by the community via pull request to describe all the various pieces of technology that must be described. 

## How to contribute

In order to contribute, please search the Github Issues for a similar request. If there is one, please comment on that with your desired change. If there is no a `serviceDescriptor`, please see the `ServiceDescriptorTemplate.md` file in the /docs folder. Please fill out that template to describe the `serviceDescriptor`. Submit this template as an `Issue` in Github and the team will assess it as soon as possible. 
