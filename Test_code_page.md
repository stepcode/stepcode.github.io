---
title: Test code page
---

Demonstrating use of mediawiki [code
extension](http://www.mediawiki.org/wiki/Extension:Code) / GeSHi.

### Usage

Copied from that page

`   <code [options]>your code</code>`

`   where options are:`  
`   lang='s'       This is the language type that explains how to highlight the code. Default is 'text'.`  
`              See GeSHi for full list of supported syntaxes`  
`   linenumbers    Turn on line numbers for each line in your code`  
`   download       Turn on the "Download Code" link for this block of your code `**`NOTE:`**` this option is broken!`  
`   tabwidth='n'   How many spaces does a TAB represent`  
`   fileurl='s'    Instead of processing the code provided between the tags, process the code at specified URL`

### C demo with line numbers

`
void ALGresolve_expressions_statements( Scope s, Linked_List statements ) {
    int status = 0;

    if( print_objects_while_running & OBJ_ALGORITHM_BITS &
            OBJget_bits( s->type ) ) {
        fprintf( stdout, "pass %d: %s (%s)\n", EXPRESSpass,
                 s->symbol.name, OBJget_type( s->type ) );
    }

    SCOPEresolve_expressions_statements( s );
    STMTlist_resolve( statements, s );

    s->symbol.resolved = status;
}
`
