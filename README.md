# n

This is a simple SQLite3 note-taking database.  The original was written by 
[Mike Chirico](mailto:mchirico@users.sourceforge.net) and in a tutorial he wrote, at 
[sourceforge.net](http://souptonuts.sourceforge.net/readme_sqlite_tutorial.html).

### Prerequites
- **SQLite3** (included with most modern operating systems) [Download](https://sqlite.org/download.html)
- **GNU awk** (included with most non-BSD flavours of Unix/Linux) OSX users can install it via [homebrew](https://brew.sh/)
- **Perl** (included with most modern operating systems)

### Usage
```
$ n
This command is used to list notes in 
a database.

n <option> 
 -a list all notes
 -l <rows> list most recent notes
 -t list notes for today
 -c list categories
 -f <search string> seach for text
 -e <cmd> execute command and add to notes
 -d delete last entry

$ n "This is a test"
$ n -t
1|This is a test|MyPC|2017-09-13 08:55:49
```

### Modifications

- Changed **timeEnter** column to use local time, instead of UTC.  In my opinion, dates and times that are 
"human-facing" should use local time.  UTC is useful for internal processes, and when comparing transactions.
- For better protection against SQL-injection, the simplistic method of replacing double and single quotes 
with an underscore has been replaced with [_perl_](https://www.perl.org/)_'s_ **uri_escape()** and a 
[_GNU awk_](https://www.gnu.org/software/gawk/) script for proper URI/URL encoding and decoding, respectively.
  - The **uri_unescape()** routine in [_perl_](https://www.perl.org/) was not suitable, since newlines are 
  handled in an undesirable maner for this application.
- Added **-l** option, to show the **last x** entries in the database.  This improves upon the **-t** switch 
that show's today's notes.
- Set default category to the hostname of the machine being used
  - This is a forward-looking feature, to distinguish between computers (I have more than one computer on my network.)
