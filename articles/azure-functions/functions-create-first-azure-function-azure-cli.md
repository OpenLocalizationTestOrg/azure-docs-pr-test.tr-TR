---
title: "İlk Azure CLI hello işlev aaaCreate | Microsoft Docs"
description: "Bilgi nasıl ilk Azure işlev kullanılarak sunucusuz yürütme için toocreate hello Azure CLI."
services: functions
keywords: 
author: ggailey777
ms.author: glenga
ms.assetid: 674a01a7-fd34-4775-8b69-893182742ae0
ms.date: 08/22/2017
ms.topic: hero-article
ms.service: functions
ms.custom: mvc
ms.devlang: azure-cli
manager: erikre
ms.openlocfilehash: 5feed0045d4998b88b0e1bb50996cb7bb42b0822
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-function-using-hello-azure-cli"></a>Hello Azure CLI kullanarak ilk işlevinizi oluşturma

Bu hızlı başlangıç Öğreticisi nasıl anlatılmaktadır toouse Azure işlevleri toocreate ilk işlevinizi. Hello Azure CLI toocreate işlevinizi barındıran hello sunucusuz altyapısıdır bir işlev uygulaması kullanın. Merhaba işlev kodu kendisini bir GitHub örnek depodan dağıtılır.    

Mac, Windows veya Linux bilgisayar kullanarak aşağıda hello adımları izleyebilirsiniz. 

## <a name="prerequisites"></a>Ön koşullar 

Bu örneği çalıştırmadan önce hello şunlara sahip olmanız gerekir:

