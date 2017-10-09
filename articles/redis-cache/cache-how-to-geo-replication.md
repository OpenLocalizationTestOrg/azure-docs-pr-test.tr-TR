---
title: "Azure Redis önbelleği için coğrafi çoğaltma aaaHow tooconfigure | Microsoft Docs"
description: "Nasıl tooreplicate coğrafi bölgeler arasında Azure Redis önbelleği örnekleri hakkında bilgi edinin."
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 375643dc-dbac-4bab-8004-d9ae9570440d
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: sdanie
ms.openlocfilehash: edcd6f202b51055d1a4e47ecaf11f9977d50aa81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-geo-replication-for-azure-redis-cache"></a>Nasıl Azure Redis önbelleği için coğrafi çoğaltma tooconfigure

Coğrafi çoğaltma iki Premium katmanı Azure Redis önbelleği örnekleri bağlama için bir mekanizma sağlar. Bir önbellek hello birincil bağlantılı önbellek ve hello hello ikincil bağlantılı önbelleği gibi diğer olarak atanır. Merhaba ikincil bağlantılı önbellek salt okunur olur ve yazılı toohello birincil önbelleği veri toohello ikincil bağlantılı önbellek çoğaltılır. Bu işlev Azure bölgeler arasında kullanılan tooreplicate bir önbellek olabilir. Bu makale, Premium katmanı Azure Redis önbelleği örnekleri için kılavuz tooconfiguring coğrafi çoğaltma sağlar.

## <a name="geo-replication-prerequisites"></a>Coğrafi çoğaltma önkoşulları

iki önbellekleri, Önkoşullar aşağıdaki hello arasında tooconfigure coğrafi çoğaltma karşılanmalıdır:

- Her iki önbellekleri olmalıdır [Premium katmanı](cache-premium-tier-intro.md) önbelleğe alır.
- Her iki önbellekleri hello olmalıdır aynı Azure aboneliği.
- Merhaba ikincil bağlantılı önbellek gerekir olması ya da hello aynı fiyatlandırma katmanı veya hello birincil bağlantılı önbellek daha büyük bir fiyatlandırma katmanı.
- Merhaba birincil bağlantılı önbellek kümeleme özelliği etkinleştirilmiş varsa hello ikincil bağlantılı önbellek Kümeleme ile Merhaba özelliği etkinleştirilmiş olmalıdır aynı sayıda hello birincil bağlantılı önbellek parça.
- Her iki önbellekleri oluşturulmalıdır ve çalışır durumda.
- Kalıcılık ya da önbellek etkinleştirilmemelidir.
- Coğrafi çoğaltma aynı sanal ağı desteklenen hello önbellekleri arasında. Coğrafi çoğaltma farklı vnet'lerdeki önbellekleri arasında da desteklenir, hello iki sanal ağlar hello Vnet'lerdeki kaynaklar mümkün tooreach olduğunu şekilde yapılandırılmış olduğu sürece diğer TCP bağlantıları aracılığıyla.

Coğrafi çoğaltma yapılandırıldıktan sonra hello aşağıdaki kısıtlamalar tooyour bağlantılı önbellek çifti geçerlidir:

