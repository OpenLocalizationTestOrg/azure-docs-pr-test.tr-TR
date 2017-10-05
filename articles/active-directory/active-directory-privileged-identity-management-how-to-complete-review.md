---
title: "Bir erişim gözden geçirme tamamlama | Microsoft Docs"
description: "Azure AD Privileged Identity Management erişim gözden geçirme başlatıldıktan sonra tamamlamak ve sonuçları görüntüleme hakkında bilgi edinin"
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
ms.openlocfilehash: ca2a1c7c287e4cf6b1b50cfb0068861b6f525596
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-complete-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="80d9a-103">Azure AD Privileged Identity Management erişim incelemede tamamlama</span><span class="sxs-lookup"><span data-stu-id="80d9a-103">How to complete an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="80d9a-104">Ayrıcalıklı rol Yöneticiler gözden geçirebileceğiniz ayrıcalıklı erişim kez bir [güvenlik incelemesi başlatıldıysa](active-directory-privileged-identity-management-how-to-start-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="80d9a-104">Privileged role administrators can review privileged access once a [security review has been started](active-directory-privileged-identity-management-how-to-start-security-review.md).</span></span> <span data-ttu-id="80d9a-105">Azure AD Privileged Identity Management (PIM) otomatik olarak erişimleri gözden geçirmek için kullanıcıların isteyen bir e-posta gönderir.</span><span class="sxs-lookup"><span data-stu-id="80d9a-105">Azure AD Privileged Identity Management (PIM) will automatically send an email prompting users to review their access.</span></span> <span data-ttu-id="80d9a-106">Bir kullanıcı bir e-posta almadığını varsa, bunları yönergeleri gönderebilirsiniz [güvenlik incelemesi gerçekleştirme](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="80d9a-106">If a user did not get an email, you can send them the instructions in [how to perform a security review](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span></span>

<span data-ttu-id="80d9a-107">Güvenlik değerlendirme süresi sona erer veya tüm kullanıcılar kendi kendini gözden tamamladıktan sonra gözden geçirme yönetmek ve sonuçları görmek için bu makaledeki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="80d9a-107">After the security review period is over, or all the users have finished their self-review, follow the steps in this article to manage the review and see the results.</span></span>

## <a name="manage-security-reviews"></a><span data-ttu-id="80d9a-108">Güvenlik değerlendirmeleri yönetme</span><span class="sxs-lookup"><span data-stu-id="80d9a-108">Manage security reviews</span></span>
1. <span data-ttu-id="80d9a-109">Git [Azure portal](https://portal.azure.com/) seçip **Azure AD Privileged Identity Management** Panonuzda uygulama.</span><span class="sxs-lookup"><span data-stu-id="80d9a-109">Go to the [Azure portal](https://portal.azure.com/) and select the **Azure AD Privileged Identity Management** application on your dashboard.</span></span>
2. <span data-ttu-id="80d9a-110">Seçin **erişim incelemeler** bölümü.</span><span class="sxs-lookup"><span data-stu-id="80d9a-110">Select the **Access reviews** section of the dashboard.</span></span>
3. <span data-ttu-id="80d9a-111">Yönetmek istediğiniz erişim gözden geçirme seçin.</span><span class="sxs-lookup"><span data-stu-id="80d9a-111">Select the access review that you want to manage.</span></span>

<span data-ttu-id="80d9a-112">Erişim gözden geçirme 's ayrıntı dikey penceresinde bu gözden geçirme yönetmek için bir numara seçenekleri mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="80d9a-112">On the access review's detail blade there are a number options for managing that review.</span></span>

![PIM erişim gözden geçirme düğmeleri - ekran görüntüsü][1]

### <a name="remind"></a><span data-ttu-id="80d9a-114">Şu aralıklarla uyar</span><span class="sxs-lookup"><span data-stu-id="80d9a-114">Remind</span></span>
<span data-ttu-id="80d9a-115">Böylece kullanıcılar kendileri gözden erişim gözden geçirme ayarlanıp ayarlanmadığını **Anımsat** düğmesi bir bildirim gönderir.</span><span class="sxs-lookup"><span data-stu-id="80d9a-115">If an access review is set up so that the users review themselves, the **Remind** button sends out a notification.</span></span> 

### <a name="stop"></a><span data-ttu-id="80d9a-116">Durdur</span><span class="sxs-lookup"><span data-stu-id="80d9a-116">Stop</span></span>
<span data-ttu-id="80d9a-117">Bitiş tarihi tüm erişim değerlendirmeleri sahip, ancak kullanabileceğiniz **durdurmak** erken bitirme düğmesi.</span><span class="sxs-lookup"><span data-stu-id="80d9a-117">All access reviews have an end date, but you can use the **Stop** button to finish it early.</span></span> <span data-ttu-id="80d9a-118">Tüm kullanıcılar bu zamana kadar gözden yapmadıysanız, gözden geçirme durdurduktan sonra için değiştiremezler.</span><span class="sxs-lookup"><span data-stu-id="80d9a-118">If any users haven't been reviewed by this time, they won't be able to after you stop the review.</span></span> <span data-ttu-id="80d9a-119">Durdurulmuş sonra bir gözden geçirme yeniden başlatılamıyor.</span><span class="sxs-lookup"><span data-stu-id="80d9a-119">You cannot restart a review after it's been stopped.</span></span>

### <a name="apply"></a><span data-ttu-id="80d9a-120">Başvurun</span><span class="sxs-lookup"><span data-stu-id="80d9a-120">Apply</span></span>
<span data-ttu-id="80d9a-121">Bir erişim gözden geçirme tamamlandıktan sonra da bitiş tarihi ulaşıldı veya el ile durduruldu çünkü **Uygula** düğmesi gözden sonucunu uygular.</span><span class="sxs-lookup"><span data-stu-id="80d9a-121">After an access review is completed, either because you reached the end date or stopped it manually, the **Apply** button implements the outcome of the review.</span></span> <span data-ttu-id="80d9a-122">Bir kullanıcının erişimi incelemede reddedildiyse, kendi rol atamasını kaldıracak adım budur.</span><span class="sxs-lookup"><span data-stu-id="80d9a-122">If a user's access was denied in the review, this is the step that will remove their role assignment.</span></span>  

### <a name="export"></a><span data-ttu-id="80d9a-123">Dışarı Aktarma</span><span class="sxs-lookup"><span data-stu-id="80d9a-123">Export</span></span>
<span data-ttu-id="80d9a-124">Güvenlik incelemesi sonuçlarını el ile uygulamak istiyorsanız, gözden geçirme dışarı aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="80d9a-124">If you want to apply the results of the security review manually, you can export the review.</span></span> <span data-ttu-id="80d9a-125">**Verme** düğmesi, bir CSV dosyası yükleme başlayacak.</span><span class="sxs-lookup"><span data-stu-id="80d9a-125">The **Export** button will start downloading a CSV file.</span></span> <span data-ttu-id="80d9a-126">Excel veya CSV dosyalarını açma diğer programları sonuçlarını yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="80d9a-126">You can manage the results in Excel or other programs that open CSV files.</span></span>

### <a name="delete"></a><span data-ttu-id="80d9a-127">Sil</span><span class="sxs-lookup"><span data-stu-id="80d9a-127">Delete</span></span>
<span data-ttu-id="80d9a-128">Başka incelemede değil ilgileniyorsanız, dosyayı silin.</span><span class="sxs-lookup"><span data-stu-id="80d9a-128">If you are not interested in the review any further, delete it.</span></span> <span data-ttu-id="80d9a-129">**Silmek** düğmesini gözden geçirme PIM uygulamasını kaldırır.</span><span class="sxs-lookup"><span data-stu-id="80d9a-129">The **Delete** button removes the review from the PIM application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="80d9a-130">Değil silme oluşmadan önce bir uyarı almak, böylece bu gözden geçirme silmek istediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="80d9a-130">You will not get a warning before deletion occurs, so be sure that you want to delete that review.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="80d9a-131">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="80d9a-131">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-complete-review/PIM_review_buttons.png
