# default-environment-charts

The default git repository used when creating new GitOps based Environments

## Usage

To use this repository for your Jenkins X Environment (Note, old-school, NON jx boot) use this command:

```
jx create env -n <environment-name> \
    -l <environment-label> -s <environment-namespace> \
    -o 200 -p never --vault -b \
    -f https://github.com/joostvdg/default-environment-charts.git
```

## TLS

To enable TLS with minimal effort, for an Jenkins X environments, this fork ships with a Certmanager Certificate Issuer.

If your Jenkins X environment has External-DNS, Ingress, and Certmanager configured (jx boot defaults), you only have to add two annotations to the Ingress resources in this environment.

```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  annotations:
    cert-manager.io/issuer: letsencrypt-prod
    kubernetes.io/tls-acme: "true"
```
