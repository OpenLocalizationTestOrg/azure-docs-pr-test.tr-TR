---
title: "Veri Kataloğu aaaIntroduction tooAzure | Microsoft Docs"
description: "Bu makalede, Microsoft Azure veri Kataloğu özellikleri ve onu ele hello sorunları da dahil olmak üzere, genel bir bakış sağlar. Veri Kataloğu hiçbir kullanıcı tooregister sağlar, Bul, anlamak ve veri kaynaklarını tüketebilir."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: cc733907-17ec-4153-9f0c-5b3754b2db19
ms.service: data-catalog
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 82144c440b5692d3608af08208f36ee8e6dfdc93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-data-catalog"></a>Azure Veri Kataloğu nedir?
Azure veri Kataloğu, kullanıcıların ihtiyaç duydukları ve buldukları hello veri kaynaklarını anlamasına hello veri kaynakları bulabilmesi için bir tam olarak yönetilen bir bulut hizmetidir. Merhaba aynı zaman, veri Kataloğu yardımcı olan kuruluşlar get var olan yatırımlarından daha fazla değer. 

Veri Kataloğu sayesinde, tüm kullanıcılar (analist, veri bilim insanı veya geliştirici) veri kaynaklarını bulabilir, anlayabilir ve tüketebilir. Veri Kataloğu, meta veriler ve ek açıklamalar için bir kitle kaynağı modelini içerir. Bir tek, merkezi bir kuruluşun kullanıcıları toocontribute tamamı için kendi bilgi yerdir ve yapı topluluğu ve kültürü veri.

## <a name="discovery-challenges-for-data-consumers"></a>Veri tüketicileri için bulma zorlukları
Geleneksel olarak, kurumsal veri kaynaklarının bulunması grupsal bilgilere dayanan organik bir süreç olmuştur. Tooget hello bilgi varlıklarına çoğu değerinden isteyen şirketler için çeşitli zorluklar bu yaklaşım sunulmaktadır:

* Kullanıcılar, başka bir işlem kapsamında denk gelinmediği sürece bir veri kaynağının mevcut olduğundan haberdar olmayabilir. Veri kaynaklarının kayıtlı olduğu merkezi bir konum yoktur.
* Kullanıcıların bir veri kaynağı hello konumu bilmiyorsanız, bir istemci uygulaması kullanarak toohello veri bağlanamıyor. Veri kullanımı deneyimleri, kullanıcıların tooknow hello bağlantı dizesini veya yolunu gerektirir.
* Kullanıcıların bir veri kaynağının belgelerinin hello konumu bilmiyorsanız, bunlar hello veri hello hedeflenen kullanımlarını anlayamamaktadır. Veri kaynakları ve belgeler çeşitli yerlerde bulunabilir ve çeşitli deneyimler aracılığıyla tüketilebilir.
* Kullanıcılar bir bilgi varlığı hakkında sorularınız varsa, bunlar hello uzman veya hello verilerden sorumlu bir ekip bulun ve çevrimdışı göster. Veriler ile bunların nasıl kullanacağına ilişkin uzman görüşleri arasında açık bir bağlantı yoktur.
* Kullanıcıların erişim toohello veri kaynağı isteyen hello işlem anlamadan hello veri kaynağının ve belgelerinin bulunması hala bunları hello veri erişim korumaz.

## <a name="discovery-challenges-for-data-producers"></a>Veri üreticileri için bulma zorlukları
Veri tüketicileri yüz hello daha önce bahsedilen zorluklar rağmen oluşturmaktan ve bilgi varlıklarını koruma için sorumlu olan kullanıcıları kendi güçlüklerle karşılaşır:

* Veri kaynaklarına açıklayıcı meta verilerle ek açıklama ekleme, genellikle sonuç vermeyen bir işlemdir. İstemci uygulamaları genellikle hello veri kaynağında depolanan açıklamaları yok sayar.
* Veri kaynakları için belge oluşturma genellikle sonuç vermeyen bir işlemdir. Belgelerin veri kaynaklarıyla eşitlenmiş halde tutulması sürekli bir sorumluluktur ve kullanıcılar eski olduğunu düşündüğü belgelere güvenmeyebilir.
* Veri kaynaklarına yönelik belgelerin oluşturulması ve bakımının yapılması karmaşık ve zaman alan işlemlerdir. Merhaba veri kaynağını kullanan bu belgeleri kullanıma hazır tooeveryone yaparak daha da olabilir.
* Toodata kaynaklarına erişim kısıtlama ve veri tüketicilerinin nasıl toorequest erişim sürekli karşılaşılan bir zorluktur bilmesinin sağlanması.

