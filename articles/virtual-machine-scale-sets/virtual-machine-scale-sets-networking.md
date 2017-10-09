---
title: "Azure sanal makine ölçek kümeleri için aaaNetworking | Microsoft Docs"
description: "Azure sanal makine ölçek kümeleri için yapılandırma ağ hizmeti özellikleri."
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: guybo
ms.openlocfilehash: ef3f0cfe648d2195c051a73987e654f0e15d13bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="networking-for-azure-virtual-machine-scale-sets"></a>Azure sanal makine ölçek kümeleri için ağ hizmeti

Bir Azure sanal makinesi ölçeği hello Portalı aracılığıyla Ayarla dağıttığınızda, belirli ağ özellikleri olarak ayarlanır, örneğin olan bir Azure yük dengeleyici gelen NAT kuralları. Bu makalede nasıl toouse hello bazıları ölçekli yapılandırabilirsiniz ağ özellikleri daha gelişmiş ayarlar açıklanır.

Tüm Azure Resource Manager şablonları kullanarak bu makalede ele alınan hello özelliklerini yapılandırabilirsiniz. Belirli özellikler için Azure CLI ve PowerShell örnekleri de eklenmiştir. CLI 2.10 ve PowerShell 4.2.0 veya üstünü kullanın.

## <a name="accelerated-networking"></a>Hızlandırılmış Ağ
Azure [hızlandırılmış ağ](../virtual-network/virtual-network-create-vm-accelerated-networking.md) tek köklü g/ç Sanallaştırması (SR-IOV) tooa sanal makine etkinleştirerek ağ performansını artırır. toouse hızlandırılmış ölçek kümeleri ile ağ, enableAcceleratedNetworking çok ayarlamak**true** ölçek kümesinin Networkınterfaceconfiguration Ayarları'nda. Örneğin:
```json
"networkProfile": {
    "networkInterfaceConfigurations": [
    {
      "name": "niconfig1",
      "properties": {
        "primary": true,
        "enableAcceleratedNetworking" : true,
        "ipConfigurations": [
          ...
        ]
      }
    }
   ]
}
```

## <a name="create-a-scale-set-that-references-an-existing-azure-load-balancer"></a>Mevcut Azure Load Balancer’a başvuran bir ölçek kümesi oluşturma
Ölçek kümesini hello Azure portal kullanarak oluşturulduğunda, yeni bir yük dengeleyici çoğu yapılandırma seçenekleri için oluşturulur. Var olan bir yük dengeleyici tooreference gereken bir ölçek kümesi oluşturursanız, CLI kullanarak bunu yapabilirsiniz. Aşağıdaki örnek komut dosyası hello bir yük dengeleyici ve başvurduğu bir ölçek kümesi oluşturur:
```bash
az network lb create -g lbtest -n mylb --vnet-name myvnet --subnet mysubnet --public-ip-address-allocation Static --backend-pool-name mybackendpool

az vmss create -g lbtest -n myvmss --image Canonical:UbuntuServer:16.04-LTS:latest --admin-username negat --ssh-key-value /home/myuser/.ssh/id_rsa.pub --upgrade-policy-mode Automatic --instance-count 3 --vnet-name myvnet --subnet mysubnet --lb mylb --backend-pool-name mybackendpool

```

## <a name="configurable-dns-settings"></a>Yapılandırılabilir DNS Ayarları
Varsayılan olarak, Ölçek kümeleri hello belirli DNS ayarlarını oluşturuldukları hello VNET ve alt ağ üzerinde yapın. Ancak, ölçeği doğrudan Ayarla için hello DNS ayarlarını yapılandırın.
~
### <a name="creating-a-scale-set-with-configurable-dns-servers"></a>Yapılandırılabilir DNS sunucularıyla ölçek kümesi oluşturma
bir ölçek kümesi CLI 2.0 kullanan bir özel DNS yapılandırması ile toocreate eklemek hello **--dns sunucuları** bağımsız değişkeni toohello **vmss oluşturma** boşluk bırakarak komutu, sunucu IP adreslerini ayrılmış. Örneğin:
```bash
--dns-servers 10.0.0.6 10.0.0.5
```
bir Azure şablonu tooconfigure özel DNS sunucuları ekleme Networkınterfaceconfiguration bölüm bir dnsSettings özelliği toohello ölçek kümesi. Örneğin:
```json
"dnsSettings":{
    "dnsServers":["10.0.0.6", "10.0.0.5"]
}
```

### <a name="creating-a-scale-set-with-configurable-virtual-machine-domain-names"></a>Yapılandırılabilir sanal makine etki alanı adlarıyla ölçek kümesi oluşturma
bir ölçek kümesi CLI 2.0 kullanarak sanal makineleri için özel bir DNS adı ile toocreate eklemek hello **--vm etki alanı adı** bağımsız değişkeni toohello **vmss oluşturma** hello etki alanı adını temsil eden bir dize tarafından izlenen komutu.

