---
title: aaaAzure Active Directory Connect sistem durumu ile ilgili SSS - Azure | Microsoft Docs
description: "Bu SSS, Azure AD Connect Health hakkında sorular yanıtlanmaktadır. Bu SSS faturalama modeli, özellikler, sınırlamalar ve Destek hello dahil hello hizmetini kullanma hakkında soruları kapsar."
services: active-directory
documentationcenter: 
author: billmath
manager: samueld
editor: curtand
ms.assetid: f1b851aa-54d7-4cb4-8f5c-60680e2ce866
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 3f15d9e9b557b09ef74ceff85806579dd51f2412
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-health-frequently-asked-questions"></a>Azure AD Connect Health hakkında sık sorulan sorular
Bu makale, Azure Active Directory (Azure AD) Connect Health hakkında sık sorulan soruların (FAQ) yanıtlar toofrequently içerir. Bu SSS nasıl toouse hello faturalama modeli, özellikler, sınırlamalar ve Destek hello içeren hizmet hakkındaki soruları kapsar.

## <a name="general-questions"></a>Genel sorular
**S: birden çok Azure AD dizinlerinden yönetin. Azure Active Directory Premium içeren toohello nasıl geçiş yapabilirim?**

farklı arasında tooswitch Azure AD kiracıları, select hello şu anda açan **kullanıcı adı** hello sağ üst köşesinde ve hello uygun hesabı seçin. Merhaba hesap buraya listelenmemişse seçin **oturumu**, ve ardından hello genel yönetici kimlik bilgilerini kullan Azure Active Directory Premium sahip hello dizininin içinde toosign etkin.

**S: hangi sürümünün kimlik rolleri Azure AD Connect Health tarafından destekleniyor mu?**

Merhaba aşağıdaki tabloda hello rolleri listeler ve desteklenen işletim sistemi sürümleri.

|Rol| İşletim sistemi / sürümü|
|--|--|
|Active Directory Federasyon Hizmetleri (AD FS)| <ul> <li> Windows Server 2008 R2 </li><li> Windows Server 2012  </li> <li>Windows Server 2012 R2 </li> <li> Windows Server 2016  </li> </ul>|
|Azure AD Connect | Sürüm 1.0.9125 veya üzeri|
|Active Directory etki alanı Hizmetleri (AD DS)| <ul> <li> Windows Server 2008 R2 </li><li> Windows Server 2012  </li> <li>Windows Server 2012 R2 </li> <li> Windows Server 2016  </li> </ul>|

Hello hizmeti tarafından sağlanan hello özellikleri farklı olabileceği Not hello rol ve hello işletim sistemine göre. Diğer bir deyişle, tüm hello özellikler tüm işletim sistemi sürümleri için kullanılabilir olmayabilir. Merhaba özellik açıklamalarını Ayrıntılar için bkz.

**S: kaç tane yapmak my altyapı toomonitor ihtiyacım?**

* Merhaba ilk Connect Health aracısını en az bir Azure AD Premium lisansı gerektirir.
* Her bir ek kayıtlı aracının 25 ek Azure AD Premium lisansı gerektirir.
* Aracı sayısı eşdeğer toohello toplam tüm izlenen rolleri arasında (AD FS, Azure AD Connect ve/veya AD DS) kayıtlı olan aracıları sayısıdır.

