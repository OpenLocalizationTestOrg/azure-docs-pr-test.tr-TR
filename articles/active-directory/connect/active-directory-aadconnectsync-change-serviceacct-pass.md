---
title: "Azure AD Connect eşitleme: hello Azure AD Connect eşitleme hizmeti hesabını değiştirme | Microsoft Docs"
description: "Bu konuda belge hello şifreleme anahtarını ve nasıl tooabandon hello parola sonra açıklar değiştirildi."
services: active-directory
keywords: "Azure AD eşitleme hizmeti hesabını, parola"
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: 76b19162-8b16-4960-9e22-bd64e6675ecc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 11948ac4662f722e4f684ef6c9b9ccdc6387e60f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="changing-hello-azure-ad-connect-sync-service-account-password"></a><span data-ttu-id="8fac8-104">Hello Azure AD Connect eşitleme hizmeti hesabı parolasını değiştirme</span><span class="sxs-lookup"><span data-stu-id="8fac8-104">Changing hello Azure AD Connect sync service account password</span></span>
<span data-ttu-id="8fac8-105">Hello Azure AD Connect eşitleme hizmeti hesabı parolasını değiştirirseniz, hello şifreleme anahtarı terk ve hello Azure AD Connect eşitleme hizmeti hesabının parolasını yeniden kadar hello eşitleme hizmeti mümkün başlangıç doğru olmaz.</span><span class="sxs-lookup"><span data-stu-id="8fac8-105">If you change hello  Azure AD Connect sync service account password, hello Synchronization Service will not be able start correctly until you have abandoned hello encryption key and reinitialized hello Azure AD Connect sync service account password.</span></span> 

<span data-ttu-id="8fac8-106">Azure AD Connect Eşitleme Hizmetleri hello bir parçası olarak bir şifreleme anahtarı toostore hello parolaları hello AD DS ve Azure AD hizmet hesaplarını kullanır.</span><span class="sxs-lookup"><span data-stu-id="8fac8-106">Azure AD Connect, as part of hello Synchronization Services uses an encryption key toostore hello passwords of hello AD DS and Azure AD service accounts.</span></span>  <span data-ttu-id="8fac8-107">Bu hesapları hello veritabanında depolanan önce şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="8fac8-107">These accounts are encrypted before they are stored in hello database.</span></span> 

