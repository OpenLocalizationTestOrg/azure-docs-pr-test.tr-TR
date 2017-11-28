---
title: "aaaAzure kapsayıcı örnekleri - birden çok kapsayıcı grubu | Azure belgeleri"
description: "Azure kapsayıcı örnekleri - birden çok kapsayıcı grubu"
services: container-instances
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 976f578cd2a9bf7f05ab97f24662139bb72062ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-container-group"></a><span data-ttu-id="9eeb4-103">Kapsayıcı grubu dağıtma</span><span class="sxs-lookup"><span data-stu-id="9eeb4-103">Deploy a container group</span></span>

<span data-ttu-id="9eeb4-104">Azure kapsayıcı örnekleri birden çok kapsayıcı kullanarak tek bir ana bilgisayar üzerine hello dağıtımını destekleyen bir *kapsayıcı grubu*.</span><span class="sxs-lookup"><span data-stu-id="9eeb4-104">Azure Container Instances support hello deployment of multiple containers onto a single host using a *container group*.</span></span> <span data-ttu-id="9eeb4-105">Bu günlüğe kaydetme, izleme veya başka bir yapılandırma için bir uygulama sepet oluştururken bir hizmetin ikinci bir bağlı işlem nerede ihtiyaç yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="9eeb4-105">This is useful when building an application sidecar for logging, monitoring, or any other configuration where a service needs a second attached process.</span></span> 

<span data-ttu-id="9eeb4-106">Bu belge, Azure Resource Manager şablonu kullanarak basit çok kapsayıcı sepet yapılandırma çalıştıran anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="9eeb4-106">This document walks through running a simple multi-container sidecar configuration using an Azure Resource Manager template.</span></span>

## <a name="configure-hello-template"></a><span data-ttu-id="9eeb4-107">Merhaba şablonu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="9eeb4-107">Configure hello template</span></span>

<span data-ttu-id="9eeb4-108">Adlı bir dosya oluşturun `azuredeploy.json` ve kopyalama hello aşağıdaki json içine.</span><span class="sxs-lookup"><span data-stu-id="9eeb4-108">Create a file named `azuredeploy.json` and copy hello following json into it.</span></span> 

<span data-ttu-id="9eeb4-109">Bu örnekte, bir kapsayıcı grubu iki kapsayıcıları ve genel bir IP adresi ile tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="9eeb4-109">In this sample, a container group with two containers and a public IP address is defined.</span></span> <span data-ttu-id="9eeb4-110">Merhaba ilk kapsayıcı hello grubunun Internet karşılıklı uygulamasını çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="9eeb4-110">hello first container of hello group runs an internet facing application.</span></span> <span data-ttu-id="9eeb4-111">Merhaba ikinci kapsayıcı, hello sepet bir HTTP isteği toohello ana web uygulamasını hello grubun yerel ağ aracılığıyla yapar.</span><span class="sxs-lookup"><span data-stu-id="9eeb4-111">hello second container, hello sidecar, makes an HTTP request toohello main web application via hello group's local network.</span></span> 

