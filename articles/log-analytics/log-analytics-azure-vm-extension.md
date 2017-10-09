---
title: aaaConnect Azure sanal makineleri tooLog Analytics | Microsoft Docs
description: "Windows ve Linux için Azure'da çalışan sanal makineler hello toplanan günlüklerinin yolu önerilen ve ölçümleri hello günlük analizi Azure VM uzantısı yüklemektir. Hello Azure portal veya PowerShell tooinstall hello Azure VM üzerine günlük analizi sanal makine uzantısını kullanabilirsiniz."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: ewinner
editor: 
ms.assetid: ca39e586-a6af-42fe-862e-80978a58d9b1
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2017
ms.author: richrund
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ac96c242d03ed3a22ca96368e5a8cc53f9a993db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-azure-virtual-machines-toolog-analytics-with-a-log-analytics-agent"></a>Günlük analizi aracı ile Azure sanal makineleri tooLog Analytics Bağlan

Windows ve Linux bilgisayarlar için hello yöntemi günlüklerinin toplanması için önerilen ve ölçümleri hello günlük analizi aracı yüklemektir.

Hello kolay şekilde tooinstall hello günlük analizi Azure sanal makinelerde hello Log Analytics VM uzantısı aracısıdır.  Merhaba uzantısını kullanarak hello yükleme işlemini basitleştirir ve belirttiğiniz hello Aracısı toosend veri toohello günlük analizi çalışma alanı otomatik olarak yapılandırır. Merhaba aracı ayrıca otomatik olarak hello en son özellikleri ve düzeltmeleri sahip olduktan yükseltilir.

Windows sanal makineler için hello etkinleştirmek *Microsoft İzleme Aracısı* sanal makine uzantısı.
Linux sanal makineleri için hello etkinleştirmek *için OMS Aracısı Linux* sanal makine uzantısı.

