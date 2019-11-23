---
layout: docs
permalink: /docs/p21_cpp_example/
title: Minimal Part 21 C++ example
---

Based on [P21read](/docs/p21read/)

### Contents
* TOC
{:toc}


## Code


{% highlight cpp linenos %}
#include <sc_cf.h>
extern void SchemaInit( class Registry & );
#include <STEPfile.h>
#include <sdai.h>
#include <STEPattribute.h>
#include <ExpDict.h>
#include <Registry.h>
#include <errordesc.h>
#ifdef HAVE_UNISTD_H
# include <unistd.h>
#endif

int main( int argc, char * argv[] ) {

    // the registry contains information about types present in the current schema; SchemaInit 
    // is a function in the schema-specific SDAI library
    Registry  registry( SchemaInit );

    //the InstMgr holds instances that have been created or that have been loaded from a file
    InstMgr   instance_list;

    // STEPfile takes care of reading and writing Part 21 files
    STEPfile  sfile( registry, instance_list, "", false );

    // read a file, using the name from the command line
    sfile.ReadExchangeFile( argv[1] );

    // check for errors; exit if they are particularly severe
    if( sfile.Error().severity() < SEVERITY_USERMSG ) {
        sfile.Error().PrintContents( cout );
    }
    if ( sfile.Error().severity() <= SEVERITY_INCOMPLETE ) {
        exit(1);
    }

    /**************************************************
    ** do something with the data here
    ***************************************************/

    // write to "file.out", then check for write errors. The write operation overwrites any
    // errors caused by previous operations.
    sfile.WriteExchangeFile( "file.out" );
    if( sfile.Error().severity() < SEVERITY_USERMSG ) {
        sfile.Error().PrintContents( cout );
    }
}
{% endhighlight %}

## Include Paths

Stepcode's includes are not relative the top level of the stepcode
include directory, so multiple include paths are needed to compile this
example:

-   include/stepcode
-   include/stepcode/cldai
-   include/stepcode/cleditor
-   include/stepcode/clstepcore
-   include/stepcode/clutils

## Linking

Your executable will need to link to various libraries, likely including
a generated library, specific to the schema you are interested in. Once
generated, this lib can be found in build/lib with a prefix of
libsdai_.

It will also need to link with cldai, cleditor, clstepcore, and clutils - all found in build/lib.

If you get stuck, consider examining the compile/link commands used for one of the p21read executables. This can be done with **make VERBOSE=1_**:

`make VERBOSE=1 p21read_sdai_ap214e3`

## Related Pages
- [Basic Use](/docs/usage/)
- [Other examples](/docs/examples/)

