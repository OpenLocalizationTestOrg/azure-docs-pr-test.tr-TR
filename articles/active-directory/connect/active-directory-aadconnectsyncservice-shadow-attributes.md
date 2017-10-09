---
title: "aaaAzure AD Connect eşitleme hizmeti gölge öznitelikleri | Microsoft Docs"
description: "Gölge öznitelikler Azure AD Connect eşitleme hizmetinin nasıl çalıştığı açıklanmaktadır."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 1b8665e7488c6078b655f8a3e35519145bacd898
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-service-shadow-attributes"></a><span data-ttu-id="7fc34-103">Azure AD Connect eşitleme hizmeti gölge öznitelikleri</span><span class="sxs-lookup"><span data-stu-id="7fc34-103">Azure AD Connect sync service shadow attributes</span></span>
<span data-ttu-id="7fc34-104">Çoğu öznitelikleri temsil aynı yolla da hello Azure AD, şirket içi Active Directory'de oldukları gibi.</span><span class="sxs-lookup"><span data-stu-id="7fc34-104">Most attributes are represented hello same way in Azure AD as they are in your on-premises Active Directory.</span></span> <span data-ttu-id="7fc34-105">Ancak bazı özel işleme bazı özniteliklere sahip ve Azure AD hello öznitelik değeri Azure AD Connect eşitler daha farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="7fc34-105">But some attributes have some special handling and hello attribute value in Azure AD might be different than what Azure AD Connect synchronizes.</span></span>

## <a name="introducing-shadow-attributes"></a><span data-ttu-id="7fc34-106">Gölge öznitelikleri Tanıtımı</span><span class="sxs-lookup"><span data-stu-id="7fc34-106">Introducing shadow attributes</span></span>
<span data-ttu-id="7fc34-107">Bazı öznitelikler Azure AD içinde iki sunumu sahiptir.</span><span class="sxs-lookup"><span data-stu-id="7fc34-107">Some attributes have two representations in Azure AD.</span></span> <span data-ttu-id="7fc34-108">Merhaba şirket içi değer ve bir hesaplanan değer depolanır.</span><span class="sxs-lookup"><span data-stu-id="7fc34-108">Both hello on-premises value and a calculated value are stored.</span></span> <span data-ttu-id="7fc34-109">Bu ek öznitelikler gölge öznitelikleri denir.</span><span class="sxs-lookup"><span data-stu-id="7fc34-109">These extra attributes are called shadow attributes.</span></span> <span data-ttu-id="7fc34-110">Bu davranış gördüğünüz hello iki en yaygın öznitelikleri **userPrincipalName** ve **proxyAddress**.</span><span class="sxs-lookup"><span data-stu-id="7fc34-110">hello two most common attributes where you see this behavior are **userPrincipalName** and **proxyAddress**.</span></span> <span data-ttu-id="7fc34-111">doğrulanmamış etki alanları temsil eden içinde bu özniteliklerin değerleri olduğunda öznitelik değerleri hello değişiklik olur.</span><span class="sxs-lookup"><span data-stu-id="7fc34-111">hello change in attribute values happens when there are values in these attributes representing non-verified domains.</span></span> <span data-ttu-id="7fc34-112">Ancak hello eşitleme altyapısı Bağlan hello değerini hello gölge özniteliğinde bunu kendi açısından okur, hello özniteliği Azure AD tarafından onaylanmıştır.</span><span class="sxs-lookup"><span data-stu-id="7fc34-112">But hello sync engine in Connect reads hello value in hello shadow attribute so from its perspective, hello attribute has been confirmed by Azure AD.</span></span>

<span data-ttu-id="7fc34-113">Hello Azure portal veya PowerShell ile kullanarak hello gölge özniteliklerini göremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="7fc34-113">You cannot see hello shadow attributes using hello Azure portal or with PowerShell.</span></span> <span data-ttu-id="7fc34-114">Ancak anlama hello kavram, tootroubleshoot belirli senaryolar farklı değerler şirket içi hello özniteliğine sahip olduğunda ve hello bulutta yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="7fc34-114">But understanding hello concept helps you tootroubleshoot certain scenarios where hello attribute has different values on-premises and in hello cloud.</span></span>

<span data-ttu-id="7fc34-115">toobetter hello davranışlarını anlamak, Fabrikam bu örnekten bakın:</span><span class="sxs-lookup"><span data-stu-id="7fc34-115">toobetter understand hello behavior, look at this example from Fabrikam:</span></span>  
![Etki Alanları](./media/active-directory-aadconnectsyncservice-shadow-attributes/domains.png)  
<span data-ttu-id="7fc34-117">Kendi şirket içi Active Directory'de birden çok UPN soneki olabilirler, ancak bunlar yalnızca biri doğruladıktan.</span><span class="sxs-lookup"><span data-stu-id="7fc34-117">They have multiple UPN suffixes in their on-premises Active Directory, but they have only verified one.</span></span>

