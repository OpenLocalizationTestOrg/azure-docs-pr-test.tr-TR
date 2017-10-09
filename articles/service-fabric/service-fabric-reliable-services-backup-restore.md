---
title: "aaaService doku yedekleme ve geri yükleme | Microsoft Docs"
description: "Service Fabric yedekleme ve geri yükleme için kavramsal belgeler"
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: subramar,jessebenson
ms.assetid: 91ea6ca4-cc2a-4155-9823-dcbd0b996349
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: mcoskun
ms.openlocfilehash: e502b59c84999c3fe825167383f00a5ebd70c9b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-and-restore-reliable-services-and-reliable-actors"></a>Ve Reliable Services ve Reliable Actors geri yükleme
Azure Service Fabric hello durumu arasında birden fazla düğüm toomaintain bu yüksek oranda kullanılabilir çoğaltan bir yüksek kullanılabilirlik platformudur.  Bu nedenle, hello kümedeki bir düğümün başarısız olsa bile, hello Hizmetleri toobe kullanılabilir devam edin. Belirli durumlarda daha Hello platform tarafından sağlanan bu-yerleşik artıklık bazı için yeterli olsa bile hello hizmet tooback verileri (tooan dış deposu) için tercih edilir.

> [!NOTE]
> Kritik toobackup olduğundan ve verilerinizi (ve beklendiği gibi çalıştığını test) geri yüklemek için veri kaybı senaryolarını kurtarabilirsiniz.
> 
> 

Örneğin, bir hizmet sırası tooprotect senaryoları aşağıdaki hello gelen verilerini tooback isteyebilirsiniz:

- Merhaba olayı tüm Service Fabric kümesinin hello kalıcı kaybı.
- Bir hizmet bölüm hello çoğaltmalarının çoğunu kalıcı kaybı
- Yapabildiği hello durumu yanlışlıkla silinen bozuk alır veya yönetimsel hatalar. Örneğin, yeterli ayrıcalığa sahip bir yönetici yanlışlıkla hello hizmet silerse bu ortaya çıkabilir.
- Veri bozulmasına neden hatalar hello hizmetindeki. Örneğin, bir hizmet kod yükseltme hatalı veri tooa güvenilir koleksiyonu yazma başlatıldığında bu ortaya çıkabilir. Böyle bir durumda, her ikisi de kodu hello ve hello veri toobe olabilir tooan geri önceki belirtin.
- Çevrimdışı veri işleme. Uygun toohave çevrimdışı hello veriler üretir hello hizmetinden ayrı ayrı gerçekleşir iş zekası verileri işlenmesini olabilir.

Merhaba yedekleme/geri yükleme özelliği hello güvenilir Hizmetleri API toocreate ve geri yükleme yedeklemelerin üzerine kurulmuş hizmetler sağlar. Merhaba hello platform tarafından sağlanan yedekleme API'ler engelleme okuma veya yazma işlemleri olmadan bir hizmet bölümünün durumunun yedekleri izin verir. Merhaba geri yükleme API'leri seçilen bir yedekten geri yüklenmiş bir hizmet bölümünün durumu toobe izin verir.

## <a name="types-of-backup"></a>Yedekleme türleri
Yedekleme iki seçenek vardır: tam ve artımlı.
Tam yedekleme tüm hello gerekli verileri toorecreate hello durum hello çoğaltmasının içeren yedeğidir: denetim noktaları ve tüm günlük kayıtları.
Hello kontrol noktalarına ve hello günlük olduğundan, tek başına bir yedekten geri yüklenebilir.

Merhaba kontrol noktaları büyük olduğunda tam yedeklemeler hello sorun ortaya çıkar.
Örneğin, 16 GB durumuna sahip bir çoğaltma yaklaşık too16 GB eklemek kontrol noktaları sahip olur.
Biz beş dakikalık bir kurtarma noktası hedefi varsa hello çoğaltma beş dakikada yedeklenen toobe gerekir.
İsteğe bağlı olarak yedekler her zaman toocopy gereken kontrol noktaları ayrıca 16 GB too50 MB (yapılandırılabilir kullanarak `CheckpointThresholdInMB`) günlükleri tutarında.

