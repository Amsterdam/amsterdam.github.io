---
abstract: Descriptive statistics about the population and real estate of Amsterdam
reusability: 1
---

# Basisstatistiek

All documentation, scripts and syntaxes, and datamodels (refered to as `code`) used for generating
descriptive statistics about the population and real estate of Amsterdam.

User friendly documentation can be found on our [documentation](https://basisstatistiek.amsterdam.nl) website.

The project is built modular and split in various components which are split across various (github) repositories:
- [Documenation and definitions](https://github.com/amsterdam/basisstatistiek-documentatie)
- [Database structure, documentation and datatransformations](https://github.com/amsterdam/basisstatistiek-database)
- [Birth statistics](https://github.com/amsterdam/basisstatistiek-persoon-geboorte)
- [Mortality statistics](https://github.com/amsterdam/basisstatistiek-persoon-sterfte)
- [Migration and movement statistics](https://github.com/amsterdam/basisstatistiek-persoon-vestiging-vertrek-verhuizing)
- [Data-sources import/export](https://github.com/amsterdam/basisstatistiek-bronnen)

## Reusability

**This project in only available in Dutch**

Our generalized database model is the core of our statistical products.
We transform various governmental data streams to this model making it robust for changes and
making it easy to do selections for statistical purposes.

In order to reuse our code the database must be filled with own data according to
our datatransformation guideliness. This often means writing new datatransformation,
reusing or adopting ours. Once the database has been filled, our queries can be used to generate
statistics, similar to ours.

We try to follow Dutch governmental standards wherever possible and sufficient.
Sometimes we are forced to use custom extractions making some of our code specific for
the City of Amsterdam.

## Openess

At the moment we only publicly publish code that we consider production ready.
Our development is kept internal, until we have marked a new release.

## New releases

New code is released whenever new statistics are published. For example in our 'Jaarboek' or 'Kerncijfers' books, or periodically such as each new year.
These code releases are however limited to the codebase we have developed around our statistical database. Statistics we publish based on our old codebase
will not be publically available, until we have replaced it with a new codebase based built around our statistical database.

New releases will be made available in single commits changes. All commit history with the accompanied discussions are kept private.