### <a name="userprincipalname"></a><span data-ttu-id="7fc34-118">userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="7fc34-118">userPrincipalName</span></span>
<span data-ttu-id="7fc34-119">Bir kullanıcının öznitelik değerleri doğrulanmamış bir etki alanında aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="7fc34-119">A user has hello following attribute values in a non-verified domain:</span></span>

| <span data-ttu-id="7fc34-120">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="7fc34-120">Attribute</span></span> | <span data-ttu-id="7fc34-121">Değer</span><span class="sxs-lookup"><span data-stu-id="7fc34-121">Value</span></span> |
| --- | --- |
| <span data-ttu-id="7fc34-122">Şirket içi userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="7fc34-122">on-premises userPrincipalName</span></span> | lee.sperry@fabrikam.com |
| <span data-ttu-id="7fc34-123">Azure AD shadowUserPrincipalName</span><span class="sxs-lookup"><span data-stu-id="7fc34-123">Azure AD shadowUserPrincipalName</span></span> | lee.sperry@fabrikam.com |
| <span data-ttu-id="7fc34-124">Azure AD userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="7fc34-124">Azure AD userPrincipalName</span></span> | lee.sperry@fabrikam.onmicrosoft.com |

<span data-ttu-id="7fc34-125">Merhaba userPrincipalName özniteliği, PowerShell kullanırken gördüğünüz hello değerdir.</span><span class="sxs-lookup"><span data-stu-id="7fc34-125">hello userPrincipalName attribute is hello value you see when using PowerShell.</span></span>

<span data-ttu-id="7fc34-126">Azure AD hello userPrincipalName özniteliği Hello gerçek şirket içi öznitelik değeri zaman hello fabrikam.com etki alanını doğrulayın, Azure AD içinde kaydedildiği hello shadowUserPrincipalName başlangıç değerinden ile güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="7fc34-126">Since hello real on-premises attribute value is stored in Azure AD, when you verify hello fabrikam.com domain, Azure AD updates hello userPrincipalName attribute with hello value from hello shadowUserPrincipalName.</span></span> <span data-ttu-id="7fc34-127">Güncelleştirilmiş bu değerleri toobe için Azure AD Connect değişiklikleri toosynchronize sahip değil.</span><span class="sxs-lookup"><span data-stu-id="7fc34-127">You do not have toosynchronize any changes from Azure AD Connect for these values toobe updated.</span></span>

### <a name="proxyaddresses"></a><span data-ttu-id="7fc34-128">proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="7fc34-128">proxyAddresses</span></span>
<span data-ttu-id="7fc34-129">Merhaba yalnızca doğrulanmış etki alanlarını dahil etmek için aynı işlemi proxyAddresses, ancak bazı ilave bir mantık daha da oluşur.</span><span class="sxs-lookup"><span data-stu-id="7fc34-129">hello same process for only including verified domains also occurs for proxyAddresses, but with some additional logic.</span></span> <span data-ttu-id="7fc34-130">doğrulanmış etki alanları için Hello onay yalnızca posta kutusu kullanıcılar için gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="7fc34-130">hello check for verified domains only happens for mailbox users.</span></span> <span data-ttu-id="7fc34-131">Bir posta etkin bir kullanıcıya veya kişi temsil eden bir kullanıcı başka bir Exchange kuruluşunda ve proxyAddresses toothese nesnelerindeki değerleri ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7fc34-131">A mail-enabled user or contact represent a user in another Exchange organization and you can add any values in proxyAddresses toothese objects.</span></span>

<span data-ttu-id="7fc34-132">Her iki şirket içi posta kutusu bir kullanıcı için ya da Exchange Online'da yalnızca değerleri doğrulanmış etki alanları için görünür.</span><span class="sxs-lookup"><span data-stu-id="7fc34-132">For a mailbox user, either on-premises or in Exchange Online, only values for verified domains appear.</span></span> <span data-ttu-id="7fc34-133">Şu şekilde görünebilir:</span><span class="sxs-lookup"><span data-stu-id="7fc34-133">It could look like this:</span></span>

| <span data-ttu-id="7fc34-134">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="7fc34-134">Attribute</span></span> | <span data-ttu-id="7fc34-135">Değer</span><span class="sxs-lookup"><span data-stu-id="7fc34-135">Value</span></span> |
| --- | --- |
| <span data-ttu-id="7fc34-136">Şirket içi proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="7fc34-136">on-premises proxyAddresses</span></span> | SMTP:abbie.spencer@fabrikamonline.com</br>smtp:abbie.spencer@fabrikam.com</br>smtp:abbie@fabrikamonline.com |
| <span data-ttu-id="7fc34-137">Exchange Online proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="7fc34-137">Exchange Online proxyAddresses</span></span> | SMTP:abbie.spencer@fabrikamonline.com</br>smtp:abbie@fabrikamonline.com</br>SIP:abbie.spencer@fabrikamonline.com |