<span data-ttu-id="8fac8-108">Merhaba kullanılan şifreleme anahtarı güvenliğinin ile [Windows Data Protection (DPAPI)](https://msdn.microsoft.com/library/ms995355.aspx).</span><span class="sxs-lookup"><span data-stu-id="8fac8-108">hello encryption key used is secured using [Windows Data Protection (DPAPI)](https://msdn.microsoft.com/library/ms995355.aspx).</span></span> <span data-ttu-id="8fac8-109">DPAPI korur hello kullanarak hello şifreleme anahtarı **hello Azure AD Connect eşitleme hizmeti hesabı parolasını**.</span><span class="sxs-lookup"><span data-stu-id="8fac8-109">DPAPI protects hello encryption key using hello **password of hello Azure AD Connect sync service account**.</span></span> 

<span data-ttu-id="8fac8-110">Toochange hello hizmet hesabı parolası gerekirse hello yordamlarda kullanabilirsiniz [Abandoning hello Azure AD Connect eşitleme şifreleme anahtarı](#abandoning-the-azure-ad-connect-sync-encryption-key) tooaccomplish bu.</span><span class="sxs-lookup"><span data-stu-id="8fac8-110">If you need toochange hello service account password you can use hello procedures in [Abandoning hello Azure AD Connect Sync encryption key](#abandoning-the-azure-ad-connect-sync-encryption-key) tooaccomplish this.</span></span>  <span data-ttu-id="8fac8-111">Bu yordamları da tooabandon hello şifreleme anahtarı herhangi bir nedenle ihtiyacınız varsa kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8fac8-111">These procedures should also be used if you need tooabandon hello encryption key for any reason.</span></span>

##<a name="issues-that-arise-from-changing-hello-password"></a><span data-ttu-id="8fac8-112">Merhaba parolasını değiştirme ortaya çıkan sorunları</span><span class="sxs-lookup"><span data-stu-id="8fac8-112">Issues that arise from changing hello password</span></span>
<span data-ttu-id="8fac8-113">Merhaba hizmet hesabı parolasını değiştirdiğinizde bitti toobe gereken iki şey vardır.</span><span class="sxs-lookup"><span data-stu-id="8fac8-113">There are two things that need toobe done when you change hello service account password.</span></span>

<span data-ttu-id="8fac8-114">İlk olarak, Windows Hizmet Denetimi Yöneticisi hello altında toochange hello parola gerekir.</span><span class="sxs-lookup"><span data-stu-id="8fac8-114">First, you need toochange hello password under hello Windows Service Control Manager.</span></span>  <span data-ttu-id="8fac8-115">Bu sorun çözülene kadar aşağıdaki hatalar görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="8fac8-115">Until this issue is resolved you will see following errors:</span></span>


- <span data-ttu-id="8fac8-116">Merhaba hatasını alıyorsunuz toostart hello eşitleme hizmeti Windows Hizmet Denetimi Yöneticisi'nde çalışırsanız, "**Windows hello Microsoft Azure AD eşitleme hizmeti yerel bilgisayarda başlatılamadı**".</span><span class="sxs-lookup"><span data-stu-id="8fac8-116">If you try toostart hello Synchronization Service in Windows Service Control Manager, you receive hello error "**Windows could not start hello Microsoft Azure AD Sync service on Local Computer**".</span></span> <span data-ttu-id="8fac8-117">**Hata 1069: tooa oturum açma hatası hello hizmeti başlatılmadı.** "</span><span class="sxs-lookup"><span data-stu-id="8fac8-117">**Error 1069: hello service did not start due tooa logon failure.**"</span></span>
- <span data-ttu-id="8fac8-118">Windows Olay Görüntüleyicisi'ni altında bir hata ile Merhaba sistem olay günlüğünü içeren **olay kimliği 7038** ve ileti "**hello ADSync hizmeti tarihi oluşturulamıyor toolog parolayla şu anda yapılandırılmış hello gibi toohello aşağıdaki son hata: Merhaba kullanıcı adı veya parola doğru değil.** "</span><span class="sxs-lookup"><span data-stu-id="8fac8-118">Under Windows Event Viewer, hello system event log contains an error with **Event ID 7038** and message “**hello ADSync service was unable toolog on as with hello currently configured password due toohello following error: hello user name or password is incorrect.**"</span></span>

<span data-ttu-id="8fac8-119">Merhaba parola güncelleştirilirse, ikinci olarak, belirli koşullar altında hello eşitleme hizmeti artık hello şifreleme anahtarı DPAPI aracılığıyla alabilir.</span><span class="sxs-lookup"><span data-stu-id="8fac8-119">Second, under specific conditions, if hello password is updated, hello Synchronization Service can no longer retrieve hello encryption key via DPAPI.</span></span> <span data-ttu-id="8fac8-120">Merhaba şifreleme anahtar olmadan, eşitleme hizmeti hello parolaları gerekli toosynchronize denetleyicisinden şifresi çözülemiyor hello AD ve Azure AD şirket içi.</span><span class="sxs-lookup"><span data-stu-id="8fac8-120">Without hello encryption key, hello Synchronization Service cannot decrypt hello passwords required toosynchronize to/from on-premises AD and Azure AD.</span></span>
<span data-ttu-id="8fac8-121">Hataları gibi görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="8fac8-121">You will see errors such as:</span></span>

- <span data-ttu-id="8fac8-122">Windows Hizmet Denetimi Yöneticisi altında toostart hello eşitleme hizmeti çalışırsanız ve hello şifreleme anahtarını alamıyor hatasıyla başarısız "** Windows hello Microsoft Azure AD eşitleme yerel bilgisayarda başlatılamadı.</span><span class="sxs-lookup"><span data-stu-id="8fac8-122">Under Windows Service Control Manager, if you try toostart hello Synchronization Service and it cannot retrieve hello encryption key, it fails with error “**Windows could not start hello Microsoft Azure AD Sync on Local Computer.</span></span> <span data-ttu-id="8fac8-123">Daha fazla bilgi için hello sistem olay günlüğünü gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="8fac8-123">For more information, review hello System Event log.</span></span> <span data-ttu-id="8fac8-124">Bu Microsoft dışı service ise, hello hizmet satıcısını ve tooservice özel hata kodunu **-21451857952 ***. "</span><span class="sxs-lookup"><span data-stu-id="8fac8-124">If this is a non-Microsoft service, contact hello service vendor, and refer tooservice-specific error code **-21451857952****.”</span></span>
- <span data-ttu-id="8fac8-125">Windows Olay Görüntüleyicisi'ni altında hello uygulama olay günlüğüne bir hata ile içeren **olay kimliği 6028** ve hata iletisi *"**hello sunucusu şifreleme anahtarı erişilemez.* *"*</span><span class="sxs-lookup"><span data-stu-id="8fac8-125">Under Windows Event Viewer, hello application event log contains an error with **Event ID 6028** and error message *“**hello server encryption key cannot be accessed.**”*</span></span>

<span data-ttu-id="8fac8-126">Bu hatalar almazsınız tooensure hello yordamları izleyin [Abandoning hello Azure AD Connect eşitleme şifreleme anahtarı](#abandoning-the-azure-ad-connect-sync-encryption-key) hello parola değiştirme.</span><span class="sxs-lookup"><span data-stu-id="8fac8-126">tooensure that you do not receive these errors, follow hello procedures in [Abandoning hello Azure AD Connect Sync encryption key](#abandoning-the-azure-ad-connect-sync-encryption-key) when changing hello password.</span></span>
 
## <a name="abandoning-hello-azure-ad-connect-sync-encryption-key"></a><span data-ttu-id="8fac8-127">Hello Azure AD Connect eşitleme şifreleme anahtarını bırakıp</span><span class="sxs-lookup"><span data-stu-id="8fac8-127">Abandoning hello Azure AD Connect Sync encryption key</span></span>
>[!IMPORTANT]
><span data-ttu-id="8fac8-128">Merhaba aşağıdaki yordamlar yalnızca tooAzure AD Connect yapı 1.1.443.0 uygulanır veya daha eski.</span><span class="sxs-lookup"><span data-stu-id="8fac8-128">hello following procedures only apply tooAzure AD Connect build 1.1.443.0 or older.</span></span>

<span data-ttu-id="8fac8-129">Aşağıdaki yordamlar tooabandon hello şifreleme anahtarı hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="8fac8-129">Use hello following procedures tooabandon hello encryption key.</span></span>

### <a name="what-toodo-if-you-need-tooabandon-hello-encryption-key"></a><span data-ttu-id="8fac8-130">Tooabandon hello şifreleme anahtarı gerekiyorsa hangi toodo</span><span class="sxs-lookup"><span data-stu-id="8fac8-130">What toodo if you need tooabandon hello encryption key</span></span>

<span data-ttu-id="8fac8-131">Tooabandon hello şifreleme anahtarı gerekiyorsa, aşağıdaki yordamları tooaccomplish hello bunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="8fac8-131">If you need tooabandon hello encryption key, use hello following procedures tooaccomplish this.</span></span>

1. [<span data-ttu-id="8fac8-132">Merhaba varolan şifreleme anahtarını iptal</span><span class="sxs-lookup"><span data-stu-id="8fac8-132">Abandon hello existing encryption key</span></span>](#abandon-the-existing-encryption-key)

2. [<span data-ttu-id="8fac8-133">Merhaba AD DS hesabı Hello parolasını sağlayın</span><span class="sxs-lookup"><span data-stu-id="8fac8-133">Provide hello password of hello AD DS account</span></span>](#provide-the-password-of-the-ad-ds-account)

3. [<span data-ttu-id="8fac8-134">Merhaba hello Azure AD eşitleme hesabının parolasını yeniden Başlat</span><span class="sxs-lookup"><span data-stu-id="8fac8-134">Reinitialize hello password of hello Azure AD sync account</span></span>](#reinitialize-the-password-of-the-azure-ad-sync-account)

4. [<span data-ttu-id="8fac8-135">Merhaba eşitleme hizmetini Başlat</span><span class="sxs-lookup"><span data-stu-id="8fac8-135">Start hello Synchronization Service</span></span>](#start-the-synchronization-service)

#### <a name="abandon-hello-existing-encryption-key"></a><span data-ttu-id="8fac8-136">Merhaba varolan şifreleme anahtarını iptal</span><span class="sxs-lookup"><span data-stu-id="8fac8-136">Abandon hello existing encryption key</span></span>
<span data-ttu-id="8fac8-137">Bu yeni bir şifreleme anahtarı oluşturulabilmesi hello var olan şifreleme anahtarı bırakın:</span><span class="sxs-lookup"><span data-stu-id="8fac8-137">Abandon hello existing encryption key so that new encryption key can be created:</span></span>

1. <span data-ttu-id="8fac8-138">Tooyour içinde Azure AD Connect Server yönetici olarak oturum.</span><span class="sxs-lookup"><span data-stu-id="8fac8-138">Log in tooyour Azure AD Connect Server as administrator.</span></span>

2. <span data-ttu-id="8fac8-139">Yeni bir PowerShell oturumu başlatın.</span><span class="sxs-lookup"><span data-stu-id="8fac8-139">Start a new PowerShell session.</span></span>

3. <span data-ttu-id="8fac8-140">Toofolder gidin:`$env:Program Files\Microsoft Azure AD Sync\bin\`</span><span class="sxs-lookup"><span data-stu-id="8fac8-140">Navigate toofolder: `$env:Program Files\Microsoft Azure AD Sync\bin\`</span></span>

4. <span data-ttu-id="8fac8-141">Merhaba komutu çalıştırın:`./miiskmu.exe /a`</span><span class="sxs-lookup"><span data-stu-id="8fac8-141">Run hello command: `./miiskmu.exe /a`</span></span>

![Azure AD Connect eşitleme şifreleme anahtarı yardımcı programı](media/active-directory-aadconnectsync-encryption-key/key5.png)

#### <a name="provide-hello-password-of-hello-ad-ds-account"></a><span data-ttu-id="8fac8-143">Merhaba AD DS hesabı Hello parolasını sağlayın</span><span class="sxs-lookup"><span data-stu-id="8fac8-143">Provide hello password of hello AD DS account</span></span>
<span data-ttu-id="8fac8-144">Merhaba var olan parolaların Hello veritabanı içinde depolanan artık şifresi çözülebilir gibi hello AD DS hesabının hello parolayla tooprovide hello eşitleme hizmeti gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="8fac8-144">As hello existing passwords stored inside hello database can no longer be decrypted, you need tooprovide hello Synchronization Service with hello password of hello AD DS account.</span></span> <span data-ttu-id="8fac8-145">Merhaba eşitleme hizmeti hello parolaları hello yeni bir şifreleme anahtarı kullanarak şifreler:</span><span class="sxs-lookup"><span data-stu-id="8fac8-145">hello Synchronization Service encrypts hello passwords using hello new encryption key:</span></span>

1. <span data-ttu-id="8fac8-146">Merhaba Eşitleme Hizmeti Yöneticisi'ni (Başlangıç → eşitleme hizmeti) başlatın.</span><span class="sxs-lookup"><span data-stu-id="8fac8-146">Start hello Synchronization Service Manager (START → Synchronization Service).</span></span>
</br><span data-ttu-id="8fac8-147">![Eşitleme Hizmeti Yöneticisi](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span><span class="sxs-lookup"><span data-stu-id="8fac8-147">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span></span>  
2. <span data-ttu-id="8fac8-148">Toohello Git **Bağlayıcılar** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="8fac8-148">Go toohello **Connectors** tab.</span></span>
3. <span data-ttu-id="8fac8-149">Select hello **AD Bağlayıcısı** tooyour karşılık gelen şirket içi AD.</span><span class="sxs-lookup"><span data-stu-id="8fac8-149">Select hello **AD Connector** that corresponds tooyour on-premises AD.</span></span> <span data-ttu-id="8fac8-150">Birden fazla AD bağlayıcısı varsa, bunların her biri için aşağıdaki adımları hello yineleyin.</span><span class="sxs-lookup"><span data-stu-id="8fac8-150">If you have more than one AD connector, repeat hello following steps for each of them.</span></span>
4. <span data-ttu-id="8fac8-151">Altında **Eylemler**seçin **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="8fac8-151">Under **Actions**, select **Properties**.</span></span>
5. <span data-ttu-id="8fac8-152">Merhaba açılan iletişim kutusunda seçin **tooActive Directory ormanına Bağlan**:</span><span class="sxs-lookup"><span data-stu-id="8fac8-152">In hello pop-up dialog, select **Connect tooActive Directory Forest**:</span></span>
6. <span data-ttu-id="8fac8-153">Hello hello AD DS hesap Hello parolasını girin **parola** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="8fac8-153">Enter hello password of hello AD DS account in hello **Password** textbox.</span></span> <span data-ttu-id="8fac8-154">Parolasını bilmiyorsanız, bu adımı uygulamadan önce değer bilinen tooa ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8fac8-154">If you do not know its password, you must set it tooa known value before performing this step.</span></span>
7. <span data-ttu-id="8fac8-155">Tıklatın **Tamam** toosave hello yeni parola ve Kapat hello açılan iletişim.</span><span class="sxs-lookup"><span data-stu-id="8fac8-155">Click **OK** toosave hello new password and close hello pop-up dialog.</span></span>
<span data-ttu-id="8fac8-156">![Azure AD Connect eşitleme şifreleme anahtarı yardımcı programı](media/active-directory-aadconnectsync-encryption-key/key6.png)</span><span class="sxs-lookup"><span data-stu-id="8fac8-156">![Azure AD Connect Sync Encryption Key Utility](media/active-directory-aadconnectsync-encryption-key/key6.png)</span></span>

#### <a name="reinitialize-hello-password-of-hello-azure-ad-sync-account"></a><span data-ttu-id="8fac8-157">Merhaba hello Azure AD eşitleme hesabının parolasını yeniden Başlat</span><span class="sxs-lookup"><span data-stu-id="8fac8-157">Reinitialize hello password of hello Azure AD sync account</span></span>
<span data-ttu-id="8fac8-158">Doğrudan hello parolasını hello Azure AD hizmet hesabı toohello eşitleme hizmeti sağlayamıyor.</span><span class="sxs-lookup"><span data-stu-id="8fac8-158">You cannot directly provide hello password of hello Azure AD service account toohello Synchronization Service.</span></span> <span data-ttu-id="8fac8-159">Bunun yerine, toouse hello cmdlet gerekir **Ekle ADSyncAADServiceAccount** tooreinitialize hello Azure AD hizmet hesabı.</span><span class="sxs-lookup"><span data-stu-id="8fac8-159">Instead, you need toouse hello cmdlet **Add-ADSyncAADServiceAccount** tooreinitialize hello Azure AD service account.</span></span> <span data-ttu-id="8fac8-160">Merhaba cmdlet hello hesabı parolasını sıfırlar ve kullanılabilir toohello eşitleme hizmeti yapar:</span><span class="sxs-lookup"><span data-stu-id="8fac8-160">hello cmdlet resets hello account password and makes it available toohello Synchronization Service:</span></span>

1. <span data-ttu-id="8fac8-161">Hello Azure AD Connect sunucuda yeni bir PowerShell oturumu başlatın.</span><span class="sxs-lookup"><span data-stu-id="8fac8-161">Start a new PowerShell session on hello Azure AD Connect server.</span></span>
2. <span data-ttu-id="8fac8-162">Cmdlet'i çalıştırmak `Add-ADSyncAADServiceAccount`.</span><span class="sxs-lookup"><span data-stu-id="8fac8-162">Run cmdlet `Add-ADSyncAADServiceAccount`.</span></span>
3. <span data-ttu-id="8fac8-163">Merhaba açılan iletişim kutusunda, Azure AD kiracınız için hello Azure AD genel yönetici kimlik bilgilerini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="8fac8-163">In hello pop-up dialog, provide hello Azure AD Global admin credentials for your Azure AD tenant.</span></span>
<span data-ttu-id="8fac8-164">![Azure AD Connect eşitleme şifreleme anahtarı yardımcı programı](media/active-directory-aadconnectsync-encryption-key/key7.png)</span><span class="sxs-lookup"><span data-stu-id="8fac8-164">![Azure AD Connect Sync Encryption Key Utility](media/active-directory-aadconnectsync-encryption-key/key7.png)</span></span>
4. <span data-ttu-id="8fac8-165">Başarılı olursa, hello PowerShell komut istemi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="8fac8-165">If it is successful, you will see hello PowerShell command prompt.</span></span>

#### <a name="start-hello-synchronization-service"></a><span data-ttu-id="8fac8-166">Merhaba eşitleme hizmetini Başlat</span><span class="sxs-lookup"><span data-stu-id="8fac8-166">Start hello Synchronization Service</span></span>
<span data-ttu-id="8fac8-167">Merhaba eşitleme hizmeti erişim toohello şifreleme anahtarına sahiptir ve tüm parolaları hello göre gereksinim duyduğu, hello Windows Hizmet Denetimi Yöneticisi hello hizmetini yeniden başlatabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8fac8-167">Now that hello Synchronization Service has access toohello encryption key and all hello passwords it needs, you can restart hello service in hello Windows Service Control Manager:</span></span>


1. <span data-ttu-id="8fac8-168">TooWindows Hizmet Denetim Yöneticisi (Başlangıç → Hizmetleri) gidin.</span><span class="sxs-lookup"><span data-stu-id="8fac8-168">Go tooWindows Service Control Manager (START → Services).</span></span>
2. <span data-ttu-id="8fac8-169">Seçin **Microsoft Azure AD eşitleme** ve yeniden Başlat'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="8fac8-169">Select **Microsoft Azure AD Sync** and click Restart.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8fac8-170">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8fac8-170">Next steps</span></span>
<span data-ttu-id="8fac8-171">**Genel bakış konuları**</span><span class="sxs-lookup"><span data-stu-id="8fac8-171">**Overview topics**</span></span>

* [<span data-ttu-id="8fac8-172">Azure AD Connect eşitleme: anlamak ve eşitleme özelleştirme</span><span class="sxs-lookup"><span data-stu-id="8fac8-172">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)

* [<span data-ttu-id="8fac8-173">Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="8fac8-173">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
