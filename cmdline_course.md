---
layout: default
---

![Command Line Tool](https://imgs.xkcd.com/comics/tar_2x.png)  

# **Introduction**

Command-Line Tools for Linguists introduces students to essential command-line skills for linguistics, enabling them to navigate UNIX environments, process text data, run programs and write basic scripts. It covers basic commands, regular expressions, remote server work,  version control and webpage creating on GitHub Pages. You can visit the course page [here](https://studies.helsinki.fi/courses/course-implementation/hy-opt-cur-2425-261401a1-c550-4436-91b9-7edf4a1a3b57/KIK-LG221).  

The time schedule and the content of this course are shown in the below table:    

|  Time  |  Content                               |
| :----: | :------------------------------------: |
| Week 1 | Introduction to Command Line Environments |
| Week 2 | Navigating a UNIX system               |
| Week 3 | Basic Corpus Processing                |
| Week 4 | Advanced Corpus Processing             |
| Week 5 | Scripting and Configuration Files      |
| Week 6 | Installing and Running Programs        |
| Week 7 | Version Control                        |
| Week 8 | Jekyll, GitHub Pages and Final Project | 

## **Week 1: Introduction to Command Line Environments**  

In the first week, the course will begin by demonstrating how to set up the command line environment in Ubuntu. After that, it will cover how to list the contents of the current directory, how to retrieve files from the Internet, how to create, remove, copy, rename, and move files, and how to open and edit text files using **Nano**.  

I have learned many useful basic commands, such as, `ls`, `cd`, `mv`, `rm`, `pwd`, etc.  For example: 

```bash
wget https://www.gutenberg.org/cache/epub/74661/pg74661.txt
```
This command will download a plain text from [Gutenberg](https://www.gutenberg.org/).  

```bash
cd KIK-LG221/
```
This command will change the current working directory to **KIK-LG221** directory.   

```bash
less life_of_bees.txt
```
This command will show the contents of **life_of_bees.txt** only in one page at a time.

## **Week 2: Navigating a UNlX system**

In this week, the course will first introduce the UNIX file system. Next, it will cover the basics of processes and process management in the command line. Finally, we will learn how to connect to and work on a remote server, specifically using the remote server provided by [**CSC**](https://csc.fi/) in Finland.  

Here're the specific topics covered in this week's course:
 * how to copy, move and delete a directory
 * visit the root directory of the system
 * how to compress a file and a directory using `gzip` and `tar`
 * how to find out and change the read and write permissions for a file
 * find the PID of a process and kill it and run commands in the background
 * how to form a remote connection to a server and copy files to and from a server using `scp`
 
```bash
mkdir homework/
```
This command will create a new directory called **homewrok/** under current working directory. 

```bash
ssh puhti.csc.fi
ssh <username>@puhti.csc.fi
```
Both of these two commands connect us to a Bash program running on the remote server, [**Puhti**](https://www.puhti.csc.fi/public/). If the username on the current computer differs from the username on the remote server, the server's username should be specified in the `ssh` command, as shown in the second example.

```bash
scp KIK-LG219/week1/life_of_bee.txt puhti:~
```
This command will copy **life_of_bees.txt** from our local computer to the remote server, [**Puhti**](https://www.puhti.csc.fi/public/).

## **Week 3: Basic Corpus Processing**

In the third week, we focus on basic corpus processing, divided into two parts. In the first part, we cover different character encodings and commands for processing and searching within text files. In the second part, we learn about structured text files and the specific commands used to process them.  

In this week, I've learned the following:
  1. The difference between the ASCII, Latin-1 and utf-8 encoding systems
  2. the concept of regular expressions and how they work
  3. `grep` command (global regular expression print)
  4. how to count the number of lines, words and characters in a text file
  5. how to search for patterns in files

```bash
dos2unix katinka_rabe.utf-8.txt.
```
This command converts the file **katinka_rabe.utf-8.txt** from DOS/Windows format to Unix format.

```bash
egrep "\b[a-z]*ss\b" life_of_bee.txt
```
This command searches for a pattern in **life_of_bee.txt** that begins with any number of lowercase letters, contains the sequence **"ss"**, and is bounded by word boundaries.

```bash
wc -l languages.csv
```
This command counts the number of lines in the file **languages.csv**

## **Week 4: Advanced Corpus Processing**

In the fourth week, we will learn to combine simple commands into more complex command pipelines which allows you to easily perform quite complex operations on text files without generating a lot of intermediate files. The other major theme of this week is the `sed` command which is used to transform text files.  

In this course, I've learned how to use `sed` to find and replace patterns in a file. And also I am able to use regular expressions with `sed`. Furthermore, I've learned text processing pipelines.  

![Corpus Processing](https://imgs.xkcd.com/comics/regular_expressions.png)  

```bash
sed -nE 's/that/which/gp' ulysses.txt
```
The command will search for the word **"that"** in the file **ulysses.txt** and replace it with **"which"**. And it will finally print out modified lines.

```bash
cat life_of_bee.sent | sed -E "s/^/# /" | sed -E "s/$/ #/" | sed -E "s/([a-ZA-Z])([;:,.?!])/1 \2/g" | tr -s"[:space:]""\n" > life_of_bee.unigram
```
This command processes the contents of the file **life_of_bee.sent** into a unigram list.

## **Week 5: Scripting and Configuration Files**

In the fifth week, we are putting together our commands in tidy **"scripts"** instead of typing them one by one. We will be creating some scripts for ourselves to solve some complex problems. Later on, we will also learn about the concept of environment variables in UNIX systems, and set up a configuration file for ourselves to keep these settings.  

```bash
#!/bin/bash
cat $1 |
dos2unix | 
tr -s "[:space:]" "\n" | 
tr -d "[:punct:]" | 
sort | 
uniq -c | 
sort -nr > $2
```
This is a **script**. It processes an input text by converting it to Unix format, splitting it into words, removing punctuation, counting the occurrences of each unique word, and then sorting those counts in descending order. Finally, it writes the file to another specified output file. 

```bash
PS1="\n ${RED}\w\n ${BROWN}[\t] ${BLUE}\h :) ${COLOR_NONE}"
```
This command sets the value of the PS1 variable. Prompt configuration will display the current working directory in red, the current time in brown, and the hostname in blue, ending with a smiley face. 

```bash
echo $PATH
```
This command displays the current value of the **PATH** environment variable in the terminal. 

## **Week 6: Installing and Running Programs**

In this week, we will first focus on installing programs and package manager. Package management tools help manage these dependencies, allowing users to install programs with a simple command. In the second part of the week, we will explore `make`, a utility that automates the building of projects and running of scripts on files, streamlining entire workflows.

In this course, I've grasped how to install softwares and python modules. In addition, I've learned how to write and use **Makefile**.

```bash
sudo apt-get install imagemagick
```
This command will help install [**ImageMagick**](https://imagemagick.org/) software. 

```bash
pip install nltk
```
`pip` is Python's package manager. This command will help install nltk module. 

```bash
results/%.freq.txt:data/%.no_md.txt
	src/freqlist.sh $< $@
```
This is a `make` rule. It will create files in **results/** directory with the **.freq.txt** suffix from a corresponding file in **data/** directory that has the **.no_md.txt** suffix, using the **freqlist.sh** script to perform the transformation.

## **Week 7: Version Control**

In the seventh week, we will learn about version control. We'll be introduced to **Git**, one of the most widely used and flexible version control systems today, as well as [**GitHub**](https://github.com/), a widely used platform providing Git support.  

![Version Control](https://imgs.xkcd.com/comics/git_commit_2x.png)  

In this course, I've learned how to add files to my local repository, commit these changes, and push the changes to my global repository in Github.

```bash
git clone https://github.com/aojieyin/cmdline-course .
```
This command will clone the remote repository **cmdline-course** from [GitHub](https://github.com/aojieyin/cmdline-course) to the local computer in the current working directory.

```bash
git add -A
```
The command will stage all changes in the current repository for the next commit.

```bash
git push origin master
```
This command will upload local changes from the master branch to the remote repository.

## **Week 8: Jekyll, GitHub Pages and Final Project**

In the last week, we will learn how to use Jekyll to build a website. Based on this, we will build our own website and publish it on GitHub pages.  

In this course, I've learned how to write Markdown documents and use Jekyll to build a website.

```markdown
# H1
## H2
### H3
#### H4
```
This shows how to write headers in Markdown.

```markdown
[I'm an inline-style link](https://www.google.com)
```
This shows how to write an inline link in Markdown.

