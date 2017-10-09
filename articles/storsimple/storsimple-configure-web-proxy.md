---
title: "StorSimple cihazı için web Ara sunucusu kurma aaaSet | Microsoft Docs"
description: "Bilgi edinmek için StorSimple tooconfigure toouse Windows PowerShell web StorSimple cihazınız için proxy ayarları nasıl."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 6c2ca351-a7c6-4da6-ab5e-c081e6d08261
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: c0213eb2a1902ff994147bb16593f0ff300eb70c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-proxy-for-your-storsimple-device"></a>StorSimple cihazınız için Web Proxy'yi Yapılandır
## <a name="overview"></a>Genel Bakış
Bu öğretici açıklar nasıl toouse Windows PowerShell StorSimple tooconfigure ve görünüm için web proxy ayarlarını StorSimple cihazınız için. Hello web proxy ayarları hello bulut ile iletişim kurarken hello StorSimple cihaz tarafından kullanılır. Web proxy sunucusu kullanılan tooadd olan başka bir güvenlik katmanı, filtre içerik, tooease bant genişliği gereksinimlerini önbelleğe veya bile, analytics ile Yardım.

Web proxy, StorSimple cihazınız için isteğe bağlı bir yapılandırmadır. StorSimple için Windows PowerShell aracılığıyla yalnızca web sunucusu yapılandırabilir. başlangıç yapılandırmasını iki adımlı bir işlem aşağıdaki gibidir:

1. İlk StorSimple cmdlet'leri hello Kurulum Sihirbazı'nı veya Windows PowerShell aracılığıyla web proxy ayarlarını yapılandırın.
2. Ardından, Itanium tabanlı sistemler için yapılandırılmış hello web proxy ayarları Windows PowerShell aracılığıyla StorSimple cmdlet'leri de etkinleştirin.

Hello web proxy yapılandırması tamamlandıktan sonra yapılandırılmış hello web proxy ayarlarını hem hello Microsoft Azure StorSimple Yöneticisi hizmeti hem de hello Windows PowerShell için StorSimple görüntüleyebilirsiniz. 

Bu öğretici okuduktan sonra aşağıdakileri gerçekleştirebilirsiniz:

* Kurulum Sihirbazı'nı ve cmdlet'lerini kullanarak Web Proxy'yi Yapılandır
* Cmdlet'lerini kullanarak Web ara sunucusunu etkinleştirme
* Web proxy ayarları hello Klasik Azure portalında görüntüleyin
* Web proxy yapılandırması sırasında hatalarında sorun giderme

## <a name="configure-web-proxy-via-windows-powershell-for-storsimple"></a>StorSimple için Windows PowerShell aracılığıyla Web Proxy'yi Yapılandır
Tooconfigure web proxy ayarları aşağıdaki hello birini kullanın:

* Kurulum Sihirbazı'nı tooguide sizi hello yapılandırma adımlarına.
* StorSimple için Windows PowerShell cmdlet'leri.

Bu yöntemlerin her biri hello aşağıdaki bölümlerde ele alınmıştır.

## <a name="configure-web-proxy-via-hello-setup-wizard"></a>Merhaba Kurulum Sihirbazı aracılığıyla Web Proxy'yi Yapılandır
İçin web proxy yapılandırması hello Kurulum Sihirbazı'nı tooguide hello size adımları kullanabilirsiniz. Adımları tooconfigure web proxy aygıtınızda aşağıdaki hello gerçekleştirin.

#### <a name="tooconfigure-web-proxy-via-hello-setup-wizard"></a>Merhaba Kurulum Sihirbazı aracılığıyla tooconfigure web proxy
1. Merhaba seri konsol menüsünde seçeneği 1, **oturum oturum tam erişim** ve hello sağlamak **cihaz Yöneticisi parolası**. Kurulum Sihirbazı'nı oturumu toostart türü hello şu komutu:
   
    `Invoke-HcsSetupWizard`
