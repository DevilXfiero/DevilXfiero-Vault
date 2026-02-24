h -> left
j -> down 
k -> up
l -> right

i -> insert mode start of the word
Esc -> normal 
a -> append insert mode but end of the word
A -> append after the line
I -> append before the line

w -> jump around words
b -> jump back with words
e -> jump end of the word
$ -> end of the line
0 -> start of the line

f -> find follow by the first letter of the word
f ( -> find the first occurrence of ( 
; -> repeat find
, -> repeat backwards
F -> find backwards to the cursor

== - fix indentation
gg - top 
G -> bottom

dw - delete word (actually cut the text)
u - undo
p - paste after the cursor
P - paste before the cursor
y - yank 
yw - yanks word
dd - delete entire line
yy - yank the line
v - visual mode
R -> replace mode
ctrl + r -> redo
% -> takes to the matching counterpart of braces
ctrl + - -> to open terminal in lazy vim


<leader> c a - Code Actions
a - to add folder or file in neovim
<leader> s k - to search for keybindings
<leader> s s - symbols with telescope
shift + L -> right tab
shift + H -> left tab


Tmux

Sessions - Top most layer collection of one or more windows
Windows - tabs contains multiple panes 
Panes - splits in the windows

Prefix Key - ctrl + b
new window - <prefix> c
change window - <prefix> window number
cycle windows - <prefix> n or p (next or prev)
kill window - <prefix> &

panes horizontally <prefix> %
panes vertically <prefix> "
navigation <prefix> arrow keys
pane number - <prefix> q
zoom in pane to take full window - <prefix> z
pane into window -> <prefix> !
close the pane - <prefix> x


tmux ls
<prefix> s to see the tmux session 


VS Code shortcuts

Cmd + Shift + I -> Chat 
Cmd + J -> Terminal 
Cmd + . -> quickFix like getters and setters


## Vim with VSCode


Notes and Useful Vim Commands:

Modes:
- i: Enter Insert Mode
- Esc: Return to Normal Mode
- v: Enter Visual Mode
- V: Enter Visual Line Mode
- Ctrl+v: Enter Visual Block Mode

Navigation:
- h, j, k, l: Move left, down, up, right
- gg: Go to the beginning of the file
- G: Go to the end of the file
- :3: Go to line 3
- %: Jump to matching braces

Editing:
- yy: Yank (copy) a line
- p: Paste below
- dd: Delete a line
- u: Undo
- Ctrl+r: Redo
- :s/old/new/: Replace 'old' with 'new' in the current line
- :%s/old/new/g: Replace 'old' with 'new' globally

Visual Mode:
- v + movement: Select text
- d: Delete selected text
- y: Yank (copy) selected text

Macros:
- q<register>: Start recording a macro
- q: Stop recording
- @<register>: Play the macro

Buffers and Tabs:
- :e <filename>: Open a file in a buffer
- :ls: List all buffers
- :bnext / :bn: Go to the next buffer
- :bprev / :bp: Go to the previous buffer
- :tabedit <filename>: Open a file in a new tab
- gt: Go to the next tab
- gT: Go to the previous tab

Basic Search 
- /keyword  n->next match N->previous match 
- ?Keyword - Search backward
- /keyword\c - Case-sensitive
- 