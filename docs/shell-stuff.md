# Shell Stuff

A collection of notes taken while trying to make sense of
the various `setup-*` scripts that come with Alpine Linux.

## Encountered Constructs

* `:` - alias for true(?), sometimes used for side-effects

    : ${LIBDIR=$PREFIX/lib}   # shell expansion and redir still happen(?)

  dropping : will lead to execution of whatever $PREFIX/lib
  turns out to be?

  the point here seems to be to set LIBDIR if LIBDIR does not
  "exist" already.  it could "exist" if it was specified
  earlier (or say it was specified on the command line and
  the construct was in a script)

* `-t` - true if argument is open and refers to a terminal

    if [ -t 1 ]; then ...

* `-n` - true if length of string is non-zero

   (finding in man page of bash was laborious too many hits for '-n')

* `-z` - true if length of string is zero

    if [ -z "$name" ] && [ $# -eq 1 ]; then

   (finding in man page of bash was laborious too many hits for '-n')

* `-eq` - arithmetic comparison

    if [ -z "$name" ] && [ $# -eq 1 ]; then

* `-a` - true if file exists (how is this different from `-e`?)

    [ -n "$DEVDOPTS" -a "$DEVDOPTS" != mdev ]
    
* `${PARAMETER%%PATTERN}`

  removing longest matching but match pattern from end of string

  https://bash-hackers.gabe565.com/syntax/pe/#from-the-end

    variant=/etc/keymap/kr.bmap.gz
    variant=${variant%%.*}
    echo $variant                  # outputs kr

* `${PARAMETER:+WORD}`

  expands to nothing if parameter unset or empty, if set, does not
  expand to parameter's value but instead specified value (here value
  of WORD)

    setup-interfaces ${quick:+-a} ${rst_if:+-r}

* `set -- $resp`

  special case behavior see set(1p)
  
  sets positional arguments so e.g.:
  
    echo $1                         # no real output
    set -- "hello"
    echo $1                         # outputs hello

## Resources

* https://bash-hackers.gabe565.com/

* https://www.gnu.org/software/bash/manual/html_node/Shell-Parameter-Expansion.html

* https://effective-shell.com/

* https://bash.cyberciti.biz/bash-reference-manual/Shell-Parameter-Expansion.html
