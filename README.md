# consult-vulpea

[![MELPA](https://melpa.org/packages/consult-vulpea-badge.svg)](https://melpa.org/#/consult-vulpea)

Use [Consult](https://github.com/minad/consult) in tandem with [Vulpea](https://github.com/d12frosted/vulpea).

## Features

- **Live previews**: When selecting notes via `vulpea-find`, `vulpea-insert` and `vulpea-find-backlink`, get a live preview of the note file as you navigate through candidates. During `vulpea-find-backlink` preview, the backlinks are also highlighted and you can easily navigate between them..
- **Consult-powered grep/find**: Use `consult-vulpea-grep` and `consult-vulpea-find` to search within your vulpea directories with live previews.

## Installation

consult-vulpea is available on [MELPA](https://melpa.org/#/consult-vulpea).

```elisp
(use-package consult-vulpea
  :ensure t
  :after vulpea
  :config
  (consult-vulpea-mode 1))
```

Or install manually with `M-x package-install RET consult-vulpea RET`.

### Doom Emacs

Add to `packages.el`:

```elisp
(package! consult-vulpea)
```

Add to `config.el`:

```elisp
(use-package! consult-vulpea
  :after vulpea
  :config
  (consult-vulpea-mode 1))
```

> [!IMPORTANT]
> Do not use `:after consult` — this can prevent the package from loading properly at startup.

## Commands

| Command | Description |
|---------|-------------|
| `consult-vulpea-grep` | Search vulpea notes using ripgrep with live preview |
| `consult-vulpea-find` | Find vulpea note files with live preview |

## Customization

| Variable | Default | Description |
|----------|---------|-------------|
| `consult-vulpea-grep-command` | `consult-ripgrep` | Grep command to use (can also be `consult-grep`) |
| `consult-vulpea-find-command` | `consult-find` | Find command to use |
| `consult-vulpea-preview-key` | `consult-preview-key` | Key to trigger preview, defaults to consult's global setting |

The `consult-vulpea-preview-face` face can be customized to modify how backlinks are highlighted during preview. You can also move between different backlinks during preview with the `consult-vulpea-go-to-next-backlink-overlay`/`consult-vulpea-go-to-previous-backlink-overlay` functions. The configuration below adapts the previous use-package configuration to add keybinds for `Ctrl+<right/left>` arrow keys to these two functions.

```emacs-lisp
(use-package consult-vulpea
  :ensure t
  :after vulpea
  :config
  (consult-vulpea-mode 1)
  :bind ( :map minibuffer-local-map
          ("C-<right>" . consult-vulpea-go-to-next-backlink-overlay)
          ("C-<left>" . consult-vulpea-go-to-previous-backlink-overlay)))
```

## How it works

When `consult-vulpea-mode` is enabled, the package advises `vulpea-select-from` with a consult-powered replacement. This means all vulpea commands that use the note selection interface (like `vulpea-find`, `vulpea-insert` and `vulpea-find-backlink`) automatically gain consult features. In the case of `vulpea-find-backlink`, overlays are created in the preview buffer to highligh all backlinks.

## Requirements

- Emacs 28.1+
- [vulpea](https://github.com/d12frosted/vulpea) 2.0.0+
- [consult](https://github.com/minad/consult) 2.2+

## Related

- [consult-org-roam](https://github.com/jgru/consult-org-roam) — Similar integration for [org-roam](https://github.com/org-roam/org-roam)
- [consult-denote](https://github.com/protesilaos/consult-denote) — Similar integration for [Denote](https://github.com/protesilaos/denote)

## License

GPL-3.0
