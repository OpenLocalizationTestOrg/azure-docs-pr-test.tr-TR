---
title: "Resource Manager şablonları oluşturmak için aaaBest uygulamalar | Microsoft Docs"
description: "Azure Resource Manager şablonlarınızı basitleştirmeye yönelik yönergeler verilmiştir."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 31b10deb-0183-47ce-a5ba-6d0ff2ae8ab3
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: tomfitz
ms.openlocfilehash: ec9bbe218c4f2c6a92ca44b5e9c9c71029e22151
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-creating-azure-resource-manager-templates"></a><span data-ttu-id="e93a6-103">Azure Resource Manager şablonları oluşturmak için en iyi uygulamalar</span><span class="sxs-lookup"><span data-stu-id="e93a6-103">Best practices for creating Azure Resource Manager templates</span></span>
<span data-ttu-id="e93a6-104">Bu yönergeleri, güvenilir ve kolay toouse olan Azure Resource Manager şablonları oluşturmanıza yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="e93a6-104">These guidelines can help you create Azure Resource Manager templates that are reliable and easy toouse.</span></span> <span data-ttu-id="e93a6-105">Merhaba, yalnızca önerileri yönergelerdir.</span><span class="sxs-lookup"><span data-stu-id="e93a6-105">hello guidelines are only suggestions.</span></span> <span data-ttu-id="e93a6-106">Bunlar belirtilenler dışında gereksinimleri değildir.</span><span class="sxs-lookup"><span data-stu-id="e93a6-106">They are not requirements, except where noted.</span></span> <span data-ttu-id="e93a6-107">Senaryonuz hello birini çeşitlemesi gerektirebilir yaklaşımlar ve örnekler aşağıdaki.</span><span class="sxs-lookup"><span data-stu-id="e93a6-107">Your scenario might require a variation of one of hello following approaches or examples.</span></span>

## <a name="resource-names"></a><span data-ttu-id="e93a6-108">Kaynak adları</span><span class="sxs-lookup"><span data-stu-id="e93a6-108">Resource names</span></span>
<span data-ttu-id="e93a6-109">Genellikle, kaynak adları Kaynak Yöneticisi'nde üç türleri ile çalışır:</span><span class="sxs-lookup"><span data-stu-id="e93a6-109">Generally, you work with three types of resource names in Resource Manager:</span></span>

* <span data-ttu-id="e93a6-110">Kaynak adları benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e93a6-110">Resource names that must be unique.</span></span>
* <span data-ttu-id="e93a6-111">Toobe benzersiz olmayan kaynak adları gerekli, ancak tooprovide yardımcı olabilecek bir ad belirlemek bağlamına dayalı bir kaynak seçin.</span><span class="sxs-lookup"><span data-stu-id="e93a6-111">Resource names that are not required toobe unique, but you choose tooprovide a name that can help you identify a resource based on context.</span></span>
* <span data-ttu-id="e93a6-112">Genel kaynak adları.</span><span class="sxs-lookup"><span data-stu-id="e93a6-112">Resource names that can be generic.</span></span>

 <span data-ttu-id="e93a6-113">Kaynak adı kısıtlamaları hakkında daha fazla bilgi için bkz: [Azure kaynakları için adlandırma kurallarını önerilen](../guidance/guidance-naming-conventions.md).</span><span class="sxs-lookup"><span data-stu-id="e93a6-113">For information about resource name restrictions, see [Recommended naming conventions for Azure resources](../guidance/guidance-naming-conventions.md).</span></span>

### <a name="unique-resource-names"></a><span data-ttu-id="e93a6-114">Benzersiz kaynak adları</span><span class="sxs-lookup"><span data-stu-id="e93a6-114">Unique resource names</span></span>
<span data-ttu-id="e93a6-115">Veri erişim uç noktası olan herhangi bir kaynak türü için bir benzersiz kaynak adı sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e93a6-115">You must provide a unique resource name for any resource type that has a data access endpoint.</span></span> <span data-ttu-id="e93a6-116">Benzersiz bir ad gerektiren bazı yaygın kaynak türleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="e93a6-116">Some common resource types that require a unique name include:</span></span>

* <span data-ttu-id="e93a6-117">Azure depolama<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="e93a6-117">Azure Storage<sup>1</sup></span></span> 
* <span data-ttu-id="e93a6-118">Azure Uygulama Hizmeti’nin Web Apps özelliği</span><span class="sxs-lookup"><span data-stu-id="e93a6-118">Web Apps feature of Azure App Service</span></span>
* <span data-ttu-id="e93a6-119">SQL Server</span><span class="sxs-lookup"><span data-stu-id="e93a6-119">SQL Server</span></span>
* <span data-ttu-id="e93a6-120">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="e93a6-120">Azure Key Vault</span></span>
* <span data-ttu-id="e93a6-121">Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="e93a6-121">Azure Redis Cache</span></span>
* <span data-ttu-id="e93a6-122">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="e93a6-122">Azure Batch</span></span>
* <span data-ttu-id="e93a6-123">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="e93a6-123">Azure Traffic Manager</span></span>
* <span data-ttu-id="e93a6-124">Azure Search</span><span class="sxs-lookup"><span data-stu-id="e93a6-124">Azure Search</span></span>
* <span data-ttu-id="e93a6-125">Azure Hdınsight</span><span class="sxs-lookup"><span data-stu-id="e93a6-125">Azure HDInsight</span></span>

<span data-ttu-id="e93a6-126"><sup>1</sup> depolama hesabı adları de küçük olmalıdır, 24 karakter veya daha az ve tire sahip değil.</span><span class="sxs-lookup"><span data-stu-id="e93a6-126"><sup>1</sup> Storage account names also must be lowercase, 24 characters or less, and not have any hyphens.</span></span>

