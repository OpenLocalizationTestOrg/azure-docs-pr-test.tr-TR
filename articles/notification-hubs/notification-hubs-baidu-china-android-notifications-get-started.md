---
title: "aaaGet Baidu kullanarak Azure Notification Hubs ile çalışmaya | Microsoft Docs"
description: "Bu öğreticide, bilgi nasıl Baidu kullanarak toouse Azure Notification Hubs toopush bildirimleri tooAndroid cihazları."
services: notification-hubs
documentationcenter: android
author: ysxu
manager: erikre
editor: 
ms.assetid: 23bde1ea-f978-43b2-9eeb-bfd7b9edc4c1
ms.service: notification-hubs
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: mobile-baidu
ms.workload: mobile
ms.date: 08/19/2016
ms.author: yuaxu
ms.openlocfilehash: 2767fdd3bb04674e7a531634237cc05cd8c21cb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-notification-hubs-using-baidu"></a><span data-ttu-id="503f0-103">Baidu kullanarak Azure Notification Hubs ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="503f0-103">Get started with Notification Hubs using Baidu</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="503f0-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="503f0-104">Overview</span></span>
<span data-ttu-id="503f0-105">Baidu bulut anında iletme toosend anında iletme bildirimleri toomobile aygıtları kullanabileceğiniz bir Çin bulut hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="503f0-105">Baidu cloud push is a Chinese cloud service that you can use toosend push notifications toomobile devices.</span></span> <span data-ttu-id="503f0-106">Bu hizmet, burada tooAndroid hello varlığını farklı uygulama mağazalarının ve anında iletme nedeniyle karmaşıktır anında iletme bildirimleri teslim hizmetleri, ayrıca genellikle bağlı tooGCM (Google olmayan Android cihazları toohello kullanılabilirliğini Çin'de yararlıdır Mesajlaşma bulut).</span><span class="sxs-lookup"><span data-stu-id="503f0-106">This service is useful in China, where delivering push notifications tooAndroid is complex because of hello presence of different app stores and push services, in addition toohello availability of Android devices that are not typically connected tooGCM (Google Cloud Messaging).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="503f0-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="503f0-107">Prerequisites</span></span>
<span data-ttu-id="503f0-108">Bu öğretici için aşağıdakiler gereklidir:</span><span class="sxs-lookup"><span data-stu-id="503f0-108">This tutorial requires:</span></span>

* <span data-ttu-id="503f0-109">Hello karşıdan yükleyebileceğiniz, (varsayıyoruz Eclipse kullanın) android SDK <a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android sitesi</a></span><span class="sxs-lookup"><span data-stu-id="503f0-109">Android SDK (we assume that you use Eclipse), which you can download from hello <a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android site</a></span></span>
* <span data-ttu-id="503f0-110">[Mobile Services Android SDK'sı]</span><span class="sxs-lookup"><span data-stu-id="503f0-110">[Mobile Services Android SDK]</span></span>
* <span data-ttu-id="503f0-111">[Baidu anında iletme Android SDK]</span><span class="sxs-lookup"><span data-stu-id="503f0-111">[Baidu Push Android SDK]</span></span>

> [!NOTE]
> <span data-ttu-id="503f0-112">toocomplete Bu öğretici, etkin bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="503f0-112">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="503f0-113">Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="503f0-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="503f0-114">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-baidu-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="503f0-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-baidu-get-started%2F).</span></span>
> 
> 

## <a name="create-a-baidu-account"></a><span data-ttu-id="503f0-115">Bir Baidu hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="503f0-115">Create a Baidu account</span></span>
<span data-ttu-id="503f0-116">Baidu toouse, bir Baidu hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="503f0-116">toouse Baidu, you must have a Baidu account.</span></span> <span data-ttu-id="503f0-117">Zaten varsa, toohello içinde oturum [Baidu portalında] ve toohello bir sonraki adımı atlayın.</span><span class="sxs-lookup"><span data-stu-id="503f0-117">If you already have one, log in toohello [Baidu portal] and skip toohello next step.</span></span> <span data-ttu-id="503f0-118">Aksi takdirde hakkında yönergeleri izleyerek hello bkz toocreate bir Baidu hesabı.</span><span class="sxs-lookup"><span data-stu-id="503f0-118">Otherwise, see hello following instructions on how toocreate a Baidu account.</span></span>  

1. <span data-ttu-id="503f0-119">Toohello Git [Baidu portalında] hello tıklatıp**登录**(**oturum açma**) bağlantı.</span><span class="sxs-lookup"><span data-stu-id="503f0-119">Go toohello [Baidu portal] and click hello **登录** (**Login**) link.</span></span> <span data-ttu-id="503f0-120">Tıklatın**立即注册**toostart hello hesap kayıt işlemi.</span><span class="sxs-lookup"><span data-stu-id="503f0-120">Click **立即注册** toostart hello account registration process.</span></span>
   
   ![][1]
2. <span data-ttu-id="503f0-121">Merhaba gerekli ayrıntıları girin: telefon/e-posta adresi, parola ve doğrulama kodu — tıklatıp **kaydolma**.</span><span class="sxs-lookup"><span data-stu-id="503f0-121">Enter hello required details—phone/email address, password, and verification code—and click **Signup**.</span></span>
   
   ![][2]
3. <span data-ttu-id="503f0-122">Bir e-posta toohello e-posta adresine gönderilecek bir bağlantı tooactivate ile Baidu hesabınızı girilen.</span><span class="sxs-lookup"><span data-stu-id="503f0-122">You will be sent an email toohello email address that you entered with a link tooactivate your Baidu account.</span></span>
   
   ![][3]
4. <span data-ttu-id="503f0-123">Tooyour e-posta hesabında oturum, hello Baidu etkinleştirme posta açın ve Baidu hesabınızı hello etkinleştirme bağlantı tooactivate tıklatın.</span><span class="sxs-lookup"><span data-stu-id="503f0-123">Log in tooyour email account, open hello Baidu activation mail, and click hello activation link tooactivate your Baidu account.</span></span>
   
   ![][4]

<span data-ttu-id="503f0-124">Baidu hesabınızı etkinleştirdikten sonra toohello içinde oturum [Baidu portalında].</span><span class="sxs-lookup"><span data-stu-id="503f0-124">Once you have an activated Baidu account, log in toohello [Baidu portal].</span></span>

## <a name="register-as-a-baidu-developer"></a><span data-ttu-id="503f0-125">Bir Baidu geliştiricisi olarak kaydolma</span><span class="sxs-lookup"><span data-stu-id="503f0-125">Register as a Baidu developer</span></span>
1. <span data-ttu-id="503f0-126">İçinde toohello oturum açtıktan sonra [Baidu portalında], tıklatın**更多 >>** (**daha fazla**).</span><span class="sxs-lookup"><span data-stu-id="503f0-126">Once you have logged in toohello [Baidu portal], click **更多>>** (**more**).</span></span>
   
      ![][5]
2. <span data-ttu-id="503f0-127">Aşağı kaydırın hello**站长与开发者服务 (yayımlanması ve geliştirici Hizmetleri)** 'ye tıklayın**百度开放云平台**(**Baidu bulut platformu açmak**).</span><span class="sxs-lookup"><span data-stu-id="503f0-127">Scroll down in hello **站长与开发者服务 (Webmaster and Developer Services)** section and click **百度开放云平台** (**Baidu open cloud platform**).</span></span>
   
      ![][6]
3. <span data-ttu-id="503f0-128">Merhaba sonraki sayfasında, tıklatın**开发者服务**(**Geliştirici Hizmetleri**) hello sağ üst köşede.</span><span class="sxs-lookup"><span data-stu-id="503f0-128">On hello next page, click **开发者服务** (**Developer Services**) on hello top-right corner.</span></span>
   
      ![][7]
4. <span data-ttu-id="503f0-129">Merhaba sonraki sayfasında, tıklatın**注册开发者**(**kayıtlı geliştiriciler**) hello sağ üst köşesinde hello menüsünden.</span><span class="sxs-lookup"><span data-stu-id="503f0-129">On hello next page, click **注册开发者** (**Registered Developers**) from hello menu on hello top-right corner.</span></span>
   
      ![][8]
5. <span data-ttu-id="503f0-130">Bir doğrulama kısa mesajı almak için adınızı, açıklamayı ve cep telefonu numarasını girin ve ardından **送验证码** (**Doğrulama Kodu Gönder**) öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="503f0-130">Enter your name, a description, and a mobile phone number for receiving a verification text message, and then click **送验证码** (**Send Verification Code**).</span></span> <span data-ttu-id="503f0-131">Uluslararası telefon numaraları için parantez içinde tooenclose hello ülke kodu gerekir.</span><span class="sxs-lookup"><span data-stu-id="503f0-131">For international phone numbers, you need tooenclose hello country code in parentheses.</span></span> <span data-ttu-id="503f0-132">Örneğin, bir Amerika Birleşik Devletleri numarası için bu **(1) 1234567890** şeklinde olacaktır.</span><span class="sxs-lookup"><span data-stu-id="503f0-132">For example, for a United States number, it is **(1)1234567890**.</span></span>
   
      ![][9]
6. <span data-ttu-id="503f0-133">Ardından hello aşağıdaki örnekte gösterildiği gibi bir doğrulama numarasına sahip bir kısa mesaj almalısınız:</span><span class="sxs-lookup"><span data-stu-id="503f0-133">You should then receive a text message with a verification number, as shown in hello following example:</span></span>
   
      ![][10]
7. <span data-ttu-id="503f0-134">Merhaba iletisi Hello doğrulama numarasını girin**验证码**(**onay kodu**).</span><span class="sxs-lookup"><span data-stu-id="503f0-134">Enter hello verification number from hello message in **验证码** (**Confirmation code**).</span></span>
8. <span data-ttu-id="503f0-135">Son olarak, hello Geliştirici kayıt hello Baidu anlaşmayı kabul eden ve'ı tıklatarak tamamlayın**提交**(**gönderme**).</span><span class="sxs-lookup"><span data-stu-id="503f0-135">Finally, complete hello developer registration by accepting hello Baidu agreement and clicking **提交** (**Submit**).</span></span> <span data-ttu-id="503f0-136">Kayıt başarılı şekilde tamamlandığını sayfasında aşağıdaki hello görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="503f0-136">You will see hello following page on successful completion of registration:</span></span>
   
      ![][11]

## <a name="create-a-baidu-cloud-push-project"></a><span data-ttu-id="503f0-137">Bir Baidu bulut anında iletme projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="503f0-137">Create a Baidu cloud push project</span></span>
<span data-ttu-id="503f0-138">Bir Baidu bulut anında iletme projesi oluşturduğunuzda, uygulama kimliğinizi, API anahtarınızı ve gizli anahtarınızı alırsınız.</span><span class="sxs-lookup"><span data-stu-id="503f0-138">When you create a Baidu cloud push project, you receive your app ID, API key, and secret key.</span></span>

1. <span data-ttu-id="503f0-139">İçinde toohello oturum açtıktan sonra [Baidu portalında], tıklatın**更多 >>** (**daha fazla**).</span><span class="sxs-lookup"><span data-stu-id="503f0-139">Once you have logged in toohello [Baidu portal], click **更多>>** (**more**).</span></span>
   
      ![][5]
2. <span data-ttu-id="503f0-140">Aşağı kaydırın hello**站长与开发者服务**(**yayımlanması ve geliştirici Hizmetleri**) bölümünde ve tıklatın**百度开放云平台**(**Baidu bulut platformu açmak**).</span><span class="sxs-lookup"><span data-stu-id="503f0-140">Scroll down in hello **站长与开发者服务** (**Webmaster and Developer Services**) section and click **百度开放云平台** (**Baidu open cloud platform**).</span></span>
   
      ![][6]
3. <span data-ttu-id="503f0-141">Merhaba sonraki sayfasında, tıklatın**开发者服务**(**Geliştirici Hizmetleri**) hello sağ üst köşede.</span><span class="sxs-lookup"><span data-stu-id="503f0-141">On hello next page, click **开发者服务** (**Developer Services**) on hello top-right corner.</span></span>
   
      ![][7]
4. <span data-ttu-id="503f0-142">Merhaba sonraki sayfasında, tıklatın**云推送**(**bulut itme**) hello gelen**云服务**(**bulut Hizmetleri**) bölümü.</span><span class="sxs-lookup"><span data-stu-id="503f0-142">On hello next page, click **云推送** (**Cloud Push**) from hello **云服务** (**Cloud Services**) section.</span></span>
   
      ![][12]
5. <span data-ttu-id="503f0-143">Kayıtlı bir geliştirici olduktan sonra gördüğünüz**管理控制台**(**Yönetim Konsolu**) hello üst menüsünde.</span><span class="sxs-lookup"><span data-stu-id="503f0-143">Once you are a registered developer, you see **管理控制台** (**Management Console**) at hello top menu.</span></span> <span data-ttu-id="503f0-144">**开发者服务管理** (**Geliştirici Hizmeti Yönetimi**) öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="503f0-144">Click **开发者服务管理** (**Developers Service Management**).</span></span>
   
      ![][13]
6. <span data-ttu-id="503f0-145">Merhaba sonraki sayfasında, tıklatın**创建工程**(**proje oluştur**).</span><span class="sxs-lookup"><span data-stu-id="503f0-145">On hello next page, click **创建工程** (**Create Project**).</span></span>
   
      ![][14]
7. <span data-ttu-id="503f0-146">Bir uygulama adı girin ve **创建** (**Oluştur**) öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="503f0-146">Enter an application name and click **创建** (**Create**).</span></span>
   
      ![][15]
8. <span data-ttu-id="503f0-147">Bir Baidu bulut anında iletme projesi başarılı bir şekilde oluşturulduktan sonra, **Uygulama Kimliği**, **API Anahtarı** ve **Gizli Anahtar** değerlerini içeren bir sayfa görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="503f0-147">Upon successful creation of a Baidu cloud push project, you see a page with **AppID**, **API Key**, and **Secret Key**.</span></span> <span data-ttu-id="503f0-148">Merhaba API anahtarı ve daha sonra kullanacağımız gizli anahtarı not edin.</span><span class="sxs-lookup"><span data-stu-id="503f0-148">Make a note of hello API key and secret key, which we will use later.</span></span>
   
      ![][16]
9. <span data-ttu-id="503f0-149">Tıklayarak Hello projesi anında iletme bildirimleri için yapılandırma**云推送**(**bulut anında iletme**) hello sol bölmedeki.</span><span class="sxs-lookup"><span data-stu-id="503f0-149">Configure hello project for push notifications by clicking **云推送** (**Cloud Push**) on hello left pane.</span></span>
   
      ![][31]
10. <span data-ttu-id="503f0-150">Merhaba Hello sonraki sayfasında, tıklatın**推送设置**(**ayarları göndermek**) düğmesi.</span><span class="sxs-lookup"><span data-stu-id="503f0-150">On hello next page, click hello **推送设置** (**Push settings**) button.</span></span>
    
    ![][32]  
11. <span data-ttu-id="503f0-151">Merhaba Android projenizde kullanacağınız hello paket adı Hello yapılandırma sayfasında, eklemek**应用包名**(**uygulama paketi**) alan ve ardından**保存设置**() **Kaydetmek**).</span><span class="sxs-lookup"><span data-stu-id="503f0-151">On hello configuration page, add hello package name that you will be using in your Android project in hello **应用包名** (**Application package**) field, and then click **保存设置** (**Save**).</span></span>  
    
    ![][33]

