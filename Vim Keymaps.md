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
