# [Regex](https://hexdocs.pm/elixir/Regex.html)

Regex is based on PCRE (Perl Compatible Regular Expressions) and built on top of Erlang's `:re` module. More information can be found in the [`:re` module documentation](http://www.erlang.org/doc/man/re.html).

```elixir
# A simple regular expression that matches foo anywhere in the string
~r/foo/

# A regular expression with case insensitive and Unicode options
~r/foo/iu

#Internally a struct so matches
~r/(?<foo>.)(?<bar>.)/ == ~r/(?<foo>.)(?<bar>.)/


~r/https?.*example\d?\.com$/
~r/https?.*eta-pr-[[:digit:]]+.onrender.com$/ #matches "https://eta-pr-455.onrender.com" where number can change
```

### Usage

```elixir
String.match?("123", ~r/^[[:alnum:]]+$/) #true
String.match?("123 456", ~r/^[[:alnum:][:blank:]]+$/) #true
```

The supported class names are:

- alnum - Letters and digits
- alpha - Letters
- ascii - Character codes 0-127
- blank - Space or tab only
- cntrl - Control characters
- digit - Decimal digits (same as \d)
- graph - Printing characters, excluding space
- lower - Lowercase letters
- print - Printing characters, including space
- punct - Printing characters, excluding letters, digits, and space
- space - Whitespace (the same as \s from PCRE 8.34)
- upper - Uppercase letters
- word - "Word" characters (same as \w)
- xdigit - Hexadecimal digits