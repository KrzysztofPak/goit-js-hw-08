Parcel template

Ten projekt został stworzony przy pomocy Parcel. W celu zapoznania się i skonfigurowania dodatkowych opcji zobacz dokumentację

Przygotowanie nowego projektu

Upewnij się, że na komputerze zainstalowana jest wersja LTS Node.js. Ściągnij i zainstaluj, jeśli jest taka potrzeba.
Sklonuj to repozytorium.
Zmień nazwę folderu z parcel-project-template na nazwę swojego projektu.
Utwórz nowe, puste repozytorium na GitHub.
Otwórz projekt w VSCode, uruchom terminal i zwiąż projekt z repozytorium GitHub zgodnie z instrukcją.
Utwórz zależność projektu w terminalu przez polecenie npm install .
Włącz tryb edycji, wykonując polecenie npm start.
Przejdź w przeglądarce pod adres http://localhost:1234. Ta strona będzie się automatycznie odświeżać po dokonaniu zmian w plikach projektu.
Pliki i foldery

Wszystkie partiale plików stylów powinny znajdować się w folderze src/sass i importować się w pliki stylów stron. Na przykład dla index.html plik stylów nazywa się index.scss.
Obrazy dodawaj do pliku src/images. Moduł zbierający optymalizuje je, ale tylko przy deploymencie wersji produkcyjnej projektu. Wszystko to zachodzi w chmurze, aby nie obciążać twojego komputera, ponieważ na słabszym sprzęcie może to zająć sporo czasu.
Deployment

Aby skonfigurować deployment projektu należy wykonać kilka dodatkowych kroków konfigurowania twojego repozytorium. Wejdź w zakładkę Settings i w podsekcji Actions wybierz punkt General.

GitHub actions settings

Przejdź do ostatniej sekcji, w której upewnij się, że wybrane opcje są takie same jak na następnym obrazku i kliknij Save. Bez tych ustawień w module zbierającym będzie zbyt mało pozwoleń dla automatyzacji procesu deploymentu.

GitHub actions settings

Wersja produkcyjna projektu będzie automatycznie gromadzić się i deployować na GitHub Pages w gałęzi gh-pages za każdym razem, gdy aktualizuje się gałąź main. Na przykład po bezpośrednim pushu lub przyjętym pull requeście. W tym celu niezbędne jest, aby w pliku package.json wyedytować pole homepage i skrypt build, zamieniając your_username i your_repo_name na swoje nazwy i wysłać zmiany na GitHub.

"homepage": "https://your_username.github.io/your_repo_name/",
"scripts": {
  "build": "parcel build src/*.html --public-url /your_repo_name/"
},
Dalej należy wejść w ustawienia repozytorium GitHub (Settings > Pages) i wystawić dystrybucję wersji produkcyjnej z folderu /root gałęzi gh-pages, jeśli nie zrobiło się to automatycznie.

GitHub Pages settings

Status deploymentu

Status deploymentu ostatniego commitu wyświetla się na ikonie obok jego identyfikatora.

** Żółty kolor** - wykonuje się zbudowanie i deployment projektu.
** Zielony kolor** - deployment zakończył się sukcesem.
** Czerwony kolor** - w czasie lintingu, budowania lub deplymentu pojawił się błąd.
Więcej informacji o statusie można zobaczyć klikając na ikonkę i w wyskakującym oknie przejść do odnośnika Details.

Deployment status

Działająca strona

Po jakimś czasie, zazwyczaj kilku minut, działającą stronę będzie można zobaczyć pod adresem wskazanym w wyedytowanej właściwości homepage. Na przykład tu znajduje się odnośnik do działającej strony dla tego repozytorium https://goitacademy.github.io/parcel-project-template.

Jeżeli otwiera się pusta strona, upewnij się, że w zakładce Console nie ma błędów związanych z nieprawidłowymi ścieżkami do plików projektu CSS i JS (404). Najprawdopodobniej wprowadzona została nieprawidłowa wartość właściwości homepage lub skryptu build w pliku package.json.

Jak to działa

How it works

Po każdym pushu w gałęzi main repozytorium GitHub, włącza się specjalny skrypt (GitHub Action) z pliku .github/workflows/deploy.yml.
Wszystkie pliki repozytorium kopiują się na serwer, gdzie projekt inicjalizuje się i buduje przed deploymentem.
Jeżeli wszystkie kroki zakończyły się sukcesem, zbudowana wersja produkcyjna plików projektu wysyła się w gałąź gh-pages. W przeciwnym razie, w logu wykonania skryptu wskazane zostanie, w czym jest problem.
