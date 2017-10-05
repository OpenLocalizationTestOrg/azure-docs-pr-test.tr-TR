---
title: "Kişisel bir cihazı kuruluşunuza katma | Microsoft Docs"
description: "Kullanıcıların kişisel Windows 10 cihazlarını şirket ağlarına nasıl kaydedebilirsiniz açıklanmakta ve bir BYOD senaryosu için dağıtım adımları sağlar."
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 9f3d38f5-1cfd-43d4-97da-4fed1255a1ff
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 9418365ea18b065551448742b21c8b17a1749fc8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="join-a-personal-device-to-your-organization"></a><span data-ttu-id="be5be-103">Kişisel bir cihazı kuruluşunuza katma</span><span class="sxs-lookup"><span data-stu-id="be5be-103">Join a personal device to your organization</span></span>
## <a name="to-join-a-windows-10-device-to-your-organization"></a><span data-ttu-id="be5be-104">Windows 10 cihaz kuruluşunuza katma</span><span class="sxs-lookup"><span data-stu-id="be5be-104">To join a Windows 10 device to your organization</span></span>
1. <span data-ttu-id="be5be-105">Gelen **Başlat** menüsünde, select **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="be5be-105">From the **Start** menu, select **Settings**.</span></span>
2. <span data-ttu-id="be5be-106">Seçin **hesapları**ve ardından **hesabınızı**.</span><span class="sxs-lookup"><span data-stu-id="be5be-106">Select **Accounts**, and then click **Your account**.</span></span>
3. <span data-ttu-id="be5be-107">Tıklatın **eklemek iş veya Okul hesabı**ve ardından kuruluş hesabınızı yazın.</span><span class="sxs-lookup"><span data-stu-id="be5be-107">Click **Add Work or School account**, and then type in your organizational account.</span></span>
4. <span data-ttu-id="be5be-108">Kuruluşunuzun oturum açma sayfasında, kullanıcı adınızı ve parolanızı girin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="be5be-108">On the sign-in page for your organization, enter your user name and password, and then click **OK**.</span></span>
5. <span data-ttu-id="be5be-109">Çok faktörlü kimlik doğrulaması sınaması için istenir.</span><span class="sxs-lookup"><span data-stu-id="be5be-109">You will be prompted for a multi-factor authentication challenge.</span></span> <span data-ttu-id="be5be-110">(Bu sorunu, bir BT yöneticisi tarafından yapılandırılabilir.)</span><span class="sxs-lookup"><span data-stu-id="be5be-110">(This challenge is configurable by an IT administrator.)</span></span>
6. <span data-ttu-id="be5be-111">Azure Active Directory (Azure AD) cihaz mobil cihaz Yönetimi kaydı gerekli olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="be5be-111">Azure Active Directory (Azure AD) checks whether the device requires mobile device management enrollment.</span></span>
7. <span data-ttu-id="be5be-112">Windows Azure AD'de kuruluşunuzun dizininde cihazı kaydeder ve uygun durumlarda mobil cihaz Yönetimi'nde kaydeder.</span><span class="sxs-lookup"><span data-stu-id="be5be-112">Windows registers the device in the organization’s directory in Azure AD and enrolls it in mobile device management, if appropriate.</span></span>
8. <span data-ttu-id="be5be-113">Yönetilen bir kullanıcı varsa, Windows, masaüstüne otomatik oturum açma alır.</span><span class="sxs-lookup"><span data-stu-id="be5be-113">If you are a managed user, Windows takes you to the desktop through the automatic sign-in.</span></span>
9. <span data-ttu-id="be5be-114">Bir Federasyon kullanıcısı varsa, bir Windows ekrana oturum açma kimlik bilgilerinizi girmeniz için alınır.</span><span class="sxs-lookup"><span data-stu-id="be5be-114">If you are a federated user, you will be taken to a Windows sign-in screen to enter your credentials.</span></span>

## <a name="additional-information"></a><span data-ttu-id="be5be-115">Ek bilgiler</span><span class="sxs-lookup"><span data-stu-id="be5be-115">Additional information</span></span>
* [<span data-ttu-id="be5be-116">Kurumlar için Windows 10: Cihazları iş için kullanmanın yolları</span><span class="sxs-lookup"><span data-stu-id="be5be-116">Windows 10 for the enterprise: Ways to use devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="be5be-117">Azure Active Directory Join ile bulut işlevlerini Windows 10 cihazlarına genişletme</span><span class="sxs-lookup"><span data-stu-id="be5be-117">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="be5be-118">Microsoft Passport aracılığıyla parolası olmayan kimlikleri doğrulama</span><span class="sxs-lookup"><span data-stu-id="be5be-118">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)
* [<span data-ttu-id="be5be-119">Azure AD Katılımı kullanım senaryoları hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="be5be-119">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="be5be-120">Windows 10 deneyiminden faydalanmak için etki alanına katılan cihazları Azure AD'ye bağlama</span><span class="sxs-lookup"><span data-stu-id="be5be-120">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="be5be-121">Azure AD'ye Katılım ayarlama</span><span class="sxs-lookup"><span data-stu-id="be5be-121">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

