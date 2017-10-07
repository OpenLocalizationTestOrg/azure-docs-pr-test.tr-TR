---
title: "aaaCreate Hadoop kümeleri - Azure Hdınsight bir web tarayıcısı kullanarak | Microsoft Docs"
description: "Azure Önizleme portalını hello ve nasıl toocreate Hadoop, HBase, Storm ve Spark Hdınsight için bir web tarayıcısı kullanarak Linux kümeleri öğrenin."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 697278cf-0032-4f7c-b9b2-a84c4347659e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 63027e35e2d66dd76218aff3e0c085fc811736ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-linux-based-clusters-in-hdinsight-using-hello-azure-portal"></a>Hello Azure portal kullanarak Hdınsight'ta Linux tabanlı kümelerde oluşturma
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

Hello Azure portal, hizmet ve kaynakları hello Microsoft Azure bulutta barındırılan bir web tabanlı yönetim aracıdır. Bu makalede nasıl hello portal kullanarak toocreate Linux tabanlı Hdınsight kümeleri öğreneceksiniz.

## <a name="prerequisites"></a>Ön koşullar
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* **Bir Azure aboneliği**. Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **Modern bir web tarayıcısı**. Hello Azure portal, HTML5 ve Javascript kullanır ve eski web tarayıcısında doğru şekilde çalışmayabilir.

