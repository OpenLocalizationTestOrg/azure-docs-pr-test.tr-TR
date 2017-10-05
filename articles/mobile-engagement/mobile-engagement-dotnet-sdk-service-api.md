---
title: "Azure Mobile Engagement hizmet API'leri erişmek için .NET SDK kullanarak"
description: "Mobile Engagement .NET SDK'sı Azure Mobile Engagement hizmet API'leri erişmek için nasıl kullanılacağını açıklar"
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
ms.openlocfilehash: 6a497189268c5a1b7e269cc57904ebc77c1906fd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="using-net-sdk-to-access-azure-mobile-engagement-service-apis"></a><span data-ttu-id="8f789-103">Azure Mobile Engagement hizmet API'leri erişmek için .NET SDK kullanarak</span><span class="sxs-lookup"><span data-stu-id="8f789-103">Using .NET SDK to access Azure Mobile Engagement Service APIs</span></span>
<span data-ttu-id="8f789-104">Azure Mobile Engagement kullanıma sunan bir dizi API aygıtları yönetebilmeniz için Reach/anında iletme kampanyalarını vb.. Bu API'leri ile etkileşim kurmak için de size sağladığımız bir [Swagger dosyası](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) için tercih ettiğiniz dili SDK'ları oluşturmak için Araçlar ile kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8f789-104">Azure Mobile Engagement exposes a set of APIs for you to manage Devices, Reach/Push campaigns etc. To interact with these APIs, we also provide you a [Swagger file](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) that you can use with tools to generate SDKs for your preferred language.</span></span> <span data-ttu-id="8f789-105">Kullanmanızı öneririz [AutoRest](https://github.com/Azure/AutoRest) aracı, SDK bizim Swagger dosyasından oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8f789-105">We recommend using the [AutoRest](https://github.com/Azure/AutoRest) tool to generate your SDK from our Swagger file.</span></span>

> [!NOTE]
> <span data-ttu-id="8f789-106">Azure Mobile Engagement hizmeti, Mart 2018’de devre dışı bırakılacaktır. Şu anda yalnızca mevcut müşteriler tarafından kullanılabilmektedir.</span><span class="sxs-lookup"><span data-stu-id="8f789-106">The Azure Mobile Engagement service will be retired March 2018 and is currently only available to existing customers.</span></span> <span data-ttu-id="8f789-107">Daha fazla bilgi için bkz. [Mobile Engagement nedir?](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="8f789-107">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="8f789-108">Bu API'leri ile etkileşime olanak tanıyan bir C# sarmalayıcı kullanarak benzer şekilde bir .NET SDK'sı oluşturduk ve kimlik doğrulama belirteci anlaşma yapın ve kendiniz yenilemek yok.</span><span class="sxs-lookup"><span data-stu-id="8f789-108">We have created a .NET SDK in a similar manner which allows you to interact with these APIs using a C# wrapper and you don't have to do the authentication token negotiation and refresh yourself.</span></span>  

<span data-ttu-id="8f789-109">Bu örnek, .NET SDK'yı kullanmak için izlemeniz gereken adımlar kümesi üzerinden geçer:</span><span class="sxs-lookup"><span data-stu-id="8f789-109">This sample goes through the set of steps to follow to use the .NET SDK:</span></span>

1. <span data-ttu-id="8f789-110">Öncelikle, kimlik doğrulaması açıklandığı gibi Azure Active Directory'yi kullanarak, API için Kurulum gerekir [burada](mobile-engagement-api-authentication.md#authentication).</span><span class="sxs-lookup"><span data-stu-id="8f789-110">First of all, you need to setup the authentication for your APIs using the Azure Active Directory as described [here](mobile-engagement-api-authentication.md#authentication).</span></span> <span data-ttu-id="8f789-111">Bu adımları sonunda, geçerli bir olmalıdır **Subscriptionıd**, **Tenantıd**, **ApplicationId** ve **gizli**.</span><span class="sxs-lookup"><span data-stu-id="8f789-111">At the end of these steps, you should have a valid **SubscriptionId**, **TenantId**, **ApplicationId** and **Secret**.</span></span> 
2. <span data-ttu-id="8f789-112">.NET SDK'sı bir duyuru kampanya oluşturma senaryo ile çalışma göstermek için basit bir Windows konsol uygulaması kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="8f789-112">We will use a simple Windows Console app to demonstrate working with the .NET SDK with the scenario of creating an Announcement campaign.</span></span> <span data-ttu-id="8f789-113">Bu nedenle Visual Studio'yu açın ve oluşturma bir **konsol uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="8f789-113">So open up Visual Studio and create a **Console Application**.</span></span>   
3. <span data-ttu-id="8f789-114">Olarak kullanılabilir olan .NET SDK'yı yüklemek gereken sonraki **Microsoft Azure katılım Yönetimi Kitaplığı** Nuget galerisinde [burada](https://www.nuget.org/packages/Microsoft.Azure.Management.Engagement/).</span><span class="sxs-lookup"><span data-stu-id="8f789-114">Next you need to download the .NET SDK which is available as **Microsoft Azure Engagement Management Library** in the Nuget gallery [here](https://www.nuget.org/packages/Microsoft.Azure.Management.Engagement/).</span></span>
   <span data-ttu-id="8f789-115">Nuget Visual Studio'dan yüklüyorsanız, onay işaretli olduğundan emin olmak gereken **INCLUDE yayın öncesi** paketi için arama seçeneği:</span><span class="sxs-lookup"><span data-stu-id="8f789-115">If you are installing the Nuget from Visual Studio, you need to ensure that you have check marked the **Include prerelease** option while searching for the package:</span></span>
   
    ![][1]
4. <span data-ttu-id="8f789-116">İçinde `Program.cs` dosyasında, şu ad alanlarından ekleyin:</span><span class="sxs-lookup"><span data-stu-id="8f789-116">In the `Program.cs` file, add the following namespaces:</span></span>
   
        using Microsoft.Rest.Azure.Authentication;
        using Microsoft.Azure.Management.Engagement;
        using Microsoft.Azure.Management.Engagement.Models;
5. <span data-ttu-id="8f789-117">Sonraki kimlik doğrulaması ve Mobile Engagement uygulaması duyuru kampanya oluşturmakta olduğunuz etkileşim kullanacağız aşağıdaki sabitleri tanımlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="8f789-117">Next you need to define the following constants that we will use for authentication and interacting with the Mobile Engagement App in which you are creating the Announcement campaign:</span></span>
   
        // For authentication
        const string TENANT_ID = "<Your TenantId>";
        const string CLIENT_ID = "<Your Application Id>";
        const string CLIENT_SECRET = "<Your Secret>";
        const string SUBSCRIPTION_ID = "<Your Subscription Id>";
   
        // This is the Azure Resource group concept for grouping together resources 
        //  see here: https://azure.microsoft.com/en-us/documentation/articles/resource-group-portal/
        const string RESOURCE_GROUP = "";
   
        // For Mobile Engagement operations
        // App Collection Name 
        const string APP_COLLECTION_NAME = "";
        // Application Resource Name - make sure you are using the one as specified in the Azure portal (NOT the App Name)
        const string APP_RESOURCE_NAME = "";
6. <span data-ttu-id="8f789-118">Tanımlamak `EngagementManagementClient` Mobile Engagement SDK'sı yöntemleri çağırmak için kullanacağı değişkeni:</span><span class="sxs-lookup"><span data-stu-id="8f789-118">Define the `EngagementManagementClient` variable which we will use to call the Mobile Engagement SDK methods:</span></span>
   
        static EngagementManagementClient engagementClient; 
7. <span data-ttu-id="8f789-119">Aşağıdakileri ekleyin, `Main` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="8f789-119">Add the following to your `Main` method:</span></span>
   
        try
            {
                // Initialize the Engagement SDK to call out APIs. 
                InitEngagementClient().Wait();
   
                // Create a Reach campaign
                CreateCampaign().Wait();
            }
            catch (Exception ex)
            {
                Console.WriteLine(ex.InnerException.Message);
                throw ex;
            }
8. <span data-ttu-id="8f789-120">Başlatma mvc'deki aşağıdaki yöntemi tanımlayın `EngagementManagementClient` ilk kimlik doğrulaması ve kendisini içinde planladığınız duyuru kampanya oluşturmak Mobile Engagement uygulamayla ilişkilendirme:</span><span class="sxs-lookup"><span data-stu-id="8f789-120">Define the following method which takes care of initializing the `EngagementManagementClient` by first authenticating and then associating itself with the Mobile Engagement App in which you plan to create the Announcement campaign:</span></span>
   
        private static async Task InitEngagementClient()
        {
            var credentials = await ApplicationTokenProvider.LoginSilentAsync(TENANT_ID, CLIENT_ID, CLIENT_SECRET);
            engagementClient = new EngagementManagementClient(credentials) { SubscriptionId = SUBSCRIPTION_ID };
   
            // This is the Azure concept of ResourceGroup
            engagementClient.ResourceGroupName = RESOURCE_GROUP;
   
            // This is your Mobile Engagement App Collection & App Resource Name in which you create the campaign
            engagementClient.AppCollection = APP_COLLECTION_NAME;
            engagementClient.AppName = APP_RESOURCE_NAME;
        }
   
   > [!IMPORTANT]
   > <span data-ttu-id="8f789-121">Kullanmanız gereken Not **uygulama kaynak adı** AppName parametresi için Azure Yönetim Portalı'nda tanımlanan.</span><span class="sxs-lookup"><span data-stu-id="8f789-121">Note that you need to use the **App Resource Name** as defined in the Azure management portal for the AppName parameter.</span></span> 
   > 
   > 
9. <span data-ttu-id="8f789-122">Son olarak, hangi ele basit bir oluşturmak için daha önce başlatılmış EngagementClient kullanmanın önemli CreateCampaign yöntemi tanımlayın **dilediğiniz zaman** & **yalnızca bildirim** bir başlık ve ileti kampanyayla:</span><span class="sxs-lookup"><span data-stu-id="8f789-122">Lastly, define the CreateCampaign method which will take care of using the previously initialized EngagementClient to create a simple **AnyTime** & **Notification-only** campaign with a title and message:</span></span> 
   
        private async static Task CreateCampaign()
        {
            //  Refer to the Announcement Campaign format from here - 
            //      https://msdn.microsoft.com/en-us/library/azure/mt683751.aspx
            // Make sure you are passing all the non-optional parameters
            Campaign parameters = new Campaign(
                name:"WelcomeCampaign",
                notificationTitle: "Welcome", 
                notificationMessage: "Thank you for installing the app!",
                type:"only_notif",
                deliveryTime:"any"
                );
   
            // Refer to the Campaign Kinds from here - https://msdn.microsoft.com/en-us/library/azure/mt683742.aspx
            CampaignStateResult result = 
                await engagementClient.Campaigns.CreateAsync(CampaignKinds.Announcements, parameters);
            Console.WriteLine("Campaign Id '{0}' was created successfully and it is in '{1}' state", result.Id, result.State);
        }
10. <span data-ttu-id="8f789-123">Konsol uygulamasını çalıştırın ve aşağıdaki kampanya başarılı oluşturulmasını görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="8f789-123">Run the console app and you will see the following on successful creation of the campaign:</span></span>
    
    <span data-ttu-id="8f789-124">**Kampanya Kimliği '159' başarıyla oluşturuldu ve 'Taslak' durumda**</span><span class="sxs-lookup"><span data-stu-id="8f789-124">**Campaign Id '159' was created successfully and it is in 'draft' state**</span></span>

<!-- Images. -->

[1]: ./media/mobile-engagement-dotnet-sdk-service-api/include-prerelease.png
