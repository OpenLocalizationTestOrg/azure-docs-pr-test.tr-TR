---
title: "StorSimple 8000 serisi cihaz için web Ara sunucusu kurma aaaSet | Microsoft Docs"
description: "Bilgi edinmek için StorSimple tooconfigure toouse Windows PowerShell web StorSimple cihazınız için proxy ayarları nasıl."
services: storsimple
documentationcenter: 
author: alkohli
manager: 
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: alkohli
ms.openlocfilehash: ed34ff400df66a5f1950c21d5298b41acc538cca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-proxy-for-your-storsimple-device"></a>StorSimple cihazınız için Web Proxy'yi Yapılandır

## <a name="overview"></a>Genel Bakış

Bu öğretici açıklar nasıl toouse Windows PowerShell StorSimple tooconfigure ve görünüm için web proxy ayarlarını StorSimple cihazınız için. Hello web proxy ayarları hello bulut ile iletişim kurarken hello StorSimple cihaz tarafından kullanılır. Web proxy sunucusu kullanılan tooadd olan başka bir güvenlik katmanı, filtre içerik, tooease bant genişliği gereksinimlerini önbelleğe veya bile, analytics ile Yardım.

Bu öğreticide Hello yönerge yalnızca tooStorSimple 8000 serisi fiziksel cihazlar geçerlidir. Web proxy yapılandırması hello StorSimple bulut uygulaması (8010 hem de 8020) üzerinde desteklenmiyor.

Web proxy'si, bir _isteğe bağlı_ StorSimple cihazınız için yapılandırma. StorSimple için Windows PowerShell aracılığıyla yalnızca web sunucusu yapılandırabilir. başlangıç yapılandırmasını iki adımlı bir işlem aşağıdaki gibidir:

1. İlk StorSimple cmdlet'leri hello Kurulum Sihirbazı'nı veya Windows PowerShell aracılığıyla web proxy ayarlarını yapılandırın.
2. Ardından, Itanium tabanlı sistemler için yapılandırılmış hello web proxy ayarları Windows PowerShell aracılığıyla StorSimple cmdlet'leri de etkinleştirin.

Merhaba web proxy yapılandırması tamamlandıktan sonra yapılandırılmış hello web proxy ayarlarını hem hello Microsoft Azure StorSimple cihaz Yöneticisi hizmeti hem de hello Windows PowerShell için StorSimple görüntüleyebilirsiniz.

Bu öğretici okuduktan sonra aşağıdakileri gerçekleştirebilirsiniz:

* Web ara Sunucusu Kurulum Sihirbazı'nı ve cmdlet'lerini kullanarak yapılandırın.
* Web proxy cmdlet'leri kullanarak etkinleştirin.
* Web proxy ayarları hello Azure portalında görüntüleyin.
* Web proxy yapılandırması sırasında hataları giderin.


## <a name="configure-web-proxy-via-windows-powershell-for-storsimple"></a>StorSimple için Windows PowerShell aracılığıyla Web Proxy'yi Yapılandır

Tooconfigure web proxy ayarları aşağıdaki hello birini kullanın:

* Kurulum Sihirbazı'nı tooguide sizi hello yapılandırma adımlarına.
* StorSimple için Windows PowerShell cmdlet'leri.

Bu yöntemlerin her biri hello aşağıdaki bölümlerde ele alınmıştır.

## <a name="configure-web-proxy-via-hello-setup-wizard"></a>Merhaba Kurulum Sihirbazı aracılığıyla Web Proxy'yi Yapılandır

Merhaba size adımları hello Kurulum Sihirbazı'nı tooguide için web proxy yapılandırması kullanın. Adımları tooconfigure web proxy aygıtınızda aşağıdaki hello gerçekleştirin.

#### <a name="tooconfigure-web-proxy-via-hello-setup-wizard"></a>Merhaba Kurulum Sihirbazı aracılığıyla tooconfigure web proxy

