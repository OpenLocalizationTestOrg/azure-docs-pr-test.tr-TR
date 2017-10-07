---
title: "aaaAzure MFA oturum açma ile iki aşamalı doğrulama | Microsoft Docs"
description: "Bu sayfa, burada toogo toosee hello oturum açma Azure MFA ile kullanılabilen yöntemleri hakkında kılavuzluk sağlar."
keywords: "Kullanıcı kimlik doğrulaması, oturum açma deneyimi, cep telefonu ile oturum aç ofis telefonu ile oturum açma"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: b310b762-471b-4b26-887a-a321c9e81d46
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/02/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: end-user
ms.openlocfilehash: fcd5eb5e8426eda537db9e099bf247bde29c195b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="hello-sign-in-experience-with-azure-multi-factor-authentication"></a><span data-ttu-id="4081f-104">Azure multi-Factor Authentication ile Merhaba oturum açma deneyimi</span><span class="sxs-lookup"><span data-stu-id="4081f-104">hello sign-in experience with Azure Multi-Factor Authentication</span></span>
> [!NOTE]
> <span data-ttu-id="4081f-105">Bu makalede Hello amacı tipik bir oturum açma deneyimi aracılığıyla toowalk budur.</span><span class="sxs-lookup"><span data-stu-id="4081f-105">hello purpose of this article is toowalk through a typical sign-in experience.</span></span> <span data-ttu-id="4081f-106">Oturum açma veya tootroubleshoot sorunları ile ilgili Yardım için bkz [Azure multi-Factor Authentication sorununuz](multi-factor-authentication-end-user-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="4081f-106">For help with signing in, or tootroubleshoot problems, see [Having trouble with Azure Multi-Factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).</span></span>

## <a name="what-will-your-sign-in-experience-be"></a><span data-ttu-id="4081f-107">Oturum açma deneyimini ne olacak?</span><span class="sxs-lookup"><span data-stu-id="4081f-107">What will your sign-in experience be?</span></span>
<span data-ttu-id="4081f-108">Oturum açma deneyimini toouse ikinci faktörü olarak seçtiğiniz öğeye bağlı olarak farklılık gösterir: telefon araması, bir kimlik doğrulama uygulaması veya metinleri.</span><span class="sxs-lookup"><span data-stu-id="4081f-108">Your sign-in experience differs depending on what you choose toouse as your second factor: a phone call, an authentication app, or texts.</span></span> <span data-ttu-id="4081f-109">En iyi ne yaptığınızı açıklayan hello seçenek belirleyin:</span><span class="sxs-lookup"><span data-stu-id="4081f-109">Choose hello option that best describes what you are doing:</span></span>

| <span data-ttu-id="4081f-110">Nasıl oturum?</span><span class="sxs-lookup"><span data-stu-id="4081f-110">How do you sign in?</span></span> | 
| --- |
| [<span data-ttu-id="4081f-111">Olan bir telefon araması toomy cep telefonu numarası veya office telefon</span><span class="sxs-lookup"><span data-stu-id="4081f-111">With a phone call toomy mobile or office phone</span></span>](#signing-in-with-a-phone-call) |
| [<span data-ttu-id="4081f-112">Metin toomy cep telefonuyla</span><span class="sxs-lookup"><span data-stu-id="4081f-112">With a text toomy mobile phone</span></span>](#signing-in-with-a-text-message)
| [<span data-ttu-id="4081f-113">Merhaba Microsoft Authenticator uygulaması ile bildirim</span><span class="sxs-lookup"><span data-stu-id="4081f-113">With notifications from hello Microsoft Authenticator app</span></span>](#signing-in-with-the-microsoft-authenticator-app-using-notification) |
| [<span data-ttu-id="4081f-114">Merhaba Microsoft Authenticator uygulaması ile doğrulama kodları</span><span class="sxs-lookup"><span data-stu-id="4081f-114">With verification codes from hello Microsoft Authenticator app</span></span>](#signing-in-with-the-microsoft-authenticator-app-using-verification-code) |
| [<span data-ttu-id="4081f-115">Alternatif bir yöntem ile my tercih edilen yöntem şu anda kullanamazsınız çünkü</span><span class="sxs-lookup"><span data-stu-id="4081f-115">With an alternate method, because I can't use my preferred method right now</span></span>](#signing-in-with-an-alternate-method) |

## <a name="signing-in-with-a-phone-call"></a><span data-ttu-id="4081f-116">Bir telefon araması oturum imzalama</span><span class="sxs-lookup"><span data-stu-id="4081f-116">Signing in with a phone call</span></span>
<span data-ttu-id="4081f-117">Aşağıdaki bilgilerle hello hello iki aşamalı doğrulama deneyimi bir çağrı tooyour mobil veya ofis telefonu açıklar.</span><span class="sxs-lookup"><span data-stu-id="4081f-117">hello following information describes hello two-step verification experience with a call tooyour mobile or office phone.</span></span>

1. <span data-ttu-id="4081f-118">Tooan uygulama veya kullanıcı adı ve parola kullanarak Office 365 gibi hizmetinde oturum açın.</span><span class="sxs-lookup"><span data-stu-id="4081f-118">Sign in tooan application or service such as Office 365 using your username and password.</span></span>  
2. <span data-ttu-id="4081f-119">Microsoft, çağırır.</span><span class="sxs-lookup"><span data-stu-id="4081f-119">Microsoft calls you.</span></span>  
3. <span data-ttu-id="4081f-120">Merhaba telefona yanıt verin ve hello # tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="4081f-120">Answer hello phone and hit hello # key.</span></span>  

## <a name="signing-in-with-a-text-message"></a><span data-ttu-id="4081f-121">SMS mesajı oturum imzalama</span><span class="sxs-lookup"><span data-stu-id="4081f-121">Signing in with a text message</span></span>
<span data-ttu-id="4081f-122">Aşağıdaki bilgilerle hello hello iki aşamalı doğrulama metin iletisi tooyour cep telefonu deneyimiyle açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="4081f-122">hello following information describes hello two-step verification experience with a text message tooyour mobile phone:</span></span>

1. <span data-ttu-id="4081f-123">Tooan uygulama veya kullanıcı adı ve parola kullanarak Office 365 gibi hizmetinde oturum açın.</span><span class="sxs-lookup"><span data-stu-id="4081f-123">Sign in tooan application or service such as Office 365 using your username and password.</span></span> 
2. <span data-ttu-id="4081f-124">Microsoft bir numara kodu içeren bir kısa mesaj gönderir.</span><span class="sxs-lookup"><span data-stu-id="4081f-124">Microsoft sends you a text message that contains a number code.</span></span> 
3. <span data-ttu-id="4081f-125">Oturum açma hello sayfada sağlanan hello kutusuna Hello kodu girin.</span><span class="sxs-lookup"><span data-stu-id="4081f-125">Enter hello code in hello box provided on hello sign-in page.</span></span> 

## <a name="signing-in-with-hello-microsoft-authenticator-app"></a><span data-ttu-id="4081f-126">Merhaba Microsoft Authenticator uygulama ile oturum açılmasını</span><span class="sxs-lookup"><span data-stu-id="4081f-126">Signing in with hello Microsoft Authenticator app</span></span> 
<span data-ttu-id="4081f-127">Merhaba aşağıdaki bilgiler için iki aşamalı Doğrulamalar hello Microsoft Authenticator uygulaması kullanılarak hello deneyimi açıklar.</span><span class="sxs-lookup"><span data-stu-id="4081f-127">hello following information describes hello experience of using hello Microsoft Authenticator app for two-step verifications.</span></span> <span data-ttu-id="4081f-128">İki farklı şekilde toouse hello uygulama vardır.</span><span class="sxs-lookup"><span data-stu-id="4081f-128">There are two different ways toouse hello app.</span></span> <span data-ttu-id="4081f-129">Cihazınızda anında iletme bildirimleri alabilir veya hello uygulama tooget bir doğrulama kodu açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4081f-129">You can receive push notifications on your device, or you can open hello app tooget a verification code.</span></span>

### <a name="toosign-in-with-a-notification-from-hello-microsoft-authenticator-app"></a><span data-ttu-id="4081f-130">bir bildirim hello Microsoft Authenticator uygulamadan oturum toosign</span><span class="sxs-lookup"><span data-stu-id="4081f-130">toosign in with a notification from hello Microsoft Authenticator app</span></span>
1. <span data-ttu-id="4081f-131">Tooan uygulama veya kullanıcı adı ve parola kullanarak Office 365 gibi hizmetinde oturum açın.</span><span class="sxs-lookup"><span data-stu-id="4081f-131">Sign in tooan application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="4081f-132">Microsoft, Cihazınızda bir bildirim toohello Microsoft Authenticator uygulaması gönderir.</span><span class="sxs-lookup"><span data-stu-id="4081f-132">Microsoft sends a notification toohello Microsoft Authenticator app on your device.</span></span>

  ![Microsoft bildirim gönderir](./media/multi-factor-authentication-end-user-signin/notify.png)

3. <span data-ttu-id="4081f-134">Telefon ve select hello açık hello bildirim **doğrula** anahtarı.</span><span class="sxs-lookup"><span data-stu-id="4081f-134">Open hello notification on your phone and select hello **Verify** key.</span></span> <span data-ttu-id="4081f-135">Şirketiniz bir PIN gerektiriyorsa, buraya girin.</span><span class="sxs-lookup"><span data-stu-id="4081f-135">If your company requires a PIN, enter it here.</span></span>
4. <span data-ttu-id="4081f-136">Artık oturum açmanız.</span><span class="sxs-lookup"><span data-stu-id="4081f-136">You should now be signed in.</span></span>

### <a name="toosign-in-using-a-verification-code-with-hello-microsoft-authenticator-app"></a><span data-ttu-id="4081f-137">Merhaba Microsoft Authenticator uygulamasıyla doğrulama kodunu kullanarak toosign</span><span class="sxs-lookup"><span data-stu-id="4081f-137">toosign in using a verification code with hello Microsoft Authenticator app</span></span>

<span data-ttu-id="4081f-138">Merhaba Microsoft Authenticator uygulama tooget doğrulama kodları kullanırsanız, hello uygulamasını açın, sonra bir sayı, hesap adı altında görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="4081f-138">If you use hello Microsoft Authenticator app tooget verification codes, then when you open hello app you see a number under your account name.</span></span> <span data-ttu-id="4081f-139">Bu sayı her 30 saniyede değiştirir, böylece aynı iki kez sayı hello kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="4081f-139">This number changes every 30 seconds so that you don't use hello same number twice.</span></span> <span data-ttu-id="4081f-140">İçin bir doğrulama kodu sorulduğunda, hello uygulamasını açın ve sayıyı görüntülenmekte kullanın.</span><span class="sxs-lookup"><span data-stu-id="4081f-140">When you're asked for a verification code, open hello app and use whatever number is currently displayed.</span></span> 

1. <span data-ttu-id="4081f-141">Tooan uygulama veya kullanıcı adı ve parola kullanarak Office 365 gibi hizmetinde oturum açın.</span><span class="sxs-lookup"><span data-stu-id="4081f-141">Sign in tooan application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="4081f-142">Microsoft için bir doğrulama kodu ister.</span><span class="sxs-lookup"><span data-stu-id="4081f-142">Microsoft prompts you for a verification code.</span></span>

  ![Doğrulama kodunu girin](./media/multi-factor-authentication-end-user-signin/verify3.png)

3. <span data-ttu-id="4081f-144">Telefonunuz Hello Microsoft Authenticator uygulamasını açın ve burada oturum hello kutusunda hello kodu girin.</span><span class="sxs-lookup"><span data-stu-id="4081f-144">Open hello Microsoft Authenticator app on your phone and enter hello code in hello box where you are signing in.</span></span>

## <a name="signing-in-with-an-alternate-method"></a><span data-ttu-id="4081f-145">Alternatif bir yöntem ile imzalama</span><span class="sxs-lookup"><span data-stu-id="4081f-145">Signing in with an alternate method</span></span>
<span data-ttu-id="4081f-146">Bazen hello telefon veya tercih edilen doğrulama yöntemi olarak ayarladığınız cihaz yok.</span><span class="sxs-lookup"><span data-stu-id="4081f-146">Sometimes you don't have hello phone or device that you set up as your preferred verification method.</span></span> <span data-ttu-id="4081f-147">Hesabınız için yedekleme yöntemleri ayarlamak öneririz neden bu durumda.</span><span class="sxs-lookup"><span data-stu-id="4081f-147">This situation is why we recommend that you set up backup methods for your account.</span></span> <span data-ttu-id="4081f-148">Merhaba aşağıdaki bölümde, nasıl gösterilir birincil yönteminiz kullanılamayabilir, alternatif bir yöntem oturum toosign.</span><span class="sxs-lookup"><span data-stu-id="4081f-148">hello following section shows you how toosign in with an alternate method when your primary method may not be available.</span></span>

1. <span data-ttu-id="4081f-149">Tooan uygulama veya kullanıcı adı ve parola kullanarak Office 365 gibi hizmetinde oturum açın.</span><span class="sxs-lookup"><span data-stu-id="4081f-149">Sign in tooan application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="4081f-150">Seçin **farklı bir doğrulama seçeneği kullanma**.</span><span class="sxs-lookup"><span data-stu-id="4081f-150">Select **Use a different verification option**.</span></span> <span data-ttu-id="4081f-151">Kaç tane Kurulum sahip bağlı olarak farklı bir doğrulama seçeneklerini bakın.</span><span class="sxs-lookup"><span data-stu-id="4081f-151">You see different verification options based on how many you have setup.</span></span>
3. <span data-ttu-id="4081f-152">Alternatif bir yöntem seçin ve oturum açın.</span><span class="sxs-lookup"><span data-stu-id="4081f-152">Choose an alternate method and sign in.</span></span>

  ![Alternatif yöntemi kullanın.](./media/multi-factor-authentication-end-user-signin/alt.png)

## <a name="next-steps"></a><span data-ttu-id="4081f-154">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4081f-154">Next steps</span></span>

<span data-ttu-id="4081f-155">İki aşamalı doğrulamayı oturum imzalama sorunlarınız varsa, daha fazla bilgi almak [Azure multi-Factor Authentication sorununuz](multi-factor-authentication-end-user-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="4081f-155">If you have problems signing in with two-step verification, get more information at [Having trouble with Azure Multi-Factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).</span></span>

<span data-ttu-id="4081f-156">Nasıl çok öğrenin[iki basamaklı doğrulama ayarlarınızı yönetme](multi-factor-authentication-end-user-manage-settings.md).</span><span class="sxs-lookup"><span data-stu-id="4081f-156">Learn how too[Manage your two-step verification settings](multi-factor-authentication-end-user-manage-settings.md).</span></span>

<span data-ttu-id="4081f-157">Çok öğrenin[hello Microsoft Authenticator uygulaması ile çalışmaya başlama](microsoft-authenticator-app-how-to.md) böylece bildirimleri toosign, metinleri ve telefon aramaları yerine kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4081f-157">Find out how too[Get started with hello Microsoft Authenticator app](microsoft-authenticator-app-how-to.md) so that you can use notifications toosign in, instead of texts and phone calls.</span></span> 
