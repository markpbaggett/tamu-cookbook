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

