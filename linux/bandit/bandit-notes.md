Over the wire bandit

## Bandit Level 0 → 1

**Challenge:** Locate the README file which holds the password.

**Solution:**
```bash
ls
cat readme
```

**Explanation:** `ls` lists all files in the current directory so I can see the README exists; `cat` then reads and prints its contents to the terminal.

**Password:** ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If

**What I learned:** `ls` lists files in a directory, and `cat` is a powerful tool for reading file contents directly in the terminal.

## Bandit Level 1 → 2

**Challenge:** Locate the dashed `-` file inside the home directory.

**Solution:**
```bash
ls
cat ./-
```

**Explanation:** Using `cat ./-` tells the terminal that `-` is a filename, not a flag/symbol, so it reads the file instead of misinterpreting it as an option.

**Password:** 263JGJPfgU6LtdEvgfWU1XP5yac29mFx

**What I learned:** Prefixing a filename with `./` is important when a file may start with a symbol that could otherwise be mistaken for a command option.

---

## Bandit Level 2 → 3

**Challenge:** Locate the file named `--spaces in this filename--` and read it.

**Solution:**
```bash
cat -- "--spaces in this filename--"
```

**Explanation:** `--` signals the end of options for the command; anything after it is treated as a literal argument, not a flag.

**Password:** MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx

**What I learned:** `--` is a general Unix convention for telling a command "stop parsing flags, treat the rest as arguments."

---

## Bandit Level 3 → 4

**Challenge:** Find the password in a hidden file.

**Solution:**
```bash
ls -la inhere
```

**Explanation:** The `-la` option shows hidden files (those starting with a `.`), which are otherwise excluded from a normal `ls` listing.

**Password:** 2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ

**What I learned:** Hidden files start with a `.` and need `-a` to appear in a directory listing.

---

## Bandit Level 4 → 5

**Challenge:** Find the human-readable password among several files in a directory.

**Solution:**
```bash
cat ./-file07
```

**Explanation:** Of all the files in the directory, `-file07` was the only one containing human-readable text, this was shown by the 'ASCII text' indicator — the rest were binary/non-readable.

**Password:** 4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw

**What I learned:** Not all files in a directory are readable text — checking each one (or using `file` to check type first) is often necessary.

---

## Bandit Level 5 → 6

**Challenge:** Find a file with these properties: human-readable, 1033 bytes in size, not executable.

**Solution:**
```bash
cd inhere
ls -la
find . type -f -size 1033c ! -executable
cat ./maybehere07/.file2
```

**Explanation:** `ls -la` was used to inspect file sizes and permissions across the directory tree to narrow down which file matched all three properties, leading to `.file2` inside `maybehere07`.

**Password:** HWasnPhtq9AVKe0dmk45nxy20cvUa6EG

**What I learned:** `ls -la` is useful for comparing file sizes and permissions side-by-side when hunting for a file matching specific criteria.

---

## Bandit Level 6 → 7

**Challenge:** Find a password stored somewhere on the server, owned by user `bandit7`, group `bandit6`, size 33 bytes.

**Solution:**
```bash
cd /
find / -group bandit6 -user bandit7 -size 33c 2>/dev/null
cat ./var/lib/dpkg/info/bandit7.password
```

**Explanation:** `find` searches from the given starting point (`/`) which searches the entire filesystem using the listed criteria (group, user, size); `2>/dev/null` redirects error output (e.g. permission denied messages) to null so only valid results are shown.

**Password:** c morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj

**What I learned:** `find` can filter by ownership and exact size, and redirecting stderr with `2>/dev/null` keeps noisy permission errors out of the results.

---

## Bandit Level 7 → 8

**Challenge:** Password is stored next to the word "millionth" in `data.txt`.

**Solution:**
```bash
grep "millionth" data.txt
```

**Explanation:** `grep` searches the file for the given string and prints the matching line, which contains the password.

**Password:** dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc

**What I learned:** `grep` is a fast way to search large files for a known keyword instead of reading through manually.

---

## Bandit Level 8 → 9

**Challenge:** Password is on the line that occurs only once in the file.

**Solution:**
```bash
cat data.txt | sort | uniq -u
```

