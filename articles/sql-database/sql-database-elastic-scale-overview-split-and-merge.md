---
title: "ölçeklendirilen bulut veritabanları arasında aaaMoving verileri | Microsoft Docs"
description: "API toomanipulate parça ve esnek kullanarak bir kendi kendini barındıran hizmet aracılığıyla taşıma verilerine nasıl veritabanı açıklanmaktadır."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 204fd902-0397-4185-985a-dea3ed7c7d9f
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 629dee06e22609e9b61edf93ba5c38d997132d8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="moving-data-between-scaled-out-cloud-databases"></a>Ölçeği genişletilen bulut veritabanları arasında veri taşıma
Bir hizmet geliştiricisi olarak yazılımlardır ve uygulamanızı inanılmaz isteğe bağlı aniden uğradığında tooaccommodate hello büyüme gerekir. Bu nedenle daha fazla veritabanı (bölümler) ekleyin. Nasıl hello veri bütünlüğü kesintiye uğratmadan hello veri toohello yeni veritabanları dağıtabilir? Kullanım hello **bölünmüş Birleştirme aracı** kısıtlanmış toomove verilerden veritabanları toohello yeni veritabanları.  

Merhaba bölünmüş Birleştirme aracı bir Azure web hizmeti olarak çalışır. Bir yönetici veya Geliştirici farklı veritabanları (bölümler) arasında hello aracı toomove shardlets (bir parça verilerden) kullanır. Merhaba aracı parça eşleme yönetim toomaintain hello hizmeti meta veri veritabanı kullanır ve tutarlı eşlemeleri emin olun.

![Genel Bakış][1]

## <a name="download"></a>İndir
[Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge/)

## <a name="documentation"></a>Belgeler
1. [Esnek veritabanı bölünmüş Birleştirme aracı Öğreticisi](sql-database-elastic-scale-configure-deploy-split-and-merge.md)
2. [Bölünmüş birleştirme güvenlik yapılandırması](sql-database-elastic-scale-split-merge-security-configuration.md)
3. [Bölünmüş birleştirme güvenlik konuları](sql-database-elastic-scale-split-merge-security-configuration.md)
4. [Parça eşleme yönetimi](sql-database-elastic-scale-shard-map-management.md)
5. [Varolan veritabanları tooscale kullanıma geçirme](sql-database-elastic-convert-to-use-elastic-tools.md)
6. [Esnek veritabanı araçları](sql-database-elastic-scale-introduction.md)
7. [Esnek veritabanı araçlarını sözlüğü](sql-database-elastic-scale-glossary.md)

## <a name="why-use-hello-split-merge-tool"></a>Merhaba bölünmüş Birleştirme aracı neden kullanılır?
**Esneklik**

Uygulamaları tek bir Azure SQL DB veritabanı hello sınırları dışına esnek toostretch gerekir. Merhaba aracı toomove veri bütünlüğü korurken gerekli toonew veritabanları olarak kullanın.

**Bölünmüş toogrow** 

Genel tooincrease gereken kapasite toohandle Patlayıcı büyüme. toodo bu nedenle, oluşturma ek kapasite parçalama hello veri ve tarafından kapasite gereksinimleri karşılandıktan kadar artımlı olarak daha fazla veritabanı arasında dağıtma. Bu, 'bölme' hello özelliğinin prime bir örnektir. 

**Tooshrink birleştirme**

Kapasite toohello Mevsimlik yapısını iş Küçült. İş yavaşlatır zaman toofewer ölçek birimleri ölçeklendirme hello araç sağlar. Merhaba esnek ölçek bölme birleştirme hizmetine Hello 'merge' özelliği bu gereksinim kapsar. 

**Etkin noktalarına shardlets taşıyarak yönetme**

Veritabanı başına birden çok Kiracı ile üzerinde bazı parça toocapacity performans sorunlarını shardlets tooshards hello ayrılması yol açabilir. Bu, shardlets yeniden ayırma veya meşgul shardlets toonew veya daha az kullanılan parça taşımayı gerektirir. 

## <a name="concepts--key-features"></a>Kavramları ve anahtar özellikler
**Müşteri barındırılan hizmetleri**

