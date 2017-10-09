---
title: "aaaAzure Depolama Gezgini sorun giderme kılavuzu | Microsoft Docs"
description: "Azure hello iki hata ayıklama özelliğine genel bakış"
services: virtual-machines
documentationcenter: 
author: Deland-Han
manager: cshepard
editor: 
ms.assetid: 
ms.service: virtual-machines
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: delhan
ms.openlocfilehash: 21705629500359222bc566c599f0864ad50036ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-explorer-troubleshooting-guide"></a>Azure Storage Gezgini sorun giderme kılavuzu

## <a name="introduction"></a>Giriş

Microsoft Azure Storage Gezgini (Önizleme), Windows, macOS ve Linux Azure Storage verilerle tooeasily çalışma sağlayan tek başına bir uygulamadır. Merhaba uygulaması Azure, Sovereign Bulutlar ve Azure yığın üzerinde barındırılan toStorage hesapları bağlanabilirler.

Bu kılavuz, depolama Gezgini'nde görülen yaygın sorunlar için çözümleri özetler.

## <a name="sign-in-issues"></a>Oturum açma sorunları

Yalnızca Azure Active Directory (AAD) hesapları desteklenir. Bir ADFS hesabını kullanıyorsanız, bu Explorer işe yaramayacaktır tooStorage içinde imzalama beklenen. Devam etmeden önce uygulamanızı yeniden başlatmayı deneyin ve hello sorunların giderilip giderilemeyeceğini bakın.

### <a name="error-self-signed-certificate-in-certificate-chain"></a>Hatası: Sertifika zincirindeki otomatik olarak imzalanan sertifika

Neden bu hatayla karşılaşabilirsiniz ve hello en yaygın iki sebepleri şunlardır birkaç nedeni vardır:

1. Merhaba uygulaması "(örneğin, şirket sunucunuzun) bir sunucu HTTPS trafiği kesintiye uğratan, şifre çözme ve kendinden imzalı bir sertifika kullanarak şifreleme anlamı saydam bir proxy", bağlı.

2. Bir uygulama otomatik olarak imzalanan bir SSL sertifikası aldığınız hello HTTPS iletilere injecting virüsten koruma yazılımı gibi çalışıyor.

Depolama Gezgini hello sorunları karşılaştığında, artık alınan hello HTTPS ileti oynanmadığını bilebilirsiniz. Merhaba otomatik olarak imzalanan sertifika bir kopyasına sahipseniz, bu güven Depolama Gezgini izin verebilirsiniz. Merhaba sertifika injecting emin değilseniz, bu adımları toofind izleyin:

