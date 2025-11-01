# Enforcing Documentation Structure: Template-Based Information Architecture

Based on your content type categorization, here are the most effective ways to enforce documentation structure using template-driven Information Architecture:

## 1. **Template-as-Schema Approach**

### **Structured Markdown Templates with Validation**

````markdown
---
template_version: "1.0"
content_type: "release_notes"
owner: "Product Owner (PO)"
required_sections: ["version_info", "new_features", "enhancements", "bug_fixes", "technical_improvements", "breaking_changes"]
validation_rules:
  - heading_hierarchy: true
  - required_metadata: true
  - link_validation: true
---

# Release Notes v{VERSION}

## Metadata
- **Release Date**: {YYYY-MM-DD}
- **Module**: {MODULE_NAME}
- **Owner**: {PRODUCT_OWNER}
- **Status**: {draft|review|published}

## Version Information
<!-- REQUIRED: Brief overview of this release -->

## New Features
<!-- REQUIRED: Features visible to end users -->
### {Feature Name}
- **Description**: {What it does}
- **Benefits**: {Why it matters}
- **Documentation**: [Link to feature docs]

## Enhancements
<!-- REQUIRED: Improvements to existing features -->

## Bug Fixes
<!-- REQUIRED: Issues resolved -->

## Technical Improvements
<!-- REQUIRED: Backend/infrastructure improvements -->

## Breaking Changes
<!-- CONDITIONAL: Required if any breaking changes exist -->

## Migration Guide
<!-- CONDITIONAL: Required if breaking changes exist -->

## Implementation Guides
- [Installation Guide](../installation/)
- [Configuration Guide](../configuration/)
- [User Guide](../user-guide/)
````

## 2. **Multi-Level Enforcement Strategy**

### **Level 1: Template Structure Enforcement**

````python
# validation/template_validator.py
import yaml
import re
from pathlib import Path

class DocumentationValidator:
    def __init__(self, templates_dir: Path):
        self.templates = self.load_templates(templates_dir)
    
    def validate_document(self, doc_path: Path) -> ValidationResult:
        """Validate document against its template"""
        
        # Extract frontmatter
        frontmatter, content = self.parse_document(doc_path)
        
        # Determine content type
        content_type = self.determine_content_type(doc_path, frontmatter)
        
        if content_type not in self.templates:
            return ValidationResult(False, f"No template found for {content_type}")
        
        template = self.templates[content_type]
        
        # Validate structure
        issues = []
        issues.extend(self.validate_required_sections(content, template))
        issues.extend(self.validate_heading_hierarchy(content))
        issues.extend(self.validate_metadata(frontmatter, template))
        issues.extend(self.validate_links(content))
        
        return ValidationResult(len(issues) == 0, issues)
    
    def validate_required_sections(self, content: str, template: dict) -> list:
        """Check if all required sections are present"""
        issues = []
        required_sections = template.get('required_sections', [])
        
        for section in required_sections:
            section_pattern = rf"#{1,6}\s+.*{section.replace('_', '[ _]')}.*"
            if not re.search(section_pattern, content, re.IGNORECASE):
                issues.append(f"Missing required section: {section}")
        
        return issues
````

### **Level 2: Content Type Enforcement**

````yaml
# .mosip-docs/content-types.yml
content_types:
  release_notes:
    owner: "Product Owner (PO)"
    template: "release-notes-template.md"
    required_sections:
      - version_info
      - new_features
      - enhancements
      - bug_fixes
      - technical_improvements
    conditional_sections:
      breaking_changes:
        condition: "has_breaking_changes"
        required_with: ["migration_guide"]
    validation_rules:
      - name: "version_format"
        pattern: "v\\d+\\.\\d+\\.\\d+"
      - name: "date_format"
        pattern: "\\d{4}-\\d{2}-\\d{2}"
    file_patterns:
      - "**/release-notes/*.md"
      - "**/releases/v*.md"

  features:
    owner: "Product Owner (PO)"
    template: "features-template.md"
    required_sections:
      - core_features
      - implementation_guides
    validation_rules:
      - name: "feature_structure"
        pattern: "### .+\\n\\n- \\*\\*.*\\*\\*:"
    file_patterns:
      - "**/features.md"
      - "**/overview/features.md"

  user_guides:
    owner: "Technical Writer (TW)"
    template: "user-guide-template.md"
    required_sections:
      - overview
      - prerequisites
      - step_by_step_instructions
      - troubleshooting
    validation_rules:
      - name: "step_numbering"
        pattern: "\\d+\\. "
    file_patterns:
      - "**/*user-guide*.md"
      - "**/guides/*.md"
````

