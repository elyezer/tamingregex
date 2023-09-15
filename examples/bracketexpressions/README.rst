Setup::

    $ touch {1..2} {a..b} {a..b}{{1..2},{a..b}}

Examples::

    $ ls [[:alpha:]]
    a  b

    $ ls [[:digit:]]
    1  2

    $ ls [[:alpha:]][[:digit:]]
    a1  a2  b1  b2

    $ ls [[:alpha:]][[:alpha:]]
    aa  ab  ba  bb

    $ ls [[:alpha:]]*
    a  a1  a2  aa  ab  b  b1  b2  ba  bb

    $ ls [[:alpha:]]?
    a1  a2  aa  ab  b1  b2  ba  bb
