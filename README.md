Python bcrypt
============

This repository is a clone of the [Google Code project](http://code.google.com/p/py-bcrypt/), which has not been updated in more than a year.

Most significantly, this clone applies a number of patches which allows compilation on Windows
and improves a number of small details in the original implementation, as supplied by the community. The original authors whose patches are included in this author are:

This project has been tested using msvc9, and should be compiled with the same C compiler as the python installation you are using (typically, msvc9)
If you are having issues compiling on Windows using VC++, fix the msvc9compiler python defaults, and tweak your environment using this [guide](http://blog.victorjabur.com/2011/06/05/compiling-python-2-7-modules-on-windows-32-and-64-using-msvc-2008-express/)

benghattem@gmail.com
Providing the basis for this patch, fixing compilation flags and ifdefs [patch](http://code.google.com/p/py-bcrypt/issues/attachmentText?id=1&aid=10003000&name=py-bcrypt_11.patch&token=EFCIp9qVR4pi3SaJ7kDaVmy3OQc%3A1346047268712)

florian.ruechel@gmail.com 
Extending the patch and fixing memset + bzero issues to make the code more standards compliant [patch](http://code.google.com/p/py-bcrypt/issues/attachmentText?id=1&aid=10008000&name=py-bcrypt.patch&token=esLPoSRqwBo90FHQ2B_NOyZbtas%3A1346047268714)

Original README
------------

__py-bcrypt__ is an implementation the OpenBSD Blowfish password hashing
algorithm, as described in "A Future-Adaptable Password Scheme" by Niels
Provos and David Mazieres: http://www.openbsd.org/papers/bcrypt-paper.ps

This system hashes passwords using a version of Bruce Schneier's
Blowfish block cipher with modifications designed to raise the cost of
off-line password cracking. The computation cost of the algorithm is
parametised, so it can be increased as computers get faster.

py-bcrypt requires Python 2.4. Older versions may work, but the
bcrypt.gensalt() method won't - it requires the cryptographic random
number generator os.urandom() introduced in 2.4.

To install, use the standard Python distutils incantation:

	$ python setup.py build
	$ python setup.py install

Regression tests are in the test/test.py file. This is deliberately in
a subdirectory so it does not mistakenly pick up the top-level bcrypt/
directory.

py-bcrypt is licensed under a ISC/BSD licence. The underlying Blowfish
and password hashing code is taken from OpenBSD's libc. See the LICENSE
file for details.

Please report bugs to Damien Miller <djm@mindrot.org>. Please check the
TODO file first, in case your problem is something I already know about
(please send patches!)

A simple example that demonstrates most of the features:
```
	import bcrypt

	# Hash a password for the first time
	hashed = bcrypt.hashpw(password, bcrypt.gensalt())

	# gensalt's log_rounds parameter determines the complexity
	# the work factor is 2**log_rounds, and the default is 12
	hashed = bcrypt.hashpw(password, bcrypt.gensalt(10))

	# Check that an unencrypted password matches one that has
	# previously been hashed
	if bcrypt.hashpw(plaintext, hashed) == hashed:
		print "It matches"
	else:
		print "It does not match"
```

