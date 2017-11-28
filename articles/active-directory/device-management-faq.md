---
title: "aaaAzure Active Directory cihaz yönetimi ile ilgili SSS | Microsoft Docs"
description: "Azure Active Directory cihaz Yönetimi SSS."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: cdc25576-37f2-4afb-a786-f59ba4c284c2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 000eb6a930187e13cb24cf628793afd06813be23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-device-management-faq"></a><span data-ttu-id="679a3-103">Azure Active Directory cihaz yönetimi ile ilgili SSS</span><span class="sxs-lookup"><span data-stu-id="679a3-103">Azure Active Directory device management FAQ</span></span>

<span data-ttu-id="679a3-104">**S: hello aygıt son kayıtlı. Kullanıcı bilgilerimi hello Azure portal'ın altında hello aygıt neden göremiyorum?**</span><span class="sxs-lookup"><span data-stu-id="679a3-104">**Q: I registered hello device recently. Why can’t I see hello device under my user info in hello Azure portal?**</span></span>

<span data-ttu-id="679a3-105">**Y:** ile otomatik cihaz kaydı etki alanına katılan Windows 10 cihazları gösterme altında hello kullanıcı bilgileri.</span><span class="sxs-lookup"><span data-stu-id="679a3-105">**A:** Windows 10 devices that are domain-joined with automatic device registration do not show up under hello USER info.</span></span>
<span data-ttu-id="679a3-106">Tüm cihazlar toouse PowerShell toosee gerekir.</span><span class="sxs-lookup"><span data-stu-id="679a3-106">You need toouse PowerShell toosee all devices.</span></span> 

<span data-ttu-id="679a3-107">Yalnızca hello aşağıdaki cihazları hello kullanıcı bilgileri altında listelenmiştir:</span><span class="sxs-lookup"><span data-stu-id="679a3-107">Only hello following devices are listed under hello USER info:</span></span>

- <span data-ttu-id="679a3-108">Birleştirilmiş Kurumsal olmayan tüm kişisel cihazlar</span><span class="sxs-lookup"><span data-stu-id="679a3-108">All personal devices that are not enterprise joined</span></span> 
- <span data-ttu-id="679a3-109">Tüm Windows 10 olmayan / Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="679a3-109">All non-Windows 10 / Windows Server 2016</span></span> 
- <span data-ttu-id="679a3-110">Tüm Windows dışı cihazlar</span><span class="sxs-lookup"><span data-stu-id="679a3-110">All non-Windows devices</span></span> 

---

<span data-ttu-id="679a3-111">**S: neden hello Azure portalında Azure Active Directory'de kayıtlı tüm hello cihazlar görebilirim değil mi?**</span><span class="sxs-lookup"><span data-stu-id="679a3-111">**Q: Why can I not see all hello devices registered in Azure Active Directory in hello Azure portal?**</span></span> 

<span data-ttu-id="679a3-112">**Y:** şu anda bulunmamaktadır hiçbir şekilde toosee tüm kayıtlı cihazlar hello Azure portalı.</span><span class="sxs-lookup"><span data-stu-id="679a3-112">**A:** Currently, there is no way toosee all registered devices in hello Azure portal.</span></span> <span data-ttu-id="679a3-113">Tüm cihazlar Azure PowerShell toofind kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="679a3-113">You can use Azure PowerShell toofind all devices.</span></span> <span data-ttu-id="679a3-114">Daha fazla ayrıntı için bkz: Merhaba [Get-MsolDevice](/powershell/module/msonline/get-msoldevice?view=azureadps-1.0) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="679a3-114">For more details, see hello [Get-MsolDevice](/powershell/module/msonline/get-msoldevice?view=azureadps-1.0) cmdlet.</span></span>

--- 

<span data-ttu-id="679a3-115">**Hangi hello cihaz kayıt durumu hello istemcisinin nasıl bilebilirim s: mi?**</span><span class="sxs-lookup"><span data-stu-id="679a3-115">**Q: How do I know what hello device registration state of hello client is?**</span></span>

