# 03 – Pipes Exercises

---

## 03-a-0200

**Task:**
Sort /etc/passwd lexicographically by the UserID field.

**Solution:**

```bash
sort -t ':' -k 3 /etc/passwd
```

---

## 03-a-0201

**Task:**
Sort /etc/passwd numerically by the UserID field.
(Observe the differences with lexicographical sorting)

**Solution:**

```bash
sort -t ':' -k 3 -n /etc/passwd
```

---

## 03-a-0210

**Task:**
Print only the 1st and 5th columns of /etc/passwd using ":" as delimiter.

**Solution:**

```bash
cut -d ':' -f 1,5 /etc/passwd
```

---

## 03-a-0211

**Task:**
Print the contents of /etc/passwd from the 2nd to the 6th character.

**Solution:**

```bash
cut -c 2-6 /etc/passwd
```

---

## 03-a-0212

**Task:**
Print the usernames and their home directories from /etc/passwd.

**Solution:**

```bash
cut -d ':' -f 1,6 /etc/passwd
```

---

## 03-a-0213

**Task:**
Print the second column of /etc/passwd, using '/' as delimiter.

**Solution:**

```bash
cut -d '/' -f 2 /etc/passwd
```

---

## 03-a-1500

**Task:**
Print the number of bytes in /etc/passwd.
Print the number of characters in /etc/passwd.
Print the number of lines in /etc/passwd.

**Solution:**

```bash
wc -c /etc/passwd
wc -m /etc/passwd
wc -l /etc/passwd
```

---

## 03-a-2000

**Task:**
Using separate commands, extract from /etc/passwd:

* the first 12 lines
* the first 26 characters
* all lines except the last 4
* the last 17 lines
* the 151st line (or another if not enough lines) – 20th
* the last 4 characters of the 13th line

**Solution:**

```bash
head -n 12 /etc/passwd
head -c 26 /etc/passwd
head -n -4 /etc/passwd
tail -n 17 /etc/passwd
head -n 20 /etc/passwd | tail -n 1
head -n 13 /etc/passwd | tail -n 1 | tail -c 5
```

---

## 03-a-3000

**Task:**
Save the output of `df -P` into a file in your home directory.

Write a command that prints the contents of this file without the first line (header), sorted by the second field (numeric).

**Solution:**

```bash
touch 03-a-3000.txt
df -P | cat >> 03-a-3000.txt
tail -n +2 ~/03-a-3000.txt | sort -k 2 -n
```

---

## 03-a-3100

**Task:**
Save only the usernames from /etc/passwd into a file called users in your home directory.

**Solution:**

```bash
cut -d ':' -f 1 /etc/passwd > ~/users
```

---

## 03-a-3500

**Task:**
Print all usernames from /etc/passwd in uppercase.

**Solution:**

```bash
cut -d ':' -f 1 /etc/passwd | tr 'a-z' 'A-Z'
```

---

## 03-a-5000

**Task:**
Print the line in /etc/passwd containing your user.

Print that line and the two lines before it.

Print that line, the two lines before it, and the three lines after it.

Print *only* the line that is 2 lines before the line containing your user.

**Solution:**

```bash
grep "$USER:" /etc/passwd (grep -i "monio" /etc/passwd)
grep -B 2 "$USER:" /etc/passwd
grep -B 2 -A 3 "$USER:" /etc/passwd
grep -B 2 "$USER:" /etc/passwd | head -n 1
```

---

## 03-a-5001

**Task:**
Print how many users do not use /bin/bash as login shell according to /etc/passwd.

**Solution:**

```bash
cut -d ':' -f 7 /etc/passwd | grep -v "^/bin/bash$" | wc -l
```

---

## 03-a-5002

**Task:**
Print only the names of people with a second name longer than 6 characters according to /etc/passwd.

**Solution:**

```bash
cut -d ':' -f 5 /etc/passwd | grep -E "^[^ ]+ [^ ]{7,}.*$"
```

---

## 03-a-5003

