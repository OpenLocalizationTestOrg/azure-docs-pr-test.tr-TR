---
title: "aaaManage iki basamaklı doğrulama ayarlarınızı | Microsoft Docs"
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
ms.openlocfilehash: 2c974b08c584943f3c5a6b9bf16497d1706e8329
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-settings-for-two-step-verification"></a><span data-ttu-id="ddb14-104">İki aşamalı doğrulama için ayarlarınızı yönetme</span><span class="sxs-lookup"><span data-stu-id="ddb14-104">Manage your settings for two-step verification</span></span>
<span data-ttu-id="ddb14-105">Bu makalede nasıl hakkında sorular yanıtlanmaktadır iki aşamalı doğrulama veya çok faktörlü kimlik doğrulaması için tooupdate ayarlar.</span><span class="sxs-lookup"><span data-stu-id="ddb14-105">This article answers questions about how tooupdate settings for two-step verification or multi-factor authentication.</span></span> <span data-ttu-id="ddb14-106">Tooyour hesabında imzalama sorunları yaşıyorsanız, çok başvuran[iki aşamalı doğrulamayı sorununuz](multi-factor-authentication-end-user-troubleshoot.md) sorun giderme Yardımı.</span><span class="sxs-lookup"><span data-stu-id="ddb14-106">If you are having issues signing in tooyour account, refer too[Having trouble with two-step verification](multi-factor-authentication-end-user-troubleshoot.md) for troubleshooting help.</span></span>

## <a name="where-toofind-hello-settings-page"></a><span data-ttu-id="ddb14-107">Burada toofind hello Ayarları sayfası</span><span class="sxs-lookup"><span data-stu-id="ddb14-107">Where toofind hello settings page</span></span>
<span data-ttu-id="ddb14-108">Şirketiniz Azure çok faktörlü kimlik doğrulamasını nasıl ayarladığınıza bağlı olarak, ayarlarınızı telefon numaranız gibi değiştirebileceğiniz birkaç yer vardır.</span><span class="sxs-lookup"><span data-stu-id="ddb14-108">Depending on how your company set up Azure Multi-Factor Authentication, there are a few places where you can change your settings like your phone number.</span></span>

<span data-ttu-id="ddb14-109">BT yöneticiniz belirli URL veya adımları toomanage iki aşamalı doğrulamayı gönderirse, bu yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="ddb14-109">If your IT admin sent out a specific URL or steps toomanage two-step verification, follow those instructions.</span></span> <span data-ttu-id="ddb14-110">Aksi durumda, yönergeleri izleyerek hello herkes için çalışması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ddb14-110">Otherwise, hello following instructions should work for everybody else.</span></span> <span data-ttu-id="ddb14-111">Aşağıdaki adımları izleyin, ancak görmüyorum Merhaba, işiniz veya okulunuz kendi portal özelleştirilmiş anlamına aynı seçenekleri.</span><span class="sxs-lookup"><span data-stu-id="ddb14-111">If you follow these steps but don't see hello same options, that means that your work or school customized their own portal.</span></span> <span data-ttu-id="ddb14-112">Yöneticinizden hello bağlantı tooyour Azure çok faktörlü kimlik doğrulama portalı için isteyin.</span><span class="sxs-lookup"><span data-stu-id="ddb14-112">Ask your admin for hello link tooyour Azure Multi-Factor Authentication portal.</span></span>

