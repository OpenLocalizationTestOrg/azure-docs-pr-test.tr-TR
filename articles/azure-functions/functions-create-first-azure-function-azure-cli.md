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
# <a name="create-your-first-function-using-hello-azure-cli"></a><span data-ttu-id="0faa9-103">Hello Azure CLI kullanarak ilk işlevinizi oluşturma</span><span class="sxs-lookup"><span data-stu-id="0faa9-103">Create your first function using hello Azure CLI</span></span>

<span data-ttu-id="0faa9-104">Bu hızlı başlangıç Öğreticisi nasıl anlatılmaktadır toouse Azure işlevleri toocreate ilk işlevinizi.</span><span class="sxs-lookup"><span data-stu-id="0faa9-104">This quickstart tutorial walks through how toouse Azure Functions toocreate your first function.</span></span> <span data-ttu-id="0faa9-105">Hello Azure CLI toocreate işlevinizi barındıran hello sunucusuz altyapısıdır bir işlev uygulaması kullanın.</span><span class="sxs-lookup"><span data-stu-id="0faa9-105">You use hello Azure CLI toocreate a function app, which is hello serverless infrastructure that hosts your function.</span></span> <span data-ttu-id="0faa9-106">Merhaba işlev kodu kendisini bir GitHub örnek depodan dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="0faa9-106">hello function code itself is deployed from a GitHub sample repository.</span></span>    

<span data-ttu-id="0faa9-107">Mac, Windows veya Linux bilgisayar kullanarak aşağıda hello adımları izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0faa9-107">You can follow hello steps below using a Mac, Windows, or Linux computer.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="0faa9-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="0faa9-108">Prerequisites</span></span> 

<span data-ttu-id="0faa9-109">Bu örneği çalıştırmadan önce hello şunlara sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="0faa9-109">Before running this sample, you must have hello following:</span></span>

