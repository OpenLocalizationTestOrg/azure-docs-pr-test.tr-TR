---
title: "Azure Active Directory B2C: dil özelleştirme kullanarak | Microsoft Docs"
description: 
services: active-directory-b2c
documentationcenter: 
author: sama
ms.assetid: eec4d418-453f-4755-8b30-5ed997841b56
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/25/2017
ms.author: sama
ms.openlocfilehash: a8e4037014f5adf929dac7b5dc4db72ba0f5b292
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-using-language-customization"></a>Azure Active Directory B2C: Kullanarak dil özelleştirme

>[!NOTE] 
>Bu özellik genel önizlemede değil.  Bu özelliği kullanırken bir test Kiracı kullanmanız önerilir.  Biz hello Önizleme toohello genel kullanılabilirlik sürümünden en son değişiklikleri üzerinde planı yoktur, ancak Biz bu tür değişiklikleri tooimprove hello özelliği hello sağ toomake yedek.  Lütfen bir fırsat tootry özelliği karşılaşmışsınız sonra deneyimlerinizi geribildirim ve nasıl biz bunu daha iyi duruma getirebilirsiniz belirtin.  Aracıyla hello gülen yüz sağ hello üstte hello Azure portal aracılığıyla geribildirim sağlayabilir.   Merhaba Önizleme aşamasında bu özelliği kullanarak canlı, toogo için bir iş gerekliliği varsa, bize senaryolarınızı bildirin ve size hello uygun Kılavuzu ve Yardım sağlayabilir.  Adresinden bize başvurun [ aadb2cpreview@microsoft.com ](mailto:aadb2cpreview@microsoft.com).

