---
title: "aaaHow toocomplete erişim gözden geçirme | Microsoft Docs"
description: "Azure AD Privileged Identity Management erişim gözden geçirme başlatıldıktan sonra öğrenin nasıl toocomplete ve görünüm hello sonuçları"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: abc2d3dd-afd5-42cf-8a17-6c11f5674c35
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: kgremban
ms.custom: pim
ms.openlocfilehash: f99ddf3ebcf80b51110326064d584f33d8e1679a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocomplete-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="9fe59-103">Nasıl toocomplete access gözden Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="9fe59-103">How toocomplete an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="9fe59-104">Ayrıcalıklı rol Yöneticiler gözden geçirebileceğiniz ayrıcalıklı erişim kez bir [güvenlik incelemesi başlatıldıysa](active-directory-privileged-identity-management-how-to-start-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="9fe59-104">Privileged role administrators can review privileged access once a [security review has been started](active-directory-privileged-identity-management-how-to-start-security-review.md).</span></span> <span data-ttu-id="9fe59-105">Azure AD Privileged Identity Management (PIM) otomatik olarak kullanıcılar tooreview bunların erişim isteyen bir e-posta gönderir.</span><span class="sxs-lookup"><span data-stu-id="9fe59-105">Azure AD Privileged Identity Management (PIM) will automatically send an email prompting users tooreview their access.</span></span> <span data-ttu-id="9fe59-106">Bir kullanıcı bir e-posta almadığını varsa, bunları hello yönergeleri gönderebilirsiniz [nasıl tooperform güvenlik gözden](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="9fe59-106">If a user did not get an email, you can send them hello instructions in [how tooperform a security review](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span></span>

<span data-ttu-id="9fe59-107">Merhaba güvenlik değerlendirme süresi sona erer veya tüm hello kullanıcılar kendi kendini gözden tamamladıktan sonra bu makale toomanage hello gözden hello adımları izleyin ve hello sonuçlarını görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9fe59-107">After hello security review period is over, or all hello users have finished their self-review, follow hello steps in this article toomanage hello review and see hello results.</span></span>

## <a name="manage-security-reviews"></a><span data-ttu-id="9fe59-108">Güvenlik değerlendirmeleri yönetme</span><span class="sxs-lookup"><span data-stu-id="9fe59-108">Manage security reviews</span></span>
1. <span data-ttu-id="9fe59-109">Toohello Git [Azure portal](https://portal.azure.com/) ve select hello **Azure AD Privileged Identity Management** Panonuzda uygulama.</span><span class="sxs-lookup"><span data-stu-id="9fe59-109">Go toohello [Azure portal](https://portal.azure.com/) and select hello **Azure AD Privileged Identity Management** application on your dashboard.</span></span>
2. <span data-ttu-id="9fe59-110">Select hello **erişim incelemeler** başlangıç Panosu bölümü.</span><span class="sxs-lookup"><span data-stu-id="9fe59-110">Select hello **Access reviews** section of hello dashboard.</span></span>
3. <span data-ttu-id="9fe59-111">Merhaba erişim gözden geçirme toomanage istediğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="9fe59-111">Select hello access review that you want toomanage.</span></span>

<span data-ttu-id="9fe59-112">Merhaba erişim gözden geçirme 's ayrıntı dikey penceresinde bu gözden geçirme yönetmek için bir numara seçenekleri mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="9fe59-112">On hello access review's detail blade there are a number options for managing that review.</span></span>

![PIM erişim gözden geçirme düğmeleri - ekran görüntüsü][1]

### <a name="remind"></a><span data-ttu-id="9fe59-114">Şu aralıklarla uyar</span><span class="sxs-lookup"><span data-stu-id="9fe59-114">Remind</span></span>
<span data-ttu-id="9fe59-115">Böylece Hello kullanıcıların kendilerini gözden erişim gözden geçirme ayarlanıp ayarlanmadığını hello **Anımsat** düğmesi bir bildirim gönderir.</span><span class="sxs-lookup"><span data-stu-id="9fe59-115">If an access review is set up so that hello users review themselves, hello **Remind** button sends out a notification.</span></span> 

### <a name="stop"></a><span data-ttu-id="9fe59-116">Durdur</span><span class="sxs-lookup"><span data-stu-id="9fe59-116">Stop</span></span>
<span data-ttu-id="9fe59-117">Bitiş tarihi tüm erişim değerlendirmeleri sahip, ancak hello kullanabilirsiniz **durdurmak** düğmesini toofinish, erken.</span><span class="sxs-lookup"><span data-stu-id="9fe59-117">All access reviews have an end date, but you can use hello **Stop** button toofinish it early.</span></span> <span data-ttu-id="9fe59-118">Tüm kullanıcılar bu zamana kadar gözden yapmadıysanız, bunlar hello gözden geçirme durdurmak mümkün tooafter olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="9fe59-118">If any users haven't been reviewed by this time, they won't be able tooafter you stop hello review.</span></span> <span data-ttu-id="9fe59-119">Durdurulmuş sonra bir gözden geçirme yeniden başlatılamıyor.</span><span class="sxs-lookup"><span data-stu-id="9fe59-119">You cannot restart a review after it's been stopped.</span></span>

### <a name="apply"></a><span data-ttu-id="9fe59-120">Başvurun</span><span class="sxs-lookup"><span data-stu-id="9fe59-120">Apply</span></span>
<span data-ttu-id="9fe59-121">Bir erişim gözden geçirme tamamlandıktan sonra hello bitiş tarihi ulaşıldı veya el ile durduruldu çünkü ya da hello **Uygula** düğmesi uygulayan hello sonucu hello gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="9fe59-121">After an access review is completed, either because you reached hello end date or stopped it manually, hello **Apply** button implements hello outcome of hello review.</span></span> <span data-ttu-id="9fe59-122">Bir kullanıcının erişimi hello incelemede reddedildiyse, kendi rol atamasını kaldıracak hello adım budur.</span><span class="sxs-lookup"><span data-stu-id="9fe59-122">If a user's access was denied in hello review, this is hello step that will remove their role assignment.</span></span>  

### <a name="export"></a><span data-ttu-id="9fe59-123">Dışarı Aktarma</span><span class="sxs-lookup"><span data-stu-id="9fe59-123">Export</span></span>
<span data-ttu-id="9fe59-124">Tooapply hello hello güvenlik incelemesi sonuçlarını el ile istiyorsanız hello gözden geçirme dışarı aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9fe59-124">If you want tooapply hello results of hello security review manually, you can export hello review.</span></span> <span data-ttu-id="9fe59-125">Merhaba **verme** düğmesi, bir CSV dosyası yükleme başlayacak.</span><span class="sxs-lookup"><span data-stu-id="9fe59-125">hello **Export** button will start downloading a CSV file.</span></span> <span data-ttu-id="9fe59-126">Excel veya CSV dosyalarını açma diğer programları hello sonuçlarını yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9fe59-126">You can manage hello results in Excel or other programs that open CSV files.</span></span>

### <a name="delete"></a><span data-ttu-id="9fe59-127">Sil</span><span class="sxs-lookup"><span data-stu-id="9fe59-127">Delete</span></span>
<span data-ttu-id="9fe59-128">Hello ilgilenen değilseniz daha fazla gözden, silin.</span><span class="sxs-lookup"><span data-stu-id="9fe59-128">If you are not interested in hello review any further, delete it.</span></span> <span data-ttu-id="9fe59-129">Merhaba **silmek** düğmesini hello gözden geçirme hello PIM uygulama ' kaldırır.</span><span class="sxs-lookup"><span data-stu-id="9fe59-129">hello **Delete** button removes hello review from hello PIM application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9fe59-130">Değil silme oluşmadan önce bir uyarı almak, böylece gözden toodelete istediğiniz emin olun.</span><span class="sxs-lookup"><span data-stu-id="9fe59-130">You will not get a warning before deletion occurs, so be sure that you want toodelete that review.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9fe59-131">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9fe59-131">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-complete-review/PIM_review_buttons.png