<span data-ttu-id="679a3-116">**Y:** hello cihaz kayıt durumu bağlıdır:</span><span class="sxs-lookup"><span data-stu-id="679a3-116">**A:** hello device registration state depends on:</span></span>

- <span data-ttu-id="679a3-117">Hangi hello cihaz</span><span class="sxs-lookup"><span data-stu-id="679a3-117">What hello device is</span></span>
- <span data-ttu-id="679a3-118">Nasıl kaydedildi</span><span class="sxs-lookup"><span data-stu-id="679a3-118">How it was registered</span></span> 
- <span data-ttu-id="679a3-119">Tooit ilgili tüm ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="679a3-119">Any details related tooit.</span></span> 
 

---

<span data-ttu-id="679a3-120">**I silinmiş bir aygıt neden olduğundan hello Azure portalı veya Windows PowerShell kullanarak hala kayıtlı olarak listeleniyor?**</span><span class="sxs-lookup"><span data-stu-id="679a3-120">**Q: Why is a device I have deleted in hello Azure portal or using Windows PowerShell still listed as registered?**</span></span>

<span data-ttu-id="679a3-121">**Y:** bu tasarım gereğidir.</span><span class="sxs-lookup"><span data-stu-id="679a3-121">**A:** This is by design.</span></span> <span data-ttu-id="679a3-122">Merhaba aygıt erişim tooresources hello buluta sahip olmaz.</span><span class="sxs-lookup"><span data-stu-id="679a3-122">hello device will not have access tooresources in hello cloud.</span></span> <span data-ttu-id="679a3-123">Tooremove hello aygıt istiyorsanız ve yeniden kaydettirin işlemi el ile Merhaba cihazda gerçekleştirilen toobe olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="679a3-123">If you want tooremove hello device and register again, a manual action must be toobe taken on hello device.</span></span> 

<span data-ttu-id="679a3-124">Windows 10 ve Windows Server 2016'de, şirket içi AD etki alanına katılmış:</span><span class="sxs-lookup"><span data-stu-id="679a3-124">For Windows 10 and Windows Server 2016 that are on-premises AD domain-joined:</span></span>

1.  <span data-ttu-id="679a3-125">Merhaba komut istemini yönetici olarak açın.</span><span class="sxs-lookup"><span data-stu-id="679a3-125">Open hello command prompt as an administrator.</span></span>

2.  <span data-ttu-id="679a3-126">Türü`dsregcmd.exe /debug /leave`</span><span class="sxs-lookup"><span data-stu-id="679a3-126">Type `dsregcmd.exe /debug /leave`</span></span>

3.  <span data-ttu-id="679a3-127">Oturumu kapatın ve yeniden hello aygıtı kaydeden tootrigger hello de zamanlanmış görevi açın.</span><span class="sxs-lookup"><span data-stu-id="679a3-127">Sign out and sign in tootrigger hello scheduled task that registers hello device again.</span></span> 

<span data-ttu-id="679a3-128">Şirket içi diğer Windows platformları için AD etki alanına katılmış:</span><span class="sxs-lookup"><span data-stu-id="679a3-128">For other Windows platforms that are on-premises AD domain-joined:</span></span>

1.  <span data-ttu-id="679a3-129">Merhaba komut istemini yönetici olarak açın.</span><span class="sxs-lookup"><span data-stu-id="679a3-129">Open hello command prompt as an administrator.</span></span>
2.  <span data-ttu-id="679a3-130">`"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /l"` yazın.</span><span class="sxs-lookup"><span data-stu-id="679a3-130">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /l"`.</span></span>
3.  <span data-ttu-id="679a3-131">`"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /j"` yazın.</span><span class="sxs-lookup"><span data-stu-id="679a3-131">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /j"`.</span></span>

---

<span data-ttu-id="679a3-132">**Azure Portalı'nda yinelenen aygıt girişleri neden görüyor musunuz?**</span><span class="sxs-lookup"><span data-stu-id="679a3-132">**Q: Why do I see duplicate device entries in Azure portal?**</span></span>

