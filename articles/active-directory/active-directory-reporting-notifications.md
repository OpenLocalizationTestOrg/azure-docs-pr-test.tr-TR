---
title: aaaAzure Active Directory raporlama bildirimleri
description: "Nasıl toouse hello şüpheli oturum için Azure Active Directory raporlama bildirimleri bileşenleri."
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
ms.openlocfilehash: 3843c45eaf9d68e671943bfdbc7ab68933f38fbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-notifications"></a><span data-ttu-id="b5959-103">Azure Active Directory raporlama bildirimleri</span><span class="sxs-lookup"><span data-stu-id="b5959-103">Azure Active Directory Reporting Notifications</span></span>
## <a name="what-reports-generate-email-notifications"></a><span data-ttu-id="b5959-104">E-posta bildirimleri hangi raporlar oluşturur</span><span class="sxs-lookup"><span data-stu-id="b5959-104">What reports generate email notifications</span></span>
<span data-ttu-id="b5959-105">Şu anda yalnızca hello düzensiz oturum Etkinlik Raporu Tetikleyicileri e-posta bildirimleri.</span><span class="sxs-lookup"><span data-stu-id="b5959-105">At this time, only hello Irregular Sign in Activity report triggers email notifications.</span></span>

## <a name="what-is-an-irregular-sign-in"></a><span data-ttu-id="b5959-106">Bir "düzensiz oturum açma" nedir?</span><span class="sxs-lookup"><span data-stu-id="b5959-106">What is an "Irregular Sign in"?</span></span>
<span data-ttu-id="b5959-107">Düzensiz oturum açma işlemleri bizim machine learning algoritmaları, bir oturum açma anormal konum ve cihaz ile birlikte bir "mümkün olmayan seyahat" koşulun hello temelinde tarafından tanımlanmış izinlerdir.</span><span class="sxs-lookup"><span data-stu-id="b5959-107">Irregular sign-ins are those that have been identified by our machine learning algorithms, on hello basis of an "impossible travel" condition combined with an anomalous sign-in location and device.</span></span> <span data-ttu-id="b5959-108">Bu, bir bilgisayar korsanının bu hesabı kullanarak toosign çalışıyor olduğunu gösteriyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="b5959-108">This may indicate that a hacker has been trying toosign in using this account.</span></span>

## <a name="who-receives-hello-email-notifications"></a><span data-ttu-id="b5959-109">Kimin hello e-posta bildirimleri alan?</span><span class="sxs-lookup"><span data-stu-id="b5959-109">Who receives hello email notifications?</span></span>
<span data-ttu-id="b5959-110">bir Active Directory Premium lisansı atanmış olan tooall genel Yöneticiler Hello e-posta gönderilir.</span><span class="sxs-lookup"><span data-stu-id="b5959-110">hello email is sent tooall global admins who have been assigned an Active Directory Premium license.</span></span> <span data-ttu-id="b5959-111">teslim tooensure, biz de toohello admins alternatif e-posta adresi göndermek.</span><span class="sxs-lookup"><span data-stu-id="b5959-111">tooensure it is delivered, we send it toohello admins Alternate Email Address as well.</span></span> <span data-ttu-id="b5959-112">Yöneticileri içermelidir aad-alerts-noreply@mail.windowsazure.com hello e-posta kaçırmamak için kendi Güvenilir Gönderenler listesinde.</span><span class="sxs-lookup"><span data-stu-id="b5959-112">Admins should include aad-alerts-noreply@mail.windowsazure.com in their safe senders list so they don’t miss hello email.</span></span>

## <a name="how-often-are-these-emails-sent"></a><span data-ttu-id="b5959-113">Gönderilen bu e-postaları ne sıklıkla misiniz?</span><span class="sxs-lookup"><span data-stu-id="b5959-113">How often are these emails sent?</span></span>
<span data-ttu-id="b5959-114">Merhaba e-posta, 10 yeni düzensiz oturum açma etkinliklerini hello son 30 günde bir yapılır ya da hello son e-posta gönderilip gönderilmediğini olduğundan, hangisi daha az ise gönderilir.</span><span class="sxs-lookup"><span data-stu-id="b5959-114">hello email is sent if 10 new irregular sign-in activities occur in hello last 30 days, or since hello last email was sent, whichever is less.</span></span>

