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
# <a name="service-fabric-container-networking-modes"></a><span data-ttu-id="6b2c7-103">Service Fabric kapsayıcı ağ modları</span><span class="sxs-lookup"><span data-stu-id="6b2c7-103">Service Fabric container networking modes</span></span>

<span data-ttu-id="6b2c7-104">Merhaba varsayılan ağ modu hello Service Fabric kümesi için kapsayıcı hizmetlerini hello sunulur `nat` ağ modu.</span><span class="sxs-lookup"><span data-stu-id="6b2c7-104">hello default networking mode offered in hello Service Fabric cluster for container services is hello `nat` networking mode.</span></span> <span data-ttu-id="6b2c7-105">Merhaba ile `nat` modu, birden fazla kapsayıcı hizmeti dinleme toohello sahip ağ aynı dağıtım hataları sonuçlarında bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="6b2c7-105">With hello `nat` networking mode, having more than one containers service listening toohello same port results in deployment errors.</span></span> <span data-ttu-id="6b2c7-106">Aynı bağlantı noktasını, Service Fabric destekleyen hello üzerinde dinleme birkaç hizmetlerini çalıştırmak için hello `open` ağ modu (sürüm 5.7 veya daha yüksek).</span><span class="sxs-lookup"><span data-stu-id="6b2c7-106">For running several services that listen on hello same port, Service Fabric supports hello `open` networking mode (version 5.7 or higher).</span></span> <span data-ttu-id="6b2c7-107">Merhaba ile `open` modu ağ, her kapsayıcı hizmeti dahili olarak aynı bağlantı noktasını birden çok Hizmetleri toolisten toohello izin vererek dinamik olarak atanmış bir IP adresi alır.</span><span class="sxs-lookup"><span data-stu-id="6b2c7-107">With hello `open` networking mode, each container service gets a dynamically assigned IP address internally allowing multiple services toolisten toohello same port.</span></span>   

<span data-ttu-id="6b2c7-108">Bu nedenle, hello hizmet bildiriminde tanımlanan statik bir uç noktası ile tek hizmet türü ile yeni hizmetleri oluşturulabilir ve hello kullanarak dağıtım hatasız silinmiş `open` ağ modu.</span><span class="sxs-lookup"><span data-stu-id="6b2c7-108">Thus, with a single service type with a static endpoint defined in hello service manifest, new services may be created and deleted without deployment errors using hello `open` networking mode.</span></span> <span data-ttu-id="6b2c7-109">Benzer şekilde, kullanabilirsiniz aynı hello `docker-compose.yml` birden fazla hizmet oluşturmak için dosya statik bağlantı noktası eşlemesi.</span><span class="sxs-lookup"><span data-stu-id="6b2c7-109">Similarly, one can use hello same `docker-compose.yml` file with static port mappings for creating multiple services.</span></span>

<span data-ttu-id="6b2c7-110">Merhaba hizmeti yeniden başlatır veya tooanother düğüme taşır dinamik olarak atanan IP toodiscover Hizmetleri hello kullanarak hello IP adresi değişiklikleri itibaren önerilmez.</span><span class="sxs-lookup"><span data-stu-id="6b2c7-110">Using hello dynamically assigned IP toodiscover services is not advisable since hello IP address changes when hello service restarts or moves tooanother node.</span></span> <span data-ttu-id="6b2c7-111">Yalnızca hello kullan **Service Fabric adlandırma hizmeti** veya hello **DNS hizmeti** hizmet bulmayı için.</span><span class="sxs-lookup"><span data-stu-id="6b2c7-111">Only use hello **Service Fabric Naming Service**  or hello **DNS Service** for service discovery.</span></span> 


> [!WARNING]
> <span data-ttu-id="6b2c7-112">Yalnızca 4096 IP'leri toplam Azure vNET başına izin verilir.</span><span class="sxs-lookup"><span data-stu-id="6b2c7-112">Only a total of 4096 IPs are allowed per vNET in Azure.</span></span> <span data-ttu-id="6b2c7-113">Bu nedenle, hello toplamını hello düğümlerinin hello sayısını ve kapsayıcı hizmeti örnekleri (ile `open` ağ) bir sanal ağ içindeki 4096 aşamaz.</span><span class="sxs-lookup"><span data-stu-id="6b2c7-113">Thus, hello sum of hello number of nodes and hello number of container service instances (with `open` networking) cannot exceed 4096 within a vNET.</span></span> <span data-ttu-id="6b2c7-114">Bu tür yüksek yoğunluklu senaryoları için hello `nat` ağ modu önerilir.</span><span class="sxs-lookup"><span data-stu-id="6b2c7-114">For such high-density scenarios, hello `nat` networking mode is recommended.</span></span>
>

