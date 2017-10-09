---
title: "aaaTroubleshoot ortak Azure dağıtım hataları | Microsoft Docs"
description: "Açıklar nasıl kaynakları tooAzure Azure Kaynak Yöneticisi'ni kullanarak dağıttığınızda tooresolve sık karşılaşılan hatalar."
services: azure-resource-manager
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
keywords: "Dağıtım hatası, azure dağıtım tooazure dağıtma"
ms.assetid: c002a9be-4de5-4963-bd14-b54aa3d8fa59
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: tomfitz
ms.openlocfilehash: 8571e9941879eb5586e4258a785b6a09247da771
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-common-azure-deployment-errors-with-azure-resource-manager"></a><span data-ttu-id="90b25-104">Ortak Azure dağıtım hataları Azure Resource Manager ile ilgili sorunları giderme</span><span class="sxs-lookup"><span data-stu-id="90b25-104">Troubleshoot common Azure deployment errors with Azure Resource Manager</span></span>
<span data-ttu-id="90b25-105">Bu konu, bazı ortak nasıl çözebilirsiniz açıklar karşılaşabileceğiniz Azure dağıtım hataları.</span><span class="sxs-lookup"><span data-stu-id="90b25-105">This topic describes how you can resolve some common Azure deployment errors you may encounter.</span></span>

<span data-ttu-id="90b25-106">hata kodları aşağıdaki hello bu konuda açıklanan:</span><span class="sxs-lookup"><span data-stu-id="90b25-106">hello following error codes are described in this topic:</span></span>

