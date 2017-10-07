---
title: "aaaGuide toocreating hello Market için bir çözüm şablonu | Microsoft Docs"
description: "Nasıl toocreate, onaylamak ve hello Azure Marketi satınalma için çoklu VM görüntü çözüm şablon dağıtma ayrıntılı yönergeler için."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: e14e05f2-2385-4ce0-b351-0747cb74ba19
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: b0e7067176337dd0d3f6f6ec04c963f80f706ab0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="guide-toocreate-a-solution-template-for-azure-marketplace"></a>Kılavuzu toocreate Azure Market'ten bir çözüm şablonu
Adım 1 ' tamamladıktan sonra [hesap oluşturma ve kayıt][link-acct-creation], size bir Azure uyumlu çözüm şablon hello oluşturulmasını üzerinde destekli [oluşturmak için teknik Önkoşullar bir Çözüm şablonu](marketplace-publishing-solution-template-creation-prerequisites.md). Biz, hello birden çok sanal makine için bir çözüm şablonu oluşturmak için hello adımlarda size yol gösterecek artık [yayımlama portalında] [ link-pubportal] hello Azure Marketi için.

## <a name="create-your-solution-template-offer-in-hello-publishing-portal"></a>Çözüm şablonu teklifiniz hello yayımlama Portal oluşturma
Çok Git [https://publish.windowsazure.com](http://publish.windowsazure.com). Merhaba ilk zaman toohello için oturum açarken [yayımlama portalında](https://publish.windowsazure.com/), aynı hesabı, şirketinizin satıcı profili kaydedildiği ile kullanım hello. Daha sonra şirketinizin herhangi bir personel hello Yayımlama Portalı'nda bir ortak yönetici olarak ekleyebilirsiniz.

### <a name="1-select-solution-templates"></a>1. "Çözüm şablonları" seçin
  ![Çizim][img-pubportal-menu-sol-templ]

### <a name="2-create-a-new-solution-template"></a>2. Yeni bir çözüm şablonu oluşturun
  ![Çizim][img-pubportal-sol-templ-new]

### <a name="3-start-with-topologies"></a>3. Topolojileri ile Başlat
Bir çözüm şablonu "üst" tooall topolojileri olur. Bir teklif/çözüm şablonunda birden fazla topoloji tanımlayabilirsiniz. Bir teklif toostaging gönderildiğinde tüm topolojileri ile gönderilir. Teklifiniz toodefine Hello adımları izleyin:     

* Bir topoloji oluşturun: "Topolojisi tanımlayıcısı" adıdır genellikle hello hello topoloji hello çözüm şablonu için. Merhaba topolojisi tanımlayıcısı hello URL'de aşağıda gösterildiği gibi kullanılır:

  Azure Market: http://azure.microsoft.com/marketplace/partners/ {PublisherNamespace} / {OfferIdentifier} {TopologyIdentifier}

  Azure Portal: https://portal.azure.com/#gallery/ {PublisherNamespace}. {OfferIdentifier} {TopologyIdentifier}
* Yeni bir sürüm ekleyin.

### <a name="4-get-your-topology-versions-certified"></a>4. Sertifikalı topoloji sürümlerinizi Al
Tüm gerekli dosyaları tooprovision hello topoloji belirli bu sürümünü içeren bir zip dosyasını karşıya yükleyin. Bu zip dosyası hello şunları içermelidir:

* *mainTemplate.json* ve *createUiDefinition.json* dosyasını kendi kök dizininde.
* Tüm bağlı şablonları ve gerekli tüm betikler.

  > [!TIP]
  > Geliştiricilerinize hello çözüm şablonu topolojileri oluşturmak ve bunları sertifikalı, hello iş alma üzerinde çalışırken pazarlama ve/veya yasal Departmanlar şirketinizin hello pazarlama ve yasal içerik üzerinde çalışabilir.
  >
  >

## <a name="next-steps"></a>Sonraki adımlar
Çözüm şablonu oluşturduğunuz ve hello zip dosyası karşıya göre Lütfen hello hello yönergeleri izleyin [Market pazarlama içerik Kılavuzu](marketplace-publishing-push-to-staging.md) hello teklif toostaging Ftp'den önce. toosee Market makaleler, yayımlama hello tam kümesi ziyaret [Başlarken: nasıl toopublish bir teklif toohello Azure Marketi](marketplace-publishing-getting-started.md).

Bu ilgili makalelerde ilginizi çekebilir:

* VM görüntüleri: [azure'da sanal makine görüntülerini hakkında](https://msdn.microsoft.com/library/azure/dn790290.aspx)
* VM uzantıları: [VM aracısı ve VM uzantılarına genel bakış](https://msdn.microsoft.com/library/azure/dn832621.aspx) ve [Azure VM uzantıları ve özellikleri](https://msdn.microsoft.com/library/azure/dn606311.aspx)
* Azure Kaynak Yöneticisi: [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md) ve [basit bir şablon örnekleri](https://github.com/rjmax/ArmExamples)
* Depolama hesabı kısıtlar: [nasıl tooMonitor depolama hesabı daraltması](http://blogs.msdn.com/b/mast/archive/2014/08/02/how-to-monitor-for-storage-account-throttling.aspx) ve [Premium depolama](../storage/common/storage-premium-storage.md#scalability-and-performance-targets)

[img-pubportal-menu-sol-templ]:media/marketplace-publishing-solution-template-creation/pubportal-menu-solution-templates.png
[img-pubportal-sol-templ-new]:media/marketplace-publishing-solution-template-creation/pubportal-solution-template-new.png
[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
[link-pubportal]:https://publish.windowsazure.com
