---
title: "Uygulama yükseltme konuları aaaAdvanced | Microsoft Docs"
description: "Bu makalede tooupgrading Service Fabric uygulaması ilgili bazı gelişmiş konular ele alınmaktadır."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: e29585ff-e96f-46f4-a07f-6682bbe63281
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar;chackdan
ms.openlocfilehash: bdaf3db6209c574d39f57e0bf9951fad5ad1cbec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-upgrade-advanced-topics"></a>Service Fabric uygulama yükseltme: Gelişmiş konular
## <a name="adding-or-removing-services-during-an-application-upgrade"></a>Ekleme veya uygulama yükseltme sırasında hizmetleri kaldırılıyor
Yeni bir hizmet zaten dağıtılmış yayımlanan ve tooan uygulama yükseltme olarak eklediyseniz, hello yeni eklenen toohello dağıtılan uygulama hizmetidir.  Bu tür yükseltme zaten hello uygulamanın parçası olan hello Hizmetleri etkilemez. Ancak, eklendi hello Hizmeti'nin bir örneğini hello yeni hizmet toobe için etkin başlatılmış olması gerekir (hello kullanarak `New-ServiceFabricService` cmdlet'i).

Hizmetleri, yükseltme işleminin bir parçası olarak uygulamadan de kaldırılabilir. Ancak, geçerli hizmetin tüm örneklerine ait hello to-edilecek silinmiş hello yükseltmeye devam etmeden önce durdurulması gerekir (hello kullanarak `Remove-ServiceFabricService` cmdlet'i).

## <a name="manual-upgrade-mode"></a>El ile yükseltme moduna
> [!NOTE]
> Merhaba izlenmeyen el ile modu yalnızca başarısız veya askıya alınmış yükseltme için dikkate alınmalıdır. Merhaba izlenen hello yükseltme modu Service Fabric uygulamaları için önerilen moddur.
>
>

Azure Service Fabric toosupport geliştirme ve üretim kümeleri birden fazla yükseltme modu sağlar. Seçilen dağıtım seçenekleri farklı ortamlar için farklı olabilir.

izlenen hello yükseltme uygulama hello en tipik yükseltme toouse hello üretim ortamında ' dir. Merhaba yükselttiğinizde İlkesi belirtilmemişse, Service Fabric hello yükseltme devam etmeden önce hello uygulama sağlıklı olmasını sağlar.

 Merhaba Uygulama Yöneticisi Uygulama yükseltme modu toohave toplam denetime hello hello aracılığıyla yükseltme işlemi ilerleme durumu çeşitli yükseltme etki alanlarının çalışırken hello el ile kullanabilirsiniz. Bu mod özelleştirilmiş veya karmaşık sistem durumu değerlendirme İlkesi gereklidir veya Geleneksel olmayan yükseltme gerçekleştiği yararlıdır (örneğin, Merhaba uygulaması veri kaybından zaten).

Son olarak, hello otomatik uygulama yükseltme geliştirme veya test ortamları tooprovide hızlı yineleme döngüsü sırasında hizmeti geliştirme için yararlıdır.

## <a name="change-toomanual-upgrade-mode"></a>Toomanual yükseltme modu Değiştir
**El ile**--hello geçerli UD ve değişiklik hello Dur hello uygulama yükseltmeyi modu tooUnmonitored el ile yükseltme. Hello Yöneticisi gereken toomanually çağrısı **MoveNextApplicationUpgradeDomainAsync** tooproceed hello ile yükseltme veya yeni bir yükseltme başlatarak bir geri alma tetikler. Merhaba yükseltme hello el ile moduna girdikten sonra yeni bir yükseltme başlatılana kadar hello el ile modunda kalır. Hello **GetApplicationUpgradeProgressAsync** komut döndürür DOKU\_uygulama\_yükseltme\_durumu\_çalışırken\_İleri\_BEKLEMEDE.

## <a name="upgrade-with-a-diff-package"></a>Diff paketi ile yükseltme
Service Fabric uygulaması, tam ve müstakil uygulama paketiyle sağlama tarafından yükseltilebilir. Bir uygulama aynı zamanda yalnızca güncelleştirilmiş hello uygulama dosyalarını içeren bir fark paketini kullanarak yükseltilebilmesi için uygulama bildirimi ve hello hizmet bildirim dosyaları hello güncelleştirildi.

Bir tam uygulama paketi tüm hello dosyaları gerekli toostart içerir ve Service Fabric uygulaması çalıştırın. Fark paketi hello son sağlamak ve hello geçerli yükseltme arasında değişen hello dosyaları içerir ve ayrıca dosyaları hello tam uygulama bildirimi ve hello hizmet bildirimi. Merhaba uygulama bildirimini veya hello yapı düzende bulunamıyor hizmet bildirimi herhangi başvurusu için hello görüntü deposunda aranır.

Tam uygulama paketleri hello için bir uygulama toohello kümenin ilk yüklemesi gereklidir. Sonraki güncelleştirmeler tam uygulama paketi veya bir fark paket olabilir.

Durumlar fark paket iyi bir seçimdir kullanırken:

* Birkaç hizmet bildirim dosyaları ve/veya birkaç kod paketler, yapılandırma paketleri veya veri paketleri başvuruda bulunan bir geniş Uygulama paketiniz varsa, bir fark paket tercih edilir.
* Hello yapı düzeni doğrudan, uygulama derleme işlemini oluşturan bir dağıtım sistemi olduğunda bir fark paket tercih edilir. Bu durumda, Hello kod değişmediğinden olsa bile, yeni oluşturulan derlemeleri farklı bir sağlama toplamı alın. Bir tam uygulama paketini kullanarak, tooupdate hello sürümünde tüm kod paketler gerektirir. Diff paketini kullanarak, yalnızca değiştirilen hello dosyaları ve hello sürüm değiştiği hello bildirim dosyaları sağlar.

Bir uygulama, Visual Studio kullanarak yükseltildiğinde hello fark paketini otomatik olarak yayımlanır. toocreate fark paketini el ile uygulama bildirimini hello ve hello hizmet bildirimlerini güncelleştirilmesi gerekir, ancak yalnızca değiştirilen hello paketler hello son uygulama paketinde eklenmelidir.

Örneğin, uygulama (sürüm numaraları anlama kolaylığı için sağlanan) aşağıdaki hello ile başlayalım:

```text
app1           1.0.0
  service1     1.0.0
    code       1.0.0
    config     1.0.0
  service2     1.0.0
    code       1.0.0
    config     1.0.0
```

Şimdi, PowerShell kullanarak bir fark paketini kullanarak tooupdate yalnızca hello kod paketi service1 istediğinizi varsayalım. Şimdi, güncelleştirilmiş uygulamanızı klasör yapısı aşağıdaki hello sahiptir:

```text
app1           2.0.0      <-- new version
  service1     2.0.0      <-- new version
    code       2.0.0      <-- new version
    config     1.0.0
  service2     1.0.0
    code       1.0.0
    config     1.0.0
```

Bu durumda, hello uygulama bildirim too2.0.0 ve hello hizmet bildirimi service1 tooreflect hello kod paketi güncelleştirme için güncelleştirin. Uygulama paketinizi için Hello klasör yapısı aşağıdaki hello sahip olur:

```text
app1/
  service1/
    code/
```

## <a name="next-steps"></a>Sonraki adımlar
[Uygulama kullanarak Visual Studio yükseltme](service-fabric-application-upgrade-tutorial.md) Visual Studio kullanarak bir uygulama yükseltme yol gösterir.

[Uygulama Powershell kullanarak yükseltme](service-fabric-application-upgrade-tutorial-powershell.md) PowerShell kullanarak bir uygulama yükseltme yol gösterir.

Uygulamanızı kullanarak yükseltme nasıl kontrol [yükseltme parametreleri](service-fabric-application-upgrade-parameters.md).

Uygulama yükseltme öğrenme tarafından uyumlu hale getirmek nasıl toouse [veri seri hale getirme](service-fabric-application-upgrade-data-serialization.md).

Toohello adımlarda başvurarak uygulama yükseltmeleri sık karşılaşılan sorunları düzeltmek [sorun giderme uygulama yükseltmelerini](service-fabric-application-upgrade-troubleshooting.md).
