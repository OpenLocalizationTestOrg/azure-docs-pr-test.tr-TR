---
title: "aaaCreate bir deneme birden çok modellerinden | Microsoft Docs"
description: "Birden çok Machine Learning modellerini PowerShell toocreate kullanın ve web hizmeti uç hello ile aynı algoritmanın ancak farklı eğitim veri kümeleri."
services: machine-learning
documentationcenter: 
author: hning86
manager: jhubbard
editor: cgronlun
ms.assetid: 1076b8eb-5a0d-4ac5-8601-8654d9be229f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: garye;haining
ms.openlocfilehash: 4a258a8ab26395d4169a058520151c860e16e169
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-many-machine-learning-models-and-web-service-endpoints-from-one-experiment-using-powershell"></a>PowerShell kullanarak bir denemeden çok sayıda Machine Learning modeli ve web hizmeti uç noktası oluşturma
Bir ortak makine öğrenimi sorun şudur: hello birçok modelleri toocreate istediğiniz aynı eğitim iş akışı ve kullanım hello aynı algoritması, ancak giriş olarak farklı eğitim veri kümeleri. Bu makale size nasıl gösterir toodo bu yalnızca bir deneme kullanarak Azure Machine Learning Studio'daki ölçekte.

Örneğin, bir genel bisiklet kiralama Acentelik işletme sahibi varsayalım. Regresyon modeli toopredict hello kiralama isteğe bağlı geçmiş verilere dayanan toobuild istiyor. Merhaba dünya genelindeki 1.000 kiralama konumunuz varsa ve her tarih, saat, hava durumu gibi önemli özellikler içeren konumu ve belirli tooeach konumunun trafiği için bir veri kümesi derledik.

Bir kez tüm konumlar arasında tüm hello veri kümeleri birleştirilmiş bir sürümünü kullanarak modelinizi eğitmek. Konumların her bir benzersiz ortamı olduğundan, daha iyi bir yaklaşım olur, ancak ayrı ayrı her konum için hello veri kümesini kullanarak, regresyon modeli tootrain olabilir. Bu şekilde, her eğitilen model ele geçirebilir hesap hello farklı depolama boyutları, birim, coğrafi konum, popülasyon, bisiklet kolay trafiği ortamı *vb.*.

Merhaba en iyi yaklaşımı olabilir ancak her bir benzersiz bir konumu temsil eden toocreate 1.000 eğitim denemeler Azure Machine learning'de istemiyorsanız. Bunaltıcı görev olmasının yanı sıra, aynı zamanda olup her deneme tüm hello eğitim veri kümesi dışında aynı bileşenleri hello olacağından oldukça verimsiz gibi görünüyor.

Neyse ki, biz bu hello kullanarak gerçekleştirebilirsiniz [Azure Machine Learning yeniden eğitme API](machine-learning-retrain-models-programmatically.md) ve otomatik otomatikleştirme hello görevle [Azure Machine Learning PowerShell](machine-learning-powershell-module.md).

> [!NOTE]
> toomake bizim örnek çalıştırmak daha hızlı, biz 1.000 too10 konumlardan hello sayısını azaltın. Ancak hello aynı ilkeleri ve yordamları too1, 000 konumları uygulanır. Merhaba yalnızca 1.000 veri kümelerinden tootrain istiyorsanız, aşağıdaki PowerShell betikleri paralel hello çalışan toothink istemenizdir farktır. Nasıl bu makalede, ancak hello kapsamı dışındadır toodo PowerShell örnekleri çoklu iş parçacığı hello Internet üzerinde bulabilirsiniz.  
> 
> 

