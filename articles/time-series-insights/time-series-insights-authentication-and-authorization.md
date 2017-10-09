---
title: "aaaConfigure kimlik doğrulama ve yetkilendirme çağıran özel bir uygulama için hello Azure zaman serisi Insights API'si | Microsoft Docs"
description: "Bu öğretici Azure zaman serisi Insights API'si tooconfigure kimlik doğrulama ve yetkilendirme çağıran özel bir uygulama için nasıl hello açıklar"
keywords: 
services: time-series-insights
documentationcenter: 
author: dmdenmsft
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/24/2017
ms.author: dmden
ms.openlocfilehash: 5043468bfc2af3c0d27e8602508d92ba2848409e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-authorization-for-azure-time-series-insights-api"></a><span data-ttu-id="f6494-103">Kimlik doğrulama ve yetkilendirme Azure zaman serisi Insights API'si</span><span class="sxs-lookup"><span data-stu-id="f6494-103">Authentication and authorization for Azure Time Series Insights API</span></span>

<span data-ttu-id="f6494-104">Bu makalede nasıl tooconfigure çağıran özel bir uygulama hello Azure zaman serisi Insights API'si açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="f6494-104">This article explains how tooconfigure a custom application that calls hello Azure Time Series Insights API.</span></span>

## <a name="service-principal"></a><span data-ttu-id="f6494-105">Hizmet sorumlusu</span><span class="sxs-lookup"><span data-stu-id="f6494-105">Service principal</span></span>

<span data-ttu-id="f6494-106">Bu bölümde, nasıl tooconfigure bir uygulama tooaccess hello zaman serisi Insights API'si hello uygulama adına açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="f6494-106">This section explains how tooconfigure an application tooaccess hello Time Series Insights API on behalf of hello application.</span></span> <span data-ttu-id="f6494-107">Merhaba uygulaması sonra verileri sorgulamak veya uygulama kimlik bilgilerini ve değil hello kullanıcı kimlik bilgileri ile Merhaba zaman serisi Öngörüler ortamda başvuru veri yayımlama.</span><span class="sxs-lookup"><span data-stu-id="f6494-107">hello application can then query data or publish reference data in hello Time Series Insights environment with application credentials and not hello user credentials.</span></span>

<span data-ttu-id="f6494-108">Zaman serisi Öngörüler tooaccess gerektiren bir uygulamanız varsa, Azure Active Directory Uygulama ayarlama ve hello veri erişimi ilkelerini hello zaman serisi Öngörüler ortamında atamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f6494-108">When you have an application that needs tooaccess Time Series Insights, you must set up an Azure Active Directory application and assign hello data access policies in hello Time Series Insights environment.</span></span> <span data-ttu-id="f6494-109">Bu yaklaşım tercih toorunning hello uygulama kendi kimlik bilgileri altında nedeni:</span><span class="sxs-lookup"><span data-stu-id="f6494-109">This approach is preferable toorunning hello app under your own credentials because:</span></span>

* <span data-ttu-id="f6494-110">Kendi izinlerden farklıdır toohello uygulama kimliği izinleri atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f6494-110">You can assign permissions toohello app identity that are different from your own permissions.</span></span> <span data-ttu-id="f6494-111">Genellikle, bu kısıtlı tooexactly hangi hello uygulamanın toodo ihtiyacı izinlerdir.</span><span class="sxs-lookup"><span data-stu-id="f6494-111">Typically, these permissions are restricted tooexactly what hello app needs toodo.</span></span> <span data-ttu-id="f6494-112">Örneğin, belirli bir zaman serisi Öngörüler ortamda veri hello uygulama tooonly okuma izin verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f6494-112">For example, you can allow hello app tooonly read data in a particular Time Series Insights environment.</span></span>
* <span data-ttu-id="f6494-113">Sizin Sorumluluklarınız değiştirirseniz toochange hello uygulamanın kimlik bilgileri yok.</span><span class="sxs-lookup"><span data-stu-id="f6494-113">You don't have toochange hello app's credentials if your responsibilities change.</span></span>
* <span data-ttu-id="f6494-114">Katılımsız betik çalıştırılırken bir sertifika veya bir uygulamanın anahtar tooautomate kimlik doğrulaması kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f6494-114">You can use a certificate or an application key tooautomate authentication when you're running an unattended script.</span></span>

