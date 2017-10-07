---
title: "aaaImport ve Azure Redis önbelleği verileri dışarı aktarma | Microsoft Docs"
description: "Bilgi nasıl tooimport ve dışarı aktarma veri tooand premium Azure Redis önbelleği örnekleri ile blob depolama biriminden"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 4a68ac38-87af-4075-adab-569d37d7cc9e
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: sdanie
ms.openlocfilehash: f17464b207f1c652952f4da63ca147473fee2759
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="import-and-export-data-in-azure-redis-cache"></a>İçeri ve dışarı aktarma veri Azure Redis önbelleği
İçeri/dışarı aktarma tooimport veri Azure Redis önbelleği veya Azure Redis önbelleği verme verileri içeri aktarma ve Redis önbelleği veritabanı'nı (RDB) anlık bir Azure premium önbellek tooa blob dışarı aktarma sağlayan bir Azure Redis önbelleği veri yönetimi, bir işlemdir Depolama hesabı. 

- **Dışarı aktarma** -Azure Redis önbelleği RDB anlık görüntüleri tooa sayfa blobu dışarı aktarabilirsiniz.
- **Alma** -sayfa blobu veya bir blok blobu, Redis önbelleği RDB anlık görüntüleri içeri aktarabilirsiniz.

İçeri/dışarı aktarma farklı Azure Redis önbelleği örnekleri arasında toomigrate etkinleştirir veya hello önbellek kullanmadan önce verilerle doldurma.

Bu makalede, Azure Redis önbelleği ile veri alma ve verme için bir kılavuz sağlar ve hello yanıtlar sağlayan sorular toocommonly.

> [!IMPORTANT]
> İçeri/dışarı aktarma Önizleme aşamasındadır ve yalnızca için kullanılabilir [premium katmanı](cache-premium-tier-intro.md) önbelleğe alır.
>
>

## <a name="import"></a>İçeri Aktarma
İçeri aktarma kullanılan toobring Redis uyumlu RDB dosyalarından herhangi bir bulut veya ortamını Linux, Windows ya da herhangi bir bulut sağlayıcısına Amazon Web Hizmetleri ve diğerleri gibi çalışan Redis çalıştıran herhangi bir Redis sunucu olabilir. Veri alma kolay bir yolu toocreate önceden doldurulmuş haldedir verilerle bir önbellek olur. Merhaba içeri aktarma işlemi sırasında Azure Redis önbelleği hello RDB dosyaları Azure Storage'dan belleğe yükler ve sonra hello anahtarları hello önbelleğine ekler.

