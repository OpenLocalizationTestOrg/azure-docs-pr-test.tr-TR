---
title: Klasik web hizmeti aaaRetrain | Microsoft Docs
description: "Tooprogrammatically bir model ve güncelleştirme hello web hizmeti toouse hello yeni eğitilen model Azure Machine Learning nasıl yeniden eğitme öğrenin."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondlaghaeian
editor: 
ms.assetid: e36e1961-9e8b-4801-80ef-46d80b140452
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: d3ba21ed75f02868535cb2fcac607643303a9554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-a-classic-web-service"></a>Klasik web hizmetini yeniden eğitme
Merhaba dağıttığınız Tahmine dayalı Web Hizmeti uç noktası Puanlama hello varsayılandır. Varsayılan uç noktalar hello ile senkronize eğitim ve puanlama denemeler özgün tutulur ve bu nedenle hello eğitilen model hello varsayılan uç noktası için değiştirilemez. tooretrain hello web hizmeti, yeni bir uç nokta toohello web hizmeti eklemeniz gerekir. 

## <a name="prerequisites"></a>Ön koşullar
Eğitim denemenizi ve Tahmine dayalı denemeye gösterildiği gibi ayarlamış olmanız gerekir [yeniden eğitme Machine Learning modellerini programlama aracılığıyla](machine-learning-retrain-models-programmatically.md). 

> [!IMPORTANT]
> Merhaba Tahmine dayalı denemeye Klasik machine learning web hizmeti dağıtılması gerekir. 
> 
> 

Web hizmetleri dağıtma hakkında ek bilgi için bkz: [bir Azure Machine Learning web hizmetini dağıtma](machine-learning-publish-a-machine-learning-web-service.md).

## <a name="add-a-new-endpoint"></a>Yeni bir uç nokta ekleyin
Merhaba dağıttığınız Tahmine dayalı Web hizmeti Puanlama hello özgün eğitim ve puanlama denemeler eğitilen model ile eşitlenmiş olarak saklanmasını uç noktası varsayılan içerir. tooupdate, web hizmeti toowith yeni bir modeli yeni bir Puanlama uç noktası oluşturmanız gerekir. 

Yeni bir Puanlama uç noktası, hello hello eğitilen model ile güncelleştirilebilir Tahmine dayalı Web hizmeti üzerinde toocreate:

> [!NOTE]
> Merhaba uç nokta toohello Tahmine dayalı Web hizmeti, hello eğitim Web hizmeti ekleme emin olun. Eğitim ve Tahmine dayalı bir Web hizmeti doğru olarak dağıttıysanız, listelenen iki ayrı bir web hizmetleri görmeniz gerekir. Merhaba Tahmine dayalı Web hizmeti, "[Tahmine dayalı exp.]" bitmelidir.
> 
> 

Yeni bir uç noktası tooa web hizmeti eklemenin üç yolu vardır:

1. Programlama yoluyla
2. Merhaba Microsoft Azure Web Hizmetleri portalı kullanın
3. Merhaba Klasik Azure portalını kullanın

### <a name="programmatically-add-an-endpoint"></a>Program aracılığıyla bir uç nokta ekleme
Bu konuda sağlanan hello örnek kodu kullanarak Puanlama uç noktalar ekleyebilirsiniz [github deposunu](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs).

### <a name="use-hello-microsoft-azure-web-services-portal-tooadd-an-endpoint"></a>Merhaba Microsoft Azure Web Hizmetleri portalı tooadd bir uç nokta kullanın
1. Machine Learning Studio'da hello sol gezinti sütuna, Web Hizmetleri'ı tıklatın.
2. Merhaba web hizmeti Pano Hello altındaki tıklatın **yönetin uç noktaları Önizleme**.
3. **Ekle**'ye tıklayın.
4. Bir ad ve hello yeni uç noktası için bir açıklama yazın. Merhaba günlüğe kaydetme düzeyi ve örnek verileri etkinleştirilip etkinleştirilmediğini seçin. Günlüğe kaydetme hakkında daha fazla bilgi için bkz: [Machine Learning web hizmetleri için günlüğe kaydetmeyi etkinleştirmek](machine-learning-web-services-logging.md).

### <a name="use-hello-azure-classic-portal-tooadd-an-endpoint"></a>Hello Azure Klasik portalı tooadd bir uç nokta kullanın
1. İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com).
2. Merhaba soldaki menüde tıklatın **Machine Learning**.
3. Adı altında çalışma alanına tıklayın ve ardından **Web Hizmetleri**.
4. Adı altında tıklatın **Census modeli [Tahmine dayalı exp.]** .
5. Merhaba sayfasının Hello altında tıklatın **uç nokta Ekle**. Uç noktaları ekleme hakkında daha fazla bilgi için bkz: [uç noktaları oluşturma](machine-learning-create-endpoint.md). 

