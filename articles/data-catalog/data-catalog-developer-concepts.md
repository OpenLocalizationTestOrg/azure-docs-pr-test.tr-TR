---
title: "aaaData katalog Geliştirici kavramları | Microsoft Docs"
description: "Başlangıç kataloğu REST API'si aracılığıyla sunulan olarak Azure veri Kataloğu kavramsal modelde giriş toohello önemli kavramlar."
services: data-catalog
documentationcenter: 
author: spelluru
manager: jhubbard
editor: 
tags: 
ms.assetid: 89de9137-a0a4-40d1-9f8d-625acad31619
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/03/2017
ms.author: spelluru
ms.openlocfilehash: d0b1628ff6c31458cb650efef852244f0c139b1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-developer-concepts"></a>Azure veri Kataloğu Geliştirici kavramları
Microsoft **Azure veri Kataloğu** kitle kaynak veri kaynağı meta verilerini ve veri kaynağı bulma için özellikleri sağlayan bir tam olarak yönetilen bir bulut hizmetidir. Geliştiriciler kendi REST API'leri aracılığıyla hello hizmetini kullanabilirsiniz. Merhaba hizmetinde uygulanan hello kavramlarını anlama toosuccessfully tümleştirme ile geliştiricilere yönelik önemli **Azure veri Kataloğu**.

## <a name="key-concepts"></a>Önemli kavramlar
Merhaba **Azure veri Kataloğu** kavramsal model dört temel kavramları hakkında temel: Merhaba **katalog**, **kullanıcılar**, **varlıklar**ve **Ek açıklamaları**.

![Kavram][1]

*Şekil 1 - Azure veri Kataloğu Basitleştirilmiş kavramsal model*

### <a name="catalog"></a>Katalog
A **katalog** tüm kuruluş depolar meta verileri hello hello en üst düzey kapsayıcısı aranır. Bir **katalog** Azure hesap başına izin verilen. Katalog bağlı tooan ancak yalnızca bir Azure aboneliği olan **katalog** herhangi belirli Azure hesabı için bir hesap birden fazla abonelik olabilir olsa da oluşturulabilir.

Bir katalog içeren **kullanıcılar** ve **varlıklar**.

### <a name="users"></a>Kullanıcılar
Kullanıcılardır izinleri tooperform Eylemler sahip güvenlik sorumlularının (arama hello Kataloğu, eklemek, düzenlemek veya kaldırmak öğeleri, vb.) hello katalog içinde.

Bir kullanıcı sahip birçok farklı rol vardır. Merhaba bölüm rolleri ve yetkilendirme rolleri hakkında daha fazla bilgi için bkz.

Tek tek kullanıcılar ve güvenlik grupları eklenebilir.

Azure veri Kataloğu, kimlik ve erişim yönetimi için Azure Active Directory kullanır. Her bir katalog kullanıcı hello Active Directory hello hesabının bir üyesi olması gerekir.

### <a name="assets"></a>Varlıklar
A **katalog** veri varlıklarını içerir. **Varlıklar** hello birim hello Kataloğu tarafından yönetilen ayrıntı şunlardır.

bir varlık Hello kesinliği veri kaynağına göre değişir. SQL Server ya da Oracle veritabanı için bir varlık bir tablo veya görünüm olabilir. SQL Server Analysis Services için bir varlık, bir ölçü, boyut veya bir ana performans göstergesi (KPI) olabilir. SQL Server Raporlama Hizmetleri için bir varlık bir rapordur.

Bir **varlık** Kataloğu'ndan ekleyip hello şeydir. Bu, geri alma gelen sonucunun hello birimdir **arama**.

Bir **varlık** adı, konumu ve türü ve daha fazla açıklayan ek açıklamaları oluşur.

### <a name="annotations"></a>Ek Açıklamalar
Ek açıklamalar meta veri varlıkları hakkında gösteren öğelerdir.

Örnek açıklamalarının açıklama, etiketler, şema, belge, vb. verilebilir. Merhaba varlık nesne modeli bölümü hello varlık türleri ve ek açıklama türlerinin tam listesi var.

## <a name="crowdsourcing-annotations-and-user-perspective-multiplicity-of-opinion"></a>Kitle kaynak ek açıklamalar ve kullanıcı perspektifinden (fikir çokluğu)
Bir anahtar Azure veri kataloğu nasıl hello sistemde hello kitle kaynak meta verilerin desteklediği yönüdür. Karşılıklı tooa wiki yaklaşımı olarak – burada yalnızca bir olduğundan fikir ve hello son yazıcı WINS – hello Azure veri Kataloğu model birden çok görüşlerini hello sistemindeki yan yana toolive sağlar.

Bu yaklaşım hello gerçek dünya farklı kullanıcıların farklı perspektiflerini belirli bir varlık üzerinde sahip olduğu kurumsal verilerin yansıtır:

* Veritabanı Yöneticisi toplu ETL işlemleri için hizmet düzeyi sözleşmelerine veya hello kullanılabilir işleme penceresi hakkında bilgiler sağlayabilir
* Bir veri steward hello iş işlemleri toowhich hello varlık hakkında bilgi uygular veya iş hello hello sınıflandırmaları tooit uygulanan sağlayabilir
* Finans analist hello veri süre sonu raporlama görevleri sırasında nasıl kullanıldığı hakkında bilgi sağlayabilir

toosupport Bu örnekte, her bir kullanıcı – hello DBA, hello veri steward ve hello analist – hello katalog kayıtlı açıklama tooa tek bir tabloya ekleyebilirsiniz. Tüm açıklamaları hello sistemde korunur ve tüm açıklamaları hello Azure veri Kataloğu Portalı'nda görüntülenir.

