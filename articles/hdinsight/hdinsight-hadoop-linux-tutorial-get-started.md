---
title: "Hadoop ve Azure hdınsight'ta Hive kullanmaya aaaGet | Microsoft Docs"
description: "Nasıl toocreate Hdınsight kümeleri ve Hive sorgusu verilerle öğrenin."
keywords: "hadoop kullanmaya başlama,hadoop linux,hadoop hızlı başlangıç,hive kullanmaya başlama,hive hızlı başlangıç"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 6a12ed4c-9d49-4990-abf5-0a79fdfca459
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/23/2017
ms.author: jgao
ms.openlocfilehash: 3d96d78121200ebda3626dd2c3885e3ddacd546d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="hadoop-tutorial-get-started-using-hadoop-in-hdinsight"></a>Hadoop öğreticisi: HDInsight’ta Hadoop kullanmaya başlama

Bilgi nasıl toocreate [Hadoop](http://hadoop.apache.org/) ve Hdınsight'ta nasıl toorun Hive işleri kümeleri. [Apache Hive](https://hive.apache.org/) hello Hadoop ekosistemindeki hello en popüler bileşendir. Şu anda HDInsight [yedi farklı küme türüyle](hdinsight-hadoop-introduction.md#overview) ile birlikte gelir. Her küme türü farklı bir bileşen kümesini destekler. Tüm küme türleri Hive'ı destekler. Hdınsight'ta desteklenen bileşenlerin listesi için bkz: [Hdınsight tarafından sağlanan hello Hadoop küme sürümlerindeki yenilikler nelerdir?](hdinsight-component-versioning.md)  

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="prerequisites"></a>Ön koşullar
Bu öğreticiye başlamadan önce

* **Azure aboneliği**: toocreate ücretsiz bir aylık deneme hesabı, Gözat çok[azure.microsoft.com/free](https://azure.microsoft.com/free).

## <a name="create-cluster"></a>Küme oluşturma

Hadoop işlerinin çoğu toplu işlemdir. Bir küme oluşturmak, bazı işleri çalıştırır ve hello küme silin. Bu bölümde, [Azure Resource Manager şablonu](../azure-resource-manager/resource-group-template-deploy.md) kullanarak HDInsight'ta Hadoop kümesi oluşturacaksınız. Bu öğreticiyi kullanmak için Resource Manager şablonuyla deneyim sahibi olmak gerekli değildir. Diğer küme oluşturma yöntemleri ve Bu öğreticide kullanılan hello özellikler hakkında bilgi edinmek bkz [Hdınsight kümeleri oluşturma](hdinsight-hadoop-provision-linux-clusters.md). Merhaba seçiciyi hello sayfa toochoose hello üstte, küme oluşturma seçenekleri kullanın.

Bu öğreticide kullanılan hello Resource Manager şablonu bulunduğu [GitHub](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-password/). 

1. Görüntü toosign tooAzure olarak ve açık hello Resource Manager şablonu hello Azure Portalı'nda aşağıdaki hello'ı tıklatın. 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-ssh-password%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hadoop-linux-tutorial-get-started/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. Girin veya değerleri aşağıdaki hello seçin:
   
    ![Hdınsight Linux ile çalışmaya başlama Resource Manager şablonu portalında](./media/hdinsight-hadoop-linux-tutorial-get-started/hdinsight-linux-get-started-arm-template-on-portal.png "HDInsigut kullanarak dağıtmak Hadoop kümesi hello Azure portalı ve bir kaynak grubu yöneticisi şablonu").
   
    * **Abonelik**: Azure aboneliğinizi seçin.
    * **Kaynak grubu**: Kaynak grubu oluşturun veya mevcut bir kaynak grubunu seçin.  Kaynak grubu, Azure bileşenleri için bir kapsayıcıdır.  Bu durumda, hello kaynak grubu hello Hdınsight kümesi ve hello bağımlı Azure depolama hesabı içeriyor. 
    * **Konum**: toocreate kümenizi bir Azure konumu seçin.  Daha iyi performans için bir konum daha yakından tooyou seçin. 
    * **Küme Türü**: Bu öğretici için **hadoop**'u seçin.
    * **Küme adı**: Merhaba Hadoop kümesi için bir ad girin.
    * **Küme oturum açma adı ve parola**: hello varsayılan oturum açma adı **yönetici**.
    * **SSH kullanıcı adı ve parola**: hello varsayılan kullanıcı adı **sshuser**.  Bunu yeniden adlandırabilirsiniz. 
     
    Bazı özellikler sabit kodlanmış hello şablonunda olmuştur.  Bu değerleri hello şablondan yapılandırabilirsiniz.

    * **Konum**: Merhaba hello küme konumunu ve hello bağımlı depolama hesabı paylaşımı hello hello kaynak grubu olarak aynı konumu.
    * **Küme sürümü**: 3.5
    * **İşletim Sistemi Türü**: Linux
    * **Çalışan düğümü sayısı**: 2

     Her kümenin bir [Azure Depolama hesabı](hdinsight-hadoop-use-blob-storage.md) veya [Azure Data Lake hesabı](hdinsight-hadoop-use-data-lake-store.md) bağımlılığı vardır. Merhaba varsayılan depolama hesabı olarak adlandırılır. Hdınsight kümesi ve kümenin varsayılan depolama hesabının bulunması gerekir. ortak hello aynı Azure bölgesi. Kümeleri silmek hello depolama hesabını silmez. 
     
     Bu özellikler hakkında daha fazla açıklama için bkz. [HDInsight'ta Hadoop kümeleri oluşturma](hdinsight-hadoop-provision-linux-clusters.md).

3. Seçin **toohello hüküm ve koşullar yukarıda belirtildiği kabul** ve **PIN toodashboard**ve ardından **satın alma**. Başlıklı yeni bir kutucuk göreceksiniz **dağıtma şablon dağıtımı** hello portal panosunda. Bir küme hakkında toocreate yaklaşık 20 dakika sürer. Hello Küme oluşturulduktan sonra hello döşeme hello resim yazısı belirttiğiniz değiştirilen toohello kaynak grubu adı ' dir. Ve hello portal, otomatik olarak hello kaynak grubu yeni bir dikey pencerede açar. Merhaba küme ve listelenen hello varsayılan depolama görebilirsiniz.
   
    ![HDInsight - Linux - başlarken - kaynak grubu](./media/hdinsight-hadoop-linux-tutorial-get-started/hdinsight-linux-get-started-resource-group.png "Azure HDInsight küme kaynağı grubu").

4. Yeni bir dikey penceresinde Hello küme adı tooopen hello kümesine tıklayın.

   ![HDInsight - Linux - başlarken - küme ayarları](./media/hdinsight-hadoop-linux-tutorial-get-started/hdinsight-linux-get-started-cluster-settings.png "HDInsight küme özellikleri")


## <a name="run-hive-queries"></a>Hive sorguları çalıştırma
[Apache Hive](hdinsight-use-hive.md) Hdınsight'ta kullanılan hello en popüler bileşendir. Hdınsight'ta Hive işleri toorun birçok yolu vardır. Bu öğreticide, hello hello portal Ambari Hive görünümünü kullanın. Hive işlerini göndermenin diğer yöntemleri için bkz. [HDInsight’ta Hive kullanma](hdinsight-use-hive.md).

1. Merhaba önceki ekran görüntüsünde tıklatın **küme Panosu**ve ardından **Hdınsight küme Panosu**.  Ayrıca çok gözatabilirsiniz **https://&lt;ClusterName >. azurehdinsight.net**, burada &lt;ClusterName > merhaba önceki bölümde tooopen içinde Ambari oluşturduğunuz hello kümedir.
2. Merhaba Hadoop kullanıcı adını ve hello önceki bölümde belirttiğiniz parolayı girin. Merhaba varsayılan kullanıcı adı **yönetici**.
3. Açık **Hive görünümü** hello ekran aşağıdaki gösterildiği gibi:
   
    ![Ambari görünümlerini seçme](./media/hdinsight-hadoop-linux-tutorial-get-started/selecthiveview.png "HDInsight Hive Viewer menüsü").
4. Merhaba, **sorgu Düzenleyicisi'ni** hello sayfasının Yapıştır hello HiveQL ifadelerini hello çalışma sayfasına aşağıdaki bölümü:
   
        SHOW TABLES;
   
   > [!NOTE]
   > Hive noktalı virgül gerektirmektedir.       
   > 
   > 
5. **Yürüt**’e tıklayın. A **sorgu işleminin sonuçları** bölümü sorgu Düzenleyicisi'ni hello altında görünür ve hello işi hakkındaki bilgileri görüntüler. 
   
    Merhaba sorgu tamamladığında hello **sorgu işleminin sonuçları** bölümü hello işlemi hello sonuçlarını görüntüler. **hivesampletable** adlı bir tablo görürsünüz. Bu örnek Hive tablosu tüm hello Hdınsight kümeleri ile birlikte gelir.
   
    ![HDInsight Hive görünümleri](./media/hdinsight-hadoop-linux-tutorial-get-started/hiveview.png "HDInsight Hive Görünümü Sorgu Düzenleyicisi").
6. Adım 4 ve 5. adım toorun hello sorgu aşağıdaki Yinele:
   
        SELECT * FROM hivesampletable;
   
   > [!TIP]
   > Not hello **Sonuçları Kaydet** açılır listede hello üst sol Merhaba **sorgu işleminin sonuçları** bölümünde; bu tooeither indirme hello sonuçlarını kullanın veya bunları tooHDInsight depolama bir CSV dosyası olarak kaydedin.
   > 
   > 
7. Tıklatın **geçmişi** tooget hello işlerin bir listesini.

Hive işini tamamladıktan sonra [hello sonuçları tooAzure SQL database veya SQL Server veritabanı dışarı](hdinsight-use-sqoop-mac-linux.md), ayrıca [Excel kullanarak hello sonuçlarını görselleştirme](hdinsight-connect-excel-power-query.md). Hdınsight'ta Hive kullanma hakkında daha fazla bilgi için bkz: [Hive ve HiveQL Hdınsight tooanalyze bir örnek Apache log4j dosyasını Hadoop ile](hdinsight-use-hive.md).

## <a name="clean-up-hello-tutorial"></a>Merhaba öğreticiyi silme
Merhaba öğreticiyi tamamladıktan sonra toodelete hello küme isteyebilirsiniz. HDInsight ile, verileriniz Azure Storage’da depolanır, böylece kullanılmadığında bir kümeyi güvenle silebilirsiniz. Ayrıca, kullanılmıyorken dahi HDInsight kümesi için sizden ücret kesilir. Merhaba ücretleri hello küme için hello ücretleri depolama birkaç katı olduğundan, bunlar kullanımda olmadığında ekonomik toodelete kümeleri mantıklıdır. 

> [!NOTE]
> Kullanarak [Azure Data Factory](hdinsight-hadoop-create-linux-clusters-adf.md), isteğe bağlı Hdınsight kümeleri oluşturma ve bir TimeToLive yapılandırma ayarı çok hello küme silme otomatik olarak. 
> 
> 

**toodelete hello küme ve/veya hello varsayılan depolama hesabı**

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Merhaba portal panosunda hello küme oluştururken kullandığınız hello kaynak grubu adı ile Merhaba kutucuğa tıklayın.
3. Tıklatın **silmek** hello hello küme ve varsayılan depolama hesabı hello; içeren kaynak dikey toodelete hello kaynak grubu, veya hello hello küme adına tıklayın **kaynakları** kutucuğuna ve ardından **Silmek** hello küme dikey. Merhaba kaynak grubunun silinmesi Not hello depolama hesabını siler. Tookeep hello depolama hesabı toodelete hello yalnızca küme belirleyin.

## <a name="troubleshoot"></a>Sorun giderme

HDInsight kümeleri oluştururken sorun yaşarsanız bkz. [erişim denetimi gereksinimleri](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Sonraki adımlar
Bu öğreticide, toocreate Linux tabanlı Hdınsight kümesi nasıl Resource Manager şablonu kullanarak ve nasıl öğrendiniz tooperform temel Hive sorguları.

Hdınsight ile verileri çözümleme hakkında daha fazla toolearn makaleler hello bakın:

* Visual Studio'dan nasıl tooperform Hive sorguları dahil, Hdınsight ile Hive kullanma hakkında daha fazla toolearn bkz [Hdınsight ile Hive kullanma][hdinsight-use-hive].
* toolearn Pig hakkında bir dilde kullanılan tootransform veri bkz [Hdınsight ile Pig kullanma][hdinsight-use-pig].
* toolearn MapReduce, hadoop'ta verileri işleyen bir şekilde toowrite programlar hakkında bkz [Hdınsight ile MapReduce kullanma][hdinsight-use-mapreduce].
* Hdınsight, Visual Studio tooanalyze verileri hello Hdınsight araçları kullanma hakkında toolearn bkz [Hdınsight için Visual Studio Hadoop araçlarını kullanmaya başlamanıza](hdinsight-hadoop-visual-studio-tools-get-started.md).

Kendi verilerinizle çalışmaya hazır toostart olduğunuz ve Hdınsight verilerini depolayan nasıl ya da Hdınsight, tooget verilerini görmek nasıl hello aşağıdaki tooknow hakkında daha fazla bilgi gerekiyor:

* HDInsight’ın Azure Depolama’yı nasıl kullandığı hakkında daha fazla bilgi için bkz. [HDInsight ile Azure Depolama kullanma](hdinsight-hadoop-use-blob-storage.md).
* Hakkında bilgi için tooupload veri tooHDInsight bkz [karşıya veri tooHDInsight][hdinsight-upload-data].

Toolearn oluşturma veya bir Hdınsight kümesi yönetme hakkında daha fazla bilgi isterseniz, hello aşağıdakilere bakın:

* Linux tabanlı Hdınsight kümenizi yönetme hakkında toolearn bkz [Ambari kullanarak Hdınsight kümelerini yönetme](hdinsight-hadoop-manage-ambari.md).
* toolearn daha seçebileceğiniz bir Hdınsight kümesi oluştururken hello seçenekleri hakkında bkz [özel seçenekleri kullanarak Linux'ta Hdınsight oluşturma](hdinsight-hadoop-provision-linux-clusters.md).
* Linux ve Hadoop hakkında bilginiz ancak tooknow hadoop'a ilişkin teknik özellikleri hello Hdınsight üzerinde istiyorsanız bkz [Linux'ta Hdınsight ile çalışma](hdinsight-hadoop-linux-information.md). Bu makale aşağıdaki gibi bilgiler sağlar:
  
  * Ambari ve WebHCat gibi hello kümesi üzerinde barındırılan hizmetlerin URL'leri
  * Hadoop dosyalarının ve örneklerin hello yerel dosya sisteminde Hello konumu
  * Merhaba varsayılan veri deposu olarak, Azure Storage (WASB) HDFS yerine Hello kullan

[1]: ../HDInsight/hdinsight-hadoop-visual-studio-tools-get-started.md

[hdinsight-provision]: hdinsight-provision-linux-clusters.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


