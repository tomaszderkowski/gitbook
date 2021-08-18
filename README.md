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

## Przydatne polecenia

`ip a | ip addr | ip link` - pokazuje ustawienia wszystkich interfejsów sięciowych

`route | ip route show | ip route list` - pokazuje tablice routingu na danej maszynie

`ip route add default via <ip_adres>` - dodaje domyślną brame sieciową na podany adres

`ip route add  via <ip_adres>` - dodaje nową brame dla podanej sieci

{% hint style="info" %}
ip\_forward - domyślnie w systemach linux routing pomiedzy interfejsami sieciowymi jest wyłączony aby włączyć go należy
{% endhint %}

```text
$ echo 1 > /proc/sys/net/ipv4/ip_forward #tymczasowe rozwiązanie, działające do restartu maszyny

$ cat /etc/sysctl.conf # pernamętne rozwiązanie
# Uncomment the line
net.ipv4.ip_forward=1
```

`sysctl -a` - pokazuje wszystkie ustawienia sysctl

`sysctl --system` - przeładowywuje ustawienia po zmianie

dig 

nslookup

## Serwisy

Rodzaje serwisów

* ClusterIP - type serwisu odstępny tylko z wnętrza klastra, nie dostępny z zewnątrz.
* NodePort - działa na takie zasadzie jak ClusterIP z tą różnicą, że wystawia się również na zdefiniowanym porcie na każdej z maszyn w obrębie klastra, przez co jest również dostępny z zewnątrz
* LoadBalancer

## DNS

`service-name.namespace.svc.cluster.local` - schemat nazw dns dla serwisów 

`pod-ip.namespace.pod.cluster.local` - schemat nazw dns dla podów, gdzie z w adresie ip zamieniane są kropki na myślinki

## 

