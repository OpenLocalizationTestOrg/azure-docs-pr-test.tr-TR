---
title: "aaaPrevent beklenmeyen maliyetlerini yönetme faturalama - Azure | Microsoft Docs"
description: "Bilgi nasıl tooavoid Azure faturasını beklenmeyen giderler. Microsoft Azure aboneliği için maliyet izleme ve yönetim özelliklerini kullanabilirsiniz."
services: 
documentationcenter: 
author: tonguyen10
manager: tonguyen
editor: 
tags: billing
ms.assetid: 482191ac-147e-4eb6-9655-c40c13846672
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/10/2017
ms.author: tonguyen
experimental_id: a2b2579c-cd2e-41
ms.openlocfilehash: 4827c65a55fe953c329ab26cc4e882266073c60a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="prevent-unexpected-costs-with-azure-billing-and-cost-management"></a>Azure faturalama ve maliyet yönetimi ile beklenmeyen maliyetleri engelle

Azure için kaydolduğunuzda, harcama iyi bir fikir tooget yapabileceğiniz birkaç işlem vardır. Merhaba, [Azure portal](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade), hello abonelik seçtiğinizde, geçerli maliyet dökümünü görmek ve yazma oranı. Ayrıca [indirme faturaları ve ayrıntılı kullanım dosyalar](billing-download-azure-invoice-daily-usage-date.md). Farklı projelere veya gruplar için kullanılan kaynaklar için toogroup maliyetleri istiyorsanız bakmak [kaynak etiketleme](../azure-resource-manager/resource-group-using-tags.md). Kuruluşunuz toouse tercih ettiğiniz bir raporlama sistemi varsa, hello denetleyin [API'leri faturalama](billing-usage-rate-card-overview.md). 

Günlük kullanımı hakkında daha fazla bilgi için bkz: [faturanızı anlamak için Microsoft Azure](billing-understand-your-bill.md).

Aboneliğinizi bir Kurumsal Anlaşma (Kurumsal Sözleşme), bulut çözümü sağlayıcısı (CSP) veya Azure sponsorluk ise, bu makaledeki birçok özellik tooyou uygulanmaz. Bunun yerine, farklı bir maliyet yönetimi için kullanabileceğiniz araçlar kümesi vardır. Bkz: [EA, CSP ve sponsorluk için ek kaynaklar](#other-offers).

Aboneliğinizin ücretsiz bir deneme ise [Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/), açık (AIO) ya da BizSpark, Azure hakkında bilgi edinin [harcama limitlerini](#spending-limit) tooavoid unexpectantly devre dışı aboneliğiniz sahip. 

## <a name="day-0-before-you-add-azure-services"></a>0. gün: Azure Hizmetleri, Ekle

### <a name="estimate-cost-online-using-hello-pricing-calculator"></a>Tahmini maliyet çevrimiçi hello fiyatlandırma hesaplayıcısı kullanma

Merhaba denetleyin [fiyatlandırma hesaplayıcısı](https://azure.microsoft.com/pricing/calculator/) ve [toplam sahip olma hesaplayıcı maliyeti](https://aka.ms/azure-tco-calculator) tooget bir tahmin hello aylık maliyeti, ilgilendiğiniz hello hizmet. Örneğin, A1 Windows sanal makine (VM) hello tüm zaman çalışmasını bırakırsanız $66.96 ABD Doları/ay saat işlem tahmini toocost şöyledir:

![Merhaba fiyatlandırma hesaplayıcısı A1 Windows VM aylık tahmini toocost $66.96 ABD Doları olduğunu gösteren ekran görüntüsü](./media/billing-getting-started/pricing-calcVM.png)

Daha fazla bilgi için bkz: [fiyatlandırma hakkında SSS](https://azure.microsoft.com/pricing/faq/). Veya tootalk tooa kişi istiyorsanız 1-800-867-1389 çağırın.

### <a name="check-your-subscription-and-access"></a>Abonelik ve erişim denetimi

Görüntüleme maliyetleri gerektiren [abonelik düzeyinde erişim toobilling bilgi](billing-manage-access.md), ancak yalnızca hello Hesap Yöneticisi hello erişebilir [hesap Merkezi'nde](https://account.windowsazure.com/Home/Index)faturalama bilgileri değiştirme ve abonelikleri yönetme. Merhaba Hesap Yöneticisi hello kaydolma işlemine geçmeden hello kullanıcıdır. Daha fazla bilgi için bkz: [hello abonelik ya da hizmetleri yönetmek ekleme veya değiştirme Azure yönetici rolleri](billing-add-change-azure-subscription-administrator.md).

toosee olduğunuz hello Hesap Yöneticisi gönderilmiyorsa toohello [abonelikleri dikey penceresinde hello Azure portal](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) ve hello erişiminiz Aboneliklerin listesini bakın. Kısmına bakın **My rol**. Bunu diyorsa *Hesap Yöneticisi*, Tamam sonra. Gibi başka bir şey diyorsa *sahibi*, sonra da tam ayrıcalığa sahip değilsiniz.

![Merhaba hello Azure portalında abonelikleri görünümünde rolünüze ekran görüntüsü](./media/billing-getting-started/sub-blade-view.PNG)

Olduğunuz değil hello Hesap Yöneticisi sonra birisi aracılığıyla kısmi erişim büyük olasılıkla verdiğiniz [Azure Active Directory rol tabanlı erişim denetimi](../active-directory/role-based-access-control-configure.md) (RBAC). toomanage abonelikleri ve değişiklik bilgileri, fatura [hello Hesap Yöneticisi Bul](billing-subscription-transfer.md#whoisaa) ve tooperform hello görevleri isteyin veya [aktarım hello abonelik tooyou](billing-subscription-transfer.md).

Hesap yöneticiniz artık değil, kuruluşunuz ve toomanage faturalama ihtiyacınız varsa [desteğine başvurun](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade). 

### <a name="spending-limit"></a>Bir harcama sınırına sahip olmadığını denetleyin

Krediler kullanan bir aboneliğiniz varsa, ardından harcama sınırı hello sizin için varsayılan olarak açıktır. Tüm kredinizi, harcadığı zaman bu şekilde, kredi kartınızdan ücret değil. Merhaba bkz [Azure teklifleri ve harcama sınırı, hello kullanılabilirlik tam listesi](https://azure.microsoft.com/support/legal/offer-details/).

Ancak, harcama limitine ulaştı, hizmetlerinizi devre dışı. Vm'leriniz serbest anlamına gelir. tooavoid hizmeti kapalı kalma süresi, harcama sınırı hello kapatmanız gerekir. Aşmalar üzerine dosyada kredi kartınızdan ücret. 

size, harcama sınırı var varsa toosee Git toohello [abonelikleri görmek hello hesap Merkezi'nde](https://account.windowsazure.com/Subscriptions). Harcama sınırınızı açıksa bir başlığın görünür:

![Harcama sınırı üzerinde hello hesap Merkezi'nde olan hakkında bir uyarı gösteren ekran görüntüsü](./media/billing-getting-started/spending-limit-banner.PNG)

Merhaba başlığını tıklatın ve harcama sınırı tooremove hello istemleri izleyin. Kaydolurken kredi kartı bilgilerini girmediyseniz, harcama sınırı tooremove hello girmeniz gerekir. Daha fazla bilgi için bkz: [Azure harcama sınırını – nasıl çalıştığını ve nasıl tooenable veya kaldırmayı](https://azure.microsoft.com/pricing/spending-limits/).

### <a name="set-up-billing-alerts"></a>Fatura uyarılarını ayarlama

Kullanım maliyetleriniz belirttiğiniz bir miktar aştıklarında tooget e-postaları fatura Uyarıları ayarlayın. Aylık kredilerin varsa, belirtilen tutarı oluşturan kullandığınızda için uyarıları ayarlama. Daha fazla bilgi için bkz: [uyarılar, Microsoft Azure abonelikleri için ödeme yukarı ayarlamak](billing-set-up-alerts.md).

![Fatura bir uyarı e-posta ekran görüntüsü](./media/billing-getting-started/billing-alert.png)

> [!NOTE]
> Bu özellik hala önizlemede olduğundan kullanımınızı düzenli olarak denetlemeniz gerekir.

Toouse hello maliyetini tahmin, ilk uyarı için bir kılavuz olarak fiyatlandırma hesaplayıcısı hello gelen isteyebilirsiniz.

### <a name="understand-limits-and-quotas-for-your-subscription"></a>Sınırları ve kotalar aboneliğiniz için anlama

Tooeach abonelik hello CPU çekirdek sayısı ve IP adresleri gibi şeyler için varsayılan sınır vardır. Bu sınırları dikkatli olun. Daha fazla bilgi için bkz: [Azure aboneliği ve hizmet sınırları, kotaları ve kısıtlamaları](../azure-subscription-service-limits.md). Bir artış tooyour sınırı veya göre kota isteği [Destek](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).

## <a name="day-1-as-you-add-services"></a>1. güne: Hizmetleri ekledikçe

### <a name="review-hello-estimated-cost-in-hello-portal"></a>Gözden geçirme hello tahmini maliyet hello portalında

Genellikle hello Azure portalına hizmet eklemek, benzer bir tahmini maliyet aylık gösteren bir görünüm yok. Örneğin, Windows VM hello boyutunu seçtiğinizde hello hello işlem saatleri için aylık maliyeti tahmini bakın:

![Örnek: A1 Windows VM aylık tahmini toocost $66.96 ABD Doları değil.](./media/billing-getting-started/vm-size-cost.PNG)

### <a name="tags"></a>Faturalama verileriniz etiketleri tooyour kaynakları toogroup Ekle

Desteklenen hizmetler için etiketleri toogroup faturalama verisi kullanabilirsiniz. Örneğin, birkaç VM'ler farklı ekipler için çalıştırırsanız, etiketleri toocategorize maliyetleri maliyet merkezi (HR, pazarlama, Finans) ya da ortam (üretim, üretim öncesi test) kullanabilirsiniz. 

![Etiketleri ayarlama hello Portalı'nda gösteren ekran görüntüsü](./media/billing-getting-started/tags.PNG)

görünümleri raporlama farklı maliyet Hello etiketleri gösterilir. Örneğin, görünür, [analiz görünümü maliyet](#costs) hemen ve [kullanım .csv ayrıntı](#invoice-and-usage) ilk fatura süreniz sonra.

Daha fazla bilgi için bkz: [kullanarak Azure kaynaklarınızı tooorganize etiketler](../azure-resource-manager/resource-group-using-tags.md).

### <a name="consider-enabling-cost-cutting-features-like-auto-shutdown-for-vms"></a>VM'ler için otomatik kapatma gibi maliyet kesme özellikleri etkinleştirmeyi düşünün

Senaryonuza bağlı olarak, hello Azure portal'ın Vm'leriniz için otomatik kapatma yapılandırabilirsiniz. Daha fazla bilgi için bkz: [Azure Kaynak Yöneticisi'ni kullanarak sanal makineleri için otomatik kapatma](https://azure.microsoft.com/blog/announcing-auto-shutdown-for-vms-using-azure-resource-manager/).

![Merhaba portal otomatik kapatma seçeneğinin ekran görüntüsü](./media/billing-getting-started/auto-shutdown.PNG)

Otomatik kapatma değil hello içinde kapattığınızda VM güç seçenekleri ile Merhaba gibi aynı. Otomatik kapatma durdurur ve ek kullanım ücretleri VM'ler toostop kaldırır. Fiyatlandırma hakkında SSS için daha fazla bilgi için bkz: [Linux VM'ler](https://azure.microsoft.com/pricing/details/virtual-machines/linux/) ve [Windows VM'ler](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) VM durumları hakkında.

Geliştirme ve test ortamları için daha fazla maliyet kesme özellikleri için kullanıma [Azure DevTest Labs](https://azure.microsoft.com/services/devtest-lab/).

## <a name="cost-reporting"></a>Günü 2 +: Hizmetleri kullandıktan sonra kullanımını görüntüleyin

### <a name="costs"></a>Düzenli olarak Maliyet dökümü için hello portalına bakın ve yazma oranı

Çalışan hizmetlerinizi aldıktan sonra ne kadar bunlar, maliyetlendirme düzenli olarak denetleyin. Merhaba geçerli görebilirsiniz harcamanız ve Azure Portal'da yazma oranı. 

1. Merhaba ziyaret [Azure portalında abonelikleri dikey](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade).

2. Toosee istediğiniz aboneliğinizi seçin. Yalnızca bir tooselect sahip olabilir.

3. Merhaba maliyet dökümünü görmek ve yazma oranı hello açılan dikey penceresinde gerekir. (Bir uyarı hello üstüne yakın görüntülenir) teklifiniz için desteklenmeyebilir. Merhaba veri toopopulate için bir hizmet ekledikten sonra 24 saat bekleyin.
    
    ![Yazma oranını ve çözümleme hello Azure portal'ın ekran görüntüsü](./media/billing-getting-started/burn-rate.PNG)

4. Toopin hello görünüm tooyour Pano isteyebilirsiniz.

    ![Bir görünüm toohello panoya sabitleme işleminin ekran görüntüsü](./media/billing-getting-started/pin.PNG)

5. Tıklatın **analiz maliyetiyle** hello listesi toohello sol toosee hello Maliyet dökümü kaynak tarafından içinde.

    ![Azure portalında hello maliyet analiz görünümünün ekran görüntüsü](./media/billing-getting-started/cost-analysis.PNG)

6. Gibi farklı özelliklere göre filtreleyebilirsiniz [etiketleri](#tags), kaynak grubu ve timespan. Tıklatın **Uygula** tooconfirm hello filtreleri ve **karşıdan** tooexport hello görünüm tooa virgül ile ayrılmış değerler (.csv) dosyası.

7. Bir kaynağa tıklayın toosee harcamanız geçmişi ve ne kadar bu, her gün maliyetlendirme.

    ![Ekran görüntüsü hello harcamanız Azure portalında geçmişini görüntüle](./media/billing-getting-started/costhistory.PNG)

Merhaba Hizmetleri seçildiğinde gördüğünüz hello tahminler gördüğünüz hello maliyetleri denetlemenizi öneririz. Merhaba maliyetleri müthiş bir başarı tahminleri farklıysa, kaynaklarınız için seçtiğiniz (A0 VM, örneğin A1 vs) planı fiyatlandırma hello kontrol edin. 

#### <a name="view-costs-for-all-your-subscriptions-in-hello-billing-blade"></a>Tüm aboneliklerinizi hello faturalama dikey penceresinde görünüm maliyetleri

Hesap Yöneticisi hello gibi birden çok abonelik yönetiyorsanız, hello toplama fatura tutar ve çözümleme, hello tüm abonelikler için gördüğünüz [faturalama dikey penceresine](https://portal.azure.com/#blade/Microsoft_Azure_Billing/BillingBlade). 

<!-- Add screenshots of multiple subs each with billed usage -->

### <a name="turn-on-and-check-out-azure-advisor-recommendations"></a>' Yı açmak ve Azure Advisor önerileri denetleyin

[Azure Danışmanı](../advisor/advisor-overview.md) yardımcı olan bir önizleme özelliği ile düşük kullanımını kaynakları belirleyerek maliyetlerini azaltmak olduğu. Hello Azure portalını açın:

![Azure portalında Azure Danışmanı ekran düğmesi](./media/billing-getting-started/advisor-button.PNG)

Daha sonra hello tıklatılabilir öneriler alabilirsiniz **maliyet** hello Danışmanı Pano sekmesinde:

![Ekran görüntüsü, Advisor maliyet öneri örneği](./media/billing-getting-started/advisor-action.PNG)

Daha fazla bilgi için bkz: [Danışmanı maliyet önerileri](../advisor/advisor-cost-recommendations.md).

### <a name="invoice-and-usage"></a>İlk fatura süre, fatura ve ayrıntı kullanımını Al

İlk fatura süreniz sonra taşınabilir belge biçimi (.pdf) fatura ve virgül ile ayrılmış değerler (.csv) kullanım ayrıntılarını indirebilirsiniz. İçinde toohave faturanızı seçebilirsiniz tooyou e-posta ile. Bu dosyalar, sonuçta Faturalanan tooyou vergi, indirim ve krediler sonra nedir toounderstand yardımcı olur. Ödeme yöntemi bağlı tooyour aboneliğiniz varsa alamadık, bu dosyalar sizin için kullanılamıyor olabilir. Daha fazla bilgi için bkz: [nasıl tooget Azure faturalama fatura ve günlük kullanım verileri](billing-download-azure-invoice-daily-usage-date.md) ve [faturanızı anlamak için Microsoft Azure](billing-understand-your-bill.md).

![.Pdf fatura ekran görüntüsü](./media/billing-getting-started/invoice.png)

daha önce belirlediğiniz hello etiketleri hello ayrıntı kullanım .csv dosyalarını göster:

![Etiketler hello kullanım .csv gösteren ekran görüntüsü](./media/billing-getting-started/csv.png)

### <a name="billing-api"></a>Faturalandırma API’si

Bizim fatura API tooprogrammatically get kullanım verileri kullanın. Merhaba RateCard API ve hello kullanım API'si birlikte tooget Faturalanan kullanımınızı kullanın. Daha fazla bilgi için bkz: [Microsoft Azure kaynak tüketimini Öngörüler elde](billing-usage-rate-card-overview.md).

## <a name="other-offers"></a>EA, CSP ve sponsorluk için ek kaynaklar

Tooyour Hesap Yöneticisi'ni veya Azure iş ortağı tooget başlatılan konuşun.

| Sunduğu | Kaynaklar |
|-------------------------------|-----------------------------------------------------------------------------------|
| Kurumsal Anlaşma (EA) | [EA portal](https://ea.azure.com/), [belgeleri Yardım](https://ea.azure.com/helpdocs), ve [Power BI raporu](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-enterprise/) |
| Bulut Çözümü Sağlayıcısı (CSP) | Konuşma tooyour sağlayıcısı |
| Azure Sponsorluğu | [Sponsorluk portalı](https://www.microsoftazuresponsorships.com/) |

Siz yönetiyorsanız BT büyük bir kuruluş için okuma öneririz [Azure enterprise iskele](../azure-resource-manager/resource-manager-subscription-governance.md) ve hello [kurumsal BT incelemeyi](http://download.microsoft.com/download/F/F/F/FFF60E6C-DBA1-4214-BEFD-3130C340B138/Azure_Onboarding_Guide_for_IT_Organizations_EN_US.pdf) (.pdf indirme, yalnızca İngilizce).

## <a name="need-help-contact-support"></a>Yardım mı gerekiyor? Desteğe başvurun

Yardıma gereksiniminiz varsa [desteğine başvurun](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) sorunu Çözümlendi hızla tooget.
