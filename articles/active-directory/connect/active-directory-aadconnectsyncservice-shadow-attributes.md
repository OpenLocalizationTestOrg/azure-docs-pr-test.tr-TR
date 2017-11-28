---
title: "Azure AD Connect eşitleme hizmeti gölge öznitelikleri | Microsoft Docs"
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
ms.openlocfilehash: 0b6a7f22d744480a40a878c979986cdd7667109c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-service-shadow-attributes"></a><span data-ttu-id="23a5b-103">Azure AD Connect eşitleme hizmeti gölge öznitelikleri</span><span class="sxs-lookup"><span data-stu-id="23a5b-103">Azure AD Connect sync service shadow attributes</span></span>
<span data-ttu-id="23a5b-104">Şirket içi Active Directory oldukları gibi özelliklerin çoğu Azure AD'de aynı şekilde gösterilir.</span><span class="sxs-lookup"><span data-stu-id="23a5b-104">Most attributes are represented the same way in Azure AD as they are in your on-premises Active Directory.</span></span> <span data-ttu-id="23a5b-105">Ancak bazı özel işleme bazı özniteliklere sahip ve Azure AD öznitelik değerinde Azure AD Connect eşitler daha farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="23a5b-105">But some attributes have some special handling and the attribute value in Azure AD might be different than what Azure AD Connect synchronizes.</span></span>

## <a name="introducing-shadow-attributes"></a><span data-ttu-id="23a5b-106">Gölge öznitelikleri Tanıtımı</span><span class="sxs-lookup"><span data-stu-id="23a5b-106">Introducing shadow attributes</span></span>
<span data-ttu-id="23a5b-107">Bazı öznitelikler Azure AD içinde iki sunumu sahiptir.</span><span class="sxs-lookup"><span data-stu-id="23a5b-107">Some attributes have two representations in Azure AD.</span></span> <span data-ttu-id="23a5b-108">Şirket içi değer ve bir hesaplanan değer depolanır.</span><span class="sxs-lookup"><span data-stu-id="23a5b-108">Both the on-premises value and a calculated value are stored.</span></span> <span data-ttu-id="23a5b-109">Bu ek öznitelikler gölge öznitelikleri denir.</span><span class="sxs-lookup"><span data-stu-id="23a5b-109">These extra attributes are called shadow attributes.</span></span> <span data-ttu-id="23a5b-110">Bu davranış gördüğünüz iki en yaygın öznitelikleri **userPrincipalName** ve **proxyAddress**.</span><span class="sxs-lookup"><span data-stu-id="23a5b-110">The two most common attributes where you see this behavior are **userPrincipalName** and **proxyAddress**.</span></span> <span data-ttu-id="23a5b-111">Doğrulanmamış etki alanları temsil eden içinde bu özniteliklerin değerleri olduğunda öznitelik değerleri değişikliği olur.</span><span class="sxs-lookup"><span data-stu-id="23a5b-111">The change in attribute values happens when there are values in these attributes representing non-verified domains.</span></span> <span data-ttu-id="23a5b-112">Ancak eşitleme altyapısı Bağlan gölge öznitelik değeri bunu kendi açısından okur, öznitelik Azure AD tarafından onaylanmıştır.</span><span class="sxs-lookup"><span data-stu-id="23a5b-112">But the sync engine in Connect reads the value in the shadow attribute so from its perspective, the attribute has been confirmed by Azure AD.</span></span>

<span data-ttu-id="23a5b-113">Azure portal veya PowerShell ile kullanarak gölge özniteliklerini göremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="23a5b-113">You cannot see the shadow attributes using the Azure portal or with PowerShell.</span></span> <span data-ttu-id="23a5b-114">Ancak kavramı anlamak, belirli senaryolar farklı değerler şirket içi özniteliğine sahip olduğunda ve bulutta gidermenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="23a5b-114">But understanding the concept helps you to troubleshoot certain scenarios where the attribute has different values on-premises and in the cloud.</span></span>

<span data-ttu-id="23a5b-115">Davranış daha iyi anlamak için bu örnekten Fabrikam bakın:</span><span class="sxs-lookup"><span data-stu-id="23a5b-115">To better understand the behavior, look at this example from Fabrikam:</span></span>  
![Etki Alanları](./media/active-directory-aadconnectsyncservice-shadow-attributes/domains.png)  
<span data-ttu-id="23a5b-117">Kendi şirket içi Active Directory'de birden çok UPN soneki olabilirler, ancak bunlar yalnızca biri doğruladıktan.</span><span class="sxs-lookup"><span data-stu-id="23a5b-117">They have multiple UPN suffixes in their on-premises Active Directory, but they have only verified one.</span></span>

### <a name="userprincipalname"></a><span data-ttu-id="23a5b-118">userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="23a5b-118">userPrincipalName</span></span>
<span data-ttu-id="23a5b-119">Bir kullanıcı, aşağıdaki öznitelik değerlerini doğrulanmamış bir etki alanı vardır:</span><span class="sxs-lookup"><span data-stu-id="23a5b-119">A user has the following attribute values in a non-verified domain:</span></span>

