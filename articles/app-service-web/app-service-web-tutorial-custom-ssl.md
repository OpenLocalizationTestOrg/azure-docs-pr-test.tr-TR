---
title: "aaaBind var olan bir özel SSL sertifika tooAzure Web Apps | Microsoft Docs"
description: "Özel SSL sertifika tooyour web uygulaması, mobil uygulama arka ucu veya Azure App Service'teki API uygulamasına tootoobind öğrenin."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 5d5bf588-b0bb-4c6d-8840-1b609cfb5750
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 06/23/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 3503ba9f96c8ea8d18451e8bf9a9b441797ef44d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="bind-an-existing-custom-ssl-certificate-tooazure-web-apps"></a>Bir var olan özel SSL sertifika tooAzure Web Apps bağlama

Azure Web Apps düzeyde ölçeklenebilir, otomatik olarak düzeltme eki uygulama web barındırma hizmeti sağlar. Bu öğretici nasıl toobind özel bir SSL sertifikası güvenilir bir sertifika yetkilisinden çok satın aldığınız gösterir[Azure Web Apps](app-service-web-overview.md). İşiniz bittiğinde, web uygulamanızı mümkün tooaccess olacak özel bir DNS etki alanının hello HTTPS uç noktası.

![Özel SSL sertifikası ile Web uygulaması](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

Bu öğreticide şunların nasıl yapıldığını öğreneceksiniz:

> [!div class="checklist"]
> * Uygulamanızın fiyatlandırma katmanı yükseltme
> * Özel bir SSL sertifikası tooApp hizmet bağlama
> * Uygulamanız için HTTPS zorla
> * SSL sertifikası bağlaması kodlarıyla otomatikleştirme

> [!NOTE]
> Özel bir SSL sertifikası tooget gerekiyorsa, hello Azure portal birinde doğrudan almak ve tooyour web uygulaması bağlayın. Merhaba izleyin [uygulama hizmeti sertifikaları Öğreticisi](web-sites-purchase-ssl-web-site.md).

## <a name="prerequisites"></a>Ön koşullar

toocomplete Bu öğretici:

- [Bir App Service uygulaması oluşturma](/azure/app-service/)
- [Bir özel DNS adı tooyour web uygulaması eşleme](app-service-web-tutorial-custom-domain.md)
- Güvenilen sertifika yetkilisinden bir SSL sertifikası alın

<a name="requirements"></a>

### <a name="requirements-for-your-ssl-certificate"></a>SSL sertifika için gereksinimler

toouse App Service'te bir sertifika, hello sertifika tüm hello aşağıdaki gereksinimleri karşılaması gerekir:

* Bir güvenilir sertifika yetkilisi tarafından imzalanmış
* Parola korumalı bir PFX dosyası olarak dışa
* Özel anahtarı en az 2048 bit uzun içerir
* Merhaba Sertifika zincirindeki tüm ara sertifikaların içerir

> [!NOTE]
> **Eliptik Eğri Şifrelemesi (ECC) sertifikaları** App Service ile çalışabilir, ancak bu makalenin ele alınmamaktadır. Sertifika yetkilisi ile Merhaba tam adımlar toocreate ECC sertifikaları üzerinde çalışır.

## <a name="prepare-your-web-app"></a>Web uygulamanızı hazırlama

toobind özel bir SSL sertifikası tooyour web uygulaması, sizin [uygulama hizmeti planı](https://azure.microsoft.com/pricing/details/app-service/) hello olmalıdır **temel**, **standart**, veya **Premium** katmanı. Bu adımda, fiyatlandırma katmanı, web uygulamanızın hello desteklendiğinden emin olun.

### <a name="log-in-tooazure"></a>İçinde tooAzure oturum

Açık hello [Azure portal](https://portal.azure.com).

### <a name="navigate-tooyour-web-app"></a>Tooyour web uygulamasına gidin

Merhaba sol menüden **uygulama hizmetleri**ve ardından web uygulamanızı hello adına tıklayın.

![Web uygulaması seçin](./media/app-service-web-tutorial-custom-ssl/select-app.png)

Web uygulamanızın Yönetimi sayfasında hello indiniz.  

### <a name="check-hello-pricing-tier"></a>Fiyatlandırma katmanı hello denetleyin

Merhaba sol gezinti web uygulaması sayfanızın bölmesinde toohello kaydırma **ayarları** bölümünde ve seçin **(uygulama hizmeti planı) ölçeklendirme**.

![Büyütme menüsü](./media/app-service-web-tutorial-custom-ssl/scale-up-menu.png)

Web uygulamanızı hello olmadığından emin toomake denetleyin **serbest** veya **paylaşılan** katmanı. Web uygulamanızın geçerli katmanı Koyu mavi bir kutu vurgulanır.

![Fiyatlandırma katmanı denetleyin](./media/app-service-web-tutorial-custom-ssl/check-pricing-tier.png)

Özel SSL hello desteklenmiyor **serbest** veya **paylaşılan** katmanı. Yukarı tooscale gerekiyorsa, hello sonraki bölümde hello adımları izleyin. Aksi takdirde hello kapatmak **fiyatlandırma katmanınızı seçin** sayfasında ve çok atla[karşıya yükleme ve SSL sertifikanız bağlama](#upload).

### <a name="scale-up-your-app-service-plan"></a>Uygulama hizmeti planınızı ölçeklendirin

Merhaba birini **temel**, **standart**, veya **Premium** katmanları.

**Seç**'e tıklayın.

![Fiyatlandırma katmanı seçin](./media/app-service-web-tutorial-custom-ssl/choose-pricing-tier.png)

Bildirim aşağıdaki hello gördüğünüzde, hello ölçeklendirme işlemi tamamlanır.

![Bildirimi ölçeklendirme](./media/app-service-web-tutorial-custom-ssl/scale-notification.png)

<a name="upload"></a>

## <a name="bind-your-ssl-certificate"></a>SSL sertifikası bağlama

SSL sertifikası tooyour web uygulamanız hazır tooupload şunlardır.

### <a name="merge-intermediate-certificates"></a>Ara Sertifika birleştirme

Sertifika yetkilinize hello sertifika zincirinde birden çok sertifika veriyorsa, sırayla toomerge hello sertifikalar gerektirir. 

toodo bu açık her sertifika, bir metin düzenleyicisinde aldı. 

Adlı hello birleştirilmiş sertifikası için bir dosya oluşturmak _mergedcertificate.crt_. Bir metin düzenleyicisinde her sertifika Merhaba içeriğine bu dosyaya kopyalayın. sertifikalarınızı Hello sırasını hello şablon aşağıdaki gibi görünmelidir:

```
-----BEGIN CERTIFICATE-----
<your Base64 encoded SSL certificate>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded intermediate certificate 1>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded intermediate certificate 2>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded root certificate>
-----END CERTIFICATE-----
```

### <a name="export-certificate-toopfx"></a>Sertifika tooPFX dışarı aktarma

Sertifika isteğinizi ile oluşturulan hello özel anahtar ile birleştirilmiş SSL sertifikanızı verin.

Ardından OpenSSL kullanarak sertifika isteğinizi oluşturursa, özel bir anahtar dosyası oluşturdunuz. tooexport hello aşağıdaki komutu çalıştırın, sertifika tooPFX. Merhaba yer tutucuları değiştirmek  _&lt;özel anahtar dosyası >_ ve  _&lt;birleştirilmiş-sertifika-dosyası >_.

```
openssl pkcs12 -export -out myserver.pfx -inkey <private-key-file> -in <merged-certificate-file>  
```

İstendiğinde, bir dışarı aktarma parolası tanımlayın. Bu parola, SSL sertifikası tooApp hizmeti daha sonra karşıya yüklenirken kullanacaksınız.

IIS kullandıysanız veya _Certreq.exe_ toogenerate sertifika isteği, yükleme hello sertifika tooyour yerel makine ve ardından [hello sertifika tooPFX verme](https://technet.microsoft.com/library/cc754329(v=ws.11).aspx).

### <a name="upload-your-ssl-certificate"></a>SSL sertifikasını karşıya yükle

tooupload SSL sertifikanızı tıklatın **SSL sertifikalarını** sol gezinti web uygulamanızın hello içinde.

Tıklatın **karşıya sertifika**.

İçinde **PFX sertifika dosyanızı**, PFX dosyasını seçin. İçinde **sertifika parolası**, hello PFX dosyası dışarı aktardığınızda, oluşturduğunuz hello parolayı girin.

**Karşıya Yükle**'ye tıklayın.

![Sertifikayı karşıya yükleme](./media/app-service-web-tutorial-custom-ssl/upload-certificate.png)

Uygulama hizmeti sertifikanızı karşıya yükleme tamamlandığında, hello göründüğü **SSL sertifikalarını** sayfası.

![Karşıya sertifika](./media/app-service-web-tutorial-custom-ssl/certificate-uploaded.png)

### <a name="bind-your-ssl-certificate"></a>SSL sertifikası bağlama

Merhaba, **SSL bağlamaları** 'yi tıklatın **eklemek bağlama**.

Merhaba, **SSL bağlaması Ekle** sayfasında, hello bırakmalar tooselect hello etki alanı adı toosecure ve hello sertifika toouse kullanın.

> [!NOTE]
> Sertifikanız karşıya yüklediğiniz halde hello hello etki alanı adları göremiyorsanız **ana bilgisayar adı** açılan listesinde, hello tarayıcı sayfayı yenilemeyi deneyin.
>
>

İçinde **SSL türü**seçin olup olmadığını toouse  **[sunucu adı göstergesi (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)**  ya da IP tabanlı SSL.

- **SNI tabanlı SSL** -birden çok SNI tabanlı SSL bağlamaları eklenebilir. Bu seçenek birden çok SSL sertifikalarını toosecure hello üzerinde birden çok etki alanı sağlar. aynı IP adresi. (Internet Explorer, Chrome, Firefox ve Opera dahil) çoğu modern tarayıcılar SNI destekler (daha kapsamlı tarayıcı destek bilgilerini bulmak [sunucu adı göstergesi](http://wikipedia.org/wiki/Server_Name_Indication)).
- **IP tabanlı SSL** -yalnızca bir IP temelli SSL bağlama eklenebilir. Bu seçenek yalnızca bir SSL sertifikası toosecure adanmış bir ortak IP adresi sağlar. toosecure birden çok etki alanı, bunları tüm kullanarak güvenli hale getirmenize gerekir hello aynı SSL sertifikası. SSL bağlaması için hello geleneksel seçenek budur.

Tıklatın **bağlama eklemek**.

![SSL sertifikası bağlama](./media/app-service-web-tutorial-custom-ssl/bind-certificate.png)

Uygulama hizmeti sertifikanızı karşıya yükleme tamamlandığında, hello göründüğü **SSL bağlamaları** bölümler.

![Sertifika ilişkili tooweb uygulama](./media/app-service-web-tutorial-custom-ssl/certificate-bound.png)

## <a name="remap-a-record-for-ip-ssl"></a>IP SSL için bir kayıt yeniden eşleme

Web uygulamanızda IP tabanlı SSL kullanmıyorsanız, çok atla[Test HTTPS özel etki alanınız için](#test).

Varsayılan olarak, web uygulamanızı paylaşılan bir ortak IP adresini kullanır. IP tabanlı SSL sertifikasıyla bağladığınızda, App Service web uygulamanız için yeni, ayrılmış bir IP adresi oluşturur.

Bir A kaydı tooyour web uygulaması eşledikten ise, etki alanı kayıt defteri bu yeni, özel IP adresi ile güncelleştirin.

Web uygulamanızın **özel etki alanı** sayfa hello yeni, özel IP adresi ile güncelleştirilir. [Bu IP adresi Kopyala](app-service-web-tutorial-custom-domain.md#info), ardından [eşleme hello kayıt](app-service-web-tutorial-custom-domain.md#map-an-a-record) toothis yeni bir IP adresi.

<a name="test"></a>

## <a name="test-https"></a>Test HTTPS

Tüm toodo şimdi ayrıldı toomake HTTPS için özel etki alanınızı çalıştığından emin olan. Çok çeşitli tarayıcılarda Gözat`https://<your.custom.domain>` web uygulamanıza hizmet toosee.

![Portal Gezinti tooAzure uygulama](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

> [!NOTE]
> Web uygulamanız varsa doğrulama hatalarını sertifika, büyük olasılıkla otomatik olarak imzalanan bir sertifika kullanıyorsanız.
>
> Merhaba durum bu değilse, sertifika toohello PFX dosyanızı dışa aktardığınızda Ara sertifikalara sol.

<a name="bkmk_enforce"></a>

## <a name="enforce-https"></a>HTTPS zorlama

Uygulama hizmeti yapar *değil* herkes, HTTP kullanarak web uygulamanızı erişebilmesi için HTTPS zorla. web uygulamanız için HTTPS tooenforce tanımlayan bir yeniden yazma kuralı hello _web.config_ web uygulamanız için dosya. Uygulama hizmeti, web uygulamanızın hello dili çerçevesini bağımsız olarak bu dosyayı kullanır.

> [!NOTE]
> Dile özgü yeniden yönlendirme istekleri yoktur. ASP.NET MVC hello kullanabileceğiniz [RequireHttps](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filtre hello yeniden yazma kuralı yerine _web.config_.

.NET Geliştirici değilseniz, bu dosya ile görece tanıyor olmalıdır. Çözümünüzü hello kök dizininde değil.

Alternatif olarak, PHP, Node.js, Python veya Java ile ortaya çıkarsa, size bu dosyayı sizin adınıza App Service içinde oluşturulan bir fırsat yok.

Merhaba yönergeleri izleyerek tooyour web uygulamanızın FTP uç noktası bağlanın [, uygulama tooAzure uygulama FTP/S kullanarak hizmeti dağıtmak](app-service-deploy-ftp.md).

Bu dosyanın içinde bulunması _/home/site/wwwroot_. Değilse, oluşturmak bir _web.config_ XML aşağıdaki hello ile bu klasörde dosya:

```xml   
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <system.webServer>
    <rewrite>
      <rules>
        <!-- BEGIN rule ELEMENT FOR HTTPS REDIRECT -->
        <rule name="Force HTTPS" enabled="true">
          <match url="(.*)" ignoreCase="false" />
          <conditions>
            <add input="{HTTPS}" pattern="off" />
          </conditions>
          <action type="Redirect" url="https://{HTTP_HOST}/{R:1}" appendQueryString="true" redirectType="Permanent" />
        </rule>
        <!-- END rule ELEMENT FOR HTTPS REDIRECT -->
      </rules>
    </rewrite>
  </system.webServer>
</configuration>
```

Mevcut bir _web.config_ dosya, hello bütün kopyası `<rule>` öğesine, _web.config_'s `configuration/system.webServer/rewrite/rules` öğesi. Varsa diğer `<rule>` öğelerinde, _web.config_, kopyalanan yer hello `<rule>` öğesinden hello diğer önce `<rule>` öğeleri.

Merhaba kullanıcı bir HTTP isteği tooyour web uygulaması yaptığında bu kural bir HTTP 301 (kalıcı yeniden yönlendirme) toohello HTTPS protokolünü döndürür. Örneğin, gelen yönlendirir `http://contoso.com` çok`https://contoso.com`.

Merhaba hello IIS URL yeniden yazma modülü hakkında daha fazla bilgi için bkz: [URL yeniden yazma](http://www.iis.net/downloads/microsoft/url-rewrite) belgeleri.

## <a name="enforce-https-for-web-apps-on-linux"></a>Linux üzerinde Web uygulamaları için HTTPS zorla

Uygulama hizmeti Linux'ta mu *değil* herkes, HTTP kullanarak web uygulamanızı erişebilmesi için HTTPS zorla. web uygulamanız için HTTPS tooenforce tanımlayan bir yeniden yazma kuralı hello _.htaccess_ web uygulamanız için dosya. 

Merhaba yönergeleri izleyerek tooyour web uygulamanızın FTP uç noktası bağlanın [, uygulama tooAzure uygulama FTP/S kullanarak hizmeti dağıtmak](app-service-deploy-ftp.md).

İçinde _/home/site/wwwroot_, oluşturma bir _.htaccess_ koddan hello dosyasıyla:

```
RewriteEngine On
RewriteCond %{HTTP:X-ARR-SSL} ^$
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```

Merhaba kullanıcı bir HTTP isteği tooyour web uygulaması yaptığında bu kural bir HTTP 301 (kalıcı yeniden yönlendirme) toohello HTTPS protokolünü döndürür. Örneğin, gelen yönlendirir `http://contoso.com` çok`https://contoso.com`.

## <a name="automate-with-scripts"></a>Komut dosyalarıyla otomatikleştirme

Hello kullanarak komut dosyaları ile web uygulamanız için SSL bağlamaları otomatikleştirebilirsiniz [Azure CLI](/cli/azure/install-azure-cli) veya [Azure PowerShell](/powershell/azure/overview).

### <a name="azure-cli"></a>Azure CLI

komutu aşağıdaki hello hello parmak izi alır ve bir dışarı aktarılan PFX dosyasını yükler.

```bash
thumbprint=$(az appservice web config ssl upload \
    --name <app_name> \
    --resource-group <resource_group_name> \
    --certificate-file <path_to_PFX_file> \
    --certificate-password <PFX_password> \
    --query thumbprint \
    --output tsv)
```

Merhaba aşağıdaki komut hello parmak hello önceki komutundan kullanarak bir SNI tabanlı SSL bağlaması ekler.

```bash
az appservice web config ssl bind \
    --name <app_name> \
    --resource-group <resource_group_name>
    --certificate-thumbprint $thumbprint \
    --ssl-type SNI \
```

### <a name="azure-powershell"></a>Azure PowerShell

Merhaba aşağıdaki komutu bir dışarı aktarılan PFX dosyasını yükler ve SNI tabanlı SSL bağlaması ekler.

```PowerShell
New-AzureRmWebAppSSLBinding `
    -WebAppName <app_name> `
    -ResourceGroupName <resource_group_name> `
    -Name <dns_name> `
    -CertificateFilePath <path_to_PFX_file> `
    -CertificatePassword <PFX_password> `
    -SslState SniEnabled
```

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, şunların nasıl yapıldığını öğrendiniz:

> [!div class="checklist"]
> * Uygulamanızın fiyatlandırma katmanı yükseltme
> * Özel bir SSL sertifikası tooApp hizmet bağlama
> * Uygulamanız için HTTPS zorla
> * SSL sertifikası bağlaması kodlarıyla otomatikleştirme

Toohello sonraki öğretici toolearn nasıl ilerlemek toouse Azure içerik teslim ağı.

> [!div class="nextstepaction"]
> [İçerik teslim ağı (CDN) tooan Azure uygulama hizmeti Ekle](app-service-web-tutorial-content-delivery-network.md)
