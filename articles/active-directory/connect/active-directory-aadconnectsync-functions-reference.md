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
ms.openlocfilehash: fbe0df856ca2efda965650fb85c7e831a0be32c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-functions-reference"></a><span data-ttu-id="1f609-103">Azure AD Connect eşitleme: işlevleri başvurusu</span><span class="sxs-lookup"><span data-stu-id="1f609-103">Azure AD Connect sync: Functions Reference</span></span>
<span data-ttu-id="1f609-104">Azure AD Connect eşitleme sırasında kullanılan toomanipulate bir öznitelik değeri işlevlerdir.</span><span class="sxs-lookup"><span data-stu-id="1f609-104">In Azure AD Connect, functions are used toomanipulate an attribute value during synchronization.</span></span>  
<span data-ttu-id="1f609-105">Merhaba hello işlevlerin sözdizimi biçimini izleyen hello kullanarak ifade edilir:</span><span class="sxs-lookup"><span data-stu-id="1f609-105">hello Syntax of hello functions is expressed using hello following format:</span></span>  
`<output type> FunctionName(<input type> <position name>, ..)`

<span data-ttu-id="1f609-106">İşlev aşırı yüklendi ve birden çok sözdizimleri kabul eder, tüm geçerli sözdizimi listelenir.</span><span class="sxs-lookup"><span data-stu-id="1f609-106">If a function is overloaded and accepts multiple syntaxes, all valid syntaxes are listed.</span></span>  
<span data-ttu-id="1f609-107">Merhaba işlevleri kesin türü belirtilmiş ve geçirilen eşleşmeleri belgelenen hello tür hello türü doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="1f609-107">hello functions are strongly typed and they verify that hello type passed in matches hello documented type.</span></span>  
<span data-ttu-id="1f609-108">Merhaba türü eşleşmiyorsa, bir hata oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="1f609-108">If hello type does not match, an error is thrown.</span></span>

<span data-ttu-id="1f609-109">Merhaba türleri sözdizimi aşağıdaki hello ile ifade edilir:</span><span class="sxs-lookup"><span data-stu-id="1f609-109">hello types are expressed with hello following syntax:</span></span>

* <span data-ttu-id="1f609-110">**Depo** – ikili</span><span class="sxs-lookup"><span data-stu-id="1f609-110">**bin** – Binary</span></span>
* <span data-ttu-id="1f609-111">**bool** – Boole</span><span class="sxs-lookup"><span data-stu-id="1f609-111">**bool** – Boolean</span></span>
* <span data-ttu-id="1f609-112">**dt** – UTC tarihi/saati</span><span class="sxs-lookup"><span data-stu-id="1f609-112">**dt** – UTC Date/Time</span></span>
* <span data-ttu-id="1f609-113">**Enum** – bilinen sabitleri numaralandırması</span><span class="sxs-lookup"><span data-stu-id="1f609-113">**enum** – Enumeration of known constants</span></span>
* <span data-ttu-id="1f609-114">**exp** – olan ifade tooevaluate tooa Boolean bekleniyor</span><span class="sxs-lookup"><span data-stu-id="1f609-114">**exp** – Expression, which is expected tooevaluate tooa Boolean</span></span>
* <span data-ttu-id="1f609-115">**mvbin** – birden çok değerli ikili</span><span class="sxs-lookup"><span data-stu-id="1f609-115">**mvbin** – Multi-Valued Binary</span></span>
* <span data-ttu-id="1f609-116">**mvstr** – birden çok değerli dize</span><span class="sxs-lookup"><span data-stu-id="1f609-116">**mvstr** – Multi-Valued String</span></span>
* <span data-ttu-id="1f609-117">**mvref** – birden çok değerli başvurusu</span><span class="sxs-lookup"><span data-stu-id="1f609-117">**mvref** – Multi-Valued Reference</span></span>
* <span data-ttu-id="1f609-118">**NUM** – sayısal</span><span class="sxs-lookup"><span data-stu-id="1f609-118">**num** – Numeric</span></span>
* <span data-ttu-id="1f609-119">**Ref** – başvurusu</span><span class="sxs-lookup"><span data-stu-id="1f609-119">**ref** – Reference</span></span>
* <span data-ttu-id="1f609-120">**str** – dize</span><span class="sxs-lookup"><span data-stu-id="1f609-120">**str** – String</span></span>
* <span data-ttu-id="1f609-121">**var** – bir değişken (neredeyse) herhangi bir tür</span><span class="sxs-lookup"><span data-stu-id="1f609-121">**var** – A variant of (almost) any other type</span></span>
* <span data-ttu-id="1f609-122">**void** – bir değer döndürmüyor</span><span class="sxs-lookup"><span data-stu-id="1f609-122">**void** – doesn’t return a value</span></span>

<span data-ttu-id="1f609-123">Merhaba işlevleri hello türleriyle **mvbin**, **mvstr**, ve **mvref** birden çok değerli öznitelikleri yalnızca çalışabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1f609-123">hello functions with hello types **mvbin**, **mvstr**, and **mvref** can only work on multi-valued attributes.</span></span> <span data-ttu-id="1f609-124">İle işlevleri **bin**, **str**, ve **ref** hem tek değerli ve birden çok değerli öznitelikleri üzerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="1f609-124">Functions with **bin**, **str**, and **ref** work on both single-valued and multi-valued attributes.</span></span>