Bu desen hello nesne modelinde hello öğelerinin uygulanan toomost olduğundan, nesne türlerini hello JSON yükündeki genellikle özellikleri için bir singleton burada bekleyebilirsiniz dizidir.

Örneğin, hello varlık altında kök açıklama nesneleri dizisidir. Merhaba dizisi özelliği "Açıklamalar" olarak adlandırılır. Açıklama nesnesi bir özellik - açıklama sahiptir. Hello düzeni açıklama nesne türleri açıklamasını alır her bir kullanıcı hello kullanıcı tarafından sağlanan hello değeri için oluşturulmuş olur.

Merhaba UX nasıl toodisplay hello bileşimini seçebilirsiniz. Görüntü için üç farklı düzenleri vardır.

* Merhaba basit düzeni "Tümünü Göster" dir. Bu modelinde tüm hello nesneler bir liste görünümünde gösterilir. Hello Azure veri Kataloğu portalını UX açıklamasını bu deseni kullanır.
* Başka bir desen "Merge" dir. Bu modelinde hello farklı kullanıcılar tüm hello değerlerinden birlikte, kaldırılan yineleme ile birleştirilir. Bu desen hello Azure veri Kataloğu portalında UX hello etiketleri ve uzmanlar özellikleri gösterilebilir.
* Üçüncü bir desen "son yazan kazanır" dir. Bu modelinde yazdığınız yalnızca hello en son değer gösterilir. friendlyName bu deseni örneğidir.

## <a name="asset-object-model"></a>Varlık nesne modeli
Merhaba anahtar kavramlar bölümünde sunulduğu şekilde hello **Azure veri Kataloğu** nesne modeli varlıklar ya da ek açıklamalar öğeleri içerir. Öğelerinin isteğe bağlı ya da gerekli özellikler vardır. Bazı özellikler tooall öğelerini uygulayın. Bazı özellikleri tooall varlıklar geçerlidir. Bazı özellikleri yalnızca toospecific varlık türleri geçerlidir.

### <a name="system-properties"></a>Sistem özellikleri
<table><tr><td><b>Özellik adı</b></td><td><b>Veri türü</b></td><td><b>Açıklamalar</b></td></tr><tr><td>timestamp</td><td>Tarih saat</td><td>Merhaba son zaman hello öğeyi değiştirildi. Bu alan, bir öğe eklendiğinde ve öğenin her güncelleştirildiğinde hello sunucusu tarafından oluşturulur. Merhaba bu özelliğin değeri giriş, göz ardı edilir işlemleri yayımlayın.</td></tr><tr><td>id</td><td>URI</td><td>Mutlak url hello öğesinin (salt okunur). Bu, hello öğesi için benzersiz adreslenebilir URI hello olur.  Merhaba bu özelliğin değeri giriş, göz ardı edilir işlemleri yayımlayın.</td></tr><tr><td>type</td><td>Dize</td><td>Merhaba varlık (salt okunur) Hello türü.</td></tr><tr><td>ETag</td><td>Dize</td><td>Dize karşılık gelen toohello hello katalog öğeleri güncelleştirme işlemleri gerçekleştirirken iyimser eşzamanlılık denetimi için kullanılabilen hello öğenin sürümü. "*" kullanılan toomatch herhangi bir değer olabilir.</td></tr></table>

### <a name="common-properties"></a>Ortak Özellikler
Bu özellikleri tooall kök varlık türleri ve tüm ek açıklama türleri geçerlidir.

<table>
<tr><td><b>Özellik adı</b></td><td><b>Veri türü</b></td><td><b>Açıklamalar</b></td></tr>
<tr><td>fromSourceSystem</td><td>Boole değeri</td><td>Öğenin veri (Sql Server veritabanı, Oracle veritabanı gibi) bir kaynak sistemden türetilmiş veya bir kullanıcı tarafından yazılan olup olmadığını gösterir.</td></tr>
</table>

### <a name="common-root-properties"></a>Ortak kök özellikleri
<p>
Bu özellikleri tooall kök varlık türleri geçerlidir.

<table><tr><td><b>Özellik adı</b></td><td><b>Veri türü</b></td><td><b>Açıklamalar</b></td></tr><tr><td>ad</td><td>Dize</td><td>Hello veri kaynağı konum bilgilerini türetilmiş bir adı</td></tr><tr><td>DSL</td><td>DataSourceLocation</td><td>Benzersiz şekilde hello veri kaynağı açıklar ve hello varlık için hello tanımlayıcıları biridir. (Çift kimlik bölümüne bakın).  Merhaba dsl Hello yapısını hello protokolü tarafından değişir ve kaynak türü.</td></tr><tr><td>veri kaynağı</td><td>Datasourceınfo</td><td>Daha fazla ayrıntı varlık hello tür.</td></tr><tr><td>lastRegisteredBy</td><td>SecurityPrincipal</td><td>Bu varlık en kısa süre önce kaydolan hello kullanıcı açıklar.  Merhaba hello kullanıcı (Merhaba upn) için benzersiz kimlik ve görünen ad (Soyadı ve adı) içerir.</td></tr><tr><td>Containerıd</td><td>Dize</td><td>Merhaba kapsayıcı varlık hello veri kaynağı için kimliği. Bu özellik hello kapsayıcı türü için desteklenmiyor.</td></tr></table>

