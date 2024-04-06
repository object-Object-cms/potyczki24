# Witamy w finale!
Potyczki Młodych Adminów 2024

## Wstęp
Tegoroczne zadania są pomyślane jako dzień z pracy administratora w korporacji. Jest trochę codziennych, podstawowych czynności, jest znaczący nacisk na elementy związane z bezpieczeństwem, są też zagadkowe awarie, które należy jak najszybciej naprawić bo kosztują naszą firmę ogromne pieniądze. Jak w prawdziwym życiu, zadań jest więcej niż czasu i warto odpowiednio priorytetyzować!

### Zadanie 0
Najlepiej napisany program i najlepiej wdrożony system jest tykającą bombą bez odpowiedniej dokumentacji. Nikt nie lubi jej pisać, ale jest kluczowa dla łatwości późniejszego utrzymywania i efektywnej współpracy - a także do sprawdzania zadań! Dlatego udokumentuj wszystkie zadania, co najmniej oznaczając te które zostały wykonane, bo **tylko te zostaną sprawdzone**. Niektóre zadania wymagają pisemnej odpowiedzi, umieść je też w dokumentacji.

Opisz kroki wykonane w celu realizacji zadania, szczególnie lokalizacje zasobów, użyte opcje i komendy - nie musisz tego robić bardzo dokładnie, ale w razie wątpliwości będą one działać na twoją korzyść. Na przykład jeśli zadanie nie zostało do końca wykonane, ale znacząca część kroków jest opisana poprawnie, zaliczymy za to częściowe punkty. Albo jeśli zadanie zostało wykonane, ale nie w sposób jaki był spodziewany, to opis będzie kluczem do uzyskania za nie punktów. To, co nie jest opisane, a nie jest oczywiste z interfejsu, będzie rozstrzygane na twoją niekorzyść (jak w prawdziwm korpo-życiu, nikt nie ma szklanej kuli, a ma dużo własnej pracy!).

### Zadanie
Na klastrze "potyczki" utwórz projekt "web-server" a w nim namespace "ngnx". W tym namespace uruchom kontener “nginx” w najnowszej wersji (5pkt).
- Utwórz usługę dzieki której można się odwołać do naszego ngnx z całego klastra (5pkt)
- Chcemy zapewnić wysoką dostępność tej usługi - upewnij się, że cały czas będą działały co najmniej trzy repliki naszego kontenera (2pkt)
- Zapewnij dostępność usługi na internet. Nie masz czasu czekać aż administratorzy sieci udostępnią ci firmowy DNS, a potrzebujesz szybko przetestować dostępność, więc wymyśl jak zapewnić rozwiązywalny url wskazujący na IP hosta, na którym jest twój klaster "potyczki". 20pkt (pełnym rozwiązaniem jest podanie adresu typu ngnx.xxxx.xxxx.xx rozwiązywalnego z internetu, pod którym zgłosi się działająca usługa);

### Zadanie
 Sprawdź czy host klastra "potyczki" spełnia wymagania (prerequisites) dla aplikacji Longhorn; doinstaluj ewentualne braki. 5pkt
 Z katalogu aplikacji wbudowanych Ranchera zainstaluj Longhorn w najnowszej stabilnej wersji na klastrze "potyczki", ustawiając w konfiguracji instalacyjnej 1 replikę i domyślny StorageClass. 5pkt
 Potwierdź status wszystkich podów Longhorna 7pkt

### Zadanie
Dodaj nowe repozytorium do katalogu aplikacji. URL repo: https://rancher.github.io/rodeo 5 pkt

### Zadanie
Z katalogu aplikacji zainstaluj NeuVector w najnowszej stabilnej wersji - 10pkt

### Zadanie
Nasi deweloperzy chcą korzystać z publicznie dostępnych obrazów, ale mogą one zawierać groźne podatności. Dlatego chcemy najperw przeskanować rejestr, zanim zaczniemy z niego korzystać. Użyj NeuVector, żeby przeskanować sekcję nvbeta/* w rejestrze https://registry.hub.docker.com ; jako rozwiązanie podaj nazwę image z największą ilością podatności. 7pkt

### Zadanie



### Zadanie 
Twój niezbyt rozgarnięty kolega z pracy, Adrian, prosi cię o poradę: w klastrze mam pewien resource, ale nie wiem jak znaleźć yaml tego zasobu? Jak go podejrzeć?
5pkt (+5pkt za dodatkową metodę)

### Zadanie
Adrian uruchomił aplikację składającą się z front-endu i bazy danych MySQL. Widzisz, że jego kontener MySQL jest uruchomiony na najprostszych domyślnych ustawieniach. Czy jest to zalecany sposób? Uzasadnij w kilku zdaniach (min. 20 słów dla pełnej punktacji).
5pkt (+5pkt jeśli uzasadnienie zawiera za i przeciw oraz sugestię poprawy)

### Zadanie
Wytłumacz Adrianowi w kilku prostych zdaniach czym jest resource o nazwie Gateway w Kubernetes? (min. 20 słów dla pełnej punktacji)
7pkt

### Zadanie
Adrian jest bardzo skonfundowany dlaczego są dwa różne resource w Kubernetes, które "robią to samo" czyli zarządzają zestawem identycznych podów: Deployment i ReplicaSet. Wyjaśnij mu na czym polega różnica między tymi resource'ami. (min. 20 słów dla pełnej punktacji)
5pkt
