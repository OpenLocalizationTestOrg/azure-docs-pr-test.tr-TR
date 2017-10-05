---
title: "Azure yönetilen uygulamalar oluşturma UI tanımı anlama | Microsoft Docs"
description: "Azure yönetilen uygulamaları için kullanıcı Arabirimi tanımları oluşturmayı açıklar"
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/11/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: 176b891538f85c5638a2321561c3d8bd377d245b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-createuidefinition"></a><span data-ttu-id="a8d13-103">CreateUiDefinition ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="a8d13-103">Getting started with CreateUiDefinition</span></span>
<span data-ttu-id="a8d13-104">Bu belge, Azure portal tarafından yönetilen bir uygulama oluşturmak için kullanılan kullanıcı arabirimi oluşturmak için kullanılan bir CreateUiDefinition çekirdek kavramlarını tanıtır.</span><span class="sxs-lookup"><span data-stu-id="a8d13-104">This document introduces the core concepts of a CreateUiDefinition, which is used by the Azure portal to generate the user interface for creating a managed application.</span></span>

```json
{
   "$schema": "https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json",
   "handler": "Microsoft.Compute.MultiVm",
   "version": "0.1.2-preview",
   "parameters": {
      "basics": [ ],
      "steps": [ ],
      "outputs": { }
   }
}
```

<span data-ttu-id="a8d13-105">Bir CreateUiDefinition her zaman üç özellikleri içerir:</span><span class="sxs-lookup"><span data-stu-id="a8d13-105">A CreateUiDefinition always contains three properties:</span></span> 

* <span data-ttu-id="a8d13-106">işleyici</span><span class="sxs-lookup"><span data-stu-id="a8d13-106">handler</span></span>
* <span data-ttu-id="a8d13-107">Sürüm</span><span class="sxs-lookup"><span data-stu-id="a8d13-107">version</span></span>
* <span data-ttu-id="a8d13-108">Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a8d13-108">parameters</span></span>

<span data-ttu-id="a8d13-109">Yönetilen uygulamalar için işleyici her zaman olmalıdır `Microsoft.Compute.MultiVm`, ve en son desteklenen sürümünü `0.1.2-preview`.</span><span class="sxs-lookup"><span data-stu-id="a8d13-109">For managed applications, handler should always be `Microsoft.Compute.MultiVm`, and the latest supported version is `0.1.2-preview`.</span></span>

<span data-ttu-id="a8d13-110">Parameters özelliği şema sürümü ve belirtilen işleyici birleşimi bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="a8d13-110">The schema of the parameters property depends on the combination of the specified handler and version.</span></span> <span data-ttu-id="a8d13-111">Yönetilen uygulamalar için desteklenen özelliklerdir `basics`, `steps`, ve `outputs`.</span><span class="sxs-lookup"><span data-stu-id="a8d13-111">For managed applications, the supported properties are `basics`, `steps`, and `outputs`.</span></span> <span data-ttu-id="a8d13-112">Temel kavramları ve adımları özelliklerini içeren _öğeleri_ - gibi metin kutuları ve bırakmalar - Azure portalında görüntülenecek.</span><span class="sxs-lookup"><span data-stu-id="a8d13-112">The basics and steps properties contain the _elements_ - like textboxes and dropdowns - to be displayed in the Azure portal.</span></span> <span data-ttu-id="a8d13-113">Çıktılar özelliğini Azure Resource Manager dağıtım şablonu parametreleri için belirtilen öğelerinin çıkış değerlerini eşlemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a8d13-113">The outputs property is used to map the output values of the specified elements to the parameters of the Azure Resource Manager deployment template.</span></span>

<span data-ttu-id="a8d13-114">Dahil olmak üzere `$schema` önerilir ancak isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="a8d13-114">Including `$schema` is recommended, but optional.</span></span> <span data-ttu-id="a8d13-115">Belirtilmişse, değerin için `version` içinde eşleşmelidir `$schema` URI.</span><span class="sxs-lookup"><span data-stu-id="a8d13-115">If specified, the value for `version` must match the version within the `$schema` URI.</span></span>

