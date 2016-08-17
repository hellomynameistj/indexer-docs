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

# mbed Project Indexer

Welcome to the mbed Indexer API documentation! You can use this API to get data
about mbed projects, create new projects in the indexer, or modify existing
projects.

A "project" is simply a resource which describes where to find source code for
a program that is compatible with an [ARM mbed enabled platform](https://developer.mbed.org/platforms/?mbed-enabled=15).
The resource also includes lots of other useful data which describes the project.
This data can be used by other services enabling features such as importing an
mbed project into a development environment, or looking up which projects are
compatible with a given mbed platform.

The API supports features such as pagination, sorting, and filtering of results.

The API is designed to conform to the [JSON API spec](http://jsonapi.org), so both
server and client are obliged follow the specification in order to process valid
requests.


# The JSON API Content Type
All requests and responses which carry a JSON document must set the `Content-Type`
header to the JSON API content type to: `application/vnd.api+json`

Also the relevant `Accept` headers can be set in accordance with the spec.
Please see the section about [content negotiation](http://jsonapi.org/format/#content-negotiation-clients)
in the JSON API spec for more information on client responsibilities when handling JSON API requests/responses.


# The Project Resource
Projects have a list of attributes, many of which are derived from metadata from
the project's repository. These attributes will appear in the JSON data of a
response from the API. Below is a table with descriptions of each of the project
resource's attributes, and whether they are editable via the indexer API.

Attribute      | Description                                                                                           | Editable
-------------- | ----------------------------------------------------------------------------------------------------- | --------
id             | A UUID according to [RFC 4122](https://tools.ietf.org/html/rfc4122.html) which identifies the project | <i class="fa fa-times"></i>
title          | The title of the project                                                                              | <i class="fa fa-check"></i>
description    | A long description of the project                                                                     | <i class="fa fa-check"></i>
url            | The URL of the project's repository                                                                   | <i class="fa fa-check"></i>
version        | The version of this program - e.g. a hash of a git commit or release tag                              | <i class="fa fa-check"></i>
provider       | The version control system provider for the repo                                                      | <i class="fa fa-times"></i>
protocol       | The version control protocol, e.g. Git, Mercurial, etc.                                               | <i class="fa fa-times"></i>
imports        | The number of times this project has been imported into official mbed development tools               | <i class="fa fa-times"></i>
repo_owner     | The user who own's this project's repo, e.g. a GitHub or Bitbucket username                           | <i class="fa fa-times"></i>
repo_name      | The repo's name as it appears in the repo URL                                                         | <i class="fa fa-times"></i>
release_date   | The release date of this version                                                                      | <i class="fa fa-times"></i>
license        | The license of the program                                                                            | <i class="fa fa-times"></i>
commit_count   | The number of commits to this project's repo                                                          | <i class="fa fa-times"></i>
fork_count     | The number of times this project has been forked                                                      | <i class="fa fa-times"></i>
branch_count   | The number of branches this project's repo has                                                        | <i class="fa fa-times"></i>
follower_count | The number of followers/stars/watchers for this repo                                                  | <i class="fa fa-times"></i>
summary        | A short summary of the repo (comes from repo metadata)                                                | <i class="fa fa-times"></i>
readme         | The README file from the repo                                                                         | <i class="fa fa-times"></i>


# Authentication
To do...


# Projects API
