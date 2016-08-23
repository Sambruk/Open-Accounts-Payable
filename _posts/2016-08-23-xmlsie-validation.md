---
layout: page
title: "XMLSIE validation"
category: tool
date: 2016-08-23 17:25:13
order: 1
---
As XMLSIE is defined by an XML-schema (XSD) there is virtually an unlimited number of softwares that can validate the
document structure. XSD will however not validate the integrity of the actual content, for instance the internal
references between objects within XMLSIE, such as the existence of an account referenced to from a ledger entry.

A tool to do handle this has been developed and is available as source code and deployed service:

* [Deployed project](https://xmlsie.sambruk.kodapan.se/validate.html)
* [Github project page](https://github.com/kodapan/xmlsie-tools)