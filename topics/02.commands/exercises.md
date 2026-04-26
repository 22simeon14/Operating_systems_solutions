# Week 02 – Command Line Exercises

---

## 02-a-0100

**Task:**
Make a copy of the file /etc/passwd in your home directory under the name my_passwd.

**Solution:**

```bash
cp /etc/passwd my_passwd (От ~/)
```

---

## 02-a-0500

**Task:**
Create a directory practice-test in your home directory. Inside it, create a directory test1.
Can you do these two things at once? Check the appropriate man page.
Then create an empty file inside it called test.txt, and move it to practice-test using relative paths.

**Solution:**

```bash
mkdir -p ~/practice-test/test1
cd practice-test/test1
touch test.txt
mv test.txt ../test.txt
```

---

## 02-a-0600

**Task:**
Create the directory practice/01 in your home directory.
Create 3 files in it - f1, f2, f3.
Copy the files f1, f2, f3 from the directory practice/01/ to the directory dir1,
located in your home directory. If you do not have such a directory, create it.

**Solution:**

```bash
mkdir -p practice/01/
cd practice/01
touch f1
touch f2
touch f3
mv f1 ~/dir1
mv f2 ~/dir1
mv f3 ~/dir1
```

---

## 02-a-0601

**Task:**
Let the file f2 be moved to the directory dir2, located in your home directory, and be renamed to numbers.

**Solution:**

```bash
mkdir ~/dir2
cd dir1
mv f2 ~/dir2
cd ~/dir2
mv f2 numbers
```

---

## 02-a-1200

**Task:**
Print the names of all directories in the /home directory.

**Solution:**

```bash
find /home -mindepth 1 -maxdepth 1 -type d
```

---

## 02-a-4000

**Task:**
Create a file permissions.txt in your home directory. Give it only read permission
for the user who created the file, write and execute for the group, and read and execute for all others.
Do it both with bits and with symbolic notation.

**Solution:**

```bash
chmod 435 permissions.txt
chmod u=r,g=wx,o=rx permissions.txt
```

---

## 02-a-4100

**Task:**
To find what you have done today: find all files in your home directory
that have been modified in the last 1 hour.

**Solution:**

```bash
find ~/ -maxdepth 2 -type f -mmin -60
```

---

## 02-a-5000

**Task:**
Copy /etc/services to your home directory. Read it using the cat command.

**Solution:**

```bash
cp /etc/services ~/
cat services
```

---

## 02-a-5200

**Task:**
Create a symlink of the file /etc/passwd in your home directory.

**Solution:**

```bash
ln -s /etc/passwd passwd_symlink
```

---

## 02-a-5400

**Task:**
Print all regular files that /etc and its immediate subdirectories contain.

**Solution:**

```bash
find /etc -mindepth 1 -maxdepth 2 -type f
```

---

## 02-a-5401

**Task:**
Print only the first 5 lines of /etc/services

**Solution:**

```bash
head -n 5 /etc/services
```

---

## 02-a-5402

**Task:**
Print all regular files that only the immediate subdirectories of /etc contain.

**Solution:**

```bash
find /etc -mindepth 2 -maxdepth 2 -type f
```

---

## 02-a-5403

**Task:**
Print all immediate subdirectories of /etc

**Solution:**

```bash
find /etc -mindepth 1 -maxdepth 1 -type d
```

---

## 02-a-5500

**Task:**
Create a file that contains only the last 10 lines of the output of 02-a-5403

**Solution:**

```bash
touch log.txt
find /etc -mindepth 1 -maxdepth 1 -type d | tail -n 10 > log.txt
```

---

## 02-a-5501

**Task:**
Print the regular files larger than 42 bytes in your home directory

**Solution:**

```bash
find ~/ -type f -size +42c
```

---

## 02-a-5504

**Task:**
Print all regular files in the /tmp directory that belong to your group
and have write permission for the group or for others (o=w)

**Solution:**

```bash
find /tmp -type f -group $(id -gn) \( -perm -g=w -or -perm -o=w \)
```

---

## 02-a-5505

**Task:**
Print all files that are newer than practice/01/f1

**Solution:**

```bash
find ~ -type f -newer ~/dir1/f1
```

---

## 02-a-5506

**Task:**
Delete the files in your home directory that are newer than practice/01/f3

**Solution:**

```bash
find ~ -type f -newer ~/dir1/f3 -exec rm -i {} \;
```

---

## 02-a-6000

**Task:**
Find the files in /bin that can be read, written, and executed by everyone.

**Solution:**

```bash
find /bin -type f -perm -a=rwx
```

---

## 02-a-8000

**Task:**
Copy all files from /etc that can be read by everyone into the directory myetc

**Solution:**

```bash
mkdir ~/myetc
find /etc -type f -perm -a=r -exec cp {} ~/myetc \;
```

---

## 02-a-9000

**Task:**
Archive the files starting with 'c', then delete the directory and the archive.

**Solution:**

```bash
find ~/myetc -type f -name "c*" -exec tar -rf c_start.tar {} +;
rm -r ~/myetc
rm c_start.tar
```

---

## 02-a-9500

**Task:**
Print the number of lines in each file in /etc

**Solution:**

```bash
find /etc -type f -exec wc -l {} \;
```

---

## 02-b-4000

**Task:**
Copy the smallest file from those located in /etc

**Solution:**

```bash
find /etc -type f -exec wc -c {} + | sort -n | head -n 1
```
