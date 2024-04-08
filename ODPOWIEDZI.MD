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

# Zadanie 7

Aby odczytać YAMLa jakiegoś resource'a można:

- Użyć Rancher UI:

    * Znaleść resource w UI - na przykład Pods -> tetris.
    * W rogu strony, kliknąć na menu "..." w pionie, poten "Edit YAML" - YAML zostanie ukazany

- Użyć kubectl przez Rancher CLI

    * Znaleść resource przez CLI - na przykład `rancher kubectl get pods`
    * Odczytać YAMLa tego resource'a - `rancher kubectl get pod -o yaml <nazwa poda>`

# Zadanie 14

W pliku `adrian-nginx.yaml` readinessProbe ustawione jest na port 8080, a nginx działa na porcie 80
W dodatku livenessProbe requestuje path `/somepath`, który nie istnieje i powoduje błąd podczas proba
Zmieniłem obie wartości na poprawne

Stworzyłem namespace adrian: `rancher kubectl create namespace adrian`

Zdeployowałem plik do namespace'a: `rancher kubectl apply -f adrian-nginx.yaml --namespace adrian`


