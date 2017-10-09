---
title: "aaaTroubleshoot Azure noktası site bağlantısı sorunlarını giderme | Microsoft Docs"
description: "Bilgi nasıl tootroubleshoot noktadan siteye bağlantı sorunları."
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/23/2017
ms.author: genli
ms.openlocfilehash: 98d66074be62ad8c7153a903f69cb0d01f988cd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-point-to-site-connection-problems"></a>Giderme: Azure noktadan siteye bağlantı sorunlarını

Bu makalede karşılaşabileceğiniz genel noktadan siteye bağlantı sorunları listeler. Ayrıca bu sorunlar için olası nedenler ve çözümler açıklanmaktadır.

## <a name="vpn-client-error-a-certificate-could-not-be-found"></a>VPN istemci hatası: bir sertifika bulunamadı

### <a name="symptom"></a>Belirti

Hello VPN istemcisi kullanarak tooconnect tooan Azure sanal ağı çalıştığınızda hello aşağıdaki hata iletisini alıyorsunuz:

**Bu Genişletilebilir kimlik doğrulama protokolü ile kullanılabilir bir sertifika bulunamadı. (Hata 798)**

### <a name="cause"></a>Nedeni

Merhaba istemci sertifikası eksik Bu sorun oluşur **Sertifikalar - Geçerli User\Personal\Certificates**.

### <a name="solution"></a>Çözüm

Bu hello istemci sertifikası (Certmgr.msc) hello sertifika deposunun konumu aşağıdaki hello yüklü olduğundan emin olun:
 
**Sertifikalar - Geçerli User\Personal\Certificates**

Nasıl tooinstall hello istemci sertifikası hakkında daha fazla bilgi için bkz: [noktadan siteye bağlantıları için oluşturma ve verme sertifikaları](vpn-gateway-certificates-point-to-site.md).

> [!NOTE]
> Merhaba istemci sertifikasını içeri aktardığınızda hello seçmeyin **güçlü özel anahtar korumasını etkinleştir** seçeneği.

## <a name="vpn-client-error-hello-message-received-was-unexpected-or-badly-formatted"></a>VPN istemci hatası: beklenmeyen veya hatalı biçimlendirilmiş hello ileti alındı

### <a name="symptom"></a>Belirti

Hello VPN istemcisi kullanarak tooconnect tooan Azure sanal ağı çalıştığınızda hello aşağıdaki hata iletisini alıyorsunuz:

**beklenmeyen veya hatalı biçimlendirilmiş hello iletisi alındı. (Hata 0x80090326)**

### <a name="cause"></a>Nedeni

Merhaba kök sertifika genel anahtarı hello Azure VPN ağ geçidine yüklenmemiştir Bu sorun oluşur. Başlangıç anahtarı bozuk veya süresi dolmuş da oluşabilir.

### <a name="solution"></a>Çözüm

