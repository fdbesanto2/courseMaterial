Before the course
-----------------

Prerequisites:
-   you have used a computer before and you are know what are "files"
    and "directories" (also called "folders") on a computer

After the course
----------------

You will know how to:
-   connect to a remote server
-   navigate around files and folders from the command line
-   create, copy, move and delete files and folders
-   run programs from the command line
-   combine commands to perform complex operations
-   create scripts to automate tasks

Introducing the shell
=====================

What is the shell?
------------------

![](images/shell-screenshot.png)

In brief:
-   Command-line interface, looks old-fashioned but very convenient
-   Main interface when you want to login to **remote servers** (e.g.
    CSC servers, workstation)
-   Also present in **Linux** distributions for personal computers and
    **Macs**
-   With **Windows**, the `cmd` prompt is a bit similar (text-based) but
    not as powerful

Usage:
-   Often the only interface for remote connections
-   Powerful built-in commands
-   **Automate repetitive tasks**
-   Shell scripts to **reproduce** data manipulation

Where can we find the shell?
----------------------------

To find a shell:
-   On **GNU/Linux** and **MacOS** systems: open a **terminal**. This
    will provide you with a Unix-like shell on both systems.
-   On **Windows**: run `cmd.exe` or `cmd`. This shell is quite
    different from the Unix-like shell found in Linux and MacOS. To
    obtain a Unix shell on Windows, one can install the Cygwin tools.
-   It is strongly recommended to learn how to use a **Unix shell** (the
    most likely to be installed on a **remote server**).

### One shell or several shells?

-   A shell: a program providing an **interface** between the user and
    the computer. **Different shells exist**.
-   The most popular and widely used shell is probably **bash**. It is
    the default shell in most GNU/Linux distributions.
-   If you learn how to use **bash**, you will be able to use most
    **remote servers** you'll have to connect to, and also the
    **terminal** from MacOS or the **Cygwin** tools on Windows.

\*One word on terminology\*: During the course, we will often say
interchangeably "the terminal", "the console", "the shell" or "bash".

The CSC center in Kajaani
-------------------------

![](images/digitice-csc-kajaani-800_ilmakuva_tehtaasta.jpg)

Meet the Taito cluster (`taito.csc.fi`)
---------------------------------------

![](images/yle-taito-supertietokone-kajaani.jpg)

Meet bio109-113 (130.234.109.113)
---------------------------------

![](images/workstation.png)

-   Today, we are going to connect to a remote workstation on the other
    side of the lake: `bio109-113`.
-   Runs a GNU/Linux system
-   Provides a **bash** shell (similar to **Taito**)

Hands-on practice
=================

1. Connection to a remote shell
-------------------------------

The plan:
-   Use our workstation in Ambiotica (student accounts were created on
    this server)
-   Tools: **putty** (Windows) or **ssh** (Mac and GNU/Linux)
-   A word about **ssh** and the **security of connections**

### 1.1 How to use ssh?

-   `ssh` syntax:

    ``` {.bash}
    ssh username@host
    ```

-   `username` - this is your identifier on the host machine:
    -   `matthieu`
    -   `matthieuBruneaux`
    -   `mabrunea`
    -   `jyybio48`
-   `host` - this is the address of the machine you are connecting to:
    -   `taito.csc.fi`
    -   `130.234.109.113`

### 1.2 Connect to your student account

#### Student account:

-   Logins: `jyybio01` to `jyybio25`
-   Password: on the whiteboard!

#### Connection:

-   **Mac or GNU/Linux**: from a terminal

    ``` {.bash}
    ssh jyybioxx@130.234.109.113
    ```

    where `xx` is your student number.

-   **Windows**: using putty. Live demonstration, ask a teacher
    if needed. Remember to tune your putty settings for a better look
    and feel:
    -   **Window** &gt; **Appearance** &gt; Change font to "Deja Vu Sans
        Mono", 11-point
    -   **Window** &gt; **Translation** &gt; Change "Remote character
        set" to UTF-8 (top of the list)
    -   **Window** &gt; **Colours** &gt; Tick "Use system colours"
    -   Save settings if you wish
-   You might be asked to accept the **host RSA key fingerprint**. It
    should be:

        2048 74:55:8b:ad:2d:85:84:74:be:ce:53:da:12:5a:13:32   (RSA)

    (this ensures that you are connecting to the intended host, not to a
    malicious server impersonating the host)

2. First contact with the shell
-------------------------------

### 2.1 Just after connection:

-   What you see after connection is the **shell prompt**. It tells you
    the shell is ready to receive your input:

    ``` {.example}
    jyybioxx@bio109-113$
    ```

-   `jyybioxx` is your username, `bio109-113` is the host server to
    which you are connected.

### 2.2 Execute a command (`ls`)

-   The shell **reads** and **executes** commands you enter at the
    prompt, and **prints** the output.
-   Type:

    ``` {.bash}
    ls
    ```

    and press `RETURN`. You should see:

    ``` {.example}
    practicals  readme
    ```

-   You just ran the `ls` command which produces an output: the list of
    files and folders present in the current directory.
-   Try another command:

    ``` {.bash}
    whoami
    ```

    What does this command do?

\*Important note\*: Do **not** copy-paste the commands from the course
material to your terminal! You will get a much better feeling for the
shell if you type the commands yourself.

### 2.3 Execute a command (`pwd`)

-   When you login to a server, you are automatically sent to your
    home folder.
-   You can see where you are by typing:

    ``` {.bash}
    pwd
    ```

    which produces:

    ``` {.example}
    /home/jyybioxx
    ```

-   So you are now in the folder `jyybioxx`, which is itself contained
    in `home`, which is at the root of the file system (`/`, there is no
    parent directory above).

3. Adding options to a command
------------------------------

-   You can add options to a command with the dash sign `-`:

    ``` {.bash}
    ls -l
    ```

    (this is `-l` with the letter L, not `-1`)
-   This runs the `ls` command with the `-l` option, which produces a
    detailed output:

    ``` {.example}
    total 4
    drwxr-xr-x. 3 jyybioxx users 23 Nov  9 16:22 practicals
    -rw-r--r--. 1 jyybioxx users 25 Nov  9 16:22 README
    ```

-   Now you can see the date of last modification of the files and some
    other information.

4. A word about rights
----------------------

### 4.1 The rights system

-   In a Unix system, every file has a **owner** and belongs to a
    **group**
-   Every file has rights for **reading**, **writing** and **execution**
-   Those rights are set for three categories of users: **owner**,
    **group** and **others**

### 4.2 `ls -l` output

``` {.example}
total 4
drwxr-xr-x. 3 jyybioxx users 23 Nov  9 16:22 practicals
-rw-r--r--. 1 jyybioxx users 25 Nov  9 16:22 README
```

-   The very first letter for `practicals` row (`d`) means this row is
    a directory. Let's consider the nine following characters
    (`rwx------`)
-   The three first letters are rights for the owner, the next three
    rights for the group, and the last three rights for others.
-   If a letter is replaced by a dash, the right is not granted.
-   What do those mean?

    ``` {.example}
    -rwx------
    -r--r--r--
    -rwxr--r--
    drwxr-xr-x
    ```

5. Basic folder navigation
--------------------------

### 5.1 `cd` command

-   We can navigate from folder to folder using the `cd` command:

    ``` {.bash}
    ls
    cd practicals
    ls
    cd ecoli-data
    ls
    ```

-   You can see there are already some files in this folder. Let’s ask
    for more details with `ls -l`

-   How many files are there? How large are they?

### 5.2 Combining options for `ls`

-   We can ask for more human-readable sizes with:

    ``` {.bash}
    ls -l -h
    ```

-   Can you see the difference with `ls -l`? What does `ls -h` do?

-   We could also combine both options: `ls -lh` . Try it.

### 5.3 Moving to the parent directory

-   We can go back through the parent folders using `cd ..`

    ``` {.bash}
    pwd      # Where are you at this point?
    cd ..
    pwd      # And now?
    ls
    cd ..
    pwd      # And here?
    ls
    cd .. 
    pwd      # And here?
    ls
    ```

### 5.4 Going back to the home directory

-   A faster way to go back to your home directory, from any starting
    directory, is just to type `cd` without any argument:

    ``` {.bash}
    pwd
    cd
    pwd
    ```

-   Go back to the `ecoli-data` subfolder and back again to your home
    directory using `cd`

-   From your home folder, instead of typing `cd practicals` and then
    `cd
     ecoli-data` to go through folder one at a time, we can go directly
    to the subfolder by typing:

    ``` {.bash}
    cd practicals/ecoli-data
    pwd
    ls
    ```

#### Shortcut for the home folder

-   Another way to go to the home folder is to use the `~` character:
    this is automatically replaced by the path to your home folder by
    `bash`.

    ``` {.bash}
    cd              # Back to your home folder
    cd practicals
    cd ~            # Bash understands "~" as "/home/jyybioxx"
    cd ..
    pwd             # Where are you at this stage?
    cd ~/practicals # Where are you now?
    ```