![Tam yedekleme örnek.](media/service-fabric-reliable-services-backup-restore/FullBackupExample.PNG)

Merhaba çözüm toothis artımlı yedeklemeler, yedekleme yalnızca değiştirilen hello günlük kayıtlarını hello son yedeklemeden içerdiği bir sorundur.

![Artımlı yedekleme örnek.](media/service-fabric-reliable-services-backup-restore/IncrementalBackupExample.PNG)

Artımlı yedeklemeler yalnızca değişiklikleri (Merhaba kontrol noktalarını içermez) hello son yedeklemeden olduğundan, toobe daha hızlı eğilimindedir ancak bunlar, kendi geri yüklenemez.
toorestore artımlı yedekleme, hello tamamını yedekleme zinciri gereklidir.
Bir yedekleme zinciri, tam yedekleme ile başlayan yedekleme zinciri ve bitişik artımlı yedeklemeler sayısına göre gelmelidir.

## <a name="backup-reliable-services"></a>Yedekleme güvenilir hizmetler
Merhaba hizmet Yazar sahip olduğunda üzerinde tam denetimi toomake yedeklemeler ve yedeklemeleri depolanacağı.

toostart bir yedekleme, hello hizmetin ihtiyaç tooinvoke hello devralınan üye işlevi `BackupAsync`.  
Yedeklemeler yalnızca birincil çoğaltmalardan yapılabilir ve verilen yazma durumu toobe gerektirir.

Aşağıda gösterildiği gibi `BackupAsync` alır bir `BackupDescription` nesnesi, burada bir belirtebilirsiniz bir geri çağırma işlevini yanı sıra, bir tam veya artımlı yedekleme, `Func<< BackupInfo, CancellationToken, Task<bool>>>` hello yedekleme klasörü yerel olarak oluşturulduğundan ve toosome kullanıma hazır toobe taşınır çağrılır harici depolama.

```csharp

BackupDescription myBackupDescription = new BackupDescription(backupOption.Incremental,this.BackupCallbackAsync);

await this.BackupAsync(myBackupDescription);

```

Artımlı yedekleme başarısız olabilir isteği tootake `FabricMissingFullBackupException`. Bu özel bir şey aşağıdaki hello gerçekleşmekte olduğunu gösterir:

- Birincil oldu beri hello çoğaltma hiçbir zaman bir tam yedekleme sürdü,
- Merhaba bazıları günlük kayıtlarının hello son yedekleme kesildi bu yana veya
- Merhaba geçirilen çoğaltma `MaxAccumulatedBackupLogSizeInMB` sınırı.

Kullanıcıların yapılandırarak artımlı yedeklemeler yapabilir toodo olma hello olasılığını artırmak `MinLogSizeInMB` veya `TruncationThresholdFactor`.
Bu değerleri artırılması çoğaltma disk kullanımı başına hello artırır unutmayın.
Daha fazla bilgi için bkz: [güvenilir Hizmetleri Yapılandırması](service-fabric-reliable-services-configuration.md)

`BackupInfo`Merhaba hello çalışma zamanı hello yedekleme kaydedildiği hello klasörünün konumunu dahil olmak üzere, hello yedekleme ile ilgili bilgiler sağlar (`BackupInfo.Directory`). Merhaba geri çağırma işlevi hello taşıyabilirsiniz `BackupInfo.Directory` tooan dış depolama veya başka bir konum.  Bu işlev, ayrıca mümkün toosuccessfully taşıma hello yedekleme klasörü tooits hedef konumu olup olmadığını gösteren bir Boole döndürür.

Merhaba aşağıdaki kodu gösterir nasıl hello `BackupCallbackAsync` yöntemi kullanılan tooupload hello yedekleme tooAzure depolama olabilir:

```csharp
private async Task<bool> BackupCallbackAsync(BackupInfo backupInfo, CancellationToken cancellationToken)
{
    var backupId = Guid.NewGuid();

    await externalBackupStore.UploadBackupFolderAsync(backupInfo.Directory, backupId, cancellationToken);

    return true;
}
```

Merhaba önceki örnekte, `ExternalBackupStore` Azure Blob storage ile kullanılan toointerface hello örnek sınıfı olan ve `UploadBackupFolderAsync` hello klasörü sıkıştırır ve hello Azure Blob deposuna yerleştirir hello yöntemidir.

Şunlara dikkat edin:

  - Olabilir yalnızca bir yedekleme işlemi çoğaltma yürütülen herhangi bir zamanda. Birden fazla `BackupAsync` birer birer çağrısı throw `FabricBackupInProgressException` toolimit ınflight yedeklemeleri tooone.
  - Bir yedekleme işlemi devam ederken bir çoğaltma üzerinde başarısız olursa, hello yedekleme tamamlanmamış. Merhaba yük devretme tamamlandıktan sonra bu nedenle, onu hello hizmetin sorumluluk toorestart hello çağırarak yedeğidir `BackupAsync` gerektiği.

## <a name="restore-reliable-services"></a>Güvenilir Hizmetleri geri yükleme
Genel olarak, bir geri yükleme işlemi tooperform gerektiğinde hello durumlarda bu kategoriden ayrılır:

  - Merhaba hizmeti veri kaybı bölüm. Örneğin, iki üç çoğaltması (Merhaba birincil çoğaltma dahil) bir bölüm için hello disk bozuk temizlenmeden veya. Merhaba yeni birincil toorestore verileri bir yedekten gerekebilir.
  - Merhaba tüm hizmet kaybolur. Örneğin, yönetici hello tüm hizmet kaldırır ve bu nedenle geri toobe hello hizmeti ve hello verileri gerekir.
  - Merhaba hizmet bozuk uygulama verileri (örneğin, bir uygulama hatası nedeniyle) çoğaltılan. Bu durumda, hello hizmet yükseltme toobe veya toobe geri döndürülen tooremove hello nedenini hello bozulması ve bozuk olmayan veri içeriyor.

Birçok yaklaşım mümkün olsa da, kullanarak ilişkin bazı örnekler sunuyoruz `RestoreAsync` senaryoları yukarıda hello gelen toorecover.

## <a name="partition-data-loss-in-reliable-services"></a>Bölüm veri kaybına güvenilir hizmetler
Bu durumda, hello çalışma zamanı otomatik olarak hello veri kaybı algılaması ve hello çağırma `OnDataLossAsync` API.

Merhaba hizmet Yazar toorecover aşağıdaki tooperform hello gerekir:

  - Merhaba sanal temel sınıf yöntemini geçersiz kılın `OnDataLossAsync`.
  - Hello son yedekleme hello hizmetin yedeklemeleri içeren hello dış konumda bulur.
  - Merhaba son yedekleme indirin (ve onu sıkıştırılmış hello yedekleme hello yedekleme klasörüne sıkıştırmasını açın).
  - Merhaba `OnDataLossAsync` yöntemi sağlayan bir `RestoreContext`. Merhaba çağrısı `RestoreAsync` sağlanan hello API `RestoreContext`.
  - Merhaba geri yükleme başarılı olursa true döndürür.

Aşağıdadır hello örnek uygulaması `OnDataLossAsync` yöntemi:

```csharp
protected override async Task<bool> OnDataLossAsync(RestoreContext restoreCtx, CancellationToken cancellationToken)
{
    var backupFolder = await this.externalBackupStore.DownloadLastBackupAsync(cancellationToken);

    var restoreDescription = new RestoreDescription(backupFolder);

    await restoreCtx.RestoreAsync(restoreDescription);

    return true;
}
```

