---
title: "Azure Service Fabric kapsayıcı hizmetlerini modlarını ağ aaaConfigure | Microsoft Docs"
description: "Toosetup hello farklı ağ modları, Azure Service Fabric nasıl destekler? öğrenin."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: d552c8cd-67d1-45e8-91dc-871853f44fc6
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 5c5dd4c590c7698a947503cbe8ef66ff7d6b503a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-container-networking-modes"></a>Service Fabric kapsayıcı ağ modları

Merhaba varsayılan ağ modu hello Service Fabric kümesi için kapsayıcı hizmetlerini hello sunulur `nat` ağ modu. Merhaba ile `nat` modu, birden fazla kapsayıcı hizmeti dinleme toohello sahip ağ aynı dağıtım hataları sonuçlarında bağlantı noktası. Aynı bağlantı noktasını, Service Fabric destekleyen hello üzerinde dinleme birkaç hizmetlerini çalıştırmak için hello `open` ağ modu (sürüm 5.7 veya daha yüksek). Merhaba ile `open` modu ağ, her kapsayıcı hizmeti dahili olarak aynı bağlantı noktasını birden çok Hizmetleri toolisten toohello izin vererek dinamik olarak atanmış bir IP adresi alır.   

Bu nedenle, hello hizmet bildiriminde tanımlanan statik bir uç noktası ile tek hizmet türü ile yeni hizmetleri oluşturulabilir ve hello kullanarak dağıtım hatasız silinmiş `open` ağ modu. Benzer şekilde, kullanabilirsiniz aynı hello `docker-compose.yml` birden fazla hizmet oluşturmak için dosya statik bağlantı noktası eşlemesi.

Merhaba hizmeti yeniden başlatır veya tooanother düğüme taşır dinamik olarak atanan IP toodiscover Hizmetleri hello kullanarak hello IP adresi değişiklikleri itibaren önerilmez. Yalnızca hello kullan **Service Fabric adlandırma hizmeti** veya hello **DNS hizmeti** hizmet bulmayı için. 


> [!WARNING]
> Yalnızca 4096 IP'leri toplam Azure vNET başına izin verilir. Bu nedenle, hello toplamını hello düğümlerinin hello sayısını ve kapsayıcı hizmeti örnekleri (ile `open` ağ) bir sanal ağ içindeki 4096 aşamaz. Bu tür yüksek yoğunluklu senaryoları için hello `nat` ağ modu önerilir.
>

## <a name="setting-up-open-networking-mode"></a>Açık ağ modunu ayarlama

1. DNS hizmeti etkinleştirerek Hello Azure Resource Manager şablon ayarlama ve IP sağlayıcısı altında hello `fabricSettings`. 

    ```json
    "fabricSettings": [
                {
                    "name": "DnsService",
                    "parameters": [
                       {
                            "name": "IsEnabled",
                            "value": "true"
                      }
                    ]
                },
                {
                    "name": "Hosting",
                    "parameters": [
                      { 
                            "name": "IPProviderEnabled",
                            "value": "true"
                      }
                    ]
                },
                {
                    "name":  "Trace/Etw", 
                    "parameters": [
                    {
                            "name": "Level",
                            "value": "5"
                    }
                    ]
                },
                {
                    "name": "Setup",
                    "parameters": [
                    {
                            "name": "ContainerNetworkSetup",
                            "value": "true"
                    }
                    ]
                }
            ],
    ```

