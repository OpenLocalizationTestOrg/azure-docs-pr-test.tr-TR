---
title: "Azure Active Directory kimlik koruması ve Microsoft Graph kullanmaya başlama | Microsoft Docs"
description: "Sorgu Microsoft Graph risk olaylarına ve ilişkili bilgi listesi için Azure Active Directory'den tanıtılmaktadır."
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
ms.openlocfilehash: 9b01ff86da6a1fd4a439a6ba59ea15ed6480cdad
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-azure-active-directory-identity-protection-and-microsoft-graph"></a><span data-ttu-id="884d5-104">Azure Active Directory kimlik koruması ve Microsoft Graph kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="884d5-104">Get started with Azure Active Directory Identity Protection and Microsoft Graph</span></span>
<span data-ttu-id="884d5-105">Microsoft Graph olan Microsoft unified API uç noktasını ve giriş, [Azure Active Directory kimlik koruması](active-directory-identityprotection.md) API'leri.</span><span class="sxs-lookup"><span data-stu-id="884d5-105">Microsoft Graph is the Microsoft unified API endpoint and the home of [Azure Active Directory Identity Protection](active-directory-identityprotection.md) APIs.</span></span> <span data-ttu-id="884d5-106">İlk API **identityRiskEvents**, bir listesi için Microsoft Graph sorgu sayesinde [risk olayları](active-directory-identityprotection-risk-events-types.md) ve bilgi ilişkili.</span><span class="sxs-lookup"><span data-stu-id="884d5-106">The first API, **identityRiskEvents**, allows you to query Microsoft Graph for a list of [risk events](active-directory-identityprotection-risk-events-types.md) and associated information.</span></span> <span data-ttu-id="884d5-107">Bu makalede bu API sorgulama başlamanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="884d5-107">This article gets you started querying this API.</span></span> <span data-ttu-id="884d5-108">Bir ayrıntılı giriş, tam belgelere ve Graph Explorer'da erişim için bakın [Microsoft Graph site](https://graph.microsoft.io/).</span><span class="sxs-lookup"><span data-stu-id="884d5-108">For an in-depth introduction, full documentation, and access to the Graph Explorer, see the [Microsoft Graph site](https://graph.microsoft.io/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="884d5-109">Microsoft, Azure AD’yi bu makalede bahsedilen Klasik Azure Portalı yerine Azure portalındaki [Azure AD yönetim merkezini](https://aad.portal.azure.com) kullanarak yönetmenizi öneriyor.</span><span class="sxs-lookup"><span data-stu-id="884d5-109">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span>

<span data-ttu-id="884d5-110">Microsoft Graph kimlik koruması verilere erişmek için üç adım vardır:</span><span class="sxs-lookup"><span data-stu-id="884d5-110">There are three steps to accessing Identity Protection data through Microsoft Graph:</span></span>

1. <span data-ttu-id="884d5-111">Bir istemci parolası uygulamayla ekleyin.</span><span class="sxs-lookup"><span data-stu-id="884d5-111">Add an application with a client secret.</span></span> 
2. <span data-ttu-id="884d5-112">Bu gizli anahtar ve birkaç bilgi parçalarını bir kimlik doğrulama belirteci almanıza Microsoft Graph için kimlik doğrulaması yapmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="884d5-112">Use this secret and a few other pieces of information to authenticate to Microsoft Graph, where you receive an authentication token.</span></span> 
3. <span data-ttu-id="884d5-113">İstekte API uç noktasına ve kimlik koruma verilerini geri almak için bu belirteci kullanın.</span><span class="sxs-lookup"><span data-stu-id="884d5-113">Use this token to make requests to the API endpoint and get Identity Protection data back.</span></span>

<span data-ttu-id="884d5-114">Başlamadan önce ihtiyacınız vardır:</span><span class="sxs-lookup"><span data-stu-id="884d5-114">Before you get started, you’ll need:</span></span>

* <span data-ttu-id="884d5-115">Azure AD içinde uygulama oluşturmak için yönetici ayrıcalıkları</span><span class="sxs-lookup"><span data-stu-id="884d5-115">Administrator privileges to create the application in Azure AD</span></span>
* <span data-ttu-id="884d5-116">Kiracı'nın etki alanı (örneğin, contoso.onmicrosoft.com) adı</span><span class="sxs-lookup"><span data-stu-id="884d5-116">The name of your tenant's domain (for example, contoso.onmicrosoft.com)</span></span>

## <a name="add-an-application-with-a-client-secret"></a><span data-ttu-id="884d5-117">Bir istemci parolası ile uygulama ekleme</span><span class="sxs-lookup"><span data-stu-id="884d5-117">Add an application with a client secret</span></span>
1. <span data-ttu-id="884d5-118">[Oturum](https://manage.windowsazure.com) yönetici olarak, Azure Klasik portalı.</span><span class="sxs-lookup"><span data-stu-id="884d5-118">[Sign in](https://manage.windowsazure.com) to your Azure classic portal as an administrator.</span></span> 
2. <span data-ttu-id="884d5-119">Sol gezinti bölmesinde, tıklayın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="884d5-119">On on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Uygulama oluşturma](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_01.png)
3. <span data-ttu-id="884d5-121">Gelen **Directory** listesinde, directory tümleştirmesini etkinleştirmek istediğiniz dizini seçin.</span><span class="sxs-lookup"><span data-stu-id="884d5-121">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
4. <span data-ttu-id="884d5-122">Üstteki menüde tıklatın **uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="884d5-122">In the menu on the top, click **Applications**.</span></span>
   
    ![Uygulama oluşturma](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_02.png)
5. <span data-ttu-id="884d5-124">Tıklatın **Ekle** sayfanın sonundaki.</span><span class="sxs-lookup"><span data-stu-id="884d5-124">Click **Add** at the bottom of the page.</span></span>
   
    ![Uygulama oluşturma](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_03.png)
6. <span data-ttu-id="884d5-126">Üzerinde **ne yapmak istiyorsunuz** iletişim kutusunda, tıklatın **kuruluşumun geliştirmekte olduğu bir uygulama Ekle**.</span><span class="sxs-lookup"><span data-stu-id="884d5-126">On the **What do you want to do** dialog, click **Add an application my organization is developing**.</span></span>
   
    ![Uygulama oluşturma](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_04.png)
7. <span data-ttu-id="884d5-128">Üzerinde **bize uygulamanızı anlatın** iletişim kutusunda, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="884d5-128">On the **Tell us about your application** dialog, perform the following steps:</span></span>
   
    ![Uygulama oluşturma](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_05.png)
   
    <span data-ttu-id="884d5-130">a.</span><span class="sxs-lookup"><span data-stu-id="884d5-130">a.</span></span> <span data-ttu-id="884d5-131">İçinde **adı** metin kutusuna, uygulamanız için bir ad yazın (örneğin: AADIP Risk olayı API uygulama).</span><span class="sxs-lookup"><span data-stu-id="884d5-131">In the **Name** textbox, type a name for your application (e.g.: AADIP Risk Event API Application).</span></span>
   
    <span data-ttu-id="884d5-132">b.</span><span class="sxs-lookup"><span data-stu-id="884d5-132">b.</span></span> <span data-ttu-id="884d5-133">Olarak **türü**seçin **Web uygulaması ve / veya Web API**.</span><span class="sxs-lookup"><span data-stu-id="884d5-133">As **Type**, select **Web Application And / Or Web API**.</span></span>
   
    <span data-ttu-id="884d5-134">c.</span><span class="sxs-lookup"><span data-stu-id="884d5-134">c.</span></span> <span data-ttu-id="884d5-135">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="884d5-135">Click **Next**.</span></span>
8. <span data-ttu-id="884d5-136">Üzerinde **uygulama özellikleri** iletişim kutusunda, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="884d5-136">On the **App properties** dialog, perform the following steps:</span></span>
   
    ![Uygulama oluşturma](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_06.png)
   
    <span data-ttu-id="884d5-138">a.</span><span class="sxs-lookup"><span data-stu-id="884d5-138">a.</span></span> <span data-ttu-id="884d5-139">İçinde **oturum açma URL'si** metin kutusuna, türü `http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="884d5-139">In the **Sign-On URL** textbox, type `http://localhost`.</span></span>
   
    <span data-ttu-id="884d5-140">b.</span><span class="sxs-lookup"><span data-stu-id="884d5-140">b.</span></span> <span data-ttu-id="884d5-141">İçinde **uygulama kimliği URI'si** metin kutusuna, türü `http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="884d5-141">In the **App ID URI** textbox, type `http://localhost`.</span></span>
   
    <span data-ttu-id="884d5-142">c.</span><span class="sxs-lookup"><span data-stu-id="884d5-142">c.</span></span> <span data-ttu-id="884d5-143">**Tamamla**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="884d5-143">Click **Complete**.</span></span>

<span data-ttu-id="884d5-144">Can şimdi uygulamanızı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="884d5-144">Your can now configure your application.</span></span>

![Uygulama oluşturma](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_07.png)

## <a name="grant-your-application-permission-to-use-the-api"></a><span data-ttu-id="884d5-146">Uygulama API kullanma izni verin</span><span class="sxs-lookup"><span data-stu-id="884d5-146">Grant your application permission to use the API</span></span>
1. <span data-ttu-id="884d5-147">Uygulamanızın sayfasında, üst menüsünde tıklatın **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="884d5-147">On your application's page, in the menu on the top, click **Configure**.</span></span> 
   
    ![Uygulama oluşturma](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_08.png)
2. <span data-ttu-id="884d5-149">İçinde **diğer uygulamalara izinler** 'yi tıklatın **uygulama eklemek**.</span><span class="sxs-lookup"><span data-stu-id="884d5-149">In the **permissions to other applications** section, click **Add application**.</span></span>
   
    ![Uygulama oluşturma](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_09.png)
3. <span data-ttu-id="884d5-151">Üzerinde **diğer uygulamalara izinler** iletişim kutusunda, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="884d5-151">On the **permissions to other applications** dialog, perform the following steps:</span></span>
   
    ![Uygulama oluşturma](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_10.png)
   
    <span data-ttu-id="884d5-153">a.</span><span class="sxs-lookup"><span data-stu-id="884d5-153">a.</span></span> <span data-ttu-id="884d5-154">Seçin **Microsoft Graph**.</span><span class="sxs-lookup"><span data-stu-id="884d5-154">Select **Microsoft Graph**.</span></span>
   
    <span data-ttu-id="884d5-155">b.</span><span class="sxs-lookup"><span data-stu-id="884d5-155">b.</span></span> <span data-ttu-id="884d5-156">**Tamamla**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="884d5-156">Click **Complete**.</span></span>
4. <span data-ttu-id="884d5-157">Tıklatın **uygulama izinleri: 0**ve ardından **tüm kimlik risk olay bilgilerini okuma**.</span><span class="sxs-lookup"><span data-stu-id="884d5-157">Click **Application Permissions: 0**, and then select **Read all identity risk event information**.</span></span>
   
    ![Uygulama oluşturma](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_11.png)
5. <span data-ttu-id="884d5-159">Sayfanın alt kısmındaki **Kaydet**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="884d5-159">Click **Save** at the bottom of the page.</span></span>
   
    ![Uygulama oluşturma](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)

## <a name="get-an-access-key"></a><span data-ttu-id="884d5-161">Bir erişim anahtarı alma</span><span class="sxs-lookup"><span data-stu-id="884d5-161">Get an access key</span></span>
1. <span data-ttu-id="884d5-162">Uygulamanızın sayfasında içinde **anahtarları** bölümünde, 1 yıl süre olarak seçin.</span><span class="sxs-lookup"><span data-stu-id="884d5-162">On your application's page, in the **keys** section, select 1 year as duration.</span></span>
   
    ![Uygulama oluşturma](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_13.png)
2. <span data-ttu-id="884d5-164">Sayfanın alt kısmındaki **Kaydet**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="884d5-164">Click **Save** at the bottom of the page.</span></span>
   
    ![Uygulama oluşturma](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)
3. <span data-ttu-id="884d5-166">anahtarları bölümünde, yeni oluşturulan anahtarı değerini kopyalayın ve güvenli bir konuma yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="884d5-166">in the keys section, copy the value of your newly created key, and then paste it into a safe location.</span></span>
   
    ![Uygulama oluşturma](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_14.png)
   
   > [!NOTE]
   > <span data-ttu-id="884d5-168">Bu anahtar kaybederseniz, bu bölüme geri dönün ve yeni bir anahtar oluşturun gerekecektir.</span><span class="sxs-lookup"><span data-stu-id="884d5-168">If you lose this key, you will have to return to this section and create a new key.</span></span> <span data-ttu-id="884d5-169">Bu anahtarı bir gizli tutma: olan herkes verilerinize erişebilir.</span><span class="sxs-lookup"><span data-stu-id="884d5-169">Keep this key a secret: anyone who has it can access your data.</span></span>
   > 
   > 
4. <span data-ttu-id="884d5-170">İçinde **özellikleri** bölümünde, kopyalama **istemci kimliği**ve güvenli bir konuma yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="884d5-170">In the **properties** section, copy the **Client ID**, and then paste it into a safe location.</span></span> 

## <a name="authenticate-to-microsoft-graph-and-query-the-identity-risk-events-api"></a><span data-ttu-id="884d5-171">Microsoft Graph için kimlik doğrulaması ve kimlik Risk olayları API sorgulama</span><span class="sxs-lookup"><span data-stu-id="884d5-171">Authenticate to Microsoft Graph and query the Identity Risk Events API</span></span>
<span data-ttu-id="884d5-172">Bu noktada, olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="884d5-172">At this point, you should have:</span></span>

* <span data-ttu-id="884d5-173">İstemci kimliği üzerinde kopyalanır</span><span class="sxs-lookup"><span data-stu-id="884d5-173">The client ID you copied above</span></span>
* <span data-ttu-id="884d5-174">Yukarıdaki kopyaladığınız anahtar</span><span class="sxs-lookup"><span data-stu-id="884d5-174">The key you copied above</span></span>
* <span data-ttu-id="884d5-175">Kiracı'nın etki alanı adı</span><span class="sxs-lookup"><span data-stu-id="884d5-175">The name of your tenant's domain</span></span>

<span data-ttu-id="884d5-176">Kimlik doğrulaması için bir post İsteği Gönder `https://login.microsoft.com` gövdesinde aşağıdaki parametrelerle:</span><span class="sxs-lookup"><span data-stu-id="884d5-176">To authenticate, send a post request to `https://login.microsoft.com` with the following parameters in the body:</span></span>

* <span data-ttu-id="884d5-177">grant_type: "**client_credentials**"</span><span class="sxs-lookup"><span data-stu-id="884d5-177">grant_type: “**client_credentials**”</span></span>
* <span data-ttu-id="884d5-178">Kaynak: "**https://graph.microsoft.com**"</span><span class="sxs-lookup"><span data-stu-id="884d5-178">resource: “**https://graph.microsoft.com**”</span></span>
* <span data-ttu-id="884d5-179">client_id:<your client ID></span><span class="sxs-lookup"><span data-stu-id="884d5-179">client_id: <your client ID></span></span>
* <span data-ttu-id="884d5-180">client_secret:<your key></span><span class="sxs-lookup"><span data-stu-id="884d5-180">client_secret: <your key></span></span>

> [!NOTE]
> <span data-ttu-id="884d5-181">İçin değerler sağlaması gereken **client_id** ve **client_secret** parametresi.</span><span class="sxs-lookup"><span data-stu-id="884d5-181">You need to provide values for the **client_id** and the **client_secret** parameter.</span></span>
> 
> 

<span data-ttu-id="884d5-182">Başarılı olursa, bu kimlik doğrulama belirtecini döndürür.</span><span class="sxs-lookup"><span data-stu-id="884d5-182">If successful, this returns an authentication token.</span></span>  
<span data-ttu-id="884d5-183">API'yi çağırmak için bir başlığı aşağıdaki parametreyle oluşturun:</span><span class="sxs-lookup"><span data-stu-id="884d5-183">To call the API, create a header with the following parameter:</span></span>

    `Authorization`=”<token_type> <access_token>"


<span data-ttu-id="884d5-184">Kimlik doğrulamasını yaparken, belirteç türü ve erişim belirteci döndürülen belirteç bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="884d5-184">When authenticating, you can find the token type and access token in the returned token.</span></span>

<span data-ttu-id="884d5-185">Bu üst aşağıdaki API URL'si bir istek gönderin:`https://graph.microsoft.com/beta/identityRiskEvents`</span><span class="sxs-lookup"><span data-stu-id="884d5-185">Send this header as a request to the following API URL: `https://graph.microsoft.com/beta/identityRiskEvents`</span></span>

<span data-ttu-id="884d5-186">Yanıt başarılı olursa, kimlik risk olaylarına ve ilişkili veriler, ayrıştırılmış ve uygun gördüğünüz şekilde ele OData JSON biçiminde koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="884d5-186">The response, if successful, is a collection of identity risk events and associated data in the OData JSON format, which can be parsed and handled as see fit.</span></span>

<span data-ttu-id="884d5-187">Kimlik doğrulaması ve Powershell kullanarak API'yi çağıran için örnek kod aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="884d5-187">Here’s sample code for authenticating and calling the API using Powershell.</span></span>  
<span data-ttu-id="884d5-188">Yalnızca istemci Kimliğiniz Ekle anahtarı ve Kiracı etki alanı.</span><span class="sxs-lookup"><span data-stu-id="884d5-188">Just add your client ID, key, and tenant domain.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="884d5-189">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="884d5-189">Next steps</span></span>
<span data-ttu-id="884d5-190">Tebrikler, Microsoft Graph, ilk çağrıda yaptığınız.</span><span class="sxs-lookup"><span data-stu-id="884d5-190">Congratulations, you just made your first call to Microsoft Graph!</span></span>  
<span data-ttu-id="884d5-191">Şimdi kimlik risk olaylarını sorgular ve uygun gördüğünüz ancak verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="884d5-191">Now you can query identity risk events and use the data however you see fit.</span></span>

<span data-ttu-id="884d5-192">Microsoft Graph ve grafik API'sini kullanarak uygulamaların nasıl yapılandırıldığı hakkında daha fazla bilgi için kullanıma [belgelerine](https://graph.microsoft.io/docs) ve çok daha fazlası üzerinde [Microsoft Graph site](https://graph.microsoft.io/).</span><span class="sxs-lookup"><span data-stu-id="884d5-192">To learn more about Microsoft Graph and how to build applications using the Graph API, check out the [documentation](https://graph.microsoft.io/docs) and much more on the [Microsoft Graph site](https://graph.microsoft.io/).</span></span> <span data-ttu-id="884d5-193">Ayrıca, yer işareti emin [Azure AD Identity Protection API](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root) tüm grafiğinde kullanılabilir kimlik koruma API'leri listeler sayfası.</span><span class="sxs-lookup"><span data-stu-id="884d5-193">Also, make sure to bookmark the [Azure AD Identity Protection API](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root) page that lists all of the Identity Protection APIs available in Graph.</span></span> <span data-ttu-id="884d5-194">API aracılığıyla kimlik koruması çalışmak için yeni yollar eklediğimiz gibi ilgili sayfada görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="884d5-194">As we add new ways to work with Identity Protection via API, you’ll see them on that page.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="884d5-195">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="884d5-195">Additional resources</span></span>
* [<span data-ttu-id="884d5-196">Azure Active Directory kimlik koruması</span><span class="sxs-lookup"><span data-stu-id="884d5-196">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)
* [<span data-ttu-id="884d5-197">Azure Active Directory kimlik koruması tarafından algılanan risk olayı türleri</span><span class="sxs-lookup"><span data-stu-id="884d5-197">Types of risk events detected by Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-risk-events-types.md)
* [<span data-ttu-id="884d5-198">Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="884d5-198">Microsoft Graph</span></span>](https://graph.microsoft.io/)
* [<span data-ttu-id="884d5-199">Microsoft Graph genel bakış</span><span class="sxs-lookup"><span data-stu-id="884d5-199">Overview of Microsoft Graph</span></span>](https://graph.microsoft.io/docs)
* [<span data-ttu-id="884d5-200">Azure AD kimlik koruması hizmet kök</span><span class="sxs-lookup"><span data-stu-id="884d5-200">Azure AD Identity Protection Service Root</span></span>](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root)