6. Creating folders
-------------------

### 6.1 The `mkdir` command

-   Go to the `practicals` folder and create a new folder in it:

    ``` {.bash}
    cd ~/practicals
    mkdir results
    cd results
    ls
    ```

### 6.2 Exercise

-   Create the following directory structure:

    ``` {.bash}
    ~/practicals/scripts/python/modules/seqAnalysis
    ```

-   Go back to your home folder.

7. Auto-completion
------------------

### 7.1 The magic `TAB` key

-   Let’s go into the `seqAnalysis` folder, but let’s be lazy:

    ``` {.bash}
    cd         # Start from your home folder
    cd pr      # Press TAB at this point
    ```

-   What happened?

-   Use this feature to go quickly to `seqAnalysis`. What is the minimum
    number of keystrokes you have to use to go there from your home
    folder?

### 7.2 Remember!

-   When you press `TAB`, the shell tries to complete what you just
    typed by itself. This **auto-completion** feature of the shell is
    very convenient and will save you a lot of typing!

### 7.3 Test auto-completion

-   Now create a folder:

    ``` {.bash}
    ~/practicals/scripts/python/modifiedSources
    ```

-   Go back to your home folder, and go into `modifiedSources` using the
    `TAB` completion as much as you can. What do you notice?

### 7.4 Double `TAB`

-   Now create the folder:

    ``` {.bash}
    ~/practicals/scripts/python/modularComponents
    ```

-   Type:

    ``` {.bash}
    cd ~/practicals/scripts/python/mod   # Press TAB twice here
                                         # Type "ule" and press TAB again
    ```

-   Do you understand how `TAB` completion works? This also works for
    command names.

### 7.5 `UP` and `DOWN` arrow

-   Try typing a few times on the `UP ARROW`. What happens?

-   Try typing a few times on the `UP ARROW`, and then on the
    `DOWN ARROW`. What happens?

-   Try typing a few times on the `UP ARROW`, and then press `CTRL + C`.
    What happens?

-   Type `history`. What happens?

8. Copying, moving and removing files
-------------------------------------

### 8.1 Creating an empty file

-   Go the the `seqAnalysis` folder and type:

    ``` {.bash}
    touch DNA-analysis.py
    ls
    ```

-   What happened?

-   Find out the size of the new file.

### 8.2 Moving a file

-   Now type:

    ``` {.bash}
    mv DNA-analysis.py ../modularComponents
    ```

-   What happened? Did you use the `TAB` key? (you should!)

-   Explore the directory structure to find `DNA-analysis.py` again.

### 8.3 Copying a file

-   Go to the `modularComponents` subfolder and type:

    ``` {.bash}
    cp DNA-analysis.py ../modules
    ```

-   What happened?

### 8.4 Removing a file

-   From `modularComponents` folder, type:

    ``` {.bash}
    rm DNA-analysis.py
    ```

-   What happened?

9. Creating a directory hierarchy
---------------------------------

### 9.1 Moving a folder

-   From the `scripts` folder, move modularComponents into modules:

    ``` {.bash}
    mv modularComponents modules
    tree
    ```

-   What does `tree` do?

### 9.2 Copying a folder

-   Go to the `practicals` folder and make a copy of scripts:

    ``` {.bash}
    cp -r scripts scripts-backup
    ```

-   Note the `-r` option used for recursive copy inside the directories.

### 9.3 Removing a folder

-   Remove the newly created folder with:

    ``` {.bash}
    rm -r scripts-backup
    ```

-   Again, note the `-r` option to work on folders.

### 9.4 Exercise

-   Now that you have gained some experience, create the exact following
    directory structure (folders only shown here):

    ``` {.bash}
    .
    ├── archives
    ├── practicals
    │   ├── book
    │   │   └── ...
    │   ├── ecoli-data
    │   │   └── ...
    │   └── results
    │       └── 2016-11-14
    ├── scripts
    │   ├── R
    │   └── python
    │       ├── popGenetics
    │       ├── proteinStructure
    │       └── seqAnalysis
    └── zipped.archives
    ```

10. Viewing a file
------------------

### 10.1 `cat` command

-   Go to the `ecoli-data` folder and type:

    ``` {.bash}
    cat README
    ```

-   Try also `cat` on one of the fasta files. What happened?

-   By the way, do you know what is a fasta file?

### 10.2 `head` and `tail` commands

