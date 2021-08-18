# Scheduling

## Ręczne przypisanie poda do konkretnego noda

Działa nawet jeżeli scheduler jest nie dostępny, omija taints,tolerations oraz affinity.

```text
apiVersion: v1 
kind: Pod 
metadata: 
 name: nginx 
 labels: 
  name: nginx 
spec: 
 containers: 
 - name: nginx 
   image: nginx 
   ports: 
   - containerPort: 8080 
 nodeName: node02
```

