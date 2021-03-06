# SK Card

## Help for learning a foreign language with batch-generated audio flashcards

This is a simple shell script that will generate foreign language audio flashcards.
It is called "SK Card" because, as written, the script generates flashcards for
learning the Slovak language.  However, you can edit the script to use any two
languages supported by Google's text-to-speech service.

## How to use

Invoke this script with two arguments:

1. The text for the front of the flashcard
2. The text for the back of the flashcard

By default, both the front and back of the card will be spoken in the foreign language
that is configured within the script.  By using the `-f` command-line option, the front of
the card will be spoken in the local language that is configured within the script.

As written, the local language is English and the foreign language is Slovak.

### Example

    skcard -o /home/fred/tmp/ -f "I am here" "Ja som tu"

In this example, The generated flashcard will be an MP3 file
containing the card-front speech in the local language, followed by
the card-back speech repeated twice in the foreign language, with
silence before and after the card-back speech.  The output file will be written to the
`/home/fred/tmp` directory.

Without the `-o` command-line option, the output file will be written
to the current working directory.  Without the `-f` command-line option, the card-front
text will be spoken in the foreign language.

## Using Existing Sound Files

If you already have the audio files, you can use this script to assemble them into a single file
by using the `-n` option:

    skcard -n <output-dir> <first-filename> <second-filename> [ <third-filename> ]

The third filename is optional.  If provided, the generated flashcard will contain the content of
each input file once.  If you provide only two input files, the second one will be repeated once.

The name of the output file will be generated from the names of the first (or only) two input files.
Everything after the last period in the input filenames will be stripped before
determining the name of the output file.

If you provide your own input files, they must be in MP3 format.

## Dependencies

For this script to work, you will need the following programs installed:

1. `ffmpeg`
2. `curl`
3. `jq`
3. `grep`
4. `sed`
5. `awk`
6. `hexdump`

Most of these are pretty standard.

## Bugs

The single-letter command-line arguments cannot be combined into clusters, and the order matters.
In particular, the debugging switch `-d` must, if used, come first.

If you provide audio files their names must have a suffix that will be stripped before
determining the output filename.

This script invokes `ffmpeg` more times than necessary to get the parameters necessary for generating
the silence in the output file.

## Credits

This is just a simple shell script that makes network requests using `curl`.  The actual text-to-speech
work is performed by the back-end of [Nick Pierson](https://twitter.com/NickOnTheWeb)'s
[Sound of Text](https://soundoftext.com/) web application.  This, in turn, uses
the speech-to-text engine of [Google Translate](https://translate.google.com/).
You can support Nick's valuable work on his [Patreon](https://www.patreon.com/nickpierson).
