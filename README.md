## WCFC-Apps

### Overview

This GitHub org holds the source code for several apps used by the
Wings of Carolina Flying Club.  The apps are:

* `wcfc-manuals`: Stores the Pilot's Operating Handbooks and other manuals for WCFC airplanes. Allows access by registered members.
* `wcfc-quiz`: Manages a question bank and generates quizzes for initial and recurrent training of WCFC pilots.
* `wcfc-groundschool`: Provides educational materials to enrolled ground school students.
* `wcfc-groups`: Administrative tool used to sync membership between MyFBO, groups.io and the wcfc-manuals app.

The following apps also exist, but are no longer used (or were never used):

* `wcfc-learning`: Learning management system with presentations, events, etc.
* `wcfc-students`: Flight training management system
* `wcfc-squawk`: Aircraft defect management system

Additionally, the following repos store code used internally or for utility purposes:

* `wcfc-backup`: Container image used to perform regular backups of the MongoDB data
* `wcfc-updater`: Container image used for a Google Run Job to redeploy apps after Dependabot updates
* `wcfc-integration-testing`: Container image with Playwright and WireMock, used for running integration tests

### Deployment

These apps are deployed to Google Cloud, under consolidated billing with the club's Google Workspace account.
The applications use a MongoDB database, which is hosted on a MongoDB Atlas Flex instance billed through Google
Cloud Marketplace.  MongoDB admin access is via SSO to Google Workplace.  DNS is hosted on Ionos along with the Club's
main website.

### Diagram

```mermaid
---
config:
    theme: neutral
---
graph LR
    subgraph "Google Cloud"
        secrets[Secrets Manager]
        outbound_ip["Public IP (outbound)<br/>104.197.22.243"]
        inbound_ip["Public IP (inbound)<br/>34.111.135.191"]
        subgraph "Google Cloud Run"
            wcfc-groups[wcfc-groups service]
            wcfc-manuals[wcfc-manuals service]
            wcfc-groundschool[wcfc-groundschool service]
            wcfc-quiz[wcfc-quiz service]
        end
        loadbal[Application Load Balancer]
        iap["Identity-Aware Proxy<br/>(Google SSO login)"]
        registry["Container Registry"]
        manuals_bucket["Cloud Storage Bucket<br/>(manuals)"]
    end

    dns[Ionos DNS]
    mongodb[MongoDB Atlas]

    secrets-->wcfc-groups
    secrets-->wcfc-manuals
    secrets-->wcfc-groundschool
    secrets-->wcfc-quiz
    dns-->inbound_ip
    inbound_ip-->loadbal
    loadbal-->iap
    iap-->wcfc-groups
    loadbal-->wcfc-manuals
    loadbal-->wcfc-groundschool
    loadbal-->wcfc-quiz
    wcfc-groups-->outbound_ip
    wcfc-manuals-->outbound_ip
    wcfc-groundschool-->outbound_ip
    wcfc-quiz-->outbound_ip
    outbound_ip-->mongodb
    manuals_bucket<-->wcfc-manuals
    
    subgraph "GitHub"
        wcfc-groups-repo["wcfc-groups repo"]
        wcfc-manuals-repo["wcfc-manuals repo"]
        wcfc-groundschool-repo["wcfc-groundschool repo"]
        wcfc-quiz-repo["wcfc-quiz repo"]
    end
    wcfc-groups-repo-->registry
    wcfc-manuals-repo-->registry
    wcfc-groundschool-repo-->registry
    wcfc-quiz-repo-->registry
    registry-->wcfc-groups
    registry-->wcfc-manuals
    registry-->wcfc-groundschool
    registry-->wcfc-quiz

    groups-io["groups.io"]
    wcfc-groups-->groups-io
    wcfc-groups-->wcfc-manuals

    slack["Slack"]
    wcfc-quiz-->slack
    wcfc-groundschool-->slack
    wcfc-manuals-->slack


```
