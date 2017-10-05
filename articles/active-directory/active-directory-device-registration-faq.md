---
title: "Azure Active Directory otomatik cihaz kaydı SSS | Microsoft Docs"
description: "Azure Active Directory ile ilgili SSS ile otomatik cihaz kaydı."
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
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 29751239ae2a26cd7b07ddd0d8a8e706d4056b68
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-automatic-device-registration-faq"></a><span data-ttu-id="70d19-103">Azure Active Directory otomatik cihaz kaydı - SSS</span><span class="sxs-lookup"><span data-stu-id="70d19-103">Azure Active Directory automatic device registration FAQ</span></span>

<span data-ttu-id="70d19-104">**S: son cihazın kayıtlı. Azure portalında kullanıcı bilgilerimi altında aygıt neden göremiyorum?**</span><span class="sxs-lookup"><span data-stu-id="70d19-104">**Q: I registered the device recently. Why can’t I see the device under my user info in the Azure portal?**</span></span>

<span data-ttu-id="70d19-105">**Y:** ile otomatik cihaz kaydı etki alanına katılan Windows 10 cihazları gösterme altında kullanıcı bilgileri.</span><span class="sxs-lookup"><span data-stu-id="70d19-105">**A:** Windows 10 devices that are domain-joined with automatic device registration do not show up under the USER info.</span></span>
<span data-ttu-id="70d19-106">Tüm aygıtları görmek için PowerShell kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="70d19-106">You need to use PowerShell to see all devices.</span></span> 

<span data-ttu-id="70d19-107">Yalnızca aşağıdaki aygıtlar, kullanıcı bilgisi altında listelenir:</span><span class="sxs-lookup"><span data-stu-id="70d19-107">Only the following devices are listed under the USER info:</span></span>

- <span data-ttu-id="70d19-108">Birleştirilmiş Kurumsal olmayan tüm kişisel cihazlar</span><span class="sxs-lookup"><span data-stu-id="70d19-108">All personal devices that are not enterprise joined</span></span> 
- <span data-ttu-id="70d19-109">Tüm Windows 10 olmayan / Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="70d19-109">All non-Windows 10 / Windows Server 2016</span></span> 
- <span data-ttu-id="70d19-110">Tüm Windows dışı cihazlar</span><span class="sxs-lookup"><span data-stu-id="70d19-110">All non-Windows devices</span></span> 

---

<span data-ttu-id="70d19-111">**Neden Azure portalında Azure Active Directory'de kayıtlı tüm cihazları görebilirim değil mi?**</span><span class="sxs-lookup"><span data-stu-id="70d19-111">**Q: Why can I not see all the devices registered in Azure Active Directory in the Azure portal?**</span></span> 

<span data-ttu-id="70d19-112">**Y:** şu anda Azure Portalı'ndaki tüm kayıtlı cihazları görmek için bir yolu yoktur.</span><span class="sxs-lookup"><span data-stu-id="70d19-112">**A:** Currently, there is no way to see all registered devices in the Azure portal.</span></span> <span data-ttu-id="70d19-113">Tüm aygıtları bulmak için Azure PowerShell'i kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="70d19-113">You can use Azure PowerShell to find all devices.</span></span> <span data-ttu-id="70d19-114">Daha fazla ayrıntı için bkz: [Get-MsolDevice](/powershell/module/msonline/get-msoldevice?view=azureadps-1.0) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="70d19-114">For more details, see the [Get-MsolDevice](/powershell/module/msonline/get-msoldevice?view=azureadps-1.0) cmdlet.</span></span>

--- 

<span data-ttu-id="70d19-115">**S: istemci cihaz kayıt durumu nedir nasıl biliyor musunuz?**</span><span class="sxs-lookup"><span data-stu-id="70d19-115">**Q: How do I know what the device registration state of the client is?**</span></span>

