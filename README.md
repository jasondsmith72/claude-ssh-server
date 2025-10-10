# Claude SSH Server

**Direct SSH connections with IP/username/password - no config required!**

This MCP server enables Claude to connect to any SSH server on-demand using just IP address, username, and password. No SSH config files needed!

## 🚀 Key Feature

Unlike traditional SSH MCP servers that require pre-configured hosts in `~/.ssh/config`, Claude SSH Server supports **ad-hoc connections** with credentials passed directly in each request.

## 📦 Installation

### NPM Global Install
```bash
npm install -g claude-ssh-server
```

### Local Install
```bash
cd claude-ssh-server
npm install
npm run build
```

## 🔧 Configuration

### Claude Desktop

Add to your `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "claude-ssh": {
      "command": "npx",
      "args": [
        "-y",
        "claude-ssh-server"
      ]
    }
  }
}
```

## 🎯 Usage

### Direct Connection (New!)

Connect to any SSH server without pre-configuration:

```typescript
{
  "tool": "direct_exec",
  "host": "10.100.100.53",
  "username": "mtusa",
  "password": "your-password",
  "command": "ls -la",
  "port": 22,  // optional, defaults to 22
  "timeout": 60000  // optional, defaults to 60000ms
}
```

### Traditional CLI Mode

You can still use the traditional mode with CLI arguments:

```bash
claude-ssh-server --host=10.100.100.53 --user=mtusa --password=mypass
```

Then use the `exec` tool (credentials from CLI args).

## 🛠️ Available Tools

### `direct_exec` (Recommended)
Execute commands with credentials provided per-request:
- **host**: SSH server IP or hostname
- **username**: SSH username  
- **password**: SSH password (optional if using privateKey)
- **privateKey**: SSH private key content (optional if using password)
- **command**: Command to execute
- **port**: SSH port (default: 22)
- **timeout**: Timeout in ms (default: 60000)

### `exec` (Legacy)
Execute commands using CLI-configured credentials:
- **command**: Command to execute

## 🔒 Security Notes

- Credentials are passed per-request and not stored
- Supports both password and private key authentication
- Connection timeout protection (default 60s)
- Command sanitization and validation
- No persistent connections or credential storage

## 📝 Examples

### Check disk space on remote server
```json
{
  "tool": "direct_exec",
  "host": "192.168.1.100",
  "username": "admin",
  "password": "secure-password",
  "command": "df -h"
}
```

### Run multiple commands
```json
{
  "tool": "direct_exec",
  "host": "server.example.com",
  "username": "devops",
  "password": "password123",
  "command": "cd /var/log && tail -n 50 syslog"
}
```

### Using SSH key
```json
{
  "tool": "direct_exec",
  "host": "prod-server",
  "username": "deploy",
  "privateKey": "-----BEGIN RSA PRIVATE KEY-----\n...",
  "command": "systemctl status nginx"
}
```

## 🤝 Credits

Forked from [tufantunc/ssh-mcp](https://github.com/tufantunc/ssh-mcp)

Modified by Jason Smith to add direct connection support for Claude Desktop integration.

## 📄 License

MIT License - see LICENSE file for details

## 🐛 Issues & Contributions

Report issues: https://github.com/jasondsmith72/claude-ssh-server/issues

Pull requests welcome!