**Explanation:** `cat` read the contents of the file, `uniq` only compares *adjacent* lines, so the file needs to be sorted first so repeated lines end up next to each other. `uniq -u` then prints only the lines that have no duplicates. The `|` pipes the sorted output directly into `uniq`.

**Password:** 4CKMh1JI91bUIZZPXDqGanal4xvAg0JM

**What I learned:** `uniq` requires sorted input to work correctly, and piping (`|`) lets you chain a command's output directly into the next command's input.

---

## Bandit Level 9 → 10

**Challenge:** Password is one of the few human-readable strings in the file, preceded by several `=` characters.

**Solution:**
```bash
strings data.txt | grep "="
```

**Explanation:** `strings` extracts human-readable text from a file (useful for binary/mixed-content files), and piping into `grep "="` filters down to lines containing the `=` characters mentioned in the challenge.

**Password:** FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey

**What I learned:** `strings` is essential for pulling readable text out of binary or non-plain-text files.

---

## Bandit Level 10 → 11

**Challenge:** `data.txt` contains base64-encoded... actually ROT13-encoded data (based on the solution used).

**Solution:**
```bash
cat data.txt | base64 -d 
or
base64 -d data.txt
```

**Explanation:** `base64` is the command of working with base64 and `-d` is the command to decode the file in base64

**Password:** dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr

**What I learned:** `-d` is essential for working with base64 as it decodes the file.

## Bandit Level 11 → 12

**Challenge:** password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions

**Solution:**

```bash
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```
**Explanation**: tr translates characters from one set to a corresponding character in another set. Here it implements a ROT13 cipher — shifting each letter 13 places through the alphabet, with ranges wrapping (A-M ↔ N-Z, a-m ↔ n-z) to decode the text back to plain readable form.

**Password**: GROozWPO8QyN0mGrjUkID0WCYkZiQxrN

**What I learned:**: tr can define multiple character ranges in one call, each range mapping to its corresponding range in the second set — useful for implementing simple substitution ciphers like ROT13.


## Bandit Level 12 → 13

**Challenge:** password is in a hexdump, has been repeatedly comrpessed

**Solution:** 

```bash
mkdir /tmp/bandit122
cp data.txt /tmp/bandit122
cd /tmp/bandit12
xxd -r data.txt data
file data
mv data data.gz
gzip -d data.gz
file data
```
**Explanation**: In Bandit Level 12 → 13, I learned how to work with files that have been converted into a hexadecimal dump and then compressed multiple times. I used xxd -r to reverse the hex dump back into a file, and then used the file command to identify what type of compression or archive I was dealing with

**What I learned:** I learned how to use commands such as gzip, bzip2, and tar to decompress or extract files, repeating the process until I reached the final text file containing the password. This taught me how to identify file types and work with different compression formats in Linux.

## Bandit Level 13 → 14

**Challenge:** The challenge was to send the Bandit 14 password to a service running on port 30000 using Netcat (`nc`) and receive the password for Bandit 15.


**Solution:**
```bash
cat sshkey.private
exit
touch ~/sshkey.private
nano ~/sshkey.private ## paste the key
ls -l ~/sshkey.private
chmod 600 ~/sshkey.private
ssh -i ~/sshkey.private -p 2220 bandit14@bandit.labs.overthewire.org
whoami
```

**Explanation** In Bandit Level 13 → 14, I was given an SSH private key called sshkey.private instead of a password. The aim was to use this private key to authenticate as the bandit14 user. Because OverTheWire prevents SSH connections between Bandit accounts from inside the server, I had to copy the private key to my own computer and then connect to bandit14 from my local Ubuntu terminal using SSH. The -i option tells SSH which private key to use, while -p 2220 specifies the port used by the Bandit server.

**What I learned:** I learned that SSH can authenticate users using a private key instead of a password. I also learned how to use the -i option with SSH to specify an identity file and how to use -p to specify a non-standard SSH port. I learned that files created with touch are empty until content is added, and that SSH private keys need to be stored correctly and given appropriate permissions using chmod 600. This level also helped me understand the difference between working inside a remote Linux server and using my own local terminal.

## Bandit Level 14 → 15
**Challenge:** The challenge was to find the Bandit 14 password and submit it to a service running on the local machine at port 30000. The service would check the password and return the password for Bandit 15 if it was correct.

