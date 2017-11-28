---
title: "Azure Mobile Engagement - arka uç tümleştirme"
description: "SharePoint'ten kampanyalar oluşturmak için SharePoint arka ucu ile Azure Mobile Engagement Bağlan"
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
ms.openlocfilehash: d49f1094f4c3f170f3618f3e19e42266f9ae8858
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-mobile-engagement---api-integration"></a><span data-ttu-id="d27a3-103">Azure Mobile Engagement - API tümleştirme</span><span class="sxs-lookup"><span data-stu-id="d27a3-103">Azure Mobile Engagement - API integration</span></span>
<span data-ttu-id="d27a3-104">Otomatik bir pazarlama sisteminde, oluşturma ve pazarlama kampanyaları etkinleştirme de otomatik olarak gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="d27a3-104">In an automated marketing system, creating and activating the marketing campaigns also occur automatically.</span></span> <span data-ttu-id="d27a3-105">Bu amaçla - Azure Mobile Engagement API'lerini de kullanarak bu tür otomatik pazarlama kampanyaları oluşturma sağlar.</span><span class="sxs-lookup"><span data-stu-id="d27a3-105">For this purpose - Azure Mobile Engagement enables creating such automated marketing campaigns using APIs as well.</span></span> 

<span data-ttu-id="d27a3-106">Genellikle müşteriler kendi pazarlama kampanyaları bir parçası olarak Duyurular/yoklamalar vb. oluşturmak için Mobile Engagement ön uç arabirimi kullanın.</span><span class="sxs-lookup"><span data-stu-id="d27a3-106">Typically customers use the Mobile Engagement front end interface to create announcements/polls etc as part of their marketing campaigns.</span></span> <span data-ttu-id="d27a3-107">Ancak pazarlama kampanyaları olgun dönüşürken, böylece tam otomatik bir işlem hattı, arka uç sistemlerden akan verilere dinamik olarak temel Mobile Engagement, kampanyalar oluşturan oluşturulabilir (örneğin, CRM sistem veya CMS sistemi SharePoint gibi) arka uç sistemlerindeki kilitli verilerden yararlanın gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="d27a3-107">However as the marketing campaigns become mature, there is a need to leverage the data locked in the backend systems (like any CRM system or CMS system like SharePoint) so that a fully automated pipeline can be created which creates campaigns in Mobile Engagement dynamically based on the data flowing in from the backend systems.</span></span> 

![][5]

<span data-ttu-id="d27a3-108">Bu öğretici burada bir SharePoint iş kullanıcı bir SharePoint listesi Pazarlama verilerle doldurur ve otomatik bir işlem listeden öğeler seçer ve bir pazarlama kampanyası SharePoint verileri oluşturmak için kullanılabilir REST API'lerini kullanarak Mobile Engagement sistemiyle bağlanır böyle bir senaryo geçer.</span><span class="sxs-lookup"><span data-stu-id="d27a3-108">This tutorial goes through such a scenario where a SharePoint business user populates a SharePoint list with marketing data and an automated process picks up items from the list and connects with the Mobile Engagement system using the available REST APIs to create a marketing campaign from the SharePoint data.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="d27a3-109">Genel olarak, iki unsur dayanan API'leri - kimlik doğrulama ve geçen parametreleri çağırma ayrıntıları gibi herhangi bir Mobile Engagement REST API'yi çağırmak nasıl anlamak için bu örnek bir başlangıç noktası olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d27a3-109">In general, you can use this sample as a starting point for understanding how to call any Mobile Engagement REST API as it details the two key aspects of calling the APIs - authenticating and passing parameters.</span></span> 
> 
> 

## <a name="sharepoint-integration"></a><span data-ttu-id="d27a3-110">SharePoint Tümleştirmesi</span><span class="sxs-lookup"><span data-stu-id="d27a3-110">SharePoint integration</span></span>
1. <span data-ttu-id="d27a3-111">İşte örnek SharePoint listesi gibi görünüyor.</span><span class="sxs-lookup"><span data-stu-id="d27a3-111">Here is what the sample SharePoint list looks like.</span></span> <span data-ttu-id="d27a3-112">**Başlık**, **kategori**, **NotificationTitle**, **ileti** ve **URL** duyuru oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d27a3-112">**Title**, **Category**, **NotificationTitle**, **Message** and **URL** are used for creating the announcement.</span></span> <span data-ttu-id="d27a3-113">Adlı bir sütun **IsProcessed** bir konsol programı biçiminde örnek otomasyon işlemi tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d27a3-113">There is a column called **IsProcessed** which is used by the sample automation process in the form of a console program.</span></span> <span data-ttu-id="d27a3-114">Böylece, zamanlayabilirsiniz bir Azure Web işi bu konsolu program ya da çalışma olabilir veya SharePoint iş akışı oluşturma ve SharePoint listesine bir öğe eklendiğinde duyuruyu etkinleştirme programa doğrudan kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d27a3-114">You can either run this console program as an Azure WebJob so that you can schedule it or you can directly use the SharePoint workflow to program creating and activating the announcement when an item is inserted into the SharePoint list.</span></span> <span data-ttu-id="d27a3-115">Bu örnekte, öğeler arasında SharePoint listesi ve bunların her biri için Azure Mobile Engagement duyuru Oluştur gider ve son olarak işaretler konsol programı kullanıyoruz **IsProcessed** başarılı duyuru oluşturulması doğru olması için bayrak.</span><span class="sxs-lookup"><span data-stu-id="d27a3-115">In this sample we use the console program which goes through the items in the SharePoint list and create announcement in Azure Mobile Engagement for each of them and then finally marks the **IsProcessed** flag to be true on successful announcement creation.</span></span>
   
    ![][1]
