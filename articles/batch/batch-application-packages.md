---
title: "işlem düğümlerinde - Azure Batch uygulama paketleri aaaInstall | Microsoft Docs"
description: "Toplu yükleme için sürümler işlem düğümleri ve kullanım hello uygulama paketleri Özelliği Azure Batch tooeasily birden çok uygulama yönetin."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 3b6044b7-5f65-4a27-9d43-71e1863d16cf
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 07/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 683be7b7f1bd5db7835332016f6dccb72f45c3b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-applications-toocompute-nodes-with-batch-application-packages"></a>Uygulamaları toocompute düğümleri Batch uygulama paketleri ile dağıtma

Azure Batch uygulama paketleri özelliği Hello görev uygulamaları kolay yönetim sağlar ve bunların dağıtım toohello işlem düğümlerini havuzunuzdaki. Uygulama paketleri ile karşıya yükleyin ve birden fazla sürümünü de dahil olmak üzere destek dosyalarını, görevleri çalıştırmak hello uygulamaları yönetin. Ardından otomatik olarak bir dağıtabilirsiniz veya bu uygulamaları toohello fazlasını havuzunuzdaki düğümlerden işlem.

Bu makalede, öğreneceksiniz nasıl tooupload ve hello Azure portal'ın uygulama paketlerini yönetin. Ardından nasıl tooinstall bir havuzun üzerlerinde ile işlem düğümleri öğreneceksiniz hello [Batch .NET] [ api_net] kitaplığı.

> [!NOTE]
> 
> Uygulama paketleri 5 Temmuz 2017’den sonra oluşturulmuş tüm Batch havuzlarında desteklenir. Bunlar yalnızca hello havuzu, bir bulut Hizmeti Yapılandırması kullanılarak oluşturulduysa 10 Mart 2016 ve 5 Temmuz 2017 arasında oluşturulan Batch havuzu üzerinde desteklenir. Önceki too10 Mart 2016 oluşturulan batch havuzları, uygulama paketleri desteklemez.
>
> Merhaba oluşturmak ve uygulama paketleri yönetmek için API hello [Batch yönetimi .NET] parçasıdır [[api_net_mgmt]] kitaplık. Merhaba bir işlem düğümünde uygulama paketleri yüklemek için API hello parçasıdır [Batch .NET] [ api_net] kitaplığı.  
>
> Burada açıklanan hello uygulama paketleri özelliği hello toplu işlem uygulamaları özelliği hello hizmet önceki sürümlerinde kullanılabilir yerini alır.
> 
> 

