---
title: "aaaSQL veritabanı olağanüstü durum kurtarma ayrıntılarını | Microsoft Docs"
description: "Yönerge ve Azure SQL veritabanı tooperform olağanüstü durum kurtarma ayrıntısına toohelp Koru kullanmak için en iyi uygulamalar, görev kritik iş uygulamaları dayanıklı toofailures ve kesintileri öğrenin."
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: b44a269c-fe2a-404f-b013-290030860bd1
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 07/31/2016
ms.author: sashan
ms.openlocfilehash: bf17857a19fdebddf0d4f55e4db3a1b33efb4e8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="performing-disaster-recovery-drill"></a>Olağanüstü durum kurtarma ayrıntıya gerçekleştirme
Kurtarma iş akışı için uygulama hazırlık doğrulanması düzenli aralıklarla gerçekleştirilen önerilir. Bu yük devretme doğrulanıyor hello uygulama davranışına ve veri kaybı ve/veya başlangıç engellemeyi etkilerini içerir iyi bir mühendislik uygulamadır. Ayrıca, çoğu endüstri standartlarına göre gerekli iş sürekliliği sertifika kapsamında değildir.

Bir olağanüstü durum kurtarma ayrıntıya gerçekleştirme oluşur:

* Benzetirme veri katmanı kesinti
* Kurtarma
* Uygulama bütünlüğü post kurtarma doğrula

Nasıl bağlı olarak, [uygulamanız iş sürekliliği için tasarlanmış](sql-database-business-continuity.md), hello iş akışı tooexecute hello ayrıntıya farklılık gösterir. Aşağıda Azure SQL veritabanı hello bağlamında bir olağanüstü durum kurtarma ayrıntıya gerçekleştirme hello en iyi uygulamaları açıklar.

## <a name="geo-restore"></a>Coğrafi Geri Yükleme
bir olağanüstü durum kurtarma ayrıntıya yürütülürken tooprevent hello olası veri kaybı hello üretim ortamında bir kopyası oluşturuluyor ve kullanılarak test ortamı kullanarak hello ayrıntıya gerçekleştirme tooverify hello uygulamanın yük devretme iş akışı öneririz.

#### <a name="outage-simulation"></a>Kesinti benzetimi
toosimulate kesinti Merhaba, silebilir veya hello kaynak veritabanını yeniden adlandırın. Bu uygulama bağlantısı hataları neden olur.

#### <a name="recovery"></a>Kurtarma
* Açıklandığı gibi Hello coğrafi geri yükleme hello veritabanı farklı bir sunucu gerçekleştirmeniz [burada](sql-database-disaster-recovery.md).
* Değişiklik hello uygulama yapılandırma tooconnect toohello kurtarılan veritabanı ve izleme hello [bir veritabanını kurtarma işleminden sonra yapılandırma](sql-database-disaster-recovery.md) toocomplete hello Kurtarma Kılavuzu.

#### <a name="validation"></a>Doğrulama
* Merhaba uygulama bütünlüğü post Kurtarma (bağlantı dizeleri, oturum açma bilgileri, temel işlevselliğini test etme veya diğer standart uygulama signoffs yordamları doğrulamaları parçası dahil) doğrulama tam hello detaya gitme.

## <a name="geo-replication"></a>Coğrafi çoğaltma
Coğrafi çoğaltma hello ayrıntıya kullanarak korunan bir veritabanı için planlanan yük devretme toohello ikincil veritabanı alıştırma içerir. Merhaba planlı yük devretme hello rolleri anahtarlı zaman hello birincil ve ikincil veritabanlarıyla hello eşitlenmiş kalmasını sağlar. Aksine planlanmamış yük devretme Merhaba, hello ayrıntıya hello üretim ortamında gerçekleştirilebilir şekilde bu işlem veri kaybına yol değil.

#### <a name="outage-simulation"></a>Kesinti benzetimi
toosimulate hello kesinti Merhaba web uygulaması veya sanal makineye bağlı toohello veritabanı devre dışı bırakabilirsiniz. Bu hello bağlantı hataları hello web istemcileri için sonuçlanır.

#### <a name="recovery"></a>Kurtarma
* Hangi hello hale hello DR bölge noktaları toohello eski ikincil emin hello uygulama yapılandırması olun tamamen erişilebilir yeni birincil.
* Gerçekleştirmek [planlanan yük devretme](scripts/sql-database-setup-geodr-and-failover-database-powershell.md) toomake hello ikincil yeni birincil veritabanı
* Merhaba izleyin [bir veritabanını kurtarma işleminden sonra yapılandırma](sql-database-disaster-recovery.md) toocomplete hello Kurtarma Kılavuzu.

#### <a name="validation"></a>Doğrulama
* Merhaba uygulama bütünlüğü post Kurtarma (bağlantı dizeleri, oturum açma bilgileri, temel işlevselliğini test etme veya diğer standart uygulama signoffs yordamları doğrulamaları parçası dahil) doğrulama tam hello detaya gitme.

## <a name="next-steps"></a>Sonraki adımlar
* toolearn iş sürekliliği senaryoları hakkında bkz [sürekliliği senaryoları](sql-database-business-continuity.md)
* Azure SQL veritabanı otomatik yedeklemeler hakkında toolearn bakın [SQL veritabanı otomatik yedeklemeler](sql-database-automated-backups.md)
* Kurtarma için otomatik yedeklemeler kullanma hakkında toolearn bakın [bir veritabanı hello hizmeti tarafından başlatılan yedeklerden geri yükleme](sql-database-recovery-using-backups.md)
* toolearn daha hızlı kurtarma seçenekleri hakkında bkz [aktif coğrafi çoğaltma](sql-database-geo-replication-overview.md)  
