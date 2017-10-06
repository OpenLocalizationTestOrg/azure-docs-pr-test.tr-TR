---
title: "Azure Active Directory B2C: Sayfa UI Özelleştirme Yardımcısı aracı | Microsoft Docs"
description: "Bir yardımcı aracı toodemonstrate hello sayfası kullanıcı Arabirimi özelleştirme özelliğini Azure Active Directory B2C'de kullanılır."
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: ae935d52-3520-4a94-b66e-b35bb40e7514
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: swkrish
ms.openlocfilehash: 5137ac112019369b4244a925df1acb96fefb758f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-a-helper-tool-used-toodemonstrate-hello-page-user-interface-ui-customization-feature"></a>Azure Active Directory B2C: Yardımcısı aracı toodemonstrate hello sayfası kullanıcı arabirimi (UI) özelleştirme özelliğini kullanılır.
Bu makalede yardımcı toohello olan [ana UI Özelleştirme makalesi](active-directory-b2c-reference-ui-customization.md) Azure Active Directory (Azure AD) B2C içinde. Merhaba aşağıdaki adımlar nasıl tooexercise hello sayfası kullanıcı Arabirimi özelleştirme özelliğini sağladık örnek HTML ve CSS içerik kullanarak açıklar.

## <a name="get-an-azure-ad-b2c-tenant"></a>Bir Azure AD B2C kiracısı edinme
Herhangi bir şey özelleştirmeden önce çok gerekir[bir Azure AD B2C kiracısı edinme](active-directory-b2c-get-started.md) zaten yoksa.