2. Bu hello cihaz kaydı için kullanılan hello Kurulum Sihirbazı'nı ilk kez kullanıyorsanız, hello web proxy yapılandırması gelene kadar tüm gerekli hello ağ ayarlarını tooconfigure gerekir. Aygıtınız zaten kayıtlı değilse, hello web proxy yapılandırması gelene kadar tüm hello yapılandırılmış ağ ayarlarını kabul edebilirsiniz. Merhaba Kurulum Sihirbazı'nda istendiğinde tooconfigure web proxy ayarları, yazın **Evet**.
3. Hello için **Web Proxy URL'si**, başlangıç IP adresi belirtin veya tam etki alanı adı (FQDN) hello bulut ile iletişim kurarken, aygıt toouse istersiniz, web proxy sunucusu ve hello TCP bağlantı noktası numarası hello. Hello aşağıdaki biçimi kullanın:
   
    `http://<IP address or FQDN of hello web proxy server>:<TCP port number>`
   
    Varsayılan olarak, TCP bağlantı noktası 8080 belirtilir.
4. Merhaba kimlik doğrulaması türü olarak seçin **NTLM**, **temel**, veya **hiçbiri**. Merhaba hello proxy sunucu yapılandırması için en az güvenli kimlik doğrulaması temel kullanılır. NT LAN Yöneticisi (NTLM) olan bir üç yönlü bir ileti sistemi (bazen dört ek bütünlük gerekliyse) kullanan bir yüksek güvenlikli ve karmaşık kimlik doğrulama protokolü tooauthenticate bir kullanıcı. Merhaba varsayılan kimlik doğrulaması, NTLM kullanılır. Daha fazla bilgi için bkz: [temel](http://hc.apache.org/httpclient-3.x/authentication.html) ve [NTLM kimlik doğrulaması](http://hc.apache.org/httpclient-3.x/authentication.html). 
   
   > [!IMPORTANT]
   > **Hello StorSimple Yöneticisi hizmeti, hello cihaz izleme grafikleri basit çalışmıyor veya NTLM kimlik doğrulaması hello proxy sunucusu yapılandırmasını hello cihaz için etkinleştirilir. Grafikler toowork izleme Merhaba tooensure gerekir, kimlik doğrulamasının tooNONE ayarlanır.**
   > 
   > 
5. Kimlik doğrulaması kullanıyorsanız, kaynağı bir **Web Proxy Kullanıcı** ve **Web Proxy parola**. Ayrıca tooconfirm hello parola gerekir.
   
    ![StorSimple cihaz1 Web Proxy'yi Yapılandır](./media/storsimple-configure-web-proxy/IC751830.png)

Cihazınız hello için ilk kez kaydediyorsanız hello kayıt işlemine devam edin. Aygıtınız zaten kayıtlı, Başlangıç Sihirbazı'nı çıkılacak. yapılandırılmış hello ayarları kaydedilir.

Web proxy şimdi de etkinleştirilir. Merhaba atlayabilirsiniz [etkinleştirmek web proxy](#enable-web-proxy) adım ve doğrudan çok Git[görünüm web proxy ayarları hello Klasik Azure portalı](#view-web-proxy-settings-in-the-azure-classic-portal).

## <a name="configure-web-proxy-via-windows-powershell-for-storsimple-cmdlets"></a>StorSimple cmdlet'leri için Windows PowerShell aracılığıyla Web Proxy'yi Yapılandır
Bir alternatif bir yol tooconfigure web proxy ayarları hello Windows PowerShell için StorSimple cmdlet'leri aracılığıyla değil. Aşağıdaki adımları tooconfigure web proxy hello gerçekleştirin.

#### <a name="tooconfigure-web-proxy-via-cmdlets"></a>cmdlet'leri aracılığıyla tooconfigure web proxy
1. Merhaba seri konsol menüsünde seçeneği 1, **oturum oturum tam erişim**. İstendiğinde, hello sağlayın **cihaz Yöneticisi parolası**. Merhaba varsayılan parola `Password1`.
2. Merhaba komut satırına aşağıdakini yazın:
   
    `Set-HcsWebProxy -Authentication NTLM -ConnectionURI "<http://<IP address or FQDN of web proxy server>:<TCP port number>" -Username "<Username for web proxy server>"`
   
    Sağlayın ve aşağıda gösterildiği gibi istendiğinde hello parolayı onaylayın.
   
    ![Üzerinde StorSimple cihaz3'te Web Proxy'yi Yapılandır](./media/storsimple-configure-web-proxy/IC751831.png)

Merhaba web proxy yapılandırılmıştır ve etkin toobe gerekiyor.

## <a name="enable-web-proxy"></a>Web ara sunucusunu etkinleştirme
Web proxy varsayılan olarak devre dışıdır. StorSimple Cihazınızda hello web proxy ayarlarını yapılandırdıktan sonra StorSimple tooenable hello web proxy ayarlarını toouse hello Windows PowerShell gerekir.

> [!NOTE]
> **Merhaba Kurulum Sihirbazı'nı tooconfigure web proxy kullandıysanız, bu adım gerekli olur. Web ara Sunucusu Kurulum Sihirbazı oturumu sonra otomatik olarak varsayılan olarak etkindir.**
> 
> 

Merhaba aygıtınızda aşağıdaki StorSimple tooenable web proxy'si için Windows PowerShell'de adımları gerçekleştirin:

#### <a name="tooenable-web-proxy"></a>tooenable web proxy
1. Merhaba seri konsol menüsünde seçeneği 1, **oturum oturum tam erişim**. İstendiğinde, hello sağlayın **cihaz Yöneticisi parolası**. Merhaba varsayılan parola `Password1`.
2. Merhaba komut satırına aşağıdakini yazın:
   
    `Enable-HcsWebProxy`
   
    StorSimple Cihazınızda hello web proxy yapılandırması şimdi etkinleştirdiniz.
   
    ![Üzerinde StorSimple cihaz4'te Web Proxy'yi Yapılandır](./media/storsimple-configure-web-proxy/IC751832.png)

## <a name="view-web-proxy-settings-in-hello-azure-classic-portal"></a>Web proxy ayarları hello Klasik Azure portalında görüntüleyin
Merhaba web proxy ayarları hello Windows PowerShell arabirimi üzerinden yapılandırılır ve hello Klasik portalını değiştirilemez. Ancak, bu yapılandırılmış ayarları hello Klasik Portalı'nda görüntüleyebilirsiniz. Aşağıdaki adımları tooview web proxy hello gerçekleştirin.

#### <a name="tooview-web-proxy-settings"></a>tooview web proxy ayarları
1. Çok gidin**StorSimple Yöneticisi hizmeti > aygıtları**. Seçin ve bir cihaza tıklayın ve ardından çok gidin**yapılandırma**.
2. Aşağı kaydırın hello üzerinde **yapılandırma** çok sayfa**Web proxy ayarlarını** bölümü. Aşağıda gösterildiği gibi StorSimple Cihazınızda yapılandırılmış hello web proxy ayarlarını görüntüleyebilirsiniz.
   
    ![Yönetim Portalı'nda Görünümü Web Proxy](./media/storsimple-configure-web-proxy/ViewWebProxyPortal_M.png)

## <a name="errors-during-web-proxy-configuration"></a>Web proxy yapılandırması sırasında hatalar
Merhaba web proxy ayarları hatalı yapılandırıldıysa, hata iletileri görüntülenen toohello kullanıcı StorSimple için Windows PowerShell'de olacaktır. Aşağıdaki tablonun hello bazı bu hata iletileri, olası nedenler ve önerilen eylemler açıklanmaktadır.

| Seri yok. | HRESULT hata kodu | Olası temel nedeni | Önerilen eylem |
|:--- |:--- |:--- |:--- |
| 1. |0x80070001 |Merhaba pasif denetleyicisinden komutunu çalıştırın ve hello etkin denetleyicisiyle mümkün toocommunicate değil. |Merhaba komutu hello etkin denetleyicisinde çalıştırın. toorun hello komutu hello pasif denetleyicisinden pasif tooactive denetleyicisinden toofix hello bağlantısı gerekir. Bu bağlantı bozuk ise tooengage Microsoft Support gerekir. |
| 2. |0x800710dd - hello işlemi tanımlayıcısı geçerli değil |Proxy ayarları, StorSimple sanal cihazlar üzerinde desteklenmez. |Proxy ayarları, StorSimple sanal cihazlar üzerinde desteklenmez. Bu, yalnızca bir StorSimple fiziksel cihazda yapılandırılabilir. |
| 3. |0x80070057 - geçersiz parametre |Merhaba proxy ayarlarını sağlanan hello parametrelerden biri geçerli değil. |Merhaba URI doğru biçimde sağlanmadı. Hello aşağıdaki biçimi kullanın:`http://<IP address or FQDN of hello web proxy server>:<TCP port number>` |
| 4. |0x800706ba - RPC sunucusu kullanılamıyor |Merhaba kök nedeni hello aşağıdakilerden biridir:</br></br>Küme ayarlama değil.</br></br>DataPath hizmeti çalışmıyor.</br></br>Pasif denetleyicisinden Hello komutunu çalıştırın ve hello etkin denetleyicisiyle mümkün toocommunicate değil. |Lütfen küme hello engage Microsoft Support tooensure yukarı ve datapath hizmeti çalışıyor.</br></br>Merhaba etkin denetleyicisinden Hello komutunu çalıştırın. Merhaba pasif denetleyicisinden toorun hello komutunun istiyorsanız, tooensure gerekir hello pasif denetleyiciyi hello etkin denetleyicisi ile iletişim kurabilir. Bu bağlantı bozuk ise tooengage Microsoft Support gerekir. |
| 5. |0X800706be - RPC çağrısı başarısız oldu |Küme çalışmıyor. |Lütfen Microsoft Küme hello tooensure çalışıyor Support göster. |
| 6. |0x8007138f - küme kaynak bulunamadı |Platform Hizmet küme kaynağı bulunamadı. Bu durum Hello yükleme doğru değildi ortaya çıkar. |Tooperform, cihazda bir Fabrika sıfırlaması gerekebilir. Toocreate platform kaynak gerekebilir. Sonraki adımlar için Microsoft Support temasa geçin. |
| 7. |0x8007138c - küme kaynağı çevrimiçi değil |Platform veya datapath küme kaynaklarının çevrimiçi değildir. |Lütfen kişi Microsoft Support toohelp hello datapath ve platform Hizmet kaynağı olduğundan emin olun çevrimiçi. |

> [!NOTE]
> * hata iletilerinin listesi yukarıda Hello geniş kapsamlı değildir. 
> * Merhaba, StorSimple Yöneticisi hizmetiniz Klasik Azure portalında içinde hatalarla ilgili tooweb proxy ayarlarını görüntülenmez. Web proxy ile ilgili bir sorun varsa hello Yapılandırma tamamlandıktan sonra hello Aygıt durumu çok değiştirmek**çevrimdışı** hello Klasik Portalı'ndaki. |
> 
> 

## <a name="next-steps"></a>Sonraki Adımlar
* Cihazınızı dağıtma veya web proxy ayarlarını yapılandırma sırasında herhangi bir sorunla karşılaşırsanız, çok başvuran[StorSimple cihaz dağıtımına sorun giderme](storsimple-troubleshoot-deployment.md).
* toouse hello StorSimple Yöneticisi hizmeti, Git çok nasıl toolearn[kullanım StorSimple Cihazınızı StorSimple Yöneticisi hizmet tooadminister hello](storsimple-manager-service-administration.md).

