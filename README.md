This is a [standard-spec](https://github.com/sunjay/brainfuck/blob/master/brainfuck.md) brainfuck interpreter I've written in zsh.


Usage:

    ./bf_run /path/to/brainfuck/program.bf
    ./bf_run $brainfuck_program


Flag 'memlimit' controls memory size in mb (default 1mb):

    memlimit=512 ./bf_run /path/to/brainfuck/program.bf

Above example runs program.bf with 512mb memory

Memory wrapping is disabled by default, but can be enabled by setting 'mem_wrap' to 1 before launch, like so:

    mem_wrap=1 ./bf_run /path/to/brainfuck/program.bf


By default, bf_run executes with an 8-bit bitmask, meaning cells wrap after 255 (this is accurate to brainfuck spec). However, there are times when it is much more useful to have a higher ceiling (such as with calculator.bf).

Flag 'bits' solves this. Set to 16, 32, 64, or 128 in order to modify bitmask.

    bits=32 ./bf_run /path/to/brainfuck/program.bf

Note that 64-bit/128-bit modes require 'libalm' (https://github.com/m1ndflay3r/libalm) and will prompt to install it if not found.


Flag 'streamfile' controls file to be used for byte stream:

    streamfile=/path/to/file.txt ./bf_run /path/to/brainfuck/program.bf

Above example runs program.bf with file.txt as streamfile.

If 'streamfile' is not set, bf_run will instead fetch bytes interactively.

If 'streamfile' is set but doesnt exist, all byte stream calls will result in 0.

Contents of specified streamfile can be modified mid-program and these changes will be detected.

You can use FIFO as streamfile for dynamic non-interactive bytestream like so:

    mkfifo /tmp/brainfuck_stream
    streamfile=/tmp/brainfuck_stream /path/to/brainfuck/program.bf

Data should be sent to the above FIFO in 1-byte increments padded with null bytes equating to current streamfile offset value, as streamfile is reread on every byte (which is what allows for dynamic byte stream via FIFO to exist).


An example program (helloworld.bf) is included with this interpreter for testing purposes.

You can run it like so:

    ./bf_run examples/helloworld.bf

Another example program (calculator.bf) is included with this interpreter for testing purposes (https://github.com/dougaak/brainfuck-calculator).

You can run it like so:

    ./bf_run examples/calculator.bf

Lastly, example program (stream.bf) is included with this interpreter for streamfile demonstration.

You can run it like so:

    streamfile=examples/streamfile_ex ./bf_run examples/stream.bf
