---
title: "aaaUsing .NET SDK'sı tooaccess Azure Mobile Engagement hizmet API'leri"
description: "Nasıl toouse hello Mobile Engagement .NET SDK'sı tooaccess Azure Mobile Engagement hizmet API'leri açıklar"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: c07728aa-43f2-4238-8b4a-c9eddf9d838b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 812be6f507b29f7b2de6454e06face8082c2d161
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-net-sdk-tooaccess-azure-mobile-engagement-service-apis"></a><span data-ttu-id="1f239-103">.NET SDK'sı tooaccess Azure Mobile Engagement hizmet API'leri kullanarak</span><span class="sxs-lookup"><span data-stu-id="1f239-103">Using .NET SDK tooaccess Azure Mobile Engagement Service APIs</span></span>
<span data-ttu-id="1f239-104">Azure Mobile Engagement kullanıma sunan bir kümesi, toomanage aygıtları için API'ler ulaşma/itme kampanyaları vb. toointeract bu API'leri ile biz de sağladığınız bir [Swagger dosyası](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) toogenerate SDK'ları için tercih ettiğiniz araçları ile birlikte kullanabileceğiniz dili.</span><span class="sxs-lookup"><span data-stu-id="1f239-104">Azure Mobile Engagement exposes a set of APIs for you toomanage Devices, Reach/Push campaigns etc. toointeract with these APIs, we also provide you a [Swagger file](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) that you can use with tools toogenerate SDKs for your preferred language.</span></span> <span data-ttu-id="1f239-105">Merhaba kullanmanızı öneririz [AutoRest](https://github.com/Azure/AutoRest) toogenerate bizim Swagger dosyasından, SDK aracı.</span><span class="sxs-lookup"><span data-stu-id="1f239-105">We recommend using hello [AutoRest](https://github.com/Azure/AutoRest) tool toogenerate your SDK from our Swagger file.</span></span>

