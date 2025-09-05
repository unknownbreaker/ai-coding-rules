# TCL LSP for Neovim - Updated Project Outline

## Project Architecture

```
tcl-lsp.nvim/
├── lua/
│   ├── tcl-lsp/
│   │   ├── init.lua              # Main plugin entry
│   │   ├── server.lua            # LSP server wrapper
│   │   ├── config.lua            # Configuration management
│   │   ├── parser/               # Tcl parsing logic
│   │   │   ├── init.lua
│   │   │   ├── ast.lua           # AST building
│   │   │   ├── symbols.lua       # Symbol extraction
│   │   │   └── scope.lua         # Scope analysis
│   │   ├── analyzer/             # Symbol analysis
│   │   │   ├── init.lua
│   │   │   ├── workspace.lua     # Workspace scanning
│   │   │   ├── references.lua    # Reference finding
│   │   │   └── definitions.lua   # Definition resolution
│   │   ├── features/             # LSP feature implementations
│   │   │   ├── completion.lua    # Code completion
│   │   │   ├── hover.lua         # Hover information
│   │   │   ├── signature.lua     # Signature help
│   │   │   ├── diagnostics.lua   # Error/warning detection
│   │   │   ├── formatting.lua    # Code formatting
│   │   │   ├── highlights.lua    # Document highlights
│   │   │   ├── symbols.lua       # Document/workspace symbols
│   │   │   ├── codelens.lua      # Code lens
│   │   │   └── folding.lua       # Folding ranges
│   │   ├── actions/              # Code actions
│   │   │   ├── init.lua
│   │   │   ├── rename.lua        # Symbol renaming
│   │   │   ├── cleanup.lua       # Remove unused items
│   │   │   └── refactor.lua      # Future refactoring actions
│   │   └── utils/                # Utility functions
│   │       ├── cache.lua         # Caching system
│   │       ├── logger.lua        # Logging utilities
│   │       └── helpers.lua       # Common helpers
├── tcl/                          # Tcl scripts for analysis
│   ├── core/
│   │   ├── parser.tcl           # Main parsing engine
│   │   ├── ast_builder.tcl      # AST construction
│   │   ├── symbol_finder.tcl    # Symbol identification
│   │   ├── scope_analyzer.tcl   # Scope resolution
│   │   └── workspace_scanner.tcl # Workspace indexing
│   ├── features/
│   │   ├── completion.tcl       # Completion logic
│   │   ├── hover.tcl           # Hover info generation
│   │   ├── diagnostics.tcl     # Error detection
│   │   ├── formatting.tcl      # Code formatting
│   │   └── references.tcl      # Reference finding
│   └── utils/
│       ├── file_utils.tcl      # File operations
│       └── string_utils.tcl    # String manipulation
├── plugin/
│   └── tcl-lsp.vim             # Vim plugin registration
├── doc/
│   └── tcl-lsp.txt             # Documentation
└── tests/
    ├── lua/                    # Lua tests
    ├── tcl/                    # Tcl tests
    └── fixtures/               # Test files
```

## Development Phases

### Phase 1: Core Infrastructure (Weeks 1-2)
**Foundation Setup**
- [ ] Basic Neovim plugin structure
- [ ] LSP server initialization and lifecycle management
- [ ] Tclsh process spawning and communication
- [ ] Basic message handling (JSON-RPC)
- [ ] Configuration system
- [ ] Logging and error handling

### Phase 2: Parsing Engine (Weeks 3-4)
**Tcl Analysis Core**
- [ ] Tcl AST parser using tclsh
- [ ] Symbol identification (procs, namespaces, variables, packages)
- [ ] Scope analysis and resolution
- [ ] Workspace file scanning and indexing
- [ ] Cross-file reference tracking
- [ ] Caching system for performance

### Phase 3: Essential LSP Features (Weeks 5-8)
**Core Language Features**
- [ ] **Go to Definition** (same file → cross-file → packages/namespaces)
- [ ] **Go to References** (with workspace-wide search)
- [ ] **Code Completion** (procs, variables, packages, namespaces, built-ins)
- [ ] **Hover Information** (proc signatures, variable info, documentation)
- [ ] **Diagnostics** (syntax errors, undefined variables, unreachable code)
- [ ] **Document Symbols** (outline view)

### Phase 4: Code Actions & Advanced Features (Weeks 9-11)
**Productivity Features**
- [ ] **Symbol Renaming** (workspace-wide)
- [ ] **Code Actions** (remove unused variables/packages/procs)
- [ ] **Signature Help** (proc parameters, built-in command syntax)
- [ ] **Document Formatting** (indentation, brace placement, style)
- [ ] **Workspace Symbols** (global symbol search)
- [ ] **Document Highlights** (highlight symbol under cursor)

### Phase 5: Polish & Performance (Weeks 12-14)
**Enhancement Features**
- [ ] **Code Lens** (reference counts, executable indicators)
- [ ] **Folding Ranges** (procs, namespaces, comments)
- [ ] **Inlay Hints** (variable types, parameter names)
- [ ] Performance optimization (incremental parsing, smart caching)
- [ ] Error handling improvements
- [ ] Comprehensive testing suite