## <a name="functions-reference"></a><span data-ttu-id="1f609-125">İşlevler Başvurusu</span><span class="sxs-lookup"><span data-stu-id="1f609-125">Functions Reference</span></span>
| <span data-ttu-id="1f609-126">İşlevlerin listesi</span><span class="sxs-lookup"><span data-stu-id="1f609-126">List of functions</span></span> |  |  |  |  |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="1f609-127">**Sertifika**</span><span class="sxs-lookup"><span data-stu-id="1f609-127">**Certificate**</span></span> | | | | |
| [<span data-ttu-id="1f609-128">CertExtensionOids</span><span class="sxs-lookup"><span data-stu-id="1f609-128">CertExtensionOids</span></span>](#certextensionoids) |[<span data-ttu-id="1f609-129">CertFormat</span><span class="sxs-lookup"><span data-stu-id="1f609-129">CertFormat</span></span>](#certformat) |[<span data-ttu-id="1f609-130">CertFriendlyName</span><span class="sxs-lookup"><span data-stu-id="1f609-130">CertFriendlyName</span></span>](#certfriendlyname) |[<span data-ttu-id="1f609-131">CertHashString</span><span class="sxs-lookup"><span data-stu-id="1f609-131">CertHashString</span></span>](#certhashstring) | |
| [<span data-ttu-id="1f609-132">CertIssuer</span><span class="sxs-lookup"><span data-stu-id="1f609-132">CertIssuer</span></span>](#certissuer) |[<span data-ttu-id="1f609-133">CertIssuerDN</span><span class="sxs-lookup"><span data-stu-id="1f609-133">CertIssuerDN</span></span>](#certissuerdn) |[<span data-ttu-id="1f609-134">CertIssuerOid</span><span class="sxs-lookup"><span data-stu-id="1f609-134">CertIssuerOid</span></span>](#certissueroid) |[<span data-ttu-id="1f609-135">CertKeyAlgorithm</span><span class="sxs-lookup"><span data-stu-id="1f609-135">CertKeyAlgorithm</span></span>](#certkeyalgorithm) | |
| [<span data-ttu-id="1f609-136">CertKeyAlgorithmParams</span><span class="sxs-lookup"><span data-stu-id="1f609-136">CertKeyAlgorithmParams</span></span>](#certkeyalgorithmparams) |[<span data-ttu-id="1f609-137">CertNameInfo</span><span class="sxs-lookup"><span data-stu-id="1f609-137">CertNameInfo</span></span>](#certnameinfo) |[<span data-ttu-id="1f609-138">CertNotAfter</span><span class="sxs-lookup"><span data-stu-id="1f609-138">CertNotAfter</span></span>](#certnotafter) |[<span data-ttu-id="1f609-139">CertNotBefore</span><span class="sxs-lookup"><span data-stu-id="1f609-139">CertNotBefore</span></span>](#certnotbefore) | |
| [<span data-ttu-id="1f609-140">CertPublicKeyOid</span><span class="sxs-lookup"><span data-stu-id="1f609-140">CertPublicKeyOid</span></span>](#certpublickeyoid) |[<span data-ttu-id="1f609-141">CertPublicKeyParametersOid</span><span class="sxs-lookup"><span data-stu-id="1f609-141">CertPublicKeyParametersOid</span></span>](#certpublickeyparametersoid) |[<span data-ttu-id="1f609-142">CertSerialNumber</span><span class="sxs-lookup"><span data-stu-id="1f609-142">CertSerialNumber</span></span>](#certserialnumber) |[<span data-ttu-id="1f609-143">CertSignatureAlgorithmOid</span><span class="sxs-lookup"><span data-stu-id="1f609-143">CertSignatureAlgorithmOid</span></span>](#certsignaturealgorithmoid) | |
| [<span data-ttu-id="1f609-144">CertSubject</span><span class="sxs-lookup"><span data-stu-id="1f609-144">CertSubject</span></span>](#certsubject) |[<span data-ttu-id="1f609-145">CertSubjectNameDN</span><span class="sxs-lookup"><span data-stu-id="1f609-145">CertSubjectNameDN</span></span>](#certsubjectnamedn) |[<span data-ttu-id="1f609-146">CertSubjectNameOid</span><span class="sxs-lookup"><span data-stu-id="1f609-146">CertSubjectNameOid</span></span>](#certsubjectnameoid) |[<span data-ttu-id="1f609-147">Certthumbprınt</span><span class="sxs-lookup"><span data-stu-id="1f609-147">CertThumbprint</span></span>](#certthumbprint) | |
[<span data-ttu-id="1f609-148">CertVersion</span><span class="sxs-lookup"><span data-stu-id="1f609-148"> CertVersion</span></span>](#certversion) |[<span data-ttu-id="1f609-149">IsCert</span><span class="sxs-lookup"><span data-stu-id="1f609-149">IsCert</span></span>](#iscert) | | | |
| <span data-ttu-id="1f609-150">**Dönüştürme**</span><span class="sxs-lookup"><span data-stu-id="1f609-150">**Conversion**</span></span> | | | | |
| [<span data-ttu-id="1f609-151">CBool</span><span class="sxs-lookup"><span data-stu-id="1f609-151">CBool</span></span>](#cbool) |[<span data-ttu-id="1f609-152">CDate</span><span class="sxs-lookup"><span data-stu-id="1f609-152">CDate</span></span>](#cdate) |[<span data-ttu-id="1f609-153">CGuid</span><span class="sxs-lookup"><span data-stu-id="1f609-153">CGuid</span></span>](#cguid) |[<span data-ttu-id="1f609-154">ConvertFromBase64</span><span class="sxs-lookup"><span data-stu-id="1f609-154">ConvertFromBase64</span></span>](#convertfrombase64) | |
| [<span data-ttu-id="1f609-155">ConvertToBase64</span><span class="sxs-lookup"><span data-stu-id="1f609-155">ConvertToBase64</span></span>](#converttobase64) |[<span data-ttu-id="1f609-156">ConvertFromUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="1f609-156">ConvertFromUTF8Hex</span></span>](#convertfromutf8hex) |[<span data-ttu-id="1f609-157">ConvertToUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="1f609-157">ConvertToUTF8Hex</span></span>](#converttoutf8hex) |[<span data-ttu-id="1f609-158">CNum</span><span class="sxs-lookup"><span data-stu-id="1f609-158">CNum</span></span>](#cnum) | |
| [<span data-ttu-id="1f609-159">CRef</span><span class="sxs-lookup"><span data-stu-id="1f609-159">CRef</span></span>](#cref) |[<span data-ttu-id="1f609-160">CStr</span><span class="sxs-lookup"><span data-stu-id="1f609-160">CStr</span></span>](#cstr) |[<span data-ttu-id="1f609-161">StringFromGuid</span><span class="sxs-lookup"><span data-stu-id="1f609-161">StringFromGuid</span></span>](#StringFromGuid) |[<span data-ttu-id="1f609-162">StringFromSid</span><span class="sxs-lookup"><span data-stu-id="1f609-162">StringFromSid</span></span>](#stringfromsid) | |
| <span data-ttu-id="1f609-163">**Tarih / saat**</span><span class="sxs-lookup"><span data-stu-id="1f609-163">**Date / Time**</span></span> | | | | |
| [<span data-ttu-id="1f609-164">DateAdd</span><span class="sxs-lookup"><span data-stu-id="1f609-164">DateAdd</span></span>](#dateadd) |[<span data-ttu-id="1f609-165">DateFromNum</span><span class="sxs-lookup"><span data-stu-id="1f609-165">DateFromNum</span></span>](#datefromnum) |[<span data-ttu-id="1f609-166">FormatDateTime</span><span class="sxs-lookup"><span data-stu-id="1f609-166">FormatDateTime</span></span>](#formatdatetime) |[<span data-ttu-id="1f609-167">Şimdi</span><span class="sxs-lookup"><span data-stu-id="1f609-167">Now</span></span>](#now) | |
| [<span data-ttu-id="1f609-168">NumFromDate</span><span class="sxs-lookup"><span data-stu-id="1f609-168">NumFromDate</span></span>](#numfromdate) | | | | |
| <span data-ttu-id="1f609-169">**Dizin**</span><span class="sxs-lookup"><span data-stu-id="1f609-169">**Directory**</span></span> | | | | |
| [<span data-ttu-id="1f609-170">DNComponent</span><span class="sxs-lookup"><span data-stu-id="1f609-170">DNComponent</span></span>](#dncomponent) |[<span data-ttu-id="1f609-171">DNComponentRev</span><span class="sxs-lookup"><span data-stu-id="1f609-171">DNComponentRev</span></span>](#dncomponentrev) |[<span data-ttu-id="1f609-172">EscapeDNComponent</span><span class="sxs-lookup"><span data-stu-id="1f609-172">EscapeDNComponent</span></span>](#escapedncomponent) | | |
| <span data-ttu-id="1f609-173">**Değerlendirme**</span><span class="sxs-lookup"><span data-stu-id="1f609-173">**Evaluation**</span></span> | | | | |
| [<span data-ttu-id="1f609-174">IsBitSet</span><span class="sxs-lookup"><span data-stu-id="1f609-174">IsBitSet</span></span>](#isbitset) |[<span data-ttu-id="1f609-175">IsDate</span><span class="sxs-lookup"><span data-stu-id="1f609-175">IsDate</span></span>](#isdate) |[<span data-ttu-id="1f609-176">IsEmpty</span><span class="sxs-lookup"><span data-stu-id="1f609-176">IsEmpty</span></span>](#isempty) |[<span data-ttu-id="1f609-177">IsGuid</span><span class="sxs-lookup"><span data-stu-id="1f609-177">IsGuid</span></span>](#isguid) | |
| [<span data-ttu-id="1f609-178">IsNull</span><span class="sxs-lookup"><span data-stu-id="1f609-178">IsNull</span></span>](#isnull) |[<span data-ttu-id="1f609-179">IsNullOrEmpty</span><span class="sxs-lookup"><span data-stu-id="1f609-179">IsNullOrEmpty</span></span>](#isnullorempty) |[<span data-ttu-id="1f609-180">IsNumeric</span><span class="sxs-lookup"><span data-stu-id="1f609-180">IsNumeric</span></span>](#isnumeric) |[<span data-ttu-id="1f609-181">Olmasına</span><span class="sxs-lookup"><span data-stu-id="1f609-181">IsPresent</span></span>](#ispresent) | |
| [<span data-ttu-id="1f609-182">IsString</span><span class="sxs-lookup"><span data-stu-id="1f609-182">IsString</span></span>](#isstring) | | | | |
| <span data-ttu-id="1f609-183">**Matematik**</span><span class="sxs-lookup"><span data-stu-id="1f609-183">**Math**</span></span> | | | | |
| [<span data-ttu-id="1f609-184">BitAnd</span><span class="sxs-lookup"><span data-stu-id="1f609-184">BitAnd</span></span>](#bitand) |[<span data-ttu-id="1f609-185">BitOr</span><span class="sxs-lookup"><span data-stu-id="1f609-185">BitOr</span></span>](#bitor) |[<span data-ttu-id="1f609-186">RandomNum</span><span class="sxs-lookup"><span data-stu-id="1f609-186">RandomNum</span></span>](#randomnum) | | |
| <span data-ttu-id="1f609-187">**Birden çok değerli**</span><span class="sxs-lookup"><span data-stu-id="1f609-187">**Multi-valued**</span></span> | | | | |
| [<span data-ttu-id="1f609-188">İçerir</span><span class="sxs-lookup"><span data-stu-id="1f609-188">Contains</span></span>](#contains) |[<span data-ttu-id="1f609-189">Sayısı</span><span class="sxs-lookup"><span data-stu-id="1f609-189">Count</span></span>](#count) |[<span data-ttu-id="1f609-190">Öğesi</span><span class="sxs-lookup"><span data-stu-id="1f609-190">Item</span></span>](#item) |[<span data-ttu-id="1f609-191">ItemOrNull</span><span class="sxs-lookup"><span data-stu-id="1f609-191">ItemOrNull</span></span>](#itemornull) | |
| [<span data-ttu-id="1f609-192">Birleştir</span><span class="sxs-lookup"><span data-stu-id="1f609-192">Join</span></span>](#join) |[<span data-ttu-id="1f609-193">RemoveDuplicates</span><span class="sxs-lookup"><span data-stu-id="1f609-193">RemoveDuplicates</span></span>](#removeduplicates) |[<span data-ttu-id="1f609-194">Böl</span><span class="sxs-lookup"><span data-stu-id="1f609-194">Split</span></span>](#split) | | |
| <span data-ttu-id="1f609-195">**Program akışı**</span><span class="sxs-lookup"><span data-stu-id="1f609-195">**Program Flow**</span></span> | | | | |
| [<span data-ttu-id="1f609-196">Hata</span><span class="sxs-lookup"><span data-stu-id="1f609-196">Error</span></span>](#error) |[<span data-ttu-id="1f609-197">IIF</span><span class="sxs-lookup"><span data-stu-id="1f609-197">IIF</span></span>](#iif) |[<span data-ttu-id="1f609-198">Seç</span><span class="sxs-lookup"><span data-stu-id="1f609-198">Select</span></span>](#select) |[<span data-ttu-id="1f609-199">Anahtar</span><span class="sxs-lookup"><span data-stu-id="1f609-199">Switch</span></span>](#switch) | |
| [<span data-ttu-id="1f609-200">Burada</span><span class="sxs-lookup"><span data-stu-id="1f609-200">Where</span></span>](#where) |[<span data-ttu-id="1f609-201">İle</span><span class="sxs-lookup"><span data-stu-id="1f609-201">With</span></span>](#with) | | | |
| <span data-ttu-id="1f609-202">**Metin**</span><span class="sxs-lookup"><span data-stu-id="1f609-202">**Text**</span></span> | | | | |
| [<span data-ttu-id="1f609-203">GUID</span><span class="sxs-lookup"><span data-stu-id="1f609-203">GUID</span></span>](#guid) |[<span data-ttu-id="1f609-204">InStr</span><span class="sxs-lookup"><span data-stu-id="1f609-204">InStr</span></span>](#instr) |[<span data-ttu-id="1f609-205">InStrRev</span><span class="sxs-lookup"><span data-stu-id="1f609-205">InStrRev</span></span>](#instrrev) |[<span data-ttu-id="1f609-206">LCase</span><span class="sxs-lookup"><span data-stu-id="1f609-206">LCase</span></span>](#lcase) | |
| [<span data-ttu-id="1f609-207">Sol</span><span class="sxs-lookup"><span data-stu-id="1f609-207">Left</span></span>](#left) |[<span data-ttu-id="1f609-208">Len</span><span class="sxs-lookup"><span data-stu-id="1f609-208">Len</span></span>](#len) |[<span data-ttu-id="1f609-209">LTrim</span><span class="sxs-lookup"><span data-stu-id="1f609-209">LTrim</span></span>](#ltrim) |[<span data-ttu-id="1f609-210">Orta</span><span class="sxs-lookup"><span data-stu-id="1f609-210">Mid</span></span>](#mid) | |
| [<span data-ttu-id="1f609-211">PadLeft</span><span class="sxs-lookup"><span data-stu-id="1f609-211">PadLeft</span></span>](#padleft) |[<span data-ttu-id="1f609-212">PadRight</span><span class="sxs-lookup"><span data-stu-id="1f609-212">PadRight</span></span>](#padright) |[<span data-ttu-id="1f609-213">PCase</span><span class="sxs-lookup"><span data-stu-id="1f609-213">PCase</span></span>](#pcase) |[<span data-ttu-id="1f609-214">Değiştir</span><span class="sxs-lookup"><span data-stu-id="1f609-214">Replace</span></span>](#replace) | |
| [<span data-ttu-id="1f609-215">ReplaceChars</span><span class="sxs-lookup"><span data-stu-id="1f609-215">ReplaceChars</span></span>](#replacechars) |[<span data-ttu-id="1f609-216">Sağ</span><span class="sxs-lookup"><span data-stu-id="1f609-216">Right</span></span>](#right) |[<span data-ttu-id="1f609-217">RTrim</span><span class="sxs-lookup"><span data-stu-id="1f609-217">RTrim</span></span>](#rtrim) |[<span data-ttu-id="1f609-218">Kırpma</span><span class="sxs-lookup"><span data-stu-id="1f609-218">Trim</span></span>](#trim) | |
| [<span data-ttu-id="1f609-219">UCase</span><span class="sxs-lookup"><span data-stu-id="1f609-219">UCase</span></span>](#ucase) |[<span data-ttu-id="1f609-220">Word</span><span class="sxs-lookup"><span data-stu-id="1f609-220">Word</span></span>](#word) | | | |

- - -
### <a name="bitand"></a><span data-ttu-id="1f609-221">BitAnd</span><span class="sxs-lookup"><span data-stu-id="1f609-221">BitAnd</span></span>
<span data-ttu-id="1f609-222">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-222">**Description:**</span></span>  
<span data-ttu-id="1f609-223">Merhaba BitAnd işlevi belirtilen BITS üzerinde bir değer ayarlar.</span><span class="sxs-lookup"><span data-stu-id="1f609-223">hello BitAnd function sets specified bits on a value.</span></span>

<span data-ttu-id="1f609-224">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-224">**Syntax:**</span></span>  
`num BitAnd(num value1, num value2)`

* <span data-ttu-id="1f609-225">value1, value2: and değerini birlikte olmalıdır sayısal değerler</span><span class="sxs-lookup"><span data-stu-id="1f609-225">value1, value2: numeric values that should be AND’ed together</span></span>

<span data-ttu-id="1f609-226">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="1f609-226">**Remarks:**</span></span>  
<span data-ttu-id="1f609-227">Bu işlev, her iki parametre toohello ikili gösterimine dönüştürür ve biraz ayarlar:</span><span class="sxs-lookup"><span data-stu-id="1f609-227">This function converts both parameters toohello binary representation and sets a bit to:</span></span>

* <span data-ttu-id="1f609-228">biri veya her ikisi içinde karşılık gelen bitler hello yoksa 0 - *maskesi* ve *bayrağı* 0</span><span class="sxs-lookup"><span data-stu-id="1f609-228">0 - if one or both of hello corresponding bits in *mask* and *flag* are 0</span></span>
* <span data-ttu-id="1f609-229">1 - hello karşılık gelen bit hem de 1 olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1f609-229">1 - if both of hello corresponding bits are 1.</span></span>

<span data-ttu-id="1f609-230">Diğer bir deyişle, her iki parametre karşılık gelen bitleri hello 1 olduğu durumlar dışında tüm durumlarda 0 döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-230">In other words, it returns 0 in all cases except when hello corresponding bits of both parameters are 1.</span></span>

<span data-ttu-id="1f609-231">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="1f609-231">**Example:**</span></span>  
`BitAnd(&HF, &HF7)`  
<span data-ttu-id="1f609-232">Onaltılık "F" ve "F7" toothis değeri değerlendirmek için 7 döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-232">Returns 7 because hexadecimal "F" AND "F7" evaluate toothis value.</span></span>

- - -
### <a name="bitor"></a><span data-ttu-id="1f609-233">BitOr</span><span class="sxs-lookup"><span data-stu-id="1f609-233">BitOr</span></span>
<span data-ttu-id="1f609-234">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-234">**Description:**</span></span>  
<span data-ttu-id="1f609-235">Merhaba BitOr işlevi belirtilen BITS üzerinde bir değer ayarlar.</span><span class="sxs-lookup"><span data-stu-id="1f609-235">hello BitOr function sets specified bits on a value.</span></span>

<span data-ttu-id="1f609-236">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-236">**Syntax:**</span></span>  
`num BitOr(num value1, num value2)`

* <span data-ttu-id="1f609-237">value1, value2: or birlikte olmalıdır sayısal değerler</span><span class="sxs-lookup"><span data-stu-id="1f609-237">value1, value2: numeric values that should be OR’ed together</span></span>

<span data-ttu-id="1f609-238">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="1f609-238">**Remarks:**</span></span>  
<span data-ttu-id="1f609-239">Bu işlev, her iki parametre toohello ikili gösterimine dönüştürür ve hello karşılık gelen BITS her ikisi de 0 olduğunda birini veya her ikisini hello karşılık gelen bit maskesi ve bayrağı 1 ve too0 olması durumunda bir bit too1 ayarlar.</span><span class="sxs-lookup"><span data-stu-id="1f609-239">This function converts both parameters toohello binary representation and sets a bit too1 if one or both of hello corresponding bits in mask and flag are 1, and too0 if both of hello corresponding bits are 0.</span></span> <span data-ttu-id="1f609-240">Diğer bir deyişle, her iki parametre hello karşılık gelen bitleri 0 nerede dışında tüm durumlarda 1 döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-240">In other words, it returns 1 in all cases except where hello corresponding bits of both parameters are 0.</span></span>

- - -
### <a name="cbool"></a><span data-ttu-id="1f609-241">CBool</span><span class="sxs-lookup"><span data-stu-id="1f609-241">CBool</span></span>
<span data-ttu-id="1f609-242">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-242">**Description:**</span></span>  
<span data-ttu-id="1f609-243">Bir Boole değeri hesaplanan hello ifadesi temelinde Hello CBool işlevi döndürür</span><span class="sxs-lookup"><span data-stu-id="1f609-243">hello CBool function returns a Boolean based on hello evaluated expression</span></span>

<span data-ttu-id="1f609-244">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-244">**Syntax:**</span></span>  
`bool CBool(exp Expression)`

<span data-ttu-id="1f609-245">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="1f609-245">**Remarks:**</span></span>  
<span data-ttu-id="1f609-246">CBool True değerini döndürür sonra hello ifadeyi tooa sıfır olmayan bir değer, hesaplar varsa, aksi takdirde, False değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-246">If hello expression evaluates tooa nonzero value, then CBool returns True, else it returns False.</span></span>

<span data-ttu-id="1f609-247">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="1f609-247">**Example:**</span></span>  
`CBool([attrib1] = [attrib2])`  

<span data-ttu-id="1f609-248">Hello aynı değeri true hem öznitelikleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-248">Returns True if both attributes have hello same value.</span></span>

- - -
### <a name="cdate"></a><span data-ttu-id="1f609-249">CDate</span><span class="sxs-lookup"><span data-stu-id="1f609-249">CDate</span></span>
<span data-ttu-id="1f609-250">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-250">**Description:**</span></span>  
<span data-ttu-id="1f609-251">Merhaba CDate işlevi bir dizeden bir UTC DateTime değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-251">hello CDate function returns a UTC DateTime from a string.</span></span> <span data-ttu-id="1f609-252">Tarih saat yerel öznitelik türü eşitlenmiş değil ancak bazı işlevler tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1f609-252">DateTime is not a native attribute type in Sync but is used by some functions.</span></span>

<span data-ttu-id="1f609-253">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-253">**Syntax:**</span></span>  
`dt CDate(str value)`

* <span data-ttu-id="1f609-254">Değer: Bir dizeyi bir tarih, saat ve isteğe bağlı olarak saat dilimi</span><span class="sxs-lookup"><span data-stu-id="1f609-254">Value: A string with a date, time, and optionally time zone</span></span>

<span data-ttu-id="1f609-255">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="1f609-255">**Remarks:**</span></span>  
<span data-ttu-id="1f609-256">Merhaba dize her zaman UTC olarak döndürülür.</span><span class="sxs-lookup"><span data-stu-id="1f609-256">hello returned string is always in UTC.</span></span>

<span data-ttu-id="1f609-257">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="1f609-257">**Example:**</span></span>  
`CDate([employeeStartTime])`  
<span data-ttu-id="1f609-258">Merhaba çalışanın başlangıç zamanı temel alınarak bir DateTime döndürür</span><span class="sxs-lookup"><span data-stu-id="1f609-258">Returns a DateTime based on hello employee’s start time</span></span>

`CDate("2013-01-10 4:00 PM -8")`  
<span data-ttu-id="1f609-259">Döndürür DateTime temsil eden bir "2013-01-11 12: 00'da"</span><span class="sxs-lookup"><span data-stu-id="1f609-259">Returns a DateTime representing "2013-01-11 12:00 AM"</span></span>








- - -
### <a name="certextensionoids"></a><span data-ttu-id="1f609-260">CertExtensionOids</span><span class="sxs-lookup"><span data-stu-id="1f609-260">CertExtensionOids</span></span>
<span data-ttu-id="1f609-261">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-261">**Description:**</span></span>  
<span data-ttu-id="1f609-262">Bir sertifika nesnesinin tüm hello Kritik Uzantılar OID değerlerini döndürür hello.</span><span class="sxs-lookup"><span data-stu-id="1f609-262">Returns hello Oid values of all hello critical extensions of a certificate object.</span></span>

<span data-ttu-id="1f609-263">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-263">**Syntax:**</span></span>  
`mvstr CertExtensionOids(binary certificateRawData)`  
*   <span data-ttu-id="1f609-264">certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi.</span><span class="sxs-lookup"><span data-stu-id="1f609-264">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="1f609-265">Merhaba bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.</span><span class="sxs-lookup"><span data-stu-id="1f609-265">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certformat"></a><span data-ttu-id="1f609-266">CertFormat</span><span class="sxs-lookup"><span data-stu-id="1f609-266">CertFormat</span></span>
<span data-ttu-id="1f609-267">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-267">**Description:**</span></span>  
<span data-ttu-id="1f609-268">Bu X.509v3 sertifikasını hello biçimi adını döndürür hello.</span><span class="sxs-lookup"><span data-stu-id="1f609-268">Returns hello name of hello format of this X.509v3 certificate.</span></span>

<span data-ttu-id="1f609-269">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-269">**Syntax:**</span></span>  
`str CertFormat(binary certificateRawData)`  
*   <span data-ttu-id="1f609-270">certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi.</span><span class="sxs-lookup"><span data-stu-id="1f609-270">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="1f609-271">Merhaba bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.</span><span class="sxs-lookup"><span data-stu-id="1f609-271">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certfriendlyname"></a><span data-ttu-id="1f609-272">CertFriendlyName</span><span class="sxs-lookup"><span data-stu-id="1f609-272">CertFriendlyName</span></span>
<span data-ttu-id="1f609-273">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-273">**Description:**</span></span>  
<span data-ttu-id="1f609-274">Diğer adı için bir sertifika ilişkili hello döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-274">Returns hello associated alias for a certificate.</span></span>

<span data-ttu-id="1f609-275">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-275">**Syntax:**</span></span>  
`str CertFriendlyName(binary certificateRawData)`  
*   <span data-ttu-id="1f609-276">certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi.</span><span class="sxs-lookup"><span data-stu-id="1f609-276">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="1f609-277">Merhaba bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.</span><span class="sxs-lookup"><span data-stu-id="1f609-277">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certhashstring"></a><span data-ttu-id="1f609-278">CertHashString</span><span class="sxs-lookup"><span data-stu-id="1f609-278">CertHashString</span></span>
<span data-ttu-id="1f609-279">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-279">**Description:**</span></span>  
<span data-ttu-id="1f609-280">Döndürür hello X.509v3 sertifikasını SHA1 karma değeri bir onaltılık dize hello.</span><span class="sxs-lookup"><span data-stu-id="1f609-280">Returns hello SHA1 hash value for hello X.509v3 certificate as a hexadecimal string.</span></span>

<span data-ttu-id="1f609-281">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-281">**Syntax:**</span></span>  
`str CertHashString(binary certificateRawData)`  
*   <span data-ttu-id="1f609-282">certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi.</span><span class="sxs-lookup"><span data-stu-id="1f609-282">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="1f609-283">Merhaba bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.</span><span class="sxs-lookup"><span data-stu-id="1f609-283">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certissuer"></a><span data-ttu-id="1f609-284">CertIssuer</span><span class="sxs-lookup"><span data-stu-id="1f609-284">CertIssuer</span></span>
<span data-ttu-id="1f609-285">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-285">**Description:**</span></span>  
<span data-ttu-id="1f609-286">Döndürür hello X.509v3 sertifikasını veren hello sertifika yetkilisinin adı hello.</span><span class="sxs-lookup"><span data-stu-id="1f609-286">Returns hello name of hello certificate authority that issued hello X.509v3 certificate.</span></span>

<span data-ttu-id="1f609-287">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-287">**Syntax:**</span></span>  
`str CertIssuer(binary certificateRawData)`  
*   <span data-ttu-id="1f609-288">certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi.</span><span class="sxs-lookup"><span data-stu-id="1f609-288">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="1f609-289">Merhaba bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.</span><span class="sxs-lookup"><span data-stu-id="1f609-289">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certissuerdn"></a><span data-ttu-id="1f609-290">CertIssuerDN</span><span class="sxs-lookup"><span data-stu-id="1f609-290">CertIssuerDN</span></span>
<span data-ttu-id="1f609-291">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-291">**Description:**</span></span>  
<span data-ttu-id="1f609-292">Döndürür hello sertifikayı verenin ayırt edici adı hello.</span><span class="sxs-lookup"><span data-stu-id="1f609-292">Returns hello distinguished name of hello certificate issuer.</span></span>

<span data-ttu-id="1f609-293">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-293">**Syntax:**</span></span>  
`str CertIssuerDN(binary certificateRawData)`  
*   <span data-ttu-id="1f609-294">certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi.</span><span class="sxs-lookup"><span data-stu-id="1f609-294">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="1f609-295">Merhaba bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.</span><span class="sxs-lookup"><span data-stu-id="1f609-295">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certissueroid"></a><span data-ttu-id="1f609-296">CertIssuerOid</span><span class="sxs-lookup"><span data-stu-id="1f609-296">CertIssuerOid</span></span>
<span data-ttu-id="1f609-297">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-297">**Description:**</span></span>  
<span data-ttu-id="1f609-298">Döndürür hello sertifika verenin OID hello.</span><span class="sxs-lookup"><span data-stu-id="1f609-298">Returns hello Oid of hello certificate issuer.</span></span>

<span data-ttu-id="1f609-299">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-299">**Syntax:**</span></span>  
`str CertIssuerOid(binary certificateRawData)`  
*   <span data-ttu-id="1f609-300">certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi.</span><span class="sxs-lookup"><span data-stu-id="1f609-300">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="1f609-301">Merhaba bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.</span><span class="sxs-lookup"><span data-stu-id="1f609-301">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certkeyalgorithm"></a><span data-ttu-id="1f609-302">CertKeyAlgorithm</span><span class="sxs-lookup"><span data-stu-id="1f609-302">CertKeyAlgorithm</span></span>
<span data-ttu-id="1f609-303">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-303">**Description:**</span></span>  
<span data-ttu-id="1f609-304">Merhaba anahtar algoritması bilgi bu X.509v3 sertifikasını için bir dize olarak döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-304">Returns hello key algorithm information for this X.509v3 certificate as a string.</span></span>

<span data-ttu-id="1f609-305">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-305">**Syntax:**</span></span>  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   <span data-ttu-id="1f609-306">certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi.</span><span class="sxs-lookup"><span data-stu-id="1f609-306">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="1f609-307">Merhaba bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.</span><span class="sxs-lookup"><span data-stu-id="1f609-307">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certkeyalgorithmparams"></a><span data-ttu-id="1f609-308">CertKeyAlgorithmParams</span><span class="sxs-lookup"><span data-stu-id="1f609-308">CertKeyAlgorithmParams</span></span>
<span data-ttu-id="1f609-309">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-309">**Description:**</span></span>  
<span data-ttu-id="1f609-310">Merhaba anahtar algoritması parametreleri hello X.509v3 sertifikasını için bir onaltılık dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-310">Returns hello key algorithm parameters for hello X.509v3 certificate as a hexadecimal string.</span></span>

<span data-ttu-id="1f609-311">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-311">**Syntax:**</span></span>  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   <span data-ttu-id="1f609-312">certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi.</span><span class="sxs-lookup"><span data-stu-id="1f609-312">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="1f609-313">Merhaba bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.</span><span class="sxs-lookup"><span data-stu-id="1f609-313">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certnameinfo"></a><span data-ttu-id="1f609-314">CertNameInfo</span><span class="sxs-lookup"><span data-stu-id="1f609-314">CertNameInfo</span></span>
<span data-ttu-id="1f609-315">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-315">**Description:**</span></span>  
<span data-ttu-id="1f609-316">Merhaba konu ve sertifikayı veren adları bir sertifika verir.</span><span class="sxs-lookup"><span data-stu-id="1f609-316">Returns hello subject and issuer names from a certificate.</span></span>

<span data-ttu-id="1f609-317">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-317">**Syntax:**</span></span>  
`str CertNameInfo(binary certificateRawData, str x509NameType, bool includesIssuerName)`  
*   <span data-ttu-id="1f609-318">certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi.</span><span class="sxs-lookup"><span data-stu-id="1f609-318">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="1f609-319">Merhaba bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.</span><span class="sxs-lookup"><span data-stu-id="1f609-319">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>
*   <span data-ttu-id="1f609-320">X509NameType: hello hello konu X509NameType değeri.</span><span class="sxs-lookup"><span data-stu-id="1f609-320">X509NameType: hello X509NameType value for hello subject.</span></span>
*   <span data-ttu-id="1f609-321">includesIssuerName: true tooinclude hello verenin adı; Aksi takdirde false.</span><span class="sxs-lookup"><span data-stu-id="1f609-321">includesIssuerName: true tooinclude hello issuer name; otherwise, false.</span></span>

- - -
### <a name="certnotafter"></a><span data-ttu-id="1f609-322">CertNotAfter</span><span class="sxs-lookup"><span data-stu-id="1f609-322">CertNotAfter</span></span>
<span data-ttu-id="1f609-323">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-323">**Description:**</span></span>  
<span data-ttu-id="1f609-324">Yerel saatle sonra bir sertifika artık geçerli olduğu başlangıç tarihi döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-324">Returns hello date in local time after which a certificate is no longer valid.</span></span>

<span data-ttu-id="1f609-325">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-325">**Syntax:**</span></span>  
`dt CertNotAfter(binary certificateRawData)`  
*   <span data-ttu-id="1f609-326">certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi.</span><span class="sxs-lookup"><span data-stu-id="1f609-326">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="1f609-327">Merhaba bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.</span><span class="sxs-lookup"><span data-stu-id="1f609-327">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certnotbefore"></a><span data-ttu-id="1f609-328">CertNotBefore</span><span class="sxs-lookup"><span data-stu-id="1f609-328">CertNotBefore</span></span>
<span data-ttu-id="1f609-329">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-329">**Description:**</span></span>  
<span data-ttu-id="1f609-330">Yerel saatte bir sertifikanın geçerli hale geldiği Hello tarihi döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-330">Returns hello date in local time on which a certificate becomes valid.</span></span>

<span data-ttu-id="1f609-331">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-331">**Syntax:**</span></span>  
`dt CertNotBefore(binary certificateRawData)`  
*   <span data-ttu-id="1f609-332">certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi.</span><span class="sxs-lookup"><span data-stu-id="1f609-332">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="1f609-333">Merhaba bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.</span><span class="sxs-lookup"><span data-stu-id="1f609-333">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certpublickeyoid"></a><span data-ttu-id="1f609-334">CertPublicKeyOid</span><span class="sxs-lookup"><span data-stu-id="1f609-334">CertPublicKeyOid</span></span>
<span data-ttu-id="1f609-335">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-335">**Description:**</span></span>  
<span data-ttu-id="1f609-336">Döndürür hello X.509v3 sertifikası için ortak anahtar hello OID hello.</span><span class="sxs-lookup"><span data-stu-id="1f609-336">Returns hello Oid of hello public key for hello X.509v3 certificate.</span></span>

<span data-ttu-id="1f609-337">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-337">**Syntax:**</span></span>  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   <span data-ttu-id="1f609-338">certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi.</span><span class="sxs-lookup"><span data-stu-id="1f609-338">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="1f609-339">Merhaba bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.</span><span class="sxs-lookup"><span data-stu-id="1f609-339">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certpublickeyparametersoid"></a><span data-ttu-id="1f609-340">CertPublicKeyParametersOid</span><span class="sxs-lookup"><span data-stu-id="1f609-340">CertPublicKeyParametersOid</span></span>
<span data-ttu-id="1f609-341">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-341">**Description:**</span></span>  
<span data-ttu-id="1f609-342">Ortak anahtar parametrelerini hello X.509v3 sertifikasını hello OID döndürür hello.</span><span class="sxs-lookup"><span data-stu-id="1f609-342">Returns hello Oid of hello public key parameters for hello X.509v3 certificate.</span></span>

<span data-ttu-id="1f609-343">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-343">**Syntax:**</span></span>  
`str CertPublicKeyParametersOid(binary certificateRawData)`  
*   <span data-ttu-id="1f609-344">certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi.</span><span class="sxs-lookup"><span data-stu-id="1f609-344">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="1f609-345">Merhaba bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.</span><span class="sxs-lookup"><span data-stu-id="1f609-345">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certserialnumber"></a><span data-ttu-id="1f609-346">CertSerialNumber</span><span class="sxs-lookup"><span data-stu-id="1f609-346">CertSerialNumber</span></span>
<span data-ttu-id="1f609-347">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-347">**Description:**</span></span>  
<span data-ttu-id="1f609-348">Merhaba X.509v3 sertifikasını Hello seri numarasını döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-348">Returns hello serial number of hello X.509v3 certificate.</span></span>

<span data-ttu-id="1f609-349">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-349">**Syntax:**</span></span>  
`str CertSerialNumber(binary certificateRawData)`  
*   <span data-ttu-id="1f609-350">certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi.</span><span class="sxs-lookup"><span data-stu-id="1f609-350">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="1f609-351">Merhaba bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.</span><span class="sxs-lookup"><span data-stu-id="1f609-351">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsignaturealgorithmoid"></a><span data-ttu-id="1f609-352">CertSignatureAlgorithmOid</span><span class="sxs-lookup"><span data-stu-id="1f609-352">CertSignatureAlgorithmOid</span></span>
<span data-ttu-id="1f609-353">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-353">**Description:**</span></span>  
<span data-ttu-id="1f609-354">Döndürür hello hello algoritmasının OID toocreate hello bir sertifikanın imzasını kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1f609-354">Returns hello Oid of hello algorithm used toocreate hello signature of a certificate.</span></span>

<span data-ttu-id="1f609-355">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-355">**Syntax:**</span></span>  
`str CertSignatureAlgorithmOid(binary certificateRawData)`  
*   <span data-ttu-id="1f609-356">certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi.</span><span class="sxs-lookup"><span data-stu-id="1f609-356">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="1f609-357">Merhaba bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.</span><span class="sxs-lookup"><span data-stu-id="1f609-357">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsubject"></a><span data-ttu-id="1f609-358">CertSubject</span><span class="sxs-lookup"><span data-stu-id="1f609-358">CertSubject</span></span>
<span data-ttu-id="1f609-359">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-359">**Description:**</span></span>  
<span data-ttu-id="1f609-360">Bir sertifikadan konu ayırt edici adı alır hello.</span><span class="sxs-lookup"><span data-stu-id="1f609-360">Gets hello subject distinguished name from a certificate.</span></span>

<span data-ttu-id="1f609-361">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-361">**Syntax:**</span></span>  
`str CertSubject(binary certificateRawData)`  
*   <span data-ttu-id="1f609-362">certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi.</span><span class="sxs-lookup"><span data-stu-id="1f609-362">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="1f609-363">Merhaba bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.</span><span class="sxs-lookup"><span data-stu-id="1f609-363">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsubjectnamedn"></a><span data-ttu-id="1f609-364">CertSubjectNameDN</span><span class="sxs-lookup"><span data-stu-id="1f609-364">CertSubjectNameDN</span></span>
<span data-ttu-id="1f609-365">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-365">**Description:**</span></span>  
<span data-ttu-id="1f609-366">Bir sertifikadan konu ayırt edici adı döndürür hello.</span><span class="sxs-lookup"><span data-stu-id="1f609-366">Returns hello subject distinguished name from a certificate.</span></span>

<span data-ttu-id="1f609-367">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-367">**Syntax:**</span></span>  
`str CertSubjectNameDN(binary certificateRawData)`  
*   <span data-ttu-id="1f609-368">certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi.</span><span class="sxs-lookup"><span data-stu-id="1f609-368">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="1f609-369">Merhaba bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.</span><span class="sxs-lookup"><span data-stu-id="1f609-369">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsubjectnameoid"></a><span data-ttu-id="1f609-370">CertSubjectNameOid</span><span class="sxs-lookup"><span data-stu-id="1f609-370">CertSubjectNameOid</span></span>
<span data-ttu-id="1f609-371">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-371">**Description:**</span></span>  
<span data-ttu-id="1f609-372">Bir sertifikadan konu adı hello OID döndürür hello.</span><span class="sxs-lookup"><span data-stu-id="1f609-372">Returns hello Oid of hello subject name from a certificate.</span></span>

<span data-ttu-id="1f609-373">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-373">**Syntax:**</span></span>  
`str CertSubjectNameOid(binary certificateRawData)`  
*   <span data-ttu-id="1f609-374">certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi.</span><span class="sxs-lookup"><span data-stu-id="1f609-374">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="1f609-375">Merhaba bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.</span><span class="sxs-lookup"><span data-stu-id="1f609-375">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certthumbprint"></a><span data-ttu-id="1f609-376">Certthumbprınt</span><span class="sxs-lookup"><span data-stu-id="1f609-376">CertThumbprint</span></span>
<span data-ttu-id="1f609-377">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-377">**Description:**</span></span>  
<span data-ttu-id="1f609-378">Bir sertifikanın parmak izini döndürür hello.</span><span class="sxs-lookup"><span data-stu-id="1f609-378">Returns hello thumbprint of a certificate.</span></span>

<span data-ttu-id="1f609-379">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-379">**Syntax:**</span></span>  
`str CertThumbprint(binary certificateRawData)`  
*   <span data-ttu-id="1f609-380">certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi.</span><span class="sxs-lookup"><span data-stu-id="1f609-380">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="1f609-381">Merhaba bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.</span><span class="sxs-lookup"><span data-stu-id="1f609-381">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certversion"></a><span data-ttu-id="1f609-382">CertVersion</span><span class="sxs-lookup"><span data-stu-id="1f609-382">CertVersion</span></span>
<span data-ttu-id="1f609-383">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-383">**Description:**</span></span>  
<span data-ttu-id="1f609-384">Bir sertifikanın X.509 biçimindeki sürümü döndürür hello.</span><span class="sxs-lookup"><span data-stu-id="1f609-384">Returns hello X.509 format version of a certificate.</span></span>

<span data-ttu-id="1f609-385">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-385">**Syntax:**</span></span>  
`str CertThumbprint(binary certificateRawData)`  
*   <span data-ttu-id="1f609-386">certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi.</span><span class="sxs-lookup"><span data-stu-id="1f609-386">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="1f609-387">Merhaba bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.</span><span class="sxs-lookup"><span data-stu-id="1f609-387">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="cguid"></a><span data-ttu-id="1f609-388">CGuid</span><span class="sxs-lookup"><span data-stu-id="1f609-388">CGuid</span></span>
<span data-ttu-id="1f609-389">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-389">**Description:**</span></span>  
<span data-ttu-id="1f609-390">Merhaba CGuid işlevi bir GUID tooits ikili gösterim hello dize gösterimini dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-390">hello CGuid function converts hello string representation of a GUID tooits binary representation.</span></span>

<span data-ttu-id="1f609-391">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-391">**Syntax:**</span></span>  
`bin CGuid(str GUID)`

* <span data-ttu-id="1f609-392">Bu desen biçimlendirilmiş bir dize: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx veya {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span><span class="sxs-lookup"><span data-stu-id="1f609-392">A String formatted in this pattern: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx or {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span></span>

- - -
### <a name="contains"></a><span data-ttu-id="1f609-393">Contains</span><span class="sxs-lookup"><span data-stu-id="1f609-393">Contains</span></span>
<span data-ttu-id="1f609-394">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-394">**Description:**</span></span>  
<span data-ttu-id="1f609-395">Merhaba içerir işlev bir dize birden çok değerli özniteliğinde bulur</span><span class="sxs-lookup"><span data-stu-id="1f609-395">hello Contains function finds a string inside a multi-valued attribute</span></span>

<span data-ttu-id="1f609-396">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-396">**Syntax:**</span></span>  
<span data-ttu-id="1f609-397">`num Contains (mvstring attribute, str search)`-büyük küçük harfe duyarlı</span><span class="sxs-lookup"><span data-stu-id="1f609-397">`num Contains (mvstring attribute, str search)` - case-sensitive</span></span>  
`num Contains (mvstring attribute, str search, enum Casetype)`  
<span data-ttu-id="1f609-398">`num Contains (mvref attribute, str search)`-büyük küçük harfe duyarlı</span><span class="sxs-lookup"><span data-stu-id="1f609-398">`num Contains (mvref attribute, str search)` - case-sensitive</span></span>

* <span data-ttu-id="1f609-399">Öznitelik: hello birden çok değerli özniteliği toosearch.</span><span class="sxs-lookup"><span data-stu-id="1f609-399">attribute: hello multi-valued attribute toosearch.</span></span>
* <span data-ttu-id="1f609-400">Arama: hello özniteliğinde toofind dize.</span><span class="sxs-lookup"><span data-stu-id="1f609-400">search: string toofind in hello attribute.</span></span>
* <span data-ttu-id="1f609-401">Casetype: CaseInsensitive veya CaseSensitive.</span><span class="sxs-lookup"><span data-stu-id="1f609-401">Casetype: CaseInsensitive or CaseSensitive.</span></span>

<span data-ttu-id="1f609-402">Dizin hello dize bulunduğu hello birden çok değerli özniteliği döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-402">Returns index in hello multi-valued attribute where hello string was found.</span></span> <span data-ttu-id="1f609-403">Merhaba dize bulunamazsa, 0 döndürülür.</span><span class="sxs-lookup"><span data-stu-id="1f609-403">0 is returned if hello string is not found.</span></span>

<span data-ttu-id="1f609-404">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="1f609-404">**Remarks:**</span></span>  
<span data-ttu-id="1f609-405">Birden çok değerli dize öznitelikleri için hello arama alt dizeler hello değerleri bulur.</span><span class="sxs-lookup"><span data-stu-id="1f609-405">For multi-valued string attributes, hello search finds substrings in hello values.</span></span>  
<span data-ttu-id="1f609-406">Başvuru özniteliği için hello Aranan dize tam olarak bir eşleşme olarak kabul hello değeri toobe eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="1f609-406">For reference attributes, hello searched string must exactly match hello value toobe considered a match.</span></span>

<span data-ttu-id="1f609-407">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="1f609-407">**Example:**</span></span>  
`IIF(Contains([proxyAddresses],"SMTP:")>0,[proxyAddresses],Error("No primary SMTP address found."))`  
<span data-ttu-id="1f609-408">Bir birincil e-posta adresi Hello proxyAddresses özniteliğine sahipse, (büyük harf tarafından gösterilen "SMTP:"), hello proxyAddress özniteliği döndürür, aksi takdirde bir hata döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-408">If hello proxyAddresses attribute has a primary email address (indicated by uppercase "SMTP:"), then return hello proxyAddress attribute, else return an error.</span></span>

- - -
### <a name="convertfrombase64"></a><span data-ttu-id="1f609-409">ConvertFromBase64</span><span class="sxs-lookup"><span data-stu-id="1f609-409">ConvertFromBase64</span></span>
<span data-ttu-id="1f609-410">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-410">**Description:**</span></span>  
<span data-ttu-id="1f609-411">Merhaba ConvertFromBase64 işlevi dönüştürür hello base64 kodlu değer tooa normal dizesi belirtildi.</span><span class="sxs-lookup"><span data-stu-id="1f609-411">hello ConvertFromBase64 function converts hello specified base64 encoded value tooa regular string.</span></span>

<span data-ttu-id="1f609-412">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-412">**Syntax:**</span></span>  
<span data-ttu-id="1f609-413">`str ConvertFromBase64(str source)`-Unicode kodlama için varsayar.</span><span class="sxs-lookup"><span data-stu-id="1f609-413">`str ConvertFromBase64(str source)` - assumes Unicode for encoding</span></span>  
`str ConvertFromBase64(str source, enum Encoding)`

* <span data-ttu-id="1f609-414">Kaynak: Base64 ile kodlanmış dize</span><span class="sxs-lookup"><span data-stu-id="1f609-414">source: Base64 encoded string</span></span>  
* <span data-ttu-id="1f609-415">Kodlaması: Unicode, ASCII, UTF8</span><span class="sxs-lookup"><span data-stu-id="1f609-415">Encoding: Unicode, ASCII, UTF8</span></span>

<span data-ttu-id="1f609-416">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="1f609-416">**Example**</span></span>  
`ConvertFromBase64("SABlAGwAbABvACAAdwBvAHIAbABkACEA")`  
`ConvertFromBase64("SGVsbG8gd29ybGQh", UTF8)`

<span data-ttu-id="1f609-417">Örneklerin her ikisi de döndürmek "*Merhaba Dünya!*"</span><span class="sxs-lookup"><span data-stu-id="1f609-417">Both examples return "*Hello world!*"</span></span>

- - -
### <a name="convertfromutf8hex"></a><span data-ttu-id="1f609-418">ConvertFromUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="1f609-418">ConvertFromUTF8Hex</span></span>
<span data-ttu-id="1f609-419">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-419">**Description:**</span></span>  
<span data-ttu-id="1f609-420">Merhaba ConvertFromUTF8Hex işlevi dönüştürür hello UTF8 olarak kodlanmış onaltılık değer tooa dizesi belirtildi.</span><span class="sxs-lookup"><span data-stu-id="1f609-420">hello ConvertFromUTF8Hex function converts hello specified UTF8 Hex encoded value tooa string.</span></span>

<span data-ttu-id="1f609-421">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-421">**Syntax:**</span></span>  
`str ConvertFromUTF8Hex(str source)`

* <span data-ttu-id="1f609-422">Kaynak: UTF8 2-bayt kodlanmış dizesi</span><span class="sxs-lookup"><span data-stu-id="1f609-422">source: UTF8 2-byte encoded sting</span></span>

<span data-ttu-id="1f609-423">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="1f609-423">**Remarks:**</span></span>  
<span data-ttu-id="1f609-424">Merhaba ile arasındaki fark bu işlevi ConvertFromBase64([],UTF8) hello sonucunda ortaya çıkan hello DN özniteliği için kolay.</span><span class="sxs-lookup"><span data-stu-id="1f609-424">hello difference between this function and ConvertFromBase64([],UTF8) in that hello result is friendly for hello DN attribute.</span></span>  
<span data-ttu-id="1f609-425">Bu biçim DN Azure Active Directory tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1f609-425">This format is used by Azure Active Directory as DN.</span></span>

<span data-ttu-id="1f609-426">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="1f609-426">**Example:**</span></span>  
`ConvertFromUTF8Hex("48656C6C6F20776F726C6421")`  
<span data-ttu-id="1f609-427">Döndürür "*Merhaba Dünya!*"</span><span class="sxs-lookup"><span data-stu-id="1f609-427">Returns "*Hello world!*"</span></span>

- - -
### <a name="converttobase64"></a><span data-ttu-id="1f609-428">ConvertToBase64</span><span class="sxs-lookup"><span data-stu-id="1f609-428">ConvertToBase64</span></span>
<span data-ttu-id="1f609-429">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-429">**Description:**</span></span>  
<span data-ttu-id="1f609-430">Merhaba ConvertToBase64 işlev bir dize tooa Unicode base64 dizesi dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-430">hello ConvertToBase64 function converts a string tooa Unicode base64 string.</span></span>  
<span data-ttu-id="1f609-431">Base-64 basamak ile kodlanmış tamsayı tooits eşdeğer dize gösterimi dizisi Hello değerini dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-431">Converts hello value of an array of integers tooits equivalent string representation that is encoded with base-64 digits.</span></span>

<span data-ttu-id="1f609-432">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-432">**Syntax:**</span></span>  
`str ConvertToBase64(str source)`

<span data-ttu-id="1f609-433">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="1f609-433">**Example:**</span></span>  
`ConvertToBase64("Hello world!")`  
<span data-ttu-id="1f609-434">"SABlAGwAbABvACAAdwBvAHIAbABkACEA" döndürür</span><span class="sxs-lookup"><span data-stu-id="1f609-434">Returns "SABlAGwAbABvACAAdwBvAHIAbABkACEA"</span></span>

- - -
### <a name="converttoutf8hex"></a><span data-ttu-id="1f609-435">ConvertToUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="1f609-435">ConvertToUTF8Hex</span></span>
<span data-ttu-id="1f609-436">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-436">**Description:**</span></span>  
<span data-ttu-id="1f609-437">Merhaba ConvertToUTF8Hex işlev bir dize tooa UTF8 olarak kodlanmış onaltılık değer dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-437">hello ConvertToUTF8Hex function converts a string tooa UTF8 Hex encoded value.</span></span>

<span data-ttu-id="1f609-438">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-438">**Syntax:**</span></span>  
`str ConvertToUTF8Hex(str source)`

<span data-ttu-id="1f609-439">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="1f609-439">**Remarks:**</span></span>  
<span data-ttu-id="1f609-440">Bu işlevin Hello çıktı biçimi DN özniteliği biçimi olarak Azure Active Directory tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1f609-440">hello output format of this function is used by Azure Active Directory as DN attribute format.</span></span>

<span data-ttu-id="1f609-441">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="1f609-441">**Example:**</span></span>  
`ConvertToUTF8Hex("Hello world!")`  
<span data-ttu-id="1f609-442">Döndürür 48656C6C6F20776F726C6421</span><span class="sxs-lookup"><span data-stu-id="1f609-442">Returns 48656C6C6F20776F726C6421</span></span>

- - -
### <a name="count"></a><span data-ttu-id="1f609-443">Sayı</span><span class="sxs-lookup"><span data-stu-id="1f609-443">Count</span></span>
<span data-ttu-id="1f609-444">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-444">**Description:**</span></span>  
<span data-ttu-id="1f609-445">Merhaba Count işlevi, birden çok değerli bir öznitelikte hello sayıda öğeyi döndürür</span><span class="sxs-lookup"><span data-stu-id="1f609-445">hello Count function returns hello number of elements in a multi-valued attribute</span></span>

<span data-ttu-id="1f609-446">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-446">**Syntax:**</span></span>  
`num Count(mvstr attribute)`

- - -
### <a name="cnum"></a><span data-ttu-id="1f609-447">CNum</span><span class="sxs-lookup"><span data-stu-id="1f609-447">CNum</span></span>
<span data-ttu-id="1f609-448">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-448">**Description:**</span></span>  
<span data-ttu-id="1f609-449">Merhaba CNum işlev bir dize alır ve sayısal veri türü döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-449">hello CNum function takes a string and returns a numeric data type.</span></span>

<span data-ttu-id="1f609-450">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-450">**Syntax:**</span></span>  
`num CNum(str value)`

- - -
### <a name="cref"></a><span data-ttu-id="1f609-451">CRef</span><span class="sxs-lookup"><span data-stu-id="1f609-451">CRef</span></span>
<span data-ttu-id="1f609-452">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-452">**Description:**</span></span>  
<span data-ttu-id="1f609-453">Bir dize tooa başvuru özniteliği dönüştürür</span><span class="sxs-lookup"><span data-stu-id="1f609-453">Converts a string tooa reference attribute</span></span>

<span data-ttu-id="1f609-454">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-454">**Syntax:**</span></span>  
`ref CRef(str value)`

<span data-ttu-id="1f609-455">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="1f609-455">**Example:**</span></span>  
`CRef("CN=LC Services,CN=Microsoft,CN=lcspool01,CN=Pools,CN=RTC Service," & %Forest.LDAP%)`

- - -
### <a name="cstr"></a><span data-ttu-id="1f609-456">CStr</span><span class="sxs-lookup"><span data-stu-id="1f609-456">CStr</span></span>
<span data-ttu-id="1f609-457">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-457">**Description:**</span></span>  
<span data-ttu-id="1f609-458">CStr işlevi Hello tooa dize veri türü dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-458">hello CStr function converts tooa string data type.</span></span>

<span data-ttu-id="1f609-459">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-459">**Syntax:**</span></span>  
`str CStr(num value)`  
`str CStr(ref value)`  
`str CStr(bool value)`  

* <span data-ttu-id="1f609-460">değer: bir sayısal değer, başvuru özniteliği ya da Boole değeri olabilir.</span><span class="sxs-lookup"><span data-stu-id="1f609-460">value: Can be a numeric value, reference attribute, or Boolean.</span></span>

<span data-ttu-id="1f609-461">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="1f609-461">**Example:**</span></span>  
`CStr([dn])`  
<span data-ttu-id="1f609-462">Döndürebilirsiniz "cn = Can, dc = contoso, dc = com"</span><span class="sxs-lookup"><span data-stu-id="1f609-462">Could return "cn=Joe,dc=contoso,dc=com"</span></span>

- - -
### <a name="dateadd"></a><span data-ttu-id="1f609-463">DateAdd</span><span class="sxs-lookup"><span data-stu-id="1f609-463">DateAdd</span></span>
<span data-ttu-id="1f609-464">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-464">**Description:**</span></span>  
<span data-ttu-id="1f609-465">Belirli bir zaman aralığı eklenen tarih toowhich içeren bir tarih döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-465">Returns a Date containing a date toowhich a specified time interval has been added.</span></span>

<span data-ttu-id="1f609-466">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-466">**Syntax:**</span></span>  
`dt DateAdd(str interval, num value, dt date)`

* <span data-ttu-id="1f609-467">aralığı: dize hello aralığı tooadd istediğiniz süreyi ifade.</span><span class="sxs-lookup"><span data-stu-id="1f609-467">interval: String expression that is hello interval of time you want tooadd.</span></span> <span data-ttu-id="1f609-468">Merhaba dize değerlerini aşağıdaki hello birine sahip olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="1f609-468">hello string must have one of hello following values:</span></span>
  * <span data-ttu-id="1f609-469">yyyy yıl</span><span class="sxs-lookup"><span data-stu-id="1f609-469">yyyy Year</span></span>
  * <span data-ttu-id="1f609-470">q üç aylık dönem</span><span class="sxs-lookup"><span data-stu-id="1f609-470">q Quarter</span></span>
  * <span data-ttu-id="1f609-471">m ay</span><span class="sxs-lookup"><span data-stu-id="1f609-471">m Month</span></span>
  * <span data-ttu-id="1f609-472">yılın y günü</span><span class="sxs-lookup"><span data-stu-id="1f609-472">y Day of year</span></span>
  * <span data-ttu-id="1f609-473">d gün</span><span class="sxs-lookup"><span data-stu-id="1f609-473">d Day</span></span>
  * <span data-ttu-id="1f609-474">w haftanın günü</span><span class="sxs-lookup"><span data-stu-id="1f609-474">w Weekday</span></span>
  * <span data-ttu-id="1f609-475">ww hafta</span><span class="sxs-lookup"><span data-stu-id="1f609-475">ww Week</span></span>
  * <span data-ttu-id="1f609-476">h Saat</span><span class="sxs-lookup"><span data-stu-id="1f609-476">h Hour</span></span>
  * <span data-ttu-id="1f609-477">n dakika</span><span class="sxs-lookup"><span data-stu-id="1f609-477">n Minute</span></span>
  * <span data-ttu-id="1f609-478">s ikinci</span><span class="sxs-lookup"><span data-stu-id="1f609-478">s Second</span></span>
* <span data-ttu-id="1f609-479">değer: Merhaba sayı ölçü tooadd istiyor.</span><span class="sxs-lookup"><span data-stu-id="1f609-479">value: hello number of units you want tooadd.</span></span> <span data-ttu-id="1f609-480">Pozitif olabilir (Merhaba gelecekteki tooget tarihleri) veya negatif (Merhaba son tarihleri tooget).</span><span class="sxs-lookup"><span data-stu-id="1f609-480">It can be positive (tooget dates in hello future) or negative (tooget dates in hello past).</span></span>
* <span data-ttu-id="1f609-481">Tarih: DateTime temsil eden tarih toowhich hello aralığı eklenir.</span><span class="sxs-lookup"><span data-stu-id="1f609-481">date: DateTime representing date toowhich hello interval is added.</span></span>

<span data-ttu-id="1f609-482">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="1f609-482">**Example:**</span></span>  
`DateAdd("m", 3, CDate("2001-01-01"))`  
<span data-ttu-id="1f609-483">3 ay ekler ve "2001-04-01" temsil eden bir DateTime döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-483">Adds 3 months and returns a DateTime representing "2001-04-01".</span></span>

- - -
### <a name="datefromnum"></a><span data-ttu-id="1f609-484">DateFromNum</span><span class="sxs-lookup"><span data-stu-id="1f609-484">DateFromNum</span></span>
<span data-ttu-id="1f609-485">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-485">**Description:**</span></span>  
<span data-ttu-id="1f609-486">Merhaba DateFromNum işlevi Reklamın tarih biçimi tooa DateTime türü bir değere dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-486">hello DateFromNum function converts a value in AD’s date format tooa DateTime type.</span></span>

<span data-ttu-id="1f609-487">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-487">**Syntax:**</span></span>  
`dt DateFromNum(num value)`

<span data-ttu-id="1f609-488">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="1f609-488">**Example:**</span></span>  
`DateFromNum([lastLogonTimestamp])`  
`DateFromNum(129699324000000000)`  
<span data-ttu-id="1f609-489">2012-01-01 temsil eden bir DateTime döndürür 23:00:00</span><span class="sxs-lookup"><span data-stu-id="1f609-489">Returns a DateTime representing 2012-01-01 23:00:00</span></span>

- - -
### <a name="dncomponent"></a><span data-ttu-id="1f609-490">DNComponent</span><span class="sxs-lookup"><span data-stu-id="1f609-490">DNComponent</span></span>
<span data-ttu-id="1f609-491">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-491">**Description:**</span></span>  
<span data-ttu-id="1f609-492">Merhaba DNComponent işlevi soldan giderek belirtilen bir DN bileşen hello değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-492">hello DNComponent function returns hello value of a specified DN component going from left.</span></span>

<span data-ttu-id="1f609-493">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-493">**Syntax:**</span></span>  
`str DNComponent(ref dn, num ComponentNumber)`

* <span data-ttu-id="1f609-494">DN: hello başvuru özniteliği toointerpret</span><span class="sxs-lookup"><span data-stu-id="1f609-494">dn: hello reference attribute toointerpret</span></span>
* <span data-ttu-id="1f609-495">ComponentNumber: Merhaba DN tooreturn hello bileşeni</span><span class="sxs-lookup"><span data-stu-id="1f609-495">ComponentNumber: hello component in hello DN tooreturn</span></span>

<span data-ttu-id="1f609-496">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="1f609-496">**Example:**</span></span>  
`DNComponent([dn],1)`  
<span data-ttu-id="1f609-497">DN ise "CN = Joe, ou = =..." Can döndürür</span><span class="sxs-lookup"><span data-stu-id="1f609-497">If dn is "cn=Joe,ou=…," it returns Joe</span></span>

- - -
### <a name="dncomponentrev"></a><span data-ttu-id="1f609-498">DNComponentRev</span><span class="sxs-lookup"><span data-stu-id="1f609-498">DNComponentRev</span></span>
<span data-ttu-id="1f609-499">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-499">**Description:**</span></span>  
<span data-ttu-id="1f609-500">Merhaba DNComponentRev işlevi (Merhaba uç) sağdan giderek belirtilen bir DN bileşen hello değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-500">hello DNComponentRev function returns hello value of a specified DN component going from right (hello end).</span></span>

<span data-ttu-id="1f609-501">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-501">**Syntax:**</span></span>  
`str DNComponentRev(ref dn, num ComponentNumber)`  
`str DNComponentRev(ref dn, num ComponentNumber, enum Options)`

* <span data-ttu-id="1f609-502">DN: hello başvuru özniteliği toointerpret</span><span class="sxs-lookup"><span data-stu-id="1f609-502">dn: hello reference attribute toointerpret</span></span>
* <span data-ttu-id="1f609-503">ComponentNumber - hello DN tooreturn hello bileşeni</span><span class="sxs-lookup"><span data-stu-id="1f609-503">ComponentNumber - hello component in hello DN tooreturn</span></span>
* <span data-ttu-id="1f609-504">Seçenekler: DC – tüm bileşenleri Yoksay "dc ="</span><span class="sxs-lookup"><span data-stu-id="1f609-504">Options: DC – Ignore all components with "dc="</span></span>

<span data-ttu-id="1f609-505">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="1f609-505">**Example:**</span></span>  
<span data-ttu-id="1f609-506">DN ise "CN = Joe, ou = Atlanta, ou = GA, ou = = US, dc = contoso, dc = com" sonra</span><span class="sxs-lookup"><span data-stu-id="1f609-506">If dn is "cn=Joe,ou=Atlanta,ou=GA,ou=US, dc=contoso,dc=com" then</span></span>  
`DNComponentRev([dn],3)`  
`DNComponentRev([dn],1,"DC")`  
<span data-ttu-id="1f609-507">Her ikisi de BİZE döndür.</span><span class="sxs-lookup"><span data-stu-id="1f609-507">Both return US.</span></span>

- - -
### <a name="error"></a><span data-ttu-id="1f609-508">Hata</span><span class="sxs-lookup"><span data-stu-id="1f609-508">Error</span></span>
<span data-ttu-id="1f609-509">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-509">**Description:**</span></span>  
<span data-ttu-id="1f609-510">Merhaba hata işlevi kullanılan tooreturn özel bir hata var.</span><span class="sxs-lookup"><span data-stu-id="1f609-510">hello Error function is used tooreturn a custom error.</span></span>

<span data-ttu-id="1f609-511">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-511">**Syntax:**</span></span>  
`void Error(str ErrorMessage)`

<span data-ttu-id="1f609-512">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="1f609-512">**Example:**</span></span>  
`IIF(IsPresent([accountName]),[accountName],Error("AccountName is required"))`  
<span data-ttu-id="1f609-513">Merhaba özniteliği accountName mevcut değilse, bir hata hello nesnesinde atar.</span><span class="sxs-lookup"><span data-stu-id="1f609-513">If hello attribute accountName is not present, throw an error on hello object.</span></span>

- - -
### <a name="escapedncomponent"></a><span data-ttu-id="1f609-514">EscapeDNComponent</span><span class="sxs-lookup"><span data-stu-id="1f609-514">EscapeDNComponent</span></span>
<span data-ttu-id="1f609-515">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-515">**Description:**</span></span>  
<span data-ttu-id="1f609-516">Merhaba EscapeDNComponent işlevi bir DN biri bileşenini alır ve LDAP temsil edilebilir şekilde çıkışları.</span><span class="sxs-lookup"><span data-stu-id="1f609-516">hello EscapeDNComponent function takes one component of a DN and escapes it so it can be represented in LDAP.</span></span>

<span data-ttu-id="1f609-517">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-517">**Syntax:**</span></span>  
`str EscapeDNComponent(str value)`

<span data-ttu-id="1f609-518">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="1f609-518">**Example:**</span></span>  
`EscapeDNComponent("cn=" & [displayName]) & "," & %ForestLDAP%)`  
<span data-ttu-id="1f609-519">Merhaba displayName özniteliği LDAP'de kaçış karakterleri olsa bile, bir LDAP dizininde hello nesne oluşturulabilir emin olur.</span><span class="sxs-lookup"><span data-stu-id="1f609-519">Makes sure hello object can be created in an LDAP directory even if hello displayName attribute has characters that must be escaped in LDAP.</span></span>

- - -
### <a name="formatdatetime"></a><span data-ttu-id="1f609-520">FormatDateTime</span><span class="sxs-lookup"><span data-stu-id="1f609-520">FormatDateTime</span></span>
<span data-ttu-id="1f609-521">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-521">**Description:**</span></span>  
<span data-ttu-id="1f609-522">Hello FormatDateTime işlevi kullanılan tooformat DateTime tooa dizesi belirtilen biçime sahip değil</span><span class="sxs-lookup"><span data-stu-id="1f609-522">hello FormatDateTime function is used tooformat a DateTime tooa string with a specified format</span></span>

<span data-ttu-id="1f609-523">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-523">**Syntax:**</span></span>  
`str FormatDateTime(dt value, str format)`

* <span data-ttu-id="1f609-524">değer: hello tarih saat biçiminde bir değer</span><span class="sxs-lookup"><span data-stu-id="1f609-524">value: a value in hello DateTime format</span></span>
* <span data-ttu-id="1f609-525">Biçim: hello biçimi tooconvert temsil eden dize.</span><span class="sxs-lookup"><span data-stu-id="1f609-525">format: a string representing hello format tooconvert to.</span></span>

<span data-ttu-id="1f609-526">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="1f609-526">**Remarks:**</span></span>  
<span data-ttu-id="1f609-527">Merhaba olası değerler hello biçimi burada bulunabilir: [kullanıcı tanımlı tarih/saat biçimleri (biçim işlevi)](http://msdn2.microsoft.com/library/73ctwf33\(VS.90\).aspx)</span><span class="sxs-lookup"><span data-stu-id="1f609-527">hello possible values for hello format can be found here: [User-Defined Date/Time Formats (Format Function)](http://msdn2.microsoft.com/library/73ctwf33\(VS.90\).aspx)</span></span>

<span data-ttu-id="1f609-528">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="1f609-528">**Example:**</span></span>  

`FormatDateTime(CDate("12/25/2007"),"yyyy-mm-dd")`  
<span data-ttu-id="1f609-529">"2007-12-25" sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="1f609-529">Results in "2007-12-25".</span></span>

`FormatDateTime(DateFromNum([pwdLastSet]),"yyyyMMddHHmmss.0Z")`  
<span data-ttu-id="1f609-530">"İçinde 20140905081453.0Z" neden olabilir</span><span class="sxs-lookup"><span data-stu-id="1f609-530">Can result in "20140905081453.0Z"</span></span>

- - -
### <a name="guid"></a><span data-ttu-id="1f609-531">GUID</span><span class="sxs-lookup"><span data-stu-id="1f609-531">GUID</span></span>
<span data-ttu-id="1f609-532">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-532">**Description:**</span></span>  
<span data-ttu-id="1f609-533">Yeni bir rastgele GUID Hello işlevi GUID oluşturur</span><span class="sxs-lookup"><span data-stu-id="1f609-533">hello function GUID generates a new random GUID</span></span>

<span data-ttu-id="1f609-534">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-534">**Syntax:**</span></span>  
`str GUID()`

- - -
### <a name="iif"></a><span data-ttu-id="1f609-535">IIF</span><span class="sxs-lookup"><span data-stu-id="1f609-535">IIF</span></span>
<span data-ttu-id="1f609-536">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-536">**Description:**</span></span>  
<span data-ttu-id="1f609-537">Merhaba IIF işlevi belirtilen bir koşula göre olası değerlerin kümesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-537">hello IIF function returns one of a set of possible values based on a specified condition.</span></span>

<span data-ttu-id="1f609-538">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-538">**Syntax:**</span></span>  
`var IIF(exp condition, var valueIfTrue, var valueIfFalse)`

* <span data-ttu-id="1f609-539">koşul: herhangi bir değer veya olabilir ifade hesaplanan tootrue ya da yanlış.</span><span class="sxs-lookup"><span data-stu-id="1f609-539">condition: any value or expression that can be evaluated tootrue or false.</span></span>
* <span data-ttu-id="1f609-540">Koşul: hello koşul tootrue değerlendirilirse hello değer döndürdü.</span><span class="sxs-lookup"><span data-stu-id="1f609-540">valueIfTrue: If hello condition evaluates tootrue, hello returned value.</span></span>
* <span data-ttu-id="1f609-541">valueIfFalse: hello koşul toofalse değerlendirilirse hello değer döndürdü.</span><span class="sxs-lookup"><span data-stu-id="1f609-541">valueIfFalse: If hello condition evaluates toofalse, hello returned value.</span></span>

<span data-ttu-id="1f609-542">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="1f609-542">**Example:**</span></span>  
`IIF([employeeType]="Intern","t-" & [alias],[alias])`  
 <span data-ttu-id="1f609-543">Merhaba kullanıcı bir stajyer ise, bir kullanıcı ile "t-" Merhaba diğer adı olarak hello kullanıcının diğer adı, başka toohello başlangıcını döndürür eklenen döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-543">If hello user is an intern, returns hello alias of a user with "t-" added toohello beginning of it, else returns hello user’s alias as is.</span></span>

- - -
### <a name="instr"></a><span data-ttu-id="1f609-544">InStr</span><span class="sxs-lookup"><span data-stu-id="1f609-544">InStr</span></span>
<span data-ttu-id="1f609-545">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-545">**Description:**</span></span>  
<span data-ttu-id="1f609-546">Merhaba InStr işlevi bir alt dizenin ilk örneğinin hello dizede bulur.</span><span class="sxs-lookup"><span data-stu-id="1f609-546">hello InStr function finds hello first occurrence of a substring in a string</span></span>

<span data-ttu-id="1f609-547">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-547">**Syntax:**</span></span>  

`num InStr(str stringcheck, str stringmatch)`  
`num InStr(str stringcheck, str stringmatch, num start)`  
`num InStr(str stringcheck, str stringmatch, num start , enum compare)`

* <span data-ttu-id="1f609-548">stringcheck: arama toobe dize</span><span class="sxs-lookup"><span data-stu-id="1f609-548">stringcheck: string toobe searched</span></span>
* <span data-ttu-id="1f609-549">stringmatch: bulunan toobe dize</span><span class="sxs-lookup"><span data-stu-id="1f609-549">stringmatch: string toobe found</span></span>
* <span data-ttu-id="1f609-550">Başlat: konum toofind hello substring başlatılıyor</span><span class="sxs-lookup"><span data-stu-id="1f609-550">start: starting position toofind hello substring</span></span>
* <span data-ttu-id="1f609-551">karşılaştırma: vbTextCompare veya vbBinaryCompare</span><span class="sxs-lookup"><span data-stu-id="1f609-551">compare: vbTextCompare or vbBinaryCompare</span></span>

<span data-ttu-id="1f609-552">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="1f609-552">**Remarks:**</span></span>  
<span data-ttu-id="1f609-553">Merhaba substring bulunduğu döndürür hello konum veya 0 ise bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="1f609-553">Returns hello position where hello substring was found or 0 if not found.</span></span>

<span data-ttu-id="1f609-554">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="1f609-554">**Example:**</span></span>  
`InStr("hello quick brown fox","quick")`  
<span data-ttu-id="1f609-555">Evalues too5</span><span class="sxs-lookup"><span data-stu-id="1f609-555">Evalues too5</span></span>

`InStr("repEated","e",3,vbBinaryCompare)`  
<span data-ttu-id="1f609-556">Too7 hesaplar</span><span class="sxs-lookup"><span data-stu-id="1f609-556">Evaluates too7</span></span>

- - -
### <a name="instrrev"></a><span data-ttu-id="1f609-557">InStrRev</span><span class="sxs-lookup"><span data-stu-id="1f609-557">InStrRev</span></span>
<span data-ttu-id="1f609-558">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-558">**Description:**</span></span>  
<span data-ttu-id="1f609-559">Merhaba InStrRev işlevi dizesi içinde son a geçişi hello bir alt dizenin bulur</span><span class="sxs-lookup"><span data-stu-id="1f609-559">hello InStrRev function finds hello last occurrence of a substring in a string</span></span>

<span data-ttu-id="1f609-560">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-560">**Syntax:**</span></span>  
`num InstrRev(str stringcheck, str stringmatch)`  
`num InstrRev(str stringcheck, str stringmatch, num start)`  
`num InstrRev(str stringcheck, str stringmatch, num start, enum compare)`

* <span data-ttu-id="1f609-561">stringcheck: arama toobe dize</span><span class="sxs-lookup"><span data-stu-id="1f609-561">stringcheck: string toobe searched</span></span>
* <span data-ttu-id="1f609-562">stringmatch: bulunan toobe dize</span><span class="sxs-lookup"><span data-stu-id="1f609-562">stringmatch: string toobe found</span></span>
* <span data-ttu-id="1f609-563">Başlat: konum toofind hello substring başlatılıyor</span><span class="sxs-lookup"><span data-stu-id="1f609-563">start: starting position toofind hello substring</span></span>
* <span data-ttu-id="1f609-564">karşılaştırma: vbTextCompare veya vbBinaryCompare</span><span class="sxs-lookup"><span data-stu-id="1f609-564">compare: vbTextCompare or vbBinaryCompare</span></span>

<span data-ttu-id="1f609-565">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="1f609-565">**Remarks:**</span></span>  
<span data-ttu-id="1f609-566">Merhaba substring bulunduğu döndürür hello konum veya 0 ise bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="1f609-566">Returns hello position where hello substring was found or 0 if not found.</span></span>

<span data-ttu-id="1f609-567">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="1f609-567">**Example:**</span></span>  
`InStrRev("abbcdbbbef","bb")`  
<span data-ttu-id="1f609-568">7 döndürür</span><span class="sxs-lookup"><span data-stu-id="1f609-568">Returns 7</span></span>

- - -
### <a name="isbitset"></a><span data-ttu-id="1f609-569">IsBitSet</span><span class="sxs-lookup"><span data-stu-id="1f609-569">IsBitSet</span></span>
<span data-ttu-id="1f609-570">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-570">**Description:**</span></span>  
<span data-ttu-id="1f609-571">Merhaba işlevi IsBitSet veya bir bit ayarlanmışsa, testleri</span><span class="sxs-lookup"><span data-stu-id="1f609-571">hello function IsBitSet Tests if a bit is set or not</span></span>

<span data-ttu-id="1f609-572">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-572">**Syntax:**</span></span>  
`bool IsBitSet(num value, num flag)`

* <span data-ttu-id="1f609-573">değer: evaluated.flag bir sayısal değer: hello olan sayısal bir değer bit hesaplanan toobe</span><span class="sxs-lookup"><span data-stu-id="1f609-573">value: a numeric value that is evaluated.flag: a numeric value that has hello bit toobe evaluated</span></span>

<span data-ttu-id="1f609-574">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="1f609-574">**Example:**</span></span>  
`IsBitSet(&HF,4)`  
<span data-ttu-id="1f609-575">Bit "4" Merhaba on altılık değeri "F" olarak ayarlandığından True değerini döndürür</span><span class="sxs-lookup"><span data-stu-id="1f609-575">Returns True because bit "4" is set in hello hexadecimal value "F"</span></span>

- - -
### <a name="isdate"></a><span data-ttu-id="1f609-576">IsDate</span><span class="sxs-lookup"><span data-stu-id="1f609-576">IsDate</span></span>
<span data-ttu-id="1f609-577">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-577">**Description:**</span></span>  
<span data-ttu-id="1f609-578">Merhaba ifade olabiliyorsa tooTrue hello IsDate işlevi değerlendirir sonra bir DateTime türü değerlendirir.</span><span class="sxs-lookup"><span data-stu-id="1f609-578">If hello expression can be evaluates as a DateTime type, then hello IsDate function evaluates tooTrue.</span></span>

<span data-ttu-id="1f609-579">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-579">**Syntax:**</span></span>  
`bool IsDate(var Expression)`

<span data-ttu-id="1f609-580">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="1f609-580">**Remarks:**</span></span>  
<span data-ttu-id="1f609-581">CDate() başarılı olması durumunda toodetermine kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1f609-581">Used toodetermine if CDate() can be successful.</span></span>

- - -
### <a name="iscert"></a><span data-ttu-id="1f609-582">IsCert</span><span class="sxs-lookup"><span data-stu-id="1f609-582">IsCert</span></span>
<span data-ttu-id="1f609-583">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-583">**Description:**</span></span>  
<span data-ttu-id="1f609-584">.NET X509Certificate2 sertifika nesnesine Hello ham verileri seri hale getirilebilir true değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-584">Returns true if hello raw data can be serialized into .NET X509Certificate2 certificate object.</span></span>

<span data-ttu-id="1f609-585">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-585">**Syntax:**</span></span>  
`bool CertThumbprint(binary certificateRawData)`  
*   <span data-ttu-id="1f609-586">certificateRawData: Bayt dizisine bir X.509 sertifikası gösterimi.</span><span class="sxs-lookup"><span data-stu-id="1f609-586">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="1f609-587">Merhaba bayt dizisi olarak kodlanmış ikili (DER) veya Base64 ile kodlanmış X.509 veri olabilir.</span><span class="sxs-lookup"><span data-stu-id="1f609-587">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>
- - -
### <a name="isempty"></a><span data-ttu-id="1f609-588">IsEmpty</span><span class="sxs-lookup"><span data-stu-id="1f609-588">IsEmpty</span></span>
<span data-ttu-id="1f609-589">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-589">**Description:**</span></span>  
<span data-ttu-id="1f609-590">Merhaba özniteliği hello CS veya MV var, ancak tooan boş dize olarak değerlendirilir, hello IsEmpty işlevi tooTrue değerlendirir.</span><span class="sxs-lookup"><span data-stu-id="1f609-590">If hello attribute is present in hello CS or MV but evaluates tooan empty string, then hello IsEmpty function evaluates tooTrue.</span></span>

<span data-ttu-id="1f609-591">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-591">**Syntax:**</span></span>  
`bool IsEmpty(var Expression)`

- - -
### <a name="isguid"></a><span data-ttu-id="1f609-592">IsGuid</span><span class="sxs-lookup"><span data-stu-id="1f609-592">IsGuid</span></span>
<span data-ttu-id="1f609-593">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-593">**Description:**</span></span>  
<span data-ttu-id="1f609-594">Merhaba dize dönüştürülmüş tooa GUID edilebiliyorsa Merhaba IsGuid işlevi tootrue değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="1f609-594">If hello string could be converted tooa GUID, then hello IsGuid function evaluated tootrue.</span></span>

<span data-ttu-id="1f609-595">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-595">**Syntax:**</span></span>  
`bool IsGuid(str GUID)`

<span data-ttu-id="1f609-596">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="1f609-596">**Remarks:**</span></span>  
<span data-ttu-id="1f609-597">Bir GUID bu desenleri birini izleyen bir dize olarak tanımlanır: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx veya {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span><span class="sxs-lookup"><span data-stu-id="1f609-597">A GUID is defined as a string following one of these patterns: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx or {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span></span>

<span data-ttu-id="1f609-598">CGuid() başarılı olması durumunda toodetermine kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1f609-598">Used toodetermine if CGuid() can be successful.</span></span>

<span data-ttu-id="1f609-599">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="1f609-599">**Example:**</span></span>  
`IIF(IsGuid([strAttribute]),CGuid([strAttribute]),NULL)`  
<span data-ttu-id="1f609-600">Merhaba StrAttribute GUID biçimine varsa, bir ikili biçimi döndürür, aksi takdirde null değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-600">If hello StrAttribute has a GUID format, return a binary representation, otherwise return a Null.</span></span>

- - -
### <a name="isnull"></a><span data-ttu-id="1f609-601">IsNull</span><span class="sxs-lookup"><span data-stu-id="1f609-601">IsNull</span></span>
<span data-ttu-id="1f609-602">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-602">**Description:**</span></span>  
<span data-ttu-id="1f609-603">TooNull Hello ifadeyi hesaplar, hello IsNull işlevi true döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-603">If hello expression evaluates tooNull, then hello IsNull function returns true.</span></span>

<span data-ttu-id="1f609-604">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-604">**Syntax:**</span></span>  
`bool IsNull(var Expression)`

<span data-ttu-id="1f609-605">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="1f609-605">**Remarks:**</span></span>  
<span data-ttu-id="1f609-606">Bir öznitelik için bir Null hello özniteliği hello yokluğu tarafından ifade edilir.</span><span class="sxs-lookup"><span data-stu-id="1f609-606">For an attribute, a Null is expressed by hello absence of hello attribute.</span></span>

<span data-ttu-id="1f609-607">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="1f609-607">**Example:**</span></span>  
`IsNull([displayName])`  
<span data-ttu-id="1f609-608">Merhaba özniteliği hello CS veya MV mevcut değilse True değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-608">Returns True if hello attribute is not present in hello CS or MV.</span></span>

- - -
### <a name="isnullorempty"></a><span data-ttu-id="1f609-609">IsNullOrEmpty</span><span class="sxs-lookup"><span data-stu-id="1f609-609">IsNullOrEmpty</span></span>
<span data-ttu-id="1f609-610">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-610">**Description:**</span></span>  
<span data-ttu-id="1f609-611">Hello ifade null veya boş bir dize ise, hello IsNullOrEmpty işlevi true döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-611">If hello expression is null or an empty string, then hello IsNullOrEmpty function returns true.</span></span>

<span data-ttu-id="1f609-612">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-612">**Syntax:**</span></span>  
`bool IsNullOrEmpty(var Expression)`

<span data-ttu-id="1f609-613">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="1f609-613">**Remarks:**</span></span>  
<span data-ttu-id="1f609-614">Hello özniteliği yok veya var ancak boş bir dize için bir öznitelik, bu tooTrue değerlendirmek.</span><span class="sxs-lookup"><span data-stu-id="1f609-614">For an attribute, this would evaluate tooTrue if hello attribute is absent or is present but is an empty string.</span></span>  
<span data-ttu-id="1f609-615">Bu işlev Hello tersini olmasına adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="1f609-615">hello inverse of this function is named IsPresent.</span></span>

<span data-ttu-id="1f609-616">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="1f609-616">**Example:**</span></span>  
`IsNullOrEmpty([displayName])`  
<span data-ttu-id="1f609-617">Merhaba özniteliği mevcut değil ya da boş bir dize hello CS veya MV varsa True değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-617">Returns True if hello attribute is not present or is an empty string in hello CS or MV.</span></span>

- - -
### <a name="isnumeric"></a><span data-ttu-id="1f609-618">IsNumeric</span><span class="sxs-lookup"><span data-stu-id="1f609-618">IsNumeric</span></span>
<span data-ttu-id="1f609-619">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-619">**Description:**</span></span>  
<span data-ttu-id="1f609-620">Merhaba IsNumeric işlevi bir ifadenin sayı türü değerlendirilebilir olup olmadığını gösteren bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-620">hello IsNumeric function returns a Boolean value indicating whether an expression can be evaluated as a number type.</span></span>

<span data-ttu-id="1f609-621">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-621">**Syntax:**</span></span>  
`bool IsNumeric(var Expression)`

<span data-ttu-id="1f609-622">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="1f609-622">**Remarks:**</span></span>  
<span data-ttu-id="1f609-623">CNum() başarılı tooparse hello ifade olabiliyorsa toodetermine kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1f609-623">Used toodetermine if CNum() can be successful tooparse hello expression.</span></span>

- - -
### <a name="isstring"></a><span data-ttu-id="1f609-624">IsString</span><span class="sxs-lookup"><span data-stu-id="1f609-624">IsString</span></span>
<span data-ttu-id="1f609-625">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-625">**Description:**</span></span>  
<span data-ttu-id="1f609-626">Merhaba ifade yapabiliyorsanız olması değerlendirilen tooa dize türünde, tooTrue hello IsString işlevi değerlendirir sonra.</span><span class="sxs-lookup"><span data-stu-id="1f609-626">If hello expression can be evaluated tooa string type, then hello IsString function evaluates tooTrue.</span></span>

<span data-ttu-id="1f609-627">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-627">**Syntax:**</span></span>  
`bool IsString(var expression)`

<span data-ttu-id="1f609-628">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="1f609-628">**Remarks:**</span></span>  
<span data-ttu-id="1f609-629">CStr() başarılı tooparse hello ifade olabiliyorsa toodetermine kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1f609-629">Used toodetermine if CStr() can be successful tooparse hello expression.</span></span>

- - -
### <a name="ispresent"></a><span data-ttu-id="1f609-630">Olmasına</span><span class="sxs-lookup"><span data-stu-id="1f609-630">IsPresent</span></span>
<span data-ttu-id="1f609-631">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-631">**Description:**</span></span>  
<span data-ttu-id="1f609-632">Null olmayan ve boş değil tooa dize Hello ifadeyi hesaplar, işlevi true değerini döndürür olmasına hello.</span><span class="sxs-lookup"><span data-stu-id="1f609-632">If hello expression evaluates tooa string that is not Null and is not empty, then hello IsPresent function returns true.</span></span>

<span data-ttu-id="1f609-633">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-633">**Syntax:**</span></span>  
`bool IsPresent(var expression)`

<span data-ttu-id="1f609-634">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="1f609-634">**Remarks:**</span></span>  
<span data-ttu-id="1f609-635">Bu işlev Hello tersini IsNullOrEmpty olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="1f609-635">hello inverse of this function is named IsNullOrEmpty.</span></span>

<span data-ttu-id="1f609-636">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="1f609-636">**Example:**</span></span>  
`Switch(IsPresent([directManager]),[directManager], IsPresent([skiplevelManager]),[skiplevelManager], IsPresent([director]),[director])`

- - -
### <a name="item"></a><span data-ttu-id="1f609-637">Öğe</span><span class="sxs-lookup"><span data-stu-id="1f609-637">Item</span></span>
<span data-ttu-id="1f609-638">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-638">**Description:**</span></span>  
<span data-ttu-id="1f609-639">Merhaba öğesi işlevi, birden çok değerli bir dize/özniteliğinden bir öğeyi döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-639">hello Item function returns one item from a multi-valued string/attribute.</span></span>

<span data-ttu-id="1f609-640">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-640">**Syntax:**</span></span>  
`var Item(mvstr attribute, num index)`

* <span data-ttu-id="1f609-641">Öznitelik: birden çok değerli özniteliği</span><span class="sxs-lookup"><span data-stu-id="1f609-641">attribute: multi-valued attribute</span></span>
* <span data-ttu-id="1f609-642">Dizin: dizin tooan öğesinde hello birden çok değerli dize.</span><span class="sxs-lookup"><span data-stu-id="1f609-642">index: index tooan item in hello multi-valued string.</span></span>

<span data-ttu-id="1f609-643">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="1f609-643">**Remarks:**</span></span>  
<span data-ttu-id="1f609-644">Merhaba ikinci işlevi hello birden çok değerli özniteliğinde hello dizin tooan öğesi döndürdüğünden hello öğesi işlevi içerir işlevi hello birlikte yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="1f609-644">hello Item function is useful together with hello Contains function since hello latter function returns hello index tooan item in hello multi-valued attribute.</span></span>

<span data-ttu-id="1f609-645">Dizin sınırların dışında olması durumunda bir hata oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1f609-645">Throws an error if index is out of bounds.</span></span>

<span data-ttu-id="1f609-646">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="1f609-646">**Example:**</span></span>  
`Mid(Item([proxyAddress],Contains([proxyAddress], "SMTP:")),6)`  
<span data-ttu-id="1f609-647">Birincil e-posta adresi döndürür hello.</span><span class="sxs-lookup"><span data-stu-id="1f609-647">Returns hello primary email address.</span></span>

- - -
### <a name="itemornull"></a><span data-ttu-id="1f609-648">ItemOrNull</span><span class="sxs-lookup"><span data-stu-id="1f609-648">ItemOrNull</span></span>
<span data-ttu-id="1f609-649">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-649">**Description:**</span></span>  
<span data-ttu-id="1f609-650">Merhaba ItemOrNull işlevi, birden çok değerli bir dize/özniteliğinden bir öğeyi döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-650">hello ItemOrNull function returns one item from a multi-valued string/attribute.</span></span>

<span data-ttu-id="1f609-651">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-651">**Syntax:**</span></span>  
`var ItemOrNull(mvstr attribute, num index)`

* <span data-ttu-id="1f609-652">Öznitelik: birden çok değerli özniteliği</span><span class="sxs-lookup"><span data-stu-id="1f609-652">attribute: multi-valued attribute</span></span>
* <span data-ttu-id="1f609-653">Dizin: dizin tooan öğesinde hello birden çok değerli dize.</span><span class="sxs-lookup"><span data-stu-id="1f609-653">index: index tooan item in hello multi-valued string.</span></span>

<span data-ttu-id="1f609-654">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="1f609-654">**Remarks:**</span></span>  
<span data-ttu-id="1f609-655">Merhaba ikinci işlevi hello birden çok değerli özniteliğinde hello dizin tooan öğesi döndürdüğünden hello ItemOrNull işlevi içerir işlevi hello birlikte yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="1f609-655">hello ItemOrNull function is useful together with hello Contains function since hello latter function returns hello index tooan item in hello multi-valued attribute.</span></span>

<span data-ttu-id="1f609-656">Dizin sınırların dışında ise, bir Null değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-656">If index is out of bounds, then returns a Null value.</span></span>

- - -
### <a name="join"></a><span data-ttu-id="1f609-657">Birleştir</span><span class="sxs-lookup"><span data-stu-id="1f609-657">Join</span></span>
<span data-ttu-id="1f609-658">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-658">**Description:**</span></span>  
<span data-ttu-id="1f609-659">Merhaba birleştirme işlevi birden çok değerli bir dize alır ve her bir öğe eklenen belirtilen ayırıcı ile tek değerli bir dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-659">hello Join function takes a multi-valued string and returns a single-valued string with specified separator inserted between each item.</span></span>

<span data-ttu-id="1f609-660">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-660">**Syntax:**</span></span>  
`str Join(mvstr attribute)`  
`str Join(mvstr attribute, str Delimiter)`

* <span data-ttu-id="1f609-661">Öznitelik: birden çok değerli özniteliği içeren dizeleri birleştirilmiş toobe.</span><span class="sxs-lookup"><span data-stu-id="1f609-661">attribute: Multi-valued attribute containing strings toobe joined.</span></span>
* <span data-ttu-id="1f609-662">sınırlayıcı: herhangi bir dize, dize döndürdü hello içinde kullanılan tooseparate hello alt dizeler.</span><span class="sxs-lookup"><span data-stu-id="1f609-662">delimiter: Any string, used tooseparate hello substrings in hello returned string.</span></span> <span data-ttu-id="1f609-663">Atlanırsa, boşluk karakteri hello ("") kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1f609-663">If omitted, hello space character (" ") is used.</span></span> <span data-ttu-id="1f609-664">Sınırlayıcı sıfır uzunlukta bir dize ise ("") veya hiçbir şey hello listedeki tüm öğelerin hiçbir sınırlayıcıları ile birleşir.</span><span class="sxs-lookup"><span data-stu-id="1f609-664">If Delimiter is a zero-length string ("") or Nothing, all items in hello list are concatenated with no delimiters.</span></span>

<span data-ttu-id="1f609-665">**Açıklamalar**</span><span class="sxs-lookup"><span data-stu-id="1f609-665">**Remarks**</span></span>  
<span data-ttu-id="1f609-666">Merhaba birleştirme ve bölme işlevleri arasında eşlik bulunur.</span><span class="sxs-lookup"><span data-stu-id="1f609-666">There is parity between hello Join and Split functions.</span></span> <span data-ttu-id="1f609-667">Merhaba birleştirme işlevi bir dizeler dizisi alır ve bunları tooreturn tek bir dize sınırlayıcı bir dize kullanarak birleştirir.</span><span class="sxs-lookup"><span data-stu-id="1f609-667">hello Join function takes an array of strings and joins them using a delimiter string, tooreturn a single string.</span></span> <span data-ttu-id="1f609-668">Merhaba bölünmüş işlev bir dize alır ve tooreturn bir dizeler dizisi hello sınırlayıcı ayırır.</span><span class="sxs-lookup"><span data-stu-id="1f609-668">hello Split function takes a string and separates it at hello delimiter, tooreturn an array of strings.</span></span> <span data-ttu-id="1f609-669">Ancak, bir anahtar farktır birleştirme sınırlayıcı dizesiyle dizeyi birleştirmek, bölme yalnızca bir tek karakter ayırıcısı kullanarak dizeleri ayırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1f609-669">However, a key difference is that Join can concatenate strings with any delimiter string, Split can only separate strings using a single character delimiter.</span></span>

<span data-ttu-id="1f609-670">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="1f609-670">**Example:**</span></span>  
`Join([proxyAddresses],",")`  
<span data-ttu-id="1f609-671">Döndürebilirsiniz: "SMTP:john.doe@contoso.com,smtp:jd@contoso.com"</span><span class="sxs-lookup"><span data-stu-id="1f609-671">Could return: "SMTP:john.doe@contoso.com,smtp:jd@contoso.com"</span></span>

- - -
### <a name="lcase"></a><span data-ttu-id="1f609-672">LCase</span><span class="sxs-lookup"><span data-stu-id="1f609-672">LCase</span></span>
<span data-ttu-id="1f609-673">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-673">**Description:**</span></span>  
<span data-ttu-id="1f609-674">Merhaba LCase işlev bir dize toolower durumda tüm karakterleri dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-674">hello LCase function converts all characters in a string toolower case.</span></span>

<span data-ttu-id="1f609-675">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-675">**Syntax:**</span></span>  
`str LCase(str value)`

<span data-ttu-id="1f609-676">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="1f609-676">**Example:**</span></span>  
`LCase("TeSt")`  
<span data-ttu-id="1f609-677">"Test" döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-677">Returns "test".</span></span>

- - -
### <a name="left"></a><span data-ttu-id="1f609-678">Sol</span><span class="sxs-lookup"><span data-stu-id="1f609-678">Left</span></span>
<span data-ttu-id="1f609-679">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-679">**Description:**</span></span>  
<span data-ttu-id="1f609-680">Merhaba sol işlevi bir dize hello soldan belirtilen sayıda karakteri döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-680">hello Left function returns a specified number of characters from hello left of a string.</span></span>

<span data-ttu-id="1f609-681">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-681">**Syntax:**</span></span>  
`str Left(str string, num NumChars)`

* <span data-ttu-id="1f609-682">dize: Merhaba dize tooreturn karakterler</span><span class="sxs-lookup"><span data-stu-id="1f609-682">string: hello string tooreturn characters from</span></span>
* <span data-ttu-id="1f609-683">NumChars: başından (sol) hello dizenin karakter tooreturn hello sayısı tanımlayan bir numara</span><span class="sxs-lookup"><span data-stu-id="1f609-683">NumChars: a number identifying hello number of characters tooreturn from hello beginning (left) of string</span></span>

<span data-ttu-id="1f609-684">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="1f609-684">**Remarks:**</span></span>  
<span data-ttu-id="1f609-685">Dizedeki Hello ilk numChars karakter içeren bir dize:</span><span class="sxs-lookup"><span data-stu-id="1f609-685">A string containing hello first numChars characters in string:</span></span>

* <span data-ttu-id="1f609-686">Varsa numChars = 0, boş bir dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-686">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="1f609-687">NumChars < 0, döndürmesi durumunda giriş dizesi.</span><span class="sxs-lookup"><span data-stu-id="1f609-687">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="1f609-688">Dize null ise, boş bir dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-688">If string is null, return empty string.</span></span>

<span data-ttu-id="1f609-689">Dize numChars içinde belirtilen hello sayıdan daha az karakter içeriyorsa, (yani parametre 1'deki tüm karakterleri içeren) bir dize aynı toostring döndürülür.</span><span class="sxs-lookup"><span data-stu-id="1f609-689">If string contains fewer characters than hello number specified in numChars, a string identical toostring (that is, containing all characters in parameter 1) is returned.</span></span>

<span data-ttu-id="1f609-690">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="1f609-690">**Example:**</span></span>  
`Left("John Doe", 3)`  
<span data-ttu-id="1f609-691">"Joh" döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-691">Returns "Joh".</span></span>

- - -
### <a name="len"></a><span data-ttu-id="1f609-692">Len</span><span class="sxs-lookup"><span data-stu-id="1f609-692">Len</span></span>
<span data-ttu-id="1f609-693">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-693">**Description:**</span></span>  
<span data-ttu-id="1f609-694">Merhaba Len işlevi bir dizedeki karakter sayısını döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-694">hello Len function returns number of characters in a string.</span></span>

<span data-ttu-id="1f609-695">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-695">**Syntax:**</span></span>  
`num Len(str value)`

<span data-ttu-id="1f609-696">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="1f609-696">**Example:**</span></span>  
`Len("John Doe")`  
<span data-ttu-id="1f609-697">8 döndürür</span><span class="sxs-lookup"><span data-stu-id="1f609-697">Returns 8</span></span>

- - -
### <a name="ltrim"></a><span data-ttu-id="1f609-698">LTrim</span><span class="sxs-lookup"><span data-stu-id="1f609-698">LTrim</span></span>
<span data-ttu-id="1f609-699">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-699">**Description:**</span></span>  
<span data-ttu-id="1f609-700">Merhaba LTrim işlevi bir dizeden öndeki boşlukları kaldırır.</span><span class="sxs-lookup"><span data-stu-id="1f609-700">hello LTrim function removes leading white spaces from a string.</span></span>

<span data-ttu-id="1f609-701">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-701">**Syntax:**</span></span>  
`str LTrim(str value)`

<span data-ttu-id="1f609-702">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="1f609-702">**Example:**</span></span>  
`LTrim(" Test ")`  
<span data-ttu-id="1f609-703">"Test" döndürür</span><span class="sxs-lookup"><span data-stu-id="1f609-703">Returns "Test "</span></span>

- - -
### <a name="mid"></a><span data-ttu-id="1f609-704">Orta</span><span class="sxs-lookup"><span data-stu-id="1f609-704">Mid</span></span>
<span data-ttu-id="1f609-705">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-705">**Description:**</span></span>  
<span data-ttu-id="1f609-706">Mid Merhaba işlevi bir dizedeki belirtilen konumdan belirtilen sayıda karakteri döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-706">hello Mid function returns a specified number of characters from a specified position in a string.</span></span>

<span data-ttu-id="1f609-707">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-707">**Syntax:**</span></span>  
`str Mid(str string, num start, num NumChars)`

* <span data-ttu-id="1f609-708">dize: Merhaba dize tooreturn karakterler</span><span class="sxs-lookup"><span data-stu-id="1f609-708">string: hello string tooreturn characters from</span></span>
* <span data-ttu-id="1f609-709">Başlat: dize tooreturn karakterlerinden konumda başlangıç hello tanımlayan bir numara</span><span class="sxs-lookup"><span data-stu-id="1f609-709">start: a number identifying hello starting position in string tooreturn characters from</span></span>
* <span data-ttu-id="1f609-710">NumChars: dizesinde konumundan karakterleri tooreturn hello sayısı tanımlayan bir numara</span><span class="sxs-lookup"><span data-stu-id="1f609-710">NumChars: a number identifying hello number of characters tooreturn from position in string</span></span>

<span data-ttu-id="1f609-711">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="1f609-711">**Remarks:**</span></span>  
<span data-ttu-id="1f609-712">Konumundan başlayan dönüş numChars karakter dizesi içinde başlatın.</span><span class="sxs-lookup"><span data-stu-id="1f609-712">Return numChars characters starting from position start in string.</span></span>  
<span data-ttu-id="1f609-713">Konumu başlangıç dizesinde numChars karakterler içeren bir dize:</span><span class="sxs-lookup"><span data-stu-id="1f609-713">A string containing numChars characters from position start in string:</span></span>

* <span data-ttu-id="1f609-714">Varsa numChars = 0, boş bir dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-714">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="1f609-715">NumChars < 0, döndürmesi durumunda giriş dizesi.</span><span class="sxs-lookup"><span data-stu-id="1f609-715">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="1f609-716">Başlat > merhaba dize uzunluğu, giriş dizesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-716">If start > hello length of string, return input string.</span></span>
* <span data-ttu-id="1f609-717">Varsa Başlat < = 0, giriş dizesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-717">If start <= 0, return input string.</span></span>
* <span data-ttu-id="1f609-718">Dize null ise, boş bir dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-718">If string is null, return empty string.</span></span>

<span data-ttu-id="1f609-719">NumChar karakter değilse kadar çok konumu başından dizesinde kalan karakterler mümkün olduğunca döndürülür.</span><span class="sxs-lookup"><span data-stu-id="1f609-719">If there are not numChar characters remaining in string from position start, as many characters as possible are returned.</span></span>

<span data-ttu-id="1f609-720">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="1f609-720">**Example:**</span></span>  
`Mid("John Doe", 3, 5)`  
<span data-ttu-id="1f609-721">"Hn" döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-721">Returns "hn Do".</span></span>

`Mid("John Doe", 6, 999)`  
<span data-ttu-id="1f609-722">"Doe" döndürür</span><span class="sxs-lookup"><span data-stu-id="1f609-722">Returns "Doe"</span></span>

- - -
### <a name="now"></a><span data-ttu-id="1f609-723">Şimdi</span><span class="sxs-lookup"><span data-stu-id="1f609-723">Now</span></span>
<span data-ttu-id="1f609-724">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-724">**Description:**</span></span>  
<span data-ttu-id="1f609-725">Merhaba şimdi işlevi tooyour bilgisayarın sistem tarihi ve saati göre geçerli tarih ve saat, hello belirten bir DateTime döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-725">hello Now function returns a DateTime specifying hello current date and time, according tooyour computer's system date and time.</span></span>

<span data-ttu-id="1f609-726">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-726">**Syntax:**</span></span>  
`dt Now()`

- - -
### <a name="numfromdate"></a><span data-ttu-id="1f609-727">NumFromDate</span><span class="sxs-lookup"><span data-stu-id="1f609-727">NumFromDate</span></span>
<span data-ttu-id="1f609-728">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-728">**Description:**</span></span>  
<span data-ttu-id="1f609-729">Merhaba NumFromDate işlevi bir tarih Reklamın tarih biçiminde döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-729">hello NumFromDate function returns a date in AD’s date format.</span></span>

<span data-ttu-id="1f609-730">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-730">**Syntax:**</span></span>  
`num NumFromDate(dt value)`

<span data-ttu-id="1f609-731">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="1f609-731">**Example:**</span></span>  
`NumFromDate(CDate("2012-01-01 23:00:00"))`  
<span data-ttu-id="1f609-732">129699324000000000 döndürür</span><span class="sxs-lookup"><span data-stu-id="1f609-732">Returns 129699324000000000</span></span>

- - -
### <a name="padleft"></a><span data-ttu-id="1f609-733">PadLeft</span><span class="sxs-lookup"><span data-stu-id="1f609-733">PadLeft</span></span>
<span data-ttu-id="1f609-734">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-734">**Description:**</span></span>  
<span data-ttu-id="1f609-735">Belirtilen dize tooa Hello PadLeft işlev sol klavye takımı sağlanan doldurma karakteri kullanarak uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="1f609-735">hello PadLeft function left-pads a string tooa specified length using a provided padding character.</span></span>

<span data-ttu-id="1f609-736">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-736">**Syntax:**</span></span>  
`str PadLeft(str string, num length, str padCharacter)`

* <span data-ttu-id="1f609-737">dize: dize toopad hello.</span><span class="sxs-lookup"><span data-stu-id="1f609-737">string: hello string toopad.</span></span>
* <span data-ttu-id="1f609-738">Uzunluk: hello temsil eden bir tamsayı istenen dize uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="1f609-738">length: An integer representing hello desired length of string.</span></span>
* <span data-ttu-id="1f609-739">padCharacter: hello doldurma karakteri tek karakter toouse oluşan bir dize</span><span class="sxs-lookup"><span data-stu-id="1f609-739">padCharacter: A string consisting of a single character toouse as hello pad character</span></span>

<span data-ttu-id="1f609-740">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="1f609-740">**Remarks:**</span></span>

* <span data-ttu-id="1f609-741">Dize uzunluğu Hello uzunluğundan az ise, bir uzunluk eşit toolength olana kadar sonra padCharacter (sol) art arda eklenmiş toohello dize başlangıcıdır.</span><span class="sxs-lookup"><span data-stu-id="1f609-741">If hello length of string is less than length, then padCharacter is repeatedly appended toohello beginning (left) of string until it has a length equal toolength.</span></span>
* <span data-ttu-id="1f609-742">padCharacter bir boşluk karakteri olabilir, ancak bir null değer olamaz.</span><span class="sxs-lookup"><span data-stu-id="1f609-742">PadCharacter can be a space character, but it cannot be a null value.</span></span>
* <span data-ttu-id="1f609-743">Dize uzunluğu Hello eşit tooor uzunluğundan fazla ise, dize değişmeden döndürülür.</span><span class="sxs-lookup"><span data-stu-id="1f609-743">If hello length of string is equal tooor greater than length, string is returned unchanged.</span></span>
* <span data-ttu-id="1f609-744">Dize uzunluğu daha büyük veya eşit toolength varsa, bir dize aynı toostring döndürülür.</span><span class="sxs-lookup"><span data-stu-id="1f609-744">If string has a length greater than or equal toolength, a string identical toostring is returned.</span></span>
* <span data-ttu-id="1f609-745">Dize uzunluğu Hello uzunluğundan az ise, hello yeni bir dize uzunluğu padCharacter ile doldurulan dizeyi içeren döndürülür istenen.</span><span class="sxs-lookup"><span data-stu-id="1f609-745">If hello length of string is less than length, then a new string of hello desired length is returned containing string padded with a padCharacter.</span></span>
* <span data-ttu-id="1f609-746">Dize null ise, hello işlevi boş bir dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-746">If string is null, hello function returns an empty string.</span></span>

<span data-ttu-id="1f609-747">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="1f609-747">**Example:**</span></span>  
`PadLeft("User", 10, "0")`  
<span data-ttu-id="1f609-748">"000000User" döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-748">Returns "000000User".</span></span>

- - -
### <a name="padright"></a><span data-ttu-id="1f609-749">PadRight</span><span class="sxs-lookup"><span data-stu-id="1f609-749">PadRight</span></span>
<span data-ttu-id="1f609-750">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-750">**Description:**</span></span>  
<span data-ttu-id="1f609-751">Belirtilen dize tooa Hello PadRight işlev sağ klavye takımı sağlanan doldurma karakteri kullanarak uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="1f609-751">hello PadRight function right-pads a string tooa specified length using a provided padding character.</span></span>

<span data-ttu-id="1f609-752">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-752">**Syntax:**</span></span>  
`str PadRight(str string, num length, str padCharacter)`

* <span data-ttu-id="1f609-753">dize: dize toopad hello.</span><span class="sxs-lookup"><span data-stu-id="1f609-753">string: hello string toopad.</span></span>
* <span data-ttu-id="1f609-754">Uzunluk: hello temsil eden bir tamsayı istenen dize uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="1f609-754">length: An integer representing hello desired length of string.</span></span>
* <span data-ttu-id="1f609-755">padCharacter: hello doldurma karakteri tek karakter toouse oluşan bir dize</span><span class="sxs-lookup"><span data-stu-id="1f609-755">padCharacter: A string consisting of a single character toouse as hello pad character</span></span>

<span data-ttu-id="1f609-756">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="1f609-756">**Remarks:**</span></span>

* <span data-ttu-id="1f609-757">Dize uzunluğu Hello uzunluğundan az uzunluğu eşit toolength olana kadar sonra padCharacter art arda eklenmiş toohello (sağdaki) dize sonu ise.</span><span class="sxs-lookup"><span data-stu-id="1f609-757">If hello length of string is less than length, then padCharacter is repeatedly appended toohello end (right) of string until it has a length equal toolength.</span></span>
* <span data-ttu-id="1f609-758">padCharacter bir boşluk karakteri olabilir, ancak bir null değer olamaz.</span><span class="sxs-lookup"><span data-stu-id="1f609-758">padCharacter can be a space character, but it cannot be a null value.</span></span>
* <span data-ttu-id="1f609-759">Dize uzunluğu Hello eşit tooor uzunluğundan fazla ise, dize değişmeden döndürülür.</span><span class="sxs-lookup"><span data-stu-id="1f609-759">If hello length of string is equal tooor greater than length, string is returned unchanged.</span></span>
* <span data-ttu-id="1f609-760">Dize uzunluğu daha büyük veya eşit toolength varsa, bir dize aynı toostring döndürülür.</span><span class="sxs-lookup"><span data-stu-id="1f609-760">If string has a length greater than or equal toolength, a string identical toostring is returned.</span></span>
* <span data-ttu-id="1f609-761">Dize uzunluğu Hello uzunluğundan az ise, hello yeni bir dize uzunluğu padCharacter ile doldurulan dizeyi içeren döndürülür istenen.</span><span class="sxs-lookup"><span data-stu-id="1f609-761">If hello length of string is less than length, then a new string of hello desired length is returned containing string padded with a padCharacter.</span></span>
* <span data-ttu-id="1f609-762">Dize null ise, hello işlevi boş bir dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-762">If string is null, hello function returns an empty string.</span></span>

<span data-ttu-id="1f609-763">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="1f609-763">**Example:**</span></span>  
`PadRight("User", 10, "0")`  
<span data-ttu-id="1f609-764">"User000000" döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-764">Returns "User000000".</span></span>

- - -
### <a name="pcase"></a><span data-ttu-id="1f609-765">PCase</span><span class="sxs-lookup"><span data-stu-id="1f609-765">PCase</span></span>
<span data-ttu-id="1f609-766">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-766">**Description:**</span></span>  
<span data-ttu-id="1f609-767">Merhaba PCase işlevi hello ilk karakteri bir dize tooupper durumda her boşlukla ayrılmış sözcük dönüştürür ve diğer tüm karakterler dönüştürülür toolower durumda.</span><span class="sxs-lookup"><span data-stu-id="1f609-767">hello PCase function converts hello first character of each space delimited word in a string tooupper case, and all other characters are converted toolower case.</span></span>

<span data-ttu-id="1f609-768">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-768">**Syntax:**</span></span>  
`String PCase(string)`

<span data-ttu-id="1f609-769">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="1f609-769">**Remarks:**</span></span>

* <span data-ttu-id="1f609-770">Bu işlev bir kısaltma gibi tamamen büyük bir sözcük doğru büyük/küçük harf tooconvert şu anda sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="1f609-770">This function does not currently provide proper casing tooconvert a word that is entirely uppercase, such as an acronym.</span></span>

<span data-ttu-id="1f609-771">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="1f609-771">**Example:**</span></span>  
`PCase("TEsT")`  
<span data-ttu-id="1f609-772">"Test" döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-772">Returns "Test".</span></span>

`PCase(LCase("TEST"))`  
<span data-ttu-id="1f609-773">"Test" döndürür</span><span class="sxs-lookup"><span data-stu-id="1f609-773">Returns "Test"</span></span>

- - -
### <a name="randomnum"></a><span data-ttu-id="1f609-774">RandomNum</span><span class="sxs-lookup"><span data-stu-id="1f609-774">RandomNum</span></span>
<span data-ttu-id="1f609-775">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-775">**Description:**</span></span>  
<span data-ttu-id="1f609-776">Merhaba RandomNum işlevi, belirtilen aralık arasında rastgele bir sayı döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-776">hello RandomNum function returns a random number between a specified interval.</span></span>

<span data-ttu-id="1f609-777">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-777">**Syntax:**</span></span>  
`num RandomNum(num start, num end)`

* <span data-ttu-id="1f609-778">Başlat: numara tanımlayıcı hello alt sınır olarak hello rastgele bir değeri toogenerate</span><span class="sxs-lookup"><span data-stu-id="1f609-778">start: a number identifying hello lower limit of hello random value toogenerate</span></span>
* <span data-ttu-id="1f609-779">Son: bir numara tanımlayıcı hello sayısı üst sınırı hello rastgele bir değeri toogenerate</span><span class="sxs-lookup"><span data-stu-id="1f609-779">end: a number identifying hello upper limit of hello random value toogenerate</span></span>

<span data-ttu-id="1f609-780">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="1f609-780">**Example:**</span></span>  
`Random(100,999)`  
<span data-ttu-id="1f609-781">734 döndürebilir.</span><span class="sxs-lookup"><span data-stu-id="1f609-781">Can return 734.</span></span>

- - -
### <a name="removeduplicates"></a><span data-ttu-id="1f609-782">RemoveDuplicates</span><span class="sxs-lookup"><span data-stu-id="1f609-782">RemoveDuplicates</span></span>
<span data-ttu-id="1f609-783">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-783">**Description:**</span></span>  
<span data-ttu-id="1f609-784">Merhaba RemoveDuplicates işlevi, birden çok değerli bir dize alır ve her değerin benzersiz olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="1f609-784">hello RemoveDuplicates function takes a multi-valued string and make sure each value is unique.</span></span>

<span data-ttu-id="1f609-785">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-785">**Syntax:**</span></span>  
`mvstr RemoveDuplicates(mvstr attribute)`

<span data-ttu-id="1f609-786">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="1f609-786">**Example:**</span></span>  
`RemoveDuplicates([proxyAddresses])`  
<span data-ttu-id="1f609-787">Burada tüm yinelenen değerleri kaldırılmış bir ayıklanmış proxyAddress özniteliği döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-787">Returns a sanitized proxyAddress attribute where all duplicate values have been removed.</span></span>

- - -
### <a name="replace"></a><span data-ttu-id="1f609-788">Değiştir</span><span class="sxs-lookup"><span data-stu-id="1f609-788">Replace</span></span>
<span data-ttu-id="1f609-789">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-789">**Description:**</span></span>  
<span data-ttu-id="1f609-790">Merhaba Değiştir işlev bir dize tooanother dize tüm oluşumlarını değiştirir.</span><span class="sxs-lookup"><span data-stu-id="1f609-790">hello Replace function replaces all occurrences of a string tooanother string.</span></span>

<span data-ttu-id="1f609-791">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-791">**Syntax:**</span></span>  
`str Replace(str string, str OldValue, str NewValue)`

* <span data-ttu-id="1f609-792">dize: dize tooreplace değerler.</span><span class="sxs-lookup"><span data-stu-id="1f609-792">string: A string tooreplace values in.</span></span>
* <span data-ttu-id="1f609-793">OldValue: hello dize toosearch ve tooreplace.</span><span class="sxs-lookup"><span data-stu-id="1f609-793">OldValue: hello string toosearch for and tooreplace.</span></span>
* <span data-ttu-id="1f609-794">NewValue: dize tooreplace hello.</span><span class="sxs-lookup"><span data-stu-id="1f609-794">NewValue: hello string tooreplace to.</span></span>

<span data-ttu-id="1f609-795">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="1f609-795">**Remarks:**</span></span>  
<span data-ttu-id="1f609-796">Merhaba işlevi özel adlar aşağıdaki hello tanır:</span><span class="sxs-lookup"><span data-stu-id="1f609-796">hello function recognizes hello following special monikers:</span></span>

* <span data-ttu-id="1f609-797">\n – yeni satır</span><span class="sxs-lookup"><span data-stu-id="1f609-797">\n – New Line</span></span>
* <span data-ttu-id="1f609-798">\r – satır başı</span><span class="sxs-lookup"><span data-stu-id="1f609-798">\r – Carriage Return</span></span>
* <span data-ttu-id="1f609-799">\t – sekmesi</span><span class="sxs-lookup"><span data-stu-id="1f609-799">\t – Tab</span></span>

<span data-ttu-id="1f609-800">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="1f609-800">**Example:**</span></span>  
`Replace([address],"\r\n",", ")`  
<span data-ttu-id="1f609-801">CRLF virgül ve boşluk ile değiştirir ve çok neden olabilir "Bir Microsoft yolu, Redmond, WA, ABD"</span><span class="sxs-lookup"><span data-stu-id="1f609-801">Replaces CRLF with a comma and space, and could lead too"One Microsoft Way, Redmond, WA, USA"</span></span>

- - -
### <a name="replacechars"></a><span data-ttu-id="1f609-802">ReplaceChars</span><span class="sxs-lookup"><span data-stu-id="1f609-802">ReplaceChars</span></span>
<span data-ttu-id="1f609-803">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-803">**Description:**</span></span>  
<span data-ttu-id="1f609-804">Merhaba ReplaceChars işlevi karakterler hello ReplacePattern dize bulundu tüm oluşumlarını değiştirir.</span><span class="sxs-lookup"><span data-stu-id="1f609-804">hello ReplaceChars function replaces all occurrences of characters found in hello ReplacePattern string.</span></span>

<span data-ttu-id="1f609-805">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-805">**Syntax:**</span></span>  
`str ReplaceChars(str string, str ReplacePattern)`

* <span data-ttu-id="1f609-806">dize: içinde bir dize tooreplace karakter.</span><span class="sxs-lookup"><span data-stu-id="1f609-806">string: A string tooreplace characters in.</span></span>
* <span data-ttu-id="1f609-807">ReplacePattern: karakter tooreplace ile bir sözlük içeren bir dize.</span><span class="sxs-lookup"><span data-stu-id="1f609-807">ReplacePattern: a string containing a dictionary with characters tooreplace.</span></span>

<span data-ttu-id="1f609-808">Hello biçimi {kaynak1} şeklindedir: {target1}, {kaynak2}: {target2}, {kaynakN}, {targetN} kaynak hello karakter toofind ve hedef hello dize tooreplace sahip olduğu.</span><span class="sxs-lookup"><span data-stu-id="1f609-808">hello format is {source1}:{target1},{source2}:{target2},{sourceN},{targetN} where source is hello character toofind and target hello string tooreplace with.</span></span>

<span data-ttu-id="1f609-809">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="1f609-809">**Remarks:**</span></span>

* <span data-ttu-id="1f609-810">Hello işlev her oluşumu tanımlanan kaynakları alır ve bunları hello hedefleri ile değiştirir.</span><span class="sxs-lookup"><span data-stu-id="1f609-810">hello function takes each occurrence of defined sources and replaces them with hello targets.</span></span>
* <span data-ttu-id="1f609-811">Merhaba kaynak tam olarak bir (unicode) karakter olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1f609-811">hello source must be exactly one (unicode) character.</span></span>
* <span data-ttu-id="1f609-812">Merhaba kaynağı boş veya bir karakter (ayrıştırma hatası) daha uzun olamaz.</span><span class="sxs-lookup"><span data-stu-id="1f609-812">hello source cannot be empty or longer than one character (parsing error).</span></span>
* <span data-ttu-id="1f609-813">Merhaba hedef örneğin ö:oe, β:ss birden çok karakter uzunluğunda olabilir.</span><span class="sxs-lookup"><span data-stu-id="1f609-813">hello target can have multiple characters, for example ö:oe, β:ss.</span></span>
* <span data-ttu-id="1f609-814">Merhaba hedef hello karakter kaldırılması gerektiğini belirten boş olabilir.</span><span class="sxs-lookup"><span data-stu-id="1f609-814">hello target can be empty indicating that hello character should be removed.</span></span>
* <span data-ttu-id="1f609-815">Merhaba kaynak küçük harfe duyarlıdır ve tam bir eşleşme olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1f609-815">hello source is case-sensitive and must be an exact match.</span></span>
* <span data-ttu-id="1f609-816">Merhaba, (virgül) ve: (iki nokta üst üste) ayrılmış karakterler ve bu işlevi kullanılarak değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="1f609-816">hello , (comma) and : (colon) are reserved characters and cannot be replaced using this function.</span></span>
* <span data-ttu-id="1f609-817">Alanları ve diğer beyaz karakter hello ReplacePattern dize göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="1f609-817">Spaces and other white characters in hello ReplacePattern string are ignored.</span></span>

<span data-ttu-id="1f609-818">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="1f609-818">**Example:**</span></span>  
`%ReplaceString% = ’:,Å:A,Ä:A,Ö:O,å:a,ä:a,ö,o`

`ReplaceChars("Räksmörgås",%ReplaceString%)`  
<span data-ttu-id="1f609-819">Raksmorgas döndürür</span><span class="sxs-lookup"><span data-stu-id="1f609-819">Returns Raksmorgas</span></span>

`ReplaceChars("O’Neil",%ReplaceString%)`  
<span data-ttu-id="1f609-820">Kaldırılan tanımlı toobe değilse "ONeil", hello tek değer döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-820">Returns "ONeil", hello single tick is defined toobe removed.</span></span>

- - -
### <a name="right"></a><span data-ttu-id="1f609-821">Sağ</span><span class="sxs-lookup"><span data-stu-id="1f609-821">Right</span></span>
<span data-ttu-id="1f609-822">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-822">**Description:**</span></span>  
<span data-ttu-id="1f609-823">Merhaba sağ işlevi hello bir dize sağ (Bitiş) belirtilen sayıda karakteri döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-823">hello Right function returns a specified number of characters from hello right (end) of a string.</span></span>

<span data-ttu-id="1f609-824">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-824">**Syntax:**</span></span>  
`str Right(str string, num NumChars)`

* <span data-ttu-id="1f609-825">dize: Merhaba dize tooreturn karakterler</span><span class="sxs-lookup"><span data-stu-id="1f609-825">string: hello string tooreturn characters from</span></span>
* <span data-ttu-id="1f609-826">NumChars: hello uçtan (sağdaki) dizenin karakter tooreturn hello sayısı tanımlayan bir numara</span><span class="sxs-lookup"><span data-stu-id="1f609-826">NumChars: a number identifying hello number of characters tooreturn from hello end (right) of string</span></span>

<span data-ttu-id="1f609-827">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="1f609-827">**Remarks:**</span></span>  
<span data-ttu-id="1f609-828">NumChars karakter hello son dize konumundan döndürülür.</span><span class="sxs-lookup"><span data-stu-id="1f609-828">NumChars characters are returned from hello last position of string.</span></span>

<span data-ttu-id="1f609-829">Dizedeki son numChars karakter Hello içeren bir dize:</span><span class="sxs-lookup"><span data-stu-id="1f609-829">A string containing hello last numChars characters in string:</span></span>

* <span data-ttu-id="1f609-830">Varsa numChars = 0, boş bir dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-830">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="1f609-831">NumChars < 0, döndürmesi durumunda giriş dizesi.</span><span class="sxs-lookup"><span data-stu-id="1f609-831">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="1f609-832">Dize null ise, boş bir dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-832">If string is null, return empty string.</span></span>

<span data-ttu-id="1f609-833">Sayı belirtilen NumChars hello daha az karakter dizesini içeren bir dize aynı toostring döndürülür.</span><span class="sxs-lookup"><span data-stu-id="1f609-833">If string contains fewer characters than hello number specified in NumChars, a string identical toostring is returned.</span></span>

<span data-ttu-id="1f609-834">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="1f609-834">**Example:**</span></span>  
`Right("John Doe", 3)`  
<span data-ttu-id="1f609-835">"Doe" döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-835">Returns "Doe".</span></span>

- - -
### <a name="rtrim"></a><span data-ttu-id="1f609-836">RTrim</span><span class="sxs-lookup"><span data-stu-id="1f609-836">RTrim</span></span>
<span data-ttu-id="1f609-837">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-837">**Description:**</span></span>  
<span data-ttu-id="1f609-838">Merhaba RTrim işlevi bir dizeden sondaki boşluk kaldırır.</span><span class="sxs-lookup"><span data-stu-id="1f609-838">hello RTrim function removes trailing white spaces from a string.</span></span>

<span data-ttu-id="1f609-839">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-839">**Syntax:**</span></span>  
`str RTrim(str value)`

<span data-ttu-id="1f609-840">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="1f609-840">**Example:**</span></span>  
`RTrim(" Test ")`  
<span data-ttu-id="1f609-841">"Test" döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-841">Returns " Test".</span></span>

- - -
### <a name="select"></a><span data-ttu-id="1f609-842">Şunu seçin:</span><span class="sxs-lookup"><span data-stu-id="1f609-842">Select</span></span>
<span data-ttu-id="1f609-843">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-843">**Description:**</span></span>  
<span data-ttu-id="1f609-844">Birden çok değerli bir öznitelik (veya bir ifade çıktısını) içindeki tüm değerleri belirtilen işlevine dayalı işlemi.</span><span class="sxs-lookup"><span data-stu-id="1f609-844">Process all values in a multi-valued attribute (or output of an expression) based on function specified.</span></span>

<span data-ttu-id="1f609-845">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-845">**Syntax:**</span></span>  
`mvattr Select(variable item, mvattr attribute, func function)`  
`mvattr Select(variable item, exp expression, func function)`

* <span data-ttu-id="1f609-846">Madde: hello birden çok değerli öznitelik bir öğeyi temsil eder</span><span class="sxs-lookup"><span data-stu-id="1f609-846">item: Represents an element in hello multi-valued attribute</span></span>
* <span data-ttu-id="1f609-847">Öznitelik: hello birden çok değerli özniteliği</span><span class="sxs-lookup"><span data-stu-id="1f609-847">attribute: hello multi-valued attribute</span></span>
* <span data-ttu-id="1f609-848">ifade: değerler koleksiyonu döndüren bir ifadeye</span><span class="sxs-lookup"><span data-stu-id="1f609-848">expression: an expression that returns a collection of values</span></span>
* <span data-ttu-id="1f609-849">koşul: hello özniteliği bir öğeyi işleyebilir işlevi</span><span class="sxs-lookup"><span data-stu-id="1f609-849">condition: any function that can process an item in hello attribute</span></span>

<span data-ttu-id="1f609-850">**Örnekler:**</span><span class="sxs-lookup"><span data-stu-id="1f609-850">**Examples:**</span></span>  
`Select($item,[otherPhone],Replace($item,“-”,“”))`  
<span data-ttu-id="1f609-851">Tire (-) kaldırdıktan sonra tüm hello değerler hello birden çok değerli özniteliği otherPhone döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-851">Return all hello values in hello multi-valued attribute otherPhone after hyphens (-) have been removed.</span></span>

- - -
### <a name="split"></a><span data-ttu-id="1f609-852">Böl</span><span class="sxs-lookup"><span data-stu-id="1f609-852">Split</span></span>
<span data-ttu-id="1f609-853">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-853">**Description:**</span></span>  
<span data-ttu-id="1f609-854">Merhaba bölünmüş işlevi bir sınırlayıcı ile ayrılmış bir dize alır ve birden çok değerli bir dize kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="1f609-854">hello Split function takes a string separated with a delimiter and makes it a multi-valued string.</span></span>

<span data-ttu-id="1f609-855">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-855">**Syntax:**</span></span>  
`mvstr Split(str value, str delimiter)`  
`mvstr Split(str value, str delimiter, num limit)`

* <span data-ttu-id="1f609-856">değer: Merhaba sınırlayıcı karakter tooseparate dizesi.</span><span class="sxs-lookup"><span data-stu-id="1f609-856">value: hello string with a delimiter character tooseparate.</span></span>
* <span data-ttu-id="1f609-857">sınırlayıcı: tek bir sınırlayıcı hello olarak kullanılan karakter toobe.</span><span class="sxs-lookup"><span data-stu-id="1f609-857">delimiter: single character toobe used as hello delimiter.</span></span>
* <span data-ttu-id="1f609-858">sınır: en yüksek sayıda döndürebilir değeri.</span><span class="sxs-lookup"><span data-stu-id="1f609-858">limit: maximum number of values that can return.</span></span>

<span data-ttu-id="1f609-859">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="1f609-859">**Example:**</span></span>  
`Split("SMTP:john.doe@contoso.com,smtp:jd@contoso.com",",")`  
<span data-ttu-id="1f609-860">Merhaba proxyAddress özniteliği için yararlı 2 öğeleri birden çok değerli bir dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-860">Returns a multi-valued string with 2 elements useful for hello proxyAddress attribute.</span></span>

- - -
### <a name="stringfromguid"></a><span data-ttu-id="1f609-861">StringFromGuid</span><span class="sxs-lookup"><span data-stu-id="1f609-861">StringFromGuid</span></span>
<span data-ttu-id="1f609-862">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-862">**Description:**</span></span>  
<span data-ttu-id="1f609-863">Merhaba StringFromGuid işlevi bir ikili GUID alır ve tooa dizesini sayıya dönüştürür</span><span class="sxs-lookup"><span data-stu-id="1f609-863">hello StringFromGuid function takes a binary GUID and converts it tooa string</span></span>

<span data-ttu-id="1f609-864">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-864">**Syntax:**</span></span>  
`str StringFromGuid(bin GUID)`

- - -
### <a name="stringfromsid"></a><span data-ttu-id="1f609-865">StringFromSid</span><span class="sxs-lookup"><span data-stu-id="1f609-865">StringFromSid</span></span>
<span data-ttu-id="1f609-866">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-866">**Description:**</span></span>  
<span data-ttu-id="1f609-867">Merhaba StringFromSid işlevi bir güvenlik tanımlayıcısı tooa dizesi içeren bir bayt dizisi dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-867">hello StringFromSid function converts a byte array containing a security identifier tooa string.</span></span>

<span data-ttu-id="1f609-868">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-868">**Syntax:**</span></span>  
`str StringFromSid(bin ObjectSID)`  

- - -
### <a name="switch"></a><span data-ttu-id="1f609-869">Anahtar</span><span class="sxs-lookup"><span data-stu-id="1f609-869">Switch</span></span>
<span data-ttu-id="1f609-870">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-870">**Description:**</span></span>  
<span data-ttu-id="1f609-871">Merhaba anahtar kullanılan tooreturn değerlendirilen koşullara göre tek bir değer işlevdir.</span><span class="sxs-lookup"><span data-stu-id="1f609-871">hello Switch function is used tooreturn a single value based on evaluated conditions.</span></span>

<span data-ttu-id="1f609-872">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-872">**Syntax:**</span></span>  
`var Switch(exp expr1, var value1[, exp expr2, var value … [, exp expr, var valueN]])`

* <span data-ttu-id="1f609-873">Expr: tooevaluate istediğiniz değişken ifadesi.</span><span class="sxs-lookup"><span data-stu-id="1f609-873">expr: Variant expression you want tooevaluate.</span></span>
* <span data-ttu-id="1f609-874">değer: değerin toobe döndürülen hello karşılık gelen ifadesi True ise.</span><span class="sxs-lookup"><span data-stu-id="1f609-874">value: Value toobe returned if hello corresponding expression is True.</span></span>

<span data-ttu-id="1f609-875">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="1f609-875">**Remarks:**</span></span>  
<span data-ttu-id="1f609-876">Merhaba anahtar işlevi bağımsız değişken listesi ifadeleri ve değer çiftlerinden oluşur.</span><span class="sxs-lookup"><span data-stu-id="1f609-876">hello Switch function argument list consists of pairs of expressions and values.</span></span> <span data-ttu-id="1f609-877">Merhaba ifadeler sol tooright değerlendirilir ve hello ilk ifade tooevaluate tooTrue ile ilişkili hello değeri döndürülür.</span><span class="sxs-lookup"><span data-stu-id="1f609-877">hello expressions are evaluated from left tooright, and hello value associated with hello first expression tooevaluate tooTrue is returned.</span></span> <span data-ttu-id="1f609-878">Merhaba bölümleri düzgün eşleştirilmedi, bir çalışma zamanı hatası oluşur.</span><span class="sxs-lookup"><span data-stu-id="1f609-878">If hello parts aren't properly paired, a run-time error occurs.</span></span>

<span data-ttu-id="1f609-879">Örneğin, Expr1 True ise, anahtar value1 döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-879">For example, if expr1 is True, Switch returns value1.</span></span> <span data-ttu-id="1f609-880">Yanlış ifade 1., ancak expr 2 True ise, anahtar değeri 2 vb. döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-880">If expr-1 is False, but expr-2 is True, Switch returns value-2, and so on.</span></span>

<span data-ttu-id="1f609-881">Anahtar döndüren bir hiçbir şeyin varsa:</span><span class="sxs-lookup"><span data-stu-id="1f609-881">Switch returns a Nothing if:</span></span>

* <span data-ttu-id="1f609-882">Merhaba ifadeleri hiçbiri True olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="1f609-882">None of hello expressions are True.</span></span>
* <span data-ttu-id="1f609-883">Merhaba ilk True ifadenin null karşılık gelen bir değere sahip.</span><span class="sxs-lookup"><span data-stu-id="1f609-883">hello first True expression has a corresponding value that is Null.</span></span>

<span data-ttu-id="1f609-884">Bunlardan yalnızca birini döndürür olsa bile anahtar tüm ifadeler değerlendirir.</span><span class="sxs-lookup"><span data-stu-id="1f609-884">Switch evaluates all expressions, even though it returns only one of them.</span></span> <span data-ttu-id="1f609-885">Bu nedenle, istenmeyen yan etkileri için izlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1f609-885">For this reason, you should watch for undesirable side effects.</span></span> <span data-ttu-id="1f609-886">Örneğin, herhangi bir ifade Hello değerlendirmesi sıfır hatası bir bölme sonuçlanırsa, bir hata oluşur.</span><span class="sxs-lookup"><span data-stu-id="1f609-886">For example, if hello evaluation of any expression results in a division by zero error, an error occurs.</span></span>

<span data-ttu-id="1f609-887">Değer, özel bir dize döndürür hello hata işlevi de olabilir.</span><span class="sxs-lookup"><span data-stu-id="1f609-887">Value can also be hello Error function, which would return a custom string.</span></span>

<span data-ttu-id="1f609-888">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="1f609-888">**Example:**</span></span>  
`Switch([city] = "London", "English", [city] = "Rome", "Italian", [city] = "Paris", "French", True, Error("Unknown city"))`  
<span data-ttu-id="1f609-889">Bazı önemli şehirlerde konuşulan hello dili döndürür, aksi takdirde bir hata döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-889">Returns hello language spoken in some major cities, otherwise returns an Error.</span></span>

- - -
### <a name="trim"></a><span data-ttu-id="1f609-890">Kırpma</span><span class="sxs-lookup"><span data-stu-id="1f609-890">Trim</span></span>
<span data-ttu-id="1f609-891">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-891">**Description:**</span></span>  
<span data-ttu-id="1f609-892">Merhaba kırpma işlevi baştaki ve sondaki boşlukları bir dizeden kaldırır.</span><span class="sxs-lookup"><span data-stu-id="1f609-892">hello Trim function removes leading and trailing white spaces from a string.</span></span>

<span data-ttu-id="1f609-893">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-893">**Syntax:**</span></span>  
`str Trim(str value)`  

<span data-ttu-id="1f609-894">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="1f609-894">**Example:**</span></span>  
`Trim(" Test ")`  
<span data-ttu-id="1f609-895">"Test" döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-895">Returns "Test".</span></span>

`Trim([proxyAddresses])`  
<span data-ttu-id="1f609-896">Baştaki ve sondaki boşlukları hello proxyAddress özniteliğinde her bir değer için kaldırır.</span><span class="sxs-lookup"><span data-stu-id="1f609-896">Removes leading and trailing spaces for each value in hello proxyAddress attribute.</span></span>

- - -
### <a name="ucase"></a><span data-ttu-id="1f609-897">UCase</span><span class="sxs-lookup"><span data-stu-id="1f609-897">UCase</span></span>
<span data-ttu-id="1f609-898">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-898">**Description:**</span></span>  
<span data-ttu-id="1f609-899">Merhaba UCase işlev bir dize tooupper durumda tüm karakterleri dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-899">hello UCase function converts all characters in a string tooupper case.</span></span>

<span data-ttu-id="1f609-900">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-900">**Syntax:**</span></span>  
`str UCase(str string)`

<span data-ttu-id="1f609-901">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="1f609-901">**Example:**</span></span>  
`UCase("TeSt")`  
<span data-ttu-id="1f609-902">"TEST" döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-902">Returns "TEST".</span></span>

- - -
### <a name="where"></a><span data-ttu-id="1f609-903">Burada</span><span class="sxs-lookup"><span data-stu-id="1f609-903">Where</span></span>

<span data-ttu-id="1f609-904">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-904">**Description:**</span></span>  
<span data-ttu-id="1f609-905">Belirli bir koşula dayalı birden çok değerli özniteliği (veya bir ifade çıktısını) değerleri kümesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-905">Returns a subset of values from a multi-valued attribute (or output of an expression) based on specific condition.</span></span>

<span data-ttu-id="1f609-906">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-906">**Syntax:**</span></span>  
`mvattr Where(variable item, mvattr attribute, exp condition)`  
`mvattr Where(variable item, exp expression, exp condition)`  
* <span data-ttu-id="1f609-907">Madde: hello birden çok değerli öznitelik bir öğeyi temsil eder</span><span class="sxs-lookup"><span data-stu-id="1f609-907">item: Represents an element in hello multi-valued attribute</span></span>
* <span data-ttu-id="1f609-908">Öznitelik: hello birden çok değerli özniteliği</span><span class="sxs-lookup"><span data-stu-id="1f609-908">attribute: hello multi-valued attribute</span></span>
* <span data-ttu-id="1f609-909">koşul: olabilir herhangi bir ifade hesaplanan tootrue ya da yanlış</span><span class="sxs-lookup"><span data-stu-id="1f609-909">condition: any expression that can be evaluated tootrue or false</span></span>
* <span data-ttu-id="1f609-910">ifade: değerler koleksiyonu döndüren bir ifadeye</span><span class="sxs-lookup"><span data-stu-id="1f609-910">expression: an expression that returns a collection of values</span></span>

<span data-ttu-id="1f609-911">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="1f609-911">**Example:**</span></span>  
`Where($item,[userCertificate],CertNotAfter($item)>Now())`  
<span data-ttu-id="1f609-912">Merhaba sertifika değerler, süresi dolmuş olmayan hello birden çok değerli özniteliği userCertificate içinde döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-912">Return hello certificate values in hello multi-valued attribute userCertificate which aren’t expired.</span></span>

- - -
### <a name="with"></a><span data-ttu-id="1f609-913">İle</span><span class="sxs-lookup"><span data-stu-id="1f609-913">With</span></span>
<span data-ttu-id="1f609-914">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-914">**Description:**</span></span>  
<span data-ttu-id="1f609-915">işlevi ile Merhaba yolu toosimplify değişken toorepresent bir görünen bir alt kullanarak veya birden fazla kez hello karmaşık ifadesinde karmaşık bir ifade sağlar.</span><span class="sxs-lookup"><span data-stu-id="1f609-915">hello With function provides a way toosimplify a complex expression by using a variable toorepresent a subexpression which appears one or more times in hello complex expression.</span></span>

<span data-ttu-id="1f609-916">**Sözdizimi:**
`With(var variable, exp subExpression, exp complexExpression)`</span><span class="sxs-lookup"><span data-stu-id="1f609-916">**Syntax:**
`With(var variable, exp subExpression, exp complexExpression)`</span></span>  
* <span data-ttu-id="1f609-917">değişken: Merhaba alt temsil eder.</span><span class="sxs-lookup"><span data-stu-id="1f609-917">variable: Represents hello subexpression.</span></span>
* <span data-ttu-id="1f609-918">Alt: değişkeni tarafından temsil edilen alt.</span><span class="sxs-lookup"><span data-stu-id="1f609-918">subExpression: subexpression represented by variable.</span></span>
* <span data-ttu-id="1f609-919">complexExpression: karmaşık bir ifade.</span><span class="sxs-lookup"><span data-stu-id="1f609-919">complexExpression: A complex expression.</span></span>

<span data-ttu-id="1f609-920">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="1f609-920">**Example:**</span></span>  
`With($unExpiredCerts,Where($item,[userCertificate],CertNotAfter($item)>Now()),IIF(Count($unExpiredCerts)>0,$unExpiredCerts,NULL))`  
<span data-ttu-id="1f609-921">İşlevsel olarak eşdeğerdir:</span><span class="sxs-lookup"><span data-stu-id="1f609-921">Is functionally equivalent to:</span></span>  
`IIF (Count(Where($item,[userCertificate],CertNotAfter($item)>Now()))>0, Where($item,[userCertificate],CertNotAfter($item)>Now()),NULL)`  
<span data-ttu-id="1f609-922">Hangi hello userCertificate özniteliği yalnızca süresi dolmamış sertifika değerleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-922">Which returns only unexpired certificate values in hello userCertificate attribute.</span></span>


- - -
### <a name="word"></a><span data-ttu-id="1f609-923">Word</span><span class="sxs-lookup"><span data-stu-id="1f609-923">Word</span></span>
<span data-ttu-id="1f609-924">**Açıklama:**</span><span class="sxs-lookup"><span data-stu-id="1f609-924">**Description:**</span></span>  
<span data-ttu-id="1f609-925">Hello Word işlevi hello sınırlayıcıları toouse ve hello word numara tooreturn açıklayan parametrelerine göre bir dize içindeki bir sözcük döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-925">hello Word function returns a word contained within a string, based on parameters describing hello delimiters toouse and hello word number tooreturn.</span></span>

<span data-ttu-id="1f609-926">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="1f609-926">**Syntax:**</span></span>  
`str Word(str string, num WordNumber, str delimiters)`

* <span data-ttu-id="1f609-927">dize: dize tooreturn bir sözcük hello.</span><span class="sxs-lookup"><span data-stu-id="1f609-927">string: hello string tooreturn a word from.</span></span>
* <span data-ttu-id="1f609-928">WordNumber: hangi word numarasını tanımlayan bir sayı döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="1f609-928">WordNumber: a number identifying which word number should return.</span></span>
* <span data-ttu-id="1f609-929">Sınırlayıcılar: kullanılan tooidentify sözcükler olmalıdır hello delimiter(s) temsil eden bir dize</span><span class="sxs-lookup"><span data-stu-id="1f609-929">delimiters: a string representing hello delimiter(s) that should be used tooidentify words</span></span>

<span data-ttu-id="1f609-930">**Notlar:**</span><span class="sxs-lookup"><span data-stu-id="1f609-930">**Remarks:**</span></span>  
<span data-ttu-id="1f609-931">Her bir hello sınırlayıcıları hello karakter birini ayırarak dizedeki karakter dizesini sözcükler olarak tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="1f609-931">Each string of characters in string separated by hello one of hello characters in delimiters are identified as words:</span></span>

* <span data-ttu-id="1f609-932">Varsa < 1 sayı, boş dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-932">If number < 1, returns empty string.</span></span>
* <span data-ttu-id="1f609-933">Dize null ise, boş bir dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f609-933">If string is null, returns empty string.</span></span>

<span data-ttu-id="1f609-934">Sözcük sayısı sayısından az dize içeriyor ya da dizesi sınırlayıcıları tarafından tanımlanan herhangi bir sözcük içermiyor, boş bir dize döndürdü.</span><span class="sxs-lookup"><span data-stu-id="1f609-934">If string contains less than number words, or string does not contain any words identified by delimiters, an empty string is returned.</span></span>

<span data-ttu-id="1f609-935">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="1f609-935">**Example:**</span></span>  
`Word("hello quick brown fox",3," ")`  
<span data-ttu-id="1f609-936">"Kahverengi" döndürür</span><span class="sxs-lookup"><span data-stu-id="1f609-936">Returns "brown"</span></span>

`Word("This,string!has&many separators",3,",!&#")`  
<span data-ttu-id="1f609-937">"Var" döndürür</span><span class="sxs-lookup"><span data-stu-id="1f609-937">Would return "has"</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1f609-938">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="1f609-938">Additional Resources</span></span>
* [<span data-ttu-id="1f609-939">Bildirim temelli hazırlama ifadelerini anlama</span><span class="sxs-lookup"><span data-stu-id="1f609-939">Understanding Declarative Provisioning Expressions</span></span>](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md)
* [<span data-ttu-id="1f609-940">Azure AD Connect eşitleme: Eşitleme seçeneklerini özelleştirme</span><span class="sxs-lookup"><span data-stu-id="1f609-940">Azure AD Connect Sync: Customizing Synchronization options</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="1f609-941">Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="1f609-941">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
