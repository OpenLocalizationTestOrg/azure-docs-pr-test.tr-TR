---
title: "Azure Active Directory B2C: Başvuru: hello kullanıcı gezisine UI özel ilkeleriyle özelleştirme | Microsoft Docs"
description: "Bir konu Azure Active Directory B2C özel ilkeler hakkında"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/25/2017
ms.author: joroja
ms.openlocfilehash: 11f2a7575b95a186399d83266850fe44d650371b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-hello-ui-of-a-user-journey-with-custom-policies"></a>Merhaba kullanıcı gezisine UI özel ilkeleriyle özelleştirme

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

> [!NOTE]
> Bu makalede, bir Gelişmiş açıklama UI özelleştirme nasıl çalıştığını ve nasıl tooenable kullanarak B2C özel ilkeleriyle hello kimlik deneyimi Framework yer alır.


Kesintisiz kullanıcı deneyimi iş tüketici çözüme yönelik bir anahtardır. Kesintisiz kullanıcı deneyimi, cihaz veya tarayıcı, burada bir kullanıcının gezisine bizim hizmeti aracılığıyla, kullandıkları hello Müşteri Hizmetleri ayırt edilebilir olamaz bir deneyim anlama.

## <a name="understand-hello-cors-way-for-ui-customization"></a>UI Özelleştirme Hello CORS yol anlama

Azure AD B2C, potansiyel olarak sunulan ve özel ilkelerinizi Azure AD B2C tarafından görüntülenen çeşitli sayfalar hello üzerinde toocustomize hello Görünüm-ve-yapısını (UX) kullanıcı deneyimi sağlar.

