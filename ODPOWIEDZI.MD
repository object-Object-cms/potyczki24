# Zadanie 1

Stworzyłem projekt web-server:
```
$ rancher project create web-server
```
Przełączyłem kontekst na web-server
```
$ rancher context switch web-server
```
Stworzyłem namespace za pomocą kubectl'a
```
$ rancher kubectl create namespace nginx
```
Stworzyłem zestaw deployment z 3 replikami, serwisem pozwalającym na dostęp z całego klastra i ingressem pozwalający na dostęp z internetu
```
$ kubectl apply -f zad1.yaml
```
Dostępne pod: `http://nginx.193.187.69.136.sslip.io`

# Zadanie 2
1. Prerequisites:
- zainstalowane containerd w wersji v1.7.11
- zainstalowane kubernetes v1.26.13
- bash, curl, findmnt, grep, awk i blkid są zainstalowane
- brakuje open-iscsi
- instalacja za pomocą zyppera
  `sudo zypper install open-iscsi`
- włączenie serwisu iscsi
  `sudo systemctl enable --now iscsid`
2. Instalacja, wybranie default storage class i ustawienie replik na 1
3. Wszystkie pody są aktywne
```
NAME                                                READY   STATUS    RESTARTS        AGE
csi-attacher-5859bc989f-4xjtb                       1/1     Running   0               7m5s       
csi-attacher-5859bc989f-9pb4v                       1/1     Running   0               7m5s       
csi-attacher-5859bc989f-gx9rb                       1/1     Running   0               7m5s       
csi-provisioner-c7ffcc5cc-gktcf                     1/1     Running   0               7m4s       
csi-provisioner-c7ffcc5cc-p8c5t                     1/1     Running   0               7m4s       
csi-provisioner-c7ffcc5cc-xtgxm                     1/1     Running   0               7m5s       
csi-resizer-777857494b-jdh5p                        1/1     Running   0               7m4s       
csi-resizer-777857494b-jh9cj                        1/1     Running   0               7m4s       
csi-resizer-777857494b-qmj52                        1/1     Running   0               7m4s       
csi-snapshotter-64cdff5bb4-g6xqh                    1/1     Running   0               7m4s       
csi-snapshotter-64cdff5bb4-hklvd                    1/1     Running   0               7m4s       
csi-snapshotter-64cdff5bb4-ksjcg                    1/1     Running   0               7m4s       
engine-image-ei-933d45a5-mbg28                      1/1     Running   0               7m28s      
instance-manager-12662523553b77548349eb5a415428a4   1/1     Running   0               7m28s      
longhorn-csi-plugin-m7n56                           3/3     Running   0               7m4s       
longhorn-driver-deployer-c77dd9cd6-klf45            1/1     Running   0               8m22s      
longhorn-manager-q76xp                              1/1     Running   1 (7m42s ago)   8m22s      
longhorn-ui-77ddf5bdf-rfj9h                         1/1     Running   0               8m22s      
longhorn-ui-77ddf5bdf-xfxd2                         1/1     Running   0               8m22s      
```

# Zadanie 3

W rancher web UI, otworzyłem cluster potyczki, sekcja Apps, Repositories, Create, wprowadziłem nazwę i URL.

W zakładce Apps, charts wyszukałem "tetris" i zainstalowem aplikację. Jako hostname podałem `tetris.193.187.69.136.sslip.io`.

Aplikacja działa

# Zadanie 4

W zakładce Apps, charts wyszukałem NeuVector i go zainstalowałem. Jest dostępny pod adresem https://193.187.69.136.sslip.io:31824/
Aby ingress zadziałał, dodaję annotacje

```
$ rancher kubectl annotate --namespace cattle-neuvector-system ingress neuvector-webui-ingress nginx.ingress.kubernetes.io/backend-protocol="HTTPS"
```

Teraz jest także dostępny pod https://neuvector.193.187.69.136.sslip.io/

Zalogowałem się za pomocą defaultowych danych - admin, admin.

Włączyłem Auto-Scan - przełącznik na górze ekranu.

# Zadanie 5

W zakładce "Assets" > "Registries" dodałem rejestr "https://registry.hub.docker.com" z filtrem "nvbeta/*" i rozpocząłem scan.

Projektem o największej liczbie podatności to nvbeta/node:latest - jest w nim 1294 danger i 824 warning.

# Zadanie 6
PVC nie usuwa się podczas skalowania

Aby użyć provisioning z longhorna dodaje `storageClassName: longhorn`

Aplikuje na klaster
```
$ rancher kubectl apply -f nie-usuwaj.yaml
```
Uruchamiam `sh` w podzie i zapisuje testowe pliki
```
$ rancher kubectl exec --stdin --tty ubuntu-5ffb86755d-ht4zv -- /bin/sh
/shared_files # ls
lost+found
/shared_files # echo test > plik
/shared_files # cat plik
test
/shared_files #
```
Skaluje deployment do 0
```
$ rancher kubectl scale deployment ubuntu --replicas 0
...
NAME     READY   UP-TO-DATE   AVAILABLE   AGE
ubuntu   0/0     0            0           4m12s
```
Skaluje z powrotem do 1
```
$ rancher kubectl scale deployment ubuntu --replicas 1
...
NAME     READY   UP-TO-DATE   AVAILABLE   AGE
ubuntu   1/1     1            1           5m11s
```
Uruchamiam `sh` w nowym podzie i weryfikuje, że pliki nadal się tam znajdują
```
$ rancher kubectl exec --stdin --tty ubuntu-5ffb86755d-rxbfr -- /bin/sh
/ # cd shared_files/
/shared_files # ls
lost+found  plik
/shared_files # cat plik
test
/shared_files #
```

