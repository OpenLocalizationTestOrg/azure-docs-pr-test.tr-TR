---
title: "aaaHow toostart erişim gözden geçirme | Microsoft Docs"
description: "Toocreate erişimini nasıl gözden hello Azure Privileged Identity Management uygulaması ile ayrıcalıklı kimlikleri için öğrenin."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 3e52b731-55f4-4c8a-ba87-9fd34033f52f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/04/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 24feac307f77c69b5d68d6ae0623dbcb52416b01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toostart-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="44a9e-103">Nasıl toostart access gözden Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="44a9e-103">How toostart an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="44a9e-104">Kullanıcılar ayrıcalıklı artık gerekmeyen erişimi olan, rol atamaları "eski" olur.</span><span class="sxs-lookup"><span data-stu-id="44a9e-104">Role assignments become "stale" when users have privileged access that they don't need anymore.</span></span> <span data-ttu-id="44a9e-105">Bu eski rol atamaları ile ilişkili sipariş tooreduce hello riskine ayrıcalıklı rol Yöneticiler düzenli olarak kullanıcılara verilen hello rolleri gözden geçirmelidir.</span><span class="sxs-lookup"><span data-stu-id="44a9e-105">In order tooreduce hello risk associated with these stale role assignments, privileged role administrators should regularly review hello roles that users have been given.</span></span> <span data-ttu-id="44a9e-106">Bu belge, Azure AD Privileged Identity Management (PIM) erişim gözden geçirme başlatmak için hello adımlar kapsanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="44a9e-106">This document covers hello steps for starting an access review in Azure AD Privileged Identity Management (PIM).</span></span>

## <a name="start-an-access-review"></a><span data-ttu-id="44a9e-107">Bir erişim incelemesi başlatma</span><span class="sxs-lookup"><span data-stu-id="44a9e-107">Start an access review</span></span>
> [!NOTE]
> <span data-ttu-id="44a9e-108">Hello Azure portal hello PIM uygulama tooyour Panosu eklemediyseniz, hello adımlara bakın [Azure Privileged Identity Management ile çalışmaya başlama](active-directory-privileged-identity-management-getting-started.md)</span><span class="sxs-lookup"><span data-stu-id="44a9e-108">If you haven't added hello PIM application tooyour dashboard in hello Azure portal, see hello steps in  [Getting Started with Azure Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md)</span></span>
> 
> 

<span data-ttu-id="44a9e-109">Merhaba PIM uygulama ana sayfası, bir erişim gözden geçirme üç yolu toostart vardır:</span><span class="sxs-lookup"><span data-stu-id="44a9e-109">From hello PIM application main page, there are three ways toostart an access review:</span></span>

* <span data-ttu-id="44a9e-110">**Erişim incelemeler** > **Ekle**</span><span class="sxs-lookup"><span data-stu-id="44a9e-110">**Access reviews** > **Add**</span></span>
* <span data-ttu-id="44a9e-111">**Rolleri** > **gözden geçirme** düğmesi</span><span class="sxs-lookup"><span data-stu-id="44a9e-111">**Roles** > **Review** button</span></span>
* <span data-ttu-id="44a9e-112">Select hello belirli rol toobe gözden hello rollerinin listesinden > **gözden geçirme** düğmesi</span><span class="sxs-lookup"><span data-stu-id="44a9e-112">Select hello specific role toobe reviewed from hello roles list > **Review** button</span></span>

<span data-ttu-id="44a9e-113">Merhaba üzerinde tıkladığınızda **gözden** hello düğmesi, **erişim incelemesi başlatma** dikey penceresi görünür.</span><span class="sxs-lookup"><span data-stu-id="44a9e-113">When you click on hello **Review** button, hello **Start an access review** blade appears.</span></span> <span data-ttu-id="44a9e-114">Bu dikey giderek tooconfigure hello gözden bir ada sahip olduğunuz ve sınırı süresi, bir rol tooreview seçin ve hello gözden geçirme işlemini gerçekleştirecek karar verin.</span><span class="sxs-lookup"><span data-stu-id="44a9e-114">On this blade, you're going tooconfigure hello review with a name and time limit, choose a role tooreview, and decide who will perform hello review.</span></span>

