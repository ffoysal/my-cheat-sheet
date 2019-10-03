# Shell Terminal

## Read all pods and write them to yaml file

```console
ns=default
alias kgp='kubectl get pods -n $ns'

kgp | awk -F " " '{print $1}' | sed '1d' | while read line; do echo "getting pod: $line"; kgp $line -o yaml > $line.yaml; done
```