Bu sorun, hello kök hello durumunu kontrol sertifika hello Azure portal toosee iptal edildi olup olmadığını tooresolve. Bunu iptal edilmediğini, toodelete hello kök sertifikasını ve reupload deneyin. Daha fazla bilgi için bkz: [oluşturma sertifikaları](vpn-gateway-howto-point-to-site-classic-azure-portal.md#generatecerts).

## <a name="vpn-client-error-a-certificate-chain-processed-but-terminated"></a>VPN istemci hatası: bir sertifika zinciri işlendi, ancak sona erdi 

### <a name="symptom"></a>Belirti 

Hello VPN istemcisi kullanarak tooconnect tooan Azure sanal ağı çalıştığınızda hello aşağıdaki hata iletisini alıyorsunuz:

**Bir sertifika zinciri işlendi, ancak hello güven sağlayıcısı tarafından güvenilmeyen bir kök sertifika sona erdi.**

### <a name="solution"></a>Çözüm

1. Sertifika aşağıdaki o hello hello doğru konumda olduğundan emin olun:

    | Sertifika | Konum |
    | ------------- | ------------- |
    | AzureClient.pfx  | Geçerli User\Personal\Certificates |
    | Azuregateway -*GUID*. cloudapp.net  | Geçerli User\Trusted kök sertifika yetkilileri|
    | AzureGateway -*GUID*. cloudapp.net, AzureRoot.cer    | Yerel bilgisayar/güvenilen kök sertifika yetkilileri|

2. Merhaba sertifikaları hello konumda zaten varsa, toodelete hello sertifikaları deneyin ve yeniden yükleyin. Merhaba  **azuregateway -*GUID*. hello Azure portal ' yüklenen hello VPN istemcisi yapılandırma paketini cloudapp.net** sertifika konusu. Dosya archivers tooextract hello dosyaları hello paketten kullanabilirsiniz.

## <a name="file-download-error-target-uri-is-not-specified"></a>Dosya indirme hatası: hedef URI belirtilmedi

### <a name="symptom"></a>Belirti

Merhaba aşağıdaki hata iletisini alıyorsunuz:

**Dosya indirme hatası. Hedef URI belirtilmedi.**

### <a name="cause"></a>Nedeni 

Bu sorun bir hatalı ağ geçidi türü nedeniyle oluşur. 

### <a name="solution"></a>Çözüm

Merhaba VPN ağ geçidi türü olmalıdır **VPN**, ve hello VPN türü olmalıdır **RouteBased**.

## <a name="vpn-client-error-azure-vpn-custom-script-failed"></a>VPN istemci hatası: Azure VPN özel komut başarısız oldu 

### <a name="symptom"></a>Belirti

Hello VPN istemcisi kullanarak tooconnect tooan Azure sanal ağı çalıştığınızda hello aşağıdaki hata iletisini alıyorsunuz:

**Özel bir komut dosyası (tooupdate, yönlendirme tablosu) başarısız oldu. (Hata 8007026f)**

### <a name="cause"></a>Nedeni

Kısayol kullanarak tooopen hello site noktası VPN bağlantısı çalışıyorsanız, bu sorun ortaya çıkabilir.

### <a name="solution"></a>Çözüm 

Merhaba kısayoldan açmadan yerine doğrudan hello VPN paketini açın.

## <a name="cannot-install-hello-vpn-client"></a>Merhaba VPN istemcisi yüklenemiyor

### <a name="cause"></a>Nedeni 

Sanal ağınız için gerekli tootrust hello VPN ağ geçidi bir ek sertifikadır. Merhaba sertifika hello Azure portal ' oluşturulan hello VPN istemcisi yapılandırma paketini dahil edilir.

### <a name="solution"></a>Çözüm

Merhaba VPN istemcisi yapılandırma paketini ayıklayın ve hello .cer dosyasını bulun. tooinstall hello sertifika, aşağıdaki adımları izleyin:

1. MMC.exe açın.
2. Merhaba eklemek **sertifikaları** ek bileşenini.
3. Select hello **bilgisayar** hesap hello yerel bilgisayar için.
4. Sağ hello **güvenilen kök sertifika yetkilileri** düğümü. Tıklatın **tüm görev** > **alma**ve hello VPN istemci yapılandırma paketi ayıkladığınız gözatma toohello .cer dosyası.
5. Merhaba bilgisayarı yeniden başlatın. 
6. Tooinstall hello VPN istemcisi deneyin.

## <a name="azure-portal-error-failed-toosave-hello-vpn-gateway-and-hello-data-is-invalid"></a>Azure portal hata: toosave hello VPN ağ geçidi başarısız oldu ve hello verileri geçersiz

### <a name="symptom"></a>Belirti

Hello Azure portal hello VPN ağ geçidi için toosave hello değişiklikleri çalıştığınızda hello aşağıdaki hata iletisini alıyorsunuz:

**Başarısız toosave sanal ağ geçidi &lt;* ağ geçidi adı*&gt;. Sertifikasının verileri &lt; *kimliği sertifika* &gt; olan invalid.* *

### <a name="cause"></a>Nedeni 

Yüklediğiniz hello kök sertifikanın ortak anahtarı bir alanı gibi geçersiz bir karakter içeriyorsa, bu sorun ortaya çıkabilir.

### <a name="solution"></a>Çözüm

Merhaba sertifikada Hello veri satır sonları (satır başı) gibi geçersiz karakterler içermediğinden emin olun. Merhaba tüm değer uzun bir satır olması gerekir. metin aşağıdaki hello hello sertifika örneğidir:

    -----BEGIN CERTIFICATE-----
    MIIC5zCCAc+gAwIBAgIQFSwsLuUrCIdHwI3hzJbdBjANBgkqhkiG9w0BAQsFADAW
    MRQwEgYDVQQDDAtQMlNSb290Q2VydDAeFw0xNzA2MTUwMjU4NDZaFw0xODA2MTUw
    MzE4NDZaMBYxFDASBgNVBAMMC1AyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEF
    AAOCAQ8AMIIBCgKCAQEAz8QUCWCxxxTrxF5yc5uUpL/bzwC5zZ804ltB1NpPa/PI
    sa5uwLw/YFb8XG/JCWxUJpUzS/kHUKFluqkY80U+fAmRmTEMq5wcaMhp3wRfeq+1
    G9OPBNTyqpnHe+i54QAnj1DjsHXXNL4AL1N8/TSzYTm7dkiq+EAIyRRMrZlYwije
    407ChxIp0stB84MtMShhyoSm2hgl+3zfwuaGXoJQwWiXh715kMHVTSj9zFechYd7
    5OLltoRRDyyxsf0qweTFKIgFj13Hn/bq/UJG3AcyQNvlCv1HwQnXO+hckVBB29wE
    sF8QSYk2MMGimPDYYt4ZM5tmYLxxxvGmrGhc+HWXzMeQIDAQABozEwLzAOBgNVHQ8B
    Af8EBAMCAgQwHQYDVR0OBBYEFBE9zZWhQftVLBQNATC/LHLvMb0OMA0GCSqGSIb3
    DQEBCwUAA4IBAQB7k0ySFUQu72sfj3BdNxrXSyOT4L2rADLhxxxiK0U6gHUF6eWz
    /0h6y4mNkg3NgLT3j/WclqzHXZruhWAXSF+VbAGkwcKA99xGWOcUJ+vKVYL/kDja
    gaZrxHlhTYVVmwn4F7DWhteFqhzZ89/W9Mv6p180AimF96qDU8Ez8t860HQaFkU6
    2Nw9ZMsGkvLePZZi78yVBDCWMogBMhrRVXG/xQkBajgvL5syLwFBo2kWGdC+wyWY
    U/Z+EK9UuHnn3Hkq/vXEzRVsYuaxchta0X2UNRzRq+o706l+iyLTpe6fnvW6ilOi
    e8Jcej7mzunzyjz4chN0/WVF94MtxbUkLkqP
    -----END CERTIFICATE-----

## <a name="azure-portal-error-failed-toosave-hello-vpn-gateway-and-hello-resource-name-is-invalid"></a>Azure portal hata: toosave hello VPN ağ geçidi başarısız oldu ve hello kaynak adı geçersiz

### <a name="symptom"></a>Belirti

Hello Azure portal hello VPN ağ geçidi için toosave hello değişiklikleri çalıştığınızda hello aşağıdaki hata iletisini alıyorsunuz: 

**Başarısız toosave sanal ağ geçidi &lt;* ağ geçidi adı*&gt;. Kaynak adı &lt; *tooupload deneyin sertifika adı* &gt; geçersiz ** değil.

### <a name="cause"></a>Nedeni

Merhaba sertifikanın Hello adı bir boşluk gibi geçersiz bir karakter içerdiğinden bu sorun oluşur. 

## <a name="azure-portal-error-vpn-package-file-download-error-503"></a>Azure portal hata: VPN paket dosyasını indirme hatası 503

### <a name="symptom"></a>Belirti

Toodownload hello VPN istemcisi yapılandırma paketini çalıştığınızda hello aşağıdaki hata iletisini alıyorsunuz:

**Toodownload hello dosyası açılamadı. Hata ayrıntıları: 503 hatası. Merhaba sunucu meşgul.**
 
### <a name="solution"></a>Çözüm

Bu hata geçici bir ağ sorunu neden olabilir. Toodownload hello VPN paketi birkaç dakika sonra yeniden deneyin.

## <a name="azure-vpn-gateway-upgrade-all-p2s-clients-are-unable-tooconnect"></a>Azure VPN ağ geçidi yükseltme: tüm P2S istemcileridir oluşturulamıyor tooconnect

### <a name="cause"></a>Nedeni

Merhaba sertifika yüzde 50'den fazla ise yaşam hello sertifika alındı.

### <a name="solution"></a>Çözüm

tooresolve bu sorunu oluşturun ve yeni sertifikalar toohello VPN istemcileri yeniden dağıtabilirsiniz. 

## <a name="too-many-vpn-clients-connected-at-once"></a>Çok fazla VPN istemcileri aynı anda bağlı

Her VPN ağ geçidi için hello en fazla izin verilen bağlantı sayısı 128'dir. Hello Azure portal'ın bağlanan istemcilerin toplam sayısı hello görebilirsiniz.

## <a name="point-to-site-vpn-incorrectly-adds-a-route-for-100008-toohello-route-table"></a>Noktadan siteye VPN yanlış 10.0.0.0/8 toohello yol tablosu için bir yol ekler

### <a name="symptom"></a>Belirti

Merhaba hello noktadan siteye istemci VPN bağlantısıyla çevirdiğinizde hello VPN istemcisi hello Azure sanal ağı doğru bir yol eklemeniz gerekir. Merhaba IP yardımcı hizmeti hello alt hello VPN istemcileri için bir rota eklemeniz gerekir. 

Merhaba VPN istemci aralığı 10.0.12.0/24 gibi 10.0.0.0/8 tooa daha küçük alt aittir. 10.0.12.0/24 için bir yol yerine, daha yüksek önceliğe sahip 10.0.0.0/8 için bir rota eklenir. 

Bu yanlış yol tanımlanan belirli bir yolu olmayan tooanother alt 10.50.0.0/24 gibi hello 10.0.0.0/8 aralıkta ait diğer şirket içi ağlar ile bağlantısını keser. 

### <a name="cause"></a>Nedeni

Bu davranış, Windows istemcileri için tasarım gereğidir. Hello istemci hello PPP IPCP protokol kullandığında, hello hello tünel arabirimi için IP adresi (Merhaba VPN ağ geçidi bu durumda) hello sunucusundan alır. Ancak, hello protokolünde bir sınırlama nedeniyle hello alt ağ maskesi hello istemci sahip değil. Başka bir şekilde tooget olduğundan, hello istemci tooguess hello alt ağ maskesi hello tünel arabirimi IP adresi hello sınıfına göre çalışır. 

Bu nedenle, bir yol statik eşleme aşağıdaki hello göre eklenir: 

Adres tooclass A aitse--> /8 Uygula

Adres aitse B--> tooclass /16 Uygula

Adres aitse C--> tooclass /24 Uygula

## <a name="vpn-client-cannot-access-network-file-shares"></a>VPN istemcisi ağ dosya paylaşımlarına erişemez

### <a name="symptom"></a>Belirti

Merhaba VPN istemci toohello Azure sanal ağı bağlandı. Ancak, hello istemci ağ paylaşımlarına erişemez.

### <a name="cause"></a>Nedeni

Merhaba SMB protokolü dosya paylaşımı erişimi için kullanılır. Hello bağlantısı başlatıldığında hello VPN istemcisi hello oturum bilgilerini ekler ve hello hatası oluşur. Merhaba bağlantı kurulduktan sonra hello istemci toouse hello kimlik bilgilerini önbelleğe Kerberos kimlik doğrulaması zorlanır. Bu işlem sorguları toohello Anahtar Dağıtım Merkezi (bir etki alanı denetleyicisi) tooget bir belirteç başlatır. Merhaba istemci Internet hello bağlandığından, mümkün tooreach hello etki alanı denetleyicisi olmayabilir. Bu nedenle, hello istemci üzerinden Kerberos tooNTLM kapatamazsınız. 

Merhaba hello istemci için geçerli bir sertifika sahip olduğunda bir kimlik bilgisi sorulup yalnızca zaman (SAN ile UPN =) birleştirilmiş hello etki alanı toowhich tarafından verilmiş. Merhaba istemci ayrıca fiziksel olarak bağlı toohello etki alanı ağında olmalıdır. Bu durumda, hello istemci toouse hello sertifika dener ve toohello etki alanı denetleyicisi ulaşır. Ardından hello anahtar dağıtım merkezi bir "KDC_ERR_C_PRINCIPAL_UNKNOWN" hatası döndürür. Merhaba zorlanmış toofail tooNTLM istemcidir. 

### <a name="solution"></a>Çözüm

toowork hello soruna geçici bir çözüm hello hello kayıt defteri alt anahtarını aşağıdaki etki alanı kimlik bilgilerini önbelleğe almayı devre dışı bırakın: 

    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\DisableDomainCreds - Set hello value too1 


## <a name="cannot-find-hello-point-to-site-vpn-connection-in-windows-after-reinstalling-hello-vpn-client"></a>Merhaba VPN istemcisi yeniden yükledikten sonra Windows Hello noktadan siteye VPN bağlantısı bulunamadı.

### <a name="symptom"></a>Belirti

Merhaba noktadan siteye VPN bağlantısını kaldırın ve hello VPN istemcisini yeniden yükleyin. Bu durumda, hello VPN bağlantısı başarıyla yapılandırılmadı. Merhaba hello VPN bağlantısının görüyor musunuz **ağ bağlantıları** Windows ayarları.

### <a name="solution"></a>Çözüm

tooresolve hello sorunu delete hello eski VPN istemci yapılandırma dosyalarından **C:\Users\TheUserName\AppData\Roaming\Microsoft\Network\Connections**, ve hello VPN istemci yükleyiciyi yeniden çalıştırın.
