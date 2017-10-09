---
title: "aaaJoin bir kişisel cihaz tooyour kuruluş | Microsoft Docs"
description: "Kullanıcıların kişisel Windows 10 cihazları tootheir şirket ağlarına nasıl kaydedebilirsiniz açıklanmakta ve bir BYOD senaryosu için dağıtım adımları sağlar."
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
ms.openlocfilehash: 979e2461dd9ad0438aa402a0a3223cc84c4c625c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-personal-device-tooyour-organization"></a><span data-ttu-id="4b1fd-103">Kişisel cihaz tooyour kuruluş katılma</span><span class="sxs-lookup"><span data-stu-id="4b1fd-103">Join a personal device tooyour organization</span></span>
## <a name="toojoin-a-windows-10-device-tooyour-organization"></a><span data-ttu-id="4b1fd-104">toojoin Windows 10 cihaz tooyour kuruluş</span><span class="sxs-lookup"><span data-stu-id="4b1fd-104">toojoin a Windows 10 device tooyour organization</span></span>
1. <span data-ttu-id="4b1fd-105">Merhaba gelen **Başlat** menüsünde, select **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="4b1fd-105">From hello **Start** menu, select **Settings**.</span></span>
2. <span data-ttu-id="4b1fd-106">Seçin **hesapları**ve ardından **hesabınızı**.</span><span class="sxs-lookup"><span data-stu-id="4b1fd-106">Select **Accounts**, and then click **Your account**.</span></span>
3. <span data-ttu-id="4b1fd-107">Tıklatın **eklemek iş veya Okul hesabı**ve ardından kuruluş hesabınızı yazın.</span><span class="sxs-lookup"><span data-stu-id="4b1fd-107">Click **Add Work or School account**, and then type in your organizational account.</span></span>
4. <span data-ttu-id="4b1fd-108">Merhaba oturum açma sayfasında, kuruluşunuz için kullanıcı adınızı ve parolanızı girin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="4b1fd-108">On hello sign-in page for your organization, enter your user name and password, and then click **OK**.</span></span>
5. <span data-ttu-id="4b1fd-109">Çok faktörlü kimlik doğrulaması sınaması için istenir.</span><span class="sxs-lookup"><span data-stu-id="4b1fd-109">You will be prompted for a multi-factor authentication challenge.</span></span> <span data-ttu-id="4b1fd-110">(Bu sorunu, bir BT yöneticisi tarafından yapılandırılabilir.)</span><span class="sxs-lookup"><span data-stu-id="4b1fd-110">(This challenge is configurable by an IT administrator.)</span></span>
6. <span data-ttu-id="4b1fd-111">Azure Active Directory (Azure AD) hello cihaz mobil cihaz Yönetimi kaydı gerekli olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="4b1fd-111">Azure Active Directory (Azure AD) checks whether hello device requires mobile device management enrollment.</span></span>
7. <span data-ttu-id="4b1fd-112">Windows hello aygıt hello kuruluşunuzun dizininde Azure AD'de kaydeder ve uygun durumlarda mobil cihaz Yönetimi'nde kaydeder.</span><span class="sxs-lookup"><span data-stu-id="4b1fd-112">Windows registers hello device in hello organization’s directory in Azure AD and enrolls it in mobile device management, if appropriate.</span></span>
8. <span data-ttu-id="4b1fd-113">Yönetilen bir kullanıcı varsa, Windows hello otomatik oturum açma aracılığıyla toohello masaüstüne alır.</span><span class="sxs-lookup"><span data-stu-id="4b1fd-113">If you are a managed user, Windows takes you toohello desktop through hello automatic sign-in.</span></span>
9. <span data-ttu-id="4b1fd-114">Bir Federasyon kullanıcısı varsa, siz olacaksınız kimlik bilgilerinizi tooa Windows oturum açma ekranı tooenter gerçekleştirilecek.</span><span class="sxs-lookup"><span data-stu-id="4b1fd-114">If you are a federated user, you will be taken tooa Windows sign-in screen tooenter your credentials.</span></span>

## <a name="additional-information"></a><span data-ttu-id="4b1fd-115">Ek bilgiler</span><span class="sxs-lookup"><span data-stu-id="4b1fd-115">Additional information</span></span>
* [<span data-ttu-id="4b1fd-116">Merhaba kuruluş için Windows 10: yolları toouse cihazlar iş için</span><span class="sxs-lookup"><span data-stu-id="4b1fd-116">Windows 10 for hello enterprise: Ways toouse devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="4b1fd-117">Bulut özellikleri tooWindows 10 cihazların Azure Active Directory katılım aracılığıyla genişletme</span><span class="sxs-lookup"><span data-stu-id="4b1fd-117">Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="4b1fd-118">Microsoft Passport aracılığıyla parolası olmayan kimlikleri doğrulama</span><span class="sxs-lookup"><span data-stu-id="4b1fd-118">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)
* [<span data-ttu-id="4b1fd-119">Azure AD Katılımı kullanım senaryoları hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="4b1fd-119">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="4b1fd-120">Etki alanına katılmış aygıtlar tooAzure Windows 10 deneyimleri için AD Bağlan</span><span class="sxs-lookup"><span data-stu-id="4b1fd-120">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="4b1fd-121">Azure AD'ye Katılım ayarlama</span><span class="sxs-lookup"><span data-stu-id="4b1fd-121">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