+ <span data-ttu-id="0faa9-110">Etkin bir [GitHub](https://github.com) hesabı.</span><span class="sxs-lookup"><span data-stu-id="0faa9-110">An active [GitHub](https://github.com) account.</span></span> 
+ <span data-ttu-id="0faa9-111">Etkin bir Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="0faa9-111">An active Azure subscription.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="0faa9-112">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="0faa9-112">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="0faa9-113">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="0faa9-113">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="0faa9-114">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="0faa9-114">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="create-a-resource-group"></a><span data-ttu-id="0faa9-115">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="0faa9-115">Create a resource group</span></span>

<span data-ttu-id="0faa9-116">Bir kaynak grubu ile Merhaba oluşturmak [az grubu oluşturma](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="0faa9-116">Create a resource group with hello [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="0faa9-117">Azure kaynak grubu; işlev uygulamaları, veritabanları ve depolama hesapları gibi Azure kaynaklarının dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="0faa9-117">An Azure resource group is a logical container into which Azure resources like function apps, databases, and storage accounts are deployed and managed.</span></span>

<span data-ttu-id="0faa9-118">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="0faa9-118">hello following example creates a resource group named `myResourceGroup`.</span></span>  
<span data-ttu-id="0faa9-119">Cloud Shell kullanmıyorsanız önce `az login` kullanarak oturum açmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0faa9-119">If you are not using Cloud Shell, you must first sign in using `az login`.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```


## <a name="create-an-azure-storage-account"></a><span data-ttu-id="0faa9-120">Azure Depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="0faa9-120">Create an Azure Storage account</span></span>

<span data-ttu-id="0faa9-121">İşlevler, bir Azure depolama hesabı toomaintain durumu ve işlevlerinizi ilgili diğer bilgileri kullanır.</span><span class="sxs-lookup"><span data-stu-id="0faa9-121">Functions uses an Azure Storage account toomaintain state and other information about your functions.</span></span> <span data-ttu-id="0faa9-122">Merhaba kaynak grubunda hello kullanılarak oluşturulan depolama hesabı oluşturma [az depolama hesabı oluşturma](/cli/azure/storage/account#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="0faa9-122">Create a storage account in hello resource group you created by using hello [az storage account create](/cli/azure/storage/account#create) command.</span></span>

<span data-ttu-id="0faa9-123">Hello hello gördüğünüz kendi genel benzersiz depolama hesabı adı yerine komutu, aşağıdaki `<storage_name>` yer tutucu.</span><span class="sxs-lookup"><span data-stu-id="0faa9-123">In hello following command, substitute your own globally unique storage account name where you see hello `<storage_name>` placeholder.</span></span> <span data-ttu-id="0faa9-124">Depolama hesabı adları 3 ile 24 karakter arasında olmalı ve yalnızca sayıyla küçük harf içermelidir.</span><span class="sxs-lookup"><span data-stu-id="0faa9-124">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span>

```azurecli-interactive
az storage account create --name <storage_name> --location westeurope --resource-group myResourceGroup --sku Standard_LRS
```

<span data-ttu-id="0faa9-125">Merhaba depolama hesabı oluşturulduktan sonra hello Azure CLI aşağıdaki örneğine benzer toohello bilgileri gösterir:</span><span class="sxs-lookup"><span data-stu-id="0faa9-125">After hello storage account has been created, hello Azure CLI shows information similar toohello following example:</span></span>

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

## <a name="create-a-function-app"></a><span data-ttu-id="0faa9-126">İşlev uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="0faa9-126">Create a function app</span></span>

<span data-ttu-id="0faa9-127">Bir işlev uygulaması toohost hello işlevlerinizin yürütülmesini olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0faa9-127">You must have a function app toohost hello execution of your functions.</span></span> <span data-ttu-id="0faa9-128">Merhaba işlev uygulaması işlevi kodunuzu sunucusuz yürütülmesi için bir ortam sağlar.</span><span class="sxs-lookup"><span data-stu-id="0faa9-128">hello function app provides an environment for serverless execution of your function code.</span></span> <span data-ttu-id="0faa9-129">Kaynakların daha kolay yönetilmesi, dağıtılması ve paylaşılması için işlevleri bir mantıksal birim olarak gruplandırmanıza olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="0faa9-129">It lets you group functions as a logic unit for easier management, deployment, and sharing of resources.</span></span> <span data-ttu-id="0faa9-130">Hello kullanarak bir işlev uygulaması oluşturma [az functionapp oluşturma](/cli/azure/functionapp#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="0faa9-130">Create a function app by using hello [az functionapp create](/cli/azure/functionapp#create) command.</span></span> 

<span data-ttu-id="0faa9-131">Hello hello gördüğünüz kendi benzersiz işlevi uygulama adı yerine komutu, aşağıdaki `<app_name>` yer tutucu ve hello depolama hesabı adı için `<storage_name>`.</span><span class="sxs-lookup"><span data-stu-id="0faa9-131">In hello following command, substitute your own unique function app name where you see hello `<app_name>` placeholder and hello storage account name for  `<storage_name>`.</span></span> <span data-ttu-id="0faa9-132">Merhaba `<app_name>` hello varsayılan DNS etki alanı için hello işlev uygulaması ve bunu hello adı toobe benzersiz tüm uygulamalarında Azure gereksinimleriniz değiştikçe kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0faa9-132">hello `<app_name>` is used as hello default DNS domain for hello function app, and so hello name needs toobe unique across all apps in Azure.</span></span> 

```azurecli-interactive
az functionapp create --name <app_name> --storage-account  <storage_name>  --resource-group myResourceGroup \
--consumption-plan-location westeurope
```
<span data-ttu-id="0faa9-133">Varsayılan olarak, bu kaynaklar işlevlerinizi gerektirdiği gibi dinamik olarak eklenir ve işlevleri çalıştırırken yalnızca ödeme hello tüketim barındırma planı ile bir işlev uygulaması oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="0faa9-133">By default, a function app is created with hello Consumption hosting plan, which means that resources are added dynamically as required by your functions and you only pay when functions are running.</span></span> <span data-ttu-id="0faa9-134">Daha fazla bilgi için bkz: [Seç hello doğru barındırma planı](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="0faa9-134">For more information, see [Choose hello correct hosting plan](functions-scale.md).</span></span> 

<span data-ttu-id="0faa9-135">Merhaba işlev uygulaması oluşturulduktan sonra hello Azure CLI örnek aşağıdaki bilgileri benzer toohello gösterir:</span><span class="sxs-lookup"><span data-stu-id="0faa9-135">After hello function app has been created, hello Azure CLI shows information similar toohello following example:</span></span>

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

<span data-ttu-id="0faa9-136">Bir işlev uygulaması sahip olduğunuza göre hello gerçek işlev kodu hello GitHub örnek depodan dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0faa9-136">Now that you have a function app, you can deploy hello actual function code from hello GitHub sample repository.</span></span>

## <a name="deploy-your-function-code"></a><span data-ttu-id="0faa9-137">İşlev kodunuzu dağıtma</span><span class="sxs-lookup"><span data-stu-id="0faa9-137">Deploy your function code</span></span>  

<span data-ttu-id="0faa9-138">Yeni işlev uygulamanız işlevi kodunuzu birkaç yolu toocreate vardır.</span><span class="sxs-lookup"><span data-stu-id="0faa9-138">There are several ways toocreate your function code in your new function app.</span></span> <span data-ttu-id="0faa9-139">Bu konuda tooa örnek GitHub deposunda bağlanır.</span><span class="sxs-lookup"><span data-stu-id="0faa9-139">This topic connects tooa sample repository in GitHub.</span></span> <span data-ttu-id="0faa9-140">Önceki gibi hello koddan Değiştir hello `<app_name>` yer tutucu oluşturduğunuz hello işlev uygulaması hello adı.</span><span class="sxs-lookup"><span data-stu-id="0faa9-140">As before, in hello following code replace hello `<app_name>` placeholder with hello name of hello function app you created.</span></span> 

```azurecli-interactive
az functionapp deployment source config --name <app_name> --resource-group myResourceGroup --branch master \
--repo-url https://github.com/Azure-Samples/functions-quickstart \
--manual-integration 
```
<span data-ttu-id="0faa9-141">Merhaba dağıtımdan sonra kaynak ayarlandığı hello Azure CLI örneğin (okunabilirlik için kaldırılan null değerler) aşağıdaki bilgileri benzer toohello gösterir:</span><span class="sxs-lookup"><span data-stu-id="0faa9-141">After hello deployment source been set, hello Azure CLI shows information similar toohello following example (null values removed for readability):</span></span>

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

## <a name="test-hello-function"></a><span data-ttu-id="0faa9-142">Test hello işlevi</span><span class="sxs-lookup"><span data-stu-id="0faa9-142">Test hello function</span></span>

<span data-ttu-id="0faa9-143">Mac veya Linux bilgisayarda veya Bash Windows kullanarak cURL tootest dağıtılan hello işlevini kullanın.</span><span class="sxs-lookup"><span data-stu-id="0faa9-143">Use cURL tootest hello deployed function on a Mac or Linux computer or using Bash on Windows.</span></span> <span data-ttu-id="0faa9-144">Merhaba değiştirme cURL komutunu aşağıdaki hello yürütme `<app_name>` yer tutucu işlevi uygulamanızı hello adı.</span><span class="sxs-lookup"><span data-stu-id="0faa9-144">Execute hello following cURL command, replacing hello `<app_name>` placeholder with hello name of your function app.</span></span> <span data-ttu-id="0faa9-145">Merhaba sorgu dizesi eklemek `&name=<yourname>` toohello URL.</span><span class="sxs-lookup"><span data-stu-id="0faa9-145">Append hello query string `&name=<yourname>` toohello URL.</span></span>

```bash
curl http://<app_name>.azurewebsites.net/api/HttpTriggerJS1?name=<yourname>
```  

![Tarayıcıda gösterilen işlev yanıtı.](./media/functions-create-first-azure-function-azure-cli/functions-azure-cli-function-test-curl.png)  

<span data-ttu-id="0faa9-147">Komut satırında kullanılabilir cURL yoksa girin'hello adresini web tarayıcınızı aynı URL'ye hello.</span><span class="sxs-lookup"><span data-stu-id="0faa9-147">If you don't have cURL available in your command line, enter hello same URL in hello address of your web browser.</span></span> <span data-ttu-id="0faa9-148">Yeniden hello yerine `<app_name>` yer tutucu işlevi uygulamanızın hello adla ve hello sorgu dizesi eklemek `&name=<yourname>` toohello URL ve hello istek yürütülemiyor.</span><span class="sxs-lookup"><span data-stu-id="0faa9-148">Again, replace hello `<app_name>` placeholder with hello name of your function app, and append hello query string `&name=<yourname>` toohello URL and execute hello request.</span></span> 

    http://<app_name>.azurewebsites.net/api/HttpTriggerJS1?name=<yourname>
   
![Tarayıcıda gösterilen işlev yanıtı.](./media/functions-create-first-azure-function-azure-cli/functions-azure-cli-function-test-browser.png)  

## <a name="clean-up-resources"></a><span data-ttu-id="0faa9-150">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="0faa9-150">Clean up resources</span></span>

<span data-ttu-id="0faa9-151">Bu koleksiyondaki diğer hızlı başlangıçlar, bu hızlı başlangıcı temel alır.</span><span class="sxs-lookup"><span data-stu-id="0faa9-151">Other quickstarts in this collection build upon this quickstart.</span></span> <span data-ttu-id="0faa9-152">Toowork sonraki quickstarts veya hello öğreticileri üzerinde toocontinue düşünüyorsanız yapmak bu quickstart oluşturulan hello kaynakları temizlemek değil.</span><span class="sxs-lookup"><span data-stu-id="0faa9-152">If you plan toocontinue on toowork with subsequent quickstarts or with hello tutorials, do not clean up hello resources created in this quickstart.</span></span> <span data-ttu-id="0faa9-153">Toocontinue düşünmüyorsanız komutu toodelete aşağıdaki hello Bu hızlı başlangıç tarafından oluşturulan tüm kaynakları kullanın:</span><span class="sxs-lookup"><span data-stu-id="0faa9-153">If you do not plan toocontinue, use hello following command toodelete all resources created by this quickstart:</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```
<span data-ttu-id="0faa9-154">İstendiğinde `y` yazın.</span><span class="sxs-lookup"><span data-stu-id="0faa9-154">Type `y` when prompted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0faa9-155">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0faa9-155">Next steps</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]
