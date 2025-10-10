# Claude SSH Server - Installation Guide

## 🎯 Quick Setup for Claude Desktop

### 1. Install the MCP Server

```bash
npm install -g claude-ssh-server
```

### 2. Configure Claude Desktop

Open your Claude Desktop configuration file:
- **Windows**: `C:\Users\%username%\AppData\Roaming\Claude\claude_desktop_config.json`
- **macOS**: `~/Library/Application Support/Claude/claude_desktop_config.json`
- **Linux**: `~/.config/Claude/claude_desktop_config.json`

Add this configuration:

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

### 3. Restart Claude Desktop

Close and reopen Claude Desktop to load the new MCP server.

### 4. Test the Connection

Try connecting to your n8n server:

```
Can you connect to 10.100.100.53 with username mtusa and password mtusaRocks1980 and run the command "ls -la"?
```

## 🔧 Usage Examples

### Basic Command Execution
```
Connect to 192.168.1.100 with user admin and password mypass123, then run "df -h"
```

### Check Service Status
```
SSH to 10.10.10.120 as root with password securepass and check if nginx is running with "systemctl status nginx"
```

### Multiple Commands
```
Connect to server.example.com as devops (password: dev123) and run "cd /var/log && tail -n 50 syslog"
```

## 📋 Tool Parameters

When Claude uses the `direct_exec` tool, it will include:
- **host**: Your server IP or hostname
- **username**: SSH username
- **password**: SSH password (or privateKey if using key auth)
- **command**: The command to execute
- **port**: SSH port (default: 22)
- **timeout**: Timeout in milliseconds (default: 60000)

## ⚠️ Security Notes

- Credentials are passed per-request and never stored
- Each connection is temporary and closed after command execution
- Use strong passwords and consider SSH key authentication for production
- Monitor your SSH server logs for unauthorized access attempts

## 🆘 Troubleshooting

### MCP Server Not Loading
1. Check Claude Desktop logs in the same directory as config file
2. Verify npm global installation path is in your system PATH
3. Try manual installation: Clone repo and run `npm install && npm run build`

### Connection Failures
- Verify SSH is enabled on target server
- Check firewall rules allow SSH connections
- Test credentials with standard SSH client first
- Verify network connectivity to target server

### Command Timeouts
- Increase timeout parameter for long-running commands
- Break complex operations into smaller commands
- Check server resources (CPU, memory, disk)

## 📚 Additional Resources

- GitHub Repository: https://github.com/jasondsmith72/claude-ssh-server
- Report Issues: https://github.com/jasondsmith72/claude-ssh-server/issues
- Original Project: https://github.com/tufantunc/ssh-mcp

## 🎉 You're Ready!

Claude can now connect to any SSH server you specify without pre-configuration!
