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
# <a name="azure-mobile-engagement---api-integration"></a>Azure Mobile Engagement - API tümleştirme
Otomatik bir pazarlama sisteminde, oluşturma ve ayrıca pazarlama kampanyaları hello etkinleştirme otomatik olarak gerçekleşir. Bu amaçla - Azure Mobile Engagement API'lerini de kullanarak bu tür otomatik pazarlama kampanyaları oluşturma sağlar. 

Genellikle müşteriler hello Mobile Engagement ön uç arabirimi toocreate Duyurular/yoklamalar vb. kendi pazarlama kampanyaları bir parçası olarak kullanın. Pazarlama kampanyaları olgun hale hello yoktur ancak gerek tooleverage hello veri kilitli hello arka uç sistemleri (örneğin, CRM sistem veya CMS sistemi SharePoint gibi), böylece Mobile'da Kampanyalar oluşturan tam otomatik bir işlem hattı oluşturulabilir Dinamik olarak hello arka uç sistemlerden akan hello verileri temel alan katılım. 

![][5]

Bu öğretici gelecek burada bir SharePoint iş kullanıcı bir SharePoint listesi veri pazarlama doldurur ve otomatik bir işlem hello listeden öğeler seçer ve sistem Mobile Engagement hello kullanarak bağlanır böyle bir senaryo aracılığıyla kullanılabilir REST API'leri hello toocreate bir pazarlama kampanyası hello SharePoint verileri. 

> [!IMPORTANT]
> Genel olarak, nasıl toocall herhangi Mobile Engagement REST API şekilde hello API'leri - kimlik doğrulama ve geçen parametreleri arama hello iki unsur ayrıntıları anlamak için bu örnek bir başlangıç noktası olarak kullanabilirsiniz. 
> 
> 

## <a name="sharepoint-integration"></a>SharePoint Tümleştirmesi
1. Burada, hangi hello örnek SharePoint listesi benzer verilmiştir. **Başlık**, **kategori**, **NotificationTitle**, **ileti** ve **URL** hello duyuru oluşturmak için kullanılır. Adlı bir sütun **IsProcessed** bir konsol programı hello biçiminde hello örnek otomasyon işlemi tarafından kullanılıyor. Böylece, zamanlayabilirsiniz veya hello SharePoint listesine bir öğe eklendiğinde, doğrudan hello SharePoint iş akışı tooprogram oluşturma ve etkinleştiren hello duyuru kullanabileceğiniz bir Azure Web işi ya da bu konsol programı çalıştırabilirsiniz. Bu örnekte kullanırız hello öğeler arasında hello SharePoint listesi ve bunların her biri için Azure Mobile Engagement duyuru Oluştur geçer ve ardından son olarak işaretler hello hello konsol program **IsProcessed** bayrağı toobe true olarak başarılı Duyuru oluşturma.
   
    ![][1]
2. Merhaba örnek hello koddan kullanıyoruz *SharePoint Online'ı kullanmaya hello istemci nesne modelini de uzaktan kimlik doğrulama* [burada](https://code.msdn.microsoft.com/Remote-Authentication-in-b7b6f43c) tooauthenticate hello SharePoint listesi.
3. Kimlik doğrulaması yapıldıktan sonra biz hello liste öğeleri toofind yeni oluşturulan tüm öğeleri döngü (olan **IsProcessed** = false). 
   
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

## <a name="mobile-engagement-integration"></a>Mobile Engagement tümleştirmesi
1. Biz işleme gerektiren bir öğe bulunamadı - biz gerekli hello bilgi ayıklamak sonra toocreate duyuru hello gelen liste öğesi ve arama `CreateAzMECampaign` toocreate bunu ve arkasından `ActivateAzMECampaign` tooactivate onu. Bunlar aslında toohello Mobile Engagement arka çağırma REST API çağrıları aynıdır. 
2. Merhaba Mobile Engagement REST API'leri gerektiren bir **temel kimlik doğrulama düzeni yetkilendirme HTTP üstbilgisi** Merhaba oluşan `ApplicationId` ve hello `ApiKey` hangi hello Azure portal ' alın. Başlangıç anahtarı hello gelen kullandığınızdan emin olun **API anahtarları** bölüm ve *değil* hello gelen **sdk anahtarları** bölümü. 
   
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
3. Merhaba bildiri türü oluşturmak için kampanya - toohello bakın [belgelerine](https://msdn.microsoft.com/library/azure/mt683750.aspx). Merhaba kampanya belirtiyorsanız emin toomake gerek `kind` olarak *duyuru* ve hello [yükü](https://msdn.microsoft.com/library/azure/mt683751.aspx) ve FormUrlEncodedContent geçirme. 
   
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
4. Oluşturulan hello duyuru olduktan sonra hello Mobile Engagement portalında aşağıdaki hello gibi bir şey görürsünüz (Bu hello durumu Not taslak ve etkinleştirildi = = yok)
   
    ![][3]
5. `CreateAzMECampaign`Bir duyurunun kampanya oluşturur ve kendi kimliği toohello çağıran döndürür. `ActivateAzMECampaign`Bu kimliği hello parametresi tooactivate hello kampanya gerektirir. 
   
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
6. Etkinleştirilen hello duyuru olduktan sonra hello aşağıdaki gibi bir şey hello Mobile Engagement portalında görürsünüz:
   
    ![][4]
7. Merhaba kampanya etkinleştirilmiş almaz, hello kampanyası hello ölçütü karşılayan tüm cihazlarda bildirimleri görmesini başlar. 
8. Bu hello liste öğesi olarak işaretlenmiş göreceksiniz ile IsProcessed = false hello duyuru kampanya oluşturulduktan sonra tooTrue ayarlandı.  

Bu örnek, çoğunlukla hello gerekli özellikleri belirtme basit duyuru kampanya oluşturulur. Merhaba bilgileri kullanarak hello portalından yapabilirsiniz kadar bu özelleştirebilirsiniz [burada](https://msdn.microsoft.com/library/azure/mt683751.aspx). 

<!-- Images. -->
[1]: ./media/mobile-engagement-sample-backend-integration-sharepoint/sharepointlist.png
[2]: ./media/mobile-engagement-sample-backend-integration-sharepoint/properties.png
[3]: ./media/mobile-engagement-sample-backend-integration-sharepoint/new-announcement.png
[4]: ./media/mobile-engagement-sample-backend-integration-sharepoint/activate-announcement.png
[5]: ./media/mobile-engagement-sample-backend-integration-sharepoint/diagram.png



