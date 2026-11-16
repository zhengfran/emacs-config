# Emacs configuration

Modular Emacs configuration, snippets and supporting scripts, extracted from
[zhengfran/dotconfig](https://github.com/zhengfran/dotconfig) with their Git history.

## Start

```bash
git clone https://github.com/zhengfran/emacs-config.git ~/emacs-config
emacs --init-directory ~/emacs-config/modular/
```

When used as the dotconfig submodule, the checkout stays at
`~/dotconfig/basic/editor/emacs`. Dotconfig's `scripts/setup-config.sh` links
`modular/` to `~/.config/emacs`; existing configuration paths remain unchanged.
The setup script may replace live files after prompting: review before running.

## Contents

- `modular/`: initialization, feature modules, architecture notes and ERT tests.
- `snippets/`: checked-in snippet templates. The active snippet store is configured
  separately in `modular/modules/snippets.el` (currently `~/org/snippets`).
- `scripts/`: Emacs client launchers for shell/PowerShell, the source-build script,
  font installer and launcher usage documentation in `scripts/README.md`.
- `CLAUDE.md`: module architecture and editing/validation conventions; read before
  changing Emacs Lisp. `AGENTS.md` links to the same instructions.

The configuration remains personal: Org paths, fonts and external tools may need
local adjustment. Rime data is shared with dotconfig at `~/dotconfig/Rime` and is
not bundled here. PowerShell launchers still contain legacy machine-specific
client/auth paths; inspect them before use on another machine.

## Scripts and tests

```bash
# Help only; an actual build installs dependencies and writes outside this repo.
bash scripts/build-emacs.sh --help

# Full initialization and project-tracking ERT suite (requires Emacs and packages).
emacs --batch --init-directory "$PWD/modular/" -l init.el
bash modular/tests/run-tests.sh
```

The font installer also installs system packages and writes to the user font
directory. Standalone Emacs startup does not run it; dotconfig's full
`scripts/setup.sh` does invoke it through the compatibility link.

Dotconfig retains compatibility links at `scripts/emacs/`,
`scripts/build-emacs.sh` and `scripts/setup-fonts.sh`, so existing shell aliases
and launcher commands continue to reach these scripts. On Windows, these Git
symlinks require symlink support (`core.symlinks=true` and Developer Mode or
administrator privileges); otherwise use the canonical submodule paths.

## Development in dotconfig

Commit and push changes in this repository first. Then stage and commit the
`basic/editor/emacs` gitlink in dotconfig. Check `git submodule status` before
updating submodules: `git submodule update` checks out the commit recorded by the
parent, not necessarily the latest `main`.

History includes the former `emacs/` and `.doom.d/` locations, the later
`basic/editor/emacs/` configuration, and Emacs-specific scripts. Paths are mapped
into this standalone layout; empty unrelated commits are pruned. Dotconfig's
history is unchanged.
