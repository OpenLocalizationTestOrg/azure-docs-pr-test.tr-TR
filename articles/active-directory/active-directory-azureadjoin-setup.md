---
title: "Kullanıcılarınız için Azure AD'ye Katılımı ayarlama | Microsoft Belgeleri"
description: "Yöneticilerin, şirket içi dizin ve cihaz kaydı için Azure AD Katılımını nasıl ayarlayacakları açıklanmaktadır."
services: active-directory
documentationcenter: 
author: femila
manager: swadhwa
editor: 
tags: azure-classic-portal
ms.assetid: bfc5d415-c918-4d8b-afee-b3f41cc28469
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: c37adc2654f7e931fdda22627e4a6ece2789fd86
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="setting-up-azure-ad-join-in-your-organization"></a><span data-ttu-id="26dc5-103">Kuruluşunuzda Azure AD'ye Katılımı ayarlama</span><span class="sxs-lookup"><span data-stu-id="26dc5-103">Setting up Azure AD Join in your organization</span></span>
<span data-ttu-id="26dc5-104">Azure Active Directory Katılımını (Azure AD Katılımı) ayarlamadan önce kullanıcıların şirket içi dizinini buluta eşitlemeniz veya Azure AD'de yönetilen hesaplar oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="26dc5-104">Before you set up Azure Active Directory Join (Azure AD Join), you need to either sync up your on-premises directory of users to the cloud or manually create managed accounts in Azure AD.</span></span>

<span data-ttu-id="26dc5-105">Şirket içi kullanıcılarınızı Azure AD'ye eşitlemeye ilişkin ayrıntılı yönergeler için bkz. [Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="26dc5-105">Detailed instructions for syncing your on-premises users to Azure AD is covered in [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