### **Level 3: Automated Enforcement Pipeline**

````yaml
# .github/workflows/docs-structure-enforcement.yml
name: Documentation Structure Enforcement

on:
  pull_request:
    paths: ['docs/**/*.md']
  push:
    paths: ['docs/**/*.md']

jobs:
  validate-structure:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Setup Documentation Validator
        run: |
          pip install pyyaml markdown
          pip install -e ./tools/docs-validator
      
      - name: Validate Documentation Structure
        run: |
          python tools/docs-validator/validate.py \
            --docs-dir docs/ \
            --templates-dir unsegregated/templates/ \
            --config .mosip-docs/content-types.yml \
            --output validation-report.json
      
      - name: Check for Structure Violations
        run: |
          if [ -s validation-report.json ]; then
            echo "❌ Documentation structure violations found"
            cat validation-report.json
            exit 1
          else
            echo "✅ All documentation follows proper structure"
          fi
      
      - name: Comment on PR with Violations
        if: failure() && github.event_name == 'pull_request'
        uses: actions/github-script@v6
        with:
          script: |
            const fs = require('fs');
            const report = JSON.parse(fs.readFileSync('validation-report.json', 'utf8'));
            
            let comment = '## 📋 Documentation Structure Validation\n\n';
            comment += '❌ **Structure violations found:**\n\n';
            
            for (const file of report.violations) {
              comment += `### ${file.path}\n`;
              for (const issue of file.issues) {
                comment += `- ${issue.severity}: ${issue.message}\n`;
              }
              comment += '\n';
            }
            
            comment += '\n📚 **Please refer to:**\n';
            comment += '- [Documentation Templates](unsegregated/templates/)\n';
            comment += '- [Content Type Guidelines](.mosip-docs/content-types.yml)\n';
            
            github.rest.issues.createComment({
              issue_number: context.issue.number,
              owner: context.repo.owner,
              repo: context.repo.repo,
              body: comment
            });
````

## 3. **VS Code Integration for Real-Time Enforcement**

### **VS Code Extension Configuration**

````json
// .vscode/settings.json
{
  "mosip-docs.templateValidation": {
    "enabled": true,
    "templatesPath": "unsegregated/templates/",
    "configPath": ".mosip-docs/content-types.yml",
    "validateOnSave": true,
    "showInlineErrors": true
  },
  "mosip-docs.contentTypes": {
    "autoDetect": true,
    "suggestTemplate": true,
    "enforceOwnership": true
  }
}
````

### **Custom VS Code Extension Features**

````typescript
// VS Code extension for MOSIP docs enforcement
export class MOSIPDocsValidator {
    
    validateDocument(document: vscode.TextDocument): vscode.Diagnostic[] {
        const diagnostics: vscode.Diagnostic[] = [];
        
        // Detect content type
        const contentType = this.detectContentType(document.fileName);
        
        if (!contentType) {
            return diagnostics;
        }
        
        // Load template requirements
        const template = this.loadTemplate(contentType);
        
        // Validate structure
        const structureIssues = this.validateStructure(document.getText(), template);
        
        structureIssues.forEach(issue => {
            const diagnostic = new vscode.Diagnostic(
                new vscode.Range(issue.line, 0, issue.line, 100),
                issue.message,
                vscode.DiagnosticSeverity.Error
            );
            diagnostics.push(diagnostic);
        });
        
        return diagnostics;
    }
    
    suggestTemplate(document: vscode.TextDocument): void {
        const contentType = this.detectContentType(document.fileName);
        
        if (contentType && document.getText().trim() === '') {
            vscode.window.showInformationMessage(
                `Insert ${contentType} template?`,
                'Yes', 'No'
            ).then(selection => {
                if (selection === 'Yes') {
                    this.insertTemplate(document, contentType);
                }
            });
        }
    }
}
````

## 4. **Template Inheritance System**

### **Base Template with Inheritance**

````markdown
<!-- base-template.md -->
---
template_type: "base"
template_version: "1.0"
---

# {TITLE}

<!-- METADATA_BLOCK -->
<!-- Inherited by all content types -->

<!-- CONTENT_SECTIONS -->
<!-- Specific to each content type -->

<!-- FOOTER_BLOCK -->
## Implementation Guides
<!-- Standard across all content types -->
````

### **Content-Specific Template Inheritance**

````markdown
<!-- release-notes-template.md -->
---
extends: "base-template.md"
template_type: "release_notes"
owner: "Product Owner (PO)"
---

<!-- METADATA_BLOCK -->
- **Release Date**: {YYYY-MM-DD}
- **Module**: {MODULE_NAME}
- **Owner**: {PRODUCT_OWNER}

