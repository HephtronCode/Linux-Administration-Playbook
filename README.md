# My Ultimate Linux Sysadmin Playbook (v1.3 - Missions Included!) 🐧🔥

Alright, let's DO this! This is my personal playbook for conquering the Linux command line, from the absolute basics to becoming a comfortable sysadmin. Forget clicking around – the real power is in the terminal! This guide includes learning sections **with inline command examples *and detailed breakdowns***, PLUS hands-on missions after each level to make sure the knowledge sticks. Time to fire up that terminal! 💻

**My Core Philosophy (Gotta Remember This!):**

> *   **Everything is a file:** Devices, connections, etc., often look like files. Simple.
> *   **Small, sharp tools:** Commands do one thing well. Chain 'em with pipes (`|`) for superpowers!
> *   **Automation is King/Queen! 👑:** If I do it twice, script it! Ops life.

**My Linux Lab Setup:**

I need a playground! My best options:

1.  **Virtual Machine (Recommended):** VirtualBox/VMware Player + **Ubuntu Server** or **Rocky/AlmaLinux**. No desktop needed!
2.  **WSL (Windows Subsystem for Linux):** Good for quick access on Windows.
3.  **Cloud Server (VPS):** DigitalOcean, Linode, AWS EC2 free tier, etc. Real-world practice!
4.  **Raspberry Pi:** Fun, dedicated Linux box.

