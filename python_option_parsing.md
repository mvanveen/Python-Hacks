----
title:  Option Parsing In Python
format: post
-----

Adding Options
==============

Initialization
--------------

    >>> from optparse import OptionParser
    >>> parser = OptionParser()

Setting A Destination
---------------------
You can specify which key the option will write to with the dest argument.
For example, the following will send results to the 'destination' key.

    >>> parser.add_option('--dest', dest='destination')

When you look at the results of parse_args

Specifying Argument Type
------------------------
The `type` argument can be set to `'complex'`, `'choice'`,`'float'`, `'int'`, `'long'`, or `'string''.  The `optparse` module will perform type checking on all types except `string`, which is left alone.  It will also perform automatic type conversion.  Please consult the [documentation](http://docs.python.org/library/optparse.html#optparse-standard-option-types) for more information.

    >>> parser.add_option('--integer-option', type='int')

Handling Standalone Arguments
-----------------------------
Sometimes you need an option which doesn't take any parameters.  You can add such an option to your option parser like so:

    >>> parser.add_option('--boolean', default=False, action='store_true')

This will set the default parsed option to False, and will set the option to True when it is invoked on the command line.

Variadic Arguments
------------------
 the `nargs` option allows you to specify the number of arguments to include when inputting a particular option.

    >>> parser.add_option('--twoargs', nargs=2)

Grabbing Input 
--------------
Run the following line to grab the output from your parsed options:

    >>> (options, args) = parser.parse_args()

`options.dest` will be the destination setting you made for a given option by supplying a `dest` parameter to the `add_option` method.

_e.g._

* When you add an option with:

    >>> parser.add_option('--some_opt', dest='dest_parameter')

* ...and grab the parsed output by running:

    >>> (options, args) = parser.parse_args()

`options.dest_parameter` will contain your parsed parameter.


Help Output
===========

Printing Help
-------------
The `optparse` module will automattically generate help output for you.  You can add help messages to options by specifying a help argument:

    >>> parser.add_option('--help-option' help='this is some help text')

Running your script with the `-h` or `--help` options will display help.  Additionally, you can call any OptionParser object's `print_help` method to print help output.

    >>> parser.print_help()
    >>> Usage: run_tests.py [options]
    >>> Options:
    >>> -h, --help            show this help message and exit

Setting Usage
-------------
You can optionally set the usage string of the help output generated.  The usage string will be show up at the top of any of help output that gets printed.

    >>> parser.set_usage('Usage: some_script.py [options] [args]')