<span data-ttu-id="9eeb4-112">Bir HTTP yanıt kodu 200 dışında Tamam aldıysanız bu sepet örnek genişletilmiş tootrigger bir uyarı olabilir.</span><span class="sxs-lookup"><span data-stu-id="9eeb4-112">This sidecar example could be expanded tootrigger an alert if it received an HTTP response code other than 200 OK.</span></span> 

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
  },
  "variables": {
    "container1name": "aci-tutorial-app",
    "container1image": "microsoft/aci-helloworld:latest",
    "container2name": "aci-tutorial-sidecar",    
    "container2image": "microsoft/aci-tutorial-sidecar"
  },
    "resources": [
      {
        "name": "myContainerGroup",
        "type": "Microsoft.ContainerInstance/containerGroups",
        "apiVersion": "2017-08-01-preview",
        "location": "[resourceGroup().location]",
        "properties": {
          "containers": [
            {
              "name": "[variables('container1name')]",
              "properties": {
                "image": "[variables('container1image')]",
                "resources": {
                  "requests": {
                    "cpu": 1,
                    "memoryInGb": 1.5
                    }
                },
                "ports": [
                  {
                    "port": 80
                  }
                ]
              }
            },
            {
              "name": "[variables('container2name')]",
              "properties": {
                "image": "[variables('container2image')]",
                "resources": {
                  "requests": {
                    "cpu": 1,
                    "memoryInGb": 1.5
                    }
                }
              }
            }
          ],
          "osType": "Linux",
          "ipAddress": {
            "type": "Public",
            "ports": [
              {
                "protocol": "tcp",
                "port": "80"
              }
            ]
          }
        }
      }
    ],
    "outputs": {
      "containerIPv4Address": {
        "type": "string",
        "value": "[reference(resourceId('Microsoft.ContainerInstance/containerGroups/', 'myContainerGroup')).ipAddress.ip]"
      }
    }
  }
