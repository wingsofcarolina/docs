## Secrets Remediation

Many secrets were hardcoded in the original versions of these apps.  Each of
these needs to be fixed in the code, and also have the secret itself
revoked/rotated.  This document tracks the status of this effort.

### AWS
- wcfc-groundschool/misc/dfrye\_accessKeys.csv
    - [ ] code fixed
    - [ ] credential revoked
- wcfc-groundschool/src/main/resources/credentials-wcfc
    - [ ] code fixed
    - [ ] credential revoked
- wcfc-manuals/src/main/resources/credentials-wcfc
    - [X] code fixed
    - [ ] credential revoked
- wcfc-students/src/main/resources/credentials-wcfc
    - (obsolete app - no code fix)
    - [ ] credential revoked

### MongoDB
- wcfc-groups/launch
    - [X] code fixed
    - [ ] credential revoked

### Slack
- wcfc-groundschool/src/main/java/org/wingsofcarolina/gs/resources/GsResource.java
    - [ ] code fixed
    - [ ] credential revoked
- wcfc-groundschool/src/main/java/org/wingsofcarolina/gs/slack/SlackAuthService.java
    - [ ] code fixed
    - [ ] credential revoked
- wcfc-manuals/src/main/java/org/wingsofcarolina/manuals/slack/SlackAuthService.java
    - [X] code fixed
    - [ ] credential revoked
- wcfc-quiz/src/main/java/org/wingsofcarolina/quiz/resources/Slack.java
    - [ ] code fixed
    - [ ] credential revoked
- wcfc-students/deployment/slack
    - (obsolete app - no code fix)
    - [ ] credential revoked
- wcfc-students/src/main/java/org/wingsofcarolina/students/slack/SlackAuthService.java
    - (obsolete app - no code fix)
    - [ ] credential revoked

### WCFC\_TOKEN
- wcfc-groups/src/main/java/org/wingsofcarolina/groups/http/ManualsService.java
    - [X] code fixed
    - [ ] credential revoked
- wcfc-manuals/src/main/java/org/wingsofcarolina/manuals/resources/MembersResource.java
    - [X] code fixed
    - [ ] credential revoked

### Groups.io
- wcfc-groups/src/main/java/org/wingsofcarolina/groups/server/UpdateHandler.java
    - [X] code fixed
    - [ ] credential revoked

### Google OAuth token
- wcfc-learning/src/main/resources/credentials.json
- wcfc-learning/src/main/resources/StoredCredential
    - (obsolete app - no code fix)
    - [ ] credential revoked

### Hardcoded JWT master key
- wcfc-groundschool/src/main/java/org/wingsofcarolina/gs/authentication/AuthUtils.java
    - [ ] code fixed
    - [ ] credential revoked
- wcfc-manuals/src/main/java/org/wingsofcarolina/quiz/authentication/AuthUtils.java
    - [X] code fixed
    - [ ] credential revoked
- wcfc-quiz/src/main/java/org/wingsofcarolina/quiz/authentication/AuthUtils.java
    - [ ] code fixed
    - [ ] credential revoked

