---
title: "Azure kapsayıcı örnekleri - birden çok kapsayıcı grubu | Azure belgeleri"
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
ms.openlocfilehash: 140f58582645ea32f77e901eb13364ed145bbecf
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-a-container-group"></a><span data-ttu-id="aff22-103">Kapsayıcı grubu dağıtma</span><span class="sxs-lookup"><span data-stu-id="aff22-103">Deploy a container group</span></span>

<span data-ttu-id="aff22-104">Azure kapsayıcı örnekleri birden çok kapsayıcı kullanarak tek bir ana bilgisayar üzerine dağıtımını destekleyen bir *kapsayıcı grubu*.</span><span class="sxs-lookup"><span data-stu-id="aff22-104">Azure Container Instances support the deployment of multiple containers onto a single host using a *container group*.</span></span> <span data-ttu-id="aff22-105">Bu günlüğe kaydetme, izleme veya başka bir yapılandırma için bir uygulama sepet oluştururken bir hizmetin ikinci bir bağlı işlem nerede ihtiyaç yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="aff22-105">This is useful when building an application sidecar for logging, monitoring, or any other configuration where a service needs a second attached process.</span></span> 

<span data-ttu-id="aff22-106">Bu belge, Azure Resource Manager şablonu kullanarak basit çok kapsayıcı sepet yapılandırma çalıştıran anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="aff22-106">This document walks through running a simple multi-container sidecar configuration using an Azure Resource Manager template.</span></span>

## <a name="configure-the-template"></a><span data-ttu-id="aff22-107">Şablon yapılandırma</span><span class="sxs-lookup"><span data-stu-id="aff22-107">Configure the template</span></span>

<span data-ttu-id="aff22-108">Adlı bir dosya oluşturun `azuredeploy.json` ve aşağıdaki json dosyasını buraya kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="aff22-108">Create a file named `azuredeploy.json` and copy the following json into it.</span></span> 

<span data-ttu-id="aff22-109">Bu örnekte, bir kapsayıcı grubu iki kapsayıcıları ve genel bir IP adresi ile tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="aff22-109">In this sample, a container group with two containers and a public IP address is defined.</span></span> <span data-ttu-id="aff22-110">İlk kapsayıcı grubunun Internet karşılıklı uygulamasını çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="aff22-110">The first container of the group runs an internet facing application.</span></span> <span data-ttu-id="aff22-111">İkinci kapsayıcı, sepet grubun yerel ağ aracılığıyla ana web uygulaması için bir HTTP isteği yapar.</span><span class="sxs-lookup"><span data-stu-id="aff22-111">The second container, the sidecar, makes an HTTP request to the main web application via the group's local network.</span></span> 

<span data-ttu-id="aff22-112">Bu sepet örnek, bir HTTP yanıt kodu 200 dışında Tamam aldıysanız, bir uyarıyı tetiklemek için genişletilemiyor.</span><span class="sxs-lookup"><span data-stu-id="aff22-112">This sidecar example could be expanded to trigger an alert if it received an HTTP response code other than 200 OK.</span></span> 

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

<span data-ttu-id="aff22-113">Bir özel kapsayıcı görüntü kayıt defterini kullanmak için json belgesi aşağıdaki biçime sahip bir nesne ekleyin.</span><span class="sxs-lookup"><span data-stu-id="aff22-113">To use a private container image registry, add an object to the json document with the following format.</span></span>

```json
"imageRegistryCredentials": [
    {
    "server": "[parameters('imageRegistryLoginServer')]",
    "username": "[parameters('imageRegistryUsername')]",
    "password": "[parameters('imageRegistryPassword')]"
    }
]
```

## <a name="deploy-the-template"></a><span data-ttu-id="aff22-114">Şablonu dağıtma</span><span class="sxs-lookup"><span data-stu-id="aff22-114">Deploy the template</span></span>

