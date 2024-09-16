##########
Philosophy
##########

*****
About
*****

When creating work and file types for the objects in our repository system, we adhere to several principles to ensure
semantic clarity, consistency, data validation, and interoperability.

This document describes these principles and aims to explain decisions and models found elsewhere.

**********
Principles
**********

our philosophy seeks to ensure that we are good linked data citizens by attempting to adhere to the
principles, standards, and best practices set forth of linked data described in documents such as `Tim Berners-Lee’s Four Principles of Linked Data <https://www.w3.org/DesignIssues/LinkedData.html>`_,
`Best Practice Recipes for Publishing RDF Vocabularies <https://www.w3.org/TR/swbp-vocab-pub/>`_,
`How to Publish Linked Data on the Web <wifo5-03.informatik.uni-mannheim.de/bizer/pub/LinkedDataTutorial/>`_,
`Cool URIs for the Semantic Web <https://www.w3.org/TR/cooluris/>`_, and `RDF Schema <https://www.w3.org/TR/rdf-schema/>`_.
The philosophy also attempts to have a user centered approach to description and keep things as simple as possible
from a technical standpoint. Each principle is detailed below.

**********
Principles
**********

I. Leverage Portland Common Data Model (PCDM) Ontologies with Fedora Commons Repository Ontology Where Possible
===============================================================================================================

The Portland Common Data Model (PCDM) is a flexible data model designed to represent digital objects, such as digital
libraries, archives, and museum collections. PCDM provides a framework to represent complex, multi-part digital objects
in a standardized way, ensuring that objects like documents, images, videos, and their associated metadata can be
effectively described and linked together. The model is particularly useful for institutions that need to manage complex
digital collections.

PCDM is made up of 5 ontologies:

* `PCDM Models <https://pcdm.org/models>`_
* `PCDM Use <https://pcdm.org/use>`_
* `PCDM Rights <https://pcdm.org/rights>`_
* `PCDM Works <https://pcdm.org/works>`_
* `PCDM File Formats <https://pcdm.org/2015/10/14/file-format-types>`_

Together, these ontologies allow institutions to create a more interconnected digital infrastructure for cultural
heritage institutions. By using PCDM, we allow for more seamless sharing and integration of digital content across
institutions and platforms and foster collaboration and the ability to create and adopt shared software that can be
leveraged by any PCDM adopter.

Similarly, the Fedora Commons Repository Ontology is designed to facilitate the modeling, storage, and management of
digital assets in a semantic, machine-readable way using RDF and make it possible to expose Fedora-curated RDF predicates
via de-reference-able URIs.

Like PCDM, utilizing this ontology allows us to express relationships between files and objects in our repository and
develop tooling that can be used with other repository software.

II. Adhere to "rdfs:domain" and "rdfs:range" Properties
=======================================================

When adopting predicates and models for work and file types, we adhere to rules set forth in :code:`rdfs:domain` and
:code:`rdfs:range` properties.

:code:`rdfs:domain`, or `<https:>`_, is a property in RDF Schema (RDFS) that specifies the class (or classes) of
resources to which a particular property can apply. In other words, it defines the type of the subject that can use the
specified property. When you define a property and associate it with a particular domain, you are saying that if this
property is used, the subject of the statement must be an instance of the class specified by :code:`rdfs:domain`.
If a resource is found to use this property, it is inferred that the resource belongs to the class defined by
:code:`rdfs:domain`, even if it hasn’t been explicitly typed as such.

Conversely, :code:`rdfs:range` is a property in RDF Schema (RDFS) that specifies the class or datatype of the :code:`object`
(value) that a particular property can have. In other words, it defines the type of the value or resource that can be
the object of the specified property. When you define a property and associate it with a range, you are indicating that
the objects (values) of statements using this property must be of the class or datatype specified by :code:`rdfs:range`.
If the object of a property is not explicitly typed, the system can infer the type of the object based on the
:code:`rdfs:range`.

For instance, let's think about these properties using `PCDM models <https://pcdm.org/2016/04/18/models>`_. This ontology defines a
property called `pcdm:hasFile <http://pcdm.org/models#hasFile>`_. This property links to a file contained by an object
and has an :code:`rdfs:domain` of :code:`pcdm:Object` and a :code:`rdfs:range` of :code:`pcdm:File`. We can see its full
graph here:

.. code-block:: turtle

    @prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .

    <http://pcdm.org/models#hasFile> a rdf:Property ;
        rdfs:label "has file"@en ;
        rdfs:comment "Links to a File contained by this Object."@en ;
        rdfs:domain <http://pcdm.org/models#Object> ;
        rdfs:isDefinedBy <http://pcdm.org/models#> ;
        rdfs:range <http://pcdm.org/models#File> ;
        rdfs:subPropertyOf <http://www.openarchives.org/ore/terms/aggregates> .

Let's pretend we were modelling our Collections as a `pcdm:Collection <http://pcdm.org/models#Collection>`_. If we inspect
its graph, we can see that a :code:`pcdm:Collection` is not a :code:`pcdm:Object` and thus cannot use the
:code:`pcdm:hasFile` property:

.. code-block:: turtle

    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .

    <http://pcdm.org/models#Collection> a rdfs:Class ;
        rdfs:label "Collection"@en ;
        rdfs:comment """
            A Collection is a group of resources. Collections have descriptive metadata, access metadata,
            and may links to works and/or collections. By default, member works and collections are an
            unordered set, but can be ordered using the ORE Proxy class.
          """@en ;
        rdfs:isDefinedBy <http://pcdm.org/models#> ;
        rdfs:subClassOf <http://www.openarchives.org/ore/terms/Aggregation> .

Similarly, let's pretend we had a binary file that was a :code:`TIF` and we wanted to attach if to a :code:`pcdm:Object`.
We should not do this because the :code:`rdfs:range` of :code:`pcdm:hasFile` is `pcdm:File <http://pcdm.org/models#File>`_.
This is a RDF class that has its own properties. If you wanted to attach a binary to an object, a more correct way of doing
this would be to first attach the :code:`pcdm:Object` to a :code:`pcdm:File` via :code:`pcdm:hasFile` and use :code:`fedora:hasContent`
or :code:`fedora:hasVersions`:

.. code-block:: turtle

    @prefix ebucore:  <http://www.ebu.ch/metadata/ontologies/ebucore/ebucore#> .
    @prefix exif:  <http://www.w3.org/2003/12/exif/ns#> .
    @prefix fedora:  <http://fedora.info/definitions/v4/repository#> .
    @prefix pcdm:  <http://pcdm.org/models#> .
    @prefix rdf:  <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
    @prefix rdfs:  <http://www.w3.org/2000/01/rdf-schema#> .

    <http://example/pcdm/object> a pcdm:Object ;
        rdfs:label "Demo Object" ;
        pcdm:hasFile <http://example/pcdm/file>.

    <http://example/pcdm/file> a pcdm:File ;
        rdf:type ldp:NonRDFSource ;
        rdf:type pcdm:File ;
        rdf:type fedora:Resource ;
        ebucore:filename "Example.tif" ;
        ebucore:hasMimeType "image/tiff" ;
        ebucore:width "2106" ;
        ebucore:height "2808" ;
        exif:colorSpace "RGB" ;
        fedora:hasContent <https://example/pcdm/file/Example.tif> .


III. Avoid Blank Nodes
======================

IV. Mint New Objects and Predicates Only as a Last Resort
=========================================================

V. Utilize Dereferenceable and Content Negotiable URIs
======================================================
