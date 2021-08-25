# General questions

## What is Decompilation? What is matching decompilation?

Decompilation is a type of reverse engineering: analysing the compiled binary data that is on the cartridge to produce human-readable code that has the same result. *Matching* decompilation more specific: instead of merely functionally equivalent code, it aims to produce code that compiles to *exactly* the same data as the original.


## What is the point of this project? What will I be able to do with decomp when it is finished?

The aim is to produce a complete documented codebase of every version of the game in its original language (C), before it is compiled into assembly, as has been done in the past for various Pokemon games and Super Mario 64 already. This codebase can be used for various purposes:

- General knowledge and analysis of all the game's systems
- with, for example, applications for speedrunning
- Modding, with no need to learn assembly
- Any other project that wishes to repurpose the code.


## Will there be a PC port of Ocarina of Time/Majora's Mask?

Porting to other platforms will be possible as a result of the work that these projects are carrying out. However, a PC Port is *not* in the scope of this project: *we are not making a PC Port*, but someone else will be able to.


## Does decomp run on console?

The romfile that the decompilation project compiles is identical to the original ROM (that's what *matching* means). Therefore it runs wherever that romfile will. (Since Ocarina of Time currently only targets the MQ debug ROM, it requires the Expansion Pak to run on Nintendo 64, because the debug ROM itself needs the extra 4 MB for debugging features).


## What language was Ocarina of Time/Majora's Mask written in?

They are both written in C, which is compiled to MIPS assembly language, which transliterates precisely into the raw bytes of machine code/data that are on the cartridge.


## How do I set up the decompilation on my computer?

See the instructions in the appropriate README.md:
- [Ocarina of Time](https://github.com/zeldaret/oot/#readme)
- [Majora's Mask](https://github.com/zeldaret/mm/#readme)


## What decompiler is being used?

We mostly use a custom-built decompiler called [mips_to_c](https://github.com/matt-kempster/mips_to_c). Occasionally some people have found Ghidra helpful, but for matching decompilation of MIPS, custom tools for the job have proven much more capable.


## Who can contribute? What do I need to know?

Anyone with a decent knowledge of how the games work can contribute usefully in some way or other if they learn the basics of C.

- To work with the decompiled code in a nontrivial way you need to know C (you can learn enough C to read the code in a week, so it's not a major time investment).
- Code decompilation itself requires a good knowledge of C, particularly structs and pointers, but C has a sufficiently small vocabulary and grammar that these can be acquired quickly. MIPS assembly knowledge is not actually necessary to start learning to decompile, but you will pick it up relatively quickly too.
- To work with asset files, you need to be able to use the repository and build the ROM, and know some xml and C, but we now have plenty of useful tools (especially [Z64Utils]) that make understanding how asset files are structured relatively simple.
- Documentation requires good knowledge of C, but much moreso than the other areas an understanding of how the game works.
- To contribute to the repository and organise your work with proper version control, you need to know the basics of git, and how to use it with GitHub.

There is one exception:


### Is any use being made of leaked materials?

No. *No one is allowed to contribute to the project who has accessed material relating to relevant source code or documentation leaks.* For specifics, see [the Discord server](http://discord.zelda64.dev/).


## Why does the progress graph move so inconsistently?

Firstly, on any project like this, the beginning is slow as the methods and techniques are created and understanding of anything requires a lot of analysis of all factors involved. The middle period is fastest, as techniques are refined, more people join, and can learn more quickly from established understanding. Ocarina of Time is now in the final stages of decompilation: a lot of the files left are taking a long time because they are hard to decompile.

Secondly, the graph does not take into account
- Code decompiled on people's forks that is currently being documented or cleaned up.
- Code in PRs that is under review.
- Asset analysis, symbol replacement, and other documentation.

All of these represent significant decompilation progress that is not accounted for by the graph. Recent spikes in progress represent code that has been completed, but required months to document properly.

Lastly, people are doing this in their spare time, so when they don't have spare time, they aren't able to contribute.


## When will the project be finished? How long will a PC Port take?

This is being done by people in their spare time, so we do not have a specific deadline in mind. The best way to keep track of the overall progress is [the progress page](progress.html) (but see previous question): you can [ask in Discord](http://discord.zelda64.dev/) if you would like more specific information.

As was said above, **we are not making a PC Port**. However, Ocarina of Time and Majora's Mask are considerably more complicated than Super Mario 64, so even when the project is in a useable state, it will be a while before a PC Port is ready.


## Where can I get more information?

For more information on any of the topics in the scope of this project that have been discussed here, please join [the Discord](http://discord.zelda64.dev/). We aim to be helpful and friendly to newcomers, provided they have read the basics in this FAQ.


### I would like to write an article or make a video about this project. Who should I contact for further information?

Please reach out to one of the project leads (via Discord?). They will either answer your questions themselves, or direct you to someone who is more knowledgeable in the relevant areas.



# Specific to Ocarina of Time

## Is Ocarina of Time more optimised than Super Mario 64?

Yes, the debug ROM that we are using has the standard `-O2` optimisation flags for most files (some of the low-level Nintendo 64 system files are compiled with other flags). This means that the entire game has been approximately as difficult to decompile as the last part of Super Mario 64 that was completed, namely the audio, although we have benefited greatly from the prior experience of Super Mario 64 decomp, as well as our custom decompiler `mips_to_c`.


## Which versions will be decompiled?

It is intended to eventually support every version we have available: N64/GC, NTSC/PAL, etc.


## Why start with the PAL Master Quest Debug version?

Before the project began, this version of the game had the most information available: most romhacks have used it as a base, and it includes certain data ("debug strings") that help with identification of some of the purposes of functions and variables. It also appears to be slightly easier to match due to being compiled with slightly different flags from retail versions.


## How can I help? 

- Currently OoT is close to finishing code, so there is no code available to work on decompiling.
- Object decompilation is analysis and identification of the content of the asset files used in code (textures, 3D models, animations, collision data, etc.). There is plenty of this still to do.
- If you want to do code decompilation now, MM is similar to OoT, but a bit more difficult. It has plenty of simple actor files available that are suitable for beginners.



# Specific to Majora's Mask

## How similar is Majora's Mask to Ocarina of Time? Can code be copypasted between the two?

Some things are very similar: both use the same coding styles, share some code, some of the asset files are identical (only about 10% of the files are the exactly the same, though). However, other parts are very different, an obvious example being Link's multiple forms, but there are less obvious differences as well, such as use of animated textures containing framedata instead of animating textures directly with code, much more prevelent use of load-on-demand, and more that we will discover in due course. So far there have also been a surprisingly large number of changes from OoT files that you would expect to just transfer (Keese in MM are quite different from their OoT versions, for example).


## Why is Majora's Mask harder to match than Ocarina of Time?

Majora's Mask is compiled with `-O2 -g3`. `-g3` is a debugging flag that includes far more debugging information than just `-O2`, but also changes how the compiled code looks. `-g3` is also more sensitive to the scope in which variables are declared, so it is harder to produce matching code; OoT debug is more flexible here. However, retail versions of Ocarina of Time are also compiled with `-O2 -g3`, so it too will have this problem when that project moves to supporting retail versions.


## Why is Majora's Mask so far behind Ocarina of Time?

It was decided by the Majora's Mask project leads to concentrate on Ocarina of Time first, with the expectation that a lot of Ocarina of Time code could be used to help, directly or indirectly, with Majora's Mask decompilation, and this has proven to be the case so far! But recently, knowledge from MM has also been helping with matching stubborn functions in Ocarina of Time.


## Are OoT and MM using the same decompilation method?

Broadly yes: both games are sufficiently similar that the same method can be used for compiling the files. However, Ocarina of Time keeps the remaining undecompiled assembly code in the main repository, while Majora's Mask uses transient assembly, which makes the extraction and disassembly process more complicated.


## Why is there no assembly code in MM's repo? What is transient ASM?

It is the view of the MM project leads that transient asm is safer than storing the disassembly in the repo. We feel like the C code is more transformative than a straight disassembly.

This does require a more sophisticated way of dealing with the code (find/replace for renaming things must be replaced by a script and dictionary, data must be handled with more care, etc.), but it also produces a much cleaner codebase while the project is still in progress.

Most of decompilation work itself is not really any different from the Ocarina of Time process: it just requires a few extra steps.