**Solution:**
```bash
cat /etc/bandit_pass/bandit14
aaWecNkG4FhxJQxz07uiwzVP6bJiYS65
## paste password in
```
**Explanation:** The challenge involved connecting to a service running on localhost on port 30000 using Netcat (nc). I retrieved the Bandit 14 password and entered it into the service, which returned the password for Bandit 15.

**What I learned:** I learned how to use Netcat to communicate with a network service through a specific port. I also learned how localhost refers to the current machine and how ports are used to access different network services.

## Bandit Level 15 → 16
**Challenge:** The challenge was to connect to a service running on localhost at port 30001 and submit the Bandit 15 password. Unlike the previous level, this service required an SSL/TLS encrypted connection.
**Solution:**
```bash
whoami
cat /etc/bandit_pass/bandit15 ### copy and paste password into the next command to recieve password for bandit 16
openssl s_client -connect localhost:30001
```
**Explanation:** I used openssl s_client -connect localhost:30001 to establish a secure connection to the service. I then entered the Bandit 15 password, and the service returned the password for Bandit 16.

**What I learned:** to create an SSL/TLS connection to a network service. I also learned that some services require encrypted connections rather than a standard Netcat connection.

## Bandit Level 16 → 17
**Challenge:** The challenge was to scan ports 31000–32000 and find the one running an SSL service that accepted the Bandit 16 password. After connecting to the correct port, the service provided an SSH private key that could be used to log into Bandit 17.

**Solution:**
```bash
nmap -sV -p 31000-32000 localhost
openssl s_client -connect localhost:31790
nano ~/bandit17_keyy
chmod 600 ~/bandit17_key
ssh bandit16@bandit.labs.overthewire.org -p 2220
```

**Explanation:** I used nmap to scan the available ports and identified port 31790 as the relevant SSL service. I then used openssl s_client to connect securely to the service and entered the Bandit 16 password, which returned an SSH private key. I saved the key locally, changed its permissions with chmod 600, and used it to connect to Bandit 17.

**What I learned:** I learned how to scan ports with nmap, connect to an SSL service using OpenSSL, and use an SSH private key for authentication. I also learned why private keys need secure file permissions and why SSH connections must sometimes be made from the local machine.
## Bandit Level 17 → 18
**Challenge:** The goal was to find the password for Bandit 18. There were two files, passwords.old and passwords.new, and the password was the only line that had changed between them.
**Solution:**
```bash
ls 
diff passwords.old passwords.new
```
**Explanation:** I used the diff command to compare the two files:

diff passwords.old passwords.new

This showed the difference between the files, allowing me to identify the changed line. The changed line was the password for Bandit 18.
**What I learned:** I learned how to use diff to compare the contents of two files and identify changes. I also learned how comparing files can be useful for finding specific information efficiently.
## Bandit Level 18 → 19
**Challenge:** The challenge was to log in as Bandit 18 and find the password for Bandit 19. However, the shell was configured to immediately log me out, so I had to find another way to access the readme file.
**Solution:**
```bash
ssh bandit18@bandit.labs.overthewire.org -p 2220 cat readme
```
**Explanation:** Instead of opening an interactive SSH session, I used SSH to run the cat readme command directly on the Bandit 18 server. This allowed me to read the file before the shell could log me out and retrieve the password for Bandit 19.
**What I learned:** I learned that SSH can be used to execute commands remotely without opening an interactive shell. I also learned how this can be useful when a user's shell prevents normal login access.
## Bandit Level 19 → 20

**Challenge:** The goal was to find the password for Bandit 20. The bandit20-do program allowed me to execute commands as the bandit20 user, so I needed to use it to access the Bandit 20 password file.

**Solution:** 
```bash
ls
./bandit20-do
./bandit20-do cat /etc/bandit_pass/bandit20
```

**Explanation:** I used `./bandit20-do cat /etc/bandit_pass/bandit20.` The `bandit20-do` program ran the cat command with the permissions of the Bandit 20 user, allowing me to read the password file and retrieve the password for the next level.

**What I learned:** I learned how executables can be used to run commands with another user's permissions. I also learned how Linux file permissions and user privileges control access to sensitive files.