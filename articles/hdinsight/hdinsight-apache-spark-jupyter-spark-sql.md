---
title: "aaaCreate bir Apache Spark küme Azure Hdınsight'ta | Microsoft Docs"
description: "Hdınsight'ta bir Apache Spark toocreate küme nasıl üzerinde Hdınsight Spark hızlı başlangıç."
keywords: "spark hızlı başlangıç,etkileşimli spark,etkileşimli sorgu,hdinsight spark,azure spark"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 91f41e6a-d463-4eb4-83ef-7bbb1f4556cc
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: 002f71b3cd4fb315d4a556cebc9263026515ec4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-apache-spark-cluster-in-azure-hdinsight"></a>Azure HDInsight’ta Apache Spark kümesi oluşturma

Bu makalede, nasıl toocreate bir Apache Spark küme Azure Hdınsight'ta öğrenin. HDInsight’ta Spark hakkında daha fazla bilgi için bkz. [Genel Bakış: Azure HDInsight’ta Apache Spark](hdinsight-apache-spark-overview.md).

   ![Azure Hdınsight'ta Apache Spark kümesi adımları toocreate açıklayan hızlı başlangıç diyagramı](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-quickstart-interactive-spark-query-flow.png "Hdınsight'ta Apache Spark kullanarak Spark hızlı başlangıç. Gösterilen adımlar: küme oluşturma; etkileşimli Spark sorgusu çalıştırma")

## <a name="prerequisites"></a>Ön koşullar

* **Bir Azure aboneliği**. Bu öğreticiye başlamadan önce bir Azure aboneliğinizin olması gerekir. Bkz. [Ücretsiz Azure hesabınızı hemen oluşturun](https://azure.microsoft.com/free).

## <a name="create-hdinsight-spark-cluster"></a>HDInsight Spark kümesi oluşturma

Bu bölümde, [Azure Resource Manager şablonu](https://azure.microsoft.com/resources/templates/101-hdinsight-spark-linux/) kullanarak bir HDInsight Spark kümesi oluşturacaksınız. Diğer küme oluşturma yöntemleri için bkz. [HDInsight kümeleri oluşturma](hdinsight-hadoop-provision-linux-clusters.md).

1. Görüntü tooopen hello hello Azure portal şablonda aşağıdaki hello'ı tıklatın.         

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-spark-linux%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apache-spark-jupyter-spark-sql/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. Hello aşağıdaki değerleri girin:

    ![Azure Resource Manager şablonu kullanarak HDInsight Spark kümesi oluşturma](./media/hdinsight-apache-spark-jupyter-spark-sql/create-spark-cluster-in-hdinsight-using-azure-resource-manager-template.png "Azure Resource Manager şablonu kullanarak Spark kümesi oluşturma")

    * **Abonelik**: Bu kümeye ait Azure aboneliğinizi seçin.
    * **Kaynak grubu**: Bir kaynak grubu oluşturun veya mevcut bir kaynak grubunu seçin. Kaynak grubu kullanılan toomanage olan projelerinizi için Azure kaynakları.
    * **Konum**: hello kaynak grubu için bir konum seçin. Merhaba şablon hello kümesi de hello varsayılan küme depolama ettirilmesi oluşturmak için bu konumu kullanır.
    * **ClusterName**: toocreate istediğiniz hello Hdınsight kümesi için bir ad girin.
    * **Spark sürüm**: seçin **2.0** tooinstall hello kümede istediğiniz hello sürüm olarak.
    * **Küme oturum açma adı ve parola**: hello varsayılan oturum açma adıdır, yönetici
    * **SSH kullanıcı adı ve parola**.

   Bu değerleri not alın.  Bunları daha sonra hello öğreticide gerekir.

3. Seçin **toohello hüküm ve koşullar yukarıda belirtildiği kabul**seçin **PIN toodashboard**ve ardından **satın alma**. Şablon dağıtımı için Dağıtım gönderme başlıklı yeni bir kutucuk görürsünüz. Yaklaşık 20 dakika toocreate hello küme alır.

Hdınsight kümeleri oluşturma konusunda bir sorun alıyorsanız, hello doğru izinleri toodo böylece yok olabilir. Daha fazla bilgi için [erişim denetimi gereksinimlerine](hdinsight-administer-use-portal-linux.md#create-clusters) bakın.

> [!NOTE]
> Bu makalede kullanan bir Spark kümesi oluşturur [hello olarak Azure Storage Bloblarında küme depolama](hdinsight-hadoop-use-blob-storage.md). Kullanan bir Spark kümesi oluşturabilirsiniz [Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md) hello varsayılan depolama. Yönergeler için bkz. [Data Lake Store ile HDInsight kümesi oluşturma](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).
>
>

## <a name="run-a-hive-query-using-spark-sql"></a>Spark SQL kullanarak Hive sorgusu çalıştırma

Hdınsight Spark kümeniz için yapılandırılmış Jupyter not defteri kullandığınızda, bir hazır almak `sqlContext` Spark SQL kullanarak toorun Hive sorgularını kullanabilirsiniz. Bu bölümde, bilgi nasıl toostart Jupyter not defteri ve temel Hive sorgusu çalıştırma.

1. Açık hello [Azure portal](https://portal.azure.com/).

2. Toopin hello küme toohello Pano ettiyseniz, hello Pano toolaunch hello küme dikey penceresinden hello küme kutucuğa tıklayın.

    Merhaba sol bölmesinden hello küme toohello Pano değil sabitlerseniz tıklatın **Hdınsight kümeleri**ve ardından oluşturduğunuz hello kümesine tıklayın.

3. **Hızlı bağlantılar** bölümünde **Küme panoları**'na ve ardından **Jupyter Notebook**'a tıklayın. İstenirse, hello küme için hello yönetici kimlik bilgilerini girin.

   ![Açık Jupyter not defteri toorun etkileşimli Spark SQL sorgusu](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-open-jupyter-interactive-spark-sql-query.png "açık Jupyter not defteri toorun etkileşimli Spark SQL sorgusu")

   > [!NOTE]
   > Kümenizin açma hello tarayıcınızda URL aşağıdaki tarafından hello Jupyter Not Defteri de erişebilirsiniz. Değiştir **CLUSTERNAME** kümenizi hello adı:
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. Bir not defteri oluşturun. **Yeni** ve ardından **PySpark** seçeneğine tıklayın.

   ![Jupyter not defteri toorun etkileşimli Spark SQL sorgu oluşturma](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "Jupyter not defteri toorun etkileşimli Spark SQL sorgu oluşturma")

   Yeni bir not defteri oluşturulur ve Untitled(Untitled.pynb) hello adı ile açılır.

4. Merhaba üstünde Hello dizüstü bilgisayar adına tıklayın ve isterseniz kolay bir ad girin.

    ![Merhaba Jupter not defteri toorun etkileşimli Spark sorgu için bir ad](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-jupyter-notebook-name.png "hello Jupter not defteri toorun etkileşimli Spark sorgu için bir ad sağlayın")

5.  Yapıştır hello aşağıdaki kod boş bir hücreye ve tuşuna basarak **SHIFT + ENTER** toorun hello kodu. Aşağıdaki hello kodda `%%sql` (çağrılan hello sql Sihirli) söyler Jupyter not defteri toouse hello önceden `sqlContext` toorun hello Hive sorgusu. Merhaba sorgu hello üst 10 satır Hive tablosundan alır (**hivesampletable**) tüm Hdınsight kümeleri üzerinde varsayılan olarak kullanılabilir.

        %%sql
        SELECT * FROM hivesampletable LIMIT 10

    ![HDInsight Spark'ta Hive sorgusu](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query.png "HDInsight Spark'ta Hive sorgusu")

    Merhaba hakkında daha fazla bilgi için `%%sql` Sihirli ve hello önceden bağlamları bkz [Jupyter defterlerinde Hdınsight kümesi için kullanılabilen çekirdekler](hdinsight-apache-spark-jupyter-notebook-kernels.md).

    > [!NOTE]
    > Jupyter'de bir sorgu çalıştırmadan her zaman, web tarayıcınızın Pencere başlığında gösteren bir **(meşgul)** hello not defteri başlığı ile birlikte durum. Ayrıca dolu daire sonraki toohello bkz **PySpark** hello sağ üst köşedeki metin. Merhaba iş tamamlandıktan sonra tooa boş daire değiştirir.
    >
    >
    
6. Merhaba ekranında tooshow hello sorgu çıktısı yenilemeniz gerekir.

    ![HDInsight Spark'ta Hive sorgusu çıkışı](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query-output.png "HDInsight Spark'ta Hive sorgusu çıkışı")

7. Merhaba uygulaması çalıştıran bitirdikten sonra hello not defteri toorelease hello küme kaynaklarını kapatın. toodo çok hello **dosya** hello dizüstü menüsünde **Kapat ve Durdur**.

8. Daha sonraki bir zamanda toocomplete hello sonraki adımlar planlıyorsanız, bu makaledeki oluşturulan hello Hdınsight kümesi silme emin olun. 

    [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-step"></a>Sonraki adım 

Sorgu öğrenilen nasıl toocreate bir Hdınsight Spark küme bu makalede ve temel bir Spark SQL Çalıştır. Toohello nasıl toouse bir Hdınsight Spark küme sonraki makalede toolearn toorun etkileşimli sorgular örnek verilere ilerleyin.

> [!div class="nextstepaction"]
>[Bir HDInsight Spark kümesinde etkileşimli sorguları çalıştırma](hdinsight-apache-spark-load-data-run-query.md)



