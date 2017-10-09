---
title: "Tahmine dayalı varolan aaaRetrain web hizmetini | Microsoft Docs"
description: "Web hizmeti toouse hello yeni eğitilen modeli Azure Machine learning'de tooretrain bir model ve güncelleştirme nasıl hello öğrenin."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: cc4c26a2-5672-4255-a767-cfd971e46775
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: v-donglo
ms.openlocfilehash: fb0760d0a2adc34fc5f3df1ae41bdac075f91bf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-an-existing-predictive-web-service"></a>Var olan bir Tahmine dayalı web hizmetini yeniden eğitme
Bu belgede senaryo aşağıdaki hello işlemlerinde yeniden eğitme hello açıklanmaktadır:

* Eğitim denemenizi ve kullanıma hazır hale getirilmiş web hizmeti olarak dağıttığınız bir tahmini deneme var.
* Tahmine dayalı web hizmeti toouse tooperform kendi Puanlama istediğiniz yeni veriler var.

> [!NOTE] 
> toodeploy yeni bir web hizmeti yeterli izniniz hello abonelik toowhich, hello web Hizmeti'ni dağıtma olması gerekir. Daha fazla bilgi için [hello Azure Machine Learning Web Hizmetleri portalı kullanarak bir Web hizmeti yönetmek](machine-learning-manage-new-webservice.md). 

Denemeler ve varolan web hizmeti ile başlayarak, aşağıdaki adımları toofollow gerekir:

1. Merhaba modeli güncelleştirin.
   1. Web hizmeti girişleri ve çıkışları, eğitim deneme tooallow değiştirin.
   2. Merhaba eğitim denemenizi yeniden eğitme bir web hizmeti olarak dağıtın.
   3. Merhaba eğitim deneme toplu yürütme hizmeti (BES) tooretrain hello modeli kullanır.
2. Hello Azure Machine Learning PowerShell cmdlet'leri tooupdate hello Tahmine dayalı denemeye kullanın.
   1. Tooyour Azure Resource Manager hesabı oturum açın.
   2. Merhaba web hizmeti tanımının alın.
   3. Merhaba web hizmeti tanımının JSON olarak dışarı aktarın.
   4. Merhaba başvuru toohello ilearner blob hello JSON güncelleştirin.
   5. Merhaba JSON web hizmeti tanımının alın.
   6. Merhaba web hizmeti ile yeni bir web hizmeti tanımının güncelleştirin.

## <a name="deploy-hello-training-experiment"></a>Merhaba eğitim denemenizi dağıtma
toodeploy hello eğitim denemenizi yeniden eğitme web hizmeti olarak web hizmeti girişleri ve çıkışları toohello modeli eklemeniz gerekir. Bağlanarak bir *Web hizmeti çıkış* modülü toohello deneme  *[Train Model] [ train-model]*  modülünde deneme eğitim hello etkinleştir Tahmine dayalı denemenizde kullanabileceğiniz yeni bir eğitilen model tooproduce. Varsa bir *Evaluate Model* modülü, çıktı olarak web hizmeti çıkış tooget hello değerlendirme sonuçlarını da ekleyebilirsiniz.

tooupdate eğitim denemenizi:

1. Bağlantı bir *Web hizmeti giriş* modülü tooyour veri girişi (örneğin, bir *Clean Missing Data* Modülü). Genellikle, giriş verilerinizi içinde işlenir tooensure istediğiniz aynı hello özgün eğitim verilerinizi şekilde.
2. Bağlantı bir *Web hizmeti çıkış* modülü toohello çıktısı, *Train Model* modülü.
3. Varsa bir *Evaluate Model* modülü ve toooutput hello değerlendirme sonuçlarını istiyorsanız, bağlanmak bir *Web hizmeti çıkış* modülü toohello çıktısı, *Evaluate Model* Modül.

Denemenizi çalıştırın.

Ardından, hello eğitim denemenizi eğitilen bir modelin ve model değerlendirme sonuçlarını üreten bir web hizmeti olarak dağıtmanız gerekir.  

Merhaba deneme tuvalinin Hello altındaki tıklatın **Web hizmetinin ayarı**ve ardından **Web hizmeti dağıtma [Yeni]**. Hello Azure Machine Learning Web Hizmetleri portalı açar toohello **Web hizmeti Dağıt** sayfası. Web hizmetiniz için bir ad yazın, ödeme planı seçin ve ardından **dağıtma**. Eğitilmiş modeller oluşturmak için yalnızca hello toplu iş yürütme yöntemi kullanabilirsiniz.

