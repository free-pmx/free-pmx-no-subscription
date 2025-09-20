free-pmx: No-subscription setup tool for Proxmox suite
======================================================

Project homepage provides **comprehensive overview**:

-  https://free-pmx.org/tools/free-pmx-no-subscription/

This README is a mere addendum to the **technical description**:

-  https://free-pmx.org/insights/no-subscription/

Package contents
================

The ``free-pmx-no-subscription`` directory in the root of the working
tree holds the actual package payload. There is no compiled code. Some
files are compressed. All the information is contained *within*:

.. code:: bash

   # package details
   cat DEBIAN/control

   # copyright and licensing
   cat usr/share/doc/free-pmx-no-subscription/copyright

   # full changelog
   zcat usr/share/doc/free-pmx-no-subscription/changelog.gz

   # manual pages
   man free-pmx-no-subscription/usr/share/man/man1/no-subscription.1.gz
   man free-pmx-no-subscription/usr/share/man/man1/no-nag.1.gz

Build
=====

The package can be assembled with no build dependencies from *within*
the contents directory:

.. code:: bash

   dpkg-deb --build --root-owner-group . self-built.deb

Verifiability
-------------

Reproducible build - one that results in a binary-identical ``.deb``
file - is possible by recreating the original environment.

File permissions
~~~~~~~~~~~~~~~~

-  ensure ``umask 0022`` is set *prior* to ``git clone`` (or more
   precisely, *checkout*); or
-  *alternatively* set correct file permissions with ``source .permsrc``
   *thereafter*.

Build metadata
~~~~~~~~~~~~~~

Source ``<package>.buildmeta`` file - there is exactly one - and export
environment variables for ``dpkg-deb``:

.. code:: bash

   source *.buildmeta
   export SOURCE_DATE_EPOCH DPKG_DEB_COMPRESSOR_TYPE

Expected checksum and published package URL
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Further environment variables are available:

-  ``DEB_SHA256`` - expected ``.deb`` file checksum value; and
-  ``DEB_URL`` - URL of the published package.

Correctly reproduced build results in a matching checksum, also
identical to that of the published package.

Audit
=====

Instead of full manual audit and/or self-build of each new version,
there is an automated workflow to review:

-  https://github.com/free-pmx/free-pmx-no-subscription/actions/workflows/repro-build.yml
