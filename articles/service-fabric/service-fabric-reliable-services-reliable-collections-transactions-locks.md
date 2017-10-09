---
title: "Azure Service Fabric güvenilir koleksiyonları ve kilit modlarında aaaTransactions | Microsoft Docs"
description: "Azure Service Fabric güvenilir durum Yöneticisi ve güvenilir koleksiyonları işlemleri ve kilitleme."
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: masnider,rajak
ms.assetid: 62857523-604b-434e-bd1c-2141ea4b00d1
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/1/2017
ms.author: mcoskun
ms.openlocfilehash: 340e029aa98f43ad6e46b48f687dad01f9d96f69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="transactions-and-lock-modes-in-azure-service-fabric-reliable-collections"></a>İşlemler ve Azure Service Fabric güvenilir koleksiyonları kilit modu

## <a name="transaction"></a>İşlem
Bir işlem, tek bir mantıksal birim iş olarak gerçekleştirilen işlemler dizisidir.
Bir işlem ACID özellikleri aşağıdaki hello göstermesi gerekir. (bkz: https://technet.microsoft.com/en-us/library/ms190612)
* **Kararlılık**: atomik bir iş birimine bir işlem olmalıdır. Diğer bir deyişle, tüm veri değişiklikleri gerçekleştirilen ya da bunların hiçbiri gerçekleştirilir.
* **Tutarlılık**: tamamlandığında, bir işlem tüm verileri tutarlı bir durumda bırakmanız gerekir. Tüm iç veri yapılarını hello hello işlem sonunda doğru olması gerekir.
* **Yalıtım**: eşzamanlı işlemler tarafından yapılan değişiklikler diğer eşzamanlı işlemler tarafından yapılan hello değişiklikler üzerinden olmalıdır. bir ITransaction içinde bir işlem için kullanılan hello yalıtım düzeyi hello IReliableState gerçekleştirme hello işlemi tarafından belirlenir.
* **Dayanıklılık**: bir işlem tamamlandıktan sonra etkileri kalıcı olarak hello sistemde karşılandığından. Merhaba değişiklikler bile hello olayda bir sistem hatasının kalıcı olmasını sağlar.

### <a name="isolation-levels"></a>Yalıtım düzeyi
Yalıtım düzeyi tanımlar hello derece toowhich hello işlem diğer işlemler tarafından yapılan değişiklikler üzerinden olmalıdır.
Güvenilir koleksiyonlarda desteklenen iki yalıtım düzeyi vardır:

* **Yinelenebilir Okuma**: deyimleri değiştirildi, ancak henüz diğer işlemler tarafından kaydedilen veri okunamıyor ve başka bir işlem hello geçerli kadar hello geçerli işlem tarafından okunur verileri değiştirebilir belirtir işlem tamamlanır. Daha fazla ayrıntı için bkz: [https://msdn.microsoft.com/library/ms173763.aspx](https://msdn.microsoft.com/library/ms173763.aspx).
* **Anlık Görüntü**: bir işlemde herhangi bir deyim tarafından okunan veriler hello işlemsel olarak tutarlı hello hello işlem başlangıcında var hello veri sürümü olup olmadığını belirtir.
  Merhaba işlem yalnızca hello işlem hello başlamadan önce kaydedilmiş veri değişiklikleri tanıyabilirsiniz.
  Merhaba hello geçerli işlemi başladıktan sonra diğer işlemler tarafından yapılan veri değişiklikleri hello geçerli işlemde yürütme görünür toostatements değildir.
  Merhaba hello hello işlem başlangıcında var gibi hello bir işlemde hello kaydedilen verilerin bir anlık görüntüsünü get deyimleri gibi etkisidir.
  Anlık görüntüler güvenilir koleksiyonlar genelinde tutarlı değil.
  Daha fazla ayrıntı için bkz: [https://msdn.microsoft.com/library/ms173763.aspx](https://msdn.microsoft.com/library/ms173763.aspx).

Güvenilir koleksiyonları hello yalıtım düzeyi toouse hareketin oluşturma hello zamanında hello işlemi ve hello çoğaltma hello rolü bağlı olarak belirli bir okuma işlemi için otomatik olarak seçin.
Güvenilir sözlük ve sıra işlemleri için yalıtım düzeyi varsayılan değerlerini gösterir hello tablosu aşağıdadır.

| İşlem \ rolü | Birincil | İkincil |
| --- |:--- |:--- |
| Tek varlık okuma |Yinelenebilir Okuma |Anlık Görüntü |
| Numaralandırma, sayısı |Anlık Görüntü |Anlık Görüntü |

> [!NOTE]
> Tek varlık işlemleri için ortak örnekler `IReliableDictionary.TryGetValueAsync`, `IReliableQueue.TryPeekAsync`.
> 

Merhaba güvenilir sözlük ve hello güvenilir sıra okuma bilgisayarınızı Yazar destekler.
Diğer bir deyişle, herhangi bir işlem içinde olması görünür tooa aşağıdaki okuyup okumayacağını toohello ait yazma aynı işlem.

## <a name="locks"></a>Kilitler
Kilitleme güvenilir koleksiyonlarında tüm işlemleri uygulama sıkı iki aşama: bir işlem alınan bir durdurma veya bir yürütme ile Merhaba işlem sonlanana kadar hello kilitleri bırakmaz.

Güvenilir sözlüğü satır düzeyinde tüm tek bir varlık işlemler için kilitleme kullanır.
Eşzamanlılık katı işlem FIFO özelliği için devre dışı güvenilir sıra trades.
Güvenilir kuyruğu kullanan bir işlemle izin verme işlemi düzeyi kilitleri `TryPeekAsync` ve/veya `TryDequeueAsync` ve bir işlemle `EnqueueAsync` birer birer.
Bu toopreserve FIFO, Not bir `TryPeekAsync` veya `TryDequeueAsync` hiç gözlemleyen hello güvenilir sıra boşsa, ayrıca kilitleyecek `EnqueueAsync`.

Yazma işlemlerinin her zaman özel kilit alıyor.
Okuma işlemleri için hello kilitleme, birkaç etkene bağlıdır.
Anlık görüntü yalıtımı kullanılarak gerçekleştirilen okuma işlemi kilidi serbest ' dir.
Varsayılan olarak tüm yinelenebilir okuma işlemi paylaşılan kilitleri alır.
Ancak, yinelenebilir okuma destekleyen tüm okuma işlemi için hello kullanıcı hello paylaşılan kilit yerine bir güncelleştirme kilidi isteyebilir.
Bir güncelleştirme kilidi asimetrik kilit tooprevent birden çok işlem kaynakları daha sonraki bir zamanda potansiyel güncelleştirmeleri kilitlediğinizde gerçekleşen kilitlenme ortak biçimi kullanılır.

Aşağıdaki tablonun hello Hello kilit uyumluluk matrisi bulunabilir:

| İstek \ verildi | None | Paylaşılan | Güncelleştirme | Özel |
| --- |:--- |:--- |:--- |:--- |
| Paylaşılan |Çakışma |Çakışma |Çakışma |Çakışma |
| Güncelleştirme |Çakışma |Çakışma |Çakışma |Çakışma |
| Özel |Çakışma |Çakışma |Çakışma |Çakışma |

Zaman aşımı hello güvenilir koleksiyonları API'leri değişkeninde kilitlenme algılama için kullanılır.
Örneğin, iki işlemleri (T1 ve T2) tooread çalıştığınız ve K1 güncelleştirin.
Bunlar için mümkündür toodeadlock, her ikisi de şunun için kilit sahip hello paylaşılan.
Bu durumda, bir veya iki hello işlemlerinin zaman aşımına uğrar.

Bu kilitlenme senaryo, bir güncelleştirme kilidi kilitlenmeleri nasıl engelleyebilirsiniz, harika bir örnektir.

## <a name="next-steps"></a>Sonraki adımlar
* [Güvenilir Koleksiyonlar ile çalışma](service-fabric-work-with-reliable-collections.md)
* [Güvenilir hizmetler bildirimleri](service-fabric-reliable-services-notifications.md)
* [Güvenilir hizmetler yedekleme ve geri yükleme (olağanüstü durum kurtarma)](service-fabric-reliable-services-backup-restore.md)
* [Güvenilir durum Yöneticisi yapılandırması](service-fabric-reliable-services-configuration.md)
* [Güvenilir koleksiyonlar için Geliştirici Başvurusu](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)

