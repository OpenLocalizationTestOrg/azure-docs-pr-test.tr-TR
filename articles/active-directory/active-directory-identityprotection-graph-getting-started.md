---
title: "aaaGet başlatılan Azure Active Directory kimlik koruması ve Microsoft Graph | Microsoft Docs"
description: "Bir giriş tooquery Microsoft Graph risk olaylarına ve ilişkili bilgi listesi için Azure Active Directory'den sağlar."
services: active-directory
keywords: "Azure active directory kimlik koruması, risk olay, güvenlik açığı, güvenlik ilkesi, Microsoft Graph"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: fa109ba7-a914-437b-821d-2bd98e681386
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 75b8b7629a0120d8101f6fde0d9163122503d276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-active-directory-identity-protection-and-microsoft-graph"></a><span data-ttu-id="546b0-104">Azure Active Directory kimlik koruması ve Microsoft Graph kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="546b0-104">Get started with Azure Active Directory Identity Protection and Microsoft Graph</span></span>
<span data-ttu-id="546b0-105">Microsoft Graph, Microsoft unified API uç noktası hello ve, ev hello [Azure Active Directory kimlik koruması](active-directory-identityprotection.md) API'leri.</span><span class="sxs-lookup"><span data-stu-id="546b0-105">Microsoft Graph is hello Microsoft unified API endpoint and hello home of [Azure Active Directory Identity Protection](active-directory-identityprotection.md) APIs.</span></span> <span data-ttu-id="546b0-106">Merhaba ilk API **identityRiskEvents**, bir listesi için Microsoft Graph tooquery sağlar, [risk olayları](active-directory-identityprotection-risk-events-types.md) ve bilgileri ilişkilendirilmiş.</span><span class="sxs-lookup"><span data-stu-id="546b0-106">hello first API, **identityRiskEvents**, allows you tooquery Microsoft Graph for a list of [risk events](active-directory-identityprotection-risk-events-types.md) and associated information.</span></span> <span data-ttu-id="546b0-107">Bu makalede bu API sorgulama başlamanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="546b0-107">This article gets you started querying this API.</span></span> <span data-ttu-id="546b0-108">Bir ayrıntılı giriş, tam belgelere ve erişim toohello Graph Explorer'a için hello bakın [Microsoft Graph site](https://graph.microsoft.io/).</span><span class="sxs-lookup"><span data-stu-id="546b0-108">For an in-depth introduction, full documentation, and access toohello Graph Explorer, see hello [Microsoft Graph site](https://graph.microsoft.io/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="546b0-109">Microsoft önerir hello kullanarak Azure AD'yi yönetme [Azure AD Yönetim Merkezi](https://aad.portal.azure.com) hello yerine Azure portal hello bu makalede başvurulan Klasik Azure portalı.</span><span class="sxs-lookup"><span data-stu-id="546b0-109">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span>

<span data-ttu-id="546b0-110">Üç adımları tooaccessing kimlik koruması verilerine Microsoft Graph vardır:</span><span class="sxs-lookup"><span data-stu-id="546b0-110">There are three steps tooaccessing Identity Protection data through Microsoft Graph:</span></span>

1. <span data-ttu-id="546b0-111">Bir istemci parolası uygulamayla ekleyin.</span><span class="sxs-lookup"><span data-stu-id="546b0-111">Add an application with a client secret.</span></span> 
2. <span data-ttu-id="546b0-112">Bu gizli anahtar ve birkaç bilgi tooauthenticate tooMicrosoft grafiği, bir kimlik doğrulama belirteci almanıza parçalarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="546b0-112">Use this secret and a few other pieces of information tooauthenticate tooMicrosoft Graph, where you receive an authentication token.</span></span> 
3. <span data-ttu-id="546b0-113">Bu belirteç toomake istekleri toohello API uç noktası kullan ve kimlik koruması verileri geri alın.</span><span class="sxs-lookup"><span data-stu-id="546b0-113">Use this token toomake requests toohello API endpoint and get Identity Protection data back.</span></span>

<span data-ttu-id="546b0-114">Başlamadan önce ihtiyacınız vardır:</span><span class="sxs-lookup"><span data-stu-id="546b0-114">Before you get started, you’ll need:</span></span>

* <span data-ttu-id="546b0-115">Azure AD'de yönetici ayrıcalıkları toocreate hello uygulaması</span><span class="sxs-lookup"><span data-stu-id="546b0-115">Administrator privileges toocreate hello application in Azure AD</span></span>
* <span data-ttu-id="546b0-116">Kiracı'nın etki alanı (örneğin, contoso.onmicrosoft.com) Hello adı</span><span class="sxs-lookup"><span data-stu-id="546b0-116">hello name of your tenant's domain (for example, contoso.onmicrosoft.com)</span></span>

## <a name="add-an-application-with-a-client-secret"></a><span data-ttu-id="546b0-117">Bir istemci parolası ile uygulama ekleme</span><span class="sxs-lookup"><span data-stu-id="546b0-117">Add an application with a client secret</span></span>
1. <span data-ttu-id="546b0-118">[Oturum](https://manage.windowsazure.com) tooyour Klasik Azure portalında yönetici olarak.</span><span class="sxs-lookup"><span data-stu-id="546b0-118">[Sign in](https://manage.windowsazure.com) tooyour Azure classic portal as an administrator.</span></span> 
2. <span data-ttu-id="546b0-119">Merhaba sol gezinti bölmesinde, tıklayın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="546b0-119">On on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Uygulama oluşturma](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_01.png)
3. <span data-ttu-id="546b0-121">Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.</span><span class="sxs-lookup"><span data-stu-id="546b0-121">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
4. <span data-ttu-id="546b0-122">Hello içinde hello üst menüsünde **uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="546b0-122">In hello menu on hello top, click **Applications**.</span></span>
   
    ![Uygulama oluşturma](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_02.png)
5. <span data-ttu-id="546b0-124">Tıklatın **Ekle** hello sayfanın hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="546b0-124">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Uygulama oluşturma](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_03.png)
6. <span data-ttu-id="546b0-126">Merhaba üzerinde **neler toodo istediğiniz** iletişim kutusunda, tıklatın **kuruluşumun geliştirmekte olduğu bir uygulama Ekle**.</span><span class="sxs-lookup"><span data-stu-id="546b0-126">On hello **What do you want toodo** dialog, click **Add an application my organization is developing**.</span></span>
   
    ![Uygulama oluşturma](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_04.png)
