---
title: Power BI ile SQL Data Warehouse aaaUse | Microsoft Docs
description: "Power BI çözümleri geliştirmek için Azure SQL Data Warehouse ile kullanma ipuçları."
services: sql-data-warehouse
documentationcenter: NA
author: mlee3gsd
manager: jhubbard
editor: 
ms.assetid: b12bee87-2268-40c2-81bf-ab27588b32e8
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: martinle;barbkess
ms.openlocfilehash: a3a347493d07af6824a561567f05894cfe3c0471
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-power-bi-with-sql-data-warehouse"></a>Power BI ile SQL veri ambarı kullanın
Azure SQL Database'de olduğu gibi kullanıcı tooleverage güçlü mantıksal aşağı itme hello analitik Power BI özelliklerini yanında SQL veri ambarı doğrudan bağlantı sağlar.  Merhaba veri keşfetmenizde doğrudan bağlantı ile sorgular geri tooyour Azure SQL Data Warehouse gerçek zamanlı olarak gönderilir.  Bu, birleştirilmiş SQL Data Warehouse, kullanıcıların sağlar hello ölçeğini ile toocreate dinamik raporlar terabayt veri göre dakika cinsinden.  Ayrıca, Power BI düğmesi açık hello hello giriş kullanıcılara toodirectly Azure diğer bölümlerden bilgilerini toplamadan Power BI tootheir SQL Data Warehouse bağlanın.

Doğrudan bağlantı Lütfen Not kullanırken:

* (Daha fazla Ayrıntılar için aşağıya bakın) bağlanırken Hello tam sunucu adını belirtin
* Merhaba veritabanı yapılandırılması için güvenlik duvarı kuralları çok "erişim tooAzure Hizmetleri izin ver" emin olun.
* Bir sütunun seçilmesi veya bir filtre eklemeden gibi her eylem hello veri ambarı doğrudan sorgu
* Döşeme yaklaşık 15 (yenileme zamanlanan toobe gerekmez) dakikada bir yenilenir.
* Soru- cevap veri kümeleri doğrudan bağlanmak için kullanılabilir değil
* Şema değişiklikleri otomatik olarak toplanmaz
* Tüm doğrudan bağlanmak sorguları 2 dakika sonra zaman aşımına uğrar

Biz tooimprove hello deneyimleri devam ederken bu kısıtlamaları ve notlar değişebilir. Merhaba adımları tooconnect ayrıntılı aşağıda.  

## <a name="using-hello-open-in-power-bi-button"></a>Merhaba 'Power bı'da Aç' düğmesini kullanarak
Power BI düğmesi açık hello ile Merhaba en kolay yolu toomove SQL veri ambarı ve Power BI arasında olur. Bu düğme sağlar tooseamlessly başlamak Power BI'da yeni panolar oluşturma.  

1. başlatılan tooget hello Klasik Azure Portalı'nda tooyour SQL Data Warehouse örneğine gidin.
2. Merhaba 'Power bı'da Aç' düğmesini tıklatın.
3. Biz mümkün toosign değilseniz, size, doğrudan veya Power BI hesabınız yoksa, toosign bileşenini gerekir.  
4. SQL veri ambarı hello bilgileriyle SQL Data Warehouse bağlantı sayfası toohello önceden doldurulmuş yönlendirilir.
5. Kimlik bilgilerinizi girdikten sonra tam olarak bağlı tooyour SQL Data Warehouse olacaktır.

## <a name="connecting-through-hello-power-bi-portal"></a>Merhaba Power BI Portalı aracılığıyla bağlanma
Toplama toousing hello içinde Aç Power BI düğmesi, kullanıcıların hello Power BI Portal tootheir SQL Data Warehouse da bağlanabilirsiniz.

1. Merhaba Gezinti bölmesinin hello altındaki ' Veri Al' tıklayın.
2. 'Veritabanlarını' seçin.
3. Bir kez 'Azure SQL Data Warehouse' hello veritabanlarını sayfasında, seçin ve 'Bağlan' ı.
4. Merhaba gerekli bağlantı bilgileri girin.  Sunucu adını ve veritabanı adını hello Azure portalında bulunabilir.
5. Size, toohello ana sayfa bağlantınızı 'Veri kümeleri' altında yeni bir giriş yapıldıktan sonra ve Power BI örneğinizi hello adıyla görünür yeniden yönlendirilir.  
6. Merhaba yeni veri kümesi tooexplore tıklayabilirsiniz tüm hello tabloların ve görünümlerin veritabanınızdaki. Bir sütunun seçilmesi, visual dinamik olarak oluşturma bir sorgu geri toohello kaynağı gönderir. Bu görsel yeni bir raporda kaydedilebilir ve geri tooyour Pano sabitlenir.

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop/
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integration/

<!--MSDN references-->

<!--Other Web references-->
