---
title: "Azure çok faktörlü kimlik doğrulaması - nasıl çalışır?"
description: "Azure Multi-Factor Authentication, kullanıcıların basit bir oturum açma işlemi taleplerini karşılarken, verilere ve uygulamalara erişimi korumaya da yardımcı olur. İkinci bir form kimlik doğrulama isteyerek ek güvenlik sağlar ve bir dizi kolay doğrulama seçeneklerini aracılığıyla güçlü kimlik doğrulaması sunar."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d14db902-9afe-4fca-b3a5-4bd54b3d8ec5
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 6fee02885cc76b3a4fdad11e8702f623d6fe6597
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-azure-multi-factor-authentication-works"></a><span data-ttu-id="8a284-104">Azure multi-Factor Authentication nasıl çalışır</span><span class="sxs-lookup"><span data-stu-id="8a284-104">How Azure Multi-Factor Authentication works</span></span>
<span data-ttu-id="8a284-105">İki aşamalı doğrulama güvenlik, katmanlı yaklaşımın arasındadır.</span><span class="sxs-lookup"><span data-stu-id="8a284-105">The security of two-step verification lies in its layered approach.</span></span> <span data-ttu-id="8a284-106">Birden çok kimlik doğrulama faktörleri tehlikeye saldırganlar için önemli bir sınama gösterir.</span><span class="sxs-lookup"><span data-stu-id="8a284-106">Compromising multiple authentication factors presents a significant challenge for attackers.</span></span> <span data-ttu-id="8a284-107">Bir saldırgan kullanıcı parolasının öğrenmek bile yönetiliyorsa, bu da güvenilen cihaza sahip gerek kalmadan gereksizdir.</span><span class="sxs-lookup"><span data-stu-id="8a284-107">Even if an attacker manages to learn the user's password, it is useless without also having possession of the trusted device.</span></span> 

![Proofup](./media/multi-factor-authentication-how-it-works/howitworks.png)

<span data-ttu-id="8a284-109">Azure Multi-Factor Authentication, kullanıcıların basit bir oturum açma işlemi taleplerini karşılarken, verilere ve uygulamalara erişimi korumaya da yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="8a284-109">Azure Multi-Factor Authentication helps safeguard access to data and applications while meeting user demand for a simple sign-in process.</span></span>  <span data-ttu-id="8a284-110">İkinci bir form kimlik doğrulama isteyerek ek güvenlik sağlar ve bir dizi kolay doğrulama seçeneklerini aracılığıyla güçlü kimlik doğrulaması sunar.</span><span class="sxs-lookup"><span data-stu-id="8a284-110">It provides additional security by requiring a second form of authentication and delivers strong authentication via a range of easy verification options.</span></span>


## <a name="methods-available-for-two-step-verification"></a><span data-ttu-id="8a284-111">İki aşamalı doğrulama için kullanılabilen yöntemler</span><span class="sxs-lookup"><span data-stu-id="8a284-111">Methods available for two-step verification</span></span>
<span data-ttu-id="8a284-112">Bir kullanıcı oturum açtığında ek doğrulama kullanıcıya gönderilir.</span><span class="sxs-lookup"><span data-stu-id="8a284-112">When a user signs in, an additional verification is sent to the user.</span></span>  <span data-ttu-id="8a284-113">Bu ikinci doğrulama için kullanılan yöntemleri listesi verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="8a284-113">The following are a list of methods that can be used for this second verification.</span></span>