### Phase 6: Quality & Documentation (Weeks 15-16)
**Final Polish**
- [ ] Security scan compliance
- [ ] Performance benchmarking (<300ms response times)
- [ ] Documentation and examples
- [ ] User configuration options
- [ ] Plugin distribution setup

## Success Metrics (Updated)

### Original Requirements
- [ ] Go to definition (procs, packages, namespaces, variables)
- [ ] Go to references (workspace-wide)
- [ ] Symbol outline
- [ ] Code actions (rename, cleanup unused items)
- [ ] Performance (<300ms response times)
- [ ] Security scan compliance

### New Essential Features
- [ ] **Code Completion**
  - Proc names with signatures
  - Variable names with scope awareness
  - Package names with auto-import
  - Namespace completion
  - Built-in Tcl commands
- [ ] **Hover Information**
  - Proc signatures and documentation
  - Variable type and scope info
  - Package descriptions
  - Namespace information
- [ ] **Signature Help**
  - Real-time parameter information
  - Parameter highlighting
  - Overload navigation
- [ ] **Diagnostics**
  - Syntax error detection
  - Undefined variable warnings
  - Unreachable code detection
  - Style/convention hints
- [ ] **Document Formatting**
  - Consistent indentation
  - Brace placement standardization
  - Line length management

### Advanced Features
- [ ] **Document Highlights** - Highlight all instances of symbol under cursor
- [ ] **Workspace Symbols** - Global project symbol search
- [ ] **Code Lens** - Inline reference counts and actionable information
- [ ] **Folding Ranges** - Code folding for better navigation
- [ ] **Inlay Hints** - Inline type and parameter information

## Technical Implementation Notes

### RVT Support Architecture
**librivetparser.so Integration:**
- Official Apache Rivet parser library for accurate RVT template parsing
- Graceful fallback to pure Tcl parser when library unavailable
- Cross-platform binary distribution (Linux, macOS, Windows)
- Automatic installation and configuration

**Mixed Content Analysis:**
- HTML structure parsing and validation
- TCL code block extraction and analysis using tclsh
- Template variable scope tracking across boundaries
- Context-aware completions for HTML, TCL, and Rivet commands

### Performance Considerations
- **Incremental Parsing**: Only re-parse changed files
- **Smart Caching**: Cache parsed results with file modification tracking
- **Background Processing**: Workspace scanning in separate process
- **Lazy Loading**: Load symbols on-demand for large projects

### Tcl-Specific Challenges
- **Dynamic Nature**: Handle runtime variable creation and modification
- **Package System**: Parse `pkgIndex.tcl` files and track package dependencies
- **Namespace Resolution**: Complex namespace inheritance and variable scoping
- **Source Command**: Handle dynamic file inclusion and evaluation

### LSP Capability Registration
```lua
capabilities = {
  textDocumentSync = "incremental",
  completionProvider = {
    triggerCharacters = {".", ":", "$", "["},
    resolveProvider = true
  },
  hoverProvider = true,
  signatureHelpProvider = {
    triggerCharacters = {"(", " ", ","}
  },
  definitionProvider = true,
  referencesProvider = true,
  documentSymbolProvider = true,
  workspaceSymbolProvider = true,
  codeActionProvider = true,
  renameProvider = true,
  documentFormattingProvider = true,
  documentHighlightProvider = true,
  foldingRangeProvider = true,
  codeLensProvider = {
    resolveProvider = false
  },
  inlayHintProvider = true
}
```

## Recommended Workflow for Development

### Test-Driven Development (TDD) Approach

**For Each Function:**
1. **Write Documentation First** - Define function signature, parameters, return values
2. **Write Tests** - Create comprehensive test cases including edge cases
3. **Implement Function** - Write the actual implementation
4. **Verify Coverage** - Ensure all tests pass and coverage requirements are met
5. **Generate Docs** - Auto-generate API documentation from comments

**Example Development Cycle:**
```lua
-- Step 1: Document the function
--- Extracts all procedure definitions from Tcl source code
--- @param source_code string The Tcl source code to parse
--- @param file_path string Path to the source file for error reporting
--- @return table List of procedure definitions with metadata
--- @return string|nil Error message if parsing fails

-- Step 2: Write tests
describe("extract_proc_definitions", function()
  it("should extract simple proc", function()
    local code = "proc hello {} { puts \"Hello\" }"
    local result = extract_proc_definitions(code, "test.tcl")
    assert.equals(1, #result)
    assert.equals("hello", result[1].name)
  end)
end)

-- Step 3: Implement
local function extract_proc_definitions(source_code, file_path)
  -- Implementation here
end
```

### Documentation Generation

**Automated Documentation:**
- Use **LuaLS annotations** for Lua functions
- Use **custom parser** for Tcl procedure documentation
- Generate **HTML/markdown docs** from source comments
- Include **usage examples** in all documentation
- Maintain **API reference** with cross-links

**Documentation Tools:**
- **ldoc** for Lua documentation generation
- **Custom Tcl doc parser** for Tcl procedures
- **GitHub Pages** for hosting documentation
- **VSCode integration** for inline documentation

This comprehensive approach ensures that every function is well-documented, thoroughly tested, and maintainable. The emphasis on TDD and documentation-first development will result in a professional-quality codebase that's easy to understand, extend, and debug.
