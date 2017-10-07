---
title: "Özel ilkeler - Azure AD B2C kullanarak bir UI Özelleştirme | Microsoft Docs"
description: "Azure AD B2C'de özel ilkeler kullanırken bir kullanıcı arabirimi (UI) özelleştirme hakkında bilgi edinin."
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: 658c597e-3787-465e-b377-26aebc94e46d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/04/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: 6f00995e54c9f9ef27cc51e38f3de07cd5817cc1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-configure-ui-customization-in-a-custom-policy"></a>Azure Active Directory B2C: Kullanıcı Arabirimi özelleştirme özel bir ilke yapılandırın.

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Bu makalede tamamladıktan sonra kaydolma ve oturum açma özel bir ilke ile marka ve görünümüne sahip olur. Azure Active Directory B2C ile (Azure AD B2C) elde hello HTML ve CSS içeriğin neredeyse tam denetim, toousers sunulan. Özel bir ilke kullandığınızda, kullanıcı arabirimini özelleştirme XML biçiminde hello Azure portal denetimleri kullanmak yerine yapılandırın. 

## <a name="prerequisites"></a>Ön koşullar

Başlamadan önce tamamlamanız [özel ilkeleri ile çalışmaya başlama](active-directory-b2c-get-started-custom.md). Çalışma özel bir ilke için kaydolma ve oturum açma yerel hesaplara sahip olmalıdır.

## <a name="page-ui-customization"></a>Sayfanın UI Özelleştirme

Başlangıç sayfası kullanıcı Arabirimi özelleştirme özelliğini kullanarak, herhangi bir özel ilke hello Görünüm ve yapısını özelleştirebilirsiniz. Ayrıca, marka ve uygulama ve Azure AD B2C arasında visual tutarlılık koruyabilirsiniz.

