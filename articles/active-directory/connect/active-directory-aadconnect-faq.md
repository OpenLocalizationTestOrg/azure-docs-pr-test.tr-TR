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
ms.openlocfilehash: 39c0b127d3dcf6f45607ad8b4647a9ad79dfc732
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-azure-active-directory-connect"></a><span data-ttu-id="35b47-103">Azure Active Directory Connect için sık sorulan sorular</span><span class="sxs-lookup"><span data-stu-id="35b47-103">Frequently asked questions for Azure Active Directory Connect</span></span>

## <a name="general-installation"></a><span data-ttu-id="35b47-104">Genel yükleme</span><span class="sxs-lookup"><span data-stu-id="35b47-104">General installation</span></span>
<span data-ttu-id="35b47-105">**S: Hello Azure AD genel yönetici etkin 2FA varsa yükleme çalışacak mı?**</span><span class="sxs-lookup"><span data-stu-id="35b47-105">**Q: Will installation work if hello Azure AD Global Admin has 2FA enabled?**</span></span>  
<span data-ttu-id="35b47-106">Şubat 2016 ile yapılar Merhaba, bu desteklenir.</span><span class="sxs-lookup"><span data-stu-id="35b47-106">With hello builds from February 2016, this is supported.</span></span>

<span data-ttu-id="35b47-107">**S: bir şekilde tooinstall Azure AD Connect katılımsız var mı?**</span><span class="sxs-lookup"><span data-stu-id="35b47-107">**Q: Is there a way tooinstall Azure AD Connect unattended?**</span></span>  
<span data-ttu-id="35b47-108">Yalnızca desteklenen tooinstall Azure AD Connect olduğu hello Yükleme Sihirbazı'nı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="35b47-108">It is only supported tooinstall Azure AD Connect using hello installation wizard.</span></span> <span data-ttu-id="35b47-109">Katılımsız ve sessiz bir yükleme desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="35b47-109">An unattended and silent installation is not supported.</span></span>

<span data-ttu-id="35b47-110">**S: olduğu bir etki alanına erişilemiyor bir ormana sahibim. Azure AD Connect yükleme nasıl yaparım?**</span><span class="sxs-lookup"><span data-stu-id="35b47-110">**Q: I have a forest where one domain cannot be contacted. How do I install Azure AD Connect?**</span></span>  
<span data-ttu-id="35b47-111">Şubat 2016 ile yapılar Merhaba, bu desteklenir.</span><span class="sxs-lookup"><span data-stu-id="35b47-111">With hello builds from February 2016, this is supported.</span></span>

<span data-ttu-id="35b47-112">**S: Sunucu Çekirdeği üzerinde AD DS'yi sistem durumu aracısı çalışmanın hello mu?**</span><span class="sxs-lookup"><span data-stu-id="35b47-112">**Q: Does hello AD DS health agent work on server core?**</span></span>  
<span data-ttu-id="35b47-113">Evet.</span><span class="sxs-lookup"><span data-stu-id="35b47-113">Yes.</span></span> <span data-ttu-id="35b47-114">Merhaba aracıyı yükledikten sonra hello aşağıdaki PowerShell cmdlet'ini kullanarak hello kayıt işlemini tamamlamak:</span><span class="sxs-lookup"><span data-stu-id="35b47-114">After installing hello agent, you can complete hello registration process using hello following PowerShell cmdlet:</span></span> 

`Register-AzureADConnectHealthADDSAgent -Credentials $cred`

