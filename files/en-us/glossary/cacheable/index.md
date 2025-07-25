---
title: Cacheable
slug: Glossary/Cacheable
page-type: glossary-definition
sidebar: glossarysidebar
---

A **cacheable** response is an HTTP response that can be cached, that is stored to be retrieved and used later, saving a new request to the server. Not all HTTP responses can be cached; these are the constraints for an HTTP response to be cacheable:

- The method used in the request is _cacheable_, that is either a {{HTTPMethod("GET")}} or a {{HTTPMethod("HEAD")}} method. A response to a {{HTTPMethod("POST")}} or {{HTTPMethod("PATCH")}} request can also be cached if freshness is indicated and the {{HTTPHeader("Content-Location")}} header is set, but this is rarely implemented. For example, Firefox does not support it ([Firefox bug 109553](https://bugzil.la/109553)). Other methods, like {{HTTPMethod("PUT")}} or {{HTTPMethod("DELETE")}} are not cacheable and their result cannot be cached.
- The status code of the response is _known_ by the application caching, and is _cacheable_. The following status codes are cacheable: {{HTTPStatus("200")}}, {{HTTPStatus("203")}}, {{HTTPStatus("204")}}, {{HTTPStatus("206")}}, {{HTTPStatus("300")}}, {{HTTPStatus("301")}}, {{HTTPStatus("404")}}, {{HTTPStatus("405")}}, {{HTTPStatus("410")}}, {{HTTPStatus("414")}}, and {{HTTPStatus("501")}}.
- There are no specific headers in the response, like {{HTTPHeader("Cache-Control")}}, with values that would prohibit caching.

Note that some requests with non-cacheable responses to a specific URI may invalidate previously cached responses from the same URI. For example, a {{HTTPMethod("PUT")}} to `/pageX.html` will invalidate all cached responses to {{HTTPMethod("GET")}} or {{HTTPMethod("HEAD")}} requests to `/pageX.html`.

When both the method of the request and the status of the response are cacheable, the response to the request can be cached:

```http
GET /pageX.html HTTP/1.1
(…)

200 OK
(…)
```

The response to a {{HTTPMethod("PUT")}} request cannot be cached. Moreover, it invalidates cached data for requests to the same URI using {{HTTPMethod("HEAD")}} or {{HTTPMethod("GET")}} methods:

```http
PUT /pageX.html HTTP/1.1
(…)

200 OK
(…)
```

The presence of the {{HTTPHeader("Cache-Control")}} header with a particular value in the response can prevent caching:

```http
GET /pageX.html HTTP/1.1
(…)

200 OK
Cache-Control: no-cache
(…)
```

## See also

- Details about [methods and caching](https://httpwg.org/specs/rfc9110.html#rfc.section.9.2.3) are provided in the HTTP specification.
- Description of common cacheable methods: {{HTTPMethod("GET")}}, {{HTTPMethod("HEAD")}}
- Description of common non-cacheable methods: {{HTTPMethod("PUT")}}, {{HTTPMethod("DELETE")}}, often {{HTTPMethod("POST")}}
