---
title: "aaaHow tooData profil veri kaynakları"
description: "Azure veri Kataloğu'nda veri kaynaklarını kaydederek zaman tooinclude tablo ve sütun düzeyi verileri nasıl profilleri ve toouse veri toounderstand veri kaynaklarını nasıl profilleri vurgulama nasıl-tooarticle."
services: data-catalog
documentationcenter: 
author: spelluru
manager: NA
editor: 
tags: 
ms.assetid: 94a8274b-5c9c-4962-a4b1-2fed38a3d919
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/03/2017
ms.author: spelluru
ms.openlocfilehash: 12c9f38501cdaee903d0dcbbdd0b82395f35a187
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="data-profile-data-sources"></a>Veri profili veri kaynakları
## <a name="introduction"></a>Giriş
**Microsoft Azure veri Kataloğu** bir kayıt ve sistemi kurumsal veri kaynakları için bulma görevi gören bir tam olarak yönetilen bir bulut hizmetidir. Diğer bir deyişle, **Azure veri Kataloğu** tüm yardımcı kişilerle ilgili bulmak, anlamak ve veri kaynaklarını kullanmak ve kuruluşların tooget yardımcı olacak daha fazla kendi varolan veriler değeri. Ne zaman bir veri kaynağı kayıtlı ile **Azure veri Kataloğu**, meta verilerini kopyalanır ve hello hizmeti tarafından dizine ancak hello Öykü yok uç.

Merhaba **profil oluşturma verilerini** özelliği **Azure veri Kataloğu** hello veri kataloğunuzu desteklenen veri kaynaklarından inceler ve istatistikleri ve bu verileri hakkında bilgiler toplar. Kolay tooinclude veri varlıklarınız profilini olur. Bir veri varlığına kaydederken seçin **dahil veri profili** hello veri kaynağı kayıt aracında.

## <a name="what-is-data-profiling"></a>Profil oluşturma verilerini nedir
Profil oluşturma verilerini hello veri Kaydedilmekte hello veri kaynağındaki inceler ve istatistikleri ve bu verileri hakkında bilgiler toplar. Veri kaynağı bulma sırasında bu İstatistikler hello veri toosolve hello uygunluğunu iş sorunlarını belirlemenize yardımcı olabilir.

<!-- In [How toodiscover data sources](data-catalog-how-to-discover.md), you learn about **Azure Data Catalog's** extensive search capabilities including searching for data assets that have a profile. See [How tooinclude a data profile when registering a data source](#howto). -->

Merhaba aşağıdaki veri kaynakları profil oluşturma verilerini destekler:

* SQL Server'ın (Azure SQL DB ve Azure SQL Data Warehouse dahil) tabloları ve görünümleri
* Oracle tabloları ve görünümleri
* Teradata tabloları ve görünümleri
* Hive tabloları

Veri varlıklarını kaydetme kullanıcılar yardımcı olduğunda dahil olmak üzere veri profilleri de dahil olmak üzere, veri kaynakları ile ilgili soruları yanıtlayın:

* Bunu iş sorunumu kullanılan toosolve olabilir?
* Merhaba verileri tooparticular standartları veya kalıp uygun mu?
* Bazı hello anormallikleri hello veri kaynağının nelerdir?
* Bu veriler my uygulamasına tümleştirme olası zorluklar nelerdir?

> [!NOTE]
> Verileri bir uygulamaya nasıl tümleşik belgelerine tooan varlık toodescribe de ekleyebilirsiniz. Bkz: [nasıl toodocument veri kaynakları](data-catalog-how-to-documentation.md).
>
>

<a name="howto"/>

## <a name="how-tooinclude-a-data-profile-when-registering-a-data-source"></a>Tooinclude veri nasıl profil data source kaydedilirken
Kolay tooinclude veri kaynağınızın bir profil var. Hello bir veri kaynağını kaydettiğinizde **kayıtlı nesneler toobe** hello veri kaynağı kaydı panelinde aracı, seçin **dahil veri profili**.

![](media/data-catalog-data-profile/data-catalog-register-profile.png)

toolearn tooregister veri kaynaklarını nasıl görürüm hakkında daha fazla bilgi [nasıl tooregister veri kaynakları](data-catalog-how-to-register.md) ve [Azure veri Kataloğu ile çalışmaya başlama](data-catalog-get-started.md).

## <a name="filtering-on-data-assets-that-include-data-profiles"></a>Veri profillerini içeren veri varlıklarını üzerinde filtreleme
Veri profili içeren toodiscover veri varlıklarını içerebilir `has:tableDataProfiles` veya `has:columnsDataProfiles` arama terimleri biri olarak.

> [!NOTE]
> Seçme **dahil veri profili** hello veri kaynağı kayıt aracını tablo ve sütun düzeyi profil bilgilerini içerir. Ancak, hello veri Kataloğu API'si veri varlıklarını toobe eklenen profili bilgileri yalnızca bir kümesi kayıtlı sağlar.
>
>

## <a name="viewing-data-profile-information"></a>Veri profili bilgilerini görüntüleme
Bir profili uygun veri kaynağıyla bulduktan sonra hello veri profili ayrıntıları görüntüleyebilirsiniz. tooview hello veri profili, bir veri varlığına seçip **veri profili** hello veri Kataloğu portalı penceresinde.

![](media/data-catalog-data-profile/data-catalog-view.png)

Bir veri profilinde **Azure veri Kataloğu** tablo ve sütun profil bilgileri de dahil olmak üzere gösterir:

### <a name="object-data-profile"></a>Nesne veri profili
* Satır sayısı
* Tablo boyutu
* Merhaba nesne en son güncelleştirildiği

### <a name="column-data-profile"></a>Sütun veri profili
* Sütun veri türü
* Farklı değerleri sayısı
* NULL değerlere sahip satır sayısı
* Minimum, maksimum, ortalama ve sütun değerleri için standart sapma

## <a name="summary"></a>Özet
Hakkında bilgi kayıtlı veri varlıklarını toohelp hello uygunluğunu hello veri toosolve iş sorunlarını belirlemek ve profil oluşturma verilerini istatistikler sağlar. Açıklama ve veri kaynaklarını belgeleme yanı sıra veri profilleri, verilerinizin daha derin bir anlayış kullanıcılara verebilirsiniz.

## <a name="see-also"></a>Ayrıca Bkz.
* [Nasıl tooregister veri kaynakları](data-catalog-how-to-register.md)
* [Azure Veri Kataloğu ile çalışmaya başlama](data-catalog-get-started.md)
