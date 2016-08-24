---
layout: page
title: "XLXS to XMLSIE conversion"
category: tool
date: 2016-08-23 17:25:27
order: 2
---
While authoring this document, a simple software was developed in order to convert [the existing open publication of
accounts payable monthly distributed by Örebro kommun](http://www.orebro.se/36465.html). This software accepts
XLSX-files, convert them to tab-separated CSV files, and produce an XMLSIE-file as output.

The input format is six columns with a header row:

1. Payer
2. Supplier name
3. Supplier organization number
4. Invoice internal identity
5. Account number and optionally a descriptive name (why isn’t this two columns?)
6. Amount debited to account

Account types are converted from the Swedish BAS-standard, which means that the first number in the account is an
indicator for the account type:

1. Assets
2. Liabilities
3. Incomes
4. Costs

The Örebro ledger of accounts also contains accounts starting at 5, 6, 7 and 8. Any account not known to the standard
BAS ledger of accounts will therefore be treated as a cost account. This is probably safe in all cases as this project
is about account payables: costs.

* [Deployed conversion tool](https://xmlsie.sambruk.kodapan.se/convert.html)
* [Github project page](https://github.com/kodapan/xmlsie-tools)

## Example of Örebro-style table
An excerpt from [November 2013](http://www.orebro.se/download/18.2eb6484c142f02427ba800010581/1392724243768/Leverant%C3%B6rsfakturor+2013-11.xls)

|Payer|Supplier|Supplier number|Invoice|Account|Amount|
|-----|-------------|----------------------------|--------------|-------|------|
|STÖ Teknisk nämnd övrigt|HEWLETT-PACKARD SVERIGE AB|556084-2139 |11476708|76500 Avg kurser konf studieb mässor|34 400|
|BGY Gymnasienämnd|LÄRA FÖR LIVET|556509-5238 |11584196|76500 Avg kurser konf studieb mässor|3 214,32|
|BGY Gymnasienämnd|LÄRA FÖR LIVET|556509-5238 |11584196|76500 Avg kurser konf studieb mässor|3 214,28|
|OÖN Områdesnämnd Östernärke BoU|SODEXO AB |556232-7873 |11584624|61301 Lokalvård ex städning|587,12|
|OÖN Områdesnämnd Östernärke BoU|SODEXO AB |556232-7873 |11584985|61301 Lokalvård ex städning|391,75|
