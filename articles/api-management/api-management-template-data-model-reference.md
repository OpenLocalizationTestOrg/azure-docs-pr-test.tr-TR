---
title: "aaaAzure API Management şablonu veri modeli başvurusu | Microsoft Docs"
description: "Azure API Management'ta Geliştirici Portalı şablonları hello hello veri modellerinde kullanılan ortak öğeler için hello varlığı ve türü Beyanları hakkında bilgi edinin."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: b0ad7e15-9519-4517-bb73-32e593ed6380
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 7d049d8ecc9e597cf48ce0c820c172798bcf86de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-template-data-model-reference"></a>Azure API Management şablonu veri modeli başvurusu
Bu konuda hello varlığı ve türü Beyanları hello veri modellerinde Azure API Management'ta Geliştirici Portalı şablonları hello için kullanılan ortak öğeler için açıklanmaktadır.  
  
 Şablonları ile çalışma hakkında daha fazla bilgi için bkz: [nasıl toocustomize hello şablonları kullanarak API Management Geliştirici Portalı](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).  
  
-   [API](#API)  
-   [API özeti](#APISummary)  
-   [Uygulama](#Application)  
-   [Eki](#Attachment)  
-   [Kod örneği](#Sample)  
-   [Açıklama](#Comment)  
-   [Filtreleme](#Filtering)  
-   [Üstbilgi](#Header)  
-   [HTTP isteği](#HTTPRequest)  
-   [HTTP yanıtı](#HTTPResponse)  
-   [Sorunu](#Issue)  
-   [İşlem](#Operation)  
-   [İşlemi menüsü](#Menu)  
-   [İşlemi menü öğesi](#MenuItem)  
-   [Disk belleği](#Paging)  
-   [Parametre](#Parameter)  
-   [Ürün](#Product)  
-   [Sağlayıcı](#Provider)  
-   [Gösterimi](#Representation)  
-   [Abonelik](#Subscription)  
-   [Abonelik özeti](#SubscriptionSummary)  
-   [Kullanıcı hesabı bilgileri](#UserAccountInfo)  
-   [Kullanıcı oturum açma](#UseSignIn)  
-   [Kullanıcı Kaydolma](#UserSignUp)  
  
##  <a name="API"></a>API  
 Merhaba `API` varlık hello aşağıdaki özelliklere sahiptir.  
  
|Özellik|Tür|Açıklama|  
|--------------|----------|-----------------|  
|id|Dize|Kaynak tanımlayıcısı. Merhaba API hello geçerli API Management hizmet örneği içinde benzersiz olarak tanımlar. Merhaba değerdir hello biçiminde geçerli bir göreli URL `apis/{id}` burada `{id}` bir API tanımlayıcısıdır. Bu özellik salt okunurdur.|  
|ad|Dize|Merhaba API adı. Boş olmamalıdır. En fazla 100 karakter olabilir.|  
|açıklama|Dize|Merhaba API açıklaması. Boş olmamalıdır. HTML biçimlendirme etiketleriyle içerebilir. En fazla 1000 karakter olabilir.|  
|serviceUrl|Dize|Bu API uygulama hello arka uç hizmetinin mutlak URL.|  
|Yol|Dize|Bu API ve tüm alt kaynak yolları hello API Management hizmet örneği içinde benzersiz olarak tanımlama göreli URL'si. Bunu eklenir toohello API uç noktası temel URL bu API için genel bir URL hello hizmet örneği oluşturma tooform sırasında belirtilen.|  
|protokolleri|dizi numarası|Bu API işlemleri hangi protokolleri hello çağrılabilir açıklar. İzin verilen değerler `1 - http` ve `2 - https`, veya her ikisini de.|  
|authenticationSettings|[Yetkilendirme sunucusu kimlik doğrulama ayarları](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#AuthenticationSettings)|Bu API içinde bulunan kimlik doğrulama ayarları koleksiyonu.|  
|subscriptionKeyParameterNames|Nesne|Merhaba abonelik anahtarı içeren sorgu ve/veya üstbilgi parametreleri için kullanılan toospecify özel adları olabilir isteğe bağlı özellik. Bu özellik bulunduğunda hello iki aşağıdaki özellikleri en az birini içermelidir.<br /><br /> `{   "subscriptionKeyParameterNames":   {     "query": “customQueryParameterName",     "header": “customHeaderParameterName"   } }`|  
  
##  <a name="APISummary"></a>API özeti  
 Merhaba `API summary` varlık hello aşağıdaki özelliklere sahiptir.  
  
|Özellik|Tür|Açıklama|  
|--------------|----------|-----------------|  
|id|Dize|Kaynak tanımlayıcısı. Merhaba API hello geçerli API Management hizmet örneği içinde benzersiz olarak tanımlar. Merhaba değerdir hello biçiminde geçerli bir göreli URL `apis/{id}` burada `{id}` bir API tanımlayıcısıdır. Bu özellik salt okunurdur.|  
|ad|Dize|Merhaba API adı. Boş olmamalıdır. En fazla 100 karakter olabilir.|  
|açıklama|Dize|Merhaba API açıklaması. Boş olmamalıdır. HTML biçimlendirme etiketleriyle içerebilir. En fazla 1000 karakter olabilir.|  
  
##  <a name="Application"></a>Uygulama  
 Merhaba `application` varlık hello aşağıdaki özelliklere sahiptir.  
  
|Özellik|Tür|Açıklama|  
|--------------|----------|-----------------|  
|Kimlik|Dize|Merhaba hello uygulamanın benzersiz tanımlayıcısı.|  
|Başlık|Dize|Merhaba uygulaması Hello başlığı.|  
|Açıklama|Dize|Merhaba uygulaması Hello açıklaması.|  
|Url|URI|Merhaba URI Merhaba uygulaması.|  
|Sürüm|Dize|Merhaba uygulaması için sürüm bilgileri.|  
|Gereksinimler|Dize|Merhaba uygulamanın gereksinimleri açıklaması.|  
|Durum|Sayı|Merhaba hello uygulamasının geçerli durumu.<br /><br /> -0 - kayıtlı<br /><br /> -Gönderilen 1-<br /><br /> -Yayımlanan 2-<br /><br /> -Reddedilen 3-<br /><br /> -4 - yayımlanmamış|  
|RegistrationDate|Tarih saat|Başlangıç tarihi ve saati Merhaba uygulaması kaydettirildi.|  
|Adlı kullanıcı, Categoryıd'si|Sayı|Merhaba kategori hello uygulamanın (Finans, eğlence, vs.)|  
|DeveloperId|Dize|Merhaba Merhaba uygulaması gönderilen hello Developer benzersiz tanımlayıcısı.|  
|Ekleri|Koleksiyonu [ek](#Attachment) varlıklar.|Herhangi bir ek ekran görüntüleri veya simgeler gibi hello uygulama için.|  
|Simgesi|[Eki](#Attachment)|Merhaba simgesi hello Merhaba uygulaması için.|  
  
##  <a name="Attachment"></a>Eki  
 Merhaba `attachment` varlık hello aşağıdaki özelliklere sahiptir.  
  
|Özellik|Tür|Açıklama|  
|--------------|----------|-----------------|  
|UniqueId|Dize|Merhaba hello eki için benzersiz tanımlayıcı.|  
|Url|Dize|Merhaba kaynak Hello URL'si.|  
|Tür|Dize|Ek Hello türü.|  
|ContentType|Dize|Merhaba eki Hello medya türü.|  
  
##  <a name="Sample"></a>Kod örneği  
  
|Özellik|Tür|Açıklama|  
|--------------|----------|-----------------|  
|Başlık|Dize|Merhaba işlemi Hello adı.|  
|kod parçacığında|Dize|Bu özellik kullanım dışıdır ve kullanılmamalıdır.|  
|Fırça|Dize|Hangi sözdizimi hello kod örneği görüntülenirken kullanılan şablon toobe renklendirme kodu. İzin verilen değerler `plain`, `php`, `java`, `xml`, `objc`, `python`, `ruby`, ve `csharp`.|  
|şablon|Dize|Bu kod örneği şablon Hello adı.|  
|Gövde|Dize|Merhaba kod örnek hello parçacığı kısmı için bir yer tutucu.|  
|Yöntemi|Dize|Merhaba hello işleminin HTTP yöntemi.|  
|Düzeni|Dize|Merhaba Protokolü toouse hello işlemi isteği için.|  
|Yol|Dize|Merhaba işlemi Hello yolu.|  
|sorgu|Dize|Sorgu dizesi örnek tanımlanan parametrelere sahip.|  
|ana bilgisayar|Dize|Merhaba API Management hizmeti hello bu işlem içeriyor API için ağ geçidi Hello URL'si.|  
|Üstbilgileri|Koleksiyonu [üstbilgi](#Header) varlıklar.|Bu işlem için üstbilgiler.|  
|parametreler|Koleksiyonu [parametresi](#Parameter) varlıklar.|Bu işlem için tanımlanan parametreleri.|  
  
##  <a name="Comment"></a>Açıklama  
 Merhaba `API` varlık hello aşağıdaki özelliklere sahiptir.  
  
|Özellik|Tür|Açıklama|  
|--------------|----------|-----------------|  
|Kimlik|Sayı|Merhaba yorum Hello kimliği.|  
|CommentText|Dize|Merhaba gövdesi hello açıklaması. HTML içerebilir.|  
|DeveloperCompany|Dize|Merhaba Geliştirici Hello şirket adı.|  
|PostedOn|Tarih saat|Başlangıç tarihi ve saati hello yorum gönderildi.|  
  
##  <a name="Issue"></a>Sorunu  
 Merhaba `issue` varlık hello aşağıdaki özelliklere sahiptir.  
  
|Özellik|Tür|Açıklama|  
|--------------|----------|-----------------|  
|Kimlik|Dize|Merhaba hello sorunu için benzersiz tanımlayıcı.|  
|ApiID|Dize|Bu sorun bildirildi hello API Hello kimliği.|  
|Başlık|Dize|Merhaba sorunu başlığı.|  
|Açıklama|Dize|Merhaba sorun açıklaması.|  
|SubscriptionDeveloperName|Dize|Merhaba sorunu bildiren hello Geliştirici adı.|  
|IssueState|Dize|Merhaba hello sorunun geçerli durumu. Olası değerler şunlardır: Önerilen, açık, kapalı.|  
|ReportedOn|Tarih saat|Başlangıç tarihi ve saati hello sorun bildirildi.|  
|Yorumlar|Koleksiyonu [açıklama](#Comment) varlıklar.|Bu konu hakkında açıklamalar.|  
|Ekleri|Koleksiyonu [ek](api-management-template-data-model-reference.md#Attachment) varlıklar.|Tüm ekleri toohello sorun.|  
|Hizmetler|Koleksiyonu [API](#API) varlıklar.|Merhaba API'leri hello sorunu Dosyalanan tooby hello kullanıcı abone.|  
  
##  <a name="Filtering"></a>Filtreleme  
 Merhaba `filtering` varlık hello aşağıdaki özelliklere sahiptir.  
  
|Özellik|Tür|Açıklama|  
|--------------|----------|-----------------|  
|düzeni|Dize|Arama terimi geçerli Hello; veya `null` arama terimi yok ise.|  
|Yer tutucu|Dize|Belirtilen arama terimi yok olduğunda hello arama kutusuna Hello metin toodisplay.|  
  
##  <a name="Header"></a>Üstbilgi  
 Bu bölümde hello açıklanmaktadır `parameter` gösterimi.  
  
|Özellik|Açıklama|Tür|  
|--------------|-----------------|----------|  
|ad|Dize|Parametre adı.|  
|açıklama|Dize|Parametre açıklaması.|  
|değer|Dize|Üstbilgi değeri.|  
|TypeName|Dize|Üstbilgi değeri veri türü.|  
|Seçenekler|Dize|Seçenekler.|  
|Gerekli|Boole değeri|Merhaba üstbilgi gerekli olup olmadığı.|  
|salt okunur|Boole değeri|Merhaba üstbilgi salt okunur olup olmadığı.|  
  
##  <a name="HTTPRequest"></a>HTTP isteği  
 Bu bölümde hello açıklanmaktadır `request` gösterimi.  
  
|Özellik|Tür|Açıklama|  
|--------------|----------|-----------------|  
|açıklama|Dize|İşlem isteği açıklaması.|  
|Üstbilgileri|dizi [üstbilgi](#Header) varlıklar.|İstek üstbilgileri.|  
|parametreler|dizi [parametresi](#Parameter)|İşlem istek parametreleri topluluğu.|  
|temsili|dizi [gösterimi](#Representation)|İşlem istek sunumlarını koleksiyonu.|  
  
##  <a name="HTTPResponse"></a>HTTP yanıtı  
 Bu bölümde hello açıklanmaktadır `response` gösterimi.  
  
|Özellik|Tür|Açıklama|  
|--------------|----------|-----------------|  
|statusCode|Pozitif tamsayı|İşlem yanıt durum kodu.|  
|açıklama|Dize|İşlem yanıt açıklaması.|  
|temsili|dizi [gösterimi](#Representation)|İşlem yanıt Beyanları koleksiyonu.|  
  
##  <a name="Operation"></a>İşlemi  
 Merhaba `operation` varlık hello aşağıdaki özelliklere sahiptir.  
  
|Özellik|Tür|Açıklama|  
|--------------|----------|-----------------|  
|id|Dize|Kaynak tanımlayıcısı. Merhaba işlemi hello geçerli API Management hizmet örneği içinde benzersiz olarak tanımlar. Merhaba değerdir hello biçiminde geçerli bir göreli URL `apis/{aid}/operations/{id}` nerede `{aid}` bir API tanımlayıcısıdır ve `{id}` işlemi tanımlayıcıdır. Bu özellik salt okunurdur.|  
|ad|Dize|Merhaba işlemin adı. Boş olmamalıdır. En fazla 100 karakter olabilir.|  
|açıklama|Dize|Merhaba işlemi açıklaması. Boş olmamalıdır. HTML biçimlendirme etiketleriyle içerebilir. En fazla 1000 karakter olabilir.|  
|Düzeni|Dize|Bu API işlemleri hangi protokolleri hello çağrılabilir açıklar. İzin verilen değerler `http`, `https`, veya her ikisini de `http` ve `https`.|  
|uriTemplate|Dize|Bu işlem için Hello hedef kaynak tanımlayan göreli URL şablonu. Parametreler içerebilir. Örnek:`customers/{cid}/orders/{oid}/?date={date}`|  
|ana bilgisayar|Dize|Merhaba API barındıran hello API Yönetimi ağ geçidi URL'si.|  
|HttpMethod|Dize|İşlemi HTTP yöntemi.|  
|İstek|[HTTP isteği](#HTTPRequest)|İstek ayrıntıları içeren bir varlık.|  
|yanıtları|dizi [HTTP yanıtı](#HTTPResponse)|İşlem dizisi [HTTP yanıtı](#HTTPResponse) varlıklar.|  
  
##  <a name="Menu"></a>İşlemi menüsü  
 Merhaba `operation menu` varlık hello aşağıdaki özelliklere sahiptir.  
  
|Özellik|Tür|Açıklama|  
|--------------|----------|-----------------|  
|ApiId|Dize|Merhaba geçerli API Hello kimliği.|  
|CurrentOperationId|Dize|Merhaba geçerli işlem Hello kimliği.|  
|Eylem|Dize|Merhaba menü türü.|  
|MenuItems|Koleksiyonu [işlemi menü öğesi](#MenuItem) varlıklar.|Merhaba işlemleri hello geçerli API için.|  
  
##  <a name="MenuItem"></a>İşlemi menü öğesi  
 Merhaba `operation menu item` varlık hello aşağıdaki özelliklere sahiptir.  
  
|Özellik|Tür|Açıklama|  
|--------------|----------|-----------------|  
|Kimlik|Dize|Merhaba işlemi Hello kimliği.|  
|Başlık|Dize|Merhaba işlemi Hello açıklaması.|  
|HttpMethod|Dize|Merhaba hello işleminin Http yöntemi.|  
  
##  <a name="Paging"></a>Disk belleği  
 Merhaba `paging` varlık hello aşağıdaki özelliklere sahiptir.  
  
|Özellik|Tür|Açıklama|  
|--------------|----------|-----------------|  
|Sayfa|Sayı|Merhaba geçerli sayfa numarası.|  
|PageSize|Sayı|Merhaba en fazla sonuç toobe tek bir sayfada görüntülenir.|  
|TotalItemCount|Sayı|Merhaba görüntülenmesi için öğe sayısı.|  
|ShowAll|Boole değeri|Olup toosho tüm tek bir sayfada sonuçlanır.|  
|PageCount|Sayı|Merhaba sonuçlarının sayfa sayısı.|  
  
##  <a name="Parameter"></a>Parametre  
 Bu bölümde hello açıklanmaktadır `parameter` gösterimi.  
  
|Özellik|Açıklama|Tür|  
|--------------|-----------------|----------|  
|ad|Dize|Parametre adı.|  
|açıklama|Dize|Parametre açıklaması.|  
|değer|Dize|Parametre değeri.|  
|Seçenekler|Dize dizisi|Sorgu parametre değerleri için tanımlanan değerleri.|  
|Gerekli|Boole değeri|Parametresi gerekli olup olmadığını belirtir.|  
|türü|Sayı|Bu parametre bir yol parametresi (1) veya bir sorgu dizesi parametresi (2) olup olmadığı.|  
|TypeName|Dize|Parametre türü.|  
  
##  <a name="Product"></a>Ürün  
 Merhaba `product` varlık hello aşağıdaki özelliklere sahiptir.  
  
|Özellik|Tür|Açıklama|  
|--------------|----------|-----------------|  
|Kimlik|Dize|Kaynak tanımlayıcısı. Merhaba ürün hello geçerli API Management hizmet örneği içinde benzersiz olarak tanımlar. Merhaba değerdir hello biçiminde geçerli bir göreli URL `products/{pid}` burada `{pid}` bir ürün tanımlayıcısı. Bu özellik salt okunurdur.|  
|Başlık|Dize|Merhaba ürün adı. Boş olmamalıdır. En fazla 100 karakter olabilir.|  
|Açıklama|Dize|Merhaba ürün açıklaması. Boş olmamalıdır. HTML biçimlendirme etiketleriyle içerebilir. En fazla 1000 karakter olabilir.|  
|Koşullar|Dize|Kullanım koşulları ürün. Geliştiriciler toosubscribe toohello ürün çalışırken sunulur ve hello Abonelik işlemini tamamlamadan önce bu koşulları tooaccept gerekli.|  
|ProductState|Sayı|Merhaba ürün veya yayımlanan belirtir. Yayımlanan ürünleri hello Geliştirici portalındaki geliştiriciler tarafından bulunabilir. Ürün olmayan yayımlanan görünür yalnızca tooadministrators değil.<br /><br /> Merhaba ürün durumu için izin verilen değerler şunlardır:<br /><br /> - `0 - Not Published`<br /><br /> - `1 - Published`<br /><br /> - `2 - Deleted`|  
|AllowMultipleSubscriptions|Boole değeri|Bir kullanıcı birden fazla abonelik toothis ürün hello sahip olup olmadığını belirtir aynı anda.|  
|MultipleSubscriptionsCount|Sayı|Abonelikler toothis ürün hello geçerli kullanıcı tarafından Hello sayısı.|  
  
##  <a name="Provider"></a>Sağlayıcı  
 Merhaba `provider` varlık hello aşağıdaki özelliklere sahiptir.  
  
|Özellik|Tür|Açıklama|  
|--------------|----------|-----------------|  
|Özellikler|dize sözlüğü|Bu kimlik doğrulama sağlayıcısı özellikleri.|  
|authenticationType|Dize|Merhaba sağlayıcısı türü. (Azure Active Directory, Facebook oturum açma, Google hesabı, Microsoft Account, Twitter).|  
|Açıklamalı alt yazı|Dize|Merhaba sağlayıcının görünen adı.|  
  
##  <a name="Representation"></a>Gösterimi  
 Bu bölümde açıklanmıştır bir `representation`.  
  
|Özellik|Tür|Açıklama|  
|--------------|----------|-----------------|  
|ContentType|Dize|Kayıtlı ya da özel bir içerik türü için bu gösterim örneğin belirtir `application/xml`.|  
|Örnek|Dize|Merhaba gösterim örneği.|  
  
##  <a name="Subscription"></a>Abonelik  
 Merhaba `subscription` varlık hello aşağıdaki özelliklere sahiptir.  
  
|Özellik|Tür|Açıklama|  
|--------------|----------|-----------------|  
|Kimlik|Dize|Kaynak tanımlayıcısı. Merhaba abonelik hello geçerli API Management hizmet örneği içinde benzersiz olarak tanımlar. Merhaba değerdir hello biçiminde geçerli bir göreli URL `subscriptions/{sid}` burada `{sid}` bir abonelik tanımlayıcısı. Bu özellik salt okunurdur.|  
|ProductID|Dize|Merhaba ürün kaynak hello tanıtıcısı ürün abone. Merhaba değerdir hello biçiminde geçerli bir göreli URL `products/{pid}` burada `{pid}` bir ürün tanımlayıcısı.|  
|ProductTitle|Dize|Merhaba ürün adı. Boş olmamalıdır. En fazla 100 karakter olabilir.|  
|ProductDescription|Dize|Merhaba ürün açıklaması. Boş olmamalıdır. HTML biçimlendirme etiketleriyle içerebilir. En fazla 1000 karakter olabilir.|  
|ProductDetailsUrl|Dize|Göreli URL toohello Ürün Ayrıntıları.|  
|durum|Dize|Merhaba abonelik Hello durumu. Olası durumlar şunlardır:<br /><br /> - `0 - suspended`– hello abonelik engellenir ve hello abone hello ürünün herhangi bir API çağrılamıyor.<br /><br /> - `1 - active`– hello abonelik etkin olduğunu.<br /><br /> - `2 - expired`– hello abonelik sona erme tarihini ulaştı ve devre dışı bırakıldı.<br /><br /> - `3 - submitted`– hello abonelik isteği hello geliştirici tarafından yapılan ancak henüz onaylanamıyor veya reddedilemiyor.<br /><br /> - `4 - rejected`– bir yönetici tarafından hello abonelik isteği reddedildi.<br /><br /> - `5 - cancelled`– hello geliştirici veya yönetici tarafından hello aboneliği iptal edildi.|  
|Görünen adı|Dize|Merhaba abonelik adını görüntüler.|  
|CreatedDate|Tarih saat|Başlangıç tarihi hello abonelik oluşturuldu, ISO 8601 biçiminde: `2014-06-24T16:25:00Z`.|  
|CanBeCancelled|Boole değeri|Olup hello abonelik hello geçerli kullanıcı tarafından iptal edilebilir.|  
|IsAwaitingApproval|Boole değeri|Olup hello abonelik onayını bekliyor.|  
|StartDate|Tarih saat|Merhaba başlangıç tarihi hello abonelik için ISO 8601 biçiminde: `2014-06-24T16:25:00Z`.|  
|ExpirationDate|Tarih saat|Merhaba sona erme tarihini ISO 8601 biçiminde hello abonelik: `2014-06-24T16:25:00Z`.|  
|NotificationDate|Tarih saat|ISO 8601 biçiminde hello abonelik için Hello bildirim tarihi: `2014-06-24T16:25:00Z`.|  
|primaryKey|Dize|Merhaba birincil abonelik anahtarı. En fazla uzunluğu 256 karakterden uzun.|  
|secondaryKey|Dize|Merhaba ikincil abonelik anahtarı. En fazla uzunluğu 256 karakterden uzun.|  
|CanBeRenewed|Boole değeri|Merhaba abonelik hello geçerli kullanıcı tarafından yenilenmesi.|  
|HasExpired|Boole değeri|Merhaba abonelik süresi doldu.|  
|IsRejected|Boole değeri|Olup hello abonelik istek reddedildi.|  
|CancelUrl|Dize|Merhaba göreli Url toocancel hello abonelik.|  
|RenewUrl|Dize|Merhaba göreli Url toorenew hello abonelik.|  
  
##  <a name="SubscriptionSummary"></a>Abonelik özeti  
 Merhaba `subscription summary` varlık hello aşağıdaki özelliklere sahiptir.  
  
|Özellik|Tür|Açıklama|  
|--------------|----------|-----------------|  
|Kimlik|Dize|Kaynak tanımlayıcısı. Merhaba abonelik hello geçerli API Management hizmet örneği içinde benzersiz olarak tanımlar. Merhaba değerdir hello biçiminde geçerli bir göreli URL `subscriptions/{sid}` burada `{sid}` bir abonelik tanımlayıcısı. Bu özellik salt okunurdur.|  
|Görünen adı|Dize|Merhaba görüntülemek hello abonelik adı|  
  
##  <a name="UserAccountInfo"></a>Kullanıcı hesabı bilgileri  
 Merhaba `user account info` varlık hello aşağıdaki özelliklere sahiptir.  
  
|Özellik|Tür|Açıklama|  
|--------------|----------|-----------------|  
|FirstName|Dize|İlk adı. Boş olmamalıdır. En fazla 100 karakter olabilir.|  
|Soyadı|Dize|Soyadı. Boş olmamalıdır. En fazla 100 karakter olabilir.|  
|E-posta|Dize|E-posta adresi. Boş olmamalı ve hello hizmet örneği içinde benzersiz olmalıdır. En fazla uzunluğu 254 karakter olabilir.|  
|Parola|Dize|Kullanıcı hesabı parolası.|  
|NameIdentifier|Dize|Tanımlayıcı, hello hello kullanıcı e-postalara aynı hesap.|  
|ProviderName|Dize|Kimlik doğrulama sağlayıcısının adı.|  
|IsBasicAccount|Boole değeri|Bu hesabın e-posta ve parola kullanarak kaydolduysanız true; Merhaba hesap bir sağlayıcı kullanarak kaydolduysanız yanlış.|  
  
##  <a name="UseSignIn"></a>Kullanıcı oturum açma  
 Merhaba `user sign in` varlık hello aşağıdaki özelliklere sahiptir.  
  
|Özellik|Tür|Açıklama|  
|--------------|----------|-----------------|  
|E-posta|Dize|E-posta adresi. Boş olmamalı ve hello hizmet örneği içinde benzersiz olmalıdır. En fazla uzunluğu 254 karakter olabilir.|  
|Parola|Dize|Kullanıcı hesabı parolası.|  
|ReturnUrl|Dize|Merhaba kullanıcı oturum açma tıklattığınız hello sayfasının Hello URL'si.|  
|Kullandığınız Beni anımsa|Boole değeri|Olup toosave mevcut kullanıcının bilgileri hello.|  
|RegistrationEnabled|Boole değeri|Kayıt etkinleştirilip etkinleştirilmediği.|  
|DelegationEnabled|Boole değeri|Temsilci oturum açma etkinleştirilip etkinleştirilmediği.|  
|DelegationUrl|Dize|Merhaba, URL'de oturum etkinleştirilirse temsilci.|  
|SsoSignUpUrl|Dize|Merhaba tek oturum URL'yi hello kullanıcıdan varsa.|  
|AuxServiceUrl|Dize|Merhaba geçerli kullanıcı bir yöneticiyse, bir bağlantı toohello hizmet örneği hello Klasik Azure Portalı'nda budur.|  
|Sağlayıcılar|Koleksiyonu [sağlayıcı](#Provider) varlıklar|Bu kullanıcı için kimlik doğrulama sağlayıcıları hello.|  
|UserRegistrationTerms|Dize|Bir kullanıcı oturum açma toobefore kabul etmelidirler koşulları.|  
|UserRegistrationTermsEnabled|Boole değeri|Koşulları etkinleştirilip etkinleştirilmediği.|  
  
##  <a name="UserSignUp"></a>Kullanıcı Kaydolma  
 Merhaba `user sign up` varlık hello aşağıdaki özelliklere sahiptir.  
  
|Özellik|Tür|Açıklama|  
|--------------|----------|-----------------|  
|PasswordConfirm|Boole değeri|Merhaba tarafından kullanılan değer [kaydolma](api-management-page-controls.md#sign-up)kaydolma denetim.|  
|Parola|Dize|Kullanıcı hesabı parolası.|  
|PasswordVerdictLevel|Sayı|Merhaba tarafından kullanılan değer [kaydolma](api-management-page-controls.md#sign-up)kaydolma denetim.|  
|UserRegistrationTerms|Dize|Bir kullanıcı oturum açma toobefore kabul etmelidirler koşulları.|  
|UserRegistrationTermsOptions|Sayı|Merhaba tarafından kullanılan değer [kaydolma](api-management-page-controls.md#sign-up)kaydolma denetim.|  
|ConsentAccepted|Boole değeri|Merhaba tarafından kullanılan değer [kaydolma](api-management-page-controls.md#sign-up)kaydolma denetim.|  
|E-posta|Dize|E-posta adresi. Boş olmamalı ve hello hizmet örneği içinde benzersiz olmalıdır. En fazla uzunluğu 254 karakter olabilir.|  
|FirstName|Dize|İlk adı. Boş olmamalıdır. En fazla 100 karakter olabilir.|  
|Soyadı|Dize|Soyadı. Boş olmamalıdır. En fazla 100 karakter olabilir.|  
|UserData|Dize|Merhaba tarafından kullanılan değer [kaydolma](api-management-page-controls.md#sign-up) denetim.|  
|NameIdentifier|Dize|Merhaba tarafından kullanılan değer [kaydolma](api-management-page-controls.md#sign-up)kaydolma denetim.|  
|ProviderName|Dize|Kimlik doğrulama sağlayıcısının adı.|

## <a name="next-steps"></a>Sonraki adımlar
Şablonları ile çalışma hakkında daha fazla bilgi için bkz: [nasıl toocustomize hello şablonları kullanarak API Management Geliştirici Portalı](api-management-developer-portal-templates.md).
