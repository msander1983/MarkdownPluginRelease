# The Markdown Plugin for MadCap Flare

## Release Notes 

See the [release information](https://github.com/msander1983/MarkdownPluginRelease/releases).

# Documentation

## Flare Plugin

### Import to Flare
* Import a folder with Markdown files to Flare topics.
* Import a folder with Markdown files to Flare snippets.
* Convert a Flare topics to a Flare TOC file (Experimental).

### Export to Markdown
* Export a Flare topic or snippet to a Markdown file.
* Export a folder of topics and snippets to Markdown files. 

### Synchronize to Markdown
* Convert the current topic to Markdown.
* Sync a folder of topics and snippets to Markdown.

### Refresh from Markdown
* Overwrite the content of the current topic with the converted content from its corresponding Markdown file.
* Refresh all topics and snippets in a folder from the corresponding Markdown files. 

**NOTE:** If a topic is called `Topic.htm`, the corresponding Markdown file would be `Topic.md`, and for a snippet called `Snippet.flsnp`, the corresponding Markdown files is `Snippet.flsnp.md`.

### Settings

The settings for converting Markdown to Flare topics are set in a file called `MarkdownSettings.xml`, which is placed either in your Flare project, or in your application data folder in Windows. If a Flare project has a settings file - that file takes precedence over the settings file in the application data folder. 

```xml
<?xml version="1.0" encoding="utf-8" standalone="yes"?>
<Settings>
  <HeaderlessTables>true</HeaderlessTables>
  <ComplexTables>false</ComplexTables>
</Settings>
```

These are the settings you can make: 
| Settings | Comment | 
| --- | --- | 
HeaderlessTables | If **true** (default) - Markdown tables without headers are converted to headerless tables. If **false** - tables are converted with headers, even if the Markdown tables don't have headers. |
ComplexTables | If **true** - adjacent empty table cells to the right are merged with the previous cell. The default setting is **false**|
RemoveAttributesOnExport |  If set to **true** the HTML file is exported to Markdown without attributes.  If set to **false** (default) - any HTML element with attributes is exported as HTML to the Markdown file. |

## MarkdownCommander.exe CLI

With the MarkdownCommander CLI you can import and export files using the command line. 


To import Markdown files to topics:
```
C:\>MarkdownCommander -import "C:\...\from-folder"" ""C:\...\to-folder"
C:\>MarkdownCommander -import "C:\...\from-folder\myfile.md" "C:\...\to-folder"
C:\>MarkdownCommander -import "C:\...\from-folder\myfile.md" "C:\...\to-folder\myfile.htm"
```
To export topics to Markdown files: 
```
C:\>MarkdownCommander -export "C:\...\from-folder"" ""C:\...\to-folder"
C:\>MarkdownCommander -export "C:\...\from-folder\mytopic.htm" "C:\...\to-folder"
C:\>MarkdownCommander -export "C:\...\from-folder\mytopic.htm" "C:\...\to-folder\mytopic.md"
```
| Flag | Comment | 
| --- | ---|
| /f | Force overwrite |
| /i | Include sub-folders |
| /t | Generate output to console (single file only) |
| /s | Suppress dialogs. |
| /settings:[file] | Uses a specific settings file for the Markdown import, e.g. `"/settings:C:\users\mattias\my files\mySettings.xml"` |

## Ignoring files
* To keep files from being imported, you can set up a `.markdownimportignore` file in the source folder.
* To keep files from being exported, you can set up a `.markdownexportignore` file in the source folder.

The syntax is based on wildcards, where
* `*` represents a range of wildcard characters, and 
* `?` represents a single wildcard character

To ensure that the .ignore rules are processed relative to the folder of the .ignore file the line in the ignore file must contain `\`.

### Examples
| Rule | Comment |
| --- | ---- |
| `*\Lorem.md` | Excludes the files called `Lorem.md` in any subfolder to the folder with the rule file | 
| `\Lorem.md` | Excludes the `Lorem.md` file from the folder with the rule file | 
| `*Lorem*`  |  Excludes any file with `Lorem` in its full path. | 
