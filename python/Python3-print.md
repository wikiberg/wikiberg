# print in python3

> Converts the print statement to the print() function.


## Code


```bash
echo 'print "Hello world"' | tee /tmp/hello.py
```

    print "Hello world"



```bash
2to3 /tmp/hello.py
```

    RefactoringTool: Skipping optional fixer: buffer
    RefactoringTool: Skipping optional fixer: idioms
    RefactoringTool: Skipping optional fixer: set_literal
    RefactoringTool: Skipping optional fixer: ws_comma
    RefactoringTool: Refactored /tmp/hello.py
    --- /tmp/hello.py	(original)
    +++ /tmp/hello.py	(refactored)
    @@ -1 +1 @@
    -print "Hello world"
    +print("Hello world")
    RefactoringTool: Files that need to be modified:
    RefactoringTool: /tmp/hello.py



```bash
2to3 --no-diffs -f print --add-suffix=3 -n -w /tmp/hello.py
```

    RefactoringTool: Refactored /tmp/hello.py
    RefactoringTool: Writing converted /tmp/hello.py to /tmp/hello.py3.
    RefactoringTool: Files that were modified:
    RefactoringTool: /tmp/hello.py



```bash
cat /tmp/hello.py3
```

    print("Hello world")



```bash
# like 2to3, but futurize can add import from __future__ 
futurize /tmp/hello.py
```

    RefactoringTool: Skipping optional fixer: idioms
    RefactoringTool: Skipping optional fixer: ws_comma
    RefactoringTool: Refactored /tmp/hello.py
    --- /tmp/hello.py	(original)
    +++ /tmp/hello.py	(refactored)
    @@ -1 +1,2 @@
    -print "Hello world"
    +from __future__ import print_function
    +print("Hello world")
    RefactoringTool: Files that need to be modified:
    RefactoringTool: /tmp/hello.py



```bash
futurize --add-suffix=2 -n -w /tmp/hello.py
```

    RefactoringTool: Skipping optional fixer: idioms
    RefactoringTool: Skipping optional fixer: ws_comma
    RefactoringTool: Refactored /tmp/hello.py
    --- /tmp/hello.py	(original)
    +++ /tmp/hello.py	(refactored)
    @@ -1 +1,2 @@
    -print "Hello world"
    +from __future__ import print_function
    +print("Hello world")
    RefactoringTool: Writing converted /tmp/hello.py to /tmp/hello.py2.
    RefactoringTool: Files that were modified:
    RefactoringTool: /tmp/hello.py



```bash
cat /tmp/hello.py2
```

    from __future__ import print_function
    print("Hello world")



```bash
2to3 -h
```

    Usage: 2to3 [options] file|dir ...
    
    Options:
      -h, --help            show this help message and exit
      -d, --doctests_only   Fix up doctests only
      -f FIX, --fix=FIX     Each FIX specifies a transformation; default: all
      -j PROCESSES, --processes=PROCESSES
                            Run 2to3 concurrently
      -x NOFIX, --nofix=NOFIX
                            Prevent a transformation from being run
      -l, --list-fixes      List available transformations
      -p, --print-function  Modify the grammar so that print() is a function
      -v, --verbose         More verbose logging
      --no-diffs            Don't show diffs of the refactoring
      -w, --write           Write back modified files
      -n, --nobackups       Don't write backups for modified files
      -o OUTPUT_DIR, --output-dir=OUTPUT_DIR
                            Put output files in this directory instead of
                            overwriting the input files.  Requires -n.
      -W, --write-unchanged-files
                            Also write files even if no changes were required
                            (useful with --output-dir); implies -w.
      --add-suffix=ADD_SUFFIX
                            Append this string to all output filenames. Requires
                            -n if non-empty.  ex: --add-suffix='3' will generate
                            .py3 files.



```bash
futurize -h
```

    Usage: futurize [options] file|dir ...
    
    Options:
      -h, --help            show this help message and exit
      -V, --version         Report the version number of futurize
      -a, --all-imports     Add all __future__ and future imports to each module
      -1, --stage1          Modernize Python 2 code only; no compatibility with
                            Python 3 (or dependency on ``future``)
      -2, --stage2          Take modernized (stage1) code and add a dependency on
                            ``future`` to provide Py3 compatibility.
      -0, --both-stages     Apply both stages 1 and 2
      -u, --unicode-literals
                            Add ``from __future__ import unicode_literals`` to
                            implicitly convert all unadorned string literals ''
                            into unicode strings
      -f FIX, --fix=FIX     Each FIX specifies a transformation; default: all.
                            Either use '-f division -f metaclass' etc. or use the
                            fully-qualified module name: '-f
                            lib2to3.fixes.fix_types -f
                            libfuturize.fixes.fix_unicode_keep_u'
      -j PROCESSES, --processes=PROCESSES
                            Run 2to3 concurrently
      -x NOFIX, --nofix=NOFIX
                            Prevent a fixer from being run.
      -l, --list-fixes      List available transformations
      -p, --print-function  Modify the grammar so that print() is a function
      -v, --verbose         More verbose logging
      --no-diffs            Don't show diffs of the refactoring
      -w, --write           Write back modified files
      -n, --nobackups       Don't write backups for modified files.
      -o OUTPUT_DIR, --output-dir=OUTPUT_DIR
                            Put output files in this directory instead of
                            overwriting the input files.  Requires -n. For Python
                            >= 2.7 only.
      -W, --write-unchanged-files
                            Also write files even if no changes were required
                            (useful with --output-dir); implies -w.
      --add-suffix=ADD_SUFFIX
                            Append this string to all output filenames. Requires
                            -n if non-empty. For Python >= 2.7 only.ex: --add-
                            suffix='3' will generate .py3 files.


## See also
1. [Features from future](Features-from-future.md)

## Reference
1. [Automated Python 2 to 3 code translation](https://docs.python.org/2/library/2to3.html)
2. [Porting Python 2 Code to Python 3](https://docs.python.org/3/howto/pyporting.html)
3. [PEP 3105 -- Make print a function](https://www.python.org/dev/peps/pep-3105/)
