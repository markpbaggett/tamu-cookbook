==========
Namespaces
==========

The various components and work types described throughout this document leverage properties and classes defined in a
limited number of core ontologies.  This document lists those ontologies and how they are used.

.. list-table::
  :width: 100 %
  :widths: 20 10 20 50
  :header-rows: 1

  * - Ontology Name
    - Prefix
    - Namespace URI
    - Description
  * - Fedora Commons Repository Ontology
    - fcrepo
    - http://fedora.info/definitions/v4/repository#
    - Ontology for the Fedora data model intended primarily to make it possible to expose Fedora-curated RDF predicates via de-reference-able URIs.
  * - OAI ORE Terms
    - ore
    - http://www.openarchives.org/ore/terms/
    - The set of terms provided by the OAI ORE initiative
  * - PCDM Models
    - pcdm
    - https://pcdm.org/models#
    - Base ontology for the Portland Common Data Model intended to underlie a wide array of repository and DAMS applications.
  * - PCDM File Formats Genre
    - pcdmff
    - https://pcdm.org/2015/10/14/file-format-types#
    - Provides terms for describing file formats selected from vocabularies such as DCMIType, UDFRS, Nepomuk, Pronom, and MARC Resource Types.
  * - PCDM Use
    - pcdmuse
    - https://pcdm.org/2021/04/09/use#
    - Ontology for a PCDM extension to add subclasses of PCDM File for the different roles files have in relation to the Object they are attached to.
  * - PCDM Works
    - pcdmworks
    - https://pcdm.org/2021/04/09/works#
    - Ontology for a PCDM extension that adds subclasses of pcdm:Object to refine the relationships between a work and its constituent parts. Also establishes links to the IIIF Presentation API.