### <a name="common-non-singleton-annotation-properties"></a>Yaygın olarak kullanılan tek olmayan ek açıklama özellikleri
Bu özellikleri tooall tek olmayan ek açıklama türleri geçerlidir (toobe izin verilen ek açıklamaları birden çok varlık başına).

<table>
<tr><td><b>Özellik adı</b></td><td><b>Veri türü</b></td><td><b>Açıklamalar</b></td></tr>
<tr><td>anahtar</td><td>Dize</td><td>Merhaba açıklama hello geçerli koleksiyonu içinde benzersiz olarak tanımlayan bir kullanıcı belirtilen anahtar. Merhaba anahtar uzunluğu 256 karakterden uzun olamaz.</td></tr>
</table>

### <a name="root-asset-types"></a>Kök varlık türleri
Kök varlık hello kataloğa kayıtlı veri varlıklarını çeşitli türleri temsil eden türleri hello türleridir. Her kök türü için varlık ve hello görünümüne dahil ek açıklamaları açıklar bir görünüm yok. Görünüm adı, REST API kullanarak bir varlık yayımlarken hello karşılık gelen {view_name} url kesimi kullanılmalıdır.

<table><tr><td><b>Varlık türü (Görünüm adı)</b></td><td><b>Ek Özellikler</b></td><td><b>Veri türü</b></td><td><b>İzin verilen ek açıklamaları</b></td><td><b>Açıklamalar</b></td></tr><tr><td>Tabloda ("Tablo")</td><td></td><td></td><td>Açıklama<p>FriendlyName<p>Etiket<p>Şema<p>ColumnDescription<p>ColumnTag<p> Uzman<p>Önizleme<p>AccessInstruction<p>TableDataProfile<p>ColumnDataProfile<p>ColumnDataClassification<p>Belgeler<p></td><td>Bir tabloda hiç tablo verisi temsil eder.  Örneğin: SQL tablosu, SQL görünümü, Analysis Services Tabular tablo, Analysis Services çok boyutlu boyut, Oracle tablo, vs.   </td></tr><tr><td>Ölçü ("ölçüler")</td><td></td><td></td><td>Açıklama<p>FriendlyName<p>Etiket<p>Uzman<p>AccessInstruction<p>Belgeler<p></td><td>Bu tür bir Analysis Services ölçü temsil eder.</td></tr><tr><td></td><td>Ölçü birimi</td><td>Sütun</td><td></td><td>Meta veri açıklayan hello ölçü</td></tr><tr><td></td><td>isCalculated </td><td>Boole değeri</td><td></td><td>Merhaba ölçü veya hesaplanan olmadığını belirtir.</td></tr><tr><td></td><td>measureGroup</td><td>Dize</td><td></td><td>Ölçü için fiziksel kapsayıcı</td></tr><td>KPI'yı ("KPI'lar")</td><td></td><td></td><td>Açıklama<p>FriendlyName<p>Etiket<p>Uzman<p>AccessInstruction<p>Belgeler</td><td></td></tr><tr><td></td><td>measureGroup</td><td>Dize</td><td></td><td>Ölçü için fiziksel kapsayıcı</td></tr><tr><td></td><td>goalExpression</td><td>Dize</td><td></td><td>Sayısal MDX ifadesi veya hello KPI hedef değerini hello döndüren bir hesaplama.</td></tr><tr><td></td><td>valueExpression</td><td>Dize</td><td></td><td>Merhaba KPI hello gerçek değerini döndüren bir MDX sayısal ifade.</td></tr><tr><td></td><td>statusExpression</td><td>Dize</td><td></td><td>Zaman içinde belirtilen bir noktada hello KPI hello durumunu temsil eden MDX ifadesi.</td></tr><tr><td></td><td>trendExpression</td><td>Dize</td><td></td><td>Zaman içinde hello KPI hello değerini değerlendiren bir MDX ifadesi. Merhaba eğilimi belirli iş bağlamında yararlıdır zamana dayalı ölçüt olabilir.</td>
<tr><td>Rapor ("rapor")</td><td></td><td></td><td>Açıklama<p>FriendlyName<p>Etiket<p>Uzman<p>AccessInstruction<p>Belgeler<p></td><td>Bu tür bir SQL Server Reporting Services rapor temsil eder </td></tr><tr><td></td><td>assetCreatedDate</td><td>Dize</td><td></td><td></td></tr><tr><td></td><td>assetCreatedBy</td><td>Dize</td><td></td><td></td></tr><tr><td></td><td>assetModifiedDate</td><td>Dize</td><td></td><td></td></tr><tr><td></td><td>assetModifiedBy</td><td>Dize</td><td></td><td></td></tr><tr><td>Kapsayıcı ("kapsayıcıları")</td><td></td><td></td><td>Açıklama<p>FriendlyName<p>Etiket<p>Uzman<p>AccessInstruction<p>Belgeler<p></td><td>Bu tür bir SQL veritabanı, bir Azure BLOB kapsayıcısı veya bir Analysis Services modeli gibi diğer varlıklar bir kapsayıcıyı temsil eder.</td></tr></table>

### <a name="annotation-types"></a>Ek açıklama türleri
Ek açıklama türleri hello katalog içindeki tooother tür atanabilir meta veri türlerini temsil eder.

<table>
<tr><td><b>Ek açıklama türü (iç içe Görünüm adı)</b></td><td><b>Ek Özellikler</b></td><td><b>Veri türü</b></td><td><b>Açıklamalar</b></td></tr>

