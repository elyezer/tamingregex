Metacharacters
==============

* ``.`` - wildcard, matches anything
* ``^`` - matches the start of the string or the start of the line
* ``$`` - matches the end of the string or the end of the line
* ``[...]`` - matches a character class (a set of characters). The ``-`` can be
  used to specify ranges such as ``[a-z]`` which matches all the lower case
  alphabetical characters.
* ``\`` - used to escape metacharacters, strip their special meaning. For
  example: ``\\`` will match a literal ``\`` and ``\[`` will match a literal
  ``\``.
* ``\b`` - matches the empty string on a word boundary
* ``\B`` - matches the empty string when it is not on a word boundary
* ``|`` - the `or` operator, if A and B are regular expressions, ``A|B`` will
  match either A or B.

Metacharacters for repeating
----------------------------

* ``*`` - matches the previous character zero or more times
* ``+`` - matches the previous character one or more times
* ``?`` - matches once or zero times, same as making a character optional
* ``{m}`` - matches m times
* ``{m,n}`` - matches at least m times and at most n times.
* ``{,n}`` - matches at least 0 times and at most n times.
* ``{m,}`` - matches at least m times and at most infinite times.

Non-greedy Metacharacters
-------------------------

* ``*?`` - matches the previous character zero or more times
* ``+?`` - matches the previous character one or more times
* ``??`` - matches once or zero times, same as making a character optional
* ``{}?`` - matches once or zero times, same as making a character optional

Groups and Backreferences
=========================

* ``(A)`` - creates a group that will both match the regex A and capture it.
* ``\N`` - backreference N, where N is a positive integer, usually, from 1 to
  9. Each group defined in a regular expression will be assigned to a
  backreference, e.g. the following regular expression ``([a-z])\1`` will match
  any duplicated character like `aa`, `bb`, `cc`, etc. But it won't match `ab`,
  for example.
