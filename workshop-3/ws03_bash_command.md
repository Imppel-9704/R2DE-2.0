# Road to Data Engineer - Workshop 3
## Command Line (CLI)

This chapter we are going to learn about basic command line. I decided to use terminal in Google cloud shell in this chapter because it's free.

## basic command
- ls : list all files in current directory | ls -l : list all files with more details | -h : human readable | -a : show hidden files | * is wildcard | ls *zip : only list .zip file
- pwd : print full path. show currect directory where we are at
- cd : change directory | cd ~ : return to home | cd - : return to previous directory

![Image](https://drive.google.com/uc?id=1juPag_-Wm7MqkaMlUemq1BJjqdzkEWrS)

## Print / Create file / Read file
- echo : print word | echo $ : print variable
- cat : concatnate (read file) | cat [FILE_NAME] : print file
- more / less : view a single file separated by lines | more / less [FILE_NAME] | press space bar to view next page | press q to exit
- touch : create blank file | touch [FILE_NAME]

## Manage directory / Manage files
- mkdir : make directory or create folder | mkdir [DIRECTORY_NAME] | mkdir -p newfolder/in/sub/folder : in case creating folder in sub folder
- cp : copy | cp [SOURCE] ... [DESINATION] | cp file.txt new_folder | cp -r whole_folder/ desination_folder (-r = recursive. to copy whole folder)
- mv : move or change file name or change folder name | mv [SOURCE] ... [DESINATION] | mv old_name.txt new_name.txt
- rm : delete files or folder | rm [FILE_NAME] | rm -r folder (-r = recursive to remove folder)

## Others
- wget : download file (-O to name file) | wget -O data.zip https://path.com/to/download/file
- unzip / zip : use to unzip file | unzip [FILE_NAME] | zip [FILE_NAME.zip] [FILE_to_ZIP]
- wc : word count | wc [FILE_NAME] | wc -l [FILE_NAME] : only show line count
- man : open manual about command | man [COMMAND_NAME] | press q to exit
- bonus : how to get out of vim | vim is text editor in terminal | press : and q to exit
