---
title: MFA sunucusu mobil uygulama Web Hizmeti'ni aaaAzure | Microsoft Docs
description: "Merhaba Microsoft Authenticator uygulaması ek bant dışı kimlik doğrulama seçeneği sunar.  Merhaba MFA sunucusu toouse anında iletme bildirimleri toousers sağlar."
services: multi-factor-authentication
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: 6c8d6fcc-70f4-4da4-9610-c76d66635b8b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2017
ms.author: joflore
ms.reviewer: alexwe
ms.custom: it-pro
ms.openlocfilehash: 4175b68fcbf85ec3fd53d8edf4e07306c75a4c71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-mobile-app-authentication-with-azure-multi-factor-authentication-server"></a>Azure Multi-Factor Authentication Sunucusu ile mobil uygulama kimlik doğrulamasını etkinleştirme

Merhaba Microsoft Authenticator uygulaması ek bant dışı doğrulama seçeneği sunar. Bir otomatik telefon çağrısı veya SMS toohello kullanıcı oturum açma sırasında uygulamak yerine, Azure multi-Factor Authentication bir bildirim toohello Microsoft Authenticator uygulaması hello kullanıcının akıllı telefonundaki veya tabletindeki iter. Merhaba kullanıcı yalnızca dokunur **doğrula** (veya bir PIN girer ve "Kimliği doğrula" dokunur), kullanıcıların oturum açma uygulama toocomplete hello.

Şebeke sinyal gücünün güvenilir olmadığı durumlarda iki aşamalı doğrulama için bir mobil uygulama kullanmak tercih edilir. Bir OATH belirteci Oluşturucu olarak hello uygulamasını kullanıyorsanız, herhangi bir ağ veya Internet bağlantısı olmasını gerektirmez.

Ortamınıza bağlı olarak toodeploy hello mobil uygulama web hizmeti hello isteyebilirsiniz Azure multi-Factor Authentication sunucusu veya başka bir internet'e yönelik sunucuda aynı sunucu.

## <a name="requirements"></a>Gereksinimler

toouse hello Microsoft Authenticator uygulaması hello aşağıdaki Hello uygulama başarıyla mobil uygulama Web hizmeti ile iletişim kurabilmesi için gereklidir:

