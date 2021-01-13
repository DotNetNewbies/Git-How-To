##### Configure Beyond Compare 4 as a Diff (difference) tool  

Beyond Compare (BC) is a fabulous (in this authors' opinion) differencing and  
merge tool. It's inexpensive and works on just about anything (binary files,  
text, etc.)  
If the user decides to use BC for such purposes, below explains how to  
configure git to use BC as the preferred difference/merge tool.  
Perform this activity wherever BC is installed to ensure consistent operation.  
And, just so you know, Beyond Compare is a "for-pay" tool. Not expensive (I  
believe it's a staggering $30.00 USD for the standard edition, the author  
recommends the "pro" edition as this gives the 3-way comparison and a bunch  
of other goodies, it's $60.00 for a multi-platform release), see the info on  
the download page for more information.  

  * `git config --global diff.tool bc`  
  * `git config --global difftool.bc.path "C:\Program Files\Beyond Compare 4\BCompare.exe"`  
    * Ensure that the path is to your copy of BC.  
    * Ensure that, if there are spaces in the path, that the path is enclosed  
      in double quotes (").

##### To use BC as a difference tool

  * `git difftool --dir-diff`
    * This will compare the difference between the working directory and the  
      last fetch/pull.  
  * `git difftool <some file name>`  
    * This will compare the content of individual files.  

##### Configure Beyond Compare as a Merge tool

  * `git config --global merge.tool bc`  
  * `git config --global mergetool.bc.path "C:\Program Files\Beyond Compare 4\BCompare.exe"`  

##### To use BC as a 3-way merge tool

  * `git mergetool <some File Name>`

Gits default setting is to retain merge files with *.orig extensions after a  
successful merge. To disable this **_safety feature_** and automatically  
delete *.orig files after a merge, execute:

  * `git config --global mergetool.keepBackup false`

If you are presented with a prompt, e.g. "Launch 'bc4' [Y/n]?" when performing  
a diff and you do not wish to see said prompt, execute the following

  * `git config --global difftool.prompt false`  

and the prompt should not longer be displayed.  

##### Installation Validation

Once you have completed your desired changes, to ensure that git was indeed  
paying attention and did as you asked, execute the following command:

`git config --list --show-origin`

The "--list" portion will show you the settings, the "--show-origin" portion  
will show you which of the many config files git took the setting from.  

