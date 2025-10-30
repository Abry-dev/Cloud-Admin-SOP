# Azure: Automation and Clean-up

1.  Open **PowerShell on Azure**
    1.  Run: `Get-AzVM -ResourceGroupName “RG-Support-1” | Stop-AzVM -Force`
    2.  Then run: `az group delete –name RG-Support-1 –yes –no-wait`
