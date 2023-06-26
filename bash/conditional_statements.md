## Bash Scripting: conditional statements by example
bash script has following conditional statements

- `if`
``` bash
#!/bin/bash

read val 

if [[ $val -eq 1 ]]; then
 echo "value is $val"
fi 
```

- `if elif else`
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

- `if else`
``` bash
#!/bin/bash

read val 

if [[ $val -eq "1" ]]; then
 echo "value is 1"
else
 echo "value is less than 1" 
fi 
```