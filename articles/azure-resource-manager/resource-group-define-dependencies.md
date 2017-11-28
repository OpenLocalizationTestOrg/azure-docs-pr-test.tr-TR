---
title: "Azure kaynakları için dağıtım sırasını Ayarla | Microsoft Docs"
description: "Bir kaynak olarak başka bir kaynağa bağımlı kaynakları doğru sırayla dağıtılan emin olmak için dağıtım sırasında nasıl kurulacağı açıklanmaktadır."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: 
ms.assetid: 34ebaf1e-480c-4b4d-9bf6-251bd3f8f2cf
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/03/2017
ms.author: tomfitz
ms.openlocfilehash: 3d6a46116ae9d7d940bc10dfa832540f42c0af7e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="define-the-order-for-deploying-resources-in-azure-resource-manager-templates"></a><span data-ttu-id="2f6ab-103">Azure Resource Manager şablonları kaynaklarında dağıtmak için sipariş tanımlayın</span><span class="sxs-lookup"><span data-stu-id="2f6ab-103">Define the order for deploying resources in Azure Resource Manager templates</span></span>
<span data-ttu-id="2f6ab-104">Belirli bir kaynak için kaynak dağıtılmadan önce bulunmalıdır diğer kaynaklara olabilir.</span><span class="sxs-lookup"><span data-stu-id="2f6ab-104">For a given resource, there can be other resources that must exist before the resource is deployed.</span></span> <span data-ttu-id="2f6ab-105">Örneğin, bir SQL server SQL veritabanı dağıtmayı denemeden önce mevcut olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f6ab-105">For example, a SQL server must exist before attempting to deploy a SQL database.</span></span> <span data-ttu-id="2f6ab-106">Bir kaynağı başka kaynaklara bağlı olarak işaretleyerek bu ilişkiyi tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f6ab-106">You define this relationship by marking one resource as dependent on the other resource.</span></span> <span data-ttu-id="2f6ab-107">Bir bağımlılıkla tanımladığınız **dependsOn** öğesini kullanarak veya **başvuru** işlevi.</span><span class="sxs-lookup"><span data-stu-id="2f6ab-107">You define a dependency with the **dependsOn** element, or by using the **reference** function.</span></span> 

<span data-ttu-id="2f6ab-108">Resource Manager kaynakları arasındaki bağımlılıkları değerlendirir ve bunların bağımlı sırası dağıtır.</span><span class="sxs-lookup"><span data-stu-id="2f6ab-108">Resource Manager evaluates the dependencies between resources, and deploys them in their dependent order.</span></span> <span data-ttu-id="2f6ab-109">Kaynakları birbirlerine bağımlı olmadıkları zaman Resource Manager bunları paralel olarak dağıtır.</span><span class="sxs-lookup"><span data-stu-id="2f6ab-109">When resources are not dependent on each other, Resource Manager deploys them in parallel.</span></span> <span data-ttu-id="2f6ab-110">Yalnızca bağımlılıkları dağıtılan kaynaklar için aynı şablonu tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f6ab-110">You only need to define dependencies for resources that are deployed in the same template.</span></span> 

## <a name="dependson"></a><span data-ttu-id="2f6ab-111">dependsOn</span><span class="sxs-lookup"><span data-stu-id="2f6ab-111">dependsOn</span></span>
<span data-ttu-id="2f6ab-112">Şablonunuzu içinde dependsOn öğesi bir veya daha fazla kaynak bağlı olarak bir kaynak tanımlamanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="2f6ab-112">Within your template, the dependsOn element enables you to define one resource as a dependent on one or more resources.</span></span> <span data-ttu-id="2f6ab-113">Kaynak adlarının virgülle ayrılmış bir liste değeri olabilir.</span><span class="sxs-lookup"><span data-stu-id="2f6ab-113">Its value can be a comma-separated list of resource names.</span></span> 

