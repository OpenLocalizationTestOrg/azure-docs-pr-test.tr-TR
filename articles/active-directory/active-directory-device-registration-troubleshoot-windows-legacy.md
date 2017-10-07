---
title: "aaaTroubleshooting hello otomatik kaydı Azure AD etki alanına katılmış bilgisayarları Windows alt düzey istemciler için | Microsoft Docs"
description: "Sorun giderme Hello otomatik kaydı Azure AD etki alanı bilgisayarları Windows alt düzey istemciler için katıldı."
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
ms.openlocfilehash: 84fe666576f13de09d1eaa5692517d45a4dbeebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-tooazure-ad-for-windows-down-level-clients"></a><span data-ttu-id="bf949-103">Windows alt düzey istemciler için alanına katılmış bilgisayarları tooAzure AD otomatik kaydı etki alanının sorun giderme</span><span class="sxs-lookup"><span data-stu-id="bf949-103">Troubleshooting auto-registration of domain joined computers tooAzure AD for Windows down-level clients</span></span> 

<span data-ttu-id="bf949-104">Bu konuda geçerli yalnızca toohello istemcileri aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="bf949-104">This topic is applicable only toohello following clients:</span></span> 

- <span data-ttu-id="bf949-105">Windows 7</span><span class="sxs-lookup"><span data-stu-id="bf949-105">Windows 7</span></span> 
- <span data-ttu-id="bf949-106">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="bf949-106">Windows 8.1</span></span> 
- <span data-ttu-id="bf949-107">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="bf949-107">Windows Server 2008 R2</span></span> 
- <span data-ttu-id="bf949-108">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="bf949-108">Windows Server 2012</span></span> 
- <span data-ttu-id="bf949-109">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="bf949-109">Windows Server 2012 R2</span></span> 
 

<span data-ttu-id="bf949-110">Windows 10 veya Windows Server 2016 için bkz: [alanına katılmış bilgisayarları tooAzure AD – Windows 10 ve Windows Server 2016 etki alanının otomatik kaydı sorun giderme](active-directory-device-registration-troubleshoot-windows.md).</span><span class="sxs-lookup"><span data-stu-id="bf949-110">For Windows 10 or Windows Server 2016, see [Troubleshooting auto-registration of domain joined computers tooAzure AD – Windows 10 and Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md).</span></span>

