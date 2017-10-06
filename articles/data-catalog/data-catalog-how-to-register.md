---
title: "Azure veri Kataloğu'ndaki aaaRegister veri kaynaklarında | Microsoft Docs"
description: "Bu makalede, kayıt sırasında hello meta veri alanları da dahil olmak üzere Azure veri Kataloğu'ndaki tooregister veri kaynaklarında nasıl ayıklanan vurgular."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: bab89906-186f-4d35-9ffd-61b1d903905d
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: efc8a852ddc9fb4bbacc7b0280477bd47814936f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="register-data-sources-in-azure-data-catalog"></a>Azure veri Kataloğu'nda veri kaynaklarını kaydetme
## <a name="introduction"></a>Giriş
Azure veri Kataloğu kayıt ve bulma kurumsal veri kaynakları için bir sistem görevi gören bir tam olarak yönetilen bir bulut hizmetidir. Diğer bir deyişle, Bul, anlamak ve veri kaynaklarını kullanan kişilerin veri Kataloğu yardımcı olur ve daha fazla değer, var olan verilerden alma kuruluşlar yardımcı olur. İlk adım toomaking bir veri kaynağı hello veri Kataloğu aracılığıyla bulunabilirlik tooregister o veri kaynağıdır.

## <a name="register-data-sources"></a>Veri kaynaklarını kaydetme
Kayıt hello veri kaynağından meta verilerin ayıklanması ve bu verileri toohello veri Kataloğu hizmet kopyalama hello işlemidir. Burada o anda bulunduğu ve hello denetimi hello Yöneticiler ve hello geçerli sistem ilkelerini altında kaldığı hello veri kalır.

bir veri kaynağı tooregister hello aşağıdaki:
1. Hello Azure veri Kataloğu portalında hello veri Kataloğu veri kaynağı kayıt aracını başlatın. 
2. İş veya Okul hesabınızla hello aynı oturum Azure Active Directory kimlik toohello Portalı'nda toosign kullanın.
3. Tooregister istediğiniz hello veri kaynağını seçin.

Daha fazla adım adım ayrıntılar için bkz: hello [Azure veri Kataloğu ile çalışmaya başlama](data-catalog-get-started.md) Öğreticisi.

Merhaba veri kaynağı kaydınız sonra hello katalog konumuna izler ve meta verilerini dizinler. Kullanıcıların arama, göz atın ve hello veri kaynağını Bul ve ardından Merhaba uygulaması veya kendi seçtikleri aracını kullanarak kendi konumu tooconnect tooit kullanın.

## <a name="supported-data-sources"></a>Desteklenen veri kaynakları
Şu anda desteklenen veri kaynaklarının listesi için bkz: [veri Kataloğu DSR](data-catalog-dsr.md).

## <a name="structural-metadata"></a>Yapısal meta verileri
Bir veri kaynağını kaydettiğinizde hello kayıt aracı seçtiğiniz hello nesnelerin hello yapısı hakkında bilgi ayıklar. Bu bilgiler başvurulan tooas yapısal meta verilerin olur.

Merhaba veri Bul kullanıcılar bu bilgileri tooconnect toohello nesne hello istemci araçlarında kendi seçtikleri kullanabilmesi için tüm nesneler için bu yapısal meta verilerin hello nesnenin konumunu içerir. Nesne adı ve türü diğer yapısal meta verileri içerir ve öznitelik/sütun adı ve veri türü.

## <a name="descriptive-metadata"></a>Açıklayıcı meta verileri
Ayrıca toohello çekirdek hello veri kaynağından ayıklanan yapısal meta verileri, hello veri kaynağı kayıt aracını açıklayıcı meta verileri ayıklar. SQL Server Analysis Services ve SQL Server Reporting Services için bu hizmetleri tarafından sunulan hello açıklama özellikleri bu meta veriler alınır. SQL Server, hello ms kullanarak sağlanan değerler için\_genişletilmiş özellik açıklama ayıklanır. Oracle veritabanı için hello veri kaynağı kayıt aracını ayıklar hello açıklamaları sütundan hello tüm\_sekmesini\_açıklamaları görünümü.

