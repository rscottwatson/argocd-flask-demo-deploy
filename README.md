This a repo to contain the yaml files to deploy the sample flask app from argocd-flask-demo-repo.

Created a write enable ssh key to add to this repo to allow argocd image updater to writeback to this repo.

Sealed Secret is just an example and not really used.
  https://aws.amazon.com/blogs/opensource/managing-secrets-deployment-in-kubernetes-using-sealed-secrets/

ssh-keygen -t rsa -b 4096 -f argocd-flask-demo-keys

kubectl create secret generic git-creds \
   --from-file=sshPrivateKey=../argocd-flask-demo-keys \
   --dry-run=client -o yaml \
| kubeseal --format yaml  \
| tee ./base/deploy-github-cred.yaml

