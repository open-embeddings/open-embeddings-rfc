---
title: RFC
layout: page
nav-include: true
---
# Open Embeddings SiteList - Draft Specification

**This is a living document.**

## Abstract

The Open Embeddings specification defines a standardized JSON format for content providers to expose embeddings of their content at site level.

## Technical Specification

### Locations
1. /open-embeddings.json
2. /.well-known/open-embeddings.json
3. /query/() # API Service
4. http://hub.open-embeddings.org/ # Indexer Service

### Robots.txt / llms.txt
 OE should not conflict with the directives of `robots.txt` or `llms.txt`

### Signing Authority [for examples, example.com]
1. Any email address @example.com is considered authoratative for now
1. Any other address is subordinate to the example.com address
1. The indexer service



### File Format

Open Embeddings uses JSON format with the following structure:

```json
{
  "version": "1.0",
  "metadata": {
    "generated": "2024-01-15T10:30:00Z",
    "generator": "open-embeddings-tool/1.0",
    "license": "CC-BY-4.0"
    "URI-Scope": "https://example.com/",
    "Signed-By": "nlange@example.com"
    "Signature": "sha256:abc123...", #
  },
  "content": [
    {
      "uri": "/path/to/content",
      "content_type": "text/html",
      "last_modified": "2024-01-15T09:00:00Z",
      "title": "Content Title",
      "dynamic-content": false, # optional flag [ see faq ]
      "embeddings": [
        {
          "model": "text-embedding-ada-002",
          "version": "1.0",
          "dimensions": 1536,
          "last_generated": "2024-01-15T09:00:00Z",
          "vector": [0.023, -0.019, 0.041, "..."],
          "metadata": {
            "chunk_size": 512,
            "overlap": 0,
            "language": "en"
          }
        }
      ]
    }
  ]
}
```


### Hard Implementation Problems

**Model Sprawl**: Can we build on recent academic work to generalize on a framework to transform between embedding spaces for multi-modal models?

**Cache-Invalidation**: Trusting the embeddings and metadata - ensuring content freshness and embedding accuracy.

## References

- [RFC 2119 - Key words for use in RFCs](https://tools.ietf.org/html/rfc2119)
- [RFC 8259 - The JavaScript Object Notation (JSON) Data Interchange Format](https://tools.ietf.org/html/rfc8259)
- [Well-Known URIs](https://tools.ietf.org/html/rfc5785)

---