## <a name="application-package-requirements"></a>Uygulama paketi gereksinimleri
toouse uygulama paketleri, gereksinim duyduğunuz çok[bir Azure depolama hesabı bağlantı](#link-a-storage-account) tooyour toplu işlem hesabı.

Bu özellik sunulmuştur [Batch REST API'si] [ api_rest] sürüm 2015 12 01.2.2 ve hello karşılık gelen [Batch .NET] [ api_net] kitaplığı sürümü 3.1.0. Her zaman hello son API sürümü Batch ile çalışırken kullanmanızı öneririz.

> [!NOTE]
> Uygulama paketleri 5 Temmuz 2017’den sonra oluşturulmuş tüm Batch havuzlarında desteklenir. Bunlar yalnızca hello havuzu, bir bulut Hizmeti Yapılandırması kullanılarak oluşturulduysa 10 Mart 2016 ve 5 Temmuz 2017 arasında oluşturulan Batch havuzu üzerinde desteklenir. Önceki too10 Mart 2016 oluşturulan batch havuzları, uygulama paketleri desteklemez.
>
>

## <a name="about-applications-and-application-packages"></a>Uygulamalar ve uygulama paketleri hakkında
Azure Batch içindeki bir *uygulama* havuzunuzdaki işlem düğümlerine otomatik olarak indirilen toohello olabilir sürümlü ikili dosyaları tooa kümesini ifade eder. Bir *uygulama paketi* tooa başvuruyor *belirli* bu ikili dosyaları ve temsil bir verilen *sürüm* hello uygulamasının.

![Uygulamalar ve uygulama paketleri üst düzey diyagramı][1]

### <a name="applications"></a>Uygulamalar
Toplu bir uygulamada içeriyor veya daha fazla uygulama paketleri ve Merhaba uygulaması için yapılandırma seçeneklerini belirtir. Örneğin, bir uygulama üzerinde işlem düğümlerini ve kendi paketleri olup güncelleştirilmiş veya silinebilir hello varsayılan uygulama paketi sürümü tooinstall belirtebilirsiniz.

### <a name="application-packages"></a>Uygulama paketleri
Bir uygulama paketi hello uygulama ikili dosyaları içeren bir .zip dosyası ve görevleri toorun hello uygulamanız için gerekli destek dosyaları ' dir. Her uygulama paketi hello uygulamanın belirli bir sürümünü temsil eder.

Uygulama paketleri hello havuzu ve görev düzeylerinde belirtebilirsiniz. Bir havuz veya görev oluşturduğunuzda, bir veya daha fazla bu paketleri ve (isteğe bağlı) bir sürüm belirtebilirsiniz.

* **Havuz uygulama paketleri** çok dağıtılan*her* hello havuzdaki düğüm. Bir düğüm bir havuzu katıldığında ve onu yeniden başlatıldığı ya da dağıtılır.
  
    Bir havuzdaki tüm düğümlerin işe ait görevleri yürüttüğünüzde havuzu uygulama paketleri uygundur. Bir veya daha fazla uygulama paketlerini bir havuz oluşturduğunuzda ve ekleme veya güncelleştirme mevcut havuzun paketleri belirtebilirsiniz. Varolan bir havuzun uygulama paketleri güncelleştirirseniz, alt düğümleri tooinstall hello yeni paketi yeniden başlatmanız gerekir.
* **Görev uygulama paketleri** tooa işlem düğümü toorun hello görevin komut satırı çalıştırmadan önce bir görev zamanlanan yalnızca dağıtılır. Uygulama paketi ve sürümü olduğundan zaten hello düğümde Hello belirtilmişse değil imzalanmasını ve hello varolan paket kullanılır.
  
    Görev uygulama paketleri Burada farklı işleri bir havuzu üzerinde çalışır ve bir iş tamamlandığında hello havuzu silinmez paylaşılan havuzu ortamlarında yararlıdır. İşinizi hello havuzunda düğümleri'den daha az görev varsa, görev uygulama paketleri bir uygulamanız görevleri çalıştırmak dağıtılan yalnızca toohello düğümleri olduğundan veri aktarımını en aza indirebilirsiniz.
  
    Büyük bir uygulamayı çalıştırma işleri görev uygulama paketi yararlanabilir diğer senaryolar verilmiştir ancak yalnızca birkaç görevler için. Örneğin, önceden işlem aşama veya hello ön işleme veya birleştirme uygulama ağır olduğu, bir birleştirme görev görev uygulama paketlerini kullanarak yararlanabilir.

> [!IMPORTANT]
> Uygulamalar ve toplu işlem hesabı içindeki uygulama paketleri hello sayısını ve hello en fazla uygulama paket boyutu kısıtlamalar vardır. Bkz: [hello Azure Batch hizmeti için kotalar ve sınırlar](batch-quota-limit.md) bu sınırları hakkında ayrıntılı bilgi için.
> 
> 

### <a name="benefits-of-application-packages"></a>Uygulama paketleri yararları
Uygulama paketleri hello kodu Batch çözümü ve görevlerinizi çalıştırmak alt hello genel gider gerekli toomanage hello uygulamalarınızdaki basitleştirebilirsiniz.

Uygulama paketleri ile havuzun görev başlatma toospecify hello düğümler üzerinde tek tek kaynak dosyaları tooinstall uzun bir listesi sahip değil. Uygulama dosyalarınızı Azure Storage veya düğümlerinizi birden fazla sürümünü yönetmek toomanually yok. Ve oluşturma hakkında tooworry gerekmeyen [SAS URL'leri](../storage/common/storage-dotnet-shared-access-signature-part-1.md) tooprovide depolama hesabınızdaki toohello dosyalara erişim. Merhaba arka planda Azure Storage toostore uygulama paketleri ile Works toplu ve bunları toocompute düğümleri dağıtabilirsiniz.

> [!NOTE] 
> Merhaba toplam boyutu bir başlangıç görevi küçük veya buna eşit olmalıdır kaynak dosyaları ve ortam değişkenleri dahil, too32768 karakteri. Başlangıç görevi bu sınırı aşarsa, uygulama paketleri kullanarak başka bir seçenektir. Ayrıca, kaynak dosyaları içeren bir sıkıştırılmış arşivi oluşturma blob tooAzure depolama karşıya yükleme ve hello komut satırından, başlangıç görevinin sıkıştırmasını açın. 
>
>

## <a name="upload-and-manage-applications"></a>Karşıya yükleme ve uygulamalarını yönetme
Merhaba kullanabilirsiniz [Azure portal] [ portal] veya hello [Batch yönetimi .NET](batch-management-dotnet.md) kitaplığı toomanage hello uygulama paketleri Batch hesabınızdaki. Buna birkaç bölümler sonraki Merhaba, ilk nasıl toolink bir depolama hesabı sonra uygulamalarını ekleyerek ele almaktadır ve paketleri ve bunları yönetme portal hello gösteriyoruz.

### <a name="link-a-storage-account"></a>Bir depolama hesabı bağlantı
toouse uygulama paketleri, ilk Azure Storage hesabı tooyour toplu işlem hesabı bağlamanız gerekir. Henüz bir depolama hesabı yapılandırmadıysanız hello Azure portal uyarı hello hello'ı ilk kez görüntüler **uygulamaları** döşeme hello **Batch hesabı** dikey.

> [!IMPORTANT]
> Batch şu anda destekler *yalnızca* hello **genel amaçlı** 5. adımda açıklandığı gibi depolama hesabı türü [depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account), [Azure hakkında Depolama hesapları](../storage/common/storage-create-storage-account.md). Bir Azure depolama hesabı tooyour toplu işlem hesabı bağladığınızda, bağlantı *yalnızca* bir **genel amaçlı** depolama hesabı.
> 
> 

![Azure portalında 'depolama hesabı yapılandırıldı' uyarısı][9]

Merhaba Batch hizmetini kullanan hello depolama hesabı toostore, uygulama paketlerinizi ilişkilendirilmiş. Merhaba iki hesap bağladığınız sonra toplu hello bağlantılı depolama hesabı tooyour işlem düğümlerine depolanan hello paketleri otomatik olarak dağıtabilirsiniz. toolink bir depolama hesabı tooyour Batch hesabını tıklatın **depolama hesabı ayarlarını** hello üzerinde **uyarı** dikey ve ardından **depolama hesabı** hello üzerinde**Depolama hesabı** dikey.

![Azure Portal'da depolama hesabı dikey seçin][10]

Bir depolama hesabı oluşturmanızı öneririz *özellikle* , toplu işlem hesabı ile kullanmak için ve burada seçin. Hakkında ayrıntılar için toocreate bir depolama hesabı bkz "Bir depolama hesabı oluşturma" [hakkında Azure depolama hesapları](../storage/common/storage-create-storage-account.md). Bir depolama hesabı oluşturduktan sonra daha sonra onu tooyour toplu işlem hesabı hello kullanarak bağlayabilirsiniz **depolama hesabı** dikey.

> [!WARNING]
> Merhaba Batch hizmeti Azure Storage toostore, uygulama paketlerinizi blok blobları kullanır. Olduğunuz [normal olarak ücretlendirilir] [ storage_pricing] hello blok blobu veri. Emin tooconsider hello boyutu ve uygulama paketlerinizi sayısı ve düzenli olarak kullanım dışı paketleri toominimize maliyetleri kaldırın.
> 
> 

### <a name="view-current-applications"></a>Geçerli uygulamaları görüntüle
Batch hesabınızdaki tooview hello Uygulamalar'a tıklayın hello **uygulamaları** hello görüntülerken hello soldaki menüde menü öğesi **Batch hesabı** dikey.

![Uygulamaları döşeme][2]

Bu menü seçeneğini seçerek açar hello **uygulamaları** dikey penceresinde:

![Uygulamaları listeleme][3]

Merhaba **uygulamaları** hesabınızdaki her bir uygulama Kimliğini hello ve aşağıdaki özelliklere hello dikey penceresinde görüntüler:

* **Paketleri**: Merhaba bu uygulamayla ilişkili sürüm sayısı.
* **Varsayılan sürüm**: hello uygulama havuzu için belirttiğinizde bir sürüm belirtmezseniz yüklü hello uygulama sürümü. Bu ayar isteğe bağlıdır.
* **Güncelleştirmelere izin**: olup paketini güncelleştirir, silme ve eklemeleri belirten hello değeri izin verilir. Bu çok ayarlanırsa**Hayır**, paket güncelleştirme ve silme işlemleri hello uygulama için devre dışıdır. Yalnızca yeni uygulama paketi sürümleri eklenebilir. Merhaba varsayılandır **Evet**.

### <a name="view-application-details"></a>Uygulama Ayrıntıları görüntüle
bir uygulama, select hello uygulama hello ayrıntılarını hello içerir tooopen hello dikey **uygulamaları** dikey.

![Uygulama Ayrıntıları][4]

Merhaba uygulama ayrıntıları dikey penceresinde, uygulamanızın ayarlarını aşağıdaki hello yapılandırabilirsiniz.

* **Güncelleştirmelere izin**: uygulama paketlerinin güncelleştirilmiş veya silinebilir olup olmadığını belirtin. Bu makalenin sonraki bölümlerinde "Güncelleştirmek veya bir uygulama paketini silmeniz" bakın.
* **Varsayılan sürüm**: varsayılan uygulama paketi toodeploy toocompute düğüm belirtin.
* **Görünen ad**: kolay bir çözüm hello uygulamayla ilgili bilgileri gibi hello tooyour müşterileri toplu ile sağlayan bir hizmet UI gösterildiğinde kullanabilir, Batch ad belirtin.

### <a name="add-a-new-application"></a>Yeni bir uygulama Ekle
toocreate yeni bir uygulama bir uygulama paketi eklemek ve yeni ve benzersiz uygulama kimliği belirtin. Merhaba yeni uygulama kimliği ile eklediğiniz hello ilk uygulama paketi de hello yeni bir uygulama oluşturur.

Tıklatın **Ekle** hello üzerinde **uygulamaları** dikey tooopen hello **yeni uygulama** dikey.

![Azure portalında yeni uygulama dikey penceresi][5]

Merhaba **yeni uygulama** dikey penceresinde hello aşağıdaki alanlar yeni uygulama ve uygulama paketi toospecify hello ayarlarını sağlar.

**Uygulama Kimliği**

Bu alan konu toohello standart Azure toplu işlem kimliği doğrulama kuralları, yeni uygulama hello Kimliğini belirtir. bir uygulama kimliği sağlamak için hello kurallar aşağıdaki gibidir:

* Windows düğümlerinde hello kimlik alfasayısal karakterler, tire ve alt çizgi, herhangi bir birleşimini içerebilir. Linux düğümleri üzerinde yalnızca alfasayısal karakterler ve alt çizgi izin verilir.
* Birden fazla 64 karakter içeremez.
* Toplu işlem hesabı Hello içinde benzersiz olmalıdır.
* Servis talebi koruyarak ve büyük küçük harf duyarsız ' dir.

**Sürüm**

Bu alan hello uygulama paketini karşıya yüklediğiniz hello sürümünü belirtir. Sürüm dizelerini doğrulama kuralları aşağıdaki konu toohello şunlardır:

* Windows düğümlerinde hello sürüm dizesi alfasayısal karakterler, tire, alt çizgi ve nokta herhangi bir birleşimini içerebilir. Linux düğümleri üzerinde hello sürüm dizesi yalnızca alfasayısal karakterler ve alt çizgi içerebilir.
* Birden fazla 64 karakter içeremez.
* Merhaba uygulama içinde benzersiz olmalıdır.
* Servis talebi koruyarak ve büyük küçük harf duyarsız'dır.

**Uygulama paketi**

Bu alan hello uygulama ikili dosyaları içeren hello .zip dosyası ve gerekli tooexecute Merhaba uygulaması destekleyici dosyaları belirtir. Merhaba tıklatın **bir dosya seçin** kutusu veya hello klasör simgesine toobrowse tooand uygulamanızın dosyaları içeren bir .zip dosyası seçin.

Bir dosyayı seçtikten sonra tıklayın **Tamam** toobegin hello karşıya yükleme tooAzure depolama. Merhaba karşıya yükleme işlemi tamamlandığında hello portalı bir bildirim görüntüler ve hello dikey penceresi kapanır. Merhaba dosya karşıya yükleme ve başlangıç hızı ağ bağlantınızın olduğunu Hello boyutuna bağlı olarak bu işlem biraz zaman alabilir.

> [!WARNING]
> Merhaba kapatmayın **yeni uygulama** hello karşıya yükleme işlemi tamamlanmadan önce dikey. Bunun yapılması hello karşıya yükleme işlemi durdurulacak.
> 
> 

### <a name="add-a-new-application-package"></a>Yeni bir uygulama paketi ekleme
tooadd olan bir uygulamanın yeni bir uygulama Paket sürümü hello bir uygulama seçin **uygulamaları** dikey penceresinde tıklatın **paketleri**, ardından **Ekle** tooopen Merhaba **Ekle paket** dikey.

![Azure portalında uygulama paketi dikey ekleme][8]

Gördüğünüz gibi hello alanları hello eşleşen **yeni uygulama** dikey ancak hello **uygulama kimliği** kutusu devre dışıdır. Merhaba yeni uygulaması için yaptığınız gibi hello belirtin **sürüm** tooyour yeni paketiniz için Gözat **uygulama paketi** .zip dosyası ve ardından **Tamam** tooupload hello Paket.

### <a name="update-or-delete-an-application-package"></a>Güncelleştirme veya uygulama paketi silme
var olan bir uygulama paketini, açık hello ayrıntıları dikey penceresinde hello uygulama tooupdate veya Sil'i tıklatın **paketleri** tooopen hello **paketleri** dikey penceresinde hello tıklatın **üç nokta**toomodify istediğiniz ve seçin tooperform istediğiniz hello eylem hello uygulama paketini hello satırda.

![Güncelleştirme veya Azure portalında paketi silme][7]

**Güncelleştirme**

Tıkladığınızda **güncelleştirme**, hello *güncelleştirme paketini* dikey penceresi görüntülenir. Bu dikey benzer toohello olan *yeni uygulama paketi* toospecify yeni bir ZIP dosyası tooupload izin vererek, ancak yalnızca hello paket seçimi alanını etkin, dikey.

![Güncelleştirme paketi dikey Azure portalında][11]

**Silme**

Tıkladığınızda **silmek**tooconfirm hello hello Paket sürümü silinmesini sorulur ve toplu Azure depolama biriminden hello paketini siler. Bir uygulamanın hello varsayılan sürümü silerseniz, hello **varsayılan sürüm** ayarı Merhaba uygulaması kaldırılır.

![Uygulama silme][12]

## <a name="install-applications-on-compute-nodes"></a>İşlem düğümlerinde uygulamaları yükleme
Artık nasıl hello Azure portal ile toomanage uygulama paketleri öğrendiğinize göre aşağıdakiler ele nasıl toodeploy bunları toocompute düğümleri ve toplu işlem görevleri ile çalıştırın.

### <a name="install-pool-application-packages"></a>Havuz uygulama paketlerini yükleme
tooinstall bir uygulama paketi tüm işlem düğümleri havuzunda, bir veya daha fazla uygulama paketi belirleyin *başvuruları* hello havuzu için. için bir havuz belirtin hello uygulama paketlerini her işlem düğümünde bu düğüme hello havuzu katıldığında ve hello düğümün yeniden başlatıldığı ya da zaman yüklenir.

Batch .NET içinde bir veya daha fazla belirtin [CloudPool][net_cloudpool].[ ApplicationPackageReferences] [ net_cloudpool_pkgref] yeni bir havuz oluşturduğunuzda veya mevcut bir havuzu. Merhaba [ApplicationPackageReference] [ net_pkgref] sınıfı, bir uygulama kimliği ve sürüm tooinstall bulunan bir havuzdaki işlem düğümleri belirtir.

```csharp
// Create hello unbound CloudPool
CloudPool myCloudPool =
    batchClient.PoolOperations.CreatePool(
        poolId: "myPool",
        targetDedicatedComputeNodes: 1,
        virtualMachineSize: "small",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

// Specify hello application and version tooinstall on hello compute nodes
myCloudPool.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference {
        ApplicationId = "litware",
        Version = "1.1001.2b" }
};

// Commit hello pool so that it's created in hello Batch service. As hello nodes join
// hello pool, hello specified application package is installed on each.
await myCloudPool.CommitAsync();
```

> [!IMPORTANT]
> Bir uygulama paketi dağıtım için herhangi bir nedenle başarısız olursa, düğümün hello Batch hizmeti işaretleri hello [kullanılamaz][net_nodestate], ve bu düğümde yürütülmek zamanlanmış hiçbir görevler. Bu durumda, aşağıdakileri yapmalısınız **yeniden** hello düğümü tooreinitiate hello paketi dağıtımı. Görev hello düğümde yeniden zamanlamayı yeniden başlatmayı hello düğümü de sağlar.
> 
> 

### <a name="install-task-application-packages"></a>Görev uygulama paketlerini yükleme
Benzer tooa havuzu, belirttiğiniz uygulama paketi *başvuruları* bir görev için. Bir görev bir düğüm üzerinde zamanlanmış toorun olduğunda hello paket indirilir ve yalnızca hello görevin komut satırı yürütülmeden önce ayıklanan. Belirtilen paket ve sürümü zaten yüklüyse hello düğümde, hello paket yüklenmez ve hello mevcut paketi kullanılır.

tooinstall bir görev uygulama paketi yapılandırma hello görevin [CloudTask][net_cloudtask].[ ApplicationPackageReferences] [ net_cloudtask_pkgref] özelliği:

```csharp
CloudTask task =
    new CloudTask(
        "litwaretask001",
        "cmd /c %AZ_BATCH_APP_PACKAGE_LITWARE%\\litware.exe -args -here");

task.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference
    {
        ApplicationId = "litware",
        Version = "1.1001.2b"
    }
};
```

## <a name="execute-hello-installed-applications"></a>Merhaba yüklü uygulamaları yürütme
Merhaba, bir havuz ya da görev için belirttiğiniz paketleri karşıdan yüklenir ve hello dizininde adlı tooa ayıklanan `AZ_BATCH_ROOT_DIR` hello düğümü. Toplu dizin adlı hello yolu toohello içeren bir ortam değişkeni de oluşturur. Görev komut satırları Merhaba uygulaması hello düğümde başvururken bu ortam değişkenini kullanın. 

Windows düğümlerinde hello biçimini izleyen hello değişkenidir:

```
Windows:
AZ_BATCH_APP_PACKAGE_APPLICATIONID#version
```

Linux düğümleri üzerinde hello biçimi biraz farklıdır. Nokta (.), kısa çizgi (-) ve numara işareti (#) olduğundan hello ortam değişkeninde düzleştirilmiş toounderscores. Örneğin:

```
Linux:
AZ_BATCH_APP_PACKAGE_APPLICATIONID_version
```

`APPLICATIONID`ve `version` toohello uygulama ve Paket sürümü dağıtımı için belirtilen karşılık gelen değerler. Örneğin, uygulama sürümünün 2.7 belirtilmişse *blender* yüklenmesi gereken Windows düğümlerinde dosyalarından bu ortam değişkeni tooaccess görev komut satırları kullanır:

```
Windows:
AZ_BATCH_APP_PACKAGE_BLENDER#2.7
```

Linux düğümleri üzerinde hello ortam değişkeni bu biçimde belirtin:

```
Linux:
AZ_BATCH_APP_PACKAGE_BLENDER_2_7
``` 

Bir uygulama paketini karşıya yüklediğinizde, varsayılan sürüm toodeploy tooyour işlem düğümlerini belirtebilirsiniz. Bir uygulama için varsayılan bir sürümünün belirtilmişse Merhaba uygulaması başvurduğunuzda hello Sürüm soneki atlayabilirsiniz. Merhaba varsayılan uygulama sürümü hello hello uygulamalar dikey penceresinde, Azure portal gösterildiği gibi belirleyebilirsiniz [karşıya yükleyin ve uygulamalarını yönetin](#upload-and-manage-applications).

Örneğin, "2.7" Merhaba uygulama için varsayılan sürüm olarak ayarlarsanız *blender*ve görevlerinizi ortam değişkeni aşağıdaki hello başvuru, sonra Windows düğümleriniz sürüm 2.7 çalıştırır:

`AZ_BATCH_APP_PACKAGE_BLENDER`

Merhaba aşağıdaki kod parçacığını gösterir hello hello varsayılan sürümü başlatan bir örnek görev komut satırı *blender* uygulama:

```csharp
string taskId = "blendertask01";
string commandLine =
    @"cmd /c %AZ_BATCH_APP_PACKAGE_BLENDER%\blender.exe -args -here";
CloudTask blenderTask = new CloudTask(taskId, commandLine);
```

> [!TIP]
> Bkz: [görevler için ortam ayarları](batch-api-basics.md#environment-settings-for-tasks) hello içinde [Batch özelliklerine genel bakış](batch-api-basics.md) işlem düğümü ortam ayarları hakkında daha fazla bilgi.
> 
> 

## <a name="update-a-pools-application-packages"></a>Bir havuzun uygulama paketlerini güncelleştirme
Var olan bir havuzu bir uygulama paketiyle yapılandırılmış hello havuzu için yeni bir paket belirtebilirsiniz. Bir havuz için yeni bir paket başvuru belirtirseniz, hello aşağıdakileri uygulayın:

* Hello Batch hizmeti hello havuzuna Katıl tüm yeni düğümler ve herhangi bir düğümde, yeniden başlatıldığı ya da varolan hello yeni belirtilen paketi yükler.
* Merhaba paket referanslarını güncelleştirdiğinizde zaten hello havuzunda düğümlerini hello yeni uygulama paketi otomatik olarak yüklemeyin işlem. Bu, düğümlerin yeniden başlatılması gerekiyor veya görüntülenen tooreceive hello yeni paket işlem.
* Yeni bir paket dağıtıldığında, ortam değişkenleri oluşturulan hello hello yeni uygulama paket referanslarını yansıtır.

Bu örnekte, hello varolan havuzu hello 2.7 sürümüne sahip *blender* biri olarak yapılandırılmış bir uygulama, [CloudPool][net_cloudpool].[ ApplicationPackageReferences][net_cloudpool_pkgref]. Yeni bir sürümle 2.76b, tooupdate hello havuzun düğümleri belirtin [ApplicationPackageReference] [ net_pkgref] hello yeni sürümü ve yürütme hello değiştirin.

```csharp
string newVersion = "2.76b";
CloudPool boundPool = await batchClient.PoolOperations.GetPoolAsync("myPool");
boundPool.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference {
        ApplicationId = "blender",
        Version = newVersion }
};
await boundPool.CommitAsync();
```

Merhaba yeni sürümü yapılandırıldı, hello Batch hizmeti sürüm 2.76b tooany yükler *yeni* hello havuzuna katılır düğümü. Merhaba düğümleri üzerinde tooinstall 2.76b *zaten* hello havuzundaki yeniden veya onları yeniden görüntü oluşturma. Yeniden başlatılan düğümleri önceki paket dağıtımlarından hello dosyaları korumak unutmayın.

## <a name="list-hello-applications-in-a-batch-account"></a>Bir Batch hesabında hello uygulamaları listeleme
Hello kullanarak hello uygulamaları ve bunların paketleri bir Batch hesabında listeleyebilirsiniz [ApplicationOperations][net_appops].[ ListApplicationSummaries] [ net_appops_listappsummaries] yöntemi.

```csharp
// List hello applications and their application packages in hello Batch account.
List<ApplicationSummary> applications = await batchClient.ApplicationOperations.ListApplicationSummaries().ToListAsync();
foreach (ApplicationSummary app in applications)
{
    Console.WriteLine("ID: {0} | Display Name: {1}", app.Id, app.DisplayName);

    foreach (string version in app.Versions)
    {
        Console.WriteLine("  {0}", version);
    }
}
```

## <a name="wrap-up"></a>Kaydırma
Uygulama paketleri ile işlerini hello uygulamaları seçin ve Batch özellikli hizmetinizi işleriyle işlerken hello tam sürümünü toouse belirtin, müşterilerinizin yardımcı olabilir. Ayrıca, hizmetinizi kendi uygulamaları izlemek için müşteriler tooupload hello olanağı sunar. ve.

## <a name="next-steps"></a>Sonraki adımlar
* Merhaba [Batch REST API'si] [ api_rest] destek toowork ile uygulama paketleri de sağlar. Örneğin, hello bkz [applicationPackageReferences] [ rest_add_pool_with_packages] öğesinde [bir havuz tooan hesabı eklemek] [ rest_add_pool] hakkında bilgi için toospecify tooinstall hello REST API kullanarak paketler. Bkz: [uygulamaları] [ rest_applications] nasıl tooobtain uygulama bilgilerini kullanarak hello Batch REST API'si hakkında ayrıntılar için.
* Bilgi nasıl tooprogrammatically [Azure Batch hesaplarını ve kotalarını Batch yönetimi .NET ile yönetme](batch-management-dotnet.md). Merhaba [Batch yönetimi .NET][api_net_mgmt] kitaplığı, toplu uygulama veya hizmet hesabı oluşturma ve silme özellikleri etkinleştirebilir.

[api_net]: https://docs.microsoft.com/dotnet/api/overview/azure/batch/client?view=azure-dotnet
[api_net_mgmt]: https://docs.microsoft.com/dotnet/api/overview/azure/batch/management?view=azure-dotnet
[api_rest]: https://docs.microsoft.com/en-us/rest/api/batchservice/
[batch_mgmt_nuget]: https://www.nuget.org/packages/Microsoft.Azure.Management.Batch/
[github_samples]: https://github.com/Azure/azure-batch-samples
[storage_pricing]: https://azure.microsoft.com/pricing/details/storage/
[net_appops]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationoperations.aspx
[net_appops_listappsummaries]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationoperations.listapplicationsummaries.aspx
[net_cloudpool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_cloudpool_pkgref]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.applicationpackagereferences.aspx
[net_cloudtask]: https://msdn.microsoft.com/library/microsoft.azure.batch.cloudtask.aspx
[net_cloudtask_pkgref]: https://msdn.microsoft.com/library/microsoft.azure.batch.cloudtask.applicationpackagereferences.aspx
[net_nodestate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.state.aspx
[net_pkgref]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationpackagereference.aspx
[portal]: https://portal.azure.com
[rest_applications]: https://msdn.microsoft.com/library/azure/mt643945.aspx
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[rest_add_pool_with_packages]: https://msdn.microsoft.com/library/azure/dn820174.aspx#bk_apkgreference

[1]: ./media/batch-application-packages/app_pkg_01.png "Uygulama paketleri üst düzey diyagramı"
[2]: ./media/batch-application-packages/app_pkg_02.png "Azure portalında uygulamaları kutucuğu"
[3]: ./media/batch-application-packages/app_pkg_03.png "Azure portalında uygulamalar dikey penceresi"
[4]: ./media/batch-application-packages/app_pkg_04.png "Uygulama Ayrıntıları dikey Azure portalında"
[5]: ./media/batch-application-packages/app_pkg_05.png "Azure portalında yeni uygulama dikey penceresi"
[7]: ./media/batch-application-packages/app_pkg_07.png "Update veya delete paketleri açılan Azure portalında"
[8]: ./media/batch-application-packages/app_pkg_08.png "Azure portalında yeni uygulama paketi dikey penceresi"
[9]: ./media/batch-application-packages/app_pkg_09.png "Bağlantılı Depolama hesabı uyarı"
[10]: ./media/batch-application-packages/app_pkg_10.png "Azure Portal'da depolama hesabı dikey seçin"
[11]: ./media/batch-application-packages/app_pkg_11.png "Güncelleştirme paketi dikey Azure portalında"
[12]: ./media/batch-application-packages/app_pkg_12.png "Azure portalında paket onay iletişim Sil"
