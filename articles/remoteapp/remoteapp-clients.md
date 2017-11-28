---
title: "Herhangi bir aygıttan uygulamalarınıza erişme | Microsoft Docs"
description: "Hangi istemcilerin Azure RemoteApp için desteklenir ve uygulamalarınıza erişmek nasıl öğrenin."
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
ms.openlocfilehash: 10a5be6251765b59fac92a33120cedcf8091a677
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="accessing-your-apps-in-azure-remoteapp"></a><span data-ttu-id="cf924-103">Azure RemoteApp içindeki uygulamalarınıza erişim</span><span class="sxs-lookup"><span data-stu-id="cf924-103">Accessing your apps in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="cf924-104">Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="cf924-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="cf924-105">Ayrıntılı bilgi için [duyuruyu](https://go.microsoft.com/fwlink/?linkid=821148) okuyun.</span><span class="sxs-lookup"><span data-stu-id="cf924-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="cf924-106">Azure RemoteApp beauties herhangi aygıtlarınızın uygulamaları erişebilir biridir.</span><span class="sxs-lookup"><span data-stu-id="cf924-106">One of the beauties of Azure RemoteApp is that you can access apps from any of your devices.</span></span> <span data-ttu-id="cf924-107">Bile daha iyi bir cihazda çalışmaya başlamak ve ikinci bir cihaz sorunsuz geçiş ve kullanabilirsiniz kaldığınız yerden yukarı sola çekme.</span><span class="sxs-lookup"><span data-stu-id="cf924-107">Even better, you can start working on one device and then seamlessly transition to a second device and pick up right where you left off.</span></span> <span data-ttu-id="cf924-108">Başlamak için cihazınız için uygun istemci yükleme ve hizmete oturum açmak gerekir.</span><span class="sxs-lookup"><span data-stu-id="cf924-108">To get started you need to download the appropriate client for your device and sign in to the service.</span></span>

<span data-ttu-id="cf924-109">Bu konuda, sizi şu anda desteklenen istemciler ve ı RemoteApp her istemcilerin oturum açma göstermeden önce bunları indirmek nasıl gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="cf924-109">In this topic, we'll review the clients currently supported and how to download them before I show you how to sign in to RemoteApp from each of the clients.</span></span>

## <a name="supported-clients"></a><span data-ttu-id="cf924-110">Desteklenen istemciler</span><span class="sxs-lookup"><span data-stu-id="cf924-110">Supported clients</span></span>
<span data-ttu-id="cf924-111">RemoteApp Cihazınızı bu işletim sistemlerinden birini çalıştıran, aşağıdaki adımları kullanarak erişebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="cf924-111">You can access RemoteApp using the steps below if your device is running one of these operating systems:</span></span>

* <span data-ttu-id="cf924-112">Windows 10</span><span class="sxs-lookup"><span data-stu-id="cf924-112">Windows 10</span></span> 
* <span data-ttu-id="cf924-113">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="cf924-113">Windows 8.1</span></span>
* <span data-ttu-id="cf924-114">Windows 8</span><span class="sxs-lookup"><span data-stu-id="cf924-114">Windows 8</span></span>
* <span data-ttu-id="cf924-115">Windows 7 Service Pack 1</span><span class="sxs-lookup"><span data-stu-id="cf924-115">Windows 7 Service Pack 1</span></span>
* <span data-ttu-id="cf924-116">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="cf924-116">Windows Phone 8.1</span></span>
* <span data-ttu-id="cf924-117">iOS</span><span class="sxs-lookup"><span data-stu-id="cf924-117">iOS</span></span>
* <span data-ttu-id="cf924-118">Mac OS X</span><span class="sxs-lookup"><span data-stu-id="cf924-118">Mac OS X</span></span>
* <span data-ttu-id="cf924-119">Android</span><span class="sxs-lookup"><span data-stu-id="cf924-119">Android</span></span>

 <span data-ttu-id="cf924-120">Küçük boyutlu istemciler hakkında neler?</span><span class="sxs-lookup"><span data-stu-id="cf924-120">What about thin clients?</span></span> <span data-ttu-id="cf924-121">Aşağıdaki Windows Embedded ince istemciler desteklenir:</span><span class="sxs-lookup"><span data-stu-id="cf924-121">The following Windows Embedded thin clients are supported:</span></span>

