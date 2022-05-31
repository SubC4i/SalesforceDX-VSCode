# Setup Salesforce IDE for Sandbox in VSCode
Works with both production and sandbox instances. Replaces MavensMate IDE for Salesforce development.

## 1) Download and Install Required Components
- VSCode
    - https://code.visualstudio.com/Download
- VSCode Extension: `Salesforce Extension Pack`
    - https://marketplace.visualstudio.com/items?itemName=salesforce.salesforcedx-vscode
- VSCode Extension: `Sublime MavensMate Monokai for Apex`
    - https://marketplace.visualstudio.com/items?itemName=SubC4i.sublime-mavensmate-monokai-apex
- VSCode Extension: `Salesforce Package.xml Generator Extension for VS Code`
    - https://marketplace.visualstudio.com/items?itemName=VignaeshRamA.sfdx-package-xml-generator
- Salesforce CLI (Windows 64 for command prompt)
    - https://developer.salesforce.com/tools/sfdxcli

## 2) Create Project
- Open the Command Palette (press Ctrl+Shift+P on Windows) and run `SFDX: Create Project with Manifest`
- Select `Standard` and press Enter
- Type name for project (will also be folder name on hard drive) and press Enter
- Select folder location (project files will be created in a new folder within the location you choose)

## 3) Authorize Salesforce Org
- Open Command Palette and run `SFDX: Authorize an Org`
- Type alias name for Salesforce org and press Enter
- Browser will open and enter your credentials to log into org

## 4) Update package.xml
- In project folder `manifest`, open and edit package.xml file for metadata types
- Alternatively, use the VSCode extension `Salesforce Package.xml Generator Extension for VS Code` to generate the syntax for you
    - Easiest way to pull metadata where the wildcard (*) symbol is not allowed
    - Certain metadata must be populated in the package.xml with explicit names
    - Example: For Dashboards, you must list the name of every dashboard you want to retrieve in order for it to be pulled from the source org
- Recommended metatdata types to include: `ApexClass, ApexComponent, ApexEmailNotifications, ApexPage, ApexTestSuite, ApexTrigger, AssignmentRule, AssignmentRules, AuraDefinitionBundle, CustomField, CustomMetadata, CustomObject, CustomPageWebLink, Dashboard, DuplicateRule, EmailTemplate, FlexiPage, Flow, FlowCategory, FlowDefinition, HomePageComponent, HomePageLayout, Layout, LightningBolt, LightningComponentBundle, MatchingRule, MatchingRules, Report, SharingCriteriaRule, SharingOwnerRule, SharingRules, StaticResource, ValidationRule, Workflow, WorkflowAlert, WorkflowFieldUpdate, WorkflowRule, WorkflowTask`

    ### Sample `package.xml`:
    ~~~xml
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <Package xmlns="http://soap.sforce.com/2006/04/metadata">
        <types>
            <members>*</members>
            <name>ApexClass</name>
        </types>
        <types>
            <members>*</members>
            <name>ApexComponent</name>
        </types>
        <types>
            <members>*</members>
            <name>ApexPage</name>
        </types>
        <types>
            <members>*</members>
            <name>ApexTestSuite</name>
        </types>
        <types>
            <members>*</members>
            <name>ApexTrigger</name>
        </types>
        <version>46.0</version>
    </Package>
    ~~~

## 5) Retrieve Metadata
- Right-click on package.xml and select `SFDX: Retrieve Source in Manifest from Org`

## 6) Enable Auto-Push/Compile Code on Save
- In project folder `.vscode`, open file `settings.json` and add the following lines:
    - ` "salesforcedx-vscode-core.push-or-deploy-on-save.enabled": true, `

## 7) Enable Running Test Classes
- In project folder `.vscode`, open file `settings.json` and add the following lines:
    - ` "salesforcedx-vscode-core.retrieve-test-code-coverage": true `
    ### Sample `settings.json`:
    ~~~json
    {
    "search.exclude": {
        "**/node_modules": true,
        "**/bower_components": true,
        "**/.sfdx": true
    },
    "workbench.colorTheme": "Sublime MavensMate Monokai",
    "salesforcedx-vscode-core.push-or-deploy-on-save.enabled": true,
    "salesforcedx-vscode-core.show-cli-success-msg": false,
    "salesforcedx-vscode-core.retrieve-test-code-coverage": true
    }
    ~~~