## <a name="network"></a><span data-ttu-id="35b47-115">Ağ</span><span class="sxs-lookup"><span data-stu-id="35b47-115">Network</span></span>
<span data-ttu-id="35b47-116">**S: sahip bir güvenlik duvarı, ağ aygıtı veya başka bir şey hello en uzun süre bağlantıları sınırlayan Ağımdaki açık kalabilir. Ne kadar süreyle my istemci tarafı zaman aşımı eşiği Azure AD Connect kullanırken olmalıdır?**</span><span class="sxs-lookup"><span data-stu-id="35b47-116">**Q: I have a firewall, network device, or something else that limits hello maximum time connections can stay open on my network. How long should my client side timeout threshold be when using Azure AD Connect?**</span></span>  
<span data-ttu-id="35b47-117">Tüm ağ yazılımı, fiziksel aygıtların ya da başka bir şey, hello Azure AD Connect istemcisinin yüklü olduğu sunucu bağlantıları açık kalabileceği en uzun süre hello arasında bağlantı için en az 5 dakika (300 saniye) eşiğinin kullanması gereken sınırları hello ve Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="35b47-117">All networking software, physical devices, or anything else that limits hello maximum time connections can remain open should use a threshold of at least 5 minutes (300 seconds) for connectivity between hello server where hello Azure AD Connect client is installed and Azure Active Directory.</span></span> <span data-ttu-id="35b47-118">Bu, daha önce yayımlanmış tooall Microsoft Identity eşitleme araçları da geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="35b47-118">This also applies tooall previously released Microsoft Identity synchronization tools.</span></span>

<span data-ttu-id="35b47-119">**S: desteklenen SLD'ler (tek etiketli etki alanları) misiniz?**</span><span class="sxs-lookup"><span data-stu-id="35b47-119">**Q: Are SLDs (Single Label Domains) supported?**</span></span>  
<span data-ttu-id="35b47-120">Hayır, Azure AD Connect, şirket içi ormanlar/SLD'ler kullanarak etki alanları desteklemez.</span><span class="sxs-lookup"><span data-stu-id="35b47-120">No, Azure AD Connect does not support on-premises forests/domains using SLDs.</span></span>

<span data-ttu-id="35b47-121">**S: "noktalı" adlı NetBIOS desteklenir?**</span><span class="sxs-lookup"><span data-stu-id="35b47-121">**Q: Are "dotted" NetBios named supported?**</span></span>  
<span data-ttu-id="35b47-122">Hayır, Azure AD Connect, şirket içi ormanlar/etki, hello NetBIOS adı içerdiği bir süre desteklemiyor "." Merhaba adı.</span><span class="sxs-lookup"><span data-stu-id="35b47-122">No, Azure AD Connect does not support on-premises forests/domains where hello NetBios name contains a period "." in hello name.</span></span>

## <a name="federation"></a><span data-ttu-id="35b47-123">Federasyon</span><span class="sxs-lookup"><span data-stu-id="35b47-123">Federation</span></span>
<span data-ttu-id="35b47-124">**S: t, bana toorenew isteyen bir e-posta almaya devam ederseniz ne yapmalıyım my Office 365 sertifika**</span><span class="sxs-lookup"><span data-stu-id="35b47-124">**Q: What do I do if I receive an email that asking me toorenew my Office 365 certificate**</span></span>  
<span data-ttu-id="35b47-125">Hello özetlenen hello yönergeleri kullanmanız [sertifikaları Yenile](active-directory-aadconnect-o365-certs.md) nasıl toorenew hello sertifika üzerindeki konu.</span><span class="sxs-lookup"><span data-stu-id="35b47-125">Use hello guidance that is outlined in hello [renew certificates](active-directory-aadconnect-o365-certs.md) topic on how toorenew hello certificate.</span></span>

<span data-ttu-id="35b47-126">**S: "Otomatik olarak bağlı olan taraf O365 bağlı olan taraf için ayarlanmış güncelleştir" sahibim. My belirteç imzalama sertifikası otomatik olarak geldiğinde ı tootake herhangi bir işlem var mı?**</span><span class="sxs-lookup"><span data-stu-id="35b47-126">**Q: I have "Automatically update relying party" set for O365 relying party. Do I have tootake any action when my token signing certificate automatically rolls over?**</span></span>  
<span data-ttu-id="35b47-127">Merhaba makalesinde ana hatlarıyla hello yönergeleri kullanmanız [sertifikaları Yenile](active-directory-aadconnect-o365-certs.md).</span><span class="sxs-lookup"><span data-stu-id="35b47-127">Use hello guidance that is outlined in hello article [renew certificates](active-directory-aadconnect-o365-certs.md).</span></span>

