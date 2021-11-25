# Shell Terminal

## Read all pods and write them to yaml file

```console
ns=default
alias kgp='kubectl get pods -n $ns'

kgp | awk -F " " '{print $1}' | sed '1d' | while read line; do echo "getting pod: $line"; kgp $line -o yaml > $line.yaml; done
```

## List Pod name and Node name

```console
kubectl get pod -o=custom-columns=NODE:.spec.nodeName,NAME:.metadata.name
```

[stackoverflow](https://stackoverflow.com/questions/48983354/kubernetes-list-all-pods-and-its-nodes?rq=1)


## Delete certain files from all subfolders

```console
find . -name \*.orig -type f -delete
```

## Get all deployments name in a new line

```console
kubectl get deployments -ojsonpath='{range .items[*]}{.metadata.name}{"\n"}{end}'
```

## Find and Copy files

[stackoverflow](https://stackoverflow.com/questions/5241625/find-and-copy-files)

find from /home/user1/dir1 and copy to /tmp along with source folder structure

```console
find /home/user1/dir1 -name '*2011*.xml' -exec cp --parents {} /tmp  \;
```

## Remove unsed docker images

```console
docker images -q |xargs docker rmi
```

## Remove all stoped container

```console
docker ps -q |xargs docker rm 
```

## Delete all `none` tagged images

```console
docker rmi -f $(docker images | grep "^<none>" | awk '{print $3}')
```

## Access to docker-dektop (mac) vm

run previlige pod `docker run -it --privileged --pid=host debian nsenter -t 1 -m -u -n -i sh`

Follow the link [docker-desktop VM](https://forums.docker.com/t/is-it-possible-to-ssh-to-the-xhyve-machine/17426/3)

## Spinup redis client in kubernetes cluster

```console
kubectl run redis-client  --image=bitnami/redis:latest --restart=Never --rm -it -- sh

redis-cli -h redis-server

Or

redis-cli -h redis-server -a <password> #if AUTH enabled in the server

```

verify server tls cert

```
openssl s_client -connect example.com:443 -showcerts -servername  example.com

# verify finger print
openssl x509 -noout -fingerprint -sha256 -in demo-device3.crt

# verify certificate and kye in sync
openssl x509 -noout -modulus -in cert.crt | openssl md5
openssl rsa -noout -modulus -in privkey.txt | openssl md5
```

git wip in `~/.gitconfig`

```
[core]
	ignorecase = false
[alias]
        wip = for-each-ref --sort='authordate:iso8601' --format=' %(color:green)%(authordate:relative)%09%(color:white)%(refname:short)' refs/heads
[merge]
	tool = vscode
[mergetool "vscode"]
	cmd = code -n --wait $MERGED
[diff]
	tool = vscode
[difftool "vscode"]
	cmd = code --wait --diff $LOCAL $REMOTE
[pull]
	rebase = false
```

