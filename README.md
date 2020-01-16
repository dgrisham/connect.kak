# connect.kak

Connect a program to [Kakoune] clients.

## Installation

Add [`rc`] to your autoload or source [`connect.kak`] and its [modules] manually.

### Add to desktop

1. Copy [`kakoune-connect.desktop`] to `$XDG_DATA_HOME/applications`.
2. Add [`kak-connect`] to your path.
3. Open `$XDG_CONFIG_HOME/mimeapps.list` and add the following MIME type association.

```
[Default Applications]
text/plain=kakoune-connect.desktop
```

Add more entries to your liking.

[`kakoune-connect.desktop`]: share/applications/kakoune-connect.desktop
[`kak-connect`]: bin/kak-connect

## Usage

Connect a terminal with [`:connect-terminal`].  Open files with [`edit`] or your
favorite program; buffers with the [`buffer`] command…

If you loaded the [modules], [`:fzf-files`] and [`:fzf-buffers`] commands are
also available.  connect.kak currently has batteries for [fzf], [Rofi], [lf]
and [Dolphin].

**Note**: [`fzf`] and [`rofi`] modules require [fd] for listing files.

**Example** – **Kakoune** – Connect a terminal with [`:connect-terminal`]:

``` kak
connect-terminal
```

Or simply [`:t`].

**Example** – **Terminal** – Send a file to the client with [`edit`] or its alias [`e`]:

``` sh
edit file.txt
```

**Example** – **Terminal** – Open multiple files:

``` sh
e *.txt
```

**Example** – **Terminal** – Open files with [lf]:

``` sh
lf
```

**Note**: Not to be confused with [`:lf`].  connect.kak pairs with [modules]
that you can load with the [`:require-module`] command.

Also works great with GUI programs.

**Example** – **Kakoune** – Open files with [Dolphin]:

``` kak
connect-shell dolphin
```

Or simply [`:dolphin`] if you have loaded the module.

**Example** – **Kakoune** – Open selected files with [Rofi]:

``` kak
connect-shell %{
  edit $(fd --type file | rofi -dmenu)
}
```

**Example** – **Terminal** – List all buffers with [`buffer`] or its alias [`b`]:

``` sh
buffer
```

**Example** – **Terminal** – Open buffers with [fzf]:

``` sh
b $(b | fzf)
```

**Example** – **Terminal** – [`git-add`] the current buffer:

``` sh
git add $(it)
```

**Example** – **Terminal** – Render Markdown with [Glow]:

``` sh
glow $(it)
```

**Example** – **Terminal** – Load a previous yank with [fzf], by sending the result to [`:yank-ring-load-from-file`]:

``` sh
send yank-ring-load-from-file $(find $(get %opt{yank_ring_path}) -type f | sort -n -r | fzf --preview 'cat {}')
```

**Note**: If you have [yank-ring.kak] installed, you can simply call [`:yank-ring`].

## Configuration

``` kak
require-module connect-fzf
require-module connect-rofi
require-module connect-lf
require-module connect-dolphin

map global normal <c-t> ': connect-terminal<ret>'
```

## Kakoune commands

- [`:connect-terminal`] | [`:t`]
- [`:connect-shell`]
- [`:fzf-files`] | [`:fzf`]
- [`:fzf-buffers`]
- [`:rofi-files`] | [`:rofi`]
- [`:rofi-buffers`]
- [`:lf`]
- [`:dolphin`]

[`rc`]: rc
[modules]: rc/modules

[`connect.kak`]: rc/connect.kak
[`:connect-terminal`]: rc/connect.kak
[`:t`]: rc/connect.kak
[`:connect-shell`]: rc/connect.kak

[`fzf`]: rc/modules/fzf.kak
[`:fzf-files`]: rc/modules/fzf.kak
[`:fzf`]: rc/modules/fzf.kak
[`:fzf-buffers`]: rc/modules/fzf.kak

[`rofi`]: rc/modules/rofi.kak
[`:rofi-files`]: rc/modules/rofi.kak
[`:rofi`]: rc/modules/rofi.kak
[`:rofi-buffers`]: rc/modules/rofi.kak

[`lf`]: rc/modules/lf.kak
[`:lf`]: rc/modules/lf.kak

[`dolphin`]: rc/modules/dolphin.kak
[`:dolphin`]: rc/modules/dolphin.kak

## Shell commands

- [`edit`] | [`e`]
- [`buffer`] | [`b`]
- [`it`]
- [`send`]
- [`get`]

[`edit`]: rc/paths/commands/edit
[`e`]: rc/paths/aliases/e
[`buffer`]: rc/paths/commands/buffer
[`b`]: rc/paths/aliases/b
[`it`]: rc/paths/commands/it
[`send`]: rc/paths/commands/send
[`get`]: rc/paths/commands/get

[Kakoune]: https://kakoune.org
[fzf]: https://github.com/junegunn/fzf
[Rofi]: https://github.com/davatorium/rofi
[lf]: https://github.com/gokcehan/lf
[Dolphin]: https://dolphin.kde.org
[fd]: https://github.com/sharkdp/fd
[jq]: https://stedolan.github.io/jq/
[yank-ring.kak]: https://github.com/alexherbo2/yank-ring.kak
[`:yank-ring`]: https://github.com/alexherbo2/yank-ring.kak
[`:yank-ring-load-from-file`]: https://github.com/alexherbo2/yank-ring.kak
[`git-add`]: https://git-scm.com/docs/git-add
[Glow]: https://github.com/charmbracelet/glow
[`:require-module`]: https://github.com/mawww/kakoune/blob/master/doc/pages/commands.asciidoc#module-commands
