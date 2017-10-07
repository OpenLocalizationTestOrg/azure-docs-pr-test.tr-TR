---
title: "Power Query - Azure Hdınsight ile aaaConnect Excel tooHadoop | Microsoft Docs"
description: "Hdınsight'ta Hadoop nasıl tootake avantajı, business Intelligence bileşenleri ve Excel tooaccess veriler için Power Query kullanın depolanır öğrenin."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 01ad2f90-7520-44d9-8c16-4d936faaff9b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jgao
ms.openlocfilehash: 1213849f1bc04e0ed206750b80766ff2268664b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-excel-toohadoop-by-using-power-query"></a>Excel tooHadoop Power Query kullanarak bağlanma
Bir anahtar hello Microsoft büyük veri çözümü hello Microsoft iş zekası (BI) bileşenleri Azure hdınsight'ta Hadoop kümeleri ile tümleştirilmesi özelliğidir. Merhaba özelliği tooconnect Excel toohello hello verileri için Excel eklenti hello Microsoft Power Query kullanarak Hadoop kümenizle ilişkilendirilmiş Azure depolama hesabı birincil örnektir. Bu makalede nasıl tooset ayarlama ve kullanma Power Query tooquery verileri Hadoop kümesi ile ilişkili Hdınsight ile yönetilen aracılığıyla anlatılmaktadır.

### <a name="prerequisites"></a>Ön koşullar
Bu makalede başlamadan önce aşağıdaki öğelerindeki hello sahip olmanız gerekir:

* **Hdınsight kümesi**. tooconfigure biri bkz [Azure Hdınsight kullanmaya başlama][hdinsight-get-started].
* **Bir iş istasyonu** Windows 7, Windows Server 2008 R2 veya sonraki bir işletim sistemi çalıştıran.
* **Office 2016, Office 2013 Professional Plus, Office 365 ProPlus, Excel 2013 tek başına veya Office 2010 Professional Plus**.

## <a name="install-power-query"></a>Power Query yükleme
Power Query, çıktı veya bir Hdınsight kümesi üzerinde çalışan bir Hadoop iş tarafından oluşturuldu verileri içeri aktarabilirsiniz.

Excel 2016'da, Power Query hello Al & dönüştürme bölümü altında hello veri Şerit içine tümleştirilmiştir. Eski Excel sürümleri için Microsoft Power Query Excel için hello karşıdan [Microsoft Download Center] [ powerquery-download] ve yükleyin.

## <a name="import-hdinsight-data-into-excel"></a>Hdınsight verileri Excel'e aktarmak
Excel için Power Query Eklentisi Hello Hdınsight kümenize Excel'e burada PowerPivot ve güç harita gibi BI araçları kullanılan tooinspect olması, çözümlemek ve hello verileri görüntülemektedir kolay tooimport verilerden kolaylaştırır.

**Hdınsight kümesi tooimport verileri**

1. Excel'i açın.
2. Yeni bir boş çalışma kitabı oluşturun.
3. Aşağıdaki adımları Hello Excel sürümlerine göre hello gerçekleştirin:

    - Excel 2016

        - Hello'ı tıklatın **veri** menüsünde tıklatın **Veri Al** hello gelen **Get & dönüştürme veri** Şerit'ye tıklayın **Azure**ve 'ıtıklatın** Azure HDInsight(HDFS) gelen**.

        ![HDI. PowerQuery.SelectHdiSource](./media/hdinsight-connect-excel-power-query/hdi.powerquery.selecthdisource.excel2016.png)

    - Excel 2013/2010

        - Merhaba tıklatın **Power Query** menüsünde tıklatın **Azure**ve ardından **Microsoft Azure Hdınsight'den**.
   
        ![HDI. PowerQuery.SelectHdiSource][image-hdi-powerquery-hdi-source]
       
        **Not:** hello görmüyorsanız, **Power Query** menüsünde çok Git**dosya** > **seçenekleri** > **eklentileri**seçip **COM eklentileri** hello açılan gelen **Yönet** hello sayfasının hello alttaki kutusu. Select hello **Git... ** düğmesine tıklayın ve Excel eklentisi için Power Query hello teslim için hello kutunun doğrulayın.
       
        **Not:** Power Query de verir HDFS tooimport verilerden tıklayarak **diğer kaynaklardan**.
4. İçin **hesap adı**hello hello kümenizle ilişkilendirilmiş Azure Blob Depolama hesabı adını girin ve ardından **Tamam**. Bu hesap hello olabilir [varsayılan depolama hesabı](hdinsight-administer-use-management-portal.md#find-the-default-storage-account) ya da bağlantılı depolama hesabı.  Merhaba biçimi *https://&lt;StorageAccountName >.blob.core.windows.net/*.
5. İçin **hesap anahtarı**hello Blob storage hesabı hello anahtarını girin ve ardından **kaydetmek**. (Bu deposuna erişim ilk kez tooenter hello hesap bilgileri yalnızca hello gerekir.)
6. Merhaba, **Gezgini** hello bölmesi sol Merhaba sorgu Düzenleyicisi'ni, hello Blob Depolama kapsayıcısını adına çift tıklayın. Varsayılan olarak, hello kapsayıcı adı olduğu hello aynı hello küme adı olarak adı.
7. Bulun **HiveSampleData.txt** hello içinde **adı** sütun (Merhaba klasör yolu **.. / hive / / hivesampletable/ambar**) ve ardından **ikili** HiveSampleData.txt hello soldaki. HiveSampleData.txt tüm hello kümesi ile birlikte gelir. İsteğe bağlı olarak, kendi dosyasını kullanabilirsiniz.
   
    ![HDI. PowerQuery.ImportData][image-hdi-powerquery-importdata]
8. İsterseniz, hello sütun adlarını yeniden adlandırabilirsiniz. Hazır olduğunuzda tıklatın **Kapat & yük**.  Merhaba veri yüklenen tooyour çalışma kitabı oldu:
   
    ![HDI. PowerQuery.ImportedTable][image-hdi-powerquery-imported-table]

## <a name="next-steps"></a>Sonraki adımlar
Bu makalede, nasıl öğrenilen toouse Power Query tooretrieve verileri Excel'e Hdınsight. Benzer şekilde, Hdınsight'ta Azure SQL veritabanına veri alabilir. Hdınsight olası tooupload verilerini de olabilir. toolearn daha makaleler hello bakın:

* [Excel tooHDInsight hello Microsoft Hive ODBC sürücüsü ile bağlanma][hdinsight-ODBC]
* [Veri tooHDInsight karşıya yükle][hdinsight-upload-data]

[hdinsight-ODBC]: hdinsight-connect-excel-hive-odbc-driver.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[image-hdi-powerquery-hdi-source]: ./media/hdinsight-connect-excel-power-query/hdi.powerquery.selecthdisource.png
[image-hdi-powerquery-importdata]: ./media/hdinsight-connect-excel-power-query/hdi.powerquery.importdata.png
[image-hdi-powerquery-imported-table]: ./media/hdinsight-connect-excel-power-query/hdi.powerquery.importedtable.PNG

[powerquery-download]: http://go.microsoft.com/fwlink/?LinkID=286689
