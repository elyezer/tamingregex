Patterns
========

Normal pattern language
-----------------------

* ``*``: Matches any string, including the null string (empty string)
* ``?``: Matches any single character
* ``X``: Matches the character X which can be any character that has no special
  meaning
* ``\X``: Matches the character X, where the character's special meaning is
  stripped by the backslash
* ``\\``: Matches a backslash
* ``[…]``: Defines a pattern bracket expression. Matches any of the enclosed
  characters at this position.

Bracket expressions
-------------------

* ``[XYZ]``: The "normal" bracket expression, matching either X, Y or Z
* ``[X-Z]``: A range expression: Matching all the characters from X to Y (your
  current locale, defines how the characters are sorted!)
* ``[[:class:]]``: Matches all the characters defined by a POSIX character
  class.
* ``[^…]``: A negating expression: It matches all the characters that are not
  in the bracket expression
* ``[!…]``: Equivalent to [^…]
* ``[]...]`` or ``[-…]``: Used to include the characters ``]`` and ``-`` into
  the set, they need to be the first characters after the opening bracket

POSIX character classes
-----------------------

+------------+----------------------------------------------------+--------------------------+
| POSIX      | Description                                        | ASCII                    |
+============+====================================================+==========================+
| [:alnum:]  | Alphanumeric characters                            | ``[a-zA-Z0-9]``          |
+------------+----------------------------------------------------+--------------------------+
| [:alpha:]  | Alphabetic characters                              | ``[a-zA-Z]``             |
+------------+----------------------------------------------------+--------------------------+
| [:ascii:]  | ASCII characters                                   | ``[\x00-\x7F]``          |
+------------+----------------------------------------------------+--------------------------+
| [:blank:]  | Space and tab                                      | ``[ \t]``                |
+------------+----------------------------------------------------+--------------------------+
| [:cntrl:]  | Control characters                                 | ``[\x00-\x1F\x7F]``      |
+------------+----------------------------------------------------+--------------------------+
| [:digit:]  | Digits                                             | ``[0-9]``                |
+------------+----------------------------------------------------+--------------------------+
| [:graph:]  | Visible characters                                 | ``[\x21-\x7E]``          |
|            | (anything except spaces and control characters)    |                          |
+------------+----------------------------------------------------+--------------------------+
| [:lower:]  | Lowercase letters                                  | ``[a-z]``                |
+------------+----------------------------------------------------+--------------------------+
| [:print:]  | Visible characters and spaces                      | ``[\x20-\x7E]``          |
|            | (anything except control characters)               |                          |
+------------+----------------------------------------------------+--------------------------+
| [:punct:]  | Punctuation and symbols.                           | ``[!"\#$%&'()*+,\-./:;   |
|            |                                                    | <=>?@\[\\\]^_`{|}~]``    |
+------------+----------------------------------------------------+--------------------------+
| [:space:]  | All whitespace characters, including line breaks   | ``[ \t\r\n\v\f]``        |
+------------+----------------------------------------------------+--------------------------+
| [:upper:]  | Uppercase letters                                  | ``[a-z]``                |
+------------+----------------------------------------------------+--------------------------+
| [:word:]   | Word characters (letters, numbers and underscores) | ``[A-Za-z0-9_]``         |
+------------+----------------------------------------------------+--------------------------+
| [:xdigit:] | Hexadecimal digits                                 | ``[A-Fa-f0-9]``          |
+------------+----------------------------------------------------+--------------------------+

Pathname Expansion (Globbing)
=============================

Use one of the following glob characters to match paths:

* \* - means 'match any number of characters'. ``/`` is not matched (and
  depending on your settings, things like ``.`` may or may not be matched
* ? - means 'match any single character'
* [abc] - match any of the characters listed. This syntax also supports ranges,
  like [0-9]. A bracket expression can be used.

Parameter Expansion
===================

Substring Removal
-----------------

* ``${PARAMETER#PATTERN}``: non-greedy match from the beginning of the
  parameter
* ``${PARAMETER##PATTERN}``: greedy match from the beginning of the parameter
* ``${PARAMETER%PATTERN}``: non-greedy match from the end of the parameter
* ``${PARAMETER%%PATTERN}``: greedy match from the end of the parameter

Examples::

    $ PARAMETER="words with spaces for the substring removal"

    $ echo ${PARAMETER#* }
    with spaces for the substring removal

    $ echo ${PARAMETER##* }
    removal

    $ echo ${PARAMETER% *}
    words with spaces for the substring

    $ echo ${PARAMETER%% *}
    words

Search and Replace
------------------

* ``${PARAMETER/PATTERN/STRING}``: replace the first occurrence of PATTERN with
  STRING.
* ``${PARAMETER//PATTERN/STRING}``: replace all occurrences of PATTERN with
  STRING
* ``${PARAMETER/PATTERN}``: remove the first occurrence of pattern, same as
  ``${PARAMETER/PATTERN/}``
* ``${PARAMETER//PATTERN}``: remove all occurrences of pattern, same as
  ``${PARAMETER//PATTERN/}``

.. note:: Prefixing the PATTERN with ``#`` or ``%`` force the match to happen
    against the beginning or the end of the PARAMETER respectively

Examples::

    $ PARAMETER="the toy is in the box"

    $ echo ${PARAMETER/the/a}
    a toy is in the box

    $ echo ${PARAMETER//the/a}
    a toy is in a box

    $ echo ${PARAMETER/the}
    toy is in the box

    $ echo ${PARAMETER//the}
    toy is in box

    $ echo ${PARAMETER/the/}
    toy is in the box

    $ echo ${PARAMETER//the/}
    toy is in box

    $ PARAMETER="xxx"

    $ echo ${PARAMETER/#x/a}
    axx

    $ echo ${PARAMETER/%x/a}
    xxa

Conditional Expressions
=======================

* ``<STRING> == <PATTERN>``: <STRING> is checked against the pattern <PATTERN>.
  TRUE on a match. **Note**: quoting the pattern forces a literal comparison.
* ``<STRING> = <PATTERN>``: equivalent to the == operator
* ``<STRING> != <PATTERN>``: <STRING> is checked against the pattern <PATTERN>.
  TRUE on no match
* ``<STRING> =~ <ERE>``: <STRING> is checked against the extended regular
  expression <ERE>. TRUE on a match

Examples::

    $ [[ "abc" =~ [[:alpha:]]+ ]] # true
    $ [[ "123" =~ [[:alpha:]]+ ]] # false
    $ [[ "abc" = [[:alpha:]]+ ]] # false, not an extended regex
    $ [[ "abc" = [[:alpha:]]\+ ]] # false, not a pattern
    $ [[ "abc" = [[:alpha:]]?? ]] # true
    $ [[ "abc" = [[:alpha:]]* ]] # true
    $ [[ "abc" = [a-c]* ]] # true

Basic vs Extended Regular expressions
-------------------------------------

In basic regular expressions the metacharacters ``?``, ``+``, ``{``, ``|``,
``(``, and ``)`` lose their special meaning; instead use the backslashed
versions ``\?``, ``\+``, ``\{``, ``\|``, ``\(``, and ``\)``.

References
==========

* http://wiki.bash-hackers.org/syntax/pattern
* http://tldp.org/LDP/Bash-Beginners-Guide/html/chap_04.html
