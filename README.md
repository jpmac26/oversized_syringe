# oversized_syringe
Modding tool for the Hyperdimension Neptunia series games; enable packing/unpacking of resources from the games' custom archive format

**under active developement and still experimental**

# Abstract

The games themselves run pretty well under wine, the existing modding tools, however, do not (neither kitserver nor the packer created by anon).

Since I wanted to try the new translation for ReBirth;2, I had to borrow a friend's PC in order to statically patch my game files.

However, since being dependant on that kind of sucks, I decided to make my own packing/unpacking tool, by reverse-engineering the game's archive format.

I was able to un-compress the files by using QuickBMS (which you should also check out), then it was just a matter of discovering the compression algorithm, comparing "before" and "after".

The file's directory and compression formats are pretty much understood now (I'd say 99.9%); the developement is now aimed at creating a stable and usable tool

# Usage

## CLI version

    ./oversized_syringe.py -h
    
The command line tool has 2 general usages:
#### Non-staging mode

For read-only operation of the archive, like listing its content and extracting specific/all files
    
#### Staging mode

git-like interface for staging and applying modifications to an existing/new pac files. It must be
explicitly enabled for each step via the *-S* option

The usual workflow is something like this:

    oversized_syringe.py -S PACFILE.pac
        
Initialize the staging environment, the staged pac-object is a copy of PACFILE's content.
If you want to create a wholly new pacfile, run:
oversized_syringe.py -S
        
        
    oversized_syringe.py -S -a file/name.xyz
    oversized_syringe.py -S -m directory/
    oversized_syringe.py -S -r file/name.xyz
    
Add a file (-a), merge a directory (-m), remove a file (-r)
        
When merging, the file with conflicting names will be staged for replacement
        
    oversized_syringe.py -S -u file/name.xyz
    
Undo (-u) the modifies (add/replace/delete) staged for file/name.xyz
        
The internal name (the name of the file inside the pac archive's directory) is translated directly from the filesystem path passed as an argument (with eventual conversion of slashes into backslashes). It is often useful to set a base-directory: basically, the path of the base-dir is subtrcted from the file's, and the result is used as the internal name:

    oversized_syringe.py -S -B extracted/ -a extracted/file/name.xyz
        
the file will be added as "file\name.xyz"
    
When you're done:
    
    oversized_syringe.py -S -c
    
Commit (-c) the modifies, meaning that the staged modifies will be applied to the staged pac-object
    
    oversized_syringe.py -S -w NEWFILE.pac
    
Finally, begin the compression of a new pacfile, using the previously build staged object as model.

If something went wrong during the process, you can reset the staging environment by deleting the .ovs_staging file.

The file will also be deleted once the write (-w) operation was completed with success.
    
    
## GUI version

not yet developed

# Roadmap

1. Extensive testing
2. Multicore parallel de-compression
3. GUI
4. Test support for other OSes

# Thanks to

[Luigi Auriemma](aluigi.altervista.org)

[Idea Factory International](http://www.ideafintl.com/)