---
title: 'Azure Active Directory Connect: SSS - | Microsoft Docs'
description: "Bu sayfa, Azure AD Connect hakkında sık bir sorulan sorular."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
ms.assetid: 4e47a087-ebcd-4b63-9574-0c31907a39a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: fd5988b2d4170166902bb5cc39603d4a0f83be59
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="frequently-asked-questions-for-azure-active-directory-connect"></a><span data-ttu-id="93a53-103">Azure Active Directory Connect için sık sorulan sorular</span><span class="sxs-lookup"><span data-stu-id="93a53-103">Frequently asked questions for Azure Active Directory Connect</span></span>

## <a name="general-installation"></a><span data-ttu-id="93a53-104">Genel yükleme</span><span class="sxs-lookup"><span data-stu-id="93a53-104">General installation</span></span>
<span data-ttu-id="93a53-105">**S: Azure AD genel yönetici etkin 2FA varsa yükleme çalışacak mı?**</span><span class="sxs-lookup"><span data-stu-id="93a53-105">**Q: Will installation work if the Azure AD Global Admin has 2FA enabled?**</span></span>  
<span data-ttu-id="93a53-106">Şubat 2016 yapılar ile bu desteklenir.</span><span class="sxs-lookup"><span data-stu-id="93a53-106">With the builds from February 2016, this is supported.</span></span>

<span data-ttu-id="93a53-107">**S: Azure AD Connect Katılımsız yüklemenin bir yolu var mı?**</span><span class="sxs-lookup"><span data-stu-id="93a53-107">**Q: Is there a way to install Azure AD Connect unattended?**</span></span>  
<span data-ttu-id="93a53-108">Yalnızca Azure AD Connect Yükleme Sihirbazı'nı kullanarak yüklemek için desteklenir.</span><span class="sxs-lookup"><span data-stu-id="93a53-108">It is only supported to install Azure AD Connect using the installation wizard.</span></span> <span data-ttu-id="93a53-109">Katılımsız ve sessiz bir yükleme desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="93a53-109">An unattended and silent installation is not supported.</span></span>

<span data-ttu-id="93a53-110">**S: olduğu bir etki alanına erişilemiyor bir ormana sahibim. Azure AD Connect yükleme nasıl yaparım?**</span><span class="sxs-lookup"><span data-stu-id="93a53-110">**Q: I have a forest where one domain cannot be contacted. How do I install Azure AD Connect?**</span></span>  
<span data-ttu-id="93a53-111">Şubat 2016 yapılar ile bu desteklenir.</span><span class="sxs-lookup"><span data-stu-id="93a53-111">With the builds from February 2016, this is supported.</span></span>

<span data-ttu-id="93a53-112">**S: AD DS Sistem Durumu Aracısı Sunucu Çekirdeği yüklemesinde çalışmıyor?**</span><span class="sxs-lookup"><span data-stu-id="93a53-112">**Q: Does the AD DS health agent work on server core?**</span></span>  
<span data-ttu-id="93a53-113">Evet.</span><span class="sxs-lookup"><span data-stu-id="93a53-113">Yes.</span></span> <span data-ttu-id="93a53-114">Aracıyı yükledikten sonra aşağıdaki PowerShell cmdlet'ini kullanarak kayıt işlemini tamamlamak:</span><span class="sxs-lookup"><span data-stu-id="93a53-114">After installing the agent, you can complete the registration process using the following PowerShell cmdlet:</span></span> 

`Register-AzureADConnectHealthADDSAgent -Credentials $cred`

