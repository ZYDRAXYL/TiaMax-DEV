# TiaMax-DEV

Controller repo for the TiaMax multi-repository project. It holds no
application code — only the VS Code workspace, the setup script, and the
gitignore rules that keep the 14 real repos out of this one's history.

## Layout

```
TiaMax-DEV/
├── TiaMax.code-workspace   # multi-root workspace (relative paths, safe to move)
├── scripts/setup.ps1       # clone whichever child repos are missing + npm install
├── TiaMax-APP/
├── TiaMax-SDB/
├── TiaMax-TRX/
├── TiaMax-EXE/
├── TiaMax-PWA/
├── TiaMax-PKG/
├── TiaMax-WEB/
├── TiaMax-DOCS/
├── TiaMax-PLATFORM/
├── TiaMax-LANG/
├── TiaMax-FRAMEWORK/
├── TiaMax-ENGINE/
├── TiaMax-TOOLS/
├── TiaMax-TOOLCHAIN/
```

Each `TiaMax-*` folder is its own git repository (own `.git`, own GitHub
remote under `ZYDRAXYL/`). `.gitignore` excludes them entirely from this repo.

## Chained repositories

From [`TiaMax-APP/chain/chain.json`](https://github.com/ZYDRAXYL/TiaMax-APP/blob/main/chain/chain.json):

| Repo | Role | Owns | Releases | Visibility |
|---|---|---|---|---|
| [TiaMax-APP](https://github.com/ZYDRAXYL/TiaMax-APP) | hub | `.claude/`, `chain/`, `docs/`, `process/`, `tools/` | — | private |
| [TiaMax-SDB](https://github.com/ZYDRAXYL/TiaMax-SDB) | schema | `schema/`, `supabase/`, `assets/`, `generated/` | `sdb-v*` | public |
| [TiaMax-TRX](https://github.com/ZYDRAXYL/TiaMax-TRX) | service | `netlify/`, `public/`, `netlify.toml` | — | public |
| [TiaMax-EXE](https://github.com/ZYDRAXYL/TiaMax-EXE) | app | `electron/` | `v*` | private |
| [TiaMax-PWA](https://github.com/ZYDRAXYL/TiaMax-PWA) | build | `tools/`, `shim/`, `dist/` | — | public |
| [TiaMax-PKG](https://github.com/ZYDRAXYL/TiaMax-PKG) | content | `packages/`, `index.json` | `pkg-v*` | public |
| [TiaMax-WEB](https://github.com/ZYDRAXYL/TiaMax-WEB) | site | `*.html`, `assets/` | `mirror` | public |
| [TiaMax-DOCS](https://github.com/ZYDRAXYL/TiaMax-DOCS) | docs | `compatibility-matrix.md`, `shared/`, `architecture/` | — | public |
| [TiaMax-PLATFORM](https://github.com/ZYDRAXYL/TiaMax-PLATFORM) | library | `include/zx/platform/`, `src/`, `tests/` | `v*` | public |
| [TiaMax-LANG](https://github.com/ZYDRAXYL/TiaMax-LANG) | library | `include/zx/lang/`, `src/`, `tests/` | `v*` | public |
| [TiaMax-FRAMEWORK](https://github.com/ZYDRAXYL/TiaMax-FRAMEWORK) | library | `include/zx/framework/`, `src/`, `tests/` | `v*` | public |
| [TiaMax-ENGINE](https://github.com/ZYDRAXYL/TiaMax-ENGINE) | superbuild | `superbuild/`, `include/zx/engine/`, `src/`, `tests/` | `v*` | public |
| [TiaMax-TOOLS](https://github.com/ZYDRAXYL/TiaMax-TOOLS) | tools | `src/`, `tests/` | `v*` | public |
| [TiaMax-TOOLCHAIN](https://github.com/ZYDRAXYL/TiaMax-TOOLCHAIN) | service | `src/`, `tests/` | `v*` | public |

Changes flow one way along the chain:

```
EXE    APP > SDB, TRX > EXE > PKG, WEB, PWA
PWA    APP > SDB, TRX > EXE > PWA > WEB
ENGINE APP > DOCS > PLATFORM, LANG > FRAMEWORK > ENGINE > TOOLS, TOOLCHAIN > EXE
```

## First-time setup on a new device

Prerequisites: [Git](https://git-scm.com/) with access to the `ZYDRAXYL` org (APP, EXE are private), and [Node.js LTS](https://nodejs.org/).

```powershell
git clone https://github.com/ZYDRAXYL/TiaMax-DEV.git
cd TiaMax-DEV
./scripts/setup.ps1
```

Then open `TiaMax.code-workspace` in VS Code.

> If PowerShell refuses to run the script, run it once as:
> `powershell -ExecutionPolicy Bypass -File .scriptssetup.ps1`

## License

MIT — see [LICENSE](LICENSE). Created by LDKTC.