<span data-ttu-id="aff22-115">[az group create](/cli/azure/group#create) komutuyla bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="aff22-115">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="aff22-116">Şablonla dağıtmak [az grup dağıtımı oluşturmak](/cli/azure/group/deployment#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="aff22-116">Deploy the template with the [az group deployment create](/cli/azure/group/deployment#create) command.</span></span>

```azurecli-interactive
az group deployment create --name myContainerGroup --resource-group myResourceGroup --template-file azuredeploy.json
```

<span data-ttu-id="aff22-117">Birkaç saniye içinde Azure'dan ilk yanıt alırsınız.</span><span class="sxs-lookup"><span data-stu-id="aff22-117">Within a few seconds, you will receive an initial response from Azure.</span></span> 

## <a name="view-deployment-state"></a><span data-ttu-id="aff22-118">Dağıtım durumunu görüntüle</span><span class="sxs-lookup"><span data-stu-id="aff22-118">View deployment state</span></span>

<span data-ttu-id="aff22-119">Dağıtım durumunu görüntülemek için kullanın `az container show` komutu.</span><span class="sxs-lookup"><span data-stu-id="aff22-119">To view the state of the deployment, use the `az container show` command.</span></span> <span data-ttu-id="aff22-120">Bu uygulama erişilebilen sağlanan genel IP adresini döndürür.</span><span class="sxs-lookup"><span data-stu-id="aff22-120">This returns the provisioned public IP address over which the application can be accessed.</span></span>

```azurecli-interactive
az container show --name myContainerGroup --resource-group myResourceGroup -o table
```

<span data-ttu-id="aff22-121">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="aff22-121">Output:</span></span>

```azurecli
Name              ResourceGroup    ProvisioningState    Image                                                             IP:ports           CPU/Memory    OsType    Location
----------------  ---------------  -------------------  ----------------------------------------------------------------  -----------------  ------------  --------  ----------
myContainerGroup  myResourceGrou2  Succeeded            microsoft/aci-tutorial-sidecar,microsoft/aci-tutorial-app:v1      40.118.253.154:80  1.0 core/1.5 gb   Linux     westus
```

## <a name="view-logs"></a><span data-ttu-id="aff22-122">Günlükleri görüntüle</span><span class="sxs-lookup"><span data-stu-id="aff22-122">View logs</span></span>   

<span data-ttu-id="aff22-123">Kullanarak bir kapsayıcı günlük çıktısını görüntüleyin `az container logs` komutu.</span><span class="sxs-lookup"><span data-stu-id="aff22-123">View the log output of a container using the `az container logs` command.</span></span> <span data-ttu-id="aff22-124">`--container-name` Bağımsız değişkeni günlüklerini kapsayıcıyı belirtir.</span><span class="sxs-lookup"><span data-stu-id="aff22-124">The `--container-name` argument specifies the container from which to pull logs.</span></span> <span data-ttu-id="aff22-125">Bu örnekte, ilk kapsayıcı belirtilir.</span><span class="sxs-lookup"><span data-stu-id="aff22-125">In this example, the first container is specified.</span></span> 

```azurecli-interactive
az container logs --name myContainerGroup --container-name aci-tutorial-app --resource-group myResourceGroup
```

<span data-ttu-id="aff22-126">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="aff22-126">Output:</span></span>

```bash
istening on port 80
::1 - - [27/Jul/2017:17:35:29 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:32 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:35 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:38 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
```

<span data-ttu-id="aff22-127">Yan araba kapsayıcısı için günlükleri görmek için ikinci kapsayıcı adı belirterek aynı komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="aff22-127">To see the logs for the side-car container, run the same command specifying the second container name.</span></span>

```azurecli-interactive
az container logs --name myContainerGroup --container-name aci-tutorial-sidecar --resource-group myResourceGroup
```

<span data-ttu-id="aff22-128">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="aff22-128">Output:</span></span>

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

<span data-ttu-id="aff22-129">Gördüğünüz gibi sepet bir HTTP isteği düzenli aralıklarla çalıştığından emin olmak için ana web uygulamasına grubun yerel ağ üzerinden yapılmasıdır.</span><span class="sxs-lookup"><span data-stu-id="aff22-129">As you can see, the sidecar is periodically making an HTTP request to the main web application via the group's local network to ensure that it is running.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aff22-130">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="aff22-130">Next steps</span></span>

<span data-ttu-id="aff22-131">Bu belgede bir çok kapsayıcı Azure kapsayıcı örneği dağıtmak için gerekli olan adımları ele.</span><span class="sxs-lookup"><span data-stu-id="aff22-131">This document covered the steps needed for deploying a multi-container Azure container instance.</span></span> <span data-ttu-id="aff22-132">Bir uçtan uca Azure kapsayıcı örnekleri deneyimi için Azure kapsayıcı örnekleri öğretici bakın.</span><span class="sxs-lookup"><span data-stu-id="aff22-132">For an end to end Azure Container Instances experience, see the Azure Container Instances tutorial.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="aff22-133">[Azure kapsayıcı örnekleri öğretici]:./container-instances-tutorial-prepare-app.md</span><span class="sxs-lookup"><span data-stu-id="aff22-133">[Azure Container Instances tutorial]: ./container-instances-tutorial-prepare-app.md</span></span>
