---
title: aaaConfigure Git - Azure kullanarak, API Management hizmetiniz | Microsoft Docs
description: "Bilgi nasıl toosave ve Git kullanarak API Management hizmeti yapılandırmanızı yapılandırın."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: mattfarm
ms.assetid: 364cd53e-88fb-4301-a093-f132fa1f88f5
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: ef7d4c18f2ea3f5c9b86403349a83aef240f979b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosave-and-configure-your-api-management-service-configuration-using-git"></a>Nasıl toosave ve Git kullanarak API Management hizmeti yapılandırmanızı yapılandırın
> 
> 

Her API Management hizmeti örneği hello yapılandırması ve hello hizmet örneği için meta veriler hakkında bilgi içeren bir yapılandırma veritabanı tutar. Değişiklikleri toohello hizmet örneği hello yayımcı Portalı'ndaki bir ayarı değiştirmek, bir PowerShell cmdlet'ini kullanarak veya bir REST API çağrısı yapma yapılabilir. Ayrıca toothese yöntemleri, Git kullanarak, hizmet yönetim senaryoları gibi etkinleştirme, hizmet örneği yapılandırması da yönetebilirsiniz:

* Yapılandırma sürüm oluşturma - karşıdan yüklemek ve hizmetinizi farklı sürümlerini depolamak
* Yapılandırma değişiklikleri toplu - yerel depoda hizmetinizi toomultiple bölümlerini değişiklik ve hello değişiklikleri geri toohello sunucusunu tek bir işlem ile tümleştirme
* Tanıdık Git araç zinciri ve iş akışı - hello Git araçları ve zaten aşina iş akışlarını kullanma

Diyagram aşağıdaki hello hello farklı şekillerde tooconfigure genel bir bakış API Management hizmet örneği gösterir.

![Git yapılandırın][api-management-git-configure]

Merhaba yayımcı portalı, PowerShell cmdlet'leri veya hello REST API kullanarak tooyour hizmeti bir değişiklik yaptığınızda hello kullanarak hizmet yapılandırma veritabanınızı yönettiğiniz `https://{name}.management.azure-api.net` hello sağ tarafında hello diyagramda gösterildiği gibi endpoint. Merhaba diyagramı sol tarafındaki Hello gösterilmektedir hizmeti yapılandırmanızı Git kullanarak nasıl yönetebileceğinizi ve hizmetiniz için Git deposu bulunan `https://{name}.scm.azure-api.net`.

Aşağıdaki adımları hello Git kullanarak, API Management hizmet örneğinizin yönetimine genel bir bakış sağlar.

1. Hizmet erişim Git yapılandırması
2. Hizmet yapılandırma veritabanı tooyour Git deponuza Kaydet
3. Merhaba Git deposuna tooyour yerel makineyi kopyalama
4. Merhaba son depodaki tooyour yerel makinede aşağı ve tamamlama ve anında iletme değişiklikleri geri tooyour depodaki isteme
5. Hizmet yapılandırma veritabanınıza, depodaki Hello değişikliklerden dağıtma

Bu makalede nasıl tooenable ve Git toomanage hizmetinizi kullanabilir ve hello dosya ve klasörleri hello Git deposu için bir başvuru sağlar.

## <a name="access-git-configuration-in-your-service"></a>Hizmet erişim Git yapılandırması
Merhaba sağ üst köşesinde hello yayımcı portalına hello Git simge görüntüleyerek hızla Git yapılandırmanızı hello durumunu görüntüleyebilirsiniz. Bu örnekte, kaydedilmemiş değişiklikler toohello depo olduğunu hello durum iletisi gösterir. Merhaba API Management hizmeti yapılandırma veritabanına toohello deposu henüz kaydedilmedi olmasıdır.

![Git durumu][api-management-git-icon-enable]

tooview ve Git yapılandırma ayarlarını yapılandırma, hello Git simgesine tıklayın veya hello tıklatın **güvenlik** menü toohello giderek **yapılandırma deposu** sekmesi.

