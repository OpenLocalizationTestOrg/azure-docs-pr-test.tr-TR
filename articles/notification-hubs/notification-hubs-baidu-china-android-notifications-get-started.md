---
title: "Baidu kullanarak Azure Notification Hubs ile çalışmaya başlama | Microsoft Belgeleri"
description: "Bu öğreticide, Baidu kullanarak Android cihazlarına anında iletme bildirimleri göndermek için Azure Notification Hubs'ın nasıl kullanılacağını öğrenirsiniz."
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
ms.openlocfilehash: df3bbda15e1245b6068c2b8290d0c96856051f1f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-notification-hubs-using-baidu"></a><span data-ttu-id="3fb47-103">Baidu kullanarak Azure Notification Hubs ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="3fb47-103">Get started with Notification Hubs using Baidu</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="3fb47-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="3fb47-104">Overview</span></span>
<span data-ttu-id="3fb47-105">Baidu bulut anında iletme, mobil cihazlara anında iletme bildirimleri göndermede kullanabileceğiniz bir Çin bulut hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="3fb47-105">Baidu cloud push is a Chinese cloud service that you can use to send push notifications to mobile devices.</span></span> <span data-ttu-id="3fb47-106">Farklı uygulama mağazalarının ve anında iletme hizmetlerinin varlığı ve de genellikle GCM'ye (Google Cloud Messaging) bağlı olmayan Android cihazlarının kullanılabilirliği nedeniyle, bu hizmet özellikle Android'e anında iletme bildirimleri göndermenin karmaşık olduğu Çin'de kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="3fb47-106">This service is useful in China, where delivering push notifications to Android is complex because of the presence of different app stores and push services, in addition to the availability of Android devices that are not typically connected to GCM (Google Cloud Messaging).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3fb47-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="3fb47-107">Prerequisites</span></span>
<span data-ttu-id="3fb47-108">Bu öğretici için aşağıdakiler gereklidir:</span><span class="sxs-lookup"><span data-stu-id="3fb47-108">This tutorial requires:</span></span>

* <span data-ttu-id="3fb47-109"><a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android sitesinden</a> indirebileceğiniz Android SDK'sı (Eclipse kullanacağınız varsayılır)</span><span class="sxs-lookup"><span data-stu-id="3fb47-109">Android SDK (we assume that you use Eclipse), which you can download from the <a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android site</a></span></span>
* <span data-ttu-id="3fb47-110">[Mobile Services Android SDK'sı]</span><span class="sxs-lookup"><span data-stu-id="3fb47-110">[Mobile Services Android SDK]</span></span>
* <span data-ttu-id="3fb47-111">[Baidu Anında İletme Android SDK’sını]</span><span class="sxs-lookup"><span data-stu-id="3fb47-111">[Baidu Push Android SDK]</span></span>

> [!NOTE]
> <span data-ttu-id="3fb47-112">Bu öğreticiyi tamamlamak için etkin bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3fb47-112">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="3fb47-113">Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3fb47-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="3fb47-114">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-baidu-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="3fb47-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-baidu-get-started%2F).</span></span>
> 
> 

## <a name="create-a-baidu-account"></a><span data-ttu-id="3fb47-115">Bir Baidu hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="3fb47-115">Create a Baidu account</span></span>
<span data-ttu-id="3fb47-116">Baidu kullanmak için bir Baidu hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3fb47-116">To use Baidu, you must have a Baidu account.</span></span> <span data-ttu-id="3fb47-117">Zaten varsa [Baidu portalında] oturum açın ve sonraki adıma atlayın.</span><span class="sxs-lookup"><span data-stu-id="3fb47-117">If you already have one, log in to the [Baidu portal] and skip to the next step.</span></span> <span data-ttu-id="3fb47-118">Aksi halde, bir Baidu hesabının nasıl oluşturulacağı hakkında aşağıdaki yönergelere bakın.</span><span class="sxs-lookup"><span data-stu-id="3fb47-118">Otherwise, see the following instructions on how to create a Baidu account.</span></span>  

1. <span data-ttu-id="3fb47-119">[Baidu portalında] gidin ve **登录** (**Oturum Açma**) bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fb47-119">Go to the [Baidu portal] and click the **登录** (**Login**) link.</span></span> <span data-ttu-id="3fb47-120">Hesap kayıt işlemini başlatmak için **立即注册** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fb47-120">Click **立即注册** to start the account registration process.</span></span>
   
   ![][1]
