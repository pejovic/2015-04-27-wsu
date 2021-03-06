---
layout: page
Title: Creating, moving, and deleting files and directories
---

# Creating, moving, and deleting files and directories

I'm going to be working mainly in the `Desktop` directory -- recommend that
people follow along.

## Creating an empty file

Lets create an empty file using the `touch` command. Enter the command:

~~~ {.bash}
$ touch testfile
~~~

Then list the contents of the directory again using `ls`. You should see that a new entry, called `testfile`, exists. It does not have a slash at the end, showing that it is not a directory. The `touch` command just creates an empty file.

Some terminals can color the directory entries in this very convenient way. In those terminals, use `ls -G` instead of `ls` if you are on a Mac or `ls --color` if you run on Windows. Now your directories, files, and executables will have different colors.

Now if you use the command `ls -l` you will notice that `testfile` has a size of zero. OK then, let's get rid of `testfile`. To remove a file, just enter the command:

~~~ {.bash}
$ rm -i testfile
~~~

When prompted, type:

~~~ {.bash}
$ y
~~~


The `rm` command can be used to remove files. The `-i` adds the "are you sure?" message. If you enter `ls` again, you will see that `testfile` is gone.

***Warning: The shell does not have a recycling bin. So any file removed with `rm` is gone forever. Use with caution. Remember the -i argument***

If you want to create a file with some text, say notes about what you are doing, you'll need to use a text editor. The one we'll be using here is nano.

> #### Which Editor?
>
> When we say, "`nano` is a text editor," we really do mean "text": it can
> only work with plain character data, not tables, images, or any other
> human-friendly media. We use it in examples because almost anyone can
> drive it anywhere without training, but please use something more
> powerful for real work. On Unix systems (such as Linux and Mac OS X),
> many programmers use [Emacs](http://www.gnu.org/software/emacs/) or
> [Vim](http://www.vim.org/) (both of which are completely unintuitive,
> even by Unix standards), or a graphical editor such as
> [Gedit](http://projects.gnome.org/gedit/). On Windows, you may wish to
> use [Notepad++](http://notepad-plus-plus.org/).
>
> No matter what editor you use, you will need to know where it searches
> for and saves files. If you start it from the shell, it will (probably)
> use your current working directory as its default location. If you use
> your computer's start menu, it may want to save files in your desktop or
> documents directory instead. You can change this by navigating to
> another directory the first time you "Save As..."

To create a new file and open nano, type

~~~ {.bash}
$ nano notes.txt
~~~


*Pause to make sure this worked for everyone, especially Windows users who may not have installed nano.*

Now, type a line of text, something like "This is where I am keeping my notes." To exit, hit Ctrl-X, then Y (to save), then Enter.

Now use `ls` to view the contents of your desktop. Do you see the file you created? *(Does anyone not see it?)*

**Exercise:** View the contents of the file you just created within your terminal (hint: we learned a command for viewing the contents of a file in the last section). Then, open the file, add some more text to it, save it, and exit.

## Manipulating the file system

Make directories with `mkdir`. This will create a new directory within the current directory.

~~~ {.bash}
$ mkdir swc-wsu
~~~


You can create as many folders as you like in a single call.

~~~ {.bash}
$ mkdir directory_name_1 directory_name_2 directory_name_3
~~~


To copy and move files, we use the commands `cp` and `mv`, followed by the file you want to copy/move, and then the location that you want to copy/move it to.

~~~ {.bash}
$ cp file1 file2
$ mv file1 file2
~~~


So if I am in my data directory and I want to copy or move one of the data files to my desktop, I would do. *(Do these, then show them on the Desktop. Do rm ~/Desktop/car-speeds.csv in between.)*

~~~ {.bash}
$ cp gapminder.csv swc-wsu/
$ mv gapminder.csv swc-wsu/
~~~


`cp` and `mv` can also rename files. If you want to rename a file in place, just do:

~~~ {.bash}
$ mv file_oldname file_newname
~~~


When we moved `gapminder.csv` to the `swc-wsu` folder, if we'd wanted to rename it at the same time we could have done:

~~~ {.bash}
$ cp gapminder.csv swc-wsu/gapminder-2.csv
~~~


Both `cp` and `mv` can be used with directories in addition to files.

See the `man` command to get help on options you can use with these commands.

Remove files with `rm`.

> ### Challenge {.challenge}
>
> In the `swc-wsu` folder create two subdirectories: one called `R` and one
> called `figures`.

## Let's try out some of the commands above

First create a temporary directory on your desktop. *Ask for people to call out commands to make directory and navigate into it.*

~~~ {.bash}
$ cd ~/Desktop
$ mkdir scratchpad
$ cd scratchpad
~~~


Make a few directories inside `scratchpad`

~~~ {.bash}
$ mkdir dir1 dir2 dir3
$ cp ~/Desktop/swc-data/*.png .
~~~


Use `ls` to view the contents of the current directory. What just happened? *(Ask for a volunteer)*

This is our first introduction to wildcards, which I'm going to talk a bit more about later. The `*.png` is telling the computer to match anything that ends in `.png`, which in this case is all of the figures from Karl's ggplot2 lesson.

Now try and remove scratchpad.

~~~ {.bash}
rm scratchpad
~~~


What just happened? If you want to remove everything within scratchpad no matter what, you will need to add the `-r` argument to function `rm`

~~~ {.bash}
rm -r scratchpad
~~~

One could also create lots of subdirectories at once using curly brackets expansions (not entirely sure if this works on Windows).

~~~ {.bash}
mkdir temp
cd temp
ls
mkdir dir-{0..10}
ls
rm -r temp
~~~


> ### Challenge {.challenge}
>
> Using the shell, create a folder on your desktop for materials from this
> workshop that looks like this:
>
> ~~~ {.output}
> |-- swc-wsu/
> |-- |-- data/
> |-- |-- |-- (data here)
> |-- |-- figures/
> |-- |-- |-- (figures here)
> |-- |-- notes/
> |-- |-- R/
> |-- |-- |-- (R scripts here)
> |-- |-- swc-wsu.Rproj
> ~~~

Note that this will break read.csv in your R script *go to RStudio and
demonstrate, then use relative paths to fix loading of data*

It is a good idea to keep all the materials for a given project or analysis
organized. Separating data (raw vs cleaned), scripts, figures, and manuscript
text in a logical project structure will help you and your collaborators
understand what is 

***
Acknowledgments: these lessons were adapted by Kara Woo from materials by [Diego Barneche](http://nicercode.github.io/2014-02-13-UNSW/lessons/60-shell/).
