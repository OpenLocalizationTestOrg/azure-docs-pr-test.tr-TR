---
title: "aaaMigrate, veri ambarı veri tooSQL | Microsoft Docs"
description: "Çözümleri geliştirmek için SQL veri ambarı veri tooAzure geçirmek için ipuçları."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: d78f954a-f54c-4aa4-9040-919bc6414887
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 06/29/2017
ms.author: joeyong;barbkess
ms.openlocfilehash: fe4c6b7e82094c59c45e06be6da225fee1b707ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-data"></a>Verilerinizi geçirme
Veri çeşitli araçları ile SQL veri ambarında farklı kaynaklardan yeniden taşınabilir.  ADF kopyalama, SSIS ve tüm bu hedef kullanılan tooachieve olarak bcp olabilir. Ancak, Hello veri miktarı arttıkça hello veri geçiş işlemi adımlara bölmek hakkında düşünmelisiniz. Bu, ortaya koymaktadır her adım performans ve esneklik tooensure kesintisiz veri geçişi için Fırsat toooptimize hello.

Bu makalede, ilk ADF kopyalama, SSIS ve bcp hello basit geçiş senaryoları açıklanmaktadır. Ardından, görünüm nasıl hello geçiş iyileştirilebilir içine biraz daha derin.

## <a name="azure-data-factory-adf-copy"></a>Azure veri fabrikası (ADF) kopyalama
[ADF kopyalama] [ ADF Copy] parçası olan [Azure Data Factory][Azure Data Factory]. Azure blob depolama alanındaki veya SQL Data Warehouse doğrudan tooremote düz dosyalar tutulan yerel depolama alanında bulunan veri tooflat dosyalarınızı ADF kopyalama tooexport kullanabilirsiniz.

Verilerinizi düz dosyalarda başlatır sonra ilk tootransfer gerekir, yükü başlatmadan önce tooAzure depolama blobu SQL Data Warehouse içine. Azure blob depolama alanına aktarılan Hello verileri sonra toouse seçebilirsiniz [ADF kopyalama] [ ADF Copy] yeniden toopush hello verileri SQL veri ambarı.

PolyBase aynı zamanda hello veri yükleme için yüksek performanslı seçeneği sağlar. Ancak, iki tane yerine araçlarla anlamına gelmez. PolyBase kullanan yeniden hello en iyi performansı gerekiyor durumunda. Bir tek aracı deneyimi istediğiniz (ve hello veri yoğun değil) sonra ADF yanıtınız olur.


> 
> 

Makale için bazı harika aşağıdaki toohello üzerinden baş [ADF örnekleri][ADF samples].

## <a name="integration-services"></a>Tümleştirme Hizmetleri
Integration Services (SSIS) karmaşık iş akışları, veri dönüştürme ve birkaç veri yükleme seçeneklerini destekleyen bir güçlü ve esnek ayıklamak dönüştürme ve yükleme (ETL) aracıdır. SSIS toosimply aktarımı veri tooAzure kullanın veya daha geniş bir geçişin parçası olarak.

> [!NOTE]
> SSIS tooUTF-8 hello dosyasındaki hello Unicode bayt sırası işareti olmadan dışa aktarabilirsiniz. Bu ilk hello kullanmalısınız sütun bileşen tooconvert hello karakter verileri türetilmiş tooconfigure hello veri akışı toouse hello 65001 UTF-8 kod sayfası. Merhaba sütunları dönüştürüldükten sonra hello veri toohello düz dosya hedef bağdaştırıcı 65001 hello hello dosyası için kod sayfası olarak da seçilmiş sağlama yazma.
> 
> 

Yalnızca bu tooa SQL Server dağıtımı bağlandığınız gibi tooSQL veri ambarı SSIS bağlanır. Ancak, bağlantılarınızı bir ADO.NET Bağlantı Yöneticisi'ni kullanarak toobe gerekir. Ayrıca tooconfigure hello "Kullanım toplu ekleme kullanılabilir olduğunda" ilgilenebilmek ayarı toomaximize işleme. Lütfen toohello bakın [ADO.NET hedef bağdaştırıcı] [ ADO.NET destination adapter] makale toolearn bu özellik hakkında daha fazla bilgi

