---
title: "MySQL için Azure veritabanındaki kısıtlamaları | Microsoft Docs"
description: "MySQL için Azure veritabanındaki Önizleme sınırlamaları açıklar."
services: mysql
author: jasonh
ms.author: kamathsun
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: c61d70897b66c2ffee819ac98c38ab75000db907
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="limitations-in-azure-database-for-mysql-preview"></a>MySQL (Önizleme) Azure veritabanındaki sınırlamaları
MySQL hizmeti için Azure veritabanı genel önizlemede değil. Aşağıdaki bölümlerde, kapasite ve veritabanı hizmeti işlevsel sınırları açıklanmaktadır.

## <a name="service-tier-maximums"></a>Hizmet katmanı üst sınırlar
Azure veritabanı MySQL için bir sunucu oluştururken seçebileceğiniz birden çok hizmet katmanı vardır. Daha fazla bilgi için bkz: [her hizmet katmanında nelerin kullanılabildiğini anlama](concepts-service-tiers.md).  

Olduğundan maksimum sayısını bağlantıları, işlem birimleri ve depolama her hizmet katmanında hizmet Önizleme sırasında şu şekilde: 

|                            |                   |
| :------------------------- | :---------------- |
| **En fazla bağlantı**        |                   |
| Temel 50 işlem birimleri     | 50 bağlantıları    |
| Temel 100 işlem birimleri    | 100 bağlantılar   |
| Standart 100 işlem birimleri | 200 bağlantıları   |
| Standart 200 işlem birimleri | 300 bağlantıları   |
| Standart 400 işlem birimleri | 400 bağlantıları   |
| Standart 800 işlem birimleri | 500 bağlantılar   |
| **En fazla işlem birimleri**      |                   |
| Temel hizmet katmanı         | 100 işlem birimleri |
| Standart hizmet katmanı      | 800 işlem birimleri |
| **En fazla depolama**            |                   |
| Temel hizmet katmanı         | 1 TB              |
| Standart hizmet katmanı      | 1 TB              |

Çok fazla bağlantı erişildiğinde, aşağıdaki hata iletisini alabilirsiniz:
> 1040 (08004). hata: Çok fazla bağlantı

## <a name="preview-functional-limitations"></a>Önizleme işlevsel sınırlamaları:
### <a name="scale-operations"></a>Ölçek işlemleri:
1.  Dinamik sunucularının hizmet katmanları arasında ölçeklendirme şu anda desteklenmiyor. Diğer bir deyişle, temel ve standart hizmet katmanları arasında geçiş yapma.
2.  Önceden oluşturulmuş sunucusundaki depolama dinamik talep üzerine çıktığını şu anda desteklenmiyor.
3.  Sunucu depolama boyutunu azaltmak desteklenmiyor.

### <a name="server-version-upgrades"></a>Sunucu sürüm yükseltme:
- Ana veritabanı altyapısı sürümleri arasında otomatik geçiş şu anda desteklenmiyor.

### <a name="subscription-management"></a>Abonelik Yönetimi:
- Önceden oluşturulmuş sunucuları abonelik ve kaynak grubu arasında dinamik olarak taşıma şu anda desteklenmiyor.

### <a name="point-in-time-restore"></a>Noktası-içinde--geri yükleme:
1.  Farklı bir hizmet katmanı ve/veya bir işlem birimleri ve depolama boyutu geri izin verilmiyor.
2.  Bırakılan bir sunucuya geri yüklenmesi desteklenmez.

## <a name="next-steps"></a>Sonraki Adımlar:
[Her hizmet katmanında nelerin kullanılabildiğini](concepts-service-tiers.md)
[MySQL veritabanı sürümleri desteklenir](concepts-supported-versions.md)