<span data-ttu-id="f6494-115">Bu makalede, bu adımları aracılığıyla tooperform hello Azure portalına nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="f6494-115">This article shows you how tooperform those steps through hello Azure portal.</span></span> <span data-ttu-id="f6494-116">Merhaba uygulaması yalnızca bir kuruluştaki hedeflenen toorun olduğu bir tek kiracılı uygulama odaklanır.</span><span class="sxs-lookup"><span data-stu-id="f6494-116">It focuses on a single-tenant application where hello application is intended toorun in only one organization.</span></span> <span data-ttu-id="f6494-117">Genellikle, kuruluşunuzda çalıştırmak satır iş kolu uygulamaları için tek Kiracı uygulamaları kullanın.</span><span class="sxs-lookup"><span data-stu-id="f6494-117">You typically use single-tenant applications for line-of-business applications that run in your organization.</span></span>

<span data-ttu-id="f6494-118">Merhaba Kurulum akışında üç üst düzey adımları içerir:</span><span class="sxs-lookup"><span data-stu-id="f6494-118">hello setup flow consists of three high-level steps:</span></span>

1. <span data-ttu-id="f6494-119">Azure Active Directory'de bir uygulama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f6494-119">Create an application in Azure Active Directory.</span></span>
2. <span data-ttu-id="f6494-120">Bu uygulama tooaccess hello zaman serisi Öngörüler ortamı yetkilendirin.</span><span class="sxs-lookup"><span data-stu-id="f6494-120">Authorize this application tooaccess hello Time Series Insights environment.</span></span>
3. <span data-ttu-id="f6494-121">Merhaba uygulama kimliği ve anahtarı tooacquire belirteci toohello kullanma `"https://api.timeseries.azure.com/"` İzleyici veya kaynak.</span><span class="sxs-lookup"><span data-stu-id="f6494-121">Use hello application ID and key tooacquire a token toohello `"https://api.timeseries.azure.com/"` audience or resource.</span></span> <span data-ttu-id="f6494-122">Merhaba belirteci sonra kullanılan toocall hello zaman serisi Insights API'si olabilir.</span><span class="sxs-lookup"><span data-stu-id="f6494-122">hello token can then be used toocall hello Time Series Insights API.</span></span>

<span data-ttu-id="f6494-123">Ayrıntılı adımlar hello şunlardır:</span><span class="sxs-lookup"><span data-stu-id="f6494-123">Here are hello detailed steps:</span></span>

