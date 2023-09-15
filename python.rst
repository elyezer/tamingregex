Character sequences
===================

* ``\d`` - Matches any decimal digit; this is equivalent to the class [0-9].
* ``\D`` - Matches any non-digit character; this is equivalent to the class
  [^0-9].
* ``\s`` - Matches any whitespace character; this is equivalent to the class [
  \t\n\r\f\v].
* ``\S`` - Matches any non-whitespace character; this is equivalent to the
  class [^ \t\n\r\f\v].
* ``\w`` - Matches any alphanumeric character; this is equivalent to the class
  [a-zA-Z0-9_].
* ``\W`` - Matches any non-alphanumeric character; this is equivalent to the
  class [^a-zA-Z0-9_].

These sequences can be included inside a character class. For example, [\s,.]
is a character class that will match any whitespace character, or ',' or '.'.

Using Raw Strings
=================

Python strings accept the ``\`` slash as the escape character so to insert a
single ``\`` for a regex ``\\`` needs to be used, to avoid having a lot of back
slashes Python provides the raw string where ``\`` will be literal and you can
think that is now the regex escape character, not the string.

r'\\'

Non-capturing and Named Groups
==============================

* ``(?...)`` - The extension notation (a '?' following a '(' is not meaningful
  otherwise). The first character after the '?' determines what the meaning and
  further syntax of the construct is. Extensions usually do not create a new
  group; (?P<name>...) is the only exception to this rule.
* ``(?:...)`` - Create a non-capturing group, useful to help denote a part of a
  regular expression.
* ``(?P<name>...)`` - Create a group named `name` which will match the regex
  represented by ``...``.
* ``(?P=name)`` - Denotes a backreference to a named group; it matches whatever
  text was matched by the earlier group named name.

Lookahead Assertions
====================

* ``(?=...)`` -  Positive lookahead assertion. This succeeds if the contained
  regular expression, represented here by ``...``, successfully matches at the
  current location, and fails otherwise. But, once the contained expression has
  been tried, the matching engine doesn’t advance at all; the rest of the
  pattern is tried right where the assertion started.
* ``(?!...)`` -  Negative lookahead assertion. This is the opposite of the
  positive assertion; it succeeds if the contained expression doesn’t match at
  the current position in the string.


References
==========

* https://docs.python.org/3.6/howto/regex.html
* https://docs.python.org/3.6/library/re.html