## <a name="network"></a><span data-ttu-id="93a53-115">Ağ</span><span class="sxs-lookup"><span data-stu-id="93a53-115">Network</span></span>
<span data-ttu-id="93a53-116">**S: sahibim bir güvenlik duvarı, ağ aygıtını veya başka bir şey en uzun süre bağlantıları sınırlayan Ağımdaki açık kalabilir. Ne kadar süreyle my istemci tarafı zaman aşımı eşiği Azure AD Connect kullanırken olmalıdır?**</span><span class="sxs-lookup"><span data-stu-id="93a53-116">**Q: I have a firewall, network device, or something else that limits the maximum time connections can stay open on my network. How long should my client side timeout threshold be when using Azure AD Connect?**</span></span>  
<span data-ttu-id="93a53-117">Tüm ağ yazılımı, fiziksel aygıtların ya da başka bir şey bağlantıları açık kalabileceği en uzun süre sınırlayan bir eşik en az 5 dakika (300 saniye olarak) Azure Active Directory ve Azure AD Connect istemcisinin yüklü olduğu sunucu arasındaki bağlantıyı için kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="93a53-117">All networking software, physical devices, or anything else that limits the maximum time connections can remain open should use a threshold of at least 5 minutes (300 seconds) for connectivity between the server where the Azure AD Connect client is installed and Azure Active Directory.</span></span> <span data-ttu-id="93a53-118">Bu durum, tüm daha önce yayımlanmış Microsoft Identity eşitleme araçları için de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="93a53-118">This also applies to all previously released Microsoft Identity synchronization tools.</span></span>

<span data-ttu-id="93a53-119">**S: desteklenen SLD'ler (tek etiketli etki alanları) misiniz?**</span><span class="sxs-lookup"><span data-stu-id="93a53-119">**Q: Are SLDs (Single Label Domains) supported?**</span></span>  
<span data-ttu-id="93a53-120">Hayır, Azure AD Connect, şirket içi ormanlar/SLD'ler kullanarak etki alanları desteklemez.</span><span class="sxs-lookup"><span data-stu-id="93a53-120">No, Azure AD Connect does not support on-premises forests/domains using SLDs.</span></span>

<span data-ttu-id="93a53-121">**S: "noktalı" adlı NetBIOS desteklenir?**</span><span class="sxs-lookup"><span data-stu-id="93a53-121">**Q: Are "dotted" NetBios named supported?**</span></span>  
<span data-ttu-id="93a53-122">Hayır, Azure AD Connect, şirket içi ormanlar/etki, NetBIOS adını içerdiği bir süre desteklemiyor "." adında.</span><span class="sxs-lookup"><span data-stu-id="93a53-122">No, Azure AD Connect does not support on-premises forests/domains where the NetBios name contains a period "." in the name.</span></span>

## <a name="federation"></a><span data-ttu-id="93a53-123">Federasyon</span><span class="sxs-lookup"><span data-stu-id="93a53-123">Federation</span></span>
<span data-ttu-id="93a53-124">**S: t, bana my Office 365 sertifikayı yenilemek için isteyen bir e-posta almaya devam ederseniz ne yapmalıyım**</span><span class="sxs-lookup"><span data-stu-id="93a53-124">**Q: What do I do if I receive an email that asking me to renew my Office 365 certificate**</span></span>  
<span data-ttu-id="93a53-125">İçinde açıklanan yönergeleri kullanmanız [sertifikaları Yenile](active-directory-aadconnect-o365-certs.md) sertifikayı yenilemek nasıl konu.</span><span class="sxs-lookup"><span data-stu-id="93a53-125">Use the guidance that is outlined in the [renew certificates](active-directory-aadconnect-o365-certs.md) topic on how to renew the certificate.</span></span>

<span data-ttu-id="93a53-126">**S: "Otomatik olarak bağlı olan taraf O365 bağlı olan taraf için ayarlanmış güncelleştir" sahibim. My belirteç imzalama sertifikası otomatik olarak geldiğinde herhangi bir eylemde bulunmanız gerekir mi?**</span><span class="sxs-lookup"><span data-stu-id="93a53-126">**Q: I have "Automatically update relying party" set for O365 relying party. Do I have to take any action when my token signing certificate automatically rolls over?**</span></span>  
<span data-ttu-id="93a53-127">Makalede açıklanan yönergeleri kullanmanız [sertifikaları Yenile](active-directory-aadconnect-o365-certs.md).</span><span class="sxs-lookup"><span data-stu-id="93a53-127">Use the guidance that is outlined in the article [renew certificates](active-directory-aadconnect-o365-certs.md).</span></span>

