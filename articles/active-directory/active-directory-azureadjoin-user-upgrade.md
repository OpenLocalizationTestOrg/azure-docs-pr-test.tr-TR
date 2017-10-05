---
title: "Ayarlar'dan Azure AD ile Windows 10 cihazı ayarlama | Microsoft Docs"
description: "Ayarlar menüsünde aracılığıyla Azure ad kullanıcıların nasıl katılabilirsiniz açıklanmaktadır."
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
ms.openlocfilehash: 5a3963f16b471ad1ca8681b22a1a027935400465
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-a-windows-10-device-with-azure-ad-from-settings"></a><span data-ttu-id="da470-103">Ayarlar'dan Azure AD ile Windows 10 cihazı ayarlama</span><span class="sxs-lookup"><span data-stu-id="da470-103">Set up a Windows 10 device with Azure AD from Settings</span></span>
<span data-ttu-id="da470-104">Zaten Windows 7 veya Windows 8 kullanıyorsanız ve bilgisayarınızı veya Cihazınızı Windows 10'a yükseltildikten ayarlar menüsünü kullanarak Azure Active Directory (Azure AD) katılabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="da470-104">If you are already using Windows 7 or Windows 8, and your computer or device has been upgraded to Windows 10, you can join to Azure Active Directory (Azure AD) through the Settings menu.</span></span>

## <a name="to-join-to-azure-ad-from-the-settings-menu"></a><span data-ttu-id="da470-105">Azure AD için Ayarlar menüsünden katılmak için</span><span class="sxs-lookup"><span data-stu-id="da470-105">To join to Azure AD from the Settings menu</span></span>
1. <span data-ttu-id="da470-106">Gelen **Başlat** menüsünde tıklatın **ayarları** düğmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="da470-106">From the **Start** menu, click the **Settings** charm.</span></span>
2. <span data-ttu-id="da470-107">Gelen **ayarları**seçin **sistem**->**hakkında**->**katılma Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="da470-107">From **Settings**, select     **System**->**About**->**Join Azure AD**.</span></span>
   
   <span data-ttu-id="da470-108"><center>
   ![Ayarlar menüsünde Azure AD katılım](./media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png)</center></span><span class="sxs-lookup"><span data-stu-id="da470-108"><center>
![Join Azure AD from the Settings menu](./media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png) </center></span></span>
3. <span data-ttu-id="da470-109">Tıklatın **devam** Azure AD katılım ileti penceresinde.</span><span class="sxs-lookup"><span data-stu-id="da470-109">Click **Continue** in the Azure AD Join message window.</span></span>
   
   <span data-ttu-id="da470-110"><center>
   ![Azure AD birleştirme ileti penceresinde](./media/active-directory-azureadjoin/active-directory-azureadjoin-message.png)</center></span><span class="sxs-lookup"><span data-stu-id="da470-110"><center>
![Join Azure AD message window](./media/active-directory-azureadjoin/active-directory-azureadjoin-message.png) </center></span></span>
4. <span data-ttu-id="da470-111">Oturum açma kimlik bilgilerinizi sağlayın.</span><span class="sxs-lookup"><span data-stu-id="da470-111">Provide your sign-in credentials.</span></span> <span data-ttu-id="da470-112">Bu oturum açma deneyimini tam kimlik doğrulaması için gereken tüm adımları içerir.</span><span class="sxs-lookup"><span data-stu-id="da470-112">This sign-in experience will include all the steps that are required to complete authentication.</span></span> <span data-ttu-id="da470-113">Federasyon Kiracı parçası ise, yöneticiniz size kuruluşunuz tarafından barındırılan bir Federasyon deneyim sağlayacaktır.</span><span class="sxs-lookup"><span data-stu-id="da470-113">If you are part of a federated tenant, your administrator will provide you with the federation experience that's hosted by your organization.</span></span>
   <span data-ttu-id="da470-114"><center>
   ![Oturum açma kimlik bilgilerini sağlamanız](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png)</center></span><span class="sxs-lookup"><span data-stu-id="da470-114"><center>
![Provide sign-in credentials](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png) </center></span></span>
5. <span data-ttu-id="da470-115">Kuruluşunuz, Azure AD ile katılmak için Azure multi-Factor Authentication yapılandırdıysa, devam etmeden önce ikinci Faktörlü sağlar.</span><span class="sxs-lookup"><span data-stu-id="da470-115">If your organization has configured Azure Multi-Factor Authentication for joining to Azure AD, provide the second factor before proceeding.</span></span>
6. <span data-ttu-id="da470-116">Tıklatın **kabul** üzerinde **bu cihazın yönetilmesine izin** ekran.</span><span class="sxs-lookup"><span data-stu-id="da470-116">Click **Accept** on the **Allow this device to be managed** screen.</span></span>
7. <span data-ttu-id="da470-117">"Cihazınız artık kuruluşunuzun Azure AD'de katıldı" iletisini görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="da470-117">You should see the message "Your device is now joined to your organization in Azure AD".</span></span>

## <a name="additional-information"></a><span data-ttu-id="da470-118">Ek bilgiler</span><span class="sxs-lookup"><span data-stu-id="da470-118">Additional information</span></span>
* [<span data-ttu-id="da470-119">Azure AD Katılımı kullanım senaryoları hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="da470-119">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="da470-120">Windows 10 deneyiminden faydalanmak için etki alanına katılan cihazları Azure AD'ye bağlama</span><span class="sxs-lookup"><span data-stu-id="da470-120">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="da470-121">Azure AD'ye Katılım ayarlama</span><span class="sxs-lookup"><span data-stu-id="da470-121">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)
* [<span data-ttu-id="da470-122">Microsoft Passport aracılığıyla parolası olmayan kimlikleri doğrulama</span><span class="sxs-lookup"><span data-stu-id="da470-122">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)

