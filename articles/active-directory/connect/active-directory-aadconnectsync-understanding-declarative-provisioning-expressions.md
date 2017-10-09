---
title: "Azure AD Connect: Bildirim temelli hazırlama ifadelerini | Microsoft Docs"
description: "Merhaba bildirim temelli hazırlama ifadelerini açıklanmaktadır."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: e3ea53c8-3801-4acf-a297-0fb9bb1bf11d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 516bcf1991c608d33aefc19551254d8b2bfc024f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understanding-declarative-provisioning-expressions"></a><span data-ttu-id="5560d-103">Azure AD Connect eşitleme: bildirim temelli hazırlama ifadeleri anlama</span><span class="sxs-lookup"><span data-stu-id="5560d-103">Azure AD Connect sync: Understanding Declarative Provisioning Expressions</span></span>
<span data-ttu-id="5560d-104">Azure AD Connect eşitleme ilk Forefront Identity Manager 2010'da sunulan bildirim temelli hazırlama üzerinde oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5560d-104">Azure AD Connect sync builds on declarative provisioning first introduced in Forefront Identity Manager 2010.</span></span> <span data-ttu-id="5560d-105">Tooimplement tanır tam kimlik tümleştirme iş mantığınızı hello gerek toowrite olmadan derlenmiş kod.</span><span class="sxs-lookup"><span data-stu-id="5560d-105">It allows you tooimplement your complete identity integration business logic without hello need toowrite compiled code.</span></span>

<span data-ttu-id="5560d-106">Bildirim temelli hazırlama, önemli bir bölümünü özniteliği akışlarında kullanılan hello ifade dilidir.</span><span class="sxs-lookup"><span data-stu-id="5560d-106">An essential part of declarative provisioning is hello expression language used in attribute flows.</span></span> <span data-ttu-id="5560d-107">kullanılan hello dili, Microsoft® Visual Basic® for Applications (VBA) bir alt kümesidir.</span><span class="sxs-lookup"><span data-stu-id="5560d-107">hello language used is a subset of Microsoft® Visual Basic® for Applications (VBA).</span></span> <span data-ttu-id="5560d-108">Bu dil Microsoft Office'de kullanılır ve VBScript deneyimi olan kullanıcılar da onu tanımaz.</span><span class="sxs-lookup"><span data-stu-id="5560d-108">This language is used in Microsoft Office and users with experience of VBScript will also recognize it.</span></span> <span data-ttu-id="5560d-109">Merhaba bildirim temelli hazırlama ifade dili yalnızca işlevler kullanılarak ve yapılandırılmış bir dil değil.</span><span class="sxs-lookup"><span data-stu-id="5560d-109">hello Declarative Provisioning Expression Language is only using functions and is not a structured language.</span></span> <span data-ttu-id="5560d-110">Yöntemleri veya deyimleri yok.</span><span class="sxs-lookup"><span data-stu-id="5560d-110">There are no methods or statements.</span></span> <span data-ttu-id="5560d-111">İşlevleri yerine içe tooexpress program akışı.</span><span class="sxs-lookup"><span data-stu-id="5560d-111">Functions are instead nested tooexpress program flow.</span></span>