-   Type:

    ``` {.bash}
    # Use TAB for auto-completion as much as you can!
    head Escherichia_coli_o5_k4_l_h4_str_atcc_23502.GCA_000333195.1.26.pep.all.fa
    tail Escherichia_coli_o5_k4_l_h4_str_atcc_23502.GCA_000333195.1.26.pep.all.fa
    # Try head and tail options
    head -n 30 Escherichia_coli_o5_k4_l_h4_str_atcc_23502.GCA_000333195.1.26.pep.all.fa
    tail -n 3 Escherichia_coli_o5_k4_l_h4_str_atcc_23502.GCA_000333195.1.26.pep.all.fa
    ```

-   What do those commands do? What does the `-n` option do?

### 10.3 `less` command

-   `less` is very useful to examine large files.
-   You can navigate using the `UP` and `DOWN` arrows
-   You can also use the `B` and `SPACE` keys to move faster
-   You can exit with `Q`

``` {.bash}
less Escherichia_coli_o5_k4_l_h4_str_atcc_23502.GCA_000333195.1.26.pep.all.fa
```

11. A tour of some useful tools
-------------------------------

Let's go through a quick tour of some of the most useful commands in the
shell toolbox!

### 11.1 `wc` to count words

-   Go to the `ecoli-data` folder and type:

    ``` {.bash}
    wc Escherichia_coli_o55_h7_str_06_3555.GCA_000617385.1.26.pep.all.fa
    ```

    which produces:

    ``` {.bash}
      26318   51865 1824223 Escherichia_coli_o55_h7_str_06_3555.GCA_000617385.1.26.pep.all.fa
    ```

-   What does this output mean?

-   We can have only the number of lines with `wc -l` (try it!)

-   Which file in the `ecoli-data` folder has the most lines?

#### Wildcards

-   Try:

    ``` {.bash}
    wc -l *.fa
    ```

-   What happened?

-   Which file in the `ecoli-data` folder has the most lines?

### 11.2 Redirection

#### The `>` operator

-   When a command produces some output, it can be redirected to a file
    instead of to the terminal:

    ``` {.bash}
    wc -l *.fa > lineCounts
    cat lineCounts
    ```

-   `>` is a **redirection** operator, and automatically creates a new
    file or erases an existing file.

#### The `>>` operator

-   To redirect output and append it to an existing file, we can use the
    `>>` operator.

-   Compare `lineCounts.1` and `lineCounts.2` when you type:

    ``` {.bash}
    # lineCounts.1
    wc -l *.fa > lineCounts.1
    wc -l README > lineCounts.1
    # lineCounts.2
    wc -l *.fa > lineCounts.2
    wc -l README >> lineCounts.2
    ```

-   What happened?

### 11.3 `grep` to search for matches

-   Run the following commands from the `ecoli-data` folder:

    ``` {.bash}
    grep "flagellin" Escherichia_coli_o55_h7_str_06_3555.GCA_000617385.1.26.pep.all.fa
    grep --color=always "flagellin" Escherichia_coli_o55_h7_str_06_3555.GCA_000617385.1.26.pep.all.fa
    grep -n --color=always "flagellin" Escherichia_coli_o55_h7_str_06_3555.GCA_000617385.1.26.pep.all.fa
    grep -c --color=always "flagellin" Escherichia_coli_o55_h7_str_06_3555.GCA_000617385.1.26.pep.all.fa
    ```

-   What does each of the `grep` option do?

#### Exercise

-   Use `grep` to extract all the sequence names from one of the fasta
    file and store them in a file called `proteinNames`.

#### =grep= is versatile

-   Run the commands:

    ``` {.bash}
    grep -c flagellin *.fa
    grep -c flagel *.fa
    ```

-   Can you explain what `grep` did?

#### Exercise

-   How would you count the number of proteins in each fasta file?

### 11.4 `cut` to get columns

-   Run the commands:

    ``` {.bash}
    grep -c flagel *.fa > flagelCounts
    cat flagelCounts
    cut -d "_" -f 1 flagelCounts
    cut -d "_" -f 3 flagelCounts
    cut -d "_" -f 3,5 flagelCounts
    cut -d ":" -f 2 flagelCounts
    ```

-   Do you understand what `cut` does and the roles of the `-d` and `-f`
    options?

### 11.5 `sort` to sort things

-   Use `sort` to sort the line counts from `lineCounts`:

    ``` {.bash}
    sort lineCounts
    ```

-   Is everything correct? What if you try `sort -n lineCounts`? Can you
    see a difference?

