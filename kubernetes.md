# Kubernetes

## Controller vs Operator

> All Operators use the controller pattern, but not all controllers are Operators. It's only an Operator if it's got: controller pattern + API extension + single-app focus.
> 
> Operator is a customized controller implemented with CRD. It follows the same pattern as built-in controllers (i.e. watch, diff, action).

https://stackoverflow.com/questions/47848258/what-is-the-difference-between-a-kubernetes-controller-and-a-kubernetes-operator
