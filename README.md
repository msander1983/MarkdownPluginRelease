# The Markdown Plugin II for MadCap Flare

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
* Sync all topics and snippets in your Flare project to Markdown.

### Refresh from Markdown
* Overwrite the content of the current topic with the converted content from its corresponding Markdown file.
* Refresh all topics and snippets in a folder from the corresponding Markdown files. 
* Refresh all topics and snippets in your Flare project from Markdown.

**NOTE:** If a topic is called `Topic.htm`, the corresponding Markdown file would be `Topic.md`, and for a snippet called `Snippet.flsnp`, the corresponding Markdown files is `Snippet.flsnp.md`.

### Settings

The settings for converting Markdown to Flare topics are set in a file called `MarkdownSettings.xml`, which is placed either in your Flare project, or in your application data folder in Windows. If a Flare project has a settings file - that file takes precedence over the settings file in the application data folder. 

```xml
<?xml version="1.0" encoding="utf-8" standalone="yes"?>
<Settings>
  <HeaderlessTables>true</HeaderlessTables>
  <ComplexTables>false</ComplexTables>
  <RemoveAttributesOnExport>false</RemoveAttributesOnExport>
  <ConvertXrefs>false</ConvertXrefs>
  <ConvertLocalLinksToXref>false</ConvertLocalLinksToXref>
  <ExportYaml>false</ExportYaml>
</Settings>
```

These are the settings you can make: 
| Settings | Comment | 
| --- | --- | 
HeaderlessTables | If **true** (default) - Markdown tables without headers are converted to headerless tables. If **false** - tables are converted with headers, even if the Markdown tables don't have headers. |
ComplexTables | If **true** - adjacent empty table cells to the right are merged with the previous cell. The default setting is **false**|
RemoveAttributesOnExport |  If set to **true** the HTML file is exported to Markdown without attributes.  If set to **false** (default) - any HTML element with attributes is exported as HTML to the Markdown file. |
ConvertXrefs | If set to **true** any MadCap:xref elements are converted to Markdown as regular hyperlinks. 
ConvertLocalLinksToXref | If set to **true** any local links are converted to MadCap:xref when converting from Markdown to Flare.
ExportYaml | If set to **true** meta-data and conditions, condition tag expressions, and file tags are exported from your Flare topics and snippets to YAML in the Markdown file. 

### YAML meta data
If a Markdown file contains YAML dat, the YAML tags are converted to meta-tags in Flare. 
* There are a few special cases that are processed differently:
  * **conditions** are converted to the conditions of the topic or snippet.
  * **conditionTagExpression** are converted to the snippet conditions of the topic or snippet. 
  * **fileTags** are converted to file tags for the topic or snippet.

For example,

```yaml
description: Lorem ipsum dolor
keywords: lorem, ipsum, dolor
category: lorem
```
is imported into Flare as 

```html
<meta name="description" content="Lorem ipsum dolor" />
<meta name="keywords" content="lorem, ipsum, dolor" />
<meta name="category" content="lorem" />
```

and this YAML code

```yaml
---
conditions: Default.Mobile,Default.Tablet
conditionTagExpression: include[Default.Mobile], exclude[Default.Tablet]
fileTags: Author.Author1,Author.Author2
---
```

is imported as 

```html
<html xmlns:MadCap="http://www.madcapsoftware.com/Schemas/MadCap.xsd" MadCap:conditions="Default.Mobile,Default.Tablet" 
      MadCap:conditionTagExpression="include[Default.Mobile], exclude[Default.Tablet]" 
      MadCap:snippetVariables="General.VersionNumber:1231231223," MadCap:fileTags="Author.Author1,Author.Author2">
```

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
