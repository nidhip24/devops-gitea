# cdevops-gitea
k8s gitea lab to take dev (sqlite based) to prod (mysql based)

TLDR;


## Run the Application

1. Run the ansible playbook

```bash
cd prod && ansible-playbook up.yaml
```

2. Once you have made it through the `up.yaml` playbook you can forward the port:

```bash
kubectl port-forward svc/gitea-http 3000:3000
```

3. Expose gitea publicly using Ngrok

```bash
kubectl apply -f ngrok/
```

If you run into any problem follow below troubleshooting methods


## Troubleshooting

1. Make sure that docker is running by doing `docker ps` until it shows 

```
CONTAINER ID   IMAGE                            COMMAND                  CREATED         STATUS         PORTS                             NAMES

```

2. run `ansible-playbook --version` to see if you have ansible. If not run:

```bash
bash <(curl -Ls https://raw.githubusercontent.com/conestogac-acsit/cdevops-bootstrap/refs/heads/main/bootstrap.sh)
```

3. run `kubectl get ns default` to see if you have a cluster. The expected result is:

```
NAME      STATUS   AGE
default   Active   29m
```

If you have another result try installing a k8s cluster:

```bash
bash <(curl -Ls https://raw.githubusercontent.com//conestogac-acsit/cdevops-bootstrap/refs/heads/main/k8s.sh)
```