<span data-ttu-id="7fc34-138">Bu durumda  **smtp:abbie.spencer@fabrikam.com**  bu etki alanı doğrulanmadı beri kaldırıldı.</span><span class="sxs-lookup"><span data-stu-id="7fc34-138">In this case **smtp:abbie.spencer@fabrikam.com** was removed since that domain has not been verified.</span></span> <span data-ttu-id="7fc34-139">Ancak aynı zamanda eklenen Exchange  **SIP:abbie.spencer@fabrikamonline.com** . Fabrikam Lync/Skype şirket içi ancak Azure AD kullanmamış ve Exchange Online hazırlamak için.</span><span class="sxs-lookup"><span data-stu-id="7fc34-139">But Exchange also added **SIP:abbie.spencer@fabrikamonline.com**. Fabrikam has not used Lync/Skype on-premises, but Azure AD and Exchange Online prepare for it.</span></span>

<span data-ttu-id="7fc34-140">Başvurulan tooas proxyAddresses için bu mantığı olan **ProxyCalc**.</span><span class="sxs-lookup"><span data-stu-id="7fc34-140">This logic for proxyAddresses is referred tooas **ProxyCalc**.</span></span> <span data-ttu-id="7fc34-141">ProxyCalc her değişikliğe bir kullanıcı olarak çağrılan zaman:</span><span class="sxs-lookup"><span data-stu-id="7fc34-141">ProxyCalc is invoked with every change on a user when:</span></span>

- <span data-ttu-id="7fc34-142">Merhaba kullanıcı hello kullanıcının Exchange için lisanslı değil olsa bile Exchange Online içeren bir hizmet planına atanmıştır.</span><span class="sxs-lookup"><span data-stu-id="7fc34-142">hello user has been assigned a service plan that includes Exchange Online even if hello user was not licensed for Exchange.</span></span> <span data-ttu-id="7fc34-143">Örneğin, hello kullanıcı atanmışsa Office E3 SKU Merhaba, ancak yalnızca SharePoint Online atanmadı.</span><span class="sxs-lookup"><span data-stu-id="7fc34-143">For example, if hello user is assigned hello Office E3 SKU, but only was assigned SharePoint Online.</span></span> <span data-ttu-id="7fc34-144">Posta hala şirket içi olsa bile bu geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="7fc34-144">This is true even if your mailbox is still on-premises.</span></span>
- <span data-ttu-id="7fc34-145">Merhaba özniteliği msExchRecipientTypeDetails bir değer içeriyor.</span><span class="sxs-lookup"><span data-stu-id="7fc34-145">hello attribute msExchRecipientTypeDetails has a value.</span></span>
- <span data-ttu-id="7fc34-146">Bir değişiklik tooproxyAddresses veya userPrincipalName olun.</span><span class="sxs-lookup"><span data-stu-id="7fc34-146">You make a change tooproxyAddresses or userPrincipalName.</span></span>

<span data-ttu-id="7fc34-147">ProxyCalc bazı zaman tooprocess bir kullanıcı bir değişiklik alabilir ve hello Azure AD Connect dışarı aktarma işlemine zaman uyumlu değil.</span><span class="sxs-lookup"><span data-stu-id="7fc34-147">ProxyCalc might take some time tooprocess a change on a user and is not synchronous with hello Azure AD Connect export process.</span></span>

> [!NOTE]
> <span data-ttu-id="7fc34-148">Bu konudaki belgelenmemiş Gelişmiş senaryolar için bazı ek davranışları Hello ProxyCalc mantığı vardır.</span><span class="sxs-lookup"><span data-stu-id="7fc34-148">hello ProxyCalc logic has some additional behaviors for advanced scenarios not documented in this topic.</span></span> <span data-ttu-id="7fc34-149">Bu konu, toounderstand davranışı hello ve tüm İç mantık belge değil sağlanır.</span><span class="sxs-lookup"><span data-stu-id="7fc34-149">This topic is provided for you toounderstand hello behavior and not document all internal logic.</span></span>

### <a name="quarantined-attribute-values"></a><span data-ttu-id="7fc34-150">Karantinaya alınan öznitelik değerleri</span><span class="sxs-lookup"><span data-stu-id="7fc34-150">Quarantined attribute values</span></span>
<span data-ttu-id="7fc34-151">Yinelenen öznitelik değerleri olduğunda gölge öznitelikler de kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7fc34-151">Shadow attributes are also used when there are duplicate attribute values.</span></span> <span data-ttu-id="7fc34-152">Daha fazla bilgi için bkz: [yinelenen öznitelik dayanıklılık](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span><span class="sxs-lookup"><span data-stu-id="7fc34-152">For more information, see [duplicate attribute resiliency](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="7fc34-153">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="7fc34-153">See also</span></span>
* [<span data-ttu-id="7fc34-154">Azure AD Connect eşitleme</span><span class="sxs-lookup"><span data-stu-id="7fc34-154">Azure AD Connect sync</span></span>](active-directory-aadconnectsync-whatis.md)
* <span data-ttu-id="7fc34-155">[Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="7fc34-155">[Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
