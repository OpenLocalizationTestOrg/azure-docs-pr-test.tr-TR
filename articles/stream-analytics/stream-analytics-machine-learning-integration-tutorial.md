---
title: "aaaAzure akış analizi ve makine öğrenme tümleştirme | Microsoft Docs"
description: "Nasıl toouse bir kullanıcı tanımlı işlev ve Machine Learning Stream Analytics işi"
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: cfced01f-ccaa-4bc6-81e2-c03d1470a7a2
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 07/06/2017
ms.author: jeffstok
ms.openlocfilehash: e1ba7ab51ece80719839793e1320a7666cfc4181
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="performing-sentiment-analysis-by-using-azure-stream-analytics-and-azure-machine-learning"></a>Azure akış analizi ve Azure Machine Learning kullanarak düşünceleri analiz gerçekleştirme
Bu makalede, Azure Machine Learning tümleştiren basit bir Azure akış analizi işi tooquickly nasıl ayarlamak açıklanmaktadır. Gerçek zamanlı hello düşünceleri puan belirlemek ve hello metin veri akışı Cortana Intelligence Galerisi tooanalyze Machine Learning düşünceleri analytics modelden kullanın. Merhaba Cortana Intelligence Suite kullanarak düşünceleri analiz modeli oluşturmanın hello ayrıntılı olarak incelenmektedir hakkında endişelenmeden bu görevi gerçekleştirirken olanak sağlar.

Bu makale tooscenarios bunlar gibi gelen öğrenin uygulayabilirsiniz:

* Twitter veri akışı üzerinde gerçek zamanlı düşünceleri çözümleniyor.
* Müşteri kayıtlarını çözümleme destek personeli ile sohbetleri.
* Forum, bloglar ve videolar açıklamaları değerlendiriliyor. 
* Birçok diğer gerçek zamanlı, Tahmine dayalı Puanlama senaryoları.

Gerçek dünya senaryoda hello verileri doğrudan bir Twitter veri akışından alın. Böylece Hello akış analizi işi tweet'leri Azure Blob Depolama alanında bir CSV dosyasından alır toosimplify hello öğretici, biz yazdıktan. Kendi CSV dosyası oluşturabilirsiniz veya görüntü aşağıdaki hello gösterildiği örnek bir CSV dosyası kullanabilirsiniz:

