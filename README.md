<div align="center">
<h1>Linux Cheat Sheet</h1>
<p>A curated list of essential Linux information and commands every user should know</p>

![OS-Linux-icon](https://icons.iconarchive.com/icons/dakirby309/simply-styled/128/OS-Linux-icon.png)
</div>

# Index
**File Management** :file_folder:  
&emsp;• [Change Directories](#change-directories)  
&emsp;• [List Files](#list-files)  
&emsp;• [Current Directory](#current-directory)  
&emsp;• [File Contents](#file-contents)  
&emsp;• [File Creation](#file-creation)  
&emsp;• [File Deletion](#file-deletion)  
&emsp;• [Copy Files](#copy-files)  
&emsp;• [Move Files](#move-files)  
&emsp;• [Compare Files](#compare-files)  
&emsp;• [Symbolic Links](#symbolic-links)  
**Permission Manipulation** :briefcase:  
&emsp;• [Accessors](#accessors)  
&emsp;• [Permissions](#permissions)  
&emsp;• [Symbolic vs Absolute](#symbolic-vs-absolute)  
&emsp;• [Change Ownership](#change-ownership)  
&emsp;• [Set Permissions](#set-permissions)  
**Packaging** :package:  
&emsp;• [Sync Package List](#sync-package-list)  
&emsp;• [Query Packages](#query-packages)  
&emsp;• [Install Packages](#install-packages)  
&emsp;• [Delete Packages](#delete-packages)  
&emsp;• [List Packages](#list-packages)  
&emsp;• [Package Information](#package-information)   
**Source Control** :octocat:  
&emsp;• [Clone Repositories](#clone-repositories)  
&emsp;• [Stage Files](#stage-files)  
&emsp;• [Commit Files](#commit-files)  
&emsp;• [Upload Files](#upload-files)

## Legend
&ensp;• angle brackets `<required argument>`  
&ensp;• square brackets `[optional option]`  
&ensp;• curly braces `{default values}`  
&ensp;• parenthesis `(miscellaneous info)`  
&ensp;• hastag `# comment`

<details open><summary><h3>:file_folder: File Management</h3></summary>

In Linux everything is a file. Directories are just a list of files and for that reason, many programs such as `ls` and `mv` don't disctriminate
## Change Directories
change to a directory (home)
```bash
cd [dirPath]
```

## List Files
list all files in a directory (current)
```bash
ls [dirPath]
# including hidden
ls -A [dirPath]
```

## Current Directory
return path to working directory
```bash
pwd
```

## File Contents
output file content to terminal
```bash
cat <filePath>
# first <N> lines
head <N> <filePath>
# last <N> lines
tail <N> <filePath>
```

## File Creation
make file
```bash
cat [someText] > <filePath>
# join two files into a new file
cat <filePath> <filePath> > <filePath>
# make directory
mkdir <dirPath>
```

## File Deletion
```bash
rm <filePath>
# and directories
rm -r <dirPath>
# recursive force (without confirmation)
rm -fr <dirPath>
```

## Copy Files
copy files to a destination directory
```bash
cp <filePath> <dirPath>
# and directories
cp -r <dirPath> <dirPath>
```

## Move Files
move files/directories to a destination
```bash
mv <filePath> <dirPath>
# rename a file
mv <fileName> <newFileName>
```

## Compare Files
check the difference between two files
```bash
diff <filePath> <filePath>
```

## Symbolic Links
create a link pointing to target file (shortcut)
```bash
ln -s <filePath> <linkName>
```

---
</details>
<details open><summary><h3>:briefcase: Permission Manipulation</h3></summary>

Every file on a Linux system has read, write & execute permissions defined per user, group & other
## Accessors
[`u`]ser — who created the file  
[`g`]roup — set of users with common permissions  
[`o`]ther — anyone who isn't user or in groups  
[`a`]ll — all of the above (`ugo`)

## Permissions
[`r`]ead — view file contents  
[`w`]rite — edit/modify file  
e[`x`]ecute — run executable or view directory  
none - no rights (`-`)

## Symbolic vs Absolute
symbolic ｜ absolute, read, write & execute per user, group & other command sequence table

• | u | g | o | ug | uo | go | a
--- | --- | --- | --- | --- | --- | --- | ---
**r** | `u=r`｜`400` | `g=r`｜`040` | `o=r`｜`004` | `ug=r`｜`440` | `uo=r`｜`404` | `go=r`｜`044` | `a=r`｜`444`
**w** | `u=w`｜`200` | `g=w`｜`020` | `o=w`｜`002` | `ug=w`｜`220` | `uo=w`｜`202` | `go=w`｜`022` | `a=w`｜`222`
**x** | `u=x`｜`100` | `g=x`｜`010` | `o=x`｜`001` | `ug=x`｜`110` | `uo=x`｜`101` | `go=x`｜`011` | `a=x`｜`111`
**rw** | `u=rw`｜`600` | `g=rw`｜`060` | `o=rw`｜`006` | `ug=rw`｜`660` | `uo=rw`｜`606` | `go=rw`｜`066` | `a=rw`｜`666`
**rx** | `u=rx`｜`500` | `g=rx`｜`050` | `o=rx`｜`005` | `ug=rx`｜`550` | `uo=rx`｜`505` | `go=rx`｜`055` | `a=rx`｜`555`
**wx** | `u=wx`｜`300` | `g=wx`｜`030` | `o=wx`｜`003` | `ug=wx`｜`330` | `uo=wx`｜`303` | `go=wx`｜`033` | `a=wx`｜`333`
**rwx** | `u=rwx`｜`700` | `g=rwx`｜`070` | `o=rwx`｜`007` | `ug=rwx`｜`770` | `uo=rwx`｜`707` | `go=rwx`｜`007` | `a=rwx`｜`777`

## Change Ownership
set a user (and group) to a file
```bash
chown <user>[:group] <filePath>
```

## Set Permissions
define permissions per user, group & other of file
```bash
chmod <permissions> <filePath>
```

</details>
<details open><summary><h3>:package: Packaging</h3></summary>

Installing programs in Linux is a bit different than on Windows. When you need a specific program, it's best to use your system's package manager to install software. Package managers handle dependencies, upgrading, querying, installing, removing, listing packages and much more. They severly reduce the complexity of installing software for the end-user 
## Sync Package List
upgrade packages & sync repositories
```bash
# arch linux
pacman -Syu
# debian
apt update && apt upgrade
```

## Query Packages
search for a package
```bash
# arch linux
pacman -Ss [package]
# debian
apt search [package]
```

## Install Packages
install a package
```bash
# arch linux
pacman -S <package>
# debian
apt install <package>
```

## Delete Packages
uninstall a package
```bash
# arch linux
pacman -Runss <package>
# debian
apt purge <package>
```

## List Installed
list installed packages
```bash
# arch linux
pacman -Qe
# debian
apt list --installed
```

## Package Information
```bash
# arch linux
pacman -Si <package>
# debian
apt info <package>
```

</details>
<details open><summary><h3>:octocat: Source Control</h3></summary>

Using below methods to clone an existing (empty) repository, means we can skip several unecessary, over-complicated commands
## Clone Repositories
download a repositories contents (& .git)
```bash
git clone https://github.com/<user>/<repository>
# or a specific branch
git clone -b <branch> --single-branch https://github.com/<user>/<repository>
```

﹡ _although this command uses github as a refrence, any suitable version control software should work as intended_

## Stage Files
add new or changed files to the staging area
```bash
git add .
```

## Commit Files
snapshot staged files with a message
```bash
git commit -m 'initial commit'
```

## Upload Files
upload staged files
```bash
git push
```

</details>
