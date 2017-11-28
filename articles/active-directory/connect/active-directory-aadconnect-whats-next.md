---
title: "Azure AD Connect: Sonraki adımlar ve nasıl toomanage Azure AD Connect | Microsoft Docs"
description: "Nasıl tooextend hello varsayılan yapılandırması ve işletimsel görevler için Azure AD Connect öğrenin."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: c18bee36-aebf-4281-b8fc-3fe14116f1a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 4404aaff24d54d76b83baca3b331a6a250ba4c03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="next-steps-and-how-toomanage-azure-ad-connect"></a><span data-ttu-id="0afff-103">Sonraki adımlar ve nasıl toomanage Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="0afff-103">Next steps and how toomanage Azure AD Connect</span></span>
<span data-ttu-id="0afff-104">Bu makale toocustomize Azure Active Directory (Azure AD) Bağlan toomeet Hello işletimsel yordamları, kuruluşunuzun ihtiyaçları ve gereksinimleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="0afff-104">Use hello operational procedures in this article toocustomize Azure Active Directory (Azure AD) Connect toomeet your organization's needs and requirements.</span></span>  

## <a name="add-additional-sync-admins"></a><span data-ttu-id="0afff-105">Ek eşitleme yöneticileri ekleyin</span><span class="sxs-lookup"><span data-stu-id="0afff-105">Add additional sync admins</span></span>
<span data-ttu-id="0afff-106">Varsayılan olarak, yükleme ve yerel Yöneticiler hello yalnızca hello kullanıcının mümkün toomanage yüklü hello eşitleme altyapısı etkilenir.</span><span class="sxs-lookup"><span data-stu-id="0afff-106">By default, only hello user who did hello installation and local admins are able toomanage hello installed sync engine.</span></span> <span data-ttu-id="0afff-107">Diğer kişilere toobe mümkün tooaccess için ve hello eşitleme altyapısı yönetmek, hello yerel sunucuda ADSyncAdmins adlı hello grubunu bulun ve toothis grubunu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0afff-107">For additional people toobe able tooaccess and manage hello sync engine, locate hello group named ADSyncAdmins on hello local server and add them toothis group.</span></span>

## <a name="assign-licenses-tooazure-ad-premium-and-enterprise-mobility-suite-users"></a><span data-ttu-id="0afff-108">Kullanıcıların AD Premium ve Enterprise Mobility Suite lisansları tooAzure atayın</span><span class="sxs-lookup"><span data-stu-id="0afff-108">Assign licenses tooAzure AD Premium and Enterprise Mobility Suite users</span></span>
<span data-ttu-id="0afff-109">Kullanıcılarınızın silinmiş göre toohello bulut eşitlenen tooassign gerekir bunları bunlar Office 365 gibi bulut uygulamalarıyla kullanmaya başlayabilirsiniz için bir lisans.</span><span class="sxs-lookup"><span data-stu-id="0afff-109">Now that your users have been synchronized toohello cloud, you need tooassign them a license so they can get going with cloud apps such as Office 365.</span></span>

### <a name="tooassign-an-azure-ad-premium-or-enterprise-mobility-suite-license"></a><span data-ttu-id="0afff-110">bir Azure AD Premium veya Enterprise Mobility Suite lisansı tooassign</span><span class="sxs-lookup"><span data-stu-id="0afff-110">tooassign an Azure AD Premium or Enterprise Mobility Suite License</span></span>

1. <span data-ttu-id="0afff-111">İçinde toohello Azure portalında bir yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="0afff-111">Sign in toohello Azure portal as an admin.</span></span>
2. <span data-ttu-id="0afff-112">Merhaba solda seçin **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0afff-112">On hello left, select **Active Directory**.</span></span>
3. <span data-ttu-id="0afff-113">Merhaba üzerinde **Active Directory** sayfasında, Yukarı tooset istediğiniz hello kullanıcılara hello dizini çift tıklatın.</span><span class="sxs-lookup"><span data-stu-id="0afff-113">On hello **Active Directory** page, double-click hello directory that has hello users you want tooset up.</span></span>
4. <span data-ttu-id="0afff-114">Merhaba hello dizin sayfanın en üstünde, seçin **lisansları**.</span><span class="sxs-lookup"><span data-stu-id="0afff-114">At hello top of hello directory page, select **Licenses**.</span></span>
5. <span data-ttu-id="0afff-115">Merhaba üzerinde **lisansları** sayfasında, **Active Directory Premium** veya **Enterprise Mobility Suite**ve ardından **atamak**.</span><span class="sxs-lookup"><span data-stu-id="0afff-115">On hello **Licenses** page, select **Active Directory Premium** or **Enterprise Mobility Suite**, and then click **Assign**.</span></span>
6. <span data-ttu-id="0afff-116">Merhaba iletişim kutusunda, tooassign lisansları istediğiniz ve hello onay işareti simgesi toosave hello değişiklikleri ardından hello kullanıcıları seçin.</span><span class="sxs-lookup"><span data-stu-id="0afff-116">In hello dialog box, select hello users you want tooassign licenses to, and then click hello check mark icon toosave hello changes.</span></span>

