---
layout: page
title: "XMLSIE anonymizer"
category: tool
date: 2016-09-04 17:50:13
order: 3
---
This is a tool for anonymizing Swedish sole traders suppliers in an XMLSIE file.

See
[the potential legal problems with PUL and sole traders](https://sambruk.github.io/Open-Accounts-Payable/doc/legal-considerations.html)
for further information.

The tool accepts XMLSIE and returns a new XMLSIE where all potential sole traders (based on their
organization number) will be removed and all references to them replaced by a new single anonymous supplier entry.

Be aware that although it will catch all sole traders, it might also catch some false positives, i.e. organisations that
are not sole traders might end up in this group and be anonymized.

A sole trader organization number is according to the logics of this tool defined by:
`yyMMdd-nnnc`, where `yyMMdd` is a valid gregorian date and where `c` is the modulus 10 luhn checksum of the 9 preceding digits.

The supplier created by this tool will look like this:
```xml
<Supplier>
    <SupplierId>SOLE_TRADERS</SupplierId>
    <SupplierName>Anonymized sole traders</SupplierName>
    <SupplierOrganizationalNumber>000000-0000</SupplierOrganizationalNumber>
</Supplier>
```

The deployed service is encrypted and will not remember any data sent to it. If you worry about legal problems you
should consider running this service on a local machine.


* [Deployed project](https://xmlsie.sambruk.kodapan.se/anonymize.html)
* [Github project page](https://github.com/kodapan/xmlsie-tools)


