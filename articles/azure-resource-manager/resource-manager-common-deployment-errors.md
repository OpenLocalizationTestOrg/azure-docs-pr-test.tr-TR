---
title: "Ortak Azure dağıtım hatalarını giderme | Microsoft Docs"
description: "Azure Kaynak Yöneticisi'ni kullanarak Azure kaynakları dağıttığınızda sık karşılaşılan hataların nasıl çözüleceği açıklanmaktadır."
services: azure-resource-manager
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
keywords: "Dağıtım hatası, azure dağıtım azure'a dağıtma"
ms.assetid: c002a9be-4de5-4963-bd14-b54aa3d8fa59
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: tomfitz
ms.openlocfilehash: 30adc10d01290f14a3e116813b19916fa36ab0bc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-common-azure-deployment-errors-with-azure-resource-manager"></a><span data-ttu-id="0e874-104">Ortak Azure dağıtım hataları Azure Resource Manager ile ilgili sorunları giderme</span><span class="sxs-lookup"><span data-stu-id="0e874-104">Troubleshoot common Azure deployment errors with Azure Resource Manager</span></span>
<span data-ttu-id="0e874-105">Bu konu, bazı ortak nasıl çözebilirsiniz açıklar karşılaşabileceğiniz Azure dağıtım hataları.</span><span class="sxs-lookup"><span data-stu-id="0e874-105">This topic describes how you can resolve some common Azure deployment errors you may encounter.</span></span>

<span data-ttu-id="0e874-106">Bu konuda aşağıdaki hata kodları açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="0e874-106">The following error codes are described in this topic:</span></span>

