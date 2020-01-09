# Local Modifications

## Middle click to paste

According to [#1700], it was an intentional design choice to not support
unshifted middle click to paste when in mouse mode. The check for this is in
`input.rs` under the matcher for `Action::PasteSelection`, where it checks
`!mouse_mode` before working.

[#1700]: https://github.com/jwilm/alacritty/issues/1700

Simply changing from `PasteSelection` to `Paste` suppresses the check, but
it now sends the click through to the app in addition to pasting, which works
sometimes (when there's nothing to paste in tmux, it seems) but not always.

## Block selection with alt

Block selection was initially discussed in [#981], with a config option for
ctrl vs alt, but this PR was never merged. It finally landed in [#2552], but
the config option was dropped because "alt is already passed through to some
applications which can't use anything else since shift and control is already
occupied".  But I don't care about those applications, so I've changed the
check in `input.rs` to simply look for `this.ctx.modifiers().alt()` instead
of `ctrl`.

[#981]: https://github.com/jwilm/alacritty/pull/981
[#2552]: https://github.com/jwilm/alacritty/pull/2552
