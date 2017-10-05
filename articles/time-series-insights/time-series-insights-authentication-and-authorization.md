---
title: "Kimlik doğrulama ve yetkilendirme Azure zaman serisi Öngörüler API çağrılarının özel bir uygulama için yapılandırma | Microsoft Docs"
description: "Bu öğretici kimlik doğrulama ve yetkilendirme Azure zaman serisi Öngörüler API çağrılarının özel bir uygulama için nasıl yapılandırılacağı açıklanmaktadır."
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
ms.openlocfilehash: 4dd4865dc556e09a31d2cb7a32768aeb19ba9900
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="authentication-and-authorization-for-azure-time-series-insights-api"></a><span data-ttu-id="c7b82-103">Kimlik doğrulama ve yetkilendirme Azure zaman serisi Insights API'si</span><span class="sxs-lookup"><span data-stu-id="c7b82-103">Authentication and authorization for Azure Time Series Insights API</span></span>

<span data-ttu-id="c7b82-104">Bu makalede Azure zaman serisi Öngörüler API çağrılarının özel bir uygulamasının nasıl yapılandırılacağını açıklar.</span><span class="sxs-lookup"><span data-stu-id="c7b82-104">This article explains how to configure a custom application that calls the Azure Time Series Insights API.</span></span>

## <a name="service-principal"></a><span data-ttu-id="c7b82-105">Hizmet sorumlusu</span><span class="sxs-lookup"><span data-stu-id="c7b82-105">Service principal</span></span>

<span data-ttu-id="c7b82-106">Bu bölümde, uygulama adına zaman serisi Insights API'si erişmek için bir uygulama yapılandırma açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="c7b82-106">This section explains how to configure an application to access the Time Series Insights API on behalf of the application.</span></span> <span data-ttu-id="c7b82-107">Uygulama sonra verileri sorgulamak veya uygulama kimlik bilgileri ve kullanıcı kimlik bilgilerini değil zaman serisi Öngörüler ortamında başvuru veri yayımlama.</span><span class="sxs-lookup"><span data-stu-id="c7b82-107">The application can then query data or publish reference data in the Time Series Insights environment with application credentials and not the user credentials.</span></span>

<span data-ttu-id="c7b82-108">Gerektiren bir uygulamaya erişim zaman serisi Öngörüler varsa, Azure Active Directory Uygulama ayarlama ve veri erişimi ilkelerini zaman serisi Öngörüler ortamında atamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c7b82-108">When you have an application that needs to access Time Series Insights, you must set up an Azure Active Directory application and assign the data access policies in the Time Series Insights environment.</span></span> <span data-ttu-id="c7b82-109">Bu yaklaşım, çünkü uygulama kendi kimlik bilgileri altında çalışırken için tercih edilir:</span><span class="sxs-lookup"><span data-stu-id="c7b82-109">This approach is preferable to running the app under your own credentials because:</span></span>

* <span data-ttu-id="c7b82-110">Kendi izinlerinin farklı uygulama kimliği için izinleri atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c7b82-110">You can assign permissions to the app identity that are different from your own permissions.</span></span> <span data-ttu-id="c7b82-111">Genellikle, bu izinleri tam olarak hangi uygulama yapması gereken için kısıtlanır.</span><span class="sxs-lookup"><span data-stu-id="c7b82-111">Typically, these permissions are restricted to exactly what the app needs to do.</span></span> <span data-ttu-id="c7b82-112">Örneğin, yalnızca belirli bir zaman serisi Öngörüler ortamda verileri okumak uygulama izin verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c7b82-112">For example, you can allow the app to only read data in a particular Time Series Insights environment.</span></span>
* <span data-ttu-id="c7b82-113">Sizin Sorumluluklarınız değiştirirseniz uygulamanın kimlik bilgilerini değiştirmek zorunda değilsiniz.</span><span class="sxs-lookup"><span data-stu-id="c7b82-113">You don't have to change the app's credentials if your responsibilities change.</span></span>
* <span data-ttu-id="c7b82-114">Katılımsız betik çalışırken kimlik doğrulaması otomatikleştirmek için bir sertifika veya bir uygulama anahtarı kullanın.</span><span class="sxs-lookup"><span data-stu-id="c7b82-114">You can use a certificate or an application key to automate authentication when you're running an unattended script.</span></span>