**Task:**
Print the names of people with a second name shorter than 8 characters (<=7) according to /etc/passwd.

**Solution:**

```bash
cut -d ':' -f 5 /etc/passwd | grep -E "^[^ ]+ [^ ]{0,7}( |$)"
```

---

## 03-a-5004

**Task:**
Print the full lines from /etc/passwd for the people from 03-a-5003.

**Solution:**

```bash
grep -E '^[^:]*:[^:]*:[^:]*:[^:]*:[^ ]+ [^ ]{0,7} ' /etc/passwd
```

---

## 03-a-6000

**Task:**
Copy <REPO>/exercises/data/emp.data to your home directory.
Using awk, print:

* total number of lines
* the third line
* the last field of each line
* the last field of the last line
* each line with more than 4 fields
* each line whose last field is greater than 4
* total number of fields across all lines
* number of lines containing "Beth"
* the largest third field and the line containing it
* each line with at least one field
* each line with more than 17 characters
* number of fields per line and the line itself
* first two fields swapped
* each line with swapped first two fields
* each line with first field replaced by line number
* each line without the second field
* sum of second and third field for each line
* total sum of second and third field

**Solution:**

```bash
awk 'END {print NR}' ~/emp.data
awk 'NR==3' ~/emp.data
awk '{print $NF}' ~/emp.data
awk 'END {print $NF}' ~/emp.data
awk 'NF>4 {print $0}' ~/emp.data
awk '$NF>4 {print $0}' ~/emp.data
awk '{sum+=NF} END {print sum}' ~/emp.data
awk '/Beth/ {c++} END {print c}' ~/emp.data
awk 'max<$3 {max=$3; line=$0} END {print max ":" line}' ~/emp.data
awk 'NF>=1 {print}' ~/emp.data
awk 'length($0)>17' ~/emp.data
awk '{print NF ":" $0}' ~/emp.data
awk '{print $2, $1}' ~/emp.data
awk '{tmp=$1; $1=$2; $2=tmp; print}' ~/emp.data
awk '{$1=NR; print}' ~/emp.data
awk '{$2=""; print}' ~/emp.data
awk '{print $2+$3}' ~/emp.data
awk '{s+=($2+$3)} END {print s}' ~/emp.data
```

---

## 03-b-0300

**Task:**
Find only your Group ID from /etc/passwd.

**Solution:**

```bash
grep -E '^.*'$USER'.*$' /etc/passwd | cut -d ':' -f 4
grep "^$USER:" /etc/passwd | cut -d ':' -f 4
```

---

## 03-b-3400

**Task:**
How many comments are there in /etc/services?

**Solution:**

```bash
grep -c '#' /etc/services
```

---

## 03-b-3500

**Task:**
How many files in /bin are shell scripts (ASCII text files)?

**Solution:**

```bash
find /bin -type f -exec file {} \; | grep -E 'ASCII text' | wc -l
```

---

## 03-b-3600

**Task:**
Create a list of directories in your filesystem that you do not have access to (up to depth 3).

**Solution:**

```bash
find / -mindepth 1 -maxdepth 3 -type d 2>&1 >/dev/null | grep -E 'Permission denied' > ~/unreachable.txt
```

---

## 03-b-4000

**Task:**
Create the following structure in your home directory:

dir5/file1
dir5/file2
dir5/file3

Fill them with given content using vi.

Print:

* stats (lines, words, characters) per file
* stats (lines, characters) total
* total number of lines

**Solution:**

```bash
mkdir -p ~/dir5
cd ~/dir5
touch file1 file2 file3
vi file1
vi file2
vi file3
wc file1 file2 file3
wc -l -m file1 file2 file3
cat file1 file2 file3 | wc -l
```

---

## 03-b-4001

**Task:**
Replace all lowercase letters with uppercase in file2 (in place).

**Solution:**

```bash
cat ~/dir5/file2 | tr 'a-z' 'A-Z' > temp && mv temp ~/dir5/file2
```
