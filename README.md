# SecureStack Application Composition Analysis GitHub Action

A GitHub Action to execute SecureStack application composition analysis on an application code repository.  When you add this to GitHub Actions we will analyze your source code for vulnerable third party and open source libraries.  It's like "software composition analysis" but only better!  This Action supports Go, Python and Javascript languages.  See below for what types of issues this action scans for and what files are required.

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
          securestack_api_key: ${{ secrets.SECURESTACK_API_KEY }}
          securestack_app_id: ${{ secrets.SECURESTACK_API_KEY }}
          severity: critical
          language: node
          flags: '--path . --debug'
```

NOTE - to understand possible values for the action input `flags`, run the SecureStack cli locally:

`$ bloodhound-cli code --help`

ADDITIONAL NOTE - Make sure you change the `language: node` to whatever language is in your repo.  SecureStack supports 4 types currently:  `node`, `yarn`, `python` and `go`.  To learn more run the SecureStack CLI locally:

`$ bloodhound-cli code -t --help`

## Create your SecureStack API Key as GitHub Secret

1. Create a [SecureStack](https://app.securestack.com) account using your GitHub credentials.  You get 20 scans for free and you don't need to add a credit card.
2. Once you are logged in go to "Profile" in the black drawer on the left, and then -> GENERATE KEY tab.
3. Generate an API key and copy the value.
4. Go to Settings for your GitHub repository and click on Secrets -> Actions at the bottom left.
5. Create a new secret named SECURESTACK_API_KEY and paste the value from step 2 into the field.

## Retreiving your SecureStack Application ID

1. Log in to [SecureStack](https://app.securestack.com).
2. Open the application you wish to analyse.  If you haven't created a managed application you can follow the directions in this [VIDEO](https://youtu.be/mapgawLMVKg) to create one.  
3. Copy the value of the application id on the View Application screen.
4. Go to Settings for your GitHub repository and click on Secrets -> Actions at the bottom left.
5. Create a new secret named SECURESTACK_APP_ID and paste the value from step 3 into the field.

## Watch this video to learn how to setup your first GitHub Action with SecureStack
[![IMAGE ALT TEXT](http://img.youtube.com/vi/0sYXsCmY2es/0.jpg)](http://www.youtube.com/watch?v=0sYXsCmY2es "Video Title")

## What types of issues does this GitHub Action find?
1. Vulnerable third party libraries from place like NPM, PyPi, and Go repositories
2. Vulnerable open source libraries
3. Libraries and frameworks that have recently had ownership changes or that are malicious

## What files are necessary for this Action to work?
1. For Yarn:  yarn.lock and package.json
2. For NPM: package.json and package-lock.json
3. For Go: go.dep or go.mod
4. For Python: requirements.txt

## Check out our other GitHub Actions:
1. [SecureStack Secrets Analysis](https://github.com/marketplace/actions/securestack-secrets-analysis) - Scan your application for embedded api keys, credentials and senstive data.
2. [SecureStack Web Vulnerability & Cloud Misconfiguration Analysis](https://github.com/marketplace/actions/securestack-web-vulnerability-analysis) - Scan your running application url for cloud misconfigurations and web vulnerabilities.
3. [SecureStack Log4j Analysis](https://github.com/marketplace/actions/securestack-log4j-vulnerability-analysis) - Scan your application for Log4j/Log4Shell vulnerabilities.

## Learn more about SecureStack with our YouTube Channel:
https://www.youtube.com/watch?v=YrPITQNy9UM&list=PL_8Xjyi5rInxzhpQkDRipipmaj0lT6pJ8 

Made with 💜  by [SecureStack](https://securestack.com)