## <a name="setting-up-open-networking-mode"></a><span data-ttu-id="6b2c7-115">Açık ağ modunu ayarlama</span><span class="sxs-lookup"><span data-stu-id="6b2c7-115">Setting up open networking mode</span></span>

1. <span data-ttu-id="6b2c7-116">DNS hizmeti etkinleştirerek Hello Azure Resource Manager şablon ayarlama ve IP sağlayıcısı altında hello `fabricSettings`.</span><span class="sxs-lookup"><span data-stu-id="6b2c7-116">Set up hello Azure Resource Manager template by enabling DNS Service and hello IP Provider under `fabricSettings`.</span></span> 

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

2. <span data-ttu-id="6b2c7-117">Merhaba ağ profili bölüm tooallow toobe hello kümenin her düğümüne yapılandırılmış birden çok IP adresleriyle ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="6b2c7-117">Set up hello network profile section tooallow multiple IP addresses toobe configured on each node of hello cluster.</span></span> <span data-ttu-id="6b2c7-118">Merhaba aşağıdaki örnek düğüm başına beş IP adreslerini kurar (Bu nedenle her düğüm toohello bağlantı noktasını dinleyen beş hizmet örnekleri olabilir) Windows Service Fabric kümesi için.</span><span class="sxs-lookup"><span data-stu-id="6b2c7-118">hello following example sets up five IP addresses per node (thus you can have five service instances listening toohello port on each node) for a Windows Service Fabric cluster.</span></span>

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

    <span data-ttu-id="6b2c7-119">Linux kümeleri için ek bir ortak IP yapılandırması tooallow giden bağlantı eklenir.</span><span class="sxs-lookup"><span data-stu-id="6b2c7-119">For Linux clusters, an additional public IP configuration is added tooallow outbound connectivity.</span></span> <span data-ttu-id="6b2c7-120">Merhaba aşağıdaki kod parçacığında Linux kümesi için düğüm başına beş IP adresini ayarlar:</span><span class="sxs-lookup"><span data-stu-id="6b2c7-120">hello following snippet sets up five IP addresses per node for a Linux cluster:</span></span>

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

3. <span data-ttu-id="6b2c7-121">Yalnızca, bir NSG kümeleri Windows için yukarı bağlantı noktası UDP/53 hello vNET için değerleri aşağıdaki hello ile açma kural:</span><span class="sxs-lookup"><span data-stu-id="6b2c7-121">For Windows clusters only, set up an NSG rule opening up port UDP/53 for hello vNET with hello following values:</span></span>

   | <span data-ttu-id="6b2c7-122">Öncelik</span><span class="sxs-lookup"><span data-stu-id="6b2c7-122">Priority</span></span> |    <span data-ttu-id="6b2c7-123">Ad</span><span class="sxs-lookup"><span data-stu-id="6b2c7-123">Name</span></span>    |    <span data-ttu-id="6b2c7-124">Kaynak</span><span class="sxs-lookup"><span data-stu-id="6b2c7-124">Source</span></span>      |  <span data-ttu-id="6b2c7-125">Hedef</span><span class="sxs-lookup"><span data-stu-id="6b2c7-125">Destination</span></span>   |   <span data-ttu-id="6b2c7-126">Hizmet</span><span class="sxs-lookup"><span data-stu-id="6b2c7-126">Service</span></span>    | <span data-ttu-id="6b2c7-127">Eylem</span><span class="sxs-lookup"><span data-stu-id="6b2c7-127">Action</span></span> |
   |:--------:|:----------:|:--------------:|:--------------:|:------------:|:------:|
   |     <span data-ttu-id="6b2c7-128">2000</span><span class="sxs-lookup"><span data-stu-id="6b2c7-128">2000</span></span> | <span data-ttu-id="6b2c7-129">Custom_Dns</span><span class="sxs-lookup"><span data-stu-id="6b2c7-129">Custom_Dns</span></span> | <span data-ttu-id="6b2c7-130">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="6b2c7-130">VirtualNetwork</span></span> | <span data-ttu-id="6b2c7-131">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="6b2c7-131">VirtualNetwork</span></span> | <span data-ttu-id="6b2c7-132">DNS (UDP/53)</span><span class="sxs-lookup"><span data-stu-id="6b2c7-132">DNS (UDP/53)</span></span> | <span data-ttu-id="6b2c7-133">İzin Ver</span><span class="sxs-lookup"><span data-stu-id="6b2c7-133">Allow</span></span>  |


