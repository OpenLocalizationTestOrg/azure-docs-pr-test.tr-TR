---
title: "Azure Storage Bloblarında Data Lake Store içine aaaCopy verilerden | Microsoft Docs"
description: "Azure depolama BLOB'lar tooData Lake deposundan AdlCopy aracı toocopy verileri kullanma"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: dc273ef8-96ef-47a6-b831-98e8a777a5c1
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: a3d4172eaefe7395cdef2fff72691bd70f642b78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-from-azure-storage-blobs-toodata-lake-store"></a>Azure Storage Blobları tooData Lake Mağazası'ndan veri kopyalama
> [!div class="op_single_selector"]
> * [DistCp’yi kullanma](data-lake-store-copy-data-wasb-distcp.md)
> * [AdlCopy’yi kullanma](data-lake-store-copy-data-azure-storage-blob.md)
>
>

Azure Data Lake Store sağlayan bir komut satırı aracı [AdlCopy](http://aka.ms/downloadadlcopy), aşağıdaki kaynaklar hello toocopy verileri:

* Data Lake Store içinde Azure Storage Bloblarından. Data Lake Store tooAzure depolama BLOB'ları AdlCopy toocopy verileri kullanamazsınız.
* İki Azure Data Lake Store hesapları arasında.

Ayrıca, iki farklı modda hello AdlCopy aracını kullanabilirsiniz:

* **Tek başına**burada hello aracı Data Lake Store kaynakları tooperform hello görevi kullanır.
* **Bir Data Lake Analytics hesabı kullanarak**, burada tooyour Data Lake Analytics hesabı atanan hello kullanılan tooperform hello kopyalama işlemi birimleridir. Tahmin edilebilir bir biçimde tooperform hello kopyalama görevleri bakıldığında, bu seçenek toouse isteyebilirsiniz.

## <a name="prerequisites"></a>Ön koşullar
Bu makaleye başlamadan önce hello şunlara sahip olmanız gerekir:

* **Bir Azure aboneliği**. Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/pricing/free-trial/).
* **Azure Storage Bloblarında** bazı verileri içeren kapsayıcı.
* **Bir Azure Data Lake Store hesabı**. Yönergeler için toocreate bir, bkz: [Azure Data Lake Store ile çalışmaya başlama](data-lake-store-get-started-portal.md)
* **Azure Data Lake Analytics hesabı (isteğe bağlı)** -bkz [Azure Data Lake Analytics ile çalışmaya başlama](../data-lake-analytics/data-lake-analytics-get-started-portal.md) nasıl toocreate bir Data Lake depolamak hakkında yönergeler için hesap.
* **AdlCopy aracı**. Merhaba AdlCopy aracından yüklemek [http://aka.ms/downloadadlcopy](http://aka.ms/downloadadlcopy).

## <a name="syntax-of-hello-adlcopy-tool"></a>Merhaba AdlCopy aracının sözdizimi
Merhaba AdlCopy aracıyla sözdizimi toowork aşağıdaki hello kullanın

    AdlCopy /Source <Blob or Data Lake Store source> /Dest <Data Lake Store destination> /SourceKey <Key for Blob account> /Account <Data Lake Analytics account> /Unit <Number of Analytics units> /Pattern

hello sözdiziminde Hello Parametreler aşağıda açıklanmıştır:

| Seçenek | Açıklama |
| --- | --- |
| Kaynak |Merhaba kaynak verilerin Hello konumunu hello Azure depolama blobunu belirtir. Merhaba kaynağı, bir blob kapsayıcı, blob veya başka bir Data Lake Store hesabı olabilir. |
| Hedef |Merhaba Data Lake Store hedef toocopy belirtir. |
| SourceKey |Merhaba depolama erişim tuşu'hello Azure storage blobu kaynağı için belirtir. Bu, yalnızca hello kaynak blob kapsayıcısı veya bir blobu ise gereklidir. |
| Hesap |**İsteğe bağlı**. Toouse Azure Data Lake Analytics hesabı toorun hello kopyalama işini isterseniz bunu kullanın. Hello ApplicationTier/account seçeneği hello sözdiziminde kullanın, ancak bir Data Lake Analytics hesabı belirtmezseniz, varsayılan hesap toorun hello iş AdlCopy kullanır. Bu seçeneği kullanırsanız, ayrıca, (Azure depolama Blob) hello kaynak ve hedef (Azure Data Lake Store) veri kaynakları olarak Data Lake Analytics hesabınız için eklemeniz gerekir. |
| Birimler |Merhaba hello kopyalama işlemi için kullanılan Data Lake Analytics birim sayısını belirtir. Merhaba kullanırsanız, bu seçenek zorunludur **/hesabını** seçeneği toospecify hello Data Lake Analytics hesabı. |
| düzeni |Hangi BLOB veya dosyaları toocopy gösteren bir regex düzenidir belirtir. Büyük küçük harfe duyarlı eşleşen AdlCopy kullanır. Merhaba varsayılan düzen kullanılan tüm öğeleri toocopy olan hiçbir düzeni belirtildiğinde. Birden çok dosya desenlerinin belirtilmesi desteklenmiyor. |

## <a name="use-adlcopy-as-standalone-toocopy-data-from-an-azure-storage-blob"></a>Bir Azure Storage blobu AdlCopy (olarak tek başına) toocopy verileri kullan
1. Bir komut istemi açın ve AdlCopy yüklü olduğu, genellikle toohello dizinine gidin `%HOMEPATH%\Documents\adlcopy`.
2. Komut toocopy aşağıdaki hello hello kaynak kapsayıcı tooa Data Lake Store belirli bir blobu çalıştırın:

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>

    Örneğin:

        AdlCopy /source https://mystorage.blob.core.windows.net/mycluster/HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b.log /dest swebhdfs://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

    >[AZURE.NOTE] Merhaba söz dizimini hello Data Lake Store hesabında hello dosya toobe kopyalanan tooa klasörü belirtir. Merhaba belirtilen klasör adı yoksa, AdlCopy aracı bir klasör oluşturur.

    Merhaba kimlik bilgileri istendiğinde tooenter olacaktır Azure aboneliğinizin Data Lake Store hesabınızın altında elinizde hello. Bir çıkış benzer toohello aşağıdaki görürsünüz:

        Initializing Copy.
        Copy Started.
        100% data copied.
        Finishing Copy.
        Copy Completed. 1 file copied.

1. Ayrıca, tüm hello BLOB'lar komutu aşağıdaki hello kullanarak bir kapsayıcı toohello Data Lake Store hesabından kopyalayabilirsiniz:

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/ /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>        

    Örneğin:

        AdlCopy /Source https://mystorage.blob.core.windows.net/mycluster/example/data/gutenberg/ /dest adl://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

### <a name="performance-considerations"></a>Performansla ilgili önemli noktalar

Bir Azure Blob Depolama hesabından kopyalıyorsanız hello blob depolama tarafında kopyalama sırasında kısıtlanan. Bu kopyalama işinin hello performansının düşmesine neden. Azure Blob Storage ' hello sınırları hakkında daha fazla toolearn adresindeki Azure depolama sınırları bkz [Azure aboneliği ve hizmet sınırları](../azure-subscription-service-limits.md).

## <a name="use-adlcopy-as-standalone-toocopy-data-from-another-data-lake-store-account"></a>(Tek başına) olarak AdlCopy toocopy verileri başka bir Data Lake Store hesabını kullan
İki Data Lake Store hesapları arasında AdlCopy toocopy verileri de kullanabilirsiniz.

1. Bir komut istemi açın ve AdlCopy yüklü olduğu, genellikle toohello dizinine gidin `%HOMEPATH%\Documents\adlcopy`.
2. Komut toocopy aşağıdaki hello bir Data Lake Store hesabı tooanother belirli bir dosya çalıştırın.

        AdlCopy /Source adl://<source_adls_account>.azuredatalakestore.net/<path_to_file> /dest adl://<dest_adls_account>.azuredatalakestore.net/<path>/

    Örneğin:

        AdlCopy /Source adl://mydatastore.azuredatalakestore.net/mynewfolder/909f2b.log /dest adl://mynewdatalakestore.azuredatalakestore.net/mynewfolder/

   > [!NOTE]
   > Merhaba söz dizimini hello hedef Data Lake Store hesabında hello dosya toobe kopyalanan tooa klasörü belirtir. Merhaba belirtilen klasör adı yoksa, AdlCopy aracı bir klasör oluşturur.
   >
   >

    Merhaba kimlik bilgileri istendiğinde tooenter olacaktır Azure aboneliğinizin Data Lake Store hesabınızın altında elinizde hello. Bir çıkış benzer toohello aşağıdaki görürsünüz:

        Initializing Copy.
        Copy Started.|
        100% data copied.
        Finishing Copy.
        Copy Completed. 1 file copied.
3. Merhaba aşağıdaki komutu tüm dosyaları hello kaynak Data Lake Store hesabı tooa klasöründe hello hedef Data Lake Store hesabı belirli bir klasöre kopyalar.

        AdlCopy /Source adl://mydatastore.azuredatalakestore.net/mynewfolder/ /dest adl://mynewdatalakestore.azuredatalakestore.net/mynewfolder/

### <a name="performance-considerations"></a>Performansla ilgili önemli noktalar

AdlCopy ayrı bir araç olarak kullanırken, hello kopyalama paylaşılan çalıştırıldığı, yönetilen Azure kaynakları. Bu ortamda alabilirsiniz hello performans sistem yükü ve kullanılabilir kaynakları bağlıdır. Bu mod, en iyi geçici düzenli olarak küçük aktarımlar için kullanılır. Hiçbir parametre AdlCopy ayrı bir araç olarak kullanırken ayarlanmış toobe gerekir.

## <a name="use-adlcopy-with-data-lake-analytics-account-toocopy-data"></a>(Data Lake Analytics hesabıyla) AdlCopy toocopy verileri kullanma
Data Lake Analytics ayrıca kullanabileceğiniz toorun hello AdlCopy iş toocopy verileri Azure depolama biriminden BLOB'ların tooData Lake Store hesabı. Genellikle taşınmış hello veri toobe gigabayt ve terabayt hello aralığında olan ve daha iyi ve tahmin edilebilir performans verimlilik istediğinizde bu seçeneği kullanırsınız.

toouse Data Lake Analytics hesabınızla bir Azure depolama Blob hello kaynak (Azure depolama Blob) gelen AdlCopy toocopy Data Lake Analytics hesabınız için bir veri kaynağı olarak eklenmesi gerekir. Ek veri kaynaklarını tooyour Data Lake Analytics hesabı ekleme ile ilgili yönergeler için bkz: [yönetmek Data Lake Analytics hesabı veri kaynaklarını](../data-lake-analytics/data-lake-analytics-manage-use-portal.md#manage-data-sources).

> [!NOTE]
> Bir Data Lake Analytics hesabı kullanarak hello kaynağı olarak bir Azure Data Lake Store hesabından kopyalıyorsanız hello Data Lake Analytics hesabı ile tooassociate hello Data Lake Store hesabı gerekmez. Merhaba gereksinim tooassociate hello kaynak hello Data Lake Analytics hesabı ile yalnızca hello kaynak bir Azure Storage hesabı olduğunda deposudur.
>
>

Data Lake Analytics hesabı kullanarak bir Azure Storage blobu tooa Data Lake Store hesabından komutu toocopy aşağıdaki hello çalıştırın:

    AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container> /Account <data_lake_analytics_account> /Unit <number_of_data_lake_analytics_units_to_be_used>

Örneğin:

    AdlCopy /Source https://mystorage.blob.core.windows.net/mycluster/example/data/gutenberg/ /dest swebhdfs://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ== /Account mydatalakeanalyticaccount /Units 2

Benzer şekilde, Data Lake Analytics hesabı kullanarak bir Azure Storage blobu tooa Data Lake Store hesabından komutu toocopy aşağıdaki hello çalıştırın:

    AdlCopy /Source adl://mysourcedatalakestore.azuredatalakestore.net/mynewfolder/ /dest adl://mydestdatastore.azuredatalakestore.net/mynewfolder/ /Account mydatalakeanalyticaccount /Units 2

### <a name="performance-considerations"></a>Performansla ilgili önemli noktalar

Veri terabayt hello aralığında kopyalarken, kendi Azure Data Lake Analytics hesabıyla AdlCopy kullanarak daha iyi ve daha tahmin edilebilir performans sağlar. ayarlanması hello parametre hello hello kopyalama işini için Azure Data Lake Analytics birimleri toouse sayısıdır. Birimleri Hello sayısını artırmayı kopyalama işini hello performansını artırır. Kopyalanan her dosyayı toobe en fazla bir birimi kullanabilirsiniz. Kopyalanan dosyalar hello sayısından daha fazla birimi belirtme performans da artar.

## <a name="use-adlcopy-toocopy-data-using-pattern-matching"></a>Desen eşleştirme kullanarak AdlCopy toocopy veri kullanın
Bu bölümde, bilgi nasıl toouse AdlCopy toocopy veri kaynağından (Bizim örneğimizde Azure Storage Blobuna kullanırız) desen eşleştirme kullanarak tooa hedef Data Lake Store hesabı. Örneğin, hello kaynak blob toohello hedef .csv uzantılı tüm dosyaları toocopy hello adımları kullanabilirsiniz.

1. Bir komut istemi açın ve AdlCopy yüklü olduğu, genellikle toohello dizinine gidin `%HOMEPATH%\Documents\adlcopy`.
2. Komut toocopy aşağıdaki hello tüm dosyaları *.csv uzantısı ile belirli bir blob hello kaynak kapsayıcı tooa Data Lake Store üzerinden çalıştırın:

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container> /Pattern *.csv

    Örneğin:

        AdlCopy /source https://mystorage.blob.core.windows.net/mycluster/HdiSamples/HdiSamples/FoodInspectionData/ /dest adl://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ== /Pattern *.csv

## <a name="billing"></a>Faturalandırma
* Taşıma için çıkışı maliyeti, Fatura edilecek bağımsız hello AdlCopy aracı kullanırsanız hello kaynak Azure depolama hesabı değilse veri aynı bölgede Data Lake Store hello gibi hello.
* Data Lake Analytics ile Merhaba AdlCopy aracı kullanırsanız, standart hesap [Data Lake Analytics oranları faturalama](https://azure.microsoft.com/pricing/details/data-lake-analytics/) uygulanır.

## <a name="considerations-for-using-adlcopy"></a>AdlCopy kullanma konuları
* AdlCopy (için sürüm 1.0.5), topluca binlerce dosyaları ve klasörleri birden fazla sahip kaynaklardan veri kopyalamayı destekler. Ancak, büyük bir veri kümesini kopyalama sorunlarla karşılaşırsanız, hello dosyaların/klasörlerin farklı alt klasörler halinde dağıtabilir ve hello yolu toothose alt klasörleri hello kaynağı olarak kullanın.

## <a name="performance-considerations-for-using-adlcopy"></a>Başarım Değerlendirmeleri AdlCopy kullanma

AdlCopy binlerce dosyaları ve klasörleri içeren veri kopyalamayı destekler. Ancak, büyük bir veri kümesini kopyalama sorunlarla karşılaşırsanız, daha küçük alt klasörler halinde hello dosyaların/klasörlerin dağıtabilirsiniz. AdlCopy için geçici kopya oluşturuldu. Yinelenen temelinde toocopy veri çalışıyorsanız kullanmayı düşünmelisiniz [Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md) hello kopyalama işlemleri geçici tam yönetim sağlar.

## <a name="release-notes"></a>Sürüm notları
* Veri toohello kopyalıyorsanız 1.0.13 - birden çok adlcopy arasında aynı Azure Data Lake Store hesabı komutlar, her biri için kimlik bilgilerinizi çalıştırmak artık tooreenter gerekmez. Adlcopy artık birden çok çalıştırmaları arasında bu bilgileri önbelleğe alır.

## <a name="next-steps"></a>Sonraki adımlar
* [Data Lake Store'da verilerin güvenliğini sağlama](data-lake-store-secure-data.md)
* [Azure Data Lake Analytics'i Data Lake Store ile kullanma](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Azure HDInsight'ı Data Lake Store ile kullanma](data-lake-store-hdinsight-hadoop-use-portal.md)