## <a name="basics"></a><span data-ttu-id="a8d13-116">Temel Bilgiler</span><span class="sxs-lookup"><span data-stu-id="a8d13-116">Basics</span></span>
<span data-ttu-id="a8d13-117">Temel bilgileri her zaman Azure portalında bir CreateUiDefinition ayrıştırırken oluşturulan Sihirbazı'nın ilk adımı adımdır.</span><span class="sxs-lookup"><span data-stu-id="a8d13-117">The Basics step is always the first step of the wizard generated when the Azure portal parses a CreateUiDefinition.</span></span> <span data-ttu-id="a8d13-118">Belirtilen öğeleri görüntüleme yanı sıra `basics`, portalı abonelik, kaynak grubu ve dağıtımı için konum seçmek kullanıcıları için öğeleri yerleştirir.</span><span class="sxs-lookup"><span data-stu-id="a8d13-118">In addition to displaying the elements specified in `basics`, the portal injects elements for users to choose the subscription, resource group, and location for the deployment.</span></span> <span data-ttu-id="a8d13-119">Genellikle, bir küme veya yönetici kimlik bilgileri adı gibi dağıtım çapında parametreler için sorgu öğeleri bu adımı tamamlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="a8d13-119">Generally, elements that query for deployment-wide parameters, like the name of a cluster or administrator credentials, should go in this step.</span></span>

<span data-ttu-id="a8d13-120">Bir öğenin davranışı kullanıcının abonelik, kaynak grubu veya konum bağımlı olması durumunda, bu öğenin temel kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="a8d13-120">If an element's behavior depends on the user's subscription, resource group, or location, then that element can't be used in basics.</span></span> <span data-ttu-id="a8d13-121">Örneğin, **Microsoft.Compute.SizeSelector** kullanıcının abonelik ve kullanılabilir boyutların listesi belirlemek için konum bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="a8d13-121">For example, **Microsoft.Compute.SizeSelector** depends on the user's subscription and location to determine the list of available sizes.</span></span> <span data-ttu-id="a8d13-122">Bu nedenle, **Microsoft.Compute.SizeSelector** adımlarda yalnızca kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a8d13-122">Therefore, **Microsoft.Compute.SizeSelector** can only be used in steps.</span></span> <span data-ttu-id="a8d13-123">Genellikle, yalnızca öğeleri **Microsoft.Common** ad alanı temelleri kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a8d13-123">Generally, only elements in the **Microsoft.Common** namespace can be used in basics.</span></span> <span data-ttu-id="a8d13-124">Ancak bazı öğeler diğer ad (gibi **Microsoft.Compute.Credentials**), kullanıcının içeriğine bağlı verme, hala izin verilir.</span><span class="sxs-lookup"><span data-stu-id="a8d13-124">Although some elements in other namespaces (like **Microsoft.Compute.Credentials**) that don't depend on the user's context, are still allowed.</span></span>

## <a name="steps"></a><span data-ttu-id="a8d13-125">Adımlar</span><span class="sxs-lookup"><span data-stu-id="a8d13-125">Steps</span></span>
<span data-ttu-id="a8d13-126">Adımları özelliği her biri bir veya daha fazla öğe içeren temel bilgileri sonra görüntülemek için sıfır veya daha fazla ek adımlar içerebilir.</span><span class="sxs-lookup"><span data-stu-id="a8d13-126">The steps property can contain zero or more additional steps to display after basics, each of which contains one or more elements.</span></span> <span data-ttu-id="a8d13-127">Rol veya dağıtılan uygulama katmanı başına adımları eklemeyi düşünün.</span><span class="sxs-lookup"><span data-stu-id="a8d13-127">Consider adding steps per role or tier of the application being deployed.</span></span> <span data-ttu-id="a8d13-128">Örneğin, bir adım ana düğüm girdileri için ve çalışan düğümleri için bir adım bir kümede ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a8d13-128">For example, add a step for inputs for the master nodes, and a step for the worker nodes in a cluster.</span></span>

