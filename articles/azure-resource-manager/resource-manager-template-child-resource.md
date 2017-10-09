---
title: "Azure şablonu aaaDefine alt kaynak | Microsoft Docs"
description: "Tooset nasıl hello kaynak türü ve Azure Resource Manager şablonu alt kaynağın adını gösterir"
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: tomfitz
ms.openlocfilehash: c502c589100d7ae864d7fb01b5ba10ddfaf92592
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-name-and-type-for-child-resource-in-resource-manager-template"></a><span data-ttu-id="26390-103">Alt kaynak için ad ve tür Resource Manager şablonunda ayarlayın</span><span class="sxs-lookup"><span data-stu-id="26390-103">Set name and type for child resource in Resource Manager template</span></span>
<span data-ttu-id="26390-104">Bir şablon oluştururken, sık tooinclude ilgili tooa üst kaynak bir alt kaynak gerekir.</span><span class="sxs-lookup"><span data-stu-id="26390-104">When creating a template, you frequently need tooinclude a child resource that is related tooa parent resource.</span></span> <span data-ttu-id="26390-105">Örneğin, şablonunuza bir SQL server ve veritabanı içerebilir.</span><span class="sxs-lookup"><span data-stu-id="26390-105">For example, your template may include a SQL server and a database.</span></span> <span data-ttu-id="26390-106">Merhaba SQL server hello üst kaynak ve hello alt kaynak hello veritabanıdır.</span><span class="sxs-lookup"><span data-stu-id="26390-106">hello SQL server is hello parent resource, and hello database is hello child resource.</span></span> 