![-Ekran görüntüsü bir erişim incelemesi başlatma][1]

### <a name="configure-hello-review"></a><span data-ttu-id="44a9e-116">Merhaba gözden geçirme yapılandırın</span><span class="sxs-lookup"><span data-stu-id="44a9e-116">Configure hello review</span></span>
<span data-ttu-id="44a9e-117">access toocreate gözden geçirin, tooname ve bir başlangıç ve bitiş tarihi kümesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="44a9e-117">toocreate an access review, you need tooname it and set a start and end date.</span></span>

![Gözden geçirme - ekran görüntüsü yapılandırma][2]

<span data-ttu-id="44a9e-119">Merhaba uzunluğu yeteri kadar kullanıcılar toocomplete için gözden hello olun.</span><span class="sxs-lookup"><span data-stu-id="44a9e-119">Make hello length of hello review long enough for users toocomplete it.</span></span> <span data-ttu-id="44a9e-120">Merhaba bitiş tarihinden önce son varsa, her zaman hello gözden geçirme erken durdurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44a9e-120">If you finish before hello end date, you can always stop hello review early.</span></span>

### <a name="choose-a-role-tooreview"></a><span data-ttu-id="44a9e-121">Bir rol tooreview seçin</span><span class="sxs-lookup"><span data-stu-id="44a9e-121">Choose a role tooreview</span></span>
<span data-ttu-id="44a9e-122">Her gözden geçirme sadece tek bir rol üzerinde odaklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="44a9e-122">Each review focuses on only one role.</span></span> <span data-ttu-id="44a9e-123">Belirli bir rol dikey penceresinden hello erişim gözden geçirme başlattığınız sürece toochoose rol artık gerekir.</span><span class="sxs-lookup"><span data-stu-id="44a9e-123">Unless you started hello access review from a specific role blade, you'll need toochoose a role now.</span></span>

1. <span data-ttu-id="44a9e-124">Çok gidin**rol üyeliğini gözden geçirin**</span><span class="sxs-lookup"><span data-stu-id="44a9e-124">Navigate too**Review role membership**</span></span>
   
    ![Gözden geçirme rol üyeliğini - ekran görüntüsü][3]
2. <span data-ttu-id="44a9e-126">Bir rol hello listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="44a9e-126">Choose one role from hello list.</span></span>

### <a name="decide-who-will-perform-hello-review"></a><span data-ttu-id="44a9e-127">Merhaba gözden geçirme işlemini gerçekleştirecek karar verin</span><span class="sxs-lookup"><span data-stu-id="44a9e-127">Decide who will perform hello review</span></span>
<span data-ttu-id="44a9e-128">Bir gözden geçirme gerçekleştirmek için üç seçenek vardır.</span><span class="sxs-lookup"><span data-stu-id="44a9e-128">There are three options for performing a review.</span></span> <span data-ttu-id="44a9e-129">Merhaba gözden geçirme toosomeone atayabilirsiniz başka toocomplete kendiniz yapabileceğiniz ya da kendi access gözden her kullanıcının olabilir.</span><span class="sxs-lookup"><span data-stu-id="44a9e-129">You can assign hello review toosomeone else toocomplete, you can do it yourself, or you can have each user review their own access.</span></span>

1. <span data-ttu-id="44a9e-130">Çok gidin**gözden geçirenler seçin**</span><span class="sxs-lookup"><span data-stu-id="44a9e-130">Navigate too**Select reviewers**</span></span>
   
    ![Gözden geçirenler - ekran görüntüsü seçin][4]
