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
 ```
 
