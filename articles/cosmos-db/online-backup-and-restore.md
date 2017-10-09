---
title: "aaaOnline yedekleme ve geri yükleme ile Azure Cosmos DB | Microsoft Docs"
description: "Bilgi nasıl tooperform otomatik yedekleme ve geri yükleme, bir Azure Cosmos DB veritabanı."
keywords: "Yedekleme ve geri yükleme, çevrimiçi yedekleme"
services: cosmos-db
documentationcenter: 
author: RahulPrasad16
manager: jhubbard
editor: monicar
ms.assetid: 98eade4a-7ef4-4667-b167-6603ecd80b79
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 08/11/2017
ms.author: raprasa
ms.openlocfilehash: a0b464c95681dfc7b5462b02bf04c2c43d6bc16f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="automatic-online-backup-and-restore-with-azure-cosmos-db"></a>Otomatik çevrimiçi yedekleme ve geri yükleme ile Azure Cosmos DB
Azure Cosmos DB tüm verilerinizi yedeklerini düzenli aralıklarla otomatik olarak alır. Merhaba otomatik yedeklemeler hello performans veya veritabanı işlemlerinizin kullanılabilirliğini etkilemeden alınır. Tüm yedeklemeler ayrı olarak başka bir depolama hizmetinde depolanır ve bu yedekleri bölgesel afetler karşı dayanıklılık için genel olarak çoğaltılır. yanlışlıkla Comos DB kapsayıcı sildiğinizde ve daha sonra veri kurtarma veya bir olağanüstü durum kurtarma çözümü gerektiren hello otomatik yedekleme senaryoları için tasarlanmıştır.  

Bu makalede hızlı bir özeti hello veri artıklık ve kullanılabilirlik Cosmos DB'de ile başlayan ve yedeklemeleri ele alınmaktadır. 

## <a name="high-availability-with-cosmos-db---a-recap"></a>Cosmos DB - bir özeti ile yüksek kullanılabilirlik
Cosmos DB olduğu tasarlanmış toobe [Genel dağıtılmış](distribute-data-globally.md) –, yük devretme ve saydam çok girişli API'leri güdümlü İlkesi ile birlikte birden çok Azure bölgeler arasında tooscale verimlilik sağlar. Bir veritabanı sistem sunumu olarak [% 99,99 kullanılabilirlik SLA](https://azure.microsoft.com/support/legal/sla/cosmos-db), Cosmos DB'de tüm hello yazma işlemi taahhüt toolocal çoğaltmalarının bir yerel veri merkezi içinde bir çekirdek tarafından toohello istemci bildirmeden disklerdir. Cosmos DB yüksek kullanılabilirliğini Hello yerel depolama biriminde bulunan güvenir ve hiçbir harici depolama teknolojileri bağlı değildir unutmayın. Ayrıca, veritabanı hesabınızı birden fazla Azure bölgesiyle ilişkiliyse, yazma diğer bölgeler arasında çoğaltılır. tooscale birçok dilediğiniz şekilde veritabanı hesabınızla ilişkili bölgeler salt okunur, üretilen iş ve erişim verilerinizi en düşük gecikme olabilir. Okuma her bölgede (Yinelenmiş) hello veri çoğaltma kümesi boyunca işlemi kalıcıdır.  

Hello Aşağıdaki diyagramda gösterildiği gibi bir tek Cosmos DB kapsayıcıdır [yatay olarak bölümlenmiş](partition-data.md). "Bölüm" diyagramı aşağıdaki hello içinde bir daire gösterilir ve her bölüm bir çoğaltma kümesi yüksek oranda kullanılabilir hale gelir. Yerel bir dağıtım hello (Merhaba X ekseni tarafından gösterilen) tek bir Azure bölgesi içinde budur. Ayrıca, her bölüm (karşılık gelen çoğaltma kümesi) sonra genel veritabanı hesabınızı (örneğin, bu çizimde hello üç Bölgeler – Doğu ABD, Batı ABD ve orta Hindistan) ile ilişkili birden çok bölgeye dağıtılır. Merhaba "bölüm kümesi" Genel dağıtılmış olduğu varlık verilerinizi (Merhaba Y ekseni tarafından gösterilen) her bölgede birden çok kopyasını kapsayan. Veritabanı hesabınızla ilişkili toohello bölgeler öncelik atayabilirsiniz ve Cosmos DB olacak saydam yük devretme toohello sonraki bölgeyi olağanüstü durum durumunda. El ile de yük devretme tootest hello uçtan uca kullanılabilirlik uygulamanızın benzetimini de yapabilirsiniz.  

Merhaba aşağıdaki görüntüde artıklık Cosmos DB ile yüksek derecede hello gösterilmektedir.

![Yüksek düzeyde artıklık Cosmos DB ile](./media/online-backup-and-restore/redundancy.png)

![Yüksek düzeyde artıklık Cosmos DB ile](./media/online-backup-and-restore/global-distribution.png)

