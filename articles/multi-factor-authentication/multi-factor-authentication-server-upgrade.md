---
title: "aaaAzure MFA sunucusu yükseltme | Microsoft Docs"
description: "Adımlar ve kılavuz tooupgrade hello Azure çok faktörlü kimlik doğrulama sunucusu tooa daha yeni sürümü."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 50bb8ac3-5559-4d8b-a96a-799a74978b14
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: aaa8d400e0e5f1c6be3a6d22cde6dd893ef4d546
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-toohello-latest-azure-multi-factor-authentication-server"></a>Toohello yükseltme en son Azure multi-Factor Authentication sunucusu

Bu makalede hello anlatılmaktadır Azure çok faktörlü kimlik doğrulama (MFA) sunucusu v6.0 yükseltme sürecini ya da daha yüksek. Tooupgrade hello PhoneFactor Aracısı'nın eski bir sürümü gereksinim duyarsanız, çok başvurun[yükseltme hello PhoneFactor Aracısı tooAzure çok faktörlü kimlik doğrulama sunucusu](multi-factor-authentication-get-started-server-upgrade.md).

Yükseltme v6.x veya eski toov7.x ya da daha yeni varsa, tüm bileşenler .NET 2.0 too.NET 4.5 değiştirin. Tüm bileşenler için Microsoft Visual C++ 2015 Redistributable Update 1 veya daha yüksek de gerekir. Bunlar zaten yüklü değilse hello MFA sunucusu yükleyici hem hello x86 hem x64 sürümlerini bu bileşenleri yükler. Merhaba Kullanıcı Portalı ve mobil uygulama Web hizmeti ayrı sunucularda çalıştırırsanız, tooinstall bu paketleri bu bileşenler yükseltmeden önce gerekir. En son Microsoft Visual C++ 2015 Redistributable güncelleştirmesini hello hello arayabilirsiniz [Microsoft Download Center](https://www.microsoft.com/en-us/download/). 

## <a name="install-hello-latest-version-of-azure-mfa-server"></a>Azure MFA sunucusu Hello en son sürümünü yükleyin

1. Merhaba yönergeleri kullanın [indirme hello Azure çok faktörlü kimlik doğrulama sunucusu](multi-factor-authentication-get-started-server.md#download-the-azure-multi-factor-authentication-server) tooget hello en son sürümünü hello Azure MFA sunucusu.
2. Merhaba MFA sunucusu veri dosyasındaki ana MFA sunucunuzda C:\Program Files\Multi-Factor Authentication Server\Data\PhoneFactor.pfdata (olduğunu varsayarak hello varsayılan yükleme konumu) konumunda bulunan bir yedeğini alın.
3. Yüksek kullanılabilirlik için birden çok sunucu çalıştırırsanız, toohello MFA sunucusu kimlik doğrulaması ve böylece yükseltiyorsanız toohello sunucuları trafiği göndermeye Durdur hello istemci sistemleri değiştirin. Bir yük dengeleyici kullanırsanız, MFA sunucusu hello yük dengeleyiciden kaldırın, yükseltme Merhaba ve ardından hello sunucu geri hello grubuna ekleyin.
4. Merhaba yeni Yükleyici her MFA sunucusunda çalıştırın. Hello Yöneticisi tarafından çoğaltılmasını hello eski veri dosyası okuyabilir bağımlı sunucular ilk yükseltin. 

  Geçerli MFA sunucunuz çalışan hello Yükleyici önce toouninstall gerekmez. Merhaba yükleyici yerinde yükseltme gerçekleştirir. aynı hello yükler şekilde hello yükleme yolu hello önceki yüklemesinden hello kayıt defterinden kayıt konum (örneğin, C:\Program Files\Multi-Factor Authentication Server). 
  
5. İstendiğinde tooinstall Microsoft Visual C++ 2015 Redistributable güncelleştirme paketini değilseniz, hello isteğini kabul edin. Her iki hello x86 hem x64 sürümleri hello paketi yüklenir.
5. Merhaba Web hizmeti SDK'sı kullanıyorsanız istenir tooinstall hello yeni Web hizmeti SDK'sı. Yüklediğinizde yeni Web hizmeti SDK'sı Merhaba, daha önce yüklenmiş hello sanal dizin (örneğin, Phonefactorwebservicesdk) bu hello sanal dizin adıyla eşleştiğinden emin olun.
6. Tüm bağımlı sunucularında Hello adımları yineleyin. Merhaba ast toobe hello yeni ana sonra yükseltme hello eski ana sunucu birini yükseltin. 

## <a name="upgrade-hello-user-portal"></a>Merhaba Kullanıcı Portalı yükseltme

1. Merhaba sanal hello Kullanıcı Portalı yükleme konumu (örneğin, C:\inetpub\wwwroot\MultiFactorAuth) Directory'de hello web.config dosyasının yedeğini alın. Toohello varsayılan tema herhangi bir değişiklik yapıldıysa, hello App_Themes\Default klasörünün yanı sıra bir yedeğini alın. Daha iyi toocreate hello varsayılan klasör kopyasıdır ve toochange hello varsayılan tema daha yeni bir tema oluşturun.
2. MFA sunucusu yüklemesi Hello Kullanıcı Portalı aynı sunucu diğer MFA sunucusu bileşenleri hello gibi hello hello üzerinde çalışıyorsa tooupdate hello Kullanıcı Portalı ister. Merhaba isteğini kabul edin ve hello Kullanıcı Portalı güncelleştirmesini yükleyin. Daha önce yüklenmiş hello sanal dizin (örneğin, MultiFactorAuth) bu hello sanal dizin adıyla eşleşen denetleyin.
3. Merhaba Kullanıcı Portalı kendi sunucusundaysa, hello hello multifactorauthenticationuserportalsetup64.msi dosyasını dosya Kopyala yükleme konumu hello MFA sunucuları birinin ve hello Kullanıcı Portalı web sunucusuna yerleştirin. Merhaba yükleyiciyi çalıştırın. 

  Belirten bir hata oluşursa, "Microsoft Visual C++ 2015 Redistributable Update 1 veya daha yüksek gereklidir" yükleyip hello son güncelleştirme paketini hello [Microsoft Download Center](https://www.microsoft.com/download/). Her iki hello x86 hem x64 sürümünü yükleyin.

4. Kullanıcı Portalı yazılımı yüklü Hello güncelleştirdikten sonra hello yeni web.config dosyasını 1. adımda yaptığınız hello web.config yedekleme karşılaştırın. Yeni öznitelik hello yeni web.config dosyasında yoksa, hello sanal dizin toooverwrite hello yeni bir yedekleme web.config kopyalayın. Toocopy/Yapıştır hello appSettings değerleri ve hello Web hizmeti SDK hello yedekleme hello yeni web.config dosyasına URL'den bunun başka bir seçenektir.

Birden çok sunucuya hello kullanıcı portalı varsa, bunların tümünün hello yüklemesinde yineleyin. 


## <a name="upgrade-hello-mobile-app-web-service"></a>Yükseltme hello mobil uygulama Web hizmeti

1. Mobil uygulama Web hizmeti yükleme konumu (örneğin, C:\inetpub\wwwroot\app veya C:\inetpub\wwwroot\MultiFactorAuthMobileAppWebService) hello sanal hello dizinde: hello web.config dosyasının yedeğini alın.
2. Merhaba hello multifactorauthenticationmobileappwebservicesetup64.msi dosyasını dosya Kopyala yüklemesi hello MFA sunucuları konumunu ve hello mobil uygulama kayıt web sunucunuza yerleştirin.
3. Merhaba yükleyiciyi çalıştırın. 

  Microsoft Visual C++ 2015 Redistributable Update 1 veya daha yüksek gerekli olduğunu bildiren bir hata meydana gelirse yükleyip hello son güncelleştirme paketini hello [Microsoft Download Center](https://www.microsoft.com/download/). Her iki hello x86 hem x64 sürümünü yükleyin.

4. Güncelleştirilmiş hello mobil uygulama Web hizmeti yazılım yüklendikten sonra hello yeni web.config dosyasını 1. adımda yedeklenen hello web.config dosyasında karşılaştırın. Yeni öznitelik hello yeni web.config dosyasında yoksa, kaydedilen web.config hello sanal dizinine kopyalayın ve hello yeni bir üzerine yazma. Toocopy/Yapıştır hello appSettings değerleri ve hello Web hizmeti SDK hello yedekleme hello yeni web.config dosyasına URL'den bunun başka bir seçenektir.

Birden çok sunucuya hello mobil uygulama Web hizmeti varsa, bunların tümünün hello yüklemesinde yineleyin. 

## <a name="upgrade-hello-ad-fs-adapters"></a>Yükseltme hello AD FS bağdaştırıcısı


### <a name="if-mfa-runs-on-different-servers-than-ad-fs"></a>MFA ADFS değerinden farklı sunucularda çalışıyorsa

Multi-Factor Authentication sunucusu, AD FS sunucularından ayrı olarak çalıştırırsanız, bu yönergeler yalnızca geçerlidir. Her iki hizmet çalıştırırsanız hello aynı sunucuları, bu bölüm atlayın ve toohello yükleme adımlarını gidin. 

1. AD FS'de kaydedildiği hello MultiFactorAuthenticationAdfsAdapter.config dosyasının bir kopyasını kaydedin veya hello aşağıdaki PowerShell komutunu kullanarak hello yapılandırmasını dışarı aktarma: `Export-AdfsAuthenticationProviderConfigurationData -Name [adapter name] -FilePath [path tooconfig file]`. Merhaba bağdaştırıcı adı "WindowsAzureMultiFactorAuthentication" veya "AzureMfaServerAuthentication" daha önce yüklenmiş hello bağlı olarak sürümüdür.
2. Merhaba hello MFA sunucusu yükleme konumu toohello AD FS sunucularından aşağıdaki dosyaları kopyalayın:

  - MultiFactorAuthenticationAdfsAdapterSetup64.msi
  - Register-MultiFactorAuthenticationAdfsAdapter.ps1
  - Unregister-MultiFactorAuthenticationAdfsAdapter.ps1
  - MultiFactorAuthenticationAdfsAdapter.config

3. Ekleyerek Hello Register-MultiFactorAuthenticationAdfsAdapter.ps1 betiğini düzenleyin `-ConfigurationFilePath [path]` hello toohello sonuna `Register-AdfsAuthenticationProvider` komutu. Değiştir *[path]* hello tam yolu toohello MultiFactorAuthenticationAdfsAdapter.config dosyasını veya hello yapılandırma dosyasını dışarı hello önceki adımda. 

  Merhaba eski yapılandırma dosyası eşleşirlerse hello yeni MultiFactorAuthenticationAdfsAdapter.config toosee hello öznitelikleri denetleyin. Öznitelik eklenmiş veya hello yeni sürümde kaldırılmış, hello eski yapılandırma dosyası toohello yeni bir hello öznitelik değerlerini kopyalayın veya hello eski yapılandırma dosyası toomatch değiştirin.

### <a name="install-new-ad-fs-adapters"></a>Yeni AD FS bağdaştırıcısı yükleme

> [!IMPORTANT] 
> Kullanıcılarınız, bu bölümün gerekli tooperform iki aşamalı doğrulama sırasında adım 3-8 olmaz. AD FS yapılandırılan varsa, birden çok kümeleri, kaldırabilirsiniz, yükseltme ve geri yükleme hello her kümedeki grubu bağımsız diğer kümeleri tooavoid kapalı kalma süresi hello.

1. Bazı AD FS sunucuları hello grubundan kaldırın. Başkalarının hala çalışıyor hello sırasında bu sunucuları güncelleştirin.
2. Merhaba yeni AD FS bağdaştırıcısı hello AD FS grubundan kaldırıldı her sunucuya yükleyin. Merhaba MFA sunucusu her AD FS sunucusunda yüklüyse, hello MFA sunucusu Yöneticisi UX güncelleştirebilirsiniz Aksi takdirde MultiFactorAuthenticationAdfsAdapterSetup64.msi çalıştırarak güncelleştirin. 

  Belirten bir hata oluşursa, "Microsoft Visual C++ 2015 Redistributable Update 1 veya daha yüksek gereklidir" yükleyip hello son güncelleştirme paketini hello [Microsoft Download Center](https://www.microsoft.com/download/). Her iki hello x86 hem x64 sürümünü yükleyin.

3. Çok Git**AD FS** > **kimlik doğrulama ilkeleri** > **genel çok faktörlü kimlik doğrulama ilkesini Düzenle**. İşaretini **WindowsAzureMultiFactorAuthentication** veya **AzureMFAServerAuthentication** (bağlı olarak yüklenen hello geçerli sürüm). 

  Bu adım tamamlandıktan sonra MFA sunucusu üzerinden iki aşamalı doğrulamayı adım 8 tamamlanana kadar bu AD FS kümede kullanılabilir değil.

4. Merhaba Unregister-MultiFactorAuthenticationAdfsAdapter.ps1 PowerShell betiğini çalıştırarak hello AD FS bağdaştırıcısının unregister hello eski sürümü. Bu hello olun *-Name* parametresi ("WindowsAzureMultiFactorAuthentication" veya "AzureMFAServerAuthentication"), 3. adımda görüntülenen hello adı ile eşleşen. Merkezi bir yapılandırma olduğundan bu hello aynı AD FS kümesindeki tooall sunucular için geçerlidir.
5. Merhaba yeni AD FS bağdaştırıcısı hello Register-MultiFactorAuthenticationAdfsAdapter.ps1 PowerShell betiğini çalıştırarak kaydedin. Merkezi bir yapılandırma olduğundan bu hello aynı AD FS kümesindeki tooall sunucular için geçerlidir.
6. Merhaba hello AD FS grubundan kaldırıldı her sunucuda AD FS hizmetini yeniden başlatın.
7. Kaldır hello hello gruptan diğer sunuculara ve güncelleştirilmiş hello sunucuları toohello AD FS grubunu geri ekleyin.
8. Çok Git**AD FS** > **kimlik doğrulama ilkeleri** > **genel çok faktörlü kimlik doğrulama ilkesini Düzenle**. Denetleme **AzureMfaServerAuthentication**.
9. 2. adım tooupdate hello sunucular şimdi hello AD FS grubundan kaldırıldı yineleyin ve bu sunucular üzerinde hello AD FS hizmetini yeniden başlatın.
10. Bu sunucuların geri hello AD FS grubuna ekleyin.

## <a name="next-steps"></a>Sonraki adımlar

- Örnekleri alın [Azure çok faktörlü kimlik doğrulama ve üçüncü taraf VPN ile Gelişmiş senaryolar](multi-factor-authentication-advanced-vpn-configurations.md)

- [MFA sunucusu Windows Server Active Directory ile eşitleme](multi-factor-authentication-get-started-server-dirint.md)

- [Windows kimlik doğrulamasını yapılandırmak](multi-factor-authentication-get-started-server-windows.md) uygulamalarınız için
