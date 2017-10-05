---
title: "Çevrimiçi Yedekleme ve geri yükleme Azure Cosmos DB ile | Microsoft Docs"
description: "Otomatik yedekleme gerçekleştirmek ve bir Azure Cosmos DB veritabanını geri yükleme hakkında bilgi edinin."
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
ms.openlocfilehash: 130f0eb259621737d6dbdb151e363915fb334ce1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="automatic-online-backup-and-restore-with-azure-cosmos-db"></a>Otomatik çevrimiçi yedekleme ve geri yükleme ile Azure Cosmos DB
Azure Cosmos DB tüm verilerinizi yedeklerini düzenli aralıklarla otomatik olarak alır. Otomatik yedekleme performansı veya veritabanı işlemlerinizin kullanılabilirliğini etkilemeden alınır. Tüm yedeklemeler ayrı olarak başka bir depolama hizmetinde depolanır ve bu yedekleri bölgesel afetler karşı dayanıklılık için genel olarak çoğaltılır. Yanlışlıkla Comos DB kapsayıcı sildiğinizde ve daha sonra veri kurtarma veya bir olağanüstü durum kurtarma çözümü gerektiren otomatik yedekleme senaryoları için tasarlanmıştır.  

Bu makalede hızlı bir özeti veri artıklık ve kullanılabilirlik Cosmos DB'de ile başlayan ve yedeklemeleri ele alınmaktadır. 

## <a name="high-availability-with-cosmos-db---a-recap"></a>Cosmos DB - bir özeti ile yüksek kullanılabilirlik
Cosmos DB olacak şekilde tasarlanmıştır [Genel dağıtılmış](distribute-data-globally.md) – yük devretme ve saydam çok girişli API'leri güdümlü İlkesi ile birlikte birden çok Azure bölgeler arasında verimliliği ölçeklendirmenizi sağlar. Bir veritabanı sistem sunumu olarak [% 99,99 kullanılabilirlik SLA](https://azure.microsoft.com/support/legal/sla/cosmos-db), Cosmos DB tüm yazma işlemlerini istemciye bildirmeden önce yerel disklere işlemi, bir yerel veri merkezi içinde çoğaltmalarının bir çekirdek tarafından uygulanır. Cosmos DB yüksek kullanılabilirliğini yerel depolama biriminde bulunan güvenir ve hiçbir harici depolama teknolojileri bağlı değildir unutmayın. Ayrıca, veritabanı hesabınızı birden fazla Azure bölgesiyle ilişkiliyse, yazma diğer bölgeler arasında çoğaltılır. Birçok dilediğiniz şekilde veritabanı hesabınızla ilişkili bölgeler salt okunur düşük gecikme, üretilen iş ve erişim verilerinizi ölçeklendirmek için olabilir. Okuma her bölgede (çoğaltılmış) veri çoğaltma kümesi boyunca işlemi kalıcıdır.  

Aşağıdaki çizimde gösterildiği gibi bir tek Cosmos DB kapsayıcıdır [yatay olarak bölümlenmiş](partition-data.md). "Bölüm" Aşağıdaki diyagramda bir daire gösterilir ve her bölüm bir çoğaltma kümesi yüksek oranda kullanılabilir hale gelir. Yerel dağıtım (X ekseni tarafından gösterilen) tek bir Azure bölgesi içinde budur. Ayrıca, her bölüm (karşılık gelen çoğaltma kümesi) sonra genel veritabanı hesabınızı (örneğin, bölgelerde Bu çizim üç – Doğu ABD, Batı ABD ve orta Hindistan) ile ilişkili birden çok bölgeye dağıtılır. "Bölüm kümesi" Genel dağıtılmış olduğu varlık verilerinizi (Y ekseni tarafından gösterilen) her bölgede birden çok kopyasını kapsayan. Veritabanı hesabınızla ilişkili bölgeler öncelik atayabilir ve Cosmos DB olacak saydam yük devretme durumunda olağanüstü durum sonraki bölge. El ile de uygulamanız uçtan uca kullanılabilirliğini test etmek için yük devretme benzetimini de yapabilirsiniz.  

Aşağıdaki resimde artıklık Cosmos DB ile yüksek derecede gösterilmektedir.

![Yüksek düzeyde artıklık Cosmos DB ile](./media/online-backup-and-restore/redundancy.png)

![Yüksek düzeyde artıklık Cosmos DB ile](./media/online-backup-and-restore/global-distribution.png)

