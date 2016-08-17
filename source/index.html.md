---
title: Indexer API Reference

language_tabs:
  - shell
  - python

toc_footers:
  - © ARM Ltd. Copyright 2016

includes:
  - get
  - list
  - post
  - patch

search: true
---

# Introduction

Welcome to the ARM mbed Indexer API! You can use this API to get data about mbed
projects, create new projects in the indexer, or modify existing projects.

A "project" is simply a resource which describes where to find source code for
a program that is compatible with an ARM mbed enabled platform. The resource also
includes lots of other useful data which describes the project. This data can be
used by other services enabling features such as importing an mbed project into
a development environment, or looking up which projects are compatible with a
given mbed platform.

The API supports features such as pagination of results, and sorting & filtering
of results.

The API is designed to conform to the [JSON API spec](http://jsonapi.org), so both
server and client are obliged follow the specification in order to process valid
requests.


# The JSON API Content Type
All requests and responses which carry a JSON document must set the `Content-Type`
header to the JSON API content type to: `application/vnd.api+json`

Also the relevant `Accept` headers can be set in accordance with the spec.
Please see the section about [content negotiation](http://jsonapi.org/format/#content-negotiation-clients)
in the JSON API spec for more information on client responsibilities when handling JSON API requests/responses.


# Authentication
To do...


# Projects API
