---
layout: page
title: "Why XMLSIE?"
category: doc
date: 2016-08-23 16:56:07
order: 1
---
## SIE

SIE (Standard Import and Export) is the de facto accounting data interchange format of Sweden, an open specification
developed since 1992 by [the SIE consortium](http://sie.se) for easy migration of accounting data, typically when
passing on bookkeeping from a company to an external accounting or auditing firm.

## XMLSIE

[XMLSIE 1.0](http://www.sie.se/?page_id=24) is an XML representation of SIE, introduced in 2003.
Sometimes also known as SIE-XML.

XMLSIE 1.0 is well developed and specified. It handles all the requirements and more spanning this Sambruk open data
project. We choose a subset of XMLSIE as the common denominator of all data that will be published, but it also allows
any party that wish to publish more accounting data to do so in a predefined and well specified way that spans much
further than accounts payable.

So far no one involved in this Sambruk open data project has been able to identify a reason to invent a new standard.
A majority of the accounting software in Sweden have an import and export function for SIE. Developers of accounting
software are used to the standard, it is simple to understand for those with basic knowledge about accounting data,
it is not too complex nor does it limit this project.

This project does not aim at using XMLSIE in order to publish a true representation of the original data source,
the internal bookkeeping system. Published data should of course be valid and correct, we do however use XMLSIE
in order to publish a subset of accounts payable meta-data rather than a partial clone of the source database.
Therefor internal identities of suppliers, journal entries, etc, may differ with those in the data source.
Only the internal identity of invoices must be guaranteed to be corresponding with the data source.

