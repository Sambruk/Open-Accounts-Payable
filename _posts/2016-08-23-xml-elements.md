---
layout: page
title: "XML elements"
category: doc
date: 2016-08-23 17:07:24
order: 4
---

# SIE, Company and Currency

The root object of the XMLSIE is `<SIE>`, which contains the Company and default currency object. 

There are no requirements to set company information, it does however make it easier for machine readability if
available, compared to parsing it from an URL, file name or what not.

The XSD defines the default currency as SEK if left out, it is still however recommend to explicitly set it to avoid
any problems.

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<SIE>
  <Company
    name="Örebro kommun" organizationalnumber="212000-1967"
    addressLine1="BOX 30000" postcode="701 35" city="Örebro" countryCode="SE"
    homepage="http://www.orebro.se/"
  />
  <Currency>SEK</Currency>
```


# Accounts

For the purpose of this project, a published XMLSIE-file should contain at least all accounts used by any ledger entry
in the file. Since this project is about accounts payable and the scope of this project does not require ledger entries
with, for instance, VAT-account debit and bank-account credit, all accounts listed are probably of the type `COST`.

```xml
<Accounting>
  <Accounts>
    <Account>
      <Id>60150</Id>
      <Name>Lokalhyror parkering garage</Name>
      <Type>COST</Type>
    </Account>
  </Accounts>
```

If you plan to add more complete ledger entries with, for instance, VAT and bank accounts, then your ledger of accounts
must also contain these accounts:

```xml
  <Account>
    <Id>2640</Id>
    <Name>Ingånde moms</Name>
    <Type>LIABILITY</Type>
  </Account>
  <Account>
    <Id>1940</Id>  
    <Name>Bankkonto</Name>
    <Type>ASSET</Type>
  </Account>
</Accounts>
```

# Financial year

All ledger journals are grouped by financial year (_sv: verksamhetsår_). There are no requirements in this project that
the journal entries contains date an invoice was registered, therefore the financial year is recommended to represent
the date range of all journal entries in the file, for instance all of April 2016 in timezone Stockholm/Sweden:

```xml
<FinancialYears>
  <FinancialYear start="2016-04-01+02:00" end="2016-05-01+02:00">
```

If instead each and every journal entry infact have a date stamp, then set financial year as the actual period,
for instance 2016:

```xml
<FinancialYears>
  <FinancialYear start="2016-01-01+02:00" end="2017-01-01+02:00">
```

If the file contains entries that span multiple financial years, then the file should also reflect that, no matter
whether journal entries contains date stamps or not:

```xml
<FinancialYears>
  <FinancialYear start="2015-12-10+02:00" end="2016-01-01+02:00">
    <Journals>
      …
    </Journals>
  </FinancialYear>
  <FinancialYear start="2016-01-01+02:00" end="2016-01-10+02:00">
    <Journals>
      …
    </Journals>
  </FinancialYear>
```


# Journals
Financial years are grouped in journals (_sv: verifikationsserie_). For the scope of this project we use journals to
represent the administration an invoice has been sent to, for instance “BGY Gymnasienämnd” or
“VFH Nämnd för funktionshindrade”.

Journal identity is required in order to associate invoices with a journal entry. The identity is unique only within
the parent financial year.

```xml
<FinancialYears>
  <FinancialYear start="2016-04-01+02:00" end="2016-05-01+02:00">
    <Journals>
      <Journal>
        <Id>0</Id>
        <Name>SPN Programnämnd Samhällsbyggnad</Name>
```


# JournalEntry

Journals are grouped in journal entries (_sv: verifikationer_). Typically a journal entry would represent a single
invoice, but could also be a group of invoices. The association between journal entries and invoices are set in the
invoice object.

Journal entry identity is required in order to associate invoices with a journal entry. The identity is unique only
within the parent journal.

```xml
<Journal>
  <Id>0</Id>
  <Name>SPN Programnämnd Samhällsbyggnad</Name>
  <JournalEntry>
    <Id>0</Id>
```

A recommended and more complete journal entry would also contain a date stamp for when it was registered, and could
also contain a descriptive text.

```xml
<Journal>
  <Id>0</Id>
  <Name>SPN Programnämnd Samhällsbyggnad</Name>
  <JournalEntry>
    <Id>0</Id>
    <Date>2016-04-01+02:00</Date>
    <Text>Inköp av ett och annat, leverantörsfaktura 12356</Text>
    <LedgerEntry>
      …
    </LedgerEntry>
  </JournalEntry>
