## Code layout

* Be consistent. Pick one style and stick to it.

* Use two spaces per indentation level. The main advantage being that it makes
  it difficult for other coders to insert tabs all over the place. It also
  helps in keeping the standard of 78 maximum width characters.

```perl
## Good.
sub function {
  my ($arg, @args) = @_;
  for my $item (@args) {
    last if divs_by_zero $item;
    do_something $item;
  }
  return $arg;
}

## Bad.
sub function {
    my ($arg, @args) = @_;
    for my $item (@args) {
        last if divs_by_zero $item;
        do_something $item;
    }
    return $arg;
}
```

* Do not use tabs. It makes code difficult to browse in some hosts (where 8
  spaces per tab is the standard) and only works when indenting by blocks.

### Comments

* Use Common Lisp comment style, meaning: Use four hash marks on headers; three hash marks on un-indented comments; two hash marks on indented comments and put inline comments starting at column 40, using one hash mark.

```perl
#### Module     : Useless module
#### Author     : elrzn <eric.lrzn@gmail.com>
#### Created on : 31 MAY 2012
package MyModule;

### Warning, evil function ahead!

## Does black magic. Highly unstable!
sub evil_function {
  my @damned = map  { evil_stuff $_ }  # This is an inline comment, and
               grep { guiltyp $_    }  #  we continue it this way.
               process @_;
  wantarray ? @damned : [@damned];
}
```

