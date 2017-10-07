---
title: "Windows 10 için aaaConnect etki alanına katılmış aygıtlar tooAzure AD karşılaştığında | Microsoft Docs"
description: "Yöneticiler Grup İlkesi tooenable aygıtları toobe etki alanına katılmış toohello kuruluş ağı nasıl yapılandırabileceğiniz açıklanmaktadır."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 2ff29f3e-5325-4f43-9baa-6ae8d6bad3e3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 9766aa702352dea2ecad3a9a0bdf8d3286ee6d91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-domain-joined-devices-tooazure-ad-for-windows-10-experiences"></a><span data-ttu-id="0dfbd-103">Etki alanına katılmış aygıtlar tooAzure Windows 10 deneyimleri için AD Bağlan</span><span class="sxs-lookup"><span data-stu-id="0dfbd-103">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>
<span data-ttu-id="0dfbd-104">Etki alanına katılma hello geleneksel şekilde kuruluşlar iş hello son 15 yıl ve daha fazlası için Aygıtlar bağlı olur.</span><span class="sxs-lookup"><span data-stu-id="0dfbd-104">Domain join is hello traditional way organizations have connected devices for work for hello last 15 years and more.</span></span> <span data-ttu-id="0dfbd-105">Kullanıcıların toosign tootheir aygıtları, Windows Server Active Directory (Active Directory) işlerini kullanarak etkinleştirilmiş veya Okul hesapları ve izin verilen BT toofully bu aygıtları yönetin.</span><span class="sxs-lookup"><span data-stu-id="0dfbd-105">It has enabled users toosign in tootheir devices by using their Windows Server Active Directory (Active Directory) work or school accounts and allowed IT toofully manage these devices.</span></span> <span data-ttu-id="0dfbd-106">Kuruluşlar genellikle yöntemleri tooprovision aygıtları toousers Imaging kullanır ve genellikle Grup İlkesi veya System Center Configuration Manager (SCCM) toomanage kullanması bunları.</span><span class="sxs-lookup"><span data-stu-id="0dfbd-106">Organizations typically rely on imaging methods tooprovision devices toousers and generally use System Center Configuration Manager (SCCM) or Group Policy toomanage them.</span></span>


<span data-ttu-id="0dfbd-107">Windows 10 etki alanına katılma ile Merhaba aygıtları tooAzure Active Directory (Azure AD) bağlandıktan sonra aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="0dfbd-107">Domain join in Windows 10 provides you with hello following benefits after you connect devices tooAzure Active Directory (Azure AD):</span></span>

* <span data-ttu-id="0dfbd-108">Çoklu oturum açma (SSO) tooAzure AD kaynaklara her yerden</span><span class="sxs-lookup"><span data-stu-id="0dfbd-108">Single sign-on (SSO) tooAzure AD resources from anywhere</span></span>
* <span data-ttu-id="0dfbd-109">İş kullanarak toohello enterprise Windows mağazası erişmek veya Okul hesapları (Microsoft hesabı gereklidir)</span><span class="sxs-lookup"><span data-stu-id="0dfbd-109">Access toohello enterprise Windows Store by using work or school accounts (no Microsoft account required)</span></span>
* <span data-ttu-id="0dfbd-110">Kurumsal uyumlu kullanıcı cihaz üzerinden iş veya Okul hesapları (Microsoft hesabı gereklidir) kullanarak Dolaşım ayarları</span><span class="sxs-lookup"><span data-stu-id="0dfbd-110">Enterprise-compliant roaming of user settings across devices by using work or school accounts (no Microsoft account required)</span></span>
* <span data-ttu-id="0dfbd-111">Güçlü kimlik doğrulaması ve güvenli oturum açma için iş veya Okul hesaplarıyla iş için Windows Hello ve Windows Hello</span><span class="sxs-lookup"><span data-stu-id="0dfbd-111">Strong authentication and convenient sign-in for work or school accounts with Windows Hello for Business and Windows Hello</span></span>
* <span data-ttu-id="0dfbd-112">Özelliği toorestrict kuruluş aygıt Grup İlkesi ayarları ile uyumlu toodevices erişim</span><span class="sxs-lookup"><span data-stu-id="0dfbd-112">Ability toorestrict access only toodevices that comply with organizational device Group Policy settings</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0dfbd-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="0dfbd-113">Prerequisites</span></span>
<span data-ttu-id="0dfbd-114">Etki alanına katılma toobe yararlı devam eder.</span><span class="sxs-lookup"><span data-stu-id="0dfbd-114">Domain join continues toobe useful.</span></span> <span data-ttu-id="0dfbd-115">Ancak, hello Azure AD yararları SSO tooget, ayarlarla, gezici iş veya Okul hesapları ve çalışmak tooWindows deposuna erişim veya Okul hesapları, aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="0dfbd-115">However, tooget hello Azure AD benefits of SSO, roaming of settings with work or school accounts, and access tooWindows Store with work or school accounts, you will need hello following:</span></span>

* <span data-ttu-id="0dfbd-116">Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="0dfbd-116">Azure AD subscription</span></span>
* <span data-ttu-id="0dfbd-117">Azure AD Connect tooextend hello şirket içi dizin tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="0dfbd-117">Azure AD Connect tooextend hello on-premises directory tooAzure AD</span></span>
* <span data-ttu-id="0dfbd-118">Tooconnect etki alanına katılmış aygıtlar tooAzure AD ayarlanmış İlkesi</span><span class="sxs-lookup"><span data-stu-id="0dfbd-118">Policy that's set tooconnect domain-joined devices tooAzure AD</span></span>
* <span data-ttu-id="0dfbd-119">Cihazlar için Windows 10 derleme (derleme 10551 ya da daha yeni)</span><span class="sxs-lookup"><span data-stu-id="0dfbd-119">Windows 10 build (build 10551 or newer) for devices</span></span>

