# plan-commands
Gemini CLI Extension with Custom Commands for plan, refine, implement.

**See** [Gemini CLI Extensions](https://github.com/google-gemini/gemini-cli/blob/main/docs/extensions/index.md) for more details.

**Credits**: [@dandobrin](https://github.com/ddobrin), this work was copied from Dan's [production serverless repository](https://github.com/GoogleCloudPlatform/serverless-production-readiness-java-gcp/tree/main/genai/quotes-llm/.gemini/commands) and broken into separate repository for easy installation.

## Prerequisites
Install the [Gemini CLI](https://github.com/google-gemini/gemini-cli)

## Extension Installation
From your command line:

```bash
gemini extensions install https://github.com/jjdelorme/plan-commands
```

## Sql Commands

A new subfolder `./sql` was created to support a 5 phase process of taking a legacy stored procedure and generating a Cloud Native, Domain Driven Design, Clean Architecture, and Test Driven Implementation.

### 1. Generate Analysis
```
/sql:analysis @./path-to-your/sp_name.sql 
```

### 2. Generate Logical Architecture (tech-stack agnostic)
```
/sql:logical @./path-to-ANALYSIS.md
```

### 3. Generate Physical Architecture
Provide tech stack guidance; C#, .NET 10, Postgres, GCP Cloud Run, etc...
```
/sql:physical @./path-to-logical.md
```

### 4. Generate a detailed implementation plan
```
/sql:plan
```

**NOTE:** At this point it would be wise to `/clear` the context window.

### 5. Execute the plan
```
/sql:implement @IMPLEMENTATION_PLAN.md
```
