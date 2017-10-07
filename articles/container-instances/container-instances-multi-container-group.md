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
# <a name="deploy-a-container-group"></a>Kapsayıcı grubu dağıtma

Azure kapsayıcı örnekleri birden çok kapsayıcı kullanarak tek bir ana bilgisayar üzerine hello dağıtımını destekleyen bir *kapsayıcı grubu*. Bu günlüğe kaydetme, izleme veya başka bir yapılandırma için bir uygulama sepet oluştururken bir hizmetin ikinci bir bağlı işlem nerede ihtiyaç yararlıdır. 

Bu belge, Azure Resource Manager şablonu kullanarak basit çok kapsayıcı sepet yapılandırma çalıştıran anlatılmaktadır.

## <a name="configure-hello-template"></a>Merhaba şablonu yapılandırma

Adlı bir dosya oluşturun `azuredeploy.json` ve kopyalama hello aşağıdaki json içine. 

Bu örnekte, bir kapsayıcı grubu iki kapsayıcıları ve genel bir IP adresi ile tanımlanır. Merhaba ilk kapsayıcı hello grubunun Internet karşılıklı uygulamasını çalıştırır. Merhaba ikinci kapsayıcı, hello sepet bir HTTP isteği toohello ana web uygulamasını hello grubun yerel ağ aracılığıyla yapar. 

Bir HTTP yanıt kodu 200 dışında Tamam aldıysanız bu sepet örnek genişletilmiş tootrigger bir uyarı olabilir. 

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

toouse özel kapsayıcı görüntü kayıt defteri biçimini izleyen hello bir nesne toohello json belgesi ekleyin.

```json
"imageRegistryCredentials": [
    {
    "server": "[parameters('imageRegistryLoginServer')]",
    "username": "[parameters('imageRegistryUsername')]",
    "password": "[parameters('imageRegistryPassword')]"
    }
]
```

## <a name="deploy-hello-template"></a>Merhaba şablonu dağıtma

Bir kaynak grubu ile Merhaba oluşturmak [az grubu oluşturma](/cli/azure/group#create) komutu.

```azurecli-interactive
az group create --name myResourceGroup --location westus
```

Merhaba Hello şablonla dağıtmak [az grup dağıtımı oluşturmak](/cli/azure/group/deployment#create) komutu.

```azurecli-interactive
az group deployment create --name myContainerGroup --resource-group myResourceGroup --template-file azuredeploy.json
```

Birkaç saniye içinde Azure'dan ilk yanıt alırsınız. 

## <a name="view-deployment-state"></a>Dağıtım durumunu görüntüle

Merhaba dağıtımının, kullanım hello tooview hello durumu `az container show` komutu. Bu uygulama hangi hello erişilebilir sağlanan hello genel IP adresi döndürür.

```azurecli-interactive
az container show --name myContainerGroup --resource-group myResourceGroup -o table
```

Çıktı:

```azurecli
Name              ResourceGroup    ProvisioningState    Image                                                             IP:ports           CPU/Memory    OsType    Location
----------------  ---------------  -------------------  ----------------------------------------------------------------  -----------------  ------------  --------  ----------
myContainerGroup  myResourceGrou2  Succeeded            microsoft/aci-tutorial-sidecar,microsoft/aci-tutorial-app:v1      40.118.253.154:80  1.0 core/1.5 gb   Linux     westus
```

## <a name="view-logs"></a>Günlükleri görüntüle   

Görüntüleme hello kullanarak bir kapsayıcı hello günlük çıktısı `az container logs` komutu. Merhaba `--container-name` bağımsız değişkeni hangi toopull günlükleri hello kapsayıcıdan belirtir. Bu örnekte, hello ilk kapsayıcı belirtilir. 

```azurecli-interactive
az container logs --name myContainerGroup --container-name aci-tutorial-app --resource-group myResourceGroup
```

Çıktı:

```bash
istening on port 80
::1 - - [27/Jul/2017:17:35:29 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:32 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:35 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:38 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
```

hello yan araba kapsayıcısı toosee hello günlükleri, hello çalıştırmak aynı belirten hello ikinci kapsayıcı adı komutu.

```azurecli-interactive
az container logs --name myContainerGroup --container-name aci-tutorial-sidecar --resource-group myResourceGroup
```

Çıktı:

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

Gördüğünüz gibi hello sepet düzenli aralıklarla bir HTTP isteği toohello ana web uygulaması çalıştığı hello grubun yerel ağ tooensure üzerinden yapılmasıdır.

## <a name="next-steps"></a>Sonraki adımlar

Bu belgede Azure kapsayıcı örneği birden çok kapsayıcı dağıtmak için gerekli hello adımları ele. Azure kapsayıcı örnekleri deneyimi bir bitiş tooend için hello Azure kapsayıcı örnekleri öğretici bakın.

> [!div class="nextstepaction"]
> [Azure kapsayıcı örnekleri öğretici]:./container-instances-tutorial-prepare-app.md
