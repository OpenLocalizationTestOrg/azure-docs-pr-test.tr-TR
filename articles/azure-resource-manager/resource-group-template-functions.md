---
title: "aaaResource Manager şablonu işlevleri | Microsoft Docs"
description: "Hello işlevleri toouse açıklayan bir Azure Resource Manager şablonu tooretrieve değerlerini iş dizeler ve sayısal türler ile ve dağıtım bilgilerini almak."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 0644abe1-abaa-443d-820d-1966d7d26bfd
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: tomfitz
ms.openlocfilehash: d1b2e68a33d75058f83d6972dadb33a6390d49b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-manager-template-functions"></a><span data-ttu-id="54100-103">Azure Resource Manager şablonu işlevleri</span><span class="sxs-lookup"><span data-stu-id="54100-103">Azure Resource Manager template functions</span></span>
<span data-ttu-id="54100-104">Bu konuda, bir Azure Resource Manager şablonunda kullanabileceğiniz tüm hello işlevler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="54100-104">This topic describes all hello functions you can use in an Azure Resource Manager template.</span></span>

<span data-ttu-id="54100-105">Köşeli ayraç içinde yazarak, şablonlarda işlevler eklemek: `[` ve `]`sırasıyla.</span><span class="sxs-lookup"><span data-stu-id="54100-105">You add functions in your templates by enclosing them within brackets: `[` and `]`, respectively.</span></span> <span data-ttu-id="54100-106">Merhaba ifade dağıtımı sırasında değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="54100-106">hello expression is evaluated during deployment.</span></span> <span data-ttu-id="54100-107">Bir dize yazılmış olsa da, hello ifade değerlendirme hello sonucunu bir dizi, nesne veya tamsayı gibi farklı bir JSON türde olabilir.</span><span class="sxs-lookup"><span data-stu-id="54100-107">While written as a string literal, hello result of evaluating hello expression can be of a different JSON type, such as an array, object, or integer.</span></span> <span data-ttu-id="54100-108">JavaScript'te, işlev çağrıları olarak biçimlendirilmiş gibi yalnızca `functionName(arg1,arg2,arg3)`.</span><span class="sxs-lookup"><span data-stu-id="54100-108">Just like in JavaScript, function calls are formatted as `functionName(arg1,arg2,arg3)`.</span></span> <span data-ttu-id="54100-109">Özellikler hello nokta ve [dizin] işleçleri kullanarak başvuru.</span><span class="sxs-lookup"><span data-stu-id="54100-109">You reference properties by using hello dot and [index] operators.</span></span>

<span data-ttu-id="54100-110">Bir şablon ifadesi 24.576 karakterden uzun olamaz.</span><span class="sxs-lookup"><span data-stu-id="54100-110">A template expression cannot exceed 24,576 characters.</span></span>

<span data-ttu-id="54100-111">Şablon işlevleri ve bunların parametrelerini büyük/küçük harf duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="54100-111">Template functions and their parameters are case-insensitive.</span></span> <span data-ttu-id="54100-112">Örneğin, Resource Manager çözümler **variables('var1')** ve **VARIABLES('VAR1')** aynı hello gibi.</span><span class="sxs-lookup"><span data-stu-id="54100-112">For example, Resource Manager resolves **variables('var1')** and **VARIABLES('VAR1')** as hello same.</span></span> <span data-ttu-id="54100-113">Değerlendirildiğinde, hello işlevi açıkça durumda (örneğin, toUpper veya toLower) değiştirir sürece hello işlevi hello çalışması korur.</span><span class="sxs-lookup"><span data-stu-id="54100-113">When evaluated, unless hello function expressly modifies case (such as toUpper or toLower), hello function preserves hello case.</span></span> <span data-ttu-id="54100-114">Belirli kaynak türlerine işlevleri nasıl değerlendirildiği yedeklemiş servis talebi gereksinimleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="54100-114">Certain resource types may have case requirements irrespective of how functions are evaluated.</span></span>

