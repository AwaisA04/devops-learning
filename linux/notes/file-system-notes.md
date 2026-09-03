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

2. **`command`** —
   What it does:
   Why it's useful:

3. **`command`** —
   What it does:
   Why it's useful:

4. **`command`** —
   What it does:
   Why it's useful:

5. **`command`** —
   What it does:
   Why it's useful:

