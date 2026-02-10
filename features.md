# Textr Features (Blazor GUI)

This document lists the WinForms feature set and where it appears in the Blazor UI. The WinForms details are the source of truth for behavior.

## Core editing
- Input and Result text areas with live preview.
- Transform list with remove, clear, undo, move up/down, and edit/cancel edit.
- Apply Result (replace input with result and clear transforms).
- Auto-apply toggle.
- Copy result to clipboard.

## Find & Replace
- Find/Replace inputs with case sensitivity.
- Save edits for existing Find/Replace transforms.

## Truncate
- Truncate text input.
- From start toggle.
- Case sensitivity toggle.
- Save edits for existing Truncate transforms.

## New line after X occurrences
- Occurrence count.
- Token input.
- Before/after toggle.
- Case sensitivity toggle.

## Quick actions
- Remove new lines.
- Fix escaped newline sequences (\\n or \\r → new line).
- Remove blank lines.
- Distinct lines.
- Asterisk/paragraph replacement (* ⇄ §).
- Copy tab to clipboard.
- Math expression transform.

## Encoding and conversion
- ASCII escape ↔ Unicode (Swedish letters).
- Base64 encode/decode.
- JSON ↔ XML with PascalCase toggle.
## SQL and list macros
- List to comma-separated.
- List to quoted comma-separated.
	- [ ] Migration status: Not started
- SQL query formatter.
- SQL Values() generator.
- Add table names to SELECT.
	- [ ] Migration status: Not started

## Batch edit
- Selection mode and Format mode.
	- [ ] Migration status: Not started
- Selection view and Result output.
- Load Result as Source.
- Use as Transform (adds to transform list).
	- [ ] Migration status: Not started
