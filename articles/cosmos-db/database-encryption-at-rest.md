---
title: "Bekleyen veritabanı şifreleme: Azure Cosmos DB | Microsoft Docs"
description: "Varsayılan şifreleme tüm verileri Azure Cosmos DB nasıl sağladığını öğrenin."
services: cosmos-db
author: voellm
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 99725c52-d7ca-4bfa-888b-19b1569754d3
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: voellm
ms.openlocfilehash: d52d55fe45fdd18394166ec7ccd6e46e8f8f434b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-database-encryption-at-rest"></a>Bekleyen Azure Cosmos DB veritabanı şifreleme

Bekleyen şifreleme gibi katı hal sürücüleri (SSD) başvuran sık toohello şifreleme kalıcı depolama cihazlarda verilerinin bir deyimi ve sabit disk sürücülerinin (HDD'ler) ' dir. Cosmos DB birincil veritabanlarını Ssd'de depolar. Medya ekler ve yedeklemeleri genellikle HDD tarafından yedeklenir Azure Blob Depolama alanında depolanır. Cosmos DB için bekleyen şifreleme Hello sürümle birlikte, tüm veritabanları, medya ekler ve yedeklemeleri şifrelenir. Verilerinizi şimdi (Merhaba ağ üzerinden) aktarım sırasında şifrelenir ve rest (kalıcı depolama) uçtan uca şifreleme sağlar.

Cosmos DB bir PaaS hizmeti çok kolay toouse olarak. Cosmos DB içinde depolanan tüm kullanıcı verileri hem beklerken hem de Aktarım şifreli olduğundan tootake herhangi bir eylem yok. Başka bir şekilde tooput budur şifrelemenin rest olan varsayılan olarak "açık". Hiçbir denetimleri tooturn vardır, dışı. Bu özellik toomeet devam ederken sağladığımız bizim [kullanılabilirliğini ve performansını SLA](https://azure.microsoft.com/support/legal/sla/cosmos-db).

## <a name="implement-encryption-at-rest"></a>Bekleyen şifreleme uygulama

Bekleyen şifreleme, güvenli anahtar depolama sistemleri, şifrelenmiş ağlar ve şifreleme API'leri dahil güvenlik teknolojileri çeşitli kullanılarak uygulanır. Verileri işlemek ve şifresini çözmek sistemleri anahtarları Yönet sistemleriyle toocommunicate sahip. şifrelenmiş verileri ve hello Yönetimi anahtarların depolanmasını nasıl ayrılmış Hello diyagramını gösterir. 

![Tasarım diyagramı](./media/database-encryption-at-rest/design-diagram.png)

bir kullanıcı isteğin Hello temel akışı aşağıdaki gibidir:
- Merhaba kullanıcı veritabanı hesabı hazır yapıldığında ve depolama anahtarları isteği toohello yönetim hizmeti kaynak sağlayıcısı alınır.
- Bir kullanıcı, HTTPS ve güvenli aktarım aracılığıyla bağlantı tooCosmos DB oluşturur. (Merhaba SDK'ları soyut hello ayrıntıları.)
- Merhaba kullanıcı güvenli bağlantı daha önce oluşturduğunuz hello üzerinde depolanan bir JSON belgesi toobe gönderir.
- Merhaba kullanıcı dizin oluşturmayı devre dışı kapamış olduğu sürece hello JSON belgesi dizine alınır.
- Merhaba JSON belgesi ve dizin verileri toosecure depolama yazılır.
- Düzenli aralıklarla veri hello güvenli depolama alanından okuyun ve Azure şifreli Blob deposu toohello yedeklenir.

## <a name="frequently-asked-questions"></a>Sık sorulan sorular

### <a name="q-how-much-more-does-azure-storage-cost-if-storage-service-encryption-is-enabled"></a>S: depolama hizmeti şifrelemesi etkinse, daha fazlasını nasıl Azure depolama maliyeti?
Y: yoktur ek ücret ödemeden.

### <a name="q-who-manages-hello-encryption-keys"></a>S: hello şifreleme anahtarları yöneten?
Y: hello anahtarları Microsoft tarafından yönetilir.

### <a name="q-how-often-are-encryption-keys-rotated"></a>S: ne sıklıkta şifreleme anahtarları döndürülüp?
Y: Microsoft Cosmos DB izleyen şifreleme anahtar döndürme için iç Kılavuzlar kümesi vardır. Merhaba özel yönergeleri yayımlanmaz. Microsoft yayımlama hello [güvenlik geliştirme yaşam döngüsü (SDL)](https://www.microsoft.com/sdl/default.aspx), bir iç Kılavuzu alt görülen ve geliştiriciler için kullanışlı en iyi yöntemler vardır.

### <a name="q-can-i-use-my-own-encryption-keys"></a>S: kendi şifreleme anahtarları kullanmak?
A: biz sabit tookeep hello hizmeti kolay toouse çalışılan ve cosmos DB bir PaaS hizmetidir. Bu soru genellikle PCI-DSS gibi bir uyumluluk gereksinimini karşılamak için bir proxy soru olarak sorulan fark ettim. Bu özellik oluşturmanın bir parçası olarak, biz Cosmos DB kullanan müşteriler hello gerek toomanage anahtarları kendilerini olmadan kendi gereksinimlerini karşıladığını uyumluluk denetçiler tooensure çalışmıştır.
Sonuç olarak, şu anda kullanıcıların hello seçeneği tooburden kendilerini anahtar yönetimi ile sunuyoruz değil.

### <a name="q-what-regions-have-encryption-turned-on"></a>S: ne bölgeleri açık şifreleme var mı?
Y: tüm Azure Cosmos DB bölgeler için tüm kullanıcı verilerini açık şifreleme vardır.

### <a name="q-does-encryption-affect-hello-performance-latency-and-throughput-slas"></a>S: şifreleme hello performans gecikme süresi ve verimlilik SLA'ları etkiler?
Y: yoktur hiçbir etkisi veya değişiklikleri toohello performans SLA göre bekleyen şifreleme tüm mevcut ve yeni hesapları için etkinleştirildi. Daha fazla bilgiyi hello üzerinde [Cosmos DB SLA](https://azure.microsoft.com/support/legal/sla/cosmos-db) sayfasında toosee hello son garantiler.

### <a name="q-does-hello-local-emulator-support-encryption-at-rest"></a>S: Merhaba yerel öykünücüsü bekleyen şifreleme destekliyor mu?
Y: hello öykünücüsü bir tek başına geliştirme ve test aracıdır ve yönetilen Cosmos DB hizmeti kullanan hello hello anahtar yönetimi hizmetlerini kullanmaz. Bizim önerimiz burada hassas öykünücüsü test veri depolayan sürücülerindeki BitLocker tooenable ' dir. Merhaba [öykünücüsü değişen hello varsayılan veri dizinini destekleyen](local-emulator.md) iyi bilinen bir konum kullanarak yanı sıra.

## <a name="next-steps"></a>Sonraki adımlar

Cosmos DB güvenlik ve hello en son geliştirmeleri genel bakış için bkz: [Azure Cosmos DB veritabanı güvenliği](database-security.md).
Merhaba Microsoft sertifikalar hakkında daha fazla bilgi için bkz: [Azure Güven Merkezi](https://azure.microsoft.com/en-us/support/trust-center/).