> [!NOTE]
> Merhaba alma işlemi başlamadan önce Redis veritabanı (RDB) dosya veya dosyalar sayfasına yüklenir blok blobları hello de Azure depolama alanında aynı olduğundan emin olun veya bölge ve Azure Redis önbelleği örneğinizi olarak abonelik. Daha fazla bilgi için bkz: [Azure Blob storage ile çalışmaya başlama](../storage/blobs/storage-dotnet-how-to-use-blobs.md). RDB dosyanızı hello kullanarak veriliyorsa [Azure Redis önbelleği dışarı aktarma](#export) özelliği RDB dosyanızın bir sayfa blob'u zaten depolanır ve içeri aktarmak için hazırdır.
>
>

1. tooimport bir veya daha fazla önbellek BLOB'ları dışarı [tooyour önbelleği Gözat](cache-configure.md#configure-redis-cache-settings) Azure portal hello ve tıklatın **veri içeri aktarma** hello gelen **kaynak menü**.

    ![Veri içeri aktarma][cache-import-data]
2. Tıklatın **seçin Blob(s)** ve hello veri tooimport içeren hello depolama hesabını seçin.

    ![Depolama hesabı seçin][cache-import-choose-storage-account]
3. Merhaba veri tooimport içeren hello kapsayıcı'ı tıklatın.

    ![Kapsayıcı seçin][cache-import-choose-container]
4. Bir veya daha fazla BLOB tooimport hello alanı toohello hello blob adı solundaki tıklayarak seçin ve ardından **seçin**.

    ![BLOB'ları seçin][cache-import-choose-blobs]
5. Tıklatın **alma** toobegin hello içeri aktarma işlemi.

   > [!IMPORTANT]
   > Merhaba önbellek hello içeri aktarma işlemi sırasında önbelleği istemcileri tarafından erişilebilir durumda değil ve hello önbelleğinde mevcut verileri silinir.
   >
   >

    ![İçeri Aktarma][cache-import-blobs]

    Hello Azure portalı aşağıdaki hello bildirimleri tarafından veya hello hello olayları görüntüleyerek hello içeri aktarma işlemi hello ilerlemesini izleyebilirsiniz [denetim günlüğü](../azure-resource-manager/resource-group-audit.md).

    ![İçeri aktarma ilerlemesi][cache-import-data-import-complete]

## <a name="export"></a>Dışarı Aktarma
Dışarı aktarma Azure Redis önbelleği tooRedis uyumlu RDB dosyasında depolanan tooexport hello verileri sağlar. Bu özellik toomove verilerden bir Azure Redis önbelleği örneği tooanother veya tooanother Redis sunucusu kullanabilirsiniz. Hello dışa aktarma işlemi sırasında Azure Redis önbelleği sunucu örneği konakları hello ve depolama hesabı belirlenmiş karşıya yüklenen toohello hello dosyadır VM hello üzerinde geçici bir dosya oluşturulur. Merhaba dışa aktarma işlemi ya da durumunu başarı veya hata ile tamamlandığında hello geçici dosya silindi.

1. tooexport hello geçerli içeriğini hello önbellek toostorage [tooyour önbelleği Gözat](cache-configure.md#configure-redis-cache-settings) Azure portal hello ve tıklatın **dışarı veri** hello gelen **kaynak menü**.

    ![Depolama kapsayıcısı seçin][cache-export-data-choose-storage-container]
2. Tıklatın **depolama kapsayıcısı seçin** ve istenen hello depolama hesabını seçin. Merhaba depolama hesabı hello olmalıdır aynı abonelikte ve bölgede önbelleğiniz.

   > [!IMPORTANT]
   > Klasik ve Resource Manager depolama hesapları tarafından desteklenir, ancak tarafından desteklenmeyen sayfa bloblarını çalışır verme [Blob storage hesapları](../storage/blobs/storage-blob-storage-tiers.md#blob-storage-accounts) şu anda.
   >
   >

    ![Depolama hesabı][cache-export-data-choose-account]
3. Merhaba istenen blob kapsayıcısı ve tıklatın seçin **seçin**. toouse yeni bir kapsayıcı tıklatın **kapsayıcı ekleme** tooadd ilk ve ardından onu hello listeden.

    ![Depolama kapsayıcısı seçin][cache-export-data-container]
4. Bir **Blob adı ön ekini** tıklatıp **verme** toostart hello dışa aktarma işlemi. Bu dışarı aktarma işlemi tarafından oluşturulan dosyaların kullanılan tooprefix hello adlarını Hello blob adı önekidir.

    ![Dışarı Aktarma][cache-export-data]

    Hello Azure portalı aşağıdaki hello bildirimleri tarafından veya hello hello olayları görüntüleyerek hello dışa aktarma işlemi hello ilerlemesini izleyebilirsiniz [denetim günlüğü](../azure-resource-manager/resource-group-audit.md).

    ![Tam Veri dışarı aktarma][cache-export-data-export-complete]

    Önbellekleri hello dışa aktarma işlemi sırasında kullanılabilir kalır.

## <a name="importexport-faq"></a>İçeri/dışarı aktarma ile ilgili SSS
Bu bölümde hello içeri/dışarı aktarma özelliği hakkında sık sorulan sorular bulunmaktadır.

* [Hangi fiyatlandırma katmanlarını içeri/dışarı aktarma kullanabilir miyim?](#what-pricing-tiers-can-use-importexport)
* [Herhangi bir Redis sunucudan verileri alabilir miyim?](#can-i-import-data-from-any-redis-server)
* [Hangi RDB sürümleri alabilirim?](#what-rdb-versions-can-i-import)
* [My önbellek içeri/dışarı aktarma işlemi sırasında var mı?](#is-my-cache-available-during-an-importexport-operation)
* [İçeri/dışarı aktarma ile Redis kümesi kullanabilir miyim?](#can-i-use-importexport-with-redis-cluster)
* [İçeri/dışarı aktarma ayarı için özel bir veritabanlarını nasıl çalışır?](#how-does-importexport-work-with-a-custom-databases-setting)
* [İçeri/dışarı aktarma Redis kalıcılığı farklı mı?](#how-is-importexport-different-from-redis-persistence)
* [İçeri/dışarı aktarma PowerShell'i, CLI veya diğer yönetim istemcileri kullanarak otomatik hale getirebilirsiniz?](#can-i-automate-importexport-using-powershell-cli-or-other-management-clients)
* [My içeri/dışarı aktarma işlemi sırasında zaman aşımı hatası aldım. Ne anlama geliyor?](#i-received-a-timeout-error-during-my-importexport-operation-what-does-it-mean)
* [My veri tooAzure Blob Storage dışarı aktarılırken bir hata ile aldım. Ne oldu?](#i-got-an-error-when-exporting-my-data-to-azure-blob-storage-what-happened)

### <a name="what-pricing-tiers-can-use-importexport"></a>Hangi fiyatlandırma katmanlarını içeri/dışarı aktarma kullanabilir miyim?
İçeri/dışarı aktarma premium fiyatlandırma katmanına yalnızca hello içinde kullanılabilir.

### <a name="can-i-import-data-from-any-redis-server"></a>Herhangi bir Redis sunucudan verileri alabilir miyim?
Evet, ayrıca Azure Redis önbelleği örneklerden verilen tooimporting verileri RDB dosyaları herhangi bir bulut veya Linux, Windows veya Amazon Web Hizmetleri gibi bulut sağlayıcıları gibi ortam çalıştıran herhangi bir Redis sunucudan alabilirsiniz. toodo bu karşıya yükleme hello RDB dosyanızı istenen hello Redis sunucusundan bir sayfa veya blok blobu bir Azure depolama hesabı ve ardından içeri aktarma, premium Azure Redis önbelleği örneğine. Örneğin, üretim önbellekten tooexport hello veri istediğiniz ve test veya geçiş için hazırlama ortamının bir parçası kullanılan bir önbellek içe.

> [!IMPORTANT]
> toosuccessfully verileri kullanarak bir sayfa blobu, hello sayfa blob boyutu 512 baytlık sınırında hizalanmalıdır aktardığınızda Azure Redis önbelleği dışında Redis sunucularından dışarı aktarın. Bayt doldurma gerekli örnek kodu tooperform için bkz: [örnek sayfa blog yüklemesi](https://github.com/JimRoberts-MS/SamplePageBlobUpload).
> 
> 

### <a name="what-rdb-versions-can-i-import"></a>Hangi RDB sürümleri alabilirim?

Azure Redis önbelleği RDB alma sürüm 7 RDB yukarı destekler.

### <a name="is-my-cache-available-during-an-importexport-operation"></a>My önbellek içeri/dışarı aktarma işlemi sırasında var mı?
* **Dışarı aktarma** - önbellekleri kullanılabilir olmaya devam eder ve önbelleğiniz toouse dışa aktarma işlemi sırasında devam edebilirsiniz.
* **Alma** - içe aktarma işlemi başladığında, kullanılamaz hale ve hello içeri aktarma işlemi tamamlandıktan sonra kullanılabilir hale önbellekleri.

### <a name="can-i-use-importexport-with-redis-cluster"></a>İçeri/dışarı aktarma ile Redis kümesi kullanabilir miyim?
Evet, ve, alma/kümelenmemiş bir önbellek ve kümelenmiş bir önbellek arasında verme. Redis kümesi itibaren [destekler 0 veritabanı yalnızca](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering), herhangi bir veri 0 dışında veritabanlarında içe değil. Verileri kümelenmiş önbelleğe alındığı sırada hello anahtarları hello küme hello parça arasında dağıtılır.

### <a name="how-does-importexport-work-with-a-custom-databases-setting"></a>İçeri/dışarı aktarma ayarı için özel bir veritabanlarını nasıl çalışır?
Bazı fiyatlandırma katmanları farklı sahip [veritabanları sınırları](cache-configure.md#databases), böylece bazı noktalar hello için özel bir değer yapılandırdıysanız alırken `databases` önbellek oluşturma sırasında ayarlama.

* Fiyatlandırma katmanı ile bir alt tooa alırken `databases` içinden dışa aktardığınız hello katmanı sınırından:
  * Merhaba varsayılan sayısı kullanıyorsanız `databases`, tüm fiyatlandırma katmanlarına 16 olduğu, veri kaybı olmamasına.
  * Özel bir dizi kullanıyorsanız `databases` hello sınırları içinde düştüğünde hello için içeri aktardığınız toowhich katmanının, veri kaybı olmamasına.
  * Verilen verilerinizi hello yeni katmanının hello sınırlarını aşıyor bir veritabanında veri içeriyorsa, bu daha yüksek veritabanlarındaki hello veriler içe aktarılmaz.

### <a name="how-is-importexport-different-from-redis-persistence"></a>İçeri/dışarı aktarma Redis kalıcılığı farklı mı?
Azure Redis önbelleği kalıcılığı Redis tooAzure depolama depolanan toopersist verileri sağlar. Azure Redis önbelleği Kalıcılık yapılandırıldığında, bir anlık görüntüsünü hello Redis Önbelleği'nde yapılandırılabilir bir yedekleme sıklığına bağlı bir Redis ikili biçimi toodisk devam ettirir. Merhaba birincil ve çoğaltma önbelleği devre dışı bırakan geri dönülemez bir olay meydana gelirse, hello önbellek verilerini hello en son anlık görüntü kullanılarak otomatik olarak geri yüklenir. Daha fazla bilgi için bkz: [nasıl Premium Azure Redis önbelleği için tooconfigure veri kalıcılığını](cache-how-to-premium-persistence.md).

Alma / verme verir toobring verisine veya Azure Redis Önbelleği'den dışarı aktarma. Yedekleme yapılandırması yok ve Redis kalıcılığı kullanarak geri yükleyin.

### <a name="can-i-automate-importexport-using-powershell-cli-or-other-management-clients"></a>İçeri/dışarı aktarma PowerShell'i, CLI veya diğer yönetim istemcileri kullanarak otomatik hale getirebilirsiniz?
Evet, yönergeler için PowerShell bkz [tooimport Redis önbelleği](cache-howto-manage-redis-cache-powershell.md#to-import-a-redis-cache) ve [tooexport Redis önbelleği](cache-howto-manage-redis-cache-powershell.md#to-export-a-redis-cache).

### <a name="i-received-a-timeout-error-during-my-importexport-operation-what-does-it-mean"></a>My içeri/dışarı aktarma işlemi sırasında zaman aşımı hatası aldım. Ne anlama geliyor?
Merhaba üzerinde kalırsa **veri içeri aktarma** veya **dışarı veri** aşağıdaki örneğine bir hata iletisi benzer toohello ile bir hata alıyorsunuz dikey penceresinde hello işlemini başlatmadan önce 15 dakikadan daha uzun süre:

    hello request tooimport data into cache 'contoso55' failed with status 'error' and error 'One of hello SAS URIs provided could not be used for hello following reason: hello SAS token end time (se) must be at least 1 hour from now and hello start time (st), if given, must be at least 15 minutes in hello past.

tooresolve bunu başlatmak hello içeri aktarma veya dışarı aktarma işlemi 15 dakika geçtikten önce.

### <a name="i-got-an-error-when-exporting-my-data-tooazure-blob-storage-what-happened"></a>My veri tooAzure Blob Storage dışarı aktarılırken bir hata ile aldım. Ne oldu?
Sayfa blobları depolanan dosyalarla yalnızca RDB verme çalışır. Diğer blob türleri şu anda, blob storage hesapları sık erişimli ve seyrek katmanları dahil olmak üzere desteklenmez. Daha fazla bilgi için bkz: [Blob storage hesapları](../storage/blobs/storage-blob-storage-tiers.md#blob-storage-accounts).

## <a name="next-steps"></a>Sonraki adımlar
Toouse daha premium özellikleri nasıl önbelleğe alma hakkında bilgi edinin.

* [Giriş toohello Azure Redis önbelleği Premium katmanına](cache-premium-tier-intro.md)    

<!-- IMAGES -->
[cache-settings-import-export-menu]: ./media/cache-how-to-import-export-data/cache-settings-import-export-menu.png
[cache-export-data-choose-account]: ./media/cache-how-to-import-export-data/cache-export-data-choose-account.png
[cache-export-data-choose-storage-container]: ./media/cache-how-to-import-export-data/cache-export-data-choose-storage-container.png
[cache-export-data-container]: ./media/cache-how-to-import-export-data/cache-export-data-container.png
[cache-export-data-export-complete]: ./media/cache-how-to-import-export-data/cache-export-data-export-complete.png
[cache-export-data]: ./media/cache-how-to-import-export-data/cache-export-data.png
[cache-import-data]: ./media/cache-how-to-import-export-data/cache-import-data.png
[cache-import-choose-storage-account]: ./media/cache-how-to-import-export-data/cache-import-choose-storage-account.png
[cache-import-choose-container]: ./media/cache-how-to-import-export-data/cache-import-choose-container.png
[cache-import-choose-blobs]: ./media/cache-how-to-import-export-data/cache-import-choose-blobs.png
[cache-import-blobs]: ./media/cache-how-to-import-export-data/cache-import-blobs.png
[cache-import-data-import-complete]: ./media/cache-how-to-import-export-data/cache-import-data-import-complete.png
