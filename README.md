# node_modules-disk-image

<center>
<img alt="A meme about node_modules being the heaviest object in the universe" src="./meme.jpg" width="400">
</center>

This is a macOS-only tool that creates a disk image to put `node_modules` in.

This allows `node_modules` to be treated as a single file, resulting in these
benefits:

- Spotlight won't go crazy indexing the contents in the background.
- Your Spotlight search results won't be cluttered with irrelevant files.
- Disk management tools will be able to calculate the "folder" size instantly.
  When calculating which disk usage across your computer, tools like
  GrandPerspective won't take 5-10 seconds calculating the size of each
  `node_modules` you have. tens of thousands of tiny files are copied
  individually.

This tool can't make your `node_modules` folder smaller, but at least it can
stop it from being annoying in other ways!

## Usage

**To install:**\
Clone this repo and give yourself an easy way to run `bin/nmg` from anywhere.

The easiest way is to add `bin/` to `$PATH`:

> To do this in fish, run: `fish_add_path bin`

> In other shells, add `export PATH="$PATH:path/to/cloned/repo/bin"` to your
> shell profile or rc file.

**To set up for a repo:**\
Run `nmg init` to create the `node_modules` disk image. Then, if you have an existing
`node_modules` folder, run `nmg migrate` to move it over to this new system.

**Now everything is set up!**\
Run `nmg mount` to mount the disk image, and `nmg unmount` to unmount it. (You can
also click the eject button in Finder.)

# Related

Seen something similar before? Electron apps like Slack and VSCode also they
pack their `node_modules` into a single file, an
[asar archive](https://www.electronjs.org/docs/latest/tutorial/asar-archives).
However, it requires a patch to trick Node into thinking it's a normal folder,
so it only works in Electron. Even if hypothetically that patch was upstreamed,
the asar format is read-only, so you can't install new packages.
