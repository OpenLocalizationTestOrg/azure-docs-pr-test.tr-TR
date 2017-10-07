---
title: aaaUpgrade PhoneFactor tooAzure MFA sunucusu | Microsoft Docs
description: "Merhaba eski phonefactor aracısından yükseltme sırasında Azure MFA sunucusu kullanmaya başlayın."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 42838ff7-bdf2-4d06-bacc-b3839a00cd76
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/06/2017
ms.author: kgremban
ms.openlocfilehash: 15b7b8517929c30f66e6a39cd44c69d12d25c6d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-hello-phonefactor-agent-tooazure-multi-factor-authentication-server"></a>Yükseltme hello PhoneFactor Aracısı tooAzure çok faktörlü kimlik doğrulama sunucusu
tooupgrade PhoneFactor Agent v5.x ya da eski tooAzure çok faktörlü kimlik doğrulama sunucusu hello hello PhoneFactor Aracısı'ı kaldırın ve bileşenler ilk bağlı. Çok faktörlü kimlik doğrulama sunucusu hello ve bunun bağlı bileşenleri yüklenebilir.

## <a name="uninstall-hello-phonefactor-agent"></a>Merhaba PhoneFactor aracısı kaldırma

1. İlk olarak, hello PhoneFactor veri dosyasının yedeğini alın. Merhaba varsayılan yükleme konumu C:\Program Files\PhoneFactor\Data\Phonefactor.pfdata şeklindedir.

2. Merhaba Kullanıcı Portalı yüklü ise:
  1. Toohello yükleme klasörüne gidin ve hello web.config dosyasını yedekleyin. Merhaba varsayılan yükleme konumu C:\inetpub\wwwroot\PhoneFactor şeklindedir.

  2. Özel Temalar toohello portal eklediyseniz, hello C:\inetpub\wwwroot\PhoneFactor\App_Themes dizini altındaki özel klasörünüzü yedekleyin.

  3. Merhaba Kullanıcı Portalı hello PhoneFactor Aracısı aracılığıyla ya da kaldırma (Merhaba üzerinde yüklü değilse yalnızca kullanılabilir aynı sunucuya hello PhoneFactor Aracısı) ya da Windows programlar ve özellikler aracılığıyla.

3. Merhaba mobil uygulama Web hizmeti yüklü ise:

  1. Toohello yükleme klasörüne gidin ve hello web.config dosyasını yedekleyin. Merhaba varsayılan yükleme konumu C:\inetpub\wwwroot\PhoneFactorPhoneAppWebService şeklindedir.

  2. Merhaba mobil uygulama Web Hizmeti'ni Windows programlar ve özellikler aracılığıyla kaldırın.

4. Merhaba Web hizmeti SDK'sı yüklü ise hello PhoneFactor Aracısı aracılığıyla ya da Windows programlar ve özellikler aracılığıyla kaldırın.

5. Merhaba PhoneFactor Aracısı Windows programlar ve özellikler aracılığıyla kaldırın.

## <a name="install-hello-multi-factor-authentication-server"></a>Merhaba multi-Factor Authentication sunucusu yükleyin

aynı hello yüklemelidir şekilde hello yükleme yolu hello kayıt defteri hello önceki PhoneFactor Aracısı yüklemesinin kayıt konum (örneğin, C:\Program Files\PhoneFactor). Yeni yüklemeler farklı bir varsayılan yükleme yoluna (örneğin, C:\Program Files\Multi-Factor Authentication Server) sahip olacaktır. kullanıcılarınız ve ayarlarınız yeni multi-Factor Authentication sunucusu hello yükledikten sonra devam şekilde PhoneFactor Aracısı yükleme sırasında yükseltilmelidir hello tarafından önceki kalan veri dosyası hello.

1. İstenirse, hello multi-Factor Authentication Sunucusu'nu etkinleştirin ve toohello doğru çoğaltma grubuna atandığından emin olun.

2. Web hizmeti SDK'sı önceden yüklenmişse, hello yüklerseniz hello multi-Factor Authentication sunucusu kullanıcı arabirimi aracılığıyla yeni Web hizmeti SDK hello.

  sanal dizin adının artık varsayılan Hello **Phonefactorwebservicesdk** yerine **Multifactorauthwebservicesdk**. Toouse hello önceki adı isterseniz, yükleme sırasında hello hello sanal dizin adını değiştirmeniz gerekir. Merhaba yükleme toouse hello yeni varsayılan adı izin Aksi takdirde toochange hello URL herhangi bir uygulamanın bu başvuru hello Web hizmeti SDK'sı (örneğin, hello Kullanıcı Portalı ve mobil uygulama Web hizmeti) toopoint hello doğru konumda varsa.

