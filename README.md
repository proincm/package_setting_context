# PluginSettingContext

This "package" is a dependency for *your* package(s). It allows your users to enable/disable a key
binding by simply changing your package's settings. And all it requires you to do is to add:

```json
"context": [
    { "key": "plugin_setting.YourPackage.setting_to_enable_this_key_binding" }
]
```

That's it!

## Overview

A `YourPackage.sublime-settings` file:

```json
{
    "enabled_shortcut_my_super_command": true
}
```

```json
[
    {
        "keys": ["ctrl+l"],
        "command": "my_super_command",
        "context": [
            { "key": "plugin_setting.YourPackage.enabled_shortcut_my_super_command" }
        ]
    }
]
```

And this shortcut will work. But if you set `YourPackage.sublime-settings`'s content to:

```json
{
    "enabled_shortcut_my_super_command": false
}
```

You guessed it: this key binding wouldn't work any more. Pretty handy, right?

## Further infos

In the overview's example, the `operator: equal` and `operand: true` is implicit, but you can of
course change it:

```json
[
    {
        "keys": ["ctrl+l"],
        "command": "my_super_command",
        "context": [
            { "key": "plugin_setting.YourPackage.enabled_shortcut_my_super_command",
              "operand": "not_equal",
              "operator": "a string for example!"}
        ]
    }
]
```

The `key` is quiet clever too. Have a look:

In `Hello.sublime-settings`:

```json
{
    "my_setting": {
        "my_key": ["my", "list", {
            "and": "it goes on and",
            "on": true
        }]
    }
}
```

And your key binding:

```json
[
    {
        "keys": ["ctrl+l"],
        "command": "my_super_command",
        "context": [
            { "key": "plugin_setting.Hello.my_setting.my_key.2.on"}
        ]
    }
]
```

And it works!