- Merhaba ikincil bağlantılı önbellek salt okunurdur; okuyabilir, ancak hiçbir veri tooit yazılamıyor. 
- Merhaba ikincil bağlantılı Önbelleği'nde Hello bağlantı eklenmeden önce olan tüm veriler kaldırılır. Merhaba coğrafi çoğaltma sonradan ancak kaldırılırsa, hello hello ikincil bağlantılı önbellekteki veriler kalır çoğaltılan.
- İşlemi başlatamaz bir [işlemi ölçeklendirme](cache-how-to-scale.md) ya da önbellekteki veya [parça hello sayısını değiştirme](cache-how-to-premium-clustering.md) hello önbellek kümeleme özelliği etkinleştirilmiş varsa.
- Kalıcılık ya da önbellekteki etkinleştiremezsiniz.
- Kullanabilirsiniz [verme](cache-how-to-import-export-data.md#export) ya da önbelleğiyle ancak yalnızca [alma](cache-how-to-import-export-data.md#import) önbellek hello birincil bağlı.
- Bağlantılı önbellek veya hello coğrafi çoğaltma bağlantısı kaldırana kadar bunları içeren hello kaynak grubu silinemiyor. Daha fazla bilgi için bkz: [neden hello işlemi başarısız toodelete my bağlantılı önbellek çalıştığında?](#why-did-the-operation-fail-when-i-tried-to-delete-my-linked-cache)
- Merhaba iki önbellekleri farklı bölgelerde bulunuyorsa, ağ çıkışı maliyeti toohello veri bölgeleri toohello ikincil bağlantılı önbellek arasında çoğaltılan uygulanır. Daha fazla bilgi için bkz: [ne kadar mu tooreplicate verilerimi Azure bölgeler arasında maliyet?](#how-much-does-it-cost-to-replicate-my-data-across-azure-regions)
- Merhaba birincil önbelleği (ve onun çoğaltması) kesilirse otomatik yük devretme toohello ikincil bağlantılı önbellek yok yok. Sipariş toofailover istemci uygulamalarında toomanually Kaldır hello coğrafi çoğaltma bağlantısını gerekir ve hello istemci uygulamaları toohello önbelleğe noktası önceden hello ikincil bağlantılı önbellek olmuştur. Daha fazla bilgi için bkz: [nasıl toohello ikincil bağlantılı önbellek yapabilmesini çalışır?](#how-does-failing-over-to-the-secondary-linked-cache-work)

## <a name="add-a-geo-replication-link"></a>Coğrafi çoğaltma bağlantısı ekleme

1. iki premium önbelleğe birlikte coğrafi çoğaltma için toolink tıklatın **coğrafi çoğaltma** bağlı hello birincil hedeflenen hello önbelleğin hello kaynak menüsünden önbelleğe ve ardından **Ekle önbellek çoğaltma bağlantısı**hello gelen **coğrafi çoğaltma** dikey.

    ![Bağlantı Ekle](./media/cache-how-to-geo-replication/cache-geo-location-menu.png)

2. İstenen hello ikincil hello önbellekten Hello adına tıklayın **uyumlu önbellekleri** listesi. İstenen önbelleğiniz hello listesinde görüntülenmiyorsa, o hello doğrulayın [coğrafi çoğaltma Önkoşullar](#geo-replication-prerequisites) ikincil önbellek karşılanmadığı hello istenen için. toofilter hello bölge tarafından önbellekleri hello istenen yalnızca önbelleğe hello hello harita toodisplay bölgede **uyumlu önbellekleri** listesi.

    ![Coğrafi çoğaltma uyumlu önbellekler](./media/cache-how-to-geo-replication/cache-geo-location-select-link.png)
    
    Merhaba bağlam menüsünü kullanarak hello ikincil önbellek işlem veya Görünüm ayrıntılarını bağlama hello de başlatabilirsiniz.

    ![Coğrafi çoğaltma bağlam menüsü](./media/cache-how-to-geo-replication/cache-geo-location-select-link-context-menu.png)

3. Tıklatın **bağlantı** toolink iki önbellekleri birlikte hello ve hello çoğaltma işlemine başlar.

    ![Bağlantı önbellekler](./media/cache-how-to-geo-replication/cache-geo-location-confirm-link.png)

4. Merhaba üzerinde hello çoğaltma işlemi hello ilerlemesini görüntüleyebilirsiniz **coğrafi çoğaltma** dikey.

    ![Bağlantı durumu](./media/cache-how-to-geo-replication/cache-geo-location-linking.png)

    Merhaba durumu bağlama hello de görüntüleyebilirsiniz **genel bakış** dikey hem hello birincil ve ikincil önbellekler için.

    ![Önbellek durumu](./media/cache-how-to-geo-replication/cache-geo-location-link-status.png)

    Merhaba çoğaltma işlemi tamamlandıktan sonra hello **bağlantı durumu** çok değiştirir**başarılı**.

    ![Önbellek durumu](./media/cache-how-to-geo-replication/cache-geo-location-link-successful.png)

    Merhaba, işlem bağlama sırasında hello birincil bağlantılı önbellek kullanılabilir kalır ancak işlem bağlama hello tamamlanana kadar hello ikincil bağlantılı önbellek kullanılabilir değil.

## <a name="remove-a-geo-replication-link"></a>Coğrafi çoğaltma bağlantısını Kaldır

1. iki önbellekleri Dur coğrafi çoğaltma, arasındaki tooremove hello bağlantısına tıklayın **bağlantısını önbellekleri** hello gelen **coğrafi çoğaltma** dikey.
    
    ![Önbellekleri bağlantısını Kaldır](./media/cache-how-to-geo-replication/cache-geo-location-unlink.png)

    Merhaba bağlantı kaldırma işlemi tamamlandıktan sonra hello ikincil önbelleği hem okuma için kullanılabilir ve yazar.

>[!NOTE]
>Merhaba coğrafi çoğaltma bağlantısı kaldırıldığında, hello veri hello birincil bağlantılı önbellek kalır hello ikincil önbelleğinde gelen çoğaltılan.
>
>

## <a name="geo-replication-faq"></a>Coğrafi çoğaltma ile ilgili SSS

- [Coğrafi çoğaltma ile standart ya da temel katmanı önbellek kullanabilir miyim?](#can-i-use-geo-replication-with-a-standard-or-basic-tier-cache)
- [My önbellek hello bağlama veya bağlantı kaldırma işlemi sırasında kullanılacak var mı?](#is-my-cache-available-for-use-during-the-linking-or-unlinking-process)
- [İkiden fazla önbellekleri birlikte bağlayabilir miyim?](#can-i-link-more-than-two-caches-together)
- [Farklı Azure aboneliklerinden iki önbellekleri bağlayabilir miyim?](#can-i-link-two-caches-from-different-azure-subscriptions)
- [Farklı boyutlarda iki önbelleklerle bağlayabilir miyim?](#can-i-link-two-caches-with-different-sizes)
- [Coğrafi çoğaltma kümeleme özelliği etkinleştirilmiş kullanabilir miyim?](#can-i-use-geo-replication-with-clustering-enabled)
- [Bir sanal ağda my önbellekleri ile coğrafi çoğaltma kullanabilir miyim?](#can-i-use-geo-replication-with-my-caches-in-a-vnet)
- [PowerShell veya Azure CLI toomanage coğrafi çoğaltma kullanabilir miyim?](#can-i-use-powershell-or-azure-cli-to-manage-geo-replication)
- [Nasıl onu tooreplicate verilerimi Azure bölgeler arasında maliyeti nedir?](#how-much-does-it-cost-to-replicate-my-data-across-azure-regions)
- [Neden toodelete my bağlantılı önbellek çalıştığında hello işlemi başarısız oldu?](#why-did-the-operation-fail-when-i-tried-to-delete-my-linked-cache)
- [My ikincil bağlantılı önbelleği için hangi bölge kullanmalıyım?](#what-region-should-i-use-for-my-secondary-linked-cache)
- [Toohello ikincil bağlantılı önbellek yapabilmesini nasıl çalışır?](#how-does-failing-over-to-the-secondary-linked-cache-work)

### <a name="can-i-use-geo-replication-with-a-standard-or-basic-tier-cache"></a>Coğrafi çoğaltma ile standart ya da temel katmanı önbellek kullanabilir miyim?

Coğrafi çoğaltma Hayır, yalnızca Premium katmanı önbellekler için olarak kullanılabilir.

### <a name="is-my-cache-available-for-use-during-hello-linking-or-unlinking-process"></a>My önbellek hello bağlama veya bağlantı kaldırma işlemi sırasında kullanılacak var mı?

- İki önbellekleri coğrafi çoğaltma için birlikte bağlanırken hello birincil bağlantılı önbellek kullanılabilir kalır, ancak işlem bağlama hello tamamlanana kadar hello ikincil bağlantılı önbellek kullanılabilir değil.
- İki önbellekleri arasında Hello coğrafi çoğaltma bağlantısı kaldırırken, her iki önbellekleri kullanılabilir kalır.

### <a name="can-i-link-more-than-two-caches-together"></a>İkiden fazla önbellekleri birlikte bağlayabilir miyim?

Hayır, coğrafi çoğaltma kullanırken, yalnızca iki önbellekleri birbirine bağlayabilirsiniz.

### <a name="can-i-link-two-caches-from-different-azure-subscriptions"></a>Farklı Azure aboneliklerinden iki önbellekleri bağlayabilir miyim?

Hayır, her iki önbellekleri hello olmalıdır aynı Azure aboneliği.

### <a name="can-i-link-two-caches-with-different-sizes"></a>Farklı boyutlarda iki önbelleklerle bağlayabilir miyim?

Evet, ikincil Hello bağlı olduğu sürece önbellek hello birincil bağlantılı önbellek büyüktür.

### <a name="can-i-use-geo-replication-with-clustering-enabled"></a>Coğrafi çoğaltma kümeleme özelliği etkinleştirilmiş kullanabilir miyim?

Evet, hem önbellekleri hello olduğu sürece aynı sayıda parça.

### <a name="can-i-use-geo-replication-with-my-caches-in-a-vnet"></a>Bir sanal ağda my önbellekleri ile coğrafi çoğaltma kullanabilir miyim?

Evet, coğrafi çoğaltma vnet'lerdeki önbelleklerinin desteklenir. 

- Coğrafi çoğaltma aynı sanal ağı desteklenen hello önbellekleri arasında.
- Coğrafi çoğaltma farklı vnet'lerdeki önbellekleri arasında da desteklenir, hello iki sanal ağlar hello Vnet'lerdeki kaynaklar mümkün tooreach olduğunu şekilde yapılandırılmış olduğu sürece diğer TCP bağlantıları aracılığıyla.

### <a name="can-i-use-powershell-or-azure-cli-toomanage-geo-replication"></a>PowerShell veya Azure CLI toomanage coğrafi çoğaltma kullanabilir miyim?

Yalnızca yönetebilmeniz için şu anda coğrafi çoğaltma'yı kullanarak Azure portalında hello.

### <a name="how-much-does-it-cost-tooreplicate-my-data-across-azure-regions"></a>Nasıl onu tooreplicate verilerimi Azure bölgeler arasında maliyeti nedir?

Coğrafi çoğaltma kullanırken, veri hello birincil bağlantılı önbelleğinden çoğaltılmış toohello ikincil bağlı önbelleğidir. Merhaba iki bağlanmışsa önbellekleri hello olan aynı Azure bölgesinde hello veri aktarımı için herhangi bir ücret alınmaz. Merhaba iki bağlanmışsa önbellekleri farklı Azure bölgelerinde, hello coğrafi çoğaltma veri aktarımı ücretsiz olarak bu verileri toohello diğer Azure bölgesi çoğaltma hello bant genişliği maliyetidir. Daha fazla bilgi için bkz: [bant genişliği fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/bandwidth/).

### <a name="why-did-hello-operation-fail-when-i-tried-toodelete-my-linked-cache"></a>Neden toodelete my bağlantılı önbellek çalıştığında hello işlemi başarısız oldu?

İki önbellekleri birbirine bağlı olduğunda, hello coğrafi çoğaltma bağlantısı kaldırana kadar bunları içeren önbellek veya hello kaynak grubu silinemiyor. Dener birini veya her ikisini hello içeren toodelete hello kaynak grubunu bağlı önbellekleri, hello hello kaynak grubundaki kaynaklar silinir, ancak hello kaynak grubu kalır hello `deleting` durumu ve bağlı hello kaynak grubunda önbellekler Hello kalır `running` durumu. açıklandığı gibi hello kaynak grubu ve hello toocomplete hello silme bağlı önbellekleri içindeki sonu hello coğrafi çoğaltma bağlantı [coğrafi çoğaltma bağlantısını kaldırmak](#remove-a-geo-replication-link).

### <a name="what-region-should-i-use-for-my-secondary-linked-cache"></a>My ikincil bağlantılı önbelleği için hangi bölge kullanmalıyım?

Genel olarak, bu, önbelleği tooexist hello içinde için aynı önerilir eriştiği Merhaba uygulaması olarak Azure bölgesi. Birincil ve geri dönüş bölge uygulamanız varsa, birincil ve ikincil önbellekleri bu aynı bölgede var olmalıdır. Eşleştirilmiş bölgeler hakkında daha fazla bilgi için bkz: [en iyi uygulamaları – Azure eşleştirilmiş bölgeleri](../best-practices-availability-paired-regions.md).

### <a name="how-does-failing-over-toohello-secondary-linked-cache-work"></a>Toohello ikincil bağlantılı önbellek yapabilmesini nasıl çalışır?

Merhaba ilk sürümünde coğrafi çoğaltma, Azure Redis önbelleği Azure bölgeler arasında otomatik yük devretme desteklemez. Coğrafi çoğaltma öncelikle bir olağanüstü durum kurtarma senaryosunda kullanılır. Distater kurtarma senaryosunda, müşterilerin hello tüm uygulama yığınını yedekleme bir bölgede koordineli bir şekilde yerine tek tek uygulama bileşenleri vermenize izin vererek tooswitch tootheir yedeklemelerin kendi getirecek. Bu özellikle ilgili tooRedis olur. Redis hello başlıca avantajlarından biri, çok düşük gecikme süreli depolama olmasıdır. Redis tarafından kullanılan tooa farklı Azure bölgesi bir uygulama başarısız ancak hello işlem katmanı yok, seyahat zamanında eklenen hello bir fark performansı etkiler. Bu nedenle, tooavoid Redis başarısız üzerinden otomatik olarak tootransient kullanılabilirlik sorunları isteriz.

Şu anda, coğrafi çoğaltma bağlantı hello Azure portal ve hello Redis İstemcisi'nde hello bağlantı uç nokta hello birincil bağlantılı önbelleği (önceki adıyla bağlı) toohello ikincil değiştirin tooremove hello ihtiyacınız tooinitiate hello yük devretme, önbellek. İki önbellekleri ilişkilendirmesi, hello hello çoğaltma bir normal olduğunda önbellek yeniden okuma-yazma ve doğrudan Redis istemcilerinden gelen istekleri kabul eder.


## <a name="next-steps"></a>Sonraki adımlar

Merhaba hakkında daha fazla bilgi [Azure Redis önbelleği Premium katmanına](cache-premium-tier-intro.md).

