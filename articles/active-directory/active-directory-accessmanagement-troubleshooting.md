---
title: "Gruplar için dinamik üyelik sorunlarını giderme | Microsoft Docs"
description: "Azure AD grupları için dinamik üyelik için sorun giderme ipuçları."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 89bb04b6-a379-49c2-8465-fe386641816a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: 32947e8cc69c9a48d9a285bf0a37ab3398571f86
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-dynamic-memberships-for-groups"></a><span data-ttu-id="cd956-103">Gruplar için dinamik üyelik sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="cd956-103">Troubleshooting dynamic memberships for groups</span></span>
<span data-ttu-id="cd956-104">**I bir kural bir grup üzerinde yapılandırılmış ancak hiçbir üyelik grubunda güncelleştirilmesi**</span><span class="sxs-lookup"><span data-stu-id="cd956-104">**I configured a rule on a group but no memberships get updated in the group**</span></span><br/><span data-ttu-id="cd956-105">Doğrulayın **etkinleştir Temsilcili Grup Yönetimi** ayar **Evet** içinde **yapılandırma** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="cd956-105">Verify that the **Enable delegated group management** setting is set to **Yes** in the **Configure** tab.</span></span> <span data-ttu-id="cd956-106">Yalnızca, bir Azure Active Directory Premium lisansı atandığı kullanıcı olarak oturum açarsanız, bu ayar görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="cd956-106">You will see this setting only if you are signed in as a user to whom an Azure Active Directory Premium license is assigned.</span></span> <span data-ttu-id="cd956-107">Kullanıcı öznitelikleri kuralda değerlerini doğrulayın: kural karşılayan kullanıcılar vardır?</span><span class="sxs-lookup"><span data-stu-id="cd956-107">Verify the values for user attributes on the rule: are there users that satisfy the rule?</span></span>

<span data-ttu-id="cd956-108">**Bir kural yapılandırılmış, ancak şimdi kuralının var olan üyeleri kaldırılır**</span><span class="sxs-lookup"><span data-stu-id="cd956-108">**I configured a rule, but now the existing members of the rule are removed**</span></span><br/><span data-ttu-id="cd956-109">Bu beklenen bir davranıştır.</span><span class="sxs-lookup"><span data-stu-id="cd956-109">This is expected behavior.</span></span> <span data-ttu-id="cd956-110">Bir kural etkin veya değiştirildiğinde varolan grubun üyeleri kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="cd956-110">Existing members of the group are removed when a rule is enabled or changed.</span></span> <span data-ttu-id="cd956-111">Kural değerlendirme sürümünden döndürülen kullanıcılar grubuna üye olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="cd956-111">The users returned from evaluation of the rule are added as members to the group.</span></span>     

<span data-ttu-id="cd956-112">**Ne zaman eklemek veya bir kural neden değiştirmek instantly üyeliği değiştiğinde görmüyorum?**</span><span class="sxs-lookup"><span data-stu-id="cd956-112">**I don’t see membership changes instantly when I add or change a rule, why not?**</span></span><br/><span data-ttu-id="cd956-113">Ayrılmış üyeliği değerlendirmesi düzenli aralıklarla bir zaman uyumsuz arka planda gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="cd956-113">Dedicated membership evaluation is done periodically in an asynchronous background process.</span></span> <span data-ttu-id="cd956-114">İşlem için gereken süreyi dizininizdeki kullanıcı sayısı ve kural sonucu olarak oluşturulan grubu boyutu tarafından belirlenir.</span><span class="sxs-lookup"><span data-stu-id="cd956-114">How long the process takes is determined by the number of users in your directory and the size of the group created as a result of the rule.</span></span> <span data-ttu-id="cd956-115">Genellikle, kullanıcıların küçük sayıda dizinlerle grup üyeliği değişikliklerinin değerinden birkaç dakika içinde görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="cd956-115">Typically, directories with small numbers of users will see the group membership changes in less than a few minutes.</span></span> <span data-ttu-id="cd956-116">Çok sayıda kullanıcı dizinlerle 30 dakika alabilir veya doldurmak için daha uzun.</span><span class="sxs-lookup"><span data-stu-id="cd956-116">Directories with a large number of users can take 30 minutes or longer to populate.</span></span>

### <a name="next-steps"></a><span data-ttu-id="cd956-117">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cd956-117">Next steps</span></span>
<span data-ttu-id="cd956-118">Bu makalelerde Azure Active Directory ile ilgili ek bilgi sağlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="cd956-118">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="cd956-119">Azure Active Directory grupları ile kaynaklara erişimi yönetme</span><span class="sxs-lookup"><span data-stu-id="cd956-119">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="cd956-120">Azure Active Directory'de Uygulama Yönetimi için Makale Dizini</span><span class="sxs-lookup"><span data-stu-id="cd956-120">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="cd956-121">Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="cd956-121">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="cd956-122">Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="cd956-122">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
