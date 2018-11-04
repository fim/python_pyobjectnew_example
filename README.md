# Issue description

PyObjects initialized with PyObject_New have invalid values in uninitialized pointers that cause unexcepted behavior

# How to repro 

```
$ python setup.py build
[...]
$ pip install . 
[...]
$ python -c 'import custom; custom.Custom()'
weird pointer has value of: 0x8ec480
deallocating weird pointer
$ python
Python 3.7.1 (default, Nov  3 2018, 09:33:27) 
[GCC 5.4.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import custom, gc
>>> custom.Custom()
weird pointer has value of: 0x1
<custom2.Custom object at 0x7f1a2b8e4ed0>
>>> gc.collect()
deallocating weird pointer
zsh: segmentation fault  python
```