## <a name="create-clusters"></a>Küme oluşturma
Hello Azure portal hello küme özelliklerinin çoğu kullanıma sunar. Azure Resource Manager şablonu kullanarak, çok sayıda ayrıntıları gizleyebilirsiniz. Daha fazla bilgi için bkz: [oluşturma Linux tabanlı Hadoop kümeleri Azure Resource Manager şablonları kullanarak Hdınsight'ta](hdinsight-hadoop-create-linux-clusters-arm-templates.md).

[!INCLUDE [secure-transfer-enabled-storage-account](../../includes/hdinsight-secure-transfer.md)]


1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Tıklatın  **+** , tıklatın **Intelligence + analiz**ve ardından **Hdınsight**.
   
    ![Hello Azure portalında yeni bir küme oluşturma](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster.png "hello Azure portalında yeni bir küme oluşturma")

3. Merhaba, **Hdınsight** dikey penceresinde'ı tıklatın **özel (boyutu, ayarları, uygulamalar)**, tıklatın **Temelleri**ve ardından aşağıdaki bilgilerle hello girin.

    ![Hello Azure portalında yeni bir küme oluşturma](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-basics.png "hello Azure portalında yeni bir küme oluşturma")

    * **Küme Adı** girin: Bu ad genel olarak benzersiz olmalıdır.

    * Merhaba gelen **abonelik** açılan listesinde, select hello hello küme için kullanılacak Azure aboneliği.

    * Tıklatın **küme türü**ve ardından seçin:
   
        * **Küme türü**: hangi toochoose bilmiyorsanız seçin **Hadoop**. Merhaba en popüler küme türü budur.
     
            > [!IMPORTANT]
            > Hdınsight kümeleri gelen toohello iş yükü karşılık türleri çeşitli veya için küme hello teknolojisi ayarlanmış. Bir küme üzerinde Storm ve HBase gibi birden çok tür birleştiren bir küme için desteklenen yöntem toocreate yoktur. 
            > 
            > 
        
        * **İşletim Sistemi**: **Linux** seçeneğini belirleyin.
        
        * **Sürüm**: hangi toochoose bilmiyorsanız hello varsayılan sürümü kullanın. Daha fazla bilgi için bkz. [HDInsight küme sürümleri](hdinsight-component-versioning.md).
        * **Küme katmanı**: Azure Hdınsight iki kategoride hello büyük veri Bulutu teklifleri sunar: standart katmanı ve Premium katmanı. Daha fazla bilgi için bkz. [Küme katmanları](hdinsight-hadoop-provision-linux-clusters.md#cluster-tiers).

    * İçin **küme oturum açma kullanıcı** ve **küme oturum açma parolasını**, hello kullanıcı adını ve hello yönetici kullanıcı için parola sağlayın.

    * Girin bir **SSH kullanıcı adı** ve aynı yönetici parolasını daha önce belirttiğiniz hello toohave hello SSH parolası istiyorsanız hello seçin **küme oturum açma aynı parolayı kullanın** onay kutusu. Değilse, ya da sağlayan bir **parola** veya **ortak anahtar**, kullanılan tooauthenticate hello SSH kullanıcı olacaktır. Ortak anahtar kullanılması önerilen yaklaşımı hello ' dir. Tıklatın **seçin** hello alt toosave hello kimlik bilgileri yapılandırması sırasında.
   
        Bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

    * İçin **kaynak grubu**, toocreate yeni bir kaynak grubu istediğiniz veya var olanı Kullan olup olmadığını belirtin.

    * Bir veri merkezi belirtin **konumu** burada hello küme oluşturulur.

    * **İleri**’ye tıklayın.

4. Merhaba üzerinde **depolama** dikey penceresinde, varsayılan depolama alanı olarak Azure Storage (WASB) veya Data Lake Store istediğinizi belirtin. Daha fazla bilgi için aşağıdaki hello tabloya bakın.

    ![Hello Azure portalında yeni bir küme oluşturma](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-storage.png "hello Azure portalında yeni bir küme oluşturma")

    | Depolama                                      | Açıklama |
    |----------------------------------------------|-------------|
    | **Azure Storage Bloblarında varsayılan depolama**   | <ul><li>İçin **birincil depolama türü**seçin **Azure Storage**. Bundan sonra için **seçim yöntemini**, seçebileceğiniz **My abonelikleri** toospecify, Azure aboneliğinizin bir parçası olan bir depolama hesabını ve ardından hello depolama hesabı istiyorsanız. Aksi takdirde tıklatın **erişim tuşu** ve Azure aboneliğiniz dışında toochoose gelen istediğiniz hello depolama hesabı için hello bilgileri sağlayın.</li><li>İçin **varsayılan kapsayıcı**, hello portal tarafından önerilen hello varsayılan kapsayıcı adıyla toogo seçin ya da kendi belirtin.</li><li>Varsayılan depolama alanı olarak WASB kullanıyorsanız (isteğe bağlı) tıklayabilirsiniz **ek depolama hesapları** toospecify ek depolama hesapları hello kümesi ile tooassociate. Merhaba, **Azure depolama anahtarları** dikey penceresinde tıklatın **depolama anahtarı eklemek**, ve ardından, bir depolama hesabı, Azure aboneliklerinize veya diğer abonelikler (Merhaba depolama hesabı sağlayarak sağlayabilir erişim anahtarı).</li><li>Varsayılan depolama alanı olarak WASB kullanıyorsanız (isteğe bağlı) tıklayabilirsiniz **Data Lake Store erişim** toospecify ek depolama alanı olarak Azure Data Lake Store. Daha fazla bilgi için bkz: [Azure Portal'ı kullanarak Data Lake Store ile bir Hdınsight kümesi oluşturmayı](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</li></ul> |
    | **Azure Data Lake Store varsayılan depolama** | İçin **birincil depolama türü**seçin **Data Lake Store** toohello makalesine başvurun [Azure Portal'ı kullanarak Data Lake Store ile bir Hdınsight kümesi oluşturmayı](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md) için yönergeler. |
    | **Dış meta deponuz**                      | İsteğe bağlı olarak, hello kümesi ile ilişkili bir SQL veritabanı toosave Hive ve Oozie meta verileri belirtebilirsiniz. İçin **bir SQL veritabanı için Hive seçin** bir SQL veritabanını seçin ve ardından hello veritabanı için hello kullanıcı adı/parola sağlayın. Oozie meta verileri için bu adımları yineleyin.<br><br>Azure SQL veritabanı için meta deponuz kullanırken bazı noktalar. <ul><li>Merhaba meta depo için kullanılan hello Azure SQL veritabanı bağlantısı tooother Azure Hdınsight dahil olmak üzere Azure hizmetlerinin izin vermeniz gerekir. Merhaba sağ tarafındaki hello Azure SQL veritabanı panosundaki hello sunucu adına tıklayın. Bu hangi hello SQL veritabanı örneğinin çalıştığından hello sunucusudur. Hello sunucu görünümünde olduktan sonra tıklatın **yapılandırma**ve ardından **Azure Hizmetleri**, tıklatın **Evet**ve ardından **kaydetmek**.</li><li>Bu hello küme oluşturma işlemi toofail neden bir meta depo oluştururken, kısa çizgi veya kısa çizgi, içeren bir veritabanı adı kullanmayın.</li></ul>                                                                                                                                                                       |

    **İleri**’ye tıklayın. 

    > [!WARNING]
    > Merhaba Hdınsight kümesi farklı bir konumda bir ek depolama alanı hesabı kullanarak desteklenmiyor.

5. İsteğe bağlı olarak, tıklayın **uygulamaları** Hdınsight kümeleri ile çalışma tooinstall uygulamalar. Bu uygulamalar Microsoft veya bağımsız yazılım satıcıları (ISV) tarafından ya da sizin tarafınızdan geliştirilebilir. Daha fazla bilgi için bkz: [yükleme Hdınsight uygulamaları](hdinsight-apps-install-applications.md#install-applications-during-cluster-creation).


6. Tıklatın **küme boyutu** bu küme için oluşturulan hello düğümleri hakkında toodisplay bilgi. Merhaba hello küme için gereksinim duyduğunuz çalışan düğümü sayısını ayarlayın. Merhaba hello küme maliyetini hello Dikey içinde gösterilecek tahmin.
   
    ![Düğüm fiyatlandırma katmanları dikey](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-nodes.png "Küme düğüm sayısını belirtin")
   
   > [!IMPORTANT]
   > 32'den fazla çalışan düğümlerine planlıyorsanız, küme oluşturma sırasında veya bir baş düğüm boyutu en az 8 çekirdek ve 14 GB ile seçmelisiniz sonra hello Küme oluşturulduktan sonra ölçeklendirme ram.
   > 
   > Düğümü boyutları ve ilişkili maliyetler hakkında daha fazla bilgi için bkz: [Hdınsight fiyatlandırma](https://azure.microsoft.com/pricing/details/hdinsight/).
   > 
   > 
   
   Tıklatın **sonraki** yapılandırma fiyatlandırma toosave hello düğümü.

7. Tıklatın **Gelişmiş ayarları** tooconfigure kullanarak gibi diğer isteğe bağlı ayarlar **betik eylemleri** toocustomize küme tooinstall özel bileşenler veya birleştirme bir **sanal ağ**. Daha fazla bilgi için aşağıdaki hello tabloya bakın.

    ![Düğüm fiyatlandırma katmanları dikey](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-advanced.png "Küme düğüm sayısını belirtin")

    | Seçenek | Açıklama |
    |--------|-------------|
    | **Betik eylemleri** | Özel bir komut dosyası toocustomize bir küme toouse istiyorsanız hello küme oluşturulduğunda bu seçeneği kullanın. Betik eylemleri hakkında daha fazla bilgi için bkz: [özelleştirme Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster-linux.md). |
    | **Sanal Ağ** | Bir sanal ağ tooplace hello kümesine istiyorsanız bir Azure sanal ağ ve hello alt ağ seçin. Bir ağla sanal hello sanal ağ için belirli yapılandırma gereksinimlerini de dahil olmak üzere, Hdınsight kullanma hakkında bilgi için bkz: [bir Azure sanal ağı kullanarak genişletme Hdınsight yetenekleri](hdinsight-extend-hadoop-virtual-network.md). |

    **İleri**’ye tıklayın.

8. Merhaba üzerinde **Özet** dikey penceresinde, daha önce girdiğiniz hello bilgileri doğrulayın ve ardından **oluşturma**.

    ![Düğüm fiyatlandırma katmanları dikey](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-summary.png "Küme düğüm sayısını belirtin")
    
    > [!NOTE]
    > Bu, genellikle yaklaşık 15 dakika oluşturulan hello küme toobe için biraz zaman alabilir. Merhaba döşeme Sabitle hello üzerinde kullanın ya da hello **bildirimleri** hello girişinde sol hello sayfa toocheck sağlama işlemi hello üzerinde.
    > 
    > 
12. Merhaba oluşturma işlemi tamamlandıktan sonra hello Sabitle toolaunch hello küme dikey penceresinde hello kümeden için hello kutucuğa tıklayın. Merhaba küme dikey penceresinde aşağıdaki bilgilerle hello sağlar.
    
    ![Küme dikey](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-completed.png "küme özellikleri")
    
    Bu dikey pencerenin hello üstünde toounderstand hello simgeleri aşağıdaki hello kullanın.
    
    * **Genel Bakış** sekmesi tüm hello hello adı, ait olduğu için hello konumu, hello işletim sistemi, hello küme Panosu, vb. için URL hello kaynak grubu gibi hello küme hakkında önemli bilgiler sağlar.
    * **Pano** hello kümesi ile ilişkili toohello Ambari portal yönlendirir.
    * **Kabuk güvenli**: tooaccess hello küme SSH kullanarak gerekli bilgiler.
    * **Ölçek kümesi** hello hello kümesi ile ilişkili çalışan düğümü sayısını artırmak sağlar.
    * **Silme**: siler hello Hdınsight kümesi.
    

## <a name="customize-clusters"></a>Kümeleri özelleştirme
* Bkz: [önyükleme kullanarak özelleştirme Hdınsight kümelerini](hdinsight-hadoop-customize-cluster-bootstrap.md).
* Bkz: [özelleştirme Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster-linux.md).

## <a name="delete-hello-cluster"></a>Merhaba küme silme
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a>Sorun giderme

HDInsight kümeleri oluştururken sorun yaşarsanız bkz. [erişim denetimi gereksinimleri](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Sonraki adımlar
Hdınsight kümesi başarıyla oluşturuldu, toolearn nasıl aşağıdaki hello kullan toowork kümenizi ile:

### <a name="hadoop-clusters"></a>Hadoop kümeleri
* [HDInsight ile Hive kullanma](hdinsight-use-hive.md)
* [HDInsight ile Pig kullanma](hdinsight-use-pig.md)
* [Hdınsight ile MapReduce kullanma](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a>HBase kümeleri
* [Hdınsight'ta HBase kullanmaya başlama](hdinsight-hbase-tutorial-get-started-linux.md)
* [Hdınsight'ta HBase için Java uygulamaları geliştirme](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a>Storm kümeleri
* [Hdınsight üzerinde Storm için Java topolojisi geliştirme](hdinsight-storm-develop-java-topology.md)
* [Hdınsight üzerinde Storm Python bileşenleri kullanma](hdinsight-storm-develop-python-topology.md)
* [Dağıtma ve hdınsight'ta Storm topolojileri izleme](hdinsight-storm-deploy-monitor-topology-linux.md)

### <a name="spark-clusters"></a>Spark kümeleri
* [Scala kullanarak tek başına uygulama oluşturma](hdinsight-apache-spark-create-standalone-application.md)
* [Livy kullanarak Spark kümesinde işleri uzaktan çalıştırma](hdinsight-apache-spark-livy-rest-interface.md)
* [BI ile Spark: BI araçlarıyla HDInsight’ta Spark kullanarak etkileşimli veri çözümlemesi gerçekleştirme](hdinsight-apache-spark-use-bi-tools.md)
* [Machine Learning ile Spark: Spark Hdınsight toopredict yemek İnceleme sonuçlarını içinde kullanma](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Spark Akış: Gerçek zamanlı akış uygulamaları oluşturmak için HDInsight’ta Spark kullanma](hdinsight-apache-spark-eventhub-streaming.md)

