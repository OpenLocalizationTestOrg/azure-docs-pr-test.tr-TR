---
title: "Azure yönetilen uygulamaları için kullanıcı Arabirimi tanımı oluşturma aaaUnderstand | Microsoft Docs"
description: "Açıklar nasıl toocreate UI tanımları Azure yönetilen uygulamalar"
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
ms.openlocfilehash: d53ddf438c24d5a6cb8dd53ca0b4694ab0462515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-createuidefinition"></a><span data-ttu-id="59f6a-103">CreateUiDefinition ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="59f6a-103">Getting started with CreateUiDefinition</span></span>
<span data-ttu-id="59f6a-104">Bu belge hello çekirdek hello Azure portal toogenerate hello kullanıcı arabirimi tarafından yönetilen bir uygulama oluşturmak için kullanılan bir CreateUiDefinition kavramlarını tanıtır.</span><span class="sxs-lookup"><span data-stu-id="59f6a-104">This document introduces hello core concepts of a CreateUiDefinition, which is used by hello Azure portal toogenerate hello user interface for creating a managed application.</span></span>

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

<span data-ttu-id="59f6a-105">Bir CreateUiDefinition her zaman üç özellikleri içerir:</span><span class="sxs-lookup"><span data-stu-id="59f6a-105">A CreateUiDefinition always contains three properties:</span></span> 

* <span data-ttu-id="59f6a-106">işleyici</span><span class="sxs-lookup"><span data-stu-id="59f6a-106">handler</span></span>
* <span data-ttu-id="59f6a-107">Sürüm</span><span class="sxs-lookup"><span data-stu-id="59f6a-107">version</span></span>
* <span data-ttu-id="59f6a-108">parametreler</span><span class="sxs-lookup"><span data-stu-id="59f6a-108">parameters</span></span>

<span data-ttu-id="59f6a-109">Yönetilen uygulamalar için işleyici her zaman olmalıdır `Microsoft.Compute.MultiVm`, ve en son desteklenen hello sürümü `0.1.2-preview`.</span><span class="sxs-lookup"><span data-stu-id="59f6a-109">For managed applications, handler should always be `Microsoft.Compute.MultiVm`, and hello latest supported version is `0.1.2-preview`.</span></span>

<span data-ttu-id="59f6a-110">Merhaba parameters özelliği Hello şeması hello birleşimi hello belirtilen işleyici ve sürüm üzerinde bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="59f6a-110">hello schema of hello parameters property depends on hello combination of hello specified handler and version.</span></span> <span data-ttu-id="59f6a-111">Yönetilen uygulamalar için desteklenen hello özelliklerdir `basics`, `steps`, ve `outputs`.</span><span class="sxs-lookup"><span data-stu-id="59f6a-111">For managed applications, hello supported properties are `basics`, `steps`, and `outputs`.</span></span> <span data-ttu-id="59f6a-112">Hello temel kavramları ve adımları özelliklerini içeren hello _öğeleri_ - metin kutuları ve bırakmalar gibi - toobe hello Azure portal görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="59f6a-112">hello basics and steps properties contain hello _elements_ - like textboxes and dropdowns - toobe displayed in hello Azure portal.</span></span> <span data-ttu-id="59f6a-113">kullanılan toomap hello çıkış değerini özelliktir hello çıkışları belirtilen öğeleri toohello hello Azure Resource Manager dağıtım şablonu parametrelerinin hello.</span><span class="sxs-lookup"><span data-stu-id="59f6a-113">hello outputs property is used toomap hello output values of hello specified elements toohello parameters of hello Azure Resource Manager deployment template.</span></span>

<span data-ttu-id="59f6a-114">Dahil olmak üzere `$schema` önerilir ancak isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="59f6a-114">Including `$schema` is recommended, but optional.</span></span> <span data-ttu-id="59f6a-115">Belirtilmişse, değeri hello `version` hello hello içinde sürümüyle eşleşmelidir `$schema` URI.</span><span class="sxs-lookup"><span data-stu-id="59f6a-115">If specified, hello value for `version` must match hello version within hello `$schema` URI.</span></span>