-   Try also `sort -r lineCounts`. What is the difference?

#### Exercise

-   Using `grep` and `sort` and an intermediate file, sort the bacterial
    proteomes by decreasing number of proteins.

-   Hint: `sort` supports two interesting options, `-t` to specify a
    field separator and `-k` to specify which field to use for sorting.

### 11.6 `uniq` to remove or count duplicates

-   Go to the folder `~/practicals/boook` and use the Python script
    provided in the folder to convert *The Hound of the Baskervilles* to
    a list of words. Store this list in a file called `houndList`

-   Have a look at `houndList` using `head`, `tail` and `less`

-   Which words Arthur Conan Doyle used in his book? To get a list of
    distinct words, we can use `uniq`:

        uniq houndList > uniqueList

-   Have a look at this list. Are words really unique?

-   `uniq` only removes duplicates which are grouped together. How would
    you do to sort the list of all words, and then get a list of unique
    words used in this text file?

-   When using the `-c` option, `uniq` gives another
    additional information. Can you guess what it is?

### 11.7 Combining tools with pipes

#### Pipes can connect output and input streams

-   When we did sort `lineCounts`, we used `sort` on the output of `wc`,
    but we used an intermediate file.
-   The shell offers a powerful way to connect directly the output of a
    command to the input of another: the **pipe operator**.

    ``` {.bash}
    wc -l *.fa | sort -n
    ```

(to type a "|" on a Finnish keyboard, hold `AltGr` and press `<`)

#### Exercises

-   The `w` command output the list of connected users on the server.
    Try it, and then try:

        w | head
        w | tail

-   Use a pipe to find all the users whose login contains "jyy".

-   Extend the same pipe to count how many there are.

-   Using only pipes, get a sorted list of the word counts from *The
    Hound of the Baskervilles*. Which are the top ten most used words?
    How many times was "elementary" used? How many times "dear"? How
    many times "Watson"?

12. Wrap-up exercise
--------------------

At this stage, you can already leverage much of the shell power by using
simple commands and combining them into more complex tools. Let's put
what you learnt into practice!

For the next exercise, we are going to use:
-   a **ready-made Python script** designed to perform one simple action
-   some of the **shell tools** which also perform one simple action
    each
-   some "duct tape" to connect them together: **pipes** and
    **redirections**

### 12.1 Test the Python script

-   The script `seqComposition.py` takes a fasta file and produces a
    table containing the amino-acid composition of each protein in
    the file.

-   To run the script, type:

    ``` {.bash}
    python seqComposition.py myFastaFile
    # Use the fasta file you wish instead of "myFastaFile"
    ```

-   The output is sent to the terminal display.

-   **Exercise**: propose at least two practical ways to have a look at
    this output.

### 12.2 Real-life exercise

-   Using only the shell tools you know, the Python script and pipes,
    determine the distribution of the number of histidines per protein
    in the proteome of the strain of your choice.

-   More clearly stated: for a given strain, determines how many
    proteins have one histidine, how many have two, how many have
    three, ...

-   Good luck!

One step towards wizardry: shell scripts
========================================

1. Reusing your tool pipeline
-----------------------------

### Store your commands in a script

-   Let's use `nano` to store your pipeline in a file:

    ``` {.bash}
    nano getHistDistrib.sh
    ```

    (the usage of `nano` will be demonstrated live)

-   The idea is to be able to produce the histidine distribution results
    just by typing:

    ``` {.bash}
    bash getHistDistrib.sh myFastaFile
    ```

### Test your pipeline with a few files

-   Test your pipeline for five strains. Does it work fine? What would
    you do to be confident that the code is working properly?

-   Now you want to make a comparative study of the histidine
    distributions across the proteomes of all prokaryotic
    genomes available. How do you feel about running your script
    manually for several thousands strains?

-   As Raymond Hettinger would put it: "there must be a better way!"

2. Making a general purpose listing script
------------------------------------------

-   Create a shell script `testListing.sh` with this content:

    ``` {.bash}
    listFiles=‘ls *.fa‘
    echo $listFiles
    for myFile in $listFiles; do
        echo $myFile
        echo $myFile.results
    done
    ```

-   Run it with `bash`. What does it do?

3. Exercise: final script
-------------------------

-   Combine your pipeline script and the listing script into a single
    script to get the histidine distribution for all the fasta files in
    this folder.

-   How would you do if you wanted to do the same analysis in two
    months, after updating your genomic data with the latest sequences
    available?


