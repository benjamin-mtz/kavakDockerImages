# Apolo

This images is intended to be used in Apolo CI

## Includes (as of 20/04/2020):

- gcc
- zip
- git
- python-dev
- python-setuptools
- python
- python-pip
- curl
- awsebcli
- awscli
- @angular/cli

## Example:

```yaml
buildStage:
  image: kavakci/apolo:latest
  script:
    - npm install
    ....
```