Daha fazla bilgi edinmek [Azure sanal makine uzantıları](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ve hello [Linux Aracısı](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Aracı tabanlı koleksiyon için günlük verileri kullandığınızda, yapılandırmalısınız [günlük analizi veri kaynaklarında](log-analytics-data-sources.md) toospecify hello günlüklerini ve ölçümleri toocollect istiyor.

> [!IMPORTANT]
> Günlük analizi tooindex günlük verilerini kullanarak yapılandırırsanız [Azure tanılama](log-analytics-azure-storage.md), ve hello günlükleri iki kez toplandıktan sonra aynı günlükleri, hello Aracısı toocollect hello yapılandırın. Her iki veri kaynakları için ücretlendirilirsiniz. Merhaba aracısı yüklü varsa, yalnızca hello aracı kullanarak günlük verileri toplamak - Azure tanılama günlük analizi toocollect günlük verilerini yapılandırmayın.
>
>

Tooenable hello günlük analizi sanal makine uzantısı kolay üç yolu vardır:

* Hello Azure portal kullanarak
* Azure PowerShell kullanarak
* Bir Azure Resource Manager şablonu kullanarak

## <a name="enable-hello-vm-extension-in-hello-azure-portal"></a>Hello Azure portal Hello VM uzantı etkinleştirilemedi
Günlük analizi için hello aracısı yükleyin ve hello üzerinde çalıştığı hello kullanarak Azure sanal makinesi bağlanın [Azure portal](https://portal.azure.com).

### <a name="tooinstall-hello-log-analytics-agent-and-connect-hello-virtual-machine-tooa-log-analytics-workspace"></a>tooinstall günlük analizi aracı hello ve hello sanal makine tooa günlük analizi çalışma bağlayın
1. Merhaba içine oturum [Azure portal](http://portal.azure.com).
2. Seçin **Gözat** üzerinde hello hello portal ve ardından çok sol tarafı**günlük analizi (OMS)** ve seçin.
3. Günlük analizi çalışma alanları, listeden toouse hello Azure VM ile istediğiniz hello birini seçin.  
   ![OMS çalışma alanları](./media/log-analytics-azure-vm-extension/oms-connect-azure-01.png)
4. Altında **oturum analytics Yönetimi**seçin **sanal makineleri**.  
   ![Sanal makineler](./media/log-analytics-azure-vm-extension/oms-connect-azure-02.png)
5. Merhaba listesinde **sanal makineleri**, hello tooinstall hello Aracısı istediğiniz sanal makinenin seçin. Merhaba **OMS bağlantı durumu** şekilde hello VM gösterir için **bağlı**.  
   ![VM bağlı değil](./media/log-analytics-azure-vm-extension/oms-connect-azure-03.png)
6. Sanal makineniz için Hello ayrıntılarında seçin **Bağlan**. Merhaba Aracısı otomatik olarak yüklenir ve günlük analizi çalışma alanınız için yapılandırılır. Bu işlem hello OMS bağlantı durumu hangi sırada olan birkaç dakika sürer *bağlanıyor...*  
   ![VM Bağlan](./media/log-analytics-azure-vm-extension/oms-connect-azure-04.png)
7. Yükleyip hello aracısına bağlanmak sonra hello **OMS bağlantısı** durum güncelleştirilmiş tooshow olacaktır **bu çalışma**.  
   ![Bağlı](./media/log-analytics-azure-vm-extension/oms-connect-azure-05.png)

## <a name="enable-hello-vm-extension-using-powershell"></a>PowerShell kullanarak hello VM uzantısı etkinleştir
PowerShell kullanarak sanal makineniz yapılandırırken tooprovide hello gerekir **Workspaceıd** ve **workspaceKey**. json yapılandırmanızda Hello özellik adları **büyük küçük harfe duyarlı**.

Merhaba kimliği ve anahtarı üzerinde hello bulabilir **ayarları** sayfasında hello OMS portalı veya hello önceki örnekte gösterildiği gibi PowerShell kullanarak.

![Çalışma alanı kimliği ve birincil anahtar](./media/log-analytics-azure-vm-extension/oms-analyze-azure-sources.png)

Azure Klasik sanal makineleri ve Resource Manager sanal makineleri için farklı komutlar vardır. Aşağıda, Klasik ve Resource Manager sanal makineleri için örnekler verilmiştir.

Klasik sanal makineler için aşağıdaki PowerShell örneğine hello kullan:

```PowerShell
Add-AzureAccount

$workspaceId = "enter workspace ID here"
$workspaceKey = "enter workspace key here"
$hostedService = "enter hosted service here"

$vm = Get-AzureVM –ServiceName $hostedService

# For Windows VM uncomment hello following line
# Set-AzureVMExtension -VM $vm -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionName 'MicrosoftMonitoringAgent' -Version '1.*' -PublicConfiguration "{'workspaceId': '$workspaceId'}" -PrivateConfiguration "{'workspaceKey': '$workspaceKey' }" | Update-AzureVM -Verbose

# For Linux VM uncomment hello following line
# Set-AzureVMExtension -VM $vm -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionName 'OmsAgentForLinux' -Version '1.*' -PublicConfiguration "{'workspaceId': '$workspaceId'}" -PrivateConfiguration "{'workspaceKey': '$workspaceKey' }" | Update-AzureVM -Verbose
```

CLI aşağıdaki hello kullanarak Resource Manager Linux VM'ler için
```azurecli
az vm extension set --resource-group myRGMonitor --vm-name myMonitorVM --name OmsAgentForLinux --publisher Microsoft.EnterpriseCloud.Monitoring --version 1.3 --protected-settings ‘{"workspaceKey": "<workspace-key>"}’ --settings ‘{"workspaceId": "<workspace-id>"}’ 
```

Resource Manager sanal makineler için aşağıdaki PowerShell örneğine hello kullan:

```PowerShell
Login-AzureRMAccount
Select-AzureRMSubscription -SubscriptionId "**"

$workspaceName = "your workspace name"
$VMresourcegroup = "**"
$VMresourcename = "**"

$workspace = (Get-AzureRmOperationalInsightsWorkspace).Where({$_.Name -eq $workspaceName})

if ($workspace.Name -ne $workspaceName)
{
    Write-Error "Unable toofind OMS Workspace $workspaceName. Do you need toorun Select-AzureRMSubscription?"
}

$workspaceId = $workspace.CustomerId
$workspaceKey = (Get-AzureRmOperationalInsightsWorkspaceSharedKeys -ResourceGroupName $workspace.ResourceGroupName -Name $workspace.Name).PrimarySharedKey

$vm = Get-AzureRmVM -ResourceGroupName $VMresourcegroup -Name $VMresourcename
$location = $vm.Location

# For Windows VM uncomment hello following line
# Set-AzureRmVMExtension -ResourceGroupName $VMresourcegroup -VMName $VMresourcename -Name 'MicrosoftMonitoringAgent' -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionType 'MicrosoftMonitoringAgent' -TypeHandlerVersion '1.0' -Location $location -SettingString "{'workspaceId': '$workspaceId'}" -ProtectedSettingString "{'workspaceKey': '$workspaceKey'}"

# For Linux VM uncomment hello following line
# Set-AzureRmVMExtension -ResourceGroupName $VMresourcegroup -VMName $VMresourcename -Name 'OmsAgentForLinux' -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionType 'OmsAgentForLinux' -TypeHandlerVersion '1.0' -Location $location -SettingString "{'workspaceId': '$workspaceId'}" -ProtectedSettingString "{'workspaceKey': '$workspaceKey'}"


```


## <a name="deploy-hello-vm-extension-using-a-template"></a>Bir şablon kullanarak hello VM uzantısı dağıtma
Azure Kaynak Yöneticisi'ni kullanarak hello dağıtım ve uygulamanızın yapılandırmasını tanımlayan bir şablon (JSON biçiminde) oluşturabilirsiniz. Bu şablon Resource Manager şablonu olarak bilinir ve bildirim temelli yolu toodefine dağıtılmasını sağlar. Bir şablon kullanarak, sürekli olarak hello uygulama yaşam döngüsü boyunca uygulamanızı dağıtmak ve kaynaklarınızın tutarlı bir durumda dağıtılması emin olabilirsiniz.

Merhaba günlük analizi aracı, Resource Manager şablonu bir parçası olarak dahil ederek, her bir sanal makine önceden yapılandırılmış tooreport tooyour günlük analizi çalışma alanı olduğundan emin olabilirsiniz.

Resource Manager şablonları hakkında daha fazla bilgi için bkz: [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md).

Windows hello yüklü Microsoft İzleme Aracısı uzantısı ile çalışan bir sanal makine dağıtmak için kullanılan bir Resource Manager şablonu örneği verilmiştir. Bu şablon bir tipik sanal makine şablonuyla eklemeleri aşağıdaki hello şöyledir:

* Workspaceıd ve workspaceName parametreleri
* Microsoft.EnterpriseCloud.Monitoring kaynak uzantısı bölümü
* Merhaba Workspaceıd ve workspaceSharedKey çıkışları toolook

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "adminUsername": {
      "type": "string",
      "metadata": {
        "description": "Username for hello Virtual Machine."
      }
    },
    "adminPassword": {
      "type": "securestring",
      "metadata": {
        "description": "Password for hello Virtual Machine."
      }
    },
    "dnsLabelPrefix": {
       "type": "string",
       "metadata": {
          "description": "DNS Label for hello Public IP. Must be lowercase. It should match with hello following regular expression: ^[a-z][a-z0-9-]{1,61}[a-z0-9]$ or it will raise an error."
       }
    },
    "workspaceId": {
      "type": "string",
      "metadata": {
        "description": "OMS workspace ID"
      }
    },
    "workspaceName": {
      "type": "string",
      "metadata": {
         "description": "OMS workspace name"
      }
    },
    "windowsOSVersion": {
      "type": "string",
      "defaultValue": "2012-R2-Datacenter",
      "allowedValues": [
        "2008-R2-SP1",
        "2012-Datacenter",
        "2012-R2-Datacenter",
        "Windows-Server-Technical-Preview"
      ],
      "metadata": {
        "description": "hello Windows version for hello VM. This will pick a fully patched image of this given Windows version. Allowed values: 2008-R2-SP1, 2012-Datacenter, 2012-R2-Datacenter, Windows-Server-Technical-Preview."
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]",
    "apiVersion": "2015-06-15",
    "imagePublisher": "MicrosoftWindowsServer",
    "imageOffer": "WindowsServer",
    "OSDiskName": "osdiskforwindowssimple",
    "nicName": "myVMNic",
    "addressPrefix": "10.0.0.0/16",
    "subnetName": "Subnet",
    "subnetPrefix": "10.0.0.0/24",
    "storageAccountType": "Standard_LRS",
    "publicIPAddressName": "myPublicIP",
    "publicIPAddressType": "Dynamic",
    "vmStorageAccountContainerName": "vhds",
    "vmName": "MyWindowsVM",
    "vmSize": "Standard_DS1",
    "virtualNetworkName": "MyVNET",
    "resourceId": "[resourceGroup().id]",
    "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
    "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables('subnetName'))]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "[variables('apiVersion')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "accountType": "[variables('storageAccountType')]"
      }
    },
    {
      "apiVersion": "[variables('apiVersion')]",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIPAddressName')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
        "dnsSettings": {
          "domainNameLabel": "[parameters('dnsLabelPrefix')]"
        }
      }
    },
    {
      "apiVersion": "[variables('apiVersion')]",
      "type": "Microsoft.Network/virtualNetworks",
      "name": "[variables('virtualNetworkName')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "addressSpace": {
          "addressPrefixes": [
            "[variables('addressPrefix')]"
          ]
        },
        "subnets": [
          {
            "name": "[variables('subnetName')]",
            "properties": {
              "addressPrefix": "[variables('subnetPrefix')]"
            }
          }
        ]
      }
    },
    {
      "apiVersion": "[variables('apiVersion')]",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[variables('nicName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'))]",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
      ],
      "properties": {
        "ipConfigurations": [
          {
            "name": "ipconfig1",
            "properties": {
              "privateIPAllocationMethod": "Dynamic",
              "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses',variables('publicIPAddressName'))]"
              },
              "subnet": {
                "id": "[variables('subnetRef')]"
              }
            }
          }
        ]
      }
    },
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Compute/virtualMachines",
      "name": "[variables('vmName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
        "[concat('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
      ],
      "properties": {
        "hardwareProfile": {
          "vmSize": "[variables('vmSize')]"
        },
        "osProfile": {
          "computername": "[variables('vmName')]",
          "adminUsername": "[parameters('adminUsername')]",
          "adminPassword": "[parameters('adminPassword')]"
        },
        "storageProfile": {
          "imageReference": {
            "publisher": "[variables('imagePublisher')]",
            "offer": "[variables('imageOffer')]",
            "sku": "[parameters('windowsOSVersion')]",
            "version": "latest"
          },
          "osDisk": {
            "name": "osdisk",
            "vhd": {
              "uri": "[concat('http://',variables('storageAccountName'),'.blob.core.windows.net/',variables('vmStorageAccountContainerName'),'/',variables('OSDiskName'),'.vhd')]"
            },
            "caching": "ReadWrite",
            "createOption": "FromImage"
          }
        },
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]"
            }
          ]
        },
        "diagnosticsProfile": {
          "bootDiagnostics": {
             "enabled": "true",
             "storageUri": "[concat('http://',variables('storageAccountName'),'.blob.core.windows.net')]"
          }
        }
      },
      "resources": [
        {
          "type": "extensions",
          "name": "Microsoft.EnterpriseCloud.Monitoring",
          "apiVersion": "[variables('apiVersion')]",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
          ],
          "properties": {
            "publisher": "Microsoft.EnterpriseCloud.Monitoring",
            "type": "MicrosoftMonitoringAgent",
            "typeHandlerVersion": "1.0",
            "autoUpgradeMinorVersion": true,
            "settings": {
              "workspaceId": "[parameters('workspaceId')]"
            },
            "protectedSettings": {
              "workspaceKey": "[listKeys(resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspaceName')), '2015-03-20').primarySharedKey]"
            }
          }
        }
      ]
    }
  ],
  "outputs": {
      "sharedKeyOutput": {
         "value": "[listKeys(resourceId('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName')), '2015-03-20').primarySharedKey]",
         "type": "string"
      },
      "workspaceIdOutput": {
         "value": "[reference(concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName')), '2015-03-20').customerId]",
        "type" : "string"
      }
  }
}
```

Bir şablonu PowerShell komutunu aşağıdaki hello kullanarak dağıtabilirsiniz:

```PowerShell
New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath
```

## <a name="troubleshooting-hello-log-analytics-vm-extension"></a>Merhaba günlük analizi VM uzantısı sorunlarını giderme
Genellikle Azure portalında veya Azure powershell şeyler çalışmıyor zaman bir ileti alırsınız.

1. Merhaba içine oturum [Azure portal](http://portal.azure.com).
2. Merhaba VM bulun ve VM Ayrıntıları'nı açın.
3. Tıklatın **uzantıları** OMS uzantısı veya etkinleştirilirse toocheck.

   ![VM uzantısı görünümü](./media/log-analytics-azure-vm-extension/oms-vmview-extensions.png)

4. Merhaba tıklatın *MicrosoftMonitoringAgent*(Windows) veya *OmsAgentForLinux*(Linux) uzantısı ve görünüm ayrıntıları. 

   ![VM uzantısı ayrıntıları](./media/log-analytics-azure-vm-extension/oms-vmview-extensiondetails.png)

### <a name="troubleshooting-windows-virtual-machines"></a>Sorun giderme Windows sanal makineler
Merhaba, *Microsoft İzleme Aracısı* VM Aracısı uzantısı yükleme değil veya raporlama, aşağıdaki adımları tootroubleshoot hello sorunu hello gerçekleştirebilirsiniz.

1. Hello Azure VM aracısının yüklü olduğundan ve doğru şekilde de hello kullanarak çalışma adımları denetleyin [KB 2965986](https://support.microsoft.com/kb/2965986#mt1).
   * Merhaba VM aracı günlük dosyasını gözden geçirebilirsiniz`C:\WindowsAzure\logs\WaAppAgent.log`
   * Merhaba günlük yoksa hello VM aracısı yüklü değil.
     * [Klasik sanal makinelerin Hello Azure VM Aracısı yükleme](../virtual-machines/windows/classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
2. Merhaba uzantısı sinyal görev hello aşağıdaki adımları kullanarak çalışan Microsoft Monitoring Agent onaylayın:
   * Toohello sanal makinede oturum açın
   * Görev Zamanlayıcısı'nı açın ve hello bulur `update_azureoperationalinsight_agent_heartbeat` görevi
   * Hello görev etkinleştirilir ve bir dakikada çalıştığını onaylayın
   * Merhaba sinyal günlük dosyası iade etme`C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\heartbeat.log`
3. Merhaba Microsoft İzleme Aracısı VM uzantısı günlük dosyalarını inceleyin`C:\Packages\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent`
4. Merhaba sanal makine PowerShell betikleri çalıştırabilirsiniz emin olun
5. C:\Windows\temp izinlerini değiştirmezsiniz emin olun
6. Komutu yükseltilmiş bir PowerShell penceresinde hello sanal makinede aşağıdaki hello yazarak Microsoft İzleme Aracısı hello hello durumunu görüntüleme`  (New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg').GetCloudWorkspaces() | Format-List`
7. Merhaba Microsoft Monitoring Agent Kurulum günlük dosyalarını inceleyin`C:\Windows\System32\config\systemprofile\AppData\Local\SCOM\Logs`

Daha fazla bilgi için bkz: [Windows uzantıları sorun giderme](../virtual-machines/windows/extensions-troubleshoot.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

### <a name="troubleshooting-linux-virtual-machines"></a>Linux sanal makineleri sorunlarını giderme
Merhaba, *Linux için OMS aracısının* VM Aracısı uzantısı yükleme değil veya raporlama, aşağıdaki adımları tootroubleshoot hello sorunu hello gerçekleştirebilirsiniz.

1. Merhaba uzantı durumu ise *bilinmeyen* hello Azure VM aracısı yüklü olup olmadığını denetleyin ve doğru şekilde hello VM aracı günlük dosyasını gözden geçirerek çalışma`/var/log/waagent.log`
   * Merhaba günlük yoksa hello VM aracısı yüklü değil.
   * [Linux VM'ler Hello Azure VM Aracısı yükleme](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
2. Sağlıksız diğer durumlar için Linux VM uzantısı için gözden geçirme hello OMS aracısının günlük dosyaları `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/extension.log` ve`/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/CommandExecution.log`
3. Merhaba uzantı durumu sağlam ancak veri karşıya Linux oturum açmak için dosyaları hello OMS Aracısı gözden geçirin`/var/opt/microsoft/omsagent/log/omsagent.log`

## <a name="next-steps"></a>Sonraki adımlar
* Yapılandırma [günlük analizi veri kaynaklarında](log-analytics-data-sources.md) toospecify hello günlüklerini ve ölçümleri toocollect.
* sanal makineler toogather verileri [hello Çözümleri Galerisi eklemek günlük analizi çözümleri](log-analytics-add-solutions.md).
* [Azure Tanılama'yı kullanarak verileri toplamak](log-analytics-azure-storage.md) Azure'da çalışan diğer kaynaklar için.

Azure'da olmayan bilgisayarlar için hello günlük analizi aracı makaleler hello açıklanan hello yöntemleri kullanarak yükleyebilirsiniz:

* [Windows bilgisayarları tooLog Analytics Bağlan](log-analytics-windows-agents.md)
* [Linux bilgisayarları tooLog Analytics Bağlan](log-analytics-linux-agents.md)
