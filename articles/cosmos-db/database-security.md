---
title: "aaaDatabase güvenliği - Azure Cosmos DB | Microsoft Docs"
description: "Azure Cosmos DB verileriniz için veritabanı koruma ve veri güvenliği nasıl sağladığını öğrenin."
keywords: "nosql veritabanı güvenlik, bilgi güvenliği, veri güvenliği, veritabanı şifreleme, veritabanı koruma, güvenlik ilkeleri, güvenlik test etme"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: a02a6a82-3baf-405c-9355-7a00aaa1a816
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: mimig
ms.openlocfilehash: 85ffa62f611bfad00bf3fc5dbe536f91f97f1113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-database-security"></a>Azure Cosmos DB veritabanı güvenliği

Bu makalede ele en iyi güvenlik uygulamalarını, veritabanı ve temel özellikleri engellemenize, algılamanıza ve toodatabase ihlallerini yanıt Azure Cosmos DB toohelp tarafından sunulan.
 
## <a name="whats-new-in-azure-cosmos-db-security"></a>Yeni Azure Cosmos DB güvenlik nedir?

Bekleyen şifreleme belgeler ve Azure Cosmos DB tüm Azure bölgeleri içinde depolanan yedeklemeler için kullanıma sunulmuştur. Bekleyen şifreleme Bu bölgeler hem yeni hem de mevcut müşteriler için otomatik olarak uygulanır. Olduğundan hiç gerek tooconfigure herhangi bir şey; elde hello aynı harika gecikme, işleme, kullanılabilirlik ve işlevsellik önce bilmesinin hello avantajı ile verilerinizi bekleyen şifreleme ile güvenli olarak.

## <a name="how-do-i-secure-my-database"></a>Veritabanım güvenliğini nasıl sağlayabilirim? 

Veri güvenliği, hello müşteri ve veritabanı sağlayıcınız arasında paylaşılan bir sorumluluğundadır. Seçtiğiniz hello veritabanı sağlayıcısı bağlı olarak, yapmanız sorumluluk hello miktarını farklılık gösterebilir. Bir şirket içi çözüm seçerseniz, tooprovide her şeyi uç nokta koruma toophysical güvenlik kolay görev olan donanım - gerekir. Bir PaaS bulut veritabanı sağlayıcısı Azure Cosmos DB gibi seçerseniz, bölgenizdeki sorun önemli ölçüde küçültür. Merhaba aşağıdaki görüntü, Microsoft'un Web sitesinden ödünç [bulut bilgi işlemin paylaşılan sorumlulukları](https://aka.ms/sharedresponsibility) teknik incelemesi gösterir nasıl Azure Cosmos DB gibi bir PaaS sağlayıcısı ile sizin sorumluluğunuzdadır azaltır.

![Müşteri ve veritabanı sağlayıcısı sorumlulukları](./media/database-security/nosql-database-security-responsibilities.png)

Yukarıdaki diyagramda gösterir üst düzey bulut güvenlik bileşenleri Merhaba, ancak hangi öğeleri özellikle veritabanı çözümünüz için hakkında tooworry gerekiyor mu? Ve diğer çözümleri tooeach nasıl karşılaştırabilirsiniz? 

Hangi toocompare veritabanı sistemlerinde gereksinimleri listesi aşağıdaki hello öneririz:

- Ağ güvenliği ve güvenlik duvarı ayarları
- Kullanıcı kimlik doğrulaması ve hassas kullanıcı denetimleri
- Bölgesel arızalara için genel özelliği tooreplicate verileri
- Bir veri alanından özelliği tooperform yerine tooanother Merkezi
- Bir veri merkezi içinde yerel veri çoğaltma
- Otomatik veri yedeklemeleri
- Silinen veri yedeklerden geri yükleme
- Koruma ve hassas verileri yalıtma
- Saldırıları için izleme
- Tooattacks yanıt
- Özelliği toogeo dilimi veri tooadhere toodata idare sınırlamaları
- Korumalı veri merkezlerinde sunucuların fiziksel koruma

