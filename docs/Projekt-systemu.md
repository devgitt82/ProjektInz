# Projekt Systemu - Składy budowlane

## Wstęp

Projekt ma za cel implementacje aplikacji internetowego dostarczającej informacji o składach budowlanych. Aplikacja będzie umożliwiała wyszukanie lokalnych składów budowlanych, przegląd ich najpopularniejszego asortymentu z podziałem na kategorie oraz innych przydatnych informacji takich jak: 
- godziny otwarcia
- przynależność do sieci sklepów
- oferta - podzielona na kategorie
- ceny najbarziej popularnych produktów
- lokalizacja geograficzna

Aplikacja będzie również umożliwiała wyznaczenia trasy z lokalizacji użytkownika do wybranego składu budowlanego.


## Aktorzy

- Bezpośredni użytkownicy aplikacji,
- Administratorzy,
- Twórcy oraz osoby zaangażowane w jej utrzymanie.


## Główne funkcje systemu (Sposób ich wywołania i parametry)

- Wyświetlanie mapy
- Znajdowanie trasy
- Wyszukiwanie składu
- Naniesienie na mapę obiektów (składy budowlane)
- Naniesienie na mapę pozycji użytkownika
    - poprzez interfejs postawienie markera na mapie.
- Dodawanie i edycja obiektów dla administratora
- Prezentacja informacji o wybranym obiekcie
- Wyliczanie drogi pomiedzy obiektami
- Scalanie markerów przy zmniejszaniu skali
    - Pomniejszenie mapy poprzez interfejs lub scroll myszy
- Znajdowanie składu
- Trasowanie - wyznacznie trasy z punktu np. lokalizacji użytkownika do wybranego składu budowlanego


## Przypadki użycia

![Przypadki użycia][use-cases] 



## Diagramy sekwencji

![uwierzytelnianie][sd-auth]

![dodawanie składów][sd-add-asset]



## Struktury danych i bazy danych

### Bazy danych


![Database ERD][database-erd]

![Użytkownicy ERD][users-erd]



## Architektura, technologia i narzędzia

### Architektura systemu

Aplikacja zostanie stworzona jako samodzielny system o architekturze *klient - serwer*. Kod będzie zorganizowany według wzorca monolit z podziałem na moduły funkcjonalne, część frontendową i backendową. Frontend odpowiada za interfejs użytkownika, interakcję z sytemem i prezentację danych. Backend odpowiadza za zarządzanie, modyfiakcje, przechowywanie i udostępnianie danych (administracja). Dane z backendu będą udostępnane frontendowi poprzez API.

![Architektura trój warstwowa][triple-layer-arch]


### API

Backend aplikacji udostepnia dane poprzez REST API z danymi w formacie JSON.
API ma dostarczać danych z bazy potrzebnych do wypełnienia interfejsów użytkownika.

Endpointy backend:
- `/sieci-sklepow` - ma zwracać liste wszystkich sieci sklepów 
- `/sklady-budowlane` - ma zwracać listę wszystkich sklepów budowlanych
- `/kategorie-produktów` - ma zwracać listę wszystkich kategorii produktów
- `/produkty` - ma zwracać listę wszystkich produktów


### Środowisko tworzenia aplikacji

- język programowania
    - Frotend (Technologie Web)
        - HTML
        - CSS
        - Javascript
    - Backend
        - PHP
        - SQL (MySql - MariaDB)
- kompilator i środowisko
    - Do edycji kodu źródłowego developer może używać dowolnego edytora, wszystkie potrzebne narzędzia są dostępne z poziomu CLI
    - Aplikacja bedzie serwowana przez Apache HTTP Serwer


## Wykorzystane zasoby

- Open Layers - komponent mapowy
- Nominati - geokodowanie, zwracanie informacji o punkcie/markerze



## Projekt interfejsu użytkownika

- wymagania co do rozmiaru okna
    Interfejs będzie responsywny. Korzystanie z niego ma być możliwe na różnych rozdzielczościach ekranów desktopowych. Wersji na ekrany urządzeń mobilnych w tej wersji nie przewidujemy.






[database-erd]: ./img/database-erd-lucidchart.png
[triple-layer-arch]: ./img/architektura-trojwarstwowa-klient-serwer.jpg
[sd-auth]: ./img/sd-auth.png
[sd-add-asset]: ./img/sd-add-asset.png
[use-cases]: ./img/use-cases.png
[users-erd]: ./img/users-erd.png