</Journal>
```

The date stamp is however only correct in case the journal entry is describing a single invoice. In the case of
multiple invoices bundled in the same journal entry it’s more correct to date stamp the individual ledger entries,
especially if the dates differ.

It is recommended that journal entries and ledger entries in the file are listed in chronological order if no date
stamp is listed in journal entries nor ledger entries.


# LedgerEntry

Journal entries are grouped in ledger entries (_sv: verifikationsrad_). Each ledger entry contains a sum of money
debited or credited to an account. For the scope of this project we’re only requiring debit entries to cost accounts,
individual implementations might however contain debit entries to VAT, credit entries to bank accounts, and so on.

```xml
<JournalEntry>
  <Id>0</Id>
  <LedgerEntry>
    <AccountId>60150</AccountId>
    <Amount>57.0</Amount>
  </LedgerEntry>
</JournalEntry>
```

A journal entry could of course contain multiple ledger entries, and in any double-entry bookkeeping system there are
always at least two: debit and credit that balance each other out. In the scope of this Sambruk project there are no
requirements to balance a journal entry, but it would probably be interesting for many consumers if the data was
published. In the following example we’ve added VAT and bank account ledger entries:

```xml
<JournalEntry>
  <Id>0</Id>
  <Date>2016-04-01+02:00</Date>
  <Text>Inköp av ett och annat</Text>
  <LedgerEntry>
    <AccountId>60150</AccountId>
    <Amount>57.0</Amount>
  </LedgerEntry>
  <LedgerEntry>
    <!-- VAT -->
    <AccountId>2640</AccountId>
    <Amount>11.4</Amount>
  </LedgerEntry>
  <LedgerEntry>
    <!-- Bank account -->
    <AccountId>1940</AccountId>
    <Amount>-68.4</Amount>
    </LedgerEntry>
  </JournalEntry>
```

LedgerEntries might have different date stamps, something that might have to be used when they’re representing multiple
invoices from different dates that have been bundled in the same journal entry. Ledger entries without a date inherits
the date from the journal entry.

```xml
<LedgerEntry>
  <AccountId>60150</AccountId>
  <Amount>57.0</Amount>
  <Date>2016-04-01+02:00</Date>
</LedgerEntry>
```

It is recommended that journal entries and ledger entries in the file are listed in chronological order if no
date stamp is listed in neither journal entries nor ledger entries.


# Invoice

XMLSIE contains two different invoice (_sv: faktura_) objects, one in `AccountsPayable` and one in `AccountsReceivable`.
The latter is out of scope for this project.

Invoices are associated with ledger entries using the financial year start date, journal identity and journal entry
identity using the `JournalInfo` object.

```xml
<AccountsPayable>
  <Invoices>
    <Invoice>
      <SupplierId>0</SupplierId>
      <InternalId>835595</InternalId>
      <JournalInfo>
        <FinancialYear>2016-04-01+02:00</FinancialYear>
        <JournalId>27</JournalId>
        <JournalEntryId>322</JournalEntryId>
      </JournalInfo>
    </Invoice>
  </Invoices>
```

Thus above `JournalInfo` corresponds to:

```xml
<FinancialYears>
  <FinancialYear start="2016-04-01+02:00" end="2016-05-01+02:00">
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
```

Optionally you might want to read more about `ArrivalDate`, `RegistredDate`, `GrossAmount` and `VatAmount` in the
official XMLSIE 1.0 documentation.


# Supplier

The supplier (_sv: leverantör/betalningsmottagare_) is the origin of one or many invoices. 

There are no requirements to give any specifics about a supplier. 

A supplier does not have to keep the same `SupplierId` in different XMLSIE-files from the same publisher. This value is
for internal references within a single file only. Joining data between files and sources should be done using the
`SupplierOrganizationalNumber`.

TODO: Borde kanske organisationsnummer vara internationell VAT-standard, ex SE-5566778899-01?
Vad händer annars med suppliers som kommer från utlandet?

```xml
<AccountsPayable>
  <Suppliers>
    <Supplier>
      <SupplierId>0</SupplierId>
      <SupplierName>ÖREBROBOSTÄDER AB</SupplierName>
      <SupplierOrganizationalNumber>556334-8449</SupplierOrganizationalNumber>
    </Supplier>
  </Suppliers>
```


