---
title: "Windows alt düzey istemciler için katılmış bilgisayarları Azure AD etki alanının otomatik kayıt sorunlarını giderme | Microsoft Docs"
description: "Azure AD etki alanının otomatik kayıt sorunlarını giderme bilgisayarları Windows alt düzey istemciler için katıldı."
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
ms.openlocfilehash: a7c8ef4c59c53c21258f0c61963d8f994a3946ba
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-to-azure-ad-for-windows-down-level-clients"></a><span data-ttu-id="01d32-103">Otomatik kaydı etki alanının sorun giderme bilgisayarlar, alt düzey istemciler için Windows Azure AD alanına katılmış</span><span class="sxs-lookup"><span data-stu-id="01d32-103">Troubleshooting auto-registration of domain joined computers to Azure AD for Windows down-level clients</span></span> 

<span data-ttu-id="01d32-104">Bu konuda, yalnızca aşağıdaki istemciler için geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="01d32-104">This topic is applicable only to the following clients:</span></span> 

- <span data-ttu-id="01d32-105">Windows 7</span><span class="sxs-lookup"><span data-stu-id="01d32-105">Windows 7</span></span> 
- <span data-ttu-id="01d32-106">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="01d32-106">Windows 8.1</span></span> 
- <span data-ttu-id="01d32-107">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="01d32-107">Windows Server 2008 R2</span></span> 
- <span data-ttu-id="01d32-108">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="01d32-108">Windows Server 2012</span></span> 
- <span data-ttu-id="01d32-109">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="01d32-109">Windows Server 2012 R2</span></span> 
 

<span data-ttu-id="01d32-110">Windows 10 veya Windows Server 2016 için bkz: [etki alanının otomatik kaydı sorun giderme alanına katılmış bilgisayarları Azure AD ile – Windows 10 ve Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md).</span><span class="sxs-lookup"><span data-stu-id="01d32-110">For Windows 10 or Windows Server 2016, see [Troubleshooting auto-registration of domain joined computers to Azure AD – Windows 10 and Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md).</span></span>

