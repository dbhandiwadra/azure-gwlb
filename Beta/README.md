# **Azure Gateway Load Balancer**

## **Phase:** Beta(preview)

**Steps:**
1. **Create resource-group in "eastus2euap" region** 

az group create --name <resource-group> --location "eastus2euap"

2. **Provider Deployment**

az deployment group create --name providertemplate --resource-group <resource-group> --template-file provider-simple-lb.json
--parameters adminUsername=<user_name> adminPassword=<password> vmName=<vmseries-name> 
customDataField=storage-account=<storagaccname>,access-key=<storageaccesskey>,file-share=<filesharename>,share-directory=.

3. **Consumer side Deployment**

az deployment group create --name consumertemplate --resource-group <resource-group> --template-file consumer-simple-lb.json 
--parameters adminUsername=<user_name> adminPassword=<password> providerResourceGroup=<resource-group>

**Requirements:**

- Minimum of PAN-OS 10.1.2 and vm-series plugin 2.1.2 is required

**init-cfg data:**

plugin-op-commands=azure-gwlb-inspect:enable+internal-port-2000+external-port-2001+internal-vni-800,external-vni-801

## **Documentation Reference:**