Merhaba bölünmüş birleştirme müşteri tarafından barındırılan bir hizmet olarak teslim edilir. Dağıtmak ve Microsoft Azure aboneliğiniz hello hizmetini barındırır. Nuget'ten yükleme hello paketi yapılandırma şablonu toocomplete belirli dağıtımınız için hello bilgilerle içerir. Merhaba bkz [bölünmüş birleştirme öğretici](sql-database-elastic-scale-configure-deploy-split-and-merge.md) Ayrıntılar için. Azure aboneliğinizde Hello hizmeti çalışır olduğundan, denetlemek ve hello hizmet çoğu güvenlik özelliklerini yapılandırın. Merhaba varsayılan şablon hello seçenekleri tooconfigure SSL, istemci sertifika tabanlı kimlik doğrulaması, şifreleme için depolanan kimlik bilgileri, kullanılan koruyarak DoS ve IP kısıtlamaları içerir. Belge aşağıdaki hello güvenlik yönünden hello hakkında daha fazla bilgi bulabilirsiniz [bölünmüş birleştirme Güvenlik Yapılandırması](sql-database-elastic-scale-split-merge-security-configuration.md).

Merhaba varsayılan hizmeti çalıştığında bir çalışan ve bir web rolü ile birlikte dağıtılır. Her Azure Cloud Services hello A1 VM boyutu kullanır. Merhaba paketini dağıtırken bu ayarları değiştiremezsiniz, ancak bir bulut hizmeti (hello Azure portalı) çalıştıran hello başarılı dağıtım sonrasında değiştirebilir. Bu hello çalışan rolü birden çok tek bir örnek için teknik nedenlerle yapılandırılmamalıdır unutmayın. 

**Parça eşleme tümleştirme**

Merhaba bölünmüş birleştirme hizmetine hello parça haritasını Merhaba uygulaması ile etkileşime girer. Merhaba bölünmüş birleştirme hizmetine toosplit veya birleştirme aralıkları veya toomove shardlets arasında parça kullanırken, hello hizmet toodate hello parça harita otomatik olarak tutar. toodo bu nedenle, hello hizmet toohello parça eşleme Yöneticisi veritabanı hello uygulamasının bağlanır ve aralıkları ve eşlemeleri birleştirme/bölünmüş/taşıma isteği ilerleme durumunu korur. Bölünmüş birleştirme işlemleri yükleyecekseniz bu hello parça eşlenen her zaman sunar güncel bir görünüm sağlar. Bölme, birleştirme ve shardlet taşıma işlemleri hello kaynak parça toohello hedef parça shardlets toplu taşıyarak uygulanır. Merhaba shardlet taşıma işlemi hello shardlets konu toohello geçerli toplu işlem sırasında hello parça eşlemesinde çevrimdışı olarak işaretlenir ve hello kullanarak veri bağımlı yönlendirme bağlantılarında kullanılamadığından **OpenConnectionForKey** API. 

**Tutarlı shardlet bağlantıları**

Veri taşıma shardlets yeni toplu için başladığında, tüm parça eşleme sağlanan veri bağımlı yönlendirme bağlantıları toohello parça depolanmasını hello shardlet olan hello parça eşleme bu shardlets engellendi API'leri toohello kli ve sonraki bağlantılarından sırada Merhaba veri taşıma sipariş tooavoid tutarsızlığa sürüyor. Bağlantıları tooother shardlets aynı parça ayrıca sonlandırıldı, ancak yeniden başarılı olur hello üzerinde hemen üzerinde yeniden deneyin. Hello toplu taşındıktan sonra hello shardlets yeniden hello hedef parça için çevrimiçi olarak işaretlenir ve hello kaynak parça hello kaynak verileri kaldırılır. Tüm shardlets taşınana kadar hello hizmeti her toplu işlemi için bu adımları geçer. Bu birleştirme/bölünmüş/taşıma işlemi tamamlamak hello hello sürecinde tooseveral bağlantı sonlandırma işlemleri götürür.  

**Shardlet kullanılabilirlik yönetme**

Yukarıda açıklanan şekilde shardlets toohello geçerli toplu sonlandırılması hello bağlantı sınırlaması shardlets kullanılamazlık tooone toplu hello kapsamını aynı anda kısıtlar. Bu bir yaklaşım hello tam parça bölme veya birleştirme işlemi hello sürecinde burada kendi shardlets için çevrimdışı kalarak tercih edilir. Merhaba aynı anda farklı shardlets toomove hello sayısı olarak tanımlanan bir toplu işin yapılandırma parametresi boyutudur. Her bölme ve birleştirme işleminin hello uygulamanın kullanılabilirliğini ve performansını gereksinimlerine bağlı olarak tanımlanabilir. Merhaba parça eşlemesinde kilitli hello aralık belirtilen hello toplu boyuttan büyük olabileceğine dikkat edin. Hello gerçek hello verilerdeki parçalama anahtar değerlerinin sayısı yaklaşık hello toplu iş boyutu eşleşen şekilde hello hizmet hello aralık boyutu Çekmeleri olmasıdır. Önemli tooremember özellikle seyrek doldurulmuş parçalama tuşları budur. 