## <a name="full-automatic-online-backups"></a>Tam otomatik, çevrimiçi yedeklemeleri
Hata, ı my kapsayıcı veya veritabanı silindi! Cosmos DB ile yalnızca verilerinizi ancak verilerinizin yedekleri da bölgesel olağanüstü yüksek oranda yedekli ve esnek yapılır. Bu otomatik yedeklemeler şu anda yaklaşık dört saat alınır ve her zaman en son 2 yedeklemeler depolanır. Verilerin yanlışlıkla ise bırakılan veya bozuk, lütfen [Azure desteğine başvurun](https://azure.microsoft.com/support/options/) 8 saat içinde. 

Yedeklemeler, performans veya veritabanı işlemlerinizin kullanılabilirliğini etkilemeden alınır. Cosmos DB yedekleme sağlanan RUs kullanma veya performansını etkileyen olmadan ve veritabanınızın kullanılabilirliğini etkilemeden arka planda alır. 

Cosmos DB içinde depolanan verileriniz farklı olarak, otomatik yedeklemeler, Azure Blob Storage hizmetinde depolanır. Düşük gecikme/verimli karşıya yükleme güvence altına almak için yedekleme anlık görüntü Cosmos DB veritabanı hesabınızın geçerli yazma bölge ile aynı bölgede Azure Blob storage'nın bir örneğine yüklenir. Bölgesel olağanüstü durum karşı dayanıklılık için Azure Blob Depolama, yedekleme verilerinizin her anlık görüntü yeniden başka bir bölgeye coğrafi olarak yedekli depolama (GRS) üzerinden çoğaltılır. Aşağıdaki diyagramda, Batı ABD uzak bir Azure Blob Storage hesabında tüm Cosmos DB kapsayıcıyla (üç birincil içindeki tüm bölümlerin Batı ABD, bu örnekte) yedeklenen ve ardından GRS Doğu ABD kopyalandığı gösterir. 

Aşağıdaki resimde GRS Azure depolama birimindeki tüm Cosmos DB varlıkların düzenli tam yedeklemeler gösterilmektedir.

![Tüm Cosmos DB varlıkların GRS Azure storage'da düzenli tam yedeklemeler](./media/online-backup-and-restore/automatic-backup.png)

## <a name="backup-retention-period"></a>Yedekleme saklama süresi
Yukarıda açıklandığı gibi Azure Cosmos DB dört saatte verilerinizin anlık görüntüleri alır ve her bölümün son iki anlık görüntü 30 gün boyunca korur. Bizim uyumluluk düzenlemeleri anlık görüntüleri 90 gün sonra temizlenir.

Kendi anlık görüntülerini korumak istiyorsanız, JSON seçeneği ver Azure Cosmos DB'de kullanabilirsiniz [veri geçiş aracı](import-data.md#export-to-json-file) ek yedeklemeleri zamanlamak için. 

## <a name="restoring-a-database-from-an-online-backup"></a>Bir veritabanı çevrimiçi bir yedekten geri yükleme
Veritabanı veya koleksiyon yanlışlıkla silerseniz, şunları yapabilirsiniz [bir destek bileti dosya](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) veya [Azure destek çağrısı](https://azure.microsoft.com/support/options/) verileri son otomatik yedeklemeden geri yüklemek için. Veri bozulması sorunları nedeniyle veritabanınızı geri yüklemeniz gerekiyorsa bkz [veri bozulması işleme](#handling-data-corruption) olarak bozuk verilerin yedeklemeleri penetrating engellemek için ek adımlar uygulamanız gerekir. Belirli bir anlık görüntüye geri yüklenecek yedekleme için verileri bu anlık görüntü için yedekleme döngüsü boyunca kullanılabilir olduğunu Cosmos DB gerektirir.

## <a name="handling-data-corruption"></a>Veri bozulması işleme
Azure Cosmos DB sistemde her bölümün son iki yedekleme korur. Son sürümlerinden birini geri bu yana bir kapsayıcı (belgeler, grafik, tablo koleksiyonu) veya bir veritabanı yanlışlıkla silindiğinde, bu model çok iyi çalışır. Ancak, durumda kullanıcıların bir veri bozulması sorunu zaman çıkarabilir, Azure Cosmos DB veri bozulmasını farkında ve bozulmayı yedeklemeleri penetrated mümkündür. Bozulması algıladı hemen yedeklemeler bozuk verilerle üzerine korunmaya bozuk kapsayıcı (grafik/koleksiyonu/tablosu) silmeniz gerekir. Dört saat eski olabilir son yedekleme olduğundan, kullanıcı uygulayabileceğiniz [akış değiştirmek](change-feed.md) yakalamak ve son dört kapsayıcı silmeden önce saat değerinde veri depolamak için.

## <a name="next-steps"></a>Sonraki adımlar

Birden çok veri merkezleri veritabanınızda çoğaltmak için bkz: [verilerinizle genel Cosmos DB dağıtmak](distribute-data-globally.md). 

Azure desteği, dosya kişiye [Azure portalından bir bilet dosya](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).

