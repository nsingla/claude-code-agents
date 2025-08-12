# Claude Code Agents: Impact Analyzer & Test Planner

This repository contains specialized AI agents for performing comprehensive impact analysis and test planning for software projects. These agents are designed to work with Claude Code in Cursor IDE and can analyze GitHub PRs, Jira tickets, and other project artifacts to generate detailed reports.

## Overview

The repository includes two main agents:

1. **Impact Analyzer** (`impact-analyzer.md`) - Analyzes the potential impact of code changes, architectural decisions, or system modifications
2. **Test Planner** (`test-plan-gen-subagent.md`) - Creates comprehensive test plans for features by gathering requirements from multiple sources

## Directory Structure

```
claude-code-agents/
├── impact-analyzer.md                    # Impact analyzer agent template
├── impact-analyzer-subagent.md           # Detailed subagent implementation
├── test-plan-gen-subagent.md             # Test planner agent template
├── extra-test-requirements.md            # Additional test requirements
├── impact-analyzer-requirements/         # Requirements for impact analysis
│   ├── README.md
│   ├── analysis-framework.md
│   ├── impact-categories.md
│   └── reporting-templates.md
├── test-plan-requirements/               # Requirements for test planning
│   ├── README.md
│   ├── test-categories.md
│   ├── test-environments.md
│   └── test-templates.md
└── README.md                             # This file
```

## Agent Descriptions

### Impact Analyzer Agent

**Purpose**: Analyzes the potential impact of code changes, architectural decisions, or system modifications across multiple dimensions including functionality, performance, security, and user experience.

**Key Capabilities**:
- Identifies direct dependencies and cascading effects
- Assesses risk levels by severity and likelihood
- Evaluates impacts across multiple dimensions
- Provides actionable recommendations
- Structures analysis in clear, prioritized format

**Input Sources**:
- GitHub Repository (current state and PR changes)
- Jira tickets (implementation details)
- Architecture documentation
- Test files and coverage

### Test Planner Agent

**Purpose**: Creates comprehensive test plans for features by gathering requirements from Google Documents, implementation details from Jira, and product information from GitHub repositories.

**Key Capabilities**:
- Generates structured test plans with required sections
- Covers multiple test categories (functional, security, performance, etc.)
- Supports different deployment configurations
- Includes compatibility matrix testing
- Provides test case templates and execution schedules

**Input Sources**:
- Google Documents (feature requirements)
- GitHub Repository (product details)
- Jira tickets (implementation details)

## Usage Instructions

### Method 1: Using Agents with Requirements Directories

#### Step 1: Set Up Requirements

1. **Impact Analyzer Requirements**:
   ```bash
   # Navigate to impact analyzer requirements
   cd impact-analyzer-requirements/
   
   # Review the analysis framework
   cat analysis-framework.md
   
   # Check impact categories
   cat impact-categories.md
   ```

2. **Test Plan Requirements**:
   ```bash
   # Navigate to test plan requirements
   cd test-plan-requirements/
   
   # Review test categories
   cat test-categories.md
   
   # Check test environments
   cat test-environments.md
   ```

#### Step 2: Configure Agent Parameters

For **Impact Analyzer**:
```yaml
agent_config:
  name: impact-analyzer
  description: "Analyze impact of code changes and architectural decisions"
  inputs:
    github_repo_url: "https://github.com/org/repo"
    github_pr_url: "https://github.com/org/repo/pull/123"
    jira_ticket_urls: ["https://company.atlassian.net/browse/TICKET-123"]
  requirements_dir: "./impact-analyzer-requirements/"
  output_format: "markdown"
```

For **Test Planner**:
```yaml
agent_config:
  name: test-plan-creator
  description: "Create comprehensive test plans for features"
  inputs:
    google_doc_url: "https://docs.google.com/document/d/..."
    github_repo_url: "https://github.com/org/repo"
    jira_ticket_urls: ["https://company.atlassian.net/browse/TICKET-123"]
  requirements_dir: "./test-plan-requirements/"
  output_format: "markdown"
```

#### Step 3: Execute Analysis