| <span data-ttu-id="23a5b-120">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="23a5b-120">Attribute</span></span> | <span data-ttu-id="23a5b-121">Değer</span><span class="sxs-lookup"><span data-stu-id="23a5b-121">Value</span></span> |
| --- | --- |
| <span data-ttu-id="23a5b-122">Şirket içi userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="23a5b-122">on-premises userPrincipalName</span></span> | lee.sperry@fabrikam.com |
| <span data-ttu-id="23a5b-123">Azure AD shadowUserPrincipalName</span><span class="sxs-lookup"><span data-stu-id="23a5b-123">Azure AD shadowUserPrincipalName</span></span> | lee.sperry@fabrikam.com |
| <span data-ttu-id="23a5b-124">Azure AD userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="23a5b-124">Azure AD userPrincipalName</span></span> | lee.sperry@fabrikam.onmicrosoft.com |

<span data-ttu-id="23a5b-125">UserPrincipalName özniteliğinin PowerShell kullanırken gördüğünüz değerdir.</span><span class="sxs-lookup"><span data-stu-id="23a5b-125">The userPrincipalName attribute is the value you see when using PowerShell.</span></span>

<span data-ttu-id="23a5b-126">Gerçek şirket içi öznitelik değeri ne zaman fabrikam.com etki alanını doğrulayın, Azure AD içinde kaydedildiği Azure AD userPrincipalName özniteliği shadowUserPrincipalName değeri ile güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="23a5b-126">Since the real on-premises attribute value is stored in Azure AD, when you verify the fabrikam.com domain, Azure AD updates the userPrincipalName attribute with the value from the shadowUserPrincipalName.</span></span> <span data-ttu-id="23a5b-127">Değişiklikleri güncelleştirilmesi için Azure AD Connect bu değerleri için eşitleme gerekmez.</span><span class="sxs-lookup"><span data-stu-id="23a5b-127">You do not have to synchronize any changes from Azure AD Connect for these values to be updated.</span></span>

### <a name="proxyaddresses"></a><span data-ttu-id="23a5b-128">proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="23a5b-128">proxyAddresses</span></span>
<span data-ttu-id="23a5b-129">Yalnızca doğrulanmış etki alanları dahil olmak üzere aynı işlemi proxyAddresses, ancak bazı ilave bir mantık daha da oluşur.</span><span class="sxs-lookup"><span data-stu-id="23a5b-129">The same process for only including verified domains also occurs for proxyAddresses, but with some additional logic.</span></span> <span data-ttu-id="23a5b-130">Doğrulanmış etki alanları için onay yalnızca posta kutusu kullanıcılar için gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="23a5b-130">The check for verified domains only happens for mailbox users.</span></span> <span data-ttu-id="23a5b-131">Bir posta etkin bir kullanıcıya veya kişi temsil eden bir kullanıcı başka bir Exchange kuruluşunda ve bu nesnelere Proxyaddresses'teki tüm değerleri ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="23a5b-131">A mail-enabled user or contact represent a user in another Exchange organization and you can add any values in proxyAddresses to these objects.</span></span>

<span data-ttu-id="23a5b-132">Her iki şirket içi posta kutusu bir kullanıcı için ya da Exchange Online'da yalnızca değerleri doğrulanmış etki alanları için görünür.</span><span class="sxs-lookup"><span data-stu-id="23a5b-132">For a mailbox user, either on-premises or in Exchange Online, only values for verified domains appear.</span></span> <span data-ttu-id="23a5b-133">Şu şekilde görünebilir:</span><span class="sxs-lookup"><span data-stu-id="23a5b-133">It could look like this:</span></span>

| <span data-ttu-id="23a5b-134">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="23a5b-134">Attribute</span></span> | <span data-ttu-id="23a5b-135">Değer</span><span class="sxs-lookup"><span data-stu-id="23a5b-135">Value</span></span> |
| --- | --- |
| <span data-ttu-id="23a5b-136">Şirket içi proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="23a5b-136">on-premises proxyAddresses</span></span> | SMTP:abbie.spencer@fabrikamonline.com</br>smtp:abbie.spencer@fabrikam.com</br>smtp:abbie@fabrikamonline.com |
| <span data-ttu-id="23a5b-137">Exchange Online proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="23a5b-137">Exchange Online proxyAddresses</span></span> | SMTP:abbie.spencer@fabrikamonline.com</br>smtp:abbie@fabrikamonline.com</br>SIP:abbie.spencer@fabrikamonline.com |