*(Assuming I'm logged in and facing a terminal prompt like `myuser@myhostname:~$`)*

---

## Playbook Level 0: The Absolute Bare Minimum (Getting In & Looking Around)

**My Goal:** Log in, figure out where I am, and know how to ask for help.

*   **Logging In:** Via terminal or SSH.
    ```bash
    ssh myuser@192.168.1.100
    ```
    *   `ssh`: The command to initiate a Secure Shell connection.
    *   `myuser`: The username I want to log in as on the remote machine.
    *   `@`: Separator between the username and the hostname/IP address.
    *   `192.168.1.100`: The IP address (or hostname) of the machine I want to connect to.
    *   *(After running, it will likely prompt for `myuser`'s password).*

*   **The Prompt (`user@host:~$`):** Shows `user`, `hostname`, current directory (`~` is home), and privilege level (`$`=regular, `#`=root!).

*   **Who/What/Where:** Getting basic system info.
    *   `whoami`: Shows my current username.
        ```bash
        whoami
        ```
        *   `whoami`: The command itself, asking "who am I?".
        *   *(Output: myuser)*
    *   `hostname`: Displays the system's network name.
        ```bash
        hostname
        ```
        *   `hostname`: The command to show the configured name of the machine.
        *   *(Output: server01)*
    *   `uname -a`: Shows system/OS/kernel details.
        ```bash
        uname -a
        ```
        *   `uname`: Command to print system information.
        *   `-a`: Option meaning "all" information (kernel name, hostname, kernel release, kernel version, machine hardware name, operating system).
        *   *(Output: Linux server01 5.15.0-76-generic ... x86_64 GNU/Linux)*
    *   `pwd`: **P**rint **W**orking **D**irectory (my current location).
        ```bash
        pwd
        ```
        *   `pwd`: The command to show the full path of the directory I'm currently in.
        *   *(Output: /home/myuser)*

*   **Listing Files (`ls`):** Viewing directory contents.
    *   `ls`: Basic list.
        ```bash
        ls
        ```
        *   `ls`: The **l**i**s**t command. By default, lists non-hidden files/directories in the current directory.
        *   *(Output: Documents Downloads Pictures Videos my_script.sh)*
    *   `ls -l`: Long format (permissions, owner, size, date).
        ```bash
        ls -l
        ```
        *   `ls`: The list command.
        *   `-l`: Option for **l**ong listing format, showing detailed information per item.
        *   *(Output: -rw-rw-r-- 1 myuser myuser 1024 Jul 28 10:30 my_notes.txt)*
    *   `ls -a`: Show **a**ll files (including hidden `.dotfiles`).
        ```bash
        ls -a
        ```
        *   `ls`: The list command.
        *   `-a`: Option to show **a**ll entries, including those starting with a `.` (which are normally hidden).
        *   *(Output: . .. .bashrc .profile Documents my_notes.txt)*
    *   `ls -lh`: Long format + **h**uman-readable sizes (KB, MB, GB).
        ```bash
        ls -lh
        ```
        *   `ls`: The list command.
        *   `-l`: Option for long listing format.
        *   `-h`: Option for **h**uman-readable file sizes (used *with* `-l`).
        *   *(Output: -rw-rw-r-- 1 myuser myuser 1.1K Jul 28 10:30 my_notes.txt)*
    *   `ls -lha`: **My standard `ls`!** Combine options. Order often doesn't matter.
        ```bash
        ls -lha
        ```
        *   `ls`: The list command.
        *   `-l`: Long format.
        *   `-h`: Human-readable sizes.
        *   `-a`: Show all files.

*   **Changing Directories (`cd`):** Navigating the filesystem.
    *   `cd /var/log`: Go to the `/var/log` directory.
        *   `cd`: The **c**hange **d**irectory command.
        *   `/var/log`: The argument, specifying the absolute path to navigate to.
    *   `cd ..`: Go up one level from the current directory.
        *   `cd`: The change directory command.
        *   `..`: Special directory entry representing the parent directory.
    *   `cd ~` or just `cd`: Go directly to my home directory.
        *   `cd`: The change directory command.
        *   `~` (Tilde): Special character representing the current user's home directory. `cd` with no arguments also defaults to home.
    *   `cd -`: Go to the *previous* directory I was in. Very useful for toggling!
        *   `cd`: The change directory command.
        *   `-`: Special argument meaning the previous working directory.

*   **Getting Help (CRITICAL!):** Don't guess, ask!
    *   `man ls`: Show the full manual page for the `ls` command.
        *   `man`: The command to display **man**ual pages.
        *   `ls`: The argument, specifying which command's manual page to show. (`q` to quit).
    *   `cp --help`: Show a short usage summary for the `cp` command.
        *   `cp`: The command (`cp` in this case).
        *   `--help`: A common option (usually double-dash) to request brief help output directly from the command.
    *   `apropos network`: Search manual pages for keyword "network".
        *   `apropos`: Command to search the manual page names and descriptions.
        *   `network`: The keyword to search for.
    *   `whatis pwd`: Give a one-line description of `pwd`.
        *   `whatis`: Command to display a very brief description from the manual page database.
        *   `pwd`: The command to describe.

*   **Clearing Screen:** `clear` or `Ctrl+L`. Command `clear` redraws the terminal screen. `Ctrl+L` is a keyboard shortcut that does the same thing.

*   **Exiting:** `exit` or `Ctrl+D`. Command `exit` terminates the current shell session. `Ctrl+D` often sends an End-of-File signal, which also typically exits the shell.

***
Alright, first steps taken! Feeling the power yet? 😉 Let's make sure that initial info is locked in.

**🎯 My First Mission:**

1.  Log into my Linux system.
2.  Who am I logged in as? (`whoami`) What's this machine called? (`hostname`) What OS/kernel? (`uname -a`) Get familiar!
3.  Where exactly *am* I right now? (`pwd`) List *everything* in that directory, long format, human-readable sizes (`ls -lha`).
4.  Time for a field trip! Navigate to the `/var/log` directory. What interesting files do I see there? (`cd /var/log`, then `ls -lh`).
5.  Now, head over to `/etc`. Poke around! (`cd /etc`, `ls`). Find any files ending in `.conf`? (Hint: `ls *.conf`).
6.  Quick! Get back to my home directory without typing the full path (`cd`). Confirm I'm home (`pwd`).
7.  Feeling lost? 🧭 How would I find out *exactly* what the `cd` command does and its options? (`man cd` or `cd --help`). Practice looking things up!
8.  Tidy up that screen (`clear` or `Ctrl+L`). Looks better, right? ✨
9.  Log out (`exit` or `Ctrl+D`).

Boom! Mission 0 complete. See? Not so scary. I'll repeat this until navigating and listing feels totally natural.
***

---

## Playbook Level 1: Working with Files & Directories

**My Goal:** Create, view, edit, move, copy, and (carefully!) delete files and folders.

*   **Viewing Files:** Looking inside.
    *   `cat /etc/os-release`: Show entire (short) file content.
        *   `cat`: Command to con**cat**enate and display file contents.
        *   `/etc/os-release`: The file path to display.
    *   `less /var/log/syslog`: **Best way!** Page through large files.
        *   `less`: Pager command, allows scrolling (arrows, PageUp/Down), searching (`/pattern`), quitting (`q`).
        *   `/var/log/syslog`: The large log file to view.
    *   `head /var/log/dmesg`: Show first 10 lines.
        *   `head`: Command to show the beginning (head) of a file. Default is 10 lines.
        *   `/var/log/dmesg`: The file to view.
    *   `head -n 5 /etc/passwd`: Show first 5 lines.
        *   `head`: The command.
        *   `-n 5`: Option specifying the **n**umber of lines to show (5 in this case).
        *   `/etc/passwd`: The file to view.
    *   `tail /var/log/syslog`: Show last 10 lines.
        *   `tail`: Command to show the end (tail) of a file. Default is 10 lines.
        *   `/var/log/syslog`: The file to view.
    *   `tail -n 20 /var/log/auth.log`: Show last 20 lines.
        *   `tail`: The command.
        *   `-n 20`: Option specifying the **n**umber of lines to show (20).
        *   `/var/log/auth.log`: The file to view.
    *   `tail -f /var/log/nginx/access.log`: **Follow** file updates live.
        *   `tail`: The command.
        *   `-f`: Option to **f**ollow the file, showing new lines as they are added. (`Ctrl+C` stops).
        *   `/var/log/nginx/access.log`: The log file to watch.

*   **Creating:** Making new things.
    *   `touch my_new_file.txt`: Create empty file / update timestamp.
        *   `touch`: Command to change file timestamps, or create an empty file if it doesn't exist.
        *   `my_new_file.txt`: The name of the file to create/update.
    *   `mkdir my_project_files`: Make a directory.
        *   `mkdir`: The **m**a**k**e **dir**ectory command.
        *   `my_project_files`: The name of the directory to create.
    *   `mkdir -p ~/work/reports/q3`: Create `work`, `reports`, `q3` if they don't exist.
        *   `mkdir`: The make directory command.
        *   `-p`: Option to create **p**arent directories as needed (no error if they already exist).
        *   `~/work/reports/q3`: The nested path to create (`~` is home directory).

*   **Editing (Choose `nano` or `vim`):** Modifying file content.
    *   `nano config.txt`: Open `config.txt` in `nano`.
        *   `nano`: Simple text editor command.
        *   `config.txt`: The file to edit (will be created if it doesn't exist). Use `Ctrl+X` to exit.
    *   `vim script.py`: Open `script.py` in `vim`.
        *   `vim`: Powerful modal text editor command.
        *   `script.py`: The file to edit. Requires learning `vim` modes (`i`=Insert, `Esc`=Normal, `:wq`=Save&Quit).

*   **Copying (`cp`):** Duplicating files/directories.
    *   `cp main.py main_backup.py`: Copy file `main.py` to `main_backup.py`.
        *   `cp`: The **c**o**p**y command.
        *   `main.py`: The source file.
        *   `main_backup.py`: The destination file name.
    *   `cp important.docx ~/Documents/`: Copy `important.docx` *into* my `Documents` folder.
        *   `cp`: The copy command.
        *   `important.docx`: The source file.
        *   `~/Documents/`: The destination directory (the filename `important.docx` is implied).
    *   `cp -r website_files/ /var/www/html/`: Copy directory `website_files` **r**ecursively.
        *   `cp`: The copy command.
        *   `-r` or `-R`: Option to copy directories **r**ecursively.
        *   `website_files/`: The source directory.
        *   `/var/www/html/`: The destination directory.

*   **Moving/Renaming (`mv`):** Same command for both!
    *   `mv temp_name.txt final_name.log`: Rename `temp_name.txt` to `final_name.log`.
        *   `mv`: The **m**o**v**e command (also used for renaming).
        *   `temp_name.txt`: The source file/original name.
        *   `final_name.log`: The destination/new name.
    *   `mv *.tmp ~/trash/`: Move all files ending in `.tmp` to my `trash` directory.
        *   `mv`: The move command.
        *   `*.tmp`: The source files, using a wildcard (`*`) to match any characters ending in `.tmp`.
        *   `~/trash/`: The destination directory.
    *   `mv project_a project_final`: Rename directory `project_a` to `project_final`.
        *   `mv`: The move/rename command.
        *   `project_a`: Source directory.
        *   `project_final`: Destination directory name.

*   **Deleting (`rm`, `rmdir`):** ☠️ **DANGER ZONE - NO UNDO! BE SURE!** ☠️ Removing items.
    *   `rm old_report.pdf`: Remove the file `old_report.pdf`.
        *   `rm`: The **r**e**m**ove command.
        *   `old_report.pdf`: The file to delete (might prompt for confirmation).
    *   `rm -f data.csv`: **F**orce remove `data.csv` without prompting.
        *   `rm`: The remove command.
        *   `-f`: Option to **f**orce deletion without confirmation. Use with extreme caution!
        *   `data.csv`: The file to force-delete.
    *   `rmdir empty_folder`: Remove the directory `empty_folder` *only if it's empty*.
        *   `rmdir`: The **r**e**m**ove **dir**ectory command (only works on empty dirs).
        *   `empty_folder`: The directory to remove.
    *   `rm -r old_project/`: Remove the directory `old_project` and all its contents **r**ecursively.
        *   `rm`: The remove command.
        *   `-r` or `-R`: Option to remove directories and their contents **r**ecursively. **Very dangerous.**
        *   `old_project/`: The directory to delete.
    *   `rm -rf logs/*`: **F**orce remove all files/dirs inside `logs` **r**ecursively.
        *   `rm`: The remove command.
        *   `-r`: Recursive option.
        *   `-f`: Force option.
        *   `logs/*`: Target - everything (`*`) inside the `logs` directory. **Extremely dangerous.** Double-check the path and wildcard!

*   **Finding Files:** Searching the filesystem structure.
    *   `find . -name "config.yaml"`: Find files named `config.yaml` starting from current dir (`.`).
        *   `find`: The search command.
        *   `.`: The starting directory for the search (current directory).
        *   `-name "config.yaml"`: The primary test - match items whose **name** is exactly `config.yaml`. Quotes prevent shell expansion.
    *   `find /home/myuser/Documents -type f -iname "*.pdf"`: Find regular files ending in `.pdf` (case-insensitive) under a specific path.
        *   `find`: The search command.
        *   `/home/myuser/Documents`: The starting path.
        *   `-type f`: Primary test - match only regular **f**iles.
        *   `-iname "*.pdf"`: Primary test - match names **i**gnoring case, ending in `.pdf` (`*` wildcard).
    *   `find /tmp -mtime +7 -delete`: Find files in `/tmp` modified more than 7 days ago and delete them.
        *   `find`: The search command.
        *   `/tmp`: Starting path.
        *   `-mtime +7`: Primary test - match files whose data was **m**odified more (`+`) than `7` 24-hour periods ago.
        *   `-delete`: Action - **delete** the files found. Use action flags with caution!
    *   `locate bashrc`: Quickly **locate** files with `bashrc` in their name using an indexed database.
        *   `locate`: The fast search command (uses pre-built index).
        *   `bashrc`: The pattern to search for in filenames. May need `sudo updatedb` to refresh the index.

*   **Searching Inside Files (`grep`):** Finding text patterns within file content.
    *   `grep "Error 404" /var/log/apache2/error.log`: Find lines containing "Error 404".
        *   `grep`: Command to search for **p**atterns in input text.
        *   `"Error 404"`: The pattern (string) to search for. Quoted as it contains a space.
        *   `/var/log/apache2/error.log`: The file to search within.
    *   `grep -i 'session closed' /var/log/auth.log`: Case-**i**nsensitive search.
        *   `grep`: The search command.
        *   `-i`: Option for case-**i**nsensitive matching.
        *   `'session closed'`: The pattern (single quotes also work for strings).
        *   `/var/log/auth.log`: The file to search.
    *   `grep -r 'api_key' /etc/myapp/conf.d/`: **R**ecursively search for 'api_key' in a directory.
        *   `grep`: The search command.
        *   `-r`: Option to search **r**ecursively through files in the specified directory.
        *   `'api_key'`: The potentially sensitive pattern to find. **Risk of exposing secrets!**
        *   `/etc/myapp/conf.d/`: The directory to start searching within.
    *   `ps aux | grep -v grep`: Show processes, but exclude (`-v`) the grep command itself.
        *   `ps aux`: List processes (source of text).
        *   `|`: Pipe - sends output of `ps` to `grep`.
        *   `grep`: The search command.
        *   `-v`: Option to **v**ert (exclude) lines matching the pattern.
        *   `grep`: The pattern to exclude (the grep command itself often shows up).
    *   `grep -E '^([0-9]{1,3}\.){3}[0-9]{1,3}' access.log`: Use **E**xtended regex to find IPv4 addresses at the start (`^`) of lines.
        *   `grep`: The search command.
        *   `-E`: Option to use **E**xtended Regular Expressions (more powerful patterns).
        *   `'^([0-9]{1,3}\.){3}[0-9]{1,3}'`: The regex pattern matching an IPv4 address at the beginning (`^`) of a line. (Regex is a mini-language itself!).
        *   `access.log`: The file to search.

*   **Links (`ln`):** Creating filesystem pointers.
    *   `ln -s /var/log/app/current.log ~/app.log`: Create a **s**ymbolic link named `app.log` in home dir pointing to actual log file.
        *   `ln`: The **l**i**n**k command.
        *   `-s`: Option to create a **s**ymbolic link (pointer).
        *   `/var/log/app/current.log`: The **target** file or directory the link points to.
        *   `~/app.log`: The **name and path** of the symbolic link being created.
    *   `ln data.txt data_hardlink.txt`: Create a hard link (another name for the same file content).
        *   `ln`: The link command (without `-s`, creates a hard link).
        *   `data.txt`: The existing target file.
        *   `data_hardlink.txt`: The new name (hard link) for the same file data.

***
Okay, now I'm manipulating things! Creating, moving, deleting... this is where I start building (and breaking, which is part of learning 😉).

**🎯 Mission 1: File & Folder Frenzy!**

1.  Back in my home directory (`cd ~`). Create a new directory called `linux_practice`. (`mkdir linux_practice`). Go into it (`cd linux_practice`).
2.  Inside `linux_practice`, create three empty files: `notes.txt`, `script.sh`, `data.csv`. (`touch notes.txt script.sh data.csv`). Verify they exist (`ls -l`).
3.  Use `nano` (or `vim`!) to open `notes.txt`. Add lines like "Learning Linux commands." "Today I learned about `cp`, `mv`, `rm`." Save and exit (`nano`: Ctrl+X, Y, Enter).
4.  Display the contents of `notes.txt` using `cat`. Simple!
5.  Now imagine `notes.txt` was HUGE. View it again using `less`. Practice scrolling up/down, searching for a word (type `/word`), and quitting (`q`). Much better for big files!
6.  Make a subdirectory called `backups`. (`mkdir backups`).
7.  Copy `notes.txt` *into* the `backups` directory. (`cp notes.txt backups/`). Check inside `backups` (`ls backups/`).
8.  Oops, bad name. Rename `script.sh` to `important_script.sh`. (`mv script.sh important_script.sh`). Verify (`ls`).
9.  Move `data.csv` into the `backups` directory. (`mv data.csv backups/`). Check both directories now (`ls` and `ls backups/`).
10. Search Time! From *inside* `linux_practice`, find `important_script.sh` using `find`. (`find . -name "important_script.sh"`). The `.` means current directory!
11. Let's peek inside! Use `grep` to find the line containing "Linux" inside `notes.txt`. (`grep "Linux" notes.txt`). Try case-insensitive (`grep -i "linux" notes.txt`).
12. Tidy up? Carefully remove the *copy* of `notes.txt` inside `backups`. (`rm backups/notes.txt`). **Delete the right one!**
13. Feeling brave? Try `rmdir backups`. Why does it fail? Now, carefully remove `backups` *and its contents* using `rm -r`. (`rm -r backups/`). **Triple-check before Enter!** 🙏

Whew! File management unlocked. This is bread-and-butter stuff, gotta get comfortable with it!
***

---

## Playbook Level 2: Users, Groups & Permissions

**My Goal:** Understand the security model – who owns what, who can do what. Crucial stuff! 🔒

*   **Accounts & Info Files:** User/Group ID system.
    *   User: Has UID (User ID), primary GID (Group ID). `root` = UID 0 (superuser).
    *   Info Files: `/etc/passwd` (user list), `/etc/shadow` (encrypted passwords - root only!), `/etc/group` (group list). Don't edit directly unless expert!
*   **Identifying Who/What:** Checking current/other users/groups.
    *   `id`: Show my own User ID (uid), Group ID (gid), and supplementary groups.
    *   `id alice`: Show UID, GID, groups for user `alice`.
    *   `groups`: List just the names of groups I'm in.
    *   `groups bob`: List groups user `bob` is in.
    *   `who`: Show users currently logged into the system (terminal, login time, origin IP).
    *   `w`: More detailed `who`, including current command/process.

*   **Managing Users (requires `sudo`):** Adding, modifying, deleting users.
    *   `sudo useradd -m -s /bin/bash charlie`: Add user `charlie`.
        *   `sudo`: Run command as superuser.
        *   `useradd`: Command to add a new user.
        *   `-m`: Option to **m**ake the user's home directory.
        *   `-s /bin/bash`: Option to set the login **s**hell (interactive command interpreter) to `/bin/bash`.
        *   `charlie`: The username to create.
    *   `sudo passwd charlie`: Set (or change) the password for `charlie`.
        *   `sudo`: Run as superuser.
        *   `passwd`: Command to manage passwords.
        *   `charlie`: The user whose password to set (prompts for new password twice).
    *   `sudo usermod -aG developers charlie`: **A**dd `charlie` to the supplementary **G**roup `developers`.
        *   `sudo`: Run as superuser.
        *   `usermod`: Command to modify user account properties.
        *   `-a`: Option to **a**ppend (add) to group list (crucial!). Without `-a`, it *replaces* all supplementary groups.
        *   `-G developers`: Option specifying the **G**roup(s) to add the user to.
        *   `charlie`: The user to modify.
    *   `sudo usermod -l new_charlie charlie`: Change login **n**ame from `charlie` to `new_charlie`.
        *   `-l new_charlie`: Option specifies the **l**ogin name to change to.
        *   `charlie`: The original/current username.
    *   `sudo usermod -L dave`: **L**ock user `dave`'s account.
        *   `-L`: Option to **L**ock the account (prevents password login).
    *   `sudo usermod -U dave`: **U**nlock user `dave`'s account.
        *   `-U`: Option to **U**nlock the account.
    *   `sudo userdel eve`: Delete user `eve`.
        *   `userdel`: Command to delete a user account.
        *   `eve`: The username to delete. Note: Doesn't remove home directory by default.
    *   `sudo userdel -r frank`: Delete user `frank` **and r**emove home directory.
        *   `-r`: Option to **r**emove the user's home directory and mail spool. Careful!

*   **Managing Groups (requires `sudo`):**
    *   `sudo groupadd webmasters`: Create new group `webmasters`.
        *   `groupadd`: Command to add a new group.
        *   `webmasters`: Name of the group to create.
    *   `sudo groupmod -n webdevs webmasters`: Change group **n**ame from `webmasters` to `webdevs`.
        *   `groupmod`: Command to modify group properties.
        *   `-n webdevs`: Option specifying the **n**ew name.
        *   `webmasters`: The original group name.
    *   `sudo groupdel oldgroup`: Delete group `oldgroup`.
        *   `groupdel`: Command to delete a group. Must ensure no users have it as primary group first.

*   **Switching User / Running As Another:**
    *   `su bob`: **S**witch **U**ser to `bob` (needs *bob's* password). Shell remains in same directory.
    *   `su - jane`: Switch user to `jane`, get a full login shell (changes dir to jane's home, loads her profile). Needs *jane's* password.
    *   `sudo apt update`: Run `apt update` as `root` (needs *my* password, if I'm in `sudoers`). **Preferred for admin tasks.**
    *   `sudo -i`: Start an **i**nteractive `root` shell via `sudo`. Remember to `exit`!
    *   `visudo`: **Use ONLY this command to edit `/etc/sudoers`.** It prevents saving invalid syntax.

*   **File Permissions (`ls -l` -> `-rwxr-xr--`):** Decoding the access string.
    *   `Type | Owner(u) | Group(g) | Other(o)` (1 + 3 + 3 + 3 = 10 characters).
    *   Permissions: `r`=Read, `w`=Write, `x`=Execute. `-` = Permission denied.
    *   *Directory Meaning*: `r`=list names, `w`=create/delete/rename within, `x`=enter (`cd`).

*   **Changing Permissions (`chmod`):** Modifying access rights.
    *   **Symbolic (`u`/`g`/`o`/`a`, `+`/`-`/`=`):** Readable for single changes.
        ```bash
        # Add execute for user (owner)
        chmod u+x my_script.sh
        # Remove write for group and other
        chmod go-w shared_doc.txt
        # Set others to have exactly read permission (remove w/x)
        chmod o=r data.csv
        # Make file readable by all, writable only by user/group
        chmod ug=rw,o=r config.yml
        ```
    *   **Octal (Numeric: `r=4,w=2,x=1`):** Sets all permissions concisely. 3 digits: `User`, `Group`, `Other`.
        *   `7=rwx`, `6=rw-`, `5=r-x`, `4=r--`, `0=---`.
        ```bash
        # rwxr-xr-x -> (4+2+1)(4+0+1)(4+0+1) = 755 (Common for scripts/dirs)
        chmod 755 my_script.sh
        # rw-r--r-- -> (4+2+0)(4+0+0)(4+0+0) = 644 (Common for data files)
        chmod 644 index.html
        # rwx------ -> (4+2+1)(0+0+0)(0+0+0) = 700 (Private directory)
        chmod 700 ~/.config/my_app/
        # rw------- -> (4+2+0)(0+0+0)(0+0+0) = 600 (Private key file)
        chmod 600 ~/.ssh/id_rsa
        ```
    *   **Recursive:** `chmod -R <permissions> <directory>` applies changes to the directory and everything inside it.
        ```bash
        # Make all files under data_dir readable/writable by owner, readable by group
        chmod -R u=rw,g=r data_dir/
        # BE CAREFUL applying execute recursively! Often wrong for data files.
        ```

*   **Changing Ownership (`chown`, `chgrp` - needs `sudo`):** Who controls the file?
    *   `sudo chown bob important.txt`: Change **own**er to `bob`.
        *   `chown`: The **ch**ange **own**er command.
    *   `sudo chgrp editors report.doc`: Change **gr**ou**p** to `editors`.
        *   `chgrp`: The **ch**ange **gr**ou**p** command.
    *   `sudo chown alice:projectx config.ini`: Change owner to `alice` **and** group to `projectx`. Colon `:` separates user and group.
    *   `sudo chown -R www-data:www-data /var/www/my_app/`: **R**ecursively change owner and group for web server files.
        *   `-R`: Recursive option.
        *   `www-data:www-data`: The web server user and group (common on Debian/Ubuntu, might be `apache` on others).
        *   `/var/www/my_app/`: The web application directory.

***
Security time! 🔒 Understanding who can do what is *super* important. Mess this up, and things go sideways fast.

**🎯 Mission 2: Permission Power Play!**

1.  Still in my `linux_practice` directory, create `secret_plans.txt`. (`touch secret_plans.txt`).
2.  Check its permissions (`ls -l secret_plans.txt`). Defaults? Owner? Group?
3.  Lock it down! Permissions so *only owner* reads/writes. Octal method? (Think `rw-------`. 4+2+0=6 for owner, 0 group, 0 others = `chmod 600 secret_plans.txt`). Verify (`ls -l`).
4.  Too secret? Symbolic method: *add* read for *group*. (`chmod g+r secret_plans.txt`). Verify.
5.  Remove *all* permissions for "others" symbolically (`chmod o= secret_plans.txt`). Verify.
6.  Who am I again? (`id`). What groups am I in? (`groups`).
7.  **(Optional - If I have `sudo` access):**
    *   Create test group: `sudo groupadd project_alpha`.
    *   Create test user (no home dir yet): `sudo useradd testbuddy`.
    *   Set their password: `sudo passwd testbuddy` (enter twice).
    *   Add `testbuddy` to `project_alpha` group: `sudo usermod -aG project_alpha testbuddy`. **Remember the `-a`!**
    *   Change `secret_plans.txt` group to `project_alpha`: `sudo chgrp project_alpha secret_plans.txt`. Verify (`ls -l`).
    *   Change owner to `testbuddy`: `sudo chown testbuddy secret_plans.txt`. Verify.
    *   Switch user: `su - testbuddy` (enter their password). `pwd`? Home dir? Try `cd /home/my_user/linux_practice` then `cat secret_plans.txt`. Readable? Try `nano secret_plans.txt`. Writable? Should match permissions!
    *   Switch back: `exit`.
    *   Clean up: `sudo userdel testbuddy`, `sudo groupdel project_alpha`.
8.  What does `sudo -l` do? (Try it if I have sudo). Tells me my sudo powers!

Understanding `rwx` for `ugo` is key! I'll play around safely until it clicks.
***

---

## Playbook Level 3: Process Management

**My Goal:** See what's running, manage programs, stop them if needed. Keeping tabs! 🤠

*   **Process:** A running instance of a program (PID, PPID, owner, resources).

*   **Listing Processes:** Viewing activity.
    *   `ps aux`: **A**ll processes, **u**ser-oriented format, include processes without **x**terminal. Standard, detailed view. Pipe to `less` for large lists: `ps aux | less`.
    *   `ps -ef`: Alternative "full" format (System V style). Shows PPID well, also standard.
    *   `ps aux | grep nginx`: Find `nginx` related processes.
        *   `ps aux`: Generate the process list.
        *   `|`: Pipe the output of `ps` into `grep`.
        *   `grep nginx`: Filter for lines containing "nginx".
    *   `pgrep httpd`: Get only the **P**rocess **ID**(s) for processes named `httpd`. Useful for scripting.
    *   `pgrep -u www-data php-fpm`: Find PIDs for `php-fpm` processes run by user `www-data`.
        *   `-u www-data`: Option to filter by **u**ser.

*   **Live Monitoring:** Real-time view.
    *   `top`: Classic CPU-sorted live view (`q`=quit). Press keys like `M` (memory sort), `P` (CPU sort), `k` (kill process), `u` (filter user).
    *   `htop`: Modern, colorful, user-friendly `top` alternative. Highly recommended! Use function keys (F1-F10) or mouse. (`sudo apt/dnf install htop`).

*   **Stopping Processes (Sending Signals):** Terminating programs.
    *   `kill 1234`: Send default SIGTERM (15) signal to PID 1234 (polite request to exit).
        *   `kill`: The command to send a signal.
        *   `1234`: The Process ID (PID) to send the signal to.
    *   `kill -l`: **L**ist available signal names and numbers.
    *   `kill -SIGTERM 1234` or `kill -15 1234`: Send SIGTERM explicitly.
    *   `kill -SIGKILL 1234` or `kill -9 1234`: Send SIGKILL signal (force kill). **Last resort!**
        *   `-SIGKILL` or `-9`: The signal specification. Cannot be ignored.
    *   `kill -SIGHUP 5678` or `kill -1 5678`: Send SIGHUP (Hang Up) signal (often tells service to reload config).
        *   `-SIGHUP` or `-1`: The signal specification.
    *   `killall firefox`: Kill all processes named `firefox`. Be specific!
    *   `pkill -f my_buggy_script.py`: Kill process matching full (`-f`) command line pattern.

*   **Process Priority (Niceness):** Affecting scheduler (-20 high prio, +19 low prio).
    *   `nice -n 10 ./run_backup.sh`: Start command with nice value `10` (lower priority).
        *   `nice`: The command to run another command with modified priority.
        *   `-n 10`: Option to set the **n**ice adjustment value.
    *   `renice 5 -p 1234`: Change running process `1234` to nice value `5`.
        *   `renice`: Command to **re**set **nice** value of running processes.
        *   `5`: The new absolute nice value.
        *   `-p 1234`: Target the process with **P**ID `1234`.
    *   `sudo renice -10 -p 5678`: Increase priority (nice value -10 requires `sudo`).

*   **Background/Foreground Job Control (`&`, `jobs`, `fg`, `bg`, `Ctrl+Z`):** Shell task management.
    *   `sleep 60 &`: Run `sleep 60` in the **background**. `&` makes it run in background.
        *   `&`: Operator telling the shell not to wait for the command to finish.
    *   `jobs`: List active background jobs started in *this* shell session.
    *   `Ctrl+Z`: (Press keys) Suspend the currently running foreground job. Puts it in "Stopped" state.
    *   `bg %1`: Resume suspended job number `1` in the **b**ack**g**round.
        *   `bg`: Command to resume a stopped job in the background.
        *   `%1`: Specifies job number 1 (from `jobs` output).
    *   `fg %1`: Bring job number `1` (background or stopped) to the **f**ore**g**round.
        *   `fg`: Command to bring a job to the foreground.
        *   `%1`: Specifies job number 1.
    *   `nohup ./long_process.sh &`: Run command immune to **no** **h**ang**up**, in background. Output goes to `nohup.out`.
        *   `nohup`: Command prefix making the following command ignore hangup signals.

***
Keeping track of what's running and controlling it – essential sysadmin skills. Let's wrangle some processes! 🤠

**🎯 Mission 3: Process Patrol!**

1.  Find out what processes *I* am currently running using `ps`.
2.  Now see *everything* running. Use `ps aux | less`. Can I spot `sshd`? `systemd` (PID 1)?
3.  Make background noise! Run `sleep 300 &`. What does `&` do? What message appears? (`[1] 12345`)
4.  Use `jobs` to see my background job. Note its job number (e.g., `[1]`).
5.  Find the PID of that `sleep` command. Two ways:
    *   `ps aux | grep sleep` (Shows `sleep` and the `grep` itself).
    *   `pgrep sleep`. Much cleaner! Note the PID.
6.  Bring `sleep` to the foreground using its job number (`fg %1`). No prompt now!
7.  Need the prompt back! *Suspend* the job: `Ctrl+Z`. See `[1]+ Stopped`?
8.  Check `jobs`. See "Stopped"?
9.  Let it continue *in the background*: `bg %1`. Check `jobs` - should be "Running".
10. Open *another terminal*. Find the `sleep` PID again using `pgrep sleep`.
11. Time to terminate! Try politely first: `kill <PID>`. Back in terminal 1, did it end? (Should see "Terminated").
12. If `kill` failed, *then* I'd use `kill -9 <PID>`. The hammer! 🔨
13. Open `top` or `htop` (install `htop`!). Watch processes. Sort by memory (`M`/`F6`+Select)? By CPU (`P`/Default)? Explore `top`/`htop`. Quit (`q`).

I'm the process whisperer now! Finding, monitoring, stopping processes – critical.
***

---

## Playbook Level 4: Package Management

**My Goal:** Install, update, remove software using my system's manager (APT or DNF/YUM). Handles dependencies automatically! 📦

*   **Know Your System!** `apt` (Debian/Ubuntu) vs `dnf`/`yum` (RHEL/Fedora/CentOS).

1.  **APT (Debian/Ubuntu) - Requires `sudo`:**
    *   `sudo apt update`: **ALWAYS FIRST!** Resynchronize package index files.
    *   `sudo apt upgrade`: Upgrade installed packages.
    *   `sudo apt full-upgrade`: Like `upgrade`, may add/remove pkgs to resolve conflicts.
    *   `sudo apt install tree wget curl`: Install specified packages.
        *   `install`: Action to install packages.
        *   `tree wget curl`: List of package names to install.
    *   `sudo apt remove nano`: Remove `nano` package (configs might stay).
        *   `remove`: Action to remove packages.
    *   `sudo apt purge apache2-utils`: Remove `apache2-utils` AND global configs.
        *   `purge`: Stronger removal action.
    *   `sudo apt autoremove`: Remove orphaned dependencies.
    *   `apt search "http server"`: Search available packages for a term.
        *   `search`: Action to search repository metadata.
        *   `"http server"`: Search term (quoted due to space).
    *   `apt show nginx`: Show details for package `nginx`.
        *   `show`: Action to display package information.

2.  **DNF (RHEL/Fedora/CentOS) - Requires `sudo`:** (`yum` similar).
    *   `sudo dnf check-update`: Check for available updates.
    *   `sudo dnf update`: Apply all available updates. `-y` auto-answers yes.
    *   `sudo dnf install tmux vim-enhanced`: Install specified packages.
        *   `install`: Action to install.
    *   `sudo dnf remove httpd-tools`: Remove `httpd-tools` package.
        *   `remove`: Action to remove.
    *   `sudo dnf autoremove`: Remove unneeded dependencies.
    *   `dnf search "text editor"`: Search packages.
        *   `search`: Action to search.
    *   `dnf info htop`: Show package details.
        *   `info`: Action to display information.

3.  **Lower-Level Tools:** Used by package managers.
    *   `dpkg -l`: (`apt` systems) **l**ist installed packages.
        *   `-l`: Option to list.
    *   `dpkg -L coreutils`: (`apt`) **L**ist files owned by package `coreutils`.
        *   `-L`: Option to list files.
    *   `dpkg -S /bin/ls`: (`apt`) Find package owning (`-S`) file `/bin/ls`.
        *   `-S`: Option to search for packages owning a file.
    *   `rpm -qa`: (`dnf` systems) **q**uery **a**ll installed packages.
        *   `-q`: Query mode.
        *   `-a`: All packages.
    *   `rpm -ql bash`: (`dnf`) **q**uery, **l**ist files in package `bash`.
        *   `-q`: Query mode.
        *   `-l`: List files option.
    *   `rpm -qf /etc/passwd`: (`dnf`) **q**uery package owning **f**ile `/etc/passwd`.
        *   `-q`: Query mode.
        *   `-f`: Query package owning file option.

***
Software installation time! Gotta install, update, remove tools. Let's practice with *my* package manager (APT or DNF/YUM). 📦

**🎯 Mission 4: Package Power-Up!**

1.  Refresh package lists! Command for my system? (`sudo apt update` or `sudo dnf check-update`). Do this *every time*!
2.  Find a fun/useful CLI tool. Search "command line file browser" or "ascii art". Examples: `tree`, `ncdu` (disk usage!), `cowsay`, `sl`. Use `apt search <term>` or `dnf search <term>`.
3.  Pick one (`tree`?). Get info (`apt show tree` or `dnf info tree`). What's it do? Version?
4.  Install it! (`sudo apt install tree` or `sudo dnf install tree`). Did it pull dependencies?
5.  Run it! Try `tree` in home dir. `tree /etc`. (If `cowsay`, try `cowsay "Linux is Fun!"`).
6.  Where did it install files? (`dpkg -L tree` or `rpm -ql tree`).
7.  Playtime over. Remove it (`sudo apt remove tree` or `sudo dnf remove tree`).
8.  Leftover dependencies? Clean 'em up (`sudo apt autoremove` or `sudo dnf autoremove`).
9.  Check package manager log. Where? (`/var/log/apt/history.log` or `/var/log/dnf.log`). `less` it to see install/remove actions.

Mastering my package manager is fundamental. Keeping things updated = Security Job #1!
***

---

## Playbook Level 5: Networking

**My Goal:** Check network setup, test connections, DNS, secure transfers. Gotta connect! 🌐

*   **IP/Interface Info:** My system's network address and devices.
    *   `ip addr show` or `ip a`: Show interface information. **Standard tool.**
        *   `ip`: Modern network configuration command suite.
        *   `addr` or `a`: Subcommand for address/interface information.
        *   `show`: Default action, displays info.
    *   `ip route show`: Display routing table, crucial for finding the **default gateway**.
        *   `ip`: Network command suite.
        *   `route` or `r`: Subcommand for routing table.
        *   `show`: Default action.

*   **Connectivity Tests:** Reaching out.
    *   `ping 8.8.8.8`: Send ICMP echo requests to check reachability/latency.
        *   `ping`: Command to send ICMP ECHO_REQUEST packets.
        *   `8.8.8.8`: Target IP address (Google Public DNS). (`Ctrl+C` stops).
    *   `traceroute example.com`: Show the network hops (routers) packets take.
        *   `traceroute`: Command to trace the network path.
        *   `example.com`: Target hostname.
    *   `mtr google.com`: Live `ping` + `traceroute`. Interactive & informative.
        *   `mtr`: **M**y **Tr**aceroute command. Combines ping and traceroute.
        *   `google.com`: Target hostname.

*   **DNS Lookup:** Name to Address resolution.
    *   `dig www.google.com`: Query DNS for info.
        *   `dig`: **D**omain **I**nformation **G**roper - detailed DNS query tool.
        *   `www.google.com`: Hostname to query. (Defaults usually to A record).
    *   `dig AAAA example.com`: Query for IPv6 address (AAAA record).
        *   `AAAA`: Specify the record type to query.
    *   `dig MX google.com`: Query for Mail Exchanger (MX) records.
        *   `MX`: Specify Mail Exchanger record type.
    *   `host example.com`: Simpler DNS query tool.
    *   `cat /etc/resolv.conf`: View the system's configured DNS nameservers file.

*   **Check Connections/Listening Ports:** What's running on the network?
    *   `ss -tulnp`: **MEMORIZE!** **S**ocket **S**tats: **t**cp, **u**dp, **l**istening, **n**umeric, **p**rocess. **Essential.**
        *   `ss`: The command.
        *   `-t`: Show TCP sockets.
        *   `-u`: Show UDP sockets.
        *   `-l`: Show only listening sockets.
        *   `-n`: Show numeric addresses/ports (don't resolve names).
        *   `-p`: Show the process (program) using the socket.
    *   `ss -tan`: Show **a**ll **t**cp sockets (listening & connected), **n**umeric.
    *   `netstat -tulnp`: Older equivalent, similar flags.

*   **Secure Shell (SSH):** Encrypted remote command line.
    *   `ssh myuser@remote.server.com`: Connect to remote as `myuser`.
    *   `ssh -p 2222 myuser@other.server.org`: Connect using (`-p`) non-standard port `2222`.
    *   **SSH Keys:** Better security/convenience.
        *   `ssh-keygen -t ed25519 -C "my_email@example.com"`: Generate key pair.
            *   `ssh-keygen`: Command to generate keys.
            *   `-t ed25519`: Specify key **t**ype (ED25519 is modern/secure).
            *   `-C "comment"`: Add a **C**omment (often email) to identify key.
        *   `ssh-copy-id myuser@remote.server.com`: Copies your public key to the remote server's `authorized_keys`.
            *   `ssh-copy-id`: Helper script to install public key remotely.

*   **Secure File Transfer:** Moving files over SSH.
    *   `scp my_local_file.txt user@remote:/path/to/destination/`: **S**ecure **C**opy local file *to* remote.
        *   `scp`: The command. Follows `cp` syntax: `source destination`.
        *   `user@remote:/path/...`: Remote destination format.
    *   `scp user@remote:/path/to/remote_file.log .`: Copy remote file *from* server to local current dir (`.`).
    *   `scp -r my_local_directory/ user@remote:/backups/`: Copy directory **r**ecursively. `-r` flag.
    *   `rsync -avz --progress my_local_data/ user@remote:/data_archive/`: **R**emote **Sync**. Efficient for large/repeat transfers.
        *   `rsync`: The command.
        *   `-a`: **a**rchive (recursive, preserve permissions/ownership/times).
        *   `-v`: **v**erbose.
        *   `-z`: Compresses data (**z**ip).
        *   `--progress`: Show progress.
        *   `source` `destination`: Like `cp`.

*   **Basic Firewall:** Control traffic. Varies by distro tool.
    *   **`ufw`** (Ubuntu): Simple commands.
        ```bash
        # Examples
        sudo ufw status verbose  # Check state and rules
        sudo ufw allow ssh       # Allow traffic based on service name (port 22/tcp)
        sudo ufw allow 80/tcp    # Allow specific port and protocol
        ```
    *   **`firewalld`** (RHEL/CentOS): Zone-based. Rules often need `--permanent` then `--reload`.
        ```bash
        # Examples
        sudo firewall-cmd --list-all # See rules for default zone
        sudo firewall-cmd --permanent --add-service=http # Allow HTTP service
        sudo firewall-cmd --reload   # Apply saved permanent rules
        ```

***
Let's get connected! 🌐 Checking IPs, testing connections, moving files securely... standard Ops tasks.

**🎯 Mission 5: Network Navigator!**

1.  Find my IP address & interface name (`ip a`). Note IPv4 (`inet`).
2.  Find default gateway (`ip route`).
3.  Can I reach gateway? `ping <gateway_ip>` (Stop with `Ctrl+C`). What's the `time=`? (Latency).
4.  Reach outside world? `ping 8.8.8.8`. Stop. If this works but `ping google.com` fails, what's likely wrong? (DNS!).
5.  Trace the path! `traceroute google.com` or `tracepath google.com`. Watch hops.
6.  My DNS servers? Check `/etc/resolv.conf`.
7.  Use `dig` for `github.com` A record (`dig github.com A`). Find its mail servers (`dig github.com MX`).
8.  What's *listening*? The magic `ss -tulnp`. Spot `sshd`? Port? Anything else?
9.  **(If I have a second Linux machine/VM or can SSH to localhost):**
    *   Generate SSH keys? `ssh-keygen` (Enter for defaults).
    *   Copy *public* key: `ssh-copy-id my_user@target_host`.
    *   Try SSH login: `ssh my_user@target_host`. Password prompt? (Shouldn't be!). Magic! ✨
    *   Create test file: `echo "SCP test" > scp_test.txt`.
    *   Copy TO target: `scp scp_test.txt my_user@target_host:~`.
    *   Copy FROM target: `scp my_user@target_host:~/scp_test.txt ./scp_test_back.txt`. Verify (`ls`).
    *   Try `rsync`: `rsync -avz scp_test.txt my_user@target_host:~`. Different output? (More verbose about transfer).
10. Check firewall status! (`sudo ufw status` or `sudo firewall-cmd --state` & `--list-all`). Active? Rules?

Networking is vast, but these are my tools for basic checks and secure moves.
***

---

## Playbook Level 6: System Services & Startup (Systemd)

**My Goal:** Manage background services (daemons), understand boot sequence (modern `systemd` way). ⚙️

*   **Systemd Overview:** Init system/service manager. Uses `units`. Configs: `/lib/systemd/system/`, `/etc/systemd/system/`.

*   **Managing Services (`systemctl` - requires `sudo`):** Core command.
    *   `sudo systemctl status nginx.service`: Check service **status**. Active? Enabled? Logs? **Fundamental.**
        *   `systemctl`: The command for interacting with systemd.
        *   `status`: Action to check the current state of a unit.
        *   `nginx.service`: The name of the unit (service) to check. `.service` suffix is often optional.
    *   `sudo systemctl start apache2`: Start the service now.
        *   `start`: Action to activate (start) the unit.
    *   `sudo systemctl stop bluetooth`: Stop the service now.
        *   `stop`: Action to deactivate (stop) the unit.
    *   `sudo systemctl restart sshd`: Stop and then start the service.
        *   `restart`: Action to stop and immediately start the unit.
    *   `sudo systemctl reload php-fpm`: Reload config without full restart (if supported).
        *   `reload`: Action to ask the unit to reload its configuration. Faster/less disruptive than restart if supported.
    *   `sudo systemctl enable cron`: Configure service to start automatically on boot.
        *   `enable`: Action to create links so the service starts in appropriate targets (like multi-user).
    *   `sudo systemctl disable unattended-upgrades`: Prevent service from starting automatically on boot.
        *   `disable`: Action to remove the links, preventing automatic start.
    *   `systemctl is-enabled NetworkManager`: Check if service is configured to start on boot.
        *   `is-enabled`: Action to report the enablement status (enabled/disabled/static etc.).
    *   `systemctl list-units --type=service --all`: List loaded service units (active/inactive).
        *   `list-units`: Action to list currently loaded units.
        *   `--type=service`: Filter for units of type 'service'.
        *   `--all`: Show all loaded units, regardless of state (active, inactive, failed).
    *   `systemctl list-unit-files --type=service`: List available service files and their boot status.
        *   `list-unit-files`: Action to list all unit files found on the system.

*   **Analyzing Boot Process:** Performance tuning.
    *   `systemd-analyze time`: Show kernel vs userspace startup time.
        *   `systemd-analyze`: Command for analyzing boot performance.
        *   `time`: (Default action) Show basic timings.
    *   `systemd-analyze blame`: List units sorted by time taken during boot.
        *   `blame`: Subcommand showing initialization time per unit.
    *   `systemd-analyze critical-chain`: Show dependency chain affecting boot time.
        *   `critical-chain`: Subcommand showing units potentially bottlenecking boot.

*   **Systemd Journal Logging (`journalctl`):** Accessing logs.
    *   `journalctl`: View all journal logs (uses `less`).
    *   `journalctl -u sshd`: Show logs ONLY for `sshd` unit. **Super useful.**
        *   `-u sshd`: Option to filter logs for a specific **u**nit.
    *   `journalctl -f`: **F**ollow new log entries live (`Ctrl+C` stops).
        *   `-f`: Follow option.
    *   `journalctl -b`: Show logs since last **b**oot. `-b -1` for previous.
        *   `-b`: Boot offset option (0 is current, -1 previous, etc.).
    *   `journalctl --since "yesterday"`: Filter logs by start **since** time.
        *   `--since "..."`: Time specification (understands "yesterday", "1 hour ago", "YYYY-MM-DD HH:MM:SS").
    *   `journalctl -p err`: Filter logs by **p**riority (e.g., `err`, `warning`).
        *   `-p err`: Filter for priority `err` (3) and higher (crit/alert/emerg).

*   **Power Management:** System state.
    *   `sudo systemctl reboot`: Cleanly reboot.
    *   `sudo systemctl poweroff`: Cleanly shut down.
    *   `sudo systemctl suspend`: Sleep mode.
    *   `sudo systemctl hibernate`: Save state to disk (needs config).

***
Controlling the daemons! 👻 Making sure services run right, checking health, reading logs.

**🎯 Mission 6: Service Supervisor!**

1.  Pick a service: `cron`, `rsyslog`, `sshd`.
2.  Check its status: `sudo systemctl status cron`. Active (running)? Enabled (boot start)? Note the output.
3.  See its logs via journal: `sudo journalctl -u cron`. What messages? Add `-n 50` for last 50 lines. Try `-f` to follow live (`Ctrl+C` to stop).
4.  Enabled for boot start? `systemctl is-enabled cron`.
5.  **(CAREFUL! Use non-critical service like `cron`, NOT `sshd` if I might lock myself out!)**
    *   Stop it: `sudo systemctl stop cron`.
    *   Check status (`sudo systemctl status cron`). Inactive (dead)?
    *   Start it: `sudo systemctl start cron`.
    *   Check status (`sudo systemctl status cron`). Active?
    *   Reload config: `sudo systemctl reload cron`. Check status again.
6.  System boot time? `systemd-analyze time`.
7.  Slowest boot services? `systemd-analyze blame | less`. Any surprises?
8.  List loaded service units: `systemctl list-units --type=service`. All units (incl inactive): `systemctl list-units --type=service --all`.

`systemctl` is my go-to for services. Gotta know `status`, `start`, `stop`, `enable`, `disable`, and `journalctl -u`.
***

---

## Playbook Level 7: Storage & Filesystems

**My Goal:** Understand disks, partitions, filesystems, manage space. Where does data live? 💾

*   **Check Usage:** Seeing how much space is free/used.
    *   `df -h`: **D**isk **F**ree (**h**uman). Usage for mounted filesystems. **Essential.**
        *   `-h`: Human-readable sizes (K, M, G).
    *   `df -i`: Check **i**node usage (file count limits).
        *   `-i`: Show inode information instead of block usage.
    *   `du -sh /var/log`: **D**isk **U**sage **s**ummary (**h**uman) for `/var/log`. Shows total size.
        *   `du`: Disk usage command.
        *   `-s`: Provide only a **s**ummary (total).
        *   `-h`: Human-readable sizes.
        *   `/var/log`: Path to measure.
    *   `du -h --max-depth=1 /home | sort -rh`: List top-level dirs in `/home` by size.
        *   `--max-depth=1`: Limit `du` recursion depth to 1 level.
        *   `|`: Pipe `du` output to `sort`.
        *   `sort -rh`: Sort numerically (**r**everse, largest first), treat sizes as **h**uman-readable.

*   **Identify Devices:** Knowing what disks/partitions exist.
    *   `lsblk`: **L**i**s**t **Bl**oc**k** Devices. **Best overview**. Tree view of disks, partitions, sizes, mount points.
    *   `sudo blkid`: Show **Bl**ock **ID**s (**UUID** and TYPE). Needed for reliable `fstab`.

*   **Partitioning:** ☠️ **DANGER! Backup first!** ☠️ Dividing disks.
    *   Tools: `fdisk` (MBR), `gdisk` (GPT - use this!), `parted`.
    *   Flow (`sudo gdisk /dev/sdx`): `p` (print table), `d` (delete partition), `n` (new partition), `t` (set type code, e.g., `8300` Linux, `8200` Swap, `8e00` LVM), `w` (WRITE! - final step).

*   **Formatting (Makes Filesystem):** ☠️ **ERASES DATA!** ☠️ Preparing partition.
    *   `sudo mkfs.ext4 /dev/sdb1`: Create **ext4** filesystem.
        *   `mkfs.ext4`: Command to **m**a**k**e **f**ile**s**ystem of type ext4.
        *   `/dev/sdb1`: Target device/partition.
    *   `sudo mkfs.xfs /dev/sdc1`: Create **xfs** filesystem.
    *   `sudo mkswap /dev/sda3`: Initialize partition as **swap**.

*   **Mounting:** Attaching filesystem to directory.
    *   `mount`: Show current mounts.
    *   `sudo mkdir /mnt/point`: Create empty mount point dir.
    *   `sudo mount /dev/sdb1 /mnt/point`: Mount device onto point.
        *   `mount`: The mount command.
        *   `/dev/sdb1`: Device containing the filesystem.
        *   `/mnt/point`: Existing directory to attach filesystem to.
    *   `sudo umount /mnt/point` or `sudo umount /dev/sdb1`: Unmount. Fails if busy!
        *   `umount`: The unmount command.
    *   `sudo lsof /mnt/point`: **L**ist **O**pen **F**iles on path (find process holding mount).

*   **Persistent Mounts (`/etc/fstab`):** ☠️ **CRITICAL FILE!** ☠️ Mount on boot.
    *   Backup: `sudo cp /etc/fstab /etc/fstab.bak.$(date +%F)`
    *   Format: `UUID=<uuid> <mount_point> <type> <options> <dump> <pass>`
    *   Test after edit: `sudo mount -a` (attempts to mount all non-mounted fstab entries). Fix any reported errors immediately!

*   **Swap:** `swapon --show` (list active), `free -h` (see usage).
*   **LVM:** PV -> VG -> LV. `pvcreate`, `vgcreate`, `lvcreate`, `lvextend`, etc.

***
Where does the data live? 💾 Managing disks, partitions, filesystems. Let's check my storage.

**🎯 Mission 7: Disk Duty!**

1.  Disk space used? Human-readable! (`df -h`). Note usage for `/`.
2.  Physical/virtual disks & partitions? `lsblk`. Match devices to mount points in `df`?
3.  What's big under `/var`? Use `du` summary trick: `sudo du -sh /var/* | sort -rh | head -n 10`. Try for my home dir too (`du -sh ~/* | ...`).
4.  The boot mount file: `less /etc/fstab`. Spot the line for root (`/`)? Using `UUID=`? (Should be!).
5.  Find UUID for root device. `lsblk` finds device (e.g., `/dev/sda2`), then `sudo blkid | grep /dev/sda2`. Match UUID in fstab?
6.  **(Optional & CAREFUL - Only with a *test* VM disk I added!):**
    *   Identify *unused* test disk (`/dev/sdb`?) with `lsblk`. **SURE it's empty!**
    *   `sudo fdisk /dev/sdb` or `sudo gdisk /dev/sdb`.
    *   Print table (`p`). Create *one* new Linux partition (`n`, defaults, type `83`/`8300` via `t`).
    *   Print (`p`) again. **Write (`w`)!**
    *   Format it (e.g., `/dev/sdb1`): `sudo mkfs.ext4 /dev/sdb1`.
    *   Create mount point: `sudo mkdir /mnt/testdata`.
    *   Mount it: `sudo mount /dev/sdb1 /mnt/testdata`.
    *   Verify: `df -h`, `lsblk`. See it mounted?
    *   Create file: `sudo touch /mnt/testdata/hello.txt`.
    *   Unmount: `sudo umount /mnt/testdata`. Mount again.
    *   **(Super Bonus - fstab):** Backup fstab! Get UUID (`sudo blkid | grep /dev/sdb1`). Add line to `/etc/fstab`: `UUID=... /mnt/testdata ext4 defaults 0 2`. Test: `sudo mount -a`. Then `sudo umount /mnt/testdata` and *remove the line*! Restore backup if needed.
    *   Clean up partition table on test disk? (`fdisk/gdisk` `d` delete, `w` write).

Storage commands `df`, `du`, `lsblk`, and understanding `/etc/fstab` are vital!
***

---

## Playbook Level 8: Logs & Monitoring

**My Goal:** Find/read system logs, basic performance monitoring. What's happening? 🕵️‍♂️

*   **Log Locations (`/var/log`):** Traditional text files.
    *   `syslog` / `messages`: General events.
    *   `auth.log` / `secure`: **Security/Login**. Crucial!
    *   `dmesg`: Kernel messages (use `dmesg` command).
    *   Package logs: `apt/`, `dnf.log`.
    *   Application logs: `nginx/`, `mysql/`, etc.
*   **Viewing Logs:** Reading text logs.
    *   `less <logfile>`: Page through.
    *   `sudo tail -f <logfile>`: Follow live (`Ctrl+C` stops). **Useful.**
    *   `sudo grep -i "pattern" <logfile>`: Search within log.
    *   `dmesg`: View kernel buffer. `dmesg -T` adds timestamps.

*   **Systemd Journal (`journalctl`):** Centralized system/service logs.
    *   `journalctl`: View all (newest at bottom).
    *   `journalctl -u <service_name>`: Filter by service. **Primary tool.**
    *   `journalctl -b`: Logs since last **b**oot.
    *   `journalctl -p err`: Filter by **p**riority (e.g., `err`, `warning`).
    *   `journalctl -f`: Follow journal updates live.

*   **Log Rotation (`logrotate`):** Manages log file size. Auto-runs via cron. Configs `/etc/logrotate.conf`, `/etc/logrotate.d/`.

*   **Basic Performance Checks:** Quick glance at health.
    *   `uptime`: Uptime & Load Average (1, 5, 15 min). Load < #CPUs is good.
    *   `free -h`: Memory & Swap usage (**h**uman). Check `available` RAM and `Swap` usage.
    *   `vmstat 1 5`: Quick stats (CPU: `us`,`sy`,`id`,`wa` I/O Wait%; Mem: `si`,`so` Swap I/O; Disk: `bi`,`bo`). Run for 5 seconds.
    *   `iostat -xz 1 5`: Disk I/O details (need `sysstat`). Check `%util`, `r/s`, `w/s`. `-x` = extended, `-z` = hide idle.
    *   `top`/`htop`: Real-time process resources.

***
What's happening? 🕵️‍♂️ Logs tell the story, monitoring gives a dashboard.

**🎯 Mission 8: Log Lookout & Performance Peeking!**

1.  Open two terminals. Term 1: watch auth log: `sudo tail -f /var/log/auth.log` (or `secure`).
2.  Term 2: try bad login: `ssh doesnt_exist@localhost`. Permission denied? Look at Term 1! See failure logged?
3.  Term 2: run `sudo echo test`. Look at Term 1 again. See `sudo` usage logged? (`Ctrl+C` in Term 1).
4.  Search main system log (`syslog`/`messages`) for `error/warn/fail` (case-insensitive) in last 100 lines: `sudo journalctl -p err..warn -n 100` or `sudo grep -iE 'error|warn|fail' /var/log/syslog | tail -n 100`. Worrying signs?
5.  Kernel messages: `dmesg | less`. Look for anything related to your disk drives (`sda`, `nvme`) or network cards (`eth`, `enp`). (`q` to exit `less`).
6.  Check system load: `uptime`. Note the three load average numbers.
7.  Check memory usage: `free -h`. How much memory is "available"? Is any swap being used? (Ideally swap used should be 0 or low).
8.  Install `sysstat` if needed (`sudo apt install sysstat` / `sudo dnf install sysstat`).
9.  Run `vmstat 2 5`. Watch the `us` (user cpu), `sy` (system cpu), `id` (idle cpu), and `wa` (wait I/O) columns. Also look at `si`/`so` (swap in/out - want 0!).
10. Run `iostat -xz 2 5`. Watch the `%util` for your main disk (`sda`, `nvme0n1`). This shows how busy the disk is. Also look at `r/s` (reads/sec) and `w/s` (writes/sec).

Knowing logs and basic perf tools (`uptime`, `free`, `vmstat`, `iostat`) is crucial!
***

---

## Playbook Level 9: Shell Scripting Basics & Automation

**My Goal:** Automate simple tasks with shell scripts (`bash`). Make the computer work for ME! 🤖

*   **Script Basics:** Create text file (`.sh`), first line `#!/bin/bash`, `chmod +x file`, run `./file`. `#` for comments.
*   **Variables:** Store data.
    ```bash
    MY_NAME="Admin"          # Assign string (no spaces around =)
    echo "Hello, $MY_NAME"   # Use variable ($) inside double quotes
    echo 'Literal: $MY_NAME' # Single quotes print literally
    ```
*   **Command Substitution:** Capture command output into variable or use inline.
    ```bash
    NOW=$(date)                # Capture output of 'date' into NOW variable
    echo "Report generated on: $NOW"
    echo "Users logged in: $(who | wc -l)" # Use output directly in string
    ```
*   **User Input:** Get data from user running script.
    ```bash
    read -p "Enter filename: " FILENAME # -p shows prompt before reading
    echo "Processing file: $FILENAME"
    ```
*   **Arguments:** Access command-line parameters passed to the script (`./script.sh arg1 arg2`).
    *   `$1`, `$2`, ... : First arg, second arg, etc.
    *   `$0` : Name script was run with.
    *   `$#` : Number of arguments passed.
    *   `$@` : All arguments as separate strings (e.g., `for arg in "$@"`).
    *   `$*` : All arguments as a single string.
*   **Conditionals (`if`):** Make decisions based on tests. Use `[[ ... ]]` and quote variables!
    *   Tests: `-f`(file), `-d`(dir), `-z`(empty var), `$A == $B`, `$N -eq 10`.
    *   Logic: `!`(NOT), `&&`(AND), `||`(OR).
    *   ```bash
        TARGET="$1" # Assign first argument to variable TARGET
        if [[ -z "$TARGET" ]]; then # Is TARGET empty (-z)?
          echo "Error: No target specified!" >&2 # Print error to stderr
          exit 1 # Exit with error code
        elif [[ -f "$TARGET" ]]; then # Else if TARGET is a file (-f)?
          echo "$TARGET is a file."
        elif [[ -d "$TARGET" ]]; then # Else if TARGET is a directory (-d)?
          echo "$TARGET is a directory."
        else # Otherwise
          echo "$TARGET does not exist or is not a file/directory."
        fi
        ```
*   **Loops (`for`, `while`):** Repeat blocks of code.
    *   `for` loop: Iterate over items.
        ```bash
        # Iterate over a list of strings
        for item in one two three; do echo "Item: $item"; done
        # Iterate over files matching a pattern
        for file in *.log; do echo "Processing $file"; done
        # C-style number loop
        for (( i=0; i<3; i++ )); do echo "Number $i"; done
        ```
    *   `while` loop: Repeat while condition is true.
        ```bash
        COUNTER=0
        while [[ $COUNTER -lt 5 ]]; do
          echo "Current count: $COUNTER"
          (( COUNTER++ )) # Increment using ((...)) arithmetic context
        done
        ```
*   **Redirection & Pipes (`>`, `>>`, `2>`, `&>`, `<`, `|`):** Control input/output streams. **Crucial!**
    *   `ls -l > file.txt`: Redirect `ls` stdout to `file.txt`, overwriting.
    *   `date >> log.txt`: Append date stdout to `log.txt`.
    *   `find / -name x 2> errors.txt`: Redirect find's stderr (errors) to `errors.txt`.
    *   `./script.sh &> output_and_errors.log`: Redirect both stdout & stderr to file.
    *   `sort < names.txt`: Feed `names.txt` into `sort`'s stdin.
    *   `cat file.txt | grep "WARN" | wc -l`: **Pipe!** `cat` output -> `grep` input -> `wc` input. Counts lines containing "WARN".

*   **Functions:** Create reusable named blocks of code.
    ```bash
    #!/bin/bash
    function check_file() {
      # Use local vars inside functions
      local target_file="$1" # Assign function's first arg
      if [[ -f "$target_file" ]]; then
        echo "File '$target_file' exists."
      else
        echo "File '$target_file' not found."
      fi
    }
    # Call the function with an argument
    check_file "/etc/hosts"
    check_file "/nonexistent"
    ```

***
Time to automate! Turn commands into reusable scripts. 🤖

**🎯 Mission 9: Scripting Success!**

1.  Create `sys_info.sh`. Make executable (`chmod +x sys_info.sh`).
2.  Edit it (`nano sys_info.sh`):
    ```bash
    #!/bin/bash
    # Script to display basic system info
    echo "--- My System Info ---"
    echo "Hostname: $(hostname)"
    echo "User: $(whoami)"
    echo "Date: $(date)"
    echo "Uptime: $(uptime -p)" # Pretty uptime
    echo "--- Memory ---"
    free -h
    echo "--- Root Disk Usage ---"
    df -h /
    echo "----------------------"
    ```
3.  Save & run: `./sys_info.sh`. My personal dashboard! 😎
4.  Create `checker.sh`. Make executable.
5.  Edit `checker.sh` for the mission:
    *   Takes one argument (`$1`).
    *   First check if argument is missing (`if [[ -z "$1" ]]`): Print usage `Usage: $0 <directory_path>` to stderr (`>&2`) and `exit 1`.
    *   Then check if argument is a directory (`if [[ -d "$1" ]]`). **Quote the vars!**
    *   If yes: print "Analyzing: $1", then run `ls -lh "$1"` and `du -sh "$1"`.
    *   If no: print error "Error: '$1' not a directory." to stderr (`>&2`) and `exit 1`.
6.  Test it!
    *   `./checker.sh` (-> usage error)
    *   `./checker.sh /etc` (-> should work)
    *   `./checker.sh /etc/hosts` (-> 'not a directory' error)
    *   `./checker.sh /no/such/dir` (-> 'not a directory' error)
7.  **Bonus:** Script `findlogs.sh`. Uses `for f in /var/log/*.log; do ... done` to loop. Inside loop: `echo "--- $f ---"; tail -n 5 "$f"`. Run with `sudo` if needed.

Scripting = Automation Power! Start simple, build up. Variables, `if`, `for`, pipes are key.
***

---

## Playbook Level 10: Security Essentials

**My Goal:** Basic security hygiene & hardening practices. Locking things down! 🛡️ (Crucial Basics).

*   **Keep Updated:** Patch vulnerabilities frequently.
    ```bash
    # Debian/Ubuntu: Refresh lists and upgrade packages, auto-yes
    sudo apt update && sudo apt upgrade -y
    # RHEL/CentOS/Fedora: Update packages, auto-yes
    sudo dnf update -y
    ```
*   **Users/Passwords:** Principle of Least Privilege.
    *   Strong passwords; Use **SSH Keys** (disable password auth).
    *   Remove/Lock unused accounts: `sudo userdel <user>`, `sudo usermod -L <user>`.
*   **Minimize Surface:** Install only needed software; disable unused services.
    *   Check listening ports: `sudo ss -tulnp`. Close unnecessary ports via firewall/disabling service.
*   **`sudo` Config:** Use `visudo`. Grant access via groups (`%sudo`/`%wheel`), not individual users if possible. Be specific with commands allowed.
*   **Harden SSH (`/etc/ssh/sshd_config` & reload `sudo systemctl reload sshd`):**
    *   `PermitRootLogin no`: **MUST HAVE**. Don't allow root login.
    *   `PasswordAuthentication no`: **MUST HAVE** *after* keys work. Use keys only.
    *   Consider non-default `Port <num>`: Reduces log spam.
    *   Use `Fail2ban`: Install (`sudo apt/dnf install fail2ban`) and enable (`sudo systemctl enable --now fail2ban`). Auto-blocks brute-force IPs.
*   **Firewall:** Enable! (`sudo ufw enable` / `sudo systemctl enable --now firewalld`). Default policy should be to deny incoming traffic. Explicitly `allow` only necessary services/ports (like SSH!).
*   **Check Logs:** Monitor `auth.log`/`secure` (`journalctl -u sshd`, etc.) for failed attempts, unusual activity.
*   **Permissions:** Use `chmod` appropriately. NO `chmod 777`! Keys should be `600`. Web files need proper ownership/perms.
*   **Backups:** Essential! `rsync`, `tar`, dedicated tools. Regularly test restores!

***
Locking things down! 🛡️ Security is ongoing. Let's check basics.

**🎯 Mission 10: Security Scan!**

1.  Review listening ports: `sudo ss -tulnp`. Each port: What is it? Do I NEED it? Research unknowns.
2.  Examine SSH config: `sudo less /etc/ssh/sshd_config`.
    *   `PermitRootLogin`: Is it `no` or `prohibit-password`? (Good!). Change if `yes`?
    *   `PasswordAuthentication`: Is it `no`? (Excellent if using keys!). Change if `yes`?
    *   `Port`: Default `22`? (Okay).
3.  Check firewall: `sudo ufw status verbose` or `sudo firewall-cmd --list-all`. Default deny incoming? Only needed ports allowed?
4.  Last update? Check log (`/var/log/apt/history.log` or `dnf.log`). Been a while? Update now! `sudo apt update && sudo apt upgrade -y` or `sudo dnf update -y`.
5.  Rootkit check (basic scan): Install `chkrootkit rkhunter`. Update: `sudo rkhunter --update`. Scan: `sudo chkrootkit`, `sudo rkhunter --check --sk`. Review warnings.
6.  Review `sudo` access: Use `sudo visudo` to view rules. Is access granted via groups (`%sudo`, `%wheel`)?

Basic security: Update, firewall, minimal services, strong access control. Constant vigilance!
***

---

## Playbook Level 11: Advanced Topics (My Next Frontiers!) 🚀

**My Goal:** Know where to explore next. The journey continues!

*   **Text Power Tools:** Master `sed` (stream editor), `awk` (column processor), `grep` + Regex.
    ```bash
    # sed: substitute 'foo' with 'bar' globally (-g)
    sed 's/foo/bar/g' input.txt
    # awk: print first ($1) and third ($3) space-separated fields
    awk '{print $1, $3}' data.txt
    ```
*   **Version Control (`git`):** Essential! Manage code, scripts, configs. `clone`, `add`, `commit`, `push`, `pull`, `branch`.
    ```bash
    # Basic flow example
    git clone <repo_url>
    cd <repo_dir>
    # ... make changes ...
    git add changed_file.txt new_script.sh
    git commit -m "Made changes to script X"
    git push origin main
    ```
*   **Configuration Management:** Automate server config! **Ansible** (YAML, agentless), Puppet, Chef, Salt. Crucial for scaling!
*   **Virtualization:** KVM/libvirt (`virsh` cli, `virt-manager` gui). Run full VMs.
*   **Containers:** **Docker** / Podman. Package apps + dependencies. Lightweight, fast. `run`, `build`, `ps`, `compose`.
    ```bash
    # Build docker image from Dockerfile in current dir
    docker build -t myapp:v1 .
    # Run container in background (-d), map host port 8080 to container 80 (-p)
    docker run -d -p 8080:80 --name web myapp:v1
    ```
*   **Monitoring:** **Prometheus + Grafana** (metrics + dashboards), Zabbix, Nagios. Watch systems, get alerts.
*   **Centralized Logging:** Elastic Stack (ELK), Graylog, Loki. Aggregate logs.
*   **Adv. Networking:** VLANs, Bonding, Routing basics, VPNs (WireGuard!).
*   **Kernel Tuning (`sysctl`):** Tweak kernel params (`/proc/sys/`, `/etc/sysctl.conf`). Needs deep understanding!
*   **Performance:** `perf`, `strace` (syscalls), `gdb` (debugger).
*   **Cloud (AWS, Azure, GCP):** Core skill. Learn VMs, storage, network, IAM for your provider.

---

## My Path Forward (Conclusion)

This playbook is my detailed foundation! The real learning comes from **DOING**.

1.  **Do the Missions!** Type the commands, understand them, see the output. Break things (in lab!), learn to fix.
2.  **Understand WHY!** Read `man` pages for options. Why this command? When *not*?
3.  **Build Something!** Web server, file server, backup script. Apply knowledge.
4.  **Go Deeper:** Specialize in areas like Automation, Security, Cloud.
5.  **Read Docs & Ask:** Official docs, Stack Exchange/Server Fault, Reddit communities.
6.  **Stay Curious!** Linux & tech evolve constantly. Embrace learning!

Time to get hands-on and truly own this command line! 💪

