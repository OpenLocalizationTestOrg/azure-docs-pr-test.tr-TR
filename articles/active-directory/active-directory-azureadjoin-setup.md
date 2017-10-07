---
title: "Kullanıcılarınız için Azure AD'ye katılımı ayarlama aaaSetting | Microsoft Docs"
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
ms.openlocfilehash: 60a5aeb11292cb6057ab1065c3ab77e5981d0cdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-azure-ad-join-in-your-organization"></a><span data-ttu-id="e559b-103">Kuruluşunuzda Azure AD'ye Katılımı ayarlama</span><span class="sxs-lookup"><span data-stu-id="e559b-103">Setting up Azure AD Join in your organization</span></span>
<span data-ttu-id="e559b-104">Azure Active Directory katılımını (Azure AD katılımı) ayarlamadan önce tooeither eşitleme gereksinim yukarı şirket içi dizininize kullanıcılar toohello Bulut veya el ile Azure AD'de yönetilen hesapları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e559b-104">Before you set up Azure Active Directory Join (Azure AD Join), you need tooeither sync up your on-premises directory of users toohello cloud or manually create managed accounts in Azure AD.</span></span>

<span data-ttu-id="e559b-105">Şirket içi kullanıcıların tooAzure AD eşitlemeye için ayrıntılı yönergeler [şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="e559b-105">Detailed instructions for syncing your on-premises users tooAzure AD is covered in [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

<span data-ttu-id="e559b-106">toomanually oluşturmak ve kullanıcıların Azure AD'de yönetmek, çok bakın[Azure AD'de kullanıcı yönetimi](https://msdn.microsoft.com/library/azure/hh967609.aspx).</span><span class="sxs-lookup"><span data-stu-id="e559b-106">toomanually create and manage users in Azure AD, refer too[User management in Azure AD](https://msdn.microsoft.com/library/azure/hh967609.aspx).</span></span>

## <a name="set-up-device-registration"></a><span data-ttu-id="e559b-107">Cihaz kaydı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e559b-107">Set up device registration</span></span>
1. <span data-ttu-id="e559b-108">Toohello üzerinde Azure portal yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="e559b-108">Log on toohello Azure portal as an administrator.</span></span>
2. <span data-ttu-id="e559b-109">Merhaba soldaki bölmede bulunan seçin **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e559b-109">On hello left pane, select **Active Directory**.</span></span>
3. <span data-ttu-id="e559b-110">Merhaba üzerinde **Directory** sekmesinde, dizininizi seçin.</span><span class="sxs-lookup"><span data-stu-id="e559b-110">On hello **Directory** tab, select your directory.</span></span>
4. <span data-ttu-id="e559b-111">Select hello **yapılandırma** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="e559b-111">Select hello **Configure** tab.</span></span>
5. <span data-ttu-id="e559b-112">Toohello Git **aygıtları** bölümü.</span><span class="sxs-lookup"><span data-stu-id="e559b-112">Go toohello **Devices** section.</span></span>
6. <span data-ttu-id="e559b-113">Merhaba üzerinde **aygıtları** sekmesinde, hello aşağıdakileri ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="e559b-113">On hello **devices** tab, set hello following:</span></span>  
   * <span data-ttu-id="e559b-114">**En büyük sayı, CİHAZLARI kullanıcı başına**: hello en fazla bir kullanıcı Azure AD'de sahip cihaz sayısını seçin.</span><span class="sxs-lookup"><span data-stu-id="e559b-114">**MAXIMUM NUMBER OF DEVICES PER USER**: Select hello maximum number of devices that a user can have in Azure AD.</span></span>  <span data-ttu-id="e559b-115">Bir kullanıcı bu kota ulaşırsa, bir veya daha fazla var olan cihazlarının kaldırılana kadar bunlar mümkün tooadd ek cihazlar olmaz.</span><span class="sxs-lookup"><span data-stu-id="e559b-115">If a user reaches this quota, they will not be able tooadd additional devices until one or more of their existing devices are removed.</span></span>
   * <span data-ttu-id="e559b-116">**İSTE MULTİ-FACTOR AUTH tooJOIN AYGITLARI**: kullanıcılar gerekli tooprovide olup ayarlamak ikinci bir kimlik doğrulama faktörü toojoin kendi cihaz tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="e559b-116">**REQUIRE MULTI-FACTOR AUTH tooJOIN DEVICES**: Set whether users are required tooprovide a second authentication factor toojoin their device tooAzure AD.</span></span> <span data-ttu-id="e559b-117">Azure çok faktörlü kimlik doğrulaması hakkında daha fazla bilgi için bkz: [hello bulutta Azure multi Factor Authentication ile çalışmaya başlama](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="e559b-117">For more information on Azure Multi-Factor Authentication, see [Getting started with Azure Multi-Factor Authentication in hello cloud](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span></span>
   * <span data-ttu-id="e559b-118">**USERS MAY AZURE AD birleştirme AYGITLARI**: hello kullanıcılar ve toojoin aygıtları tooAzure AD izin verilen grubu seçin.</span><span class="sxs-lookup"><span data-stu-id="e559b-118">**USERS MAY AZURE AD JOIN DEVICES**: Select hello users and groups that are allowed toojoin devices tooAzure AD.</span></span>
   * <span data-ttu-id="e559b-119">**Ek Yöneticiler ON AZURE AD alanına KATILAN CİHAZLAR**: Azure AD Premium veya Enterprise Mobility Suite (EMS) hello ile hangi kullanıcılara yerel yönetici hakları verilen seçebilirsiniz toohello aygıt.</span><span class="sxs-lookup"><span data-stu-id="e559b-119">**ADDITIONAL ADMINISTRATORS ON AZURE AD JOINED DEVICES**: With Azure AD Premium or hello Enterprise Mobility Suite (EMS), you can choose which users are granted local administrator rights toohello device.</span></span> <span data-ttu-id="e559b-120">Varsayılan olarak genel yöneticilere ve cihaz sahiplerine yerel yönetici hakları verilir.</span><span class="sxs-lookup"><span data-stu-id="e559b-120">Global administrators and device owners are granted local administrator rights by default.</span></span>

<span data-ttu-id="e559b-121"><center>![Cihaz kaydı ayarlama](./media/active-directory-azureadjoin/active-directory-aadjoin-configure-devices.png) </center></span><span class="sxs-lookup"><span data-stu-id="e559b-121"><center>![Set up device regisration](./media/active-directory-azureadjoin/active-directory-aadjoin-configure-devices.png) </center></span></span>

<span data-ttu-id="e559b-122">Kullanıcılarınız için Azure AD'ye katılımı ayarladıktan sonra tooAzure AD aracılığıyla kendi Kurumsal veya kişisel aygıtlar bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="e559b-122">After you set up Azure AD Join for your users, they can connect tooAzure AD through their corporate or personal devices.</span></span>

<span data-ttu-id="e559b-123">Tooenable kullanıcılar tooset Azure AD'ye katılımı kullanabileceğiniz hello üç senaryolar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="e559b-123">Following are hello three scenarios you can use tooenable your users tooset up Azure AD Join:</span></span>

* <span data-ttu-id="e559b-124">Kullanıcıların katılma şirkete ait bir cihazı doğrudan tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="e559b-124">Users join a company-owned device directly tooAzure AD.</span></span>
* <span data-ttu-id="e559b-125">Kullanıcıları etki alanına katılma bir şirketin aygıt toohello şirket içi Active Directory ve hello aygıt tooAzure AD genişletir.</span><span class="sxs-lookup"><span data-stu-id="e559b-125">Users domain-join a company-owned device toohello on-premises Active Directory and then extend hello device tooAzure AD.</span></span>
* <span data-ttu-id="e559b-126">Kullanıcıların iş veya Okul tooWindows kişisel bir cihazda hesapları</span><span class="sxs-lookup"><span data-stu-id="e559b-126">Users add work or school accounts tooWindows on a personal device</span></span>

## <a name="additional-information"></a><span data-ttu-id="e559b-127">Ek bilgiler</span><span class="sxs-lookup"><span data-stu-id="e559b-127">Additional information</span></span>
* [<span data-ttu-id="e559b-128">Merhaba kuruluş için Windows 10: yolları toouse cihazlar iş için</span><span class="sxs-lookup"><span data-stu-id="e559b-128">Windows 10 for hello enterprise: Ways toouse devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="e559b-129">Bulut özellikleri tooWindows 10 cihazların Azure Active Directory katılım aracılığıyla genişletme</span><span class="sxs-lookup"><span data-stu-id="e559b-129">Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="e559b-130">Azure AD Katılımı kullanım senaryoları hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="e559b-130">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="e559b-131">Etki alanına katılmış aygıtlar tooAzure Windows 10 deneyimleri için AD Bağlan</span><span class="sxs-lookup"><span data-stu-id="e559b-131">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="e559b-132">Azure AD'ye Katılım ayarlama</span><span class="sxs-lookup"><span data-stu-id="e559b-132">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