## <a name="verify-hello-scheduled-synchronization-task"></a><span data-ttu-id="0afff-117">Merhaba zamanlanmış eşitleme görevi doğrulayın</span><span class="sxs-lookup"><span data-stu-id="0afff-117">Verify hello scheduled synchronization task</span></span>
<span data-ttu-id="0afff-118">Hello Azure portal toocheck hello bir eşitleme durumunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="0afff-118">Use hello Azure portal toocheck hello status of a synchronization.</span></span>

### <a name="tooverify-hello-scheduled-synchronization-task"></a><span data-ttu-id="0afff-119">tooverify hello zamanlanmış eşitleme görevi</span><span class="sxs-lookup"><span data-stu-id="0afff-119">tooverify hello scheduled synchronization task</span></span>
1. <span data-ttu-id="0afff-120">İçinde toohello Azure portalında bir yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="0afff-120">Sign in toohello Azure portal as an admin.</span></span>
2. <span data-ttu-id="0afff-121">Merhaba solda seçin **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0afff-121">On hello left, select **Active Directory**.</span></span>
3. <span data-ttu-id="0afff-122">Merhaba üzerinde **Active Directory** sayfasında, Yukarı tooset istediğiniz hello kullanıcılara hello dizini çift tıklatın.</span><span class="sxs-lookup"><span data-stu-id="0afff-122">On hello **Active Directory** page, double-click hello directory that has hello users you want tooset up.</span></span>
4. <span data-ttu-id="0afff-123">Merhaba hello dizin sayfanın en üstünde, seçin **dizin tümleştirme**.</span><span class="sxs-lookup"><span data-stu-id="0afff-123">At hello top of hello directory page, select **Directory Integration**.</span></span>
5. <span data-ttu-id="0afff-124">Altında **yerel active directory ile tümleştirme**, Not hello son eşitleme zamanı.</span><span class="sxs-lookup"><span data-stu-id="0afff-124">Under **integration with local active directory**, note hello last sync time.</span></span>

<span data-ttu-id="0afff-125"><center>![Dizin eşitleme zamanı](./media/active-directory-aadconnect-whats-next/verify.png)</center></span><span class="sxs-lookup"><span data-stu-id="0afff-125"><center>![Directory sync time](./media/active-directory-aadconnect-whats-next/verify.png)</center></span></span>

## <a name="start-a-scheduled-synchronization-task"></a><span data-ttu-id="0afff-126">Zamanlanan eşitleme görevi Başlat</span><span class="sxs-lookup"><span data-stu-id="0afff-126">Start a scheduled synchronization task</span></span>
<span data-ttu-id="0afff-127">Eşitleme görevi toorun gerekiyorsa, hello Azure AD Connect Sihirbazı yeniden çalıştırarak bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0afff-127">If you need toorun a synchronization task, you can do this by running through hello Azure AD Connect wizard again.</span></span>  <span data-ttu-id="0afff-128">Azure AD kimlik bilgilerinizi tooprovide gerekir.</span><span class="sxs-lookup"><span data-stu-id="0afff-128">You need tooprovide your Azure AD credentials.</span></span>  <span data-ttu-id="0afff-129">Merhaba Hello Sihirbazı'nda seçin **eşitleme seçeneklerini özelleştirme** tıklayın ve görev **sonraki** toomove hello Sihirbazı aracılığıyla.</span><span class="sxs-lookup"><span data-stu-id="0afff-129">In hello wizard, select hello **Customize synchronization options** task, and click **Next** toomove through hello wizard.</span></span> <span data-ttu-id="0afff-130">Bu hello Hello sonunda olun **hello ilk yapılandırma tamamlandıktan hemen sonra hello eşitleme işlemini başlatmak** kutusu seçilidir.</span><span class="sxs-lookup"><span data-stu-id="0afff-130">At hello end, ensure that hello **Start hello synchronization process as soon as hello initial configuration completes** box is selected.</span></span>