# Zadanie 7

Aby odczytać YAMLa jakiegoś resource'a można:

- Użyć Rancher UI:

    * Znaleść resource w UI - na przykład Pods -> tetris.
    * W rogu strony, kliknąć na menu "..." w pionie, poten "Edit YAML" - YAML zostanie ukazany

- Użyć kubectl przez Rancher CLI

    * Znaleść resource przez CLI - na przykład `rancher kubectl get pods`
    * Odczytać YAMLa tego resource'a - `rancher kubectl get pod -o yaml <nazwa poda>`

# Zadanie

Uruchamianie MySQLa na ustawieniach standardowych będzie definitywnie prostrze i szybsze od konfigurowania go ręcznie, jednak może być związane z pogorszonym bezpieczeństwem bazy danch.

Baza uruchomiona w ten właśnie sposób nie będzie także wyoptymalizowana do konkretnego use-case'u tej aplikacji.

Zaleca się konfigurację ręczną, po poprzednim przeczytaniu dokumentacji. 

# Zadanie 8

Gateway jest nową alternatywą dla ingressa. Pozwala na upublicznienie serwisów działających w klastrze na publiczne adresy. Przesyła dane pomiędzy siecią zewnętrzną a serwisami w klastrze.

# Zadanie 9

Deployment zarządza cyklem życia aplikacji w Kubernetes, w tym wdrażaniem, aktualizacjami i rollbackami. Deployment wykorzystuje ReplicaSety. ReplicaSety pozwalają kontrolować ilość replik (instancji) w klastrze.

# Zadanie 10

W Rancher UI, wchodzę w "Cluster Management" i przy potyczki klikam w "Edit Config". Zmieniam Kubernetes version na najnowszą i klikam "Save".

# Zadanie 11
Stworzenie dwóch użtkowników loalnych
- muhammed.yassuff (Manager IT)
- muhhamad.yussuff (Praktykant)

Manager dostał role 'looking' na klustrze potyczki, nie może czytać sekretów
Praktykant dostał role 'Cluster Owner' na projekcie web-server

# Zadanie 12

Adrian jest winny - przydzielił on zbyt mało pamięci RAM dla MySQLa. Pobrałem YAMLa tego poda, zedytowałem resources i zdeployowałem go jeszcze raz.

Yaml dołączony do repo.

# Zadanie 13

Używam zakładki "Network Activity"

![Połączenia](https://github.com/object-Object-cms/potyczki24/blob/main/Graph_8.04.2024.png?raw=true)

Zapisałem przykładowe pakiety, które wysyłane były do nginx'a, oraz dołączyłem je do tego repozytorium

Analiza pakietów polega na przeglądaniu pakiet po pakiecie jakie dane zostały wysłane do i z danego hosta, w celu analizy transferów. Przykładowym narzędziem do ich analizy jest Wireshark, który także pozwala na inch przechwytywanie.

# Zadanie 14

W pliku `adrian-nginx.yaml` readinessProbe ustawione jest na port 8080, a nginx działa na porcie 80, w dodatku livenessProbe requestuje path `/somepath`, który nie istnieje i powoduje błąd podczas proba, zmieniłem obie wartości na poprawne

Stworzyłem namespace adrian: `rancher kubectl create namespace adrian`

Zdeployowałem plik do namespace'a: `rancher kubectl apply -f adrian-nginx.yaml --namespace adrian`

# Zadanie 15

Dodałem regułę w sekcji policies > Network Rules.

W settings > configuration przeszedłem na tryb protect

# Zadanie 16

Plik `serwis.yaml` miał źle ustawione labele dla podów.
Po dodaniu `app.kubernetes.io/name: nginx` do deployment.spec.template.metadata.labels, serwis jest dobrze dopięty do Poda:
```
Name:              nginx-svc
Namespace:         serwis
Labels:            <none>
Annotations:       <none>
Selector:          app.kubernetes.io/name=nginx
Type:              ClusterIP
IP Family Policy:  SingleStack
IP Families:       IPv4
IP:                10.43.202.111
IPs:               10.43.202.111
Port:              <unset>  80/TCP
TargetPort:        80/TCP
Endpoints:         10.42.190.35:80
Session Affinity:  None
Events:            <none>
```
(Endpoint jest ustalony)
Plik `serwis.yaml` został zaktualizowany w repozytorium.

# Zadanie 17

Plik `baza.yaml` miał błąd polegający na błędnej definicji zmiennej środowiskowej MYSQL_ROOT_PASSWORD (było MYSQL_ROT_PASSWORD)
Stworzyłem namespace:
```
$ rancher kubectl create namespace baza
```

I zdeployowałem plik:
```
$ rancher kubectl apply -f baza.yaml --namespace baza
```

Zweryfikowałem, że baza działa - po podaniu hasła miałem dostęp do bazy:

```
$ rancher kubectl exec --stdin --tty --namespace baza mysql-7fcbf5dfd6-lpvwj -- mysql -p
```

# Zadanie 18

hello-world nie działał, ponieważ Adrian wybrał architekturę arm64, a komputer na którym stoi cluster to maszyna x86_64. Po usunięciu taga architektury, hello-world działa, ale oczywiście się wyłącza (hello-world musi się wyłączyć).


