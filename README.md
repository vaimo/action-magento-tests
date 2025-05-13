# GitHub Action For Magento Tests

This action is used to run tests for Magento projects.

# Supported types:

- unit
- integration

# Supported versions

- v1
    - Setup for running tests for Magento projects.
    - Added support for uploading test results to Codacy.

## Compatibility

This action is compatible only with the custom Docker image: [vaimo/image-action-magento](https://github.com/vaimo/image-action-magento).

# Usage

```yaml
jobs:
  code-sniffer:
    runs-on: ubuntu-latest
    container:
      image: ghcr.io/vaimo/image-action-magento:${{inputs.version}}-v1
    steps:
      - name: Tests action
        uses: vaimo/action-magento-tests@v1
        with:
          # Secret variable that stores the contents of auth.json.
          # Required
          composer-auth: ${{secrets.COMPOSER_AUTH}}
          # Directory name that will be used to run action.
          # Optional - if not specified then uses the root directory.
          working-directory: ${{env.working-directory}}
          # Path to the phpunit.xml file.
          # Optional - if not specified then uses the phpunit.xml in the root directory.
          config-path: dev/tests/unit/ci.workflow.phpunit.xml
          # Test suites to be executed.
          # Optional - if not specified then uses the root directory (separated by comma).
          test-suites: Catalog,Checkout,Customer
          # Upload the test results to Codacy. (yes/no)
          # Optional - if not specified then "no" is used.
          upload-to-codacy: yes
          # Codacy project token.
          # Required - if "upload-to-codacy" set to "yes".
          codacy-token: ${{secrets.CODACY_PROJECT_TOKEN}}
```

`