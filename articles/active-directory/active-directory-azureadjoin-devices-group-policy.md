---
title: "Windows 10 deneyimleri için etki alanına katılmış cihazları Azure AD'ye bağlanma | Microsoft Docs"
description: "Yöneticiler cihazlarının kurumsal ağ etki alanına katılmasını sağlamak için Grup İlkesi nasıl yapılandırabileceğiniz açıklanmaktadır."
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
ms.openlocfilehash: 9c91579d20bb84701f6d0b97d944728c84044adf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="connect-domain-joined-devices-to-azure-ad-for-windows-10-experiences"></a><span data-ttu-id="3b82f-103">Windows 10 deneyiminden faydalanmak için, etki alanına katılan cihazları Azure AD'ye bağlama</span><span class="sxs-lookup"><span data-stu-id="3b82f-103">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>
<span data-ttu-id="3b82f-104">Etki alanına katılma, geleneksel bir şekilde kuruluşların son 15 yıl ve daha fazlası için iş için cihazları bağlandınız ' dir.</span><span class="sxs-lookup"><span data-stu-id="3b82f-104">Domain join is the traditional way organizations have connected devices for work for the last 15 years and more.</span></span> <span data-ttu-id="3b82f-105">Kullanıcıların cihazlarına, Windows Server Active Directory (Active Directory) işlerini kullanarak oturum açın veya Okul hesapları etkin ve izin verilen tam olarak bu cihazları yönetmek için BT.</span><span class="sxs-lookup"><span data-stu-id="3b82f-105">It has enabled users to sign in to their devices by using their Windows Server Active Directory (Active Directory) work or school accounts and allowed IT to fully manage these devices.</span></span> <span data-ttu-id="3b82f-106">Kuruluşlar, genellikle kullanıcılara cihazları sağlamak için görüntü oluşturma yöntemleri kullanır ve genellikle bunları yönetmek için Grup İlkesi veya System Center Configuration Manager (SCCM) kullanın.</span><span class="sxs-lookup"><span data-stu-id="3b82f-106">Organizations typically rely on imaging methods to provision devices to users and generally use System Center Configuration Manager (SCCM) or Group Policy to manage them.</span></span>


<span data-ttu-id="3b82f-107">Azure Active Directory (Azure AD) aygıtları bağladıktan sonra Windows 10 etki alanına katılma ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="3b82f-107">Domain join in Windows 10 provides you with the following benefits after you connect devices to Azure Active Directory (Azure AD):</span></span>

* <span data-ttu-id="3b82f-108">Çoklu oturum açma (SSO) Azure AD kaynaklara her yerden</span><span class="sxs-lookup"><span data-stu-id="3b82f-108">Single sign-on (SSO) to Azure AD resources from anywhere</span></span>
* <span data-ttu-id="3b82f-109">İş veya Okul hesapları (Microsoft hesabı gereklidir) kullanarak kurumsal Windows mağazası erişimi</span><span class="sxs-lookup"><span data-stu-id="3b82f-109">Access to the enterprise Windows Store by using work or school accounts (no Microsoft account required)</span></span>
* <span data-ttu-id="3b82f-110">Kurumsal uyumlu kullanıcı cihaz üzerinden iş veya Okul hesapları (Microsoft hesabı gereklidir) kullanarak Dolaşım ayarları</span><span class="sxs-lookup"><span data-stu-id="3b82f-110">Enterprise-compliant roaming of user settings across devices by using work or school accounts (no Microsoft account required)</span></span>
* <span data-ttu-id="3b82f-111">Güçlü kimlik doğrulaması ve güvenli oturum açma için iş veya Okul hesaplarıyla iş için Windows Hello ve Windows Hello</span><span class="sxs-lookup"><span data-stu-id="3b82f-111">Strong authentication and convenient sign-in for work or school accounts with Windows Hello for Business and Windows Hello</span></span>
* <span data-ttu-id="3b82f-112">Kurumsal cihaz Grup İlkesi ayarları ile uyumlu cihazlara erişimi sınırlandırma</span><span class="sxs-lookup"><span data-stu-id="3b82f-112">Ability to restrict access only to devices that comply with organizational device Group Policy settings</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3b82f-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="3b82f-113">Prerequisites</span></span>
<span data-ttu-id="3b82f-114">Etki alanına katılma yararlı olacak şekilde devam eder.</span><span class="sxs-lookup"><span data-stu-id="3b82f-114">Domain join continues to be useful.</span></span> <span data-ttu-id="3b82f-115">Ancak, için SSO Azure AD yararları almak için iş veya Okul hesapları ve erişim ayarlarının Windows Mağazası'na iş veya Okul hesaplarıyla dolaşım, aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="3b82f-115">However, to get the Azure AD benefits of SSO, roaming of settings with work or school accounts, and access to Windows Store with work or school accounts, you will need the following:</span></span>

* <span data-ttu-id="3b82f-116">Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="3b82f-116">Azure AD subscription</span></span>
* <span data-ttu-id="3b82f-117">Azure AD ile şirket içi dizin genişletmek için azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="3b82f-117">Azure AD Connect to extend the on-premises directory to Azure AD</span></span>
* <span data-ttu-id="3b82f-118">Etki alanına katılmış cihazları Azure AD'ye bağlamak için ayarlanmış İlkesi</span><span class="sxs-lookup"><span data-stu-id="3b82f-118">Policy that's set to connect domain-joined devices to Azure AD</span></span>
* <span data-ttu-id="3b82f-119">Cihazlar için Windows 10 derleme (derleme 10551 ya da daha yeni)</span><span class="sxs-lookup"><span data-stu-id="3b82f-119">Windows 10 build (build 10551 or newer) for devices</span></span>

