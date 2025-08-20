# Project: TCL LSP for Neovim

## Core Features

1. Go to definition
2. Go to references
3. Symbol outline
4. Code actions - Renaming all references to a variable/package/proc/namespace
5. Code actions - Removing unused definitions

## Technical Stack

- Engine: tclsh
- Language: Lua
- AI Tools: Claude

## Success Metrics

- [ ] When the cursor is on a proc call and the proc definition is in the same
      file, go to definition should move the cursor to the corresponding proc
      definition within that file
- [ ] When the cursor is on a proc call and the proc definition is in not in the
      same file, go to definition should open the file where the proc definition
      exists and move the cursor to the corresponding proc definition in that
      file
- [ ] When the cursor is on a package name, like
      `package require [package name]`, go to definition should open the
      lspconfig's finder popup to show both the file that contains the
      `package provide [package name]` and the `pkgIndex.tcl` file that indexed
      the package.
- [ ] When the cursor is on a namespace, like `::namespace::someProcCall`, go to
      definition should open the file where the namespace definition exists and
      move the cursor to where the namespace is defined.
- [ ] When the cursor is on a nested namespace, like being on `namespace2` in
      `::namespace1::namespace2::namespace3::someProcCall`, go to definition
      should open the file where the namespace definition exists and move the
      cursor to where `namespace2` is defined.
- [ ] When the cursor is on a variable, like `$variable`, and the variable's
      definition is within the same scope, go to definition should move the
      cursor to where it is defined within that scope.
- [ ] When the cursor is on a variable, like `$variable`, and the variable's
      definition is within a higher scope, go to definition should move the
      cursor to the nearest scope for where it is defined.
- [ ] When the cursor is on a variable, like `$variable`, and the variable's
      definition is not within the same file, go to definition should open the
      file for where it is defined and move the cursor to its definition.
- [ ] When the cursor is on a symbol that is either a definition or a call, go
      to reference should open lspconfig's finder popup to show a list of all
      references to that symbol across the workspace.
- [ ] When the cursor is on any symbol name, triggering the code action to
      rename the symbol should be able to rename all references to it across the
      workspace.
- [ ] When the cursor is anywhere in a file, triggering the code action to
      remove unused variables should delete all references to any variable not
      being called in that file.
- [ ] When the cursor is anywhere in a file, triggering the code action to
      remove unused packages should remove the statement for requiring that
      package in that file.
- [ ] When the cursor is anywhere in a file, triggering the code action to
      remove unused proc definition should remove the entire block of the proc
      from that file.
- [ ] Go to definition should complete its process within 300ms
- [ ] Go to references should complete its process within 300ms
- [ ] Code actions should complete their processes within 300ms
- [ ] Passes security scan

## AI Instructions

"Always use TypeScript" "Follow React best practices" "Prioritize readability
over cleverness"
