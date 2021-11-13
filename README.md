# Post Create Hook Example
## My familiarity with helm
Used the default chart template to host my containers.
Switched to using the devspace component-chart for most of my uses.
https://devspace.sh/component-chart/docs/introduction

I use these tools to manage namespaces and contexts
https://github.com/ahmetb/kubectx
https://github.com/jonmosco/kube-ps1

```zsh
minikube start -p hookdemo
(⎈ |hookdemo:default)jon in ~/workspace/helm-post-hook λ kubectl create namespace example                
namespace/example created
(⎈ |hookdemo:default)jon in ~/workspace/helm-post-hook λ kubens example                                  
Context "hookdemo" modified.
Active namespace is "example".
(⎈ |hookdemo:example)jon in ~/workspace/helm-post-hook λ helm install post-hook-example post-hook-example
NAME: post-hook-example
LAST DEPLOYED: Sat Nov 13 10:50:17 2021
NAMESPACE: example
STATUS: deployed
REVISION: 1
NOTES:
1. Get the application URL by running these commands:
  export POD_NAME=$(kubectl get pods --namespace example -l "app.kubernetes.io/name=post-hook-example,app.kubernetes.io/instance=post-hook-example" -o jsonpath="{.items[0].metadata.name}")
  export CONTAINER_PORT=$(kubectl get pod --namespace example $POD_NAME -o jsonpath="{.spec.containers[0].ports[0].containerPort}")
  echo "Visit http://127.0.0.1:8080 to use your application"
  kubectl --namespace example port-forward $POD_NAME 8080:$CONTAINER_PORT
(⎈ |hookdemo:example)jon in ~/workspace/helm-post-hook λ helm list
NAME                    NAMESPACE       REVISION        UPDATED                                 STATUS          CHART                   APP VERSION
post-hook-example       example         1               2021-11-13 10:50:17.185792 -0600 CST    deployed        post-hook-example-0.1.0 1.16.0 
```

Examples taken from.

https://www.golinuxcloud.com/kubernetes-helm-hooks-examples/
./post-hook-example/templates/post-install-hook.yaml

## Follow up on helm conversation
Helm doesn't delete Custom Resource Definitions or Instances of them:
https://helm.sh/docs/chart_best_practices/custom_resource_definitions/#method-1-let-helm-do-it-for-you

post-delete hook reference

https://helm.sh/docs/topics/charts_hooks/#the-available-hooks

I thought the above hook existed and could be used to handle the CRD issue.

## Final Thoughts.
Sorry we had technical issues. I learned something new and I enjoyed showing you my development configuration and project. Thanks :)