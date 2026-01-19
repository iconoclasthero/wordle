# wordle

A Bash script to help filter and suggest **Wordle** guesses from system dictionaries.
It builds a regex search based on known information (green/yellow/gray letters, position constraints, duplicates) and narrows down candidate words.

## Usage

```bash
CLI usage: $ wordle [OPTIONS] [GUESSES...]

Options:
  -m, --more, --huge         Always seach larger/additional dictionaries
                             (defined by $moredics in script)
  -L, --lower                Match only lowercase words in dictionaries (default behavior)
  -u, --upper                Match words containing uppercase letters in dictionaries
  -n, --noguess              Skip entering a new guess
  -r, --recycle              Reuse a single result from last run (usually paired with --choose)
  -c, --choose               Interactive candidate picker (*requires gum choose)
  -l, --letters <#>          Change from default 5-letter wordle to # letters
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
  Entering "quit!" at the case-insenstive allowed letters prompt will exit.
  Control-C exits at any time.

* https://github.com/charmbracelet/gum

```


## Example run

```
$ wordle -ncr intro deals
Enter green and allowed letters: te    
Enter pattern using _ or - for unknowns: -e 
Guessed words: INTRO DEALS
Pattern: _ E _ _ _
Allowed letters: E T
Disallowed positions: T:3

Candidate list:
BEGET
HEFTY
TEETH
TEMPT
TEPEE

 Select from candidates:
   BEGET
   HEFTY
   TEETH
 > TEMPT
   TEPEE

The selected word: TEMPT


New guess count is 1.
RESTARTING /usr/local/bin/wordle with additional guess TEMPT

Enter green and allowed letters: 2te
Enter pattern using _ or - for unknowns: te   
Guessed words: INTRO DEALS TEMPT
Pattern: T E _ _ _
Allowed letters: E T
Duplicate letter: 2 T's.
Disallowed positions: T:3,5
TEETH
The selected word: TEETH


New guess count is 1.
RESTARTING /usr/local/bin/wordle with additional guess TEETH
Enter green and allowed letters: quit!
Exiting per user signal "QUIT!"
```

## Limitations

Presently the coloration marks all instances of a letter of known position from pattern entry as green regardless of where it appears in candidate words. The primary purpose of the yellow and green letters is to help the user to select words with unguessed letters as appropriate and this limitation is unlikley to change as it would represent diminishing returns.


