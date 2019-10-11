# command_line_quickies
A collection of various command (one)liners and some useful ingredients to shell scripts.   
Some could be perfect examples of [nocontext subreddit](https://www.reddit.com/r/nocontext/) heh, but it means I used them in some project, so..
Collected from the interwebz mostly. Will give credits if I haven't forgotten the source.  

####  Error when pushing large files to git repo
Error when pushing : "error: RPC failed; HTTP 401 curl 22 The requested URL returned error: 401"
Use ```git config --global --unset http.postBuffer```

#### Random 
- basename of current directory    
 ```
CURRENT=`pwd`
BASENAME=`basename $CURRENT`
echo $BASENAME
```
- Name of the current folder:   
`pwd|awk -F'/' '{print $NF}'`   

Name of the current folder's parent:   
`pwd|awk -F'/' '{SL = NF-1; print $SL}'`   

- resize using imagemagick  
`find . -name "*.png" -exec convert {} -resize 400X400 {} \;`   
can also (officially) convert b/w image formats using imagemagick 

#### don't be a git tit
- Initialize git repo and add github remote
```
git init .
base_name=$(basename $(pwd))
git remote add github git@github.com:aashiqmuhamed/${base_name}.git
```

#### Renaming files (recursively)
- Recursively list all unique file extensions (this sort of breaks if you have files with no extension)     
`find ./ -type f | awk -F . '{print $NF}' |  sort --unique`

- change file names to some pattern    
`exiftool -ext '' '-filename<%f_${ImageSize}.${FileType}' .`

- Recursively find files with extension OLD_FILE_EXTENSION    
`find . -name "*.OLD_FILE_EXTENSION"`

- Rename to NEW_FILE_EXTENSION    
`find . -name "*.OLD_FILE_EXTENSION" -exec rename -v 's/\.OLD_FILE_EXTENSION$/\.NEW_FILE_EXTENSION/i' {} \;`

- Recursively delete files with no extension    
`find . -type f  ! -name "*.*"  `    
 if that's good, let's delete them   
`find . -type f  ! -name "*.*" -delete`

- Recursively delete files with a certain extension.   
  use it with precaution. Run first:
`find . -name "*.THIS_FILE_EXTENSION" -type f`
 If it's alright, let's delete it
`find . -name "*.THIS_FILE_EXTENSION" -type f -delete`

- Delete files other than .THIS_FILE_EXTENSION   
`rm -- *.!(THIS_FILE_EXTENSION)`   
Delete files other than .THIS_FILE_EXTENSION + those without any extension   
`rm -- !(*.THIS_FILE_EXTENSION)`   

- remove a string from all filenames
`for file in *; do mv "${file}" "${file//\REMOVE_THIS_STRING/}"; done`

- add a string in all fileneames
`for f in *; do mv "$f" "ADD_THIS_STRING_$f"; done`

- replace string
`rename 's/OLD_STRING/NEW_STRING/' *.FILE_EXTENSION`

- [Append name of parent folders and subfolders to the names of the multiple files [closed]](http://stackoverflow.com/questions/643372/append-name-of-parent-folders-and-subfolders-to-the-names-of-the-multiple-files)
```
#!/bin/bash

for f in `find . -name '*jpg'`
do
   filename=`echo $f|awk -F'/' '{SL = NF-1; TL = NF-2; print $TL "_" $SL  "_" $NF}'`
   cp $f newfolder/$filename
done
```

- PPA not found https://askubuntu.com/questions/65911/how-can-i-fix-a-404-error-when-using-a-ppa-or-updating-my-package-lists
```
#!/bin/bash
sudo rm /tmp/update.txt; tput setaf 6; echo "Initializing.. Please Wait" 
sudo apt-get update >> /tmp/update.txt 2>&1; awk '( /W:/ && /launchpad/ && /404/ ) { print substr($5,26) }' /tmp/update.txt > /tmp/awk.txt; awk -F '/' '{ print $1"/"$2 }' /tmp/awk.txt > /tmp/awk1.txt; sort -u /tmp/awk1.txt > /tmp/awk2.txt
tput sgr0
if [ -s /tmp/awk2.txt ]
then
  tput setaf 1
  printf "PPA's going to be removed\n%s\n" "$(cat /tmp/awk2.txt)"
  tput sgr0
  while read -r line; do echo "sudo add-apt-repository -r ppa:$line"; done < /tmp/awk2.txt > out
  bash out
else
  tput setaf 1
  echo "No PPA's to be removed"
  tput sgr0
fi
```
#### Basic vim configuration ~/.vimrc

```
set tabstop=4 expandtab
set list
set listchars=tab:>-
set mouse=r
```

#### Tmux right click to paste
prefix : set -g mouse off

#### Fastai on Google Colab
```
!pip install torchvision==0.1.9
!pip install fastai==0.7.0
!pip install torchtext==0.2.3
```

#### Delete files from a folder
/bin/rm: cannot execute [Argument list too long] (https://stackoverflow.com/questions/11289551/argument-list-too-long-error-for-rm-cp-mv-commands)
```
for f in *.pdf; do rm "$f"; done
```
#### Copy from tmux buffer to system buffer (clipboard)
For this to happen, you need to install xclip on your computer. Do it as:

```sudo apt-get install --assume-yes xclip```
After that, you need to add this line in ~/.tmux.conf file:

```bind -t vi-copy y copy-pipe "xclip -sel clip -i"```
Now close all your tmux sessions. From now onwards, whatever you copy in Tmux buffer will also land into system clipboard.

#### Jupyter port forwarding
https://fizzylogic.nl/2017/11/06/edit-jupyter-notebooks-over-ssh/

#### Docker run with mount
```docker run -v /host/directory:/container/directory -other -options image_name command_to_run```

#### Tensorboard on given port
``` tensorboard --logdir=/tmp  --port=8008 ```

#### Tmux conf - select and copy text within pane
I add the following to my ~/.tmux.conf. It will enable CTRL+b M (to turn tmux mouse on) and CTRL+b m (to turn tmux mouse off).
https://unix.stackexchange.com/questions/478922/tmux-select-and-copy-pane-text-with-mouse
```
# Toggle mouse on
bind-key M \
  set-option -g mouse on \;\
  display-message 'Mouse: ON'

# Toggle mouse off
bind-key m \
  set-option -g mouse off \;\
  display-message 'Mouse: OFF'
  ```
