---
title: "iki aşamalı doğrulama Azure MFA hakkında aaaLearn | Microsoft Docs"
description: "Azure multi-Factor Authentication nedir, neden MFA, hello çok faktörlü kimlik doğrulama istemcisi ve hello farklı yöntemler ve kullanılabilir sürümleri hakkında daha fazla bilgi kullanın. "
keywords: "mfa nedir giriş tooMFA, mfa genel bakış"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: c40d7a34-1274-4496-96b0-784850c06e9b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/03/2017
ms.author: kgremban
ms.openlocfilehash: a91b8d6941d2b6ce72a789a97c57e10e594e7ada
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-multi-factor-authentication"></a><span data-ttu-id="4df91-104">Azure Multi-Factor Authentication nedir?</span><span class="sxs-lookup"><span data-stu-id="4df91-104">What is Azure Multi-Factor Authentication?</span></span>
<span data-ttu-id="4df91-105">İki aşamalı doğrulama, birden fazla doğrulama yöntemi gerektiren ve güvenlik toouser oturum açmalarına ve işlemlerine önemli bir ikinci katmanı ekleyen kimlik doğrulama yöntemidir.</span><span class="sxs-lookup"><span data-stu-id="4df91-105">Two-step verification is a method of authentication that requires more than one verification method and adds a critical second layer of security toouser sign-ins and transactions.</span></span> <span data-ttu-id="4df91-106">Her iki veya daha fazla doğrulama yöntemlerini aşağıdaki hello isteyerek çalışır:</span><span class="sxs-lookup"><span data-stu-id="4df91-106">It works by requiring any two or more of hello following verification methods:</span></span>

* <span data-ttu-id="4df91-107">(Genellikle parola) bildiğiniz bir şey</span><span class="sxs-lookup"><span data-stu-id="4df91-107">Something you know (typically a password)</span></span>
* <span data-ttu-id="4df91-108">(Kolayca, bir telefon gibi yineleniyor değil güvenilir bir cihaz) sahip olduğunuz şey</span><span class="sxs-lookup"><span data-stu-id="4df91-108">Something you have (a trusted device that is not easily duplicated, like a phone)</span></span>
* <span data-ttu-id="4df91-109">(Biyometri) olan bir şey</span><span class="sxs-lookup"><span data-stu-id="4df91-109">Something you are (biometrics)</span></span>

<span data-ttu-id="4df91-110"><center>![Kullanıcı adı ve parola](./media/multi-factor-authentication/pword.png) &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ![sertifikaları](./media/multi-factor-authentication/phone.png) &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ![Akıllı Telefon](./media/multi-factor-authentication/hware.png) &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ![akıllı kart](./media/multi-factor-authentication/smart.png) &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ![sanal akıllı kart](./media/multi-factor-authentication/vsmart.png) &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ![kullanıcı adı ve parola](./media/multi-factor-authentication/cert.png)</center></span><span class="sxs-lookup"><span data-stu-id="4df91-110"><center>![Username and Password](./media/multi-factor-authentication/pword.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Certificates](./media/multi-factor-authentication/phone.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Smart Phone](./media/multi-factor-authentication/hware.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Smart Card](./media/multi-factor-authentication/smart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Virtual Smart Card](./media/multi-factor-authentication/vsmart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Username and Password](./media/multi-factor-authentication/cert.png)</center></span></span>

<span data-ttu-id="4df91-111">Azure Multi-Factor Authentication (MFA) Microsoft'un iki adımlı doğrulama çözümüdür.</span><span class="sxs-lookup"><span data-stu-id="4df91-111">Azure Multi-Factor Authentication (MFA) is Microsoft's two-step verification solution.</span></span> <span data-ttu-id="4df91-112">Azure MFA kullanıcı talebine basit bir oturum açma işlemi için buluştururken koruma erişim toodata ve uygulamaları yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="4df91-112">Azure MFA helps safeguard access toodata and applications while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="4df91-113">Bir dizi doğrulama yöntemi (ör. telefon çağrısı, metin mesajı veya mobil uygulama doğrulaması) aracılığıyla güçlü kimlik doğrulaması sunar.</span><span class="sxs-lookup"><span data-stu-id="4df91-113">It delivers strong authentication via a range of verification methods, including phone call, text message, or mobile app verification.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/WA-MFA-Overview/player]
>
>

## <a name="why-use-azure-multi-factor-authentication"></a><span data-ttu-id="4df91-114">Azure multi-Factor Authentication neden kullanılır?</span><span class="sxs-lookup"><span data-stu-id="4df91-114">Why use Azure Multi-Factor Authentication?</span></span>
<span data-ttu-id="4df91-115">Bugün, birden çok, kişilerin giderek bağlanır.</span><span class="sxs-lookup"><span data-stu-id="4df91-115">Today, more than ever, people are increasingly connected.</span></span> <span data-ttu-id="4df91-116">Akıllı telefonlar, tabletler, dizüstü bilgisayarlar ve Bilgisayarları ile kişilerin nasıl tooconnect giderek ve herhangi bir zamanda bağlı kalın üzerinde birkaç farklı seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="4df91-116">With smart phones, tablets, laptops, and PCs, people have several different options on how they are going tooconnect and stay connected at any time.</span></span> <span data-ttu-id="4df91-117">Kişiler kendi hesaplarının ve uygulamaların yerden, onların kullanıcılarınızın daha fazla işi halletmesine ve böylelikle müşterilerine hizmet anlamına gelir daha iyi erişebilir.</span><span class="sxs-lookup"><span data-stu-id="4df91-117">People can access their accounts and applications from anywhere, which means that they can get more work done and serve their customers better.</span></span>

