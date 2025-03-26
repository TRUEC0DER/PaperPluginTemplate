## Paper Plugin Template

This repository provides a template for creating Minecraft plugins for the **Paper** server. It is pre-configured to use **enhanced hot code swapping** with **JBR (JetBrains Runtime)**, allowing you to modify your plugin’s code without needing to restart the server.

### Features:
- **Enhanced HotSwap**: Hot code swapping with JBR, enabling rapid testing of code changes without restarting the server.
- **Gradle Build System**: Built with Gradle for easy dependency management and plugin building.
- **Test Server**: Includes a built-in mechanism for launching a test server to run your plugin and test changes immediately.
- **Plugin Configuration**: Configure plugin settings via `plugin.json` (e.g., Java version, Paper server version, Modrinth publishing options).
- **Lombok Support**: Integrated Lombok for reducing boilerplate code and simplifying development.

### Example Configuration (plugin.json):
```json5
{
  "java": {
    "version": 21, // Target java version
    "allow_enhanced_hotswap": true // Enable hot code swapping without restart
  },
  "plugin": {
    "name": "PaperPluginTemplate", // Plugin name, that shows in /plugins and JAR filename
    "version": "1.0.0", // Plugin version, that shows in /plugins and JAR filename
    "api_version": "1.21" // Minimal required server version
  },
  "paper": {
    "server_version": "1.21.4", // Version of run server
    "paper_version": "1.21.4-R0.1-SNAPSHOT", // Version of Paper API
  },
  "modrinth": { // Modrinth publishing options. You need to set MODRINTH_TOKEN environment variable to publish
    "project_id": "paper-plugin-template", // Can be the project ID or the slug
    "version_number": "1.0.0", // Will fail if Modrinth has this version already
    "version_type": "release", // Can be `release`, `beta`, `alpha`
    "upload_file": "jar", // File type to upload
    "game_versions": [ // Must be an array, even with only one version
      "1.21.4"
    ],
    "loaders": [ // Must also be an array
      "paper"
    ],
    "dependencies": { // A special DSL for creating dependencies
      // scope.type
      // The scope can be `required`, `optional`, `incompatible`, or `embedded`
      // The type can either be `project` or `version`
      "optional": [
        {"type": "version", "name": "trueportals", "version": "1.3.1"} // Optional dependency on truePortals version 1.3.1
      ],
      "required": [
        {"type": "project", "name": "mwl"} // Required dependency on mWL project
      ],
      "incompatible": [
        {"type": "version", "name": "trueportals", "version":  "1.1.0"} // Incompatible version of truePortals
      ],
      "embedded": [
        {"type": "project", "name":  "mwl"} // Embedded dependency on mWL project
      ]
    }
  }
}
```

### Features Breakdown:
- **Java Version**: Supports Java 21 by default, but you can modify it in `plugin.json` for other versions.
- **Modrinth Publishing**: Easily configure and publish to **Modrinth** with options to specify the project ID, version, and dependencies.
- **Paper Server**: Pre-configured for **Paper** with automatic updates and version management.

This template is ideal for developers looking to quickly create and test Paper plugins with modern Java features and efficient hot-reloading.