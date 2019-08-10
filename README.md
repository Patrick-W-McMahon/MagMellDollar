Mag Mell Dollar Core integration/staging tree
=====================================

[![Build Status](https://travis-ci.org/magmelldollar-project/magmelldollar.svg?branch=master)](https://travis-ci.org/magmelldollar-project/magmelldollar)

https://magmelldollar.org

What is Mag Mell Dollar?
----------------

Mag Mell Dollar is an experimental digital currency that enables instant payments to
anyone, anywhere in the world. Mag Mell Dollar uses peer-to-peer technology to operate
with no central authority: managing transactions and issuing money are carried
out collectively by the network. Mag Mell Dollar Core is the name of open source
software which enables the use of this currency.

For more information, as well as an immediately useable, binary version of
the Mag Mell Dollar Core software, see [https://magmelldollar.org](https://magmelldollar.org).

License
-------

Mag Mell Dollar Core is released under the terms of the MIT license. See [COPYING](COPYING) for more
information or see https://opensource.org/licenses/MIT.

Development Process
-------------------

The `master` branch is the stable build.

The `dev` branch is the test branch is not guaranteed to be completely stable. 

Testing
-------

Testing and code review is the bottleneck for development; we get more pull
requests than we can review and test on short notice. Please be patient and help out by testing
other people's pull requests, and remember this is a security-critical project where any mistake might cost people
lots of money.

### Automated Testing

Developers are strongly encouraged to write [unit tests](/doc/unit-tests.md) for new code, and to
submit new unit tests for old code. Unit tests can be compiled and run
(assuming they weren't disabled in configure) with: `make check`

There are also [regression and integration tests](/qa) of the RPC interface, written
in Python, that are run automatically on the build server.
These tests can be run (if the [test dependencies](/qa) are installed) with: `qa/pull-tester/rpc-tests.py`

The Travis CI system makes sure that every pull request is built for Windows, Linux, and OS X, and that unit/sanity tests are run automatically.

### Manual Quality Assurance (QA) Testing

Changes should be tested by somebody other than the developer who wrote the
code. This is especially important for large or high-risk changes. It is useful
to add a test plan to the pull request description if testing the changes is
not straightforward.

Translations
------------

We only accept translation fixes that are submitted through [Magmelldollar Core's Transifex page](https://www.transifex.com/projects/p/magmelldollar/).
Translations are converted to Magmelldollar periodically.

Translations are periodically pulled from Transifex and merged into the git repository. See the
[translation process](doc/translation_process.md) for details on how this works.

**Important**: We do not accept translation changes as GitHub pull requests because the next
pull from Transifex would automatically overwrite them again.
