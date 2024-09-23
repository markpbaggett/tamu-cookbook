======
Object
======

PCDM defines a class called :code:`pcdm:Object`. Objects have descriptive metadata, access metadata, may contain files
and other Objects as member "components". An instance of a :code:`pcdm:Object` is capable of standing on its own, being
linked to from Collections and other Objects, and can be ordered using the ORE Proxy class.

The `PCDM Works extension <https://pcdm.org/2021/04/09/works>`_ defines several subclasses of :code:`pcdm:Object` including:

* :code:`pcdmworks:FileSet`
* :code:`pcdmworks:Range`
* :code:`pcdmworks:Work`

These subclasses are designed to be used with the properties that PCDM defines for the Object class while giving you
flexibility and a way to more easily differentiate these various ideas.

Because of this, :code:`pcdm:Object` won't be used directly as nodes in our repository.
