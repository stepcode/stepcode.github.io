---
title: BRL-CAD patches
---

October, 2012 - patches to be merged from the BRL-CAD SVN repo

Ignore the number in italics - it is a git commit id from an svn import
operation. It is present here to ease patch creation, and does not refer
to the GitHub repo.

**If you move a commit from one category to another, please leave the
svn revision & git commit id intact, so that I can extract the page text
and run a script on it.**

Revision Range
--------------

For this list, revisions
[r45683](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=45683)
through
[r52540](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=52540)
have been considered. Earlier BRL-CAD revisions had already been merged;
any later revisions have yet to be examined.

Compiler warnings, Coverity
---------------------------

[r48327](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=48327)
*3ac1cb4* strcpy() is unsafe to use given the 'n' argument is a
parameter to the function. use strncpy() instead so we can always
null-terminate the result. issue detected in brl-cad coverity scan (cov
cid 1925)

[r48833](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=48833)
*5b62b1a* initialize all of the class fields. fixes report from coverity
UNINIT_CTOR check. (cid 2014)

[r48834](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=48834)
*a33a60f* initialize all of the class fields. fixes report from coverity
UNINIT_CTOR check. (cid 2034)

[r49068](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49068)
*b2dd1f0* Can't take it any longer. Doggy bag all the gcc vomit about
SCL's qualified type errors. Reduces the build log by about 16MB, 78k
warning lines, approx 765 unique instances. Quell them all with a teeny
little one-liner bit of scripting based on the build log output: for
match in \`grep qualifiers build.log | sort | uniq | cut -d: -f1,2\` ;
do export file="\`echo \$match | cut -d: -f1\`" ; export line="\`echo
\$match | cut -d: -f2\`" ; export pline="\`expr \$line - 1\`" ; if test
"x\`sed -n \${pline}p \$file |grep const\`" = "x" ; then sed -n
\${line}p \$file ; sed "\${line}s/\([[:space:]]*\)const \(.*\)/\\1\\2/"
\< \$file \> \$file.sed ; mv \$file.sed \$file ; else sed -n \${pline}p
\$file ; sed "\${pline}s/\([[:space:]]*\)const \(.*\)/\\1\\2/" \< \$file
\> \$file.sed ; mv \$file.sed \$file ; fi ; done As to the issue at
hand, there is no such thing as returning a "const int". It's just a
value (same goes for all the non-pointer return types). Old SGI compiler
was one of the first to be pedantic about that mistake, but gcc wised up
a few years ago and warns about it now too.

[r49069](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49069)
*51b1f9a* more warning quellage. shouldn't pass string constants to
char\* parameters as they should be considered immutable/const. make
SelectTypeDescriptor() constructor take a const char\* instead,
fortunately TypeDescriptor's constructor is correct.

[r49566](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49566)
*0a4cb29* address some constant string warnings

[r49667](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49667)
*021cd6f* suppress unused variable warnings

[r49683](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49683)
*d9db160* Generated step sources raising return-type qualifier warnings
from improper use of const. Implement intended behavior by returning
const versions of typedef'ed reference types. Related to r49068.

[r49687](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49687)
*0583fe1* Address warnings about non-explicit base class initialization
by adding intialization list to generated copy constructors.

[r49973](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49973)
*c338e11* Ah, I see now. g++ warning was from conversion when calling
default constructor EntNode(char \*nm = (const char[])""). Git 8e256d7
suppressed warning by calling with (char\*)"". Real solution is to make
the parameter const.

[r50222](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50222)
*7f5707c* initialize all of the class members. cid 2014 UNINIT_CTOR.

[r52252](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=52252)
*b1a2e88* quell warning on unused var since it won't necessarily get
used given its use is in conditional code

Whitespace, preprocessor, cleanup
---------------------------------

[r45683](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=45683)
*76d5fff* leaking something nasty

[r46648](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=46648)
*010efda* ws consistency removing trailing ws and much more (see
sh/ws.sh)

[r47187](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=47187)
*3099bef* \#include ridiculousness. full path to sys/stat.h (and dirent)
is not portable.

[r47239](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=47239)
*44b21f3* added missing header guard

[r49204](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49204)
*90bb05f* Clean up some ws in src/other

[r49477](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49477)
*736b104* remove some dead code

[r49571](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49571)
*2299c2e* remove references to non-existent function

[r49665](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49665)
*f86a139* remove unused variables

[r50478](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50478)
*ffa8a4e* remove some commented code

[r50561](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50561)
*17a7e8c* consolidate definitions of STRING_DELIM

[r50801](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50801)
*0469371* don't believe I have any account names as morrison with
stepcode affiliation

[r51527](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51527)
*f2bedf3* ws

[r52250](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=52250)
*f565ff2* save a few bytes, eliminate generated trailing ws

[r52265](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=52265)
*cd7caba* add missing header guard

Parser
------

[r47006](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=47006)
*ba7f5d7* added initial bison to lemon syntax conversion of expparse.y

[r47028](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=47028)
*6fe4e9d* indent/ws

[r47038](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=47038)
*c24fc7a* making choice for ambigous reduction explicit to suppress
conflict error from lemon

[r47039](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=47039)
*565a6eb* seems lemon requires real type name in type declaration

[r47040](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=47040)
*307c8ca* Added disabled macros to build temp fedex_new target for
development. Added expscan.re to build against, but it has not yet been
converted to re2c.

[r47152](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=47152)
*4f761f7* working through type-mismatch compile errors

[r47157](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=47157)
*9601319* got lemon source compiling; not yet operational

[r47163](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=47163)
*f3def5d* added new version of express.c with lemon parsing loop;
building fedex_plus with lemon as well

[r47197](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=47197)
*d0799fd* build new scanner output into new libexpress

[r47198](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=47198)
*f22ab86* putting token type definition in its own header

[r47201](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=47201)
*63dbcdd* making lemon parser sources the only parser sources

[r47203](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=47203)
*36d4faf* remove debug output

[r47257](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=47257)
*3910a5d* yylval is YYSTYPE, not int

[r47259](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=47259)
*b2a3656* Doing state init via func call since lemon isn't running
start-symbol action as soon as bison was.

[r47261](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=47261)
*a992692* typo in action was causing segfault

[r47304](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=47304)
*d5ca57d* add token printing debug routine

[r47314](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=47314)
*fe5a91d* Developing routine to print parser return object, useful for
inferring parser behavior.

[r47317](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=47317)
*1b37638* making progress; learning about the Express object structure
as I go

[r47321](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=47321)
*1c7654f* pass null to parser at eof

[r47322](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=47322)
*1717658* Added missing rule assignment. Lemon parser now gives same
(error) output as bison parser for all but ap239.

[r47336](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=47336)
*a21ace8* have lemon print message on stack overflow

[r47348](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=47348)
*ad24a24* add declarations for lemon functions

[r47349](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=47349)
*67cf76c* s/int/YYSTYPE for yylval. Incorrect type was causing memory
corruption.

[r47461](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=47461)
*abc6f2c* add modified lemon_target macro

[r47462](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=47462)
*9ece199* modified CMakeLists for alt lemon macro

[r47463](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=47463)
*71b01bd* Get the FindLEMON logic working with the new paradigm
(specifying the target header file)

[r47465](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=47465)
*f891d79* FindYACC no longer used; removed

[r47468](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=47468)
*d9fedf1* quiet messages for now

[r47642](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=47642)
*f47b818* sync top-level cmake file

[r47819](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=47819)
*ab5d701* Make sure the executables are present before we try doing
anything with them.

[r47882](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=47882)
*4823666* Make another stab at reworking the third party executable
logic - idea is to support specifying the full path to an executable
from the command line and have 'the right thing' happen.

[r48033](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=48033)
*33c0bba* Update the other FindLEMON files

[r48059](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=48059)
*3888df9* Rework the non-tcl 3rd party logic as well. Split the build
target macros for code generators into their own files, so we don't have
to load the Find\*.cmake files in all situations.

[r48076](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=48076)
*8029a39* Not really sure what's going on with printScope here...

[r48102](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=48102)
*df2381c* Do a little rework on the lemon target macro - saw an error:
Error renaming from 'expparse.c' to 'expparse.c': No such file or
directory - this might happen if lemon does something wrong, but it
could also mean lemon isn't done and the copy command tries to proceed
anyway, so split out the steps to make intermediate file dependencies
explicit - may help.

[r48121](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=48121)
*b5c7c24* initial build of step express parser using perplex scanner

[r48147](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=48147)
*8c7d2a7* fixed a few typos

[r48329](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=48329)
*efe7278* default code was being appended to rule code to prevent
fall-through; now requiring a cl flag to avoid generating unreachable
code

[r48548](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=48548)
*c84d3c8* Go ahead and depend on the template file when running lemon -
it's usually static, but we just had a case where it WAS changed, so
check in the future.

[r49161](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49161)
*334e727* Fix shiftwidth for vim in .cmake files

[r49201](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49201)
*9426397* Sync src/other copies of LEMON_Util.cmake

[r49205](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49205)
*73eb85a* Try to be better about using misc/CMake .cmake files by
default. Tweak the listing of additional files to clean from lemon
output.

[r49207](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49207)
*f51701b* remove debug message

[r49432](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49432)
*2d2522e* looks like we forgot to ignore a token

[r49434](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49434)
*9a14545* another missed ignore

[r49750](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49750)
*9977cc9* Nevermind the LoadMacros hack - just prevent the re2c/lemon
macro definitions from being overwritten if they're already defined
using Alexander Neundorf's tip from
<http://www.cmake.org/pipermail/cmake/2008-February/019776.html>.
BRL-CAD defines 'em first, so the src/other copies won't get loaded
(makes sure older versions of macro files that might linger in src/other
don't stomp misc/CMake versions) but stand-alone builds will use the
local copies. Properly set up search ordering with CMAKE_MODULE_PATH
should take care of this for the find_package commands, but the utility
macros are separate and so must be handled differently.

[r49772](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49772)
*ecb1f93* Go ahead and sync the toplevel files from
<https://github.com/mpictor/StepClassLibrary> - not all of them apply to
our branch as yet, but the idea is to sync the two trees so get these
out of the diff. Eventually we'll have a patch to submit back to the
github project, so updates to these files for things like re2c/lemon
will be part of that.

[r51476](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51476)
*76a52ce* Start building towards an SCL build that can work with or
without perplex/re2c/lemon. Fair bit more work to do - these are just
the fundamental essentials.

[r51481](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51481)
*6e4f011* Don't want a BRL-CAD path hardcoded into the perplex CMake
macros, now that the prospect of them being used elsewhere is real.

[r51482](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51482)
*a7c1289* Try to be a little more helpful with the template error
message.

[r51485](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51485)
*0cccc28* use generated lemon variables to avoid unused warnings

[r51496](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51496)
*eddc17c* Get a proper AUTO/ON/OFF toplevel configuration variable in
place to control the use of perplex/re2c/lemon in SCL.

[r51497](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51497)
*268de7a* Start working on the easier verification case - verifying
generated sources haven't been monkeyed with.

[r51498](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51498)
*3cecbec* Checkpoint some more work on generated src management.

[r51499](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51499)
*dc7b48a* Update generated sources to actually match the current inputs
- this will eventually be automated but that part's not in place yet.

[r51500](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51500)
*83dac30* More tweaks and added logic to generated source verification

[r51502](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51502)
*7d1d626* Be noisy for now so it's clear what's actually going on, fix
copy-paste error.

[r51504](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51504)
*2014c16* Add a README file for the generated sources explaining how
this will work...

[r51506](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51506)
*07623f2* Can't include debugging lines if we're going to manage the
generated sources this way.

[r51507](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51507)
*007f25f* Add necessary re2c flag

[r51508](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51508)
*cc26dcf* Fix README and add header comment to verification info

[r51509](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51509)
*57c2754* Add management routines for syncing info back into the
generated source tree.

[r51510](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51510)
*b2afab6* Use DEBUGGING_GENERATED_SOURCES to allow re2c debugging
information to appear in re2c intermediate output. Disable normal
behavior while doing so, so the debug-enabled output won't poison the
MD5 management mechanism.

[r51528](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51528)
*ae57d2f* Fix dependencies for verification targets.

[r51533](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51533)
*013e155* Upgrade template searching logic a bit, in light of new
perplex build logic. In the 'standard' case, builds using perplex now
stand a chance of 'just working' without requiring manual template
specification.

[r51567](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51567)
*10290fa* Tweak handling of perplex template

[r51575](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51575)
*7109233* Sync generated source file.

[r51734](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51734)
*4840692* harden managed sources file against weird pathnames

[r52006](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=52006)
*1ceb95b* Update documentation on handling of INSTALL.new,
configure.new, and perplex/re2c/lemon cached files.

[r52540](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=52540)
*de2a123* typos carl noticed, but looks like they're all benign

CMake
-----

[r47244](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=47244)
*7f0101d* remove references to non-existent headers

[r49115](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49115)
*93238df* Go with 'lib' for all instances of
CMAKE_LIBRARY_OUTPUT_DIRECTORY

[r49163](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49163)
*792b7ea* Dispose of the one-off CHECK_C_FILE_RUNS and instead
enhance CHECK_C_SOURCE_RUNS. Will try to contribute the change
upstream.

[r49164](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49164)
*6529fb9* Quote SOURCE in case of spaces in pathnames...

[r49321](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49321)
*9e94d0c* Hopefully this will get things cleaned up on Windows again.
Untested.

[r49763](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49763)
*cd05b6d* Rework handling of config.h files, with an eye towards hitting
the disk less - seems to shave a couple seconds off the configure
process on Linux.

[r49791](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49791)
*effdeed* Don't need the messages when SCL is a subbuild.

[r49840](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49840)
*f722ec4* Significant simplification of the distcheck logic - reduce it
to two macros, one of which calls the other. Add documentation, improve
behavior in some corner cases, enforce a convention we already pretty
much followed by default of using relative paths to specify source files
in the source tree (this is a robust way to spot generated files in
build target definitions, since support for an out of directory build
requires that they be specified with their full CMAKE_BINARY_DIR
output path.)

[r49859](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49859)
*10fd188* add newline

[r49860](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49860)
*94fbf3b* let the toplevel build tell us where to put scl man pages

[r49867](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49867)
*13786d1* Finally bite the bullet and start reworking the build logic to
be robust to weirder source and build directory names. This is not
everything needed, but it's a step in the right direction.

[r49905](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49905)
*f3dad58* Take a stab at making configure_file cmakefiles appending
more robust

[r49924](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49924)
*3b7b6ed* libs-\>libslist, per 49867

[r49925](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49925)
*805c7c0* Need quotes for this comparison...

[r50420](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50420)
*5213861* more stl linkages for external deps compiling through cache or
different compilers

[r50426](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50426)
*f2be60e* Try to make the stdc++ usage a matter of detection instead of
hardcoding. Untested on systems which would show the issue.

[r50441](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50441)
*a1ab6a0* rename STDCXX_LINKLIB to STDCXX_LIBRARIES to comply with
cmake's documented convention (and it can require multiple libraries
like -lm and -lc, too)

[r51372](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51372)
*f6a6295* scl_version_string.h needs to be generated before fedex.c is
compiled

[r51397](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51397)
*125234b* missing semicolon

[r51459](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51459)
*c921d92* Don't use absolte path for install directory.

[r51555](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51555)
*9a0b7d0* hmm - exppp tried to build before fedex, and didn't have
version_string. Make the version string dependency trigger on expres
build

[r51568](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51568)
*596fd9a* fix SCL cmake logic

[r51576](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51576)
*9e2f601* Thanks Keith for reminding me of the potential problem - strip
newlines out of md5 calculations so Windows can't toss in a monkey
wrench.

[r51593](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51593)
*fc87734* exppp needs base lib for getopt

[r51594](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51594)
*81941ca* consistently use spaces rather than semicolons in list
arguments

[r51716](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51716)
*ee4fc2e* Use semicolons in lists for SCL_ADD macros as well.

Bug fix, reorganization, rewrite
--------------------------------

[r47200](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=47200)
*8707df0* replaced conditional variable declarations with explcit ones
to simplify building

[r47243](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=47243)
*7ff6798* Removed toggled declarations/definitions in headers. Headers
include only declarations, and explicit definitions found in appropriate
sources.

[r47324](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=47324)
*403540b* remove dead code

[r47337](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=47337)
*0c09ca4* set dangling pointers to null

[r47338](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=47338)
*6e61e3a* s/malloc/calloc

[r47790](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=47790)
*684d759* Fixed asStr(), was broken in the scl_string -\> std::string
rework.

[r48192](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=48192)
*b66ce02* need to generate default return statement per fix in r41174

[r48193](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=48193)
*d2ba4dc* don't generate unused variables, per r41173

[r49030](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49030)
*fe71ad4* fix size in memset() initialization when growing buffer

[r49031](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49031)
*fb5c87d* make sure to ClearEntries() when array instances not owned by
MgrNodeArray otherwise parent class GenNodeArray will try and delete
memory error

[r49185](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49185)
*811d380* use __inline__ instead of inline for c89 compilation

[r49186](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49186)
*5b3f97c* use static_inline instead of 'static inline' so that we're
consistent with other uses and expand correctly to the right symbols for
this compilation

[r49193](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49193)
*441414a* more static_inline propagation so we support strict c89 mode

[r49478](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49478)
*ea46e08* don't output unused variable

[r49570](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49570)
*d0a68a9* fix bad int- and float-to-string conversions

[r49581](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49581)
*fa66a3a* logic looked a hair off (trying recovery even if bad bit set).
rewrite for readability.

[r49622](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49622)
*aebfb14* Copy changes to the commited SdaiCONFIG_CONTROL_DESIGN.cc,
which disables adding of certain parent-class attributes on object
creation, to the corresponding generation code.

[r49709](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49709)
*b8e3088* incorrect copy loops were indexing past end of source strings

[r49710](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49710)
*f09c469* ensure null termination as well

[r49754](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49754)
*3ad7117* move some sdai sources from clstepcore to cldai

[r49825](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49825)
*92efc8b* restore STACKempty macro that was removed in r47243 for no
particular reason

[r49981](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49981)
*a76474f* missing function prototypes causing bad compilation on Mac
10.6

[r51427](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51427)
*e86e777* remove unportable/unnecessary calls to unistd.h pause used
after certain errors to allow attaching debugger

[r51461](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51461)
*9b5c6c4* combine multiple definitions of LISTempty

[r51562](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51562)
*1023328* remove conflicting EntityClassName declaration

[r51577](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51577)
*fffe638* don't bother making practically useless fedex -z debug flag
portable; just remove it

[r51579](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51579)
*75220c8* strictly match EXPRESSinit_init defs to the express.h
declaration

[r51598](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51598)
*2684045* have check-express compile its own EXPRESSinit_init
definition like all the other programs that use fedex.c so we don't need
to conditionally override an express dll definition on windows

[r51720](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51720)
*41d66ee* move classes to break cyclic dependency and document in
clstepcore/README

[r51723](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51723)
*5f5c110* don't use scl_memmgr.h definitions if mem checks aren't
enabled

[r52251](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=52251)
*5804198* fix for a gcc internal compiler error due to inlining. make
AssignAggrCreator() be defined in a compilation unit.

[r52276](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=52276)
*f4ef1c7* Use stdarg.h unconditionally and avoid undefined behavior by
remembering to call va_end. Appears to fix fedex_plus crash seen when
doing a Windows release build.

Need to look at these more
--------------------------

[r49636](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49636)
*a3657e6* added the steptools ap express schemas

[r51120](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51120)
*f9110c3* use stdlib.h instead of malloc.h

Differs from GitHub
-------------------

[r47791](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=47791)
*f5b4ff4* Looks like possible debugging code left in during the
scl_string -\> std::string rework breaking STEPattribute::is_null()
for STRING_TYPE and BINARY_TYPE, commented out for now.

[r49071](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49071)
*07335d3* might make merging a bit more difficult or (more likely)
repeats work already done in the github tree, but helps ease our sanity
in the meantime. eliminate a slew of gcc warnings about string literals
being passed as char\* parameters when they should be treated immutable.
mark them all const.

[r49794](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49794)
*0f1486e* Replaced generated cleditor sources with tweaked copies of the
388901d versions from the mpictor git repo. These were apparently
generated by running fedex_plus on the Ed 2 header schema
(http://www.steptools.com/sc4/archive/imp-methods/10303-21-header.exp).

[r50389](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50389)
*5527ddf* reject SCL git df8f8d5 and replace temp array with vector

Will probably skip
------------------

[r45968](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=45968)
*4fbd00e* Key the static lib building on the build type. Exposed a
problem with making the trigger variable an OPTION in sub-builds - doing
so forces the setting into the cache and makes it impractical for the
AUTO_OPTION macro to do its thing. Fortunately, the only files doing
that were the ones we wrote - corrected them, and we're good to go.

[r48101](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=48101)
*d362332* Nick says he created this for debugging purposes and it can
go.

[r48180](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=48180)
*7a949a5* remove old debug header

[r49705](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49705)
*f615c39* remove miscellaneous unused files

[r51470](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51470)
*46fbcbc* Include fedex_python subdir to make it easier to build
fedex_python for testing. Make paths relative to avoid CMAKEFILES
warning.

Skip (duplicated effort, autotools, etc)
----------------------------------------

[r46913](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=46913)
*8065a91* Redo comments a bit in src/other/CMakeLists.txt

[r46914](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=46914)
*20df9d4* oops

[r47211](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=47211)
*2a6a16b* remove reference to non-existant file

[r47359](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=47359)
*b383b97* ignore scl_cf.h.in since autoheader will create it during
autogen.sh

[r48188](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=48188)
*e487dc0* adding a modified ap203 express file that fedex_plus doesn't
fail on

[r49192](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49192)
*02d36f2* include getopt.h directly in case we're compiling in strict
c89 mode

[r49476](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49476)
*e4ac75b* try to fix strings changed to std::string that still called
non-existant chars member function

[r49757](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49757)
*b4a28ab* remove step autotools files

[r49765](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49765)
*5fbe3db* remove unused config/\*

[r49773](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49773)
*74209c7* Add other toplevel files, update step.dist

[r49821](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49821)
*d87fde3* run astyle on SCL sources with misc/astyle.cfg options

[r51651](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51651)
*f76bb1b* remove exception specifications

[r51655](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51655)
*c239a1f* revert 51651 - breaks build on Linux

[r52410](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=52410)
*c4d9549* ignore/inclue the scl_cf.h.in header template

[r52411](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=52411)
*3742b9f* bah, it's not actually a repo file -- something is writing to
the src tree

[r52412](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=52412)
*aa75aec* don't ignore generated source, should be in bin dir

Commits from GitHub
-------------------

[r49771](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49771)
*0c85d2f* go with the mpictor github capitalization

[r49774](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49774)
*f2b45de* remove SCL clivfasd; deemed obsolete and removed from mpictor
git repo in a0353bc

[r49776](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49776)
*4337b40* Edge our CMakeLists.txt file and tree a little closer to the
github tree. base and fedex_python are turned off and ignored for the
moment.

[r49777](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49777)
*430217f* More syncing with github tree

[r49788](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49788)
*2594021* Sync step doc dir to github, except convert postscript files
to pdf and fix page ordering of Fed-X document

[r49790](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49790)
*f2fb6cc* Grab some minor changes from github

[r49793](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49793)
*6524b04* Make a stab at syncing with the github data dir - we need to
keep ap203edit.exp, since that's the one that works with our step-g
converter.

[r49795](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49795)
*89a25f0* don't use a generic IS_SUBBUILD variable - bad idea.

[r49797](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49797)
*bacb8c1* remove symlink program; removed from mpictor git repo in
23cf6a5

[r49799](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49799)
*e20cd29* remove fedex_idl program; removed from mpictor git repo in
dbbf4b9

[r49822](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49822)
*bde4c12* remove references to OODB/O3DB as in mpictor git repo ca0824d
and d067534

[r49824](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49824)
*85c067c* Removed references to PART26/CORBA and ODI_OSSG. Corresponds
primarily to SCL git e99240a, d6aa13f, and 4c5a8e0.

[r49826](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49826)
*71760df* remove unused variable; SCL git 47b4963

[r49827](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49827)
*bc256e6* initialize some uninitialize variables; SCL git b9156ad

[r49830](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49830)
*2fa8eb4* remove references to non-existant dir.h and SCLString to match
SCL git a0353bc version

[r49836](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49836)
*cf57641* Replaced basic.h's Boolean/True/False with bool/true/false via
stdbool.h or else scl_stdbool.h. Includes changes from SCL git e40cbca
and 71bd7b2. Honest attempts made to ensure all affected symbols were
actually being used as real booleans (as opposed to sdaiEnum.h's trinary
Boolean type).

[r49837](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49837)
*70b98d3* apply warning fixes from SCL git 19e501a

[r49897](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49897)
*e694174* sync comment changes from 7b54e23

[r49899](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49899)
*f880277* Fix printf format errors. Informed by SCL git c075554,
0366706, af7d90d, ec41f80, d33d4c5, and e52c290.

[r49903](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49903)
*7d85d42* sync with SCL git 993167e

[r49904](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49904)
*93442dd* match SCL git style

[r49913](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49913)
*3334e88* remove unused variables as seen in SCL git 1492641 and 2b31086

[r49963](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49963)
*1b008b8* Address unused variable warnings first quelled in r41173.
Rather than creating 30 named pointer vars, create a pointer array and
use a cleaned-up version of SCL git c1b5743 to choose a good size for
it.

[r49968](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49968)
*2f53810* Remove unused variables as identified by SCL git 89237b8,
860bd45, 90de2d7, d56117f, f3e2eaf, and 7a68580.

[r49969](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49969)
*e791605* variable initializations informed by SCL git cc155a8 and
b9156ad

[r49970](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49970)
*64bb184* EntNode doesn't have a no-parameter constructor; construct
from empty string. SCL git 8e256d7.

[r49971](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=49971)
*9a7e770* might as well match git formatting

[r50158](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50158)
*3514d1e* Apply SCL git d6d7c48 changes. SCLP23 macros replaced with
simple SDAI_ prefix.

[r50171](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50171)
*3c20152* remove unused variables and functions identified in SCL git
8ce79ec, 73cc97f, e98d00f, 63295f1, and 2a0ee4e

[r50179](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50179)
*865bbd8* apply changes from SCL git d6da40c and 275977d (commented code
removal/style)

[r50278](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50278)
*9c55d45* changes based on SCL git d35f73f and 696d8e3

[r50279](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50279)
*77856a3* some const char corrections including remaining changes from
SCL git 4cf16d7

[r50294](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50294)
*37376b7* replace shorts with ints along the lines of SCL git d2baec0,
but be more judicious in using unsigned versus signed

[r50295](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50295)
*4865978* ignore spaces in generate_attribute_name. SCL git 1ebee6d

[r50303](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50303)
*dd9acf9* apply more commented code removal from SCL git c0b2b05,
37bbfd3, 9324acc, d7410be, 62304a7, and 0dccb8b

[r50306](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50306)
*76e6dc7* apply SCL git db70465 removing more unused variables

[r50307](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50307)
*b93b50c* remove another unused variable (LISTdo already creates one)
identified in SCL git 0153f15

[r50322](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50322)
*9b92011* Remove rcsid strings from sources and don't generate Id
comments. SCL git 922a795 and 9367823.

[r50331](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50331)
*7fefe24* add default switch cases as in SCL git b10a697, but avoid
using abort if the error can be logged and/or returned

[r50335](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50335)
*19bcdf3* apply changes from SCL git f678f0b, but extract assignments
used as truth values for benefit of windows

[r50385](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50385)
*9ecb334* minor string comparison improvements from SCL git 1ad14e1,
70a8382, 7a6ba24, c316f21, and 572e9ad

[r50387](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50387)
*87d704f* use stringstream to correctly print file id, SCL git 71b3a28

[r50394](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50394)
*483c8f3* fix missing types, prototypes, and returns based on SCL git
562f4de, 6e6b8ca, 2dc4e7e, fd1d32c, 99407fb, and b5238df

[r50408](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50408)
*46f6605* apply cleanup changes from SCL git 9f83ece, 5e6ebb0, and
ca50d53

[r50421](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50421)
*79f5a3b* signed/unsigned comparison changes based on SCL git f479cf4
and 402225e

[r50422](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50422)
*3802f9d* cpp initialization warning fixes from SCL git f727293,
b6bebbb, and 3156ea7

[r50431](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50431)
*e63b935* Using std::string c_str() too much and empty() not enough.
SCL git 2295e71 and b759a0e.

[r50432](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50432)
*5e7986c* ws and old comment removal from SCL git 657a283

[r50436](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50436)
*98b327d* remove some goto statements based on SCL git a13ba21 and
ecd400c

[r50438](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50438)
*2082d23* Apply SCL git 900d94d. fedex_plus no longer generates
make_schema file.

[r50467](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50467)
*3461161* Rewrite PushPastString to avoid two consecutive get/putback as
identified by SCL git abb3add. Also if first char on stream isn't string
delimiter, don't take it off the stream.

[r50468](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50468)
*a187ad8* apply SCL git 0d9c16d, which fixes fedex_plus failure on
ap203e2 schema

[r50470](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50470)
*37f77fa* Make HASHsearch item param const. SCL git defe0dd.

[r50472](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50472)
*541ade5* Remove P21CommentRep() and move p21Comment string to stack to
simplify things. SCL git 219957d.

[r50477](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50477)
*f561ff6* SCL git de55c37, remove unused variables

[r50492](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50492)
*e719967* Fix and doxify comments, plus misc cleanup. SCL git 3e8c116,
5dc0439, 5d36b32, and 65791a2.

[r50506](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50506)
*86decc8* Cleanup in clstepcore. SCL git 239ce49 and f9b9383.

[r50557](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50557)
*173316a* Apply changes from SCL git 1016b07. Use std::string more
frequently and move ErrorDescriptor message strings to stack to simplify
things.

[r50584](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50584)
*e63ac83* Apply changes based on SCL git 6e9b5a7. Creates GetLiteralStr
function to implement and extend functionality common to
SDAI_String::STEPread and PushPastString.

[r50598](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50598)
*9a3670a* Add collectAttributes function based on the one added by SCL
git 290850a.

[r50630](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50630)
*1262db4* apply more changes from SCL git 290850a: cleanup some multiple
inheritance code - passing around attribute list to print routines
instead of rebuilding it

[r50631](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50631)
*b1da4f6* apply rest of SCL git 290850a: change output suffix of
aggregate select types from 's' to '_agg'

[r50632](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50632)
*49ac297* apply header guard symbol change from SCL git d1cd32b

[r50654](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50654)
*f177db2* Apply changes from SCL git 4858af2 removing code supporting
step files (N279 files) that pre-date ISO 10303-21:1994.

[r50682](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50682)
*89d10d4* apply SCL git e72ca29; remove some superfluous boolean types
and use std bool more often

[r50741](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50741)
*ba6c8dd* Have STEPfile::schemaName return std::string instead of
writing char\* arg. SCL git b8fc557.

[r50745](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50745)
*ab400df* Remove a few unnecessary extern declarations. SCL git aef6e73,
5c8c5aa, 15f9c40.

[r50762](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50762)
*4c78a90* Allow local variables to have generic types; fixes failure on
ap239 express schema. SCL git 254b5a3.

[r50767](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50767)
*9ea3ba0* optimize utype_member based on SCL git 27ce560

[r50770](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50770)
*26fa107* Remove some unneeded functions. SCL git 1faaf69 and 2d7ed17.

[r50772](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50772)
*1357cbd* Apply SCL git f5a130a. Loosens restriction on dictionary
duplicates.

[r50791](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50791)
*8375f1f* Simplify filepath handling and use more std::string and bool.
SCL git 19a1bae and b277759.

[r50792](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50792)
*6512c4f* change return type to bool; SCL git 4dc0891

[r50794](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50794)
*b365619* Another int/bool substitution. This is SCL git b277759; r50791
was actually SCL git 1b69382.

[r50795](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50795)
*e8e6f2b* cleanup from SCL git c497168

[r50798](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50798)
*ae87712* better error printing; SCL git 99abb18 and 6b95067

[r50810](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50810)
*4fc4845* Simplify STEPread a bit. SCL git 6871bc4.

[r50814](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50814)
*d888228* Add strict flag to STEPread functions; affects handling of
missing attributes. SCL git de3495d and 373d415.

[r50815](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50815)
*4fe9ad8* correct SCANsave_comment; SCL git c6bc7ec

[r50892](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50892)
*2bb7046* generate spaces instead of tabs; SCL git 86b9f12

[r50893](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50893)
*0745c75* Use UNKNOWN_TYPE when an attribute has no NonRefType. SCL git
6aa4695.

[r50895](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50895)
*cb235b2* ensure constructors receive non-null AttrDescriptor; SCL git
e547807

[r50903](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50903)
*df6a719* Put generated globals in a namespace. Namespace declaration
written to \*Names.h. SCL git 88e9634, da0a395, and 3ed8797.

[r50909](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50909)
*60698f4* cleanup from SCL git cb35164 and 1cfb41d

[r50910](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50910)
*1bb2464* cleanup from SCL git 0bb182b and ed8474e

[r50940](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50940)
*2e0f0ef* MSVC fixes from SCL git 6226717 and 879f509

[r50955](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50955)
*f1d3cb3* start adding symbols for MSVC dll import/export; SCL git
ba12196

[r50965](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50965)
*588956b* more symbols for MSVC dll import/export; SCL git f853b99

[r50985](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50985)
*4e45ba2* Add public domain getopt implementation. SCL git c3f9ff5,
dc302ea, and 2d26da7.

[r50986](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50986)
*92bdca1* actually add getopt sources

[r50987](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50987)
*ef4b92c* add dll export symbols to clutils; SCL git 457d51e

[r50989](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50989)
*82afeb8* add dll export symbols to cldai; SCL git c409145

[r50991](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50991)
*a4ea28b* add dll export symbols to clstepcore; SCL git 0705c50

[r50992](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50992)
*5d25423* add dll export symbols to cleditor; SCL git 2e01a01, c771b27,
and 0869e41.

[r50993](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50993)
*e331b0c* fix buffer overrun based on SCL git 5e9dfd7

[r50995](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50995)
*ad9a78f* support comments in entities; SCL git 4ddce86

[r50996](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50996)
*308cedf* Have fedex_plus generate dll import/export symbols. SCL git
80208dc.

[r50997](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=50997)
*667b223* Prefix scl_hash routines with SCL_. SCL git 4740f4d and
737c53e.

[r51001](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51001)
*aad496c* warning fixes from SCL git 2179c8a and ca4940e

[r51004](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51004)
*c6b372e* warning fixes from SCL git 166425a and dcdd77a

[r51029](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51029)
*daa2b2f* warning fixes from SCL git 7712b9b and 03fd892

[r51038](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51038)
*fe0bd1e* warning fixes from SCL git 07ed8f6, 0aa9b5d, and 2b0da3f

[r51055](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51055)
*5fe4bef* add process.h for getpid on windows; SCL git 870edbf

[r51056](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51056)
*72b7649* suppress return warning; SCL git f688f2a

[r51057](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51057)
*12a0aec* cleanup/ws from SCL git 1da31f6 and 3aee5f3

[r51058](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51058)
*6d7bb27* handle indexing on generics; SCL git ed76f0b

[r51066](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51066)
*92e2cd1* Warn about indexing a select with mixed base types. SCL git
67f8897.

[r51067](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51067)
*f7da8c2* ws/style from SCL git 09f3472 and d94a449

[r51068](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51068)
*57e2678* Have SDAI_String and SDAI_Binary wrap std::string rather
than inherit from it. SCL git 82898d7.

[r51069](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51069)
*059b187* Borland-specific stuff from SCL git c0c423c and 3a9fa99.

[r51070](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51070)
*ce6e56a* put enums in separate table; SCL git c415e49

[r51072](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51072)
*783150e* Warn about indexing binary types instead of failing. Allows
fedex_plus to produce output for ap221 and ap235 express schemas. SCL
git 4cd7e7c.

[r51074](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51074)
*448eddb* remove 'backwards compatiblity' symbols; SCL git 1481950 and
a63ac73

[r51078](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51078)
*661b008* Allocate aggregate members on heap. SCL git 809e1dd, 260fd55,
and e421f70.

[r51093](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51093)
*fd5654a* break up generated strings; SCL git 212c114

[r51096](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51096)
*e5e8012* Apply SCL git 3fd2222 which removes scl_char_str_list
class, but std::vector makes a better replacement than std::deque.

[r51097](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51097)
*678d07e* eliminate a temp buffer; SCL git 1cc2774

[r51104](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51104)
*36947b9* use scl_memmgr in express; SCL git 82c84e7 and 4d6d249

[r51105](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51105)
*17b28d9* use scl_memmgr in exppp and fedex_plus; SCL git 7ce8bcb and
4e0d73d

[r51141](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51141)
*9580c9e* use scl_memmgr in clutils; SCL git 010e02b

[r51145](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51145)
*ab135d3* use scl_memmgr in clstepcore; SCL git 245ff14

[r51146](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51146)
*6766111* use scl_memmgr in cldai; SCL git b49d2be

[r51147](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51147)
*8667bf7* use scl_memmgr in cleditor; SCL git 3be4220

[r51235](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51235)
*d56d107* Use scl_memmgr in generated schema libraries. Since
scl_memmgr.h makes "new" a macro, it has to be included after uses of
placement new to avoid breakage. SCL git d8d293b.

[r51236](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51236)
*051b262* avoid generating 'else if' to avoid MSVC limit of 128; SCL git
dea7f8c

[r51238](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51238)
*d3a8e5e* add fedex_plus/express memory cleanup function; SCL git
f5d0cc5

[r51239](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51239)
*21e086d* fix memory leaks reported by scl_memmgr; SCL git 3010afa

[r51240](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51240)
*e7c22aa* fix memory leaks reported by scl_memmgr; SCL git f7cde9f

[r51241](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51241)
*b5ec68f* remove \#if 0 code; SCL git ee13cda

[r51242](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51242)
*f05c8ad* more verbose warning message; SCL git c84330b

[r51247](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51247)
*72e194b* partial support for aggregate bounds that aren't compile-time
constants; SCL git 7425e55d

[r51250](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51250)
*5230033* cleanup from SCL git a86b035 and 6f60a8a

[r51252](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51252)
*19cd0eb* print aggregate name instead of data member name; SCL git
a72fa6e

[r51253](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51253)
*799015d* fix Registry memory leaks; SCL git a9173c8 and 626bb73

[r51254](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51254)
*36442c5* free attributes list; SCL git c77471a

[r51255](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51255)
*bef24b2* stash unnamed types in a list so they can be freed; SCL git
04f4c1d

[r51256](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51256)
*e8b1eff* fix STEPaggregate memory leaks; SCL git 8a2665e

[r51257](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51257)
*dfc6e17* fix memory leaks; SCL git a1d6b25

[r51261](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51261)
*fb76485* fix memory leaks; SCL git 5aca337 and dd6ef88

[r51263](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51263)
*ee9d842* mark some member functions const; SCL git 225180f

[r51268](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51268)
*c92ebbb* support for checking read/write progress; SCL git 0bea3ef

[r51270](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51270)
*5d3a447* remove extra semicolons; SCL git 17cec63

[r51272](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51272)
*81e1fb5* s/cstddef/stddef.h/ for benefit of borland; SCL git e45d705

[r51341](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51341)
*510d564* Address warning about indexing with char type values based on
ASCII characters (same problem as in r51103). Unlikely to be a problem
in this case so just quell by casting to int. SCL git 512968e and
425a9c3.

[r51343](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51343)
*9891ba7* Some unapplied changes from SCL git a362210, 696d8e3, and
2b46efb, mostly fixing STEPattribute::is_null.

[r51344](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51344)
*4a93e88* need shlwapi for Windows path handling routines; SCL git
02feb6f

[r51345](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51345)
*9812081* simplify function prototype; SCL git 07d8791

[r51346](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51346)
*c7a150d* add missing lib dependencies; SCL git d0293fd

[r51358](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51358)
*48836ca* Update version strings in fedex, fedex_plus, generated code,
and documentation. SCL git 6851b27, fa615a1, dc30ee2, d190a1e, a33cba8,
698b9e0.

[r51435](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51435)
*9cf01aa* Add/remove files to match github data directory. Will use
their copy of the edited ap203.exp to generate step-g sources.

[r51471](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51471)
*fcbe328* update fedex_python sources to SCL git 7ffbb73 versions, but
use the classes.h declaration of the FundamentalType func for
consistency

[r51472](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51472)
*b7f6bff* apply changes for fedex_python from SCL git 10999e7 and
2dcfaed

[r51473](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51473)
*842786b* update python scripts to SCL git ee13526 versions

[r51486](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51486)
*1683d67* missed ws and doxification changes from SCL git f9b9383

[r51563](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51563)
*63b3633* rename getopt to sc_getopt and include it as part of base
lib; SCL git 1a60cf9 and dd93a96

[r51566](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51566)
*8717c87* update dll export macros and remove local definitions; SCL git
7be54f3

[r51578](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51578)
*cb42eb1* Rename fedex program to check-express. Need to link it against
base lib; SCL git a42a448

[r51581](http://brlcad.svn.sourceforge.net/viewvc/brlcad?view=revision&revision=51581)
*0e8494f* s/snprintf/sprintf in absence of snprintf wrapper. sprintf is
pretty safe for this usage; SCL git 910faf0
