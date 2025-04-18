# My Ultimate Linux Sysadmin Playbook (v1.2 - Extra Detailed!) 🐧🔥

Alright, let's DO this! This is my personal playbook for conquering the Linux command line, from the absolute basics to becoming a comfortable sysadmin. Forget clicking around – the real power is in the terminal! This guide includes learning sections **with inline command examples *and detailed breakdowns***, plus hands-on missions to make sure the knowledge sticks. Time to fire up that terminal! 💻

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
(Practice Mission 0 unchanged)
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
    *   `rm -r old_project/`: Remove directory `old_project` and all its contents **r**ecursively.
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
(Practice Mission 1 unchanged)
***

---

## Playbook Level 2: Users, Groups & Permissions

**My Goal:** Understand the security model – who owns what, who can do what. Crucial stuff! 🔒

*   **Accounts & Info Files:** User/Group ID system.
    *   User: Has UID, primary GID. `root`=UID 0.
    *   Info Files: `/etc/passwd` (users), `/etc/shadow` (passwords!), `/etc/group` (groups). Don't edit directly unless expert!
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
    *   `sudo passwd charlie`: Set (or change) password for `charlie`.
        *   `sudo`: Run as superuser.
        *   `passwd`: Command to manage passwords.
        *   `charlie`: The user whose password to set (prompts for new password twice).
    *   `sudo usermod -aG developers charlie`: **A**dd `charlie` to the **G**roup `developers`.
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

*   **File Permissions (`ls -l` -> `-rwxr-xr--`):** Decoding the string.
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
(Practice Mission 2 unchanged)
***

---

## Playbook Level 3: Process Management

**My Goal:** See what's running, manage programs, stop them if needed. Keeping tabs! 🤠

*   **Process:** Running instance of a program (PID, PPID, owner, resources).

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
    *   `jobs`: List active background jobs started in *this* shell session.
    *   `Ctrl+Z`: (Press keys) Suspend the currently running foreground job. Puts it in "Stopped" state.
    *   `bg %1`: Resume suspended job number `1` in the **b**ack**g**round.
    *   `fg %1`: Bring job number `1` (background or stopped) to the **f**ore**g**round.
    *   `nohup ./long_process.sh &`: Run command immune to **no** **h**ang**up**, in background. Output goes to `nohup.out`.

***
(Practice Mission 3 unchanged)
***

---

## Playbook Level 4: Package Management

**My Goal:** Install, update, remove software using my system's manager (APT or DNF/YUM). Handles dependencies automatically! 📦

*   **Know Your System!** `apt` (Debian/Ubuntu) vs `dnf`/`yum` (RHEL/Fedora/CentOS).

1.  **APT (Debian/Ubuntu) - Requires `sudo`:**
    *   `sudo apt update`: **ALWAYS FIRST!** Resynchronize package index files from sources.
    *   `sudo apt upgrade`: Upgrade installed packages to available newer versions.
    *   `sudo apt full-upgrade`: Like `upgrade`, but may remove packages if needed to resolve conflicts (use carefully).
    *   `sudo apt install tree wget curl`: Install the packages `tree`, `wget`, `curl`. `install` is the action, package names are arguments.
    *   `sudo apt remove nano`: Remove package `nano`. `remove` is the action. Config files might stay.
    *   `sudo apt purge apache2-utils`: Remove `apache2-utils` AND its global configs. `purge` is the action.
    *   `sudo apt autoremove`: Remove automatically installed dependencies that are no longer needed. `autoremove` is the action.
    *   `apt search "http server"`: Search package names/descriptions for the term "http server". `search` is the action.
    *   `apt show nginx`: Show details about the package `nginx`. `show` is the action.

2.  **DNF (RHEL/Fedora/CentOS) - Requires `sudo`:** (`yum` is similar on older systems).
    *   `sudo dnf check-update`: Check if updates are available for installed packages.
    *   `sudo dnf update`: Apply all available updates. `-y` auto-answers yes.
    *   `sudo dnf install tmux vim-enhanced`: Install `tmux` and `vim-enhanced`. `install` is the action.
    *   `sudo dnf remove httpd-tools`: Remove `httpd-tools`. `remove` is the action.
    *   `sudo dnf autoremove`: Remove unneeded dependencies. `autoremove` is the action.
    *   `dnf search "text editor"`: Search packages for "text editor". `search` is the action.
    *   `dnf info htop`: Show details about `htop`. `info` is the action.

