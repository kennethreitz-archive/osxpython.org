Properly Installing Python 
==========================

*Or, "Installing Python 2.7 via Homebrew".*

One of the reasons everybody loves Python is the interactive shell.  It
basically allows you to execute Python commands in real time and
immediately get results back.  Flask itself does not come with an
interactive shell, because it does not require any specific setup upfront,
just import your application and start playing around.




Package Manager
---------------

While Snow Leopard comes with a large number of UNIX utilities, those 
familiar with Linux systems will notice one key component missing: a 
package manager. Mxcl's *Homebrew* is the answer.

To install Homebrew, simply run: ::

    $ ruby -e "$(curl -fsS http://gist.github.com/raw/323731/install_homebrew.rb)"


It's basic commands are **update**, **install**, and **remove**. 

.. man brew



Python Interpreter
------------------

And we can now install Python 2.7: ::

    $ sudo brew install python --framework


The ``--framework`` option tells Homebrew to compile Python in Framework 
mode. The outdated version of Python that Snow Leopard comes packaged with 
is built as a Framework, so this helps avoid some future module installation 
bugs. 


Distribute & Pip
----------------

*Distribute* is a fantastic drop-in replacement for *easy_install* and 
*setuptools*. It allows you to install and manage python packages from 
pypi.python.org, amongst a few other sources. It also plays well with 
*virtualenv* and user-enviornments.

To install *Distribute* and it's *easy_install* run the following commands: ::

    $ curl -O http://python-distribute.org/distribute_setup.py
    $ python distribute_setup.py

**easy_install** is considered by many to be a deprecated system, so we will 
install it's replacement: **pip**. Pip allows for uninstallation of packages, 
and is actively maintained, unlike setuptool's easy_install.

To install ``pip``: ::

    $ easy_install pip

Hopefully you'll never have to use **easy_install** again.


.. Firing Before/After Request
.. ---------------------------
.. 
.. By just creating a request context, you still don't have run the code that
.. is normally run before a request.  This probably results in your database
.. being unavailable, the current user not being stored on the
.. :data:`~flask.g` object etc.
.. 
.. This however can easily be done yourself.  Just call
.. :meth:`~flask.Flask.preprocess_request`:
.. 
.. >>> ctx = app.test_request_context()
.. >>> ctx.push()
.. >>> app.preprocess_request()
.. 
.. Keep in mind that the :meth:`~flask.Flask.preprocess_request` function
.. might return a response object, in that case just ignore it.
.. 
.. To shutdown a request, you need to trick a bit before the after request
.. functions (triggered by :meth:`~flask.Flask.process_response`) operate on
.. a response object:
.. 
.. >>> app.process_response(app.response_class())
.. <Response 0 bytes [200 OK]>
.. >>> ctx.pop()


Further Improving the Shell Experience
--------------------------------------

If you like the idea of experimenting in a shell, create yourself a module
with stuff you want to star import into your interactive session.  There
you could also define some more helper methods for common things such as
initializing the database, dropping tables etc.

Just put them into a module (like `shelltools` and import from there):

>>> from shelltools import *