<span data-ttu-id="e93a6-127">Bir parametre için bir kaynak adı sağlarsanız, hello kaynak dağıttığınızda benzersiz bir ad sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e93a6-127">If you provide a parameter for a resource name, you must provide a unique name when you deploy hello resource.</span></span> <span data-ttu-id="e93a6-128">İsteğe bağlı olarak, hello kullanan bir değişken oluşturabilirsiniz [uniqueString()](resource-group-template-functions-string.md#uniquestring) toogenerate bir ad işlev.</span><span class="sxs-lookup"><span data-stu-id="e93a6-128">Optionally, you can create a variable that uses hello [uniqueString()](resource-group-template-functions-string.md#uniquestring) function toogenerate a name.</span></span> 

<span data-ttu-id="e93a6-129">Ayrıca olabilir veya tooadd bir önek istediğiniz toohello soneki **uniqueString** sonucu.</span><span class="sxs-lookup"><span data-stu-id="e93a6-129">You also might want tooadd a prefix or suffix toohello **uniqueString** result.</span></span> <span data-ttu-id="e93a6-130">Değiştirme hello benzersiz bir ad daha fazla kolayca hello kaynak türü hello adından belirlemenize yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="e93a6-130">Modifying hello unique name can help you more easily identify hello resource type from hello name.</span></span> <span data-ttu-id="e93a6-131">Örneğin, değişkeni aşağıdaki hello kullanarak bir depolama hesabı için benzersiz bir ad oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e93a6-131">For example, you can generate a unique name for a storage account by using hello following variable:</span></span>

```json
"variables": {
    "storageAccountName": "[concat(uniqueString(resourceGroup().id),'storage')]"
}
```

### <a name="resource-names-for-identification"></a><span data-ttu-id="e93a6-132">Tanımlama için kaynak adları</span><span class="sxs-lookup"><span data-stu-id="e93a6-132">Resource names for identification</span></span>
<span data-ttu-id="e93a6-133">Bazı kaynak türleri tooname isteyebilirsiniz, ancak adları benzersiz toobe sahip değil.</span><span class="sxs-lookup"><span data-stu-id="e93a6-133">Some resource types you might want tooname, but their names do not have toobe unique.</span></span> <span data-ttu-id="e93a6-134">Bu kaynak türleri için hello kaynak bağlamını ve hello kaynak türünü tanımlayan bir ad sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e93a6-134">For these resource types, you can provide a name that identifies both hello resource context and hello resource type.</span></span> <span data-ttu-id="e93a6-135">Merhaba kaynak kaynakların bir listesinde tanımanıza yardımcı olacak açıklayıcı bir ad sağlayın.</span><span class="sxs-lookup"><span data-stu-id="e93a6-135">Provide a descriptive name that helps you identify hello resource in a list of resources.</span></span> <span data-ttu-id="e93a6-136">Toouse farklı bir kaynak adı farklı dağıtımlar için gerekiyorsa, bir parametre için hello adı kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e93a6-136">If you need toouse a different resource name for different deployments, you can use a parameter for hello name:</span></span>

```json
"parameters": {
    "vmName": { 
        "type": "string",
        "defaultValue": "demoLinuxVM",
        "metadata": {
            "description": "hello name of hello VM toocreate."
        }
    }
}
```

<span data-ttu-id="e93a6-137">Dağıtım sırasında bir ad toopass ihtiyacınız yoksa, bir değişkeni kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e93a6-137">If you do not need toopass in a name during deployment, you can use a variable:</span></span> 

```json
"variables": {
    "vmName": "demoLinuxVM"
}
```

<span data-ttu-id="e93a6-138">Bir sabit kodlu değer de kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e93a6-138">You also can use a hard-coded value:</span></span>

```json
{
  "type": "Microsoft.Compute/virtualMachines",
  "name": "demoLinuxVM",
  ...
}
```

### <a name="generic-resource-names"></a><span data-ttu-id="e93a6-139">Genel kaynak adları</span><span class="sxs-lookup"><span data-stu-id="e93a6-139">Generic resource names</span></span>
<span data-ttu-id="e93a6-140">Farklı bir kaynak çoğunlukla erişim kaynak türleri için hello şablonu sabit kodlanmış olan bir ad kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e93a6-140">For resource types that you mostly access through a different resource, you can use a generic name that is hard-coded in hello template.</span></span> <span data-ttu-id="e93a6-141">Örneğin, bir SQL Server'da Güvenlik duvarı kuralları için standart, genel bir ad ayarlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e93a6-141">For example, you can set a standard, generic name for firewall rules on a SQL server:</span></span>

```json
{
    "type": "firewallrules",
    "name": "AllowAllWindowsAzureIps",
    ...
}
```

## <a name="parameters"></a><span data-ttu-id="e93a6-142">Parametreler</span><span class="sxs-lookup"><span data-stu-id="e93a6-142">Parameters</span></span>
<span data-ttu-id="e93a6-143">parametrelerle çalışırken hello aşağıdaki bilgiler yararlı olabilir:</span><span class="sxs-lookup"><span data-stu-id="e93a6-143">hello following information can be helpful when you work with parameters:</span></span>

