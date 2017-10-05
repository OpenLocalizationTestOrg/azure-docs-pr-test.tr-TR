---
title: "Birleştirilmiş alt düzey cihazlar Azure Active Directory karma sorunlarını giderme | Microsoft Docs"
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
ms.openlocfilehash: 715fca79e488ae3759926181c244a42026f4a554
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshooting-hybrid-azure-active-directory-joined-down-level-devices"></a><span data-ttu-id="71814-103">Alt düzey aygıtları birleştirilmiş karma Azure Active Directory sorun giderme</span><span class="sxs-lookup"><span data-stu-id="71814-103">Troubleshooting hybrid Azure Active Directory joined down-level devices</span></span> 

<span data-ttu-id="71814-104">Bu konuda, yalnızca aşağıdaki cihazlar için geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="71814-104">This topic is applicable only to the following devices:</span></span> 

- <span data-ttu-id="71814-105">Windows 7</span><span class="sxs-lookup"><span data-stu-id="71814-105">Windows 7</span></span> 
- <span data-ttu-id="71814-106">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="71814-106">Windows 8.1</span></span> 
- <span data-ttu-id="71814-107">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="71814-107">Windows Server 2008 R2</span></span> 
- <span data-ttu-id="71814-108">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="71814-108">Windows Server 2012</span></span> 
- <span data-ttu-id="71814-109">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="71814-109">Windows Server 2012 R2</span></span> 
 

