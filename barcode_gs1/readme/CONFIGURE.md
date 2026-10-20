No configuration is needed: once installed, GS1 barcodes are parsed wherever
the app reads a scan. Two things can be adjusted.

## Application identifiers

The application identifiers are read from a GS1 ``barcode.nomenclature``: the
one set on the company when it is a GS1 nomenclature, otherwise the first GS1
nomenclature found (the *Default GS1 Nomenclature* Odoo ships). Its GS1-128
rules are fetched once, when the barcode app opens.

To teach the scanner a new application identifier, add a rule under
*Inventory → Configuration → Barcode Nomenclatures* — no code change. A rule
whose *Type* is one the app maps to a field — *Unit Product*, *Lot number*,
*Quantity*, *Package*, *Package Type*, *Best before Date*, *Expiration Date*,
*Pack Date*, *Location* or *Destination location*, the selectable types in
Odoo 17 — lands on the matching field of the parsed scan (see Usage); the value
of any other rule is still available in ``ais``.

Weight, price and production date are not selectable rule types in Odoo 17:
they are read by the identifiers built into the module (AI 310n–360n,
390n–393n and 11). A measure rule configured as *Quantity* with *Decimal*
enabled fills ``weight``; any other rule's value remains available in ``ais``.

Identifiers the nomenclature does not define keep working through the ones built
into the module, and if the nomenclature cannot be read at all the module falls
back to them entirely.

## Scanners that cannot send FNC1

GS1 ends a variable-length value with FNC1 unless it is the last element of the
barcode, and a keyboard-wedge scanner often sends nothing in its place. Odoo has
a field for exactly that — *FNC1 Separator* on the nomenclature — so configure
the scanner to send one of those characters (``#`` out of the box) and the scan
is read as printed.