Dil özelleştirme kullanıcı gezisine müşteri gereken tooa farklı dil toosuit toochange sağlar.  36 diller için çeviriler sağladığımız (bkz [ek bilgi](#additional-information)).  Deneyiminizi yalnızca tek bir dil için sağlanan olsa bile, gereksinimlerinizi hello sayfaları toosuit herhangi bir metin özelleştirebilirsiniz.  

## <a name="how-does-language-customization-work"></a>Dil özelleştirme nasıl çalışır?
Dil özelleştirme kullanıcı Yolculuğunuzun hangi dillerde kullanılabilir: tooselect sağlar.  Merhaba özelliği etkinleştirildiğinde, hello sorgu dizesi parametresi, ui_locales, uygulamanızı sağlar.  Azure AD B2C çağırdığınızda, biz belirttiniz sayfa toohello bölgeniz çevir.  Yapılandırma türünü kullanan kullanıcı Yolculuğunuzun hello dilleri üzerinde tam denetim verir ve hello Müşteri'nin tarayıcısının hello dil ayarlarını yoksayar. Alternatif olarak, müşteriniz bkz hangi dilde üzerinde denetim düzeyini gerekmeyebilir.  Ui_locales parametresi sağlamazsanız, hello Müşteri'nin deneyimi, tarayıcının ayarları tarafından dikte edilir.  Hangi hala denetleyebilirsiniz kullanıcı Yolculuğunuzun olan dilleri desteklenen bir dil ekleme tooby çevrilir.  Müşteri'nin tarayıcı kümesi tooshow ise bir dil toosupport sonra varsayılan olarak desteklenen kültürler yerine gösterildiği gibi seçtiğiniz hello dil istemezsiniz.

1. **kullanıcı arabirimi yerel ayarlar belirtilen dil** -dil özelleştirme etkinleştirdiğinizde, kullanıcı Yolculuğunuzun burada belirtilen çevrilmiş toohello dildir
2. **Tarayıcı istenen dil** -kullanıcı arabirimi yerel belirtildi, toohello çevirir tarayıcı istenen dil **desteklenen dilleri eklediyseniz**
3. **İlke varsayılan dil** -hello tarayıcı olmayan bir dil belirtin veya desteklenmeyen bir belirtir, toohello ilkesi varsayılan dili çevirir

>[!NOTE]
>Özel kullanıcı özniteliklerini kullanıyorsanız, kendi çevirileri tooprovide gerekir. Bkz. '[dizelerinizi özelleştirme](#customize-your-strings)' Ayrıntılar için.
>

## <a name="support-uilocales-requested-languages"></a>Dil desteği ui_locales istendi 
Bir ilkedeki ' dil özelleştirme' etkinleştirerek hello ui_locales parametresini ekleyerek hello kullanıcı gezisine hello dilinin şimdi kontrol edebilirsiniz.
1. [Bu adımları toonavigate toohello B2C özellikleri dikey hello Azure portalı üzerinde izleyin.](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-app-registration#navigate-to-b2c-settings)
2. Tooenable çevirileri için istediğiniz tooa ilkeye gidin.
3. Tıklatın **dil özelleştirme**.
4. Dikkatle uyarı hello okuyun.  Etkinleştirildiğinde, 'Devre dışı dil özelleştirme' kapatamazsınız.
5. Merhaba özelliğini açın ve'ı tıklatın **Tamam**.
6. Merhaba sol üst köşesindeki ilkeniz kaydetmek, **Düzenle İlkesi** dikey.

## <a name="select-which-languages-your-user-journey-supports"></a>Kullanıcı Yolculuğunuzun destekleyen hangi dilleri seçin 
İçinde hello ui_locales parametresi sağlanmadığında çevrilmiş, kullanıcı gezisine toobe için izin verilen dillerin bir listesi oluşturun.
1. 'Önceki yönergeleri etkin dil özelleştirme' ilkeniz olduğundan emin olun.
2. Öğesinden, **Düzenle İlkesi** dikey penceresinde, select **dil özelleştirme**.
3. Tooyour alınır **desteklenen diller** dikey.  Buradan, seçtiğiniz **dil eklemek**.
4. Desteklenen toobe istediğiniz tüm hello dilleri seçin.  

>[!NOTE]
>Ui_locales parametresi sağlanmazsa, yalnızca bu listede ise hello sayfa çevrilmiş toohello Müşteri'nin tarayıcının dili ise
>

5. Tıklatın **Tamam** hello altındaki
6. Kapat hello **dil özelleştirme** dikey ve **kaydetmek** ilkeniz.

## <a name="customize-your-strings"></a>Dizelerinizi özelleştirme
'Dil özelleştirme' herhangi bir kullanıcı Yolculuğunuzun dize toocustomize sağlar.
1. 'Hello önceki yönergeleri etkin dil özelleştirme' ilkeniz olduğundan emin olun.
2. Öğesinden, **Düzenle İlkesi** dikey penceresinde, select **dil özelleştirme**.
3. Merhaba sol taraftaki gezinti menüsünde seçin **içeriği indirirken**.
4. Tooedit istediğiniz başlangıç sayfasını seçin.
5. Merhaba açılır listede tooedit için istediğiniz hello dili seçin.
6. **İndir**’e tıklayın. 

Bu adımları dizelerinizi düzenleme toostart kullanabileceğiniz bir JSON dosyası verin.

### <a name="changing-any-string-on-hello-page"></a>Merhaba sayfasında herhangi bir dize değiştirme
1. Açık hello JSON dosyası önceki yönergeleri bir JSON Düzenleyicisi'ni indirilen.
2. Toochange istediğiniz Bul hello öğesi.  Merhaba bulabilirsiniz `StringId` aradığınız veya Merhaba bakın hello dizesinin `Value` toochange istiyor.
3. Güncelleştirme hello `Value` görüntülenmesini istediğiniz ile özniteliği.
4. Merhaba dosyasını kaydedin ve değişikliklerinizi karşıya yükleyin.

### <a name="changing-extension-attributes"></a>Uzantı özniteliklerini değiştirme
Toochange hello dize için bir özel kullanıcı özniteliği aradığınız veya tooadd bir toohello JSON istiyorsanız biçimini izleyen hello şöyledir:
```JSON
{
  "LocalizedStrings": [
    {
      "ElementType": "ClaimType",
      "ElementId": "extension_<ExtensionAttribute>",
      "StringId": "DisplayName",
      "Override": false,
      "Value": "<ExtensionAttributeValue>"
    }
    [...]
}
```
>[!IMPORTANT]
>Toooverride bir dize gerekiyorsa, emin tooset hello olun `Override` çok değer`true`.  Merhaba değeri değiştirilmez, hello girişi göz ardı edilir. 
>

Değiştir `<ExtensionAttribute>` , özel kullanıcı özniteliği hello adı.  
Değiştir `<ExtensionAttributeValue>` görüntülenen hello yeni dize toobe ile.

### <a name="using-localizedcollections"></a>LocalizedCollections kullanma
Yanıtlar için tooprovide değer kümesi listesi istiyorsanız, toocreate gerekir bir `LocalizedCollections`.  A `LocalizedCollections` dizisidir `Name` ve `Value` çiftleri.  Merhaba `Name` ne görüntülenir ve hello `Value` hello talep döndürülen değil.  tooadd bir `LocalizedCollections`, biçimini izleyen hello vardır:

```JSON
{
  "LocalizedStrings": [...],
  "LocalizedCollections": [{
      "ElementType":"ClaimType", 
      "ElementId":"<UserAttribute>",
      "TargetCollection":"Restriction",
      "Override": false,
      "Items":[
           {
                "Name":"<Response1>",
                "Value":"<Value1>"
           },
           {
                "Name":"<Response2>",
                "Value":"<Value2>"
           }
     ]
  }]
}
```
>[!IMPORTANT]
>Toooverride bir dize gerekiyorsa, emin tooset hello olun `Override` çok değer`true`.  Merhaba değeri değiştirilmez, hello girişi göz ardı edilir. 
>

* `ElementId`olan hello kullanıcı özniteliği bu `LocalizedCollections` yanıt olarak
* `Name`Merhaba değer gösterilen toohello kullanıcı
* `Value`Bu seçenek belirlendiğinde, hello talep döndürülür olduğu

### <a name="upload-your-changes"></a>Değişikliklerinizi karşıya yüklemek
1. Merhaba değişiklikleri tooyour JSON dosyası tamamladıktan sonra geri tooyour B2C Kiracı gidin.
2. Öğesinden, **Düzenle İlkesi** dikey penceresinde, select **dil özelleştirme**.
3. Merhaba sol taraftaki gezinti menüsünde seçin **içerik Yükle**.
4. Değişikliklerinizi için tooupload istediğiniz başlangıç sayfasını seçin.
5. JSON için önceden sağladığınız bir dil tooupload istiyorsanız toodelete hello önceki girişi gerekir.  Merhaba tıklayarak silebilirsiniz `...` hello o dil sağına ve seçin **silmek**.
6. Tıklatın **Ekle** hello üst sol taraftaki.
7. JSON dosyanız Hello dilini seçin.
8. Merhaba klasör düğmesine hello sağ tıklayın ve JSON dosyanız için göz atın.
9. Merhaba tıklatın **karşıya** hello dikey penceresinde hello alt düğmesinde.
10. Tooyour dönün **Düzenle İlkesi** tıklayın ve dikey **kaydetmek**.

## <a name="additional-information"></a>Ek bilgiler
### <a name="recommendations-for-language-customization"></a>'Dil özelleştirme' için öneriler
Yalnızca dizeleri için girişleri tooyour Türkçe kaynaklar içinde açıkça istediğiniz tooreplace koyma öneririz.  Biz dışında tüm JSON çevirileri derlenmiş bir boyut sınırı toohello dosya uygulayın.  Dosyalarınızı çok büyük alırsanız, kullanıcı Yolculuğunuzun hello performansını etkiler.
### <a name="page-ui-customization-labels-are-removed-once-language-customization-is-enabled"></a>'Dil özelleştirme' etkinleştirildikten sonra sayfası kullanıcı Arabirimi özelleştirme etiketleri kaldırılır
'Dil özelleştirme' etkinleştirdiğinizde, önceki düzenlemeleriniz sayfa UI Özelleştirme kullanarak etiketleri için özel kullanıcı özniteliklerini dışında kaldırılır.  Bu değişiklik, dizelerinizi düzenleyebileceğiniz içinde tooavoid çakışmaları yapılır.  Toochange etiketleri ve diğer dizeleri 'Dil özelleştirme' dil kaynaklarının yükleyerek devam edebilirsiniz.
### <a name="microsoft-is-committed-tooprovide-hello-most-up-to-date-translations-for-your-use"></a>Microsoft, kullanımınız için kaydedilmiş tooprovide hello en güncel Çeviriler
Biz sürekli çevirileri geliştirmek ve bunları sizin için Uyumluluk tutun.  Biz hatalar ve genel terminolojisi değişiklikleri tanımlamak ve çalışacak hello güncelleştirmeleri sorunsuz kullanıcı Yolculuğunuzun yapın.
### <a name="support-for-right-to-left-languages"></a>Sağdan sola yazılan diller için destek
Bu özellik Lütfen oy bu özelliği için gerekiyorsa sağdan sola yazılan diller için destek yok olduğundan [Azure geri bildirim](https://feedback.azure.com/forums/169401-azure-active-directory/suggestions/19393000-provide-language-support-for-right-to-left-languag).
### <a name="social-identity-provider-translations"></a>Sosyal kimlik sağlayıcısı çevirileri
Merhaba ui_locales OIDC parametresi toosocial oturumları sağladığımız ancak Facebook ve Google dahil olmak üzere bazı sosyal kimlik sağlayıcıları tarafından onaylanmaz. 
### <a name="browser-behavior"></a>Tarayıcı davranışı
Chrome ve Firefox her ikisini de kümesi dillerini iste ve desteklenen bir dil ise, önce hello varsayılan görüntülenir.  Edge şu anda bir dil istemez ve düz toohello varsayılan dili geçer.
### <a name="known-issues"></a>Bilinen sorunlar
* Bir profili düzenlemek İlkesi'nde hello MFA sayfa için Türkçe kaynaklar karşıya yükleme şu anda kullanılamıyor.
* `LocalizedCollections`Merhaba yanıt türü tarafından istendiğinde değerlerini oluşturulan değil
### <a name="what-if-i-want-a-language-that-isnt-supported"></a>Desteklenmeyen bir dil ne istiyorum?
Tooprovide tooupload 'özel diller' doğrultusunda JSON kaynak sağlayan bu özellik, bir uzantı planladığınız.  Merhaba özelliği toospecify hello adı sağlar ve dil kodu herhangi bir dil için ve sağlamak *tüm* hello çevirileri o dil için.  Bu özellik gerekiyorsa, senaryonuza en bize gönderin [ aadb2cpreview@microsoft.com ](mailto:aadb2cpreview@microsoft.com).  

### <a name="what-languages-are-supported"></a>Hangi dilleri destekleniyor mu?

| Dil              | Dil kodu |
|-----------------------|---------------|
| Bangla                | Bn            |
| Çekçe                 | cs            |
| Danca                | da            |
| Almanca                | de            |
| Yunanca                 | el            |
| Türkçe               | en            |
| İspanyolca               | es            |
| Fince               | fi            |
| Fransızca                | fr            |
| Gucerat dili              | gu            |
| Hintçe                 | yüksek            |
| Hırvatça              | İK            |
| Macarca             | hu            |
| İtalyanca               | it            |
| Japonca              | ja            |
| Kannada dili               | KN            |
| Kore dili                | ko            |
| Malayalam dili             | ML            |
| Marathi               | MR            |
| Malay dili                 | MS            |
| Norveççe Bokmal      | nb            |
| Hollanda dili                 | nl            |
| Pencap dili               | Pa            |
| Lehçe                | pl            |
| Portekizce - Brezilya   | pt-br         |
| Portekizce - Portekiz | pt-pt         |
| Rumence              | ro            |
| Rusça               | ru            |
| Slovakça                | SK            |
| İsveç dili               | sv            |
| Tamil dili                 | eri            |
| Telugu dili                | metin            |
| Tay dili                  | TH            |
| Türkçe               | tr            |
| Çince - Basitleştirilmiş  | zh-atanır       |
| Geleneksel Çince- | zh-hant       |