## <a name="create-a-sign-up-or-sign-in-policy"></a>Bir kayıt veya oturum açma ilkesi oluşturma
Merhaba sunulmuştur örnek içeriği kullanılan toocustomze iki sayfalarında olabilir bir [kaydolma veya oturum açma ilkesi](active-directory-b2c-reference-policies.md): Merhaba [birleştirilmiş oturum açma sayfası](active-directory-b2c-reference-ui-customization.md) ve hello [kendi kendine sürülen öznitelikleri sayfa](active-directory-b2c-reference-ui-customization.md). Zaman [kaydolma veya oturum açma ilkesi oluşturma](active-directory-b2c-reference-policies.md#create-a-sign-up-or-sign-in-policy), yerel hesap (e-posta adresi), Facebook, Google ve Microsoft eklemek **kimlik sağlayıcıları**. Bunlar olan hello bizim örnek HTML içeriğini kabul edecek IDPs.  İsterseniz, bu IDPs kümesini de ekleyebilirsiniz.

## <a name="register-an-application"></a>Bir uygulamayı kaydetme
Çok gerekir[bir uygulamayı kaydetme](active-directory-b2c-app-registration.md) , B2C Kiracı kullanılan tooexecute ilkeniz olabilir. Uygulamanızı kaydolduktan sonra kaydolma ilkenizde çalıştırmak tooactually kullanabileceğiniz birkaç seçeneğiniz vardır:

* Hızlı Başlangıç uygulamaları "Merhaba kullanmaya başlayın" bölümünde listelenen hello Azure AD B2C birini yapı [oturum ayarlama ve tüketicilerinizin uygulamanıza oturum](active-directory-b2c-overview.md#get-started).
* Önceden oluşturulmuş kullanım hello [Azure AD B2C Playground](https://aadb2cplayground.azurewebsites.net) uygulama. Toouse hello playground seçerseniz, bir uygulama B2C kiracınızın hello kullanarak kaydetmelisiniz **yeniden yönlendirme URI'si** `https://aadb2cplayground.azurewebsites.net/`.
* Kullanım hello **Şimdi Çalıştır** ilkenizde hello düğmesinde [Azure portal](https://portal.azure.com/).

## <a name="customize-your-policy"></a>İlkeniz özelleştirme
toocustomize hello Görünüm ve yapısını ilkeniz, gereksinim duyduğunuz toofirst hello belirli kuralları Azure AD B2C kullanarak HTML ve CSS dosyaları oluşturun. Azure AD B2C erişebilmesi ardından statik içerik tooa genel kullanıma açık konumunuz karşıya yükleyebilirsiniz. Bu, kendi özel web sunucusu, Azure Blob Storage, Azure içerik teslim ağı veya tüm diğer statik kaynak barındırma sağlayıcı olabilir. Merhaba yalnızca gereksinimleri, içeriğinizi HTTPS üzerinden kullanılabilir ve CORS kullanarak erişilebilir değildir. Statik içeriğinizi hello web üzerinde açığa sonra ilke toopoint toothis konumu ve tooyour müşteriler içerik mevcut düzenleyebilirsiniz. Merhaba [ana UI Özelleştirme makalesi](active-directory-b2c-reference-ui-customization.md) hello Azure AD B2C özelleştirme özelliğinin nasıl çalıştığı ayrıntılı olarak açıklanmaktadır.

Bu öğreticinin Hello amaçları doğrultusunda, zaten bazı örnek içeriği oluşturulan artık ve Azure Blob Depolama alanında barındırılan. Merhaba örnek çok basit hello tema özelleştirmesinde kurgusal şirketimizin, "Wingtip Toys" içeriktir. tootry out kendi ilke içinde şu adımları izleyin:

1. Oturum açma tooyour Kiracı hello ' [Azure portal](https://portal.azure.com/) ve toohello B2C özellikleri dikey penceresine gidin.
2. Tıklatın **oturum açma veya kaydolma ilkeleri** tıkladıktan sonra ilkenizin (örneğin, "b2c\_1\_oturum\_yukarı\_oturum\_içinde").
3. Tıklatın **sayfa UI özelleştirme** ve ardından **Unified kaydolma veya oturum açma sayfası**.
4. İki durumlu hello **kullanım özel sayfa** çok geçiş**Evet**. Merhaba, **özel sayfa URI** alanına, `https://wingtiptoysb2c.blob.core.windows.net/b2c/wingtip/unified.html`. **Tamam** düğmesine tıklayın.
5. Tıklatın **yerel hesap kayıt sayfasına**. İki durumlu hello **özel şablonu kullan** çok geçiş**Evet**. Merhaba, **özel sayfa URI** alanına, `https://wingtiptoysb2c.blob.core.windows.net/b2c/wingtip/selfasserted.html`.
6. Hello için aynı adımı tekrarlayın hello **sosyal hesap kayıt sayfası**.
   Tıklatın **Tamam** iki kez tooclose hello UI Özelleştirme Kanatlar.
7. **Kaydet** düğmesine tıklayın.

Şimdi, özelleştirilmiş ilke deneyebilirsiniz. Kendi uygulama veya hello Azure AD B2C playground istediğiniz, ancak hello kısaca tıklayabilirsiniz kullanabilirsiniz **Şimdi Çalıştır** hello İlkesi dikey penceresinde komutu. Uygulamanızı hello açılan kutusunda seçin ve hello uygun yeniden yönlendirme URI'sini belirtin. Merhaba tıklatın **Şimdi Çalıştır** düğmesi. Yeni bir tarayıcı sekmesi açar ve yerinde hello yeni içerikle, uygulamanız için kaydolan hello kullanıcı deneyimi aracılığıyla çalıştırabilirsiniz!

## <a name="upload-hello-sample-content-tooazure-blob-storage"></a>Merhaba örnek içerik tooAzure Blob Storage karşıya yükle
Toouse Azure Blob Storage toohost isterseniz sayfanızın içeriği, kendi depolama hesabı oluşturma ve dosyalarınızı bizim B2C yardımcı aracı tooupload kullanın.

### <a name="create-a-storage-account"></a>Depolama hesabı oluşturma
1. İçinde toohello oturum [Azure portal](https://portal.azure.com/).
2. Tıklatın **+ yeni** > **veri + depolama** > **depolama hesabı**. Bir Azure aboneliği toocreate bir Azure Blob Storage hesabı gerekir. Merhaba, ücretsiz deneme yukarı imzalayabilirsiniz [Azure Web sitesi](https://azure.microsoft.com/pricing/free-trial/).
3. Sağlayan bir **adı** hello depolama hesabı (örneğin, "contoso") ve çekme hello için uygun seçimleri **fiyatlandırma katmanı**, **kaynak grubu** ve  **Abonelik**. Merhaba sahip olduğunuzdan emin olun **PIN tooStartboard** iade seçeneği. **Oluştur**'a tıklayın.
4. Toohello Sabitle geri dönün ve yeni oluşturduğunuz hello depolama hesabı'nı tıklatın.
5. Merhaba, **Özet** 'yi tıklatın **kapsayıcıları**ve ardından **+ Ekle**.
6. Sağlayan bir **adı** hello kapsayıcı (örneğin, "b2c") ve select **Blob** hello olarak **erişim türüne**. **Tamam** düğmesine tıklayın.
7. oluşturduğunuz hello kapsayıcı hello hello listesinde görünür **BLOB'lar** dikey. Merhaba kapsayıcı Hello URL'sini yazma; Örneğin, bu çok benzer görünmelidir`https://contoso.blob.core.windows.net/b2c`. Kapat hello **BLOB'lar** dikey.
8. Merhaba depolama hesabı dikey penceresinde **anahtarları** ve hello hello değerler yazma **depolama hesabı adı** ve **birincil erişim anahtarını** alanları.

> [!NOTE]
> **Birincil erişim anahtarını** önemli güvenlik kimlik bilgileri.
> 
> 

### <a name="download-hello-helper-tool-and-sample-files"></a>Merhaba yardımcı aracı ve örnek dosyalarını indirme
Merhaba indirebilirsiniz [.zip dosyası olarak Azure Blob Storage yardımcı aracı ve örnek dosyalar](https://github.com/azureadquickstarts/b2c-azureblobstorage-client/archive/master.zip) veya Github'dan kopyalayın:

```
git clone https://github.com/azureadquickstarts/b2c-azureblobstorage-client
```

Bu depo içeren bir `sample_templates\wingtip` örnek HTML, CSS ve görüntüleri içeren dizini. Kendi Azure Blob Depolama hesabı için bu şablonları tooreference gerekir tooedit hello HTML dosyaları. Açık `unified.html` ve `selfasserted.html` ve tüm örneklerini Değiştir `https://localhost` hello önceki adımda yazdığınız kendi kapsayıcı hello URL'si ile. HTML dosyaları hello etki alanı altında Azure AD tarafından hello HTML bu durumda, sunulacak çünkü hello hello mutlak yolu kullanmalısınız `https://login.microsoftonline.com`.

### <a name="upload-hello-sample-files"></a>Merhaba örnek dosyaları karşıya yükleme
Buna Merhaba aynı deponun, sıkıştırmasını `B2CAzureStorageClient.zip` ve çalışma hello `B2CAzureStorageClient.exe` içinde dosya. Bu program yalnızca tooyour depolama hesabı belirtin ve bu dosyaları için CORS erişimini etkinleştirmek hello dizindeki tüm hello dosyaları karşıya yükler. Yukarıdaki hello adımları izlediyseniz, hello HTML ve CSS dosyaları şimdi tooyour depolama hesabı işaret. Bu hello Not depolama hesabınızın adını önündeki hello parçası olduğu `blob.core.windows.net`; Örneğin, `contoso`. Merhaba içeriği doğru tooaccess deneyerek yüklendiğini doğrulayabilirsiniz `https://{storage-account-name}.blob.core.windows.net/{container-name}/wingtip/unified.html` bir tarayıcıdan. Aynı zamanda [http://test-cors.org/](http://test-cors.org/) toomake hello içeriği artık CORS'yi olduğundan emin. (Ara "XHR durumu: 200" Merhaba sonuç.)

### <a name="customize-your-policy-again"></a>İlkeniz, yeniden özelleştirme
Merhaba örnek içerik tooyour kendi depolama hesabı yüklediğiniz, kayıt ilkesi tooreference düzenlemeniz gerekir. Merhaba Hello adımları yineleyin ["ilkenizi özelleştirmek"](#customize-your-policy) yukarıdaki kendi depolama hesabının URL'leri kullanarak bu kez bölüm. Örneğin, konumunu Merhaba, `unified.html` dosya olacaktır `<url-of-your-container>/wingtip/unified.html`.

Artık hello kullanarak **Şimdi Çalıştır** düğmesini veya kendi uygulama tooexecute ilkeniz yeniden. Merhaba sonuç arama neredeyse tam olarak Merhaba, kullanılan aynı--hello aynı HTML ve CSS her iki durumda da örnek. Ancak, ilkelerinizi kendi örneğini Azure Blob Storage şimdi başvuruda bulunuyor ve ücretsiz tooedit olan ve hello dosyaları yeniden olarak Lütfen karşıya yükleyin. Merhaba özelleştirme hakkında daha fazla bilgi için HTML ve CSS, toohello başvuran [ana UI Özelleştirme makalesi](active-directory-b2c-reference-ui-customization.md).