3. Hello Kullanıcı Portalı önceden PhoneFactor Aracısı sunucusu hello üzerinde yüklüyse, yükleme hello multi-Factor Authentication sunucusu kullanıcı arabirimi aracılığıyla yeni multi-Factor Authentication Kullanıcı Portalı hello.

  sanal dizin adının artık varsayılan Hello **MultiFactorAuth** yerine **PhoneFactor**. Toouse hello önceki adı isterseniz, yükleme sırasında hello hello sanal dizin adını değiştirmeniz gerekir. Aksi takdirde hello yükleme toouse hello yeni varsayılan adı izin verirseniz, hello hello multi-Factor Authentication sunucusu kullanıcı portalı simgesine tıklayın ve hello Ayarlar sekmesinde kullanıcı portalı URL'si hello güncelleştirmesi gerekir.

4. Merhaba Kullanıcı Portalı ve/veya mobil uygulama Web hizmeti daha önce yüklendiyse, farklı bir sunucudan PhoneFactor Aracısı hello:

  1. Toohello yükleme konumu (örneğin, C:\Program Files\PhoneFactor) gidin ve diğer sunucu bir veya daha fazla yükleyicileri toohello kopyalayın. Merhaba Kullanıcı Portalı ve mobil uygulama Web hizmeti için 32-bit ve 64-bit yükleyiciler vardır. Bunlara MultiFactorAuthenticationUserPortalSetupXX.msi ve MultiFactorAuthenticationMobileAppWebServiceSetupXX.msi adı verilir.

  2. tooinstall hello Kullanıcı Portalı hello web sunucusunda bir yönetici olarak bir komut istemi açın ve multifactorauthenticationuserportalsetupxx.msi komutunu çalıştırın.

    sanal dizin adının artık varsayılan Hello **MultiFactorAuth** yerine **PhoneFactor**. Toouse hello önceki adı isterseniz, yükleme sırasında hello hello sanal dizin adını değiştirmeniz gerekir. Aksi takdirde hello yükleme toouse hello yeni varsayılan adı izin verirseniz, hello hello multi-Factor Authentication sunucusu kullanıcı portalı simgesine tıklayın ve hello Ayarlar sekmesinde kullanıcı portalı URL'si hello güncelleştirmesi gerekir. Mevcut kullanıcıları hello yeni URL konusunda bilgi sahibi toobe gerekir.

  3. Toohello Kullanıcı Portalı yükleme konumuna (örneğin, C:\inetpub\wwwroot\MultiFactorAuth) gidin ve hello web.config dosyasını düzenleyin. Merhaba yükseltmeden önce hello yeni web.config dosyasına Yedeklenen özgün web.config dosyanızın hello appSettings ve applicationSettings bölümlerindeki Hello değerlerini kopyalayın. Hello Web hizmeti SDK'sını yüklerken Hello yeni varsayılan sanal dizin adını sakladıysanız hello applicationSettings bölümünde toopoint toohello doğru konumda hello URL'yi değiştirin. Merhaba önceki web.config dosyasında diğer varsayılan değerler değiştirildiyse, bu aynı değişiklikleri toohello yeni web.config dosyasına uygulayın.

  4. Merhaba web sunucusunda tooinstall hello mobil uygulama Web hizmeti bir yönetici olarak bir komut istemi açın ve hello multifactorauthenticationmobileappwebservicesetupxx.msi komutunun çalıştırın.

    sanal dizin adının artık varsayılan Hello **multifactorauthmobileappwebservice değerini** yerine **Multifactorauthmobileappwebservice**. Toouse hello önceki adı isterseniz, yükleme sırasında hello hello sanal dizin adını değiştirmeniz gerekir. Toochoose daha kısa bir ad toomake isteyebilirsiniz, mobil cihazlarında son kullanıcıların tootype daha kolay. Aksi takdirde hello yükleme toouse hello yeni varsayılan adı izin verirseniz, hello çok faktörlü kimlik doğrulama sunucusu hello mobil uygulama simgesine tıklayın ve hello mobil uygulama Web hizmeti URL'sini güncelleştirmesi gerekir.

  5. Toohello mobil uygulama Web hizmeti yükleme konumu (örneğin, C:\inetpub\wwwroot\MultiFactorAuthMobileAppWebService) gidin ve hello web.config dosyasını düzenleyin. Merhaba yükseltmeden önce hello yeni web.config dosyasına Yedeklenen özgün web.config dosyanızın hello appSettings ve applicationSettings bölümlerindeki Hello değerlerini kopyalayın. Hello Web hizmeti SDK'sını yüklerken Hello yeni varsayılan sanal dizin adını sakladıysanız hello applicationSettings bölümünde toopoint toohello doğru konumda hello URL'yi değiştirin. Merhaba önceki web.config dosyasında diğer varsayılan değerler değiştirildiyse, bu aynı değişiklikleri toohello yeni web.config dosyasına uygulayın.

## <a name="next-steps"></a>Sonraki adımlar

- [Merhaba kullanıcı portalını yükleme](multi-factor-authentication-get-started-portal.md) hello Azure multi-Factor Authentication sunucusu için.

- Uygulamalarınız için [Windows Kimlik Doğrulamasını yapılandırın](multi-factor-authentication-get-started-server-windows.md). 