<span data-ttu-id="70d19-116">**Y:** cihaz kayıt durumu bağlıdır:</span><span class="sxs-lookup"><span data-stu-id="70d19-116">**A:** The device registration state depends on:</span></span>

- <span data-ttu-id="70d19-117">Cihaz nedir</span><span class="sxs-lookup"><span data-stu-id="70d19-117">What the device is</span></span>
- <span data-ttu-id="70d19-118">Nasıl kaydedildi</span><span class="sxs-lookup"><span data-stu-id="70d19-118">How it was registered</span></span> 
- <span data-ttu-id="70d19-119">Bununla ilgili tüm ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="70d19-119">Any details related to it.</span></span> 
 

---

<span data-ttu-id="70d19-120">**Bir aygıt neden olduğundan Azure portalında silinmiş ya da Windows PowerShell kullanarak hala listelenen kayıtlı olarak?**</span><span class="sxs-lookup"><span data-stu-id="70d19-120">**Q: Why is a device I have deleted in the Azure portal or using Windows PowerShell still listed as registered?**</span></span>

<span data-ttu-id="70d19-121">**Y:** bu tasarım gereğidir.</span><span class="sxs-lookup"><span data-stu-id="70d19-121">**A:** This is by design.</span></span> <span data-ttu-id="70d19-122">Cihazın kaynaklara bulutta erişimi.</span><span class="sxs-lookup"><span data-stu-id="70d19-122">The device will not have access to resources in the cloud.</span></span> <span data-ttu-id="70d19-123">Aygıtı kaldırın ve yeniden kaydetmek istiyorsanız, el ile bir eylem cihaz üzerinde gerçekleştirilecek olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="70d19-123">If you want to remove the device and register again, a manual action must be to be taken on the device.</span></span> 

<span data-ttu-id="70d19-124">Windows 10 ve Windows Server 2016'de, şirket içi AD etki alanına katılmış:</span><span class="sxs-lookup"><span data-stu-id="70d19-124">For Windows 10 and Windows Server 2016 that are on-premises AD domain-joined:</span></span>

1.  <span data-ttu-id="70d19-125">Komut istemini yönetici olarak açın.</span><span class="sxs-lookup"><span data-stu-id="70d19-125">Open the command prompt as an administrator.</span></span>

2.  <span data-ttu-id="70d19-126">Türü`dsregcmd.exe /debug /leave`</span><span class="sxs-lookup"><span data-stu-id="70d19-126">Type `dsregcmd.exe /debug /leave`</span></span>

3.  <span data-ttu-id="70d19-127">Oturumu kapatın ve aygıt yeniden kaydeder zamanlanmış görev tetiklemek oturum açın.</span><span class="sxs-lookup"><span data-stu-id="70d19-127">Sign out and sign in to trigger the scheduled task that registers the device again.</span></span> 

<span data-ttu-id="70d19-128">Şirket içi diğer Windows platformları için AD etki alanına katılmış:</span><span class="sxs-lookup"><span data-stu-id="70d19-128">For other Windows platforms that are on-premises AD domain-joined:</span></span>

1.  <span data-ttu-id="70d19-129">Komut istemini yönetici olarak açın.</span><span class="sxs-lookup"><span data-stu-id="70d19-129">Open the command prompt as an administrator.</span></span>
2.  <span data-ttu-id="70d19-130">`"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /l"` yazın.</span><span class="sxs-lookup"><span data-stu-id="70d19-130">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /l"`.</span></span>
3.  <span data-ttu-id="70d19-131">`"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /j"` yazın.</span><span class="sxs-lookup"><span data-stu-id="70d19-131">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /j"`.</span></span>

---

<span data-ttu-id="70d19-132">**Azure Portalı'nda yinelenen aygıt girişleri neden görüyor musunuz?**</span><span class="sxs-lookup"><span data-stu-id="70d19-132">**Q: Why do I see duplicate device entries in Azure portal?**</span></span>

