```bash
clang-format -style=microsoft -dump-config > .clang-format
```

## .clang-format
```bash
---
Language: Cpp
BasedOnStyle: Microsoft

# === Indentation & Alignment ===
UseTab: Never
IndentWidth: 4
TabWidth: 4
ContinuationIndentWidth: 4
AccessModifierOffset: -2
AlignAfterOpenBracket: Align
AlignOperands: Align
AlignTrailingComments: true

# === Braces & Blocks ===
BreakBeforeBraces: Attach # void func() {
BraceWrapping:
  AfterFunction: true
  AfterClass: true
  AfterStruct: true
  AfterNamespace: true
  BeforeElse: true
  BeforeCatch: true

# === Line & Spacing ===
ColumnLimit: 120
SpaceBeforeParens: ControlStatements
SpaceBeforeParensOptions:
  AfterControlStatements: true
  AfterFunctionDefinitionName: false
  AfterFunctionDeclarationName: false
PointerAlignment: Right
SpaceAfterTemplateKeyword: true
SpacesInContainerLiterals: true
SpacesInParentheses: false
SpacesInSquareBrackets: false

# === Statements & Formatting Rules ===
AllowShortFunctionsOnASingleLine: None
AllowShortIfStatementsOnASingleLine: Never
AllowShortLoopsOnASingleLine: false
AllowShortBlocksOnASingleLine: Never
AllowShortCaseLabelsOnASingleLine: false
AllowAllParametersOfDeclarationOnNextLine: true
AllowAllArgumentsOnNextLine: true

# === Includes ===
SortIncludes: CaseSensitive
IncludeBlocks: Preserve

# === Misc ===
FixNamespaceComments: true
NamespaceIndentation: None
ReflowComments: true
---

```

## .vscode/settings.json
```json
{
	// --- Standard ---
	"C_Cpp.default.cppStandard": "c++23",
	// --- CMake ---
	"cmake.useCMakePresets": "always",
	"cmake.options.statusBarVisibility": "visible",
	// --- Code Analysis ---
	"C_Cpp.codeAnalysis.clangTidy.enabled": true,
	"C_Cpp.codeAnalysis.clangTidy.path": "clang-tidy",
	"C_Cpp.codeAnalysis.clangTidy.buildPath": "${workspaceFolder}/build",
	"C_Cpp.codeAnalysis.runAutomatically": true,
	// --- Formatting ---
	"editor.formatOnSave": true,
	"editor.insertSpaces": false,
	"editor.tabSize": 4,
	"editor.detectIndentation": false,
	"clang-format.style": "file",
	// --- Include Associations (standard C++ headers) ---
	"files.associations": {
		"*.defaults": "kconfig",
		"*.h": "cpp",
		"*.hpp": "cpp",
		"*.inl": "cpp",
		"chrono": "cpp",
		"vector": "cpp",
		"string": "cpp",
		"iostream": "cpp",
		"iomanip": "cpp",
		"thread": "cpp",
		"algorithm": "cpp",
		"any": "cpp",
		"array": "cpp",
		"atomic": "cpp",
		"bit": "cpp",
		"bitset": "cpp",
		"cmath": "cpp",
		"concepts": "cpp",
		"coroutine": "cpp",
		"deque": "cpp",
		"exception": "cpp",
		"filesystem": "cpp",
		"format": "cpp",
		"functional": "cpp",
		"future": "cpp",
		"initializer_list": "cpp",
		"iterator": "cpp",
		"limits": "cpp",
		"list": "cpp",
		"map": "cpp",
		"memory": "cpp",
		"mutex": "cpp",
		"optional": "cpp",
		"ostream": "cpp",
		"queue": "cpp",
		"set": "cpp",
		"span": "cpp",
		"sstream": "cpp",
		"stack": "cpp",
		"stdexcept": "cpp",
		"tuple": "cpp",
		"type_traits": "cpp",
		"typeinfo": "cpp",
		"unordered_map": "cpp",
		"unordered_set": "cpp",
		"utility": "cpp",
		"variant": "cpp",
		"xutility": "cpp",
		"print": "cpp"
	},
}
```