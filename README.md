# CS 46B Lab 12 – Baggins Family Tree + git/GitHub

A Java tree that models the Baggins hobbit family tree, built while practicing
git and GitHub.

## Project layout

```
lab12/
├── .gitignore
├── BagginsFamilyTree.txt      # input data: parent:child1,child2,...
├── lab12.jar                  # runnable jar (Main-Class: tree.FamilyTree)
├── README.md
└── src/
    ├── App.java               # VS Code template (unused)
    └── tree/
        ├── FamilyTree.java    # FamilyTree + nested TreeNode class
        └── TreeException.java
```

## Running

```
java -jar lab12.jar
```

A file chooser opens. Pick `BagginsFamilyTree.txt`. The program prints the tree
and the most recent common ancestor of Bilbo and Frodo.

The jar holds the compiled classes (Java 11 bytecode, so Java 11 or newer
runs it) and the `.java` sources.

### Program output

```
Tree:
Family Tree:

Balbo
  Mungo
    Bungo
      Bilbo
    Belba
    Longo
      Otho
        Lotho
    Linda
    Bingo
      Falco
        Poppy
  Pansy
  Ponto
    Rosa
    Polo
      Posco
        Ponto2
          Angelica
        Porto
        Peony
      Prisca
  Largo
    Fosco
      Dora
      Drogo
        Frodo
      Dudo
        Daisy
  Lily

**************

Most recent common ancestor of Bilbo and Frodo is Balbo
```

**Did `main()` find the right ancestor?** Yes. Bilbo's ancestors, most recent
first, are Bungo, Mungo, Balbo. Frodo's are Drogo, Fosco, Largo, Balbo. The
first name the two lists share is **Balbo**.

---

## git commands run and their output

Each command below appears in the order the lab gave it, with the output it
actually produced.

> **Note on commit messages:** every commit made for this lab also has a
> `Co-Authored-By:` trailer line added after the message shown. The first line
> of each message is exactly what the lab asked for.

### Setting up git

#### Step 1 – Install git

```
$ git --version
git version 2.39.5 (Apple Git-154)
```

