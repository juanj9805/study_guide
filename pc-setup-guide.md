# Dev Workstation Setup Guide

**Date**: April 9, 2026
**Machine**: Windows 11 Pro | AMD Ryzen 5 3600 | 24GB RAM

---

## What Was Changed

### VS Code Extensions Installed

| Extension | Purpose |
|---|---|
| ms-dotnettools.csharp | C# IntelliSense, refactoring, debugging |
| ms-dotnettools.csdevkit | Solution Explorer, test runner, project management |
| ms-dotnettools.vscode-dotnet-runtime | .NET runtime acquisition for extensions |
| humao.rest-client | Test APIs with `.http` files directly in VS Code |
| mtxr.sqltools | Database explorer inside VS Code |
| mtxr.sqltools-driver-pg | PostgreSQL driver for SQLTools |
| mtxr.sqltools-driver-mssql | SQL Server driver for SQLTools |

### .NET Global Tools Installed

| Tool | Command | Purpose |
|---|---|---|
| dotnet-ef 10.0.5 | `dotnet ef` | EF Core migrations and database commands |
| dotnet-outdated 4.7.1 | `dotnet outdated` | Check for outdated NuGet packages |

### Git Configuration

**Settings added:**
- Default editor: VS Code
- Default branch: `main`
- Line endings: `core.autocrlf = true`
- Global gitignore: `~/.gitignore_global`

**Aliases:**

| Alias | Command | Usage |
|---|---|---|
| `git st` | `git status -sb` | Short status with branch |
| `git lg` | `git log --oneline --graph --decorate --all` | Visual branch graph |
| `git last` | `git log -1 HEAD --stat` | Last commit with file stats |
| `git undo` | `git reset HEAD~1 --mixed` | Undo last commit, keep changes |
| `git unstage` | `git reset HEAD --` | Unstage all files |
| `git save` | `git stash push -m` | Stash with a message |
| `git pop` | `git stash pop` | Pop last stash |

### Files Created

#### `~/.gitignore_global`
Ignores globally: `.vs/`, `.idea/`, `bin/`, `obj/`, `node_modules/`, `.env`, `*.log`, OS junk files.

#### `~/.wslconfig`
```ini
[wsl2]
memory=8GB
processors=4
swap=2GB
localhostForwarding=true

[experimental]
autoMemoryReclaim=gradual
```
Caps WSL at 8GB RAM and 4 cores so it doesn't starve Windows processes.

#### `~/.bashrc`
Git Bash prompt showing current branch + aliases:

| Alias | Command |
|---|---|
| `gs` | `git status -sb` |
| `ga` | `git add` |
| `gc` | `git commit -m` |
| `gp` | `git push` |
| `gl` | `git pull` |
| `gco` | `git checkout` |
| `gcb` | `git checkout -b` |
| `glg` | `git log --oneline --graph --decorate --all` |
| `gundo` | `git reset HEAD~1 --mixed` |
| `dr` | `dotnet run` |
| `db` | `dotnet build` |
| `dt` | `dotnet test` |
| `dw` | `dotnet watch run` |
| `dpg` | `docker start pg-dev` |
| `dpgstop` | `docker stop pg-dev` |

### VS Code Settings Updated

File: `AppData\Roaming\Code\User\settings.json`

- C# formatter set for `.cs` files (tab size 4)
- Auto-import from unimported namespaces enabled
- Parameter inlay hints enabled
- Bracket pair colorization and guides enabled
- Sticky scroll enabled
- Trailing whitespace trimmed on save
- Final newline inserted on save
- Git autofetch enabled
- **`bin/`, `obj/`, `node_modules/`** excluded from file watcher and search (prevents VS Code lag during builds)

### Manual Changes Applied

- **Power plan**: switched to High Performance
- **Windows Defender**: excluded `~/dev`, `dotnet.exe`, `node.exe`, `rider64.exe` from scanning
- **Startup programs disabled**: Docker Desktop, UrbanVPN, Opera GX, Adobe Acrobat Sync, duplicate Google Drive entries
- **File extensions**: visible in Explorer
- **WSL**: restarted to apply `.wslconfig`

---

## Not Installed (Skipped)

- **PowerToys** — window management, app launcher, file locksmith
- **Oh-My-Posh** — PowerShell prompt with .NET SDK version and git branch

Both can be installed later with:
```
winget install Microsoft.PowerToys
winget install JanDeLaaj.oh-my-posh
```

---

## IDE Strategy

| IDE | Use For |
|---|---|
| JetBrains Rider | Primary IDE for `.sln`/`.csproj` C# projects |
| VS Code | React, TypeScript, quick edits, config files, REST Client |
| Visual Studio 2026 | When Rider doesn't cover a specific .NET feature |

Avoid running Rider + VS Code simultaneously unless necessary (Rider uses ~1.4GB RAM).

---

## PostgreSQL via Docker (Ready to Use)

When you need PostgreSQL:
```bash
# First time only (pull image + create container):
docker pull postgres:16
docker run --name pg-dev -e POSTGRES_PASSWORD=devpassword -e POSTGRES_USER=devuser -p 5432:5432 -d postgres:16

# After that, start/stop with:
docker start pg-dev
docker stop pg-dev

# Or use the bash aliases:
dpg       # start
dpgstop   # stop
```

Connect with DBeaver: `localhost:5432`, user=`devuser`, password=`devpassword`
