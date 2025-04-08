2025-02-15 19:29

Status: #baby 

Tags: [[Programming]] [[Programming Knowledge]] [[Web Programming]]

---
# Index
---

# What is Git ?
---
*Git* viene considerato come il più famoso [[Programming Knowledge#VCS (Version Control System)|VCS]] (Version Control System), utilizzato da tutti i programmatori, sia quando lavorano in team, sia quando devono svolgere dei lavori per conto loro.

Lavorare con *Git* e il tuo codice si possono paragonare hai progressi di un videogame, semplicemente cominciamo con una versione di base, che in questo caso sarà l'inizio del gioco, fino a dover salvare ripetutamente gli stati/livelli del gioco in cui vogliamo che un determinato momento venga memorizzato. 

# Git main commands
--- 
Ogni comando che andremmo a vedere avrà bisogno prima di tutto di inserire il prefisso `git <comando della lista>` non va scritto da solo.

`clone <url>`: Il comando che viene accompagnato con l'url della repository che si vuole salvare in una cartella nella nostra macchina in locale (semplicemente salvare nel PC)

In the case that you want to create your first project, in a existing repository that you create you can use this command:
```
$ git init
```
In this part of the project, you didn't do, nothing yet, but you can add in your staging area the first files, in this case we say that we have a file named `README.MD`, so the command that we need to use for add this file in the staging are is this one.

```
git add README.md

or in general

git add <file name> or for add all the project just add the dot .
```

Right now we put our file inside the staging area (the red one), it's mean that we did not still save them yet in the history, for do that, we are going to use the command.
```
$ git commit -m "message you want to write"
```
You can either use code for doing that just write the same command without the message ad the -m.
```
$ git commit
```

To contribute or clone a repository locally you can do that by using the command:
```
$ git clone <url>
```
for example if we need to copy the `libgit2` repository locally, we have two ways to do that:
1. `git clone https://github.com/libgit2/libgit2` after the command in your PC we are going to have the directory libgit2, but if we want to save into another directory.
2. `git clone https://github.com/libgit2/libgit2 <directory name>` We are going to put the name of the new directory that is going to create it automatically.

The new command we are going to see rnw, is necessary to see if a file that we created is staged or not.
```console
$ git status
```
We are going to see if there is any file inside your directory that we didn't stage them, that's mean, the file we created is new from the previous commit we did, so in the first case, we clone the directory, and we find that all the file are staged.
```console
$ git status
On branch master
nothing to commit, working directory clean
```
If we create a new file inside the working repository, for example a LICENSE, we find out after doing the same command we did before, that something change.
```console
$ echo 'My Project' > LICENSE
$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)

    LICENSE

nothing added to commit but untracked files present (use "git add" to track)
```
Git says to us that there is a new file in the working directory, that need to be stage, this is useful because whenever we want, we can decide if we want to include or not a new file we created, without being unaware.

![[Pasted image 20250318184720.png]]
In case you want to add the file in the next snapshot (commit), you can use this command to add the file inside the next snapshot.
```console
git add LICENSE
```
after you did this command now you add the file in the staged area (the orange one), when you are going to run again the command.
```console
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    new file:   LICENSE

```
Now your file is sure to be include in the next commit; for add multiple file inside the next commit you can use the same command but in this case you are going to include the dot `git add .`

There is a short way to see the status of the files inside the git repo, in this case you just need to add the `--short` or the easier way is the `-s`, now we are going to analyze each part.
```console 
$ git status -s
 M README
MM Rakefile
A  lib/git.rb
M  lib/simplegit.rb
?? LICENSE.txt
```

>[!quote] **Legenda**
>- ?? means that the file is untracked and is new inside the directory
>- A means that the file have been added to the stage area
>- M means that the file was modified.
>

There are two columns, the left hand column indicate that the file is staged, the right hand column indicate that is modified (edited from the previous commit) and not staged.

Previously we have been working with `git status` to saw which files have been saved in the staging area or no, but we don't know which type of changes we made, for this reason, we use `git diff` that helps us to know what did we do before.

Let's say for example we made a change inside the file `CONTRIBUTING.md`
```
$ git diff 
diff --git a/CONTRIBUTING.md b/CONTRIBUTING.md
index 8ebb991..643e24f 100644
--- a/CONTRIBUTING.md
+++ b/CONTRIBUTING.md
@@ -65,7 +65,8 @@ branch directly, things can get messy.
 Please include a nice description of your changes when you submit your PR;
 if we have to read the whole diff to figure out why you're contributing
 in the first place, you're less likely to get feedback and have your change
-merged in.
+merged in. Also, split your changes into comprehensive chunks if you patch is
+longer than a dozen lines.

 If you are starting to work on a particular area, feel free to submit a PR
 that highlights your work in progress (and note in the PR title that it's
```
With this command we have a (short) vision of  what did inside the file, whereas before with just the `git status` we were not able to see what we did previously.

Furthermore if we want to see which changes we made in the staged area, we can use the same prompt, but we just add the `--staged` flag
# .gitignore

The `.gitignore` is a default file, that's used to ignore (like the name says) in the staging area, the directory/files that are written inside of it, following a specific pattern.

Let's see an example of it.
```console
$ nano .gitignore

what you are going to write inside the .gitingore file:

> *.[oa]
> npm/*
> gradle/
> *~
```

In the first line all the file that ends with `.a` or `.o` are going to be ignored, these one are the acronymous of archive and object, used to build your code, in the next one all the file inside the directory `npm/` will be discard too, either the `gradle/` one, the last one is only for the [Emacs](https://en.wikipedia.org/wiki/Emacs) text editors where they save temporary file inside the directory. 

There are different type of pattern that are important to remember.
>[!info] **Pattern to remember**
>- `*` the asterisk means that includes zero or more characters.
>- `[abc]` match all the character inside the bracket (in this case is a, b, c).
>- The question mark `?` means that is going to match a single character.
>- Square brackets within numbers separate by the [[Programming Knowledge#^860ddc|hypen]] like this `[0-9]` means that we are any character between them (in this case 0 though 9)

Here there others example of others lines of `.gitignore`
```
# no .a files
*.a

# but do track lib.a, even though you're ignoring .a files above
!lib.a

# only ignore the root TODO file, not subdir/TODO
/TODO

# ignore all files in the build/ directory
build/

# ignore doc/notes.txt, but not doc/server/arch.txt
doc/*.txt

# ignore all .txt files in the doc/ directory
doc/**/*.txt
```

# Branching

To see all the branches that you have in the project, you should use this command:
```console
$ git branch -a 
```


# Reference
---
Book: https://git-scm.com/book/it/v2 

[^1]: hype