**Meta veri depolama**

Merhaba bölünmüş birleştirme hizmeti durumunu ve tookeep günlüklerini isteği işleme sırasında bir veritabanı toomaintain kullanır. Merhaba kullanıcı kendi abonelikte bu veritabanı oluşturur ve hello bağlantı dizesi için hello yapılandırma dosyasındaki hello hizmet dağıtımı sağlar. Merhaba kullanıcının kuruluş yöneticileri aynı zamanda toothis bağlanmak veritabanı tooreview isteği ilerleme ve tooinvestigate ayrıntılı olası hataları ile ilgili bilgiler.

**Parçalama tanıma**

Merhaba bölünmüş birleştirme hizmetine (1) parçalı tabloları, (2) başvuru tabloları ve (3) normal tablolar arasında ayırır. bir birleştirme/bölünmüş/taşıma işlemi Hello semantiği hello kullanılan hello tablo türüne bağlıdır ve şu şekilde tanımlanır: 

* **Parçalı tabloları**: bölünmüş, birleştirme ve taşıma işlemlerini kaynak tootarget parça shardlets taşıyın. Merhaba başarıyla tamamlandıktan sonra genel istek, bu shardlets artık mevcut hello kaynağında. Merhaba hedef tabloları hello hedef parça üzerinde tooexist gerekir ve hello Hedef aralık önceki tooprocessing hello işleminin verilerde içermemelidir unutmayın. 
* **Başvuru tabloları**: başvuru tabloları, hello bölme, birleştirme ve işlemleri hello kaynak toohello hedef parça hello veri kopyalama taşıyın. Ancak, herhangi bir satır zaten bu tabloda hello hedefte varsa, hiçbir değişiklik hello hedef parça belirli bir tabloya ait üzerinde gerçekleşmesini unutmayın. Merhaba tablosu toobe işlenen tüm başvuru tablosu kopyalama işlemi tooget için boş sahiptir.
* **Diğer tablolar**: diğer tablolarla hello kaynak ya da bir bölme ve birleştirme işleminin hello hedef üzerinde bulunabilir. Merhaba bölünmüş birleştirme hizmetine herhangi bir veri taşıma veya kopyalama işlemleri için bu tablolar yok sayar. Ancak, bunlar bu işlemleri kısıtlamaları durumunda olan etkileyebilir unutmayın.

başvuru parçalı tabloları karşılaştırması Hello bilgi hello tarafından sağlanan **SchemaInfo** hello parça eşleme API'leri. Aşağıdaki örnek hello verilen parça eşleme Yöneticisi nesnesi smm bu API'leri hello kullanımını göstermektedir: 

    // Create hello schema annotations 
    SchemaInfo schemaInfo = new SchemaInfo(); 

    // Reference tables 
    schemaInfo.Add(new ReferenceTableInfo("dbo", "region")); 
    schemaInfo.Add(new ReferenceTableInfo("dbo", "nation")); 

    // Sharded tables 
    schemaInfo.Add(new ShardedTableInfo("dbo", "customer", "C_CUSTKEY")); 
    schemaInfo.Add(new ShardedTableInfo("dbo", "orders", "O_CUSTKEY")); 

    // Publish 
    smm.GetSchemaInfoCollection().Add(Configuration.ShardMapName, schemaInfo); 

Merhaba tabloları 'bölge' ve 'ulus' başvuru tabloları tanımlanır ve birleştirme/bölünmüş/taşıma işlemleriyle kopyalanacak. sırayla 'Müşteri' ve 'Siparişler' parçalı tablo olarak tanımlanır. C_CUSTKEY ve O_CUSTKEY hello parçalama anahtarı olarak görev yapar. 

**Bilgi tutarlılığı**

