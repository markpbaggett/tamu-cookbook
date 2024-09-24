======================================================
Questions and Things We Need For Final Decision Making
======================================================

----------------------------
Directionality of Properties
----------------------------

At my previous institution, we had an external triple store that also kept nodes and triples about our resources in
Fedora.  This allowed us to do face SPARQL queries for interoperable applications and allowed us to use fewer properties.
For instance, properties were always placed on the *child* resource to point at a parent and not vice versa. Currently,
the pattern here seems to be to use both properties.  In many of my examples, there is little consistency about this as
I still need to understand more about the Fedora APIs to make a recommendation.  If I remember correctly, many of the
ideas in the Fedora 3.8 API were dropped in Fedora 4 (e.g. getRelationships). Because of this, we need to think more about
directionality and the API before we determine the relationship between properties and instance of classes.

-----------------------
Existing Fedora Content
-----------------------

We have a lot of content already modelled in Fedora.  My instinct is to keep that stuff modelled as is and instead build
logic to look for new models whether than readjusting.  Can we do that?

-------------------------------------
Omitting Valid Properties and Classes
-------------------------------------

PCDM is designed not to express a specific method that must be followed to create a certain concept. Instead, PCDM
allows for flexibility and room for institutions to approach problems differently for their own use cases.

In this document, certain valid properties and classes have been intentionally omitted to keep things as simple as
possible. While doing this is valid, it may cause problems for other institutions that try to adopt any software we
write or try to write with the community. As a result, we need to decide whether we should add more complex components
or simply try to account for other approaches in third party tooling we write.

---------------------------------------------------------------------------------
Should Canvases be an Instance of pcdmuse:IntermediateFile or pcdmuse:ServiceFile
---------------------------------------------------------------------------------

Depending on what we ultimately decide to store and serve, we need to choose one of the two options and reflect the
decision across all attached documentation.