`RestoreDescription`içinde toohello geçirilen `RestoreContext.RestoreAsync` çağrı içerir adında bir üyeye `BackupFolderPath`.
Tek bir tam yedekleme geri yüklerken bu `BackupFolderPath` tam yedekleme içeren hello klasörün yerel yol toohello ayarlamanız gerekir.
Tam yedekleme ve artımlı yedeklemeler, bir dizi geri yüklerken `BackupFolderPath` hello tam yedekleme, ancak aynı zamanda tüm hello artımlı yedeklemeler yalnızca içeren hello klasörün yerel yol toohello ayarlamanız gerekir.
`RestoreAsync`Arama throw `FabricMissingFullBackupException` hello varsa `BackupFolderPath` sağlanan tam yedekleme içermiyor.
Ayrıca atabilirsiniz `ArgumentException` varsa `BackupFolderPath` artımlı yedeklemeler bozuk zincirine sahiptir.
Örneğin, tam yedekleme hello içeriyorsa, ilk artımlı hello ve üçüncü artımlı yedekleme ancak hiçbir hello ikinci artımlı yedekleme hello.

> [!NOTE]
> Merhaba RestorePolicy tooSafe varsayılan olarak ayarlanır.  Bu hello yani `RestoreAsync` bu hello yedekleme klasörü içerir, bu çoğaltma bulunan eşit veya daha eski toohello durumu bir durum algılarsa, API ArgumentException ile başarısız olur.  `RestorePolicy.Force`kullanılan tooskip bu güvenlik denetimi olabilir. Bu bir parçası olarak belirtilen `RestoreDescription`.
> 

## <a name="deleted-or-lost-service"></a>Silinen veya kayıp hizmeti
Bir hizmet kaldırılırsa, hello veri geri yüklenebilmesi için önce ilk hello hizmeti yeniden oluşturmanız gerekir.  Bu önemli toocreate hello düzeni, veri hello şekilde bölümleme aynı yapılandırması, örn., sorunsuz bir şekilde geri yüklenebilir hello ile hizmetidir.  Merhaba hizmetin çalışır durumda sonra API toorestore veri hello (`OnDataLossAsync` yukarıda) sahip toobe bu hizmetin her bölüme çağrılır. Tek yönlü elde kullanarak bu olup `[FabricClient.TestManagementClient.StartPartitionDataLossAsync](https://msdn.microsoft.com/library/mt693569.aspx)` her bölüm üzerinde.  

Bu noktadan uygulaması olan hello hello yukarıda senaryo ile aynı. Her bölüm toorestore hello son ilgili yedekleme hello dış depolama alanından gerekir. Bir uyarı hello çalışma zamanı dinamik olarak bölüm kimlikleri oluşturduğundan kimliği artık, değişmiş olabilir, hello bölümdür. Bu nedenle, hello hizmet toostore hello uygun bölüm bilgileri ve hizmet adı tooidentify hello doğru son yedekleme toorestore gelen her bölüm için gerekir.

> [!NOTE]
> Toouse önerilmez `FabricClient.ServiceManager.InvokeDataLossAsync` , küme durumunu bozabilir bu yana her bölüm toorestore hello tüm hizmet,.
> 

## <a name="replication-of-corrupt-application-data"></a>Bozuk uygulama verilerinin çoğaltma
Yeni dağıtılan hello uygulama yükseltmesi bir hata varsa, veri bozulmasına neden. Örneğin, geçersiz bir alan kodu ile güvenilir sözlükteki uygulama yükseltme tooupdate her telefon numarası kaydı başlayabilir.  Bu durumda, Service Fabric hello depolanıyor hello veri yapısını farkında olmadığından hello geçersiz telefon numaraları çoğaltılır.

Hello ilk şey, veri bozulması neden olan böyle bir egregious hata algılamanıza sonra toodo toofreeze hello hello uygulama düzeyinde hizmetidir ve, mümkünse, hello hata yok hello uygulama kodu toohello sürümüne yükseltme.  Ancak, hello servis kodu dahi giderildikten sonra hello veri hala bozuk olabilir ve böylece veri geri toobe gerekebilir.  Merhaba son yedekleme de bozuk olabileceğinden bu gibi durumlarda, yeterli toorestore hello son yedekleme, onu olmayabilir.  Dolayısıyla, hello verileri bozuk önce yapan toofind hello son yedekleme sahip.

