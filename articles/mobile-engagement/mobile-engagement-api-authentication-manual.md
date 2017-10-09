---
title: Mobile Engagement REST API'leri - el ile kuruluma ile aaaAuthenticate
description: "Nasıl toomanually Kurulum kimlik doğrulaması için Mobile Engagement REST API'leri"
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
ms.openlocfilehash: 3884f94afcd6b9a62bfcf498fb6ee84bb6e837b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-mobile-engagement-rest-apis---manual-setup"></a><span data-ttu-id="04986-103">Mobile Engagement REST API'leri ile - el ile kuruluma kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="04986-103">Authenticate with Mobile Engagement REST APIs - manual setup</span></span>
<span data-ttu-id="04986-104">Bu bir ek çok belgesidir[Mobile Engagement REST API'leri ile kimlik doğrulama](mobile-engagement-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="04986-104">This is an appendix documentation too[Authenticate with Mobile Engagement REST APIs](mobile-engagement-api-authentication.md).</span></span> <span data-ttu-id="04986-105">İlk tooget hello bağlam okuma emin olun.</span><span class="sxs-lookup"><span data-stu-id="04986-105">Make sure you read it first tooget hello context.</span></span> <span data-ttu-id="04986-106">Merhaba Mobile Engagement REST API'lerini kullanarak hello için Azure Portal Bu, kimlik doğrulama kurma bir alternatif bir yol toodo hello kerelik Kurulum açıklar.</span><span class="sxs-lookup"><span data-stu-id="04986-106">This describes an alternate way toodo hello One-time setup for setting up your authentication for hello Mobile Engagement REST APIs using hello Azure Portal.</span></span> 

> [!NOTE]
> <span data-ttu-id="04986-107">Merhaba yönergelerde bu dayalı [Active Directory Kılavuzu](../azure-resource-manager/resource-group-create-service-principal-portal.md) ve Mobile Engagement API'leri için kimlik doğrulaması için gerekli olan için özelleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="04986-107">hello instructions below are based on this [Active Directory guide](../azure-resource-manager/resource-group-create-service-principal-portal.md) and customized for what is required for authentication for Mobile Engagement APIs.</span></span> <span data-ttu-id="04986-108">Ayrıntılı toounderstand hello adımları istiyorsanız, bu nedenle tooit bakın.</span><span class="sxs-lookup"><span data-stu-id="04986-108">So refer tooit if you want toounderstand hello steps below in detail.</span></span> 
> 
> 

1. <span data-ttu-id="04986-109">Merhaba aracılığıyla Azure hesabı oturum açma tooyour [Klasik portal](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="04986-109">Login tooyour Azure Account through hello [classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="04986-110">Seçin **Active Directory** hello sol bölmesinden.</span><span class="sxs-lookup"><span data-stu-id="04986-110">Select **Active Directory** from hello left pane.</span></span>
   
     ![Active Directory'yi seçin][1]
3. <span data-ttu-id="04986-112">Merhaba seçin **varsayılan Active Directory** , Azure portalında.</span><span class="sxs-lookup"><span data-stu-id="04986-112">Choose hello **Default Active Directory** in your Azure portal.</span></span> 
   
     ![dizin seçin][2]
   
   > [!IMPORTANT]
   > <span data-ttu-id="04986-114">Bu yaklaşım, yalnızca hello varsayılan Active Directory hesabınızın çalışıyorsanız ve hesabınızı oluşturduğunuz bir Active Directory bu yapıyorlarsa, işe yaramaz olduğunda çalışır.</span><span class="sxs-lookup"><span data-stu-id="04986-114">This approach works only when you are working in hello default Active Directory of your account and will not work if you are doing this in an Active Directory that you have created in your account.</span></span> 
   > 
   > 
4. <span data-ttu-id="04986-115">dizininizde, tooview hello uygulamaları tıklayın **uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="04986-115">tooview hello applications in your directory, click on **Applications**.</span></span>
   
     ![uygulamaları görüntüle][3]
5. <span data-ttu-id="04986-117">Tıklayın **eklemek**.</span><span class="sxs-lookup"><span data-stu-id="04986-117">Click on **ADD**.</span></span> 
   
     ![Uygulama ekleme][4]
6. <span data-ttu-id="04986-119">Tıklayın **kuruluşumun geliştirmekte olduğu bir uygulama Ekle**</span><span class="sxs-lookup"><span data-stu-id="04986-119">Click on **Add an application my organization is developing**</span></span>
   
     ![Yeni uygulama][5]
7. <span data-ttu-id="04986-121">Merhaba uygulama ve uygulamanın olarak select hello türü adını doldurun **WEB uygulaması ve/veya WEB API** ve hello İleri düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="04986-121">Fill in name of hello application and select hello type of application as **WEB APPLICATION AND/OR WEB API** and click hello next button.</span></span>
   
     ![Uygulama adı][6]
8. <span data-ttu-id="04986-123">Herhangi bir kukla URL için sağladığınız **oturum açma URL** ve **uygulama kimliği URI'si**.</span><span class="sxs-lookup"><span data-stu-id="04986-123">You can provide any dummy URLs for **SIGN-ON URL** and **APP ID URI**.</span></span> <span data-ttu-id="04986-124">Senaryomuz için kullanılmaz ve hello URL'leri kendilerini doğrulanmamış.</span><span class="sxs-lookup"><span data-stu-id="04986-124">They are not used for our scenario and hello URLs themselves are not validated.</span></span>  
   
     ![Uygulama özellikleri][7]
9. <span data-ttu-id="04986-126">Bu Hello sonunda hello aşağıdaki gibi daha önce sağlanan hello adı bir AAD uygulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="04986-126">At hello end of this, you will have an AAD app with hello name you provided previously like hello following.</span></span> <span data-ttu-id="04986-127">Bu, **AD\_uygulama\_adı** ve onu not edin.</span><span class="sxs-lookup"><span data-stu-id="04986-127">This is your **AD\_APP\_NAME** and make a note of it.</span></span>  
   
     ![Uygulama adı][8]
10. <span data-ttu-id="04986-129">Merhaba uygulama adına tıklayın ve tıklayın **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="04986-129">Click on hello app name and click on **Configure**.</span></span>
    
      ![uygulamayı yapılandırma][9]
11. <span data-ttu-id="04986-131">Hello olarak kullanılacak bir istemci kimliği Not **istemci\_kimliği** API'nize çağırır.</span><span class="sxs-lookup"><span data-stu-id="04986-131">Make a note of hello CLIENT ID that will be used as **CLIENT\_ID** for your API calls.</span></span> 
    
     ![uygulamayı yapılandırma][10]
12. <span data-ttu-id="04986-133">Toohello aşağı **anahtarları** bölüm ve tercihen 2 yıl (Bitiş) süresi ile bir anahtar ekleyin ve tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="04986-133">Scroll down toohello **Keys** section and add a key with preferably 2 years (expiry) duration and click **Save**.</span></span> 
    
     ![uygulamayı yapılandırma][11]
13. <span data-ttu-id="04986-135">Hemen herhangi bir zamanda yeniden görüntülenmeyecek depolanır, böylece değildir ve yalnızca şimdi gösterilen gibi hello anahtarı gösterilen hello değeri kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="04986-135">Immediately copy hello value which is shown for hello key as it is only shown now and is not stored so will not be displayed ever again.</span></span> <span data-ttu-id="04986-136">Ardından, kaybetmeniz durumunda toogenerate yeni bir anahtar gerekir.</span><span class="sxs-lookup"><span data-stu-id="04986-136">If you lose it then you will have toogenerate a new key.</span></span> <span data-ttu-id="04986-137">Bu hello olacaktır **CLIENT_SECRET** API'nize çağırır.</span><span class="sxs-lookup"><span data-stu-id="04986-137">This will be hello **CLIENT_SECRET** for your API calls.</span></span> 
    
     ![uygulamayı yapılandırma][12]
    
    > [!IMPORTANT]
    > <span data-ttu-id="04986-139">Bu anahtar, başlangıç zamanı Aksi takdirde, API kimlik geldiğinde artık çalışmaz, bunu yap emin toorenew belirtilen hello hello süre sonunda süresi dolar.</span><span class="sxs-lookup"><span data-stu-id="04986-139">This key will expire at hello end of hello duration that you specified so make sure toorenew it when hello time comes otherwise your API authentication will not work anymore.</span></span> <span data-ttu-id="04986-140">Ayrıca silin ve tehlikeye düşünüyorsanız, bu anahtarı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="04986-140">You can also delete and recreate this key if you think that it has been compromised.</span></span>
    > 
    > 
14. <span data-ttu-id="04986-141">Tıklayın **uç noktalarını GÖRÜNTÜLE** düğmesini şimdi hello açılacağı **uygulama uç noktaları** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="04986-141">Click on **VIEW ENDPOINTS** button now which will open up hello **App Endpoints** dialog box.</span></span> 
    
    ![][13]
15. <span data-ttu-id="04986-142">Merhaba Hello uygulama uç noktaları iletişim kutusundan kopyalama **OAUTH 2.0 BELİRTEÇ uç noktası**.</span><span class="sxs-lookup"><span data-stu-id="04986-142">From hello App Endpoints dialog box, copy hello **OAUTH 2.0 TOKEN ENDPOINT**.</span></span> 
    
    ![][14]
16. <span data-ttu-id="04986-143">Bu uç noktaya hello hello URL'de GUID olduğu form aşağıdaki hello olacaktır, **TENANT_ID** bu nedenle, not edin:</span><span class="sxs-lookup"><span data-stu-id="04986-143">This endpoint will be in hello following form where hello GUID in hello URL is your **TENANT_ID** so make a note of it:</span></span> 
    
        https://login.microsoftonline.com/<GUID>/oauth2/token
17. <span data-ttu-id="04986-144">Şimdi biz tooconfigure hello bu uygulama izinlerini devam edin.</span><span class="sxs-lookup"><span data-stu-id="04986-144">Now we will proceed tooconfigure hello permissions on this app.</span></span> <span data-ttu-id="04986-145">Bu tooopen hello yukarı olacaktır [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="04986-145">For this you will have tooopen up hello [Azure portal](https://portal.azure.com).</span></span> 
18. <span data-ttu-id="04986-146">Tıklayın **kaynak grupları** ve hello bulur **Mobile Engagement** kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="04986-146">Click on **Resource Groups** and find hello **Mobile Engagement** resource group.</span></span>  
    
    ![][15]
19. <span data-ttu-id="04986-147">Hello tıklatın **Mobile Engagement** kaynak grubu ve toohello gidin **ayarları** dikey burada.</span><span class="sxs-lookup"><span data-stu-id="04986-147">Click hello **Mobile Engagement** resource group and navigate toohello **Settings** blade here.</span></span> 
    
    ![][16]
20. <span data-ttu-id="04986-148">Tıklayın **kullanıcılar** ayarlar dikey penceresinde hello ve tıklayın **Ekle** tooadd bir kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="04986-148">Click on **Users** in hello Settings blade and then click on **Add** tooadd a user.</span></span> 
    
    ![][17]
21. <span data-ttu-id="04986-149">Tıklayın **bir rol seçin**</span><span class="sxs-lookup"><span data-stu-id="04986-149">Click on **Select a role**</span></span>
    
    ![][18]
22. <span data-ttu-id="04986-150">Tıklayın **sahibi**</span><span class="sxs-lookup"><span data-stu-id="04986-150">Click on **Owner**</span></span>
    
    ![][19]
23. <span data-ttu-id="04986-151">Uygulamanızın hello adını arayın **AD\_uygulama\_adı** hello arama kutusuna.</span><span class="sxs-lookup"><span data-stu-id="04986-151">Search for hello name of your application **AD\_APP\_NAME** in hello Search box.</span></span> <span data-ttu-id="04986-152">Bunu burada varsayılan olarak görmez.</span><span class="sxs-lookup"><span data-stu-id="04986-152">You will not see this by default here.</span></span> <span data-ttu-id="04986-153">Bulduğunuzda, onu seçin ve tıklayın **seçin** hello dikey penceresinde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="04986-153">Once you find it, select it and click on **Select** at hello bottom of hello blade.</span></span> 
    
    ![][20]
24. <span data-ttu-id="04986-154">Merhaba üzerinde **eklemek erişim** dikey penceresinde gösterilir olarak **1 kullanıcının, 0 gruplarını**.</span><span class="sxs-lookup"><span data-stu-id="04986-154">On hello **Add Access** blade, it will show up as **1 user, 0 groups**.</span></span> <span data-ttu-id="04986-155">Tıklatın **Tamam** bu dikey tooconfirm hello değişir.</span><span class="sxs-lookup"><span data-stu-id="04986-155">Click **OK** on this blade tooconfirm hello change.</span></span> 
    
    ![][21]

<span data-ttu-id="04986-156">Gerekli hello AAD yapılandırmasını tamamladınız ve tüm kümesi toocall hello API'leri demektir.</span><span class="sxs-lookup"><span data-stu-id="04986-156">You have now completed hello required AAD configuration and you are all set toocall hello APIs.</span></span> 

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