<span data-ttu-id="70d19-133">**A:**</span><span class="sxs-lookup"><span data-stu-id="70d19-133">**A:**</span></span>

-   <span data-ttu-id="70d19-134">Windows 10 ve Windows Server 2016 için ayrılma ve aynı aygıt yeniden katılmak için yinelenen denemeleri olmaları durumunda olabilir yinelenen girdi.</span><span class="sxs-lookup"><span data-stu-id="70d19-134">For Windows 10 and Windows Server 2016, if they are repeated attempts to unjoin and re-join the same device, there might be duplicate entries.</span></span> 

-   <span data-ttu-id="70d19-135">Ekleme iş veya Okul hesabınızla kullandıysanız, eklemek iş veya Okul hesabını kullanan her bir windows kullanıcı aynı cihaz adı ile yeni bir cihaz kaydı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="70d19-135">If you have used Add Work or School Account, each windows user who uses Add Work or School Account will create a new device record with the same device name.</span></span>

-   <span data-ttu-id="70d19-136">Şirket içi diğer Windows platformları etki alanına katılmış otomatik kayıt kullanarak AD cihazda oturum her etki alanı kullanıcı için aynı aygıt adıyla yeni bir cihaz kayıt oluşturur.</span><span class="sxs-lookup"><span data-stu-id="70d19-136">Other Windows platforms that are on-premises AD domain-joined using automatic registration will create a new device record with the same device name for each domain user who logs into the device.</span></span> 

-   <span data-ttu-id="70d19-137">Temizlenmeden, yeniden yüklendi ve aynı adla yeniden birleştirilmiş bir AADJ makine görünmesini sağlar başka bir kayıtla aynı aygıt adı olarak.</span><span class="sxs-lookup"><span data-stu-id="70d19-137">An AADJ machine that has been wiped, re-installed and re-joined with the same name, will show up as another record with the same device name.</span></span>

---

<span data-ttu-id="70d19-138">**Neden bir kullanıcı Azure portalında devre dışı bırakan bir aygıttan hala kaynaklarına erişebilir mi?**</span><span class="sxs-lookup"><span data-stu-id="70d19-138">**Q: Why can a user still access resources from a device I have disabled in the Azure portal?**</span></span>

<span data-ttu-id="70d19-139">**Y:** uygulanacak iptal etmek için bir saat sürebilir.</span><span class="sxs-lookup"><span data-stu-id="70d19-139">**A:** It can take up to an hour for a revoke to be applied.</span></span>

