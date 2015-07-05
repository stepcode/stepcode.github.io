---
layout: docs
permalink: /docs/included_schemas/
title: Included EXPRESS schemas
---

For an up-to-date list, see [STEPcode/data](http://github.com/stepcode/stepcode/tree/master/data)

### Contents
* TOC
{:toc}

More schemas are available in [STEPMod](http://sourceforge.net/projects/stepmod), and some are available at [STEPTools SC4 Archive](http://www.steptools.com/sc4/archive/APs)

## AP schemas
APs, or Application Protocols, are the "top parts" of the STEP standard. Each covers a particular application or industry domain.
See also: [APs on Wikipedia](https://en.wikipedia.org/wiki/ISO_10303#Coverage_of_STEP_Application_Protocols_.28AP.29)

Official descriptions are in *italics*.

### ap203
- *Configuration controlled 3D designs of mechanical parts and assemblies*
- One of the first schemas. Widely used, but also relatively primitive.
- New work should prefer AP242, as it offers a superset of ap203 modeling capabilities

### ap203e2
- Second edition of ap203
- New work should prefer AP242, as it offers a superset of ap203 modeling capabilities

### ap209
- *Composite and metallic structural analysis and related design*

### ap210e2
- *Electronic assembly, interconnect and packaging design*
- Second edition of ap210

### ap210e3
- Third edition of ap210

### ap214e3
- *Core data for automotive mechanical design processes*
- Third edition of ap214
- New work should prefer AP242, as it offers a superset of ap203 modeling capabilities

### ap219
- *Dimensional inspection information exchange*

### ap227
- *Plant spatial configuration*

### ap235
- *Materials information for the design and verification of products*

### [ap238](https://en.wikipedia.org/wiki/STEP-NC)
- *Application interpreted model for computer numeric controllers*

### ap239
- *Product life cycle support*

### ap240
- *Process plans for machined products*

### [ap242](http://www.ap242.org/)
- *Managed model based 3d engineering*
- combines and replaces the following previous APs in an upward compatible way:
  - AP 201, Explicit draughting. Simple 2D drawing geometry related to a product. No association, no assembly hierarchy.
  - AP 202, Associative draughting. 2D/3D drawing with association, but no product structure.
  - AP 203, Configuration controlled 3D designs of mechanical parts and assemblies.
  - AP 204, Mechanical design using boundary representation
  - AP 214, Core data for automotive mechanical design processes

## External Standards
These utilize parts of ISO10303 but are developed separately.

### [ISO15926](https://en.wikipedia.org/wiki/ISO_15926)
- Process plant lifecycle data
- Developed for oil & gas industry

### ifc2x3
- Industry Foundation Classes - used in Building Information Modeling (BIM)

### ifc4
- Newer version of Industry Foundation Classes

## Other

### pdm
- Product data management schema, embedded into many APs

### STEPTools_merged_schema
- Created by STEPTools
- Modified due to a STEPcode parser error
- Not recommended for use, due to entity differences between the schemas that were merged.
  - **data corruption is likely**
