---
id: nlrddzog5fikvb3m0vup488
title: API Bites — Payload Conventions
desc: ""
updated: 1669536838759
created: 1669536544480
---

Encoding, Data Formats and Document Structure

> https://medium.com/@trgoodwill/api-bites-payload-conventions-76ffde7f5eb2

API Development Standards are a focused collection of imperatives, conventions and guidance, and are intended to improve the **_consistency, stability, generality, predictability and usability of business resource APIs_**.

_The following_ **_‘sample’ set of standards_** _is focused purely on payload conventions. More to come…_

## Encoding

Unicode Transformation Format-8 (UTF-8) is the standard encoding type for all text and textual representations of data through APIs and is the default encoding for JSON (RFC 7159). UTF-8 encoding must be adhered to for all APIs published across the enterprise and externally. Other encodings may be used for ‘private’ partner APIs if and only if there are technical limitations to using UTF-8.

## Interoperable Data Formats

### JSON as the Default Format

All new and uplifted API implementations _really should_ support the JSON data format at a minimum. This does not preclude other media types, such as XML.

JSON payload must comply with API Request and API Response document structure requirements. JSON ‘RequestBody’ and ‘Responses’ payloads should be defined under the OpenAPI 3.0 ‘application/json’ content keyword.

### Other Media Types

It is possible to request more than representation the same resource if multiple supported media types are specified in the OpenAPI 3.0 API specification.

The returned media type must conform to the value provided in the API request Accept header, or the 1st supported media type if multiple values are specified. The default content type is JSON (application/json).

If the requested media type(s) are unsupported, the server is expected to return an HTTP response status ‘415 — Unsupported Media Type’.

The practice of specifying media type with a resource label should be avoided for resource APIs documented with an OpenAPI specification (e.g. avoid ‘resource/{resourceId}.json’).

### **Date-Time Format**

