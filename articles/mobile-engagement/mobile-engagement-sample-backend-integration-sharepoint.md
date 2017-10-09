---
title: "aaaAzure Mobile Engagement - arka uç tümleştirme"
description: "Bir SharePoint arka uç toocreate Kampanyalar SharePoint ile Azure Mobile Engagement Bağlan"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 06297b43-579f-46e6-8a58-961a68f9aa09
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 89e1ef57db607d63c326a760b20260ad439f08b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement---api-integration"></a><span data-ttu-id="03a9f-103">Azure Mobile Engagement - API tümleştirme</span><span class="sxs-lookup"><span data-stu-id="03a9f-103">Azure Mobile Engagement - API integration</span></span>
<span data-ttu-id="03a9f-104">Otomatik bir pazarlama sisteminde, oluşturma ve ayrıca pazarlama kampanyaları hello etkinleştirme otomatik olarak gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="03a9f-104">In an automated marketing system, creating and activating hello marketing campaigns also occur automatically.</span></span> <span data-ttu-id="03a9f-105">Bu amaçla - Azure Mobile Engagement API'lerini de kullanarak bu tür otomatik pazarlama kampanyaları oluşturma sağlar.</span><span class="sxs-lookup"><span data-stu-id="03a9f-105">For this purpose - Azure Mobile Engagement enables creating such automated marketing campaigns using APIs as well.</span></span> 

<span data-ttu-id="03a9f-106">Genellikle müşteriler hello Mobile Engagement ön uç arabirimi toocreate Duyurular/yoklamalar vb. kendi pazarlama kampanyaları bir parçası olarak kullanın.</span><span class="sxs-lookup"><span data-stu-id="03a9f-106">Typically customers use hello Mobile Engagement front end interface toocreate announcements/polls etc as part of their marketing campaigns.</span></span> <span data-ttu-id="03a9f-107">Pazarlama kampanyaları olgun hale hello yoktur ancak gerek tooleverage hello veri kilitli hello arka uç sistemleri (örneğin, CRM sistem veya CMS sistemi SharePoint gibi), böylece Mobile'da Kampanyalar oluşturan tam otomatik bir işlem hattı oluşturulabilir Dinamik olarak hello arka uç sistemlerden akan hello verileri temel alan katılım.</span><span class="sxs-lookup"><span data-stu-id="03a9f-107">However as hello marketing campaigns become mature, there is a need tooleverage hello data locked in hello backend systems (like any CRM system or CMS system like SharePoint) so that a fully automated pipeline can be created which creates campaigns in Mobile Engagement dynamically based on hello data flowing in from hello backend systems.</span></span> 

![][5]

<span data-ttu-id="03a9f-108">Bu öğretici gelecek burada bir SharePoint iş kullanıcı bir SharePoint listesi veri pazarlama doldurur ve otomatik bir işlem hello listeden öğeler seçer ve sistem Mobile Engagement hello kullanarak bağlanır böyle bir senaryo aracılığıyla kullanılabilir REST API'leri hello toocreate bir pazarlama kampanyası hello SharePoint verileri.</span><span class="sxs-lookup"><span data-stu-id="03a9f-108">This tutorial goes through such a scenario where a SharePoint business user populates a SharePoint list with marketing data and an automated process picks up items from hello list and connects with hello Mobile Engagement system using hello available REST APIs toocreate a marketing campaign from hello SharePoint data.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="03a9f-109">Genel olarak, nasıl toocall herhangi Mobile Engagement REST API şekilde hello API'leri - kimlik doğrulama ve geçen parametreleri arama hello iki unsur ayrıntıları anlamak için bu örnek bir başlangıç noktası olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="03a9f-109">In general, you can use this sample as a starting point for understanding how toocall any Mobile Engagement REST API as it details hello two key aspects of calling hello APIs - authenticating and passing parameters.</span></span> 
> 
> 