3.  **Lower-Level Tools:** What `apt`/`dnf` use underneath.
    *   `dpkg -l`: (`apt` systems) **l**ist installed packages.
    *   `dpkg -L coreutils`: (`apt`) **L**ist files owned by `coreutils`.
    *   `dpkg -S /bin/ls`: (`apt`) Find package owning (`-S`) `/bin/ls`.
    *   `rpm -qa`: (`dnf` systems) List (**q**uery **a**ll) installed packages.
    *   `rpm -ql bash`: (`dnf`) **q**uery, **l**ist files owned by `bash`.
    *   `rpm -qf /etc/passwd`: (`dnf`) **q**uery package owning **f**ile `/etc/passwd`.

***
(Practice Mission 4 unchanged)
***

---

## Playbook Level 5: Networking

**My Goal:** Check network setup, test connections, DNS, secure transfers. Gotta connect! 🌐

*   **IP/Interface Info:** My system's network address and devices.
    *   `ip addr show` or `ip a`: Show interface information. **Standard tool.** Look for `inet` (IPv4) and `inet6` addresses, `link/ether` (MAC).
    *   `ip route show`: Display routing table, crucial for finding the **default gateway**.

*   **Connectivity Tests:** Reaching out.
    *   `ping 8.8.8.8`: Send ICMP echo requests to check reachability and round-trip time (latency). Use `Ctrl+C` to stop.
    *   `traceroute example.com`: Trace the path (routers/hops) packets take to reach a destination.
    *   `mtr google.com`: Live `ping` + `traceroute`. Interactive & informative. Install if needed (`sudo apt/dnf install mtr`).

*   **DNS Lookup:** Name to Address resolution.
    *   `dig www.google.com`: Query DNS for info about `www.google.com`. By default, gets A record (IPv4).
        *   `dig`: The **D**omain **I**nformation **G**roper tool.
    *   `dig AAAA example.com`: Query for IPv6 address (AAAA record).
    *   `dig MX google.com`: Query for Mail Exchanger (MX) records.
    *   `host example.com`: Simpler DNS query tool.
    *   `cat /etc/resolv.conf`: View the system's configured DNS nameservers.

*   **Check Connections/Listening Ports:** What's running on the network?
    *   `ss -tulnp`: **MEMORIZE!** **S**ocket **S**tats: **t**cp, **u**dp, **l**istening, **n**umeric, **p**rocess. Shows which programs are listening on which ports. **Essential.**
    *   `ss -tan`: Show **a**ll **t**cp sockets (listening & connected), **n**umeric. See active connections.
    *   `netstat -tulnp`: Older equivalent of `ss -tulnp`. Still very common.

*   **Secure Shell (SSH):** Encrypted remote command line.
    *   `ssh myuser@remote.server.com`: Connect to `remote.server.com` as `myuser`.
    *   `ssh -p 2222 myuser@other.server.org`: Connect using non-standard (`-p`) port `2222`.
    *   **SSH Keys:** More secure & convenient than passwords.
        *   `ssh-keygen -t ed25519 -C "my_email@example.com"`: Generate modern ED25519 key pair. `-t` specifies type, `-C` adds a comment. Use strong passphrase! Creates `~/.ssh/id_ed25519` (private) and `~/.ssh/id_ed25519.pub` (public).
        *   `ssh-copy-id myuser@remote.server.com`: Copies your public key (`~/.ssh/id_*.pub`) to the remote server's `~/.ssh/authorized_keys` file.
    *   **Harden SSH Server:** Edit `/etc/ssh/sshd_config` (`sudo`). Changes need `sudo systemctl reload sshd`.
        *   `PasswordAuthentication no`: Disables password login (use keys only!).
        *   `PermitRootLogin no`: Prevent direct root login.