<span data-ttu-id="679a3-133">**A:**</span><span class="sxs-lookup"><span data-stu-id="679a3-133">**A:**</span></span>

-   <span data-ttu-id="679a3-134">Windows 10 ve Windows Server 2016 yinelenen denemeleri toounjoin olan ve yeniden katılabilir, aynı aygıt hello için yinelenen giriş olabilir.</span><span class="sxs-lookup"><span data-stu-id="679a3-134">For Windows 10 and Windows Server 2016, if they are repeated attempts toounjoin and re-join hello same device, there might be duplicate entries.</span></span> 

-   <span data-ttu-id="679a3-135">Ekleme iş veya Okul hesabınızla kullandıysanız, eklemek iş veya Okul hesabını kullanan her bir windows kullanıcı hello ile yeni bir cihaz kaydı oluşturmak aynı aygıt adı.</span><span class="sxs-lookup"><span data-stu-id="679a3-135">If you have used Add Work or School Account, each windows user who uses Add Work or School Account will create a new device record with hello same device name.</span></span>

-   <span data-ttu-id="679a3-136">Şirket içi diğer Windows platformları AD etki alanına katılmış otomatik kayıt kullanarak yeni bir cihaz kaydı ile Merhaba oluşturur hello cihazda oturum her etki alanı kullanıcı için aynı aygıt adı.</span><span class="sxs-lookup"><span data-stu-id="679a3-136">Other Windows platforms that are on-premises AD domain-joined using automatic registration will create a new device record with hello same device name for each domain user who logs into hello device.</span></span> 

-   <span data-ttu-id="679a3-137">Temizlendiğinde bir AADJ makine yeniden yükledikten ve hello ile aynı yeniden birleştirilmiş adı, başka bir kayıtla hello olarak gösterilir aynı aygıt adı.</span><span class="sxs-lookup"><span data-stu-id="679a3-137">An AADJ machine that has been wiped, re-installed and re-joined with hello same name, will show up as another record with hello same device name.</span></span>

---

<span data-ttu-id="679a3-138">**Neden kullanıcı hello Azure portal devre dışı bırakan bir aygıttan hala kaynaklarına erişebilir mi?**</span><span class="sxs-lookup"><span data-stu-id="679a3-138">**Q: Why can a user still access resources from a device I have disabled in hello Azure portal?**</span></span>

<span data-ttu-id="679a3-139">**Y:** uygulanan revoke toobe tooan saattir yukarı alabilir.</span><span class="sxs-lookup"><span data-stu-id="679a3-139">**A:** It can take up tooan hour for a revoke toobe applied.</span></span>

