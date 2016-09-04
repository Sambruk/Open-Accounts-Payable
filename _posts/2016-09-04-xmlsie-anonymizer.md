---
layout: page
title: "XMLSIE anonymizer"
category: tool
date: 2016-09-04 17:50:13
order: 3
---
A tool to do handle
[the potential legal problems with PUL and sole traders](https://sambruk.github.io/Open-Accounts-Payable/doc/legal-considerations.html)
has been developed. It accepts XMLSIE and returns a new XMLSIE where all potential sole traders (based on their
organization number) has been grouped in a single supplier.

Be aware that although it will catch all sole traders, it might also catch some false positives, i.e. organisations that
are not sole traders might end up in this group and be anonymized.

The deployed service is encrypted and will not remember any data sent to it. If you worry about legal problems you
should consider running this service on a local machine.

* [Deployed project](https://xmlsie.sambruk.kodapan.se/anonymize.html)
* [Github project page](https://github.com/kodapan/xmlsie-tools)