<tr><td>Açıklama ("Açıklamalar")</td><td></td><td></td><td>Bu özellik, bir varlık için bir açıklama içerir. Merhaba sisteminin her bir kullanıcı kendi açıklama ekleyebilirsiniz.  Yalnızca bu kullanıcının hello açıklaması nesnesine düzenleyebilirsiniz.  (Yöneticiler ve varlık sahipleri hello açıklama nesneyi silmek ancak düzenlemek değil). Merhaba sistem kullanıcıların açıklamaları ayrı ayrı tutar.  Bu nedenle açıklamaları her varlık (kimin bilgilerini hakkında bilgi içeren bir hello veri kaynağından türetilmiş toplama toopossibly hello varlığı katıldığını bir her kullanıcı için) üzerinde bir dizi yoktur.</td></tr>
<tr><td></td><td>açıklama</td><td>Dize</td><td>Merhaba varlık kısa bir açıklama (2-3 satırlar)</td></tr>

<tr><td>Etiket ("etiketler")</td><td></td><td></td><td>Bu özellik, bir varlık için bir etiket tanımlar. Merhaba sisteminin her bir kullanıcı bir varlık için birden çok etiket ekleyebilirsiniz.  Etiket nesneleri oluşturan hello kullanıcı bunları düzenleyebilirsiniz.  (Yöneticiler ve varlık sahipleri hello etiketi nesneyi silmek ancak düzenlemek değil). Merhaba sistem kullanıcıların etiketleri ayrı ayrı tutar.  Bu nedenle her varlık etiketi nesneler dizisi yok.</td></tr>
<tr><td></td><td>Etiket</td><td>Dize</td><td>Bir etiketi açıklayan hello varlığı.</td></tr>

<tr><td>FriendlyName ("friendlyName")</td><td></td><td></td><td>Bu özellik, bir varlık için bir kolay ad içerir. FriendlyName tek ek açıklama - yalnızca bir FriendlyName tooan varlık eklenebilir.  FriendlyName nesnesi oluşturan hello kullanıcı düzenleyebilirsiniz. (Yöneticiler ve varlık sahipleri hello FriendlyName nesneyi silmek ancak düzenlemek değil). Merhaba sistem kullanıcıların kolay adlar ayrı ayrı tutar.</td></tr>
<tr><td></td><td>FriendlyName</td><td>Dize</td><td>Merhaba varlık kolay adı.</td></tr>

<tr><td>Şeması ("şema")</td><td></td><td></td><td>Merhaba şema hello veri hello yapısını tanımlar.  Merhaba özniteliği (sütun, öznitelik, alan, vb.) adlarını listeler, de diğer meta veri türleri.  Bu bilgiler tüm hello veri kaynağından türetilir.  Şema tek ek açıklama - yalnızca bir şema için bir varlık eklenebilir.</td></tr>
<tr><td></td><td>sütunları</td><td>Sütun]</td><td>Sütun nesnelerinin bir dizisi. Bunlar hello veri kaynağından türetilmiş bilgilerle hello sütun açıklanmaktadır.</td></tr>

<tr><td>ColumnDescription ("columnDescriptions")</td><td></td><td></td><td>Bu özellik, bir sütun için bir açıklama içerir.  Merhaba sisteminin her bir kullanıcı birden çok sütun (en çok her bir sütunun) için kendi açıklamalar ekleyebilirsiniz. ColumnDescription nesneleri oluşturan hello kullanıcı bunları düzenleyebilirsiniz.  (Yöneticiler ve varlık sahipleri hello ColumnDescription nesneyi silmek ancak düzenlemek değil). Merhaba sistem bu kullanıcının sütun açıklamaları ayrı ayrı tutar.  Bu nedenle her varlık üzerinde ColumnDescription nesnelerinin bir dizisi yoktur (sütun bilgilerini hello sütun hakkında katıldığını her kullanıcı için her bir ek olarak toopossibly bilgi içeren bir türetilmiş hello veri kaynağı'ndan).  eşitlenmemiş sınıflandırıp hello ColumnDescription gevşek bağlanmış toohello şema ' dir. Merhaba ColumnDescription hello şemada artık bir sütun açıklayabilir.  Bu toohello yazan tookeep açıklama ve şema eşitlenmiş olur.  Hello veri kaynağı sütunları açıklama bilgilere sahip ve bunlar hello Aracı çalıştırırken oluşturulacak ek ColumnDescription nesneler.</td></tr>
<tr><td></td><td>columnName</td><td>Dize</td><td>Bu açıklama başvurduğu hello sütunun Hello adı.</td></tr>
<tr><td></td><td>açıklama</td><td>Dize</td><td>kısa bir açıklama (2-3 satırları) hello sütun.</td></tr>

<tr><td>ColumnTag ("columnTags")</td><td></td><td></td><td>Bu özellik, bir sütun için bir etiket içerir. Her kullanıcı hello sisteminin belirtilen sütun için birden çok etiket ekleyebilirsiniz ve birden çok sütun için etiketler ekleyebilirsiniz. ColumnTag nesneleri oluşturan hello kullanıcı bunları düzenleyebilirsiniz. (Yöneticiler ve varlık sahipleri hello ColumnTag nesneyi silmek ancak düzenlemek değil). Merhaba sistem bu kullanıcıların sütun etiketleri ayrı ayrı tutar.  Bu nedenle her varlık üzerinde ColumnTag nesnelerinin bir dizisi yok.  eşitlenmemiş sınıflandırıp hello ColumnTag gevşek bağlanmış toohello schema'dır. Merhaba ColumnTag hello şemada artık bir sütun açıklayabilir.  Bu toohello yazan tookeep sütun etiketi ve şema eşitlenmiş olur.</td></tr>
<tr><td></td><td>columnName</td><td>Dize</td><td>Bu etiket başvurduğu hello sütunun Hello adı.</td></tr>
<tr><td></td><td>Etiket</td><td>Dize</td><td>Bir etiket açıklayan başlangıç sütunu.</td></tr>

<tr><td>Uzman ("uzmanlar")</td><td></td><td></td><td>Bu özellik hello veri kümesindeki bir uzman kabul bir kullanıcıyı içerir. Merhaba uzmanlar opinions(descriptions) Kabarcık toohello üstündeki hello açıklamaları listelerken UX. Her bir kullanıcı kendi uzmanlar belirtebilirsiniz. Yalnızca bu kullanıcının hello uzmanlar nesneyi düzenleyebilirsiniz. (Yöneticiler ve varlık sahipleri hello Uzman nesneleri silmek ancak düzenlemek değil).</td></tr>
<tr><td></td><td>Uzman</td><td>SecurityPrincipal</td><td></td></tr>

<tr><td>Önizleme ("Önizleme")</td><td></td><td></td><td>Merhaba Önizleme hello üst 20 veri satırı hello varlık için bir görüntüsünü içerir. Önizleme yalnızca algılama için oluşturma (tablo için kullanılabilir ancak ölçü mantıklıdır) varlıklar bazı türleri.</td></tr>
<tr><td></td><td>Önizleme</td><td>Object]</td><td>Bir sütunu temsil eden nesneler dizisi.  Her nesne hello satır için bu sütun için bir değer ile tooa sütun eşlemesi bir özelliğe sahiptir.</td></tr>

