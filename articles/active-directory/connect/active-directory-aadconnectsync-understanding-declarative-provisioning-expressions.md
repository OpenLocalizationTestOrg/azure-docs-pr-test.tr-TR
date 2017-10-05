---
title: "Azure AD Connect: Bildirim temelli hazırlama ifadelerini | Microsoft Docs"
description: "Bildirim temelli hazırlama ifadelerini açıklanmaktadır."
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
ms.openlocfilehash: e3a03a97b10e04fb85261620879b2102e1db8465
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-understanding-declarative-provisioning-expressions"></a><span data-ttu-id="f8df7-103">Azure AD Connect eşitleme: bildirim temelli hazırlama ifadeleri anlama</span><span class="sxs-lookup"><span data-stu-id="f8df7-103">Azure AD Connect sync: Understanding Declarative Provisioning Expressions</span></span>
<span data-ttu-id="f8df7-104">Azure AD Connect eşitleme ilk Forefront Identity Manager 2010'da sunulan bildirim temelli hazırlama üzerinde oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f8df7-104">Azure AD Connect sync builds on declarative provisioning first introduced in Forefront Identity Manager 2010.</span></span> <span data-ttu-id="f8df7-105">Derlenmiş kod yazmak zorunda kalmadan, tam kimlik tümleştirme iş mantığı uygulamanız imkan tanır.</span><span class="sxs-lookup"><span data-stu-id="f8df7-105">It allows you to implement your complete identity integration business logic without the need to write compiled code.</span></span>

<span data-ttu-id="f8df7-106">Öznitelik akışlarında kullanılan ifade dili bildirim temelli hazırlama, önemli bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="f8df7-106">An essential part of declarative provisioning is the expression language used in attribute flows.</span></span> <span data-ttu-id="f8df7-107">Kullanılan dili, Microsoft® Visual Basic® for Applications (VBA) bir alt kümesidir.</span><span class="sxs-lookup"><span data-stu-id="f8df7-107">The language used is a subset of Microsoft® Visual Basic® for Applications (VBA).</span></span> <span data-ttu-id="f8df7-108">Bu dil Microsoft Office'de kullanılır ve VBScript deneyimi olan kullanıcılar da onu tanımaz.</span><span class="sxs-lookup"><span data-stu-id="f8df7-108">This language is used in Microsoft Office and users with experience of VBScript will also recognize it.</span></span> <span data-ttu-id="f8df7-109">Bildirim temelli hazırlama ifade dili yalnızca işlevler kullanılarak ve yapılandırılmış bir dil değil.</span><span class="sxs-lookup"><span data-stu-id="f8df7-109">The Declarative Provisioning Expression Language is only using functions and is not a structured language.</span></span> <span data-ttu-id="f8df7-110">Yöntemleri veya deyimleri yok.</span><span class="sxs-lookup"><span data-stu-id="f8df7-110">There are no methods or statements.</span></span> <span data-ttu-id="f8df7-111">Express program akışı işlevleri yerine iç içe.</span><span class="sxs-lookup"><span data-stu-id="f8df7-111">Functions are instead nested to express program flow.</span></span>