* Azure Multi-Factor Authentication Sunucusu v6.0 veya üzeri
* Microsoft® [Internet Information Services (IIS) IIS 7.x veya üzerini](http://www.iis.net/) çalıştıran İnternet’e yönelik bir web sunucusuna Mobil Uygulama Web Hizmeti’ni yükleme
* ASP.NET v4.0.30319 yüklü, kayıtlı ve tooAllowed ayarlayın
* Gerekli rol hizmetleri ASP.NET ve IIS 6 Metatabanı Uyumluluğu’nu içerir.
* Mobil Uygulama Web Hizmeti’nin genel bir URL ile erişilebilir olması
* Mobil Uygulama Web Hizmeti’nin bir SSL sertifikası ile güvenli hale getirilmesi.
* IIS'de Hello Azure çok faktörlü kimlik doğrulama Web hizmeti SDK'sı yükleme 7.x ya da daha yüksek hello üzerinde **hello Azure multi-Factor Authentication sunucusu ile aynı sunucu**
* Hello Azure çok faktörlü kimlik doğrulama Web hizmeti SDK'sı bir SSL sertifikası ile güvenli hale getirilir.
* Mobil uygulama Web hizmeti SSL üzerinden Azure multi-Factor Authentication Web hizmeti SDK toohello bağlanabilir
* Mobil uygulama Web hizmeti toohello Azure MFA Web hizmeti SDK'sı kimlik doğrulaması hello hello "PhoneFactor Admins" güvenlik grubunun üyesi olan bir hizmet hesabı kimlik bilgilerini kullanarak. Etki alanına katılmış bir sunucuda Hello Azure çok faktörlü kimlik doğrulama sunucusu ise, bu hizmet hesabı ve grubu Active Directory'de mevcut. Birleştirilmiş tooa etki alanında değilse bu hizmet hesabı ve grubu hello Azure çok faktörlü kimlik doğrulama sunucusu üzerinde yerel olarak mevcut.

## <a name="install-hello-mobile-app-web-service"></a>Merhaba mobil uygulama web Hizmeti'ni yükleme

Merhaba mobil uygulama web Hizmeti'ni yüklemeden önce aşağıdaki ayrıntılara hello dikkat edin:

* "PhoneFactor Admins" grubunun bir parçası olan bir Hizmet Hesabınız olması gerekir. Bu hesap bir hello aynı hello Kullanıcı Portalı yükleme için kullanılan hello olabilir.
* Bu yararlı tooopen hello Internet'e yönelik web sunucusunda bir web tarayıcısı ve hello hello web.config dosyasına girilen Web hizmeti SDK toohello URL'sini gidin. Merhaba tarayıcı toohello web hizmetine başarıyla gidebilirse, kimlik bilgilerinizi ister. Merhaba kullanıcı adı ve hello dosyasında göründüğü gibi hello web.config dosyasına girilen parolayı girin. Sertifika uyarısı ya da hatası görüntülenmediğinden emin olun.
* Ters proxy ya da güvenlik duvarı hello mobil uygulama Web hizmeti web sunucusunun önünde ve SSL boşaltma gerçekleştiriyorsa, hello mobil uygulama Web hizmeti http yerine https kullanabilmesi için hello mobil uygulama Web hizmeti web.config dosyasını düzenleyebilirsiniz. SSL, mobil uygulama toohello güvenlik duvarı/ters proxy'ye hello hala gereklidir. Anahtar toohello aşağıdaki hello eklemek \<appSettings\> bölümü:

        <add key="SSL_REQUIRED" value="false"/>

### <a name="install-hello-web-service-sdk"></a>Merhaba web hizmeti SDK'sını yükleyin

Her iki durumda da hello Azure çok faktörlü kimlik doğrulama Web hizmeti SDK'sı ise **değil** hello Azure çok faktörlü kimlik doğrulama (MFA) sunucu üzerinde yüklü, tam hello adımlar anlatılmaktadır.

1. Merhaba çok faktörlü kimlik doğrulama sunucusu konsolunu açın.
2. Toohello Git **Web hizmeti SDK'sı** seçip **Web hizmeti SDK'sını yüklemek**.
3. Tam hello yükleme toochange gerekmedikçe hello varsayılanları kullanarak herhangi bir nedenle bunları.
4. IIS'de bir SSL sertifikası toohello sitesi bağlayın.

Bir IIS sunucusunda bir SSL sertifikası yapılandırma hakkında sorularınız varsa, hello makalesine bakın [nasıl tooSet SSL IIS'de](https://docs.microsoft.com/en-us/iis/manage/configuring-security/how-to-set-up-ssl-on-iis).

Merhaba Web hizmeti SDK'sı bir SSL sertifikası ile güvenli gerekir. Bu amaç için otomatik olarak imzalanan bir sertifika kullanılabilir. Böylece hello SSL bağlantısı başlatılırken bu sertifikayı güvenleri hello sertifika hello hello Kullanıcı Portalı web sunucusundaki yerel bilgisayar hesabının hello "Güvenilen kök sertifika yetkilileri" deposuna aktarın.

![MFA Sunucusu yapılandırma kurulum Web hizmeti SDK'sı](./media/multi-factor-authentication-get-started-server-webservice/sdk.png)

### <a name="install-hello-service"></a>Merhaba Hizmeti'ni yükleme

1. **Merhaba MFA sunucusu üzerinde**, toohello yükleme yolu göz atın.
2. Toohello gidin hello Azure MFA sunucusu yüklü hello varsayılan olduğu klasördür **C:\Program Files\Azure multi-Factor Authentication**.
3. Merhaba yükleme dosyasını bulun **MultiFactorAuthenticationMobileAppWebServiceSetup64**. Merhaba sunucusuysa **değil** İnternete dönük, kopyalama hello yükleme dosyası toohello Internet'e sunucusu.
4. Merhaba MFA sunucusu ise **değil** Internet'e anahtar toohello **Internet'e sunucu**.
5. Merhaba çalıştırmak **MultiFactorAuthenticationMobileAppWebServiceSetup64** yönetici olarak dosya yüklemek, isterseniz hello Site değiştirin ve isterseniz hello sanal dizin tooa kısa adı değiştirin.
6. Sonlandırma hello yüklendikten sonra çok Gözat**C:\inetpub\wwwroot\MultiFactorAuthMobileAppWebService** (veya hello sanal dizin adını temel alarak uygun dizin) ve hello Web.Config dosyasını düzenleyin.

   * Merhaba anahtarını bulun **"Web_servıce_sdk_authentıcatıon_username"** değiştirip **değer = ""** çok**değer "Etki alanı\kullanıcı" =** burada bir parçası olan bir hizmet hesabı, etki alanı\kullanıcı "PhoneFactor Admins" grubu.
   * Hello anahtarını bulun **"Web_servıce_sdk_authentıcatıon_password değerlerini"** değiştirip **değeri = ""** çok**değeri "Password" =** parola hello hizmet hello parolasını olduğu Merhaba önceki satırda girilen hesabı.
   * Hello bulur **pfMobile App Web Service_pfwssdk_PfWsSdk** ayarlama ve hello değerinden değiştirme **http://localhost:4898/PfWsSdk.asmx** toohello Web hizmeti SDK URL'si (örnek: https://mfa.contoso.com/ MultiFactorAuthWebServiceSdk/PfWsSdk.asmx).
   * Merhaba Web.Config dosyasını kaydedin ve Not Defteri'ni kapatın.

   > [!NOTE]
   > Bu bağlantı için SSL kullanılır başvurmalısınız Web hizmeti SDK'sı tarafından hello **tam etki alanı adı (FQDN)** ve **IP adresi değil**. Hello SSL sertifikası hello FQDN için verilmiş ve hello kullanılan URL hello sertifika üzerindeki hello adı eşleşmelidir.

7. Mobil uygulama Web hizmeti altında yüklendi hello Web sitesi ortak olarak imzalanmış bir sertifika ile zaten bağlı değil, hello sertifika hello sunucuya yükleyin, IIS Yöneticisi'ni açın ve hello sertifika toohello Web bağlayın.
8. Herhangi bir bilgisayarda web tarayıcısını açın ve mobil uygulama Web Hizmeti'nin yüklendiği toohello URL'ye gidin (örnek: https://mfa.contoso.com/MultiFactorAuthMobileAppWebService). Sertifika uyarısı ya da hatası görüntülenmediğinden emin olun.

## <a name="configure-hello-mobile-app-settings-in-hello-azure-multi-factor-authentication-server"></a>Hello Azure çok faktörlü kimlik doğrulama sunucusu Hello mobil uygulama ayarlarını yapılandırın

Merhaba mobil uygulama web hizmetinin yüklü olduğu, tooconfigure hello Azure çok faktörlü kimlik doğrulama sunucusu toowork hello portalıyla gerekir.

1. Merhaba çok faktörlü kimlik doğrulama sunucusu konsolunda hello Kullanıcı Portalı simgesine tıklayın. Kullanıcıların toocontrol izin verilen kendi kimlik doğrulama yöntemlerini denetleyin **mobil uygulama** hello ayarları sekmesinde altında **tooselect yöntemi kullanıcıların**. Bu özellik etkinleştirilmeden, son kullanıcılar gerekli toocontact olan hello mobil uygulama için Yardım Masası toocomplete etkinleştirme.
2. Merhaba denetleyin **kullanıcılar tooactivate mobil uygulama izin** kutusu.
3. Merhaba denetleyin **kullanıcı kaydına izin ver** kutusu.
4. Merhaba tıklatın **mobil uygulama** simgesi.
5. MultiFactorAuthenticationMobileAppWebServiceSetup64 yüklerken oluşturulan hello sanal dizinle kullanılan hello URL'sini girin (örnek: https://mfa.contoso.com/MultiFactorAuthMobileAppWebService/) hello alanında  **Mobil uygulama Web hizmeti URL'si:**.
6. Merhaba doldurmak **hesap adı** hello şirketiniz veya kuruluşunuz adı toodisplay bu hesap için hello mobil uygulamada ile alan.
   ![MFA Sunucusu yapılandırması Mobil Uygulama ayarları](./media/multi-factor-authentication-get-started-server-webservice/mobile.png)

## <a name="next-steps"></a>Sonraki adımlar

- [Azure Multi-Factor Authentication ve üçüncü taraf VPN’ler ile gelişmiş senaryolar](multi-factor-authentication-advanced-vpn-configurations.md).