A consistent date-time format, conforming to [RFC3339](https://xml2rfc.tools.ietf.org/public/rfc/html/rfc3339.html#anchor14), **_should_** be used. RFC3339 compliant date-time formats are provided by the OpenAPI 3.0 specification. Date-time fields should be defined in an API specification in the following manner:

- Date fields should be defined as type = “string”, format=”date”.
- Datetime fields should be defined as type = “string”, format=”date-time”.

The RFC 3339 profile of the standard ISO 8601, in Coordinated Universal Time (UTC), is the standard datetime format for data and timestamp fields in enterprise business resource APIs. The date format is <yyyy-mm-dd> while timestamp format is <yyyy-mm-dd>T<hh:mm:ss>Z. Time duration values should be strings, formatted as recommended by ISO 8601, e.g. “P3Y6M4DT12H30M5S”. Any other representation of time in the source system should be converted to and from these standard formats when exchanging data via APIs.

## Naming Conventions

### Field Names

For request and response body field names (and query parameter names), case MUST be consistent. camelCase should probably be the default choice unless there are compelling reasons to go a different way. e.g. `"familyName" : "Jones"`

Fields that represent arrays should be named using plural nouns (e.g. ‘products’).

### Resource Names

Resource names must be plural nouns when referring to a resource collection (there are potentially a number of instances) e.g. ‘/**customers’**. A singleton, such as ‘/customers/1234/**cart’** must be singular.

https://api.myorg.com/store/v1/**customers**

Resource names should be lower-case and use only alphabetic characters, with hyphens employed to separate words in the URI. URIs are the only place where hyphens are used as a word separator. In all other situations, the word separation scheme should align with enterprise field naming conventions (e.g. camelCase or snake_case).

### Resource Identifiers

A resource identifier can be a string or numeric value, and must be URL safe. A protected or confidential resource identifier must be un-guessable and non-sequential, providing maximum abstraction from Personally Identifiable Information, primary keys, and time or order of creation. This requirement may be met with a randomly generated unique identifier, e.g.

/v1/applicants/**538d9bb1**

The resource identifier must be immutable.

### Resource References

Resource identifiers returned with the core data should be referenced consistently — a standard should be mandated.

The most popular schemes are:

- Return an “id” field. e.g. `"id" : "12B34C"`. The name of the resource is implied, having been addressed in the URL.
- Return an unambiguous concatenation of the resource name followed by the “Id” designation, e.g. `"customerId" : "12B34C"`.

All **_external resource id references_** should in any case be concatenation of the resource name followed by the “Id” designation, e.g. `"orderId" : "34C56D"`.

## Document Structure

### Root Level Object

Request and response documents containing JSON data must contain a root level JSON object. This object defines the JSON document’s root. Obviously this does not apply to body-less API requests and responses, such as a GET request. e.g.

**POST** /v1/persons{  
 "familyName": "SMITH",  
 "givenName": "Jane",  
 "birthDate": "1992-01-01"  
}

### Flat Structure

There is little argument about the need for experience APIs to deliver the leanest, flattest JSON structures possible, _as per the above example_. In most scenarios, this imperative will also apply to business resource APIs, however alignment with regulatory or industry frameworks/formalisms will occasionally require a more structured approach. In any case, data structures should be as flat and lean as possible — expressing composability and cohesion in alignment with [core domain and conceptual contours principles.](https://medium.com/@trgoodwill/where-do-business-resource-apis-come-from-472cc8422dec)

### The “data” Object

Regulatory or industry frameworks _may_ facilitate the transmission of structured metadata alongside business data (e.g. Open Banking), and when this is a significant organizational use-case, it may be advisable for the enterprise to consistently encapsulate business data in a “data” object.

The root object **_may_** in this case optionally contain a ‘meta’ top-level member in addition to the data member. The ‘meta’ object is used to provide additional information such as copyright, timestamps, origin, ownership, or other contextual data for regulatory or temporal analytical purposes. e.g.

**POST** /v1/applications{  
 "data": {  
 "familyName": "SMITH",  
 "givenName": "Jane",  
 "birthDate": "1992-01-01"  
 },  
 "meta": {  
 "classification": "sensitive",  
 "consent": "538d9bb1–95c9–4ceb-864c-80887776573"  
 }  
}

This requirement would apply to both request and response documents. When taking this approach, the “links” (or “\_links”) object is also top-level and returned as a peer of the “data” member. E.g.

**GET** /v1/applications/808877765733**Response** 200 OK  
Content-Type: application/json; charset=utf-8{  
 "data": {  
 "applicationId": "808877765733**",  
** "applicationDate": "2022-01-01",  
 "applicationStatus": "submitted",  
 },  
 **"links": {  
 "memberReferrals": "/v1/applications/12345/memberReferrals",  
 "cancelApplication": "/v1/applications/12345/cancel"  
 }**  
}

Reserved top-level properties in this scheme might include (at least): _“data”, “meta”, “links”_ (and/or _“\_links”_)_, “messages”, “risk”_ (Open Banking) and _“errors”._

It is worth taking the time to validate the requirement for such a structure. _Note that_ **_in an OAuth2 context, the token should be the source-of-truth_** _for contextual information such as originating user and client system, and tokens may, by agreement or by virtue of applicable extended frameworks, carry additional claims relevant to the user and system context._

## Request Document

### Resource Instances and Collections

Client systems may interact with a single resource, or with the resource collection.

To interact with a single, specific manifest, for example, GET/HEAD, PUT, PATCH or DELETE requests are sent to the URI `/v1/manifests/{manifestId}`

To interact with the collection of manifests, GET/HEAD or POST (and potentially, QUERY) requests are sent to the resource collection URI `/v1/manifests`

### Request Payload

Resource instance payloads will be substantially similar across POST (request), GET (response) and PUT (request), and these should ideally reference a shared OpenAPI schema definition. PATCH payload will contain an optional subset of resource data.

_Note that the ‘resourceId’ member (eg ‘customerId’) is not required (nor should it be supported) when a new resource is POSTed to the service. The resource Id is owned by the resource service and is returned in the POST response._

```json
{
  "familyName": "Jones",
  "givenName": "James",
  "birthDate": "1983-01-01"
}
```

## Response Document

### Media Type

The returned media type must conform to the value provided in the API request Accept header, or the 1st supported media type if multiple values are specified.

In the absence of an Accept header, the default content type should be JSON (application/json). If the requested media type is unsupported, the server must return an HTTP response of 415 — Unsupported Media Type.

### Resource Identifier

representations of resource data in a response document will always include the unique resource Id, e.g. `"customerId" : "12B34C"`. Refer to the “Naming Conventions” section above.

### Related Resources

A GET request to the parent resource should return ‘core’ resource data only. _Core and sub resource concepts are discussed_ [_here_](https://medium.com/@trgoodwill/where-do-business-resource-apis-come-from-472cc8422dec)_._

References to existentially related resources and sub-resources should be unambiguous, consisting of a concatenation of the resource name followed by the “Id” designation, e.g. `"orderId" : "34C56D"`.

Ideally, referenced resources should be nested, and contain the resource id together with the minimum of non-sensitive data pertinent to the context. e.g.

```json
{
  "applicationId": "808877765733",
  "applicationDate": "2022-01-01",
  "applicationStatus": "submitted",
  "applicant": {
    "applicantId": "1234",
    "name": "John Smith"
  }
}
```

### Link Relations and HATEOAS

Existentially related sub-resources may **_optionally_** be represented as links, however, take care linking versioned APIs external to the current namespace, as it creates dependencies, and such links may in fact be invalid for some clients when these services undergo major version changes. It is best to reserve links for operations and resources within the same versioned namespace.

When links are employed as HATEOAS ([**the engine of application state**](https://medium.com/@trgoodwill/the-engine-of-application-state-92bfdce0d41c)), applicable, adjacent state-lifecycle affordances are presented as links in the payload. In a managed API context, the name of every HATEOAS link should correspond to a documented operation with an explicitly defined request and response document, referring to an **_operationId_** or to an OAS 3 **_link name_**.

Links should employ the most efficient link format for the use-case. The simple format employed by the [Open Banking standard](https://openbanking.atlassian.net/wiki/spaces/DZ/pages/1077805207/Read+Write+Data+API+Specification+-+v3.1.2#Read%2FWriteDataAPISpecification-v3.1.2-Links) is preferential to unnecessarily verbose mechanisms (such as HAL) which are [poorly aligned with specification-first API management](https://medium.com/@trgoodwill/the-engine-of-application-state-92bfdce0d41c). _HOWEVER_, development framework support should be considered.

_More on HATEOAS and links in the article_ [**_The Engine of Application State_**](https://medium.com/@trgoodwill/the-engine-of-application-state-92bfdce0d41c)**_._**

Example:

**GET** /v1/applications/808877765733**Response** 200 OK
Content-Type: application/json; charset=utf-8{
"applicationId": "808877765733**",
** "applicationDate": "2022-01-01",
"applicationStatus": "submitted",
**"links": {
"memberReferrals": "/v1/applications/12345/memberReferrals",
"cancelApplication": "/v1/applications/12345/cancel"
}**
}

### Pagination

Resource servers and their APIs **SHOULD** support pagination to assist in the management of payload size and performance.

Pagination strategies include (but are not limited to): page-based, offset-based, and cursor-based. The page query parameter can be used as a basis for any of these strategies. For example, a page-based strategy might use query parameters such as

- page\[number\] and page\[size\] e.g. `?page[number]**=**2&page[size]**=**10`
- an offset-based strategy might use page\[offset\] and page\[limit\].
- a cursor-based strategy might use page\[cursor\].

As with link notation, the pagination notation supported by development frameworks in common use should be considered. _Pagination notation_ **_MUST_** _be consistent with_ [_hyperlink/HATEOAS conventions_](https://medium.com/@trgoodwill/the-engine-of-application-state-92bfdce0d41c)_._

Always refer to a URL-Path (URL part following the hostname and port).

“prev”: “/v1/resources/?page\[number\]=2&page\[size\]=1”

Pagination links MUST appear in the links object that corresponds to a collection. The following keys **SHOULD** be provided for page-based pagination links:

- **_self_** : the current page of data
- **_first_** : the first page of data
- **_prev_** : the previous page of data
- **_next_** : the next page of data
- **_last_** : the last page of data

```json
{
  "links": {
    "self": "/v1/orders?page[number]=3&page[size]=1",
    "first": "/v1/orders?page[number]=1&page[size]=1",
    "prev": "/v1/orders?page[number]=2&page[size]=1",
    "next": "/v1/orders?page[number]=4&page[size]=1",
    "last": "/v1/orders?page[number]=13&page[size]=1"
  }
}
```

**Query Parameter Syntax and Amazon API Gateways**

Note that native Amazon API Gateways do not fully implement [RFC 3986](https://tools.ietf.org/html/rfc3986) and are more restrictive — query parameters must conform to the regular expression `^[a-zA-Z0–9:._$-]+$`

### Collections of Resources

A GET performed on a resource collection (without specifying a resource Id) will return potentially multiple resource instances in a “data” array. e.g.

**GET** /v1/applications**Response** 200 OK
Content-Type: application/json; charset=utf-8{
"data": \[
{
"applicationId": "808877765733**",
** "applicationDate": "2022-01-01",
"applicationStatus": "submitted"
},
{
"applicationId": "80851456484**",
** "applicationDate": "2022-06-01",
"applicationStatus": "pending"
}
\]
}

The response to a GET on a collection **_must return a top-level data array even if only one record exists_**, or meets the filter criteria. This rule does not apply when no records exist, or meet filter requirements, in which case a response of 404 — Not found should be returned.

Uncontrolled arrays containing large data sets or large binary objects such as documents or images, must not be returned. **_Large arrays must be controlled by pagination_**. It is suggested that payload size should not exceed 2 Mb— primarily for the sake of performance and composability, and because this is a legacy default payload maximum for some platforms. Avoid exceeding 10 Mb at all costs — it is a hard limit for several platforms.

A POST may also be performed on a resource collection to create a new instance of the resource. The server should return a ‘Location’ header containing the relative path of the newly created resource, and an ‘id’ field containing the resource identifier. Additional _derived_ data _may_ be returned as deemed appropriate. A links object _may_ be returned if relevant. e.g.

**POST** /v1/applicants
{ "familyName": "Jones",
"givenName": "James",
"birthDate": "1983-01-01"
}**Response** 201 Created
Content-Type: application/json; charset=utf-8
Location: /v1/applicants/538d9bb1–95c9–4ceb-864c-808877765733{
"applicantId": "538d9bb1–95c9–4ceb-864c-808877765733",
}

These are the only operations that may be performed on a collection. Creating or updating multiple resource instances in the same request is not standardized, and should be avoided. There are factors such as receipt acknowledgement and how to handle partial success in a set of batches that add significant complexity.

## Binary and Multi-part Content

Implementation details for large binary uploads are often necessarily different from small JSON payloads (for example virus scanning, different tuning for HTTP variables for efficient compression, different DDOS protection strategies, etc). For these reasons, care needs to be taken with the modeling of binary data to avoid unnecessary imposts on performance and availability.

If at all possible, binary data should be modeled as a dedicated sub-resource on a separate path to facilitate upload and download as discrete operations.

_More on this topic in the article:_ [_Binary and Multi-Part Content_](https://medium.com/@trgoodwill/api-bites-binary-and-multi-part-content-283ef69fc5e9)

## Wrap-up

Governed, opiniated standards and patterns will be required to enable **_seamless interoperability between independent, decoupled domains_**. While sample guidance and exemplars are offered in this article, there is often more than one tried-and-tested approach in any one area of API design — specific tactics and conventions should be tailored to the target environment.

## Related Discussions on Medium

[API Bites — Versioning APIs](https://medium.com/@trgoodwill/api-bites-1af949efdd1b)

[API Bites — API Path Conventions](https://medium.com/@trgoodwill/api-bites-7373b2127ed1)

[API Bites — Filtering Conventions](https://medium.com/@trgoodwill/api-bites-filtering-conventions-8a1a19c03975)

[API Bites — Binary and Multi-Part Content](https://medium.com/@trgoodwill/283ef69fc5e9)

[Modeling Coherent and Composable Business Resource APIs](https://medium.com/@trgoodwill/where-do-business-resource-apis-come-from-472cc8422dec)

[The Engine of Application State. Aligning HATEOAS, Affordances and Business Events](https://medium.com/@trgoodwill/the-engine-of-application-state-92bfdce0d41c)
