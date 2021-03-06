==============================================================
Reference codebase for Universal-ctags
==============================================================

This is the reference codebase for measuring the performance of
Universal-ctags parsers.


How to run ctags for the code base
==============================================================

We assume you may have enough storage space on your PC.

1. Get the input code for a parser for the language you are
   interested in with following command line:

   .. code-block:: console

	$ ./codebase clone <LANGUAGE>


   The following command lists available languages:


   .. code-block:: console

	$ ./codebase list-languages
	#           LANGUAGE	CODE
			   C	linux
			 C++	qtbase rocksdb
			  Go	buildah kubernetes
			HTML	cockpit
		  JavaScript	cockpit
		    LdScript	linux
		  ObjectiveC	gnustep-libs-base

   An example preapting C source code:
   .. code-block:: console

	$ ./codebae clone C
	...

2. Run Universal-ctags for the cloned code with following command line:

   .. code-block:: console

	$ [CTAGS_EXE=${where your ctags executable is}] ./codebase ctags <LANGUAGE> [<PROFILE>]

   codebase refers *CTAGS_EXE* environment variable to run ctags.

   You can run ctags with different option combination.
   We call such option combination *PROFILE*.
   The following command is for listing pre defined profiles:

   .. code-block:: console

	$ ./codebase list-profiles

		PROFILE		DESCRIPTION
		maximum0	Enables all extras, fields, and kinds
		minimum0	Disables all fields and extras.


   Results are displayed to your terminal. Tee'ed output goes
   to a file under results/ directory.

   An example command line for running C parser:

   .. code-block:: console

	$ cd /home/yamato/hacking/ctags-github; ./autogen.sh; ./configure; make
	$ cd /home/yamato/hacking/codebase
	$ CTAGS_EXE=/home/yamato/hacking/ctags-github/ctags ./codebase ctags C
	version: 2c46f6d4
	features: +wildcards +regex +iconv +option-directory +xpath +json +interactive +sandbox +yaml +aspell +packcc
	log: results/2c46f6d4,C...................,..........,time......,default...,2019-03-18-12:47:20.log
	tagsoutput: /dev/null
	cmdline: + /home/yamato/var/ctags-github/ctags --quiet --options=NONE --sort=no --options=profile.d/maps --totals=yes --languages=C -o - -R code/linux code/php-src code/ruby
	27886 files, 19784832 lines (555082 kB) scanned in 15.1 seconds (36686 kB/s)
	1158391 tags added to tag file

	real	0m15.172s
	user	0m14.735s
	sys	0m0.399s
	+ set +x

   In the above output, "36686 kB/s" represents the speed of parsing of C parser.
   "1158391 tags" represents the number of tags captured by C parser.


How to add your code to code base
==============================================================

You have to write a .lcopy file and put it to lcopy.d directory.
See lcopy.d/linux.lcopy as an example.


How to add your profile to preset list
==============================================================

You have to write a .ctags file and put it to profile.d directory.
A line started from "# @" is used as a description for the profile.
You may wan to use `--options-maybe` to extend profile without
modifying existing .ctags files.


Let's optimize ourt parsers!
Masatake YAMATO <yamato@redhat.com>