## <a name="full-automatic-online-backups"></a>Tam otomatik, çevrimiçi yedeklemeleri
Hata, ı my kapsayıcı veya veritabanı silindi! Cosmos DB ile yalnızca, veriler, ancak hello yedekleme verilerinizin yüksek oranda yedekli ve esnek tooregional olağanüstü da yapılır. Bu otomatik yedeklemeler şu anda yaklaşık dört saat alınır ve her zaman en son 2 yedeklemeler depolanır. Merhaba veri yanlışlıkla ise bırakılan veya bozuk, lütfen [Azure desteğine başvurun](https://azure.microsoft.com/support/options/) 8 saat içinde. 

Merhaba yedeklemeleri hello performans veya veritabanı işlemlerinizin kullanılabilirliğini etkilemeden alınır. Cosmos DB hello yedekleme sağlanan RUs kullanma veya hello performansını etkileyen olmadan ve veritabanınızı hello kullanılabilirliğini etkilemeden hello arka planda alır. 

Cosmos DB içinde depolanan farklı olarak, verilerinizin hello otomatik yedeklemeler, Azure Blob Storage hizmetinde depolanır. tooguarantee hello düşük gecikme/verimli karşıya yükleme, yedeklemenin hello anlık görüntüsüdür Azure Blob depolama alanına karşıya yüklenen tooan örneğini hello hello geçerli yazma bölge Cosmos DB veritabanı hesabının aynı bölgede. Bölgesel olağanüstü durum karşı dayanıklılık için Azure Blob Depolama, yedekleme verilerinizin her anlık görüntü yeniden coğrafi olarak yedekli depolama (GRS) tooanother bölge çoğaltılır. Merhaba Aşağıdaki diyagramda hello tüm Cosmos DB kapsayıcıyla (üç birincil içindeki tüm bölümlerin Batı ABD, bu örnekte) Batı ABD uzak bir Azure Blob Storage hesabında yedeklenir ve ardından GRS tooEast BİZE kopyalandığı gösterilmektedir. 

Merhaba aşağıdaki görüntüde GRS Azure depolama birimindeki tüm Cosmos DB varlıkların düzenli tam yedeklemeler gösterilmektedir.

![Tüm Cosmos DB varlıkların GRS Azure storage'da düzenli tam yedeklemeler](./media/online-backup-and-restore/automatic-backup.png)

## <a name="backup-retention-period"></a>Yedekleme saklama süresi
Yukarıda açıklandığı gibi Azure Cosmos DB dört saatte verilerinizin anlık görüntüleri alır ve her bölümün hello son iki anlık görüntü 30 gün boyunca korur. Bizim uyumluluk düzenlemeleri anlık görüntüleri 90 gün sonra temizlenir.

Kendi anlık görüntüleri toomaintain istiyorsanız hello verme tooJSON seçeneği hello Azure Cosmos DB kullanabilirsiniz [veri geçiş aracı](import-data.md#export-to-json-file) tooschedule ek yedeklemeler. 

## <a name="restoring-a-database-from-an-online-backup"></a>Bir veritabanı çevrimiçi bir yedekten geri yükleme
Veritabanı veya koleksiyon yanlışlıkla silerseniz, şunları yapabilirsiniz [bir destek bileti dosya](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) veya [Azure destek çağrısı](https://azure.microsoft.com/support/options/) hello son otomatik yedekleme toorestore hello verileri. Veri bozulması sorunları nedeniyle veritabanınıza toorestore gerekiyorsa, bkz: [veri bozulması işleme](#handling-data-corruption) gerektiği tootake ek tooprevent hello bozuk veri penetrating hello yedeklemelerden adımları. Belirli bir anlık görüntüsünü geri, yedekleme toobe için hello veri hello süre hello yedekleme döngüsü bu anlık görüntü için kullanılabilir olduğunu Cosmos DB gerektirir.

## <a name="handling-data-corruption"></a>Veri bozulması işleme
Azure Cosmos DB hello son iki yedekleme her bölümün hello sistemde korur. Merhaba son sürümlerinden birini geri bu yana bir kapsayıcı (belgeler, grafik, tablo koleksiyonu) veya bir veritabanı yanlışlıkla silindiğinde, bu model çok iyi çalışır. Ancak, hello kullanıcıların bir veri bozulması sorunu çıkarabilir, Azure Cosmos DB hello veri bozulmasını farkında ve Bozulması hello mümkün olduğunda çalışması hello yedeklemeleri penetrated. Bozulması algıladı hemen yedeklemeler bozuk verilerle üzerine korunmaya bozuk hello kapsayıcı (grafik/koleksiyonu/tablosu) silmeniz gerekir. Dört saat eski olabilir Hello son yedekleme beri hello kullanıcı uygulayabileceğiniz [akış değiştirme](change-feed.md) toocapture ve deposu hello son dört hello kapsayıcı silmeden önce saat değerinde veri.

## <a name="next-steps"></a>Sonraki adımlar

birden çok veri merkezleri, veritabanınızda tooreplicate gördüğünüz [verilerinizle genel Cosmos DB dağıtmak](distribute-data-globally.md). 

toofile kişi Azure Destek [hello Azure portal biletindeki dosya](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).