## <a name="sharepoint-integration"></a><span data-ttu-id="03a9f-110">SharePoint Tümleştirmesi</span><span class="sxs-lookup"><span data-stu-id="03a9f-110">SharePoint integration</span></span>
1. <span data-ttu-id="03a9f-111">Burada, hangi hello örnek SharePoint listesi benzer verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="03a9f-111">Here is what hello sample SharePoint list looks like.</span></span> <span data-ttu-id="03a9f-112">**Başlık**, **kategori**, **NotificationTitle**, **ileti** ve **URL** hello duyuru oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="03a9f-112">**Title**, **Category**, **NotificationTitle**, **Message** and **URL** are used for creating hello announcement.</span></span> <span data-ttu-id="03a9f-113">Adlı bir sütun **IsProcessed** bir konsol programı hello biçiminde hello örnek otomasyon işlemi tarafından kullanılıyor.</span><span class="sxs-lookup"><span data-stu-id="03a9f-113">There is a column called **IsProcessed** which is used by hello sample automation process in hello form of a console program.</span></span> <span data-ttu-id="03a9f-114">Böylece, zamanlayabilirsiniz veya hello SharePoint listesine bir öğe eklendiğinde, doğrudan hello SharePoint iş akışı tooprogram oluşturma ve etkinleştiren hello duyuru kullanabileceğiniz bir Azure Web işi ya da bu konsol programı çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="03a9f-114">You can either run this console program as an Azure WebJob so that you can schedule it or you can directly use hello SharePoint workflow tooprogram creating and activating hello announcement when an item is inserted into hello SharePoint list.</span></span> <span data-ttu-id="03a9f-115">Bu örnekte kullanırız hello öğeler arasında hello SharePoint listesi ve bunların her biri için Azure Mobile Engagement duyuru Oluştur geçer ve ardından son olarak işaretler hello hello konsol program **IsProcessed** bayrağı toobe true olarak başarılı Duyuru oluşturma.</span><span class="sxs-lookup"><span data-stu-id="03a9f-115">In this sample we use hello console program which goes through hello items in hello SharePoint list and create announcement in Azure Mobile Engagement for each of them and then finally marks hello **IsProcessed** flag toobe true on successful announcement creation.</span></span>
   
    ![][1]
2. <span data-ttu-id="03a9f-116">Merhaba örnek hello koddan kullanıyoruz *SharePoint Online'ı kullanmaya hello istemci nesne modelini de uzaktan kimlik doğrulama* [burada](https://code.msdn.microsoft.com/Remote-Authentication-in-b7b6f43c) tooauthenticate hello SharePoint listesi.</span><span class="sxs-lookup"><span data-stu-id="03a9f-116">We are using hello code from hello sample *Remote Authentication in SharePoint Online Using hello Client Object Model* [here](https://code.msdn.microsoft.com/Remote-Authentication-in-b7b6f43c) tooauthenticate with hello SharePoint list.</span></span>
3. <span data-ttu-id="03a9f-117">Kimlik doğrulaması yapıldıktan sonra biz hello liste öğeleri toofind yeni oluşturulan tüm öğeleri döngü (olan **IsProcessed** = false).</span><span class="sxs-lookup"><span data-stu-id="03a9f-117">Once authenticated, we loop through hello list items toofind out any newly created items (which will have **IsProcessed** = false).</span></span> 
   
         static async void CreateCampaignFromSharepoint()
        {
            using (ClientContext clientContext = ClaimClientContext.GetAuthenticatedContext(targetSharepointSite))
            {
                // Using https://code.msdn.microsoft.com/Remote-Authentication-in-b7b6f43c for authentication     
                Web site = clientContext.Web;
                List list = site.Lists.GetByTitle("VideoContent");
                CamlQuery query = new CamlQuery();
                query.ViewXml = "<View/>";
                ListItemCollection items = list.GetItems(query);
   
                // Load hello SharePoint list
                clientContext.Load(list);
                clientContext.Load(items);
                clientContext.ExecuteQuery();
   
                // Loop through hello list toogo through all hello items which are newly added
                foreach (ListItem item in items)
                    if (item["IsProcessed"].ToString() != "Yes")
                    {
                        string name = item["Title"].ToString();
                        string notificationTitle = item["NotificationTitle"].ToString();
                        string notificationMessage = item["Message"].ToString();
                        string category = item["Category"].ToString();
                        string actionURL = ((FieldUrlValue)item["URL"]).Url;
   
                        // Send an HTTP request toocreate AzME campaign
                        int campaignId = CreateAzMECampaign
                            (name, notificationTitle, notificationMessage, category, actionURL).Result;
   
                        if (campaignId != -1)
                        {
                            // If creating campaign is successful then set this tootrue
                            item["IsProcessed"] = "Yes";
   
                            // Now try tooactivate hello campaign also
                            await ActivateAzMECampaign(campaignId);
                        }
                        else
                        {
                            item["IsProcessed"] = "Error";
                        }
                        item.Update();
                    }
                clientContext.ExecuteQuery();
            }
        }

