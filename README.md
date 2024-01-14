# getGIT

getGIT.sh is a  script that aim to allow to make a download of a large number of repositories from https://github.com

It has number of functions:

**Download a specific OWNER/REPOSITORY**:
: getGIT.sh $OWNER $REPOSITORY
: getGIT.sh $OWNER/$REPOSITORY

examples:
  - getGIT.sh ggerganov/ggml
  - getGIT.sh ggerganov ggml

**Download all the repositories of an OWNER (limited to 250)**
: getGIT.sh $OWNER -all

example:
  - getGIT.sh vim -all

**Download the list of REPOSITORY for one OWNER (limited to 250)**:
: getGIT.sh $OWNER -list

example: 
  - vim -list

**Download the list of REPOSITORY for one OWNER (limited to 8000)**:
: getGIT.sh $OWNER -longList

example:
  - getGIT.sh microsoft -longList

**The list generated both by -list and -longList** is a file "$OWNER.lst", which contains:
  - the first line: @$OWNER
  - 2nd: blank
  - the following lines: $OWNER/$REPOSITORY \<tab\> DESCRIPTION \<tab\> public \<tab\> date_of_last_modification

example for `getGIT.sh vim -list` produce a file '**vim.lst**' which contains:
```
@vim

vim/vim	The official Vim repository	public	2023-12-20T12:10:18Z
vim/winget-pkgs	The Microsoft community Windows Package Manager manifest repository	public, fork	2023-12-20T07:58:36Z
vim/vim-appimage	AppImage for gVim	public	2023-12-20T00:49:49Z
vim/vim-win32-installer	Vim Win32 Installer	public	2023-12-19T23:00:47Z
vim/colorschemes	colorschemes for Vim	public	2023-12-15T09:07:45Z
vim/website_next_generation	The new website	public	2023-11-02T14:16:06Z
vim/killersheep	Silly game for Vim 8.2	public	2023-10-18T14:58:53Z
vim/vim-history	Very very old history of Vim (from v1.14 to v6.4)	public	2023-01-11T14:35:08Z
```

**Download the repositories from an OWNER listed in a file (old version)**:
: getGIT.sh $OWNER -file $file

The $file contains the list of the of repositories. It can be as:
```
OWNER/REPOSITORY
REPOSITORY
OWNER/REPOSITORY <tab> additional descrition
REPOSITORY <tab> additional descrition
```

and a line can be commented by starting the line with '#' or ';' or '@' or '!'

**Download the list of OWNER/REPOSITORY from a list stored in a file MyFILE.lst**:
: getGIT.sh MyFILE.lst

The script check for the extension .lst and if it finds that extension, it expects it to be a list.
The first line of the file, determine the type of the list:
  - **@OWNER** : all the repositories belong to the same OWNER
  - **!list** : the repositories belong to different owners





 
  /home/david/bin/getGIT2.sh $OWNER $REP        : download the repository $REP from the owner $OWNER
  /home/david/bin/getGIT2.sh $OWNER/$REP        : download the repository $REP from the owner $OWNER
  /home/david/bin/getGIT2.sh $OWNER -all         : download all the repositories of the owner $OWNER
  /home/david/bin/getGIT2.sh $OWNER -list        : list all the repositories of the owner $OWNER and create a file $OWNER.lst (limited to 250)
  /home/david/bin/getGIT2.sh $OWNER -longList    : list all the repositories of the owner $OWNER and create a file $OWNER.lst (limited to 6000)
  /home/david/bin/getGIT2.sh $OWNER -file fname  : download all the repositories of the owner $OWNER listed in fname
  /home/david/bin/getGIT2.sh $OWNER.lst          : download a all listing (defined by  $APP $OWNER -list  or user defined, see below

* Note: fname needs to contains one repository per line
* There are two format for $OWNER.lst, differentiated by the first line:
	 - if it starts with @$OWNER : repository listing
	 - if it starts with !list : personalized listing

* repository listing
	 - The fist line is : @$OWNER
	 - then there is one repository name for each line
if a line starts with ';', '#', '@', !' then it is a comment
all the repositories that are not commented will be downloaded
all the repositories belong to the same owner $OWNER

The listing: .lst can be generated automatically with:
	 /home/david/bin/getGIT2.sh $OWNER -list
The lines are by commented when generated, you need to uncomment the lines you wish to download

* personalized list
	 - the first line is : !list
then each line are:
	 - user : download all the repositories of that user
	 - user/repository : download the repository user/repository
if a line starts with ';', '#', '@', !' then it is a comment

* fname
fname is almost identical to 'repository listing' except the first line '@$OWNER' is not needed