![GIT etkinleştir][api-management-enable-git]

> [!IMPORTANT]
> Özellikleri hello deposunda saklanır ve onun geçmişinde dek kalacak şekilde, tanımlı değil tüm gizli devre dışı bırakın ve Git erişim yeniden etkinleştirin. Özellikler sağlayan güvenli bir yerde toomanage toostore aktarıp gizli tüm API yapılandırması ve ilkeleri de dahil olmak üzere sabit dize değerleri, doğrudan ilke deyimleri bunları. Daha fazla bilgi için bkz: [nasıl Azure API yönetimi ilkelerini toouse özelliklerinde](api-management-howto-properties.md).
> 
> 

Etkinleştirme veya hello REST API kullanarak Git erişimini devre dışı bırakma hakkında daha fazla bilgi için bkz: [etkinleştirmek veya devre dışı hello REST API kullanarak Git erişim](https://msdn.microsoft.com/library/dn781420.aspx#EnableGit).

## <a name="toosave-hello-service-configuration-toohello-git-repository"></a>toosave hello hizmet yapılandırma toohello Git deposu
Merhaba depo kopyalama önce hello ilk toosave hello geçerli durumunu hello hizmeti yapılandırma toohello havuzu adımdır. Tıklatın **yapılandırma toorepository kaydetmek**.

![Yapılandırmayı kaydedin][api-management-save-configuration]

Merhaba onay ekranda istediğiniz değişiklikleri yapın ve tıklatın **Tamam** toosave.

![Yapılandırmayı kaydedin][api-management-save-configuration-confirm]

Birkaç dakika sonra hello yapılandırma kaydedilir ve başlangıç tarihi ve saati hello son yapılandırma değişikliği ve hello hizmet yapılandırmasını ve hello arasındaki hello son eşitleme dahil olmak üzere hello yapılandırma durumu hello havuzun görüntülenir Depo.

![Yapılandırma durumu][api-management-configuration-status]

Merhaba yapılandırma toohello depo kaydedildikten sonra kopyalanabilir.

Merhaba REST API'sini kullanarak bu işlemi gerçekleştirme hakkında daha fazla bilgi için bkz: [hello REST API kullanarak anlık görüntü yürütme yapılandırma](https://msdn.microsoft.com/library/dn781420.aspx#CommitSnapshot).

## <a name="tooclone-hello-repository-tooyour-local-machine"></a>tooclone hello depo tooyour yerel makine
bir depo tooclone hello URL tooyour deposu, bir kullanıcı adı ve parola gerekir. Merhaba kullanıcı adı ve URL hello hello yukarıya yakın görüntülenir **yapılandırma deposu** sekmesi.

![Git kopyalama][api-management-configuration-git-clone]

Merhaba hello altındaki oluşturulan Hello parola **yapılandırma deposu** sekmesi.

![Parola oluştur][api-management-generate-password]

toogenerate bir parola önce o hello emin **süre sonu** sona erme tarihi ve saati istenen toohello ayarlayın ve ardından **belirteç Oluştur**.

![Parola][api-management-password]

> [!IMPORTANT]
> Bu parolayı not edin. Çıktıktan sonra bu sayfayı hello parolayı yeniden görüntülenmeyecek.
> 
> 

Örnek Kullanım hello Git Bash hello aracı [Windows için Git](http://www.git-scm.com/downloads) ancak bilginiz herhangi bir Git aracını kullanabilirsiniz.

Git aracınızı hello istenen klasöründe açın ve aşağıdaki komutu tooclone hello git deposu tooyour yerel makine, hello yayımcı portalı tarafından sağlanan hello komutunu kullanarak hello çalıştırın.

```
git clone https://bugbashdev4.scm.azure-api.net/
```

Merhaba kullanıcı adı ve istendiğinde parolayı belirtin.

Herhangi bir hata alırsanız, değiştirmeyi deneyin, `git clone` komut tooinclude hello kullanıcı adı ve parola, hello aşağıdaki örnekte gösterildiği gibi.

```
git clone https://username:password@bugbashdev4.scm.azure-api.net/
```

Bu bir hata sağlıyorsa, URL hello komutu hello parola bölümü kodlama deneyin. Bir hızlı yol toodo bu tooopen Visual Studio ve sorunu hello şu komutu hello **komut penceresi**. tooopen hello **komut penceresi**, herhangi bir çözüm veya proje Visual Studio'da açın (veya yeni bir boş konsol uygulaması oluşturun) ve seçin **Windows**, **hemen** gelen Merhaba **hata ayıklama** menüsü.

```
?System.NetWebUtility.UrlEncode("password from publisher portal")
```

Kodlanmış hello parola, kullanıcı adını ve depo konumu tooconstruct hello git komutu ile birlikte kullanın.

```
git clone https://username:url encoded password@bugbashdev4.scm.azure-api.net/
```

Merhaba deposu kopyalanması sonra görüntülemek ve, yerel dosya sistemi ile çalışır. Daha fazla bilgi için bkz: [dosya ve klasör yapısı yerel Git deposu başvuru](#file-and-folder-structure-reference-of-local-git-repository).

## <a name="tooupdate-your-local-repository-with-hello-most-current-service-instance-configuration"></a>tooupdate yerel deponuza yapılandırmasıyla hello en güncel hizmet örneği
Merhaba yayımcı portalı veya hello REST API kullanarak değişiklikleri tooyour API Management hizmet örneği yaparsanız, yerel deponuza hello en son değişikliklerle güncelleştirmek için önce bu değişiklikleri toohello depo kaydetmeniz gerekir. toodo bunu, **yapılandırma toorepository kaydetmek** hello üzerinde **yapılandırma deposu** sekmesinde hello yayımcı Portalı'nda ve yerel deponuza komutunda aşağıdaki hello sorun.

```
git pull
```

Çalıştırmadan önce `git pull` için yerel deponuza hello klasörde olduğundan emin olun. Merhaba yalnızca tamamladıysanız `git clone` hello aşağıdaki gibi bir komutu çalıştırarak hello dizin tooyour depodaki değiştirmeli sonra komutu.

```
cd bugbashdev4.scm.azure-api.net/
```

## <a name="toopush-changes-from-your-local-repo-toohello-server-repo"></a>Yerel Depodaki toohello sunucu depodaki toopush değişiklikler
Yerel deposu toohello sunucu depodan toopush değiştirir, yaptığınız değişiklikleri kaydetmek ve bunları toohello sunucu deposu gönderme gerekir. toocommit yaptığınız değişiklikler, Git komut aracı, anahtar toohello dizinin yerel deposu ve aşağıdaki komutları sorunu hello açın.

```
git add --all
git commit -m "Description of your changes"
```

Tüm hello tamamlar çalıştırmak toohello sunucu toopush hello komutu.

```
git push
```

## <a name="toodeploy-any-service-configuration-changes-toohello-api-management-service-instance"></a>toodeploy tüm hizmet yapılandırma değişiklikleri toohello API Management hizmeti örneği
Kabul edilen ve basılmış toohello sunucu deposu yerel değişikliklerinizi olduktan sonra bunları tooyour API Management hizmet örneği dağıtabilirsiniz.

![Dağıtma][api-management-configuration-deploy]

Merhaba REST API'sini kullanarak bu işlemi gerçekleştirme hakkında daha fazla bilgi için bkz: [dağıtmak Git değişiklikleri hello REST API kullanarak tooconfiguration veritabanı](https://docs.microsoft.com/en-us/rest/api/apimanagement/tenantconfiguration).

## <a name="file-and-folder-structure-reference-of-local-git-repository"></a>Yerel Git deposu dosya ve klasör yapısı başvurusu
Merhaba hello yerel git deposu bulunan dosya ve klasörleri hello hizmet örneği hakkında hello yapılandırma bilgilerini içerir.

| Öğe | Açıklama |
| --- | --- |
| Kök API management klasörü |Merhaba hizmet örneği için en üst düzey yapılandırmayı içerir |
| API klasörü |Merhaba hizmet örneği içinde hello API'leri için Hello yapılandırmayı içerir |
| grupları klasörü |Merhaba hizmet örneği içinde hello grupları için Hello yapılandırmayı içerir |
| ilkeleri klasörü |Merhaba hizmet örneği içinde Hello ilkelerini içerir |
| portalStyles klasörü |Merhaba hizmet örneği içinde hello Geliştirici Portalı özelleştirmeleri için Hello yapılandırmayı içerir |
| Ürünler klasörü |Merhaba hizmet örneği içinde hello ürünleri için Hello yapılandırmayı içerir |
| Şablonlar klasörü |Merhaba hizmet örneği içinde hello e-posta şablonları için Hello yapılandırmayı içerir |

Her klasör bir veya daha fazla içerebilir ve bazı durumlarda bir veya daha fazla klasör, örneğin her API, ürün veya grup için bir klasör durumda. Her klasördeki Hello dosyalar hello klasör adı tarafından açıklanan hello varlık türü için özeldir.

| Dosya türü | Amaç |
| --- | --- |
| JSON |Yapılandırma bilgilerini hello ilgili varlık hakkında |
| HTML |Açıklamaları genellikle hello Geliştirici Portalı'nda görüntülenen hello varlık hakkında |
| xml |İlke deyimleri |
| CSS |Geliştirici Portalı özelleştirme için stil sayfaları |

Bu dosyalar oluşturulabilir, silinen, düzenlenemez ve yerel dosya sisteminde yönetilen ve hello değişiklikleri geri toohello API Management hizmet örneğinizin dağıtılır.

> [!NOTE]
> Merhaba aşağıdaki varlıklar hello Git deposunda yer almayan ve Git kullanılarak yapılandırılamaz.
> 
> * Kullanıcılar
> * Abonelikler
> * Özellikler
> * Geliştirici Portalı varlıkları stilleri dışında
> 
> 

### <a name="root-api-management-folder"></a>Kök API management klasörü
Merhaba kök `api-management` klasörünü içeren bir `configuration.json` biçimini izleyen hello hello hizmet örneği hakkında üst düzey bilgileri içeren dosya.

```json
{
  "settings": {
    "RegistrationEnabled": "True",
    "UserRegistrationTerms": null,
    "UserRegistrationTermsEnabled": "False",
    "UserRegistrationTermsConsentRequired": "False",
    "DelegationEnabled": "False",
    "DelegationUrl": "",
    "DelegatedSubscriptionEnabled": "False",
    "DelegationValidationKey": ""
  },
  "$ref-policy": "api-management/policies/global.xml"
}
```

ilk dört ayarları hello (`RegistrationEnabled`, `UserRegistrationTerms`, `UserRegistrationTermsEnabled`, ve `UserRegistrationTermsConsentRequired`) üzerinde hello ayarları aşağıdaki toohello eşleme **kimlikleri** hello sekmesinde **güvenlik** bölümü.

| Kimlik ayarı | Çok eşlemeleri|
| --- | --- |
| RegistrationEnabled |**Anonim kullanıcılar toosign açma sayfasına yeniden yönlendir** onay kutusu |
| UserRegistrationTerms |**Kullanıcı Kaydolma kullanım koşullarını** metin kutusu |
| UserRegistrationTermsEnabled |**Kullanım koşulları kaydolma sayfasında göster** onay kutusu |
| UserRegistrationTermsConsentRequired |**Onay gerektiren** onay kutusu |

![Kimlik ayarları][api-management-identity-settings]

Sonraki dört ayarları hello (`DelegationEnabled`, `DelegationUrl`, `DelegatedSubscriptionEnabled`, ve `DelegationValidationKey`) üzerinde hello ayarları aşağıdaki toohello eşleme **temsilci** hello sekmesinde **güvenlik** bölümü.

| Temsilci ayarı | Çok eşlemeleri|
| --- | --- |
| DelegationEnabled |**Oturum açma ve kaydolma temsilci** onay kutusu |
| DelegationUrl |**Temsilci uç nokta URL'si** metin kutusu |
| DelegatedSubscriptionEnabled |**Temsilci ürün aboneliği** onay kutusu |
| DelegationValidationKey |**Doğrulama anahtarı temsilci** metin kutusu |

![Temsilci ayarları][api-management-delegation-settings]

Merhaba son ayar `$ref-policy`, toohello genel ilke deyimleri dosya hello hizmet örneği için eşler.

### <a name="apis-folder"></a>API klasörü
Merhaba `apis` klasörü aşağıdaki öğelerindeki hello içeren hello hizmet örneği içinde her API için bir klasör içerir.

* `apis\<api name>\configuration.json`-Bu hello API için başlangıç yapılandırmasını ve hello arka uç hizmeti URL'si ve hello işlemleri hakkındaki bilgileri içerir. Merhaba budur toocall olsaydı döndürülür aynı bilgileri [belirli bir API alma](https://msdn.microsoft.com/library/azure/dn781423.aspx#GetAPI) ile `export=true` içinde `application/json` biçimi.
* `apis\<api name>\api.description.html`-Bu hello API hello açıklaması ve toohello karşılık gelen `description` hello özelliğinin [API varlık](https://msdn.microsoft.com/library/azure/dn781423.aspx#EntityProperties).
* `apis\<api name>\operations\`-Bu klasörde `<operation name>.description.html` hello API toohello işlemlerinde eşleme dosyaları. Her dosya hello toohello eşleştiren API tek bir işlemde hello açıklamasını içerir `description` hello özelliğinin [işlemi varlık](https://msdn.microsoft.com/library/azure/dn781423.aspx#OperationProperties) hello REST API de.

### <a name="groups-folder"></a>grupları klasörü
Merhaba `groups` klasörü hello hizmet örneği içinde tanımlanan her grup için bir klasör içerir.

* `groups\<group name>\configuration.json`-Bu hello hello grubu için bir yapılandırmadır. Merhaba budur toocall hello olsaydı döndürülür aynı bilgileri [belirli bir grup alma](https://msdn.microsoft.com/library/azure/dn776329.aspx#GetGroup) işlemi.
* `groups\<group name>\description.html`-Bu hello grubunun hello açıklaması ve toohello karşılık gelen `description` hello özelliğinin [Grup varlık](https://msdn.microsoft.com/library/azure/dn776329.aspx#EntityProperties).

### <a name="policies-folder"></a>ilkeleri klasörü
Merhaba `policies` klasörü hizmet örneğiniz hello İlkesi ifadeleri içerir.

* `policies\global.xml`-Hizmet Örneğiniz için genel kapsamda tanımlanan ilkeleri içerir.
* `policies\apis\<api name>\`-API kapsamda tanımlanan tüm ilkeler varsa, bu klasörde yer alır.
* `policies\apis\<api name>\<operation name>\`Klasör - işlemi kapsamında tanımlı tüm ilkeler varsa, bu klasörde yer alır `<operation name>.xml` toohello ilke deyimleri her işlem için eşleme dosyaları.
* `policies\products\`-Ürün kapsamda tanımlanan tüm ilkeler varsa, bunlar içeren bu klasörde yer alan `<product name>.xml` toohello ilke deyimleri her ürün için eşleme dosyaları.

### <a name="portalstyles-folder"></a>portalStyles klasörü
Merhaba `portalStyles` klasörü, Geliştirici Portalı özelleştirmeler hello hizmet örneği için yapılandırma ve stil sayfalarını içerir.

* `portalStyles\configuration.json`-hello Geliştirici Portalı tarafından kullanılan hello stil sayfaları hello adlarını içerir
* `portalStyles\<style name>.css`-Her `<style name>.css` dosyasını içeren hello Geliştirici Portalı için stiller (`Preview.css` ve `Production.css` varsayılan olarak).

### <a name="products-folder"></a>Ürünler klasörü
Merhaba `products` klasörü hello hizmet örneği içinde tanımlanan her ürün için bir klasör içerir.

* `products\<product name>\configuration.json`-Bu hello hello ürünü için bir yapılandırmadır. Merhaba budur toocall hello olsaydı döndürülür aynı bilgileri [belirli bir ürün almak](https://msdn.microsoft.com/library/azure/dn776336.aspx#GetProduct) işlemi.
* `products\<product name>\product.description.html`-Bu hello ürününün hello açıklaması ve toohello karşılık gelen `description` hello özelliğinin [ürün varlığı](https://msdn.microsoft.com/library/azure/dn776336.aspx#Product) hello REST API de.

### <a name="templates"></a>şablonları
Merhaba `templates` hello yapılandırmasını içeren klasör [şablonları e-posta](api-management-howto-configure-notifications.md) hello hizmet örneği.

* `<template name>\configuration.json`-Bu hello hello e-posta şablonu için bir yapılandırmadır.
* `<template name>\body.html`-hello hello e-posta şablonunun gövdesini budur.

## <a name="next-steps"></a>Sonraki adımlar
Diğer yolları toomanage hakkında bilgi için hizmet örneği bakın:

* Hizmet örneğinizi PowerShell cmdlet'lerini aşağıdaki hello kullanarak yönetme
  * [Hizmet dağıtımı PowerShell cmdlet başvurusu](https://msdn.microsoft.com/library/azure/mt619282.aspx)
  * [Hizmet Yönetimi PowerShell cmdlet başvurusu](https://msdn.microsoft.com/library/azure/mt613507.aspx)
* Hizmet örneğinizi hello yayımcı portalında Yönet
  * [İlk API'nizi yönetme](api-management-get-started.md)
* Hizmet örneğinizi Hello REST API kullanarak yönetme
  * [API Management REST API Başvurusu](https://msdn.microsoft.com/library/azure/dn776326.aspx)

## <a name="watch-a-video-overview"></a>Video genel izleyin
> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Configuration-over-Git/player]
> 
> 

[api-management-enable-git]: ./media/api-management-configuration-repository-git/api-management-enable-git.png
[api-management-git-enabled]: ./media/api-management-configuration-repository-git/api-management-git-enabled.png
[api-management-save-configuration]: ./media/api-management-configuration-repository-git/api-management-save-configuration.png
[api-management-save-configuration-confirm]: ./media/api-management-configuration-repository-git/api-management-save-configuration-confirm.png
[api-management-configuration-status]: ./media/api-management-configuration-repository-git/api-management-configuration-status.png
[api-management-configuration-git-clone]: ./media/api-management-configuration-repository-git/api-management-configuration-git-clone.png
[api-management-generate-password]: ./media/api-management-configuration-repository-git/api-management-generate-password.png
[api-management-password]: ./media/api-management-configuration-repository-git/api-management-password.png
[api-management-git-configure]: ./media/api-management-configuration-repository-git/api-management-git-configure.png
[api-management-configuration-deploy]: ./media/api-management-configuration-repository-git/api-management-configuration-deploy.png
[api-management-identity-settings]: ./media/api-management-configuration-repository-git/api-management-identity-settings.png
[api-management-delegation-settings]: ./media/api-management-configuration-repository-git/api-management-delegation-settings.png
[api-management-git-icon-enable]: ./media/api-management-configuration-repository-git/api-management-git-icon-enable.png




