---
title: "Kurulum sırasında Azure AD ile yeni bir cihaz ayarlama aaaSet | Microsoft Docs"
description: "Nasıl kullanıcıları Azure AD'ye katılımı kendi ilk çalıştırma deneyimi sırasında ayarlayabilirsiniz açıklayan bir konu."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 06a149f7-4aa1-4fb9-a8ec-ac2633b031fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 6afce4be7f084f1956a6f9dbddaa8def0605956d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-new-device-with-azure-ad-during-setup"></a><span data-ttu-id="d0a2c-103">Kurulum sırasında Azure AD ile yeni bir cihaz ayarlama</span><span class="sxs-lookup"><span data-stu-id="d0a2c-103">Set up a new device with Azure AD during Setup</span></span>
<span data-ttu-id="d0a2c-104">Windows 10'da, kullanıcıların kendi aygıtlarını tooAzure Active Directory (Azure AD) hello ilk çalıştırma deneyimi (FRX) birleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0a2c-104">In Windows 10, users can join their devices tooAzure Active Directory (Azure AD) in hello first-run experience (FRX).</span></span> <span data-ttu-id="d0a2c-105">Bu kuruluşların toodistribute naylon aygıtları tootheir çalışanlar veya Öğrenciler izin verir veya kendi aygıt (CYOD) seçmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="d0a2c-105">This allows organizations toodistribute shrink-wrapped devices tootheir employees or students, or let them choose their own devices (CYOD).</span></span>
<span data-ttu-id="d0a2c-106">Windows 10 Professional veya Windows 10 Enterprise Edition bir cihaz üzerinde yüklüyse, hello şirkete ait cihazlar için varsayılan toohello Kurulum işlemi karşılaşırsınız.</span><span class="sxs-lookup"><span data-stu-id="d0a2c-106">If either Windows 10 Professional or Windows 10 Enterprise editions is installed on a device, hello experience defaults toohello setup process for company-owned devices.</span></span>

## <a name="toojoin-a-device-tooazure-ad"></a><span data-ttu-id="d0a2c-107">toojoin aygıt tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="d0a2c-107">toojoin a device tooAzure AD</span></span>
1. <span data-ttu-id="d0a2c-108">Yeni aygıtınızı açın ve hello Kurulum işlemini başlatamazsa, hello görmelisiniz **alma hazır** ileti.</span><span class="sxs-lookup"><span data-stu-id="d0a2c-108">When you turn on your new device and start hello setup process, you should see hello  **Getting Ready** message.</span></span> <span data-ttu-id="d0a2c-109">Cihazınızı yukarı Hello istemleri tooset izleyin.</span><span class="sxs-lookup"><span data-stu-id="d0a2c-109">Follow hello prompts tooset up your device.</span></span>
2. <span data-ttu-id="d0a2c-110">Bölge ve dil özelleştirerek başlatın.</span><span class="sxs-lookup"><span data-stu-id="d0a2c-110">Start by customizing your region and language.</span></span> <span data-ttu-id="d0a2c-111">Ardından hello Microsoft Yazılımı Lisans koşulları kabul edin.</span><span class="sxs-lookup"><span data-stu-id="d0a2c-111">Then accept hello Microsoft Software License Terms.</span></span>
   <span data-ttu-id="d0a2c-112">![Bölgeniz için özelleştirme](./media/active-directory-azureadjoin/active-directory-azureadjoin-customize-region.png)</span><span class="sxs-lookup"><span data-stu-id="d0a2c-112">![Customize for your region](./media/active-directory-azureadjoin/active-directory-azureadjoin-customize-region.png)</span></span>
