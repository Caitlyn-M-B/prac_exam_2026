notes

# Commands[CB1.1]
Basic command structure & tips:
- ```clear``` - Clears past commands out of the terminal.
- cntrl c - escape
- ' ' Quotes represent a search area. You may get stuck in carrots if you accidentally open a quote without closing it.
- tab - autocomplete. Saves a lot of time and errors. Capitalization matters.
- --help can give information on modifications for commands
- `>`, `>>`, and `|` are different ways of redirecting output.
    - ```|``` sends output to a dfferent command.
    - ```> 'file'``` redirect. Sends information to a place other than printing it to the screen. Added to the end of a grep or other printing command.
    - `command >> file` redirects a command's output to a file without overwriting the existing contents of the file.
- ```*``` to select everything in adirectory

Navigation and file management:
- ```cd 'file'``` - change directories. Type directory name after cd.
    - ```cd ~``` - brings you back to your home directory
    - ```../``` - back up one step in directories
- ```mkdir 'new directory name'``` - make directory
- ```cp 'old file' 'new file name'``` - copy file
- ```mv 'file' 'directory'``` - move file
- ```rm 'file'``` - remove/delete. Careful!
- ```> 'file'``` redirect. Sends information to a place other than printing it to the screen. Added to the end of a grep or other printing command.
- ```history``` - shows entire history of commands

Looking at what you have:
- ```pwd``` - Print Working Directory. Shows open directories. Like a map showing where within the files you're working; gives you the absolute path.
-  ```ls``` - List. Shows all files and folders in working directory.
    - ```ls -lrth``` - shows more information than just the names, shows permissions, users, file size and more.
    - ```--all``` - shows all files, including hidden files.
    - ```ls .*``` - shows hidden files
    - ``` ls -laF``` - show all files in long form with slash and directory format.
    - ```ls -l``` - shows file permissions
    - ```ls -lh``` - shows file permissions, plus in a human readable format, so file sizes are in bites instead of bits.
- ```head 'file'``` - print out first few lines of files to screen. Must specifiy file.
- ```cat 'file'``` - print whole file. Proceed with caution.
- ```grep '@' 'file'``` - searches a file for given text. Must specifiy in quotes what you're looking for and file to look in.
- ```WC``` - shows line, word, and character count
- ```less``` shows some but not all of the content of a file; more of a preview than head.

Gen711/811 Practice Practical 2023 (40 scaled points)[CB2.1]

NAME: Caitlyn Bailey

Instructions:  
- Make sure to paste all the commands that you use below each of the tasks.  
- Some tasks require you to copy your output here. All output that you paste is less than 10 lines.   
- Do not spend too much time on a single prompt. It's important to get to all prompts.    
- If you get stuck and do not know how to proceed: specifically ask for the answer.  
- Help will get you to the next step, but you will lose points for that prompt.  
- Questions on clarification of the question does not result in the loss of points.  
- Replace MYNAME with your first and last name.   
- Download the practical into your gen711/811 folder as indicated at the begining of class. 
- Keep the '.md' extension until you turn it in. 
- Right before you upload it, save it as a '.txt' document MYNAME_practical.txt. 
- Save the document to your lab folder so that you know where it is when you need to upload it.
- Document must be uploaded before 5pm to get credit. 

Hints: 
- Remember, if you want to re-run a command, but change it slightly to try to fix it, hit the up arrow and edit the last command that you ran. 
- When typing out commands, filenames, or paths, hit the tab button a couple time to see if it autocompletes for you

### 1. Paste the command(s) below that you used get practical exam pasted into vscode. (2 point)

ctrl c & ctrl v into a new .md file.

### 2. From your home directory, make a new directory to hold fastq files called 'analysis' (2 points)

```mkdir 'analysis'```

### 3. Copy the fastq files /tmp/gen711_2023/Sample1.fastq and /tmp/gen711_2023/Sample2.fastq directly into the 'analysis' directory without changing your current directory. (2 points, partial credit if you need to change directories first)
For todays practice practical, use SRR fastqs instead

