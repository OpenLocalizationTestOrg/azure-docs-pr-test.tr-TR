---
title: "aaaUse hello Azure portal toocreate Azure Hdınsight kümeleri Data Lake Store ile | Microsoft Docs"
description: "Hello Azure portal toocreate kullanın ve Hdınsight kümeleri Azure Data Lake Store ile kullanma"
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: a8c45a83-a8e3-4227-8b02-1bc1e1de6767
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/14/2017
ms.author: nitinme
ms.openlocfilehash: f23113d444a3c5a01894dba29f75f3621b2d16bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-hdinsight-clusters-with-data-lake-store-by-using-hello-azure-portal"></a>Hello Azure portal kullanarak Data Lake Store ile Hdınsight kümeleri oluşturma
> [!div class="op_single_selector"]
> * [Hello Azure portalını kullanın](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [(Varsayılan depolama için) PowerShell kullanma](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [PowerShell (için ek depolama alanı) kullanın](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [Kaynak Yöneticisi'ni kullanın](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

Nasıl toouse hello Azure portal toocreate bir Azure Data Lake Store hesabı olan bir Hdınsight kümesi hello varsayılan depolama veya ek depolama alanı olarak öğrenin. Ek depolama alanı bir Hdınsight kümesi için isteğe bağlı olsa da, olan iş verilerinizi hello ek depolama hesapları toostore önerilir.

## <a name="prerequisites"></a>Ön koşullar
Bu öğreticiye başlamadan önce gereksinimleri aşağıdaki hello karşılamanızın emin olun:

* **Bir Azure aboneliği**. Çok Git[alma Azure ücretsiz deneme sürümü](https://azure.microsoft.com/pricing/free-trial/).
* **Bir Azure Data Lake Store hesabı**. Merhaba yönergeleri uygulayın [hello Azure portal kullanarak Azure Data Lake Store ile çalışmaya başlama](data-lake-store-get-started-portal.md). Ayrıca kök klasör hello hesabı oluşturmanız gerekir.  Bu öğreticide, bir kök klasör adında __/kümeleri__ kullanılır.
* **Bir Azure Active Directory hizmet asıl**. Bu öğretici hakkında yönergeler sağlar toocreate Azure Active Directory'de (Azure AD) bir hizmet sorumlusu. Ancak, bir hizmet sorumlusu toocreate olmalıdır Azure AD yönetici. Bir yöneticiyseniz, bu önkoşulu atlayın ve hello eğitici devam edin.

    >[!NOTE]
    >Yalnızca, Azure AD yöneticisiyseniz, bir hizmet asıl oluşturabilirsiniz. Azure AD yöneticinizin Data Lake Store ile Hdınsight kümesi oluşturmadan önce bir hizmet asıl oluşturmanız gerekir. Ayrıca, hello hizmet sorumlusu bir sertifikayla konusunda açıklandığı gibi oluşturulmalıdır [sertifikayla bir hizmet sorumlusu oluşturma](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate).
    >

## <a name="create-an-hdinsight-cluster"></a>Hdınsight kümesi oluşturma

Bu bölümde, Data Lake Store hesapları hello varsayılan veya hello ek depolama alanı olarak ile bir Hdınsight kümesi oluşturun. Bu makalede yalnızca Data Lake Store hesaplarını yapılandırma hello parçası odaklanır.  Merhaba genel küme oluşturma bilgiler ve yordamlar için bkz: [Hdınsight'ta oluşturmak Hadoop kümeleri](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md).

### <a name="create-a-cluster-with-data-lake-store-as-default-storage"></a>Data Lake Store ile varsayılan depolama alanı olarak bir küme oluşturma

**toocreate bir Hdınsight kümesini Data Lake Store ile Merhaba varsayılan depolama hesabı olarak**

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. İzleyin [küme oluşturma](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md#create-clusters) hello Hdınsight kümeleri oluşturma hakkında genel bilgi için.
3. Merhaba üzerinde **depolama** dikey altında **birincil depolama türü**seçin **Data Lake Store**ve ardından aşağıdaki bilgilerle hello girin:

    ![Ekle hizmet asıl tooHDInsight küme](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.1.adls.storage.png "Ekle hizmet asıl tooHDInsight küme")

    - **Select Data Lake Store hesabı**: mevcut bir Data Lake Store hesabını seçin. Mevcut bir Data Lake Store hesabı gereklidir.  Bkz: [Önkoşullar](#prereuisites).
    - **Kök yolu**: hello kümeye özgü dosyaları depolanan toobe olduğu bir yol girin. Merhaba ekran olduğu __/ / myhdiadlcluster/kümeleri__, hangi hello içinde __/kümeleri__ klasör var olmalıdır ve hello Portal oluşturur *myhdicluster* klasör.  Merhaba *myhdicluster* hello küme adıdır.
    - **Data Lake Store erişim**: hello Data Lake Store hesabı ve Hdınsight kümesi arasında erişim yapılandırın. Yönergeler için bkz: [yapılandırma Data Lake Store erişim](#configure-data-lake-store-access).
    - **Ek depolama hesapları**: hesapları hello küme için ek depolama alanı olarak Azure Storage hesapları ekleyin. tooadd ek veri Gölü depoları hello küme izinleri daha fazla Data Lake Store hesapları veriler üzerinde bir Data Lake Store hesabı hello birincil depolama türü olarak yapılandırılırken verilerek yapılır. Bkz. [Data Lake Store erişimini yapılandırma](#configure-data-lake-store-access).

4. Merhaba üzerinde **Data Lake Store erişim**, tıklatın **seçin**ve açıklandığı gibi küme oluşturma ile devam et [Hdınsight'ta oluşturmak Hadoop kümeleri](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md).


### <a name="create-a-cluster-with-data-lake-store-as-additional-storage"></a>Data Lake Store ile ek depolama alanı olarak bir küme oluşturma

Merhaba aşağıdaki yönergeleri bir Hdınsight kümesi ile Merhaba varsayılan depolama alanı olarak Azure Storage hesabı ve ek depolama alanı olarak Data Lake Store hesabı oluşturun.
**toocreate bir Hdınsight kümesini Data Lake Store ile Merhaba varsayılan depolama hesabı olarak**

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. İzleyin [küme oluşturma](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md#create-clusters) hello Hdınsight kümeleri oluşturma hakkında genel bilgi için.
3. Merhaba üzerinde **depolama** dikey altında **birincil depolama türü**seçin **Azure Storage**ve ardından aşağıdaki bilgilerle hello girin:

    ![Ekle hizmet asıl tooHDInsight küme](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.1.png "Ekle hizmet asıl tooHDInsight küme")

    - **Seçim yöntemini**: seçenekleri aşağıdaki hello birini kullanın:

        * toospecify, Azure aboneliğinizin bir parçası olan bir depolama hesabını seçin **My abonelikleri**ve ardından hello depolama hesabını seçin.
        * Azure aboneliğiniz dışında select bir depolama hesabı toospecify **erişim tuşu**ve ardından depolama hesabı dışında hello hello bilgiler sağlar.

    - **Varsayılan kapsayıcı**: her iki hello varsayılan değeri kullanın veya kendi adı belirtin.

    - Ek depolama hesapları: hello ek depolama alanı olarak daha fazla Azure Storage hesaplarını ekleyin.
    - Data Lake Store erişim: hello Data Lake Store hesabı ve Hdınsight kümesi arasında erişim yapılandırın. Yönergeler için bkz [yapılandırma Data Lake Store erişim](#configure-data-lake-store-access).

## <a name="configure-data-lake-store-access"></a>Data Lake Store erişimi yapılandırma 

Bu bölümde, bir Azure Active Directory hizmet asıl kullanarak Hdınsight kümelerini Data Lake Store erişimden yapılandırın. 

### <a name="specify-a-service-principal"></a>Bir hizmet sorumlusu belirtin

Hello Azure portal, mevcut bir hizmet sorumlusu kullanabilir veya yeni bir tane oluşturun.

**toocreate hello Azure Portalı'ndan bir hizmet sorumlusu**

1. Tıklatın **Data Lake Store erişim** hello Store dikey penceresinden.
2. Merhaba üzerinde **Data Lake Store erişim** dikey penceresinde tıklatın **Yeni Oluştur**.
3. Tıklatın **hizmet sorumlusu**ve ardından hello yönergeleri toocreate bir hizmet sorumlusu izleyin.
4. Toouse karar verirseniz hello sertifikayı indirin yeniden hello gelecekteki içinde. İndirme hello sertifika toouse hello isterseniz ek Hdınsight kümeleri oluşturduğunuzda aynı asıl hizmet yararlıdır.

    ![Ekle hizmet asıl tooHDInsight küme](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.2.png "Ekle hizmet asıl tooHDInsight küme")

4. Tıklatın **erişim** tooconfigure hello klasör erişimi.  Bkz: [dosya izinlerini yapılandırın](#configure-file-permissions).


**toouse var olan bir hizmet hello Azure portal ' sorumlusu**

1. Tıklatın **Data Lake Store erişim**.
1. Merhaba üzerinde **Data Lake Store erişim** dikey penceresinde tıklatın **var olanı kullan**.
2. Tıklatın **hizmet sorumlusu**ve ardından bir hizmet sorumlusu seçin. 
3. Seçilen hizmet sorumlusuyla ilişkili hello sertifika (.pfx dosyası) karşıya yükleyin ve hello sertifikanın parolasını girin.

    ![Ekle hizmet asıl tooHDInsight küme](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.5.png "Ekle hizmet asıl tooHDInsight küme")

4. Tıklatın **erişim** tooconfigure hello klasör erişimi.  Bkz: [dosya izinlerini yapılandırın](#configure-file-permissions).


### <a name="configure-file-permissions"></a>Dosya izinleri yapılandırma

Merhaba yapılandırır hello hesabı hello varsayılan depolama veya ek depolama alanı hesabı olarak kullanılan bağlı olarak farklı olur:

- Varsayılan depolama alanı olarak kullanılan

    - Merhaba kök düzeyinde hello Data Lake Store hesabı izni
    - Merhaba kök düzeyinde hello Hdınsight küme depolama izni. Örneğin, hello __/kümeleri__ hello öğreticide daha önce kullanılan klasör.
- Ek depolama alanı kullanın

    - Burada erişim dosya hello klasörleri izni.

**Merhaba Data Lake Store hesap kök düzeyinde tooassign izni**

1. Merhaba üzerinde **Data Lake Store erişim** dikey penceresinde tıklatın **erişim**. Merhaba **dosya izinlerini seçin** dikey penceresi açılır. Aboneliğinizdeki tüm hello Data Lake Store hesaplarını listeler.
2. Getirin (tıklamayın) hello fare hello toomake hello onay kutusunu görünür, onay kutusunu seçin hello sonra Data Lake Store hesabı hello adını üzerinden.

    ![Ekle hizmet asıl tooHDInsight küme](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.3.png "Ekle hizmet asıl tooHDInsight küme")

  Varsayılan olarak, __okuma__, __yazma__, ve __yürütme__ hepsi seçilidir.

3. Tıklatın **seçin** hello sayfanın hello üzerinde.
4. Tıklatın **çalıştırmak** tooassign izni.
5. **Bitti**’ye tıklayın.

**Merhaba Hdınsight küme kök düzeyinde tooassign izni**

1. Merhaba üzerinde **Data Lake Store erişim** dikey penceresinde tıklatın **erişim**. Merhaba **dosya izinlerini seçin** dikey penceresi açılır. Aboneliğinizdeki tüm hello Data Lake Store hesaplarını listeler.
1. Merhaba gelen **dosya izinlerini seçin** dikey penceresinde hello Data Lake Store adı tooshow içeriği'ı tıklatın.
2. Merhaba Hdınsight küme depolama kök hello klasörünün hello soldaki hello onay kutusunu işaretleyerek seçin. Toohello ekran görüntüsü önceki göre hello küme depolama köküdür __/kümeleri__ varsayılan depolama alanı olarak hello Data Lake Store seçerken belirtilen klasör.
3. Merhaba, hello klasörde izinler.  Varsayılan olarak, okuma, yazma ve yürütme hepsi seçilidir.
4. Tıklatın **seçin** hello sayfanın hello üzerinde.
5. **Çalıştır**’a tıklayın.
6. **Bitti**’ye tıklayın.

Data Lake Store ek depolama alanı olarak kullanıyorsanız, tooaccess hello Hdınsight kümeden istediğiniz hello klasör izinlerini yalnızca atamanız gerekir. Örneğin, hello ekran görüntüsünde, yalnızca çok erişilmesine**hdiaddonstorage** bir Data Lake Store hesabında klasör.

![Hizmet asıl izinleri toohello Hdınsight kümesi atama](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.3-1.png "Ata hizmet asıl izinleri toohello Hdınsight kümesi")


## <a name="verify-cluster-set-up"></a>Küme ayarlama doğrulayın

Merhaba Küme kurulumu tamamlandıktan sonra hello küme dikey penceresinde veya her ikisini hello aşağıdaki adımları uygulayarak sonuçlarınızı doğrulayın:

* Merhaba küme belirttiğiniz hello Data Lake Store hesabı için ilişkili depolama Merhaba, tıklatın tooverify **depolama hesapları** hello sol bölmede.

    ![Ekle hizmet asıl tooHDInsight küme](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.6-1.png "Ekle hizmet asıl tooHDInsight küme")

* Hizmet sorumlusu hello tooverify doğru hello Hdınsight kümesi ile ilişkili, tıklatın **Data Lake Store erişim** hello sol bölmede.

    ![Ekle hizmet asıl tooHDInsight küme](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.6.png "Ekle hizmet asıl tooHDInsight küme")


## <a name="examples"></a>Örnekler

Data Lake Store ile Merhaba küme, depolama alanı olarak ayarladıktan sonra nasıl toouse Hdınsight küme Data Lake Store'da depolanan tooanalyze hello veri örnekleri toothese bakın.

### <a name="run-a-hive-query-against-data-in-a-data-lake-store-as-primary-storage"></a>(Birincil depolama) bir Data Lake Store'da verileri karşı Hive sorgusu çalıştırma

toorun bir Hive sorgusu hello Hive görünümleri hello Ambari portal arabiriminde kullanın. Nasıl toouse Ambari Hive görünümleri ile ilgili yönergeler için bkz: [kullanım hello hdınsight'ta Hadoop ile Hive görünümü](../hdinsight/hdinsight-hadoop-use-hive-ambari-view.md).

Bir Data Lake Store'da verilerle çalışırken, birkaç dizeleri toochange vardır.

Merhaba yol toohello verileri, örneğin, birincil depolama olarak Data Lake Store ile oluşturulan hello küme kullandığınız ise: *adl: / / < data_lake_store_account_name > /azuredatalakestore.net/path/to/file*. Bir Hive sorgusu toocreate hello Data Lake Store hesabı depolanan örnek veri tablosundan hello deyimi aşağıdaki gibi görünür:

    CREATE EXTERNAL TABLE websitelog (str string) LOCATION 'adl://hdiadlsstorage.azuredatalakestore.net/clusters/myhdiadlcluster/HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/'

Açıklamaları:
* `adl://hdiadlstorage.azuredatalakestore.net/`Merhaba Data Lake Store hesabı Hello köküdür.
* `/clusters/myhdiadlcluster`Merhaba küme oluşturulurken belirtilen hello küme verileri Hello köküdür.
* `/HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/`Merhaba hello sorguda kullanılan hello örnek dosyasının konumudur.

### <a name="run-a-hive-query-against-data-in-a-data-lake-store-as-additional-storage"></a>Bir Data Lake Store'da verileri karşı (ek depolama alanı olarak) Hive sorgusu çalıştırma

Oluşturduğunuz hello küme varsayılan depolama alanı olarak Blob Depolama birimi kullanıyorsa, hello örnek verileri hello ek depolama alanı olarak kullanılan Azure Data Lake Store hesabı dahil değil. Böyle bir durumda, ilk Blob Depolama toohello Data Lake Store hello verileri aktarmak ve ardından hello sorguları hello önceki örnekte gösterildiği gibi çalıştırın.

Nasıl toocopy verileri Blob depolama biriminden tooa Data Lake depolama hakkında daha fazla bilgi için aşağıdaki makaleleri hello bakın:

* [Azure Storage blobları ve Data Lake Store arasında Distcp'yi toocopy veri kullanın](data-lake-store-copy-data-wasb-distcp.md)
* [BLOB'ların tooData Lake Store AdlCopy toocopy verileri Azure Storage kullan](data-lake-store-copy-data-azure-storage-blob.md)

### <a name="use-data-lake-store-with-a-spark-cluster"></a>Kullanım Data Lake Store ile Spark kümesi
Bir Data Lake Store'da depolanan veriler üzerinde bir Spark kümesi toorun Spark işlerinin kullanabilirsiniz. Daha fazla bilgi için bkz: [kullanım Hdınsight Spark küme tooanalyze verileri Data Lake Store'da](../hdinsight/hdinsight-apache-spark-use-with-data-lake-store.md).


### <a name="use-data-lake-store-in-a-storm-topology"></a>Data Lake Store'da Storm topolojisini kullan
Bir Storm topolojisinin hello Data Lake Store toowrite verileri kullanabilirsiniz. Yönergeler için tooachieve bu senaryo, bkz: [kullanım Azure Data Lake Store Hdınsight ile Apache Storm ile](../hdinsight/hdinsight-storm-write-data-lake-store.md).

## <a name="see-also"></a>Ayrıca bkz.
* [PowerShell: Hdınsight küme toouse Data Lake Store oluşturma](data-lake-store-hdinsight-hadoop-use-powershell.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