2. <span data-ttu-id="3fb47-121">Gerekli ayrıntıları girin (telefon/e-posta adresi, parola ve doğrulama kodu) ve **Kaydol**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fb47-121">Enter the required details—phone/email address, password, and verification code—and click **Signup**.</span></span>
   
   ![][2]
3. <span data-ttu-id="3fb47-122">Girdiğiniz e-posta adresine, Baidu hesabınızı etkinleştirmek için bir bağlantıya sahip bir e-posta gönderilir.</span><span class="sxs-lookup"><span data-stu-id="3fb47-122">You will be sent an email to the email address that you entered with a link to activate your Baidu account.</span></span>
   
   ![][3]
4. <span data-ttu-id="3fb47-123">E-posta hesabınızda oturum açın, Baidu etkinleştirme e-postasını açın ve Baidu hesabınızı etkinleştirmek için etkinleştirme bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fb47-123">Log in to your email account, open the Baidu activation mail, and click the activation link to activate your Baidu account.</span></span>
   
   ![][4]

<span data-ttu-id="3fb47-124">Baidu hesabınızı etkinleştirdikten sonra, [Baidu portalında] oturum açın.</span><span class="sxs-lookup"><span data-stu-id="3fb47-124">Once you have an activated Baidu account, log in to the [Baidu portal].</span></span>

## <a name="register-as-a-baidu-developer"></a><span data-ttu-id="3fb47-125">Bir Baidu geliştiricisi olarak kaydolma</span><span class="sxs-lookup"><span data-stu-id="3fb47-125">Register as a Baidu developer</span></span>
1. <span data-ttu-id="3fb47-126">[Baidu portalında] oturum açtıktan sonra, **更多>>** (**daha fazlası**) öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fb47-126">Once you have logged in to the [Baidu portal], click **更多>>** (**more**).</span></span>
   
      ![][5]
2. <span data-ttu-id="3fb47-127">**站长与开发者服务 (Web Uzmanı ve Geliştirici Hizmetleri)** bölümde aşağı kaydırın ve **百度开放云平台** (**Baidu açık bulut platformu**) öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fb47-127">Scroll down in the **站长与开发者服务 (Webmaster and Developer Services)** section and click **百度开放云平台** (**Baidu open cloud platform**).</span></span>
   
      ![][6]
3. <span data-ttu-id="3fb47-128">Sonraki sayfada sağ üst köşedeki **开发者服务** (**Geliştirici Hizmetleri**) öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fb47-128">On the next page, click **开发者服务** (**Developer Services**) on the top-right corner.</span></span>
   
      ![][7]
4. <span data-ttu-id="3fb47-129">Sonraki sayfada sağ üst köşedeki menüden **注册开发者** (**Kayıtlı Geliştiriciler**) öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fb47-129">On the next page, click **注册开发者** (**Registered Developers**) from the menu on the top-right corner.</span></span>
   
      ![][8]
5. <span data-ttu-id="3fb47-130">Bir doğrulama kısa mesajı almak için adınızı, açıklamayı ve cep telefonu numarasını girin ve ardından **送验证码** (**Doğrulama Kodu Gönder**) öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fb47-130">Enter your name, a description, and a mobile phone number for receiving a verification text message, and then click **送验证码** (**Send Verification Code**).</span></span> <span data-ttu-id="3fb47-131">Uluslararası telefon numaraları için ülke kodunu parantez içine almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3fb47-131">For international phone numbers, you need to enclose the country code in parentheses.</span></span> <span data-ttu-id="3fb47-132">Örneğin, bir Amerika Birleşik Devletleri numarası için bu **(1) 1234567890** şeklinde olacaktır.</span><span class="sxs-lookup"><span data-stu-id="3fb47-132">For example, for a United States number, it is **(1)1234567890**.</span></span>
   
      ![][9]
6. <span data-ttu-id="3fb47-133">Ardından, aşağıdaki örnekte gösterildiği gibi bir doğrulama numarasına sahip bir kısa mesaj almanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="3fb47-133">You should then receive a text message with a verification number, as shown in the following example:</span></span>
   
      ![][10]
7. <span data-ttu-id="3fb47-134">İletideki doğrulama numarasını **验证码** (**Doğrulama kodu**) konumuna girin.</span><span class="sxs-lookup"><span data-stu-id="3fb47-134">Enter the verification number from the message in **验证码** (**Confirmation code**).</span></span>
8. <span data-ttu-id="3fb47-135">Son olarak, Baidu sözleşmesini kabul edip **提交** (**Gönder**) öğesine tıklayarak geliştirici kaydını tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="3fb47-135">Finally, complete the developer registration by accepting the Baidu agreement and clicking **提交** (**Submit**).</span></span> <span data-ttu-id="3fb47-136">Kayıt başarılı bir şekilde tamamlandığında aşağıdaki sayfayı görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="3fb47-136">You will see the following page on successful completion of registration:</span></span>
   
      ![][11]