* [<span data-ttu-id="0e874-107">AccountNameInvalid</span><span class="sxs-lookup"><span data-stu-id="0e874-107">AccountNameInvalid</span></span>](#accountnameinvalid)
* [<span data-ttu-id="0e874-108">Yetkilendirme başarısız oldu</span><span class="sxs-lookup"><span data-stu-id="0e874-108">Authorization failed</span></span>](#authorization-failed)
* [<span data-ttu-id="0e874-109">BadRequest</span><span class="sxs-lookup"><span data-stu-id="0e874-109">BadRequest</span></span>](#badrequest)
* [<span data-ttu-id="0e874-110">DeploymentFailed</span><span class="sxs-lookup"><span data-stu-id="0e874-110">DeploymentFailed</span></span>](#deploymentfailed)
* [<span data-ttu-id="0e874-111">DisallowedOperation</span><span class="sxs-lookup"><span data-stu-id="0e874-111">DisallowedOperation</span></span>](#disallowedoperation)
* [<span data-ttu-id="0e874-112">InvalidContentLink</span><span class="sxs-lookup"><span data-stu-id="0e874-112">InvalidContentLink</span></span>](#invalidcontentlink)
* [<span data-ttu-id="0e874-113">InvalidTemplate</span><span class="sxs-lookup"><span data-stu-id="0e874-113">InvalidTemplate</span></span>](#invalidtemplate)
* [<span data-ttu-id="0e874-114">MissingSubscriptionRegistration</span><span class="sxs-lookup"><span data-stu-id="0e874-114">MissingSubscriptionRegistration</span></span>](#noregisteredproviderfound)
* [<span data-ttu-id="0e874-115">NotFound</span><span class="sxs-lookup"><span data-stu-id="0e874-115">NotFound</span></span>](#notfound)
* [<span data-ttu-id="0e874-116">NoRegisteredProviderFound</span><span class="sxs-lookup"><span data-stu-id="0e874-116">NoRegisteredProviderFound</span></span>](#noregisteredproviderfound)
* [<span data-ttu-id="0e874-117">OperationNotAllowed</span><span class="sxs-lookup"><span data-stu-id="0e874-117">OperationNotAllowed</span></span>](#quotaexceeded)
* [<span data-ttu-id="0e874-118">ParentResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="0e874-118">ParentResourceNotFound</span></span>](#parentresourcenotfound)
* [<span data-ttu-id="0e874-119">QuotaExceeded</span><span class="sxs-lookup"><span data-stu-id="0e874-119">QuotaExceeded</span></span>](#quotaexceeded)
* [<span data-ttu-id="0e874-120">RequestDisallowedByPolicy</span><span class="sxs-lookup"><span data-stu-id="0e874-120">RequestDisallowedByPolicy</span></span>](#requestdisallowedbypolicy)
* [<span data-ttu-id="0e874-121">ResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="0e874-121">ResourceNotFound</span></span>](#notfound)
* [<span data-ttu-id="0e874-122">SkuNotAvailable</span><span class="sxs-lookup"><span data-stu-id="0e874-122">SkuNotAvailable</span></span>](#skunotavailable)
* [<span data-ttu-id="0e874-123">StorageAccountAlreadyExists</span><span class="sxs-lookup"><span data-stu-id="0e874-123">StorageAccountAlreadyExists</span></span>](#storagenamenotunique)
* [<span data-ttu-id="0e874-124">StorageAccountAlreadyTaken</span><span class="sxs-lookup"><span data-stu-id="0e874-124">StorageAccountAlreadyTaken</span></span>](#storagenamenotunique)

## <a name="deploymentfailed"></a><span data-ttu-id="0e874-125">DeploymentFailed</span><span class="sxs-lookup"><span data-stu-id="0e874-125">DeploymentFailed</span></span>

<span data-ttu-id="0e874-126">Bu hata kodu genel dağıtım hatası gösterir, ancak sorun giderme başlatmak için gereken hata kodu değil.</span><span class="sxs-lookup"><span data-stu-id="0e874-126">This error code indicates a general deployment error, but it is not the error code you need to start troubleshooting.</span></span> <span data-ttu-id="0e874-127">Aslında, sorunu gidermenize yardımcı olacak hata genellikle bir düzey altında bu hata kodudur.</span><span class="sxs-lookup"><span data-stu-id="0e874-127">The error code that actually helps you resolve the issue is usually one level below this error.</span></span> <span data-ttu-id="0e874-128">Örneğin, aşağıdaki gösterir görüntü **RequestDisallowedByPolicy** altında dağıtım hata hata kodu.</span><span class="sxs-lookup"><span data-stu-id="0e874-128">For example, the following image shows the **RequestDisallowedByPolicy** error code that is under the deployment error.</span></span>

![Hata Kodu Göster](./media/resource-manager-common-deployment-errors/error-code.png)

## <a name="skunotavailable"></a><span data-ttu-id="0e874-130">SkuNotAvailable</span><span class="sxs-lookup"><span data-stu-id="0e874-130">SkuNotAvailable</span></span>

<span data-ttu-id="0e874-131">Bir kaynak (genellikle bir sanal makine) dağıtırken şu hata kodu ve hata iletisini alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0e874-131">When deploying a resource (typically a virtual machine), you may receive the following error code and error message:</span></span>

```
Code: SkuNotAvailable
Message: The requested tier for resource '<resource>' is currently not available in location '<location>' 
for subscription '<subscriptionID>'. Please try another tier or deploy to a different location.
```

<span data-ttu-id="0e874-132">(VM boyutu gibi) seçtiniz SKU kaynak seçtiğiniz konum için kullanılabilir olmadığında bu hatayı alırsınız.</span><span class="sxs-lookup"><span data-stu-id="0e874-132">You receive this error when the resource SKU you have selected (such as VM size) is not available for the location you have selected.</span></span> <span data-ttu-id="0e874-133">Bu sorunu çözmek için SKU'ları bir bölgede kullanılabilir olan belirlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="0e874-133">To resolve this issue, you need to determine which SKUs are available in a region.</span></span> <span data-ttu-id="0e874-134">Kullanılabilir SKU'lar bulmak için PowerShell, portalı veya REST işlemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="0e874-134">You can use PowerShell, the portal, or a REST operation to find available SKUs.</span></span>

- <span data-ttu-id="0e874-135">İçin PowerShell kullanın [Get-AzureRmComputeResourceSku](/powershell/module/azurerm.compute/get-azurermcomputeresourcesku) ve konuma göre filtre.</span><span class="sxs-lookup"><span data-stu-id="0e874-135">For PowerShell, use [Get-AzureRmComputeResourceSku](/powershell/module/azurerm.compute/get-azurermcomputeresourcesku) and filter by location.</span></span> <span data-ttu-id="0e874-136">Bu komut için PowerShell en son sürümünü olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0e874-136">You must have the latest version of PowerShell for this command.</span></span>

  ```powershell
  Get-AzureRmComputeResourceSku | where {$_.Locations.Contains("southcentralus")}
  ```

  <span data-ttu-id="0e874-137">Sonuçlar SKU'ları listesi için konum ve SKU yönelik kısıtlamaları içerir.</span><span class="sxs-lookup"><span data-stu-id="0e874-137">The results include a list of SKUs for the location and any restrictions for that SKU.</span></span>

  ```powershell
  ResourceType                Name      Locations Restriction                      Capability Value
  ------------                ----      --------- -----------                      ---------- -----
  availabilitySets         Classic southcentralus             MaximumPlatformFaultDomainCount     3
  availabilitySets         Aligned southcentralus             MaximumPlatformFaultDomainCount     3
  virtualMachines      Standard_A0 southcentralus
  virtualMachines      Standard_A1 southcentralus
  virtualMachines      Standard_A2 southcentralus
  ```

- <span data-ttu-id="0e874-138">Kullanılacak [portal](https://portal.azure.com), portalda oturum açın ve kaynak arabirimi üzerinden ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0e874-138">To use the [portal](https://portal.azure.com), log in to the portal and add a resource through the interface.</span></span> <span data-ttu-id="0e874-139">Değerleri ayarlama gibi bu kaynak için kullanılabilir SKU'lar bakın.</span><span class="sxs-lookup"><span data-stu-id="0e874-139">As you set the values, you see the available SKUs for that resource.</span></span> <span data-ttu-id="0e874-140">Dağıtımın tamamlanması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="0e874-140">You do not need to complete the deployment.</span></span>

    ![kullanılabilir SKU'lar](./media/resource-manager-common-deployment-errors/view-sku.png)

- <span data-ttu-id="0e874-142">Sanal makineler için REST API kullanmak için aşağıdaki isteği gönder:</span><span class="sxs-lookup"><span data-stu-id="0e874-142">To use the REST API for virtual machines, send the following request:</span></span>

  ```HTTP 
  GET
  https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/skus?api-version=2016-03-30
  ```

  <span data-ttu-id="0e874-143">Kullanılabilir SKU'ları ve bölgeler şu biçimde döndürür:</span><span class="sxs-lookup"><span data-stu-id="0e874-143">It returns available SKUs and regions in the following format:</span></span>

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

<span data-ttu-id="0e874-144">Bu bölgede uygun SKU bulamıyor veya işletmenizin karşılayan bir alternatif bölge gönderme gereksinimlerini bir [SKU isteği](https://aka.ms/skurestriction) Azure desteği.</span><span class="sxs-lookup"><span data-stu-id="0e874-144">If you are unable to find a suitable SKU in that region or an alternative region that meets your business needs, submit a [SKU request](https://aka.ms/skurestriction) to Azure Support.</span></span>

## <a name="disallowedoperation"></a><span data-ttu-id="0e874-145">DisallowedOperation</span><span class="sxs-lookup"><span data-stu-id="0e874-145">DisallowedOperation</span></span>

```
Code: DisallowedOperation
Message: The current subscription type is not permitted to perform operations on any provider 
namespace. Please use a different subscription.
```

<span data-ttu-id="0e874-146">Bu hata alırsanız, Azure Active Directory dışındaki herhangi bir Azure hizmeti erişim izni olmayan bir aboneliği kullanıyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="0e874-146">If you receive this error, you are using a subscription that is not permitted to access any Azure services other than Azure Active Directory.</span></span> <span data-ttu-id="0e874-147">Klasik Portalı'nı erişmeniz gerekir, ancak kaynaklar dağıtmak için izin verilmiyor durumlarda bu tür aboneliği olabilir.</span><span class="sxs-lookup"><span data-stu-id="0e874-147">You might have this type of subscription when you need to access the classic portal but are not permitted to deploy resources.</span></span> <span data-ttu-id="0e874-148">Bu sorunu çözmek için kaynakları dağıtmak için izne sahip bir abonelik kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0e874-148">To resolve this issue, you must use a subscription that has permission to deploy resources.</span></span>  

<span data-ttu-id="0e874-149">PowerShell ile kullanılabilir aboneliklerinizi görüntülemek için kullanın:</span><span class="sxs-lookup"><span data-stu-id="0e874-149">To view your available subscriptions with PowerShell, use:</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="0e874-150">Ve şu anki aboneliği ayarlamak için kullanın:</span><span class="sxs-lookup"><span data-stu-id="0e874-150">And, to set the current subscription, use:</span></span>

```powershell
Set-AzureRmContext -SubscriptionName {subscription-name}
```

<span data-ttu-id="0e874-151">Azure CLI 2.0 ile birlikte kullanılabilir aboneliklerinizi görüntülemek için kullanın:</span><span class="sxs-lookup"><span data-stu-id="0e874-151">To view your available subscriptions with Azure CLI 2.0, use:</span></span>

```azurecli
az account list
```

<span data-ttu-id="0e874-152">Ve şu anki aboneliği ayarlamak için kullanın:</span><span class="sxs-lookup"><span data-stu-id="0e874-152">And, to set the current subscription, use:</span></span>

```azurecli
az account set --subscription {subscription-name}
```

## <a name="invalidtemplate"></a><span data-ttu-id="0e874-153">InvalidTemplate</span><span class="sxs-lookup"><span data-stu-id="0e874-153">InvalidTemplate</span></span>
<span data-ttu-id="0e874-154">Bu hata, birkaç farklı türlerinden hataları neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="0e874-154">This error can result from several different types of errors.</span></span>

- <span data-ttu-id="0e874-155">Sözdizimi hatası</span><span class="sxs-lookup"><span data-stu-id="0e874-155">Syntax error</span></span>

   <span data-ttu-id="0e874-156">Şablon başarısız doğrulama bildiren bir hata iletisi alırsanız, şablonunuzun söz dizimi sorunu olabilir.</span><span class="sxs-lookup"><span data-stu-id="0e874-156">If you receive an error message that indicates the template failed validation, you may have a syntax problem in your template.</span></span>

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed
  ```

   <span data-ttu-id="0e874-157">Bu hata, şablon ifadeleri karmaşık olabileceğinden yapmak kolaydır.</span><span class="sxs-lookup"><span data-stu-id="0e874-157">This error is easy to make because template expressions can be intricate.</span></span> <span data-ttu-id="0e874-158">Örneğin, aşağıdaki ad ataması bir depolama hesabı için bir dizi köşeli ayraçlar, üç işlevi, parantez üç kümesi, tek tırnak bir dizi ve bir özellik içerir:</span><span class="sxs-lookup"><span data-stu-id="0e874-158">For example, the following name assignment for a storage account contains one set of brackets, three functions, three sets of parentheses, one set of single quotes, and one property:</span></span>

  ```json
  "name": "[concat('storage', uniqueString(resourceGroup().id))]",
  ```

   <span data-ttu-id="0e874-159">Eşleştirme sözdizimi belirtmezseniz, şablon amacınız farklı bir değer oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0e874-159">If you do not provide the matching syntax, the template produces a value that is different than your intention.</span></span>

   <span data-ttu-id="0e874-160">Bu tür hatalara aldığınızda, ifade sözdizimini dikkatle gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="0e874-160">When you receive this type of error, carefully review the expression syntax.</span></span> <span data-ttu-id="0e874-161">Bir JSON Düzenleyicisi gibi kullanmayı [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) veya [Visual Studio Code](resource-manager-vs-code.md), hangi uyar, söz dizimi hataları hakkında.</span><span class="sxs-lookup"><span data-stu-id="0e874-161">Consider using a JSON editor like [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) or [Visual Studio Code](resource-manager-vs-code.md), which can warn you about syntax errors.</span></span>

- <span data-ttu-id="0e874-162">Yanlış segment uzunluklarına</span><span class="sxs-lookup"><span data-stu-id="0e874-162">Incorrect segment lengths</span></span>

   <span data-ttu-id="0e874-163">Kaynak adı doğru biçimde değil başka bir geçersiz şablon hata oluşur.</span><span class="sxs-lookup"><span data-stu-id="0e874-163">Another invalid template error occurs when the resource name is not in the correct format.</span></span>

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed: 'The template resource {resource-name}'
  for type {resource-type} has incorrect segment lengths.
  ```

   <span data-ttu-id="0e874-164">Kök düzeyinde kaynak daha az bir kesim adından kaynak türünde olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0e874-164">A root level resource must have one less segment in the name than in the resource type.</span></span> <span data-ttu-id="0e874-165">Her segmentinde bir eğik çizgiyle Ayrıştırılan.</span><span class="sxs-lookup"><span data-stu-id="0e874-165">Each segment is differentiated by a slash.</span></span> <span data-ttu-id="0e874-166">Aşağıdaki örnekte, iki bölümü türü ve dolayısıyla bir kesim adına sahip bir **geçerli ad**.</span><span class="sxs-lookup"><span data-stu-id="0e874-166">In the following example, the type has two segments and the name has one segment, so it is a **valid name**.</span></span>

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "myHostingPlanName",
    ...
  }
  ```

   <span data-ttu-id="0e874-167">Ancak sonraki örnek **geçerli bir ad değil** türü aynı sayıda Segment içerdiğinden.</span><span class="sxs-lookup"><span data-stu-id="0e874-167">But the next example is **not a valid name** because it has the same number of segments as the type.</span></span>

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "appPlan/myHostingPlanName",
    ...
  }
  ```

   <span data-ttu-id="0e874-168">Alt kaynakları için kesimleri ile aynı sayıda türü ve ada sahip.</span><span class="sxs-lookup"><span data-stu-id="0e874-168">For child resources, the type and name have the same number of segments.</span></span> <span data-ttu-id="0e874-169">Tam adı ve alt türü içerdiği için üst adını ve türünü Segment sayısı mantıklıdır.</span><span class="sxs-lookup"><span data-stu-id="0e874-169">This number of segments makes sense because the full name and type for the child includes the parent name and type.</span></span> <span data-ttu-id="0e874-170">Bu nedenle, tam adı, tam türünü daha küçük bir kesim hala vardır.</span><span class="sxs-lookup"><span data-stu-id="0e874-170">Therefore, the full name still has one less segment than the full type.</span></span>

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

   <span data-ttu-id="0e874-171">Segment sağ alma kaynak sağlayıcıları uygulanan Resource Manager türleriyle zor olabilir.</span><span class="sxs-lookup"><span data-stu-id="0e874-171">Getting the segments right can be tricky with Resource Manager types that are applied across resource providers.</span></span> <span data-ttu-id="0e874-172">Örneğin, bir web sitesi için bir kaynak kilidi uygulama dört kesimine sahip bir türü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="0e874-172">For example, applying a resource lock to a web site requires a type with four segments.</span></span> <span data-ttu-id="0e874-173">Bu nedenle, üç kesimleri adıdır:</span><span class="sxs-lookup"><span data-stu-id="0e874-173">Therefore, the name is three segments:</span></span>

  ```json
  {
      "type": "Microsoft.Web/sites/providers/locks",
      "name": "[concat(variables('siteName'),'/Microsoft.Authorization/MySiteLock')]",
      ...
  }
  ```

- <span data-ttu-id="0e874-174">Kopya dizini beklenmiyor</span><span class="sxs-lookup"><span data-stu-id="0e874-174">Copy index is not expected</span></span>

   <span data-ttu-id="0e874-175">Bu karşılaştığınız **InvalidTemplate** uygulandığında hata **kopya** bu öğe desteklemiyor şablonunun parçası öğesi.</span><span class="sxs-lookup"><span data-stu-id="0e874-175">You encounter this **InvalidTemplate** error when you have applied the **copy** element to a part of the template that does not support this element.</span></span> <span data-ttu-id="0e874-176">Yalnızca bir kaynak türü kopya öğesi uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e874-176">You can only apply the copy element to a resource type.</span></span> <span data-ttu-id="0e874-177">Bir kaynak türü içinde bir özellik kopyalama uygulayamazsınız.</span><span class="sxs-lookup"><span data-stu-id="0e874-177">You cannot apply copy to a property within a resource type.</span></span> <span data-ttu-id="0e874-178">Örneğin, kopya bir sanal makine için geçerli, ancak bir sanal makine için işletim sistemi disklere uygulanamıyor.</span><span class="sxs-lookup"><span data-stu-id="0e874-178">For example, you apply copy to a virtual machine, but you cannot apply it to the OS disks for a virtual machine.</span></span> <span data-ttu-id="0e874-179">Bazı durumlarda, kopyalama döngüsü oluşturmak için bir üst kaynağına bağımlı kaynak dönüştürebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e874-179">In some cases, you can convert a child resource to a parent resource to create a copy loop.</span></span> <span data-ttu-id="0e874-180">Kopya kullanma hakkında daha fazla bilgi için bkz: [Azure Resource Manager'da kaynakları birden çok örneğini oluşturma](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="0e874-180">For more information about using copy, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

- <span data-ttu-id="0e874-181">Parametre geçerli değil</span><span class="sxs-lookup"><span data-stu-id="0e874-181">Parameter is not valid</span></span>

   <span data-ttu-id="0e874-182">İzin verilen değerler bir parametre için kullanılacak şablonu belirtir ve bu değerlerden biri olmayan bir değer sağlayın, aşağıdakine benzer bir ileti alırsınız:</span><span class="sxs-lookup"><span data-stu-id="0e874-182">If the template specifies permitted values for a parameter, and you provide a value that is not one of those values, you receive a message similar to the following error:</span></span>

  ```
  Code=InvalidTemplate;
  Message=Deployment template validation failed: 'The provided value {parameter value}
  for the template parameter {parameter name} is not valid. The parameter value is not
  part of the allowed values
  ``` 

   <span data-ttu-id="0e874-183">Double şablondaki izin verilen değerler denetleyin ve dağıtım sırasında bir sağlayın.</span><span class="sxs-lookup"><span data-stu-id="0e874-183">Double check the allowed values in the template, and provide one during deployment.</span></span>

- <span data-ttu-id="0e874-184">Döngüsel bağımlılık algılandı</span><span class="sxs-lookup"><span data-stu-id="0e874-184">Circular dependency detected</span></span>

   <span data-ttu-id="0e874-185">Birbirine bağımlı kaynakları dağıtım başlatılmasını engelleyen bir şekilde, bu hatayı alırsınız.</span><span class="sxs-lookup"><span data-stu-id="0e874-185">You receive this error when resources depend on each other in a way that prevents the deployment from starting.</span></span> <span data-ttu-id="0e874-186">Ayrıca bekleyen için diğer kaynaklar bekleyin iki veya daha fazla kaynak bağımlılıklarını bileşimini yapar.</span><span class="sxs-lookup"><span data-stu-id="0e874-186">A combination of interdependencies makes two or more resource wait for other resources that are also waiting.</span></span> <span data-ttu-id="0e874-187">Örneğin, üzerinde resource3 resource1 bağlıdır, üzerinde resource1 switch2 bağlıdır ve üzerinde switch2 resource3 bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="0e874-187">For example, resource1 depends on resource3, resource2 depends on resource1, and resource3 depends on resource2.</span></span> <span data-ttu-id="0e874-188">Genellikle, gereksiz bağımlılıkları kaldırarak bu sorunu çözebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e874-188">You can usually solve this problem by removing unnecessary dependencies.</span></span> 

<a id="notfound" />
### <a name="notfound-and-resourcenotfound"></a><span data-ttu-id="0e874-189">NotFound ve ResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="0e874-189">NotFound and ResourceNotFound</span></span>
<span data-ttu-id="0e874-190">Şablonunuzu çözümlenemeyen kaynağın adını içerdiğinde, benzer bir hata alırsınız:</span><span class="sxs-lookup"><span data-stu-id="0e874-190">When your template includes the name of a resource that cannot be resolved, you receive an error similar to:</span></span>

```
Code=NotFound;
Message=Cannot find ServerFarm with name exampleplan.
```

<span data-ttu-id="0e874-191">Şablon eksik kaynak dağıtmak çalışıyorsunuz, bir bağımlılık eklemeniz gerekip gerekmediğini denetleyin.</span><span class="sxs-lookup"><span data-stu-id="0e874-191">If you are attempting to deploy the missing resource in the template, check whether you need to add a dependency.</span></span> <span data-ttu-id="0e874-192">Resource Manager kaynakları paralel olarak, mümkün olduğunda oluşturarak dağıtım en iyi duruma getirir.</span><span class="sxs-lookup"><span data-stu-id="0e874-192">Resource Manager optimizes deployment by creating resources in parallel, when possible.</span></span> <span data-ttu-id="0e874-193">Bir kaynak sonra başka bir kaynak dağıtılmalıdır, kullanmanıza gerek **dependsOn** öğesi şablonunuzda diğer kaynak üzerinde bir bağımlılık oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0e874-193">If one resource must be deployed after another resource, you need to use the **dependsOn** element in your template to create a dependency on the other resource.</span></span> <span data-ttu-id="0e874-194">Örneğin, bir web uygulaması dağıtımını yaparken, uygulama hizmeti planı bulunması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0e874-194">For example, when deploying a web app, the App Service plan must exist.</span></span> <span data-ttu-id="0e874-195">Web uygulaması uygulama hizmeti plan üzerinde bağlıdır belirtmediyseniz, Resource Manager aynı anda hem de kaynaklar oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0e874-195">If you have not specified that the web app depends on the App Service plan, Resource Manager creates both resources at the same time.</span></span> <span data-ttu-id="0e874-196">Bunu henüz web uygulamasında bir özellik Ayarla girişiminde bulunulduğunda var olmadığından uygulama hizmeti planı kaynağın bulunamadığını bildiren bir hata alırsınız.</span><span class="sxs-lookup"><span data-stu-id="0e874-196">You receive an error stating that the App Service plan resource cannot be found, because it does not exist yet when attempting to set a property on the web app.</span></span> <span data-ttu-id="0e874-197">Bu hata, web uygulamasında bağımlılık ayarlayarak engeller.</span><span class="sxs-lookup"><span data-stu-id="0e874-197">You prevent this error by setting the dependency in the web app.</span></span>

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

<span data-ttu-id="0e874-198">Bağımlılık hatalarında sorun giderme hakkında daha fazla bilgi için bkz: [denetleyin dağıtım sırası](#check-deployment-sequence).</span><span class="sxs-lookup"><span data-stu-id="0e874-198">For suggestions on troubleshooting dependency errors, see [Check deployment sequence](#check-deployment-sequence).</span></span>

<span data-ttu-id="0e874-199">İçin dağıtılan olandan farklı bir kaynak grubundaki kaynak mevcut olduğunda bu hata Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="0e874-199">You also see this error when the resource exists in a different resource group than the one being deployed to.</span></span> <span data-ttu-id="0e874-200">Bu durumda, kullanın [ResourceId işlevi](resource-group-template-functions-resource.md#resourceid) kaynak tam adını almak için.</span><span class="sxs-lookup"><span data-stu-id="0e874-200">In that case, use the [resourceId function](resource-group-template-functions-resource.md#resourceid) to get the fully qualified name of the resource.</span></span>

```json
"properties": {
    "name": "[parameters('siteName')]",
    "serverFarmId": "[resourceId('plangroup', 'Microsoft.Web/serverfarms', parameters('hostingPlanName'))]"
}
```

<span data-ttu-id="0e874-201">Kullanmayı denerseniz, [başvuru](resource-group-template-functions-resource.md#reference) veya [listKeys](resource-group-template-functions-resource.md#listkeys) işlevleri bir kaynakla aşağıdaki hata iletisini çözümlenemiyor:</span><span class="sxs-lookup"><span data-stu-id="0e874-201">If you attempt to use the [reference](resource-group-template-functions-resource.md#reference) or [listKeys](resource-group-template-functions-resource.md#listkeys) functions with a resource that cannot be resolved, you receive the following error:</span></span>

```
Code=ResourceNotFound;
Message=The Resource 'Microsoft.Storage/storageAccounts/{storage name}' under resource
group {resource group name} was not found.
```

<span data-ttu-id="0e874-202">İçeren bir ifade Ara **başvuru** işlevi.</span><span class="sxs-lookup"><span data-stu-id="0e874-202">Look for an expression that includes the **reference** function.</span></span> <span data-ttu-id="0e874-203">Parametre değerleri doğru olduğunu kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="0e874-203">Double check that the parameter values are correct.</span></span>

## <a name="parentresourcenotfound"></a><span data-ttu-id="0e874-204">ParentResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="0e874-204">ParentResourceNotFound</span></span>

<span data-ttu-id="0e874-205">Bir kaynağı başka bir kaynak için bir üst olduğunda, üst kaynak alt kaynak oluşturmadan önce mevcut olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0e874-205">When one resource is a parent to another resource, the parent resource must exist before creating the child resource.</span></span> <span data-ttu-id="0e874-206">Henüz yoksa, aşağıdaki hatayı alırsınız:</span><span class="sxs-lookup"><span data-stu-id="0e874-206">If it does not yet exist, you receive the following error:</span></span>

```
Code=ParentResourceNotFound;
Message=Can not perform requested operation on nested resource. Parent resource 'exampleserver' not found."
```

<span data-ttu-id="0e874-207">Alt kaynağın adını üst adı içerir.</span><span class="sxs-lookup"><span data-stu-id="0e874-207">The name of the child resource includes the parent name.</span></span> <span data-ttu-id="0e874-208">Örneğin, bir SQL veritabanı olarak tanımlanabilir:</span><span class="sxs-lookup"><span data-stu-id="0e874-208">For example, a SQL Database might be defined as:</span></span>

```json
{
  "type": "Microsoft.Sql/servers/databases",
  "name": "[concat(variables('databaseServerName'), '/', parameters('databaseName'))]",
  ...
```

<span data-ttu-id="0e874-209">Ancak, bir bağımlılık üst kaynakta belirtmezseniz, alt kaynak önce üst dağıtılan.</span><span class="sxs-lookup"><span data-stu-id="0e874-209">But, if you do not specify a dependency on the parent resource, the child resource may get deployed before the parent.</span></span> <span data-ttu-id="0e874-210">Bu hatayı gidermek için bir bağımlılık ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0e874-210">To resolve this error, include a dependency.</span></span>

```json
"dependsOn": [
    "[variables('databaseServerName')]"
]
```

<a id="storagenamenotunique" />

## <a name="storageaccountalreadyexists-and-storageaccountalreadytaken"></a><span data-ttu-id="0e874-211">StorageAccountAlreadyExists ve StorageAccountAlreadyTaken</span><span class="sxs-lookup"><span data-stu-id="0e874-211">StorageAccountAlreadyExists and StorageAccountAlreadyTaken</span></span>
<span data-ttu-id="0e874-212">Depolama hesapları için Azure arasında benzersiz kaynak için bir ad sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0e874-212">For storage accounts, you must provide a name for the resource that is unique across Azure.</span></span> <span data-ttu-id="0e874-213">Benzersiz bir ad belirtmezseniz, benzer bir hata alırsınız:</span><span class="sxs-lookup"><span data-stu-id="0e874-213">If you do not provide a unique name, you receive an error like:</span></span>

```
Code=StorageAccountAlreadyTaken
Message=The storage account named mystorage is already taken.
```

<span data-ttu-id="0e874-214">Adlandırma kuralınızın sonucu ile birleştirerek benzersiz bir ad oluşturabilirsiniz [uniqueString](resource-group-template-functions-string.md#uniquestring) işlevi.</span><span class="sxs-lookup"><span data-stu-id="0e874-214">You can create a unique name by concatenating your naming convention with the result of the [uniqueString](resource-group-template-functions-string.md#uniquestring) function.</span></span>

```json
"name": "[concat('storage', uniqueString(resourceGroup().id))]",
"type": "Microsoft.Storage/storageAccounts",
```

<span data-ttu-id="0e874-215">Aboneliğinizde var olan bir depolama hesabıyla aynı ada sahip bir depolama hesabı dağıtmak, ancak farklı bir konum sağlayın, depolama hesabı zaten var. farklı bir konumda belirten bir hata alırsınız.</span><span class="sxs-lookup"><span data-stu-id="0e874-215">If you deploy a storage account with the same name as an existing storage account in your subscription, but provide a different location, you receive an error indicating the storage account already exists in a different location.</span></span> <span data-ttu-id="0e874-216">Var olan depolama hesabını silmek ya da var olan depolama hesabı ile aynı konumda sağlayın.</span><span class="sxs-lookup"><span data-stu-id="0e874-216">Either delete the existing storage account, or provide the same location as the existing storage account.</span></span>

## <a name="accountnameinvalid"></a><span data-ttu-id="0e874-217">AccountNameInvalid</span><span class="sxs-lookup"><span data-stu-id="0e874-217">AccountNameInvalid</span></span>
<span data-ttu-id="0e874-218">Gördüğünüz **AccountNameInvalid** yasaklanmış karakterleri içeren bir adı bir depolama hesabı verin girişimi sırasında hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="0e874-218">You see the **AccountNameInvalid** error when attempting to give a storage account a name that includes prohibited characters.</span></span> <span data-ttu-id="0e874-219">Depolama hesabı adları 3 ile 24 karakter uzunluğunda olmalıdır ve rakamlar ve yalnızca küçük harfler kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0e874-219">Storage account names must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span></span> <span data-ttu-id="0e874-220">[UniqueString](resource-group-template-functions-string.md#uniquestring) işlevi 13 karakter döndürür.</span><span class="sxs-lookup"><span data-stu-id="0e874-220">The [uniqueString](resource-group-template-functions-string.md#uniquestring) function returns 13 characters.</span></span> <span data-ttu-id="0e874-221">Bir önek birleştirmek, **uniqueString** neden, 11 karakterdir bir önek sağlayın veya daha az.</span><span class="sxs-lookup"><span data-stu-id="0e874-221">If you concatenate a prefix to the **uniqueString** result, provide a prefix that is 11 characters or less.</span></span>

## <a name="badrequest"></a><span data-ttu-id="0e874-222">BadRequest</span><span class="sxs-lookup"><span data-stu-id="0e874-222">BadRequest</span></span>

<span data-ttu-id="0e874-223">Özelliği için geçersiz bir değer sağlarsanız, bir BadRequest durum karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e874-223">You may encounter a BadRequest status when you provide an invalid value for a property.</span></span> <span data-ttu-id="0e874-224">Örneğin, bir depolama hesabı için hatalı bir SKU değer sağlarsanız, dağıtım başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="0e874-224">For example, if you provide an incorrect SKU value for a storage account, the deployment fails.</span></span> <span data-ttu-id="0e874-225">Özellik için geçerli değerler belirlemek için bakmak [REST API](/rest/api) dağıttığınız kaynak türü için.</span><span class="sxs-lookup"><span data-stu-id="0e874-225">To determine valid values for property, look at the [REST API](/rest/api) for the resource type you are deploying.</span></span>

<a id="noregisteredproviderfound" />

## <a name="noregisteredproviderfound-and-missingsubscriptionregistration"></a><span data-ttu-id="0e874-226">NoRegisteredProviderFound ve MissingSubscriptionRegistration</span><span class="sxs-lookup"><span data-stu-id="0e874-226">NoRegisteredProviderFound and MissingSubscriptionRegistration</span></span>
<span data-ttu-id="0e874-227">Kaynak dağıtırken şu hata kodu ve ileti alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0e874-227">When deploying resource, you may receive the following error code and message:</span></span>

```
Code: NoRegisteredProviderFound
Message: No registered resource provider found for location {location}
and API version {api-version} for type {resource-type}.
```

<span data-ttu-id="0e874-228">Veya bildiren benzer bir ileti alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0e874-228">Or, you may receive a similar message that states:</span></span>

```
Code: MissingSubscriptionRegistration
Message: The subscription is not registered to use namespace {resource-provider-namespace}
```

<span data-ttu-id="0e874-229">Üç nedenden biri için bu hataları alırsınız:</span><span class="sxs-lookup"><span data-stu-id="0e874-229">You receive these errors for one of three reasons:</span></span>

1. <span data-ttu-id="0e874-230">Kaynak sağlayıcısı, aboneliğiniz için kayıtlı değil</span><span class="sxs-lookup"><span data-stu-id="0e874-230">The resource provider has not been registered for your subscription</span></span>
2. <span data-ttu-id="0e874-231">API sürümü kaynak türü için desteklenmiyor</span><span class="sxs-lookup"><span data-stu-id="0e874-231">API version not supported for the resource type</span></span>
3. <span data-ttu-id="0e874-232">Kaynak türü için desteklenmeyen konumu</span><span class="sxs-lookup"><span data-stu-id="0e874-232">Location not supported for the resource type</span></span>

<span data-ttu-id="0e874-233">Hata iletisi desteklenen konumlar ve API sürümleri için öneriler vermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="0e874-233">The error message should give you suggestions for the supported locations and API versions.</span></span> <span data-ttu-id="0e874-234">Şablonunuzu önerilen değerlerden birine değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e874-234">You can change your template to one of the suggested values.</span></span> <span data-ttu-id="0e874-235">Azure portal ya da kullandığınız komut satırı arabirimi tarafından otomatik olarak kayıtlı ancak tüm çoğu sağlayıcıları.</span><span class="sxs-lookup"><span data-stu-id="0e874-235">Most providers are registered automatically by the Azure portal or the command-line interface you are using, but not all.</span></span> <span data-ttu-id="0e874-236">Belirli kaynak sağlayıcısı önce kullanmadıysanız, bu sağlayıcıyı kaydetmeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="0e874-236">If you have not used a particular resource provider before, you may need to register that provider.</span></span> <span data-ttu-id="0e874-237">PowerShell veya Azure CLI aracılığıyla kaynak sağlayıcıları hakkında daha fazla bulabilir.</span><span class="sxs-lookup"><span data-stu-id="0e874-237">You can discover more about resource providers through PowerShell or Azure CLI.</span></span>

<span data-ttu-id="0e874-238">**Portal**</span><span class="sxs-lookup"><span data-stu-id="0e874-238">**Portal**</span></span>

<span data-ttu-id="0e874-239">Kayıt durumunu görmek ve bir kaynak sağlayıcısı ad alanı Portalı aracılığıyla kaydedin.</span><span class="sxs-lookup"><span data-stu-id="0e874-239">You can see the registration status and register a resource provider namespace through the portal.</span></span>

1. <span data-ttu-id="0e874-240">Aboneliğiniz için seçin **kaynak sağlayıcıları**.</span><span class="sxs-lookup"><span data-stu-id="0e874-240">For your subscription, select **Resource providers**.</span></span>

   ![kaynak sağlayıcıları seç](./media/resource-manager-common-deployment-errors/select-resource-provider.png)

2. <span data-ttu-id="0e874-242">Kaynak sağlayıcıları listesi bakın ve gerekiyorsa, seçin **kaydetmek** kayıt kaynak sağlayıcısı dağıtmaya çalıştığınız türü için bağlantı.</span><span class="sxs-lookup"><span data-stu-id="0e874-242">Look at the list of resource providers, and if necessary, select the **Register** link to register the resource provider of the type you are trying to deploy.</span></span>

   ![kaynak sağlayıcıları Listele](./media/resource-manager-common-deployment-errors/list-resource-providers.png)

<span data-ttu-id="0e874-244">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="0e874-244">**PowerShell**</span></span>

<span data-ttu-id="0e874-245">Kayıt durumunu görmek için **Get-AzureRmResourceProvider**.</span><span class="sxs-lookup"><span data-stu-id="0e874-245">To see your registration status, use **Get-AzureRmResourceProvider**.</span></span>

```powershell
Get-AzureRmResourceProvider -ListAvailable
```

<span data-ttu-id="0e874-246">Bir sağlayıcı kaydetmek için kullanın **Register-AzureRmResourceProvider** ve kaydetmek istediğiniz kaynak sağlayıcısının adını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="0e874-246">To register a provider, use **Register-AzureRmResourceProvider** and provide the name of the resource provider you wish to register.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Cdn
```

<span data-ttu-id="0e874-247">Belirli bir kaynak türü için desteklenen konumlardan almak için kullanın:</span><span class="sxs-lookup"><span data-stu-id="0e874-247">To get the supported locations for a particular type of resource, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

<span data-ttu-id="0e874-248">Belirli bir kaynak türü için desteklenen API sürümleri almak için kullanın:</span><span class="sxs-lookup"><span data-stu-id="0e874-248">To get the supported API versions for a particular type of resource, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).ApiVersions
```

<span data-ttu-id="0e874-249">**Azure CLI**</span><span class="sxs-lookup"><span data-stu-id="0e874-249">**Azure CLI**</span></span>

<span data-ttu-id="0e874-250">Sağlayıcı kayıtlı olup olmadığını görmek için `azure provider list` komutu.</span><span class="sxs-lookup"><span data-stu-id="0e874-250">To see whether the provider is registered, use the `azure provider list` command.</span></span>

```azurecli
az provider list
```

<span data-ttu-id="0e874-251">Bir kaynak sağlayıcısı kaydetmek için kullanın `azure provider register` komut ve belirtin *ad alanı* kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="0e874-251">To register a resource provider, use the `azure provider register` command, and specify the *namespace* to register.</span></span>

```azurecli
az provider register --namespace Microsoft.Cdn
```

<span data-ttu-id="0e874-252">Desteklenen konumlar ve bir kaynak türü için API sürümlerini görmek için kullanın:</span><span class="sxs-lookup"><span data-stu-id="0e874-252">To see the supported locations and API versions for a resource type, use:</span></span>

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

<a id="quotaexceeded" />

## <a name="quotaexceeded-and-operationnotallowed"></a><span data-ttu-id="0e874-253">QuotaExceeded ve OperationNotAllowed</span><span class="sxs-lookup"><span data-stu-id="0e874-253">QuotaExceeded and OperationNotAllowed</span></span>
<span data-ttu-id="0e874-254">Dağıtım kaynak grubu, abonelikler, hesapları ve diğer kapsamları olabilecek bir kota aştığında sorunları olabilir.</span><span class="sxs-lookup"><span data-stu-id="0e874-254">You might have issues when deployment exceeds a quota, which could be per resource group, subscriptions, accounts, and other scopes.</span></span> <span data-ttu-id="0e874-255">Örneğin, aboneliğinizi bir bölge için çekirdek sayısını sınırlamak için yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="0e874-255">For example, your subscription may be configured to limit the number of cores for a region.</span></span> <span data-ttu-id="0e874-256">İzin verilen miktardan daha fazla çekirdeğe sahip bir sanal makineyi dağıtma girişiminde, kota aşıldı bildiren bir hata alırsınız.</span><span class="sxs-lookup"><span data-stu-id="0e874-256">If you attempt to deploy a virtual machine with more cores than the permitted amount, you receive an error stating the quota has been exceeded.</span></span>
<span data-ttu-id="0e874-257">Tam kota bilgi için bkz: [Azure aboneliği ve hizmet sınırları, kotaları ve kısıtlamaları](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="0e874-257">For complete quota information, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="0e874-258">Aboneliğinizin kotaları çekirdekleri incelemek için kullanabileceğiniz `azure vm list-usage` Azure CLI komutu.</span><span class="sxs-lookup"><span data-stu-id="0e874-258">To examine your subscription's quotas for cores, you can use the `azure vm list-usage` command in the Azure CLI.</span></span> <span data-ttu-id="0e874-259">Aşağıdaki örnek, ücretsiz bir deneme hesabı için çekirdek kota 4 olduğunu gösterir:</span><span class="sxs-lookup"><span data-stu-id="0e874-259">The following example illustrates that the core quota for a free trial account is 4:</span></span>

```azurecli
az vm list-usage --location "South Central US"
```

<span data-ttu-id="0e874-260">Hangi döndürür:</span><span class="sxs-lookup"><span data-stu-id="0e874-260">Which returns:</span></span>

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

<span data-ttu-id="0e874-261">Batı ABD bölgesinde dörtten fazla çekirdek oluşturan bir şablonu dağıtmak, benzer bir dağıtım hatası alırsınız:</span><span class="sxs-lookup"><span data-stu-id="0e874-261">If you deploy a template that creates more than four cores in the West US region, you get a deployment error that looks like:</span></span>

```
Code=OperationNotAllowed
Message=Operation results in exceeding quota limits of Core.
Maximum allowed: 4, Current in use: 4, Additional requested: 2.
```

<span data-ttu-id="0e874-262">Veya PowerShell içinde kullandığınız **Get-AzureRmVMUsage** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="0e874-262">Or in PowerShell, you can use the **Get-AzureRmVMUsage** cmdlet.</span></span>

```powershell
Get-AzureRmVMUsage
```

<span data-ttu-id="0e874-263">Hangi döndürür:</span><span class="sxs-lookup"><span data-stu-id="0e874-263">Which returns:</span></span>

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

<span data-ttu-id="0e874-264">Bu durumlarda, Portalı'na gidin ve dağıtmak istediğiniz bölgeyi için kotayı artırmak için bir destek sorununu dosya gerekir.</span><span class="sxs-lookup"><span data-stu-id="0e874-264">In these cases, you should go to the portal and file a support issue to raise your quota for the region into which you want to deploy.</span></span>

> [!NOTE]
> <span data-ttu-id="0e874-265">Kaynak grupları için tüm abonelik için tek tek her bölge için kota olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="0e874-265">Remember that for resource groups, the quota is for each individual region, not for the entire subscription.</span></span> <span data-ttu-id="0e874-266">Batı ABD 30 çekirdeğini dağıtımı yapmanız gerekirse, Batı ABD 30 Resource Manager çekirdekleri yapmasını istemek zorunda.</span><span class="sxs-lookup"><span data-stu-id="0e874-266">If you need to deploy 30 cores in West US, you have to ask for 30 Resource Manager cores in West US.</span></span> <span data-ttu-id="0e874-267">Hangi bölgeleri hiçbirinde erişiminiz 30 çekirdek dağıtımı yapmanız gerekirse, tüm bölgelerde 30 Resource Manager çekirdekleri istemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="0e874-267">If you need to deploy 30 cores in any of the regions to which you have access, you should ask for 30 Resource Manager cores in all regions.</span></span>
>
>

## <a name="invalidcontentlink"></a><span data-ttu-id="0e874-268">InvalidContentLink</span><span class="sxs-lookup"><span data-stu-id="0e874-268">InvalidContentLink</span></span>
<span data-ttu-id="0e874-269">Ne zaman hata iletisini alıyorsunuz:</span><span class="sxs-lookup"><span data-stu-id="0e874-269">When you receive the error message:</span></span>

```
Code=InvalidContentLink
Message=Unable to download deployment content from ...
```

<span data-ttu-id="0e874-270">Büyük olasılıkla kullanılamıyor iç içe geçmiş bir şablon bağlantı denediniz.</span><span class="sxs-lookup"><span data-stu-id="0e874-270">You have most likely attempted to link to a nested template that is not available.</span></span> <span data-ttu-id="0e874-271">İç içe geçmiş şablon için sağladığınız URI kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="0e874-271">Double check the URI you provided for the nested template.</span></span> <span data-ttu-id="0e874-272">Şablon bir depolama hesabı varsa, URI erişilebilir olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="0e874-272">If the template exists in a storage account, make sure the URI is accessible.</span></span> <span data-ttu-id="0e874-273">Bir SAS belirteci geçmesi gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="0e874-273">You may need to pass a SAS token.</span></span> <span data-ttu-id="0e874-274">Daha fazla bilgi için bkz. [Azure Resource Manager ile bağlı şablonları kullanma](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="0e874-274">For more information, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>

## <a name="requestdisallowedbypolicy"></a><span data-ttu-id="0e874-275">RequestDisallowedByPolicy</span><span class="sxs-lookup"><span data-stu-id="0e874-275">RequestDisallowedByPolicy</span></span>
<span data-ttu-id="0e874-276">Aboneliğinizi dağıtımı sırasında gerçekleştirmeye eylem engelleyen bir kaynak İlkesi içerdiğinde bu hatayı alırsınız.</span><span class="sxs-lookup"><span data-stu-id="0e874-276">You receive this error when your subscription includes a resource policy that prevents an action you are trying to perform during deployment.</span></span> <span data-ttu-id="0e874-277">Hata iletisinde için ilke tanımlayıcısı arayın.</span><span class="sxs-lookup"><span data-stu-id="0e874-277">In the error message, look for the policy identifier.</span></span>

```
Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'
```

<span data-ttu-id="0e874-278">İçinde **PowerShell**, bu ilke tanımlayıcısı olarak sağlamak **kimliği** dağıtımınızı engellenen İlkesi hakkındaki ayrıntıları almak için parametre.</span><span class="sxs-lookup"><span data-stu-id="0e874-278">In **PowerShell**, provide that policy identifier as the **Id** parameter to retrieve details about the policy that blocked your deployment.</span></span>

```powershell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

<span data-ttu-id="0e874-279">İçinde **Azure CLI**, ilke tanımı adını sağlayın:</span><span class="sxs-lookup"><span data-stu-id="0e874-279">In **Azure CLI**, provide the name of the policy definition:</span></span>

```azurecli
az policy definition show --name regionPolicyAssignment
```

<span data-ttu-id="0e874-280">Daha fazla bilgi için aşağıdaki makalelere bakın:</span><span class="sxs-lookup"><span data-stu-id="0e874-280">For more information, see the following articles:</span></span>

- [<span data-ttu-id="0e874-281">RequestDisallowedByPolicy hatası</span><span class="sxs-lookup"><span data-stu-id="0e874-281">RequestDisallowedByPolicy error</span></span>](resource-manager-policy-requestdisallowedbypolicy-error.md)
- <span data-ttu-id="0e874-282">[Kaynakları yönetme ve erişimi denetlemek için ilke kullanma](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="0e874-282">[Use Policy to manage resources and control access](resource-manager-policy.md).</span></span>

## <a name="authorization-failed"></a><span data-ttu-id="0e874-283">Yetkilendirme başarısız oldu</span><span class="sxs-lookup"><span data-stu-id="0e874-283">Authorization failed</span></span>
<span data-ttu-id="0e874-284">Bu eylemleri gerçekleştirmek için erişim hesabı ya da hizmet sorumlusu kaynakları dağıtma denemesi sahip olmadığından, dağıtım sırasında bir hata alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e874-284">You may receive an error during deployment because the account or service principal attempting to deploy the resources does not have access to perform those actions.</span></span> <span data-ttu-id="0e874-285">Azure Active Directory sağlar veya hangi kimlikleri denetlemek için yöneticinize duyarlık önemli ölçüde ile hangi kaynaklara erişebilir.</span><span class="sxs-lookup"><span data-stu-id="0e874-285">Azure Active Directory enables you or your administrator to control which identities can access what resources with a great degree of precision.</span></span> <span data-ttu-id="0e874-286">Hesabınızı okuyucu rolüne atanırsa, örneğin, kaynakları oluşturmak mümkün değildir.</span><span class="sxs-lookup"><span data-stu-id="0e874-286">For example, if your account is assigned to the Reader role, you are not able to create resources.</span></span> <span data-ttu-id="0e874-287">Bu durumda, yetkilendirme başarısız olduğunu belirten bir hata iletisi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="0e874-287">In that case, you see an error message indicating that authorization failed.</span></span>

<span data-ttu-id="0e874-288">Rol tabanlı erişim denetimi hakkında daha fazla bilgi için bkz: [Azure rol tabanlı erişim denetimi](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="0e874-288">For more information about role-based access control, see [Azure Role-Based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="0e874-289">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0e874-289">Next steps</span></span>
* <span data-ttu-id="0e874-290">Eylemler denetleme hakkında bilgi edinmek için [denetim işlemleri Resource Manager ile](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="0e874-290">To learn about auditing actions, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="0e874-291">Dağıtım sırasında hataları belirlemek için Eylemler hakkında bilgi edinmek için [görüntülemek dağıtım işlemlerini](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="0e874-291">To learn about actions to determine the errors during deployment, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