## <a name="basics"></a><span data-ttu-id="59f6a-116">Temel Bilgiler</span><span class="sxs-lookup"><span data-stu-id="59f6a-116">Basics</span></span>
<span data-ttu-id="59f6a-117">Merhaba temel bilgileri her zaman hello Azure portalında bir CreateUiDefinition ayrıştırırken oluşturulan hello Sihirbazı'nın ilk adımı hello adımdır.</span><span class="sxs-lookup"><span data-stu-id="59f6a-117">hello Basics step is always hello first step of hello wizard generated when hello Azure portal parses a CreateUiDefinition.</span></span> <span data-ttu-id="59f6a-118">Toodisplaying hello öğeleri ayrıca belirtilen `basics`, hello portalı kullanıcıları toochoose hello abonelik, kaynak grubunu ve konumu hello dağıtılmak için öğeleri yerleştirir.</span><span class="sxs-lookup"><span data-stu-id="59f6a-118">In addition toodisplaying hello elements specified in `basics`, hello portal injects elements for users toochoose hello subscription, resource group, and location for hello deployment.</span></span> <span data-ttu-id="59f6a-119">Genellikle, bir küme veya yönetici kimlik bilgileri hello adı gibi dağıtım çapında parametreleri için sorgu öğeleri bu adımda gitmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="59f6a-119">Generally, elements that query for deployment-wide parameters, like hello name of a cluster or administrator credentials, should go in this step.</span></span>

<span data-ttu-id="59f6a-120">Bir öğenin davranışı hello kullanıcının abonelik, kaynak grubu veya konum bağımlı olması durumunda, bu öğenin temel bilgileri kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="59f6a-120">If an element's behavior depends on hello user's subscription, resource group, or location, then that element can't be used in basics.</span></span> <span data-ttu-id="59f6a-121">Örneğin, **Microsoft.Compute.SizeSelector** hello kullanıcının abonelik ve konumda toodetermine hello kullanılabilir boyutların listesi üzerinde bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="59f6a-121">For example, **Microsoft.Compute.SizeSelector** depends on hello user's subscription and location toodetermine hello list of available sizes.</span></span> <span data-ttu-id="59f6a-122">Bu nedenle, **Microsoft.Compute.SizeSelector** adımlarda yalnızca kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="59f6a-122">Therefore, **Microsoft.Compute.SizeSelector** can only be used in steps.</span></span> <span data-ttu-id="59f6a-123">Genellikle, yalnızca öğeleri hello **Microsoft.Common** ad alanı temelleri kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="59f6a-123">Generally, only elements in hello **Microsoft.Common** namespace can be used in basics.</span></span> <span data-ttu-id="59f6a-124">Ancak bazı öğeler diğer ad (gibi **Microsoft.Compute.Credentials**), kullanıcının Merhaba içeriğine bağlı verme, hala izin verilir.</span><span class="sxs-lookup"><span data-stu-id="59f6a-124">Although some elements in other namespaces (like **Microsoft.Compute.Credentials**) that don't depend on hello user's context, are still allowed.</span></span>

## <a name="steps"></a><span data-ttu-id="59f6a-125">Adımlar</span><span class="sxs-lookup"><span data-stu-id="59f6a-125">Steps</span></span>
<span data-ttu-id="59f6a-126">Merhaba adımları özellik sıfır veya daha fazla ek adımlar toodisplay her biri bir veya daha fazla öğe içeren temel bilgileri sonra içerebilir.</span><span class="sxs-lookup"><span data-stu-id="59f6a-126">hello steps property can contain zero or more additional steps toodisplay after basics, each of which contains one or more elements.</span></span> <span data-ttu-id="59f6a-127">Rol veya dağıtılan hello uygulama katmanı başına adımları eklemeyi düşünün.</span><span class="sxs-lookup"><span data-stu-id="59f6a-127">Consider adding steps per role or tier of hello application being deployed.</span></span> <span data-ttu-id="59f6a-128">Örneğin, bir adım hello ana düğüm girdileri için ve adım hello çalışan düğümleri için bir kümede ekleyin.</span><span class="sxs-lookup"><span data-stu-id="59f6a-128">For example, add a step for inputs for hello master nodes, and a step for hello worker nodes in a cluster.</span></span>

