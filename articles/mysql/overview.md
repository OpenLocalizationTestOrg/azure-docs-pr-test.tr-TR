---
title: "Azure veritabanı aaaOverview MySQL ilişkisel veritabanı hizmeti için | Microsoft Docs"
description: "Hello Azure veritabanı MySQL ilişkisel veritabanı hizmeti için genel bakış."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 08/02/2017
ms.custom: mvc
ms.openlocfilehash: f02493e2c3c38ccab408a718f98861600481812d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-database-for-mysql-service-introduction"></a>Azure veritabanı için MySQL nedir? Hizmet giriş
Azure için MySQL veritabanıdır hello Microsoft bulut dayalı bir ilişkisel veritabanı hizmeti [MySQL Community Edition](https://www.mysql.com/products/community/) veritabanı altyapısı.  Azure veritabanı için MySQL sunar:

- Tahmin edilebilir performans birden çok hizmet düzeyleri
- Hiçbir uygulama kapalı kalma süresi ile dinamik ölçeklenebilirlik
- Yerleşik yüksek kullanılabilirlik
- Veri koruma

Bu özellikler neredeyse hiçbir yönetim gerektirir ve tüm hiçbir ek ücret sağlanır. Hızlı Uygulama geliştirme ve zaman toomarket hızlandırmaya, yerine çok değerli bir zaman ve kaynak toomanaging sanal makineleri ve altyapıyı ayırma toofocus sağlarlar. Ayrıca, hello uygulamanızla kaynak araçları ve seçtiğiniz platform açın ve hello hızı ve toolearn yeni yetenekler gerek kalmadan işinizin talep verimliliği ile teslim toodevelop devam edebilirsiniz.

![Azure veritabanı için MySQL kavramsal diyagramı](media/overview/1-azure-db-for-mysql-conceptual-diagram.png)

Bu makalede MySQL temel kavramlarını ve özelliklerini ilgili tooperformance, ölçeklenebilirlik ve yönetilebilirlik açısından, bağlantılar tooexplore ayrıntılarla giriş tooAzure veritabanı değil. Bu hızlı başlattığınız tooget başlatır bakın:
- [Azure portalını kullanarak MySQL için Azure Veritabanı sunucusu oluşturma](quickstart-create-mysql-server-database-using-azure-portal.md)
- [Azure CLI kullanarak MySQL için Azure Veritabanı sunucusu oluşturma](quickstart-create-mysql-server-database-using-azure-cli.md)

Azure CLI örnekler kümesi için bkz:
- [Azure veritabanı için MySQL için Azure CLI örnekleri](sample-scripts-azure-cli.md)

## <a name="adjust-performance-and-scale-without-downtime"></a>Kesinti olmadan performansı ayarlama ve ölçeklendirme
MySQL hizmeti için Azure veritabanı iki hizmet katmanları sunar: temel ve standart. Her katman farklı performans ve yetenekleri toosupport basit tooheavyweight veritabanı iş yükleri sunar. İlk uygulamanızı küçük bir veritabanı üzerinde için birkaç dolar bir ay sonra hizmet katmanı tooscale ile çözümünüzün kapalı kalma süresi olmadan gereken değişiklik oluşturabilirsiniz. Kaynak gereksinimlerinin değiştirilmesi, veritabanı tootransparently yanıt toorapidly dinamik ölçeklenebilirlik sağlar. Yalnızca gereksinim duyduğunuzda, gereksinim hello kaynaklar için ödeme yaparsınız.

## <a name="monitoring-and-alerting"></a>İzleme ve uyarı
Yukarı ve aşağı çevirdiğinizde hello sağ tıklayın durdurma nasıl bilebilirsiniz? Merhaba yerleşik performans izleme ve işlem birimine dayalı hello performans değerlendirmeleri birlikte özellikleri, uyarı kullanın. Bu özellikleri kullanarak hello etkisini yukarı veya aşağı geçerli göre ölçeklendirme hızla değerlendirebilirsiniz veya proje performans gereksinimlerine. Bkz: [Kavramları: hizmet katmanları](concepts-service-tiers.md) Ayrıntılar için.

## <a name="keep-your-app-and-business-running"></a>Uygulamanızın ve işinizin hiç kesintiye uğramamasını sağlayın
Azure'nın endüstri lideri genel bir veri merkezleri, Microsoft tarafından yönetilen ağ tarafından desteklenen % 99,99 kullanılabilirlik hizmet düzeyi sözleşmesi (SLA), uygulamanızın 7/24 çalıştıran tutmaya yardımcı olur. MySQL sunucusu için her Azure veritabanı ile yerleşik güvenlik, hata toleransı ve oluşturmak ve yönetmek toobuy veya tasarımı, aksi takdirde olması gereken veri koruma yararlanın. MySQL için Azure veritabanı, zaman içinde nokta geri yükleme toorecover sunucu tooan kullanabileceğiniz daha önce durumunda, a kadar 35 gün.

## <a name="secure-your-data"></a>Verilerinizin güvenliğini sağlama
Azure veritabanı hizmetleri gelenek veri güvenliği Azure veritabanı için MySQL erişimi sınırlamak, çalışmıyorken veri ve hareket halinde korumak ve etkinlikleri izlemenize yardımcı özelliklerle anlayışına sahiptir. Merhaba ziyaret [Azure Güven Merkezi](https://www.microsoft.com/en-us/TrustCenter/Security/default.aspx) Azure'nın platform güvenliği hakkında bilgi için.

MySQL hizmeti için Hello Azure veritabanı veri çalışmıyorken için depolama şifrelemesi kullanır. Veri yedekleri, dahil olmak üzere (sorgu çalıştırılırken hello altyapısı tarafından oluşturulan geçici dosyalar hello durumla) diskteki şifrelenir. Azure depolama şifreleme dahil AES 256 bit şifreleme Hello hizmet kullanıyor ve hello anahtarları sistem tarafından yönetiliyor. Depolama şifreleme her zaman açıktır ve devre dışı bırakılamaz.

MySQL hizmeti yapılandırılmış toorequire için varsayılan olarak, Azure veritabanı hello [SSL bağlantı güvenliği](./concepts-ssl-connection-security.md) veri hareket halinde hello ağ üzerinden için. Veritabanı sunucunuz ve istemci uygulamalarınız arasında SSL bağlantılarını zorlamayı "Merhaba ortadaki adam" saldırılarına karşı hello veri akışı hello sunucusu ve uygulamanız arasındaki şifreleyerek korunmasına yardımcı.  İsteğe bağlı olarak, istemci uygulamanız SSL bağlantısını desteklemiyorsa tooyour veritabanı hizmeti bağlanmak için SSL gerektirme devre dışı bırakabilirsiniz.

## <a name="next-steps"></a>Sonraki Adımlar
Bir giriş tooAzure veritabanı için MySQL okuyun ve hello sorusunu yanıtladığınıza göre "Azure veritabanı için MySQL nedir?", yapmaya hazırsınız:
- Merhaba fiyatlandırma sayfası maliyet karşılaştırmaları ve hesaplayıcıları için bkz. [Fiyatlandırma](https://azure.microsoft.com/pricing/details/mysql/)
- İlk sunucunuzun oluşturarak başlayın. [Azure portalını kullanarak MySQL için Azure Veritabanı sunucusu oluşturma](quickstart-create-mysql-server-database-using-azure-portal.md)
- Python, PHP, Ruby, C kullanarak ilk uygulamanızı oluşturma\#, Java, Node.js: [bağlantı kitaplıkları kullanılan tooconnect tooAzure veritabanı için MySQL](concepts-connection-libraries.md)
