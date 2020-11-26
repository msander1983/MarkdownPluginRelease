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
HeaderlessTables | If **true** - Markdown tables without headers are converted to headerless tables. If **false** - tables are converted with headers, even if the Markdown tables don't have headers. |
ComplexTables | If **true** - adjacent empty table cells to the right are merged with the previous cell. |

## MarkdownCommander.exe CLI

With the MarkdownCommander CLI you can import and export files using the command line. 


To import Markdown files to topics:
```
C:\>MarkdownCommander -export "C:\...\from-folder"" ""C:\...\to-folder"
C:\>MarkdownCommander -export "C:\...\from-folder\myfile.md" "C:\...\to-folder"
C:\>MarkdownCommander -export "C:\...\from-folder\myfile.md" "C:\...\to-folder\myfile.htm"
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
