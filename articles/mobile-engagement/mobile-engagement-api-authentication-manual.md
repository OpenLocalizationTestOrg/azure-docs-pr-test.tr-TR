---
title: "Mobile Engagement REST API'leri ile - el ile kuruluma kimlik doğrulaması"
description: "El ile kimlik doğrulaması için Mobile Engagement REST API'leri Kurulum açıklar"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2e79f9c9-41e4-45ac-b427-3b8338675163
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 9d6132e1a01be489b8e8e28a0219cf8a0b50b318
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="authenticate-with-mobile-engagement-rest-apis---manual-setup"></a><span data-ttu-id="8eae5-103">Mobile Engagement REST API'leri ile - el ile kuruluma kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="8eae5-103">Authenticate with Mobile Engagement REST APIs - manual setup</span></span>
<span data-ttu-id="8eae5-104">Bir ek belgelerine budur [Mobile Engagement REST API'leri ile kimlik doğrulama](mobile-engagement-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="8eae5-104">This is an appendix documentation to [Authenticate with Mobile Engagement REST APIs](mobile-engagement-api-authentication.md).</span></span> <span data-ttu-id="8eae5-105">İlk içerik Al okuma emin olun.</span><span class="sxs-lookup"><span data-stu-id="8eae5-105">Make sure you read it first to get the context.</span></span> <span data-ttu-id="8eae5-106">Bu, kimlik doğrulaması için Azure Portalı'nı kullanarak Mobile Engagement REST API'leri ayarlamak için tek seferlik kurulumu yapmak için alternatif bir yolu açıklar.</span><span class="sxs-lookup"><span data-stu-id="8eae5-106">This describes an alternate way to do the One-time setup for setting up your authentication for the Mobile Engagement REST APIs using the Azure Portal.</span></span> 

> [!NOTE]
> <span data-ttu-id="8eae5-107">Aşağıdaki yönergeleri bunu temel alarak [Active Directory Kılavuzu](../azure-resource-manager/resource-group-create-service-principal-portal.md) ve Mobile Engagement API'leri için kimlik doğrulaması için gerekli olan için özelleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="8eae5-107">The instructions below are based on this [Active Directory guide](../azure-resource-manager/resource-group-create-service-principal-portal.md) and customized for what is required for authentication for Mobile Engagement APIs.</span></span> <span data-ttu-id="8eae5-108">Ayrıntılı adımları anlamak istiyorsanız, bu nedenle başvurduğu.</span><span class="sxs-lookup"><span data-stu-id="8eae5-108">So refer to it if you want to understand the steps below in detail.</span></span> 
> 
> 

1. <span data-ttu-id="8eae5-109">Azure hesabınız ile oturum açma [Klasik portal](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="8eae5-109">Login to your Azure Account through the [classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="8eae5-110">Seçin **Active Directory** sol bölmeden.</span><span class="sxs-lookup"><span data-stu-id="8eae5-110">Select **Active Directory** from the left pane.</span></span>
   
     ![Active Directory'yi seçin][1]
3. <span data-ttu-id="8eae5-112">Seçin **varsayılan Active Directory** , Azure portalında.</span><span class="sxs-lookup"><span data-stu-id="8eae5-112">Choose the **Default Active Directory** in your Azure portal.</span></span> 
   
     ![dizin seçin][2]
   
   > [!IMPORTANT]
   > <span data-ttu-id="8eae5-114">Bu yaklaşım, yalnızca varsayılan Active Directory hesabınızın çalışıyorsanız ve hesabınızı oluşturduğunuz bir Active Directory bu yapıyorlarsa, işe yaramaz olduğunda çalışır.</span><span class="sxs-lookup"><span data-stu-id="8eae5-114">This approach works only when you are working in the default Active Directory of your account and will not work if you are doing this in an Active Directory that you have created in your account.</span></span> 
   > 
   > 
4. <span data-ttu-id="8eae5-115">Dizininizde uygulamaları görüntülemek için tıklatın **uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="8eae5-115">To view the applications in your directory, click on **Applications**.</span></span>
   
     ![uygulamaları görüntüle][3]
5. <span data-ttu-id="8eae5-117">Tıklayın **eklemek**.</span><span class="sxs-lookup"><span data-stu-id="8eae5-117">Click on **ADD**.</span></span> 
   
     ![Uygulama ekleme][4]
6. <span data-ttu-id="8eae5-119">Tıklayın **kuruluşumun geliştirmekte olduğu bir uygulama Ekle**</span><span class="sxs-lookup"><span data-stu-id="8eae5-119">Click on **Add an application my organization is developing**</span></span>
   
     ![Yeni uygulama][5]
7. <span data-ttu-id="8eae5-121">Uygulamanın adını girin ve uygulama olarak türünü seçin **WEB uygulaması ve/veya WEB API** ve İleri düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8eae5-121">Fill in name of the application and select the type of application as **WEB APPLICATION AND/OR WEB API** and click the next button.</span></span>
   
     ![Uygulama adı][6]
8. <span data-ttu-id="8eae5-123">Herhangi bir kukla URL için sağladığınız **oturum açma URL** ve **uygulama kimliği URI'si**.</span><span class="sxs-lookup"><span data-stu-id="8eae5-123">You can provide any dummy URLs for **SIGN-ON URL** and **APP ID URI**.</span></span> <span data-ttu-id="8eae5-124">Senaryomuz için kullanılmaz ve URL'leri kendilerini doğrulanmamış.</span><span class="sxs-lookup"><span data-stu-id="8eae5-124">They are not used for our scenario and the URLs themselves are not validated.</span></span>  
   
     ![Uygulama özellikleri][7]
9. <span data-ttu-id="8eae5-126">Sonunda bu, aşağıdaki gibi daha önce verilen ada sahip bir AAD uygulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8eae5-126">At the end of this, you will have an AAD app with the name you provided previously like the following.</span></span> <span data-ttu-id="8eae5-127">Bu, **AD\_uygulama\_adı** ve onu not edin.</span><span class="sxs-lookup"><span data-stu-id="8eae5-127">This is your **AD\_APP\_NAME** and make a note of it.</span></span>  
   
     ![Uygulama adı][8]
10. <span data-ttu-id="8eae5-129">Uygulama adına tıklayın ve tıklayın **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="8eae5-129">Click on the app name and click on **Configure**.</span></span>
    
      ![uygulamayı yapılandırma][9]
11. <span data-ttu-id="8eae5-131">Olarak kullanılacak istemci Kimliğini Not **istemci\_kimliği** API'nize çağırır.</span><span class="sxs-lookup"><span data-stu-id="8eae5-131">Make a note of the CLIENT ID that will be used as **CLIENT\_ID** for your API calls.</span></span> 
    
     ![uygulamayı yapılandırma][10]
12. <span data-ttu-id="8eae5-133">Ekranı aşağı kaydırarak **anahtarları** bölüm ve tercihen 2 yıl (Bitiş) süresi ile bir anahtar ekleyin ve tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="8eae5-133">Scroll down to the **Keys** section and add a key with preferably 2 years (expiry) duration and click **Save**.</span></span> 
    
     ![uygulamayı yapılandırma][11]
13. <span data-ttu-id="8eae5-135">Hemen herhangi bir zamanda yeniden görüntülenmeyecek depolanır, böylece değildir ve yalnızca şimdi gösterilen gibi anahtar için gösterilen değeri kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="8eae5-135">Immediately copy the value which is shown for the key as it is only shown now and is not stored so will not be displayed ever again.</span></span> <span data-ttu-id="8eae5-136">Ardından, kaybetmeniz durumunda yeni bir anahtar oluşturmak gerekir.</span><span class="sxs-lookup"><span data-stu-id="8eae5-136">If you lose it then you will have to generate a new key.</span></span> <span data-ttu-id="8eae5-137">Bu **CLIENT_SECRET** API'nize çağırır.</span><span class="sxs-lookup"><span data-stu-id="8eae5-137">This will be the **CLIENT_SECRET** for your API calls.</span></span> 
    
     ![uygulamayı yapılandırma][12]
    
    > [!IMPORTANT]
    > <span data-ttu-id="8eae5-139">Bu anahtar zamanı Aksi takdirde, API kimlik geldiğinde yenilemek emin olun artık çalışmayacak şekilde, belirttiğiniz süre sonunda süresi dolar.</span><span class="sxs-lookup"><span data-stu-id="8eae5-139">This key will expire at the end of the duration that you specified so make sure to renew it when the time comes otherwise your API authentication will not work anymore.</span></span> <span data-ttu-id="8eae5-140">Ayrıca silin ve tehlikeye düşünüyorsanız, bu anahtarı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8eae5-140">You can also delete and recreate this key if you think that it has been compromised.</span></span>
    > 
    > 
14. <span data-ttu-id="8eae5-141">Tıklayın **uç noktalarını GÖRÜNTÜLE** düğmesini şimdi açılacağı **uygulama uç noktaları** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="8eae5-141">Click on **VIEW ENDPOINTS** button now which will open up the **App Endpoints** dialog box.</span></span> 
    
    ![][13]
15. <span data-ttu-id="8eae5-142">Uygulama uç noktaları iletişim kutusundan kopyalama **OAUTH 2.0 BELİRTEÇ uç noktası**.</span><span class="sxs-lookup"><span data-stu-id="8eae5-142">From the App Endpoints dialog box, copy the **OAUTH 2.0 TOKEN ENDPOINT**.</span></span> 
    
    ![][14]
16. <span data-ttu-id="8eae5-143">Bu uç noktaya URL'de GUID olduğu şu biçimde olacaktır, **TENANT_ID** bu nedenle, not edin:</span><span class="sxs-lookup"><span data-stu-id="8eae5-143">This endpoint will be in the following form where the GUID in the URL is your **TENANT_ID** so make a note of it:</span></span> 
    
        https://login.microsoftonline.com/<GUID>/oauth2/token
17. <span data-ttu-id="8eae5-144">Şimdi Biz bu uygulamasını izinlerini yapılandırmak için devam edin.</span><span class="sxs-lookup"><span data-stu-id="8eae5-144">Now we will proceed to configure the permissions on this app.</span></span> <span data-ttu-id="8eae5-145">Bunun için açmanız gerekecek [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8eae5-145">For this you will have to open up the [Azure portal](https://portal.azure.com).</span></span> 
18. <span data-ttu-id="8eae5-146">Tıklayın **kaynak grupları** ve Bul **Mobile Engagement** kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="8eae5-146">Click on **Resource Groups** and find the **Mobile Engagement** resource group.</span></span>  
    
    ![][15]
19. <span data-ttu-id="8eae5-147">Tıklatın **Mobile Engagement** kaynak grubu ve gidin **ayarları** dikey burada.</span><span class="sxs-lookup"><span data-stu-id="8eae5-147">Click the **Mobile Engagement** resource group and navigate to the **Settings** blade here.</span></span> 
    
    ![][16]
20. <span data-ttu-id="8eae5-148">Tıklayın **kullanıcılar** ayarlar dikey ve ardından üzerinde **Ekle** bir kullanıcı eklemek için.</span><span class="sxs-lookup"><span data-stu-id="8eae5-148">Click on **Users** in the Settings blade and then click on **Add** to add a user.</span></span> 
    
    ![][17]
21. <span data-ttu-id="8eae5-149">Tıklayın **bir rol seçin**</span><span class="sxs-lookup"><span data-stu-id="8eae5-149">Click on **Select a role**</span></span>
    
    ![][18]
22. <span data-ttu-id="8eae5-150">Tıklayın **sahibi**</span><span class="sxs-lookup"><span data-stu-id="8eae5-150">Click on **Owner**</span></span>
    
    ![][19]
23. <span data-ttu-id="8eae5-151">Uygulamanızın adını arayın **AD\_uygulama\_adı** arama kutusuna.</span><span class="sxs-lookup"><span data-stu-id="8eae5-151">Search for the name of your application **AD\_APP\_NAME** in the Search box.</span></span> <span data-ttu-id="8eae5-152">Bunu burada varsayılan olarak görmez.</span><span class="sxs-lookup"><span data-stu-id="8eae5-152">You will not see this by default here.</span></span> <span data-ttu-id="8eae5-153">Bulduğunuzda, onu seçin ve tıklayın **seçin** dikey pencerenin altındaki.</span><span class="sxs-lookup"><span data-stu-id="8eae5-153">Once you find it, select it and click on **Select** at the bottom of the blade.</span></span> 
    
    ![][20]
24. <span data-ttu-id="8eae5-154">Üzerinde **eklemek erişim** dikey penceresinde gösterilir olarak **1 kullanıcının, 0 gruplarını**.</span><span class="sxs-lookup"><span data-stu-id="8eae5-154">On the **Add Access** blade, it will show up as **1 user, 0 groups**.</span></span> <span data-ttu-id="8eae5-155">Tıklatın **Tamam** Değişikliği onaylamak için bu dikey penceredeki.</span><span class="sxs-lookup"><span data-stu-id="8eae5-155">Click **OK** on this blade to confirm the change.</span></span> 
    
    ![][21]

<span data-ttu-id="8eae5-156">Gerekli bir AAD yapılandırmasına tamamladınız ve tüm API'leri çağırmak için ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="8eae5-156">You have now completed the required AAD configuration and you are all set to call the APIs.</span></span> 

<!-- Images -->
[1]: ./media/mobile-engagement-api-authentication-manual/active-directory.png
[2]: ./media/mobile-engagement-api-authentication-manual/active-directory-details.png
[3]: ./media/mobile-engagement-api-authentication-manual/view-applications.png
[4]: ./media/mobile-engagement-api-authentication-manual/add-icon.png
[5]: ./media/mobile-engagement-api-authentication-manual/what-do-you-want-to-do.png
[6]: ./media/mobile-engagement-api-authentication-manual/tell-us-about-your-application.png
[7]: ./media/mobile-engagement-api-authentication-manual/app-properties.png
[8]: ./media/mobile-engagement-api-authentication-manual/aad-app.png
[9]: ./media/mobile-engagement-api-authentication-manual/configure-menu.png
[10]: ./media/mobile-engagement-api-authentication-manual/client-id.png
[11]: ./media/mobile-engagement-api-authentication-manual/client_secret.png
[12]: ./media/mobile-engagement-api-authentication-manual/keys.png
[13]: ./media/mobile-engagement-api-authentication-manual/view-endpoints.png
[14]: ./media/mobile-engagement-api-authentication-manual/app-endpoints.png
[15]: ./media/mobile-engagement-api-authentication-manual/resource-groups.png
[16]: ./media/mobile-engagement-api-authentication-manual/resource-groups-settings.png
[17]: ./media/mobile-engagement-api-authentication-manual/add-users.png
[18]: ./media/mobile-engagement-api-authentication-manual/add-role.png
[19]: ./media/mobile-engagement-api-authentication-manual/select-role.png
[20]: ./media/mobile-engagement-api-authentication-manual/add-user-select.png
[21]: ./media/mobile-engagement-api-authentication-manual/add-access-final.png