<!-- CONTENT_SECTIONS -->
## Version Information
## New Features
## Enhancements
## Bug Fixes
## Technical Improvements
## Breaking Changes
## Migration Guide

<!-- FOOTER_BLOCK inherited from base -->
````

## 5. **Benefits of This Approach**

### **For Your MOSIP Documentation:**

1. **Consistent Structure**: Every content type follows its defined template
2. **Quality Assurance**: Automatic validation prevents structural violations
3. **Clear Ownership**: Each content type has a defined owner (PO, TW, Dev, etc.)
4. **Scalable Enforcement**: Works across all modules and content types
5. **Developer-Friendly**: Integrates with existing docs-as-code workflow

### **Implementation Priority:**

1. **Phase 1**: Define templates for your most critical content types (Release Notes, Features, User Guides)
2. **Phase 2**: Set up validation scripts and GitHub Actions
3. **Phase 3**: Create VS Code extension for real-time feedback
4. **Phase 4**: Expand to all content types with inheritance system

## 6. **Content Type Validation Rules**

### **MOSIP-Specific Validation Rules**

````yaml
# .mosip-docs/validation-rules.yml
global_rules:
  - name: "heading_hierarchy"
    description: "Ensure proper heading hierarchy (no skipped levels)"
  - name: "link_validation" 
    description: "Validate all internal and external links"
  - name: "frontmatter_required"
    description: "All documents must have frontmatter"

content_type_rules:
  release_notes:
    - name: "version_in_title"
      pattern: "# Release Notes v\\d+\\.\\d+\\.\\d+"
    - name: "date_format"
      pattern: "\\*\\*Release Date\\*\\*: \\d{4}-\\d{2}-\\d{2}"
    - name: "breaking_changes_warning"
      condition: "contains_breaking_changes"
      required_warning: "⚠️ **Breaking Changes**"
  
  features:
    - name: "overview_section"
      required: true
      pattern: "## Overview"
    - name: "implementation_guides_section"
      required: true
      pattern: "## Implementation Guides"
    - name: "feature_bullet_format"
      pattern: "- \\*\\*[^*]+\\*\\*: .+"
  
  user_guides:
    - name: "prerequisites_section"
      required: true
      pattern: "## Prerequisites"
    - name: "step_numbering"
      pattern: "\\d+\\. "
    - name: "troubleshooting_section"
      required: true
      pattern: "## Troubleshooting"
````

## 7. **Automated Template Generation**

### **Template Generator Script**

````python
# tools/template-generator.py
import yaml
from pathlib import Path
from jinja2 import Template

class TemplateGenerator:
    def __init__(self, config_path: Path):
        self.config = yaml.safe_load(config_path.read_text())
    
    def generate_template(self, content_type: str, output_path: Path):
        """Generate a template file for a content type"""
        
        if content_type not in self.config['content_types']:
            raise ValueError(f"Unknown content type: {content_type}")
        
        content_config = self.config['content_types'][content_type]
        
        # Load base template if inheritance is used
        base_template = None
        if 'extends' in content_config:
            base_template = self.load_base_template(content_config['extends'])
        
        # Generate template content
        template_content = self.build_template_content(content_config, base_template)
        
        # Write to file
        output_path.write_text(template_content)
    
    def build_template_content(self, config: dict, base_template: str = None) -> str:
        """Build the template content based on configuration"""
        
        # Start with frontmatter
        frontmatter = {
            'template_version': '1.0',
            'content_type': config.get('content_type'),
            'owner': config.get('owner'),
            'required_sections': config.get('required_sections', [])
        }
        
        content = "---\n"
        content += yaml.dump(frontmatter, default_flow_style=False)
        content += "---\n\n"
        
        # Add title placeholder
        content += f"# {{{config.get('title_placeholder', 'TITLE')}}}\n\n"
        
        # Add required sections
        for section in config.get('required_sections', []):
            section_title = section.replace('_', ' ').title()
            content += f"## {section_title}\n"
            content += f"<!-- REQUIRED: {section.replace('_', ' ')} -->\n\n"
        
        # Add conditional sections
        for section, conditions in config.get('conditional_sections', {}).items():
            section_title = section.replace('_', ' ').title()
            content += f"## {section_title}\n"
            content += f"<!-- CONDITIONAL: {conditions.get('condition', '')} -->\n\n"
        
        # Add footer from base template if inherited
        if base_template:
            content += "\n<!-- FOOTER_BLOCK inherited from base -->\n"
        
        return content
````

This template-driven approach ensures that your Information Architecture is not just documented but actively enforced throughout the documentation lifecycle, maintaining consistency and quality across your entire MOSIP documentation ecosystem.