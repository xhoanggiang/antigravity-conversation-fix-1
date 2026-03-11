# Antigravity Conversation Fix

Your Antigravity conversation history disappeared? Conversations showing in the wrong order? Titles replaced with placeholder text? This tool fixes all of that.

## ⚡ Quick Start (Windows)

1. Download **`Antigravity_Conversation_Fix.exe`** from the Releases Page
2. Double-click it — a terminal window will open
3. If Antigravity is still running, the tool will warn you and ask you to close it first
4. The tool scans your conversations, rebuilds the index, and shows you the results
5. Restart your PC, then open Antigravity — your conversations are back, sorted by date

> **No Python or developer tools required.** Just download, run, done.

## What It Fixes

| Problem | Fixed? |
|---|---|
| Conversations missing from sidebar | ✅ |
| Conversations in wrong order | ✅ Sorted newest first |
| Placeholder titles instead of real names | ✅ Restores from brain artifacts |
| Titles lost after previous fix attempts | ✅ Preserves existing titles |

## How It Works

Antigravity stores conversation data in two places:

- **Conversation files** (`*.pb`) in `%USERPROFILE%\.gemini\antigravity\conversations\`
- **Sidebar index** in a SQLite database at `%APPDATA%\antigravity\User\globalStorage\state.vscdb`

When the index gets corrupted, conversations still exist on disk but don't show up in the sidebar. This tool scans your conversation files, sorts them by date, pulls titles from brain artifacts, and writes a clean index back to the database.

**Title resolution priority:**
1. Brain artifact `.md` headings (best source)
2. Titles already in the database (preserved across re-runs)
3. Fallback: `Conversation (date) short-id`

## Output Legend

| Marker | Meaning |
|---|---|
| `[+]` | Title extracted from brain artifact |
| `[~]` | Title preserved from existing database |
| `[?]` | Fallback title (no source available) |

## Advanced: Run from Source

If you prefer running the Python script directly (or you're on Mac/Linux):

```bash
python rebuild_conversations.py
```

Requires Python 3.7+ with no external packages.

## Safety

- **Automatic backup** — your current index is saved to `trajectorySummaries_backup.txt` before any changes
- **Non-destructive** — conversation files (`*.pb`) are never modified, only the sidebar index is rebuilt
- **Idempotent** — safe to run multiple times

## FAQ

**Q: Do I really need to restart my PC?**
A: A full restart is the safest way to ensure Antigravity picks up the changes. In most cases, simply closing and reopening Antigravity works too.

**Q: Why do some titles show as "Conversation (Mar 10) abc12345"?**
A: Those conversations don't have brain artifacts, and their original titles weren't in the database. Future re-runs will preserve any titles the app generates going forward.

**Q: Can I run this while Antigravity is open?**
A: The tool will detect if Antigravity is running and warn you. It's recommended to close it first so the app doesn't overwrite your fix when it exits.

## License

MIT — free to use, share, and modify.

---

**⭐ If this fixed your conversations, please star the repo so others can find it!**
