---
title: "Windows sanal makine ölçek kümeleri aaaAutoscale | Microsoft Docs"
description: "Bir Windows sanal makine ölçek Azure PowerShell kullanarak ayarlamak için otomatik ölçeklendirmeyi ayarlayalım ayarlayın"
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 88886cad-a2f0-46bc-8b58-32ac2189fc93
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: adegeo
ms.openlocfilehash: 67cf1c5063ceba4fc076dc270090defdbddbcfe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-scale-machines-in-a-virtual-machine-scale-set"></a>Bir sanal makine ölçek kümesindeki makineleri otomatik olarak ölçeklendirin
Sanal makine ölçek kümeleri sizin için toodeploy kolaylaştırır ve aynı sanal makineleri bir küme olarak yönetin. Ölçek kümeleri ölçekte uygulamalar için yüksek oranda ölçeklenebilir ve özelleştirilebilir bilgi işlem katmanını sağlar ve Windows platform görüntüleri, Linux platform görüntüleri, özel resimler ve uzantıları destekler. Ölçek kümeleri hakkında daha fazla bilgi için bkz: [sanal makine ölçek ayarlar](virtual-machine-scale-sets-overview.md).

Bu öğretici toocreate Windows sanal makineler ve otomatik olarak ölçek hello hello makinelerinizde ölçek kümesi nasıl ayarlanacağını gösterir. Ve Azure Resource Manager şablonu oluşturma ve Azure PowerShell kullanarak dağıtmayı ölçeklendirmeyi ayarlayın hello ölçeği oluşturun. Şablonlar hakkında daha fazla bilgi için bkz. [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md). Otomatik ölçek kümesi ölçeklendirme hakkında daha fazla toolearn bkz [otomatik ölçeklendirme ve sanal makine ölçek ayarlar](virtual-machine-scale-sets-autoscale-overview.md).

Bu makalede, dağıttığınız hello aşağıdaki kaynaklar ve uzantıları:

* Microsoft.Storage/storageAccounts
* Microsoft.Network/virtualNetworks
* Microsoft.Network/publicIPAddresses
* Microsoft.Network/loadBalancers
* Microsoft.Network/networkInterfaces
* Microsoft.Compute/virtualMachines
* Microsoft.Compute/virtualMachineScaleSets
* Microsoft.Insights.VMDiagnosticsSettings
* Microsoft.Insights/autoscaleSettings

Resource Manager kaynakları hakkında daha fazla bilgi için bkz: [Azure Resource Manager ve klasik dağıtım](../azure-resource-manager/resource-manager-deployment-model.md).

## <a name="step-1-install-azure-powershell"></a>1. adım: Azure PowerShell'i yükleme
Bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) hello Azure PowerShell'in en son sürümünü yükleme, aboneliğinizi seçme ve tooAzure içinde imzalama hakkında bilgi.