<span data-ttu-id="0dfbd-120">İş ve Windows Hello için Windows Hello tooenable hello aşağıdakileri de gerekir:</span><span class="sxs-lookup"><span data-stu-id="0dfbd-120">tooenable Windows Hello for Business and Windows Hello, you will also need hello following:</span></span>

- <span data-ttu-id="0dfbd-121">**Ortak anahtar altyapısı (PKI)** kullanıcı sertifikaları verme için.</span><span class="sxs-lookup"><span data-stu-id="0dfbd-121">**Public key infrastructure (PKI)** for user certificates issuance.</span></span>

- <span data-ttu-id="0dfbd-122">**System Center Configuration Manager geçerli dalının** -tooinstall sürümü 1606 veya üzeri gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="0dfbd-122">**System Center Configuration Manager Current Branch** - You need tooinstall version 1606 or better.</span></span>  
<span data-ttu-id="0dfbd-123">Daha fazla bilgi için bkz.</span><span class="sxs-lookup"><span data-stu-id="0dfbd-123">For more information, see:</span></span> 
    - [<span data-ttu-id="0dfbd-124">System Center Configuration Manager belgeleri</span><span class="sxs-lookup"><span data-stu-id="0dfbd-124">Documentation for System Center Configuration Manager</span></span>](https://technet.microsoft.com/library/mt346023.aspx)
    - [<span data-ttu-id="0dfbd-125">System Center Configuration Manager ekip blogu</span><span class="sxs-lookup"><span data-stu-id="0dfbd-125">System Center Configuration Manager Team Blog</span></span>](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx)
    - [<span data-ttu-id="0dfbd-126">İşletme ayarlarını System Center Configuration Manager için Windows Hello</span><span class="sxs-lookup"><span data-stu-id="0dfbd-126">Windows Hello for Business settings in System Center Configuration Manager</span></span>](https://docs.microsoft.com/sccm/protect/deploy-use/windows-hello-for-business-settings)

<span data-ttu-id="0dfbd-127">Bir alternatif toohello PKI Dağıtımı gereksinimini bunu hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="0dfbd-127">As an alternative toohello PKI deployment requirement, you can do hello following:</span></span>

* <span data-ttu-id="0dfbd-128">Windows Server 2016 Active Directory etki alanı Hizmetleri ile birkaç etki alanı denetleyicilerine sahip.</span><span class="sxs-lookup"><span data-stu-id="0dfbd-128">Have a few domain controllers with Windows Server 2016 Active Directory Domain Services.</span></span>

<span data-ttu-id="0dfbd-129">tooenable koşullu erişim, hiçbir ek dağıtımı ile erişim toodomain katılmış cihazları izin ver Grup İlkesi ayarları oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0dfbd-129">tooenable conditional access, you can create Group Policy settings that allow access toodomain-joined devices with no additional deployments.</span></span> <span data-ttu-id="0dfbd-130">Merhaba aygıt uyumluluğuna göre toomanage erişim denetimi hello aşağıdaki gerekir:</span><span class="sxs-lookup"><span data-stu-id="0dfbd-130">toomanage access control based on compliance of hello device, you will need hello following:</span></span>

* <span data-ttu-id="0dfbd-131">System Center Configuration Manager geçerli dalının (1606 veya üstü) için iş senaryoları için Windows Hello</span><span class="sxs-lookup"><span data-stu-id="0dfbd-131">System Center Configuration Manager Current Branch (1606 or later) for Windows Hello for Business scenarios</span></span>

## <a name="deployment-instructions"></a><span data-ttu-id="0dfbd-132">Dağıtım yönergeleri</span><span class="sxs-lookup"><span data-stu-id="0dfbd-132">Deployment instructions</span></span>

<span data-ttu-id="0dfbd-133">toodeploy, listelenen hello adımları [nasıl tooconfigure otomatik kayıt Windows etki alanına katılmış cihazları Azure Active Directory ile](active-directory-conditional-access-automatic-device-registration-setup.md)</span><span class="sxs-lookup"><span data-stu-id="0dfbd-133">toodeploy, follow hello steps listed in [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span></span>

## <a name="next-step"></a><span data-ttu-id="0dfbd-134">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="0dfbd-134">Next step</span></span>
* [<span data-ttu-id="0dfbd-135">Merhaba kuruluş için Windows 10: yolları toouse cihazlar iş için</span><span class="sxs-lookup"><span data-stu-id="0dfbd-135">Windows 10 for hello enterprise: Ways toouse devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="0dfbd-136">Bulut özellikleri tooWindows 10 cihazların Azure Active Directory katılım aracılığıyla genişletme</span><span class="sxs-lookup"><span data-stu-id="0dfbd-136">Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="0dfbd-137">Azure AD Katılımı kullanım senaryoları hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="0dfbd-137">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="0dfbd-138">Etki alanına katılmış aygıtlar tooAzure Windows 10 deneyimleri için AD Bağlan</span><span class="sxs-lookup"><span data-stu-id="0dfbd-138">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="0dfbd-139">Azure AD'ye Katılım ayarlama</span><span class="sxs-lookup"><span data-stu-id="0dfbd-139">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