## <a name="environment"></a><span data-ttu-id="93a53-128">Ortam</span><span class="sxs-lookup"><span data-stu-id="93a53-128">Environment</span></span>
<span data-ttu-id="93a53-129">**S: Azure AD Connect yüklendikten sonra sunucuyu yeniden adlandırmak için destekleniyor mu?**</span><span class="sxs-lookup"><span data-stu-id="93a53-129">**Q: Is it supported to rename the server after Azure AD Connect has been installed?**</span></span>  
<span data-ttu-id="93a53-130">Hayır.</span><span class="sxs-lookup"><span data-stu-id="93a53-130">No.</span></span> <span data-ttu-id="93a53-131">Sunucu adının değiştirilmesi SQL veritabanına bağlanabilmek için olmaması eşitleme altyapısı neden olur ve hizmeti başlatmak mümkün olmaz.</span><span class="sxs-lookup"><span data-stu-id="93a53-131">Changing the server name will cause the sync engine to not be able to connect to the SQL database and the service will not be able to start.</span></span>

## <a name="identity-data"></a><span data-ttu-id="93a53-132">Kimlik verileri</span><span class="sxs-lookup"><span data-stu-id="93a53-132">Identity data</span></span>
<span data-ttu-id="93a53-133">**S: Azure AD UPN (userPrincipalName) özniteliğinde şirket içi UPN - neden eşleşmiyor?**</span><span class="sxs-lookup"><span data-stu-id="93a53-133">**Q: The UPN (userPrincipalName) attribute in Azure AD does not match the on-prem UPN - why?**</span></span>  
<span data-ttu-id="93a53-134">Bu makalelere bakın:</span><span class="sxs-lookup"><span data-stu-id="93a53-134">See these articles:</span></span>