| <span data-ttu-id="8a284-114">Doğrulama yöntemi</span><span class="sxs-lookup"><span data-stu-id="8a284-114">Verification Method</span></span> | <span data-ttu-id="8a284-115">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8a284-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8a284-116">Telefon araması</span><span class="sxs-lookup"><span data-stu-id="8a284-116">Phone call</span></span> |<span data-ttu-id="8a284-117">Çağrı, bir kullanıcının kayıtlı telefon yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="8a284-117">A call is placed to a user’s registered phone.</span></span> <span data-ttu-id="8a284-118">Gerekli ardından # tuşuna bastığında, kullanıcı bir PIN girer.</span><span class="sxs-lookup"><span data-stu-id="8a284-118">The user enters a PIN if necessary then presses the # key.</span></span> |
| <span data-ttu-id="8a284-119">SMS mesajı</span><span class="sxs-lookup"><span data-stu-id="8a284-119">Text message</span></span> |<span data-ttu-id="8a284-120">Kısa mesaj kullanıcı cep telefonu altı rakamlı bir kod ile gönderilir.</span><span class="sxs-lookup"><span data-stu-id="8a284-120">A text message is sent to a user’s mobile phone with a six-digit code.</span></span> <span data-ttu-id="8a284-121">Kullanıcı oturum açma sayfasında bu kodu girer.</span><span class="sxs-lookup"><span data-stu-id="8a284-121">The user enters this code on the sign-in page.</span></span> |
| <span data-ttu-id="8a284-122">Mobil uygulama bildirimi</span><span class="sxs-lookup"><span data-stu-id="8a284-122">Mobile app notification</span></span> |<span data-ttu-id="8a284-123">Bir kullanıcının Akıllı telefonu doğrulama isteği gönderilir.</span><span class="sxs-lookup"><span data-stu-id="8a284-123">A verification request is sent to a user’s smart phone.</span></span> <span data-ttu-id="8a284-124">Kullanıcı bir PIN gerekli olduğunda girer sonra seçer **doğrula** mobil uygulama üzerinde.</span><span class="sxs-lookup"><span data-stu-id="8a284-124">The user enters a PIN if necessary then selects **Verify** on the mobile app.</span></span> |
| <span data-ttu-id="8a284-125">Mobil uygulama doğrulama kodu</span><span class="sxs-lookup"><span data-stu-id="8a284-125">Mobile app verification code</span></span> |<span data-ttu-id="8a284-126">Bir kullanıcının Akıllı telefonu üzerinde çalıştığından, mobil uygulama değişiklikleri her 30 saniyede bir doğrulama kodu görüntüler.</span><span class="sxs-lookup"><span data-stu-id="8a284-126">The mobile app, which is running on a user’s smart phone, displays a verification code that changes every 30 seconds.</span></span> <span data-ttu-id="8a284-127">Kullanıcı en son kod bulur ve oturum açma sayfasında girer.</span><span class="sxs-lookup"><span data-stu-id="8a284-127">The user finds the most recent code and enters it on the sign-in page.</span></span> |
| <span data-ttu-id="8a284-128">Üçüncü taraf OATH belirteçleri</span><span class="sxs-lookup"><span data-stu-id="8a284-128">Third-party OATH tokens</span></span> | <span data-ttu-id="8a284-129">Azure multi-Factor Authentication sunucusu, üçüncü taraf doğrulaması yöntemlerini kabul edecek şekilde yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="8a284-129">Azure Multi-Factor Authentication Server can be configured to accept third-party verification methods.</span></span> |

<span data-ttu-id="8a284-130">Azure çok faktörlü kimlik doğrulaması, hem bulut hem de sunucu için seçilebilir doğrulama yöntemlerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="8a284-130">Azure Multi-Factor Authentication provides selectable verification methods for both cloud and server.</span></span> <span data-ttu-id="8a284-131">Hangi yöntemler, kullanıcılarınız için kullanılabilir seçebilirsiniz: telefon araması, metin, uygulama bildirimi veya uygulama kodları.</span><span class="sxs-lookup"><span data-stu-id="8a284-131">You can choose which methods are available for your users: phone call, text, app notification, or app codes.</span></span> <span data-ttu-id="8a284-132">Daha fazla bilgi için bkz: [seçilebilir doğrulama yöntemlerini](multi-factor-authentication-whats-next.md#selectable-verification-methods).</span><span class="sxs-lookup"><span data-stu-id="8a284-132">For more information, see [selectable verification methods](multi-factor-authentication-whats-next.md#selectable-verification-methods).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8a284-133">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8a284-133">Next steps</span></span>

- <span data-ttu-id="8a284-134">Farklı hakkında okuyun [sürümleri ve Azure çok faktörlü kimlik doğrulaması için tüketim yöntemi](multi-factor-authentication-versions-plans.md)</span><span class="sxs-lookup"><span data-stu-id="8a284-134">Read about the different [versions and consumption methods for Azure Multi-Factor Authentication](multi-factor-authentication-versions-plans.md)</span></span>

- <span data-ttu-id="8a284-135">Azure MFA dağıtmak isteyip istemediğinizi seçin [bulutta veya şirket içi](multi-factor-authentication-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="8a284-135">Choose whether to deploy Azure MFA [in the cloud or on-premises](multi-factor-authentication-get-started.md)</span></span>

- <span data-ttu-id="8a284-136">Okuma yanıtlar için [sık sorulan sorular](multi-factor-authentication-faq.md)</span><span class="sxs-lookup"><span data-stu-id="8a284-136">Read answers for [Frequently asked questions](multi-factor-authentication-faq.md)</span></span>