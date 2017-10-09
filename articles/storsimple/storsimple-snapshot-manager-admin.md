---
title: "Anlık Görüntü Yöneticisi Yönetim aaaStorSimple | Microsoft Docs"
description: "Genel bir bakış ve bağlantıları toomore StorSimple Snapshot Manager çözüm yönetim görevleri ve iş akışları hakkında bilgi sağlar."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 1cdbb61d-bd16-4be4-ade2-ceab11508acb
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2016
ms.author: v-sharos
ms.openlocfilehash: d875f2efbdeb844b412cf8d9f1f971f18da7526e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-tooadminister-your-storsimple-solution"></a>StorSimple çözümünüzün StorSimple Snapshot Manager tooadminister kullanın

## <a name="overview"></a>Genel Bakış
StorSimple Snapshot Manager, veri koruma ve Microsoft Azure StorSimple ortamda yedekleme yönetimini basitleştirir Microsoft Yönetim Konsolu (MMC) ek bileşenidir. StorSimple Snapshot Manager ile Microsoft Azure StorSimple verileri hello veri merkezi ve hello bulut tek bir tümleşik depolama çözümü olarak, bu nedenle yedekleme işlemlerini basitleştirir ve maliyetlerini azaltır yönetebilirsiniz.

Merhaba StorSimple Snapshot Manager Merkezi Yönetim Konsolu toocreate tutarlı, zaman içinde nokta yedek kopyalarını yerel ve bulut verilerini sağlar. Örneğin, hello konsola kullanabilirsiniz:

* Yapılandırma, yedekleme ve birimleri silin.
* Birimi yedeklenmiş verileri grupları tooensure uygulama tutarlı olduğundan.
* Böylece verilerin belirlenmiş bir zamanlamayla yedeklendiğinden yedekleme ilkelerini yönetin.
* Merhaba bulutta depolanan ve olağanüstü durum kurtarma için kullanılan veri bağımsız kopyalarını oluşturun.

Bu makalede StorSimple Snapshot Manager açıklamak bağlantılar tootutorials sağlar ve nasıl toouse, toocomplete sistem yönetim görevleri ve iş akışları.

* StorSimple Snapshot Manager bileşenleri ve mimarisi hakkında daha fazla bilgi için bkz: [StorSimple anlık görüntü Yöneticisi nedir?](storsimple-what-is-snapshot-manager.md) 
* StorSimple Snapshot Manager toodownload Git çok[hello StorSimple Snapshot Manager indirme sayfası](https://www.microsoft.com/download/details.aspx?id=44220).
* StorSimple Snapshot Manager dağıtım yordamları için çok Git[dağıtmak StorSimple Snapshot Manager](storsimple-snapshot-manager-deployment.md).

> [!NOTE]
> StorSimple Snapshot Manager toomanage Microsoft Azure StorSimple sanal (olarak da bilinen StorSimple sanal cihazlar şirket) diziler kullanamazsınız.


## <a name="storsimple-snapshot-manager-tasks-and-workflows"></a>StorSimple Snapshot Manager görevleri ve iş akışları
Merhaba StorSimple Snapshot Manager toomonitor kullanın ve geçerli, zamanlanmış ve tamamlanan yedekleme işleri yönetin. Ayrıca, StorSimple Snapshot Manager Kataloğu tamamlandı too64 yedekleri kurma sağlar. Merhaba katalog toofind kullanın ve birimleri veya tek tek dosyaları geri yükleyin. 

| Eğer tooDO bu istediğiniz... | BU ÖĞRETİCİYİ KULLANIN... |
|:--- |:--- |
| StorSimple anlık görüntü Yöneticisi hakkında daha fazla bilgi edinin |[StorSimple anlık görüntü Yöneticisi nedir?](storsimple-what-is-snapshot-manager.md) |
| StorSimple anlık görüntü Yöneticisi'ni yükleyin<br>StorSimple anlık görüntü Yöneticisi'ni yeniden yükleyin<br>StorSimple anlık görüntü Yöneticisi'ni Kaldır |[StorSimple Snapshot Manager dağıtma](storsimple-snapshot-manager-deployment.md) |
| StorSimple anlık görüntü Yöneticisi'ni kullanın menüleri ve özellikleri:<ul><li>Menü çubuğu</li><li>Araç çubuğu</li><li>Kapsam bölmesi</li><li>Sonuçlar Bölmesi</li><li>Eylemler bölmesi</li><li>Klavye gezinme ve kısayollar</li></ul> |[StorSimple anlık görüntü Yöneticisi kullanıcı arabirimi](storsimple-use-snapshot-manager.md) |
| StorSimple anlık görüntü Yöneticisi'nde bulunan hello ortak MMC özelliklerini kullanın:<ul><li>Görünüm</li><li>Buradan yeni pencere</li><li>Yenileme</li><li>Listeyi dışarı aktar</li><li>Yardım</li></ul> |[StorSimple anlık görüntü Yöneticisi'nde Hello MMC menü eylemlerini kullanın](storsimple-snapshot-manager-mmc-menu.md) |
| Ekleme veya bir aygıt değiştirme<br>Bir aygıtı bağlayın<br>İçeri aktarılan birim grupları doğrulayın<br>Bağlı aygıtlar Yenile<br>Bir cihaz kimlik doğrulaması<br>Cihaz ayrıntıları görüntüle<br>Cihaz yapılandırmasını Sil<br>Aygıt parola değiştirme<br>Başarısız aygıt değiştirin<br> |[StorSimple Snapshot Manager tooconnect kullanma ve StorSimple cihazları yönetme](storsimple-snapshot-manager-manage-devices.md) |
| Bağlama birimleri<br>Birimler hakkındaki bilgileri görüntüleme<br>Bir birim Sil<br>Birimleri yeniden tara<br>Yapılandırma ve temel bir birimi yedekleyin<br>Yapılandırma ve dinamik yansıtılmış birim yedekleme |[StorSimple Snapshot Manager tooview kullanın ve birimleri yönetme](storsimple-snapshot-manager-manage-volumes.md) |
| Birim grupları görüntüle<br>Birim grubu oluştur<br>Bir birim grubunu yedekleyin<br>Bir birim grubu Düzenle<br>Bir birim grubu Sil |[StorSimple Snapshot Manager toocreate kullanma ve birim grupları yönetme](storsimple-snapshot-manager-manage-volume-groups.md) |
| Bir yedekleme İlkesi Oluştur <br>Yedekleme ilkesini Düzenle<br>Bir yedekleme ilkesi silme |[StorSimple Snapshot Manager toocreate kullanın ve yedekleme ilkelerini yönetme](storsimple-snapshot-manager-manage-backup-policies.md) |
| Zamanlanmış yedekleme işleri görüntüle ve Yönet<br>Son yedekleme işleri görüntüle ve Yönet<br>Görüntüleme ve şu anda çalışan yedekleme işi yönetme |[StorSimple Snapshot Manager tooview kullanma ve yedekleme işlerini yönetme](storsimple-snapshot-manager-manage-backup-jobs.md) |
| Bir birime geri yükleme<br>Bir birim veya birim grubu kopyalama<br>Yedek Sil<br>Bir dosya kurtarma<br>Merhaba StorSimple Snapshot Manager veritabanını geri yükle |[StorSimple anlık görüntü Yöneticisi'ni kullanın toomanage hello yedekleme kataloğu](storsimple-snapshot-manager-manage-backup-catalog.md) |

## <a name="next-steps"></a>Sonraki adımlar
[StorSimple anlık görüntü Yöneticisi karşıdan](https://www.microsoft.com/download/details.aspx?id=44220).

