## Bash Scripting: conditional statements
bash script has following conditional statements

- `if`
``` bash
#!/bin/bash

read val 

if [[ $val -eq 1 ]]; then
 echo "value is $val"
fi 
```

- `if elif`
``` bash
#!/bin/bash

read val 

if [[ $val -eq 1 ]]; then
 echo "value is 1"
elif [[ $val -gt 1 ]]; then
 echo "value is greater than 1"
else
 echo "value is less than 1"
fi
```

- `if`
``` bash
#!/bin/bash

read val 

if [[ $val -eq "1" ]]; then
 echo "value is 1"
else
 echo "value is less than 1" 
fi 
```