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

