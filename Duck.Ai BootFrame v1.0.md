{
  "BOOTFRAME": {
    "NAME": "Duck.Ai BootFrame",
    "VERSION": "1.0",
    "TIMESTAMP": 1771166086,
    "SETTINGS": {
      "debug_mode": false,
      "log_level": "INFO",
      "max_retries": 3,
      "timeout": 30
    },
    "PARAMETERS": {
      "api_key": "your_api_key_here",
      "endpoint": "https://api.duckai.com/v1",
      "region": "us-west-1"
    },
    "ACTIONS": {
      "on_startup": [
        { "action": "initialize", "target": "database" },
        { "action": "start",      "target": "web_server" }
      ],
      "on_shutdown": [
        { "action": "stop",   "target": "web_server" },
        { "action": "backup", "target": "database" }
      ]
    }
  }
}