Hangi yedeklemeler bozuk olduğundan emin değilseniz, yeni bir Service Fabric kümesi dağıtma ve "Silinen veya kayıp hizmeti" yukarıda hello gibi etkilenen bölümlerinin hello yedeklerini geri senaryo.  Her bölüm için en az hello en son toohello hello yedekleri geri yükleme başlatın. Merhaba Bozulması sahip olmayan bir yedek bulduktan sonra taşıma / (Yedekleme) daha yeni tüm yedeklemeler bu bölümün silme. Her bölüm için bu işlemi yineleyin. Şimdi, ne zaman `OnDataLossAsync` çağrılır hello üretim kümedeki hello bölüme hello son yedekleme hello dış depolama bir çekilen hello işlem yukarıda hello tarafından bulunabilir.

Şimdi, hello "Silinen veya kayıp hizmeti" Merhaba adımları bölümü olabilir hello buggy kod hello durumu bozuk önce toorestore hello durumu hello hizmet toohello durumunun kullanıldı.

Şunlara dikkat edin:

  - Geri yüklendiğinde hello veriler kayboldu önce yedekleme hello şansı yapılıyor geri hello bölüm hello durumunu eski yoktur. Bu nedenle, son çare toorecover yalnızca bir kadar verileri mümkün olduğunca geri yüklemeniz gerekir.
  - hello yedekleme klasörünün yolunu temsil eden dize hello ve hello hello yedekleme klasörü içindeki dosyaları yollarına bağlı olarak hello FabricDataRoot yol ve uygulama türü adı'nın uzunluğu 255 karakterden daha büyük olabilir. Bu gibi bazı .NET yöntemleri neden `Directory.Move`, toothrow hello `PathTooLongException` özel durum. Bir geçici çözüm toodirectly olduğu gibi kernel32 API'leri çağırmak `CopyFile`.

## <a name="backup-and-restore-reliable-actors"></a>Yedekleme ve geri yükleme Reliable Actors


Güvenilir aktörler Framework Reliable Services üzerinde oluşturulmuştur. Merhaba hello actor(s) barındıran ActorService bir durum bilgisi olan güvenilir hizmetidir. Bu nedenle, tüm hello yedekleme ve geri yükleme işlevleri güvenilir Hizmetleri'nde kullanılabilir de kullanılabilir tooReliable aktörler (dışında durumu sağlayıcısı belirli davranışlarını). Yedeklemeler bir bölüm başına temelinde gerçekleştirilecek olduğundan, tüm aktörleri bölüm yedeklenecek (ve geri yükleme benzer ve bölüm başına temelinde gerçekleşir,) belirtir. tooperform yedekleme/geri yükleme, hello hizmet sahibi ActorService sınıfından türetilen özel aktör hizmeti sınıfı oluşturmanız gerekir ve ardından yedekleme/benzer tooReliable yukarıda önceki bölümlerde açıklandığı gibi hizmetleri geri yükleme.

```csharp
class MyCustomActorService : ActorService
{
     public MyCustomActorService(StatefulServiceContext context, ActorTypeInformation actorTypeInfo)
            : base(context, actorTypeInfo)
     {                  
     }
    
    //
   // Method overrides and other code.
    //
}
```

Özel aktör hizmet sınıfı oluşturduğunuzda, hello aktör kaydedilirken tooregister bu de gerekir.

```csharp
ActorRuntime.RegisterActorAsync<MyActor>(
   (context, typeInfo) => new MyCustomActorService(context, typeInfo)).GetAwaiter().GetResult();
```

Merhaba varsayılan durumu Sağlayıcısı güvenilir aktörler için `KvsActorStateProvider`. Artımlı yedekleme için varsayılan olarak etkin değil `KvsActorStateProvider`. Artımlı yedekleme oluşturarak etkinleştirebilirsiniz `KvsActorStateProvider` kurucusunda ayarlama ve aşağıdaki kod parçacığında gösterildiği gibi tooActorService Oluşturucusu geçirme ile Merhaba uygun:

```csharp
class MyCustomActorService : ActorService
{
     public MyCustomActorService(StatefulServiceContext context, ActorTypeInformation actorTypeInfo)
            : base(context, actorTypeInfo, null, null, new KvsActorStateProvider(true)) // Enable incremental backup
     {                  
     }
    
    //
   // Method overrides and other code.
    //
}
```

Artımlı yedekleme etkinleştirildikten sonra bir artımlı yedekleme yapmayı FabricMissingFullBackupException ile aşağıdaki nedenlerden birinden dolayı başarısız olabilir ve artımlı yedekleri çıkarmadan önce tootake tam yedekleme gerekir:

  - Birincil hale geldi beri hello çoğaltma hiçbir zaman tam yedekleme sürdü.
  - Son yedekleme alındıktan sonra bazı hello günlük kayıtlarını kesildi.

Artımlı yedekleme etkinleştirildiğinde, `KvsActorStateProvider` kendi günlük kaydeder ve düzenli aralıklarla kesen döngüsel arabellek toomanage kullanmaz. Yedekleme, kullanıcı tarafından 45 dakika boyunca alınmışsa hello sistem hello günlük kayıtları otomatik olarak keser. Bu zaman aralığını belirterek yapılandırılabilir `logTrunctationIntervalInMinutes` içinde `KvsActorStateProvider` Oluşturucusu (artımlı yedeklemeyi etkinleştirme benzer toowhen). Birincil çoğaltma toobuild başka bir çoğaltma kendi veri göndererek gerekiyorsa hello günlük kayıtlarını da kesilmiş.

Bir yedekleme zincirinden benzer tooReliable Hizmetleri geri yükleme yaparken hello BackupFolderPath tam yedekleme ve diğerleri artımlı yedekleri içeren alt dizinleri içeren bir alt alt dizinleri içermelidir. Merhaba yedekleme zinciri doğrulama başarısız olursa hello geri yükleme API ile ilgili hata iletisi FabricException durum oluşturur. 

> [!NOTE]
> `KvsActorStateProvider`şu anda hello seçenek RestorePolicy.Safe yok sayar. Bu özellik için destek gelecek bir sürümde planlanmaktadır.
> 

## <a name="testing-backup-and-restore"></a>Yedekleme ve geri yükleme test etme
Kritik verileri yedeklenmekte ve geri yüklenebileceği önemli tooensure olur. Bu hello çağırarak yapılabilir `Start-ServiceFabricPartitionDataLoss` hello veri yedekleme ve hizmetinizi beklendiği gibi çalıştığını için işlevselliği geri yüklemek isteyip belirli bölüm tootest veri kaybına anlamına PowerShell cmdlet'ini.  Olası tooprogrammatically da olan veri kaybı çağırma ve bu olaydan geri yükleyin.

> [!NOTE]
> Yedekleme için bir örnek uygulama bulmak ve hello Web başvuru uygulaması github'da işlevindeki geri yükleyin. Lütfen hello bakın `Inventory.Service` daha fazla ayrıntı için hizmet.
> 
> 

## <a name="under-hello-hood-more-details-on-backup-and-restore"></a>Merhaba başlık altında: yedekleme ve geri yükleme hakkında daha fazla bilgi
Burada, bazı yedekleme ve geri yükleme hakkında daha fazla ayrıntı verilmiştir.

