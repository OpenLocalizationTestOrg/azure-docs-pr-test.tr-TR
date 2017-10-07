---
title: "aaaRetrain Machine Learning modellerini programlama aracılığıyla | Microsoft Docs"
description: "Tooprogrammatically bir model ve güncelleştirme hello web hizmeti toouse hello yeni eğitilen model Azure Machine Learning nasıl yeniden eğitme öğrenin."
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: 7ae4f977-e6bf-4d04-9dde-28a66ce7b664
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: raymondl;garye;v-donglo
ms.openlocfilehash: edbb64c08f7d9edf3c76e23e0cc7e14c0125d697
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-machine-learning-models-programmatically"></a>Machine Learning modellerini programlı olarak yeniden eğitme
Bu kılavuzda, tooprogrammatically bir Azure Machine Learning Web hizmeti C# ve makine öğrenme toplu yürütme hizmeti hello kullanarak nasıl yeniden eğitme öğreneceksiniz.

Merhaba modeli retrained sonra izlenecek yollar aşağıdaki hello nasıl tooupdate hello Tahmine dayalı web hizmetiniz modelinde göster:

* Merhaba Machine Learning Web Hizmetleri portalında bir Klasik web hizmeti dağıttıysanız bkz [bir Klasik web hizmeti yeniden eğitme](machine-learning-retrain-a-classic-web-service.md). 
* Yeni bir web hizmetini dağıttıysanız bkz [hello makine öğrenme yönetimi cmdlet'lerini kullanarak yeni bir web hizmeti yeniden eğitme](machine-learning-retrain-new-web-service-using-powershell.md).

İşlemi yeniden eğitme hello genel bakış için bkz: [makine öğrenimi modeline yeniden eğitme](machine-learning-retrain-machine-learning-model.md).

Yeni Azure Resource Manager web hizmeti bağlı olarak, var olan toostart istiyorsanız, bkz: [var olan bir Tahmine dayalı web hizmetini yeniden eğitme](machine-learning-retrain-existing-resource-manager-based-web-service.md).

## <a name="create-a-training-experiment"></a>Eğitim denemenizi oluşturma
Bu örnek için kullanacağınız "örnek 5: Eğitimi, Test, değerlendir ikili sınıflandırma: yetişkinlere yönelik veri kümesi" Merhaba Microsoft Azure Machine Learning örnekleri gelen. 

toocreate hello deneme:

1. Azure Machine Learning Studio tooMicrosoft oturum açın. 
2. Merhaba üzerinde hello panosunu sağ alt köşesindeki, tıklatın **yeni**.
3. Microsoft Samples Hello örnek 5'i seçin.
4. Merhaba deneme tuvalinin hello üstündeki toorename hello denemeyi hello deneme adını seçin "örnek 5: Eğitimi, Test, değerlendir ikili sınıflandırma: yetişkinlere yönelik veri kümesi".
5. Tür Census modeli.
6. Merhaba deneme tuvalinin Hello altındaki tıklatın **çalıştırmak**.
7. Tıklatın **Ayarla web hizmeti** seçip **web hizmeti yeniden eğitme**. 

Merhaba aşağıdaki hello ilk deneme gösterir.
   
   ![İlk deneme.][2]


## <a name="create-a-predictive-experiment-and-publish-as-a-web-service"></a>Tahmine dayalı bir deneme oluşturma ve bir web hizmeti olarak Yayımla
Ardından bir Predicative deneme oluşturun.

1. Merhaba deneme tuvalinin Hello altındaki tıklatın **Web hizmetinin ayarı** seçip **Tahmine dayalı Web hizmeti**. Bu hello modeli eğitilen Model olarak kaydeder ve web hizmeti giriş ve çıkış modülleri ekler. 
2. **Çalıştır**’a tıklayın. 
3. Merhaba deneme çalışması bittikten sonra tıklatın **Web hizmeti Dağıt [Klasik]** veya **Web hizmeti dağıtma [Yeni]**.

> [!NOTE] 
> toodeploy yeni bir web hizmeti yeterli izniniz hello abonelik toowhich, hello web Hizmeti'ni dağıtma olması gerekir. Daha fazla bilgi için [hello Azure Machine Learning Web Hizmetleri portalı kullanarak bir Web hizmeti yönetmek](machine-learning-manage-new-webservice.md). 

## <a name="deploy-hello-training-experiment-as-a-training-web-service"></a>Merhaba eğitim denemenizi eğitim web hizmeti olarak dağıtma
tooretrain hello eğitilen model, Retraining web hizmeti olarak oluşturulan hello eğitim denemenizi dağıtmanız gerekir. Bu web hizmeti gereken bir *Web hizmeti çıkış* modülü bağlı toohello  *[Train Model] [ train-model]*  modülü, toobe mümkün tooproduce yeni eğitilmiş modeller.

1. tooreturn toohello eğitim denemenizi hello sol bölmesinde hello denemeler simgesine tıklayın, sonra Census modeli adlı hello denemeye tıklayın.  
2. Web hizmeti Hello arama deneme öğeleri arama kutusuna yazın. 
3. Sürükleme bir *Web hizmeti girişi* hello modülü tuvale denemek ve çıktı toohello bağlanmak *Clean Missing Data* modülü.  Bu yeniden eğitme verilerinizi işlenir sağlar aynı hello özgün eğitim verilerinizi şekilde.
4. İki *web hizmeti çıkış* hello üzerine modülleri deneme tuvaline. Merhaba Hello çıkışına bağlayın *Train Model* hello modülü tooone ve hello çıktısı *Evaluate Model* toohello modülü diğer. Merhaba için web hizmeti çıkış **Train Model** bize hello yeni eğitilen modeli sağlar. Merhaba çok bağlı çıktı**Evaluate Model** bu modül çıkış, hangi hello performans sonuçlarını döndürür.
5. **Çalıştır**’a tıklayın. 

Sonraki hello eğitim denemenizi eğitilen bir modelin ve model değerlendirme sonuçlarını üreten bir web hizmeti olarak dağıtmanız gerekir. Bu, sonraki kümenizi Eylemler, Klasik web hizmeti veya yeni bir web hizmeti ile çalışma hakkında bağımlı tooaccomplish.  

**Klasik web hizmeti**

Merhaba deneme tuvalinin Hello altındaki tıklatın **Web hizmetinin ayarı** seçip **Web hizmeti Dağıt [Klasik]**. Merhaba Web hizmeti **Pano** için toplu iş yürütme hello API anahtarı ve hello API Yardım sayfası görüntülenir. Yalnızca hello toplu iş yürütme yöntemi, eğitilmiş modeller oluşturmak için kullanılabilir.

**Yeni web hizmeti**

Merhaba deneme tuvalinin Hello altındaki tıklatın **Web hizmetinin ayarı** seçip **Web hizmeti dağıtma [Yeni]**. Merhaba Web hizmeti Azure Machine Learning Web Hizmetleri portalı toohello dağıtma web hizmeti sayfası açılır. Web hizmetiniz için bir ad yazın ve ödeme planı seçin ve ardından **dağıtma**. Yalnızca hello toplu iş yürütme yöntemi eğitilmiş modeller oluşturmak için kullanılabilir.

Tamamlanan çalışan deneme sahip olduktan sonra her iki durumda da hello elde edilen iş akışı aşağıdaki gibi görünmelidir:

![Çalıştırdıktan sonra elde edilen iş akışı.][4]



## <a name="retrain-hello-model-with-new-data-using-bes"></a>Merhaba modeli BES kullanarak yeni verilerle yeniden eğitme
Bu örnekte, toocreate uygulama yeniden eğitme C# hello kullanıyor. Bu görev hello Python veya R örnek kodu tooaccomplish de kullanabilirsiniz.

toocall yeniden eğitme API'lerini hello:

1. Visual Studio'da bir C# konsol uygulaması oluşturun: **yeni** > **proje** > **Visual C#** > **Windows Klasik Masaüstü** > **konsol uygulaması (.NET Framework)**.
2. İçinde toohello Machine Learning Web hizmeti portalı oturum açın.
3. Klasik web hizmeti ile çalışıyorsanız, tıklatın **Klasik Web Hizmetleri**.
   1. Birlikte çalıştığınız hello web hizmeti tıklatın.
   2. Merhaba varsayılan uç noktasına tıklayın.
   3. Tıklatın **tüketen**.
   4. Merhaba hello sonundaki **Tüket** sayfasında hello **örnek kod** 'yi tıklatın **toplu**.
   5. Bu yordamın 5 toostep devam edin.
4. Yeni bir web hizmeti ile çalışıyorsanız, tıklatın **Web Hizmetleri**.
   1. Birlikte çalıştığınız hello web hizmeti tıklatın.
   2. Tıklatın **tüketen**.
   3. Merhaba de hello Tüket sayfasında hello sonundaki **örnek kod** 'yi tıklatın **toplu**.
5. Toplu iş yürütme Hello örnek C# kodu kopyalayın ve hello ad olduğu gibi kalır emin hello Program.cs dosyasına yapıştırın.

Merhaba açıklamaları belirtildiği gibi Hello Nuget paketini Microsoft.AspNet.WebApi.Client ekleyin. tooadd hello başvuru tooMicrosoft.WindowsAzure.Storage.dll, Microsoft Azure depolama hizmetleri için tooinstall hello istemci kitaplığı ilk gerekebilir. Daha fazla bilgi için bkz: [Windows depolama hizmetleri](https://www.nuget.org/packages/WindowsAzure.Storage).

### <a name="update-hello-apikey-declaration"></a>Merhaba apikey ile yapılan bildirimini güncelleştirin
Merhaba bulun **apikey ile yapılan** bildirimi.

    const string apiKey = "abc123"; // Replace this with hello API key for hello web service

Merhaba, **temel tüketim bilgileri** hello bölümünü **Tüket** sayfasında hello birincil anahtarını bulun ve toohello kopyalama **apikey ile yapılan** bildirimi.

### <a name="update-hello-azure-storage-information"></a>Hello Azure depolama bilgilerini güncelleştir
Merhaba BES örnek kod (örneğin "C:\temp\CensusIpnput.csv") yerel sürücü tooAzure depolama bir dosyadan yükler, işler ve hello sonuçları geri tooAzure depolama yazar.  

tooaccomplish bu görev için depolama hesabınızdan hello Klasik Azure portalı ve değerlerini hello kod içinde karşılık gelen hello güncelleştirme Merhaba, depolama hesabı adı, anahtar ve kapsayıcı bilgi almanız gerekir. 

1. Toohello Klasik Azure Portalı'nda oturum açın.
2. Merhaba sol gezinti sütununda **depolama**.
3. Depolama hesapları Hello listeden seçim bir toostore hello modeli retrained.
4. Merhaba sayfasının Hello altında tıklatın **erişim anahtarlarını Yönet**.
5. Kopyalayın ve hello kaydedin **birincil erişim anahtarını** ve Kapat hello iletişim. 
6. Merhaba hello sayfanın en üstünde, tıklatın **kapsayıcıları**.
7. Var olan bir kapsayıcı seçin veya yeni bir tane oluşturun ve hello adı kaydedin.

Merhaba bulun *StorageAccountName*, *StorageAccountKey*, ve *StorageContainerName* bildirimler ve güncelleştirme hello değerleri, kaydettiğiniz hello Azure portalı.

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure Storage Account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage Key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage Container name

Ayrıca, hello giriş dosyası, hello kodda belirtme hello konumda kullanılabilir olduğundan emin olmalısınız. 

### <a name="specify-hello-output-location"></a>Merhaba çıkış konumunu belirtin
Merhaba çıkış konumu hello Request yükü belirtirken, belirtilen hello dosyasının uzantısını hello *RelativeLocation* ilearner belirtilmelidir. 

Aşağıdaki örnek hello bakın:

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with hello location you would like toouse for your output file, and valid file extension (usually .csv for scoring results, or .ilearner for trained models)*/
            }
        },

