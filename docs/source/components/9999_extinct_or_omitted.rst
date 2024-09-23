===========================================
Extinct Components or Intentionally Omitted
===========================================

This section acknowledges and gives reasoning for classes or properties that were intentionally left out.

This can be revisited or changed if necessary.

------------------
pcdmworks:TopRange
------------------

The `PCDM Works Extension <http://pcdm.org/works#TopRange>`_ defines a class :code:`pcdmworks:TopRange` that is meant to
be the parent Range in a book.  This was due to requirements for the IIIF Presentation API prior to version 3 where the
top most range in a sequence needed a :code:`viewingHint="top"` property.  Since version three, this is no longer required
and complex hierarchy can be modelled simply with the :code:`pcdmworks:Range` class and properties and classes from :code:`iana`
and :code:`ore`.

-----------
pcdm:Object
-----------

The :code:`pcdm:Object` class is extended by other subclasses that add much more flexibility. For now, :code:`pcdm:Object`
has been dropped in lieu of its subclasses.