Ve onu gibi görünse de belirgin, son [büyük ölçekli veritabanı ihlallerini](http://thehackernews.com/2017/01/mongodb-database-security.html) bize hello basit ancak kritik önemi gereksinimlerine Merhaba hatırlat:
- Toodate tutulur düzeltme sunucuları
- HTTPS varsayılan/SSL şifrelemesi
- Güçlü parolalar ile yönetici hesapları

## <a name="how-does-azure-cosmos-db-secure-my-database"></a>Azure Cosmos DB Veritabanım güvenliğini nasıl?

Geri listesi önceki hello bakalım - bu güvenlik gereksinimleri kaç Azure Cosmos DB sağlar mı? Tek tek her.

Her birini ayrıntılı içine şimdi edinebilirsiniz.

|Güvenlik gereksinimi|Azure Cosmos DB'ın güvenlik yaklaşımı|
|---|---|---|
|Ağ güvenliği|Bir IP Güvenlik Duvarı'nı kullanarak olduğu hello koruma toosecure ilk katmanını veritabanınızı. Azure Cosmos DB gelen güvenlik duvarı desteği için IP tabanlı erişim denetimlerini güdümlü İlkesi destekler. Merhaba IP tabanlı erişim denetimlerini için geleneksel veritabanı sistemleri tarafından kullanılan benzer toohello güvenlik duvarı kuralları olsa da, böylece Azure Cosmos DB veritabanı hesabı yalnızca onaylanan bir makine veya Bulut Hizmetleri kümesinden erişilebilir genişletilir. <br><br>Azure Cosmos DB, belirli bir IP adresi (168.61.48.0), bir IP aralığı (168.61.48.0/8) ve IP aralıkları ve birleşimler, tooenable sağlar. <br><br>Bu izin verilenler dışında makinelerden kaynaklanan tüm istekler Azure Cosmos DB tarafından engellendi. Gelen istekleri makineler onaylanmış ve bulut Hizmetleri sonra erişim denetimi toohello kaynakları verilen hello kimlik doğrulama işlemi toobe tamamlamanız gerekir.<br><br>Daha fazla bilgi edinin [Azure Cosmos DB Güvenlik Duvarı](firewall-support.md).|
|Yetkilendirme|Azure Cosmos DB yetkilendirme için karma tabanlı ileti kimlik doğrulama kodu (HMAC) kullanır. <br><br>Her istek hello gizli hesap anahtarı kullanarak karma uygulanır ve hello sonraki base-64 kodlanmış karma her çağrı tooAzure Cosmos DB gönderilir. toovalidate hello isteği, doğru gizli anahtar ve Özellikler toogenerate karma hello Azure Cosmos DB hizmeti kullanan hello sonra hello isteğindeki hello hello değerle karşılaştırır. Merhaba iki değerleriyle eşleşen, hello işlemi başarıyla yetkili ve hello istek işlenir, aksi takdirde bir Yetkilendirme hatası yoktur ve hello isteğini reddetti.<br><br>Kullanabilirsiniz bir [ana anahtar](secure-access-to-data.md#master-keys), veya bir [kaynak belirteci](secure-access-to-data.md#resource-tokens) bir belge gibi ayrıntılı erişim tooa kaynak izin verme.<br><br>Daha fazla bilgi edinin [erişim tooAzure Cosmos DB kaynakların güvenliğini sağlama](secure-access-to-data.md).|
|Kullanıcılar ve izinler|Hello kullanarak [ana anahtar](#master-key) hello hesabı için kullanıcı ve veritabanı başına izin kaynaklarının oluşturabilirsiniz. A [kaynak belirteci](#resource-token) bir veritabanında bir izinle ilişkili olan ve hello kullanıcı erişimi olup olmadığını belirler (okuma-yazma, salt okunur veya erişimi yok) hello veritabanındaki tooan Uygulama kaynağı. Uygulama kaynaklarını koleksiyonlar, belgeler, ekleri, saklı yordamlar, tetikleyiciler ve UDF'ler içerir. Merhaba kaynak belirteci daha sonra kimlik doğrulama tooprovide sırasında kullanılan ya da erişim toohello kaynak reddet.<br><br>Daha fazla bilgi edinin [erişim tooAzure Cosmos DB kaynakların güvenliğini sağlama](secure-access-to-data.md).|
|Active directory ile tümleştirme (RBAC)| Ayrıca, bu tablonun hello ekran görüntüsünde gösterildiği gibi hello Azure portalına erişim denetimi (IAM) kullanarak erişim toohello veritabanı hesabı sağlayabilir. IAM rol tabanlı erişim denetimi sağlar ve Active Directory ile tümleştirir. Kişiler ve hello görüntü aşağıdaki gösterildiği gibi grupları için yerleşik roller veya özel roller kullanabilirsiniz.|
|Genel çoğaltma|Azure Cosmos DB tooreplicate sağlayan anahtar teslimi genel dağıtım hello olan Azure'nın dünya çapında veri merkezlerini birini tıklatın bir düğme, veri tooany sunar. Genel çoğaltma küresel olarak ölçeklendirmeyi ve düşük gecikmeli erişim tooyour veri Merhaba Dünya sağlamanıza olanak tanır.<br><br>Güvenlik Hello bağlamında, bölgesel arızalara karşı veri koruma genel çoğaltma oluşturmasını sağlar.<br><br>Daha fazla bilgi edinin [verilerini genel dağıtmak](distribute-data-globally.md).|
|Bölgesel yük devretme|Verilerinizi birden fazla veri merkezinde çoğaltıldığından, Azure Cosmos DB bölgesel veri merkezi çevrimdışı duruma işlemlerinizin otomatik olarak yapar. Verilerinizi çoğaltılan hello bölgeleri kullanarak yük devretme bölge öncelikli listesi oluşturabilirsiniz. <br><br>Daha fazla bilgi edinin [bölgesel yük devretme işlemlerini Azure Cosmos veritabanı](regional-failover.md).|
|Yerel çoğaltma|Hatta içinde tek bir veri merkezi, Azure Cosmos DB otomatik olarak yüksek kullanılabilirlik seçeneği hello verme verilerini çoğaltır. [tutarlılık düzeylerini](consistency-levels.md). Bu garanti bir [% 99,99 açık kalma süresi kullanılabilirlik SLA](https://azure.microsoft.com/support/legal/sla/cosmos-db) ve bir finansal Garantisi ile - başka bir veritabanı hizmet sağlayabilir bir şey sunar.|
|Çevrimiçi yedeklemeleri otomatik|Azure Cosmos DB veritabanları düzenli olarak yedeklenen ve georedundant deposunda depolanır. <br><br>Daha fazla bilgi edinin [otomatik çevrimiçi yedekleme ve geri yükleme Azure Cosmos DB ile](online-backup-and-restore.md).|
|Silinmiş verileri geri yüklemek|Merhaba otomatik çevrimiçi yedeklemeler, yanlışlıkla silinmiş yukarı çok kullanılan toorecover veriler olabilir ~ hello olayından sonra 30 gün. <br><br>Daha fazla bilgi edinin [otomatik çevrimiçi yedekleme ve geri yükleme ile Azure Cosmos DB](online-backup-and-restore.md)|
|Koruma ve hassas verileri yalıtma|Merhaba bölgelerde listelenen tüm verileri [yenilikler nelerdir?](#whats-new) şimdi bekleme sırasında şifrelenir.<br><br>PII ve diğer gizli veriler yalıtılmış toospecific koleksiyonları ve okuma-yazma olabilir veya salt okunur erişim sınırlı toospecific kullanıcılar olabilir.|
|İzleme saldırıları için|Denetim günlüğü ve etkinlik günlükleri kullanarak hesabınızı normal ve anormal etkinliğinin izleyebilirsiniz. Hangi işlemlerin hello işlemi oluştuğunda, hello durumu hello işleminin ve çok daha gösterildiği gibi bu tablodan sonraki hello ekran kimin hello işlemini başlattı kaynaklarınızı gerçekleştirilen görüntüleyebilirsiniz.|
|Tooattacks yanıt|Azure destek tooreport olası bir saldırı temas sonra 5-adım olay yanıtlama süreci başlayacağı zamana devre dışı. Merhaba hello 5 adımlı işlem toorestore normal hizmet güvenliği ve işlemleri mümkün olan en kısa sürede bir sorun algıladı ve bir araştırma başlatıldıktan sonra hedefidir.<br><br>Daha fazla bilgi edinin [Microsoft Azure güvenlik hello bulut yanıtta](https://aka.ms/securityresponsepaper).|
|Coğrafi yalıtma|Veri Yönetimi ve uyumluluk sovereign bölgeler (örneğin, Almanya, Çin, BİZE kamu) için Azure Cosmos DB sağlar.|
|Korumalı özellikleri|Veriler Azure Cosmos veritabanı Azure'nın korumalı veri merkezlerinde SSD depolanır.<br><br>Daha fazla bilgi edinin [Microsoft küresel veri merkezleri](https://www.microsoft.com/en-us/cloud-platform/global-datacenters)|
|HTTPS/SSL/TLS şifrelemesi|Tüm istemci hizmeti Azure Cosmos DB etkileşimler SSL/TLS 1.2 zorlanan ' dir. Ayrıca, tüm içi veri merkezi ve çapraz veri merkezine çoğaltma SSL/TLS 1.2 zorlanan vardır.|
|Bekleme sırasında şifreleme|Bekleyen Azure Cosmos Veritabanına depolanan tüm veriler şifrelenir. Daha fazla bilgi edinin [bekleyen Azure Cosmos DB şifreleme](.\database-encryption-at-rest.md)|
|Düzeltme eki sunucuları|Yönetilen bir veritabanı olarak sizin için otomatik olarak yapılır hello gerek toomanage ve düzeltme eki sunucular, Azure Cosmos DB ortadan kaldırır.|
|Güçlü parolalar ile yönetici hesapları|Biz bile, sabit toobelieve bu gereksinim toomention gerekir, ancak bizim rakiplere bazıları imkansız toohave bir yönetici hesabı parolası Azure Cosmos veritabanı olduğu.<br><br> SSL ve HMAC gizli tabanlı kimlik doğrulaması aracılığıyla güvenlik varsayılan olarak mı baked.|
|Güvenlik ve veri koruma sertifikaları|Azure Cosmos DB sahip [ISO 27001](https://www.microsoft.com/en-us/TrustCenter/Compliance/ISO-IEC-27001), [Avrupa modeli yan tümceleri (EUMC)](https://www.microsoft.com/en-us/TrustCenter/Compliance/EU-Model-Clauses), ve [HIPAA](https://www.microsoft.com/en-us/TrustCenter/Compliance/HIPAA) sertifikalar. Ek sertifikalar sürüyor.|

Merhaba aşağıdaki ekran görüntüsü erişim denetimi (IAM) kullanarak Active directory tümleştirme (RBAC) hello Azure portal gösterir: ![hello Azure portal - gösterilmesi veritabanı güvenlik erişim denetimi (IAM)](./media/database-security/nosql-database-security-identity-access-management-iam-rbac.png)

Merhaba aşağıdaki ekran görüntüsü denetim günlüğü nasıl kullanabileceğinizi gösterir ve etkinlik günlüklerini toomonitor hesabınızı: ![etkinlik günlükleri için Azure Cosmos DB](./media/database-security/nosql-database-security-application-logging.png)

## <a name="next-steps"></a>Sonraki adımlar

Ana anahtarları ve kaynak belirteçleri hakkında daha fazla ayrıntı için [güvenliğini sağlama erişim tooAzure Cosmos DB veri](secure-access-to-data.md).

Microsoft sertifikalar hakkında daha fazla ayrıntı için bkz: [Azure Güven Merkezi](https://azure.microsoft.com/support/trust-center/).
