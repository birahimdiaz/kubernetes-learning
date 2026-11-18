# Lesson 6 — Kubernetes Persistent Storage

## Objective
Understand how Kubernetes manages persistent application data using Volumes, PersistentVolumes (PV), PersistentVolumeClaims (PVC), and StorageClasses.

## Concepts Learned
- **Volume:** Makes storage available inside a container.
- **PV:** Represents storage in the cluster.
- **PVC:** Requests persistent storage.
- **StorageClass:** Defines how storage is dynamically provisioned.
- **ReadWriteOnce:** Allows read-write mounting by one node at a time.
- **Reclaim Policy:** Determines what happens to storage after PVC deletion (`Delete` or `Retain`).

## Hands-on Lab

1. Created a PVC requesting 1Gi of storage.
2. Deployed Nginx with a mounted PVC.
3. Wrote a file inside `/usr/share/nginx/html`.
4. Deleted the Pod and verified data persistence.
5. Learned that files outside the mounted volume are not persistent.
6. Explored storage reclaim policies.

## Commands

```bash
kubectl get storageclass
kubectl apply -f pvc.yaml
kubectl apply -f nginx-deployment.yaml
kubectl get pvc
kubectl get pv
kubectl get pods
kubectl delete pod -l app=nginx-storage
```

## Key Takeaway

Pods are ephemeral, but PersistentVolumes allow applications to preserve data across Pod recreation.

Deleting a Deployment does not automatically delete its PVC.
