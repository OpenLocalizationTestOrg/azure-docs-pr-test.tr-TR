---
title: "Azure kaynakları için bir dağıtım sırasıyla aaaSet | Microsoft Docs"
description: "Açıklar nasıl tooset bir kaynak dağıtım tooensure kaynaklarını sırasında başka bir kaynağa bağlı olarak dağıtılan hello doğru sırayla."
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
ms.openlocfilehash: 2f658f4c85236966c46b34a65aafb8426c92806c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="define-hello-order-for-deploying-resources-in-azure-resource-manager-templates"></a><span data-ttu-id="2b4b7-103">Azure Resource Manager şablonları kaynaklarında dağıtmak için hello düzenini tanımlayın</span><span class="sxs-lookup"><span data-stu-id="2b4b7-103">Define hello order for deploying resources in Azure Resource Manager templates</span></span>
<span data-ttu-id="2b4b7-104">Belirli bir kaynak için hello kaynak dağıtılmadan önce bulunmalıdır diğer kaynaklara olabilir.</span><span class="sxs-lookup"><span data-stu-id="2b4b7-104">For a given resource, there can be other resources that must exist before hello resource is deployed.</span></span> <span data-ttu-id="2b4b7-105">Örneğin, bir SQL server toodeploy bir SQL veritabanı denemeden önce mevcut olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2b4b7-105">For example, a SQL server must exist before attempting toodeploy a SQL database.</span></span> <span data-ttu-id="2b4b7-106">Bu ilişki hello bağlı olarak bir kaynak işaretleyerek diğer kaynak tanımlarsınız.</span><span class="sxs-lookup"><span data-stu-id="2b4b7-106">You define this relationship by marking one resource as dependent on hello other resource.</span></span> <span data-ttu-id="2b4b7-107">Merhaba bir bağımlılıkla tanımladığınız **dependsOn** öğesi veya hello kullanarak **başvuru** işlevi.</span><span class="sxs-lookup"><span data-stu-id="2b4b7-107">You define a dependency with hello **dependsOn** element, or by using hello **reference** function.</span></span> 

<span data-ttu-id="2b4b7-108">Resource Manager kaynakları arasındaki hello bağımlılıkları değerlendirir ve bunların bağımlı sırası dağıtır.</span><span class="sxs-lookup"><span data-stu-id="2b4b7-108">Resource Manager evaluates hello dependencies between resources, and deploys them in their dependent order.</span></span> <span data-ttu-id="2b4b7-109">Kaynakları birbirlerine bağımlı olmadıkları zaman Resource Manager bunları paralel olarak dağıtır.</span><span class="sxs-lookup"><span data-stu-id="2b4b7-109">When resources are not dependent on each other, Resource Manager deploys them in parallel.</span></span> <span data-ttu-id="2b4b7-110">Yalnızca toodefine bağımlılıkları hello dağıtılan kaynaklar için gereksinim duyduğunuz aynı şablonu.</span><span class="sxs-lookup"><span data-stu-id="2b4b7-110">You only need toodefine dependencies for resources that are deployed in hello same template.</span></span> 

## <a name="dependson"></a><span data-ttu-id="2b4b7-111">dependsOn</span><span class="sxs-lookup"><span data-stu-id="2b4b7-111">dependsOn</span></span>
<span data-ttu-id="2b4b7-112">Şablonunuzu içinde hello dependsOn öğesi, toodefine bir kaynak olarak bir veya daha fazla kaynak bağımlı etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="2b4b7-112">Within your template, hello dependsOn element enables you toodefine one resource as a dependent on one or more resources.</span></span> <span data-ttu-id="2b4b7-113">Kaynak adlarının virgülle ayrılmış bir liste değeri olabilir.</span><span class="sxs-lookup"><span data-stu-id="2b4b7-113">Its value can be a comma-separated list of resource names.</span></span> 

<span data-ttu-id="2b4b7-114">Merhaba aşağıdaki örnekte bir yük dengeleyici, sanal ağ ve birden çok depolama hesabı oluşturur bir döngü bağlıdır bir sanal makine ölçek kümesi gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="2b4b7-114">hello following example shows a virtual machine scale set that depends on a load balancer, virtual network, and a loop that creates multiple storage accounts.</span></span> <span data-ttu-id="2b4b7-115">Bu diğer kaynakları aşağıdaki örneğine hello gösterilmez, ancak başka bir yerde hello şablonunda tooexist gerekir.</span><span class="sxs-lookup"><span data-stu-id="2b4b7-115">These other resources are not shown in hello following example, but they would need tooexist elsewhere in hello template.</span></span>

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

