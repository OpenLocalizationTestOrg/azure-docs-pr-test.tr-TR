---
title: Azure Active Directory raporlama bildirimleri
description: "Azure Active Directory'ı bildirimleri şüpheli oturum için raporlama kullanma bileşenleri."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ae6d4b0e-5931-4cb3-98bf-9be91b381c92
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.custom: oldportal
ms.reviewer: dhanyahk
ms.openlocfilehash: f4632bd2af802b10c8c64972e8c605d7ad7c0eaf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-reporting-notifications"></a><span data-ttu-id="d8d08-103">Azure Active Directory raporlama bildirimleri</span><span class="sxs-lookup"><span data-stu-id="d8d08-103">Azure Active Directory Reporting Notifications</span></span>
## <a name="what-reports-generate-email-notifications"></a><span data-ttu-id="d8d08-104">E-posta bildirimleri hangi raporlar oluşturur</span><span class="sxs-lookup"><span data-stu-id="d8d08-104">What reports generate email notifications</span></span>
<span data-ttu-id="d8d08-105">Şu anda yalnızca düzensiz oturum açma etkinliği raporu Tetikleyicileri e-posta bildirimleri.</span><span class="sxs-lookup"><span data-stu-id="d8d08-105">At this time, only the Irregular Sign in Activity report triggers email notifications.</span></span>

## <a name="what-is-an-irregular-sign-in"></a><span data-ttu-id="d8d08-106">Bir "düzensiz oturum açma" nedir?</span><span class="sxs-lookup"><span data-stu-id="d8d08-106">What is an "Irregular Sign in"?</span></span>
<span data-ttu-id="d8d08-107">Düzensiz oturum açma işlemleri bizim machine learning algoritmaları, bir oturum açma anormal konum ve cihaz ile birlikte bir "mümkün olmayan seyahat" koşulu temel alarak tarafından tanımlanmış izinlerdir.</span><span class="sxs-lookup"><span data-stu-id="d8d08-107">Irregular sign-ins are those that have been identified by our machine learning algorithms, on the basis of an "impossible travel" condition combined with an anomalous sign-in location and device.</span></span> <span data-ttu-id="d8d08-108">Bu, bir bilgisayar korsanının bu hesabı kullanarak oturum açmaya çalışırken gösteriyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="d8d08-108">This may indicate that a hacker has been trying to sign in using this account.</span></span>

## <a name="who-receives-the-email-notifications"></a><span data-ttu-id="d8d08-109">Kimlerin e-posta bildirimleri alacağını?</span><span class="sxs-lookup"><span data-stu-id="d8d08-109">Who receives the email notifications?</span></span>
<span data-ttu-id="d8d08-110">Bir Active Directory Premium lisansı atanmış olan tüm genel yöneticilere e-posta gönderilir.</span><span class="sxs-lookup"><span data-stu-id="d8d08-110">The email is sent to all global admins who have been assigned an Active Directory Premium license.</span></span> <span data-ttu-id="d8d08-111">Teslim emin olmak için biz bunu yöneticileri için alternatif e-posta adresi de gönderin.</span><span class="sxs-lookup"><span data-stu-id="d8d08-111">To ensure it is delivered, we send it to the admins Alternate Email Address as well.</span></span> <span data-ttu-id="d8d08-112">Yöneticileri içermelidir aad-alerts-noreply@mail.windowsazure.com e-posta kaçırmamak için kendi Güvenilir Gönderenler listesinde.</span><span class="sxs-lookup"><span data-stu-id="d8d08-112">Admins should include aad-alerts-noreply@mail.windowsazure.com in their safe senders list so they don’t miss the email.</span></span>

