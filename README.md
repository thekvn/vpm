# VARS Project Manager (vpm)

A CLI tool that helps manage local projects.

## Features

You can:
- hash the current working directory to `vpm` and give it a key/alias (i.e. the project name `example-project`)
- quickly `cd` into any hashed projects in `vpm` by using the key you previously provided (i.e. `vpm cd example-project`)
- quickly open a project using either Sublime/Xcode/Atom (it scans for Sublime/Xcode project files first then falls back to Sublime/Atom) as long as the project is hashed in `vpm`

## Commands

`vpm add <project_alias>`: Maps the current working directory to a project alias.

`vpm cd <project_alias_or_index>`: Changes the working directory to the working directory of a `vpm` project.

`vpm list`: Lists all current projects managed by `vpm`

`vpm open <project_alias_or_index` Opens the working directory of a `vpm` project in Finder.

`vpm project <project_alias_or_index` Opens a `vpm` project in designated IDE (supports Xcode/Sublime in respective priority).

`vpm remove <project_alias_or_index>`: Removes a `vpm` project from the `vpm` repository.

`vpm <command>`: When no project alias or index is specified, the last iterated project will be used to perform the `<command`>. You can use `vpm cache` to see what the last iterated project is. Not all commands support this notation.

`vpm <command> .`: Performs the `<command>` on the hashed project whose path equates the current directory (`pwd`). 

See `vpm help` or simply `vpm` for a full list of commands with details.

## Usage

Clone this repo and symlink to `/usr/local/bin` (you may need `sudo` access)
```
git clone https://github.com/variante/vpm.git
sudo ln -s /path/to/vpm /usr/local/bin
```
Create an alias in your local `.bash_profile` or equivalent so `vpm` can directly execute commands like `cd`
```
alias vpm=". vpm"
```

## Example

Suppose you have a web project located in `~/projects/SampleProject`. With `vpm`, you can enter shell, `cd` to that directory, and hash that directory to `vpm` with an alias/key by executing `vpm add SampleProject`, `SampleProject` being the alias/key.

You can then quickly access any project in the `vpm` hash by doing the following (using `SampleProject` as an example):

`vpm open SampleProject` will immediately open that directory in Finder

`vpm project SampleProject` will attempt to look for either an Xcode or Sublime in the root directory of `SampleProject` and open it

With this set up you can hash multiple projects into `vpm` and quickly access all of them. When the list of projects gets long, you can do `vpm list` to see the existing projects in the hash and simply access each of them by their index. For example, if `SampleProject` is the 6th project on the list, you can do `vpm open 6` to open it in Finder.

Most commands have equivalent short notations. For example, instead of doing `vpm project` you can do `vpm p`.

If you previously executed a command on a valid key, it stays in cache. You can then access it using `.`. i.e. `vpm p .`.  To view which key is cached, do `vpm cache`.

## License

This software is released under the [MIT License](http://opensource.org/licenses/MIT).
