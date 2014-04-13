pythonsucks
===========

It's a shame. But unfortunately the world loves Python.

There is no way to avoid it, it's all around me, it wants me to suffer.

*C'est pas parcequ'ils sont nombreux à avoir tort qu'ils ont raison*
                               -- Coluche


So this place will provide some anger management.

## import wtf

#### <a name="self"/> The self. plague

I know you got to have a way to access your instance variable. Could have been a little shorter, could have not smelled like Java, ... anyway.


Why do you need to give a pointer to the class instance to the constructor ????
 
    class Complex:
      def __init__(self):
                   ^^^^   DAFUCK
                   
                   
#### <a name="colon"/>The great colon illusion

Best example of the "it's for your own good" illusion. This is a screenshot from
 [python docs site](https://docs.python.org/2/faq/design.html#why-are-colons-required-for-the-if-while-def-class-statements) :

![ScreenShot](/sc/colon_lie.png)

Can you spot the lie? They tell you how colons are great for lisibility and give you an example... very biased. The one with the colon has syntax highlighting on.

#### <a name="switch"/> The shame of no switch

This is fugly, and looks like  kindergarden programming:

    if x == 'first state':
            ...
        elif x == 'second state':
            ...
        elif x == 'third state':
            ...
        elif x == 'fourth state':
            ...
        else:
            # default handling
            ...

but again, not THAT much different from a nice switch/case. What's hilarious is [the reason](http://legacy.python.org/dev/peps/pep-3103/#rejection-notice) for not adding the switch/case syntax: a quick handvote at PyCon 2007. All Hail Guido! 

#### <a name="poo"/> The object guilt

Python doesn't really want to be an object oriented language:

    len([1,2,3]) just calls .__len__()

So why not just use a single .len() method? [Guido](https://mail.python.org/pipermail/python-3000/2006-November/004643.html) says len() is "special" and those builtin operation are easier to read.

Python is still not a nice object oriented language:

    >>> int(str(len([1,2,3])))
    3
    >>> [1,2,3].__len__().__str__().__int__()
    Traceback (most recent call last):
      File "<stdin>", line 1, in <module>
      AttributeError: 'str' object has no attribute '__int__'

#### <a name="doc"/>The documentation fluster

Python's documentation is just a huge concatenation of `__doc__()` and a bunch of howtos. Try to find somewhere a description of the `ValueError` (a common Exception) object.  
It also contains treachery (see [colon](#colon)).
