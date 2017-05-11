---
layout: page
title: "Excel -> XMLSIE"
category: tool
date: 2016-08-23 17:25:27
order: 2
---
While authoring this document, a simple software was developed in order to convert [the existing open publication of
accounts payable monthly distributed by Örebro kommun](http://www.orebro.se/36465.html). This software accepts
XLSX-files and tab-separated CSV files, from which it produce an XMLSIE-file.

Account types are converted from the Swedish BAS-standard, which means that the first number in the account is an
indicator for the account type:

1. Assets
2. Liabilities
3. Incomes
4. Costs

Any account greater than 3 is treated as a cost account. This is probably safe in all cases as this project
is about account payables: costs.

Since the Örebro file mix account number and account name in the same field and this is not reproducable for some, the tool has been redeveloped to be more configurable. Complete documentation is available in the convertion page.

* [Deployed conversion tool](https://xmlsie.sambruk.kodapan.se/convert.html)
* [Github project page](https://github.com/kodapan/xmlsie-tools)
