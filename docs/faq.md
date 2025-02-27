Frequently Asked Questions

## General

??? faq "What does `Convert-Pheno` do?"

    This tool facilitates the conversion of clinical data between commonly used formats, such as [GA4GH standards](https://www.ga4gh.org), to enable **secure data sharing** and discovery through **semantic interoperability**.

    ##### last change 2023-01-05 by Manuel Rueda [:fontawesome-brands-github:](https://github.com/mrueda)

??? faq "Is `Convert-Pheno` free?"

    Yes - Free as in Speech. 

    ##### last change 2023-01-04 by Manuel Rueda [:fontawesome-brands-github:](https://github.com/mrueda)

??? faq "Can I use `Convert-Pheno` in _production_ software?"

    Nope. We're working on it as we speak.

    ##### last change 2023-01-04 by Manuel Rueda [:fontawesome-brands-github:](https://github.com/mrueda)

??? faq "There are multiple [download](download-and-installation.md) options, which one should I choose?"

    We recommend using the [containerized version](https://github.com/mrueda/convert-pheno#containerized).
 
    ##### last change 2023-01-04 by Manuel Rueda [:fontawesome-brands-github:](https://github.com/mrueda)

??? faq "If I use `Convert-Pheno` to convert my data to [Beacon v2 Models](bff.md), does this mean I have a Beacon v2?"

    I am afraid not. Beacon v2 is an [API specification](https://docs.genomebeacons.org), and the [Beacon v2 Models](bff.md) are merely a component of it. In order to _light a Beacon v2_, it is necessary to load the `JSON` files into a **database** and add an an **API** on top. Currently, it is advisable to utilize the [Beacon v2 Reference Implementation](https://b2ri-documentation.readthedocs.io/en/latest) which includes the database, the Beacon v2 API, and other necessary components.

    See below an example in how to integrate an OMOP-CDM export from SQL with Beacon v2.

    <figure markdown>
      ![B2RI](img/convert-pheno-beacon-integration.png){ width="600" }
      <figcaption>Beacon v2 RI integration</figcaption>
    </figure>

    ##### last change 2023-01-04 by Manuel Rueda [:fontawesome-brands-github:](https://github.com/mrueda)

??? faq "What is the difference between Beacon v2 Models and Beacon v2?"

    **Beacon v2** is a specification to build an [API](https://docs.genomebeacons.org). The [Beacon v2 Models](https://docs.genomebeacons.org/models/) define the format for the API's responses to queries regarding biological data. With the help of `Convert-Pheno`, text files ([BFF](bff.md)) that align with this response format can be generated. By doing so, the BFF files can be integrated into a non-SQL database, such as MongoDB, without the API having to perform any additional data transformations internally.

    ##### last change 2023-02-13 by Manuel Rueda [:fontawesome-brands-github:](https://github.com/mrueda)

??? faq "Are you planning in supporting other clinical data formats?"

    Afirmative. Please check our [roadmap](future-plans.md) for more information.

    ##### last change 2023-01-04 by Manuel Rueda [:fontawesome-brands-github:](https://github.com/mrueda)

??? faq "Which ontologies are supported?"

    We support [NCI Thesaurus](https://ncithesaurus.nci.nih.gov/ncitbrowser), [ICD-10](https://icd.who.int/browse10), [CDISC](https://www.cdisc.org/standards/terminology/controlled-terminology) (Study Data Tabulation Model Terminology) and data from [Athena-OHDSI](https://athena.ohdsi.org/search-terms/start) which includes multiple ontologies, such as _SNOMED, RxNorm or LOINC_.

    ##### last change 2023-01-27 by Manuel Rueda [:fontawesome-brands-github:](https://github.com/mrueda)

## Installation

??? faq "I am installing `Convert-Pheno` from source ([non-containerized version](https://github.com/mrueda/convert-pheno#non-containerized)) but I can't make it work. Any suggestions?"

    #### Problems with Python / PyPerler

    !!! Failure "About PyPerler installation"
        Apart from [PypPerler](https://github.com/tkluck/pyperler#quick-install) itself, you may need to install `libperl-dev` to make it work.

        `sudo apt-get install libperl-dev`


    ##### last change 2023-01-04 by Manuel Rueda [:fontawesome-brands-github:](https://github.com/mrueda)
