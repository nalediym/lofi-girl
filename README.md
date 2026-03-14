# gifterm

Play animated GIFs natively in your terminal.

![gifterm demo](demo.gif)

## Why

Terminals are where we live. They deserve to feel alive. gifterm brings lofi
vibes, pixel art, and ambient animation to your workspace -- no browser tab, no
electron app, just frames on your GPU.

## Install

```
git clone https://github.com/nalediym/gifterm.git
cd gifterm
cargo install --path .
```

Builds a single static binary. No runtime dependencies.

## Usage

```
gifterm lofi.gif                  # play a GIF
gifterm lofi.gif --width 400      # scale down to 400px wide
gifterm lofi.gif --cache-only     # decode and cache without playing
```

The animation is fire-and-forget: it persists in kitty after `gifterm` exits,
living on the GPU like an `<img>` on a webpage. Clear the screen to dismiss it.

Multiple animations can run simultaneously -- each gets a unique image ID.

## Requirements

A terminal that supports the [kitty graphics protocol](https://sw.kovidgoyal.net/kitty/graphics-protocol/):

- [kitty](https://sw.kovidgoyal.net/kitty/)
- [WezTerm](https://wezfurlong.org/wezterm/)
- [Konsole](https://konsole.kde.org/) (partial support)

tmux blocks the graphics protocol by default. Set `allow-passthrough on` in
your tmux.conf, or run gifterm in a raw terminal window.

## How it works

gifterm decodes GIF frames into raw RGBA buffers using the `image` crate,
optionally scaling them down with Lanczos3 filtering. Decoded frames are cached
to `~/.cache/gifterm/` keyed by a SHA-256 hash of the source file, so
subsequent plays are instant.

Frames are transmitted to the terminal via kitty's graphics protocol using
temp-file transfer (`t=t`), then assembled into a looping animation that kitty
manages entirely on the GPU side. The CLI process exits immediately -- the
animation keeps running.

## Contributing

Contributions welcome. To get started:

```
git clone https://github.com/nalediym/gifterm.git
cd gifterm
cargo build
```

The codebase is a single file (`src/main.rs`) with a straightforward pipeline:
GIF decode -> frame cache -> kitty graphics protocol transmission.

Some areas that could use help:

- **Sixel support** -- for terminals that don't support kitty graphics (e.g. foot, mlterm)
- **APNG / WebP** -- extend beyond GIF to other animated formats
- **Speed control** -- `--speed 2x` or `--fps 30` flags
- **Cleanup command** -- `gifterm --clear` to remove cached frames

Open an issue before starting large changes so we can align on direction.

## License

MIT
