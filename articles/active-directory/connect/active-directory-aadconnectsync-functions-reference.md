---
title: "Azure AD Connect eşitleme: işlevleri başvurusu | Microsoft Docs"
description: "Azure AD Connect eşitleme bildirim temelli hazırlama ifadelerini başvuru."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 4f525ca0-be0e-4a2e-8da1-09b6b567ed5f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 926f52ef64eb79205dbfb344edc7d9bece2a6947
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-functions-reference"></a><span data-ttu-id="3d184-103">Azure AD Connect eşitleme: işlevleri başvurusu</span><span class="sxs-lookup"><span data-stu-id="3d184-103">Azure AD Connect sync: Functions Reference</span></span>
<span data-ttu-id="3d184-104">Azure AD Connect işlevleri eşitleme sırasında bir öznitelik değeri işlemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3d184-104">In Azure AD Connect, functions are used to manipulate an attribute value during synchronization.</span></span>  
<span data-ttu-id="3d184-105">İşlevler söz dizimi aşağıdaki biçimi kullanarak ifade edilir:</span><span class="sxs-lookup"><span data-stu-id="3d184-105">The Syntax of the functions is expressed using the following format:</span></span>  
`<output type> FunctionName(<input type> <position name>, ..)`

<span data-ttu-id="3d184-106">İşlev aşırı yüklendi ve birden çok sözdizimleri kabul eder, tüm geçerli sözdizimi listelenir.</span><span class="sxs-lookup"><span data-stu-id="3d184-106">If a function is overloaded and accepts multiple syntaxes, all valid syntaxes are listed.</span></span>  
<span data-ttu-id="3d184-107">İşlevler kesin türü belirtilmiş ve türü belgelenen türü eşleştiğinden geçirilen doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="3d184-107">The functions are strongly typed and they verify that the type passed in matches the documented type.</span></span>  
<span data-ttu-id="3d184-108">Türü eşleşmiyorsa, bir hata oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="3d184-108">If the type does not match, an error is thrown.</span></span>

<span data-ttu-id="3d184-109">Türleri, aşağıdaki sözdizimi ile ifade edilir:</span><span class="sxs-lookup"><span data-stu-id="3d184-109">The types are expressed with the following syntax:</span></span>

* <span data-ttu-id="3d184-110">**Depo** – ikili</span><span class="sxs-lookup"><span data-stu-id="3d184-110">**bin** – Binary</span></span>
* <span data-ttu-id="3d184-111">**bool** – Boole</span><span class="sxs-lookup"><span data-stu-id="3d184-111">**bool** – Boolean</span></span>
* <span data-ttu-id="3d184-112">**dt** – UTC tarihi/saati</span><span class="sxs-lookup"><span data-stu-id="3d184-112">**dt** – UTC Date/Time</span></span>
* <span data-ttu-id="3d184-113">**Enum** – bilinen sabitleri numaralandırması</span><span class="sxs-lookup"><span data-stu-id="3d184-113">**enum** – Enumeration of known constants</span></span>
* <span data-ttu-id="3d184-114">**exp** – bir Boole değeri değerlendirmek için beklenen ifade</span><span class="sxs-lookup"><span data-stu-id="3d184-114">**exp** – Expression, which is expected to evaluate to a Boolean</span></span>
* <span data-ttu-id="3d184-115">**mvbin** – birden çok değerli ikili</span><span class="sxs-lookup"><span data-stu-id="3d184-115">**mvbin** – Multi-Valued Binary</span></span>
* <span data-ttu-id="3d184-116">**mvstr** – birden çok değerli dize</span><span class="sxs-lookup"><span data-stu-id="3d184-116">**mvstr** – Multi-Valued String</span></span>
* <span data-ttu-id="3d184-117">**mvref** – birden çok değerli başvurusu</span><span class="sxs-lookup"><span data-stu-id="3d184-117">**mvref** – Multi-Valued Reference</span></span>
* <span data-ttu-id="3d184-118">**NUM** – sayısal</span><span class="sxs-lookup"><span data-stu-id="3d184-118">**num** – Numeric</span></span>
* <span data-ttu-id="3d184-119">**Ref** – başvurusu</span><span class="sxs-lookup"><span data-stu-id="3d184-119">**ref** – Reference</span></span>
* <span data-ttu-id="3d184-120">**str** – dize</span><span class="sxs-lookup"><span data-stu-id="3d184-120">**str** – String</span></span>
* <span data-ttu-id="3d184-121">**var** – bir değişken (neredeyse) herhangi bir tür</span><span class="sxs-lookup"><span data-stu-id="3d184-121">**var** – A variant of (almost) any other type</span></span>
* <span data-ttu-id="3d184-122">**void** – bir değer döndürmüyor</span><span class="sxs-lookup"><span data-stu-id="3d184-122">**void** – doesn’t return a value</span></span>

<span data-ttu-id="3d184-123">İşlevler türleriyle **mvbin**, **mvstr**, ve **mvref** birden çok değerli öznitelikleri yalnızca çalışabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3d184-123">The functions with the types **mvbin**, **mvstr**, and **mvref** can only work on multi-valued attributes.</span></span> <span data-ttu-id="3d184-124">İle işlevleri **bin**, **str**, ve **ref** hem tek değerli ve birden çok değerli öznitelikleri üzerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="3d184-124">Functions with **bin**, **str**, and **ref** work on both single-valued and multi-valued attributes.</span></span>

