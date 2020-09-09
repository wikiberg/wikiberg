# Features from future

Why do Python release some new features in __future__ (\_\_future\_\_)?

Why do we have to use import to enable them? 

The reason is that some features are not backward compatible. Python made decision to change something in the language but cannot release it immediately, otherwise it will break a lot of programs in production.

When Python introduce a new feature from \_\_future\_\_, to apply it, either we can upgrade python immediately, or import it from \_\_future\_\_. In both cases, we need to change our programs accordingly because of compatibilty. 

The benifit of the latter is that we do not need to upgrade python, and it will still work when we finally decide to upgrade in the future. Or we can say the program is forward compatible - compatible with future versions. For example, it can support both Python 2 and Python 3, this is critical for libraires.

In a word, some features of Python are not backward compatible, but we can make our program forward compatible with the help of \_\_future\_\_.

## Code


```python
import __future__
```


```python
type(__future__)
```




    module




```python
print(__future__.__file__)
```

    /opt/conda/lib/python3.8/__future__.py



```python
# We can enable new features from future by simply importing them.

for feature_name in __future__.all_feature_names:
    print(f'from __future__ import {feature_name}')

```

    from __future__ import nested_scopes
    from __future__ import generators
    from __future__ import division
    from __future__ import absolute_import
    from __future__ import with_statement
    from __future__ import print_function
    from __future__ import unicode_literals
    from __future__ import barry_as_FLUFL
    from __future__ import generator_stop
    from __future__ import annotations



```python
import sys

# Not all are new features in your current release
for feature_name in __future__.all_feature_names:
    feature = getattr(__future__, feature_name)
    if feature.getMandatoryRelease() > sys.version_info:
        print(f'Since {feature.getOptionalRelease()}, you can enable the new feature {feature_name},')
        print(f'\t which will not be madatory until {feature.getMandatoryRelease()}\n')
```

    Since (3, 1, 0, 'alpha', 2), you can enable the new feature barry_as_FLUFL,
    	 which will not be madatory until (4, 0, 0, 'alpha', 0)
    
    Since (3, 7, 0, 'beta', 1), you can enable the new feature annotations,
    	 which will not be madatory until (4, 0, 0, 'alpha', 0)
    



```python
help(__future__)
```

    Help on module __future__:
    
    NAME
        __future__ - Record of phased-in incompatible language changes.
    
    MODULE REFERENCE
        https://docs.python.org/3.8/library/__future__
        
        The following documentation is automatically generated from the Python
        source files.  It may be incomplete, incorrect or include features that
        are considered implementation detail and may vary between Python
        implementations.  When in doubt, consult the module reference at the
        location listed above.
    
    DESCRIPTION
        Each line is of the form:
        
            FeatureName = "_Feature(" OptionalRelease "," MandatoryRelease ","
                                      CompilerFlag ")"
        
        where, normally, OptionalRelease < MandatoryRelease, and both are 5-tuples
        of the same form as sys.version_info:
        
            (PY_MAJOR_VERSION, # the 2 in 2.1.0a3; an int
             PY_MINOR_VERSION, # the 1; an int
             PY_MICRO_VERSION, # the 0; an int
             PY_RELEASE_LEVEL, # "alpha", "beta", "candidate" or "final"; string
             PY_RELEASE_SERIAL # the 3; an int
            )
        
        OptionalRelease records the first release in which
        
            from __future__ import FeatureName
        
        was accepted.
        
        In the case of MandatoryReleases that have not yet occurred,
        MandatoryRelease predicts the release in which the feature will become part
        of the language.
        
        Else MandatoryRelease records when the feature became part of the language;
        in releases at or after that, modules no longer need
        
            from __future__ import FeatureName
        
        to use the feature in question, but may continue to use such imports.
        
        MandatoryRelease may also be None, meaning that a planned feature got
        dropped.
        
        Instances of class _Feature have two corresponding methods,
        .getOptionalRelease() and .getMandatoryRelease().
        
        CompilerFlag is the (bitfield) flag that should be passed in the fourth
        argument to the builtin function compile() to enable the feature in
        dynamically compiled code.  This flag is stored in the .compiler_flag
        attribute on _Future instances.  These values must match the appropriate
        #defines of CO_xxx flags in Include/compile.h.
        
        No feature line is ever to be deleted from this file.
    
    DATA
        __all__ = ['all_feature_names', 'nested_scopes', 'generators', 'divisi...
        absolute_import = _Feature((2, 5, 0, 'alpha', 1), (3, 0, 0, 'alpha', 0...
        all_feature_names = ['nested_scopes', 'generators', 'division', 'absol...
        annotations = _Feature((3, 7, 0, 'beta', 1), (4, 0, 0, 'alpha', 0), 16...
        barry_as_FLUFL = _Feature((3, 1, 0, 'alpha', 2), (4, 0, 0, 'alpha', 0)...
        division = _Feature((2, 2, 0, 'alpha', 2), (3, 0, 0, 'alpha', 0), 1310...
        generator_stop = _Feature((3, 5, 0, 'beta', 1), (3, 7, 0, 'alpha', 0),...
        generators = _Feature((2, 2, 0, 'alpha', 1), (2, 3, 0, 'final', 0), 0)
        nested_scopes = _Feature((2, 1, 0, 'beta', 1), (2, 2, 0, 'alpha', 0), ...
        print_function = _Feature((2, 6, 0, 'alpha', 2), (3, 0, 0, 'alpha', 0)...
        unicode_literals = _Feature((2, 6, 0, 'alpha', 2), (3, 0, 0, 'alpha', ...
        with_statement = _Feature((2, 5, 0, 'alpha', 1), (2, 6, 0, 'alpha', 0)...
    
    FILE
        /opt/conda/lib/python3.8/__future__.py
    
    


## See also
1. [print in python3](Python3-print.md)

## Reference
1. [Automated Python 2 to 3 code translation](https://docs.python.org/2/library/2to3.html)
2. [Porting Python 2 Code to Python 3](https://docs.python.org/3/howto/pyporting.html)