<span data-ttu-id="23a5b-138">Bu durumda  **smtp:abbie.spencer@fabrikam.com**  bu etki alanı doğrulanmadı beri kaldırıldı.</span><span class="sxs-lookup"><span data-stu-id="23a5b-138">In this case **smtp:abbie.spencer@fabrikam.com** was removed since that domain has not been verified.</span></span> <span data-ttu-id="23a5b-139">Ancak aynı zamanda eklenen Exchange  **SIP:abbie.spencer@fabrikamonline.com** .</span><span class="sxs-lookup"><span data-stu-id="23a5b-139">But Exchange also added **SIP:abbie.spencer@fabrikamonline.com**.</span></span> <span data-ttu-id="23a5b-140">Fabrikam Lync/Skype şirket içi ancak Azure AD kullanmamış ve Exchange Online hazırlamak için.</span><span class="sxs-lookup"><span data-stu-id="23a5b-140">Fabrikam has not used Lync/Skype on-premises, but Azure AD and Exchange Online prepare for it.</span></span>

<span data-ttu-id="23a5b-141">Bu mantığı proxyAddresses olarak adlandırılır **ProxyCalc**.</span><span class="sxs-lookup"><span data-stu-id="23a5b-141">This logic for proxyAddresses is referred to as **ProxyCalc**.</span></span> <span data-ttu-id="23a5b-142">ProxyCalc her değişikliğe bir kullanıcı olarak çağrılan zaman:</span><span class="sxs-lookup"><span data-stu-id="23a5b-142">ProxyCalc is invoked with every change on a user when:</span></span>

- <span data-ttu-id="23a5b-143">Kullanıcı, kullanıcı Exchange için lisanslı değil olsa bile Exchange Online içeren bir hizmet planına atanmıştır.</span><span class="sxs-lookup"><span data-stu-id="23a5b-143">The user has been assigned a service plan that includes Exchange Online even if the user was not licensed for Exchange.</span></span> <span data-ttu-id="23a5b-144">Örneğin, kullanıcının Office E3 SKU atanmış, ancak yalnızca SharePoint çevrimiçi atandı.</span><span class="sxs-lookup"><span data-stu-id="23a5b-144">For example, if the user is assigned the Office E3 SKU, but only was assigned SharePoint Online.</span></span> <span data-ttu-id="23a5b-145">Posta hala şirket içi olsa bile bu geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="23a5b-145">This is true even if your mailbox is still on-premises.</span></span>
- <span data-ttu-id="23a5b-146">Öznitelik msExchRecipientTypeDetails bir değer içeriyor.</span><span class="sxs-lookup"><span data-stu-id="23a5b-146">The attribute msExchRecipientTypeDetails has a value.</span></span>
- <span data-ttu-id="23a5b-147">Bir değişiklik proxyAddresses veya userPrincipalName olun.</span><span class="sxs-lookup"><span data-stu-id="23a5b-147">You make a change to proxyAddresses or userPrincipalName.</span></span>

<span data-ttu-id="23a5b-148">ProxyCalc bir kullanıcının bir değişiklik işlemek için biraz zaman alabilir ve Azure AD Connect dışarı aktarma işlemine zaman uyumlu değil.</span><span class="sxs-lookup"><span data-stu-id="23a5b-148">ProxyCalc might take some time to process a change on a user and is not synchronous with the Azure AD Connect export process.</span></span>

> [!NOTE]
> <span data-ttu-id="23a5b-149">Bu konudaki belgelenmemiş Gelişmiş senaryolar için bazı ek davranışları ProxyCalc mantığı vardır.</span><span class="sxs-lookup"><span data-stu-id="23a5b-149">The ProxyCalc logic has some additional behaviors for advanced scenarios not documented in this topic.</span></span> <span data-ttu-id="23a5b-150">Bu konu, davranışlarını anlamak ve tüm İç mantık belge değil sağlanır.</span><span class="sxs-lookup"><span data-stu-id="23a5b-150">This topic is provided for you to understand the behavior and not document all internal logic.</span></span>

### <a name="quarantined-attribute-values"></a><span data-ttu-id="23a5b-151">Karantinaya alınan öznitelik değerleri</span><span class="sxs-lookup"><span data-stu-id="23a5b-151">Quarantined attribute values</span></span>
<span data-ttu-id="23a5b-152">Yinelenen öznitelik değerleri olduğunda gölge öznitelikler de kullanılır.</span><span class="sxs-lookup"><span data-stu-id="23a5b-152">Shadow attributes are also used when there are duplicate attribute values.</span></span> <span data-ttu-id="23a5b-153">Daha fazla bilgi için bkz: [yinelenen öznitelik dayanıklılık](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span><span class="sxs-lookup"><span data-stu-id="23a5b-153">For more information, see [duplicate attribute resiliency](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="23a5b-154">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="23a5b-154">See also</span></span>
* [<span data-ttu-id="23a5b-155">Azure AD Connect eşitleme</span><span class="sxs-lookup"><span data-stu-id="23a5b-155">Azure AD Connect sync</span></span>](active-directory-aadconnectsync-whatis.md)
* <span data-ttu-id="23a5b-156">[Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="23a5b-156">[Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