<span data-ttu-id="2f6ab-114">Aşağıdaki örnek, bir yük dengeleyici, sanal ağ ve birden çok depolama hesabı oluşturur bir döngü bağlıdır bir sanal makine ölçek kümesini gösterir.</span><span class="sxs-lookup"><span data-stu-id="2f6ab-114">The following example shows a virtual machine scale set that depends on a load balancer, virtual network, and a loop that creates multiple storage accounts.</span></span> <span data-ttu-id="2f6ab-115">Aşağıdaki örnekte bu diğer kaynakları gösterilmez, ancak başka bir yerde şablonda bulunması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f6ab-115">These other resources are not shown in the following example, but they would need to exist elsewhere in the template.</span></span>

```json
{
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  "name": "[variables('namingInfix')]",
  "location": "[variables('location')]",
  "apiVersion": "2016-03-30",
  "tags": {
    "displayName": "VMScaleSet"
  },
  "dependsOn": [
    "[variables('loadBalancerName')]",
    "[variables('virtualNetworkName')]",
    "storageLoop",
  ],
  ...
}
```

<span data-ttu-id="2f6ab-116">Önceki örnekte, bir bağımlılık adlı bir kopya döngü oluşturulan kaynakları içindedir **storageLoop**.</span><span class="sxs-lookup"><span data-stu-id="2f6ab-116">In the preceding example, a dependency is included on the resources that are created through a copy loop named **storageLoop**.</span></span> <span data-ttu-id="2f6ab-117">Bir örnek için bkz: [Azure Resource Manager'da kaynakları birden çok örneğini oluşturma](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="2f6ab-117">For an example, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

<span data-ttu-id="2f6ab-118">Bağımlılıklar tanımlarken, Karışıklığı önlemek için kaynak türü ve kaynak sağlayıcısı ad alanı dahil edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f6ab-118">When defining dependencies, you can include the resource provider namespace and resource type to avoid ambiguity.</span></span> <span data-ttu-id="2f6ab-119">Örneğin, bir yük dengeleyici ve diğer kaynakları aynı adları olabilir sanal ağ açıklamak için aşağıdaki biçimi kullanın:</span><span class="sxs-lookup"><span data-stu-id="2f6ab-119">For example, to clarify a load balancer and virtual network that may have the same names as other resources, use the following format:</span></span>

```json
"dependsOn": [
  "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
  "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
]
``` 

<span data-ttu-id="2f6ab-120">DependsOn kaynaklarınız arasındaki ilişkileri eşlemek için kullanılacak inclined, ancak neden yaptığınız anlamak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="2f6ab-120">While you may be inclined to use dependsOn to map relationships between your resources, it's important to understand why you're doing it.</span></span> <span data-ttu-id="2f6ab-121">Örneğin, kaynakları nasıl bağlandığına belgelemek için dependsOn sağ yaklaşım değildir.</span><span class="sxs-lookup"><span data-stu-id="2f6ab-121">For example, to document how resources are interconnected, dependsOn is not the right approach.</span></span> <span data-ttu-id="2f6ab-122">Dağıtımdan sonra hangi kaynaklara dependsOn öğesinde tanımlanan sorgulayamıyor.</span><span class="sxs-lookup"><span data-stu-id="2f6ab-122">You cannot query which resources were defined in the dependsOn element after deployment.</span></span> <span data-ttu-id="2f6ab-123">Resource Manager bağımlılığı olan paralel iki kaynakları dağıtmayan gerektiğinden dependsOn kullanarak, potansiyel olarak dağıtım süresini etkiler.</span><span class="sxs-lookup"><span data-stu-id="2f6ab-123">By using dependsOn, you potentially impact deployment time because Resource Manager does not deploy in parallel two resources that have a dependency.</span></span> <span data-ttu-id="2f6ab-124">Kaynakları arasındaki ilişkileri belge, bunun yerine kullanmak için [kaynak bağlama](/rest/api/resources/resourcelinks).</span><span class="sxs-lookup"><span data-stu-id="2f6ab-124">To document relationships between resources, instead use [resource linking](/rest/api/resources/resourcelinks).</span></span>

## <a name="child-resources"></a><span data-ttu-id="2f6ab-125">Alt kaynakları</span><span class="sxs-lookup"><span data-stu-id="2f6ab-125">Child resources</span></span>
<span data-ttu-id="2f6ab-126">Kaynaklar özellik tanımlanmakta kaynak ilgili alt kaynakları belirtmenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="2f6ab-126">The resources property allows you to specify child resources that are related to the resource being defined.</span></span> <span data-ttu-id="2f6ab-127">Alt kaynakları yalnızca tanımlı beş düzey derinliğinde olabilir.</span><span class="sxs-lookup"><span data-stu-id="2f6ab-127">Child resources can only be defined five levels deep.</span></span> <span data-ttu-id="2f6ab-128">Dolaylı bir bağımlılığı alt kaynağına ve üst arasında oluşturulmaz dikkate almak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="2f6ab-128">It is important to note that an implicit dependency is not created between a child resource and the parent resource.</span></span> <span data-ttu-id="2f6ab-129">Üst kaynak sonra dağıtılacak alt kaynak ihtiyacınız varsa, bu bağımlılık dependsOn özelliğiyle açıkça belirtmelidir.</span><span class="sxs-lookup"><span data-stu-id="2f6ab-129">If you need the child resource to be deployed after the parent resource, you must explicitly state that dependency with the dependsOn property.</span></span> 

<span data-ttu-id="2f6ab-130">Her bir üst kaynağın yalnızca belirli kaynak türleri alt kaynakları kabul eder.</span><span class="sxs-lookup"><span data-stu-id="2f6ab-130">Each parent resource accepts only certain resource types as child resources.</span></span> <span data-ttu-id="2f6ab-131">Kabul edilen kaynak türleri belirtilen [şablon şeması](https://github.com/Azure/azure-resource-manager-schemas) üst kaynak.</span><span class="sxs-lookup"><span data-stu-id="2f6ab-131">The accepted resource types are specified in the [template schema](https://github.com/Azure/azure-resource-manager-schemas) of the parent resource.</span></span> <span data-ttu-id="2f6ab-132">Üst kaynak türünün adı gibi alt kaynak türü adını içeren **Microsoft.Web/sites/config** ve **Microsoft.Web/sites/extensions** her iki alt kaynakları olan **Microsoft.Web/sites**.</span><span class="sxs-lookup"><span data-stu-id="2f6ab-132">The name of child resource type includes the name of the parent resource type, such as **Microsoft.Web/sites/config** and **Microsoft.Web/sites/extensions** are both child resources of the **Microsoft.Web/sites**.</span></span>

<span data-ttu-id="2f6ab-133">Aşağıdaki örnek, bir SQL server ve SQL veritabanı gösterir.</span><span class="sxs-lookup"><span data-stu-id="2f6ab-133">The following example shows a SQL server and SQL database.</span></span> <span data-ttu-id="2f6ab-134">Veritabanı sunucusunun bir alt olsa bile açık bağımlılığı SQL database ve SQL server arasında tanımlanır dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="2f6ab-134">Notice that an explicit dependency is defined between the SQL database and SQL server, even though the database is a child of the server.</span></span>

```json
"resources": [
  {
    "name": "[variables('sqlserverName')]",
    "type": "Microsoft.Sql/servers",
    "location": "[resourceGroup().location]",
    "tags": {
      "displayName": "SqlServer"
    },
    "apiVersion": "2014-04-01-preview",
    "properties": {
      "administratorLogin": "[parameters('administratorLogin')]",
      "administratorLoginPassword": "[parameters('administratorLoginPassword')]"
    },
    "resources": [
      {
        "name": "[parameters('databaseName')]",
        "type": "databases",
        "location": "[resourceGroup().location]",
        "tags": {
          "displayName": "Database"
        },
        "apiVersion": "2014-04-01-preview",
        "dependsOn": [
          "[variables('sqlserverName')]"
        ],
        "properties": {
          "edition": "[parameters('edition')]",
          "collation": "[parameters('collation')]",
          "maxSizeBytes": "[parameters('maxSizeBytes')]",
          "requestedServiceObjectiveName": "[parameters('requestedServiceObjectiveName')]"
        }
      }
    ]
  }
]
```

## <a name="reference-function"></a><span data-ttu-id="2f6ab-135">başvuru işlevi</span><span class="sxs-lookup"><span data-stu-id="2f6ab-135">reference function</span></span>
<span data-ttu-id="2f6ab-136">[Başvuru işlevi](resource-group-template-functions-resource.md#reference) ifadenin değerini diğer JSON ad ve değer çiftlerini veya çalışma zamanı kaynakları türetmemize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="2f6ab-136">The [reference function](resource-group-template-functions-resource.md#reference) enables an expression to derive its value from other JSON name and value pairs or runtime resources.</span></span> <span data-ttu-id="2f6ab-137">Başvuru ifadeleri örtük olarak bir kaynak üzerinde başka bir bağlıdır bildirin.</span><span class="sxs-lookup"><span data-stu-id="2f6ab-137">Reference expressions implicitly declare that one resource depends on another.</span></span> <span data-ttu-id="2f6ab-138">Genel biçimi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="2f6ab-138">The general format is:</span></span>

```json
reference('resourceName').propertyPath
```

<span data-ttu-id="2f6ab-139">Aşağıdaki örnekte, bir CDN uç noktası açıkça CDN profili bağlıdır ve örtük olarak bir web uygulamasında bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="2f6ab-139">In the following example, a CDN endpoint explicitly depends on the CDN profile, and implicitly depends on a web app.</span></span>

```json
{
    "name": "[variables('endpointName')]",
    "type": "endpoints",
    "location": "[resourceGroup().location]",
    "apiVersion": "2016-04-02",
    "dependsOn": [
            "[variables('profileName')]"
    ],
    "properties": {
        "originHostHeader": "[reference(variables('webAppName')).hostNames[0]]",
        ...
    }
```

<span data-ttu-id="2f6ab-140">Bağımlılıklar belirtmek için bu öğeyi veya dependsOn öğesini kullanabilirsiniz, ancak aynı bağımlı kaynak için her ikisini de kullanmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="2f6ab-140">You can use either this element or the dependsOn element to specify dependencies, but you do not need to use both for the same dependent resource.</span></span> <span data-ttu-id="2f6ab-141">Mümkün olduğunda, gereksiz bir bağımlılık ekleme önlemek için dolaylı bir başvuru kullanın.</span><span class="sxs-lookup"><span data-stu-id="2f6ab-141">Whenever possible, use an implicit reference to avoid adding an unnecessary dependency.</span></span>

<span data-ttu-id="2f6ab-142">Daha fazla bilgi için bkz: [başvuru işlevi](resource-group-template-functions-resource.md#reference).</span><span class="sxs-lookup"><span data-stu-id="2f6ab-142">To learn more, see [reference function](resource-group-template-functions-resource.md#reference).</span></span>

## <a name="recommendations-for-setting-dependencies"></a><span data-ttu-id="2f6ab-143">Bağımlılıklarını ayarlama önerileri</span><span class="sxs-lookup"><span data-stu-id="2f6ab-143">Recommendations for setting dependencies</span></span>

<span data-ttu-id="2f6ab-144">Ayarlamak için hangi bağımlılıkları karar verirken aşağıdaki yönergeleri kullanın:</span><span class="sxs-lookup"><span data-stu-id="2f6ab-144">When deciding what dependencies to set, use the following guidelines:</span></span>

* <span data-ttu-id="2f6ab-145">Mümkün olduğunca az bağımlılıkları ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="2f6ab-145">Set as few dependencies as possible.</span></span>
* <span data-ttu-id="2f6ab-146">Bir alt kaynak kendi üst kaynağına bağımlı olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="2f6ab-146">Set a child resource as dependent on its parent resource.</span></span>
* <span data-ttu-id="2f6ab-147">Kullanım **başvuru** bir özellik paylaşmak için gereken kaynaklar arasında örtük bağımlılıkları ayarlamak üzere işlevi.</span><span class="sxs-lookup"><span data-stu-id="2f6ab-147">Use the **reference** function to set implicit dependencies between resources that need to share a property.</span></span> <span data-ttu-id="2f6ab-148">Açık bir bağımlılık eklemeyin (**dependsOn**) ne zaman önceden tanımladığınız dolaylı bir bağımlılığı.</span><span class="sxs-lookup"><span data-stu-id="2f6ab-148">Do not add an explicit dependency (**dependsOn**) when you have already defined an implicit dependency.</span></span> <span data-ttu-id="2f6ab-149">Bu yaklaşım, gereksiz bağımlılıklara sahip olma riskini azaltır.</span><span class="sxs-lookup"><span data-stu-id="2f6ab-149">This approach reduces the risk of having unnecessary dependencies.</span></span> 
* <span data-ttu-id="2f6ab-150">Bir kaynak bulunamadığında bir bağımlılık ayarlama **oluşturulan** başka bir kaynaktan işlevselliği olmadan.</span><span class="sxs-lookup"><span data-stu-id="2f6ab-150">Set a dependency when a resource cannot be **created** without functionality from another resource.</span></span> <span data-ttu-id="2f6ab-151">Kaynakları yalnızca etkileşimde dağıtımdan sonra bir bağımlılık ayarlı değil.</span><span class="sxs-lookup"><span data-stu-id="2f6ab-151">Do not set a dependency if the resources only interact after deployment.</span></span>
* <span data-ttu-id="2f6ab-152">Açıkça ayarlamadan basamaklı bağımlılıkları olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="2f6ab-152">Let dependencies cascade without setting them explicitly.</span></span> <span data-ttu-id="2f6ab-153">Örneğin, sanal makinenize bir sanal ağ arabiriminde bağlıdır ve sanal ağ arabirimi bir sanal ağ ve genel IP adreslerine bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="2f6ab-153">For example, your virtual machine depends on a virtual network interface, and the virtual network interface depends on a virtual network and public IP addresses.</span></span> <span data-ttu-id="2f6ab-154">Bu nedenle, sanal makine dağıtılan tüm üç kaynakları bağlıdır, ancak açıkça sanal makinenin tüm üç kaynaklara bağlı olarak ayarlı değil.</span><span class="sxs-lookup"><span data-stu-id="2f6ab-154">Therefore, the virtual machine is deployed after all three resources, but do not explicitly set the virtual machine as dependent on all three resources.</span></span> <span data-ttu-id="2f6ab-155">Bu yaklaşım, bağımlılık sırası açıklar ve daha sonra şablonu değiştirmek kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="2f6ab-155">This approach clarifies the dependency order and makes it easier to change the template later.</span></span>
* <span data-ttu-id="2f6ab-156">Dağıtım öncesinde bir değer belirlenebilir, bir bağımlılık olmadan kaynağın dağıtmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="2f6ab-156">If a value can be determined before deployment, try deploying the resource without a dependency.</span></span> <span data-ttu-id="2f6ab-157">Örneğin, bir yapılandırma değeri başka bir kaynak adı gerekiyorsa, bir bağımlılık gerekmeyebilir.</span><span class="sxs-lookup"><span data-stu-id="2f6ab-157">For example, if a configuration value needs the name of another resource, you might not need a dependency.</span></span> <span data-ttu-id="2f6ab-158">Bazı kaynaklar diğer kaynak varlığını doğrulamak için bu yönergeleri her zaman çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="2f6ab-158">This guidance does not always work because some resources verify the existence of the other resource.</span></span> <span data-ttu-id="2f6ab-159">Bir hata alırsanız, bir bağımlılık ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2f6ab-159">If you receive an error, add a dependency.</span></span> 

<span data-ttu-id="2f6ab-160">Resource Manager şablonu doğrulama sırasında döngüsel bağımlılıklar tanımlar.</span><span class="sxs-lookup"><span data-stu-id="2f6ab-160">Resource Manager identifies circular dependencies during template validation.</span></span> <span data-ttu-id="2f6ab-161">Döngüsel bağımlılık var olduğunu bildiren bir hata alırsanız, şablonunuzu bağımlılıkları gerekmeyen ve Kaldırılabilir olmadığını değerlendirin.</span><span class="sxs-lookup"><span data-stu-id="2f6ab-161">If you receive an error stating that a circular dependency exists, evaluate your template to see if any dependencies are not needed and can be removed.</span></span> <span data-ttu-id="2f6ab-162">Bağımlılıklarını kaldırma çalışmazsa, bazı dağıtım işlemlerini döngüsel bağımlılık kaynakları sonra dağıtılan alt kaynakları taşınmasını tarafından döngüsel bağımlılıklar önleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f6ab-162">If removing dependencies does not work, you can avoid circular dependencies by moving some deployment operations into child resources that are deployed after the resources that have the circular dependency.</span></span> <span data-ttu-id="2f6ab-163">Örneğin, iki sanal makine dağıtıyorsanız, ancak diğer başvuran her birine özelliklerini ayarlamanız gerekir varsayalım.</span><span class="sxs-lookup"><span data-stu-id="2f6ab-163">For example, suppose you are deploying two virtual machines but you must set properties on each one that refer to the other.</span></span> <span data-ttu-id="2f6ab-164">Bunları şu sırayla dağıtabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2f6ab-164">You can deploy them in the following order:</span></span>

1. <span data-ttu-id="2f6ab-165">VM1</span><span class="sxs-lookup"><span data-stu-id="2f6ab-165">vm1</span></span>
2. <span data-ttu-id="2f6ab-166">vm2</span><span class="sxs-lookup"><span data-stu-id="2f6ab-166">vm2</span></span>
3. <span data-ttu-id="2f6ab-167">Vm1 uzantısı vm1 ve vm2 bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="2f6ab-167">Extension on vm1 depends on vm1 and vm2.</span></span> <span data-ttu-id="2f6ab-168">Uzantı vm2 alır vm1 değerlerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="2f6ab-168">The extension sets values on vm1 that it gets from vm2.</span></span>
4. <span data-ttu-id="2f6ab-169">Vm2 uzantısı vm1 ve vm2 bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="2f6ab-169">Extension on vm2 depends on vm1 and vm2.</span></span> <span data-ttu-id="2f6ab-170">Uzantı vm1 alır vm2 değerlerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="2f6ab-170">The extension sets values on vm2 that it gets from vm1.</span></span>

<span data-ttu-id="2f6ab-171">Dağıtım sırası değerlendirmek ve bağımlılık hataları çözümleme hakkında daha fazla bilgi için bkz: [ortak Azure dağıtım hataları Azure Resource Manager ile ilgili sorunları giderme](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="2f6ab-171">For information about assessing the deployment order and resolving dependency errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2f6ab-172">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2f6ab-172">Next steps</span></span>
* <span data-ttu-id="2f6ab-173">Dağıtım sırasında bağımlılıkları sorun giderme hakkında bilgi edinmek için [ortak Azure dağıtım hataları Azure Resource Manager ile ilgili sorunları giderme](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="2f6ab-173">To learn about troubleshooting dependencies during deployment, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="2f6ab-174">Azure Resource Manager şablonları oluşturma hakkında bilgi edinmek için [şablonları yazma](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="2f6ab-174">To learn about creating Azure Resource Manager templates, see [Authoring templates](resource-group-authoring-templates.md).</span></span> 
* <span data-ttu-id="2f6ab-175">Bir şablon kullanılabilir işlevlerin listesi için bkz [şablon işlevleri](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="2f6ab-175">For a list of the available functions in a template, see [Template functions](resource-group-template-functions.md).</span></span>