Bu tür zorluklar birleştirildiğinde, tooencourage istediğiniz ve hello kullanımını ve anlaşılmasını kurumsal verilerin yükseltin şirketler için ciddi bir engel sunar.

## <a name="azure-data-catalog-can-help"></a>Azure Veri Kataloğu bu konuda yardımcı olabilir
Veri Kataloğu bu sorunları ve toohelp kuruluşların get Merhaba, var olan bilgi varlıklarından en değeri tasarlanmış tooaddress ' dir. Veri Kataloğu veri kaynakları hello verileri yönetmek hello kullanıcılar tarafından kolayca bulunabilir ve anlaşılabilir hale getirir.

Veri Kataloğu, veri kaynağının kaydedilebileceği bulut tabanlı bir hizmet sağlar. Hello veri kalır, ancak kendi meta verilerinin bir kopyasını var olan konumunda tooData Kataloğu, bir başvuru toohello veri kaynağı konumu ile birlikte eklenir. meta veri hello da dizinli toomake her veri arama ve bunları bulan anlaşılabilir toohello kullanıcılar aracılığıyla kolayca bulunabilir kaynağıdır.

Bir veri kaynağı kaydedildikten sonra meta verilerini daha sonra kayıtlı hello kullanıcıyı veya hello kuruluştaki diğer kullanıcılar tarafından zenginleştirilebilir. Herhangi bir kullanıcı, açıklama, etiket veya veri kaynağı erişimi istemeye yönelik belge ve işlemler gibi diğer meta verileri sağlayarak bir veri kaynağına açıklama ekleyebilir. Bu tanımlayıcı meta veriler hello veri kaynağından kaydedilen hello gibi yapısal meta verilerin (sütun adları ve veri türleri için) tamamlar.

Keşfetmek ve veri kaynaklarını ve bunların kullanımını anlamak hello kaynakları kaydı hello birincil amaçtır. Kurumsal kullanıcılar verileri iş zekası, uygulama geliştirme, veri bilimi veya hello doğru verilerin gerekli olduğu başka bir görev için gerekebilir. Bunlar, ihtiyaçlarını karşılayan deneyimi tooquickly bulma verileri hello veri tooevaluate verilerin hello amacına uygunluğunu anlamak ve bunların seçim aracında hello veri kaynağı açarak hello verileri kullanmak hello veri Kataloğu bulma kullanabilirsiniz. 

AT hello aynı zaman, kullanıcılar etiketleme belgeleme ve önceden kaydedilmiş olan veri kaynaklarına açıklama ekleme toohello katalog katkıda. Bunlar da sonra bulunan, anladım ve hello katalog kullanıcıları topluluğu tarafından tüketilen yeni veri kaynaklarını kaydedebilirsiniz.

![Veri Kataloğu özellikleri](./media/data-catalog-what-is-data-catalog/data-catalog-capabilities.png)

## <a name="learn-more-about-data-catalog"></a>Veri Kataloğu hakkında daha fazla bilgi edinin
Veri Kataloğu'nun hello yetenekleri hakkında daha fazla toolearn bakın:

* [Nasıl tooregister veri kaynakları](data-catalog-how-to-register.md)
* [Nasıl toodiscover veri kaynakları](data-catalog-how-to-discover.md)
* [Nasıl tooannotate veri kaynakları](data-catalog-how-to-annotate.md)
* [Nasıl toodocument veri kaynakları](data-catalog-how-to-documentation.md)
* [Nasıl tooconnect toodata kaynakları](data-catalog-how-to-connect.md)
* [Nasıl toowork büyük veri ile](data-catalog-how-to-big-data.md)
* [Nasıl toomanage veri varlıklarını](data-catalog-how-to-manage.md)
* [Nasıl tooset yukarı hello iş sözlüğü](data-catalog-how-to-business-glossary.md)
* [Sık sorulan sorular](data-catalog-frequently-asked-questions.md)

## <a name="next-steps"></a>Sonraki adımlar
Veri Kataloğu ile çalışmaya tooget gidin:
* [Microsoft Azure Veri Kataloğu](https://www.azuredatacatalog.com)
* [Azure Veri Kataloğu ile çalışmaya başlama](data-catalog-get-started.md)
