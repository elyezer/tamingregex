Examples::

    # Basic regular expression
    $ grep -c '^[[:upper:]]' /usr/share/dict/words
    80011

    $ grep -c '^[[:upper:]]+' /usr/share/dict/words
    0

    $ grep -c '^[[:upper:]]\+' /usr/share/dict/words
    80011

    # Extended regular expression
    $ grep -cE '^[[:upper:]]+' /usr/share/dict/words
    80011

    $ grep -cE '^[[:upper:]]\+' /usr/share/dict/words
    0
