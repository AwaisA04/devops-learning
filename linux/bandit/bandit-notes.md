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
ls -a inhere
```

**Explanation:** The `-a` option shows hidden files (those starting with a `.`), which are otherwise excluded from a normal `ls` listing.

**Password:** 2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ

**What I learned:** Hidden files start with a `.` and need `-a` to appear in a directory listing.

---

## Bandit Level 4 → 5

**Challenge:** Find the human-readable password among several files in a directory.

**Solution:**
```bash
cat ./-file07
```

**Explanation:** Of all the files in the directory, `-file07` was the only one containing human-readable text — the rest were binary/non-readable.

**Password:** 4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw

**What I learned:** Not all files in a directory are readable text — checking each one (or using `file` to check type first) is often necessary.

---

## Bandit Level 5 → 6

**Challenge:** Find a file with these properties: human-readable, 1033 bytes in size, not executable.

**Solution:**
```bash
ls -la
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
find / -group bandit6 -user bandit7 -size 33c 2>/dev/null
```

**Explanation:** `find` searches from the given starting point (`/`) using the listed criteria (group, user, size); `2>/dev/null` redirects error output (e.g. permission denied messages) to null so only valid results are shown.

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
sort data.txt | uniq -u
```

**Explanation:** `uniq` only compares *adjacent* lines, so the file needs to be sorted first so repeated lines end up next to each other. `uniq -u` then prints only the lines that have no duplicates. The `|` pipes the sorted output directly into `uniq`.

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
cat data.txt | tr 'A-Ma-mN-Zn-z' 'N-Zn-zA-Ma-m'
```

**Explanation:** `tr` maps characters from one set to a corresponding character in another set. Here it implements a ROT13 cipher — shifting each letter 13 places through the alphabet, with ranges wrapping (A-M ↔ N-Z, a-m ↔ n-z) to decode the text back to plain readable form.

**Password:** dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr

**What I learned:** `tr` can define multiple character ranges in one call, each range mapping to its corresponding range in the second set — useful for implementing simple substitution ciphers like ROT13.