<span data-ttu-id="c7b82-115">Bu makalede Azure Portalı aracılığıyla bu adımların nasıl gerçekleştirileceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="c7b82-115">This article shows you how to perform those steps through the Azure portal.</span></span> <span data-ttu-id="c7b82-116">Uygulama yalnızca bir kuruluşta çalıştırmak için burada hedeflenen bir tek kiracılı uygulama odaklanır.</span><span class="sxs-lookup"><span data-stu-id="c7b82-116">It focuses on a single-tenant application where the application is intended to run in only one organization.</span></span> <span data-ttu-id="c7b82-117">Genellikle, kuruluşunuzda çalıştırmak satır iş kolu uygulamaları için tek Kiracı uygulamaları kullanın.</span><span class="sxs-lookup"><span data-stu-id="c7b82-117">You typically use single-tenant applications for line-of-business applications that run in your organization.</span></span>

<span data-ttu-id="c7b82-118">Kurulum akışında üç üst düzey adımları içerir:</span><span class="sxs-lookup"><span data-stu-id="c7b82-118">The setup flow consists of three high-level steps:</span></span>

1. <span data-ttu-id="c7b82-119">Azure Active Directory'de bir uygulama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c7b82-119">Create an application in Azure Active Directory.</span></span>
2. <span data-ttu-id="c7b82-120">Bu uygulamanın zaman serisi Öngörüler ortam erişim yetkisi verir.</span><span class="sxs-lookup"><span data-stu-id="c7b82-120">Authorize this application to access the Time Series Insights environment.</span></span>
3. <span data-ttu-id="c7b82-121">Bir belirteç almak için uygulama kimliği ve anahtarı kullanın `"https://api.timeseries.azure.com/"` İzleyici veya kaynak.</span><span class="sxs-lookup"><span data-stu-id="c7b82-121">Use the application ID and key to acquire a token to the `"https://api.timeseries.azure.com/"` audience or resource.</span></span> <span data-ttu-id="c7b82-122">Belirteç ardından zaman serisi Öngörüler API'sini çağırmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c7b82-122">The token can then be used to call the Time Series Insights API.</span></span>

<span data-ttu-id="c7b82-123">Ayrıntılı adımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="c7b82-123">Here are the detailed steps:</span></span>