1. Merhaba seri konsol menüsünde seçeneği 1, **oturum oturum tam erişim** ve hello sağlamak **cihaz Yöneticisi parolası**. Kurulum Sihirbazı'nı oturumu toostart türü hello şu komutu:
   
    `Invoke-HcsSetupWizard`
2. Bu hello cihaz kaydı için kullanılan hello Kurulum Sihirbazı'nı ilk kez kullanıyorsanız, hello web proxy yapılandırması gelene kadar tüm gerekli hello ağ ayarlarının tooconfigure gerekir. Aygıtınız zaten kayıtlı değilse, hello web proxy yapılandırması ulaşana kadar tüm hello yapılandırılmış ağ ayarlarını kabul edin. Merhaba Kurulum Sihirbazı'nda istendiğinde tooconfigure web proxy ayarları, yazın **Evet**.
3. Hello için **Web Proxy URL'si**, başlangıç IP adresi belirtin veya tam etki alanı adı (FQDN) hello bulut ile iletişim kurarken, aygıt toouse istersiniz, web proxy sunucusu ve hello TCP bağlantı noktası numarası hello. Hello aşağıdaki biçimi kullanın:
   
    `http://<IP address or FQDN of hello web proxy server>:<TCP port number>`
   
    Varsayılan olarak, TCP bağlantı noktası 8080 belirtilir.
