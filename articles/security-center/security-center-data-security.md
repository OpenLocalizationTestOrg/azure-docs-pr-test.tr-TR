---
title: "aaaAzure Güvenlik Merkezi veri güvenliği | Microsoft Docs"
description: "Bu belgede Azure Güvenlik Merkezi'nde verilerin yönetilmesi ve korunması açıklanmaktadır."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 33f2c9f4-21aa-4f0c-9e5e-4cd1223e39d7
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: yurid
ms.openlocfilehash: 30f8b11272dc5df6d485608abdaa62ba57e63f23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-data-security"></a>Azure Güvenlik Merkezi Veri Güvenliği
toohelp müşteriler engellemenize, algılamanıza ve toothreats yanıt, Azure Güvenlik Merkezi toplar ve yapılandırma bilgileri, meta verileri, olay günlükleri, kilitlenme döküm dosyaları ve daha da dahil olmak üzere, güvenlikle ilgili verileri işler. Microsoft aynılarını toostrict uyumluluk ve güvenlik yönergelerine — toooperating hizmet kodlama gelen.

Bu makalede Azure Güvenlik Merkezi'nde verilerin yönetilmesi ve korunması açıklanmaktadır.

>[!NOTE] 
>İçinde erken Haziran 2017'den itibaren Güvenlik Merkezi hello Microsoft İzleme Aracısı toocollect kullanmak ve verileri depolamak. Bkz: [Azure Güvenlik Merkezi platformu geçiş](security-center-platform-migration.md) toolearn daha fazla. Bu makaledeki Hello bilgiler geçiş toohello sonra Microsoft İzleme Aracısı Güvenlik Merkezi işlevlerini temsil eder.
>


## <a name="data-sources"></a>Veri kaynakları
Azure Güvenlik Merkezi güvenlik durumuna kaynakları tooprovide görünürlük aşağıdaki hello verilerini analiz eder, güvenlik açıklarını belirleme ve bunları azaltmanın yollarını önerilir ve etkin tehditleri algılayabilir:

- Azure Hizmetleri: hello Azure hizmetlerinin yapılandırmasına ilişkin ilgili hizmetin kaynak sağlayıcısıyla iletişim kurarak dağıtmış olan bilgileri kullanır.
- Ağ Trafiği: Microsoft’un altyapısından kaynak/hedef IP/bağlantı noktası, paket boyutu ve ağ protokolü gibi örneği alınmış ağ trafiği meta verilerini kullanır.
- İş Ortağı Çözümleri: Güvenlik duvarları ve kötü amaçlı yazılımdan koruma çözümleri gibi tümleşik iş ortağı çözümlerinden güvenlik uyarılarını kullanır. 
- Sanal Makineleriniz ve Sunucularınız: Sanal makinelerinizdeki yapılandırma bilgilerinin yanı sıra Windows olay ve denetim günlükleri, IIS günlükleri, syslog iletileri ve kilitlenme bilgi dökümü dosyaları gibi güvenlik olaylarına ilişkin bilgileri kullanır. Ayrıca, bir uyarı oluşturulduğunda, Azure Güvenlik Merkezi etkilenen hello VM diskin anlık görüntüsünü oluşturmak ve adli amaçlar için bir kayıt defteri dosyası gibi hello VM diskten makine yapıları ilgili toohello uyarı ayıklayın.


## <a name="data-protection"></a>Veri koruma
**Veriler arasında ayrım yapma**: veri hello hizmet boyunca her bir bileşende baz mantıksal olarak ayrı tutulur. Tüm veriler kuruluşa göre etiketlenir. Bu etiketleme hello veri yaşam döngüsü boyunca devam ederse ve her hello hizmet katmanında uygulanır.

**Veri erişimi**: içinde tooprovide güvenlik önerileri sipariş ve olası güvenlik tehditlerini araştırmak, Microsoft personeli erişebilir toplanan bilgiler ve kilitlenme döküm dosyaları da dahil olmak üzere Azure Hizmetleri tarafından analiz işlem oluşturma olayları, VM Disk anlık görüntüler ve yapıları kasıtsız olarak müşteri verilerini veya sanal makinelerinizi kişisel verileri içerebilir. Biz toohello uyması [Microsoft çevrimiçi hizmet koşulları ve gizlilik bildirimini](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31), Microsoft olmayan müşteri verilerini veya kullanacağınız bilgi reklam ya da benzeri ticari amaçlarla türetilen olduğunu belirtin. Yalnızca müşteri verileri, Azure ile bu hizmetleri sağlamayla uyumlu amaçlar da dahil olmak üzere Hizmetleri gerekli tooprovide olarak kullanırız. Tüm hakları tooCustomer verileri korur.

**Veri kullanımı**: Microsoft desenleri kullanır ve tehdit bilgileri birden çok görülen kiracılar tooenhance bizim önleme ve algılama yeteneklerini; biz açıklanan hello gizlilik taahhütlerine uygun olarak bunu bizim [gizlilik Deyimi](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx).

## <a name="data-location"></a>Veri konumu

