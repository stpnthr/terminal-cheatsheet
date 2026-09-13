# LazyVim + kitty Cheatsheet

Leader key = **Space**. `<leader>x` means: press Space, release, then press `x`.

---

## Modes

| Mode | How to enter | What it's for |
|---|---|---|
| Normal | `Esc` | Moving around, running commands (default mode) |
| Insert | `i`, `a`, `o`, `O` | Typing text |
| Visual | `v` (char), `V` (line), `Ctrl+v` (block) | Selecting text |
| Command | `:` | Typing `:w`, `:q`, etc. |

---

## Movement

| Key | Action |
|---|---|
| `h j k l` | Left / down / up / right |
| `w` / `b` | Jump forward / backward one word |
| `0` / `$` | Start / end of line |
| `gg` / `G` | Top / bottom of file |
| `{` / `}` | Jump paragraph up / down |
| `Ctrl+o` / `Ctrl+i` | Back / forward through recent cursor jumps |

## Scrolling

| Key | Action |
|---|---|
| `Ctrl+d` / `Ctrl+u` | Half page down / up |
| `Ctrl+f` / `Ctrl+b` | Full page forward / back |
| `Ctrl+e` / `Ctrl+y` | Scroll view only, cursor stays put |
| Mouse/trackpad scroll | Works natively |

---

## Inserting & Editing Text

| Key | Action |
|---|---|
| `i` / `a` | Insert before / after cursor |
| `o` / `O` | New line below / above, enter Insert mode |
| `dd` | Delete (cut) current line |
| `yy` | Yank (copy) current line |
| `p` | Paste after cursor |
| `dw` | Delete a word |
| `ciw` | Change a word (delete + insert) |
| `u` / `Ctrl+r` | Undo / redo |

**Cut** isn't separate — `d` (delete) doubles as cut, since deleted text goes into a register you can `p` (paste) back.

## Change Operators (delete + insert in one move)

`c` = "change": deletes text and drops you straight into Insert mode, instead of `d` then `i` as two steps.

| Key | Action |
|---|---|
| `cw` | Change to end of word |
| `ciw` | Change inner word (works from anywhere inside it) |
| `cc` | Change whole line (keeps indentation) |
| `C` | Change to end of line |
| `ci"` / `ci'` | Change inside quotes |
| `ci(` / `ci{` / `ci[` | Change inside brackets/braces/parens |
| `cip` | Change inner paragraph |

In Visual mode, select anything and press `c` — same idea, deletes selection and enters Insert mode.

## Selecting Text (Visual mode text objects)

| Key | Selects |
|---|---|
| `ggVG` | Entire file |
| `viw` | Inner word (just the word) |
| `vaw` | A word (word + trailing space) |
| `viW` (capital) | Word including punctuation (e.g. `foo.bar` as one chunk) |
| `vip` | Current paragraph (stops at blank lines) |
| `vap` | Paragraph + surrounding blank line |
| `vit` | Inner tag — content between `<div>` and `</div>` |
| `vat` | Around tag — includes the tags themselves |
| `v3w` | 3 words forward from cursor |
| `vf>` | Up to and including next `>` character |

`i` = inner (just the content), `a` = around (content + delimiters) — this pattern applies across words, quotes, brackets, tags, paragraphs.

## Surround (wrap/change/remove quotes, brackets, tags)

Powered by `mini.surround`, built into LazyVim.

| Key | Action |
|---|---|
| `gsa` | Add a surround — select text first, then `gsa`, then the delimiter (`"`, `'`, `(`, or `t` for a tag) |
| `gsd` | Delete a surround — e.g. `gsdt` removes the enclosing tag |
| `gsr` | Replace a surround — e.g. `gsrt` prompts old tag then new tag |
| `gsf` | Find/jump to the surrounding pair |

Example: wrap `test` in `<div>` — select it (`viw`), then `gsa` → `t` → type `div` → Enter.

## Saving & Quitting

| Command | Action |
|---|---|
| `:w` | Save |
| `:q` | Quit |
| `:wq` | Save and quit |
| `<leader>w` | Quick save (LazyVim shortcut) |

---

## File Explorer (neo-tree)

| Key | Action |
|---|---|
| `<leader>e` | Toggle file tree |
| `Enter` | Open file under cursor |
| `a` | Add new file/folder |
| `d` | Delete |
| `r` | Rename |

## Finding Files & Text (Telescope)

| Key | Action |
|---|---|
| `<leader>ff` | Find files by name |
| `<leader>fg` | Live grep (search text across project) |
| `<leader>fr` | Recently opened files |

## Creating a New File

- `:e filename.ext` then `:w` — fastest, no menus
- Or via neo-tree: `<leader>e` → `a` → type name → Enter

---

## Buffers & Tabs

**Moving between open files (buffers):**

| Key | Action |
|---|---|
| `Shift+H` / `Shift+L` | Cycle buffers left/right — most reliable across LazyVim versions |
| `<leader>bn` / `<leader>bp` | Next / previous buffer (check which-key if unbound) |
| `<leader>,` | Fuzzy-find and switch buffers by name |
| Click a tab in the top buffer line | Mouse alternative |

**Closing files/tabs:**

| Key/Command | Action |
|---|---|
| `<leader>bd` | Close current buffer, keep the split/window open |
| `:bd` | Same, via command line |
| `:q` | Close current window/split |
| `:tabclose` | Close a Neovim tab opened with `:tabnew` |
| `:qa` | Quit Neovim entirely (all buffers/windows) |

**Neovim tabs** (`:tabnew` — different from buffers, rarely needed day-to-day):

| Key | Action |
|---|---|
| `gt` / `gT` | Next / previous Neovim tab |
| `2gt` | Jump to tab #2 |
| `<leader><Tab>` | Tab command group (opens which-key menu) |

---

## Emmet (HTML/CSS shortcuts)

1. Open a `.html` (or `.css`) file
2. In Insert mode, type an abbreviation: `!` for boilerplate, or e.g. `div.container>ul>li*3`
3. Press `Ctrl+y` then `,` to expand

Requires the `lang.html` extra enabled (`:LazyExtras`) and `emmet-ls` installed via `:Mason`.

---

## Plugin & LSP Management

| Command | Action |
|---|---|
| `:LazyExtras` | Enable/disable optional plugin bundles (languages, formatters, etc) |
| `:Mason` | Manage installed languages / formatters |
| `:LazyHealth` / `:checkhealth` | Diagnose config problems |
| `:Lazy` | Plugin manager UI (update, view status) |

---

## Starting a Local Dev Server

| Project type | Command |
|---|---|
| Plain HTML/CSS/JS | `npm install -g live-server` once, then `live-server` in the folder |
| 11ty | `npm run dev` (check `package.json` for the exact script name) |

---

## kitty Terminal

| Key | Action |
|---|---|
| `Cmd+T` | New tab |
| `Cmd+W` | Close tab |
| `Cmd+Shift+]` / `Cmd+Shift+[` | Next / previous tab |
| `Cmd+1`, `Cmd+2`... | Jump to tab number |
| `Ctrl+Shift+F5` | Reload kitty.conf live |
| `kitty +kitten themes` | Interactive theme picker |

Config file: `~/.config/kitty/kitty.conf`
