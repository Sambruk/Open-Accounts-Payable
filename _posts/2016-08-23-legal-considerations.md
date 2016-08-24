---
layout: page
title: "Legal considerations"
category: doc
date: 2016-08-23 17:23:39
order: 3
---

There are in some instances legal consideration required regarding personal integrity, especially when being able to
trace an invoice to a sole trader (_sv: enskild firma_).

[_Personuppgiftslagen_ (PUL)](https://sv.wikipedia.org/wiki/Personuppgiftslagen),
the Swedish implementation of [the European data protection directive (Directive 95/46/EC)](https://en.wikipedia.org/wiki/Data_Protection_Directive),
state that you need permission from the person whom you are storing or publishing any information that can be used to
identify that person. In the case of a sole trader that includes the name of the firm, the organization number,
a phone number, or pretty much any information that can be used directly or indirectly to identify the sole trader.

One potential way to get around this problem for the scope of this project is to bundle all sole traders as a single
non identified supplier. This is however rather counter productive as it would severely cripple the dataset for further
in depth analysis. Examples of this is available in the git-repository.

The legal department of Örebro kommun made the decision that publishing accounts payable is more important than the
integrity of sole traders, thus openly publishing all data without the consent of the sole traders.

A strict interpretation of PUL would be that you are not allowed to keep track of sole traders in any accountings,
rendering more or less all Swedish organizations as criminals.

There are a number of laws regarding this subject with questionable compatibility.

Consult your own legal department before publishing.
Please contact the curators of this document and let them know what you ended up doing.