![bir CSV dosyasında örnek tweet'leri](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-2.png)  

oluşturduğunuz hello akış analizi işi hello düşünceleri analiz modeli kullanıcı tanımlı işlevi (UDF) hello blob Mağazası'ndan hello örnek metin verilere uygular. Merhaba çıkış (Merhaba düşünceleri analiz sonucunu hello) toohello yazılmış aynı blob Mağazası'nda farklı bir CSV dosyası. 

Merhaba aşağıdaki şekilde bu yapılandırma gösterilmektedir. Belirtilenler daha gerçekçi bir senaryo için blob depolama Twitter verilerini Azure Event Hubs'a giriş akış ile değiştirebilirsiniz. Ayrıca, oluşturacağınız bir [Microsoft Power BI](https://powerbi.microsoft.com/) gerçek zamanlı görsel olarak hello toplama düşünceleri.    

![Stream Analytics Machine Learning tümleştirmesine genel bakış](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-1.png)  

## <a name="prerequisites"></a>Ön koşullar
Başlamadan önce hello aşağıdaki sahip olduğunuzdan emin olun:

* Etkin bir Azure aboneliği.
* Bazı veriler içeren bir CSV dosyası. Öğesinden daha önce gösterilen hello dosyayı indirebilirsiniz [GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/sampleinput.csv), ya da kendi dosyası oluşturabilirsiniz. Bu makale için GitHub hello dosyasından kullandığınız varsayalım.

Yüksek düzeyde, bu makalede, toocomplete hello görevleri gösterilen, aşağıdaki hello:

1. Bir Azure depolama hesabı ve blob depolama kapsayıcısını oluşturun ve CSV biçimlendirilmiş giriş dosyası toohello kapsayıcı yükleyin.
3. Hello Cortana Intelligence Galerisi tooyour Azure Machine Learning çalışma alanından düşünceleri analiz modeli ekleyin ve bu model hello Machine Learning çalışma alanında bir web hizmeti olarak dağıtabilirsiniz.
5. Bu web hizmeti olarak sipariş toodetermine düşünceleri işlevinde hello metin girişi için çağıran Stream Analytics işi oluşturun.
6. Merhaba Stream Analytics işini başlatmak ve hello çıktısını denetleyin.

## <a name="create-a-storage-container-and-upload-hello-csv-input-file"></a>Depolama kapsayıcısı oluşturmak ve hello CSV giriş dosyasını karşıya yükle
Bu adım için Github'da kullanılabilir bir hello gibi herhangi bir CSV dosyası kullanabilirsiniz.

1. Hello Azure portal'ı tıklatın **yeni** &gt; **depolama** &gt; **depolama hesabı**.

   ![Yeni depolama hesabı oluştur](./media/stream-analytics-machine-learning-integration-tutorial/azure-portal-create-storage-account.png)

2. Bir ad sağlayın (`samldemo` hello örnekte). Merhaba adı yalnızca küçük harfler ve sayılar kullanabilirsiniz ve Azure arasında benzersiz olması gerekir. 

3. Varolan bir kaynak grubu belirtin ve bir konum belirtin. Konum için Bu öğretici kullanımda oluşturulan tüm hello kaynaklar aynı hello olan öneririz konumu.

    ![Depolama hesabı ayrıntılarını sağlayın](./media/stream-analytics-machine-learning-integration-tutorial/create-sa1.png)

4. Hello Azure portal, hello depolama hesabı seçin. Merhaba depolama hesabı dikey penceresinde tıklayın **kapsayıcıları** ve ardından  **+ &nbsp;kapsayıcı** toocreate blob depolama.

    ![BLOB kapsayıcı oluşturun](./media/stream-analytics-machine-learning-integration-tutorial/create-sa2.png)

5. Merhaba kapsayıcı için bir ad (`azuresamldemoblob` hello örnekte) doğrulayın **erişim türüne** çok ayarlanır**Blob**. İşiniz bittiğinde, **Tamam**’a tıklayın.

    ![BLOB kapsayıcı ayrıntıları belirtin](./media/stream-analytics-machine-learning-integration-tutorial/create-sa3.png)

6. Merhaba, **kapsayıcıları** dikey penceresinde, bu kapsayıcı için hello dikey pencere açılır select hello yeni kapsayıcı.

7. **Karşıya Yükle**'ye tıklayın.

    ![Bir kapsayıcı 'Karşıya' düğmesi](./media/stream-analytics-machine-learning-integration-tutorial/create-sa-upload-button.png)

8. Merhaba, **karşıya yükleme blob** dikey penceresinde hello CSV dosyası Bu öğretici için toouse istediğinizi belirtin. İçin **Blob türü**seçin **blok blobu** ve kümesi hello blok Bu öğretici için yeterliyse too4 MB cinsinden boyutu.

    ![BLOB dosya karşıya yükleme](./media/stream-analytics-machine-learning-integration-tutorial/create-sa4.png)

9. Merhaba tıklatın **karşıya** hello dikey penceresinde hello sonundaki düğmesi.

## <a name="add-hello-sentiment-analytics-model-from-hello-cortana-intelligence-gallery"></a>Cortana Intelligence Galerisi hello Hello düşünceleri analiz modeli ekleme

Bir blob'a Hello örnek veriler değil, hello düşünceleri çözümleme modeli Cortana Intelligence Galerisi'nde etkinleştirebilirsiniz.

1. Toohello Git [Tahmine dayalı düşünceleri analiz modeli](https://gallery.cortanaintelligence.com/Experiment/Predictive-Mini-Twitter-sentiment-analysis-Experiment-1) hello Cortana Intelligence Galerisi sayfasında.  

2. Tıklatın **Studio'da Aç**.  
   
   ![Stream Analytics Machine Learning, açık Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-open-ml-studio.png)  

3. Toogo toohello çalışma alanını açın. Bir konum seçin.

4. Tıklatın **çalıştırmak** hello sayfanın hello sonundaki. Merhaba işlem çalışır ve hangi yaklaşık bir dakika sürer.

   ![denemeyi Machine Learning Studio'da çalıştırın](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-run-experiment.png)  

5. Merhaba işlem başarıyla çalıştırıldıktan sonra seçin **Web hizmeti Dağıt** hello sayfanın hello sonundaki.

   ![denemeyi Machine Learning Studio'da bir web hizmeti olarak dağıtma](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-deploy-web-service.png)  

6. analytics modeldir hazır toouse düşünceleri hello toovalidate tıklatın hello **Test** düğmesi. Metin "ı Microsoft memnuniyet"gibi giriş sağlar. 

   ![Machine Learning Studio'da Test deneme](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test.png)  

    Merhaba test çalışırsa, örnek izleyen bir sonuç benzer toohello bakın:

   ![Machine Learning Studio'da test sonuçları](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test-results.png)  

7. Merhaba, **uygulamaları** sütun hello tıklatın **Excel 2010 veya önceki çalışma kitabı** bağlantı toodownload bir Excel çalışma kitabı. Merhaba çalışma kitabı hello bir API anahtarı ve hello Stream Analytics işi daha sonra tooset gerektiğini hello URL içerir.

    ![Stream Analytics Machine Learning, Hızlı Bakış](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-quick-glance.png)  


## <a name="create-a-stream-analytics-job-that-uses-hello-machine-learning-model"></a>Merhaba Machine Learning modelini kullanan bir Stream Analytics işi oluşturma

Artık blob storage'da hello CSV dosyasından hello örnek tweet'leri okuyan akış analizi işi oluşturabilirsiniz. 

### <a name="create-hello-job"></a>Merhaba işi oluşturma

1. Toohello Git [Azure portal](https://portal.azure.com).  

2. Tıklatın **yeni** > **nesnelerin interneti** > **Stream Analytics işi**. 

   ![Tooa yeni akış analizi işi almak için azure portal yolu](./media/stream-analytics-machine-learning-integration-tutorial/azure-portal-new-iot-sa-job.png)
   
3. Ad hello iş `azure-sa-ml-demo`bir abonelik belirtin, varolan bir kaynak grubu belirtin veya yeni bir tane oluşturun ve hello işi için başlangıç konumu seçin.

   ![Yeni akış analizi işi için ayarları belirtin](./media/stream-analytics-machine-learning-integration-tutorial/create-job-1.png)
   

### <a name="configure-hello-job-input"></a>Merhaba iş giriş yapılandırın
Merhaba iş kendi giriş önceki tooblob depolama karşıya hello CSV dosyasından alır.

1. Merhaba işi, altında oluşturulduktan sonra **iş topoloji** hello iş dikey penceresinde hello tıklayın **girişleri** kutusu.  
   
   ![Akış analizi işi dikey penceresinde 'Girişleri' kutusu](./media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input.png)  

2. Merhaba, **girişleri** dikey penceresinde tıklatın **+ Ekle**.

   !['Bir giriş toohello Stream Analytics işi ekleme düğmesi ekleme'](./media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input-button.png)  

3. Merhaba dolgu **yeni giriş** dikey penceresinde bu değerleri içeren:

    * **Giriş diğer adı**: hello adını kullan `datainput`.
    * **Kaynak türünü**: seçin **veri akışı**.
    * **Kaynak**: seçin **Blob storage**.
    * **Alma seçeneği**: seçin **blob storage'ı geçerli aboneliğe ilişkin kullanma**. 
    * **Depolama hesabı**. Daha önce oluşturduğunuz hello depolama hesabı seçin.
    * **Kapsayıcı**. Daha önce oluşturduğunuz select hello kapsayıcı (`azuresamldemoblob`).
    * **Olayı seri hale getirme biçimi**. Seçin **CSV**.

    ![Yeni iş girişi için ayarlar](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-create-sa-input-new-portal.png)

4. **Oluştur**'a tıklayın.

### <a name="configure-hello-job-output"></a>Merhaba iş çıktısı yapılandırın
Merhaba işi gönderir sonuçları toohello aynı blob depolama burada giriş. 

1. Altında **iş topoloji** hello iş dikey penceresinde hello tıklayın **çıkışları** kutusu.  
  
   ![Akış analizi işi için yeni çıkış oluşturma](./media/stream-analytics-machine-learning-integration-tutorial/create-output.png)  

2. Merhaba, **çıkışları** dikey penceresinde tıklatın **+ Ekle**ve hello diğer ada sahip bir çıkış ekleyin `datamloutput`. 

3. İçin **havuzu**seçin **Blob storage**. Merhaba hello kalanını doldurun hello blob depolama girdisi için kullandığınız aynı değerleri kullanarak ayarlarını hello çıktı:

    * **Depolama hesabı**. Daha önce oluşturduğunuz hello depolama hesabı seçin.
    * **Kapsayıcı**. Daha önce oluşturduğunuz select hello kapsayıcı (`azuresamldemoblob`).
    * **Olayı seri hale getirme biçimi**. Seçin **CSV**.

   ![Yeni iş çıktısı için ayarları](./media/stream-analytics-machine-learning-integration-tutorial/create-output2.png) 

4. **Oluştur**'a tıklayın.   


### <a name="add-hello-machine-learning-function"></a>Add Hello Machine Learning işlevi 
Daha önce bir Machine Learning modeli tooa web hizmeti yayımladı. Merhaba akış analizi işi çalıştırıldığında Senaryomuzda her örnek tweet hello giriş toohello web hizmetinden düşünceleri çözümleme için gönderir. Merhaba Machine Learning web hizmeti bir düşünceleri döndürür (`positive`, `neutral`, veya `negative`) ve hello tweet pozitif olması olasılığını. 

Merhaba öğreticinin bu bölümünde hello akış analizi işi işlevinde tanımlayın. Merhaba işlevi bir tweet toohello web hizmeti çağrılan toosend olması ve hello yanıt geri alın. 

1. Daha önce hello Excel çalışma kitabında indirdiğiniz hello web hizmeti URL'sini ve API anahtarını olduğundan emin olun.

2. Toohello iş genel bakış dikey penceresine dönün.

3. Altında **ayarları**seçin **işlevleri** ve ardından **+ Ekle**.

   ![Bir işlev toohello Stream Analytics işi ekleme](./media/stream-analytics-machine-learning-integration-tutorial/create-function1.png) 

4. Girin `sentiment` hello işlev alias ve bu değerleri kullanarak hello dikey penceresinde hello kalan doldurun:

    * **İşlev türü**: seçin **Azure ML**.
    * **Alma seçeneği**: seçin **farklı bir abonelik alma**. Bu, bir fırsat tooenter hello URL'si ve anahtar sağlar.
    * **URL**: hello web hizmeti URL'sini yapıştırın.
    * **Anahtar**: hello API anahtarını yapıştırın.
  
    ![Machine Learning işlevi toohello akış analizi işi eklemek için ayarlar](./media/stream-analytics-machine-learning-integration-tutorial/add-function.png)  
    
5. **Oluştur**'a tıklayın.

### <a name="create-a-query-tootransform-hello-data"></a>Bir sorgu tootransform hello verileri oluşturma

Akış analizi sorgu bildirim temelli, SQL tabanlı tooexamine hello giriş kullanır ve işleme. Bu bölümde, her tweet girişten okuyan ve hello Machine Learning işlevi tooperform düşünceleri analiz çağıran bir sorgu oluşturun. Merhaba sorgu daha sonra hello sonuç toohello (blob depolama) tanımlanan çıkış gönderir.

1. Toohello iş genel bakış dikey penceresine dönün.

2.  Altında **iş topoloji**, hello tıklatın **sorgu** kutusu.

    ![Akış analizi işi için bir sorgu oluşturun](./media/stream-analytics-machine-learning-integration-tutorial/create-query.png)  

3. Sorgu aşağıdaki hello girin:

    ```
    WITH sentiment AS (  
    SELECT text, sentiment(text) as result from datainput  
    )  

    Select text, result.[Score]  
    Into datamloutput
    From sentiment  
    ```    

    Merhaba sorgu daha önce oluşturduğunuz hello işlevi çağırır (`sentiment`) sipariş tooperform düşünceleri analizi hello girişte her tweet üzerinde. 

4. Tıklatın **kaydetmek** toosave hello sorgu.


## <a name="start-hello-stream-analytics-job-and-check-hello-output"></a>Merhaba Stream Analytics işini başlatmak ve hello çıktısını denetleyin

Şimdi hello Stream Analytics işi başlatabilirsiniz.

### <a name="start-hello-job"></a>Merhaba işi Başlat
1. Toohello iş genel bakış dikey penceresine dönün.

2. Tıklatın **Başlat** hello dikey penceresinde hello üstünde.

    ![Akış analizi işi için bir sorgu oluşturun](./media/stream-analytics-machine-learning-integration-tutorial/start-job.png)  

3. Merhaba, **başlangıç işi**seçin **özel**ve ardından bir gün önceki toowhen hello CSV dosyası tooblob depolama karşıya seçin. İşiniz bittiğinde tıklatın **Başlat**.  


### <a name="check-hello-output"></a>Merhaba çıktısını denetleyin
1. Merhaba etkinliğinde görene kadar birkaç dakika let hello iş **izleme** kutusu. 

2. Normalde tooexamine Merhaba içeriğine blob depolama kullanan bir aracı varsa, bu aracı tooexamine hello kullanın `azuresamldemoblob` kapsayıcı. Alternatif olarak, aşağıdaki adımları hello Azure portal'ın hello:

    1. Merhaba Hello Portalı'nda bulmak `samldemo` depolama hesabı ve hello hesabında hello bulur `azuresamldemoblob` kapsayıcı. Merhaba kapsayıcısında iki dosya bkz: Merhaba hello örnek tweet'leri içeren dosya ve hello akış analizi işi tarafından oluşturulan bir CSV dosyası.
    2. Oluşturulan hello dosyasını sağ tıklatın ve ardından **karşıdan**. 

   ![Blob depolama alanından CSV iş çıktısı indirme](./media/stream-analytics-machine-learning-integration-tutorial/download-output-csv-file.png)  

3. Açık hello CSV dosyası oluşturulur. Aşağıdaki örneğine hello gibi bir şey görürsünüz:  
   
   ![Stream Analytics Machine Learning, CSV görünümü](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-csv-view.png)  


### <a name="view-metrics"></a>Metrikleri görüntüleyin
Azure Machine Learning işlevi ödemeyle ilgili ölçümlerini de görüntüleyebilirsiniz. işlevi ile ilgili ölçümleri aşağıdaki hello hello görüntülenen **izleme** hello iş dikey penceresinde kutusunda:

* **İşlev istekleri** gönderilen istekleri tooa Machine Learning web hizmeti hello sayısını gösterir.  
* **İşlev olayları** hello olayları hello isteği sayısını gösterir. Varsayılan olarak, her isteği tooa Machine Learning web hizmeti too1, 000 olaylarını içerir.  


## <a name="next-steps"></a>Sonraki adımlar

* [Giriş tooAzure akış analizi](stream-analytics-introduction.md)
* [Azure Akış Analizi Sorgu Dili Başvurusu](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [REST API tümleştirme ve makine öğrenme](stream-analytics-how-to-configure-azure-machine-learning-endpoints-in-stream-analytics.md)
* [Azure Akış Analizi Yönetimi REST API'si Başvurusu](https://msdn.microsoft.com/library/azure/dn835031.aspx)