## <a name="create-a-baidu-cloud-push-project"></a><span data-ttu-id="3fb47-137">Bir Baidu bulut anında iletme projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="3fb47-137">Create a Baidu cloud push project</span></span>
<span data-ttu-id="3fb47-138">Bir Baidu bulut anında iletme projesi oluşturduğunuzda, uygulama kimliğinizi, API anahtarınızı ve gizli anahtarınızı alırsınız.</span><span class="sxs-lookup"><span data-stu-id="3fb47-138">When you create a Baidu cloud push project, you receive your app ID, API key, and secret key.</span></span>

1. <span data-ttu-id="3fb47-139">[Baidu portalında] oturum açtıktan sonra, **更多>>** (**daha fazlası**) öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fb47-139">Once you have logged in to the [Baidu portal], click **更多>>** (**more**).</span></span>
   
      ![][5]
2. <span data-ttu-id="3fb47-140">**站长与开发者服务** (**Web Uzmanı ve Geliştirici Hizmetleri**) bölümde aşağı kaydırın ve **百度开放云平台** (**Baidu açık bulut platformu**) öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fb47-140">Scroll down in the **站长与开发者服务** (**Webmaster and Developer Services**) section and click **百度开放云平台** (**Baidu open cloud platform**).</span></span>
   
      ![][6]
3. <span data-ttu-id="3fb47-141">Sonraki sayfada sağ üst köşedeki **开发者服务** (**Geliştirici Hizmetleri**) öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fb47-141">On the next page, click **开发者服务** (**Developer Services**) on the top-right corner.</span></span>
   
      ![][7]
4. <span data-ttu-id="3fb47-142">Sonraki sayfada **云服务** (**Cloud Services**) bölümünden **云推送** (**Bulut Anında İletme**) öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fb47-142">On the next page, click **云推送** (**Cloud Push**) from the **云服务** (**Cloud Services**) section.</span></span>
   
      ![][12]
5. <span data-ttu-id="3fb47-143">Kayıtlı bir geliştirici olduğunuzda, en üstteki menüde **管理控制台** (**Yönetim Konsolu**) öğesini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="3fb47-143">Once you are a registered developer, you see **管理控制台** (**Management Console**) at the top menu.</span></span> <span data-ttu-id="3fb47-144">**开发者服务管理** (**Geliştirici Hizmeti Yönetimi**) öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fb47-144">Click **开发者服务管理** (**Developers Service Management**).</span></span>
   
      ![][13]
6. <span data-ttu-id="3fb47-145">Sonraki sayfada **创建工程** (**Proje Oluşturma**) öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fb47-145">On the next page, click **创建工程** (**Create Project**).</span></span>
   
      ![][14]
7. <span data-ttu-id="3fb47-146">Bir uygulama adı girin ve **创建** (**Oluştur**) öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fb47-146">Enter an application name and click **创建** (**Create**).</span></span>
   
      ![][15]
8. <span data-ttu-id="3fb47-147">Bir Baidu bulut anında iletme projesi başarılı bir şekilde oluşturulduktan sonra, **Uygulama Kimliği**, **API Anahtarı** ve **Gizli Anahtar** değerlerini içeren bir sayfa görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="3fb47-147">Upon successful creation of a Baidu cloud push project, you see a page with **AppID**, **API Key**, and **Secret Key**.</span></span> <span data-ttu-id="3fb47-148">Daha sonra kullanacağımız API anahtarı ve gizli anahtarı not edin.</span><span class="sxs-lookup"><span data-stu-id="3fb47-148">Make a note of the API key and secret key, which we will use later.</span></span>
   
      ![][16]
9. <span data-ttu-id="3fb47-149">Sol bölmedeki **云推送** (**Bulut Anında İletme**) öğesine tıklayarak projeyi anında iletme bildirimleri için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="3fb47-149">Configure the project for push notifications by clicking **云推送** (**Cloud Push**) on the left pane.</span></span>
   
      ![][31]
10. <span data-ttu-id="3fb47-150">Sonraki sayfada **推送设置** (**Anında İletme ayarları**) düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fb47-150">On the next page, click the **推送设置** (**Push settings**) button.</span></span>
    
    ![][32]  
