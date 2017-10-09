---
title: "aaaAccessing uygulamalarınızı herhangi bir CİHAZDAN | Microsoft Docs"
description: "Hangi istemcilerin Azure RemoteApp için desteklendiğini öğrenin ve nasıl tooaccess uygulamalarınızı."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: fb7bd17d-7aa8-43fd-9278-f96e0e9308e4
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 15985b40d870e3155d4132063bf5b9677ff9afed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-your-apps-in-azure-remoteapp"></a><span data-ttu-id="14f09-103">Azure RemoteApp içindeki uygulamalarınıza erişim</span><span class="sxs-lookup"><span data-stu-id="14f09-103">Accessing your apps in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="14f09-104">Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="14f09-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="14f09-105">Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="14f09-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="14f09-106">Azure RemoteApp hello beauties herhangi aygıtlarınızın uygulamaları erişebilir biridir.</span><span class="sxs-lookup"><span data-stu-id="14f09-106">One of hello beauties of Azure RemoteApp is that you can access apps from any of your devices.</span></span> <span data-ttu-id="14f09-107">Bile daha iyi bir cihazda çalışmaya başlamak ve tooa ikinci bir cihaz sorunsuz geçiş ve kullanabilirsiniz kaldığınız yerden yukarı sola seçin.</span><span class="sxs-lookup"><span data-stu-id="14f09-107">Even better, you can start working on one device and then seamlessly transition tooa second device and pick up right where you left off.</span></span> <span data-ttu-id="14f09-108">tooget başlatılan toodownload hello uygun istemci cihazınız için gereken ve toohello hizmetinde oturum açın.</span><span class="sxs-lookup"><span data-stu-id="14f09-108">tooget started you need toodownload hello appropriate client for your device and sign in toohello service.</span></span>

<span data-ttu-id="14f09-109">Bu konuda, sizi şu anda desteklenen hello istemciler gözden geçirin ve nasıl toodownload bunları ı bunu nasıl yapacağınızı önce her hello istemcilerin tooRemoteApp toosign.</span><span class="sxs-lookup"><span data-stu-id="14f09-109">In this topic, we'll review hello clients currently supported and how toodownload them before I show you how toosign in tooRemoteApp from each of hello clients.</span></span>

## <a name="supported-clients"></a><span data-ttu-id="14f09-110">Desteklenen istemciler</span><span class="sxs-lookup"><span data-stu-id="14f09-110">Supported clients</span></span>
<span data-ttu-id="14f09-111">RemoteApp Cihazınızı bu işletim sistemlerinden birini çalıştıran hello adımları kullanarak erişebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="14f09-111">You can access RemoteApp using hello steps below if your device is running one of these operating systems:</span></span>

* <span data-ttu-id="14f09-112">Windows 10</span><span class="sxs-lookup"><span data-stu-id="14f09-112">Windows 10</span></span> 
* <span data-ttu-id="14f09-113">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="14f09-113">Windows 8.1</span></span>
* <span data-ttu-id="14f09-114">Windows 8</span><span class="sxs-lookup"><span data-stu-id="14f09-114">Windows 8</span></span>
* <span data-ttu-id="14f09-115">Windows 7 Service Pack 1</span><span class="sxs-lookup"><span data-stu-id="14f09-115">Windows 7 Service Pack 1</span></span>
* <span data-ttu-id="14f09-116">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="14f09-116">Windows Phone 8.1</span></span>
* <span data-ttu-id="14f09-117">iOS</span><span class="sxs-lookup"><span data-stu-id="14f09-117">iOS</span></span>
* <span data-ttu-id="14f09-118">Mac OS X</span><span class="sxs-lookup"><span data-stu-id="14f09-118">Mac OS X</span></span>
* <span data-ttu-id="14f09-119">Android</span><span class="sxs-lookup"><span data-stu-id="14f09-119">Android</span></span>

 <span data-ttu-id="14f09-120">Küçük boyutlu istemciler hakkında neler? Windows Embedded ince istemcileri aşağıdaki hello desteklenir:</span><span class="sxs-lookup"><span data-stu-id="14f09-120">What about thin clients? hello following Windows Embedded thin clients are supported:</span></span>