<span data-ttu-id="71814-110">Windows 10 veya Windows Server 2016 için bkz: [sorun giderme karma Azure Active Directory'ye katılmış Windows 10 ve Windows Server 2016 cihazları](device-management-troubleshoot-hybrid-join-windows-current.md).</span><span class="sxs-lookup"><span data-stu-id="71814-110">For Windows 10 or Windows Server 2016, see [Troubleshooting hybrid Azure Active Directory joined Windows 10 and Windows Server 2016 devices](device-management-troubleshoot-hybrid-join-windows-current.md).</span></span>

<span data-ttu-id="71814-111">Bu konu, sahibi olduğunuzu varsayar [yapılandırılmış karma Azure Active Directory'ye katılmış cihazları](device-management-hybrid-azuread-joined-devices-setup.md) aşağıdaki senaryoları desteklemek için:</span><span class="sxs-lookup"><span data-stu-id="71814-111">This topic assumes that you have [configured hybrid Azure Active Directory joined devices](device-management-hybrid-azuread-joined-devices-setup.md) to support the following scenarios:</span></span>

- <span data-ttu-id="71814-112">Cihaz temelli koşullu erişim</span><span class="sxs-lookup"><span data-stu-id="71814-112">Device-based conditional access</span></span>

- [<span data-ttu-id="71814-113">Kurumsal Dolaşım ayarları</span><span class="sxs-lookup"><span data-stu-id="71814-113">Enterprise roaming of settings</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)

- [<span data-ttu-id="71814-114">İş İçin Windows Hello</span><span class="sxs-lookup"><span data-stu-id="71814-114">Windows Hello for Business</span></span>](active-directory-azureadjoin-passport-deployment.md) 





<span data-ttu-id="71814-115">Bu konu, sorun giderme ile ilgili olası sorunları gidermek nasıl yönergelerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="71814-115">This topic provides you with troubleshooting guidance on how to resolve potential issues.</span></span>  

<span data-ttu-id="71814-116">**Bilmeniz gerekenler:**</span><span class="sxs-lookup"><span data-stu-id="71814-116">**What you should know:**</span></span> 

- <span data-ttu-id="71814-117">En fazla kullanıcı başına aygıtları Aygıt odaklı sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="71814-117">The maximum number of devices per user is device-centric.</span></span> <span data-ttu-id="71814-118">Örneğin, varsa *jdoe* ve *jharnett* oturum açma bir cihaza, ayrı bir kayıt (DeviceID) için oluşturulduğunda bunların her birini **kullanıcı** bilgileri sekmesi.</span><span class="sxs-lookup"><span data-stu-id="71814-118">For example, if *jdoe* and *jharnett* sign-in to a device, a separate registration (DeviceID) is created for each of them in the **USER** info tab.</span></span>  

- <span data-ttu-id="71814-119">İlk kaydı / aygıtların birleştirme denemesi oturum açma veya kilidi gerçekleştirmek / kilidini açmak için yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="71814-119">The initial registration / join of devices is configured to perform an attempt at either logon or lock / unlock.</span></span> <span data-ttu-id="71814-120">Bir Görev Zamanlayıcı görevi tarafından tetiklenen 5 dakikalık gecikme olabilir.</span><span class="sxs-lookup"><span data-stu-id="71814-120">There could be 5-minute delay triggered by a task scheduler task.</span></span> 

- <span data-ttu-id="71814-121">İşletim sistemi veya el ile yeniden unregister kaldırıp yeniden kaydettirin oluşturabilir yeni bir kayıt üzerinde Azure AD ve Azure portalında kullanıcı bilgileri sekmesi altında birden çok giriş sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="71814-121">A reinstall of the operating system or a manual unregister and re-register may create a new registration on Azure AD and results in multiple entries under the USER info tab in the Azure portal.</span></span> 


## <a name="step-1-retrieve-the-registration-status"></a><span data-ttu-id="71814-122">1. adım: kayıt durumunu alma</span><span class="sxs-lookup"><span data-stu-id="71814-122">Step 1: Retrieve the registration status</span></span> 

<span data-ttu-id="71814-123">**Kayıt durumunu doğrulamak için:**</span><span class="sxs-lookup"><span data-stu-id="71814-123">**To verify the registration status:**</span></span>  

1. <span data-ttu-id="71814-124">Komut istemini yönetici olarak açın</span><span class="sxs-lookup"><span data-stu-id="71814-124">Open the command prompt as an administrator</span></span> 

2. <span data-ttu-id="71814-125">Türü`"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span><span class="sxs-lookup"><span data-stu-id="71814-125">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span></span>

<span data-ttu-id="71814-126">Bu komut, birleşim durumu hakkında daha fazla ayrıntı sağlayan bir iletişim kutusu görüntüler.</span><span class="sxs-lookup"><span data-stu-id="71814-126">This command displays a dialog box that provides you with more details about the join status.</span></span>

![Windows için çalışma alanına katılma](./media/active-directory-device-registration-troubleshoot-windows-legacy/01.png)


## <a name="step-2-evaluate-the-hybrid-azure-ad-join-status"></a><span data-ttu-id="71814-128">2. adım: Azure AD birleştirme durum karma değerlendirme</span><span class="sxs-lookup"><span data-stu-id="71814-128">Step 2: Evaluate the hybrid Azure AD join status</span></span> 

<span data-ttu-id="71814-129">Karma Azure AD birleştirme başarılı olmadıysa iletişim kutusu oluştu sorun hakkında ayrıntılar sağlar.</span><span class="sxs-lookup"><span data-stu-id="71814-129">If the hybrid Azure AD join was not successful, the dialog box provides you with details about the issue that has occurred.</span></span>

<span data-ttu-id="71814-130">**En yaygın sorunları şunlardır:**</span><span class="sxs-lookup"><span data-stu-id="71814-130">**The most common issues are:**</span></span>

- <span data-ttu-id="71814-131">Yanlış yapılandırılmış AD FS veya Azure AD</span><span class="sxs-lookup"><span data-stu-id="71814-131">A misconfigured AD FS or Azure AD</span></span>

    ![Windows için çalışma alanına katılma](./media/active-directory-device-registration-troubleshoot-windows-legacy/02.png)

- <span data-ttu-id="71814-133">Bir etki alanı kullanıcısı olarak imzalı değil</span><span class="sxs-lookup"><span data-stu-id="71814-133">You are not signed on as a domain user</span></span>

    ![Windows için çalışma alanına katılma](./media/active-directory-device-registration-troubleshoot-windows-legacy/03.png)

- <span data-ttu-id="71814-135">Bir kotasına ulaşıldı</span><span class="sxs-lookup"><span data-stu-id="71814-135">A quota has been reached</span></span>

    ![Windows için çalışma alanına katılma](./media/active-directory-device-registration-troubleshoot-windows-legacy/04.png)

- <span data-ttu-id="71814-137">Hizmeti yanıt vermiyor</span><span class="sxs-lookup"><span data-stu-id="71814-137">The service is not responding</span></span> 

    ![Windows için çalışma alanına katılma](./media/active-directory-device-registration-troubleshoot-windows-legacy/05.png)

<span data-ttu-id="71814-139">Olay günlüğünde altında durum bilgisi bulabilirsiniz **uygulamaları ve Hizmetleri Log\Microsoft-çalışma alanına katılma**.</span><span class="sxs-lookup"><span data-stu-id="71814-139">You can also find the status information in the event log under **Applications and Services Log\Microsoft-Workplace Join**.</span></span>
  
<span data-ttu-id="71814-140">**Başarısız karma Azure AD katılım için en yaygın nedenler şunlardır:**</span><span class="sxs-lookup"><span data-stu-id="71814-140">**The most common causes for a failed hybrid Azure AD join are:**</span></span> 

- <span data-ttu-id="71814-141">Bilgisayarınız bir şirket içi bağlantısı olmadan VPN'yi veya kuruluşunuzun iç ağ üzerinde değil AD etki alanı denetleyicisi.</span><span class="sxs-lookup"><span data-stu-id="71814-141">Your computer is not on the organization’s internal network or a VPN without connection to an on-premises AD domain controller.</span></span>

- <span data-ttu-id="71814-142">Bilgisayarınıza yerel bilgisayar hesabı ile oturum.</span><span class="sxs-lookup"><span data-stu-id="71814-142">You are logged on to your computer with a local computer account.</span></span> 

- <span data-ttu-id="71814-143">Hizmet yapılandırma sorunları:</span><span class="sxs-lookup"><span data-stu-id="71814-143">Service configuration issues:</span></span> 

  - <span data-ttu-id="71814-144">Federasyon sunucusunu desteklemek üzere yapılandırılmış **WIAORMULTIAUTHN**.</span><span class="sxs-lookup"><span data-stu-id="71814-144">The federation server has been configured to support **WIAORMULTIAUTHN**.</span></span> 

  - <span data-ttu-id="71814-145">Bilgisayar için ait olduğu AD ormanında Azure AD'de doğrulanmış etki alanı adınızı işaret eden bir hizmet bağlantı noktası nesne yok.</span><span class="sxs-lookup"><span data-stu-id="71814-145">There is no Service Connection Point object that points to your verified domain name in Azure AD in the AD forest where the computer belongs to.</span></span>

  - <span data-ttu-id="71814-146">Bir kullanıcı cihaz sınırına ulaştı.</span><span class="sxs-lookup"><span data-stu-id="71814-146">A user has reached the limit of devices.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="71814-147">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="71814-147">Next steps</span></span>

<span data-ttu-id="71814-148">Soruları için bkz: [aygıt yönetimi hakkında SSS](device-management-faq.md)</span><span class="sxs-lookup"><span data-stu-id="71814-148">For questions, see the [device management FAQ](device-management-faq.md)</span></span>  