1. <span data-ttu-id="f6494-124">Hello Azure portal, seçin **Azure Active Directory** > **uygulama kayıtlar** > **yeni uygulama kaydı**.</span><span class="sxs-lookup"><span data-stu-id="f6494-124">In hello Azure portal, select **Azure Active Directory** > **App registrations** > **New application registration**.</span></span>

   ![Azure Active Directory'de yeni uygulama kaydı](media/authentication-and-authorization/active-directory-new-application-registration.png)  

2. <span data-ttu-id="f6494-126">Merhaba uygulama adı, select hello türü toobe vermek **Web uygulaması / API**, için geçerli bir URI seçin **oturum açma URL'si**, tıklatıp **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="f6494-126">Give hello application a name, select hello type toobe **Web app / API**, select any valid URI for **Sign-on URL**, and click **Create**.</span></span>

   ![Azure Active Directory'de Merhaba uygulaması oluşturma](media/authentication-and-authorization/active-directory-create-web-api-application.png)

3. <span data-ttu-id="f6494-128">Yeni oluşturulan uygulamanızı seçin ve kendi uygulama kimliği tooyour sık kullandığınız metin Düzenleyicisi'ni kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="f6494-128">Select your newly created application and copy its application ID tooyour favorite text editor.</span></span>

   ![Merhaba uygulama Kimliğini kopyalayın](media/authentication-and-authorization/active-directory-copy-application-id.png)

4. <span data-ttu-id="f6494-130">Seçin **anahtarları**, hello anahtar adı, select hello sona erme girin ve tıklayın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="f6494-130">Select **Keys**, enter hello key name, select hello expiration, and click **Save**.</span></span>

   ![Uygulama anahtarı seçin](media/authentication-and-authorization/active-directory-application-keys.png)

   ![Merhaba anahtar adını ve sona erme girin ve Kaydet'e tıklayın.](media/authentication-and-authorization/active-directory-application-keys-save.png)

5. <span data-ttu-id="f6494-133">Merhaba anahtar tooyour sık kullandığınız metin düzenleyiciyi kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="f6494-133">Copy hello key tooyour favorite text editor.</span></span>

   ![Merhaba uygulama anahtarı kopyalayın](media/authentication-and-authorization/active-directory-copy-application-key.png)

6. <span data-ttu-id="f6494-135">Merhaba zaman serisi Öngörüler ortamı için seçin **veri erişimi ilkelerini** tıklatıp **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="f6494-135">For hello Time Series Insights environment, select **Data Access Policies** and click **Add**.</span></span>

   ![Yeni veri erişim ilkesi toohello zaman serisi Öngörüler ortama ekleyin](media/authentication-and-authorization/time-series-insights-data-access-policies-add.png)

7. <span data-ttu-id="f6494-137">Merhaba, **Kullanıcı Seç** iletişim kutusunda, Yapıştır hello uygulama adını (2. adım) veya uygulama Kimliğinden (3. adım).</span><span class="sxs-lookup"><span data-stu-id="f6494-137">In hello **Select User** dialog box, paste hello application name (from step 2) or application ID (from step 3).</span></span>

   ![Bir uygulama Bul hello Kullanıcı Seç iletişim kutusu](media/authentication-and-authorization/time-series-insights-data-access-policies-select-user.png)

8. <span data-ttu-id="f6494-139">Select hello rolü (**okuyucu** veri sorgulama için **katkıda bulunan** veri sorgulama ve başvuru verileri değiştirme) tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="f6494-139">Select hello role (**Reader** for querying data, **Contributor** for querying data and changing reference data) and click **Ok**.</span></span>

   ![Okuyucu ve katkıda bulunan hello rolü Seç iletişim kutusunda seçin](media/authentication-and-authorization/time-series-insights-data-access-policies-select-role.png)

9. <span data-ttu-id="f6494-141">Tıklayarak Hello ilkeyi kaydetmek **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="f6494-141">Save hello policy by clicking **Ok**.</span></span>

10. <span data-ttu-id="f6494-142">Merhaba uygulama kimliği (3. adım) ve uygulama (Başlangıç 5. adım) anahtar tooacquire hello belirteci hello uygulama adına kullanın.</span><span class="sxs-lookup"><span data-stu-id="f6494-142">Use hello application ID (from step 3) and application key (from step 5) tooacquire hello token on behalf of hello application.</span></span> <span data-ttu-id="f6494-143">Merhaba belirteci sonra hello geçirilebilir `Authorization` zaman serisi Insights API'si hello uygulama çağrıları hello zaman üstbilgi.</span><span class="sxs-lookup"><span data-stu-id="f6494-143">hello token can then be passed in hello `Authorization` header when hello application calls hello Time Series Insights API.</span></span>

    <span data-ttu-id="f6494-144">C# kullanıyorsanız, kod tooacquire hello belirteci hello uygulama adına aşağıdaki hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f6494-144">If you're using C#, you can use hello following code tooacquire hello token on behalf of hello application.</span></span> <span data-ttu-id="f6494-145">Tam bir örnek için bkz: [C# kullanarak veri sorgulama](time-series-insights-query-data-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="f6494-145">For a complete sample, see [Query data using C#](time-series-insights-query-data-csharp.md).</span></span>

    ```csharp
    var authenticationContext = new AuthenticationContext(
        "https://login.microsoftonline.com/common",
        TokenCache.DefaultShared);

    AuthenticationResult token = await authenticationContext.AcquireTokenAsync(
        // Set hello resource URI toohello Azure Time Series Insights API
        resource: "https://api.timeseries.azure.com/", 
        clientCredential: new ClientCredential(
            // Application ID of application registered in Azure Active Directory
            clientId: "1bc3af48-7e2f-4845-880a-c7649a6470b8", 
            // Application key of hello application that's registered in Azure Active Directory
            clientSecret: "aBcdEffs4XYxoAXzLB1n3R2meNCYdGpIGBc2YC5D6L2="));

    string accessToken = token.AccessToken;
    ```

## <a name="next-steps"></a><span data-ttu-id="f6494-146">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f6494-146">Next steps</span></span>

<span data-ttu-id="f6494-147">Merhaba uygulama kimliği ve anahtarı uygulamanızda kullanın.</span><span class="sxs-lookup"><span data-stu-id="f6494-147">Use hello application ID and key in your application.</span></span> <span data-ttu-id="f6494-148">Merhaba zaman serisi Öngörüler API çağrıları örnek kod için bkz: [C# kullanarak veri sorgulama](time-series-insights-query-data-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="f6494-148">For sample code that calls hello Time Series Insights API, see [Query data using C#](time-series-insights-query-data-csharp.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="f6494-149">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="f6494-149">See also</span></span>

* <span data-ttu-id="f6494-150">[Sorgu API](/rest/api/time-series-insights/time-series-insights-reference-queryapi) hello tam sorgu API Başvurusu için</span><span class="sxs-lookup"><span data-stu-id="f6494-150">[Query API](/rest/api/time-series-insights/time-series-insights-reference-queryapi) for hello full Query API reference</span></span>
* [<span data-ttu-id="f6494-151">Bir hizmet sorumlusu hello Azure portal oluşturma</span><span class="sxs-lookup"><span data-stu-id="f6494-151">Create a service principal in hello Azure portal</span></span>](../azure-resource-manager/resource-group-create-service-principal-portal.md)
