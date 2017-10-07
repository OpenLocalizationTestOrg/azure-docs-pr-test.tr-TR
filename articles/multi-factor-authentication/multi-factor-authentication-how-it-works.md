---
title: "çok faktörlü kimlik doğrulaması - aaaAzure nasıl çalışır?"
description: "Azure multi-Factor Authentication kullanıcı talebine basit bir oturum açma işlemi için buluştururken koruma erişim toodata ve uygulamaları yardımcı olur. İkinci bir form kimlik doğrulama isteyerek ek güvenlik sağlar ve bir dizi kolay doğrulama seçeneklerini aracılığıyla güçlü kimlik doğrulaması sunar."
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
ms.openlocfilehash: 82f234fb86f145c42e8e56b8bdd2d61720c9ff2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-azure-multi-factor-authentication-works"></a><span data-ttu-id="09dd7-104">Azure multi-Factor Authentication nasıl çalışır</span><span class="sxs-lookup"><span data-stu-id="09dd7-104">How Azure Multi-Factor Authentication works</span></span>
<span data-ttu-id="09dd7-105">iki aşamalı doğrulamayı Hello güvenliğini, katmanlı yaklaşımın arasındadır.</span><span class="sxs-lookup"><span data-stu-id="09dd7-105">hello security of two-step verification lies in its layered approach.</span></span> <span data-ttu-id="09dd7-106">Birden çok kimlik doğrulama faktörleri tehlikeye saldırganlar için önemli bir sınama gösterir.</span><span class="sxs-lookup"><span data-stu-id="09dd7-106">Compromising multiple authentication factors presents a significant challenge for attackers.</span></span> <span data-ttu-id="09dd7-107">Bir saldırgan toolearn hello kullanıcının parolasını yönetir olsa bile, onu da hello güvenilir cihaz elinde gerek kalmadan gereksizdir.</span><span class="sxs-lookup"><span data-stu-id="09dd7-107">Even if an attacker manages toolearn hello user's password, it is useless without also having possession of hello trusted device.</span></span> 

![Proofup](./media/multi-factor-authentication-how-it-works/howitworks.png)

<span data-ttu-id="09dd7-109">Azure multi-Factor Authentication kullanıcı talebine basit bir oturum açma işlemi için buluştururken koruma erişim toodata ve uygulamaları yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="09dd7-109">Azure Multi-Factor Authentication helps safeguard access toodata and applications while meeting user demand for a simple sign-in process.</span></span>  <span data-ttu-id="09dd7-110">İkinci bir form kimlik doğrulama isteyerek ek güvenlik sağlar ve bir dizi kolay doğrulama seçeneklerini aracılığıyla güçlü kimlik doğrulaması sunar.</span><span class="sxs-lookup"><span data-stu-id="09dd7-110">It provides additional security by requiring a second form of authentication and delivers strong authentication via a range of easy verification options.</span></span>


## <a name="methods-available-for-two-step-verification"></a><span data-ttu-id="09dd7-111">İki aşamalı doğrulama için kullanılabilen yöntemler</span><span class="sxs-lookup"><span data-stu-id="09dd7-111">Methods available for two-step verification</span></span>
<span data-ttu-id="09dd7-112">Bir kullanıcı oturum açtığında ek doğrulama toohello kullanıcı gönderilir.</span><span class="sxs-lookup"><span data-stu-id="09dd7-112">When a user signs in, an additional verification is sent toohello user.</span></span>  <span data-ttu-id="09dd7-113">Merhaba, bu ikinci doğrulama için kullanılabilir yöntemlerin listesi verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="09dd7-113">hello following are a list of methods that can be used for this second verification.</span></span>