<span data-ttu-id="0afff-131"><center>![Eşitlemeyi Başlat](./media/active-directory-aadconnect-whats-next/startsynch.png)</center></span><span class="sxs-lookup"><span data-stu-id="0afff-131"><center>![Start synchronization](./media/active-directory-aadconnect-whats-next/startsynch.png)</center></span></span>

<span data-ttu-id="0afff-132">Hello Azure AD Connect eşitleme Zamanlayıcı hakkında daha fazla bilgi için bkz: [Azure AD Connect Zamanlayıcı](active-directory-aadconnectsync-feature-scheduler.md).</span><span class="sxs-lookup"><span data-stu-id="0afff-132">For more information on hello Azure AD Connect sync Scheduler, see [Azure AD Connect Scheduler](active-directory-aadconnectsync-feature-scheduler.md).</span></span>

## <a name="additional-tasks-available-in-azure-ad-connect"></a><span data-ttu-id="0afff-133">Azure AD Connect kullanılabilir ek görevler</span><span class="sxs-lookup"><span data-stu-id="0afff-133">Additional tasks available in Azure AD Connect</span></span>
<span data-ttu-id="0afff-134">Azure AD Connect ilk, yüklemeden sonra her zaman hello Sihirbazı'nı yeniden hello Azure AD Connect başlangıç sayfası veya Masaüstü kısayoldan başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0afff-134">After your initial installation of Azure AD Connect, you can always start hello wizard again from hello Azure AD Connect start page or desktop shortcut.</span></span>  <span data-ttu-id="0afff-135">Merhaba Sihirbazı aracılığıyla yeniden giderek ek görevler hello formunda yeni bazı seçenekler sunar fark edeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="0afff-135">You will notice that going through hello wizard again provides some new options in hello form of additional tasks.</span></span>  

<span data-ttu-id="0afff-136">Merhaba aşağıdaki tabloda bu görevleri özetini ve her görevin kısa bir açıklamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="0afff-136">hello following table provides a summary of these tasks and a brief description of each task.</span></span>

![Ek görevler listesi](./media/active-directory-aadconnect-whats-next/addtasks.png)

| <span data-ttu-id="0afff-138">Ek görevi</span><span class="sxs-lookup"><span data-stu-id="0afff-138">Additional task</span></span> | <span data-ttu-id="0afff-139">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0afff-139">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0afff-140">**Görünüm hello seçili senaryosu**</span><span class="sxs-lookup"><span data-stu-id="0afff-140">**View hello selected scenario**</span></span> |<span data-ttu-id="0afff-141">Geçerli Azure AD Connect çözümünüzü görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="0afff-141">View your current Azure AD Connect solution.</span></span>  <span data-ttu-id="0afff-142">Bu eşitlenmiş genel ayarları içeren dizinler ve eşitleme ayarları.</span><span class="sxs-lookup"><span data-stu-id="0afff-142">This includes general settings, synchronized directories, and sync settings.</span></span> |
| <span data-ttu-id="0afff-143">**Eşitleme seçeneklerini özelleştirme**</span><span class="sxs-lookup"><span data-stu-id="0afff-143">**Customize synchronization options**</span></span> |<span data-ttu-id="0afff-144">Ek Active Directory ormanları toohello yapılandırma ekleme ya da kullanıcı, Grup, cihaz veya parola geri yazma gibi eşitleme seçeneklerini etkinleştirme gibi hello geçerli yapılandırmasını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="0afff-144">Change hello current configuration like adding additional Active Directory forests toohello configuration, or enabling sync options such as user, group, device, or password write-back.</span></span> |
| <span data-ttu-id="0afff-145">**Hazırlama modunu etkinleştir**</span><span class="sxs-lookup"><span data-stu-id="0afff-145">**Enable Staging Mode**</span></span> |<span data-ttu-id="0afff-146">Hemen eşitlenmemiş ve değil aşaması bilgilerini tooAzure AD veya şirket içi Active Directory verildi.</span><span class="sxs-lookup"><span data-stu-id="0afff-146">Stage information that is not immediately synchronized and is not exported tooAzure AD or on-premises Active Directory.</span></span>  <span data-ttu-id="0afff-147">Bu özellik ile ortaya çıkmadan önce hello eşitlemeler önizleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0afff-147">With this feature, you can preview hello synchronizations before they occur.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0afff-148">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0afff-148">Next steps</span></span>
<span data-ttu-id="0afff-149">Daha fazla bilgi edinmek [şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="0afff-149">Learn more about [integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
