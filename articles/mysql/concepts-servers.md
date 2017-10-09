---
title: "MySQL için Azure veritabanında aaaServer kavramları | Microsoft Docs"
description: "Bu konu, MySQL sunucuları için Azure veritabanı ile çalışmak için önemli noktalar ve yönergeler sağlar."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 07/06/2017
ms.openlocfilehash: 4d994cbdbde93ac5af3f4a2a7375b5851bebb1cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="server-concepts-in-azure-database-for-mysql"></a>Azure veritabanı için MySQL Server kavramları
Bu konu, MySQL sunucuları için Azure veritabanı ile çalışmak için önemli noktalar ve yönergeler sağlar.

## <a name="what-is-an-azure-database-for-mysql-server"></a>MySQL sunucusu için bir Azure veritabanı nedir?

Bir Azure MySQL sunucusu için birden fazla veritabanı için merkezi bir yönetim noktası veritabanıdır. Bu, hello şirket içi dünyada tanıyor olabileceği aynı MySQL server yapı hello olur. Özellikle, hello Azure veritabanı için MySQL hizmeti yönetilen, performans garantileri sağlar, erişimi ve sunucu düzeyinde özellikler sunar.

Azure veritabanı MySQL sunucusu için:

- Bir Azure aboneliği içinde oluşturulur.
- Merhaba üst veritabanları kaynaktır.
- Veritabanları için bir ad alanı sağlar.
- Bir kapsayıcı güçlü ömrü semantiği ile - bir sunucu silme ve içerdiği hello veritabanları siler.
- Bir bölgedeki kaynakları collocates.
- Bağlantı uç noktasının sunucu ve veritabanı erişimi sağlar.
- Merhaba kapsamını tooits veritabanları uygulama yönetimi ilkeleri için sağlar: oturum açma, güvenlik duvarı, kullanıcılar, roller, yapılandırmaları, vb..
- Birden çok sürümlerinde kullanılabilir. Daha fazla bilgi için bkz: [desteklenen Azure veritabanı için MySQL veritabanı sürümleri](./concepts-supported-versions.md).

MySQL sunucusu için Azure Veritabanı içinde bir veya birden fazla veritabanı oluşturabilirsiniz. Tüm hello kaynakları toocreate sunucu tooutilize başına tek bir veritabanı opt veya birden çok veritabanları tooshare hello kaynakları oluşturun. Merhaba fiyatlandırma yapılandırılmış sunucu başına, fiyatlandırma katmanının hello yapılandırmasını temel alarak, işlem birimleri, depolama (GB). Daha fazla bilgi için bkz: [fiyatlandırma katmanlarına](./concepts-service-tiers.md).

## <a name="how-do-i-connect-and-authenticate-tooan-azure-database-for-mysql-server"></a>Nasıl bağlanmak ve tooan Azure veritabanı MySQL sunucusu için kimlik doğrulaması?

Merhaba aşağıdaki öğeleri tooyour veritabanı güvenli erişim sağlamaya yardımcı olur.

|||
| :-- | :-- |
| **Kimlik doğrulama ve yetkilendirme** | MySQL sunucusu için Azure veritabanı yerel MySQL kimlik doğrulamasını destekler. Bağlanın ve tooserver hello sunucunun yönetici oturum açma ile kimlik doğrulaması. |
| **Protokol** | Merhaba hizmeti MySQL tarafından kullanılan bir ileti tabanlı iletişim kuralı destekler. |
| **TCP/IP'Yİ** | Merhaba Protokolü UNIX etki alanı Yuva üzerinden ve TCP/IP üzerinden desteklenir. |
| **Güvenlik duvarı** | toohelp verilerinizi korumaya, tüm erişim tooyour veritabanı sunucusu bir güvenlik duvarı kuralı engeller veya tooits veritabanları, hangi bilgisayarların belirtene kadar izne sahip. Bkz: [Azure veritabanı için MySQL Server güvenlik duvarı kuralları](./concepts-firewall-rules.md). |
| **SSL** | Merhaba hizmeti uygulamalarınız ve veritabanı sunucunuz arasında zorunlu SSL bağlantılarını destekler.  Bkz: [yapılandırma SSL bağlantısı'nda uygulama toosecurely bağlanmak tooAzure veritabanı için MySQL](./howto-configure-ssl.md). |
|||

## <a name="how-do-i-manage-a-server"></a>Bir sunucu nasıl yönetebilirim?
Hello Azure portal kullanarak Azure veritabanı için MySQL sunucuları yönetmek veya Azure CLI hello.

## <a name="next-steps"></a>Sonraki adımlar
- Merhaba hizmeti genel bakış için bkz: [Azure veritabanı için MySQL genel bakış](./overview.md)
- Kotalar ve sınırlamalara bağlı olarak belirli bir kaynak hakkında bilgi için **hizmet katmanı**, bkz: [hizmet katmanları](./concepts-service-tiers.md)
- Bağlantı toohello hizmeti hakkında daha fazla bilgi için bkz: [Azure veritabanı için MySQL için bağlantı kitaplıkları](./concepts-connection-libraries.md).
