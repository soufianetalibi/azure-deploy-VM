# azure-deploy-VM

git remote add origin https://github.com/soufianetalibi/azure-deploy-VM.git

git add .

git status 

git commit -m "Mise a jour"

git branch -M main

git push -u origin main

==================================================================================================

comment lier gitHUB avec mon abonnement azure ?

se connecter sur azure powershell : 

az login --tenant 1324dfb4-4457-41c3-a943-293c61bbd70c --use-device-code

az account list --output table
az vm list -d --output table

============================================

créer un SPN sur azure pour GitHub : (compte de service)

az ad sp create-for-rbac --name "github-actions-sp" --role contributor --scopes /subscriptions/c5346ccd-9bc4-4053-91da-8ab9be9ab95e --sdk-auth

==>ceci va créer une app registration et un SP associé et accorder le rôle contributeur à ce SP

puis va génère un JSON :  

{
  "clientId": "xxxxxx",
  
  "clientSecret": "xxxxx",
  
  "subscriptionId": "xxxxx",
  
  "tenantId": "xxxxx",
  
  "activeDirectoryEndpointUrl": "https://login.microsoftonline.com",
  
  "resourceManagerEndpointUrl": "https://management.azure.com/",
  
  "activeDirectoryGraphResourceId": "https://graph.windows.net/",
  
  "sqlManagementEndpointUrl": "https://management.core.windows.net:8443/",
  
  "galleryEndpointUrl": "https://gallery.azure.com/",
  
  "managementEndpointUrl": "https://management.core.windows.net/"
  
}

-->créer un secret sur gitHUB "AZURE_CREDENTIALS" contenant ce JSON

Ensuite créer les workflows deploy-VM et delete-VM manage-VM...

pour tester : 

sur le dépôt / menu actions / executer le workflow "deploy-vm" ...

ceci me permet de faire des déploiments des plusieurs services sur azure, sauvegarder les VMs, monitorer ...

===== le workflow backup-vm.yml
Ce workflow est manuel, il sauvegarde les disques OS :
pour toutes les VMs du Resource Group
 Le disque OS uniquement (pas les disques DATA)
  Sous forme de snapshots Azure
  placé dans le même resource group
  Dans la même région
 