7. <span data-ttu-id="546b0-128">Merhaba üzerinde **bize uygulamanızı anlatın** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="546b0-128">On hello **Tell us about your application** dialog, perform hello following steps:</span></span>
   
    ![Uygulama oluşturma](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_05.png)
   
    <span data-ttu-id="546b0-130">a.</span><span class="sxs-lookup"><span data-stu-id="546b0-130">a.</span></span> <span data-ttu-id="546b0-131">Merhaba, **adı** metin kutusuna, uygulamanız için bir ad yazın (örneğin: AADIP Risk olayı API uygulama).</span><span class="sxs-lookup"><span data-stu-id="546b0-131">In hello **Name** textbox, type a name for your application (e.g.: AADIP Risk Event API Application).</span></span>
   
    <span data-ttu-id="546b0-132">b.</span><span class="sxs-lookup"><span data-stu-id="546b0-132">b.</span></span> <span data-ttu-id="546b0-133">Olarak **türü**seçin **Web uygulaması ve / veya Web API**.</span><span class="sxs-lookup"><span data-stu-id="546b0-133">As **Type**, select **Web Application And / Or Web API**.</span></span>
   
    <span data-ttu-id="546b0-134">c.</span><span class="sxs-lookup"><span data-stu-id="546b0-134">c.</span></span> <span data-ttu-id="546b0-135">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="546b0-135">Click **Next**.</span></span>
8. <span data-ttu-id="546b0-136">Merhaba üzerinde **uygulama özellikleri** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="546b0-136">On hello **App properties** dialog, perform hello following steps:</span></span>
   
    ![Uygulama oluşturma](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_06.png)
   
    <span data-ttu-id="546b0-138">a.</span><span class="sxs-lookup"><span data-stu-id="546b0-138">a.</span></span> <span data-ttu-id="546b0-139">Merhaba, **oturum açma URL'si** metin kutusuna, türü `http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="546b0-139">In hello **Sign-On URL** textbox, type `http://localhost`.</span></span>
   
    <span data-ttu-id="546b0-140">b.</span><span class="sxs-lookup"><span data-stu-id="546b0-140">b.</span></span> <span data-ttu-id="546b0-141">Merhaba, **uygulama kimliği URI'si** metin kutusuna, türü `http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="546b0-141">In hello **App ID URI** textbox, type `http://localhost`.</span></span>
   
    <span data-ttu-id="546b0-142">c.</span><span class="sxs-lookup"><span data-stu-id="546b0-142">c.</span></span> <span data-ttu-id="546b0-143">**Tamamla**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="546b0-143">Click **Complete**.</span></span>