```
cp 'shell_data/untrimmed_fastq/SRR097977.fastq' 'analysis/SRR097977.fastq'
cp 'shell_data/untrimmed_fastq/SRR098026.fastq' 'analysis/SRR098026.fastq'
```

### 4. Use an absolute path to change your current working directory to the 'analysis' folder/directory. (2 points, partial credit for using a relative path)

```cd gen711-811/analysis/```

### 5. The fastq file you just copied is data from the UNH genome center. This is the first time you've ever seen these FASTQs. To confirm that the format of the FASTQs look ok, view one of the two files and paste the top 4 lines of the file below. (4 points) 

```
[cmb1451@ron analysis]$ head SRR097977.fastq
@SRR097977.1 209DTAAXX_Lenski2_1_7:8:3:710:178 length=36
TATTCTGCCATAATGAAATTCGCCACTTGTTAGTGT
+SRR097977.1 209DTAAXX_Lenski2_1_7:8:3:710:178 length=36
CCCCCCCCCCCCCCC>CCCCC7CCCCCCACA?5A5<
```

### 6. You've decided that you want to make a seperate file of the reads to BLAST them at NCBI to make sure they belong to the species that you seqiuenced. However, your blast program is written to accept FASTA files rather than FASTQ files (FASTA files only contain the header line above the read, and the read itself). You will need to make a 'FASTA' file from each FASTQ file. Before you make the new files, pipe the output to a command that that allows you to see just the first lines of the output. (5 points)  

To preview:
```grep -A1 --no-group-separator '@SRR' SRR097977.fastq```

To make file:
```grep -A1 --no-group-separator '@SRR' SRR097977.fastq > SRR097977.fasta```

```grep -A1 --no-group-separator '@SRR' SRR098026.fastq > SRR098026.fasta```

#### Hints: 
### FASTA only needs 2/4 lines that are in a FASTQ: 1) the header line that starts with '@' and 2) the sequence right after the header. However, the base call quality scores could contain '@' as well, which might lead to unwanted matches. 
### You can use the info in the header line to be very specific about what you are trying to match. 
### Add the '--no-group-separator' option to the other options of your command to keep the '--' out of the output

### 7. Redirect the output of your command (command in 6 that is converting the format of the FASTQ into FASTA) into new files. Give the new file the same names, but uses the '.fasta' extension rather than the '.fastq' extension of the original file name. (5 points)

I did that already

### 8. How many reads have 15 or more uncalled bases (NNNNNNNNNNNNNNN) in both samples? Count the number of reads in both WITHOUT making a new file. (4 points)

```
grep 'NNNNNNNNNNNNNNN' *.fasta | wc
    100     100    5200
```

### 9. Make a new directory called 'to_blast' in your current directory. Then, move the two fasta files into this new 'to_blast' directory (4 points)

```
mkdir 'to_blast'
mv *.fasta to_blast/
```

### 10. Without changing directories, what command could you use to confirm that the files made it into the 'to_blast' folder. (2 points)

ls, and check for the absence of the files moved. 

### 11. What is the 100th line in the Sample1.fasta file? (hint: the 'head' command is one way to do this- but you may need to specify an option) (2 points)

```head -100 SRR097977.fasta```
...100 lines later...
```GCGGAGCTGGTGATTGGCGAACTGCTGCTGCTATTT```

### 12. Run md5sum on Sample1.fasta (md5sum Sample1.fasta). Then, run it again, but redirect the output to a new file called 'my_md5sums.txt'.  (2 points)

```md5sum SRR097977.fasta > my_md5sums.txt```

### 13. Next, run the md5sum command on Sample2.fasta and add it the the end of 'my_md5sums.txt'. (2 points)

```md5sum SRR098026.fasta >> my_md5sums.txt```

### 14. Lastly, add your name to the end of 'my_md5sums.txt' file. (2 points)

```echo 'Caitlyn Bailey' >> my_md5sums.txt```
