## `cdx:k8s` Namespace Taxonomy

| Namespace | Description |
| --- | --- |
| `cdx:k8s:component` | Namespace for metadata of [Kubernetes components](https://kubernetes.io/docs/concepts/overview/components/). |

## `cdx:k8s:component` Namespace Taxonomy

| Property | Description |
| --- | --- |
| `cdx:k8s:component:type` | Type of the [Kubernetes component](https://kubernetes.io/docs/concepts/overview/components/). Well-known roles are "controlPlane", "node" |
| `cdx:k8s:component:name` | Name of the [Kubernetes component](https://kubernetes.io/docs/concepts/overview/components/). Well-known names are "kube-apiserver", "kube-scheduler", kube-controller-manager", "cloud-controller-manager", "kubelet", "kube-proxy", "dashboard", "cni", "csi" |
