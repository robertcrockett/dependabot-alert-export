# dependabot-alert-export
Export the Dependabot alerts as CSV file from a repo with filepath 

This GitHub action helps to export the Dependabot alerts to a CSV file. One can define a workflow to run or triger based on specific event to capture all Dependabot alerts to a CSV file for further analysis. 

https://registry.npmjs.org/

## Release
GitHub Marketplace : https://github.com/marketplace/actions/dependabot-alert-csv-export

# Local Testing
For local testing of the action, there are 4 environment variables required. Each of these can be exported with a prefix of INPUT.
```
export INPUT_GITHUB_TOKEN='{Your PAT Token}'
export INPUT_org_name='{org_name}'
export INPUT_repo_name='{repo_name}'
export INPUT_csv_path='{csv_path}'
```

# How to Use the Action

## PAT Token
Create a PAT token to get access to the Dependabot alerts. Pass this token as an input to the action - GITHUB_TOKEN


## action in workflow

Include the dependabot-alert-export action in your workflow. 

Following is the sample code for integrating this action with your workflow

```
steps:               
      - name: Dependabot Alert CSV Export
        uses: ShamKarthikS-Hexaware/dependabot-alert-export@v1.0
        with:        
          GITHUB_TOKEN: ${{secrets.GH_TOKEN}}
          org_name: 'ORG_NAME'
          repo_name: 'REPO_NAME'
          csv_path: data/vulnerability.csv
          
      - name: Upload Vulnerability report
        uses: actions/upload-artifact@v3
        with:
           name: vulnerability_report
           path: data/vulnerability.csv          
```

## Parameters

| Name                           | Required  | Description                                                                      |
|--------------------------------|------------|----------------------------------------------------------------------|
| GITHUB_TOKEN                 | Yes | PAT Token for access    |
| org_name                       | Yes | GitHub Organization Name                                      |
| repo_name                   | Yes | GitHub Repository Name     |
| csv_path                       | Yes | CSV file path                                   |

## Exported Fields
Following fields are included in the Vulnerability Report
- Vulnerability Id
- Dependency Scope (`DEVELOPMENT` or `RUNTIME`)
- State (`DISMISSED`, `FIXED` or `OPEN`)
- Created At
- Manifest File Name
- Vulnerability Version Range
- Package Name
- GHSA Id (The ID of the vulnerability in the [GitHub Security Advisory Database](https://github.com/advisories))
- Severity
- Summary
- Link
- Description
- Dismissed At (for Dismissed alerts)
- Dismiss Reason
- Dismiss Comment
- Fixed At (for Fixed alerts)
- Fix Reason

## Report
Vulnerability report in CSV format will be available as part of the build artifacts for download

<img width="792" alt="Screenshot 2022-09-18 at 1 23 26 PM" src="https://user-images.githubusercontent.com/10282550/190891852-13c25b39-3779-4754-a2e5-7f431b2807c4.png">

# License

The scripts and documentation in this project are released under the [MIT License](https://github.com/actions/download-artifact/blob/main/LICENSE)