<span data-ttu-id="546b0-144">Can şimdi uygulamanızı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="546b0-144">Your can now configure your application.</span></span>

![Uygulama oluşturma](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_07.png)

## <a name="grant-your-application-permission-toouse-hello-api"></a><span data-ttu-id="546b0-146">Uygulama izni toouse hello API verin</span><span class="sxs-lookup"><span data-stu-id="546b0-146">Grant your application permission toouse hello API</span></span>
1. <span data-ttu-id="546b0-147">Uygulamanızın sayfasında hello üst hello menüsünde tıklatın **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="546b0-147">On your application's page, in hello menu on hello top, click **Configure**.</span></span> 
   
    ![Uygulama oluşturma](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_08.png)
2. <span data-ttu-id="546b0-149">Merhaba, **izinleri tooother uygulamaları** 'yi tıklatın **uygulama eklemek**.</span><span class="sxs-lookup"><span data-stu-id="546b0-149">In hello **permissions tooother applications** section, click **Add application**.</span></span>
   
    ![Uygulama oluşturma](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_09.png)
3. <span data-ttu-id="546b0-151">Merhaba üzerinde **izinleri tooother uygulamaları** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="546b0-151">On hello **permissions tooother applications** dialog, perform hello following steps:</span></span>
   
    ![Uygulama oluşturma](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_10.png)
   
    <span data-ttu-id="546b0-153">a.</span><span class="sxs-lookup"><span data-stu-id="546b0-153">a.</span></span> <span data-ttu-id="546b0-154">Seçin **Microsoft Graph**.</span><span class="sxs-lookup"><span data-stu-id="546b0-154">Select **Microsoft Graph**.</span></span>
   
    <span data-ttu-id="546b0-155">b.</span><span class="sxs-lookup"><span data-stu-id="546b0-155">b.</span></span> <span data-ttu-id="546b0-156">**Tamamla**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="546b0-156">Click **Complete**.</span></span>
4. <span data-ttu-id="546b0-157">Tıklatın **uygulama izinleri: 0**ve ardından **tüm kimlik risk olay bilgilerini okuma**.</span><span class="sxs-lookup"><span data-stu-id="546b0-157">Click **Application Permissions: 0**, and then select **Read all identity risk event information**.</span></span>
   
    ![Uygulama oluşturma](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_11.png)
5. <span data-ttu-id="546b0-159">Tıklatın **kaydetmek** hello sayfanın hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="546b0-159">Click **Save** at hello bottom of hello page.</span></span>
   
    ![Uygulama oluşturma](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)

## <a name="get-an-access-key"></a><span data-ttu-id="546b0-161">Bir erişim anahtarı alma</span><span class="sxs-lookup"><span data-stu-id="546b0-161">Get an access key</span></span>
1. <span data-ttu-id="546b0-162">Uygulamanızın sayfasında hello **anahtarları** bölümünde, 1 yıl süre olarak seçin.</span><span class="sxs-lookup"><span data-stu-id="546b0-162">On your application's page, in hello **keys** section, select 1 year as duration.</span></span>
   
    ![Uygulama oluşturma](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_13.png)
2. <span data-ttu-id="546b0-164">Tıklatın **kaydetmek** hello sayfanın hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="546b0-164">Click **Save** at hello bottom of hello page.</span></span>
   
    ![Uygulama oluşturma](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)
3. <span data-ttu-id="546b0-166">Merhaba anahtarları bölümünde, yeni oluşturulan anahtarınızı hello değerini kopyalayın ve güvenli bir konuma yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="546b0-166">in hello keys section, copy hello value of your newly created key, and then paste it into a safe location.</span></span>
   
    ![Uygulama oluşturma](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_14.png)
   
   > [!NOTE]
   > <span data-ttu-id="546b0-168">Bu anahtar kaybederseniz, tooreturn toothis bölümü ve yeni bir anahtar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="546b0-168">If you lose this key, you will have tooreturn toothis section and create a new key.</span></span> <span data-ttu-id="546b0-169">Bu anahtarı bir gizli tutma: olan herkes verilerinize erişebilir.</span><span class="sxs-lookup"><span data-stu-id="546b0-169">Keep this key a secret: anyone who has it can access your data.</span></span>
   > 
   > 
