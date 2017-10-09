---
title: "Azure AD Connect: Önkoşulları ve donanım | Microsoft Docs"
description: "Bu konu hello ön koşullar ve Azure AD Connect hello donanım gereksinimlerini açıklar"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 91b88fda-bca6-49a8-898f-8d906a661f07
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 2ec8b5da9440c92e8f9d6702d5e5e20de952b588
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="prerequisites-for-azure-ad-connect"></a>Azure AD için Önkoşullar Bağlan
Bu konuda hello ön koşullar ve Azure AD Connect'i hello donanım gereksinimleri açıklanmaktadır.

## <a name="before-you-install-azure-ad-connect"></a>Azure AD Connect yüklemeden önce
Azure AD Connect yüklemeden önce gereken birkaç nokta vardır.

### <a name="azure-ad"></a>Azure AD
* Bir Azure aboneliği veya bir [Azure deneme aboneliği](https://azure.microsoft.com/pricing/free-trial/). Bu aboneliğin yalnızca olduğu hello Azure portalına erişmek için ve Azure AD Connect kullanmayan için gereklidir. Ardından PowerShell veya Office 365 kullanıyorsanız, bir Azure aboneliği toouse Azure AD Connect gerekmez. Bir Office 365 lisansınız varsa, hello Office 365 portalı de kullanabilirsiniz. Ücretli bir Office 365 lisansına sahip hello Office 365 portalından Azure portal ayrıca hello alabilirsiniz.
  * Merhaba de kullanabilirsiniz [Azure portal](https://portal.azure.com). Bu portalı bir Azure AD lisansı gerektirmez.
* [Merhaba etki ekleyin ve doğrulayın](../active-directory-domains-add-azure-portal.md) Azure AD'de toouse planlayın. Örneğin, kullanıcılarınız için toouse contoso.com planlama sonra emin olun, bu etki alanı doğrulandı ve hello contoso.onmicrosoft.com varsayılan etki alanı yalnızca kullanmıyorsanız.
* Azure AD kiracısı varsayılan 50 k nesneleriyle sağlar. Etki alanınızı doğrulayın hello sınırı artan too300k nesneleri olur. Daha sonra Azure AD'de daha da fazla nesneleri gerekiyorsa, bir destek servis talebi toohave hello sınırı daha artan tooopen gerekir. Sonra 500'den fazla k nesneleri gerekiyorsa, Office 365, Azure AD temel, Azure AD Premium veya Enterprise Mobility ve güvenlik gibi bir lisansınız olmalıdır.

### <a name="prepare-your-on-premises-data"></a>Şirket içi verilerinizi hazırlama
* Kullanım [Idfix](https://support.office.com/article/Install-and-run-the-Office-365-IdFix-tool-f4bd2439-3e41-4169-99f6-3fabdfa326ac) tooidentify hataları çoğaltmaları ve tooAzure AD ve Office 365 eşitlemeden önce dizininizde biçimlendirme sorunları gibi.
* Gözden geçirme [isteğe bağlı eşitleme özelliklerini Azure AD içinde etkinleştirebilir](active-directory-aadconnectsyncservice-features.md) ve etkinleştirmelisiniz hangi özelliklerin değerlendirin.

### <a name="on-premises-active-directory"></a>Şirket içi Active Directory
* Merhaba AD şema sürümü ve orman işlev düzeyi Windows Server 2003 veya üstü olmalıdır. Merhaba şema ve orman düzeyi gereksinimleri karşılandığında sürece hello etki alanı denetleyicileri herhangi bir sürümünü çalıştırabilirsiniz.
* Toouse hello özelliği planlıyorsanız **parola geri yazma**, hello etki alanı denetleyicileri (en son SP ile) Windows Server 2008 veya üzeri olması gerekir. (R2 öncesi) 2008'de, DC'lerin olan sonra da uygulamalısınız [düzeltme KB2386717](http://support.microsoft.com/kb/2386717).
* Azure AD tarafından kullanılan hello etki alanı denetleyicisi yazılabilir olmalıdır. Bu **desteklenmiyor** RODC (salt okunur etki alanı denetleyicisi) ve Azure AD Connect değil izleyin herhangi toouse yazma yeniden yönlendirir.
* Bu **desteklenmiyor** toouse şirket içi SLD'ler (tek etiketli etki alanları) kullanarak ormanlar/etki alanları.
* Bu **desteklenmiyor** toouse şirket içi "noktalı" kullanarak ormanlar/etki alanları (adı içeren bir süre ".") NetBIOS adları.
* Çok önerilen[hello Active Directory Geri Dönüşüm Kutusu'nu etkinleştirmek](active-directory-aadconnectsync-recycle-bin.md).

### <a name="azure-ad-connect-server"></a>Azure AD Connect sunucusu
* Azure AD Connect Small Business Server veya Windows Server Essentials yüklenemez. Merhaba sunucu Windows Server standard ya da daha iyi kullanmanız gerekir.
* Hello Azure AD Connect sunucusu tam GUI yüklü olması gerekir. Bu **desteklenmiyor** tooinstall sunucu çekirdeği üzerinde.
* Azure AD Connect, Windows Server 2008 veya sonraki sürümlerinde yüklenmelidir. Bu sunucu bir etki alanı denetleyicisi veya üye sunucu hızlı ayarları kullanarak olabilir. Özel ayarları kullanırsanız, hello sunucusu tek başına olabilir ve toobe birleştirilmiş tooa etki alanı yok.
* Windows Server 2008 veya Windows Server 2008 R2 üzerinde Azure AD Connect'i yüklemek emin tooapply hello en son düzeltmeler Windows Update'ten olun. Merhaba yüklemesi yüklenmemiş bir sunucuyla mümkün toostart değil.
* Toouse hello özelliği planlıyorsanız **parola eşitleme**, hello Azure AD Connect sunucusu Windows Server 2008 R2 SP1 veya üzeri olması gerekir.
* Toouse planlıyorsanız bir **Grup yönetilen hizmet hesabı**, hello Azure AD Connect sunucusu Windows Server 2012 veya üzeri olması gerekir.
* Hello Azure AD Connect sunucusu olmalıdır [.NET Framework 4.5.1](#component-prerequisites) veya üstü ve [Microsoft PowerShell 3.0](#component-prerequisites) veya sonraki bir sürümü yüklü.
* Hello Azure AD Connect sunucusu PowerShell Transcription Grup İlkesi etkin olmaması gerekir.
* Active Directory Federasyon Hizmetleri dağıtılmışsa, AD FS veya Web uygulaması proxy'si yüklendiği hello sunucuları Windows Server 2012 R2 olmalıdır veya sonraki bir sürümü. [Windows Uzaktan Yönetim](#windows-remote-management) bu sunuculara uzaktan yükleme için etkinleştirilmesi gerekir.
* Active Directory Federasyon Hizmetleri dağıtılmışsa, gereksinim duyduğunuz [SSL sertifikalarını](#ssl-certificate-requirements).
* Active Directory Federasyon Hizmetleri dağıtıldığından sonra tooconfigure gerek [ad çözümlemesi](#name-resolution-for-federation-servers).
* Genel Yöneticiler etkin MFA varsa, URL hello **https://secure.aadcdn.microsoftonline-p.com** hello Güvenilen siteler listesinde olmalıdır. İstendiğinde tooadd MFA testini ve onu istendiğinde bu site toohello Güvenilen siteler listesine önce eklenmedi olduğunuz. Internet Explorer tooadd kullanabilirsiniz, tooyour Güvenilen siteler.

### <a name="sql-server-used-by-azure-ad-connect"></a>Azure AD Connect tarafından kullanılan SQL Server
* Azure AD Connect bir SQL Server veritabanı toostore kimlik verilerini gerektirir. Varsayılan olarak, bir SQL Server 2012 Express LocalDB'nı (SQL Server Express açık bir sürüm) yüklenir. SQL Server Express toomanage yaklaşık 100.000 nesneler sağlayan bir 10 GB boyutu sınırı vardır. Toomanage directory nesnelerinin daha yüksek bir birimi gerekiyorsa, toopoint hello Yükleme Sihirbazı'nı tooa farklı SQL Server yüklemesi gerekir.
* Ayrı bir SQL Server kullanıyorsanız, bu gereksinimleri geçerlidir:
  * Azure AD Connect, SQL Server 2008 (en son hizmet paketiyle) tooSQL Server 2016 SP1'den Microsoft SQL Server'ın tüm özellikleri destekler. Microsoft Azure SQL veritabanı **desteklenmiyor** veritabanı olarak.
  * Büyük küçük harf duyarsız bir SQL harmanlaması kullanmanız gerekir. Bu harmanlamaları ile tanımlanan bir \_CI_ kendi adı. Bu **desteklenmiyor** tarafından tanımlanan toouse büyük küçük harfe duyarlı bir harmanlama \_CS_ kendi adı.
  * Bir eşitleme Altyapısı SQL örneği başına yalnızca olabilir. Bu **desteklenmiyor** tooshare bir SQL örneği FIM/MIM eşitleme, DirSync veya Azure AD eşitleme.

### <a name="accounts"></a>Hesaplar
* Hello Azure AD kiracısı Azure AD genel yönetici hesabı ile toointegrate istiyor. Bu hesap olmalıdır bir **okul veya kuruluş hesabı** ve olamaz bir **Microsoft hesabı**.
* Hızlı ayarları kullanın veya Dirsync'ten yükseltme, yerel Active Directory'nizi için bir kuruluş yöneticisi hesabı olması gerekir.
* [Active Directory'de hesapları](active-directory-aadconnect-accounts-permissions.md) hello özel ayarlarını yükleme yolunu kullanır.

### <a name="connectivity"></a>Bağlantı
* Hello Azure AD Connect sunucusu, hem intranet hem de Internet için DNS çözümlemesi gerekir. Merhaba DNS sunucu kurabilmelidir tooresolve adları hem tooyour şirket içi Active Directory ve hello Azure AD uç noktaları.
* Intranet üzerindeki güvenlik duvarları varsa ve hello Azure AD Connect sunucuları ve etki alanı denetleyicileri arasında tooopen bağlantı noktalarını gerekir, ardından bkz [Azure AD Connect bağlantı noktaları](active-directory-aadconnect-ports.md) daha fazla bilgi için.
* URL'leri erişilebilen, proxy veya güvenlik duvarı sınırınızı sonra hello varsa kısmında belgelenen URL'leri [Office 365 URL'leri ve IP adresi aralıkları](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2) açılması gerekir.
  * Kullanıyorsanız, Microsoft Cloud Almanya veya hello Microsoft Azure kamu bulut hello sonra bkz [Azure AD Connect eşitleme hizmeti örnekleri konuları](active-directory-aadconnect-instances.md) URL'ler için.
* Azure AD Connect, Azure AD ile TLS 1.0 toocommunicate kullanarak varsayılan olarak açıktır. Merhaba adımları izleyerek bu tooTLS 1.2 değiştirebilirsiniz [Azure AD Connect'i etkinleştirme TLS 1.2](#enable-tls-12-for-azure-ad-connect).
* Merhaba ayarında aşağıdaki toohello Internet bağlanmak için bir giden proxy kullanıyorsanız, hello **C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config** dosya hello Yükleme Sihirbazı eklenmesi gerekiyor ve Azure AD Connect eşitleme toobe mümkün tooconnect toohello Internet ve Azure AD. Bu metin hello hello dosya sonunda girilmesi gerekir. Bu kodda, &lt;PROXYADRESS&gt; hello gerçek proxy IP adresi veya ana bilgisayar adını temsil eder.

```
    <system.net>
        <defaultProxy>
            <proxy
            usesystemdefault="true"
            proxyaddress="http://<PROXYADDRESS>:<PROXYPORT>"
            bypassonlocal="true"
            />
        </defaultProxy>
    </system.net>
```

* Proxy sunucusu kimlik doğrulaması sonra hello gerektiriyorsa [hizmet hesabı](active-directory-aadconnect-accounts-permissions.md#azure-ad-connect-sync-service-account) bulunmalıdır hello etki alanı ve özelleştirilmiş hello ayarları yükleme yolu toospecify kullanmalısınız bir [özel hizmet hesabı](active-directory-aadconnect-get-started-custom.md#install-required-components). Ayrıca farklı değişiklik toomachine.config gerekir. Machine.config bu değişikliği ile hello Yükleme Sihirbazı'nı ve eşitleme altyapısı tooauthentication istekleri hello proxy sunucusundan yanıt. Merhaba hariç tüm Yükleme Sihirbazı sayfalarındaki **yapılandırma** sayfasında, kullanıcının hello imzalı kimlik bilgileri kullanılır. Merhaba üzerinde **yapılandırma** sayfasıdır hello Yükleme Sihirbazı, hello bağlam hello sonunda anahtarlı toohello [hizmet hesabı](active-directory-aadconnect-accounts-permissions.md#azure-ad-connect-sync-service-account) , tarafından oluşturulmuş. Merhaba machine.config bölümü aşağıdaki gibi görünmelidir.

```
    <system.net>
        <defaultProxy enabled="true" useDefaultCredentials="true">
            <proxy
            usesystemdefault="true"
            proxyaddress="http://<PROXYADDRESS>:<PROXYPORT>"
            bypassonlocal="true"
            />
        </defaultProxy>
    </system.net>
```

* Azure AD Connect dizin eşitlemesi bir parçası olarak bir web isteği tooAzure AD gönderdiğinde, Azure AD too5 dakika toorespond alabilir. Proxy sunucuları toohave bağlantı boşta kalma zaman aşımı yapılandırması için yaygın bir durumdur. Lütfen en az 6 dakika veya daha fazla tooat hello yapılandırma ayarlandığından emin olun.

Daha fazla bilgi için MSDN hello hakkında bkz [proxy öğesi varsayılan](https://msdn.microsoft.com/library/kd3cf2ex.aspx).  
Bağlantı sorunlarınız, daha fazla bilgi için bkz: [bağlantı sorunlarını giderme](active-directory-aadconnect-troubleshoot-connectivity.md).

### <a name="other"></a>Diğer
* İsteğe bağlı: Bir test kullanıcı hesabı tooverify eşitleme.

## <a name="component-prerequisites"></a>Bileşen önkoşulları
### <a name="powershell-and-net-framework"></a>PowerShell ve .net Framework
Azure AD Connect Microsoft PowerShell ve .NET Framework 4.5.1 bağlıdır. Bu sürüm veya sunucunuzda yüklü sonraki bir sürümü gerekir. Windows Server sürümüne bağlı olarak aşağıdaki hello:

* Windows Server 2012 R2
  * Microsoft PowerShell varsayılan olarak yüklenir. Hiçbir eylem gerekli değildir.
  * .NET framework 4.5.1 veya sonraki sürümlerinde Windows Update aracılığıyla sunulur. Merhaba Denetim Masası hello en son güncelleştirmeleri tooWindows sunucu yüklediğinizden emin olun.
* Windows Server 2008R2 ve Windows Server 2012
  * Microsoft PowerShell'in en son sürümünü Hello sağlanmıştır **Windows Management Framework 4.0**, kullanılabilir [Microsoft Download Center](http://www.microsoft.com/downloads).
  * .NET framework 4.5.1 ve sonraki sürümlerinde kullanılabilir [Microsoft Download Center](http://www.microsoft.com/downloads).
* Windows Server 2008
  * en son desteklenen hello PowerShell sürümüdür bulunan **Windows Management Framework 3.0**, kullanılabilir [Microsoft Download Center](http://www.microsoft.com/downloads).
  * .NET framework 4.5.1 ve sonraki sürümlerinde kullanılabilir [Microsoft Download Center](http://www.microsoft.com/downloads).

### <a name="enable-tls-12-for-azure-ad-connect"></a>Azure AD Connect için TLS 1.2 etkinleştir
Azure AD Connect, varsayılan olarak hello hello eşitleme altyapısı sunucusu ve Azure AD arasındaki iletişimi şifrelemek için TLS 1.0 kullanıyor. Bu, varsayılan olarak .net uygulamaları toouse TLS 1.2 hello sunucuda yapılandırarak değiştirebilirsiniz. TLS 1.2 hakkında daha fazla bilgi bulunabilir [Microsoft güvenlik önerisi 2960358](https://technet.microsoft.com/security/advisory/2960358).

1. Windows Server 2008'de TLS 1.2 etkinleştirilemez. Windows Server 2008R2 gerekir ya da daha sonra. İşletim sisteminiz için yüklü hello .net 4.5.1'in düzeltme Bkz emin [Microsoft güvenlik önerisi 2960358](https://technet.microsoft.com/security/advisory/2960358). Bu düzeltmeyi veya sonraki bir sürümü sunucunuz üzerinde zaten yüklü olabilir.
2. Windows Server 2008R2 kullanırsanız, TLS 1.2 etkin olduğundan emin olun. Windows Server 2012 sunucu ve sonraki sürümlerinde, TLS 1.2 zaten etkinleştirilmiş olmalıdır.
   ```
   [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2]
   [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client] "DisabledByDefault"=dword:00000000 "Enabled"=dword:00000001
   [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server] "DisabledByDefault"=dword:00000000 "Enabled"=dword:00000001
   ```
3. Tüm işletim sistemleri için bu kayıt defteri anahtarını ayarlayın ve hello sunucuyu yeniden başlatın.
   ```
   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319
   "SchUseStrongCrypto"=dword:00000001
   ```
4. Ayrıca tooenable TLS 1.2 hello eşitleme altyapısı sunucusu ve uzak bir SQL Server arasında istediğiniz sonra emin olun gerekli hello sürümleri için yüklü olan [Microsoft SQL Server için TLS 1.2 desteği](https://support.microsoft.com/kb/3135244).

## <a name="prerequisites-for-federation-installation-and-configuration"></a>Federasyon yükleme ve yapılandırma için Önkoşullar
### <a name="windows-remote-management"></a>Windows Uzaktan Yönetim
Azure AD Connect toodeploy Active Directory Federasyon Hizmetleri veya hello Web uygulaması Ara sunucusu kullanırken, bu gereksinimleri denetleyin:

* Merhaba hedef sunucunun etki alanına katılmış ise, sonra Windows Uzaktan yönetilen etkinleştirildiğinden emin olun
  * Yükseltilmiş bir PSH komut penceresinde komutunu kullanın`Enable-PSRemoting –force`
* Merhaba hedef sunucu ise WAP makine bir etki alanına katılmış sonra birkaç ek gereksinimler vardır
  * Merhaba hedef makinede (WAP makine):
    * Merhaba winrm emin olun (Windows Uzaktan Yönetimi / WS-Management) hizmetinin hello Hizmetler ek bileşeni çalıştığından
    * Yükseltilmiş bir PSH komut penceresinde komutunu kullanın`Enable-PSRemoting –force`
  * (Merhaba hedef makine etki alanına katılmış veya güvenilmeyen etki alanı varsa) hangi hello üzerinde Sihirbazı çalışıyor hello makinede:
    * Yükseltilmiş bir PSH komut penceresinde hello komutunu kullanın`Set-Item WSMan:\localhost\Client\TrustedHosts –Value <DMZServerFQDN> -Force –Concatenate`
    * Sunucu Yöneticisi'nde:
      * DMZ WAP konak toomachine havuzu ekleme (Sunucu Yöneticisi -> Yönet -> sunucuları Ekle... DNS sekmesini kullanın)
      * Sunucu Yöneticisi'ni tüm sunucuları sekmesi: WAP sunucuya sağ tıklayın ve Yönet as.. seçin, hello WAP makine için yerel (etki alanı değil) kimlik bilgilerini girin
      * toovalidate uzak PSH bağlantısı, Sunucu Yöneticisi'ni tüm sunucuları sekmesinde hello: WAP sunucuya sağ tıklayın ve Windows PowerShell'i seçin. Bir uzak PSH oturum açmalıdır tooensure uzak PowerShell oturumlarınızı kurulabileceği.

### <a name="ssl-certificate-requirements"></a>SSL sertifikası gereksinimleri
* Kesinlikle önerilir, AD FS grubunun tüm düğümleri ve tüm Web uygulaması Ara sunucusu toouse hello aynı SSL sertifikası.
* Merhaba sertifika bir X509 olmalıdır sertifika.
* Bir test laboratuvarı ortamında Federasyon sunucularında otomatik olarak imzalanan sertifika kullanabilirsiniz. Ancak, bir üretim ortamı için genel bir CA'dan hello sertifika elde öneririz.
  * Genel olarak güvenilir olmayan bir sertifika kullanıyorsanız, her Web uygulaması proxy'si sunucuda yüklü o hello sertifikanın her iki hello yerel sunucuya ve tüm federasyon sunucuları güvenilir olduğundan emin olun
* Merhaba sertifika Hello kimliğiyle hello Federasyon Hizmeti adı (örneğin, sts.contoso.com) eşleşmesi gerekir.
  * Merhaba kimliktir ya da bir konu alternatif adı (SAN) uzantısı türü dNSName veya SAN girdi yoksa hello konu adı olarak belirtilen bir ortak adı.  
  * Bunlardan birini hello Federasyon Hizmeti adıyla eşleşen sağlanan birden çok SAN girişleri hello sertifikasında mevcut olabilir.
  * Toouse çalışma alanına katılma planlıyorsanız, ek bir SAN hello değerle gereklidir **enterpriseregistration.** Kuruluşunuzun, örneğin, kullanıcı asıl adı (UPN) soneki Hello ardından **enterpriseregistration.contoso.com**.
* CryptoAPI İleri nesil (CNG) anahtarları ve anahtar depolama sağlayıcıları dayalı sertifikalar desteklenmez. Başka bir deyişle, bir CSP (şifreleme hizmeti sağlayıcısı) ve KSP'ye değil (anahtar depolama sağlayıcısı) dayalı bir sertifika kullanmanız gerekir.
* Joker karakteriyle sertifikalar desteklenir.

### <a name="name-resolution-for-federation-servers"></a>Federasyon sunucuları için ad çözümlemesi
* Hello için DNS kayıtlarını hello intranet (iç DNS sunucunuzun) hem de extranet hello (ortak DNS etki alanı kayıt yoluyla) için AD FS Federasyon Hizmeti adı (örneğin sts.contoso.com) ayarlayın. Merhaba intranet DNS kaydı için A kullandığınızdan emin olun ve CNAME kayıtlarını değil. Bu doğru makinenizden etki alanına katılmış windows kimlik doğrulaması toowork için gereklidir.
* Birden fazla AD FS sunucusunun veya Web uygulaması Ara sunucusu dağıtıyorsanız, yük dengeleyici yapılandırdıysanız ve yük dengeleyici hello DNS kayıtlarını hello AD FS Federasyon Hizmeti adı (örneğin sts.contoso.com) noktası toohello emin olun.
* Internet Explorer kullanarak, intranet tarayıcı uygulamaları için Windows tümleşik kimlik doğrulaması toowork için o hello AD FS Federasyon Hizmeti adı (örneğin sts.contoso.com) IE toohello intranet bölgesine eklenir emin olun. Bu denetlenebilir Grup İlkesi ve dağıtılan tooall aracılığıyla, etki alanına katılmamış bilgisayarlar.

## <a name="azure-ad-connect-supporting-components"></a>Azure AD Connect bileşenleri destekleme
Merhaba, Azure AD Connect Azure AD Connect yüklendiği hello sunucuya yüklenen bileşenlerin bir listesi verilmiştir. İçin temel bir Express yüklemesi listesidir. Toouse farklı bir SQL Server seçerseniz, Eşitleme Hizmetleri sayfası üzerinde hello yükleyin, sonra SQL Express LocalDB yerel olarak yüklü değil.

* Azure AD Connect Health
* Microsoft Online Services oturum açma Yardımcısı (hiçbir bağımlılığını ancak yüklenir) BT uzmanları için
* Microsoft SQL Server 2012 komut satırı yardımcı programları
* Microsoft SQL Server 2012 Express LocalDB
* Microsoft SQL Server 2012 Native Client
* Microsoft Visual C++ 2013 yeniden dağıtım paketi

## <a name="hardware-requirements-for-azure-ad-connect"></a>Azure AD Connect için donanım gereksinimleri
Merhaba tabloda hello Azure AD Connect eşitleme bilgisayar için en düşük gereksinimler hello gösterir.

| Active Directory içindeki nesneleri sayısı | CPU | Bellek | Sabit sürücü boyutu |
| --- | --- | --- | --- |
| 10. 000'den az |1.6 GHz |4 GB |70 GB |
| 10,000–50,000 |1.6 GHz |4 GB |70 GB |
| 50,000–100,000 |1.6 GHz |16 GB |100 GB |
| 100.000 ya da daha fazla nesneler için SQL Server'ın tam sürümünü hello gereklidir | | | |
| 100,000–300,000 |1.6 GHz |32 GB |300 GB |
| 300,000–600,000 |1.6 GHz |32 GB |450 GB |
| Birden fazla 600.000 |1.6 GHz |32 GB |500 GB |

AD FS çalıştıran bilgisayarlar için en düşük gereksinimleri hello veya Web uygulama sunucuları hello aşağıda verilmiştir:

* CPU: Çift çekirdek 1,6 GHz veya üzeri
* Bellek: 2 GB veya üzeri
* Azure VM: A2 yapılandırma veya üzeri

## <a name="next-steps"></a>Sonraki adımlar
[Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md) hakkında daha fazla bilgi edinin.
