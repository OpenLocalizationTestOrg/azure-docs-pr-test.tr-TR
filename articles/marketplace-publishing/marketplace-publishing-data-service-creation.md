---
title: "aaaGuide toocreating hello Market için veri hizmeti | Microsoft Docs"
description: "Nasıl toocreate, onaylamak ve dağıtmak için bir veri hizmeti ayrıntılı yönergeler hello üzerinde Azure Market satın alın."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 96194198-6991-43b4-918e-ee337e250339
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: 0220d357ae0ec89e7d4f6399605850e57c646f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="data-service-publishing-guide-for-hello-azure-marketplace"></a>Veri Hizmeti Yayımlama Kılavuzu hello Azure Market
> [!IMPORTANT]
> **Şu anda artık ekleme duyuyoruz herhangi yeni veri hizmeti yayımcılar. Yeni dataservices listesine onaylanmamış.** Bir SaaS iş uygulaması varsa toopublish istediğiniz AppSource hakkında daha fazla bilgi bulabilirsiniz [burada](https://appsource.microsoft.com/partners). Bir Iaas uygulamalar varsa veya Geliştirici hizmeti misiniz Azure Market'te toopublish gibi daha fazla bilgi bulabilirsiniz [burada](https://azure.microsoft.com/marketplace/programs/certified/).
> 
> 

Merhaba adım 1 ' tamamladıktan sonra [hesap oluşturma ve kayıt](marketplace-publishing-accounts-creation-registration.md), biz hello destekli [genel teknik olmayan](marketplace-publishing-pre-requisites.md) ve [teknik gereksinimleri](marketplace-publishing-data-service-creation-prerequisites.md) veri hizmeti Azure Market sunar. Biz, bir veri hizmeti teklif üzerinde hello oluşturmak için hello adımlarda size yol gösterecek artık [yayımlama portalında] [ link-pubportal] hello Azure Marketi için.

## <a name="1----login-toohello-publishing-portal"></a>1.    Oturum açma toohello Yayımlama Portalı.
Çok Git[https://publish.windowsazure.com](https://publish.windowsazure.com.)

**İlk zaman oturum açma tooPublishing için portalı, aynı hesabı ile şirketinizin Seller profil Geliştirici Merkezi'nde kayıtlı hello kullanın.**  (Daha sonra şirketinizin herhangi bir personel hello Yayımlama Portalı'nda bir ortak yönetici olarak ekleyebilirsiniz).

Tıklatın hello üzerinde **veri hizmetleri yayımlama** Bu yayımlama hello portalında ilk oturum hello ise döşeme.

## <a name="2----choose-data-services-in-hello-navigation-menu-on-hello-left-side"></a>2.    Seçin **Veri Hizmetleri** hello yan sol gezinti menüsünde hello.
  ![Çizim](media/marketplace-publishing-data-service-creation/pubportal-main-nav.png)

## <a name="3----create-a-new-data-service"></a>3.    Yeni bir veri hizmeti oluşturma
Merhaba başlığında, yeni veri hizmeti sunmak için doldurun ve hello sağ üzerinde üzerinde "+"'i tıklatın.

  ![Çizim](media/marketplace-publishing-data-service-creation/step-3.png)

## <a name="4----review-hello-sub-menu-under-hello-newly-created-data-service-in-hello-navigation-menu"></a>4.    Gözden geçirme hello alt menüsünde hello altında veri hizmeti hello Gezinti menüsünde Yeni oluşturulmuş.
Tıklatın hello üzerinde **izlenecek** sekmesinde ve toopublish düzgün şekilde hello veri hizmeti Azure Marketi hello tüm gerekli adımları gözden geçirin.

> [!TIP]
> Her zaman hello "İzlenecek" sayfasında hello bağlantılarında tıklatın veya hello sol tarafında hello veri hizmeti teklif'ın alt menüsünde sekmeleri kullanın.
> 
> 

## <a name="5----create-a-new-plan"></a>5.    Yeni bir Plan oluşturun.
### <a name="offers-plans-transactions"></a>, İşlemleri planları sunar.
Her teklif birden çok planına sahip olabilir, ancak en az birine (1) planı olması gerekir. Son kullanıcılar tooyour teklif abone olduğunuzda bunların hello teklif'ın planı biri için abone olun. Her plan nasıl son kullanıcılar tanımlar hizmetinizi mümkün toouse olabilir.

Şu anda Azure Marketi yalnızca aylık abonelik işlem tabanlı model verileri için Destek Hizmetleri, yani son kullanıcılar toohello fiyat hello belirli planının, bunlar abone tooand göre aylık ücret ödemeniz mümkün tooconsume her ay sayısı olacaktır Merhaba planı tarafından tanımlanan işlem.

Genelde, veri hizmeti döndürülecek kayıt sayısı tanımlanan her bir işlem toohello hizmet gönderilen hello sorgusuna dayalı olarak. Merhaba, 100 varsayılandır. İşlem sayısı döndürülen tooeach sorgu kayıt sayısı 100'e bölünmüş ve toohello en yakın tamsayı yuvarlanır.

Azure Market hizmet katmanı sorumluluk toomonitor (ölçüm) sayısı her sorgu tarafından tüketilen işlemleri sayısıdır.

> [!IMPORTANT]
> Merhaba işlem sınırına hello ay sırasında son kullanıcılar kendi aylık abonelik döngüsünün sonuna kadar toouse hello hizmeti devam etmesini engellenir.
> 
> Merhaba işlemleri sınırsız sayıda plan veya hello planlarından birini yapabilirsiniz ancak değil gerekir içerir.
> 
> 

### <a name="create-a-plan"></a>Bir plan oluşturun.
1. Tıklayın **"+"** sonraki toohello "yeni bir plan Ekle".
2. Merhaba seçeneklerden birini seçin: **sınırsız** veya **sınırlı** Bu plan için kullanım.  Tooconsume, sınırlı hareket hello planı hello sayısı ardından sağlarsanız, bir ay içinde izin verir.
   
    ![Çizim](media/marketplace-publishing-data-service-creation/step-5.1.png)  
   
    Portal yayımlama son kullanıcılara hello UI hello planın adı hello ve ayrıca hello markette hizmet tooidentify hello planı tarafından kullanılan kullanılan toocommunicate toohello olacağı "Planı tanımlayıcısı" de önerir. İsterseniz, "Plan tanımlayıcısı" Merhaba değiştirebilirsiniz.
   
   > [!NOTE]
   > Merhaba "Plan tanımlayıcısı" Merhaba her teklif kapsamında benzersiz olmalıdır. Kullanılan sayıda tanımlayıcıları yayımlama Portal planlama hello ilk yayımlama tooproduction ve mümkün toochange olmaz sonra tanımlayıcısı kilitli bu tanımlayıcı hello.
   > 
   > 
3. Tooaccept tercih ettiğiniz'ı tıklatın.
4. Ardından, birkaç ek soruları yeni oluşturulan planınız istenir.
   
    ![Çizim](media/marketplace-publishing-data-service-creation/step-5.2.png)

| Soru | Anlamlı |
| --- | --- |
| **Bu Plan hazır ve kullanılabilir dünya çapında mi?** |Tamamen ücretsiz-in-ücret planı oluşturabilirsiniz. Bu teklif için – yalnızca cihazın hello düşünüyorsanız, "Ücretsiz teklif" Merhaba Market yayımladığınız olduğunu anlamına gelir. Yalnızca biri (az) için ise planı, Merhaba, size bir seçenek toooffer son kullanıcılar toolearn hizmetiniz görece küçük bir aylık işlem sayısı ile ilgili daha fazla bilgi.  Merhaba yanıt "Evet" ise, daha fazla soru istenir. |

> [!NOTE]
> Son kullanıcıların her zaman planları Ücretli toohello yükseltebilirsiniz.
> 
> 

| Soru | Anlamlı |
| --- | --- |
| **Ücretsiz deneme sürümü var mı?** |"Hayır deneme" arasında hiç seçin veya planınız "Bir ay" için bir seçenek toouse verin. Yayımcılar bu seçeneği tooprovide son kullanıcılar hello olasılığı toounderstand hello Merhaba, ücretsiz bir aylık yararlar toouse ister. |

> [!IMPORTANT]
> Ödeme yöntemini kredi kartı ör, Kurumsal Anlaşma kurduysanız son kullanıcılar yalnızca mümkün toopurchase ücretsiz deneme sürümü.
> 
> Merhaba müşteri hello aboneliği iptal başlatılan sürece hello ücretsiz deneme sürümü, bir ay sonra müşteriler hello fiyat hello aboneliğin hello tarih itibariyle şarj Azure Marketi başlar. Özel bildirim toohello son kullanıcılar sağlanacaktır.
> 
> 

| Soru | Anlamlı |
| --- | --- |
| **Bu plan bir promosyon kodu toopurchase gerektiriyor?** |Yayımcılar, "A Promocode" toospecific müşteriler adlı özel bir kod sağlayarak bir seçenek toolimit erişim tootheir hizmet planları vardır. Bu Promocode olan son kullanıcıların mümkün toosubscribe toohello planı olacaktır. "Hayır" seçin, ardından herkes burada hello teklif hello bölgesinden kullanılabilir olduğunu kabul ediyorum, (bkz [Market pazarlama içerik Kılavuzu](marketplace-publishing-push-to-staging.md) daha fazla ayrıntı için) mümkün toosubscribe toothis planı olacaktır. Daha fazla soru istenir. |
| **Ayrıca geçerli promosyon kodu yok herkes bu plandan Gizle?** |Merhaba yanıt toohello önceki sorunun "Evet" Merhaba yayımcı hello hello Market UI görünmesini bu planı kaldırma seçeneği toocompletely sahiptir. Bu anlamına gelir, müşteriler bu plana hello teklif'in ayrıntılar sayfası görmezsiniz. Promocode toopurchase alacak son kullanıcılar, olacaktır mümkün toosubscribe tooit bu promocode kullanarak. |

## <a name="6----create-your-marketplace-marketing-content"></a>6.    İçerik pazarlama, Market oluşturma
Tooprovide bilgileri nasıl gerekli için **pazarlama, fiyatlandırma, destek ve kategorileri** sekmeleri ziyaret edin [Market pazarlama içerik Kılavuzu](marketplace-publishing-push-to-staging.md) hello yayımlanan ortak tooall yapıları olduğu Azure Market.  

## <a name="7----connect-your-offer-tooyour-service-sql-azure-based-or-web-service-based"></a>7.    Teklif tooyour hizmet (SQL tabanlı Azure veya Web tabanlı hizmet) bağlayın.
Tıklatın hello üzerinde **Veri Hizmetleri** alt menüsünde.

Merhaba üst kısmında hello sayfası üzerinde tooprovide hello teklif'ın istenir, **Namespace**.  

  ![Çizim](media/marketplace-publishing-data-service-creation/step-7.png)

Soru aşağıda Hello hello yayımcı yeni oluşturulan tooexpose teklif tooAzure Market nasıl gittiğini tanımlayacaksınız. (Merhaba daha fazla ayrıntı görmek için [Veri Hizmetleri Teknik önkoşul Kılavuzu](marketplace-publishing-data-service-creation-prerequisites.md)).

  ![Çizim](media/marketplace-publishing-data-service-creation/step-7.2.png)

**Yayımlama Hello veritabanı hizmet tabanlı**

Tıklayın **veritabanı**. Sayfa aşağıdaki hello görünür:

  ![Çizim](media/marketplace-publishing-data-service-creation/step-7.3.png)

toocreate CSDL eşleme hello veri kümesi için SQL Azure DB'de hello üzerinde temel:

  ![Çizim](media/marketplace-publishing-data-service-creation/step-7.4.png)

Ve ardından her tablo için

  ![Çizim](media/marketplace-publishing-data-service-creation/step-7.5.png)

  ![Çizim](media/marketplace-publishing-data-service-creation/step-7.6.png)

Web hizmeti

  ![Çizim](media/marketplace-publishing-data-service-creation/step-7.7.png)

> [!IMPORTANT]
> Okuma [var olan eşleme web hizmeti tooOData CSDL aracılığıyla](marketplace-publishing-data-service-creation-odata-mapping.md) ayrıntılı yönergeler ve örnekler CSDL Web hizmeti oluşturmak için.
> 
> 

## <a name="next-steps"></a>Sonraki Adımlar
Veri Hizmeti teklifiniz oluşturduğunuza göre hello hello yönergeleri tamamlandığından emin olmak [Market pazarlama içerik Kılavuzu](marketplace-publishing-push-to-staging.md) İleri çok taşımadan önce[hazırlama,verihizmetitestetme](marketplace-publishing-data-service-test-in-staging.md).

## <a name="see-also"></a>Ayrıca Bkz.
* [Başlarken: Nasıl toopublish bir teklif toohello Azure Market](marketplace-publishing-getting-started.md)
* İçinde anlama ilgileniyorsanız hello genel OData eşleme işlemi ve amacı, bu makalede okuma [veri hizmeti OData eşleme](marketplace-publishing-data-service-creation-odata-mapping.md) tooreview tanımları, yapılar ve yönergeler.
* Öğrenme ve anlama hello belirli düğümler ve bunların parametrelerini ilgileniyorsanız, bu makaleyi okuyun [veri hizmeti OData eşleme düğümleri](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) tanımları ve açıklamalar, örnekler ve kullanım örneği bağlamı.
* Örnekler gözden geçirme ilgileniyorsanız, bu makaleyi okuyun [veri hizmeti OData eşleme örnekler](marketplace-publishing-data-service-creation-odata-mapping-examples.md) toosee örnek kod ve kod sözdizimi ve bağlam anladığınızdan emin olun.

[link-pubportal]:https://publish.windowsazure.com
