Getting Started Guide
=====================

First of all you need erlang installed, version should be >= 17.0, on
ubuntu it should be enough with::

    sudo apt-get install erlang-nox erlang-dev

If something failes try installing this others (should be dependencies of the
ones above)::

    sudo apt-get install erlang-parsetools erlang-syntax-tools

Then you need to install rebar3, follow the instructions on http://www.rebar3.org/
should be enough with::

    mkdir -p ~/bin
    cd ~/bin
    wget https://s3.amazonaws.com/rebar3/rebar3
    chmod u+x rebar3

Add ~/bin to your $PATH if you don't have it already::

    export PATH=$PATH:$HOME/bin

Add it to your shell rc file to have it permanently set (.zshrc for zsh, .bashrc for bash)

Clone the interfix repository::

    git clone https://github.com/marianoguerra/interfix

Build it::

    make

If you don't have make install it, on ubuntu it's::

    sudo apt-get install build-essential

The binary is located at `./_build/default/bin/interfix`, to make your life easier create
a symbilic link::

    ln -s ./_build/default/bin/interfix

Now you can start compiling, to test that it works, convert some of the examples to erlang::

    ./interfix erl examples/calls.ifx

Now let's build a hello world, put this on a file called `hello.ifx`::

    fn+ hello:
        hello "world".

    fn+ hello Name:
        io :: format "hello ~s!~n" [Name].

Now compile it::

     ./interfix beam hello.ifx .

The second argument is the destination directory, in this case, the current directory.

Now let's try it from the erlang shell::

    $ erl

    Erlang/OTP 18 [erts-7.0] [source] [64-bit] [smp:4:4] [async-threads:10] [kernel-poll:false]

    Eshell V7.0  (abort with ^G)
    1> hello:hello().
    hello world!
    ok
    2> hello:hello("Bob").
    hello Bob!
    ok
    3> q().
    ok