## <a name="mobile-engagement-integration"></a><span data-ttu-id="03a9f-118">Mobile Engagement tümleştirmesi</span><span class="sxs-lookup"><span data-stu-id="03a9f-118">Mobile Engagement integration</span></span>
1. <span data-ttu-id="03a9f-119">Biz işleme gerektiren bir öğe bulunamadı - biz gerekli hello bilgi ayıklamak sonra toocreate duyuru hello gelen liste öğesi ve arama `CreateAzMECampaign` toocreate bunu ve arkasından `ActivateAzMECampaign` tooactivate onu.</span><span class="sxs-lookup"><span data-stu-id="03a9f-119">Once we find an item which requires processing - we extract hello information required toocreate an announcement from hello list item and call `CreateAzMECampaign` toocreate it and subsequently `ActivateAzMECampaign` tooactivate it.</span></span> <span data-ttu-id="03a9f-120">Bunlar aslında toohello Mobile Engagement arka çağırma REST API çağrıları aynıdır.</span><span class="sxs-lookup"><span data-stu-id="03a9f-120">These are essentially REST API calls calling toohello Mobile Engagement backend.</span></span> 
2. <span data-ttu-id="03a9f-121">Merhaba Mobile Engagement REST API'leri gerektiren bir **temel kimlik doğrulama düzeni yetkilendirme HTTP üstbilgisi** Merhaba oluşan `ApplicationId` ve hello `ApiKey` hangi hello Azure portal ' alın.</span><span class="sxs-lookup"><span data-stu-id="03a9f-121">hello Mobile Engagement REST APIs require a **Basic auth scheme authorization HTTP header** which is composed of hello `ApplicationId` and hello `ApiKey` which you get from hello Azure portal.</span></span> <span data-ttu-id="03a9f-122">Başlangıç anahtarı hello gelen kullandığınızdan emin olun **API anahtarları** bölüm ve *değil* hello gelen **sdk anahtarları** bölümü.</span><span class="sxs-lookup"><span data-stu-id="03a9f-122">Make sure that you are using hello Key from hello **api keys** section and *not* from hello **sdk keys** section.</span></span> 
   
   ![][2]
   
       static string CreateAuthZHeader()
       {
           string BasicAuthzHeaderString = "Basic " + EncodeTo64(ApplicationId + ":" + ApiKey);
           return BasicAuthzHeaderString;
       }
   
       static public string EncodeTo64(string toEncode)
       {
           byte[] toEncodeAsBytes = System.Text.ASCIIEncoding.ASCII.GetBytes(toEncode);
           string returnValue = System.Convert.ToBase64String(toEncodeAsBytes);
           return returnValue;
       }  