## <a name="update-hello-added-endpoints-trained-model"></a>Uç noktanın eğitilen Model güncelleştirme hello eklendi
toocomplete hello yeniden eğitme işlemi, eklediğiniz hello yeni uç nokta eğitilen modelini hello güncelleştirmeniz gerekir.

* Merhaba Klasik Azure portalını kullanarak hello yeni uç nokta eklediyseniz, hello portalında hello yeni uç noktanın adına tıklayın, ardından hello **UpdateResource** bağlantı gereksinim tooupdate hello uç noktanın modeli tooget hello URL.
* Merhaba örnek kodu kullanarak hello endpoint eklediyseniz, bu hello tarafından tanımlanan hello Yardım URL'si konumunu içeren *HelpLocationURL* hello çıktı değeri.

tooretrieve hello yol URL'si:

1. Merhaba URL'sini kopyalayıp tarayıcınıza yapıştırın.
2. Merhaba güncelleştirme kaynağı bağlantısına tıklayın.
3. Merhaba hello PATCH isteği gönderme URL'sini kopyalayın. Örneğin:
   
     DÜZELTME EKİ URL: https://management.azureml.net/workspaces/00bf70534500b34rebfa1843d6/webservices/af3er32ad393852f9b30ac9a35b/endpoints/newendpoint2

Daha önce oluşturduğunuz endpoint Puanlama hello eğitilen model tooupdate hello artık kullanabilirsiniz.

Aşağıdaki örnek kod hello gösterir, nasıl toouse hello *BaseLocation*, *RelativeLocation*, *SasBlobToken*ve düzeltme eki URL tooupdate hello uç.

    private async Task OverwriteModel()
    {
        var resourceLocations = new
        {
            Resources = new[]
            {
                new
                {
                    Name = "Census Model [trained model]",
                    Location = new AzureBlobDataReference()
                    {
                        BaseLocation = "https://esintussouthsus.blob.core.windows.net/",
                        RelativeLocation = "your endpoint relative location", //from hello output, for example: “experimentoutput/8946abfd-79d6-4438-89a9-3e5d109183/8946abfd-79d6-4438-89a9-3e5d109183.ilearner”
                        SasBlobToken = "your endpoint SAS blob token" //from hello output, for example: “?sv=2013-08-15&sr=c&sig=37lTTfngRwxCcf94%3D&st=2015-01-30T22%3A53%3A06Z&se=2015-01-31T22%3A58%3A06Z&sp=rl”
                    }
                }
            }
        };

        using (var client = new HttpClient())
        {
            client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", apiKey);

            using (var request = new HttpRequestMessage(new HttpMethod("PATCH"), endpointUrl))
            {
                request.Content = new StringContent(JsonConvert.SerializeObject(resourceLocations), System.Text.Encoding.UTF8, "application/json");
                HttpResponseMessage response = await client.SendAsync(request);

                if (!response.IsSuccessStatusCode)
                {
                    await WriteFailedResponse(response);
                }

                // Do what you want with a successful response here.
            }
        }
    }

Merhaba *apikey ile yapılan* ve hello *endpointUrl* için uç nokta panodan hello çağrısı alınabilir.

Merhaba hello değerini *adı* parametresinde *kaynakları* eşleşme hello hello kaynak adını kaydedilmiş eğitilen Model hello Tahmine dayalı denemesinde. tooget hello kaynak adı:

1. İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com).
2. Merhaba soldaki menüde tıklatın **Machine Learning**.
3. Adı altında çalışma alanına tıklayın ve ardından **Web Hizmetleri**.
4. Adı altında tıklatın **Census modeli [Tahmine dayalı exp.]** .
5. Eklediğiniz hello yeni uç noktasına tıklayın.
6. Merhaba uç nokta Panoda tıklatın **güncelleştirme kaynağı**.
7. Merhaba güncelleştirme kaynağı API belgelerine sayfasında hello web hizmeti hello bulabilirsiniz **kaynak adı** altında **güncelleştirilebilir kaynakları**.

Merhaba uç noktası güncelleniyor bitirmeden SAS belirteci süresi dolarsa, bir GET hello iş kimliği tooobtain yeni bir belirteç ile gerçekleştirmeniz gerekir.

Merhaba kodu başarıyla çalıştırıldı, hello yeni uç nokta yaklaşık 30 saniye içinde retrained hello modelini kullanarak başlamanız gerekir.

## <a name="summary"></a>Özet
Kullanarak yeniden eğitme API'lerini Merhaba, eğitilen modelini senaryoları gibi etkinleştirme Tahmine dayalı bir Web hizmeti hello güncelleştirebilirsiniz:

* Yeni verilerle yeniden eğitme düzenli modeli.
* Kullanıcıların kendi verilerini kullanarak hello modeli yeniden eğitme yapmalarına izin hello amacı ile bir model toocustomers dağıtımı.

## <a name="next-steps"></a>Sonraki adımlar
[Bir Azure Machine Learning Klasik web hizmeti Hello yeniden eğitme sorunlarını giderme](machine-learning-troubleshooting-retraining-models.md)

