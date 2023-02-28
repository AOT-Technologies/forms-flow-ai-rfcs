# Title of RFC

| Status        | (Proposed / Accepted / Implemented / Obsolete)       |
:-------------- |:---------------------------------------------------- |
| **RFC PR #**     |  |
| **Author(s)** | Sumesh Kaariyil (sumesh.pk@aot-technologies.com) |


## Objective
Selectively deliver features between public and premium users.

## Motivation


## Proposal

Currently formsflow.ai is single github [repository](https://github.com/aot-technologies/forms-flow-ai). Proposal is to fork the same repository into a closed repository for easy synchronization from open source to premium codebase.


```mermaid
graph TD
  S1[forms-flow-ai OSS] --> C2[Master]
  C2 --> S2[Fork]
  S2 --> S3[forms-flow-ai-ee]
  S3 --> S4[Prem. Master Branch]
  S4 --> C3[Prem. Development Branch]
  C3 --> C4[Prem. Feature branch]
  C4 --> C3
  C3 --> C5[Prem. Release]
  C5 --> C6[Build image]
  C6 --> C8[Push to docker private repo]
  C6 --> C7[Tag release]
  C5 --> S4

  C2 --> O3[OSS Development Branch]
  O3 --> O4[OSS Feature branch]
  O4 --> O3
  O3 --> O5[OSS Release]
  O5 --> O6[Build image]
  O6 --> O9[Push to docker public repo]
  O6 --> O8[Tag release]
  O5 --> O7[Create a PR to Prem.]
  O7 --> S4

```

## Challenges

Maintaining 2 separate codebase comes up with some challenges including;
- Database migration conflicts on merging open source code with premium code.
- Increased testing effort as every release has to be tested on both versions.
- More environments to be set up for dev and test.
- Structuring the code to have less impact on merge/upgrades.