1. <span data-ttu-id="ddb14-113">Çok oturum[https://myapps.microsoft.com](https://myapps.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="ddb14-113">Sign in too[https://myapps.microsoft.com](https://myapps.microsoft.com)</span></span>  
2. <span data-ttu-id="ddb14-114">Merhaba üst sağ hesap adınızı seçin, sonra seçin **profil**.</span><span class="sxs-lookup"><span data-stu-id="ddb14-114">Select your account name in hello top right, then select **profile**.</span></span>  
3. <span data-ttu-id="ddb14-115">Seçin **ek güvenlik doğrulaması**.</span><span class="sxs-lookup"><span data-stu-id="ddb14-115">Select **Additional security verification**.</span></span>  

    ![Myapps](./media/multi-factor-authentication-end-user-manage/myapps1.png)
4. <span data-ttu-id="ddb14-117">Merhaba ek güvenlik doğrulama sayfasında, ayarlarınızı ile yükler.</span><span class="sxs-lookup"><span data-stu-id="ddb14-117">hello Additional security verification page loads with your settings.</span></span>

    ![Proofup](./media/multi-factor-authentication-end-user-manage/proofup.png)

## <a name="i-want-toochange-my-phone-number-or-add-a-secondary-number"></a><span data-ttu-id="ddb14-119">I toochange Telefon numaramı istediğiniz veya ikincil bir sayı Ekle</span><span class="sxs-lookup"><span data-stu-id="ddb14-119">I want toochange my phone number, or add a secondary number</span></span>
<span data-ttu-id="ddb14-120">Önemli tooconfigure bir ikincil kimlik doğrulama telefon numarası olur.</span><span class="sxs-lookup"><span data-stu-id="ddb14-120">It is important tooconfigure a secondary authentication phone number.</span></span>  <span data-ttu-id="ddb14-121">Birincil telefon numarası ve mobil uygulamanızı çünkü olan büyük olasılıkla hello üzerinde aynı telefon, hello ikincil telefon numarası telefonunuz kaybolur veya çalınırsa mümkün tooget geri hesabınızda olacaktır hello tek yoludur.</span><span class="sxs-lookup"><span data-stu-id="ddb14-121">Because your primary phone number and your mobile app are probably on hello same phone, hello secondary phone number is hello only way you will be able tooget back into your account if your phone is lost or stolen.</span></span>

> [!NOTE]
> <span data-ttu-id="ddb14-122">Erişim tooyour birincil telefon numarası varsa ve tooyour hesabında başlarken yardıma gerek yoktur, bizim Yardım konularına bakın [iki aşamalı doğrulamayı sorununuz](multi-factor-authentication-end-user-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="ddb14-122">If you don't have access tooyour primary phone number, and need help getting in tooyour account, see our help topics in [Having trouble with two-step verification](multi-factor-authentication-end-user-troubleshoot.md).</span></span>  

<span data-ttu-id="ddb14-123">**toochange birincil telefon numarası:**</span><span class="sxs-lookup"><span data-stu-id="ddb14-123">**toochange your primary phone number:**</span></span>  

1. <span data-ttu-id="ddb14-124">Hello ek güvenlik doğrulama sayfasında, geçerli bir telefon numarası ile Merhaba metin kutusunu seçin ve yeni telefon numaranızı ile düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="ddb14-124">On hello Additional security verification page, select hello text box with your current phone number and edit it with your new phone number.</span></span>  
2. <span data-ttu-id="ddb14-125">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="ddb14-125">Select **Save**.</span></span>  
3. <span data-ttu-id="ddb14-126">Bu, tercih edilen doğrulama seçeneğini için kullandığınız hello sayı ise, kaydedebilmek için öncelikle tooverify hello yeni numarasına sahip.</span><span class="sxs-lookup"><span data-stu-id="ddb14-126">If this is hello number that you use for your preferred verification option, you have tooverify hello new number before you can save it.</span></span>  

<span data-ttu-id="ddb14-127">**tooadd ikincil bir telefon numarası:**</span><span class="sxs-lookup"><span data-stu-id="ddb14-127">**tooadd a secondary phone number:**</span></span>  

1. <span data-ttu-id="ddb14-128">Merhaba ek güvenlik doğrulama sayfasında hello sonraki çok onay kutusunu**alternatif kimlik doğrulaması telefon.**</span><span class="sxs-lookup"><span data-stu-id="ddb14-128">On hello Additional security verification page, check hello box next too**Alternate authentication phone.**</span></span>  
2. <span data-ttu-id="ddb14-129">İkincil telefon numaranızı hello metin kutusuna girin.</span><span class="sxs-lookup"><span data-stu-id="ddb14-129">Enter your secondary phone number in hello text box.</span></span>  
3. <span data-ttu-id="ddb14-130">Seçin **kaydetmek** ve değişikliklerinizi tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="ddb14-130">Select **Save** and your changes are finished.</span></span>  

## <a name="require-two-step-verification-again-on-a-device-youve-marked-as-trusted"></a><span data-ttu-id="ddb14-131">İki aşamalı doğrulamayı yeniden güvenilir olarak işaretledikten bir aygıt gerektirir</span><span class="sxs-lookup"><span data-stu-id="ddb14-131">Require two-step verification again on a device you've marked as trusted</span></span>

<span data-ttu-id="ddb14-132">Kuruluş ayarlarınıza bağlı olarak belirten bir onay kutusu olabilir "için sorma **X** gün" tarayıcınızdaki iki aşamalı doğrulama yapılırken.</span><span class="sxs-lookup"><span data-stu-id="ddb14-132">Depending on your organization settings, you may have a checkbox that says "Don't ask again for **X** days" when you perform two-step verification on your browser.</span></span> <span data-ttu-id="ddb14-133">Bu onay kutusunu işaretleyin ve Cihazınızı kaybeder veya hesabınızın güvenliği ihlal olduğunu düşündüğünüz iki aşamalı doğrulama tooall aygıtlarınızı geri yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ddb14-133">If you check this box and then lose your device or think that your account is compromised, you should restore two-step verification tooall your devices.</span></span> 

1. <span data-ttu-id="ddb14-134">Merhaba ek güvenlik doğrulama sayfasında, seçin **önceden güvenilen cihazlara geri yükleme çok faktörlü kimlik doğrulaması**.</span><span class="sxs-lookup"><span data-stu-id="ddb14-134">On hello Additional security verification page, select **Restore multi-factor authentication on previously trusted devices**.</span></span>
2. <span data-ttu-id="ddb14-135">Merhaba herhangi bir cihazda oturum açtığınızda, istendiğinde tooperform iki aşamalı doğrulamayı olmanız.</span><span class="sxs-lookup"><span data-stu-id="ddb14-135">hello next time you sign in on any device, you'll be prompted tooperform two-step verification.</span></span> 

## <a name="how-do-i-clean-up-microsoft-authenticator-from-my-old-device-and-move-tooa-new-one"></a><span data-ttu-id="ddb14-136">Nasıl eski aygıttan Microsoft Authenticator temizlemek ve tooa yeni bir taşıma?</span><span class="sxs-lookup"><span data-stu-id="ddb14-136">How do I clean up Microsoft Authenticator from my old device and move tooa new one?</span></span>
<span data-ttu-id="ddb14-137">Aygıt ya da sıfırlama hello aygıt hello uygulamasını kaldırdığınızda hello etkinleştirme hello arka uçtaki kaldırmaz.</span><span class="sxs-lookup"><span data-stu-id="ddb14-137">When you uninstall hello app from your device or reset hello device, it does not remove hello activation on hello back end.</span></span> <span data-ttu-id="ddb14-138">Daha fazla bilgi için bkz: [Microsoft Authenticator](microsoft-authenticator-app-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="ddb14-138">For more information, see [Microsoft Authenticator](microsoft-authenticator-app-how-to.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ddb14-139">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ddb14-139">Next steps</span></span>
* <span data-ttu-id="ddb14-140">Sorun giderme ipuçları alın ve Yardım [iki aşamalı doğrulamayı sorununuz](multi-factor-authentication-end-user-troubleshoot.md)</span><span class="sxs-lookup"><span data-stu-id="ddb14-140">Get troubleshooting tips and help on [Having trouble with two-step verification](multi-factor-authentication-end-user-troubleshoot.md)</span></span>
* <span data-ttu-id="ddb14-141">Ayarlanan [uygulama parolaları](multi-factor-authentication-end-user-app-passwords.md) iki aşamalı doğrulamayı desteklemeyen uygulamalar için.</span><span class="sxs-lookup"><span data-stu-id="ddb14-141">Set up [app passwords](multi-factor-authentication-end-user-app-passwords.md) for any apps that don't support two-step verification.</span></span>