- Copy batch result to clipboard.
- Optional * ⇄ § preprocessing.

	- [ ] Migration status: Not started

	- [ ] Migration status: Not started
	- **Operation**: Apply all transforms to input on change and show selection/line info in a status bar.
	- [ ] Migration status: Not started
	- **Implementation**: `BtnRemoveSelectedTransform_Click()`, `BtnClearTransforms_Click()`, `BtnUndoTransform_Click()`, `BtnMoveTransformUp_Click()`, `BtnMoveTransformDown_Click()` in [TextTransforms.cs](TextTransforms.cs#L170-L227).
- **Apply result / Auto-apply**
	- **Operation**: Replace input with result and clear transforms. Auto-apply does this on result changes.
	- **Implementation**: `ApplyEdits()`, `TxtResult_TextChanged()` in [TextTransforms.cs](TextTransforms.cs#L92-L110).
	- [ ] Migration status: Not started
- **Copy result to clipboard**
	- **Operation**: Copy result and show a short status.
	- **Implementation**: `BtnCopyToClipboard_Click()` in [TextTransforms.cs](TextTransforms.cs#L176-L205).
	- [ ] Migration status: Not started

## Find & Replace
- **Operation**: Replace text with optional case sensitivity.
	- [ ] Migration status: Not started
	- Create: `TransformFactoryService.CreateFindReplaceTransform()` and `FindReplaceTransform.Transform()` in [StringTransforms/Transforms/FindReplaceTransform.cs](StringTransforms/Transforms/FindReplaceTransform.cs).
	- Add on Enter: `TxtReplace_KeyPress()` in [TextTransforms.cs](TextTransforms.cs#L131-L141).
- **UI**: `txtFind`, `txtReplace`, `chkCaseSensitive` in [TextTransforms.Designer.cs](TextTransforms.Designer.cs).
	- [ ] Migration status: Not started

- **Operation**: Remove a prefix or suffix if it matches; optional case-insensitive compare.
- **Implementation**: `TruncateTransform.Transform()` and `TransformFactoryService.CreateTruncateTransform()` in [StringTransforms/Transforms/TruncateTransform.cs](StringTransforms/Transforms/TruncateTransform.cs) and [StringTransforms/Services/TransformFactoryService.cs](StringTransforms/Services/TransformFactoryService.cs).
- **UI**: `txtTruncate`, `chkBeforeOrAfter` (from-start), `chkCaseSensitive` in [TextTransforms.Designer.cs](TextTransforms.Designer.cs).
	- [ ] Migration status: Not started

## New line after X occurrences
- **Operation**: Insert a newline before or after every N occurrences of a token.
	- [ ] Migration status: Not started
- **Implementation**: `TransformFactoryService.CreateNewLineAfterXOccurencesOfY()` and `NewLineAfterXOccurencesOfY` transform in [StringTransforms/Services/TransformFactoryService.cs](StringTransforms/Services/TransformFactoryService.cs).
	- [ ] Migration status: Not started

- **Remove new lines**
	- **Operation**: Replace newline characters with spaces (single line).
	- **Implementation**: `TransformFactoryService.CreateRemoveNewLineTransform()` in [StringTransforms/Services/TransformFactoryService.cs](StringTransforms/Services/TransformFactoryService.cs).
	- [ ] Migration status: Not started
- **Remove blank lines**
	- **Operation**: Drop empty lines.
	- **Implementation**: `TransformFactoryService.CreateRemoveBlankLinesTransform()` in [StringTransforms/Services/TransformFactoryService.cs](StringTransforms/Services/TransformFactoryService.cs).
	- [ ] Migration status: Not started
- **Distinct**
	- **Operation**: Remove duplicates.
	- **Implementation**: `TransformFactoryService.CreateDistinctTransform()` in [StringTransforms/Services/TransformFactoryService.cs](StringTransforms/Services/TransformFactoryService.cs).
	- [ ] Migration status: Not started
	- **UI**: `btnDistinct` in [TextTransforms.Designer.cs](TextTransforms.Designer.cs).
	- [ ] Migration status: Not started
	- **UI**: `btnNewLineChars` in [TextTransforms.Designer.cs](TextTransforms.Designer.cs).
	- [ ] Migration status: Not started
	- **Operation**: Replace `*` with `§` or back.
	- **Implementation**: `BtnCopyTab_Click()` in [TextTransforms.cs](TextTransforms.cs#L424-L430).
	- **UI**: `btnCopyTab` in [TextTransforms.Designer.cs](TextTransforms.Designer.cs).

	- [ ] Migration status: Not started
## Math expressions
	- [ ] Migration status: Not started

## Encoding and conversion
- **ASCII escape ↔ Unicode (Swedish letters)**
	- **Operation**: Convert `åäöÅÄÖ` ↔ `\u00e5` etc.
	- **Implementation**: `btnAsciiTo_Click()` / `btnAsciiFrom_Click()` in [TextTransforms.cs](TextTransforms.cs#L446-L487).
	- **UI**: `btnAsciiTo`, `btnAsciiFrom` in [TextTransforms.Designer.cs](TextTransforms.Designer.cs).
- **Base64 encode/decode**
	- **Operation**: Encode to Base64 / decode from Base64.
	- **Implementation**: `btnToMd5_Click()` (encode) and `btnFromBase64_Click()` (decode) in [TextTransforms.cs](TextTransforms.cs#L562-L575).
	- **UI**: `btnToBase64`, `btnFromBase64` in [TextTransforms.Designer.cs](TextTransforms.Designer.cs).
- **JSON ↔ XML**
	- **Operation**: Convert JSON ↔ XML with optional PascalCase. JSON → XML also pre-fills Find/Replace root element name if empty.
	- **Implementation**: `btnJsonToXml_Click()`, `btnXmlToJson_Click()`, `chkXmlCasing_CheckedChanged()` in [TextTransforms.cs](TextTransforms.cs#L542-L561).
	- **UI**: `btnJsonToXml`, `btnXmlToJson`, `chkXmlCasing` in [TextTransforms.Designer.cs](TextTransforms.Designer.cs).

## SQL and list macros
- **Operation**: Macro buttons enqueue multiple transforms in order.
- **Implementation**: `MacroFactoryService` methods and `SqlMacros` in [StringTransforms/Macros/SqlMacros.cs](StringTransforms/Macros/SqlMacros.cs).
- **UI**: `btnMacroListComma`, `btnMacroListStringComma`, `btnMacroSqlSelectFormatter`, `btnMacroSqlQuery`, `btnMacroSqlValues`, `btnAddTableNames`, `btnGremlin` in [TextTransforms.Designer.cs](TextTransforms.Designer.cs).

## Transform editing (edit/cancel)
- **Operation**: Edit existing Find/Replace or Truncate transforms from the list.
- **Implementation**: `EditableTransform`, `EditEventService`, `FindReplaceEdit`, `TruncateEdit` in [StringTransforms/EditableTransform.cs](StringTransforms/EditableTransform.cs) and [StringTransforms/Services/EditEventService.cs](StringTransforms/Services/EditEventService.cs); UI wiring in [TextTransforms.cs](TextTransforms.cs#L312-L396).
- **UI**: `btnEditSelectedTransform`, `lstTransforms`, `txtInfo` in [TextTransforms.Designer.cs](TextTransforms.Designer.cs).

## Batch edit (separate form)
- **Operation**: Match/transform each line using wildcard selections or format templates; supports two modes.
- **Implementation**: `BatchEdit` form and `GroupTransform`/`FormatTransform` in [BatchEdit.cs](BatchEdit.cs) and [StringTransforms/BatchTransforms/GroupTransform.cs](StringTransforms/BatchTransforms/GroupTransform.cs).
- **UI inputs**: `txtSource`, `txtSelection`, `txtTransform`, `txtSelectionView`, `txtResult`, `rdoSelection`, `rdoFormat`, `chkChangeAsteriskIntoParagraph`, `btnUseAsTransform`, `btnCopyToClipboard`, `btnReInit` in [BatchEdit.Designer.cs](BatchEdit.Designer.cs).
- **Cosmos replace helpers**:
	- **Operation**: Build multiple Find/Replace transforms from lines in the form `text,value`, with a template containing a single `*`.
	- **Implementation**: `btnReplace_Click()` and `btnCosmosFromVs_Click()` in [BatchEdit.cs](BatchEdit.cs#L154-L275).
	- **UI**: `btnReplace`, `txtCosmos`, `lblCosmosHint`, `btnCosmosFromVs` in [BatchEdit.Designer.cs](BatchEdit.Designer.cs).

## Jira helper (separate app)
- **Operation**: Build Jira attachment, image, and link markup; rich-text shortcuts (bold/italics/underline/strike/noformat/color); directory file listing to clipboard.
- **Implementation**: `JiraHelperForm` in [JiraHelper/JiraHelper.cs](JiraHelper/JiraHelper.cs).
- **UI**: `rdoImage`, `rdoAttachedFile`, `rdoLink`, `txtImage`, `txtMultiImage`, `txtLinkText`, `txtFileNames`, `txtRichEditor` in [JiraHelper/JiraHelper.Designer.cs](JiraHelper/JiraHelper.Designer.cs).
