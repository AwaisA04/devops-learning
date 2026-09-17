# text processing

## task
Challenge: Parse /etc/passwd to list all users with /bin/bash as their shell. Document your command.

### command and explanation

doing the following command:

'''bash
cat /etc/passwd/
'''

provides a log for passwd but there is alot of information that we dont need.

and we also need to look for all users with /bin/bash as their shell only, so we would do:

'''bash
cat /etc/passwd/ | grep "/bin/bash"
'''

this pipes the result directly to the grep command which looks for /bin/bash in the passwd log, but we still have unnecessary information we dont need.

so,

'''bash
cat /etc/passwd | grep "/bin/bash" | awk -F: '{print $1, $7}'
'''

we will add the awk command to only print the user and its shell whilst using : as a separator

### What I learned

I learned how to use `awk` to filter structured text based on a specific field and print another field from the matching results.