## <a name="step-2-create-a-resource-group-and-a-storage-account"></a>2. adım: bir kaynak grubu ve bir depolama hesabı oluşturma
1. **Bir kaynak grubu oluşturmak** – tüm kaynakları dağıtılan tooa kaynak grubu olmalıdır. Kullanım [New-AzureRmResourceGroup](https://msdn.microsoft.com/library/mt603739.aspx) bir kaynak grubu adında toocreate **vmsstestrg1**.
2. **Depolama hesabı oluşturma** – bu depolama hesabını hello şablon depolandığı yerdir. Kullanım [New-AzureRmStorageAccount](https://msdn.microsoft.com/library/mt607148.aspx) bir depolama hesabı adlı toocreate **vmsstestsa**.

## <a name="step-3-create-hello-template"></a>3. adım: hello şablonu oluşturma
Bir Azure Resource Manager şablonu, toodeploy mümkün kılar ve hello kaynakları ve ilişkili dağıtım parametreleri JSON açıklamasını kullanarak Azure kaynaklarını birlikte yönetebilirsiniz.

1. Sık kullanılan düzenleyicinizde hello dosya C:\VMSSTemplate.json oluşturun ve hello ilk JSON yapısı toosupport hello şablonu ekleyin.

    ```json
    {
      "$schema":"http://schema.management.azure.com/schemas/2014-04-01-preview/VM.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
      },
      "variables": {
      },
      "resources": [
      ]
    }
    ```

2. Parametreler her zaman gerekli değildir, ancak hello şablon dağıtıldığında değerleri yolu tooinput sağlarlar. Bu parametreleri toohello şablonu eklediğiniz hello parametreleri üst öğenin altında ekleyin.

    ```json   
    "vmName": { "type": "string" },
    "vmSSName": { "type": "string" },
    "instanceCount": { "type": "string" },
    "adminUsername": { "type": "string" },
    "adminPassword": { "type": "securestring" },
    "resourcePrefix": { "type": "string" }
    ```
   
    * Merhaba ayrı sanal makineyi hello ölçek kümesinde kullanılan tooaccess hello makineler için bir ad.
    * Merhaba şablon depolandığı hello depolama hesabını Hello adı.
    * sanal makineler tooinitially Hello sayıda hello ölçek kümesindeki oluşturun.
    * Merhaba adı ve hello sanal makinelerde hello yönetici hesabının parolası.
    * Toosupport hello ölçek oluşturulan hello kaynaklar için bir ad önekini ayarlayın.

3. Değişkenleri, sık sık değişebilir bir şablonu toospecify değerlerini kullanılabilir veya parametre değerlerini birleşiminden toobe gereken değerleri oluşturulur. Bu değişkenler toohello şablonu eklediğiniz hello değişkenleri üst öğenin altında ekleyin.

    ```json
    "dnsName1": "[concat(parameters('resourcePrefix'),'dn1')]",
    "dnsName2": "[concat(parameters('resourcePrefix'),'dn2')]",
    "publicIP1": "[concat(parameters('resourcePrefix'),'ip1')]",
    "publicIP2": "[concat(parameters('resourcePrefix'),'ip2')]",
    "loadBalancerName": "[concat(parameters('resourcePrefix'),'lb1')]",
    "virtualNetworkName": "[concat(parameters('resourcePrefix'),'vn1')]",
    "nicName": "[concat(parameters('resourcePrefix'),'nc1')]",
    "lbID": "[resourceId('Microsoft.Network/loadBalancers',variables('loadBalancerName'))]",
    "frontEndIPConfigID": "[concat(variables('lbID'),'/frontendIPConfigurations/loadBalancerFrontEnd')]",
    "storageAccountSuffix": [ "a", "g", "m", "s", "y" ],
    "diagnosticsStorageAccountName": "[concat(parameters('resourcePrefix'), 'a')]",
    "accountid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/','Microsoft.Storage/storageAccounts/', variables('diagnosticsStorageAccountName'))]",
      "wadlogs": "<WadCfg> <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" /></WindowsEventLog>",
    "wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\% Processor Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU utilization\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
    "wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
    "wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
    "wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"
    ```
   
    * Merhaba ağ arabirimleri tarafından kullanılan DNS adları.

        * Başlangıç IP adresi adları ve önekleri hello sanal ağ ve alt ağları için.
        * Merhaba adları ve tanımlayıcıları hello sanal ağ, yük dengeleyici ve ağ arabirimleri.
        * Merhaba ölçek kümesindeki hello makinelerle ilişkili hello hesapları için depolama hesabı adları.
        * Merhaba hello sanal makinelerde yüklü tanılama uzantısını yönelik ayarlar. Merhaba tanılama uzantısını hakkında daha fazla bilgi için bkz: [izleme ve tanılama Azure Resource Manager şablonu kullanarak bir Windows sanal makine oluşturma](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

4. Toohello şablonu eklediğiniz hello kaynakları üst öğenin altında Hello depolama hesabı kaynak ekleyin. Bu şablon, hello işletim sistemi disklerinde ve tanılama verilerinin depolandığı beş depolama hesapları önerilen bir döngü toocreate hello kullanır. Bu hesapları kümesi too100 hello geçerli en büyük bir ölçek kümesindeki sanal makineleri yedeklemek destekleyebilir. Her Depolama hesabı hello şablonu için başlangıç parametreleri sağlayın hello öneki ile birleştirilmiş hello değişkenlerine tanımlandı harf göstergesi ile adlandırılır.

    ```json
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat(parameters('resourcePrefix'), variables('storageAccountSuffix')[copyIndex()])]",
      "apiVersion": "2015-06-15",
      "copy": {
        "name": "storageLoop",
        "count": 5
      },
      "location": "[resourceGroup().location]",
      "properties": { "accountType": "Standard_LRS" }
    },
    ```

5. Merhaba sanal ağ kaynağı ekleyin. Daha fazla bilgi için bkz: [ağ kaynak sağlayıcısı](../virtual-network/resource-groups-networking.md).

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Network/virtualNetworks",
      "name": "[variables('virtualNetworkName')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "addressSpace": { "addressPrefixes": [ "10.0.0.0/16" ] },
        "subnets": [
          {
            "name": "subnet1",
            "properties": { "addressPrefix": "10.0.0.0/24" }
          }
        ]
      }
    },
    ```

6. Hello tarafından kullanılan hello ortak IP adresi kaynakları yük dengeleyici ve ağ arabirimi ekleyin.

    ```json
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIP1')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "publicIPAllocationMethod": "Dynamic",
        "dnsSettings": {
          "domainNameLabel": "[variables('dnsName1')]"
        }
      }
    },
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIP2')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "publicIPAllocationMethod": "Dynamic",
        "dnsSettings": {
          "domainNameLabel": "[variables('dnsName2')]"
        }
      }
    },
    ```

7. Merhaba ölçek kümesi tarafından kullanılan hello yük dengeleyici kaynak ekleyin. Daha fazla bilgi için bkz: [yük dengeleyici için Azure Resource Manager desteği](../load-balancer/load-balancer-arm.md).

    ```json   
    {
      "apiVersion": "2015-06-15",
      "name": "[variables('loadBalancerName')]",
      "type": "Microsoft.Network/loadBalancers",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIP1'))]"
      ],
      "properties": {
        "frontendIPConfigurations": [
          {
            "name": "loadBalancerFrontEnd",
            "properties": {
              "publicIPAddress": {
                "id": "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIP1'))]"
              }
            }
          }
        ],
        "backendAddressPools": [ { "name": "bepool1" } ],
        "inboundNatPools": [
          {
            "name": "natpool1",
            "properties": {
              "frontendIPConfiguration": {
                "id": "[variables('frontEndIPConfigID')]"
              },
              "protocol": "tcp",
              "frontendPortRangeStart": 50000,
              "frontendPortRangeEnd": 50500,
              "backendPort": 3389
            }
          }
        ]
      }
    },
    ```

8. Merhaba ayrı sanal makine tarafından kullanılan hello ağ arabirimi kaynağı ekleyin. Makineler ölçek kümesindeki bir ortak IP adresi üzerinden erişilebilir değil çünkü ayrı bir sanal makine hello aynı sanal oluşturulan tooremotely erişim hello makinelerin ağ.

    ```json  
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[variables('nicName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIP2'))]",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
      ],
      "properties": {
        "ipConfigurations": [
          {
            "name": "ipconfig1",
            "properties": {
              "privateIPAllocationMethod": "Dynamic",
              "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicIP2'))]"
              },
              "subnet": {
                "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/virtualNetworks/',variables('virtualNetworkName'),'/subnets/subnet1')]"
              }
            }
          }
        ]
      }
    },
    ```

9. Merhaba ayrı sanal makine aynı hello ölçek kümesi olarak ağ hello ekleyin.

    ```json
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Compute/virtualMachines",
      "name": "[parameters('vmName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "storageLoop",
        "[concat('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
      ],
      "properties": {
        "hardwareProfile": { "vmSize": "Standard_A1" },
        "osProfile": {
          "computername": "[parameters('vmName')]",
          "adminUsername": "[parameters('adminUsername')]",
          "adminPassword": "[parameters('adminPassword')]"
        },
        "storageProfile": {
          "imageReference": {
            "publisher": "MicrosoftWindowsServer",
            "offer": "WindowsServer",
            "sku": "2012-R2-Datacenter",
            "version": "latest"
          },
          "osDisk": {
            "name": "[concat(parameters('resourcePrefix'), 'os1')]",
            "vhd": {
              "uri":  "[concat('https://',parameters('resourcePrefix'),'a.blob.core.windows.net/vhds/',parameters('resourcePrefix'),'os1.vhd')]"
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
        }
      }
    },
    ```

10. Kaynak Hello sanal makine ölçek kümesi ekleyin ve hello ölçek grubundaki tüm sanal makinelerde yüklü hello tanılama uzantısını belirtin. Bu kaynak için hello ayarlarının pek çoğu hello sanal makine kaynağı ile benzerdir. Merhaba temel farklar hello ölçek kümesindeki sanal makinelerin hello sayısını belirtir hello kapasite öğesi ve güncelleştirmeleri toovirtual makineler nasıl yapılacağını belirten upgradePolicy ' dir. Tüm hello depolama hesapları oluşturulana kadar hello ölçek kümesini oluşturulmaz belirtildiği gibi hello dependsOn öğeye sahip.

    ```json
    {
      "type": "Microsoft.Compute/virtualMachineScaleSets",
      "apiVersion": "2016-03-30",
      "name": "[parameters('vmSSName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "storageLoop",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]",
        "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]"
      ],
      "sku": {
        "name": "Standard_A1",
        "tier": "Standard",
        "capacity": "[parameters('instanceCount')]"
      },
      "properties": {
        "upgradePolicy": {
          "mode": "Manual"
        },
        "virtualMachineProfile": {
          "storageProfile": {
            "osDisk": {
              "vhdContainers": [
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[0], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[1], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[2], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[3], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[4], '.blob.core.windows.net/vhds')]"
              ],
              "name": "vmssosdisk",
              "caching": "ReadOnly",
              "createOption": "FromImage"
            },
            "imageReference": {
              "publisher": "MicrosoftWindowsServer",
              "offer": "WindowsServer",
              "sku": "2012-R2-Datacenter",
              "version": "latest"
            }
          },
          "osProfile": {
            "computerNamePrefix": "[parameters('vmSSName')]",
            "adminUsername": "[parameters('adminUsername')]",
            "adminPassword": "[parameters('adminPassword')]"
          },
          "networkProfile": {
            "networkInterfaceConfigurations": [
              {
                "name": "networkconfig1",
                "properties": {
                  "primary": "true",
                  "ipConfigurations": [
                    {
                      "name": "ip1",
                      "properties": {
                        "subnet": {
                          "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/virtualNetworks/',variables('virtualNetworkName'),'/subnets/subnet1')]"
                        },
                        "loadBalancerBackendAddressPools": [
                          {
                            "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/loadBalancers/',variables('loadBalancerName'),'/backendAddressPools/bepool1')]"
                          }
                        ],
                        "loadBalancerInboundNatPools": [
                          {
                            "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/loadBalancers/',variables('loadBalancerName'),'/inboundNatPools/natpool1')]"
                          }
                        ]
                      }
                    }
                  ]
                }
              }
            ]
          },
          "extensionProfile": {
            "extensions": [
              {
                "name": "Microsoft.Insights.VMDiagnosticsSettings",
                "properties": {
                  "publisher": "Microsoft.Azure.Diagnostics",
                  "type": "IaaSDiagnostics",
                  "typeHandlerVersion": "1.5",
                  "autoUpgradeMinorVersion": true,
                  "settings": {
                    "xmlCfg": "[base64(concat(variables('wadcfgxstart'),variables('wadmetricsresourceid'),variables('wadcfgxend')))]",
                    "storageAccount": "[variables('diagnosticsStorageAccountName')]"
                  },
                  "protectedSettings": {
                    "storageAccountName": "[variables('diagnosticsStorageAccountName')]",
                    "storageAccountKey": "[listkeys(variables('accountid'), '2015-06-15').key1]",
                    "storageAccountEndPoint": "https://core.windows.net"
                  }
                }
              }
            ]
          }
        }
      }
    },
    ```

11. Merhaba ölçek kümesini nasıl hello ölçek kümesindeki hello makinelerde hello işlemci kullanımına göre ayarlar tanımlar hello autoscaleSettings kaynağı ekleyin.

    ```json
    {
      "type": "Microsoft.Insights/autoscaleSettings",
      "apiVersion": "2015-04-01",
      "name": "[concat(parameters('resourcePrefix'),'as1')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]"
      ],
      "properties": {
        "enabled": true,
        "name": "[concat(parameters('resourcePrefix'),'as1')]",
        "profiles": [
          {
            "name": "Profile1",
            "capacity": {
              "minimum": "1",
              "maximum": "10",
              "default": "1"
            },
            "rules": [
              {
                "metricTrigger": {
                  "metricName": "\\Processor(_Total)\\% Processor Time",
                  "metricNamespace": "",
                  "metricResourceUri": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]",
                  "timeGrain": "PT1M",
                  "statistic": "Average",
                  "timeWindow": "PT5M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 50.0
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              }
            ]
          }
        ],
        "targetResourceUri": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]"
      }
    }
    ```

    Bu öğretici için bu değerleri önemlidir:
    
    * **metricName**  
    Bu değer olan hello biz hello wadperfcounter değişkeninde tanımlanan hello performans sayacı ile aynı. Bu değişkeni kullanarak, hello tanılama uzantısını hello toplar **işlemci(_Toplam)\% işlemci zamanı** sayacı.
    
    * **metricResourceUri**  
    Bu değer hello sanal makine ölçek kümesinin hello kaynak tanımlayıcısı değil.
    
    * **timeGrain**  
    Bu değer toplanan hello ölçümleri hello kesinliği olur. Bu şablonda ayarlamak tooone minute.
    
    * **İstatistiği**  
    Bu değer hello ölçümleri birleşik tooaccommodate hello ölçeklendirme eylemi otomatik şeklini belirler. Merhaba olası değerler şunlardır: ortalama, Min, maks. Bu şablonda hello ortalama toplam CPU kullanımını hello sanal makinelerin toplanır.
    
    * **timeWindow**  
    Bu değer hello örnek veriler toplanır zaman aralığıdır. 5 dakika ile 12 saat arasında olmalıdır.
    
    * **timeAggregation**  
    kendi değeri, toplanan hello veri zaman içinde nasıl birleştirileceğini belirler. Ortalama Hello varsayılan değerdir. Merhaba olası değerler şunlardır: ortalama, Minimum, maksimum, son, toplam, sayısı.
    
    * **işleci**  
    Bu değer kullanılan toocompare hello ölçüm verileri ve hello eşiğin hello işlecidir. Merhaba olası değerler şunlardır: NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual eşittir.
    
    * **Eşik**  
    Bu değer hello ölçek eylemi tetikler hello değerdir. Bu şablonda makineler toohello ölçeği hello kümesindeki makineler arasında hello ortalama CPU kullanımı % 50 üzerinde olduğunda Ayarla eklenir.
    
    * **yönü**  
    Bu değer hello eşik değeri elde edilir, alınır hello eylemi belirler. Merhaba olası artış veya Azalış değerlerdir. Merhaba eşiği % 50'hello tanımlı zaman penceresinde tekrar ise bu şablonda hello hello ölçek kümesindeki sanal makine sayısı artar.
    
    * **türü**  
    Bu değer, gerçekleşeceğini ve tooChangeCount ayarlanmalıdır eylemin hello türüdür.
    
    * **değer**  
    Bu değer hello eklendiğinde veya kaldırıldığında hello ölçek kümesinden sanal makinelerin sayısıdır. Bu değer, 1 veya daha büyük olmalıdır. Merhaba varsayılan değer 1'dir. Hello eşiğine ulaşıldığında bu şablonda artar hello ölçek makinelerinizde hello sayısı 1 ile ayarlayın.
    
    * **cooldown**  
    Merhaba bir sonraki eylem oluşmadan önce bu değer hello zaman toowait hello son ölçeklendirme eylemi itibaren miktarıdır. Bu değer, bir hafta ve bir dakika arasında olmalıdır.

12. Merhaba şablon dosyasını kaydedin.    

## <a name="step-4-upload-hello-template-toostorage"></a>4. adım: Karşıya yükleme hello şablonu toostorage
Merhaba adını ve 1. adımda oluşturduğunuz hello depolama hesabının birincil anahtarını bilmesi sürece hello şablonu karşıya yüklenebilir.

1. Merhaba Microsoft Azure PowerShell penceresinde hello 1. adımda oluşturduğunuz hello depolama hesabının adını belirten bir değişken ayarlayın.
   
    ```powershell
    $storageAccountName = "vmstestsa"
    ```

2. Merhaba depolama hesabının birincil anahtar hello belirten bir değişken ayarlayın.
   
    ```powershell
    $storageAccountKey = "<primary-account-key>"
    ```
   
   Bu anahtar hello depolama hesabı kaynağı hello Azure portal görüntülerken hello anahtar simgesine tıklayarak alabilirsiniz.
3. Merhaba depolama hesabı kullanılan toovalidate işlemleriyle hello depolama hesabı bağlam nesnesi oluşturun.
   
    ```powershell
    $ctx = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
    ```

4. Merhaba şablonu depolamak için hello kapsayıcı oluşturun.

    ```powershell
    $containerName = "templates"
    New-AzureStorageContainer -Name $containerName -Context $ctx  -Permission Blob
    ```

5. Merhaba şablon dosyası toohello yeni kapsayıcı karşıya yükleyin.

    ```powershell   
    $blobName = "VMSSTemplate.json"
    $fileName = "C:\" + $BlobName
    Set-AzureStorageBlobContent -File $fileName -Container $containerName -Blob  $blobName -Context $ctx
    ```

## <a name="step-5-deploy-hello-template"></a>5. adım: hello şablonu dağıtma
Merhaba şablon oluşturduğunuza göre hello kaynakları dağıtmaya başlatabilirsiniz. Bu komut toostart hello işlemini kullanın:

```powershell
New-AzureRmResourceGroupDeployment -Name "vmsstestdp1" -ResourceGroupName "vmsstestrg1" -TemplateUri "https://vmsstestsa.blob.core.windows.net/templates/VMSSTemplate.json"
```

Bastığınızda girin, size atanan hello değişkenleri için istendiğinde tooprovide değerlerdir. Bu değerleri sağlayın:

```powershell
vmName: vmsstestvm1
  vmSSName: vmsstest1
  instanceCount: 5
  adminUserName: vmadmin1
  adminPassword: VMpass1
  resourcePrefix: vmsstest
