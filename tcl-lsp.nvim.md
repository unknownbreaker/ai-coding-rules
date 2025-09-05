# TCL LSP for Neovim - Updated Project Outline

## Project Architecture

```
tcl-lsp.nvim/
├── .github/                      # GitHub-specific files
│   ├── workflows/
│   │   ├── ci.yml               # Continuous Integration pipeline
│   │   ├── release.yml          # Release automation
│   │   └── docs.yml             # Documentation generation
│   ├── ISSUE_TEMPLATE/
│   │   ├── bug_report.md        # Bug report template
│   │   ├── feature_request.md   # Feature request template
│   │   └── config.yml           # Issue template configuration
│   ├── PULL_REQUEST_TEMPLATE.md # PR template
│   └── FUNDING.yml              # Sponsorship information
├── .gitignore                   # Git ignore patterns
├── .gitattributes              # Git attributes
├── .editorconfig               # Editor configuration
├── .luarc.json                 # Lua language server config
├── .luacheckrc                 # Luacheck configuration
├── .stylua.toml                # StyLua formatter config
├── .nvmrc                      # Node.js version for CI
├── Makefile                    # Build automation
├── README.md                   # Project overview and setup
├── CHANGELOG.md                # Version history
├── LICENSE                     # Software license (MIT recommended)
├── CONTRIBUTING.md             # Contribution guidelines
├── CODE_OF_CONDUCT.md          # Community guidelines
├── SECURITY.md                 # Security policy
├── pyproject.toml              # Python project config (for tools)
├── package.json                # Node.js dependencies (for testing)
├── requirements-dev.txt        # Python development dependencies
├── rockspec/                   # LuaRocks specifications
│   └── tcl-lsp.nvim-dev-1.rockspec
├── scripts/                    # Build and utility scripts
│   ├── prepare_release.sh      # Release preparation script
│   ├── install_deps.sh         # Dependency installation
│   ├── run_benchmarks.sh       # Performance benchmarking
│   └── generate_tcl_docs.tcl   # TCL documentation generator
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
│   ├── tcl-lsp.txt             # Neovim help documentation
│   ├── api/                    # API documentation
│   │   ├── lua/                # Lua API docs
│   │   └── tcl/                # TCL API docs
│   └── examples/               # Usage examples
│       ├── basic_setup.lua     # Basic configuration example
│       ├── advanced_config.lua # Advanced configuration
│       └── custom_handlers.lua # Custom LSP handlers
└── tests/                      # Comprehensive test suite
    ├── lua/                    # Lua module tests
    │   ├── test_init.lua       # Main plugin entry tests
    │   ├── test_server.lua     # LSP server wrapper tests
    │   ├── test_config.lua     # Configuration management tests
    │   ├── parser/             # Parser module tests
    │   │   ├── test_init.lua
    │   │   ├── test_ast.lua    # AST building tests
    │   │   ├── test_symbols.lua # Symbol extraction tests
    │   │   └── test_scope.lua  # Scope analysis tests
    │   ├── analyzer/           # Analyzer module tests
    │   │   ├── test_init.lua
    │   │   ├── test_workspace.lua # Workspace scanning tests
    │   │   ├── test_references.lua # Reference finding tests
    │   │   └── test_definitions.lua # Definition resolution tests
    │   ├── features/           # LSP features tests
    │   │   ├── test_completion.lua  # Code completion tests
    │   │   ├── test_hover.lua       # Hover information tests
    │   │   ├── test_signature.lua   # Signature help tests
    │   │   ├── test_diagnostics.lua # Diagnostics tests
    │   │   ├── test_formatting.lua  # Code formatting tests
    │   │   ├── test_highlights.lua  # Document highlights tests
    │   │   ├── test_symbols.lua     # Document/workspace symbols tests
    │   │   ├── test_codelens.lua    # Code lens tests
    │   │   └── test_folding.lua     # Folding ranges tests
    │   ├── actions/            # Code actions tests
    │   │   ├── test_init.lua
    │   │   ├── test_rename.lua      # Symbol renaming tests
    │   │   ├── test_cleanup.lua     # Remove unused items tests
    │   │   └── test_refactor.lua    # Refactoring actions tests
    │   └── utils/              # Utility tests
    │       ├── test_cache.lua       # Caching system tests
    │       ├── test_logger.lua      # Logging utilities tests
    │       └── test_helpers.lua     # Common helpers tests
    ├── tcl/                    # Tcl script tests
    │   ├── core/               # Core functionality tests
    │   │   ├── test_parser.tcl      # Main parsing engine tests
    │   │   ├── test_ast_builder.tcl # AST construction tests
    │   │   ├── test_symbol_finder.tcl # Symbol identification tests
    │   │   ├── test_scope_analyzer.tcl # Scope resolution tests
    │   │   └── test_workspace_scanner.tcl # Workspace indexing tests
    │   ├── features/           # Feature tests
    │   │   ├── test_completion.tcl  # Completion logic tests
    │   │   ├── test_hover.tcl       # Hover info generation tests
    │   │   ├── test_diagnostics.tcl # Error detection tests
    │   │   ├── test_formatting.tcl  # Code formatting tests
    │   │   └── test_references.tcl  # Reference finding tests
    │   ├── utils/              # Utility tests
    │   │   ├── test_file_utils.tcl  # File operations tests
    │   │   └── test_string_utils.tcl # String manipulation tests
    │   └── run_tests.tcl       # TCL test runner
    ├── fixtures/               # Test data files
    │   ├── sample_tcl/         # Sample Tcl files for testing
    │   │   ├── simple_proc.tcl      # Basic procedure definitions
    │   │   ├── namespaces.tcl       # Namespace examples
    │   │   ├── packages.tcl         # Package usage examples
    │   │   ├── variables.tcl        # Variable scope examples
    │   │   ├── complex_project/     # Multi-file project structure
    │   │   │   ├── main.tcl
    │   │   │   ├── utils.tcl
    │   │   │   └── config.tcl
    │   │   └── syntax_errors.tcl    # Files with intentional errors
    │   ├── sample_rvt/         # RVT template files for testing
    │   │   ├── simple_template.rvt  # Basic RVT template
    │   │   ├── complex_template.rvt # Complex mixed HTML/TCL
    │   │   └── error_template.rvt   # Templates with errors
    │   ├── expected_outputs/   # Expected test results
    │   │   ├── ast_outputs/         # Expected AST structures
    │   │   │   ├── simple_proc_ast.json
    │   │   │   ├── namespace_ast.json
    │   │   │   ├── package_ast.json
    │   │   │   ├── variable_scope_ast.json
    │   │   │   ├── complex_control_flow_ast.json
    │   │   │   ├── array_usage_ast.json
    │   │   │   ├── string_operations_ast.json
    │   │   │   ├── file_operations_ast.json
    │   │   │   ├── error_handling_ast.json
    │   │   │   ├── nested_structures_ast.json
    │   │   │   ├── comments_ast.json
    │   │   │   ├── multiline_strings_ast.json
    │   │   │   ├── escape_sequences_ast.json
    │   │   │   ├── expr_commands_ast.json
    │   │   │   ├── list_operations_ast.json
    │   │   │   ├── dict_operations_ast.json
    │   │   │   ├── upvar_global_ast.json
    │   │   │   ├── source_include_ast.json
    │   │   │   ├── eval_exec_ast.json
    │   │   │   └── rvt_template_ast.json
    │   │   ├── symbol_outputs/      # Expected symbol tables
    │   │   │   ├── proc_symbols.json
    │   │   │   ├── variable_symbols.json
    │   │   │   ├── namespace_symbols.json
    │   │   │   ├── package_symbols.json
    │   │   │   ├── global_symbols.json
    │   │   │   ├── local_scope_symbols.json
    │   │   │   ├── cross_file_symbols.json
    │   │   │   ├── builtin_commands.json
    │   │   │   ├── array_symbols.json
    │   │   │   ├── upvar_symbols.json
    │   │   │   ├── alias_symbols.json
    │   │   │   ├── imported_symbols.json
    │   │   │   ├── exported_symbols.json
    │   │   │   ├── nested_proc_symbols.json
    │   │   │   ├── lambda_symbols.json
    │   │   │   ├── closure_symbols.json
    │   │   │   ├── dynamic_symbols.json
    │   │   │   ├── overloaded_symbols.json
    │   │   │   ├── shadowed_symbols.json
    │   │   │   └── rvt_symbols.json
    │   │   ├── diagnostic_outputs/  # Expected diagnostic messages
    │   │   │   ├── syntax_errors.json
    │   │   │   ├── undefined_variables.json
    │   │   │   ├── unused_variables.json
    │   │   │   ├── unused_procedures.json
    │   │   │   ├── unreachable_code.json
    │   │   │   ├── missing_packages.json
    │   │   │   ├── invalid_namespace.json
    │   │   │   ├── type_mismatches.json
    │   │   │   ├── deprecated_commands.json
    │   │   │   ├── style_violations.json
    │   │   │   ├── performance_hints.json
    │   │   │   ├── security_warnings.json
    │   │   │   ├── circular_deps.json
    │   │   │   ├── scope_violations.json
    │   │   │   ├── command_conflicts.json
    │   │   │   ├── missing_braces.json
    │   │   │   ├── quote_mismatches.json
    │   │   │   ├── bracket_errors.json
    │   │   │   ├── encoding_issues.json
    │   │   │   └── rvt_template_errors.json
    │   │   ├── completion_outputs/  # Expected completion results
    │   │   │   ├── proc_completions.json
    │   │   │   ├── variable_completions.json
    │   │   │   ├── namespace_completions.json
    │   │   │   ├── package_completions.json
    │   │   │   ├── builtin_completions.json
    │   │   │   ├── array_key_completions.json
    │   │   │   ├── file_path_completions.json
    │   │   │   ├── option_completions.json
    │   │   │   ├── context_completions.json
    │   │   │   ├── partial_completions.json
    │   │   │   ├── snippet_completions.json
    │   │   │   ├── import_completions.json
    │   │   │   ├── method_completions.json
    │   │   │   ├── property_completions.json
    │   │   │   ├── enum_completions.json
    │   │   │   ├── callback_completions.json
    │   │   │   ├── template_completions.json
    │   │   │   ├── conditional_completions.json
    │   │   │   ├── nested_completions.json
    │   │   │   └── rvt_completions.json
    │   │   ├── hover_outputs/       # Expected hover information
    │   │   │   ├── proc_hover_info.json
    │   │   │   ├── variable_hover_info.json
    │   │   │   ├── namespace_hover_info.json
    │   │   │   ├── package_hover_info.json
    │   │   │   ├── builtin_hover_info.json
    │   │   │   ├── array_hover_info.json
    │   │   │   ├── string_hover_info.json
    │   │   │   ├── numeric_hover_info.json
    │   │   │   ├── file_hover_info.json
    │   │   │   ├── url_hover_info.json
    │   │   │   ├── comment_hover_info.json
    │   │   │   ├── error_hover_info.json
    │   │   │   ├── warning_hover_info.json
    │   │   │   ├── type_hover_info.json
    │   │   │   ├── scope_hover_info.json
    │   │   │   ├── usage_hover_info.json
    │   │   │   ├── performance_hover_info.json
    │   │   │   ├── security_hover_info.json
    │   │   │   ├── version_hover_info.json
    │   │   │   └── rvt_hover_info.json
    │   │   ├── reference_outputs/   # Expected reference results
    │   │   │   ├── proc_references.json
    │   │   │   ├── variable_references.json
    │   │   │   ├── namespace_references.json
    │   │   │   ├── package_references.json
    │   │   │   ├── global_references.json
    │   │   │   ├── local_references.json
    │   │   │   ├── cross_file_references.json
    │   │   │   ├── array_references.json
    │   │   │   ├── string_references.json
    │   │   │   ├── command_references.json
    │   │   │   ├── alias_references.json
    │   │   │   ├── import_references.json
    │   │   │   ├── export_references.json
    │   │   │   ├── recursive_references.json
    │   │   │   ├── callback_references.json
    │   │   │   ├── event_references.json
    │   │   │   ├── template_references.json
    │   │   │   ├── config_references.json
    │   │   │   ├── documentation_references.json
    │   │   │   └── rvt_references.json
    │   │   ├── definition_outputs/  # Expected definition results
    │   │   │   ├── proc_definitions.json
    │   │   │   ├── variable_definitions.json
    │   │   │   ├── namespace_definitions.json
    │   │   │   ├── package_definitions.json
    │   │   │   ├── global_definitions.json
    │   │   │   ├── local_definitions.json
    │   │   │   ├── array_definitions.json
    │   │   │   ├── alias_definitions.json
    │   │   │   ├── import_definitions.json
    │   │   │   ├── export_definitions.json
    │   │   │   ├── class_definitions.json
    │   │   │   ├── method_definitions.json
    │   │   │   ├── property_definitions.json
    │   │   │   ├── event_definitions.json
    │   │   │   ├── callback_definitions.json
    │   │   │   ├── template_definitions.json
    │   │   │   ├── macro_definitions.json
    │   │   │   ├── constant_definitions.json
    │   │   │   ├── type_definitions.json
    │   │   │   └── rvt_definitions.json
    │   │   ├── formatting_outputs/  # Expected formatting results
    │   │   │   ├── basic_formatting.tcl
    │   │   │   ├── brace_formatting.tcl
    │   │   │   ├── line_length_formatting.tcl
    │   │   │   ├── comment_formatting.tcl
    │   │   │   ├── namespace_formatting.tcl
    │   │   │   ├── procedure_formatting.tcl
    │   │   │   ├── control_flow_formatting.tcl
    │   │   │   ├── array_formatting.tcl
    │   │   │   ├── string_formatting.tcl
    │   │   │   ├── list_formatting.tcl
    │   │   │   ├── expr_formatting.tcl
    │   │   │   ├── multiline_formatting.tcl
    │   │   │   ├── nested_formatting.tcl
    │   │   │   ├── package_formatting.tcl
    │   │   │   ├── error_formatting.tcl
    │   │   │   ├── documentation_formatting.tcl
    │   │   │   ├── whitespace_formatting.tcl
    │   │   │   ├── alignment_formatting.tcl
    │   │   │   ├── consistency_formatting.tcl
    │   │   │   └── rvt_formatting.rvt
    │   │   ├── symbol_outline_outputs/ # Expected symbol outlines
    │   │   │   ├── simple_outline.json
    │   │   │   ├── complex_outline.json
    │   │   │   ├── namespace_outline.json
    │   │   │   ├── class_outline.json
    │   │   │   ├── package_outline.json
    │   │   │   ├── hierarchical_outline.json
    │   │   │   ├── filtered_outline.json
    │   │   │   ├── sorted_outline.json
    │   │   │   ├── detailed_outline.json
    │   │   │   ├── minimal_outline.json
    │   │   │   ├── workspace_outline.json
    │   │   │   ├── cross_file_outline.json
    │   │   │   ├── type_grouped_outline.json
    │   │   │   ├── scope_grouped_outline.json
    │   │   │   ├── usage_outline.json
    │   │   │   ├── documentation_outline.json
    │   │   │   ├── performance_outline.json
    │   │   │   ├── security_outline.json
    │   │   │   ├── version_outline.json
    │   │   │   └── rvt_outline.json
    │   │   └── performance_outputs/ # Expected performance metrics
    │   │       ├── parsing_benchmarks.json
    │   │       ├── completion_benchmarks.json
    │   │       ├── hover_benchmarks.json
    │   │       ├── reference_benchmarks.json
    │   │       ├── definition_benchmarks.json
    │   │       ├── diagnostic_benchmarks.json
    │   │       ├── formatting_benchmarks.json
    │   │       ├── symbol_benchmarks.json
    │   │       ├── workspace_benchmarks.json
    │   │       ├── memory_usage.json
    │   │       ├── cpu_usage.json
    │   │       ├── cache_performance.json
    │   │       ├── network_performance.json
    │   │       ├── file_io_performance.json
    │   │       ├── concurrent_performance.json
    │   │       ├── scalability_metrics.json
    │   │       ├── regression_baselines.json
    │   │       ├── optimization_results.json
    │   │       ├── profiling_data.json
    │   │       └── rvt_performance.json
    │   └── lsp_messages/       # Sample LSP message exchanges
    │       ├── completion_requests.json
    │       ├── hover_requests.json
    │       ├── definition_requests.json
    │       ├── reference_requests.json
    │       ├── diagnostic_requests.json
    │       ├── formatting_requests.json
    │       ├── symbol_requests.json
    │       ├── rename_requests.json
    │       ├── codelens_requests.json
    │       └── folding_requests.json
    ├── integration/            # Integration tests
    │   ├── test_lsp_server.lua     # Full LSP server integration
    │   ├── test_neovim_integration.lua # Neovim plugin integration
    │   ├── test_performance.lua    # Performance benchmarks
    │   ├── test_workflow.lua       # End-to-end workflow tests
    │   ├── test_multi_file.lua     # Multi-file project tests
    │   ├── test_large_projects.lua # Large codebase tests
    │   ├── test_rvt_integration.lua # RVT template integration
    │   └── test_cross_platform.lua # Cross-platform compatibility
    ├── e2e/                    # End-to-end tests
    │   ├── jest.config.js          # Jest configuration
    │   ├── setup.js               # Test setup
    │   └── specs/                 # E2E test specifications
    │       ├── completion.spec.js
    │       ├── hover.spec.js
    │       ├── goto_definition.spec.js
    │       ├── find_references.spec.js
    │       ├── diagnostics.spec.js
    │       ├── formatting.spec.js
    │       ├── rename.spec.js
    │       └── workspace.spec.js
    ├── spec/                   # Test specifications
    │   ├── busted_config.lua       # Busted test runner configuration
    │   ├── test_helpers.lua        # Common test utilities
    │   └── coverage_config.lua     # Code coverage configuration
    └── README.md               # Testing documentation
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
