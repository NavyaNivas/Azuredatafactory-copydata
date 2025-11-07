Every month, your team gets a folder in Azure Blob Storage with multiple CSV files for different regions (e.g., “RegionA_2025-11.csv”, “RegionB_2025-11.csv”, etc.). You need to load each file into an Azure SQL table. But before loading, you must validate that each file meets criteria (has header row, minimum row count, correct file size). If any file fails validation, you should trigger an alert and stop processing. After successful load for all files, send a notification.
Activities to use:
•	Get Metadata – to retrieve file list, file size, row count metadata.
•	ForEach – to iterate over each file in the folder.
•	Within ForEach:
o	Validation – to check if header exists (e.g., row count > 1) or file size > threshold.
o	If Condition – branch: if validation passes → Copy Activity; else → Fail activity or you might call Web activity to send alert.
o	Copy Data – to load the validated file to Azure SQL.
•	After ForEach completes: Web (or ExecutePipeline) to call notification service.