## <a name="set-up-hello-training-experiment"></a>Merhaba eğitim denemenizi ayarlayın
Toouse örneği yapacağız [eğitim denemenizi](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Training-Experiment-1) , hello zaten oluşturduk [Cortana Intelligence Galerisi](http://gallery.cortanaintelligence.com). Bu deneme açın, [Azure Machine Learning Studio](https://studio.azureml.net) çalışma.

> [!NOTE]
> Bu örnek ile birlikte sipariş toofollow içinde boş bir çalışma alanı yerine standart bir çalışma alanı toouse isteyebilirsiniz. Biz bir uç nokta - 10 uç noktaları - toplam her müşteri için oluşturursunuz ve boş bir çalışma alanı sınırlı too3 uç noktaları olduğundan, standart bir çalışma alanı gerektirir. Yalnızca bir ücretsiz çalışma alanı varsa, yalnızca hello betikleri tooallow yalnızca 3 konumları için aşağıda değiştirin.
> 
> 

Merhaba deneme kullanan bir **veri içeri aktarma** modülü tooimport hello eğitim veri kümesi *customer001.csv* bir Azure depolama hesabından. Biz tüm bisiklet kiralama konumlardan toplanan eğitim veri kümeleri ve bunları aynı blob depolama konumu dosya adları arasında değişen ile Merhaba depolanan varsayalım *rentalloc001.csv* çok*rentalloc10.csv* .

![Görüntü](./media/machine-learning-create-models-and-endpoints-with-powershell/reader-module.png)

Unutmayın bir **Web hizmeti çıkış** modülü toohello eklendi **Train Model** modülü.
Bu deneme bir web hizmeti olarak dağıtıldığında, o çıktıyla ilişkili hello endpoint hello eğitilen model hello .ilearner dosyası biçiminde döndürür.

Ayrıca bu hello hello URL'sini bir web hizmeti parametresini ayarlar olduğunu unutmayın **veri içeri aktarma** modülü kullanır. Bu bize toouse hello parametresi toospecify tek tek eğitim veri kümeleri tootrain hello modeli her konum için olanak sağlar.
Biz yapılan bu, bir SQL sorgusu verilerle bir web hizmeti parametresi tooget bir SQL Azure veritabanı veya yalnızca kullanarak gibi diğer yolları bir **Web hizmeti girişi** modülü toopass dataset toohello içinde web hizmeti.

![Görüntü](./media/machine-learning-create-models-and-endpoints-with-powershell/web-service-output.png)

Şimdi, hello varsayılan değerini kullanarak bu eğitim denemenizi Şimdi Çalıştır *rental001.csv* eğitim veri kümesi hello gibi. Merhaba hello çıktısını görüntülerseniz **değerlendir** Modülü (Merhaba çıkış tıklayın ve **Görselleştir**), biz alma, iyi bir performans görebilirsiniz *AUC* 0.91 =. Bu noktada, hazır toodeploy Bu eğitim denemenizi dışında bir web hizmeti olarak çalışıyoruz.

## <a name="deploy-hello-training-and-scoring-web-services"></a>Merhaba eğitim ve puanlama web hizmetlerini dağıtma
toodeploy hello web hizmeti, eğitim tıklatın hello **Web hizmetinin ayarı** hello deneme tuvalinin düğmesine tıklayın ve ardından **Web hizmeti Dağıt**. "" Bisiklet kiralama Eğitim". Bu web hizmeti çağrısı

Şimdi toodeploy hello Puanlama web hizmeti gerekir.
toodo Bu, biz tıklatabilirsiniz **Web hizmetinin ayarı** hello tuvale ve seçin **Tahmine dayalı Web hizmeti**. Bu bir Puanlama deneme oluşturur.
Biz toomake birkaç küçük ayarlamalar toomake giriş hello Etiket sütununda "cnt" Merhaba kaldırma ve hello çıktı tooonly hello örnek kimliği ve hello karşılık gelen sınırlama değeri tahmin gibi bir web hizmeti olarak çalışması gerekir.

toosave çalışma, kendiniz hello açabilirler [Tahmine dayalı denemeye](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Predicative-Experiment-1) hello zaten hazırlanır galeri içinde.

toodeploy hello web hizmeti Hello Tahmine dayalı denemeyi çalıştırın, ardından hello **Web hizmeti Dağıt** hello tuvale aşağıdaki düğmesine. Web hizmeti "Bisiklet kiralama Puanlama" Puanlama adı hello ".

## <a name="create-10-identical-web-service-endpoints-with-powershell"></a>PowerShell ile 10 aynı web hizmeti uç noktalarını oluşturma
Bu web Hizmeti'nin varsayılan uç noktası ile birlikte gelir. Ancak güncelleştirilemiyor bu yana hello varsayılan uç olarak ilgi değiliz. Ne ihtiyacımız toodo olan toocreate 10 ek uç noktalar, her konum için bir tane. Biz bu PowerShell ile gerçekleştirirsiniz.

İlk olarak, PowerShell ortamımızda ayarlayın:

    Import-Module .\AzureMLPS.dll
    # Assume hello default configuration file exists and is properly set toopoint toohello valid Workspace.
    $scoringSvc = Get-AmlWebService | where Name -eq 'Bike Rental Scoring'
    $trainingSvc = Get-AmlWebService | where Name -eq 'Bike Rental Training'

Ardından, hello aşağıdaki PowerShell komutunu çalıştırın:

    # Create 10 endpoints on hello scoring web service.
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        Write-Host ('adding endpoint ' + $endpointName + '...')
        Add-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -Description $endpointName     
    }

