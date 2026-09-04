# clon

A simple, interactive command-line backup tool for Linux. Back up a single file, a folder, a whole disk, or send a backup straight to a remote server — all from one menu-driven command.

## Features

- **File backup** — copies a single file with a timestamped name.
- **Folder backup** — compresses a folder into a timestamped `.tar.gz`.
- **Disk backup** — compresses the contents of a mounted disk/path into a timestamped `.tar.gz`.
- **Server backup** — sends a file or compressed folder to a remote server over SSH/SCP.
- Live progress while copying/compressing, so you always know it's working, not stuck.
- Warns you if a backup with the same name already exists in the destination before overwriting your disk space with another copy.
- Automatically creates the destination folder if it doesn't exist (with a `sudo` fallback if permissions are needed).
- Cleans up half-finished backups if you cancel with `Ctrl+C`.
- Installs as a normal command — run `clonny` from any directory, just like any other Linux tool.

## Project structure

```
clon/
├── clonny          # main entry point / menu
├── filebackup       # back up a single file
├── folderbackup      # back up a folder (compressed)
├── diskbackup        # back up a disk/mount path (compressed)
├── serverbackup       # back up a file or folder to a remote server
└── install.sh         # installer
```

`clonny` only loads the specific function it needs (`filebackup`, `folderbackup`, `diskbackup`, or `serverbackup`) at the moment you select it from the menu — not all four up front.

## Installation

### 1. Get the files onto your machine

Clone the repo, or download and extract a release tarball:

```bash
git clone https://github.com/<your-username>/clon.git
cd clon
```

or, if you have a `clon.tar.gz` archive instead:

```bash
tar -xzf clon.tar.gz
cd clon
```

### 2. Run the installer

**Just for yourself** (no admin rights needed):

```bash
./install.sh
```

Installs to `~/.local/share/clon` and symlinks `clonny` into `~/.local/bin`.

**For every user on the machine:**

```bash
sudo ./install.sh
```

Installs to `/opt/clon` and symlinks `clonny` into `/usr/local/bin`.

The installer detects which mode to use automatically based on whether it was run with `sudo`.

### 3. Start using it

Open a new terminal window (so your shell picks up the updated `PATH`), then just run:

```bash
clonny
```

from any directory — no `bash clonny`, no `./`, no need to remember where the project folder lives.

## Usage

Once running, `clonny` shows a simple menu:

```
Enter 'f' to back up a file, 'd' for a folder,
'h' for a hard-drive, 's' for server, or 'q' to quit:
```

- `f` — back up a single file
- `d` — back up a folder
- `h` — back up a disk / mounted path
- `s` — back up a file or folder to a remote server (you'll be asked for the server's IP)
- `q` — quit

For any backup, you'll be asked for a destination folder, or you can press `d` to use the default (`/var/www/html/clone/` locally, or the same path on the remote server for server backups).

After each backup completes, `clonny` asks if you'd like to run another one or exit.

## Requirements

- Bash
- `tar`, `du`, `find` (standard on virtually every Linux system)
- `ssh` and `scp` (only needed for server backups)
- `sudo` (only needed if the destination folder requires elevated permissions to create)


## License

This project is licensed under the GNU General Public License v3.0 — see [`LICENSE`](LICENSE) for the full text.
