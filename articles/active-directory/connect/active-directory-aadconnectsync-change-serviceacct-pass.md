---
title: "Azure AD Connect eşitleme: Azure AD Connect eşitleme hizmeti hesabını değiştirme | Microsoft Docs"
description: "Bu konuda belge şifreleme anahtarını ve parolalar değiştirildikten sonra abandon açıklar."
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
ms.openlocfilehash: bf6234d0810f870909957ee1c1e33c225a4922b9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="changing-the-azure-ad-connect-sync-service-account-password"></a><span data-ttu-id="1677e-104">Azure AD Connect eşitleme hizmeti hesabı parolasını değiştirme</span><span class="sxs-lookup"><span data-stu-id="1677e-104">Changing the Azure AD Connect sync service account password</span></span>
<span data-ttu-id="1677e-105">Azure AD Connect eşitleme hizmeti hesabı parolasını değiştirirseniz, şifreleme anahtarını terk ve Azure AD Connect eşitleme hizmeti hesabının parolasını yeniden kadar eşitleme hizmeti mümkün başlangıç doğru olmaz.</span><span class="sxs-lookup"><span data-stu-id="1677e-105">If you change the  Azure AD Connect sync service account password, the Synchronization Service will not be able start correctly until you have abandoned the encryption key and reinitialized the Azure AD Connect sync service account password.</span></span> 

<span data-ttu-id="1677e-106">Azure AD Connect Eşitleme hizmetlerini bir parçası olarak AD DS ve Azure AD hizmet hesaplarının parolaları depolamak için bir şifreleme anahtarı kullanır.</span><span class="sxs-lookup"><span data-stu-id="1677e-106">Azure AD Connect, as part of the Synchronization Services uses an encryption key to store the passwords of the AD DS and Azure AD service accounts.</span></span>  <span data-ttu-id="1677e-107">Bu hesaplar veritabanında depolanan önce şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="1677e-107">These accounts are encrypted before they are stored in the database.</span></span> 