3. <span data-ttu-id="03a9f-123">Merhaba bildiri türü oluşturmak için kampanya - toohello bakın [belgelerine](https://msdn.microsoft.com/library/azure/mt683750.aspx).</span><span class="sxs-lookup"><span data-stu-id="03a9f-123">For creating hello announcement type campaign - refer toohello [documentation](https://msdn.microsoft.com/library/azure/mt683750.aspx).</span></span> <span data-ttu-id="03a9f-124">Merhaba kampanya belirtiyorsanız emin toomake gerek `kind` olarak *duyuru* ve hello [yükü](https://msdn.microsoft.com/library/azure/mt683751.aspx) ve FormUrlEncodedContent geçirme.</span><span class="sxs-lookup"><span data-stu-id="03a9f-124">You need toomake sure that you are specifying hello campaign `kind` as *announcement* and hello [payload](https://msdn.microsoft.com/library/azure/mt683751.aspx) and passing it as FormUrlEncodedContent.</span></span> 
   
        static async Task<int> CreateAzMECampaign(string campaignName, string notificationTitle, 
            string notificationMessage, string notificationCategory, string actionURL)
        {
            string createURIFragment = "/reach/1/create";
   
            using (var client = new HttpClient())
            {
                // Add Authorization Header
                client.DefaultRequestHeaders.TryAddWithoutValidation("Authorization", CreateAuthZHeader());
   
                // Create hello payload toosend hello content
                // Reference -> https://msdn.microsoft.com/library/dn913749.aspx
                string data =
                    @"{""name"":""" + campaignName + @"""," + 
                    @"""type"":""only_notif""," + 
                    @"""deliveryTime"":""any"","" + 
                    @""notificationTitle"":""" + notificationTitle + 
                    @""",""notificationMessage"":""" + notificationMessage + 
                    @""",""actionUrl"":""" + actionURL + @"""}";
   
                var content = new FormUrlEncodedContent(new[] 
                {
                    new KeyValuePair<string, string>("kind", "announcement"),
                    new KeyValuePair<string, string>("data", data),
                });
   
                // Send hello POST request
                var response = await client.PostAsync(url + createURIFragment, content);
                var responseString = response.Content.ReadAsStringAsync().Result;
                int campaignId = -1;
                if (response.StatusCode.ToString() == "OK")
                {
                    // This is hello campaign id
                    campaignId = Convert.ToInt32(responseString);
                    Console.WriteLine("Campaign successfully created with id {0}", campaignId);
                }
                else
                {
                    Console.WriteLine("Campaign creation failed with error - '{0}'", responseString);
                }
                return campaignId;
            }
        }
4. <span data-ttu-id="03a9f-125">Oluşturulan hello duyuru olduktan sonra hello Mobile Engagement portalında aşağıdaki hello gibi bir şey görürsünüz (Bu hello durumu Not taslak ve etkinleştirildi = = yok)</span><span class="sxs-lookup"><span data-stu-id="03a9f-125">Once you have hello announcement created, you will see something like hello following on hello Mobile Engagement portal (note that hello State=Draft and Activated = N/A)</span></span>
   
    ![][3]
5. <span data-ttu-id="03a9f-126">`CreateAzMECampaign`Bir duyurunun kampanya oluşturur ve kendi kimliği toohello çağıran döndürür.</span><span class="sxs-lookup"><span data-stu-id="03a9f-126">`CreateAzMECampaign` creates an announcement campaign and returns its Id toohello caller.</span></span> <span data-ttu-id="03a9f-127">`ActivateAzMECampaign`Bu kimliği hello parametresi tooactivate hello kampanya gerektirir.</span><span class="sxs-lookup"><span data-stu-id="03a9f-127">`ActivateAzMECampaign` requires this Id as hello parameter tooactivate hello campaign.</span></span> 
   
        static async Task<bool> ActivateAzMECampaign(int campaignId)
        {
            string activateUriFragment = "/reach/1/activate";
            using (var client = new HttpClient())
            {
                // Add Authorization Header
                client.DefaultRequestHeaders.TryAddWithoutValidation("Authorization", CreateAuthZHeader());
   
                var content = new FormUrlEncodedContent(new[] 
                {
                    new KeyValuePair<string, string>("kind", "announcement"),
                    new KeyValuePair<string, string>("id", campaignId.ToString()),
                });
   
                // Send hello POST request
                var response = await client.PostAsync(url + activateUriFragment, content);
                var responseString = response.Content.ReadAsStringAsync().Result;
                if (response.StatusCode.ToString() == "OK")
                {
                    Console.WriteLine("Campaign successfully activated");
                    return true;
                }
                else
                {
                    Console.WriteLine("Campaign activation failed with error - '{0}'", responseString);
                    return false;
                }
            }
        }
6. <span data-ttu-id="03a9f-128">Etkinleştirilen hello duyuru olduktan sonra hello aşağıdaki gibi bir şey hello Mobile Engagement portalında görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="03a9f-128">Once you have hello announcement activated, you will see something like hello following on hello Mobile Engagement portal:</span></span>
   
    ![][4]
7. <span data-ttu-id="03a9f-129">Merhaba kampanya etkinleştirilmiş almaz, hello kampanyası hello ölçütü karşılayan tüm cihazlarda bildirimleri görmesini başlar.</span><span class="sxs-lookup"><span data-stu-id="03a9f-129">As soon as hello campaign gets activated, any devices which satisfy hello criterion on hello campaign will start seeing notifications.</span></span> 
8. <span data-ttu-id="03a9f-130">Bu hello liste öğesi olarak işaretlenmiş göreceksiniz ile IsProcessed = false hello duyuru kampanya oluşturulduktan sonra tooTrue ayarlandı.</span><span class="sxs-lookup"><span data-stu-id="03a9f-130">You will also notice that hello list item marked with IsProcessed = false has been set tooTrue once hello announcement campaign is created.</span></span>  

<span data-ttu-id="03a9f-131">Bu örnek, çoğunlukla hello gerekli özellikleri belirtme basit duyuru kampanya oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="03a9f-131">This sample created a simple announcement campaign specifying mostly hello required properties.</span></span> <span data-ttu-id="03a9f-132">Merhaba bilgileri kullanarak hello portalından yapabilirsiniz kadar bu özelleştirebilirsiniz [burada](https://msdn.microsoft.com/library/azure/mt683751.aspx).</span><span class="sxs-lookup"><span data-stu-id="03a9f-132">You can customize this as much as you can from hello portal by using hello information [here](https://msdn.microsoft.com/library/azure/mt683751.aspx).</span></span> 

<!-- Images. -->
[1]: ./media/mobile-engagement-sample-backend-integration-sharepoint/sharepointlist.png
[2]: ./media/mobile-engagement-sample-backend-integration-sharepoint/properties.png
[3]: ./media/mobile-engagement-sample-backend-integration-sharepoint/new-announcement.png
[4]: ./media/mobile-engagement-sample-backend-integration-sharepoint/activate-announcement.png
[5]: ./media/mobile-engagement-sample-backend-integration-sharepoint/diagram.png