<span data-ttu-id="4df91-118">Azure çok faktörlü kimlik doğrulaması, ölçeklenebilir, kolay bir toouse ve kullanıcılarınızın her zaman korunması için güvenilir çözümü, ikinci bir kimlik doğrulama yöntemi sağlar.</span><span class="sxs-lookup"><span data-stu-id="4df91-118">Azure Multi-Factor Authentication is an easy toouse, scalable, and reliable solution that provides a second method of authentication so your users are always protected.</span></span>

| ![Kolay tooUse](./media/multi-factor-authentication/simple.png) | ![Ölçeklenebilir](./media/multi-factor-authentication/scalable.png) | ![Her zaman korunması](./media/multi-factor-authentication/protected.png) | ![Güvenilir](./media/multi-factor-authentication/reliable.png) |
|:---:|:---:|:---:|:---:|
| <span data-ttu-id="4df91-123">**Kolay toouse**</span><span class="sxs-lookup"><span data-stu-id="4df91-123">**Easy toouse**</span></span> |<span data-ttu-id="4df91-124">**Ölçeklenebilir**</span><span class="sxs-lookup"><span data-stu-id="4df91-124">**Scalable**</span></span> |<span data-ttu-id="4df91-125">**Her zaman korunması**</span><span class="sxs-lookup"><span data-stu-id="4df91-125">**Always Protected**</span></span> |<span data-ttu-id="4df91-126">**Güvenilir**</span><span class="sxs-lookup"><span data-stu-id="4df91-126">**Reliable**</span></span> |

* <span data-ttu-id="4df91-127">**Kolay tooUse** -Azure çok faktörlü kimlik doğrulaması, basit tooset yukarı ve kullanın.</span><span class="sxs-lookup"><span data-stu-id="4df91-127">**Easy tooUse** - Azure Multi-Factor Authentication is simple tooset up and use.</span></span> <span data-ttu-id="4df91-128">Hello Azure multi-Factor Authentication ile birlikte gelen fazladan koruma kullanıcılar toomanage kendi cihazlarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="4df91-128">hello extra protection that comes with Azure Multi-Factor Authentication allows users toomanage their own devices.</span></span> <span data-ttu-id="4df91-129">Birçok durumlarda tüm en iyi, yalnızca birkaç basit tıklama ile ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="4df91-129">Best of all, in many instances it can be set up with just a few simple clicks.</span></span>
* <span data-ttu-id="4df91-130">**Ölçeklenebilir** -Azure multi-Factor Authentication hello bulut hello gücünü kullanır ve şirket içi ile tümleşir AD ve özel uygulamalar.</span><span class="sxs-lookup"><span data-stu-id="4df91-130">**Scalable** - Azure Multi-Factor Authentication uses hello power of hello cloud and integrates with your on-premises AD and custom apps.</span></span> <span data-ttu-id="4df91-131">Bu koruma bile tooyour yüksek hacimli, kritik senaryolar genişletilir.</span><span class="sxs-lookup"><span data-stu-id="4df91-131">This protection is even extended tooyour high-volume, mission-critical scenarios.</span></span>
* <span data-ttu-id="4df91-132">**Her zaman korumalı** -Azure multi-Factor Authentication hello yüksek endüstri standartları kullanarak güçlü kimlik doğrulaması sağlar.</span><span class="sxs-lookup"><span data-stu-id="4df91-132">**Always Protected** - Azure Multi-Factor Authentication provides strong authentication using hello highest industry standards.</span></span>
* <span data-ttu-id="4df91-133">**Güvenilir** -Azure çok faktörlü kimlik doğrulaması % 99,9 kullanılabilirliğini garanti ediyoruz.</span><span class="sxs-lookup"><span data-stu-id="4df91-133">**Reliable** - We guarantee 99.9% availability of Azure Multi-Factor Authentication.</span></span> <span data-ttu-id="4df91-134">erişemediği zaman hello hizmeti kullanılamaz olarak kabul edilir hello iki aşamalı doğrulamayı tooreceive veya işlem doğrulama istekleri.</span><span class="sxs-lookup"><span data-stu-id="4df91-134">hello service is considered unavailable when it is unable tooreceive or process verification requests for hello two-step verification.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Windows-Azure-Multi-Factor-Authentication/player]


## <a name="next-steps"></a><span data-ttu-id="4df91-135">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4df91-135">Next steps</span></span>

- <span data-ttu-id="4df91-136">Hakkında bilgi edinin [Azure multi-Factor Authentication nasıl çalışır](multi-factor-authentication-how-it-works.md)</span><span class="sxs-lookup"><span data-stu-id="4df91-136">Learn about [how Azure Multi-Factor Authentication works](multi-factor-authentication-how-it-works.md)</span></span>

- <span data-ttu-id="4df91-137">Merhaba farklı hakkında okuyun [sürümleri ve Azure çok faktörlü kimlik doğrulaması için tüketim yöntemi](multi-factor-authentication-versions-plans.md)</span><span class="sxs-lookup"><span data-stu-id="4df91-137">Read about hello different [versions and consumption methods for Azure Multi-Factor Authentication](multi-factor-authentication-versions-plans.md)</span></span>
