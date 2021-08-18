# Networking

## Network Policy

Pozwala nam definiować zasady na bazie których pod może komunikować się z innymi podami. Domyślnie kubernetes pozwala aby każdy pod mógł komunikować się z każdym podem.

```text
apiVersion: networking.k8s.io/v1 
kind: NetworkPolicy 
metadata: 
  name: <nazwa> 
  namespace: default 
spec: 
  podSelector: 
    matchLabels: 
      <nazwa_labeli>:<wartość:labeli>  # Policy bedzie podłączona do podów o podanych labelach
  policyTypes: 
  - Ingress  # typy network policy jake mają zostać zastosowane. Jeżeli pominiemy to pole zostaną zastosowane tylko te które zostały zdefiniowane
  - Egress 
  ingress: 
  - from: # poniżej opcje na podstawie które możemy zdefiniować z jakiego źródła chcemy pozwalać na ruch wchodzący  
    - ipBlock: 
        cidr: 172.17.0.0/16 
        except: 
        - 172.17.1.0/24 
      namespaceSelector:  # jeżeli chcielibyśmy łączyć selektory np. tylko pod o specyficznych labelach oraz z konkretnego namespace może się łączyć, możemy zrobić to jak tutaj usuwając "-" co działa jak operator OR
        matchLabels: 
          project: myproject 
    - podSelector: 
        matchLabels: 
          role: frontend 
    ports: 
    - protocol: TCP 
      port: 6379 
  egress: 
  - to: 
    - ipBlock: 
        cidr: 10.0.0.0/24 
    ports: 
    - protocol: TCP 
      port: 5978
```

