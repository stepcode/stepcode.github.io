---
title: Libexpress structs
---

*typedef*s
----------

`
typedef struct Statement_ * Alias;
typedef struct Statement_ * Assignment;
typedef struct Statement_ * Case_Statement;
typedef struct Statement_ * Compound_Statement;
typedef struct Statement_ * Conditional;
typedef struct Statement_ * Loop;
typedef struct Statement_ * Procedure_Call;
typedef struct Statement_ * Return_Statement;
typedef struct Statement_ * Statement;

typedef struct Scope_ *     Increment;
typedef struct Scope_ *     Type;
typedef struct Scope_ *     Scope;
typedef struct Scope_ *     Schema;
typedef struct Scope_ *     Express;
typedef struct Scope_ *     Entity;
typedef struct Scope_ *     Procedure;
typedef struct Scope_ *     Function;
typedef struct Scope_ *     Rule;

typedef struct Case_Item_ * Case_Item;
typedef struct Expression_ * Expression;
typedef struct Hash_Table_ * Dictionary;
typedef struct Linked_List_ * Linked_List;
typedef struct Query_    *   Query;
typedef struct TypeBody_ * TypeBody;
typedef struct TypeHead_ * TypeHead;
typedef struct Variable_ * Variable;
typedef struct Where_ * Where;
`

