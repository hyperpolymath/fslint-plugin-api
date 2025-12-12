# fslint-plugin-api

Plugin API for FSLint - trait definitions and core types for building file scanning plugins.

## Overview

This crate provides the core trait and types needed to build plugins for [FSLint](https://github.com/hyperpolymath/file-soup) (part of file-soup).

## Usage

Add to your `Cargo.toml`:

```toml
[dependencies]
fslint-plugin-api = "0.1"
```

## Creating a Plugin

```rust
use fslint_plugin_api::{Plugin, PluginContext, PluginResult, PluginMetadata, PluginError};

pub struct MyPlugin;

impl Plugin for MyPlugin {
    fn metadata() -> PluginMetadata {
        PluginMetadata {
            name: "my-plugin".into(),
            version: "0.1.0".into(),
            description: "My custom file scanner".into(),
            author: Some("Your Name".into()),
            enabled_by_default: true,
        }
    }

    fn check(&self, context: &PluginContext) -> Result<PluginResult, PluginError> {
        // Your plugin logic here
        Ok(PluginResult::active("my-plugin", "Found something"))
    }
}
```

## Types

- `Plugin` - The main trait all plugins implement
- `PluginContext` - Context passed to plugins (file path, metadata, etc.)
- `PluginResult` - Result returned by plugin checks
- `PluginStatus` - Status enum (Active, Inactive, Alert, Warning, Error, Skipped)
- `PluginMetadata` - Plugin name, version, description
- `PluginError` - Error types for plugin operations

## License

MIT OR Apache-2.0
