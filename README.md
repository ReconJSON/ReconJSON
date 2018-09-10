# [DRAFT] ReconJSON - A JSON-based Recon Data Standard

ReconJSON is a project dedicated to creating a flexible and consistent JSON format across popular recon tools. ReconJSON's format (obviously) is a valid JSON structure. This structure is designed to hold information about Hosts. Hosts objects are described by the set of attributes and other types defined in the standard below. Additions can be requested via the protocol in the "Contributing" section. 

## Structure

A file the conforms to the ReconJSON standard MUST have the `.json` extension. Any name for the file is permitted. 
The internal structure of a ReconJSON file MUST be as follows:

```
[
{"type":"Host"},
{"type":"Host"},
{"type":"Host"},
{"type":"Host"}
]
```

The first line of a ReconJSON file MUST be a left bracket `[` (ASCII 91) and the last line MUST be a right bracket `]` (ASCII 93). In between these brackets MUST be one or more `Host` objects. These objects MUST be collapsed JSON objects stored on a single line. These lines MUST be separated by a comma `,` (ASCII 44) and a single linefeed character `\n` (ASCII 10). The `Host` object on the last line MUST NOT have a trailing comma `,` (ASCII 44), but MUST have a trailing linefeed character `\n` (ASCII 10).

This format is pure JSON, with the `Host` objects collapsed into a single line. The reasoning behind this decision is to provide a file that can easily be parsed by programming languages' JSON libraries while also producing a file that is grep-able and one which a simple `wc -l` command will immediately convey the correct number of hosts to the user (number of lines - 2). 

When placing data into arrays, the data SHOULD be sorted alphabetically (or numerically) if not otherwise specified. 


## Types

The following types are defined within the ReconJSON standard:
* `Host`: The object used to describe a specific profile of a computer. For more details, see [Host.md](/Host.md)
* `Port`: The object used to describe the status of the ports on a specific `Host`. For more details, see [Port.md](/Port.md)
* `DNS`: The object used to describe the DNS configuration of a specific `Host`. For more details, see [DNS.md](/DNS.md)
* `Service`: The object used to describe a specific program running on a `Port` object. For more details, see [Service.md](/Service.md)
* `ServiceDescriptor`: The object used to describe a specific attribute or configuration of the `Service` object. For more details, see both the `ServiceDescriptor` spec doc ([ServiceDescriptor.md](/ServiceDescriptor.md)) and the `ServiceDescriptors` folder ([ServiceDescriptors](/ServiceDescriptors))


## Contributing

If you note any issues with ReconJSON or would like to request an attribute or object be added to the standard, please submit an issue per the templates in the [docs](docs/) folder. Before submiting any issues please use Github's Issue Search feature to check if there is a similar issue already submitted.