*   **Secure File Transfer:** Moving files over SSH.
    *   `scp my_local_file.txt user@remote:/path/to/destination/`: **S**ecure **C**opy local file *to* remote.
        *   `scp`: The command.
        *   `my_local_file.txt`: Source file.
        *   `user@remote:/path/...`: Destination (user@host:path).
    *   `scp user@remote:/path/to/remote_file.log .`: Copy remote file *from* server to current local dir (`.`).
    *   `scp -r my_local_directory/ user@remote:/backups/`: Copy directory **r**ecursively.
        *   `-r`: Recursive option.
    *   `rsync -avz --progress my_local_data/ user@remote:/data_archive/`: **R**emote **Sync** data. More efficient for repeated syncs.
        *   `rsync`: The command.
        *   `-a`: **a**rchive mode (recursive, preserves permissions, times, etc.).
        *   `-v`: **v**erbose output.
        *   `-z`: Compresses data during transfer (**z**ip).
        *   `--progress`: Show progress during transfer.
        *   `my_local_data/`: Source directory.
        *   `user@remote:/data_archive/`: Destination.

*   **Basic Firewall:** Control network access. Commands vary by tool.
    *   **`ufw`** (Ubuntu): Easy interface.
        ```bash
        sudo ufw status verbose # Detailed status
        sudo ufw enable         # Turn on
        sudo ufw allow ssh      # Allow by service name (uses /etc/services)
        sudo ufw allow 80/tcp     # Allow specific port/protocol
        sudo ufw deny from 1.2.3.4 # Deny all traffic from an IP
        sudo ufw delete allow 443 # Delete a specific rule
        ```
    *   **`firewalld`** (RHEL/CentOS): Zone-based firewall.
        ```bash
        sudo firewall-cmd --state        # Check running state
        sudo firewall-cmd --list-all    # List config for default zone
        # Use --permanent to save rules, then --reload to apply
        sudo firewall-cmd --permanent --add-service=https
        sudo firewall-cmd --permanent --add-port=8443/tcp
        sudo firewall-cmd --reload
        ```

***
(Practice Mission 5 unchanged)
***

---

## Playbook Level 6: System Services & Startup (Systemd)

**My Goal:** Manage background services (daemons), understand boot sequence (modern `systemd` way). ⚙️

*   **Systemd Overview:** Manages `units` (`.service`, `.target` etc.). Configs in `/lib/systemd/system/` (defaults), `/etc/systemd/system/` (customizations).

*   **Managing Services (`systemctl` - requires `sudo`):** Core command.
    *   `sudo systemctl status nginx.service`: Check service status (active? enabled? logs?). **Fundamental command.** `.service` often optional.
    *   `sudo systemctl start apache2`: Start the service now.
    *   `sudo systemctl stop bluetooth`: Stop the service now.
    *   `sudo systemctl restart sshd`: Stop and then start the service. For major changes.
    *   `sudo systemctl reload php-fpm`: Tell service to reload configuration (if supported). Graceful way for minor tweaks.
    *   `sudo systemctl enable cron`: Configure service to start automatically on boot.
    *   `sudo systemctl disable unattended-upgrades`: Prevent service from starting automatically on boot.
    *   `systemctl is-enabled NetworkManager`: Check if service is set to start on boot.
    *   `systemctl list-units --type=service --all`: List all loaded service units (active/inactive).
    *   `systemctl list-unit-files --type=service`: List all available service files and their boot status (enabled/disabled).

*   **Analyzing Boot Process:** How fast did it start?
    *   `systemd-analyze time`: Show kernel vs userspace startup time.
    *   `systemd-analyze blame`: List units sorted by time taken during boot. Identifies slow services.
    *   `systemd-analyze critical-chain`: Show dependency chain affecting boot time.