> [!NOTE]
> OLEDB kullanarak SQL Data Warehouse tooAzure bağlanması desteklenmiyor.
> 
> 

Ayrıca, olduğundan her zaman bir paket başarısız olabilir hello olasılığı toothrottling veya ağ sorunları nedeniyle. Tasarım paketleri bunlar olmadan hatası, hello noktada ettirilebilir şekilde yineleme, iş, hello hatasından önce tamamlandı.

Daha fazla bilgi için hello başvurun [SSIS belgelerine][SSIS documentation].

## <a name="bcp"></a>bcp
BCP düz dosya verileri içeri ve dışarı aktarma için tasarlanmış bir komut satırı yardımcı programıdır. Bazı dönüştürme veri dışa aktarma sırasında gerçekleşebilir. tooperform basit dönüşümleri hello veri dönüştürme ve bir sorgu tooselect kullanın. Dışarı sonra hello düz dosyalar ardından doğrudan hello hedef hello SQL Data Warehouse veritabanına yüklenebilir.

> [!NOTE]
> Genellikle, hello kaynak sistemde bir görünümdeki verileri sırasında kullanılan dönüşümleri verme iyi bir fikir tooencapsulate hello olur. Bu hello mantığı korunur ve hello işlem tekrarlanabilir sağlar.
> 
> 

Bcp avantajları şunlardır:

* Basitlik. BCP komutları basit toobuild olan ve yürütme
* Yeniden başlatılabilir yükleme işlemi. Bir kez dışarı aktarılan hello yük olabilir kez herhangi bir sayıda yürütülebilir.

Bcp sınırlamaları vardır:

* BCP tabloda düz dosyalarıyla yalnızca çalışır. Xml veya JSON gibi dosyalarla çalışmıyor
* Veri dönüştürme özellikleri yalnızca sınırlı toohello verme aşama ve doğası gereği basit
* Internet üzerinden verileri yükleme hello zaman bcp uyarlanmış toobe sağlam yedeklenmedi. Ağ kararsızlığa yük hataya neden olabilir.
* BCP hello hedef veritabanı önceki toohello yük bulunmasına hello şema kullanır