```

<span data-ttu-id="9eeb4-113">toouse özel kapsayıcı görüntü kayıt defteri biçimini izleyen hello bir nesne toohello json belgesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9eeb4-113">toouse a private container image registry, add an object toohello json document with hello following format.</span></span>

```json
"imageRegistryCredentials": [
    {
    "server": "[parameters('imageRegistryLoginServer')]",
    "username": "[parameters('imageRegistryUsername')]",
    "password": "[parameters('imageRegistryPassword')]"
    }
]
```

## <a name="deploy-hello-template"></a><span data-ttu-id="9eeb4-114">Merhaba şablonu dağıtma</span><span class="sxs-lookup"><span data-stu-id="9eeb4-114">Deploy hello template</span></span>

<span data-ttu-id="9eeb4-115">Bir kaynak grubu ile Merhaba oluşturmak [az grubu oluşturma](/cli/azure/group#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="9eeb4-115">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="9eeb4-116">Merhaba Hello şablonla dağıtmak [az grup dağıtımı oluşturmak](/cli/azure/group/deployment#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="9eeb4-116">Deploy hello template with hello [az group deployment create](/cli/azure/group/deployment#create) command.</span></span>

```azurecli-interactive
az group deployment create --name myContainerGroup --resource-group myResourceGroup --template-file azuredeploy.json
```

<span data-ttu-id="9eeb4-117">Birkaç saniye içinde Azure'dan ilk yanıt alırsınız.</span><span class="sxs-lookup"><span data-stu-id="9eeb4-117">Within a few seconds, you will receive an initial response from Azure.</span></span> 

## <a name="view-deployment-state"></a><span data-ttu-id="9eeb4-118">Dağıtım durumunu görüntüle</span><span class="sxs-lookup"><span data-stu-id="9eeb4-118">View deployment state</span></span>

<span data-ttu-id="9eeb4-119">Merhaba dağıtımının, kullanım hello tooview hello durumu `az container show` komutu.</span><span class="sxs-lookup"><span data-stu-id="9eeb4-119">tooview hello state of hello deployment, use hello `az container show` command.</span></span> <span data-ttu-id="9eeb4-120">Bu uygulama hangi hello erişilebilir sağlanan hello genel IP adresi döndürür.</span><span class="sxs-lookup"><span data-stu-id="9eeb4-120">This returns hello provisioned public IP address over which hello application can be accessed.</span></span>

```azurecli-interactive
az container show --name myContainerGroup --resource-group myResourceGroup -o table
```

<span data-ttu-id="9eeb4-121">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="9eeb4-121">Output:</span></span>

```azurecli
Name              ResourceGroup    ProvisioningState    Image                                                             IP:ports           CPU/Memory    OsType    Location
----------------  ---------------  -------------------  ----------------------------------------------------------------  -----------------  ------------  --------  ----------
myContainerGroup  myResourceGrou2  Succeeded            microsoft/aci-tutorial-sidecar,microsoft/aci-tutorial-app:v1      40.118.253.154:80  1.0 core/1.5 gb   Linux     westus
```

## <a name="view-logs"></a><span data-ttu-id="9eeb4-122">Günlükleri görüntüle</span><span class="sxs-lookup"><span data-stu-id="9eeb4-122">View logs</span></span>   

<span data-ttu-id="9eeb4-123">Görüntüleme hello kullanarak bir kapsayıcı hello günlük çıktısı `az container logs` komutu.</span><span class="sxs-lookup"><span data-stu-id="9eeb4-123">View hello log output of a container using hello `az container logs` command.</span></span> <span data-ttu-id="9eeb4-124">Merhaba `--container-name` bağımsız değişkeni hangi toopull günlükleri hello kapsayıcıdan belirtir.</span><span class="sxs-lookup"><span data-stu-id="9eeb4-124">hello `--container-name` argument specifies hello container from which toopull logs.</span></span> <span data-ttu-id="9eeb4-125">Bu örnekte, hello ilk kapsayıcı belirtilir.</span><span class="sxs-lookup"><span data-stu-id="9eeb4-125">In this example, hello first container is specified.</span></span> 

```azurecli-interactive
az container logs --name myContainerGroup --container-name aci-tutorial-app --resource-group myResourceGroup
```

<span data-ttu-id="9eeb4-126">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="9eeb4-126">Output:</span></span>

```bash
istening on port 80
::1 - - [27/Jul/2017:17:35:29 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:32 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:35 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:38 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
```

<span data-ttu-id="9eeb4-127">hello yan araba kapsayıcısı toosee hello günlükleri, hello çalıştırmak aynı belirten hello ikinci kapsayıcı adı komutu.</span><span class="sxs-lookup"><span data-stu-id="9eeb4-127">toosee hello logs for hello side-car container, run hello same command specifying hello second container name.</span></span>

```azurecli-interactive
az container logs --name myContainerGroup --container-name aci-tutorial-sidecar --resource-group myResourceGroup
```

<span data-ttu-id="9eeb4-128">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="9eeb4-128">Output:</span></span>

```bash
Every 3.0s: curl -I http://localhost                                                                                                                       Mon Jul 17 11:27:36 2017

  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0  0  1663    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0
HTTP/1.1 200 OK
Accept-Ranges: bytes
Content-Length: 1663
Content-Type: text/html; charset=utf-8
Last-Modified: Sun, 16 Jul 2017 02:08:22 GMT
Date: Mon, 17 Jul 2017 18:27:36 GMT
```

<span data-ttu-id="9eeb4-129">Gördüğünüz gibi hello sepet düzenli aralıklarla bir HTTP isteği toohello ana web uygulaması çalıştığı hello grubun yerel ağ tooensure üzerinden yapılmasıdır.</span><span class="sxs-lookup"><span data-stu-id="9eeb4-129">As you can see, hello sidecar is periodically making an HTTP request toohello main web application via hello group's local network tooensure that it is running.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9eeb4-130">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9eeb4-130">Next steps</span></span>

<span data-ttu-id="9eeb4-131">Bu belgede Azure kapsayıcı örneği birden çok kapsayıcı dağıtmak için gerekli hello adımları ele.</span><span class="sxs-lookup"><span data-stu-id="9eeb4-131">This document covered hello steps needed for deploying a multi-container Azure container instance.</span></span> <span data-ttu-id="9eeb4-132">Azure kapsayıcı örnekleri deneyimi bir bitiş tooend için hello Azure kapsayıcı örnekleri öğretici bakın.</span><span class="sxs-lookup"><span data-stu-id="9eeb4-132">For an end tooend Azure Container Instances experience, see hello Azure Container Instances tutorial.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="9eeb4-133">[Azure kapsayıcı örnekleri öğretici]:./container-instances-tutorial-prepare-app.md</span><span class="sxs-lookup"><span data-stu-id="9eeb4-133">[Azure Container Instances tutorial]: ./container-instances-tutorial-prepare-app.md</span></span>