## <a name="environment"></a><span data-ttu-id="35b47-128">Ortam</span><span class="sxs-lookup"><span data-stu-id="35b47-128">Environment</span></span>
<span data-ttu-id="35b47-129">**S: Azure AD Connect yüklendikten sonra desteklenen BT toorename hello sunucusu mi?**</span><span class="sxs-lookup"><span data-stu-id="35b47-129">**Q: Is it supported toorename hello server after Azure AD Connect has been installed?**</span></span>  
<span data-ttu-id="35b47-130">Hayır.</span><span class="sxs-lookup"><span data-stu-id="35b47-130">No.</span></span> <span data-ttu-id="35b47-131">Merhaba sunucu adını değiştirme neden hello eşitleme altyapısı toonot mümkün tooconnect toohello SQL veritabanı olacaktır ve hello hizmet mümkün toostart olmaz.</span><span class="sxs-lookup"><span data-stu-id="35b47-131">Changing hello server name will cause hello sync engine toonot be able tooconnect toohello SQL database and hello service will not be able toostart.</span></span>

## <a name="identity-data"></a><span data-ttu-id="35b47-132">Kimlik verileri</span><span class="sxs-lookup"><span data-stu-id="35b47-132">Identity data</span></span>
<span data-ttu-id="35b47-133">**S: hello UPN (userPrincipalName) özniteliği Azure AD'de eşleşmiyor: şirket içi UPN - neden hello?**</span><span class="sxs-lookup"><span data-stu-id="35b47-133">**Q: hello UPN (userPrincipalName) attribute in Azure AD does not match hello on-prem UPN - why?**</span></span>  
<span data-ttu-id="35b47-134">Bu makalelere bakın:</span><span class="sxs-lookup"><span data-stu-id="35b47-134">See these articles:</span></span>