>[!Note] 
><span data-ttu-id="679a3-140">Kaybolan cihazlarda, kullanıcılar hello aygıt erişemiyor hello aygıt tooensure silme öneririz.</span><span class="sxs-lookup"><span data-stu-id="679a3-140">For lost devices, we recommend wiping hello device tooensure that users cannot access hello device.</span></span> <span data-ttu-id="679a3-141">Daha fazla ayrıntı için bkz: [cihazları Yönetim için ıntune'a kaydetme](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).</span><span class="sxs-lookup"><span data-stu-id="679a3-141">For more details, see [Enroll devices for management in Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).</span></span> 


---

<span data-ttu-id="679a3-142">**Kullanıcılarım "Buradan var. alınamıyor" neden görüyor musunuz?**</span><span class="sxs-lookup"><span data-stu-id="679a3-142">**Q: Why do my users see “You can’t get there from here”?**</span></span>

<span data-ttu-id="679a3-143">**Y:** belirli koşullu erişim kuralları toorequire belirli cihaz durumu yapılandırdıktan ve hello cihaz hello ölçütleri karşılamadığında, kullanıcıların engellenir ve bu ileti görür.</span><span class="sxs-lookup"><span data-stu-id="679a3-143">**A:** If you have configured certain conditional access rules toorequire a specific device state and hello device does not meet hello criteria, users are blocked and see this message.</span></span> <span data-ttu-id="679a3-144">Merhaba aygıt lütfen hello kuralları değerlendirin ve bu ileti mümkün toomeet hello ölçütleri tooavoid içindir.</span><span class="sxs-lookup"><span data-stu-id="679a3-144">Please evaluate hello rules and ensure that hello device is able toomeet hello criteria tooavoid this message.</span></span>

---


<span data-ttu-id="679a3-145">**S: hello cihaz kaydını hello kullanıcı bilgisi'hello Azure portal'ın altında görmek ve hello durumu hello istemcide kayıtlı olarak görebilirsiniz. Koşullu erişim kullanarak ayarlarım doğru miyim?**</span><span class="sxs-lookup"><span data-stu-id="679a3-145">**Q: I see hello device record under hello USER info in hello Azure portal and can see hello state as registered on hello client. Am I setup correctly for using conditional access?**</span></span>

<span data-ttu-id="679a3-146">**Y:** hello aygıt kaydı (DeviceID) hello Azure portal durumuna gerekir eşleşen hello istemci ve koşullu erişim için herhangi bir değerlendirme ölçütleri karşılayan.</span><span class="sxs-lookup"><span data-stu-id="679a3-146">**A:** hello device record (deviceID) and state on hello Azure portal must match hello client and meet any evaluation criteria for conditional access.</span></span> <span data-ttu-id="679a3-147">Daha fazla ayrıntı için bkz: [Azure Active Directory cihaz kaydı ile çalışmaya başlama](active-directory-device-registration.md).</span><span class="sxs-lookup"><span data-stu-id="679a3-147">For more details, see [Get started with Azure Active Directory Device Registration](active-directory-device-registration.md).</span></span>

---

<span data-ttu-id="679a3-148">**Neden bir "kullanıcı adı veya parola, yanlış" iletisi alıyorum bir aygıt için t yalnızca tooAzure AD katılmış?**</span><span class="sxs-lookup"><span data-stu-id="679a3-148">**Q: Why do I get a "username or password is incorrect" message for a device I have just joined tooAzure AD?**</span></span>

<span data-ttu-id="679a3-149">**Y:** bu senaryo için yaygın nedenler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="679a3-149">**A:** Common reasons for this scenario are:</span></span>

- <span data-ttu-id="679a3-150">Kullanıcı kimlik bilgilerinizi artık geçerli değildir.</span><span class="sxs-lookup"><span data-stu-id="679a3-150">Your user credentials are no longer valid.</span></span>

- <span data-ttu-id="679a3-151">Bilgisayarınızı Azure Active Directory ile oluşturulamıyor toocommunicate ' dir.</span><span class="sxs-lookup"><span data-stu-id="679a3-151">Your computer is unable toocommunicate with Azure Active Directory.</span></span> <span data-ttu-id="679a3-152">Tüm ağ bağlantısı sorunlarını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="679a3-152">Check for any network connectivity issues.</span></span>

- <span data-ttu-id="679a3-153">Hello Azure AD katılım Önkoşullar karşılanmadı.</span><span class="sxs-lookup"><span data-stu-id="679a3-153">hello Azure AD Join pre-requisites were not met.</span></span> <span data-ttu-id="679a3-154">Lütfen başlangıç adımları izlediğinizden emin olun [bulut özellikleri tooWindows 10 cihazların Azure Active Directory katılım aracılığıyla genişletme](active-directory-azureadjoin-overview.md).</span><span class="sxs-lookup"><span data-stu-id="679a3-154">Please ensure that you have followed hello steps for [Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span></span>  

- <span data-ttu-id="679a3-155">Federe oturum açma bilgileri, Federasyon sunucusu toosupport bir WS-Trust etkin uç noktası gerektirir.</span><span class="sxs-lookup"><span data-stu-id="679a3-155">Federated logins requires your federation server toosupport a WS-Trust active endpoint.</span></span> 

---

<span data-ttu-id="679a3-156">**S: neden hello görüyorum "... Oops bir hata oluştu!" çalıştığımda iletişim Bilgisayarımda katılma?**</span><span class="sxs-lookup"><span data-stu-id="679a3-156">**Q: Why do I see hello “Oops… an error occurred!" dialog when I try do join my PC?**</span></span>

<span data-ttu-id="679a3-157">**Y:** bu bir Intune ile Azure Active Directory kaydını ayarlama sonucudur.</span><span class="sxs-lookup"><span data-stu-id="679a3-157">**A:** This is a result of setting up Azure Active Directory enrollment with Intune.</span></span> <span data-ttu-id="679a3-158">Daha fazla ayrıntı için bkz: [Windows cihaz yönetimini ayarlama](https://docs.microsoft.com/intune/deploy-use/set-up-windows-device-management-with-microsoft-intune#azure-active-directory-enrollment).</span><span class="sxs-lookup"><span data-stu-id="679a3-158">For more details, see [Set up Windows device management](https://docs.microsoft.com/intune/deploy-use/set-up-windows-device-management-with-microsoft-intune#azure-active-directory-enrollment).</span></span>  

---

<span data-ttu-id="679a3-159">**Neden bir PC başarısız hata bilgilerini almadım rağmen my girişimi toojoin mı?**</span><span class="sxs-lookup"><span data-stu-id="679a3-159">**Q: Why did my attempt toojoin a PC fail although I didn't get any error information?**</span></span>

<span data-ttu-id="679a3-160">**Y:** bir nedeni bu hello kullanıcı toohello aygıtı hello yerleşik Yönetici hesabını kullanarak oturum olması.</span><span class="sxs-lookup"><span data-stu-id="679a3-160">**A:** A likely cause is that hello user is logged in toohello device using hello built-in administrator account.</span></span> <span data-ttu-id="679a3-161">Lütfen farklı bir yerel hesap Azure Active Directory katılım toocomplete hello Kurulum kullanmadan önce oluşturun.</span><span class="sxs-lookup"><span data-stu-id="679a3-161">Please create a different local account before using Azure Active Directory Join toocomplete hello setup.</span></span> 

---

<span data-ttu-id="679a3-162">**S: otomatik cihaz kaydı hello kurulumu için yönergeler nereden bulabilirim?**</span><span class="sxs-lookup"><span data-stu-id="679a3-162">**Q: Where can I find instructions for hello setup of automatic device registration?**</span></span>

<span data-ttu-id="679a3-163">**Y:** ayrıntılı yönergeler için bkz: [nasıl tooconfigure otomatik kayıt Windows etki alanına katılmış cihazları Azure Active Directory ile](active-directory-conditional-access-automatic-device-registration-setup.md)</span><span class="sxs-lookup"><span data-stu-id="679a3-163">**A:** For detailed instructions, see [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span></span>

---

<span data-ttu-id="679a3-164">**S: sorun giderme nereden bulabilirim hello otomatik cihaz kaydı hakkında bilgi mi?**</span><span class="sxs-lookup"><span data-stu-id="679a3-164">**Q: Where can I find troubleshooting information about hello automatic device registration?**</span></span>

<span data-ttu-id="679a3-165">**Y:** sorun giderme bilgileri için bkz:</span><span class="sxs-lookup"><span data-stu-id="679a3-165">**A:** For troubleshooting information, see:</span></span>

- [<span data-ttu-id="679a3-166">Birleştirilmiş bilgisayarlar tooAzure AD – Windows 10 ve Windows Server 2016 etki alanının otomatik kayıt sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="679a3-166">Troubleshooting auto-registration of domain joined computers tooAzure AD – Windows 10 and Windows Server 2016</span></span>](active-directory-device-registration-troubleshoot-windows.md)

- [<span data-ttu-id="679a3-167">Windows alt düzey istemciler için alanına katılmış bilgisayarları tooAzure AD otomatik kaydı etki alanının sorun giderme</span><span class="sxs-lookup"><span data-stu-id="679a3-167">Troubleshooting auto-registration of domain joined computers tooAzure AD for Windows down-level clients</span></span>](active-directory-device-registration-troubleshoot-windows-legacy.md)
 
---