+ Etkin bir [GitHub](https://github.com) hesabı. 
+ Etkin bir Azure aboneliği.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir. Çalıştırma `az --version` toofind hello sürümü. Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 


## <a name="create-a-resource-group"></a>Kaynak grubu oluşturma

Bir kaynak grubu ile Merhaba oluşturmak [az grubu oluşturma](/cli/azure/group#create). Azure kaynak grubu; işlev uygulamaları, veritabanları ve depolama hesapları gibi Azure kaynaklarının dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır.

Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu `myResourceGroup`.  
Cloud Shell kullanmıyorsanız önce `az login` kullanarak oturum açmanız gerekir.

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```


## <a name="create-an-azure-storage-account"></a>Azure Depolama hesabı oluşturma

İşlevler, bir Azure depolama hesabı toomaintain durumu ve işlevlerinizi ilgili diğer bilgileri kullanır. Merhaba kaynak grubunda hello kullanılarak oluşturulan depolama hesabı oluşturma [az depolama hesabı oluşturma](/cli/azure/storage/account#create) komutu.

Hello hello gördüğünüz kendi genel benzersiz depolama hesabı adı yerine komutu, aşağıdaki `<storage_name>` yer tutucu. Depolama hesabı adları 3 ile 24 karakter arasında olmalı ve yalnızca sayıyla küçük harf içermelidir.

```azurecli-interactive
az storage account create --name <storage_name> --location westeurope --resource-group myResourceGroup --sku Standard_LRS
```

Merhaba depolama hesabı oluşturulduktan sonra hello Azure CLI aşağıdaki örneğine benzer toohello bilgileri gösterir:

```json
{
  "creationTime": "2017-04-15T17:14:39.320307+00:00",
  "id": "/subscriptions/bbbef702-e769-477b-9f16-bc4d3aa97387/resourceGroups/myresourcegroup/...",
  "kind": "Storage",
  "location": "westeurope",
  "name": "myfunctionappstorage",
  "primaryEndpoints": {
    "blob": "https://myfunctionappstorage.blob.core.windows.net/",
    "file": "https://myfunctionappstorage.file.core.windows.net/",
    "queue": "https://myfunctionappstorage.queue.core.windows.net/",
    "table": "https://myfunctionappstorage.table.core.windows.net/"
  },
     ....
    // Remaining output has been truncated for readability.
}
```

## <a name="create-a-function-app"></a>İşlev uygulaması oluşturma

Bir işlev uygulaması toohost hello işlevlerinizin yürütülmesini olması gerekir. Merhaba işlev uygulaması işlevi kodunuzu sunucusuz yürütülmesi için bir ortam sağlar. Kaynakların daha kolay yönetilmesi, dağıtılması ve paylaşılması için işlevleri bir mantıksal birim olarak gruplandırmanıza olanak tanır. Hello kullanarak bir işlev uygulaması oluşturma [az functionapp oluşturma](/cli/azure/functionapp#create) komutu. 

Hello hello gördüğünüz kendi benzersiz işlevi uygulama adı yerine komutu, aşağıdaki `<app_name>` yer tutucu ve hello depolama hesabı adı için `<storage_name>`. Merhaba `<app_name>` hello varsayılan DNS etki alanı için hello işlev uygulaması ve bunu hello adı toobe benzersiz tüm uygulamalarında Azure gereksinimleriniz değiştikçe kullanılır. 

```azurecli-interactive
az functionapp create --name <app_name> --storage-account  <storage_name>  --resource-group myResourceGroup \
--consumption-plan-location westeurope
```
Varsayılan olarak, bu kaynaklar işlevlerinizi gerektirdiği gibi dinamik olarak eklenir ve işlevleri çalıştırırken yalnızca ödeme hello tüketim barındırma planı ile bir işlev uygulaması oluşturulur. Daha fazla bilgi için bkz: [Seç hello doğru barındırma planı](functions-scale.md). 

Merhaba işlev uygulaması oluşturulduktan sonra hello Azure CLI örnek aşağıdaki bilgileri benzer toohello gösterir:

```json
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "containerSize": 1536,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "quickstart.azurewebsites.net",
  "enabled": true,
  "enabledHostNames": [
    "quickstart.azurewebsites.net",
    "quickstart.scm.azurewebsites.net"
  ],
   ....
    // Remaining output has been truncated for readability.
}
```

Bir işlev uygulaması sahip olduğunuza göre hello gerçek işlev kodu hello GitHub örnek depodan dağıtabilirsiniz.

## <a name="deploy-your-function-code"></a>İşlev kodunuzu dağıtma  

Yeni işlev uygulamanız işlevi kodunuzu birkaç yolu toocreate vardır. Bu konuda tooa örnek GitHub deposunda bağlanır. Önceki gibi hello koddan Değiştir hello `<app_name>` yer tutucu oluşturduğunuz hello işlev uygulaması hello adı. 

```azurecli-interactive
az functionapp deployment source config --name <app_name> --resource-group myResourceGroup --branch master \
--repo-url https://github.com/Azure-Samples/functions-quickstart \
--manual-integration 
```
Merhaba dağıtımdan sonra kaynak ayarlandığı hello Azure CLI örneğin (okunabilirlik için kaldırılan null değerler) aşağıdaki bilgileri benzer toohello gösterir:

```json
{
  "branch": "master",
  "deploymentRollbackEnabled": false,
  "id": "/subscriptions/bbbef702-e769-477b-9f16-bc4d3aa97387/resourceGroups/myResourceGroup/...",
  "isManualIntegration": true,
  "isMercurial": false,
  "location": "West Europe",
  "name": "quickstart",
  "repoUrl": "https://github.com/Azure-Samples/functions-quickstart",
  "resourceGroup": "myResourceGroup",
  "type": "Microsoft.Web/sites/sourcecontrols"
}
```

## <a name="test-hello-function"></a>Test hello işlevi

Mac veya Linux bilgisayarda veya Bash Windows kullanarak cURL tootest dağıtılan hello işlevini kullanın. Merhaba değiştirme cURL komutunu aşağıdaki hello yürütme `<app_name>` yer tutucu işlevi uygulamanızı hello adı. Merhaba sorgu dizesi eklemek `&name=<yourname>` toohello URL.

```bash
curl http://<app_name>.azurewebsites.net/api/HttpTriggerJS1?name=<yourname>
```  

![Tarayıcıda gösterilen işlev yanıtı.](./media/functions-create-first-azure-function-azure-cli/functions-azure-cli-function-test-curl.png)  

Komut satırında kullanılabilir cURL yoksa girin'hello adresini web tarayıcınızı aynı URL'ye hello. Yeniden hello yerine `<app_name>` yer tutucu işlevi uygulamanızın hello adla ve hello sorgu dizesi eklemek `&name=<yourname>` toohello URL ve hello istek yürütülemiyor. 

    http://<app_name>.azurewebsites.net/api/HttpTriggerJS1?name=<yourname>
   
![Tarayıcıda gösterilen işlev yanıtı.](./media/functions-create-first-azure-function-azure-cli/functions-azure-cli-function-test-browser.png)  

## <a name="clean-up-resources"></a>Kaynakları temizleme

Bu koleksiyondaki diğer hızlı başlangıçlar, bu hızlı başlangıcı temel alır. Toowork sonraki quickstarts veya hello öğreticileri üzerinde toocontinue düşünüyorsanız yapmak bu quickstart oluşturulan hello kaynakları temizlemek değil. Toocontinue düşünmüyorsanız komutu toodelete aşağıdaki hello Bu hızlı başlangıç tarafından oluşturulan tüm kaynakları kullanın:

```azurecli-interactive
az group delete --name myResourceGroup
```
İstendiğinde `y` yazın.

## <a name="next-steps"></a>Sonraki adımlar

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]
