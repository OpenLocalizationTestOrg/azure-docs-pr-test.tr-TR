---
title: "hello Azure AD eşitleme hizmeti Yöneticisi kullanıcı Arabirimi aaaConnectors | Microsoft Docs"
description: "Merhaba bağlayıcılar sekmesinde hello Synchronization Service Manager için Azure AD Connect anlayın."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 60f1d979-8e6d-4460-aaab-747fffedfc1e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c0969630313178b1e299385b1289360c8f787cb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-connectors-with-hello-azure-ad-connect-sync-service-manager"></a><span data-ttu-id="4584c-103">Bağlayıcıları hello Azure AD Connect Eşitleme Hizmeti Yöneticisi ile kullanma</span><span class="sxs-lookup"><span data-stu-id="4584c-103">Using connectors with hello Azure AD Connect Sync Service Manager</span></span>

![Eşitleme Hizmeti Yöneticisi](./media/active-directory-aadconnectsync-service-manager-ui/connectors.png)

<span data-ttu-id="4584c-105">Merhaba bağlayıcılar sekmesi tüm sistemler hello eşitleme altyapısı bağlı kullanılan toomanage aynıdır.</span><span class="sxs-lookup"><span data-stu-id="4584c-105">hello Connectors tab is used toomanage all systems hello sync engine is connected to.</span></span>