Daha fazla bilgi için bkz: [bcp tooload verileri SQL Data Warehouse'a kullanmak][Use bcp tooload data into SQL Data Warehouse].

## <a name="optimizing-data-migration"></a>Veri geçişi en iyi duruma getirme
Bir SQLDW veri taşıma işlemi, üç ayrı adımları etkili bir şekilde ayrılabilir:

1. Kaynak verileri dışa aktarma
2. Veri tooAzure aktarımını
3. Merhaba hedef SQLDW veritabanına yükleyin

Her adım tek başına en iyi duruma getirilmiş toocreate her adımı performansı en üst düzeye çıkaran güçlü, yeniden başlatılabilir ve esnek geçiş işlemi olabilir.

## <a name="optimizing-data-load"></a>En iyi duruma getirme veri yükleme
Bu bir süre için ters sırada bakarak; Merhaba en hızlı yolu tooload PolyBase verilerdir. PolyBase yükleme işlemi için en iyi duruma getirme Önkoşullar en iyi toounderstand olması için bu adımları önceki hello üzerinde ön yerleştirir. Bunlar:

1. Veri dosyaları kodlama
2. Veri dosyalarının biçimi
3. Veri dosyalarının konumu

### <a name="encoding"></a>Encoding
PolyBase, veri dosyalarını toobe UTF-8 veya UTF-16FE gerektirir. 



### <a name="format-of-data-files"></a>Veri dosyalarının biçimi
PolyBase sabit satır Sonlandırıcı \n ya da yeni satır olması zorunlu tutulmuştur. Veri dosyalarınızı toothis standart uygun olmalıdır. Dize veya sütun sonlandırıcılar üzerinde herhangi bir kısıtlamanın değil.

PolyBase, dış tablosunda bir parçası olarak yararlı hello dosyasındaki her sütun toodefine gerekir. Dışarı aktarılan tüm sütunları gereklidir ve hello türleri gerekli toohello standartlarına uygun emin olun.

Lütfen toohello bakın [şemanızı geçir] makale desteklenen veri türleri hakkında ayrıntılı bilgi için.

### <a name="location-of-data-files"></a>Veri dosyalarının konumu
SQL veri ambarı PolyBase tooload verileri Azure Blob depolama biriminden yalnızca kullanır. Sonuç olarak, hello veri ilk blob depolama alanına aktarıldı gerekir.

## <a name="optimizing-data-transfer"></a>En iyi duruma getirme veri aktarımı
Merhaba yavaş bölümleri veri geçişinin hello veri tooAzure hello aktarımını biridir. Yalnızca ağ bant genişliği bir sorun olabilir ancak aynı zamanda ağ güvenilirlik ciddi ilerlemesini. Varsayılan olarak geçirme verilerini tooAzure Internet şekilde hello makul olasılığı olan oluşan aktarımı hatalar olasılığını hello ' dir. Ancak, bu hataları tamamen veya kısmen yeniden gönderilen veri toobe gerektirebilir.

Neyse ki, çeşitli seçenekleri tooimprove hello hızı ve bu işlemin esnekliği vardır:

### <a name="expressrouteexpressroute"></a>[ExpressRoute][ExpressRoute]
Tooconsider kullanarak isteyebilirsiniz [ExpressRoute] [ ExpressRoute] toospeed hello aktarımı ayarlama. [ExpressRoute] [ ExpressRoute] bir özel bağlantı tooAzure sizinle hello bağlantı geçmez şekilde hello genel internet sağlar. Bu halinde zorunlu bir adımdır. Ancak, bu işleme bir şirket içi veri tooAzure Ftp'den zaman artırır veya ortak yerleşim tesisi.

Merhaba kullanmanın yararları [ExpressRoute] [ ExpressRoute] şunlardır:

1. Daha fazla güvenilirlik
2. Daha hızlı ağ hızı
3. Alt ağ gecikmesi
4. daha yüksek ağ güvenliği

[ExpressRoute] [ ExpressRoute] çeşitli senaryoları için faydalıdır; yalnızca, geçiş hello.

İlginizi çekiyor mu? Lütfen fiyatlandırma ve daha fazla bilgi için ziyaret hello [ExpressRoute belgeleri][ExpressRoute documentation].

### <a name="azure-import-and-export-service"></a>Azure içeri ve dışarı aktarma hizmeti
Hello Azure içe aktarma ve dışarı aktarma hizmeti olan büyük (GB ++) toomassive (TB ++) veri aktarımlarını Azure içine için tasarlanmış bir veri aktarım işlemi. Veri toodisks yazma ve tooan Azure veri merkezine sevkiyat içerir. Merhaba disk içeriği sizin adınıza ardından Azure Storage Bloblarında yüklenir.

Üst düzey bir görünümünü hello alma dışa aktarma işlemi aşağıdaki gibidir:

1. Bir Azure Blob Storage kapsayıcısı tooreceive hello verileri yapılandırma
2. Veri toolocal deponuzda dışarı aktarma
3. Merhaba veri too3.5 inç SATA II/III sabit disk hello [Azure içeri/dışarı aktarma aracı] kullanarak sürücüleri kopyalayın
4. Hello Azure içe aktarma ve dışarı aktarma [Azure içeri/dışarı aktarma aracı] hello tarafından üretilen hello günlük dosyaları sağlama hizmeti kullanılarak bir içeri aktarma işi oluşturma
5. Önerilen Azure veri merkezinizin sevk hello diskler
6. Verilerinizi aktarılan tooyour Azure Blob Storage kapsayıcıdır
7. Polybase'i kullanarak SQLDW içine hello veri yükleme

### <a name="azcopyazcopy-utility"></a>[AZCopy][AZCopy] yardımcı programı
Merhaba [AZCopy][AZCopy] Azure Storage Bloblarında aktarılan verilerinizi almak için harika bir aracı programıdır. Küçük (MB ++) toovery büyük (GB ++) veri aktarımları için tasarlanmıştır. [AZCopy] veri tooAzure ve bunu aktarma hello veri aktarımı adım için harika bir seçim olduğunda tasarlanmış tooprovide iyi dayanıklı verimlilik olmuştur. Bir kez aktarılan hello verileri SQL Data Warehouse'a PolyBase kullanarak yükleyebilirsiniz. Ayrıca, bir "Yürütme işlemi" görevini kullanarak, SSIS paketleri AZCopy dahil edebilirsiniz.

toouse AZCopy ilk toodownload ve gerekir yükleyin. Var olan bir [üretim sürümü] [ production version] ve [Önizleme sürümü] [ preview version] kullanılabilir.

tooupload bir dosyanın dosya sisteminizi aşağıda bir hello gibi bir komutu gerekir:

```
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:abc.txt
```

Bir üst düzey işlem özeti aşağıdakilerden biri olabilir:

1. Bir Azure depolama blob kapsayıcısını tooreceive hello verileri yapılandırma
2. Veri toolocal deponuzda dışarı aktarma
3. AZCopy verilerinizi hello Azure Blob Storage kapsayıcısı
4. Hello veri PolyBase kullanarak SQL Data Warehouse'a veri yükleme

Tam belgeleri kullanılabilir: [AZCopy][AZCopy].

## <a name="optimizing-data-export"></a>En iyi duruma getirme verileri dışarı aktarma
Ayrıca hello verme, PolyBase tarafından düzenlendiği toohello gereksinimlerine uyan tooensuring de toooptimize hello verme işleminin hello veri tooimprove hello daha fazla arama.



### <a name="data-compression"></a>Veri sıkıştırma
PolyBase gzip sıkıştırılmış verileri okuyabilir. Daha sonra veri toogzip dosyalarınızı hello hello ağ üzerinden gönderilen veri miktarını en aza indirmiş olursunuz mümkün toocompress varsa.

### <a name="multiple-files"></a>Birden çok dosya
Büyük tablolara pek çok dosya sonu yalnızca değil hızı verme tooimprove yardımcı olur, ayrıca ile re-startability aktarmak ve bir kez hello Azure blob depolama alanındaki hello verilerin genel yönetilebilirlik hello yardımcı olur. PolyBase iyi özelliklerinin çoğu olduğundan, tüm okuyacaksa hello biri bir klasör içindeki dosyaları hello ve bir tablo olarak ele alın. Bu nedenle, bir fikir tooisolate hello dosyaları her tablo kendi klasörüne içindir.

PolyBase "özyinelemeli klasör geçişinin" bilinen bir özellik de destekler. Bu özelliği kullanabilmek için toofurther geliştirmek, dışarı aktarılan verileri tooimprove hello organizasyonu, veri yönetimi.

PolyBase ile veri yükleme hakkında daha fazla toolearn bkz [kullanım PolyBase tooload verileri SQL Data Warehouse][Use PolyBase tooload data into SQL Data Warehouse].

## <a name="next-steps"></a>Sonraki adımlar
Geçiş hakkında daha fazla bilgi için bkz: [, çözüm tooSQL veri ambarına geçirme][Migrate your solution tooSQL Data Warehouse].
Daha fazla geliştirme ipuçları için bkz: [geliştirmeye genel bakış][development overview].

<!--Image references-->

<!--Article references-->
[AZCopy]:../storage/common/storage-use-azcopy.md
[ADF Copy]: ../data-factory/data-factory-data-movement-activities.md 
[ADF samples]: ../data-factory/data-factory-samples.md
[ADF Copy examples]: ../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md
[development overview]: sql-data-warehouse-overview-develop.md
[Migrate your solution tooSQL Data Warehouse]: sql-data-warehouse-overview-migrate.md
[SQL Data Warehouse development overview]: sql-data-warehouse-overview-develop.md
[Use bcp tooload data into SQL Data Warehouse]: sql-data-warehouse-load-with-bcp.md
[Use PolyBase tooload data into SQL Data Warehouse]: sql-data-warehouse-get-started-load-with-polybase.md


<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory]: http://azure.microsoft.com/services/data-factory/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[ExpressRoute documentation]: http://azure.microsoft.com/documentation/services/expressroute/

[production version]: http://aka.ms/downloadazcopy/
[preview version]: http://aka.ms/downloadazcopypr/
[ADO.NET destination adapter]: https://msdn.microsoft.com/library/bb934041.aspx
[SSIS documentation]: https://msdn.microsoft.com/library/ms141026.aspx
