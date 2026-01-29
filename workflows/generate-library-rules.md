---
title: "Generate single library rule file"
tags: [rules, code-generation, documentation, open-source, libraries, ai-assistance]
---

Goal: Create a single Explyt rule file based on provided library documentation or source code to improve AI-assisted code generation with that library.

## Overview
This workflow generates one rule file that guides the Explyt Agent when generating code using a specific open-source library. The rule is based on library documentation, API references, best practices, and source code patterns.

## Working mode: STRICT STEP-BY-STEP WITH FLOW CONTROL

---

## FLOW CONTROL

### STOP COMMAND
1. Complete all actions of the current step.
2. Use the **Output** section to provide the requested result.
3. As the **last line** of the message, write:
   **`STOP. Waiting for user input/confirmation.`**

### AUTOMATIC TRANSITION (CHAINING)
1. Complete all actions of the current step.
2. Add a horizontal separator: `---`.
3. Use the **Output** section from the previous step to initialize the next step.
4. In the same message, perform the **NEXT** step.

---

## WORKFLOW ALGORITHM

### STEP 1: Library Information Collection (Initiation)

**Actions:**
1. Check if the user has provided any library information (URL, name, or documentation)
2. If no library information is provided, stop the workflow and request it
3. **STRICT PROHIBITION:** Do NOT analyze the project, search for local examples, or access any project files at this stage
4. **STRICT PROHIBITION:** Do NOT read, search, or examine any files from the current project without explicit user permission

**Output:**
*If no library information is provided:*
To create a library-specific rule, I need information about the library. Please provide one of the following:
1. Library documentation URL (official docs, API reference, tutorials)
2. GitHub repository URL for the library
3. Specific library name with version
4. Key use cases you want to optimize for

**STOP COMMAND.**

*If library information is provided:* Proceed to Step 2.

---

### STEP 2: Documentation Analysis and Local Examples Request

**Actions:**
1. Fetch and analyze the provided documentation or source code
2. Identify core concepts, key classes, common usage patterns, best practices, configuration requirements, error handling approaches, and testing strategies
3. **STRICT PROHIBITION:** Do NOT access any project files without explicit user permission
4. Ask the user for explicit permission to search local project files

**Output:**
"I have analyzed the provided library documentation. 

**IMPORTANT:** Before I can search for examples in your current project files, I need your explicit permission. 

Would you like me to search for examples of this library's usage in your current project files? This can provide real-world usage patterns from your codebase.

**Note:** Without your permission, I will NOT access any project files."

**Options:**
- Yes, search local project files for usage examples
- No, generate rule based only on provided documentation

**STOP COMMAND.**

---

### STEP 3: Local Project Analysis (ONLY if user explicitly granted permission)

**Prerequisite:** User must have explicitly selected "Yes, search local project files for usage examples" in Step 2

**Actions:**
1. **ONLY PROCEED IF PERMISSION GRANTED:** Search the current project for:
   - Import statements of the library
   - Usage of library classes and methods
   - Configuration patterns
   - Error handling approaches
   - Testing patterns
2. Extract relevant code examples
3. Analyze usage patterns specific to this project

**Output:**
Collection of real-world usage examples from the current project to incorporate into the rule file.

**AUTOMATIC TRANSITION → Step 4.**

---

### STEP 4: Generate Single Rule File

**Actions:**
Generate a complete rule file with:
1. **File pattern** header (default: `**/*.kt` for Kotlin or `**/*.java` for Java, can be customized)
2. **Library overview** section explaining key concepts
3. **Code generation guidelines** for the agent
4. **Examples** section with:
   - General examples from documentation
   - *If local examples were collected:* Project-specific usage patterns
5. **Common pitfalls** to avoid
6. **Testing recommendations** if applicable
7. **Resources** section with links to documentation

**Output:**
A single complete rule file ready for use, saved with appropriate naming (e.g., `library-[library-name]-rules.md`) in the `.explyt/rules` directory.

**STOP COMMAND.**



## Single Rule File Structure

The generated rule file will follow this structure:

```
---
filePattern: "**/*.kt" 
---

# Library: [Library Name] - Code Generation Guidelines

## Overview
[Brief description of the library and its purpose]

## Key Concepts
- [Concept 1]: [Explanation]
- [Concept 2]: [Explanation]
- [Concept 3]: [Explanation]

## Code Generation Guidelines
### When generating code with [Library Name]:
1. **Imports**: Always import [specific packages] for [functionality]
2. **Initialization**: Use [preferred initialization pattern]
3. **Configuration**: Follow [configuration best practices]
4. **Error Handling**: Implement [library-specific error handling]
5. **Resource Management**: [Resource management guidelines]

### Patterns to Use
// Example of correct usage from documentation
[Code example]

### Project-Specific Patterns (if applicable)
// Examples from current project
[Local project code examples]

## Common Use Cases
1. **[Use Case 1]**: [Implementation guidance]
2. **[Use Case 2]**: [Implementation guidance]
3. **[Use Case 3]**: [Implementation guidance]

## Testing Recommendations
- [Testing approach 1]
- [Testing approach 2]
- [Mocking guidelines if applicable]

## Resources
- [Link to official documentation]
- [Link to API reference]
- [Link to examples repository]
```

## Output
A single rule file will be generated and saved with a name like `library-[library-name]-rule.md` in the `.explyt/rules` directory.

## How to Start
Provide details about the library you want to create a rule for, and I'll generate a single rule file based on that information.
