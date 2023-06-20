# Cloud Land 2023

This repository contains a simple go application. 

The directory structure is as follows:
- `ci` - manifests needed for creating the pipeline workflow
- `tekton` - an example tekton pipeline, which is referenced from the files in `ci` 


# How to try the demo?

1. Prerequisites

Flux and Tekton have to be installed on your kubernetes cluster. 

2. Install the additional operators

- Pull Request Operator: 
```
kubectl apply -f https://github.com/jquad-group/pullrequest-operator/releases/latest/download/release.yaml
```
- Pipeline Trigger Operator: 
```
kubectl apply -f https://github.com/jquad-group/pipeline-trigger-operator/releases/latest/download/release.yaml
```

3. Create the personal token for accessing the Github REST API (set status and clone)

    Go to github.com->`Profile`->`Developer Settings`->`Personal Access Tokens`->`Tokens (classic)`->`Generate new token`, and create an access token with the following permissions:

    ![Token](https://github.com/jquad-group/cloudland2023/blob/main/tekton/img/github_token_permissions.png)

4. Replace the string `MY_ACCESS_TOKEN` in https://github.com/jquad-group/cloudland2023/blob/main/tekton/pipeline.yaml#L11 with your newly created token from `3.` 

5. Deploy the example pipeline

```
kubectl apply -f ./tekton/pipeline.yaml
```

6. Deploy everything in the ci directory

```
kubectl apply -f ./ci
```

7. Observe how it works by creating new pull requests and/or new commits