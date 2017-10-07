---
title: "Azure Güvenlik Merkezi ile kişisel veriler aaaProtect | Microsoft Docs"
description: "Azure Güvenlik Merkezi'ni kullanarak kişisel verilerini koruma"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 8e2c893d13318392f47fa912089d52618f9e7b45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="protect-personal-data-from-breaches-and-attacks-azure-security-center"></a>Kişisel veriler ihlallerini ve saldırılarından korumak: Azure Güvenlik Merkezi

Bu makalede, nasıl toouse Azure Güvenlik Merkezi tooprotect kişisel verileri ihlallerini anlamanıza yardımcı olur ve saldırıları.

## <a name="scenario"></a>Senaryo 

Merhaba Amerika Birleşik Devletleri, yönetim büyük seyahat şirket, kendi işlemleri toooffer programlarıyla hello İngiliz Adaları arasında yanı sıra hello Akdeniz ve Baltık seas genişletmektedir. toohelp bu çaba içinde İtalya, Almanya, Danimarka ve hello İngiltere dayanarak birkaç küçük seyahat satırları aldı

Merhaba şirket hello bulutta Microsoft Azure toostore şirket verileri kullanır. Bu adlar, adresler, telefon numarası ve kredi kartı bilgileri gibi kişisel olarak tanımlanabilir bilgileri içerir. İnsan Kaynakları bilgi ayrıca gibi içerir:

- Adresler
- Telefon numaraları
- Vergi kimlik numaraları
- Sağlık bilgileri

Merhaba seyahat satır de ödül ve bağlılık programı üyelerinin büyük bir veritabanı tutar. Şirket çalışanları erişim hello ağdan hello şirketin şubelere ve seyahat aracılar bulunan Merhaba Dünya toosome şirket kaynaklarına sahip.
Kişisel veriler hello ağ üzerinden bu konumları ve hello Microsoft Veri Merkezi arasında geçen.

## <a name="problem-statement"></a>Sorun bildirimi

Hello Azure kaynaklarını saldırılar hello tehlikesi endişe bir şirkettir. Müşterilerin ve çalışanların kişisel veriler toounauthorized kişi tooprevent riskini isterler. Hem önleme ve yanıt/düzeltme işlemi, hem de bulut kaynakları bir etkili şekilde toomonitor hello devam eden güvenlik kılavuzu isterler.
Güçlü bir günümüzün karmaşık ve organize saldırganlara karşı savunma hattı ihtiyaç duyar.

## <a name="company-goal"></a>Şirket hedefi

Merhaba şirketin hedeflerine müşterilerin ve çalışanların kişisel verilerin tooensure hello gizliliği tehditlerine karşı koruma tarafından biridir. İhlali toomitigate toosigns etkisi hello hemen hedeflerine toorespond biridir. Geçerli güvenlik durumunu tooassess hello şekilde gerektirir, savunmasız yapılandırmaları tanımlamak ve düzeltmek.

## <a name="solutions"></a>Çözümler

Microsoft Azure Güvenlik Merkezi (ASC) bir tümleşik güvenlik izleme ve ilke yönetimi çözümü sağlar. Bu, kullanımı kolay ve etkili tehdit önleme, saptama ve yanıtlama işlevlerini sunar.

### <a name="prevention"></a>Önleme

ASC tooset güvenlik ilkeleri etkinleştirerek açıklarına, yalnızca zaman erişim sağlamak ve güvenlik önerilerini uygulama yardımcı olur.

Bir güvenlik ilkesi hello belirtilen hello içindeki kaynaklar için önerilen denetimleri kümesini tanımlayan abonelik. Tam zamanında erişim gelen trafiği tooyour Azure VM'ler, etkilenme tooattacks azaltma aşağı kullanılan toolock olabilir. Güvenlik önerileri hello Azure kaynaklarınızın güvenlik durumunu çözümledikten sonra ASC tarafından oluşturulur.

#### <a name="how-do-i-set-security-policies-in-asc"></a>Güvenlik ilkeleri ASC nasıl ayarlarım?

Her bir abonelik için güvenlik ilkeleri yapılandırabilirsiniz. bir güvenlik ilkesi toomodify sahibi veya katkıda bu aboneliğin olması gerekir. Hello Azure portalı, aşağıdaki hello:

