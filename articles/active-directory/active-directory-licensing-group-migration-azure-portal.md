---
title: "tek tek lisanslı kullanıcılar tooa Azure Active Directory'de Grup aaaHow toomigrate | Microsoft Docs"
description: "Nasıl toogroup tabanlı Azure Active Directory'yi kullanarak lisans tooswitch tek tek kullanıcı lisansları"
services: active-directory
keywords: Azure AD lisanslama
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/05/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 25e5c760b7e632ba71edde10d937fe580aa6ed35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-licensed-users-tooa-group-for-licensing-in-azure-active-directory"></a><span data-ttu-id="2092d-104">Azure Active Directory'de lisans için tooadd kullanıcılar tooa grubunun nasıl lisanslı</span><span class="sxs-lookup"><span data-stu-id="2092d-104">How tooadd licensed users tooa group for licensing in Azure Active Directory</span></span>

<span data-ttu-id="2092d-105">Varolan dağıtılmış lisansları toousers hello kuruluşlar "doğrudan atama"; aracılığıyla olabilir diğer bir deyişle, PowerShell komut dosyaları veya diğer araçlar tooassign tek tek kullanıcı lisansları kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="2092d-105">You may have existing licenses deployed toousers in hello organizations via “direct assignment”; that is, using PowerShell scripts or other tools tooassign individual user licenses.</span></span> <span data-ttu-id="2092d-106">Grup tabanlı lisans toomanage kuruluşunuzda lisanslarla toostart isterseniz, bir geçiş gerekir planı tooseamlessly var olan çözümler grup tabanlı lisanslama ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="2092d-106">If you would like toostart using group-based licensing toomanage licenses in your organization, you will need a migration plan tooseamlessly replace existing solutions with group-based licensing.</span></span>

<span data-ttu-id="2092d-107">Burada, geçirme toogroup tabanlı lisans geçici olarak, şu anda atanmış lisansları kaybetme kullanıcılar neden olacak bir durum kaçınmalısınız Hello en önemli şey tookeep aklınızda olur.</span><span class="sxs-lookup"><span data-stu-id="2092d-107">hello most important thing tookeep in mind is that you should avoid a situation where migrating toogroup-based licensing will result in users temporarily losing their currently assigned licenses.</span></span> <span data-ttu-id="2092d-108">Lisansları kaldırılmasına neden herhangi bir işlem olmalıdır tooremove hello kullanıcıların erişim tooservices ve kendi veri kaybetme riskini engellendi.</span><span class="sxs-lookup"><span data-stu-id="2092d-108">Any process that may result in removal of licenses should be avoided tooremove hello risk of users losing access tooservices and their data.</span></span>

## <a name="recommended-migration-process"></a><span data-ttu-id="2092d-109">Önerilen geçiş işlemi</span><span class="sxs-lookup"><span data-stu-id="2092d-109">Recommended migration process</span></span>

1. <span data-ttu-id="2092d-110">Lisans atama ve kullanıcılar için temizleme yönetme var olan Otomasyon (örneğin, PowerShell) sahip.</span><span class="sxs-lookup"><span data-stu-id="2092d-110">You have existing automation (for example, PowerShell) managing license assignment and removal for users.</span></span> <span data-ttu-id="2092d-111">Çalışan olduğu gibi bırakın.</span><span class="sxs-lookup"><span data-stu-id="2092d-111">Leave it running as is.</span></span>

2. <span data-ttu-id="2092d-112">Yeni bir lisans grubu oluşturma (veya var olan hangi toouse gruplar karar) ve gerekli tüm kullanıcıların üye olarak ekleneceği emin olun.</span><span class="sxs-lookup"><span data-stu-id="2092d-112">Create a new licensing group (or decide which existing groups toouse) and make sure that all required users are added as members.</span></span>

3. <span data-ttu-id="2092d-113">Gerekli hello lisansları toothose grupları atama; Amacınız tooreflect hello olmalıdır aynı durumu lisans, var olan Otomasyon (örneğin, PowerShell) toothose kullanıcılar da uyguluyor.</span><span class="sxs-lookup"><span data-stu-id="2092d-113">Assign hello required licenses toothose groups; your goal should be tooreflect hello same licensing state your existing automation (for example, PowerShell) is applying toothose users.</span></span>