İşte nasıl çalışır?: Azure AD B2C, müşterinizin tarayıcıda kodu çalıştırır ve adlı modern bir yaklaşım kullanır [çıkış noktaları arası kaynak paylaşımı (CORS)](http://www.w3.org/TR/cors/). İlk olarak, özelleştirilmiş HTML içeriğe sahip hello özel ilkesindeki bir URL belirtin. Azure AD B2C kullanıcı Arabirimi öğeleri Merhaba, URL'den yüklenir ve hello sayfa toohello müşteri görüntüleyen HTML içeriği ile birleştirir.

## <a name="create-your-html5-content"></a>HTML5 içerik oluşturma

HTML hello başlığında ürününüzün marka adıyla içerik oluşturun.

1. HTML kod parçası aşağıdaki hello kopyalayın. Doğru biçimlendirilmiş boş bir öğesiyle HTML5 adlı  *\<div ID "API" =\>\</div\>*  hello içinde bulunan  *\<gövde\>*  etiketler. Bu öğe, Azure AD B2C içerik eklenen toobe nerede gösterir.

   ```html
   <!DOCTYPE html>
   <html>
   <head>
       <title>My Product Brand Name</title>
   </head>
   <body>
       <div id="api"></div>
   </body>
   </html>
   ```

   >[!NOTE]
   >Güvenlik nedenleriyle, JavaScript hello kullanımını özelleştirme için şu anda engelleniyor.

2. Bir metin düzenleyicisinde kopyalanan hello parçacığını yapıştırın ve sonra hello dosyası olarak kaydedin *özelleştirme ui.html*.

## <a name="create-an-azure-blob-storage-account"></a>Bir Azure Blob storage hesabı oluşturma

>[!NOTE]
> Bu makalede, bazı içeriklerin Azure Blob Depolama toohost kullanırız. İçeriğinizi bir web sunucusunda toohost seçebilirsiniz, ancak gerekir [web sunucunuz üzerinde CORS'yi etkinleştirmeniz](https://enable-cors.org/server.html).

toohost bu HTML içeriğine Blob depolama alanındaki hello aşağıdaki:

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Merhaba üzerinde **Hub** menüsünde, select **yeni** > **depolama** > **depolama hesabı**.
3. Benzersiz bir girin **adı** depolama hesabınız için.
4. **Dağıtım modeli** kalabileceği **Resource Manager**.
5. Değişiklik **hesap türü** çok**Blob storage**.
6. **Performans** kalabileceği **standart**.
7. **Çoğaltma** kalabileceği **RA-GRS**.
8. **Erişim katmanı** kalabileceği **etkin**.
9. **Depolama hizmeti şifrelemesi** kalabileceği **devre dışı**.
10. Seçin bir **abonelik** depolama hesabınız için.
11. Oluşturma bir **kaynak grubu** veya varolan bir tanesini seçin.
12. Select hello **coğrafi konum** depolama hesabınız için.
13. Tıklatın **oluşturma** toocreate hello depolama hesabı.  
    Merhaba dağıtım tamamlandıktan sonra hello **depolama hesabı** dikey penceresinde otomatik olarak açılır.

## <a name="create-a-container"></a>Bir kapsayıcı oluşturma

Blob storage, ortak bir kapsayıcıda toocreate hello aşağıdaki:

1. Merhaba tıklatın **genel bakış** sekmesi.
2. Tıklatın **kapsayıcı**.
3. İçin **adı**, türü **$root**.
4. Ayarlama **erişim türüne** çok**Blob**.
5. Tıklatın **$root** tooopen hello yeni kapsayıcı.
6. **Karşıya Yükle**'ye tıklayın.
7. Merhaba klasör simgesine tıklayın sonraki çok**bir dosya seçin**.
8. Çok Git**özelleştirme ui.html**, hello daha önce oluşturmuş olduğunuz [sayfa UI özelleştirme](#the-page-ui-customization-feature) bölümü.
9. **Karşıya Yükle**'ye tıklayın.
10. Karşıya yüklediğiniz hello özelleştirme ui.html blob seçin.
11. Sonraki çok**URL**, tıklatın **kopya**.
12. Bir tarayıcıda, kopyalanan hello URL'sini yapıştırın ve toohello sitesine gidin. Merhaba site erişilemiyorsa hello kapsayıcı erişim türü çok ayarlandığından emin olun**blob**.

## <a name="configure-cors"></a>CORS'yi yapılandırın

BLOB Depolama çıkış noktaları arası kaynak paylaşımı için hello aşağıdakileri yaparak yapılandırın:

>[!NOTE]
>Bizim örnek HTML ve CSS içerik kullanarak hello UI Özelleştirme özelliği çıkışı tootry istiyorsunuz? Sağladık [basit Yardımcısı aracı](active-directory-b2c-reference-ui-customization-helper-tool.md) karşıya yükleyen ve Blob Depolama hesabınıza bizim örnek içeriği yapılandırır. İleri hello aracı kullanırsanız, çok atlayabilirsiniz[oturum açma veya kaydolma özel ilkenizi değiştirmek](#modify-your-sign-up-or-sign-in-custom-policy).

1. Merhaba üzerinde **depolama** dikey altında **ayarları**, açık **CORS**.
2. **Ekle**'ye tıklayın.
3. İçin **çıkış izin**, bir yıldız işareti girin (\*).
4. Merhaba, **fiillere izin** açılan listesinden, select **almak** ve **seçenekleri**.
5. İçin **üstbilgileri izin**, bir yıldız işareti girin (\*).
6. İçin **sunulan üstbilgileri**, bir yıldız işareti girin (\*).
7. İçin **en uzun geçerlilik süresi (saniye)**, türü **200**.
8. **Ekle**'ye tıklayın.

## <a name="test-cors"></a>Test CORS

Merhaba aşağıdakileri yaparak hazırsınız olduğunu doğrulama:

1. Toohello Git [test cors.org](http://test-cors.org/) Web sitesi ve Yapıştır hello hello URL'de **uzak URL** kutusu.
2. Tıklatın **gönderme isteği**.  
    Bir hata alırsanız, emin olun, [CORS ayarları](#configure-cors) doğrudur. Ayrıca tarayıcı önbelleğiniz tooclear ihtiyacınız veya Ctrl + Shift + P tuşuna basarak bir özel tarayıcı oturumu açın.

## <a name="modify-your-sign-up-or-sign-in-custom-policy"></a>Oturum açma veya kaydolma özel ilkesini değiştirme

Üst düzey hello altında  *\<TrustFrameworkPolicy\>*  etiketi, bulmanız gerekir  *\<BuildingBlocks\>*  etiketi. Merhaba içinde  *\<BuildingBlocks\>*  etiketler eklemek bir  *\<ContentDefinitions\>*  aşağıdaki örneğine hello kopyalayarak etiketi. Değiştir *your_storage_account* depolama hesabınızın hello ada sahip.

  ```xml
  <BuildingBlocks>
    <ContentDefinitions>
      <ContentDefinition Id="api.idpselections">
        <LoadUri>https://{your_storage_account}.blob.core.windows.net/customize-ui.html</LoadUri>
      </ContentDefinition>
    </ContentDefinitions>
  </BuildingBlocks>
  ```

## <a name="upload-your-updated-custom-policy"></a>Güncelleştirilmiş özel ilkeniz karşıya yükle

1. Merhaba, [Azure portal](https://portal.azure.com), [geçiş hello Azure AD B2C kiracınızın bağlamına](active-directory-b2c-navigate-to-b2c-context.md)ve ardından hello açın **Azure AD B2C** dikey.
2. Tıklatın **tüm ilkeleri**.
3. Tıklatın **karşıya İlkesi**.
4. Karşıya yükleme `SignUpOrSignin.xml` hello ile  *\<ContentDefinitions\>*  daha önce eklediğiniz etiketi.

## <a name="test-hello-custom-policy-by-using-run-now"></a>Test hello özel ilke kullanarak **Şimdi Çalıştır**

1. Merhaba üzerinde **Azure AD B2C** dikey penceresinde çok Git**tüm ilkeler**.
2. Karşıya yüklediğiniz hello özel ilkesini seçin ve hello tıklayın **Şimdi Çalıştır** düğmesi.
3. Bir e-posta adresi kullanarak yukarı mümkün toosign olması gerekir.

## <a name="reference"></a>Başvuru

Buraya kullanıcı arabirimini özelleştirme örnek şablonları bulabilirsiniz:

```
git clone https://github.com/azureadquickstarts/b2c-azureblobstorage-client
```

Aşağıdaki HTML dosyaları hello Hello sample_templates/wingtip klasör içerir:

| HTML5 şablonu | Açıklama |
|----------------|-------------|
| *phonefactor.HTML* | Bu dosyayı bir çok faktörlü kimlik doğrulaması sayfası için bir şablon olarak kullanın. |
| *ResetPassword.HTML* | Bu dosya için bir şablon olarak kullanmak bir parolanızı mı unuttunuz sayfasını. |
| *selfasserted.HTML* | Bu dosya, sosyal hesap kayıt sayfası, yerel hesap kaydolma sayfası veya bir yerel hesap oturum açma sayfası için bir şablon olarak kullanın. |
| *Unified.HTML* | Bu dosyayı bir birleşik kayıt veya oturum açma sayfası için bir şablon olarak kullanın. |
| *updateprofile.HTML* | Bu dosya için bir profil güncelleştirme sayfası şablon olarak kullanın. |

Merhaba, [, oturum açma veya kaydolma özel ilke bölümünü değiştirme](#modify-your-sign-up-or-sign-in-custom-policy), hello içerik tanımı için yapılandırılmış `api.idpselections`. İçerik tanımı hello Azure AD B2C kimlik deneyimi framework ve açıklamalarının tarafından tanınan kimlikleri Hello kümesini aşağıdaki tablonun hello şunlardır:

| İçerik tanımı kimliği | Açıklama | 
|-----------------------|-------------|
| *api.Error* | **Hata sayfası**. Bir özel durum ya da hatayla karşılaşıldığında bu sayfada görüntülenir. |
| *api.idpselections* | **Kimlik sağlayıcısı seçimi sayfası**. Bu sayfa, oturum açma sırasında kullanıcı hello sağlayıcıları seçebileceği kimlik listesini içerir. Bu, Kurumsal kimlik sağlayıcıları, Facebook ve Google + gibi sosyal kimlik sağlayıcıları ya da yerel hesaplar seçeneklerdir. |
| *api.idpselections.Signup* | **Kimlik sağlayıcısı seçimi için kaydolma**. Bu sayfa kullanıcı hello sağlayıcıları kayıt sırasında seçebileceği kimlik listesini içerir. Bu, Kurumsal kimlik sağlayıcıları, Facebook ve Google + gibi sosyal kimlik sağlayıcıları ya da yerel hesaplar seçeneklerdir. |
| *api.localaccountpasswordreset* | **Parolanızı mı unuttunuz sayfasını**. Bu sayfa bir formu içeren hello kullanıcı parola sıfırlama tooinitiate tamamlamanız gerekir.  |
| *api.localaccountsignin* | **Yerel hesap oturum açma sayfası**. Bu sayfa bir e-posta adresi veya bir kullanıcı adı göre yerel bir hesap ile oturum imzalamak için bir oturum açma formu içerir. Merhaba form, metin giriş kutusu ve parola giriş kutusu içerebilir. |
| *api.localaccountsignup* | **Yerel hesap kayıt sayfasına**. Bu sayfa bir e-posta adresi veya bir kullanıcı adı göre yerel bir hesap için kaydolduğunuz için bir kayıt formu içerir. Merhaba form metin giriş kutusu, bir parola giriş kutusu, bir radyo düğmesi, tek seçimlik açılan kutuları ve çoklu seçim onay kutuları gibi çeşitli giriş denetimlerini içerebilir. |
| *api.phonefactor* | **Çok faktörlü kimlik doğrulaması sayfası**. Bu sayfada, kullanıcıların telefon numaralarına (metin veya sesli kullanarak) kaydolma veya oturum açma sırasında doğrulayabilirsiniz. |
| *api.selfasserted* | **Sosyal hesap kayıt sayfası**. Bu sayfa, bunlar Facebook veya Google + gibi sosyal kimlik sağlayıcısından var olan bir hesabı kullanarak kaydolduğunuzda, kullanıcılar tamamlamalısınız bir kayıt formu içerir. Bu sayfa hello parola giriş alanları dışında sosyal hesap kayıt sayfası, önceki benzer toohello içindir. |
| *api.selfasserted.profileupdate* | **Profil güncelleştirme sayfası**. Bu sayfa kullanıcı profillerini tooupdate kullanabileceğiniz bir form içerir. Bu sayfa benzer toohello sosyal hesap kaydolma, hello parola giriş alanları dışında sayfasıdır. |
| *api.signuporsignin* | **Birleşik kayıt veya oturum açma sayfası**. Bu sayfa, kaydolma ve oturum açma Kurumsal kimlik sağlayıcıları, Facebook veya Google + veya yerel hesaplar gibi sosyal kimlik sağlayıcıları kullanan kullanıcılar, her iki hello işler.  |

## <a name="next-steps"></a>Sonraki adımlar

Özelleştirilebilir kullanıcı Arabirimi öğeleri hakkında ek bilgi için bkz: [yerleşik ilkeleri için kullanıcı Arabirimi özelleştirme için başvuru kılavuzu](active-directory-b2c-reference-ui-customization.md).