*   **Systemd Journal Logging (`journalctl`):** Central log access.
    *   `journalctl`: View all logs (uses `less`).
    *   `journalctl -u sshd`: Show logs ONLY for `sshd` unit. **Super useful.**
    *   `journalctl -f`: **F**ollow new log entries live (`Ctrl+C` stops).
    *   `journalctl -b`: Show logs since last **b**oot. `-b -1` for previous boot.
    *   `journalctl --since "yesterday"`: Filter logs by time.
    *   `journalctl -p err`: Filter logs by **p**riority (e.g., `err`, `warning`, `notice`, `info`, `debug`). `err..crit` for range.

*   **Power Management:** System state control.
    *   `sudo systemctl reboot`: Cleanly reboot.
    *   `sudo systemctl poweroff`: Cleanly shut down.
    *   `sudo systemctl suspend`: Sleep mode (low power, RAM active).
    *   `sudo systemctl hibernate`: Save state to disk, power off (needs setup).

***
(Practice Mission 6 unchanged)
***

---

## Playbook Level 7: Storage & Filesystems

**My Goal:** Understand disks, partitions, filesystems, manage space. Where does data live? 💾

*   **Check Usage:** How much free/used space?
    *   `df -h`: **D**isk **F**ree (**h**uman-readable). **Primary command** to check space on mounted filesystems.
    *   `df -i`: Check **i**node usage (limits number of files).
    *   `du -sh /var/log`: **D**isk **U**sage **s**ummary (**h**uman) for `/var/log`. Shows total size.
    *   `du -h --max-depth=1 /home | sort -rh`: List top-level directories in `/home` by size (human, recursive sort). Helps find big directories.

*   **Identify Devices:** What disks/partitions are present?
    *   `lsblk`: **L**i**s**t **Bl**oc**k** Devices. **Best overview**. Shows tree of disks, partitions, sizes, mount points.
    *   `sudo blkid`: Show **Bl**ock **ID**s (UUID and TYPE). **Use UUIDs for fstab**.

*   **Partitioning:** ☠️ **DANGER! Backup first!** ☠️ Dividing disks.
    *   Tools: `fdisk` (MBR), `gdisk` (GPT - use this!), `parted`.
    *   Flow (`sudo gdisk /dev/sdx`): `p` (print), `d` (delete), `n` (new), `t` (set type), `w` (WRITE!).

*   **Formatting (Makes Filesystem):** ☠️ **ERASES DATA!** ☠️ Preparing partition for use.
    *   `sudo mkfs.ext4 /dev/sdb1`: Create **ext4** filesystem.
    *   `sudo mkfs.xfs /dev/sdc1`: Create **xfs** filesystem.
    *   `sudo mkswap /dev/sda3`: Initialize as **swap**.

