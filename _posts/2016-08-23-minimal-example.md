---
layout: page
title: "Minimal example"
category: doc
date: 2016-08-23 18:15:48
order: 3
---

This is an XMLSIE 1.0 file containing only a single journal with a single invoice from a single supplier with
a single journal. It is, for the scope of this project, a minimal example of an accounts payable publication.

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<SIE>
 <Company
   name="Örebro kommun" organizationalnumber="212000-1967"
   addressLine1="BOX 30000" postcode="701 35" city="Örebro" countryCode="SE"
   homepage="http://www.orebro.se/"
 />
 <Currency>SEK</Currency>
 <Accounting>
  <Accounts>
   <Account>
    <Id>60150</Id>
    <Name>Lokalhyror parkering garage</Name>
    <Type>COST</Type>
   </Account>
  </Accounts>
  <FinancialYears>
   <FinancialYear start="2016-04-01+02:00" end="2016-05-01+02:00">
    <Journals>
     <Journal>
      <Id>27</Id>
      <Name>VVV Vård- och omsorgsnämnd väster</Name>
      <JournalEntry>
       <Id>322</Id>
       <LedgerEntry>
        <AccountId>60150</AccountId>
        <Amount>57.0</Amount>
       </LedgerEntry>
      </JournalEntry>
    </Journals>
   </FinancialYear>
  </FinancialYears>
 </Accounting>
 <AccountsPayable>
  <Suppliers>
   <Supplier>
    <SupplierId>0</SupplierId>
    <SupplierName>ÖREBROBOSTÄDER AB</SupplierName>
    <SupplierOrganizationalNumber>556334-8449</SupplierOrganizationalNumber>
   </Supplier>
  </Suppliers>
  <Invoices>
   <Invoice>
    <SupplierId>0</SupplierId>
    <InternalId>835595</InternalId>
    <GrossAmount>57.0</GrossAmount>
    <JournalInfo>
     <FinancialYear>2016-04-01+02:00</FinancialYear>
     <JournalId>27</JournalId>
     <JournalEntryId>322</JournalEntryId>
    </JournalInfo>
   </Invoice>
 </AccountsPayable>
</SIE>

```

