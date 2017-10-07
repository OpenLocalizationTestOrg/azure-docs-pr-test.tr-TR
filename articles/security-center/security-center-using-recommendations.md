---
title: "Azure Güvenlik Merkezi önerileri tooenhance güvenlik aaaUse | Microsoft Docs"
description: " Nasıl bir güvenlik saldırısı toouse güvenlik ilkeleri ve öneriler Azure Güvenlik Merkezi toohelp içinde en aza öğrenin. "
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/08/2017
ms.author: terrylan
ms.openlocfilehash: bd314350a5abfceea3e171f2e1b55afe4549c1b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-security-center-recommendations-tooenhance-security"></a>Kullanım Azure Güvenlik Merkezi önerileri tooenhance güvenliği
Bir güvenlik ilkesi yapılandırma ve Azure Güvenlik Merkezi tarafından sağlanan hello öneriler uygulayarak bir önemli güvenlik olayı hello olasılığını azaltır. Bu makalede nasıl güvenlik saldırısı toouse güvenlik ilkeleri ve Güvenlik Merkezi toohelp önerileri en aza gösterilmektedir.

> [!NOTE]
> Bu makalede hello rolleri ve Güvenlik Merkezi hello sunulan kavramlar derlemeler [planlama ve işlemler Kılavuzu](security-center-planning-and-operations-guide.md). Bu, devam etmeden önce bir fikir tooreview hello Planlama Kılavuzu gösterir.
>
>

## <a name="managing-security-recommendations"></a>Güvenlik önerilerini yönetme
Bir güvenlik ilkesi hello hello belirtilen abonelik veya kaynak grubu içindeki kaynaklar için önerilen denetimleri kümesini tanımlar. Güvenlik Merkezi'nde tooyour şirketinizin güvenlik gereksinimlerine göre ilkeleri tanımlarsınız. toolearn daha, fazla [Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md).

Kaynak grupları için güvenlik ilkelerini hello abonelik düzeyinden devralınır.

![Güvenlik İlkesi Devralma][1]

Belirli kaynak gruplarında özel ilkelere gereksinim duyarsanız hello kaynak grubundaki devralmayı devre dışı bırakabilirsiniz. toodisable, devralma tooUnique dikey penceresinde hello güvenlik ilkesi ayarlayın ve Güvenlik Merkezi önerileri için gösterir hello denetimleri özelleştirebilirsiniz.