2. Merhaba ağ profili bölüm tooallow toobe hello kümenin her düğümüne yapılandırılmış birden çok IP adresleriyle ayarlayın. Merhaba aşağıdaki örnek düğüm başına beş IP adreslerini kurar (Bu nedenle her düğüm toohello bağlantı noktasını dinleyen beş hizmet örnekleri olabilir) Windows Service Fabric kümesi için.

    ```json
    "variables": {
        "nicName": "NIC",
        "vmName": "vm",
        "virtualNetworkName": "VNet",
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
        "vmNodeType0Name": "[toLower(concat('NT1', variables('vmName')))]",
        "subnet0Name": "Subnet-0",
        "subnet0Prefix": "10.0.0.0/24",
        "subnet0Ref": "[concat(variables('vnetID'),'/subnets/',variables('subnet0Name'))]",
        "lbID0": "[resourceId('Microsoft.Network/loadBalancers',concat('LB','-', parameters('clusterName'),'-',variables('vmNodeType0Name')))]",
        "lbIPConfig0": "[concat(variables('lbID0'),'/frontendIPConfigurations/LoadBalancerIPConfig')]",
        "lbPoolID0": "[concat(variables('lbID0'),'/backendAddressPools/LoadBalancerBEAddressPool')]",
        "lbProbeID0": "[concat(variables('lbID0'),'/probes/FabricGatewayProbe')]",
        "lbHttpProbeID0": "[concat(variables('lbID0'),'/probes/FabricHttpGatewayProbe')]",
        "lbNatPoolID0": "[concat(variables('lbID0'),'/inboundNatPools/LoadBalancerBEAddressNatPool')]"
    }
    "networkProfile": {
                "networkInterfaceConfigurations": [
                  {
                    "name": "[concat(parameters('nicName'), '-0')]",
                    "properties": {
                      "ipConfigurations": [
                        {
                          "name": "[concat(parameters('nicName'),'-',0)]",
                          "properties": {
                            "primary": "true",
                            "loadBalancerBackendAddressPools": [
                              {
                                "id": "[variables('lbPoolID0')]"
                              }
                            ],
                            "loadBalancerInboundNatPools": [
                              {
                                "id": "[variables('lbNatPoolID0')]"
                              }
                            ],
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 1)]",
                          "properties": {
                            "primary": "false",
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 2)]",
                          "properties": {
                            "primary": "false",
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 3)]",
                          "properties": {
                            "primary": "false",
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 4)]",
                          "properties": {
                            "primary": "false",
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 5)]",
                          "properties": {
                            "primary": "false",
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        }
                      ],
                      "primary": true
                    }
                  }
                ]
              }
    ```

    Linux kümeleri için ek bir ortak IP yapılandırması tooallow giden bağlantı eklenir. Merhaba aşağıdaki kod parçacığında Linux kümesi için düğüm başına beş IP adresini ayarlar:

    ```json
    "networkProfile": {
                "networkInterfaceConfigurations": [
                  {
                    "name": "[concat(parameters('nicName'), '-0')]",
                    "properties": {
                      "ipConfigurations": [
                        {
                          "name": "[concat(parameters('nicName'),'-',0)]",
                          "properties": {
                            "primary": "true",
                            "publicipaddressconfiguration": {
                              "name": "devpub",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "loadBalancerBackendAddressPools": [
                              {
                                "id": "[variables('lbPoolID0')]"
                              }
                            ],
                            "loadBalancerInboundNatPools": [
                              {
                                "id": "[variables('lbNatPoolID0')]"
                              }
                            ],
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 1)]",
                          "properties": {
                            "primary": "false",
                            "publicipaddressconfiguration": {
                              "name": "[concat('devpub', 1)]",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 2)]",
                          "properties": {
                            "primary": "false",
                            "publicipaddressconfiguration": {
                              "name": "[concat('devpub', 2)]",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 3)]",
                          "properties": {
                            "primary": "false",
                            "publicipaddressconfiguration": {
                              "name": "[concat('devpub', 3)]",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 4)]",
                          "properties": {
                            "primary": "false",
                            "publicipaddressconfiguration": {
                              "name": "[concat('devpub', 4)]",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 5)]",
                          "properties": {
                            "primary": "false",
                            "publicipaddressconfiguration": {
                              "name": "[concat('devpub', 5)]",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        }
                      ],
                      "primary": true
                    }
                  }
                ]
              }
    ```

3. Yalnızca, bir NSG kümeleri Windows için yukarı bağlantı noktası UDP/53 hello vNET için değerleri aşağıdaki hello ile açma kural:

   | Öncelik |    Ad    |    Kaynak      |  Hedef   |   Hizmet    | Eylem |
   |:--------:|:----------:|:--------------:|:--------------:|:------------:|:------:|
   |     2000 | Custom_Dns | VirtualNetwork | VirtualNetwork | DNS (UDP/53) | İzin Ver  |


4. Her hizmet için hello uygulama bildiriminde Hello ağ modunu belirtin `<NetworkConfig NetworkType="open">`.  başlangıç modu `open` ayrılmış bir IP adresi alma hello hizmetinde neden olur. Bir mod belirtilmezse, toohello temel varsayılan olarak `nat` modu. Bu nedenle, aşağıdaki bildirim örneğine hello içinde `NodeContainerServicePackage1` ve `NodeContainerServicePackage2` her dinleme toohello için aynı bağlantı noktasını (her iki hizmetlerin dinlediği `Endpoint1`).

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <ApplicationManifest ApplicationTypeName="NodeJsApp" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
      <Description>Calculator Application</Description>
      <Parameters>
        <Parameter Name="ServiceInstanceCount" DefaultValue="3"></Parameter>
        <Parameter Name="MyCpuShares" DefaultValue="3"></Parameter>
      </Parameters>
      <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="NodeContainerServicePackage1" ServiceManifestVersion="1.0"/>
        <Policies>
          <ContainerHostPolicies CodePackageRef="NodeContainerService1.Code" Isolation="hyperv">
           <NetworkConfig NetworkType="open"/>
           <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
          </ContainerHostPolicies>
        </Policies>
      </ServiceManifestImport>
      <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="NodeContainerServicePackage2" ServiceManifestVersion="1.0"/>
        <Policies>
          <ContainerHostPolicies CodePackageRef="NodeContainerService2.Code" Isolation="default">
            <NetworkConfig NetworkType="open"/>
            <PortBinding ContainerPort="8910" EndpointRef="Endpoint1"/>
          </ContainerHostPolicies>
        </Policies>
      </ServiceManifestImport>
    </ApplicationManifest>
    ```
Karışık ve hizmetlerde Windows kümesi için bir uygulama içinde farklı ağ modları eşleşmesi. Bu nedenle, bazı hizmetler sahip `open` modu ve bazı üzerinde `nat` ağ modu. İle bir hizmeti yapılandırıldığında `nat`, başlangıç bağlantı noktasını dinleme toomust olduğu benzersiz olması. Farklı Hizmetleri için ağ modlarını karıştırma Linux kümeleri üzerinde desteklenmiyor. 


## <a name="next-steps"></a>Sonraki adımlar
Bu makalede, Service Fabric tarafından sunulan modları ağ hakkında öğrendiniz.  

* [Service Fabric uygulama modeli](service-fabric-application-model.md)
* [Service Fabric hizmet bildirimi kaynakları](service-fabric-application-model.md)
* [Bir Windows kapsayıcı tooService Windows Server 2016 doku dağıtma](service-fabric-get-started-containers.md)
* [Docker kapsayıcısı tooService doku Linux'ta dağıtma](service-fabric-get-started-containers-linux.md)
