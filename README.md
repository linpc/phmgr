phmgr
====
A simple host manager co-worked with native `known_hosts` file

Usage
----
Just type `pssh` in your console, and you can see a menu listing that
auto-generated from your `~/.ssh/known_hosts`

    $ pssh

You can quickly select what you want to do after the prompt:

    Please input your selection:

by four menas:

1. quick connect to `item 2` in the menu using `ssh`

        Please input your selection: 2

2. or using `ping`, `mosh`, `scp` by prepend command to the selection:

        Please input your selection: p 2
        Please input your selection: ping 2
        Please input your selection: m 2
        Please input your selection: mosh 2
        Please input your selection: scp 2

3. for `scp` command, use the following syntax to doing scp copy:

    from local to remote:
          * Use scp, please provide target >> local/path/file :remote/path/file

    from remote to local:
          * Use scp, please provide target >> :remote/file local/path/file

    prepend `-r` before the path if you want to recursively copy a directory


4. use `q`, `quit`, or `exit` to exit the menu.

Optional Config
----
If you have a bunch of hosts that make the menu hard to search,
you can use `~/.ssh/pssh_config` to classify hosts into different group.

The syntax of `pssh_config` is `YAML`

Use `qq`, `..`, or `../` to go back from sub-menu to main menu

* class: The class name displaying in `pssh` menu
* host: be used to do equal match with host/ip
* regexp: Perl regexp format to do pattern match with host/ip

Example config:

    classes:
      - class: School
        host:
          - 10.113.23.1
          - 10.113.23.2
        regexp:
          - .*.cs.nctu.edu.tw

      - class: *.linpc.org
        regexp:
          - .*.linpc.org

      - class: My Develop Env
        host:
          - dev1.example.com
          - dev2.example.com
