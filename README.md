# Jira Release action
This action release version & create new version in Jira


- All of sources are from https://github.com/PRNDcompany/jira-release. Just added one property at creating new version.

- Now you can select to create new version automately or not.

## Example Usage

```yaml
name: Jira Release
on:
  push:
    branches: [ main ]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    - name: Extract version name
      run: echo "##[set-output name=version;]$(echo '${{ github.event.head_commit.message }}' | egrep -o '[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}')"
      id: extract_version_name           
    - name: Jira Github Release Automation
      id: release
      uses: Geun-Oh/Jira-Github-Release-Automation@1.1.2     
      with:
        domain: 'My domain'
        project: 'My project'
        version: 'My release version name'
        auth-token: 'My release token'
        create-next-version: false ## can be true
    - name: Print New Version ## when create-next-version option is true
      run: |
        echo ${{ steps.release.outputs.new-version }}
```
