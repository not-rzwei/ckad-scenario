# Scenario Template

This template provides everything needed to create new practice scenarios.

## Template Structure

```
scenarios/
└── [scenario-name]/            # Your new scenario
    ├── README.md               # Scenario-specific README
    └── setup/                  # Initial resources
        ├── namespace.yaml      # MANDATORY
        ├── kustomization.yaml  # MANDATORY
        └── [other-resources].yaml  # As needed for the scenario
```

## How to Create a New Scenario

### 1. Create the Directory Structure
```bash
# Create new scenario directory
mkdir scenarios/[scenario-name]
mkdir scenarios/[scenario-name]/setup

# Copy mandatory template files
cp template/setup/namespace.yaml scenarios/[scenario-name]/setup/
cp template/setup/kustomization.yaml scenarios/[scenario-name]/setup/

# Copy additional resources as needed (deployment, service, configmap, etc.)
cp template/setup/[resource].yaml scenarios/[scenario-name]/setup/
```

### 2. Create the Scenario README
```bash
# Copy the README template
cp template/README-template.md scenarios/[scenario-name]/README.md
```

Then edit `scenarios/[scenario-name]/README.md`:
- Replace `[Scenario Name]` with your scenario name
- Fill in the Overview section
- Write the Background context
- Define the specific task requirements
- Set clear success criteria
- Add verification steps


### 3. Customize the Setup Files
Edit the files in `scenarios/[scenario-name]/setup/`:

- **namespace.yaml**: Change the namespace name (MANDATORY)
- **kustomization.yaml**: Update namespace and add resources (MANDATORY)
- **[other-resources].yaml**: Modify as needed for your scenario


## Scenario Design Guidelines

### Required Sections:
1. **Overview** - What the scenario tests
2. **Background** - Context/situation
3. **Your Task** - Specific requirements
4. **Success Criteria** - What defines success
5. **Verification** - How to test

### Writing Guidelines:
- Keep it concise and focused on the specific scenario
- Don't repeat information from the root README
- Use clear, actionable language
- Include specific commands and examples
- Focus on the task, not general Kubernetes concepts
- Avoid over-explaining - let users figure out the implementation

### Good Scenario Characteristics:
- **Focused**: Tests specific Kubernetes concepts
- **Realistic**: Based on real-world scenarios
- **Progressive**: Builds on previous knowledge
- **Time-bound**: Can be completed in 10-30 minutes
- **Verifiable**: Clear success criteria
