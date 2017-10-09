---
title: "Azure portal kullanarak Hdınsight'ta aaaManage Windows tabanlı Hadoop kümeleri hello | Microsoft Docs"
description: "Bilgi nasıl tooadminister Hdınsight hizmeti. Bir Hdınsight kümesi, açık hello etkileşimli JavaScript konsolu ve açık hello Hadoop komut konsolundan oluşturun."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 9295a988-bd88-453a-8c8b-55fa103bf39c
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: a237726b0e37a08005ce22e96581739e93edb050
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-windows-based-hadoop-clusters-in-hdinsight-by-using-hello-azure-portal"></a>Windows tabanlı Hadoop kümeleri hdınsight'ta hello Azure portal kullanarak yönetme

Hello kullanarak [Azure portal][azure-portal], Azure Hdınsight'ta Windows tabanlı Hadoop kümeleri oluşturma, Hadoop kullanıcı parolası değiştirme ve etkinleştirme Uzak Masaüstü Protokolü (RDP), erişebilmesi için Hadoop hello Merhaba küme konsolda komutu.

Bu makaledeki Hello bilgiler yalnızca tooWindow tabanlı Hdınsight kümeleri geçerlidir. Linux tabanlı kümelerde yönetme hakkında daha fazla bilgi için bkz: [kullanarak yönetmek Hadoop kümeleri hdınsight'ta Azure portalına hello](hdinsight-administer-use-portal-linux.md).

> [!IMPORTANT]
> Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).


## <a name="prerequisites"></a>Ön koşullar

Bu makaleye başlamadan önce hello şunlara sahip olmanız gerekir:

* **Bir Azure aboneliği**. Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **Azure depolama hesabı** -bir Hdınsight kümesi bir Azure Blob Depolama kapsayıcısını hello varsayılan dosya sistemi olarak kullanır. Azure Blob storage Hdınsight kümeleri ile sorunsuz bir deneyim nasıl sağladığını hakkında daha fazla bilgi için bkz: [kullanım Azure Blob Storage Hdınsight ile](hdinsight-hadoop-use-blob-storage.md). Bir Azure Storage hesabı oluşturma hakkında daha fazla bilgi için bkz: [nasıl tooCreate bir depolama hesabı](../storage/common/storage-create-storage-account.md).

