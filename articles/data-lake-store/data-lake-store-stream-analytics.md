---
title: "Stream Analytics Data Lake Store içine aaaStream verilerden | Microsoft Docs"
description: "Azure Stream Analytics toostream verileri Azure Data Lake Store içinde kullanma"
services: data-lake-store,stream-analytics
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: edb58e0b-311f-44b0-a499-04d7e6c07a90
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 68c727d4807db0abe6efa90145d68c78902eb789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="stream-data-from-azure-storage-blob-into-data-lake-store-using-azure-stream-analytics"></a>Azure Akış Analizi’ni kullanarak Azure Depolama Blobundan Data Lake Store’a veri akışı gerçekleştirme
Bu makalede Azure Data Lake nasıl toouse depolamak için bir Azure akış analizi işi bir çıktı olarak öğreneceksiniz. Bu makale bir Azure Storage blobundan (giriş) verilerini okuyan basit bir senaryo gösterir ve veri tooData Lake deposu (çıktı) yazma hello.

> [!NOTE]
> Şu anda oluşturma ve Data Lake Store yapılandırmasını çıkaran Stream Analytics yalnızca hello desteklenen [Klasik Azure portalı](https://manage.windowsazure.com). Bu nedenle, bu öğreticinin bazı bölümleri hello Klasik Azure portalı kullanır.
>
>

## <a name="prerequisites"></a>Ön koşullar
Bu öğreticiye başlamadan önce hello şunlara sahip olmanız gerekir:

* **Bir Azure aboneliği**. Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/pricing/free-trial/).

* **Azure Depolama hesabı**. Bu hesap tooinput verilerden bir blob kapsayıcı için bir akış analizi işi kullanır. Bu öğretici için adlı bir depolama hesabı olduğunu varsayın **storageforasa** hello hesabı içindeki bir kapsayıcı adı verilen ve **storageforasacontainer**. Merhaba kapsayıcısı oluşturduktan sonra bir örnek veri dosyası tooit karşıya yükleyin. 
  
* **Azure Data Lake Store hesabı**. Merhaba yönergeleri izleyin [Azure Data Lake hello Azure Portal kullanarak Store ile çalışmaya başlama](data-lake-store-get-started-portal.md). Adlı bir Data Lake Store hesabı sahip varsayalım **asadatalakestore**. 

## <a name="create-a-stream-analytics-job"></a>Akış analizi işi oluşturma
Bir giriş kaynağı ve bir çıkış hedefini içeren bir akış analizi işi oluşturarak başlayın. Bu öğretici için hello kaynak bir Azure blob kapsayıcısı ve hello hedef Data Lake Store.

