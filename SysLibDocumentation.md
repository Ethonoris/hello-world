# Documentation for Systems Librarianship Spring 2024

Here is where all the documentation for what we learn in this class will go. I will continue to add to this with each 
week as we learn and notes will be displayed and updated accordingly. 

### Week 1: 

- We created our **Google Cloud** accounts and a new *virtual machine* instance.
- The instance uses **Ubuntu** as its OS, and the **Gcloud SDK Shell** for its *command line*.[^1]
- We also created a *snapshot* of the instance before anything serious can be done with it, just in case it needs to be reset. 

### Week 2: 

- We learned how to set up a **GitHub** account and create a new *repository*.[^2]
- Additionally, we learned about **Markdown syntax**. I've demonstrated my knowledge of Markdown in the updated [readme file](https://github.com/Ethonoris/hello-world/blob/master/README.md) for this repository.
- From now on, each week's notes will be in Markdown complete with lists or tables.
- **Bold** text is reserved for headers and important technologies referenced in class. *Italicized* text is reserved for important terminology.
- Footnotes, images, links, and more will be provided where appropriate.[^3]

### Week 3: 

- The two ways a computer is typically used are via a *Graphical User Interface* or *GUI* and the less common, *Command Line Interface* or *CLI.*
- A GUI is primarily focused on interactions that aren't text based, while a CLI is mostly made up of text based interactions.[^4]
- A command line used with **Linux** is called a *Shell*. This is technically both a *command language* as well as a type of *scripting language*.
- The command language we're using right now is called **Bash**. A list of basic commands for Linux Shell's like Bash are as follows:

![CLI Commands](https://github.com/Ethonoris/hello-world/assets/44278023/d493020c-fce1-4880-8378-c3649fbc162d)

See caption[^5]

### Week 4: 

- **Nano** is a text editor that runs within the command line and is considered user friendly due to being *modeless*.[^6]
- Shortcuts primarily make use of the control key and other letters in order to save, cut, copy, paste, etc.
- I find using the alt key with most of the M commands, such as M-6, to be most convenient so far.
- A nanorc file can be used to configure settings for Nano, including colors, line numbers, and cursor position logging.
- One thing I noticed was that for my first file, Nano wanted to name it `test.txt` and not what I had created it as, `nano text.txt`[^7]
- The following are a few screenshots of my initial test run of Nano:

![nano1](https://github.com/Ethonoris/hello-world/assets/44278023/6d2349cb-a132-413f-879b-799cb0d661e0)

![nano2](https://github.com/Ethonoris/hello-world/assets/44278023/59513869-18f8-4b44-94ca-824e94ba8dfe)

![nano3](https://github.com/Ethonoris/hello-world/assets/44278023/514421ee-9ed2-46b2-889e-4e1bad75cb54)

### Week 5: 

- The **grep** command allows you to search through files for specific text line by line in a given file. The following consists of several grep queries I tested.
- `grep "title" scopus.bib`
  - This command was my attempt at getting grep to return just the titles of the articles in the bibliographic information. However, there are multiple other lines that contain the word title, in particular, the lines with "abbrev_source_title" but we can exclude this though.
 
![Grep1](https://github.com/Ethonoris/hello-world/assets/44278023/0813b410-3cde-4cf8-a1a1-517b29b62343)

- `grep "title" scopus.bib | grep -v "_title"`
  - By using the pipe to include the output of one grep command and another, I can get the result I want. Because both types of line that contain "title" have a space and equal sign after the word "title", I had to exclude the excess by using the invert of "_title" instead. 

![grep2](https://github.com/Ethonoris/hello-world/assets/44278023/f9f9314d-c87a-4438-b5f0-c4a17904381b)

- `grep -A4 "author =" scopus.bib`
  - This allows me to obtain the search line of "author =" and the next four lines after each instance it appears, which are the title, year, journal, and volume for each article. Because articles are the only type that I allowed in my Scopus bibtex file export, this will always return me the desired result.
 
![grep3](https://github.com/Ethonoris/hello-world/assets/44278023/314c6eb7-5c60-4281-bfdb-bc087731e5c4)

- `grep -A4 "author =" scopus.bib > results.txt`
  - I can write the results of a grep search like this one to a text file to save them for later viewing or separate use. The cat command then shows the output from grep in the "results.txt" file.[^8] I can also later view and edit it in Nano, separate from the original scopus.bib file, if I want. 
 
![grep4](https://github.com/Ethonoris/hello-world/assets/44278023/c8be8e08-cfc0-41c9-b541-75c291492ccd)



[^1]: In the command line, the commands to update the VM instance in Ubuntu are 
  `sudo apt update`
  and
  `sudo apt -y upgrade`
[^2]: As per the updated readme file, this account and repository have been revived 
  for the purposes of this course. 
[^3]: Footnotes will be used for additional specification of details, or code and commands not featured in the notes. 
  This may also include captions for images. 
[^4]: There is a trade off here between the requirement for a higher standard of user specificity and a greater degree of user control. The more detail that an interface requires, the more likely that it will perform intended operations accurately, although, this tends to make them inherently less friendly to the lay user.
[^5]: This image of a list of basic CLI commands sourced from [System Librarianship, Version 2](https://cseanburns.github.io/systems-librarianship/p1-systems-librarianship.html) by Sean Burns. 
[^6]: A modeless text editor is one that doesn't need to be switched back and forth between insert mode, to write text, and command mode, to issue commands in the command line. 
[^7]: It asked wheather I wanted to save the file under another name after I had used ctrl-o and then enter, and I haven't been able to replicate that. 
[^8]: The "results.txt" file did not exist prior to me directing the grep results to it. Like with some other commands, directing this output to "results.txt" created that text file. 
