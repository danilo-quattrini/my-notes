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
# Reference
---
Book: https://git-scm.com/book/it/v2 

