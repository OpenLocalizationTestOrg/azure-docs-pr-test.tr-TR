---
title: "Azure AD Connect Eşitleme Hizmeti Yöneticisi'ni işlemleri | Microsoft Docs"
description: "Merhaba işlemleri sekmesinde hello Synchronization Service Manager için Azure AD Connect anlayın."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 97a26565-618f-4313-8711-5925eeb47cdc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: decbc53613d456a71cd116c40c5e1fd761efd4af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-sync-service-manager-operations-tab"></a><span data-ttu-id="e7bfb-103">Merhaba Eşitleme Hizmeti Yöneticisi'ni işlemler sekmesini kullanarak</span><span class="sxs-lookup"><span data-stu-id="e7bfb-103">Using hello Sync Service Manager Operations tab</span></span>

![Eşitleme Hizmeti Yöneticisi](./media/active-directory-aadconnectsync-service-manager-ui/operations.png)

<span data-ttu-id="e7bfb-105">Hello işlemleri sekmesinde hello en son işlemleri hello sonuçlarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="e7bfb-105">hello operations tab shows hello results from hello most recent operations.</span></span> <span data-ttu-id="e7bfb-106">Bu sekme, anahtar toounderstand olduğu ve sorunlarını giderme.</span><span class="sxs-lookup"><span data-stu-id="e7bfb-106">This tab is key toounderstand and troubleshoot issues.</span></span>

## <a name="understand-hello-information-visible-in-hello-operations-tab"></a><span data-ttu-id="e7bfb-107">Merhaba bilgi hello işlemleri sekmesinde görünür anlama</span><span class="sxs-lookup"><span data-stu-id="e7bfb-107">Understand hello information visible in hello operations tab</span></span>
<span data-ttu-id="e7bfb-108">Merhaba üst yarı tüm metinler kronolojik sırada gösterir.</span><span class="sxs-lookup"><span data-stu-id="e7bfb-108">hello top half shows all runs in chronological order.</span></span> <span data-ttu-id="e7bfb-109">Varsayılan olarak, hello işlemleri günlük hello hakkında bilgi son yedi gün korur, ancak bu ayar ile Merhaba değiştirilebilir [Zamanlayıcı](active-directory-aadconnectsync-feature-scheduler.md).</span><span class="sxs-lookup"><span data-stu-id="e7bfb-109">By default, hello operations log keeps information about hello last seven days, but this setting can be changed with hello [scheduler](active-directory-aadconnectsync-feature-scheduler.md).</span></span> <span data-ttu-id="e7bfb-110">Başarı durumunu göstermez herhangi çalıştırmak için toolook istiyor.</span><span class="sxs-lookup"><span data-stu-id="e7bfb-110">You want toolook for any run that does not show a success status.</span></span> <span data-ttu-id="e7bfb-111">Merhaba üstbilgilerini tıklatarak sıralama hello değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e7bfb-111">You can change hello sorting by clicking hello headers.</span></span>

<span data-ttu-id="e7bfb-112">Merhaba **durum** hello en önemli bilgileri bir sütundur ve hello bir çalıştırma için en önemli bir sorun gösterir.</span><span class="sxs-lookup"><span data-stu-id="e7bfb-112">hello **Status** column is hello most important information and shows hello most severe problem for a run.</span></span> <span data-ttu-id="e7bfb-113">Merhaba en yaygın durumları tooinvestigate öncelik sırasına göre hızlı bir özeti aşağıda verilmiştir (burada * birkaç olası hata dizeleri gösterir).</span><span class="sxs-lookup"><span data-stu-id="e7bfb-113">Here is a quick summary of hello most common statuses in order of priority tooinvestigate (where * indicate several possible error strings).</span></span>

