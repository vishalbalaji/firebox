# Firebox *(working title)*

## What?
Firebox(*working title*) is shell script to make Firefox emulate app browsers like [Ferdi](https://github.com/getferdi/ferdi) or [Rambox](https://rambox.app). But, instead of a  heavy chromium-based application, it is a 17Kb shell script, an existing installation of [Mozilla Firefox](https://www.mozilla.org/en-US/firefox/new/)*(if you use firefox, that is)* and some basic GNU utilities like `grep`, `sed` and `xargs`.

## Why?

The primary motivation for this project is that programs like **Ferdi** and **Rambox** don't have a proper CLI, lacking essential features(for me, at least) like launching individual services from the command line.

Also, there is the chromium of it all. I use Firefox as my primary browser and I don't particularly notice any differences using modern apps like [Discord](https://discord.com) and [Whatsapp](https://web.whatsapp.com) in Firefox compared to Chromium.

## How?

Firebox creates a profile, separate from your existing firefox profiles, in your `$HOME/.local/share/` directory. You create new services by creating bookmarks in this newly created profile and workspaces using these existing services. These services and workspaces can then be launched and managed using the CLI.

## Features

* Create and manage services by reading in Firefox bookmarks.
* Individually launch one or more services straight from the command line.
* Create groupings of services or `workspaces`, that can be launched and managed from the command line.

## Requirements

* `firefox`
* `grep`
* `sed`
* `xargs`
* `sqlite3`

## Installation

Clone this repo(`git clone https://github.com/vishalbalaji/firebox`) or manually download the necessary files and place the `firebox` script in a directory present in your `PATH`. Then, make the script executable using:

```sh
chmod +x /path/to/firebox
```

## Usage

You can run `firebox --help` to print out a list of available commands. Same goes for all available commands(for example, `firebox service --help`).

### Initialization

You need to initialize `firebox` before being able to add services. You can do so by running `firebox init`.

### Services

To add new services, you can run `firebox explorer`. This will open up a browser window where you can browse websites and create or delete bookmarks. Once you close the `explorer` window, you will then be shown a list of changes and prompted as to whether you want to write these changes.

The bookmarks that you added will be saved as services. You can then list all available services by running `firebox service list` and launch those services using `firebox service launch <service-1> <service-2>...`.

https://user-images.githubusercontent.com/36506250/203126129-d2586e2d-02e1-44f0-bafd-2461ec618b28.mp4

https://user-images.githubusercontent.com/36506250/203126169-6e799b2b-4137-4433-b481-aa55367eefb0.mp4

### Workspaces

You can create and manage **Workspaces** like in **Ferdi** using the `firebox workspace` command.

* To create a workspace, run `firebox workspace create <workspace-name>`.
* To add services to a particular workspace, run `firebox workspace add <workspace-name> <service-1> <service-2>...`.
* To list a workspace and its services, run `firebox workspace list <workspace-name>`. You can also run `firebox workspace list --all` to list all workspaces.
* To launch a workspace, run `firebox workspace launch <workspace-name>`.
* To remove services to a particular workspace, run `firebox workspace remove <workspace-name> <service-1> <service-2>...`.
* To delete a workspace, run `firebox workspace delete <workspace-name>`.

https://user-images.githubusercontent.com/36506250/203126815-4ae6f3eb-241c-4129-8157-9cb191c5846b.mp4

### Clean

If you want to delete the created profile and all related files, you can do so by using Firefox's `Profile Manager`. Simply run `firefox -ProfileManager`, select the profile named `firebox`, click on `Delete Profile` and then `Delete Files`.

https://user-images.githubusercontent.com/36506250/203126345-bb7ec431-3712-4bb1-9006-d2c06b6ea692.mp4

### Additional Options

`firebox` also exposes an option called `config`, which is used to access data used internally which can be used to write custom scripts using firebox. More information about this option is available by running: `firebox config -h`. Some examples of custom scripts written around `firebox` are demonstrated below.

# `firebox_fzf`

A wrapper script around `firebox` using `fzf`. This allows for a few more handy features, such as fuzzy searching, multi-selection, etc. This script acts as a wrapper around `fzf`, so any flags passed to this command will be passed down to `fzf`, such as `--reverse` or `--height`.

## Requirements

* Same requirements as for `firebox`
* `fzf`

## Installation

Make sure that `firebox` is in your path and executable and follow the same steps for the `firebox_fzf` script.

## Usage

Running `firebox_fzf` will open an `fzf` prompt with all the available options from `firebox`, except for `config`, such as `explorer`, `service`, `workspace`.

# `firebox_dmenu`

A wrapper script around `firebox` using `dmenu`. This is for if you wish to launch services and workspaces directly without opening a terminal. Like `firebox_fzf`, any flags passed to this command will be passed down to `dmenu`.

## Requirements

* Same requirements as for `firebox`
* `dmenu`

**NOTE:** This script relies on the `TERMINAL` environment variable. By default, it is set to `xterm`, but make sure to set it to the terminal emulator of your choice. For example, if you use `kitty`, you would set the variable as so:

```sh
export TERMINAL=kitty
```

You can do this in your `.xprofile`, `.bashrc` or equivalent files so that they are accessible globally. Or, you could export it inline, in case you want to override your current setting like so:

```sh
TERMINAL=kitty firebox_dmenu
```

## Installation

Make sure that `firebox` is in your path and executable and follow the same steps for the `firebox_dmenu` script.

## Usage

Running `firebox_dmenu` will open dmenu with all the available options from `firebox`, except for `config`, such as `explorer`, `service`, `workspace`.

## TODOs

* [ ] Completion...?
* [ ] Fix bug where text case of names in workspaces and logs don't correspond to the actual service name.
* [ ] Better error and log handling.
* [ ] Update requirements in `README`.