1. <span data-ttu-id="c7b82-124">Azure portalında seçin **Azure Active Directory** > **uygulama kayıtlar** > **yeni uygulama kaydı**.</span><span class="sxs-lookup"><span data-stu-id="c7b82-124">In the Azure portal, select **Azure Active Directory** > **App registrations** > **New application registration**.</span></span>

   ![Azure Active Directory'de yeni uygulama kaydı](media/authentication-and-authorization/active-directory-new-application-registration.png)  

2. <span data-ttu-id="c7b82-126">Uygulama bir ad verin, olmasını seçin **Web uygulaması / API**, için geçerli bir URI seçin **oturum açma URL'si**, tıklatıp **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="c7b82-126">Give the application a name, select the type to be **Web app / API**, select any valid URI for **Sign-on URL**, and click **Create**.</span></span>

   ![Azure Active Directory'de uygulama oluşturma](media/authentication-and-authorization/active-directory-create-web-api-application.png)

3. <span data-ttu-id="c7b82-128">Yeni oluşturulan uygulamanızı seçin ve uygulama Kimliğini, sık kullandığınız metin düzenleyicisine kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="c7b82-128">Select your newly created application and copy its application ID to your favorite text editor.</span></span>

   ![Uygulama Kimliğini kopyalayın](media/authentication-and-authorization/active-directory-copy-application-id.png)

4. <span data-ttu-id="c7b82-130">Seçin **anahtarları**anahtar adını girin, sona erme seçin ve tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="c7b82-130">Select **Keys**, enter the key name, select the expiration, and click **Save**.</span></span>

   ![Uygulama anahtarı seçin](media/authentication-and-authorization/active-directory-application-keys.png)

   ![Süre sonu ve anahtar adını girin ve Kaydet'e tıklayın.](media/authentication-and-authorization/active-directory-application-keys-save.png)

5. <span data-ttu-id="c7b82-133">Anahtarı, sık kullandığınız metin düzenleyicisine kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="c7b82-133">Copy the key to your favorite text editor.</span></span>

   ![Uygulama anahtarı kopyalayın](media/authentication-and-authorization/active-directory-copy-application-key.png)

6. <span data-ttu-id="c7b82-135">Zaman serisi Öngörüler ortamı için seçin **veri erişimi ilkelerini** tıklatıp **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="c7b82-135">For the Time Series Insights environment, select **Data Access Policies** and click **Add**.</span></span>

   ![Zaman serisi Öngörüler ortamına yeni veri erişim ilkesi Ekle](media/authentication-and-authorization/time-series-insights-data-access-policies-add.png)

7. <span data-ttu-id="c7b82-137">İçinde **Kullanıcı Seç** iletişim kutusunda, yapıştırma uygulama adı (2. adım) veya uygulama Kimliğinden (3. adım).</span><span class="sxs-lookup"><span data-stu-id="c7b82-137">In the **Select User** dialog box, paste the application name (from step 2) or application ID (from step 3).</span></span>

   ![Kullanıcı Seç iletişim kutusunda bir uygulama Bul](media/authentication-and-authorization/time-series-insights-data-access-policies-select-user.png)

8. <span data-ttu-id="c7b82-139">Rol seçin (**okuyucu** veri sorgulama için **katkıda bulunan** veri sorgulama ve başvuru verileri değiştirme) tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="c7b82-139">Select the role (**Reader** for querying data, **Contributor** for querying data and changing reference data) and click **Ok**.</span></span>

   ![Okuyucu ve katkıda bulunan rolü Seç iletişim kutusunda seçin](media/authentication-and-authorization/time-series-insights-data-access-policies-select-role.png)

9. <span data-ttu-id="c7b82-141">Tıklayarak ilkeyi kaydedin **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="c7b82-141">Save the policy by clicking **Ok**.</span></span>

10. <span data-ttu-id="c7b82-142">Uygulama adına belirtecini almak için uygulama Kimliğinden (3. adım) ve uygulama anahtarından (5. adım) kullanın.</span><span class="sxs-lookup"><span data-stu-id="c7b82-142">Use the application ID (from step 3) and application key (from step 5) to acquire the token on behalf of the application.</span></span> <span data-ttu-id="c7b82-143">Belirteç sonra geçirilebilir `Authorization` uygulama zaman serisi Insights API'si çağırdığında üstbilgi.</span><span class="sxs-lookup"><span data-stu-id="c7b82-143">The token can then be passed in the `Authorization` header when the application calls the Time Series Insights API.</span></span>

    <span data-ttu-id="c7b82-144">C# kullanıyorsanız, uygulama adına belirtecini almak için aşağıdaki kodu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c7b82-144">If you're using C#, you can use the following code to acquire the token on behalf of the application.</span></span> <span data-ttu-id="c7b82-145">Tam bir örnek için bkz: [C# kullanarak veri sorgulama](time-series-insights-query-data-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="c7b82-145">For a complete sample, see [Query data using C#](time-series-insights-query-data-csharp.md).</span></span>

    ```csharp
    var authenticationContext = new AuthenticationContext(
        "https://login.microsoftonline.com/common",
        TokenCache.DefaultShared);

    AuthenticationResult token = await authenticationContext.AcquireTokenAsync(
        // Set the resource URI to the Azure Time Series Insights API
        resource: "https://api.timeseries.azure.com/", 
        clientCredential: new ClientCredential(
            // Application ID of application registered in Azure Active Directory
            clientId: "1bc3af48-7e2f-4845-880a-c7649a6470b8", 
            // Application key of the application that's registered in Azure Active Directory
            clientSecret: "aBcdEffs4XYxoAXzLB1n3R2meNCYdGpIGBc2YC5D6L2="));

    string accessToken = token.AccessToken;
    ```

## <a name="next-steps"></a><span data-ttu-id="c7b82-146">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c7b82-146">Next steps</span></span>

<span data-ttu-id="c7b82-147">Uygulama kimliği ve anahtarı uygulamanızda kullanın.</span><span class="sxs-lookup"><span data-stu-id="c7b82-147">Use the application ID and key in your application.</span></span> <span data-ttu-id="c7b82-148">Zaman serisi Öngörüler API çağrılarının örnek kod için bkz: [C# kullanarak veri sorgulama](time-series-insights-query-data-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="c7b82-148">For sample code that calls the Time Series Insights API, see [Query data using C#](time-series-insights-query-data-csharp.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="c7b82-149">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="c7b82-149">See also</span></span>

* <span data-ttu-id="c7b82-150">[Sorgu API](/rest/api/time-series-insights/time-series-insights-reference-queryapi) için tam sorgu API Başvurusu</span><span class="sxs-lookup"><span data-stu-id="c7b82-150">[Query API](/rest/api/time-series-insights/time-series-insights-reference-queryapi) for the full Query API reference</span></span>
* [<span data-ttu-id="c7b82-151">Azure portalında bir hizmet sorumlusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="c7b82-151">Create a service principal in the Azure portal</span></span>](../azure-resource-manager/resource-group-create-service-principal-portal.md)