## <a name="how-often-are-these-emails-sent"></a><span data-ttu-id="d8d08-113">Gönderilen bu e-postaları ne sıklıkla misiniz?</span><span class="sxs-lookup"><span data-stu-id="d8d08-113">How often are these emails sent?</span></span>
<span data-ttu-id="d8d08-114">E-posta, 10 yeni düzensiz oturum açma etkinliklerini son 30 gün içinde ortaya ya da son e-posta gönderilip gönderilmediğini olduğundan, hangisi daha az ise gönderilir.</span><span class="sxs-lookup"><span data-stu-id="d8d08-114">The email is sent if 10 new irregular sign-in activities occur in the last 30 days, or since the last email was sent, whichever is less.</span></span>

## <a name="how-do-i-access-the-report-mentioned-in-the-email"></a><span data-ttu-id="d8d08-115">Belirtilen e-posta ile rapor nasıl erişirim?</span><span class="sxs-lookup"><span data-stu-id="d8d08-115">How do I access the report mentioned in the email?</span></span>
<span data-ttu-id="d8d08-116">Bağlantıya tıkladığınızda, Klasik Azure portalı içinde rapor sayfasına yönlendirileceksiniz.</span><span class="sxs-lookup"><span data-stu-id="d8d08-116">When you click on the link, you will be redirected to the report page within the Azure classic portal.</span></span> <span data-ttu-id="d8d08-117">Rapora erişmek için her ikisinin de olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="d8d08-117">In order to access the report, you need to be both:</span></span>

* <span data-ttu-id="d8d08-118">Bir yönetici veya Azure aboneliğinizin ortak yönetici</span><span class="sxs-lookup"><span data-stu-id="d8d08-118">An admin or co-admin of your Azure subscription</span></span>
* <span data-ttu-id="d8d08-119">Dizinde genel yönetici ve bir Active Directory Premium lisansı atanmış.</span><span class="sxs-lookup"><span data-stu-id="d8d08-119">A global administrator in the directory, and assigned an Active Directory Premium license.</span></span> <span data-ttu-id="d8d08-120">Daha fazla bilgi için bkz. [Azure Active Directory sürümleri](active-directory-editions.md).</span><span class="sxs-lookup"><span data-stu-id="d8d08-120">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span></span>

## <a name="can-i-turn-off-these-emails"></a><span data-ttu-id="d8d08-121">Bu e-postaları kapatabilir miyim?</span><span class="sxs-lookup"><span data-stu-id="d8d08-121">Can I turn off these emails?</span></span>
<span data-ttu-id="d8d08-122">Evet, Klasik Azure portalı içinde anormal oturum açma işlemlerine ilgili bildirimler devre dışı bırakmak için tıklatın **yapılandırma**ve ardından **devre dışı** altında **bildirimleri** bölüm.</span><span class="sxs-lookup"><span data-stu-id="d8d08-122">Yes, to turn off notifications related to anomalous sign-ins within the Azure classic portal, click **Configure**, and then select **Disabled** under the **Notifications** section.</span></span>

## <a name="whats-next"></a><span data-ttu-id="d8d08-123">Sırada ne var?</span><span class="sxs-lookup"><span data-stu-id="d8d08-123">What's next</span></span>
* <span data-ttu-id="d8d08-124">Hangi güvenlik, Denetim ve etkinlik raporları kullanılabilir merak ediyor?</span><span class="sxs-lookup"><span data-stu-id="d8d08-124">Curious about what security, audit, and activity reports are available?</span></span> <span data-ttu-id="d8d08-125">Kullanıma [Azure AD güvenlik, Denetim ve etkinlik raporları](active-directory-view-access-usage-reports.md)</span><span class="sxs-lookup"><span data-stu-id="d8d08-125">Check out [Azure AD Security, Audit, and Activity Reports](active-directory-view-access-usage-reports.md)</span></span>
* [<span data-ttu-id="d8d08-126">Azure Active Directory Premium ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="d8d08-126">Getting started with Azure Active Directory Premium</span></span>](active-directory-get-started-premium.md)
* [<span data-ttu-id="d8d08-127">Oturum Açma ve Erişim Paneli sayfalarınıza şirket markası ekleme</span><span class="sxs-lookup"><span data-stu-id="d8d08-127">Add company branding to your Sign In and Access Panel pages</span></span>](active-directory-add-company-branding.md)