<a id="array" />
<a id="coalesce" />
<a id="concatarray" />
<a id="contains" />
<a id="createarray" />
<a id="empty" />
<a id="first" />
<a id="intersection" />
<a id="last" />
<a id="length" />
<a id="min" />
<a id="max" />
<a id="range" />
<a id="skip" />
<a id="take" />
<a id="union" />

## <a name="array-and-object-functions"></a><span data-ttu-id="54100-115">Dizi ve nesne işlevleri</span><span class="sxs-lookup"><span data-stu-id="54100-115">Array and object functions</span></span>
<span data-ttu-id="54100-116">Kaynak Yöneticisi, nesneler ve diziler ile çalışmak için birkaç işlevleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="54100-116">Resource Manager provides several functions for working with arrays and objects.</span></span>

* [<span data-ttu-id="54100-117">dizi</span><span class="sxs-lookup"><span data-stu-id="54100-117">array</span></span>](resource-group-template-functions-array.md#array)
* [<span data-ttu-id="54100-118">birleşim</span><span class="sxs-lookup"><span data-stu-id="54100-118">coalesce</span></span>](resource-group-template-functions-array.md#coalesce)
* [<span data-ttu-id="54100-119">concat</span><span class="sxs-lookup"><span data-stu-id="54100-119">concat</span></span>](resource-group-template-functions-array.md#concat)
* [<span data-ttu-id="54100-120">içerir</span><span class="sxs-lookup"><span data-stu-id="54100-120">contains</span></span>](resource-group-template-functions-array.md#contains)
* [<span data-ttu-id="54100-121">createArray</span><span class="sxs-lookup"><span data-stu-id="54100-121">createArray</span></span>](resource-group-template-functions-array.md#createarray)
* [<span data-ttu-id="54100-122">boş</span><span class="sxs-lookup"><span data-stu-id="54100-122">empty</span></span>](resource-group-template-functions-array.md#empty)
* [<span data-ttu-id="54100-123">ilk</span><span class="sxs-lookup"><span data-stu-id="54100-123">first</span></span>](resource-group-template-functions-array.md#first)
* [<span data-ttu-id="54100-124">kesişim</span><span class="sxs-lookup"><span data-stu-id="54100-124">intersection</span></span>](resource-group-template-functions-array.md#intersection)
* [<span data-ttu-id="54100-125">JSON</span><span class="sxs-lookup"><span data-stu-id="54100-125">json</span></span>](resource-group-template-functions-array.md#json)
* [<span data-ttu-id="54100-126">Son</span><span class="sxs-lookup"><span data-stu-id="54100-126">last</span></span>](resource-group-template-functions-array.md#last)
* [<span data-ttu-id="54100-127">uzunluğu</span><span class="sxs-lookup"><span data-stu-id="54100-127">length</span></span>](resource-group-template-functions-array.md#length)
* [<span data-ttu-id="54100-128">Min</span><span class="sxs-lookup"><span data-stu-id="54100-128">min</span></span>](resource-group-template-functions-array.md#min)
* [<span data-ttu-id="54100-129">max</span><span class="sxs-lookup"><span data-stu-id="54100-129">max</span></span>](resource-group-template-functions-array.md#max)
* [<span data-ttu-id="54100-130">Aralık</span><span class="sxs-lookup"><span data-stu-id="54100-130">range</span></span>](resource-group-template-functions-array.md#range)
* [<span data-ttu-id="54100-131">Atla</span><span class="sxs-lookup"><span data-stu-id="54100-131">skip</span></span>](resource-group-template-functions-array.md#skip)
* [<span data-ttu-id="54100-132">Al</span><span class="sxs-lookup"><span data-stu-id="54100-132">take</span></span>](resource-group-template-functions-array.md#take)
* [<span data-ttu-id="54100-133">birleşim</span><span class="sxs-lookup"><span data-stu-id="54100-133">union</span></span>](resource-group-template-functions-array.md#union)

<a id="equals" />
<a id="less" />
<a id="lessorequals" />
<a id="greater" />
<a id="greaterorequals" />

## <a name="comparison-functions"></a><span data-ttu-id="54100-134">Karşılaştırma işlevleri</span><span class="sxs-lookup"><span data-stu-id="54100-134">Comparison functions</span></span>
<span data-ttu-id="54100-135">Resource Manager şablonlarınızı içinde karşılaştırmaları yapmak için çeşitli işlevleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="54100-135">Resource Manager provides several functions for making comparisons in your templates.</span></span>

* [<span data-ttu-id="54100-136">eşittir</span><span class="sxs-lookup"><span data-stu-id="54100-136">equals</span></span>](resource-group-template-functions-comparison.md#equals)
* [<span data-ttu-id="54100-137">daha az</span><span class="sxs-lookup"><span data-stu-id="54100-137">less</span></span>](resource-group-template-functions-comparison.md#less)
* [<span data-ttu-id="54100-138">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="54100-138">lessOrEquals</span></span>](resource-group-template-functions-comparison.md#lessorequals)
* [<span data-ttu-id="54100-139">büyük</span><span class="sxs-lookup"><span data-stu-id="54100-139">greater</span></span>](resource-group-template-functions-comparison.md#greater)
* [<span data-ttu-id="54100-140">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="54100-140">greaterOrEquals</span></span>](resource-group-template-functions-comparison.md#greaterorequals)

<a id="deployment" />
<a id="parameters" />
<a id="variables" />

## <a name="deployment-value-functions"></a><span data-ttu-id="54100-141">Dağıtım değer işlevleri</span><span class="sxs-lookup"><span data-stu-id="54100-141">Deployment value functions</span></span>
<span data-ttu-id="54100-142">Resource Manager hello aşağıdaki değerleri hello şablon bölümlerinden alma için İşlevler ve ilgili toohello dağıtım değerleri sunar:</span><span class="sxs-lookup"><span data-stu-id="54100-142">Resource Manager provides hello following functions for getting values from sections of hello template and values related toohello deployment:</span></span>

* [<span data-ttu-id="54100-143">Dağıtım</span><span class="sxs-lookup"><span data-stu-id="54100-143">deployment</span></span>](resource-group-template-functions-deployment.md#deployment)
* [<span data-ttu-id="54100-144">parametreleri</span><span class="sxs-lookup"><span data-stu-id="54100-144">parameters</span></span>](resource-group-template-functions-deployment.md#parameters)
* [<span data-ttu-id="54100-145">değişkenleri</span><span class="sxs-lookup"><span data-stu-id="54100-145">variables</span></span>](resource-group-template-functions-deployment.md#variables)

<a id="add" />
<a id="copyindex" />
<a id="div" />
<a id="float" />
<a id="int" />
<a id="minint" />
<a id="maxint" />
<a id="mod" />
<a id="mul" />
<a id="sub" />

## <a name="logical-functions"></a><span data-ttu-id="54100-146">Mantıksal işlevleri</span><span class="sxs-lookup"><span data-stu-id="54100-146">Logical functions</span></span>
<span data-ttu-id="54100-147">Resource Manager işlevleri mantıksal koşulları ile çalışmak için aşağıdaki hello sunar:</span><span class="sxs-lookup"><span data-stu-id="54100-147">Resource Manager provides hello following functions for working with logical conditions:</span></span>

* [<span data-ttu-id="54100-148">ve</span><span class="sxs-lookup"><span data-stu-id="54100-148">and</span></span>](resource-group-template-functions-logical.md#and)
* [<span data-ttu-id="54100-149">bool</span><span class="sxs-lookup"><span data-stu-id="54100-149">bool</span></span>](resource-group-template-functions-logical.md#bool)
* [<span data-ttu-id="54100-150">Eğer</span><span class="sxs-lookup"><span data-stu-id="54100-150">if</span></span>](resource-group-template-functions-logical.md#if)
* [<span data-ttu-id="54100-151">değil</span><span class="sxs-lookup"><span data-stu-id="54100-151">not</span></span>](resource-group-template-functions-logical.md#not)
* [<span data-ttu-id="54100-152">veya</span><span class="sxs-lookup"><span data-stu-id="54100-152">or</span></span>](resource-group-template-functions-logical.md#or)

## <a name="numeric-functions"></a><span data-ttu-id="54100-153">Sayısal İşlevler</span><span class="sxs-lookup"><span data-stu-id="54100-153">Numeric functions</span></span>
<span data-ttu-id="54100-154">Resource Manager hello şu tamsayıları ile çalışmak için işlevleri sunar:</span><span class="sxs-lookup"><span data-stu-id="54100-154">Resource Manager provides hello following functions for working with integers:</span></span>

* [<span data-ttu-id="54100-155">ekleme</span><span class="sxs-lookup"><span data-stu-id="54100-155">add</span></span>](resource-group-template-functions-numeric.md#add)
* [<span data-ttu-id="54100-156">Copyındex</span><span class="sxs-lookup"><span data-stu-id="54100-156">copyIndex</span></span>](resource-group-template-functions-numeric.md#copyindex)
* [<span data-ttu-id="54100-157">div</span><span class="sxs-lookup"><span data-stu-id="54100-157">div</span></span>](resource-group-template-functions-numeric.md#div)
* [<span data-ttu-id="54100-158">kayan nokta</span><span class="sxs-lookup"><span data-stu-id="54100-158">float</span></span>](resource-group-template-functions-numeric.md#float)
* [<span data-ttu-id="54100-159">int</span><span class="sxs-lookup"><span data-stu-id="54100-159">int</span></span>](resource-group-template-functions-numeric.md#int)
* [<span data-ttu-id="54100-160">Min</span><span class="sxs-lookup"><span data-stu-id="54100-160">min</span></span>](resource-group-template-functions-numeric.md#min)
* [<span data-ttu-id="54100-161">max</span><span class="sxs-lookup"><span data-stu-id="54100-161">max</span></span>](resource-group-template-functions-numeric.md#max)
* [<span data-ttu-id="54100-162">mod</span><span class="sxs-lookup"><span data-stu-id="54100-162">mod</span></span>](resource-group-template-functions-numeric.md#mod)
* [<span data-ttu-id="54100-163">mul</span><span class="sxs-lookup"><span data-stu-id="54100-163">mul</span></span>](resource-group-template-functions-numeric.md#mul)
* [<span data-ttu-id="54100-164">Sub</span><span class="sxs-lookup"><span data-stu-id="54100-164">sub</span></span>](resource-group-template-functions-numeric.md#sub)

<a id="listkeys" />
<a id="list" />
<a id="providers" />
<a id="reference" />
<a id="resourcegroup" />
<a id="resourceid" />
<a id="subscription" />

## <a name="resource-functions"></a><span data-ttu-id="54100-165">Kaynak işlevleri</span><span class="sxs-lookup"><span data-stu-id="54100-165">Resource functions</span></span>
<span data-ttu-id="54100-166">Resource Manager kaynak değerlerini alma işlevleri aşağıdaki hello sunar:</span><span class="sxs-lookup"><span data-stu-id="54100-166">Resource Manager provides hello following functions for getting resource values:</span></span>

* [<span data-ttu-id="54100-167">listKeys ve liste {Value}</span><span class="sxs-lookup"><span data-stu-id="54100-167">listKeys and list{Value}</span></span>](resource-group-template-functions-resource.md#listkeys)
* [<span data-ttu-id="54100-168">sağlayıcıları</span><span class="sxs-lookup"><span data-stu-id="54100-168">providers</span></span>](resource-group-template-functions-resource.md#providers)
* [<span data-ttu-id="54100-169">başvuru</span><span class="sxs-lookup"><span data-stu-id="54100-169">reference</span></span>](resource-group-template-functions-resource.md#reference)
* [<span data-ttu-id="54100-170">kaynak grubu</span><span class="sxs-lookup"><span data-stu-id="54100-170">resourceGroup</span></span>](resource-group-template-functions-resource.md#resourcegroup)
* [<span data-ttu-id="54100-171">ResourceId</span><span class="sxs-lookup"><span data-stu-id="54100-171">resourceId</span></span>](resource-group-template-functions-resource.md#resourceid)
* [<span data-ttu-id="54100-172">aboneliği</span><span class="sxs-lookup"><span data-stu-id="54100-172">subscription</span></span>](resource-group-template-functions-resource.md#subscription)

<a id="base64" />
<a id="base64tojson" />
<a id="base64tostring" />
<a id="concat" />
<a id="containsstring" />
<a id="datauri" />
<a id="datauritostring" />
<a id="emptystring" />
<a id="endswith" />
<a id="firststring" />
<a id="indexof" />
<a id="laststring" />
<a id="lastindexof" />
<a id="lengthstring" />
<a id="padleft" />
<a id="replace" />
<a id="skipstring" />
<a id="split" />
<a id="startswith" />
<a id="string" />
<a id="substring" />
<a id="takestring" />
<a id="tolower" />
<a id="toupper" />
<a id="trim" />
<a id="uniquestring" />
<a id="uri" />
<a id="uricomponent" />
<a id="uricomponenttostring" />

## <a name="string-functions"></a><span data-ttu-id="54100-173">Dize işlevleri</span><span class="sxs-lookup"><span data-stu-id="54100-173">String functions</span></span>
<span data-ttu-id="54100-174">Resource Manager Dizelerle çalışmaya yönelik işlevler aşağıdaki hello sunar:</span><span class="sxs-lookup"><span data-stu-id="54100-174">Resource Manager provides hello following functions for working with strings:</span></span>

* [<span data-ttu-id="54100-175">Base64</span><span class="sxs-lookup"><span data-stu-id="54100-175">base64</span></span>](resource-group-template-functions-string.md#base64)
* [<span data-ttu-id="54100-176">base64ToJson</span><span class="sxs-lookup"><span data-stu-id="54100-176">base64ToJson</span></span>](resource-group-template-functions-string.md#base64tojson)
* [<span data-ttu-id="54100-177">base64ToString</span><span class="sxs-lookup"><span data-stu-id="54100-177">base64ToString</span></span>](resource-group-template-functions-string.md#base64tostring)
* [<span data-ttu-id="54100-178">concat</span><span class="sxs-lookup"><span data-stu-id="54100-178">concat</span></span>](resource-group-template-functions-string.md#concat)
* [<span data-ttu-id="54100-179">içerir</span><span class="sxs-lookup"><span data-stu-id="54100-179">contains</span></span>](resource-group-template-functions-string.md#contains)
* [<span data-ttu-id="54100-180">dataUri</span><span class="sxs-lookup"><span data-stu-id="54100-180">dataUri</span></span>](resource-group-template-functions-string.md#datauri)
* [<span data-ttu-id="54100-181">dataUriToString</span><span class="sxs-lookup"><span data-stu-id="54100-181">dataUriToString</span></span>](resource-group-template-functions-string.md#datauritostring)
* [<span data-ttu-id="54100-182">boş</span><span class="sxs-lookup"><span data-stu-id="54100-182">empty</span></span>](resource-group-template-functions-string.md#empty)
* [<span data-ttu-id="54100-183">endsWith</span><span class="sxs-lookup"><span data-stu-id="54100-183">endsWith</span></span>](resource-group-template-functions-string.md#endswith)
* [<span data-ttu-id="54100-184">ilk</span><span class="sxs-lookup"><span data-stu-id="54100-184">first</span></span>](resource-group-template-functions-string.md#first)
* [<span data-ttu-id="54100-185">IndexOf</span><span class="sxs-lookup"><span data-stu-id="54100-185">indexOf</span></span>](resource-group-template-functions-string.md#indexof)
* [<span data-ttu-id="54100-186">Son</span><span class="sxs-lookup"><span data-stu-id="54100-186">last</span></span>](resource-group-template-functions-string.md#last)
* [<span data-ttu-id="54100-187">lastIndexOf</span><span class="sxs-lookup"><span data-stu-id="54100-187">lastIndexOf</span></span>](resource-group-template-functions-string.md#lastindexof)
* [<span data-ttu-id="54100-188">uzunluğu</span><span class="sxs-lookup"><span data-stu-id="54100-188">length</span></span>](resource-group-template-functions-string.md#length)
* [<span data-ttu-id="54100-189">padLeft</span><span class="sxs-lookup"><span data-stu-id="54100-189">padLeft</span></span>](resource-group-template-functions-string.md#padleft)
* [<span data-ttu-id="54100-190">Değiştir</span><span class="sxs-lookup"><span data-stu-id="54100-190">replace</span></span>](resource-group-template-functions-string.md#replace)
* [<span data-ttu-id="54100-191">Atla</span><span class="sxs-lookup"><span data-stu-id="54100-191">skip</span></span>](resource-group-template-functions-string.md#skip)
* [<span data-ttu-id="54100-192">split</span><span class="sxs-lookup"><span data-stu-id="54100-192">split</span></span>](resource-group-template-functions-string.md#split)
* [<span data-ttu-id="54100-193">startsWith</span><span class="sxs-lookup"><span data-stu-id="54100-193">startsWith</span></span>](resource-group-template-functions-string.md#startswith)
* [<span data-ttu-id="54100-194">dize</span><span class="sxs-lookup"><span data-stu-id="54100-194">string</span></span>](resource-group-template-functions-string.md#string)
* [<span data-ttu-id="54100-195">substring</span><span class="sxs-lookup"><span data-stu-id="54100-195">substring</span></span>](resource-group-template-functions-string.md#substring)
* [<span data-ttu-id="54100-196">Al</span><span class="sxs-lookup"><span data-stu-id="54100-196">take</span></span>](resource-group-template-functions-string.md#take)
* [<span data-ttu-id="54100-197">toLower</span><span class="sxs-lookup"><span data-stu-id="54100-197">toLower</span></span>](resource-group-template-functions-string.md#tolower)
* [<span data-ttu-id="54100-198">toUpper</span><span class="sxs-lookup"><span data-stu-id="54100-198">toUpper</span></span>](resource-group-template-functions-string.md#toupper)
* [<span data-ttu-id="54100-199">Kırpma</span><span class="sxs-lookup"><span data-stu-id="54100-199">trim</span></span>](resource-group-template-functions-string.md#trim)
* [<span data-ttu-id="54100-200">uniqueString</span><span class="sxs-lookup"><span data-stu-id="54100-200">uniqueString</span></span>](resource-group-template-functions-string.md#uniquestring)
* [<span data-ttu-id="54100-201">URI</span><span class="sxs-lookup"><span data-stu-id="54100-201">uri</span></span>](resource-group-template-functions-string.md#uri)
* [<span data-ttu-id="54100-202">uriComponent</span><span class="sxs-lookup"><span data-stu-id="54100-202">uriComponent</span></span>](resource-group-template-functions-string.md#uricomponent)
* [<span data-ttu-id="54100-203">uriComponentToString</span><span class="sxs-lookup"><span data-stu-id="54100-203">uriComponentToString</span></span>](resource-group-template-functions-string.md#uricomponenttostring)


## <a name="next-steps"></a><span data-ttu-id="54100-204">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="54100-204">Next steps</span></span>
* <span data-ttu-id="54100-205">Bir Azure Resource Manager şablonu hello bölümlerde açıklaması için bkz: [Azure Resource Manager şablonları yazma](resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="54100-205">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md)</span></span>
* <span data-ttu-id="54100-206">birden fazla şablon toomerge bakın [Azure Resource Manager ile bağlı şablonları kullanma](resource-group-linked-templates.md)</span><span class="sxs-lookup"><span data-stu-id="54100-206">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md)</span></span>
* <span data-ttu-id="54100-207">tooiterate belirtilen sayıda kaynak türünü oluştururken, bkz: [Azure Resource Manager'da kaynakları birden çok örneğini oluşturma](resource-group-create-multiple.md)</span><span class="sxs-lookup"><span data-stu-id="54100-207">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md)</span></span>
* <span data-ttu-id="54100-208">toodeploy hello şablonu oluşturduğunuz toosee bkz [Azure Resource Manager şablonu ile bir uygulamayı dağıtma](resource-group-template-deploy.md)</span><span class="sxs-lookup"><span data-stu-id="54100-208">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md)</span></span>

