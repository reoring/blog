---
template: BlogPost
path: /kubernetes/rbac
date: 2020-12-15T08:44:58.971Z
title: KubebuilderでCore API GroupのSecretsにアクセスするRBACのRoleを生成するMarkerを指定する方法
---
```go
// +kubebuilder:rbac:groups=core,resources=secrets,verbs=get;list;watch
```

verbsには、`get`, `list`, `watch` の3つを指定する必要がある。

## 生成されるYAML

```yaml:config/rbac/role.yaml
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  creationTimestamp: null
  name: manager-role
rules:
- apiGroups:
  - ""
  resources:
  - secrets
  verbs:
  - get
  - list
  - watch
```