Şimdi 10 uç noktaları oluşturduk ve aynı eğitilen model eğitilmiş hello içerirler *customer001.csv*. Bunları hello Azure Yönetim Portalı görüntüleyebilirsiniz.

![Görüntü](./media/machine-learning-create-models-and-endpoints-with-powershell/created-endpoints.png)

## <a name="update-hello-endpoints-toouse-separate-training-datasets-using-powershell"></a>PowerShell kullanarak hello uç noktaları toouse ayrı eğitim veri kümelerini güncelleştirme
Merhaba sonraki tooupdate hello uç benzersiz olarak her müşterinin ayrı veri üzerinde eğitilmiş modeller ile adımdır. Ancak tooproduce hello Bu modellerden ilk ihtiyacımız **bisiklet kiralama eğitim** web hizmeti. Geri toohello edelim **bisiklet kiralama eğitim** web hizmeti. Kendi BES noktayla 10 kez sipariş tooproduce 10 farklı modelleri 10 farklı eğitim kümelerinde toocall ihtiyacımız var. Merhaba kullanacağız **InovkeAmlWebServiceBESEndpoint** PowerShell cmdlet toodo bu.

Blob depolama hesabınız için tooprovide kimlik bilgileri gerekir `$configContent`, yani, hello alanlarındaki `AccountName`, `AccountKey` ve `RelativeLocation`. Merhaba `AccountName` hello görüldüğü gibi hesap adlarını biri olabilir **Klasik Azure Yönetim Portalı** (*depolama* sekmesi). Bir depolama hesabında tıkladığınızda, `AccountKey` tuşuna basarak hello tarafından bulunabilir **erişim anahtarlarını Yönet** hello alt ve hello kopyalama düğmesini *birincil erişim anahtarını*. Merhaba `RelativeLocation` yeni bir model depolanacağı hello yolu göreli tooyour depolama değil. Örneği için hello yolu `hai/retrain/bike_rental/` adlı noktaları tooa kapsayıcı aşağıda hello betikteki `hai`, ve `/retrain/bike_rental/` alt klasörler. Şu anda, alt klasörler hello portalı kullanıcı Arabirimi üzerinden oluşturamaz, ancak vardır [birkaç Azure depolama gezginleri](../storage/common/storage-explorers.md) olanak tanıyacak şekilde toodo şekilde. Yeni bir kapsayıcı, depolama toostore hello yeni eğitilmiş modeller (.ilearner dosyaları) şu şekilde oluşturmanız önerilir: hello üzerinde depolama sayfanızdan tıklatın **Ekle** düğmesini hello altındaki ve adlandırın `retrain`. Özet olarak, hello gerekli değişiklikleri toohello aşağıdaki komut dosyası ilgilidir çok`AccountName`, `AccountKey` ve `RelativeLocation` (:`"retrain/model' + $seq + '.ilearner"`).

    # Invoke hello retraining API 10 times
    # This is hello default (and hello only) endpoint on hello training web service
    $trainingSvcEp = (Get-AmlWebServiceEndpoint -WebServiceId $trainingSvc.Id)[0];
    $submitJobRequestUrl = $trainingSvcEp.ApiLocation + '/jobs?api-version=2.0';
    $apiKey = $trainingSvcEp.PrimaryKey;
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $inputFileName = 'https://bostonmtc.blob.core.windows.net/hai/retrain/bike_rental/BikeRental' + $seq + '.csv';
        $configContent = '{ "GlobalParameters": { "URI": "' + $inputFileName + '" }, "Outputs": { "output1": { "ConnectionString": "DefaultEndpointsProtocol=https;AccountName=<myaccount>;AccountKey=<mykey>", "RelativeLocation": "hai/retrain/bike_rental/model' + $seq + '.ilearner" } } }';
        Write-Host ('training regression model on ' + $inputFileName + ' for rental location ' + $seq + '...');
        Invoke-AmlWebServiceBESEndpoint -JobConfigString $configContent -SubmitJobRequestUrl $submitJobRequestUrl -ApiKey $apiKey
    }

> [!NOTE]
> Merhaba BES endpoint hello modu bu işlem için yalnızca desteklenir. ' dir. RRS eğitilmiş modeller üretmek için kullanılamaz.
> 
> 

