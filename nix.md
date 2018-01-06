# Nix Package Manager

### Channels

Subscribe to the nixpkgs-unstable channel:

    nix-channel --add https://nixos.org/channels/nixpkgs-unstable
    nix-channel --update


### Commands

    nix-env -qa <package>                             List all available packages
    nix-env -qa <package> --description               List packages with description

    nix-env -e <package>                              Uninstall package


#### Compiling using Nix libraries

Install pkgconfig:

    nix-env -i pkgconfig

Open a shell with the appropriate environment variables for the selected libraries set:

    nix-shell -p pkgconfig [libraries]

This will set the `PATH`, `PKG_CONFIG_PATH`, `LIBRARY_PATH`, `LD_LIBRARY_PATH`, and `CPATH` to the correct values in
order to find the libraries and include files for the chosen libraries.

Then compile your code, install your gems, etc, as normal.
