---
title: "Azure veritabanında PostgreSQL için aaaServer kavramları | Microsoft Docs"
description: "Bu konu, PostgreSQL sunucuları için Azure veritabanı ile çalışmak için önemli noktalar ve yönergeler sağlar."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 07/06/2017
ms.openlocfilehash: 9cc7816992f2ddedd76fdf906075a723b97720a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-servers"></a>Azure veritabanı PostgreSQL sunucuları için
Bu konu, PostgreSQL sunucuları için Azure veritabanı ile çalışmak için önemli noktalar ve yönergeler sağlar.

## <a name="what-is-an-azure-database-for-postgresql-server"></a>Azure veritabanı PostgreSQL sunucu için nedir?
Bir Azure PostgreSQL sunucusu için birden fazla veritabanı için merkezi bir yönetim noktası veritabanıdır. Bu, hello şirket içi dünyada tanıyor olabileceği aynı PostgreSQL server yapı hello olur. Özellikle, hello PostgreSQL hizmet yönetilen, performans garantileri sağlar, erişimi ve sunucu düzeyinde özellikler sunar.

Azure veritabanı PostgreSQL sunucu için:

- Bir Azure aboneliği içinde oluşturulur.
- Merhaba üst veritabanları kaynaktır.
- Veritabanları için bir ad alanı sağlar.
- Bir kapsayıcı güçlü ömrü semantiği ile - bir sunucu silme ve içerdiği hello veritabanları siler.
- Bir bölgedeki kaynakları collocates.
- Sunucu ve veritabanına erişim için bir bağlantı uç noktasının sağlar (. postgresql.database.azure.com).
- Merhaba kapsamını tooits veritabanları uygulama yönetimi ilkeleri için sağlar: oturum açma, güvenlik duvarı, kullanıcılar, roller, yapılandırmaları, vb..
- Birden çok sürümlerinde kullanılabilir. Daha fazla bilgi için bkz: [desteklenen PostgreSQL veritabanı sürümleri](concepts-supported-versions.md).
- Kullanıcılar tarafından genişletilebilirdir. Daha fazla bilgi için bkz: [PostgreSQL uzantıları](concepts-extensions.md).

Bir Azure veritabanı içinde PostgreSQL sunucu için bir veya birden çok veritabanı oluşturabilirsiniz. Tüm hello kaynakları toocreate sunucu tooutilize başına tek bir veritabanı opt veya birden çok veritabanları tooshare hello kaynakları oluşturun. Merhaba fiyatlandırma yapılandırılmış sunucu başına, fiyatlandırma katmanının hello yapılandırmasını temel alarak, işlem birimleri, depolama (GB). Daha fazla ayrıntı için bkz: [fiyatlandırma katmanlarına](./concepts-service-tiers.md).

## <a name="how-do-i-connect-and-authenticate-tooan-azure-database-for-postgresql-server"></a>Nasıl bağlanmak ve tooan Azure veritabanı PostgreSQL sunucusu için kimlik doğrulaması?
Merhaba aşağıdaki öğeleri tooyour veritabanı güvenli erişim sağlamaya yardımcı olur.

|||
| :-- | :-- |
| **Kimlik doğrulama ve yetkilendirme** | Azure veritabanı PostgreSQL sunucu için yerel PostgreSQL kimlik doğrulamasını destekler. Bağlanın ve tooserver hello sunucunun yönetici oturum açma ile kimlik doğrulaması. |
| **Protokol** | Merhaba hizmeti PostgreSQL tarafından kullanılan bir ileti tabanlı iletişim kuralı destekler. |
| **TCP/IP'Yİ** | Merhaba Protokolü UNIX etki alanı Yuva üzerinden ve TCP/IP üzerinden desteklenir. |
| **Güvenlik duvarı** | toohelp verilerinizi korumaya, tüm erişim tooyour veritabanı sunucusu bir güvenlik duvarı kuralı engeller veya tooits veritabanları, hangi bilgisayarların belirtene kadar izne sahip. Bkz: [Azure veritabanı PostgreSQL sunucunun güvenlik duvarı kuralları için](concepts-firewall-rules.md). |
|||

## <a name="how-do-i-manage-a-server"></a>Bir sunucu nasıl yönetebilirim?
Azure portal veya hello kullanarak PostgreSQL sunucularını hello için Azure veritabanı yönetebilirsiniz [Azure CLI](/cli/azure/postgres).

## <a name="next-steps"></a>Sonraki adımlar
- Merhaba hizmeti genel bakış için bkz: [Azure veritabanı PostgreSQL genel bakış](overview.md)
- Kotalar ve sınırlamalara bağlı olarak belirli bir kaynak hakkında bilgi için **hizmet katmanı**, bkz: [hizmet katmanları](concepts-service-tiers.md)
- Bağlantı toohello hizmeti hakkında daha fazla bilgi için bkz: [PostgreSQL için Azure veritabanı için bağlantı kitaplıkları](concepts-connection-libraries.md).
