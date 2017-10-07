---
title: "aaaAzure veri Kataloğu terminolojisi | Microsoft Docs"
description: "Bu makalede, bir giriş tooconcepts ve Azure veri Kataloğu belgelerde kullanılan terimler sağlar."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 6fec74d9-4a3c-4b4b-88ba-cad5ad143331
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: b5f071db4f62c914d2c1cdef9aa686b18d5297d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-terminology"></a>Azure veri Kataloğu terminolojisi
## <a name="catalog"></a>Katalog
Hello Azure veri Kataloğu, veri kaynakları ve veri varlıklarını kaydedilebilir bulut tabanlı meta veri deposudur. Merhaba Kataloğu, veri kaynağından ayıklanan yapısal meta verileri ve kullanıcılar tarafından eklenen açıklayıcı meta verileri için merkezi depolama konumu olarak görev yapar.

## <a name="data-source"></a>Veri kaynağı
Bir veri kaynağı bir sistem veya veri varlıklarını yönetir kapsayıcı ' dir. Örnekler, SQL Server veritabanları, Oracle veritabanları, (tablo veya çok boyutlu) SQL Server Analysis Services veritabanları ve SQL Server Reporting Services sunucuları içerir.

## <a name="data-asset"></a>Veri varlığı
Veri varlıklarını hello Kataloğu ile kayıtlı veri kaynaklarına içindeki nesneleridir. SQL Server tabloları ve görünümleri, Oracle tabloları ve görünümleri, SQL Server Analysis Services ölçüler, boyutlar ve KPI'leri örnekler ve SQL Server Reporting Services raporları.

## <a name="data-asset-location"></a>Veri varlık konumu
Hello katalog depolayan bir veri kaynağı veya kullanılan tooconnect toohello olabilir veri varlığına hello konumunun bir istemci uygulaması kullanarak kaynak. Merhaba biçimi ve hello konumu ayrıntılarını hello veri kaynağı türüne göre değişir. Örneğin, bir SQL Server Raporlama Hizmetleri rapor URL'sini göre tanımlanabilir sırasında bir SQL Server tablo dört bölümü adıyla – sunucu adı, veritabanı adı, şema adı, nesne adı – tanımlanabilir.

## <a name="structural-metadata"></a>Yapısal meta verileri
Yapısal meta verilerin bir veri varlığına hello yapısını açıklayan bir veri kaynağından ayıklanan hello meta verilerdir. Bu, hello varlıklar konumu, nesne adı ve türü ve ek türüne özgü özellikleri içerir. Örneğin, tabloları ve görünümleri için hello yapısal meta verilerin hello adlarını ve hello nesnenin sütunların veri türleri içerir.

