---
title: "Azure Service Fabric için aaaNetworking desenleri | Microsoft Docs"
description: "Ortak ağ desenler için Service Fabric açıklar ve nasıl toocreate Azure ağ özelliklerini kullanarak bir küme."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/16/2017
ms.author: ryanwi
ms.openlocfilehash: 5973e3f9917076c6a36e71443ec256e0f414ff87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-networking-patterns"></a>Service Fabric ağ desenleri
Azure Service Fabric kümesi Azure diğer ağ özelliklerini ile tümleştirebilirsiniz. Bu makalede, nasıl toocreate özellikler aşağıdaki bu kullanım hello kümeleri gösteriyoruz:

- [Var olan sanal ağ veya alt ağ](#existingvnet)
- [Statik genel IP adresi](#staticpublicip)
- [Yalnızca dahili yük dengeleyici](#internallb)
- [İç ve dış yük dengeleyici](#internalexternallb)

Service Fabric standart sanal makine ölçek kümesindeki çalışır. Bir sanal makine ölçek kümesindeki kullanabileceğiniz herhangi bir işlevsellik, Service Fabric kümesi ile kullanabilirsiniz. sanal makine ölçek kümeleri ve Service Fabric hello Azure Resource Manager şablonları ağ bölümlerini Hello aynıdır. Sanal ağ varolan tooan dağıttıktan sonra diğer kolay tooincorporate olan ağ Azure ExpressRoute, Azure VPN ağ geçidi, bir ağ güvenlik grubu ve sanal ağ eşlemesi gibi özellikleri.

Service Fabric diğer ağ özelliklerini tek bir yönüne içinde benzersizdir. Merhaba [Azure portal](https://portal.azure.com) dahili olarak kullandığı Service Fabric kaynak sağlayıcısı toocall tooa küme tooget düğümleri ve uygulamalar hakkında bilgi hello. Hello Service Fabric kaynak sağlayıcı genel olarak erişilebilir gelen erişim toohello HTTP ağ geçidi bağlantı noktası (varsayılan olarak 19080, bağlantı noktası) hello yönetim uç nokta gerektiriyor. [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) kullanır, küme yönetim uç nokta toomanage hello. Merhaba Service Fabric kaynak sağlayıcısı ayrıca kümenizi, toodisplay hello Azure portal'ın bu bağlantı noktası tooquery bilgilerini kullanır. 

Bağlantı noktası 19080 hello Service Fabric kaynak Sağlayıcısı'ndan erişilebilir durumda değilse, bir ileti ister *düğümleri bulunamadı* hello Portalı'nda görüntülenir ve düğüm ve uygulama listenizi boş görünür. Hello Azure portal kümenizdeki toosee istiyorsanız, bir ortak IP adresi, yük dengeleyici kullanıma gerekir ve ağ güvenlik grubu gelen bağlantı noktası 19080 trafiğe izin vermelidir. Kurulumunuzu bu gereksinimlerini karşılamıyorsa hello Azure portal kümenizi hello durumunu göstermez.

## <a name="templates"></a>Şablonlar

Tüm Service Fabric şablonları bulunan [bir yükleme dosyası](https://msdnshared.blob.core.windows.net/media/2016/10/SF_Networking_Templates.zip). Merhaba şablon olarak kullanabilirsiniz toodeploy olmalıdır-hello aşağıdaki PowerShell komutlarını kullanmaktır. Dağıtıyorsanız hello olan Azure Virtual Network şablonu veya hello statik genel IP şablonu, ilk hello okuma [ilk kurulum](#initialsetup) bu makalenin.

<a id="initialsetup"></a>
## <a name="initial-setup"></a>İlk kurulumu

### <a name="existing-virtual-network"></a>Var olan sanal ağ

Aşağıdaki örneğine hello biz ExistingRG-vnet, hello adlı varolan bir sanal ağı Başlat **ExistingRG** kaynak grubu. Merhaba alt ağ varsayılan olarak adlandırılır. Hello Azure portal toocreate standart bir sanal makine (VM) kullandığınızda, bu varsayılan kaynakları oluşturulur. Merhaba VM oluşturmadan hello sanal ağ ve alt ağ oluşturabilirsiniz, ancak küme tooan varolan sanal ağ ekleme hello ana tooprovide ağ bağlantısı tooother VM'ler hedeftir. Oluşturma hello VM varolan bir sanal ağı genellikle nasıl kullanıldığını, iyi bir örnek verir. Service Fabric kümesi yalnızca bir iç yük dengeleyici, genel bir IP adresi olmadan kullanıyorsa kullanabileceğiniz VM ve güvenli olarak ortak IP hello *kutusunu atlama*.

### <a name="static-public-ip-address"></a>Statik genel IP adresi

Bir statik genel IP adresi, genellikle hello VM veya atandığı VM'ler gelen ayrı olarak yönetilen ayrılmış bir kaynak değil. Bu ayrılmış bir ağ kaynak grubunda (karşılıklı tooin hello Service Fabric küme kaynak grubu kendisi) sağlanır. Merhaba staticIP1 adlı bir statik genel IP adresi oluşturma hello Azure portal veya PowerShell kullanarak aynı ExistingRG kaynak grubu:

```powershell
PS C:\Users\user> New-AzureRmPublicIpAddress -Name staticIP1 -ResourceGroupName ExistingRG -Location westus -AllocationMethod Static -DomainNameLabel sfnetworking

Name                     : staticIP1
ResourceGroupName        : ExistingRG
Location                 : westus
Id                       : /subscriptions/1237f4d2-3dce-1236-ad95-123f764e7123/resourceGroups/ExistingRG/providers/Microsoft.Network/publicIPAddresses/staticIP1
Etag                     : W/"fc8b0c77-1f84-455d-9930-0404ebba1b64"
ResourceGuid             : 77c26c06-c0ae-496c-9231-b1a114e08824
ProvisioningState        : Succeeded
Tags                     :
PublicIpAllocationMethod : Static
IpAddress                : 40.83.182.110
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : null
DnsSettings              : {
                             "DomainNameLabel": "sfnetworking",
                             "Fqdn": "sfnetworking.westus.cloudapp.azure.com"
                           }
```

### <a name="service-fabric-template"></a>Service Fabric şablonu

Bu makalede Hello örneklerde hello Service Fabric template.json kullanırız. Küme oluşturmadan önce hello standart portal Sihirbazı toodownload hello hello portal şablondan kullanabilirsiniz. Merhaba şablonlarından birini de hello kullanabilirsiniz [Şablon Galerisi](https://azure.microsoft.com/en-us/documentation/templates/?term=service+fabric), hello gibi [beş düğümlü Service Fabric kümesi](https://azure.microsoft.com/en-us/documentation/templates/service-fabric-unsecure-cluster-5-node-1-nodetype/).

<a id="existingvnet"></a>
## <a name="existing-virtual-network-or-subnet"></a>Var olan sanal ağ veya alt ağ

1. Hello alt parametre toohello hello mevcut alt adını değiştirin ve sonra iki yeni parametreleri tooreference hello var olan bir sanal ağ ekleyin:

    ```
        "subnet0Name": {
                "type": "string",
                "defaultValue": "default"
            },
            "existingVNetRGName": {
                "type": "string",
                "defaultValue": "ExistingRG"
            },

            "existingVNetName": {
                "type": "string",
                "defaultValue": "ExistingRG-vnet"
            },
            /*
            "subnet0Name": {
                "type": "string",
                "defaultValue": "Subnet-0"
            },
            "subnet0Prefix": {
                "type": "string",
                "defaultValue": "10.0.0.0/24"
            },*/
    ```


2. Değişiklik hello `vnetID` değişken toopoint toohello var olan sanal ağ:

    ```
            /*old "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',parameters('virtualNetworkName'))]",*/
            "vnetID": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', parameters('existingVNetRGName'), '/providers/Microsoft.Network/virtualNetworks/', parameters('existingVNetName'))]",
    ```

3. Kaldırma `Microsoft.Network/virtualNetworks` kaynaklarınızdan, bu nedenle Azure oluşturmaz yeni bir sanal ağ:

    ```
    /*{
    "apiVersion": "[variables('vNetApiVersion')]",
    "type": "Microsoft.Network/virtualNetworks",
    "name": "[parameters('virtualNetworkName')]",
    "location": "[parameters('computeLocation')]",
    "properities": {
        "addressSpace": {
            "addressPrefixes": [
                "[parameters('addressPrefix')]"
            ]
        },
        "subnets": [
            {
                "name": "[parameters('subnet0Name')]",
                "properties": {
                    "addressPrefix": "[parameters('subnet0Prefix')]"
                }
            }
        ]
    },
    "tags": {
        "resourceType": "Service Fabric",
        "clusterName": "[parameters('clusterName')]"
    }
    },*/
    ```

4. Açıklama hello sanal ağdan hello çıkışı `dependsOn` özniteliği `Microsoft.Compute/virtualMachineScaleSets`, yeni bir sanal ağ oluşturma ile ilgili bağımlı yok:

    ```
    "apiVersion": "[variables('vmssApiVersion')]",
    "type": "Microsoft.Computer/virtualMachineScaleSets",
    "name": "[parameters('vmNodeType0Name')]",
    "location": "[parameters('computeLocation')]",
    "dependsOn": [
        /*"[concat('Microsoft.Network/virtualNetworks/', parameters('virtualNetworkName'))]",
        */
        "[Concat('Microsoft.Storage/storageAccounts/', variables('uniqueStringArray0')[0])]",

    ```

5. Merhaba şablonunu dağıtın:

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkingexistingvnet -Location westus
    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkingexistingvnet -TemplateFile C:\SFSamples\Final\template\_existingvnet.json
    ```

    Dağıtımdan sonra sanal ağınızı içermelidir hello yeni ölçek kümesi VM. Merhaba sanal makine ölçek kümesi düğüm türü hello varolan sanal ağ ve alt göstermelidir. Sanal makineleri tooping hello yeni ölçek kümesi ve Uzak Masaüstü Protokolü (RDP) tooaccess hello sanal ağda zaten olan VM hello de kullanabilirsiniz:

    ```
    C:>\Users\users>ping 10.0.0.5 -n 1
    C:>\Users\users>ping NOde1000000 -n 1
    ```

Başka bir örnek için bkz: [belirli tooService doku olmayan bir](https://github.com/gbowerman/azure-myriad/tree/master/existing-vnet).


<a id="staticpublicip"></a>
## <a name="static-public-ip-address"></a>Statik genel IP adresi

1. Statik IP kaynak grubu, adı ve tam etki alanı adı (FQDN) mevcut hello hello adını parametrelerini ekleyin:

    ```
    "existingStaticIPResourceGroup": {
                "type": "string"
            },
            "existingStaticIPName": {
                "type": "string"
            },
            "existingStaticIPDnsFQDN": {
                "type": "string"
    }
    ```

2. Merhaba kaldırmak `dnsName` parametresi. (Merhaba statik IP adresi zaten varsa.)

    ```
    /*
    "dnsName": {
        "type": "string"
    },
    */
    ```

3. Değişken tooreference hello varolan statik bir IP adresi ekleyin:

    ```
    "existingStaticIP": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', parameters('existingStaticIPResourceGroup'), '/providers/Microsoft.Network/publicIPAddresses/', parameters('existingStaticIPName'))]",
    ```

4. Kaldırma `Microsoft.Network/publicIPAddresses` kaynaklarınızdan, bu nedenle Azure oluşturmaz yeni bir IP adresi:

    ```
    /*
    {
        "apiVersion": "[variables('publicIPApiVersion')]",
        "type": "Microsoft.Network/publicIPAddresses",
        "name": "[concat(parameters('lbIPName'),)'-', '0')]",
        "location": "[parameters('computeLocation')]",
        "properties": {
            "dnsSettings": {
                "domainNameLabel": "[parameters('dnsName')]"
            },
            "publicIPAllocationMethod": "Dynamic"        
        },
        "tags": {
            "resourceType": "Service Fabric",
            "clusterName": "[parameters('clusterName')]"
        }
    }, */
    ```

5. Açıklama hello hello IP adresinden çıkışı `dependsOn` özniteliği `Microsoft.Network/loadBalancers`, yeni bir IP adresi oluşturma bağımlı yok:

    ```
    "apiVersion": "[variables('lbIPApiVersion')]",
    "type": "Microsoft.Network/loadBalancers",
    "name": "[concat('LB', '-', parameters('clusterName'), '-', parameters('vmNodeType0Name'))]",
    "location": "[parameters('computeLocation')]",
    /*
    "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', concat(parameters('lbIPName'), '-', '0'))]"
    ], */
    "properties": {
    ```

6. Merhaba, `Microsoft.Network/loadBalancers` kaynak, değişiklik hello `publicIPAddress` öğesinin `frontendIPConfigurations` tooreference hello yeni oluşturulan bir yerine var olan statik IP adresi:

    ```
                "frontendIPConfigurations": [
                        {
                            "name": "LoadBalancerIPConfig",
                            "properties": {
                                "publicIPAddress": {
                                    /*"id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(parameters('lbIPName'),'-','0'))]"*/
                                    "id": "[variables('existingStaticIP')]"
                                }
                            }
                        }
                    ],
    ```

7. Merhaba, `Microsoft.ServiceFabric/clusters` kaynak, değişiklik `managementEndpoint` toohello hello statik IP adresi DNS FQDN'si. Güvenli bir küme kullanıyorsanız, değiştirdiğinizden emin olun *http://* çok*https://*. (Bu adım yalnızca tooService yapı kümeleri geçerli olduğunu unutmayın. Bir sanal makine ölçek kümesini kullanıyorsanız, bu adımı atlayın.)

    ```
                    "fabricSettings": [],
                    /*"managementEndpoint": "[concat('http://',reference(concat(parameters('lbIPName'),'-','0')).dnsSettings.fqdn,':',parameters('nt0fabricHttpGatewayPort'))]",*/
                    "managementEndpoint": "[concat('http://',parameters('existingStaticIPDnsFQDN'),':',parameters('nt0fabricHttpGatewayPort'))]",
    ```

8. Merhaba şablonunu dağıtın:

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkingstaticip -Location westus

    $staticip = Get-AzureRmPublicIpAddress -Name staticIP1 -ResourceGroupName ExistingRG

    $staticip

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkingstaticip -TemplateFile C:\SFSamples\Final\template\_staticip.json -existingStaticIPResourceGroup $staticip.ResourceGroupName -existingStaticIPName $staticip.Name -existingStaticIPDnsFQDN $staticip.DnsSettings.Fqdn
    ```

Dağıtımdan sonra Yük Dengeleyici ilişkili toohello ortak statik IP adresi hello olduğunu görebilirsiniz diğer kaynak grubu. Service Fabric istemci bağlantı uç noktasının hello ve [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) uç noktası toohello hello statik IP adresi DNS FQDN'si.

<a id="internallb"></a>
## <a name="internal-only-load-balancer"></a>Yalnızca dahili yük dengeleyici

Bu senaryo hello dış yük dengeleyici hello varsayılan Service Fabric şablonunda yalnızca iç yük dengeleyici ile değiştirir. Hello Azure portal ve hello Service Fabric kaynak sağlayıcısı için uygulamaları için önceki bölümde hello bakın.

1. Merhaba kaldırmak `dnsName` parametresi. (Bu gerekli değildir.)

    ```
    /*
    "dnsName": {
        "type": "string"
    },
    */
    ```

2. İsteğe bağlı olarak, statik ayırma yöntemi kullanırsanız, bir statik IP adresi parametre ekleyebilirsiniz. Dinamik ayırma yöntemini kullanırsanız, bu adımı toodo gerekmez.

    ```
            "internalLBAddress": {
                "type": "string",
                "defaultValue": "10.0.0.250"
            }
    ```

3. Kaldırma `Microsoft.Network/publicIPAddresses` kaynaklarınızdan, bu nedenle Azure oluşturmaz yeni bir IP adresi:

    ```
    /*
    {
        "apiVersion": "[variables('publicIPApiVersion')]",
        "type": "Microsoft.Network/publicIPAddresses",
        "name": "[concat(parameters('lbIPName'),)'-', '0')]",
        "location": "[parameters('computeLocation')]",
        "properties": {
            "dnsSettings": {
                "domainNameLabel": "[parameters('dnsName')]"
            },
            "publicIPAllocationMethod": "Dynamic"        
        },
        "tags": {
            "resourceType": "Service Fabric",
            "clusterName": "[parameters('clusterName')]"
        }
    }, */
    ```

4. Başlangıç IP adresini kaldırın `dependsOn` özniteliği `Microsoft.Network/loadBalancers`, yeni bir IP adresi oluşturma bağımlı yok. Merhaba sanal ağ ekleme `dependsOn` hello yük dengeleyici şimdi hello alt hello sanal ağdan bağımlı olduğundan dolayı özniteliği:

    ```
                "apiVersion": "[variables('lbApiVersion')]",
                "type": "Microsoft.Network/loadBalancers",
                "name": "[concat('LB','-', parameters('clusterName'),'-',parameters('vmNodeType0Name'))]",
                "location": "[parameters('computeLocation')]",
                "dependsOn": [
                    /*"[concat('Microsoft.Network/publicIPAddresses/',concat(parameters('lbIPName'),'-','0'))]"*/
                    "[concat('Microsoft.Network/virtualNetworks/',parameters('virtualNetworkName'))]"
                ],
    ```

5. Değiştirme hello yük dengeleyicisinin `frontendIPConfigurations` kullanımından ayarını bir `publicIPAddress`, toousing bir alt ağ ve `privateIPAddress`. `privateIPAddress`önceden tanımlanmış statik iç IP adresi kullanır. toouse dinamik bir IP adresi kaldırmak hello `privateIPAddress` öğesini ve ardından değişiklik `privateIPAllocationMethod` çok**dinamik**.

    ```
                "frontendIPConfigurations": [
                        {
                            "name": "LoadBalancerIPConfig",
                            "properties": {
                                /*
                                "publicIPAddress": {
                                    "id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(parameters('lbIPName'),'-','0'))]"
                                } */
                                "subnet" :{
                                    "id": "[variables('subnet0Ref')]"
                                },
                                "privateIPAddress": "[parameters('internalLBAddress')]",
                                "privateIPAllocationMethod": "Static"
                            }
                        }
                    ],
    ```

6. Merhaba, `Microsoft.ServiceFabric/clusters` kaynak, değişiklik `managementEndpoint` toopoint toohello iç yük dengeleyici adresi. Güvenli bir küme kullanıyorsanız, değiştirdiğiniz emin olun *http://* çok*https://*. (Bu adım yalnızca tooService yapı kümeleri geçerli olduğunu unutmayın. Bir sanal makine ölçek kümesini kullanıyorsanız, bu adımı atlayın.)

    ```
                    "fabricSettings": [],
                    /*"managementEndpoint": "[concat('http://',reference(concat(parameters('lbIPName'),'-','0')).dnsSettings.fqdn,':',parameters('nt0fabricHttpGatewayPort'))]",*/
                    "managementEndpoint": "[concat('http://',reference(variables('lbID0')).frontEndIPConfigurations[0].properties.privateIPAddress,':',parameters('nt0fabricHttpGatewayPort'))]",
    ```

7. Merhaba şablonunu dağıtın:

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkinginternallb -Location westus

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkinginternallb -TemplateFile C:\SFSamples\Final\template\_internalonlyLB.json
    ```

Dağıtımdan sonra Yük Dengeleyici hello özel statik 10.0.0.250 IP adresini kullanır. Bu aynı sanal ağdaki başka bir makine varsa, iç toohello gidebilirsiniz [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) uç noktası. Merhaba yük dengeleyicinin arkasındaki hello düğümlerinin tooone bağladığı unutmayın.

<a id="internalexternallb"></a>
## <a name="internal-and-external-load-balancer"></a>İç ve dış yük dengeleyici

Bu senaryoda, hello var olan tek bir düğüm türü dış yük dengeleyici ile başlatın ve hello için bir iç yük dengeleyici eklemek aynı düğüm türü. Yalnızca tooa tek yük dengeleyici arka uç bağlantı noktası bağlı tooa arka uç adres havuzu atanabilir. Hangi yük dengeleyici, uygulama bağlantı noktaları sahip ve hangi yük dengeleyici Yönetimi noktalarınızı (bağlantı noktaları 19000 ve 19080) sahip seçin. Merhaba iç yük dengeleyicide hello yönetim uç noktalarının yerleştirirseniz göz hello Service Fabric kaynak sağlayıcısı kısıtlamaları hello makalenin önceki bölümlerinde açıklanan tutun. Kullanırız hello örnekte hello yönetim uç noktalarının hello dış yük dengeleyici üzerinde kalır. Ayrıca bir bağlantı noktası 80 uygulama bağlantı noktası eklemek ve hello iç yük dengeleyicide yerleştirin.

İki düğüm türü kümedeki bir düğüm üzerinde hello dış yük dengeleyici türüdür. Merhaba diğer düğümü hello iç yük dengeleyicide türüdür. toouse (sahip iki yük dengeleyici gelen) hello portal tarafından oluşturulan iki düğüm türü şablonu, bir iki düğüm türü kümede hello ikinci yük dengeleyici tooan iç yük dengeleyici geçin. Daha fazla bilgi için bkz: Merhaba [yalnızca dahili yük dengeleyici](#internallb) bölümü.

1. Merhaba statik iç yük dengeleyici IP adresi parametresini ekleyin. (Notları ilgili toousing için dinamik bir IP adresi, bu makalenin önceki bölümlerinde bkz.)

    ```
            "internalLBAddress": {
                "type": "string",
                "defaultValue": "10.0.0.250"
            }
    ```

2. Bir uygulama bağlantı noktası 80 parametresini ekleyin.

3. Merhaba varolan tooadd iç sürümlerini kopyalama değişkenleri, ağ ve kopyalayıp yapıştırın ve Ekle "-Int" toohello adı:

    ```
    /* Add internal load balancer networking variables */
            "lbID0-Int": "[resourceId('Microsoft.Network/loadBalancers', concat('LB','-', parameters('clusterName'),'-',parameters('vmNodeType0Name'), '-Internal'))]",
            "lbIPConfig0-Int": "[concat(variables('lbID0-Int'),'/frontendIPConfigurations/LoadBalancerIPConfig')]",
            "lbPoolID0-Int": "[concat(variables('lbID0-Int'),'/backendAddressPools/LoadBalancerBEAddressPool')]",
            "lbProbeID0-Int": "[concat(variables('lbID0-Int'),'/probes/FabricGatewayProbe')]",
            "lbHttpProbeID0-Int": "[concat(variables('lbID0-Int'),'/probes/FabricHttpGatewayProbe')]",
            "lbNatPoolID0-Int": "[concat(variables('lbID0-Int'),'/inboundNatPools/LoadBalancerBEAddressNatPool')]",
            /* Internal load balancer networking variables end */
    ```

4. Uygulama bağlantı noktası 80 kullanan hello portal tarafından oluşturulan şablon ile başlatırsanız, hello varsayılan portal şablonu AppPort1 ekler (bağlantı noktası 80) hello dış yük dengeleyici üzerinde. Bu durumda, AppPort1 hello dış yük dengeleyiciden kaldırın `loadBalancingRules` ve araştırmalar toohello iç yük dengeleyici eklemek için:

    ```
    "loadBalancingRules": [
        {
            "name": "LBHttpRule",
            "properties":{
                "backendAddressPool": {
                    "id": "[variables('lbPoolID0')]"
                },
                "backendPort": "[parameters('nt0fabricHttpGatewayPort')]",
                "enableFloatingIP": "false",
                "frontendIPConfiguration": {
                    "id": "[variables('lbIPConfig0')]"            
                },
                "frontendPort": "[parameters('nt0fabricHttpGatewayPort')]",
                "idleTimeoutInMinutes": "5",
                "probe": {
                    "id": "[variables('lbHttpProbeID0')]"
                },
                "protocol": "tcp"
            }
        } /* Remove AppPort1 from hello external load balancer.
        {
            "name": "AppPortLBRule1",
            "properties": {
                "backendAddressPool": {
                    "id": "[variables('lbPoolID0')]"
                },
                "backendPort": "[parameters('loadBalancedAppPort1')]",
                "enableFloatingIP": "false",
                "frontendIPConfiguration": {
                    "id": "[variables('lbIPConfig0')]"            
                },
                "frontendPort": "[parameters('loadBalancedAppPort1')]",
                "idleTimeoutInMinutes": "5",
                "probe": {
                    "id": "[concate(variables('lbID0'), '/probes/AppPortProbe1')]"
                },
                "protocol": "tcp"
            }
        }*/

    ],
    "probes": [
        {
            "name": "FabricGatewayProbe",
            "properties": {
                "intervalInSeconds": 5,
                "numberOfProbes": 2,
                "port": "[parameters('nt0fabricTcpGatewayPort')]",
                "protocol": "tcp"
            }
        },
        {
            "name": "FabricHttpGatewayProbe",
            "properties": {
                "intervalInSeconds": 5,
                "numberOfProbes": 2,
                "port": "[parameters('nt0fabricHttpGatewayPort')]",
                "protocol": "tcp"
            }
        } /* Remove AppPort1 from hello external load balancer.
        {
            "name": "AppPortProbe1",
            "properties": {
                "intervalInSeconds": 5,
                "numberOfProbes": 2,
                "port": "[parameters('loadBalancedAppPort1')]",
                "protocol": "tcp"
            }
        } */

    ],
    "inboundNatPools": [
    ```

5. İkinci bir ekleme `Microsoft.Network/loadBalancers` kaynak. Hello oluşturulan benzer toohello iç yük dengeleyici görünüyor [yalnızca dahili yük dengeleyici](#internallb) bölüm, ancak kullanan hello "-Int" dengeleyici değişkenleri ve uygular yalnızca hello uygulama bağlantı noktası 80'i yükler. Bu da kaldırır `inboundNatPools`, hello genel yük dengeleyiciye üzerindeki tookeep RDP uç noktaları. Merhaba iç yük dengeleyici üzerinde RDP istiyorsanız taşıyın `inboundNatPools` hello dış yük dengeleyici toothis iç yük dengeleyici:

    ```
            /* Add a second load balancer, configured with a static privateIPAddress and hello "-Int" load balancer variables. */
            {
                "apiVersion": "[variables('lbApiVersion')]",
                "type": "Microsoft.Network/loadBalancers",
                /* Add "-Internal" toohello name. */
                "name": "[concat('LB','-', parameters('clusterName'),'-',parameters('vmNodeType0Name'), '-Internal')]",
                "location": "[parameters('computeLocation')]",
                "dependsOn": [
                    /* Remove public IP dependsOn, add vnet dependsOn
                    "[concat('Microsoft.Network/publicIPAddresses/',concat(parameters('lbIPName'),'-','0'))]"
                    */
                    "[concat('Microsoft.Network/virtualNetworks/',parameters('virtualNetworkName'))]"
                ],
                "properties": {
                    "frontendIPConfigurations": [
                        {
                            "name": "LoadBalancerIPConfig",
                            "properties": {
                                /* Switch from Public tooPrivate IP address
                                */
                                "publicIPAddress": {
                                    "id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(parameters('lbIPName'),'-','0'))]"
                                }
                                */
                                "subnet" :{
                                    "id": "[variables('subnet0Ref')]"
                                },
                                "privateIPAddress": "[parameters('internalLBAddress')]",
                                "privateIPAllocationMethod": "Static"
                            }
                        }
                    ],
                    "backendAddressPools": [
                        {
                            "name": "LoadBalancerBEAddressPool",
                            "properties": {}
                        }
                    ],
                    "loadBalancingRules": [
                        /* Add hello AppPort rule. Be sure tooreference hello "-Int" versions of backendAddressPool, frontendIPConfiguration, and hello probe variables. */
                        {
                            "name": "AppPortLBRule1",
                            "properties": {
                                "backendAddressPool": {
                                    "id": "[variables('lbPoolID0-Int')]"
                                },
                                "backendPort": "[parameters('loadBalancedAppPort1')]",
                                "enableFloatingIP": "false",
                                "frontendIPConfiguration": {
                                    "id": "[variables('lbIPConfig0-Int')]"
                                },
                                "frontendPort": "[parameters('loadBalancedAppPort1')]",
                                "idleTimeoutInMinutes": "5",
                                "probe": {
                                    "id": "[concat(variables('lbID0-Int'),'/probes/AppPortProbe1')]"
                                },
                                "protocol": "tcp"
                            }
                        }
                    ],
                    "probes": [
                    /* Add hello probe for hello app port. */
                    {
                            "name": "AppPortProbe1",
                            "properties": {
                                "intervalInSeconds": 5,
                                "numberOfProbes": 2,
                                "port": "[parameters('loadBalancedAppPort1')]",
                                "protocol": "tcp"
                            }
                        }
                    ],
                    "inboundNatPools": [
                    ]
                },
                "tags": {
                    "resourceType": "Service Fabric",
                    "clusterName": "[parameters('clusterName')]"
                }
            },
    ```

6. İçinde `networkProfile` hello için `Microsoft.Compute/virtualMachineScaleSets` kaynak hello iç arka uç adres havuzu ekleyin:

    ```
    "loadBalancerBackendAddressPools": [
                                                        {
                                                            "id": "[variables('lbPoolID0')]"
                                                        },
                                                        {
                                                            /* Add internal BE pool */
                                                            "id": "[variables('lbPoolID0-Int')]"
                                                        }
    ],
    ```

7. Merhaba şablonunu dağıtın:

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkinginternalexternallb -Location westus

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkinginternalexternallb -TemplateFile C:\SFSamples\Final\template\_internalexternalLB.json
    ```

Dağıtımdan sonra hello kaynak grubunda iki yük dengeleyici görebilirsiniz. Merhaba yük dengeleyici göz atarsanız, hello genel IP adresi ve yönetim atanan uç noktaları (ve bağlantı noktaları 19000 19080) toohello genel IP adresi görebilirsiniz. Merhaba statik iç IP adresi ve uygulama atanan uç noktasını (bağlantı noktası 80) toohello iç de görebilirsiniz yük dengeleyici. Yük Dengeleyici kullanın hello aynı sanal makine ölçek kümesi arka uç havuzu.

## <a name="next-steps"></a>Sonraki adımlar
[Küme oluşturma](service-fabric-cluster-creation-via-arm.md)