* [<span data-ttu-id="93a53-135">Office 365, Azure veya Intune kullanıcı adları şirket içi UPN veya alternatif oturum açma kimliği eşleşmiyor</span><span class="sxs-lookup"><span data-stu-id="93a53-135">User names in Office 365, Azure, or Intune don't match the on-premises UPN or alternate login ID</span></span>](https://support.microsoft.com/en-us/kb/2523192)
* [<span data-ttu-id="93a53-136">Farklı bir Federasyon etki alanını kullanmak için bir kullanıcı hesabının UPN değiştirdikten sonra değişiklikleri Azure Active Directory eşitleme aracı tarafından eşitlenen değil</span><span class="sxs-lookup"><span data-stu-id="93a53-136">Changes aren't synced by the Azure Active Directory Sync tool after you change the UPN of a user account to use a different federated domain</span></span>](https://support.microsoft.com/en-us/kb/2669550)

<span data-ttu-id="93a53-137">UserPrincipalName açıklandığı şekilde güncelleştirmek eşitleme altyapısı izin vermek için Azure AD de yapılandırabilirsiniz [Azure AD Connect eşitleme hizmeti özelliklerini](active-directory-aadconnectsyncservice-features.md).</span><span class="sxs-lookup"><span data-stu-id="93a53-137">You can also configure Azure AD to allow the sync engine to update the userPrincipalName as described in [Azure AD Connect sync service features](active-directory-aadconnectsyncservice-features.md).</span></span>

<span data-ttu-id="93a53-138">**S: olan yazılım eşleşen desteklenen şirket içi AD grup/kişisi nesneleri ile var olan Azure AD Grup/kişi nesneleri?**</span><span class="sxs-lookup"><span data-stu-id="93a53-138">**Q: Is it supported to soft match on-premises AD Group/Contact objects with existing Azure AD Group/Contact objects?**</span></span>  
<span data-ttu-id="93a53-139">Hayır, bu şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="93a53-139">No, this is currently not supported.</span></span>

<span data-ttu-id="93a53-140">**S: olan desteklenen el ile ayarlamak için sabit kendisine eşleştirmek için var olan Azure AD Grup/kişi nesneleri İmmutableıd özniteliği şirket içi AD Grup/kişi nesneleri?**</span><span class="sxs-lookup"><span data-stu-id="93a53-140">**Q: Is it supported to manually set ImmutableId attribute on existing Azure AD Group/Contact objects to hard match it to on-premises AD Group/Contact objects?**</span></span>  
<span data-ttu-id="93a53-141">Hayır, bu şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="93a53-141">No, this is currently not supported.</span></span>



## <a name="custom-configuration"></a><span data-ttu-id="93a53-142">Özel yapılandırma</span><span class="sxs-lookup"><span data-stu-id="93a53-142">Custom configuration</span></span>
<span data-ttu-id="93a53-143">**S: Burada Azure AD Connect için PowerShell cmdlet'leri belgelenen?**</span><span class="sxs-lookup"><span data-stu-id="93a53-143">**Q: Where are the PowerShell cmdlets for Azure AD Connect documented?**</span></span>  
<span data-ttu-id="93a53-144">Bu sitede belgelenen cmdlet'leri hariç olmak üzere, Azure AD Connect içinde bulunan diğer PowerShell cmdlet'leri müşteri kullanım için desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="93a53-144">With the exception of the cmdlets documented on this site, other PowerShell cmdlets found in Azure AD Connect are not supported for customer use.</span></span>

<span data-ttu-id="93a53-145">**S: "sunucu dışa aktarma/sunucu alma bulundu" kullanabilirim *Eşitleme Hizmeti Yöneticisi'ni* yapılandırma sunucuları arasında taşımak için?**</span><span class="sxs-lookup"><span data-stu-id="93a53-145">**Q: Can I use "Server export/server import" found in *Synchronization Service Manager* to move configuration between servers?**</span></span>  
<span data-ttu-id="93a53-146">Hayır.</span><span class="sxs-lookup"><span data-stu-id="93a53-146">No.</span></span> <span data-ttu-id="93a53-147">Bu seçenek, tüm yapılandırma ayarlarını almaz ve kullanılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="93a53-147">This option will not retrieve all configuration settings and should not be used.</span></span> <span data-ttu-id="93a53-148">Bunun yerine, temel yapılandırma ikinci sunucusunda oluşturmak ve herhangi bir özel kural sunucular arasında taşımak için PowerShell komut dosyaları oluşturmak için eşitleme kuralı Düzenleyicisi'ni kullanmak için Sihirbazı'nı kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="93a53-148">You should instead use the wizard to create the base configuration on the second server and use the sync rule editor to generate PowerShell scripts to move any custom rule between servers.</span></span> <span data-ttu-id="93a53-149">Bkz: [çarpma geçiş](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span><span class="sxs-lookup"><span data-stu-id="93a53-149">See [Swing migration](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span></span>

<span data-ttu-id="93a53-150">**S: Azure oturum açma sayfası için parolaları önbelleğe ve bir parola input öğesi otomatik tamamlama ile içerdiğinden bu engellenebilir = "false" özniteliği?**</span><span class="sxs-lookup"><span data-stu-id="93a53-150">**Q: Can passwords be cached for the Azure sign-in page and can this be prevented since it contains a password input element with the autocomplete = "false" attribute?**</span></span></br>
<span data-ttu-id="93a53-151">Şu anda parola giriş alanını otomatik tamamlama etiketi de dahil olmak üzere, HTML özniteliklerini değiştirme desteklemiyoruz.</span><span class="sxs-lookup"><span data-stu-id="93a53-151">We currently do not support modifying the HTML attributes of the Password input field, including the autocomplete tag.</span></span> <span data-ttu-id="93a53-152">Şu anda herhangi bir öznitelik parola alanına eklemenize olanak tanıyan özel Javascript için izin veren bir özellik üzerinde çalışıyoruz.</span><span class="sxs-lookup"><span data-stu-id="93a53-152">We are currently working on a feature that will allow for custom Javascript which will allow you to add any attribute to the password field.</span></span> <span data-ttu-id="93a53-153">Bu 2017 kullanılabilir sonraki parçası olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="93a53-153">This should be available later part of 2017.</span></span>

<span data-ttu-id="93a53-154">**S: Azure oturum açma sayfasında, daha önce başarıyla oturum açtıktan kullanıcılar için kullanıcı adları gösterilir.  Bu davranış kapalı?**</span><span class="sxs-lookup"><span data-stu-id="93a53-154">**Q: On the Azure sign-in page, usernames for users who have previously signed in successfully are shown.  Can this behavior be turned off?**</span></span></br>
<span data-ttu-id="93a53-155">Şu anda oturum açma sayfasının HTML özniteliklerini değiştirme desteklemiyoruz.</span><span class="sxs-lookup"><span data-stu-id="93a53-155">We currently do not support modifying the HTML attributes of the sign-in page.</span></span> <span data-ttu-id="93a53-156">Şu anda herhangi bir öznitelik parola alanına eklemenize olanak tanıyan özel Javascript için izin veren bir özellik üzerinde çalışıyoruz.</span><span class="sxs-lookup"><span data-stu-id="93a53-156">We are currently working on a feature that will allow for custom Javascript which will allow you to add any attribute to the password field.</span></span> <span data-ttu-id="93a53-157">Bu 2017 kullanılabilir sonraki parçası olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="93a53-157">This should be available later part of 2017.</span></span>

<span data-ttu-id="93a53-158">**S: eşzamanlı oturum önlemek için bir yol var mı?**</span><span class="sxs-lookup"><span data-stu-id="93a53-158">**Q: Is there a way to prevent concurrent sessions?**</span></span></br>
<span data-ttu-id="93a53-159">Hayır.</span><span class="sxs-lookup"><span data-stu-id="93a53-159">No.</span></span>



## <a name="troubleshooting"></a><span data-ttu-id="93a53-160">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="93a53-160">Troubleshooting</span></span>
<span data-ttu-id="93a53-161">**S: Azure AD Connect ile ilgili Yardım nasıl alabilirim?**</span><span class="sxs-lookup"><span data-stu-id="93a53-161">**Q: How can I get help with Azure AD Connect?**</span></span>

[<span data-ttu-id="93a53-162">Microsoft Bilgi Bankası'nda (KB) arama</span><span class="sxs-lookup"><span data-stu-id="93a53-162">Search the Microsoft Knowledge Base (KB)</span></span>](https://www.microsoft.com/en-us/Search/result.aspx?q=azure%20active%20directory%20connect&form=mssupport)

* <span data-ttu-id="93a53-163">Ortak onarım sorunları Azure AD Connect desteği hakkında teknik çözümleri için Microsoft Bilgi Bankası (KB) arayın.</span><span class="sxs-lookup"><span data-stu-id="93a53-163">Search the Microsoft Knowledge Base (KB) for technical solutions to common break-fix issues about Support for Azure AD Connect.</span></span>

[<span data-ttu-id="93a53-164">Microsoft Azure Active Directory forumları</span><span class="sxs-lookup"><span data-stu-id="93a53-164">Microsoft Azure Active Directory Forums</span></span>](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=WindowsAzureAD)

* <span data-ttu-id="93a53-165">Arama ve teknik sorular ve yanıtlar topluluktan veya kendi tıklayarak soru sorun göz atmak [burada](https://social.msdn.microsoft.com/Forums/azure/en-US/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required).</span><span class="sxs-lookup"><span data-stu-id="93a53-165">You can search and browse for technical questions and answers from the community or ask your own question by clicking [here](https://social.msdn.microsoft.com/Forums/azure/en-US/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required).</span></span>

[<span data-ttu-id="93a53-166">Azure AD Connect müşteri desteği</span><span class="sxs-lookup"><span data-stu-id="93a53-166">Azure AD Connect customer support</span></span>](https://manage.windowsazure.com/?getsupport=true)

* <span data-ttu-id="93a53-167">Azure portalı üzerinden destek almak için bu bağlantıyı kullanın.</span><span class="sxs-lookup"><span data-stu-id="93a53-167">Use this link to get support through the Azure portal.</span></span>

