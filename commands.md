#### List open ports and processes that own them

    lsof -i -n
    netstat -antdlpu


#### Delete a network interface

    ip link del <name>


#### Open serial interface

    screen /dev/tty.<name> <baud_rate>


#### Find

    find <dir> -name <pattern>                      Find <pattern> in <dir>
    find -L <dir> -name <pattern>                   Find <pattern> in <dir>, following symlinks
