# Editorconfig

- [[VS Code]] extension: [EditorConfig for VS Code](https://marketplace.visualstudio.com/items?itemName=EditorConfig.EditorConfig)

## Config

`.editorconfig`

```sh
# EditorConfig helps developers define and maintain consistent
# coding styles between different editors and IDEs
# editorconfig.org

root = true

[*]

# change these settings to your own preference
indent_style = tab

# we recommend you to keep these unchanged
end_of_line = lf
charset = utf-8
trim_trailing_whitespace = true
insert_final_newline = true

# language specific commands
[*.md]
trim_trailing_whitespace = false
```
