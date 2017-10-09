---
title: "Azure AD Connect eşitleme: yanlışlıkla silmeleri engelleme | Microsoft Docs"
description: "Bu konu, hello açıklar Azure AD Connect özelliği (yanlışlıkla silmeleri engelleme) yanlışlıkla silmeleri engelleme."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 6b852cb4-2850-40a1-8280-8724081601f7
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 159597f8354806fcaea1430e0ff84956338592a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-prevent-accidental-deletes"></a><span data-ttu-id="ad1d1-103">Azure AD Connect Eşitleme: Yanlışlıkla Silmeleri Engelleme</span><span class="sxs-lookup"><span data-stu-id="ad1d1-103">Azure AD Connect sync: Prevent accidental deletes</span></span>
<span data-ttu-id="ad1d1-104">Bu konu, hello açıklar Azure AD Connect özelliği (yanlışlıkla silmeleri engelleme) yanlışlıkla silmeleri engelleme.</span><span class="sxs-lookup"><span data-stu-id="ad1d1-104">This topic describes hello prevent accidental deletes (preventing accidental deletions) feature in Azure AD Connect.</span></span>

<span data-ttu-id="ad1d1-105">Azure AD Connect yükleme engellediğinizde yanlışlıkla silmeleri, varsayılan olarak etkindir ve yapılandırılmış toonot izin verme ile 500'den fazla siler.</span><span class="sxs-lookup"><span data-stu-id="ad1d1-105">When installing Azure AD Connect, prevent accidental deletes is enabled by default and configured toonot allow an export with more than 500 deletes.</span></span> <span data-ttu-id="ad1d1-106">Bu özellik, yanlışlıkla yapılandırmadan ve çok sayıda kullanıcı ve diğer nesneleri etkileyecek tooyour şirket içi dizin değiştirir tasarlanmış tooprotect olur.</span><span class="sxs-lookup"><span data-stu-id="ad1d1-106">This feature is designed tooprotect you from accidental configuration changes and changes tooyour on-premises directory that would affect many users and other objects.</span></span>

## <a name="what-is-prevent-accidental-deletes"></a><span data-ttu-id="ad1d1-107">Ne yanlışlıkla silmeleri engelleme olduğu</span><span class="sxs-lookup"><span data-stu-id="ad1d1-107">What is prevent accidental deletes</span></span>
<span data-ttu-id="ad1d1-108">Dahil birçok siler gördüğünüzde yaygın senaryolar:</span><span class="sxs-lookup"><span data-stu-id="ad1d1-108">Common scenarios when you see many deletes include:</span></span>

