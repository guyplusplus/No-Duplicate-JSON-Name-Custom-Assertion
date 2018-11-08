## No Duplicate JSON Name

Duplicate name in a JSON object is actually allowed but not recommended. For example `{"a":1, "a":2}`. For reference [JSON Object RFC 7159](https://tools.ietf.org/html/rfc7159#section-4) where SHOULD is defined in [Key words RFC 2119](https://tools.ietf.org/html/rfc2119).

To avoid any doubt, this assertion parses a JSON message inside the request object ${request.mainpart} and detects any possible duplicated name in any object contained in it. In the case the JSON request can not be parsed, this assertion does not fail, the service logic continues.

The first duplicated name found is stored in the context variable 'duplicatedName', in a JSON path format, for example `$.a`. In case no duplication found, this variable is set to empty.

The assertion performance is very good as the JSON object is parsed via JSON stream.

**Warning:** use this assertion after the request JSON object size is bounded, typically via a 'Protect Against JSON Document Structure Assertion' and set 'container depth' and 'object entry count' with reasonable values.
