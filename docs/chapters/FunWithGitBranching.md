### A bit of fun with git branching

  1.  Still working from the command prompt you opened earlier, we will presume  
      that the repository created via the above process still exists. If not,  
      please go re-create it.  
      Go ahead and create the "TestFile.txt" file or whatever you used before.  
      Commit it to the "main" branch - this is what happens when you do a  
      "commit" without changing branches - the default, first-created "branch"  
      is "main" (used to be "master" but that had some connotations that were  
      frowned upon, so "main" is used instead - you established the default  
      branch when installing git for the first time, remember?).  
      It should be noted that there is _nothing_ special about the so-called  
      "main" (or "master" or whatever) default branch, it's just a branch.  
      It's only claim to fame and brief fame it is, is that it is automatically  
      created whenever a `git init` is executed where no .git directory exists.  
      So, with the original file created, modified, staged and committed  
      locally, we are now ready to play with branches.
  2.  Now, to create a branch, execute the following command:
        `git branch Toy`

      This creates a branch in the "Playground" repository called "Toy".  
      A note should be taken here - creating a branch _does nothing more than_  
      _create a **new** place in the git file system to store snapshots_.  
      Remember, this is all about the working directory and the snapshots  
      produced there.
  3.  Do a directory and you will see that the content of the working directory  
      _is unchanged!_
      All that took place here is that Git was told to create a new  
      "sub-directory" if you will, in its own little file system.
  4.  Now, for Git to point that branch at your _working directory_, you need  
      to execute this command:

      `git checkout Toy`  
      
      You should see output similar to this:
      ```
      Switched to branch 'Toy'
      ```
  5.  Again, perform a directory list (`dir`) or (`ls`) and observe that your  
      file is still there, even though Git is now pointing to a different  
      branch. 
      Now, a bit of subtlety here. When you created your "Toy" branch, Git  
      privately took a snapshot of your current working directory and made  
      that snapshot it's first "commit". Why is this important?  
      Simple. When you change branches, you need to make **_ABSOLUTELY SURE  
      THAT THERE ARE NO PENDING CHANGES IN YOUR WORKING DIRECTORY!_**  
      What does this mean? No "open" files, all editing completed, all editors  
      saved, all changes written, nothing pending. Stage all your files (or  
      stash them, more about that later) and commit the changes.  
      Why, you might ask? Because when Git does a checkout, it writes the  
      current snapshot of the branch you are pointing at **to your working  
      directory** thus any changes you might have had would be otherwise lost.  
      Git is real good about warning you and even preventing you from doing  
      something monumentally stupid but the key here is that the snapshot  
      pointed to by the current branch is what your working directory will  
      look like when the checkout is complete.  
      Now, before you panic and wonder what happened to all your work that  
      you just completed, _don't worry_, it's still there. What Git did was  
      subtle - it took the snapshot of your working directory, made the new  
      branch, committed that snapshot to the new branch, then immediately  
      checked it back out so that your starting state in the new branch  
      _looks **exactly** like the place you were in the other branch. Git will  
      do this only once - when the branch is created and then checked out for  
      the first time. Git recognizes that the branch is entirely empty and  
      will look at the content of the "from" branch and make the new branch  
      look exactly the same.  
      There is, of course, **much** more to branching (and merging) than what  
      is described herein. This paper will not attempt to delve into all the  
      intricacies of branching and merging, rather simply give exposure to the  
      process and leave the rest of the research to the student.  
  6.  How to verify this? Open the file in your editor and add the following  
      text: "...this was done in the "Toy" branch." and save the file.
  7.  Stage the file and commit it: (`git add *` followed by `git commit`) if  
      you forgot.
  8.  Now, perform a `git checkout main`. Again, you should see a message  
      similar to:  
      ```
      Switched to branch 'main'  
      ```  
  9.  Now, the fun part. Open your file and observe that your change made  
      when in the "Toy" branch **_is gone_**!  
      Close the editor.
  10. Not to worry, execute the following command:  

      `git checkout Toy`  
  
      to switch back to the "Toy" branch.
  11. Open the file in your editor and viola! your change is back! Close the  
      editor.  
  12. Now, just to be sure we aren't lost, change back to the "main" branch:  
  
      `git checkout main`.  
  
      That, in a nutshell, is Git branching. Obviously this is a powerful tool  
      and much more investigation needs to be performed so this paper leaves  
      said investigation as "an exercise for the student".  
      Something to remember: as long as you don't commit to a remote location  
      you can "play" all you want to as long as the repository you are  
      "playing" with is devoted solely to "play" because at the end of the  
      day, clean-up consists of simply deleting the repository root directory  
      (the one that contains the .git folder).
      There will be more examples of branching and merging in this paper in the  
      section titled "process".  
