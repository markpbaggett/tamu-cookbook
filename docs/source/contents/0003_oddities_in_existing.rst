==============================
Oddities in Our Current Models
==============================

-----
About
-----

In our current Fedora repository, there are several odd models that don't align with the
`Philosophy Section <https://tamu-cookbook.readthedocs.io/en/latest/contents/0002_philosophy.html>`_. In order to
think about and decide whether our philosophy in applicable to defined models and explore whether we should
retroactively address, this document attempts to point out areas where our philosophy falls down.

**NOTE**: Some of the descriptions here go beyond structural metadata and include other forms of metadata stored in
Fedora.

------------------------------------
Collections are not pcdm:Collections
------------------------------------

PCDM Models, the base ontology for all PCDM ontologies, defines four main classes:

* :code:`pcdm:AlternateOrder`
* :code:`pcdm:Collection`
* :code:`pcdm:File`
* :code:`pcdm:Object`

Interestingly, our Fedora collections are instances of :code:`pcdm:Object` rather than :code:`pcdm:Collection`. A
:code:`pcdm:Object` is defined as:

    an intellectual entity, sometimes called a "work", "digital object", etc. that has descriptive metadata, access
    metadata, may contain files and other Objects as member "components". Each level of a work is therefore represented
    by an Object instance, and is capable of standing on its own, being linked to from Collections and other Objects.
    Member Objects can be ordered using the ORE Proxy class.

A :code:`pcdm:Collection` is:

    a group of resources that has descriptive metadata, access metadata, and may link to works and/or collections. By
    default, member works and collections are an unordered set, but can be ordered using the ORE Proxy class.

While both classes are instances of :code:`ore:Aggregation`, `models <https://pcdm.org/2016/04/18/models>`_ and the
other ontologies treat these two classes differently. The :code:`models` ontology defines properties such as
:code:`pcdm:hasFile` which is only intended to be placed on :code:`pcdm:Object`. The other :code:`models` properties that
apply to either class have a domain of :code:`ore:Aggregation`, meaning you can use them on either.

If the intention was to make these instances of :code:`pcdm:Object` was to make them more flexible (let them contain files),
this decision to use :code:`pcdm:Object` seems okay although I could not find an example of a collection with files. If
not, :code:`pcdm:Collection` is more correct. If we keep these as instances of :code:`pcdm:Object` we should consider
adding a :code:`rdf:type` from another ontology that states these are more than :code:`pcdm:Object` resources and are
something more close to the idea of a collection.

-------------------------------------------------------
Use of pcdm:hasFile does not Adhere to rdfs:range Rules
-------------------------------------------------------

Currently, :code:`pcdm:hasFile` is used to link binary data streams to :code:`pcdm:Object` resources. For instance, see
`this page file <https://api.library.tamu.edu/fcrepo/rest/3b/6f/c3/25/3b6fc325-f6ca-41d8-b91e-8c5db3be8c13/london-collection_objects/11/pages/page_0/files>`_
and the parent `page resource <https://api.library.tamu.edu/fcrepo/rest/3b/6f/c3/25/3b6fc325-f6ca-41d8-b91e-8c5db3be8c13/london-collection_objects/11/pages/page_0>`_.

Since :code:`pcdm:hasFile` has a range of :code:`pcdm:File`, the object of :code:`pcdm:hasFile` should be an RDF resource
represented as node that should have a :code:`rdf:type` of :code:`pcdm:File`.

The link to the binary datastream should be on the :code:`pcdm:File` and be done using a property such as :code:`fedora:hasBinary`.