<tr><td>AccessInstruction ("accessInstructions")</td><td></td><td></td><td></td></tr>
<tr><td></td><td>mime türü</td><td>Dize</td><td>Merhaba içerik Hello MIME türü.</td></tr>
<tr><td></td><td>İçerik</td><td>Dize</td><td>nasıl tooget toothis veri varlığına erişmek için hello yönergeler. Merhaba içeriği, bir URL, bir e-posta adresi veya yönergeler kümesi olabilir.</td></tr>

<tr><td>TableDataProfile ("tableDataProfiles")</td><td></td><td></td><td></td></tr>
<tr><td></td><td>numberOfRows</td></td><td>Int</td><td>Merhaba hello veri kümesi satır sayısı</td></tr>
<tr><td></td><td>Boyutu</td><td>uzun</td><td>Merhaba veri kümesinin bayt Hello boyutu.  </td></tr>
<tr><td></td><td>schemaModifiedTime</td><td>Dize</td><td>Merhaba son zaman hello şeması değiştirildi.</td></tr>
<tr><td></td><td>dataModifiedTime</td><td>Dize</td><td>Merhaba son zaman hello veri kümesi değiştirildi (veri, değişiklik, eklendi veya Sil)</td></tr>

<tr><td>ColumnsDataProfile ("columnsDataProfiles")</td><td></td><td></td><td></td></tr>
<tr><td></td><td>sütunları</td></td><td>ColumnDataProfile]</td><td>Sütun veri profiller bir dizi.</td></tr>

<tr><td>ColumnDataClassification ("columnDataClassifications")</td><td></td><td></td><td></td></tr>
<tr><td></td><td>columnName</td><td>Dize</td><td>Bu sınıflandırma başvurduğu hello sütunun Hello adı.</td></tr>
<tr><td></td><td>Sınıflandırma</td><td>Dize</td><td>Bu sütundaki hello verileri Hello sınıflandırması.</td></tr>

<tr><td>Belgeleri ("belgeleri")</td><td></td><td></td><td>Belirli bir varlık ile ilişkili yalnızca bir belge olabilir.</td></tr>
<tr><td></td><td>mime türü</td><td>Dize</td><td>Merhaba içerik Hello MIME türü.</td></tr>
<tr><td></td><td>İçerik</td><td>Dize</td><td>Merhaba documentation içeriği.</td></tr>

</table>

### <a name="common-types"></a>Genel türleri
Genel türleri özelliklerini hello türleri olarak kullanılabilir, ancak öğeleri değildir.

<table>
<tr><td><b>Ortak türü</b></td><td><b>Özellikleri</b></td><td><b>Veri türü</b></td><td><b>Açıklamalar</b></td></tr>
<tr><td>Datasourceınfo</td><td></td><td></td><td></td></tr>
<tr><td></td><td>Kaynak türü</td><td>Dize</td><td>Veri kaynağı Hello türünü açıklar.  Örneğin: SQL Server, Oracle veritabanı, vs.  </td></tr>
<tr><td></td><td>ObjectType</td><td>Dize</td><td>Merhaba hello veri kaynağı nesnesi türünü açıklar. Örneğin: Tablo, SQL Server için görüntüleyin.</td></tr>

<tr><td>DataSourceLocation</td><td></td><td></td><td></td></tr>
<tr><td></td><td>Protokolü</td><td>Dize</td><td>Gereklidir. Merhaba veri kaynağı ile kullanılan protokolü toocommunicate açıklar. Örneğin: SQl Server, Oracle, vb. için "oracle" için "tds". Çok başvuran[veri kaynağı başvurusu belirtimi - DSL yapısı](data-catalog-dsr.md) hello şu anda desteklenen protokollerin listesi için.</td></tr>
<tr><td></td><td>Adres</td><td>Sözlük<string, object></td><td>Gereklidir. Adres kullanılan tooidentify hello veri kaynağı başvurulan veri belirli toohello Protokolü kümesidir. Başlangıç adresi veri anlamsız hello Protokolü bilmeden anlamına tooa belirli Protokolü kapsamlı.</td></tr>
<tr><td></td><td>Kimlik doğrulaması</td><td>Dize</td><td>İsteğe bağlı. Merhaba kimlik doğrulama düzeni toocommunicate hello veri kaynağı ile kullanılır. Örneğin: windows, oauth vb..</td></tr>
<tr><td></td><td>connectionProperties</td><td>Sözlük<string, object></td><td>İsteğe bağlı. Hakkında ek bilgi tooconnect tooa veri kaynağı.</td></tr>

