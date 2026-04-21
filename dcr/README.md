# CREATE THE DCR WITH AZCLI
```
az monitor data-collection rule create \
  --name dcr-insightsmetrics \
  --resource-group <RG_NAME> \
  --location eastus2 \
  --rule-file insightsmetrics-dcr.json
```

# ASSOCIATE THE DCR TO VM
```
az monitor data-collection rule association create \
  --name dcr-association \
  --resource-group <RG_NAME> \
  --rule-name dcr-insightsmetrics \
  --resource /subscriptions/<SUB_ID>/resourceGroups/<RG_NAME>/providers/Microsoft.Compute/virtualMachines/<VM_NAME>
```

# VALIDATE DATA IS FLOWING TO INSIGHT METRICS TABLE IN YOUR LAW
```
InsightsMetrics
| where TimeGenerated > ago(15m)
| summarize count() by Computer, Namespace
```