<span data-ttu-id="503f0-152">Merhaba gördüğünüz**保存成功!** (**Başarıyla kaydedildi!**) iletisini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="503f0-152">You see hello **保存成功！** (**Successfully saved!**) message.</span></span>

## <a name="configure-your-notification-hub"></a><span data-ttu-id="503f0-153">Bildirim hub'ınızı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="503f0-153">Configure your notification hub</span></span>
1. <span data-ttu-id="503f0-154">İçinde toohello oturum [Klasik Azure portalı]ve ardından **+ yeni** Merhaba ekranında hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="503f0-154">Sign in toohello [Azure Classic Portal], and then click **+NEW** at hello bottom of hello screen.</span></span>
2. <span data-ttu-id="503f0-155">**Uygulama Hizmetleri**'ne tıklayın, **Service Bus**'a tıklayın, **Notification Hub**'a tıklayın ve ardından **Hızlı Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="503f0-155">Click **App Services**, click **Service Bus**, click **Notification Hub**, and then click **Quick Create**.</span></span>
3. <span data-ttu-id="503f0-156">İçin bir ad, **bildirim hub'ı**seçin hello **bölge** ve hello **Namespace** burada bu bildirim hub'ı oluşturulur ve ardından  **Yeni bir Notification Hub Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="503f0-156">Provide a name for your **Notification Hub**, select hello **Region** and hello **Namespace** where this notification hub will be created, and then click **Create a New Notification Hub**.</span></span>  
   
      ![][17]
