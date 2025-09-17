# wordle

A Bash script to help filter and suggest **Wordle** guesses from system dictionaries.
It builds a regex search based on known information (green/yellow/gray letters, position constraints, duplicates) and narrows down candidate words.

## Usage

```bash
CLI usage: $ wordle [OPTIONS] [GUESSES...]

Options:
  -m, --more, --huge         Always seach larger/additional dictionaries
                             (defined by $moredics in script)
  -l, --lower                Match only lowercase words in dictionaries (default behavior)
  -u, --upper                Match words containing uppercase letters in dictionaries
  -n, --noguess              Skip entering a new guess
  -r, --recycle              Reuse a single result from last run (usually paired with --choose)
  -c, --choose               Interactive candidate picker (*requires gum choose)
  -h, --help                 Show this message and exit
  [GUESSES...]               One or more 5-letter words to seed guesses

Examples:
  wordle
  wordle -u
  wordle CRANE
  wordle -r -c

Script fuctionality:
  Green/allowed letters and pattern are case insenstive.
  Specify double/triple letters by prefixing letter with 2/3, e.g., 2t2eh will result in
  a dictionary search requiring "TTEEH" **all** be included in the word > "TEETH" results.

* https://github.com/charmbracelet/gum

```