*   **Mounting:** Attaching filesystem to directory.
    *   `mount`: Show current mounts.
    *   `sudo mkdir /mnt/point`: Create empty mount point dir.
    *   `sudo mount /dev/sdb1 /mnt/point`: Mount device onto point.
    *   `sudo umount /mnt/point` or `sudo umount /dev/sdb1`: Unmount (fails if busy!).
    *   `sudo lsof /mnt/point`: **L**ist **O**pen **F**iles on path (find what's using it).

*   **Persistent Mounts (`/etc/fstab`):** ☠️ **CRITICAL FILE! Be careful!** ☠️ Mount on boot.
    *   Backup: `sudo cp /etc/fstab /etc/fstab.bak.$(date +%F)`
    *   Format: `UUID=<uuid> <mount_point> <type> <options> <dump> <pass>`
        *   Use UUID from `blkid`. `options defaults` common. `pass` is 0/1(for root)/2.
    *   Test: `sudo mount -a` (tries mounting all fstab entries). Fix errors if any!

*   **Swap:** `swapon --show` (list active), `free -h` (see usage).
*   **LVM:** Flexible volumes. PV -> VG -> LV. `pvcreate`, `vgcreate`, `lvcreate`, `lvextend`.

***
(Practice Mission 7 unchanged)
***

---

## Playbook Level 8: Logs & Monitoring

**My Goal:** Find/read system logs, basic performance monitoring. What's happening? 🕵️‍♂️

*   **Log Locations (`/var/log`):** Where logs traditionally live.
    *   `syslog` / `messages`: General events.
    *   `auth.log` / `secure`: **Security/Login** events.
    *   `dmesg`: Kernel messages (use `dmesg` command).
    *   `apt/` or `dnf.log`: Package history.
    *   Application logs (e.g., `nginx/`, `mysql/`).
*   **Viewing Logs:** Reading the messages.
    *   `less <logfile>`: Page through file.
    *   `sudo tail -f <logfile>`: Follow live updates (`Ctrl+C` stops). **Very useful.**
    *   `sudo grep -i "pattern" <logfile>`: Search for text pattern (case-`i`nsensitive).
    *   `dmesg`: View kernel buffer. `dmesg -T` for timestamps.
*   **Systemd Journal (`journalctl`):** Modern, central log system.
    *   `journalctl`: View all journal logs.
    *   `journalctl -u <service_name>`: View logs ONLY for that service. **Primary troubleshooting command for services.**
    *   `journalctl -b`: View logs since last **b**oot.
    *   `journalctl -p err`: View **p**riority `err` or higher.
    *   `journalctl -f`: Follow journal updates live.
*   **Log Rotation (`logrotate`):** Automatic log management (size, compression, deletion). Configs in `/etc/logrotate.conf`, `/etc/logrotate.d/`. Runs via cron.
*   **Basic Performance Checks:** Quick health assessment.
    *   `uptime`: Show system uptime and load average (1, 5, 15 min). Load should ideally be less than # CPU cores.
    *   `free -h`: Show memory usage (**h**uman-readable). Look at `available` memory and `Swap` used (should be low/zero ideally).
    *   `vmstat 1 5`: Quick overview of CPU (`us`, `sy`, `id`, `wa`), memory (`si`, `so`), I/O (`bi`, `bo`) over 5 seconds (1 second interval).
    *   `iostat -xz 1 5`: Disk I/O details (requires `sysstat`). Shows CPU% and disk `%util`, `r/s`, `w/s`.
    *   `top`/`htop`: Real-time process resource usage.

***
(Practice Mission 8 unchanged)
***

---

## Playbook Level 9: Shell Scripting Basics & Automation

**My Goal:** Automate simple tasks with shell scripts (`bash`). Make the computer work for ME! 🤖

*   **Script Basics:** File starts `#!/bin/bash`, `chmod +x file`, run `./file`. `#` comment.
*   **Variables:** `MY_VAR="value"`; use `$MY_VAR` or `${MY_VAR}`. Quoting matters: `"$VAR"` expands, `'$VAR'` literal.
*   **Command Substitution:** Capture output: `VAR=$(command)`. Example: `FILES=$(ls)`.
*   **User Input:** `read -p "Prompt: " VAR`.
*   **Arguments:** Passed to script: `$1`, `$2`, etc. `$0` script name, `$#` count, `$@` all args separately (best!).
*   **Conditionals (`if`):** `if [[ condition ]]; then ... elif ... else ... fi`. **Spaces inside `[[ ... ]]` needed!**
    *   Tests: `[[ -f "$FILE" ]]` (file), `[[ -d "$DIR" ]]` (dir), `[[ -z "$VAR" ]]` (empty), `[[ "$A" == "$B" ]]`, `[[ "$N" -eq 10 ]]` (numeric eq,ne,lt,le,gt,ge). Quote vars!
    *   Logic: `!` (NOT), `&&` (AND), `||` (OR).
*   **Loops (`for`, `while`):** Repeat code.
    *   `for x in a b c; do ... done`
    *   `for ((i=0; i<5; i++)); do ... done`
    *   `while [[ condition ]]; do ... done`
*   **Redirection & Pipes:** Control I/O.
    *   `>` stdout (overwrite), `>>` stdout (append), `2>` stderr, `&>` both stdout/stderr.
    *   `<` stdin from file.
    *   `|`: **Pipe!** Output of cmd1 becomes input of cmd2. `cmd1 | cmd2`. **Fundamental.**
*   **Functions:** Reusable code blocks. `function name { commands... ; }`. Call `name args...`. Use `local var` inside.

***
(Practice Mission 9 unchanged)
***

---

## Playbook Level 10: Security Essentials

**My Goal:** Basic security hygiene & hardening practices. Locking things down! 🛡️ (Crucial Basics).

*   **Keep Updated:** Patch often! `sudo apt update && sudo apt upgrade -y` or `sudo dnf update -y`.
*   **Users/Passwords:** Strong passwords, **SSH Keys >> passwords**, remove unused accounts (`sudo userdel user`), lock accounts (`sudo usermod -L user`), no defaults.
*   **Minimize Surface:** Uninstall unused packages, disable unused services (`sudo systemctl disable service`). Check `sudo ss -tulnp`. Fewer open ports = safer.
*   **`sudo` Config:** Use `visudo`. Prefer groups (`%sudo`, `%wheel`) over direct user listing. Grant specific commands if possible.
*   **Harden SSH (`/etc/ssh/sshd_config` & reload):**
    *   `PermitRootLogin no` **(Highly Recommended)**.
    *   `PasswordAuthentication no` **(Highly Recommended** after keys work).
    *   Consider non-default `Port <num>` (minor obscurity, reduces log spam).
    *   Install & enable `fail2ban` (`sudo apt/dnf install fail2ban`; `sudo systemctl enable --now fail2ban`). Auto-bans IPs trying to brute-force logins.
*   **Firewall:** Enable (`sudo ufw enable` / `sudo systemctl enable --now firewalld`). Default deny in, explicitly allow needed ports (SSH, web, etc.).
*   **Check Logs:** Regularly check `auth.log`/`secure`, `syslog`/`messages` (`journalctl`) for anomalies.
*   **Permissions:** No `chmod 777`! Least privilege. `600` for keys. Correct web server ownership/perms.
*   **Backups:** Essential for recovery. Use `rsync`, `tar`, or backup tools.

***
(Practice Mission 10 unchanged)
***

---

## Playbook Level 11: Advanced Topics (My Next Frontiers!) 🚀

**My Goal:** Know where to explore next. The journey continues!

*   **Text Power Tools:** Master `sed` (stream editor, find/replace), `awk` (column processing). Regex skills enhance everything.
    ```bash
    # sed example: replace 'old' with 'new' globally in file
    sed 's/old/new/g' input.txt > output.txt
    # awk example: print first column ($1) of lines containing "ERROR"
    grep "ERROR" logfile.log | awk '{print $1}'
    ```
*   **Version Control (`git`):** MUST learn for managing scripts, configs. Track changes, revert, collaborate. `clone`, `add`, `commit`, `push`, `pull`.
    ```bash
    # Basic Git flow
    git clone <url> MyProject && cd MyProject
    # ... make changes ...
    git add script.sh config.yml
    git commit -m "Added feature X and updated config"
    git push origin main
    ```
*   **Configuration Management:** **Ansible** (YAML playbooks, agentless, good start!), Puppet, Chef, Salt. Automate server setup consistently.
*   **Virtualization:** KVM/libvirt (`virsh`, `virt-manager`). Run VMs locally.
*   **Containers:** **Docker** / **Podman**. Package apps + dependencies. `run`, `build`, `ps`, `compose`. Fast, lightweight isolation.
    ```bash
    # Run a python app from a Dockerfile in current dir
    docker build -t my-python-app .
    docker run -d -p 5000:5000 --name webapp my-python-app
    ```
*   **Monitoring:** **Prometheus + Grafana** (modern metrics/dashboards), Zabbix, Nagios.
*   **Centralized Logging:** Elastic Stack (ELK), Graylog, Loki. Aggregate logs.
*   **Adv. Networking:** VLANs, Bonding, Routing concepts, VPNs (WireGuard!).
*   **Kernel Tuning (`sysctl`):** Tweak kernel parameters (`/proc/sys/`, `/etc/sysctl.conf`). Know why!
*   **Performance:** `perf`, `strace`, `gdb` for deep dives.
*   **Cloud (AWS, Azure, GCP):** Essential skill. Learn core services (VMs, Storage, Network, IAM).

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