Merhaba bölünmüş birleştirme hizmetine tabloları arasındaki bağımlılıkları analiz eder ve başvuru tabloları ve shardlets taşımak için yabancı anahtar birincil anahtar ilişkileri toostage hello işlem kullanır. Genel olarak, shardlets bağımlılıklarını her yığın içindeki sırasına kopyalanır sonra başvuru tabloları ilk bağımlılık sırayla kopyalanır. Böylece Hello yeni veri ulaştığında hello hedef parça FK PK kısıtlamalar dikkate alınır, bu gereklidir. 

**Parça eşleme tutarlılık ve nihai tamamlama**

Hataları varlığını Merhaba, hello bölünmüş birleştirme hizmet işlemleri herhangi kesinti sonra sürdürür ve toocomplete ilerleme isteklerine birinde amaçlar. Ancak, kurtarılamaz durumlar olabilir, örneğin, hello hedef parça kaybolduğunda veya onarım tehlikeye. Bu koşullar altında hello kaynak parça üzerinde tooreside toobe taşınmış olması bazı shardlets devam edebilir. Merhaba hizmet hello gerekli verileri başarıyla kopyalanan toohello hedef sonra shardlet eşlemeleri yalnızca güncelleştirilmesini sağlar. Shardlets yalnızca hello kaynağında tüm verilerini bırakıldı toohello hedef kopyalanır ve hello karşılık gelen eşlemeleri başarıyla güncelleştirdiniz silinir. Merhaba aralık zaten hello hedef parça üzerinde çevrimiçi durumdayken hello silme işlemi hello arka planda gerçekleşir. Merhaba bölünmüş birleştirme hizmeti her zaman hello parça eşlemesinde depolanan hello eşlemeleri doğruluk sağlar.

## <a name="hello-split-merge-user-interface"></a>Merhaba bölünmüş birleştirme kullanıcı arabirimi
Merhaba bölünmüş birleştirme hizmet paketi çalışan rolü ve bir web rolü içerir. Merhaba web rolü etkileşimli bir şekilde kullanılan toosubmit bölünmüş birleştirme isteği sayısıdır. Merhaba kullanıcı arabirimi ana bileşenlerinin Hello aşağıdaki gibidir:

* İşlem türü: Bu istek için hello hizmeti tarafından gerçekleştirilen işlem hello tür denetleyen radyo düğmesi hello işlemi türüdür. Merhaba bölme arasındaki seçin, birleştirme ve taşıma senaryoları. Ayrıca, daha önce gönderilen işlemi iptal edebilirsiniz. Bölünmüş kullanın, birleştirme ve aralığı parça eşlemeleri için istekleri taşıyın. Liste parça yalnızca destek taşıma işlemleri eşler.
* Parça eşleyin: İstek parametreleri kapak bilgi hello parça eşleme ve hello veritabanı parça haritanızı barındırma hello sonraki bölümü. Özellikle, tooprovide hello hello Azure SQL veritabanı sunucusunun adını ve veritabanı hello shardmap barındırma gerekir, kimlik bilgileri tooconnect toohello parça veritabanı eşleme ve son olarak hello parça eşleme adını hello. Şu anda hello işlemi yalnızca tek bir kimlik bilgileri kümesi kabul eder. Bu kimlik bilgileri toohave yeterli izinlere ihtiyacınız tooperform hello parça toohello kullanıcı verilerine yanı sıra toohello parça eşleme değiştirir.
* Kaynak (bölme ve birleştirme) aralığı: bölme ve birleştirme işlemi, düşük ve yüksek anahtarı kullanarak bir aralık işler. toospecify bir sınırsız yüksek anahtar değeri, onay ile bir işlem, "yüksek anahtar max" onay kutusunu hello ve hello yüksek anahtar alanı boş bırakın. Belirttiğiniz hello aralık anahtar değerleri gerek tooprecisely eşleşmiyor bir eşleme ve kendi sınırları içinde parça eşlemenizi yapın. Tüm aralığı sınırları hiç belirtmezseniz hello hizmet hello en yakın aralığı sizin için otomatik olarak Infer. Verilen parça eşlemesinde hello GetMappings.ps1 PowerShell komut dosyası tooretrieve hello geçerli eşlemelerini kullanabilirsiniz.
* Bölünmüş kaynak davranış (bölme): bölünmüş işlemleri için başlangıç noktası toosplit hello kaynak aralığı tanımlayın. Bunun için toooccur hello bölmek istediğiniz yere hello parçalama anahtarı sağlayarak. Kullanım hello radyo düğmesi hello (anahtar bölme hello hariç) aralığı toomove alt kısmı hello isteyip istemediğiniz veya hello üst kısmındaki toomove (Merhaba bölünmüş anahtar dahil) isteyip istemediğinizi belirtin.
* Kaynak Shardlet (taşıma): işlemleri bölme sonucunda farklı taşımak veya bir aralık toodescribe hello kaynağı gerektirmeyen gibi işlemleri birleştirme. Taşıma için bir kaynak yalnızca toomove planlama hello parçalama anahtar değeri tarafından tanımlanır.
* Hedef parça (bölme): bölme işlemi hello kaynağında hello bilgileri girdikten sonra istediğiniz hello veri toobe kopyalanan tooby sağlayan hello Azure SQL veritabanı sunucusu ve veritabanı adını hello hedef toodefine gerekir.
* Hedef aralık (merge): birleştirme işlemleri shardlets tooan varolan parça taşıyın. Merhaba aralığı sınırları toomerge ile istediğiniz hello varolan aralığın sağlayarak hello varolan parça tanımlayın.
* Toplu iş boyutu: hello toplu iş boyutu denetimleri çevrimdışı hello veri taşıma sırasında zaman gidecek shardlets sayısı hello. Burada shardlets için kapalı kalma süresi hassas toolong dönemlerini olduğunda küçük değerler kullanabilirsiniz bir tamsayı değeri budur. Daha büyük değerler verilen shardlet hello saati artıracaktır çevrimdışı ancak performansı iyileştirebilir.
* İşlem kimliği (İptal): artık gerekli olmadığında devam eden bir işlem varsa, hello işlemi bu alandaki işlem Kimliğini sağlayarak iptal edebilirsiniz. Merhaba istek durumu tablosundan hello işlem kimliği alabilirsiniz (Bölüm 8.1 bakın) veya hello istek gönderildiği hello web tarayıcısında hello çıktısından.

