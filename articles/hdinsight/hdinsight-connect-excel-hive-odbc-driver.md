---
title: "Merhaba Hive ODBC sürücüsü - Azure Hdınsight ile aaaConnect Excel tooHadoop | Microsoft Docs"
description: "Excel tooquery veri Hdınsight kümelerinde Microsoft Excel için Microsoft Hive ODBC sürücüsü tooset ayarlama ve kullanma nasıl hello öğrenin."
keywords: hadoop excel, hive excel, hive odbc
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
tags: azure-portal
editor: cgronlun
ms.assetid: a7665a14-0211-4521-b3e7-3b26e8029cc0
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/22/2017
ms.author: jgao
ms.openlocfilehash: f01f89e7d4203c739d56079dc589fc11f4aa2174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-excel-toohadoop-in-azure-hdinsight-with-hello-microsoft-hive-odbc-driver"></a>Azure hdınsight'ta Excel tooHadoop hello Microsoft Hive ODBC sürücüsü ile bağlanma

[!INCLUDE [ODBC-JDBC-selector](../../includes/hdinsight-selector-odbc-jdbc.md)]

Microsoft'un büyük veri çözüm Microsoft Business Intelligence (BI) bileşenleri hello Azure Hdınsight tarafından dağıtılan Apache Hadoop kümeleri ile tümleşir. Bu tümleştirme hello özelliği tooconnect Excel toohello Hive veri ambarının hello Microsoft Hive açık veritabanı bağlantısı (ODBC) sürücüsü kullanarak hdınsight'ta Hadoop kümesi örneğidir.

Ayrıca bir Hdınsight kümesi ve diğer veri kaynakları ile ilgili olası tooconnect hello veri olduğundan, diğer (olmayan-Hdınsight) Hadoop kümeleri, hello kullanarak Excel'den Excel için Microsoft Power Query Eklentisi. Yükleme ve Power Query kullanma hakkında daha fazla bilgi için bkz: [Power Query ile bağlanma Excel tooHDInsight][hdinsight-power-query].

> [!NOTE]
> Merhaba adımları sırasında bu makalede bir ya da Linux ile kullanılabilir veya Windows tabanlı Hdınsight kümesi, Windows hello istemci iş istasyonu için gereklidir.
> 
> 

**Önkoşullar**:

Bu makalede başlamadan önce aşağıdaki öğelerindeki hello sahip olmanız gerekir:

* **Hdınsight kümesi**. toocreate biri bkz [Azure Hdınsight kullanmaya başlama][hdinsight-get-started].
* **Bir iş istasyonu** Office 2013 Professional Plus, Office 365 Pro Plus, Excel 2013 tek başına veya Office 2010 Professional Plus ile.

