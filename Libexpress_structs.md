---
title: Libexpress structs
---

`
typedef struct Statement_ * Alias;
typedef struct Statement_ * Assignment;
typedef struct Statement_ * Case_Statement;
typedef struct Statement_ * Compound_Statement;
typedef struct Statement_ * Conditional;
typedef struct Statement_ * Loop;
typedef struct Statement_ * Procedure_Call;
typedef struct Statement_ * Return_Statement;
typedef struct Statement_*  Statement;

typedef struct Scope_*      Increment;
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

### Increment

[Category:Code discussion](Category:Code discussion "wikilink")
