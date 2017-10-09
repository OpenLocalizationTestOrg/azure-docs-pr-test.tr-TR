---
title: "aaaTroubleshooting karma Azure Active Directory birleştirilmiş alt düzey aygıtları | Microsoft Docs"
description: "Karma Azure Active Directory sorun giderme alt düzey aygıtları katıldı."
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
ms.openlocfilehash: edd56b89579fac6b427732902284ad9c568b87b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hybrid-azure-active-directory-joined-down-level-devices"></a><span data-ttu-id="ba06b-103">Alt düzey aygıtları birleştirilmiş karma Azure Active Directory sorun giderme</span><span class="sxs-lookup"><span data-stu-id="ba06b-103">Troubleshooting hybrid Azure Active Directory joined down-level devices</span></span> 

<span data-ttu-id="ba06b-104">Bu konuda geçerli yalnızca toohello cihazları aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="ba06b-104">This topic is applicable only toohello following devices:</span></span> 

- <span data-ttu-id="ba06b-105">Windows 7</span><span class="sxs-lookup"><span data-stu-id="ba06b-105">Windows 7</span></span> 
- <span data-ttu-id="ba06b-106">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="ba06b-106">Windows 8.1</span></span> 
- <span data-ttu-id="ba06b-107">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="ba06b-107">Windows Server 2008 R2</span></span> 
- <span data-ttu-id="ba06b-108">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="ba06b-108">Windows Server 2012</span></span> 
- <span data-ttu-id="ba06b-109">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="ba06b-109">Windows Server 2012 R2</span></span> 
 