* <span data-ttu-id="e93a6-144">Parametreleri kullanımını en aza indirin.</span><span class="sxs-lookup"><span data-stu-id="e93a6-144">Minimize your use of parameters.</span></span> <span data-ttu-id="e93a6-145">Mümkün olduğunda, bir değişkeni veya hazır değer kullanın.</span><span class="sxs-lookup"><span data-stu-id="e93a6-145">Whenever possible, use a variable or a literal value.</span></span> <span data-ttu-id="e93a6-146">Parametreleri için yalnızca bu senaryoları kullanın:</span><span class="sxs-lookup"><span data-stu-id="e93a6-146">Use parameters only for these scenarios:</span></span>
   
   * <span data-ttu-id="e93a6-147">Tooenvironment (SKU, boyut, Kapasite) according, toouse Çeşitlemeler istediğiniz ayarları.</span><span class="sxs-lookup"><span data-stu-id="e93a6-147">Settings that you want toouse variations of according tooenvironment (SKU, size, capacity).</span></span>
   * <span data-ttu-id="e93a6-148">Kaynak adları için kolay bir şekilde tanımlanması toospecify istiyor.</span><span class="sxs-lookup"><span data-stu-id="e93a6-148">Resource names that you want toospecify for easy identification.</span></span>
   * <span data-ttu-id="e93a6-149">Değerleri toocomplete sık diğer görevleri (örneğin, bir yönetici kullanıcı adı) kullanın.</span><span class="sxs-lookup"><span data-stu-id="e93a6-149">Values that you use frequently toocomplete other tasks (such as an admin user name).</span></span>
   * <span data-ttu-id="e93a6-150">Gizli (parolalar gibi).</span><span class="sxs-lookup"><span data-stu-id="e93a6-150">Secrets (such as passwords).</span></span>
   * <span data-ttu-id="e93a6-151">Merhaba numarası veya bir kaynak türü birden çok örneğini oluşturduğunuzda değerleri toouse dizisi.</span><span class="sxs-lookup"><span data-stu-id="e93a6-151">hello number or array of values toouse when you create multiple instances of a resource type.</span></span>
* <span data-ttu-id="e93a6-152">Ortası büyük parametre adları için kullanın.</span><span class="sxs-lookup"><span data-stu-id="e93a6-152">Use camel case for parameter names.</span></span>
* <span data-ttu-id="e93a6-153">Her parametre hello meta verilerindeki bir açıklama belirtin:</span><span class="sxs-lookup"><span data-stu-id="e93a6-153">Provide a description of every parameter in hello metadata:</span></span>

   ```json
   "parameters": {
       "storageAccountType": {
           "type": "string",
           "metadata": {
               "description": "hello type of hello new storage account created toostore hello VM disks."
           }
       }
   }
   ```

* <span data-ttu-id="e93a6-154">(Dışında parolalar ve SSH anahtarları) parametrelerinin varsayılan değerleri tanımlayın:</span><span class="sxs-lookup"><span data-stu-id="e93a6-154">Define default values for parameters (except for passwords and SSH keys):</span></span>
   
   ```json
   "parameters": {
        "storageAccountType": {
            "type": "string",
            "defaultValue": "Standard_GRS",
            "metadata": {
                "description": "hello type of hello new storage account created toostore hello VM disks."
            }
        }
   }
   ```

* <span data-ttu-id="e93a6-155">Kullanım **SecureString** tüm parolalar ve gizli anahtarları için:</span><span class="sxs-lookup"><span data-stu-id="e93a6-155">Use **SecureString** for all passwords and secrets:</span></span> 
   
   ```json
   "parameters": {
       "secretValue": {
           "type": "securestring",
           "metadata": {
               "description": "hello value of hello secret toostore in hello vault."
           }
       }
   }
   ```

* <span data-ttu-id="e93a6-156">Mümkün olduğunda, bir parametre toospecify konumu kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="e93a6-156">Whenever possible, don't use a parameter toospecify location.</span></span> <span data-ttu-id="e93a6-157">Bunun yerine, hello kullanın **konumu** hello kaynak grubunun özelliği.</span><span class="sxs-lookup"><span data-stu-id="e93a6-157">Instead, use hello **location** property of hello resource group.</span></span> <span data-ttu-id="e93a6-158">Hello kullanarak **resourceGroup () .location** ifade tüm kaynaklarınız için hello şablon kaynaklarında içinde dağıtılan hello hello kaynak grubu ile aynı konumda:</span><span class="sxs-lookup"><span data-stu-id="e93a6-158">By using hello **resourceGroup().location** expression for all your resources, resources in hello template are deployed in hello same location as hello resource group:</span></span>
   
   ```json
   "resources": [
     {
         "name": "[variables('storageAccountName')]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         ...
     }
   ]
   ```
   
   <span data-ttu-id="e93a6-159">Bir kaynak türü konumları, yalnızca sınırlı sayıda destekleniyorsa, toospecify geçerli bir konum hello şablonu doğrudan isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e93a6-159">If a resource type is supported in only a limited number of locations, you might want toospecify a valid location directly in hello template.</span></span> <span data-ttu-id="e93a6-160">Kullanmanız gerekiyorsa bir **konumu** parametresi mümkün olduğunca Bu parametre değeri Merhaba, büyük olasılıkla toobe kaynakları paylaşmak aynı konumu.</span><span class="sxs-lookup"><span data-stu-id="e93a6-160">If you must use a **location** parameter, share that parameter value as much as possible with resources that are likely toobe in hello same location.</span></span> <span data-ttu-id="e93a6-161">Bu kullanıcılar tooprovide konum bilgileri sorulur hello sayı en aza indirir.</span><span class="sxs-lookup"><span data-stu-id="e93a6-161">This minimizes hello number of times users are asked tooprovide location information.</span></span>
* <span data-ttu-id="e93a6-162">Bir kaynak türü için hello API sürümü için bir parametre veya değişken kullanmaktan kaçının.</span><span class="sxs-lookup"><span data-stu-id="e93a6-162">Avoid using a parameter or variable for hello API version for a resource type.</span></span> <span data-ttu-id="e93a6-163">Kaynak özellikleri ve değerlerini sürüm numarasına göre farklılık gösterebilir.</span><span class="sxs-lookup"><span data-stu-id="e93a6-163">Resource properties and values can vary by version number.</span></span> <span data-ttu-id="e93a6-164">Merhaba API sürümü tooa parametre veya değişken ayarlandığında bir kod düzenleyicisinde IntelliSense hello doğru şemayı belirleyemiyor.</span><span class="sxs-lookup"><span data-stu-id="e93a6-164">IntelliSense in a code editor cannot determine hello correct schema when hello API version is set tooa parameter or variable.</span></span> <span data-ttu-id="e93a6-165">Bunun yerine, sabit kodlu hello hello şablonunda API sürümü.</span><span class="sxs-lookup"><span data-stu-id="e93a6-165">Instead, hard-code hello API version in hello template.</span></span>