4. <span data-ttu-id="503f0-157">Bildirim hub'ınızı oluşturduğunuz hello ad alanına tıklayın ve ardından **bildirim hub'ları** hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="503f0-157">Click hello namespace in which you created your notification hub, and then click **Notification Hubs** at hello top.</span></span>
   
      ![][18]
5. <span data-ttu-id="503f0-158">Oluşturulan ve ardından select hello bildirim hub'ı **yapılandırma** hello üst menüsünde.</span><span class="sxs-lookup"><span data-stu-id="503f0-158">Select hello notification hub that you created, and then click **Configure** from hello top menu.</span></span>
   
      ![][19]
6. <span data-ttu-id="503f0-159">Toohello aşağı **baidu bildirim ayarları** bölümünde ve hello Baidu konsolundan Baidu bulut anında iletme projeniz için daha önce edindiğiniz gizli anahtar ve hello API anahtarını girin.</span><span class="sxs-lookup"><span data-stu-id="503f0-159">Scroll down toohello **baidu notification settings** section and enter hello API key and secret key that you obtained from hello Baidu console previously for your Baidu cloud push project.</span></span> <span data-ttu-id="503f0-160">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="503f0-160">Click **Save**.</span></span>
   
      ![][20]
7. <span data-ttu-id="503f0-161">Merhaba tıklatın **Pano** sekmesinde hello üst hello bildirim hub'ı ve ardından **bağlantı dizesini görüntüle**.</span><span class="sxs-lookup"><span data-stu-id="503f0-161">Click hello **Dashboard** tab at hello top for hello notification hub, and then click **View Connection String**.</span></span>
   
      ![][21]