2. <span data-ttu-id="d27a3-116">Örnek koddan kullanıyoruz *çevrimiçi istemci nesne modelini kullanarak SharePoint uzaktan kimlik doğrulama* [burada](https://code.msdn.microsoft.com/Remote-Authentication-in-b7b6f43c) SharePoint listesi ile kimlik doğrulaması için.</span><span class="sxs-lookup"><span data-stu-id="d27a3-116">We are using the code from the sample *Remote Authentication in SharePoint Online Using the Client Object Model* [here](https://code.msdn.microsoft.com/Remote-Authentication-in-b7b6f43c) to authenticate with the SharePoint list.</span></span>
3. <span data-ttu-id="d27a3-117">Kimlik doğrulaması yapıldıktan sonra Biz yeni oluşturulan tüm öğeleri bulmak için liste öğelerini döngü (olan **IsProcessed** = false).</span><span class="sxs-lookup"><span data-stu-id="d27a3-117">Once authenticated, we loop through the list items to find out any newly created items (which will have **IsProcessed** = false).</span></span> 
   
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
   
                // Load the SharePoint list
                clientContext.Load(list);
                clientContext.Load(items);
                clientContext.ExecuteQuery();
   
                // Loop through the list to go through all the items which are newly added
                foreach (ListItem item in items)
                    if (item["IsProcessed"].ToString() != "Yes")
                    {
                        string name = item["Title"].ToString();
                        string notificationTitle = item["NotificationTitle"].ToString();
                        string notificationMessage = item["Message"].ToString();
                        string category = item["Category"].ToString();
                        string actionURL = ((FieldUrlValue)item["URL"]).Url;
   
                        // Send an HTTP request to create AzME campaign
                        int campaignId = CreateAzMECampaign
                            (name, notificationTitle, notificationMessage, category, actionURL).Result;
   
                        if (campaignId != -1)
                        {
                            // If creating campaign is successful then set this to true
                            item["IsProcessed"] = "Yes";
   
                            // Now try to activate the campaign also
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

## <a name="mobile-engagement-integration"></a><span data-ttu-id="d27a3-118">Mobile Engagement tümleştirmesi</span><span class="sxs-lookup"><span data-stu-id="d27a3-118">Mobile Engagement integration</span></span>
1. <span data-ttu-id="d27a3-119">Biz işleme - gerektiren bir öğe bulduktan sonra biz liste öğesi ve çağrı duyuru oluşturmak için gereken bilgileri ayıklamak `CreateAzMECampaign` oluşturun ve daha sonra `ActivateAzMECampaign` etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="d27a3-119">Once we find an item which requires processing - we extract the information required to create an announcement from the list item and call `CreateAzMECampaign` to create it and subsequently `ActivateAzMECampaign` to activate it.</span></span> <span data-ttu-id="d27a3-120">Aslında Mobile Engagement arka ucuna çağırma REST API çağrıları bunlar.</span><span class="sxs-lookup"><span data-stu-id="d27a3-120">These are essentially REST API calls calling to the Mobile Engagement backend.</span></span> 
2. <span data-ttu-id="d27a3-121">Mobile Engagement REST API'leri gerektiren bir **temel kimlik doğrulama düzeni yetkilendirme HTTP üstbilgisi** oluşan `ApplicationId` ve `ApiKey` hangi Azure portalından alın.</span><span class="sxs-lookup"><span data-stu-id="d27a3-121">The Mobile Engagement REST APIs require a **Basic auth scheme authorization HTTP header** which is composed of the `ApplicationId` and the `ApiKey` which you get from the Azure portal.</span></span> <span data-ttu-id="d27a3-122">Anahtarından kullandığınızdan emin olun **API anahtarları** bölüm ve *değil* gelen **sdk anahtarları** bölümü.</span><span class="sxs-lookup"><span data-stu-id="d27a3-122">Make sure that you are using the Key from the **api keys** section and *not* from the **sdk keys** section.</span></span> 
   
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
3. <span data-ttu-id="d27a3-123">Duyuru oluşturmak için tür kampanya - başvurmak [belgelerine](https://msdn.microsoft.com/library/azure/mt683750.aspx).</span><span class="sxs-lookup"><span data-stu-id="d27a3-123">For creating the announcement type campaign - refer to the [documentation](https://msdn.microsoft.com/library/azure/mt683750.aspx).</span></span> <span data-ttu-id="d27a3-124">Kampanya belirtiyorsanız emin olmanız gerekir `kind` olarak *duyuru* ve [yükü](https://msdn.microsoft.com/library/azure/mt683751.aspx) ve FormUrlEncodedContent geçirme.</span><span class="sxs-lookup"><span data-stu-id="d27a3-124">You need to make sure that you are specifying the campaign `kind` as *announcement* and the [payload](https://msdn.microsoft.com/library/azure/mt683751.aspx) and passing it as FormUrlEncodedContent.</span></span> 
   
        static async Task<int> CreateAzMECampaign(string campaignName, string notificationTitle, 
            string notificationMessage, string notificationCategory, string actionURL)
        {
            string createURIFragment = "/reach/1/create";
   
            using (var client = new HttpClient())
            {
                // Add Authorization Header
                client.DefaultRequestHeaders.TryAddWithoutValidation("Authorization", CreateAuthZHeader());
   
                // Create the payload to send the content
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
   
                // Send the POST request
                var response = await client.PostAsync(url + createURIFragment, content);
                var responseString = response.Content.ReadAsStringAsync().Result;
                int campaignId = -1;
                if (response.StatusCode.ToString() == "OK")
                {
                    // This is the campaign id
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
4. <span data-ttu-id="d27a3-125">Oluşturulan duyuru olduktan sonra aşağıdakine benzer Mobile Engagement portalında görürsünüz (unutmayın durumu Taslak ve etkinleştirildi = = yok)</span><span class="sxs-lookup"><span data-stu-id="d27a3-125">Once you have the announcement created, you will see something like the following on the Mobile Engagement portal (note that the State=Draft and Activated = N/A)</span></span>
   
    ![][3]
5. <span data-ttu-id="d27a3-126">`CreateAzMECampaign`Bir duyurunun kampanya oluşturur ve çağırana kimliğini döndürür.</span><span class="sxs-lookup"><span data-stu-id="d27a3-126">`CreateAzMECampaign` creates an announcement campaign and returns its Id to the caller.</span></span> <span data-ttu-id="d27a3-127">`ActivateAzMECampaign`Bu kimliği kampanyayı etkinleştirmek için parametre olarak gerektirir.</span><span class="sxs-lookup"><span data-stu-id="d27a3-127">`ActivateAzMECampaign` requires this Id as the parameter to activate the campaign.</span></span> 
   
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
   
                // Send the POST request
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
6. <span data-ttu-id="d27a3-128">Etkinleştirilen duyuru olduktan sonra aşağıdakine benzer Mobile Engagement portalında görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="d27a3-128">Once you have the announcement activated, you will see something like the following on the Mobile Engagement portal:</span></span>
   
    ![][4]
7. <span data-ttu-id="d27a3-129">Kampanya etkinleştirilmiş almaz, kampanya ölçütü karşılayan tüm cihazlarda bildirimleri görmesini başlar.</span><span class="sxs-lookup"><span data-stu-id="d27a3-129">As soon as the campaign gets activated, any devices which satisfy the criterion on the campaign will start seeing notifications.</span></span> 
8. <span data-ttu-id="d27a3-130">Liste öğesi IsProcessed ile işaretlenmiş göreceksiniz = false duyuru kampanya oluşturulduğunda True olarak ayarlandı.</span><span class="sxs-lookup"><span data-stu-id="d27a3-130">You will also notice that the list item marked with IsProcessed = false has been set to True once the announcement campaign is created.</span></span>  

<span data-ttu-id="d27a3-131">Bu örnek, çoğunlukla gerekli özellikleri belirtme basit duyuru kampanya oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="d27a3-131">This sample created a simple announcement campaign specifying mostly the required properties.</span></span> <span data-ttu-id="d27a3-132">Bilgileri kullanarak portalından yapabilirsiniz kadar bu özelleştirebilirsiniz [burada](https://msdn.microsoft.com/library/azure/mt683751.aspx).</span><span class="sxs-lookup"><span data-stu-id="d27a3-132">You can customize this as much as you can from the portal by using the information [here](https://msdn.microsoft.com/library/azure/mt683751.aspx).</span></span> 

<!-- Images. -->
[1]: ./media/mobile-engagement-sample-backend-integration-sharepoint/sharepointlist.png
[2]: ./media/mobile-engagement-sample-backend-integration-sharepoint/properties.png
[3]: ./media/mobile-engagement-sample-backend-integration-sharepoint/new-announcement.png
[4]: ./media/mobile-engagement-sample-backend-integration-sharepoint/activate-announcement.png
[5]: ./media/mobile-engagement-sample-backend-integration-sharepoint/diagram.png