| <span data-ttu-id="09dd7-114">Doğrulama yöntemi</span><span class="sxs-lookup"><span data-stu-id="09dd7-114">Verification Method</span></span> | <span data-ttu-id="09dd7-115">Açıklama</span><span class="sxs-lookup"><span data-stu-id="09dd7-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="09dd7-116">Telefon araması</span><span class="sxs-lookup"><span data-stu-id="09dd7-116">Phone call</span></span> |<span data-ttu-id="09dd7-117">Çağrı tooa kullanıcının kayıtlı telefon yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="09dd7-117">A call is placed tooa user’s registered phone.</span></span> <span data-ttu-id="09dd7-118">Merhaba kullanıcı bir PIN gerekli olduğunda girer sonra hello # tuşuna basar.</span><span class="sxs-lookup"><span data-stu-id="09dd7-118">hello user enters a PIN if necessary then presses hello # key.</span></span> |
| <span data-ttu-id="09dd7-119">SMS mesajı</span><span class="sxs-lookup"><span data-stu-id="09dd7-119">Text message</span></span> |<span data-ttu-id="09dd7-120">Tooa kullanıcının cep telefonu altı rakamlı kodu içeren bir kısa mesaj gönderilir.</span><span class="sxs-lookup"><span data-stu-id="09dd7-120">A text message is sent tooa user’s mobile phone with a six-digit code.</span></span> <span data-ttu-id="09dd7-121">Merhaba kullanıcı oturum açma hello sayfasında bu kodu girer.</span><span class="sxs-lookup"><span data-stu-id="09dd7-121">hello user enters this code on hello sign-in page.</span></span> |
| <span data-ttu-id="09dd7-122">Mobil uygulama bildirimi</span><span class="sxs-lookup"><span data-stu-id="09dd7-122">Mobile app notification</span></span> |<span data-ttu-id="09dd7-123">Doğrulama isteği tooa kullanıcının Akıllı telefonu gönderilir.</span><span class="sxs-lookup"><span data-stu-id="09dd7-123">A verification request is sent tooa user’s smart phone.</span></span> <span data-ttu-id="09dd7-124">Merhaba kullanıcı bir PIN gerekli olduğunda girer sonra seçer **doğrula** hello mobil uygulama üzerinde.</span><span class="sxs-lookup"><span data-stu-id="09dd7-124">hello user enters a PIN if necessary then selects **Verify** on hello mobile app.</span></span> |
| <span data-ttu-id="09dd7-125">Mobil uygulama doğrulama kodu</span><span class="sxs-lookup"><span data-stu-id="09dd7-125">Mobile app verification code</span></span> |<span data-ttu-id="09dd7-126">bir kullanıcının Akıllı telefonu üzerinde çalıştığından, hello mobil uygulama değişiklikleri her 30 saniyede bir doğrulama kodu görüntüler.</span><span class="sxs-lookup"><span data-stu-id="09dd7-126">hello mobile app, which is running on a user’s smart phone, displays a verification code that changes every 30 seconds.</span></span> <span data-ttu-id="09dd7-127">Merhaba kullanıcı hello en son kod bulur ve oturum açma hello sayfasında girer.</span><span class="sxs-lookup"><span data-stu-id="09dd7-127">hello user finds hello most recent code and enters it on hello sign-in page.</span></span> |
| <span data-ttu-id="09dd7-128">Üçüncü taraf OATH belirteçleri</span><span class="sxs-lookup"><span data-stu-id="09dd7-128">Third-party OATH tokens</span></span> | <span data-ttu-id="09dd7-129">Azure multi-Factor Authentication Sunucusu'nda yapılandırılan tooaccept üçüncü taraf doğrulaması yöntemleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="09dd7-129">Azure Multi-Factor Authentication Server can be configured tooaccept third-party verification methods.</span></span> |

<span data-ttu-id="09dd7-130">Azure çok faktörlü kimlik doğrulaması, hem bulut hem de sunucu için seçilebilir doğrulama yöntemlerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="09dd7-130">Azure Multi-Factor Authentication provides selectable verification methods for both cloud and server.</span></span> <span data-ttu-id="09dd7-131">Hangi yöntemler, kullanıcılarınız için kullanılabilir seçebilirsiniz: telefon araması, metin, uygulama bildirimi veya uygulama kodları.</span><span class="sxs-lookup"><span data-stu-id="09dd7-131">You can choose which methods are available for your users: phone call, text, app notification, or app codes.</span></span> <span data-ttu-id="09dd7-132">Daha fazla bilgi için bkz: [seçilebilir doğrulama yöntemlerini](multi-factor-authentication-whats-next.md#selectable-verification-methods).</span><span class="sxs-lookup"><span data-stu-id="09dd7-132">For more information, see [selectable verification methods](multi-factor-authentication-whats-next.md#selectable-verification-methods).</span></span>

## <a name="next-steps"></a><span data-ttu-id="09dd7-133">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="09dd7-133">Next steps</span></span>

- <span data-ttu-id="09dd7-134">Merhaba farklı hakkında okuyun [sürümleri ve Azure çok faktörlü kimlik doğrulaması için tüketim yöntemi](multi-factor-authentication-versions-plans.md)</span><span class="sxs-lookup"><span data-stu-id="09dd7-134">Read about hello different [versions and consumption methods for Azure Multi-Factor Authentication](multi-factor-authentication-versions-plans.md)</span></span>

- <span data-ttu-id="09dd7-135">Seçin olup olmadığını toodeploy Azure MFA [hello Bulut veya şirket içi](multi-factor-authentication-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="09dd7-135">Choose whether toodeploy Azure MFA [in hello cloud or on-premises](multi-factor-authentication-get-started.md)</span></span>

- <span data-ttu-id="09dd7-136">Okuma yanıtlar için [sık sorulan sorular](multi-factor-authentication-faq.md)</span><span class="sxs-lookup"><span data-stu-id="09dd7-136">Read answers for [Frequently asked questions](multi-factor-authentication-faq.md)</span></span>