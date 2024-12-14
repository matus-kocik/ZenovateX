# Notes

## Inštalácia Pythonu

Prvým krokom v našom projekte je **inštalácia Pythonu**. Python je jazyk, ktorý používame na vývoj webovej aplikácie.

<!-- https://www.python.org/downloads/

```bash
python --version
python3 --version
``` -->

## Inštalácia Poetry

Po inštalácii Pythonu budeme používať Poetry, ktorý slúži na správu závislostí a správu virtuálnych prostredí pre Python projekty. Poetry umožňuje jednoduchšie spravovať knižnice a verzie bez konfliktov medzi projektmi.

<!--
```bash
curl -sSL https://install.python-poetry.org | python3 
pipx install poetry
poetry --version
``` -->

## Vytvorenie virtuálneho prostredia

Po inštalácii Pythona a Poetry môžeme prejsť k vytvoreniu virtuálneho prostredia a inštalácii závislostí. To nám pomôže spravovať všetky knižnice, ktoré náš projekt potrebuje, bez toho, aby sa ovplyvňovali iné projekty.

<!--
```bash
poetry init
poetry add <názov_knižnice>

``` -->

## Nastavenie MkDocs a dokumentácie

Po inštalácii všetkých potrebných knižníc môžeme začať pracovať na nastavení MkDocs pre generovanie dokumentácie. MkDocs umožňuje rýchlo vytvoriť statickú webovú stránku s dokumentáciou pomocou jednoduchého Markdown formátu.

<!--
```bash
mkdocs new . (. znamena, ze v tomto priecinku)

``` -->

Otvorte súbor mkdocs.yml a upravte ho podľa svojich potrieb. Pridajte napríklad nasledujúcu konfiguráciu:

<!-- ```yaml
site_name: ZenovateX Documentation
theme:
  name: 'readthedocs'
``` -->

<!-- ```bash
mkdocs serve
``` -->

## Nasadenie dokumentácie na Read the Docs

Po dokončení základného nastavenia MkDocs sme pristúpili k nasadeniu dokumentácie na platformu Read the Docs, ktorá umožňuje jednoduché hostovanie a správu dokumentácie.

Vytvorili sme repo na githube ...
Zabezpečenie kompatibility súborov s Read the Docs

<!-- ```bash
poetry export -f requirements.txt --output requirements.txt --without-hashes
``` -->

Konfigurácia súboru .readthedocs.yml
Pre lepšiu kontrolu nad konfiguráciou nasadenia na Read the Docs pridajte do koreňového adresára projektu súbor .readthedocs.yml s nasledovným obsahom:

<!-- ```yaml
version: 2

build:
  os: ubuntu-24.04
  tools:
    python: "3"

python:
  install:
    - requirements: requirements.txt

mkdocs:
  configuration: mkdocs.yml
  ``` -->

## Inštalácia Django cez Poetry

## Vytvorenie projektu s nazvon config, co je lepsie

<!-- poetry add django 
poetry shell - pre venv alebo prikaz s poetry run...
poetry run django-admin startproject config .
-->

## Vytvorenie priecinka pre appky

V projekte používame modulárnu štruktúru, kde všetky aplikácie umiestňujeme do priečinka apps. Tento priečinok je už vytvorený a obsahuje súbor <!-- __init__ -->.py, aby ho Python rozpoznal ako balík.
<!-- mkdir apps
touch apps/__init__.py -->

## Vytvorenie aplikácie finance

Pre správu financií sme vytvorili aplikáciu finance v priečinku apps:
vytvorenie priecinku finance
poetry run python manage.py startapp finance apps/finance

## Upravime INSTALLED_APPS v súbore settings.py

INSTALLED_APPS = [
    # ostatné aplikácie
    'apps.finance',
]

## Presunutie existujúcich nastaveni

Presuňte obsah pôvodného settings.py do nového súboru base.py a vymažte pôvodný settings.py.

## Zmena SECRET_KEY, kvoli gitu

## Inštalácia balíka python-decouple

poetry add python-decouple

## Vytvorenie .env suboru

.env súbor bude obsahovať všetky citlivé údaje ako SECRET_KEY, prihlasovacie údaje do databázy, a iné konfigurácie. Tento súbor by nemal byť verzovaný v gite.