8. <span data-ttu-id="503f0-162">Merhaba Not **DefaultListenSharedAccessSignature** ve **DefaultFullSharedAccessSignature** hello gelen **erişim bağlantısı bilgileri** penceresi.</span><span class="sxs-lookup"><span data-stu-id="503f0-162">Make a note of hello **DefaultListenSharedAccessSignature** and **DefaultFullSharedAccessSignature** from hello **Access connection information** window.</span></span>
   
    ![][22]

## <a name="connect-your-app-toohello-notification-hub"></a><span data-ttu-id="503f0-163">Uygulama toohello bildirim hub'ınıza bağlanın</span><span class="sxs-lookup"><span data-stu-id="503f0-163">Connect your app toohello notification hub</span></span>
1. <span data-ttu-id="503f0-164">Eclipse ADT'de yeni bir Android projesi (**Dosya** > **Yeni** > **Android Uygulama Projesi**) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="503f0-164">In Eclipse ADT, create a new Android project (**File** > **New** > **Android Application Project**).</span></span>
   
    ![][23]
2. <span data-ttu-id="503f0-165">Girin bir **uygulama adı** ve o hello olun **gereken Minimum SDK** sürümü çok Ayarla**API 16: Android 4.1**.</span><span class="sxs-lookup"><span data-stu-id="503f0-165">Enter an **Application Name** and ensure that hello **Minimum Required SDK** version is set too**API 16: Android 4.1**.</span></span>
   
    ![][24]
3. <span data-ttu-id="503f0-166">Tıklatın **sonraki** ve hello kadar hello Sihirbazı aşağıdaki devam **etkinlik Oluştur** penceresi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="503f0-166">Click **Next** and continue following hello wizard until hello **Create Activity** window appears.</span></span> <span data-ttu-id="503f0-167">Olduğundan emin olun **boş etkinlik** seçili ve son olarak select **son** toocreate yeni bir Android uygulaması.</span><span class="sxs-lookup"><span data-stu-id="503f0-167">Make sure that **Blank Activity** is selected, and finally select **Finish** toocreate a new Android Application.</span></span>
   
    ![][25]
4. <span data-ttu-id="503f0-168">Bu hello emin olun **proje derleme hedefi** doğru olarak ayarlanmış.</span><span class="sxs-lookup"><span data-stu-id="503f0-168">Make sure that hello **Project Build Target** is set correctly.</span></span>
   
    ![][26]