### <a name="backup"></a>Backup
Merhaba güvenilir durum Yöneticisi herhangi bir engelleme olmadan hello özelliği toocreate tutarlı yedeklemeler okuma veya yazma işlemlerini sağlar. toodo bu nedenle, bir denetim noktası ve günlük Kalıcılık mekanizması kullanır.  Merhaba güvenilir durum Yöneticisi belirli noktaları toorelieve baskısı hello işlem günlüğündeki belirsiz (Basit) denetim noktası alır ve kurtarma sürelerini geliştirebilir.  Zaman `BackupAsync` olarak adlandırılan, hello güvenilir durum Yöneticisi tüm güvenilir nesneler toocopy bunların en son denetim noktası dosyaları tooa yerel yedekleme klasörü bildirir.  Ardından, hello güvenilir durum Yöneticisi hello "işaretçi Başlat" toohello en son günlük kaydından hello yedekleme klasörüne başlayan tüm günlük kayıtları kopyalar.  Toohello en son günlük kaydı tüm hello günlük kayıtları hello yedeklemeye dahil edilir ve hello güvenilir durum Yöneticisi korur yazma tamamlanan günlük olduğundan, tüm işlemler, kaydedilmiş olduğunu hello güvenilir durum Yöneticisi garanti eder (`CommitAsync` döndürdü başarılı bir şekilde) hello yedeklemeye dahil edilir.

Sonra uygulayan herhangi bir işlem `BackupAsync` Mayıs adlı veya hello yedeklemeye olmayabilir.  Merhaba yerel yedekleme klasörü hello platformu tarafından doldurulmuş sonra (yani, yerel yedekleme hello çalışma zamanı tarafından tamamlandığını), yedekleme geri çağırma hello hizmetin çağrılır.  Bu geri çağırma hello yedekleme klasörü tooan Azure depolama gibi dış konuma taşımak için sorumludur.

### <a name="restore"></a>Geri Yükleme
Merhaba güvenilir durum Yöneticisi hello özelliği toorestore bir yedek kopyadan hello kullanarak sağlar `RestoreAsync` API.  
Merhaba `RestoreAsync` yöntemi `RestoreContext` yalnızca hello içinde çağrılabilir `OnDataLossAsync` yöntemi.
bool tarafından döndürülen hello `OnDataLossAsync` hello hizmet bir dış kaynaktan durumuna geri olup olmadığını gösterir.
Merhaba, `OnDataLossAsync` döndürür true, Service Fabric yeniden oluşturma bu birincil diğer tüm çoğaltmalardan. Service Fabric sağlar alacak çoğaltmaları `OnDataLossAsync` çağrısı ilk geçiş toohello birincil rolü, ancak durum verilen okuma değil ya da durum yazma.
Bu, StatefulService uygulayıcılar için gelir `RunAsync` kadar çağrılmaz `OnDataLossAsync` başarıyla tamamlanır.
Ardından, `OnDataLossAsync` hello yeni birincil çağrılır.
Bir hizmet başarıyla (true veya false döndürerek) Bu API tamamlandıktan ve hello ilgili yeniden yapılandırma tamamlanana kadar hello API birer birer çağrılan tutmak.

`RestoreAsync`ilk kez çağrıldı birincil çoğaltma hello tüm mevcut durumda bırakır.  
Daha sonra hello güvenilir durum Yöneticisi hello yedekleme klasörde bulunan tüm hello güvenilir nesneler oluşturur.  
Ardından, hello güvenilir belirtildiği toorestore hello yedekleme klasörü bunların denetim noktaları gelen nesneleridir.  
Son olarak, hello güvenilir durum Yöneticisi hello yedekleme klasöründe hello günlük kayıtlarından kendi durumuna kurtarır ve kurtarma işlemini gerçekleştirir.  
Merhaba kurtarma işleminin bir parçası olarak, tamamlama günlük kayıtlarını hello yedekleme klasörüne sahip hello "başlangıç noktasından" Başlangıç işlemleri yeniden yürütülmüş toohello güvenilir nesneleridir.  
Bu adım, hello sağlar kurtarılan durumu tutarlı değil.

## <a name="next-steps"></a>Sonraki adımlar
  - [Güvenilir Koleksiyonlar](service-fabric-work-with-reliable-collections.md)
  - [Güvenilir hizmetler hızlı başlangıç](service-fabric-reliable-services-quick-start.md)
  - [Güvenilir hizmetler bildirimleri](service-fabric-reliable-services-notifications.md)
  - [Güvenilir Hizmetleri Yapılandırması](service-fabric-reliable-services-configuration.md)
  - [Güvenilir koleksiyonlar için Geliştirici Başvurusu](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)

