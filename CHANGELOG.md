# master

# 0.4

This release includes many refactors and cleanups to the code. Flicker in
drawing the UI has been resolved, and work has begun on macOS support. And
finally, the algorithm for matching on filenames has received an update and
should be even more precise.

Commit hashes are now included in the changelog for convenience.

* **feat**: increase ranking algorithm precision
  ([d31e70](https://github.com/natecraddock/zf/commit/d31e70))

  Matches on filenames are now given a rank priority relative to the percentage
  of the filename matched. As more query term letters match the filename, the
  higher it ranks.

* **feat**: draw count information in the query line
  ([6aa45e](https://github.com/natecraddock/zf/commit/6aa45e))

  Display a [filtered count]/[total count] indicator on the right side of the
  query line. Currently this is enabled and cannot be toggled, but a flag will
  be added soon.

* **feat**: add more readline bindings ([@jmbaur](https://github.com/jmbaur))
  ([9c7a78](https://github.com/natecraddock/zf/commit/9c7a78))

* **feat**: add `ctrl-j` and `ctrl-k` mappings
  ([3fb459](https://github.com/natecraddock/zf/commit/3fb459))

* **feat**: switch from bright blue to cyan for highlights
  ([ee05d3](https://github.com/natecraddock/zf/commit/ee05d3))

* **fix**: delete keybinding
  ([cbb467](https://github.com/natecraddock/zf/commit/cbb467))

* **fix**: remove flicker in the TUI
  ([cc7c2c](https://github.com/natecraddock/zf/commit/cc7c2c))

  The default TTY writer was not buffered. Buffering the output reduces syscalls
  and makes the TUI much more responsive!

* **fix**: emit DECCKM "application mode" escape sequences
  ([@ratfactor](https://github.com/ratfactor))
  ([d2c795](https://github.com/natecraddock/zf/commit/d2c795))

* **fix**: failure to render TUI on macOS
  ([9ade19](https://github.com/natecraddock/zf/commit/9ade19))

  macOS support is still not official, but should work better now.

# 0.3

This release improves the ranking algorithm, adds two new commandline options,
fixes a few bugs, and optimizes the TUI drawing code. Shell completion scripts
are now provided for bash, zsh, and fish.

* **feat**: prioritize matches on beginning of words

  Matches that begin at the start of a word will be ranked higher than matches
  in the middle of a word.

* **feat**: add keep order option (`-k` `--keep-order`)

  Adds an option to skip sorting of items and preserve the order of lines read
  on stdin.

* **feat**: add plain text option ('-p' '--plain')

  Adds an option to skip the filename match prioritization. Useful when the
  lines are not filepaths.

* **feat**: expose case-sensitive matching in libzf

  Update to the zf algorithm to make matching more precise. Matches on the
  beginning of words are ranked higher.

* **extra**: add shell completions for bash, zsh, and fish

* **fix**: query mangling when moving the cursor left or right

* **fix**: off-by-one scrolling error at bottom of terminals

  When zf was run at the bottom of a terminal the scrolling would remove the
  previous prompt.

* **fix**: don't require pressing esc three times to cancel

# 0.2

This release fixes a few minor bugs, optimizes drawing the terminal user
interface, and introduces a number of new features:

* **feat**: add `libzf` ffi library

  Exposes the zf ranking algorithm to be used as a library. See
  [natecraddock/telescope-zf-native.nvim](https://github.com/natecraddock/telescope-zf-native.nvim)
  for an example neovim plugin that uses libzf.

* **feat**: match highlights

  The results are now highlighted to show the substrings that match the query
  tokens.

* **feat**: drop semver.

  Once v1.0 is released, the commandline argument api will be stabilized. Any
  changes to flags will require a major version increment. Any fixes and
  non-breaking features are considered minor releases.

* **break**: rename `--query` flag to `--filter`

  This makes more sense, and is compatible with fzf. It also makes it possible
  to support a `--query` flag in the future if needed.

* **feat**: add `--lines [num lines]` option

  Allows controlling the number of displayed result lines in the terminal user
  interface.

# 0.0.1

Initial release
