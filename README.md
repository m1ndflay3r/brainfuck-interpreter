This is a [standard-spec](https://github.com/sunjay/brainfuck/blob/master/brainfuck.md) brainfuck interpreter I've written in zsh.


Usage:

    ./bf_run /path/to/brainfuck/program.bf
    ./bf_run $brainfuck_program


Flag 'memlimit' controls memory size in mb (default 1mb):

    memlimit=512 ./bf_run /path/to/brainfuck/program.bf

Above example runs program.bf with 512mb memory


Flag 'streamfile' controls file to be used for byte stream (default /tmp/bf_streamfile):

    streamfile=/path/to/file.txt ./bf_run /path/to/brainfuck/program.bf

Above example runs program.bf with file.txt as streamfile.

Contents of specified streamfile can be modified mid-program and these changes will be detected.


An example program (helloworld.bf) is included with this interpreter for testing purposes.

You can run it like so:

    ./bf_run helloworld.bf
