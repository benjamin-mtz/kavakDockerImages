# Angular Preview

This image is intended to be used as build env for projects that will use the preview deploy service.

## Includes (as of 20/04/2020):

- zip
- git
- jq
- openssh-client
- node lts
- angular 9

## Example:

```yaml
deploy-preview:
  image: kavakci/angular-preview:latest
  script:
    - npm install
    - bash ./deploy-preview.sh
  except:
    - master
    - qa
    - develop
  when: manual
```
