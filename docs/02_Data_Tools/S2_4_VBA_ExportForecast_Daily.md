# S2.4 — Automatisation VBA : Export Quotidien du Forecast  
NOVAFOOD GLOBAL — Automatisation du process Forecast → Reporting

---

## 🎯 Objectif du cas

Automatiser le **processus d’export quotidien** des prévisions NOVAFOOD Europe vers :

- un fichier Excel formaté pour les équipes Sales & Marketing,
- un CSV ingérable par SAP / Oracle / Sofco,
- un dossier d’archives automatique (traçabilité).

L’automatisation doit :

- être déclenchée en un clic (ou automatiquement à l’ouverture),
- générer un **export propre, sécurisé, horodaté**,  
- réduire les erreurs manuelles,
- fiabiliser les inputs du processus **S&OP Europe**.

---

# 1. Structure du fichier Excel à automatiser

📂 Fichier source :  
`excel_templates/forecasting_models/Forecast_Europe_Master.xlsx`

Il contient :

- **Feuille `Forecast_Final`** → résultat final du consensus S&OP
- **Feuille `Metadata`** → informations système (version, auteur)
- Des données provenant :
  - de Power Query (actuals, historiques),
  - de Power Pivot (DAX, mesures),
  - des inputs Sales/Marketing

---

# 2. Travail demandé — Étapes détaillées

---

## 🔵 Étape 1 — Création du dossier d’exports automatiques

Chemin local recommandé :


C:\NOVAFOOD\Forecast_Exports
├── Daily
├── Archive
└── Logs\


📌 *L’automatisation doit créer les dossiers si nécessaire.*

---

## 🔵 Étape 2 — Macro VBA de nettoyage & préparation

Avant export, le fichier doit :

- rafraîchir Power Query :  
  `ActiveWorkbook.RefreshAll`

- recalculer les mesures :  
  `Application.CalculateFull`

- vérifier la présence des colonnes obligatoires :

  - Date  
  - Country  
  - SKU  
  - Forecast_Final  

- nettoyer les formats (dates, décimales, SKU)

Exemple de code :

```VBA
Sub Prepare_Forecast_Data()

    Sheets("Forecast_Final").Select
    
    ' Vérifier colonnes essentielles
    If WorksheetFunction.CountA(Range("A1:D1")) < 4 Then
        MsgBox "Colonnes obligatoires manquantes.", vbCritical
        Exit Sub
    End If
    
    ' Rafraîchir les données Power Query
    ActiveWorkbook.RefreshAll
    
    ' Recalcul complet
    Application.CalculateFull
    
End Sub


🔵 Étape 3 — Macro d’export Excel

Objectif :
Créer un fichier export propre avec horodatage :

Format :

Forecast_EXPORT_EU_YYYYMMDD.xlsx


Code recommandé :

Sub Export_Forecast_Excel()

    Dim exportPath As String
    Dim fileName As String
    
    exportPath = "C:\NOVAFOOD\Forecast_Exports\Daily\"
    fileName = "Forecast_EXPORT_EU_" & Format(Now(), "yyyymmdd") & ".xlsx"
    
    Sheets("Forecast_Final").Copy
    ActiveWorkbook.SaveAs Filename:=exportPath & fileName, FileFormat:=xlOpenXMLWorkbook
    ActiveWorkbook.Close False
    
    MsgBox "Export Excel généré avec succès : " & fileName, vbInformation

End Sub

🔵 Étape 4 — Export CSV SAP / Oracle

Certaines équipes IT préfèrent un export CSV normalisé.

Colonnes obligatoires :

Date (YYYY-MM-DD)

SKU

Country

Forecast

Channel

Version (SOP / Consensus / Stat)

Code :

Sub Export_Forecast_CSV()

    Dim exportPath As String
    Dim fileName As String
    
    exportPath = "C:\NOVAFOOD\Forecast_Exports\Daily\"
    fileName = "Forecast_EU_SAP_" & Format(Now(), "yyyymmdd") & ".csv"
    
    Sheets("Forecast_Final").Copy
    ActiveWorkbook.SaveAs Filename:=exportPath & fileName, FileFormat:=xlCSVUTF8
    ActiveWorkbook.Close False
    
End Sub

🔵 Étape 5 — Archivage automatique

Objectif :
Garder une copie de chaque export dans un dossier dédié.

Code :

Sub Archive_Export()

    Dim sourceFile As String
    Dim archivePath As String
    
    sourceFile = "C:\NOVAFOOD\Forecast_Exports\Daily\"
    archivePath = "C:\NOVAFOOD\Forecast_Exports\Archive\"
    
    FileCopy sourceFile & "Forecast_EXPORT_EU_" & Format(Now(), "yyyymmdd") & ".xlsx", _
            archivePath & "Forecast_EXPORT_EU_" & Format(Now(), "yyyymmdd_hhmmss") & ".xlsx"
    
End Sub

🔵 Étape 6 — Macro globale “One-Click Forecast Export”

Créer un bouton : Exporter Forecast (1 Click)

Code combiné :

Sub Export_Forecast_OneClick()

    Call Prepare_Forecast_Data
    Call Export_Forecast_Excel
    Call Export_Forecast_CSV
    Call Archive_Export
    
    MsgBox "Processus complet d'export NOVAFOOD terminé.", vbInformation

End Sub

3. Livrables attendus

Macro complète :
excel_templates/VBA_macros/S2_4_ExportForecast_Daily.bas

Fichier Excel automatisé :
excel_templates/forecasting_models/Forecast_Europe_Master.xlsm

Documentation utilisateur :
docs/02_Data_Tools/S2_4_UserGuide.md

4. Critères d’évaluation

✔ Code VBA propre, commenté, robuste
✔ Export fiable & horodaté
✔ Pas d’intervention humaine nécessaire
✔ Process compatible S&OP NOVAFOOD
✔ Archivage & traçabilité OK
✔ Capacité à gérer les erreurs (QRQC)

5. Extension (niveau expert)

planification via Windows Task Scheduler

appui d’un script Python pour automatiser côté serveur

export JSON pour API Oracle / SAP IBP

ajout d’un log détaillé (succès / erreurs / durée de calcul)