4. Merhaba kimlik doğrulaması türü olarak seçin **NTLM**, **temel**, veya **hiçbiri**. Merhaba hello proxy sunucu yapılandırması için en az güvenli kimlik doğrulaması temel kullanılır. NT LAN Yöneticisi (NTLM) olan bir üç yönlü bir ileti sistemi (bazen dört ek bütünlük gerekliyse) kullanan bir yüksek güvenlikli ve karmaşık kimlik doğrulama protokolü tooauthenticate bir kullanıcı. Merhaba varsayılan kimlik doğrulaması, NTLM kullanılır. Daha fazla bilgi için bkz: [temel](http://hc.apache.org/httpclient-3.x/authentication.html) ve [NTLM kimlik doğrulaması](http://hc.apache.org/httpclient-3.x/authentication.html). 
   
   > [!IMPORTANT]
   > **Hello StorSimple cihaz Yöneticisi hizmeti, hello cihaz izleme grafikleri basit çalışmıyor veya NTLM kimlik doğrulaması hello proxy sunucusu yapılandırmasını hello cihaz için etkinleştirilir. Grafikler toowork izleme Merhaba tooensure gerekir, kimlik doğrulamasının tooNONE ayarlanır.**
  
5. Merhaba kimlik doğrulaması etkinleştirilirse, kaynağı bir **Web Proxy Kullanıcı** ve **Web Proxy parola**. Ayrıca tooconfirm hello parola gerekir.
   
    ![StorSimple cihaz1 Web Proxy'yi Yapılandır](./media/storsimple-configure-web-proxy/IC751830.png)

Cihazınız hello için ilk kez kaydediyorsanız hello kayıt işlemine devam edin. Aygıtınız zaten kayıtlı, Başlangıç Sihirbazı'ndan çıkar. yapılandırılmış hello ayarları kaydedilir.

Web proxy şimdi etkinleştirildi. Merhaba atlayabilirsiniz [etkinleştirmek web proxy](#enable-web-proxy) adım ve doğrudan çok Git[hello Azure portal web proxy ayarlarını görüntülemek](#view-web-proxy-settings-in-the-azure-portal).

## <a name="configure-web-proxy-via-windows-powershell-for-storsimple-cmdlets"></a>StorSimple cmdlet'leri için Windows PowerShell aracılığıyla Web Proxy'yi Yapılandır

Bir alternatif bir yol tooconfigure web proxy ayarları hello Windows PowerShell için StorSimple cmdlet'leri aracılığıyla değil. Aşağıdaki adımları tooconfigure web proxy hello gerçekleştirin.

#### <a name="tooconfigure-web-proxy-via-cmdlets"></a>cmdlet'leri aracılığıyla tooconfigure web proxy
1. Merhaba seri konsol menüsünde seçeneği 1, **oturum oturum tam erişim**. İstendiğinde, hello sağlayın **cihaz Yöneticisi parolası**. Merhaba varsayılan parola `Password1`.
2. Merhaba komut satırına aşağıdakini yazın:
   
    `Set-HcsWebProxy -Authentication NTLM -ConnectionURI "<http://<IP address or FQDN of web proxy server>:<TCP port number>" -Username "<Username for web proxy server>"`
   
    Sağlayın ve istendiğinde hello parolayı onaylayın.
   
    ![Üzerinde StorSimple cihaz3'te Web Proxy'yi Yapılandır](./media/storsimple-configure-web-proxy/IC751831.png)

Merhaba web proxy yapılandırılmıştır ve etkin toobe gerekiyor.

## <a name="enable-web-proxy"></a>Web ara sunucusunu etkinleştirme

Web proxy varsayılan olarak devre dışıdır. StorSimple Cihazınızda hello web proxy ayarlarını yapılandırdıktan sonra hello Windows PowerShell için StorSimple tooenable hello web proxy ayarlarını kullanın.

> [!NOTE]
> **Merhaba Kurulum Sihirbazı'nı tooconfigure web proxy kullandıysanız, bu adım gerekli değildir. Web ara Sunucusu Kurulum Sihirbazı oturumu sonra otomatik olarak varsayılan olarak etkindir.**


Merhaba aygıtınızda aşağıdaki StorSimple tooenable web proxy'si için Windows PowerShell'de adımları gerçekleştirin:

#### <a name="tooenable-web-proxy"></a>tooenable web proxy
1. Merhaba seri konsol menüsünde seçeneği 1, **oturum oturum tam erişim**. İstendiğinde, hello sağlayın **cihaz Yöneticisi parolası**. Merhaba varsayılan parola `Password1`.
2. Merhaba komut satırına aşağıdakini yazın:
   
    `Enable-HcsWebProxy`
   
    StorSimple Cihazınızda hello web proxy yapılandırması şimdi etkinleştirdiniz.
   
    ![Üzerinde StorSimple cihaz4'te Web Proxy'yi Yapılandır](./media/storsimple-configure-web-proxy/IC751832.png)

## <a name="view-web-proxy-settings-in-hello-azure-portal"></a>Hello Azure portal Web proxy ayarlarını görüntüleme

Merhaba web proxy ayarları hello Windows PowerShell arabirimi üzerinden yapılandırılır ve hello portalını değiştirilemez. Ancak, bu yapılandırılmış ayarları hello Portalı'nda görüntüleyebilirsiniz. Aşağıdaki adımları tooview web proxy hello gerçekleştirin.

#### <a name="tooview-web-proxy-settings"></a>tooview web proxy ayarları
1. Çok gidin**StorSimple cihaz Yöneticisi hizmeti > aygıtları**. Seçin ve bir cihaza tıklayın ve ardından çok gidin**Aygıt Ayarları > Ağ**.

    ![Ağ'ı tıklatın](./media/storsimple-8000-configure-web-proxy/view-web-proxy-1.png)

2. Merhaba, **ağ ayarlarını** dikey penceresinde hello tıklatın **Web proxy** döşeme.

    ![Web proxy'yi tıklatın](./media/storsimple-8000-configure-web-proxy/view-web-proxy-2.png)

3. Merhaba, **Web proxy** dikey penceresinde, gözden geçirme yapılandırılmış hello web proxy ayarları, StorSimple Cihazınızda.
   
    ![Görünümü web proxy ayarları](./media/storsimple-8000-configure-web-proxy/view-web-proxy-3.png)


## <a name="errors-during-web-proxy-configuration"></a>Web proxy yapılandırması sırasında hatalar

Merhaba web proxy ayarları yanlış yapılandırılmış, hata iletileri görüntülenen toohello kullanıcı StorSimple için Windows PowerShell'de demektir. Aşağıdaki tablonun hello bazı bu hata iletileri, olası nedenler ve önerilen eylemler açıklanmaktadır.

| Seri yok. | HRESULT hata kodu | Olası temel nedeni | Önerilen eylem |
|:--- |:--- |:--- |:--- |
| 1. |0x80070001 |Merhaba pasif denetleyicisinden komutunu çalıştırın ve hello etkin denetleyicisiyle mümkün toocommunicate değil. |Merhaba komutu hello etkin denetleyicisinde çalıştırın. toorun hello komutu hello pasif denetleyicisinden hello bağlantı pasif tooactive denetleyicisinden düzeltmeniz gerekir. Bu bağlantı bozuk ise Microsoft Support devreye gerekir. |
| 2. |0x800710dd - hello işlemi tanımlayıcısı geçerli değil |Proxy ayarlarını StorSimple bulut uygulaması üzerinde desteklenmez. |Proxy ayarlarını StorSimple bulut uygulaması üzerinde desteklenmez. Bu, yalnızca bir StorSimple fiziksel cihazda yapılandırılabilir. |
| 3. |0x80070057 - geçersiz parametre |Merhaba proxy ayarlarını sağlanan hello parametrelerden biri geçerli değil. |Merhaba URI doğru biçimde sağlanmadı. Hello aşağıdaki biçimi kullanın:`http://<IP address or FQDN of hello web proxy server>:<TCP port number>` |
| 4. |0x800706ba - RPC sunucusu kullanılamıyor |Merhaba kök nedeni hello aşağıdakilerden biridir:</br></br>Küme ayarlama değil. </br></br>DataPath hizmeti çalışmıyor.</br></br>Pasif denetleyicisinden Hello komutunu çalıştırın ve hello etkin denetleyicisiyle mümkün toocommunicate değil. |Küme hello engage Microsoft Support tooensure çalışıyor ve datapath hizmeti çalışıyor.</br></br>Merhaba etkin denetleyicisinden Hello komutunu çalıştırın. Merhaba pasif denetleyicisinden toorun hello komutunun istiyorsanız, o hello pasif denetleyiciyi hello etkin denetleyicisi ile iletişim kurabildiğini emin olmalısınız. Bu bağlantı bozuk ise Microsoft Support devreye gerekir. |
| 5. |0X800706be - RPC çağrısı başarısız oldu |Küme çalışmıyor. |Microsoft Küme hello tooensure çalışıyor Support göster. |
| 6. |0x8007138f - küme kaynak bulunamadı |Platform Hizmet küme kaynağı bulunamadı. Bu durum Hello yükleme doğru değildi ortaya çıkar. |Tooperform, cihazda bir Fabrika sıfırlaması gerekebilir. Toocreate platform kaynak gerekebilir. Sonraki adımlar için Microsoft Support başvurun. |
| 7. |0x8007138c - küme kaynağı çevrimiçi değil |Platform veya datapath küme kaynaklarının çevrimiçi değildir. |Kişi Microsoft Support toohelp hello datapath ve platform Hizmet kaynağı çevrimiçi olduğundan emin olun. |

> [!NOTE]
> * hata iletilerinin listesi yukarıda Hello geniş kapsamlı değildir.
> * Hatalarla ilgili tooweb proxy ayarlarını hello StorSimple Aygıt Yöneticisi'ni hizmetinizi Azure portalında görüntülenmez. Web proxy ile ilgili bir sorun varsa hello Yapılandırma tamamlandıktan sonra hello Aygıt durumu çok değiştirmek**çevrimdışı** hello Klasik Portalı'ndaki. |

## <a name="next-steps"></a>Sonraki Adımlar
* Cihazınızı dağıtma veya web proxy ayarlarını yapılandırma sırasında herhangi bir sorunla karşılaşırsanız, çok başvuran[StorSimple cihaz dağıtımına sorun giderme](storsimple-troubleshoot-deployment.md).
* toouse hello StorSimple cihaz Yöneticisi hizmeti, Git çok nasıl toolearn[kullanım StorSimple Cihazınızı StorSimple cihaz Yöneticisi hizmeti tooadminister hello](storsimple-8000-manager-service-administration.md).