## <a name="outputs"></a><span data-ttu-id="59f6a-129">Çıkışları</span><span class="sxs-lookup"><span data-stu-id="59f6a-129">Outputs</span></span>
<span data-ttu-id="59f6a-130">Hello Azure portal kullanır hello `outputs` özelliği toomap öğelerinden `basics` ve `steps` hello Azure Resource Manager dağıtım şablonu toohello parametreleri.</span><span class="sxs-lookup"><span data-stu-id="59f6a-130">hello Azure portal uses hello `outputs` property toomap elements from `basics` and `steps` toohello parameters of hello Azure Resource Manager deployment template.</span></span> <span data-ttu-id="59f6a-131">Bu sözlüğün anahtarlarını Hello hello şablon parametrelerinin hello adlarının ve başvurulan hello öğelerden hello çıkış nesnelerin özelliklerini hello değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="59f6a-131">hello keys of this dictionary are hello names of hello template parameters, and hello values are properties of hello output objects from hello referenced elements.</span></span>

## <a name="functions"></a><span data-ttu-id="59f6a-132">İşlevler</span><span class="sxs-lookup"><span data-stu-id="59f6a-132">Functions</span></span>
<span data-ttu-id="59f6a-133">Benzer çok[şablon işlevleri](resource-group-template-functions.md) Azure Kaynak Yöneticisi'nde (hem de söz dizimi ve işlevsellik) CreateUiDefinition öğeleri girişleri ve çıkışları ile çalışmak için işlevleri sağlayan yanı sıra koşulları gibi özellikleri.</span><span class="sxs-lookup"><span data-stu-id="59f6a-133">Similar too[template functions](resource-group-template-functions.md) in Azure Resource Manager (both in syntax and functionality), CreateUiDefinition provides functions for working with elements' inputs and outputs, as well as features such as conditionals.</span></span>

## <a name="next-steps"></a><span data-ttu-id="59f6a-134">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="59f6a-134">Next steps</span></span>
<span data-ttu-id="59f6a-135">CreateUiDefinition kendisini basit bir şeması vardır.</span><span class="sxs-lookup"><span data-stu-id="59f6a-135">CreateUiDefinition itself has a simple schema.</span></span> <span data-ttu-id="59f6a-136">Hello gerçek derinliğini, tüm desteklenen hello öğeleri ve İşlevler, belgeleri aşağıdaki hangi hello wondrous ayrıntılı olarak açıklayın gelir:</span><span class="sxs-lookup"><span data-stu-id="59f6a-136">hello real depth of it comes from all hello supported elements and functions, which hello following documents describe in wondrous detail:</span></span>

- [<span data-ttu-id="59f6a-137">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="59f6a-137">Elements</span></span>](managed-application-createuidefinition-elements.md)
- [<span data-ttu-id="59f6a-138">İşlevler</span><span class="sxs-lookup"><span data-stu-id="59f6a-138">Functions</span></span>](managed-application-createuidefinition-functions.md)

<span data-ttu-id="59f6a-139">CreateUiDefinition için geçerli bir JSON şeması burada bulunur: https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json.</span><span class="sxs-lookup"><span data-stu-id="59f6a-139">A current JSON schema for CreateUiDefinition is available here: https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json.</span></span> 

<span data-ttu-id="59f6a-140">Sonraki sürümlerinde kullanılabilir hello aynı konumu.</span><span class="sxs-lookup"><span data-stu-id="59f6a-140">Later versions will be available at hello same location.</span></span> <span data-ttu-id="59f6a-141">Hello yerine `0.1.2-preview` hello URL ve hello bölümünü `version` değeri toouse düşündüğünüz hello sürüm tanımlayıcısına sahip.</span><span class="sxs-lookup"><span data-stu-id="59f6a-141">Replace hello `0.1.2-preview` portion of hello URL and hello `version` value with hello version identifier you intend toouse.</span></span> <span data-ttu-id="59f6a-142">şu anda desteklenen hello sürüm tanımlayıcılardır `0.0.1-preview`, `0.1.0-preview`, `0.1.1-preview`, ve `0.1.2-preview`.</span><span class="sxs-lookup"><span data-stu-id="59f6a-142">hello currently supported version identifiers are `0.0.1-preview`, `0.1.0-preview`, `0.1.1-preview`, and `0.1.2-preview`.</span></span>