## <a name="requirements-and-limitations"></a>Gereksinimler ve sınırlamalar
Merhaba geçerli hello bölünmüş birleştirme hizmetine uygulamasıdır konu toohello aşağıdaki gereksinimler ve sınırlamalar: 

* Merhaba parça tooexist gerekir ve bu parça üzerinde bir bölme birleştirme işlemi gerçekleştirilmeden önce hello parça eşlemesinde kayıtlı olmalıdır. 
* Merhaba hizmet tablolar veya başka bir veritabanı nesneleri işlemlerinin bir parçası olarak otomatik olarak oluşturmaz. Tüm parçalı tablo için şema hello ve başvuru tabloları deyişle hello hedef parça önceki tooany birleştirme/bölünmüş/taşıma işlemi üzerinde tooexist gerekir. Parçalı tablolar özellikle gerekli toobe yeni shardlets bir birleştirme/bölünmüş/taşıma işlemi tarafından eklenen toobe nerede hello aralıktaki boş değildir. Aksi takdirde hello işlemi hello hedef parça hello ilk tutarlılık denetimi başarısız olur. Ayrıca şekilde tooother eşzamanlı yazma işlemlerinin hello başvuru tabloları ile not hello başvuru tablosu boş ise, başvuru verileri yalnızca kopyalanır ve hiçbir tutarlılık olduğunu güvence altına alır. Bu öneririz: bölünmüş/birleştirme işlemleri çalışırken, başka bir yazma işlemleri toohello başvuru tabloları değişiklikleri yapın.
* Merhaba hizmeti bir benzersiz dizin veya hello parçalama anahtar tooimprove performansı ve güvenilirliği büyük shardlets içeren anahtar tarafından oluşturulan satır kimliği kullanır. Bu değerden yalnızca hello parçalama anahtar bile daha hassas bir ayrıntı düzeyi en hello hizmet toomove verileri sağlar. Bu tooreduce hello maksimum günlük alanının ve hello işlemi sırasında gerekli kilitler yardımcı olur. Benzersiz bir dizin veya birincil anahtar toouse istiyorsanız, belirli bir tablodaki hello parçalama anahtarı da dahil olmak üzere bu tabloyu birleştirme/bölünmüş/taşıma istekleriyle oluşturmayı düşünün. Performans nedenleriyle hello parçalama anahtar hello başında sütununda hello anahtar veya hello dizin olmalıdır.
* İstek işleme Hello sürecinde bazı shardlet veriler hem hello kaynak ve hedef parça hello mevcut olabilir. Merhaba shardlet taşıma sırasında gerekli tooprotect hatalarına karşı budur. Merhaba bölünmüş birleştirme hello parça eşleme ile tümleştirilmesi hello veri bağımlı yönlendirme API'lerini kullanarak aracılığıyla bağlantıları hello sağlar **OpenConnectionForKey** yöntemi hello parça haritaya tutarsız bir ara durum göremezsiniz. Ancak, ne zaman bağlanan toohello kaynak ya da hello hedef parça hello kullanmadan **OpenConnectionForKey** yöntemi, tutarsız Ara durumlar olabilir görünür birleştirme/bölünmüş/taşıma isteği yükleyecekseniz. Bu bağlantıları, kısmi veya yinelenen sonuçları hello zamanlama veya hello parça arka plandaki hello bağlantı bağlı olarak gösterebilir. Bu sınırlama, şu anda esnek ölçek çok-Shard-sorgular tarafından yapılan hello bağlantılar içerir.
* Hello hello bölünmüş birleştirme hizmet için meta veri veritabanı farklı rolleri arasında paylaşılmayan gerekir. Örneğin, hazırlamada çalışan hello bölünmüş birleştirme hizmeti rolü toopoint tooa farklı meta veri veritabanından hello üretim rol daha gerekir.

