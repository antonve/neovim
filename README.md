# Neovim config

My reusable Neovim configuration. It uses Lua throughout, bootstraps
[lazy.nvim](https://github.com/folke/lazy.nvim), and keeps plugin versions
pinned in `lazy-lock.json`.

## Install

Requirements:

- Neovim 0.11 or newer
- Git
- A C compiler for Tree-sitter parsers
- `rg` and `fd` for project search
- Any language servers you want to use; the config enables `gopls`, `ts_ls`,
  `terraformls`, `lua_ls`, and `nil_ls`

Clone the repository into Neovim's config directory:

```sh
git clone https://github.com/antonve/neovim.git "${XDG_CONFIG_HOME:-$HOME/.config}/nvim"
```

Back up or remove an existing config directory first. Start `nvim` after
cloning; lazy.nvim installs itself and the configured plugins automatically.
To install exactly the versions in the lockfile from a headless shell, run:

```sh
nvim --headless '+Lazy! restore' +qa
```

The accompanying
[`antonve/agent-dotfiles`](https://github.com/antonve/agent-dotfiles) setup
clones this repository to `~/xdev/personal/neovim` and links that directory to
`~/.config/nvim`.

## What is configured

- Kanagawa colorscheme, relative line numbers, persistent undo, visible
  whitespace, and an OSC 52 clipboard suitable for remote terminals
- LSP navigation, rename, code actions, formatting, and completion through
  `nvim-lspconfig` and `blink.cmp`
- Tree-sitter highlighting and indentation for Go, TypeScript, Terraform,
  Lua, Nix, shell, common data formats, and Markdown
- Git integration with Fugitive and Gitsigns
- Project navigation with fzf-lua and Oil
- Comment, surround, and Flash editing motions
- Go run, test, build, formatting, import organization, and alternate-file
  commands

## Keybindings

The leader key is comma.

| Binding | Action |
|---|---|
| `<leader>ff` | Find Git-tracked files, or all files outside a Git repository |
| `<leader>fi` | Find files |
| `<leader>fh` | Open file history |
| `<leader>fb` | Switch buffers |
| `<leader>fl` | Search lines in the current buffer |
| `<leader>fr` | Live grep |
| `<leader>fg` | Grep the project |
| `<leader>e` | Open Oil's file browser |
| `s` | Flash jump |
| `gd` / `gh` | Go to definition / show hover information |
| `gt` / `gi` / `gR` | Type definition / implementation / references |
| `gr` / `gq` | Rename / code action |
| `<leader>c<Space>` | Toggle a comment |

In Go buffers, `<leader>r`, `<leader>t`, and `<leader>b` run, test, and build.
`:A`, `:AV`, `:AS`, and `:AT` open the alternate source or test file in the
current window, a vertical split, a horizontal split, or a new tab.

The config intentionally disables arrow keys and remaps `j` and `k` to move
by display lines. Delete and change operations avoid overwriting the yank
register.

## Layout

```text
init.lua                Entry point
lazy-lock.json          Pinned plugin revisions
lua/vim_config.lua      Core Neovim options and autocommands
lua/keys.lua            General keybindings
lua/go.lua              Go-specific commands and keybindings
lua/plugin.lua          lazy.nvim bootstrap
lua/plugins/            Plugin specifications
```

## Updating

Pull configuration changes and update plugins with:

```sh
git pull --ff-only
nvim --headless '+Lazy! sync' +qa
```

Review and commit any resulting `lazy-lock.json` change so installations stay
reproducible.