```bash
# Run impact analysis
claude-code-agent impact-analyzer \
  --repo-url "https://github.com/org/repo" \
  --pr-url "https://github.com/org/repo/pull/123" \
  --jira-tickets "TICKET-123,TICKET-456" \
  --requirements-dir "./impact-analyzer-requirements/" \
  --output "impact-analysis-report.md"

# Run test planning
claude-code-agent test-plan-creator \
  --google-doc "https://docs.google.com/document/d/..." \
  --repo-url "https://github.com/org/repo" \
  --jira-tickets "TICKET-123,TICKET-456" \
  --requirements-dir "./test-plan-requirements/" \
  --output "test-plan-report.md"
```

### Method 2: Direct Usage in Cursor IDE

#### Using Impact Analyzer in Cursor

1. **Open the Agent Template**:
   ```bash
   # Open the impact analyzer template in Cursor
   cursor impact-analyzer.md
   ```

2. **Set Up Your Analysis Context**:
   Create a new file `analysis-context.md`:
   ```markdown
   # Impact Analysis Context
   
   ## Project Information
   - **GitHub Repository**: https://github.com/org/repo
   - **Pull Request**: https://github.com/org/repo/pull/123
   - **Jira Tickets**: 
     - https://company.atlassian.net/browse/TICKET-123
     - https://company.atlassian.net/browse/TICKET-456
   
   ## Analysis Requirements
   - Focus on security implications
   - Include performance impact assessment
   - Consider multi-tenant deployment scenarios
   - Evaluate backward compatibility
   ```

3. **Use Claude Code with the Agent**:
   ```bash
   # In Cursor, use the following prompt:
   ```
   I need to analyze the impact of changes in PR #123. Please use the impact-analyzer agent template and the requirements from the impact-analyzer-requirements directory to generate a comprehensive impact analysis report.
   
   Context:
   - GitHub Repo: https://github.com/org/repo
   - PR: https://github.com/org/repo/pull/123
   - Jira Tickets: TICKET-123, TICKET-456
   
   Please follow the analysis framework and include all required impact categories.
   ```

#### Using Test Planner in Cursor

1. **Open the Agent Template**:
   ```bash
   # Open the test planner template in Cursor
   cursor test-plan-gen-subagent.md
   ```

2. **Set Up Your Test Context**:
   Create a new file `test-context.md`:
   ```markdown
   # Test Planning Context
   
   ## Feature Information
   - **Feature Requirements**: https://docs.google.com/document/d/...
   - **GitHub Repository**: https://github.com/org/repo
   - **Jira Tickets**: 
     - https://company.atlassian.net/browse/TICKET-123
     - https://company.atlassian.net/browse/TICKET-456
   
   ## Test Requirements
   - Include FIPS mode testing
   - Test disconnected cluster scenarios
   - Validate multi-tenant configurations
   - Performance testing required
   ```

3. **Use Claude Code with the Agent**:
   ```bash
   # In Cursor, use the following prompt:
   ```
   I need to create a comprehensive test plan for a new feature. Please use the test-plan-creator agent template and the requirements from the test-plan-requirements directory to generate a detailed test plan.
   
   Context:
   - Feature Requirements: https://docs.google.com/document/d/...
   - GitHub Repo: https://github.com/org/repo
   - Jira Tickets: TICKET-123, TICKET-456
   
   Please include all required test sections and follow the test templates provided.
   ```

## Requirements Directories

### Impact Analyzer Requirements (`impact-analyzer-requirements/`)

This directory contains structured requirements and templates for impact analysis:

- **`analysis-framework.md`**: Defines the analysis methodology and approach
- **`impact-categories.md`**: Lists all impact categories to be evaluated
- **`reporting-templates.md`**: Provides templates for different types of impact reports
- **`README.md`**: Detailed instructions for using the requirements

### Test Plan Requirements (`test-plan-requirements/`)

This directory contains structured requirements and templates for test planning:

- **`test-categories.md`**: Defines all test categories and their requirements
- **`test-environments.md`**: Specifies test environment configurations
- **`test-templates.md`**: Provides templates for different test scenarios
- **`README.md`**: Detailed instructions for using the requirements