## <a name="billing"></a>Faturalandırma
Merhaba bölünmüş birleştirme hizmeti Microsoft Azure aboneliğiniz bulut hizmetinde çalışır. Bu nedenle hello hizmeti tooyour örneği ücretleri bulut Hizmetleri için geçerlidir. Birleştirme/bölünmüş/taşıma işlemleri sık gerçekleştirmediğiniz sürece, bölünmüş birleştirme bulut hizmetini silin öneririz. Çalışan maliyetlerini kaydeder veya Bulut hizmeti örnekleri dağıtılır. Yeniden dağıtın ve tooperform ihtiyaç duyduğunuzda taşımalarına runnable yapılandırmanızı Başlat bölme veya birleştirme işlemleri. 

## <a name="monitoring"></a>İzleme
### <a name="status-tables"></a>Durum tabloları
Merhaba bölünmüş birleştirme hello hizmetidir **RequestStatus** tamamlanmış ve devam eden isteklerinin izleme hello meta veri deposu veritabanı tablosunda. Merhaba tablo hello bölünmüş birleştirme hizmetine gönderilen toothis örneğini bırakıldı her bölme birleştirme isteği için bir satır listeler. Her istek için bilgisinden hello sağlar:

* **Zaman damgası**: Merhaba saat ve tarih zaman hello isteği başlatıldı.
* **Operationıd**: hello isteği benzersiz olarak tanımlayan bir GUID. Bu istek kullanılan toocancel hello işlemi hala devam eden de olabilir.
* **Durum**: Merhaba hello isteğin geçerli durumu. Devam eden istekler için Ayrıca hangi hello isteğidir geçerli aşama hello listeler.
* **CancelRequest**: hello isteği iptal olup olmadığını belirten bir bayrak.
* **İlerleme**: hello işleminin tamamlanma yüzdesi tahmin. Bir değeri 50 hello işlemi yaklaşık %50 tamamlanmış olduğunu gösterir.
* **Ayrıntılar**: ayrıntılı ilerleme raporu sağlar XML değeri. satır kümeleri kaynak tootarget kopyalanır gibi hello İlerleme raporu düzenli olarak güncelleştirilir. Hataları veya özel durumları durumunda bu sütun ayrıca hello hatayla ilgili daha ayrıntılı bilgiler içerir.

