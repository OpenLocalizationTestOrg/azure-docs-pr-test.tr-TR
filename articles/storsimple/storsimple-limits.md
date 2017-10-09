---
title: "aaaStorSimple 8000 serisi sistem sınırlarını | Microsoft Docs"
description: "Sistem sınırlarını ve StorSimple 8000 serisi bileşenleri ve bağlantıları için önerilen boyutlar açıklar."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: c7392678-0924-46c6-9c59-1665cb9b6586
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5f21862989f23f2fa4cf02c884cc0fc85c6cc2bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-storsimple-8000-series-system-limits"></a>StorSimple 8000 serisi sistem sınırları nelerdir?
## <a name="overview"></a>Genel Bakış
StorSimple merkeziniz için ölçeklenebilir ve esnek depolama sağlar. Ancak, planlamak, dağıtmak ve StorSimple çözümünüzün çalıştırmak gibi göz önünde bulundurmanız gereken bazı sınırlamalar vardır. Merhaba aşağıdaki tabloda bu sınırları açıklar ve böylece hello StorSimple çözümünüzün dışında en alabilir bazı öneriler sağlar.

| Sınır tanımlayıcı | Sınır | Yorumlar |
| --- | --- | --- |
| Depolama hesabının kimlik bilgilerini maksimum sayısı |64 | |
| Birim kapsayıcıları maksimum sayısı |64 | |
| En fazla sayıda birime |255 | |
| Yerel olarak sabitlenmiş birimlerin sayısı |32 | |
| Zamanlamalar bant genişliği şablonu başına maksimum sayısı |168 |Her gün (24 * 7) hello haftanın her saat için bir zamanlama. |
| Katmanlı birim fiziksel aygıtlarda en büyük boyutu |8100 ve 8600 64 TB |8100 ve 8600 fiziksel aygıtlardır. |
| Azure'da sanal cihazlarda katmanlı birim en büyük boyutu |8010 30 TB <br></br> 8020 için 64 TB |8010 hem de 8020 sırasıyla standart depolama ve Premium depolama kullanan sanal Azure aygıtlardır. |
| Fiziksel cihazları yerel olarak sabitlenmiş bir birimde en büyük boyutu |8100 8,5 TB <br></br> 8600 22,5 TB |8100 ve 8600 fiziksel aygıtlardır. |
| İSCSI bağlantısı sayısı |512 | |
| İSCSI başlatıcıları bağlantılarından maksimum sayısı |512 | |
| Erişim denetimi kayıtları aygıt başına maksimum sayısı |64 | |
| En fazla sayıda birime yedekleme İlkesi başına |20 | |
| Yedekleme zamanlaması (Yedekleme ilkesinde) başına korunur maksimum sayısı |64 | |
| Zamanlamalar yedekleme İlkesi başına maksimum sayısı |10 | |
| Maksimum sayıda anlık görüntü birim başına korunabilir herhangi bir türde |256 |Bu sayı yerel anlık görüntülerini içerir ve bulut anlık görüntüleri. |
| Maksimum sayıda içinde herhangi bir cihazda mevcut olabilecek anlık görüntü |10,000 | |
| En fazla sayıda paralel yedekleme, geri yükleme için işlenen ya da kopyalama birime |16 |<ul><li>16'dan fazla birim varsa, işleme yuvaları kullanılabilir duruma geldiğinde, sıralı olarak işlenir.</li><li>Merhaba işlemi tamamlanana kadar bir kopyalanan yeni yedeklerini veya geri yüklenen bir katmanlı birim oluşamaz. Ancak, yerel bir birim için Hello birim çevrimiçi olduktan sonra yedeklemeler izin verilir.</li></ul> |
| Geri yükleme ve kurtarma zamanı katmanlı birimler için kopyalama |< 2 dakika |<ul><li>Merhaba birim boyutu bağımsız olarak, geri yükleme veya kopyalama işleminin 2 dakika içinde Hello birim kullanılabilir hale getirilir.</li><li>Merhaba birim performans başlangıçta hello veri ve meta veri çoğunu hala yer aldığı hello bulutta normalden daha yavaş olabilir. Merhaba bulut toohello StorSimple aygıttan veri akışları olarak performansı artırabilir.</li><li>Merhaba toplam süre toodownload meta veriler üzerinde birim boyutu ayrılmış hello bağlıdır. Meta verileri otomatik olarak ayrılmış birim verilerini TB başına 5 dakika hello hızında hello arka planda hello aygıt halinde duruma getirilir. Bu oran Internet bant genişliği toohello bulut tarafından etkilenebilir.</li><li>geri yükleme hello veya tüm hello meta veriler hello aygıtta olduğunda kopyalama işlemi tamamlanmış demektir.</li><li>Kopya işlemi tam olarak tamamlandıktan veya yedekleme işlemleri kadar hello geri yükleme gerçekleştirilemez. |
| Yerel olarak sabitlenmiş birimler için kurtarma süresi geri yükleme |< 2 dakika |<ul><li>Merhaba birim boyutu bakılmaksızın hello geri yükleme işleminin 2 dakika içinde Hello birim kullanılabilir hale getirilir.</li><li>Merhaba birim performans başlangıçta hello veri ve meta veri çoğunu hala yer aldığı hello bulutta normalden daha yavaş olabilir. Merhaba bulut toohello StorSimple aygıttan veri akışları olarak performansı artırabilir.</li><li>Merhaba toplam süre toodownload meta veriler üzerinde birim boyutu ayrılmış hello bağlıdır. Meta verileri otomatik olarak ayrılmış birim verilerini TB başına 5 dakika hello hızında hello arka planda hello aygıt halinde duruma getirilir. Bu oran Internet bant genişliği toohello bulut tarafından etkilenebilir.</li><li>Yerel olarak sabitlenmiş birimlerin, katmanlı birimleri aksine hello birim verilerini de yerel olarak hello aygıtta indirilir. Tüm hello birim verilerini duruma zaman toohello aygıt hello geri yükleme işlemi tamamlanır.</li><li>Merhaba geri yükleme işlemleri uzun olabilir. Merhaba toplam süre toocomplete hello geri yükleme hello boyutunu sağlanan hello yerel birim, Internet bant genişliği ve hello aygıttaki hello var olan verileri bağlıdır. Merhaba geri yükleme işlemi devam ederken hello yerel olarak sabitlenmiş birim üzerindeki yedekleme işlemlerine izin verilir. |
| Bulut anlık görüntüleri için işlem hızı |15 dakika/TB |<ul><li>En küçük zaman toomake hello bulut anlık görüntüsü yedeklemesine ayrılmış birim verilerini TB başına karşıya yükleme için hazır. </li><li> Toplam bulut anlık görüntü saati hello Internet bant genişliği toocloud tarafından etkilenen bu zamanı toohello anlık görüntü yükleme süresi, ekleyerek hesaplanır. |
| (Merhaba SSD katmanından sunulduğunda) en fazla istemci okuma/yazma verimlilik * |920/720 MB/s tek bir 10 GbE ağ arabirimine sahip |MPIO ve iki ağ arabirimi ile too2x. |
| (Merhaba HDD Katmanı'ndan sunulduğunda) en fazla istemci okuma/yazma verimlilik * |120/250 MB/s | |
| (Merhaba bulut Katmanı'ndan sunulduğunda) en fazla istemci okuma/yazma verimlilik * güncelleştirme 3 ve sonraki sürümlerinde ** |40/60 MB/s için katmanlı birimler<br><br>60/80 MB/s için katmanlı birimlerin birim oluşturma sırasında seçilen arşivleme seçeneğiyle |Okuma üretilen işi oluşturmak ve yeterli g/ç sıra derinliğini koruyarak istemcilerde bağlıdır. <br><br>Elde edilen hızı hello kullanılan temel alınan depolama hesabı hello hızına bağlıdır. |

&#42; G/ç türü başına en fazla üretilen iş yüzde 100 okuma ve yüzde 100 yazma senaryoları ile ölçülen. Gerçek verimlilik daha düşük olabilir ve g/ç üzerinde bağlı karışımı ve ağ koşulları.

&#42; &#42; Performans numaraları önceki tooUpdate 3 daha düşük olabilir.

## <a name="next-steps"></a>Sonraki adımlar
Gözden geçirme hello [StorSimple sistem gereksinimleri](storsimple-system-requirements.md). 

