---
title: "Yeniden çalıştırarak hello Azure AD Connect Yükleme Sihirbazı'nı | Microsoft Docs"
description: "Merhaba Yükleme Sihirbazı'nı hello ikinci çalıştırdığınızda nasıl çalıştığını açıklar."
keywords: "Hello Azure AD Connect Yükleme Sihirbazı, ikinci çalıştırdığınızda bakım ayarlarını hello yapılandırmanıza olanak sağlar"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: d800214e-e591-4297-b9b5-d0b1581cc36a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 83cc74aca471ef9b4f65f7f3582e3e48d3d81cfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-running-hello-installation-wizard-a-second-time"></a><span data-ttu-id="7f620-104">Azure AD Connect eşitleme: ikinci kez hello yükleme sihirbazını çalıştırma</span><span class="sxs-lookup"><span data-stu-id="7f620-104">Azure AD Connect sync: Running hello installation wizard a second time</span></span>
<span data-ttu-id="7f620-105">Merhaba hello Azure AD Connect Yükleme Sihirbazı, çalıştırdığınız ilk kez onu, nasıl anlatan tooconfigure yüklemenizi.</span><span class="sxs-lookup"><span data-stu-id="7f620-105">hello first time you run hello Azure AD Connect installation wizard, it walks you through how tooconfigure your installation.</span></span> <span data-ttu-id="7f620-106">Merhaba Yükleme Sihirbazı'nı yeniden çalıştırın, Bakım seçenekleri sunar.</span><span class="sxs-lookup"><span data-stu-id="7f620-106">If you run hello installation wizard again, it offers options for maintenance.</span></span>

<span data-ttu-id="7f620-107">Merhaba Yükleme Sihirbazı'nı adlı hello Başlat menüsünde bulabilirsiniz **Azure AD Connect**.</span><span class="sxs-lookup"><span data-stu-id="7f620-107">You can find hello installation wizard in hello start menu named **Azure AD Connect**.</span></span>

![Başlat menüsü](./media/active-directory-aadconnectsync-installation-wizard/startmenu.png)

<span data-ttu-id="7f620-109">Merhaba Yükleme Sihirbazı'nı başlattığınızda, bu seçenekleri içeren bir sayfa görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="7f620-109">When you start hello installation wizard, you see a page with these options:</span></span>

![Ek görevler listesi sayfası](./media/active-directory-aadconnectsync-installation-wizard/additionaltasks.png)

