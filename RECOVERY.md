# RECOVERY.md - How to Restore Cloudflare Krabs 🦀

If the Cloudflare container gets wiped, here's how to get me back.

## Step 1: Access Your Cloudflare Container

**Via Cloudflare Dashboard:**
1. Go to your Cloudflare Workers & Pages dashboard
2. Find your OpenClaw deployment
3. Access the container terminal/shell
4. You should be in `/root` or similar

**Via wrangler CLI** (if you have it):
```bash
wrangler dev --compatibility-date=2024-01-01
# or whatever your specific deployment command is
```

**Via SSH** (if configured):
```bash
ssh root@your-container-ip
```

## Step 2: Install OpenClaw (Fresh Container)

```bash
# Update package manager
apt update

# Install Node.js (if not present)
curl -fsSL https://deb.nodesource.com/setup_lts.x | bash -
apt-get install -y nodejs

# Install OpenClaw globally
npm install -g openclaw

# Verify install
openclaw --version
```

## Step 3: Initialize Gateway

```bash
# Start gateway (creates directory structure)
openclaw gateway start

# This creates /root/.openclaw/workspace and other directories
```

## Step 4: Restore My Configuration

```bash
# Go to workspace
cd /root/.openclaw/workspace

# Clone backup repo (use the GitHub token from your secure notes)
git clone https://YOUR_GITHUB_TOKEN@github.com/gittiltuser/cloudflarekrabs.git temp_restore

# Copy all config files
cp temp_restore/* . 2>/dev/null || true
cp -r temp_restore/memory . 2>/dev/null || true

# Clean up
rm -rf temp_restore

# Verify files are there
ls -la
ls memory/
```

## Step 5: Reconfigure API Keys

```bash
# Set environment variables or use openclaw config
export ANTHROPIC_API_KEY="your-anthropic-key"
export NVIDIA_API_KEY="your-nvidia-key" 
export GROQ_API_KEY="your-groq-key"

# Or add via config (check openclaw config --help)
```

## Step 6: Telegram Setup

```bash
# Pair with Telegram
openclaw telegram pair

# Follow the prompts to set bot token and pair with your account
```

## Step 7: Restart Gateway

```bash
# Restart to pick up all changes
openclaw gateway restart

# Check status
openclaw status
```

## Step 8: Test Connection

Send a message to the Telegram bot to verify I'm back online as Cloudflare Krabs 🦀

## What Gets Restored

✅ **My personality** (SOUL.md)  
✅ **Your info** (USER.md)  
✅ **My identity** (IDENTITY.md)  
✅ **Operating instructions** (AGENTS.md)  
✅ **Local notes** (TOOLS.md)  
✅ **Task configs** (HEARTBEAT.md)  
✅ **Memory files** (memory/)  

## What Needs Manual Setup

❌ **API keys** (security - not stored in git)  
❌ **Telegram pairing** (security - not stored in git)  
❌ **Container access** (platform-specific)  

## Emergency Contact

If you can't reach the container at all:
- Check Cloudflare Workers dashboard
- Look for deployment logs/errors
- Might need to redeploy the whole thing

## Backup Location

**GitHub:** https://github.com/gittiltuser/cloudflarekrabs  
**Token:** Check your secure notes for the GitHub personal access token

---

*This file gets backed up too, so you'll always have these instructions! 🦀*