4. <span data-ttu-id="546b0-170">Merhaba, **özellikleri** bölümü, kopyalama hello **istemci kimliği**ve güvenli bir konuma yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="546b0-170">In hello **properties** section, copy hello **Client ID**, and then paste it into a safe location.</span></span> 

## <a name="authenticate-toomicrosoft-graph-and-query-hello-identity-risk-events-api"></a><span data-ttu-id="546b0-171">TooMicrosoft grafik ve sorgu hello kimlik Risk olayları API kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="546b0-171">Authenticate tooMicrosoft Graph and query hello Identity Risk Events API</span></span>
<span data-ttu-id="546b0-172">Bu noktada, olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="546b0-172">At this point, you should have:</span></span>

* <span data-ttu-id="546b0-173">Yukarıdaki kopyaladığınız hello istemci kimliği</span><span class="sxs-lookup"><span data-stu-id="546b0-173">hello client ID you copied above</span></span>
* <span data-ttu-id="546b0-174">Yukarıdaki kopyaladığınız hello anahtarı</span><span class="sxs-lookup"><span data-stu-id="546b0-174">hello key you copied above</span></span>
* <span data-ttu-id="546b0-175">Merhaba, kiracının etki alanı adı</span><span class="sxs-lookup"><span data-stu-id="546b0-175">hello name of your tenant's domain</span></span>

<span data-ttu-id="546b0-176">tooauthenticate, gönderme bir post isteği çok`https://login.microsoft.com` şu parametreler hello gövdesindeki hello ile:</span><span class="sxs-lookup"><span data-stu-id="546b0-176">tooauthenticate, send a post request too`https://login.microsoft.com` with hello following parameters in hello body:</span></span>

* <span data-ttu-id="546b0-177">grant_type: "**client_credentials**"</span><span class="sxs-lookup"><span data-stu-id="546b0-177">grant_type: “**client_credentials**”</span></span>
* <span data-ttu-id="546b0-178">Kaynak: "**https://graph.microsoft.com**"</span><span class="sxs-lookup"><span data-stu-id="546b0-178">resource: “**https://graph.microsoft.com**”</span></span>
* <span data-ttu-id="546b0-179">client_id:<your client ID></span><span class="sxs-lookup"><span data-stu-id="546b0-179">client_id: <your client ID></span></span>
* <span data-ttu-id="546b0-180">client_secret:<your key></span><span class="sxs-lookup"><span data-stu-id="546b0-180">client_secret: <your key></span></span>

> [!NOTE]
> <span data-ttu-id="546b0-181">Merhaba tooprovide değerlerine gereksinim **client_id** ve hello **client_secret** parametresi.</span><span class="sxs-lookup"><span data-stu-id="546b0-181">You need tooprovide values for hello **client_id** and hello **client_secret** parameter.</span></span>
> 
> 

<span data-ttu-id="546b0-182">Başarılı olursa, bu kimlik doğrulama belirtecini döndürür.</span><span class="sxs-lookup"><span data-stu-id="546b0-182">If successful, this returns an authentication token.</span></span>  
<span data-ttu-id="546b0-183">toocall hello API, parametre aşağıdaki hello bir üstbilgi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="546b0-183">toocall hello API, create a header with hello following parameter:</span></span>

    `Authorization`=”<token_type> <access_token>"


<span data-ttu-id="546b0-184">Kimlik doğrulamasını yaparken, belirteç döndürdü hello hello belirteç türü ve erişim belirteci bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="546b0-184">When authenticating, you can find hello token type and access token in hello returned token.</span></span>

<span data-ttu-id="546b0-185">Bu üst API URL aşağıdaki isteği toohello gönder:`https://graph.microsoft.com/beta/identityRiskEvents`</span><span class="sxs-lookup"><span data-stu-id="546b0-185">Send this header as a request toohello following API URL: `https://graph.microsoft.com/beta/identityRiskEvents`</span></span>

<span data-ttu-id="546b0-186">Merhaba yanıt başarılı olursa, kimlik, risk olaylarını koleksiyonudur ve hello ayrıştırılır ve uygun gördüğünüz şekilde ele OData JSON biçimine verilerde ilişkili.</span><span class="sxs-lookup"><span data-stu-id="546b0-186">hello response, if successful, is a collection of identity risk events and associated data in hello OData JSON format, which can be parsed and handled as see fit.</span></span>

