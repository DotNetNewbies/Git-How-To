### .gitignore files  

The basics are these:
* Blank lines are lines starting with a '#' are ignored  
* Standard "glob" patterns work.  
  * An asterisk (*) matches zero or more characters.  
  * Letters in brackets, e.g. [aeiou], match any single character inside the  
    brackets, e.g. [AaEeIiOoUu~]-log ignores all files that start with  
    A, a, E, e, I, i, O, o, U, u or a tilde (~) character that contain "-log".  
    The characters _are_ case-sensitive.  
  * A question mark (?) matches any single character.  
  * Characters enclosed in brackets, separated by a hyphen (-) specify a range  
    of characters e.g. [0-9] matches 0,1,2,3,4,5,6,7,8,9.  
  * Two asterisks (**) match nested directories, e.g. a/**/z matches a/z, a/b/z  
    a/b/c/z, etc.  
  * A leading forward slash specifies a single directory in the root to ignore  
    not some-sub-directory/directory.  
  * A trailing forward slash (/) ignores all files in the specified directory  
    e.g. build/ ignores all files in the build directory.  
  * Negation of a pattern is done by preceding the pattern with a bang (!).  

A good reference for additional information on .gitignore files:  
* https://github.com/github/gitignore  
  * You'll see a reference to "glob patterns" in the aforementioned reference,  
    a good reference for what those are is found here:  
      https://en.wikipedia.org/wiki/Glob_%28programming%29  