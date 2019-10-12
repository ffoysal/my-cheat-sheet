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