## <a name="retrain-hello-model-with-new-data-by-using-bes"></a>BES kullanarak Hello modeli yeni verilerle birlikte yeniden eğitme
Bu örnekte, biz toocreate uygulama yeniden eğitme C# hello kullanıyorsunuz. Bu görev Python veya R örnek kodu tooaccomplish de kullanabilirsiniz.

yeniden eğitme API'lerini toocall hello:

1. Visual Studio'da bir C# konsol uygulaması oluşturun: **yeni** > **proje** > **Visual C#** > **Windows Klasik Masaüstü** > **konsol uygulaması (.NET Framework)**.
2. İçinde toohello Machine Learning Web Hizmetleri portalında oturum açın.
3. Üzerinde çalıştığınız hello web hizmeti tıklatın.
4. Tıklatın **tüketen**.
5. Merhaba hello sonundaki **Tüket** sayfasında hello **örnek kod** 'yi tıklatın **toplu**.
6. Toplu iş yürütme Hello örnek C# kodu kopyalayın ve hello Program.cs dosyasına yapıştırın. Merhaba ad olduğu gibi kalır emin olun.

Merhaba açıklamaları belirtildiği gibi Hello NuGet paketini Microsoft.AspNet.WebApi.Client, ekleyin. tooadd hello başvuru tooMicrosoft.WindowsAzure.Storage.dll ilk ihtiyacınız olabilecek tooinstall hello [Azure depolama hizmetleri için İstemci Kitaplığı](https://www.nuget.org/packages/WindowsAzure.Storage).

Merhaba aşağıdaki ekran gösterilir hello **Tüket** hello Azure Machine Learning Web Hizmetleri portalında sayfası.

![Sayfa kullanma][1]

### <a name="update-hello-apikey-declaration"></a>Merhaba apikey ile yapılan bildirimini güncelleştirin
Merhaba bulun **apikey ile yapılan** bildirimi:

    const string apiKey = "abc123"; // Replace this with hello API key for hello web service

Merhaba, **temel tüketim bilgileri** hello bölümünü **Tüket** sayfasında hello birincil anahtarını bulun ve toohello kopyalama **apikey ile yapılan** bildirimi.

### <a name="update-hello-azure-storage-information"></a>Hello Azure depolama bilgilerini güncelleştir
Merhaba BES örnek kod bir yerel sürücüye (örneğin, "C:\temp\CensusIpnput.csv") tooAzure depolama bir dosyadan yükler, işler ve hello sonuçları geri tooAzure depolama yazar.  

tooupdate hello Azure depolama bilgilerini hello depolama hesabı adı, anahtar ve kapsayıcı bilgilerini depolama hesabınızdan hello Klasik Azure portalı ve denemenizi, çalıştırdıktan sonra güncelleştirme hello correspondi kaynaklanan hello almanız gerekir İş akışı benzer toohello aşağıdaki gibi olmalıdır:

![Çalıştırdıktan sonra elde edilen iş akışı][4]Merhaba kod NG değerleri.

1. İçinde toohello Klasik Azure portalında oturum açın.
2. Merhaba sol gezinti sütununda **depolama**.
3. Depolama hesapları Hello listeden seçim bir toostore hello modeli retrained.
4. Merhaba sayfasının Hello altında tıklatın **erişim anahtarlarını Yönet**.
5. Kopyalayın ve hello kaydedin **birincil erişim anahtarını** ve Kapat hello iletişim.
6. Merhaba hello sayfanın en üstünde, tıklatın **kapsayıcıları**.
7. Var olan bir kapsayıcıyı seçin veya yeni bir tane oluşturun ve hello adı kaydedin.

Merhaba bulun *StorageAccountName*, *StorageAccountKey*, ve *StorageContainerName* bildirimler ve hello Klasik portalından kaydedilen güncelleştirme hello değerleri .

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure storage account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage container name

Ayrıca bu hello giriş dosyası, hello kodda belirtme hello konumda kullanılabilir olduğundan emin olmalısınız.

### <a name="specify-hello-output-location"></a>Merhaba çıkış konumunu belirtin
Merhaba Request yükü hello çıkış konumu belirttiğinizde, belirtilen hello dosya uzantısını hello *RelativeLocation* olarak belirtilmelidir `ilearner`. Aşağıdaki örnek hello bakın:

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with hello location you want toouse for your output file and a valid file extension (usually .csv for scoring results or .ilearner for trained models)*/
            }
        },

Merhaba çıkış yeniden eğitme bir örnek şudur: ![çıkış yeniden eğitme][6]

## <a name="evaluate-hello-retraining-results"></a>Sonuçları yeniden eğitme hello değerlendir
Merhaba uygulamayı çalıştırdığınızda, hello çıktı hello URL ve gerekli tooaccess hello değerlendirme sonuçları paylaşılan erişim imzaları belirteci içerir.

