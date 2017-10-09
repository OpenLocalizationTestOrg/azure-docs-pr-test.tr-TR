---
ms.assetid: 
title: "aaaAzure anahtar kasası geçici silme | Microsoft Docs"
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 07/10/2017
ms.openlocfilehash: 1b402c58db6f25ae4ae5e2720786fa81eb0e839a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-soft-delete-overview"></a>Azure anahtar kasası soft-delete genel bakış

Anahtar Kasası'nın geçici silme özelliği silinmiş hello kasalarını ve soft-Sil olarak bilinen kasası nesneleri kurtarılmasını sağlar. Özellikle, aşağıdaki senaryoları hello adresi:

- Bir anahtar kasası kurtarılabilir silinmesini desteği
- Anahtar kasası nesnelerin (örneğin kurtarılabilir silinmesi için destek anahtarları, gizli, Sertifikalar)

## <a name="supporting-interfaces"></a>Arabirimleri destekleme

Merhaba soft-delete özellik hello REST, .NET başlangıçta kullanılabilir / C# ve PowerShell arabirimleri. Toohello başvuruları bunlar hakkında daha fazla bilgi için bkz [anahtar kasası başvurusu](https://docs.microsoft.com/azure/key-vault/).

## <a name="scenarios"></a>Senaryolar

Azure anahtar kasası, Azure Resource Manager tarafından yönetilen, izlenen kaynaklardır. Azure Resource Manager, aynı zamanda başarılı bir silme işlemi artık erişilebilir olmaması, kaynak neden gerekir gerektirir silme işlemi için iyi tanımlanmış bir davranış belirtir. Merhaba silme yanlışlıkla veya kasıtlı olup hello soft-delete özelliği adresleri silinmiş hello nesnesinin kurtarma hello.

1. Merhaba tipik senaryo, bir kullanıcı yanlışlıkla bir anahtar kasası ya da bir anahtar kasası nesnesi silmiş; önceden belirlenmiş bir süre için toobe kurtarılabilir nesne bu anahtar kasası veya anahtar kasası, hello kullanıcı hello silme işlemi geri almak ve verilerini kurtarın.

2. Farklı bir senaryoda dolandırıcı bir kullanıcı bir anahtar kasası veya bir anahtarı toocause iş kesintisi bir kasa içinde gibi bir anahtar kasası nesnesi toodelete deneyebilir. Merhaba silinmesi hello anahtar kasası veya anahtar kasası nesne hello gerçek silinmesini arka plandaki veri hello ayıran bir güvenlik önlemi olarak, örneğin, veri silme tooa farklı izinlerini kısıtlayarak rol güvenilir olarak kullanılabilir. Bu yaklaşım, aksi takdirde bir hemen veri kaybına neden bir işlem için etkili bir şekilde çekirdek gerektirir.

### <a name="soft-delete-behavior"></a>Geçici silme davranışı

Bu özellik, bir anahtar kasasını silme işlemi hello ya da bir yumuşak hello görünüm hello nesne vermiş silinmiş etkili bir şekilde hello kaynakları için belirli bekletme süresi, tutarken silme, anahtar kasası nesnesidir. Daha fazla Hello hizmeti aslında hello silme işlemi geri alma hello Silinmiş nesne kurtarmak için bir mekanizma sağlar. 

Soft-delete isteğe bağlı bir anahtar kasası davranışı ve **varsayılan olarak etkin değildir** bu sürümde. Soft-delete anahtar kasanız için etkinleştirme Ayrıntılar için bkz: hello Başvurusu'hello arabirimi tercih ettiğiniz için özel yönergeler hello [anahtar kasası başvurusu](https://docs.microsoft.com/azure/key-vault/).

### <a name="key-vault-recovery"></a>Anahtar kasası kurtarma

Bir anahtar kasası silmeden sonra kurtarma için yeterli meta verileri ekleme hello abonelik altında bir proxy kaynak hello hizmeti oluşturur. Merhaba proxy kaynaktır, hello kullanılabilir saklanan bir nesne silindi hello anahtar kasası ile aynı konumda. 

### <a name="key-vault-object-recovery"></a>Anahtar kasası nesne kurtarma

Bir anahtarı gibi bir anahtar kasası nesnesi silme bağlı hello hizmet hello nesne silinmiş durumda, böylece erişilemez tooany alma işlemleri yapma yerleştirir. Bu durumundayken, hello anahtar kasası nesne yalnızca, kurtarılan veya zorla/kalıcı olarak silinmiş listelenebilir. 

Merhaba aynı zaman, anahtar kasası veri karşılık gelen toohello silinmiş temel hello hello silinmesini zamanlar anahtar kasası veya önceden belirlenmiş bekletme aralığından sonra yürütme için anahtar kasası nesnesi. Merhaba DNS kayıt karşılık gelen toohello kasası ayrıca hello hello elde tutma aralığı süresince tutulur.

### <a name="soft-delete-retention-period"></a>Saklama dönemi Soft-Sil

Geçici silinen kaynaklar ayarlanmış saat, 90 gün boyunca saklanır. Merhaba soft-delete bekletme aralığı boyunca hello aşağıdakileri uygulayın:

- Tüm anahtar kasalarını hello ve bunlarla ilgili erişim silme ve kurtarma bilgileri yanı sıra, abonelik hello soft-delete durumdaki anahtar kasası nesneler listeleyebilir.
    - Yalnızca özel izinlere sahip kullanıcılar, silinen kasalarını listeleyebilirsiniz. Kullanıcılarımızın silinmiş işleme kasaları için bu özel izinlere sahip olan özel bir rol oluşturmanızı öneririz.
- Bir anahtar kasası ile aynı adı hello oluşturulamıyor hello aynı konuma; Bu anahtar kasası hello sahip bir nesne içeriyorsa, buna bağlı olarak, bir anahtar kasası nesne belirli bir kasada oluşturulamıyor aynı ada ve silinmiş durumda olduğu 
- Özellikle ayrıcalıklı bir kullanıcı bir anahtar kasası veya anahtar kasası nesne, hello karşılık gelen proxy kaynak Kurtar komutunda vererek geri yükleyebilirsiniz.
    - Merhaba kullanıcı hello ayrıcalık toocreate bir anahtar kasası hello kaynak grubu altında olan hello özel rol üyesi hello kasası geri yükleyebilirsiniz.
- Yalnızca özellikle ayrıcalıklı kullanıcı zorla bir anahtar kasası veya anahtar kasası nesne silme komutunu hello karşılık gelen proxy kaynakta yayımlayarak silebilir.

Bir anahtar kasası veya anahtar kasası nesne kurtarılan sürece, hello son hello bekletme aralığı hello hizmetinin geçici olarak silinen hello anahtar kasası veya anahtar kasası nesne ve içeriğini bir temizleme gerçekleştirir. Kaynak silme yeniden değil.

### <a name="permitted-purge"></a>İzin verilen temizleme

Kalıcı olarak silmek, temizleme, bir anahtar kasası hello proxy kaynak üzerinde bir POST işlemi aracılığıyla mümkündür ve özel ayrıcalıklar gerektirir. Genellikle, yalnızca hello abonelik sahibi mümkün toopurge bir anahtar kasası olacaktır. Merhaba POST işlemi tetikleyicileri, kasa anında ve kurtarılamaz silinmesini hello. 

Bir özel durum toothis Hello Azure aboneliği olarak işaretlenmiş hello durumda olduğunda *silinemez*. Bu durumda, yalnızca hello hizmeti hello gerçek silme sonra gerçekleştirebilir ve zamanlanmış bir işlem olarak bunu yapar. 