<span data-ttu-id="1677e-108">Kullanılan şifreleme anahtarını kullanarak güvenliği [Windows Data Protection (DPAPI)](https://msdn.microsoft.com/library/ms995355.aspx).</span><span class="sxs-lookup"><span data-stu-id="1677e-108">The encryption key used is secured using [Windows Data Protection (DPAPI)](https://msdn.microsoft.com/library/ms995355.aspx).</span></span> <span data-ttu-id="1677e-109">DPAPI koruyan şifreleme anahtarı kullanarak **Azure AD Connect eşitleme hizmeti hesabının parolasını**.</span><span class="sxs-lookup"><span data-stu-id="1677e-109">DPAPI protects the encryption key using the **password of the Azure AD Connect sync service account**.</span></span> 

<span data-ttu-id="1677e-110">Hizmet hesabı parolasını değiştirmeniz gerekiyorsa yordamları kullanabilirsiniz [Azure AD Connect eşitleme şifreleme anahtarını bırakıp](#abandoning-the-azure-ad-connect-sync-encryption-key) bunu gerçekleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="1677e-110">If you need to change the service account password you can use the procedures in [Abandoning the Azure AD Connect Sync encryption key](#abandoning-the-azure-ad-connect-sync-encryption-key) to accomplish this.</span></span>  <span data-ttu-id="1677e-111">Şifreleme anahtarı herhangi bir nedenle abandon gerekiyorsa, bu yordamları da kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1677e-111">These procedures should also be used if you need to abandon the encryption key for any reason.</span></span>

##<a name="issues-that-arise-from-changing-the-password"></a><span data-ttu-id="1677e-112">Parola değiştirme ortaya çıkan sorunları</span><span class="sxs-lookup"><span data-stu-id="1677e-112">Issues that arise from changing the password</span></span>
<span data-ttu-id="1677e-113">Hizmet hesabı parolasını değiştirdiğinizde yapılmasına gerek iki nokta vardır.</span><span class="sxs-lookup"><span data-stu-id="1677e-113">There are two things that need to be done when you change the service account password.</span></span>

<span data-ttu-id="1677e-114">İlk olarak, altında Windows hizmet denetimi yöneticisi parolasını değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1677e-114">First, you need to change the password under the Windows Service Control Manager.</span></span>  <span data-ttu-id="1677e-115">Bu sorun çözülene kadar aşağıdaki hatalar görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="1677e-115">Until this issue is resolved you will see following errors:</span></span>


- <span data-ttu-id="1677e-116">Windows Hizmet Denetimi Yöneticisi'nde eşitleme hizmetini başlatmayı denerseniz, şu hatayı alıyorsunuz "**Windows yerel bilgisayarda Microsoft Azure AD eşitleme hizmeti başlatılamadı**".</span><span class="sxs-lookup"><span data-stu-id="1677e-116">If you try to start the Synchronization Service in Windows Service Control Manager, you receive the error "**Windows could not start the Microsoft Azure AD Sync service on Local Computer**".</span></span> <span data-ttu-id="1677e-117">**Hata 1069: Bir oturum açma hatası nedeniyle hizmeti başlatılmadı.** "</span><span class="sxs-lookup"><span data-stu-id="1677e-117">**Error 1069: The service did not start due to a logon failure.**"</span></span>
- <span data-ttu-id="1677e-118">Windows Olay Görüntüleyicisi'ni altında sistem olay günlüğüne bir hata ile içeren **olay kimliği 7038** ve ileti "**ADSync hizmeti şu hata nedeniyle şu anda yapılandırılmış parola olarak oturum açamadı: kullanıcı adı veya parola doğru değil.** "</span><span class="sxs-lookup"><span data-stu-id="1677e-118">Under Windows Event Viewer, the system event log contains an error with **Event ID 7038** and message “**The ADSync service was unable to log on as with the currently configured password due to the following error: The user name or password is incorrect.**"</span></span>

<span data-ttu-id="1677e-119">Parola güncelleştirilirse, ikinci olarak, belirli koşullar altında eşitleme hizmeti artık DPAPI aracılığıyla şifreleme anahtarını alabilir.</span><span class="sxs-lookup"><span data-stu-id="1677e-119">Second, under specific conditions, if the password is updated, the Synchronization Service can no longer retrieve the encryption key via DPAPI.</span></span> <span data-ttu-id="1677e-120">Şifreleme anahtarı olmadan, eşitleme hizmeti AD ve Azure AD şirket içi denetleyicisinden eşitlemek için gerekli olan parolaları şifresi çözülemiyor.</span><span class="sxs-lookup"><span data-stu-id="1677e-120">Without the encryption key, the Synchronization Service cannot decrypt the passwords required to synchronize to/from on-premises AD and Azure AD.</span></span>
<span data-ttu-id="1677e-121">Hataları gibi görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="1677e-121">You will see errors such as:</span></span>

- <span data-ttu-id="1677e-122">Windows Hizmet Denetimi Yöneticisi altında eşitleme hizmeti başlatmayı deneyin ve şifreleme anahtarını alamıyor hatasıyla başarısız "** Windows yerel bilgisayarda Microsoft Azure AD eşitleme başlatılamadı.</span><span class="sxs-lookup"><span data-stu-id="1677e-122">Under Windows Service Control Manager, if you try to start the Synchronization Service and it cannot retrieve the encryption key, it fails with error “**Windows could not start the Microsoft Azure AD Sync on Local Computer.</span></span> <span data-ttu-id="1677e-123">Daha fazla bilgi için sistem olay günlüğünü gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="1677e-123">For more information, review the System Event log.</span></span> <span data-ttu-id="1677e-124">Microsoft dışı hizmeti varsa hizmet satıcısını ve hizmete özgü hata koduna başvurun **-21451857952 ***. "</span><span class="sxs-lookup"><span data-stu-id="1677e-124">If this is a non-Microsoft service, contact the service vendor, and refer to service-specific error code **-21451857952****.”</span></span>
- <span data-ttu-id="1677e-125">Windows Olay Görüntüleyicisi'ni altında uygulama olay günlüğüne bir hata ile içeren **olay kimliği 6028** ve hata iletisi *"**sunucu şifreleme anahtarına erişilemiyor.* *"*</span><span class="sxs-lookup"><span data-stu-id="1677e-125">Under Windows Event Viewer, the application event log contains an error with **Event ID 6028** and error message *“**The server encryption key cannot be accessed.**”*</span></span>

<span data-ttu-id="1677e-126">Bu hatalar almazsınız emin olmak için konusundaki yordamları izleyin [Azure AD Connect eşitleme şifreleme anahtarını bırakıp](#abandoning-the-azure-ad-connect-sync-encryption-key) parola değiştirme.</span><span class="sxs-lookup"><span data-stu-id="1677e-126">To ensure that you do not receive these errors, follow the procedures in [Abandoning the Azure AD Connect Sync encryption key](#abandoning-the-azure-ad-connect-sync-encryption-key) when changing the password.</span></span>
 
## <a name="abandoning-the-azure-ad-connect-sync-encryption-key"></a><span data-ttu-id="1677e-127">Azure AD Connect eşitleme şifreleme anahtarını bırakıp</span><span class="sxs-lookup"><span data-stu-id="1677e-127">Abandoning the Azure AD Connect Sync encryption key</span></span>
>[!IMPORTANT]
><span data-ttu-id="1677e-128">Aşağıdaki yordamlar yalnızca Azure AD Connect yapı 1.1.443.0 uygulanır veya daha eski.</span><span class="sxs-lookup"><span data-stu-id="1677e-128">The following procedures only apply to Azure AD Connect build 1.1.443.0 or older.</span></span>

<span data-ttu-id="1677e-129">Şifreleme anahtarını iptal etmek için aşağıdaki yordamları kullanın.</span><span class="sxs-lookup"><span data-stu-id="1677e-129">Use the following procedures to abandon the encryption key.</span></span>

### <a name="what-to-do-if-you-need-to-abandon-the-encryption-key"></a><span data-ttu-id="1677e-130">Şifreleme anahtarını iptal ihtiyacınız varsa yapmanız gerekenler</span><span class="sxs-lookup"><span data-stu-id="1677e-130">What to do if you need to abandon the encryption key</span></span>

<span data-ttu-id="1677e-131">Şifreleme anahtarını iptal ihtiyacınız varsa, bunu gerçekleştirmek için aşağıdaki yordamları kullanın.</span><span class="sxs-lookup"><span data-stu-id="1677e-131">If you need to abandon the encryption key, use the following procedures to accomplish this.</span></span>

1. [<span data-ttu-id="1677e-132">Var olan şifreleme anahtarı iptal</span><span class="sxs-lookup"><span data-stu-id="1677e-132">Abandon the existing encryption key</span></span>](#abandon-the-existing-encryption-key)

2. [<span data-ttu-id="1677e-133">AD DS hesabı için parola sağlayın</span><span class="sxs-lookup"><span data-stu-id="1677e-133">Provide the password of the AD DS account</span></span>](#provide-the-password-of-the-ad-ds-account)

3. [<span data-ttu-id="1677e-134">Azure AD eşitleme hesabının parolasını yeniden Başlat</span><span class="sxs-lookup"><span data-stu-id="1677e-134">Reinitialize the password of the Azure AD sync account</span></span>](#reinitialize-the-password-of-the-azure-ad-sync-account)

4. [<span data-ttu-id="1677e-135">Eşitleme hizmetini Başlat</span><span class="sxs-lookup"><span data-stu-id="1677e-135">Start the Synchronization Service</span></span>](#start-the-synchronization-service)

#### <a name="abandon-the-existing-encryption-key"></a><span data-ttu-id="1677e-136">Var olan şifreleme anahtarı iptal</span><span class="sxs-lookup"><span data-stu-id="1677e-136">Abandon the existing encryption key</span></span>
<span data-ttu-id="1677e-137">Bu yeni bir şifreleme anahtarı oluşturulabilmesi varolan şifreleme anahtarını bırakın:</span><span class="sxs-lookup"><span data-stu-id="1677e-137">Abandon the existing encryption key so that new encryption key can be created:</span></span>

1. <span data-ttu-id="1677e-138">Azure AD Connect sunucunuza yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="1677e-138">Log in to your Azure AD Connect Server as administrator.</span></span>

2. <span data-ttu-id="1677e-139">Yeni bir PowerShell oturumu başlatın.</span><span class="sxs-lookup"><span data-stu-id="1677e-139">Start a new PowerShell session.</span></span>

3. <span data-ttu-id="1677e-140">Klasöre gidin:`$env:Program Files\Microsoft Azure AD Sync\bin\`</span><span class="sxs-lookup"><span data-stu-id="1677e-140">Navigate to folder: `$env:Program Files\Microsoft Azure AD Sync\bin\`</span></span>

4. <span data-ttu-id="1677e-141">Komutu çalıştırın:`./miiskmu.exe /a`</span><span class="sxs-lookup"><span data-stu-id="1677e-141">Run the command: `./miiskmu.exe /a`</span></span>

![Azure AD Connect eşitleme şifreleme anahtarı yardımcı programı](media/active-directory-aadconnectsync-encryption-key/key5.png)

#### <a name="provide-the-password-of-the-ad-ds-account"></a><span data-ttu-id="1677e-143">AD DS hesabı için parola sağlayın</span><span class="sxs-lookup"><span data-stu-id="1677e-143">Provide the password of the AD DS account</span></span>
<span data-ttu-id="1677e-144">Veritabanı içinde depolanan var olan parolaların artık şifresi çözülebilir gibi AD DS hesap parolası ile eşitleme hizmeti sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1677e-144">As the existing passwords stored inside the database can no longer be decrypted, you need to provide the Synchronization Service with the password of the AD DS account.</span></span> <span data-ttu-id="1677e-145">Eşitleme hizmetinin yeni bir şifreleme anahtarı kullanarak parolalarını şifreler:</span><span class="sxs-lookup"><span data-stu-id="1677e-145">The Synchronization Service encrypts the passwords using the new encryption key:</span></span>

1. <span data-ttu-id="1677e-146">Eşitleme Hizmeti Yöneticisi'ni (Başlangıç → eşitleme hizmeti) başlatın.</span><span class="sxs-lookup"><span data-stu-id="1677e-146">Start the Synchronization Service Manager (START → Synchronization Service).</span></span>
</br><span data-ttu-id="1677e-147">![Eşitleme Hizmeti Yöneticisi](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span><span class="sxs-lookup"><span data-stu-id="1677e-147">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span></span>  
2. <span data-ttu-id="1677e-148">Git **Bağlayıcılar** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="1677e-148">Go to the **Connectors** tab.</span></span>
3. <span data-ttu-id="1677e-149">Seçin **AD Bağlayıcısı** şirket içi için karşılık gelen AD.</span><span class="sxs-lookup"><span data-stu-id="1677e-149">Select the **AD Connector** that corresponds to your on-premises AD.</span></span> <span data-ttu-id="1677e-150">Birden fazla AD bağlayıcısı varsa, bunların her biri için aşağıdaki adımları yineleyin.</span><span class="sxs-lookup"><span data-stu-id="1677e-150">If you have more than one AD connector, repeat the following steps for each of them.</span></span>
4. <span data-ttu-id="1677e-151">Altında **Eylemler**seçin **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="1677e-151">Under **Actions**, select **Properties**.</span></span>
5. <span data-ttu-id="1677e-152">Açılan iletişim kutusunda seçin **Active Directory ormanına Bağlan**:</span><span class="sxs-lookup"><span data-stu-id="1677e-152">In the pop-up dialog, select **Connect to Active Directory Forest**:</span></span>
6. <span data-ttu-id="1677e-153">AD DS hesap parolasını girin **parola** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="1677e-153">Enter the password of the AD DS account in the **Password** textbox.</span></span> <span data-ttu-id="1677e-154">Parolasını bilmiyorsanız, bu adımı uygulamadan önce bilinen bir değere ayarlamalısınız.</span><span class="sxs-lookup"><span data-stu-id="1677e-154">If you do not know its password, you must set it to a known value before performing this step.</span></span>
7. <span data-ttu-id="1677e-155">Tıklatın **Tamam** yeni parolayı Kaydet ve açılır iletişim kutusunu kapatın.</span><span class="sxs-lookup"><span data-stu-id="1677e-155">Click **OK** to save the new password and close the pop-up dialog.</span></span>
<span data-ttu-id="1677e-156">![Azure AD Connect eşitleme şifreleme anahtarı yardımcı programı](media/active-directory-aadconnectsync-encryption-key/key6.png)</span><span class="sxs-lookup"><span data-stu-id="1677e-156">![Azure AD Connect Sync Encryption Key Utility](media/active-directory-aadconnectsync-encryption-key/key6.png)</span></span>

#### <a name="reinitialize-the-password-of-the-azure-ad-sync-account"></a><span data-ttu-id="1677e-157">Azure AD eşitleme hesabının parolasını yeniden Başlat</span><span class="sxs-lookup"><span data-stu-id="1677e-157">Reinitialize the password of the Azure AD sync account</span></span>
<span data-ttu-id="1677e-158">Azure AD hizmet hesabı için parola eşitleme hizmetine doğrudan sağlayamaz.</span><span class="sxs-lookup"><span data-stu-id="1677e-158">You cannot directly provide the password of the Azure AD service account to the Synchronization Service.</span></span> <span data-ttu-id="1677e-159">Bunun yerine, cmdlet kullanmanıza gerek **Ekle ADSyncAADServiceAccount** Azure AD hizmet hesabını yeniden başlatmak için.</span><span class="sxs-lookup"><span data-stu-id="1677e-159">Instead, you need to use the cmdlet **Add-ADSyncAADServiceAccount** to reinitialize the Azure AD service account.</span></span> <span data-ttu-id="1677e-160">Cmdlet, hesap parolasını sıfırlar ve eşitleme hizmeti için kullanılabilir hale getirir:</span><span class="sxs-lookup"><span data-stu-id="1677e-160">The cmdlet resets the account password and makes it available to the Synchronization Service:</span></span>

1. <span data-ttu-id="1677e-161">Azure AD Connect sunucuda yeni bir PowerShell oturumu başlatın.</span><span class="sxs-lookup"><span data-stu-id="1677e-161">Start a new PowerShell session on the Azure AD Connect server.</span></span>
2. <span data-ttu-id="1677e-162">Cmdlet'i çalıştırmak `Add-ADSyncAADServiceAccount`.</span><span class="sxs-lookup"><span data-stu-id="1677e-162">Run cmdlet `Add-ADSyncAADServiceAccount`.</span></span>
3. <span data-ttu-id="1677e-163">Açılan iletişim kutusunda, Azure AD kiracınız için Azure AD genel yönetici kimlik bilgilerini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="1677e-163">In the pop-up dialog, provide the Azure AD Global admin credentials for your Azure AD tenant.</span></span>
<span data-ttu-id="1677e-164">![Azure AD Connect eşitleme şifreleme anahtarı yardımcı programı](media/active-directory-aadconnectsync-encryption-key/key7.png)</span><span class="sxs-lookup"><span data-stu-id="1677e-164">![Azure AD Connect Sync Encryption Key Utility](media/active-directory-aadconnectsync-encryption-key/key7.png)</span></span>
4. <span data-ttu-id="1677e-165">Başarılı olursa, PowerShell komut istemi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="1677e-165">If it is successful, you will see the PowerShell command prompt.</span></span>

#### <a name="start-the-synchronization-service"></a><span data-ttu-id="1677e-166">Eşitleme hizmetini Başlat</span><span class="sxs-lookup"><span data-stu-id="1677e-166">Start the Synchronization Service</span></span>
<span data-ttu-id="1677e-167">Eşitleme hizmeti için şifreleme anahtarı ve gerekli tüm parolaları erişimi, Windows Hizmet Denetimi Yöneticisi'ndeki hizmetini yeniden başlatabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1677e-167">Now that the Synchronization Service has access to the encryption key and all the passwords it needs, you can restart the service in the Windows Service Control Manager:</span></span>


1. <span data-ttu-id="1677e-168">Windows Hizmet Denetimi Yöneticisi (Başlangıç → Hizmetleri) gidin.</span><span class="sxs-lookup"><span data-stu-id="1677e-168">Go to Windows Service Control Manager (START → Services).</span></span>
2. <span data-ttu-id="1677e-169">Seçin **Microsoft Azure AD eşitleme** ve yeniden Başlat'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="1677e-169">Select **Microsoft Azure AD Sync** and click Restart.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1677e-170">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1677e-170">Next steps</span></span>
<span data-ttu-id="1677e-171">**Genel bakış konuları**</span><span class="sxs-lookup"><span data-stu-id="1677e-171">**Overview topics**</span></span>

* [<span data-ttu-id="1677e-172">Azure AD Connect eşitleme: anlamak ve eşitleme özelleştirme</span><span class="sxs-lookup"><span data-stu-id="1677e-172">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)

* [<span data-ttu-id="1677e-173">Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="1677e-173">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