<span data-ttu-id="26dc5-106">Azure AD'de el ile kullanıcı oluşturmak ve yönetmek için bkz. [Azure AD'de kullanıcı yönetimi](https://msdn.microsoft.com/library/azure/hh967609.aspx).</span><span class="sxs-lookup"><span data-stu-id="26dc5-106">To manually create and manage users in Azure AD, refer to [User management in Azure AD](https://msdn.microsoft.com/library/azure/hh967609.aspx).</span></span>

## <a name="set-up-device-registration"></a><span data-ttu-id="26dc5-107">Cihaz kaydı oluşturma</span><span class="sxs-lookup"><span data-stu-id="26dc5-107">Set up device registration</span></span>
1. <span data-ttu-id="26dc5-108">Azure portalında yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="26dc5-108">Log on to the Azure portal as an administrator.</span></span>
2. <span data-ttu-id="26dc5-109">Sol bölmede **Active Directory**'yi seçin.</span><span class="sxs-lookup"><span data-stu-id="26dc5-109">On the left pane, select **Active Directory**.</span></span>
3. <span data-ttu-id="26dc5-110">**Directory (Dizin)** sekmesinde dizininizi seçin.</span><span class="sxs-lookup"><span data-stu-id="26dc5-110">On the **Directory** tab, select your directory.</span></span>
4. <span data-ttu-id="26dc5-111">**Configure (Yapılandır)** sekmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="26dc5-111">Select the **Configure** tab.</span></span>
5. <span data-ttu-id="26dc5-112">**Devices (Cihazlar)** bölümüne gidin.</span><span class="sxs-lookup"><span data-stu-id="26dc5-112">Go to the **Devices** section.</span></span>
6. <span data-ttu-id="26dc5-113">**Devices (Cihazlar)** sekmesinde şunları ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="26dc5-113">On the **devices** tab, set the following:</span></span>  
   * <span data-ttu-id="26dc5-114">**MAXIMUM NUMBER OF DEVICES PER USER (KULLANICI BAŞINA MAKSİMUM CİHAZ SAYISI)**: Kullanıcıların Azure AD'de sahip olabileceği maksimum cihaz sayısını belirleyin.</span><span class="sxs-lookup"><span data-stu-id="26dc5-114">**MAXIMUM NUMBER OF DEVICES PER USER**: Select the maximum number of devices that a user can have in Azure AD.</span></span>  <span data-ttu-id="26dc5-115">Bu kotayı dolduran bir kullanıcı, var olan cihazlarının bir veya birden fazlasını kaldırmadan yeni cihaz ekleyemez.</span><span class="sxs-lookup"><span data-stu-id="26dc5-115">If a user reaches this quota, they will not be able to add additional devices until one or more of their existing devices are removed.</span></span>
   * <span data-ttu-id="26dc5-116">**REQUIRE MULTI-FACTOR AUTH TO JOIN DEVICES (CİHAZLARIN KATILIMI İÇİN MULTI-FACTOR AUTHENTICATION'I GEREKLİ KIL)**: Kullanıcıların cihazlarını Azure AD'ye eklemeleri için ikinci bir kimlik doğrulama faktörü sağlamalarının gerekip gerekmediğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="26dc5-116">**REQUIRE MULTI-FACTOR AUTH TO JOIN DEVICES**: Set whether users are required to provide a second authentication factor to join their device to Azure AD.</span></span> <span data-ttu-id="26dc5-117">Azure Multi-Factor Authentication hakkında daha fazla bilgi edinmek için bkz. [Bulutta Azure Multi-Factor Authentication ile çalışmaya başlama](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="26dc5-117">For more information on Azure Multi-Factor Authentication, see [Getting started with Azure Multi-Factor Authentication in the cloud](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span></span>
   * <span data-ttu-id="26dc5-118">**USERS MAY AZURE AD JOIN DEVICES (KULLANICILAR AZURE AD'YE CİHAZ KATABİLİR)**: Cihazlarını Azure AD'ye ekleme izni olan kullanıcıları ve grupları seçin.</span><span class="sxs-lookup"><span data-stu-id="26dc5-118">**USERS MAY AZURE AD JOIN DEVICES**: Select the users and groups that are allowed to join devices to Azure AD.</span></span>
   * <span data-ttu-id="26dc5-119">**ADDITIONAL ADMINISTRATORS ON AZURE AD JOINED DEVICES (AZURE AD'YE KATILAN CİHAZLAR İÇİN EK YÖNETİCİLER)**: Azure AD Premium veya Enterprise Mobility Suite (EMS) ile hangi kullanıcılara cihaz için yerel yönetici haklarının verileceğini belirleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="26dc5-119">**ADDITIONAL ADMINISTRATORS ON AZURE AD JOINED DEVICES**: With Azure AD Premium or the Enterprise Mobility Suite (EMS), you can choose which users are granted local administrator rights to the device.</span></span> <span data-ttu-id="26dc5-120">Varsayılan olarak genel yöneticilere ve cihaz sahiplerine yerel yönetici hakları verilir.</span><span class="sxs-lookup"><span data-stu-id="26dc5-120">Global administrators and device owners are granted local administrator rights by default.</span></span>

<span data-ttu-id="26dc5-121"><center>![Cihaz kaydı ayarlama](./media/active-directory-azureadjoin/active-directory-aadjoin-configure-devices.png) </center></span><span class="sxs-lookup"><span data-stu-id="26dc5-121"><center>![Set up device regisration](./media/active-directory-azureadjoin/active-directory-aadjoin-configure-devices.png) </center></span></span>

<span data-ttu-id="26dc5-122">Kullanıcılarınız için Azure AD'ye Katılımı ayarladığınızda kurumsal veya kişisel cihazları üzerinden Azure AD'ye bağlanabilirler.</span><span class="sxs-lookup"><span data-stu-id="26dc5-122">After you set up Azure AD Join for your users, they can connect to Azure AD through their corporate or personal devices.</span></span>

<span data-ttu-id="26dc5-123">Kullanıcılarınızın Azure AD Katılımını ayarlamalarını sağlamak üzere şu üç senaryoyu kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="26dc5-123">Following are the three scenarios you can use to enable your users to set up Azure AD Join:</span></span>

* <span data-ttu-id="26dc5-124">Kullanıcılar, şirketlerine ait cihazları doğrudan Azure AD'ye ekler.</span><span class="sxs-lookup"><span data-stu-id="26dc5-124">Users join a company-owned device directly to Azure AD.</span></span>
* <span data-ttu-id="26dc5-125">Kullanıcılar, şirketlerine ait bir cihazı şirket içi Active Directory'deki etki alanına ekler ve ardından cihazı Azure AD'ye genişletir.</span><span class="sxs-lookup"><span data-stu-id="26dc5-125">Users domain-join a company-owned device to the on-premises Active Directory and then extend the device to Azure AD.</span></span>
* <span data-ttu-id="26dc5-126">Kullanıcılar, kişisel bir cihazdan Windows'a iş veya okul hesabı ekler.</span><span class="sxs-lookup"><span data-stu-id="26dc5-126">Users add work or school accounts to Windows on a personal device</span></span>

## <a name="additional-information"></a><span data-ttu-id="26dc5-127">Ek bilgiler</span><span class="sxs-lookup"><span data-stu-id="26dc5-127">Additional information</span></span>
* [<span data-ttu-id="26dc5-128">Kurumlar için Windows 10: Cihazları iş için kullanmanın yolları</span><span class="sxs-lookup"><span data-stu-id="26dc5-128">Windows 10 for the enterprise: Ways to use devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="26dc5-129">Azure Active Directory Join ile bulut işlevlerini Windows 10 cihazlarına genişletme</span><span class="sxs-lookup"><span data-stu-id="26dc5-129">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="26dc5-130">Azure AD Katılımı kullanım senaryoları hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="26dc5-130">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="26dc5-131">Windows 10 deneyiminden faydalanmak için etki alanına katılan cihazları Azure AD'ye bağlama</span><span class="sxs-lookup"><span data-stu-id="26dc5-131">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="26dc5-132">Azure AD'ye Katılım ayarlama</span><span class="sxs-lookup"><span data-stu-id="26dc5-132">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