V koreňovom adresári tvojho projektu (kde je napríklad manage.py), vytvor .env súbor. Tento súbor obsahuje konfiguráciu, ktorá by nemala byť zahrnutá do Gitu. Pridaj ho do .gitignore, aby bol chránený.
Obsah: ...

<!-- SECRET_KEY=
DEBUG=
DATABASE_URL=
ALLOWED_HOSTS= -->

## VZDY AKTUALIZOVAT GITIGNORE

## Nacitanie hodnot z env do settings.py

Otvori settings.py a importuj funkciu config z balíčka decouple:

<!-- from decouple import config

# Secret key
SECRET_KEY = config("SECRET_KEY")

# Debug mode 
DEBUG = config("DEBUG")

# Allowed hosts 
ALLOWED_HOSTS = config("ALLOWED_HOSTS")

# Database settings
DATABASES = {
    "default": {
        "ENGINE": "django.db.backends.postgresql",
        "NAME": config("DB_NAME"),
        "USER": config("DB_USER"),
        "PASSWORD": config("DB_PASSWORD"),
        "HOST": config("DB_HOST"),
        "PORT": config("DB_PORT"),
    }
} -->

## Update exportovacieho pluginu poetry na requirements

Exportovací plugin (poetry-plugin-export) budeš musieť nainštalovať manuálne.

Čo sa deje:
  Poetry momentálne obsahuje funkciu na exportovanie requirements.txt, ale plánuje túto funkciu presunúť do samostatného pluginu.

  Ak chceš túto funkciu zachovať aj v budúcnosti, odporúčajú nainštalovať plugin už teraz, aby si bol pripravený.

poetry self add poetry-plugin-export

Export:

poetry export -f requirements.txt --output requirements.txt --without-hashes

<!-- 

erp/
├── erp/                     # Hlavná aplikácia Django (core nastavenia)
│   ├── settings.py
│   ├── urls.py              # Vstupný bod pre URL
│   ├── wsgi.py
│   └── asgi.py
├── finances/                # Modul Financie
│   ├── models/
│   │   ├── __init__.py
│   │   ├── budget.py        # Model pre rozpočet
│   │   ├── expenses.py      # Model pre výdavky
│   │   └── accounting.py    # Model pre účtovníctvo
│   ├── views/
│   │   ├── __init__.py
│   │   ├── budget_views.py
│   │   └── expenses_views.py
│   ├── urls.py
│   ├── tests/
│   │   ├── test_budget.py
│   │   └── test_expenses.py
│   └── templates/
│       └── finances/
│           ├── budget_list.html
│           └── expense_detail.html
├── calendar/                # Modul Kalendár
├── wellness/                # Modul Zdravie a wellness
├── tasks/                   # Modul Úlohy a produktivita
├── analytics/               # Modul Analytika a reporty
└── common/                  # Zdieľané komponenty (napr. autentifikácia, notifikácie)
    ├── models.py
    ├── utils.py
    ├── serializers.py
    └── middleware.py

warehouse/
├── __init__.py
├── admin.py
├── apps.py
├── migrations/
├── models/
│   ├── __init__.py
│   ├── inventory.py       # Modely pre inventár
│   ├── orders.py          # Modely pre objednávky
│   └── suppliers.py       # Modely pre dodávateľov
├── views/
│   ├── __init__.py
│   ├── inventory_views.py # Views pre inventár
│   ├── order_views.py     # Views pre objednávky
│   └── supplier_views.py  # Views pre dodávateľov
├── serializers/
│   ├── __init__.py
│   ├── inventory_serializers.py
│   └── order_serializers.py
├── urls.py
├── tests/
│   ├── __init__.py
│   ├── test_inventory.py
│   └── test_orders.py
└── templates/
    └── warehouse/
        ├── inventory/
        ├── orders/
        └── suppliers/

1. Financie

    • Správa príjmov a výdavkov
    • Sledovanie investícií
    • Plánovanie rozpočtu
    • Štatistiky a reporty
    • Účtovníctvo a fakturácia

2. Bankové účty a investičné portfólio

    • Import bankových výpisov
    • Správa rôznych účtov a investícií
    • Sledovanie stavu účtov a investičných výnosov
    • Scrapovanie a automatické sledovanie aktuálneho stavu investícií (napr. ceny akcií, stav účtov)