11. <span data-ttu-id="3fb47-151">Yapılandırma sayfasında Android projenizde kullanacağınız paket adını **应用包名** (**Uygulama paketi**) alanına ekleyin ve ardından **保存设置** (**Kaydet**) öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fb47-151">On the configuration page, add the package name that you will be using in your Android project in the **应用包名** (**Application package**) field, and then click **保存设置** (**Save**).</span></span>  
    
    ![][33]

<span data-ttu-id="3fb47-152">Şunu görürsünüz: **保存成功！** (**Başarıyla kaydedildi!**) iletisini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="3fb47-152">You see the **保存成功！** (**Successfully saved!**) message.</span></span>

## <a name="configure-your-notification-hub"></a><span data-ttu-id="3fb47-153">Bildirim hub'ınızı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3fb47-153">Configure your notification hub</span></span>
1. <span data-ttu-id="3fb47-154">[Klasik Azure Portalı]'nda oturum açın ve ardından ekranın alt kısmındaki **+YENİ**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fb47-154">Sign in to the [Azure Classic Portal], and then click **+NEW** at the bottom of the screen.</span></span>
2. <span data-ttu-id="3fb47-155">**Uygulama Hizmetleri**'ne tıklayın, **Service Bus**'a tıklayın, **Notification Hub**'a tıklayın ve ardından **Hızlı Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fb47-155">Click **App Services**, click **Service Bus**, click **Notification Hub**, and then click **Quick Create**.</span></span>
3. <span data-ttu-id="3fb47-156">**Notification Hub**'ınız için bir ad sağlayın, bu bildirim hub'ının oluşturulacağı **Bölge** ve **Ad Alanı**'nı seçin ve ardından **Yeni bir Notification Hub Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fb47-156">Provide a name for your **Notification Hub**, select the **Region** and the **Namespace** where this notification hub will be created, and then click **Create a New Notification Hub**.</span></span>  
   
      ![][17]
4. <span data-ttu-id="3fb47-157">Bildirim hub'ınızı oluşturduğunuz ad alanına tıklayın ve ardından üst kısımdaki **Notification Hubs**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fb47-157">Click the namespace in which you created your notification hub, and then click **Notification Hubs** at the top.</span></span>
   
      ![][18]
5. <span data-ttu-id="3fb47-158">Oluşturduğunuz bildirim hub'ını seçin ve ardından, üstteki menüden **Yapılandır**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fb47-158">Select the notification hub that you created, and then click **Configure** from the top menu.</span></span>
   
      ![][19]
6. <span data-ttu-id="3fb47-159">**Baidu bildirim ayarları** bölümüne doğru aşağı kaydırın ve Baidu bulut anında iletme projeniz için önceden Baidu konsolundan elde ettiğiniz API anahtarını ve gizli anahtarı girin.</span><span class="sxs-lookup"><span data-stu-id="3fb47-159">Scroll down to the **baidu notification settings** section and enter the API key and secret key that you obtained from the Baidu console previously for your Baidu cloud push project.</span></span> <span data-ttu-id="3fb47-160">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fb47-160">Click **Save**.</span></span>
   
      ![][20]
7. <span data-ttu-id="3fb47-161">Bildirim hub'ı için en üstteki **Pano** sekmesine tıklayın ve ardından **Bağlantı Dizesini Görüntüle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fb47-161">Click the **Dashboard** tab at the top for the notification hub, and then click **View Connection String**.</span></span>
   
      ![][21]
8. <span data-ttu-id="3fb47-162">**Erişim bağlantı bilgileri** penceresinde **DefaultListenSharedAccessSignature** ve **DefaultFullSharedAccessSignature**'ı not edin.</span><span class="sxs-lookup"><span data-stu-id="3fb47-162">Make a note of the **DefaultListenSharedAccessSignature** and **DefaultFullSharedAccessSignature** from the **Access connection information** window.</span></span>
   
    ![][22]

## <a name="connect-your-app-to-the-notification-hub"></a><span data-ttu-id="3fb47-163">Uygulamanızı bildirim hub'ına bağlama</span><span class="sxs-lookup"><span data-stu-id="3fb47-163">Connect your app to the notification hub</span></span>
1. <span data-ttu-id="3fb47-164">Eclipse ADT'de yeni bir Android projesi (**Dosya** > **Yeni** > **Android Uygulama Projesi**) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3fb47-164">In Eclipse ADT, create a new Android project (**File** > **New** > **Android Application Project**).</span></span>
   
    ![][23]
2. <span data-ttu-id="3fb47-165">Bir **Uygulama Adı** girin ve **Gereken Minimum SDK** sürümünün **API 16: Android 4.1** olarak ayarlandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="3fb47-165">Enter an **Application Name** and ensure that the **Minimum Required SDK** version is set to **API 16: Android 4.1**.</span></span>
   
    ![][24]