5. <span data-ttu-id="503f0-169">Hello Hello notification-hubs-0.4.jar dosyasını indirin **dosyaları** hello sekmesinde [Notification-Hubs-Android-SDK Bintray'deki üzerinde](https://bintray.com/microsoftazuremobile/SDK/Notification-Hubs-Android-SDK/0.4).</span><span class="sxs-lookup"><span data-stu-id="503f0-169">Download hello notification-hubs-0.4.jar file from hello **Files** tab of hello [Notification-Hubs-Android-SDK on Bintray](https://bintray.com/microsoftazuremobile/SDK/Notification-Hubs-Android-SDK/0.4).</span></span> <span data-ttu-id="503f0-170">Merhaba dosya toohello ekleme **kitaplıklar** klasörü Eclipse projenizin ve yenileme hello *kitaplıklar* klasör.</span><span class="sxs-lookup"><span data-stu-id="503f0-170">Add hello file toohello **libs** folder of your Eclipse project, and refresh hello *libs* folder.</span></span>
6. <span data-ttu-id="503f0-171">İndirip hello sıkıştırmasını [Baidu anında iletme Android SDK]açın hello **kitaplıklar** klasörünü ve ardından kopyalama hello **libs-x.y.z** jar dosyasını ve hello **pushservice**  &  **MIPS** hello klasörlerde **kitaplıklar** Android uygulamanızın klasör.</span><span class="sxs-lookup"><span data-stu-id="503f0-171">Download and unzip hello [Baidu Push Android SDK], open hello **libs** folder, and then copy hello **pushservice-x.y.z** jar file and hello **armeabi** & **mips** folders in hello **libs** folder of your Android application.</span></span>
7. <span data-ttu-id="503f0-172">Açık hello **AndroidManifest.xml** dosya Android projesi ve Baidu SDK hello tarafından gerekli olan hello izinleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="503f0-172">Open hello **AndroidManifest.xml** file of your Android project and add hello permissions that are required by hello Baidu SDK.</span></span>
   
        <uses-permission android:name="android.permission.INTERNET" />
        <uses-permission android:name="android.permission.READ_PHONE_STATE" />
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.WRITE_SETTINGS" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
        <uses-permission android:name="android.permission.DISABLE_KEYGUARD" />
        <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
        <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
        <uses-permission android:name="android.permission.ACCESS_DOWNLOAD_MANAGER" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION" />
8. <span data-ttu-id="503f0-173">Merhaba eklemek **android: name** özelliği tooyour **uygulama** öğesinde **AndroidManifest.xml**değiştirerek *yourprojectname* (için Örneğin, **com.example.BaiduTest**).</span><span class="sxs-lookup"><span data-stu-id="503f0-173">Add hello **android:name** property tooyour **application** element in **AndroidManifest.xml**, replacing *yourprojectname* (for example, **com.example.BaiduTest**).</span></span> <span data-ttu-id="503f0-174">Bu proje adı hello Baidu konsolunda yapılandırdığınız hello bir eşleştiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="503f0-174">Make sure that this project name matches hello one that you configured in hello Baidu console.</span></span>
   
        <application android:name="yourprojectname.DemoApplication"
9. <span data-ttu-id="503f0-175">Merhaba hello sonra yapılandırmasını hello uygulama öğesi içinde aşağıdaki ekleme **. MainActivity** etkinlik öğesinden değiştirme *yourprojectname* (örneğin, **com.example.BaiduTest**):</span><span class="sxs-lookup"><span data-stu-id="503f0-175">Add hello following configuration within hello application element after hello **.MainActivity** activity element, replacing *yourprojectname* (for example, **com.example.BaiduTest**):</span></span>
   
        <receiver android:name="yourprojectname.MyPushMessageReceiver">
            <intent-filter>
                <action android:name="com.baidu.android.pushservice.action.MESSAGE" />
                <action android:name="com.baidu.android.pushservice.action.RECEIVE" />
                <action android:name="com.baidu.android.pushservice.action.notification.CLICK" />
            </intent-filter>
        </receiver>
   
        <receiver android:name="com.baidu.android.pushservice.PushServiceReceiver"
            android:process=":bdservice_v1">
            <intent-filter>
                <action android:name="android.intent.action.BOOT_COMPLETED" />
                <action android:name="android.net.conn.CONNECTIVITY_CHANGE" />
                <action android:name="com.baidu.android.pushservice.action.notification.SHOW" />
            </intent-filter>
        </receiver>
   
        <receiver android:name="com.baidu.android.pushservice.RegistrationReceiver"
            android:process=":bdservice_v1">
            <intent-filter>
                <action android:name="com.baidu.android.pushservice.action.METHOD" />
                <action android:name="com.baidu.android.pushservice.action.BIND_SYNC" />
            </intent-filter>
            <intent-filter>
                <action android:name="android.intent.action.PACKAGE_REMOVED"/>
                <data android:scheme="package" />
            </intent-filter>
        </receiver>
   
        <service
            android:name="com.baidu.android.pushservice.PushService"
            android:exported="true"
            android:process=":bdservice_v1"  >
            <intent-filter>
                <action android:name="com.baidu.android.pushservice.action.PUSH_SERVICE" />
            </intent-filter>
        </service>
10. <span data-ttu-id="503f0-176">Adlı yeni bir sınıf ekleyin **ConfigurationSettings.java** toohello projesi.</span><span class="sxs-lookup"><span data-stu-id="503f0-176">Add a new class called **ConfigurationSettings.java** toohello project.</span></span>
    
     ![][28]
    
     ![][29]
11. <span data-ttu-id="503f0-177">Aşağıdaki kod tooit hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="503f0-177">Add hello following code tooit:</span></span>
    
        public class ConfigurationSettings {
                public static String API_KEY = "...";
                public static String NotificationHubName = "...";
                public static String NotificationHubConnectionString = "...";
            }
    
    <span data-ttu-id="503f0-178">Merhaba değeri olarak ayarlayın **apı_key** ne hello Baidu bulut projesinden daha önce alınan ile **NotificationHubName** hello Klasik Azure Portalı'ndan bildirim hub'ı adıyla ve  **NotificationHubConnectionString** defaultlistensharedaccesssignature hello Klasik Azure portalı ile.</span><span class="sxs-lookup"><span data-stu-id="503f0-178">Set hello value of **API_KEY** with what you retrieved from hello Baidu cloud project earlier, **NotificationHubName** with your notification hub name from hello Azure Classic Portal and **NotificationHubConnectionString** with DefaultListenSharedAccessSignature from hello Azure Classic Portal.</span></span>
12. <span data-ttu-id="503f0-179">Adlı yeni bir sınıf ekleyin **DemoApplication.java**ve kod tooit aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="503f0-179">Add a new class called **DemoApplication.java**, and add hello following code tooit:</span></span>
    
        import com.baidu.frontia.FrontiaApplication;
    
        public class DemoApplication extends FrontiaApplication {
            @Override
            public void onCreate() {
                super.onCreate();
            }
        }
13. <span data-ttu-id="503f0-180">Adlı başka bir yeni sınıf ekleyin **MyPushMessageReceiver.java**ve kod tooit aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="503f0-180">Add another new class called **MyPushMessageReceiver.java**, and add hello following code tooit.</span></span> <span data-ttu-id="503f0-181">Merhaba Baidu anında iletme sunucusundan alınan anında iletme bildirimleri tanıtıcıları hello hello sınıfı var.</span><span class="sxs-lookup"><span data-stu-id="503f0-181">It is hello class that handles hello push notifications that are received from hello Baidu push server.</span></span>
    
        import java.util.List;
        import android.content.Context;
        import android.os.AsyncTask;
        import android.util.Log;
        import com.baidu.frontia.api.FrontiaPushMessageReceiver;
        import com.microsoft.windowsazure.messaging.NotificationHub;
    
        public class MyPushMessageReceiver extends FrontiaPushMessageReceiver {
            /** TAG tooLog */
            public static NotificationHub hub = null;
            public static String mChannelId, mUserId;
            public static final String TAG = MyPushMessageReceiver.class
                    .getSimpleName();
    
            @Override
            public void onBind(Context context, int errorCode, String appid,
                    String userId, String channelId, String requestId) {
                String responseString = "onBind errorCode=" + errorCode + " appid="
                        + appid + " userId=" + userId + " channelId=" + channelId
                        + " requestId=" + requestId;
                Log.d(TAG, responseString);
                mChannelId = channelId;
                mUserId = userId;
    
                try {
                    if (hub == null) {
                        hub = new NotificationHub(
                                ConfigurationSettings.NotificationHubName,
                                ConfigurationSettings.NotificationHubConnectionString,
                                context);
                        Log.i(TAG, "Notification hub initialized");
                    }
                } catch (Exception e) {
                   Log.e(TAG, e.getMessage());
                }
    
                registerWithNotificationHubs();
            }
    
            private void registerWithNotificationHubs() {
               new AsyncTask<Void, Void, Void>() {
                  @Override
                  protected Void doInBackground(Void... params) {
                     try {
                         hub.registerBaidu(mUserId, mChannelId);
                         Log.i(TAG, "Registered with Notification Hub - '"
                                 + ConfigurationSettings.NotificationHubName + "'"
                                 + " with UserId - '"
                                 + mUserId + "' and Channel Id - '"
                                 + mChannelId + "'");
                     } catch (Exception e) {
                         Log.e(TAG, e.getMessage());
                     }
                     return null;
                 }
               }.execute(null, null, null);
            }
    
            @Override
            public void onSetTags(Context context, int errorCode,
                    List<String> sucessTags, List<String> failTags, String requestId) {
                String responseString = "onSetTags errorCode=" + errorCode
                        + " sucessTags=" + sucessTags + " failTags=" + failTags
                        + " requestId=" + requestId;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onDelTags(Context context, int errorCode,
                    List<String> sucessTags, List<String> failTags, String requestId) {
                String responseString = "onDelTags errorCode=" + errorCode
                        + " sucessTags=" + sucessTags + " failTags=" + failTags
                        + " requestId=" + requestId;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onListTags(Context context, int errorCode, List<String> tags,
                    String requestId) {
                String responseString = "onListTags errorCode=" + errorCode + " tags="
                        + tags;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onUnbind(Context context, int errorCode, String requestId) {
                String responseString = "onUnbind errorCode=" + errorCode
                        + " requestId = " + requestId;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onNotificationClicked(Context context, String title,
                    String description, String customContentString) {
                String notifyString = "title=\"" + title + "\" description=\""
                        + description + "\" customContent=" + customContentString;
                Log.d(TAG, notifyString);
            }
    
            @Override
            public void onMessage(Context context, String message,
                    String customContentString) {
                String messageString = "message=\"" + message + "\" customContentString=" + customContentString;
                Log.d(TAG, messageString);
            }
        }
14. <span data-ttu-id="503f0-182">Açık **MainActivity.java**ve toohello aşağıdaki hello ekleyin **onCreate** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="503f0-182">Open **MainActivity.java**, and add hello following toohello **onCreate** method:</span></span>
    
            PushManager.startWork(getApplicationContext(),
                    PushConstants.LOGIN_TYPE_API_KEY, ConfigurationSettings.API_KEY);
15. <span data-ttu-id="503f0-183">İçeri aktarma deyimlerini hello üstünde aşağıdaki hello açın:</span><span class="sxs-lookup"><span data-stu-id="503f0-183">Open hello following import statements at hello top:</span></span>
    
            import com.baidu.android.pushservice.PushConstants;
            import com.baidu.android.pushservice.PushManager;

## <a name="send-notifications-tooyour-app"></a><span data-ttu-id="503f0-184">Bildirimleri tooyour uygulama Gönder</span><span class="sxs-lookup"><span data-stu-id="503f0-184">Send notifications tooyour app</span></span>
<span data-ttu-id="503f0-185">Hello bildirimleri göndererek uygulamanızda bildirim alma hızlı bir şekilde test edebilirsiniz [Azure portal](https://portal.azure.com/) hello kullanarak **Gönder** hello ekran aşağıdaki gösterildiği gibi hello bildirim hub'ı üzerinde düğmesi:</span><span class="sxs-lookup"><span data-stu-id="503f0-185">You can quickly test receiving notifications in your app by sending notifications in hello [Azure portal](https://portal.azure.com/) using hello **Send** button on hello notification hub, as shown in hello following screen:</span></span>

![](./media/notification-hubs-baidu-get-started/notification-hub-test-send-baidu.png)

<span data-ttu-id="503f0-186">Anında iletme bildirimleri normalde, uyumlu bir kitaplık kullanılarak Mobile Services veya ASP.NET gibi bir arka uç hizmetinde gönderilir.</span><span class="sxs-lookup"><span data-stu-id="503f0-186">Push notifications are normally sent in a back-end service like Mobile Services or ASP.NET using a compatible library.</span></span> <span data-ttu-id="503f0-187">Bir kitaplık arka ucunuz için kullanılabilir durumda değilse, hello REST API'sini kullanabilirsiniz doğrudan toosend bildirim iletileri.</span><span class="sxs-lookup"><span data-stu-id="503f0-187">If a library is not available for your back-end, you can use hello REST API directly toosend notification messages .</span></span>

<span data-ttu-id="503f0-188">Bu öğreticide, basit tutmak ve yalnızca arka uç hizmeti yerine bir konsol uygulamasındaki bildirim hub'ları için hello .NET SDK kullanarak bildirim göndererek istemci uygulamanızı test etme gösterme.</span><span class="sxs-lookup"><span data-stu-id="503f0-188">In this tutorial, we keep it simple and just demonstrate testing your client app by sending notifications using hello .NET SDK for notification hubs in a console application instead of a backend service.</span></span> <span data-ttu-id="503f0-189">Merhaba öneririz [Notification Hubs kullanma toopush bildirimleri toousers](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) hello bir ASP.NET arka ucundan bildirim göndermek için sonraki adım olarak Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="503f0-189">We recommend hello [Use Notification Hubs toopush notifications toousers](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) tutorial as hello next step for sending notifications from an ASP.NET backend.</span></span> <span data-ttu-id="503f0-190">Ancak, aşağıdaki yaklaşımlardan hello bildirim göndermek için kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="503f0-190">However, hello following approaches can be used for sending notifications:</span></span>

* <span data-ttu-id="503f0-191">**REST arabirimi**: hello kullanarak herhangi bir arka uç platform bildirim destekleyebilir [REST arabirimini](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="503f0-191">**REST Interface**:  You can support notification on any backend platform using  hello [REST interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span></span>
* <span data-ttu-id="503f0-192">**Microsoft Azure Notification Hubs .NET SDK'sı**: hello Visual Studio için Nuget Paket Yöneticisi, çalışması [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="503f0-192">**Microsoft Azure Notification Hubs .NET SDK**: In hello Nuget Package Manager for Visual Studio, run [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>
* <span data-ttu-id="503f0-193">**Node.js**: [nasıl toouse node.js'den Notification Hubs](notification-hubs-nodejs-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="503f0-193">**Node.js**: [How toouse Notification Hubs from Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span></span>
* <span data-ttu-id="503f0-194">**Mobile Apps**: bir örneği için Notification Hubs ile tümleştirilmiş Azure App Service Mobile Apps arka uç toosend bildirimleri bkz [Ekle anında iletme bildirimleri tooyour mobil uygulama](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="503f0-194">**Mobile Apps**: For an example of how toosend notifications from an Azure App Service Mobile Apps backend that's integrated with Notification Hubs, see [Add push notifications tooyour mobile app](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).</span></span>
* <span data-ttu-id="503f0-195">**Java / PHP**: REST API'lerini kullanarak toosend bildirim nasıl hello ilişkin bir örnek için bkz: "nasıl toouse Java/php'den Notification Hubs" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span><span class="sxs-lookup"><span data-stu-id="503f0-195">**Java / PHP**: For an example of how toosend notifications by using hello REST APIs, see "How toouse Notification Hubs from Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span></span>

## <a name="optional-send-notifications-from-a-net-console-app"></a><span data-ttu-id="503f0-196">(İsteğe bağlı) Bir .NET konsol uygulamasından bildirim gönderme</span><span class="sxs-lookup"><span data-stu-id="503f0-196">(Optional) Send notifications from a .NET console app.</span></span>
<span data-ttu-id="503f0-197">Bu bölümde, bir .NET konsol uygulaması kullanarak bildirim göndermeyi göstereceğiz.</span><span class="sxs-lookup"><span data-stu-id="503f0-197">In this section, we show sending a notification using a .NET console app.</span></span>

1. <span data-ttu-id="503f0-198">Yeni bir Visual C# konsol uygulaması oluşturun:</span><span class="sxs-lookup"><span data-stu-id="503f0-198">Create a new Visual C# console application:</span></span>
   
    ![][30]
2. <span data-ttu-id="503f0-199">Hello Paket Yöneticisi konsolu penceresinde, hello ayarlamak **varsayılan proje** tooyour yeni konsol uygulama projesi ve sonra hello konsol penceresinde hello aşağıdaki komutu yürütün:</span><span class="sxs-lookup"><span data-stu-id="503f0-199">In hello Package Manager Console window, set hello **Default project** tooyour new console application project, and then in hello console window, execute hello following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="503f0-200">Bu yönerge başvuru toohello Azure Notification Hubs SDK'sı ekler hello kullanarak <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet paketini</a>.</span><span class="sxs-lookup"><span data-stu-id="503f0-200">This instruction adds a reference toohello Azure Notification Hubs SDK using hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
3. <span data-ttu-id="503f0-201">Açık hello dosya **Program.cs** ve hello aşağıdakileri ekleyin deyimi kullanarak:</span><span class="sxs-lookup"><span data-stu-id="503f0-201">Open hello file **Program.cs** and add hello following using statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
4. <span data-ttu-id="503f0-202">İçinde `Program` sınıfı, yöntem aşağıdaki hello ekleyebilir ve *DefaultFullSharedAccessSignatureSASConnectionString* ve *NotificationHubName* elinizde hello değerlere sahip.</span><span class="sxs-lookup"><span data-stu-id="503f0-202">In your `Program` class, add hello following method and replace *DefaultFullSharedAccessSignatureSASConnectionString* and *NotificationHubName* with hello values that you have.</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("DefaultFullSharedAccessSignatureSASConnectionString", "NotificationHubName");
            string message = "{\"title\":\"((Notification title))\",\"description\":\"Hello from Azure\"}";
            var result = await hub.SendBaiduNativeNotificationAsync(message);
        }
5. <span data-ttu-id="503f0-203">Hello aşağıdaki satırları ekleyin, **ana** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="503f0-203">Add hello following lines in your **Main** method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();

## <a name="test-your-app"></a><span data-ttu-id="503f0-204">Uygulamanızı test etme</span><span class="sxs-lookup"><span data-stu-id="503f0-204">Test your app</span></span>
<span data-ttu-id="503f0-205">Bu uygulama, yalnızca gerçek bir telefonla connect tootest bir USB kablosu kullanarak telefon tooyour bilgisayar hello.</span><span class="sxs-lookup"><span data-stu-id="503f0-205">tootest this app with an actual phone, just connect hello phone tooyour computer by using a USB cable.</span></span> <span data-ttu-id="503f0-206">Bu eylem uygulamanız iliştirilmiş hello telefon yükler.</span><span class="sxs-lookup"><span data-stu-id="503f0-206">This action loads your app onto hello attached phone.</span></span>

<span data-ttu-id="503f0-207">Merhaba öykünücüsünde hello Eclipse üst araç çubuğunda, bu uygulamayla tootest tıklatın **çalıştırmak**ve ardından uygulamanızı seçin: hello öykünücüsü, yüklendiğinde başlatır ve çalıştırmalarını hello uygulama.</span><span class="sxs-lookup"><span data-stu-id="503f0-207">tootest this app with hello emulator, on hello Eclipse top toolbar, click **Run**, and then select your app: it starts hello emulator, loads, and runs hello app.</span></span>

<span data-ttu-id="503f0-208">Merhaba uygulama Baidu anında bildirim hizmeti hello hello UserID' ve 'Channelıd' alır ve hello bildirim hub'ı ile kaydeder.</span><span class="sxs-lookup"><span data-stu-id="503f0-208">hello app retrieves hello 'userId' and 'channelId' from hello Baidu Push notification service and registers with hello notification hub.</span></span>

<span data-ttu-id="503f0-209">bir test bildirimi toosend hello Klasik Azure portalı hello hata ayıklama sekmesini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="503f0-209">toosend a test notification, you can use hello debug tab of hello Azure Classic Portal.</span></span> <span data-ttu-id="503f0-210">Merhaba .NET konsol uygulaması Visual Studio için oluşturulduysa, yalnızca Visual Studio toorun hello uygulamada hello F5 tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="503f0-210">If you built hello .NET console application for Visual Studio, just press hello F5 key in Visual Studio toorun hello application.</span></span> <span data-ttu-id="503f0-211">Merhaba uygulaması hello üst bildirim alanında cihaz veya öykünücü görünür bir bildirim gönderir.</span><span class="sxs-lookup"><span data-stu-id="503f0-211">hello application sends a notification that appears in hello top notification area of your device or emulator.</span></span>

<!-- Images. -->
[1]: ./media/notification-hubs-baidu-get-started/BaiduRegistration.png
[2]: ./media/notification-hubs-baidu-get-started/BaiduRegistrationInput.png
[3]: ./media/notification-hubs-baidu-get-started/BaiduConfirmation.png
[4]: ./media/notification-hubs-baidu-get-started/BaiduActivationEmail.png
[5]: ./media/notification-hubs-baidu-get-started/BaiduRegistrationMore.png
[6]: ./media/notification-hubs-baidu-get-started/BaiduOpenCloudPlatform.png
[7]: ./media/notification-hubs-baidu-get-started/BaiduDeveloperServices.png
[8]: ./media/notification-hubs-baidu-get-started/BaiduDeveloperRegistration.png
[9]: ./media/notification-hubs-baidu-get-started/BaiduDevRegistrationInput.png
[10]: ./media/notification-hubs-baidu-get-started/BaiduDevRegistrationConfirmation.png
[11]: ./media/notification-hubs-baidu-get-started/BaiduDevConfirmationFinal.png
[12]: ./media/notification-hubs-baidu-get-started/BaiduCloudPush.png
[13]: ./media/notification-hubs-baidu-get-started/BaiduDevSvcMgmt.png
[14]: ./media/notification-hubs-baidu-get-started/BaiduCreateProject.png
[15]: ./media/notification-hubs-baidu-get-started/BaiduCreateProjectInput.png
[16]: ./media/notification-hubs-baidu-get-started/BaiduProjectKeys.png
[17]: ./media/notification-hubs-baidu-get-started/AzureNHCreation.png
[18]: ./media/notification-hubs-baidu-get-started/NotificationHubs.png
[19]: ./media/notification-hubs-baidu-get-started/NotificationHubsConfigure.png
[20]: ./media/notification-hubs-baidu-get-started/NotificationHubBaiduConfigure.png
[21]: ./media/notification-hubs-baidu-get-started/NotificationHubsConnectionStringView.png
[22]: ./media/notification-hubs-baidu-get-started/NotificationHubsConnectionString.png
[23]: ./media/notification-hubs-baidu-get-started/EclipseNewProject.png
[24]: ./media/notification-hubs-baidu-get-started/EclipseProjectCreation.png
[25]: ./media/notification-hubs-baidu-get-started/EclipseBlankActivity.png
[26]: ./media/notification-hubs-baidu-get-started/EclipseProjectBuildProperty.png
[27]: ./media/notification-hubs-baidu-get-started/EclipseBaiduReferences.png
[28]: ./media/notification-hubs-baidu-get-started/EclipseNewClass.png
[29]: ./media/notification-hubs-baidu-get-started/EclipseConfigSettingsClass.png
[30]: ./media/notification-hubs-baidu-get-started/ConsoleProject.png
[31]: ./media/notification-hubs-baidu-get-started/BaiduPushConfig1.png
[32]: ./media/notification-hubs-baidu-get-started/BaiduPushConfig2.png
[33]: ./media/notification-hubs-baidu-get-started/BaiduPushConfig3.png

<!-- URLs. -->
[Mobile Services Android SDK'sı]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409
[Baidu anında iletme Android SDK]: http://developer.baidu.com/wiki/index.php?title=docs/cplat/push/sdk/clientsdk
[Klasik Azure portalı]: https://manage.windowsazure.com/
[Baidu portalında]: http://www.baidu.com/