3. <span data-ttu-id="d0a2c-113">Toouse toohello Internet bağlanmak için hello ağı seçin.</span><span class="sxs-lookup"><span data-stu-id="d0a2c-113">Select hello network you want toouse for connecting toohello Internet.</span></span>
4. <span data-ttu-id="d0a2c-114">Kişisel bir cihazı veya şirkete ait bir cihazı kullanıyorsanız olup olmadığını seçin.</span><span class="sxs-lookup"><span data-stu-id="d0a2c-114">Select whether you're using a personal device or a company-owned device.</span></span> <span data-ttu-id="d0a2c-115">Şirkete ait ise, tıklatın **toomy kuruluş bu cihaz ait**.</span><span class="sxs-lookup"><span data-stu-id="d0a2c-115">If it's company-owned, click **This device belongs toomy organization**.</span></span> <span data-ttu-id="d0a2c-116">Bu hello Azure AD katılım deneyimi başlatır.</span><span class="sxs-lookup"><span data-stu-id="d0a2c-116">This starts hello Azure AD Join experience.</span></span> <span data-ttu-id="d0a2c-117">Aşağıdaki Windows 10 Professional kullanıyorsanız görürsünüz bir ekrandır.</span><span class="sxs-lookup"><span data-stu-id="d0a2c-117">Following is a screen that you'll see if you're using Windows 10 Professional.</span></span>
   <span data-ttu-id="d0a2c-118"><center>
   ![Bu bilgisayar ekran Kime ait](./media/active-directory-azureadjoin/active-directory-azureadjoin-who-owns-pc.png)</span><span class="sxs-lookup"><span data-stu-id="d0a2c-118"><center>
![Who owns this PC screen](./media/active-directory-azureadjoin/active-directory-azureadjoin-who-owns-pc.png)</span></span>
5. <span data-ttu-id="d0a2c-119">Tooyou kuruluşunuz tarafından sağlanan hello kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="d0a2c-119">Enter hello credentials that were provided tooyou by your organization.</span></span>
   <span data-ttu-id="d0a2c-120"><center>
   ![Oturum açma ekranı](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png)</span><span class="sxs-lookup"><span data-stu-id="d0a2c-120"><center>
![Sign-in screen](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png)</span></span>
6. <span data-ttu-id="d0a2c-121">Eşleşen bir kiracı, kullanıcı adınızı girdikten sonra Azure AD içinde yer alır.</span><span class="sxs-lookup"><span data-stu-id="d0a2c-121">After you have entered your user name, a matching tenant is located in Azure AD.</span></span> <span data-ttu-id="d0a2c-122">Federe bir etki alanındaysa, yeniden yönlendirilen tooyour şirket içi güvenli belirteç hizmeti (STS) sunucu--Örneğin, Active Directory Federasyon Hizmetleri (AD FS) olacaktır.</span><span class="sxs-lookup"><span data-stu-id="d0a2c-122">If you are in a federated domain, you will be redirected tooyour on-premises Secure Token Service (STS) server--for example, Active Directory Federation Services (AD FS).</span></span>
7. <span data-ttu-id="d0a2c-123">Federasyon olmayan bir etki alanındaki bir kullanıcı varsa, doğrudan hello üzerinde Azure AD tarafından barındırılan sayfasında kimlik bilgilerinizi girin.</span><span class="sxs-lookup"><span data-stu-id="d0a2c-123">If you are a user in a non-federated domain, enter your credentials directly on hello Azure AD-hosted page.</span></span> <span data-ttu-id="d0a2c-124">Şirket markası yapılandırdıysanız, aynı zamanda, kuruluşunuzun logosu görebilir ve metin desteği.</span><span class="sxs-lookup"><span data-stu-id="d0a2c-124">If company branding was configured, you will also see your organization’s logo and support text.</span></span>
8. <span data-ttu-id="d0a2c-125">Çok faktörlü kimlik doğrulaması sınaması için istenir.</span><span class="sxs-lookup"><span data-stu-id="d0a2c-125">You're prompted for a multi-factor authentication challenge.</span></span> <span data-ttu-id="d0a2c-126">Bu sorunu BT yöneticisi tarafından yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="d0a2c-126">This challenge is configurable by an IT administrator.</span></span>
9. <span data-ttu-id="d0a2c-127">Azure AD, bu kullanıcı/cihaz kaydı mobil cihaz Yönetimi'nde gerekli olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="d0a2c-127">Azure AD checks whether this user/device requires enrollment in mobile device management.</span></span>
10. <span data-ttu-id="d0a2c-128">Windows hello aygıt hello kuruluşunuzun dizininde Azure AD'de kaydeder ve uygun durumlarda mobil cihaz Yönetimi'nde kaydeder.</span><span class="sxs-lookup"><span data-stu-id="d0a2c-128">Windows registers hello device in hello organization’s directory in Azure AD and enrolls it in mobile device management, if appropriate.</span></span>
11. <span data-ttu-id="d0a2c-129">Yönetilen bir kullanıcı varsa, Windows hello otomatik oturum açma işlemi aracılığıyla toohello masaüstüne alır.</span><span class="sxs-lookup"><span data-stu-id="d0a2c-129">If you are a managed user, Windows takes you toohello desktop through hello automatic sign-in process.</span></span>
12. <span data-ttu-id="d0a2c-130">Bir Federasyon kullanıcısı varsa, yönlendirilmiş toohello Windows oturum açma kimlik bilgilerinizi tooenter ekran.</span><span class="sxs-lookup"><span data-stu-id="d0a2c-130">If you are a federated user, you are directed toohello Windows sign-in screen tooenter your credentials.</span></span>

