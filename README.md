# Firebox *(working title)*

## What?
Firebox(*working title*) is shell script to make Firefox emulate app browsers like [Ferdi](https://github.com/getferdi/ferdi) or [Rambox](https://rambox.app). But, instead of a  heavy chromium-based application, it is a 17Kb shell script, an existing installation of [Mozilla Firefox](https://www.mozilla.org/en-US/firefox/new/)*(if you use firefox, that is)* and some basic GNU utilities like `grep`, `sed` and `Xargs`.

## Why?

The primary motivation for this project is that programs like **Ferdi** and **Rambox** don't have a proper CLI, lacking essential features(for me, at least) like launching individual services from the command line.

Also, there is the chromium of it all. I use Firefox as my primary browser and I don't particularly notice any differences using modern apps like [Discord](https://discord.com) and [Whatsapp](https://web.whatsapp.com) in Firefox compared to Chromium.

## How?

Firebox creates a profile separate from your existing firefox in your `$HOME/.local/share/` directory. You create new services by creating bookmarks in this newly created profile and workspaces using these existing services. These services and workspaces can then be launched and managed using the CLI.

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

Clone this repo(`git clone https://github.com/vishalbalaji/firebox`) or manually download the necessary files and place the `firebox` script in a directory present in your `PATH`.

## Usage

You can run `firebox --help` to print out a list of available commands.

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