| <span data-ttu-id="e7bfb-114">Durum</span><span class="sxs-lookup"><span data-stu-id="e7bfb-114">Status</span></span> | <span data-ttu-id="e7bfb-115">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e7bfb-115">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="e7bfb-116">durdurulmuş-*</span><span class="sxs-lookup"><span data-stu-id="e7bfb-116">stopped-*</span></span> |<span data-ttu-id="e7bfb-117">çalıştırma hello tamamlanamadı.</span><span class="sxs-lookup"><span data-stu-id="e7bfb-117">hello run could not complete.</span></span> <span data-ttu-id="e7bfb-118">Örneğin, hello uzak sistem kapalı ve bağlantı kurulamıyor.</span><span class="sxs-lookup"><span data-stu-id="e7bfb-118">For example, if hello remote system is down and cannot be contacted.</span></span> |
| <span data-ttu-id="e7bfb-119">durduruldu-hata-sınırı</span><span class="sxs-lookup"><span data-stu-id="e7bfb-119">stopped-error-limit</span></span> |<span data-ttu-id="e7bfb-120">5. 000'den fazla hataları vardır.</span><span class="sxs-lookup"><span data-stu-id="e7bfb-120">There are more than 5,000 errors.</span></span> <span data-ttu-id="e7bfb-121">çalıştırma hello otomatik olarak toohello çok sayıda hata durduruldu.</span><span class="sxs-lookup"><span data-stu-id="e7bfb-121">hello run was automatically stopped due toohello large number of errors.</span></span> |
| <span data-ttu-id="e7bfb-122">Tamamlanan -\*-hataları</span><span class="sxs-lookup"><span data-stu-id="e7bfb-122">completed-\*-errors</span></span> |<span data-ttu-id="e7bfb-123">Merhaba tamamlanmış çalıştırın, ancak araştırılması gereken bir hata (daha az 5.000).</span><span class="sxs-lookup"><span data-stu-id="e7bfb-123">hello run completed, but there are errors (fewer than 5,000) that should be investigated.</span></span> |
| <span data-ttu-id="e7bfb-124">Tamamlanan -\*-uyarıları</span><span class="sxs-lookup"><span data-stu-id="e7bfb-124">completed-\*-warnings</span></span> |<span data-ttu-id="e7bfb-125">Merhaba çalıştırma tamamlandı, ancak bazı verileri beklenen hello durumda değil.</span><span class="sxs-lookup"><span data-stu-id="e7bfb-125">hello run completed, but some data is not in hello expected state.</span></span> <span data-ttu-id="e7bfb-126">Hatalar varsa, bu ileti genellikle yalnızca bir belirti içindir.</span><span class="sxs-lookup"><span data-stu-id="e7bfb-126">If you have errors, then this message is usually only a symptom.</span></span> <span data-ttu-id="e7bfb-127">Hataları ele kadar uyarıları araştırmanız gereken değil.</span><span class="sxs-lookup"><span data-stu-id="e7bfb-127">Until you have addressed errors, you should not investigate warnings.</span></span> |
| <span data-ttu-id="e7bfb-128">başarılı</span><span class="sxs-lookup"><span data-stu-id="e7bfb-128">success</span></span> |<span data-ttu-id="e7bfb-129">Sorunu yok.</span><span class="sxs-lookup"><span data-stu-id="e7bfb-129">No issues.</span></span> |

<span data-ttu-id="e7bfb-130">Bir satır seçtiğinizde, hello alt tooshow hello ayrıntılarını çalıştıran güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="e7bfb-130">When you select a row, hello bottom updates tooshow hello details of that run.</span></span> <span data-ttu-id="e7bfb-131">toohello hello sonuna kadar sol, liste bildiren olabilir **adım #**.</span><span class="sxs-lookup"><span data-stu-id="e7bfb-131">toohello far left of hello bottom, you might have a list saying **Step #**.</span></span> <span data-ttu-id="e7bfb-132">Burada her etki alanı adımı tarafından temsil edilen ormanınızdaki birden çok etki alanı varsa, bu listede yalnızca görünür.</span><span class="sxs-lookup"><span data-stu-id="e7bfb-132">This list only appears if you have multiple domains in your forest where each domain is represented by a step.</span></span> <span data-ttu-id="e7bfb-133">Merhaba etki alanı adı hello başlığı altında bulunabilir **bölüm**.</span><span class="sxs-lookup"><span data-stu-id="e7bfb-133">hello domain name can be found under hello heading **Partition**.</span></span> <span data-ttu-id="e7bfb-134">Altında **eşitleme istatistikleri**, hello işlenen değişikliklerin sayısı hakkında daha fazla bilgi bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e7bfb-134">Under **Synchronization Statistics**, you can find more information about hello number of changes that were processed.</span></span> <span data-ttu-id="e7bfb-135">Merhaba bağlantılar tooget değiştirilen hello nesnelerin bir listesini tıklatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e7bfb-135">You can click hello links tooget a list of hello changed objects.</span></span> <span data-ttu-id="e7bfb-136">Hatalarla nesneniz varsa, bu hataları altında görünmesini **eşitleme hatalarını**.</span><span class="sxs-lookup"><span data-stu-id="e7bfb-136">If you have objects with errors, those errors show up under **Synchronization Errors**.</span></span>

<span data-ttu-id="e7bfb-137">Daha fazla bilgi için bkz: [not synchronızıng bir nesne sorun giderme](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md)</span><span class="sxs-lookup"><span data-stu-id="e7bfb-137">For more information, see [troubleshoot an object that is not synchronizing](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="e7bfb-138">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e7bfb-138">Next steps</span></span>
<span data-ttu-id="e7bfb-139">Merhaba hakkında daha fazla bilgi [Azure AD Connect eşitleme](active-directory-aadconnectsync-whatis.md) yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="e7bfb-139">Learn more about hello [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="e7bfb-140">[Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md) hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="e7bfb-140">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
