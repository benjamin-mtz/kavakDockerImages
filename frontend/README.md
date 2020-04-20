# Kavak Front

This image is intended to be used as build env for projects that will use the preview deploy service.

## Includes (as of 20/04/2020):

- zip
- git
- jq
- openssh-client
- node

## Example:

```yaml
deploy-preview:
  image: kavakci/frontend:latest
  script:
    - npm install
    - "curl --header 'PRIVATE-TOKEN: $DEPLOY_SCRIPT_TOKEN' 'https://gitlab.com/api/v4/projects/18112726/repository/files/deploy-preview.sh?ref=master' | jq -r '.content' | base64 --decode > deploy-preview.sh"
    - exec ./deploy-preview.sh
  except:
    - master
    - qa
    - develop
  when: manual
```