## Configuration Options

### Environment Variables

```bash
# GitHub API Configuration
export GITHUB_TOKEN="your-github-token"
export GITHUB_API_URL="https://api.github.com"

# Jira API Configuration
export JIRA_URL="https://company.atlassian.net"
export JIRA_USERNAME="your-jira-username"
export JIRA_API_TOKEN="your-jira-api-token"

# Google Docs Configuration
export GOOGLE_APPLICATION_CREDENTIALS="path/to/credentials.json"

# Agent Configuration
export AGENT_ITERATIONS="5"
export AGENT_OUTPUT_FORMAT="markdown"
export AGENT_LOG_LEVEL="info"
```

### Configuration Files

Create `agent-config.yaml`:
```yaml
agents:
  impact-analyzer:
    enabled: true
    model: "sonnet"
    iterations: 5
    output_format: "markdown"
    requirements_dir: "./impact-analyzer-requirements/"
    
  test-plan-creator:
    enabled: true
    model: "opus"
    iterations: 5
    output_format: "markdown"
    requirements_dir: "./test-plan-requirements/"

api:
  github:
    token: "${GITHUB_TOKEN}"
    base_url: "${GITHUB_API_URL}"
  
  jira:
    url: "${JIRA_URL}"
    username: "${JIRA_USERNAME}"
    api_token: "${JIRA_API_TOKEN}"
  
  google:
    credentials_file: "${GOOGLE_APPLICATION_CREDENTIALS}"

output:
  format: "markdown"
  directory: "./reports/"
  filename_template: "{agent_name}_{timestamp}_{project_name}"
```

## Best Practices

### For Impact Analysis

1. **Always include multiple perspectives**: Technical, business, security, and user experience
2. **Validate assumptions**: Cross-reference information from multiple sources
3. **Prioritize risks**: Use clear risk assessment criteria
4. **Provide actionable recommendations**: Include specific mitigation strategies
5. **Consider deployment scenarios**: Test different deployment configurations

### For Test Planning

1. **Cover all test categories**: Functional, security, performance, boundary, and regression
2. **Include different environments**: Local, cluster-scoped, multi-tenant, FIPS, disconnected
3. **Validate requirements coverage**: Ensure every requirement has corresponding test cases
4. **Consider edge cases**: Include negative testing and error scenarios
5. **Plan for automation**: Identify which tests can be automated

### General Guidelines

1. **Iterate and refine**: Use the 5-iteration process for comprehensive analysis
2. **Cross-reference sources**: Validate information across all input sources
3. **Document assumptions**: Clearly state any assumptions made during analysis
4. **Include context**: Provide sufficient background information
5. **Maintain consistency**: Use consistent terminology and formatting

## Troubleshooting

### Common Issues

1. **API Rate Limiting**:
   ```bash
   # Add delays between API calls
   export AGENT_API_DELAY="1000ms"
   ```

2. **Authentication Errors**:
   ```bash
   # Verify credentials
   curl -H "Authorization: token $GITHUB_TOKEN" https://api.github.com/user
   ```

3. **Missing Requirements**:
   ```bash
   # Check requirements directory structure
   ls -la impact-analyzer-requirements/
   ls -la test-plan-requirements/
   ```

4. **Output Format Issues**:
   ```bash
   # Verify output directory permissions
   mkdir -p ./reports/
   chmod 755 ./reports/
   ```

### Debug Mode

Enable debug logging:
```bash
export AGENT_LOG_LEVEL="debug"
export AGENT_VERBOSE="true"
```

## Examples

### Example Impact Analysis Report

See `examples/impact-analysis-example.md` for a complete example of an impact analysis report generated using these agents.

### Example Test Plan

See `examples/test-plan-example.md` for a complete example of a test plan generated using these agents.

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Update documentation
5. Submit a pull request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Support

For questions and support:
- Create an issue in this repository
- Check the documentation in the requirements directories
- Review the examples in the `examples/` directory

## Changelog

See [CHANGELOG.md](CHANGELOG.md) for a list of changes and version history. 