>[!Note] 
><span data-ttu-id="70d19-140">Kaybolan cihazlarda, Kullanıcılar Cihaz erişemiyor emin olmak için cihaz silinirken öneririz.</span><span class="sxs-lookup"><span data-stu-id="70d19-140">For lost devices, we recommend wiping the device to ensure that users cannot access the device.</span></span> <span data-ttu-id="70d19-141">Daha fazla ayrıntı için bkz: [cihazları Yönetim için ıntune'a kaydetme](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).</span><span class="sxs-lookup"><span data-stu-id="70d19-141">For more details, see [Enroll devices for management in Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).</span></span> 


---

<span data-ttu-id="70d19-142">**Kullanıcılarım "Buradan var. alınamıyor" neden görüyor musunuz?**</span><span class="sxs-lookup"><span data-stu-id="70d19-142">**Q: Why do my users see “You can’t get there from here”?**</span></span>

<span data-ttu-id="70d19-143">**Y:** belirli koşullu erişim kuralları belirli cihaz durumu gerektirecek şekilde yapılandırılmış ve cihaz ölçütleri karşılamıyor, kullanıcılar engellenir ve bu ileti görür.</span><span class="sxs-lookup"><span data-stu-id="70d19-143">**A:** If you have configured certain conditional access rules to require a specific device state and the device does not meet the criteria, users are blocked and see this message.</span></span> <span data-ttu-id="70d19-144">Lütfen kuralları değerlendirin ve cihaz bu iletinin görünmemesi için belirttiğiniz ölçütlere uyan mümkün olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="70d19-144">Please evaluate the rules and ensure that the device is able to meet the criteria to avoid this message.</span></span>

---


<span data-ttu-id="70d19-145">**S: Azure portalında kullanıcı bilgileri altında cihaz kaydı görebilir ve istemcide kayıtlı olarak durumunu görebilirsiniz. Koşullu erişim kullanarak ayarlarım doğru miyim?**</span><span class="sxs-lookup"><span data-stu-id="70d19-145">**Q: I see the device record under the USER info in the Azure portal and can see the state as registered on the client. Am I setup correctly for using conditional access?**</span></span>

<span data-ttu-id="70d19-146">**Y:** aygıt kaydı (DeviceID) ve Azure Portal'da durumu gerekir istemci eşleşen ve koşullu erişim için herhangi bir değerlendirme ölçütleri karşılayan.</span><span class="sxs-lookup"><span data-stu-id="70d19-146">**A:** The device record (deviceID) and state on the Azure portal must match the client and meet any evaluation criteria for conditional access.</span></span> <span data-ttu-id="70d19-147">Daha fazla ayrıntı için bkz: [Azure Active Directory cihaz kaydı ile çalışmaya başlama](active-directory-device-registration.md).</span><span class="sxs-lookup"><span data-stu-id="70d19-147">For more details, see [Get started with Azure Active Directory Device Registration](active-directory-device-registration.md).</span></span>

---

<span data-ttu-id="70d19-148">**Yalnızca Azure AD alanına bir aygıt için bir "kullanıcı adı veya parola, yanlış" iletisi neden sağlarım?**</span><span class="sxs-lookup"><span data-stu-id="70d19-148">**Q: Why do I get a "username or password is incorrect" message for a device I have just joined to Azure AD?**</span></span>

<span data-ttu-id="70d19-149">**Y:** bu senaryo için yaygın nedenler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="70d19-149">**A:** Common reasons for this scenario are:</span></span>

- <span data-ttu-id="70d19-150">Kullanıcı kimlik bilgilerinizi artık geçerli değildir.</span><span class="sxs-lookup"><span data-stu-id="70d19-150">Your user credentials are no longer valid.</span></span>

- <span data-ttu-id="70d19-151">Bilgisayarınızı Azure Active Directory ile iletişim kuramıyor.</span><span class="sxs-lookup"><span data-stu-id="70d19-151">Your computer is unable to communicate with Azure Active Directory.</span></span> <span data-ttu-id="70d19-152">Tüm ağ bağlantısı sorunlarını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="70d19-152">Check for any network connectivity issues.</span></span>

- <span data-ttu-id="70d19-153">Azure AD katılım ön koşulları karşılanmadı.</span><span class="sxs-lookup"><span data-stu-id="70d19-153">The Azure AD Join pre-requisites were not met.</span></span> <span data-ttu-id="70d19-154">Lütfen adımları izlediğinizden emin olun [geniletmek bulut özelliklerini Azure Active Directory katılım aracılığıyla Windows 10 cihazlarına](active-directory-azureadjoin-overview.md).</span><span class="sxs-lookup"><span data-stu-id="70d19-154">Please ensure that you have followed the steps for [Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span></span>  

- <span data-ttu-id="70d19-155">Federasyon oturumları bir WS-Trust etkin uç noktası desteklemek için Federasyon sunucusu gerektirir.</span><span class="sxs-lookup"><span data-stu-id="70d19-155">Federated logins requires your federation server to support a WS-Trust active endpoint.</span></span> 

---

<span data-ttu-id="70d19-156">**S: görmemin nedeni "... Oops bir hata oluştu!" çalıştığımda iletişim Bilgisayarımda katılma?**</span><span class="sxs-lookup"><span data-stu-id="70d19-156">**Q: Why do I see the “Oops… an error occurred!" dialog when I try do join my PC?**</span></span>

<span data-ttu-id="70d19-157">**Y:** bu bir Intune ile Azure Active Directory kaydını ayarlama sonucudur.</span><span class="sxs-lookup"><span data-stu-id="70d19-157">**A:** This is a result of setting up Azure Active Directory enrollment with Intune.</span></span> <span data-ttu-id="70d19-158">Daha fazla ayrıntı için bkz: [Windows cihaz yönetimini ayarlama](https://docs.microsoft.com/intune/deploy-use/set-up-windows-device-management-with-microsoft-intune#azure-active-directory-enrollment).</span><span class="sxs-lookup"><span data-stu-id="70d19-158">For more details, see [Set up Windows device management](https://docs.microsoft.com/intune/deploy-use/set-up-windows-device-management-with-microsoft-intune#azure-active-directory-enrollment).</span></span>  

---

<span data-ttu-id="70d19-159">**Neden hata bilgilerini almadım rağmen bir PC katılmaya my girişimi başarısız oldu?**</span><span class="sxs-lookup"><span data-stu-id="70d19-159">**Q: Why did my attempt to join a PC fail although I didn't get any error information?**</span></span>

<span data-ttu-id="70d19-160">**Y:** kullanıcının aygıtına yerleşik yönetici hesabı kullanarak açanlar bir nedeni olması.</span><span class="sxs-lookup"><span data-stu-id="70d19-160">**A:** A likely cause is that the user is logged in to the device using the built-in administrator account.</span></span> <span data-ttu-id="70d19-161">Lütfen farklı bir yerel hesap Azure Active Directory katılım Kurulumu tamamlamak için kullanmadan önce oluşturun.</span><span class="sxs-lookup"><span data-stu-id="70d19-161">Please create a different local account before using Azure Active Directory Join to complete the setup.</span></span> 

---

<span data-ttu-id="70d19-162">**S: otomatik cihaz kaydı için kurulum yönergeleri nereden bulabilirim?**</span><span class="sxs-lookup"><span data-stu-id="70d19-162">**Q: Where can I find instructions for the setup of automatic device registration?**</span></span>

<span data-ttu-id="70d19-163">**Y:** ayrıntılı yönergeler için bkz: [Azure Active Directory ile etki alanına katılmış Windows cihazlarının otomatik kaydını yapılandırma](active-directory-conditional-access-automatic-device-registration-setup.md)</span><span class="sxs-lookup"><span data-stu-id="70d19-163">**A:** For detailed instructions, see [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span></span>

---

<span data-ttu-id="70d19-164">**S: sorun giderme nereden bulabilirim otomatik cihaz kaydı hakkında bilgi mi?**</span><span class="sxs-lookup"><span data-stu-id="70d19-164">**Q: Where can I find troubleshooting information about the automatic device registration?**</span></span>

<span data-ttu-id="70d19-165">**Y:** sorun giderme bilgileri için bkz:</span><span class="sxs-lookup"><span data-stu-id="70d19-165">**A:** For troubleshooting information, see:</span></span>

- [<span data-ttu-id="70d19-166">Azure AD ile – Windows 10 ve Windows Server 2016 alanına katılmamış bilgisayarlar etki alanının otomatik kayıt sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="70d19-166">Troubleshooting auto-registration of domain joined computers to Azure AD – Windows 10 and Windows Server 2016</span></span>](active-directory-device-registration-troubleshoot-windows.md)

- [<span data-ttu-id="70d19-167">Otomatik kaydı etki alanının sorun giderme bilgisayarlar, alt düzey istemciler için Windows Azure AD alanına katılmış</span><span class="sxs-lookup"><span data-stu-id="70d19-167">Troubleshooting auto-registration of domain joined computers to Azure AD for Windows down-level clients</span></span>](active-directory-device-registration-troubleshoot-windows-legacy.md)
 
---

