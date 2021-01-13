### The "Three" States of a file  

This is something of a misnomer in the opinion of the author. All the books  
that have been read all describe the state of a file in the working directory  
to be in one of three states: Modified, Staged or Committed.  
Observation tells the author that this isn't quite the case. To prove the  
point, we'll walk through a demonstration showing that there are actually four  
states that a file can be in. The books say three only because Git will  
manipulate a file that is only in three of the four states.  

For right now, ignore the commands as far was what are they and what they do,  
for this walk-through you need only execute them as written in exactly  
the order presented. Full descriptions of all commands used will be provided  
at a later time, promise!

The procedure:
  1.  Open a command prompt, doesn't matter which, CMD or PowerShell. This  
      demo will presume PowerShell.
  2.  Navigate to your standard repository root. This should be something like  
      c:\Users\\\<Your User Name>\Documents\\_Repos or some such as that. This  
      is the root directory of where all your local repositories will be stored.  
  3.  Create a directory there, call it "Playground"
  4.  Change into that directory.
  5.  Execute the command `git status` just like you see it. The response  
      should be something like:

      `fatal: not a git repository (or any of the parent directories): .git`  

      This is telling you that the directory you are currently pointing to is  
      not part of the Git family. There is no repository here, no tracked  
      files, no nothing. It's just a directory as far as Git is concerned. This  
      is because the directory has yet to be turned into a repository.  
  6.  Execute the command `git init`.  This is the command that turns an  
      ordinary directory into a local git repository.  
  7.  Perform a directory list: `ls`. You should see no files and no  
      directories.  
      This is because the directory that git has created is a "hidden"  
      directory named ".git" <- Note the leading period (.).  
      A new Windows standard has come about since Microsoft decided to play  
      nice with the Linux people and have adopted some of the same standards as  
      Linux. To wit, files and/or directories that start with a period (.) are,  
      by default, hidden from normal view.  
      To actually see the content of the directory, enter the command:  
      `ls -h` (or `dir -h` if you are old-style command processor familiar).  
      You should see one directory named ".git".
  8.  Congratulations! You have created your first Git repository! That's it,  
      all one need do is run "git init" within an empty directory and git  
      does the rest.
  9.  Now, execute the command `git status`. You should see something similar  
      to the following:

      ```
        On branch main

        No commits yet

        nothing to commit (create/copy files and use "git add" to track)  

      ```  
      This is telling you that the working directory you just created is empty  
      of any entries that Git is aware of, but that it **has** been initialized  
      correctly.
  10. Now, using Notepad or some other text editor, create a file in this  
      directory and put some text into it, something you'll remember e.g.  
      "This is a test file" and save the resulting file.  
  11. Now, run `git status` again. You will see a very different response this  
      time:  

      ```  
      On branch main

      No commits yet

      Untracked files:
        (use "git add \<file\>..." to include in what will be committed)
              test.md
      
      nothing added to commit but untracked files present (use "git add" to track)  

      ```  
      You can see that Git has recognized that there is a file that wasn't there  
      before but it has no clue what to do with it. This is why the author  
      feels that there are actually four states that a file can be in, this  
      fourth state is "un-tracked" - Git doesn't know what to do with the file  
      but it _is_ **aware** of the file.  
  12. So, to rectify this problem and add the file to the repository, or at  
      least make Git aware of the file and place it in a state such that Git  
      can now manipulate the file, perform the following command:  
      `git add *`  
      You can also do a  
      `git add <file name> [<file name> <file name>]`  
      where each \<file name\> is space-separated (the brackets [] represent  
      additional, optionally included files. IOW, one may either add by  
      wild card (*) or by individual file name).  
      This moves the file status from "un-tracked" to "staged".  
      If you have set up your Git install using the authors' recommended  
      settings, then you should see the following message:

      ```
      warning: CRLF will be replaced by LF in test.md.  
      The file will have its original line endings in your working directory  
      ```

      You can see this by executing the command:  
      `git status`  
      again. You should now see something like the following:

      ```
      On branch main

      No commits yet

      Changes to be committed:
        (use "git rm --cached <file>..." to unstage)
              new file:   test.md
              
      ```  

      The file has now been copied and stored in a separate location. As a  
      matter of fact, the entire content of your working directory has been  
      "snap-shotted" and stored, ready for you to commit to a repository.  
      Note that the file has only been staged, _it is not yet part of a  
      repository_.
  13. Try this: Open the file again in Notepad (or whatever) and make some  
      modification to the content (don't erase it, add to it) and then save  
      the file. Then, execute a `git status` again to observe something like  
      the following:

      ```
      On branch main

      No commits yet

      Changes to be committed:
        (use "git rm --cached <file>..." to unstage)
              new file:   test.md

      Changes not staged for commit:
        (use "git add <file>..." to update what will be committed)
        (use "git restore <file>..." to discard changes in working directory)
              modified:   test.md

      ```  
      You can see that your file is in there twice now, once as "staged",  
      ready to be committed and, the new, modified file which needs to be  
      staged. Git has stored a snapshot of the original and noted that a  
      change to the file has been made subsequent to the creating of the  
      snapshot. As stated, if you do a `git add`, the staged file will be  
      updated and only the latest version will be ready to be committed.  
      Let's do that. Perform a `git add *` to add the modified file and  
      re-stage it.
  14. A lot of reference to this "commit" action has been made, but it hasn't  
      been explained yet. Here we go.  
      When Git "commits" a snapshot, it writes the staged snapshot into its own  
      little file system stored somewhere inside the ".git" directory created  
      when your working directory was initialized to be a Git repository. The  
      snapshot is optimized, compressed and assigned a SHA-1 hashtag value.  
      Don't know what SHA-1 is? Nothing to worry about, there are plenty of  
      references on the internet to explain. Short version: it's a 40 digit  
      hexadecimal value used to give a snapshot a (relatively) simple name.  
      You'll refer to that hash value frequently when merging, etc. It's  
      generated by running the entire content of the snapshot through a  
      hashing algorithm the result of which is the aforementioned 40 digit  
      number. This makes Git secure - change a **_single bit_** of the snapshot  
      and a new SHA-1 must be generated and **Bad Things** happen. This is why  
      Git is **VERY DIFFICULT** to persuade to "change history". It can be  
      done, but it takes an expert who knows _exactly_ what they are doing to  
      do so.  
      So...how does one actually perform a commit? Execute the following:  

      `git commit -a -m "Some Commit Message"`  <-- Note the double quotes ("")  
      around the "Some Commit Message" message - they are **_REQUIRED_**,  
      otherwise, if Git is configured correctly and the appropriate editor is  
      available, said editor will open and Git will wait patiently whilst you  
      add the aforementioned commit message. Either way, a commit message  
      **must** be provided. And remember, this is _not_ **what** you did to  
      require this commit, but instead it's **why** this commit was made.  
      We will be doing more with commit messages later, when you "extend" them  
      you can do things like tell Azure DevOps (TFS) that an item is "closed"  
      or "resolved", etc. just by using a different syntax. Not covered in this  
      document.

      The "-a" tells git to add any files that might not yet have been staged  
      and is therefore optional.  
      The "-m" tells git that the next item in quotes is the commit message,   
      which is a **_REQUIRED_** value. Git will not allow a commit without a  
      commit message. The message needs to be short, sweet and to the point.  
      Mainly, _why_ was the commit performed, not _what was in_ the commit.  
      What is in can be determined by doing a diff (something we'll get into  
      later). The commit message tells the viewer what was done last and why.  
  15. Now, execute a `git status` and you should see something like the  
      following:

      ```
      On branch main
      nothing to commit, working tree clean
      ```
  16. Congratulations! You have now stored your first snapshot in your local  
      repository.  
  17. And now, you might be saying to yourself; "That's nice, now I have this  
      mess in my repo directory and I have no idea how to get rid of it.".  
      No worries, this is another thing that makes Git unique. Ease of what  
      can be considered "brute force" maintenance. If you don't want the  
      repository anymore **and** it's not been committed remotely (or even if  
      it has), if you want to remove the local repository, simply make sure  
      that nothing is pointing to that directory and delete the entire thing.  
      Problem solved!  
      **BUT**, if you want to do a bit of playing with branching as described  
      in the next section, don't delete the repository just yet.  
      
