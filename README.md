# OPA-Gatekeeper

kubectl run weather-app --image=wededo4644/weather-app:88
Error from server (Forbidden): admission webhook "validation.gatekeeper.sh" denied the request: [required-labels] Missing required labels: {"app"}

Error from server (Forbidden): error when creating "test-namespace.yaml": admission webhook "validation.gatekeeper.sh" denied the request: [ns-must-have-labels] Namespace must have labels: {"environment", "owner"}

```
controlplane:~$ vi test-namespace.yaml

controlplane:~$ kubectl apply -f test-namespace.yaml 
Error from server (Forbidden): error when creating "test-namespace.yaml": admission webhook "validation.gatekeeper.sh" denied the request: [ns-must-have-labels] Namespace must have labels: {"environment", "owner"}

controlplane:~$ vi ns-ct.yaml 

controlplane:~$ ls
constraint_template.yaml  filesystem  ns-constraint.yaml  ns-ct.yaml  ns-label.yaml  pod-labels-enforce.yaml  test-namespace.yaml

controlplane:~$ kubectl apply -f ns-constraint.yaml 
nsrequiredlabels.constraints.gatekeeper.sh/ns-must-have-labels created

controlplane:~$ kubectl apply -f test-namespace.yaml 
namespace/test created

controlplane:~$ kubectl get constraints
NAME                                                          ENFORCEMENT-ACTION   TOTAL-VIOLATIONS
k8srequiredlabels.constraints.gatekeeper.sh/required-labels   deny                 11
NAME                                                             ENFORCEMENT-ACTION   TOTAL-VIOLATIONS
nsrequiredlabels.constraints.gatekeeper.sh/ns-must-have-labels   deny                 6

controlplane:~$ kubectl get ConstraintTemplate
NAME                AGE
k8srequiredlabels   37m
nsrequiredlabels    4m58s

```