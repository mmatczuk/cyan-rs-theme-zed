# Cyan Light and Dark for Zed

Cyan Light brings the JetBrains palette and RustRover's Rust highlighting to Zed. Cyan Dark uses the same syntax color roles on cool charcoal surfaces.

## Install

This is a dev-only extension. Clone this repository, run `zed: install dev extension`, and select the `cyan-rs-theme-zed` checkout folder.

Set `theme` in `settings.json` to follow your system appearance.

```json
"theme": {
  "mode": "system",
  "light": "Cyan Light",
  "dark": "Cyan Dark"
}
```

## Matching RustRover

The light palette comes from the JetBrains theme, its parent `Default` scheme and RustRover's Rust defaults.
Some Rust highlighting depends on rust-analyzer token modifiers, which a theme can't select.
To match RustRover, add these to `settings.json` (with `"semantic_tokens": "combined"` or `"full"`):

```jsonc
"global_lsp_settings": {
  "semantic_token_rules": [
    // Primitive types and `Self` as keywords
    { "token_type": "builtinType", "style": ["type.builtin"] },
    { "token_type": "selfTypeKeyword", "style": ["keyword"] },
    // Crate names, trait methods (italic), statics, macro `!`, `#[...]`, `?`
    { "token_type": "namespace", "token_modifiers": ["crateRoot"], "style": ["namespace.crate"] },
    { "token_type": "method", "token_modifiers": ["trait"], "style": ["function.method.trait"] },
    { "token_type": "static", "style": ["constant.static"] },
    { "token_type": "macroBang", "style": ["function.macro"] },
    { "token_type": "attributeBracket", "style": ["attribute"] },
    { "token_type": "operator", "token_modifiers": ["controlFlow"], "style": ["operator.try"] },
    // Underlined mutable bindings
    { "token_type": "variable", "token_modifiers": ["mutable"], "underline": true },
    { "token_type": "parameter", "token_modifiers": ["mutable"], "underline": true },
    { "token_type": "selfKeyword", "token_modifiers": ["mutable"], "underline": true },
    // Unsafe operations background
    { "token_type": "function", "token_modifiers": ["unsafe"], "style": ["rust.unsafe"] },
    { "token_type": "method", "token_modifiers": ["unsafe"], "style": ["rust.unsafe"] },
    { "token_type": "operator", "token_modifiers": ["unsafe"], "style": ["rust.unsafe"] }
  ]
}
```

If you copied an earlier version of these rules, replace it with the snippet above. Mutable underlines follow the token color, and unsafe operations use the active theme's background for unsafe code.

## Preview

![Cyan Light in Zed](./assets/preview.png)

## Credits

Original IntelliJ theme by [Olga Berdnikova](https://plugins.jetbrains.com/plugin/12102-cyan-light-theme).

The discussion with the maintainer of the general-purpose Zed port explains the focus on Rust. [Cyan Light Theme issue #4](https://github.com/bIaqat/cyan-light-theme-zed/issues/4)

## License

[MIT](LICENSE)
