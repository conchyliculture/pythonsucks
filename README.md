pythonsucks
===========

Until you can become this guy

![jake](/sc/jake_snake.jpg)


you have to do a lot of Python Wrestling.

It's a shame. But unfortunately the world loves Python.

There is no way to avoid it, it's all around me, it wants me to suffer.

So this place will provide some anger management.

> This is a list of stuff, in no particular order
> that annoy non-python zealots !

*C'est pas parcequ'ils sont nombreux à avoir tort qu'ils ont raison*
                               -- Coluche


## Python hates you

First part dedicated to python core, the stdlib comes next.


#### <a name="space"/> The space fascism

Did you ever want to program in a language where whitespaces have a meaning in the grammar? You can code in [Whitespace](http://en.wikipedia.org/wiki/Whitespace_%28programming_language%29), or in Python.

Have you ever copypasted whitespaces to ensure code will run? Welcome to Python.

A wonderful world where you can't just hack some script without being sure your text editor is the same as the one used originally for that script. Maybe because Python developpers are all old geezers used to programming with punch card.

But at least Fortran was coherent in fascism : 6th column for everyone

Want to quickly test that if `something` is  ̀False` without having to recreate your database?

    if something:
        print "Okay"
    else:
        drop_all_databases()
    
    other_stuff

.... then just don't comment the line or you'll get 

      File "lol.py", line 6
           other_stuff
                     ^
    IndentationError: expected an indented block

It also makes logic debugging horrible.

    def yourLifeIsMiserable:
      for machin in chie:
        if something:
          ....
          haha() 
          ....
        else:
          if this_is_fun:
            ....
            kill_yourself
            ...
            ...
      yield fail

Did you notice the yield line needs 2 more spaces?
 

#### <a name="self"/> The self. plague

I know you got to have a way to access your instance variable. Could have been a little shorter, could have not smelled like Java, ... anyway.


Why do you need to give a pointer to the class instance to the constructor ????
 
    class Complex:
      def __init__(self):
                   ^^^^   DAFUCK
                   
#### <a name="break"/> Breaking bad

It looks like there is no way to do a while loop, with the condition tested after the first loop, like so:

    do:
        something()
    while condition

The "python" way is ugly:

    while True:
        something()
        if condition:
            break

#### <a name="colon"/> The great colon illusion

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

Of course things get worse when you try "advanced" stuff like sorting:

    In [10]: a =[4,3,5]
    In [11]: a.sort()
    In [12]: a
    Out[12]: [3, 4, 5]

What ?! it doesn't return itself ?
So you can't write :

   a.sort().pop()
 
OK, lets try on a dict :

    In [17]: a={1: 'D', 2: 'B', 3: 'B', 4: 'E', 5: 'A'}
    In [18]: a.sort()
    VAttributeError: 'dict' object has no attribute 'sort'

... apparently you have to use the super object oriented builtin "sorted".
Let's try :

    In [19]: sorted(a)
    Out[19]: [1, 2, 3, 4, 5]

No comment.

#### <a name="join"/>The join foolishness

From what I understand from reading [this thread about string methods](https://mail.python.org/pipermail/python-dev/1999-June/095366.html) being coded into Python, the language developer decided that since Python isn't an object oriented language, it was easier (as in 'no need to re-code a join method for different collection structures') to just code the `join()` method that way :

    sep.join(iterable)

Fortunately Python doesn't make you do:

    "|".split("a|b|c|d")

#### <a name="doc"/>The documentation fluster

Python's documentation is just a huge concatenation of `__doc__()` and a bunch of howtos. Try to find a description of the object `ValueError` (a common Exception).  
It also contains treachery (see [colon](#colon)).

#### <a name="false"/>Falsehood

Do you expect a 72 bytes object to be evaluated as False ? Well Python does. Like PHP and Javascript, an empty string, or anything with a 0 length will be evaluated as False for some reason.

    if u'':
      print u'No.'
    else:
      print u'This is driving me crazy' 

False should be your language NULL and zero, basta. Like any sane language like C++ Java or Ruby.

#### <a name="unicode"/>The unicode failure

Handling weird characters is hard. All languages have their own caveats, but few of them make me as angry as python.

    $ python -c "print u'\u03ba\u03c1\u03b1\u03b6\u03b9\u03bd\u03b5\u03c3\u03c2'"
    κραζινεσς

    $ python -c "print u'\u03ba\u03c1\u03b1\u03b6\u03b9\u03bd\u03b5\u03c3\u03c2'" | head
    Traceback (most recent call last):
      File "<string>", line 1, in <module>
      UnicodeEncodeError: 'ascii' codec can't encode characters in position 0-8: ordinal not in range(128)

    $PYTHONIOENCODING="utf-8" python -c "print u'\u03ba\u03c1\u03b1\u03b6\u03b9\u03bd\u03b5\u03c3\u03c2'" | head
    κραζινεσς

#### <a name="range"/>Shooting range

    $ for i in `seq 0 10` ; do echo -n "$i " ; done
    0 1 2 3 4 5 6 7 8 9 10 
    $ ruby -e "print 0.upto(10).to_a"
    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
    $ ruby -e "(0..10).each {|i| print \"#{i} \"}"
    0 1 2 3 4 5 6 7 8 9 10 
    $ python -c "print range(0,10)"
    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

This makes sense in Python's world, where the developper is a noob and we want to squeeze him in a little cage
where he won't do off by one errors when he wants to
    
    for hate in range(len(facsism)):
        ....

#### <a name=""/> Helping hand

    class A(object):                                                                
        def __init__(self, race=None,lol=None):                                        
            pass                                                                        

    class B(A):                                                                      
        def __init__(self, race, lol=None):                                            
            super(B, self).__init__(race, lol=lol)                                      
    B(lol=None)

    TypeError: __init__() takes at least 2 arguments (2 given)

The code is buggy, yes, and Python will just be a little bitch about it.

In a more condensed and unreadable form:

    (lambda x,y='': None)(y='')

    <lambda>() takes at least 1 argument (1 given)

Python takes at least 0 fuck (0 given).

## import wtf

Extra crazyness comes with extra imports

#### <a name="re"/>The regex confusion

`import re` opens a whole new world of pain. Try to simply parse a file with it.

    endpageRE   = re.compile(r'^\s*<\/page>\s*$')
    idRE        = re.compile(r'^\s*<id>(\d+)<\/id>\s*$')
    startpageRE = re.compile(r'^\s*<page>\s*$')
    titleRE     = re.compile(r'^\s*<title>(.+)<\/title>\s*')
    revisionRE  = re.compile(r'\s*<revision>$')

    curpos = 0

    for line in inputstream:
        lol_python_is_shit = endpageRE.match(line)
        if lol_python_is_shit:
            ...
            next

        seriously_what_am_i_doing = idRE.match(line)
        if seriously_what_am_i_doing:
            ...
            next

        get_me_out_of_here = startpageRE.match(line)
        if get_me_out_of_here:
            ...
            start = curpos
            id_ = 0
            next

        this_can_t_be_happening = titleRE.match(line)
        if this_can_t_be_happening:
            ...
            title = this_can_t_be_happening.group(1)
            ...
            next

        when_will_this_craziness_end = revisionRE.match(line)
        if when_will_this_craziness_end:
            ...
            next

#### <a name="rfc3986"/> Can I haz RFC3986 validation

If you want to parse valid URI only, you're out of luck with the stdlib.

    from urlparse import urlparse
    In [2]: urlparse("£:&  :!!!!!!!! BEST ?    URL&&&&&  EV444444 @@@@@@    htt://   ")
    Out[2]: ParseResult(scheme='', netloc='', path='\xc2\xa3:&  :!!!!!!!! BEST ', params='', query='    URL&&&&&  EV444444 @@@@@@    htt://   ', fragment='')

#### <a name="pathjoin"/> os.path.join joins... sometimes

From the [doc](https://docs.python.org/2/library/os.path.html#os.path.join) :

<< If any component is an absolute path, all previous components ([...]) are thrown away, and joining continues. >>

    $ python -c "import os; print os.path.join('/tmp','/lolwrong')"
    /lolwrong

Python v3 [doc](https://docs.python.org/3/library/os.path.html#os.path.join) is even more annoying :

<< Join one or more path components intelligently. If any component is an absolute path [...] >>

OMG INTELLIGENCE:

    $ python -c "import os; print os.path.join([])"
    []
    $ python -c "import os; print os.path.join(False)"
    False
    $ python -c "import os; print os.path.join(os.path.join)"
    <function join at 0x7fe203269ed8>

And I'm not the only one being fooled by crazy methods : [arbitrary file upload vulnerability in Cuckoo Sandbox](http://cuckoosandbox.org/2014-10-07-cuckoo-sandbox-111.html) was caused by it.

By the way, people who commited that method, forgot to be pythonic (see [join()](#join)).

#### <a name="zipfail"> import zipfail

zipfile doesn't care about symlinks, and will do weird stuff with them.

    $ mkdir lol
    $ echo "lolilol" > lol/wtfpython
    $ ln -s wtfpython lol/symlink
    $ ls -l lol
    total 4
    lrwxrwxrwx symlink -> wtfpython
    -rw-r----- wtfpython

    $ python -m zipfile -c noob.zip lol
    $ python -m zipfile -e noob.zip noob
    $ ls -l noob/lol/
    total 8
    -rw-r----- symlink
    -rw-r----- wtfpython

    $ zip -r noob.zip lol
    adding: lol/ (stored 0%)
    adding: lol/wtfpython (stored 0%)
    adding: lol/symlink (stored 0%)
    $ python -m zipfile -e noob.zip noob
    Traceback (most recent call last):
      File "/usr/lib/python2.7/runpy.py", line 162, in _run_module_as_main
        "__main__", fname, loader, pkg_name)
      File "/usr/lib/python2.7/runpy.py", line 72, in _run_code
        exec code in run_globals
      File "/usr/lib/python2.7/zipfile.py", line 1527, in <module>
        main()
      File "/usr/lib/python2.7/zipfile.py", line 1505, in main
        with open(tgt, 'wb') as fp:
    IOError: [Errno 21] Is a directory: 'noob/lol/'
