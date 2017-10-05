---
title: "Kurulum sırasında Azure AD ile yeni bir cihaz ayarlama | Microsoft Docs"
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
ms.openlocfilehash: 4367f453ef7c794653dfa9f305b137a168e0d207
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="set-up-a-new-device-with-azure-ad-during-setup"></a><span data-ttu-id="8f4c2-103">Kurulum sırasında Azure AD ile yeni bir cihaz ayarlama</span><span class="sxs-lookup"><span data-stu-id="8f4c2-103">Set up a new device with Azure AD during Setup</span></span>
<span data-ttu-id="8f4c2-104">Windows 10'da, kullanıcıların cihazlarını Azure Active Directory (Azure AD) ilk çalıştırma deneyimi (FRX) birleştirebilirler.</span><span class="sxs-lookup"><span data-stu-id="8f4c2-104">In Windows 10, users can join their devices to Azure Active Directory (Azure AD) in the first-run experience (FRX).</span></span> <span data-ttu-id="8f4c2-105">Bu, kuruluşların kendi çalışanlar veya Öğrenciler naylon cihazlara dağıtmak veya kendi aygıt (CYOD) seçmesini sağlayan olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="8f4c2-105">This allows organizations to distribute shrink-wrapped devices to their employees or students, or let them choose their own devices (CYOD).</span></span>
<span data-ttu-id="8f4c2-106">Windows 10 Professional veya Windows 10 Enterprise Edition bir cihaz üzerinde yüklüyse, deneyimi Kurulum işlemi şirkete ait cihazlar için varsayılan olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="8f4c2-106">If either Windows 10 Professional or Windows 10 Enterprise editions is installed on a device, the experience defaults to the setup process for company-owned devices.</span></span>

## <a name="to-join-a-device-to-azure-ad"></a><span data-ttu-id="8f4c2-107">Bir aygıt için Azure AD katılmak için</span><span class="sxs-lookup"><span data-stu-id="8f4c2-107">To join a device to Azure AD</span></span>
1. <span data-ttu-id="8f4c2-108">Yeni aygıtınızı açın ve kurulum işlemini başlatamazsa, görmelisiniz **alma hazır** ileti.</span><span class="sxs-lookup"><span data-stu-id="8f4c2-108">When you turn on your new device and start the setup process, you should see the  **Getting Ready** message.</span></span> <span data-ttu-id="8f4c2-109">Cihazınızı ayarlamak için istemleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="8f4c2-109">Follow the prompts to set up your device.</span></span>
2. <span data-ttu-id="8f4c2-110">Bölge ve dil özelleştirerek başlatın.</span><span class="sxs-lookup"><span data-stu-id="8f4c2-110">Start by customizing your region and language.</span></span> <span data-ttu-id="8f4c2-111">Ardından, Microsoft Yazılımı Lisans koşulları kabul edin.</span><span class="sxs-lookup"><span data-stu-id="8f4c2-111">Then accept the Microsoft Software License Terms.</span></span>
   <span data-ttu-id="8f4c2-112">![Bölgeniz için özelleştirme](./media/active-directory-azureadjoin/active-directory-azureadjoin-customize-region.png)</span><span class="sxs-lookup"><span data-stu-id="8f4c2-112">![Customize for your region](./media/active-directory-azureadjoin/active-directory-azureadjoin-customize-region.png)</span></span>
3. <span data-ttu-id="8f4c2-113">Internet'e bağlanmak için kullanmak istediğiniz ağı seçin.</span><span class="sxs-lookup"><span data-stu-id="8f4c2-113">Select the network you want to use for connecting to the Internet.</span></span>
4. <span data-ttu-id="8f4c2-114">Kişisel bir cihazı veya şirkete ait bir cihazı kullanıyorsanız olup olmadığını seçin.</span><span class="sxs-lookup"><span data-stu-id="8f4c2-114">Select whether you're using a personal device or a company-owned device.</span></span> <span data-ttu-id="8f4c2-115">Şirkete ait ise, tıklatın **bu cihaz kuruluşuma ait**.</span><span class="sxs-lookup"><span data-stu-id="8f4c2-115">If it's company-owned, click **This device belongs to my organization**.</span></span> <span data-ttu-id="8f4c2-116">Bu, Azure AD katılım deneyimi başlatır.</span><span class="sxs-lookup"><span data-stu-id="8f4c2-116">This starts the Azure AD Join experience.</span></span> <span data-ttu-id="8f4c2-117">Aşağıdaki Windows 10 Professional kullanıyorsanız görürsünüz bir ekrandır.</span><span class="sxs-lookup"><span data-stu-id="8f4c2-117">Following is a screen that you'll see if you're using Windows 10 Professional.</span></span>
   <span data-ttu-id="8f4c2-118"><center>
   ![Bu bilgisayar ekran Kime ait](./media/active-directory-azureadjoin/active-directory-azureadjoin-who-owns-pc.png)</span><span class="sxs-lookup"><span data-stu-id="8f4c2-118"><center>
![Who owns this PC screen](./media/active-directory-azureadjoin/active-directory-azureadjoin-who-owns-pc.png)</span></span>
5. <span data-ttu-id="8f4c2-119">Kuruluşunuz tarafından size sağlanan kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="8f4c2-119">Enter the credentials that were provided to you by your organization.</span></span>
   <span data-ttu-id="8f4c2-120"><center>
   ![Oturum açma ekranı](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png)</span><span class="sxs-lookup"><span data-stu-id="8f4c2-120"><center>
