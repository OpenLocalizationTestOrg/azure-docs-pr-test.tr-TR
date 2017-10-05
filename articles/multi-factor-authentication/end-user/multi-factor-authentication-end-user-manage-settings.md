---
title: "İki basamaklı doğrulama ayarlarınızı yönetme | Microsoft Docs"
description: "İletişim bilgilerinizi değiştirmek veya aygıtlarınızı yapılandırma dahil olmak üzere Azure multi-Factor Authentication kullanımını yönetin."
services: multi-factor-authentication
keywords: "çok faktörlü kimlik doğrulama istemcisi, kimlik doğrulama sorunu bağıntı kimliği"
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: d3372d9a-9ad1-4609-bdcf-2c4ca9679a3b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: kgremban
ms.custom: end-user
ms.openlocfilehash: f752fb19e4ff2f831d50104e9c7d5f42cc3486d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-your-settings-for-two-step-verification"></a><span data-ttu-id="8bdff-104">İki aşamalı doğrulama için ayarlarınızı yönetme</span><span class="sxs-lookup"><span data-stu-id="8bdff-104">Manage your settings for two-step verification</span></span>
<span data-ttu-id="8bdff-105">Bu makalede, iki aşamalı doğrulama veya çok faktörlü kimlik doğrulama ayarlarını güncelleştirme hakkında sorular yanıtlanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="8bdff-105">This article answers questions about how to update settings for two-step verification or multi-factor authentication.</span></span> <span data-ttu-id="8bdff-106">Hesabınızda oturum açma sorunu yaşıyor oluştuysa, [iki aşamalı doğrulamayı sorununuz](multi-factor-authentication-end-user-troubleshoot.md) sorun giderme Yardımı.</span><span class="sxs-lookup"><span data-stu-id="8bdff-106">If you are having issues signing in to your account, refer to [Having trouble with two-step verification](multi-factor-authentication-end-user-troubleshoot.md) for troubleshooting help.</span></span>

## <a name="where-to-find-the-settings-page"></a><span data-ttu-id="8bdff-107">Nerede Ayarları sayfası</span><span class="sxs-lookup"><span data-stu-id="8bdff-107">Where to find the settings page</span></span>
<span data-ttu-id="8bdff-108">Şirketiniz Azure çok faktörlü kimlik doğrulamasını nasıl ayarladığınıza bağlı olarak, ayarlarınızı telefon numaranız gibi değiştirebileceğiniz birkaç yer vardır.</span><span class="sxs-lookup"><span data-stu-id="8bdff-108">Depending on how your company set up Azure Multi-Factor Authentication, there are a few places where you can change your settings like your phone number.</span></span>

<span data-ttu-id="8bdff-109">İki aşamalı doğrulamayı yönetmek için belirli bir URL veya adımları BT yöneticinize gönderilen bu yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="8bdff-109">If your IT admin sent out a specific URL or steps to manage two-step verification, follow those instructions.</span></span> <span data-ttu-id="8bdff-110">Aksi takdirde, aşağıdaki yönergeleri herkes için çalışması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8bdff-110">Otherwise, the following instructions should work for everybody else.</span></span> <span data-ttu-id="8bdff-111">Aşağıdaki adımları izleyin, ancak aynı seçenekleri göremiyorsanız, işiniz veya okulunuz kendi portal özelleştirilmiş anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="8bdff-111">If you follow these steps but don't see the same options, that means that your work or school customized their own portal.</span></span> <span data-ttu-id="8bdff-112">Bağlantı Azure multi-Factor Authentication portalınız için yöneticinize başvurun.</span><span class="sxs-lookup"><span data-stu-id="8bdff-112">Ask your admin for the link to your Azure Multi-Factor Authentication portal.</span></span>

