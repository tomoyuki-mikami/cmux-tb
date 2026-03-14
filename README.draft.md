<h1 align="center">cmux + TextBox</h1>
<p align="center">A fork of <a href="https://github.com/manaflow-ai/cmux">cmux</a> with a built-in TextBox input mode</p>

<p align="center">
  <img src="./docs/assets/textbox-hero.png" alt="TextBox screenshot" width="900" />
</p>

## Why TextBox?

Terminals weren't designed for writing long-form input. There's no easy way to go back and edit a previous line, selecting and cutting arbitrary ranges of text is cumbersome, and multi-line text requires awkward escapes or heredocs. For anyone used to normal text editors, this friction adds up fast.

TextBox adds a persistent input bar at the bottom of each terminal pane. It bridges the gap between a rich text editor and the raw terminal — two input modes that feel like one seamless experience.

- **When the TextBox is empty**, arrow keys, Tab, Backspace, and Ctrl shortcuts pass straight through to the terminal. It feels like you're typing directly into the shell.
- **When you're composing text**, it works like a familiar text editor — arrow keys navigate within your draft, and multi-line editing just works. Press Return (or click the send button) to submit.

No mode switching. No mental overhead. You type, and the right thing happens.

## Features

| Feature | Description |
|---------|-------------|
| **Seamless input** | When the TextBox is empty, arrow keys, Backspace, and other keys control the terminal directly. |
| **Ctrl shortcuts** | Ctrl+C, Ctrl+D, and other control sequences are forwarded to the terminal even while the TextBox is focused. |
| **Enter to Send** | Choose whether Return sends text immediately or inserts a newline (Shift+Return for the other). |
| **Toggle on/off** | Show or hide the TextBox anytime with a keyboard shortcut. |

## Install

This is a development fork. Clone and build from source:

```bash
git clone --recurse-submodules https://github.com/<your-username>/cmux.git
cd cmux
./scripts/setup.sh
./scripts/reload.sh --tag textbox
```

## Keyboard Shortcuts

### TextBox

| Shortcut | Action |
|----------|--------|
| ⌘ ⌥ T (Cmd + Option + T) | Toggle TextBox on/off |
| Return | Send text to terminal (when Enter-to-Send is enabled) |
| ⌥ Return (Option + Return) | Insert newline (when Enter-to-Send is enabled) |
| Escape | Return focus to terminal |

All standard cmux shortcuts continue to work. See the [cmux README](https://github.com/manaflow-ai/cmux#keyboard-shortcuts) for the full list.

## Settings

| Setting | Default | Description |
|---------|---------|-------------|
| Enabled | On | Show the TextBox input bar |
| Enter to Send | Off | Return key sends text (instead of inserting a newline) |

## License

Same as cmux — [AGPL-3.0-or-later](LICENSE).