Merhaba veri kaynağından ayıklanan toplama toohello açıklayıcı meta verilerde, kullanıcıların açıklayıcı meta verileri hello veri kaynağı kayıt aracını kullanarak girebilirsiniz. Kullanıcılar etiketleri ekleyebilir ve Kaydedilmekte hello nesneler için uzmanlar tanımlayabilirsiniz. Tüm bu tanımlayıcı meta veriler toohello veri Kataloğu hizmetinin hello yapısal meta verilerin yanı sıra kopyalanacak.

## <a name="include-previews"></a>Önizlemeler içerir
Varsayılan olarak, yalnızca meta veri kaynakları ve kopyalanan toohello veri Kataloğu hizmet, ancak içerdiği hello verilerin bir örnek görüntülediğinizde, bir veri kaynağı genellikle kolaylaştırılır anlama ayıklanır.

Merhaba veri Kataloğu veri kaynağı kayıt aracını kullanarak, her tablo ve kayıtlı görünüm hello verilerin bir anlık görüntü önizlemesini içerebilir. Kayıt sırasında tooinclude önizlemeleri seçerseniz, her bir tablo ve görünüm too20 kayıtları yukarı hello kayıt aracı içerir. Bu anlık görüntü sonra kopyalanır hello yapısal ve açıklayıcı meta verileri birlikte toohello Kataloğu.

> [!NOTE]
> Çok sayıda sütun geniş tablolarla 20'den az kayıtları kendi Önizleme'de dahil olabilir.
>
>

## <a name="include-data-profiles"></a>Veri profiller içerir
Dahil olmak üzere önizlemeleri veri Kataloğu veri kaynaklarında arama kullanıcılar için değerli bağlamı yalnızca sağlayabilir gibi bir veri profili dahil olmak üzere, daha kolay toounderstand bulunan veri kaynakları yapabilirsiniz.

Merhaba veri Kataloğu veri kaynağı kayıt aracını kullanarak, her bir tablo ve kayıtlı görünüm için bir veri profili içerebilir. Kayıt sırasında veri profili tooinclude seçerseniz, hello kayıt aracı hello veri ilgili toplu istatistikler her tablo ve görünüm içeren dahil olmak üzere:

* Merhaba sayıda satır ve hello nesnesindeki hello verilerin boyutu.
* Merhaba veri ve hello nesne şemasının hello en son güncelleştirme tarihi Hello.
* boş kayıtlar ve sütunlar için farklı değerler Hello sayısı.
* Merhaba minimum, maksimum, ortalama ve standart sapma değerler sütunlar için.

Bu istatistikler sonra kopyalanır hello yapısal ve açıklayıcı meta verileri birlikte toohello Kataloğu.

> [!NOTE]
> Metin ve tarih sütunlarını ortalama veya standart sapma istatistikleri kendi veri profili dahil etmeyin.
>
>

## <a name="update-registrations"></a>Güncelleştirme kayıtları
Merhaba meta verileri ve isteğe bağlı Önizleme kayıt sırasında ayıklanan kullandığınızda bir veri kaynağı kaydetme veri Kataloğu'nda bulunabilir kolaylaştırır. Merhaba veri kaynağı (örneğin, bir nesnenin hello şema değişti, başlangıçta dışlanan tablolar dahil, veya hello önizlemelerde dahil tooupdate hello veri istiyorsanız) hello kataloğunda güncelleştirilmiş toobe gerekiyorsa hello veri kaynağı kayıt aracını yeniden çalıştırılabilir.

Zaten kayıtlı veri kaynağı yeniden kaydetme birleştirme "upsert" işlemi gerçekleştirir: var olan nesneleri güncelleştirilir ve yeni nesneler oluşturulur. Merhaba veri Kataloğu portalı yoluyla kullanıcılar tarafından sağlanan herhangi bir meta veri korunur.

## <a name="summary"></a>Özet
Yapısal ve açıklayıcı meta verilerini bir veri kaynağı toohello Kataloğu hizmetinden kopyaladığı için veri Kataloğu'nda hello veri kaynağı kaydetme hello veri daha kolay toodiscover yapar ve anlayın. Merhaba veri kaynağı kaydettikten sonra açıklama, yönetmek ve hello veri Kataloğu portalını kullanarak keşfedin.

## <a name="next-steps"></a>Sonraki adımlar
Veri kaynaklarını kaydetme hakkında daha fazla bilgi için bkz: Merhaba [Azure veri Kataloğu ile çalışmaya başlama](data-catalog-get-started.md) Öğreticisi.