## <a name="open-hello-portal"></a>Merhaba Portal açın
1. Çok oturum[https://portal.azure.com](https://portal.azure.com).
2. Merhaba portal açtıktan sonra şunları yapabilirsiniz:

   * Tıklatın **yeni** hello soldaki menüden toocreate yeni bir küme gelen:

       ![Yeni Hdınsight küme düğmesi](./media/hdinsight-administer-use-management-portal/azure-portal-new-button.png)
   * Tıklatın **Hdınsight kümeleri** hello sol menüden.

       ![Azure portal Hdınsight küme düğmesi](./media/hdinsight-administer-use-management-portal/azure-portal-hdinsight-button.png)

     Varsa **Hdınsight** hello soldaki menüde görünür değil'ye tıklayın **Gözat**.

     ![Azure portal gözatma küme düğmesi](./media/hdinsight-administer-use-management-portal/azure-portal-browse-button.png)

## <a name="create-clusters"></a>Küme oluşturma
Merhaba Portal kullanarak hello oluşturma yönergeleri için bkz: [Hdınsight kümeleri oluşturma](hdinsight-hadoop-provision-linux-clusters.md).

Hdınsight geniş Hadoop bileşenleri ile çalışır. Doğrulandı ve desteklenen hello bileşenler Hello listesi için bkz [hangi sürümüdür Azure Hdınsight'ta hadoop](hdinsight-component-versioning.md). Seçenekler aşağıdaki hello birini kullanarak Hdınsight özelleştirebilirsiniz:

* Bir küme tooeither özelleştirebileceğiniz betik eylemi toorun özel komut dosyası kullanma küme yapılandırmasını değiştirmek veya Giraph veya Solr gibi özel bileşenlerini yükleyin. Daha fazla bilgi için bkz: [betik eylemi kullanarak özelleştirme Hdınsight kümesi](hdinsight-hadoop-customize-cluster.md).
* Küme oluşturma sırasında Hello küme özelleştirme parametreleri hello Hdınsight .NET SDK veya Azure PowerShell kullanın. Bu yapılandırma değişikliklerini hello küme hello ömrü sonra korunur ve Azure platformu düzenli olarak bakımını gerçekleştirir küme düğümü reimages etkilenmez. Hello küme özelleştirme parametreleri kullanma hakkında daha fazla bilgi için bkz: [Hdınsight kümeleri oluşturma](hdinsight-hadoop-provision-linux-clusters.md).
* Mahout ve basamaklama, gibi yerel bazı Java bileşenleri hello kümede JAR dosyaları olarak çalıştırabilirsiniz. Bu JAR dosyalarını dağıtılmış tooAzure Blob Depolama olabilir ve tooHDInsight kümeleri Hadoop iş gönderme mekanizmalar aracılığıyla gönderilir. Daha fazla bilgi için bkz: [gönderme Hadoop işleri program aracılığıyla](hdinsight-submit-hadoop-jobs-programmatically.md).

  > [!NOTE]
  > Hdınsight kümelerinde JAR dosyalarını çağırma başvurun veya JAR dosyalarını tooHDInsight kümelerini dağıtma sorunları varsa [Microsoft Support](https://azure.microsoft.com/support/options/).
  >
  > Geçişli Hdınsight tarafından desteklenmiyor ve Microsoft Support uygun değil. Desteklenen bileşenlerin bir listesi için bkz: [Hdınsight tarafından sağlanan hello küme sürümlerindeki yenilikler](hdinsight-component-versioning.md).
  >
  >

Uzak Masaüstü bağlantısı kullanarak hello kümede özel yazılım yüklemesi desteklenmez. Toore ihtiyacınız varsa bunlar kaybolur gibi hello sürücülerinde hello baş düğümü, herhangi bir dosya depolama kaçınmalısınız-hello kümeleri oluşturma. Azure Blob Depolama dosyalarda depolamanızı öneririz. BLOB Depolama kalıcıdır.

## <a name="list-and-show-clusters"></a>Liste ve kümeleri Göster
1. Çok oturum[https://portal.azure.com](https://portal.azure.com).
2. Tıklatın **Hdınsight kümeleri** hello sol menüden.
3. Merhaba küme adına tıklayın. Merhaba küme listesi uzunsa hello sayfa hello üstündeki filtresini kullanabilirsiniz.
4. Merhaba listesi tooshow hello ayrıntılarını kümeden çift tıklayın.

    **Menü ve essentials**:

    ![Azure portal Hdınsight küme temelleri](./media/hdinsight-administer-use-management-portal/hdinsight-essentials.png)

   * toocustomize hello menüsünde, başlangıç menüsünde herhangi bir yere sağ tıklayın ve ardından **Özelleştir**.
   * **Ayarları** ve **tüm ayarları**: görüntüler hello **ayarları** tooaccess sağlayan hello küme dikey penceresinde hello küme için yapılandırma bilgilerini ayrıntılı.
   * **Pano**, **küme Panosu** ve **URL: Linux tabanlı kümeler için Ambari Web olan tüm yolları tooaccess hello küme Panosu, bunlar. -**Güvenli Kabuk **: Hello yönergeleri tooconnect toohello küme güvenli Kabuk (SSH) bağlantısı kullanarak gösterir.
   * **Küme ölçeklendirme**: Bu küme için toochange hello çalışan düğümü sayısını sağlar.
   * **Silme**: hello küme siler.
   * **Hızlı Başlangıç**: yardımcı olacak bilgileri görüntüler, Hdınsight kullanarak başlayın.
   * ** Kullanıcıları: tooset izinlerini verir *portal Yönetim* diğer kullanıcılar için bu kümenin, Azure aboneliğinizin üzerinde.

     > [!IMPORTANT]
     > Bu *yalnızca* hello Azure portalına erişim ve izinleri toothis kümede etkiler ve tooor gönderme işleri toohello Hdınsight kümesi bağlanan üzerinde hiçbir etkisi olmaz.
     >
     >
   * **Etiketler**: etiketleri bulut hizmetlerinizi, özel bir sınıflandırma, tooset anahtar/değer çiftleri toodefine izin. Örneğin, adlı bir anahtar oluşturabilir **proje**ve ardından belirli bir projeyle ilişkili tüm hizmetler için ortak bir değer kullanın.
   * **Ambari görünümleri**: tooAmbari Web bağlar.

     > [!IMPORTANT]
     > toomanage hello Hizmetleri Hdınsight kümesi hello tarafından sağlanan, Ambari REST API hello veya Ambari Web kullanmanız gerekir. Ambari kullanarak daha fazla bilgi için bkz: [Ambari kullanarak Hdınsight kümelerini yönetme](hdinsight-hadoop-manage-ambari.md).
     >
     >

     **Kullanım**:

     ![Azure portal Hdınsight küme kullanımı](./media/hdinsight-administer-use-management-portal/hdinsight-portal-cluster-usage.png)
5. Tıklatın **ayarları**.

    ![Azure portal Hdınsight küme kullanımı](./media/hdinsight-administer-use-management-portal/hdinsight.portal.cluster.settings.png)

   * **Özellikleri**: hello küme özelliklerini görüntüleyin.
   * **Küme AAD kimlik**:
   * **Azure depolama anahtarları**: hello varsayılan depolama hesabı ve anahtarını görüntüleyin. Merhaba depolama hesabı hello küme oluşturma işlemi sırasında bir yapılandırmadır.
   * **Oturum açma küme**: hello küme HTTP kullanıcı adınızı ve parolanızı değiştirin.
   * **Dış meta deponuz**: hello Hive ve Oozie meta deponuz görüntüleyin. Merhaba meta deponuz yalnızca hello küme oluşturma işlemi sırasında yapılandırılabilir.
   * **Küme ölçeklendirme**: artırma ve azaltma hello küme çalışan düğüm sayısı.
   * **Uzak Masaüstü**: etkinleştirmek ve Uzak Masaüstü (RDP) erişimi devre dışı bırakın ve hello RDP kullanıcı adı yapılandırın.  Merhaba RDP kullanıcı adı hello HTTP kullanıcı adından farklı olmalıdır.
   * **Kayıtlı iş ortağı**:

     > [!NOTE]
     > Bu, kullanılabilir ayarlar genel bir listesi verilmiştir; tümünü değil, tüm küme türleri için mevcut olacaktır.
     >
     >
6. Tıklatın **özellikleri**:

    Merhaba özellikler bölümü hello aşağıdakiler yer alır:

   * **Ana bilgisayar adı**: küme adı.
   * **Küme URL**.
   * **Durum**: dahil, kabul iptal ClusterStorageProvisioned, AzureVMConfiguration, çalıştığından, silme, hatası, HDInsightConfiguration, işletimsel, silinen, süresi sona erdi, DeleteQueued, DeleteTimedout, DeleteError, PatchQueued, CertRolloverQueued, ResizeQueued, ClusterCustomization
   * **Bölge**: Azure konumu. Merhaba desteklenen Azure konumu listesi için bkz **bölge** açılan liste kutusunu [Hdınsight fiyatlandırma](https://azure.microsoft.com/pricing/details/hdinsight/).
   * **Oluşturulan veri**.
   * **İşletim sistemi**: ya da **Windows** veya **Linux**.
   * **Tür**: Hadoop, HBase, Storm, Spark.
   * **Sürüm**. Bkz: [Hdınsight sürümleri](hdinsight-component-versioning.md)
   * **Abonelik**: Abonelik adı.
   * **Abonelik kimliği**.
   * **Birincil veri kaynağını**. Hello Azure Blob Depolama hesabı Hadoop dosya sistemi hello varsayılan olarak kullanılır.
   * **Çalışan düğüm fiyatlandırma katmanı**.
   * **Baş düğüm fiyatlandırma katmanı**.

## <a name="delete-clusters"></a>Küme silme
Bir küme silme hello varsayılan depolama hesabı ya da bağlı tüm depolama hesaplarını silmez. Merhaba küme kullanarak yeniden oluşturabileceğiniz hello aynı depolama hesapları ve hello aynı meta depolar.

1. İçinde toohello oturum [Portal][azure-portal].
2. Tıklatın **tümüne Gözat** hello sol menüden **Hdınsight kümeleri**, küme adına tıklayın.
3. Tıklatın **silmek** hello üst menüsünden ve hello yönergeleri izleyin.

Ayrıca bkz. [Duraklat/kümeleri kapatma](#pauseshut-down-clusters).

## <a name="scale-clusters"></a>Kümeleri ölçeklendirme
özellik ölçeklendirme hello küme toochange hello Azure Hdınsight'ta toore gerek kalmadan çalışan bir küme tarafından kullanılan çalışan düğüm sayısı sağlar-hello kümesi oluşturun.

> [!NOTE]
> Yalnızca, Hdınsight sürüm 3.1.3 ile kümeleri veya üzeri desteklenir. Kümenizin hello sürümü değilseniz hello özellikler sayfasını kontrol edebilirsiniz.  Bkz: [listesi ve Göster kümeleri](#list-and-show-clusters).
>
>

hello etkisini, her tür Hdınsight tarafından desteklenen küme için veri düğümünün hello numarasını değiştirmek için:

* Hadoop

    Sorunsuz bir şekilde hello tüm bekleyen veya çalışan işler etkilemeden çalıştıran bir Hadoop kümesinde çalışan düğümü sayısını da artırabilirsiniz. Merhaba işlemi devam ederken yeni işleri da gönderilebilir. Böylece Hello küme her zaman işlevsel bir durumda bırakılır bir ölçeklendirme işlemi hatalar düzgün bir şekilde ele alınır.

    Bir Hadoop kümesine veri düğümlerini hello sayısını azaltarak ölçeklendirilir, bazı hello kümedeki hello hizmetleri yeniden başlatılır. Bu, tüm çalışan ve işleri toofail hello tamamlanma işlemi ölçeklendirme Merhaba, bekleyen neden olur. Hello işlemi tamamlandıktan sonra ancak, hello sunmaları olabilir.
* HBase

    Sorunsuz bir şekilde ekleme veya düğümleri tooyour HBase kümesi çalışırken kaldırın. Bölgesel sunucuları işlemi ölçeklendirme hello tamamladıktan birkaç dakika içinde otomatik olarak dengeli. Ancak, küme ve komutlar bir komut istemi penceresinden aşağıdaki çalışan hello hello headnode açarak el ile de hello bölgesel sunucular dengeleyebilirsiniz:

        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer

    Merhaba HBase Kabuğu'nu kullanarak daha fazla bilgi için bkz:]
* Storm

    Sorunsuz bir şekilde ekleyebilir veya çalışırken veri düğümleri tooyour Storm kümesi kaldırabilirsiniz. Ancak hello ölçekleme işlemi başarıyla tamamlandıktan sonra toorebalance hello topoloji gerekir.

    İki yolla yeniden dengelenmesi gerçekleştirilebilir:

  * Storm web kullanıcı Arabirimi
  * Komut satırı arabirimi (CLI) aracı

    Lütfen toohello bakın [Apache Storm belgelerine](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) daha fazla ayrıntı için.

    Merhaba Storm web kullanıcı Arabirimi hello Hdınsight kümesinde kullanılabilir:

    ![Hdınsight storm ölçek yeniden dengeleyin](./media/hdinsight-administer-use-management-portal/hdinsight-portal-scale-cluster-storm-rebalance.png)

    Örneği nasıl toouse hello CLI komutu toorebalance hello Storm topolojisini:

        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

**tooscale kümeleri**

1. İçinde toohello oturum [Portal][azure-portal].
2. Tıklatın **tümüne Gözat** hello sol menüden **Hdınsight kümeleri**, küme adına tıklayın.
3. Tıklatın **ayarları** hello üst menüsünden ve ardından **ölçekte küme**.
4. Girin **sayı, alt düğümleri**. Merhaba küme düğümü hello sayısı Azure abonelikleri arasında değişiklik gösterir. Faturalama desteği tooincrease hello sınırı başvurabilirsiniz.  Merhaba maliyet bilgileri toohello düğüm sayısını yapmış olduğunuz hello değişiklikleri yansıtır.

    ![Hdınsight Hadoop HBase Storm Spark ölçek](./media/hdinsight-administer-use-management-portal/hdinsight.portal.scale.cluster.png)

## <a name="pauseshut-down-clusters"></a>Kümeleri Duraklat/kapatma
Hadoop işlerinin çoğu yalnızca toplu işleri bazen çalışan ' dir. Çoğu Hadoop kümeleri için büyük nokta vardır süresini bu hello küme işleme için kullanılmayan. HDInsight ile, verileriniz Azure Storage’da depolanır, böylece kullanılmadığında bir kümeyi güvenle silebilirsiniz.
Ayrıca, kullanılmıyorken dahi HDInsight kümesi için sizden ücret kesilir. Merhaba ücretleri hello küme için hello ücretleri depolama birkaç katı olduğundan, bunlar kullanımda olmadığında ekonomik toodelete kümeleri mantıklıdır.

Merhaba işlem programı birçok yolu vardır:

* Kullanıcı Azure Data Factory. Bkz: [Azure Hdınsight bağlı hizmeti](../data-factory/data-factory-compute-linked-services.md) ve [dönüştürme ve Azure Data Factory kullanarak Analiz](../data-factory/data-factory-data-transformation-activities.md) Hizmetleri için isteğe bağlı ve otomatik olarak tanımlanan Hdınsight bağlı.
* Azure PowerShell kullanın.  Bkz: [uçuş gecikme verilerini çözümleme](hdinsight-analyze-flight-delay-data.md).
* Azure CLI kullanın. Bkz: [Azure CLI kullanarak Hdınsight kümelerini yönetme](hdinsight-administer-use-command-line.md).
* Hdınsight .NET SDK'yı kullanın. Bkz: [gönderme Hadoop işlerini](hdinsight-submit-hadoop-jobs-programmatically.md).

Fiyatlandırma bilgileri hello için bkz: [Hdınsight fiyatlandırma](https://azure.microsoft.com/pricing/details/hdinsight/). toodelete hello Portal, bir kümeden bkz [küme silme](#delete-clusters)

## <a name="change-cluster-username"></a>Değişiklik kümesi kullanıcı adı
Hdınsight kümesi, iki kullanıcı hesapları olabilir. Merhaba Hdınsight küme kullanıcı hesabı hello oluşturma işlemi sırasında oluşturulur. RDP aracılığıyla hello küme erişmek için bir RDP kullanıcı hesabı da oluşturabilirsiniz. Bkz: [etkinleştir Uzak Masaüstü](#connect-to-hdinsight-clusters-by-using-rdp).

**toochange hello Hdınsight küme kullanıcı adı ve parola**

1. İçinde toohello oturum [Portal][azure-portal].
2. Tıklatın **tümüne Gözat** hello sol menüden **Hdınsight kümeleri**, küme adına tıklayın.
3. Tıklatın **ayarları** hello üst menüsünden ve ardından **küme oturum açma**.
4. Varsa **küme oturum açma** bırakıldı etkin'ı tıklatmalısınız **devre dışı**ve ardından **etkinleştirmek** hello kullanıcı adı ve parola değiştirmeden önce...
5. Değişiklik hello **küme oturum açma adı** ve/veya hello **küme oturum açma parolasını**ve ardından **kaydetmek**.

    ![Hdınsight küme, kullanıcı, kullanıcı adı, parola, http, kullanıcı değiştirme](./media/hdinsight-administer-use-management-portal/hdinsight.portal.change.username.password.png)

## <a name="grantrevoke-access"></a>GRANT/revoke erişim
Hdınsight kümeleri HTTP web Hizmetleri (Bu hizmetlerin tümü için RESTful uç noktaları vardır) aşağıdaki hello vardır:

* ODBC
* JDBC
* Ambari
* Oozie
* Templeton

Varsayılan olarak, bu hizmetleri için erişim verilir. İptal etme/hello erişim hello Azure portal ' sağlayıcısını.

> [!NOTE]
> Verme/hello erişimi iptal ederek, hello küme kullanıcı adı ve parola sıfırlanır.
>
>

**toogrant/revoke HTTP web hizmetleri erişimi**

1. İçinde toohello oturum [Portal][azure-portal].
2. Tıklatın **tümüne Gözat** hello sol menüden **Hdınsight kümeleri**, küme adına tıklayın.
3. Tıklatın **ayarları** hello üst menüsünden ve ardından **küme oturum açma**.
4. Varsa **küme oturum açma** bırakıldı etkin'ı tıklatmalısınız **devre dışı**ve ardından **etkinleştirmek** hello kullanıcı adı ve parola değiştirmeden önce...
5. İçin **küme oturum açma kullanıcı** ve **küme oturum açma parolasını**, hello yeni bir kullanıcı adı ve parola hello küme için (sırasıyla) girin.
6. **KAYDET**'e tıklayın.

    ![Hdınsight genel http web hizmeti erişimi Kaldır](./media/hdinsight-administer-use-management-portal/hdinsight.portal.change.username.password.png)

## <a name="find-hello-default-storage-account"></a>Merhaba varsayılan depolama hesabı bulunamadı
Her Hdınsight kümesinde bir varsayılan depolama hesabı vardır. Merhaba varsayılan depolama hesabı ve alt anahtarları altında bir küme görünür **ayarları**/**özellikleri**/**Azure depolama anahtarları**. Bkz: [listesi ve Göster kümeleri](#list-and-show-clusters).

## <a name="find-hello-resource-group"></a>Merhaba kaynak grup bulunamıyor
Hello Azure Kaynak Yöneticisi modunda her Hdınsight kümesi içeren bir Azure kaynak grubu oluşturulur. bir küme içinde tooappears ait hello Azure kaynak grubu:

* Merhaba küme listesi olan bir **kaynak grubu** sütun.
* Küme **temel** döşeme.  

Bkz: [listesi ve Göster kümeleri](#list-and-show-clusters).

## <a name="open-hdinsight-query-console"></a>Hdınsight sorgu Konsolu'nu Aç
Merhaba Hdınsight sorgu konsol hello aşağıdaki özellikleri içerir:

* **Düzenleyici hive**: Hive işlerini göndermenin bir GUI web arabirimi.  Bkz: [kullanarak Hive sorgularını çalıştırma hello sorgu konsol](hdinsight-hadoop-use-hive-query-console.md).

    ![Hdınsight portal hive Düzenleyicisi](./media/hdinsight-administer-use-management-portal/hdinsight-hive-editor.png)
* **İş Geçmişi**: İzleyici Hadoop işler.  

    ![Hdınsight portal iş geçmişi](./media/hdinsight-administer-use-management-portal/hdinsight-job-history.png)

    Tıklatın **sorgu adı** iş özellikleri dahil olmak üzere tooshow hello ayrıntılarını **sorgu iş**, ve ** iş çıktısı. Ayrıca, hello sorgu ve hello çıktı tooyour iş istasyonu indirebilirsiniz.
* **Tarayıcı dosya**: hello varsayılan depolama hesabını bulun ve bağlantılı depolama hesapları hello.

    ![Hdınsight portal dosya tarayıcısı Gözat](./media/hdinsight-administer-use-management-portal/hdinsight-file-browser.png)

    Merhaba ekran hello  **<Account>**  hello öğesi olan bir Azure depolama hesabı türünü belirtir.  Merhaba hesap adı toobrowse hello dosyalar'ı tıklatın.
* **Hadoop UI**.

    ![Hdınsight portal Hadoop kullanıcı Arabirimi](./media/hdinsight-administer-use-management-portal/hdinsight-hadoop-ui.png)

    Gelen **Hadoop UI*, dosyalara gözatın ve günlüklerini denetleyin.
* **Yarn UI**.

    ![Hdınsight portal YARN kullanıcı Arabirimi](./media/hdinsight-administer-use-management-portal/hdinsight-yarn-ui.png)

## <a name="run-hive-queries"></a>Hive sorguları çalıştırma
Merhaba Portal, tooran Hive işlerini tıklatın **Hive Düzenleyicisi** hello Hdınsight sorgu konsol. Bkz: [açık Hdınsight sorgu konsol](#open-hdinsight-query-console).

## <a name="monitor-jobs"></a>İşleri izleme
Merhaba Portal, toomonitor işlerden tıklatın **iş geçmişi** hello Hdınsight sorgu konsol. Bkz: [açık Hdınsight sorgu konsol](#open-hdinsight-query-console).

## <a name="browse-files"></a>Gözatma dosyaları
toobrowse dosyaları hello varsayılan depolama hesabında depolanan ve bağlantılı depolama hesapları Merhaba, tıklatın **dosya tarayıcısı** hello Hdınsight sorgu konsol. Bkz: [açık Hdınsight sorgu konsol](#open-hdinsight-query-console).

Merhaba de kullanabilirsiniz **Gözat hello dosya sistemi** yardımcı programı'ndan hello **Hadoop UI** hello Hdınsight konsolunda.  Bkz: [açık Hdınsight sorgu konsol](#open-hdinsight-query-console).

## <a name="monitor-cluster-usage"></a>Küme kullanımını izleme
Merhaba **kullanım** hello Hdınsight kümesi dikey bölümünü hello toothis küme ve bulundukları nasıl ayrılan çekirdek sayısı yanı sıra, Hdınsight ile kullanmak için çekirdek kullanılabilir tooyour abonelik hello sayısı hakkında bilgileri görüntüler Bu küme içindeki hello düğümler için ayrılmış. Bkz: [listesi ve Göster kümeleri](#list-and-show-clusters).

> [!IMPORTANT]
> toomonitor hello Hizmetleri Hdınsight kümesi hello tarafından sağlanan, Ambari REST API hello veya Ambari Web kullanmanız gerekir. Ambari kullanarak daha fazla bilgi için bkz: [Ambari kullanarak Hdınsight kümelerini yönetme](hdinsight-hadoop-manage-ambari.md)
>
>

## <a name="open-hadoop-ui"></a>Hadoop kullanıcı arabirimini açın
toomonitor hello küme, Gözat hello dosya sistemi ve onay günlükleri, **Hadoop UI** hello Hdınsight sorgu konsol. Bkz: [açık Hdınsight sorgu konsol](#open-hdinsight-query-console).

## <a name="open-yarn-ui"></a>Yarn kullanıcı arabirimini açın
toouse Yarn kullanıcı arabirimi, tıklatın **Yarn kullanıcı Arabiriminde** hello Hdınsight sorgu konsol. Bkz: [açık Hdınsight sorgu konsol](#open-hdinsight-query-console).

## <a name="connect-tooclusters-using-rdp"></a>RDP kullanarak tooclusters Bağlan
Merhaba kimlik bilgilerini, oluşturma sırasında sağlanan hello küme toohello Hizmetleri hello küme ancak değil toohello kümenin kendisi Uzak Masaüstü aracılığıyla erişmenizi sağlar. Bir küme sağladığınızda veya bir küme sağlandıktan sonra Uzak Masaüstü erişimi kapatabilirsiniz. Oluşturma sırasında Uzak Masaüstü'nü etkinleştirme hakkında hello yönergeler için bkz: [oluşturma Hdınsight kümesi](hdinsight-hadoop-provision-linux-clusters.md).

**tooenable Uzak Masaüstü**

1. İçinde toohello oturum [Portal][azure-portal].
2. Tıklatın **tümüne Gözat** hello sol menüden **Hdınsight kümeleri**, küme adına tıklayın.
3. Tıklatın **ayarları** hello üst menüsünden ve ardından **Uzak Masaüstü**.
4. Girin **süresi**, **Uzak Masaüstü kullanıcı adı** ve **Uzak Masaüstü parola**ve ardından **etkinleştirmek**.

    ![Hdınsight etkinleştirme devre dışı bırakma, Uzak Masaüstü'nü yapılandırma](./media/hdinsight-administer-use-management-portal/hdinsight.portal.remote.desktop.png)

    Merhaba varsayılan değerleri süresi bir hafta olur.

   > [!NOTE]
   > Bir kümede hello Hdınsight .NET SDK'sı tooenable Uzak Masaüstü'nü de kullanabilirsiniz. Kullanım hello **EnableRdp** hello Hdınsight istemci şekilde aşağıdaki hello nesnesinde yöntemi: **istemci. EnableRdp (clustername, konum, "rdpuser", "rdppassword", DateTime.Now.AddDays(6))**. Benzer şekilde, Uzak Masaüstü toodisable hello kümede kullanabileceğiniz **istemci. DisableRdp (clustername, konum)**. Bu yöntemleri hakkında daha fazla bilgi için bkz: [Hdınsight .NET SDK'sı başvurusu](http://go.microsoft.com/fwlink/?LinkId=529017). Bu, yalnızca Windows üzerinde çalışan Hdınsight kümeleri için geçerlidir.
   >
   >

**RDP kullanarak tooconnect tooa küme**

1. İçinde toohello oturum [Portal][azure-portal].
2. Tıklatın **tümüne Gözat** hello sol menüden **Hdınsight kümeleri**, küme adına tıklayın.
3. Tıklatın **ayarları** hello üst menüsünden ve ardından **Uzak Masaüstü**.
4. Tıklatın **Bağlan** ve hello yönergeleri izleyin. Bağlantı devre dışı ise, önce etkinleştirmelisiniz. Merhaba Uzak Masaüstü kullanıcı adı ve parola kullanarak emin olun.  Merhaba küme kullanıcı kimlik bilgilerini kullanamazsınız.

## <a name="open-hadoop-command-line"></a>Hadoop komut satırı açın
Uzak Masaüstü'nü ve kullanım hello Hadoop komut satırını kullanarak tooconnect toohello küme, önce Uzak Masaüstü erişimi toohello küme hello önceki bölümde açıklandığı gibi etkinleştirmiş olmanız gerekir.

**tooopen Hadoop komut satırı**

1. Uzak Masaüstü kullanarak toohello kümesine bağlanın.
2. Merhaba masaüstünden çift **Hadoop komut satırı**.

    ![HDI. HadoopCommandLine][image-hadoopcommandline]

    Hadoop komutları hakkında daha fazla bilgi için bkz: [Hadoop komutları başvuru](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-common/CommandsManual.html).

Merhaba önceki ekran görüntüsünde, hello klasör adı katıştırılmış hello Hadoop sürüm numarasına sahip. Merhaba sürüm numarası hello kümeye yüklü hello Hadoop bileşenleri değiştirilen göre hello sürümü olabilir. Hadoop ortam değişkenleri toorefer toothose klasörleri kullanabilirsiniz. Örneğin:

    cd %hadoop_home%
    cd %hive_home%
    cd %hbase_home%
    cd %pig_home%
    cd %sqoop_home%
    cd %hcatalog_home%

## <a name="next-steps"></a>Sonraki adımlar
Bu makalede, nasıl toocreate kullanarak bir Hdınsight kümesi hello Portal ve nasıl tooopen hello Hadoop komut satırı aracı öğrendiniz. toolearn daha makaleler hello bakın:

* [Hdınsight Azure PowerShell kullanarak yönetme](hdinsight-administer-use-powershell.md)
* [Hdınsight Azure CLI kullanarak yönetme](hdinsight-administer-use-command-line.md)
* [Hdınsight kümeleri oluşturma](hdinsight-hadoop-provision-linux-clusters.md)
* [Hadoop işlerini programlı olarak gönderme](hdinsight-submit-hadoop-jobs-programmatically.md)
* [Azure Hdınsight kullanmaya başlama](hdinsight-hadoop-linux-tutorial-get-started.md)
* [Azure Hdınsight'ta Hadoop hangi sürümünün mi?](hdinsight-component-versioning.md)

[azure-portal]: https://portal.azure.com
[image-hadoopcommandline]: ./media/hdinsight-administer-use-management-portal/hdinsight-hadoop-command-line.png "Hadoop komut satırı"