* [<span data-ttu-id="35b47-135">İçinde Office 365, Azure veya Intune eşleşmiyor kullanıcı adları şirket içi UPN veya alternatif oturum açma kimliği hello</span><span class="sxs-lookup"><span data-stu-id="35b47-135">User names in Office 365, Azure, or Intune don't match hello on-premises UPN or alternate login ID</span></span>](https://support.microsoft.com/en-us/kb/2523192)
* [<span data-ttu-id="35b47-136">Bir kullanıcı hesabı toouse farklı bir Federasyon etki alanına UPN hello değiştirdikten sonra değişiklikleri hello Azure Active Directory eşitleme aracı tarafından eşitlenen değil</span><span class="sxs-lookup"><span data-stu-id="35b47-136">Changes aren't synced by hello Azure Active Directory Sync tool after you change hello UPN of a user account toouse a different federated domain</span></span>](https://support.microsoft.com/en-us/kb/2669550)

<span data-ttu-id="35b47-137">Azure AD tooallow hello eşitleme altyapısı tooupdate hello userPrincipalName açıklandığı gibi yapılandırabilirsiniz [Azure AD Connect eşitleme hizmeti özelliklerini](active-directory-aadconnectsyncservice-features.md).</span><span class="sxs-lookup"><span data-stu-id="35b47-137">You can also configure Azure AD tooallow hello sync engine tooupdate hello userPrincipalName as described in [Azure AD Connect sync service features](active-directory-aadconnectsyncservice-features.md).</span></span>

<span data-ttu-id="35b47-138">**S: desteklenen BT toosoft eşleşme şirket içi AD grup/kişisi nesneleri mevcut Azure AD grup/kişisi nesnelerle mi?**</span><span class="sxs-lookup"><span data-stu-id="35b47-138">**Q: Is it supported toosoft match on-premises AD Group/Contact objects with existing Azure AD Group/Contact objects?**</span></span>  
<span data-ttu-id="35b47-139">Hayır, bu şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="35b47-139">No, this is currently not supported.</span></span>

<span data-ttu-id="35b47-140">**S: olan desteklenen BT toomanually ayarlamak İmmutableıd özniteliği var olan Azure AD Grup/başvurun nesneleri toohard eşleşen onu tooon içi AD Grup/kişi nesneleri?**</span><span class="sxs-lookup"><span data-stu-id="35b47-140">**Q: Is it supported toomanually set ImmutableId attribute on existing Azure AD Group/Contact objects toohard match it tooon-premises AD Group/Contact objects?**</span></span>  
<span data-ttu-id="35b47-141">Hayır, bu şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="35b47-141">No, this is currently not supported.</span></span>



## <a name="custom-configuration"></a><span data-ttu-id="35b47-142">Özel yapılandırma</span><span class="sxs-lookup"><span data-stu-id="35b47-142">Custom configuration</span></span>
<span data-ttu-id="35b47-143">**S: hello PowerShell cmdlet'leri için Azure AD Connect belgelenen nerede?**</span><span class="sxs-lookup"><span data-stu-id="35b47-143">**Q: Where are hello PowerShell cmdlets for Azure AD Connect documented?**</span></span>  
<span data-ttu-id="35b47-144">Bu sitede belgelenen hello cmdlet'leri Hello özel durum ile Azure AD Connect içinde bulunan diğer PowerShell cmdlet'leri müşteri kullanım için desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="35b47-144">With hello exception of hello cmdlets documented on this site, other PowerShell cmdlets found in Azure AD Connect are not supported for customer use.</span></span>

<span data-ttu-id="35b47-145">**S: "sunucu dışa aktarma/sunucu alma bulundu" kullanabilirim *Eşitleme Hizmeti Yöneticisi'ni* toomove yapılandırma sunucusu arasında?**</span><span class="sxs-lookup"><span data-stu-id="35b47-145">**Q: Can I use "Server export/server import" found in *Synchronization Service Manager* toomove configuration between servers?**</span></span>  
<span data-ttu-id="35b47-146">Hayır.</span><span class="sxs-lookup"><span data-stu-id="35b47-146">No.</span></span> <span data-ttu-id="35b47-147">Bu seçenek, tüm yapılandırma ayarlarını almaz ve kullanılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="35b47-147">This option will not retrieve all configuration settings and should not be used.</span></span> <span data-ttu-id="35b47-148">Bunun yerine hello ikinci sunucusunda hello toocreate hello temel Yapılandırma Sihirbazı'nı kullanın ve hello eşitleme kuralı Düzenleyicisi toogenerate PowerShell komut dosyaları toomove sunucular arasında herhangi bir özel kural kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="35b47-148">You should instead use hello wizard toocreate hello base configuration on hello second server and use hello sync rule editor toogenerate PowerShell scripts toomove any custom rule between servers.</span></span> <span data-ttu-id="35b47-149">Bkz: [çarpma geçiş](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span><span class="sxs-lookup"><span data-stu-id="35b47-149">See [Swing migration](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span></span>

<span data-ttu-id="35b47-150">**S: parolalar için hello Azure oturum açma sayfası önbelleğe alınabilir ve bir parola input öğesi hello otomatik tamamlama ile içerdiğinden bu engellenebilir = "false" özniteliği?**</span><span class="sxs-lookup"><span data-stu-id="35b47-150">**Q: Can passwords be cached for hello Azure sign-in page and can this be prevented since it contains a password input element with hello autocomplete = "false" attribute?**</span></span></br>
<span data-ttu-id="35b47-151">Şu anda hello otomatik tamamlama etiketi de dahil olmak üzere hello parola giriş alanı değiştirme hello HTML özniteliklerini desteklemiyoruz.</span><span class="sxs-lookup"><span data-stu-id="35b47-151">We currently do not support modifying hello HTML attributes of hello Password input field, including hello autocomplete tag.</span></span> <span data-ttu-id="35b47-152">Şu anda tooadd olanak tanıyan özel Javascript için izin veren bir özellik üzerinde herhangi bir öznitelik toohello parola alan çalışıyoruz.</span><span class="sxs-lookup"><span data-stu-id="35b47-152">We are currently working on a feature that will allow for custom Javascript which will allow you tooadd any attribute toohello password field.</span></span> <span data-ttu-id="35b47-153">Bu 2017 kullanılabilir sonraki parçası olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="35b47-153">This should be available later part of 2017.</span></span>

<span data-ttu-id="35b47-154">**S: Azure oturum açma sayfası Hello üzerinde önceden başarıyla oturum açtıktan kullanıcılar için kullanıcı adları gösterilir.  Bu davranış kapalı?**</span><span class="sxs-lookup"><span data-stu-id="35b47-154">**Q: On hello Azure sign-in page, usernames for users who have previously signed in successfully are shown.  Can this behavior be turned off?**</span></span></br>
<span data-ttu-id="35b47-155">Şu anda hello oturum açma sayfası değiştirme hello HTML özniteliklerini desteklemiyoruz.</span><span class="sxs-lookup"><span data-stu-id="35b47-155">We currently do not support modifying hello HTML attributes of hello sign-in page.</span></span> <span data-ttu-id="35b47-156">Şu anda tooadd olanak tanıyan özel Javascript için izin veren bir özellik üzerinde herhangi bir öznitelik toohello parola alan çalışıyoruz.</span><span class="sxs-lookup"><span data-stu-id="35b47-156">We are currently working on a feature that will allow for custom Javascript which will allow you tooadd any attribute toohello password field.</span></span> <span data-ttu-id="35b47-157">Bu 2017 kullanılabilir sonraki parçası olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="35b47-157">This should be available later part of 2017.</span></span>

<span data-ttu-id="35b47-158">**S: bir şekilde tooprevent eşzamanlı oturum var mı?**</span><span class="sxs-lookup"><span data-stu-id="35b47-158">**Q: Is there a way tooprevent concurrent sessions?**</span></span></br>
<span data-ttu-id="35b47-159">Hayır.</span><span class="sxs-lookup"><span data-stu-id="35b47-159">No.</span></span>



## <a name="troubleshooting"></a><span data-ttu-id="35b47-160">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="35b47-160">Troubleshooting</span></span>
<span data-ttu-id="35b47-161">**S: Azure AD Connect ile ilgili Yardım nasıl alabilirim?**</span><span class="sxs-lookup"><span data-stu-id="35b47-161">**Q: How can I get help with Azure AD Connect?**</span></span>

[<span data-ttu-id="35b47-162">Arama hello Microsoft Bilgi Bankası (KB)</span><span class="sxs-lookup"><span data-stu-id="35b47-162">Search hello Microsoft Knowledge Base (KB)</span></span>](https://www.microsoft.com/en-us/Search/result.aspx?q=azure%20active%20directory%20connect&form=mssupport)

* <span data-ttu-id="35b47-163">Azure AD Connect desteği hakkında teknik çözümler toocommon onarım sorunlar için Microsoft Bilgi Bankası (KB) Hello arayın.</span><span class="sxs-lookup"><span data-stu-id="35b47-163">Search hello Microsoft Knowledge Base (KB) for technical solutions toocommon break-fix issues about Support for Azure AD Connect.</span></span>

[<span data-ttu-id="35b47-164">Microsoft Azure Active Directory forumları</span><span class="sxs-lookup"><span data-stu-id="35b47-164">Microsoft Azure Active Directory Forums</span></span>](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=WindowsAzureAD)

* <span data-ttu-id="35b47-165">Arama ve teknik sorular ve yanıtlar hello Topluluğu'ndan veya kendi tıklayarak soru sorun göz atmak [burada](https://social.msdn.microsoft.com/Forums/azure/en-US/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required).</span><span class="sxs-lookup"><span data-stu-id="35b47-165">You can search and browse for technical questions and answers from hello community or ask your own question by clicking [here](https://social.msdn.microsoft.com/Forums/azure/en-US/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required).</span></span>

[<span data-ttu-id="35b47-166">Azure AD Connect müşteri desteği</span><span class="sxs-lookup"><span data-stu-id="35b47-166">Azure AD Connect customer support</span></span>](https://manage.windowsazure.com/?getsupport=true)

* <span data-ttu-id="35b47-167">Bu bağlantıyı tooget destek hello Azure portal aracılığıyla kullanın.</span><span class="sxs-lookup"><span data-stu-id="35b47-167">Use this link tooget support through hello Azure portal.</span></span>

