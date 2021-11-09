This a repo to contain the yaml files to deploy the sample flask app from argocd-flask-demo-repo.

Created a write enable ssh key to add to this repo to allow argocd image updater to writeback to this repo.

ssh-keygen -t rsa -b 4096 -f argocd-flask-demo-keys

kubectl create secret generic git-creds \
   --from-file=ssh-privatekey=./argocd-flask-demo-keys \
   --from-file=ssh-publickey=./argocd-flask-demo-keys.pub \
   --dry-run=client -o yaml \
| kubeseal --format yaml  \
| tee ./argocd-flask-demo-deploy/base/deploy-github-cred.yaml