<tr><td>SecurityPrincipal</td><td></td><td></td><td>Merhaba arka uç tüm AAD karşı sağlanan özellikler doğrulama yayımlama sırasında gerçekleştirmez.</td></tr>
<tr><td></td><td>UPN</td><td>Dize</td><td>Kullanıcının benzersiz e-posta adresi. ObjectID sağlanmazsa, veya "lastRegisteredBy" özelliği, aksi takdirde isteğe bağlı Merhaba içeriğine belirtilmelidir.</td></tr>
<tr><td></td><td>objectID</td><td>GUID</td><td>Kullanıcı veya güvenlik grubu AAD kimliği. İsteğe bağlı. UPN, aksi takdirde isteğe bağlı sağlanmadı varsa belirtilmelidir.</td></tr>
<tr><td></td><td>FirstName</td><td>Dize</td><td>Kullanıcı (görüntüleme amaçlarıyla) adı. İsteğe bağlı. Yalnızca "lastRegisteredBy" özelliği hello bağlamında geçerli. Güvenlik sorumlusu "rol", "izinleri" ve "uzmanlar" için sağlanırken belirtilemez.</td></tr>
<tr><td></td><td>Soyadı</td><td>Dize</td><td>Kullanıcının soyadını (görüntüleme amaçlarıyla). İsteğe bağlı. Yalnızca "lastRegisteredBy" özelliği hello bağlamında geçerli. Güvenlik sorumlusu "rol", "izinleri" ve "uzmanlar" için sağlanırken belirtilemez.</td></tr>

<tr><td>Sütun</td><td></td><td></td><td></td></tr>
<tr><td></td><td>ad</td><td>Dize</td><td>Merhaba sütun veya öznitelik adı.</td></tr>
<tr><td></td><td>type</td><td>Dize</td><td>Merhaba sütun ya da öznitelik veri türü. Merhaba izin verilen türleri hello varlık veri kaynak türü bağlıdır.  Yalnızca bir alt türleri desteklenir.</td></tr>
<tr><td></td><td>maxLength</td><td>Int</td><td>Hello sütun veya özniteliği için izin verilen maksimum uzunluğu hello. Veri kaynağından türetilmiş. Yalnızca geçerli toosome kaynak türleri.</td></tr>
<tr><td></td><td>Duyarlılık</td><td>Bayt</td><td>Merhaba duyarlık hello sütun veya özniteliği için. Veri kaynağından türetilmiş. Yalnızca geçerli toosome kaynak türleri.</td></tr>
<tr><td></td><td>IsNullable</td><td>Boole değeri</td><td>Merhaba sütun olup toohave bir null değere izin. Veri kaynağından türetilmiş. Yalnızca geçerli toosome kaynak türleri.</td></tr>
<tr><td></td><td>ifade</td><td>Dize</td><td>Merhaba değer hesaplanmış bir sütun ise, bu alan hello değerini ifade hello ifade içeriyor. Veri kaynağından türetilmiş. Yalnızca geçerli toosome kaynak türleri.</td></tr>

<tr><td>ColumnDataProfile</td><td></td><td></td><td></td></tr>
<tr><td></td><td>columnName </td><td>Dize</td><td>Merhaba sütunun Hello adı</td></tr>
<tr><td></td><td>type </td><td>Dize</td><td>Merhaba sütununun başlangıç türü</td></tr>
<tr><td></td><td>dk </td><td>Dize</td><td>Merhaba en küçük değerin hello veri kümesi</td></tr>
<tr><td></td><td>max </td><td>Dize</td><td>Merhaba veri kümesindeki Hello en büyük değer</td></tr>
<tr><td></td><td>Ortalama </td><td>Çift</td><td>Merhaba veri kümesindeki Hello ortalama değer</td></tr>
<tr><td></td><td>STDEV </td><td>Çift</td><td>Merhaba standart sapma hello veri kümesi için</td></tr>
<tr><td></td><td>nullCount </td><td>Int</td><td>null değerler hello veri kümesindeki Hello sayısı</td></tr>
<tr><td></td><td>distinctCount  </td><td>Int</td><td>Merhaba veri kümesi ayrı değerleri Hello sayısı</td></tr>


</table>

## <a name="asset-identity"></a>Varlık Kimliği
Ve hello katalog içindeki varlık kimlik özelliklerinden hello hello DataSourceLocation "dsl" özelliği toogenerate kimliğini kullanılan tooaddress olan hello varlık özellik paketi "Adres" Merhaba "Protokolü" Azure veri kataloğu kullanır.
Örneğin, kimlik özellikleri "server", "veritabanı", "şema" ve "nesne" hello "tds" Protokolü sahiptir. Merhaba hello protokolü ve hello kimlik özellikleri kullanılan toogenerate hello hello SQL Server tablo varlık kimliğini birleşimleridir.
Azure veri Kataloğu sağlar adresinde listelenmiş birkaç yerleşik veri kaynağı protokolleri [veri kaynağı başvurusu belirtimi - DSL yapısı](data-catalog-dsr.md).
Merhaba desteklenen protokolleri kümesi programlı olarak Genişletilebilir (tooData Kataloğu REST API Başvurusu bakın). Merhaba katalog yöneticileri özel veri kaynağı protokolleri kaydedebilirsiniz. Merhaba aşağıdaki tabloda hello gereken özellikleri tooregister özel bir protokol açıklanmaktadır.