<span data-ttu-id="26390-107">Merhaba alt kaynak türünün Hello biçimdedir:`{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`</span><span class="sxs-lookup"><span data-stu-id="26390-107">hello format of hello child resource type is: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`</span></span>

<span data-ttu-id="26390-108">Merhaba alt kaynak adın Hello biçimdedir:`{parent-resource-name}/{child-resource-name}`</span><span class="sxs-lookup"><span data-stu-id="26390-108">hello format of hello child resource name is: `{parent-resource-name}/{child-resource-name}`</span></span>

<span data-ttu-id="26390-109">Ancak, hello türü ve bir şablon adı farklı içindeki hello üst kaynak olup olmadığını iç içe yerleştirilmiş üzerinde veya kendi hello en üst düzeyde göre belirtin.</span><span class="sxs-lookup"><span data-stu-id="26390-109">However, you specify hello type and name in a template differently based on whether it is nested within hello parent resource, or on its own at hello top level.</span></span> <span data-ttu-id="26390-110">Bu konu, her iki toohandle nasıl yaklaşıyor gösterir.</span><span class="sxs-lookup"><span data-stu-id="26390-110">This topic shows how toohandle both approaches.</span></span>

<span data-ttu-id="26390-111">Tam başvuru tooa kaynak oluştururken hello sipariş toocombine hello türünden kesim ve ad hello iki yalnızca bir birleşimini değil.</span><span class="sxs-lookup"><span data-stu-id="26390-111">When constructing a fully qualified reference tooa resource, hello order toocombine segments from hello type and name  is not simply a concatenation of hello two.</span></span>  <span data-ttu-id="26390-112">Bunun yerine, bir dizi hello ad alanından sonra kullanın *türü/adı* az belirli toomost belirli çiftlerinden:</span><span class="sxs-lookup"><span data-stu-id="26390-112">Instead, after hello namespace, use a sequence of *type/name* pairs from least specific toomost specific:</span></span>

```json
{resource-provider-namespace}/{parent-resource-type}/{parent-resource-name}[/{child-resource-type}/{child-resource-name}]*
```

<span data-ttu-id="26390-113">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="26390-113">For example:</span></span>

<span data-ttu-id="26390-114">`Microsoft.Compute/virtualMachines/myVM/extensions/myExt`doğru `Microsoft.Compute/virtualMachines/extensions/myVM/myExt` doğru değil</span><span class="sxs-lookup"><span data-stu-id="26390-114">`Microsoft.Compute/virtualMachines/myVM/extensions/myExt` is correct `Microsoft.Compute/virtualMachines/extensions/myVM/myExt` is not correct</span></span>

## <a name="nested-child-resource"></a><span data-ttu-id="26390-115">İç içe alt kaynak</span><span class="sxs-lookup"><span data-stu-id="26390-115">Nested child resource</span></span>
<span data-ttu-id="26390-116">Merhaba en kolay yolu toodefine alt kaynak olan toonest hello üst kaynak içinde.</span><span class="sxs-lookup"><span data-stu-id="26390-116">hello easiest way toodefine a child resource is toonest it within hello parent resource.</span></span> <span data-ttu-id="26390-117">Merhaba aşağıdaki örnek bir SQL Server içinde iç içe geçmiş bir SQL veritabanı gösterir.</span><span class="sxs-lookup"><span data-stu-id="26390-117">hello following example shows a SQL database nested within in a SQL Server.</span></span>

```json
{
  "name": "exampleserver",
  "type": "Microsoft.Sql/servers",
  "apiVersion": "2014-04-01",
  ...
  "resources": [
    {
      "name": "exampledatabase",
      "type": "databases",
      "apiVersion": "2014-04-01",
      ...
    }
  ]
}
```

<span data-ttu-id="26390-118">Merhaba alt kaynak için çok hello türü ayarlanmış`databases` ancak kendi tam kaynak türü `Microsoft.Sql/servers/databases`.</span><span class="sxs-lookup"><span data-stu-id="26390-118">For hello child resource, hello type is set too`databases` but its full resource type is `Microsoft.Sql/servers/databases`.</span></span> <span data-ttu-id="26390-119">Sunmaz `Microsoft.Sql/servers/` hello üst kaynak türünden varsayıldığından.</span><span class="sxs-lookup"><span data-stu-id="26390-119">You do not provide `Microsoft.Sql/servers/` because it is assumed from hello parent resource type.</span></span> <span data-ttu-id="26390-120">Merhaba alt kaynak adı olarak ayarlanmış çok`exampledatabase` ancak hello tam ad hello üst adı içerir.</span><span class="sxs-lookup"><span data-stu-id="26390-120">hello child resource name is set too`exampledatabase` but hello full name includes hello parent name.</span></span> <span data-ttu-id="26390-121">Sunmaz `exampleserver` hello üst kaynaktan varsayıldığından.</span><span class="sxs-lookup"><span data-stu-id="26390-121">You do not provide `exampleserver` because it is assumed from hello parent resource.</span></span>

## <a name="top-level-child-resource"></a><span data-ttu-id="26390-122">Üst düzey alt kaynak</span><span class="sxs-lookup"><span data-stu-id="26390-122">Top-level child resource</span></span>
<span data-ttu-id="26390-123">Merhaba en üst düzeyinde hello alt kaynak tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="26390-123">You can define hello child resource at hello top level.</span></span> <span data-ttu-id="26390-124">Merhaba üst kaynak hello dağıtılmamışsa, bu yaklaşım kullanabilir aynı şablonu veya toouse istiyorsanız `copy` toocreate birden çok alt kaynakları.</span><span class="sxs-lookup"><span data-stu-id="26390-124">You might use this approach if hello parent resource is not deployed in hello same template, or if want toouse `copy` toocreate multiple child resources.</span></span> <span data-ttu-id="26390-125">Bu yaklaşımda, hello tam kaynak türü sağlayın ve hello üst kaynak adı hello alt kaynak adında gerekir.</span><span class="sxs-lookup"><span data-stu-id="26390-125">With this approach, you must provide hello full resource type, and include hello parent resource name in hello child resource name.</span></span>

```json
{
  "name": "exampleserver",
  "type": "Microsoft.Sql/servers",
  "apiVersion": "2014-04-01",
  "resources": [ 
  ],
  ...
},
{
  "name": "exampleserver/exampledatabase",
  "type": "Microsoft.Sql/servers/databases",
  "apiVersion": "2014-04-01",
  ...
}
```

<span data-ttu-id="26390-126">aynı hello şablonunda düzey hello üzerinde tanımlı olsa bile hello veritabanı bir alt kaynak toohello sunucusudur.</span><span class="sxs-lookup"><span data-stu-id="26390-126">hello database is a child resource toohello server even though they are defined on hello same level in hello template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="26390-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="26390-127">Next steps</span></span>
* <span data-ttu-id="26390-128">Nasıl hakkında öneriler için bkz: toocreate şablonları [en iyi uygulamalar Azure Resource Manager şablonları oluşturmak için](resource-manager-template-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="26390-128">For recommendations about how toocreate templates, see [Best practices for creating Azure Resource Manager templates](resource-manager-template-best-practices.md).</span></span>
* <span data-ttu-id="26390-129">Birden çok alt kaynakları oluşturma örneği için bkz: [Azure Resource Manager şablonları kaynaklarında birden çok örneğini dağıtmak](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="26390-129">For an example of creating multiple child resources, see [Deploy multiple instances of resources in Azure Resource Manager templates](resource-group-create-multiple.md).</span></span>