## <a name="how-do-i-access-hello-report-mentioned-in-hello-email"></a><span data-ttu-id="b5959-115">Merhaba e-postayla bahsedilen hello raporu nasıl erişirim?</span><span class="sxs-lookup"><span data-stu-id="b5959-115">How do I access hello report mentioned in hello email?</span></span>
<span data-ttu-id="b5959-116">Merhaba bağlantısına tıkladığınızda, yeniden yönlendirilen toohello rapor sayfasının hello Klasik Azure portalı içinde olacaktır.</span><span class="sxs-lookup"><span data-stu-id="b5959-116">When you click on hello link, you will be redirected toohello report page within hello Azure classic portal.</span></span> <span data-ttu-id="b5959-117">Sırayla tooaccess rapor Merhaba, toobe hem gerekir:</span><span class="sxs-lookup"><span data-stu-id="b5959-117">In order tooaccess hello report, you need toobe both:</span></span>

* <span data-ttu-id="b5959-118">Bir yönetici veya Azure aboneliğinizin ortak yönetici</span><span class="sxs-lookup"><span data-stu-id="b5959-118">An admin or co-admin of your Azure subscription</span></span>
* <span data-ttu-id="b5959-119">Merhaba dizininde genel yönetici ve bir Active Directory Premium lisansı atanmış.</span><span class="sxs-lookup"><span data-stu-id="b5959-119">A global administrator in hello directory, and assigned an Active Directory Premium license.</span></span> <span data-ttu-id="b5959-120">Daha fazla bilgi için bkz. [Azure Active Directory sürümleri](active-directory-editions.md).</span><span class="sxs-lookup"><span data-stu-id="b5959-120">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span></span>

## <a name="can-i-turn-off-these-emails"></a><span data-ttu-id="b5959-121">Bu e-postaları kapatabilir miyim?</span><span class="sxs-lookup"><span data-stu-id="b5959-121">Can I turn off these emails?</span></span>
<span data-ttu-id="b5959-122">Evet, bildirimler devre dışı tooturn tooanomalous oturum açma işlemleri hello Klasik Azure portalı içinde ilgili, tıklatın **yapılandırma**ve ardından **devre dışı** hello altında **bildirimleri**bölümü.</span><span class="sxs-lookup"><span data-stu-id="b5959-122">Yes, tooturn off notifications related tooanomalous sign-ins within hello Azure classic portal, click **Configure**, and then select **Disabled** under hello **Notifications** section.</span></span>

## <a name="whats-next"></a><span data-ttu-id="b5959-123">Sırada ne var?</span><span class="sxs-lookup"><span data-stu-id="b5959-123">What's next</span></span>
* <span data-ttu-id="b5959-124">Hangi güvenlik, Denetim ve etkinlik raporları kullanılabilir merak ediyor?</span><span class="sxs-lookup"><span data-stu-id="b5959-124">Curious about what security, audit, and activity reports are available?</span></span> <span data-ttu-id="b5959-125">Kullanıma [Azure AD güvenlik, Denetim ve etkinlik raporları](active-directory-view-access-usage-reports.md)</span><span class="sxs-lookup"><span data-stu-id="b5959-125">Check out [Azure AD Security, Audit, and Activity Reports](active-directory-view-access-usage-reports.md)</span></span>
* [<span data-ttu-id="b5959-126">Azure Active Directory Premium ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="b5959-126">Getting started with Azure Active Directory Premium</span></span>](active-directory-get-started-premium.md)
* [<span data-ttu-id="b5959-127">Tooyour oturum aç ve erişim paneli sayfalarınıza şirket markası ekleme</span><span class="sxs-lookup"><span data-stu-id="b5959-127">Add company branding tooyour Sign In and Access Panel pages</span></span>](active-directory-add-company-branding.md)

