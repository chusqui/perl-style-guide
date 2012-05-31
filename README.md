# Perl style guide

A few guidelines for a 'post-modern' Perl coding style.

Work in progress. Suggestions and contributions are welcome!

### Disclaimer

This is just another coding style guide and by no means an attempt to define a
standard. Please don't take it as the ultimate truth.

If you don't agree with something on this guide, fine! I'll invite to make
your very own one. Make sure to read the excellent Perl Best Practices book by
Damian Conway.

The most important thing, after all, is that both you and your teammates are
comfortable with a given guideline and stick to it.

## Code layout

* Try to limit your code to 72-78 column lines...

* ... but don't stress over it. Real world code often has very long sentences,
  and trying to force them to be below 78 columns leads to tight, but ugly code.
  In a nutshell: <= 72 is perfect, <= 78 is great, > 78 is not as bad as some
  folks might try to make you believe.

```perl
## Don't do this:
my $str =
  "Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor aliqua.";

## Do this instead:
my $str = "Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor aliqua.";

## This is just wrong and a waste of time. Don't ever do this:
my $str = "Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do "
        . "tempor incididunt ut labore et dolore magna aliqua. Ut enim ad"   
        . "minim veniam, quis nostrud exercitation ullamco laboris nisi ut"  
        . "aliquip ex ea commodo consequat. Duis aute irure dolor in "       
        . "reprehenderit in voluptate velit esse cillum dolore eu fugiat"    
        . "nulla pariatur. Excepteur sint occaecat cupidatat non proident, " 
        . "sunt in culpa qui officia deserunt mollit anim id est laborum.";

## This is actually okay. Notice the EOL flag?
my $str = "Lorem ipsum dolor amet, consectetur adipisicing elit, sed do eiusmod tempor aliqua.\n"
        . "Ut enim ad minim veniam, quis nostrud exercitation laboris nisi commodo consequat.\n"
        . "Duis aute irure dolor in reprehenderit in cillum dolore eu fugiat nulla pariatur.\n"
        . "Excepteur sint occaecat non proident, sunt in culpa qui mollit anim id est laborum.";
```

* Use two spaces per indentation level. The main advantage being that it makes
  it a bit more difficult for undisciplined coders to insert tabs all over the
  place. Decreasing the level of indentation also helps in keeping a maximum of
  78 column lines.

```perl
## Good.
sub function {
  my ($arg, @args) = @_;
  for my $item (@args) {
    last if divides_by_zero $item;
    do_something $item;
  }
  $arg;
}

## Bad.
sub function {
    my ($arg, @args) = @_;
    for my $item (@args) {
        last if divides_by_zero $item;
        do_something $item;
    }
    $arg;
}
```

* Do not use tabs. It makes code difficult to browse in some hosts (where 8
  spaces per tab is the standard) and only works when indenting by blocks.

* Brace operators in a K&R style. GNU style adds an unnecessary amount of
  lines with no additional information on them.

```perl
## Good.
sub function {
  if (test) {
    ...
  }
}

## Bad.
sub function
{
  if (test)
  {
    ...
  }
}
```

* Brace, parenthesize and indent data structures on a Lispy way.

```perl
## Good.
my $self = {name    => 'Max Payne',
            age     => 43,
            weapon  => 'Beretta 92f'
            motives => [qw(revenge)]
            targets => ['Vladimir Lem', 'Vinnie Cognitti',
                        'Jack Lupino',  'Frankie Niagara']};

## Bad.
my $self = {
  name    => 'Max Payne',
  age     => 43,
  weapon  => 'Beretta 92f'
  motives => [qw(revenge)]
  targets => [
    'Vladimir Lem', 'Vinnie Cognitti',
    'Jack Lupino',  'Frankie Niagara'
  ]
};
```

* Try to restrict yourself to only one statement per line of code.

* Put a semicolon after every statement, unless it's the last statement in a
  one-line block.

```perl
## Notice that the last statement doesn't have a semicolon afterwards.
my $fact = sub { my ($n, $ret) = ($_[0], 1); $ret *= $_ for 1 .. $n; $ret }
```

* Do not put spaces between spaces, braces and brackets. That is, arrays,
  hashes, array and hash references, string and command line delimiters.

```perl
my ( $self, $who, @params ) = @_;      # Bad.
my ($self, $who, @params) = @_;        # Good.

my $self = { name => "Eric", age => 26 };  # Bad.
my $self = {name => "Eric", age => 26};    # Good.

my @files = qx| ls $str |;             # Bad.
my @files = qx|ls $str|;               # Good.
```

Please keep in mind that this does not apply to operators.

```perl
my $fn = sub {$_[0] + 1};              # Bad.
my $fn = sub { $_[0] + 1 };            # Good.

my @items = map {do_something_to $_} @_;    # Bad.
my @items = map { do_something_to $_ } @_;  # Good.
```

* Use whitespace between operators.

```perl
## Good.
my $area = $pi * ($radius ^ 2);

## Bad.
my $area = $pi*($radius^2);
```

* Don't cuddle an else.

```perl
## Good
if (condition) {
  ...
}
else {
  ...
}

## Bad.
if (condition) {
  ...
} else {
  ...
}
```

* Align items vertically.

```perl
my @months = qw(January   February March    April
                May       June     July     August
                September October  November December);

my $var_          = ...;
my $var_2         = ...;
my $var_long_name = ...;

my %h = (key1          => $val1,
         key_2         => $val2,
         key_long_name => $val3);
```

