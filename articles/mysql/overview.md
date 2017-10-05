---
title: "MySQL ilişkisel veritabanı hizmeti için Azure veritabanı'nın genel bakış | Microsoft Docs"
description: "Azure veritabanı MySQL ilişkisel veritabanı hizmeti için genel bakış."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 08/02/2017
ms.custom: mvc
ms.openlocfilehash: a1becaf8465f68ecac768c5c6b2dbc95e8ff7278
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="what-is-azure-database-for-mysql-service-introduction"></a>Azure veritabanı için MySQL nedir? Hizmet giriş
Azure için MySQL veritabanıdır göre Microsoft bulut ilişkisel veritabanı hizmeti [MySQL Community Edition](https://www.mysql.com/products/community/) veritabanı altyapısı.  Azure veritabanı için MySQL sunar:

- Tahmin edilebilir performans birden çok hizmet düzeyleri
- Hiçbir uygulama kapalı kalma süresi ile dinamik ölçeklenebilirlik
- Yerleşik yüksek kullanılabilirlik
- Veri koruma

Bu özellikler neredeyse hiçbir yönetim gerektirir ve tüm hiçbir ek ücret sağlanır. Hızlı Uygulama geliştirme ve pazara zamanınızı hızlandırmaya yerine değerli zaman ve sanal makineleri ve altyapıyı yönetmek için kaynak ayırma odaklanmak olanak sağlar. Ayrıca, seçtiğiniz platform ve açık kaynaklı araçları ile uygulamanızı geliştirin ve hız ve yeni yetenekler öğrenmek zorunda kalmadan işinizin talep verimliliği ile teslim etmek devam edebilirsiniz.

![Azure veritabanı için MySQL kavramsal diyagramı](media/overview/1-azure-db-for-mysql-conceptual-diagram.png)

Bu makale Azure veritabanı giriş MySQL temel kavramlar ve performans, ölçeklenebilirlik ve yönetilebilirlik ayrıntıları keşfetmek için bağlantılar ile ilgili özellikler için yazılmıştır. Başlamanıza yardımcı olacak şu hızlı başlangıçlara bakın:
- [Azure portalını kullanarak MySQL için Azure Veritabanı sunucusu oluşturma](quickstart-create-mysql-server-database-using-azure-portal.md)
- [Azure CLI kullanarak MySQL için Azure Veritabanı sunucusu oluşturma](quickstart-create-mysql-server-database-using-azure-cli.md)

Azure CLI örnekler kümesi için bkz:
- [Azure veritabanı için MySQL için Azure CLI örnekleri](sample-scripts-azure-cli.md)

## <a name="adjust-performance-and-scale-without-downtime"></a>Kesinti olmadan performansı ayarlama ve ölçeklendirme
MySQL hizmeti için Azure veritabanı iki hizmet katmanları sunar: temel ve standart. Her katman farklı performans ve ağır veritabanı iş yükleri için basit desteklemek için özellikleri sunar. İlk uygulamanızı küçük bir veritabanı üzerinde için birkaç dolar bir ay sonra hizmet katmanı ölçek çözümünüzün kapalı kalma süresi olmadan gereksinimleri olan değişiklik oluşturabilirsiniz. Kaynak gereksinimleri hızla değişen şeffaf bir şekilde yanıt vermesi veritabanınızı dinamik ölçeklenebilirlik sağlar. Yalnızca gereksinim duyduğunuzda, ihtiyacınız olan kaynakları için ödeme yaparsınız.

## <a name="monitoring-and-alerting"></a>İzleme ve uyarı
Performansı yükseltmeye veya düşürmeye karar vereceğiniz doğru zamanı nasıl belirlersiniz? Yerleşik performans izleme ve uyarı özellikleri, işlem birimini temel alan performans değerlendirmeleri birlikte kullanın. Bu özellikleri kullanarak, yukarı veya aşağı geçerli göre ölçeklendirme etkisini hızla değerlendirebilirsiniz veya proje performans gereksinimlerine. Bkz: [Kavramları: hizmet katmanları](concepts-service-tiers.md) Ayrıntılar için.

## <a name="keep-your-app-and-business-running"></a>Uygulamanızın ve işinizin hiç kesintiye uğramamasını sağlayın
Azure'nın endüstri lideri genel bir veri merkezleri, Microsoft tarafından yönetilen ağ tarafından desteklenen % 99,99 kullanılabilirlik hizmet düzeyi sözleşmesi (SLA), uygulamanızın 7/24 çalıştıran tutmaya yardımcı olur. MySQL sunucusu için her Azure veritabanı ile yerleşik güvenlik, hata toleransı ve satın alma veya tasarlama, derleme ve yönetmek için Aksi durumda olması gereken veri koruma yararlanın. MySQL için Azure veritabanı ile bir sunucu a 35 gün kadar daha önceki bir duruma kurtarmak için zaman içinde nokta geri yükleme kullanabilirsiniz.

## <a name="secure-your-data"></a>Verilerinizin güvenliğini sağlama
Azure veritabanı hizmetleri gelenek veri güvenliği Azure veritabanı için MySQL erişimi sınırlamak, çalışmıyorken veri ve hareket halinde korumak ve etkinlikleri izlemenize yardımcı özelliklerle anlayışına sahiptir. Ziyaret [Azure Güven Merkezi](https://www.microsoft.com/en-us/TrustCenter/Security/default.aspx) Azure'nın platform güvenliği hakkında bilgi için.

MySQL hizmeti için Azure veritabanına veri çalışmıyorken için depolama şifrelemesi kullanır. Veri yedekleri, dahil olmak üzere (hariç sorgu çalıştırılırken altyapısı tarafından oluşturulan geçici dosyalar) diskte şifrelenir. Azure depolama şifreleme dahil AES 256 bit şifreleme hizmeti kullanıyor ve anahtarları sistem tarafından yönetiliyor. Depolama şifreleme her zaman açıktır ve devre dışı bırakılamaz.

Varsayılan olarak, Azure veritabanı için MySQL hizmeti gerektirecek şekilde yapılandırılmış [SSL bağlantı güvenliği](./concepts-ssl-connection-security.md) veri hareket halinde ağ üzerinden için. Veritabanı sunucunuz ve istemci uygulamalarınız arasında SSL bağlantılarını zorlamayı "ortadaki adam" saldırılarına karşı uygulamanız ile sunucu arasındaki veri akışını şifreleyerek korunmasına yardımcı.  İsteğe bağlı olarak, istemci uygulamanız SSL bağlantısını desteklemiyorsa, veritabanı hizmete bağlanmak için SSL gerektirme devre dışı bırakabilirsiniz.

## <a name="next-steps"></a>Sonraki Adımlar
Azure veritabanı giriş MySQL için okuma ve sorusunu yanıtladığınıza göre "Azure veritabanı için MySQL nedir?", yapmaya hazırsınız:
- Maliyet karşılaştırmaları ve hesaplayıcıları için fiyatlandırma sayfasını bakın. [Fiyatlandırma](https://azure.microsoft.com/pricing/details/mysql/)
- İlk sunucunuzun oluşturarak başlayın. [Azure portalını kullanarak MySQL için Azure Veritabanı sunucusu oluşturma](quickstart-create-mysql-server-database-using-azure-portal.md)
- Python, PHP, Ruby, C kullanarak ilk uygulamanızı oluşturma\#, Java, Node.js: [MySQL için Azure veritabanına bağlanmak için kullanılan bağlantı kitaplıkları](concepts-connection-libraries.md)