## <a name="descriptive-metadata"></a>Açıklayıcı meta verileri
Açıklayıcı meta verileri hello amaç veya bir veri varlığına amacını açıklayan meta veriler oluşturur. Açıklayıcı meta veri Kataloğu kullanıcılar hello Azure veri Kataloğu portalını kullanarak genellikle eklendiği, ancak bunu da hello veri kaynağından kayıt sırasında ayıklanabilir. Örneğin, hello Azure veri Kataloğu kayıt aracı açıklamaları hello açıklama özelliği SQL Server Analysis Services ve SQL Server Reporting Services ve hello ayıklanır [genişletilmiş özellikms_description](https://technet.microsoft.com/library/ms190243.aspx)SQL Server veritabanlarında, bu özellikleri değerlerle doldurulduğunu varsa.

## <a name="request-access"></a>Erişim isteği
Bir veri varlığın açıklayıcı meta verileri nasıl toorequest erişim toohello veri varlık veya veri kaynağı bilgileri içerebilir. Bu bilgiler hello veri varlık konumu ile sunulan ve bir veya daha fazla seçenekleri aşağıdaki hello içerebilir:

* Merhaba kullanıcı veya takım erişim toohello veri kaynağı vermek için sorumlu Hello e-posta adresi.
* hello Hello URL'sini kullanıcılar toogain erişim toohello veri kaynağı izlemelisiniz işlemi açıklanmaktadır.
* kullanılan toogain erişim toohello veri kaynağı olabilecek bir kimlik ve erişim yönetimi aracını (Microsoft Identity Manager gibi) Hello URL'si.
* Kullanıcılar erişimi toohello veri kaynağına nasıl kazanmadan açıklar serbest metin girişi.

## <a name="preview"></a>Önizleme
Azure veri Kataloğu önizlemede kayıt sırasında hello veri kaynağından ayıklanan ve hello veri varlık meta verilerle hello kataloğunda depolanan too20 kayıtları yukarı anlık görüntüsüdür. Merhaba Önizleme yardımcı bir veri varlığına Bul kullanıcıları daha iyi anlamak işlevi ve amacı. Diğer bir deyişle, örnek verileri görmesini yalnızca hello sütun adları ve veri türleri görmesini değerinden daha yararlı olabilir.
Önizleme yalnızca tablo ve görünümler için desteklenir ve kayıt sırasında hello kullanıcı tarafından açıkça seçilmelidir.

## <a name="data-profile"></a>Veri profili
Azure veri Kataloğu veri profilinde kayıt sırasında hello veri kaynağından ayıklanan ve hello veri varlık meta verilerle hello kataloğunda depolanan bir kayıtlı veri varlığını ilgili tablo ve sütun düzeyi meta verilerin bir anlık görüntüdür. Merhaba veri profili yardımcı bir veri varlığına Bul kullanıcıları daha iyi anlamak işlevi ve amacı. Benzer toopreviews, veri profilleri, kayıt sırasında hello kullanıcı tarafından açıkça seçilmelidir.

> [!NOTE]
> Veri profili ayıklanıyor büyük tabloları ve görünümleri için pahalı bir işlem olabilir ve önemli ölçüde artırmak gereken süre tooregister bir veri kaynağı hello.
>
>

## <a name="user-perspective"></a>Kullanıcı perspektifi
Azure veri Kataloğu'nda herhangi bir kullanıcı için bir kayıtlı veri varlığına açıklayıcı meta verileri sağlayabilir. Her kullanıcının ayrı bir perspektif hello veri ve kullanımına vardır. Örneğin, bir sunucu için sorumlu hello Yöneticisi kendi hizmet düzeyi sözleşmesi (SLA) veya yedekleme windows hello Ayrıntılar sağlayabilir; bir veri steward hello verilerinizin desteklediği bağlantılar toodocumentation hello iş için işler sağlayabilir; Ayrıca bir analist en uygun tooother analistleri olan ve toodiscover gerekir ve hello verileri anlamak en değerli toothose kullanıcılar olabilen hello koşullarını açıklamasında sağlayabilir.

Her bu Perspektifleri kendiliğinden değerli ve Azure veri Kataloğu ile her kullanıcının tüm kullanıcılar bu bilgileri toounderstand hello verileri ve amacı kullanabilirsiniz, ancak anlamlı toothem hello bilgileri sağlayabilir.

## <a name="expert"></a>Uzman
Uzman bilinçli "Uzman" bakış açısı için bir veri varlığına sahip olarak belirlenmiştir kullanıcıdır. Herhangi bir kullanıcı, bir varlık için bir uzman olarak kendilerini veya başka bir kullanıcı ekleyebilirsiniz. Uzmanı listelenmiş herhangi bir ek ayrıcalık Azure veri Kataloğu'nda iletmek değil; Kullanıcıların verir tooeasily bir varlığın açıklayıcı meta verileri gözden geçirirken büyük olasılıkla toobe yararlı olan bu Perspektifler bulun.

## <a name="owner"></a>Sahip
Azure veri Kataloğu'ndaki bir veri varlığına yönetmek için ek ayrıcalıklarına sahip bir kullanıcı sahibidir. Kullanıcılar, kayıtlı veri varlıklarının sahipliğini alabilir ve sahipleri ikincil sahip diğer kullanıcılar ekleyebilirsiniz. Daha fazla bilgi için bkz: [nasıl toomanage veri varlıklarını](data-catalog-how-to-manage.md)  

> [!NOTE]
> Sahipliği ve yönetimi, yalnızca hello, Azure veri Kataloğu standart sürümü kullanılabilir.
>
>

## <a name="registration"></a>Kayıt
Kayıt, veri varlık meta veri kaynağından ayıklanacağı ve toohello Azure veri Kataloğu hizmet kopyalama hello işlemidir. Kayıtlı veri varlıklarını sonra açıklama bulunan ve.

## <a name="see-also"></a>Ayrıca bkz.
* [Azure Veri Kataloğu nedir?](data-catalog-what-is-data-catalog.md) -Bu makalede hello Azure veri Kataloğu hizmet, sağladığı hello değeri ve destekliyorsa hello senaryoları genel bakış sağlar.
* [Azure veri Kataloğu ile çalışmaya başlama](data-catalog-get-started.md) -bu makalede nasıl toouse veri kaynağı bulma için Azure veri Kataloğu gösteren bir uçtan uca öğretici sağlar.  
