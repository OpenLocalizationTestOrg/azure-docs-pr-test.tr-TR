---
title: "REST API ve şablon aaaDeploy kaynaklarla | Microsoft Docs"
description: "Azure Resource Manager ve Resource Manager REST API'si toodeploy kaynakları tooAzure kullanın. Merhaba kaynaklar bir Resource Manager şablonunda tanımlanır."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 1d8fbd4c-78b0-425b-ba76-f2b7fd260b45
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/10/2017
ms.author: tomfitz
ms.openlocfilehash: 347ad3bdb604429e7291297d448688204af69b46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-resource-manager-rest-api"></a><span data-ttu-id="ff251-104">Kaynakları Resource Manager şablonları ve Resource Manager REST API’si ile dağıtma</span><span class="sxs-lookup"><span data-stu-id="ff251-104">Deploy resources with Resource Manager templates and Resource Manager REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ff251-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ff251-105">PowerShell</span></span>](resource-group-template-deploy.md)
> * [<span data-ttu-id="ff251-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ff251-106">Azure CLI</span></span>](resource-group-template-deploy-cli.md)
> * [<span data-ttu-id="ff251-107">Portal</span><span class="sxs-lookup"><span data-stu-id="ff251-107">Portal</span></span>](resource-group-template-deploy-portal.md)
> * [<span data-ttu-id="ff251-108">REST API</span><span class="sxs-lookup"><span data-stu-id="ff251-108">REST API</span></span>](resource-group-template-deploy-rest.md)
> 
> 

<span data-ttu-id="ff251-109">Bu makalede nasıl toouse hello Resource Manager REST API'si ile Resource Manager şablonları toodeploy kaynakları tooAzure açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ff251-109">This article explains how toouse hello Resource Manager REST API with Resource Manager templates toodeploy your resources tooAzure.</span></span>  

> [!TIP]
> <span data-ttu-id="ff251-110">Dağıtım sırasında bir hata ayıklama daha fazla yardım için bkz:</span><span class="sxs-lookup"><span data-stu-id="ff251-110">For help with debugging an error during deployment, see:</span></span>
> 
> * <span data-ttu-id="ff251-111">[Dağıtım işlemlerini görüntülemek](resource-manager-deployment-operations.md) toolearn yardımcı olacak bilgileri alma hakkında sorun giderme, hata</span><span class="sxs-lookup"><span data-stu-id="ff251-111">[View deployment operations](resource-manager-deployment-operations.md) toolearn about getting information that helps you troubleshoot your error</span></span>
> * <span data-ttu-id="ff251-112">[Azure Resource Manager ile kaynakları tooAzure dağıtırken sık karşılaşılan sorunları giderme](resource-manager-common-deployment-errors.md) toolearn nasıl tooresolve ortak dağıtım hataları</span><span class="sxs-lookup"><span data-stu-id="ff251-112">[Troubleshoot common errors when deploying resources tooAzure with Azure Resource Manager](resource-manager-common-deployment-errors.md) toolearn how tooresolve common deployment errors</span></span>
> 
> 

<span data-ttu-id="ff251-113">Şablonunuz, yerel bir dosya veya bir URI kullanılabilir olan dış dosyası olabilir.</span><span class="sxs-lookup"><span data-stu-id="ff251-113">Your template can be either a local file or an external file that is available through a URI.</span></span> <span data-ttu-id="ff251-114">Şablonunuzu bir depolama hesabında bulunduğunda, access toohello şablonu kısıtlamak ve dağıtım sırasında bir paylaşılan erişim imzası (SAS) belirteci sağlayın.</span><span class="sxs-lookup"><span data-stu-id="ff251-114">When your template resides in a storage account, you can restrict access toohello template and provide a shared access signature (SAS) token during deployment.</span></span>

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

