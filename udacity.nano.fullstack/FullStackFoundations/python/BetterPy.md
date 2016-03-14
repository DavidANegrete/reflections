# Writin' Better Python

## Writting Conventions
Writting code that follows the rules blends the code better with others code and
makes it easier to spot errors.

PEP - Python Enhancement Proposal there are hundreds of PEPs

PEP8
	these are the readability rules help with Python readability. 

	import this
		The Zen of Python, by Tim Peters

		Beautiful is better than ugly.
		Explicit is better than implicit.
		Simple is better than complex.
		Complex is better than complicated.
		Flat is better than nested.
		Sparse is better than dense.
		Readability counts.
		Special cases aren't special enough to break the rules.
		Although practicality beats purity.
		Errors should never pass silently.
		Unless explicitly silenced.
		In the face of ambiguity, refuse the temptation to guess.
		There should be one-- and preferably only one --obvious way to do it.
		Although that way may not be obvious at first unless you're Dutch.
		Now is better than never.
		Although never is often better than *right* now.
		If the implementation is hard to explain, it's a bad idea.
		If the implementation is easy to explain, it may be a good idea.
		Namespaces are one honking great idea -- let's do more of those!

## Doc strings
Allows functions and classes provide there own help text

To create them you can use tripple quotes ''' or """
PEP27 sets the rules for creating them.


## Using PDB (Python Debugger)
The debugger is a way of seeing what the code is doing and a given point

To use it it must first be imported or a semicolon can be used where you want to debug
	
	# add this line where you want to start the checking
	import pdb; pdb.set_trace() 

