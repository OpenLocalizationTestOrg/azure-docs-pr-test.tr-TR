---
title: "Azure portalını kullanarak Hdınsight'ta aaaManage Hadoop kümeleri | Microsoft Docs"
description: "Bilgi nasıl toocreate ve hello Azure portal kullanarak Hdınsight kümelerini yönetme."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5a76f897-02e8-4437-8f2b-4fb12225854a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: jgao
ms.openlocfilehash: c242d43d4ccea7cf1e7be19c3f3d7ed3c4f50918
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-hello-azure-portal"></a>Hello Azure portal kullanarak hdınsight'ta Hadoop kümelerini yönetme
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

Hello kullanarak [Azure portal][azure-portal], Azure hdınsight'ta Hadoop kümelerini yönetebilirsiniz. Diğer araçları kullanarak hdınsight'ta Hadoop kümelerini yönetme hakkında bilgi için Hello sekme seçicisini kullanın.

**Önkoşullar**

Bu makalede başlamadan önce aşağıdaki öğelerindeki hello sahip olmanız gerekir:

* **Bir Azure aboneliği**. Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

## <a name="open-hello-portal"></a>Açık hello portalı
1. Çok oturum[https://portal.azure.com](https://portal.azure.com).
2. Merhaba portal açtıktan sonra şunları yapabilirsiniz:

   * Tıklatın **yeni** hello soldaki menüden toocreate yeni bir küme gelen:

       ![Yeni Hdınsight küme düğmesi](./media/hdinsight-administer-use-portal-linux/azure-portal-new-button.png)
   * Tıklatın **Hdınsight kümeleri** hello soldaki menüden toolist hello var olan kümeleri

       ![Azure portal Hdınsight küme düğmesi](./media/hdinsight-administer-use-portal-linux/azure-portal-hdinsight-button.png)

       ' I tıklatın, Hdınsight kümesi görmüyorsanız, **daha fazla hizmet** üzerinde hello hello listesinin altında ve ardından **Hdınsight kümeleri** hello altında **Intelligence + analiz** bölüm.


## <a name="create-clusters"></a>Küme oluşturma
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

Hdınsight geniş Hadoop bileşenleri ile çalışır. Doğrulandı ve desteklenen hello bileşenler Hello listesi için bkz [hangi sürümüdür Azure Hdınsight'ta hadoop](hdinsight-component-versioning.md). Merhaba genel küme oluşturma için bilgi [Hdınsight'ta oluşturmak Hadoop kümeleri](hdinsight-hadoop-provision-linux-clusters.md).

### <a name="access-control-requirements"></a>Erişim denetimi gereksinimleri

Bir Hdınsight kümesi oluştururken, bir Azure aboneliği belirtmeniz gerekir. Bu küme, yeni bir Azure kaynak grubu veya varolan bir kaynak grubu içinde oluşturulabilir. Hdınsight kümeleri oluşturmak için izinlerinizi adımları tooverify aşağıdaki hello kullanabilirsiniz:

- toouse varolan bir kaynak grubu.

    1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
    2. Tıklatın **kaynak grupları** hello soldaki menüden toolist hello kaynak gruplarından.
    3. Hdınsight kümesi oluşturmak için toouse istediğiniz hello kaynak grubunu tıklatın.
    4. Tıklatın **erişim denetimi (IAM)**, doğrulayın sizin (veya ait olduğunuz bir grubu) sahip en az, katkıda bulunan erişim toohello kaynak grubu hello.

- toocreate yeni bir kaynak grubu

    1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
    2. Tıklatın **abonelik** hello sol menüden. Sarı bir anahtar simgesi vardır. Aboneliklerin listesini göreceksiniz.
    3. Toocreate kümeleri kullandığınız hello aboneliğe tıklayın. 
    4. Tıklatın **izinlerimi**.  Bunu gösterir, [rol](../active-directory/role-based-access-control-what-is.md#built-in-roles) hello abonelikte. En az gereksinim duyduğunuz katkıda bulunan erişim toocreate Hdınsight kümesi.

Merhaba NoRegisteredProviderFound hatası veya hello MissingSubscriptionRegistration hatası alırsanız, bkz: [ortak Azure dağıtım hataları Azure Resource Manager ile ilgili sorunları giderme](../azure-resource-manager/resource-manager-common-deployment-errors.md).

## <a name="list-and-show-clusters"></a>Liste ve kümeleri Göster
1. Çok oturum[https://portal.azure.com](https://portal.azure.com).
2. Tıklatın **Hdınsight kümeleri** hello soldaki menüden toolist hello var olan kümeleri.
3. Merhaba küme adına tıklayın. Merhaba küme listesi uzunsa hello sayfa hello üstündeki filtresini kullanabilirsiniz.
4. Merhaba liste toosee hello genel bakış sayfasında bir kümeden tıklatın:

    ![Azure portal Hdınsight küme temelleri](./media/hdinsight-administer-use-portal-linux/hdinsight-essentials.png)

    * **Pano**: Linux tabanlı kümeler için Ambari Web olduğu açılır hello küme Panosu.
    * **Güvenli Kabuk**: gösterir hello yönergeleri tooconnect toohello küme güvenli Kabuk (SSH) bağlantısı kullanarak.
    * **Küme ölçeklendirme**: Bu küme için toochange hello çalışan düğümü sayısını sağlar.
    * **Silme**: hello küme siler.
    * **Etkinlik günlükleri**: Göster ve sorgu etkinlik günlükleri.
    * **Erişim denetimi (IAM)**: rol atamalarını kullanın.  Bkz: [rol atamalarını toomanage erişim tooyour Azure abonelik kaynaklarını kullanmak](../active-directory/role-based-access-control-configure.md).
    * **Etiketler**: Bulut hizmetlerinizi, özel bir sınıflandırma, tooset anahtar/değer çiftleri toodefine sağlar. Örneğin, adlı bir anahtar oluşturabilir **proje**ve ardından belirli bir projeyle ilişkili tüm hizmetler için ortak bir değer kullanın.
    * **Sorunları tanılamak ve**: sorun giderme bilgileri görüntüler.
    * **Kilitler**: kilit tooprevent hello küme olan değiştirilmiş veya silinmiş ekleyin.
    * **Otomasyon betiğini**: hello kümesi için görüntüleme ve dışarı aktarma hello Azure Resource Manager şablonu. Şu anda yalnızca hello bağımlı Azure depolama hesabı dışarı aktarabilirsiniz. Bkz: [oluşturma Linux tabanlı Hadoop kümeleri Azure Resource Manager şablonları kullanarak Hdınsight'ta](hdinsight-hadoop-create-linux-clusters-arm-templates.md).
    * **Hızlı Başlangıç**: yardımcı olacak bilgileri görüntüler, Hdınsight kullanarak başlayın.
    * **Hdınsight Araçları**: Hdınsight için Yardım bilgileri ilgili araçlar.
    * **Oturum açma küme**: hello küme oturum açma bilgileri görüntüler.
    * **Abonelik çekirdek kullanım**: görüntü hello aboneliğiniz için kullanılan ve kullanılabilir çekirdekler.
    * **Küme ölçeklendirme**: artırma ve azaltma hello küme çalışan düğüm sayısı. Bkz:[ölçek kümeleri](hdinsight-administer-use-management-portal.md#scale-clusters).
    * **Güvenli Kabuk**: gösterir hello yönergeleri tooconnect toohello küme güvenli Kabuk (SSH) bağlantısı kullanarak. Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).
    * **Hdınsight iş ortağı**: Merhaba geçerli Hdınsight iş ortağını ekleyin/kaldırın.
    * **Dış meta deponuz**: hello Hive ve Oozie meta deponuz görüntüleyin. Merhaba meta deponuz yalnızca hello küme oluşturma işlemi sırasında yapılandırılabilir. Bkz: [Hive/Oozie meta depo kullanmak](hdinsight-hadoop-provision-linux-clusters.md#use-hiveoozie-metastore).
    * **Betik eylemleri**: çalıştırmak Bash betikleri hello kümede. Bkz: [özelleştirme Linux tabanlı Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster-linux.md).
    * **Uygulamaları**: Ekle/Kaldır Hdınsight uygulamaları.  Bkz: [özel Hdınsight uygulamaları yükleme](hdinsight-apps-install-custom-applications.md).
    * **Özellikleri**: hello küme özelliklerini görüntüleyin.
    * **Depolama hesapları**: hello depolama hesapları ve hello anahtarları görüntüleyin. Merhaba depolama hesapları hello küme oluşturma işlemi sırasında yapılandırılır.
    * **Küme AAD kimlik**:
    * **Yeni destek isteği**: toocreate Microsoft desteği ile bir destek bileti sağlar.
    
6. Tıklatın **özellikleri**:

    Merhaba özellikleri şunlardır:

   * **Ana bilgisayar adı**: küme adı.
   * **Küme URL**. Merhaba Ambari web arabirimi Hello URL'si.
   * **Durum**: dahil, kabul iptal ClusterStorageProvisioned, AzureVMConfiguration, çalıştığından, silme, hatası, HDInsightConfiguration, işletimsel, silinen, süresi sona erdi, DeleteQueued, DeleteTimedout, DeleteError, PatchQueued, CertRolloverQueued, ResizeQueued, ClusterCustomization
   * **Bölge**: Azure konumu. Merhaba desteklenen Azure konumu listesi için bkz **bölge** açılan liste kutusunu [Hdınsight fiyatlandırma](https://azure.microsoft.com/pricing/details/hdinsight/).
   * **Oluşturulma tarihi**.
   * **İşletim sistemi**: ya da **Windows** veya **Linux**.
   * **Tür**: Hadoop, HBase, Storm, Spark.
   * **Sürüm**. Bkz: [Hdınsight sürümleri](hdinsight-component-versioning.md)
   * **Abonelik**: Abonelik adı.
   * **Varsayılan veri kaynağı**: Merhaba varsayılan küme dosya sistemi.
   * **Çalışan düğüm boyutu**.
   * **Baş düğüm boyutu**.

## <a name="delete-clusters"></a>Küme silme
Küme silme hello varsayılan depolama hesabı ya da bağlı tüm depolama hesaplarını silmez. Merhaba küme kullanarak yeniden oluşturabileceğiniz hello aynı depolama hesapları ve hello aynı meta depolar. Bu yeniden hello Küme oluşturduğunuzda, yeni varsayılan Blob kapsayıcısını toouse önerilir.

1. İçinde toohello oturum [Portal][azure-portal].
2. Tıklatın **Hdınsight kümeleri** hello sol menüden. Görmüyorsanız, **Hdınsight kümeleri**, tıklatın **daha fazla hizmet** ilk.
3. Toodelete istediğiniz hello kümesine tıklayın.
4. Tıklatın **silmek** hello üst menüsünden ve hello yönergeleri izleyin.

Ayrıca bkz. [Duraklat/kümeleri kapatma](#pauseshut-down-clusters).

## <a name="add-additional-storage-accounts"></a>Başka depolama hesapları ekleme

Bir küme oluşturulduktan sonra ek Azure Storage ve Azure Data Lake Store hesapları ekleyebilirsiniz. Daha fazla bilgi için bkz: [ek depolama hesapları tooHDInsight eklemek](./hdinsight-hadoop-add-storage.md).

## <a name="scale-clusters"></a>Kümeleri ölçeklendirme
özellik ölçeklendirme hello küme toochange hello Azure Hdınsight'ta toore gerek kalmadan çalışan bir küme tarafından kullanılan çalışan düğüm sayısı sağlar-hello kümesi oluşturun.

> [!NOTE]
> Yalnızca, Hdınsight sürüm 3.1.3 ile kümeleri veya üzeri desteklenir. Kümenizin hello sürümü değilseniz hello özellikler sayfasını kontrol edebilirsiniz.  Bkz: [listesi ve Göster kümeleri](#list-and-show-clusters).
>
>

hello etkisini, her tür Hdınsight tarafından desteklenen küme için veri düğümünün hello numarasını değiştirmek için:

* Hadoop

    Sorunsuz bir şekilde hello tüm bekleyen veya çalışan işler etkilemeden çalıştıran bir Hadoop kümesinde çalışan düğümü sayısını da artırabilirsiniz. Merhaba işlemi devam ederken yeni işleri da gönderilebilir. Böylece Hello küme her zaman işlevsel bir durumda bırakılır bir ölçeklendirme işlemi hatalar düzgün bir şekilde ele alınır.

    Bir Hadoop kümesine veri düğümlerini hello sayısını azaltarak ölçeklendirilir, bazı hello kümedeki hello hizmetleri yeniden başlatılır. Bu davranış, tüm çalışan ve işleri toofail hello tamamlanma işlemi ölçeklendirme Merhaba, bekleyen neden olur. Hello işlemi tamamlandıktan sonra ancak, hello sunmaları olabilir.
* HBase

    Sorunsuz bir şekilde ekleme veya düğümleri tooyour HBase kümesi çalışırken kaldırın. Bölgesel sunucuları işlemi ölçeklendirme hello tamamladıktan birkaç dakika içinde otomatik olarak dengeli. Ancak, küme ve komutlar bir komut istemi penceresinden aşağıdaki çalışan hello toohello headnode oturum açarak hello bölgesel sunucular el ile de dengeleyebilirsiniz:

        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer

    Merhaba HBase Kabuğu'nu kullanarak daha fazla bilgi için bkz:]
* Storm

    Sorunsuz bir şekilde ekleyebilir veya çalışırken veri düğümleri tooyour Storm kümesi kaldırabilirsiniz. Ancak hello ölçekleme işlemi başarıyla tamamlandıktan sonra toorebalance hello topoloji gerekir.

    İki yolla yeniden dengelenmesi gerçekleştirilebilir:

  * Storm web kullanıcı Arabirimi
  * Komut satırı arabirimi (CLI) aracı

    Toohello başvuran [Apache Storm belgelerine](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) daha fazla ayrıntı için.

    Merhaba Storm web kullanıcı Arabirimi hello Hdınsight kümesinde kullanılabilir:

    ![Hdınsight Storm ölçek yeniden dengeleyin](./media/hdinsight-administer-use-portal-linux/hdinsight-portal-scale-cluster-storm-rebalance.png)

    Örneği nasıl toouse hello CLI komutu toorebalance hello Storm topolojisini:

        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

**tooscale kümeleri**

1. İçinde toohello oturum [Portal][azure-portal].
2. Tıklatın **Hdınsight kümeleri** hello sol menüden.
3. Tooscale istediğiniz hello kümesine tıklayın.
3. Tıklatın **ölçeklendirme kümesi**.
4. Girin **sayı, alt düğümleri**. Merhaba küme düğümleri sayısı hello Azure abonelikleri arasında değişiklik gösterir. Faturalama desteği tooincrease hello sınırı başvurabilirsiniz.  Merhaba maliyet bilgileri toohello düğüm sayısını yapmış olduğunuz hello değişiklikleri yansıtır.

    ![Hdınsight, hadoop, hbase, storm, spark, Ölçek](./media/hdinsight-administer-use-portal-linux/hdinsight-portal-scale-cluster.png)

## <a name="pauseshut-down-clusters"></a>Kümeleri Duraklat/kapatma

Hadoop işlerinin çoğu yalnızca zaman zaman çalıştırmak toplu işleri ' dir. Çoğu Hadoop kümeleri için büyük nokta vardır süresini bu hello küme işleme için kullanılmayan. HDInsight ile, verileriniz Azure Storage’da depolanır, böylece kullanılmadığında bir kümeyi güvenle silebilirsiniz.
Ayrıca, kullanılmıyorken dahi HDInsight kümesi için sizden ücret kesilir. Merhaba ücretleri hello küme için hello ücretleri depolama birkaç katı olduğundan, bunlar kullanımda olmadığında ekonomik toodelete kümeleri mantıklıdır.

Merhaba işlem programı birçok yolu vardır:

* Kullanıcı Azure Data Factory. Bkz: [oluşturma isteğe bağlı Linux tabanlı Hadoop kümeleri Azure Data Factory kullanarak Hdınsight'ta](hdinsight-hadoop-create-linux-clusters-adf.md) isteğe bağlı Hdınsight oluşturmak için bağlantılı Hizmetleri.
* Azure PowerShell kullanın.  Bkz: [uçuş gecikme verilerini çözümleme](hdinsight-analyze-flight-delay-data.md).
* Azure CLI kullanın. Bkz: [Azure CLI kullanarak Hdınsight kümelerini yönetme](hdinsight-administer-use-command-line.md).
* Hdınsight .NET SDK'yı kullanın. Bkz: [gönderme Hadoop işlerini](hdinsight-submit-hadoop-jobs-programmatically.md).

Fiyatlandırma bilgileri hello için bkz: [Hdınsight fiyatlandırma](https://azure.microsoft.com/pricing/details/hdinsight/). toodelete hello Portal, bir kümeden bkz [küme silme](#delete-clusters)


## <a name="upgrade-clusters"></a>Küme yükseltme

Bkz: [yükseltme Hdınsight küme tooa daha yeni sürümü](./hdinsight-upgrade-cluster.md).

## <a name="change-passwords"></a>Parolaları değiştirme
Hdınsight kümesi, iki kullanıcı hesapları olabilir. Hdınsight küme kullanıcı hesabı (paketini hello HTTP kullanıcı hesabı) ve hello SSH kullanıcı hesabı hello oluşturma işlemi sırasında oluşturulur. Merhaba Ambari web kullanıcı Arabirimi toochange hello küme kullanıcı hesabı kullanıcı adı ve parola ve betik eylemleri toochange hello SSH kullanıcı hesabı kullanabilirsiniz

### <a name="change-hello-cluster-user-password"></a>Merhaba küme kullanıcı parolasını değiştirme
Merhaba Ambari Web kullanıcı arabirimini toochange hello küme kullanıcı parolası kullanabilirsiniz. toolog tooAmbari içinde hello var olan küme kullanıcı adı ve parola kullanmanız gerekir.

> [!NOTE]
> Merhaba küme kullanıcı (Yönetici) parolası değiştiriliyor Eylemler bu küme toofail karşı çalışan betik neden olabilir. Çalışan düğümü hedef kalıcı betik eylemleri varsa, yeniden boyutlandırma işlemleri aracılığıyla düğümleri toohello kümesi eklediğinizde, bu komut dosyaları başarısız olabilir. Betik eylemleri hakkında daha fazla bilgi için bkz: [özelleştirme Hdınsight kümeleri betik eylemleri kullanılarak](hdinsight-hadoop-customize-cluster-linux.md).
>
>

1. Toohello Ambari Web kullanıcı arabirimini kullanarak oturum Hdınsight küme kullanıcı kimlik bilgilerini hello. Merhaba varsayılan kullanıcı adı **yönetici**. URL hello **https://&lt;Hdınsight küme adı > azurehdinsight.net**.
2. Tıklatın **yönetici** hello üst menüden "Ambarı Yönet"'a tıklayın.
3. Merhaba sol menüden **kullanıcılar**.
4. Tıklatın **yönetici**.
5. Tıklatın **Parola Değiştir**.

Ambari, ardından hello kümedeki tüm düğümlerde hello parolasını değiştirir.

### <a name="change-hello-ssh-user-password"></a>Merhaba SSH kullanıcı parolasını değiştirme
1. Bir metin düzenleyicisi kullanarak metin adlı bir dosya aşağıdaki hello Kaydet **changepassword.sh**.

   > [!IMPORTANT]
   > Merhaba satır bitiş olarak LF kullanan bir Düzenleyicisi'ni kullanmanız gerekir. Merhaba Düzenleyicisi CRLF kullanıyorsa, hello komut çalışmaz.
   >
   >

        #! /bin/bash
        USER=$1
        PASS=$2

        usermod --password $(echo $PASS | openssl passwd -1 -stdin) $USER
2. Bir HTTP veya HTTPS adresi kullanarak Hdınsight'ta erişilebilir hello dosya tooa depolama konumu karşıya yükleyin. Örneğin, ortak bir dosyanın gibi OneDrive veya Azure Blob Depolama depolayın. Bu URI hello sonraki adımda gerektiğinde Merhaba URI (HTTP veya HTTPS adresi) toohello dosyayı kaydedin.
3. Hello ifadesini Azure portal'ı tıklatın **Hdınsight kümeleri**.
4. Hdınsight kümesine tıklayın.
4. Tıklatın **betik eylemleri**.
4. Merhaba gelen **betik eylemleri** dikey penceresinde, select **gönderme yeni**. Ne zaman hello **betik eylemi Gönder** dikey penceresi görünür, aşağıdaki bilgilerle hello girin:

   | Alan | Değer |
   | --- | --- |
   | Ad |SSH parolasını değiştirme |
   | Bash betik URI |Merhaba URI toohello changepassword.sh dosyası |
   | Düğümler (Head, çalışan, Nimbus, yönetici, Zookeeper, vb.) |✓ listelenen tüm düğüm türleri |
   | Parametreler |Merhaba SSH kullanıcı adı ve ardından hello yeni parolayı girin. Merhaba kullanıcı adı ve parola hello arasında bir boşluk olması gerekir. |
   | Bu betik eylemini Sürdür... |Bu alan işaretli bırakın. |
5. Seçin **oluşturma** tooapply hello komut dosyası. Hello betik tamamlandıktan sonra SSH hello yeni parolayla kullanarak mümkün tooconnect toohello kümelerdir.

## <a name="grantrevoke-access"></a>GRANT/revoke erişim
Hdınsight kümeleri HTTP web Hizmetleri (Bu hizmetlerin tümü için RESTful uç noktaları vardır) aşağıdaki hello vardır:

* ODBC
* JDBC
* Ambari
* Oozie
* Templeton

Varsayılan olarak, bu hizmetleri için erişim verilir. İptal etme/hello kullanarak erişimini grant [Azure CLI](hdinsight-administer-use-command-line.md#enabledisable-http-access-for-a-cluster) ve [Azure PowerShell](hdinsight-administer-use-powershell.md#grantrevoke-access).

## <a name="find-hello-subscription-id"></a>Merhaba abonelik kimliği bulunamadı

**toofind, Azure aboneliğinizin kimlikleri**

1. İçinde toohello oturum [Portal][azure-portal].
2. Tıklatın **abonelikleri**. Her abonelik bir ada ve bir kimliğe sahip

Her küme bağlı tooan Azure aboneliği ' dir. Merhaba abonelik kimliği hello kümede gösterilen **temel** döşeme. Bkz: [listesi ve Göster kümeleri](#list-and-show-clusters).

## <a name="find-hello-resource-group"></a>Merhaba kaynak grup bulunamıyor
Hello Azure Kaynak Yöneticisi modunda her Hdınsight kümesi içeren bir Azure Resource Manager grubu oluşturulur. bir küme içinde tooappears ait hello Resource Manager Grup:

* Merhaba küme listesi olan bir **kaynak grubu** sütun.
* Küme **temel** döşeme.  

Bkz: [listesi ve Göster kümeleri](#list-and-show-clusters).

## <a name="find-hello-default-storage-account"></a>Merhaba varsayılan depolama hesabı bulunamadı
Her Hdınsight kümesinde bir varsayılan depolama hesabı vardır. Merhaba varsayılan depolama hesabı ve alt anahtarları altında bir küme görünür **depolama hesapları**. Bkz: [listesi ve Göster kümeleri](#list-and-show-clusters).

## <a name="run-hive-queries"></a>Hive sorguları çalıştırma
Doğrudan hello Azure Portalı ' Hive işi çalıştırılamıyor. ancak hello Ambari Web kullanıcı arabirimini Hive görünümü kullanabilirsiniz.

**Ambari Hive görünümünü kullanarak toorun Hive sorguları**

1. Toohello Ambari Web kullanıcı arabirimini kullanarak oturum Hdınsight küme kullanıcı kimlik bilgilerini hello. Merhaba varsayılan kullanıcı adı **yönetici**. URL hello **https://&lt;Hdınsight küme adı > azurehdinsight.net**.
2. Hive görünümü hello ekran aşağıdaki gösterildiği gibi açın:  

    ![Hdınsight hive görünümü](./media/hdinsight-administer-use-portal-linux/hdinsight-hive-view.png)
3. Tıklatın **sorgu** hello üst menüsünde.
4. Bir Hive sorgusu girin **sorgu Düzenleyicisi'ni**ve ardından **yürütme**.

## <a name="monitor-jobs"></a>İşleri izleme
Bkz: [Hdınsight kümelerini yönetme hello Ambari Web kullanıcı arabirimini kullanarak](hdinsight-hadoop-manage-ambari.md#monitoring).

## <a name="browse-files"></a>Gözatma dosyaları
Hello Azure portal kullanarak hello varsayılan kapsayıcı Merhaba içeriğine göz atabilirsiniz.

1. Çok oturum[https://portal.azure.com](https://portal.azure.com).
2. Tıklatın **Hdınsight kümeleri** hello soldaki menüden toolist hello var olan kümeleri.
3. Merhaba küme adına tıklayın. Merhaba küme listesi uzunsa hello sayfa hello üstündeki filtresini kullanabilirsiniz.
4. Tıklatın **depolama hesapları** hello küme sol menüden.
5. Bir depolama hesabı'nı tıklatın.
7. Merhaba tıklatın **BLOB'lar** döşeme.
8. Merhaba varsayılan kapsayıcı adına tıklayın.

## <a name="monitor-cluster-usage"></a>Küme kullanımını izleme
Merhaba **kullanım** hello Hdınsight kümesi dikey bölümünü hello toothis küme ve bulundukları nasıl ayrılan çekirdek sayısı yanı sıra, Hdınsight ile kullanmak için çekirdek kullanılabilir tooyour abonelik hello sayısı hakkında bilgileri görüntüler Bu küme içindeki hello düğümler için ayrılmış. Bkz: [listesi ve Göster kümeleri](#list-and-show-clusters).

> [!IMPORTANT]
> toomonitor hello Hizmetleri Hdınsight kümesi hello tarafından sağlanan, Ambari REST API hello veya Ambari Web kullanmanız gerekir. Ambari kullanarak daha fazla bilgi için bkz: [Ambari kullanarak Hdınsight kümelerini yönetme](hdinsight-hadoop-manage-ambari.md)
>
>

## <a name="connect-tooa-cluster"></a>Tooa kümesine bağlanın

* [HDInsight ile Hive kullanma](hdinsight-hadoop-use-hive-ambari-view.md)
* [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md)

## <a name="next-steps"></a>Sonraki adımlar
Bu makalede, bazı temel daki Hizmetler'i işlevleri öğrendiniz. toolearn daha makaleler hello bakın:

* [Hdınsight Azure PowerShell kullanarak yönetme](hdinsight-administer-use-powershell.md)
* [Hdınsight Azure CLI kullanarak yönetme](hdinsight-administer-use-command-line.md)
* [Hdınsight kümeleri oluşturma](hdinsight-hadoop-provision-linux-clusters.md)
* [Hdınsight'ta Hive kullanma](hdinsight-use-hive.md)
* [Hdınsight'ta pig kullanma](hdinsight-use-pig.md)
* [Hdınsight'ta Sqoop kullanma](hdinsight-use-sqoop.md)
* [Azure Hdınsight kullanmaya başlama](hdinsight-hadoop-linux-tutorial-get-started.md)
* [Azure Hdınsight'ta Hadoop hangi sürümünün mi?](hdinsight-component-versioning.md)

[azure-portal]: https://portal.azure.com
[image-hadoopcommandline]: ./media/hdinsight-administer-use-portal-linux/hdinsight-hadoop-command-line.png "Hadoop komut satırı"