bir Azure şablonu tooset hello etki alanı adını eklemek bir **dnsSettings** özellik toohello ölçek kümesi **Networkınterfaceconfiguration** bölümü. Örneğin:

```json
"networkProfile": {
  "networkInterfaceConfigurations": [
    {
    "name": "nic1",
    "properties": {
      "primary": "true",
      "ipConfigurations": [
      {
        "name": "ip1",
        "properties": {
          "subnet": {
            "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
          },
          "publicIPAddressconfiguration": {
            "name": "publicip",
            "properties": {
            "idleTimeoutInMinutes": 10,
              "dnsSettings": {
                "domainNameLabel": "[parameters('vmssDnsName')]"
              }
            }
          }
        }
      }
    ]
    }
}
```

bir sanal makinenin dns adı için Hello çıkış form aşağıdaki hello olacaktır: 
```
<vm><vmindex>.<specifiedVmssDomainNameLabel>
```

## <a name="public-ipv4-per-virtual-machine"></a>Sanal makine başına genel IPv4
Genel olarak, Azure ölçek kümesi sanal makinelerinin kendi genel IP adresleri olması gerekmez. Çoğu senaryoda, olmasından daha ekonomik ve güvenli tooassociate bir ortak IP adresi tooa yük dengeleyici veya tooan tek tek sanal, ardından gelen bağlantıları tooscale kümesi sanal makineleri (örneğin, aracılığıyla gerektiğinde yönlendiren makine (diğer adıyla bir jumpbox), gelen NAT kuralları).

Ancak, bazı senaryolar ölçek kümesi sanal makineleri toohave kendi ortak IP gerektiren adresleri. Bir örnek oyun, burada bir konsol toomake doğrudan bağlantı tooa bulut sanal hangi oyun fizik işlem yaptığını makine gerekiyor. Sanal makineler toomake dış bağlantıları tooone gereken yeri başka bir örnektir başka bölgelere dağıtılan bir veritabanı içinde.

### <a name="creating-a-scale-set-with-public-ip-per-virtual-machine"></a>Sanal makine başına bir genel IP ile ölçek kümesi oluşturma
toocreate ortak IP adresi tooeach sahip bir sanal makine CLI 2.0 atar ölçek kümesi ekleme hello **--vm başına ortak IP** parametresi toohello **vmss oluşturma** komutu. 

bir Azure şablonu kullanarak bir ölçek toocreate hello Microsoft.Compute/virtualMachineScaleSets kaynak hello API sürümü en az olduğundan emin olun **2017-03-30**ve ekleme bir **publicIpAddressConfiguration**JSON özellik toohello ölçek kümesi Ipconfigurations bölümü. Örneğin:

```json
"publicIpAddressConfiguration": {
    "name": "pub1",
    "properties": {
      "idleTimeoutInMinutes": 15
    }
}
```
Örnek şablon: [201-vmss-public-ip-linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-public-ip-linux)

### <a name="querying-hello-public-ip-addresses-of-hello-virtual-machines-in-a-scale-set"></a>Merhaba sanal makinelerin bir ölçek adreslerini kümesini Hello genel IP sorgulama
CLI 2.0 kullanarak kümesi sanal makineleri atanmış tooscale toolist hello ortak IP adresleri, hello kullan **az vmss listesi-örnek-genel-IP'leri** komutu.

toolist ölçek kümesi PowerShell kullanarak genel IP adresleri, hello kullan _Get-AzureRmPublicIpAddress_ komutu. Örneğin:
```PowerShell
PS C:\> Get-AzureRmPublicIpAddress -ResourceGroupName myrg -VirtualMachineScaleSetName myvmss
```

Sorgu hello genel IP adresleri ayrıca hello ortak IP adresi yapılandırması hello kaynak kimliği doğrudan başvurarak erişebilirsiniz. Örneğin:
```PowerShell
PS C:\> Get-AzureRmPublicIpAddress -ResourceGroupName myrg -Name myvmsspip
```