[Statement\_ \*](http://stepcode.org/doxygen/struct_statement__.html)
---------------------------------------------------------------------

`
/* these should probably all be expression types */

struct Statement_ {
    Symbol symbol;  /**< can hold pcall or alias name but otherwise is not used for anything */
    int type;   /**< one of STMT_XXX above */
    /* hey, is there nothing in common beside symbol and private data?? */
    union u_statement {
        struct Alias_     *     alias;
        struct Assignment_   *  assign;
        struct Case_Statement_   *  Case;
        struct Compound_Statement_ * compound;
        struct Conditional_  *  cond;
        struct Loop_      *     loop;
        struct Procedure_Call_   *  proc;
        struct Return_Statement_  * ret;
        /* skip & escape have no data */
    } u;
};
`

### Alias

` struct Alias_ {
    struct Scope_ * scope;
    struct Variable_ * variable;
    Linked_List statements;     /**< list of statements */
};
`

### Assignment

` struct Assignment_ {
    Expression lhs;
    Expression rhs;
};
`

### Case_Statement

`
struct Case_Statement_ {
    Expression selector;
    Linked_List cases;
};
`

### Compound_Statement

`
struct Compound_Statement_ {
    Linked_List statements;
};
`

### Conditional

`
struct Conditional_ {
    Expression test;
    Linked_List code;       /**< list of statements */
    Linked_List otherwise;      /**< list of statements */
};
`

### Loop

`
struct Loop_ {
    struct Scope_ * scope;      /**< scope for increment control */
    Expression while_expr;
    Expression until_expr;
    Linked_List statements;     /**< list of statements */
};
`

### Procedure_Call

`
struct Procedure_Call_ {
    struct Scope_ * procedure;
    Linked_List parameters; /**< list of expressions */
};
`

### Return_Statement

`
struct Return_Statement_ {
    Expression value;
};
`

[Scope\_ \*](http://stepcode.org/doxygen/struct_scope__.html)
-------------------------------------------------------------

`
struct Scope_ {
    Symbol          symbol;
    char            type;       /* see above */
    ClientData      clientData; /**< user may use this for any purpose */
    int             search_id;  /**< key to avoid searching this scope twice */
    Dictionary      symbol_table,enum_table;
    struct Scope_ * superscope;
    union {
        struct Procedure_ * proc;
        struct Function_ * func;
        struct Rule_ * rule;
        struct Entity_ * entity;
        struct Schema_ * schema;
        struct Express_ * express;
        struct Increment_ * incr;
        struct TypeHead_ * type;
        /* no, query owns a scope rather than scope owning a query
         *      struct Query *query;  */
    } u;
    Linked_List where;      /**< optional where clause */
};
`

### Increment

`/** this is an element in the optional Loop scope */
struct Increment_ {
    Expression init;
    Expression end;
    Expression increment;
};`

### Type

`//NOTE - this is TypeHead_, not Type_!
struct TypeHead_ {
    Type head;          /**< if we are a defined type this is who we point to */
    struct TypeBody_ * body;    /**< true type, ignoring defined types */
};` `struct TypeBody_ {
#if 1
    struct TypeHead_ * head;    /**< for debugging only */
#endif
    enum type_enum type;        /**< bits describing this type, int, real, etc */
    struct {
        unsigned unique     : 1;
        unsigned optional   : 1;
        unsigned fixed      : 1;
        unsigned shared     : 1; /**< type is shared */
        unsigned repeat     : 1; /**< expression is a repeat count*/
        unsigned encoded    : 1; /**< encoded string */
    } flags;
    Type base;      /**< underlying base type if any can also contain true type if this type is a type reference */
    Type tag;       /**< optional tag */
    /* a lot of the stuff below can be unionized */
    Expression precision;
    Linked_List list;   /**< used by select_types and composed types, such as for a list of entities in an instance */
    Expression upper;
    Expression lower;
    struct Scope_ * entity;     /**< only used by entity types */
};`

### Schema

`struct Schema_ {
    Linked_List rules;
    Linked_List reflist;
    Linked_List uselist;
    /** \var refdict, usedict
     * dictionarys into which are entered renames for each specific 
     * object specified in a rename clause (even if it uses the same
     * name */
    Dictionary refdict;
    Dictionary usedict;

    Linked_List use_schemas; /**< lists of schemas that are fully use'd
                              * entries can be 0 if schemas weren't found during RENAMEresolve */
     Linked_List ref_schemas; /**< lists of schemas that are fully ref'd
                               * entries can be 0 if schemas weren't found during RENAMEresolve */
};`

### Express

`struct Express_ {
    FILE * file;
    char * filename;
    char * basename; /**< name of file but without directory or .exp suffix */
};`

### Entity

`struct Entity_ {
    Linked_List supertype_symbols;  /**< linked list of original symbols as generated by parser */
    Linked_List supertypes;         /**< linked list of supertypes (as entities) */
    Linked_List subtypes;           /**< simple list of subtypes useful for simple lookups */
    Expression  subtype_expression; /**< DAG of subtypes, with complete information including, OR, AND, and ONEOF */
    Linked_List attributes;         /**< explicit attributes */
    int         inheritance;        /**< total number of attributes inherited from supertypes */
    int         attribute_count;
    Linked_List unique;             /**< list of identifiers that are unique */
    Linked_List instances;          /**< hook for applications */
    int         mark;               /**< usual hack - prevent traversing sub/super graph twice */
    bool        abstract;           /**< is this an abstract supertype? */
    Type        type;               /**< type pointing back to ourself, useful to have when evaluating expressions involving entities */
};`

### Procedure

`/** location of fulltext of algorithm in source file */
struct FullText {
    char * filename;
    unsigned int start, end;
};` `/** 'parameters' are lists of lists of (type) expressions */
struct Procedure_ {
    int pcount; /**< # of parameters */
    int tag_count;  /**< # of different parameter tags */
    Linked_List parameters;
    Linked_List body;
    struct FullText text;
    int builtin;    /**< builtin if true */
};`

### Function

`struct Function_ {
    int pcount; /**< # of parameters */
    int tag_count;  /**< # of different parameter/return value tags */
    Linked_List parameters;
    Linked_List body;
    Type return_type;
    struct FullText text;
    int builtin;    /**< builtin if true */
};`

### Rule

`struct Rule_ {
    Linked_List parameters;
    Linked_List body;
    struct FullText text;
};`

Others
------

### Case_Item

``

### Dictionary

``

### Expression

`struct Qualified_Attr {
    struct Expression_ * complex;   /**< complex entity instance */
    Symbol * entity;
    Symbol * attribute;
};

struct Op_Subexpression {
    Op_Code op_code;
    Expression op1;
    Expression op2;
    Expression op3;
};

struct Query_ {
    Variable local;
    Expression aggregate;   /**< set from which to test */
    Expression expression;  /**< logical expression */
    struct Scope_ * scope;
};

struct Funcall {
    struct Scope_ * function; /**< can also be an entity because entities can be called as functions */
    Linked_List list;
};

union expr_union {
    int integer;
    float real;
    char * attribute;   /**< inverse .... for 'attr' */
    char * binary;
    int logical;
    bool boolean;
    struct Query_ * query;
    struct Funcall funcall;

    /* if etype == aggregate, list of expressions */
    /* if etype == funcall, 1st element of list is funcall or entity */
    /*  remaining elements are parameters */
    Linked_List list;   /**< aggregates (bags, lists, sets, arrays) or lists for oneof expressions */
    Expression expression;  /**< derived value in derive attrs, or
                             * initializer in local vars, or
                             * enumeration tags
                             * or oneof value */
    struct Scope_ * entity; /**< used by subtype exp, group expr
                              * and self expr, some funcall's and any
                              * expr that results in an entity */
    Variable variable;  /**< attribute reference */
};

/** The difference between 'type' and 'return_type' is illustrated
 * by "func(a)".  Here, 'type' is Type_Function while 'return_type'
 * might be Type_Integer (assuming func returns an integer). */
struct Expression_ {
    Symbol symbol;      /**< contains things like funcall names, string names, binary values, enumeration names */
    Type type;
    Type return_type;   /**< type of value returned by expression */
    struct Op_Subexpression e;
    union expr_union u;
};
`

### Linked_List

``

### Query

``

### Statement

``

### Variable

`struct Variable_ {
    Expression  name;    /**< Symbol is inside of 'name' below */
    Type        type;
    Expression  initializer; /**< or 'derived' */
    int         offset;

    struct {
        int optional    : 1; /**< OPTIONAL keyword */
        int var         : 1; /**< VAR keyword */
        int constant    : 1; /**< from CONSTANT...END_CONSTANT */
        int unique      : 1; /**< appears in UNIQUE list */
        int parameter   : 1; /**< is a formal parameter */
        int attribute   : 1; /**< is an attribute (rule parameters are marked this way, too) */
    } flags;

#define query_symbol inverse_symbol
    Symbol   *  inverse_symbol;     /**< entity symbol */
    Variable    inverse_attribute;  /**< attribute related by inverse relationship */
};
`

### Where

``

[Category:Code discussion](Category:Code_discussion.html)