### <a name="custom-data-source-protocol-specification"></a>Özel veri kaynağı protokolü belirtimi
<table>
<tr><td><b>Tür</b></td><td><b>Özellikleri</b></td><td><b>Veri türü</b></td><td><b>Açıklamalar</b></td></tr>

<tr><td>DataSourceProtocol</td><td></td><td></td><td></td></tr>
<tr><td></td><td>Namespace</td><td>Dize</td><td>Merhaba Protokolü Hello ad alanı. Namespace, nokta (.) tarafından ayrılmış bir veya daha fazla boş bölümleri içeren 1 too255 karakterden uzun olmalıdır. Her bölümü karakter 1 too255 uzun olması, bir harf ile başlamalı ve yalnızca harfler ve sayılar içeren.</td></tr>
<tr><td></td><td>ad</td><td>Dize</td><td>Merhaba Protokolü Hello adı. Adı karakter 1 too255 uzun olması, bir harf ile başlamalı ve yalnızca harf, rakam ve tire (-) karakterinden hello içerir.</td></tr>
<tr><td></td><td>identityProperties</td><td>DataSourceProtocolIdentityProperty]</td><td>Liste kimlik özelliklerinin, en az bir, ancak hiçbir 20'den fazla özelliklerine sahip olması gerekir. Örneğin: "server", "veritabanı", "şema", "nesne" hello "tds" Protokolü kimlik özelliklerinin şunlardır.</td></tr>
<tr><td></td><td>identitySets</td><td>DataSourceProtocolIdentitySet]</td><td>Kimlik listesini ayarlar. Geçerli varlığın kimliğini temsil etmek kimlik özellikler kümesini tanımlar. En az bir, ancak hiçbir 20'den fazla kümeleri içermelidir. Örneğin: {"server", "veritabanı", "şema" ve "nesne"} olan Sql Server tablosu varlık kimliğini tanımlar "tds" Protokolü için bir kimlik.</td></tr>

<tr><td>DataSourceProtocolIdentityProperty</td><td></td><td></td><td></td></tr>
<tr><td></td><td>ad</td><td>Dize</td><td>Merhaba özelliğinin Hello adı. Adı 1 too100 karakterden uzun bir harf ile başlangıç arasında olmalı ve yalnızca harf ve sayı içerebilir.</td></tr>
<tr><td></td><td>type</td><td>Dize</td><td>Merhaba özelliğinin Hello türü. Desteklenen değerler: "bool", boolean ","bayt","guid","int","tamsayı","uzun","dize","url"</td></tr>
<tr><td></td><td>ignoreCase</td><td>bool</td><td>Servis talebi özelliğin değerini kullanırken yok sayılıp sayılmayacağını belirtir. Yalnızca "dize" türündeki özellikler için belirtilebilir. Varsayılan değer false şeklindedir.</td></tr>
<tr><td></td><td>urlPathSegmentsIgnoreCase</td><td>bool]</td><td>Durum her hello URL'sinin yol kesimi için yok sayılıp sayılmayacağını belirtir. Yalnızca "url" türündeki özellikler için belirtilebilir. Varsayılan değer [] false'tur.</td></tr>

<tr><td>DataSourceProtocolIdentitySet</td><td></td><td></td><td></td></tr>
<tr><td></td><td>ad</td><td>Dize</td><td>Merhaba kimlik Hello adını ayarlayın.</td></tr>
<tr><td></td><td>properties</td><td>String]</td><td>Bu kimlik dahil kimlik özellikleri Hello listesini ayarlayın. Yinelenen değer içeremez. Kimlik kümesi tarafından başvurulan her bir özellik hello Protokolü "identityProperties" Merhaba listesinde tanımlanması gerekir.</td></tr>

</table>

## <a name="roles-and-authorization"></a>Rolleri ve yetkilendirme
Microsoft Azure veri Kataloğu varlıkları ve ek açıklamaları CRUD işlemleri için yetkilendirme özellikleri sağlar.

## <a name="key-concepts"></a>Önemli kavramlar
Hello Azure veri Kataloğu iki yetkilendirme mekanizması kullanır:

* Rol tabanlı yetkilendirme
* İzni tabanlı bir yetkilendirme

### <a name="roles"></a>Roller
Üç rol vardır: **yönetici**, **sahibi**, ve **katkıda bulunan**.  Her rol kapsam ve aşağıdaki tablonun hello özetlenir hakları sahiptir.

<table><tr><td><b>Rol</b></td><td><b>Kapsam</b></td><td><b>Hakları</b></td></tr><tr><td>Yönetici</td><td>Katalog (tüm varlıklar/ek açıklamalar hello katalog)</td><td>Okuma silme ViewRoles

ChangeOwnership ChangeVisibility ViewPermissions</td></tr><tr><td>Sahip</td><td>Her varlık (kök öğe)</td><td>Okuma silme ViewRoles

ChangeOwnership ChangeVisibility ViewPermissions</td></tr><tr><td>Katılımcı</td><td>Her bir tek varlığı ve ek açıklaması</td><td>Okuma güncelleştirme ViewRoles Not silin: hello sağa hello öğesi katkıda bulunan hello iptal okuyorsanız tüm hello hakları iptal edilir</td></tr></table>

