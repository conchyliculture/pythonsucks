pythonsucks
===========

It's a shame. But unfortunately the world loves Python.

There is no way to avoid it, it's all around me, it wants me to suffer.

*C'est pas parcequ'ils sont nombreux à avoir tort qu'ils ont raison*
                               -- Coluche


So this place will provide some anger management.

## Examples of hate

#### The self. plague

I know you got to have a way to access your instance variable. Could have been a little shorter, could have not smelled like Java, ... anyway.



Why do you need to give a pointer to the class instance to the constructor ????
 
    class Complex:
      def __init__(self):
                   ^^^^   DAFUCK
                   
                   
#### The great colon illusion

Best example of the "it's for your own good" illusion. This is a screenshot from
 [python docs site](https://docs.python.org/2/faq/design.html#why-are-colons-required-for-the-if-while-def-class-statements) :

![ScreenShot](/sc/colon_lie.png)

Can you spot the lie? They tell you how colons are great for lisibility and give you an example... very biased. The one with the colon has syntax highlighting on.

#### The shame of no switch

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

#### The object guilt

Python doesn't really want to be an object oriented language:

  len([1,2,3])  calls [1,2,3].__len__()
