---
title: "Beklenmeyen maliyetleri önlemek için faturalama - Azure yönetme | Microsoft Docs"
description: "Azure faturasını üzerinde beklenmeyen ücretlerden kaçınmak öğrenin. Microsoft Azure aboneliği için maliyet izleme ve yönetim özelliklerini kullanabilirsiniz."
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
ms.openlocfilehash: 5f9ae830da86a9d03f6d862d4adc7c99849d5014
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="prevent-unexpected-costs-with-azure-billing-and-cost-management"></a>Azure faturalama ve maliyet yönetimi ile beklenmeyen maliyetleri engelle

Azure için kaydolduğunuzda, harcama iyi bir fikir almak için yapabileceğiniz birkaç işlem vardır. İçinde [Azure portal](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade), abonelik seçtiğinizde, geçerli maliyet dökümünü görmek ve yazma oranı. Ayrıca [indirme faturaları ve ayrıntılı kullanım dosyalar](billing-download-azure-invoice-daily-usage-date.md). Farklı projelere veya gruplar için kullanılan kaynaklar için Grup maliyetleri istiyorsanız bakmak [kaynak etiketleme](../azure-resource-manager/resource-group-using-tags.md). Kuruluşunuzda kullanmak için tercih ettiğiniz bir raporlama sistemi varsa kullanıma [API'leri faturalama](billing-usage-rate-card-overview.md). 

Günlük kullanımı hakkında daha fazla bilgi için bkz: [faturanızı anlamak için Microsoft Azure](billing-understand-your-bill.md).

Aboneliğinizi bir Kurumsal Anlaşma (Kurumsal Sözleşme), bulut çözümü sağlayıcısı (CSP) veya Azure sponsorluk ise, bu makalede birçok özellik sizin için geçerli değil. Bunun yerine, farklı bir maliyet yönetimi için kullanabileceğiniz araçlar kümesi vardır. Bkz: [EA, CSP ve sponsorluk için ek kaynaklar](#other-offers).

Aboneliğinizin ücretsiz bir deneme ise [Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/), açık (AIO) ya da BizSpark, Azure hakkında bilgi edinin [harcama limitlerini](#spending-limit) unexpectantly devre dışı aboneliğiniz zorunda kalmamak için. 

## <a name="day-0-before-you-add-azure-services"></a>0. gün: Azure Hizmetleri, Ekle

### <a name="estimate-cost-online-using-the-pricing-calculator"></a>Çevrimiçi fiyatlandırma hesaplayıcısı kullanma maliyetini tahmin etmek

Kullanıma [fiyatlandırma hesaplayıcısı](https://azure.microsoft.com/pricing/calculator/) ve [toplam sahip olma hesaplayıcı maliyeti](https://aka.ms/azure-tco-calculator) , ilgilendiğiniz hizmetinin aylık ücreti kestirmek için. Örneğin, tüm zaman çalışmasını bırakırsanız $66.96 ABD Doları/ay işlem saat cinsinden maliyet A1 Windows sanal makine (VM) tahmini:

![Fiyatlandırma hesaplayıcısı A1 Windows VM başına ay $66.96 ABD Doları maliyet tahmini olduğunu gösteren ekran görüntüsü](./media/billing-getting-started/pricing-calcVM.png)

Daha fazla bilgi için bkz: [fiyatlandırma hakkında SSS](https://azure.microsoft.com/pricing/faq/). Veya bir kişinin iletişim kurabilecek şekilde 1-800-867-1389 çağırır.

### <a name="check-your-subscription-and-access"></a>Abonelik ve erişim denetimi

Görüntüleme maliyetleri gerektiren [fatura bilgilerine abonelik düzeyinde erişim](billing-manage-access.md), ancak yalnızca Hesap Yöneticisi erişebilirsiniz [hesap Merkezi'nde](https://account.windowsazure.com/Home/Index)faturalama bilgileri değiştirme ve abonelikleri yönetme. Hesap Yöneticisi kaydolma işlemine geçmeden kullanıcıdır. Daha fazla bilgi için bkz: [abonelik ya da hizmetleri yönetmek ekleme veya değiştirme Azure yönetici rolleri](billing-add-change-azure-subscription-administrator.md).

Hesap Yöneticisi olup olmadığınızı görmek için Git [Azure portalında abonelikleri dikey](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) erişiminiz Aboneliklerin listesini bakın. Kısmına bakın **My rol**. Bunu diyorsa *Hesap Yöneticisi*, Tamam sonra. Gibi başka bir şey diyorsa *sahibi*, sonra da tam ayrıcalığa sahip değilsiniz.

![Azure portalında abonelikleri görünümünde rolünüze ekran görüntüsü](./media/billing-getting-started/sub-blade-view.PNG)

Hesap Yöneticisi değilseniz sonra birisi aracılığıyla kısmi erişim büyük olasılıkla verdiğiniz [Azure Active Directory rol tabanlı erişim denetimi](../active-directory/role-based-access-control-configure.md) (RBAC). Abonelikler ve değişiklik bilgileri, fatura yönetmek için [Hesap Yöneticisi Bul](billing-subscription-transfer.md#whoisaa) ve görevleri gerçekleştirmesini isteyin veya [abonelik için aktarım](billing-subscription-transfer.md).

Hesap yöneticiniz artık, kuruluşunuz ve fatura, yönetmeniz gereken [desteğine başvurun](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade). 

### <a name="spending-limit"></a>Bir harcama sınırına sahip olmadığını denetleyin

Krediler kullanan bir aboneliğiniz varsa, ardından harcama sınırını sizin için varsayılan olarak açıktır. Tüm kredinizi, harcadığı zaman bu şekilde, kredi kartınızdan ücret değil. Bkz: [Azure teklifleri harcama sınırı, kullanılabilirlik ve tam listesi](https://azure.microsoft.com/support/legal/offer-details/).

Ancak, harcama limitine ulaştı, hizmetlerinizi devre dışı. Vm'leriniz serbest anlamına gelir. Bir hizmet kesintisi kaçınmak için harcama sınırı kapatmanız gerekir. Aşmalar üzerine dosyada kredi kartınızdan ücret. 

Üzerinde harcama sınırı var olmadığını görmek için Git [abonelikleri görmek hesap Merkezi'nde](https://account.windowsazure.com/Subscriptions). Harcama sınırınızı açıksa bir başlığın görünür:

![Harcama sınırı üzerinde hesap Merkezi'nde olan hakkında bir uyarı gösteren ekran görüntüsü](./media/billing-getting-started/spending-limit-banner.PNG)

Başlık tıklayın ve harcama sınırını kaldırmak için istemleri izleyin. Kaydolurken kredi kartı bilgilerini girmediyseniz, harcama sınırını kaldırmak için girmeniz gerekir. Daha fazla bilgi için bkz: [Azure harcama sınırını – nasıl çalıştığını ve etkinleştirmek veya kaldırmak nasıl](https://azure.microsoft.com/pricing/spending-limits/).

### <a name="set-up-billing-alerts"></a>Fatura uyarılarını ayarlama

Kullanım maliyetleriniz belirttiğiniz bir miktar aştıklarında e-postaları almak için fatura Uyarıları ayarlayın. Aylık kredilerin varsa, belirtilen tutarı oluşturan kullandığınızda için uyarıları ayarlama. Daha fazla bilgi için bkz: [uyarılar, Microsoft Azure abonelikleri için ödeme yukarı ayarlamak](billing-set-up-alerts.md).

![Fatura bir uyarı e-posta ekran görüntüsü](./media/billing-getting-started/billing-alert.png)

> [!NOTE]
> Bu özellik hala önizlemede olduğundan kullanımınızı düzenli olarak denetlemeniz gerekir.

Fiyatlandırma hesaplayıcısı gelen maliyetini tahmin ilk uyarı için bir kılavuz olarak kullanmak isteyebilirsiniz.

### <a name="understand-limits-and-quotas-for-your-subscription"></a>Sınırları ve kotalar aboneliğiniz için anlama

Her abonelik için CPU çekirdek sayısı ve IP adresleri gibi şeyler için varsayılan sınır vardır. Bu sınırları dikkatli olun. Daha fazla bilgi için bkz: [Azure aboneliği ve hizmet sınırları, kotaları ve kısıtlamaları](../azure-subscription-service-limits.md). Sınırı veya göre kota artışı isteyebilir [Destek](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).

## <a name="day-1-as-you-add-services"></a>1. güne: Hizmetleri ekledikçe

### <a name="review-the-estimated-cost-in-the-portal"></a>Tahmini maliyet portalında gözden geçirin

Genellikle Azure portalında bir hizmet eklediğinizde, benzer bir tahmini maliyet aylık gösteren bir görünüm yok. Örneğin, Windows VM boyutu seçtiğinizde işlem saatleri için tahmini aylık maliyeti bakın:

![Örnek: her ay $66.96 ABD Doları maliyet A1 Windows VM tahmini](./media/billing-getting-started/vm-size-cost.PNG)

### <a name="tags"></a>Faturalama verileriniz gruplandırmak için kaynaklarınıza etiketler ekleme

Desteklenen hizmetler için fatura verileri gruplandırmak için etiketleri kullanabilirsiniz. Birkaç VM'ler farklı ekipler için çalıştırırsanız, örneğin, daha sonra etiketleri maliyetleri maliyet merkezi (HR, pazarlama, Finans) ya da ortam (üretim, üretim öncesi test) tarafından kategorilere ayırmak için kullanabilirsiniz. 

![Portalda etiketleri ayarlama gösteren ekran görüntüsü](./media/billing-getting-started/tags.PNG)

Görünümleri raporlama farklı maliyet etiketler gösterilir. Örneğin, görünür, [analiz görünümü maliyet](#costs) hemen ve [kullanım .csv ayrıntı](#invoice-and-usage) ilk fatura süreniz sonra.

Daha fazla bilgi için bkz: [etiketleri kullanarak Azure kaynaklarınızı düzenleme](../azure-resource-manager/resource-group-using-tags.md).

### <a name="consider-enabling-cost-cutting-features-like-auto-shutdown-for-vms"></a>VM'ler için otomatik kapatma gibi maliyet kesme özellikleri etkinleştirmeyi düşünün

Senaryonuza bağlı olarak, Azure portalında Vm'leriniz için otomatik kapatma yapılandırabilirsiniz. Daha fazla bilgi için bkz: [Azure Kaynak Yöneticisi'ni kullanarak sanal makineleri için otomatik kapatma](https://azure.microsoft.com/blog/announcing-auto-shutdown-for-vms-using-azure-resource-manager/).

![Portal otomatik kapatma seçeneğinin ekran görüntüsü](./media/billing-getting-started/auto-shutdown.PNG)

Otomatik kapatma zaman güç seçenekleri ile VM dahilinde kapattığınız ile aynı değil. Otomatik kapatma durdurur ve ek kullanım ücretleri durdurmak için sanal makineleri kaldırır. Fiyatlandırma hakkında SSS için daha fazla bilgi için bkz: [Linux VM'ler](https://azure.microsoft.com/pricing/details/virtual-machines/linux/) ve [Windows VM'ler](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) VM durumları hakkında.

Geliştirme ve test ortamları için daha fazla maliyet kesme özellikleri için kullanıma [Azure DevTest Labs](https://azure.microsoft.com/services/devtest-lab/).

## <a name="cost-reporting"></a>Günü 2 +: Hizmetleri kullandıktan sonra kullanımını görüntüleyin

### <a name="costs"></a>Düzenli olarak Maliyet Dökümü portal denetleyin ve yazma oranı

Çalışan hizmetlerinizi aldıktan sonra ne kadar bunlar, maliyetlendirme düzenli olarak denetleyin. Geçerli harcama görebilir ve Azure Portal'da yazma oranı. 

1. Ziyaret [Azure portalında abonelikleri dikey](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade).

2. Görmek istediğiniz aboneliğinizi seçin. Yalnızca birini seçmek için olabilir.

3. Maliyet dökümü bakın ve açılan dikey penceresinde yazma oranı. (Bir uyarı en üstüne yakın görüntülenir) teklifiniz için desteklenmeyebilir. Verilerin doldurmak bir hizmet ekledikten sonra 24 saat bekleyin.
    
    ![Yazma oranını ve çözümleme Azure portalında ekran görüntüsü](./media/billing-getting-started/burn-rate.PNG)

4. Görünüm panonuza sabitlemek istediğiniz.

    ![Bir görünüm panoya sabitleme işleminin ekran görüntüsü](./media/billing-getting-started/pin.PNG)

5. Tıklatın **analiz maliyetiyle** kaynak tarafından Maliyet dökümü görmek için sola listesinde.

    ![Azure portalında maliyet analiz görünümünün ekran görüntüsü](./media/billing-getting-started/cost-analysis.PNG)

6. Gibi farklı özelliklere göre filtreleyebilirsiniz [etiketleri](#tags), kaynak grubu ve timespan. Tıklatın **Uygula** filtreleri onaylamak için ve **karşıdan** görünümü bir virgül ile ayrılmış değerler (.csv) dosyasına aktarmak için.

7. Bir kaynağı görmek için tıklatın geçmişi ve ne kadar bu, her gün maliyetlendirme harcamanız.

    ![Azure portalında harcama geçmiş görünümünün ekran görüntüsü](./media/billing-getting-started/costhistory.PNG)

Hizmetleri seçildiğinde gördüğünüz tahminler gördüğünüz maliyetleri denetlemenizi öneririz. Maliyetleri müthiş bir başarı tahminleri farklıysa, kaynaklarınız için seçtiğiniz fiyatlandırma planı (A0 VM, örneğin A1 vs) kontrol edin. 

#### <a name="view-costs-for-all-your-subscriptions-in-the-billing-blade"></a>Faturalama dikey penceresinde tüm aboneliklerinizi görünüm maliyetleri

Birden çok aboneliğiniz Hesap Yöneticisi yönetiyorsanız, çözümleme ve birleşik Fatura miktarı, tüm abonelikler için gördüğünüz [faturalama dikey penceresine](https://portal.azure.com/#blade/Microsoft_Azure_Billing/BillingBlade). 

<!-- Add screenshots of multiple subs each with billed usage -->

### <a name="turn-on-and-check-out-azure-advisor-recommendations"></a>' Yı açmak ve Azure Advisor önerileri denetleyin

[Azure Danışmanı](../advisor/advisor-overview.md) yardımcı olan bir önizleme özelliği ile düşük kullanımını kaynakları belirleyerek maliyetlerini azaltmak olduğu. Azure portalında açın:

![Azure portalında Azure Danışmanı ekran düğmesi](./media/billing-getting-started/advisor-button.PNG)

Ardından, işlem yapılabilir önerileri alabileceğiniz **maliyet** Danışmanı Pano sekmesinde:

![Ekran görüntüsü, Advisor maliyet öneri örneği](./media/billing-getting-started/advisor-action.PNG)

Daha fazla bilgi için bkz: [Danışmanı maliyet önerileri](../advisor/advisor-cost-recommendations.md).

### <a name="invoice-and-usage"></a>İlk fatura süre, fatura ve ayrıntı kullanımını Al

İlk fatura süreniz sonra taşınabilir belge biçimi (.pdf) fatura ve virgül ile ayrılmış değerler (.csv) kullanım ayrıntılarını indirebilirsiniz. Ayrıca, size e-posta ile faturanızı olmasını tercih edebilirsiniz. Bu dosyaları ne Sonuçta, vergi, indirim ve krediler sonra faturalandırılır anlamanıza yardımcı olur. Aboneliğinize bağlı bir ödeme yöntemi varsa alamadık, bu dosyaları için kullanılamıyor olabilir. Daha fazla bilgi için bkz: [faturayı ve günlük kullanım verileri faturalama Azure alma](billing-download-azure-invoice-daily-usage-date.md) ve [faturanızı anlamak için Microsoft Azure](billing-understand-your-bill.md).

![.Pdf fatura ekran görüntüsü](./media/billing-getting-started/invoice.png)

Daha önce belirlediğiniz etiketleri ayrıntısı kullanım .csv dosyaları göster:

![Etiketleri içinde kullanım .csv gösteren ekran görüntüsü](./media/billing-getting-started/csv.png)

### <a name="billing-api"></a>Faturalandırma API’si

Program aracılığıyla kullanım verilerini almak için fatura API'mize kullanın. RateCard API ve kullanım API'si Faturalanan kullanımınızı almak için birlikte kullanın. Daha fazla bilgi için bkz: [Microsoft Azure kaynak tüketimini Öngörüler elde](billing-usage-rate-card-overview.md).

## <a name="other-offers"></a>EA, CSP ve sponsorluk için ek kaynaklar

Başlamak için Hesap Yöneticisi'ni veya Azure iş ortağı konuşun.

| Sunduğu | Kaynaklar |
|-------------------------------|-----------------------------------------------------------------------------------|
| Kurumsal Anlaşma (EA) | [EA portal](https://ea.azure.com/), [belgeleri Yardım](https://ea.azure.com/helpdocs), ve [Power BI raporu](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-enterprise/) |
| Bulut Çözümü Sağlayıcısı (CSP) | Sağlayıcınıza konuşun |
| Azure Sponsorluğu | [Sponsorluk portalı](https://www.microsoftazuresponsorships.com/) |

Siz yönetiyorsanız BT büyük bir kuruluş için okuma öneririz [Azure enterprise iskele](../azure-resource-manager/resource-manager-subscription-governance.md) ve [kurumsal BT incelemeyi](http://download.microsoft.com/download/F/F/F/FFF60E6C-DBA1-4214-BEFD-3130C340B138/Azure_Onboarding_Guide_for_IT_Organizations_EN_US.pdf) (.pdf indirme, yalnızca İngilizce).

## <a name="need-help-contact-support"></a>Yardım mı gerekiyor? Desteğe başvurun

Yardıma gereksiniminiz varsa [desteğine başvurun](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) hızla çözümlenen sorunu almak için.