* <span data-ttu-id="cf924-122">Windows Embedded Standard 7</span><span class="sxs-lookup"><span data-stu-id="cf924-122">Windows Embedded Standard 7</span></span>
* <span data-ttu-id="cf924-123">Windows Embedded 8 Standard</span><span class="sxs-lookup"><span data-stu-id="cf924-123">Windows Embedded 8 Standard</span></span>
* <span data-ttu-id="cf924-124">Windows Embedded 8.1 Industry Pro</span><span class="sxs-lookup"><span data-stu-id="cf924-124">Windows Embedded 8.1 Industry Pro</span></span>
* <span data-ttu-id="cf924-125">Windows 10 IoT Enterprise</span><span class="sxs-lookup"><span data-stu-id="cf924-125">Windows 10 IoT Enterprise</span></span>

## <a name="downloading-the-client"></a><span data-ttu-id="cf924-126">İstemci Yükleme</span><span class="sxs-lookup"><span data-stu-id="cf924-126">Downloading the client</span></span>
<span data-ttu-id="cf924-127">Kullanmakta olduğunuz hangi platformu olsun RemoteApp erişmek için gereken istemci bulunabilir [Uzak Masaüstü İstemcisi indirme](https://www.remoteapp.windowsazure.com/ClientDownload/AllClients.aspx) sayfası.</span><span class="sxs-lookup"><span data-stu-id="cf924-127">No matter what platform you are using, the client you need to access RemoteApp can be found on the [Remote Desktop client download](https://www.remoteapp.windowsazure.com/ClientDownload/AllClients.aspx) page.</span></span>

<span data-ttu-id="cf924-128">Farklı bağlantıları tıklatarak ya da doğrudan istemci indirme başlatılacak veya sayfa, platform için uygulama mağazasında bulunan istemciye indirdiğiniz gönderir.</span><span class="sxs-lookup"><span data-stu-id="cf924-128">Clicking the different links will either directly start downloading the client or will send you to the client download page in the app store for that platform.</span></span> <span data-ttu-id="cf924-129">Ekrandaki yönergeleri izleyerek istemciyi yükleyin.</span><span class="sxs-lookup"><span data-stu-id="cf924-129">Install the client by following the instructions on the screen.</span></span>

<span data-ttu-id="cf924-130">İstemci aygıtınızda yüklü ve bu başlatıldıktan sonra Bu istemciden RemoteApp oturum açmak öğrenmek için aşağıdaki ilgili bölümüne geçin.</span><span class="sxs-lookup"><span data-stu-id="cf924-130">Once you have installed the client on your device and launched it, jump to the corresponding section below to learn how to sign in to RemoteApp from that client.</span></span>

## <a name="android"></a><span data-ttu-id="cf924-131">Android</span><span class="sxs-lookup"><span data-stu-id="cf924-131">Android</span></span>
<span data-ttu-id="cf924-132">Google Play Mağazası'ndan Microsoft Uzak Masaüstü uygulamasını yükledikten sonra bu uygulama listenizde altında bulabilirsiniz **Uzak Masaüstü**.</span><span class="sxs-lookup"><span data-stu-id="cf924-132">Once you have installed the Microsoft Remote Desktop app from the Google Play store, you can find it in your app list under **Remote Desktop**.</span></span>

1. <span data-ttu-id="cf924-133">Zaten uygulamayı kullanmakta olduğunuz sürece uygulamasını başlatarak boş bir bağlantı merkezine getirir.</span><span class="sxs-lookup"><span data-stu-id="cf924-133">Launching the app brings you to an empty Connection Center, unless you've already been using the app.</span></span> <span data-ttu-id="cf924-134">Azure RemoteApp ile çalışmaya başlamak için Ekle düğmesine dokunun **"" +""** ve dokunun **Azure RemoteApp**.</span><span class="sxs-lookup"><span data-stu-id="cf924-134">To get started with Azure RemoteApp, tap the add button **""+""** and tap **Azure RemoteApp**.</span></span>    
   
     ![Boş bağlantı Merkezi](./media/remoteapp-clients/Android1.png)
2. <span data-ttu-id="cf924-136">Hizmete erişmek için e-posta adresinizi oturum oturum açmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="cf924-136">You need to sign in with your email address to access the service.</span></span> <span data-ttu-id="cf924-137">Dokunun **başlama**.</span><span class="sxs-lookup"><span data-stu-id="cf924-137">Tap **Get started**.</span></span>
   
    ![Komut isteminde oturum](./media/remoteapp-clients/Android2.png)
3. <span data-ttu-id="cf924-139">Sonraki sayfada yazın, **e-posta adresi** ve dokunun **devam**.</span><span class="sxs-lookup"><span data-stu-id="cf924-139">On the next page, type in your **email address** and tap **Continue**.</span></span> <span data-ttu-id="cf924-140">Bu, Azure Active Directory'yi kullanarak oturum açma işlemi başlar.</span><span class="sxs-lookup"><span data-stu-id="cf924-140">This begins the sign-in process using Azure Active Directory.</span></span>
   
    ![İlk Azure Active Directory sayfası](./media/remoteapp-clients/Android3.png)
4. <span data-ttu-id="cf924-142">Microsoft hesabı (daha önce "LiveID" denir) veya kuruluş kimliği oturum açmanız için ekrandaki yönergeleri izleyin</span><span class="sxs-lookup"><span data-stu-id="cf924-142">Follow the instructions on the screen to sign in with your Microsoft account (previously called "LiveID") or organization ID.</span></span> <span data-ttu-id="cf924-143">Oturum açtıktan sonra aldığınız tüm davetleri listelendiği bir sayfa ile sunulan.</span><span class="sxs-lookup"><span data-stu-id="cf924-143">Once signed in, you may be presented with a page listing all the invitations you have received.</span></span> <span data-ttu-id="cf924-144">Varsa, güven ve dokunun davetleri seçin **Bitti**.</span><span class="sxs-lookup"><span data-stu-id="cf924-144">If you are, select the invitations you trust and tap **Done**.</span></span>    
   
    ![Davetiye sayfası](./media/remoteapp-clients/Android4.png)
5. <span data-ttu-id="cf924-146">Davetleri kabul ettikten sonra erişiminiz uygulamalar listesini, cihaza indirilip ve olması bağlantı Merkezi'nde kullanılabilir hale.</span><span class="sxs-lookup"><span data-stu-id="cf924-146">After accepting your invitations, the list of apps you have access to will be downloaded to your device and made available in the Connection Center.</span></span> <span data-ttu-id="cf924-147">Bir uygulama, kullanmaya başlamak için dokunun.</span><span class="sxs-lookup"><span data-stu-id="cf924-147">Tap one of the apps to start using it.</span></span>
   
    ![Bir akış ile bağlantı Merkezi](./media/remoteapp-clients/Android5.png)
6. <span data-ttu-id="cf924-149">Davetiye henüz yoksa servisi hala deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cf924-149">If you do not have an invitation yet, you can still try out the service.</span></span> <span data-ttu-id="cf924-150">Bunu yapmak için dokunun **ücretsiz deneme sürümü için Git** istendiğinde.</span><span class="sxs-lookup"><span data-stu-id="cf924-150">To do so, tap **Go to free trial** when prompted.</span></span>
   
    ![Komut isteminde akış Tanıtımı](./media/remoteapp-clients/Android6.png)
7. <span data-ttu-id="cf924-152">Bu, RemoteApp ile başlamanıza yardımcı olmak için uygulamaların temel bir dizi erişmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="cf924-152">This will give you access to a basic set of apps to get you started with RemoteApp.</span></span>
   
    ![Azure RemoteApp için akış Tanıtımı](./media/remoteapp-clients/Android7.png)

## <a name="ios"></a><span data-ttu-id="cf924-154">iOS</span><span class="sxs-lookup"><span data-stu-id="cf924-154">iOS</span></span>
<span data-ttu-id="cf924-155">Uygulama Mağazası'ndan Microsoft Uzak Masaüstü uygulamasını yükledikten sonra bu uygulama listenizde altında bulabilirsiniz **RD istemcisini**.</span><span class="sxs-lookup"><span data-stu-id="cf924-155">Once you have installed the Microsoft Remote Desktop app from the App store, you can find it in your app list under **RD Client**.</span></span>

1. <span data-ttu-id="cf924-156">Zaten uygulamayı kullanmakta olduğunuz sürece uygulamasını başlatarak boş bir bağlantı merkezine getirir.</span><span class="sxs-lookup"><span data-stu-id="cf924-156">Launching the app brings you to an empty Connection Center, unless you've already been using the app.</span></span> <span data-ttu-id="cf924-157">Azure RemoteApp ile çalışmaya başlamak için Ekle düğmesine dokunun **"" +""** ve dokunun **eklemek Azure RemoteApp**.</span><span class="sxs-lookup"><span data-stu-id="cf924-157">To get started with Azure RemoteApp, tap the add button **""+""** and tap **Add Azure RemoteApp**.</span></span>
   
    ![Boş bağlantı Merkezi](./media/remoteapp-clients/IOS1.png)
2. <span data-ttu-id="cf924-159">Bu işlemi başlatmak için hizmete erişmek için e-posta adresinizi oturum imzalamak için yazmanız, **e-posta adresi** ve dokunun **devam**.</span><span class="sxs-lookup"><span data-stu-id="cf924-159">You need to sign in with your email address to access the service, to start that process, type in your **email address** and tap **Continue**.</span></span>
   
    ![Komut isteminde oturum](./media/remoteapp-clients/picture1.png)
3. <span data-ttu-id="cf924-161">Microsoft hesabı (LiveId) veya kuruluş kimliği oturum açmanız için ekrandaki yönergeleri izleyin</span><span class="sxs-lookup"><span data-stu-id="cf924-161">Follow the instructions on the screen to sign in with your Microsoft account (LiveID) or Organization ID.</span></span> <span data-ttu-id="cf924-162">Oturum açtıktan sonra aldığınız tüm davetleri listelendiği bir sayfa ile sunulan.</span><span class="sxs-lookup"><span data-stu-id="cf924-162">Once signed in, you may be presented with a page listing all the invitations you have received.</span></span> <span data-ttu-id="cf924-163">Varsa, güven ve dokunun davetleri seçin **Bitti**.</span><span class="sxs-lookup"><span data-stu-id="cf924-163">If you are, select the invitations you trust and tap **Done**.</span></span>
   
    ![Davetiye sayfası](./media/remoteapp-clients/IOS3.png)
4. <span data-ttu-id="cf924-165">Davetleri kabul ettikten sonra erişiminiz uygulamalar listesini, cihaza indirilip ve olması bağlantı Merkezi'nde kullanılabilir hale.</span><span class="sxs-lookup"><span data-stu-id="cf924-165">After accepting your invitations, the list of apps you have access to will be downloaded to your device and made available in the Connection Center.</span></span> <span data-ttu-id="cf924-166">Bir uygulama başlatın ve kullanmaya başlamak için dokunun.</span><span class="sxs-lookup"><span data-stu-id="cf924-166">Tap one of the apps to launch it and start using it.</span></span>
   
    ![Bir akış ile bağlantı Merkezi](./media/remoteapp-clients/IOS4.png)
5. <span data-ttu-id="cf924-168">Davetiye henüz yoksa servisi hala deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cf924-168">If you do not have an invitation yet, you can still try out the service.</span></span> <span data-ttu-id="cf924-169">Bunu yapmak için dokunun **ücretsiz deneme sürümü için Git** istendiğinde.</span><span class="sxs-lookup"><span data-stu-id="cf924-169">To do so, tap **Go to free trial** when prompted.</span></span>
   
    ![Komut isteminde akış Tanıtımı](./media/remoteapp-clients/IOS5.png)
6. <span data-ttu-id="cf924-171">Bu, RemoteApp ile başlamanıza yardımcı olmak için uygulamaların temel bir dizi erişmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="cf924-171">This will give you access to a basic set of apps to get you started with RemoteApp.</span></span>
   
    ![Azure RemoteApp için akış Tanıtımı](./media/remoteapp-clients/IOS6.png)

## <a name="mac-os-x"></a><span data-ttu-id="cf924-173">Mac OS X</span><span class="sxs-lookup"><span data-stu-id="cf924-173">Mac OS X</span></span>
<span data-ttu-id="cf924-174">Uygulama Mağazası'ndan Microsoft Uzak Masaüstü uygulamasını yükledikten sonra bu uygulama listenizde altında bulabilirsiniz **Microsoft Uzak Masaüstü**.</span><span class="sxs-lookup"><span data-stu-id="cf924-174">Once you have installed the Microsoft Remote Desktop app from the App store, you can find it in your app list under **Microsoft Remote Desktop**.</span></span>

1. <span data-ttu-id="cf924-175">Zaten uygulamayı kullanmakta olduğunuz sürece uygulamasını başlatarak boş bir bağlantı merkezine getirir.</span><span class="sxs-lookup"><span data-stu-id="cf924-175">Launching the app brings you to an empty Connection Center, unless you've already been using the app.</span></span> <span data-ttu-id="cf924-176">Azure RemoteApp ile kullanmaya başlamak için tıklayın **Azure RemoteApp** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="cf924-176">To get started with Azure RemoteApp, click the **Azure RemoteApp** button.</span></span>
   
    ![Boş bağlantı Merkezi](./media/remoteapp-clients/Mac1.png)
2. <span data-ttu-id="cf924-178">Bu işlemi başlatmak için hizmete erişmek için e-posta adresinizi oturum imzalamak için dokunun **Get Started**.</span><span class="sxs-lookup"><span data-stu-id="cf924-178">You need to sign in with your email address to access the service, to start that process, tap **Get Started**.</span></span>
   
    ![Komut isteminde oturum](./media/remoteapp-clients/Mac2.png)
3. <span data-ttu-id="cf924-180">Sonraki sayfada yazın, **e-posta adresi** ve dokunun **devam**.</span><span class="sxs-lookup"><span data-stu-id="cf924-180">On the next page, type in your **email address** and tap **Continue**.</span></span> <span data-ttu-id="cf924-181">Bu oturum açma Azure Active Directory'yi kullanarak işlemine başlar.</span><span class="sxs-lookup"><span data-stu-id="cf924-181">This begins the sign in process using Azure Active Directory.</span></span>
   
    ![İlk Azure Active Directory sayfası](./media/remoteapp-clients/picture2.png)
4. <span data-ttu-id="cf924-183">Microsoft hesabı (LiveId) veya kuruluş kimliği oturum açmanız için ekrandaki yönergeleri izleyin</span><span class="sxs-lookup"><span data-stu-id="cf924-183">Follow the instructions on the screen to sign in with your Microsoft account (LiveID) or Organization ID.</span></span> <span data-ttu-id="cf924-184">Oturum açtıktan sonra aldığınız tüm davetleri listelendiği bir sayfa ile sunulan.</span><span class="sxs-lookup"><span data-stu-id="cf924-184">Once signed in, you may be presented with a page listing all the invitations you have received.</span></span> <span data-ttu-id="cf924-185">Varsa, güven ve iletişim kutusunu kapatın davetleri seçin.</span><span class="sxs-lookup"><span data-stu-id="cf924-185">If you are, select the invitations you trust and close the dialog.</span></span>
   
    ![Davetiye sayfası](./media/remoteapp-clients/Mac4.png)
5. <span data-ttu-id="cf924-187">Davetleri kabul ettikten sonra erişiminiz uygulamalar listesini, cihaza indirilip ve olması bağlantı Merkezi'nde kullanılabilir hale.</span><span class="sxs-lookup"><span data-stu-id="cf924-187">After accepting your invitations, the list of apps you have access to will be downloaded to your device and made available in the Connection Center.</span></span> <span data-ttu-id="cf924-188">Bir uygulama başlatın ve kullanmaya başlamak için çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cf924-188">Double-click one of the apps to launch it and start using it.</span></span>
   
    ![Bir akış ile bağlantı Merkezi](./media/remoteapp-clients/Mac5.png)
6. <span data-ttu-id="cf924-190">Davetiye henüz yoksa servisi hala deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cf924-190">If you do not have an invitation yet, you can still try out the service.</span></span> <span data-ttu-id="cf924-191">Bunu yapmak için tıklatın **ücretsiz deneme sürümü için Git** istendiğinde.</span><span class="sxs-lookup"><span data-stu-id="cf924-191">To do so, click **Go to free trial** when prompted.</span></span>
   
    ![Komut isteminde akış Tanıtımı](./media/remoteapp-clients/Mac6.png)
7. <span data-ttu-id="cf924-193">Bu, RemoteApp ile başlamanıza yardımcı olmak için uygulamaların temel bir dizi erişmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="cf924-193">This will give you access to a basic set of apps to get you started with RemoteApp.</span></span>
   
    ![Azure RemoteApp için akış Tanıtımı](./media/remoteapp-clients/Mac7.png)

## <a name="windows-all-supported-versions-except-windows-phone"></a><span data-ttu-id="cf924-195">Windows (Windows Phone hariç desteklenen tüm sürümleri)</span><span class="sxs-lookup"><span data-stu-id="cf924-195">Windows (All supported versions except Windows Phone)</span></span>
<span data-ttu-id="cf924-196">Yükleme, erişim gerektiğinde ancak daha sonra yeniden şu adla uygulama listenizde bulunabilir bittikten sonra istemci otomatik olarak başlatır **Azure RemoteApp**.</span><span class="sxs-lookup"><span data-stu-id="cf924-196">The client launches automatically after it finishes installing, however when you need to access it again later it can be found in your app list under the name **Azure RemoteApp**.</span></span>

1. <span data-ttu-id="cf924-197">İstemci, gördüğünüz ilk sayfa başlatma onra Azure RemoteApp beklemektedir.</span><span class="sxs-lookup"><span data-stu-id="cf924-197">Ater launching the client, the first page you see welcomes you to Azure RemoteApp.</span></span> <span data-ttu-id="cf924-198">Devam etmek için tıklayın **Get Started**.</span><span class="sxs-lookup"><span data-stu-id="cf924-198">To proceed, click on **Get Started**.</span></span>
   
    ![Azure RemoteApp istemcisi Karşılama sayfası](./media/remoteapp-clients/Windows1.png)
2. <span data-ttu-id="cf924-200">Sonraki sayfada, Azure Active Directory'yi kullanarak Azure RemoteApp için işleminde oturum başlatır.</span><span class="sxs-lookup"><span data-stu-id="cf924-200">The next page starts the sign in process for Azure RemoteApp using Azure Active Directory.</span></span> <span data-ttu-id="cf924-201">Bu işlem Microsoft Hizmetleri geçmişte kullandıysanız, tanıdık gelecektir.</span><span class="sxs-lookup"><span data-stu-id="cf924-201">This process should look familiar if you have used Microsoft services in the past.</span></span> <span data-ttu-id="cf924-202">Başlangıç yazarak, **e-posta adresi** tıklatıp **devam**.</span><span class="sxs-lookup"><span data-stu-id="cf924-202">Start by typing your **email address** and click **Continue**.</span></span>
   
    ![İlk Azure Active Directory istemi](./media/remoteapp-clients/Windows2.png)
3. <span data-ttu-id="cf924-204">Microsoft hesabı (LiveId) veya kuruluş kimliği oturum açmanız için ekrandaki yönergeleri izleyin</span><span class="sxs-lookup"><span data-stu-id="cf924-204">Follow the instructions on the screen to sign in with your Microsoft account (LiveID) or Organization ID.</span></span> <span data-ttu-id="cf924-205">Oturum açtıktan sonra aldığınız tüm davetleri listelendiği bir sayfa ile sunulan.</span><span class="sxs-lookup"><span data-stu-id="cf924-205">Once signed in, you may be presented with a page listing all the invitations you have received.</span></span> <span data-ttu-id="cf924-206">Varsa, güven ve tıklayın davetleri seçin **Bitti**.</span><span class="sxs-lookup"><span data-stu-id="cf924-206">If you are, select the invitations you trust and click **Done**.</span></span>
   
    ![Azure RemoteApp istemci davetleri sayfası](./media/remoteapp-clients/Windows3.png)
4. <span data-ttu-id="cf924-208">Davetleri kabul ettikten sonra erişiminiz uygulamalar listesini, cihaza indirilip ve olması bağlantı Merkezi'nde kullanılabilir hale.</span><span class="sxs-lookup"><span data-stu-id="cf924-208">After accepting your invitations, the list of apps you have access to will be downloaded to your device and made available in the Connection Center.</span></span> <span data-ttu-id="cf924-209">Bir uygulama başlatın ve kullanmaya başlamak için çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cf924-209">Double-click one of the apps to launch it and start using it.</span></span>
   
    ![Azure RemoteApp istemcinin bağlantı Merkezi](./media/remoteapp-clients/Windows4.png)
5. <span data-ttu-id="cf924-211">Hiç kimse, henüz bir davet göndermişse, endişelenmeyin biz, kapsamdaki var!</span><span class="sxs-lookup"><span data-stu-id="cf924-211">If no one has sent you an invitation yet, don't worry we've got you covered!</span></span> <span data-ttu-id="cf924-212">Dolayısıyla servisi test yine demo koleksiyona erişimi gerekir.</span><span class="sxs-lookup"><span data-stu-id="cf924-212">You'll still have access to a demo collection so you can test out the service.</span></span>
   
    ![Azure RemoteApp için akış Tanıtımı](./media/remoteapp-clients/Windows5.png)

## <a name="windows-phone-81"></a><span data-ttu-id="cf924-214">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="cf924-214">Windows Phone 8.1</span></span>
<span data-ttu-id="cf924-215">Windows Phone 8.1 Mağaza'dan Microsoft Uzak Masaüstü uygulamasını yükledikten sonra bu uygulama listenizde altında bulabilirsiniz **Uzak Masaüstü**.</span><span class="sxs-lookup"><span data-stu-id="cf924-215">Once you have installed the Microsoft Remote Desktop app from the Windows Phone 8.1 store, you can find it in your app list under **Remote Desktop**.</span></span>

1. <span data-ttu-id="cf924-216">Zaten uygulamayı kullanmakta olduğunuz sürece uygulamasını başlatarak doğrudan bir boş bağlantı merkezine getirir.</span><span class="sxs-lookup"><span data-stu-id="cf924-216">Launching the app brings you directly to an empty Connection Center, unless you've already been using the app.</span></span> <span data-ttu-id="cf924-217">Azure RemoteApp ile çalışmaya başlamak için Ekle düğmesine dokunun **"" +""** ekranın altındaki.</span><span class="sxs-lookup"><span data-stu-id="cf924-217">To get started with Azure RemoteApp, tap the add button **""+""** at the bottom of the screen.</span></span>
   
    ![Boş bağlantı Merkezi](./media/remoteapp-clients/WinPhone1.png)
2. <span data-ttu-id="cf924-219">Ardından, seçeneğine dokunun **Azure RemoteApp**.</span><span class="sxs-lookup"><span data-stu-id="cf924-219">Next, tap on **Azure RemoteApp**.</span></span>
   
    ![Öğe bir sayfa ekleyin](./media/remoteapp-clients/WinPhone2.png)
3. <span data-ttu-id="cf924-221">Bu işlemi başlatmak için hizmete erişmek için e-posta adresinizi oturum imzalamak için dokunun **bağlanmak**.</span><span class="sxs-lookup"><span data-stu-id="cf924-221">You need to sign in with your email address to access the service, to start that process, tap **connect**.</span></span>
   
    ![Komut isteminde oturum](./media/remoteapp-clients/WinPhone3.png)
4. <span data-ttu-id="cf924-223">Sonraki sayfada yazın, **e-posta adresi** ve dokunun **devam**.</span><span class="sxs-lookup"><span data-stu-id="cf924-223">On the next page, type in your **email address** and tap **Continue**.</span></span> <span data-ttu-id="cf924-224">Bu oturum açma Azure Active Directory'yi kullanarak işlemine başlar.</span><span class="sxs-lookup"><span data-stu-id="cf924-224">This begins the sign in process using Azure Active Directory.</span></span>
   
    ![İlk Azure Active Directory sayfası](./media/remoteapp-clients/WinPhone4.png)
5. <span data-ttu-id="cf924-226">Microsoft hesabı (LiveId) veya kuruluş kimliği oturum açmanız için ekrandaki yönergeleri izleyin</span><span class="sxs-lookup"><span data-stu-id="cf924-226">Follow the instructions on the screen to sign in with your Microsoft account (LiveID) or Organization ID.</span></span> <span data-ttu-id="cf924-227">Oturum açtıktan sonra aldığınız tüm davetleri listelendiği bir sayfa ile sunulan.</span><span class="sxs-lookup"><span data-stu-id="cf924-227">Once signed in, you may be presented with a page listing all the invitations you have received.</span></span> <span data-ttu-id="cf924-228">Varsa, güven ve dokunun davetleri seçin **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="cf924-228">If you are, select the invitations you trust and tap **save**.</span></span>
   
    ![Davetiye sayfası](./media/remoteapp-clients/WinPhone5.png)
6. <span data-ttu-id="cf924-230">Davetleri kabul ettikten sonra erişiminiz uygulamalar listesini, cihaza indirilip ve olması bağlantı Merkezi'nde kullanılabilir hale.</span><span class="sxs-lookup"><span data-stu-id="cf924-230">After accepting your invitations, the list of apps you have access to will be downloaded to your device and made available in the Connection Center.</span></span> <span data-ttu-id="cf924-231">Bir uygulama başlatın ve kullanmaya başlamak için dokunun.</span><span class="sxs-lookup"><span data-stu-id="cf924-231">Tap one of the apps to launch it and start using it.</span></span>
   
    ![Bir akış ile bağlantı Merkezi](./media/remoteapp-clients/WinPhone6.png)
7. <span data-ttu-id="cf924-233">Davetiye henüz yoksa servisi hala deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cf924-233">If you do not have an invitation yet, you can still try out the service.</span></span> <span data-ttu-id="cf924-234">Bunu yapmak için dokunun **Evet** istendiğinde.</span><span class="sxs-lookup"><span data-stu-id="cf924-234">To do so, tap **yes** when prompted.</span></span>
   
    ![Komut isteminde akış Tanıtımı](./media/remoteapp-clients/WinPhone7.png)
8. <span data-ttu-id="cf924-236">Bu, RemoteApp ile başlamanıza yardımcı olmak için uygulamaların temel bir dizi erişmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="cf924-236">This will give you access to a basic set of apps to get you started with RemoteApp.</span></span>
   
    ![Azure RemoteApp için akış Tanıtımı](./media/remoteapp-clients/WinPhone8.png)

