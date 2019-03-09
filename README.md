# Chordpro mode #

## Introduction ##

This is an emacs major mode, derived from text-mode, for editing files
in the Chordpro format, see
<http://www.chordii.org/> and <http://www.chordpro.org/>.

This is a fork of <https://github.com/hading/chordpro-mode.git>.
It has been adjusted for the official ChordPro format as implemented
by the reference implementation Chordii, see
<http://www.chordii.org>.

It is currently somewhat crude, but it does simplify a few things and
I do intend to keep adding any refinements that I find useful in my
work with Chordpro files. The font-lock is based off a previously
existing chordpro mode, but this provides more operations.

I'm still developing and experimenting with this, so as I go along I
might decide that different mouse or keybindings work better and will
probably provide more functionality as I see things that will make the
work that I do easier. There are some fairly obvious things left to do
and I'll add them I need them. If you have any ideas feel free to
create an issue (or even better do it and send a pull request).

## Installation ##

Copy chordpro-mode.el into somewhere in your emacs load path (I put it
in ~/.emacs.d).

Then put something like this into your .emacs file (I use the .cho
extension for such files; .pro would be an alternative but it is
already in use):

    (setq auto-mode-alist (cons '("\\.cho$" . chordpro-mode) auto-mode-alist))
    (autoload 'chordpro-mode "chordpro-mode")

Now when you visit a .cho file you should automatically get
chordpro-mode. The file will automatically be saved in latin-1
encoding (you can change this by setting the chordpro-file-encoding
variable in your .emacs, but you probably shouldn't as Chordii
currently expects latin-1 encoded files).

Some of the functions use dropdown-list.el, which can be installed
with package-list-packages in modern emacs. If you don't have this
installed they'll just do nothing.

## Use ##

### Keyboard ###

When you type a [ character, Emacs will prompt for a chord name. You
can enter the chord in all lowercase, it will be automatically upcased
if necessary. For convenience, minibuffer input can be terminated with
a ] character.

If this is too hot for you, set variable chordpro-hot-insert to nil
before loading chordpro-mode.el

Most of the other keyboard commands use the Ctrl-c prefix.

* Ctrl-c i : Insert a chord at the point. You'll be prompted for the
  chord name in the minibuffer. The brackets will automatically be
  inserted, space trimmed, and the chord capitalized.
* Ctrl-c l : Insert a chord at the point, chosen from a dropdown list
  of chords already in the document.
* Ctrl-c w : Kills the current chord. The current chord is one
  containing the point - because of the way emacs works this means
  that this command doesn't do what you want if the cursor is on the
  opening [ of a chord, only if it is between that and the closing ],
  inclusive. But there's another command for that.
* Ctrl-c z : Kills the next chord. Finds the next chord after the
  point and kills it. This one works if you are on the opening
  [, or if you are between chords.
* Ctrl-c r : Replace the current chord with one chosen from a dropdown
  list of chords already in the document.
* Ctrl-c c : Copy the current chord
* Ctrl-c x : Copy the next chord
* Ctrl-Meta-n : Move current chord forward PREFIX chars. 
* Ctrl-Meta-p : Move current chord backward PREFIX chars
* Ctrl-c m : Insert a chordpro comment
* Ctrl-c h : Insert a chordpro chorus
* Ctrl-c t : Insert a chordpro title
* Ctrl-c s : Insert a chordpro subtitle

### Mouse ###

Some of the commands can be invoked with the mouse. I still haven't
decided what I think the best way to go is, but these are some starting
experiments. All of them have corresponding keyboard commands (whether
specific to this mode or standard emacs commands).

* Ctrl-mouse-1 : Kills current chord
* Ctrl-mouse-2 : Insert a chord at the point, chosen from a dropdown list
  of chords already in the document. Note that unfortunately as currently
  implemented the mouse click can only bring up the menu - you still need
  to use the keyboard to perform the selection.
* Ctrl-mouse-3 : Kills next chord
* Shift-mouse-1 : Copies current chord
* Shift-mouse-2 : Insert chord
* Shift-mouse-3 : Copies next chord


