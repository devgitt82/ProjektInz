# Instalacja środowiska

Do pracy nad projektem dostępne są środowiska:
- [Docker](##uruchamianie-projektu-z-Sail-(docker-compose)) (Laravelowa komenda `sail`)
- [Windows z XAMPP](##instalacja-środowiska-dla-windows)

---

## Instalacja środowiska dla Windows

- [XAMPP](https://www.apachefriends.org/pl/index.html) - apache, php, mysql.
- [GIT](https://git-scm.com/)
- Dowolny edytor kodu, np. [Visual Studio Code](https://code.visualstudio.com/)
- [Composer](https://getcomposer.org/) - dependency manager for PHP
- [nodejs](https://nodejs.org/dist/v14.15.4/node-v14.15.4-x64.msi) - dla npm - dependency manager for JS

### Uruchamianie projektu

- XAMPP Control Panel
    - Start Apache (do podglądu/edycji bazy danych przez phpmyadmin)
    - Start MySQL
    - Tworzymy bazę danych `sip_db`, np przy pomocy [phpmyadmin](http://locahost/phpmyadmin)
- Odpalamy konsolę __GIT BASH__
    - Klonujemy repo
        ```shell
        git clone https://github.com/devgitt82/ProjektInz/project
        ```
    - Przechodzimy do folderu `cd ./sip/project`
    - Zamien w `.env` wartość `DB_HOST` na `DB_HOST=127.0.0.1`.
    - `composer install` (instalacja zależności PHP)
    - Ze względu na brak pełnej kompatybilności z mariadb należy zmodyfikować nieco bibliotekę _grimzy_
        - w pliku `.\vendor\grimzy\laravel-mysql-spatial\src\Eloquent\SpatialExpression.php` usuwamy `'axis-order=long-lat'` z funkcji `getValue()`. Funkcja ma wyglądać tak:
        ```php
        public function getValue()
        {
            return "ST_GeomFromText(?, ?)";
        }
        ```
    - `npm install` (instalacja zależności JS)
    - `php artisan serve` (uruchomienie serwera)
- Aplikacja jest dostępna pod adresem [localhost:8000](http://localhost:8000/)
- Wstępne generowanie danych do bazy [localhost:8000/generate-data](http://localhost:8000/generate-data)

---

## Uruchamianie projektu z Sail (docker-compose)

### Wymaga: 
- Docker
- docker-compose
- composer

### Uruchamianie:

```shell
composer install

alias sail='bash vendor/bin/sail'   # alias dla wygody

sail up -d                          # -d = run in detached mode
sail artisan migrate:fresh --seed   # creates migration table, 
                                    # runs migrations and seed db 
                                    # with example data
```

Aplikacja jest dostępna pod [localhost:80](http://localhost)

### Zamykanie:

```shell
sail down       # podobnie jak docker-compose down
sail down -v    # to dodatkowo usuwa volumeny (czyści bazę)
```

### Export zawartości bazy

```shell
docker exec project_mysql_1 mysqldump sip_db > sip_db.sql

# clean sql, no comments
docker exec project_mysql_1 mysqldump --no-data --skip-comments --skip-add-drop-table sip_db | grep -v '^\/\*![0-9]\{5\}.*\/;$' > sip_db.sql
```