1. Seçin **İlkesi** hello ASC panosunda.

2. Tooenable hello İlkesi istediğiniz hello aboneliği seçin.

3. Seçin **önleme İlkesi** abonelik başına tooconfigure ilkeleri. **Sanal makinelerden veri toplama** çok ayarlanmalıdır**üzerinde.**

4. Merhaba, **önleme İlkesi** seçenekleri, select **üzerinde** hello abonelik için uygun olan tooenable hello güvenlik önerileri.

![](media/protect-personal-data-azure-security-center/prevention-policy.png)

Daha ayrıntılı yönergeler ve etkinleştirilebilir hello İlkesi önerileri bir açıklaması için bkz: [Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](https://docs.microsoft.com/azure/security-center/security-center-policies#set-security-policies).

#### <a name="how-do-i-configure-just-in-time-access-jit"></a>Zaman erişim (JIT) nasıl sadece yapılandırırım?

JIT etkinleştirilmişse, Güvenlik Merkezi bir NSG kuralı oluşturarak Azure VM'ler gelen trafiği tooyour kilitler. Merhaba bağlantı noktalarını seçmek aşağı gelen trafiği üzerinde hello VM toowhich kilitlenir. toouse JIT erişmek için aşağıdaki hello:

1. Select hello **zaman VM erişim döşemesinin sadece** hello ASC dikey.

2. Select hello **önerilen** sekmesi.

3. Altında **VM'ler**, hello VM'ler tooenable istediğinizi seçin. Bir onay işareti sonraki tooa VM koyar. 
4. Seçin **etkinleştirmek JIT** vm'lerde.
5. **Kaydet**’i seçin.

Daha sonra JIT için etkinleştirilen ASC önerir hello varsayılan bağlantı noktalarını görebilirsiniz. Ayrıca, ekleyebilir ve tooenable hello yalnızca zaman çözümü istediğiniz yeni bir bağlantı noktası yapılandırın. Merhaba **saat VM erişimi hemen** hello Güvenlik Merkezi parçasında JIT erişimi için yapılandırılan VM hello sayısını gösterir. Ayrıca, geçen hafta hello yapılan onaylanan erişim istekleri hello sayısını gösterir.

![](media/protect-personal-data-azure-security-center/jit-vm.png)

Yönergeler için toodo bunu ve zaman Access'te sadece hakkında ek bilgi için bkz [tam zamanında kullanarak sanal makine erişimini yönetme.](https://docs.microsoft.com/azure/security-center/security-center-just-in-time)

#### <a name="how-do-i-implement-asc-security-recommendations"></a>ASC güvenlik önerileri nasıl uygulansın mı?

Güvenlik Merkezi olası güvenlik açıklarını belirlediğinde öneriler oluşturur. Merhaba önerileri gerekli hello denetimlerini yapılandırma hello işleminde size kılavuzluk. 
1. Select hello **önerileri** döşeme hello ASC Panoda.

2. Her satır bir öneri temsil ettiği bir tablo biçiminde gösterilen hello önerileri görüntüleyin.

3. toofilter önerileri seçin **filtre** ve toosee istediğiniz hello önem ve durum değerleri seçin.

4. toodismiss geçerli olmayan bir öneri, sağ tıklatın ve seçin **atla.**

5. Hangi öneri önce uygulanması gereken değerlendirin.

6. Öncelik sırasına göre Hello önerileri geçerlidir.

Olası önerileri ve nasıl kılavuzlarına listesi için bkz tooapply her [Azure Güvenlik Merkezi'nde güvenlik önerilerini yönetme.](https://docs.microsoft.com/azure/security-center/security-center-recommendations)

### <a name="detection-and-response"></a>Algılama ile yanıtı

Bir tehdit algılandıktan sonra toorespond mümkün olan en kısa sürede istediğiniz şekilde algılama ile yanıtı birlikte gidin.
ASC tehdit algılama, Azure kaynaklarını, hello ağ ve bağlı iş ortağı çözümlerinden güvenlik bilgileri otomatik olarak toplayarak çalışır. Saldırganlar yeni ve giderek karmaşık ortaya çıkardıkça ASC kendi algılama algoritmalarını hızlı bir şekilde güncelleştirebilirsiniz. Tehdit algılama ASC'ın nasıl çalıştığı hakkında daha ayrıntılı bilgi için bkz: [Azure Güvenlik Merkezi algılama özellikleri](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities).

#### <a name="how-do-i-manage-and-respond-toosecurity-alerts"></a>Nasıl yönetmek ve toosecurity uyarıları yanıt?

Öncelikli güvenlik uyarıları listesi hello birlikte Güvenlik Merkezi'nde gösterilen tooquickly gereksinim duyduğunuz bilgileri hello sorunu araştırın. Güvenlik Merkezi, ayrıca nasıl için öneriler içerir tooremediate saldırının. Güvenlik Uyarıları, aşağıdaki hello yapmak toomanage:

1. Select hello **güvenlik uyarıları** döşeme hello ASC panosunda. Her uyarı ayrıntılarını gösterir.

2. Tarih, durum ve önem derecesi göre toofilter uyarıları seçin **filtre** ve toosee istediğiniz hello değerleri seçin.

3. toorespond tooan uyarı, onu seçin, hello bilgileri gözden geçirin ve sonra Saldırıya uğrayan hello kaynağı seçin.

4. Merhaba, **açıklama** alan, önerilen düzeltmeyi dahil ayrıntılarını göreceksiniz.

![](media/protect-personal-data-azure-security-center/security-alerts.png)

Daha ayrıntılı yanıt veren toosecurity uyarılar hakkında yönergeler için bkz: [yönetme ve yanıt toosecurity Azure Güvenlik Merkezi'nde uyarıları.](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts)

Güvenlik Uyarıları araştırırken daha fazla yardım için hello şirket kendi SIEM çözümüyle ASC uyarıları tümleşebilir kullanılarak [Azure günlük tümleştirme](https://aka.ms/AzLog).

#### <a name="how-do-i-manage-security-incidents"></a>Güvenlik olayları nasıl yönetebilirim?

ASC bir güvenlik olayı sonlandırma zinciri desenlerle Hizala tüm uyarıların bir kaynak için bir toplama ' dir. Bir olay, tooobtain sağlayan hello ilgili uyarıların listesi, her oluşumu hakkında daha fazla bilgi görüntüleyebilirsiniz. Olaylar, güvenlik uyarıları kutucuğu hello ve dikey penceresi görünür.

tooreview ve güvenlik olayları yönetmek için aşağıdaki hello:

1. Select hello **güvenlik uyarıları** döşeme. bir güvenlik olayı algılanırsa, hello güvenlik uyarıları grafiğin altında görünür. Diğer uyarılardan farklı bir simge sahip olur.

2. Bu güvenlik olayı hakkında daha fazla ayrıntı Hello olay toosee seçin. Ek ayrıntılar dahil tam açıklamasını, kendi önem derecesi, kendi geçerli durumunda, saldırıya hello kaynak, hello düzeltme adımları hello olay için ve bu olayın eklenmiş olan uyarılar hello.

Toosee filtreleyebilirsiniz **olaylar yalnızca**, **yalnızca uyarıları**, veya **her ikisi de**.

#### <a name="how-do-i-access-hello-threat-intelligence-report"></a>Merhaba tehdit Intelligence rapor nasıl erişirim?

ASC birden çok kaynakları tooidentify tehditlere karşı bilgileri analiz eder. tooassist olay yanıtlama ekipleri araştırmak ve tehditleri düzeltme, Güvenlik Merkezi algılandı hello tehdit hakkında bilgi içeren bir tehdit Intelligence rapor içerir.

Güvenlik Merkezi üç tür saldırı değişebilir tehdit rapor vardır.
kullanılabilir Hello raporlar şunlardır:

- Etkinlik grubu raporu: saldırganlar, hedefler ve taktiği derin çekecek sağlar.

- Kampanya raporu: belirli saldırı Kampanyalar ayrıntılarını odaklanır.

- İş parçacığı özet raporu: hello önceki iki raporlarındaki tüm öğeleri içerir.

Bu tür bilgiler hello olay yanıtlama işlemi sırasında çok kullanışlı, bir sürekli araştırma toounderstand hello kaynak hello saldırı olduğunda, saldırganın sözleri ve hangi toodo toomitigate, bu sorunu taşıma İleri hello.

1. tooaccess hello tehdit bilgileri bildirmek için aşağıdaki hello:

2. Select hello **güvenlik uyarıları** döşeme hello ASC Panoda.

3. Daha fazla bilgi tooobtain istediğiniz hello güvenlik uyarısı seçin.

4. Merhaba, **raporları** hello bağlantı toohello tehdit Intelligence rapor'ı tıklatın.

5. Bu indirebilirsiniz hello PDF dosyasını açar.

![](media/protect-personal-data-azure-security-center/security-alerts-suspicious-process.png)

Merhaba ASC tehdit Intelligence rapor hakkında ek bilgi için bkz: [Azure Güvenlik Merkezi tehdit Intelligence rapor.](https://docs.microsoft.com/azure/security-center/security-center-threat-report)

### <a name="assessment"></a>Değerlendirme

toohelp test etme, değerlendirme ve güvenlikle ilgili tutumunuzu değerlendirmesine ASC Qualys ile tümleşik güvenlik açığı değerlendirmesi için bulut aracıları, sanal makine önerileri bileşen bir parçası olarak sağlar.

Merhaba Qualys Aracısı Güvenlik Açığı ve sistem durumu izleme verilerini tooASC geri gönderen güvenlik açığı veri toohello Qualys yönetim platformu, raporlar. bir güvenlik açığı değerlendirmesi çözümü hello görüntülenir öneri tooadd hello **önerileri** dikey penceresinde hello ASC Panoda.

Merhaba güvenlik açığı değerlendirmesi çözüm hello hedef VM yüklendikten sonra Güvenlik Merkezi taramaları VM toodetect hello ve sistem ve uygulama güvenlik açıklarını belirleme. Sorunları hello altında gösterilen algılanan **sanal makine önerileri** seçeneği.

#### <a name="how-do-i-implement-a-vulnerability-assessment-solution"></a>Bir güvenlik açığı değerlendirmesi çözümü nasıl uygulansın mı? 

Bir sanal makine zaten dağıtılmış bir tümleşik güvenlik açığı değerlendirmesi çözüm yoksa, Güvenlik Merkezi yüklü olmasını önerir.

1. Merhaba üzerinde hello ASC panosunda **önerileri** dikey penceresinde, select **bir güvenlik açığı değerlendirmesi çözüme ekleyin.**

2. Merhaba VM'ler tooinstall hello güvenlik açığı değerlendirmesi çözüm istediğiniz yeri seçin.

3. Tıklayın **[sayısı] Vm'lerinde yükleyin.**

4. Hello Azure Marketi veya altındaki bir iş ortağı çözümü seçin **varolan bir çözümü kullanın** seçin **Qualys.**

5. Hello hello otomatik güncelleştirme ayarlarını açıp kapatabilirsiniz **iş ortağı çözümleri** dikey.

Daha ayrıntılı yönergeler için tooimplement bir güvenlik açığı değerlendirmesi çözüm bkz [Azure Güvenlik Merkezi'nde Güvenlik Açığı değerlendirmesi.](https://docs.microsoft.com/azure/security-center/security-center-vulnerability-assessment-recommendations)

## <a name="next-steps"></a>Sonraki adımlar

- [Azure Güvenlik Merkezi Hızlı Başlangıç Kılavuzu](https://docs.microsoft.com/azure/security-center/security-center-get-started)

- [Giriş tooAzure Güvenlik Merkezi](https://docs.microsoft.com/azure/security-center/security-center-intro)

- [Azure Güvenlik Merkezi uyarılarını Azure günlük tümleştirme ile tümleştirme](https://docs.microsoft.com/azure/security-center/security-center-integrating-alerts-with-log-integration)

- [Artırma Azure Güvenlik Merkezi ile tümleşik güvenlik açığı değerlendirmesi](https://blogs.msdn.microsoft.com/azuresecurity/2016/12/16/boost-azure-security-center-with-integrated-vulnerability-assessment/)