1. <span data-ttu-id="8bdff-113">Oturum [https://myapps.microsoft.com](https://myapps.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="8bdff-113">Sign in to [https://myapps.microsoft.com](https://myapps.microsoft.com)</span></span>  
2. <span data-ttu-id="8bdff-114">Sağ üst hesap adınızı seçin, sonra seçin **profil**.</span><span class="sxs-lookup"><span data-stu-id="8bdff-114">Select your account name in the top right, then select **profile**.</span></span>  
3. <span data-ttu-id="8bdff-115">Seçin **ek güvenlik doğrulaması**.</span><span class="sxs-lookup"><span data-stu-id="8bdff-115">Select **Additional security verification**.</span></span>  

    ![Myapps](./media/multi-factor-authentication-end-user-manage/myapps1.png)
4. <span data-ttu-id="8bdff-117">Ek güvenlik doğrulama sayfasında, ayarlarınızı ile yükler.</span><span class="sxs-lookup"><span data-stu-id="8bdff-117">The Additional security verification page loads with your settings.</span></span>

    ![Proofup](./media/multi-factor-authentication-end-user-manage/proofup.png)

## <a name="i-want-to-change-my-phone-number-or-add-a-secondary-number"></a><span data-ttu-id="8bdff-119">Telefon numaramı değiştirmek veya ikincil bir sayı eklemek istiyorum</span><span class="sxs-lookup"><span data-stu-id="8bdff-119">I want to change my phone number, or add a secondary number</span></span>
<span data-ttu-id="8bdff-120">İkincil kimlik doğrulama telefon numaranızı yapılandırılması önemlidir.</span><span class="sxs-lookup"><span data-stu-id="8bdff-120">It is important to configure a secondary authentication phone number.</span></span>  <span data-ttu-id="8bdff-121">Birincil telefon numaranızı ve mobil uygulamanızı büyük olasılıkla aynı telefonda olduğundan, ikincil bir telefon numarası telefonunuz kaybolur veya çalınırsa hesabınızda geri alma kuramaz tek yoludur.</span><span class="sxs-lookup"><span data-stu-id="8bdff-121">Because your primary phone number and your mobile app are probably on the same phone, the secondary phone number is the only way you will be able to get back into your account if your phone is lost or stolen.</span></span>

> [!NOTE]
> <span data-ttu-id="8bdff-122">Erişim birincil telefon numaranız varsa ve hesabınıza başlarken yardıma gerek yoktur, bizim Yardım konularına bakın [iki aşamalı doğrulamayı sorununuz](multi-factor-authentication-end-user-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="8bdff-122">If you don't have access to your primary phone number, and need help getting in to your account, see our help topics in [Having trouble with two-step verification](multi-factor-authentication-end-user-troubleshoot.md).</span></span>  

<span data-ttu-id="8bdff-123">**Birincil telefon numaranızı değiştirmek için:**</span><span class="sxs-lookup"><span data-stu-id="8bdff-123">**To change your primary phone number:**</span></span>  

1. <span data-ttu-id="8bdff-124">Ek güvenlik doğrulama sayfasında, geçerli bir telefon numarası metin kutusunu seçin ve yeni telefon numaranızı ile düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="8bdff-124">On the Additional security verification page, select the text box with your current phone number and edit it with your new phone number.</span></span>  
2. <span data-ttu-id="8bdff-125">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="8bdff-125">Select **Save**.</span></span>  
3. <span data-ttu-id="8bdff-126">Bu, tercih edilen doğrulama seçeneğini için kullandığınız sayı ise, kaydedebilmek için öncelikle yeni numarayı doğrulamak gerekir.</span><span class="sxs-lookup"><span data-stu-id="8bdff-126">If this is the number that you use for your preferred verification option, you have to verify the new number before you can save it.</span></span>  

<span data-ttu-id="8bdff-127">**İkincil bir telefon numarası eklemek için:**</span><span class="sxs-lookup"><span data-stu-id="8bdff-127">**To add a secondary phone number:**</span></span>  

1. <span data-ttu-id="8bdff-128">Ek güvenlik doğrulama sayfasında yanındaki kutuyu işaretleyin **alternatif kimlik doğrulaması telefon.**</span><span class="sxs-lookup"><span data-stu-id="8bdff-128">On the Additional security verification page, check the box next to **Alternate authentication phone.**</span></span>  
2. <span data-ttu-id="8bdff-129">İkincil telefon numaranızı metin kutusuna girin.</span><span class="sxs-lookup"><span data-stu-id="8bdff-129">Enter your secondary phone number in the text box.</span></span>  
3. <span data-ttu-id="8bdff-130">Seçin **kaydetmek** ve değişikliklerinizi tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="8bdff-130">Select **Save** and your changes are finished.</span></span>  

## <a name="require-two-step-verification-again-on-a-device-youve-marked-as-trusted"></a><span data-ttu-id="8bdff-131">İki aşamalı doğrulamayı yeniden güvenilir olarak işaretledikten bir aygıt gerektirir</span><span class="sxs-lookup"><span data-stu-id="8bdff-131">Require two-step verification again on a device you've marked as trusted</span></span>

<span data-ttu-id="8bdff-132">Kuruluş ayarlarınıza bağlı olarak belirten bir onay kutusu olabilir "için sorma **X** gün" tarayıcınızdaki iki aşamalı doğrulama yapılırken.</span><span class="sxs-lookup"><span data-stu-id="8bdff-132">Depending on your organization settings, you may have a checkbox that says "Don't ask again for **X** days" when you perform two-step verification on your browser.</span></span> <span data-ttu-id="8bdff-133">Bu onay kutusunu işaretleyin ve Cihazınızı kaybeder veya hesabınızın güvenliği ihlal olduğunu düşündüğünüz tüm cihazlarınıza iki aşamalı doğrulama geri yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8bdff-133">If you check this box and then lose your device or think that your account is compromised, you should restore two-step verification to all your devices.</span></span> 

1. <span data-ttu-id="8bdff-134">Ek güvenlik doğrulama sayfasında, seçin **önceden güvenilen cihazlara geri yükleme çok faktörlü kimlik doğrulaması**.</span><span class="sxs-lookup"><span data-stu-id="8bdff-134">On the Additional security verification page, select **Restore multi-factor authentication on previously trusted devices**.</span></span>
2. <span data-ttu-id="8bdff-135">Herhangi bir cihazda oturum açtığınızda iki aşamalı doğrulamayı gerçekleştirmek için istenir.</span><span class="sxs-lookup"><span data-stu-id="8bdff-135">The next time you sign in on any device, you'll be prompted to perform two-step verification.</span></span> 

## <a name="how-do-i-clean-up-microsoft-authenticator-from-my-old-device-and-move-to-a-new-one"></a><span data-ttu-id="8bdff-136">Nasıl eski aygıttan Microsoft Authenticator temizlemek ve yeni bir taşıma?</span><span class="sxs-lookup"><span data-stu-id="8bdff-136">How do I clean up Microsoft Authenticator from my old device and move to a new one?</span></span>
<span data-ttu-id="8bdff-137">Uygulamasını cihazınızdan kaldırdığınızda veya cihaz sıfırlama etkinleştirme arka uçtaki kaldırmaz.</span><span class="sxs-lookup"><span data-stu-id="8bdff-137">When you uninstall the app from your device or reset the device, it does not remove the activation on the back end.</span></span> <span data-ttu-id="8bdff-138">Daha fazla bilgi için bkz: [Microsoft Authenticator](microsoft-authenticator-app-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="8bdff-138">For more information, see [Microsoft Authenticator](microsoft-authenticator-app-how-to.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8bdff-139">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8bdff-139">Next steps</span></span>
* <span data-ttu-id="8bdff-140">Sorun giderme ipuçları alın ve Yardım [iki aşamalı doğrulamayı sorununuz](multi-factor-authentication-end-user-troubleshoot.md)</span><span class="sxs-lookup"><span data-stu-id="8bdff-140">Get troubleshooting tips and help on [Having trouble with two-step verification](multi-factor-authentication-end-user-troubleshoot.md)</span></span>
* <span data-ttu-id="8bdff-141">Ayarlanan [uygulama parolaları](multi-factor-authentication-end-user-app-passwords.md) iki aşamalı doğrulamayı desteklemeyen uygulamalar için.</span><span class="sxs-lookup"><span data-stu-id="8bdff-141">Set up [app passwords](multi-factor-authentication-end-user-app-passwords.md) for any apps that don't support two-step verification.</span></span>