<span data-ttu-id="2b4b7-116">Örnek önceki hello içinde bir bağımlılık adlı bir kopya döngü oluşturan hello kaynakları içindedir **storageLoop**.</span><span class="sxs-lookup"><span data-stu-id="2b4b7-116">In hello preceding example, a dependency is included on hello resources that are created through a copy loop named **storageLoop**.</span></span> <span data-ttu-id="2b4b7-117">Bir örnek için bkz: [Azure Resource Manager'da kaynakları birden çok örneğini oluşturma](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="2b4b7-117">For an example, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

<span data-ttu-id="2b4b7-118">Bağımlılıklar tanımlarken hello kaynak sağlayıcısı ad alanı ve kaynak türü tooavoid belirsizlik içerebilir.</span><span class="sxs-lookup"><span data-stu-id="2b4b7-118">When defining dependencies, you can include hello resource provider namespace and resource type tooavoid ambiguity.</span></span> <span data-ttu-id="2b4b7-119">Örneğin, bir yük dengeleyici ve aynı kullanım hello aşağıdaki gibi diğer kaynaklar adları hello olabilir sanal ağ biçim tooclarify:</span><span class="sxs-lookup"><span data-stu-id="2b4b7-119">For example, tooclarify a load balancer and virtual network that may have hello same names as other resources, use hello following format:</span></span>

```json
"dependsOn": [
  "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
  "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
]
``` 

<span data-ttu-id="2b4b7-120">Kaynaklarınız arasında eilimli toouse dependsOn toomap ilişkileri olabilir, ancak neden yaptığınız önemli toounderstand var.</span><span class="sxs-lookup"><span data-stu-id="2b4b7-120">While you may be inclined toouse dependsOn toomap relationships between your resources, it's important toounderstand why you're doing it.</span></span> <span data-ttu-id="2b4b7-121">Örneğin, kaynakları nasıl bağlandığına, toodocument dependsOn hello sağ yaklaşım değildir.</span><span class="sxs-lookup"><span data-stu-id="2b4b7-121">For example, toodocument how resources are interconnected, dependsOn is not hello right approach.</span></span> <span data-ttu-id="2b4b7-122">Dağıtımdan sonra hangi kaynaklara hello dependsOn öğesinde tanımlanan sorgulayamıyor.</span><span class="sxs-lookup"><span data-stu-id="2b4b7-122">You cannot query which resources were defined in hello dependsOn element after deployment.</span></span> <span data-ttu-id="2b4b7-123">Resource Manager bağımlılığı olan paralel iki kaynakları dağıtmayan gerektiğinden dependsOn kullanarak, potansiyel olarak dağıtım süresini etkiler.</span><span class="sxs-lookup"><span data-stu-id="2b4b7-123">By using dependsOn, you potentially impact deployment time because Resource Manager does not deploy in parallel two resources that have a dependency.</span></span> <span data-ttu-id="2b4b7-124">kaynaklar arasındaki toodocument ilişkileri kullanmanız [kaynak bağlama](/rest/api/resources/resourcelinks).</span><span class="sxs-lookup"><span data-stu-id="2b4b7-124">toodocument relationships between resources, instead use [resource linking](/rest/api/resources/resourcelinks).</span></span>

## <a name="child-resources"></a><span data-ttu-id="2b4b7-125">Alt kaynakları</span><span class="sxs-lookup"><span data-stu-id="2b4b7-125">Child resources</span></span>
<span data-ttu-id="2b4b7-126">Merhaba kaynaklar özellik tanımlanmakta ilgili toohello kaynaktır toospecify alt kaynakları sağlar.</span><span class="sxs-lookup"><span data-stu-id="2b4b7-126">hello resources property allows you toospecify child resources that are related toohello resource being defined.</span></span> <span data-ttu-id="2b4b7-127">Alt kaynakları yalnızca tanımlı beş düzey derinliğinde olabilir.</span><span class="sxs-lookup"><span data-stu-id="2b4b7-127">Child resources can only be defined five levels deep.</span></span> <span data-ttu-id="2b4b7-128">Alt kaynağı ve hello üst kaynağı arasında örtük bir bağımlılığa sahip değilse toonote oluşturulan önemlidir.</span><span class="sxs-lookup"><span data-stu-id="2b4b7-128">It is important toonote that an implicit dependency is not created between a child resource and hello parent resource.</span></span> <span data-ttu-id="2b4b7-129">Alt kaynak toobe hello üst kaynak sonra dağıtılan hello varsa, bu bağımlılık hello dependsOn özelliğiyle açıkça belirtmelidir.</span><span class="sxs-lookup"><span data-stu-id="2b4b7-129">If you need hello child resource toobe deployed after hello parent resource, you must explicitly state that dependency with hello dependsOn property.</span></span> 

<span data-ttu-id="2b4b7-130">Her bir üst kaynağın yalnızca belirli kaynak türleri alt kaynakları kabul eder.</span><span class="sxs-lookup"><span data-stu-id="2b4b7-130">Each parent resource accepts only certain resource types as child resources.</span></span> <span data-ttu-id="2b4b7-131">Merhaba kabul kaynak türleri hello belirtilen [şablon şeması](https://github.com/Azure/azure-resource-manager-schemas) hello üst kaynak.</span><span class="sxs-lookup"><span data-stu-id="2b4b7-131">hello accepted resource types are specified in hello [template schema](https://github.com/Azure/azure-resource-manager-schemas) of hello parent resource.</span></span> <span data-ttu-id="2b4b7-132">alt kaynak türünün Hello adını içeren hello üst kaynak türünün hello adı gibi **Microsoft.Web/sites/config** ve **Microsoft.Web/sites/extensions** hello ,herikialtkaynakları **Microsoft.Web/sites**.</span><span class="sxs-lookup"><span data-stu-id="2b4b7-132">hello name of child resource type includes hello name of hello parent resource type, such as **Microsoft.Web/sites/config** and **Microsoft.Web/sites/extensions** are both child resources of hello **Microsoft.Web/sites**.</span></span>

<span data-ttu-id="2b4b7-133">SQL server ve SQL veritabanı aşağıdaki örneğine hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="2b4b7-133">hello following example shows a SQL server and SQL database.</span></span> <span data-ttu-id="2b4b7-134">Merhaba veritabanı hello sunucu alt olsa bile açık bağımlılığı hello SQL database ve SQL server arasında tanımlanır dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="2b4b7-134">Notice that an explicit dependency is defined between hello SQL database and SQL server, even though hello database is a child of hello server.</span></span>

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

## <a name="reference-function"></a><span data-ttu-id="2b4b7-135">başvuru işlevi</span><span class="sxs-lookup"><span data-stu-id="2b4b7-135">reference function</span></span>
<span data-ttu-id="2b4b7-136">Merhaba [başvuru işlevi](resource-group-template-functions-resource.md#reference) diğer JSON ad ve değer çiftlerini veya çalışma zamanı kaynakları değerini bir deyim tooderive sağlar.</span><span class="sxs-lookup"><span data-stu-id="2b4b7-136">hello [reference function](resource-group-template-functions-resource.md#reference) enables an expression tooderive its value from other JSON name and value pairs or runtime resources.</span></span> <span data-ttu-id="2b4b7-137">Başvuru ifadeleri örtük olarak bir kaynak üzerinde başka bir bağlıdır bildirin.</span><span class="sxs-lookup"><span data-stu-id="2b4b7-137">Reference expressions implicitly declare that one resource depends on another.</span></span> <span data-ttu-id="2b4b7-138">Merhaba genel biçimi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="2b4b7-138">hello general format is:</span></span>

```json
reference('resourceName').propertyPath
```

<span data-ttu-id="2b4b7-139">Hello aşağıdaki örnek, bir CDN uç noktası açıkça CDN profili hello üzerinde bağlıdır ve örtük olarak bir web uygulamasında bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="2b4b7-139">In hello following example, a CDN endpoint explicitly depends on hello CDN profile, and implicitly depends on a web app.</span></span>

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

<span data-ttu-id="2b4b7-140">Bu öğe veya hello dependsOn öğesi toospecify bağımlılıkları kullanabilirsiniz, ancak Merhaba toouse hem gerekmez aynı bağımlı kaynak.</span><span class="sxs-lookup"><span data-stu-id="2b4b7-140">You can use either this element or hello dependsOn element toospecify dependencies, but you do not need toouse both for hello same dependent resource.</span></span> <span data-ttu-id="2b4b7-141">Mümkün olduğunda, gereksiz bir bağımlılık ekleme dolaylı başvuru tooavoid kullanın.</span><span class="sxs-lookup"><span data-stu-id="2b4b7-141">Whenever possible, use an implicit reference tooavoid adding an unnecessary dependency.</span></span>

<span data-ttu-id="2b4b7-142">toolearn daha, fazla [başvuru işlevi](resource-group-template-functions-resource.md#reference).</span><span class="sxs-lookup"><span data-stu-id="2b4b7-142">toolearn more, see [reference function](resource-group-template-functions-resource.md#reference).</span></span>

## <a name="recommendations-for-setting-dependencies"></a><span data-ttu-id="2b4b7-143">Bağımlılıklarını ayarlama önerileri</span><span class="sxs-lookup"><span data-stu-id="2b4b7-143">Recommendations for setting dependencies</span></span>

<span data-ttu-id="2b4b7-144">Hangi bağımlılıkları tooset karar verirken, yönergeleri izleyerek hello kullan:</span><span class="sxs-lookup"><span data-stu-id="2b4b7-144">When deciding what dependencies tooset, use hello following guidelines:</span></span>

* <span data-ttu-id="2b4b7-145">Mümkün olduğunca az bağımlılıkları ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="2b4b7-145">Set as few dependencies as possible.</span></span>
* <span data-ttu-id="2b4b7-146">Bir alt kaynak kendi üst kaynağına bağımlı olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="2b4b7-146">Set a child resource as dependent on its parent resource.</span></span>
* <span data-ttu-id="2b4b7-147">Kullanım hello **başvuru** işlev tooshare bir özellik gereken kaynaklar arasındaki tooset örtük bağımlılıkları.</span><span class="sxs-lookup"><span data-stu-id="2b4b7-147">Use hello **reference** function tooset implicit dependencies between resources that need tooshare a property.</span></span> <span data-ttu-id="2b4b7-148">Açık bir bağımlılık eklemeyin (**dependsOn**) ne zaman önceden tanımladığınız dolaylı bir bağımlılığı.</span><span class="sxs-lookup"><span data-stu-id="2b4b7-148">Do not add an explicit dependency (**dependsOn**) when you have already defined an implicit dependency.</span></span> <span data-ttu-id="2b4b7-149">Bu yaklaşım, gereksiz bağımlılıklara sahip olmanın hello riskini azaltır.</span><span class="sxs-lookup"><span data-stu-id="2b4b7-149">This approach reduces hello risk of having unnecessary dependencies.</span></span> 
* <span data-ttu-id="2b4b7-150">Bir kaynak bulunamadığında bir bağımlılık ayarlama **oluşturulan** başka bir kaynaktan işlevselliği olmadan.</span><span class="sxs-lookup"><span data-stu-id="2b4b7-150">Set a dependency when a resource cannot be **created** without functionality from another resource.</span></span> <span data-ttu-id="2b4b7-151">Merhaba kaynakları yalnızca dağıtımdan sonra etkileşimde, bir bağımlılık ayarlı değil.</span><span class="sxs-lookup"><span data-stu-id="2b4b7-151">Do not set a dependency if hello resources only interact after deployment.</span></span>
* <span data-ttu-id="2b4b7-152">Açıkça ayarlamadan basamaklı bağımlılıkları olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="2b4b7-152">Let dependencies cascade without setting them explicitly.</span></span> <span data-ttu-id="2b4b7-153">Örneğin, sanal makinenize bir sanal ağ arabiriminde bağlıdır ve hello sanal ağ arabirimi bir sanal ağ ve genel IP adreslerine bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="2b4b7-153">For example, your virtual machine depends on a virtual network interface, and hello virtual network interface depends on a virtual network and public IP addresses.</span></span> <span data-ttu-id="2b4b7-154">Bu nedenle, dağıtılan tüm üç kaynakları hello sanal makine bağlıdır, ancak açıkça hello sanal makinenin tüm üç kaynaklara bağlı olarak ayarlı değil.</span><span class="sxs-lookup"><span data-stu-id="2b4b7-154">Therefore, hello virtual machine is deployed after all three resources, but do not explicitly set hello virtual machine as dependent on all three resources.</span></span> <span data-ttu-id="2b4b7-155">Bu yaklaşım hello bağımlılık sırası açıklar ve daha sonra daha kolay toochange hello şablon hale getirir.</span><span class="sxs-lookup"><span data-stu-id="2b4b7-155">This approach clarifies hello dependency order and makes it easier toochange hello template later.</span></span>
* <span data-ttu-id="2b4b7-156">Dağıtım öncesinde bir değer belirlenebilir, bir bağımlılık olmadan hello kaynak dağıtmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="2b4b7-156">If a value can be determined before deployment, try deploying hello resource without a dependency.</span></span> <span data-ttu-id="2b4b7-157">Örneğin, bir yapılandırma değeri başka bir kaynağın hello adı gerekiyorsa, bir bağımlılık gerekmeyebilir.</span><span class="sxs-lookup"><span data-stu-id="2b4b7-157">For example, if a configuration value needs hello name of another resource, you might not need a dependency.</span></span> <span data-ttu-id="2b4b7-158">Bazı kaynaklar diğer kaynak hello hello varlığını doğrulamak için bu yönergeleri her zaman çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="2b4b7-158">This guidance does not always work because some resources verify hello existence of hello other resource.</span></span> <span data-ttu-id="2b4b7-159">Bir hata alırsanız, bir bağımlılık ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2b4b7-159">If you receive an error, add a dependency.</span></span> 

<span data-ttu-id="2b4b7-160">Resource Manager şablonu doğrulama sırasında döngüsel bağımlılıklar tanımlar.</span><span class="sxs-lookup"><span data-stu-id="2b4b7-160">Resource Manager identifies circular dependencies during template validation.</span></span> <span data-ttu-id="2b4b7-161">Döngüsel bağımlılık var olduğunu bildiren bir hata alırsanız, bağımlılıkları gerekmeyen ve Kaldırılabilir şablonu toosee değerlendirin.</span><span class="sxs-lookup"><span data-stu-id="2b4b7-161">If you receive an error stating that a circular dependency exists, evaluate your template toosee if any dependencies are not needed and can be removed.</span></span> <span data-ttu-id="2b4b7-162">Bağımlılıklarını kaldırma çalışmazsa, bazı dağıtım işlemlerini hello döngüsel bağımlılık sahip hello kaynakları sonra dağıtılan alt kaynakları taşınmasını tarafından döngüsel bağımlılıklar önleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2b4b7-162">If removing dependencies does not work, you can avoid circular dependencies by moving some deployment operations into child resources that are deployed after hello resources that have hello circular dependency.</span></span> <span data-ttu-id="2b4b7-163">Örneğin, iki sanal makine dağıtıyorsanız ancak toohello diğer başvuran her birinin özelliklerini ayarlamalısınız varsayalım.</span><span class="sxs-lookup"><span data-stu-id="2b4b7-163">For example, suppose you are deploying two virtual machines but you must set properties on each one that refer toohello other.</span></span> <span data-ttu-id="2b4b7-164">Bunları sırasının hello dağıtabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2b4b7-164">You can deploy them in hello following order:</span></span>

1. <span data-ttu-id="2b4b7-165">VM1</span><span class="sxs-lookup"><span data-stu-id="2b4b7-165">vm1</span></span>
2. <span data-ttu-id="2b4b7-166">vm2</span><span class="sxs-lookup"><span data-stu-id="2b4b7-166">vm2</span></span>
3. <span data-ttu-id="2b4b7-167">Vm1 uzantısı vm1 ve vm2 bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="2b4b7-167">Extension on vm1 depends on vm1 and vm2.</span></span> <span data-ttu-id="2b4b7-168">Merhaba uzantısı vm2 alır vm1 değerlerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="2b4b7-168">hello extension sets values on vm1 that it gets from vm2.</span></span>
4. <span data-ttu-id="2b4b7-169">Vm2 uzantısı vm1 ve vm2 bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="2b4b7-169">Extension on vm2 depends on vm1 and vm2.</span></span> <span data-ttu-id="2b4b7-170">Merhaba uzantısı vm1 alır vm2 değerlerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="2b4b7-170">hello extension sets values on vm2 that it gets from vm1.</span></span>

<span data-ttu-id="2b4b7-171">Merhaba dağıtım sırası değerlendirmek ve bağımlılık hataları çözümleme hakkında daha fazla bilgi için bkz: [ortak Azure dağıtım hataları Azure Resource Manager ile ilgili sorunları giderme](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="2b4b7-171">For information about assessing hello deployment order and resolving dependency errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b4b7-172">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2b4b7-172">Next steps</span></span>
* <span data-ttu-id="2b4b7-173">Bağımlılıklar, dağıtım sırasında sorun giderme hakkında toolearn bkz [ortak Azure dağıtım hataları Azure Resource Manager ile ilgili sorunları giderme](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="2b4b7-173">toolearn about troubleshooting dependencies during deployment, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="2b4b7-174">Azure Resource Manager şablonları oluşturma hakkında daha fazla toolearn bkz [şablonları yazma](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="2b4b7-174">toolearn about creating Azure Resource Manager templates, see [Authoring templates](resource-group-authoring-templates.md).</span></span> 
* <span data-ttu-id="2b4b7-175">Bir şablona hello kullanılabilen işlevlerin listesi için bkz [şablon işlevleri](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="2b4b7-175">For a list of hello available functions in a template, see [Template functions](resource-group-template-functions.md).</span></span>