Bu amaç için Azure AD B2C kodu, tüketicinin tarayıcıda çalışır ve kullandığı hello modern ve standart bir yaklaşım [çıkış noktaları arası kaynak paylaşımı (CORS)](http://www.w3.org/TR/cors/) özel bir ilke belirttiğiniz belirli bir URL tooload özel içeriği toopoint tooyour HTML5/CSS şablonları. CORS yazı tiplerini, hello kaynak kaynaklandığı hello etki alanı dışındaki başka bir etki alanından istenen web sayfasının toobe gibi sınırlı kaynakları sağlayan bir mekanizmadır.

Burada şablon sayfalarını burada sınırlı metin sağlanan ve burada düzeni ve hissi sınırlı denetim başında toomore sorunlar tooachieve sorunsuz bir deneyim daha sunulmuştur, görüntüler, CORS hello hello çözümü tarafından sahip olunan toohello eski geleneksel şekilde karşılaştırma yol HTML5 ve CSS destekler ve olanak sağlar:

- Merhaba içeriğini barındırmak ve hello çözüm yerleştirir istemci tarafı komut dosyası kullanarak kendi denetimleri.
- Her piksel düzeni ve hissi üzerinde tam denetime sahiptir.

HTML5/CSS dosyaları uygun şekilde hazırlayın tarafından istediğiniz kadar çok içerik sayfaları sağlayabilir.

> [!NOTE]
> Güvenlik nedenleriyle, JavaScript hello kullanımını özelleştirme için şu anda engelleniyor. toounblock JavaScript, kullanım, Azure AD B2C kiracınızın özel etki alanı adı gereklidir.

Her HTML5/CSS şablonlarınızı sağladığınız bir *bağlantı* gerekli toohello karşılık gelen öğe `<div id=”api”>` olarak bundan böyle göstermeye hello HTML veya hello içerik sayfasındaki öğe. Azure AD B2C tüm içerik sayfalarının bu belirli DIV sahip olmasını gerektirir

```
<!DOCTYPE html>
<html>
  <head>
    <title>Your page content’s tile!</title>
  </head>
  <body>
    <div id="api"></div>
  </body>
</html>
```

Azure AD B2C ile ilgili içerik hello sayfa hello rest hello sayfasının sırasında bu div içine eklenen için sizindir toocontrol. Hello Azure AD B2C'in JavaScript kodu, içeriği çeker ve bu belirli div öğesinin bizim HTML yerleştirir. Azure AD B2C yerleştirir denetimleri uygun olarak aşağıdaki hello: hesap Seçici denetim, oturum açma denetimleri, çok faktörlü (şu anda telefon tabanlı) denetimleri ve öznitelik koleksiyonu denetimleri. Azure AD B2C tüm hello denetimleri HTML5 uyumlu ve erişilebilir olduğundan, tüm hello denetimleri tam olarak biçimlendirilebilir ve denetimi sürüm değil ilerletmek sağlar.

Merhaba birleştirilen içeriğin sonunda hello dinamik belge tooyour tüketici olarak görüntülenir.

Yukarıdaki hello tooensure beklendiği gibi çalıştığından, şunları yapmalısınız:

- İçeriğinizi HTML5 uyumlu ve erişilebilir olduğundan emin olun
- İçeriğinize CORS için etkinleştirildiğinden emin olun.
- HTTPS üzerinden içerik sunmak.
- Mutlak URL'ler https://yourdomain/content gibi tüm bağlantılar ve CSS içerik için kullanın.

> [!TIP]
> sitesi üzerinde içeriğinizi barındırma hello tooverify CORS'yi sahiptir ve CORS isteklerini test, hello site http://test-cors.org/ kullanabilirsiniz. Teşekkür ederiz toothis site, yalnızca hello CORS tooa uzak sunucu isteği (CORS destekleniyorsa tootest) göndermek veya hello CORS tooa test sunucu isteği gönder (tooexplore CORS belirli özelliklerini).

> [!TIP]
> Merhaba site http://enable-cors.org/ de CORS yararlı kaynaklara fazla meydana gelir.

Thanks toothis CORS dayalı yaklaşım, hello son kullanıcılar daha sonra uygulama ve Azure AD B2C tarafından sunulan hello sayfaları arasında tutarlı deneyimleri sahip olur.

## <a name="create-a-storage-account"></a>Depolama hesabı oluşturma

Bir önkoşul olarak toocreate bir depolama hesabı gerekir. Bir Azure aboneliği toocreate bir Azure Blob Storage hesabı gerekir. Merhaba, ücretsiz deneme yukarı imzalayabilirsiniz [Azure Web sitesi](https://azure.microsoft.com/en-us/pricing/free-trial/).

1. Bir tarayıcı oturumu açın ve toohello gidin [Azure portal](https://portal.azure.com).
2. Yönetici kimlik bilgilerinizle oturum.
3. Tıklatın **yeni** > **veri + depolama** > **depolama hesabı**.  A **depolama hesabı oluşturma** dikey penceresi açılır.
4. İçinde **adı**, örneğin, hello depolama hesabı için bir ad sağlayın *contoso369b2c*. Bu değer daha sonra çok olarak anılacaktır*storageAccountName*.
5. Fiyatlandırma katmanı, hello kaynak grubu ve hello abonelik hello için uygun seçimleri Hello seçin. Merhaba sahip olduğunuzdan emin olun **PIN tooStartboard** iade seçeneği. **Oluştur**'a tıklayın.
6. Toohello Sabitle geri dönün ve yeni oluşturduğunuz hello depolama hesabı'nı tıklatın.
7. Merhaba, **Hizmetleri** 'yi tıklatın **BLOB'lar**. A **Blob hizmeti dikey** açılır.
8. Tıklatın **+ kapsayıcı**.
9. İçinde **adı**, örneğin, hello kapsayıcı için bir ad sağlayın *b2c*. Bu değer daha sonra başvurulan tooas olacaktır *containerName*.
9. Seçin **Blob** hello olarak **erişim türüne**. **Oluştur**'a tıklayın.
10. oluşturduğunuz hello kapsayıcı hello hello listesinde görünür **Blob hizmeti dikey**.
11. Kapat hello **BLOB'lar** dikey.
12. Merhaba üzerinde **depolama hesabı dikey**, hello tıklatın **anahtar** simgesi. Bir **erişim anahtarları dikey** açılır.  
13. Hello değerini yazmak **key1**. Bu değer daha sonra olarak anılacaktır *key1*.

## <a name="downloading-hello-helper-tool"></a>Merhaba Yardımcısı aracı yükleniyor

1.  Merhaba Yardımcısı aracından karşıdan [GitHub](https://github.com/azureadquickstarts/b2c-azureblobstorage-client/archive/master.zip).
2.  Merhaba Kaydet *B2C-AzureBlobStorage-istemci-master.zip* yerel makinenizde dosya.
3.  Yerel diskinizde, örneğin hello altında hello B2C-AzureBlobStorage-istemci-master.zip dosyasının Hello içeriği Ayıkla **UI Özelleştirme paketi** klasör. Bu oluşturacak bir *AzureBlobStorage istemci yönetici B2C* klasörü altında.
4.  Bu klasörü açın ve hello arşiv dosyasını Merhaba içeriğine ayıklamak *B2CAzureStorageClient.zip* içindeki.

## <a name="upload-hello-ui-customization-pack-sample-files"></a>Merhaba UI Özelleştirme paketi örnek dosyaları karşıya yükleme

1.  Windows Gezgini'ni kullanarak toohello klasörüne gidin *AzureBlobStorage istemci yönetici B2C* hello altında bulunan *UI Özelleştirme paketi* hello önceki bölümde oluşturduğunuz klasör.
2.  Merhaba çalıştırmak *B2CAzureStorageClient.exe* dosya. Bu program yalnızca tooyour depolama hesabı belirtin ve bu dosyaları için CORS erişimini etkinleştirmek hello dizindeki tüm hello dosyaları karşıya yükler.
3.  İstendiğinde, belirtin: bir.  Depolama hesabınızın adını Hello *storageAccountName*, örneğin *contoso369b2c*.
    b.  azure blob depolama alanınızın Hello birincil erişim anahtarını *key1*, örneğin *contoso369b2c*.
    c.  Depolama blob depolama kapsayıcısını Hello adını *containerName*, örneğin *b2c*.
    d.  Merhaba Hello yolunu *başlangıç paketi* örnek dosyaları, örneğin *... \B2CTemplates\wingtiptoys*.

Yukarıdaki hello adımları izlediyseniz, HTML5 ve CSS dosyaları hello hello *UI Özelleştirme paketi* hello kurgusal şirket için **wingtiptoys** tooyour depolama hesabı artık işaret.  Merhaba içeriği doğru hello Azure portal hello ilgili kapsayıcı dikey açarak yüklendiğini doğrulayabilirsiniz. Alternatif olarak, hello içeriği düzgün bir tarayıcıdan hello sayfa erişerek yüklendiğini doğrulayabilirsiniz. Daha fazla bilgi için bkz: [Azure Active Directory B2C: toodemonstrate hello sayfası kullanıcı arabirimi (UI) özelleştirme özelliğini Yardımcısı aracı kullanılan](active-directory-b2c-reference-ui-customization-helper-tool.md).

## <a name="ensure-hello-storage-account-has-cors-enabled"></a>CORS'yi Hello depolama hesabı olduğundan emin olun

CORS (çıkış noktaları arası kaynak paylaşımı) olmalıdır, uç noktası için Azure AD B2C Premium tooload içeriğinizi etkin. Merhaba etki alanına Azure AD B2C Premium hello sayfasından hizmet daha içeriğinizi farklı bir etki alanında barındırılan olmasıdır.

CORS'yi, üzerinde içeriğinizi barındırma hello depolama sahip tooverify aşağıdaki adımları hello ile devam edin:

1. Bir tarayıcı oturumu açın ve toohello sayfadan *unified.html* depolama hesabınızdaki konumunu hello tam URL'yi kullanarak `https://<storageAccountName>.blob.core.windows.net/<containerName>/unified.html`. Örneğin, https://contoso369b2c.blob.core.windows.net/b2c/unified.html.
2. Toohttp://Test-cors.org gidin. Bu site, kullanmakta olduğunuz sayfa hello tooverify CORS'yi sahip sağlar.  
<!--
![test-cors.org](../../media/active-directory-b2c-customize-ui-of-a-user-journey/test-cors.png)
-->

3. İçinde **uzak URL**unified.html içeriğiniz için hello tam URL'yi girin ve tıklatın **İsteği Gönder**.
4. Merhaba, hello çıkışında doğrulayın **sonuçları** bölüm içerir *XHR durumu: 200*. Bu, CORS etkin olduğunu gösterir.
<!--
![CORS enabled](../../media/active-directory-b2c-customize-ui-of-a-user-journey/cors-enabled.png)
-->
Merhaba depolama hesabı adlı bir blob kapsayıcı şimdi içermelidir *b2c* içeren bizim çizimde hello wingtiptoys şablonları aşağıdaki hello *başlangıç paketi*.

<!--
![Correctly configured storage account](../../articles/active-directory-b2c/media/active-directory-b2c-reference-customize-ui-custom/storage-account-final.png)
-->

Merhaba aşağıdaki tabloda HTML5 sayfaları yukarıda hello hello amacını açıklar.

| HTML5 şablonu | Açıklama |
|----------------|-------------|
| *phonefactor.HTML* | Bu sayfa bir çok faktörlü kimlik doğrulaması sayfası için bir şablon olarak kullanılabilir. |
| *ResetPassword.HTML* | Bu sayfa için bir şablon olarak kullanılan bir parolanızı mı unuttunuz sayfasını. |
| *selfasserted.HTML* | Bu sayfa, sosyal hesap kayıt sayfası, yerel hesap kaydolma sayfası veya bir yerel hesap oturum açma sayfası için bir şablon olarak kullanılabilir. |
| *Unified.HTML* | Bu sayfa bir birleşik kayıt veya oturum açma sayfası için bir şablon olarak kullanılabilir. |
| *updateprofile.HTML* | Bu sayfa için bir profil güncelleştirme sayfası şablon olarak kullanılabilir. |

## <a name="add-a-link-tooyour-html5css-templates-tooyour-user-journey"></a>Bir bağlantı tooyour HTML5/CSS şablonları tooyour kullanıcı gezisine Ekle

Özel bir ilke doğrudan düzenleyerek bir bağlantı tooyour HTML5/CSS şablonları tooyour kullanıcı gezisine ekleyebilirsiniz.

Bu kullanıcı Yolculuklar kullanılabilir içerik tanımları listesinde belirtilen toobe Hello özel HTML5/CSS şablonları toouse kullanıcı Yolculuğunuzun içinde var. Bunun için isteğe bağlı bir  *<ContentDefinitions>*  XML öğesi altında hello bildirilmelidir  *<BuildingBlocks>*  özel ilke XML dosyasını bölümü.

Merhaba aşağıdaki tabloda hello hello Azure AD B2C kimlik deneyimi altyapısı ve toothem ilişkili sayfaları hello türü tarafından tanınan içerik tanımı kimlikleri açıklar.

| İçerik tanımı kimliği | Açıklama |
|-----------------------|-------------|
| *api.Error* | **Hata sayfası**. Bir özel durum ya da hatayla karşılaşıldığında bu sayfada görüntülenir. |
| *api.idpselections* | **Kimlik sağlayıcısı seçimi sayfası**. Bu sayfa, oturum açma sırasında kullanıcı hello sağlayıcıları seçebileceği kimlik listesini içerir. Kurumsal kimlik sağlayıcıları, Facebook ve Google + gibi sosyal kimlik sağlayıcıları ya da (e-posta adresi veya kullanıcı adına göre) yerel hesaplar şunlardır. |
| *api.idpselections.Signup* | **Kimlik sağlayıcısı seçimi için kaydolma**. Bu sayfa kullanıcı hello sağlayıcıları kayıt sırasında seçebileceği kimlik listesini içerir. Kurumsal kimlik sağlayıcıları, Facebook ve Google + gibi sosyal kimlik sağlayıcıları ya da (e-posta adresi veya kullanıcı adına göre) yerel hesaplar şunlardır. |
| *api.localaccountpasswordreset* | **Parolanızı mı unuttunuz sayfasını**. Bu sayfa bir formu içeren hello kullanıcının parolasını sıfırlama toofill tooinitiate sahip.  |
| *api.localaccountsignin* | **Yerel hesap oturum açma sayfası**. Bu sayfa bir oturum açma formu içeren bir e-posta adresi veya bir kullanıcı adı göre yerel bir hesap ile oturum açarken bu hello kullanıcı toofill vardır. Merhaba form, metin giriş kutusu ve parola giriş kutusu içerebilir. |
| *api.localaccountsignup* | **Yerel hesap kayıt sayfasına**. Bu sayfa bir kayıt formu içeren bir e-posta adresi veya bir kullanıcı adı göre yerel bir hesap için kaydolmak hello kullanıcı toofill vardır. Merhaba form metin giriş kutusuna, parola giriş kutusu, radyo düğmesi, tek seçimlik açılan kutuları ve çoklu seçim onay kutuları gibi farklı giriş denetimlerini içerebilir. |
| *api.phonefactor* | **Çok faktörlü kimlik doğrulaması sayfası**. Bu sayfada, kullanıcıların telefon numaralarına (metin veya sesli kullanarak) kaydolma veya oturum açma sırasında doğrulayabilirsiniz. |
| *api.selfasserted* | **Sosyal hesap kayıt sayfası**. Bu sayfa bir kayıt formu içeren hello kullanıcının ne zaman varolan kullanarak kaydolan hesap Facebook veya Google + gibi sosyal kimlik sağlayıcısından içinde toofill sahip. Sosyal hesap kayıt sayfası hello parola giriş alanlarının hello durumla yukarıda benzer toohello sayfasıdır. |
| *api.selfasserted.profileupdate* | **Profil güncelleştirme sayfası**. Bu sayfa bir formu içeren hello kullanıcı profillerini tooupdate kullanabilirsiniz. Sosyal hesap kayıt sayfası hello parola giriş alanlarının hello durumla yukarıda benzer toohello sayfasıdır. |
| *api.signuporsignin* | **Birleşik kayıt veya oturum açma sayfası**.  Bu sayfa, hem kaydolma ve oturum açma Kurumsal kimlik sağlayıcıları, Facebook veya Google + veya yerel hesaplar gibi sosyal kimlik sağlayıcıları kullanan kullanıcıların işler.

## <a name="next-steps"></a>Sonraki adımlar
[Başvuru: nasıl özel ilkeler anlamak hello B2C kimlik deneyimi Framework ile çalışma](active-directory-b2c-reference-custom-policies-understanding-contents.md)
