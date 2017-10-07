---
title: "aaaAdd bir SSL sertifikası tooyour Azure App Service uygulaması | Microsoft Docs"
description: "Nasıl tooadd bir SSL sertifikası tooyour App Service uygulaması hakkında bilgi edinin."
services: app-service
documentationcenter: .net
author: ahmedelnably
manager: stefsch
editor: cephalin
tags: buy-ssl-certificates
ms.assetid: cdb9719a-c8eb-47e5-817f-e15eaea1f5f8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/19/2016
ms.author: apurvajo
ms.openlocfilehash: f4652794ba745790a073264f6a102c64c73e8db0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="buy-and-configure-an-ssl-certificate-for-your-azure-app-service"></a>Azure App Service için SSL Sertifikası Satın Alma ve Yapılandırma

Bu öğreticide, web uygulamanız için bir SSL sertifikası satın alarak güvenliğini,  **[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)**, güvenli bir şekilde de depolamak [Azure anahtar kasası](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis)ve bunu ilişkilendirme özel bir etki alanı ile.

## <a name="step-1---log-in-tooazure"></a>1. adım - tooAzure günlüğünde

İçinde toohello http://portal.azure.com Azure portalında oturum açın

## <a name="step-2---place-an-ssl-certificate-order"></a>2. adım - bir SSL sertifikası sipariş verin

