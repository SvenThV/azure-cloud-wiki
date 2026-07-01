# Business Central Datenbankexport nach Azure Storage

## Übersicht

## Voraussetzungen
- Azure Storage Account
- Blob Container
- SAS URI
- Business Central Admin Center
- Produktionsumgebung

## Manueller Export
- Ablauf
- Screenshots
- BACPAC-Datei

## Automatisierung
- Business Central Admin Center API
- PowerShell-Skripte von Microsoft
- Azure Automation
- App Registration für die BC API
- SAS-Token-Erstellung per PowerShell

## Einschränkungen
- nur Production
- max. 10 Exporte/Monat
- Exportformat BACPAC
- kein vollständiges BC-On-Prem-Backup

## Erkenntnisse aus dem Projekt
- Export erfolgt ausschließlich über SAS URI
- Kein direkter Export per Managed Identity
- Storage Account kann zusätzlich per SFTP bereitgestellt werden (anderes Thema)
