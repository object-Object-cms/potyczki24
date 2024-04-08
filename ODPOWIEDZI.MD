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

# Zadanie 3

W rancher web UI, otworzyłem cluster potyczki, sekcja Apps, Repositories, Create, wprowadziłem nazwę i URL.

W zakładce Apps, charts wyszukałem "tetris" i zainstalowem aplikację. Jako hostname podałem `tetris.193.187.69.136.sslip.io`.

Aplikacja działa

# Zadanie 7

Aby odczytać YAMLa jakiegoś resource'a można:

- Użyć Rancher UI:

* Znaleść resource w UI - na przykład Pods -> tetris.
* W rogu strony, kliknąć na menu "..." w pionie, poten "Edit YAML" - YAML zostanie ukazany

- Użyć kubectl przez Rancher CLI

* Znaleść resource przez CLI - na przykład `rancher kubectl get pods`
* Odczytać YAMLa tego resource'a - `rancher kubectl get pod -o yaml <nazwa poda>`