## <a name="variables"></a><span data-ttu-id="e93a6-166">Değişkenler</span><span class="sxs-lookup"><span data-stu-id="e93a6-166">Variables</span></span>
<span data-ttu-id="e93a6-167">değişkenlerle çalışırken hello aşağıdaki bilgiler yararlı olabilir:</span><span class="sxs-lookup"><span data-stu-id="e93a6-167">hello following information can be helpful when you work with variables:</span></span>

* <span data-ttu-id="e93a6-168">Toouse birden çok kez bir şablon ihtiyacınız olduğunu değerleri için değişkenlerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="e93a6-168">Use variables for values that you need toouse more than once in a template.</span></span> <span data-ttu-id="e93a6-169">Bir değer yalnızca bir kez kullanılır, sabit kodlanmış bir değer, şablonu daha kolay tooread yapar.</span><span class="sxs-lookup"><span data-stu-id="e93a6-169">If a value is used only once, a hard-coded value makes your template easier tooread.</span></span>
* <span data-ttu-id="e93a6-170">Merhaba kullanamazsınız [başvuru](resource-group-template-functions-resource.md#reference) hello işlevinde **değişkenleri** hello şablonu bölümü.</span><span class="sxs-lookup"><span data-stu-id="e93a6-170">You cannot use hello [reference](resource-group-template-functions-resource.md#reference) function in hello **variables** section of hello template.</span></span> <span data-ttu-id="e93a6-171">Merhaba **başvuru** işlevi hello kaynağın çalışma zamanı durumunu değerinden türetilir.</span><span class="sxs-lookup"><span data-stu-id="e93a6-171">hello **reference** function derives its value from hello resource's runtime state.</span></span> <span data-ttu-id="e93a6-172">Ancak, değişkenleri hello hello şablonunu ayrıştırma ilk sırasında çözümlenir.</span><span class="sxs-lookup"><span data-stu-id="e93a6-172">However, variables are resolved during hello initial parsing of hello template.</span></span> <span data-ttu-id="e93a6-173">Merhaba gereken değerleri oluşturmak **başvuru** hello doğrudan işlevinde **kaynakları** veya **çıkarır** hello şablonu bölümü.</span><span class="sxs-lookup"><span data-stu-id="e93a6-173">Construct values that need hello **reference** function directly in hello **resources** or **outputs** section of hello template.</span></span>
* <span data-ttu-id="e93a6-174">Bölümünde açıklandığı gibi benzersiz kaynak adları için değişkenleri dahil [kaynak adları](#resource-names).</span><span class="sxs-lookup"><span data-stu-id="e93a6-174">Include variables for resource names that must be unique, as described in [Resource names](#resource-names).</span></span>
* <span data-ttu-id="e93a6-175">Değişkenleri karmaşık nesneleri gruplayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e93a6-175">You can group variables into complex objects.</span></span> <span data-ttu-id="e93a6-176">Kullanım hello **variable.subentry** tooreference karmaşık bir nesne arasında bir değer biçimlendirin.</span><span class="sxs-lookup"><span data-stu-id="e93a6-176">Use hello **variable.subentry** format tooreference a value from a complex object.</span></span> <span data-ttu-id="e93a6-177">Değişkenleri gruplandırma ilgili değişkenleri izlemenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="e93a6-177">Grouping variables can help you track related variables.</span></span> <span data-ttu-id="e93a6-178">Ayrıca, hello şablon okunabilirliğini artırır.</span><span class="sxs-lookup"><span data-stu-id="e93a6-178">It also improves readability of hello template.</span></span> <span data-ttu-id="e93a6-179">Örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="e93a6-179">Here's an example:</span></span>
   
   ```json
   "variables": {
       "storage": {
           "name": "[concat(uniqueString(resourceGroup().id),'storage')]",
           "type": "Standard_LRS"
       }
   },
   "resources": [
     {
         "type": "Microsoft.Storage/storageAccounts",
         "name": "[variables('storage').name]",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         "sku": {
             "name": "[variables('storage').type]"
         },
         ...
     }
   ]
   ```
   
   > [!NOTE]
   > <span data-ttu-id="e93a6-180">Karmaşık bir nesne değeri karmaşık bir nesneden başvuran bir ifade içeremez.</span><span class="sxs-lookup"><span data-stu-id="e93a6-180">A complex object cannot contain an expression that references a value from a complex object.</span></span> <span data-ttu-id="e93a6-181">Bu amaç için ayrı bir değişken tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="e93a6-181">Define a separate variable for this purpose.</span></span>
   > 
   > 
   
     <span data-ttu-id="e93a6-182">Karmaşık nesne değişkenleri olarak kullanarak gelişmiş örnekler için bkz: [paylaşmak Azure Resource Manager şablonları durumda](best-practices-resource-manager-state.md).</span><span class="sxs-lookup"><span data-stu-id="e93a6-182">For advanced examples of using complex objects as variables, see [Share state in Azure Resource Manager templates](best-practices-resource-manager-state.md).</span></span>

## <a name="resources"></a><span data-ttu-id="e93a6-183">Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="e93a6-183">Resources</span></span>
<span data-ttu-id="e93a6-184">kaynaklarla çalışırken hello aşağıdaki bilgiler yararlı olabilir:</span><span class="sxs-lookup"><span data-stu-id="e93a6-184">hello following information can be helpful when you work with resources:</span></span>

* <span data-ttu-id="e93a6-185">toohelp diğer katkıda bulunanlar hello kaynak hello amacı anlamak, belirtin **açıklamaları** hello şablonundaki her bir kaynak için:</span><span class="sxs-lookup"><span data-stu-id="e93a6-185">toohelp other contributors understand hello purpose of hello resource, specify **comments** for each resource in hello template:</span></span>
   
   ```json
   "resources": [
     {
         "name": "[variables('storageAccountName')]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         "comments": "This storage account is used toostore hello VM disks.",
         ...
     }
   ]
   ```

* <span data-ttu-id="e93a6-186">Etiketler tooadd meta veri tooresources kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e93a6-186">You can use tags tooadd metadata tooresources.</span></span> <span data-ttu-id="e93a6-187">Kaynaklarınızın hakkında meta veri tooadd bilgileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="e93a6-187">Use metadata tooadd information about your resources.</span></span> <span data-ttu-id="e93a6-188">Örneğin, bir kaynak için meta veri toorecord fatura ayrıntılarına ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e93a6-188">For example, you can add metadata toorecord billing details for a resource.</span></span> <span data-ttu-id="e93a6-189">Daha fazla bilgi için bkz: [kullanarak Azure kaynaklarınızı tooorganize etiketler](resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="e93a6-189">For more information, see [Using tags tooorganize your Azure resources](resource-group-using-tags.md).</span></span>
* <span data-ttu-id="e93a6-190">Kullanırsanız, bir *ortak uç nokta* şablonunuzda (örneğin, bir Azure Blob Depolama ortak uç nokta), *olmayan sabit kodlu* ad alanı hello.</span><span class="sxs-lookup"><span data-stu-id="e93a6-190">If you use a *public endpoint* in your template (such as an Azure Blob storage public endpoint), *do not hard-code* hello namespace.</span></span> <span data-ttu-id="e93a6-191">Kullanım hello **başvuru** işlevi toodynamically almak hello ad alanı.</span><span class="sxs-lookup"><span data-stu-id="e93a6-191">Use hello **reference** function toodynamically retrieve hello namespace.</span></span> <span data-ttu-id="e93a6-192">Bu yaklaşım toodeploy hello şablonu toodifferent genel ad alanı ortamlarında el ile Merhaba şablonunda hello endpoint değiştirmeden kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e93a6-192">You can use this approach toodeploy hello template toodifferent public namespace environments without manually changing hello endpoint in hello template.</span></span> <span data-ttu-id="e93a6-193">Ayarlama hello API sürümü toohello şablonunuzda hello depolama hesabı için kullandığınız aynı sürüm:</span><span class="sxs-lookup"><span data-stu-id="e93a6-193">Set hello API version toohello same version that you are using for hello storage account in your template:</span></span>
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   <span data-ttu-id="e93a6-194">Merhaba depolama hesabı hello dağıtılırsa oluşturmakta olduğunuz aynı şablonu gerektirmeyen toospecify hello sağlayıcı ad alanı hello kaynak başvurduğunuzda.</span><span class="sxs-lookup"><span data-stu-id="e93a6-194">If hello storage account is deployed in hello same template that you are creating, you do not need toospecify hello provider namespace when you reference hello resource.</span></span> <span data-ttu-id="e93a6-195">Basitleştirilmiş hello sözdizimi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="e93a6-195">This is hello simplified syntax:</span></span>
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(variables('storageAccountName'), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   <span data-ttu-id="e93a6-196">Yapılandırılmış toouse ortak bir ad alanı olan diğer değerleri şablonunuzda varsa, bu değerleri değiştirmek tooreflect hello aynı **başvuru** işlevi.</span><span class="sxs-lookup"><span data-stu-id="e93a6-196">If you have other values in your template that are configured toouse a public namespace, change these values tooreflect hello same **reference** function.</span></span> <span data-ttu-id="e93a6-197">Örneğin, hello ayarlayabilirsiniz **storageUri** hello sanal makine tanılama profili özelliği:</span><span class="sxs-lookup"><span data-stu-id="e93a6-197">For example, you can set hello **storageUri** property of hello virtual machine diagnostics profile:</span></span>
   
   ```json
   "diagnosticsProfile": {
       "bootDiagnostics": {
           "enabled": "true",
           "storageUri": "[reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob]"
       }
   }
   ```
   
   <span data-ttu-id="e93a6-198">Ayrıca, farklı kaynak grubunda bulunan mevcut bir depolama hesabını başvurabilir:</span><span class="sxs-lookup"><span data-stu-id="e93a6-198">You also can reference an existing storage account that is in a different resource group:</span></span>

   ```json
   "osDisk": {
       "name": "osdisk", 
       "vhd": {
           "uri":"[concat(reference(resourceId(parameters('existingResourceGroup'), 'Microsoft.Storage/storageAccounts/', parameters('existingStorageAccountName')), '2016-01-01').primaryEndpoints.blob,  variables('vmStorageAccountContainerName'), '/', variables('OSDiskName'),'.vhd')]"
       }
   }
   ```

* <span data-ttu-id="e93a6-199">Yalnızca bir uygulama gerektirdiğinde, ortak IP adresleri tooa sanal makine atayın.</span><span class="sxs-lookup"><span data-stu-id="e93a6-199">Assign public IP addresses tooa virtual machine only when an application requires it.</span></span> <span data-ttu-id="e93a6-200">hata ayıklama için ya da Yönetim veya yönetim amacıyla tooconnect tooa sanal makine (VM) gelen NAT kuralları, bir sanal ağ geçidi ya da bir jumpbox kullanın.</span><span class="sxs-lookup"><span data-stu-id="e93a6-200">tooconnect tooa virtual machine (VM) for debugging, or for management or administrative purposes, use inbound NAT rules, a virtual network gateway, or a jumpbox.</span></span>
   
     <span data-ttu-id="e93a6-201">Toovirtual makineler bağlanma hakkında daha fazla bilgi için bkz:</span><span class="sxs-lookup"><span data-stu-id="e93a6-201">For more information about connecting toovirtual machines, see:</span></span>
   
   * [<span data-ttu-id="e93a6-202">N katmanlı mimari Azure VM'ler çalıştırın</span><span class="sxs-lookup"><span data-stu-id="e93a6-202">Run VMs for an N-tier architecture in Azure</span></span>](../guidance/guidance-compute-n-tier-vm.md)
   * [<span data-ttu-id="e93a6-203">Azure Kaynak Yöneticisi'nde yer alan VM'ler için WinRM erişimini Ayarla</span><span class="sxs-lookup"><span data-stu-id="e93a6-203">Set up WinRM access for VMs in Azure Resource Manager</span></span>](../virtual-machines/windows/winrm.md)
   * [<span data-ttu-id="e93a6-204">Hello Azure portalını kullanarak dış erişim tooyour VM izin ver</span><span class="sxs-lookup"><span data-stu-id="e93a6-204">Allow external access tooyour VM by using hello Azure portal</span></span>](../virtual-machines/windows/nsg-quickstart-portal.md)
   * [<span data-ttu-id="e93a6-205">PowerShell kullanarak dış erişim tooyour VM izin ver</span><span class="sxs-lookup"><span data-stu-id="e93a6-205">Allow external access tooyour VM by using PowerShell</span></span>](../virtual-machines/windows/nsg-quickstart-powershell.md)
   * [<span data-ttu-id="e93a6-206">Azure CLI kullanarak dış erişim tooyour Linux VM izin ver</span><span class="sxs-lookup"><span data-stu-id="e93a6-206">Allow external access tooyour Linux VM by using Azure CLI</span></span>](../virtual-machines/virtual-machines-linux-nsg-quickstart.md)
* <span data-ttu-id="e93a6-207">Merhaba **domainNameLabel** özelliği genel IP adresleri için benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e93a6-207">hello **domainNameLabel** property for public IP addresses must be unique.</span></span> <span data-ttu-id="e93a6-208">Merhaba **domainNameLabel** değeri gerekir 3 ile 63 karakter uzunluğunda olmalıdır ve bu normal bir ifadeyle belirtilen hello kurallarına: `^[a-z][a-z0-9-]{1,61}[a-z0-9]$`.</span><span class="sxs-lookup"><span data-stu-id="e93a6-208">hello **domainNameLabel** value must be between 3 and 63 characters long, and follow hello rules specified by this regular expression: `^[a-z][a-z0-9-]{1,61}[a-z0-9]$`.</span></span> <span data-ttu-id="e93a6-209">Çünkü hello **uniqueString** işlevi hello 13 karakterden uzun olan bir dize oluşturur **dnsPrefixString** parametredir sınırlı too50 karakterler:</span><span class="sxs-lookup"><span data-stu-id="e93a6-209">Because hello **uniqueString** function generates a string that is 13 characters long, hello **dnsPrefixString** parameter is limited too50 characters:</span></span>

   ```json
   "parameters": {
       "dnsPrefixString": {
           "type": "string",
           "maxLength": 50,
           "metadata": {
               "description": "hello DNS label for hello public IP address. It must be lowercase. It should match hello following regular expression, or it will raise an error: ^[a-z][a-z0-9-]{1,61}[a-z0-9]$"
           }
       }
   },
   "variables": {
       "dnsPrefix": "[concat(parameters('dnsPrefixString'),uniquestring(resourceGroup().id))]"
   }
   ```

* <span data-ttu-id="e93a6-210">Bir parola tooa özel betik uzantısı eklediğinizde, hello kullan **commandToExecute** hello özelliğinde **protectedSettings** özelliği:</span><span class="sxs-lookup"><span data-stu-id="e93a6-210">When you add a password tooa custom script extension, use hello **commandToExecute** property in hello **protectedSettings** property:</span></span>
   
   ```json
   "properties": {
       "publisher": "Microsoft.Azure.Extensions",
       "type": "CustomScript",
       "typeHandlerVersion": "2.0",
       "autoUpgradeMinorVersion": true,
       "settings": {
           "fileUris": [
               "[concat(variables('template').assets, '/lamp-app/install_lamp.sh')]"
           ]
       },
       "protectedSettings": {
           "commandToExecute": "[concat('sh install_lamp.sh ', parameters('mySqlPassword'))]"
       }
   }
   ```
   
   > [!NOTE]
   > <span data-ttu-id="e93a6-211">gizli olan tooensure parametreleri tooVMs ve uzantıları geçirildiğinde şifrelenmiş hello kullan **protectedSettings** hello ilgili uzantılar özelliği.</span><span class="sxs-lookup"><span data-stu-id="e93a6-211">tooensure that secrets are encrypted when they are passed as parameters tooVMs and extensions, use hello **protectedSettings** property of hello relevant extensions.</span></span>
   > 
   > 

## <a name="outputs"></a><span data-ttu-id="e93a6-212">Çıkışları</span><span class="sxs-lookup"><span data-stu-id="e93a6-212">Outputs</span></span>
<span data-ttu-id="e93a6-213">Bir şablon toocreate ortak IP adresleri kullanıyorsanız dahil bir **çıkarır** başlangıç IP adresi ve hello tam etki alanı adı (FQDN) ayrıntılarını döndürür bölümü.</span><span class="sxs-lookup"><span data-stu-id="e93a6-213">If you use a template toocreate public IP addresses, include an **outputs** section that returns details of hello IP address and hello fully qualified domain name (FQDN).</span></span> <span data-ttu-id="e93a6-214">Dağıtımdan sonra çıktı değerleri tooeasily alma ayrıntılarını ortak IP adresleri ve FQDN'ler kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e93a6-214">You can use output values tooeasily retrieve details about public IP addresses and FQDNs after deployment.</span></span> <span data-ttu-id="e93a6-215">Merhaba kaynağa başvuran toocreate kullanılan hello API sürümü kullanın:</span><span class="sxs-lookup"><span data-stu-id="e93a6-215">When you reference hello resource, use hello API version that you used toocreate it:</span></span> 

```json
"outputs": {
    "fqdn": {
        "value": "[reference(resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName')), '2016-07-01').dnsSettings.fqdn]",
        "type": "string"
    },
    "ipaddress": {
        "value": "[reference(resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName')), '2016-07-01').ipAddress]",
        "type": "string"
    }
}
```

## <a name="single-template-vs-nested-templates"></a><span data-ttu-id="e93a6-216">İç içe geçmiş şablonları karşılaştırması tek şablonu</span><span class="sxs-lookup"><span data-stu-id="e93a6-216">Single template vs. nested templates</span></span>
<span data-ttu-id="e93a6-217">toodeploy, çözümünüzün birden çok iç içe geçmiş şablonları ile tek bir şablon ya da ana şablon kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e93a6-217">toodeploy your solution, you can use either a single template or a main template with multiple nested templates.</span></span> <span data-ttu-id="e93a6-218">İç içe geçmiş şablonları daha Gelişmiş senaryolar için yaygındır.</span><span class="sxs-lookup"><span data-stu-id="e93a6-218">Nested templates are common for more advanced scenarios.</span></span> <span data-ttu-id="e93a6-219">Avantajları aşağıdaki hello iç içe geçmiş şablonu verir kullanma:</span><span class="sxs-lookup"><span data-stu-id="e93a6-219">Using a nested template gives you hello following advantages:</span></span>

* <span data-ttu-id="e93a6-220">Bir çözüm hedeflenen bileşenlere aşağı bozulabilir.</span><span class="sxs-lookup"><span data-stu-id="e93a6-220">You can break down a solution into targeted components.</span></span>
* <span data-ttu-id="e93a6-221">Farklı ana şablonları ile iç içe geçmiş şablonlarını yeniden kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e93a6-221">You can reuse nested templates with different main templates.</span></span>

<span data-ttu-id="e93a6-222">İç içe geçmiş toouse şablonları seçerseniz, yönergeleri izleyerek hello şablon tasarımı standartlaştırmak yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="e93a6-222">If you choose toouse nested templates, hello following guidelines can help you standardize your template design.</span></span> <span data-ttu-id="e93a6-223">Bu yönergelere dayalı [Azure Resource Manager şablonları tasarlamak için desenleri](best-practices-resource-manager-design-templates.md).</span><span class="sxs-lookup"><span data-stu-id="e93a6-223">These guidelines are based on [patterns for designing Azure Resource Manager templates](best-practices-resource-manager-design-templates.md).</span></span> <span data-ttu-id="e93a6-224">Şablonları aşağıdaki hello sahip bir tasarım öneririz:</span><span class="sxs-lookup"><span data-stu-id="e93a6-224">We recommend a design that has hello following templates:</span></span>

* <span data-ttu-id="e93a6-225">**Ana şablon** (azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="e93a6-225">**Main template** (azuredeploy.json).</span></span> <span data-ttu-id="e93a6-226">Merhaba giriş parametreleri için kullanın.</span><span class="sxs-lookup"><span data-stu-id="e93a6-226">Use for hello input parameters.</span></span>
* <span data-ttu-id="e93a6-227">**Paylaşılan kaynaklar şablon**.</span><span class="sxs-lookup"><span data-stu-id="e93a6-227">**Shared resources template**.</span></span> <span data-ttu-id="e93a6-228">Kullanım toodeploy paylaşılan tüm diğer kaynakları kullanan kaynakları (örneğin, sanal ağ ve kullanılabilirlik kümeleri gibi).</span><span class="sxs-lookup"><span data-stu-id="e93a6-228">Use toodeploy shared resources that all other resources use (for example, virtual network and availability sets).</span></span> <span data-ttu-id="e93a6-229">Kullanım hello **dependsOn** ifade tooensure bu şablonu önce diğer şablonlar dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="e93a6-229">Use hello **dependsOn** expression tooensure that this template is deployed before other templates.</span></span>
* <span data-ttu-id="e93a6-230">**İsteğe bağlı kaynakları şablon**.</span><span class="sxs-lookup"><span data-stu-id="e93a6-230">**Optional resources template**.</span></span> <span data-ttu-id="e93a6-231">Kullanım tooconditionally bir parametre (örneğin, bir jumpbox) temel alarak kaynaklara dağıtın.</span><span class="sxs-lookup"><span data-stu-id="e93a6-231">Use tooconditionally deploy resources based on a parameter (for example, a jumpbox).</span></span>
* <span data-ttu-id="e93a6-232">**Üye kaynakları şablon**.</span><span class="sxs-lookup"><span data-stu-id="e93a6-232">**Member resources template**.</span></span> <span data-ttu-id="e93a6-233">Bir uygulama katmanı içindeki her örnek türü kendi yapılandırmasına sahip.</span><span class="sxs-lookup"><span data-stu-id="e93a6-233">Each instance type within an application tier has its own configuration.</span></span> <span data-ttu-id="e93a6-234">Bir katman içinde farklı bir örnek türleri tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e93a6-234">Within a tier, you can define different instance types.</span></span> <span data-ttu-id="e93a6-235">(Örneğin, bir küme hello ilk örneği oluşturur ve ek örnekler toohello varolan bir kümeye eklenir.) Her örneği türü kendi dağıtım şablonu yok.</span><span class="sxs-lookup"><span data-stu-id="e93a6-235">(For example, hello first instance creates a cluster, and additional instances are added toohello existing cluster.) Each instance type has its own deployment template.</span></span>
* <span data-ttu-id="e93a6-236">**Komut dosyaları**.</span><span class="sxs-lookup"><span data-stu-id="e93a6-236">**Scripts**.</span></span> <span data-ttu-id="e93a6-237">Yaygın olarak yeniden kullanılabilir komut dosyaları her örneği türü (örneğin, başlatma ve biçimi ek diskleri) için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="e93a6-237">Widely reusable scripts are applicable for each instance type (for example, initialize and format additional disks).</span></span> <span data-ttu-id="e93a6-238">Belirli özelleştirme amaçla oluşturduğunuz özel komut dosyaları hello örneği türüne göre farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="e93a6-238">Custom scripts that you create for a specific customization purpose are different, based on hello instance type.</span></span>

![İç içe geçmiş şablonu](./media/resource-manager-template-best-practices/nestedTemplateDesign.png)

<span data-ttu-id="e93a6-240">Daha fazla bilgi için bkz: [Azure Resource Manager ile bağlı şablonları kullanma](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="e93a6-240">For more information, see [Use linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>

## <a name="conditionally-link-toonested-templates"></a><span data-ttu-id="e93a6-241">Koşullu toonested şablonları bağlantı</span><span class="sxs-lookup"><span data-stu-id="e93a6-241">Conditionally link toonested templates</span></span>
<span data-ttu-id="e93a6-242">Bir parametre tooconditionally bağlantı toonested şablonları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e93a6-242">You can use a parameter tooconditionally link toonested templates.</span></span> <span data-ttu-id="e93a6-243">Merhaba parametre hello URI hello şablonunun parçası haline gelir:</span><span class="sxs-lookup"><span data-stu-id="e93a6-243">hello parameter becomes part of hello URI for hello template:</span></span>

```json
"parameters": {
    "newOrExisting": {
        "type": "String",
        "allowedValues": [
            "new",
            "existing"
        ]
    }
},
"variables": {
    "templatelink": "[concat('https://raw.githubusercontent.com/Contoso/Templates/master/',parameters('newOrExisting'),'StorageAccount.json')]"
},
"resources": [
    {
        "apiVersion": "2015-01-01",
        "name": "nestedTemplate",
        "type": "Microsoft.Resources/deployments",
        "properties": {
            "mode": "incremental",
            "templateLink": {
                "uri": "[variables('templatelink')]",
                "contentVersion": "1.0.0.0"
            },
            "parameters": {
            }
        }
    }
]
```

## <a name="template-format"></a><span data-ttu-id="e93a6-244">Şablon biçimi</span><span class="sxs-lookup"><span data-stu-id="e93a6-244">Template format</span></span>
<span data-ttu-id="e93a6-245">İyi bir uygulama toopass olan şablonunuzu JSON Doğrulayıcı aracılığıyla.</span><span class="sxs-lookup"><span data-stu-id="e93a6-245">It's a good practice toopass your template through a JSON validator.</span></span> <span data-ttu-id="e93a6-246">Bir doğrulayıcı yabancı virgül, parantez ve dağıtım sırasında bir hata neden olabilir parantezler kaldırmanıza yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="e93a6-246">A validator can help you remove extraneous commas, parentheses, and brackets that might cause an error during deployment.</span></span> <span data-ttu-id="e93a6-247">Deneyin [JSONLint](http://jsonlint.com/) veya sık kullanılan için linter paketi düzenleme ortamı (Visual Studio Code, Atom, Sublime metin, Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="e93a6-247">Try [JSONLint](http://jsonlint.com/) or a linter package for your favorite editing environment (Visual Studio Code, Atom, Sublime Text, Visual Studio).</span></span>

<span data-ttu-id="e93a6-248">Aynı zamanda bir fikir tooformat olan, JSON okunabilirliği.</span><span class="sxs-lookup"><span data-stu-id="e93a6-248">It's also a good idea tooformat your JSON for better readability.</span></span> <span data-ttu-id="e93a6-249">Bir JSON biçimlendirici paketi için yerel, Düzenleyicisi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e93a6-249">You can use a JSON formatter package for your local editor.</span></span> <span data-ttu-id="e93a6-250">Visual Studio'da tooformat hello belge basın **Ctrl + K, Ctrl + D**.</span><span class="sxs-lookup"><span data-stu-id="e93a6-250">In Visual Studio, tooformat hello document, press **Ctrl+K, Ctrl+D**.</span></span> <span data-ttu-id="e93a6-251">Visual Studio Code basın **Alt + üst karakter + F**.</span><span class="sxs-lookup"><span data-stu-id="e93a6-251">In Visual Studio Code, press **Alt+Shift+F**.</span></span> <span data-ttu-id="e93a6-252">Yerel düzenleyicinizi hello belge biçimlendirmez, kullanabileceğiniz bir [çevrimiçi biçimlendirici](https://www.bing.com/search?q=json+formatter).</span><span class="sxs-lookup"><span data-stu-id="e93a6-252">If your local editor doesn't format hello document, you can use an [online formatter](https://www.bing.com/search?q=json+formatter).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e93a6-253">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e93a6-253">Next steps</span></span>
* <span data-ttu-id="e93a6-254">Sanal makineler için çözüm mimarisi oluşturma ile ilgili yönergeler için bkz: [bir Windows VM Azure'da çalışan](../guidance/guidance-compute-single-vm.md) ve [Azure'da bir Linux VM çalışması](../guidance/guidance-compute-single-vm-linux.md).</span><span class="sxs-lookup"><span data-stu-id="e93a6-254">For guidance on architecting your solution for virtual machines, see [Run a Windows VM in Azure](../guidance/guidance-compute-single-vm.md) and [Run a Linux VM in Azure](../guidance/guidance-compute-single-vm-linux.md).</span></span>
* <span data-ttu-id="e93a6-255">Bir depolama hesabı ayarlama hakkında yönergeler için bkz [Azure Storage performans ve ölçeklenebilirlik Yapılacaklar listesi](../storage/common/storage-performance-checklist.md).</span><span class="sxs-lookup"><span data-stu-id="e93a6-255">For guidance on setting up a storage account, see [Azure Storage performance and scalability checklist](../storage/common/storage-performance-checklist.md).</span></span>
* <span data-ttu-id="e93a6-256">Kuruluş Resource Manager tooeffectively nasıl kullanabileceğiniz hakkında toolearn abonelikleri yönetmek için bkz [Azure enterprise iskele: Düzenleyici abonelik idare](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="e93a6-256">toolearn about how an enterprise can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold: Prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