<span data-ttu-id="3b82f-120">Windows Hello iş ve Windows Hello için etkinleştirmek için ayrıca aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="3b82f-120">To enable Windows Hello for Business and Windows Hello, you will also need the following:</span></span>

- <span data-ttu-id="3b82f-121">**Ortak anahtar altyapısı (PKI)** kullanıcı sertifikaları verme için.</span><span class="sxs-lookup"><span data-stu-id="3b82f-121">**Public key infrastructure (PKI)** for user certificates issuance.</span></span>

- <span data-ttu-id="3b82f-122">**System Center Configuration Manager geçerli dalının** -sürüm 1606 ya da daha iyi yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="3b82f-122">**System Center Configuration Manager Current Branch** - You need to install version 1606 or better.</span></span>  
<span data-ttu-id="3b82f-123">Daha fazla bilgi için bkz.</span><span class="sxs-lookup"><span data-stu-id="3b82f-123">For more information, see:</span></span> 
    - [<span data-ttu-id="3b82f-124">System Center Configuration Manager belgeleri</span><span class="sxs-lookup"><span data-stu-id="3b82f-124">Documentation for System Center Configuration Manager</span></span>](https://technet.microsoft.com/library/mt346023.aspx)
    - [<span data-ttu-id="3b82f-125">System Center Configuration Manager ekip blogu</span><span class="sxs-lookup"><span data-stu-id="3b82f-125">System Center Configuration Manager Team Blog</span></span>](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx)
    - [<span data-ttu-id="3b82f-126">İşletme ayarlarını System Center Configuration Manager için Windows Hello</span><span class="sxs-lookup"><span data-stu-id="3b82f-126">Windows Hello for Business settings in System Center Configuration Manager</span></span>](https://docs.microsoft.com/sccm/protect/deploy-use/windows-hello-for-business-settings)

<span data-ttu-id="3b82f-127">PKI Dağıtımı gereksinimini alternatif olarak, aşağıdakileri yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3b82f-127">As an alternative to the PKI deployment requirement, you can do the following:</span></span>

* <span data-ttu-id="3b82f-128">Windows Server 2016 Active Directory etki alanı Hizmetleri ile birkaç etki alanı denetleyicilerine sahip.</span><span class="sxs-lookup"><span data-stu-id="3b82f-128">Have a few domain controllers with Windows Server 2016 Active Directory Domain Services.</span></span>

<span data-ttu-id="3b82f-129">Koşullu erişimi etkinleştirmek için hiçbir ek dağıtımı ile etki alanına katılmış cihazları erişmesine izin vermek Grup İlkesi ayarları oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3b82f-129">To enable conditional access, you can create Group Policy settings that allow access to domain-joined devices with no additional deployments.</span></span> <span data-ttu-id="3b82f-130">Cihaz uyumluluğuna göre erişim denetimini yönetmek için aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="3b82f-130">To manage access control based on compliance of the device, you will need the following:</span></span>

* <span data-ttu-id="3b82f-131">System Center Configuration Manager geçerli dalının (1606 veya üstü) için iş senaryoları için Windows Hello</span><span class="sxs-lookup"><span data-stu-id="3b82f-131">System Center Configuration Manager Current Branch (1606 or later) for Windows Hello for Business scenarios</span></span>

## <a name="deployment-instructions"></a><span data-ttu-id="3b82f-132">Dağıtım yönergeleri</span><span class="sxs-lookup"><span data-stu-id="3b82f-132">Deployment instructions</span></span>

<span data-ttu-id="3b82f-133">Dağıtmak için listelenen adımları [Azure Active Directory ile etki alanına katılmış Windows cihazlarının otomatik kaydını yapılandırma](active-directory-conditional-access-automatic-device-registration-setup.md)</span><span class="sxs-lookup"><span data-stu-id="3b82f-133">To deploy, follow the steps listed in [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span></span>

## <a name="next-step"></a><span data-ttu-id="3b82f-134">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="3b82f-134">Next step</span></span>
* [<span data-ttu-id="3b82f-135">Kurumlar için Windows 10: Cihazları iş için kullanmanın yolları</span><span class="sxs-lookup"><span data-stu-id="3b82f-135">Windows 10 for the enterprise: Ways to use devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="3b82f-136">Azure Active Directory Join ile bulut işlevlerini Windows 10 cihazlarına genişletme</span><span class="sxs-lookup"><span data-stu-id="3b82f-136">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="3b82f-137">Azure AD Katılımı kullanım senaryoları hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="3b82f-137">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="3b82f-138">Windows 10 deneyiminden faydalanmak için etki alanına katılan cihazları Azure AD'ye bağlama</span><span class="sxs-lookup"><span data-stu-id="3b82f-138">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="3b82f-139">Azure AD'ye Katılım ayarlama</span><span class="sxs-lookup"><span data-stu-id="3b82f-139">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

