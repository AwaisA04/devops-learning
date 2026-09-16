# File System Notes

Practical notes from Task 2 — File System Navigation.

## Commands Practiced

```bash
# Navigation
cd /var/log
ls -lah
pwd

# File operations
touch test.txt
mkdir -p projects/demo
cp test.txt projects/demo/
mv projects/demo/test.txt projects/demo/backup.txt
rm projects/demo/backup.txt

# Viewing files
cat /etc/passwd
less /var/log/syslog
head -n 20 /etc/services
tail -f /var/log/auth.log
```

## 5 Useful Commands I Discovered


1. **`tail -n`** —
   What it does: shows the last given lines in the file specified
   Why it's useful: instead of looking at the complete contents of the file, you could only look at the most recent ones, may also be more useful than less in a few cases as less requires you to navigate through the file entirely

2. **`file <filename>`** —
   What it does: tells you what type of file something is
   Why it's useful: it is not easy to determine the type of a file type and it may be misleading in some cases, for example data,txt may not be a text file but an image instead. Confirms file format without guessing

3. **`du -sh <folder>`** —
   What it does: shows the size of any given folder
   Why it's useful: gives the size of a specific folder instead of relying on ls -lh to show the size of the full directory

4. **`find . -name "*.txt"`** —
   What it does: searches through each directory for a similar pattern, in this case it looks for each file that contains '.txt'. You can replace the . to start from a specific path. Alternatively, you can add -type d to look for directories (find . -type d -name "demo")
   Why it's useful: allows you to look through specific directories or the entire folder for files containing a pattern instead of manually searching directories to find what is needed.

5. **`wc -l <filename>`** —
   What it does: tells you how many lines there are within a file
   Why it's useful: allows you to quickly receive a numerical figure of a file wc nstead of manually looking thorugh to see if it has any content (can also use it as a path)

