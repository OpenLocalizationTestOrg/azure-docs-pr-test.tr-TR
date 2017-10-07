---
title: "gruplar için dinamik üyelik aaaTroubleshooting | Microsoft Docs"
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
ms.openlocfilehash: d792fc406288844e2c5dbe3702c2c9870d09473e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-dynamic-memberships-for-groups"></a><span data-ttu-id="9a6c0-103">Gruplar için dinamik üyelik sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="9a6c0-103">Troubleshooting dynamic memberships for groups</span></span>
<span data-ttu-id="9a6c0-104">**I bir kural bir grup üzerinde yapılandırılmış ancak hiçbir üyelik hello grubunda güncelleştirilmesi**</span><span class="sxs-lookup"><span data-stu-id="9a6c0-104">**I configured a rule on a group but no memberships get updated in hello group**</span></span><br/><span data-ttu-id="9a6c0-105">Bu hello doğrulayın **etkinleştir Temsilcili Grup Yönetimi** ayar çok**Evet** hello içinde **yapılandırma** sekmesi. Bir kullanıcı toowhom bir Azure Active Directory Premium lisansı atanmış olarak yalnızca, oturum açarsanız, bu ayar görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-105">Verify that hello **Enable delegated group management** setting is set too**Yes** in hello **Configure** tab. You will see this setting only if you are signed in as a user toowhom an Azure Active Directory Premium license is assigned.</span></span> <span data-ttu-id="9a6c0-106">Kullanıcı öznitelikleri hello kuralında Hello değerlerini doğrulayın: hello kural karşılayan kullanıcılar vardır?</span><span class="sxs-lookup"><span data-stu-id="9a6c0-106">Verify hello values for user attributes on hello rule: are there users that satisfy hello rule?</span></span>

<span data-ttu-id="9a6c0-107">**Bir kural yapılandırılmış, ancak şimdi hello kuralı var olan üyelerine hello kaldırılır**</span><span class="sxs-lookup"><span data-stu-id="9a6c0-107">**I configured a rule, but now hello existing members of hello rule are removed**</span></span><br/><span data-ttu-id="9a6c0-108">Bu beklenen bir davranıştır.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-108">This is expected behavior.</span></span> <span data-ttu-id="9a6c0-109">Bir kural etkin veya değiştirildiğinde hello grubunun varolan üyeleri kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-109">Existing members of hello group are removed when a rule is enabled or changed.</span></span> <span data-ttu-id="9a6c0-110">Merhaba kural değerlendirme sürümünden döndürülen hello kullanıcılar üyeleri toohello grup olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-110">hello users returned from evaluation of hello rule are added as members toohello group.</span></span>     

<span data-ttu-id="9a6c0-111">**Ne zaman eklemek veya bir kural neden değiştirmek instantly üyeliği değiştiğinde görmüyorum?**</span><span class="sxs-lookup"><span data-stu-id="9a6c0-111">**I don’t see membership changes instantly when I add or change a rule, why not?**</span></span><br/><span data-ttu-id="9a6c0-112">Ayrılmış üyeliği değerlendirmesi düzenli aralıklarla bir zaman uyumsuz arka planda gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-112">Dedicated membership evaluation is done periodically in an asynchronous background process.</span></span> <span data-ttu-id="9a6c0-113">Ne kadar süreyle hello işlem alır belirlenir başlangıç dizini ve hello boyutunuz hello kural sonucu olarak oluşturulan hello grubunun kullanıcıların sayısı.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-113">How long hello process takes is determined by hello number of users in your directory and hello size of hello group created as a result of hello rule.</span></span> <span data-ttu-id="9a6c0-114">Genellikle, kullanıcıların küçük sayıda dizinlerle hello grup üyeliği değişikliklerinin değerinden birkaç dakika içinde görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-114">Typically, directories with small numbers of users will see hello group membership changes in less than a few minutes.</span></span> <span data-ttu-id="9a6c0-115">Çok sayıda kullanıcı dizinlerle 30 dakika veya daha uzun toopopulate alabilir.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-115">Directories with a large number of users can take 30 minutes or longer toopopulate.</span></span>

### <a name="next-steps"></a><span data-ttu-id="9a6c0-116">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9a6c0-116">Next steps</span></span>
<span data-ttu-id="9a6c0-117">Bu makalelerde Azure Active Directory ile ilgili ek bilgi sağlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-117">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="9a6c0-118">Azure Active Directory grupları ile erişim tooresources yönetme</span><span class="sxs-lookup"><span data-stu-id="9a6c0-118">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="9a6c0-119">Azure Active Directory'de Uygulama Yönetimi için Makale Dizini</span><span class="sxs-lookup"><span data-stu-id="9a6c0-119">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="9a6c0-120">Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="9a6c0-120">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="9a6c0-121">Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="9a6c0-121">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
