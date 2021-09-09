# JSON PATH

Pozwala na parsowanie informacji które zwraca Kubernetes API

Podstawowa składnia:  
`<polecenie_kubectl_get> -o=jsonpath=<zapytanie>`

Przykłady zapytań:  
`kubectl get pods -o=jsonpath= '{.items[0].spec.containers.image}'` - pokazuje wersje image dla pierwszego kontenera w podzie  
`kubectl get node -o=jsonpath='{.items[*].metadata.name}'` - pokazuje wszystkie wartości pola name w podsekcji metadata dla wszystkich obiektów wylistowanych  
`kubectl get nodes -o=jsonpath='{.items[*].status.capacity.cpu}'` - pokazuje ilość cpu przydzielonego do wszystkich nodów  
`kubectl get node -o=jsonpath='{.items[].metadata.name} {.items[].status.capacity.cpu}'` - wyświetla nazwę podów oraz ilość przydzielonch do nich cpu

```text
kubernetes-master kubernetes-worker1 kubernetes-worker2 2 2 2
```

`kubectl get node -o=jsonpath='{.items[*].metadata.name} {"\n"} {.items[*].status.capacity.cpu}'`- wyświetla nazwę podów oraz ilość przydzielonch do nich cpu

```text
kubernetes-master kubernetes-worker1 kubernetes-worker2 
 2 2 2
```

`kubectl get nodes -o=custom-columns=NODE:.metadata.name,CPU:.status.capacity.cpu` - pozwala na nadawanie nazw kolumnom

```text
NODE                 CPU
kubernetes-master    2
kubernetes-worker1   2
kubernetes-worker2   2
```

`kubectl get nodes --sort-by=.metadata.name` - pozwala na sortowanie outputu po podanyej kolumnie

