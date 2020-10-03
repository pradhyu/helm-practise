# values schema 
https://karuppiah7890.github.io/blog/posts/helm-values-schema-gen-plugin/
````
helm plugin uninstall schema-gen
helm plugin install https://github.com/karuppiah7890/helm-schema-gen
install didn't work so i manually cloned it and compiled it with go
helm-schem-gen  values.yml > values.

````


# render notes 
## helm2 way of rendering notest is broken, previous way of -s templates/NOTES.txt --notes 

https://github.com/helm/helm/issues/6901

## work around in helm 3
helm install . --dry-run  --generate-name