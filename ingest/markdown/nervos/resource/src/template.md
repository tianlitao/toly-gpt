[View code on GitHub](https://github.com/nervosnetwork/ckb/resource/src/template.rs)

The code defines a template engine that can be used to generate configuration files for different chain specs. The engine is designed to work with TOML files, and it supports two main features: spec branches and variables.

Spec branches allow the user to define different configurations for different chain specs. The engine replaces a line with a branch matching the given spec name. The block starts with the line ending with ` # {{` and ends with a line `# }}`. Between the start and end markers, every line is a branch starting with `# SPEC => CONTENT`, where `SPEC` is the branch spec name, and `CONTENT` is the text to be replaced for the spec. A special spec name `_` acts as a wildcard which matches any spec name. In the `CONTENT`, variables are expanded and all the escape sequences `\n` are replaced by new lines.

Variables are defined as key-value pairs in `TemplateContext` via `TemplateContext::new` or `TemplateContext::insert`. Template uses variables by surrounding the variable names with curly brackets. The variables expansions only happen inside the spec branches in the spec `CONTENT`.

The `Template` struct represents a TOML template, and the `TemplateContext` struct represents the context used to expand the `Template`. The `render_to` method expands the template using the context and writes the result via the writer `w`. The `render` method renders the template and returns the result as a string.

The code also defines some constants for the default chain spec, the list of bundled chain specs, the default RPC listen port, and the default P2P listen port.
## Questions: 
 1. What is the purpose of the `Template` struct and how is it used?
   
   The `Template` struct is a simple template which supports spec branches and variables. It is designed so that without expanding the template, it is still a valid TOML file. It is used to expand the template using the context and writes the result via the writer.

2. What is the purpose of the `TemplateContext` struct and how is it used?
   
   The `TemplateContext` struct is the context used to expand the `Template`. It is used to create a new template with the specified content and to insert a new variable into the context.

3. What is the purpose of the `render` and `render_to` methods on the `Template` struct?
   
   The `render` method renders the template and returns the result as a string. The `render_to` method expands the template using the context and writes the result via the writer. Both methods return `std::io::Error` when they fail to write the chunks to the underlying writer or it failed to convert the result text to UTF-8.