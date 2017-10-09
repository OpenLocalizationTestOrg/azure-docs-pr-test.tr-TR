---
title: "Güvenlik Merkezi ve Azure SQL veritabanı hizmetinin aaaAzure | Microsoft Docs"
description: "Bu makalede, Güvenlik Merkezi, Azure SQL veritabanı veritabanlarında güvenli nasıl yardımcı olabileceğini gösterir."
services: sql-database
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: f109adfd-daed-4257-9692-2042a1399480
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 173590500f0ce64140f214ada24b9692e01dbd4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-and-azure-sql-database-service"></a>Azure Güvenlik Merkezi ve Azure SQL veritabanı hizmeti
[Azure Güvenlik Merkezi](https://azure.microsoft.com/documentation/services/security-center/) engellemenize, algılamanıza ve toothreats yanıt yardımcı olur. Aboneliklerinizde, tümleşik güvenlik izleme ve ilke yönetimi sağlar; normal koşullarda gözden kaçabilecek tehditleri algılamaya yardımcı olur ve güvenlik çözümlerinin geniş ekosistemiyle çalışır.

Bu makalede, Güvenlik Merkezi, Azure SQL veritabanı veritabanlarında güvenli nasıl yardımcı olabileceğini gösterir.

## <a name="why-use-security-center"></a>Güvenlik Merkezi neden kullanılır?
Güvenlik Merkezi, tüm sunucular ve veritabanları hello güvenliğini görünürlük sağlayarak SQL veritabanındaki verileri korumaya yardımcı olur. Güvenlik Merkezi ile şunları yapabilirsiniz:

* SQL veritabanı şifreleme ve denetim ilkeleri tanımlar.
* SQL Database kaynaklarının Hello güvenlik tüm aboneliklerinizi izleyin.
* Hızlı bir şekilde tanımlamak ve güvenlik sorunları düzeltin.
* Gelen uyarılar tümleştirmek [Azure SQL veritabanı tehdit algılama](../sql-database/sql-database-threat-detection.md).

Ayrıca toohelping SQL veritabanı kaynaklarınızı korumak, Güvenlik Merkezi güvenlik izleme ve yönetim Azure sanal makineler, bulut Hizmetleri, uygulama hizmetleri, sanal ağlar ve daha fazlası için de sağlar. Güvenlik Merkezi hakkında daha fazla bilgi [burada](security-center-intro.md).

## <a name="prerequisites"></a>Ön koşullar
Güvenlik Merkezi ile çalışmaya tooget abonelik tooMicrosoft Azure olması gerekir. Merhaba ücretsiz katmanı Güvenlik Merkezi, aboneliğiniz ile etkinleştirilir. Güvenlik Merkezi'nin ücretsiz ve standart katmanları hakkında daha fazla bilgi için bkz: [Güvenlik Merkezi fiyatlandırma](https://azure.microsoft.com/pricing/details/security-center/).

Güvenlik Merkezi, rol tabanlı erişim destekler. Azure, rol tabanlı erişim denetimi (RBAC) hakkında daha fazla toolearn bkz [Azure Active Directory rol tabanlı erişim denetimi](../active-directory/role-based-access-control-configure.md). Merhaba Güvenlik Merkezi ile ilgili SSS hakkında bilgi verilmektedir [izinleri Güvenlik Merkezi'nde işlenme](security-center-faq.md#permissions).

## <a name="access-security-center"></a>Güvenlik Merkezi'ne erişme
Merhaba Güvenlik Merkezi erişim [Azure portal](https://azure.microsoft.com/features/azure-portal/). [Toohello Portalı'nda oturum](https://portal.azure.com/) ve select hello **Güvenlik Merkezi seçeneği**.

![Güvenlik Merkezi seçeneği][1]

Merhaba **Güvenlik Merkezi** dikey pencere açılır.
![Güvenlik Merkezi dikey penceresi][2]

## <a name="set-security-policy"></a>Güvenlik ilkesi ayarlama
Bir güvenlik ilkesi hello hello belirtilen abonelik veya kaynak grubu içindeki kaynaklar için önerilen denetimleri kümesini tanımlar. Güvenlik Merkezi'nde abonelik veya kaynak grupları tooyour şirketin güvenlik gereksinimlerini ve uygulamaların hello türü veya hello her Abonelikteki verilerin duyarlılığına göre ilkeleri tanımlarsınız.

Öneriler SQL denetimi ve SQL saydam veri şifreleme (TDE) için bir ilke tooshow ayarlayabilirsiniz.

* Ne zaman açmanız **SQL denetim ve tehdit algılama**, Güvenlik Merkezi erişim tooAzure veritabanı denetim uyumluluk, Gelişmiş algılama ve araştırma amacıyla etkinleştirilmesini önerir.
* Ne zaman açmanız **SQL saydam veri şifrelemesi**, Güvenlik Merkezi önerir bekleyen şifrelemenin Azure SQL veritabanınızı, ilişkili yedeklemelerinizi ve işlem günlüğü dosyalarını etkin olmalıdır.

tooset bir güvenlik ilkesi seçin hello **İlkesi** döşeme hello Güvenlik Merkezi dikey penceresinde. Merhaba üzerinde **Güvenlik İlkesi** dikey penceresinde, tooenable hello güvenlik ilkesi istediğiniz select hello abonelik. Seçin **önleme İlkesi** ve **üzerinde** hello toouse bu abonelikte istediğiniz güvenlik önerilerini.
![Güvenlik ilkesi][3]

toolearn daha, fazla [güvenlik ilkelerini ayarlama](security-center-policies.md).

## <a name="manage-security-recommendation"></a>Güvenlik açısından yönetme
Güvenlik Merkezi düzenli aralıklarla hello Azure kaynaklarınızın güvenlik durumunu çözümler. Güvenlik Merkezi olası güvenlik açıklarını belirlediğinde öneriler oluşturur. Merhaba önerileri gerekli hello denetimlerini yapılandırma hello işleminde size kılavuzluk.

Bir güvenlik ilkesi ayarladıktan sonra Güvenlik Merkezi, kaynakları tooidentify olası güvenlik açıklarını hello güvenlik durumunu çözümler. Merhaba öneriler her satırın belirli bir önerinin temsil ettiği bir tablo biçiminde görüntülenir. Azure SQL veritabanı ve onu uygularsanız her hangi bir öneri mu hello kullanılabilir önerilerini anlama başvuru toohelp olarak aşağıdaki tablonun hello kullanın. Bir öneri seçerek nasıl tooimplement hello Güvenlik Merkezi'nde öneri açıklar tooan makale alır.

| Öneri | Açıklama |
| --- | --- |
| [Denetim ve tehdit algılama SQL sunucularında etkinleştir](security-center-enable-auditing-on-sql-servers.md) |SQL veritabanı sunucuları için Denetim ve tehdit algılama Aç önerir. (Yalnızca SQL veritabanı hizmeti. Sanal makinelerde çalışan Microsoft SQL Server içermez.) |
| [SQL veritabanlarında denetim ve tehdit algılama etkinleştir](security-center-enable-auditing-on-sql-databases.md) |SQL veritabanı veritabanları için Denetim ve tehdit algılama Aç önerir. (Yalnızca SQL veritabanı hizmeti. Sanal makinelerde çalışan Microsoft SQL Server içermez.) |
| [Saydam Veri Şifrelemesini Etkinleştirme](security-center-enable-transparent-data-encryption.md) |SQL veritabanları için şifrelemeyi etkinleştirmek önerir. (Yalnızca SQL veritabanı hizmeti.) |

Azure kaynaklarınızı, select hello için toosee önerileri **önerileri** döşeme hello Güvenlik Merkezi dikey penceresinde. Merhaba üzerinde **önerileri** dikey penceresinde bir öneri toosee Ayrıntılar'ı seçin. Bu örnekte, şimdi seçin **SQL sunucularında denetimi etkinleştirme ve tehdit algılama**.

![Öneriler][4]

Aşağıda, burada denetim ve tehdit algılama etkin SQL sunucuları hello Güvenlik Merkezi gösterir gösterilen. Denetim açıldıktan sonra tehdit algılama ayarları yapılandırın ve ayarları tooreceive e-posta güvenlik uyarıları. Tehdit algılama, olası güvenlik tehditlerine toohello veritabanı gösteren anormal veritabanı etkinliklerini algıladığında sizi uyarır. Merhaba uyarılar hello Güvenlik Merkezi panosunda görüntülenir.
![Denetim ve tehdit algılama][5]

Merhaba adımları [SQL veritabanı tehdit Algılama'hello Azure portal'ın](../sql-database/sql-database-threat-detection-portal.md) üzerinde tooturn ve tehdit algılama ve anormal etkinlikler algılandığında güvenlik uyarı alacak olan e-posta tooconfigure hello liste yapılandırın.

toolearn öneriler hakkında daha fazla bilgi görmek [güvenlik önerilerini yönetme](security-center-recommendations.md).

## <a name="monitor-security-health"></a>Güvenlik durumunu izleme
Etkinleştirdikten sonra [güvenlik ilkeleri](security-center-policies.md) bir aboneliğin kaynakları için Güvenlik Merkezi, kaynakları tooidentify olası güvenlik açıklarını hello güvenliğini analiz eder.  Hello hello kaynaklarınızın güvenlik durumunu görüntüleyebilirsiniz **kaynak güvenlik durumu** döşeme. Tıkladığınızda **veri** hello içinde **kaynak güvenlik durumu** , hello döşeme **veri kaynaklarını** dikey penceresi açılır ve saydam denetim gibi sorunlar için SQL önerilerle birlikte veri şifreleme etkinleştirilmemiş olması. Ayrıca, hello veritabanı hello genel sistem durumu için öneriler içerir.
![Kaynak güvenlik durumu][6]

toolearn daha, fazla [güvenlik durumunu izleme](security-center-monitoring.md).

## <a name="manage-and-respond-toosecurity-alerts"></a>Yönetme ve yanıtlama toosecurity uyarıları
Güvenlik Merkezi otomatik olarak toplar, çözümler ve tümleştirir günlük verilerini [Azure SQL tehdit algılama](../sql-database/sql-database-threat-detection.md)olarak yanı sıra diğer Azure kaynaklarına toodetect gerçek tehditleri ve hatalı pozitif sonuçları azaltmak. Öncelikli güvenlik uyarıları listesi hello birlikte Güvenlik Merkezi'nde gösterilen tooquickly gereksinim duyduğunuz bilgileri araştırın hello sorun ve nasıl için öneriler tooremediate saldırının.

toosee uyarıları, select hello **güvenlik uyarıları** döşeme hello Güvenlik Merkezi dikey penceresinde. Merhaba üzerinde **güvenlik uyarıları** dikey penceresinde, seçin, adımlar varsa ve hangi hello uyarı tetikleyen daha hello olaylar hakkında bir uyarı toolearn tootake tooremediate saldırının gerekiyor. Bu örnekte, şimdi seçin **olası SQL ekleme**.
![Güvenlik Uyarıları][7]

Aşağıda gösterildiği gibi Güvenlik Merkezi, hangi tetiklenen hello uyarı bir anlayış hello teklif ek ayrıntılar hedef kaynak, geçerli hello kaynak zaman IP adresi ve öneriler konusunda sağlar tooremediate.
![Olası SQL ekleme][8]

toolearn daha, fazla [yönetme ve yanıt toosecurity uyarıları](security-center-managing-and-responding-alerts.md).

## <a name="next-steps"></a>Sonraki adımlar
* [Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) — hello hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.
* [Güvenlik Merkezi planlama ve işlemler Kılavuzu](security-center-planning-and-operations-guide.md) - bir dizi adımları izleyin ve kuruluşunuzun güvenlik gereksinimlerine ve bulut Yönetimi modeline göre Güvenlik Merkezi kullanımınızı toooptimize görevler.
* [Güvenlik Merkezi veri güvenliği](security-center-data-security.md) – Güvenlik Merkezi nasıl topladığı öğrenin ve yapılandırma bilgileri, meta verileri, olay günlükleri, kilitlenme döküm dosyaları ve daha da dahil olmak üzere Azure kaynaklarınızı hakkındaki verileri işler.
* [Güvenlik olayları işleme](security-center-incident.md) -nasıl toouse hello güvenlik uyarısı Güvenlik Merkezi tooassist özelliği öğrenin size güvenlik olaylarını işleme.

<!--Image references-->
[1]: ./media/security-center-sql-database/security-center.png
[2]: ./media/security-center-sql-database/security-center-blade.png
[3]: ./media/security-center-sql-database/security-policy.png
[4]: ./media/security-center-sql-database/recommendation.png
[5]: ./media/security-center-sql-database/turn-on-auditing.png
[6]: ./media/security-center-sql-database/monitor-health.png
[7]: ./media/security-center-sql-database/alert.png
[8]: ./media/security-center-sql-database/sql-injection.png