## <a name="outputs"></a><span data-ttu-id="a8d13-129">Çıkışları</span><span class="sxs-lookup"><span data-stu-id="a8d13-129">Outputs</span></span>
<span data-ttu-id="a8d13-130">Azure Portalı'nı kullanan `outputs` öğelerinden eşlemek için özellik `basics` ve `steps` Azure Resource Manager dağıtım şablonu parametreleri.</span><span class="sxs-lookup"><span data-stu-id="a8d13-130">The Azure portal uses the `outputs` property to map elements from `basics` and `steps` to the parameters of the Azure Resource Manager deployment template.</span></span> <span data-ttu-id="a8d13-131">Bu sözlüğün anahtarlarını şablon parametrelerinin adları ve değerleri başvurulan öğelerin çıkış nesnelerden özellikleridir.</span><span class="sxs-lookup"><span data-stu-id="a8d13-131">The keys of this dictionary are the names of the template parameters, and the values are properties of the output objects from the referenced elements.</span></span>

## <a name="functions"></a><span data-ttu-id="a8d13-132">İşlevler</span><span class="sxs-lookup"><span data-stu-id="a8d13-132">Functions</span></span>
<span data-ttu-id="a8d13-133">Benzer şekilde [şablon işlevleri](resource-group-template-functions.md) Azure Kaynak Yöneticisi'nde (hem de söz dizimi ve işlevsellik) CreateUiDefinition öğeleri girişleri ve çıkışları ile çalışmak için işlevleri sağlayan yanı sıra koşulları gibi özellikleri.</span><span class="sxs-lookup"><span data-stu-id="a8d13-133">Similar to [template functions](resource-group-template-functions.md) in Azure Resource Manager (both in syntax and functionality), CreateUiDefinition provides functions for working with elements' inputs and outputs, as well as features such as conditionals.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a8d13-134">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a8d13-134">Next steps</span></span>
<span data-ttu-id="a8d13-135">CreateUiDefinition kendisini basit bir şeması vardır.</span><span class="sxs-lookup"><span data-stu-id="a8d13-135">CreateUiDefinition itself has a simple schema.</span></span> <span data-ttu-id="a8d13-136">Tüm desteklenen öğeleri ve aşağıdaki belgeler wondrous ayrıntılı olarak açıklayan işlevleri gerçek derinliği geldiği:</span><span class="sxs-lookup"><span data-stu-id="a8d13-136">The real depth of it comes from all the supported elements and functions, which the following documents describe in wondrous detail:</span></span>

- [<span data-ttu-id="a8d13-137">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="a8d13-137">Elements</span></span>](managed-application-createuidefinition-elements.md)
- [<span data-ttu-id="a8d13-138">İşlevler</span><span class="sxs-lookup"><span data-stu-id="a8d13-138">Functions</span></span>](managed-application-createuidefinition-functions.md)

<span data-ttu-id="a8d13-139">CreateUiDefinition için geçerli bir JSON şeması burada bulunur: https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json.</span><span class="sxs-lookup"><span data-stu-id="a8d13-139">A current JSON schema for CreateUiDefinition is available here: https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json.</span></span> 

<span data-ttu-id="a8d13-140">Sonraki sürümlerinde aynı konumda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a8d13-140">Later versions will be available at the same location.</span></span> <span data-ttu-id="a8d13-141">Değiştir `0.1.2-preview` URL'sinin ve `version` kullanmayı düşündüğünüz sürüm tanıtıcısını değerle.</span><span class="sxs-lookup"><span data-stu-id="a8d13-141">Replace the `0.1.2-preview` portion of the URL and the `version` value with the version identifier you intend to use.</span></span> <span data-ttu-id="a8d13-142">Şu anda desteklenen sürüm tanımlayıcılardır `0.0.1-preview`, `0.1.0-preview`, `0.1.1-preview`, ve `0.1.2-preview`.</span><span class="sxs-lookup"><span data-stu-id="a8d13-142">The currently supported version identifiers are `0.0.1-preview`, `0.1.0-preview`, `0.1.1-preview`, and `0.1.2-preview`.</span></span>