Lisans bilgilerini de hello üzerinde bulunan [Azure AD fiyatlandırma sayfası](https://aka.ms/aadpricing).

Örnek:

| Kayıtlı aracıları | Gerekli lisansları | Örnek izleme yapılandırması |
| ------ | --------------- | --- |
| 1 | 1 | 1 azure AD Connect sunucusu |
| 2 | 26| 1 azure AD Connect sunucusu ve 1 etki alanı denetleyicisi |
| 3 | 51 | 1 active Directory Federasyon Hizmetleri (AD FS) server, 1 AD FS proxy ve 1 etki alanı denetleyicisi |
| 4 | 76 | 1 AD FS sunucusu, 1 AD FS proxy ve 2 etki alanı denetleyicileri |
| 5 | 101 | 1 azure AD Connect sunucusu, 1 AD FS sunucusu, 1 AD FS proxy ve 2 etki alanı denetleyicileri |


## <a name="installation-questions"></a>Yükleme soruları

**S: tek başına sunucularda hello Azure AD Connect Health aracısını yükleme hello etkisi nedir?**

Yükleme hello Microsoft Azure AD Connect Health Aracısı, AD FS web uygulaması proxy sunucuları, Azure AD Connect (eşitleme) sunucuları, etki alanı denetleyicileri hello saygı toohello CPU, bellek kullanımı, ağ bant genişliği ve depolama ile en az etkisidir.

sayı aşağıdaki hello yaklaşık şunlardır:

* CPU tüketimi: % ~ 1-5 artırma.
* Bellek tüketimi: hello toplam sistem belleği too10%.

> [!NOTE]
> Merhaba Aracısı Azure ile iletişim kuramıyorsa hello aracı yerel olarak tanımlanmış bir üst sınır hello verilerini depolar. Merhaba Aracısı hello "önbelleğe alınan" verileri "yakın zamanda hizmet" olarak üzerine yazar.
>
>

* Azure AD Connect Health aracıları için yerel arabellek Depolama: ~ 20 MB.
* AD FS sunucuları için onu yazılmadan önce tüm hello denetim verilerini 1024 MB (1 GB) Azure AD Connect Health aracılarını tooprocess hello AD FS denetim kanalı için bir disk alanı sağlamak öneririz.

**S: tooreboot Sunucularım hello Azure AD Connect Health aracılarını hello yüklemesi sırasında sahibim?**

Hayır. Merhaba aracıları Hello yüklemesini tooreboot hello sunucunuz gerektirmez. Ancak, bazı adımlar yüklemesini hello server'ın bir yeniden başlatma gerektirebilir.

Örneğin, Windows Server 2008 R2'de .NET Framework 4.5 yüklemesi bir sunucu yeniden başlatma gerekiyor.

**S: Azure AD Connect Health iş doğrudan bir HTTP proxy üzerinden mi?**

Evet. Devam eden işlemler için bir HTTP proxy tooforward giden HTTP isteklerini hello sistem durumu aracısı toouse yapılandırabilirsiniz.
Daha fazla bilgi edinin [Health aracılarını HTTP proxy'sini yapılandırma](active-directory-aadconnect-health-agent-install.md#configure-azure-ad-connect-health-agents-to-use-http-proxy).

Aracı kaydı sırasında tooconfigure bir proxy sunucu gerekiyorsa, Internet Explorer Proxy ayarlarınızı toomodify önceden gerekebilir.

1. Internet Explorer'ı Aç > **ayarları** > **Internet Seçenekleri** > **bağlantıları** > **LAN Ayarları**.
2. Seçin **AĞINIZ için bir Proxy sunucusu kullan**.
3. Seçin **Gelişmiş** HTTP ve HTTPS/güvenli için farklı bir proxy bağlantı noktası varsa.

**S: Azure AD Connect Health destek temel kimlik doğrulama tooHTTP proxy'leri bağlanırken mu?**

Hayır. Bir mekanizma toospecify bir isteğe bağlı bir kullanıcı adı ve parola temel kimlik doğrulaması için şu anda desteklenmiyor.

**S: güvenlik duvarı bağlantı noktalarının ne hello Azure AD Connect Health Aracısı toowork için tooopen ihtiyacım?**

Merhaba bkz [gereksinimleri bölümüne](active-directory-aadconnect-health-agent-install.md#requirements) hello listesi güvenlik duvarı bağlantı noktaları ve diğer bağlantı gereksinimleri için.

**Merhaba hello Azure AD Connect Health Portalı'ndaki adı aynı olan iki sunucu neden görüyor musunuz?**

Bir sunucudan bir aracıyı kaldırdığınızda, hello sunucu hello Azure AD Connect Health Portalı'ndan otomatik olarak kaldırılmaz. El ile bir sunucudan bir aracı kaldırma veya hello sunucusunun kendisi kaldırırsanız, toomanually delete hello sunucu girdisini hello Azure AD Connect Health Portalı'ndan gerekir.

Bir sunucu görüntüsünü yeniden oluşturmak veya yeni bir sunucu ile Merhaba aynı ayrıntıları (örneğin, makine adı) oluşturma olabilir. Hello Azure AD Connect Health Portalı'ndan hello zaten kayıtlı sunucu kaldırmadı ve hello Aracısı hello yeni sunucuda yüklü, hello içeren iki girişleri görebilirsiniz aynı adı.

Bu durumda, toohello daha eski bir sunucuya ait hello girdisini el ile silin. Bu sunucu için Hello veriler güncel olmalıdır.

## <a name="health-agent-registration-and-data-freshness"></a>Sistem Durumu Aracısı kaydı ve veri yenilik

**S: hello sistem durumu aracısı kayıt hataları yaygın nedenler nelerdir ve sorunları nasıl giderebilirim?**

Merhaba sistem durumu aracısı tooregister toohello aşağıdaki nedeniyle başarısız olabilir olası nedenler:

* bir güvenlik duvarı trafiği engelleyen çünkü hello Aracısı gerekli hello uç ile iletişim kuramıyor. Bu, özellikle web uygulama proxy sunucularında yaygındır. Giden iletişim gerekli toohello uç noktaları ve bağlantı noktaları izin verdiğiniz emin olun. Merhaba bkz [gereksinimleri bölümüne](active-directory-aadconnect-health-agent-install.md#requirements) Ayrıntılar için.
* Giden iletişim tabi tooan SSL denetlemesi hello ağ katmanı tarafından önemlidir. Bu hello denetleme sunucu/varlık tarafından değiştirilen toobe hello Aracısı kullanır ve hello adımları toocomplete hello aracı kaydı başarısız hello sertifika neden olur.
* Merhaba kullanıcı erişimi tooperform hello kayıt hello aracısı yok. Genel Yöneticiler, varsayılan olarak erişimi. Kullanabileceğiniz [rol tabanlı erişim denetimi](active-directory-aadconnect-health-operations.md#manage-access-with-role-based-access-control) toodelegate erişim tooother kullanıcıları.

**S: "sistem sağlığı hizmeti verileri toodate olmadığını." uyarı Merhaba sorun giderme nasıl?**

Azure AD Connect Health, tüm hello veri noktaları hello hello sunucudan son iki saat almadığında hello uyarı oluşturur. Bu uyarı için birden çok nedeni olabilir.

* bir güvenlik duvarı trafiği engelleyen çünkü hello Aracısı gerekli hello uç ile iletişim kuramıyor. Bu, özellikle web uygulama proxy sunucularında yaygındır. Giden iletişim gerekli toohello bitiş noktalarını ve bağlantı noktaları izin verdiğiniz emin olun. Merhaba bkz [gereksinimleri bölümüne](active-directory-aadconnect-health-agent-install.md#requirements) Ayrıntılar için.
* Giden iletişim tabi tooan SSL denetlemesi hello ağ katmanı tarafından önemlidir. Bu hello denetleme sunucu/varlık tarafından değiştirilen toobe hello Aracısı kullanır ve tooupload veri toohello Azure AD Connect Health hizmeti hello işlemi başarısız hello sertifika neden olur.
* Merhaba Aracısı yerleşik hello bağlantı komutunu kullanabilirsiniz. [Daha fazla bilgi](active-directory-aadconnect-health-agent-install.md#test-connectivity-to-azure-ad-connect-health-service).
* Merhaba aracıları Ayrıca kimliği doğrulanmamış bir HTTP Proxy üzerinden giden bağlantıyı destekler. [Daha fazla bilgi](active-directory-aadconnect-health-agent-install.md##configure-azure-ad-connect-health-agents-to-use-http-proxy).

## <a name="operations-questions"></a>Operations sorular
**S: Merhaba web uygulaması proxy sunucuları üzerinde denetim tooenable gerekiyor?**

Hayır, Denetim hello web uygulaması proxy sunucuları üzerinde etkin toobe gerekmez.

**S: nasıl Azure AD Connect Health uyarıları çözülmesi?**

Azure AD Connect Health uyarıları, bir başarı koşulu çözülmüş. Azure AD Connect Health aracılarını algılamak ve hello başarı koşullar toohello hizmeti düzenli aralıklarla rapor. Birkaç uyarılar için zamana dayalı hello gizleme. Merhaba aynı hata koşulu uyarı oluşturma 72 saat içinde gözlenir değil, diğer bir deyişle, hello uyarı otomatik olarak çözümlenir.

**S: "Test kimlik doğrulama isteği (yapay işlem) tooobtain bir belirteç başarısız olduğunu." uyarı Merhaba sorun giderme nasıl?**

Sistem Durumu Aracısı hello tarafından başlatılan yapay bir işlem bir parçası olarak tooobtain bir belirteç Hello sistem durumu aracısı bir AD FS sunucusunda yüklü başarısız olduğunda azure AD Connect Health AD FS için bu uyarı oluşturur. Merhaba sistem durumu aracısı hello yerel sistem bağlamında kullanır ve kendi kendine bağlı olan taraf için bir belirteç tooget çalışır. AD FS belirteç, bir durumda bir catch tüm test tooensure budur.

En sık Hello sistem durumu aracısı yüklenemiyor tooresolve hello AD FS grup adı olduğundan bu sınama başarısız olur. Bu durum bir ağ yük dengeleyici hello AD FS sunucuları varsa ve bu hello isteği hello yük dengeleyicinin arkasına (önündeki hello yük dengeleyicinin karşılıklı tooa normal istemci olarak) olan bir düğümün başlatıldığına meydana gelebilir. Bu hello "ana" dosyasını "C:\Windows\System32\drivers\etc" tooinclude hello hello AD FS sunucusunun IP adresi veya bir geri döngü IP adresi (127.0.0.1) altında bulunan güncelleştirerek hello AD FS grubu adı (örneğin, sts.contoso.com) için düzeltilebilir. Ekleme hello ana bilgisayar dosyası hello ağ çağrısı, böylece hello sistem durumu aracısı tooget hello belirteci sağlar kısa devre oluşturur.

**S: my makineler için son ransomeware saldırıları hello düzeltme değil belirten bir e-posta aldı. Bu e-posta neden aldınız mı?**

Azure AD Connect Health hizmeti tooensure hello gerekli düzeltme eklerini izler makinelere yüklenen tüm hello taraması. en az bir makine hello kritik yazılım düzeltme eklerini değilse toohello Kiracı Yöneticiler hello e-posta gönderildi. Merhaba mantığı kullanılan toomake bu belirlemeyi oluştu.
1. Merhaba makinede yüklü tüm hello düzeltmeleri bulun.
2. Merhaba düzeltmeleri hello gelen en az biri listesi tanımlanmışsa onay yok.
3. Yanıt Evet ise, hello makine korunuyor. Aksi durumda, risk hello saldırı hello makinesidir.

Bu denetimi el ile aşağıdaki PowerShell komut dosyası tooperform hello kullanabilirsiniz. Merhaba mantığı yukarıda uygular.

```
Function CheckForMS17-010 ()
{
    $hotfixes = "KB3205409", "KB3210720", "KB3210721", "KB3212646", "KB3213986", "KB4012212", "KB4012213", "KB4012214", "KB4012215", "KB4012216", "KB4012217", "KB4012218", "KB4012220", "KB4012598", "KB4012606", "KB4013198", "KB4013389", "KB4013429", "KB4015217", "KB4015438", "KB4015546", "KB4015547", "KB4015548", "KB4015549", "KB4015550", "KB4015551", "KB4015552", "KB4015553", "KB4015554", "KB4016635", "KB4019213", "KB4019214", "KB4019215", "KB4019216", "KB4019263", "KB4019264", "KB4019472", "KB4015221", "KB4019474", "KB4015219", "KB4019473"

    #checks hello computer it's run on if any of hello listed hotfixes are present
    $hotfix = Get-HotFix -ComputerName $env:computername | Where-Object {$hotfixes -contains $_.HotfixID} | Select-Object -property "HotFixID"

    #confirms whether hotfix is found or not
    if (Get-HotFix | Where-Object {$hotfixes -contains $_.HotfixID})
    {
        "Found HotFix: " + $hotfix.HotFixID
    } else {
        "Didn't Find HotFix"
    }
}

CheckForMS17-010

```



## <a name="related-links"></a>İlgili bağlantılar
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Azure AD Connect Health Aracısı yüklemesi](active-directory-aadconnect-health-agent-install.md)
* [Azure AD Connect Health işlemleri](active-directory-aadconnect-health-operations.md)
* [Azure AD Connect Health'i AD FS ile Kullanma](active-directory-aadconnect-health-adfs.md)
* [Eşitleme için Azure AD Connect Health'i kullanma](active-directory-aadconnect-health-sync.md)
* [Azure AD Connect Health'i AD DS ile Kullanma](active-directory-aadconnect-health-adds.md)
* [Azure AD Connect Health sürüm geçmişi](active-directory-aadconnect-health-version-history.md)