1. Toohello üzerinde oturum [Azure Portal](https://portal.azure.com).

2. Merhaba sol bölmeden tıklatın **akış analizi işleri**ve ardından **Ekle**.

    ![Stream Analytics işi oluşturmak](./media/data-lake-store-stream-analytics/create.job.png "Stream Analytics işi oluşturma")

    > [!NOTE]
    > Hello iş oluşturduğunuzdan emin olun veya hello depolama hesabı ile aynı bölgeye bölgeler arasında veri taşıma ek maliyet erişimliye.
    >

## <a name="create-a-blob-input-for-hello-job"></a>Bir Blob giriş hello işi için oluşturma

1. Merhaba sol bölmesinden hello Stream Analytics işi için açık hello sayfasını tıklatın hello **girişleri** sekmesini ve ardından **Ekle**.

    ![Bir giriş tooyour işi eklemek](./media/data-lake-store-stream-analytics/create.input.1.png "bir giriş tooyour işi ekleme")

2. Merhaba üzerinde **yeni giriş** dikey penceresinde hello aşağıdaki değerleri sağlayın.

    ![Bir giriş tooyour işi eklemek](./media/data-lake-store-stream-analytics/create.input.2.png "bir giriş tooyour işi ekleme")

    * İçin **giriş diğer adı**, hello iş giriş için benzersiz bir ad girin.
    * İçin **kaynak türünü**seçin **veri akışı**.
    * İçin **kaynak**seçin **Blob storage**.
    * İçin **abonelik**seçin **blob storage'ı geçerli aboneliğe ilişkin kullanma**.
    * İçin **depolama hesabı**, hello Önkoşullar bir parçası olarak, oluşturduğunuz hello depolama hesabını seçin. 
    * İçin **kapsayıcı**seçin hello oluşturulan hello kapsayıcı seçilen depolama hesabı.
    * İçin **olayı seri hale getirme biçimi**seçin **CSV**.
    * İçin **sınırlayıcı**seçin **sekmesini**.
    * İçin **kodlama**seçin **UTF-8**.

    **Oluştur**'a tıklayın. Merhaba portal şimdi hello giriş ekler ve hello bağlantı tooit sınar.


## <a name="create-a-data-lake-store-output-for-hello-job"></a>Bir Data Lake Store çıktı hello işi için oluşturma

1. Merhaba hello Stream Analytics işi hello sayfasını açın, **çıkışları** sekmesini ve ardından **Ekle**.

    ![Bir çıkış tooyour işi eklemek](./media/data-lake-store-stream-analytics/create.output.1.png "bir çıktı tooyour işi ekleme")

2. Merhaba üzerinde **yeni çıktı** dikey penceresinde hello aşağıdaki değerleri sağlayın.

    ![Bir çıkış tooyour işi eklemek](./media/data-lake-store-stream-analytics/create.output.2.png "bir çıktı tooyour işi ekleme")

    * İçin **çıkış diğer adları**, girin bir hello iş çıktısı için benzersiz bir ad. Bu sorguları toodirect hello sorgu çıktı toothis Data Lake Store kullanılan kolay bir addır.
    * İçin **havuzu**seçin **Data Lake Store**.
    * İstendiğinde tooauthorize olacaktır erişim tooData Lake Store hesabı. Tıklatın **yetkilendirmek**.

3. Hello üzerinde **yeni çıktı** dikey penceresinde değerleri aşağıdaki tooprovide hello devam edin.

    ![Bir çıkış tooyour işi eklemek](./media/data-lake-store-stream-analytics/create.output.3.png "bir çıktı tooyour işi ekleme")

    * İçin **hesap adı**, hello Data Lake Store hesabını önceden oluşturulmuş hello proje çıktı toobe gönderilmesini istediğiniz yeri seçin.
    * İçin **yol önek deseni**, bir dosya yolu kullanılan toowrite girin dosyalarınızı hello içinde belirtilen Data Lake Store hesabı.
    * İçin **tarih biçimi**, hello önek yolunda bir tarih belirteci kullandıysanız, dosyalarınızı düzenlenir hello tarih biçimi seçebilirsiniz.
    * İçin **saat biçimi**, bir zaman belirteci hello önek yolunda kullandıysanız, dosyalarınızı düzenlenir hello saat biçimini belirtin.
    * İçin **olayı seri hale getirme biçimi**seçin **CSV**.
    * İçin **sınırlayıcı**seçin **sekmesini**.
    * İçin **kodlama**seçin **UTF-8**.
    
    **Oluştur**'a tıklayın. Merhaba portal şimdi hello çıktı ekler ve hello bağlantı tooit sınar.
    
## <a name="run-hello-stream-analytics-job"></a>Merhaba Stream Analytics işini çalıştır

1. toorun Stream Analytics işi, bir sorgu hello çalıştırmalısınız **sorgu** sekmesi. Bu öğretici için değiştirerek hello örnek sorgu çalıştırabilirsiniz hello hello yer tutucularını iş giriş ve çıkış diğer adları, aşağıdaki hello ekran görüntüsünde gösterildiği gibi.

    ![Sorguyu çalıştırmak](./media/data-lake-store-stream-analytics/run.query.png "sorgusu çalıştırma")

2. Tıklatın **kaydetmek** hello ekranın hello ve ardından hello **genel bakış** sekmesini tıklatın, **Başlat**. Merhaba iletişim kutusundan **özel zaman**ve geçerli tarih ve saat hello ayarlayın.

    ![İş saati ayarlayın](./media/data-lake-store-stream-analytics/run.query.2.png "iş saati ayarlayın")

    Tıklatın **Başlat** toostart hello işi. Tooa birkaç dakika toostart hello işi alabilir.

3. tootrigger hello iş toopick hello verilerden hello blob kopyalama bir örnek veri dosyası toohello blob kapsayıcısı. Örnek veri dosyası hello alabilirsiniz [Azure Data Lake Git deposu](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt). Bu öğretici için şimdi hello dosya kopyalama **vehicle1_09142014.csv**. Çeşitli istemciler gibi kullanabilir [Azure Storage Gezgini](http://storageexplorer.com/), tooupload veri tooa blob kapsayıcısı.

4. Merhaba gelen **genel bakış** sekmesinde, altında **izleme**, hello verileri nasıl işlendiği bakın.

    ![İzleyici işi](./media/data-lake-store-stream-analytics/run.query.3.png "İzleyici işi")

5. Son olarak, hello proje çıktı verilerini hello Data Lake Store hesabında kullanılabilir olup olmadığını doğrulayabilirsiniz. 

    ![Doğrulama çıktı](./media/data-lake-store-stream-analytics/run.query.4.png "çıkış doğrulayın")

    Merhaba Veri Gezgini bölmesinde, o hello çıktı yazılı tooa klasör yolu olarak belirtilen hello Data Lake Store çıktı ayarları dikkat edin (`streamanalytics/job/output/{date}/{time}`).  

## <a name="see-also"></a>Ayrıca bkz.
* [Hdınsight küme toouse Data Lake Store oluşturma](data-lake-store-hdinsight-hadoop-use-portal.md)