Merhaba birleştirerek retrained hello modelinin hello performans sonuçlarını görebilirsiniz *BaseLocation*, *RelativeLocation*, ve *SasBlobToken* hello çıkış sonuçlarından için *output2* (Merhaba çıktı görüntü yeniden eğitme önceki gösterildiği gibi) ve hello tam URL hello tarayıcınızın adres çubuğuna yapıştırma.  

Merhaba yeni eğitilen model bir varolan iyi yeterli tooreplace hello gerçekleştiğini hello sonuçları toodetermine inceleyin.

Kopya hello *BaseLocation*, *RelativeLocation*, ve *SasBlobToken* hello çıkış sonuçlarından.

## <a name="retrain-hello-web-service"></a>Merhaba web hizmeti yeniden eğitme
Yeni bir web hizmeti yeniden eğitme, hello Tahmine dayalı web hizmeti tanımı tooreference hello yeni eğitilen modeli güncelleştirin. Merhaba web hizmeti tanımının hello eğitilen model hello web hizmetinin iç bir gösterimini ve doğrudan değiştirilebilir değil. Tahmine dayalı denemenizi ve değil eğitim denemenizi hello web hizmeti tanımının alırsınız emin olun.

## <a name="sign-in-tooazure-resource-manager"></a>TooAzure Resource Manager oturum
Öncelikle tooyour hello PowerShell ortamında Azure hesabından içinde hello kullanarak oturum açmanız gerekir [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet'i.

## <a name="get-hello-web-service-definition-object"></a>Merhaba Web hizmeti tanımının nesnesini alın
Ardından, arama hello tarafından hello Web hizmeti tanımının nesne get [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet'i.

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

toodetermine hello kaynak grubu adı var olan bir web hizmeti, aboneliğinizdeki tüm parametreleri toodisplay hello web Hizmetleri olmadan hello Get-AzureRmMlWebService cmdlet'ini çalıştırın. Merhaba web hizmetini bulun ve sonra web hizmeti kimliğini arayın Hello hello kaynak grubunun adıdır hello dördüncü hello kimliği öğesinde yalnızca hello sonra *resourceGroups* öğesi. Aşağıdaki örneğine hello hello kaynak grubu adı varsayılan MachineLearning SouthCentralUS ' dir.

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

Varolan bir alternatif olarak, toodetermine hello kaynak grubu adı web hizmeti, toohello Azure Machine Learning Web Hizmetleri portalında oturum açın. Merhaba web hizmeti seçin. Merhaba kaynak grubu adı öğedir hello beşinci hello hello web hizmeti URL'sini hemen sonra hello *resourceGroups* öğesi. Aşağıdaki örneğine hello hello kaynak grubu adı varsayılan MachineLearning SouthCentralUS ' dir.

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-hello-web-service-definition-object-as-json"></a>JSON olarak Hello Web hizmeti tanımının nesneyi ver
Merhaba, eğitilen model toouse hello toomodify hello tanımını yeni eğitilmiş model, önce hello kullanmanız gerekir [verme AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet tooexport onu tooa JSON biçimli dosya.

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-hello-reference-toohello-ilearner-blob"></a>Güncelleştirme hello başvuru toohello ilearner blob
Merhaba [eğitilen model], güncelleştirme hello Hello varlıkları bulun *URI* hello değerinde *locationInfo* hello hello ilearner blob URI'si düğümle. Merhaba URI hello birleştirerek oluşturulan *BaseLocation* ve hello *RelativeLocation* hello BES yeniden eğitme çağrısı hello çıktısından.

     "asset3": {
        "name": "Retrain Sample [trained model]",
        "type": "Resource",
        "locationInfo": {
          "uri": "https://mltestaccount.blob.core.windows.net/azuremlassetscontainer/baca7bca650f46218633552c0bcbba0e.ilearner"
        },
        "outputPorts": {
          "Results dataset": {
            "type": "Dataset"
          }
        }
      },

## <a name="import-hello-json-into-a-web-service-definition-object"></a>Bir Web hizmeti tanımının nesnesine Hello JSON aktarın
Merhaba kullanmalısınız [alma AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet tooconvert hello geri tooupdate hello predicative deneme kullanabileceğiniz bir Web hizmeti tanımının nesnesine JSON dosyasını değiştirdi.

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-hello-web-service"></a>Merhaba web hizmetini güncelleştirmek
Son olarak, hello kullan [güncelleştirme AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet tooupdate hello tahmini deneme.

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

[1]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-consume-page.png
[4]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE04.png
[6]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE06.png

<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
