# Setup Salesforce DX (SFDX) for Sandbox in VSCode

## 1) Download and Install Required Components
    - VSCode
    - VSCode Extension: Salesforce Extension Pack
        - https://marketplace.visualstudio.com/items?itemName=salesforce.salesforcedx-vscode
    - VSCode Extension: Sublime MavensMate Monokai for Apex
        - Use keyword "subc4i" to search for this extension in VSCode
        - https://marketplace.visualstudio.com/items?itemName=SubC4i.sublime-mavensmate-monokai-apex
    - VSCode Extension: Salesforce Package.xml Generator Extension for VS Code
        - https://marketplace.visualstudio.com/items?itemName=VignaeshRamA.sfdx-package-xml-generator
    - Salesforce CLI (Windows 64 for command prompt)

## 2) Create Project
    - Open the Command Palette (press Ctrl+Shift+P on Windows) and run "SFDX: Create Project with Manifest"
    - Type name for project (will also be folder name on hard drive) and press Enter

## 3) Authorize Salesforce Org
    - Open command palette and run "SFDX: Authorize an Org"
    - Type alias name for Salesforce org and press Enter
    - Browser will open and enter your credentials to log into org

## 4) Update package.xml
    - In project folder "manifest", open and edit package.xml file for metadata types
    - Alternatively, use the VSCode extension "Salesforce Package.xml Generator Extension for VS Code" to generate the syntax for you

### Sample package.xml:
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
    - Right-click on package.xml and select "SFDX: Retrieve Source in Manifest from Org"

## 6) Enable Auto-Push/Compile Code on Save
    - In project folder ".vscode", open file "settings.json" and add the following lines:
        - "salesforcedx-vscode-core.push-or-deploy-on-save.enabled": true,
        - "salesforcedx-vscode-core.retrieve-test-code-coverage": true

### Sample settings.json for Salesforce Sanbox folder:
~~~json
{
  "search.exclude": {
    "**/node_modules": true,
    "**/bower_components": true,
    "**/.sfdx": true
  },
  "eslint.nodePath": "c:\\Users\\name\\.vscode\\extensions\\salesforce.salesforcedx-vscode-lwc-46.7.0\\node_modules",
  "workbench.colorTheme": "Sublime MavensMate Monokai",
  "salesforcedx-vscode-core.push-or-deploy-on-save.enabled": true,
  "salesforcedx-vscode-core.show-cli-success-msg": false,
  "salesforcedx-vscode-core.retrieve-test-code-coverage": true
}
~~~