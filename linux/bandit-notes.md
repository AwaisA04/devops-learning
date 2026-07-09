Over the wire bandit

## Level 0 - 1:
**Challenge**: 
Locate readme file which holds the password

**solution**:
ls
cat readme

**explanation**:
-ls lists all files in the directory, readme is located, so cat is used to read the contents of readme

**Password**:
-ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If

**learned**: 
-ls lists all files and that cat is a powerful tool to read contents of a file

## Level 1 - 2:
Challenge: locate dashed “-” file inside home directory

**Solution**:
ls
cat ./-

**explanation**:
-doing cat ./- tells the terminal that - is a file and we want to read it, and that its not a symbol

**Password**:
263JGJPfgU6LtdEvgfWU1XP5yac29mFx

**learned**: 
- using ./ is important when a file may contain symbols

## Level 2 - 3:
**Challenge**: 
locate --spaces in this filename-- file and read it

**Solution**:
Cat -- “--spaces in this filename–” 

**explanation**:
-- signals the end of options to the command, anything after will be taken as an argument

**Password**:
MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx

**learned**: 
--

## Level 3 - 4:
**Challenge**: 
password in hidden file

**Solution**:
- ls -a inhere
- a option displays hidden files

**explanation**:
-a option shows hidden files

**Password**:
2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ

**learned**: 
-a

## Level 4 - 5:
**Challenge**: 
find human readable password in directory with files

**Solution**:
Cat ./-file07, jad the only human readable password

**Password**:
2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ

## Level 5 - 6:
**Challenge**: 
find password that is in a file which is:
Human readable
1033 bytes in size
Nt executable

**Solution**:
- Maybehere07 directory had a file by the name .file2
- ls -la to display properties of the files, such as permissions and file size

**Password**:
HWasnPhtq9AVKe0dmk45nxy20cvUa6EG

## Level 6 - 7:
**Challenge**: 
challenge : find password stored somewhere on the server has following:
User bandit7
Group bandit6
Size 33 bytes

**Solution**:
- Find / -group bandit6 -user bandit7 -size 33c 2>/dev/null
- Find [starting from] {option} … {option}          standardout the errors to the null folder 
- This gave the path to the file

**Password**:
c morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj

## Level 7 - 8:
**Challenge**:
password stored next to “millionth” in data.txt

**Solution**:
Grep “millionth” data.txt
Displays the line with millionth as well as the password

**Password**:
dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc

## Level 8 - 9:
**Challenge**: 
password on a line that only occurs once

**Solution**:
- Uniq command compares lines adjacent to each other so sort needs to be used first
- Uniq by itself compares adjacent lines, and deletes the second line that is repeated and displays the line

- Use sort data.txt - this sorts the lines in order
- Repeated lines are all adjacent to each other
- Uniq -u displays only unrepeated line
- Use piping: output of command becomes input of another command, denoted by ‘|’
- Sort data.txt | uniq -u

**Password**:
4CKMh1JI91bUIZZPXDqGanal4xvAg0JM

## Level 9 - 10:
**Challenge**: 
password is stored in one of the few human readable strings, preceded by several “=” characters.

**Solution**:
- Strings data.txt | grep “=”
- Strings data.txt : returns lines with all human readable strings
- Piping done
- Grep to search for “=”

**Password**:
FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey

## Level 10 - 11:
**Challenge**: 
data.txt contains base64 encoded data

**Solution**:
- Cat data.txt | tr 'A-Ma-mN-Zn-z' 'N-Zn-zA-Ma-m'
- Tr command maps one set to its corresponding set
- tr [set1] [set2]
- One set can have multiple ranges, each range maps to corresponding range on the next set
- [A-Za-z] [a-zA-z]

**Password**:
7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4