4. <span data-ttu-id="2092d-114">Lisansları uygulanan tooall kullanıcılar bu gruplara verildiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="2092d-114">Verify that licenses have been applied tooall users in those groups.</span></span> <span data-ttu-id="2092d-115">Bu, her grup hello işleme durumunu denetleyerek ve denetim günlüklerini denetleyerek yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="2092d-115">This can be done by checking hello processing state on each group and by checking Audit Logs.</span></span>

  - <span data-ttu-id="2092d-116">Nokta onay bireysel kullanıcılar kendi lisans ayrıntıları bakarak yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2092d-116">You can spot check individual users by looking at their license details.</span></span> <span data-ttu-id="2092d-117">Bunlar sahip Merhaba, aynı "doğrudan" atanan lisansları ve "devralınan" gruplarından görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="2092d-117">You will see that they have hello same licenses assigned “directly” and “inherited” from groups.</span></span>

  - <span data-ttu-id="2092d-118">Bir PowerShell Betiği çok çalıştırabilirsiniz[lisansları toousers nasıl atandığını doğrulayın](active-directory-licensing-group-advanced.md#use-powershell-to-see-who-has-inherited-and-direct-licenses).</span><span class="sxs-lookup"><span data-stu-id="2092d-118">You can run a PowerShell script too[verify how licenses are assigned toousers](active-directory-licensing-group-advanced.md#use-powershell-to-see-who-has-inherited-and-direct-licenses).</span></span>

  - <span data-ttu-id="2092d-119">Merhaba aynı Ürün lisans toohello kullanıcı hem doğrudan hem de bir grubu üzerinden atandığında, yalnızca bir lisans hello kullanıcı tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2092d-119">When hello same product license is assigned toohello user both directly and through a group, only one license is consumed by hello user.</span></span> <span data-ttu-id="2092d-120">Bu nedenle hiçbir ek lisanslar gerekli tooperform geçiş ' dir.</span><span class="sxs-lookup"><span data-stu-id="2092d-120">Hence no additional licenses are required tooperform migration.</span></span>

5. <span data-ttu-id="2092d-121">Hiçbir lisans anlaşmalarını hata durumuna kullanıcılar için her grubu denetleyerek başarısız olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="2092d-121">Verify that no license assignments failed by checking each group for users in error state.</span></span> <span data-ttu-id="2092d-122">Daha fazla bilgi için bkz: [belirleme ve bir grubu için lisans sorunlarını çözmek](active-directory-licensing-group-problem-resolution-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2092d-122">For more information, see [Identifying and resolving license problems for a group](active-directory-licensing-group-problem-resolution-azure-portal.md).</span></span>

6. <span data-ttu-id="2092d-123">Merhaba özgün doğrudan atamalarını kaldırmayı düşünün; toodo isteyebilirsiniz "Dalgalar", toomonitor içinde kademeli olarak, hello sonucu bir kullanıcı alt kümesini üzerinde ilk.</span><span class="sxs-lookup"><span data-stu-id="2092d-123">Consider removing hello original direct assignments; you may want toodo it gradually, in “waves”, toomonitor hello outcome on a subset of users first.</span></span>

  <span data-ttu-id="2092d-124">Kullanıcıların özgün doğrudan atamalarını hello bırakabilir, ancak hello kullanıcılar hala korur, lisanslı gruplarına ayrıldığında büyük olasılıkla hello özgün lisans istediğiniz istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="2092d-124">You could leave hello original direct assignments on users, but when hello users leave their licensed groups they will still retain hello original license, which is possibly not want you want.</span></span>

## <a name="an-example"></a><span data-ttu-id="2092d-125">Bir örnek</span><span class="sxs-lookup"><span data-stu-id="2092d-125">An example</span></span>

<span data-ttu-id="2092d-126">1.000 kullanıcının bulunduğu bir kuruluşta sahibiz.</span><span class="sxs-lookup"><span data-stu-id="2092d-126">We have an organization with 1,000 users.</span></span> <span data-ttu-id="2092d-127">Tüm kullanıcılar, Enterprise Mobility + güvenlik (EMS) lisansı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="2092d-127">All users require Enterprise Mobility + Security (EMS) licenses.</span></span> <span data-ttu-id="2092d-128">200 kullanıcılar hello Finans departmanı ve Office 365 Kurumsal E3 lisanslar gerektirir.</span><span class="sxs-lookup"><span data-stu-id="2092d-128">200 users are in hello Finance Department and require Office 365 Enterprise E3 licenses.</span></span> <span data-ttu-id="2092d-129">Ekleme ve lisans dönün ve Git gibi kullanıcılardan kaldırma şirket içinde çalışan bir PowerShell komut dosyası sunuyoruz.</span><span class="sxs-lookup"><span data-stu-id="2092d-129">We have a PowerShell script running on premises adding and removing licenses from users as they come and go.</span></span> <span data-ttu-id="2092d-130">Lisanslar otomatik olarak Azure AD tarafından yönetilen şekilde grup tabanlı lisanslama ile tooreplace hello betik istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="2092d-130">We want tooreplace hello script with group-based licensing so licenses are managed automatically by Azure AD.</span></span>

<span data-ttu-id="2092d-131">İşte hangi hello geçiş işlemi görünüm ister:</span><span class="sxs-lookup"><span data-stu-id="2092d-131">Here is what hello migration process could look like:</span></span>

1. <span data-ttu-id="2092d-132">Azure portal Ata hello EMS lisansı toohello hello kullanarak **tüm kullanıcılar** Azure AD grubu.</span><span class="sxs-lookup"><span data-stu-id="2092d-132">Using hello Azure portal assign hello EMS license toohello **All users** group in Azure AD.</span></span> <span data-ttu-id="2092d-133">Merhaba E3 lisans toohello Ata **Finans departmanı** tüm gerekli hello kullanıcıları içeren grup.</span><span class="sxs-lookup"><span data-stu-id="2092d-133">Assign hello E3 license toohello **Finance department** group that contains all hello required users.</span></span>

2. <span data-ttu-id="2092d-134">Her grup için tüm kullanıcılar için lisans atama tamamlandığını onaylayın.</span><span class="sxs-lookup"><span data-stu-id="2092d-134">For each group, confirm that license assignment has completed for all users.</span></span> <span data-ttu-id="2092d-135">Her grup için select gidin toohello dikey **lisansları**ve hello hello üstündeki hello işleme durumunu denetleyin **lisansları** dikey.</span><span class="sxs-lookup"><span data-stu-id="2092d-135">Go toohello blade for each group, select **Licenses**, and check hello processing status at hello top of hello **Licenses** blade.</span></span>

  - <span data-ttu-id="2092d-136">Aramak için "en son lisans değişiklikleri uygulanan tooall kullanıcılar silinmiş" tooconfirm işleme tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="2092d-136">Look for “Latest license changes have been applied tooall users" tooconfirm processing has completed.</span></span>

  - <span data-ttu-id="2092d-137">Üstteki kendisi için lisansları olmayan başarıyla atanmış olan kullanıcılar hakkında bir bildirim arayın.</span><span class="sxs-lookup"><span data-stu-id="2092d-137">Look for a notification on top about any users for whom licenses may have not been successfully assigned.</span></span> <span data-ttu-id="2092d-138">Bazı kullanıcılar için lisans dışında karşılaştınız mı?</span><span class="sxs-lookup"><span data-stu-id="2092d-138">Did we run out of licenses for some users?</span></span> <span data-ttu-id="2092d-139">Bazı kullanıcılar, çakışan lisans grubu lisansları Devralmayı Engelle SKU'ları var mı?</span><span class="sxs-lookup"><span data-stu-id="2092d-139">Do some users have conflicting license SKUs that prevent them from inheriting group licenses?</span></span>

3. <span data-ttu-id="2092d-140">Nokta hello doğrudan ve uygulanan Grup lisansları sahip oldukları bazı kullanıcılar tooverify denetleyin.</span><span class="sxs-lookup"><span data-stu-id="2092d-140">Spot check some users tooverify that they have both hello direct and group licenses applied.</span></span> <span data-ttu-id="2092d-141">Bir kullanıcı seçin dikey penceresine gidin toohello **lisansları**ve lisansları hello durumunu inceleyin.</span><span class="sxs-lookup"><span data-stu-id="2092d-141">Go toohello blade for a user, select **Licenses**, and examine hello state of licenses.</span></span>

  - <span data-ttu-id="2092d-142">Bu beklenen hello kullanıcı durumu geçiş işlemi sırasında oluşur:</span><span class="sxs-lookup"><span data-stu-id="2092d-142">This is hello expected user state during migration:</span></span>

      ![Beklenen kullanıcı durumu](media/active-directory-licensing-group-migration-azure-portal/expected-user-state.png)

  <span data-ttu-id="2092d-144">Bu, hem doğrudan hem de devralınan lisansları hello kullanıcının sahip doğrular.</span><span class="sxs-lookup"><span data-stu-id="2092d-144">This confirms that hello user has both direct and inherited licenses.</span></span> <span data-ttu-id="2092d-145">Biz, bkz: her ikisi de **EMS** ve **E3** atanır.</span><span class="sxs-lookup"><span data-stu-id="2092d-145">We see that both **EMS** and **E3** are assigned.</span></span>

  - <span data-ttu-id="2092d-146">Her etkin hello Hizmetleri Lisans tooshow ayrıntılarını seçin.</span><span class="sxs-lookup"><span data-stu-id="2092d-146">Select each license tooshow details about hello enabled services.</span></span> <span data-ttu-id="2092d-147">Merhaba doğrudan ve Grup lisansları etkinleştir hello kullanıcı için aynı hizmet planları tam olarak Merhaba, bu kullanılan toocheck olabilir.</span><span class="sxs-lookup"><span data-stu-id="2092d-147">This can be used toocheck if hello direct and group licenses enable exactly hello same service plans for hello user.</span></span>

      ![hizmet planları denetleyin](media/active-directory-licensing-group-migration-azure-portal/check-service-plans.png)

4. <span data-ttu-id="2092d-149">Hem doğrudan hem de Grup lisansları eşdeğer olduğunu doğruladıktan sonra kullanıcıları doğrudan lisanslarını kaldırma başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2092d-149">After confirming that both direct and group licenses are equivalent, you can start removing direct licenses from users.</span></span> <span data-ttu-id="2092d-150">Merhaba Portalı'nda bireysel kullanıcılar için kaldırarak bunu test etmek ve ardından toplu olarak kaldırılan Otomasyon betikleri toohave çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="2092d-150">You can test this by removing them for individual users in hello portal and then run automation scripts toohave them removed in bulk.</span></span> <span data-ttu-id="2092d-151">Aynı kullanıcı hello doğrudan lisansların hello portalı üzerinden kaldırıldı hello bir örneği burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="2092d-151">Here is an example of hello same user with hello direct licenses removed through hello portal.</span></span> <span data-ttu-id="2092d-152">Merhaba lisans durumu değişmeden kalır, ancak biz artık doğrudan atamaları görmek dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="2092d-152">Notice that hello license state remains unchanged, but we no longer see direct assignments.</span></span>

  ![doğrudan lisansları kaldırıldı](media/active-directory-licensing-group-migration-azure-portal/direct-licenses-removed.png)


## <a name="next-steps"></a><span data-ttu-id="2092d-154">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2092d-154">Next steps</span></span>

<span data-ttu-id="2092d-155">toolearn grupları aracılığıyla lisans yönetimi için diğer senaryolar hakkında daha fazla okuma</span><span class="sxs-lookup"><span data-stu-id="2092d-155">toolearn more about other scenarios for license management through groups, read</span></span>

* [<span data-ttu-id="2092d-156">Azure Active Directory'de lisansları tooa grup atama</span><span class="sxs-lookup"><span data-stu-id="2092d-156">Assigning licenses tooa group in Azure Active Directory</span></span>](active-directory-licensing-group-assignment-azure-portal.md)
* [<span data-ttu-id="2092d-157">Grup tabanlı Azure Active Directory lisanslaması nedir?</span><span class="sxs-lookup"><span data-stu-id="2092d-157">What is group-based licensing in Azure Active Directory?</span></span>](active-directory-licensing-whatis-azure-portal.md)
* [<span data-ttu-id="2092d-158">Azure Active Directory'deki bir gruba lisans sorunlarını tanımlama ve</span><span class="sxs-lookup"><span data-stu-id="2092d-158">Identifying and resolving license problems for a group in Azure Active Directory</span></span>](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [<span data-ttu-id="2092d-159">Azure Active Directory grup tabanlı ilave senaryolar lisanslama</span><span class="sxs-lookup"><span data-stu-id="2092d-159">Azure Active Directory group-based licensing additional scenarios</span></span>](active-directory-licensing-group-advanced.md)
