---
title: "Azure veritabanı aaaOverview PostgreSQL ilişkisel veritabanı hizmeti için | Microsoft Docs"
description: "Azure veritabanı genel bir bakış için PostgreSQL ilişkisel veritabanı hizmeti sağlar."
services: postgresql
author: kamathsun
ms.author: sukamat
manager: jhubbard
editor: jasonwhowell
ms.custom: mvc
ms.service: postgresql
ms.topic: overview
ms.date: 08/01/2017
ms.openlocfilehash: fd6821b56e5295b8b341d87b14d113f7a4b247c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-database-for-postgresql"></a>Azure veritabanı PostgreSQL için nedir?

Azure için PostgreSQL veritabanıdır hello hello topluluk açık kaynak sürümüne geliştiriciler için Microsoft bulut ilişkisel veritabanı hizmetinde [PostgreSQL](https://www.postgresql.org/) veritabanı altyapısı. Genel önizlemede hizmetidir. Azure veritabanı PostgreSQL için sunar:
- Tahmin edilebilir performans birden çok hizmet düzeyleri
- Hiçbir uygulama kapalı kalma süresi ile dinamik ölçeklenebilirlik
- Yerleşik yüksek kullanılabilirlik
- Veri koruma

Bu özellikler neredeyse hiçbir yönetim gerektirir ve tüm hiçbir ek ücret sağlanır. Bu özellikler, hızlı uygulama geliştirme ve zaman toomarket hızlandırmaya, yerine çok değerli bir zaman ve kaynak toomanaging sanal makineleri ve altyapıyı ayırma toofocus izin verir. Ayrıca, hello uygulamanızla kaynak araçları ve seçtiğiniz platform açın ve hello hızı ve toolearn yeni yetenekler gerek kalmadan işinizin talep verimliliği ile teslim toodevelop devam edebilirsiniz. 

Bu makalede PostgreSQL temel kavramlarını ve özelliklerini ilgili tooperformance, ölçeklenebilirlik ve yönetilebilirlik için giriş tooAzure veritabanı değil. Bu hızlı başlattığınız tooget başlatır bakın:

- [Azure portalını kullanarak PostgreSQL için bir Azure veritabanı oluşturma](quickstart-create-server-database-portal.md)
- [Hello Azure CLI kullanarak PostgreSQL için bir Azure veritabanı oluşturma](quickstart-create-server-database-azure-cli.md)

Azure CLI ve PowerShell örnekleri için bkz.:

- [Azure veritabanı PostgreSQL için Azure CLI örnekleri](./sample-scripts-azure-cli.md)

## <a name="adjust-performance-and-scale-without-downtime"></a>Kesinti olmadan performansı ayarlama ve ölçeklendirme

Azure veritabanı PostgreSQL hizmet için şu anda iki hizmet katmanları sunar: temel ve standart. Her hizmet katmanı sunuyor [performans, IOPS garanti ve yetenekleri farklı düzeylerde](concepts-service-tiers.md) toosupport basit tooheavyweight veritabanı iş yükleri. Ayda birkaç liraya küçük bir sunucu üzerinde ilk uygulamanızı oluşturabilir ve ardından [hello performans düzeyini değiştirmek](scripts/sample-scale-server-up-or-down.md) hizmet içinde hiçbir zaman toomeet hello ihtiyaçlarını çözümünüzü el ile veya programlama katmanı. Kapalı kalma süresi tooyour uygulama veya tooyour müşteriler bunu yapabilirsiniz. Veritabanı tootransparently yanıt kaynak gereksinimlerini ve etkinleştirir, tooonly gereksinim duyduğunuzda ihtiyacınız hello kaynaklar için ödeme değiştirme toorapidly dinamik ölçeklenebilirlik sağlar.

## <a name="monitoring-and-alerting"></a>İzleme ve uyarı
Nasıl karar ne zaman yukarı ve aşağı toodial? Merhaba yerleşik performans izleme ve işlem birimleri temel hello performans değerlendirmeleri birlikte özellikleri, uyarı kullanın. İşlem birimleri ölçeklendirmeyi hello etkisi hızlı bir şekilde değerlendirmek bu Araçları'nı kullanarak veya aşağı geçerli veya tahmini performans gereksinimlerinize göre. Ayrıntılar için bkz [Azure veritabanı PostgreSQL seçenekleri ve performans: her hizmet katmanında nelerin kullanılabildiğini anlama](./concepts-service-tiers.md).

## <a name="keep-your-app-and-business-running"></a>Uygulamanızın ve işinizin hiç kesintiye uğramamasını sağlayın
Azure'nın endüstri lideri genel bir veri merkezleri, Microsoft tarafından yönetilen ağ tarafından desteklenen % 99,99 kullanılabilirlik (Önizleme'de kullanılamaz) hizmet düzeyi sözleşmesi (SLA), uygulamanızın 7/24 çalıştıran tutmaya yardımcı olur. Her Azure veritabanı ile PostgreSQL sunucu için yerleşik güvenlik, hata toleransı ve oluşturmak ve yönetmek toobuy veya tasarımı, aksi takdirde olması gereken veri koruma yararlanın. PostgreSQL Azure veritabanıyla, her bir hizmet katmanına iş sürekliliği özellikleri ve yukarı tooget kullanabileceğiniz seçenekleri ve çalıştığından ve Kal kapsamlı bir kümesini sunar. Kullanabileceğiniz [zaman içinde nokta geri yükleme](howto-restore-server-portal.md) tooreturn veritabanı tooan önceki durumunda, a kadar 35 gün. Ayrıca, veritabanlarınızı barındıran hello veri merkezinde bir kesinti oluşursa, son yedeklemelerini coğrafi olarak yedekli kopyalarından veritabanlarını geri yükleyebilirsiniz.

