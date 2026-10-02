
> https://www.freecodecamp.org/news/how-to-search-files-in-the-linux-terminal/

## How to Search a File by Name

Let’s say you saved a file called `hello_world.html` somewhere and you don’t even remember the directory name. But your boss is asking you to send them the file immediately.

Usually, if you forgot where you stored a file, you'd begin by going through folder after folder and checking if the file exists.

This is when the `find` command does a great job. Instead of searching the file manually on your computer, you can use the `find` command to automate the process.

By passing the name of the file using the `-name` flag, the `find` command searches and returns the location of the file.

```bash
find -name <file_name>
```

But remember the `-name` flag performs a case-sensitive search. If you are looking to do a case-insensitive search, you can use the `-iname` flag instead.

```bash
find -iname <file_name>
```

You can also use the `find` command as an alternative to the `ls` command in some places. Let's assume you need to find all the files ending with the `.txt` extension. You can do so with the `find` command using the regex pattern (`*.txt`).

```bash
find /path/to/search -name "*.txt"
```

This command will list all the `.txt` files in your current directory and its sub-directories.

To find `.txt` files in a particular directory and sub-directory, you can replace the `/path/to/search` with the path of your directory.

## How to Find a Directory in Linux

Searching for a directory is possible by passing the `d` to the `-type` parameter in the `find` command.

```bash
find /path/to/search -type d
```

In the above screenshot, we're finding a directory named `zip` from our current directory.

Similarly the `-type` option accepts other parameter options to simplify our finding process.

- `f` finds the list of regular files
- `b` finds the list of block devices
- `c` finds the list of character devices
- `l` finds the list of symbolic links
- `s` finds the list of sockets
- `p` finds the named pipes

## How to Search a File by Size in Linux

Adding the `-size` option along with the `find` command helps you find files based on size. Prepend a `+` or `-` to the size to represent greater than and less than, respectively.

```bash
find /path/to/search -size <size_of_the_file>
```

You can also search for all files that fall within a specific size range.

For example, if you want to find all the files that are above 50 MB and below 100 MB, you can run the following command:

```bash
find /path/to/search -size +50M -size -100M
```

You can specify the size in your preferred notation. A few of the available notations are:

1. K represents KB
2. M represents MB
3. G represents GB
4. b represents bytes
5. c represents blocks

## How to Search a File Based on Time Modified

Every file has a created and last updated time associated with it. Let's assume you have thousands of files in your directory. You edited a file in the past couple of days and forgot its name. You're sure that you have edited only a couple of files after that.

In such cases, you can find all the files that were modified within the past 7 days. This limits your search from 1000+ files to a more manageable amount. You'll be able to find the file you edited in seconds after running the command.

This is possible by passing `-mtime` parameter with the `find` command.

```
find /path/to/search -mtime <-number_of_days_ago>
```

Let's assume another scenario, where today's date is February 10, 2023. You modified a file before Feb 3, 2023. After Feb 3, 2023, you modified a lot of files. You have to find the file which you modified before Feb 3, 2023. So, basically, you need the files that were modified before Feb 3, 2023.

Strange scenario, right?

But, you can also run this query using the `find` command. You can achieve this by exchanging the negative sign (-) with the positive sign (+).

Here's the modified command for you:

```bash
find /path/to/search -mtime +7
```

`find` command syntax to search files modified before certain days

## How to Execute a Command on Files Filtered from the `find` Command

This question may confuse you. Before revealing the answer, let's understand the question clearly with a real scenario.

Let's assume you have 1000 files in a directory, and running the `find` command returns 20 matching files. You want to move these 20 files into a different directory. How can you achieve that?

Simply put, we have to run a command over each of the filtered files.

You can do this by passing the `-exec` option with the `find` command.

The `-exec` option executes a command on each file that is found in the search. The `-exec` option is followed by a command and its arguments, with the `{}` symbols representing the path of the file being processed.

To represent the end of the `-exec` command, we have to add `\;` (a backward slash and a semi-colon).

Here's the syntax:

```bash
find /path/to/search -name  -exec  {}  \;
```

Let’s try to move the filtered files from the `5minslearn` directory to the `zip` directory.

Here’s the command:

```
find ./5minslearn -name "*.zip" -exec mv {} ./5minslearn/zip \;
```

This command searches for all files ending with a `.zip` in the `./5minslearn` directory and then moves each file to the `./5minslearn/zip` directory.

The `-exec` option allows you to perform a wide range of operations on the files that are found. You can replace the move command from the above example by copying, deleting, or even changing the file permission command.

## How to Execute a Command on Files Filtered with a Confirmation

Most people will prefer to use this if they're not sure about whether to apply the operation on each file.

The `-ok` option is similar to the **`-exec`** option except that it will ask for confirmation before executing the operation on each file. This command is super helpful to review files that will be affected before executing the specific operation. You also have the option to decline if you're not sure or don't wish to apply the command.

For example, this time let's try to move the `.txt` files to the other directory.

```bash
find /path/to/search -name "*.txt" -ok mv {} /path/to/destination \;
```

The above command searches for all files with a `.txt` extension in the `./5minslearn` directory and then prompts the user to confirm before moving each file to the `./5minslearn/text_files` directory.

To approve the operation, enter `yes` and `no` to decline the operation and skip to the next file.

The `-ok` option is useful when you want to be cautious about the files you are modifying, as it allows you to inspect each file and its location before executing the specified command.

## How to Find a File with Detailed Information

The `-ls` option in the find command is used to display information about the files found in the search, in the format of the ls command. This option provides detailed information about the files, such as their permissions, owner, size, and last modified time.

```
find /path/to/search -name "*.<file-extension>" -ls
```

## How to Find and Remove Files

Have you ever needed to find files and remove them from your computer? The `-delete` option in the find command does this for you. It allows you to delete files that match the specified criteria.

```bash
find . -name "*.<extension>" -delete
```

Note: This operation is irreversible. Be 100% sure when you run the delete operation.

I would advise running the `find` command without the `-delete` flag at first and ensure that only the files that need to be deleted are shown. Once you're sure, you can execute the same command appending `-delete` flag.
