---
title: "aaaAzure API Management şablonu kaynakları | Microsoft Docs"
description: "Azure API Management'ta Geliştirici Portalı şablonları kullanmak için kullanılabilir kaynakları hello türleri hakkında bilgi edinin."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 51a1b4c6-a9fd-4524-9e0e-03a9800c3e94
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 2221e3852986d485d13817b483e473dfe451d3c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-template-resources"></a>Azure API Management şablonu kaynakları
Azure API Management şablonlarda hello Geliştirici Portalı kaynak türleri aşağıdaki hello sağlar.  
  
-   [Dize kaynakları](#strings)  
  
-   [Karakter kaynakları](#glyphs)  
  
##  <a name="strings"></a>Dize kaynakları  
 API Management hello Geliştirici Portalı kullanmak için dize kaynaklarını kapsamlı bir kümesini sağlar. API Management tarafından desteklenen hello dillerin tümünün içine yerelleştirilmiş bu kaynakları. Merhaba varsayılan şablonları kümesini bu kaynakları sayfa üstbilgilerinde, etiketler ve hello Geliştirici Portalı'nda görüntülenen tüm sabit dizeler için kullanır. toouse şablonlarınızı dize kaynak hello aşağıdaki örnekte gösterildiği gibi hello dize, adından hello kaynak dize öneki belirtin.  
  
```  
{% localized "Prefix|Name" %}  
  
```  
  
 Merhaba aşağıdaki örnek hello ürün listesi şablondan ve görüntüler **ürünleri** hello sayfanın üst kısmındaki hello.  
  
```  
<h2>{% localized "ProductsStrings|PageTitleProducts" %}</h2>  
  
```  
  
 Tablolar hello dize kaynaklarını Geliştirici Portalı şablonlarınızı kullanılmak için aşağıdaki toohello bakın. Merhaba tablo adı için bu tablodaki hello dize kaynaklarını hello önek olarak kullanın.  
  
-   [ApisStrings](#ApisStrings)  
  
-   [ApplicationListStrings](#ApplicationListStrings)  
  
-   [AppDetailsStrings](#AppDetailsStrings)  
  
-   [AppStrings](#AppStrings)  
  
-   [CommonResources](#CommonResources)  
  
-   [CommonStrings](#CommonStrings)  
  
-   [Belgeleri](#Documentation)  
  
-   [ErrorPageStrings](#ErrorPageStrings)  
  
-   [IssuesStrings](#IssuesStrings)  
  
-   [NotFoundStrings](#NotFoundStrings)  
  
-   [ProductDetailsStrings](#ProductDetailsStrings)  
  
-   [ProductsStrings](#ProductsStrings)  
  
-   [ProviderInfoStrings](#ProviderInfoStrings)  
  
-   [SigninResources](#SigninResources)  
  
-   [SigninStrings](#SigninStrings)  
  
-   [SignupStrings](#SignupStrings)  
  
-   [SubscriptionListStrings](#SubscriptionListStrings)  
  
-   [SubscriptionStrings](#SubscriptionStrings)  
  
-   [UpdateProfileStrings](#UpdateProfileStrings)  
  
-   [Kullanıcı profili](#UserProfile)  
  
###  <a name="ApisStrings"></a>ApisStrings  
  
|Ad|Metin|  
|----------|----------|  
|PageTitleApis|API'ler|  
  
###  <a name="AppDetailsStrings"></a>AppDetailsStrings  
  
|Ad|Metin|  
|----------|----------|  
|WebApplicationsDetailsTitle|Uygulama Önizleme|  
|WebApplicationsRequirementsHeader|Gereksinimler|  
|WebApplicationsScreenshotAlt|ekran görüntüsü|  
|WebApplicationsScreenshotsHeader|Ekran görüntüleri|  
  
###  <a name="ApplicationListStrings"></a>ApplicationListStrings  
  
|Ad|Metin|  
|----------|----------|  
|WebDevelopersAppDeleteConfirmation|Tooremove uygulama istediğinizden emin misiniz?|  
|WebDevelopersAppNotPublished|Yayımlanmadı|  
|WebDevelopersAppNotSubminted|Gönderilemedi|  
|WebDevelopersAppTableCategoryHeader|Kategori|  
|WebDevelopersAppTableNameHeader|Ad|  
|WebDevelopersAppTableStateHeader|Durum|  
|WebDevelopersEditLink|Düzenle|  
|WebDevelopersRegisterAppLink|Uygulamayı Kaydet|  
|WebDevelopersRemoveLink|Kaldır|  
|WebDevelopersSubmitLink|Gönder|  
|WebDevelopersYourApplicationsHeader|Uygulamalarınızı|  
  
###  <a name="AppStrings"></a>AppStrings  
  
|Ad|Metin|  
|----------|----------|  
|WebApplicationsHeader|Uygulamalar|  
  
###  <a name="CommonResources"></a>CommonResources  
  
|Ad|Metin|  
|----------|----------|  
|NoItemsToDisplay|Sonuç bulunamadı.|  
|GeneralExceptionMessage|Bir şey doğru değil. Geçici bir hata veya bir hata olabilir. Lütfen yeniden deneyin.|  
|GeneralJsonExceptionMessage|Bir şey doğru değil. Geçici bir hata veya bir hata olabilir. Lütfen hello sayfayı yeniden yükleyin ve yeniden deneyin.|  
|ConfirmationMessageUnsavedChanges|Bazı kaydedilmemiş değişiklikler var. Toocancel istediğiniz ve hello değişiklikleri atmak emin misiniz?|  
|AzureActiveDirectory|Azure Active Directory|  
|HttpLargeRequestMessage|HTTP istek gövdesi çok büyük.|  
  
###  <a name="CommonStrings"></a>CommonStrings  
  
|Ad|Metin|  
|----------|----------|  
|ButtonLabelCancel|İptal|  
|ButtonLabelSave|Kaydet|  
|GeneralExceptionMessage|Bir şey doğru değil. Geçici bir hata veya bir hata olabilir. Lütfen yeniden deneyin.|  
|NoItemsToDisplay|Hiçbir öğe toodisplay vardır.|  
|PagerButtonLabelFirst|İlk|  
|PagerButtonLabelLast|Son|  
|PagerButtonLabelNext|Sonraki|  
|PagerButtonLabelPrevious|Önceki|  
|PagerLabelPageNOfM|{0} {1}|  
|PasswordTooShort|Merhaba parola çok kısa|  
|EmailAsPassword|E-posta parolanızı kullanmayın|  
|PasswordSameAsUserName|Parolanız kullanıcı adınızı içeremez|  
|PasswordTwoCharacterClasses|Farklı karakter sınıflarını kullanma|  
|PasswordTooManyRepetitions|Çok fazla tekrarları|  
|PasswordSequenceFound|Parolanızı sıraları içerir|  
|PagerLabelPageSize|Sayfa boyutu|  
|CurtainLabelLoading|Yükleniyor...|  
|TablePlaceholderNothingToDisplay|Veri yok seçili hello dönemi ve kapsamı|  
|ButtonLabelClose|Kapat|  
  
###  <a name="Documentation"></a>Belgeleri  
  
|Ad|Metin|  
|----------|----------|  
|WebDocumentationInvalidHeaderErrorMessage|Geçersiz üstbilgi '{0}'|  
|WebDocumentationInvalidRequestErrorMessage|Geçersiz istek URL'si|  
|TextboxLabelAccessToken|Erişim belirteci *|  
|DropdownOptionPrimaryKeyFormat|Birincil-{0}|  
|DropdownOptionSecondaryKeyFormat|İkincil-{0}|  
|WebDocumentationSubscriptionKeyText|Abonelik anahtarınızı|  
|WebDocumentationTemplatesAddHeaders|Gerekli HTTP üst bilgisi Ekle|  
|WebDocumentationTemplatesBasicAuthSample|Temel yetkilendirme örneği|  
|WebDocumentationTemplatesCurlForBasicAuth|Temel yetkilendirme kullanmak için:--kullanıcı {username}: {parola}|  
|WebDocumentationTemplatesCurlValuesForPath|Yolu parametreleri ({...} gösterilir), abonelik anahtarı ve sorgu parametreleri için değerleri için değerleri belirtin|  
|WebDocumentationTemplatesDeveloperKey|Abonelik anahtarınızı belirtin|  
|WebDocumentationTemplatesJavaApache|Bu örnek hello Apache HTTP istemci HTTP bileşenlerden (http://hc.apache.org/httpcomponents-client-ga/) kullanır|  
|WebDocumentationTemplatesOptionalParams|Gerektiğinde isteğe bağlı parametre değerlerini belirtin|  
|WebDocumentationTemplatesPhpPackage|Bu örnek hello HTTP_Request2 paketi kullanır. (daha fazla bilgi için: http://pear.php.net/package/HTTP_Request2)|  
|WebDocumentationTemplatesPythonValuesForPath|({...} Gösterilir) yolu parametrelerin değerlerini belirtin ve gerekirse istek gövdesinde|  
|WebDocumentationTemplatesRequestBody|İstek gövdesini belirtin|  
|WebDocumentationTemplatesRequiredParams|Merhaba şu parametreler için değerleri belirtin|  
|WebDocumentationTemplatesValuesForPath|({...} Gösterilir) yolu parametrelerin değerlerini belirtin|  
|OAuth2AuthorizationEndpointDescription|Merhaba yetkilendirme uç noktası kullanılan toointeract hello kaynak sahibi olan ve bir yetkilendirme verme alın.|  
|OAuth2AuthorizationEndpointName|Yetkilendirme uç noktası|  
|OAuth2TokenEndpointDescription|Merhaba belirteç uç noktası kullanılır tarafından hello istemci tooobtain kendi yetkilendirme sunarak bir erişim belirteci vermek veya yenileme belirteci.|  
|OAuth2TokenEndpointName|belirteç uç noktası|  
|OAuth2Flow_AuthorizationCodeGrant_Step_AuthorizationRequest_Description|< p\> hello istemci hello kaynak sahibinin kullanıcı aracısı toohello yetkilendirme uç noktası yönlendirerek hello akış başlatır.  Merhaba istemcisi kendi istemci tanımlayıcısı, istenen kapsamı, yerel durum içerir ve geri erişim izni (engellendi veya sonra) bir yeniden yönlendirme URI'si toowhich hello yetkilendirme sunucusu hello Kullanıcı aracısını gönderir.     < /p\> < p\> hello yetkilendirme sunucusu hello kaynak sahibi (aracılığıyla hello kullanıcı aracısı) kimliğini doğrular ve hello kaynak sahibi verir veya hello istemcinin erişim isteği reddeder olup olmadığını belirler.     < /p\> < p\> hello kaynak sahibine erişim verir varsayıldığında, hello yetkilendirme sunucusu hello yeniden yönlendirme URI'si sağlanan kullanarak hello kullanıcı aracısı geri toohello istemciyi yönlendirir (Merhaba isteğindeki veya temcilerin sırasında önceki t kaydı).  Merhaba yeniden yönlendirme URI'si bir yetkilendirme kodu ve daha önce hello istemci tarafından sağlanan herhangi bir yerel durumu içerir.     < /p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_AuthorizationRequest_ErrorDescription|< p\> hello isteği geçersizse hello kullanıcı hello erişim isteği reddeder, hello istemci şu parametreler toohello yeniden yönlendirme eklenen hello kullanarak bildirilir: < /p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_AuthorizationRequest_Name|Yetkilendirme isteği|  
|OAuth2Flow_AuthorizationCodeGrant_Step_AuthorizationRequest_RequestDescription|< p\> hello istemci uygulaması hello kullanıcı toohello yetkilendirme uç noktası sipariş tooinitiate hello OAuth işlem Gönder gerekir.          Merhaba yetkilendirme uç noktada hello kullanıcı kimliğini doğrular ve ardından verir veya erişimi toohello uygulama reddeder.     < /p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_AuthorizationRequest_ResponseDescription|< p\> hello kaynak sahibine erişim verir varsayıldığında, yetkilendirme sunucusu hello yeniden yönlendirme URI'si sağlanan kullanan hello kullanıcı aracısı geri toohello istemci yönlendiren önceki (Merhaba isteğindeki veya istemci kaydı sırasında).  Merhaba yeniden yönlendirme URI'si bir yetkilendirme kodu ve daha önce hello istemci tarafından sağlanan herhangi bir yerel durumu içerir. < /p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_TokenRequest_Description|< p\> hello istemci isteklerini bir erişim belirteci hello yetkilendirme sunucusundan '' hello önceki adımda aldığınız hello yetkilendirme kodu ekleyerek s belirteç uç noktası.  Merhaba isteği yapılırken hello istemci hello yetkilendirme sunucusuyla kimliğini doğrular.  Merhaba istemci doğrulaması için hello yeniden yönlendirme kullanılan URI tooobtain hello yetkilendirme kodu içerir. < /p\> < p\> hello yetkilendirme sunucusu hello istemci kimliğini doğrular, hello yetkilendirme kodu doğrular ve bu hello yeniden yönlendirme URI'si alınan eşleşmeleri hello URI kullanılan tooredirect hello istemci adım (C) sağlar.  Geçerliyse, hello yetkilendirme sunucusu geri bir erişim belirteci ve bir yenileme belirteci ile isteğe bağlı olarak yanıt verir. < /p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_TokenRequest_ErrorDescription|< p\> hello isteği istemci kimlik doğrulaması başarısız oldu veya geçersizse hello yetkilendirme sunucusu (Aksi belirtilmediği sürece) bir HTTP 400 (Hatalı istek) durum koduyla yanıt verir ve şu parametreler hello yanıt hello içerir. < /p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_TokenRequest_RequestDescription|< p\> hello istemci şu parametreler bir karakter UTF-8 hello HTTP isteğinin varlık gövdesinde kodlama ile Merhaba "uygulama/x-www-form-urlencoded" biçimini kullanarak hello göndererek bir istek toohello belirteç uç noktası sağlar. < /p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_TokenRequest_ResponseDescription|< p\> hello yetkilendirme sunucusu, bir erişim belirteci ve isteğe bağlı yenileme belirteci verir ve yapıları parametreleri toohello Varlık gövdesi 200 (Tamam) durum kodlu hello HTTP yanıtının aşağıdaki hello ekleyerek yanıt hello. < /p\>|  
|OAuth2Flow_ClientCredentialsGrant_Step_TokenRequest_Description|< p\> hello istemci hello yetkilendirme ile kimlik doğrulamasını ve bir erişim belirteci hello belirteç uç noktasından ister. < /p\> < p\> hello yetkilendirme sunucusu hello istemci kimliğini doğrular ve geçerliyse, bir erişim belirteci verir. < /p\>|  
|OAuth2Flow_ClientCredentialsGrant_Step_TokenRequest_ErrorDescription|< p\> hello isteği istemci kimlik doğrulaması başarısız oldu veya geçersizse hello yetkilendirme sunucusu (Aksi belirtilmediği sürece) bir HTTP 400 (Hatalı istek) durum koduyla yanıt verir ve şu parametreler hello yanıt hello içerir. < /p\>|  
|OAuth2Flow_ClientCredentialsGrant_Step_TokenRequest_RequestDescription|< p\> hello istemci şu parametreler bir karakter UTF-8 hello HTTP isteğinin varlık gövdesinde kodlama ile Merhaba "uygulama/x-www-form-urlencoded" biçimini kullanarak hello ekleyerek bir istek toohello belirteç uç noktası sağlar. < /p\>|  
|OAuth2Flow_ClientCredentialsGrant_Step_TokenRequest_ResponseDescription|< p\> hello erişim belirteci isteği geçerli olduğundan ve yetkili hello yetkilendirme sunucusu, bir erişim belirteci ve isteğe bağlı yenileme belirteci verir ve yapıları parametreleri toohello-URI'den hello HTTP aşağıdaki hello ekleyerek yanıt hello (Tamam) 200 durum koduyla yanıt. < /p\>|  
|OAuth2Flow_ImplicitGrant_Step_AuthorizationRequest_Description|< p\> hello istemci hello kaynak sahibi yönlendirerek hello akış başlatır '' s kullanıcı aracısı toohello yetkilendirme uç noktası.  Merhaba istemcisi kendi istemci tanımlayıcısı, istenen kapsamı, yerel durum içerir ve geri erişim izni (engellendi veya sonra) bir yeniden yönlendirme URI'si toowhich hello yetkilendirme sunucusu hello Kullanıcı aracısını gönderir. < /p\> < p\> hello yetkilendirme sunucusu hello kaynak sahibi (aracılığıyla hello kullanıcı aracısı) kimliğini doğrular ve hello kaynak sahibi verir veya hello istemci engellediği olup olmadığını belirler. '' s erişim isteği. < /p\> < p\> hello kaynak sahibine erişim verir varsayıldığında, hello yetkilendirme sunucusu URI sağlanan önceki hello yeniden yönlendirmeyi kullanma hello kullanıcı aracısı geri toohello istemciyi yönlendirir.  Merhaba yeniden yönlendirme URI'si hello erişim belirteci hello URI parçadaki içerir. < /p\>|  
|OAuth2Flow_ImplicitGrant_Step_AuthorizationRequest_ErrorDescription|< p\> hello kaynak sahibi hello erişim isteği reddeder veya eksik veya geçersiz yeniden yönlendirme URI'si dışında nedenlerle hello isteği başarısız olursa, hello yetkilendirme sunucusu parametreleri toohello fragme aşağıdaki hello ekleyerek hello istemci bildirir. nt bileşen hello yeniden yönlendirme URI'si kullanma "uygulama/x-www-form-urlencoded" biçiminde hello. < /p\>|  
|OAuth2Flow_ImplicitGrant_Step_AuthorizationRequest_RequestDescription|< p\> hello istemci uygulaması hello kullanıcı toohello yetkilendirme uç noktası sipariş tooinitiate hello OAuth işlem Gönder gerekir.      Merhaba yetkilendirme uç noktada hello kullanıcı kimliğini doğrular ve ardından verir veya erişimi toohello uygulama reddeder. < /p\>|  
|OAuth2Flow_ImplicitGrant_Step_AuthorizationRequest_ResponseDescription|< p\> hello kaynak sahibi hello erişim isteği verirse hello yetkilendirme sunucusu bir erişim belirteci verir ve aşağıdaki parametreleri toohello parça hello yeniden yönlendirme URI'si bileşeninin hello ekleyerek toohello istemci sunar hello kullanarak "a Uygulama/x-www-form-urlencoded"biçimi. < /p\>|  
|OAuth2Flow_ObtainAuthorization_AuthorizationCodeGrant_Description|Yetkilendirme kodu akışını kimlik bilgilerini (PHP, Java, Python, Ruby, ASP.NET, vb. kullanılarak uygulanan örn., web sunucusu uygulamaları.) hello gizliliğini koruma özellikli istemciler için optimize edilmiştir.|  
|OAuth2Flow_ObtainAuthorization_AuthorizationCodeGrant_Name|Yetkilendirme kodu verme|  
|OAuth2Flow_ObtainAuthorization_ClientCredentialsGrant_Description|İstemci kimlik bilgileri akışının hello istemci (uygulamanızı), denetimi altındaki toohello korumalı kaynaklara erişmek istiyor olduğu durumlarda uygundur. Son kullanıcı etkileşimi gerekli olacak şekilde hello istemci kaynak sahibi olarak kabul edilir.|  
|OAuth2Flow_ObtainAuthorization_ClientCredentialsGrant_Name|İstemci kimlik bilgileri sağlama|  
|OAuth2Flow_ObtainAuthorization_ImplicitGrant_Description|Örtük akış kendi kimlik bilgileri bilinen toooperate belirli bir yeniden yönlendirme URI'si hello gizliliğini koruma kapasitesine sahip olmayan istemciler için optimize edilmiştir. Bu istemciler, genellikle bir tarayıcısında JavaScript gibi bir komut dosyası dili kullanılarak uygulanır.|  
|OAuth2Flow_ObtainAuthorization_ImplicitGrant_Name|Kapalı verin|  
|OAuth2Flow_ObtainAuthorization_ResourceOwnerPasswordCredentialsGrant_Description|Kaynak sahibi parolası kimlik bilgileri akışını hello kaynak sahibine bir güven ilişkisi hello istemci (uygulamanızı) hello aygıt işletim sistemi veya yüksek ayrıcalıklı bir uygulama gibi olması durumunda uygundur. Bu akış hello kaynak sahibinin kimlik bilgilerini (kullanıcı adı ve parola, genellikle etkileşimli form kullanarak) elde etme olasılığı özellikli istemciler için uygundur.|  
|OAuth2Flow_ObtainAuthorization_ResourceOwnerPasswordCredentialsGrant_Name|Kaynak sahibi parolası kimlik bilgileri verin|  
|OAuth2Flow_ResourceOwnerPasswordCredentialsGrant_Step_TokenRequest_Description|< p\> hello kaynak sahibi, kullanıcı adı ve parola ile Merhaba istemci sağlar. < /p\> < p\> hello istemci isteklerini bir erişim belirteci hello yetkilendirme sunucusundan '' hello kaynak sahibinden alınan hello kimlik bilgileri de dahil olmak üzere tarafından kullanılan s belirteç uç noktası.  Merhaba isteği yapılırken hello istemci hello yetkilendirme sunucusuyla kimliğini doğrular. < /p\> < p\> hello yetkilendirme sunucusu hello istemci kimlik doğrulaması hello kaynak sahibi kimlik bilgilerini doğrular ve geçerliyse, bir erişim belirteci verir. < /p\>|  
|OAuth2Flow_ResourceOwnerPasswordCredentialsGrant_Step_TokenRequest_ErrorDescription|< p\> hello isteği istemci kimlik doğrulaması başarısız oldu veya geçersizse hello yetkilendirme sunucusu (Aksi belirtilmediği sürece) bir HTTP 400 (Hatalı istek) durum koduyla yanıt verir ve şu parametreler hello yanıt hello içerir. < /p\>|  
|OAuth2Flow_ResourceOwnerPasswordCredentialsGrant_Step_TokenRequest_RequestDescription|< p\> hello istemci şu parametreler bir karakter UTF-8 hello HTTP isteğinin varlık gövdesinde kodlama ile Merhaba "uygulama/x-www-form-urlencoded" biçimini kullanarak hello ekleyerek bir istek toohello belirteç uç noktası sağlar. < /p\>|  
|OAuth2Flow_ResourceOwnerPasswordCredentialsGrant_Step_TokenRequest_ResponseDescription|< p\> hello erişim belirteci isteği geçerli olduğundan ve yetkili hello yetkilendirme sunucusu, bir erişim belirteci ve isteğe bağlı yenileme belirteci verir ve yapıları parametreleri toohello-URI'den hello HTTP respo aşağıdaki hello ekleyerek yanıt hello nse 200 (Tamam) durum koduna sahip. < /p\>|  
|OAuth2Step_AccessTokenRequest_Name|Erişim belirteci isteği|  
|OAuth2Step_AuthorizationRequest_Name|Yetkilendirme isteği|  
|OAuth2AccessToken_AuthorizationCodeGrant_TokenResponse|GEREKLİ. Merhaba erişim belirteci Hello yetkilendirme sunucusu tarafından verilmiş.|  
|OAuth2AccessToken_ClientCredentialsGrant_TokenResponse|GEREKLİ. Merhaba erişim belirteci Hello yetkilendirme sunucusu tarafından verilmiş.|  
|OAuth2AccessToken_ImplicitGrant_AuthorizationResponse|GEREKLİ. Merhaba erişim belirteci Hello yetkilendirme sunucusu tarafından verilmiş.|  
|OAuth2AccessToken_ResourceOwnerPasswordCredentialsGrant_TokenResponse|GEREKLİ. Merhaba erişim belirteci Hello yetkilendirme sunucusu tarafından verilmiş.|  
|OAuth2ClientId_AuthorizationCodeGrant_AuthorizationRequest|GEREKLİ. İstemci tanımlayıcısı.|  
|OAuth2ClientId_AuthorizationCodeGrant_TokenRequest|Merhaba istemci hello yetkilendirme sunucusu ile kimlik doğrulaması değil, gerekli.|  
|OAuth2ClientId_ImplicitGrant_AuthorizationRequest|GEREKLİ. Merhaba istemci tanımlayıcısı.|  
|OAuth2Code_AuthorizationCodeGrant_AuthorizationResponse|GEREKLİ. Merhaba yetkilendirme kodu Hello yetkilendirme sunucusu tarafından oluşturulmuş.|  
|OAuth2Code_AuthorizationCodeGrant_TokenRequest|GEREKLİ. Merhaba yetkilendirme sunucusundan alınan hello yetkilendirme kodu.|  
|OAuth2ErrorDescription_AuthorizationCodeGrant_AuthorizationErrorResponse|İSTEĞE BAĞLI. Ek bilgi sağlayan okunabilir ASCII metni.|  
|OAuth2ErrorDescription_AuthorizationCodeGrant_TokenErrorResponse|İSTEĞE BAĞLI. Ek bilgi sağlayan okunabilir ASCII metni.|  
|OAuth2ErrorDescription_ClientCredentialsGrant_TokenErrorResponse|İSTEĞE BAĞLI. Ek bilgi sağlayan okunabilir ASCII metni.|  
|OAuth2ErrorDescription_ImplicitGrant_AuthorizationErrorResponse|İSTEĞE BAĞLI. Ek bilgi sağlayan okunabilir ASCII metni.|  
|OAuth2ErrorDescription_ResourceOwnerPasswordCredentialsGrant_TokenErrorResponse|İSTEĞE BAĞLI. Ek bilgi sağlayan okunabilir ASCII metni.|  
|OAuth2ErrorUri_AuthorizationCodeGrant_AuthorizationErrorResponse|İSTEĞE BAĞLI. Merhaba hata hakkında bilgi içeren okunabilir bir web sayfası tanımlayan bir URI.|  
|OAuth2ErrorUri_AuthorizationCodeGrant_TokenErrorResponse|İSTEĞE BAĞLI. Merhaba hata hakkında bilgi içeren okunabilir bir web sayfası tanımlayan bir URI.|  
|OAuth2ErrorUri_ClientCredentialsGrant_TokenErrorResponse|İSTEĞE BAĞLI. Merhaba hata hakkında bilgi içeren okunabilir bir web sayfası tanımlayan bir URI.|  
|OAuth2ErrorUri_ImplicitGrant_AuthorizationErrorResponse|İSTEĞE BAĞLI. Merhaba hata hakkında bilgi içeren okunabilir bir web sayfası tanımlayan bir URI.|  
|OAuth2ErrorUri_ResourceOwnerPasswordCredentialsGrant_TokenErrorResponse|İSTEĞE BAĞLI. Merhaba hata hakkında bilgi içeren okunabilir bir web sayfası tanımlayan bir URI.|  
|OAuth2Error_AuthorizationCodeGrant_AuthorizationErrorResponse|GEREKLİ. Merhaba aşağıdaki tek bir ASCII hata kodu: invalid_request, unauthorized_client, ACCESS_DENIED, unsupported_response_type, invalid_scope, server_error, temporarily_unavailable.|  
|OAuth2Error_AuthorizationCodeGrant_TokenErrorResponse|GEREKLİ. Merhaba aşağıdaki tek bir ASCII hata kodu: invalid_request, invalid_client, invalid_grant, unauthorized_client, unsupported_grant_type, invalid_scope.|  
|OAuth2Error_ClientCredentialsGrant_TokenErrorResponse|GEREKLİ. Merhaba aşağıdaki tek bir ASCII hata kodu: invalid_request, invalid_client, invalid_grant, unauthorized_client, unsupported_grant_type, invalid_scope.|  
|OAuth2Error_ImplicitGrant_AuthorizationErrorResponse|GEREKLİ. Merhaba aşağıdaki tek bir ASCII hata kodu: invalid_request, unauthorized_client, ACCESS_DENIED, unsupported_response_type, invalid_scope, server_error, temporarily_unavailable.|  
|OAuth2Error_ResourceOwnerPasswordCredentialsGrant_TokenErrorResponse|GEREKLİ. Merhaba aşağıdaki tek bir ASCII hata kodu: invalid_request, invalid_client, invalid_grant, unauthorized_client, unsupported_grant_type, invalid_scope.|  
|OAuth2ExpiresIn_AuthorizationCodeGrant_TokenResponse|ÖNERİLİR. Merhaba erişim belirtecinin saniye cinsinden Hello yaşam süresi.|  
|OAuth2ExpiresIn_ClientCredentialsGrant_TokenResponse|ÖNERİLİR. Merhaba erişim belirtecinin saniye cinsinden Hello yaşam süresi.|  
|OAuth2ExpiresIn_ImplicitGrant_AuthorizationResponse|ÖNERİLİR. Merhaba erişim belirtecinin saniye cinsinden Hello yaşam süresi.|  
|OAuth2ExpiresIn_ResourceOwnerPasswordCredentialsGrant_TokenResponse|ÖNERİLİR. Merhaba erişim belirtecinin saniye cinsinden Hello yaşam süresi.|  
|OAuth2GrantType_AuthorizationCodeGrant_TokenRequest|GEREKLİ. Değeri çok ayarlanmalıdır "authorization_code".|  
|OAuth2GrantType_ClientCredentialsGrant_TokenRequest|GEREKLİ. Değeri çok ayarlanmalıdır "client_credentials".|  
|OAuth2GrantType_ResourceOwnerPasswordCredentialsGrant_TokenRequest|GEREKLİ. Değeri çok ayarlanmalıdır "parola".|  
|OAuth2Password_ResourceOwnerPasswordCredentialsGrant_TokenRequest|GEREKLİ. Merhaba kaynak sahibi parolası.|  
|OAuth2RedirectUri_AuthorizationCodeGrant_AuthorizationRequest|İSTEĞE BAĞLI. Merhaba yeniden yönlendirme uç noktası URI mutlak URI olmalıdır.|  
|OAuth2RedirectUri_AuthorizationCodeGrant_TokenRequest|GEREKLİ Hello "redirect_uri" parametresi hello yetkilendirme isteğine dahil ve bunların değerleri aynı olmalıdır.|  
|OAuth2RedirectUri_ImplicitGrant_AuthorizationRequest|İSTEĞE BAĞLI. Merhaba yeniden yönlendirme uç noktası URI mutlak URI olmalıdır.|  
|OAuth2RefreshToken_AuthorizationCodeGrant_TokenResponse|İSTEĞE BAĞLI. kullanılan tooobtain yeni erişim belirteçleri olabilir hello yenileme belirteci.|  
|OAuth2RefreshToken_ClientCredentialsGrant_TokenResponse|İSTEĞE BAĞLI. kullanılan tooobtain yeni erişim belirteçleri olabilir hello yenileme belirteci.|  
|OAuth2RefreshToken_ResourceOwnerPasswordCredentialsGrant_TokenResponse|İSTEĞE BAĞLI. kullanılan tooobtain yeni erişim belirteçleri olabilir hello yenileme belirteci.|  
|OAuth2ResponseType_AuthorizationCodeGrant_AuthorizationRequest|GEREKLİ. Değer ayarlanmalıdır çok "code".|  
|OAuth2ResponseType_ImplicitGrant_AuthorizationRequest|GEREKLİ. Değer "token" çok ayarlamanız gerekir.|  
|OAuth2Scope_AuthorizationCodeGrant_AuthorizationRequest|İSTEĞE BAĞLI. Merhaba erişim isteği Hello kapsamı.|  
|OAuth2Scope_AuthorizationCodeGrant_TokenResponse|Aynı toohello kapsam hello istemci tarafından istendiğinde isteğe BAĞLIDIR; Aksi takdirde, gerekli.|  
|OAuth2Scope_ClientCredentialsGrant_TokenRequest|İSTEĞE BAĞLI. Merhaba erişim isteği Hello kapsamı.|  
|OAuth2Scope_ClientCredentialsGrant_TokenResponse|İsteğe bağlı, aynı ise toohello kapsamı Hello istemci tarafından istenilen; Aksi takdirde, gerekli.|  
|OAuth2Scope_ImplicitGrant_AuthorizationRequest|İSTEĞE BAĞLI. Merhaba erişim isteği Hello kapsamı.|  
|OAuth2Scope_ImplicitGrant_AuthorizationResponse|Aynı toohello kapsam hello istemci tarafından istendiğinde isteğe BAĞLIDIR; Aksi takdirde, gerekli.|  
|OAuth2Scope_ResourceOwnerPasswordCredentialsGrant_TokenRequest|İSTEĞE BAĞLI. Merhaba erişim isteği Hello kapsamı.|  
|OAuth2Scope_ResourceOwnerPasswordCredentialsGrant_TokenResponse|İsteğe bağlı, aynı ise toohello kapsamı Hello istemci tarafından istenilen; Aksi takdirde, gerekli.|  
|OAuth2State_AuthorizationCodeGrant_AuthorizationErrorResponse|Merhaba "Durum" parametresi hello istemci yetkilendirme istekte mevcut olup olmadığını gerekli.  Merhaba istemciden alınan hello tam bir değer.|  
|OAuth2State_AuthorizationCodeGrant_AuthorizationRequest|ÖNERİLİR. Merhaba istemci toomaintain durumu hello istek geri çağırma arasındaki tarafından kullanılan genel olmayan bir değer.  Merhaba yetkilendirme sunucusu hello kullanıcı aracısı geri toohello istemci yönlendirirken bu değeri içerir.  Merhaba parametresi, siteler arası istek sahteciliğini önleme için kullanılmalıdır.|  
|OAuth2State_AuthorizationCodeGrant_AuthorizationResponse|Merhaba "Durum" parametresi hello istemci yetkilendirme istekte mevcut olup olmadığını gerekli.  Merhaba istemciden alınan hello tam bir değer.|  
|OAuth2State_ImplicitGrant_AuthorizationErrorResponse|Merhaba "Durum" parametresi hello istemci yetkilendirme istekte mevcut olup olmadığını gerekli.  Merhaba istemciden alınan hello tam bir değer.|  
|OAuth2State_ImplicitGrant_AuthorizationRequest|ÖNERİLİR. Merhaba istemci toomaintain durumu hello istek geri çağırma arasındaki tarafından kullanılan genel olmayan bir değer.  Merhaba yetkilendirme sunucusu hello kullanıcı aracısı geri toohello istemci yönlendirirken bu değeri içerir.  Merhaba parametresi, siteler arası istek sahteciliğini önleme için kullanılmalıdır.|  
|OAuth2State_ImplicitGrant_AuthorizationResponse|Merhaba "Durum" parametresi hello istemci yetkilendirme istekte mevcut olup olmadığını gerekli.  Merhaba istemciden alınan hello tam bir değer.|  
|OAuth2TokenType_AuthorizationCodeGrant_TokenResponse|GEREKLİ. Merhaba belirteç Hello türü.|  
|OAuth2TokenType_ClientCredentialsGrant_TokenResponse|GEREKLİ. Merhaba belirteç Hello türü.|  
|OAuth2TokenType_ImplicitGrant_AuthorizationResponse|GEREKLİ. Merhaba belirteç Hello türü.|  
|OAuth2TokenType_ResourceOwnerPasswordCredentialsGrant_TokenResponse|GEREKLİ. Merhaba belirteç Hello türü.|  
|OAuth2UserName_ResourceOwnerPasswordCredentialsGrant_TokenRequest|GEREKLİ. Merhaba kaynak sahibi kullanıcı adı.|  
|OAuth2UnsupportedTokenType|Belirteç türü '{0}' supporetd değil.|  
|OAuth2InvalidState|Yetkilendirme sunucusundan geçersiz yanıt|  
|OAuth2GrantType_AuthorizationCode|Yetkilendirme kodu|  
|OAuth2GrantType_Implicit|Örtük|  
|OAuth2GrantType_ClientCredentials|İstemci kimlik bilgileri|  
|OAuth2GrantType_ResourceOwnerPassword|Kaynak sahibi parolası|  
|WebDocumentation302Code|302 bulundu|  
|WebDocumentation400Code|400 (Hatalı istek)|  
|OAuth2SendingMethod_AuthHeader|Authorization Üstbilgisi|  
|OAuth2SendingMethod_QueryParam|Sorgu parametresi|  
|OAuth2AuthorizationServerGeneralException|{0} üzerinden erişim yetkisi verme sırasında bir hata oluştu|  
|OAuth2AuthorizationServerCommunicationException|Bir HTTP bağlantısı tooauthorization sunucusu kurulamadı veya beklenmedik şekilde kapatıldı.|  
|WebDocumentationOAuth2GeneralErrorMessage|Beklenmeyen bir hata oluştu.|  
|AuthorizationServerCommunicationException|Yetkilendirme sunucusu iletişim özel durumu oluştu. Lütfen yöneticinize başvurun.|  
|TextblockSubscriptionKeyHeaderDescription|Erişim toothis API sağlar abonelik anahtarı. Bulunan, < bir href ='/ Geliştirici '\>profil < /a\>.|  
|TextblockOAuthHeaderDescription|OAuth 2.0 erişim belirteci elde < t\>{0} < /i\>. Desteklenen sağlama türleri: < i\>{1} < /i\>.|  
|TextblockContentTypeHeaderDescription|Merhaba gövdesi toohello API gönderilen medya türü.|  
|ErrorMessageApiNotAccessible|Merhaba toocall çalıştığınız API şu anda erişilebilir durumda değil. Lütfen hello API yayımcıya başvurun < bir href = "/ sorunlar"\>burada < /a\>.|  
|ErrorMessageApiTimedout|Merhaba toocall çalıştığınız API geri normal tooget yanıt uzun sürüyor. Lütfen hello API yayımcıya başvurun < bir href = "/ sorunlar"\>burada < /a\>.|  
|BadRequestParameterExpected|"'{0}' parametresi bekleniyor"|  
|TooltipTextDoubleClickToSelectAll|Tüm tooselect çift tıklayın.|  
|TooltipTextHideRevealSecret|Göster/Gizle|  
|ButtonLinkOpenConsole|Deneyin|  
|SectionHeadingRequestBody|İstek gövdesi|  
|SectionHeadingRequestParameters|İstek parametreleri|  
|SectionHeadingRequestUrl|İstek URL'si|  
|SectionHeadingResponse|Yanıt|  
|SectionHeadingRequestHeaders|İstek üstbilgileri|  
|FormLabelSubtextOptional|İsteğe bağlı|  
|SectionHeadingCodeSamples|Kod örnekleri|  
|TextblockOpenidConnectHeaderDescription|Openıd Connect kimliği belirteci elde < t\>{0} < /i\>. Desteklenen sağlama türleri: < i\>{1} < /i\>.|  
  
###  <a name="ErrorPageStrings"></a>ErrorPageStrings  
  
|Ad|Metin|  
|----------|----------|  
|LinkLabelBack|Geri|  
|LinkLabelHomePage|Giriş sayfası|  
|LinkLabelSendUsEmail|bize bir e-posta gönderin|  
|PageTitleError|Ne yazık ki oluştu sorun sunma hello istenen bir sayfa|  
|TextblockPotentialCauseIntermittentIssue|Bu zaten kayboluyor aralıklı veri erişim sorunu olabilir.|  
|TextblockPotentialCauseOldLink|üzerinde tıkladığınız hello bağlantı eski olabilir ve değil noktası toohello konumu artık düzeltin.|  
|TextblockPotentialCauseTechnicalProblem|Bizden teknik bir sorun olabilir.|  
|TextblockPotentialSolutionRefresh|Merhaba sayfayı yenilemeyi deneyin.|  
|TextblockPotentialSolutionStartOver|Baştan başlamak bizim {0}.|  
|TextblockPotentialSolutionTryAgain|{0} gidin ve yeniden gerçekleştirilen hello eylem deneyin.|  
|TextReportProblem|geçebiliriz hemen nelerin yanlış gittiğini açıklayan {0} ve biz bakmak.|  
|TitlePotentialCause|Olası neden|  
|TitlePotentialSolution|Muhtemelen yalnızca geçici bir sorun, birkaç şey tootry olduğu|  
  
###  <a name="IssuesStrings"></a>IssuesStrings  
  
|Ad|Metin|  
|----------|----------|  
|WebIssuesIndexTitle|Sorunlar|  
|WebIssuesNoActiveSubscriptions|Hiç etkin aboneliğiniz yok. Ürün tooreport bir sorun için toosubscribe gerekir.|  
|WebIssuesNotSignin|Açmadınız. Lütfen {0} tooreport bir sorun veya yorum gönderin.|  
|WebIssuesReportIssueButton|Rapor sorunu|  
|WebIssuesSignIn|oturum aç|  
|WebIssuesStatusReportedBy|Durum: {0} &#124; {1} tarafından bildirilen|  
  
###  <a name="NotFoundStrings"></a>NotFoundStrings  
  
|Ad|Metin|  
|----------|----------|  
|LinkLabelHomePage|Giriş sayfası|  
|LinkLabelSendUsEmail|bize bir e-posta gönderin|  
|PageTitleNotFound|Üzgünüz, aradığınız hello sayfayı bulamıyoruz|  
|TextblockPotentialCauseMisspelledUrl|İçinde yazdıysanız hello URL yanlış.|  
|TextblockPotentialCauseOldLink|üzerinde tıkladığınız hello bağlantı eski olabilir ve değil noktası toohello konumu artık düzeltin.|  
|TextblockPotentialSolutionRetype|Merhaba URL yeniden yazmayı deneyin.|  
|TextblockPotentialSolutionStartOver|Baştan başlamak bizim {0}.|  
|TextReportProblem|geçebiliriz hemen nelerin yanlış gittiğini açıklayan {0} ve biz bakmak.|  
|TitlePotentialCause|Olası neden|  
|TitlePotentialSolution|Olası çözüm|  
  
###  <a name="ProductDetailsStrings"></a>ProductDetailsStrings  
  
|Ad|Metin|  
|----------|----------|  
|WebProductsAgreement|Çok abone tarafından {0} ürün, toohello kabul `<a data-toggle='modal' href='#legal-terms'\>Terms of Use</a\>`.|  
|WebProductsLegalTermsLink|Kullanım Koşulları|  
|WebProductsSubscribeButton|Abone olun|  
|WebProductsUsageLimitsHeader|Kullanım sınırları|  
|WebProductsYouAreNotSubscribed|Abone olunan toothis ürün var.|  
|WebProductsYouRequestedSubscription|Abonelik toothis ürün istedi.|  
|ErrorYouNeedtoAgreeWithLegalTerms|Devam etmeden önce toohello Kullanım Koşulları'nı kabul etmeniz gerekir.|  
|ButtonLabelAddSubscription|Abonelik ekleme|  
|LinkLabelChangeSubscriptionName|değiştirme|  
|ButtonLabelConfirm|Onayla|  
|TextblockMultipleSubscriptionsCount|{0} abonelikleri toothis ürün vardır:|  
|TextblockSingleSubscriptionsCount|{0} abonelik toothis ürün vardır:|  
|TextblockSingleApisCount|Bu ürün {0} API içerir:|  
|TextblockMultipleApisCount|Bu ürün {0} API'leri içeriyor:|  
|TextblockHeaderSubscribe|Tooproduct abone olma|  
|TextblockSubscriptionDescription|Yeni bir abonelik şu şekilde oluşturulur:|  
|TextblockSubscriptionLimitReached|Abonelik sınırına ulaşıldı.|  
  
###  <a name="ProductsStrings"></a>ProductsStrings  
  
|Ad|Metin|  
|----------|----------|  
|PageTitleProducts|Ürünler|  
  
###  <a name="ProviderInfoStrings"></a>ProviderInfoStrings  
  
|Ad|Metin|  
|----------|----------|  
|TextboxExternalIdentitiesDisabled|Oturum açma hello yöneticiler tarafından hello şu anda devre dışı bırakılır.|  
|TextboxExternalIdentitiesSigninInvitation|Alternatif olarak, oturum açın|  
|TextboxExternalIdentitiesSigninInvitationPrimary|Oturum açın:|  
  
###  <a name="SigninResources"></a>SigninResources  
  
|Ad|Metin|  
|----------|----------|  
|PrincipalNotFound|Asıl bulunamadı veya imzası geçersiz|  
|ErrorSsoAuthenticationFailed|SSO kimlik doğrulaması başarısız oldu|  
|ErrorSsoAuthenticationFailedDetailed|Sağlanan geçersiz belirteç veya imza doğrulanamıyor.|  
|ErrorSsoTokenInvalid|SSO belirteci geçersiz|  
|ValidationErrorSpecificEmailAlreadyExists|E-posta '{0}' zaten kayıtlı|  
|ValidationErrorSpecificEmailInvalid|E-posta '{0}' geçerli değil|  
|ValidationErrorPasswordInvalid|Parola geçersiz. Lütfen hello hataları düzeltin ve yeniden deneyin.|  
|PropertyTooShort|{0} çok kısa|  
|WebAuthenticationAddresserEmailInvalidErrorMessage|Geçersiz e-posta adresi.|  
|ValidationMessageNewPasswordConfirmationRequired|Yeni parolayı onaylayın|  
|ValidationErrorPasswordConfirmationRequired|Parola boş olduğunu onaylayın|  
|WebAuthenticationEmailChangeNotice|Değişiklik onay e-postadır hello üzerinde çok {0}. Lütfen tooconfirm içindeki yönergeleri izleyin, yeni e-posta adresi. Merhaba e-posta sonraki birkaç dakika hello tooyour Kutusu'nda ulaşmaz, önemsiz e-posta klasörünüzü kontrol edin.|  
|WebAuthenticationEmailChangeNoticeHeader|E-posta değişiklik isteği başarıyla işlendi|  
|WebAuthenticationEmailChangeNoticeTitle|E-posta değişiklik istendi|  
|WebAuthenticationEmailHasBeenRevertedNotice|Size e-posta zaten mevcut. İstek geri döndürüldü|  
|ValidationErrorEmailAlreadyExists|E-posta zaten var|  
|ValidationErrorEmailInvalid|Geçersiz e-posta adresi|  
|TextboxLabelEmail|E-posta|  
|ValidationErrorEmailRequired|E-posta gereklidir.|  
|WebAuthenticationErrorNoticeHeader|Hata|  
|WebAuthenticationFieldLengthErrorMessage|{0} {1} en fazla şu uzunlukta olmalıdır|  
|TextboxLabelEmailFirstName|Ad|  
|ValidationErrorFirstNameRequired|Ad gereklidir.|  
|ValidationErrorFirstNameInvalid|Geçersiz ad|  
|NoticeInvalidInvitationToken|Lütfen onay bağlantıları yalnızca 48 saat için geçerli olduğunu unutmayın. Bu süre içinde hala varsa, lütfen bağlantınızı doğru olduğundan emin olun. Bağlantı süresi dolmuşsa, lütfen tooconfirm çalıştığınız hello eylemi yineleyin.|  
|NoticeHeaderInvalidInvitationToken|Geçersiz Davet belirteci|  
|NoticeTitleInvalidInvitationToken|Doğrulama hatası|  
|WebAuthenticationLastNameInvalidErrorMessage|Geçersiz son adı|  
|TextboxLabelEmailLastName|Soyadı|  
|ValidationErrorLastNameRequired|Son adı gereklidir.|  
|WebAuthenticationLinkExpiredNotice|Onay bağlantısı tooyou gönderilen süresi doldu. `<a href={0}?token={1}>Resend confirmation email.</a\>`|  
|NoticePasswordResetLinkInvalidOrExpired|Parola sıfırlama bağlantısı geçersiz veya süresi dolmuş.|  
|WebAuthenticationLinkExpiredNoticeTitle|Gönderilen bağlantı|  
|WebAuthenticationNewPasswordLabel|Yeni parola|  
|ValidationMessageNewPasswordRequired|Yeni parola zorunludur.|  
|TextboxLabelNotificationsSenderEmail|Bildirimleri gönderen e-posta|  
|TextboxLabelOrganizationName|Kuruluş adı|  
|WebAuthenticationOrganizationRequiredErrorMessage|Kuruluş adı yok|  
|WebAuthenticationPasswordChangedNotice|Parolanızı başarıyla güncelleştirildi|  
|WebAuthenticationPasswordChangedNoticeTitle|Parola güncelleştirildi|  
|WebAuthenticationPasswordCompareErrorMessage|Parolalar eşleşmiyor|  
|WebAuthenticationPasswordConfirmLabel|Parolayı onayla|  
|ValidationErrorPasswordInvalidDetailed|Parola çok zayıf değil.|  
|WebAuthenticationPasswordLabel|Parola|  
|ValidationErrorPasswordRequired|Parola gereklidir.|  
|WebAuthenticationPasswordResetSendNotice|Değişiklik parola onayı e-posta olduğu hello üzerinde çok {0}. Lütfen parola değişikliği işlemi hello e-posta toocontinue içinde hello yönergeleri izleyin.|  
|WebAuthenticationPasswordResetSendNoticeHeader|Parola sıfırlama isteği başarıyla işlendi|  
|WebAuthenticationPasswordResetSendNoticeTitle|Parola sıfırlama istendi.|  
|WebAuthenticationRequestNotFoundNotice|İsteği bulunamadı|  
|WebAuthenticationSenderEmailRequiredErrorMessage|Bildirimleri gönderen e-posta boştur|  
|WebAuthenticationSigninPasswordLabel|Lütfen bir parola girerek hello Değişikliğini Onayla|  
|WebAuthenticationSignupConfirmNotice|Kayıt onayı e-posta yolda olduğundan çok {0}. < br /\> Lütfen izleyin yönergeleri hello içinde tooactivate e-posta hesabınızı < br /\> hello e-posta gelen kutunuza hello içinde sonraki birkaç dakika ulaşmaz Lütfen kontrol edin Önemsiz e-posta klasörünüze.|  
|WebAuthenticationSignupConfirmNoticeHeader|Hesabınız başarıyla oluşturuldu|  
|WebAuthenticationSignupConfirmNoticeRepeatHeader|Kayıt onayı e-posta yeniden gönderildi|  
|WebAuthenticationSignupConfirmNoticeTitle|Hesabı oluşturuldu|  
|WebAuthenticationTokenRequiredErrorMessage|Belirteç boş|  
|WebAuthenticationUserAlreadyRegisteredNotice|Bir kullanıcı bu e-posta ile Merhaba sistemde zaten kayıtlı görünüyor. Parolanızı unuttuysanız, lütfen toorestore bu kişi deneyin veya destek ekibimiz.|  
|WebAuthenticationUserAlreadyRegisteredNoticeHeader|Kullanıcı zaten kayıtlı|  
|WebAuthenticationUserAlreadyRegisteredNoticeTitle|Zaten kayıtlı|  
|ButtonLabelChangePassword|Parolayı Değiştir|  
|ButtonLabelChangeAccountInfo|Hesap bilgilerini değiştirme|  
|ButtonLabelCloseAccount|Hesabı Kapat|  
|WebAuthenticationInvalidCaptchaErrorMessage|Girilen metin hello resim metni eşleşmiyor. Lütfen yeniden deneyin.|  
|ValidationErrorCredentialsInvalid|E-posta veya parola geçersiz. Lütfen hello hataları düzeltin ve yeniden deneyin.|  
|WebAuthenticationRequestIsNotValid|İsteği geçerli değil|  
|WebAuthenticationUserIsNotConfirm|İçinde toosign denemeden önce lütfen Kaydınızı onaylayın.|  
|WebAuthenticationInvalidEmailFormated|E-posta geçersiz: {0}|  
|WebAuthenticationUserNotFound|Kullanıcı bulunamadı|  
|WebAuthenticationTenantNotRegistered|Hesabınızı bu portalı yetkili tooaccess olmayan tooa Azure Active Directory Kiracı aittir.|  
|WebAuthenticationAuthenticationFailed|Kimlik doğrulaması başarısız oldu.|  
|WebAuthenticationGooglePlusNotEnabled|Kimlik doğrulaması başarısız oldu. Emin Merhaba uygulaması yetkili sonra hello yönetici toomake temasa kullanırsanız, Google kimlik doğrulamasının doğru şekilde yapılandırılır.|  
|ValidationErrorAllowedTenantIsRequired|İzin verilen Kiracı gereklidir|  
|ValidationErrorTenantIsNotValid|Hello Azure Active Directory Kiracı '{0}' geçerli değil.|  
|WebAuthenticationActiveDirectoryTitle|Azure Active Directory|  
|WebAuthenticationLoginUsingYourProvider|{0} hesabınızı kullanarak oturum açın|  
|WebAuthenticationUserLimitNotice|Bu hizmet hello en fazla izin verilen kullanıcı sayısı sınırına ulaştı. Lütfen `<a href="mailto:{0}"\>contact hello administrator</a\>` tooupgrade kendi hizmet ve yeniden etkinleştirmeniz kullanıcı kaydı.|  
|WebAuthenticationUserLimitNoticeHeader|Kullanıcı kaydı devre dışı|  
|WebAuthenticationUserLimitNoticeTitle|Kullanıcı kaydı devre dışı|  
|WebAuthenticationUserRegistrationDisabledNotice|Kullanıcı kayıt hello Yöneticisi tarafından devre dışı bırakıldı. Lütfen dış kimlik sağlayıcısı ile oturum açın.|  
|WebAuthenticationUserRegistrationDisabledNoticeHeader|Kullanıcı kaydı devre dışı|  
|WebAuthenticationUserRegistrationDisabledNoticeTitle|Kullanıcı kaydı devre dışı|  
|WebAuthenticationSignupPendingConfirmationNotice|Hesabınızı hello oluşturulmasını uygulayabilmeniz için önce e-posta adresinizi tooverify ihtiyacımız var. Bir e-posta çok gönderdik {0}. Lütfen hesabınızı hello e-posta tooactivate içinde hello yönergeleri izleyin. Merhaba e-posta içinde hello sonraki birkaç dakika değil ulaşırsa, önemsiz e-posta klasörünüzü kontrol edin.|  
|WebAuthenticationSignupPendingConfirmationAccountFoundNotice|Merhaba e-posta adresi {0} onaylanmayan bir hesap bulduk. e-posta adresinizi tooverify ihtiyacımız hesabınızı toocomplete hello oluşturma. Bir e-posta çok gönderdik {0}. Lütfen hesabınızı hello e-posta tooactivate içinde hello yönergeleri izleyin. Lütfen Hello e-posta içinde hello sonraki birkaç dakika değil ulaşırsa, önemsiz e-posta klasörünüzü kontrol edin|  
|WebAuthenticationSignupConfirmationAlmostDone|Neredeyse bitti|  
|WebAuthenticationSignupConfirmationEmailSent|Bir e-posta çok gönderdik {0}. Lütfen hesabınızı hello e-posta tooactivate içinde hello yönergeleri izleyin. Merhaba e-posta içinde hello sonraki birkaç dakika değil ulaşırsa, önemsiz e-posta klasörünüzü kontrol edin.|  
|WebAuthenticationEmailSentNotificationMessage|Başarıyla çok gönderilen e-posta {0}|  
|WebAuthenticationNoAadTenantConfigured|Azure Active Directory Kiracı Hello hizmeti için yapılandırılmış.|  
|CheckboxLabelUserRegistrationTermsConsentRequired|Toohello kabul `<a data-toggle="modal" href="#" data-target="#terms"\>Terms of Use</a\>`.|  
|TextblockUserRegistrationTermsProvided|Lütfen gözden geçirin.`<a data-toggle="modal" href="#" data-target="#terms"\>Terms of Use.</a\>`|  
|DialogHeadingTermsOfUse|Kullanım Koşulları|  
|ValidationMessageConsentNotAccepted|Devam etmeden önce toohello Kullanım Koşulları'nı kabul etmeniz gerekir.|  
  
###  <a name="SigninStrings"></a>SigninStrings  
  
|Ad|Metin|  
|----------|----------|  
|WebAuthenticationForgotPassword|Parolanızı mı unuttunuz?|  
|WebAuthenticationIfAdministrator|Bir yöneticiyseniz, oturum açmanız gerekir `<a href="{0}"\>here</a\>`.|  
|WebAuthenticationNotAMember|Üyede kullanılamaz henüz? `<a href="/signup"\>Sign up now</a\>`|  
|WebAuthenticationRemember|Bu bilgisayarda Beni anımsa|  
|WebAuthenticationSigininWithPassword|Kullanıcı adı ve parola ile oturum|  
|WebAuthenticationSigninTitle|Oturum aç|  
|WebAuthenticationSignUpNow|Hemen kaydolun|  
  
###  <a name="SignupStrings"></a>SignupStrings  
  
|Ad|Metin|  
|----------|----------|  
|PageTitleSignup|Kaydolma|  
|WebAuthenticationAlreadyAMember|Zaten üye misiniz?|  
|WebAuthenticationCreateNewAccount|Yeni bir API Management hesabı oluşturma|  
|WebAuthenticationSigninNow|Şimdi oturum açın|  
|ButtonLabelSignup|Kaydolma|  
  
###  <a name="SubscriptionListStrings"></a>SubscriptionListStrings  
  
|Ad|Metin|  
|----------|----------|  
|SubscriptionCancelConfirmation|Bu abonelik toocancel istediğinizden emin misiniz?|  
|SubscriptionRenewConfirmation|Bu abonelik toorenew istediğinizden emin misiniz?|  
|WebDevelopersManageSubscriptions|Abonelikleri yönetme|  
|WebDevelopersPrimaryKey|Birincil anahtar|  
|WebDevelopersRegenerateLink|Yeniden Oluştur|  
|WebDevelopersSecondaryKey|İkincil anahtar|  
|ButtonLabelShowKey|Göster|  
|ButtonLabelRenewSubscription|Yenile|  
|WebDevelopersSubscriptionReqested|{0} istendi|  
|WebDevelopersSubscriptionRequestedState|İstenen|  
|WebDevelopersSubscriptionTableNameHeader|Ad|  
|WebDevelopersSubscriptionTableStateHeader|Durum|  
|WebDevelopersUsageStatisticsLink|Analytics Raporları|  
|WebDevelopersYourSubscriptions|Aboneliklerinizi|  
|SubscriptionPropertyLabelRequestedDate|Üzerinde istenen|  
|SubscriptionPropertyLabelStartedDate|Üzerinde başlatıldı|  
|PageTitleRenameSubscription|Aboneliği yeniden adlandırılamadı|  
|SubscriptionPropertyLabelName|Abonelik adı|  
  
###  <a name="SubscriptionStrings"></a>SubscriptionStrings  
  
|Ad|Metin|  
|----------|----------|  
|SectionHeadingCloseAccount|Hesabınızı tooclose arayan?|  
|PageTitleDeveloperProfile|Profil|  
|ButtonLabelHideKey|Gizle|  
|ButtonLabelRegenerateKey|Yeniden Oluştur|  
|InformationMessageKeyWasRegenerated|Bu anahtar tooregenerate istediğinizden emin misiniz?|  
|ButtonLabelShowKey|Göster|  
  
###  <a name="UpdateProfileStrings"></a>UpdateProfileStrings  
  
|Ad|Metin|  
|----------|----------|  
|ButtonLabelUpdateProfile|Profil güncelleştirme|  
|PageTitleUpdateProfile|Hesap bilgilerini güncelleştir|  
  
###  <a name="UserProfile"></a>Kullanıcı profili  
  
|Ad|Metin|  
|----------|----------|  
|ButtonLabelChangeAccountInfo|Hesap bilgilerini değiştirme|  
|ButtonLabelChangePassword|Parolayı Değiştir|  
|ButtonLabelCloseAccount|Hesabı Kapat|  
|TextboxLabelEmail|E-posta|  
|TextboxLabelEmailFirstName|Ad|  
|TextboxLabelEmailLastName|Soyadı|  
|TextboxLabelNotificationsSenderEmail|Bildirimleri gönderen e-posta|  
|TextboxLabelOrganizationName|Kuruluş adı|  
|SubscriptionStateActive|Etkin|  
|SubscriptionStateCancelled|İptal edildi|  
|SubscriptionStateExpired|Süresi dolmuş|  
|SubscriptionStateRejected|Reddetti|  
|SubscriptionStateRequested|İstenen|  
|SubscriptionStateSuspended|askıya alındı|  
|DefaultSubscriptionNameTemplate|{0} (varsayılan)|  
|SubscriptionNameTemplate|Geliştirici erişim #{0}|  
|TextboxLabelSubscriptionName|Abonelik adı|  
|ValidationMessageSubscriptionNameRequired|Abonelik adı boş olamaz.|  
|ApiManagementUserLimitReached|Bu hizmet hello en fazla izin verilen kullanıcı sayısı sınırına ulaştı. Lütfen daha yüksek fiyatlandırma katmanı tooa yükseltin.|  
  
##  <a name="glyphs"></a>Karakter kaynakları  
 API Management Geliştirici Portalı şablonları hello karakterlerin gelen kullanabileceğiniz [Glyphicons önyükleme gelen](http://getbootstrap.com/components/#glyphicons). Bu karakterlerin 250'den fazla karakterlerin yazı tipi biçiminde hello gelen içerir [Glyphicon](http://glyphicons.com/) Halflings ayarlayın. toouse bu karaktere ayarlamak, söz dizimi aşağıdaki hello kullanın.  
  
```html  
<span class="glyphicon glyphicon-user">  
```  
  
 Merhaba tam listesi karakterlerin için bkz: [Glyphicons önyükleme gelen](http://getbootstrap.com/components/#glyphicons).

## <a name="next-steps"></a>Sonraki adımlar
Şablonları ile çalışma hakkında daha fazla bilgi için bkz: [nasıl toocustomize hello şablonları kullanarak API Management Geliştirici Portalı](api-management-developer-portal-templates.md).