```

Tüm hello kaynakları toosuccessfully dağıtılması için yaklaşık 15 dakika sürer.

> [!NOTE]
> Merhaba portal'ın özelliği toodeploy hello kaynakları de kullanabilirsiniz. Bu bağlantıyı kullanın: "https://portal.azure.com/#create/Microsoft.Template/uri/<link tooVM Scale Set JSON template>"
> 
> 

## <a name="step-6-monitor-resources"></a>6. adım: İzleme kaynakları
Bu yöntemleri kullanarak sanal makine ölçek kümeleri hakkında bazı bilgiler elde edebilirsiniz:

* Azure portal hello - şu anda sınırlı miktarda bilgiyi hello portal kullanarak elde edebilirsiniz.
* Merhaba [Azure kaynak Gezgini](https://resources.azure.com/) -hello hello ölçek kümesinde geçerli durumunu incelemek için en iyi bu aracıdır. Bu yolu izleyin ve oluşturduğunuz kümesi hello örnek görünümü hello ölçeğin görmeniz gerekir:
  
    Abonelikler > {aboneliğinizi} > resourceGroups > vmsstestrg1 > sağlayıcıları > Microsoft.Compute > virtualMachineScaleSets > vmsstest1 > virtualMachines

* Azure PowerShell - Bu komut tooget bazı bilgileri kullanın:

  ```powershell
  Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"
  ```
  
  Veya
  
  ```powershell
  Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceView
  ```

* Toohello ayrı sanal makine, yalnızca diğer herhangi bir makine olur ve ardından uzaktan hello ölçek kümesi toomonitor tek tek işlemleri hello sanal makinelere erişmek gibi bağlanın.

> [!NOTE]
> Ölçek kümeleri hakkında bilgi almak için tam bir REST API bulunabilir [sanal makine ölçek ayarlar](https://msdn.microsoft.com/library/mt589023.aspx)

## <a name="step-7-remove-hello-resources"></a>7. adım: hello kaynakları Kaldır
Azure'da kullanılan kaynaklar için ücretlendirildiğinizden, her zaman artık gerekli olmayan bir iyi bir uygulama toodelete kaynaklarını aşıyor. Bir kaynak grubundan ayrı ayrı her bir kaynağın toodelete gerek yoktur. Merhaba kaynak grubunu silmek ve tüm kaynakları otomatik olarak silinir.

  ```powershell
  Remove-AzureRmResourceGroup -Name vmsstestrg1
  ```

Kaynak grubunuzun tookeep istiyorsanız, yalnızca kümesi hello ölçek silebilirsiniz.

  ```powershell
  Remove-AzureRmVmss -ResourceGroupName "resource group name" –VMScaleSetName "scale set name"
  ```

## <a name="next-steps"></a>Sonraki adımlar
* Merhaba bilgileri kullanarak oluşturulan yeni hello ölçek kümesini yönetmek [sanal makine ölçek kümesindeki sanal makineleri yönetme](virtual-machine-scale-sets-windows-manage.md).
* [Sanal Makine Ölçek kümeleri ile dikey otomatik ölçeklendirme](virtual-machine-scale-sets-vertical-scale-reprovision.md) bölümünü gözden geçirerek dikey ölçeklendirme hakkında daha fazla bilgi edinin
* Azure özellikleri izleme monitör örnekleri Bul [Azure İzleyici PowerShell hızlı başlangıç örnekleri](../monitoring-and-diagnostics/insights-powershell-samples.md)
* Bildirim özellikler hakkında bilgi edinin [Azure İzleyicisi'nde otomatik ölçeklendirme eylemleri toosend e-posta ve Web kancası uyarı bildirimleri kullanın](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)
* Nasıl çok öğrenin[Azure İzleyicisi'nde kullanım denetim günlüklerini toosend e-posta ve Web kancası uyarı bildirimleri](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)