* <span data-ttu-id="14f09-121">Windows Embedded Standard 7</span><span class="sxs-lookup"><span data-stu-id="14f09-121">Windows Embedded Standard 7</span></span>
* <span data-ttu-id="14f09-122">Windows Embedded 8 Standard</span><span class="sxs-lookup"><span data-stu-id="14f09-122">Windows Embedded 8 Standard</span></span>
* <span data-ttu-id="14f09-123">Windows Embedded 8.1 Industry Pro</span><span class="sxs-lookup"><span data-stu-id="14f09-123">Windows Embedded 8.1 Industry Pro</span></span>
* <span data-ttu-id="14f09-124">Windows 10 IoT Enterprise</span><span class="sxs-lookup"><span data-stu-id="14f09-124">Windows 10 IoT Enterprise</span></span>

## <a name="downloading-hello-client"></a><span data-ttu-id="14f09-125">Merhaba istemci indirme</span><span class="sxs-lookup"><span data-stu-id="14f09-125">Downloading hello client</span></span>
<span data-ttu-id="14f09-126">Hangi platformu olsun, kullanmakta olduğunuz, RemoteApp hello üzerinde bulunabilir tooaccess ihtiyacınız hello istemci [Uzak Masaüstü İstemcisi indirme](https://www.remoteapp.windowsazure.com/ClientDownload/AllClients.aspx) sayfası.</span><span class="sxs-lookup"><span data-stu-id="14f09-126">No matter what platform you are using, hello client you need tooaccess RemoteApp can be found on hello [Remote Desktop client download](https://www.remoteapp.windowsazure.com/ClientDownload/AllClients.aspx) page.</span></span>

<span data-ttu-id="14f09-127">Tıklatmak hello farklı bağlantılar ya da doğrudan hello istemci indirme başlatılacak veya o platform için hello uygulama mağazasında toohello istemcisi indirme sayfasından gönderir.</span><span class="sxs-lookup"><span data-stu-id="14f09-127">Clicking hello different links will either directly start downloading hello client or will send you toohello client download page in hello app store for that platform.</span></span> <span data-ttu-id="14f09-128">Merhaba ekranında hello yönergeleri izleyerek Hello istemcisini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="14f09-128">Install hello client by following hello instructions on hello screen.</span></span>

<span data-ttu-id="14f09-129">Merhaba istemci aygıtınızda yüklü ve bu başlatıldıktan sonra toohello karşılık gelen bölüme toolearn aşağıda nasıl Atla Bu istemciden gelen tooRemoteApp toosign.</span><span class="sxs-lookup"><span data-stu-id="14f09-129">Once you have installed hello client on your device and launched it, jump toohello corresponding section below toolearn how toosign in tooRemoteApp from that client.</span></span>

## <a name="android"></a><span data-ttu-id="14f09-130">Android</span><span class="sxs-lookup"><span data-stu-id="14f09-130">Android</span></span>
<span data-ttu-id="14f09-131">Google Play mağazasına hello hello Microsoft Uzak Masaüstü uygulaması yüklendikten sonra bu uygulama listenizi altında bulabilirsiniz **Uzak Masaüstü**.</span><span class="sxs-lookup"><span data-stu-id="14f09-131">Once you have installed hello Microsoft Remote Desktop app from hello Google Play store, you can find it in your app list under **Remote Desktop**.</span></span>

1. <span data-ttu-id="14f09-132">Zaten hello uygulama kullanmakta olduğunuz sürece başlatan hello uygulama tooan boş bağlantı merkezi getirir.</span><span class="sxs-lookup"><span data-stu-id="14f09-132">Launching hello app brings you tooan empty Connection Center, unless you've already been using hello app.</span></span> <span data-ttu-id="14f09-133">Azure RemoteApp kullanmaya başlamanıza tooget dokunun hello Ekle düğmesi **"" +""** ve dokunun **Azure RemoteApp**.</span><span class="sxs-lookup"><span data-stu-id="14f09-133">tooget started with Azure RemoteApp, tap hello add button **""+""** and tap **Azure RemoteApp**.</span></span>    
   
     ![Boş bağlantı Merkezi](./media/remoteapp-clients/Android1.png)
2. <span data-ttu-id="14f09-135">E-posta adresi tooaccess hello hizmetinizi oturum toosign gerekir.</span><span class="sxs-lookup"><span data-stu-id="14f09-135">You need toosign in with your email address tooaccess hello service.</span></span> <span data-ttu-id="14f09-136">Dokunun **başlama**.</span><span class="sxs-lookup"><span data-stu-id="14f09-136">Tap **Get started**.</span></span>
   
    ![Komut isteminde oturum](./media/remoteapp-clients/Android2.png)
3. <span data-ttu-id="14f09-138">Merhaba sonraki sayfada yazın, **e-posta adresi** ve dokunun **devam**.</span><span class="sxs-lookup"><span data-stu-id="14f09-138">On hello next page, type in your **email address** and tap **Continue**.</span></span> <span data-ttu-id="14f09-139">Azure Active Directory kullanılarak hello oturum açma işlemi başlar.</span><span class="sxs-lookup"><span data-stu-id="14f09-139">This begins hello sign-in process using Azure Active Directory.</span></span>
   
    ![İlk Azure Active Directory sayfası](./media/remoteapp-clients/Android3.png)
4. <span data-ttu-id="14f09-141">Microsoft hesabınızı (daha önce "LiveID" denir) ya da kuruluş kimliği oturum Merhaba ekranında toosign Hello yönergeleri izleyin</span><span class="sxs-lookup"><span data-stu-id="14f09-141">Follow hello instructions on hello screen toosign in with your Microsoft account (previously called "LiveID") or organization ID.</span></span> <span data-ttu-id="14f09-142">Oturum açtıktan sonra aldığınız tüm hello davetleri listelendiği bir sayfa ile sunulan.</span><span class="sxs-lookup"><span data-stu-id="14f09-142">Once signed in, you may be presented with a page listing all hello invitations you have received.</span></span> <span data-ttu-id="14f09-143">Varsa, güven ve dokunun hello davetleri seçin **Bitti**.</span><span class="sxs-lookup"><span data-stu-id="14f09-143">If you are, select hello invitations you trust and tap **Done**.</span></span>    
   
    ![Davetiye sayfası](./media/remoteapp-clients/Android4.png)
5. <span data-ttu-id="14f09-145">Kabul davetleri, uygulamaların hello listesini sonra indirilen tooyour aygıt erişim toowill sahip ve hello bağlantı merkezi kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="14f09-145">After accepting your invitations, hello list of apps you have access toowill be downloaded tooyour device and made available in hello Connection Center.</span></span> <span data-ttu-id="14f09-146">Merhaba uygulamaları toostart kullanmadan birine dokunun.</span><span class="sxs-lookup"><span data-stu-id="14f09-146">Tap one of hello apps toostart using it.</span></span>
   
    ![Bir akış ile bağlantı Merkezi](./media/remoteapp-clients/Android5.png)
6. <span data-ttu-id="14f09-148">Davetiye henüz yoksa hello servisi hala deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="14f09-148">If you do not have an invitation yet, you can still try out hello service.</span></span> <span data-ttu-id="14f09-149">Bu nedenle, toodo dokunun **Git toofree deneme** istendiğinde.</span><span class="sxs-lookup"><span data-stu-id="14f09-149">toodo so, tap **Go toofree trial** when prompted.</span></span>
   
    ![Komut isteminde akış Tanıtımı](./media/remoteapp-clients/Android6.png)
7. <span data-ttu-id="14f09-151">Bu verecektir erişim tooa temel kümesi uygulamaları tooget RemoteApp ile başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="14f09-151">This will give you access tooa basic set of apps tooget you started with RemoteApp.</span></span>
   
    ![Azure RemoteApp için akış Tanıtımı](./media/remoteapp-clients/Android7.png)

## <a name="ios"></a><span data-ttu-id="14f09-153">iOS</span><span class="sxs-lookup"><span data-stu-id="14f09-153">iOS</span></span>
<span data-ttu-id="14f09-154">Merhaba uygulama Mağazası'ndan hello Microsoft Uzak Masaüstü uygulaması yüklendikten sonra bu uygulama listenizi altında bulabilirsiniz **RD istemcisini**.</span><span class="sxs-lookup"><span data-stu-id="14f09-154">Once you have installed hello Microsoft Remote Desktop app from hello App store, you can find it in your app list under **RD Client**.</span></span>

1. <span data-ttu-id="14f09-155">Zaten hello uygulama kullanmakta olduğunuz sürece başlatan hello uygulama tooan boş bağlantı merkezi getirir.</span><span class="sxs-lookup"><span data-stu-id="14f09-155">Launching hello app brings you tooan empty Connection Center, unless you've already been using hello app.</span></span> <span data-ttu-id="14f09-156">Azure RemoteApp kullanmaya başlamanıza tooget dokunun hello Ekle düğmesi **"" +""** ve dokunun **eklemek Azure RemoteApp**.</span><span class="sxs-lookup"><span data-stu-id="14f09-156">tooget started with Azure RemoteApp, tap hello add button **""+""** and tap **Add Azure RemoteApp**.</span></span>
   
    ![Boş bağlantı Merkezi](./media/remoteapp-clients/IOS1.png)
2. <span data-ttu-id="14f09-158">Bu işlem türü e-posta adresi tooaccess hello hizmetinizi oturum toostart toosign gerekir, **e-posta adresi** ve dokunun **devam**.</span><span class="sxs-lookup"><span data-stu-id="14f09-158">You need toosign in with your email address tooaccess hello service, toostart that process, type in your **email address** and tap **Continue**.</span></span>
   
    ![Komut isteminde oturum](./media/remoteapp-clients/picture1.png)
3. <span data-ttu-id="14f09-160">Microsoft hesabı (LiveId) veya kuruluş kimliği oturum Merhaba ekranında toosign Hello yönergeleri izleyin</span><span class="sxs-lookup"><span data-stu-id="14f09-160">Follow hello instructions on hello screen toosign in with your Microsoft account (LiveID) or Organization ID.</span></span> <span data-ttu-id="14f09-161">Oturum açtıktan sonra aldığınız tüm hello davetleri listelendiği bir sayfa ile sunulan.</span><span class="sxs-lookup"><span data-stu-id="14f09-161">Once signed in, you may be presented with a page listing all hello invitations you have received.</span></span> <span data-ttu-id="14f09-162">Varsa, güven ve dokunun hello davetleri seçin **Bitti**.</span><span class="sxs-lookup"><span data-stu-id="14f09-162">If you are, select hello invitations you trust and tap **Done**.</span></span>
   
    ![Davetiye sayfası](./media/remoteapp-clients/IOS3.png)
4. <span data-ttu-id="14f09-164">Kabul davetleri, uygulamaların hello listesini sonra indirilen tooyour aygıt erişim toowill sahip ve hello bağlantı merkezi kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="14f09-164">After accepting your invitations, hello list of apps you have access toowill be downloaded tooyour device and made available in hello Connection Center.</span></span> <span data-ttu-id="14f09-165">Merhaba uygulamaları toolaunch birine ve onu kullanan başlangıç dokunun.</span><span class="sxs-lookup"><span data-stu-id="14f09-165">Tap one of hello apps toolaunch it and start using it.</span></span>
   
    ![Bir akış ile bağlantı Merkezi](./media/remoteapp-clients/IOS4.png)
5. <span data-ttu-id="14f09-167">Davetiye henüz yoksa hello servisi hala deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="14f09-167">If you do not have an invitation yet, you can still try out hello service.</span></span> <span data-ttu-id="14f09-168">Bu nedenle, toodo dokunun **Git toofree deneme** istendiğinde.</span><span class="sxs-lookup"><span data-stu-id="14f09-168">toodo so, tap **Go toofree trial** when prompted.</span></span>
   
    ![Komut isteminde akış Tanıtımı](./media/remoteapp-clients/IOS5.png)
6. <span data-ttu-id="14f09-170">Bu verecektir erişim tooa temel kümesi uygulamaları tooget RemoteApp ile başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="14f09-170">This will give you access tooa basic set of apps tooget you started with RemoteApp.</span></span>
   
    ![Azure RemoteApp için akış Tanıtımı](./media/remoteapp-clients/IOS6.png)

## <a name="mac-os-x"></a><span data-ttu-id="14f09-172">Mac OS X</span><span class="sxs-lookup"><span data-stu-id="14f09-172">Mac OS X</span></span>
<span data-ttu-id="14f09-173">Merhaba uygulama Mağazası'ndan hello Microsoft Uzak Masaüstü uygulaması yüklendikten sonra bu uygulama listenizi altında bulabilirsiniz **Microsoft Uzak Masaüstü**.</span><span class="sxs-lookup"><span data-stu-id="14f09-173">Once you have installed hello Microsoft Remote Desktop app from hello App store, you can find it in your app list under **Microsoft Remote Desktop**.</span></span>

1. <span data-ttu-id="14f09-174">Zaten hello uygulama kullanmakta olduğunuz sürece başlatan hello uygulama tooan boş bağlantı merkezi getirir.</span><span class="sxs-lookup"><span data-stu-id="14f09-174">Launching hello app brings you tooan empty Connection Center, unless you've already been using hello app.</span></span> <span data-ttu-id="14f09-175">Azure RemoteApp kullanmaya başlamanıza tooget tıklatın hello **Azure RemoteApp** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="14f09-175">tooget started with Azure RemoteApp, click hello **Azure RemoteApp** button.</span></span>
   
    ![Boş bağlantı Merkezi](./media/remoteapp-clients/Mac1.png)
2. <span data-ttu-id="14f09-177">Toosign gereken e-posta adresi tooaccess hello hizmetinizi oturum işlemek, toostart dokunun **Get Started**.</span><span class="sxs-lookup"><span data-stu-id="14f09-177">You need toosign in with your email address tooaccess hello service, toostart that process, tap **Get Started**.</span></span>
   
    ![Komut isteminde oturum](./media/remoteapp-clients/Mac2.png)
3. <span data-ttu-id="14f09-179">Merhaba sonraki sayfada yazın, **e-posta adresi** ve dokunun **devam**.</span><span class="sxs-lookup"><span data-stu-id="14f09-179">On hello next page, type in your **email address** and tap **Continue**.</span></span> <span data-ttu-id="14f09-180">Merhaba oturum açma Azure Active Directory'yi kullanarak işlemine başlar.</span><span class="sxs-lookup"><span data-stu-id="14f09-180">This begins hello sign in process using Azure Active Directory.</span></span>
   
    ![İlk Azure Active Directory sayfası](./media/remoteapp-clients/picture2.png)
4. <span data-ttu-id="14f09-182">Microsoft hesabı (LiveId) veya kuruluş kimliği oturum Merhaba ekranında toosign Hello yönergeleri izleyin</span><span class="sxs-lookup"><span data-stu-id="14f09-182">Follow hello instructions on hello screen toosign in with your Microsoft account (LiveID) or Organization ID.</span></span> <span data-ttu-id="14f09-183">Oturum açtıktan sonra aldığınız tüm hello davetleri listelendiği bir sayfa ile sunulan.</span><span class="sxs-lookup"><span data-stu-id="14f09-183">Once signed in, you may be presented with a page listing all hello invitations you have received.</span></span> <span data-ttu-id="14f09-184">Varsa, güven ve hello iletişim kutusunu kapatmak hello davetleri seçin.</span><span class="sxs-lookup"><span data-stu-id="14f09-184">If you are, select hello invitations you trust and close hello dialog.</span></span>
   
    ![Davetiye sayfası](./media/remoteapp-clients/Mac4.png)
5. <span data-ttu-id="14f09-186">Kabul davetleri, uygulamaların hello listesini sonra indirilen tooyour aygıt erişim toowill sahip ve hello bağlantı merkezi kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="14f09-186">After accepting your invitations, hello list of apps you have access toowill be downloaded tooyour device and made available in hello Connection Center.</span></span> <span data-ttu-id="14f09-187">Merhaba uygulamaları toolaunch birini çift tıklatın ve onu kullanmaya başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="14f09-187">Double-click one of hello apps toolaunch it and start using it.</span></span>
   
    ![Bir akış ile bağlantı Merkezi](./media/remoteapp-clients/Mac5.png)
6. <span data-ttu-id="14f09-189">Davetiye henüz yoksa hello servisi hala deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="14f09-189">If you do not have an invitation yet, you can still try out hello service.</span></span> <span data-ttu-id="14f09-190">Bu nedenle, toodo'ı tıklatın **Git toofree deneme** istendiğinde.</span><span class="sxs-lookup"><span data-stu-id="14f09-190">toodo so, click **Go toofree trial** when prompted.</span></span>
   
    ![Komut isteminde akış Tanıtımı](./media/remoteapp-clients/Mac6.png)
7. <span data-ttu-id="14f09-192">Bu verecektir erişim tooa temel kümesi uygulamaları tooget RemoteApp ile başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="14f09-192">This will give you access tooa basic set of apps tooget you started with RemoteApp.</span></span>
   
    ![Azure RemoteApp için akış Tanıtımı](./media/remoteapp-clients/Mac7.png)

## <a name="windows-all-supported-versions-except-windows-phone"></a><span data-ttu-id="14f09-194">Windows (Windows Phone hariç desteklenen tüm sürümleri)</span><span class="sxs-lookup"><span data-stu-id="14f09-194">Windows (All supported versions except Windows Phone)</span></span>
<span data-ttu-id="14f09-195">Yükleme tooaccess gerektiğinde ancak bunu daha sonra yeniden şu uygulama listenizde hello adı altında bulunabilir bittikten sonra hello istemci otomatik olarak başlatır **Azure RemoteApp**.</span><span class="sxs-lookup"><span data-stu-id="14f09-195">hello client launches automatically after it finishes installing, however when you need tooaccess it again later it can be found in your app list under hello name **Azure RemoteApp**.</span></span>

1. <span data-ttu-id="14f09-196">Merhaba istemci, gördüğünüz hello ilk sayfa başlatma onra tooAzure RemoteApp beklemektedir.</span><span class="sxs-lookup"><span data-stu-id="14f09-196">Ater launching hello client, hello first page you see welcomes you tooAzure RemoteApp.</span></span> <span data-ttu-id="14f09-197">tooproceed, tıklatıldığında **Get Started**.</span><span class="sxs-lookup"><span data-stu-id="14f09-197">tooproceed, click on **Get Started**.</span></span>
   
    ![Hello Azure RemoteApp istemcisi Karşılama sayfası](./media/remoteapp-clients/Windows1.png)
2. <span data-ttu-id="14f09-199">Hello sonraki sayfa, Azure Active Directory'yi kullanarak Azure RemoteApp için işleminde hello oturum başlatır.</span><span class="sxs-lookup"><span data-stu-id="14f09-199">hello next page starts hello sign in process for Azure RemoteApp using Azure Active Directory.</span></span> <span data-ttu-id="14f09-200">Bu işlem Microsoft Hizmetleri hello geçmiş kullandıysanız, tanıdık gelecektir.</span><span class="sxs-lookup"><span data-stu-id="14f09-200">This process should look familiar if you have used Microsoft services in hello past.</span></span> <span data-ttu-id="14f09-201">Başlangıç yazarak, **e-posta adresi** tıklatıp **devam**.</span><span class="sxs-lookup"><span data-stu-id="14f09-201">Start by typing your **email address** and click **Continue**.</span></span>
   
    ![İlk Azure Active Directory istemi](./media/remoteapp-clients/Windows2.png)
3. <span data-ttu-id="14f09-203">Microsoft hesabı (LiveId) veya kuruluş kimliği oturum Merhaba ekranında toosign Hello yönergeleri izleyin</span><span class="sxs-lookup"><span data-stu-id="14f09-203">Follow hello instructions on hello screen toosign in with your Microsoft account (LiveID) or Organization ID.</span></span> <span data-ttu-id="14f09-204">Oturum açtıktan sonra aldığınız tüm hello davetleri listelendiği bir sayfa ile sunulan.</span><span class="sxs-lookup"><span data-stu-id="14f09-204">Once signed in, you may be presented with a page listing all hello invitations you have received.</span></span> <span data-ttu-id="14f09-205">Varsa, güven ve tıklayın hello davetleri seçin **Bitti**.</span><span class="sxs-lookup"><span data-stu-id="14f09-205">If you are, select hello invitations you trust and click **Done**.</span></span>
   
    ![Hello Azure RemoteApp istemci davetleri sayfası](./media/remoteapp-clients/Windows3.png)
4. <span data-ttu-id="14f09-207">Kabul davetleri, uygulamaların hello listesini sonra indirilen tooyour aygıt erişim toowill sahip ve hello bağlantı merkezi kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="14f09-207">After accepting your invitations, hello list of apps you have access toowill be downloaded tooyour device and made available in hello Connection Center.</span></span> <span data-ttu-id="14f09-208">Merhaba uygulamaları toolaunch birini çift tıklatın ve onu kullanmaya başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="14f09-208">Double-click one of hello apps toolaunch it and start using it.</span></span>
   
    ![Bağlantı merkezi hello Azure RemoteApp istemcisi](./media/remoteapp-clients/Windows4.png)
5. <span data-ttu-id="14f09-210">Hiç kimse, henüz bir davet göndermişse, endişelenmeyin biz, kapsamdaki var!</span><span class="sxs-lookup"><span data-stu-id="14f09-210">If no one has sent you an invitation yet, don't worry we've got you covered!</span></span> <span data-ttu-id="14f09-211">Dolayısıyla hello servisi test erişim tooa demo koleksiyonu hala sahip olacaksınız.</span><span class="sxs-lookup"><span data-stu-id="14f09-211">You'll still have access tooa demo collection so you can test out hello service.</span></span>
   
    ![Azure RemoteApp için akış Tanıtımı](./media/remoteapp-clients/Windows5.png)

## <a name="windows-phone-81"></a><span data-ttu-id="14f09-213">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="14f09-213">Windows Phone 8.1</span></span>
<span data-ttu-id="14f09-214">Merhaba Windows Phone 8.1 Mağazası'ndan hello Microsoft Uzak Masaüstü uygulaması yüklendikten sonra bu uygulama listenizi altında bulabilirsiniz **Uzak Masaüstü**.</span><span class="sxs-lookup"><span data-stu-id="14f09-214">Once you have installed hello Microsoft Remote Desktop app from hello Windows Phone 8.1 store, you can find it in your app list under **Remote Desktop**.</span></span>

1. <span data-ttu-id="14f09-215">Zaten hello uygulama kullanmakta olduğunuz sürece başlatan hello uygulama, doğrudan bağlantı merkezi boş tooan, getirir.</span><span class="sxs-lookup"><span data-stu-id="14f09-215">Launching hello app brings you directly tooan empty Connection Center, unless you've already been using hello app.</span></span> <span data-ttu-id="14f09-216">Azure RemoteApp kullanmaya başlamanıza tooget dokunun hello Ekle düğmesi **"" +""** Merhaba ekranında hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="14f09-216">tooget started with Azure RemoteApp, tap hello add button **""+""** at hello bottom of hello screen.</span></span>
   
    ![Boş bağlantı Merkezi](./media/remoteapp-clients/WinPhone1.png)
2. <span data-ttu-id="14f09-218">Ardından, seçeneğine dokunun **Azure RemoteApp**.</span><span class="sxs-lookup"><span data-stu-id="14f09-218">Next, tap on **Azure RemoteApp**.</span></span>
   
    ![Öğe bir sayfa ekleyin](./media/remoteapp-clients/WinPhone2.png)
3. <span data-ttu-id="14f09-220">Toosign gereken e-posta adresi tooaccess hello hizmetinizi oturum işlemek, toostart dokunun **bağlanmak**.</span><span class="sxs-lookup"><span data-stu-id="14f09-220">You need toosign in with your email address tooaccess hello service, toostart that process, tap **connect**.</span></span>
   
    ![Komut isteminde oturum](./media/remoteapp-clients/WinPhone3.png)
4. <span data-ttu-id="14f09-222">Merhaba sonraki sayfada yazın, **e-posta adresi** ve dokunun **devam**.</span><span class="sxs-lookup"><span data-stu-id="14f09-222">On hello next page, type in your **email address** and tap **Continue**.</span></span> <span data-ttu-id="14f09-223">Merhaba oturum açma Azure Active Directory'yi kullanarak işlemine başlar.</span><span class="sxs-lookup"><span data-stu-id="14f09-223">This begins hello sign in process using Azure Active Directory.</span></span>
   
    ![İlk Azure Active Directory sayfası](./media/remoteapp-clients/WinPhone4.png)
5. <span data-ttu-id="14f09-225">Microsoft hesabı (LiveId) veya kuruluş kimliği oturum Merhaba ekranında toosign Hello yönergeleri izleyin</span><span class="sxs-lookup"><span data-stu-id="14f09-225">Follow hello instructions on hello screen toosign in with your Microsoft account (LiveID) or Organization ID.</span></span> <span data-ttu-id="14f09-226">Oturum açtıktan sonra aldığınız tüm hello davetleri listelendiği bir sayfa ile sunulan.</span><span class="sxs-lookup"><span data-stu-id="14f09-226">Once signed in, you may be presented with a page listing all hello invitations you have received.</span></span> <span data-ttu-id="14f09-227">Varsa, güven ve dokunun hello davetleri seçin **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="14f09-227">If you are, select hello invitations you trust and tap **save**.</span></span>
   
    ![Davetiye sayfası](./media/remoteapp-clients/WinPhone5.png)
6. <span data-ttu-id="14f09-229">Kabul davetleri, uygulamaların hello listesini sonra indirilen tooyour aygıt erişim toowill sahip ve hello bağlantı merkezi kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="14f09-229">After accepting your invitations, hello list of apps you have access toowill be downloaded tooyour device and made available in hello Connection Center.</span></span> <span data-ttu-id="14f09-230">Merhaba uygulamaları toolaunch birine ve onu kullanan başlangıç dokunun.</span><span class="sxs-lookup"><span data-stu-id="14f09-230">Tap one of hello apps toolaunch it and start using it.</span></span>
   
    ![Bir akış ile bağlantı Merkezi](./media/remoteapp-clients/WinPhone6.png)
7. <span data-ttu-id="14f09-232">Davetiye henüz yoksa hello servisi hala deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="14f09-232">If you do not have an invitation yet, you can still try out hello service.</span></span> <span data-ttu-id="14f09-233">Bu nedenle, toodo dokunun **Evet** istendiğinde.</span><span class="sxs-lookup"><span data-stu-id="14f09-233">toodo so, tap **yes** when prompted.</span></span>
   
    ![Komut isteminde akış Tanıtımı](./media/remoteapp-clients/WinPhone7.png)
8. <span data-ttu-id="14f09-235">Bu verecektir erişim tooa temel kümesi uygulamaları tooget RemoteApp ile başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="14f09-235">This will give you access tooa basic set of apps tooget you started with RemoteApp.</span></span>
   
    ![Azure RemoteApp için akış Tanıtımı](./media/remoteapp-clients/WinPhone8.png)