2. <span data-ttu-id="44a9e-132">Merhaba seçeneklerden birini seçin:</span><span class="sxs-lookup"><span data-stu-id="44a9e-132">Choose one of hello options:</span></span>
   
   * <span data-ttu-id="44a9e-133">**Select İnceleme**: erişim gerek duyan bilmiyorsanız bu seçeneği kullanın.</span><span class="sxs-lookup"><span data-stu-id="44a9e-133">**Select reviewer**: Use this option when you don't know who needs access.</span></span> <span data-ttu-id="44a9e-134">Bu seçenek ile Merhaba gözden geçirme tooa kaynak sahibi veya grup yöneticisi toocomplete atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44a9e-134">With this option, you can assign hello review tooa resource owner or group manager toocomplete.</span></span>
   * <span data-ttu-id="44a9e-135">**Bana**: toopreview nasıl istiyorsanız yararlı olamaz kişilerin adına tooreview istediğiniz veya erişim iş gözden geçirir.</span><span class="sxs-lookup"><span data-stu-id="44a9e-135">**Me**: Useful if you want toopreview how access reviews work, or you want tooreview on behalf of people who can't.</span></span>
   * <span data-ttu-id="44a9e-136">**Üyeleri kendilerini gözden**: Bu seçenek toohave hello kullanıcılar gözden kendi rol atamalarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="44a9e-136">**Members review themselves**: Use this option toohave hello users review their own role assignments.</span></span>

### <a name="start-hello-review"></a><span data-ttu-id="44a9e-137">Merhaba incelemesi başlatma</span><span class="sxs-lookup"><span data-stu-id="44a9e-137">Start hello review</span></span>
<span data-ttu-id="44a9e-138">Son olarak, kullanıcılar erişimleri onaylıyorsanız bir gerekçe sağlamasını hello seçeneği toorequire sahip.</span><span class="sxs-lookup"><span data-stu-id="44a9e-138">Finally, you have hello option toorequire that users provide a reason if they approve their access.</span></span> <span data-ttu-id="44a9e-139">Merhaba gözden geçirme açıklamasını isterseniz ekleyin ve seçin **Başlat**.</span><span class="sxs-lookup"><span data-stu-id="44a9e-139">Add a description of hello review if you like, and select **Start**.</span></span>

<span data-ttu-id="44a9e-140">Kullanıcılarınız kendileri için bekleyen bir erişim gözden geçirme olduğunu biliyor ve bunları Göster izin emin olun [tooperform erişimini nasıl gözden](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="44a9e-140">Make sure you let your users know that there's an access review waiting for them, and show them [How tooperform an access review](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span></span>

## <a name="manage-hello-access-review"></a><span data-ttu-id="44a9e-141">Merhaba erişim gözden geçirme yönetme</span><span class="sxs-lookup"><span data-stu-id="44a9e-141">Manage hello access review</span></span>
<span data-ttu-id="44a9e-142">Merhaba gözden geçirenler hello Azure AD PIM Pano içinde kendi incelemeler tamamlarken hello ilerleme durumunu izleyebilirsiniz, hello erişim bölümü gözden geçirir.</span><span class="sxs-lookup"><span data-stu-id="44a9e-142">You can track hello progress as hello reviewers complete their reviews in hello Azure AD PIM dashboard, in hello access reviews section.</span></span> <span data-ttu-id="44a9e-143">Erişim hakları yok kadar hello dizininde değiştirilecek [hello İnceleme tamamlandıktan](active-directory-privileged-identity-management-how-to-complete-review.md).</span><span class="sxs-lookup"><span data-stu-id="44a9e-143">No access rights will be changed in hello directory until [hello review completes](active-directory-privileged-identity-management-how-to-complete-review.md).</span></span>

<span data-ttu-id="44a9e-144">Merhaba gözden geçirme süresi bitene kadar kullanıcılar toocomplete gözden anımsatmak veya Dur hello gözden geçirme, hello erişimden erken bölümü gözden geçirir..</span><span class="sxs-lookup"><span data-stu-id="44a9e-144">Until hello review period is over, you can remind users toocomplete their review, or stop hello review early from hello access reviews section.</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="pim-table-of-contents"></a><span data-ttu-id="44a9e-145">PIM İçindekiler</span><span class="sxs-lookup"><span data-stu-id="44a9e-145">PIM Table of Contents</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_start_review.png
[2]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_configure.png
[3]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_role.png
[4]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_reviewers.png
