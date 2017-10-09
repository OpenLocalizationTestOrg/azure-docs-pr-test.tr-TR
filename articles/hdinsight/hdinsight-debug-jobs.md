---
title: "Hdınsight'ta Hadoop hata ayıklama: günlüklerini görüntülemek ve hata iletileri - Azure yorumlama | Microsoft Docs"
description: "PowerShell ve toorecover atabileceğiniz adımları kullanarak Hdınsight yönetirken alabilirsiniz hello hata iletileri hakkında bilgi edinin."
services: hdinsight
tags: azure-portal
editor: cgronlun
manager: jhubbard
author: mumian
documentationcenter: 
ms.assetid: 7e6ceb0e-8be8-4911-bc80-20714030a3ad
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: jgao
ms.openlocfilehash: 2f12a40e9dcac32ce2e11d66d60d8b3b212ecb53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-hdinsight-logs"></a>HDInsight günlüklerini çözümleme
Her Azure Hdınsight Hadoop kümesinde hello varsayılan dosya sistemi olarak kullanılan bir Azure depolama hesabı vardır. Merhaba depolama hesabı hello varsayılan depolama hesabı olarak adlandırılır. Küme hello Azure tablo depolaması ve hello Blob Depolama günlüklerinin hello varsayılan depolama hesabı toostore üzerinde kullanır.  toofind hello varsayılan depolama hesabı, kümeniz için bkz: [Hdınsight'ta Hadoop yönetmek kümeleri](hdinsight-administer-use-management-portal.md#find-the-default-storage-account). hatta hello kümesi silindikten sonra hello günlükleri hello depolama hesabı korur.

## <a name="logs-written-tooazure-tables"></a>TooAzure tabloları yazılmış günlükleri
Merhaba tooAzure tabloları yazılmış günlükleri neler olduğuna dair bir Hdınsight kümesini içine Insight bir düzey sağlar.

Bir Hdınsight kümesi oluştururken, 6 tabloları hello varsayılan Table storage Linux tabanlı kümelerde için otomatik olarak oluşturulur:

* hdinsightagentlog
* syslog
* daemonlog
* hadoopservicelog
* ambariserverlog
* ambariagentlog

Windows tabanlı kümeler için 3 tablolar oluşturulur:

* Setuplog: günlük olayları/özel durumların sağlama/Hdınsight kümelerini kurulumunun karşılaştı.
* hadoopinstalllog: günlük olayları/özel durumların Hadoop hello kümede yüklerken karşılaştı. Bu tablo hataları ayıklamamızda yararlı olabilecek ilgili özel parametrelerle oluşturulan tooclusters.
* hadoopservicelog: günlük olayları/özel durumların tüm Hadoop Hizmetleri tarafından kaydedilir. Bu tablo Hdınsight kümelerinde sorunları ilgili toojob hatalarını ayıklama de yararlı olabilir.

Merhaba tablo dosya adları **u<ClusterName>DDMonYYYYatHHMMSSsss<TableName>**.

Bu tablolar alanları izleyen hello içerir:

* ClusterDnsName
* ComponentName
* eventTimestamp
* Host
* MALoggingHash
* İleti
* N
* PreciseTimeStamp
* Rol
* RowIndex
* Kiracı
* ZAMAN DAMGASI
* TraceLevel

### <a name="tools-for-accessing-hello-logs"></a>Merhaba günlükleri erişmek için Araçlar
Bu tablolardaki verileri erişmek için kullanılabilen birçok araç vardır:

* Visual Studio
* Azure Depolama Gezgini
* Excel için Power Query

#### <a name="use-power-query-for-excel"></a>Excel için Power Query kullanın
Power Query yüklenebilir [www.microsoft.com/en-us/download/details.aspx?id=39379](http://www.microsoft.com/en-us/download/details.aspx?id=39379). Merhaba indirme sayfasının hello sistem gereksinimleri için bkz:

**toouse Power Query tooopen ve hello hizmeti günlüğünü analiz edin**

1. Açık **Microsoft Excel**.
2. Merhaba gelen **Power Query** menüsünde tıklatın **Azure**ve ardından **From Microsoft Azure Table depolama**.
   
    ![Hdınsight Hadoop Excel PowerQuery Azure Table depolama açın](./media/hdinsight-debug-jobs/hdinsight-hadoop-analyze-logs-using-excel-power-query-open.png)
3. Merhaba depolama hesabı adı girin. Bu hello kısa bir ad veya hello FQDN olabilir.
4. Merhaba depolama hesabı anahtarı girin. Tabloların bir listesini göreceksiniz:
   
    ![Azure Table storage'da depolanan Hdınsight Hadoop günlükleri](./media/hdinsight-debug-jobs/hdinsight-hadoop-analyze-logs-table-names.png)
5. Sağ hello hadoopservicelog hello tabloda **Gezgini** bölmesinde ve select **Düzenle**. 4 sütun göreceksiniz. İsteğe bağlı olarak, hello silin **bölüm anahtarı**, **satır anahtarını**, ve **zaman damgası** bunları seçtikten sonra tıklatarak sütunları **sütunları kaldırmak** Merhaba Şeritte Hello seçeneklerinden.
6. Merhaba tıklatın hello simgesine genişletin içerik istediğiniz tooimport hello Excel elektronik tablosuna sütun toochoose hello sütun. Bu Tanıtım için TraceLevel ve ComponentName seçtiğim: Bu bana bileşenleri üzerinde sorunları olan bazı temel bilgileri verin.
   
    ![Hdınsight Hadoop günlükleri sütunları seçin](./media/hdinsight-debug-jobs/hdinsight-hadoop-analyze-logs-using-excel-power-query-filter.png)
7. Tıklatın **Tamam** tooimport hello veri.
8. Select hello **TraceLevel**, rol ve **ComponentName** sütunları ve ardından **Group By** hello Şeritte denetim.
9. Tıklatın **Tamam** hello Group By iletişim kutusunda
10. Uygulama tıklatın ** & Kapat **.

Artık Excel toofilter ve sıralama gerektiği şekilde kullanabilirsiniz. Tabii ki, tooinclude sipariş toodrill diğer sütunlardaki (örneğin, ileti) sorunlar ortaya ancak seçerek ve yukarıda açıklanan hello sütunları gruplandırma Hadoop Hizmetleri ile neler olduğunu makul bir resim sağlanmıştır isteyebilirsiniz. Merhaba aynı fikir uygulanan toohello setuplog ve hadoopinstalllog tabloları olabilir.

#### <a name="use-visual-studio"></a>Visual Studio'yu kullanma
**Visual Studio toouse**

1. Visual Studio'yu açın.
2. Merhaba gelen **Görünüm** menüsünde tıklatın **Cloud Explorer**. Veya tıklamanız yeterlidir **CTRL +\, CTRL + X**.
3. Gelen **Cloud Explorer**seçin **kaynak türleri**.  Merhaba diğer seçenek olan **kaynak grupları**.
4. Genişletme **depolama hesapları**, Merhaba, kümeniz için varsayılan depolama hesabı ve ardından **tabloları**.
5. Çift **hadoopservicelog**.
6. Bir filtre ekleyin. Örneğin:
   
        TraceLevel eq 'ERROR'
   
    ![Hdınsight Hadoop günlükleri sütunları seçin](./media/hdinsight-debug-jobs/hdinsight-hadoop-analyze-logs-visual-studio-filter.png)
   
    Filtreleri oluşturma hakkında daha fazla bilgi için bkz: [hello Tablo Tasarımcısı için filtre dizelerini oluşturmak](../vs-azure-tools-table-designer-construct-filter-strings.md).

## <a name="logs-written-tooazure-blob-storage"></a>Günlükleri yazılan tooAzure Blob Depolama
[Merhaba günlüklerini yazılı tooAzure tabloları](#log-written-to-azure-tables) bir düzeyde neler olduğuna dair bir Hdınsight kümesini içine Insight sağlar. Ancak, bu tablolar ayrıntılara yararlı olabilir görev düzeyi günlükleri sağlamaz ortaya çıkan sorunları daha. tooprovide bu ileri düzeyde ayrıntı, Hdınsight kümesi olan toowrite görev günlükleri tooyour Blob Storage hesabı Templeton gönderilen herhangi bir iş için yapılandırılmış. Pratikte, bu hello Microsoft Azure PowerShell cmdlet'lerini veya hello .NET iş gönderme API'leri, RDP/komut-satırı erişim toohello aracılığıyla kümesine gönderilen işler kullanılarak gönderilen işler anlamına gelir. 

tooview hello günlüklerine bakın [erişim YARN uygulama günlüklerini Hdınsight'ta Linux tabanlı](hdinsight-hadoop-access-yarn-app-logs-linux.md).

Uygulama günlükleri hakkında daha fazla bilgi için bkz: [kullanıcı oturum yönetimi ve YARN erişimi basitleştirme](http://hortonworks.com/blog/simplifying-user-logs-management-and-access-in-yarn/).

## <a name="view-cluster-health-and-job-logs"></a>Küme durumu ve iş günlüklerine bakın
### <a name="access-hadoop-ui"></a>Erişim Hadoop kullanıcı Arabirimi
Azure portal Hello bir Hdınsight küme adı tooopen hello küme dikey tıklayın. Merhaba küme dikey penceresinden tıklayın **Pano**.

![Küme panosunu başlatma](./media/hdinsight-debug-jobs/hdi-debug-launch-dashboard.png)

İstendiğinde, hello Küme Yöneticisi kimlik bilgilerini girin. Hello açar sorgu konsol, tıklatın **Hadoop UI**.

![Hadoop kullanıcı arabirimini Başlat](./media/hdinsight-debug-jobs/hdi-debug-launch-dashboard-hadoop-ui.png)

### <a name="access-hello-yarn-ui"></a>Erişim hello Yarn kullanıcı Arabirimi
Azure portal Hello bir Hdınsight küme adı tooopen hello küme dikey tıklayın. Merhaba küme dikey penceresinden tıklayın **Pano**. İstendiğinde, hello Küme Yöneticisi kimlik bilgilerini girin. Hello açar sorgu konsol, tıklatın **YARN kullanıcı Arabiriminde**.

Merhaba YARN kullanıcı Arabiriminde toodo hello aşağıdakileri kullanabilirsiniz:

* **Küme durumunu Al**. Merhaba sol bölmeden genişletin **küme**, tıklatıp **hakkında**. Bu mevcut durumu ayrıntıları kullanıldığında, çekirdek bellek tahsis edilen toplam hello Küme Kaynak Yöneticisi'nin durumu gibi küme, sürüm vb. küme.
  
    ![Küme panosunu başlatma](./media/hdinsight-debug-jobs/hdi-debug-yarn-cluster-state.png)
* **Düğüm durumunu Al**. Merhaba sol bölmeden genişletin **küme**, tıklatıp **düğümleri**. Bu, tüm hello düğümlerini hello küme, her düğüm, kaynakları ayrılmış tooeach düğümü vb. HTTP adresini listeler.
* **İzleme iş durumu**. Merhaba sol bölmeden genişletin **küme**ve ardından **uygulamaları** toolist tüm işleri hello kümedeki hello. Belirli bir işlerinde adresindeki toolook istiyorsanız (örneğin, yeni, gönderilen, çalışan, vb.) durumu altında hello uygun bağlantıyı tıklatın **uygulamaları**. Daha fazla hello iş adı toofind hello çıktı, günlükleri, vb. dahil olmak üzere bu tür hello işi hakkında daha fazla tıklatabilirsiniz.

### <a name="access-hello-hbase-ui"></a>Erişim hello HBase kullanıcı Arabirimi
Azure portal Hello bir Hdınsight HBase kümesi adı tooopen hello küme dikey'i tıklatın. Merhaba küme dikey penceresinden tıklayın **Pano**. İstendiğinde, hello Küme Yöneticisi kimlik bilgilerini girin. Hello açar sorgu konsol, tıklatın **HBase UI**.

## <a name="hdinsight-error-codes"></a>Hdınsight hata kodları
Merhaba bu bölümünde listelenen hata iletileri toohelp hello Azure hdınsight'ta Hadoop kullanıcılarının anlamak hello hizmetini Azure PowerShell ve tooadvise kullanarak yönetirken karşılaşabilirsiniz olası hata koşulları sağlanan bunları hello adımlar hangi hello hatadan toorecover alınabilir.

Kullanılan toomanage Hdınsight kümeleri olduğunda bu hata iletileri bazıları hello Azure portal'ne de görülebilir. Ancak, karşılaşabileceğiniz diğer hata iletilerini vardır hello eylemlerden bu bağlamda olası toohello kısıtlamaları nedeniyle daha az ayrıntılı. Diğer hata iletilerini hello azaltma belirgin olduğu hello bağlamlarda sağlanır. 

### <a id="AtleastOneSqlMetastoreMustBeProvided"></a>AtleastOneSqlMetastoreMustBeProvided
* **Açıklama**: Lütfen Azure SQL veritabanı ayrıntıları sipariş toouse içinde en az bir bileşen için Hive ve Oozie meta deponuz için özel ayarları belirtin.
* **Azaltma**: hello kullanıcı toosupply geçerli bir SQL Azure meta depo ve Yeniden Dene'yi hello isteği gerekiyor.  

### <a id="AzureRegionNotSupported"></a>AzureRegionNotSupported
* **Açıklama**: küme bölgede oluşturulamadı *nameOfYourRegion*. Geçerli bir Hdınsight bölgesi kullanın ve isteği yeniden deneyin.
* **Azaltma**: Müşteri şu anda bunları destekleyen hello küme bölge oluşturmanız: Güneydoğu Asya, Batı Avrupa, Kuzey Avrupa, Doğu ABD veya Batı ABD.  

### <a id="ClusterContainerRecordNotFound"></a>ClusterContainerRecordNotFound
* **Açıklama**: hello sunucu bulamadı hello istenen küme kaydı.  
* **Azaltma**: hello işlemi yeniden deneyin.

### <a id="ClusterDnsNameInvalidReservedWord"></a>ClusterDnsNameInvalidReservedWord
* **Açıklama**: küme DNS adına *yourDnsName* geçersiz. Lütfen adı başlatır ve alfasayısal biten emin olun ve yalnızca içerebilir '-' özel karakter  
* **Azaltma**: başlatır ve alfasayısal biten ve hiçbir özel içeren kümenizi hello tire dışındaki karakterleri için geçerli bir DNS adı kullanılan olduğundan emin olun '-' hello işlemini yeniden deneyin.

### <a id="ClusterNameUnavailable"></a>ClusterNameUnavailable
* **Açıklama**: küme adı *yourClusterName* kullanılamıyor. Lütfen başka bir ad seçin.  
* **Azaltma**: hello kullanıcı benzersiz olan bir clustername ve değil mevcut belirtip yeniden deneyin. Merhaba kullanıcı hello portalı kullanıyorsanız, UI bunları bir küme adı zaten sırasında hello kullanılmakta olup olmadığını bildirir hello adımları oluşturun.

### <a id="ClusterPasswordInvalid"></a>ClusterPasswordInvalid
* **Açıklama**: küme parola geçersiz. Parola en az 10 karakter uzunluğunda olmalıdır ve en az bir rakam, büyük harf, küçük harf ve boşluksuz özel karakter içermelidir ve bunun bir parçası olarak hello kullanıcıadı içermemesi gerekir.  
* **Azaltma**: geçerli küme parola sağlayın ve hello işlemi yeniden deneyin.

### <a id="ClusterUserNameInvalid"></a>ClusterUserNameInvalid
* **Açıklama**: küme kullanıcı adı geçersiz. Lütfen kullanıcı adı özel karakter veya boşluk içermeyen emin olun.  
* **Azaltma**: geçerli küme kullanıcı adını belirtin ve hello işlemi yeniden deneyin.

### <a id="ClusterUserNameInvalidReservedWord"></a>ClusterUserNameInvalidReservedWord
* **Açıklama**: küme DNS adına *yourDnsClusterName* geçersiz. Lütfen adı başlatır ve alfasayısal biten emin olun ve yalnızca içerebilir '-' özel karakter  
* **Azaltma**: geçerli bir DNS küme kullanıcı adı sağlayın ve hello işlemi yeniden deneyin.

### <a id="ContainerNameMisMatchWithDnsName"></a>ContainerNameMisMatchWithDnsName
* **Açıklama**: kapsayıcı adı URI *yourcontainerURI* ve DNS adı *yourDnsName* istek gövdesi gerekir olması hello aynı.  
* **Azaltma**: emin olun, kapsayıcı adı ve DNS adı olan, hello aynı ve hello işlemi yeniden deneyin.

### <a id="DataNodeDefinitionNotFound"></a>DataNodeDefinitionNotFound
* **Açıklama**: Geçersiz küme yapılandırması. %S toofind hiçbir veri düğümü tanımlarını düğüm boyutu.  
* **Azaltma**: hello işlemi yeniden deneyin.

### <a id="DeploymentDeletionFailure"></a>DeploymentDeletionFailure
* **Açıklama**: dağıtımını silme işlemi başarısız oldu Merhaba küme  
* **Azaltma**: hello silme işlemi yeniden deneyin.

### <a id="DnsMappingNotFound"></a>DnsMappingNotFound
* **Açıklama**: hizmet yapılandırma hatası. Gerekli DNS eşlemesi bilgileri bulunamadı.  
* **Azaltma**: küme silip yeni bir küme oluşturun.

### <a id="DuplicateClusterContainerRequest"></a>DuplicateClusterContainerRequest
* **Açıklama**: Yinelenen küme kapsayıcı oluşturma girişimi. Kayıt mevcut *nameOfYourContainer* ancak Etag'ler eşleşmiyor.
* **Azaltma**: hello kapsayıcı ve Yeniden Dene'yi hello oluşturma işlemi için benzersiz bir ad girin.

### <a id="DuplicateClusterInHostedService"></a>DuplicateClusterInHostedService
* **Açıklama**: barındırılan hizmeti *nameOfYourHostedService* bir küme zaten içeriyor. Barındırılan bir hizmet birden çok küme içeremez.  
* **Azaltma**: ana bilgisayar hello kümedeki başka bir barındırılan hizmet.

### <a id="FailureToUpdateDeploymentStatus"></a>FailureToUpdateDeploymentStatus
* **Açıklama**: hello değil güncelleştirme sunucusu hello Küme dağıtımı hello durumu.  
* **Azaltma**: hello işlemi yeniden deneyin. Birden çok kez aşması durumunda, CSS ile iletişime geçin.

### <a id="HdiRestoreClusterAltered"></a>HdiRestoreClusterAltered
* **Açıklama**: küme *yourClusterName* bakım bir parçası olarak silindi. Merhaba küme oluşturun.
* **Azaltma**: hello küme yeniden oluşturun.

### <a id="HeadNodeConfigNotFound"></a>HeadNodeConfigNotFound
* **Açıklama**: Geçersiz küme yapılandırması. Baş düğüm yapılandırması düğümü boyutları bulunamadı gereklidir.
* **Azaltma**: hello işlemi yeniden deneyin.

### <a id="HostedServiceCreationFailure"></a>HostedServiceCreationFailure
* **Açıklama**: oluşturulamıyor toocreate barındırılan hizmeti *nameOfYourHostedService*. Lütfen isteği yeniden deneyin.  
* **Azaltma**: hello isteği yeniden deneyin.

### <a id="HostedServiceHasProductionDeployment"></a>HostedServiceHasProductionDeployment
* **Açıklama**: barındırılan hizmeti *nameOfYourHostedService* Üretim dağıtımı zaten sahip. Barındırılan bir hizmet birden çok üretim dağıtımları içeremez. Farklı bir küme adı ile Merhaba isteği yeniden deneyin.
* **Azaltma**: farklı bir küme adı kullanın ve hello isteği yeniden deneyin.

### <a id="HostedServiceNotFound"></a>HostedServiceNotFound
* **Açıklama**: barındırılan hizmeti *nameOfYourHostedService* için hello küme bulunamadı.  
* **Azaltma**: hello küme hata durumunda ise, onu silin ve yeniden deneyin.

### <a id="HostedServiceWithNoDeployment"></a>HostedServiceWithNoDeployment
* **Açıklama**: barındırılan hizmeti *nameOfYourHostedService* ilişkili dağıtım sahiptir.  
* **Azaltma**: hello küme hata durumunda ise, onu silin ve yeniden deneyin.

### <a id="InsufficientResourcesCores"></a>InsufficientResourcesCores
* **Açıklama**: Subscriptionıd hello *yourSubscriptionId* çekirdek sol toocreate küme yok *yourClusterName*. Gerekli: *resourcesRequired*, kullanılabilir: *resourcesAvailable*.  
* **Azaltma**: kaynakları aboneliğinizde açmak veya hello kaynakları kullanılabilir toohello abonelik sayısını artırın ve toocreate hello küme yeniden deneyin.

### <a id="InsufficientResourcesHostedServices"></a>InsufficientResourcesHostedServices
* **Açıklama**: abonelik kimliği *yourSubscriptionId* yeni HostedService toocreate kümesi için kota yok *yourClusterName*.  
* **Azaltma**: kaynakları aboneliğinizde açmak veya hello kaynakları kullanılabilir toohello abonelik sayısını artırın ve toocreate hello küme yeniden deneyin.

### <a id="InternalErrorRetryRequest"></a>InternalErrorRetryRequest
* **Açıklama**: hello sunucu bir iç hatayla karşılaştı. Lütfen isteği yeniden deneyin.  
* **Azaltma**: hello isteği yeniden deneyin.

### <a id="InvalidAzureStorageLocation"></a>InvalidAzureStorageLocation
* **Açıklama**: Azure depolama konumu *dataRegionName* geçerli bir konum değil. Merhaba bölge doğru olduğundan emin olun ve isteği yeniden deneyin.
* **Azaltma**: Hdınsight destekleyen bir depolama konumu seçin, kümenizi birlikte bulunan olup olmadığını denetleyin ve hello işlemi yeniden deneyin.

### <a id="InvalidNodeSizeForDataNode"></a>InvalidNodeSizeForDataNode
* **Açıklama**: veri düğümleri için geçersiz VM boyutu. Yalnızca 'Büyük VM' boyutu tüm veri düğümleri için desteklenir.  
* **Azaltma**: hello veri düğümü için desteklenen hello düğüm boyutu belirtin ve hello işlemi yeniden deneyin.

### <a id="InvalidNodeSizeForHeadNode"></a>InvalidNodeSizeForHeadNode
* **Açıklama**: baş düğüm için geçersiz VM boyutu. Yalnızca 'ExtraLarge VM' boyutu baş düğüm için desteklenir.  
* **Azaltma**: hello baş düğüm için desteklenen hello düğüm boyutu belirtin ve hello işlemi yeniden deneyin

### <a id="InvalidRightsForDeploymentDeletion"></a>InvalidRightsForDeploymentDeletion
* **Açıklama**: abonelik kimliği *yourSubscriptionId* kullanılan küme için yeterli izinleri tooexecute silme işlemi yok *yourClusterName*.  
* **Azaltma**: hello küme hata durumunda ise, sürükleyip bırakın ve işlemi yeniden deneyin.  

### <a id="InvalidStorageAccountBlobContainerName"></a>InvalidStorageAccountBlobContainerName
* **Açıklama**: dış depolama hesabı blob kapsayıcı adı *yourContainerName* geçersiz. Ad bir harfle başlayan ve yalnızca küçük harf, sayı ve tire içerdiğinden emin olun.  
* **Azaltma**: geçerli bir depolama hesabı blob kapsayıcı adı belirtin ve hello işlemi yeniden deneyin.

### <a id="InvalidStorageAccountConfigurationSecretKey"></a>InvalidStorageAccountConfigurationSecretKey
* **Açıklama**: dış depolama hesabı için yapılandırması *yourStorageAccountName* gizli anahtar ayrıntılarını gerekli toohave olan toobe kümesi.  
* **Azaltma**: hello depolama hesabı için geçerli bir gizli anahtarı belirtin ve hello işlemi yeniden deneyin.

### <a id="InvalidVersionHeaderFormat"></a>InvalidVersionHeaderFormat
* **Açıklama**: sürüm üst bilgisi *yourVersionHeader* geçerli yyyy-aa-gg biçiminde değil  
* **Azaltma**: hello sürüm üst bilgisi için geçerli bir biçim belirtin ve hello isteği yeniden deneyin.

### <a id="MoreThanOneHeadNode"></a>MoreThanOneHeadNode
* **Açıklama**: Geçersiz küme yapılandırması. Birden fazla baş düğüm yapılandırması bulunamadı.  
* **Azaltma**: yalnızca tek bir baş düğüm belirtilen şekilde düzenleme hello yapılandırma.

### <a id="OperationTimedOutRetryRequest"></a>OperationTimedOutRetryRequest
* **Açıklama**: hello işlemi zaman izin hello içinde tamamlanamadı veya hello maksimum yeniden deneme girişimleri mümkün. Lütfen isteği yeniden deneyin.  
* **Azaltma**: hello isteği yeniden deneyin.

### <a id="ParameterNullOrEmpty"></a>ParameterNullOrEmpty
* **Açıklama**: parametre *yourParameterName* null veya boş olamaz.  
* **Azaltma**: hello parametresi için geçerli bir değer belirtin.

### <a id="PreClusterCreationValidationFailure"></a>PreClusterCreationValidationFailure
* **Açıklama**: bir veya daha fazla hello küme oluşturma isteği girdi geçerli değil. Merhaba giriş değerleri doğru olduğundan ve isteği yeniden deneyin emin olun.  
* **Azaltma**: hello giriş değerleri doğru olduğundan ve isteği yeniden deneyin emin olun.

### <a id="RegionCapabilityNotAvailable"></a>RegionCapabilityNotAvailable
* **Açıklama**: bölge yeteneği değil bölgeniz için *yourRegionName* ve abonelik kimliği *yourSubscriptionId*.  
* **Azaltma**: Hdınsight kümeleri destekleyen bir bölge belirtin. Genel olarak desteklenen hello bölgeler: Güneydoğu Asya, Batı Avrupa, Kuzey Avrupa, Doğu ABD veya Batı ABD.

### <a id="StorageAccountNotColocated"></a>StorageAccountNotColocated
* **Açıklama**: depolama hesabı *yourStorageAccountName* bölgede *currentRegionName*. Merhaba küme bölge aynı olmalıdır *yourClusterRegionName*.  
* **Azaltma**: bir depolama hesabı belirtin hello kümenizi bulunduğu aynı bölgede veya verilerinizi hello depolama hesabında zaten varsa, yeni bir küme hello oluşturun hello varolan depolama hesabı ile aynı bölgeye. Merhaba UI hello portalı kullanıyorsanız, bunları bu sorunun önceden bildirir.

### <a id="SubscriptionIdNotActive"></a>SubscriptionIdNotActive
* **Açıklama**: verilen abonelik kimliği *yourSubscriptionId* etkin değil.  
* **Azaltma**: aboneliğinizi yeniden etkinleştirmesini veya yeni bir geçerli abonelik alın.

### <a id="SubscriptionIdNotFound"></a>SubscriptionIdNotFound
* **Açıklama**: abonelik kimliği *yourSubscriptionId* bulunamadı.  
* **Azaltma**: Abonelik Kimliğinizin geçerli olduğundan emin olun ve hello işlemi yeniden deneyin.

### <a id="UnableToResolveDNS"></a>UnableToResolveDNS
* **Açıklama**: oluşturulamıyor tooresolve DNS *yourDnsUrl*. Merhaba blob uç sağlanan için tam hello URL emin olun.  
* **Azaltma**: geçerli blob URL'si sağlayın. Merhaba URL gerekir başlayarak dahil tam olarak geçerli *http://* ve biten *.com*.

### <a id="UnableToVerifyLocationOfResource"></a>UnableToVerifyLocationOfResource
* **Açıklama**: kaynak konumunu oluşturulamıyor tooverify *yourDnsUrl*. Merhaba blob uç sağlanan için tam hello URL emin olun.  
* **Azaltma**: geçerli blob URL'si sağlayın. Merhaba URL gerekir başlayarak dahil tam olarak geçerli *http://* ve biten *.com*.

### <a id="VersionCapabilityNotAvailable"></a>VersionCapabilityNotAvailable
* **Açıklama**: sürüm yetenek sürümü için mevcut değil *specifiedVersion* ve abonelik kimliği *yourSubscriptionId*.  
* **Azaltma**: kullanılabilir bir sürüm seçin ve hello işlemi yeniden deneyin.

### <a id="VersionNotSupported"></a>VersionNotSupported
* **Açıklama**: sürüm *specifiedVersion* desteklenmiyor.
* **Azaltma**: desteklenen bir sürümünü seçin ve hello işlemi yeniden deneyin.

### <a id="VersionNotSupportedInRegion"></a>VersionNotSupportedInRegion
* **Açıklama**: sürüm *specifiedVersion* Azure bölgesinde kullanılamıyor *specifiedRegion*.  
* **Azaltma**: Belirtilen hello bölgede desteklenen bir sürüm seçin ve hello işlemi yeniden deneyin.

### <a id="WasbAccountConfigNotFound"></a>WasbAccountConfigNotFound
* **Açıklama**: Geçersiz küme yapılandırması. Gerekli WASB hesabı yapılandırması dış hesaplarında bulunamadı.  
* **Azaltma**: hello hesabı var ve yapılandırma ve Yeniden Dene'yi hello işlemde doğru belirtildiğinden emin olun.

## <a name="next-steps"></a>Sonraki adımlar
* [Hdınsight üzerinde Ambari görünümleri toodebug Tez işlerinde kullanın](hdinsight-debug-ambari-tez-view.md)
* [Linux tabanlı hdınsight'ta Hadoop Hizmetleri için yığın dökümleri etkinleştir](hdinsight-hadoop-collect-debug-heap-dump-linux.md)
* [Merhaba Ambari Web kullanıcı arabirimini kullanarak Hdınsight kümelerini yönetme](hdinsight-hadoop-manage-ambari.md)

