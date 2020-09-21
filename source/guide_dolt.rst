.. highlight:: console

.. author:: Michi <https://github.com/michi-zuri>

.. tag:: lang-go
.. tag:: database
.. tag:: version-control
.. tag:: collaboration

.. sidebar:: Logo

  .. image:: _static/images/dolt.png
      :align: center

##########
Dolt
##########

.. tag_list::

Dolt_ and DoltHub_ let users collaborate on datasets in the same way that people
collaborate on source code and other text files using Git and GitHub.
Dolt_ is a version control tracker for tabled datasets, following the concepts
of Git, combined with the functionality of a MySQL-compatible database server.
DoltHub_ provides collaboration and discovery tools for these datasets to
enable users to easily collaborate across the globe. Since 18 September 2020 it
is possible to `fork any public dataset on DoltHub`_, similar to how one would
fork code repositories on GitHub.

In contrast to Git, Dolt doesn't just track changes to whole lines or rows,
but can track the history of cells in tables, as well as the corresponding
database schemas and views, while allowing fine-grained access to the data
through the powerful SQL query language.

.. note:: In case you are wondering, why would anyone name their software *Git*
  or *Dolt* (both are terms to describe foolish persons in different ways):
  `Linus Torvalds on the naming of Git`_. Mercurial, another version control
  tool developed for the Linux kernel, has a similar background_.
  Dolt seems to be following some kind of tradition here...

----

.. hint:: For this guide you should be familiar with the basic concepts of
  :manual:`supervisord <daemons-supervisord>` and
  :manual:`MySQL <database-mysql>`.

License
=======

Dolt is distributed under the `Apache License, Version 2.0`_.


Installation
============

We will unpack the pre-compiled binaries into ~/go/bin, which should already be
in your PATH, by default:

.. code-block:: console

  [isabell@stardust ~]$ mkdir -p ~/go/bin && cd ~/go/bin
  [isabell@stardust ~]$ curl -L https://github.com/liquidata-inc/\
  dolt/releases/latest/download/dolt-linux-amd64.tar.gz | tar -xzf -
    % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                   Dload  Upload   Total   Spent    Left  Speed
  100   153  100   153    0     0    294      0 --:--:-- --:--:-- --:--:--   294
  100   649  100   649    0     0   1231      0 --:--:-- --:--:-- --:--:--  1231
  100 25.5M  100 25.5M    0     0  8231k      0  0:00:03  0:00:03 --:--:-- 10.0M
  [isabell@stardust ~]$ mv dolt-linux-amd64/bin/* . && ls
  dolt  dolt-linux-amd64  git-dolt  git-dolt-smudge
  [isabell@stardust ~]$ mv dolt-linux-amd64/LICENSES ..
  [isabell@stardust ~]$ rm -r dolt-linux-amd64/
  [isabell@stardust ~]$ dolt version
  dolt version 0.19.2
  [isabell@stardust ~]$


Configuration
=============

Just like in Git, you should set an email address and username that will be
written in your commits, but note that signing commits with gpg is not
implemented yet, so you should know that `this can easily be spoofed`_.

.. code-block:: console

 [isabell@stardust ~]$ dolt config --global --add user.email isabell@uber.space
 [isabell@stardust ~]$ dolt config --global --add user.name "isabell"
 [isabell@stardust ~]$

It is possible to use Dolt without DoltHub, so the following step is optional.
Dolt will generate a JWT_ in `~/.dolt/creds/` for authenticated access of
resources on DoltHub and link it to your existing DoltHub account. The tokens
are read-only. You need to keep them safe, just like you would guard your ssh
keys.

* Login to or join DoltHub in your regular web browser then:

.. code-block:: console

 [isabell@stardust ~]$ dolt login
 Credentials created successfully.
 pub key: 0123456789abcdef0123456789abcdef0123456789abcdef0123
 /home/isabell/.dolt/creds/fedcba987fedcba987fedcba987fedcba987fedcba987.jwk
 Opening a browser to:
	https://dolthub.com/settings/credentials#0123456789abcdef0123456789abcdef0123456789abcdef0123
 Please associate your key with your account.
 Checking remote server looking for key association.
 requesting update . . .

 Key successfully associated with user: isabellondolthub email isabell@example.email
 [isabell@stardust ~]$

In other words: to successfully associate your JWT with your DoltHub_ account,
you need to go to https://dolthub.com/settings/credentials and save your public
key with a descriptive title (I would suggest something like isabell@uberspace).

Usage
=============
WIP...

.. _Dolt: https://github.com/liquidata-inc/dolt#dolt
.. _DoltHub: https://www.dolthub.com/
.. _`Apache License, Version 2.0`: https://www.apache.org/licenses/LICENSE-2.0.html
.. _`fork any public dataset on DoltHub`: https://www.dolthub.com/blog/2020-09-18-introducing-forks/
.. _`Linus Torvalds on the naming of Git`: https://en.wikipedia.org/wiki/Git#Naming
.. _story: https://en.wikipedia.org/wiki/Mercurial#History
.. _`this can easily be spoofed`: https://medium.com/@pjbgf/spoofing-git-commits-7bef357d72f0
.. _JWT: https://jwt.io/#debugger-io

----

Tested with Dolt 0.19.2, Uberspace 7.7.7.0

.. author_list::
