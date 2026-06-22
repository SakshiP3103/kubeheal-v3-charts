# KubeHeal Helm charts

Helm chart repository for [KubeHeal](https://github.com/SakshiP3103/Kubeheal-v3) —
a GitOps-aware Kubernetes incident intelligence agent.

The chart **source** lives in the main (private) app repo under `deploy/helm/kubeheal`;
this public repo hosts the **packaged** charts so they can be served over GitHub Pages.

## Usage

```bash
helm repo add kubeheal https://sakship3103.github.io/kubeheal-v3-charts
helm repo update
helm search repo kubeheal

helm install kubeheal kubeheal/kubeheal -n kubeheal --create-namespace \
  --set image.repository=<your-dockerhub-id>/kubeheal-v3 \
  --set image.tag=latest \
  --set imagePullSecrets[0].name=dockerhub-creds \
  --set secrets.existingSecret=kubeheal-secrets \
  --set config.githubOrg=YOUR_ORG
```

## Publishing a new version

From the app repo, after bumping `version:` in `Chart.yaml`:

```bash
helm package deploy/helm/kubeheal -d ../kubeheal-v3-charts
helm repo index ../kubeheal-v3-charts --url https://sakship3103.github.io/kubeheal-v3-charts
cd ../kubeheal-v3-charts && git add . && git commit -m "Publish kubeheal-<version>" && git push
```