3. <span data-ttu-id="3fb47-166">**İleri**'ye tıklayın ve **Etkinlik Oluştur** penceresi görünene kadar sihirbazı izlemeye devam edin.</span><span class="sxs-lookup"><span data-stu-id="3fb47-166">Click **Next** and continue following the wizard until the **Create Activity** window appears.</span></span> <span data-ttu-id="3fb47-167">**Blank Activity**'nin seçildiğinden emin olun ve son olarak yeni bir Android Uygulaması oluşturmak için **Son**'u seçin.</span><span class="sxs-lookup"><span data-stu-id="3fb47-167">Make sure that **Blank Activity** is selected, and finally select **Finish** to create a new Android Application.</span></span>
   
    ![][25]
4. <span data-ttu-id="3fb47-168">**Proje Derleme Hedefi**'nin doğru ayarlandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="3fb47-168">Make sure that the **Project Build Target** is set correctly.</span></span>
   
    ![][26]
5. <span data-ttu-id="3fb47-169">[Bintray'deki Notification-Hubs-Android-SDK'sının](https://bintray.com/microsoftazuremobile/SDK/Notification-Hubs-Android-SDK/0.4) **Dosyalar** sekmesinden notification-hubs-0.4.jar dosyasını indirin.</span><span class="sxs-lookup"><span data-stu-id="3fb47-169">Download the notification-hubs-0.4.jar file from the **Files** tab of the [Notification-Hubs-Android-SDK on Bintray](https://bintray.com/microsoftazuremobile/SDK/Notification-Hubs-Android-SDK/0.4).</span></span> <span data-ttu-id="3fb47-170">Dosyaları Eclipse projenizin **libs** klasörüne ekleyin ve *libs* klasörünü yenileyin.</span><span class="sxs-lookup"><span data-stu-id="3fb47-170">Add the file to the **libs** folder of your Eclipse project, and refresh the *libs* folder.</span></span>
6. <span data-ttu-id="3fb47-171">[Baidu Anında İletme Android SDK’sını] indirip sıkıştırmasını açın, **libs** klasörünü açın ve ardından Android uygulamanızdaki **libs** klasörüne **pushservice-x.y.z** jar dosyasını ve **armeabi** & **mips** klasörlerini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="3fb47-171">Download and unzip the [Baidu Push Android SDK], open the **libs** folder, and then copy the **pushservice-x.y.z** jar file and the **armeabi** & **mips** folders in the **libs** folder of your Android application.</span></span>
7. <span data-ttu-id="3fb47-172">Android projenizin **AndroidManifest.xml** dosyasını açın ve Baidu SDK'sı için gereken izinleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3fb47-172">Open the **AndroidManifest.xml** file of your Android project and add the permissions that are required by the Baidu SDK.</span></span>
   
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
8. <span data-ttu-id="3fb47-173">**AndroidManifest.xml**'deki **uygulama** öğenize **android:name** özelliğini ekleyip *yourprojectname*'i değiştirin (ör. **com.example.BaiduTest**).</span><span class="sxs-lookup"><span data-stu-id="3fb47-173">Add the **android:name** property to your **application** element in **AndroidManifest.xml**, replacing *yourprojectname* (for example, **com.example.BaiduTest**).</span></span> <span data-ttu-id="3fb47-174">Bu proje adının, Baidu konsolunda yapılandırdığınız adla eşleştiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="3fb47-174">Make sure that this project name matches the one that you configured in the Baidu console.</span></span>
   
        <application android:name="yourprojectname.DemoApplication"
9. <span data-ttu-id="3fb47-175">**.MainActivity** etkinlik öğesinden sonra uygulama öğesinin içine aşağıdaki yapılandırmayı ekleyip *yourprojectname*'i değiştirin (ör. **com.example.BaiduTest**):</span><span class="sxs-lookup"><span data-stu-id="3fb47-175">Add the following configuration within the application element after the **.MainActivity** activity element, replacing *yourprojectname* (for example, **com.example.BaiduTest**):</span></span>
   
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
10. <span data-ttu-id="3fb47-176">Projeye **ConfigurationSettings.java** adlı yeni bir sınıf ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3fb47-176">Add a new class called **ConfigurationSettings.java** to the project.</span></span>
    
     ![][28]
    
     ![][29]
11. <span data-ttu-id="3fb47-177">Buna aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="3fb47-177">Add the following code to it:</span></span>
    
        public class ConfigurationSettings {
                public static String API_KEY = "...";
                public static String NotificationHubName = "...";
                public static String NotificationHubConnectionString = "...";
            }
    
    <span data-ttu-id="3fb47-178">**API_KEY**'i daha önce Baidu bulut projesinden aldığınız değerle, **NotificationHubName**'i Klasik Azure Portalı'ndaki bildirim hub'ı adınızla ve **NotificationHubConnectionString**'i de Klasik Azure Portalı'ndaki DefaultListenSharedAccessSignature ile ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="3fb47-178">Set the value of **API_KEY** with what you retrieved from the Baidu cloud project earlier, **NotificationHubName** with your notification hub name from the Azure Classic Portal and **NotificationHubConnectionString** with DefaultListenSharedAccessSignature from the Azure Classic Portal.</span></span>
12. <span data-ttu-id="3fb47-179">**DemoApplication.java** adlı yeni bir sınıf ekleyin ve bu sınıfa aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="3fb47-179">Add a new class called **DemoApplication.java**, and add the following code to it:</span></span>
    
        import com.baidu.frontia.FrontiaApplication;
    
        public class DemoApplication extends FrontiaApplication {
            @Override
            public void onCreate() {
                super.onCreate();
            }
        }
13. <span data-ttu-id="3fb47-180">**MyPushMessageReceiver.java** adlı başka bir yeni sınıf ekleyin ve bu sınıfa aşağıdaki kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3fb47-180">Add another new class called **MyPushMessageReceiver.java**, and add the following code to it.</span></span> <span data-ttu-id="3fb47-181">Bu, Baidu anında iletme sunucusundan alınan anında iletme bildirimlerini işleyen sınıftır.</span><span class="sxs-lookup"><span data-stu-id="3fb47-181">It is the class that handles the push notifications that are received from the Baidu push server.</span></span>
    
        import java.util.List;
        import android.content.Context;
        import android.os.AsyncTask;
        import android.util.Log;
        import com.baidu.frontia.api.FrontiaPushMessageReceiver;
        import com.microsoft.windowsazure.messaging.NotificationHub;
    
        public class MyPushMessageReceiver extends FrontiaPushMessageReceiver {
            /** TAG to Log */
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
14. <span data-ttu-id="3fb47-182">**MainActivity.java**'yı açın ve aşağıdakini **onCreate** yöntemine ekleyin:</span><span class="sxs-lookup"><span data-stu-id="3fb47-182">Open **MainActivity.java**, and add the following to the **onCreate** method:</span></span>
    
            PushManager.startWork(getApplicationContext(),
                    PushConstants.LOGIN_TYPE_API_KEY, ConfigurationSettings.API_KEY);
15. <span data-ttu-id="3fb47-183">En üstteki içeri aktarma deyimlerini açın:</span><span class="sxs-lookup"><span data-stu-id="3fb47-183">Open the following import statements at the top:</span></span>
    
            import com.baidu.android.pushservice.PushConstants;
            import com.baidu.android.pushservice.PushManager;

## <a name="send-notifications-to-your-app"></a><span data-ttu-id="3fb47-184">Uygulamanıza bildirimler gönderme</span><span class="sxs-lookup"><span data-stu-id="3fb47-184">Send notifications to your app</span></span>
<span data-ttu-id="3fb47-185">Aşağıdaki ekranda gösterildiği [Azure Portal](https://portal.azure.com/)'da bildirim hub’ındaki **Gönder** düğmesini kullanarak uygulamanızda bildirim almayı hızlıca test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3fb47-185">You can quickly test receiving notifications in your app by sending notifications in the [Azure portal](https://portal.azure.com/) using the **Send** button on the notification hub, as shown in the following screen:</span></span>

![](./media/notification-hubs-baidu-get-started/notification-hub-test-send-baidu.png)

<span data-ttu-id="3fb47-186">Anında iletme bildirimleri normalde, uyumlu bir kitaplık kullanılarak Mobile Services veya ASP.NET gibi bir arka uç hizmetinde gönderilir.</span><span class="sxs-lookup"><span data-stu-id="3fb47-186">Push notifications are normally sent in a back-end service like Mobile Services or ASP.NET using a compatible library.</span></span> <span data-ttu-id="3fb47-187">Arka ucunuz için uygun bir kitaplık yoksa bildirim iletilerini göndermek için doğrudan REST API’sini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3fb47-187">If a library is not available for your back-end, you can use the REST API directly to send notification messages .</span></span>

<span data-ttu-id="3fb47-188">Bu öğreticide konuyu basit bir şekilde işleyeceğiz ve yalnızca bir arka uç hizmeti yerine bir konsol uygulamasındaki bildirim hub'ları için .NET SDK ile bildirim göndererek istemci uygulamanızı test etmeyi göstereceğiz.</span><span class="sxs-lookup"><span data-stu-id="3fb47-188">In this tutorial, we keep it simple and just demonstrate testing your client app by sending notifications using the .NET SDK for notification hubs in a console application instead of a backend service.</span></span> <span data-ttu-id="3fb47-189">Bir ASP.NET arka ucundan bildirim göndermek için sonraki adım olarak [Kullanıcılara anında iletme bildirimleri göndermek için Notification Hubs’ı kullanma](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) öğreticisini öneririz.</span><span class="sxs-lookup"><span data-stu-id="3fb47-189">We recommend the [Use Notification Hubs to push notifications to users](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) tutorial as the next step for sending notifications from an ASP.NET backend.</span></span> <span data-ttu-id="3fb47-190">Bununla birlikte, bildirim göndermek için aşağıdaki yaklaşımlar kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="3fb47-190">However, the following approaches can be used for sending notifications:</span></span>

* <span data-ttu-id="3fb47-191">**REST Arabirimi**: [REST arabirimini](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx) kullanarak herhangi bir arka uç platformunda bildirimi destekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3fb47-191">**REST Interface**:  You can support notification on any backend platform using  the [REST interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span></span>
* <span data-ttu-id="3fb47-192">**Microsoft Azure Notification Hubs .NET SDK'sı**: Visual Studio için Nuget Paket Yöneticisi'nde [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="3fb47-192">**Microsoft Azure Notification Hubs .NET SDK**: In the Nuget Package Manager for Visual Studio, run [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>
* <span data-ttu-id="3fb47-193">**Node.js**: [Node.js'den Notification Hubs'ı kullanma](notification-hubs-nodejs-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="3fb47-193">**Node.js**: [How to use Notification Hubs from Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span></span>
* <span data-ttu-id="3fb47-194">**Mobile Apps**: Notification Hubs ile tümleştirilmiş Azure Uygulama Hizmeti Mobile Apps arka ucundan nasıl bildirim gönderildiğinin bir örneği için bkz. [Mobil uygulamalarınıza anında iletme bildirimleri ekleme](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="3fb47-194">**Mobile Apps**: For an example of how to send notifications from an Azure App Service Mobile Apps backend that's integrated with Notification Hubs, see [Add push notifications to your mobile app](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).</span></span>
* <span data-ttu-id="3fb47-195">**Java/PHP**: REST API'ler kullanarak nasıl bildirim gönderildiğinin bir örneği için bkz. "Java/PHP'den Notification Hubs'ı kullanma"([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span><span class="sxs-lookup"><span data-stu-id="3fb47-195">**Java / PHP**: For an example of how to send notifications by using the REST APIs, see "How to use Notification Hubs from Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span></span>

## <a name="optional-send-notifications-from-a-net-console-app"></a><span data-ttu-id="3fb47-196">(İsteğe bağlı) Bir .NET konsol uygulamasından bildirim gönderme</span><span class="sxs-lookup"><span data-stu-id="3fb47-196">(Optional) Send notifications from a .NET console app.</span></span>
<span data-ttu-id="3fb47-197">Bu bölümde, bir .NET konsol uygulaması kullanarak bildirim göndermeyi göstereceğiz.</span><span class="sxs-lookup"><span data-stu-id="3fb47-197">In this section, we show sending a notification using a .NET console app.</span></span>

1. <span data-ttu-id="3fb47-198">Yeni bir Visual C# konsol uygulaması oluşturun:</span><span class="sxs-lookup"><span data-stu-id="3fb47-198">Create a new Visual C# console application:</span></span>
   
    ![][30]
2. <span data-ttu-id="3fb47-199">Paket Yöneticisi Konsolu penceresinde, **Varsayılan projeyi** yeni konsol uygulaması projeniz olarak ayarlayın ve ardından konsol penceresinde aşağıdaki komutu yürütün:</span><span class="sxs-lookup"><span data-stu-id="3fb47-199">In the Package Manager Console window, set the **Default project** to your new console application project, and then in the console window, execute the following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="3fb47-200">Bu yönerge, <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet paketini</a> kullanarak Azure Notification Hubs SDK'sına bir başvuru ekler.</span><span class="sxs-lookup"><span data-stu-id="3fb47-200">This instruction adds a reference to the Azure Notification Hubs SDK using the <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
3. <span data-ttu-id="3fb47-201">**Program.cs**'yi açın ve aşağıdaki kullanım deyimini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="3fb47-201">Open the file **Program.cs** and add the following using statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
4. <span data-ttu-id="3fb47-202">`Program` sınıfınızda, aşağıdaki yöntemi ekleyin ve *DefaultFullSharedAccessSignatureSASConnectionString* ve *NotificationHubName* değerlerini sizdeki değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="3fb47-202">In your `Program` class, add the following method and replace *DefaultFullSharedAccessSignatureSASConnectionString* and *NotificationHubName* with the values that you have.</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("DefaultFullSharedAccessSignatureSASConnectionString", "NotificationHubName");
            string message = "{\"title\":\"((Notification title))\",\"description\":\"Hello from Azure\"}";
            var result = await hub.SendBaiduNativeNotificationAsync(message);
        }
5. <span data-ttu-id="3fb47-203">Aşağıdaki satırları **Main** yönteminize ekleyin:</span><span class="sxs-lookup"><span data-stu-id="3fb47-203">Add the following lines in your **Main** method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();

## <a name="test-your-app"></a><span data-ttu-id="3fb47-204">Uygulamanızı test etme</span><span class="sxs-lookup"><span data-stu-id="3fb47-204">Test your app</span></span>
<span data-ttu-id="3fb47-205">Bu uygulamayı gerçek bir telefonla test etmek için telefonu bir USB kablosu kullanarak bilgisayarınıza bağlamanız yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="3fb47-205">To test this app with an actual phone, just connect the phone to your computer by using a USB cable.</span></span> <span data-ttu-id="3fb47-206">Bu işlem uygulamanızı iliştirilmiş telefona yükler.</span><span class="sxs-lookup"><span data-stu-id="3fb47-206">This action loads your app onto the attached phone.</span></span>

<span data-ttu-id="3fb47-207">Bu uygulamayı öykünücüyle test etmek için, Eclipse üst araç çubuğunda **Çalıştır**'a tıklayın ve ardından uygulamanızı seçin: öykünücü başlatılır, uygulama yüklenir ve çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="3fb47-207">To test this app with the emulator, on the Eclipse top toolbar, click **Run**, and then select your app: it starts the emulator, loads, and runs the app.</span></span>

<span data-ttu-id="3fb47-208">Uygulama, Baidu Anında iletme bildirimi hizmetinden 'userId' ve 'channelId' alır ve bildirim hub'ı ile kaydeder.</span><span class="sxs-lookup"><span data-stu-id="3fb47-208">The app retrieves the 'userId' and 'channelId' from the Baidu Push notification service and registers with the notification hub.</span></span>

<span data-ttu-id="3fb47-209">Bir test bildirimi göndermek için, Klasik Azure Portalı'nın hata ayıklama sekmesini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3fb47-209">To send a test notification, you can use the debug tab of the Azure Classic Portal.</span></span> <span data-ttu-id="3fb47-210">Visual Studio için .NET konsol uygulamasını oluşturduysanız uygulamayı çalıştırmak için Visual Studio'da F5 tuşuna basmanız yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="3fb47-210">If you built the .NET console application for Visual Studio, just press the F5 key in Visual Studio to run the application.</span></span> <span data-ttu-id="3fb47-211">Uygulama, cihazınızın veya öykünücünüzün bildirim alanının üst kısmında görünecek bir bildirim gönderir.</span><span class="sxs-lookup"><span data-stu-id="3fb47-211">The application sends a notification that appears in the top notification area of your device or emulator.</span></span>

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
<span data-ttu-id="3fb47-212">[Mobile Services Android SDK'sı]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409</span><span class="sxs-lookup"><span data-stu-id="3fb47-212">[Mobile Services Android SDK]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409</span></span>
<span data-ttu-id="3fb47-213">[Baidu Anında İletme Android SDK’sını]: http://developer.baidu.com/wiki/index.php?title=docs/cplat/push/sdk/clientsdk</span><span class="sxs-lookup"><span data-stu-id="3fb47-213">[Baidu Push Android SDK]: http://developer.baidu.com/wiki/index.php?title=docs/cplat/push/sdk/clientsdk</span></span>
<span data-ttu-id="3fb47-214">[Klasik Azure Portalı]: https://manage.windowsazure.com/</span><span class="sxs-lookup"><span data-stu-id="3fb47-214">[Azure Classic Portal]: https://manage.windowsazure.com/</span></span>
<span data-ttu-id="3fb47-215">[Baidu portalında]: http://www.baidu.com/</span><span class="sxs-lookup"><span data-stu-id="3fb47-215">[Baidu portal]: http://www.baidu.com/</span></span>
