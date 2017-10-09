---
title: "aaaUnderstand Azure dağıtım hataları | Microsoft Docs"
description: "Açıklar nasıl toolearn Azure dağıtım hataları hakkında."
services: azure-resource-manager
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
keywords: "Dağıtım hatası, azure dağıtım tooazure dağıtma"
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/12/2017
ms.author: tomfitz
ms.openlocfilehash: a335e121e9b908a763374907e34b1f6e823d6e96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-azure-deployment-errors"></a><span data-ttu-id="34e0a-104">Azure dağıtım hataları anlama</span><span class="sxs-lookup"><span data-stu-id="34e0a-104">Understand Azure deployment errors</span></span>
<span data-ttu-id="34e0a-105">Bu konu, dağıtım hatalarını ve hata hakkında daha fazla bilgi nasıl bulabilir açıklar.</span><span class="sxs-lookup"><span data-stu-id="34e0a-105">This topic describes deployment errors and how you can discover more information about an error.</span></span> <span data-ttu-id="34e0a-106">Çözümleri toocommon dağıtım hataları için bkz: [ortak Azure dağıtım hataları Azure Resource Manager ile ilgili sorunları giderme](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="34e0a-106">For resolutions toocommon deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>

## <a name="two-types-of-errors"></a><span data-ttu-id="34e0a-107">İki tür hataları</span><span class="sxs-lookup"><span data-stu-id="34e0a-107">Two types of errors</span></span>
<span data-ttu-id="34e0a-108">İki tür alabileceğiniz hataları vardır:</span><span class="sxs-lookup"><span data-stu-id="34e0a-108">There are two types of errors you can receive:</span></span>

* <span data-ttu-id="34e0a-109">Doğrulama hataları</span><span class="sxs-lookup"><span data-stu-id="34e0a-109">validation errors</span></span>
* <span data-ttu-id="34e0a-110">Dağıtım hataları</span><span class="sxs-lookup"><span data-stu-id="34e0a-110">deployment errors</span></span>

<span data-ttu-id="34e0a-111">Görüntü aşağıdaki hello hello etkinlik günlüğü bir abonelik için gösterir.</span><span class="sxs-lookup"><span data-stu-id="34e0a-111">hello following image shows hello activity log for a subscription.</span></span> <span data-ttu-id="34e0a-112">Bu iki dağıtım temsil eder.</span><span class="sxs-lookup"><span data-stu-id="34e0a-112">It represents two deployments.</span></span> <span data-ttu-id="34e0a-113">Bir dağıtımda hello şablon, doğrulama başarısız oldu (**doğrulama**) ve devam.</span><span class="sxs-lookup"><span data-stu-id="34e0a-113">In one deployment, hello template failed validation (**Validate**) and did not proceed.</span></span> <span data-ttu-id="34e0a-114">İçindeki diğer dağıtım Merhaba, hello şablon doğrulamayı geçen ancak hello kaynakları oluşturma başarısız oldu (**yazma dağıtımları**).</span><span class="sxs-lookup"><span data-stu-id="34e0a-114">In hello other deployment, hello template passed validation but failed when creating hello resources (**Write Deployments**).</span></span> 

![Hata Kodu Göster](./media/resource-manager-troubleshoot-tips/show-activity-log.png)

<span data-ttu-id="34e0a-116">Dağıtım öncesinde belirlenebilir senaryolardan doğrulama hataları ortaya çıkar.</span><span class="sxs-lookup"><span data-stu-id="34e0a-116">Validation errors arise from scenarios that can be determined before deployment.</span></span> <span data-ttu-id="34e0a-117">Sözdizimi hataları, şablonu veya abonelik kotalarında aşacak çalışırken toodeploy kaynakları içerirler.</span><span class="sxs-lookup"><span data-stu-id="34e0a-117">They include syntax errors in your template, or trying toodeploy resources that would exceed your subscription quotas.</span></span> <span data-ttu-id="34e0a-118">Dağıtım hataları hello dağıtım işlemi sırasında ortaya koşullar ortaya çıkabilecek.</span><span class="sxs-lookup"><span data-stu-id="34e0a-118">Deployment errors arise from conditions that occur during hello deployment process.</span></span> <span data-ttu-id="34e0a-119">Paralel olarak dağıtılan bir kaynak tooaccess çalışırken içerirler.</span><span class="sxs-lookup"><span data-stu-id="34e0a-119">They include trying tooaccess a resource that is being deployed in parallel.</span></span>

<span data-ttu-id="34e0a-120">Hataları return tootroubleshoot hello dağıtım kullandığınız bir hata kodu her iki tür.</span><span class="sxs-lookup"><span data-stu-id="34e0a-120">Both types of errors return an error code that you use tootroubleshoot hello deployment.</span></span> <span data-ttu-id="34e0a-121">Her iki tür hataları hello görünür [etkinlik günlüğü](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="34e0a-121">Both types of errors appear in hello [activity log](resource-group-audit.md).</span></span> <span data-ttu-id="34e0a-122">Ancak, doğrulama hataları Hello dağıtım hiçbir zaman başlamadı çünkü dağıtım geçmişiniz görünmez.</span><span class="sxs-lookup"><span data-stu-id="34e0a-122">However, validation errors do not appear in your deployment history because hello deployment never started.</span></span>

## <a name="determine-error-code"></a><span data-ttu-id="34e0a-123">Hata kodu belirleme</span><span class="sxs-lookup"><span data-stu-id="34e0a-123">Determine error code</span></span>

<span data-ttu-id="34e0a-124">Merhaba hata iletisi ve hello hata kodu bakarak bir hata hakkında bilgi edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34e0a-124">You can learn about an error by looking at hello error message and hello error code.</span></span> <span data-ttu-id="34e0a-125">Merhaba [ortak Azure dağıtım hataları Azure Resource Manager ile ilgili sorunları giderme](resource-manager-common-deployment-errors.md) makalede hata koduna göre çözümler listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="34e0a-125">hello [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md) article lists resolutions by error code.</span></span> <span data-ttu-id="34e0a-126">Bu konu, nasıl toouse hello Azure portal toodiscover hello hata kodu gösterir.</span><span class="sxs-lookup"><span data-stu-id="34e0a-126">This topic shows how toouse hello Azure portal toodiscover hello error code.</span></span>

### <a name="validation-errors"></a><span data-ttu-id="34e0a-127">Doğrulama hataları</span><span class="sxs-lookup"><span data-stu-id="34e0a-127">Validation errors</span></span>

<span data-ttu-id="34e0a-128">Merhaba Portalı aracılığıyla dağıtırken değerlerinizi gönderdikten sonra bir doğrulama hatası bakın.</span><span class="sxs-lookup"><span data-stu-id="34e0a-128">When deploying through hello portal, you see a validation error after submitting your values.</span></span>

![Portal doğrulama hatasını göster](./media/resource-manager-troubleshoot-tips/validation-error.png)

<span data-ttu-id="34e0a-130">Daha fazla ayrıntı için selamlama iletisine seçin.</span><span class="sxs-lookup"><span data-stu-id="34e0a-130">Select hello message for more details.</span></span> <span data-ttu-id="34e0a-131">Görüntü aşağıdaki hello gördüğünüz bir **InvalidTemplateDeployment** hata ve bir ilke belirten bir ileti dağıtım engellendi.</span><span class="sxs-lookup"><span data-stu-id="34e0a-131">In hello following image, you see an **InvalidTemplateDeployment** error and a message that indicates a policy blocked deployment.</span></span>

![Doğrulama ayrıntıları göster](./media/resource-manager-troubleshoot-tips/validation-details.png)

### <a name="deployment-errors"></a><span data-ttu-id="34e0a-133">Dağıtım hataları</span><span class="sxs-lookup"><span data-stu-id="34e0a-133">Deployment errors</span></span>

<span data-ttu-id="34e0a-134">Merhaba işlemi doğrulama başarılı olur, ancak dağıtım sırasında başarısız olduğunda hello Bildirimlerde hello hatasına bakın.</span><span class="sxs-lookup"><span data-stu-id="34e0a-134">When hello operation passes validation, but fails during deployment, you see hello error in hello notifications.</span></span> <span data-ttu-id="34e0a-135">Merhaba bildirim seçin.</span><span class="sxs-lookup"><span data-stu-id="34e0a-135">Select hello notification.</span></span>

![bildirim hatası](./media/resource-manager-troubleshoot-tips/notification.png)

<span data-ttu-id="34e0a-137">Merhaba dağıtımı hakkında daha fazla ayrıntı bakın.</span><span class="sxs-lookup"><span data-stu-id="34e0a-137">You see more details about hello deployment.</span></span> <span data-ttu-id="34e0a-138">Merhaba seçeneği toofind hello hata hakkında daha fazla bilgi seçin.</span><span class="sxs-lookup"><span data-stu-id="34e0a-138">Select hello option toofind more information about hello error.</span></span>

![dağıtım başarısız oldu](./media/resource-manager-troubleshoot-tips/deployment-failed.png)

<span data-ttu-id="34e0a-140">Merhaba hata iletisi ve hata kodları bakın.</span><span class="sxs-lookup"><span data-stu-id="34e0a-140">You see hello error message and error codes.</span></span> <span data-ttu-id="34e0a-141">İki hata kodları dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="34e0a-141">Notice there are two error codes.</span></span> <span data-ttu-id="34e0a-142">Merhaba ilk hata kodu (**DeploymentFailed**) hello ayrıntılarını sağlamaz genel bir hata toosolve hello hata gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="34e0a-142">hello first error code (**DeploymentFailed**) is a general error that does not provide hello details you need toosolve hello error.</span></span> <span data-ttu-id="34e0a-143">Merhaba ikinci hata kodunu (**StorageAccountNotFound**) ihtiyacınız hello ayrıntıları sağlar.</span><span class="sxs-lookup"><span data-stu-id="34e0a-143">hello second error code (**StorageAccountNotFound**) provides hello details you need.</span></span> 

![Hata ayrıntıları](./media/resource-manager-troubleshoot-tips/error-details.png)

## <a name="enable-debug-logging"></a><span data-ttu-id="34e0a-145">Hata ayıklama günlük kaydını etkinleştir</span><span class="sxs-lookup"><span data-stu-id="34e0a-145">Enable debug logging</span></span>
<span data-ttu-id="34e0a-146">Bazen, nelerin yanlış gittiğini hello istek ve yanıt toodiscover hakkında daha fazla bilgi gerekir.</span><span class="sxs-lookup"><span data-stu-id="34e0a-146">Sometimes you need more information about hello request and response toodiscover what went wrong.</span></span> <span data-ttu-id="34e0a-147">PowerShell veya Azure CLI kullanarak bir dağıtım sırasında günlüğe ek bilgiler isteyebilir.</span><span class="sxs-lookup"><span data-stu-id="34e0a-147">By using PowerShell or Azure CLI, you can request that additional information is logged during a deployment.</span></span>

- <span data-ttu-id="34e0a-148">PowerShell</span><span class="sxs-lookup"><span data-stu-id="34e0a-148">PowerShell</span></span>

   <span data-ttu-id="34e0a-149">PowerShell'de hello ayarlamak **DeploymentDebugLogLevel** parametresi tooAll, ResponseContent veya RequestContent.</span><span class="sxs-lookup"><span data-stu-id="34e0a-149">In PowerShell, set hello **DeploymentDebugLogLevel** parameter tooAll, ResponseContent, or RequestContent.</span></span>

  ```powershell
  New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile c:\Azure\Templates\storage.json -DeploymentDebugLogLevel All
  ```

   <span data-ttu-id="34e0a-150">Merhaba istek içeriği ile Merhaba cmdlet'i aşağıdaki inceleyin:</span><span class="sxs-lookup"><span data-stu-id="34e0a-150">Examine hello request content with hello following cmdlet:</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName storageonly -ResourceGroupName startgroup).Properties.request | ConvertTo-Json
  ```

   <span data-ttu-id="34e0a-151">Veya, ile içerik yanıt hello:</span><span class="sxs-lookup"><span data-stu-id="34e0a-151">Or, hello response content with:</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName storageonly -ResourceGroupName startgroup).Properties.response | ConvertTo-Json
  ```

   <span data-ttu-id="34e0a-152">Bu bilgiler hello şablonunda bir değer yanlış ayarlanmış olup olmadığını belirlemenize yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="34e0a-152">This information can help you determine whether a value in hello template is being incorrectly set.</span></span>

- <span data-ttu-id="34e0a-153">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="34e0a-153">Azure CLI</span></span>

   <span data-ttu-id="34e0a-154">Merhaba dağıtım işlemleri ile Merhaba komutu aşağıdaki inceleyin:</span><span class="sxs-lookup"><span data-stu-id="34e0a-154">Examine hello deployment operations with hello following command:</span></span>

  ```azurecli
  az group deployment operation list --resource-group ExampleGroup --name vmlinux
  ```

- <span data-ttu-id="34e0a-155">İç içe geçmiş şablonu</span><span class="sxs-lookup"><span data-stu-id="34e0a-155">Nested template</span></span>

   <span data-ttu-id="34e0a-156">Kullanım hello iç içe geçmiş bir şablon toolog hata ayıklama bilgileri **debugSetting** öğesi.</span><span class="sxs-lookup"><span data-stu-id="34e0a-156">toolog debug information for a nested template, use hello **debugSetting** element.</span></span>

  ```json
  {
      "apiVersion": "2016-09-01",
      "name": "nestedTemplate",
      "type": "Microsoft.Resources/deployments",
      "properties": {
          "mode": "Incremental",
          "templateLink": {
              "uri": "{template-uri}",
              "contentVersion": "1.0.0.0"
          },
          "debugSetting": {
             "detailLevel": "requestContent, responseContent"
          }
      }
  }
  ```


## <a name="create-a-troubleshooting-template"></a><span data-ttu-id="34e0a-157">Sorun giderme şablonu oluşturma</span><span class="sxs-lookup"><span data-stu-id="34e0a-157">Create a troubleshooting template</span></span>
<span data-ttu-id="34e0a-158">Bazı durumlarda, en kolay yolu tootroubleshoot hello tootest bölümlerini, şablonudur.</span><span class="sxs-lookup"><span data-stu-id="34e0a-158">In some cases, hello easiest way tootroubleshoot your template is tootest parts of it.</span></span> <span data-ttu-id="34e0a-159">Merhaba hataya neden olduğunu düşündüğünüz hello Bölümü'toofocus sağlayan basitleştirilmiş bir şablon oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34e0a-159">You can create a simplified template that enables you toofocus on hello part that you believe is causing hello error.</span></span> <span data-ttu-id="34e0a-160">Örneğin, bir kaynak başvururken bir hata alıyorsunuz varsayalım.</span><span class="sxs-lookup"><span data-stu-id="34e0a-160">For example, suppose you are receiving an error when referencing a resource.</span></span> <span data-ttu-id="34e0a-161">Tüm şablon postalarla yerine, soruna hello parçası döndürür bir şablon oluşturun.</span><span class="sxs-lookup"><span data-stu-id="34e0a-161">Rather than dealing with an entire template, create a template that returns hello part that may be causing your problem.</span></span> <span data-ttu-id="34e0a-162">Şablon işlevleri doğru kullanarak hello sağ parametrelerinde geçtiğiniz ve beklediğiniz hello kaynak alınıyor belirlemenize yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="34e0a-162">It can help you determine whether you are passing in hello right parameters, using template functions correctly, and getting hello resource you expect.</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageName": {
        "type": "string"
    },
    "storageResourceGroup": {
        "type": "string"
    }
  },
  "variables": {},
  "resources": [],
  "outputs": {
    "exampleOutput": {
        "value": "[reference(resourceId(parameters('storageResourceGroup'), 'Microsoft.Storage/storageAccounts', parameters('storageName')), '2016-05-01')]",
        "type" : "object"
    }
  }
}
```

<span data-ttu-id="34e0a-163">Ya da tooincorrectly bağımlılıkları ayarlama ile ilgili olduğunu düşündüğünüz dağıtım hataları karşılaşıyoruz varsayalım.</span><span class="sxs-lookup"><span data-stu-id="34e0a-163">Or, suppose you are encountering deployment errors that you believe are related tooincorrectly set dependencies.</span></span> <span data-ttu-id="34e0a-164">Basitleştirilmiş şablonlara bölerek şablonunuzu test edin.</span><span class="sxs-lookup"><span data-stu-id="34e0a-164">Test your template by breaking it into simplified templates.</span></span> <span data-ttu-id="34e0a-165">İlk olarak, yalnızca tek bir kaynak (bir SQL sunucu gibi) dağıtan bir şablon oluşturun.</span><span class="sxs-lookup"><span data-stu-id="34e0a-165">First, create a template that deploys only a single resource (like a SQL Server).</span></span> <span data-ttu-id="34e0a-166">Bu kaynağı doğru tanımlı sahip olduğunuzdan emin olduğunuzda (SQL veritabanı gibi) bağımlı bir kaynak ekleyin.</span><span class="sxs-lookup"><span data-stu-id="34e0a-166">When you are sure you have that resource correctly defined, add a resource that depends on it (like a SQL Database).</span></span> <span data-ttu-id="34e0a-167">Doğru tanımlanmadı iki kaynaklarla varsa, bağımlı diğer kaynaklar (örneğin, denetim ilkeleri) ekleyin.</span><span class="sxs-lookup"><span data-stu-id="34e0a-167">When you have those two resources correctly defined, add other dependent resources (like auditing policies).</span></span> <span data-ttu-id="34e0a-168">Her sınama dağıtımı Between hello kaynak grubu toomake emin, yeterli sınama hello bağımlılıkları silin.</span><span class="sxs-lookup"><span data-stu-id="34e0a-168">In between each test deployment, delete hello resource group toomake sure you adequately testing hello dependencies.</span></span> 

## <a name="check-deployment-sequence"></a><span data-ttu-id="34e0a-169">Onay dağıtım sırası</span><span class="sxs-lookup"><span data-stu-id="34e0a-169">Check deployment sequence</span></span>

<span data-ttu-id="34e0a-170">Kaynakları içinde beklenmeyen bir sıra dağıtılan birçok dağıtım hata meydana gelir.</span><span class="sxs-lookup"><span data-stu-id="34e0a-170">Many deployment errors happen when resources are deployed in an unexpected sequence.</span></span> <span data-ttu-id="34e0a-171">Bağımlılıklar doğru ayarlanmadı, bu hatalar ortaya çıkar.</span><span class="sxs-lookup"><span data-stu-id="34e0a-171">These errors arise when dependencies are not correctly set.</span></span> <span data-ttu-id="34e0a-172">Gerekli bir bağımlılığı eksik olduğunda, bir kaynak için başka bir kaynak ancak hello başka bir değer henüz yok toouse çalışır.</span><span class="sxs-lookup"><span data-stu-id="34e0a-172">When you are missing a needed dependency, one resource attempts toouse a value for another resource but hello other does not yet exist.</span></span> <span data-ttu-id="34e0a-173">Bir kaynağın bulunamadığını bildiren bir hata alırsınız.</span><span class="sxs-lookup"><span data-stu-id="34e0a-173">You get an error stating that a resource is not found.</span></span> <span data-ttu-id="34e0a-174">Bu tür hatalara zaman zaman karşılaşabilirsiniz hello dağıtım süresini her kaynak için değişebileceğinden.</span><span class="sxs-lookup"><span data-stu-id="34e0a-174">You may encounter this type of error intermittently because hello deployment time for each resource can vary.</span></span> <span data-ttu-id="34e0a-175">Örneğin, ilk denemesi toodeploy kaynaklarınızı başarılı gerekli bir kaynağa zamanında rastgele tamamladığı için.</span><span class="sxs-lookup"><span data-stu-id="34e0a-175">For example, your first attempt toodeploy your resources succeeds because a required resource randomly completes in time.</span></span> <span data-ttu-id="34e0a-176">Ancak, kaynak süre içinde tamamlanmadı Hello gerekli olduğundan girişiminiz başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="34e0a-176">However, your second attempt fails because hello required resource did not complete in time.</span></span> 

<span data-ttu-id="34e0a-177">Ancak, gerekli olmayan tooavoid ayarı bağımlılıkları istiyor.</span><span class="sxs-lookup"><span data-stu-id="34e0a-177">But, you want tooavoid setting dependencies that are not needed.</span></span> <span data-ttu-id="34e0a-178">Gereksiz bağımlılıkları varsa, paralel olarak dağıtılan birbirlerine bağımlı olmayan kaynakları engelleyerek hello hello dağıtım süresini uzatmak.</span><span class="sxs-lookup"><span data-stu-id="34e0a-178">When you have unnecessary dependencies, you prolong hello duration of hello deployment by preventing resources that are not dependent on each other from being deployed in parallel.</span></span> <span data-ttu-id="34e0a-179">Ayrıca, hello dağıtım engelleme döngüsel bağımlılıklar oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="34e0a-179">In addition, you may create circular dependencies that block hello deployment.</span></span> <span data-ttu-id="34e0a-180">Merhaba [başvuru](resource-group-template-functions-resource.md#reference) işlevi bu kaynak hello dağıtıldığında bu dolaylı bir bağımlılığı hello başvurulan kaynakta oluşturur aynı şablonu.</span><span class="sxs-lookup"><span data-stu-id="34e0a-180">hello [reference](resource-group-template-functions-resource.md#reference) function creates an implicit dependency on hello referenced resource, when that resource is deployed in hello same template.</span></span> <span data-ttu-id="34e0a-181">Bu nedenle, hello belirtilen hello bağımlılıkları'den daha fazla bağımlılıkları olabilir **dependsOn** özelliği.</span><span class="sxs-lookup"><span data-stu-id="34e0a-181">Therefore, you may have more dependencies than hello dependencies specified in hello **dependsOn** property.</span></span> <span data-ttu-id="34e0a-182">Merhaba [ResourceId](resource-group-template-functions-resource.md#resourceid) işlevi oluşturmaz dolaylı bir bağımlılığı veya hello kaynak var olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="34e0a-182">hello [resourceId](resource-group-template-functions-resource.md#resourceid) function does not create an implicit dependency or validate that hello resource exists.</span></span>

<span data-ttu-id="34e0a-183">Bağımlılık sorunlarını karşılaştığınızda, kaynak dağıtım hello sırasını toogain fikirler gerekir.</span><span class="sxs-lookup"><span data-stu-id="34e0a-183">When you encounter dependency problems, you need toogain insight into hello order of resource deployment.</span></span> <span data-ttu-id="34e0a-184">Merhaba sırasını dağıtım işlemlerini tooview:</span><span class="sxs-lookup"><span data-stu-id="34e0a-184">tooview hello order of deployment operations:</span></span>

1. <span data-ttu-id="34e0a-185">Merhaba dağıtım geçmişi kaynak grubunuz için seçin.</span><span class="sxs-lookup"><span data-stu-id="34e0a-185">Select hello deployment history for your resource group.</span></span>

   ![Dağıtım geçmişi seçin](./media/resource-manager-troubleshoot-tips/select-deployment.png)

2. <span data-ttu-id="34e0a-187">Bir dağıtım hello geçmişinden ve seçin **olayları**.</span><span class="sxs-lookup"><span data-stu-id="34e0a-187">Select a deployment from hello history, and select **Events**.</span></span>

   ![Dağıtım olaylarını seçin](./media/resource-manager-troubleshoot-tips/select-deployment-events.png)

3. <span data-ttu-id="34e0a-189">Her kaynak için olayların Hello sırası inceleyin.</span><span class="sxs-lookup"><span data-stu-id="34e0a-189">Examine hello sequence of events for each resource.</span></span> <span data-ttu-id="34e0a-190">Dikkat toohello her işlemin durumunu ücret ödersiniz.</span><span class="sxs-lookup"><span data-stu-id="34e0a-190">Pay attention toohello status of each operation.</span></span> <span data-ttu-id="34e0a-191">Örneğin, hello aşağıdaki görüntüde dağıtılan üç depolama hesaplarını paralel olarak gösterir.</span><span class="sxs-lookup"><span data-stu-id="34e0a-191">For example, hello following image shows three storage accounts that deployed in parallel.</span></span> <span data-ttu-id="34e0a-192">Üç depolama hesapları hello bildirimi sırasında hello başlatıldı aynı anda.</span><span class="sxs-lookup"><span data-stu-id="34e0a-192">Notice that hello three storage accounts are started at hello same time.</span></span>

   ![Paralel dağıtım](./media/resource-manager-troubleshoot-tips/deployment-events-parallel.png)

   <span data-ttu-id="34e0a-194">Merhaba sonraki resim paralel olarak değil dağıtılan üç depolama hesaplarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="34e0a-194">hello next image shows three storage accounts that are not deployed in parallel.</span></span> <span data-ttu-id="34e0a-195">Hello ikinci depolama hesabı hello ilk depolama hesabında bağlıdır ve hello üçüncü depolama hesabı hello ikinci depolama hesabına bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="34e0a-195">hello second storage account depends on hello first storage account, and hello third storage account depends on hello second storage account.</span></span> <span data-ttu-id="34e0a-196">Bu nedenle, hello ilk depolama hesabı başlatıldı, kabul ve hello bir sonraki başlatılışında önce tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="34e0a-196">Therefore, hello first storage account is started, accepted, and completed before hello next is started.</span></span>

   ![sıralı dağıtım](./media/resource-manager-troubleshoot-tips/deployment-events-sequence.png)

<span data-ttu-id="34e0a-198">Hatta daha karmaşık senaryolar için kullandığınız dağıtım başlatıldığında ve her kaynak için tamamlanan aynı teknik toodiscover hello.</span><span class="sxs-lookup"><span data-stu-id="34e0a-198">Even for more complicated scenarios, you can use hello same technique toodiscover when deployment is started and completed for each resource.</span></span> <span data-ttu-id="34e0a-199">Merhaba sırası, beklediğinizden farklı ise, dağıtım olayları toosee arayın.</span><span class="sxs-lookup"><span data-stu-id="34e0a-199">Look through your deployment events toosee if hello sequence is different than you would expect.</span></span> <span data-ttu-id="34e0a-200">Öyleyse, bu kaynak için hello bağımlılıkları yeniden.</span><span class="sxs-lookup"><span data-stu-id="34e0a-200">If so, reevaluate hello dependencies for this resource.</span></span>

<span data-ttu-id="34e0a-201">Resource Manager şablonu doğrulama sırasında döngüsel bağımlılıklar tanımlar.</span><span class="sxs-lookup"><span data-stu-id="34e0a-201">Resource Manager identifies circular dependencies during template validation.</span></span> <span data-ttu-id="34e0a-202">Döngüsel bağımlılık özellikle bildiren bir hata iletisi yok değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="34e0a-202">It returns an error message that specifically states a circular dependency exists.</span></span> <span data-ttu-id="34e0a-203">toosolve döngüsel bağımlılık:</span><span class="sxs-lookup"><span data-stu-id="34e0a-203">toosolve a circular dependency:</span></span>

1. <span data-ttu-id="34e0a-204">Şablonunuzda, hello döngüsel bağımlılık olarak tanımlanan hello kaynak bulunamıyor.</span><span class="sxs-lookup"><span data-stu-id="34e0a-204">In your template, find hello resource identified in hello circular dependency.</span></span> 
2. <span data-ttu-id="34e0a-205">Bu kaynak için hello inceleyin **dependsOn** özellik ve tüm kullanımlarını hello **başvuru** hangi kaynaklara bağımlı toosee işlev.</span><span class="sxs-lookup"><span data-stu-id="34e0a-205">For that resource, examine hello **dependsOn** property and any uses of hello **reference** function toosee which resources it depends on.</span></span> 
3. <span data-ttu-id="34e0a-206">Hangi kaynaklara bağlı oldukları bu kaynakları toosee inceleyin.</span><span class="sxs-lookup"><span data-stu-id="34e0a-206">Examine those resources toosee which resources they depend on.</span></span> <span data-ttu-id="34e0a-207">Merhaba özgün kaynaklara bağımlı bir kaynak fark kadar hello bağımlılıkları izleyin.</span><span class="sxs-lookup"><span data-stu-id="34e0a-207">Follow hello dependencies until you notice a resource that depends on hello original resource.</span></span>
5. <span data-ttu-id="34e0a-208">Merhaba döngüsel bağımlılık olarak söz konusu Hello kaynaklar için hello tüm kullanımını dikkatlice inceleyin **dependsOn** özelliği tooidentify gerekli olmayan tüm bağımlılıkları.</span><span class="sxs-lookup"><span data-stu-id="34e0a-208">For hello resources involved in hello circular dependency, carefully examine all uses of hello **dependsOn** property tooidentify any dependencies that are not needed.</span></span> <span data-ttu-id="34e0a-209">Bu bağımlılıkları kaldırın.</span><span class="sxs-lookup"><span data-stu-id="34e0a-209">Remove those dependencies.</span></span> <span data-ttu-id="34e0a-210">Bir bağımlılık gerekli olmadığından emin değilseniz, bu kaldırmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="34e0a-210">If you are unsure that a dependency is needed, try removing it.</span></span> 
6. <span data-ttu-id="34e0a-211">Merhaba şablonunu yeniden dağıtın.</span><span class="sxs-lookup"><span data-stu-id="34e0a-211">Redeploy hello template.</span></span>

<span data-ttu-id="34e0a-212">Merhaba değerleri kaldırılıyor **dependsOn** hello şablonu dağıttığınızda, özellik hataları neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="34e0a-212">Removing values from hello **dependsOn** property can cause errors when you deploy hello template.</span></span> <span data-ttu-id="34e0a-213">Bir hatayla karşılaşırsanız hello bağımlılık hello şablon uygulamasına geri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="34e0a-213">If you encounter an error, add hello dependency back into hello template.</span></span> 

<span data-ttu-id="34e0a-214">Bu yaklaşımı hello döngüsel bağımlılık çözmezse alt kaynakları (örneğin, uzantıları veya yapılandırma ayarları), dağıtım mantığının parçası taşınmasını göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="34e0a-214">If that approach does not solve hello circular dependency, consider moving part of your deployment logic into child resources (such as extensions or configuration settings).</span></span> <span data-ttu-id="34e0a-215">Bu alt kaynakları toodeploy hello kaynakları hello döngüsel bağımlılık olarak söz konusu sonra yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="34e0a-215">Configure those child resources toodeploy after hello resources involved in hello circular dependency.</span></span> <span data-ttu-id="34e0a-216">Örneğin, iki sanal makine dağıtıyorsanız ancak toohello diğer başvuran her birinin özelliklerini ayarlamalısınız varsayalım.</span><span class="sxs-lookup"><span data-stu-id="34e0a-216">For example, suppose you are deploying two virtual machines but you must set properties on each one that refer toohello other.</span></span> <span data-ttu-id="34e0a-217">Bunları sırasının hello dağıtabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="34e0a-217">You can deploy them in hello following order:</span></span>

1. <span data-ttu-id="34e0a-218">VM1</span><span class="sxs-lookup"><span data-stu-id="34e0a-218">vm1</span></span>
2. <span data-ttu-id="34e0a-219">vm2</span><span class="sxs-lookup"><span data-stu-id="34e0a-219">vm2</span></span>
3. <span data-ttu-id="34e0a-220">Vm1 uzantısı vm1 ve vm2 bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="34e0a-220">Extension on vm1 depends on vm1 and vm2.</span></span> <span data-ttu-id="34e0a-221">Merhaba uzantısı vm2 alır vm1 değerlerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="34e0a-221">hello extension sets values on vm1 that it gets from vm2.</span></span>
4. <span data-ttu-id="34e0a-222">Vm2 uzantısı vm1 ve vm2 bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="34e0a-222">Extension on vm2 depends on vm1 and vm2.</span></span> <span data-ttu-id="34e0a-223">Merhaba uzantısı vm1 alır vm2 değerlerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="34e0a-223">hello extension sets values on vm2 that it gets from vm1.</span></span>

<span data-ttu-id="34e0a-224">Merhaba aynı yaklaşımı uygulama hizmeti uygulamalar için çalışır.</span><span class="sxs-lookup"><span data-stu-id="34e0a-224">hello same approach works for App Service apps.</span></span> <span data-ttu-id="34e0a-225">Yapılandırma değerlerini hello uygulama kaynak bir alt kaynağı taşımayı düşünün.</span><span class="sxs-lookup"><span data-stu-id="34e0a-225">Consider moving configuration values into a child resource of hello app resource.</span></span> <span data-ttu-id="34e0a-226">Sırasının hello iki web uygulamaları dağıtabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="34e0a-226">You can deploy two web apps in hello following order:</span></span>

1. <span data-ttu-id="34e0a-227">webapp1</span><span class="sxs-lookup"><span data-stu-id="34e0a-227">webapp1</span></span>
2. <span data-ttu-id="34e0a-228">webapp2</span><span class="sxs-lookup"><span data-stu-id="34e0a-228">webapp2</span></span>
3. <span data-ttu-id="34e0a-229">config webapp1 için webapp1 ve webapp2 bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="34e0a-229">config for webapp1 depends on webapp1 and webapp2.</span></span> <span data-ttu-id="34e0a-230">Uygulama ayarları webapp2 değerlerle içerir.</span><span class="sxs-lookup"><span data-stu-id="34e0a-230">It contains app settings with values from webapp2.</span></span>
4. <span data-ttu-id="34e0a-231">config webapp2 için webapp1 ve webapp2 bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="34e0a-231">config for webapp2 depends on webapp1 and webapp2.</span></span> <span data-ttu-id="34e0a-232">Uygulama ayarları webapp1 değerlerle içerir.</span><span class="sxs-lookup"><span data-stu-id="34e0a-232">It contains app settings with values from webapp1.</span></span>


## <a name="next-steps"></a><span data-ttu-id="34e0a-233">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="34e0a-233">Next steps</span></span>
* <span data-ttu-id="34e0a-234">Çözümleri toocommon dağıtım hataları için bkz: [ortak Azure dağıtım hataları Azure Resource Manager ile ilgili sorunları giderme](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="34e0a-234">For resolutions toocommon deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="34e0a-235">Eylemler, Denetim hakkında toolearn bkz [denetim işlemleri Resource Manager ile](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="34e0a-235">toolearn about auditing actions, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="34e0a-236">dağıtım sırasında Eylemler toodetermine hello hatalarla ilgili toolearn bkz [görüntülemek dağıtım işlemlerini](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="34e0a-236">toolearn about actions toodetermine hello errors during deployment, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
