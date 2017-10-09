---
title: "Azure veritabanı için MySQL aaaDatabase uygulaması geliştirmeye genel bakış | Microsoft Docs"
description: "Bir geliştirici uygulama kodu tooconnect tooAzure veritabanı için MySQL yazılırken izlemeniz gereken tasarım konuları sunar"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: f08df605eba21b4ba4b43565c0a7ded95779a171
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="application-development-overview-for-azure-database-for-mysql"></a>Azure veritabanı için MySQL için uygulama geliştirmeye genel bakış 
Bu makalede, bir geliştirici uygulama kodu tooconnect tooAzure veritabanı için MySQL yazılırken izlemeniz gereken tasarım konuları anlatılmaktadır. 

> [!TIP]
> Toocreate bir sunucu oluşturmak nasıl sunucu tabanlı güvenlik duvarı, sunucu özellikleri görüntülemek, veritabanı oluşturma, bağlanma ve sorgulama çalışma ekranı ve mysql.exe kullanarak bir öğretici gösteren için bkz: [ilk Azure MySQL veritabanınızı tasarlama](tutorial-design-database-using-portal.md)

## <a name="language-and-platform"></a>Dil ve platform
Çeşitli programlama dilleri ve platformları için kod örnekleri mevcuttur. Toohello kod örnekleri, bağlantılar bulabilirsiniz: [bağlantı kitaplıkları kullanılan tooconnect tooAzure veritabanı için MySQL](concepts-connection-libraries.md)

## <a name="tools"></a>Araçlar
Azure veritabanı için MySQL kullanır hello MySQL community sürümü, MySQL genel yönetim araçlarını mysql.exe gibi çalışma ekranı veya MySQL yardımcı programları gibi uyumlu [phpMyAdmin](https://www.phpmyadmin.net/), [Navicat](https://www.navicat.com/products/navicat-for-mysql)ve diğerleri. Merhaba veritabanı hizmeti ile Merhaba Azure portal, Azure CLI ve REST API'leri toointeract de kullanabilirsiniz.

## <a name="resource-limitations"></a>Kaynak sınırlamaları
Azure MySQL veritabanı iki farklı mekanizmalarını kullanarak hello kaynakları kullanılabilir tooa sunucusu yönetir: 
- Kaynak Yönetimi 
- Sınırları zorlama.

## <a name="security"></a>Güvenlik
Azure MySQL veritabanı sınırlama erişim, koruma verileri, yapılandırma kullanıcılar ve rolü ve bir MySQL veritabanı etkinliklerini izleme için kaynaklar sağlar.

## <a name="authentication"></a>Kimlik Doğrulaması
Azure MySQL veritabanı sunucu kimlik doğrulaması kullanıcı ve oturum açma bilgileri destekler.

## <a name="resiliency"></a>Dayanıklılık
TooMySQL veritabanına bağlanırken geçici bir hata ortaya çıktığında, kodunuzu hello çağrı yeniden denemeniz gerekir. Böylece, hello SQL veritabanı ile birden çok istemci aynı anda yeniden deneniyor doldurmaya değil hello yeniden deneme mantığı kullanım geri alma mantığı, öneririz.

- Kod örnekleri: hello dili için örnek gösteren kod örnekleri mantığı yeniden denemek için bkz: [bağlantı kitaplıkları kullanılan tooconnect tooAzure veritabanı için MySQL](concepts-connection-libraries.md)

## <a name="managing-connections"></a>Bağlantıları Yönetme
Veritabanı bağlantıları sınırlı bir kaynak olduğundan, bağlantı duyarlı kullanmayı, MySQL veritabanınızı erişirken tooachieve daha iyi performans öneririz.
- Bağlantı havuzu veya kalıcı bağlantılar kullanarak hello veritabanı erişim.
- Kısa bağlantı ömrü kullanarak hello veritabanı erişim. 
- Kullanım yeniden deneme mantığı uygulamanızda hello bağlantı girişimi, toocatch hataları tooconcurrent bağlantılar nedeniyle hello noktada hello maksimum izin verilen ulaştı. Merhaba mantığı yeniden deneyin ve kısa bir gecikme ayarlama hello ek bağlantı denemeleri önce rastgele bir süre bekleyin.