* <span data-ttu-id="ad1d1-109">Çok değiştirir[filtreleme](active-directory-aadconnectsync-configure-filtering.md) tüm burada [OU](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) veya [etki alanı](active-directory-aadconnectsync-configure-filtering.md#domain-based-filtering) seçildiyse.</span><span class="sxs-lookup"><span data-stu-id="ad1d1-109">Changes too[filtering](active-directory-aadconnectsync-configure-filtering.md) where an entire [OU](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) or [domain](active-directory-aadconnectsync-configure-filtering.md#domain-based-filtering) is unselected.</span></span>
* <span data-ttu-id="ad1d1-110">Bir OU'daki tüm nesneler silinir.</span><span class="sxs-lookup"><span data-stu-id="ad1d1-110">All objects in an OU are deleted.</span></span>
* <span data-ttu-id="ad1d1-111">Bir OU içindeki tüm nesneleri eşitleme için kapsam dışına toobe kabul edilen biçimde adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="ad1d1-111">An OU is renamed so all objects in it are considered toobe out of scope for synchronization.</span></span>

<span data-ttu-id="ad1d1-112">PowerShell ile Merhaba varsayılan değer 500 nesnelerin değiştirilebilir kullanarak `Enable-ADSyncExportDeletionThreshold`.</span><span class="sxs-lookup"><span data-stu-id="ad1d1-112">hello default value of 500 objects can be changed with PowerShell using `Enable-ADSyncExportDeletionThreshold`.</span></span> <span data-ttu-id="ad1d1-113">Bu değer toofit hello boyutu, kuruluşunuzun yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ad1d1-113">You should configure this value toofit hello size of your organization.</span></span> <span data-ttu-id="ad1d1-114">Merhaba eşitleme Zamanlayıcı 30 dakikada bir çalışır olduğundan, hello değer hello 30 dakika içinde görülen siler sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="ad1d1-114">Since hello sync scheduler runs every 30 minutes, hello value is hello number of deletes seen within 30 minutes.</span></span>

<span data-ttu-id="ad1d1-115">Varsa hello dışa aktarma durur ve böyle bir e-posta alırsınız sonra çok sayıda hazırlanan siler toobe tooAzure AD, dışarı:</span><span class="sxs-lookup"><span data-stu-id="ad1d1-115">If there are too many deletes staged toobe exported tooAzure AD, then hello export stops and you receive an email like this:</span></span>

![E-posta yanlışlıkla silmeleri engelleme](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/email.png)

> <span data-ttu-id="ad1d1-117">*Merhaba (teknik kişi). (Zaman) silme hello sayısı (kuruluş adı) için hello yapılandırılmış silme eşiği aşıldı hello kimlik eşitleme hizmeti algıladı. (Sayı) toplam nesneleri çalıştırmak bu kimlik eşitleme silinmek gönderildi. Bu karşıladığında veya (sayı) nesneleri yapılandırılmış hello silme eşik değerini aştı. Bu silme işlemlerini olmalıdır tooprovide onay ihtiyacımız ilerlemeden önce işlenir. Lütfen bu e-posta iletisinde listelenen hello hata hakkında daha fazla bilgi için yanlışlıkla silmeleri engelleme hello bakın.*</span><span class="sxs-lookup"><span data-stu-id="ad1d1-117">*Hello (technical contact). At (time) hello Identity synchronization service detected that hello number of deletions exceeded hello configured deletion threshold for (organization name). A total of (number) objects were sent for deletion in this Identity synchronization run. This met or exceeded hello configured deletion threshold value of (number) objects. We need you tooprovide confirmation that these deletions should be processed before we will proceed. Please see hello preventing accidental deletions for more information about hello error listed in this email message.*</span></span>
>
> 

<span data-ttu-id="ad1d1-118">Ayrıca hello durumunu görebilirsiniz `stopped-deletion-threshold-exceeded` hello baktığınızda **Eşitleme Hizmeti Yöneticisi'ni** hello verme profili için kullanıcı Arabirimi.</span><span class="sxs-lookup"><span data-stu-id="ad1d1-118">You can also see hello status `stopped-deletion-threshold-exceeded` when you look in hello **Synchronization Service Manager** UI for hello Export profile.</span></span>
<span data-ttu-id="ad1d1-119">![Eşitleme Hizmeti Yöneticisi kullanıcı Arabirimi yanlışlıkla silmeleri engelleme](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/syncservicemanager.png)</span><span class="sxs-lookup"><span data-stu-id="ad1d1-119">![Prevent Accidental deletes Sync Service Manager UI](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/syncservicemanager.png)</span></span>

<span data-ttu-id="ad1d1-120">Beklenmeyen olduysa, araştırın ve düzeltici eylemleri gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="ad1d1-120">If this was unexpected, then investigate and take corrective actions.</span></span> <span data-ttu-id="ad1d1-121">nesneler hakkında toobe silinmiş olan toosee hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="ad1d1-121">toosee which objects are about toobe deleted, do hello following:</span></span>

1. <span data-ttu-id="ad1d1-122">Başlat **eşitleme hizmeti** hello Başlat menüsü gelen.</span><span class="sxs-lookup"><span data-stu-id="ad1d1-122">Start **Synchronization Service** from hello Start Menu.</span></span>
2. <span data-ttu-id="ad1d1-123">Çok Git**Bağlayıcılar**.</span><span class="sxs-lookup"><span data-stu-id="ad1d1-123">Go too**Connectors**.</span></span>
3. <span data-ttu-id="ad1d1-124">Select hello bağlayıcı türü olan **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ad1d1-124">Select hello Connector with type **Azure Active Directory**.</span></span>
4. <span data-ttu-id="ad1d1-125">Altında **Eylemler** toohello sağa, select **arama bağlayıcı alanı**.</span><span class="sxs-lookup"><span data-stu-id="ad1d1-125">Under **Actions** toohello right, select **Search Connector Space**.</span></span>
5. <span data-ttu-id="ad1d1-126">Merhaba altında açılır içinde **kapsam**seçin **bağlantısı kesilmiş beri** ve hello son bir saat seçin.</span><span class="sxs-lookup"><span data-stu-id="ad1d1-126">In hello pop-up under **Scope**, select **Disconnected Since** and pick a time in hello past.</span></span> <span data-ttu-id="ad1d1-127">Tıklatın **arama**.</span><span class="sxs-lookup"><span data-stu-id="ad1d1-127">Click **Search**.</span></span> <span data-ttu-id="ad1d1-128">Bu sayfa silinmiş toobe hakkında tüm nesnelerin bir görünümünü sağlar.</span><span class="sxs-lookup"><span data-stu-id="ad1d1-128">This page provides a view of all objects about toobe deleted.</span></span> <span data-ttu-id="ad1d1-129">Her öğe tıklayarak hello nesne hakkında ek bilgi alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ad1d1-129">By clicking each item, you can get additional information about hello object.</span></span> <span data-ttu-id="ad1d1-130">Tıklatarak **sütun ayarı** tooadd ek öznitelikler toobe hello kılavuzunda görünür.</span><span class="sxs-lookup"><span data-stu-id="ad1d1-130">You can also click **Column Setting** tooadd additional attributes toobe visible in hello grid.</span></span>

![Bağlayıcı alanı arama](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/searchcs.png)

<span data-ttu-id="ad1d1-132">Ardından tüm hello siler isterseniz, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="ad1d1-132">If all hello deletes are desired, then do hello following:</span></span>

1. <span data-ttu-id="ad1d1-133">Merhaba PowerShell cmdlet'ini çalıştırın tooretrieve hello geçerli silme eşiği, `Get-ADSyncExportDeletionThreshold`.</span><span class="sxs-lookup"><span data-stu-id="ad1d1-133">tooretrieve hello current deletion threshold, run hello PowerShell cmdlet `Get-ADSyncExportDeletionThreshold`.</span></span> <span data-ttu-id="ad1d1-134">Bir Azure AD genel yönetici hesabı ve parolası belirtin.</span><span class="sxs-lookup"><span data-stu-id="ad1d1-134">Provide an Azure AD Global Administrator account and password.</span></span> <span data-ttu-id="ad1d1-135">Merhaba varsayılan değer 500'dür.</span><span class="sxs-lookup"><span data-stu-id="ad1d1-135">hello default value is 500.</span></span>
2. <span data-ttu-id="ad1d1-136">tootemporarily bu korumayı devre dışı bırakın ve Git, hello PowerShell cmdlet'ini çalıştırın bu siler izin verin: `Disable-ADSyncExportDeletionThreshold`.</span><span class="sxs-lookup"><span data-stu-id="ad1d1-136">tootemporarily disable this protection and let those deletes go through, run hello PowerShell cmdlet: `Disable-ADSyncExportDeletionThreshold`.</span></span> <span data-ttu-id="ad1d1-137">Bir Azure AD genel yönetici hesabı ve parolası belirtin.</span><span class="sxs-lookup"><span data-stu-id="ad1d1-137">Provide an Azure AD Global Administrator account and password.</span></span>
   <span data-ttu-id="ad1d1-138">![Kimlik Bilgileri](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/credentials.png)</span><span class="sxs-lookup"><span data-stu-id="ad1d1-138">![Credentials](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/credentials.png)</span></span>
3. <span data-ttu-id="ad1d1-139">Hello Azure Active Directory Bağlayıcısı seçiliyken hello bir eylem seçin **çalıştırmak** seçip **verme**.</span><span class="sxs-lookup"><span data-stu-id="ad1d1-139">With hello Azure Active Directory Connector still selected, select hello action **Run** and select **Export**.</span></span>
4. <span data-ttu-id="ad1d1-140">toore etkinleştir hello koruma, Hello PowerShell cmdlet'ini çalıştırın: `Enable-ADSyncExportDeletionThreshold -DeletionThreshold 500`.</span><span class="sxs-lookup"><span data-stu-id="ad1d1-140">toore-enable hello protection, run hello PowerShell cmdlet: `Enable-ADSyncExportDeletionThreshold -DeletionThreshold 500`.</span></span> <span data-ttu-id="ad1d1-141">500 hello geçerli silme eşiği alınırken fark hello değerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="ad1d1-141">Replace 500 with hello value you noticed when retrieving hello current deletion threshold.</span></span> <span data-ttu-id="ad1d1-142">Bir Azure AD genel yönetici hesabı ve parolası belirtin.</span><span class="sxs-lookup"><span data-stu-id="ad1d1-142">Provide an Azure AD Global Administrator account and password.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ad1d1-143">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ad1d1-143">Next steps</span></span>
<span data-ttu-id="ad1d1-144">**Genel bakış konuları**</span><span class="sxs-lookup"><span data-stu-id="ad1d1-144">**Overview topics**</span></span>

* [<span data-ttu-id="ad1d1-145">Azure AD Connect eşitleme: anlamak ve eşitleme özelleştirme</span><span class="sxs-lookup"><span data-stu-id="ad1d1-145">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="ad1d1-146">Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="ad1d1-146">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