![Sign-in screen](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png)</span></span>
6. <span data-ttu-id="8f4c2-121">Eşleşen bir kiracı, kullanıcı adınızı girdikten sonra Azure AD içinde yer alır.</span><span class="sxs-lookup"><span data-stu-id="8f4c2-121">After you have entered your user name, a matching tenant is located in Azure AD.</span></span> <span data-ttu-id="8f4c2-122">Federe bir etki alanındaysa, şirket içi güvenli belirteç hizmeti (STS) sunucunuza--Örneğin, Active Directory Federasyon Hizmetleri (AD FS) yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="8f4c2-122">If you are in a federated domain, you will be redirected to your on-premises Secure Token Service (STS) server--for example, Active Directory Federation Services (AD FS).</span></span>
7. <span data-ttu-id="8f4c2-123">Federasyon olmayan bir etki alanındaki bir kullanıcı varsa, doğrudan Azure AD tarafından barındırılan sayfasında kimlik bilgilerinizi girin.</span><span class="sxs-lookup"><span data-stu-id="8f4c2-123">If you are a user in a non-federated domain, enter your credentials directly on the Azure AD-hosted page.</span></span> <span data-ttu-id="8f4c2-124">Şirket markası yapılandırdıysanız, aynı zamanda, kuruluşunuzun logosu görebilir ve metin desteği.</span><span class="sxs-lookup"><span data-stu-id="8f4c2-124">If company branding was configured, you will also see your organization’s logo and support text.</span></span>
8. <span data-ttu-id="8f4c2-125">Çok faktörlü kimlik doğrulaması sınaması için istenir.</span><span class="sxs-lookup"><span data-stu-id="8f4c2-125">You're prompted for a multi-factor authentication challenge.</span></span> <span data-ttu-id="8f4c2-126">Bu sorunu BT yöneticisi tarafından yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="8f4c2-126">This challenge is configurable by an IT administrator.</span></span>
9. <span data-ttu-id="8f4c2-127">Azure AD, bu kullanıcı/cihaz kaydı mobil cihaz Yönetimi'nde gerekli olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="8f4c2-127">Azure AD checks whether this user/device requires enrollment in mobile device management.</span></span>
10. <span data-ttu-id="8f4c2-128">Windows Azure AD'de kuruluşunuzun dizininde cihazı kaydeder ve uygun durumlarda mobil cihaz Yönetimi'nde kaydeder.</span><span class="sxs-lookup"><span data-stu-id="8f4c2-128">Windows registers the device in the organization’s directory in Azure AD and enrolls it in mobile device management, if appropriate.</span></span>
11. <span data-ttu-id="8f4c2-129">Yönetilen bir kullanıcı varsa, Windows, Masaüstü otomatik oturum açma işlemi aracılığıyla alır.</span><span class="sxs-lookup"><span data-stu-id="8f4c2-129">If you are a managed user, Windows takes you to the desktop through the automatic sign-in process.</span></span>
12. <span data-ttu-id="8f4c2-130">Bir Federasyon kullanıcısı varsa, kimlik bilgilerinizi girmeniz için Windows oturum açma ekranı yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="8f4c2-130">If you are a federated user, you are directed to the Windows sign-in screen to enter your credentials.</span></span>

> [!NOTE]
> <span data-ttu-id="8f4c2-131">Windows out-of-box deneyiminde bir şirket içi Windows Server Active Directory etki alanına katılma desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="8f4c2-131">Joining an on-premises Windows Server Active Directory domain in the Windows out-of-box experience is not supported.</span></span> <span data-ttu-id="8f4c2-132">Bu nedenle, bir bilgisayarı bir etki alanına planlıyorsanız, bağlantıyı seçmelisiniz **Windows'u yerel hesapla ayarlamak** yerine.</span><span class="sxs-lookup"><span data-stu-id="8f4c2-132">Therefore, if you plan to join a computer to a domain, you should select the link **Set up Windows with a local account** instead.</span></span> <span data-ttu-id="8f4c2-133">Önce uyguladığınız gibi etki alanı ayarlarından sonra bilgisayarınızda birleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8f4c2-133">You can then join the domain from the settings on your computer as you’ve done before.</span></span>
> 
> 

## <a name="additional-information"></a><span data-ttu-id="8f4c2-134">Ek bilgiler</span><span class="sxs-lookup"><span data-stu-id="8f4c2-134">Additional information</span></span>
* [<span data-ttu-id="8f4c2-135">Kurumlar için Windows 10: Cihazları iş için kullanmanın yolları</span><span class="sxs-lookup"><span data-stu-id="8f4c2-135">Windows 10 for the enterprise: Ways to use devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="8f4c2-136">Azure Active Directory Join ile bulut işlevlerini Windows 10 cihazlarına genişletme</span><span class="sxs-lookup"><span data-stu-id="8f4c2-136">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="8f4c2-137">Microsoft Passport aracılığıyla parolası olmayan kimlikleri doğrulama</span><span class="sxs-lookup"><span data-stu-id="8f4c2-137">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)
* [<span data-ttu-id="8f4c2-138">Azure AD Katılımı kullanım senaryoları hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="8f4c2-138">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="8f4c2-139">Windows 10 deneyiminden faydalanmak için etki alanına katılan cihazları Azure AD'ye bağlama</span><span class="sxs-lookup"><span data-stu-id="8f4c2-139">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="8f4c2-140">Azure AD'ye Katılım ayarlama</span><span class="sxs-lookup"><span data-stu-id="8f4c2-140">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