> [!NOTE]
> <span data-ttu-id="d0a2c-131">Merhaba Windows bir şirket içi Windows Server Active Directory etki alanına katılma out-of-box deneyimi desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="d0a2c-131">Joining an on-premises Windows Server Active Directory domain in hello Windows out-of-box experience is not supported.</span></span> <span data-ttu-id="d0a2c-132">Toojoin bilgisayar tooa etki alanı planlıyorsanız, bu nedenle, hello bağlantı seçmelisiniz **Windows'u yerel hesapla ayarlamak** yerine.</span><span class="sxs-lookup"><span data-stu-id="d0a2c-132">Therefore, if you plan toojoin a computer tooa domain, you should select hello link **Set up Windows with a local account** instead.</span></span> <span data-ttu-id="d0a2c-133">Önce uyguladığınız gibi bilgisayarınızda hello etki alanından hello ayarları sonra birleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0a2c-133">You can then join hello domain from hello settings on your computer as you’ve done before.</span></span>
> 
> 

## <a name="additional-information"></a><span data-ttu-id="d0a2c-134">Ek bilgiler</span><span class="sxs-lookup"><span data-stu-id="d0a2c-134">Additional information</span></span>
* [<span data-ttu-id="d0a2c-135">Merhaba kuruluş için Windows 10: yolları toouse cihazlar iş için</span><span class="sxs-lookup"><span data-stu-id="d0a2c-135">Windows 10 for hello enterprise: Ways toouse devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="d0a2c-136">Bulut özellikleri tooWindows 10 cihazların Azure Active Directory katılım aracılığıyla genişletme</span><span class="sxs-lookup"><span data-stu-id="d0a2c-136">Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="d0a2c-137">Microsoft Passport aracılığıyla parolası olmayan kimlikleri doğrulama</span><span class="sxs-lookup"><span data-stu-id="d0a2c-137">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)
* [<span data-ttu-id="d0a2c-138">Azure AD Katılımı kullanım senaryoları hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="d0a2c-138">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="d0a2c-139">Etki alanına katılmış aygıtlar tooAzure Windows 10 deneyimleri için AD Bağlan</span><span class="sxs-lookup"><span data-stu-id="d0a2c-139">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="d0a2c-140">Azure AD'ye Katılım ayarlama</span><span class="sxs-lookup"><span data-stu-id="d0a2c-140">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

