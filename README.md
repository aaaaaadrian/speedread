speedread
=========

A simple terminal-based open source Spritz-alike.

This command line filter shows input text as a per-word RSVP (rapid
serial visual presentation) aligned on optimal reading points.  This
kind of input mode allows reading text at a much more rapid pace than
usual as the eye can stay fixed on a single place.

Basic Example
-------------

	cat tea.txt | ./speedread -w 250

	# Fullscreen mode — clears the terminal, centers the display
	cat tea.txt | ./speedread -w 500 -f

The default of 250 words per minute is very timid, designed so that you get
used to this.  Be sure to try cranking this up, 500wpm should still be fairly
easy to follow even for beginners.

![250wpm example](doc/speedread-250.gif)
![500wpm example](doc/speedread-500.gif)
![750wpm example](doc/speedread-750.gif)
![1000wpm example](doc/speedread-1000.gif)

Shell Completion
----------------

For zsh completion, copy `_speedread` to a directory on your `$fpath` and run `compinit`:

	cp _speedread ~/.zsh/completions/   # or wherever your fpath points
	echo 'fpath=(~/.zsh/completions $fpath)' >> ~/.zshrc
	echo 'autoload -U compinit && compinit' >> ~/.zshrc  # if not already set

Or run `speedread -h` / `speedread --help` for full usage.

Controls
--------

speedread is slightly interactive, with these controls accepted:

  * [ - slow down by 10%
  * ] - speed up by 10%
  * space - pause (and show the last two lines of context)
  * b - seek back 10 words
  * B - seek back 30 words
  * q - quit (shows stats and resume point)

Integration Recipes
-------------------

You can connect mutt with speedread by putting a macro like this in your
~/.muttrc (or pressing ':' in running mutt and pasting it):

	macro pager R "<enter-command>set pipe_decode=yes<enter>v|grep -v '^>' | ~/speedread/speedread<enter><enter-command>unset pipe_decode<enter>q" "speedread"

Then, just press R when viewing a message.  Unfortunately, it does not
work with non-ASCII messages (probably due to mutt limitations).

TODO
----

  * ~~Better word timing~~ — done: function words like "not", "can", "but" get extra time
  * ~~Support for seeking back/forward~~ — done: `b`/`B` keys
  * ~~More controls~~ — done: `q` to quit, `b`/`B` to seek back
  * ~~Make timing coefficients configurable~~ — done: `--wordtime`, `--commatime`, `--fstoptime`, `--lentime`, `--firsttime`
  * Automatically adjust wpm on trained content difficulty (look-ahead)?
  * Add a (Cairo-based?) simplistic graphical frontend (keeping with the
    filter philosophy). This would allow better eye guidance and large font.
  * An elinks-based recipe for reading websites this way.

Check out also [OpenSpritz](https://github.com/Miserlou/Glance-Bookmarklet) or
[spritz-js](https://github.com/richardtagger/spritz-js) if you want to
get this functionality in the web context.