3. Pracovný čas a projektový manažment

    • Sledovanie odpracovaných hodín
    • Správa úloh a projektov
    • Výkaz práce a generovanie reportov

4. Kalendár a plánovač

    • Integrovaný alebo synchronizovaný kalendár (napr. s Google Calendar)
    • Plánovanie úloh a udalostí
    • Nastavovanie pripomienok a upozornení

5. Denník a poznámky

    • Osobný denník na denné záznamy
    • Ukladanie poznámok podľa kategórií
    • Rýchle poznámky a todo zoznamy

6. Úlohy a produktivita

    • Denné, týždenné a dlhodobé ciele
    • Organizovanie úloh podľa priority a kategórií
    • Sledovanie pokroku v jednotlivých úlohách

7. Zdravie a wellness

    • Sledovanie zdravotných údajov (napr. váha, spánok, fyzická aktivita)
    • Záznamy o návštevách lekárov, procedúrach a liekoch
    • Ciele pre wellness (napr. cvičenie, diéta)

8. Stravovanie a nákupný zoznam

    • Plánovanie jedálničkov a rozpis stravy
    • Nákupné zoznamy
    • Sledovanie výdajov na potraviny

9. Cestovanie a plánovanie výletov

    • Správa cestovných plánov
    • Ukladanie itinerárov a rezervácií
    • Rozpočty a výdavky na cesty

10. Dokumenty a osobná administratíva

    • Ukladanie a manažovanie osobných dokumentov (napr. faktúry, potvrdenia)
    • Rýchly prístup k dôležitým dokumentom

11. Kontakty a CRM (správa kontaktov)

    • Evidencia dôležitých kontaktov
    • Pripomienky na kontaktovanie dôležitých osôb (napr. pripomienky na stretnutia)

12. Vzdelávanie a osobný rast

    • Evidencia kníh, kurzov a vzdelávacích aktivít
    • Záznamy z učenia (poznámky, úlohy, sledovanie pokroku)
    • Osobné a profesionálne ciele

13. Hobby a záľuby

    • Záznamy o aktivitách a záľubách (napr. šport, tvorba, umenie)
    • Ciele pre voľnočasové aktivity
    • Sledovanie pokroku a projektov v rámci hobby

14. Šetrenie a dlhodobé ciele

    • Finančné ciele a plánovanie šetrenia
    • Sledovanie cieľov a pokroku

15. Pripomienky a upozornenia

    • Pripomienky na dôležité udalosti (narodeniny, výročia)
    • Notifikácie pre osobné a pracovné úlohy

16. Sklad a správa majetku

    • Sledovanie osobného majetku a inventára
    • Správa majetku (napr. elektronika, nábytok, cennosti)

17. Bytové a domáce povinnosti

    • Údržba domácnosti (pripomienky na opravy, upratovanie)
    • Sledovanie stavu a údržby domácich spotrebičov

18. Automatizácie a integrácie

    • Integrácie s rôznymi aplikáciami (napr. Google Calendar, bankové API)
    • Automatizované úlohy (napr. spracovanie výpisov, notifikácie)

19. Osobná bezpečnosť a heslá

    • Správa hesiel a dôležitých informácií
    • Evidencia bezpečnostných opatrení (napr. dvojfaktorová autentifikácia)

20. Plánovanie a pripomienky v dlhodobom horizonte

    • Nastavenie ročných cieľov a plánov
    • Pravidelné pripomienky na dôležité dlhodobé úlohy

21. Analytika a reporty

    • Prehľady a štatistiky (napr. finančné výkazy, sledovanie návykov)
    • Export údajov a reportovanie podľa kategórií

22. AI asistent a automatické odporúčania

    • Automatické odporúčania na základe dát (napr. výdavkové vzorce, zlepšenie efektivity)
    • Integrácia s NLP modelmi na analyzovanie textov a záznamov (napr. sumarizácie poznámok)

23. Životné ciele a plány

    • Evidencia osobných a životných cieľov
    • Dlhodobé plány (napr. úspory na bývanie, dôchodok)

24. Denné rutiny a návyky

    • Sledovanie denných návykov a rutín (napr. ranná rutina, cvičenie)
    • Nastavenie pripomienok na dodržiavanie denných návykov

take nieco...
 -->