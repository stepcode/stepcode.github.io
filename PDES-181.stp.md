---
title: PDES-181.stp
---

Description
-----------

This file is available [on
wikistep](http://www.wikistep.org/index.php/PDES-181). It is a test file
for [AP210e2](AP210e2 "wikilink").

**time stamp** 2009-10-16T16:42:18

Errors reported by AP210e2 [p21read](p21read "wikilink")
--------------------------------------------------------

### Illegal complex entity

It turns out that all of the complex entity errors are identical.

    ERROR: Could not create instance of the following complex entity:
    area_with_outer_boundary
    complex_area
    compound_representation_item
    geometric_representation_item
    half_space_2d
    primitive_2d
    primitive_2d_with_inner_boundary
    representation_item

    ERROR: instance #4214 Illegal complex entity.


    ERROR: instance #4856 Illegal complex entity.


    ERROR: instance #5239 Illegal complex entity.


    ERROR: instance #5440 Illegal complex entity.


    ERROR: instance #5462 Illegal complex entity.


    ERROR: instance #6578 Illegal complex entity.


    ERROR: instance #7099 Illegal complex entity.


    ERROR: instance #7234 Illegal complex entity.


    ERROR: instance #7267 Illegal complex entity.


    ERROR: instance #7621 Illegal complex entity.
    Entity combination does not represent a legal complex entity.

### Incomplete instance

There were hundreds of errors reported; I only copied the first few.

*'\#1=FUNCTIONAL\_UNIT('5',\$,\#3,\#4,*,\$,\*);'''

    ERROR:  ENTITY #1 Functional_Unit
      id :    WARNING: attribute id of type identifierMissing asterisk for derived attribute.
        Found invalid '5' value...
        data lost looking for end of attribute: '5'
      name :    WARNING: attribute name of type labelMissing asterisk for derived attribute.
        Found invalid ' value...
        data lost looking for end of attribute: ''
    ERROR in EXCHANGE FILE: incomplete instance #1.

    ERROR:  ENTITY #6 Layered_Assembly_Module_Usage_View
      id :    WARNING: attribute id of type identifierMissing asterisk for derived attribute.
        Found invalid '2' value...
        data lost looking for end of attribute: '2'
      name :    WARNING: attribute name of type labelMissing asterisk for derived attribute.
        Found invalid 'ass value...
        data lost looking for end of attribute: 'assembly module'
    ERROR in EXCHANGE FILE: incomplete instance #6.

    ERROR:  ENTITY #27 Layered_Interconnect_Module_Usage_View
      id :    WARNING: attribute id of type identifierMissing asterisk for derived attribute.
        Found invalid '2' value...
        data lost looking for end of attribute: '2'
      name :    WARNING: attribute name of type labelMissing asterisk for derived attribute.
        Found invalid 'int value...
        data lost looking for end of attribute: 'interconnect module'
    ERROR in EXCHANGE FILE: incomplete instance #27.

    ERROR:  ENTITY #72 Interconnect_Module_Component
      id :    WARNING: attribute id of type identifierMissing asterisk for derived attribute.
        Found invalid 'boa value...
        data lost looking for end of attribute: 'board'
      name :    WARNING: attribute name of type labelMissing asterisk for derived attribute.
        Found invalid 'def value...
        data lost looking for end of attribute: 'definition usage'
    ERROR in EXCHANGE FILE: incomplete instance #72.

    ERROR:  ENTITY #76 Component_2d_Location
      name :    WARNING: attribute name of type labelMissing asterisk for derived attribute.
        Found invalid 'com value...
        data lost looking for end of attribute: 'component 2d location'
      description :    WARNING: attribute description of type textMissing asterisk for derived attribute.
        Found invalid $ value...
        data lost looking for end of attribute: $
    ERROR in EXCHANGE FILE: incomplete instance #76.

    ERROR:  ENTITY #79 Library_Stack_Model
      id :    WARNING: attribute id of type identifierMissing asterisk for derived attribute.
        Found invalid ' value...
        data lost looking for end of attribute: ''
      name :    WARNING: attribute name of type labelMissing asterisk for derived attribute.
        Found invalid ' value...
        data lost looking for end of attribute: ''
    ERROR in EXCHANGE FILE: incomplete instance #79.
    Entity #88 skipping redefined attribute material_designation.definitions


    ERROR:  ENTITY #187 Design_Stack_Model
      id :    WARNING: attribute id of type identifierMissing asterisk for derived attribute.
        Found invalid ' value...
        data lost looking for end of attribute: ''
      name :    WARNING: attribute name of type labelMissing asterisk for derived attribute.
        Found invalid ' value...
        data lost looking for end of attribute: ''
    ERROR in EXCHANGE FILE: incomplete instance #187.

    ERROR:  ENTITY #223 Layered_Interconnect_Module_Design_View
      id :    WARNING: attribute id of type identifierMissing asterisk for derived attribute.
        Found invalid '1' value...
        data lost looking for end of attribute: '1'
      name :    WARNING: attribute name of type labelMissing asterisk for derived attribute.
        Found invalid 'int value...
        data lost looking for end of attribute: 'interconnect module'
    ERROR in EXCHANGE FILE: incomplete instance #223.

### Missing and required

This is only a few of the errors.

*'\#12970=PRODUCT\_SPECIFIC\_PARAMETER\_VALUE\_ASSIGNMENT(\$,\$,*,\$,(\#501));'''

    ERROR:  ENTITY #12970 Product_Specific_Parameter_Value_Assignment
      name :   missing and required. For compatibility, replacing with ''.

EXPRESS:

`   `**`ENTITY` `product_specific_parameter_value_assignment`**  
`       SUBTYPE OF (characterized_object, product_related_product_category);`  
`   END_ENTITY;`

`   `**`ENTITY` `product_related_product_category`**  
`       SUBTYPE OF (product_category);`  
`       products : SET [1:?] OF product;`  
`   END_ENTITY;`

`   `**`ENTITY` `product_category;`**  
`       name : label;`  
`       description : OPTIONAL text;`  
`   DERIVE`  
`       id : identifier := get_id_value(SELF);`  
`   WHERE`  
`       WR1 : SIZEOF(USEDIN(SELF, 'AP210_ELECTRONIC_ASSEMBLY_INTERCONNECT_AND_PACKAGING_DESIGN_MIM_LF.' + 'ID_ATTRIBUTE.IDENTIFIED_ITEM')) <= 1;`  
`   END_ENTITY;`

    ERROR:  ENTITY #12976 Parameter_Assignment
      name :    WARNING: attribute name of type labelMissing asterisk for derived attribute.
        Found invalid $ value...
        data lost looking for end of attribute: $
      items :   missing and required
      context_of_items :   missing and required
    ERROR in EXCHANGE FILE: incomplete instance #12976.

    ERROR:  ENTITY #12977 Product_Specific_Parameter_Value_Assignment
      name :   missing and required. For compatibility, replacing with ''.

    ERROR:  ENTITY #14865 Property_Definition_Relationship
      description :   missing and required. For compatibility, replacing with ''.

    ERROR:  ENTITY #14868 Property_Definition_Relationship
      description :   missing and required. For compatibility, replacing with ''.

    ERROR:  ENTITY #14871 Property_Definition_Relationship
      description :   missing and required. For compatibility, replacing with ''.

    ERROR:  ENTITY #14874 Property_Definition_Relationship
      description :   missing and required. For compatibility, replacing with ''.

    ERROR:  ENTITY #14877 Property_Definition_Relationship
      description :   missing and required. For compatibility, replacing with ''.

    ERROR:  ENTITY #14880 Property_Definition_Relationship
      description :   missing and required. For compatibility, replacing with ''.

    ERROR:  ENTITY #17761 Item_Identified_Representation_Usage
      used_representation :   missing and required
    ERROR in EXCHANGE FILE: incomplete instance #17761.

    ERROR:  ENTITY #18053 Property_Definition_Relationship
      description :   missing and required. For compatibility, replacing with ''.
