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

### Case\_Statement

`
struct Case_Statement_ {
    Expression selector;
    Linked_List cases;
};
`

### Compound\_Statement

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

### Procedure\_Call

`
struct Procedure_Call_ {
    struct Scope_ * procedure;
    Linked_List parameters; /**< list of expressions */
};
`

### Return\_Statement

`
struct Return_Statement_ {
    Expression value;
};
`

Scope\_ \*
----------

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

`
/** this is an element in the optional Loop scope */
struct Increment_ {
    Expression init;
    Expression end;
    Expression increment;
};
`

[Category:Code discussion](Category:Code discussion "wikilink")