* Break long expressions before an operator.

```perl
## A good example taken from Conway's PBP:
push @steps, $steps[-1] +
    $radial_velocity * $elapsed_time +
    $orbital_velocity * ($phase + $phase_shift) -
    $DRAG_COEFF * $altitude;

## The same example using our custom guideline:
push @steps, $steps[-1] +
             $radial_velocity * $elapsed_time +
             $orbital_velocity * ($phase + $phase_shift) -
             $DRAG_COEFF * $altitude;
```

* Don't be afraid of using ternary operators, specially if it all fits in one
  line. An example:

```perl
say "I'll have a homemade ", is_it_summer ? 'ice cream' : 'hot chocolate';
```

* Indent ternary operators properly. A few examples:

```perl
my $variable = a_very_very_big_condition_name
                 ? is_this_very_long_subroutine
                 : is_that_one_that_is_even_larger;

my $var = cond_one               ? 'arg1'
        : cond_two               ? 'arg2'
        : cond_three_larger_name ? 'arg3'
        :                          'argn'
        ;
```

* Introduce and enforce the use of perltidy in your workplace. Be careful
  about introducing false deltas in your CVS though. Emacs has its own
  extension, so does Eclipse's EPIC. In VIM you can do something like this:

```vim
" Map F4 to a perltidy system call.
map <F4> !perltidy -q -gnu -i=2 -l=0 -pt=2 -bt=2 -sbt=2 -bbt=1 -nbl -vt=2 -vtc=2 -sct<CR>
" The same, but calling a configuration file.
map <F5> !perltidy -q -pro=/path/to/perltidyrc_file<CR>
```

### Comments

Perl always had a good reputation documentation wise. Let's keep up the good
work!

* Focus on producing self-documenting code. Document the why, not the how nor
  the what.

* Check grammatical mistakes and punctuate properly, even in in-line comments.

* Use Common Lisp comment style, meaning: Use four hash marks on headers;
  three hash marks on un-indented comments; two hash marks on indented
  comments and put in-line comments starting at column 40 (or two spaces after
  the last column where last column > 40), using one hash mark.

```perl
#### Module     : Useless module
#### Author     : elrzn <eric.lrzn@gmail.com>
#### Created on : 31 MAY 2012
package MyModule;

### Warning, evil function ahead!

## Does black magic. Highly unstable!
sub evil_function {
  ## Notice the vertical alignment in the following sentence...
  my @damned = map  { evil_stuff $_ }  # This is an inline comment, and
               grep { guiltyp $_    }  #  we continue it this way.
               process @_;
  wantarray ? @damned : [@damned];     # No explicit return in good old Perl fashion.
}
```

* Learn to use POD on all its glory.

* Place POD after your code if you're developing a module. Preferably __DATA__
  or __END__. Mixing code and POD is still acceptable when you just want to
  comment a few subroutines.

```perl
=head2 function_name : brief, optional description about types

This is a subroutine. It presumably does something.

Example:

  function_name %params;

=cut
sub function_name {
  ...
}
```

### Coding style

* Always unpack the stack first.

* Do not, ever, modify the stack. Unless necessary.

```perl
## Bad.
sub my_method {
  my $self = shift;
  my %params = @_;
  ...
}

## Good.
sub my_method {
  my ($self, %params) = @_;
  ...
}
```

* Favor the use of map and grep versus for and while loops.

* Favor the use of Perl's rich looping constructs versus recursion. Recursion
  in Perl is far from perfect, and even if you can have tail call optimization
  by using a magic goto, it's usually not advisable as it is scary for
  unexperienced developers (and then they'll fly to Ruby, or worse).

* Learn to use and master List::Util's reduce.

* Name booleans and predicates using the following nomenclature:

```perl
sub is_valid_p { ... }                 # Notice that the 'p' looks like '?'.

reboot_world if $finished_computing_p;

sub oddp { ... }

sub not_registered_p { ... }
```

* Name arrays in plural and hashes in singular.

* Use undercase separators instead of camelCase.

* Name constants in capital letters.

* Use strict and warnings (or better, Modern::Perl "$year") unless you want to
  summon the dark spirits and you really know what you're doing.

* Favor the use of Moose, Mouse, Mo or similar instead of classic Perl OOP.
  Join the revolution moose.perl.org

* Use the alternate infix if / unless syntax when working with single statements.

```perl
## Multiple statements.
if ($test) {
  do_something;
  do_something_else;
  make_sure_you_did \&function, @args;
}

# One statement.
do_something if $test;

## One, large statement.
print "Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor aliqua."
  if $can_print_p;
```

* Do not use 'and' whenever you can use an 'if' statement. It's technically
  correct, but doesn't really follow natural language rules.

```perl
## Bad.
behaves_like_zombie_p $suspicious_stranger 
  and shoot $suspicious_stranger, target => ':head';

## Good.
shoot $suspicious_stranger, target => ':head' 
  if behaves_like_zombie_p $suspicious_stranger;
```

* Do not perform 'if not', but rather 'unless'.

```perl
party_all_night if ! $sleepy;          # Bad.

party_all_night unless $sleepy         # Good.
```

* Use q{} for empty strings.

* Use q{ } for single space strings.

* Use "\t" for tabs.

## Recommended modules

## Performance tips

### Profiling