## <a name="install-microsoft-hive-odbc-driver"></a>Microsoft Hive ODBC sürücüsünü yükleme
Microsoft Hive ODBC sürücüsü hello yükleyip [Yükleme Merkezi'nden][hive-odbc-driver-download].

Bu sürücü Windows 7, Windows 8, Windows 10, Windows Server 2008 R2 ve Windows Server 2012, 32 bit veya 64 bit sürümlerinde yüklenebilir. Merhaba sürücüsü verir bağlantı tooAzure Hdınsight (sürüm 1.6 ve üstü) ve Azure Hdınsight öykünücüsünde (v.1.0.0.0 ve üzeri). Merhaba uygulaması hello ODBC sürücüsü kullandığınız hello sürümüyle eşleşen hello sürümünü yükleyin. Bu öğretici için Office Excel'den hello sürücü kullanılır.

## <a name="create-hive-odbc-data-source"></a>Hive ODBC veri kaynağı oluşturma
Merhaba aşağıdaki adımlarda size yol gösterecektir toocreate Hive ODBC veri kaynağı.

1. Windows 8 veya Windows 10, hello Windows anahtar tooopen hello başlangıç ekranı tuşuna basın ve ardından yazın **veri kaynakları**.
2. Tıklatın **ODBC veri kaynakları (32 bit) ayarlamanız** veya **ODBC veri kaynakları (64 bit) ayarlamanız** Office sürümüne bağlı olarak. Windows 7 kullanıyorsanız seçin **ODBC veri kaynakları (32 bit)** veya **ODBC veri kaynakları (64 bit)** gelen **Yönetimsel Araçlar**. Merhaba göreceksiniz **ODBC Veri Kaynağı Yöneticisi** iletişim.
   
    ![OBDC Veri Kaynağı Yöneticisi](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.DataSourceAdmin1.png "ODBC Veri Kaynağı Yöneticisi kullanan bir DSN'ye yapılandırın")

3. Kullanıcı DNS'den tıklatın **Ekle** tooopen hello **yeni veri kaynağı oluştur** Sihirbazı.
4. Seçin **Microsoft Hive ODBC sürücüsü**ve ardından **son**. Merhaba göreceksiniz **Microsoft Hive ODBC sürücüsü DNS Kurulumu** iletişim.
5. Değerleri aşağıdaki hello seçin veya yazın:
   
   | Özellik | Açıklama |
   | --- | --- |
   |  Data Source Name |Bir ad tooyour veri kaynağı verin |
   |  Host |&lt;HDInsightKümesiAdı>.azurehdinsight.net yazın. Örnek: HDIKumesi.azurehdinsight.net |
   |  Bağlantı noktası |<strong>443</strong> yazın. (Bu bağlantı noktasına 563 too443 değiştirildi.) |
   |  Database |<strong>Default</strong>’u kullanın. |
   |  Mechanism |<strong>Azure HDInsight Service</strong>’i seçin |
   |  User Name |Hdınsight küme HTTP kullanıcının kullanıcı adı girin. Merhaba varsayılan kullanıcı adı <strong>yönetici</strong>. |
   |  Parola |Hdınsight küme kullanıcı parolasını girin. |
   
    </table>
   
    Bazı önemli parametreleri toobe tıkladığınızda farkında **Gelişmiş Seçenekler**:
   
   | Parametre | Açıklama |
   | --- | --- |
   |  Yerel sorgu kullanma |Seçildiğinde, hello ODBC sürücüsü HiveQL tooconvert TSQL denemez. Yalnızca % 100 saf HiveQL ifadelerini gönderiliyor emin olduğunuzda kullanın. TooSQL sunucusu veya Azure SQL veritabanına bağlanırken denetlenmeyen bırakmanız gerekir. |
   |  Satır blok alınarak |Bu parametre ayarlama, çok sayıda kayıt getirilirken gerekli tooensure en iyi performanslarını olabilir. |
   |  Varsayılan dize sütun uzunluğu, ikili sütun uzunluğu, ondalık sütun ölçeği |Merhaba veri türü uzunlukları ve Precision bilgisayarlar, verinin nasıl döndürüldüğüne etkileyebilir. Son döndürülen yanlış bilgi toobe neden duyarlık ve/veya kesme tooloss. |

    ![Gelişmiş Seçenekleri](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.HiveOdbc.DataSource.AdvancedOptions1.png "DSN Gelişmiş yapılandırma seçenekleri")

1. Tıklatın **Test** tootest hello veri kaynağı. Merhaba veri kaynağının doğru şekilde yapılandırıldığında, gösterir *TESTLERİ başarıyla tamamlandı!*.
2. Tıklatın **Tamam** tooclose hello Test iletişim. Merhaba yeni veri kaynağı üzerinde hello listelenen **ODBC Veri Kaynağı Yöneticisi**.
3. Tıklatın **Tamam** tooexit hello Sihirbazı.

## <a name="import-data-into-excel-from-hdinsight"></a>HDInsight’tan Excel’e veri aktarma
Merhaba aşağıdaki adımlar bir Hive tablosu hello yolu tooimport verileri'hello önceki bölümde oluşturduğunuz hello ODBC veri kaynağını kullanan bir Excel çalışma kitabına açıklar.

1. Excel’de yeni veya mevcut bir çalışma kitabını açın.
2. Merhaba gelen **veri** sekmesini tıklatın, **Veri Al**, tıklatın **diğer kaynaklardan**ve ardından **gelen ODBC** toolaunch hello  **Veri Bağlantı Sihirbazı**.
   
    ![Açık Veri Bağlantı Sihirbazı'nı](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.Excel.DataConnection1.png "açık Veri Bağlantı Sihirbazı")
4. Select hello veri kaynağı hello son bölümünde oluşturduğunuz adı ve ardından **Tamam**.
5. Hadoop kullanıcı adını girin (Merhaba varsayılan addır yönetici) ve parola hello ve ardından **Bağlan**.
6. Gezgin üzerinde genişletin **HIVE**, genişletin **varsayılan**, tıklatın **hivesampletable**ve ardından **yük**. Veri içe aktarılan tooExcel büyümeden birkaç saniye sürer.

    ![Hdınsight Hive ODBC Gezgini](./media/hdinsight-connect-excel-hive-ODBC-driver/hdinsight.hive.odbc.navigator.png "açık Veri Bağlantı Sihirbazı")


## <a name="next-steps"></a>Sonraki adımlar
Bu makalede, nasıl toouse hello hello Hdınsight hizmeti Microsoft Hive ODBC sürücüsü tooretrieve verileri Excel'e öğrendiniz. Benzer şekilde, Hdınsight hizmeti hello SQL veritabanına veri alabilir. Ayrıca bir Hdınsight hizmeti olası tooupload verisine olur. toolearn daha bakın:

* [Hdınsight kullanma uçuş gecikme verilerini çözümleme][hdinsight-analyze-flight-data]
* [Veri tooHDInsight karşıya yükle][hdinsight-upload-data]
* [Hdınsight ile Sqoop kullanma][hdinsight-use-sqoop]

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-get-started]: hdinsight-hadoop-tutorial-get-started-windows.md

[hive-odbc-driver-download]: http://go.microsoft.com/fwlink/?LinkID=286698


