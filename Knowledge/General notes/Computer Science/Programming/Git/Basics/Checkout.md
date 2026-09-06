### How to go back to a previous commit (Checkout)

Here’s the easiest way for a beginner:

#### Step 1: See your history

Open your terminal (or command prompt) in your project folder and type:

Bash

```
git log --oneline
```

You will see something like this:

text

```
a1b2c3f (HEAD -> main) Fixed the login button
d4e5f6g Added the signup page
9h8i7j6 Changed the colors
```

- The top line is your **current** version.
- Each line is an old version (a commit).
- The strange letters+numbers (like a1b2c3f) is the **commit ID**.

#### Step 2: Go back to an older version

Let’s say you want to go back to the version “Changed the colors”.

You copy the commit ID (for example 9h8i7j6) and type:

Bash

```
git checkout 9h8i7j6
```

That’s it!

Now your files will change back to how they looked at that older commit. Git will say “You are in ‘detached HEAD’ state” — don’t worry, that just means you are looking at an old version right now.

#### How to go back to the latest version again

When you want to return to your newest work, just type:

Bash

```
git checkout main
```

(or git checkout master if your main branch is called master)

---