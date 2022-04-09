## General UNIX commands
### Useful bash aliases

```
alias l='ls --color -lhF --group-directories-first'
```

### Using sponge to redirect to the same file
```
 < dates.txt nl | sponge dates.txt
 ```
 
 ### Shell functions
 
 ```
 func() {(echo 1; seq $1) | paste -s -d\* - | bc;}
 func 5
 ```
 
  ### Using trim to shape output to a specified height/width of characters
 
 ```
 cat /data/ch07/tips.csv | trim 5 25
 ```
  ### Use csvlook to print csv
 ```
 csvlook file.csv
 ```
 
 ### Use bat for cat with syntax highlighting. Add -A for displaying tabs/spaces
 ```
 bat -A file.txt
 ```
 ### Use tee for writing intermediate output to file
 ```
 seq 10 | tee num.txt | trim 5
 ```
 
 ### Use man or --help for manual. Use tldr if too long to read.
 ```
 man zshbuiltins | trim
 jq --help | trim
 tldr tar | trim
 ```
 ## Obtaining data
 
 
 
 
 
 