* [<span data-ttu-id="90b25-107">AccountNameInvalid</span><span class="sxs-lookup"><span data-stu-id="90b25-107">AccountNameInvalid</span></span>](#accountnameinvalid)
* [<span data-ttu-id="90b25-108">Yetkilendirme başarısız oldu</span><span class="sxs-lookup"><span data-stu-id="90b25-108">Authorization failed</span></span>](#authorization-failed)
* [<span data-ttu-id="90b25-109">BadRequest</span><span class="sxs-lookup"><span data-stu-id="90b25-109">BadRequest</span></span>](#badrequest)
* [<span data-ttu-id="90b25-110">DeploymentFailed</span><span class="sxs-lookup"><span data-stu-id="90b25-110">DeploymentFailed</span></span>](#deploymentfailed)
* [<span data-ttu-id="90b25-111">DisallowedOperation</span><span class="sxs-lookup"><span data-stu-id="90b25-111">DisallowedOperation</span></span>](#disallowedoperation)
* [<span data-ttu-id="90b25-112">InvalidContentLink</span><span class="sxs-lookup"><span data-stu-id="90b25-112">InvalidContentLink</span></span>](#invalidcontentlink)
* [<span data-ttu-id="90b25-113">InvalidTemplate</span><span class="sxs-lookup"><span data-stu-id="90b25-113">InvalidTemplate</span></span>](#invalidtemplate)
* [<span data-ttu-id="90b25-114">MissingSubscriptionRegistration</span><span class="sxs-lookup"><span data-stu-id="90b25-114">MissingSubscriptionRegistration</span></span>](#noregisteredproviderfound)
* [<span data-ttu-id="90b25-115">NotFound</span><span class="sxs-lookup"><span data-stu-id="90b25-115">NotFound</span></span>](#notfound)
* [<span data-ttu-id="90b25-116">NoRegisteredProviderFound</span><span class="sxs-lookup"><span data-stu-id="90b25-116">NoRegisteredProviderFound</span></span>](#noregisteredproviderfound)
* [<span data-ttu-id="90b25-117">OperationNotAllowed</span><span class="sxs-lookup"><span data-stu-id="90b25-117">OperationNotAllowed</span></span>](#quotaexceeded)
* [<span data-ttu-id="90b25-118">ParentResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="90b25-118">ParentResourceNotFound</span></span>](#parentresourcenotfound)
* [<span data-ttu-id="90b25-119">QuotaExceeded</span><span class="sxs-lookup"><span data-stu-id="90b25-119">QuotaExceeded</span></span>](#quotaexceeded)
* [<span data-ttu-id="90b25-120">RequestDisallowedByPolicy</span><span class="sxs-lookup"><span data-stu-id="90b25-120">RequestDisallowedByPolicy</span></span>](#requestdisallowedbypolicy)
* [<span data-ttu-id="90b25-121">ResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="90b25-121">ResourceNotFound</span></span>](#notfound)
* [<span data-ttu-id="90b25-122">SkuNotAvailable</span><span class="sxs-lookup"><span data-stu-id="90b25-122">SkuNotAvailable</span></span>](#skunotavailable)
* [<span data-ttu-id="90b25-123">StorageAccountAlreadyExists</span><span class="sxs-lookup"><span data-stu-id="90b25-123">StorageAccountAlreadyExists</span></span>](#storagenamenotunique)
* [<span data-ttu-id="90b25-124">StorageAccountAlreadyTaken</span><span class="sxs-lookup"><span data-stu-id="90b25-124">StorageAccountAlreadyTaken</span></span>](#storagenamenotunique)

## <a name="deploymentfailed"></a><span data-ttu-id="90b25-125">DeploymentFailed</span><span class="sxs-lookup"><span data-stu-id="90b25-125">DeploymentFailed</span></span>

<span data-ttu-id="90b25-126">Bu hata kodu genel dağıtım hatası gösterir, ancak toostart sorun giderme ihtiyacınız hello hata kodu değil.</span><span class="sxs-lookup"><span data-stu-id="90b25-126">This error code indicates a general deployment error, but it is not hello error code you need toostart troubleshooting.</span></span> <span data-ttu-id="90b25-127">gerçekte hello sorunu gidermenize yardımcı olacak hello hata genellikle bir düzey altında bu hata kodudur.</span><span class="sxs-lookup"><span data-stu-id="90b25-127">hello error code that actually helps you resolve hello issue is usually one level below this error.</span></span> <span data-ttu-id="90b25-128">Örneğin, hello aşağıdaki görüntüde hello gösterir **RequestDisallowedByPolicy** hello dağıtım hata altında hata kodu.</span><span class="sxs-lookup"><span data-stu-id="90b25-128">For example, hello following image shows hello **RequestDisallowedByPolicy** error code that is under hello deployment error.</span></span>

![Hata Kodu Göster](./media/resource-manager-common-deployment-errors/error-code.png)

## <a name="skunotavailable"></a><span data-ttu-id="90b25-130">SkuNotAvailable</span><span class="sxs-lookup"><span data-stu-id="90b25-130">SkuNotAvailable</span></span>

<span data-ttu-id="90b25-131">Bir kaynak (genellikle bir sanal makine) dağıtırken hello aşağıdaki hata kodu ve hata iletisini alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="90b25-131">When deploying a resource (typically a virtual machine), you may receive hello following error code and error message:</span></span>

```
Code: SkuNotAvailable
Message: hello requested tier for resource '<resource>' is currently not available in location '<location>' 
for subscription '<subscriptionID>'. Please try another tier or deploy tooa different location.
```

<span data-ttu-id="90b25-132">Hello kaynak (VM boyutu gibi) seçtiniz SKU seçmiş olduğunuz hello konum için kullanılabilir değilse, bu hatayı alırsınız.</span><span class="sxs-lookup"><span data-stu-id="90b25-132">You receive this error when hello resource SKU you have selected (such as VM size) is not available for hello location you have selected.</span></span> <span data-ttu-id="90b25-133">tooresolve Bu sorun bir bölgede kullanılabilir SKU'lar toodetermine gerekir.</span><span class="sxs-lookup"><span data-stu-id="90b25-133">tooresolve this issue, you need toodetermine which SKUs are available in a region.</span></span> <span data-ttu-id="90b25-134">PowerShell, hello portalı veya REST işlemi toofind kullanabileceğiniz kullanılabilir SKU'ları.</span><span class="sxs-lookup"><span data-stu-id="90b25-134">You can use PowerShell, hello portal, or a REST operation toofind available SKUs.</span></span>

- <span data-ttu-id="90b25-135">İçin PowerShell kullanın [Get-AzureRmComputeResourceSku](/powershell/module/azurerm.compute/get-azurermcomputeresourcesku) ve konuma göre filtre.</span><span class="sxs-lookup"><span data-stu-id="90b25-135">For PowerShell, use [Get-AzureRmComputeResourceSku](/powershell/module/azurerm.compute/get-azurermcomputeresourcesku) and filter by location.</span></span> <span data-ttu-id="90b25-136">Merhaba PowerShell'in en son sürümünü bu komutun olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="90b25-136">You must have hello latest version of PowerShell for this command.</span></span>

  ```powershell
  Get-AzureRmComputeResourceSku | where {$_.Locations.Contains("southcentralus")}
  ```

  <span data-ttu-id="90b25-137">Merhaba sonuçları SKU'ları listesi hello konumu için ve SKU yönelik kısıtlamaları içerir.</span><span class="sxs-lookup"><span data-stu-id="90b25-137">hello results include a list of SKUs for hello location and any restrictions for that SKU.</span></span>

  ```powershell
  ResourceType                Name      Locations Restriction                      Capability Value
  ------------                ----      --------- -----------                      ---------- -----
  availabilitySets         Classic southcentralus             MaximumPlatformFaultDomainCount     3
  availabilitySets         Aligned southcentralus             MaximumPlatformFaultDomainCount     3
  virtualMachines      Standard_A0 southcentralus
  virtualMachines      Standard_A1 southcentralus
  virtualMachines      Standard_A2 southcentralus
  ```

- <span data-ttu-id="90b25-138">toouse hello [portal](https://portal.azure.com), toohello Portalı'nda oturum açın ve hello arabirimi aracılığıyla bir kaynak ekleyin.</span><span class="sxs-lookup"><span data-stu-id="90b25-138">toouse hello [portal](https://portal.azure.com), log in toohello portal and add a resource through hello interface.</span></span> <span data-ttu-id="90b25-139">Merhaba değerleri ayarlamak hello görmeniz kaynağı için kullanılabilir SKU'lar.</span><span class="sxs-lookup"><span data-stu-id="90b25-139">As you set hello values, you see hello available SKUs for that resource.</span></span> <span data-ttu-id="90b25-140">Toocomplete hello dağıtım gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="90b25-140">You do not need toocomplete hello deployment.</span></span>

    ![kullanılabilir SKU'lar](./media/resource-manager-common-deployment-errors/view-sku.png)

- <span data-ttu-id="90b25-142">sanal makineler için toouse hello REST API isteği aşağıdaki hello gönder:</span><span class="sxs-lookup"><span data-stu-id="90b25-142">toouse hello REST API for virtual machines, send hello following request:</span></span>

  ```HTTP 
  GET
  https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/skus?api-version=2016-03-30
  ```

  <span data-ttu-id="90b25-143">Kullanılabilir SKU'ları ve bölgeler biçimini izleyen hello döndürür:</span><span class="sxs-lookup"><span data-stu-id="90b25-143">It returns available SKUs and regions in hello following format:</span></span>

  ```json
  {
    "value": [
      {
        "resourceType": "virtualMachines",
        "name": "Standard_A0",
        "tier": "Standard",
        "size": "A0",
        "locations": [
          "eastus"
        ],
        "restrictions": []
      },
      {
        "resourceType": "virtualMachines",
        "name": "Standard_A1",
        "tier": "Standard",
        "size": "A1",
        "locations": [
          "eastus"
        ],
        "restrictions": []
      },
      ...
    ]
  }    
  ```

<span data-ttu-id="90b25-144">Yüklenemiyor toofind bu bölge veya iş gereksinimlerinize uygun bir alternatif bölgede uygun bir SKU varsa, gönderme bir [SKU isteği](https://aka.ms/skurestriction) tooAzure desteği.</span><span class="sxs-lookup"><span data-stu-id="90b25-144">If you are unable toofind a suitable SKU in that region or an alternative region that meets your business needs, submit a [SKU request](https://aka.ms/skurestriction) tooAzure Support.</span></span>

## <a name="disallowedoperation"></a><span data-ttu-id="90b25-145">DisallowedOperation</span><span class="sxs-lookup"><span data-stu-id="90b25-145">DisallowedOperation</span></span>

```
Code: DisallowedOperation
Message: hello current subscription type is not permitted tooperform operations on any provider 
namespace. Please use a different subscription.
```

<span data-ttu-id="90b25-146">Bu hata alırsanız, kullanmakta olduğunuz değil bir abonelik Azure Active Directory dışındaki herhangi bir Azure hizmeti tooaccess izin verilir.</span><span class="sxs-lookup"><span data-stu-id="90b25-146">If you receive this error, you are using a subscription that is not permitted tooaccess any Azure services other than Azure Active Directory.</span></span> <span data-ttu-id="90b25-147">Tooaccess hello Klasik portal gerekir, ancak toodeploy kaynakları izin verilmiyor durumlarda bu tür aboneliği olabilir.</span><span class="sxs-lookup"><span data-stu-id="90b25-147">You might have this type of subscription when you need tooaccess hello classic portal but are not permitted toodeploy resources.</span></span> <span data-ttu-id="90b25-148">tooresolve bu sorunu izni toodeploy kaynaklara sahip bir abonelik kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="90b25-148">tooresolve this issue, you must use a subscription that has permission toodeploy resources.</span></span>  

<span data-ttu-id="90b25-149">tooview kullanılabilir aboneliklerinizi PowerShell ile kullanın:</span><span class="sxs-lookup"><span data-stu-id="90b25-149">tooview your available subscriptions with PowerShell, use:</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="90b25-150">Ve tooset hello geçerli abonelik, kullanın:</span><span class="sxs-lookup"><span data-stu-id="90b25-150">And, tooset hello current subscription, use:</span></span>

```powershell
Set-AzureRmContext -SubscriptionName {subscription-name}
```

<span data-ttu-id="90b25-151">tooview kullanılabilir aboneliklerinizi Azure CLI 2.0 ile birlikte kullanın:</span><span class="sxs-lookup"><span data-stu-id="90b25-151">tooview your available subscriptions with Azure CLI 2.0, use:</span></span>

```azurecli
az account list
```

<span data-ttu-id="90b25-152">Ve tooset hello geçerli abonelik, kullanın:</span><span class="sxs-lookup"><span data-stu-id="90b25-152">And, tooset hello current subscription, use:</span></span>

```azurecli
az account set --subscription {subscription-name}
```

## <a name="invalidtemplate"></a><span data-ttu-id="90b25-153">InvalidTemplate</span><span class="sxs-lookup"><span data-stu-id="90b25-153">InvalidTemplate</span></span>
<span data-ttu-id="90b25-154">Bu hata, birkaç farklı türlerinden hataları neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="90b25-154">This error can result from several different types of errors.</span></span>

- <span data-ttu-id="90b25-155">Sözdizimi hatası</span><span class="sxs-lookup"><span data-stu-id="90b25-155">Syntax error</span></span>

   <span data-ttu-id="90b25-156">Merhaba başarısız şablonu doğrulama bildiren bir hata iletisi alırsanız, şablonunuzun söz dizimi sorunu olabilir.</span><span class="sxs-lookup"><span data-stu-id="90b25-156">If you receive an error message that indicates hello template failed validation, you may have a syntax problem in your template.</span></span>

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed
  ```

   <span data-ttu-id="90b25-157">Bu hata kolay toomake çünkü şablon ifadeleri karmaşık olabilir.</span><span class="sxs-lookup"><span data-stu-id="90b25-157">This error is easy toomake because template expressions can be intricate.</span></span> <span data-ttu-id="90b25-158">Örneğin, hello aşağıdaki ad ataması bir depolama hesabı için bir dizi köşeli ayraçlar, üç işlevi, parantez üç kümesi, tek tırnaklı bir dizi ve bir özellik içerir:</span><span class="sxs-lookup"><span data-stu-id="90b25-158">For example, hello following name assignment for a storage account contains one set of brackets, three functions, three sets of parentheses, one set of single quotes, and one property:</span></span>

  ```json
  "name": "[concat('storage', uniqueString(resourceGroup().id))]",
  ```

   <span data-ttu-id="90b25-159">Merhaba eşleştirme sözdizimi sağlamazsanız hello şablon amacınız farklı bir değer oluşturur.</span><span class="sxs-lookup"><span data-stu-id="90b25-159">If you do not provide hello matching syntax, hello template produces a value that is different than your intention.</span></span>

   <span data-ttu-id="90b25-160">Bu tür hatalara aldığınızda, hello ifade sözdizimini dikkatle gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="90b25-160">When you receive this type of error, carefully review hello expression syntax.</span></span> <span data-ttu-id="90b25-161">Bir JSON Düzenleyicisi gibi kullanmayı [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) veya [Visual Studio Code](resource-manager-vs-code.md), hangi uyar, söz dizimi hataları hakkında.</span><span class="sxs-lookup"><span data-stu-id="90b25-161">Consider using a JSON editor like [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) or [Visual Studio Code](resource-manager-vs-code.md), which can warn you about syntax errors.</span></span>

- <span data-ttu-id="90b25-162">Yanlış segment uzunluklarına</span><span class="sxs-lookup"><span data-stu-id="90b25-162">Incorrect segment lengths</span></span>

   <span data-ttu-id="90b25-163">Merhaba kaynak adı hello doğru biçimde değil başka bir geçersiz şablon hata oluşur.</span><span class="sxs-lookup"><span data-stu-id="90b25-163">Another invalid template error occurs when hello resource name is not in hello correct format.</span></span>

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed: 'hello template resource {resource-name}'
  for type {resource-type} has incorrect segment lengths.
  ```

   <span data-ttu-id="90b25-164">Kök düzeyinde kaynak daha az bir kesim hello adından hello kaynak türünde olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="90b25-164">A root level resource must have one less segment in hello name than in hello resource type.</span></span> <span data-ttu-id="90b25-165">Her segmentinde bir eğik çizgiyle Ayrıştırılan.</span><span class="sxs-lookup"><span data-stu-id="90b25-165">Each segment is differentiated by a slash.</span></span> <span data-ttu-id="90b25-166">Aşağıdaki örneğine hello hello türü iki bölümü vardır ve hello ada sahip bir segment, dolayısıyla bir **geçerli ad**.</span><span class="sxs-lookup"><span data-stu-id="90b25-166">In hello following example, hello type has two segments and hello name has one segment, so it is a **valid name**.</span></span>

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "myHostingPlanName",
    ...
  }
  ```

   <span data-ttu-id="90b25-167">Ancak hello sonraki örnek **geçerli bir ad değil** hello sahip olduğu aynı sayıda hello türü kesimleri.</span><span class="sxs-lookup"><span data-stu-id="90b25-167">But hello next example is **not a valid name** because it has hello same number of segments as hello type.</span></span>

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "appPlan/myHostingPlanName",
    ...
  }
  ```

   <span data-ttu-id="90b25-168">Alt kaynakları için hello hello türü ve ada sahip aynı sayıda kesimleri.</span><span class="sxs-lookup"><span data-stu-id="90b25-168">For child resources, hello type and name have hello same number of segments.</span></span> <span data-ttu-id="90b25-169">Hello üst ad ve tür Hello tam adı ve hello alt türü içerdiği için bu segment sayısına mantıklıdır.</span><span class="sxs-lookup"><span data-stu-id="90b25-169">This number of segments makes sense because hello full name and type for hello child includes hello parent name and type.</span></span> <span data-ttu-id="90b25-170">Bu nedenle, hello tam adı hala hello tam türünü daha küçük bir kesim içeriyor.</span><span class="sxs-lookup"><span data-stu-id="90b25-170">Therefore, hello full name still has one less segment than hello full type.</span></span>

  ```json
  "resources": [
      {
          "type": "Microsoft.KeyVault/vaults",
          "name": "contosokeyvault",
          ...
          "resources": [
              {
                  "type": "secrets",
                  "name": "appPassword",
                  ...
              }
          ]
      }
  ]
  ```

   <span data-ttu-id="90b25-171">Alma hello kesimleri doğru kaynak sağlayıcıları uygulanan Resource Manager türleriyle zor olabilir.</span><span class="sxs-lookup"><span data-stu-id="90b25-171">Getting hello segments right can be tricky with Resource Manager types that are applied across resource providers.</span></span> <span data-ttu-id="90b25-172">Örneğin, bir kaynak kilit tooa web sitesi uygulama dört kesimine sahip bir türü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="90b25-172">For example, applying a resource lock tooa web site requires a type with four segments.</span></span> <span data-ttu-id="90b25-173">Bu nedenle, üç kesimleri hello adıdır:</span><span class="sxs-lookup"><span data-stu-id="90b25-173">Therefore, hello name is three segments:</span></span>

  ```json
  {
      "type": "Microsoft.Web/sites/providers/locks",
      "name": "[concat(variables('siteName'),'/Microsoft.Authorization/MySiteLock')]",
      ...
  }
  ```

- <span data-ttu-id="90b25-174">Kopya dizini beklenmiyor</span><span class="sxs-lookup"><span data-stu-id="90b25-174">Copy index is not expected</span></span>

   <span data-ttu-id="90b25-175">Bu karşılaştığınız **InvalidTemplate** hello uygulandığında hata **kopyalama** öğesi tooa bu öğe desteklemiyor hello şablonunun parçası.</span><span class="sxs-lookup"><span data-stu-id="90b25-175">You encounter this **InvalidTemplate** error when you have applied hello **copy** element tooa part of hello template that does not support this element.</span></span> <span data-ttu-id="90b25-176">Merhaba kopyalama öğesi tooa kaynak türü yalnızca uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90b25-176">You can only apply hello copy element tooa resource type.</span></span> <span data-ttu-id="90b25-177">İçinde bir kaynak türü kopya tooa özelliği uygulanamıyor.</span><span class="sxs-lookup"><span data-stu-id="90b25-177">You cannot apply copy tooa property within a resource type.</span></span> <span data-ttu-id="90b25-178">Örneğin, kopyalama tooa sanal makine geçerli, ancak bir sanal makine için işletim sistemi toohello diskleri uygulanamıyor.</span><span class="sxs-lookup"><span data-stu-id="90b25-178">For example, you apply copy tooa virtual machine, but you cannot apply it toohello OS disks for a virtual machine.</span></span> <span data-ttu-id="90b25-179">Bazı durumlarda, bir alt kaynak tooa üst kaynak toocreate kopyalama döngüsü dönüştürebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90b25-179">In some cases, you can convert a child resource tooa parent resource toocreate a copy loop.</span></span> <span data-ttu-id="90b25-180">Kopya kullanma hakkında daha fazla bilgi için bkz: [Azure Resource Manager'da kaynakları birden çok örneğini oluşturma](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="90b25-180">For more information about using copy, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

- <span data-ttu-id="90b25-181">Parametre geçerli değil</span><span class="sxs-lookup"><span data-stu-id="90b25-181">Parameter is not valid</span></span>

   <span data-ttu-id="90b25-182">Bir parametre için izin verilen değerler Hello şablonu belirtir ve bu değerlerden biri olmayan bir değer sağlayın, aşağıdaki hata iletisini benzer toohello alırsınız:</span><span class="sxs-lookup"><span data-stu-id="90b25-182">If hello template specifies permitted values for a parameter, and you provide a value that is not one of those values, you receive a message similar toohello following error:</span></span>

  ```
  Code=InvalidTemplate;
  Message=Deployment template validation failed: 'hello provided value {parameter value}
  for hello template parameter {parameter name} is not valid. hello parameter value is not
  part of hello allowed values
  ``` 

   <span data-ttu-id="90b25-183">Çift onay hello hello şablonunda izin verilen değerler ve dağıtımı sırasında sağlayın.</span><span class="sxs-lookup"><span data-stu-id="90b25-183">Double check hello allowed values in hello template, and provide one during deployment.</span></span>

- <span data-ttu-id="90b25-184">Döngüsel bağımlılık algılandı</span><span class="sxs-lookup"><span data-stu-id="90b25-184">Circular dependency detected</span></span>

   <span data-ttu-id="90b25-185">Birbirine bağımlı kaynakları hello dağıtım başlatılmasını engelleyen bir şekilde, bu hatayı alırsınız.</span><span class="sxs-lookup"><span data-stu-id="90b25-185">You receive this error when resources depend on each other in a way that prevents hello deployment from starting.</span></span> <span data-ttu-id="90b25-186">Ayrıca bekleyen için diğer kaynaklar bekleyin iki veya daha fazla kaynak bağımlılıklarını bileşimini yapar.</span><span class="sxs-lookup"><span data-stu-id="90b25-186">A combination of interdependencies makes two or more resource wait for other resources that are also waiting.</span></span> <span data-ttu-id="90b25-187">Örneğin, üzerinde resource3 resource1 bağlıdır, üzerinde resource1 switch2 bağlıdır ve üzerinde switch2 resource3 bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="90b25-187">For example, resource1 depends on resource3, resource2 depends on resource1, and resource3 depends on resource2.</span></span> <span data-ttu-id="90b25-188">Genellikle, gereksiz bağımlılıkları kaldırarak bu sorunu çözebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90b25-188">You can usually solve this problem by removing unnecessary dependencies.</span></span> 

<a id="notfound" />
### <a name="notfound-and-resourcenotfound"></a><span data-ttu-id="90b25-189">NotFound ve ResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="90b25-189">NotFound and ResourceNotFound</span></span>
<span data-ttu-id="90b25-190">Şablonunuzu hello çözümlenemeyen kaynağın adını içerdiğinde, benzer bir hata alırsınız:</span><span class="sxs-lookup"><span data-stu-id="90b25-190">When your template includes hello name of a resource that cannot be resolved, you receive an error similar to:</span></span>

```
Code=NotFound;
Message=Cannot find ServerFarm with name exampleplan.
```

<span data-ttu-id="90b25-191">Merhaba şablon kaynağında eksik toodeploy hello çalışıyorsanız, tooadd bir bağımlılık gerekli olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="90b25-191">If you are attempting toodeploy hello missing resource in hello template, check whether you need tooadd a dependency.</span></span> <span data-ttu-id="90b25-192">Resource Manager kaynakları paralel olarak, mümkün olduğunda oluşturarak dağıtım en iyi duruma getirir.</span><span class="sxs-lookup"><span data-stu-id="90b25-192">Resource Manager optimizes deployment by creating resources in parallel, when possible.</span></span> <span data-ttu-id="90b25-193">Bir kaynak sonra başka bir kaynak dağıtılmalıdır, toouse hello gerekir **dependsOn** , şablon toocreate bağımlı bir öğedeki hello diğer kaynak.</span><span class="sxs-lookup"><span data-stu-id="90b25-193">If one resource must be deployed after another resource, you need toouse hello **dependsOn** element in your template toocreate a dependency on hello other resource.</span></span> <span data-ttu-id="90b25-194">Örneğin, bir web uygulaması dağıtırken hello uygulama hizmeti planı bulunması gerekir.</span><span class="sxs-lookup"><span data-stu-id="90b25-194">For example, when deploying a web app, hello App Service plan must exist.</span></span> <span data-ttu-id="90b25-195">Bu başlangıç web uygulaması uygulama hizmeti planı hello üzerinde bağlıdır belirtmediyseniz, Resource Manager her iki kaynağın hello oluşturur. aynı anda.</span><span class="sxs-lookup"><span data-stu-id="90b25-195">If you have not specified that hello web app depends on hello App Service plan, Resource Manager creates both resources at hello same time.</span></span> <span data-ttu-id="90b25-196">Bunu henüz tooset özellik hello web uygulaması üzerinde çalışırken var olmadığından uygulama hizmeti planı kaynak bulunamadı, bu hello bildiren bir hata alırsınız.</span><span class="sxs-lookup"><span data-stu-id="90b25-196">You receive an error stating that hello App Service plan resource cannot be found, because it does not exist yet when attempting tooset a property on hello web app.</span></span> <span data-ttu-id="90b25-197">Bu hata hello web uygulamasında hello bağımlılık ayarlayarak engeller.</span><span class="sxs-lookup"><span data-stu-id="90b25-197">You prevent this error by setting hello dependency in hello web app.</span></span>

```json
{
  "apiVersion": "2015-08-01",
  "type": "Microsoft.Web/sites",
  "dependsOn": [
    "[variables('hostingPlanName')]"
  ],
  ...
}
```

<span data-ttu-id="90b25-198">Bağımlılık hatalarında sorun giderme hakkında daha fazla bilgi için bkz: [denetleyin dağıtım sırası](#check-deployment-sequence).</span><span class="sxs-lookup"><span data-stu-id="90b25-198">For suggestions on troubleshooting dependency errors, see [Check deployment sequence](#check-deployment-sequence).</span></span>

<span data-ttu-id="90b25-199">Farklı bir kaynak grubunda biri için dağıtılan hello daha Hello kaynak mevcut olduğunda bu hata Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="90b25-199">You also see this error when hello resource exists in a different resource group than hello one being deployed to.</span></span> <span data-ttu-id="90b25-200">Bu durumda, hello kullan [ResourceId işlevi](resource-group-template-functions-resource.md#resourceid) tooget hello hello kaynağın tam adı.</span><span class="sxs-lookup"><span data-stu-id="90b25-200">In that case, use hello [resourceId function](resource-group-template-functions-resource.md#resourceid) tooget hello fully qualified name of hello resource.</span></span>

```json
"properties": {
    "name": "[parameters('siteName')]",
    "serverFarmId": "[resourceId('plangroup', 'Microsoft.Web/serverfarms', parameters('hostingPlanName'))]"
}
```

<span data-ttu-id="90b25-201">Toouse hello çalışırsanız [başvuru](resource-group-template-functions-resource.md#reference) veya [listKeys](resource-group-template-functions-resource.md#listkeys) işlevleri bir kaynakla aşağıdaki hata hello aldığınız çözümlenemiyor:</span><span class="sxs-lookup"><span data-stu-id="90b25-201">If you attempt toouse hello [reference](resource-group-template-functions-resource.md#reference) or [listKeys](resource-group-template-functions-resource.md#listkeys) functions with a resource that cannot be resolved, you receive hello following error:</span></span>

```
Code=ResourceNotFound;
Message=hello Resource 'Microsoft.Storage/storageAccounts/{storage name}' under resource
group {resource group name} was not found.
```

<span data-ttu-id="90b25-202">Merhaba içeren bir ifade Ara **başvuru** işlevi.</span><span class="sxs-lookup"><span data-stu-id="90b25-202">Look for an expression that includes hello **reference** function.</span></span> <span data-ttu-id="90b25-203">Çift hello parametre değerlerini doğru olup olmadıklarını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="90b25-203">Double check that hello parameter values are correct.</span></span>

## <a name="parentresourcenotfound"></a><span data-ttu-id="90b25-204">ParentResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="90b25-204">ParentResourceNotFound</span></span>

<span data-ttu-id="90b25-205">Bir kaynak üst tooanother kaynak olduğunda hello üst kaynak hello alt kaynak oluşturmadan önce mevcut olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="90b25-205">When one resource is a parent tooanother resource, hello parent resource must exist before creating hello child resource.</span></span> <span data-ttu-id="90b25-206">Henüz yoksa, aşağıdaki hata hello alırsınız:</span><span class="sxs-lookup"><span data-stu-id="90b25-206">If it does not yet exist, you receive hello following error:</span></span>

```
Code=ParentResourceNotFound;
Message=Can not perform requested operation on nested resource. Parent resource 'exampleserver' not found."
```

<span data-ttu-id="90b25-207">Merhaba hello alt kaynağın adını hello üst adı içerir.</span><span class="sxs-lookup"><span data-stu-id="90b25-207">hello name of hello child resource includes hello parent name.</span></span> <span data-ttu-id="90b25-208">Örneğin, bir SQL veritabanı olarak tanımlanabilir:</span><span class="sxs-lookup"><span data-stu-id="90b25-208">For example, a SQL Database might be defined as:</span></span>

```json
{
  "type": "Microsoft.Sql/servers/databases",
  "name": "[concat(variables('databaseServerName'), '/', parameters('databaseName'))]",
  ...
```

<span data-ttu-id="90b25-209">Ancak, bir bağımlılık hello üst kaynakta belirtmezseniz hello alt kaynak hello üst önce dağıtılan.</span><span class="sxs-lookup"><span data-stu-id="90b25-209">But, if you do not specify a dependency on hello parent resource, hello child resource may get deployed before hello parent.</span></span> <span data-ttu-id="90b25-210">tooresolve bu hata, bir bağımlılık içerir.</span><span class="sxs-lookup"><span data-stu-id="90b25-210">tooresolve this error, include a dependency.</span></span>

```json
"dependsOn": [
    "[variables('databaseServerName')]"
]
```

<a id="storagenamenotunique" />

## <a name="storageaccountalreadyexists-and-storageaccountalreadytaken"></a><span data-ttu-id="90b25-211">StorageAccountAlreadyExists ve StorageAccountAlreadyTaken</span><span class="sxs-lookup"><span data-stu-id="90b25-211">StorageAccountAlreadyExists and StorageAccountAlreadyTaken</span></span>
<span data-ttu-id="90b25-212">Depolama hesapları için Azure arasında benzersizdir hello kaynak için bir ad sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="90b25-212">For storage accounts, you must provide a name for hello resource that is unique across Azure.</span></span> <span data-ttu-id="90b25-213">Benzersiz bir ad belirtmezseniz, benzer bir hata alırsınız:</span><span class="sxs-lookup"><span data-stu-id="90b25-213">If you do not provide a unique name, you receive an error like:</span></span>

```
Code=StorageAccountAlreadyTaken
Message=hello storage account named mystorage is already taken.
```

<span data-ttu-id="90b25-214">Adlandırma kuralınızın hello hello sonucu ile birleştirerek benzersiz bir ad oluşturabilirsiniz [uniqueString](resource-group-template-functions-string.md#uniquestring) işlevi.</span><span class="sxs-lookup"><span data-stu-id="90b25-214">You can create a unique name by concatenating your naming convention with hello result of hello [uniqueString](resource-group-template-functions-string.md#uniquestring) function.</span></span>

```json
"name": "[concat('storage', uniqueString(resourceGroup().id))]",
"type": "Microsoft.Storage/storageAccounts",
```

<span data-ttu-id="90b25-215">Merhaba depolama hesabıyla dağıtırsanız aynı aboneliğinizde var olan bir depolama hesabı adı, ancak farklı bir konum sağlar; belirten hello depolama hesabı zaten var. farklı bir konumda bir hata alırsınız.</span><span class="sxs-lookup"><span data-stu-id="90b25-215">If you deploy a storage account with hello same name as an existing storage account in your subscription, but provide a different location, you receive an error indicating hello storage account already exists in a different location.</span></span> <span data-ttu-id="90b25-216">Merhaba var olan depolama hesabını silmek ya da sağlamak varolan depolama hesabı hello gibi aynı konuma hello.</span><span class="sxs-lookup"><span data-stu-id="90b25-216">Either delete hello existing storage account, or provide hello same location as hello existing storage account.</span></span>

## <a name="accountnameinvalid"></a><span data-ttu-id="90b25-217">AccountNameInvalid</span><span class="sxs-lookup"><span data-stu-id="90b25-217">AccountNameInvalid</span></span>
<span data-ttu-id="90b25-218">Merhaba gördüğünüz **AccountNameInvalid** çalışırken toogive bir depolama hesabını içeren bir adı yasaklanmış karakterleri sırasında hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="90b25-218">You see hello **AccountNameInvalid** error when attempting toogive a storage account a name that includes prohibited characters.</span></span> <span data-ttu-id="90b25-219">Depolama hesabı adları 3 ile 24 karakter uzunluğunda olmalıdır ve rakamlar ve yalnızca küçük harfler kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="90b25-219">Storage account names must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span></span> <span data-ttu-id="90b25-220">Merhaba [uniqueString](resource-group-template-functions-string.md#uniquestring) işlevi 13 karakter döndürür.</span><span class="sxs-lookup"><span data-stu-id="90b25-220">hello [uniqueString](resource-group-template-functions-string.md#uniquestring) function returns 13 characters.</span></span> <span data-ttu-id="90b25-221">Bir önek toohello birleştirmek, **uniqueString** neden, 11 karakterdir bir önek sağlayın veya daha az.</span><span class="sxs-lookup"><span data-stu-id="90b25-221">If you concatenate a prefix toohello **uniqueString** result, provide a prefix that is 11 characters or less.</span></span>

## <a name="badrequest"></a><span data-ttu-id="90b25-222">BadRequest</span><span class="sxs-lookup"><span data-stu-id="90b25-222">BadRequest</span></span>

<span data-ttu-id="90b25-223">Özelliği için geçersiz bir değer sağlarsanız, bir BadRequest durum karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90b25-223">You may encounter a BadRequest status when you provide an invalid value for a property.</span></span> <span data-ttu-id="90b25-224">Örneğin, bir depolama hesabı için hatalı bir SKU değer sağlarsanız, hello dağıtımı başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="90b25-224">For example, if you provide an incorrect SKU value for a storage account, hello deployment fails.</span></span> <span data-ttu-id="90b25-225">özelliği için geçerli değerler toodetermine Ara hello [REST API](/rest/api) dağıttığınız hello kaynak türü için.</span><span class="sxs-lookup"><span data-stu-id="90b25-225">toodetermine valid values for property, look at hello [REST API](/rest/api) for hello resource type you are deploying.</span></span>

<a id="noregisteredproviderfound" />

## <a name="noregisteredproviderfound-and-missingsubscriptionregistration"></a><span data-ttu-id="90b25-226">NoRegisteredProviderFound ve MissingSubscriptionRegistration</span><span class="sxs-lookup"><span data-stu-id="90b25-226">NoRegisteredProviderFound and MissingSubscriptionRegistration</span></span>
<span data-ttu-id="90b25-227">Kaynak dağıtırken, hata kodu aşağıdaki hello almak ve ileti:</span><span class="sxs-lookup"><span data-stu-id="90b25-227">When deploying resource, you may receive hello following error code and message:</span></span>

```
Code: NoRegisteredProviderFound
Message: No registered resource provider found for location {location}
and API version {api-version} for type {resource-type}.
```

<span data-ttu-id="90b25-228">Veya bildiren benzer bir ileti alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="90b25-228">Or, you may receive a similar message that states:</span></span>

```
Code: MissingSubscriptionRegistration
Message: hello subscription is not registered toouse namespace {resource-provider-namespace}
```

<span data-ttu-id="90b25-229">Üç nedenden biri için bu hataları alırsınız:</span><span class="sxs-lookup"><span data-stu-id="90b25-229">You receive these errors for one of three reasons:</span></span>

1. <span data-ttu-id="90b25-230">Merhaba kaynak sağlayıcısı, aboneliğiniz için kayıtlı değil</span><span class="sxs-lookup"><span data-stu-id="90b25-230">hello resource provider has not been registered for your subscription</span></span>
2. <span data-ttu-id="90b25-231">API sürümü Hello kaynak türü için desteklenmiyor</span><span class="sxs-lookup"><span data-stu-id="90b25-231">API version not supported for hello resource type</span></span>
3. <span data-ttu-id="90b25-232">Konum Hello kaynak türü için desteklenmiyor</span><span class="sxs-lookup"><span data-stu-id="90b25-232">Location not supported for hello resource type</span></span>

<span data-ttu-id="90b25-233">Merhaba hata iletisi desteklenen hello konumları ve API sürümleri için öneriler vermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="90b25-233">hello error message should give you suggestions for hello supported locations and API versions.</span></span> <span data-ttu-id="90b25-234">Merhaba, şablon tooone değiştirebilirsiniz önerilen değerleri.</span><span class="sxs-lookup"><span data-stu-id="90b25-234">You can change your template tooone of hello suggested values.</span></span> <span data-ttu-id="90b25-235">Çoğu sağlayıcıları hello Azure portal veya hello komut satırı kullanmakta olduğunuz arabirimi, ancak tüm tarafından otomatik olarak kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="90b25-235">Most providers are registered automatically by hello Azure portal or hello command-line interface you are using, but not all.</span></span> <span data-ttu-id="90b25-236">Belirli kaynak sağlayıcısı önce kullanmadıysanız, bu sağlayıcıyı tooregister gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="90b25-236">If you have not used a particular resource provider before, you may need tooregister that provider.</span></span> <span data-ttu-id="90b25-237">PowerShell veya Azure CLI aracılığıyla kaynak sağlayıcıları hakkında daha fazla bulabilir.</span><span class="sxs-lookup"><span data-stu-id="90b25-237">You can discover more about resource providers through PowerShell or Azure CLI.</span></span>

<span data-ttu-id="90b25-238">**Portal**</span><span class="sxs-lookup"><span data-stu-id="90b25-238">**Portal**</span></span>

<span data-ttu-id="90b25-239">Merhaba kayıt durumunu görmek ve bir kaynak sağlayıcısı ad alanı hello portal üzerinden kaydedin.</span><span class="sxs-lookup"><span data-stu-id="90b25-239">You can see hello registration status and register a resource provider namespace through hello portal.</span></span>

1. <span data-ttu-id="90b25-240">Aboneliğiniz için seçin **kaynak sağlayıcıları**.</span><span class="sxs-lookup"><span data-stu-id="90b25-240">For your subscription, select **Resource providers**.</span></span>

   ![kaynak sağlayıcıları seç](./media/resource-manager-common-deployment-errors/select-resource-provider.png)

2. <span data-ttu-id="90b25-242">Kaynak sağlayıcıları hello listenin bakın ve gerekiyorsa, seçin hello **kaydetmek** bağlantı tooregister hello kaynak sağlayıcısı hello türü toodeploy çalışıyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="90b25-242">Look at hello list of resource providers, and if necessary, select hello **Register** link tooregister hello resource provider of hello type you are trying toodeploy.</span></span>

   ![kaynak sağlayıcıları Listele](./media/resource-manager-common-deployment-errors/list-resource-providers.png)

<span data-ttu-id="90b25-244">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="90b25-244">**PowerShell**</span></span>

<span data-ttu-id="90b25-245">toosee kullanın, kayıt durumunu **Get-AzureRmResourceProvider**.</span><span class="sxs-lookup"><span data-stu-id="90b25-245">toosee your registration status, use **Get-AzureRmResourceProvider**.</span></span>

```powershell
Get-AzureRmResourceProvider -ListAvailable
```

<span data-ttu-id="90b25-246">tooregister bir sağlayıcı kullanmak **Register-AzureRmResourceProvider** hello ad hello kaynak sağlayıcısı tooregister istiyor.</span><span class="sxs-lookup"><span data-stu-id="90b25-246">tooregister a provider, use **Register-AzureRmResourceProvider** and provide hello name of hello resource provider you wish tooregister.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Cdn
```

<span data-ttu-id="90b25-247">belirli bir kaynak türü için tooget desteklenen hello konumlarını kullanın:</span><span class="sxs-lookup"><span data-stu-id="90b25-247">tooget hello supported locations for a particular type of resource, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

<span data-ttu-id="90b25-248">belirli bir kaynak, kullanım türü için desteklenen API sürümleri tooget hello:</span><span class="sxs-lookup"><span data-stu-id="90b25-248">tooget hello supported API versions for a particular type of resource, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).ApiVersions
```

<span data-ttu-id="90b25-249">**Azure CLI**</span><span class="sxs-lookup"><span data-stu-id="90b25-249">**Azure CLI**</span></span>

<span data-ttu-id="90b25-250">toosee hello sağlayıcısı kayıtlı olup olmadığını hello kullan `azure provider list` komutu.</span><span class="sxs-lookup"><span data-stu-id="90b25-250">toosee whether hello provider is registered, use hello `azure provider list` command.</span></span>

```azurecli
az provider list
```

<span data-ttu-id="90b25-251">tooregister bir kaynak sağlayıcısı kullanın hello `azure provider register` komut ve hello belirtin *ad alanı* tooregister.</span><span class="sxs-lookup"><span data-stu-id="90b25-251">tooregister a resource provider, use hello `azure provider register` command, and specify hello *namespace* tooregister.</span></span>

```azurecli
az provider register --namespace Microsoft.Cdn
```

<span data-ttu-id="90b25-252">toosee hello desteklenen konumlar ve API sürümleri için bir kaynak türünü kullanın:</span><span class="sxs-lookup"><span data-stu-id="90b25-252">toosee hello supported locations and API versions for a resource type, use:</span></span>

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

<a id="quotaexceeded" />

## <a name="quotaexceeded-and-operationnotallowed"></a><span data-ttu-id="90b25-253">QuotaExceeded ve OperationNotAllowed</span><span class="sxs-lookup"><span data-stu-id="90b25-253">QuotaExceeded and OperationNotAllowed</span></span>
<span data-ttu-id="90b25-254">Dağıtım kaynak grubu, abonelikler, hesapları ve diğer kapsamları olabilecek bir kota aştığında sorunları olabilir.</span><span class="sxs-lookup"><span data-stu-id="90b25-254">You might have issues when deployment exceeds a quota, which could be per resource group, subscriptions, accounts, and other scopes.</span></span> <span data-ttu-id="90b25-255">Örneğin, aboneliğiniz olabilir toolimit hello bir bölge için çekirdek sayısı yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="90b25-255">For example, your subscription may be configured toolimit hello number of cores for a region.</span></span> <span data-ttu-id="90b25-256">Toodeploy hello tutar izin verilenden daha fazla çekirdek sahip bir sanal makine çalışırsanız belirten hello kotası aşıldı bir hata alıyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="90b25-256">If you attempt toodeploy a virtual machine with more cores than hello permitted amount, you receive an error stating hello quota has been exceeded.</span></span>
<span data-ttu-id="90b25-257">Tam kota bilgi için bkz: [Azure aboneliği ve hizmet sınırları, kotaları ve kısıtlamaları](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="90b25-257">For complete quota information, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="90b25-258">tooexamine aboneliğinizin kotaları çekirdek için hello kullanabilirsiniz `azure vm list-usage` hello Azure CLI komutu.</span><span class="sxs-lookup"><span data-stu-id="90b25-258">tooexamine your subscription's quotas for cores, you can use hello `azure vm list-usage` command in hello Azure CLI.</span></span> <span data-ttu-id="90b25-259">ücretsiz bir deneme hesabı 4 için aşağıdaki örneğine hello bu hello çekirdek kotası gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="90b25-259">hello following example illustrates that hello core quota for a free trial account is 4:</span></span>

```azurecli
az vm list-usage --location "South Central US"
```

<span data-ttu-id="90b25-260">Hangi döndürür:</span><span class="sxs-lookup"><span data-stu-id="90b25-260">Which returns:</span></span>

```azurecli
[
  {
    "currentValue": 0,
    "limit": 2000,
    "name": {
      "localizedValue": "Availability Sets",
      "value": "availabilitySets"
    }
  },
  ...
]
```

<span data-ttu-id="90b25-261">Merhaba Batı ABD bölgesinde dörtten fazla çekirdek oluşturan bir şablonu dağıtmak, benzer bir dağıtım hatası alırsınız:</span><span class="sxs-lookup"><span data-stu-id="90b25-261">If you deploy a template that creates more than four cores in hello West US region, you get a deployment error that looks like:</span></span>

```
Code=OperationNotAllowed
Message=Operation results in exceeding quota limits of Core.
Maximum allowed: 4, Current in use: 4, Additional requested: 2.
```

<span data-ttu-id="90b25-262">Veya, PowerShell'de hello kullanabilirsiniz **Get-AzureRmVMUsage** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="90b25-262">Or in PowerShell, you can use hello **Get-AzureRmVMUsage** cmdlet.</span></span>

```powershell
Get-AzureRmVMUsage
```

<span data-ttu-id="90b25-263">Hangi döndürür:</span><span class="sxs-lookup"><span data-stu-id="90b25-263">Which returns:</span></span>

```powershell
...
CurrentValue : 0
Limit        : 4
Name         : {
                 "value": "cores",
                 "localizedValue": "Total Regional Cores"
               }
Unit         : null
...
```

<span data-ttu-id="90b25-264">Bu durumlarda, toohello portal gidin ve kota toodeploy istediğiniz hello bölge için bir destek sorunu tooraise dosya gerekir.</span><span class="sxs-lookup"><span data-stu-id="90b25-264">In these cases, you should go toohello portal and file a support issue tooraise your quota for hello region into which you want toodeploy.</span></span>

> [!NOTE]
> <span data-ttu-id="90b25-265">Kaynak grupları için hello tüm abonelik için tek tek her bölge için hello kota olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="90b25-265">Remember that for resource groups, hello quota is for each individual region, not for hello entire subscription.</span></span> <span data-ttu-id="90b25-266">Batı ABD 30 çekirdeğini toodeploy gerekiyorsa, Batı ABD 30 Resource Manager çekirdekleri tooask sahip.</span><span class="sxs-lookup"><span data-stu-id="90b25-266">If you need toodeploy 30 cores in West US, you have tooask for 30 Resource Manager cores in West US.</span></span> <span data-ttu-id="90b25-267">Herhangi bir hello bölgeleri toowhich toodeploy 30 çekirdek ihtiyacınız varsa, tüm bölgelerde 30 Resource Manager çekirdekleri istemelisiniz erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90b25-267">If you need toodeploy 30 cores in any of hello regions toowhich you have access, you should ask for 30 Resource Manager cores in all regions.</span></span>
>
>

## <a name="invalidcontentlink"></a><span data-ttu-id="90b25-268">InvalidContentLink</span><span class="sxs-lookup"><span data-stu-id="90b25-268">InvalidContentLink</span></span>
<span data-ttu-id="90b25-269">Ne zaman hello hata iletisini alıyorsunuz:</span><span class="sxs-lookup"><span data-stu-id="90b25-269">When you receive hello error message:</span></span>

```
Code=InvalidContentLink
Message=Unable toodownload deployment content from ...
```

<span data-ttu-id="90b25-270">Büyük olasılıkla kullanılamıyor toolink tooa iç içe geçmiş şablon denediniz.</span><span class="sxs-lookup"><span data-stu-id="90b25-270">You have most likely attempted toolink tooa nested template that is not available.</span></span> <span data-ttu-id="90b25-271">Çift onay hello hello iç içe geçmiş şablonu için sağlanan URI.</span><span class="sxs-lookup"><span data-stu-id="90b25-271">Double check hello URI you provided for hello nested template.</span></span> <span data-ttu-id="90b25-272">Merhaba şablon bir depolama hesabı varsa, hello URI erişilebilir olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="90b25-272">If hello template exists in a storage account, make sure hello URI is accessible.</span></span> <span data-ttu-id="90b25-273">Toopass bir SAS belirteci gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="90b25-273">You may need toopass a SAS token.</span></span> <span data-ttu-id="90b25-274">Daha fazla bilgi için bkz. [Azure Resource Manager ile bağlı şablonları kullanma](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="90b25-274">For more information, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>

## <a name="requestdisallowedbypolicy"></a><span data-ttu-id="90b25-275">RequestDisallowedByPolicy</span><span class="sxs-lookup"><span data-stu-id="90b25-275">RequestDisallowedByPolicy</span></span>
<span data-ttu-id="90b25-276">Aboneliğinizi dağıtımı sırasında tooperform çalıştığınız eylem engelleyen bir kaynak İlkesi içerdiğinde bu hatayı alırsınız.</span><span class="sxs-lookup"><span data-stu-id="90b25-276">You receive this error when your subscription includes a resource policy that prevents an action you are trying tooperform during deployment.</span></span> <span data-ttu-id="90b25-277">Merhaba hata iletisinde hello İlkesi tanımlayıcısı arayın.</span><span class="sxs-lookup"><span data-stu-id="90b25-277">In hello error message, look for hello policy identifier.</span></span>

```
Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'
```

<span data-ttu-id="90b25-278">İçinde **PowerShell**, bu ilke tanımlayıcısı hello olarak sağlamak **kimliği** parametresi tooretrieve dağıtımınızı engellenen hello ilkesi ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="90b25-278">In **PowerShell**, provide that policy identifier as hello **Id** parameter tooretrieve details about hello policy that blocked your deployment.</span></span>

```powershell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

<span data-ttu-id="90b25-279">İçinde **Azure CLI**, hello ilke tanımı hello adını sağlayın:</span><span class="sxs-lookup"><span data-stu-id="90b25-279">In **Azure CLI**, provide hello name of hello policy definition:</span></span>

```azurecli
az policy definition show --name regionPolicyAssignment
```

<span data-ttu-id="90b25-280">Daha fazla bilgi için aşağıdaki makaleler hello bakın:</span><span class="sxs-lookup"><span data-stu-id="90b25-280">For more information, see hello following articles:</span></span>

- [<span data-ttu-id="90b25-281">RequestDisallowedByPolicy hatası</span><span class="sxs-lookup"><span data-stu-id="90b25-281">RequestDisallowedByPolicy error</span></span>](resource-manager-policy-requestdisallowedbypolicy-error.md)
- <span data-ttu-id="90b25-282">[İlke toomanage kaynakları kullanın ve erişimi denetlemenize](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="90b25-282">[Use Policy toomanage resources and control access](resource-manager-policy.md).</span></span>

## <a name="authorization-failed"></a><span data-ttu-id="90b25-283">Yetkilendirme başarısız oldu</span><span class="sxs-lookup"><span data-stu-id="90b25-283">Authorization failed</span></span>
<span data-ttu-id="90b25-284">Merhaba hesabı ya da hizmet sorumlusu toodeploy hello kaynakları çalışırken erişim tooperform bu eylemleri sahip olmadığından, dağıtım sırasında bir hata alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90b25-284">You may receive an error during deployment because hello account or service principal attempting toodeploy hello resources does not have access tooperform those actions.</span></span> <span data-ttu-id="90b25-285">Azure Active Directory veya hangi kimlikleri duyarlık önemli ölçüde ile hangi kaynaklara erişebilir, yönetici toocontrol sağlar.</span><span class="sxs-lookup"><span data-stu-id="90b25-285">Azure Active Directory enables you or your administrator toocontrol which identities can access what resources with a great degree of precision.</span></span> <span data-ttu-id="90b25-286">Örneğin, hesabınıza toohello okuyucu rolüne atanan, değil mümkün toocreate kaynakları demektir.</span><span class="sxs-lookup"><span data-stu-id="90b25-286">For example, if your account is assigned toohello Reader role, you are not able toocreate resources.</span></span> <span data-ttu-id="90b25-287">Bu durumda, yetkilendirme başarısız olduğunu belirten bir hata iletisi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="90b25-287">In that case, you see an error message indicating that authorization failed.</span></span>

<span data-ttu-id="90b25-288">Rol tabanlı erişim denetimi hakkında daha fazla bilgi için bkz: [Azure rol tabanlı erişim denetimi](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="90b25-288">For more information about role-based access control, see [Azure Role-Based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="90b25-289">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="90b25-289">Next steps</span></span>
* <span data-ttu-id="90b25-290">Eylemler, Denetim hakkında toolearn bkz [denetim işlemleri Resource Manager ile](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="90b25-290">toolearn about auditing actions, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="90b25-291">dağıtım sırasında Eylemler toodetermine hello hatalarla ilgili toolearn bkz [görüntülemek dağıtım işlemlerini](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="90b25-291">toolearn about actions toodetermine hello errors during deployment, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