<span data-ttu-id="546b0-187">Kimlik doğrulaması ve Powershell kullanarak hello API'sini çağırmak için örnek kod aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="546b0-187">Here’s sample code for authenticating and calling hello API using Powershell.</span></span>  
<span data-ttu-id="546b0-188">Yalnızca istemci Kimliğiniz Ekle anahtarı ve Kiracı etki alanı.</span><span class="sxs-lookup"><span data-stu-id="546b0-188">Just add your client ID, key, and tenant domain.</span></span>

    $ClientID       = "<your client ID here>"        # Should be a ~36 hex character string; insert your info here
    $ClientSecret   = "<your client secret here>"    # Should be a ~44 character string; insert your info here
    $tenantdomain   = "<your tenant domain here>"    # For example, contoso.onmicrosoft.com

    $loginURL       = "https://login.microsoft.com"
    $resource       = "https://graph.microsoft.com"

    $body       = @{grant_type="client_credentials";resource=$resource;client_id=$ClientID;client_secret=$ClientSecret}
    $oauth      = Invoke-RestMethod -Method Post -Uri $loginURL/$tenantdomain/oauth2/token?api-version=1.0 -Body $body

    Write-Output $oauth

    if ($oauth.access_token -ne $null) {
        $headerParams = @{'Authorization'="$($oauth.token_type) $($oauth.access_token)"}

        $url = "https://graph.microsoft.com/beta/identityRiskEvents"
        Write-Output $url

        $myReport = (Invoke-WebRequest -UseBasicParsing -Headers $headerParams -Uri $url)

        foreach ($event in ($myReport.Content | ConvertFrom-Json).value) {
            Write-Output $event
        }

    } else {
        Write-Host "ERROR: No Access Token"
    } 


## <a name="next-steps"></a><span data-ttu-id="546b0-189">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="546b0-189">Next steps</span></span>
<span data-ttu-id="546b0-190">Tebrikler, ilk çağrı tooMicrosoft grafiği yaptığınız.</span><span class="sxs-lookup"><span data-stu-id="546b0-190">Congratulations, you just made your first call tooMicrosoft Graph!</span></span>  
<span data-ttu-id="546b0-191">Şimdi kimlik risk olaylarını sorgular ve uygun gördüğünüz ancak hello verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="546b0-191">Now you can query identity risk events and use hello data however you see fit.</span></span>

<span data-ttu-id="546b0-192">toolearn Microsoft Graph hakkında daha fazla grafik API'sini kullanarak toobuild uygulamaları nasıl hello denetleyip hello [belgelerine](https://graph.microsoft.io/docs) ve hello hakkında daha fazla [Microsoft Graph site](https://graph.microsoft.io/).</span><span class="sxs-lookup"><span data-stu-id="546b0-192">toolearn more about Microsoft Graph and how toobuild applications using hello Graph API, check out hello [documentation](https://graph.microsoft.io/docs) and much more on hello [Microsoft Graph site](https://graph.microsoft.io/).</span></span> <span data-ttu-id="546b0-193">Ayrıca, emin toobookmark hello olun [Azure AD Identity Protection API](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root) tüm hello kimlik koruma API'leri grafiğinde kullanılabilir listeler sayfası.</span><span class="sxs-lookup"><span data-stu-id="546b0-193">Also, make sure toobookmark hello [Azure AD Identity Protection API](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root) page that lists all of hello Identity Protection APIs available in Graph.</span></span> <span data-ttu-id="546b0-194">API aracılığıyla kimlik koruması ile yeni yolları toowork eklediğimiz gibi ilgili sayfada görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="546b0-194">As we add new ways toowork with Identity Protection via API, you’ll see them on that page.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="546b0-195">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="546b0-195">Additional resources</span></span>
* [<span data-ttu-id="546b0-196">Azure Active Directory kimlik koruması</span><span class="sxs-lookup"><span data-stu-id="546b0-196">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)
* [<span data-ttu-id="546b0-197">Azure Active Directory kimlik koruması tarafından algılanan risk olayı türleri</span><span class="sxs-lookup"><span data-stu-id="546b0-197">Types of risk events detected by Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-risk-events-types.md)
* [<span data-ttu-id="546b0-198">Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="546b0-198">Microsoft Graph</span></span>](https://graph.microsoft.io/)
* [<span data-ttu-id="546b0-199">Microsoft Graph genel bakış</span><span class="sxs-lookup"><span data-stu-id="546b0-199">Overview of Microsoft Graph</span></span>](https://graph.microsoft.io/docs)
* [<span data-ttu-id="546b0-200">Azure AD kimlik koruması hizmet kök</span><span class="sxs-lookup"><span data-stu-id="546b0-200">Azure AD Identity Protection Service Root</span></span>](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root)

