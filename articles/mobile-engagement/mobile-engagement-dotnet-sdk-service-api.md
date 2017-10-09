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
# <a name="using-net-sdk-tooaccess-azure-mobile-engagement-service-apis"></a>.NET SDK'sı tooaccess Azure Mobile Engagement hizmet API'leri kullanarak
Azure Mobile Engagement kullanıma sunan bir kümesi, toomanage aygıtları için API'ler ulaşma/itme kampanyaları vb. toointeract bu API'leri ile biz de sağladığınız bir [Swagger dosyası](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) toogenerate SDK'ları için tercih ettiğiniz araçları ile birlikte kullanabileceğiniz dili. Merhaba kullanmanızı öneririz [AutoRest](https://github.com/Azure/AutoRest) toogenerate bizim Swagger dosyasından, SDK aracı.

> [!NOTE]
> Hello Azure Mobile Engagement hizmet Mart 2018 kullanımdan kaldırılır ve şu anda yalnızca kullanılabilir tooexisting müşterileri içindir. Daha fazla bilgi için bkz. [Mobile Engagement nedir?](https://azure.microsoft.com/en-us/services/mobile-engagement/).

Bir C# sarmalayıcı kullanarak bu API'leri ile toointeract sağlayan benzer şekilde bir .NET SDK'sı oluşturduk ve kimlik doğrulama belirteci anlaşma hello ve kendiniz yenileyin toodo yok.  

Bu örnek adımları toofollow toouse hello .NET SDK'sı hello kümesi üzerinden geçer:

1. Öncelikle, Apı'lerinizi kullanarak Azure Active Directory açıklandığı gibi hello için toosetup hello kimlik gereksinim [burada](mobile-engagement-api-authentication.md#authentication). Bu adımları Hello sonunda, geçerli bir olmalıdır **Subscriptionıd**, **Tenantıd**, **ApplicationId** ve **gizli**. 
2. Bir duyuru kampanya oluşturma hello senaryo ile Merhaba .NET SDK'sı ile çalışma basit bir Windows konsol uygulaması toodemonstrate kullanacağız. Bu nedenle Visual Studio'yu açın ve oluşturma bir **konsol uygulaması**.   
3. Ardından toodownload hello olarak kullanılabilir olan .NET SDK gerekir **Microsoft Azure katılım Yönetimi Kitaplığı** hello Nuget galerisinde [burada](https://www.nuget.org/packages/Microsoft.Azure.Management.Engagement/).
   Visual Studio'dan hello Nuget yüklüyorsanız hello işaretli onay sahip tooensure gerekir **INCLUDE yayın öncesi** hello paketi için arama seçeneği:
   
    ![][1]
4. Merhaba, `Program.cs` dosya, ad alanları aşağıdaki hello ekleyin:
   
        using Microsoft.Rest.Azure.Authentication;
        using Microsoft.Azure.Management.Engagement;
        using Microsoft.Azure.Management.Engagement.Models;
5. Sonraki kimlik doğrulaması için kullanacağız sabitleri izleyerek ve hello Mobile Engagement hello duyuru kampanya oluşturmakta olduğunuz uygulama ile etkileşim toodefine hello gerekir:
   
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
6. Merhaba tanımlamak `EngagementManagementClient` kullanacağız değişkeni toocall hello Mobile Engagement SDK'sı yöntemleri:
   
        static EngagementManagementClient engagementClient; 
7. Tooyour aşağıdaki hello eklemek `Main` yöntemi:
   
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
8. Merhaba başlatma mvc'deki yöntemi aşağıdaki hello tanımlamak `EngagementManagementClient` ilk kimlik doğrulaması ve kendisini hello Mobile Engagement toocreate hello duyuru kampanya planlama uygulamayla ilişkilendirme:
   
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
   > Toouse hello gerektiğini unutmayın **uygulama kaynak adı** hello AppName parametresi için hello Azure Yönetim Portalı'nda tanımlanan. 
   > 
   > 
9. Son olarak, daha önce başlatılmış hello EngagementClient toocreate basit bir kullanarak ilgilenebilmek hello CreateCampaign yöntemi tanımlayın **dilediğiniz zaman** & **yalnızca bildirim** kampanya Başlık ve ileti ile: 
   
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
10. Çalışma hello konsol uygulaması ve hello aşağıdaki hello kampanya başarılı oluşturulmasını görürsünüz:
    
    **Kampanya Kimliği '159' başarıyla oluşturuldu ve 'Taslak' durumda**

<!-- Images. -->

[1]: ./media/mobile-engagement-dotnet-sdk-service-api/include-prerelease.png