10 farklı BES iş yapılandırma json dosyalarını oluşturmak yerine, yukarıda gördüğünüz gibi biz dinamik olarak hello yapılandırma dizesi oluşturun ve toohello akış *jobConfigString* hello parametresinin  **InvokeAmlWebServceBESEndpoint** disk üzerinde bir kopyasını gerçekten gerek tookeep olduğundan cmdlet'i.

Her şey yolunda giderse, bir süre sonra 10 .ilearner dosyaları, gelen görmelisiniz *model001.ilearner* çok*model010.ilearner*, Azure depolama hesabınızdaki. Hazır tooupdate ki artık web Puanlama bizim 10 uç noktaları hello kullanarak bu modeller ile hizmet **düzeltme eki AmlWebServiceEndpoint** PowerShell cmdlet'i. Yeniden biz yalnızca hello varsayılan olmayan uç noktaları programlı olarak daha önce oluşturduğumuz düzeltme eki olduğunu unutmayın.

    # Patch hello 10 endpoints with respective .ilearner models
    $baseLoc = 'http://bostonmtc.blob.core.windows.net/'
    $sasToken = '<my_blob_sas_token>'
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        $relativeLoc = 'hai/retrain/bike_rental/model' + $seq + '.ilearner';
        Write-Host ('Patching endpoint ' + $endpointName + '...');
        Patch-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -ResourceName 'Bike Rental [trained model]' -BaseLocation $baseLoc -RelativeLocation $relativeLoc -SasBlobToken $sasToken
    }

Bu oldukça hızlı bir şekilde çalıştırmanız gerekir. Merhaba yürütme sona erdiğinde, başarılı bir şekilde 10 Tahmine dayalı web hizmeti uç noktaları, her biri benzersiz şekilde hello dataset belirli tooa kiralama konumdan, tüm tek eğitim denemenizi üzerinde eğitilmiş bir modeli içeren oluşturduk. tooverify bunu hello kullanarak bu uç noktalarını çağırma deneyebilirsiniz **InvokeAmlWebServiceRRSEndpoint** cmdlet, bunları sağlama hello ile aynı verileri girin ve hello modelleri olduğundan toosee farklı tahmin sonuçlarını beklemeniz gerekir farklı eğitim kümeleriyle eğitildi.

## <a name="full-powershell-script"></a>Tam PowerShell Betiği
Merhaba tam kaynak kodu hello listesi aşağıdadır:

    Import-Module .\AzureMLPS.dll
    # Assume hello default configuration file exists and properly set toopoint toohello valid workspace.
    $scoringSvc = Get-AmlWebService | where Name -eq 'Bike Rental Scoring'
    $trainingSvc = Get-AmlWebService | where Name -eq 'Bike Rental Training'

    # Create 10 endpoints on hello scoring web service
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        Write-Host ('adding endpoint ' + $endpontName + '...')
        Add-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -Description $endpointName     
    }

    # Invoke hello retraining API 10 times tooproduce 10 regression models in .ilearner format
    $trainingSvcEp = (Get-AmlWebServiceEndpoint -WebServiceId $trainingSvc.Id)[0];
    $submitJobRequestUrl = $trainingSvcEp.ApiLocation + '/jobs?api-version=2.0';
    $apiKey = $trainingSvcEp.PrimaryKey;
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $inputFileName = 'https://bostonmtc.blob.core.windows.net/hai/retrain/bike_rental/BikeRental' + $seq + '.csv';
        $configContent = '{ "GlobalParameters": { "URI": "' + $inputFileName + '" }, "Outputs": { "output1": { "ConnectionString": "DefaultEndpointsProtocol=https;AccountName=<myaccount>;AccountKey=<mykey>", "RelativeLocation": "hai/retrain/bike_rental/model' + $seq + '.ilearner" } } }';
        Write-Host ('training regression model on ' + $inputFileName + ' for rental location ' + $seq + '...');
        Invoke-AmlWebServiceBESEndpoint -JobConfigString $configContent -SubmitJobRequestUrl $submitJobRequestUrl -ApiKey $apiKey
    }

    # Patch hello 10 endpoints with respective .ilearner models
    $baseLoc = 'http://bostonmtc.blob.core.windows.net/'
    $sasToken = '?test'
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        $relativeLoc = 'hai/retrain/bike_rental/model' + $seq + '.ilearner';
        Write-Host ('Patching endpoint ' + $endpointName + '...');
        Patch-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -ResourceName 'Bike Rental [trained model]' -BaseLocation $baseLoc -RelativeLocation $relativeLoc -SasBlobToken $sasToken
    }
