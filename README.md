# Witamy w finale!
Potyczki Młodych Adminów 2024

## Wstęp
Tegoroczne zadania są pomyślane jako dzień z pracy administratora w korporacji. Jest trochę codziennych, podstawowych czynności, jest znaczący nacisk na elementy związane z bezpieczeństwem, są też zagadkowe awarie, które należy jak najszybciej naprawić bo kosztują naszą firmę ogromne pieniądze. Jak w prawdziwym życiu, zadań jest więcej niż czasu i warto odpowiednio priorytetyzować!

### Zadanie 0
Najlepiej napisany program i najlepiej wdrożony system jest tykającą bombą bez odpowiedniej dokumentacji. Nikt nie lubi jej pisać, ale jest kluczowa dla łatwości późniejszego utrzymywania i efektywnej współpracy - a także do sprawdzania zadań! Dlatego udokumentuj wszystkie zadania, co najmniej wymieniając które zostały wykonane, bo **tylko te zostaną sprawdzone**. Niektóre zadania wymagają pisemnej odpowiedzi, umieść je też w dokumentacji.

Opcjonalnie: opisz kroki wykonane w celu realizacji zadania, szczególnie lokalizacje zasobów, użyte opcje i komendy - nie musisz tego robić, ale w razie wątpliwości będą one działać na twoją korzyść. Na przykład jeśli zadanie nie zostało do końca wykonane, ale znacząca część kroków jest opisana poprawnie, zaliczę za to częściowe punkty. Albo jeśli zadanie zostało wykonane, ale nie w sposób jakiego się spodziewałem, to opis będzie kluczem do uzyskania za nie punktów. To, co nie jest opisane, a nie jest oczywiste z interfejsu, będzie rozstrzygane na twoją niekorzyść (jak w prawdziwm korpo-życiu, nikt nie ma szklanej kuli, a ma dużo własnej pracy!).

### Zadanie
Na klastrze "potyczki" uruchom “nginx” w najnowszej wersji (2pkt).
- Utwórz usługę dzieki której można się odwołać do naszego ngnx z całego klastra (5pkt)
- Chcemy zapewnić wysoką dostępność tej usługi - upewnij się, że cały czas będą działały co najmniej trzy repliki naszego kontenera (2pkt)
- Zapewnij dostępność usługi na internet. Nie masz czasu czekać aż administratorzy sieci udostępnią ci firmowy DNS, a potrzebujesz szybko przetestować dostępność więc wymyśl jak zapewnić rozwiązywalny url wskazujący na IP hosta, na którym jest twój klaster "potyczki". 20pkt (rozwiązaniem jest podanie adresu typu ngnx.xxx.xx rozwiązywalny z internetu, pod którym zgłosi się działająca usługa);

### Zadanie 
Twój niezbyt rozgarnięty kolega z pracy, Adrian, prosi cię o poradę: w klastrze mam pewien resource, ale nie wiem jak znaleźć yaml tego zasobu? Jak go podejrzeć?
5pkt (+5pkt za dodatkową metodę)

### Zadanie
Adrian uruchomił aplikację składającą się z front-endu i bazy danych MySQL. Widzisz, że jego kontener MySQL jest uruchomiony na najprostszych domyślnych ustawieniach. Czy jest to zalecany sposób? Uzasadnij w kilku zdaniach (min. 20 słów dla pełnej punktacji).
5pkt (+5pkt jeśli uzasadnienie zawiera za i przeciw oraz sugestię poprawy)

### Zadanie
Wytłumacz Adrianowi w kilku prostych zdaniach czym jest resource o nazwie Gateway w Kubernetes? (min. 20 słów dla pełnej punktacji)
5pkt

### Zadanie
Adrian jest bardzo skonfundowany dlaczego są dwa różne resource w Kubernetes, które "robią to samo" czyli zarządzają zestawem identycznych podów: Deployment i ReplicaSet. Wyjaśnij mu na czym polega różnica między tymi resource'ami. (min. 20 słów dla pełnej punktacji)
5pkt