## <a name="secure-your-data"></a>Verilerinizin güvenliğini sağlama
Azure veritabanı hizmetleri gelenek veri güvenliği PostgreSQL için Azure veritabanına erişimi sınırlamak, çalışmıyorken veri ve hareket halinde korumak ve etkinlikleri izlemenize yardımcı özelliklerle anlayışına sahiptir. Merhaba ziyaret [Azure Güven Merkezi](https://www.microsoft.com/TrustCenter/Security/default.aspx) Azure'nın platform güvenliği hakkında bilgi için.

Hello Azure veritabanı PostgreSQL hizmeti için veri çalışmıyorken için depolama şifrelemesi kullanır. (Sorgu çalıştırılırken hello altyapısı tarafından oluşturulan geçici dosyalar hello durumla) diskteki yedeklemeler de dahil olmak üzere veri şifrelenir. Azure depolama şifreleme dahil AES 256 bit şifreleme Hello hizmet kullanıyor ve hello anahtarları sistem tarafından yönetiliyor. Depolama şifreleme her zaman açıktır ve devre dışı bırakılamaz.

Varsayılan olarak, PostgreSQL hizmeti yapılandırılmış toorequire için Azure veritabanı hello [SSL bağlantı güvenliği](./concepts-ssl-connection-security.md) veri hareket halinde hello ağ üzerinden için. Veritabanı sunucunuz ve istemci uygulamalarınız arasında SSL bağlantılarını zorlamayı "Merhaba ortadaki adam" saldırılarına karşı hello veri akışı hello sunucusu ve uygulamanız arasındaki şifreleyerek korunmasına yardımcı.  İsteğe bağlı olarak, istemci uygulamanız SSL bağlantısını desteklemiyorsa tooyour veritabanı hizmeti bağlanmak için SSL gerektirme devre dışı bırakabilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar
- Merhaba bkz [fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/postgresql/) maliyet karşılaştırmaları ve hesaplayıcıları için.
- İle çalışmaya başlama [PostgreSQL için ilk Azure veritabanınızı oluşturmaya](./quickstart-create-server-database-portal.md).
- Python, PHP, Ruby, C kullanarak ilk uygulamanızı oluşturma\#, Java, Node.js: [bağlantı kitaplıkları](./concepts-connection-libraries.md)