atanmış tooscale tooquery hello ortak IP adresleri hello kullanarak kümesi sanal makineleri [Azure kaynak Gezgini](https://resources.azure.com), ya da Azure REST API sürümü ile Merhaba **2017-03-30** ya da daha yüksek.

tooview genel IP adresleri hello kaynak Gezgini, kullanılarak ayarlanan bir ölçek için konum hello **publicıpaddresses** bölümü, Ölçek kümesi altında. Örneğin: https://resources.azure.com/subscriptions/_sub_kimliğiniz_/resourceGroups/_rg_değeriniz_/providers/Microsoft.Compute/virtualMachineScaleSets/_vmss_değeriniz_/publicipaddresses

```
GET https://management.azure.com/subscriptions/{your sub ID}/resourceGroups/{RG name}/providers/Microsoft.Compute/virtualMachineScaleSets/{scale set name}/publicipaddresses?api-version=2017-03-30
```

Örnek çıktı:
```json
{
  "value": [
    {
      "name": "pub1",
      "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/pipvmss/virtualMachines/0/networkInterfaces/pipvmssnic/ipConfigurations/yourvmssipconfig/publicIPAddresses/pub1",
      "etag": "W/\"a64060d5-4dea-4379-a11d-b23cd49a3c8d\"",
      "properties": {
        "provisioningState": "Succeeded",
        "resourceGuid": "ee8cb20f-af8e-4cd6-892f-441ae2bf701f",
        "ipAddress": "13.84.190.11",
        "publicIPAddressVersion": "IPv4",
        "publicIPAllocationMethod": "Dynamic",
        "idleTimeoutInMinutes": 15,
        "ipConfiguration": {
          "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmss/virtualMachines/0/networkInterfaces/yourvmssnic/ipConfigurations/yourvmssipconfig"
        }
      }
    },
    {
      "name": "pub1",
      "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmss/virtualMachines/3/networkInterfaces/yourvmssnic/ipConfigurations/yourvmssipconfig/publicIPAddresses/pub1",
      "etag": "W/\"5f6ff30c-a24c-4818-883c-61ebd5f9eee8\"",
      "properties": {
        "provisioningState": "Succeeded",
        "resourceGuid": "036ce266-403f-41bd-8578-d446d7397c2f",
        "ipAddress": "13.84.159.176",
        "publicIPAddressVersion": "IPv4",
        "publicIPAllocationMethod": "Dynamic",
        "idleTimeoutInMinutes": 15,
        "ipConfiguration": {
          "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmss/virtualMachines/3/networkInterfaces/yourvmssnic/ipConfigurations/yourvmssipconfig"
        }
      }
    }
```

## <a name="multiple-ip-addresses-per-nic"></a>NIC başına birden çok IP adresi
Her NIC VM ölçek kümesindeki kendisiyle ilişkili bir veya daha fazla IP yapılandırmaları olabilir tooa bağlı. Her yapılandırma bir özel IP adresine atanır. Her yapılandırmayla ilişkilendirilmiş bir genel IP adresi kaynağı da olabilir. kaç tane IP adresleri toounderstand tooa NIC, atanacağını ve bir Azure aboneliği kullanabileceğiniz kaç genel IP adresleri başvuruda çok[Azure sınırları](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits).

## <a name="multiple-nics-per-virtual-machine"></a>Sanal makine başına birden çok NIC
Makine boyutuna bağlı olarak sanal makine başına too8 NIC'ler yukarı sahip olabilir. Merhaba en fazla sayıda NIC makine başına hello kullanılabilir [VM boyutu makale](../virtual-machines/windows/sizes.md). Merhaba aşağıdaki ağ profili birden çok NIC girişleri ve sanal makine başına birden çok ortak IP gösteren bir ölçek kümesi örneğidir:
```json
"networkProfile": {
    "networkInterfaceConfigurations": [
        {
        "name": "nic1",
        "properties": {
            "primary": "true",
            "ipConfigurations": [
            {
                "name": "ip1",
                "properties": {
                "subnet": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                },
                "publicipaddressconfiguration": {
                    "name": "pub1",
                    "properties": {
                    "idleTimeoutInMinutes": 15
                    }
                },
                "loadBalancerInboundNatPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                    }
                ],
                "loadBalancerBackendAddressPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                    }
                ]
                }
            }
            ]
        }
        },
        {
        "name": "nic2",
        "properties": {
            "primary": "false",
            "ipConfigurations": [
            {
                "name": "ip1",
                "properties": {
                "subnet": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                },
                "publicipaddressconfiguration": {
                    "name": "pub1",
                    "properties": {
                    "idleTimeoutInMinutes": 15
                    }
                },
                "loadBalancerInboundNatPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                    }
                ],
                "loadBalancerBackendAddressPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                    }
                ]
                }
            }
            ]
        }
        }
    ]
}
```

## <a name="nsg-per-scale-set"></a>Ölçek kümesi başına NSG
Tooa ölçek kümesi, bir başvuru toohello ağ arabirimi yapılandırması bölümü hello ölçeğin ekleyerek sanal makine özelliklerini ayarla doğrudan ağ güvenlik grupları uygulanabilir.

Örneğin: 
```
"networkProfile": {
    "networkInterfaceConfigurations": [
        {
            "name": "nic1",
            "properties": {
                "primary": "true",
                "ipConfigurations": [
                    {
                        "name": "ip1",
                        "properties": {
                            "subnet": {
                                "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                            }
                "loadBalancerInboundNatPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                                }
                            ],
                            "loadBalancerBackendAddressPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                                }
                            ]
                        }
                    }
                ],
                "networkSecurityGroup": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/networkSecurityGroups/', variables('nsgName'))]"
                }
            }
        }
    ]
}
```

## <a name="next-steps"></a>Sonraki adımlar
Azure sanal ağlar hakkında daha fazla bilgi için çok başvurun[bu belgeleri](../virtual-network/virtual-networks-overview.md).
