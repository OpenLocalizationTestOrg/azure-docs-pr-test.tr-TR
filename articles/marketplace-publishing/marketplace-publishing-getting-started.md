---
title: "aaaOverview nasıl toocreate ve bir teklif toohello Market dağıtma | Microsoft Docs"
description: "Merhaba adımları gerekli toobecome onaylanmış bir Microsoft Geliştirici anlamak ve oluşturma ve sanal makine görüntüsünün, şablon, veri hizmeti veya hello Azure Marketi Geliştirici hizmetinde dağıtma"
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 5343bd26-c6e4-4589-85b7-4a2c00bba8ab
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/05/2017
ms.author: hascipio
ms.openlocfilehash: ac5480b98b8b1021a595db951ed9c974f74415dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-and-manage-an-offer-in-hello-azure-marketplace"></a>Yayımlama ve hello Azure Marketi bir teklif yönetme
Bu makalede toohelp geliştiriciler oluşturmak, dağıtmak ve diğer Azure müşterileri ve ortakları toopurchase ve kullanımı için hello Azure Marketi listelenen çözümleri yönetmek sağlanır.

## <a name="marketplace-publishing"></a>Market yayımlama
Bir Azure yayımcı olarak dağıtmak ve yenilikçi çözüm ya da hizmet tooother geliştiriciler, ISV, satış ve BT uzmanları Market hello. Merhaba Market sizinle iletişim kurabileceği tooquickly isteyen müşteriler geliştirmek, bulut tabanlı uygulamalar ve mobil çözümler. Çözümünüzü iş kullanıcıları hedefliyorsa, tooconsider hello isteyebilirsiniz [AppSource](http://appsource.microsoft.com) Market.


## <a name="supported-types-of-solutions"></a>Desteklenen tür çözümler
Merhaba ilk şey, şirketinizin ne tür bir çözüm sunan bir yayımcı toodefine olduğu gibi toodo istiyor. Merhaba Market hello şu tekliflerinden türlerini destekler:

|Çözüm türü|Sanal makine|Çözüm şablonu|
|---|---|---|
|**Tanımı**|Tam olarak yüklenmiş bir işletim sistemi ve bir veya daha fazla uygulama önceden yapılandırılmış görüntülerle. Bir sanal makine görüntüsü hello bilgi gerekli toocreate sağlar ve hello Azure sanal makineler hizmeti içindeki sanal makineler dağıtabilirsiniz.|Bir veya daha fazla farklı Azure Hizmetleri başvurabilir veri yapısı, Hizmetleri dahil olmak üzere diğer satıcılar tarafından yayımladı. Azure aboneleri kullanabilirsiniz toodeploy tek ve eşgüdümlü bir şekilde bir veya daha fazla teklifleri.|
|**Örnek**|Azure bir yayımcı olarak oluşturulabilir ve doğrulanabilir bir yenilikçi veritabanı hizmeti ile bir VM. Diğer Azure aboneleri tooprocure istediğiniz ve bu VM bulut hizmeti ortamlarını dağıtabilirsiniz.|Azure bir yayımcı olarak hızlı toodeploy bulut hizmetleriyle Yük Dengeleme, Gelişmiş Güvenlik ve yüksek kullanılabilirlik sağlamak Azure üzerinden Hizmetleri'nden bir dizi paketlenmiş. Diğer Azure aboneleri kendi hedefi karşılayan hello çözüm şablonu temin etme zamandan tasarruf edebilirsiniz. Bulun, tedarik etmek, dağıtmak ve yapılandırmak toomanually yok hello aynı veya benzer Azure Hizmetleri.|

> [!NOTE]
> Merhaba farklı türlerde çözümleri arasında paylaşılan bazı adımlar ve diğerleri ayrı toohello ilgili çözüm türüdür. Bu makalede kısa bir genel bakış sağlanmaktadır hello adımları herhangi bir çözüm türde toocomplete gerekir.

## <a name="publish-a-solution"></a>Bir çözüm yayımlama
![Belirler, kaydetme, yayımlama](media/marketplace-publishing-getting-started/img01.png)

### <a name="nominate-your-solution-for-pre-approval"></a>Çözümünüz için Ön onay belirler
bir sanal makine toopublish [çözüm](https://createopportunity.azurewebsites.net) toohello Market, tam hello Azure Microsoft Sertifikalı **çözüm Adaylığı Form**.

>[!NOTE]
> Bir iş ortağı Hesap Yöneticisi'ni veya DX ortak Yöneticisi ile çalışıyorsanız, toonominate isteyin çözümünüz hello Azure sertifikalı program için. Toohello de gidebilirsiniz [Azure Microsoft Sertifikalı](http://createopportunity.azurewebsites.net) Web sayfası ve doldururken hello uygulama formu. Hello Hello e-posta ortak hesap yöneticisi veya DX ortak Yöneticisi'ni girin **Microsoft sponsoru kişi** kutusu.

Hello hello uygunluk ölçütleri karşılamıyorsa [Azure Marketi katılım ilkeleri](http://go.microsoft.com/fwlink/?LinkID=526833) ve uygulamanızı onaylanır, biz, çözüm toohello Market, tooonboard ile çalışmaya başlayabilirsiniz.

### <a name="register-your-account-as-a-microsoft-seller"></a>Hesabınızı Microsoft satıcı olarak Kaydet
Microsoft hesabınız olarak kaydetmek bir [Microsoft Developer hesabı](marketplace-publishing-accounts-creation-registration.md).

### <a name="publish-your-solution"></a>Çözümünüzü yayımlama
toopublish çözüm toohello Market, şu adımları izleyin:
1. Merhaba yedeğin gerekliliklerini

    a. Merhaba karşılamak [yedeğin Önkoşullar](marketplace-publishing-pre-requisites.md).

    b. Merhaba karşılamak [VM teknik Önkoşullar](marketplace-publishing-vm-image-creation-prerequisites.md).

    c. Merhaba karşılamak [çözüm şablonu teknik önkoşulları](marketplace-publishing-solution-template-creation-prerequisites.md).

2. Teklifiniz oluşturun.

    a. Oluşturma bir [sanal makine](marketplace-publishing-vm-image-creation.md) sunar.

    b. Oluşturma bir [çözüm şablonu](marketplace-publishing-solution-template-creation.md) sunar.

3. Teklifiniz oluşturma [içerik pazarlama](marketplace-publishing-push-to-staging.md).

4. Teklifiniz hazırlamada sınayın.

    a. VM teklifiniz test [hazırlama](marketplace-publishing-vm-image-test-in-staging.md).

    b. Çözüm şablonu teklifiniz test [hazırlama](marketplace-publishing-solution-template-test-in-staging.md).

5. Teklif toohello dağıtmak [Market](marketplace-publishing-push-to-production.md).


### <a name="create-and-manage-a-virtual-machine-image"></a>Oluşturma ve bir sanal makine görüntüsü yönetme
Oluşturun ve bu kaynakları kullanarak bir VM görüntüsü yönetin:
* Bir VM görüntüsü oluşturma [şirket içi](marketplace-publishing-vm-image-creation-on-premise.md).
* Çalıştıran bir sanal makine oluşturma [Windows hello Azure portal'ın](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Çalıştıran bir sanal makine oluşturma [hello Azure portal'ın Linux](../virtual-machines/linux/quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Sırasında karşılaşılan yaygın sorunları giderme [VHD oluşturma](marketplace-publishing-vm-image-creation-troubleshooting.md).

## <a name="manage-your-solution"></a>Çözümünüzü yönetme
Yardım çözümünüzle kaynakları aşağıdaki hello yönetin:
* [Sanal makine için okuma hello sonrası üretim Kılavuzu sunar](marketplace-publishing-vm-image-post-publishing.md)
* [Bir teklif veya bir SKU yedeğin ayrıntılarını Hello güncelleştir](marketplace-publishing-vm-image-post-publishing.md#update-the-nontechnical-details-of-an-offer-or-a-sku)
* [Güncelleştirme bir teklif ya da bir SKU Hello teknik ayrıntıları](marketplace-publishing-vm-image-post-publishing.md#update-the-technical-details-of-a-sku)
* [Listelenen bir teklif altında yeni bir SKU ekleme](marketplace-publishing-vm-image-post-publishing.md#add-a-new-sku-under-a-listed-offer)
* [Listelenen SKU Hello veri diski sayısı değiştirme](marketplace-publishing-vm-image-post-publishing.md#change-the-data-disk-count-for-a-listed-sku)
* [Market hello listelenen teklifi Sil](marketplace-publishing-vm-image-post-publishing.md)
* [Market hello listelenen SKU Sil](marketplace-publishing-vm-image-post-publishing.md#delete-a-listed-sku-from-the-marketplace)
* [Market hello Hello listelenen SKU geçerli sürümünü silmek](marketplace-publishing-vm-image-post-publishing.md#delete-the-current-version-of-a-listed-sku-from-the-marketplace)
* [Fiyat tooproduction değerleri listeleme hello geri](marketplace-publishing-vm-image-post-publishing.md#revert-the-listing-price-to-production-values)
* [Modeli tooproduction değerlerini faturalama hello geri](marketplace-publishing-vm-image-post-publishing.md#revert-the-billing-model-to-production-values)
* [Listelenen bir SKU toohello üretim değeri Hello görünürlük ayarını geri](marketplace-publishing-vm-image-post-publishing.md#revert-the-visibility-setting-of-a-listed-sku-to-the-production-value)
* [Bulut çözümü sağlayıcısı satıcınızla ıncentive değiştirme](marketplace-publishing-csp-incentive.md)
* [Ödeme raporlama anlama](marketplace-publishing-report-payout.md)
* [Bir yayımcı olarak destek alma](marketplace-publishing-get-publisher-support.md)

## <a name="additional-resources"></a>Ek kaynaklar
[Azure PowerShell ayarlayın](marketplace-publishing-powershell-setup.md)