1. Açık SSL yükleyin

    - [Windows](https://slproweb.com/products/Win32OpenSSL.html) (Merhaba hafif sürümlerinin herhangi birinin yeterli olmalıdır)

    - Mac ve Linux: işletim sisteminizle eklenmelidir

2. Açık SSL çalıştırın

    - Windows: hello yükleme dizinini açın, **/bin/**, çift tıklayın ve ardından **openssl.exe**.
    - Mac ve Linux: çalıştırmak **openssl** bir terminal gelen.

3. S_client - showcerts yürütme-microsoft.com:443 Bağlan

4. Otomatik olarak imzalanan sertifikalar arayın. Kendinden imzalı olduğu emin değilseniz, herhangi bir yere hello konu ("%s") arayın ve veren ("i:") aynı hello şunlardır.

5. Herhangi bir otomatik olarak imzalanan sertifika bulduğunuzda, her biri için kopyalayıp her şeyi ilk ve son dahil olmak üzere **---başlangıç sertifika---** çok**---son SERTİFİKAYI---** tooa yeni .cer dosyası.

6. Depolama Gezgini'ni açın, **Düzenle** > **SSL sertifikalarını** > **alma sertifikaları**ve ardından kullanım hello dosya Seçici toofind, seçin ve oluşturduğunuz hello .cer dosyaları açın.

Merhaba yukarıdaki adımları kullanarak herhangi bir otomatik olarak imzalanan sertifika bulamazsanız, daha fazla yardım için hello geri bildirim araçla bize başvurun.

### <a name="unable-tooretrieve-subscriptions"></a>%S tooretrieve abonelikleri

Bu adımları tootroubleshoot aboneliklerinizi çalıştırdıktan sonra başarıyla oturum açamıyor tooretrieve varsa, bu sorunu izleyin:

- Azure portal hello imzalayarak hesabınıza erişim toohello abonelikleri olduğunu doğrulayın.

- Merhaba doğru ortam (Azure, Azure Çin, Azure Almanya, Azure ABD devlet kurumları veya özel ortam/Azure yığın) kullanarak imzaladığınız emin olun.

- Bir proxy'nin arkasında varsa, hello Depolama Gezgini proxy düzgün şekilde yapılandırdığınızdan emin olun.

- Kaldırarak ve yeniden ekleniyor hello hesap deneyin.

- Aşağıdaki dosyaları kök dizini (diğer bir deyişle, C:\Users\ContosoUser) ve ardından hello hesabı yeniden ekleyerek hello silmeyi deneyin:

    - .adalcache

    - .devaccounts

    - .extaccounts

- İzleme hello geliştirici araçları konsolunu (F12 tuşuna basarak tarafından) ne zaman, imzaladığınız herhangi bir hata iletisi:

![Geliştirici Araçları](./media/storage-explorer-troubleshooting/4022501_en_2.png)

### <a name="unable-toosee-hello-authentication-page"></a>%S toosee hello kimlik doğrulaması sayfası

Bu adımları tootroubleshoot oluşturulamıyor toosee hello kimlik doğrulaması sayfa varsa, bu sorunu izleyin:

- Bağlantınızı Hello hızına bağlı olarak, bu hello oturum açma sayfası tooload için sürebilir, hello kimlik doğrulama iletişim kutusunu kapatmadan önce en az bir dakika bekleyin.

- Bir proxy'nin arkasında varsa, hello Depolama Gezgini proxy düzgün şekilde yapılandırdığınızdan emin olun.

- Merhaba F12 tuşuna basarak hello Geliştirici konsol görünümü. Hello Geliştirici konsolundan Hello yanıtlarını izleyin ve tüm ipucu için neden Bul olup olmadığını görmek kimlik doğrulaması çalışmıyor.

### <a name="cannot-remove-account"></a>Hesabını kaldıramaz

Yüklenemiyor tooremove hesabınız yoksa veya hello yeniden kimlik doğrula bağlantı herhangi bir şey yapmanız durumunda, bu adımları tootroubleshoot bu sorunu izleyin:

- Kök dizininden aşağıdaki dosyaları ve hello hesabı yeniden ekleniyor hello silmeyi deneyin:

    - .adalcache

    - .devaccounts

    - .extaccounts

- Depolama kaynaklarını tooremove SAS bağlı istiyorsanız, aşağıdaki dosyaları hello silin:

    - Windows için %appdata%/StorageExplorer klasör

    - /Users/ < adiniz >/kitaplık/uygulaması destek/StorageExplorer Mac için

    - Linux için ~/.config/StorageExplorer

> [!NOTE]
>  Bu dosyaları silerseniz, tüm kimlik bilgilerinizi tooreenter gerekir.

## <a name="proxy-issues"></a>Proxy sorunları

İlk olarak, girdiğiniz bilgileri aşağıdaki o hello tüm doğru olduğundan emin olun:

- Merhaba proxy URL'si ve bağlantı noktası numarası

- Kullanıcı adı ve parola hello proxy tarafından gerekirse

### <a name="common-solutions"></a>Yaygın çözümleri

Sorunları yaşamaya devam ediyorsanız, bu adımları tootroubleshoot izleyin bunları:

- Toohello Internet proxy kullanmadan bağlanabiliyorsa Depolama Gezgini proxy ayarlarının etkin çalıştığını doğrulayın. Merhaba Durum buysa, proxy ayarlarınızı ile ilgili bir sorun olabilir. Proxy yönetici tooidentify hello sorunlarınızı ile çalışır.

- Merhaba proxy sunucusu kullanan diğer uygulamalar beklendiği gibi çalıştığını doğrulayın.

- Toohello Microsoft Azure portal, web tarayıcısı kullanarak bağlanabildiğini doğrulayın

- Hizmet uç noktalarından yanıtları alabilir doğrulayın. Uç nokta URL'leri birini tarayıcınıza girin. Bağlanabiliyorsanız, bir InvalidQueryParameterValue veya benzeri bir XML yanıt almanız gerekir.

- Başka biri de Depolama Gezgini proxy sunucunuz ile kullanıyorsa, bunlar bağlanabildiğinizi doğrulayın. Bağlanabiliyorsanız, proxy sunucu yöneticinizle toocontact olabilir.

### <a name="tools-for-diagnosing-issues"></a>Sorunları tanılamak için Araçlar

Windows Fiddler gibi ağ araçları varsa, mümkün toodiagnose hello sorunlar gibi olabilir:

- Proxy üzerinden toowork varsa, Ağ aracı tooconnect hello proxy'si aracılığıyla tooconfigure olabilir.

- Ağ aracı tarafından kullanılan başlangıç bağlantı noktası numarasını denetleyin.

- Merhaba yerel ana bilgisayar URL'sini ve proxy ayarları Depolama Gezgini olarak aracın bağlantı noktası numarası ağ hello girin. Bu doğru gerçekleştirilir, ağ aracınızı Depolama Gezgini toomanagement ve hizmet uç noktaları tarafından yapılan ağ istekleri günlüğünü başlatır. Örneğin, bir tarayıcıda blob uç noktanız için https://cawablobgrs.blob.core.windows.net/ girin ve bir yanıtı alırsınız Bu verilere erişemez olsa da, hello kaynak var, öneren hello aşağıdakine benzer.

![kod örneği](./media/storage-explorer-troubleshooting/4022502_en_2.png)

### <a name="contact-proxy-server-admin"></a>Proxy sunucu yöneticisine başvurun

Proxy ayarlarınızın doğru olduğunu, proxy sunucusu yöneticinize toocontact olabilir ve

- Proxy trafiği tooAzure yönetim veya kaynak uç noktaları engellemez emin olun.

- Proxy sunucunuz tarafından kullanılan hello kimlik doğrulama protokolü doğrulayın. Depolama Gezgini NTLM proxy'leri şu anda desteklemiyor.

## <a name="unable-tooretrieve-children-error-message"></a>"Oluşturulamıyor tooRetrieve alt" hata iletisi

Bir proxy üzerinden bağlı tooAzure varsa, proxy ayarlarının doğru olduğundan emin olun. Merhaba aboneliği veya hesabı hello sahibinden erişim tooa kaynak verilmiş, okuma veya bu kaynak için izinleri listesinde doğrulayın.

### <a name="issues-with-sas-url"></a>SAS URL ile ilgili sorunları
Bir SAS URL'si kullanarak ve bu hatanın tooa hizmeti bağlanıyorsanız:

- Merhaba URL tooread veya liste kaynakları hello gerekli izinleri sağladığından emin olun.

- URL süresi geçmemiş bu hello doğrulayın.

- Merhaba SAS URL bir erişim ilkesini temel alarak, hello erişim ilkesi edilmediğini doğrulayın.

## <a name="next-steps"></a>Sonraki adımlar

Hello çözümleri hiçbiri sizin için çalışıyorsanız, sorununuzu hello geri bildirim araçla e-posta ile gönderme ve böylece sizinle hello sorunu düzeltmek için iletişime geçebiliriz sayıda ayrıntılarını dahil ettiğiniz hello sorunu olabilir.

toodo bunu, **yardımcı** menüsüne ve ardından **geri bildirim gönder**.

![Geri Bildirim](./media/storage-explorer-troubleshooting/4022503_en_1.png)
