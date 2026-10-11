# Kali Linux `Crunch` Tool

## 1. What is Crunch?

**Crunch** is a wordlist generator available in Kali Linux. It creates lists of possible words, numbers, or character combinations based on rules you give it.

These wordlists can be useful in **authorized security testing**, for example when testing the strength of your own passwords.

## 2. Basic Syntax

The basic command is:

```bash
crunch <min> <max> [characters] -o <output_file>
```

- `<min>` — minimum length of each item.
- `<max>` — maximum length of each item.
- `[characters]` — characters Crunch can use.
- `-o` — saves the generated list to a file.

## 3. Simple Example

```bash
crunch 2 3 abc
```

This tells Crunch to create combinations using `a`, `b`, and `c`, with lengths from **2 to 3**.

The output will contain combinations such as:

```text
aa
ab
ac
ba
bb
bc
...
aaa
aab
aac
...
```

## 4. Saving the Wordlist

You can save the result to a file:

```bash
crunch 2 3 abc -o words.txt
```

Now the generated combinations are written to `words.txt`.

You can view the file with:

```bash
cat words.txt
```

## 5. Using a Fixed Length

If you want only one length, make the minimum and maximum the same:

```bash
crunch 4 4 1234
```

This creates combinations containing exactly **4 characters**, using `1`, `2`, `3`, and `4`.

## 6. Using a Character Set

You can choose your own characters:

```bash
crunch 3 3 abc123
```

This creates three-character combinations using only:

```text
a b c 1 2 3
```

The number of possible combinations can become very large very quickly.

## 7. Useful Option: `-t`

The `-t` option lets you create a **pattern**.

For example:

```bash
crunch 6 6 -t @@1234
```

Here, `@` represents lowercase letters. This creates six-character patterns where the first two characters are lowercase letters and the remaining characters are `1234`.

Crunch supports several pattern symbols, including:

- `@` — lowercase letters
- `,` — uppercase letters
- `%` — numbers
- `^` — symbols


### Quick Reference

|Command|Purpose|
|---|---|
|`crunch 2 3 abc`|Generate 2–3 character combinations|
|`crunch 4 4 1234`|Generate exactly 4-character combinations|
|`crunch 2 3 abc -o words.txt`|Save output to a file|
|`crunch 6 6 -t @@1234`|Generate values using a pattern|
|`crunch -h`|Show help|
|`man crunch`|Open the manual|

**In short:** Crunch is a simple but powerful tool for creating custom wordlists. The most important skill is understanding how the chosen **length and character set affect the size of the generated list**.

---

# Crunch — Essential Flags and Examples

## 1. `-o` — Save Output to a File

Use `-o` when you want to save the generated wordlist.

```bash
crunch 2 3 abc -o words.txt
```

The results are saved in:

```text
words.txt
```

You can then view them with:

```bash
cat words.txt
```

---

## 2. `-p` — Permutations

`-p` creates permutations from the words or characters you provide.

Example:

```bash
crunch 1 1 -p red blue green
```

This can generate combinations based on:

```text
red
blue
green
```

and their different arrangements.

### Important

When using `-p`, you normally **do not use the minimum/maximum length or character-set arguments in the usual way**. Crunch calculates the resulting combinations from the supplied strings.

For example:

```bash
crunch 1 1 -p cat dog
```

can produce:

```text
catdog
dogcat
```

This makes `-p` useful when you want to combine known words rather than generate every character combination.

---

## 3. `-t` — Use a Pattern

The `-t` option lets you describe the structure of the generated strings.

Example:

```bash
crunch 6 6 -t @@%%%%
```

Crunch uses special symbols to represent different types of characters.

Common pattern symbols are:

|Symbol|Meaning|
|---|---|
|`@`|lowercase letters|
|`,`|uppercase letters|
|`%`|numbers|
|`^`|symbols|

For example:

```bash
crunch 6 6 -t @@%%%%
```

means:

```text
2 lowercase letters + 4 numbers
```

Possible results could look like:

```text
ab1234
xy5678
```

---

## 4. `-f` — Use a Character Set File

`-f` allows Crunch to use a predefined character set.

Example:

```bash
crunch 4 4 -f /usr/share/crunch/charset.lst
```

Kali normally includes character-set definitions in the Crunch directory.

You can first check what is available:

```bash
ls /usr/share/crunch/
```

This is useful when you do not want to manually type all the characters.

---

## 5. `-s` — Start From a Specific Combination

`-s` tells Crunch where to start generating output.

Example:

```bash
crunch 2 2 abc -s ba
```

Instead of starting from the beginning, Crunch starts at:

```text
ba
```

This can be useful when a previous generation was interrupted and you want to continue from a particular point.

---

## 6. `-e` — Stop at a Specific Combination

`-e` tells Crunch where to stop.

Example:

```bash
crunch 2 2 abc -e cb
```

Crunch stops when it reaches the specified ending combination.

You can combine `-s` and `-e` to generate only a particular section.

---

## 7. `-z` — Compress the Output

`-z` allows Crunch to compress the generated output.

For example:

```bash
crunch 2 3 abc -o words.txt.gz -z gzip
```

This creates a gzip-compressed file.

Other compression types may be available depending on your Crunch version.

Check:

```bash
crunch -h
```

---

## 8. `-c` — Number of Lines per File

`-c` lets you split the generated wordlist into multiple files based on the number of lines.

Example:

```bash
crunch 2 3 abc -c 100 -o words.txt
```

This tells Crunch to create files containing up to **100 lines each**.

This is useful when the complete wordlist is too large to keep in one file.

---

## 9. `-b` — Split by File Size

`-b` can split the output based on file size.

Example:

```bash
crunch 2 5 abcdef -b 1mb -o words.txt
```

This is useful for very large wordlists.

The exact syntax for supported size units can vary, so check:

```bash
crunch -h
```

---

## 10. `-d` — Limit Repeated Characters

The `-d` option can limit the number of repeated characters.

For example:

```bash
crunch 4 4 abc -d 2
```

The exact behavior depends on the repeat/combination rule being used.

This option is useful when you want to avoid excessive repeated characters.

---

## 11. `-r` — Resume an Interrupted Generation

If Crunch stops while generating a large wordlist, `-r` can be used to resume generation.

Example:

```bash
crunch 4 6 abcdef -o words.txt -r
```

This is particularly useful for large jobs that take a long time.

---

## 12. `-q` — Read Strings From a File

`-q` allows Crunch to read strings from a file instead of directly specifying them.

Example:

```bash
crunch 1 1 -q words.txt
```

If `words.txt` contains:

```text
hello
world
admin
```

Crunch can use those strings as its input.

This is useful when you already have a list of words you want to work with.


---

# Most Useful Options at a Glance

|Option|Purpose|
|---|---|
|`-o`|Save output to a file|
|`-p`|Create permutations from supplied strings|
|`-t`|Create a pattern|
|`-f`|Use a character-set file|
|`-s`|Start at a specific combination|
|`-e`|Stop at a specific combination|
|`-c`|Split output by number of lines|
|`-b`|Split output by file size|
|`-z`|Compress output|
|`-r`|Resume generation|
|`-l`|Change pattern symbols|
|`-q`|Read strings from a file|
|`-d`|Control repeated characters|

---
