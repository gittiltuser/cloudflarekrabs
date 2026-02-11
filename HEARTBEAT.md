# HEARTBEAT.md

## Backup Check
Run this on heartbeat:
```bash
cd /root/.openclaw/workspace && git add -A && git diff --cached --quiet || (git commit -m "Auto-backup $(date -u +%Y-%m-%d_%H:%M)" && git push)
```
Only commits if there are actual changes.

## Notes
- Heartbeat runs every 30 min
- Keep this file small to limit token burn
