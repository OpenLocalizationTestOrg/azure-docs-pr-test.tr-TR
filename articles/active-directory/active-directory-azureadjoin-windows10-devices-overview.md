---
title: "Kuruluş için Windows 10: cihazları iş için kullanmanın yolları | Microsoft Docs"
description: "Windows 10 cihazları şirketler ve Microsoft bulutu için Azure Active Directory ile tümleştirme için dağıtımı genel bakış. Çelişir farklı yolları bir aygıtı sağlanan ve Azure Portalı aracılığıyla bir kuruluşta kullanılır."
keywords: "Windows bulut, Windows Azure Active Directory, Windows 10 cihazlarda Azure, Azure Windows cihazları"
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 2cb9ab6a-55b6-4658-b7f2-6e05ae015e1b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 804156048a7596f9937098e6fe762f424526473c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="windows-10-for-the-enterprise-ways-to-use-devices-for-work"></a><span data-ttu-id="3f61f-105">Kurumlar için Windows 10: Cihazları iş için kullanmanın yolları</span><span class="sxs-lookup"><span data-stu-id="3f61f-105">Windows 10 for the enterprise: Ways to use devices for work</span></span>
<span data-ttu-id="3f61f-106">Windows 10, Azure Active Directory (Azure AD) kullanmasına olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="3f61f-106">Windows 10 gives you the ability to leverage Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="3f61f-107">Böylece kullanıcılar için Windows Azure kimlikleri ekleyerek veya Azure AD hesapları kullanarak iş uygulamalarına ve kaynaklarına erişmek için oturum açabilirsiniz Windows 10 cihazları Azure AD'ye bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="3f61f-107">You can connect Windows 10 devices to Azure AD so that users can sign in to Windows by using Azure AD accounts or by adding their Azure IDs to gain access to business apps and resources.</span></span>

![Azure Active Directory Windows bulut ile](./media/active-directory-azureadjoin/windows10-overview.png)

## <a name="integrating-windows-10-devices-with-azure-active-directory--a-content-map"></a><span data-ttu-id="3f61f-109">Windows 10 cihazlarının Azure Active Directory ile--içerik haritası tümleştirme</span><span class="sxs-lookup"><span data-stu-id="3f61f-109">Integrating Windows 10 devices with Azure Active Directory--a content map</span></span>
<span data-ttu-id="3f61f-110">Aşağıdaki konular, kuruluşunuzdaki Windows 10 cihazlarının farklı özellikler fikir sağlar.</span><span class="sxs-lookup"><span data-stu-id="3f61f-110">The following topics provide insights into different capabilities of Windows 10 devices in your organization.</span></span>

|  | <span data-ttu-id="3f61f-111">Konu başlıkları</span><span class="sxs-lookup"><span data-stu-id="3f61f-111">Topics</span></span> |
| --- | --- |
| <span data-ttu-id="3f61f-112">Başlarken</span><span class="sxs-lookup"><span data-stu-id="3f61f-112">Getting started</span></span> |[<span data-ttu-id="3f61f-113">Windows 10 cihazlarını çalışma alanınızda kullanma</span><span class="sxs-lookup"><span data-stu-id="3f61f-113">Using Windows 10 devices in your workplace</span></span>](active-directory-azureadjoin-windows10-devices.md) <br> <br> [<span data-ttu-id="3f61f-114">Azure Active Directory Join ile bulut işlevlerini Windows 10 cihazlarına genişletme</span><span class="sxs-lookup"><span data-stu-id="3f61f-114">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-overview.md) <br> <br> [<span data-ttu-id="3f61f-115">Microsoft Passport aracılığıyla parolası olmayan kimlikleri doğrulama</span><span class="sxs-lookup"><span data-stu-id="3f61f-115">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md) |
| <span data-ttu-id="3f61f-116">Dağıtım</span><span class="sxs-lookup"><span data-stu-id="3f61f-116">Deployment</span></span> |[<span data-ttu-id="3f61f-117">Kullanım senaryoları ve Azure AD katılım için dağıtım konuları</span><span class="sxs-lookup"><span data-stu-id="3f61f-117">Usage scenarios and deployment considerations for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md) <br><br> [<span data-ttu-id="3f61f-118">Etki alanına katılmış cihazlar Windows 10 için Azure AD'ye bağlanma deneyimleri</span><span class="sxs-lookup"><span data-stu-id="3f61f-118">Connecting domain-joined devices to Azure AD, for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)<br><br>[<span data-ttu-id="3f61f-119">Kuruluşunuzda iş için Microsoft Passport'u etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="3f61f-119">Enabling Microsoft Passport for work in the organization</span></span>](active-directory-azureadjoin-passport-deployment.md)<br><br> [<span data-ttu-id="3f61f-120">Windows 10 Kurumsal durumda Dolaşım etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="3f61f-120">Enabling Enterprise State Roaming for Windows 10</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)<br><br> |
| <span data-ttu-id="3f61f-121">Kullanıcı görevleri</span><span class="sxs-lookup"><span data-stu-id="3f61f-121">User tasks</span></span> |[<span data-ttu-id="3f61f-122">Kurulum sırasında Azure AD ile yeni bir Windows 10 cihazı ayarlama</span><span class="sxs-lookup"><span data-stu-id="3f61f-122">Setting up a new Windows 10 device with Azure AD during setup</span></span>](active-directory-azureadjoin-user-frx.md) <br><br> [<span data-ttu-id="3f61f-123">Ayarlar'dan Azure AD ile Windows 10 cihazı ayarlama</span><span class="sxs-lookup"><span data-stu-id="3f61f-123">Setting up a Windows 10 device with Azure AD from the settings menu</span></span>](active-directory-azureadjoin-user-upgrade.md) <br><br> [<span data-ttu-id="3f61f-124">Kişisel bir Windows 10 cihazı kuruluşunuza birleştirme</span><span class="sxs-lookup"><span data-stu-id="3f61f-124">Joining a personal Windows 10 device to your organization</span></span>](active-directory-azureadjoin-personal-device.md) |