Örneğin, hello SQL veritabanında saydam veri şifreleme (TDE'nin) ilkesini gerektirmeyen iş yükleriniz varsa hello İlkesi hello abonelik düzeyinde devre dışı bırakın ve SQL TDE'nin gerekli olduğu yalnızca hello kaynak gruplarında etkinleştirin.

> [!NOTE]
> Abonelik düzeyi ilkesi ile kaynak grubu düzeyi ilkesi arasında bir çakışma varsa, hello kaynak grubu düzeyi ilkesi önceliklidir.
>
>

Güvenlik Merkezi hello Azure kaynaklarınızın güvenlik durumunu çözümler. Güvenlik Merkezi olası güvenlik açıklarını belirlediğinde hello güvenlik ilkesi ayarlayın hello denetimlerinde dayalı olarak öneriler oluşturur. Merhaba önerileri gerekli hello güvenlik denetimlerini yapılandırma hello işleminde size kılavuzluk.

Güvenlik Merkezi odağı sistem güncelleştirmeleri, işletim sistemi yapılandırması, geçerli ilke önerileri ağ alt ağlar ve sanal makineleri (VM'ler) SQL veritabanı denetimi, SQL veritabanı TDE, güvenlik grubu ve web uygulaması güvenlik duvarları. Merhaba en güncel kapsamını Güvenlik Merkezi önerileri için bkz: [Güvenlik Merkezi'nde güvenlik önerilerini yönetme](security-center-recommendations.md).

## <a name="scenario"></a>Senaryo
Bu senaryoyu nasıl toouse Güvenlik Merkezi toohelp azaltmak bir önemli güvenlik olayı hello olasılığını Güvenlik Merkezi önerilerini izleme ve eylemde gösterir. Merhaba senaryo kullanır hello kurgusal şirket, Contoso, ve rolleri içinde sunulan Güvenlik Merkezi hello [planlama ve işlemler Kılavuzu](security-center-planning-and-operations-guide.md#security-roles-and-access-controls). Merhaba rolleri, kişiler ve Güvenlik Merkezi tooperform farklı güvenlikle ilgili görevleri kullanabilir takımlar temsil eder. Merhaba rolü şunlardır:

![Senaryo rolleri][2]

Contoso son kullanıcıların şirket içi kaynakları tooAzure bazıları geçirildi. Contoso tooimplement istediği ve bunların güvenlik açığı tooa güvenlik saldırısı hello bulutta kaynaklarının azaltmak korumaları sürdürün.

## <a name="recommended-solution"></a>Önerilen çözüm
Bir çözüm toouse Güvenlik Merkezi tooprevent olduğundan ve güvenlik açıkları algılayabilir. Contoso Azure aboneliğini aracılığıyla erişim tooSecurity merkezi sahiptir. Merhaba [ücretsiz katmanı](security-center-pricing.md) , Güvenlik Merkezi tüm Azure abonelikleri üzerinde otomatik olarak etkinleştirilir ve veri toplama, Abonelikteki tüm VM'ler üzerinde etkindir.

Contoso'nun BT güvenliği, David yapılandırır bir **Güvenlik İlkesi** Güvenlik Merkezi'ni kullanma. Güvenlik Merkezi Contoso Azure kaynaklarını hello güvenlik durumunu çözümler. Güvenlik Merkezi olası güvenlik açıklarını belirlediğinde oluşturur **önerileri** hello güvenlik ilkesi ayarlayın hello denetimleri göre.

Jeff, bir bulut iş yükü sahibi, uygulama ve korumaları Contoso'nun güvenlik ilkelerini uygun koruma sorumludur. Jeff Güvenlik Merkezi tooapply korumaları göre oluşturulan hello önerileri izleyebilirsiniz. Merhaba önerileri Jeff gerekli hello güvenlik denetimlerini yapılandırma hello işleminde size kılavuzluk.

İçinde sipariş Jeff tooimplement için korumaları korumak ve güvenlik açıkları, he gereksinimlerine ortadan:

- Güvenlik Merkezi tarafından sağlanan güvenlik önerileri izleyin
- Güvenlik önerileri değerlendirmek ve kendisine uygulama kapatmak veya, karar verin
- Güvenlik önerileri uygulayın

Şimdi Jeff'ın adımları toosee izleyin nasıl kendisinin Güvenlik Merkezi önerileri tooguide ona denetimleri tooeliminate güvenlik açıkları yapılandırma hello süreci kullanır.

## <a name="how-tooimplement-this-solution"></a>Nasıl tooimplement bu çözümü
Jeff oturum açtığında çok[Azure portal](https://azure.microsoft.com/features/azure-portal/) ve hello Güvenlik Merkezi Konsolu açılır. Varsa güvenlik önerileri hello aşağıdaki adımları gerçekleştirerek izleme etkinlikleri kendi günlük bir parçası olarak, kendisinin toosee denetler:

1. Jeff seçer hello **önerileri** döşeme tooopen hello **önerileri** dikey.
   ![Select hello önerileri döşeme][3]
2. Jeff öneriler hello listesi inceler. Güvenlik Merkezi önerileri en yüksek öncelik toolowest öncelikten öncelik sırasına hello listesi sağlamıştır görür. Kendisine tooaddress yüksek öncelikli öneri hello listesinde karar verir. Belirliyor **Endpoint Protection Yükle** hello üzerinde **önerileri** dikey.
3. Merhaba **Endpoint Protection Yükle** etkin kötü amaçlı yazılımdan koruma VM'ler listesini görüntüleyen dikey pencere açılır. Jeff hello VM'lerin listesini gözden geçirir, tüm VM'ler seçer ve ardından seçer **3 Vm'lerinde yükleme**.
   ![Uç nokta korumasını yükleme][4]
4. Merhaba **işaretleyin Endpoint Protection** dikey ile iki kötü amaçlı yazılımdan koruma çözümleri sağlayan Jeff açar. Jeff seçer hello **Microsoft Antimalware** çözümü.
5. Merhaba kötü amaçlı yazılımdan koruma çözümü hakkında ek bilgi görüntülenir. Jeff seçer **oluşturma**.
   ![Microsoft kötü amaçlı yazılımdan koruma][5]
6. Jeff girer hello gerekli yapılandırma ayarlarını hello üzerinde **yükleme** dikey penceresinde ve seçer **Tamam**.

[Microsoft Antimalware](../security/azure-security-antimalware.md) hello etkin VM'ler seçili artık.

Jeff toomove hello yüksek öncelikli ve orta öncelikli önerileri aracılığıyla mantığınız kararları devam eder. Jeff başvuran hello [güvenlik önerilerini yönetme](security-center-recommendations.md) toounderstand hello öneriler ve kendisine uygulanıyorsa, her biri yaptığı makalesi.

Jeff öğrenir [Microsoft Güvenlik Yanıt Merkezi (MSRC)](../security/azure-security-response-center.md) select güvenlik hello Azure ağ ve altyapı izleme gerçekleştirir ve Üçüncü taraflardan tehdit Intelligence ve kötüye şikayetlerinden alır. Jeff Contoso'nun Azure aboneliği için güvenlik iletişim ayrıntılarını sağlıyorsa, Microsoft kişiler bu Contoso'nun müşteri verilerini hello MSRC belirlerse, Contoso erişilmeden yasadışı veya yetkisiz bir tarafın. Kendisine hello uygularken Jeff şimdi izleyin **güvenlik iletişim ayrıntılarını sağlamak** öneri (bir öneri önem derecesi Orta Yukarıdaki önerileri hello listesinde).

1. Jeff seçer **güvenlik iletişim ayrıntılarını sağlamak** hello üzerinde **önerileri** hello açar dikey **güvenlik iletişim ayrıntılarını sağlayın** dikey.
2. Jeff hello Azure aboneliği tooprovide kişi bilgilerini üzerinde seçer. İkinci bir **güvenlik iletişim ayrıntılarını sağlamak** dikey pencere açılır.
   ![Güvenlik kişi ayrıntıları][6]
3. Merhaba üzerinde ikinci **güvenlik iletişim ayrıntılarını sağlamak** dikey penceresinde Jeff girer:

  - Merhaba güvenlik iletişim e-posta adresleri (yok bir toohello sayısı sınırı kendisinin girebilirsiniz e-posta adresleri) virgülle ayrılmış
  - bir güvenlik, telefon numarası ile iletişime geçin

4. Jeff hello seçeneği de kapatır **bana Gönder e-postalar uyarılar hakkında** tooreceive e-postaları yüksek öneme sahip uyarılar hakkında.
5. Jeff seçer **Tamam** tooapply hello güvenlik bilgileri tooContoso'nin abonelik başvurun.

Son olarak, Jeff hello düşük öncelikli işler için öneri incelemeleri **düzeltmek OS güvenlik açıkları** ve bu öneriyi uygulanamaz belirler. Toodismiss hello öneri istediği. Jeff seçer toohello sağ ve seçer görünür hello üç nokta **atla**.
   ![Öneri yok sayın][7]

## <a name="conclusion"></a>Sonuç
Güvenlik Merkezi'nde öneriler izleme, saldırının gerçekleşmeden önce güvenlik açıkları ortadan kaldırmanıza yardımcı olabilir. Uygulama ve Güvenlik Merkezi'nde güvenlik ilkeleriyle korumaları koruma tarafından bir güvenlik olayı engelleyebilir.

<!--Image references-->
[1]: ./media/security-center-using-recommendations/security-center-policy-inheritance.png
[2]: ./media/security-center-using-recommendations/scenario-roles.png
[3]: ./media/security-center-using-recommendations/select-recommendations-tile.png
[4]: ./media/security-center-using-recommendations/install-endpoint-protection.png
[5]:./media/security-center-using-recommendations/microsoft-antimalware.png
[6]: ./media/security-center-using-recommendations/provide-security-contact-details.png
[7]: ./media/security-center-using-recommendations/dismiss-recommendation.png