<span data-ttu-id="bf949-111">Bu konu, etki alanına katılmış aygıtlar otomatik kaydı nda olarak açıklanan yapılandırmış olduğunuz varsayılır, [nasıl tooconfigure otomatik kayıt Windows etki alanına katılmış cihazları Azure Active Directory ile](active-directory-device-registration-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="bf949-111">This topic assumes that you have configured auto-registration of domain-joined devices as outlined in described in [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-device-registration-get-started.md).</span></span>
 
<span data-ttu-id="bf949-112">Bu konu, nasıl tooresolve olası sorunlar konusunda yönergeler sorun giderme konusunda sağlar.</span><span class="sxs-lookup"><span data-stu-id="bf949-112">This topic provides you with troubleshooting guidance on how tooresolve potential issues.</span></span>  
<span data-ttu-id="bf949-113">Bazı şeyleri toonote başarılı sonuç için:</span><span class="sxs-lookup"><span data-stu-id="bf949-113">Some things toonote for successful outcomes:</span></span> 

- <span data-ttu-id="bf949-114">Bu istemciler üzerinde Azure AD kaydını kullanıcı/cihaz değil.</span><span class="sxs-lookup"><span data-stu-id="bf949-114">Registration of these clients on Azure AD is per user/device.</span></span> <span data-ttu-id="bf949-115">Örnek: jdoe ve jharnett toothis aygıtta oturum açarsanız, hello kullanıcı bilgisi sekmesinde bu kullanıcılardan her biri için ayrı bir kayıt (DeviceID) oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="bf949-115">As an example: If jdoe and jharnett log in toothis device, a separate registration (DeviceID) is created for each of these users in hello USER info tab.</span></span>  

- <span data-ttu-id="bf949-116">Kayıt hello kutusu dışında bu istemciler, oturum açma veya kilit ve kilidini yapılandırılmış tootry değil ve bu Görev Zamanlayıcı görevi kullanılarak tetiklenir 5 dakikalık gecikme olabilir.</span><span class="sxs-lookup"><span data-stu-id="bf949-116">Registration of these clients out of hello box is configured tootry at either logon or lock/unlock and there could be 5-minute delay that this is triggered using a Task Scheduler task.</span></span> 

- <span data-ttu-id="bf949-117">Bir yeniden yükleyin hello işletim sistemi veya el ile kaydı ve yeniden kaydolun üzerinde Azure AD yeni bir kayıt oluşturabilir ve birden çok giriş hello içinde hello kullanıcı bilgileri sekmesi altında Azure portal neden olur.</span><span class="sxs-lookup"><span data-stu-id="bf949-117">A re-install of hello operating system or a manual un-register and re-register may create a new registration on Azure AD and will result in multiple entries under hello USER info tab in hello Azure portal.</span></span> 


## <a name="step-1-retrieve-hello-registration-status"></a><span data-ttu-id="bf949-118">1. adım: hello kayıt durumunu alma</span><span class="sxs-lookup"><span data-stu-id="bf949-118">Step 1: Retrieve hello registration status</span></span> 

<span data-ttu-id="bf949-119">**tooverify hello kayıt durumu:**</span><span class="sxs-lookup"><span data-stu-id="bf949-119">**tooverify hello registration status:**</span></span>  

1. <span data-ttu-id="bf949-120">Bir yönetici olarak açın hello komut istemi</span><span class="sxs-lookup"><span data-stu-id="bf949-120">Open hello command prompt as an administrator</span></span> 

2. <span data-ttu-id="bf949-121">Türü`"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span><span class="sxs-lookup"><span data-stu-id="bf949-121">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span></span>

<span data-ttu-id="bf949-122">Bu komut hello birleşim durumu hakkında daha fazla ayrıntı sağlayan bir iletişim kutusu görüntüler.</span><span class="sxs-lookup"><span data-stu-id="bf949-122">This command displays a dialog box that provides you with more details about hello join status.</span></span>

![Windows için çalışma alanına katılma](./media/active-directory-device-registration-troubleshoot-windows-legacy/01.png)


## <a name="step-2-evaluate-hello-registration-status"></a><span data-ttu-id="bf949-124">2. adım: hello kayıt durumunu değerlendirme</span><span class="sxs-lookup"><span data-stu-id="bf949-124">Step 2: Evaluate hello registration status</span></span> 

<span data-ttu-id="bf949-125">Merhaba birleştirme başarılı olmadıysa hello iletişim kutusu oluştu hello sorun hakkında ayrıntılar sağlar.</span><span class="sxs-lookup"><span data-stu-id="bf949-125">If hello join was not successful, hello dialog box provides you with details about hello issue that has occured.</span></span>

<span data-ttu-id="bf949-126">**Merhaba en sık karşılaşılan sorunları şunlardır:**</span><span class="sxs-lookup"><span data-stu-id="bf949-126">**hello most common issues are:**</span></span>

- <span data-ttu-id="bf949-127">Yanlış yapılandırılmış AD FS veya Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf949-127">A misconfigured AD FS or Azure AD</span></span>

    ![Windows için çalışma alanına katılma](./media/active-directory-device-registration-troubleshoot-windows-legacy/02.png)

- <span data-ttu-id="bf949-129">Bir etki alanı kullanıcısı olarak imzalı değil</span><span class="sxs-lookup"><span data-stu-id="bf949-129">You are not signed on as a domain user</span></span>

    ![Windows için çalışma alanına katılma](./media/active-directory-device-registration-troubleshoot-windows-legacy/03.png)

- <span data-ttu-id="bf949-131">Bir kotasına ulaşıldı</span><span class="sxs-lookup"><span data-stu-id="bf949-131">A quota has been reached</span></span>

    ![Windows için çalışma alanına katılma](./media/active-directory-device-registration-troubleshoot-windows-legacy/04.png)

- <span data-ttu-id="bf949-133">Merhaba hizmeti yanıt vermiyor</span><span class="sxs-lookup"><span data-stu-id="bf949-133">hello service is not responding</span></span> 

    ![Windows için çalışma alanına katılma](./media/active-directory-device-registration-troubleshoot-windows-legacy/05.png)

<span data-ttu-id="bf949-135">Merhaba olay günlüğünde altında hello durum bilgisi bulabilirsiniz **uygulamaları ve Hizmetleri Log\Microsoft-çalışma alanına katılma**.</span><span class="sxs-lookup"><span data-stu-id="bf949-135">You can also find hello status information in hello event log under **Applications and Services Log\Microsoft-Workplace Join**.</span></span>
  
<span data-ttu-id="bf949-136">**başarısız bir kayıt için Hello en yaygın nedenler şunlardır:**</span><span class="sxs-lookup"><span data-stu-id="bf949-136">**hello most common causes for a failed registration are:**</span></span> 

- <span data-ttu-id="bf949-137">Bilgisayarınız üzerinde değil hello kuruluşunuzun iç ağ ya da bir VPN bağlantısı tooan olmadan şirket içi AD etki alanı denetleyicisi.</span><span class="sxs-lookup"><span data-stu-id="bf949-137">Your computer is not on hello organization’s internal network or a VPN without connection tooan on-premises AD domain controller.</span></span>

- <span data-ttu-id="bf949-138">Yerel bilgisayar hesabı olan tooyour bilgisayarında günlüğe kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="bf949-138">You are logged on tooyour computer with a local computer account.</span></span> 

- <span data-ttu-id="bf949-139">Hizmet yapılandırma sorunları:</span><span class="sxs-lookup"><span data-stu-id="bf949-139">Service configuration issues:</span></span> 

  - <span data-ttu-id="bf949-140">Merhaba Federasyon sunucusu yapılandırılmış toosupport bırakıldı **WIAORMULTIAUTHN**.</span><span class="sxs-lookup"><span data-stu-id="bf949-140">hello federation server has been configured toosupport **WIAORMULTIAUTHN**.</span></span> 

  - <span data-ttu-id="bf949-141">Merhaba bilgisayar için ait olduğu hello AD ormanındaki Azure AD'de tooyour doğrulanmış etki alanı adına işaret eden bir hizmet bağlantı noktası nesne yok.</span><span class="sxs-lookup"><span data-stu-id="bf949-141">There is no Service Connection Point object that points tooyour verified domain name in Azure AD in hello AD forest where hello computer belongs to.</span></span>

  - <span data-ttu-id="bf949-142">Bir kullanıcı aygıtları hello sınırına ulaştı.</span><span class="sxs-lookup"><span data-stu-id="bf949-142">A user has reached hello limit of devices.</span></span> <span data-ttu-id="bf949-143">Azure Active Directory cihaz kaydı ile çalışmaya başlama bakın.</span><span class="sxs-lookup"><span data-stu-id="bf949-143">Please see Get Started with Azure Active Directory Device Registration.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bf949-144">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bf949-144">Next steps</span></span>

<span data-ttu-id="bf949-145">Daha fazla bilgi için bkz: Merhaba [otomatik cihaz kaydı SSS](active-directory-device-registration-faq.md)</span><span class="sxs-lookup"><span data-stu-id="bf949-145">For more information, see hello [Automatic device registration FAQ](active-directory-device-registration-faq.md)</span></span> 
