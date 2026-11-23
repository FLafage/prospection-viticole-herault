# 🍇 Prospection Viticole & Vinicole — Hérault (34)

Constitution d'une base de données de prospection terrain pour un technico-commercial intervenant sur la filière viticole et vinicole dans le département de **l'Hérault (34)**.

Le projet croise la **base SIRENE (INSEE)** avec la **liste des bénéficiaires des aides PAC (ASP / Telepac)** et génère un fichier Excel prêt à l'emploi ainsi qu'un rapport méthodologique en HTML via Quarto.

---

## 🎯 Périmètre de l'extraction

* **Zone géographique** : Département de l'Hérault (`codeCommuneEtablissement LIKE '34%'` — filtrage sur le code INSEE commune).
* **Statut** : Établissements actifs uniquement (`etatAdministratifEtablissement = 'A'`).
* **Codes NAF ciblés** :
  * `01.21Z` : Culture de la vigne
  * `11.02A` : Fabrication de vins effervescents
  * `11.02B` : Vinification

---

## 📊 Sources de données

1. **Base SIRENE (INSEE via data.gouv.fr)** :
   * Tables `StockEtablissement` et `StockUniteLegale` au format **Parquet**.
   * Interrogées directement à distance grâce à **DuckDB (`httpfs`)**, sans téléchargement intégral des fichiers nationaux.
2. **Bénéficiaires des aides PAC (ASP / Telepac)** :
   * Fichier CSV national des aides versées (FEAGA / FEADER).
   * *Note :* En raison de sa taille (> 100 Mo), ce fichier `.csv` est exclu du dépôt via `.gitignore`. Il doit être téléchargé manuellement depuis le [portail ASP](https://www.telepac.agriculture.gouv.fr/) et placé dans le dossier du projet avant exécution.

---

## 🛠️ Stack technique & Prérequis

Le projet repose sur **R** et **Quarto**. Packages nécessaires :

```r
install.packages(c("DBI", "duckdb", "jsonlite", "dplyr", "tidyr", "stringr", "openxlsx"))