# SecureStack GitHub Actions

A GitHub Action to execute SecureStack application composition analysis on an application code repository.  When you add this to GitHub Actions we will analyze your source code for vulnerable third party and open source libraries.  It's lik "software composition analysis" but only better!  This Action supports Go, Python and Javascript languages.  See below for what types of issues this action scans for and what files are required.

```
name: Example Workflow Using SecureStack Application Composition Analysis Action
on: push
jobs:
  security:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repo for running code analysis within workflow
        id: checkout
        uses: actions/checkout@v2.4.0
        with:
          fetch-depth: 0
      - name: Code Analysis Step
        id: code
        uses: SecureStackCo/actions-code@main
        with:
          securestack_api_key: ${{ secrets.SECURESTACK_API_KEY_SECRET }}
          securestack_app_id: '<Application ID>'
          severity: critical
          language: node
          flags: '--path . --debug'
```

NOTE - to understand possible values for the action input `flags`, run the SecureStack cli locally:

`$ bloodhound-cli code --help`

## Create your SecureStack API Key and save as GitHub Secret

1. Log in to [SecureStack](https://app.securestack.com) and go to the Profile -> GENERATE KEY screen.
2. Generate an API key and copy the value.
3. Go to Settings for your GitHub repository and click on Secrets at the bottom left.
4. Create a new secret named SECURESTACK_API_KEY_SECRET and paste the value from step 2 into the field.

## Retreiving your SecureStack Application ID

1. Log in to [SecureStack](https://app.securestack.com).
2. Open the application you wish to analyse.
3. Copy the value of the application id on the View Application screen.
4. Paste into the value of the `securestack_app_id` action input for the step using the SecureStack action in your workflow.

## What types of issues does this GitHub Action find?
1. Vulnerable third party libraries from place like NPM, PyPi, and Go repositories
2. Vulnerable open source libraries
3. Libraries and frameworks that have recently had ownership changes or that are malicious

## What files are necessary for this Action to work?
1. For Yarn:  yarn.lock and package.json
2. For NPM: package.json and package-lock.json
3. For Go: go.dep or go.mod
4. For Python: requirements.txt

Made with 💜  by [SecureStack](https://securestack.com)