## <a name="connector-actions"></a><span data-ttu-id="4584c-106">Bağlayıcı Eylemler</span><span class="sxs-lookup"><span data-stu-id="4584c-106">Connector actions</span></span>
| <span data-ttu-id="4584c-107">Eylem</span><span class="sxs-lookup"><span data-stu-id="4584c-107">Action</span></span> | <span data-ttu-id="4584c-108">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4584c-108">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="4584c-109">Oluştur</span><span class="sxs-lookup"><span data-stu-id="4584c-109">Create</span></span> |<span data-ttu-id="4584c-110">Kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="4584c-110">Do not use.</span></span> <span data-ttu-id="4584c-111">Tooadditional AD ormanına bağlanmak için hello Yükleme Sihirbazı'nı kullanın.</span><span class="sxs-lookup"><span data-stu-id="4584c-111">For connecting tooadditional AD forests, use hello installation wizard.</span></span> |
| <span data-ttu-id="4584c-112">Özellikler</span><span class="sxs-lookup"><span data-stu-id="4584c-112">Properties</span></span> |<span data-ttu-id="4584c-113">Etki alanı ve OU filtreleme için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="4584c-113">Used for domain and OU filtering.</span></span> |
| [<span data-ttu-id="4584c-114">Silme</span><span class="sxs-lookup"><span data-stu-id="4584c-114">Delete</span></span>](#delete) |<span data-ttu-id="4584c-115">Kullanılan tooeither hello veri hello bağlayıcı alanı veya ormanda toodelete bağlantı tooa silin.</span><span class="sxs-lookup"><span data-stu-id="4584c-115">Used tooeither delete hello data in hello connector space or toodelete connection tooa forest.</span></span> |
| [<span data-ttu-id="4584c-116">Çalıştırma profillerini Yapılandır</span><span class="sxs-lookup"><span data-stu-id="4584c-116">Configure Run Profiles</span></span>](#configure-run-profiles) |<span data-ttu-id="4584c-117">Filtreleme, hiçbir şey etki alanı dışındaki tooconfigure burada.</span><span class="sxs-lookup"><span data-stu-id="4584c-117">Except for domain filtering, nothing tooconfigure here.</span></span> <span data-ttu-id="4584c-118">Bu eylemi kullanabilirsiniz zaten yapılandırılmış toosee farklı çalıştır profili.</span><span class="sxs-lookup"><span data-stu-id="4584c-118">You can use this action toosee already configured run profiles.</span></span> |
| <span data-ttu-id="4584c-119">Çalıştırın</span><span class="sxs-lookup"><span data-stu-id="4584c-119">Run</span></span> |<span data-ttu-id="4584c-120">Bir kerelik Çalıştır profilini toostart kullanılır.</span><span class="sxs-lookup"><span data-stu-id="4584c-120">Used toostart a one-off run of a profile.</span></span> |
| <span data-ttu-id="4584c-121">Durdur</span><span class="sxs-lookup"><span data-stu-id="4584c-121">Stop</span></span> |<span data-ttu-id="4584c-122">Çalışmakta olan bir profili bir bağlayıcı durdurur.</span><span class="sxs-lookup"><span data-stu-id="4584c-122">Stops a Connector currently running a profile.</span></span> |
| <span data-ttu-id="4584c-123">Bağlayıcı dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="4584c-123">Export Connector</span></span> |<span data-ttu-id="4584c-124">Kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="4584c-124">Do not use.</span></span> |
| <span data-ttu-id="4584c-125">İçeri aktarma Bağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="4584c-125">Import Connector</span></span> |<span data-ttu-id="4584c-126">Kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="4584c-126">Do not use.</span></span> |
| <span data-ttu-id="4584c-127">Güncelleştirme Bağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="4584c-127">Update Connector</span></span> |<span data-ttu-id="4584c-128">Kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="4584c-128">Do not use.</span></span> |
| <span data-ttu-id="4584c-129">Şema Yenile</span><span class="sxs-lookup"><span data-stu-id="4584c-129">Refresh Schema</span></span> |<span data-ttu-id="4584c-130">Merhaba önbellekteki şema yeniler.</span><span class="sxs-lookup"><span data-stu-id="4584c-130">Refreshes hello cached schema.</span></span> <span data-ttu-id="4584c-131">Bu tercih edilen toouse hello hello Yükleme Sihirbazı'nda bunun yerine, bu yana, aynı zamanda güncelleştirmeleri kuralları eşitleme seçenektir.</span><span class="sxs-lookup"><span data-stu-id="4584c-131">It is preferred toouse hello option in hello installation wizard instead, since that also updates sync rules.</span></span> |
| [<span data-ttu-id="4584c-132">Bağlayıcı alanı arama</span><span class="sxs-lookup"><span data-stu-id="4584c-132">Search Connector Space</span></span>](#search-connector-space) |<span data-ttu-id="4584c-133">Kullanılan toofind nesneleri ve çok[bir nesne ve verileri hello sistemi aracılığıyla izleyin](#follow-an-object-and-its-data-through-the-system).</span><span class="sxs-lookup"><span data-stu-id="4584c-133">Used toofind objects and too[Follow an object and its data through hello system](#follow-an-object-and-its-data-through-the-system).</span></span> |

### <a name="delete"></a><span data-ttu-id="4584c-134">Sil</span><span class="sxs-lookup"><span data-stu-id="4584c-134">Delete</span></span>
<span data-ttu-id="4584c-135">Merhaba silme eylemi iki farklı işlemler için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="4584c-135">hello delete action is used for two different things.</span></span>  
![Eşitleme Hizmeti Yöneticisi](./media/active-directory-aadconnectsync-service-manager-ui/connectordelete.png)

<span data-ttu-id="4584c-137">Merhaba seçeneği **silme yalnızca bağlayıcı alanı** Koru hello yapılandırma ancak tüm verileri kaldırır.</span><span class="sxs-lookup"><span data-stu-id="4584c-137">hello option **Delete connector space only** removes all data, but keep hello configuration.</span></span>

<span data-ttu-id="4584c-138">Merhaba seçeneği **bağlayıcı silin ve bağlayıcı alanı** hello verileri ve hello yapılandırma kaldırır.</span><span class="sxs-lookup"><span data-stu-id="4584c-138">hello option **Delete Connector and connector space** removes hello data and hello configuration.</span></span> <span data-ttu-id="4584c-139">Tooconnect tooa orman artık istemediğinizde bu seçenek kullanılır.</span><span class="sxs-lookup"><span data-stu-id="4584c-139">This option is used when you do not want tooconnect tooa forest anymore.</span></span>

<span data-ttu-id="4584c-140">Her iki seçenek, tüm nesneleri eşitlemek ve hello meta veri deposu nesne güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="4584c-140">Both options sync all objects and update hello metaverse objects.</span></span> <span data-ttu-id="4584c-141">Bu işlem uzun süren bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="4584c-141">This action is a long running operation.</span></span>

### <a name="configure-run-profiles"></a><span data-ttu-id="4584c-142">Çalıştırma profillerini Yapılandır</span><span class="sxs-lookup"><span data-stu-id="4584c-142">Configure Run Profiles</span></span>
<span data-ttu-id="4584c-143">Bu seçenek çalıştırma profili için bir bağlayıcı yapılandırılmış toosee hello sağlar.</span><span class="sxs-lookup"><span data-stu-id="4584c-143">This option allows you toosee hello run profiles configured for a Connector.</span></span>

![Eşitleme Hizmeti Yöneticisi](./media/active-directory-aadconnectsync-service-manager-ui/configurerunprofiles.png)

### <a name="search-connector-space"></a><span data-ttu-id="4584c-145">Bağlayıcı alanı arama</span><span class="sxs-lookup"><span data-stu-id="4584c-145">Search Connector Space</span></span>
<span data-ttu-id="4584c-146">Merhaba arama bağlayıcı alanı eylemi yararlı toofind nesneleri ve veri sorunlarını giderme.</span><span class="sxs-lookup"><span data-stu-id="4584c-146">hello search connector space action is useful toofind objects and troubleshoot data issues.</span></span>

![Eşitleme Hizmeti Yöneticisi](./media/active-directory-aadconnectsync-service-manager-ui/cssearch.png)

<span data-ttu-id="4584c-148">Başlangıç seçerek bir **kapsam**.</span><span class="sxs-lookup"><span data-stu-id="4584c-148">Start by selecting a **scope**.</span></span> <span data-ttu-id="4584c-149">Bağlı veri (RDN, DN, bağlayıcı, alt ağacı), arama yapabilirsiniz veya durum hello nesnesinin (tüm diğer seçenekleri için).</span><span class="sxs-lookup"><span data-stu-id="4584c-149">You can search based on data (RDN, DN, Anchor, Sub-Tree), or state of hello object (all other options).</span></span>  
<span data-ttu-id="4584c-150">![Eşitleme Hizmeti Yöneticisi](./media/active-directory-aadconnectsync-service-manager-ui/cssearchscope.png)</span><span class="sxs-lookup"><span data-stu-id="4584c-150">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchscope.png)</span></span>  
<span data-ttu-id="4584c-151">Örneğin bir alt ağacı arama yaparsanız, bir OU'daki tüm nesneleri alın.</span><span class="sxs-lookup"><span data-stu-id="4584c-151">If you for example do a Sub-Tree search, you get all objects in one OU.</span></span>  
<span data-ttu-id="4584c-152">![Eşitleme Hizmeti Yöneticisi](./media/active-directory-aadconnectsync-service-manager-ui/cssearchsubtree.png)</span><span class="sxs-lookup"><span data-stu-id="4584c-152">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchsubtree.png)</span></span>  
<span data-ttu-id="4584c-153">Bu kılavuzdan nesneyi seçin, seçin **özellikleri**, ve [izleyerek](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md) hello meta veri deposu, aracılığıyla hello kaynak bağlayıcı alanı ve toohello hedef bağlayıcı alanı.</span><span class="sxs-lookup"><span data-stu-id="4584c-153">From this grid you can select an object, select **properties**, and [follow it](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md) from hello source connector space, through hello metaverse, and toohello target connector space.</span></span>

### <a name="changing-hello-ad-ds-account-password"></a><span data-ttu-id="4584c-154">Merhaba AD DS hesap parolasını değiştirme</span><span class="sxs-lookup"><span data-stu-id="4584c-154">Changing hello AD DS account password</span></span>
<span data-ttu-id="4584c-155">Merhaba hesap parolasını değiştirmek, hello eşitleme hizmeti artık mümkün tooimport/dışarı aktarma değişiklikleri tooon içi olacaktır AD.</span><span class="sxs-lookup"><span data-stu-id="4584c-155">If you change hello account password, hello Synchronization Service will no longer be able tooimport/export changes tooon-premises AD.</span></span>   <span data-ttu-id="4584c-156">Merhaba aşağıdakileri görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="4584c-156">You may see hello following:</span></span>

- <span data-ttu-id="4584c-157">Merhaba içeri/dışarı aktarma adım hello AD Bağlayıcısı için "-start-kimlik bilgileri yok" hatası ile başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="4584c-157">hello import/export step for hello AD connector fails with "no-start-credentials" error.</span></span>
- <span data-ttu-id="4584c-158">"Windows Olay Görüntüleyicisi altında hello uygulama olay günlüğüne olay kimliği 6000 ve ileti hatayla Merhaba kimlik bilgileri geçersiz olduğundan yönetim"Aracısı contoso.com başarısız oldu"toorun. Hello ifadesini" içerip</span><span class="sxs-lookup"><span data-stu-id="4584c-158">Under Windows Event Viewer, hello application event log contains an error with Event ID 6000 and message “hello management agent “contoso.com” failed toorun because hello credentials were invalid.”</span></span>

<span data-ttu-id="4584c-159">tooresolve hello vermek, hello aşağıdakileri kullanarak güncelleştirme hello AD DS kullanıcı hesabı:</span><span class="sxs-lookup"><span data-stu-id="4584c-159">tooresolve hello issue, update hello AD DS user account using hello following:</span></span>


1. <span data-ttu-id="4584c-160">Merhaba Eşitleme Hizmeti Yöneticisi'ni (Başlangıç → eşitleme hizmeti) başlatın.</span><span class="sxs-lookup"><span data-stu-id="4584c-160">Start hello Synchronization Service Manager (START → Synchronization Service).</span></span>
</br><span data-ttu-id="4584c-161">![Eşitleme Hizmeti Yöneticisi](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span><span class="sxs-lookup"><span data-stu-id="4584c-161">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span></span>
2. <span data-ttu-id="4584c-162">Toohello Git **Bağlayıcılar** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="4584c-162">Go toohello **Connectors** tab.</span></span>
3. <span data-ttu-id="4584c-163">Merhaba yapılandırılmış toouse hello AD DS hesabı olan AD Bağlayıcısı seçin.</span><span class="sxs-lookup"><span data-stu-id="4584c-163">Select hello AD Connector which is configured toouse hello AD DS account.</span></span>
4. <span data-ttu-id="4584c-164">Eylemler altında seçin **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="4584c-164">Under Actions, select **Properties**.</span></span>
5. <span data-ttu-id="4584c-165">Merhaba açılan iletişim kutusunda Bağlan tooActive Directory ormanı seçin:</span><span class="sxs-lookup"><span data-stu-id="4584c-165">In hello pop-up dialog, select Connect tooActive Directory Forest:</span></span>
6. <span data-ttu-id="4584c-166">Merhaba orman adı gösterir hello karşılık gelen şirket içi AD.</span><span class="sxs-lookup"><span data-stu-id="4584c-166">hello Forest name indicates hello corresponding on-prem AD.</span></span>
7. <span data-ttu-id="4584c-167">Eşitleme için kullanılan hello AD DS hesap Hello kullanıcı adı gösterir.</span><span class="sxs-lookup"><span data-stu-id="4584c-167">hello User name indicates hello AD DS account used for synchronization.</span></span>
8. <span data-ttu-id="4584c-168">Yeni bir parola Hello hello AD DS hesabının hello parola metin kutusuna girin ![Azure AD Connect eşitleme şifreleme anahtarı yardımcı programı](media/active-directory-aadconnectsync-encryption-key/key6.png)</span><span class="sxs-lookup"><span data-stu-id="4584c-168">Enter hello new password of hello AD DS account in hello Password textbox ![Azure AD Connect Sync Encryption Key Utility](media/active-directory-aadconnectsync-encryption-key/key6.png)</span></span>
9. <span data-ttu-id="4584c-169">Tamam toosave hello yeni parola ve hello eşitleme hizmeti tooremove hello eski parola bellek önbelleğinden yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="4584c-169">Click OK toosave hello new password and restart hello Synchronization Service tooremove hello old password from memory cache.</span></span>



## <a name="next-steps"></a><span data-ttu-id="4584c-170">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4584c-170">Next steps</span></span>
<span data-ttu-id="4584c-171">Merhaba hakkında daha fazla bilgi [Azure AD Connect eşitleme](active-directory-aadconnectsync-whatis.md) yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="4584c-171">Learn more about hello [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="4584c-172">[Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md) hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="4584c-172">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
