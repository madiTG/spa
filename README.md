# HelloSpa

This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 9.1.0.

## Development server

Run `ng serve` for a dev server. Navigate to `http://localhost:4200/`. The app will automatically reload if you change any of the source files.

## Code scaffolding

Run `ng generate component component-name` to generate a new component. You can also use `ng generate directive|pipe|service|class|guard|interface|enum|module`.

## Build

Run `ng build` to build the project. The build artifacts will be stored in the `dist/` directory. Use the `--prod` flag for a production build.

## Running unit tests

Run `ng test` to execute the unit tests via [Karma](https://karma-runner.github.io).

## Running end-to-end tests

Run `ng e2e` to execute the end-to-end tests via [Protractor](http://www.protractortest.org/).

## Further help

To get more help on the Angular CLI use `ng help` or go check out the [Angular CLI README](https://github.com/angular/angular-cli/blob/master/README.md).

## Opis działania

![alt text](https://https://github.com/madiTG/spa/edit/main/Diagram1.png)

Budowanie aplikacji można inicjować z trzech miejsc, bezpośrednio z GitHuba (Actions), automatycznie po wykonaniu push na branch main lub z przestrzeni roboczej po sklonowaniu repozytorium przy pomocy narzędzia vagrant. Budowanie odbywa się w przygotowanym obrazie dockera (**ci_dockerfile/Dockerfile**) opartym na ubuntu. Tworzenie obrazu wywoływane jest poprzez wykonanie komendy vagrant up. Efektem budowania jest utowrzenie w repozytorium brancha np. build_1515010122. Po utworzeniu brancha uruchamiany jest webhook do procesu w repozytorium Quay. Ściąga ono danego brancha i uruchamia budowanie obrazu z **cd_image/Dockerfile** - kopiuje zbudowane pliki do obrazu opartego na nginx. Na hoście na którym chcemy umieścić środowisko klonujemy repozytorium i uruchamiamy narzędzie vagrant z odpowiednimi opcjami do utowrzenia kontenera z haproxy (budowane z **proxy_dockerfile/Dockerfile**) i obrazów z serwerami www ze zbudowaną aplikacją (od 1 do 3), quay.io/tomaszgaska/spa:latest.  

Komendy:  

odpowiednia opcja (z wyjątkiem token i instances) wyzwalana jest przy pomocy słowa kluczowego "true"  
**vagrant --build=true --deploy=true --proxy=true --token=xyz --instances=(1|2|3) up**

odpowiednio vagrant destroy, np jeśli postawiliśmy środowisko przy pomocy:  
**vagrant --build=false --deploy==true --proxy=true --instances=2 --token=xyz up**
to niszczymy je w następujący sposób:  
**vagrant --build=false --deploy==true --proxy=true --instances=2 destroy  **

parametry:  
build - uruchamia budowanie aplikacji  
deploy - uruchamia deployment kontenerów z repozytorium  
proxy - uruchamia budowanie kontenera z haproxy  
token - token do githuba (można także wyeksportować go w workspace poleceniem export GITHUB_ACCESS_TOKEN=ghp_rF2...)
instance - liczba instancji nginx (od 1 do 3)

klonowanie repo:  

**git clone https://github.com/madiTG/spa.git