## <a name="deploy-with-hello-rest-api"></a><span data-ttu-id="ff251-115">REST API Hello ile dağıtma</span><span class="sxs-lookup"><span data-stu-id="ff251-115">Deploy with hello REST API</span></span>
1. <span data-ttu-id="ff251-116">Ayarlama [ortak parametrelerini ve üstbilgileri](https://docs.microsoft.com/rest/api/index), kimlik doğrulama belirteçleri de dahil olmak üzere.</span><span class="sxs-lookup"><span data-stu-id="ff251-116">Set [common parameters and headers](https://docs.microsoft.com/rest/api/index), including authentication tokens.</span></span>
2. <span data-ttu-id="ff251-117">Varolan bir kaynak grubu yoksa, bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ff251-117">If you do not have an existing resource group, create a resource group.</span></span> <span data-ttu-id="ff251-118">Abonelik kimliği, hello yeni kaynak grubunu ve çözümünüz için gereksinim duyduğunuz konumu hello adını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="ff251-118">Provide your subscription ID, hello name of hello new resource group, and location that you need for your solution.</span></span> <span data-ttu-id="ff251-119">Daha fazla bilgi için bkz: [bir kaynak grubu oluşturmak](https://docs.microsoft.com/rest/api/resources/resourcegroups#ResourceGroups_CreateOrUpdate).</span><span class="sxs-lookup"><span data-stu-id="ff251-119">For more information, see [Create a resource group](https://docs.microsoft.com/rest/api/resources/resourcegroups#ResourceGroups_CreateOrUpdate).</span></span>
   
        PUT https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>?api-version=2015-01-01
          <common headers>
          {
            "location": "West US",
            "tags": {
               "tagname1": "tagvalue1"
            }
          }
3. <span data-ttu-id="ff251-120">Merhaba çalıştırarak çalıştırmadan önce dağıtımınızı doğrulama [şablon dağıtımı doğrulamak](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Validate) işlemi.</span><span class="sxs-lookup"><span data-stu-id="ff251-120">Validate your deployment before executing it by running hello [Validate a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Validate) operation.</span></span> <span data-ttu-id="ff251-121">Tam olarak (Merhaba sonraki adımda gösterilen) hello dağıtım yürütülürken gibi hello dağıtım sınarken parametreleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="ff251-121">When testing hello deployment, provide parameters exactly as you would when executing hello deployment (shown in hello next step).</span></span>
4. <span data-ttu-id="ff251-122">Bir dağıtım oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ff251-122">Create a deployment.</span></span> <span data-ttu-id="ff251-123">Abonelik Kimliğiniz, hello hello kaynak grubunun adını, hello hello dağıtım adını ve bağlantı tooyour şablonu sağlar.</span><span class="sxs-lookup"><span data-stu-id="ff251-123">Provide your subscription ID, hello name of hello resource group, hello name of hello deployment, and a link tooyour template.</span></span> <span data-ttu-id="ff251-124">Merhaba şablon dosyası hakkında daha fazla bilgi için bkz: [parametre dosyası](#parameter-file).</span><span class="sxs-lookup"><span data-stu-id="ff251-124">For information about hello template file, see [Parameter file](#parameter-file).</span></span> <span data-ttu-id="ff251-125">Merhaba REST API toocreate bir kaynak grubu hakkında daha fazla bilgi için bkz: [şablon dağıtımı oluşturmak](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_CreateOrUpdate).</span><span class="sxs-lookup"><span data-stu-id="ff251-125">For more information about hello REST API toocreate a resource group, see [Create a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_CreateOrUpdate).</span></span> <span data-ttu-id="ff251-126">Bildirim hello **modu** çok ayarlanır**artımlı**.</span><span class="sxs-lookup"><span data-stu-id="ff251-126">Notice hello **mode** is set too**Incremental**.</span></span> <span data-ttu-id="ff251-127">toorun tam dağıtım Ayarla **modu** çok**tam**.</span><span class="sxs-lookup"><span data-stu-id="ff251-127">toorun a complete deployment, set **mode** too**Complete**.</span></span> <span data-ttu-id="ff251-128">Şablonunuzda olmayan kaynakları yanlışlıkla silebilirsiniz gibi hello tam modu kullanırken dikkatli olun.</span><span class="sxs-lookup"><span data-stu-id="ff251-128">Be careful when using hello complete mode as you can inadvertently delete resources that are not in your template.</span></span>
   
        PUT https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>/providers/Microsoft.Resources/deployments/<YourDeploymentName>?api-version=2015-01-01
          <common headers>
          {
            "properties": {
              "templateLink": {
                "uri": "http://mystorageaccount.blob.core.windows.net/templates/template.json",
                "contentVersion": "1.0.0.0"
              },
              "mode": "Incremental",
              "parametersLink": {
                "uri": "http://mystorageaccount.blob.core.windows.net/templates/parameters.json",
                "contentVersion": "1.0.0.0"
              }
            }
          }
   
      <span data-ttu-id="ff251-129">Toolog yanıt içeriğini, istek içeriği veya her ikisini istiyorsanız ekleyin **debugSetting** hello isteği.</span><span class="sxs-lookup"><span data-stu-id="ff251-129">If you want toolog response content, request content, or both, include **debugSetting** in hello request.</span></span>
   
        "debugSetting": {
          "detailLevel": "requestContent, responseContent"
        }
   
      <span data-ttu-id="ff251-130">Bir paylaşılan erişim imzası (SAS) belirteci, depolama hesabı toouse ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ff251-130">You can set up your storage account toouse a shared access signature (SAS) token.</span></span> <span data-ttu-id="ff251-131">Daha fazla bilgi için bkz: [paylaşılan erişim imzası için temsilci seçme erişimle](https://docs.microsoft.com/rest/api/storageservices/delegating-access-with-a-shared-access-signature).</span><span class="sxs-lookup"><span data-stu-id="ff251-131">For more information, see [Delegating Access with a Shared Access Signature](https://docs.microsoft.com/rest/api/storageservices/delegating-access-with-a-shared-access-signature).</span></span>
5. <span data-ttu-id="ff251-132">Merhaba şablon dağıtımı Hello durumunu alın.</span><span class="sxs-lookup"><span data-stu-id="ff251-132">Get hello status of hello template deployment.</span></span> <span data-ttu-id="ff251-133">Daha fazla bilgi için bkz: [şablon dağıtımı hakkında bilgi alma](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get).</span><span class="sxs-lookup"><span data-stu-id="ff251-133">For more information, see [Get information about a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get).</span></span>
   
          GET https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>/providers/Microsoft.Resources/deployments/<YourDeploymentName>?api-version=2015-01-01
           <common headers>

## <a name="parameter-file"></a><span data-ttu-id="ff251-134">Parametre dosyası</span><span class="sxs-lookup"><span data-stu-id="ff251-134">Parameter file</span></span>

[!INCLUDE [resource-manager-parameter-file](../../includes/resource-manager-parameter-file.md)]

## <a name="next-steps"></a><span data-ttu-id="ff251-135">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ff251-135">Next steps</span></span>
* <span data-ttu-id="ff251-136">zaman uyumsuz REST işlemlerini işleme hakkında toolearn bkz [izlemek zaman uyumsuz Azure işlemleri](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="ff251-136">toolearn about handling asynchronous REST operations, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
* <span data-ttu-id="ff251-137">Kaynaklara hello .NET istemci kitaplığı aracılığıyla dağıtmaya ilişkin bir örnek için bkz: [.NET kitaplıkları ve bir şablon kullanarak kaynakları dağıtmak](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ff251-137">For an example of deploying resources through hello .NET client library, see [Deploy resources using .NET libraries and a template](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="ff251-138">Şablon toodefine parametrelerinde bkz [şablonları yazma](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="ff251-138">toodefine parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="ff251-139">Çözüm toodifferent ortamlarınızın dağıtma ile ilgili yönergeler için bkz: [Microsoft Azure geliştirme ve test ortamlarında](solution-dev-test-environments.md).</span><span class="sxs-lookup"><span data-stu-id="ff251-139">For guidance on deploying your solution toodifferent environments, see [Development and test environments in Microsoft Azure](solution-dev-test-environments.md).</span></span>
* <span data-ttu-id="ff251-140">Kuruluşların Resource Manager tooeffectively nasıl kullanabileceğiniz hakkında rehberlik için abonelikleri yönetmek için bkz: [Azure enterprise iskele - Düzenleyici abonelik idare](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="ff251-140">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