git was already installed (Apple's git ships with the Xcode Command Line Tools).

#### Step 2 – Tell git who you are

`git config --global user.name` and `user.email` were already set before this lab:

```
$ git config user.name
<smerasharma00>
$ git config user.email
<smerasharma00@gmail.com>
```

> ⚠️ Both values still contain the literal `<` and `>` from the lab's
> placeholder. They should be set without the angle brackets:
> `git config --global user.name "smerasharma00"` and
> `git config --global user.email "smerasharma00@gmail.com"`.

#### Step 3 – Authentication with HTTPS (`gh`)

**Not done.** `brew` is not installed on this Mac (`brew not found`), and
installing it needs an interactive sudo password. Also, `gh auth login` is an
interactive browser login. Both need to be done by hand.

#### Step 4 – Authentication with SSH

```
$ ls ~/.ssh
id_ed25519
id_ed25519.pub
```

An SSH key already existed. It's an ed25519 key, not `id_rsa`, but it works the
same way, so no new key was generated. GitHub already had this key. The
first connection asked to trust GitHub's host key (the "say yes" step):

```
$ ssh -T git@github.com
Warning: Permanently added 'github.com' (ED25519) to the list of known hosts.
Hi smerasharma00-sudo! You've successfully authenticated, but GitHub does not provide shell access.
```

#### Step 5 – Create a repository

The GitHub repository already existed:
`git@github.com:smerasharma00-sudo/first-repo.git`. GitHub created it with an
initial commit containing a `README.md` and a Java `.gitignore`.

### Setting up your git repository

#### Step 1 – Create a `.gitignore`

```
$ touch .gitignore
```
(no output)

#### Step 2 – Play with git

```
$ git init
Initialized empty Git repository in /Users/smerasharma/first-repo/lab12/.git/
```

```
$ git status
On branch main

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	.gitignore
	.vscode/
	BagginsFamilyTree.txt
	README.md
	src/

nothing added to commit but untracked files present (use "git add" to track)
```

```
$ git add .gitignore src
```
(no output — this **stages** the files)

```
$ git status
On branch main

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   .gitignore
	new file:   src/App.java
	new file:   src/tree/FamilyTree.java
	new file:   src/tree/TreeException.java

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	.vscode/
	BagginsFamilyTree.txt
	README.md
```

```
$ git commit -m "Initial commit"
[main (root-commit) 52f0779] Initial commit
 4 files changed, 195 insertions(+)
 create mode 100644 .gitignore
 create mode 100644 src/App.java
 create mode 100644 src/tree/FamilyTree.java
 create mode 100644 src/tree/TreeException.java
```

```
$ git status
On branch main
Untracked files:
  (use "git add <file>..." to include in what will be committed)
	.vscode/
	BagginsFamilyTree.txt
	README.md

nothing added to commit but untracked files present (use "git add" to track)
```

#### Step 3 – Complete `TreeException.java`

`???` was replaced with `Exception`, and the constructor calls `super(s);`.

#### Step 4 – Store your files in the GitHub repo

```
$ git status
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   src/tree/TreeException.java

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	.vscode/
	BagginsFamilyTree.txt
	README.md

no changes added to commit (use "git add" and/or "git commit -a")
```

```
$ git add src/tree/TreeException.java
$ git commit -m "Complete TreeException"
[main 25ad7ee] Complete TreeException
 1 file changed, 2 insertions(+), 1 deletion(-)
```

```
$ git push
fatal: No configured push destination.
Either specify the URL from the command-line or configure a remote repository using

    git remote add <name> <url>

and then push using the remote name

    git push <name>
```

```
$ git remote add origin git@github.com:smerasharma00-sudo/first-repo.git
```
(no output; SSH URL used)

```
$ git push
fatal: The current branch main has no upstream branch.
To push the current branch and set the remote as upstream, use

    git push --set-upstream origin main

To have this happen automatically for branches without a tracking
upstream, see 'push.autoSetupRemote' in 'git help config'.
```

```
$ git push -u origin main
To github.com:smerasharma00-sudo/first-repo.git
 ! [rejected]        main -> main (fetch first)
error: failed to push some refs to 'github.com:smerasharma00-sudo/first-repo.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. ...
```

The push was rejected because the GitHub repo already had its own "Initial
commit" (README + `.gitignore`), and the local repo had a separate history.
The fix was to pull it in and merge the two histories. Nothing was
force-pushed:

```
$ git pull origin main --allow-unrelated-histories --no-rebase
From github.com:smerasharma00-sudo/first-repo
 * branch            main       -> FETCH_HEAD
 * [new branch]      main       -> origin/main
Auto-merging .gitignore
Merge made by the 'ort' strategy.
 .gitignore | 24 ++++++++++++++++++++++++
 README.md  |  2 ++
 2 files changed, 26 insertions(+)
 create mode 100644 README.md
```

```
$ git push -u origin main
To github.com:smerasharma00-sudo/first-repo.git
   4baad04..336430c  main -> main
branch 'main' set up to track 'origin/main'.
```

**What happened?** The repository page on GitHub now shows `src/` with both
Java files and the commit history.

### TreeNode class – Step 2: Commit your changes

`addChild`, `getNodeWithName`, and `collectAncestorsToList` were completed.

```
$ git pull
Already up to date.

$ git commit -am "update TreeNode class"
[main dcc7eab] update TreeNode class
 1 file changed, 12 insertions(+), 2 deletions(-)

$ git push
To github.com:smerasharma00-sudo/first-repo.git
   336430c..dcc7eab  main -> main
```

**What happened?** GitHub shows the new "update TreeNode class" commit and the
updated `FamilyTree.java`.

### Finishing FamilyTree.java + Add your changes to GitHub

The constructor, `addLine`, and `getMostRecentCommonAncestor` were completed.
There was no partner for this run, so this part was done in this repo instead
of a cloned partner repo.

```
$ git pull
Already up to date.

$ git status
On branch main
Your branch is up to date with 'origin/main'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   src/tree/FamilyTree.java

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	.vscode/
	BagginsFamilyTree.txt

no changes added to commit (use "git add" and/or "git commit -a")

$ git commit -am "Finish FamilyTree constructor, addLine, getMostRecentCommonAncestor"
[main 4c4423f] Finish FamilyTree constructor, addLine, getMostRecentCommonAncestor
 1 file changed, 20 insertions(+), 22 deletions(-)

$ git push
To github.com:smerasharma00-sudo/first-repo.git
   dcc7eab..4c4423f  main -> main

$ git pull
Already up to date.
```

**What happens on `git pull`?** "Already up to date." No one else has pushed
anything, so there is nothing new to download.

### Final commit (jar, data file, README)

The final commit adds `lab12.jar`, `BagginsFamilyTree.txt`, `.vscode/`, and
this README. The `.gitignore` from GitHub ignores `*.jar`, so the jar was added
with `git add -f`. This README can't contain the output of the commit that
adds it, so that commit isn't shown here; it's visible in `git log` and on
GitHub.

---

## Lab steps not completed

| Step | Why |
|---|---|
| Install `brew` / `gh`, `gh auth login` (HTTPS) | `brew` is not installed; installing it and logging in to `gh` both need interactive input |
| Add a partner as a collaborator; `git clone` the partner's repo | No partner available. `FamilyTree` was finished in this repo instead |
| Bonus (generic `TreeNode<T>`, custom family trees) | Optional, so it was not done |
| Repo name `lab11` / private | The existing GitHub repo `first-repo` was used. Its visibility was not checked |