## <a name="functions-reference"></a><span data-ttu-id="3d184-125">İşlevler Başvurusu</span><span class="sxs-lookup"><span data-stu-id="3d184-125">Functions Reference</span></span>
| <span data-ttu-id="3d184-126">İşlevlerin listesi</span><span class="sxs-lookup"><span data-stu-id="3d184-126">List of functions</span></span> |  |  |  |  |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="3d184-127">**Sertifika**</span><span class="sxs-lookup"><span data-stu-id="3d184-127">**Certificate**</span></span> | | | | |
| [<span data-ttu-id="3d184-128">CertExtensionOids</span><span class="sxs-lookup"><span data-stu-id="3d184-128">CertExtensionOids</span></span>](#certextensionoids) |[<span data-ttu-id="3d184-129">CertFormat</span><span class="sxs-lookup"><span data-stu-id="3d184-129">CertFormat</span></span>](#certformat) |[<span data-ttu-id="3d184-130">CertFriendlyName</span><span class="sxs-lookup"><span data-stu-id="3d184-130">CertFriendlyName</span></span>](#certfriendlyname) |[<span data-ttu-id="3d184-131">CertHashString</span><span class="sxs-lookup"><span data-stu-id="3d184-131">CertHashString</span></span>](#certhashstring) | |
| [<span data-ttu-id="3d184-132">CertIssuer</span><span class="sxs-lookup"><span data-stu-id="3d184-132">CertIssuer</span></span>](#certissuer) |[<span data-ttu-id="3d184-133">CertIssuerDN</span><span class="sxs-lookup"><span data-stu-id="3d184-133">CertIssuerDN</span></span>](#certissuerdn) |[<span data-ttu-id="3d184-134">CertIssuerOid</span><span class="sxs-lookup"><span data-stu-id="3d184-134">CertIssuerOid</span></span>](#certissueroid) |[<span data-ttu-id="3d184-135">CertKeyAlgorithm</span><span class="sxs-lookup"><span data-stu-id="3d184-135">CertKeyAlgorithm</span></span>](#certkeyalgorithm) | |
| [<span data-ttu-id="3d184-136">CertKeyAlgorithmParams</span><span class="sxs-lookup"><span data-stu-id="3d184-136">CertKeyAlgorithmParams</span></span>](#certkeyalgorithmparams) |[<span data-ttu-id="3d184-137">CertNameInfo</span><span class="sxs-lookup"><span data-stu-id="3d184-137">CertNameInfo</span></span>](#certnameinfo) |[<span data-ttu-id="3d184-138">CertNotAfter</span><span class="sxs-lookup"><span data-stu-id="3d184-138">CertNotAfter</span></span>](#certnotafter) |[<span data-ttu-id="3d184-139">CertNotBefore</span><span class="sxs-lookup"><span data-stu-id="3d184-139">CertNotBefore</span></span>](#certnotbefore) | |
| [<span data-ttu-id="3d184-140">CertPublicKeyOid</span><span class="sxs-lookup"><span data-stu-id="3d184-140">CertPublicKeyOid</span></span>](#certpublickeyoid) |[<span data-ttu-id="3d184-141">CertPublicKeyParametersOid</span><span class="sxs-lookup"><span data-stu-id="3d184-141">CertPublicKeyParametersOid</span></span>](#certpublickeyparametersoid) |[<span data-ttu-id="3d184-142">CertSerialNumber</span><span class="sxs-lookup"><span data-stu-id="3d184-142">CertSerialNumber</span></span>](#certserialnumber) |[<span data-ttu-id="3d184-143">CertSignatureAlgorithmOid</span><span class="sxs-lookup"><span data-stu-id="3d184-143">CertSignatureAlgorithmOid</span></span>](#certsignaturealgorithmoid) | |
| [<span data-ttu-id="3d184-144">CertSubject</span><span class="sxs-lookup"><span data-stu-id="3d184-144">CertSubject</span></span>](#certsubject) |[<span data-ttu-id="3d184-145">CertSubjectNameDN</span><span class="sxs-lookup"><span data-stu-id="3d184-145">CertSubjectNameDN</span></span>](#certsubjectnamedn) |[<span data-ttu-id="3d184-146">CertSubjectNameOid</span><span class="sxs-lookup"><span data-stu-id="3d184-146">CertSubjectNameOid</span></span>](#certsubjectnameoid) |[<span data-ttu-id="3d184-147">Certthumbprınt</span><span class="sxs-lookup"><span data-stu-id="3d184-147">CertThumbprint</span></span>](#certthumbprint) | |
[<span data-ttu-id="3d184-148">CertVersion</span><span class="sxs-lookup"><span data-stu-id="3d184-148"> CertVersion</span></span>](#certversion) |[<span data-ttu-id="3d184-149">IsCert</span><span class="sxs-lookup"><span data-stu-id="3d184-149">IsCert</span></span>](#iscert) | | | |
| <span data-ttu-id="3d184-150">**Dönüştürme**</span><span class="sxs-lookup"><span data-stu-id="3d184-150">**Conversion**</span></span> | | | | |
| [<span data-ttu-id="3d184-151">CBool</span><span class="sxs-lookup"><span data-stu-id="3d184-151">CBool</span></span>](#cbool) |[<span data-ttu-id="3d184-152">CDate</span><span class="sxs-lookup"><span data-stu-id="3d184-152">CDate</span></span>](#cdate) |[<span data-ttu-id="3d184-153">CGuid</span><span class="sxs-lookup"><span data-stu-id="3d184-153">CGuid</span></span>](#cguid) |[<span data-ttu-id="3d184-154">ConvertFromBase64</span><span class="sxs-lookup"><span data-stu-id="3d184-154">ConvertFromBase64</span></span>](#convertfrombase64) | |
| [<span data-ttu-id="3d184-155">ConvertToBase64</span><span class="sxs-lookup"><span data-stu-id="3d184-155">ConvertToBase64</span></span>](#converttobase64) |[<span data-ttu-id="3d184-156">ConvertFromUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="3d184-156">ConvertFromUTF8Hex</span></span>](#convertfromutf8hex) |[<span data-ttu-id="3d184-157">ConvertToUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="3d184-157">ConvertToUTF8Hex</span></span>](#converttoutf8hex) |[<span data-ttu-id="3d184-158">CNum</span><span class="sxs-lookup"><span data-stu-id="3d184-158">CNum</span></span>](#cnum) | |
| [<span data-ttu-id="3d184-159">CRef</span><span class="sxs-lookup"><span data-stu-id="3d184-159">CRef</span></span>](#cref) |[<span data-ttu-id="3d184-160">CStr</span><span class="sxs-lookup"><span data-stu-id="3d184-160">CStr</span></span>](#cstr) |[<span data-ttu-id="3d184-161">StringFromGuid</span><span class="sxs-lookup"><span data-stu-id="3d184-161">StringFromGuid</span></span>](#StringFromGuid) |[<span data-ttu-id="3d184-162">StringFromSid</span><span class="sxs-lookup"><span data-stu-id="3d184-162">StringFromSid</span></span>](#stringfromsid) | |
| <span data-ttu-id="3d184-163">**Tarih / saat**</span><span class="sxs-lookup"><span data-stu-id="3d184-163">**Date / Time**</span></span> | | | | |
| [<span data-ttu-id="3d184-164">DateAdd</span><span class="sxs-lookup"><span data-stu-id="3d184-164">DateAdd</span></span>](#dateadd) |[<span data-ttu-id="3d184-165">DateFromNum</span><span class="sxs-lookup"><span data-stu-id="3d184-165">DateFromNum</span></span>](#datefromnum) |[<span data-ttu-id="3d184-166">FormatDateTime</span><span class="sxs-lookup"><span data-stu-id="3d184-166">FormatDateTime</span></span>](#formatdatetime) |[<span data-ttu-id="3d184-167">Şimdi</span><span class="sxs-lookup"><span data-stu-id="3d184-167">Now</span></span>](#now) | |
| [<span data-ttu-id="3d184-168">NumFromDate</span><span class="sxs-lookup"><span data-stu-id="3d184-168">NumFromDate</span></span>](#numfromdate) | | | | |
| <span data-ttu-id="3d184-169">**Dizin**</span><span class="sxs-lookup"><span data-stu-id="3d184-169">**Directory**</span></span> | | | | |
| [<span data-ttu-id="3d184-170">DNComponent</span><span class="sxs-lookup"><span data-stu-id="3d184-170">DNComponent</span></span>](#dncomponent) |[<span data-ttu-id="3d184-171">DNComponentRev</span><span class="sxs-lookup"><span data-stu-id="3d184-171">DNComponentRev</span></span>](#dncomponentrev) |[<span data-ttu-id="3d184-172">EscapeDNComponent</span><span class="sxs-lookup"><span data-stu-id="3d184-172">EscapeDNComponent</span></span>](#escapedncomponent) | | |
| <span data-ttu-id="3d184-173">**Değerlendirme**</span><span class="sxs-lookup"><span data-stu-id="3d184-173">**Evaluation**</span></span> | | | | |
| [<span data-ttu-id="3d184-174">IsBitSet</span><span class="sxs-lookup"><span data-stu-id="3d184-174">IsBitSet</span></span>](#isbitset) |[<span data-ttu-id="3d184-175">IsDate</span><span class="sxs-lookup"><span data-stu-id="3d184-175">IsDate</span></span>](#isdate) |[<span data-ttu-id="3d184-176">IsEmpty</span><span class="sxs-lookup"><span data-stu-id="3d184-176">IsEmpty</span></span>](#isempty) |[<span data-ttu-id="3d184-177">IsGuid</span><span class="sxs-lookup"><span data-stu-id="3d184-177">IsGuid</span></span>](#isguid) | |
| [<span data-ttu-id="3d184-178">IsNull</span><span class="sxs-lookup"><span data-stu-id="3d184-178">IsNull</span></span>](#isnull) |[<span data-ttu-id="3d184-179">IsNullOrEmpty</span><span class="sxs-lookup"><span data-stu-id="3d184-179">IsNullOrEmpty</span></span>](#isnullorempty) |[<span data-ttu-id="3d184-180">IsNumeric</span><span class="sxs-lookup"><span data-stu-id="3d184-180">IsNumeric</span></span>](#isnumeric) |[<span data-ttu-id="3d184-181">Olmasına</span><span class="sxs-lookup"><span data-stu-id="3d184-181">IsPresent</span></span>](#ispresent) | |
| [<span data-ttu-id="3d184-182">IsString</span><span class="sxs-lookup"><span data-stu-id="3d184-182">IsString</span></span>](#isstring) | | | | |
| <span data-ttu-id="3d184-183">**Matematik**</span><span class="sxs-lookup"><span data-stu-id="3d184-183">**Math**</span></span> | | | | |
| [<span data-ttu-id="3d184-184">BitAnd</span><span class="sxs-lookup"><span data-stu-id="3d184-184">BitAnd</span></span>](#bitand) |[<span data-ttu-id="3d184-185">BitOr</span><span class="sxs-lookup"><span data-stu-id="3d184-185">BitOr</span></span>](#bitor) |[<span data-ttu-id="3d184-186">RandomNum</span><span class="sxs-lookup"><span data-stu-id="3d184-186">RandomNum</span></span>](#randomnum) | | |
| <span data-ttu-id="3d184-187">**Birden çok değerli**</span><span class="sxs-lookup"><span data-stu-id="3d184-187">**Multi-valued**</span></span> | | | | |
| [<span data-ttu-id="3d184-188">İçerir</span><span class="sxs-lookup"><span data-stu-id="3d184-188">Contains</span></span>](#contains) |[<span data-ttu-id="3d184-189">Sayısı</span><span class="sxs-lookup"><span data-stu-id="3d184-189">Count</span></span>](#count) |[<span data-ttu-id="3d184-190">Öğesi</span><span class="sxs-lookup"><span data-stu-id="3d184-190">Item</span></span>](#item) |[<span data-ttu-id="3d184-191">ItemOrNull</span><span class="sxs-lookup"><span data-stu-id="3d184-191">ItemOrNull</span></span>](#itemornull) | |
| [<span data-ttu-id="3d184-192">Birleştir</span><span class="sxs-lookup"><span data-stu-id="3d184-192">Join</span></span>](#join) |[<span data-ttu-id="3d184-193">RemoveDuplicates</span><span class="sxs-lookup"><span data-stu-id="3d184-193">RemoveDuplicates</span></span>](#removeduplicates) |[<span data-ttu-id="3d184-194">Böl</span><span class="sxs-lookup"><span data-stu-id="3d184-194">Split</span></span>](#split) | | |
| <span data-ttu-id="3d184-195">**Program akışı**</span><span class="sxs-lookup"><span data-stu-id="3d184-195">**Program Flow**</span></span> | | | | |
| [<span data-ttu-id="3d184-196">Hata</span><span class="sxs-lookup"><span data-stu-id="3d184-196">Error</span></span>](#error) |[<span data-ttu-id="3d184-197">IIF</span><span class="sxs-lookup"><span data-stu-id="3d184-197">IIF</span></span>](#iif) |[<span data-ttu-id="3d184-198">Seç</span><span class="sxs-lookup"><span data-stu-id="3d184-198">Select</span></span>](#select) |[<span data-ttu-id="3d184-199">Anahtar</span><span class="sxs-lookup"><span data-stu-id="3d184-199">Switch</span></span>](#switch) | |
| [<span data-ttu-id="3d184-200">Burada</span><span class="sxs-lookup"><span data-stu-id="3d184-200">Where</span></span>](#where) |[<span data-ttu-id="3d184-201">İle</span><span class="sxs-lookup"><span data-stu-id="3d184-201">With</span></span>](#with) | | | |
| <span data-ttu-id="3d184-202">**Metin**</span><span class="sxs-lookup"><span data-stu-id="3d184-202">**Text**</span></span> | | | | |
| [<span data-ttu-id="3d184-203">GUID</span><span class="sxs-lookup"><span data-stu-id="3d184-203">GUID</span></span>](#guid) |[<span data-ttu-id="3d184-204">InStr</span><span class="sxs-lookup"><span data-stu-id="3d184-204">InStr</span></span>](#instr) |[<span data-ttu-id="3d184-205">InStrRev</span><span class="sxs-lookup"><span data-stu-id="3d184-205">InStrRev</span></span>](#instrrev) |[<span data-ttu-id="3d184-206">LCase</span><span class="sxs-lookup"><span data-stu-id="3d184-206">LCase</span></span>](#lcase) | |
| [<span data-ttu-id="3d184-207">Sol</span><span class="sxs-lookup"><span data-stu-id="3d184-207">Left</span></span>](#left) |[<span data-ttu-id="3d184-208">Len</span><span class="sxs-lookup"><span data-stu-id="3d184-208">Len</span></span>](#len) |[<span data-ttu-id="3d184-209">LTrim</span><span class="sxs-lookup"><span data-stu-id="3d184-209">LTrim</span></span>](#ltrim) |[<span data-ttu-id="3d184-210">Orta</span><span class="sxs-lookup"><span data-stu-id="3d184-210">Mid</span></span>](#mid) | |
| [<span data-ttu-id="3d184-211">PadLeft</span><span class="sxs-lookup"><span data-stu-id="3d184-211">PadLeft</span></span>](#padleft) |[<span data-ttu-id="3d184-212">PadRight</span><span class="sxs-lookup"><span data-stu-id="3d184-212">PadRight</span></span>](#padright) |[<span data-ttu-id="3d184-213">PCase</span><span class="sxs-lookup"><span data-stu-id="3d184-213">PCase</span></span>](#pcase) |[<span data-ttu-id="3d184-214">Değiştir</span><span class="sxs-lookup"><span data-stu-id="3d184-214">Replace</span></span>](#replace) | |
| [<span data-ttu-id="3d184-215">ReplaceChars</span><span class="sxs-lookup"><span data-stu-id="3d184-215">ReplaceChars</span></span>](#replacechars) |[<span data-ttu-id="3d184-216">Sağ</span><span class="sxs-lookup"><span data-stu-id="3d184-216">Right</span></span>](#right) |[<span data-ttu-id="3d184-217">RTrim</span><span class="sxs-lookup"><span data-stu-id="3d184-217">RTrim</span></span>](#rtrim) |[<span data-ttu-id="3d184-218">Kırpma</span><span class="sxs-lookup"><span data-stu-id="3d184-218">Trim</span></span>](#trim) | |
| [<span data-ttu-id="3d184-219">UCase</span><span class="sxs-lookup"><span data-stu-id="3d184-219">UCase</span></span>](#ucase) |[<span data-ttu-id="3d184-220">Word</span><span class="sxs-lookup"><span data-stu-id="3d184-220">Word</span></span>](#word) | | | |

- - -
### <a name="bitand"></a><span data-ttu-id="3d184-221">BitAnd</span><span class="sxs-lookup"><span data-stu-id="3d184-221">BitAnd</span></span>
<span data-ttu-id="3d184-222">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-222">**Description:**</span></span>  
<span data-ttu-id="3d184-223">BitAnd işlevi belirtilen BITS üzerinde bir değer ayarlar.</span><span class="sxs-lookup"><span data-stu-id="3d184-223">The BitAnd function sets specified bits on a value.</span></span>

<span data-ttu-id="3d184-224">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-224">**Syntax:**</span></span>  
`num BitAnd(num value1, num value2)`

* <span data-ttu-id="3d184-225">value1, value2: and değerini birlikte olmalıdır sayısal değerler</span><span class="sxs-lookup"><span data-stu-id="3d184-225">value1, value2: numeric values that should be AND’ed together</span></span>

<span data-ttu-id="3d184-226">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="3d184-226">**Remarks:**</span></span>  
<span data-ttu-id="3d184-227">Bu işlev parametrelerinin her ikisini de ikili gösterimine dönüştürür ve biraz ayarlar:</span><span class="sxs-lookup"><span data-stu-id="3d184-227">This function converts both parameters to the binary representation and sets a bit to:</span></span>

* <span data-ttu-id="3d184-228">0 - biri veya her ikisini karşılık gelen bitleri *maskesi* ve *bayrağı* 0</span><span class="sxs-lookup"><span data-stu-id="3d184-228">0 - if one or both of the corresponding bits in *mask* and *flag* are 0</span></span>
* <span data-ttu-id="3d184-229">1 - karşılık gelen bit hem de 1 olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3d184-229">1 - if both of the corresponding bits are 1.</span></span>

<span data-ttu-id="3d184-230">Diğer bir deyişle, her iki parametre karşılık gelen bitleri 1 olduğu durumlar dışında tüm durumlarda 0 döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-230">In other words, it returns 0 in all cases except when the corresponding bits of both parameters are 1.</span></span>

<span data-ttu-id="3d184-231">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3d184-231">**Example:**</span></span>  
`BitAnd(&HF, &HF7)`  
<span data-ttu-id="3d184-232">Onaltılık "F" ve "F7" değerlendirmek için bu değer 7 döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-232">Returns 7 because hexadecimal "F" AND "F7" evaluate to this value.</span></span>

- - -
### <a name="bitor"></a><span data-ttu-id="3d184-233">BitOr</span><span class="sxs-lookup"><span data-stu-id="3d184-233">BitOr</span></span>
<span data-ttu-id="3d184-234">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-234">**Description:**</span></span>  
<span data-ttu-id="3d184-235">BitOr işlevi belirtilen BITS üzerinde bir değer ayarlar.</span><span class="sxs-lookup"><span data-stu-id="3d184-235">The BitOr function sets specified bits on a value.</span></span>

<span data-ttu-id="3d184-236">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-236">**Syntax:**</span></span>  
`num BitOr(num value1, num value2)`

* <span data-ttu-id="3d184-237">value1, value2: or birlikte olmalıdır sayısal değerler</span><span class="sxs-lookup"><span data-stu-id="3d184-237">value1, value2: numeric values that should be OR’ed together</span></span>

<span data-ttu-id="3d184-238">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="3d184-238">**Remarks:**</span></span>  
<span data-ttu-id="3d184-239">Bu işlev parametrelerinin her ikisini de ikili gösterimine dönüştürür ve karşılık gelen BITS her ikisi de 0 olduğunda birini veya her ikisini maskesi ve bayrağı karşılık gelen bitleri 1 ise 1 ve 0 biraz ayarlar.</span><span class="sxs-lookup"><span data-stu-id="3d184-239">This function converts both parameters to the binary representation and sets a bit to 1 if one or both of the corresponding bits in mask and flag are 1, and to 0 if both of the corresponding bits are 0.</span></span> <span data-ttu-id="3d184-240">Diğer bir deyişle, her iki parametre karşılık gelen bitleri 0 nerede dışındaki tüm durumlarda 1 döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-240">In other words, it returns 1 in all cases except where the corresponding bits of both parameters are 0.</span></span>

- - -
### <a name="cbool"></a><span data-ttu-id="3d184-241">CBool</span><span class="sxs-lookup"><span data-stu-id="3d184-241">CBool</span></span>
<span data-ttu-id="3d184-242">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-242">**Description:**</span></span>  
<span data-ttu-id="3d184-243">CBool işlevi değerlendirilen geçen ifadeye göre bir Boole değeri döndürür</span><span class="sxs-lookup"><span data-stu-id="3d184-243">The CBool function returns a Boolean based on the evaluated expression</span></span>

<span data-ttu-id="3d184-244">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-244">**Syntax:**</span></span>  
`bool CBool(exp Expression)`

<span data-ttu-id="3d184-245">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="3d184-245">**Remarks:**</span></span>  
<span data-ttu-id="3d184-246">CBool True değerini döndürür sonra ifadeyi sıfır olmayan bir değere hesaplar varsa, aksi takdirde, False değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-246">If the expression evaluates to a nonzero value, then CBool returns True, else it returns False.</span></span>

<span data-ttu-id="3d184-247">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3d184-247">**Example:**</span></span>  
`CBool([attrib1] = [attrib2])`  

<span data-ttu-id="3d184-248">Döndürür True her iki öznitelik aynı değere sahip.</span><span class="sxs-lookup"><span data-stu-id="3d184-248">Returns True if both attributes have the same value.</span></span>

- - -
### <a name="cdate"></a><span data-ttu-id="3d184-249">CDate</span><span class="sxs-lookup"><span data-stu-id="3d184-249">CDate</span></span>
<span data-ttu-id="3d184-250">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-250">**Description:**</span></span>  
<span data-ttu-id="3d184-251">CDate işlevi bir dizeden bir UTC DateTime değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-251">The CDate function returns a UTC DateTime from a string.</span></span> <span data-ttu-id="3d184-252">Tarih saat yerel öznitelik türü eşitlenmiş değil ancak bazı işlevler tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3d184-252">DateTime is not a native attribute type in Sync but is used by some functions.</span></span>

<span data-ttu-id="3d184-253">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-253">**Syntax:**</span></span>  
`dt CDate(str value)`

* <span data-ttu-id="3d184-254">Değer: Bir dizeyi bir tarih, saat ve isteğe bağlı olarak saat dilimi</span><span class="sxs-lookup"><span data-stu-id="3d184-254">Value: A string with a date, time, and optionally time zone</span></span>

<span data-ttu-id="3d184-255">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="3d184-255">**Remarks:**</span></span>  
<span data-ttu-id="3d184-256">Döndürülen dize her zaman UTC biçiminde değil.</span><span class="sxs-lookup"><span data-stu-id="3d184-256">The returned string is always in UTC.</span></span>

<span data-ttu-id="3d184-257">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3d184-257">**Example:**</span></span>  
`CDate([employeeStartTime])`  
<span data-ttu-id="3d184-258">Çalışanın üzerinde bir DateTime dayalı döndürür başlangıç zamanı</span><span class="sxs-lookup"><span data-stu-id="3d184-258">Returns a DateTime based on the employee’s start time</span></span>

`CDate("2013-01-10 4:00 PM -8")`  
<span data-ttu-id="3d184-259">Döndürür DateTime temsil eden bir "2013-01-11 12: 00'da"</span><span class="sxs-lookup"><span data-stu-id="3d184-259">Returns a DateTime representing "2013-01-11 12:00 AM"</span></span>








- - -
### <a name="certextensionoids"></a><span data-ttu-id="3d184-260">CertExtensionOids</span><span class="sxs-lookup"><span data-stu-id="3d184-260">CertExtensionOids</span></span>
<span data-ttu-id="3d184-261">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-261">**Description:**</span></span>  
<span data-ttu-id="3d184-262">Bir sertifika nesnesinin tüm kritik uzantılar OID değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-262">Returns the Oid values of all the critical extensions of a certificate object.</span></span>

<span data-ttu-id="3d184-263">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-263">**Syntax:**</span></span>  
`mvstr CertExtensionOids(binary certificateRawData)`  
*   <span data-ttu-id="3d184-264">certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi.</span><span class="sxs-lookup"><span data-stu-id="3d184-264">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="3d184-265">Bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.</span><span class="sxs-lookup"><span data-stu-id="3d184-265">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certformat"></a><span data-ttu-id="3d184-266">CertFormat</span><span class="sxs-lookup"><span data-stu-id="3d184-266">CertFormat</span></span>
<span data-ttu-id="3d184-267">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-267">**Description:**</span></span>  
<span data-ttu-id="3d184-268">Bu X.509v3 sertifikasını biçim adını döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-268">Returns the name of the format of this X.509v3 certificate.</span></span>

<span data-ttu-id="3d184-269">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-269">**Syntax:**</span></span>  
`str CertFormat(binary certificateRawData)`  
*   <span data-ttu-id="3d184-270">certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi.</span><span class="sxs-lookup"><span data-stu-id="3d184-270">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="3d184-271">Bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.</span><span class="sxs-lookup"><span data-stu-id="3d184-271">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certfriendlyname"></a><span data-ttu-id="3d184-272">CertFriendlyName</span><span class="sxs-lookup"><span data-stu-id="3d184-272">CertFriendlyName</span></span>
<span data-ttu-id="3d184-273">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-273">**Description:**</span></span>  
<span data-ttu-id="3d184-274">Bir sertifika için ilişkili diğer adı döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-274">Returns the associated alias for a certificate.</span></span>

<span data-ttu-id="3d184-275">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-275">**Syntax:**</span></span>  
`str CertFriendlyName(binary certificateRawData)`  
*   <span data-ttu-id="3d184-276">certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi.</span><span class="sxs-lookup"><span data-stu-id="3d184-276">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="3d184-277">Bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.</span><span class="sxs-lookup"><span data-stu-id="3d184-277">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certhashstring"></a><span data-ttu-id="3d184-278">CertHashString</span><span class="sxs-lookup"><span data-stu-id="3d184-278">CertHashString</span></span>
<span data-ttu-id="3d184-279">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-279">**Description:**</span></span>  
<span data-ttu-id="3d184-280">X.509v3 sertifikasını SHA1 karma değeri bir onaltılık dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-280">Returns the SHA1 hash value for the X.509v3 certificate as a hexadecimal string.</span></span>

<span data-ttu-id="3d184-281">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-281">**Syntax:**</span></span>  
`str CertHashString(binary certificateRawData)`  
*   <span data-ttu-id="3d184-282">certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi.</span><span class="sxs-lookup"><span data-stu-id="3d184-282">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="3d184-283">Bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.</span><span class="sxs-lookup"><span data-stu-id="3d184-283">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certissuer"></a><span data-ttu-id="3d184-284">CertIssuer</span><span class="sxs-lookup"><span data-stu-id="3d184-284">CertIssuer</span></span>
<span data-ttu-id="3d184-285">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-285">**Description:**</span></span>  
<span data-ttu-id="3d184-286">X.509v3 sertifikasını veren sertifika yetkilisinin adını döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-286">Returns the name of the certificate authority that issued the X.509v3 certificate.</span></span>

<span data-ttu-id="3d184-287">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-287">**Syntax:**</span></span>  
`str CertIssuer(binary certificateRawData)`  
*   <span data-ttu-id="3d184-288">certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi.</span><span class="sxs-lookup"><span data-stu-id="3d184-288">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="3d184-289">Bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.</span><span class="sxs-lookup"><span data-stu-id="3d184-289">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certissuerdn"></a><span data-ttu-id="3d184-290">CertIssuerDN</span><span class="sxs-lookup"><span data-stu-id="3d184-290">CertIssuerDN</span></span>
<span data-ttu-id="3d184-291">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-291">**Description:**</span></span>  
<span data-ttu-id="3d184-292">Sertifikayı verenin ayırt edici adını döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-292">Returns the distinguished name of the certificate issuer.</span></span>

<span data-ttu-id="3d184-293">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-293">**Syntax:**</span></span>  
`str CertIssuerDN(binary certificateRawData)`  
*   <span data-ttu-id="3d184-294">certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi.</span><span class="sxs-lookup"><span data-stu-id="3d184-294">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="3d184-295">Bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.</span><span class="sxs-lookup"><span data-stu-id="3d184-295">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certissueroid"></a><span data-ttu-id="3d184-296">CertIssuerOid</span><span class="sxs-lookup"><span data-stu-id="3d184-296">CertIssuerOid</span></span>
<span data-ttu-id="3d184-297">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-297">**Description:**</span></span>  
<span data-ttu-id="3d184-298">Sertifikayı verenin OID döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-298">Returns the Oid of the certificate issuer.</span></span>

<span data-ttu-id="3d184-299">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-299">**Syntax:**</span></span>  
`str CertIssuerOid(binary certificateRawData)`  
*   <span data-ttu-id="3d184-300">certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi.</span><span class="sxs-lookup"><span data-stu-id="3d184-300">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="3d184-301">Bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.</span><span class="sxs-lookup"><span data-stu-id="3d184-301">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certkeyalgorithm"></a><span data-ttu-id="3d184-302">CertKeyAlgorithm</span><span class="sxs-lookup"><span data-stu-id="3d184-302">CertKeyAlgorithm</span></span>
<span data-ttu-id="3d184-303">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-303">**Description:**</span></span>  
<span data-ttu-id="3d184-304">Bu X.509v3 sertifika için anahtar algoritması bilgi dize olarak döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-304">Returns the key algorithm information for this X.509v3 certificate as a string.</span></span>

<span data-ttu-id="3d184-305">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-305">**Syntax:**</span></span>  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   <span data-ttu-id="3d184-306">certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi.</span><span class="sxs-lookup"><span data-stu-id="3d184-306">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="3d184-307">Bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.</span><span class="sxs-lookup"><span data-stu-id="3d184-307">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certkeyalgorithmparams"></a><span data-ttu-id="3d184-308">CertKeyAlgorithmParams</span><span class="sxs-lookup"><span data-stu-id="3d184-308">CertKeyAlgorithmParams</span></span>
<span data-ttu-id="3d184-309">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-309">**Description:**</span></span>  
<span data-ttu-id="3d184-310">X.509v3 sertifika için anahtar algoritması parametreleri onaltılık dize olarak döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-310">Returns the key algorithm parameters for the X.509v3 certificate as a hexadecimal string.</span></span>

<span data-ttu-id="3d184-311">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-311">**Syntax:**</span></span>  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   <span data-ttu-id="3d184-312">certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi.</span><span class="sxs-lookup"><span data-stu-id="3d184-312">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="3d184-313">Bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.</span><span class="sxs-lookup"><span data-stu-id="3d184-313">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certnameinfo"></a><span data-ttu-id="3d184-314">CertNameInfo</span><span class="sxs-lookup"><span data-stu-id="3d184-314">CertNameInfo</span></span>
<span data-ttu-id="3d184-315">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-315">**Description:**</span></span>  
<span data-ttu-id="3d184-316">Konu ve sertifikayı veren adları bir sertifika verir.</span><span class="sxs-lookup"><span data-stu-id="3d184-316">Returns the subject and issuer names from a certificate.</span></span>

<span data-ttu-id="3d184-317">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-317">**Syntax:**</span></span>  
`str CertNameInfo(binary certificateRawData, str x509NameType, bool includesIssuerName)`  
*   <span data-ttu-id="3d184-318">certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi.</span><span class="sxs-lookup"><span data-stu-id="3d184-318">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="3d184-319">Bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.</span><span class="sxs-lookup"><span data-stu-id="3d184-319">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>
*   <span data-ttu-id="3d184-320">X509NameType: Konu X509NameType değeri.</span><span class="sxs-lookup"><span data-stu-id="3d184-320">X509NameType: The X509NameType value for the subject.</span></span>
*   <span data-ttu-id="3d184-321">includesIssuerName: verenin adı; dahil etmek için true Aksi takdirde false.</span><span class="sxs-lookup"><span data-stu-id="3d184-321">includesIssuerName: true to include the issuer name; otherwise, false.</span></span>

- - -
### <a name="certnotafter"></a><span data-ttu-id="3d184-322">CertNotAfter</span><span class="sxs-lookup"><span data-stu-id="3d184-322">CertNotAfter</span></span>
<span data-ttu-id="3d184-323">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-323">**Description:**</span></span>  
<span data-ttu-id="3d184-324">Yerel saatle sonra bir sertifika artık geçerli olduğu tarihi döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-324">Returns the date in local time after which a certificate is no longer valid.</span></span>

<span data-ttu-id="3d184-325">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-325">**Syntax:**</span></span>  
`dt CertNotAfter(binary certificateRawData)`  
*   <span data-ttu-id="3d184-326">certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi.</span><span class="sxs-lookup"><span data-stu-id="3d184-326">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="3d184-327">Bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.</span><span class="sxs-lookup"><span data-stu-id="3d184-327">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certnotbefore"></a><span data-ttu-id="3d184-328">CertNotBefore</span><span class="sxs-lookup"><span data-stu-id="3d184-328">CertNotBefore</span></span>
<span data-ttu-id="3d184-329">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-329">**Description:**</span></span>  
<span data-ttu-id="3d184-330">Yerel saatte bir sertifikanın geçerli hale geldiği tarihi döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-330">Returns the date in local time on which a certificate becomes valid.</span></span>

<span data-ttu-id="3d184-331">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-331">**Syntax:**</span></span>  
`dt CertNotBefore(binary certificateRawData)`  
*   <span data-ttu-id="3d184-332">certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi.</span><span class="sxs-lookup"><span data-stu-id="3d184-332">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="3d184-333">Bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.</span><span class="sxs-lookup"><span data-stu-id="3d184-333">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certpublickeyoid"></a><span data-ttu-id="3d184-334">CertPublicKeyOid</span><span class="sxs-lookup"><span data-stu-id="3d184-334">CertPublicKeyOid</span></span>
<span data-ttu-id="3d184-335">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-335">**Description:**</span></span>  
<span data-ttu-id="3d184-336">X.509v3 sertifikası için ortak anahtar OID döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-336">Returns the Oid of the public key for the X.509v3 certificate.</span></span>

<span data-ttu-id="3d184-337">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-337">**Syntax:**</span></span>  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   <span data-ttu-id="3d184-338">certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi.</span><span class="sxs-lookup"><span data-stu-id="3d184-338">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="3d184-339">Bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.</span><span class="sxs-lookup"><span data-stu-id="3d184-339">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certpublickeyparametersoid"></a><span data-ttu-id="3d184-340">CertPublicKeyParametersOid</span><span class="sxs-lookup"><span data-stu-id="3d184-340">CertPublicKeyParametersOid</span></span>
<span data-ttu-id="3d184-341">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-341">**Description:**</span></span>  
<span data-ttu-id="3d184-342">OID X.509v3 sertifikasını için bir ortak anahtar parametrelerinin döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-342">Returns the Oid of the public key parameters for the X.509v3 certificate.</span></span>

<span data-ttu-id="3d184-343">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-343">**Syntax:**</span></span>  
`str CertPublicKeyParametersOid(binary certificateRawData)`  
*   <span data-ttu-id="3d184-344">certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi.</span><span class="sxs-lookup"><span data-stu-id="3d184-344">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="3d184-345">Bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.</span><span class="sxs-lookup"><span data-stu-id="3d184-345">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certserialnumber"></a><span data-ttu-id="3d184-346">CertSerialNumber</span><span class="sxs-lookup"><span data-stu-id="3d184-346">CertSerialNumber</span></span>
<span data-ttu-id="3d184-347">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-347">**Description:**</span></span>  
<span data-ttu-id="3d184-348">X.509v3 sertifika seri numarasını döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-348">Returns the serial number of the X.509v3 certificate.</span></span>

<span data-ttu-id="3d184-349">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-349">**Syntax:**</span></span>  
`str CertSerialNumber(binary certificateRawData)`  
*   <span data-ttu-id="3d184-350">certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi.</span><span class="sxs-lookup"><span data-stu-id="3d184-350">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="3d184-351">Bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.</span><span class="sxs-lookup"><span data-stu-id="3d184-351">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsignaturealgorithmoid"></a><span data-ttu-id="3d184-352">CertSignatureAlgorithmOid</span><span class="sxs-lookup"><span data-stu-id="3d184-352">CertSignatureAlgorithmOid</span></span>
<span data-ttu-id="3d184-353">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-353">**Description:**</span></span>  
<span data-ttu-id="3d184-354">Bir sertifikanın imzasını oluşturmak için kullanılan algoritma OID döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-354">Returns the Oid of the algorithm used to create the signature of a certificate.</span></span>

<span data-ttu-id="3d184-355">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-355">**Syntax:**</span></span>  
`str CertSignatureAlgorithmOid(binary certificateRawData)`  
*   <span data-ttu-id="3d184-356">certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi.</span><span class="sxs-lookup"><span data-stu-id="3d184-356">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="3d184-357">Bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.</span><span class="sxs-lookup"><span data-stu-id="3d184-357">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsubject"></a><span data-ttu-id="3d184-358">CertSubject</span><span class="sxs-lookup"><span data-stu-id="3d184-358">CertSubject</span></span>
<span data-ttu-id="3d184-359">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-359">**Description:**</span></span>  
<span data-ttu-id="3d184-360">Bir sertifikadan konu ayırt edici adını alır.</span><span class="sxs-lookup"><span data-stu-id="3d184-360">Gets the subject distinguished name from a certificate.</span></span>

<span data-ttu-id="3d184-361">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-361">**Syntax:**</span></span>  
`str CertSubject(binary certificateRawData)`  
*   <span data-ttu-id="3d184-362">certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi.</span><span class="sxs-lookup"><span data-stu-id="3d184-362">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="3d184-363">Bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.</span><span class="sxs-lookup"><span data-stu-id="3d184-363">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsubjectnamedn"></a><span data-ttu-id="3d184-364">CertSubjectNameDN</span><span class="sxs-lookup"><span data-stu-id="3d184-364">CertSubjectNameDN</span></span>
<span data-ttu-id="3d184-365">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-365">**Description:**</span></span>  
<span data-ttu-id="3d184-366">Bir sertifikadan konu ayırt edici adını döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-366">Returns the subject distinguished name from a certificate.</span></span>

<span data-ttu-id="3d184-367">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-367">**Syntax:**</span></span>  
`str CertSubjectNameDN(binary certificateRawData)`  
*   <span data-ttu-id="3d184-368">certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi.</span><span class="sxs-lookup"><span data-stu-id="3d184-368">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="3d184-369">Bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.</span><span class="sxs-lookup"><span data-stu-id="3d184-369">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsubjectnameoid"></a><span data-ttu-id="3d184-370">CertSubjectNameOid</span><span class="sxs-lookup"><span data-stu-id="3d184-370">CertSubjectNameOid</span></span>
<span data-ttu-id="3d184-371">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-371">**Description:**</span></span>  
<span data-ttu-id="3d184-372">Bir sertifikadan konu adı OID döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-372">Returns the Oid of the subject name from a certificate.</span></span>

<span data-ttu-id="3d184-373">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-373">**Syntax:**</span></span>  
`str CertSubjectNameOid(binary certificateRawData)`  
*   <span data-ttu-id="3d184-374">certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi.</span><span class="sxs-lookup"><span data-stu-id="3d184-374">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="3d184-375">Bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.</span><span class="sxs-lookup"><span data-stu-id="3d184-375">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certthumbprint"></a><span data-ttu-id="3d184-376">Certthumbprınt</span><span class="sxs-lookup"><span data-stu-id="3d184-376">CertThumbprint</span></span>
<span data-ttu-id="3d184-377">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-377">**Description:**</span></span>  
<span data-ttu-id="3d184-378">Bir sertifikanın parmak izini döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-378">Returns the thumbprint of a certificate.</span></span>

<span data-ttu-id="3d184-379">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-379">**Syntax:**</span></span>  
`str CertThumbprint(binary certificateRawData)`  
*   <span data-ttu-id="3d184-380">certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi.</span><span class="sxs-lookup"><span data-stu-id="3d184-380">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="3d184-381">Bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.</span><span class="sxs-lookup"><span data-stu-id="3d184-381">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certversion"></a><span data-ttu-id="3d184-382">CertVersion</span><span class="sxs-lookup"><span data-stu-id="3d184-382">CertVersion</span></span>
<span data-ttu-id="3d184-383">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-383">**Description:**</span></span>  
<span data-ttu-id="3d184-384">Bir sertifikanın X.509 biçimindeki sürümü döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-384">Returns the X.509 format version of a certificate.</span></span>

<span data-ttu-id="3d184-385">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-385">**Syntax:**</span></span>  
`str CertThumbprint(binary certificateRawData)`  
*   <span data-ttu-id="3d184-386">certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi.</span><span class="sxs-lookup"><span data-stu-id="3d184-386">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="3d184-387">Bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.</span><span class="sxs-lookup"><span data-stu-id="3d184-387">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="cguid"></a><span data-ttu-id="3d184-388">CGuid</span><span class="sxs-lookup"><span data-stu-id="3d184-388">CGuid</span></span>
<span data-ttu-id="3d184-389">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-389">**Description:**</span></span>  
<span data-ttu-id="3d184-390">CGuid işlevi bir GUID dize gösterimini ikili gösterimine dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-390">The CGuid function converts the string representation of a GUID to its binary representation.</span></span>

<span data-ttu-id="3d184-391">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-391">**Syntax:**</span></span>  
`bin CGuid(str GUID)`

* <span data-ttu-id="3d184-392">Bu desen biçimlendirilmiş bir dize: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx veya {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span><span class="sxs-lookup"><span data-stu-id="3d184-392">A String formatted in this pattern: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx or {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span></span>

- - -
### <a name="contains"></a><span data-ttu-id="3d184-393">Contains</span><span class="sxs-lookup"><span data-stu-id="3d184-393">Contains</span></span>
<span data-ttu-id="3d184-394">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-394">**Description:**</span></span>  
<span data-ttu-id="3d184-395">Birden çok değerli bir öznitelik içinde bir dize içerir işlev bulur</span><span class="sxs-lookup"><span data-stu-id="3d184-395">The Contains function finds a string inside a multi-valued attribute</span></span>

<span data-ttu-id="3d184-396">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-396">**Syntax:**</span></span>  
<span data-ttu-id="3d184-397">`num Contains (mvstring attribute, str search)`-büyük küçük harfe duyarlı</span><span class="sxs-lookup"><span data-stu-id="3d184-397">`num Contains (mvstring attribute, str search)` - case-sensitive</span></span>  
`num Contains (mvstring attribute, str search, enum Casetype)`  
<span data-ttu-id="3d184-398">`num Contains (mvref attribute, str search)`-büyük küçük harfe duyarlı</span><span class="sxs-lookup"><span data-stu-id="3d184-398">`num Contains (mvref attribute, str search)` - case-sensitive</span></span>

* <span data-ttu-id="3d184-399">Öznitelik: aramak için birden çok değerli özniteliği.</span><span class="sxs-lookup"><span data-stu-id="3d184-399">attribute: the multi-valued attribute to search.</span></span>
* <span data-ttu-id="3d184-400">Arama: öznitelikte bulmak için dizesi.</span><span class="sxs-lookup"><span data-stu-id="3d184-400">search: string to find in the attribute.</span></span>
* <span data-ttu-id="3d184-401">Casetype: CaseInsensitive veya CaseSensitive.</span><span class="sxs-lookup"><span data-stu-id="3d184-401">Casetype: CaseInsensitive or CaseSensitive.</span></span>

<span data-ttu-id="3d184-402">Dizin, dize bulunduğu birden çok değerli özniteliğinde döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-402">Returns index in the multi-valued attribute where the string was found.</span></span> <span data-ttu-id="3d184-403">Dize bulunamazsa, 0 döndürülür.</span><span class="sxs-lookup"><span data-stu-id="3d184-403">0 is returned if the string is not found.</span></span>

<span data-ttu-id="3d184-404">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="3d184-404">**Remarks:**</span></span>  
<span data-ttu-id="3d184-405">Birden çok değerli dize öznitelikleri için arama alt dizeler değerleri bulur.</span><span class="sxs-lookup"><span data-stu-id="3d184-405">For multi-valued string attributes, the search finds substrings in the values.</span></span>  
<span data-ttu-id="3d184-406">Başvuru özniteliği için Aranan dize değeri bir eşleşme olarak kabul edilmesi için tam olarak eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="3d184-406">For reference attributes, the searched string must exactly match the value to be considered a match.</span></span>

<span data-ttu-id="3d184-407">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3d184-407">**Example:**</span></span>  
`IIF(Contains([proxyAddresses],"SMTP:")>0,[proxyAddresses],Error("No primary SMTP address found."))`  
<span data-ttu-id="3d184-408">Bir birincil e-posta adresi proxyAddresses özniteliğine sahipse, (büyük harf tarafından gösterilen "SMTP:"), proxyAddress özniteliği döndürür, aksi takdirde bir hata döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-408">If the proxyAddresses attribute has a primary email address (indicated by uppercase "SMTP:"), then return the proxyAddress attribute, else return an error.</span></span>

- - -
### <a name="convertfrombase64"></a><span data-ttu-id="3d184-409">ConvertFromBase64</span><span class="sxs-lookup"><span data-stu-id="3d184-409">ConvertFromBase64</span></span>
<span data-ttu-id="3d184-410">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-410">**Description:**</span></span>  
<span data-ttu-id="3d184-411">ConvertFromBase64 işlevi belirtilen base64 kodlu değer normal bir dizeye dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-411">The ConvertFromBase64 function converts the specified base64 encoded value to a regular string.</span></span>

<span data-ttu-id="3d184-412">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-412">**Syntax:**</span></span>  
<span data-ttu-id="3d184-413">`str ConvertFromBase64(str source)`-Unicode kodlama için varsayar.</span><span class="sxs-lookup"><span data-stu-id="3d184-413">`str ConvertFromBase64(str source)` - assumes Unicode for encoding</span></span>  
`str ConvertFromBase64(str source, enum Encoding)`

* <span data-ttu-id="3d184-414">Kaynak: Base64 ile kodlanmış dize</span><span class="sxs-lookup"><span data-stu-id="3d184-414">source: Base64 encoded string</span></span>  
* <span data-ttu-id="3d184-415">Kodlaması: Unicode, ASCII, UTF8</span><span class="sxs-lookup"><span data-stu-id="3d184-415">Encoding: Unicode, ASCII, UTF8</span></span>

<span data-ttu-id="3d184-416">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="3d184-416">**Example**</span></span>  
`ConvertFromBase64("SABlAGwAbABvACAAdwBvAHIAbABkACEA")`  
`ConvertFromBase64("SGVsbG8gd29ybGQh", UTF8)`

<span data-ttu-id="3d184-417">Örneklerin her ikisi de döndürmek "*Merhaba Dünya!*"</span><span class="sxs-lookup"><span data-stu-id="3d184-417">Both examples return "*Hello world!*"</span></span>

- - -
### <a name="convertfromutf8hex"></a><span data-ttu-id="3d184-418">ConvertFromUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="3d184-418">ConvertFromUTF8Hex</span></span>
<span data-ttu-id="3d184-419">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-419">**Description:**</span></span>  
<span data-ttu-id="3d184-420">ConvertFromUTF8Hex işlevi belirtilen UTF8 olarak kodlanmış onaltılık değeri dizeye dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-420">The ConvertFromUTF8Hex function converts the specified UTF8 Hex encoded value to a string.</span></span>

<span data-ttu-id="3d184-421">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-421">**Syntax:**</span></span>  
`str ConvertFromUTF8Hex(str source)`

* <span data-ttu-id="3d184-422">Kaynak: UTF8 2-bayt kodlanmış dizesi</span><span class="sxs-lookup"><span data-stu-id="3d184-422">source: UTF8 2-byte encoded sting</span></span>

<span data-ttu-id="3d184-423">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="3d184-423">**Remarks:**</span></span>  
<span data-ttu-id="3d184-424">Bu işlevin sonucu DN özniteliği için kolay olduğunu ConvertFromBase64([],UTF8) içinde arasındaki fark.</span><span class="sxs-lookup"><span data-stu-id="3d184-424">The difference between this function and ConvertFromBase64([],UTF8) in that the result is friendly for the DN attribute.</span></span>  
<span data-ttu-id="3d184-425">Bu biçim DN Azure Active Directory tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3d184-425">This format is used by Azure Active Directory as DN.</span></span>

<span data-ttu-id="3d184-426">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3d184-426">**Example:**</span></span>  
`ConvertFromUTF8Hex("48656C6C6F20776F726C6421")`  
<span data-ttu-id="3d184-427">Döndürür "*Merhaba Dünya!*"</span><span class="sxs-lookup"><span data-stu-id="3d184-427">Returns "*Hello world!*"</span></span>

- - -
### <a name="converttobase64"></a><span data-ttu-id="3d184-428">ConvertToBase64</span><span class="sxs-lookup"><span data-stu-id="3d184-428">ConvertToBase64</span></span>
<span data-ttu-id="3d184-429">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-429">**Description:**</span></span>  
<span data-ttu-id="3d184-430">ConvertToBase64 işlev bir dize Unicode base64 dizeye dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-430">The ConvertToBase64 function converts a string to a Unicode base64 string.</span></span>  
<span data-ttu-id="3d184-431">Base-64 basamak ile kodlanmış kendi eşdeğer dize gösterimi dizisi değerine dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-431">Converts the value of an array of integers to its equivalent string representation that is encoded with base-64 digits.</span></span>

<span data-ttu-id="3d184-432">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-432">**Syntax:**</span></span>  
`str ConvertToBase64(str source)`

<span data-ttu-id="3d184-433">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3d184-433">**Example:**</span></span>  
`ConvertToBase64("Hello world!")`  
<span data-ttu-id="3d184-434">"SABlAGwAbABvACAAdwBvAHIAbABkACEA" döndürür</span><span class="sxs-lookup"><span data-stu-id="3d184-434">Returns "SABlAGwAbABvACAAdwBvAHIAbABkACEA"</span></span>

- - -
### <a name="converttoutf8hex"></a><span data-ttu-id="3d184-435">ConvertToUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="3d184-435">ConvertToUTF8Hex</span></span>
<span data-ttu-id="3d184-436">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-436">**Description:**</span></span>  
<span data-ttu-id="3d184-437">ConvertToUTF8Hex işlev bir dize UTF8 olarak kodlanmış onaltılık değerine dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-437">The ConvertToUTF8Hex function converts a string to a UTF8 Hex encoded value.</span></span>

<span data-ttu-id="3d184-438">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-438">**Syntax:**</span></span>  
`str ConvertToUTF8Hex(str source)`

<span data-ttu-id="3d184-439">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="3d184-439">**Remarks:**</span></span>  
<span data-ttu-id="3d184-440">Bu işlev çıktı biçimi DN özniteliği biçimi olarak Azure Active Directory tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3d184-440">The output format of this function is used by Azure Active Directory as DN attribute format.</span></span>

<span data-ttu-id="3d184-441">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3d184-441">**Example:**</span></span>  
`ConvertToUTF8Hex("Hello world!")`  
<span data-ttu-id="3d184-442">Döndürür 48656C6C6F20776F726C6421</span><span class="sxs-lookup"><span data-stu-id="3d184-442">Returns 48656C6C6F20776F726C6421</span></span>

- - -
### <a name="count"></a><span data-ttu-id="3d184-443">Sayı</span><span class="sxs-lookup"><span data-stu-id="3d184-443">Count</span></span>
<span data-ttu-id="3d184-444">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-444">**Description:**</span></span>  
<span data-ttu-id="3d184-445">Count işlevi, birden çok değerli bir öznitelikte öğe sayısını döndürür</span><span class="sxs-lookup"><span data-stu-id="3d184-445">The Count function returns the number of elements in a multi-valued attribute</span></span>

<span data-ttu-id="3d184-446">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-446">**Syntax:**</span></span>  
`num Count(mvstr attribute)`

- - -
### <a name="cnum"></a><span data-ttu-id="3d184-447">CNum</span><span class="sxs-lookup"><span data-stu-id="3d184-447">CNum</span></span>
<span data-ttu-id="3d184-448">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-448">**Description:**</span></span>  
<span data-ttu-id="3d184-449">CNum işlev bir dize alır ve sayısal veri türü döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-449">The CNum function takes a string and returns a numeric data type.</span></span>

<span data-ttu-id="3d184-450">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-450">**Syntax:**</span></span>  
`num CNum(str value)`

- - -
### <a name="cref"></a><span data-ttu-id="3d184-451">CRef</span><span class="sxs-lookup"><span data-stu-id="3d184-451">CRef</span></span>
<span data-ttu-id="3d184-452">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-452">**Description:**</span></span>  
<span data-ttu-id="3d184-453">Bir dizeyi bir başvuru özniteliği dönüştürür</span><span class="sxs-lookup"><span data-stu-id="3d184-453">Converts a string to a reference attribute</span></span>

<span data-ttu-id="3d184-454">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-454">**Syntax:**</span></span>  
`ref CRef(str value)`

<span data-ttu-id="3d184-455">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3d184-455">**Example:**</span></span>  
`CRef("CN=LC Services,CN=Microsoft,CN=lcspool01,CN=Pools,CN=RTC Service," & %Forest.LDAP%)`

- - -
### <a name="cstr"></a><span data-ttu-id="3d184-456">CStr</span><span class="sxs-lookup"><span data-stu-id="3d184-456">CStr</span></span>
<span data-ttu-id="3d184-457">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-457">**Description:**</span></span>  
<span data-ttu-id="3d184-458">CStr işlevinin bir dize veri türüne dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-458">The CStr function converts to a string data type.</span></span>

<span data-ttu-id="3d184-459">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-459">**Syntax:**</span></span>  
`str CStr(num value)`  
`str CStr(ref value)`  
`str CStr(bool value)`  

* <span data-ttu-id="3d184-460">değer: bir sayısal değer, başvuru özniteliği ya da Boole değeri olabilir.</span><span class="sxs-lookup"><span data-stu-id="3d184-460">value: Can be a numeric value, reference attribute, or Boolean.</span></span>

<span data-ttu-id="3d184-461">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3d184-461">**Example:**</span></span>  
`CStr([dn])`  
<span data-ttu-id="3d184-462">Döndürebilirsiniz "cn = Can, dc = contoso, dc = com"</span><span class="sxs-lookup"><span data-stu-id="3d184-462">Could return "cn=Joe,dc=contoso,dc=com"</span></span>

- - -
### <a name="dateadd"></a><span data-ttu-id="3d184-463">DateAdd</span><span class="sxs-lookup"><span data-stu-id="3d184-463">DateAdd</span></span>
<span data-ttu-id="3d184-464">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-464">**Description:**</span></span>  
<span data-ttu-id="3d184-465">Belirli bir zaman aralığı eklenmiş olan bir tarih içeren bir tarih döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-465">Returns a Date containing a date to which a specified time interval has been added.</span></span>

<span data-ttu-id="3d184-466">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-466">**Syntax:**</span></span>  
`dt DateAdd(str interval, num value, dt date)`

* <span data-ttu-id="3d184-467">aralığı: dize eklemek istediğiniz zaman aralığı olan ifade.</span><span class="sxs-lookup"><span data-stu-id="3d184-467">interval: String expression that is the interval of time you want to add.</span></span> <span data-ttu-id="3d184-468">Dizenin şu değerlerden biri olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="3d184-468">The string must have one of the following values:</span></span>
  * <span data-ttu-id="3d184-469">yyyy yıl</span><span class="sxs-lookup"><span data-stu-id="3d184-469">yyyy Year</span></span>
  * <span data-ttu-id="3d184-470">q üç aylık dönem</span><span class="sxs-lookup"><span data-stu-id="3d184-470">q Quarter</span></span>
  * <span data-ttu-id="3d184-471">m ay</span><span class="sxs-lookup"><span data-stu-id="3d184-471">m Month</span></span>
  * <span data-ttu-id="3d184-472">yılın y günü</span><span class="sxs-lookup"><span data-stu-id="3d184-472">y Day of year</span></span>
  * <span data-ttu-id="3d184-473">d gün</span><span class="sxs-lookup"><span data-stu-id="3d184-473">d Day</span></span>
  * <span data-ttu-id="3d184-474">w haftanın günü</span><span class="sxs-lookup"><span data-stu-id="3d184-474">w Weekday</span></span>
  * <span data-ttu-id="3d184-475">ww hafta</span><span class="sxs-lookup"><span data-stu-id="3d184-475">ww Week</span></span>
  * <span data-ttu-id="3d184-476">h Saat</span><span class="sxs-lookup"><span data-stu-id="3d184-476">h Hour</span></span>
  * <span data-ttu-id="3d184-477">n dakika</span><span class="sxs-lookup"><span data-stu-id="3d184-477">n Minute</span></span>
  * <span data-ttu-id="3d184-478">s ikinci</span><span class="sxs-lookup"><span data-stu-id="3d184-478">s Second</span></span>
* <span data-ttu-id="3d184-479">değer: eklemek istediğiniz birim sayısı.</span><span class="sxs-lookup"><span data-stu-id="3d184-479">value: The number of units you want to add.</span></span> <span data-ttu-id="3d184-480">(Gelecekteki tarihleri almak için) olumlu veya olumsuz (geçmişteki tarihler almak için) olabilir.</span><span class="sxs-lookup"><span data-stu-id="3d184-480">It can be positive (to get dates in the future) or negative (to get dates in the past).</span></span>
* <span data-ttu-id="3d184-481">Tarih: aralık eklenir tarihini temsil eden DateTime.</span><span class="sxs-lookup"><span data-stu-id="3d184-481">date: DateTime representing date to which the interval is added.</span></span>

<span data-ttu-id="3d184-482">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3d184-482">**Example:**</span></span>  
`DateAdd("m", 3, CDate("2001-01-01"))`  
<span data-ttu-id="3d184-483">3 ay ekler ve "2001-04-01" temsil eden bir DateTime döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-483">Adds 3 months and returns a DateTime representing "2001-04-01".</span></span>

- - -
### <a name="datefromnum"></a><span data-ttu-id="3d184-484">DateFromNum</span><span class="sxs-lookup"><span data-stu-id="3d184-484">DateFromNum</span></span>
<span data-ttu-id="3d184-485">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-485">**Description:**</span></span>  
<span data-ttu-id="3d184-486">Bir değer Reklamın tarih biçimlendirme bir DateTime türü DateFromNum işlevi dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-486">The DateFromNum function converts a value in AD’s date format to a DateTime type.</span></span>

<span data-ttu-id="3d184-487">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-487">**Syntax:**</span></span>  
`dt DateFromNum(num value)`

<span data-ttu-id="3d184-488">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3d184-488">**Example:**</span></span>  
`DateFromNum([lastLogonTimestamp])`  
`DateFromNum(129699324000000000)`  
<span data-ttu-id="3d184-489">2012-01-01 temsil eden bir DateTime döndürür 23:00:00</span><span class="sxs-lookup"><span data-stu-id="3d184-489">Returns a DateTime representing 2012-01-01 23:00:00</span></span>

- - -
### <a name="dncomponent"></a><span data-ttu-id="3d184-490">DNComponent</span><span class="sxs-lookup"><span data-stu-id="3d184-490">DNComponent</span></span>
<span data-ttu-id="3d184-491">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-491">**Description:**</span></span>  
<span data-ttu-id="3d184-492">DNComponent işlevi soldan giderek belirtilen bir DN bileşen değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-492">The DNComponent function returns the value of a specified DN component going from left.</span></span>

<span data-ttu-id="3d184-493">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-493">**Syntax:**</span></span>  
`str DNComponent(ref dn, num ComponentNumber)`

* <span data-ttu-id="3d184-494">DN: yorumlamak için başvuru özniteliği</span><span class="sxs-lookup"><span data-stu-id="3d184-494">dn: the reference attribute to interpret</span></span>
* <span data-ttu-id="3d184-495">ComponentNumber: Döndürülecek DN bileşeninde</span><span class="sxs-lookup"><span data-stu-id="3d184-495">ComponentNumber: The component in the DN to return</span></span>

<span data-ttu-id="3d184-496">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3d184-496">**Example:**</span></span>  
`DNComponent([dn],1)`  
<span data-ttu-id="3d184-497">DN ise "CN = Joe, ou = =..." Can döndürür</span><span class="sxs-lookup"><span data-stu-id="3d184-497">If dn is "cn=Joe,ou=…," it returns Joe</span></span>

- - -
### <a name="dncomponentrev"></a><span data-ttu-id="3d184-498">DNComponentRev</span><span class="sxs-lookup"><span data-stu-id="3d184-498">DNComponentRev</span></span>
<span data-ttu-id="3d184-499">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-499">**Description:**</span></span>  
<span data-ttu-id="3d184-500">DNComponentRev işlevi (Bitiş) sağdan giderek belirtilen bir DN bileşen değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-500">The DNComponentRev function returns the value of a specified DN component going from right (the end).</span></span>

<span data-ttu-id="3d184-501">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-501">**Syntax:**</span></span>  
`str DNComponentRev(ref dn, num ComponentNumber)`  
`str DNComponentRev(ref dn, num ComponentNumber, enum Options)`

* <span data-ttu-id="3d184-502">DN: yorumlamak için başvuru özniteliği</span><span class="sxs-lookup"><span data-stu-id="3d184-502">dn: the reference attribute to interpret</span></span>
* <span data-ttu-id="3d184-503">ComponentNumber - döndürülecek DN bileşeni</span><span class="sxs-lookup"><span data-stu-id="3d184-503">ComponentNumber - The component in the DN to return</span></span>
* <span data-ttu-id="3d184-504">Seçenekler: DC – tüm bileşenleri Yoksay "dc ="</span><span class="sxs-lookup"><span data-stu-id="3d184-504">Options: DC – Ignore all components with "dc="</span></span>

<span data-ttu-id="3d184-505">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3d184-505">**Example:**</span></span>  
<span data-ttu-id="3d184-506">DN ise "CN = Joe, ou = Atlanta, ou = GA, ou = = US, dc = contoso, dc = com" sonra</span><span class="sxs-lookup"><span data-stu-id="3d184-506">If dn is "cn=Joe,ou=Atlanta,ou=GA,ou=US, dc=contoso,dc=com" then</span></span>  
`DNComponentRev([dn],3)`  
`DNComponentRev([dn],1,"DC")`  
<span data-ttu-id="3d184-507">Her ikisi de BİZE döndür.</span><span class="sxs-lookup"><span data-stu-id="3d184-507">Both return US.</span></span>

- - -
### <a name="error"></a><span data-ttu-id="3d184-508">Hata</span><span class="sxs-lookup"><span data-stu-id="3d184-508">Error</span></span>
<span data-ttu-id="3d184-509">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-509">**Description:**</span></span>  
<span data-ttu-id="3d184-510">Hata işlevi bir özel hata döndürmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3d184-510">The Error function is used to return a custom error.</span></span>

<span data-ttu-id="3d184-511">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-511">**Syntax:**</span></span>  
`void Error(str ErrorMessage)`

<span data-ttu-id="3d184-512">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3d184-512">**Example:**</span></span>  
`IIF(IsPresent([accountName]),[accountName],Error("AccountName is required"))`  
<span data-ttu-id="3d184-513">Öznitelik accountName mevcut değilse, bir hata nesnede atar.</span><span class="sxs-lookup"><span data-stu-id="3d184-513">If the attribute accountName is not present, throw an error on the object.</span></span>

- - -
### <a name="escapedncomponent"></a><span data-ttu-id="3d184-514">EscapeDNComponent</span><span class="sxs-lookup"><span data-stu-id="3d184-514">EscapeDNComponent</span></span>
<span data-ttu-id="3d184-515">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-515">**Description:**</span></span>  
<span data-ttu-id="3d184-516">EscapeDNComponent işlevi bir DN biri bileşenini alır ve LDAP temsil edilebilir şekilde çıkışları.</span><span class="sxs-lookup"><span data-stu-id="3d184-516">The EscapeDNComponent function takes one component of a DN and escapes it so it can be represented in LDAP.</span></span>

<span data-ttu-id="3d184-517">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-517">**Syntax:**</span></span>  
`str EscapeDNComponent(str value)`

<span data-ttu-id="3d184-518">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3d184-518">**Example:**</span></span>  
`EscapeDNComponent("cn=" & [displayName]) & "," & %ForestLDAP%)`  
<span data-ttu-id="3d184-519">DisplayName özniteliği LDAP'de kaçış karakterleri olsa bile, bir LDAP dizininde nesne oluşturulabilir emin olur.</span><span class="sxs-lookup"><span data-stu-id="3d184-519">Makes sure the object can be created in an LDAP directory even if the displayName attribute has characters that must be escaped in LDAP.</span></span>

- - -
### <a name="formatdatetime"></a><span data-ttu-id="3d184-520">FormatDateTime</span><span class="sxs-lookup"><span data-stu-id="3d184-520">FormatDateTime</span></span>
<span data-ttu-id="3d184-521">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-521">**Description:**</span></span>  
<span data-ttu-id="3d184-522">FormatDateTime işlevi DateTime bir dize olarak belirtilen biçimiyle için kullanılır</span><span class="sxs-lookup"><span data-stu-id="3d184-522">The FormatDateTime function is used to format a DateTime to a string with a specified format</span></span>

<span data-ttu-id="3d184-523">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-523">**Syntax:**</span></span>  
`str FormatDateTime(dt value, str format)`

* <span data-ttu-id="3d184-524">değer: tarih saat biçiminde bir değer</span><span class="sxs-lookup"><span data-stu-id="3d184-524">value: a value in the DateTime format</span></span>
* <span data-ttu-id="3d184-525">Biçim: dönüştürmek için kullanılacak biçimi temsil eden dize.</span><span class="sxs-lookup"><span data-stu-id="3d184-525">format: a string representing the format to convert to.</span></span>

<span data-ttu-id="3d184-526">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="3d184-526">**Remarks:**</span></span>  
<span data-ttu-id="3d184-527">Biçim için olası değerler şurada bulunabilir: [kullanıcı tanımlı tarih/saat biçimleri (biçim işlevi)](http://msdn2.microsoft.com/library/73ctwf33\(VS.90\).aspx)</span><span class="sxs-lookup"><span data-stu-id="3d184-527">The possible values for the format can be found here: [User-Defined Date/Time Formats (Format Function)](http://msdn2.microsoft.com/library/73ctwf33\(VS.90\).aspx)</span></span>

<span data-ttu-id="3d184-528">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3d184-528">**Example:**</span></span>  

`FormatDateTime(CDate("12/25/2007"),"yyyy-mm-dd")`  
<span data-ttu-id="3d184-529">"2007-12-25" sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="3d184-529">Results in "2007-12-25".</span></span>

`FormatDateTime(DateFromNum([pwdLastSet]),"yyyyMMddHHmmss.0Z")`  
<span data-ttu-id="3d184-530">"İçinde 20140905081453.0Z" neden olabilir</span><span class="sxs-lookup"><span data-stu-id="3d184-530">Can result in "20140905081453.0Z"</span></span>

- - -
### <a name="guid"></a><span data-ttu-id="3d184-531">GUID</span><span class="sxs-lookup"><span data-stu-id="3d184-531">GUID</span></span>
<span data-ttu-id="3d184-532">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-532">**Description:**</span></span>  
<span data-ttu-id="3d184-533">Yeni bir rastgele GUID GUID işlevi oluşturur</span><span class="sxs-lookup"><span data-stu-id="3d184-533">The function GUID generates a new random GUID</span></span>

<span data-ttu-id="3d184-534">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-534">**Syntax:**</span></span>  
`str GUID()`

- - -
### <a name="iif"></a><span data-ttu-id="3d184-535">IIF</span><span class="sxs-lookup"><span data-stu-id="3d184-535">IIF</span></span>
<span data-ttu-id="3d184-536">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-536">**Description:**</span></span>  
<span data-ttu-id="3d184-537">IIf işlevi belirtilen bir koşula göre olası değerlerin kümesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-537">The IIF function returns one of a set of possible values based on a specified condition.</span></span>

<span data-ttu-id="3d184-538">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-538">**Syntax:**</span></span>  
`var IIF(exp condition, var valueIfTrue, var valueIfFalse)`

* <span data-ttu-id="3d184-539">koşul: herhangi bir değer veya true veya false sonucu verebilen ifade.</span><span class="sxs-lookup"><span data-stu-id="3d184-539">condition: any value or expression that can be evaluated to true or false.</span></span>
* <span data-ttu-id="3d184-540">Koşul: koşul true olarak, döndürülen değer değerlendirilirse.</span><span class="sxs-lookup"><span data-stu-id="3d184-540">valueIfTrue: If the condition evaluates to true, the returned value.</span></span>
* <span data-ttu-id="3d184-541">valueIfFalse: koşul döndürülen değeri false olarak değerlendirilirse.</span><span class="sxs-lookup"><span data-stu-id="3d184-541">valueIfFalse: If the condition evaluates to false, the returned value.</span></span>

<span data-ttu-id="3d184-542">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3d184-542">**Example:**</span></span>  
`IIF([employeeType]="Intern","t-" & [alias],[alias])`  
 <span data-ttu-id="3d184-543">Kullanıcı bir stajyer ise "t-", başka başlangıcı eklenen sahip bir kullanıcı diğer adı olduğu gibi kullanıcının diğer adı döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-543">If the user is an intern, returns the alias of a user with "t-" added to the beginning of it, else returns the user’s alias as is.</span></span>

- - -
### <a name="instr"></a><span data-ttu-id="3d184-544">InStr</span><span class="sxs-lookup"><span data-stu-id="3d184-544">InStr</span></span>
<span data-ttu-id="3d184-545">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-545">**Description:**</span></span>  
<span data-ttu-id="3d184-546">InStr işlevi bir alt dizenin ilk örneğinin bir dizede bulur.</span><span class="sxs-lookup"><span data-stu-id="3d184-546">The InStr function finds the first occurrence of a substring in a string</span></span>

<span data-ttu-id="3d184-547">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-547">**Syntax:**</span></span>  

`num InStr(str stringcheck, str stringmatch)`  
`num InStr(str stringcheck, str stringmatch, num start)`  
`num InStr(str stringcheck, str stringmatch, num start , enum compare)`

* <span data-ttu-id="3d184-548">stringcheck: aranacak dize</span><span class="sxs-lookup"><span data-stu-id="3d184-548">stringcheck: string to be searched</span></span>
* <span data-ttu-id="3d184-549">stringmatch: dize bulunamadı</span><span class="sxs-lookup"><span data-stu-id="3d184-549">stringmatch: string to be found</span></span>
* <span data-ttu-id="3d184-550">Başlat: başlama konumu alt dizeyi bulur</span><span class="sxs-lookup"><span data-stu-id="3d184-550">start: starting position to find the substring</span></span>
* <span data-ttu-id="3d184-551">karşılaştırma: vbTextCompare veya vbBinaryCompare</span><span class="sxs-lookup"><span data-stu-id="3d184-551">compare: vbTextCompare or vbBinaryCompare</span></span>

<span data-ttu-id="3d184-552">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="3d184-552">**Remarks:**</span></span>  
<span data-ttu-id="3d184-553">Burada 0 ise bulunamadı veya alt dizeyi bulunamadı konumunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-553">Returns the position where the substring was found or 0 if not found.</span></span>

<span data-ttu-id="3d184-554">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3d184-554">**Example:**</span></span>  
`InStr("The quick brown fox","quick")`  
<span data-ttu-id="3d184-555">Evalues 5</span><span class="sxs-lookup"><span data-stu-id="3d184-555">Evalues to 5</span></span>

`InStr("repEated","e",3,vbBinaryCompare)`  
<span data-ttu-id="3d184-556">7'ye değerlendirir</span><span class="sxs-lookup"><span data-stu-id="3d184-556">Evaluates to 7</span></span>

- - -
### <a name="instrrev"></a><span data-ttu-id="3d184-557">InStrRev</span><span class="sxs-lookup"><span data-stu-id="3d184-557">InStrRev</span></span>
<span data-ttu-id="3d184-558">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-558">**Description:**</span></span>  
<span data-ttu-id="3d184-559">InStrRev işlevi bir alt dizesi son a geçişi bir dizede bulur.</span><span class="sxs-lookup"><span data-stu-id="3d184-559">The InStrRev function finds the last occurrence of a substring in a string</span></span>

<span data-ttu-id="3d184-560">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-560">**Syntax:**</span></span>  
`num InstrRev(str stringcheck, str stringmatch)`  
`num InstrRev(str stringcheck, str stringmatch, num start)`  
`num InstrRev(str stringcheck, str stringmatch, num start, enum compare)`

* <span data-ttu-id="3d184-561">stringcheck: aranacak dize</span><span class="sxs-lookup"><span data-stu-id="3d184-561">stringcheck: string to be searched</span></span>
* <span data-ttu-id="3d184-562">stringmatch: dize bulunamadı</span><span class="sxs-lookup"><span data-stu-id="3d184-562">stringmatch: string to be found</span></span>
* <span data-ttu-id="3d184-563">Başlat: başlama konumu alt dizeyi bulur</span><span class="sxs-lookup"><span data-stu-id="3d184-563">start: starting position to find the substring</span></span>
* <span data-ttu-id="3d184-564">karşılaştırma: vbTextCompare veya vbBinaryCompare</span><span class="sxs-lookup"><span data-stu-id="3d184-564">compare: vbTextCompare or vbBinaryCompare</span></span>

<span data-ttu-id="3d184-565">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="3d184-565">**Remarks:**</span></span>  
<span data-ttu-id="3d184-566">Burada 0 ise bulunamadı veya alt dizeyi bulunamadı konumunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-566">Returns the position where the substring was found or 0 if not found.</span></span>

<span data-ttu-id="3d184-567">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3d184-567">**Example:**</span></span>  
`InStrRev("abbcdbbbef","bb")`  
<span data-ttu-id="3d184-568">7 döndürür</span><span class="sxs-lookup"><span data-stu-id="3d184-568">Returns 7</span></span>

- - -
### <a name="isbitset"></a><span data-ttu-id="3d184-569">IsBitSet</span><span class="sxs-lookup"><span data-stu-id="3d184-569">IsBitSet</span></span>
<span data-ttu-id="3d184-570">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-570">**Description:**</span></span>  
<span data-ttu-id="3d184-571">Veya set IsBitSet testleri bir bit ise işlevi</span><span class="sxs-lookup"><span data-stu-id="3d184-571">The function IsBitSet Tests if a bit is set or not</span></span>

<span data-ttu-id="3d184-572">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-572">**Syntax:**</span></span>  
`bool IsBitSet(num value, num flag)`

* <span data-ttu-id="3d184-573">değer: evaluated.flag bir sayısal değer: değerlendirilecek bit olan sayısal bir değer</span><span class="sxs-lookup"><span data-stu-id="3d184-573">value: a numeric value that is evaluated.flag: a numeric value that has the bit to be evaluated</span></span>

<span data-ttu-id="3d184-574">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3d184-574">**Example:**</span></span>  
`IsBitSet(&HF,4)`  
<span data-ttu-id="3d184-575">"4" bit onaltılık değeri "F" olarak ayarlandığından True değerini döndürür</span><span class="sxs-lookup"><span data-stu-id="3d184-575">Returns True because bit "4" is set in the hexadecimal value "F"</span></span>

- - -
### <a name="isdate"></a><span data-ttu-id="3d184-576">IsDate</span><span class="sxs-lookup"><span data-stu-id="3d184-576">IsDate</span></span>
<span data-ttu-id="3d184-577">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-577">**Description:**</span></span>  
<span data-ttu-id="3d184-578">İfade olabiliyorsa IsDate işlevi True olarak değerlendirilir sonra bir DateTime türü değerlendirir.</span><span class="sxs-lookup"><span data-stu-id="3d184-578">If the expression can be evaluates as a DateTime type, then the IsDate function evaluates to True.</span></span>

<span data-ttu-id="3d184-579">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-579">**Syntax:**</span></span>  
`bool IsDate(var Expression)`

<span data-ttu-id="3d184-580">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="3d184-580">**Remarks:**</span></span>  
<span data-ttu-id="3d184-581">CDate() başarılı olup olmadığını belirlemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3d184-581">Used to determine if CDate() can be successful.</span></span>

- - -
### <a name="iscert"></a><span data-ttu-id="3d184-582">IsCert</span><span class="sxs-lookup"><span data-stu-id="3d184-582">IsCert</span></span>
<span data-ttu-id="3d184-583">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-583">**Description:**</span></span>  
<span data-ttu-id="3d184-584">.NET X509Certificate2 sertifika nesnesine ham verileri seri hale getirilebilir true değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-584">Returns true if the raw data can be serialized into .NET X509Certificate2 certificate object.</span></span>

<span data-ttu-id="3d184-585">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-585">**Syntax:**</span></span>  
`bool CertThumbprint(binary certificateRawData)`  
*   <span data-ttu-id="3d184-586">certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi.</span><span class="sxs-lookup"><span data-stu-id="3d184-586">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="3d184-587">Bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.</span><span class="sxs-lookup"><span data-stu-id="3d184-587">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>
- - -
### <a name="isempty"></a><span data-ttu-id="3d184-588">IsEmpty</span><span class="sxs-lookup"><span data-stu-id="3d184-588">IsEmpty</span></span>
<span data-ttu-id="3d184-589">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-589">**Description:**</span></span>  
<span data-ttu-id="3d184-590">Öznitelik CS veya MV var ancak boş bir dize olarak değerlendirir, IsEmpty işlevi True olarak değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="3d184-590">If the attribute is present in the CS or MV but evaluates to an empty string, then the IsEmpty function evaluates to True.</span></span>

<span data-ttu-id="3d184-591">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-591">**Syntax:**</span></span>  
`bool IsEmpty(var Expression)`

- - -
### <a name="isguid"></a><span data-ttu-id="3d184-592">IsGuid</span><span class="sxs-lookup"><span data-stu-id="3d184-592">IsGuid</span></span>
<span data-ttu-id="3d184-593">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-593">**Description:**</span></span>  
<span data-ttu-id="3d184-594">Dize için bir GUID dönüştürülebilecek, IsGuid işlevi true olarak değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="3d184-594">If the string could be converted to a GUID, then the IsGuid function evaluated to true.</span></span>

<span data-ttu-id="3d184-595">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-595">**Syntax:**</span></span>  
`bool IsGuid(str GUID)`

<span data-ttu-id="3d184-596">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="3d184-596">**Remarks:**</span></span>  
<span data-ttu-id="3d184-597">Bir GUID bu desenleri birini izleyen bir dize olarak tanımlanır: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx veya {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span><span class="sxs-lookup"><span data-stu-id="3d184-597">A GUID is defined as a string following one of these patterns: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx or {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span></span>

<span data-ttu-id="3d184-598">CGuid() başarılı olup olmadığını belirlemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3d184-598">Used to determine if CGuid() can be successful.</span></span>

<span data-ttu-id="3d184-599">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3d184-599">**Example:**</span></span>  
`IIF(IsGuid([strAttribute]),CGuid([strAttribute]),NULL)`  
<span data-ttu-id="3d184-600">GUID biçimi StrAttribute varsa, bir ikili biçimi döndürür, aksi takdirde null değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-600">If the StrAttribute has a GUID format, return a binary representation, otherwise return a Null.</span></span>

- - -
### <a name="isnull"></a><span data-ttu-id="3d184-601">IsNull</span><span class="sxs-lookup"><span data-stu-id="3d184-601">IsNull</span></span>
<span data-ttu-id="3d184-602">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-602">**Description:**</span></span>  
<span data-ttu-id="3d184-603">İfade Null olarak değerlendirilirse, IsNull işlevi true döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-603">If the expression evaluates to Null, then the IsNull function returns true.</span></span>

<span data-ttu-id="3d184-604">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-604">**Syntax:**</span></span>  
`bool IsNull(var Expression)`

<span data-ttu-id="3d184-605">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="3d184-605">**Remarks:**</span></span>  
<span data-ttu-id="3d184-606">Bir öznitelik için bir Null öznitelik yokluğu tarafından ifade edilir.</span><span class="sxs-lookup"><span data-stu-id="3d184-606">For an attribute, a Null is expressed by the absence of the attribute.</span></span>

<span data-ttu-id="3d184-607">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3d184-607">**Example:**</span></span>  
`IsNull([displayName])`  
<span data-ttu-id="3d184-608">Öznitelik CS veya MV mevcut değilse True değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-608">Returns True if the attribute is not present in the CS or MV.</span></span>

- - -
### <a name="isnullorempty"></a><span data-ttu-id="3d184-609">IsNullOrEmpty</span><span class="sxs-lookup"><span data-stu-id="3d184-609">IsNullOrEmpty</span></span>
<span data-ttu-id="3d184-610">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-610">**Description:**</span></span>  
<span data-ttu-id="3d184-611">İfade null veya boş bir dize ise, IsNullOrEmpty işlevi true döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-611">If the expression is null or an empty string, then the IsNullOrEmpty function returns true.</span></span>

<span data-ttu-id="3d184-612">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-612">**Syntax:**</span></span>  
`bool IsNullOrEmpty(var Expression)`

<span data-ttu-id="3d184-613">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="3d184-613">**Remarks:**</span></span>  
<span data-ttu-id="3d184-614">Özniteliği yok veya var ancak boş bir dize için bir öznitelik, bu True olarak değerlendirilmesi.</span><span class="sxs-lookup"><span data-stu-id="3d184-614">For an attribute, this would evaluate to True if the attribute is absent or is present but is an empty string.</span></span>  
<span data-ttu-id="3d184-615">Bu işlevinin olmasına adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="3d184-615">The inverse of this function is named IsPresent.</span></span>

<span data-ttu-id="3d184-616">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3d184-616">**Example:**</span></span>  
`IsNullOrEmpty([displayName])`  
<span data-ttu-id="3d184-617">Özniteliği mevcut değil ya da boş bir dize CS veya MV varsa True değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-617">Returns True if the attribute is not present or is an empty string in the CS or MV.</span></span>

- - -
### <a name="isnumeric"></a><span data-ttu-id="3d184-618">IsNumeric</span><span class="sxs-lookup"><span data-stu-id="3d184-618">IsNumeric</span></span>
<span data-ttu-id="3d184-619">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-619">**Description:**</span></span>  
<span data-ttu-id="3d184-620">IsNumeric işlevi bir ifadenin sayı türü değerlendirilebilir olup olmadığını gösteren bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-620">The IsNumeric function returns a Boolean value indicating whether an expression can be evaluated as a number type.</span></span>

<span data-ttu-id="3d184-621">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-621">**Syntax:**</span></span>  
`bool IsNumeric(var Expression)`

<span data-ttu-id="3d184-622">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="3d184-622">**Remarks:**</span></span>  
<span data-ttu-id="3d184-623">CNum() ifade ayrıştırma başarılı olup olmadığını belirlemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3d184-623">Used to determine if CNum() can be successful to parse the expression.</span></span>

- - -
### <a name="isstring"></a><span data-ttu-id="3d184-624">IsString</span><span class="sxs-lookup"><span data-stu-id="3d184-624">IsString</span></span>
<span data-ttu-id="3d184-625">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-625">**Description:**</span></span>  
<span data-ttu-id="3d184-626">İfade bir dize türü değerlendirilebilir, IsString işlevi True olarak değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="3d184-626">If the expression can be evaluated to a string type, then the IsString function evaluates to True.</span></span>

<span data-ttu-id="3d184-627">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-627">**Syntax:**</span></span>  
`bool IsString(var expression)`

<span data-ttu-id="3d184-628">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="3d184-628">**Remarks:**</span></span>  
<span data-ttu-id="3d184-629">CStr() ifade ayrıştırma başarılı olup olmadığını belirlemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3d184-629">Used to determine if CStr() can be successful to parse the expression.</span></span>

- - -
### <a name="ispresent"></a><span data-ttu-id="3d184-630">Olmasına</span><span class="sxs-lookup"><span data-stu-id="3d184-630">IsPresent</span></span>
<span data-ttu-id="3d184-631">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-631">**Description:**</span></span>  
<span data-ttu-id="3d184-632">İfade boş değil ve Null olmayan bir dize olarak değerlendirilirse, olmasına işlevi true döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-632">If the expression evaluates to a string that is not Null and is not empty, then the IsPresent function returns true.</span></span>

<span data-ttu-id="3d184-633">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-633">**Syntax:**</span></span>  
`bool IsPresent(var expression)`

<span data-ttu-id="3d184-634">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="3d184-634">**Remarks:**</span></span>  
<span data-ttu-id="3d184-635">Bu işlevinin IsNullOrEmpty olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="3d184-635">The inverse of this function is named IsNullOrEmpty.</span></span>

<span data-ttu-id="3d184-636">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3d184-636">**Example:**</span></span>  
`Switch(IsPresent([directManager]),[directManager], IsPresent([skiplevelManager]),[skiplevelManager], IsPresent([director]),[director])`

- - -
### <a name="item"></a><span data-ttu-id="3d184-637">Öğe</span><span class="sxs-lookup"><span data-stu-id="3d184-637">Item</span></span>
<span data-ttu-id="3d184-638">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-638">**Description:**</span></span>  
<span data-ttu-id="3d184-639">Item işlevi, birden çok değerli bir dize/özniteliğinden bir öğeyi döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-639">The Item function returns one item from a multi-valued string/attribute.</span></span>

<span data-ttu-id="3d184-640">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-640">**Syntax:**</span></span>  
`var Item(mvstr attribute, num index)`

* <span data-ttu-id="3d184-641">Öznitelik: birden çok değerli özniteliği</span><span class="sxs-lookup"><span data-stu-id="3d184-641">attribute: multi-valued attribute</span></span>
* <span data-ttu-id="3d184-642">Dizin: birden çok değerli dize içindeki bir öğenin dizini.</span><span class="sxs-lookup"><span data-stu-id="3d184-642">index: index to an item in the multi-valued string.</span></span>

<span data-ttu-id="3d184-643">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="3d184-643">**Remarks:**</span></span>  
<span data-ttu-id="3d184-644">İkinci işlevi bir öğede birden çok değerli özniteliği için dizin döndürdüğünden öğesi işlevi içerir işlevi ile birlikte yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="3d184-644">The Item function is useful together with the Contains function since the latter function returns the index to an item in the multi-valued attribute.</span></span>

<span data-ttu-id="3d184-645">Dizin sınırların dışında olması durumunda bir hata oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3d184-645">Throws an error if index is out of bounds.</span></span>

<span data-ttu-id="3d184-646">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3d184-646">**Example:**</span></span>  
`Mid(Item([proxyAddress],Contains([proxyAddress], "SMTP:")),6)`  
<span data-ttu-id="3d184-647">Birincil e-posta adresini döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-647">Returns the primary email address.</span></span>

- - -
### <a name="itemornull"></a><span data-ttu-id="3d184-648">ItemOrNull</span><span class="sxs-lookup"><span data-stu-id="3d184-648">ItemOrNull</span></span>
<span data-ttu-id="3d184-649">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-649">**Description:**</span></span>  
<span data-ttu-id="3d184-650">ItemOrNull işlevi birden çok değerli bir dize/özniteliğinden bir öğe döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-650">The ItemOrNull function returns one item from a multi-valued string/attribute.</span></span>

<span data-ttu-id="3d184-651">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-651">**Syntax:**</span></span>  
`var ItemOrNull(mvstr attribute, num index)`

* <span data-ttu-id="3d184-652">Öznitelik: birden çok değerli özniteliği</span><span class="sxs-lookup"><span data-stu-id="3d184-652">attribute: multi-valued attribute</span></span>
* <span data-ttu-id="3d184-653">Dizin: birden çok değerli dize içindeki bir öğenin dizini.</span><span class="sxs-lookup"><span data-stu-id="3d184-653">index: index to an item in the multi-valued string.</span></span>

<span data-ttu-id="3d184-654">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="3d184-654">**Remarks:**</span></span>  
<span data-ttu-id="3d184-655">İkinci işlevi bir öğede birden çok değerli özniteliği için dizin döndürdüğünden ItemOrNull işlevi ile birlikte içerir işlevi yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="3d184-655">The ItemOrNull function is useful together with the Contains function since the latter function returns the index to an item in the multi-valued attribute.</span></span>

<span data-ttu-id="3d184-656">Dizin sınırların dışında ise, bir Null değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-656">If index is out of bounds, then returns a Null value.</span></span>

- - -
### <a name="join"></a><span data-ttu-id="3d184-657">Birleştir</span><span class="sxs-lookup"><span data-stu-id="3d184-657">Join</span></span>
<span data-ttu-id="3d184-658">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-658">**Description:**</span></span>  
<span data-ttu-id="3d184-659">Birleştirme işlevi, birden çok değerli bir dize alır ve her bir öğe eklenen belirtilen ayırıcı ile tek değerli bir dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-659">The Join function takes a multi-valued string and returns a single-valued string with specified separator inserted between each item.</span></span>

<span data-ttu-id="3d184-660">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-660">**Syntax:**</span></span>  
`str Join(mvstr attribute)`  
`str Join(mvstr attribute, str Delimiter)`

* <span data-ttu-id="3d184-661">Öznitelik: birleştirilecek dizeler içeren birden çok değerli özniteliği.</span><span class="sxs-lookup"><span data-stu-id="3d184-661">attribute: Multi-valued attribute containing strings to be joined.</span></span>
* <span data-ttu-id="3d184-662">sınırlayıcı: döndürülen dize içinde alt dizeler ayırmak için kullanılan herhangi bir dize.</span><span class="sxs-lookup"><span data-stu-id="3d184-662">delimiter: Any string, used to separate the substrings in the returned string.</span></span> <span data-ttu-id="3d184-663">Atlanırsa, boşluk karakteri ("") kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3d184-663">If omitted, the space character (" ") is used.</span></span> <span data-ttu-id="3d184-664">Sınırlayıcı sıfır uzunlukta bir dize ise ("") veya hiçbir şey, listedeki tüm öğelerin hiçbir sınırlayıcıları ile birleşir.</span><span class="sxs-lookup"><span data-stu-id="3d184-664">If Delimiter is a zero-length string ("") or Nothing, all items in the list are concatenated with no delimiters.</span></span>

<span data-ttu-id="3d184-665">**Açıklamalar**</span><span class="sxs-lookup"><span data-stu-id="3d184-665">**Remarks**</span></span>  
<span data-ttu-id="3d184-666">Katılma ve bölünmüş işlevleri arasında eşlik bulunur.</span><span class="sxs-lookup"><span data-stu-id="3d184-666">There is parity between the Join and Split functions.</span></span> <span data-ttu-id="3d184-667">Birleştirme işlevi bir dizeler dizisi alır ve bunları tek bir dize döndürmek için bir sınırlayıcı dize kullanarak birleştirir.</span><span class="sxs-lookup"><span data-stu-id="3d184-667">The Join function takes an array of strings and joins them using a delimiter string, to return a single string.</span></span> <span data-ttu-id="3d184-668">Bölünmüş işlev bir dize alır ve bir dizeler dizisi döndürmek için sınırlayıcı ayırır.</span><span class="sxs-lookup"><span data-stu-id="3d184-668">The Split function takes a string and separates it at the delimiter, to return an array of strings.</span></span> <span data-ttu-id="3d184-669">Ancak, bir anahtar farktır birleştirme sınırlayıcı dizesiyle dizeyi birleştirmek, bölme yalnızca bir tek karakter ayırıcısı kullanarak dizeleri ayırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3d184-669">However, a key difference is that Join can concatenate strings with any delimiter string, Split can only separate strings using a single character delimiter.</span></span>

<span data-ttu-id="3d184-670">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3d184-670">**Example:**</span></span>  
`Join([proxyAddresses],",")`  
<span data-ttu-id="3d184-671">Döndürebilirsiniz: "SMTP:john.doe@contoso.com,smtp:jd@contoso.com"</span><span class="sxs-lookup"><span data-stu-id="3d184-671">Could return: "SMTP:john.doe@contoso.com,smtp:jd@contoso.com"</span></span>

- - -
### <a name="lcase"></a><span data-ttu-id="3d184-672">LCase</span><span class="sxs-lookup"><span data-stu-id="3d184-672">LCase</span></span>
<span data-ttu-id="3d184-673">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-673">**Description:**</span></span>  
<span data-ttu-id="3d184-674">LCase işlev bir dize içindeki tüm karakterleri küçük harflere dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-674">The LCase function converts all characters in a string to lower case.</span></span>

<span data-ttu-id="3d184-675">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-675">**Syntax:**</span></span>  
`str LCase(str value)`

<span data-ttu-id="3d184-676">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3d184-676">**Example:**</span></span>  
`LCase("TeSt")`  
<span data-ttu-id="3d184-677">"Test" döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-677">Returns "test".</span></span>

- - -
### <a name="left"></a><span data-ttu-id="3d184-678">Sol</span><span class="sxs-lookup"><span data-stu-id="3d184-678">Left</span></span>
<span data-ttu-id="3d184-679">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-679">**Description:**</span></span>  
<span data-ttu-id="3d184-680">Sol işlevi bir dizenin soldan belirtilen sayıda karakteri döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-680">The Left function returns a specified number of characters from the left of a string.</span></span>

<span data-ttu-id="3d184-681">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-681">**Syntax:**</span></span>  
`str Left(str string, num NumChars)`

* <span data-ttu-id="3d184-682">dize: dize karakterlerinden döndürmek için</span><span class="sxs-lookup"><span data-stu-id="3d184-682">string: the string to return characters from</span></span>
* <span data-ttu-id="3d184-683">NumChars: (sol) dizesi başlangıçtan itibaren döndürülecek karakter sayısını tanımlayan bir numara</span><span class="sxs-lookup"><span data-stu-id="3d184-683">NumChars: a number identifying the number of characters to return from the beginning (left) of string</span></span>

<span data-ttu-id="3d184-684">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="3d184-684">**Remarks:**</span></span>  
<span data-ttu-id="3d184-685">Dizedeki ilk numChars karakter içeren bir dize:</span><span class="sxs-lookup"><span data-stu-id="3d184-685">A string containing the first numChars characters in string:</span></span>

* <span data-ttu-id="3d184-686">Varsa numChars = 0, boş bir dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-686">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="3d184-687">NumChars < 0, döndürmesi durumunda giriş dizesi.</span><span class="sxs-lookup"><span data-stu-id="3d184-687">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="3d184-688">Dize null ise, boş bir dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-688">If string is null, return empty string.</span></span>

<span data-ttu-id="3d184-689">Sayı belirtilen numChars'den daha az karakter dizesini içeren bir dize (parametre 1'deki tüm karakterleri içeren) dizeye aynı döndürülür.</span><span class="sxs-lookup"><span data-stu-id="3d184-689">If string contains fewer characters than the number specified in numChars, a string identical to string (that is, containing all characters in parameter 1) is returned.</span></span>

<span data-ttu-id="3d184-690">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3d184-690">**Example:**</span></span>  
`Left("John Doe", 3)`  
<span data-ttu-id="3d184-691">"Joh" döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-691">Returns "Joh".</span></span>

- - -
### <a name="len"></a><span data-ttu-id="3d184-692">Len</span><span class="sxs-lookup"><span data-stu-id="3d184-692">Len</span></span>
<span data-ttu-id="3d184-693">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-693">**Description:**</span></span>  
<span data-ttu-id="3d184-694">Len işlevi bir dizedeki karakter sayısını döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-694">The Len function returns number of characters in a string.</span></span>

<span data-ttu-id="3d184-695">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-695">**Syntax:**</span></span>  
`num Len(str value)`

<span data-ttu-id="3d184-696">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3d184-696">**Example:**</span></span>  
`Len("John Doe")`  
<span data-ttu-id="3d184-697">8 döndürür</span><span class="sxs-lookup"><span data-stu-id="3d184-697">Returns 8</span></span>

- - -
### <a name="ltrim"></a><span data-ttu-id="3d184-698">LTrim</span><span class="sxs-lookup"><span data-stu-id="3d184-698">LTrim</span></span>
<span data-ttu-id="3d184-699">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-699">**Description:**</span></span>  
<span data-ttu-id="3d184-700">LTrim işlevi bir dizeden öndeki boşlukları kaldırır.</span><span class="sxs-lookup"><span data-stu-id="3d184-700">The LTrim function removes leading white spaces from a string.</span></span>

<span data-ttu-id="3d184-701">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-701">**Syntax:**</span></span>  
`str LTrim(str value)`

<span data-ttu-id="3d184-702">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3d184-702">**Example:**</span></span>  
`LTrim(" Test ")`  
<span data-ttu-id="3d184-703">"Test" döndürür</span><span class="sxs-lookup"><span data-stu-id="3d184-703">Returns "Test "</span></span>

- - -
### <a name="mid"></a><span data-ttu-id="3d184-704">Orta</span><span class="sxs-lookup"><span data-stu-id="3d184-704">Mid</span></span>
<span data-ttu-id="3d184-705">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-705">**Description:**</span></span>  
<span data-ttu-id="3d184-706">PARÇAAL işlevi bir dizedeki belirtilen konumdan belirtilen sayıda karakteri döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-706">The Mid function returns a specified number of characters from a specified position in a string.</span></span>

<span data-ttu-id="3d184-707">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-707">**Syntax:**</span></span>  
`str Mid(str string, num start, num NumChars)`

* <span data-ttu-id="3d184-708">dize: dize karakterlerinden döndürmek için</span><span class="sxs-lookup"><span data-stu-id="3d184-708">string: the string to return characters from</span></span>
* <span data-ttu-id="3d184-709">Başlat: Başlangıç tanımlayan bir numara getirin dizesindeki karakterlerinden döndürmek için</span><span class="sxs-lookup"><span data-stu-id="3d184-709">start: a number identifying the starting position in string to return characters from</span></span>
* <span data-ttu-id="3d184-710">NumChars: dizedeki döndürmek için karakter sayısını tanımlayan bir numara</span><span class="sxs-lookup"><span data-stu-id="3d184-710">NumChars: a number identifying the number of characters to return from position in string</span></span>

<span data-ttu-id="3d184-711">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="3d184-711">**Remarks:**</span></span>  
<span data-ttu-id="3d184-712">Konumundan başlayan dönüş numChars karakter dizesi içinde başlatın.</span><span class="sxs-lookup"><span data-stu-id="3d184-712">Return numChars characters starting from position start in string.</span></span>  
<span data-ttu-id="3d184-713">Konumu başlangıç dizesinde numChars karakterler içeren bir dize:</span><span class="sxs-lookup"><span data-stu-id="3d184-713">A string containing numChars characters from position start in string:</span></span>

* <span data-ttu-id="3d184-714">Varsa numChars = 0, boş bir dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-714">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="3d184-715">NumChars < 0, döndürmesi durumunda giriş dizesi.</span><span class="sxs-lookup"><span data-stu-id="3d184-715">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="3d184-716">Başlat > dize uzunluğu giriş dizesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-716">If start > the length of string, return input string.</span></span>
* <span data-ttu-id="3d184-717">Varsa Başlat < = 0, giriş dizesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-717">If start <= 0, return input string.</span></span>
* <span data-ttu-id="3d184-718">Dize null ise, boş bir dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-718">If string is null, return empty string.</span></span>

<span data-ttu-id="3d184-719">NumChar karakter değilse kadar çok konumu başından dizesinde kalan karakterler mümkün olduğunca döndürülür.</span><span class="sxs-lookup"><span data-stu-id="3d184-719">If there are not numChar characters remaining in string from position start, as many characters as possible are returned.</span></span>

<span data-ttu-id="3d184-720">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3d184-720">**Example:**</span></span>  
`Mid("John Doe", 3, 5)`  
<span data-ttu-id="3d184-721">"Hn" döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-721">Returns "hn Do".</span></span>

`Mid("John Doe", 6, 999)`  
<span data-ttu-id="3d184-722">"Doe" döndürür</span><span class="sxs-lookup"><span data-stu-id="3d184-722">Returns "Doe"</span></span>

- - -
### <a name="now"></a><span data-ttu-id="3d184-723">Şimdi</span><span class="sxs-lookup"><span data-stu-id="3d184-723">Now</span></span>
<span data-ttu-id="3d184-724">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-724">**Description:**</span></span>  
<span data-ttu-id="3d184-725">Şimdi işlevi geçerli tarih ve saat, bilgisayarınızın sistem tarihi ve saati göre belirten bir DateTime döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-725">The Now function returns a DateTime specifying the current date and time, according to your computer's system date and time.</span></span>

<span data-ttu-id="3d184-726">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-726">**Syntax:**</span></span>  
`dt Now()`

- - -
### <a name="numfromdate"></a><span data-ttu-id="3d184-727">NumFromDate</span><span class="sxs-lookup"><span data-stu-id="3d184-727">NumFromDate</span></span>
<span data-ttu-id="3d184-728">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-728">**Description:**</span></span>  
<span data-ttu-id="3d184-729">NumFromDate işlevi bir tarih Reklamın tarih biçiminde döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-729">The NumFromDate function returns a date in AD’s date format.</span></span>

<span data-ttu-id="3d184-730">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-730">**Syntax:**</span></span>  
`num NumFromDate(dt value)`

<span data-ttu-id="3d184-731">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3d184-731">**Example:**</span></span>  
`NumFromDate(CDate("2012-01-01 23:00:00"))`  
<span data-ttu-id="3d184-732">129699324000000000 döndürür</span><span class="sxs-lookup"><span data-stu-id="3d184-732">Returns 129699324000000000</span></span>

- - -
### <a name="padleft"></a><span data-ttu-id="3d184-733">PadLeft</span><span class="sxs-lookup"><span data-stu-id="3d184-733">PadLeft</span></span>
<span data-ttu-id="3d184-734">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-734">**Description:**</span></span>  
<span data-ttu-id="3d184-735">PadLeft işlevi sol-klavye takımı sağlanan doldurma karakteri kullanarak belirtilen bir süre için dize.</span><span class="sxs-lookup"><span data-stu-id="3d184-735">The PadLeft function left-pads a string to a specified length using a provided padding character.</span></span>

<span data-ttu-id="3d184-736">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-736">**Syntax:**</span></span>  
`str PadLeft(str string, num length, str padCharacter)`

* <span data-ttu-id="3d184-737">dize: doldurulacak dize.</span><span class="sxs-lookup"><span data-stu-id="3d184-737">string: the string to pad.</span></span>
* <span data-ttu-id="3d184-738">Uzunluk: istenen dize uzunluğu temsil eden bir tamsayı.</span><span class="sxs-lookup"><span data-stu-id="3d184-738">length: An integer representing the desired length of string.</span></span>
* <span data-ttu-id="3d184-739">padCharacter: doldurma karakteri olarak kullanmak üzere tek bir karakter içeren bir dize</span><span class="sxs-lookup"><span data-stu-id="3d184-739">padCharacter: A string consisting of a single character to use as the pad character</span></span>

<span data-ttu-id="3d184-740">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="3d184-740">**Remarks:**</span></span>

* <span data-ttu-id="3d184-741">Dize uzunluğu uzunluğundan az ise, ardından padCharacter art arda (bir uzunluk olana kadar Dizi uzunluğuna eşit sol) başına eklenir.</span><span class="sxs-lookup"><span data-stu-id="3d184-741">If the length of string is less than length, then padCharacter is repeatedly appended to the beginning (left) of string until it has a length equal to length.</span></span>
* <span data-ttu-id="3d184-742">padCharacter bir boşluk karakteri olabilir, ancak bir null değer olamaz.</span><span class="sxs-lookup"><span data-stu-id="3d184-742">PadCharacter can be a space character, but it cannot be a null value.</span></span>
* <span data-ttu-id="3d184-743">Dize uzunluğu eşit veya uzunluğundan büyük ise, dize değişmeden döndürülür.</span><span class="sxs-lookup"><span data-stu-id="3d184-743">If the length of string is equal to or greater than length, string is returned unchanged.</span></span>
* <span data-ttu-id="3d184-744">Dizeye özdeş bir dize, dize uzunluğu eşit veya daha büyük bir uzunluk varsa, döndürülür.</span><span class="sxs-lookup"><span data-stu-id="3d184-744">If string has a length greater than or equal to length, a string identical to string is returned.</span></span>
* <span data-ttu-id="3d184-745">Dize uzunluğu uzunluğundan az ise, yeni bir dize istenen uzunluğu padCharacter ile doldurulan içeren dize döndürülür.</span><span class="sxs-lookup"><span data-stu-id="3d184-745">If the length of string is less than length, then a new string of the desired length is returned containing string padded with a padCharacter.</span></span>
* <span data-ttu-id="3d184-746">Dize null ise, işlevi boş bir dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-746">If string is null, the function returns an empty string.</span></span>

<span data-ttu-id="3d184-747">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3d184-747">**Example:**</span></span>  
`PadLeft("User", 10, "0")`  
<span data-ttu-id="3d184-748">"000000User" döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-748">Returns "000000User".</span></span>

- - -
### <a name="padright"></a><span data-ttu-id="3d184-749">PadRight</span><span class="sxs-lookup"><span data-stu-id="3d184-749">PadRight</span></span>
<span data-ttu-id="3d184-750">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-750">**Description:**</span></span>  
<span data-ttu-id="3d184-751">PadRight işlevi sağ-klavye takımı sağlanan doldurma karakteri kullanarak belirtilen bir süre için dize.</span><span class="sxs-lookup"><span data-stu-id="3d184-751">The PadRight function right-pads a string to a specified length using a provided padding character.</span></span>

<span data-ttu-id="3d184-752">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-752">**Syntax:**</span></span>  
`str PadRight(str string, num length, str padCharacter)`

* <span data-ttu-id="3d184-753">dize: doldurulacak dize.</span><span class="sxs-lookup"><span data-stu-id="3d184-753">string: the string to pad.</span></span>
* <span data-ttu-id="3d184-754">Uzunluk: istenen dize uzunluğu temsil eden bir tamsayı.</span><span class="sxs-lookup"><span data-stu-id="3d184-754">length: An integer representing the desired length of string.</span></span>
* <span data-ttu-id="3d184-755">padCharacter: doldurma karakteri olarak kullanmak üzere tek bir karakter içeren bir dize</span><span class="sxs-lookup"><span data-stu-id="3d184-755">padCharacter: A string consisting of a single character to use as the pad character</span></span>

<span data-ttu-id="3d184-756">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="3d184-756">**Remarks:**</span></span>

* <span data-ttu-id="3d184-757">Dize uzunluğu uzunluğundan az ise, bir uzunluk uzunluğa eşit olana kadar sonra padCharacter art arda sonuna dize (sağdaki) eklenir.</span><span class="sxs-lookup"><span data-stu-id="3d184-757">If the length of string is less than length, then padCharacter is repeatedly appended to the end (right) of string until it has a length equal to length.</span></span>
* <span data-ttu-id="3d184-758">padCharacter bir boşluk karakteri olabilir, ancak bir null değer olamaz.</span><span class="sxs-lookup"><span data-stu-id="3d184-758">padCharacter can be a space character, but it cannot be a null value.</span></span>
* <span data-ttu-id="3d184-759">Dize uzunluğu eşit veya uzunluğundan büyük ise, dize değişmeden döndürülür.</span><span class="sxs-lookup"><span data-stu-id="3d184-759">If the length of string is equal to or greater than length, string is returned unchanged.</span></span>
* <span data-ttu-id="3d184-760">Dizeye özdeş bir dize, dize uzunluğu eşit veya daha büyük bir uzunluk varsa, döndürülür.</span><span class="sxs-lookup"><span data-stu-id="3d184-760">If string has a length greater than or equal to length, a string identical to string is returned.</span></span>
* <span data-ttu-id="3d184-761">Dize uzunluğu uzunluğundan az ise, yeni bir dize istenen uzunluğu padCharacter ile doldurulan içeren dize döndürülür.</span><span class="sxs-lookup"><span data-stu-id="3d184-761">If the length of string is less than length, then a new string of the desired length is returned containing string padded with a padCharacter.</span></span>
* <span data-ttu-id="3d184-762">Dize null ise, işlevi boş bir dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-762">If string is null, the function returns an empty string.</span></span>

<span data-ttu-id="3d184-763">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3d184-763">**Example:**</span></span>  
`PadRight("User", 10, "0")`  
<span data-ttu-id="3d184-764">"User000000" döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-764">Returns "User000000".</span></span>

- - -
### <a name="pcase"></a><span data-ttu-id="3d184-765">PCase</span><span class="sxs-lookup"><span data-stu-id="3d184-765">PCase</span></span>
<span data-ttu-id="3d184-766">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-766">**Description:**</span></span>  
<span data-ttu-id="3d184-767">PCase işlevi her boşlukla sözcüğün bir dizede ilk karakteri büyük harflere dönüştürür ve diğer tüm karakterleri küçük harfe dönüştürülür.</span><span class="sxs-lookup"><span data-stu-id="3d184-767">The PCase function converts the first character of each space delimited word in a string to upper case, and all other characters are converted to lower case.</span></span>

<span data-ttu-id="3d184-768">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-768">**Syntax:**</span></span>  
`String PCase(string)`

<span data-ttu-id="3d184-769">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="3d184-769">**Remarks:**</span></span>

* <span data-ttu-id="3d184-770">Bu işlev, şu anda bir kısaltma gibi tamamen büyük bir sözcük dönüştürmek için doğru büyük/küçük harf sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="3d184-770">This function does not currently provide proper casing to convert a word that is entirely uppercase, such as an acronym.</span></span>

<span data-ttu-id="3d184-771">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3d184-771">**Example:**</span></span>  
`PCase("TEsT")`  
<span data-ttu-id="3d184-772">"Test" döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-772">Returns "Test".</span></span>

`PCase(LCase("TEST"))`  
<span data-ttu-id="3d184-773">"Test" döndürür</span><span class="sxs-lookup"><span data-stu-id="3d184-773">Returns "Test"</span></span>

- - -
### <a name="randomnum"></a><span data-ttu-id="3d184-774">RandomNum</span><span class="sxs-lookup"><span data-stu-id="3d184-774">RandomNum</span></span>
<span data-ttu-id="3d184-775">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-775">**Description:**</span></span>  
<span data-ttu-id="3d184-776">RandomNum işlevi belirtilen bir zaman aralığı arasında rastgele bir sayı döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-776">The RandomNum function returns a random number between a specified interval.</span></span>

<span data-ttu-id="3d184-777">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-777">**Syntax:**</span></span>  
`num RandomNum(num start, num end)`

* <span data-ttu-id="3d184-778">Başlat: Oluşturulacak rastgele değer alt sınırı tanımlayan bir numara</span><span class="sxs-lookup"><span data-stu-id="3d184-778">start: a number identifying the lower limit of the random value to generate</span></span>
* <span data-ttu-id="3d184-779">Son: Oluşturulacak rastgele değer sayısı üst sınırı tanımlayan bir numara</span><span class="sxs-lookup"><span data-stu-id="3d184-779">end: a number identifying the upper limit of the random value to generate</span></span>

<span data-ttu-id="3d184-780">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3d184-780">**Example:**</span></span>  
`Random(100,999)`  
<span data-ttu-id="3d184-781">734 döndürebilir.</span><span class="sxs-lookup"><span data-stu-id="3d184-781">Can return 734.</span></span>

- - -
### <a name="removeduplicates"></a><span data-ttu-id="3d184-782">RemoveDuplicates</span><span class="sxs-lookup"><span data-stu-id="3d184-782">RemoveDuplicates</span></span>
<span data-ttu-id="3d184-783">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-783">**Description:**</span></span>  
<span data-ttu-id="3d184-784">RemoveDuplicates işlevi, birden çok değerli bir dize alır ve her değerin benzersiz olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="3d184-784">The RemoveDuplicates function takes a multi-valued string and make sure each value is unique.</span></span>

<span data-ttu-id="3d184-785">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-785">**Syntax:**</span></span>  
`mvstr RemoveDuplicates(mvstr attribute)`

<span data-ttu-id="3d184-786">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3d184-786">**Example:**</span></span>  
`RemoveDuplicates([proxyAddresses])`  
<span data-ttu-id="3d184-787">Burada tüm yinelenen değerleri kaldırılmış bir ayıklanmış proxyAddress özniteliği döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-787">Returns a sanitized proxyAddress attribute where all duplicate values have been removed.</span></span>

- - -
### <a name="replace"></a><span data-ttu-id="3d184-788">Değiştir</span><span class="sxs-lookup"><span data-stu-id="3d184-788">Replace</span></span>
<span data-ttu-id="3d184-789">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-789">**Description:**</span></span>  
<span data-ttu-id="3d184-790">Replace işlevi başka bir dizeye bir dizenin tüm oluşumlarını değiştirir.</span><span class="sxs-lookup"><span data-stu-id="3d184-790">The Replace function replaces all occurrences of a string to another string.</span></span>

<span data-ttu-id="3d184-791">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-791">**Syntax:**</span></span>  
`str Replace(str string, str OldValue, str NewValue)`

* <span data-ttu-id="3d184-792">dize: bir dize değerleri değiştirin.</span><span class="sxs-lookup"><span data-stu-id="3d184-792">string: A string to replace values in.</span></span>
* <span data-ttu-id="3d184-793">OldValue: Dize aramak ve değiştirmek için.</span><span class="sxs-lookup"><span data-stu-id="3d184-793">OldValue: The string to search for and to replace.</span></span>
* <span data-ttu-id="3d184-794">NewValue: için değiştirilecek dize.</span><span class="sxs-lookup"><span data-stu-id="3d184-794">NewValue: The string to replace to.</span></span>

<span data-ttu-id="3d184-795">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="3d184-795">**Remarks:**</span></span>  
<span data-ttu-id="3d184-796">İşlevi aşağıdaki özel adlar tanır:</span><span class="sxs-lookup"><span data-stu-id="3d184-796">The function recognizes the following special monikers:</span></span>

* <span data-ttu-id="3d184-797">\n – yeni satır</span><span class="sxs-lookup"><span data-stu-id="3d184-797">\n – New Line</span></span>
* <span data-ttu-id="3d184-798">\r – satır başı</span><span class="sxs-lookup"><span data-stu-id="3d184-798">\r – Carriage Return</span></span>
* <span data-ttu-id="3d184-799">\t – sekmesi</span><span class="sxs-lookup"><span data-stu-id="3d184-799">\t – Tab</span></span>

<span data-ttu-id="3d184-800">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3d184-800">**Example:**</span></span>  
`Replace([address],"\r\n",", ")`  
<span data-ttu-id="3d184-801">CRLF virgül ve boşluk ile değiştirir ve "Bir Microsoft yolu, Redmond, WA, ABD için" neden olabilir</span><span class="sxs-lookup"><span data-stu-id="3d184-801">Replaces CRLF with a comma and space, and could lead to "One Microsoft Way, Redmond, WA, USA"</span></span>

- - -
### <a name="replacechars"></a><span data-ttu-id="3d184-802">ReplaceChars</span><span class="sxs-lookup"><span data-stu-id="3d184-802">ReplaceChars</span></span>
<span data-ttu-id="3d184-803">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-803">**Description:**</span></span>  
<span data-ttu-id="3d184-804">ReplaceChars işlevi ReplacePattern dizesinde bulunan karakterleri tüm oluşumlarını değiştirir.</span><span class="sxs-lookup"><span data-stu-id="3d184-804">The ReplaceChars function replaces all occurrences of characters found in the ReplacePattern string.</span></span>

<span data-ttu-id="3d184-805">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-805">**Syntax:**</span></span>  
`str ReplaceChars(str string, str ReplacePattern)`

* <span data-ttu-id="3d184-806">dize: karakter değiştirmek için bir dize.</span><span class="sxs-lookup"><span data-stu-id="3d184-806">string: A string to replace characters in.</span></span>
* <span data-ttu-id="3d184-807">ReplacePattern: değiştirilecek karakterler içeren bir sözlük içeren bir dize.</span><span class="sxs-lookup"><span data-stu-id="3d184-807">ReplacePattern: a string containing a dictionary with characters to replace.</span></span>

<span data-ttu-id="3d184-808">{Kaynak1} biçimidir: {target1}, {kaynak2}: {target2}, {kaynakN}, {targetN} kaynağı bulmak ve değiştirmek için dize hedeflemek için karakter olduğu.</span><span class="sxs-lookup"><span data-stu-id="3d184-808">The format is {source1}:{target1},{source2}:{target2},{sourceN},{targetN} where source is the character to find and target the string to replace with.</span></span>

<span data-ttu-id="3d184-809">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="3d184-809">**Remarks:**</span></span>

* <span data-ttu-id="3d184-810">İşlev her oluşumu tanımlanan kaynakları alır ve bunları hedefleri ile değiştirir.</span><span class="sxs-lookup"><span data-stu-id="3d184-810">The function takes each occurrence of defined sources and replaces them with the targets.</span></span>
* <span data-ttu-id="3d184-811">Kaynak tam olarak bir (unicode) karakter olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="3d184-811">The source must be exactly one (unicode) character.</span></span>
* <span data-ttu-id="3d184-812">Kaynak boş veya bir karakter (ayrıştırma hatası) daha uzun olamaz.</span><span class="sxs-lookup"><span data-stu-id="3d184-812">The source cannot be empty or longer than one character (parsing error).</span></span>
* <span data-ttu-id="3d184-813">Hedef birden çok karakter, örneğin ö:oe, β:ss olabilir.</span><span class="sxs-lookup"><span data-stu-id="3d184-813">The target can have multiple characters, for example ö:oe, β:ss.</span></span>
* <span data-ttu-id="3d184-814">Hedef karakter kaldırılması gerektiğini belirten boş olabilir.</span><span class="sxs-lookup"><span data-stu-id="3d184-814">The target can be empty indicating that the character should be removed.</span></span>
* <span data-ttu-id="3d184-815">Kaynak küçük harfe duyarlıdır ve tam bir eşleşme olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="3d184-815">The source is case-sensitive and must be an exact match.</span></span>
* <span data-ttu-id="3d184-816">, (Virgül) ve: (iki nokta üst üste) ayrılmış karakterler ve bu işlevi kullanılarak değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="3d184-816">The , (comma) and : (colon) are reserved characters and cannot be replaced using this function.</span></span>
* <span data-ttu-id="3d184-817">Alanları ve diğer beyaz karakterleri ReplacePattern dizesinde göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="3d184-817">Spaces and other white characters in the ReplacePattern string are ignored.</span></span>

<span data-ttu-id="3d184-818">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3d184-818">**Example:**</span></span>  
`%ReplaceString% = ’:,Å:A,Ä:A,Ö:O,å:a,ä:a,ö,o`

`ReplaceChars("Räksmörgås",%ReplaceString%)`  
<span data-ttu-id="3d184-819">Raksmorgas döndürür</span><span class="sxs-lookup"><span data-stu-id="3d184-819">Returns Raksmorgas</span></span>

`ReplaceChars("O’Neil",%ReplaceString%)`  
<span data-ttu-id="3d184-820">Tek değer çizgilerinin "ONeil" döndürür kaldırılacak tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="3d184-820">Returns "ONeil", the single tick is defined to be removed.</span></span>

- - -
### <a name="right"></a><span data-ttu-id="3d184-821">Sağ</span><span class="sxs-lookup"><span data-stu-id="3d184-821">Right</span></span>
<span data-ttu-id="3d184-822">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-822">**Description:**</span></span>  
<span data-ttu-id="3d184-823">Right işlevi sağdan dizenin (Bitiş) belirtilen sayıda karakteri döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-823">The Right function returns a specified number of characters from the right (end) of a string.</span></span>

<span data-ttu-id="3d184-824">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-824">**Syntax:**</span></span>  
`str Right(str string, num NumChars)`

* <span data-ttu-id="3d184-825">dize: dize karakterlerinden döndürmek için</span><span class="sxs-lookup"><span data-stu-id="3d184-825">string: the string to return characters from</span></span>
* <span data-ttu-id="3d184-826">NumChars: dizesinin sonundan başlayarak (sağdaki) döndürülecek karakterlerin sayısı tanımlayan bir numara</span><span class="sxs-lookup"><span data-stu-id="3d184-826">NumChars: a number identifying the number of characters to return from the end (right) of string</span></span>

<span data-ttu-id="3d184-827">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="3d184-827">**Remarks:**</span></span>  
<span data-ttu-id="3d184-828">NumChars karakter dizesi son konumundan döndürülür.</span><span class="sxs-lookup"><span data-stu-id="3d184-828">NumChars characters are returned from the last position of string.</span></span>

<span data-ttu-id="3d184-829">Dizedeki son numChars karakter içeren bir dize:</span><span class="sxs-lookup"><span data-stu-id="3d184-829">A string containing the last numChars characters in string:</span></span>

* <span data-ttu-id="3d184-830">Varsa numChars = 0, boş bir dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-830">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="3d184-831">NumChars < 0, döndürmesi durumunda giriş dizesi.</span><span class="sxs-lookup"><span data-stu-id="3d184-831">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="3d184-832">Dize null ise, boş bir dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-832">If string is null, return empty string.</span></span>

<span data-ttu-id="3d184-833">Dize sayı belirtilen NumChars daha az karakterden içeriyorsa, dizeye özdeş bir dize döndürdü.</span><span class="sxs-lookup"><span data-stu-id="3d184-833">If string contains fewer characters than the number specified in NumChars, a string identical to string is returned.</span></span>

<span data-ttu-id="3d184-834">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3d184-834">**Example:**</span></span>  
`Right("John Doe", 3)`  
<span data-ttu-id="3d184-835">"Doe" döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-835">Returns "Doe".</span></span>

- - -
### <a name="rtrim"></a><span data-ttu-id="3d184-836">RTrim</span><span class="sxs-lookup"><span data-stu-id="3d184-836">RTrim</span></span>
<span data-ttu-id="3d184-837">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-837">**Description:**</span></span>  
<span data-ttu-id="3d184-838">RTrim işlevi bir dizeden sondaki boşluk kaldırır.</span><span class="sxs-lookup"><span data-stu-id="3d184-838">The RTrim function removes trailing white spaces from a string.</span></span>

<span data-ttu-id="3d184-839">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-839">**Syntax:**</span></span>  
`str RTrim(str value)`

<span data-ttu-id="3d184-840">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3d184-840">**Example:**</span></span>  
`RTrim(" Test ")`  
<span data-ttu-id="3d184-841">"Test" döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-841">Returns " Test".</span></span>

- - -
### <a name="select"></a><span data-ttu-id="3d184-842">Şunu seçin:</span><span class="sxs-lookup"><span data-stu-id="3d184-842">Select</span></span>
<span data-ttu-id="3d184-843">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-843">**Description:**</span></span>  
<span data-ttu-id="3d184-844">Birden çok değerli bir öznitelik (veya bir ifade çıktısını) içindeki tüm değerleri belirtilen işlevine dayalı işlemi.</span><span class="sxs-lookup"><span data-stu-id="3d184-844">Process all values in a multi-valued attribute (or output of an expression) based on function specified.</span></span>

<span data-ttu-id="3d184-845">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-845">**Syntax:**</span></span>  
`mvattr Select(variable item, mvattr attribute, func function)`  
`mvattr Select(variable item, exp expression, func function)`

* <span data-ttu-id="3d184-846">Madde: birden çok değerli öznitelik bir öğeyi temsil eder</span><span class="sxs-lookup"><span data-stu-id="3d184-846">item: Represents an element in the multi-valued attribute</span></span>
* <span data-ttu-id="3d184-847">Öznitelik: birden çok değerli özniteliği</span><span class="sxs-lookup"><span data-stu-id="3d184-847">attribute: the multi-valued attribute</span></span>
* <span data-ttu-id="3d184-848">ifade: değerler koleksiyonu döndüren bir ifadeye</span><span class="sxs-lookup"><span data-stu-id="3d184-848">expression: an expression that returns a collection of values</span></span>
* <span data-ttu-id="3d184-849">koşul: öznitelik bir öğeyi işleyebilir işlevi</span><span class="sxs-lookup"><span data-stu-id="3d184-849">condition: any function that can process an item in the attribute</span></span>

<span data-ttu-id="3d184-850">**Örnekler:**</span><span class="sxs-lookup"><span data-stu-id="3d184-850">**Examples:**</span></span>  
`Select($item,[otherPhone],Replace($item,“-”,“”))`  
<span data-ttu-id="3d184-851">Tire (-) kaldırıldıktan sonra birden çok değerli özniteliği otherPhone tüm değerleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-851">Return all the values in the multi-valued attribute otherPhone after hyphens (-) have been removed.</span></span>

- - -
### <a name="split"></a><span data-ttu-id="3d184-852">Böl</span><span class="sxs-lookup"><span data-stu-id="3d184-852">Split</span></span>
<span data-ttu-id="3d184-853">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-853">**Description:**</span></span>  
<span data-ttu-id="3d184-854">Bölünmüş işlevi bir sınırlayıcı ile ayrılmış bir dize alır ve birden çok değerli bir dize kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="3d184-854">The Split function takes a string separated with a delimiter and makes it a multi-valued string.</span></span>

<span data-ttu-id="3d184-855">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-855">**Syntax:**</span></span>  
`mvstr Split(str value, str delimiter)`  
`mvstr Split(str value, str delimiter, num limit)`

* <span data-ttu-id="3d184-856">değer: ayırmak için sınırlayıcı karakter dizesiyle.</span><span class="sxs-lookup"><span data-stu-id="3d184-856">value: the string with a delimiter character to separate.</span></span>
* <span data-ttu-id="3d184-857">sınırlayıcı: tek bir ayırıcı olarak kullanılan karakter.</span><span class="sxs-lookup"><span data-stu-id="3d184-857">delimiter: single character to be used as the delimiter.</span></span>
* <span data-ttu-id="3d184-858">sınır: en yüksek sayıda döndürebilir değeri.</span><span class="sxs-lookup"><span data-stu-id="3d184-858">limit: maximum number of values that can return.</span></span>

<span data-ttu-id="3d184-859">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3d184-859">**Example:**</span></span>  
`Split("SMTP:john.doe@contoso.com,smtp:jd@contoso.com",",")`  
<span data-ttu-id="3d184-860">ProxyAddress özniteliği için yararlı 2 öğeleri birden çok değerli bir dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-860">Returns a multi-valued string with 2 elements useful for the proxyAddress attribute.</span></span>

- - -
### <a name="stringfromguid"></a><span data-ttu-id="3d184-861">StringFromGuid</span><span class="sxs-lookup"><span data-stu-id="3d184-861">StringFromGuid</span></span>
<span data-ttu-id="3d184-862">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-862">**Description:**</span></span>  
<span data-ttu-id="3d184-863">StringFromGuid işlev ikili GUID alır ve bir dizeye dönüştürür</span><span class="sxs-lookup"><span data-stu-id="3d184-863">The StringFromGuid function takes a binary GUID and converts it to a string</span></span>

<span data-ttu-id="3d184-864">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-864">**Syntax:**</span></span>  
`str StringFromGuid(bin GUID)`

- - -
### <a name="stringfromsid"></a><span data-ttu-id="3d184-865">StringFromSid</span><span class="sxs-lookup"><span data-stu-id="3d184-865">StringFromSid</span></span>
<span data-ttu-id="3d184-866">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-866">**Description:**</span></span>  
<span data-ttu-id="3d184-867">StringFromSid işlev bir dize için bir güvenlik tanımlayıcısı içeren bir bayt dizisi dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-867">The StringFromSid function converts a byte array containing a security identifier to a string.</span></span>

<span data-ttu-id="3d184-868">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-868">**Syntax:**</span></span>  
`str StringFromSid(bin ObjectSID)`  

- - -
### <a name="switch"></a><span data-ttu-id="3d184-869">Anahtar</span><span class="sxs-lookup"><span data-stu-id="3d184-869">Switch</span></span>
<span data-ttu-id="3d184-870">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-870">**Description:**</span></span>  
<span data-ttu-id="3d184-871">Anahtar işlevini değerlendirilen koşullara göre tek bir değer döndürmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3d184-871">The Switch function is used to return a single value based on evaluated conditions.</span></span>

<span data-ttu-id="3d184-872">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-872">**Syntax:**</span></span>  
`var Switch(exp expr1, var value1[, exp expr2, var value … [, exp expr, var valueN]])`

* <span data-ttu-id="3d184-873">Expr: değerlendirmek istediğiniz değişken ifadesi.</span><span class="sxs-lookup"><span data-stu-id="3d184-873">expr: Variant expression you want to evaluate.</span></span>
* <span data-ttu-id="3d184-874">değer: karşılık gelen ifadesi True ise döndürülecek değer.</span><span class="sxs-lookup"><span data-stu-id="3d184-874">value: Value to be returned if the corresponding expression is True.</span></span>

<span data-ttu-id="3d184-875">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="3d184-875">**Remarks:**</span></span>  
<span data-ttu-id="3d184-876">Anahtar işlevi bağımsız değişken listesi ifadeleri ve değer çiftlerinden oluşur.</span><span class="sxs-lookup"><span data-stu-id="3d184-876">The Switch function argument list consists of pairs of expressions and values.</span></span> <span data-ttu-id="3d184-877">İfadeler soldan sağa değerlendirilir ve True değerlendirileceği ilk ifade ile ilişkili değeri döndürülür.</span><span class="sxs-lookup"><span data-stu-id="3d184-877">The expressions are evaluated from left to right, and the value associated with the first expression to evaluate to True is returned.</span></span> <span data-ttu-id="3d184-878">Bölümleri düzgün eşleştirilmedi, bir çalışma zamanı hatası oluşur.</span><span class="sxs-lookup"><span data-stu-id="3d184-878">If the parts aren't properly paired, a run-time error occurs.</span></span>

<span data-ttu-id="3d184-879">Örneğin, Expr1 True ise, anahtar value1 döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-879">For example, if expr1 is True, Switch returns value1.</span></span> <span data-ttu-id="3d184-880">Yanlış ifade 1., ancak expr 2 True ise, anahtar değeri 2 vb. döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-880">If expr-1 is False, but expr-2 is True, Switch returns value-2, and so on.</span></span>

<span data-ttu-id="3d184-881">Anahtar döndüren bir hiçbir şeyin varsa:</span><span class="sxs-lookup"><span data-stu-id="3d184-881">Switch returns a Nothing if:</span></span>

* <span data-ttu-id="3d184-882">İfadelerden hiçbiri True olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="3d184-882">None of the expressions are True.</span></span>
* <span data-ttu-id="3d184-883">İlk True ifade null karşılık gelen bir değer içeriyor.</span><span class="sxs-lookup"><span data-stu-id="3d184-883">The first True expression has a corresponding value that is Null.</span></span>

<span data-ttu-id="3d184-884">Bunlardan yalnızca birini döndürür olsa bile anahtar tüm ifadeler değerlendirir.</span><span class="sxs-lookup"><span data-stu-id="3d184-884">Switch evaluates all expressions, even though it returns only one of them.</span></span> <span data-ttu-id="3d184-885">Bu nedenle, istenmeyen yan etkileri için izlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="3d184-885">For this reason, you should watch for undesirable side effects.</span></span> <span data-ttu-id="3d184-886">Örneğin, herhangi bir ifade Değerlendirme hatası bir bölme sonuçlanırsa, bir hata oluşur.</span><span class="sxs-lookup"><span data-stu-id="3d184-886">For example, if the evaluation of any expression results in a division by zero error, an error occurs.</span></span>

<span data-ttu-id="3d184-887">Değer, özel bir dize döndürür hata işlevi de olabilir.</span><span class="sxs-lookup"><span data-stu-id="3d184-887">Value can also be the Error function, which would return a custom string.</span></span>

<span data-ttu-id="3d184-888">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3d184-888">**Example:**</span></span>  
`Switch([city] = "London", "English", [city] = "Rome", "Italian", [city] = "Paris", "French", True, Error("Unknown city"))`  
<span data-ttu-id="3d184-889">Bazı önemli şehirlerde konuşma dilini döndürür, aksi takdirde bir hata döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-889">Returns the language spoken in some major cities, otherwise returns an Error.</span></span>

- - -
### <a name="trim"></a><span data-ttu-id="3d184-890">Kırpma</span><span class="sxs-lookup"><span data-stu-id="3d184-890">Trim</span></span>
<span data-ttu-id="3d184-891">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-891">**Description:**</span></span>  
<span data-ttu-id="3d184-892">Kırpma işlevi baştaki ve sondaki boşlukları bir dizeden kaldırır.</span><span class="sxs-lookup"><span data-stu-id="3d184-892">The Trim function removes leading and trailing white spaces from a string.</span></span>

<span data-ttu-id="3d184-893">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-893">**Syntax:**</span></span>  
`str Trim(str value)`  

<span data-ttu-id="3d184-894">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3d184-894">**Example:**</span></span>  
`Trim(" Test ")`  
<span data-ttu-id="3d184-895">"Test" döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-895">Returns "Test".</span></span>

`Trim([proxyAddresses])`  
<span data-ttu-id="3d184-896">Baştaki ve sondaki boşlukları proxyAddress özniteliğinde her bir değer için kaldırır.</span><span class="sxs-lookup"><span data-stu-id="3d184-896">Removes leading and trailing spaces for each value in the proxyAddress attribute.</span></span>

- - -
### <a name="ucase"></a><span data-ttu-id="3d184-897">UCase</span><span class="sxs-lookup"><span data-stu-id="3d184-897">UCase</span></span>
<span data-ttu-id="3d184-898">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-898">**Description:**</span></span>  
<span data-ttu-id="3d184-899">UCase işlev bir dize içindeki tüm karakterleri büyük harfe dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-899">The UCase function converts all characters in a string to upper case.</span></span>

<span data-ttu-id="3d184-900">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-900">**Syntax:**</span></span>  
`str UCase(str string)`

<span data-ttu-id="3d184-901">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3d184-901">**Example:**</span></span>  
`UCase("TeSt")`  
<span data-ttu-id="3d184-902">"TEST" döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-902">Returns "TEST".</span></span>

- - -
### <a name="where"></a><span data-ttu-id="3d184-903">Burada</span><span class="sxs-lookup"><span data-stu-id="3d184-903">Where</span></span>

<span data-ttu-id="3d184-904">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-904">**Description:**</span></span>  
<span data-ttu-id="3d184-905">Belirli bir koşula dayalı birden çok değerli özniteliği (veya bir ifade çıktısını) değerleri kümesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-905">Returns a subset of values from a multi-valued attribute (or output of an expression) based on specific condition.</span></span>

<span data-ttu-id="3d184-906">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-906">**Syntax:**</span></span>  
`mvattr Where(variable item, mvattr attribute, exp condition)`  
`mvattr Where(variable item, exp expression, exp condition)`  
* <span data-ttu-id="3d184-907">Madde: birden çok değerli öznitelik bir öğeyi temsil eder</span><span class="sxs-lookup"><span data-stu-id="3d184-907">item: Represents an element in the multi-valued attribute</span></span>
* <span data-ttu-id="3d184-908">Öznitelik: birden çok değerli özniteliği</span><span class="sxs-lookup"><span data-stu-id="3d184-908">attribute: the multi-valued attribute</span></span>
* <span data-ttu-id="3d184-909">koşul: true veya false sonucu verebilen herhangi bir ifade</span><span class="sxs-lookup"><span data-stu-id="3d184-909">condition: any expression that can be evaluated to true or false</span></span>
* <span data-ttu-id="3d184-910">ifade: değerler koleksiyonu döndüren bir ifadeye</span><span class="sxs-lookup"><span data-stu-id="3d184-910">expression: an expression that returns a collection of values</span></span>

<span data-ttu-id="3d184-911">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3d184-911">**Example:**</span></span>  
`Where($item,[userCertificate],CertNotAfter($item)>Now())`  
<span data-ttu-id="3d184-912">Sertifika değerler, süresi dolmuş olmayan birden çok değerli özniteliği userCertificate döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-912">Return the certificate values in the multi-valued attribute userCertificate which aren’t expired.</span></span>

- - -
### <a name="with"></a><span data-ttu-id="3d184-913">İle</span><span class="sxs-lookup"><span data-stu-id="3d184-913">With</span></span>
<span data-ttu-id="3d184-914">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-914">**Description:**</span></span>  
<span data-ttu-id="3d184-915">WITH işlevi bir görünen bir alt temsil etmek için bir değişken kullanarak veya birden fazla kez karmaşık ifadesinde karmaşık bir ifade basitleştirmek için bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="3d184-915">The With function provides a way to simplify a complex expression by using a variable to represent a subexpression which appears one or more times in the complex expression.</span></span>

<span data-ttu-id="3d184-916">**Sözdizimi:**
`With(var variable, exp subExpression, exp complexExpression)`</span><span class="sxs-lookup"><span data-stu-id="3d184-916">**Syntax:**
`With(var variable, exp subExpression, exp complexExpression)`</span></span>  
* <span data-ttu-id="3d184-917">değişken: alt temsil eder.</span><span class="sxs-lookup"><span data-stu-id="3d184-917">variable: Represents the subexpression.</span></span>
* <span data-ttu-id="3d184-918">Alt: değişkeni tarafından temsil edilen alt.</span><span class="sxs-lookup"><span data-stu-id="3d184-918">subExpression: subexpression represented by variable.</span></span>
* <span data-ttu-id="3d184-919">complexExpression: karmaşık bir ifade.</span><span class="sxs-lookup"><span data-stu-id="3d184-919">complexExpression: A complex expression.</span></span>

<span data-ttu-id="3d184-920">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3d184-920">**Example:**</span></span>  
`With($unExpiredCerts,Where($item,[userCertificate],CertNotAfter($item)>Now()),IIF(Count($unExpiredCerts)>0,$unExpiredCerts,NULL))`  
<span data-ttu-id="3d184-921">İşlevsel olarak eşdeğerdir:</span><span class="sxs-lookup"><span data-stu-id="3d184-921">Is functionally equivalent to:</span></span>  
`IIF (Count(Where($item,[userCertificate],CertNotAfter($item)>Now()))>0, Where($item,[userCertificate],CertNotAfter($item)>Now()),NULL)`  
<span data-ttu-id="3d184-922">Hangi kullanıcı sertifikasını özniteliğinde yalnızca süresi dolmamış sertifika değerleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-922">Which returns only unexpired certificate values in the userCertificate attribute.</span></span>


- - -
### <a name="word"></a><span data-ttu-id="3d184-923">Word</span><span class="sxs-lookup"><span data-stu-id="3d184-923">Word</span></span>
<span data-ttu-id="3d184-924">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="3d184-924">**Description:**</span></span>  
<span data-ttu-id="3d184-925">Word işlevi kullanın ve geri dönmek için word numarası sınırlayıcıları açıklayan parametreleri temel bir dize içindeki bir sözcük döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-925">The Word function returns a word contained within a string, based on parameters describing the delimiters to use and the word number to return.</span></span>

<span data-ttu-id="3d184-926">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="3d184-926">**Syntax:**</span></span>  
`str Word(str string, num WordNumber, str delimiters)`

* <span data-ttu-id="3d184-927">dize: bir sözcük döndürmek için dize.</span><span class="sxs-lookup"><span data-stu-id="3d184-927">string: the string to return a word from.</span></span>
* <span data-ttu-id="3d184-928">WordNumber: hangi word numarasını tanımlayan bir sayı döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="3d184-928">WordNumber: a number identifying which word number should return.</span></span>
* <span data-ttu-id="3d184-929">Sınırlayıcılar: sözcükler tanımlamak için kullanılması gereken delimiter(s) temsil eden bir dize</span><span class="sxs-lookup"><span data-stu-id="3d184-929">delimiters: a string representing the delimiter(s) that should be used to identify words</span></span>

<span data-ttu-id="3d184-930">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="3d184-930">**Remarks:**</span></span>  
<span data-ttu-id="3d184-931">Her bir sınırlayıcı karakter biri ayırarak dizedeki karakter dizesini sözcükler olarak tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="3d184-931">Each string of characters in string separated by the one of the characters in delimiters are identified as words:</span></span>

* <span data-ttu-id="3d184-932">Varsa < 1 sayı, boş dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-932">If number < 1, returns empty string.</span></span>
* <span data-ttu-id="3d184-933">Dize null ise, boş bir dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d184-933">If string is null, returns empty string.</span></span>

<span data-ttu-id="3d184-934">Sözcük sayısı sayısından az dize içeriyor ya da dizesi sınırlayıcıları tarafından tanımlanan herhangi bir sözcük içermiyor, boş bir dize döndürdü.</span><span class="sxs-lookup"><span data-stu-id="3d184-934">If string contains less than number words, or string does not contain any words identified by delimiters, an empty string is returned.</span></span>

<span data-ttu-id="3d184-935">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3d184-935">**Example:**</span></span>  
`Word("The quick brown fox",3," ")`  
<span data-ttu-id="3d184-936">"Kahverengi" döndürür</span><span class="sxs-lookup"><span data-stu-id="3d184-936">Returns "brown"</span></span>

`Word("This,string!has&many separators",3,",!&#")`  
<span data-ttu-id="3d184-937">"Var" döndürür</span><span class="sxs-lookup"><span data-stu-id="3d184-937">Would return "has"</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3d184-938">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="3d184-938">Additional Resources</span></span>
* [<span data-ttu-id="3d184-939">Bildirim temelli hazırlama ifadelerini anlama</span><span class="sxs-lookup"><span data-stu-id="3d184-939">Understanding Declarative Provisioning Expressions</span></span>](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md)
* [<span data-ttu-id="3d184-940">Azure AD Connect eşitleme: Eşitleme seçeneklerini özelleştirme</span><span class="sxs-lookup"><span data-stu-id="3d184-940">Azure AD Connect Sync: Customizing Synchronization options</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="3d184-941">Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="3d184-941">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