**Çalışma alanları**: bir çalışma alanı Geos aşağıdaki Merhaba belirtilir ve Azure sanal kilitlenme bilgi dökümleri ve bazı uyarı veri türleri dahil olmak üzere makinelerinizden, toplanan verilerin çalışma en yakın hello depolanır. 

| VM'nin Bulunduğu Coğrafi Bölge                        | Çalışma Alanının Bulunduğu Coğrafi Bölge |
|-------------------------------|---------------|
| Amerika Birleşik Devletleri, Brezilya, Kanada | Amerika Birleşik Devletleri |
| Avrupa, Birleşik Krallık        | Avrupa        |
| Asya Pasifik, Japonya, Hindistan    | Asya Pasifik  |
| Avustralya                     | Avustralya     |

 
VM disk anlık görüntüler hello depolanan hello VM disk aynı depolama hesabı.
 
Sanal makineler ve diğer ortamlarda çalıştıran sunucular için örneğin şirket hello çalışma ve toplanan verilerin depolandığı bölge belirtebilirsiniz. 

**Azure Güvenlik Merkezi deposunda**: iş ortağı uyarılar dahil olmak üzere güvenlik uyarıları hakkında bilgi bölgesel depolanan hello toohello konumunu according ilgili Azure kaynak, ancak sistem durumu hakkında bilgi ve öneri hello Amerika Birleşik Devletleri veya toocustomer'ın konumu göre Avrupa merkezi olarak depolanır.
Azure Güvenlik Merkezi, kilitlenme döküm dosyalarının kısa ömürlü kopyalarını toplar ve açıktan yararlanma girişimlerinin ve başarılı uzlaşmaların kanıtı olarak analiz eder. Azure Güvenlik Merkezi gerçekleştirir bu analizi içinde aynı coğrafi çalışma hello gibi hello ve analiz tamamlandığında kısa ömürlü kopyaları siler hello.

Makine yapıları merkezi olarak içinde depolanan VM hello gibi aynı bölgede hello. 


## <a name="managing-data-collection-from-virtual-machines"></a>Sanal makinelerden veri toplamayı yönetme

Azure'da Güvenlik Merkezi'ni etkinleştirdiğinizde her Azure aboneliğiniz için veri toplama etkinleştirilir. Aboneliklerinizde hello Azure Güvenlik Merkezi güvenlik ilkesi bölümü için veri koleksiyonu açık da kapatabilirsiniz. Veri toplama açık olduğunda Azure Güvenlik Merkezi hükümleri hello Microsoft İzleme Aracısı tüm mevcut Azure sanal makineleri ve oluşturulan yeni bir tane desteklenmiyor. Merhaba Microsoft Monitoring agent için çeşitli güvenlik tarar ilgili yapılandırmaları ve olayları içine [Windows için olay izleme](https://msdn.microsoft.com/library/windows/desktop/bb968803.aspx) (ETW) izlerinde. Ayrıca, hello işletim sistemi hello makine çalışan hello sürecinde olay günlüğü olaylarını ortaya koyar. Bu tür verilerin örnekleri şunlardır: işletim sistemi türü ve sürümü, işletim sistemi günlükleri (Windows olay günlükleri), çalışan işlemler, makine adı, IP adresleri, oturum açmış kullanıcı ve kiracı kimliği. Merhaba Microsoft Monitoring Agent olay günlüğü girişleri okur ve ETW izler ve analiz için tooyour çalışma alanları kopyalar. Merhaba Microsoft Monitoring Agent ayrıca kilitlenme döküm dosyaları tooyour çalışma alanları kopyalar.

Azure Güvenlik Merkezi ücretsiz kullanıyorsanız, güvenlik ilkesi hello sanal makinelerden veri toplamayı devre dışı bırakabilirsiniz. Veri toplama hello standart katmanında abonelikler için gereklidir. Veri toplama devre dışı bırakılsa bile, VM diski anlık görüntüleri ve yapıt toplama işlemi etkin olmaya devam eder.


## <a name="see-also"></a>Ayrıca bkz.
Bu belgede Azure Güvenlik Merkezi'nde verilerin yönetilmesi ve korunması hakkında bilgi aldınız. Azure Güvenlik Merkezi hakkında daha fazla toolearn bakın:

* [Azure Güvenlik Merkezi planlama ve işlemler Kılavuzu](security-center-planning-and-operations-guide.md) — öğrenin nasıl tooplan ve hello tasarım konuları tooadopt Azure Güvenlik Merkezi anladığınızdan emin olun.
* [Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md) — nasıl toomonitor hello Azure kaynaklarınızın sistem durumunu öğrenin
* [Azure Güvenlik Merkezi'nde Uyarıları yönetme ve yanıt toosecurity](security-center-managing-and-responding-alerts.md) — öğrenin nasıl toomanage ve yanıt toosecurity uyarıları
* [Azure Güvenlik Merkezi ile iş ortağı çözümlerini izleme](security-center-partner-solutions.md) — nasıl toomonitor hello iş ortağı çözümlerinizin sistem durumunu öğrenin.
* [Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) — hello hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz
* [Azure Güvenlik Blogu](http://blogs.msdn.com/b/azuresecurity/) - Azure güvenliği ve uyumluluğu ile ilgili blog yazılarını bulabilirsiniz