4. <span data-ttu-id="6b2c7-134">Her hizmet için hello uygulama bildiriminde Hello ağ modunu belirtin `<NetworkConfig NetworkType="open">`.</span><span class="sxs-lookup"><span data-stu-id="6b2c7-134">Specify hello networking mode in hello app manifest for each service `<NetworkConfig NetworkType="open">`.</span></span>  <span data-ttu-id="6b2c7-135">başlangıç modu `open` ayrılmış bir IP adresi alma hello hizmetinde neden olur.</span><span class="sxs-lookup"><span data-stu-id="6b2c7-135">hello mode `open` results in hello service getting a dedicated IP address.</span></span> <span data-ttu-id="6b2c7-136">Bir mod belirtilmezse, toohello temel varsayılan olarak `nat` modu.</span><span class="sxs-lookup"><span data-stu-id="6b2c7-136">If a mode isn't specified, it defaults toohello basic `nat` mode.</span></span> <span data-ttu-id="6b2c7-137">Bu nedenle, aşağıdaki bildirim örneğine hello içinde `NodeContainerServicePackage1` ve `NodeContainerServicePackage2` her dinleme toohello için aynı bağlantı noktasını (her iki hizmetlerin dinlediği `Endpoint1`).</span><span class="sxs-lookup"><span data-stu-id="6b2c7-137">Thus, in hello following manifest example, `NodeContainerServicePackage1` and `NodeContainerServicePackage2` can each listen toohello same port (both services are listening on `Endpoint1`).</span></span>

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
<span data-ttu-id="6b2c7-138">Karışık ve hizmetlerde Windows kümesi için bir uygulama içinde farklı ağ modları eşleşmesi.</span><span class="sxs-lookup"><span data-stu-id="6b2c7-138">You can mix and match different networking modes across services within an application for a Windows cluster.</span></span> <span data-ttu-id="6b2c7-139">Bu nedenle, bazı hizmetler sahip `open` modu ve bazı üzerinde `nat` ağ modu.</span><span class="sxs-lookup"><span data-stu-id="6b2c7-139">Thus, you can have some services on `open` mode and some on `nat` networking mode.</span></span> <span data-ttu-id="6b2c7-140">İle bir hizmeti yapılandırıldığında `nat`, başlangıç bağlantı noktasını dinleme toomust olduğu benzersiz olması.</span><span class="sxs-lookup"><span data-stu-id="6b2c7-140">When a service is configured with `nat`, hello port it is listening toomust be unique.</span></span> <span data-ttu-id="6b2c7-141">Farklı Hizmetleri için ağ modlarını karıştırma Linux kümeleri üzerinde desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="6b2c7-141">Mixing networking modes for different services isn't supported on Linux clusters.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="6b2c7-142">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6b2c7-142">Next steps</span></span>
<span data-ttu-id="6b2c7-143">Bu makalede, Service Fabric tarafından sunulan modları ağ hakkında öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="6b2c7-143">In this article, you learned about networking modes offered by Service Fabric.</span></span>  

* [<span data-ttu-id="6b2c7-144">Service Fabric uygulama modeli</span><span class="sxs-lookup"><span data-stu-id="6b2c7-144">Service Fabric application model</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="6b2c7-145">Service Fabric hizmet bildirimi kaynakları</span><span class="sxs-lookup"><span data-stu-id="6b2c7-145">Service Fabric service manifest resources</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="6b2c7-146">Bir Windows kapsayıcı tooService Windows Server 2016 doku dağıtma</span><span class="sxs-lookup"><span data-stu-id="6b2c7-146">Deploy a Windows container tooService Fabric on Windows Server 2016</span></span>](service-fabric-get-started-containers.md)
* [<span data-ttu-id="6b2c7-147">Docker kapsayıcısı tooService doku Linux'ta dağıtma</span><span class="sxs-lookup"><span data-stu-id="6b2c7-147">Deploy a Docker container tooService Fabric on Linux</span></span>](service-fabric-get-started-containers-linux.md)
