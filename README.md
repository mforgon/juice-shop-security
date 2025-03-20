# Juice Shop Security Automation Framework

This repository contains a comprehensive security automation framework for the OWASP Juice Shop application. The system includes automated security scanning, issue tracking, team assignment, and deadline management.

## Overview

The security automation framework provides:

1. **Automated Security Scanning**: Daily scans using multiple security tools
2. **Issue Management**: Automatic creation of GitHub issues for security findings
3. **Team Assignment**: Intelligent assignment of issues to appropriate teams
4. **Deadline Management**: Dynamic deadlines based on severity
5. **Stalled Issue Handling**: Automated reminders and escalation for stalled issues
6. **Meeting Preparation**: Automated preparation of security review meeting agendas
7. **Prioritization**: Automatic prioritization of security issues

## Workflow Components

### 1. Security Scanning (`zap-scan.yml`)

This workflow performs a full security scan of the Juice Shop application using multiple security tools:

- **ZAP Baseline Scan**: Web application vulnerability scanning
- **Trivy**: Container vulnerability scanning
- **SQLMap**: SQL injection detection
- **Nikto**: Web server vulnerability scanning
- **TruffleHog**: Secrets detection

The workflow runs daily and on pushes to the main branch. It generates detailed reports and automatically creates GitHub issues for each finding.

### 2. Issue Management & Prioritization (`issue-management.yml`)

This workflow handles the ongoing management of security issues:

- **Stalled Issue Detection**: Identifies issues with no recent activity
- **Automated Reminders**: Sends reminders for stalled issues
- **Team Reassignment**: Auto-reassigns stalled issues when needed
- **Issue Prioritization**: Automatically applies priority labels (p0-p3)
- **Aging Issue Review**: Schedules reviews for issues open too long

The workflow runs daily to ensure issues don't fall through the cracks.

### 3. Security Review Meeting Preparation (`security-review-meeting.yml`)

This workflow prepares for weekly security review meetings:

- **Issue Analysis**: Analyzes open security issues by deadline and severity
- **Meeting Agenda**: Generates a structured meeting agenda
- **Team Performance Reports**: Tracks resolution metrics by team
- **Deadline Reminders**: Creates reminders for past-deadline issues

The workflow runs weekly before scheduled security meetings.

## Team Configuration

The system uses team configuration files to determine issue assignment:

- `.github/security-team-config.json`: Maps issue types to team assignments and defines deadline rules
- `.github/issue-management-config.json`: Configures stalled issue handling and escalation paths
- `.github/prioritization-config.json`: Defines prioritization rules and review thresholds

## Security Dashboard

The system generates several dashboards and reports:

1. **Security Scan Dashboard**: Overview of latest scan results
2. **Team Performance Report**: Metrics on issue resolution by team
3. **Stalled Issues Summary**: Daily summary of stalled issues
4. **Meeting Agenda**: Weekly meeting preparation document

## Getting Started

### Prerequisites

- GitHub repository with Actions enabled
- Appropriate permissions for issue creation
- GitHub teams configured according to the configuration files

### Setup

1. Copy the workflow files to your `.github/workflows/` directory
2. Update the team configuration files with your team assignments
3. Ensure GitHub Actions has appropriate permissions (issues: write, contents: read)
4. Create the necessary labels in your repository:
   - Severity labels: `CRITICAL`, `HIGH`, `MEDIUM`, `LOW`, `INFORMATIONAL`
   - Priority labels: `p0`, `p1`, `p2`, `p3`
   - Category labels: `security`, `ZAP`, `container`, `secrets`, `sql-injection`, `web-server`
   - Meta labels: `urgent`, `follow-up`, `report`, `review-needed`

## Usage

The system runs automatically on scheduled intervals:

- Security scanning: Daily at midnight UTC
- Issue management: Daily at 1:00 UTC
- Meeting preparation: Weekly on Mondays at 6:00 UTC

You can also trigger any workflow manually using the GitHub Actions interface.

## Customization

### Adjusting Deadlines

Edit the `.github/security-team-config.json` file to modify the default deadline rules:

```json
"severity_deadlines": {
  "CRITICAL": 3,     # 3 days for critical issues
  "HIGH": 7,         # 7 days for high severity
  "MEDIUM": 14,      # 14 days for medium severity
  "LOW": 30,         # 30 days for low severity
  "INFORMATIONAL": 60 # 60 days for informational findings
}
```

### Changing Team Assignments

Edit the team mappings in `.github/security-team-config.json`:

```json
"teams": {
  "web-security": ["@web-security-team", "@devops-team"],
  "container-security": ["@devops-team", "@platform-team"],
  "secrets-management": ["@security-team", "@devops-team"],
  "sql-injection": ["@db-team", "@web-security-team"], 
  "infrastructure-security": ["@devops-team", "@platform-team"]
}
```

## Contributing

Contributions to improve the security automation framework are welcome. Please submit PRs with proposed changes.

## License