> [!NOTE]
> Çıktı konumlarınıza Hello adlarını olanları bu kılavuzda hello web hizmeti çıkış modülleri eklenen hello siparişi temel alarak hello farklı olabilir. Bu eğitim denemenizi iki çıkışları ile ayarlama beri hello sonuçları her ikisi için depolama konumu bilgilerini içerir.  
> 
> 

![Çıktı yeniden eğitme][6]

Diyagram 4: çıkış yeniden eğitme.

## <a name="evaluate-hello-retraining-results"></a>Merhaba yeniden eğitme sonuçları değerlendirin
Merhaba uygulamayı çalıştırdığınızda, SAS belirteci gerekli tooaccess değerlendirme sonuçlarını hello ve hello çıktı hello URL içerir.

Merhaba birleştirerek retrained hello modelinin hello performans sonuçlarını görebilirsiniz *BaseLocation*, *RelativeLocation*, ve *SasBlobToken* hello çıkış sonuçlarından için *output2* (Merhaba çıktı görüntü yeniden eğitme önceki gösterildiği gibi) ve hello tam URL hello tarayıcınızın adres çubuğuna yapıştırma.  

Merhaba yeni eğitilen model bir varolan iyi yeterli tooreplace hello gerçekleştiğini hello sonuçları toodetermine inceleyin.

Kopya hello *BaseLocation*, *RelativeLocation*, ve *SasBlobToken* hello çıkış sonuçlarından, bunları işlem yeniden eğitme hello sırasında kullanın.

## <a name="next-steps"></a>Sonraki adımlar
Tıklayarak hello Tahmine dayalı web hizmetini dağıttıysanız **Web hizmeti Dağıt [Klasik]**, bkz: [bir Klasik web hizmeti yeniden eğitme](machine-learning-retrain-a-classic-web-service.md).

Tıklayarak hello Tahmine dayalı web hizmetini dağıttıysanız **Web hizmeti dağıtma [Yeni]**, bkz: [hello makine öğrenme yönetimi cmdlet'lerini kullanarak yeni bir web hizmeti yeniden eğitme](machine-learning-retrain-new-web-service-using-powershell.md).

<!-- Retrain a New web service using hello Machine Learning Management REST API -->


[1]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE01.png
[2]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE02.png
[3]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE03.png
[4]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE04.png
[5]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE05.png
[6]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE06.png
[7]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE07.png


<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
