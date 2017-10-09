---
title: "Varolan aaaWork şirket içi proxy sunucuları ve Azure AD | Microsoft Docs"
description: "Nasıl varolan toowork proxy sunucuları şirket içi kapsar."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: kgremban
ms.openlocfilehash: 7f8cec4f676f99bead5211bcbcf23056bd7f211f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-existing-on-premises-proxy-servers"></a>Mevcut şirket içi proxy sunucuları ile çalışma

Bu makalede açıklanır nasıl tooconfigure Azure Active Directory (Azure AD) uygulama proxy'si bağlayıcılar toowork giden proxy sunucuları ile. Varolan proxy'leri sahip ağ ortamları olan müşteriler için tasarlanmıştır.

Bu ana dağıtım senaryolarında bakarak başlatın:
* Bağlayıcılar toobypass, şirket içi giden proxy'leri yapılandırın.
* Bağlayıcılar toouse bir giden proxy tooaccess Azure AD uygulama proxy'si yapılandırın.

Bağlayıcıları nasıl çalıştığı hakkında daha fazla bilgi için bkz: [anlamak Azure AD uygulama proxy'si Bağlayıcılar](application-proxy-understand-connectors.md).

## <a name="configure-hello-outbound-proxy"></a>Merhaba giden proxy ayarlarını yapılandır

Ortamınızda bir giden proxy varsa, uygun izinleri tooconfigure hello giden proxy ile bir hesabı kullanın. Merhaba yükleyici hello hello yükleme yapan hello kullanıcının bağlamında çalıştığından, Microsoft Edge veya başka bir Internet tarayıcısı kullanarak hello yapılandırmasını kontrol edebilirsiniz.

Microsoft edge'de tooconfigure hello proxy ayarları:

1. Çok Git**ayarları** > **görünüm Gelişmiş ayarları** > **açık Proxy ayarlarını** > **el ile Ara Sunucusu Kurulumu** .
2. Ayarlama **bir proxy sunucu kullanacak** çok**üzerinde**seçin hello **hello proxy sunucusu için yerel (intranet) adresleri kullanmayın** onay kutusunu ve ardından değişiklik hello adresi ve bağlantı noktası tooreflect Yerel proxy sunucunuzun.
3. Merhaba gerekli proxy ayarlarını doldurun.

   ![Proxy ayarları iletişim kutusu](./media/application-proxy-working-with-proxy-servers/proxy-bypass-local-addresses.png)

## <a name="bypass-outbound-proxies"></a>Giden proxy atlama

Bağlayıcılar giden isteklerde temel işletim sistemi bileşeni vardır. Bu bileşenler toolocate hello ağdaki bir proxy sunucusu otomatik olarak çalışır. Merhaba ortamında etkinleştirilirse Web Proxy Otomatik Bulma (WPAD) kullanırlar.

Merhaba işletim sistemi bileşenlerini wpad.domainsuffix için DNS araması gerçekleştirerek toolocate bir proxy sunucusu deneyin. Bu DNS çözümlenirse, HTTP isteğinden sonra toohello IP yapılır wpad.dat adresi. Bu isteği hello proxy yapılandırma betiği, ortamınızdaki haline gelir. Merhaba bağlayıcı bu komut dosyası tooselect bir giden proxy sunucusunu kullanır. Ancak, bağlayıcı trafiği hala aracılığıyla, hello proxy gereken ek yapılandırma ayarları nedeniyle geçebilir değil.

Merhaba bağlayıcı toobypass kullanır, şirket içi proxy tooensure doğrudan bağlantı toohello Azure yapılandırabilirsiniz Hizmetleri. Bu yaklaşım (ağ ilkeniz için izin veriyorsa) öneririz, çünkü bu daha az bir yapılandırma toomaintain olduğu anlamına gelir.

Merhaba bağlayıcı için toodisable giden proxy kullanım hello C:\Program Files\Microsoft AAD uygulama Proxy Connector\ApplicationProxyConnectorService.exe.config dosyasını düzenleyin ve hello eklemek *system.net* Bu kod örneğinde gösterildiği bölümü :

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.net>
    <defaultProxy enabled="false"></defaultProxy>
  </system.net>
  <runtime>
    <gcServer enabled="true"/>
  </runtime>
  <appSettings>
    <add key="TraceFilename" value="AadAppProxyConnector.log" />
  </appSettings>
</configuration>
```
Merhaba bağlayıcı güncelleştirici hizmetini de hello proxy atladığı tooensure C:\Program Files\Microsoft AAD uygulama Proxy Connector Updater bulunan bir benzer değişiklik toohello ApplicationProxyConnectorUpdaterService.exe.config dosyasını olun.

Toorevert toohello varsayılan .config dosyaları gerektiğinde toomake hello özgün dosyalarının kopyalarını emin olun.

## <a name="use-hello-outbound-proxy-server"></a>Merhaba giden proxy sunucu kullan

Bazı ortamlar özel durum olmadan bir giden proxy üzerinden tüm giden trafiği toogo gerektirir. Sonuç olarak, hello proxy atlama bir seçenek değil.

Merhaba bağlayıcı trafiği toogo hello giden proxy üzerinden hello Aşağıdaki diyagramda gösterildiği gibi yapılandırabilirsiniz:

 ![Bağlayıcı trafiği toogo bir giden proxy tooAzure AD aracılığıyla yapılandırma uygulama proxy'si](./media/application-proxy-working-with-proxy-servers/configure-proxy-settings.png)

Sonuç olarak yalnızca giden trafiğe sahip olan olduğundan hiç gerek tooconfigure gelen, güvenlik duvarları üzerinden erişim.

### <a name="step-1-configure-hello-connector-and-related-services-toogo-through-hello-outbound-proxy"></a>1. adım: hello bağlayıcısını yapılandırın ve Hizmetleri toogo hello giden proxy ile ilişkili

WPAD hello ortamında etkin ve uygun şekilde yapılandırılmış varsa daha önce anlatıldığı gibi hello bağlayıcı hello giden proxy sunucusu ve girişimi toouse otomatik olarak keşfeder onu. Ancak, bir giden proxy üzerinden hello bağlayıcı toogo açıkça yapılandırabilirsiniz.

toodo bunu hello C:\Program Files\Microsoft AAD uygulama Proxy Connector\ApplicationProxyConnectorService.exe.config dosyasını düzenleyin ve hello eklemek *system.net* Bu kod örneğinde gösterildiği bölümü. Değişiklik *proxyserver:8080* yerel ara sunucu adı veya IP adresi ve başlangıç bağlantı noktası üzerinde dinleme yaptığı tooreflect.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.net>  
    <defaultProxy>   
      <proxy proxyaddress="http://proxyserver:8080" bypassonlocal="True" usesystemdefault="True"/>   
    </defaultProxy>  
  </system.net>
  <runtime>
    <gcServer enabled="true"/>
  </runtime>
  <appSettings>
    <add key="TraceFilename" value="AadAppProxyConnector.log" />
  </appSettings>
</configuration>
```

Ardından, C:\Program Files\Microsoft AAD uygulama Proxy Bağlayıcısı Updater\ApplicationProxyConnectorUpdaterService.exe.config bulunan benzer bir değişiklik toohello dosyasını yaparak hello Connector Updater hizmet toouse hello proxy yapılandırın.

### <a name="step-2-configure-hello-proxy-tooallow-traffic-from-hello-connector-and-related-services-tooflow-through"></a>2. adım: hello bağlayıcı ve ilgili hizmetler tooflow aracılığıyla hello proxy tooallow trafiği yapılandırma

Merhaba giden proxy dört yönlerini tooconsider vardır:
* Proxy giden kuralları
* Proxy kimlik doğrulaması
* Proxy bağlantı noktaları
* SSL denetleme

#### <a name="proxy-outbound-rules"></a>Proxy giden kuralları
Bağlayıcı hizmeti erişimi için uç noktalar aşağıdaki erişim toohello izin ver:

* *. msappproxy.net
* *. servicebus.windows.net

İlk kaydı için uç noktalar aşağıdaki erişim toohello izin ver:

* login.windows.net
* Login.microsoftonline.com

FQDN DEĞERİNE göre bağlantı sağlar ve bunun yerine toospecify IP aralıkları gerekir, bu seçenekleri kullanın:

* Merhaba bağlayıcı giden erişim tooall hedefleri izin verin.
* Merhaba bağlayıcı giden çok erişime[Azure veri merkezi IP aralıkları](https://www.microsoft.com/en-gb/download/details.aspx?id=41653). Azure veri merkezi IP aralıkları hello listesini kullanarak ile Merhaba haftalık güncelleştirilmiş iştir. Bir işlemde yer tooensure erişim kuralları buna göre güncelleştirilir tooput gerekir.

#### <a name="proxy-authentication"></a>Proxy kimlik doğrulaması

Proxy kimlik doğrulaması şu anda desteklenmiyor. Geçerli Bizim önerimiz tooallow hello bağlayıcı anonim erişim toohello Internet hedefleri ' dir.

#### <a name="proxy-ports"></a>Proxy bağlantı noktaları

Merhaba bağlayıcı hello BAĞLAN yöntemini kullanarak giden SSL tabanlı bağlantılar sağlar. Bu yöntem temelde hello giden proxy üzerinden tünel ayarlar. Merhaba proxy sunucu tooallow tooports 443 ve 80 tünel yapılandırın.

>[!NOTE]
>Hizmet veri yolu HTTPS üzerinden çalıştığında, 443 numaralı bağlantı noktasını kullanır. Ancak, varsayılan olarak, hizmet veri yolu doğrudan TCP bağlantıları çalışır ve yalnızca doğrudan bağlantı başarısız olursa tooHTTPS geri döner.

Service Bus trafiği de hello giden proxy sunucu üzerinden gönderilen Merhaba, bu hello bağlayıcı doğrudan toohello bağlanamıyor olun tooensure 9350, 9352 ve 5671 bağlantı noktaları için Azure Hizmetleri.

#### <a name="ssl-inspection"></a>SSL denetleme
Hello bağlayıcı trafiği için sorunlara neden olduğu SSL denetlemesi hello bağlayıcı trafiği için kullanmayın.

## <a name="troubleshoot-connector-proxy-problems-and-service-connectivity-issues"></a>Bağlayıcı proxy sorunları ve hizmet bağlantı sorunlarını giderme
Şimdi hello proxy üzerinden akan tüm trafiği görmeniz gerekir. Sorunlarınız varsa, sorun giderme bilgileri aşağıdaki hello yardımcı olmalıdır.

en iyi şekilde tooidentify hello ve bağlayıcı bağlantı sorunlarını giderme sorunları olan bir ağ yakalama hello bağlayıcı hizmetini hello bağlayıcı hizmeti başlatılırken tootake. Bu zorlu bir görev olabilir, bu nedenle yakalama ve ağ izlemelerini filtreleme hızlı ipuçları bakalım.

İzleme aracı tercih ettiğiniz hello kullanabilirsiniz. Bu makalede Hello amaçları doğrultusunda, Microsoft Network Monitor 3.4 kullandık. Yapabilecekleriniz [Microsoft'tan indirmeniz](https://www.microsoft.com/download/details.aspx?id=4865).

belirli tooNetwork İzleyicisi Merhaba örnekler ve bölümler aşağıdaki hello kullanırız filtreleri olan ancak hello ilkeleri uygulanan tooany çözümleme aracı olabilir.

### <a name="take-a-capture-by-using-network-monitor"></a>Ağ İzleyicisi'ni kullanarak bir görüntüsü alın

bir yakalama toostart:

1. Ağ İzleyicisi'ni açın ve tıklatın **yeni yakalama**.
2. Merhaba tıklatın **Başlat** düğmesi.

   ![Ağ İzleyicisi penceresi](./media/application-proxy-working-with-proxy-servers/network-capture.png)

Bir yakalama tamamladıktan sonra hello tıklayın **durdurmak** düğmesini tooend onu.

### <a name="take-a-capture-of-connector-traffic"></a>Bağlayıcı trafik görüntüsü alın

İlk sorun giderme için hello aşağıdaki adımları gerçekleştirin:

1. Services.msc hello Azure AD uygulama ara sunucusu Bağlayıcısı hizmetini durdurun.
2. Merhaba ağ yakalama başlatın.
3. Hello Azure AD uygulama ara sunucusu Bağlayıcısı hizmetini başlatın.
4. Merhaba ağ yakalama işlemini durdurun.

   ![Services.msc Azure AD uygulama ara sunucusu Bağlayıcısı hizmetinde](./media/application-proxy-working-with-proxy-servers/services-local.png)

### <a name="look-at-hello-requests-from-hello-connector-toohello-proxy-server"></a>Merhaba isteklerinin hello bağlayıcı toohello proxy sunucusundan arayın

Bir ağ yakalama olduğuna göre hazır toofilter demektir. Merhaba anahtar toolooking hello izleme sırasında nasıl toofilter hello yakalama anlamaktır.

Bir filtre (8080 hello proxy hizmet bağlantı noktası olduğu) aşağıdaki gibidir:

**(http. İstek veya http. Yanıt) ve tcp.port==8080**

Bu filtre hello girerseniz, **görüntüleme filtresi** penceresini açın ve select **Uygula**, yakalanan hello trafiği hello filtreye bağlı filtreler.

Merhaba önceki filtre yalnızca hello HTTP istekleri ve yanıtları hello proxy bağlantı noktası/gruptan gösterir. Merhaba bağlayıcı yapılandırılmış toouse bir proxy sunucusu olduğu bir bağlayıcı başlatma için hello filtresi şöyle bir şey gösterir:

 ![Filtrelenmiş HTTP istekleri ve yanıtları örnek listesi](./media/application-proxy-working-with-proxy-servers/http-requests.png)

Şimdi özellikle hello proxy sunucusu ile iletişim gösterin BAĞLAN istekleri hello aradığınız. Başarı bir HTTP Tamam (200) yanıt alın.

407 veya 502, gibi diğer yanıt kodlarını görürseniz hello proxy kimlik doğrulaması gerektiren veya başka bir nedenle hello trafiğe izin verilmez. Bu noktada, proxy sunucusu destek ekibinize göster.

### <a name="identify-failed-tcp-connection-attempts"></a>TCP bağlantı girişimleri başarısız tanımlayın

Merhaba ilginizi çekebilir diğer yaygın bir senaryo hello bağlayıcı tooconnect doğrudan çalışıyor, ancak başarısız olduğu durumdur.

Bu sorunu belirlemeye tooeasily yardımcı olan başka bir Ağ İzleyicisi filtredir:

**özellik. TCPSynRetransmit**

Eşitlemeye paket hello ilk paket tooestablish bir TCP bağlantı sayısıdır. Bu paket yanıt döndürmezse hello Eşitlemeye reattempted. Merhaba filtre toosee önceki tüm yeniden iletilen SYN isteklerini kullanabilirsiniz. Ardından, bu SYN isteklerini tooany Bağlayıcısı ilgili trafik karşılık olup olmadığını kontrol edebilirsiniz.

Merhaba aşağıdaki örnek başarısız bağlantı denemesi tooService veri yolu bağlantı noktası 9352 gösterir:

 ![Başarısız bağlantı denemesi için örnek yanıt](./media/application-proxy-working-with-proxy-servers/failed-connection-attempt.png)

Yanıt önceki hello gibi bir şey görürseniz, hello bağlayıcı hello Azure Service Bus hizmeti ile doğrudan toocommunicate çalışıyor. Merhaba bağlayıcı toomake doğrudan bağlantılar toohello Azure beklediğiniz, hizmetleri, bu yanıt olan bir ağ veya güvenlik duvarı sorunu olduğunu NET bir belirti.

>[!NOTE]
>Yapılandırılmış toouse bir proxy sunucusu varsa, bu yanıt Service Bus tooattempting bağlantı HTTPS üzerinden geçmeden önce doğrudan bir TCP bağlantı çalışıyor anlamına gelebilir.
>

Ağ izleme çözümleme herkes için değil. Ancak, ağ ile neler olduğunu bir hakkında değerli bir araç tooget hızlı bilgi olabilir.

Bağlayıcı bağlantı sorunları ile toostruggle devam ederseniz, bir bilet destek ekibimiz ile oluşturun. Merhaba takım daha fazla sorun giderme konusunda yardımcı olabilir.

Uygulama Ara sunucusu Bağlayıcısı ile hataları çözümleme hakkında daha fazla bilgi için bkz: [sorun giderme uygulaması proxy'si](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-troubleshoot).

## <a name="next-steps"></a>Sonraki adımlar

[Azure AD uygulama proxy'si bağlayıcılar anlama](application-proxy-understand-connectors.md)<br>
[Nasıl toosilently yükleme hello Azure AD uygulama ara sunucusu Bağlayıcısı](active-directory-application-proxy-silent-installation.md)