Yeni bir oluşturarak bir SSL sertifikası sipariş yerleştirebilirsiniz [uygulama hizmet sertifikası](https://portal.azure.com/#create/Microsoft.SSL) hello içinde **Azure portal**.

![Sertifika oluşturma](./media/app-service-web-purchase-ssl-web-site/createssl.png)

Kolay bir girin **adı** hello girin ve için SSL sertifika **etki alanı adı**

> [!NOTE]
> Bu, hello en kritik bölümleri hello satın alma işlemi biridir. Bu sertifika ile tooprotect istediğiniz ana bilgisayar adı (özel etki alanı) düzeltmek emin tooenter olun. **SAĞLAMADIĞI** WWW ana bilgisayar adıyla hello ekleyin. 
>

Seçin, **abonelik**, **kaynak grubu**, ve **sertifika SKU**

> [!WARNING]
> Uygulama Hizmeti sertifikaları yalnızca kullanılabilir hello içindeki diğer uygulama hizmetler tarafından aynı abonelik.  
>

## <a name="step-3---store-hello-certificate-in-azure-key-vault"></a>3. adım - Azure anahtar kasası hello sertifika deposu

> [!NOTE]
> [Anahtar kasası](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) şifreleme anahtarları ve gizli anahtarları bulut uygulamalar ve hizmetler tarafından kullanılan korumaya yardımcı olan bir Azure hizmetidir.
>

Merhaba SSL sertifikası satın alma işlemi tamamlandıktan sonra tooopen gerekir [uygulama hizmeti sertifikaları](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.CertificateRegistration%2FcertificateOrders) kaynak dikey.

![içinde KV hazır toostore görüntüsü Ekle](./media/app-service-web-purchase-ssl-web-site/ReadyKV.png)

Sertifika durumu olduğunu fark edeceksiniz **"Bekleyen verme"** birkaç adım olduğundan bu sertifikayı kullanarak başlamadan önce toocomplete gerekir.

' I tıklatın **sertifika Yapılandırması** sertifika özellikleri dikey penceresinde ve tıklayarak içinde **adım 1: depolama** toostore Azure anahtar Kasası'nda bu sertifika.

Gelen **anahtar kasası durumu** dikey penceresinde tıklatın **anahtar kasası deposu** toochoose var olan bir anahtar kasası toostore bu sertifikayı **veya oluşturma yeni anahtar kasası** toocreate yeni bir anahtar kasası aynı abonelik ve kaynak grubu içinde.

> [!NOTE]
> Azure anahtar kasası bu sertifikayı depolamak için en düşük ücretler sahiptir.
> Daha fazla bilgi için bkz:  **[Azure anahtar kasası fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/key-vault/)**.
>

Bu sertifikada hello anahtar kasası depo toostore seçtikten sonra hello **deposu** seçeneğini başarı göster.

![KV deposu başarılı bir görüntüsünü Ekle](./media/app-service-web-purchase-ssl-web-site/KVStoreSuccess.png)

## <a name="step-4---verify-hello-domain-ownership"></a>Adım 4 - hello etki alanı sahipliğini doğrulayın

> [!NOTE]
> Uygulama Hizmeti sertifikaları tarafından desteklenen etki alanı doğrulama üç tür vardır: etki alanı, posta, el ile doğrulama. Bunlar daha ayrıntılı olarak hello açıklanacak [bölüm Gelişmiş](#advanced).

Gelen aynı hello **sertifika Yapılandırması** dikey adım 3'te kullanılan, tıklatın **2. adım: doğrulayın**.

**Etki alanı doğrulama** bu hello en kolay bir işlemdir **yalnızca IF** elinizde  **[özel etki alanınızı Azure App hizmetinden satın.](custom-dns-web-site-buydomains-web-app.md)**
Tıklayın **doğrula** toocomplete bu adımı düğmesine tıklayın.

![etki alanı doğrulama görüntüsü Ekle](./media/app-service-web-purchase-ssl-web-site/DomainVerificationRequired.png)

' I tıklattıktan sonra **doğrulayın**, hello kullanın **yenileme** hello kadar düğme **doğrulayın** seçeneğini başarı göster.

![INSERT görüntüsü KV başarılı doğrulayın](./media/app-service-web-purchase-ssl-web-site/KVVerifySuccess.png)

## <a name="step-5---assign-certificate-tooapp-service-app"></a>5. adım - sertifika tooApp Service uygulaması atayın

> [!NOTE]
> Bu bölümde Hello adımları gerçekleştirmeden önce bir özel etki alanı adı uygulamanızla ilişkili sahip olmalıdır. Daha fazla bilgi için bkz:  **[bir web uygulaması için bir özel etki alanı adı yapılandırma.](app-service-web-tutorial-custom-domain.md)**
>

Merhaba,  **[Azure portal](https://portal.azure.com/)**, hello tıklatın **uygulama hizmeti** hello sayfasının hello soldaki seçeneği.

Merhaba adını tıklatın, uygulama toowhich bu sertifikayı tooassign istiyor.

Merhaba, **ayarları**, tıklatın **SSL sertifikalarını**.

Tıklatın **alma uygulaması hizmet sertifikası** ve yalnızca satın select hello sertifikası.

![Sertifika İçeri Aktar görüntüsü Ekle](./media/app-service-web-purchase-ssl-web-site/ImportCertificate.png)

Merhaba, **ssl bağlamaları** tıklatın bölümünde **bağlamaları Ekle**, SSL ile Merhaba bırakmalar tooselect hello etki alanı adı toosecure kullanın ve sertifika toouse hello. Ayrıca seçebilirsiniz olup olmadığını toouse  **[sunucu adı göstergesi (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)**  veya IP tabanlı SSL.

![SSL bağlamaları görüntüsü Ekle](./media/app-service-web-purchase-ssl-web-site/SSLBindings.png)

Tıklatın **bağlaması Ekle** toosave hello değişiklikleri ve SSL'yi etkinleştirin.

> [!NOTE]
> Seçtiyseniz **IP tabanlı SSL** ve özel etki alanınızı bir A kaydı kullanılarak yapılandırılır, hello aşağıdaki ek adımları gerçekleştirmeniz gerekir. Bunlar daha ayrıntılı olarak hello açıklanacak [bölüm Gelişmiş](#Advanced).

Bu noktada, mümkün toovisit uygulamasını kullanarak olmalıdır `HTTPS://` yerine `HTTP://` sertifika hello tooverify doğru şekilde yapılandırıldı.

<!--![insert image of https](./media/app-service-web-purchase-ssl-web-site/Https.png)-->

## <a name="step-6---management-tasks"></a>Adım 6 - yönetim görevleri

### <a name="azure-cli"></a>Azure CLI

[!code-azurecli[main](../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate to a web app")] 

### <a name="powershell"></a>PowerShell

[!code-powershell[main](../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Bind a custom SSL certificate to a web app")]

## <a name="advanced"></a>Gelişmiş

### <a name="verifying-domain-ownership"></a>Etki alanı sahipliğini doğrulama

Uygulama Hizmeti sertifikaları tarafından desteklenen etki alanı doğrulama daha fazla iki tür vardır: posta ve el ile doğrulama.

#### <a name="mail-verification"></a>Posta doğrulama

E-posta adresleri bu özel etki alanı ile ilişkili toohello doğrulama e-posta zaten gönderildi.
toocomplete hello e-posta doğrulama adımı, hello e-posta açın ve hello doğrulama bağlantısını tıklatın.

![e-posta doğrulama görüntüsü Ekle](./media/app-service-web-purchase-ssl-web-site/KVVerifyEmailSuccess.png)

Tooresend hello doğrulama e-posta gerekiyorsa, hello tıklatın **yeniden Gönder'e-posta** düğmesi.

#### <a name="manual-verification"></a>El ile doğrulama

> [!IMPORTANT]
> HTML Web sayfası Doğrulama (yalnızca standart sertifika SKU çalışır)
>

1. Adlı bir HTML dosyası oluşturmak **"starfield.html"**

1. Bu dosyanın hello tam etki alanı doğrulama belirteci hello adını içerik olması gerekir. (Etki alanı doğrulama durumu dikey penceresinde hello hello belirteci kopyalayabilirsiniz)

1. Merhaba kökündeki etki alanınızı barındırmaya hello web sunucusunun bu dosyayı karşıya yükleme`/.well-known/pki-validation/starfield.html`

1. Tıklatın **yenileme** doğrulama tamamlandıktan sonra tooupdate hello sertifika durumu. Doğrulama toocomplete için birkaç dakika sürebilir.

> [!TIP]
> Terminal kullanarak bir doğrulama `curl -G http://<domain>/.well-known/pki-validation/starfield.html` hello yanıt hello içermelidir `<verification-token>`.

#### <a name="dns-txt-record-verification"></a>DNS TXT kaydını doğrulama

1. DNS Yöneticisi'ni kullanarak, hello üzerinde bir TXT kaydını oluşturmak `@` değer eşit toohello etki alanı doğrulama belirteci ile alt etki alanı.
1. Tıklatın **"Yenile"** tooupdate hello doğrulama tamamlandıktan sonra sertifika durumu.

> [!TIP]
> Bilgisayarda toocreate TXT kaydı gerektiren `@.<domain>` değerle `<verification-token>`.

### <a name="assign-certificate-tooapp-service-app"></a>Sertifika tooApp Service uygulaması atayın

Seçtiyseniz **IP tabanlı SSL** ve özel etki alanınızı bir A kaydı kullanılarak yapılandırılır, hello aşağıdaki ek adımları gerçekleştirmeniz gerekir:

Yapılandırdıktan sonra bir IP temelli SSL bağlaması, ayrılmış bir IP adresi tooyour uygulama atanır. Bu IP adresi üzerinde hello bulabilirsiniz **özel etki alanı** hello üzerinde doğru uygulamanızın ayarlar altında sayfa **ana bilgisayar adları** bölümü. Olarak listelenen **dış IP adresi**

![IP SSL görüntüsü Ekle](./media/app-service-web-purchase-ssl-web-site/virtual-ip-address.png)

Bu IP adresi hello sanal IP adresi tooconfigure hello A kaydı etki alanınız için daha önce kullanılan farklı olduğunu unutmayın. Yapılandırdıysanız SNI tabanlı SSL veya olmayan toouse toouse SSL yapılandırılmış, bu giriş için bir adresinin.

Etki alanı adı kayıt şirketiniz tarafından sağlanan hello Araçları'nı kullanarak hello hello önceki adımdaki, özel etki alanı adı toopoint toohello IP adresi için bir kayıt değiştirin.

## <a name="rekey-and-sync-hello-certificate"></a>Yeniden anahtarlama ve eşitleme hello sertifika

Sertifikanızı erişiminizi tooRekey gerekirse seçin **anahtar yenileme ve eşitleme** gelen seçeneği **sertifika özellikleri** dikey.

Tıklatın **anahtar yenileme** düğmesini tooinitiate hello işlemi. Bu işlem, 1-10 dakika toocomplete alabilir.

![anahtar yenileme SSL görüntüsü Ekle](./media/app-service-web-purchase-ssl-web-site/Rekey.png)

Sertifikanızı yeniden anahtarlama hello sertifika hello sertifika yetkilisi tarafından verilen yeni bir sertifika ile yapar.

## <a name="next-steps"></a>Sonraki Adımlar

* [Bir içerik teslim ağı Ekle](app-service-web-tutorial-content-delivery-network.md)