<span data-ttu-id="01d32-111">Bu konu, etki alanına katılmış aygıtlar otomatik kaydı nda olarak açıklanan yapılandırmış olduğunuz varsayılır, [Azure Active Directory ile etki alanına katılmış Windows cihazlarının otomatik kaydını yapılandırma](active-directory-device-registration-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="01d32-111">This topic assumes that you have configured auto-registration of domain-joined devices as outlined in described in [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-device-registration-get-started.md).</span></span>
 
<span data-ttu-id="01d32-112">Bu konu, sorun giderme ile ilgili olası sorunları gidermek nasıl yönergelerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="01d32-112">This topic provides you with troubleshooting guidance on how to resolve potential issues.</span></span>  
<span data-ttu-id="01d32-113">Başarılı sonuç için dikkat edilecek bazı noktalar:</span><span class="sxs-lookup"><span data-stu-id="01d32-113">Some things to note for successful outcomes:</span></span> 

- <span data-ttu-id="01d32-114">Bu istemciler üzerinde Azure AD kaydını kullanıcı/cihaz değil.</span><span class="sxs-lookup"><span data-stu-id="01d32-114">Registration of these clients on Azure AD is per user/device.</span></span> <span data-ttu-id="01d32-115">Örnek: jdoe ve jharnett bu cihazda oturum açarsanız kullanıcı bilgisi sekmesinde bu kullanıcılardan her biri için ayrı bir kayıt (DeviceID) oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="01d32-115">As an example: If jdoe and jharnett log in to this device, a separate registration (DeviceID) is created for each of these users in the USER info tab.</span></span>  

- <span data-ttu-id="01d32-116">Kayıt kutunun dışında bu istemciler, oturum açma veya kilit ve kilidini denemek için yapılandırılır ve bu Görev Zamanlayıcı görevi kullanılarak tetiklenir 5 dakikalık gecikme olabilir.</span><span class="sxs-lookup"><span data-stu-id="01d32-116">Registration of these clients out of the box is configured to try at either logon or lock/unlock and there could be 5-minute delay that this is triggered using a Task Scheduler task.</span></span> 

- <span data-ttu-id="01d32-117">Bir yeniden yükleyin ve işletim sistemi veya bir el ile kaydı yeniden kaydettirin üzerinde Azure AD yeni bir kayıt oluşturabilir ve Azure portalında kullanıcı bilgileri sekmesi altında birden çok giriş neden olur.</span><span class="sxs-lookup"><span data-stu-id="01d32-117">A re-install of the operating system or a manual un-register and re-register may create a new registration on Azure AD and will result in multiple entries under the USER info tab in the Azure portal.</span></span> 


## <a name="step-1-retrieve-the-registration-status"></a><span data-ttu-id="01d32-118">1. adım: kayıt durumunu alma</span><span class="sxs-lookup"><span data-stu-id="01d32-118">Step 1: Retrieve the registration status</span></span> 

<span data-ttu-id="01d32-119">**Kayıt durumunu doğrulamak için:**</span><span class="sxs-lookup"><span data-stu-id="01d32-119">**To verify the registration status:**</span></span>  

1. <span data-ttu-id="01d32-120">Komut istemini yönetici olarak açın</span><span class="sxs-lookup"><span data-stu-id="01d32-120">Open the command prompt as an administrator</span></span> 

2. <span data-ttu-id="01d32-121">Türü`"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span><span class="sxs-lookup"><span data-stu-id="01d32-121">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span></span>

<span data-ttu-id="01d32-122">Bu komut, birleşim durumu hakkında daha fazla ayrıntı sağlayan bir iletişim kutusu görüntüler.</span><span class="sxs-lookup"><span data-stu-id="01d32-122">This command displays a dialog box that provides you with more details about the join status.</span></span>

![Windows için çalışma alanına katılma](./media/active-directory-device-registration-troubleshoot-windows-legacy/01.png)


## <a name="step-2-evaluate-the-registration-status"></a><span data-ttu-id="01d32-124">2. adım: kayıt durumunu değerlendirme</span><span class="sxs-lookup"><span data-stu-id="01d32-124">Step 2: Evaluate the registration status</span></span> 

<span data-ttu-id="01d32-125">Birleşim başarılı olmadıysa iletişim kutusu oluştu sorun hakkında ayrıntılar sağlar.</span><span class="sxs-lookup"><span data-stu-id="01d32-125">If the join was not successful, the dialog box provides you with details about the issue that has occured.</span></span>

<span data-ttu-id="01d32-126">**En yaygın sorunları şunlardır:**</span><span class="sxs-lookup"><span data-stu-id="01d32-126">**The most common issues are:**</span></span>

- <span data-ttu-id="01d32-127">Yanlış yapılandırılmış AD FS veya Azure AD</span><span class="sxs-lookup"><span data-stu-id="01d32-127">A misconfigured AD FS or Azure AD</span></span>

    ![Windows için çalışma alanına katılma](./media/active-directory-device-registration-troubleshoot-windows-legacy/02.png)

- <span data-ttu-id="01d32-129">Bir etki alanı kullanıcısı olarak imzalı değil</span><span class="sxs-lookup"><span data-stu-id="01d32-129">You are not signed on as a domain user</span></span>

    ![Windows için çalışma alanına katılma](./media/active-directory-device-registration-troubleshoot-windows-legacy/03.png)

- <span data-ttu-id="01d32-131">Bir kotasına ulaşıldı</span><span class="sxs-lookup"><span data-stu-id="01d32-131">A quota has been reached</span></span>

    ![Windows için çalışma alanına katılma](./media/active-directory-device-registration-troubleshoot-windows-legacy/04.png)

- <span data-ttu-id="01d32-133">Hizmeti yanıt vermiyor</span><span class="sxs-lookup"><span data-stu-id="01d32-133">The service is not responding</span></span> 

    ![Windows için çalışma alanına katılma](./media/active-directory-device-registration-troubleshoot-windows-legacy/05.png)

<span data-ttu-id="01d32-135">Olay günlüğünde altında durum bilgisi bulabilirsiniz **uygulamaları ve Hizmetleri Log\Microsoft-çalışma alanına katılma**.</span><span class="sxs-lookup"><span data-stu-id="01d32-135">You can also find the status information in the event log under **Applications and Services Log\Microsoft-Workplace Join**.</span></span>
  
<span data-ttu-id="01d32-136">**Başarısız bir kayıt için en yaygın nedenler şunlardır:**</span><span class="sxs-lookup"><span data-stu-id="01d32-136">**The most common causes for a failed registration are:**</span></span> 

- <span data-ttu-id="01d32-137">Bilgisayarınız bir şirket içi bağlantısı olmadan VPN'yi veya kuruluşunuzun iç ağ üzerinde değil AD etki alanı denetleyicisi.</span><span class="sxs-lookup"><span data-stu-id="01d32-137">Your computer is not on the organization’s internal network or a VPN without connection to an on-premises AD domain controller.</span></span>

- <span data-ttu-id="01d32-138">Bilgisayarınıza yerel bilgisayar hesabı ile oturum.</span><span class="sxs-lookup"><span data-stu-id="01d32-138">You are logged on to your computer with a local computer account.</span></span> 

- <span data-ttu-id="01d32-139">Hizmet yapılandırma sorunları:</span><span class="sxs-lookup"><span data-stu-id="01d32-139">Service configuration issues:</span></span> 

  - <span data-ttu-id="01d32-140">Federasyon sunucusunu desteklemek üzere yapılandırılmış **WIAORMULTIAUTHN**.</span><span class="sxs-lookup"><span data-stu-id="01d32-140">The federation server has been configured to support **WIAORMULTIAUTHN**.</span></span> 

  - <span data-ttu-id="01d32-141">Bilgisayar için ait olduğu AD ormanında Azure AD'de doğrulanmış etki alanı adınızı işaret eden bir hizmet bağlantı noktası nesne yok.</span><span class="sxs-lookup"><span data-stu-id="01d32-141">There is no Service Connection Point object that points to your verified domain name in Azure AD in the AD forest where the computer belongs to.</span></span>

  - <span data-ttu-id="01d32-142">Bir kullanıcı cihaz sınırına ulaştı.</span><span class="sxs-lookup"><span data-stu-id="01d32-142">A user has reached the limit of devices.</span></span> <span data-ttu-id="01d32-143">Azure Active Directory cihaz kaydı ile çalışmaya başlama bakın.</span><span class="sxs-lookup"><span data-stu-id="01d32-143">Please see Get Started with Azure Active Directory Device Registration.</span></span>

## <a name="next-steps"></a><span data-ttu-id="01d32-144">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="01d32-144">Next steps</span></span>

<span data-ttu-id="01d32-145">Daha fazla bilgi için bkz: [otomatik cihaz kaydı SSS](active-directory-device-registration-faq.md)</span><span class="sxs-lookup"><span data-stu-id="01d32-145">For more information, see the [Automatic device registration FAQ](active-directory-device-registration-faq.md)</span></span> 