<span data-ttu-id="f8df7-112">Daha fazla ayrıntı için bkz: ['na Hoş Geldiniz Office 2013 için dil başvurusu uygulamalar için Visual Basic](https://msdn.microsoft.com/library/gg264383.aspx).</span><span class="sxs-lookup"><span data-stu-id="f8df7-112">For more details, see [Welcome to the Visual Basic for Applications language reference for Office 2013](https://msdn.microsoft.com/library/gg264383.aspx).</span></span>

<span data-ttu-id="f8df7-113">Öznitelikleri kesin türü belirtilmiş.</span><span class="sxs-lookup"><span data-stu-id="f8df7-113">The attributes are strongly typed.</span></span> <span data-ttu-id="f8df7-114">Bir işlev yalnızca doğru türde öznitelikleri kabul eder.</span><span class="sxs-lookup"><span data-stu-id="f8df7-114">A function only accepts attributes of the correct type.</span></span> <span data-ttu-id="f8df7-115">Ayrıca, büyük küçük harfe duyarlı değildir.</span><span class="sxs-lookup"><span data-stu-id="f8df7-115">It is also case-sensitive.</span></span> <span data-ttu-id="f8df7-116">Bir hata oluşturulur veya işlev adları ve öznitelik adları doğru büyük/küçük harf olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f8df7-116">Both function names and attribute names must have proper casing or an error is thrown.</span></span>

## <a name="language-definitions-and-identifiers"></a><span data-ttu-id="f8df7-117">Dil tanımları ve tanımlayıcıları</span><span class="sxs-lookup"><span data-stu-id="f8df7-117">Language definitions and Identifiers</span></span>
* <span data-ttu-id="f8df7-118">İşlev bağımsız değişkenleri köşeli adından sonra sahip: FunctionName (1 bağımsız değişkeni, değişken N).</span><span class="sxs-lookup"><span data-stu-id="f8df7-118">Functions have a name followed by arguments in brackets: FunctionName(argument 1, argument N).</span></span>
* <span data-ttu-id="f8df7-119">Öznitelikleri köşeli tarafından tanımlanır: [attributeName]</span><span class="sxs-lookup"><span data-stu-id="f8df7-119">Attributes are identified by square brackets: [attributeName]</span></span>
* <span data-ttu-id="f8df7-120">Parametreleri yüzde işaretleri tarafından tanımlanır: % ParameterName %</span><span class="sxs-lookup"><span data-stu-id="f8df7-120">Parameters are identified by percent signs: %ParameterName%</span></span>
* <span data-ttu-id="f8df7-121">Dize sabitleri tırnak içine alınmış: Örneğin, "Contoso" (Not: düz tırnak işaretleri kullanmanız gerekir "" tırnak akıllı değil ve "")</span><span class="sxs-lookup"><span data-stu-id="f8df7-121">String constants are surrounded by quotes: For example, "Contoso" (Note: must use straight quotes "" and not smart quotes “”)</span></span>
* <span data-ttu-id="f8df7-122">Sayısal değerler tırnak işaretleri olmadan ifade ve ondalık olması bekleniyor.</span><span class="sxs-lookup"><span data-stu-id="f8df7-122">Numeric values are expressed without quotes and expected to be decimal.</span></span> <span data-ttu-id="f8df7-123">Onaltılık değerler öneki ile & H.</span><span class="sxs-lookup"><span data-stu-id="f8df7-123">Hexadecimal values are prefixed with &H.</span></span> <span data-ttu-id="f8df7-124">Örneğin, 98052 & HFF</span><span class="sxs-lookup"><span data-stu-id="f8df7-124">For example, 98052, &HFF</span></span>
* <span data-ttu-id="f8df7-125">Boole değerleri sabitler ile ifade edilir: True, False.</span><span class="sxs-lookup"><span data-stu-id="f8df7-125">Boolean values are expressed with constants: True, False.</span></span>
* <span data-ttu-id="f8df7-126">Yerleşik sabit ve değişmez değerleri yalnızca kendi adı ile ifade edilir: NULL, CRLF, IgnoreThisFlow</span><span class="sxs-lookup"><span data-stu-id="f8df7-126">Built-in constants and literals are expressed with only their name: NULL, CRLF, IgnoreThisFlow</span></span>

### <a name="functions"></a><span data-ttu-id="f8df7-127">İşlevler</span><span class="sxs-lookup"><span data-stu-id="f8df7-127">Functions</span></span>
<span data-ttu-id="f8df7-128">Bildirim temelli hazırlama, öznitelik değerleri dönüştürme etme olanağını etkinleştirmek için birçok işlevini kullanır.</span><span class="sxs-lookup"><span data-stu-id="f8df7-128">Declarative provisioning uses many functions to enable the possibility to transform attribute values.</span></span> <span data-ttu-id="f8df7-129">Bir işlevin sonuç başka bir işleve geçirilen şekilde bu işlevleri iç içe.</span><span class="sxs-lookup"><span data-stu-id="f8df7-129">These functions can be nested so the result from one function is passed in to another function.</span></span>

`Function1(Function2(Function3()))`

<span data-ttu-id="f8df7-130">İşlevlerin tam listesi bulunabilir [işlev başvurusu](active-directory-aadconnectsync-functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="f8df7-130">The complete list of functions can be found in the [function reference](active-directory-aadconnectsync-functions-reference.md).</span></span>

### <a name="parameters"></a><span data-ttu-id="f8df7-131">Parametreler</span><span class="sxs-lookup"><span data-stu-id="f8df7-131">Parameters</span></span>
<span data-ttu-id="f8df7-132">Bir parametre bir bağlayıcı veya PowerShell kullanan bir yönetici tarafından tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="f8df7-132">A parameter is defined either by a Connector or by an administrator using PowerShell.</span></span> <span data-ttu-id="f8df7-133">Parametreler genellikle sistem için farklı değerler içeren, örneğin, kullanıcı etki alanı adı bulunur.</span><span class="sxs-lookup"><span data-stu-id="f8df7-133">Parameters usually contain values that are different from system to system, for example the name of the domain the user is located in.</span></span> <span data-ttu-id="f8df7-134">Bu parametreler öznitelik akışları kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f8df7-134">These parameters can be used in attribute flows.</span></span>

<span data-ttu-id="f8df7-135">Active Directory Bağlayıcısı gelen eşitleme kuralları için aşağıdaki parametreleri sağlanan:</span><span class="sxs-lookup"><span data-stu-id="f8df7-135">The Active Directory Connector provided the following parameters for inbound Synchronization Rules:</span></span>

| <span data-ttu-id="f8df7-136">Parametre Adı</span><span class="sxs-lookup"><span data-stu-id="f8df7-136">Parameter Name</span></span> | <span data-ttu-id="f8df7-137">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f8df7-137">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="f8df7-138">Domain.Netbios</span><span class="sxs-lookup"><span data-stu-id="f8df7-138">Domain.Netbios</span></span> |<span data-ttu-id="f8df7-139">Şu anda alınmakta, örneğin FABRIKAMSALES etki alanının NetBIOS biçimi</span><span class="sxs-lookup"><span data-stu-id="f8df7-139">Netbios format of the domain currently being imported, for example FABRIKAMSALES</span></span> |
| <span data-ttu-id="f8df7-140">Domain.FQDN</span><span class="sxs-lookup"><span data-stu-id="f8df7-140">Domain.FQDN</span></span> |<span data-ttu-id="f8df7-141">Şu anda içeri aktarılmakta olan, etki alanı örneğin sales.fabrikam.com FQDN biçimi</span><span class="sxs-lookup"><span data-stu-id="f8df7-141">FQDN format of the domain currently being imported, for example sales.fabrikam.com</span></span> |
| <span data-ttu-id="f8df7-142">Domain.LDAP</span><span class="sxs-lookup"><span data-stu-id="f8df7-142">Domain.LDAP</span></span> |<span data-ttu-id="f8df7-143">Şu anda içeri aktarılmakta olan, etki alanı örneğin DC LDAP biçimi Satışlar, DC = fabrikam, DC = com =</span><span class="sxs-lookup"><span data-stu-id="f8df7-143">LDAP format of the domain currently being imported, for example DC=sales,DC=fabrikam,DC=com</span></span> |
| <span data-ttu-id="f8df7-144">Forest.Netbios</span><span class="sxs-lookup"><span data-stu-id="f8df7-144">Forest.Netbios</span></span> |<span data-ttu-id="f8df7-145">NetBIOS adının biçimi şu anda alınmakta orman örneğin FABRIKAMCORP</span><span class="sxs-lookup"><span data-stu-id="f8df7-145">Netbios format of the forest name currently being imported, for example FABRIKAMCORP</span></span> |
| <span data-ttu-id="f8df7-146">Forest.FQDN</span><span class="sxs-lookup"><span data-stu-id="f8df7-146">Forest.FQDN</span></span> |<span data-ttu-id="f8df7-147">Şu anda alınmakta orman adının örneğin fabrikam.com FQDN biçimi</span><span class="sxs-lookup"><span data-stu-id="f8df7-147">FQDN format of the forest name currently being imported, for example fabrikam.com</span></span> |
| <span data-ttu-id="f8df7-148">Forest.LDAP</span><span class="sxs-lookup"><span data-stu-id="f8df7-148">Forest.LDAP</span></span> |<span data-ttu-id="f8df7-149">Şu anda alınmakta orman adının örneğin DC LDAP biçimi fabrikam, DC = com =</span><span class="sxs-lookup"><span data-stu-id="f8df7-149">LDAP format of the forest name currently being imported, for example DC=fabrikam,DC=com</span></span> |

<span data-ttu-id="f8df7-150">Sistem şu anda çalışan bağlayıcı tanıtıcısı almak için kullanılan aşağıdaki parametre sağlar:</span><span class="sxs-lookup"><span data-stu-id="f8df7-150">The system provides the following parameter, which is used to get the identifier of the Connector currently running:</span></span>  
`Connector.ID`

<span data-ttu-id="f8df7-151">Aşağıda, kullanıcının bulunduğu etki alanının NetBIOS adı ile meta veri deposu özniteliği etki alanı dolduran bir örnek verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="f8df7-151">Here is an example that populates the metaverse attribute domain with the netbios name of the domain where the user is located:</span></span>  
`domain` <- `%Domain.Netbios%`

### <a name="operators"></a><span data-ttu-id="f8df7-152">İşleçler</span><span class="sxs-lookup"><span data-stu-id="f8df7-152">Operators</span></span>
<span data-ttu-id="f8df7-153">Aşağıdaki işleçleri kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="f8df7-153">The following operators can be used:</span></span>

* <span data-ttu-id="f8df7-154">**Karşılaştırma**: <, < =, <>, =, >, > =</span><span class="sxs-lookup"><span data-stu-id="f8df7-154">**Comparison**: <, <=, <>, =, >, >=</span></span>
* <span data-ttu-id="f8df7-155">**Matematik**: +, -, \*, -</span><span class="sxs-lookup"><span data-stu-id="f8df7-155">**Mathematics**: +, -, \*, -</span></span>
* <span data-ttu-id="f8df7-156">**Dize**: & (Birleştir)</span><span class="sxs-lookup"><span data-stu-id="f8df7-156">**String**: & (concatenate)</span></span>
* <span data-ttu-id="f8df7-157">**Mantıksal**: & & (ve) || (veya)</span><span class="sxs-lookup"><span data-stu-id="f8df7-157">**Logical**: && (and), || (or)</span></span>
* <span data-ttu-id="f8df7-158">**Değerlendirme sırası**:)</span><span class="sxs-lookup"><span data-stu-id="f8df7-158">**Evaluation order**: ( )</span></span>

<span data-ttu-id="f8df7-159">İşleçler soldan sağa değerlendirilir ve aynı değerlendirme önceliğe sahip.</span><span class="sxs-lookup"><span data-stu-id="f8df7-159">Operators are evaluated left to right and have the same evaluation priority.</span></span> <span data-ttu-id="f8df7-160">Diğer bir deyişle, \* (çarpanı) (önce - çıkarma) değerlendirilmez.</span><span class="sxs-lookup"><span data-stu-id="f8df7-160">That is, the \* (multiplier) is not evaluated before - (subtraction).</span></span> <span data-ttu-id="f8df7-161">2\*(5 + 3) 2 ile aynı değil\*5 + 3.</span><span class="sxs-lookup"><span data-stu-id="f8df7-161">2\*(5+3) is not the same as 2\*5+3.</span></span> <span data-ttu-id="f8df7-162">Köşeli ayraçlar () sağ değerlendirme sırası sola uygun olmadığı durumlarda Değerlendirme sırasını değiştirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f8df7-162">The brackets ( ) are used to change the evaluation order when left to right evaluation order isn't appropriate.</span></span>

## <a name="multi-valued-attributes"></a><span data-ttu-id="f8df7-163">Birden çok değerli öznitelikleri</span><span class="sxs-lookup"><span data-stu-id="f8df7-163">Multi-valued attributes</span></span>
<span data-ttu-id="f8df7-164">İşlevler, hem tek değerli ve birden çok değerli öznitelikleri üzerinde çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="f8df7-164">The functions can operate on both single-valued and multi-valued attributes.</span></span> <span data-ttu-id="f8df7-165">Birden çok değerli öznitelikler, işlevi her değer çalışır ve her değere aynı işlevi uygular.</span><span class="sxs-lookup"><span data-stu-id="f8df7-165">For multi-valued attributes, the function operates over every value and applies the same function to every value.</span></span>

<span data-ttu-id="f8df7-166">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="f8df7-166">For example:</span></span>  
<span data-ttu-id="f8df7-167">`Trim([proxyAddresses])`Kırpma proxyAddress özniteliğinde her değerin yapın.</span><span class="sxs-lookup"><span data-stu-id="f8df7-167">`Trim([proxyAddresses])` Do a Trim of every value in the proxyAddress attribute.</span></span>  
<span data-ttu-id="f8df7-168">`Word([proxyAddresses],1,"@") & "@contoso.com"`Her değere sahip bir @-sign, etki alanı ile Değiştir @contoso.com.</span><span class="sxs-lookup"><span data-stu-id="f8df7-168">`Word([proxyAddresses],1,"@") & "@contoso.com"` For every value with an @-sign, replace the domain with @contoso.com.</span></span>  
<span data-ttu-id="f8df7-169">`IIF(InStr([proxyAddresses],"SIP:")=1,NULL,[proxyAddresses])`SIP-adresini bakın ve değerleri kaldırın.</span><span class="sxs-lookup"><span data-stu-id="f8df7-169">`IIF(InStr([proxyAddresses],"SIP:")=1,NULL,[proxyAddresses])` Look for the SIP-address and remove it from the values.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f8df7-170">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f8df7-170">Next steps</span></span>
* <span data-ttu-id="f8df7-171">Yapılandırma modeli hakkında daha fazla bilgiyi [anlama bildirim temelli hazırlama](active-directory-aadconnectsync-understanding-declarative-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="f8df7-171">Read more about the configuration model in [Understanding Declarative Provisioning](active-directory-aadconnectsync-understanding-declarative-provisioning.md).</span></span>
* <span data-ttu-id="f8df7-172">Bkz: nasıl bildirim temelli hazırlama kullanılan out-of-box içinde olduğu [varsayılan yapılandırmayı anlama](active-directory-aadconnectsync-understanding-default-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="f8df7-172">See how declarative provisioning is used out-of-box in [Understanding the default configuration](active-directory-aadconnectsync-understanding-default-configuration.md).</span></span>
* <span data-ttu-id="f8df7-173">Bkz. bildirim temelli sağlamayı kullanarak pratik değişiklik yapmak [varsayılan yapılandırması ile değişiklik yapmak nasıl](active-directory-aadconnectsync-change-the-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="f8df7-173">See how to make a practical change using declarative provisioning in [How to make a change to the default configuration](active-directory-aadconnectsync-change-the-configuration.md).</span></span>

<span data-ttu-id="f8df7-174">**Genel bakış konuları**</span><span class="sxs-lookup"><span data-stu-id="f8df7-174">**Overview topics**</span></span>

* [<span data-ttu-id="f8df7-175">Azure AD Connect eşitleme: anlamak ve eşitleme özelleştirme</span><span class="sxs-lookup"><span data-stu-id="f8df7-175">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="f8df7-176">Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="f8df7-176">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)

<span data-ttu-id="f8df7-177">**Başvuru konuları**</span><span class="sxs-lookup"><span data-stu-id="f8df7-177">**Reference topics**</span></span>

* [<span data-ttu-id="f8df7-178">Azure AD Connect eşitleme: işlevleri başvurusu</span><span class="sxs-lookup"><span data-stu-id="f8df7-178">Azure AD Connect sync: Functions Reference</span></span>](active-directory-aadconnectsync-functions-reference.md)