<span data-ttu-id="7f620-111">Azure AD Connect ile ADFS yüklediyseniz daha da fazla seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="7f620-111">If you have installed ADFS with Azure AD Connect, you have even more options.</span></span> <span data-ttu-id="7f620-112">Merhaba sahip ADFS belgelenmiştir için ek seçenekler [ADFS Yönetim](active-directory-aadconnect-federation-management.md#manage-ad-fs).</span><span class="sxs-lookup"><span data-stu-id="7f620-112">hello additional options you have for ADFS are documented in [ADFS management](active-directory-aadconnect-federation-management.md#manage-ad-fs).</span></span>

<span data-ttu-id="7f620-113">Merhaba görevlerinden birini seçin ve tıklatın **sonraki** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="7f620-113">Select one of hello tasks and click **Next** toocontinue.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7f620-114">Merhaba Yükleme Sihirbazı'nı açın sahip olsa da, hello eşitleme Altyapısı'ndaki tüm işlemleri askıya alınır.</span><span class="sxs-lookup"><span data-stu-id="7f620-114">While you have hello installation wizard open, all operations in hello sync engine are suspended.</span></span> <span data-ttu-id="7f620-115">Yapılandırma değişiklikleri tamamladıktan hemen sonra hello yükleme sihirbazını kapatın emin olun.</span><span class="sxs-lookup"><span data-stu-id="7f620-115">Make sure you close hello installation wizard as soon as you have completed your configuration changes.</span></span>
>
>

## <a name="view-current-configuration"></a><span data-ttu-id="7f620-116">Geçerli yapılandırmayı görüntüle</span><span class="sxs-lookup"><span data-stu-id="7f620-116">View current configuration</span></span>
<span data-ttu-id="7f620-117">Bu seçenek şu anda yapılandırılmış seçeneklerinizi hızlı bir görünümünü sağlar.</span><span class="sxs-lookup"><span data-stu-id="7f620-117">This option gives you a quick view of your currently configured options.</span></span>

![Tüm seçenekler ve durumlarına Listesi Sayfası](./media/active-directory-aadconnectsync-installation-wizard/viewconfig.png)

<span data-ttu-id="7f620-119">Tıklatın **önceki** toogo geri.</span><span class="sxs-lookup"><span data-stu-id="7f620-119">Click **Previous** toogo back.</span></span> <span data-ttu-id="7f620-120">Seçerseniz **çıkış**, hello Yükleme Sihirbazı'nı kapatın.</span><span class="sxs-lookup"><span data-stu-id="7f620-120">If you select **Exit**, you close hello installation wizard.</span></span>

## <a name="customize-synchronization-options"></a><span data-ttu-id="7f620-121">Eşitleme seçeneklerini özelleştirme</span><span class="sxs-lookup"><span data-stu-id="7f620-121">Customize synchronization options</span></span>
<span data-ttu-id="7f620-122">Bu seçenek kullanılan toomake değişiklikleri toohello eşitleme yapılandırmadır.</span><span class="sxs-lookup"><span data-stu-id="7f620-122">This option is used toomake changes toohello sync configuration.</span></span> <span data-ttu-id="7f620-123">Bir alt kümesini hello özel yapılandırma yükleme yolu seçeneklerinden bakın.</span><span class="sxs-lookup"><span data-stu-id="7f620-123">You see a subset of options from hello custom configuration installation path.</span></span> <span data-ttu-id="7f620-124">Hızlı yükleme başlangıçta kullanılan olsa bile, bu seçenek görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="7f620-124">You see this option even if you used express installation initially.</span></span>

* <span data-ttu-id="7f620-125">[Daha fazla dizinler eklemek](active-directory-aadconnect-get-started-custom.md#connect-your-directories).</span><span class="sxs-lookup"><span data-stu-id="7f620-125">[Add more directories](active-directory-aadconnect-get-started-custom.md#connect-your-directories).</span></span> <span data-ttu-id="7f620-126">Bir dizin kaldırmak için bkz: [bir bağlayıcıyı silmek](active-directory-aadconnectsync-service-manager-ui-connectors.md#delete).</span><span class="sxs-lookup"><span data-stu-id="7f620-126">For removing a directory, see [Delete a Connector](active-directory-aadconnectsync-service-manager-ui-connectors.md#delete).</span></span>
* <span data-ttu-id="7f620-127">[Değişiklik etki alanı ve OU filtreleme](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering).</span><span class="sxs-lookup"><span data-stu-id="7f620-127">[Change Domain and OU filtering](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering).</span></span>
* <span data-ttu-id="7f620-128">Grup filtresini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="7f620-128">Remove Group filtering.</span></span>
* <span data-ttu-id="7f620-129">[İsteğe bağlı özellikler değiştirmek](active-directory-aadconnect-get-started-custom.md#optional-features).</span><span class="sxs-lookup"><span data-stu-id="7f620-129">[Change optional features](active-directory-aadconnect-get-started-custom.md#optional-features).</span></span>

<span data-ttu-id="7f620-130">Merhaba diğer seçenekler hello ilk yüklemesinden değiştirilemez ve kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="7f620-130">hello other options from hello initial installation cannot be changed and are not available.</span></span> <span data-ttu-id="7f620-131">Bu seçenekler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="7f620-131">These options are:</span></span>

* <span data-ttu-id="7f620-132">Merhaba özniteliği toouse userPrincipalName ve sourceAnchor için değiştirin.</span><span class="sxs-lookup"><span data-stu-id="7f620-132">Change hello attribute toouse for userPrincipalName and sourceAnchor.</span></span>
* <span data-ttu-id="7f620-133">Farklı ormandaki nesneleri için yöntem birleştirme hello değiştirin.</span><span class="sxs-lookup"><span data-stu-id="7f620-133">Change hello joining method for objects from different forest.</span></span>
* <span data-ttu-id="7f620-134">Grup tabanlı filtreleme etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="7f620-134">Enable group-based filtering.</span></span>

## <a name="refresh-directory-schema"></a><span data-ttu-id="7f620-135">Dizin şemasını Yenile</span><span class="sxs-lookup"><span data-stu-id="7f620-135">Refresh directory schema</span></span>
<span data-ttu-id="7f620-136">Merhaba şema şirket içi birini değiştirdiyseniz, bu seçenek kullanılır AD DS orman.</span><span class="sxs-lookup"><span data-stu-id="7f620-136">This option is used if you have changed hello schema in one of your on-premises AD DS forests.</span></span> <span data-ttu-id="7f620-137">Örneğin, Exchange yüklenmemiş olabilir veya tooa Windows Server 2012 şema aygıt nesneler ile yükseltme.</span><span class="sxs-lookup"><span data-stu-id="7f620-137">For example, you might have installed Exchange or upgraded tooa Windows Server 2012 schema with device objects.</span></span> <span data-ttu-id="7f620-138">Bu durumda, tooinstruct Azure AD Connect tooread hello şema AD DS'den yeniden gerekir ve önbelleğini güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="7f620-138">In this case, you need tooinstruct Azure AD Connect tooread hello schema again from AD DS and update its cache.</span></span> <span data-ttu-id="7f620-139">Bu eylem ayrıca hello eşitleme kuralları yeniden oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7f620-139">This action also regenerates hello Sync Rules.</span></span> <span data-ttu-id="7f620-140">Örnek olarak hello Exchange şema eklerseniz, Exchange için hello eşitleme kuralları toohello yapılandırma eklenir.</span><span class="sxs-lookup"><span data-stu-id="7f620-140">If you add hello Exchange schema, as an example, hello Sync Rules for Exchange are added toohello configuration.</span></span>

<span data-ttu-id="7f620-141">Bu seçeneği belirlediğinizde, yapılandırmanızda tüm hello dizinleri listelenir.</span><span class="sxs-lookup"><span data-stu-id="7f620-141">When you select this option, all hello directories in your configuration are listed.</span></span> <span data-ttu-id="7f620-142">Hello varsayılan ayar tutun ve tüm ormanlarda yenileyin veya bunlardan bazıları seçimini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="7f620-142">You can keep hello default setting and refresh all forests or unselect some of them.</span></span>

![Merhaba ortamında tüm dizinlerin listesini sayfası](./media/active-directory-aadconnectsync-installation-wizard/refreshschema.png)

## <a name="configure-staging-mode"></a><span data-ttu-id="7f620-144">Hazırlama modunu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="7f620-144">Configure staging mode</span></span>
<span data-ttu-id="7f620-145">Bu seçenek tooenable sağlar ve hello sunucuda hazırlama modunu devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="7f620-145">This option allows you tooenable and disable staging mode on hello server.</span></span> <span data-ttu-id="7f620-146">Hazırlama modu ve nasıl kullanıldığı hakkında daha fazla bilgi bulunabilir [Operations](active-directory-aadconnectsync-operations.md#staging-mode).</span><span class="sxs-lookup"><span data-stu-id="7f620-146">More information about staging mode and how it is used can be found in [Operations](active-directory-aadconnectsync-operations.md#staging-mode).</span></span>

<span data-ttu-id="7f620-147">Merhaba seçeneği hazırlama şu anda etkin veya devre dışı olmadığını gösterir:</span><span class="sxs-lookup"><span data-stu-id="7f620-147">hello option shows if staging is currently enabled or disabled:</span></span>  
![Ayrıca hazırlama modunu hello geçerli durumunu gösteren seçeneği](./media/active-directory-aadconnectsync-installation-wizard/stagingmodecurrentstate.png)

<span data-ttu-id="7f620-149">toochange Merhaba durumu, bu seçeneği ve seçimi kaldır veya seçin hello onay kutusunu seçin.</span><span class="sxs-lookup"><span data-stu-id="7f620-149">toochange hello state, select this option and select or unselect hello checkbox.</span></span>  
![Ayrıca hazırlama modunu hello geçerli durumunu gösteren seçeneği](./media/active-directory-aadconnectsync-installation-wizard/stagingmodeenable.png)

## <a name="change-user-sign-in"></a><span data-ttu-id="7f620-151">Kullanıcı oturum açma değiştirme</span><span class="sxs-lookup"><span data-stu-id="7f620-151">Change user sign-in</span></span>
<span data-ttu-id="7f620-152">Bu seçenek parola eşitleme toofederation veya hello diğer yönden toochange sağlar.</span><span class="sxs-lookup"><span data-stu-id="7f620-152">This option allows you toochange from password sync toofederation or hello other way around.</span></span> <span data-ttu-id="7f620-153">Çok değiştiremezsiniz**yapılandırmayın**.</span><span class="sxs-lookup"><span data-stu-id="7f620-153">You cannot change too**do not configure**.</span></span>

<span data-ttu-id="7f620-154">Bu seçenek hakkında daha fazla bilgi için bkz: [kullanıcı oturum açma](active-directory-aadconnect-user-signin.md#changing-the-user-sign-in-method).</span><span class="sxs-lookup"><span data-stu-id="7f620-154">For more information on this option, see [user sign-in](active-directory-aadconnect-user-signin.md#changing-the-user-sign-in-method).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7f620-155">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7f620-155">Next steps</span></span>
* <span data-ttu-id="7f620-156">Azure AD Connect eşitleme tarafından kullanılan hello yapılandırma modeli hakkında daha fazla bilgi [anlama bildirim temelli hazırlama](active-directory-aadconnectsync-understanding-declarative-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="7f620-156">Learn more about hello configuration model used by Azure AD Connect sync in [Understanding Declarative Provisioning](active-directory-aadconnectsync-understanding-declarative-provisioning.md).</span></span>

<span data-ttu-id="7f620-157">**Genel bakış konuları**</span><span class="sxs-lookup"><span data-stu-id="7f620-157">**Overview topics**</span></span>

* [<span data-ttu-id="7f620-158">Azure AD Connect eşitleme: anlamak ve eşitleme özelleştirme</span><span class="sxs-lookup"><span data-stu-id="7f620-158">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="7f620-159">Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="7f620-159">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
