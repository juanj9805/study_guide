# Windows Clipboard History

## How to Enable
Settings > System > Clipboard > Clipboard history > On

## How to Use

| Shortcut | Action |
|---|---|
| `Ctrl+C` | Copy (adds to history) |
| `Ctrl+V` | Paste most recent item |
| `Win+V` | Open clipboard history panel — pick any previous item |

## Why It Matters

Without clipboard history, `Ctrl+C` **replaces** what you had. With it, `Ctrl+C` **adds** to a list of ~25 items.

## Developer Scenarios

- **Debugging**: copy 3 different error messages from the console, then paste them one by one where you need them
- **Environment variables**: copy key from docs, copy value from another source, paste both without switching back and forth
- **Writing code**: paste a route, a DTO property name, and a connection string — all copied from different files, no back-and-forth
- **Accidental overwrite**: you copy a Stack Overflow solution, then copy something else by accident — it's still in the history via `Win+V`

## Tips

- **Pin items**: in the `Win+V` panel, pin values you use often (like localhost URLs, test credentials, SQL queries)
- **Clear history**: click the "Clear all" button in the panel, or go to Settings > System > Clipboard > Clear
- **Synced across devices**: if you enable "Sync across devices" in the same settings page, clipboard items are available on all your Windows devices signed into the same Microsoft account



● Yes, but Linux doesn't have it built-in like Windows — you need a third-party clipboard manager. The options depend on your
  desktop environment:

  GNOME (Ubuntu default)

  - CopyQ — most popular, works on any DE
  sudo apt install copyq
  - GNOME Clipboard History — extension from extensions.gnome.org, integrates into the top bar

  KDE Plasma

  - Klipper — comes pre-installed, already works out of the box with Ctrl+Alt+V (same concept as Win+V)

  Any DE / Minimal setups

  - CopyQ — the universal choice
  - Clipman (XFCE)
  - Parcellite — lightweight, good for older machines

  For your WSL Ubuntu specifically

  WSL doesn't have a desktop, so clipboard managers don't apply directly. WSL shares the Windows clipboard — when you copy in WSL
  with xclip or xsel, it goes to Windows clipboard. So your Windows Win+V already covers WSL.

  If you're working on a full Linux machine (not WSL), CopyQ is the answer:
  sudo apt install copyq
  # Then add it to startup applications
  # Default shortcut: Ctrl+Alt+H to open history

  Bottom line: Windows has the best built-in implementation. On Linux, install CopyQ and you get the same experience. On your WSL
  setup, you already have it through Windows — no extra setup needed.