<span data-ttu-id="ba06b-110">Windows 10 veya Windows Server 2016 için bkz: [sorun giderme karma Azure Active Directory'ye katılmış Windows 10 ve Windows Server 2016 cihazları](device-management-troubleshoot-hybrid-join-windows-current.md).</span><span class="sxs-lookup"><span data-stu-id="ba06b-110">For Windows 10 or Windows Server 2016, see [Troubleshooting hybrid Azure Active Directory joined Windows 10 and Windows Server 2016 devices](device-management-troubleshoot-hybrid-join-windows-current.md).</span></span>

<span data-ttu-id="ba06b-111">Bu konu, sahibi olduğunuzu varsayar [yapılandırılmış karma Azure Active Directory'ye katılmış cihazları](device-management-hybrid-azuread-joined-devices-setup.md) toosupport hello senaryolar:</span><span class="sxs-lookup"><span data-stu-id="ba06b-111">This topic assumes that you have [configured hybrid Azure Active Directory joined devices](device-management-hybrid-azuread-joined-devices-setup.md) toosupport hello following scenarios:</span></span>

- <span data-ttu-id="ba06b-112">Cihaz temelli koşullu erişim</span><span class="sxs-lookup"><span data-stu-id="ba06b-112">Device-based conditional access</span></span>

- [<span data-ttu-id="ba06b-113">Kurumsal Dolaşım ayarları</span><span class="sxs-lookup"><span data-stu-id="ba06b-113">Enterprise roaming of settings</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)

- [<span data-ttu-id="ba06b-114">İş İçin Windows Hello</span><span class="sxs-lookup"><span data-stu-id="ba06b-114">Windows Hello for Business</span></span>](active-directory-azureadjoin-passport-deployment.md) 





<span data-ttu-id="ba06b-115">Bu konu, nasıl tooresolve olası sorunlar konusunda yönergeler sorun giderme konusunda sağlar.</span><span class="sxs-lookup"><span data-stu-id="ba06b-115">This topic provides you with troubleshooting guidance on how tooresolve potential issues.</span></span>  

<span data-ttu-id="ba06b-116">**Bilmeniz gerekenler:**</span><span class="sxs-lookup"><span data-stu-id="ba06b-116">**What you should know:**</span></span> 

- <span data-ttu-id="ba06b-117">Hello en fazla kullanıcı başına aygıtları Aygıt odaklı sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="ba06b-117">hello maximum number of devices per user is device-centric.</span></span> <span data-ttu-id="ba06b-118">Örneğin, varsa *jdoe* ve *jharnett* oturum açma tooa aygıt ayrı bir kayıt (DeviceID) Merhaba, bunların her biri için oluşturulduğunda **kullanıcı** bilgileri sekmesi.</span><span class="sxs-lookup"><span data-stu-id="ba06b-118">For example, if *jdoe* and *jharnett* sign-in tooa device, a separate registration (DeviceID) is created for each of them in hello **USER** info tab.</span></span>  

- <span data-ttu-id="ba06b-119">Merhaba ilk kaydı / katılma aygıtların yapılandırılmış tooperform girişiminde oturum açma veya kilitleme veya kilidini.</span><span class="sxs-lookup"><span data-stu-id="ba06b-119">hello initial registration / join of devices is configured tooperform an attempt at either logon or lock / unlock.</span></span> <span data-ttu-id="ba06b-120">Bir Görev Zamanlayıcı görevi tarafından tetiklenen 5 dakikalık gecikme olabilir.</span><span class="sxs-lookup"><span data-stu-id="ba06b-120">There could be 5-minute delay triggered by a task scheduler task.</span></span> 

- <span data-ttu-id="ba06b-121">Merhaba işletim sistemi veya el ile yeniden unregister ve yeniden kaydolun yeni bir kayıt üzerinde Azure AD oluşturup hello kullanıcı bilgileri sekmesi altında birden çok giriş sonuçlarında hello Azure portalı.</span><span class="sxs-lookup"><span data-stu-id="ba06b-121">A reinstall of hello operating system or a manual unregister and re-register may create a new registration on Azure AD and results in multiple entries under hello USER info tab in hello Azure portal.</span></span> 


## <a name="step-1-retrieve-hello-registration-status"></a><span data-ttu-id="ba06b-122">1. adım: hello kayıt durumunu alma</span><span class="sxs-lookup"><span data-stu-id="ba06b-122">Step 1: Retrieve hello registration status</span></span> 

<span data-ttu-id="ba06b-123">**tooverify hello kayıt durumu:**</span><span class="sxs-lookup"><span data-stu-id="ba06b-123">**tooverify hello registration status:**</span></span>  

1. <span data-ttu-id="ba06b-124">Bir yönetici olarak açın hello komut istemi</span><span class="sxs-lookup"><span data-stu-id="ba06b-124">Open hello command prompt as an administrator</span></span> 

2. <span data-ttu-id="ba06b-125">Türü`"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span><span class="sxs-lookup"><span data-stu-id="ba06b-125">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span></span>

<span data-ttu-id="ba06b-126">Bu komut hello birleşim durumu hakkında daha fazla ayrıntı sağlayan bir iletişim kutusu görüntüler.</span><span class="sxs-lookup"><span data-stu-id="ba06b-126">This command displays a dialog box that provides you with more details about hello join status.</span></span>

![Windows için çalışma alanına katılma](./media/active-directory-device-registration-troubleshoot-windows-legacy/01.png)


## <a name="step-2-evaluate-hello-hybrid-azure-ad-join-status"></a><span data-ttu-id="ba06b-128">2. adım: hello karma Azure AD katılım durumunu değerlendirme</span><span class="sxs-lookup"><span data-stu-id="ba06b-128">Step 2: Evaluate hello hybrid Azure AD join status</span></span> 

<span data-ttu-id="ba06b-129">Merhaba karma Azure AD birleştirme başarılı olmadıysa hello iletişim kutusu oluştu hello sorun hakkında ayrıntılar sağlar.</span><span class="sxs-lookup"><span data-stu-id="ba06b-129">If hello hybrid Azure AD join was not successful, hello dialog box provides you with details about hello issue that has occurred.</span></span>

<span data-ttu-id="ba06b-130">**Merhaba en sık karşılaşılan sorunları şunlardır:**</span><span class="sxs-lookup"><span data-stu-id="ba06b-130">**hello most common issues are:**</span></span>

- <span data-ttu-id="ba06b-131">Yanlış yapılandırılmış AD FS veya Azure AD</span><span class="sxs-lookup"><span data-stu-id="ba06b-131">A misconfigured AD FS or Azure AD</span></span>

    ![Windows için çalışma alanına katılma](./media/active-directory-device-registration-troubleshoot-windows-legacy/02.png)

- <span data-ttu-id="ba06b-133">Bir etki alanı kullanıcısı olarak imzalı değil</span><span class="sxs-lookup"><span data-stu-id="ba06b-133">You are not signed on as a domain user</span></span>

    ![Windows için çalışma alanına katılma](./media/active-directory-device-registration-troubleshoot-windows-legacy/03.png)

- <span data-ttu-id="ba06b-135">Bir kotasına ulaşıldı</span><span class="sxs-lookup"><span data-stu-id="ba06b-135">A quota has been reached</span></span>

    ![Windows için çalışma alanına katılma](./media/active-directory-device-registration-troubleshoot-windows-legacy/04.png)

- <span data-ttu-id="ba06b-137">Merhaba hizmeti yanıt vermiyor</span><span class="sxs-lookup"><span data-stu-id="ba06b-137">hello service is not responding</span></span> 

    ![Windows için çalışma alanına katılma](./media/active-directory-device-registration-troubleshoot-windows-legacy/05.png)

<span data-ttu-id="ba06b-139">Merhaba olay günlüğünde altında hello durum bilgisi bulabilirsiniz **uygulamaları ve Hizmetleri Log\Microsoft-çalışma alanına katılma**.</span><span class="sxs-lookup"><span data-stu-id="ba06b-139">You can also find hello status information in hello event log under **Applications and Services Log\Microsoft-Workplace Join**.</span></span>
  
<span data-ttu-id="ba06b-140">**Merhaba başarısız karma Azure AD birleştirme en yaygın nedenleri şunlardır:**</span><span class="sxs-lookup"><span data-stu-id="ba06b-140">**hello most common causes for a failed hybrid Azure AD join are:**</span></span> 

- <span data-ttu-id="ba06b-141">Bilgisayarınız üzerinde değil hello kuruluşunuzun iç ağ ya da bir VPN bağlantısı tooan olmadan şirket içi AD etki alanı denetleyicisi.</span><span class="sxs-lookup"><span data-stu-id="ba06b-141">Your computer is not on hello organization’s internal network or a VPN without connection tooan on-premises AD domain controller.</span></span>

- <span data-ttu-id="ba06b-142">Yerel bilgisayar hesabı olan tooyour bilgisayarında günlüğe kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="ba06b-142">You are logged on tooyour computer with a local computer account.</span></span> 

- <span data-ttu-id="ba06b-143">Hizmet yapılandırma sorunları:</span><span class="sxs-lookup"><span data-stu-id="ba06b-143">Service configuration issues:</span></span> 

  - <span data-ttu-id="ba06b-144">Merhaba Federasyon sunucusu yapılandırılmış toosupport bırakıldı **WIAORMULTIAUTHN**.</span><span class="sxs-lookup"><span data-stu-id="ba06b-144">hello federation server has been configured toosupport **WIAORMULTIAUTHN**.</span></span> 

  - <span data-ttu-id="ba06b-145">Merhaba bilgisayar için ait olduğu hello AD ormanındaki Azure AD'de tooyour doğrulanmış etki alanı adına işaret eden bir hizmet bağlantı noktası nesne yok.</span><span class="sxs-lookup"><span data-stu-id="ba06b-145">There is no Service Connection Point object that points tooyour verified domain name in Azure AD in hello AD forest where hello computer belongs to.</span></span>

  - <span data-ttu-id="ba06b-146">Bir kullanıcı aygıtları hello sınırına ulaştı.</span><span class="sxs-lookup"><span data-stu-id="ba06b-146">A user has reached hello limit of devices.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="ba06b-147">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ba06b-147">Next steps</span></span>

<span data-ttu-id="ba06b-148">Merhaba soruları için bkz [aygıt yönetimi hakkında SSS](device-management-faq.md)</span><span class="sxs-lookup"><span data-stu-id="ba06b-148">For questions, see hello [device management FAQ](device-management-faq.md)</span></span>  
