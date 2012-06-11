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
`   download       Turn on the "Download Code" link for this block of your code `<span style="color:#ff0000">**`NOTE:`**` this option is broken!`</span>  
`   tabwidth='n'   How many spaces does a TAB represent`  
`   fileurl='s'    Instead of processing the code provided between the tags, process the code at specified URL`

### C, with line numbers

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

### Diff

`
diff --git a/src/fedex_plus/classes.c b/src/fedex_plus/classes.c
index 4921649..1529387 100644
--- a/src/fedex_plus/classes.c
+++ b/src/fedex_plus/classes.c
@@ -402,39 +402,35 @@ int Handle_FedPlus_Args( int i, char * arg ) {
  ** Side Effects:
  ** Status:  complete 8/5/93
  ******************************************************************/
-char *
-generate_attribute_name( Variable a, char * out ) {
-    char * temp, *p, *q;
-    int j;
+char * generate_attribute_name( Variable a, char * out ) {
+    char * temp, *p, *q = out;
 
     temp = EXPRto_string( VARget_name( a ) );
-    p = temp;
-    if( ! strncmp( StrToLower( p ), "self\\", 5 ) ) {
-        p = p + 5;
+    p = (char*)StrToLower(temp);
+    if( ! strncmp(p, "self\\", 5 ) ) {
+        p += 5;
     }
-    /*  copy p to out  */
-    /* DAR - fixed so that '\n's removed */
-    for( j = 0, q = out; j < BUFSIZ; p++ ) {
+    while (*p) {
         /* copy p to out, 1 char at time.  Skip \n's and spaces, convert */
         /*  '.' to '_', and convert to lowercase. */
         if( ( *p != '\n' ) && ( *p != ' ' ) ) {
             if( *p == '.' ) {
                 *q = '_';
             } else {
-                *q = tolower( *p );
+                *q = *p;
             }
-            j++;
             q++;
         }
+        p++;
     }
+    *q = '\0';
     free( temp );
     return out;
 }
`

[Category:Code discussion](Category:Code discussion "wikilink")
