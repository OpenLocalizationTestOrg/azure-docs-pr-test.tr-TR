---
title: "Windows 10 cihaz ayarlarından Azure AD ile yukarı aaaSet | Microsoft Docs"
description: "Kullanıcıların tooAzure AD hello ayarları menüsü aracılığıyla nasıl katılabilirsiniz açıklanmaktadır."
services: active-directory
documentationcenter: 
author: femila
manager: swadhwa
editor: 
tags: azure-classic-portal
ms.assetid: b844e1d9-ad43-4e4a-a398-5c4a43bf2f5c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: d6485228338db571cc01f913c99fbba49e0bb74a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-windows-10-device-with-azure-ad-from-settings"></a><span data-ttu-id="5a587-103">Ayarlar'dan Azure AD ile Windows 10 cihazı ayarlama</span><span class="sxs-lookup"><span data-stu-id="5a587-103">Set up a Windows 10 device with Azure AD from Settings</span></span>
<span data-ttu-id="5a587-104">Zaten varsa Windows 7 veya Windows 8 ve bilgisayarınızı veya Cihazınızı kullanarak yükseltilmiş tooWindows 10 bırakıldı, tooAzure Active Directory (Azure AD) hello ayarları menüsü aracılığıyla katılabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5a587-104">If you are already using Windows 7 or Windows 8, and your computer or device has been upgraded tooWindows 10, you can join tooAzure Active Directory (Azure AD) through hello Settings menu.</span></span>

## <a name="toojoin-tooazure-ad-from-hello-settings-menu"></a><span data-ttu-id="5a587-105">hello ayarları menüsünden toojoin tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="5a587-105">toojoin tooAzure AD from hello Settings menu</span></span>
1. <span data-ttu-id="5a587-106">Hello gelen **Başlat** menüsünde hello tıklatın **ayarları** düğmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="5a587-106">From hello **Start** menu, click hello **Settings** charm.</span></span>
2. <span data-ttu-id="5a587-107">Gelen **ayarları**seçin **sistem**->**hakkında**->**katılma Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="5a587-107">From **Settings**, select     **System**->**About**->**Join Azure AD**.</span></span>
   
   <span data-ttu-id="5a587-108"><center>
   ![Hello ayarları menüsünden Azure AD katılım](./media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png)</center></span><span class="sxs-lookup"><span data-stu-id="5a587-108"><center>
![Join Azure AD from hello Settings menu](./media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png) </center></span></span>
3. <span data-ttu-id="5a587-109">Tıklatın **devam** hello Azure AD katılım ileti penceresinde.</span><span class="sxs-lookup"><span data-stu-id="5a587-109">Click **Continue** in hello Azure AD Join message window.</span></span>
   
   <span data-ttu-id="5a587-110"><center>
   ![Azure AD birleştirme ileti penceresinde](./media/active-directory-azureadjoin/active-directory-azureadjoin-message.png)</center></span><span class="sxs-lookup"><span data-stu-id="5a587-110"><center>
![Join Azure AD message window](./media/active-directory-azureadjoin/active-directory-azureadjoin-message.png) </center></span></span>
4. <span data-ttu-id="5a587-111">Oturum açma kimlik bilgilerinizi sağlayın.</span><span class="sxs-lookup"><span data-stu-id="5a587-111">Provide your sign-in credentials.</span></span> <span data-ttu-id="5a587-112">Bu oturum açma deneyimini gerekli toocomplete kimlik doğrulaması tüm hello adımları içerir.</span><span class="sxs-lookup"><span data-stu-id="5a587-112">This sign-in experience will include all hello steps that are required toocomplete authentication.</span></span> <span data-ttu-id="5a587-113">Federasyon Kiracı parçası ise, yöneticiniz size hello Federasyon kuruluşunuz tarafından barındırılan bir deneyim sunar.</span><span class="sxs-lookup"><span data-stu-id="5a587-113">If you are part of a federated tenant, your administrator will provide you with hello federation experience that's hosted by your organization.</span></span>
   <span data-ttu-id="5a587-114"><center>
   ![Oturum açma kimlik bilgilerini sağlamanız](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png)</center></span><span class="sxs-lookup"><span data-stu-id="5a587-114"><center>
![Provide sign-in credentials](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png) </center></span></span>
5. <span data-ttu-id="5a587-115">Kuruluşunuz, tooAzure AD katılmak için Azure multi-Factor Authentication yapılandırdıysa, devam etmeden önce hello ikinci Faktörlü sağlar.</span><span class="sxs-lookup"><span data-stu-id="5a587-115">If your organization has configured Azure Multi-Factor Authentication for joining tooAzure AD, provide hello second factor before proceeding.</span></span>
6. <span data-ttu-id="5a587-116">Tıklatın **kabul** hello üzerinde **yönetilen bu cihaz toobe izin** ekran.</span><span class="sxs-lookup"><span data-stu-id="5a587-116">Click **Accept** on hello **Allow this device toobe managed** screen.</span></span>
7. <span data-ttu-id="5a587-117">"Cihazınız artık Azure AD alanına katılmış tooyour kuruluşta" hello iletisini görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="5a587-117">You should see hello message "Your device is now joined tooyour organization in Azure AD".</span></span>

## <a name="additional-information"></a><span data-ttu-id="5a587-118">Ek bilgiler</span><span class="sxs-lookup"><span data-stu-id="5a587-118">Additional information</span></span>
* [<span data-ttu-id="5a587-119">Azure AD Katılımı kullanım senaryoları hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="5a587-119">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="5a587-120">Etki alanına katılmış aygıtlar tooAzure Windows 10 deneyimleri için AD Bağlan</span><span class="sxs-lookup"><span data-stu-id="5a587-120">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="5a587-121">Azure AD'ye Katılım ayarlama</span><span class="sxs-lookup"><span data-stu-id="5a587-121">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)
* [<span data-ttu-id="5a587-122">Microsoft Passport aracılığıyla parolası olmayan kimlikleri doğrulama</span><span class="sxs-lookup"><span data-stu-id="5a587-122">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)