<span data-ttu-id="5560d-112">Daha fazla ayrıntı için bkz: [Office 2013 için dil başvurusu uygulamalar için Visual Basic toohello Hoş Geldiniz](https://msdn.microsoft.com/library/gg264383.aspx).</span><span class="sxs-lookup"><span data-stu-id="5560d-112">For more details, see [Welcome toohello Visual Basic for Applications language reference for Office 2013](https://msdn.microsoft.com/library/gg264383.aspx).</span></span>

<span data-ttu-id="5560d-113">Merhaba öznitelikleri kesin türü belirtilmiş.</span><span class="sxs-lookup"><span data-stu-id="5560d-113">hello attributes are strongly typed.</span></span> <span data-ttu-id="5560d-114">Bir işlev yalnızca hello doğru türde öznitelikleri kabul eder.</span><span class="sxs-lookup"><span data-stu-id="5560d-114">A function only accepts attributes of hello correct type.</span></span> <span data-ttu-id="5560d-115">Ayrıca, büyük küçük harfe duyarlı değildir.</span><span class="sxs-lookup"><span data-stu-id="5560d-115">It is also case-sensitive.</span></span> <span data-ttu-id="5560d-116">Bir hata oluşturulur veya işlev adları ve öznitelik adları doğru büyük/küçük harf olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5560d-116">Both function names and attribute names must have proper casing or an error is thrown.</span></span>

## <a name="language-definitions-and-identifiers"></a><span data-ttu-id="5560d-117">Dil tanımları ve tanımlayıcıları</span><span class="sxs-lookup"><span data-stu-id="5560d-117">Language definitions and Identifiers</span></span>
* <span data-ttu-id="5560d-118">İşlev bağımsız değişkenleri köşeli adından sonra sahip: FunctionName (1 bağımsız değişkeni, değişken N).</span><span class="sxs-lookup"><span data-stu-id="5560d-118">Functions have a name followed by arguments in brackets: FunctionName(argument 1, argument N).</span></span>
* <span data-ttu-id="5560d-119">Öznitelikleri köşeli tarafından tanımlanır: [attributeName]</span><span class="sxs-lookup"><span data-stu-id="5560d-119">Attributes are identified by square brackets: [attributeName]</span></span>
* <span data-ttu-id="5560d-120">Parametreleri yüzde işaretleri tarafından tanımlanır: % ParameterName %</span><span class="sxs-lookup"><span data-stu-id="5560d-120">Parameters are identified by percent signs: %ParameterName%</span></span>
* <span data-ttu-id="5560d-121">Dize sabitleri tırnak içine alınmış: Örneğin, "Contoso" (Not: düz tırnak işaretleri kullanmanız gerekir "" tırnak akıllı değil ve "")</span><span class="sxs-lookup"><span data-stu-id="5560d-121">String constants are surrounded by quotes: For example, "Contoso" (Note: must use straight quotes "" and not smart quotes “”)</span></span>
* <span data-ttu-id="5560d-122">Sayısal değerler teklifleri ve beklenen toobe ondalık ifade edilir.</span><span class="sxs-lookup"><span data-stu-id="5560d-122">Numeric values are expressed without quotes and expected toobe decimal.</span></span> <span data-ttu-id="5560d-123">Onaltılık değerler öneki ile & H.</span><span class="sxs-lookup"><span data-stu-id="5560d-123">Hexadecimal values are prefixed with &H.</span></span> <span data-ttu-id="5560d-124">Örneğin, 98052 & HFF</span><span class="sxs-lookup"><span data-stu-id="5560d-124">For example, 98052, &HFF</span></span>
* <span data-ttu-id="5560d-125">Boole değerleri sabitler ile ifade edilir: True, False.</span><span class="sxs-lookup"><span data-stu-id="5560d-125">Boolean values are expressed with constants: True, False.</span></span>
* <span data-ttu-id="5560d-126">Yerleşik sabit ve değişmez değerleri yalnızca kendi adı ile ifade edilir: NULL, CRLF, IgnoreThisFlow</span><span class="sxs-lookup"><span data-stu-id="5560d-126">Built-in constants and literals are expressed with only their name: NULL, CRLF, IgnoreThisFlow</span></span>

### <a name="functions"></a><span data-ttu-id="5560d-127">İşlevler</span><span class="sxs-lookup"><span data-stu-id="5560d-127">Functions</span></span>
<span data-ttu-id="5560d-128">Bildirim temelli hazırlama, birçok işlevleri tooenable hello olasılığı tootransform öznitelik değerleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="5560d-128">Declarative provisioning uses many functions tooenable hello possibility tootransform attribute values.</span></span> <span data-ttu-id="5560d-129">Bir işlevden Hello sonuç tooanother işlevinde geçirilen şekilde bu işlevleri iç içe.</span><span class="sxs-lookup"><span data-stu-id="5560d-129">These functions can be nested so hello result from one function is passed in tooanother function.</span></span>

`Function1(Function2(Function3()))`

<span data-ttu-id="5560d-130">işlevlerin tam listesi Hello hello bulunabilir [işlev başvurusu](active-directory-aadconnectsync-functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="5560d-130">hello complete list of functions can be found in hello [function reference](active-directory-aadconnectsync-functions-reference.md).</span></span>

### <a name="parameters"></a><span data-ttu-id="5560d-131">Parametreler</span><span class="sxs-lookup"><span data-stu-id="5560d-131">Parameters</span></span>
<span data-ttu-id="5560d-132">Bir parametre bir bağlayıcı veya PowerShell kullanan bir yönetici tarafından tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="5560d-132">A parameter is defined either by a Connector or by an administrator using PowerShell.</span></span> <span data-ttu-id="5560d-133">Parametreler genellikle sistem toosystem farklı değerlere sahip, hello hello etki alanı hello kullanıcının adını, örneğin bulunur.</span><span class="sxs-lookup"><span data-stu-id="5560d-133">Parameters usually contain values that are different from system toosystem, for example hello name of hello domain hello user is located in.</span></span> <span data-ttu-id="5560d-134">Bu parametreler öznitelik akışları kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="5560d-134">These parameters can be used in attribute flows.</span></span>

<span data-ttu-id="5560d-135">gelen eşitleme kuralları için şu parametreler hello Active Directory Bağlayıcısı sağlanan hello:</span><span class="sxs-lookup"><span data-stu-id="5560d-135">hello Active Directory Connector provided hello following parameters for inbound Synchronization Rules:</span></span>

| <span data-ttu-id="5560d-136">Parametre Adı</span><span class="sxs-lookup"><span data-stu-id="5560d-136">Parameter Name</span></span> | <span data-ttu-id="5560d-137">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5560d-137">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="5560d-138">Domain.Netbios</span><span class="sxs-lookup"><span data-stu-id="5560d-138">Domain.Netbios</span></span> |<span data-ttu-id="5560d-139">Şu anda alınmakta hello etki alanı örneğin FABRIKAMSALES NetBIOS biçimi</span><span class="sxs-lookup"><span data-stu-id="5560d-139">Netbios format of hello domain currently being imported, for example FABRIKAMSALES</span></span> |
| <span data-ttu-id="5560d-140">Domain.FQDN</span><span class="sxs-lookup"><span data-stu-id="5560d-140">Domain.FQDN</span></span> |<span data-ttu-id="5560d-141">Şu anda alınmakta hello etki alanı örneğin sales.fabrikam.com FQDN biçimi</span><span class="sxs-lookup"><span data-stu-id="5560d-141">FQDN format of hello domain currently being imported, for example sales.fabrikam.com</span></span> |
| <span data-ttu-id="5560d-142">Domain.LDAP</span><span class="sxs-lookup"><span data-stu-id="5560d-142">Domain.LDAP</span></span> |<span data-ttu-id="5560d-143">Şu anda alınmakta hello etki alanı örneğin DC LDAP biçimi Satışlar, DC = fabrikam, DC = com =</span><span class="sxs-lookup"><span data-stu-id="5560d-143">LDAP format of hello domain currently being imported, for example DC=sales,DC=fabrikam,DC=com</span></span> |
| <span data-ttu-id="5560d-144">Forest.Netbios</span><span class="sxs-lookup"><span data-stu-id="5560d-144">Forest.Netbios</span></span> |<span data-ttu-id="5560d-145">NetBIOS adının biçimi şu anda alınmakta hello orman örneğin FABRIKAMCORP</span><span class="sxs-lookup"><span data-stu-id="5560d-145">Netbios format of hello forest name currently being imported, for example FABRIKAMCORP</span></span> |
| <span data-ttu-id="5560d-146">Forest.FQDN</span><span class="sxs-lookup"><span data-stu-id="5560d-146">Forest.FQDN</span></span> |<span data-ttu-id="5560d-147">Şu anda alınmakta hello orman adı örneğin fabrikam.com FQDN biçimi</span><span class="sxs-lookup"><span data-stu-id="5560d-147">FQDN format of hello forest name currently being imported, for example fabrikam.com</span></span> |
| <span data-ttu-id="5560d-148">Forest.LDAP</span><span class="sxs-lookup"><span data-stu-id="5560d-148">Forest.LDAP</span></span> |<span data-ttu-id="5560d-149">LDAP adının biçimi şu anda alınmakta hello orman örneğin DC fabrikam, DC = com =</span><span class="sxs-lookup"><span data-stu-id="5560d-149">LDAP format of hello forest name currently being imported, for example DC=fabrikam,DC=com</span></span> |

<span data-ttu-id="5560d-150">Merhaba sistemidir hello parametresi kullanılan tooget hello hello bağlayıcı tanıtıcısı şu anda çalıştığı:</span><span class="sxs-lookup"><span data-stu-id="5560d-150">hello system provides hello following parameter, which is used tooget hello identifier of hello Connector currently running:</span></span>  
`Connector.ID`

<span data-ttu-id="5560d-151">Merhaba hello kullanıcının bulunduğu hello etki alanının NetBIOS adını hello meta veri deposu özniteliği etki alanı dolduran bir örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="5560d-151">Here is an example that populates hello metaverse attribute domain with hello netbios name of hello domain where hello user is located:</span></span>  
`domain` <- `%Domain.Netbios%`

### <a name="operators"></a><span data-ttu-id="5560d-152">İşleçler</span><span class="sxs-lookup"><span data-stu-id="5560d-152">Operators</span></span>
<span data-ttu-id="5560d-153">hello işleçleri aşağıdaki kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="5560d-153">hello following operators can be used:</span></span>

* <span data-ttu-id="5560d-154">**Karşılaştırma**: <, < =, <>, =, >, > =</span><span class="sxs-lookup"><span data-stu-id="5560d-154">**Comparison**: <, <=, <>, =, >, >=</span></span>
* <span data-ttu-id="5560d-155">**Matematik**: +, -, \*, -</span><span class="sxs-lookup"><span data-stu-id="5560d-155">**Mathematics**: +, -, \*, -</span></span>
* <span data-ttu-id="5560d-156">**Dize**: & (Birleştir)</span><span class="sxs-lookup"><span data-stu-id="5560d-156">**String**: & (concatenate)</span></span>
* <span data-ttu-id="5560d-157">**Mantıksal**: & & (ve) || (veya)</span><span class="sxs-lookup"><span data-stu-id="5560d-157">**Logical**: && (and), || (or)</span></span>
* <span data-ttu-id="5560d-158">**Değerlendirme sırası**:)</span><span class="sxs-lookup"><span data-stu-id="5560d-158">**Evaluation order**: ( )</span></span>

<span data-ttu-id="5560d-159">İşleçler değerlendirilen sol tooright ve hello aynı değerlendirme öncelik.</span><span class="sxs-lookup"><span data-stu-id="5560d-159">Operators are evaluated left tooright and have hello same evaluation priority.</span></span> <span data-ttu-id="5560d-160">Diğer bir deyişle, hello \* (çarpanı) (önce - çıkarma) değerlendirilmez.</span><span class="sxs-lookup"><span data-stu-id="5560d-160">That is, hello \* (multiplier) is not evaluated before - (subtraction).</span></span> <span data-ttu-id="5560d-161">2\*(5 + 3) olduğunu değil hello aynı 2 olarak\*5 + 3.</span><span class="sxs-lookup"><span data-stu-id="5560d-161">2\*(5+3) is not hello same as 2\*5+3.</span></span> <span data-ttu-id="5560d-162">Merhaba köşeli ayraçlar () kullanılan toochange hello değerlendirme sipariş bırakıldığına tooright değerlendirme sırası uygun değil.</span><span class="sxs-lookup"><span data-stu-id="5560d-162">hello brackets ( ) are used toochange hello evaluation order when left tooright evaluation order isn't appropriate.</span></span>

## <a name="multi-valued-attributes"></a><span data-ttu-id="5560d-163">Birden çok değerli öznitelikleri</span><span class="sxs-lookup"><span data-stu-id="5560d-163">Multi-valued attributes</span></span>
<span data-ttu-id="5560d-164">Merhaba işlevleri hem tek değerli ve birden çok değerli öznitelikleri üzerinde çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="5560d-164">hello functions can operate on both single-valued and multi-valued attributes.</span></span> <span data-ttu-id="5560d-165">Birden çok değerli öznitelikler için hello işlevi her değer çalışır ve hello geçerlidir tooevery değer ile aynı işlevi.</span><span class="sxs-lookup"><span data-stu-id="5560d-165">For multi-valued attributes, hello function operates over every value and applies hello same function tooevery value.</span></span>

<span data-ttu-id="5560d-166">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="5560d-166">For example:</span></span>  
<span data-ttu-id="5560d-167">`Trim([proxyAddresses])`Kırpma hello proxyAddress özniteliğinde her değerin yapın.</span><span class="sxs-lookup"><span data-stu-id="5560d-167">`Trim([proxyAddresses])` Do a Trim of every value in hello proxyAddress attribute.</span></span>  
<span data-ttu-id="5560d-168">`Word([proxyAddresses],1,"@") & "@contoso.com"`Her değere sahip bir @-sign, hello etki alanı ile Değiştir @contoso.com.</span><span class="sxs-lookup"><span data-stu-id="5560d-168">`Word([proxyAddresses],1,"@") & "@contoso.com"` For every value with an @-sign, replace hello domain with @contoso.com.</span></span>  
<span data-ttu-id="5560d-169">`IIF(InStr([proxyAddresses],"SIP:")=1,NULL,[proxyAddresses])`Merhaba SIP adresi arayın ve başlangıç değerleri kaldırın.</span><span class="sxs-lookup"><span data-stu-id="5560d-169">`IIF(InStr([proxyAddresses],"SIP:")=1,NULL,[proxyAddresses])` Look for hello SIP-address and remove it from hello values.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5560d-170">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5560d-170">Next steps</span></span>
* <span data-ttu-id="5560d-171">Merhaba yapılandırma modeli hakkında daha fazla bilgiyi [anlama bildirim temelli hazırlama](active-directory-aadconnectsync-understanding-declarative-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="5560d-171">Read more about hello configuration model in [Understanding Declarative Provisioning](active-directory-aadconnectsync-understanding-declarative-provisioning.md).</span></span>
* <span data-ttu-id="5560d-172">Bkz: nasıl bildirim temelli sağlama kullanılan out-of-box içinde olduğu [anlama hello varsayılan yapılandırma](active-directory-aadconnectsync-understanding-default-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="5560d-172">See how declarative provisioning is used out-of-box in [Understanding hello default configuration](active-directory-aadconnectsync-understanding-default-configuration.md).</span></span>
* <span data-ttu-id="5560d-173">Toomake bir pratik nasıl değiştiğini içinde bildirim temelli hazırlama kullanarak görmek [nasıl toomake değişiklik toohello varsayılan yapılandırması](active-directory-aadconnectsync-change-the-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="5560d-173">See how toomake a practical change using declarative provisioning in [How toomake a change toohello default configuration](active-directory-aadconnectsync-change-the-configuration.md).</span></span>

<span data-ttu-id="5560d-174">**Genel bakış konuları**</span><span class="sxs-lookup"><span data-stu-id="5560d-174">**Overview topics**</span></span>

* [<span data-ttu-id="5560d-175">Azure AD Connect eşitleme: anlamak ve eşitleme özelleştirme</span><span class="sxs-lookup"><span data-stu-id="5560d-175">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="5560d-176">Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="5560d-176">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)

<span data-ttu-id="5560d-177">**Başvuru konuları**</span><span class="sxs-lookup"><span data-stu-id="5560d-177">**Reference topics**</span></span>

* [<span data-ttu-id="5560d-178">Azure AD Connect eşitleme: işlevleri başvurusu</span><span class="sxs-lookup"><span data-stu-id="5560d-178">Azure AD Connect sync: Functions Reference</span></span>](active-directory-aadconnectsync-functions-reference.md)

