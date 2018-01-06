#### Command line

    list-sessions                     List sessions

    new-session                       Create session without name
    new -s <sess-name>                Create named session
    new -s <sess-name> -n <win-name>  Create named session with named window
    attach -t <sess-name>             Attach to a named session


#### Misc

    PREFIX ?                          List keybindings
    PREFIX :                          Enter command mode


#### Sessions

    PREFIX d                          Detach session


#### Windows

    PREFIX c                          Create window
    PREFIX ,                          Rename window
    PREFIX n                          Next window
    PREFIX p                          Previous window
    PREFIX f                          Find window
    PREFIX w                          Display window list
    PREFIX &                          Close window


#### Panes

    PREFIX %                          Split window vertically
    PREFIX "                          Split window horizontally
    PREFIX o                          Cycle though panes
    PREFIX <arrow>                    Navigate to pane
    PREFIX SPACEBAR                   Cycle through pane template
    PREFIX x                          Close pane