> [!NOTE]
> <span data-ttu-id="1f239-106">Hello Azure Mobile Engagement hizmet Mart 2018 kullanımdan kaldırılır ve şu anda yalnızca kullanılabilir tooexisting müşterileri içindir.</span><span class="sxs-lookup"><span data-stu-id="1f239-106">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="1f239-107">Daha fazla bilgi için bkz. [Mobile Engagement nedir?](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="1f239-107">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="1f239-108">Bir C# sarmalayıcı kullanarak bu API'leri ile toointeract sağlayan benzer şekilde bir .NET SDK'sı oluşturduk ve kimlik doğrulama belirteci anlaşma hello ve kendiniz yenileyin toodo yok.</span><span class="sxs-lookup"><span data-stu-id="1f239-108">We have created a .NET SDK in a similar manner which allows you toointeract with these APIs using a C# wrapper and you don't have toodo hello authentication token negotiation and refresh yourself.</span></span>  

<span data-ttu-id="1f239-109">Bu örnek adımları toofollow toouse hello .NET SDK'sı hello kümesi üzerinden geçer:</span><span class="sxs-lookup"><span data-stu-id="1f239-109">This sample goes through hello set of steps toofollow toouse hello .NET SDK:</span></span>

1. <span data-ttu-id="1f239-110">Öncelikle, Apı'lerinizi kullanarak Azure Active Directory açıklandığı gibi hello için toosetup hello kimlik gereksinim [burada](mobile-engagement-api-authentication.md#authentication).</span><span class="sxs-lookup"><span data-stu-id="1f239-110">First of all, you need toosetup hello authentication for your APIs using hello Azure Active Directory as described [here](mobile-engagement-api-authentication.md#authentication).</span></span> <span data-ttu-id="1f239-111">Bu adımları Hello sonunda, geçerli bir olmalıdır **Subscriptionıd**, **Tenantıd**, **ApplicationId** ve **gizli**.</span><span class="sxs-lookup"><span data-stu-id="1f239-111">At hello end of these steps, you should have a valid **SubscriptionId**, **TenantId**, **ApplicationId** and **Secret**.</span></span> 
2. <span data-ttu-id="1f239-112">Bir duyuru kampanya oluşturma hello senaryo ile Merhaba .NET SDK'sı ile çalışma basit bir Windows konsol uygulaması toodemonstrate kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="1f239-112">We will use a simple Windows Console app toodemonstrate working with hello .NET SDK with hello scenario of creating an Announcement campaign.</span></span> <span data-ttu-id="1f239-113">Bu nedenle Visual Studio'yu açın ve oluşturma bir **konsol uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="1f239-113">So open up Visual Studio and create a **Console Application**.</span></span>   
3. <span data-ttu-id="1f239-114">Ardından toodownload hello olarak kullanılabilir olan .NET SDK gerekir **Microsoft Azure katılım Yönetimi Kitaplığı** hello Nuget galerisinde [burada](https://www.nuget.org/packages/Microsoft.Azure.Management.Engagement/).</span><span class="sxs-lookup"><span data-stu-id="1f239-114">Next you need toodownload hello .NET SDK which is available as **Microsoft Azure Engagement Management Library** in hello Nuget gallery [here](https://www.nuget.org/packages/Microsoft.Azure.Management.Engagement/).</span></span>
   <span data-ttu-id="1f239-115">Visual Studio'dan hello Nuget yüklüyorsanız hello işaretli onay sahip tooensure gerekir **INCLUDE yayın öncesi** hello paketi için arama seçeneği:</span><span class="sxs-lookup"><span data-stu-id="1f239-115">If you are installing hello Nuget from Visual Studio, you need tooensure that you have check marked hello **Include prerelease** option while searching for hello package:</span></span>
   
    ![][1]
4. <span data-ttu-id="1f239-116">Merhaba, `Program.cs` dosya, ad alanları aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="1f239-116">In hello `Program.cs` file, add hello following namespaces:</span></span>
   
        using Microsoft.Rest.Azure.Authentication;
        using Microsoft.Azure.Management.Engagement;
        using Microsoft.Azure.Management.Engagement.Models;
5. <span data-ttu-id="1f239-117">Sonraki kimlik doğrulaması için kullanacağız sabitleri izleyerek ve hello Mobile Engagement hello duyuru kampanya oluşturmakta olduğunuz uygulama ile etkileşim toodefine hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="1f239-117">Next you need toodefine hello following constants that we will use for authentication and interacting with hello Mobile Engagement App in which you are creating hello Announcement campaign:</span></span>
   
        // For authentication
        const string TENANT_ID = "<Your TenantId>";
        const string CLIENT_ID = "<Your Application Id>";
        const string CLIENT_SECRET = "<Your Secret>";
        const string SUBSCRIPTION_ID = "<Your Subscription Id>";
   
        // This is hello Azure Resource group concept for grouping together resources 
        //  see here: https://azure.microsoft.com/en-us/documentation/articles/resource-group-portal/
        const string RESOURCE_GROUP = "";
   
        // For Mobile Engagement operations
        // App Collection Name 
        const string APP_COLLECTION_NAME = "";
        // Application Resource Name - make sure you are using hello one as specified in hello Azure portal (NOT hello App Name)
        const string APP_RESOURCE_NAME = "";
6. <span data-ttu-id="1f239-118">Merhaba tanımlamak `EngagementManagementClient` kullanacağız değişkeni toocall hello Mobile Engagement SDK'sı yöntemleri:</span><span class="sxs-lookup"><span data-stu-id="1f239-118">Define hello `EngagementManagementClient` variable which we will use toocall hello Mobile Engagement SDK methods:</span></span>
   
        static EngagementManagementClient engagementClient; 
7. <span data-ttu-id="1f239-119">Tooyour aşağıdaki hello eklemek `Main` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="1f239-119">Add hello following tooyour `Main` method:</span></span>
   
        try
            {
                // Initialize hello Engagement SDK toocall out APIs. 
                InitEngagementClient().Wait();
   
                // Create a Reach campaign
                CreateCampaign().Wait();
            }
            catch (Exception ex)
            {
                Console.WriteLine(ex.InnerException.Message);
                throw ex;
            }
8. <span data-ttu-id="1f239-120">Merhaba başlatma mvc'deki yöntemi aşağıdaki hello tanımlamak `EngagementManagementClient` ilk kimlik doğrulaması ve kendisini hello Mobile Engagement toocreate hello duyuru kampanya planlama uygulamayla ilişkilendirme:</span><span class="sxs-lookup"><span data-stu-id="1f239-120">Define hello following method which takes care of initializing hello `EngagementManagementClient` by first authenticating and then associating itself with hello Mobile Engagement App in which you plan toocreate hello Announcement campaign:</span></span>
   
        private static async Task InitEngagementClient()
        {
            var credentials = await ApplicationTokenProvider.LoginSilentAsync(TENANT_ID, CLIENT_ID, CLIENT_SECRET);
            engagementClient = new EngagementManagementClient(credentials) { SubscriptionId = SUBSCRIPTION_ID };
   
            // This is hello Azure concept of ResourceGroup
            engagementClient.ResourceGroupName = RESOURCE_GROUP;
   
            // This is your Mobile Engagement App Collection & App Resource Name in which you create hello campaign
            engagementClient.AppCollection = APP_COLLECTION_NAME;
            engagementClient.AppName = APP_RESOURCE_NAME;
        }
   
   > [!IMPORTANT]
   > <span data-ttu-id="1f239-121">Toouse hello gerektiğini unutmayın **uygulama kaynak adı** hello AppName parametresi için hello Azure Yönetim Portalı'nda tanımlanan.</span><span class="sxs-lookup"><span data-stu-id="1f239-121">Note that you need toouse hello **App Resource Name** as defined in hello Azure management portal for hello AppName parameter.</span></span> 
   > 
   > 
9. <span data-ttu-id="1f239-122">Son olarak, daha önce başlatılmış hello EngagementClient toocreate basit bir kullanarak ilgilenebilmek hello CreateCampaign yöntemi tanımlayın **dilediğiniz zaman** & **yalnızca bildirim** kampanya Başlık ve ileti ile:</span><span class="sxs-lookup"><span data-stu-id="1f239-122">Lastly, define hello CreateCampaign method which will take care of using hello previously initialized EngagementClient toocreate a simple **AnyTime** & **Notification-only** campaign with a title and message:</span></span> 
   
        private async static Task CreateCampaign()
        {
            //  Refer toohello Announcement Campaign format from here - 
            //      https://msdn.microsoft.com/en-us/library/azure/mt683751.aspx
            // Make sure you are passing all hello non-optional parameters
            Campaign parameters = new Campaign(
                name:"WelcomeCampaign",
                notificationTitle: "Welcome", 
                notificationMessage: "Thank you for installing hello app!",
                type:"only_notif",
                deliveryTime:"any"
                );
   
            // Refer toohello Campaign Kinds from here - https://msdn.microsoft.com/en-us/library/azure/mt683742.aspx
            CampaignStateResult result = 
                await engagementClient.Campaigns.CreateAsync(CampaignKinds.Announcements, parameters);
            Console.WriteLine("Campaign Id '{0}' was created successfully and it is in '{1}' state", result.Id, result.State);
        }
10. <span data-ttu-id="1f239-123">Çalışma hello konsol uygulaması ve hello aşağıdaki hello kampanya başarılı oluşturulmasını görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="1f239-123">Run hello console app and you will see hello following on successful creation of hello campaign:</span></span>
    
    <span data-ttu-id="1f239-124">**Kampanya Kimliği '159' başarıyla oluşturuldu ve 'Taslak' durumda**</span><span class="sxs-lookup"><span data-stu-id="1f239-124">**Campaign Id '159' was created successfully and it is in 'draft' state**</span></span>

<!-- Images. -->

[1]: ./media/mobile-engagement-dotnet-sdk-service-api/include-prerelease.png