> [!NOTE]
> **Okuma**, **güncelleştirme**, **silmek**, **ViewRoles** haklarıdır sırasında geçerli tooany öğesi (varlık veya ek açıklama) **TakeOwnership**, **ChangeOwnership**, **ChangeVisibility**, **ViewPermissions** yalnızca geçerli toohello kök varlık şunlardır.
> 
> **Silme** hak tooan öğeyi ve alt öğeler veya bunun altındaki tek öğe geçerlidir. Örneğin, bir varlık silindiğinde de bu varlık için ek açıklamaları silinir.
> 
> 

### <a name="permissions"></a>İzinler
İzni erişim denetimi girdileri listesidir. Her erişim denetim girdisi hakları tooa güvenlik sorumlusu kümesi atar. İzinleri yalnızca bir varlığı (diğer bir deyişle, kök öğe) belirtilebilir ve toohello varlık ve tüm alt öğeler uygulayın.

Merhaba sırasında **Azure veri Kataloğu** Önizleme, yalnızca **okuma** sağ hello izinleri listesi tooenable senaryo toorestrict görünürlüğünü bir varlık desteklenir.

Varsayılan olarak tüm kimliği doğrulanmış kullanıcının sahip **okuma** sağ hello kataloğunda herhangi bir öğenin görünürlüğü kısıtlanmadığı sürece toohello sorumluları hello izinler kümesi.

## <a name="rest-api"></a>REST API
**PUT** ve **POST** görünümü öğesi istekleri kullanılan toocontrol rolleri ve izinleri olabilir: ek tooitem yükünde iki sistem özellikler belirtilebilir **rolleri** ve  **izinleri**.

> [!NOTE]
> **izinleri** yalnızca geçerli tooa kök öğe.
> 
> **Sahibi** rolü yalnızca geçerli tooa kök öğe.
> 
> Bir öğe hello kataloğunda oluşturulduğunda, varsayılan olarak, **katkıda bulunan** toohello şu anda kimliği doğrulanmış kullanıcı ayarlanır. Öğe herkes tarafından güncelleştirilebilir gerekiyorsa **katkıda bulunan** çok ayarlanmalıdır&lt;herkesin&gt; hello özel bir güvenlik sorumlusu **rolleri** öğesi özelliği (ilk yayımlanan toohello aşağıdaki örneğine bakın). **Katkıda bulunan** değiştirilemez ve kalır hello aynı yaşam süresi sırasında bir öğe (hatta **yönetici** veya **sahibi** hello sağ toochange hello yok  **Katkıda bulunan**). yalnızca Hello açık ayarı hello için desteklenen değer hello **katkıda bulunan** olan &lt;herkesin&gt;: **katkıda bulunan** yalnızca bir öğe oluşturan bir kullanıcı olabilir veya &lt; Herkes&gt;.
> 
> 

### <a name="examples"></a>Örnekler
**Katkıda bulunan çok ayarlamak&lt;herkesin&gt; öğeyi yayımlarken.**
Özel bir güvenlik sorumlusu &lt;herkesin&gt; objectID "00000000-0000-0000-0000-000000000201" sahiptir.
  **POST** https://api.azuredatacatalog.com/catalogs/default/views/tables/?api-version=2016-03-30

> [!NOTE]
> Bazı HTTP istemci uygulamaları yanıt tooa 302 hello sunucusundan gelen istekleri otomatik olarak yeniden ancak genellikle paketlerden hello isteği yetkilendirme üstbilgileri kaldırın. Merhaba Authorization Üstbilgisi gerekli toomake istekleri tooAzure veri Kataloğu olduğundan hello Authorization Üstbilgisi hala Azure veri Kataloğu tarafından belirtilen bir istek tooa yeniden yönlendirme konumu verilene sağlanır emin olmalısınız. Merhaba aşağıdaki örnek kod hello .NET HttpWebRequest nesnesi kullanarak gösterir.
> 
> 

**Gövde**

    {
        "roles": [
            {
                "role": "Contributor",
                "members": [
                    {
                        "objectId": "00000000-0000-0000-0000-000000000201"
                    }
                ]
            }
        ]
    }

  **Sahiplerini atamak ve var olan bir kök öğe için görünürlüğü kısıtlama**: **PUT** https://api.azuredatacatalog.com/catalogs/default/views/tables/042297b0...1be45ecd462a?api-version=2016-03-30

    {
        "roles": [
            {
                "role": "Owner",
                "members": [
                    {
                        "objectId": "c4159539-846a-45af-bdfb-58efd3772b43",
                        "upn": "user1@contoso.com"
                    },
                    {
                        "objectId": "fdabd95b-7c56-47d6-a6ba-a7c5f264533f",
                        "upn": "user2@contoso.com"
                    }
                ]
            }
        ],
        "permissions": [
            {
                "principal": {
                    "objectId": "27b9a0eb-bb71-4297-9f1f-c462dab7192a",
                    "upn": "user3@contoso.com"
                },
                "rights": [
                    {
                        "right": "Read"
                    }
                ]
            },
            {
                "principal": {
                    "objectId": "4c8bc8ce-225c-4fcf-b09a-047030baab31",
                    "upn": "user4@contoso.com"
                },
                "rights": [
                    {
                        "right": "Read"
                    }
                ]
            }
        ]
    }

> [!NOTE]
> İŞLEMLERİNDE, toospecify hello body öğesi yükünde zorunlu değildir: PUT kullanılan tooupdate yalnızca rolleri ve/veya izinlerini olabilir.
> 
> 

<!--Image references-->
[1]: ./media/data-catalog-developer-concepts/concept2.png