### <a name="azure-diagnostics"></a>Azure Tanılama
Merhaba bölünmüş birleştirme hizmeti Azure Tanılama izleme ve tanılama için Azure SDK 2.5 üzerinde temel kullanır. Burada açıklandığı gibi hello Tanılama yapılandırmasını kontrol: [Azure Cloud Services ve sanal makineleri etkinleştirme tanılamada](../cloud-services/cloud-services-dotnet-diagnostics.md). Merhaba yükleme paketini içeren iki tanılama yapılandırması - hello web rolü, diğeri hello çalışan rolü için için. Merhaba hizmet için bu tanılama yapılandırmalar hello kılavuzluğu izleyin [Microsoft Azure bulut hizmeti temel bilgileri](https://code.msdn.microsoft.com/windowsazure/Cloud-Service-Fundamentals-4ca72649). Merhaba tanımları toolog performans sayaçları, IIS günlükleri, Windows olay günlüklerini ve bölünmüş birleştirme uygulama olay günlükleri içerir. 

## <a name="deploy-diagnostics"></a>Tanılama dağıtma
tooenable izleme ve tanılama hello web ve çalışan rolleri Azure PowerShell kullanarak komutları aşağıdaki hello çalıştırmak hello NuGet paketi tarafından sağlanan hello tanılama Yapılandırması'nı kullanarak: 

    $storage_name = "<YourAzureStorageAccount>" 

    $key = "<YourAzureStorageAccountKey" 

    $storageContext = New-AzureStorageContext -StorageAccountName $storage_name -StorageAccountKey $key  


    $config_path = "<YourFilePath>\SplitMergeWebContent.diagnostics.xml" 

    $service_name = "<YourCloudServiceName>" 

    Set-AzureServiceDiagnosticsExtension -StorageContext $storageContext -DiagnosticsConfigurationPath $config_path -ServiceName $service_name -Slot Production -Role "SplitMergeWeb" 


    $config_path = "<YourFilePath>\SplitMergeWorkerContent.diagnostics.xml" 

    $service_name = "<YourCloudServiceName>" 

    Set-AzureServiceDiagnosticsExtension -StorageContext $storageContext -DiagnosticsConfigurationPath $config_path -ServiceName $service_name -Slot Production -Role "SplitMergeWorker" 

Hakkında daha fazla bilgi bulabilirsiniz tooconfigure ve burada tanılama ayarlarını dağıtma: [Azure Cloud Services ve sanal makineleri etkinleştirme tanılamada](../cloud-services/cloud-services-dotnet-diagnostics.md). 

## <a name="retrieve-diagnostics"></a>Tanılama alma
Visual Studio Sunucu Gezgini hello hello hello Sunucu Gezgini ağacının Azure bölümü, tanılama kolayca erişebilirsiniz. Visual Studio örneğini açın ve hello menü çubuğunda Görünüm ve Server Explorer'ı tıklatın. Hello Azure simgesi tooconnect tooyour Azure aboneliğine tıklayın. Ardından gidin tooAzure depolama -> -> <your storage account> -> tabloları WADLogsTable ->. Daha fazla bilgi için bkz: [Sunucu Gezgini ile depolama kaynaklarını gözatma](http://msdn.microsoft.com/library/azure/ff683677.aspx). 

![WADLogsTable][2]

Merhaba yukarıdaki hello şekilde vurgulanmış WADLogsTable içeren hello ayrıntılı hello bölünmüş birleştirme hizmetin uygulama günlüğündeki olaylar. İndirilen hello bu hello varsayılan yapılandırmasını Not paketi doğru Üretim dağıtımı sağlamıştır. Bu nedenle, günlükleri ve sayaçları hello hizmet örneklerinin alınır hello büyük (5 dakika) aralığıdır. Test ve geliştirme için hello tanılama ayarları hello web veya çalışan rolü tooyour hello ayarlayarak alt hello aralığı gerekiyor. Merhaba rolünde hello Visual Studio Sunucu Gezgini (yukarıya bakın) sağ tıklayın ve sonra hello aktarım süresi hello iletişim hello tanılama yapılandırma ayarlarını değiştirebilirsiniz: 

![Yapılandırma][3]

## <a name="performance"></a>Performans
Genel olarak, daha iyi performans hello yüksek, Azure SQL veritabanında daha fazla kullanıcı hizmet katmanları beklenen toobe ' dir. Merhaba daha yüksek hizmet katmanları için daha yüksek g/ç, CPU ve bellek ayırmaları hello toplu kopyalama yararlanabilir ve bölünmüş birleştirme hizmeti kullanan hello operations silin. Bu nedenle, bu veritabanları için yalnızca hello hizmet katmanına bir tanımlanan, sınırlı süre artırın.

Merhaba hizmeti de doğrulama sorguları normal işlemlerinin bir parçası olarak gerçekleştirir. Bu doğrulama sorgular hello hedef aralığındaki verileri beklenmeyen varlığını denetlemek ve herhangi bir birleştirme/bölünmüş/taşıma işlemi ile tutarlı bir durumdan başladığından emin olmak. Merhaba kapsamını hello işlemi ve hello istek tanımının bir parçası olarak sağlanan hello toplu iş boyutu tarafından tanımlanan parçalama anahtar aralıklarına üzerinden tüm bu sorguları çalışır. Dizin başında sütun hello gibi hello parçalama anahtara sahip mevcut olduğunda bu sorguları en iyi şekilde çalışır. 

Ayrıca, bir Benzersizlik özelliği hello parçalama anahtarla hello başında sütun olarak hello hizmet toouse günlük alanının ve bellek açısından kaynak tüketimini sınırlandırır en iyi duruma getirilmiş bir yaklaşım izin verir. Gerekli toomove büyük veri boyutları (genellikle yukarıdaki 1 GB) bu benzersizlik özelliğidir. 

## <a name="how-tooupgrade"></a>Nasıl tooupgrade
1. Merhaba adımları [bölünmüş birleştirme hizmet dağıtma](sql-database-elastic-scale-configure-deploy-split-and-merge.md).
2. Bulut hizmet yapılandırma dosyası, bölünmüş birleştirme dağıtım tooreflect hello yeni yapılandırma parametrelerini değiştirin. Yeni gerekli parametre hello hello sertifika şifreleme için kullanılan hakkındaki bilgilerdir. Kolay bir yolu toodo toocompare hello yeni yapılandırma şablon dosyasından hello indirme varolan yapılandırmanızı karşı budur. "DataEncryptionPrimaryCertificateThumbprint" ve "DataEncryptionPrimary" Merhaba web ve çalışan rolü hello için hello ayarlarını eklediğinizden emin olun.
3. Merhaba güncelleştirme tooAzure dağıtmadan önce tüm çalışmakta bölünmüş birleştirme işlemlerinin tamamlandığından emin olun. Bu, devam eden istekleri için hello bölünmüş birleştirme meta veri veritabanındaki hello RequestStatus ve PendingWorkflows tabloları sorgulayarak kolayca yapabilirsiniz.
4. Mevcut bulut hizmeti dağıtımınız için bölünmüş birleştirme hello yeni paket Azure aboneliğinizle ve güncelleştirilmiş hizmet yapılandırma dosyanızı güncelleştirin.

Bölünmüş birleştirme tooupgrade tooprovision yeni bir meta veri veritabanı gerekmez. Merhaba yeni sürümü, var olan meta veri veritabanı toohello yeni sürümü otomatik olarak yükseltir. 

## <a name="best-practices--troubleshooting"></a>En iyi yöntemler ve sorun giderme
* Birden fazla parça hello test Kiracı en önemli birleştirme/bölünmüş/taşıma işletim çalışma ve test Kiracı tanımlayın. Tüm meta veriler parça eşlemesinde doğru şekilde tanımlandığından ve hello işlemleri kısıtlamaları veya yabancı anahtarlar ihlal etmemek emin olun.
* Canlı hello test Kiracı veri boyutu hello maksimum veri boyutu en büyük kiracınızın, değil karşılaşmadan veri boyutu tooensure ilgili sorunlar. Bu, tek bir kiracı geçici toomove sürdüğünü hello zamanında bir üst sınır değerlendirmenize yardımcı olur. 
* Şemanızı silme izin verdiğinden emin olun. Merhaba veri başarıyla kopyalanan toohello hedef silindikten sonra hello bölünmüş birleştirme hizmetine hello özelliği tooremove hello kaynak parça verilerden gerektirir. Örneğin, **Tetikleyicileri silme** hello hizmetin hello veri hello kaynağında silmesini önlemek ve işlemleri toofail neden olabilir.
* Merhaba parçalama anahtar hello başında sütun birincil anahtar veya benzersiz dizin tanımı içinde olmalıdır. Doğrulama sorguları, bölme veya birleştirme hello hello için en iyi performans sağlar ve her zaman parçalama anahtar aralıklarına üzerinde çalışan hello gerçek veri taşıma ve silme işlemleri.
* Bölünmüş birleştirme hizmetinizi veritabanlarınızı bulunduğu hello bölgeye ve veri merkezi içinde bir arada. 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Anchors-->
<!--Image references-->
[1]:./media/sql-database-elastic-scale-overview-split-and-merge/split-merge-overview.png
[2]:./media/sql-database-elastic-scale-overview-split-and-merge/diagnostics.png
[3]:./media/sql-database-elastic-scale-overview-split-and-merge/diagnostics-config.png

