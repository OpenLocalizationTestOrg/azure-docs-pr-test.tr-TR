---
title: "Var olan iş şirket içi proxy sunucuları ve Azure AD | Microsoft Docs"
description: "Mevcut şirket içi proxy sunucularıyla çalışacak şekilde nasıl ele alınmaktadır."
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
ms.openlocfilehash: bdca442755507c4ffe8d43692c5b7f2aa3a746f3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="work-with-existing-on-premises-proxy-servers"></a>Mevcut şirket içi proxy sunucuları ile çalışma

Bu makalede, giden proxy sunucuları ile çalışmak için Azure Active Directory (Azure AD) uygulama proxy'si bağlayıcıları yapılandırın açıklanmaktadır. Varolan proxy'leri sahip ağ ortamları olan müşteriler için tasarlanmıştır.

Bu ana dağıtım senaryolarında bakarak başlatın:
* Şirket içi giden proxy atlama için bağlayıcıları yapılandırın.
* Azure AD uygulama proxy'si erişmek için bir giden proxy kullanmak için bağlayıcıları yapılandırın.

Bağlayıcıları nasıl çalıştığı hakkında daha fazla bilgi için bkz: [anlamak Azure AD uygulama proxy'si Bağlayıcılar](application-proxy-understand-connectors.md).

## <a name="configure-the-outbound-proxy"></a>Giden proxy ayarlarını yapılandır

Ortamınızda bir giden proxy varsa, bir hesap uygun izinlere sahip giden proxy yapılandırmak için kullanın. Yükleyici yüklemeyi yapan kullanıcının bağlamında çalıştığından, Microsoft Edge veya başka bir Internet tarayıcısı kullanarak yapılandırmasını kontrol edebilirsiniz.

Microsoft Edge'de proxy ayarlarını yapılandırmak için:

1. Git **ayarları** > **görünüm Gelişmiş ayarları** > **Proxy ayarları** > **el ile Proxy Kurulum**.
2. Ayarlama **bir proxy sunucu kullanacak** için **üzerinde**seçin **(intranet) yerel adresler için proxy sunucusu kullanma** onay kutusunu işaretleyin ve ardından adresi ve bağlantı noktası yerel yansıtacak şekilde değiştirin proxy sunucusu.
3. Gerekli proxy ayarlarını doldurun.

   ![Proxy ayarları iletişim kutusu](./media/application-proxy-working-with-proxy-servers/proxy-bypass-local-addresses.png)

## <a name="bypass-outbound-proxies"></a>Giden proxy atlama

Bağlayıcılar giden isteklerde temel işletim sistemi bileşeni vardır. Bu bileşenleri otomatik olarak ağ üzerinde bir proxy sunucu bulmaya çalışır. Ortamında etkinleştirilirse Web Proxy Otomatik Bulma (WPAD) kullanırlar.

İşletim sistemi bileşenlerini wpad.domainsuffix için DNS araması gerçekleştirerek bir proxy sunucu bulmaya çalışır. Bu DNS çözümlenirse, bir HTTP isteği wpad.dat için IP adresi için yapılır. Bu istek proxy yapılandırması komut dosyası, ortamınızdaki olur. Bağlayıcı, bir giden proxy sunucusu seçmek için bu komut dosyasını kullanır. Ancak, bağlayıcı trafiği hala aracılığıyla, proxy gereken ek yapılandırma ayarları nedeniyle geçebilir değil.

Azure hizmetlerine doğrudan bağlantı kullandığından emin olmak için şirket içi proxy atlama bağlayıcıyı yapılandırabilirsiniz. Bu yaklaşım (ağ ilkeniz için izin veriyorsa) öneririz, çünkü korumak için daha az bir yapılandırmaya sahip anlamına gelir.

Bağlayıcı için giden proxy kullanımını devre dışı bırakmak için C:\Program Files\Microsoft AAD uygulama Proxy Connector\ApplicationProxyConnectorService.exe.config dosyasını düzenleyin ve ekleme *system.net* Bu kod örneğinde gösterildiği bölümü:

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
Bağlayıcı güncelleştirici hizmetini de proxy atladığı emin olmak için benzer C:\Program Files\Microsoft AAD uygulama Proxy Connector Updater bulunan ApplicationProxyConnectorUpdaterService.exe.config dosyasını değişiklik.

Varsayılan .config dosyaları geri gerekebileceği özgün dosyaların kopyalarını yaptığınızdan emin olun.

## <a name="use-the-outbound-proxy-server"></a>Giden proxy sunucusu kullan

Bazı ortamlar özel durum olmadan bir giden proxy gitmesi tüm giden trafiği gerektirir. Sonuç olarak, proxy atlama bir seçenek değil.

Aşağıdaki çizimde gösterildiği gibi giden proxy üzerinden gitmek için bağlayıcı trafiğini yapılandırabilirsiniz:

 ![Azure AD uygulama proxy'si giden bir proxy üzerinden gitmek için trafiği bağlayıcı yapılandırma](./media/application-proxy-working-with-proxy-servers/configure-proxy-settings.png)

Yalnızca giden trafiğe sahip sonucu olarak, güvenlik duvarı üzerinden gelen erişimi yapılandırmak için gerek yoktur.

### <a name="step-1-configure-the-connector-and-related-services-to-go-through-the-outbound-proxy"></a>Adım 1: giden proxy üzerinden gitmek için ilgili hizmetler ve bağlayıcı yapılandırma

WPAD ortamda etkin ve uygun şekilde yapılandırılmış varsa daha önce anlatıldığı gibi bağlayıcı otomatik olarak giden proxy sunucusunu bulmak ve bunu kullanmayı dener. Ancak, bir giden proxy üzerinden gitmek için bağlayıcı açıkça yapılandırabilirsiniz.

Bunu yapmak için C:\Program Files\Microsoft AAD uygulama Proxy Connector\ApplicationProxyConnectorService.exe.config dosyasını düzenleyin ve ekleme *system.net* Bu kod örneğinde gösterildiği bölümü. Değişiklik *proxyserver:8080* yerel proxy sunucunuzun adını veya IP adresi ve üzerinde dinleme bağlantı noktasını yansıtmak için.

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

Ardından, bağlayıcı güncelleştirici hizmetini C:\Program Files\Microsoft AAD uygulama Proxy Bağlayıcısı Updater\ApplicationProxyConnectorUpdaterService.exe.config bulunan dosyasına benzer bir değişiklik yapılarak proxy kullanacak şekilde yapılandırın.

### <a name="step-2-configure-the-proxy-to-allow-traffic-from-the-connector-and-related-services-to-flow-through"></a>Adım 2: proxy Bağlayıcısı ve ilgili hizmetler akışına trafiğe izin verecek şekilde yapılandırma

Giden proxy dikkate alınması gereken dört nokta vardır:
* Proxy giden kuralları
* Proxy kimlik doğrulaması
* Proxy bağlantı noktaları
* SSL denetleme

#### <a name="proxy-outbound-rules"></a>Proxy giden kuralları
Bağlayıcı hizmeti erişim şu uç noktalar için erişim izni ver:

* *. msappproxy.net
* *. servicebus.windows.net

İlk kayıt için aşağıdaki uç noktalarına erişime izin ver:

* login.windows.net
* Login.microsoftonline.com

FQDN DEĞERİNE göre bağlantı sağlar ve bunun yerine IP aralıklarını belirtmeniz gerekir, bu seçenekleri kullanın:

* Tüm hedefler bağlayıcı giden erişim sağlar.
* Bağlayıcı giden erişmesine izin vermek [Azure veri merkezi IP aralıkları](https://www.microsoft.com/en-gb/download/details.aspx?id=41653). Azure veri merkezi IP aralıkları listesi kullanarak haftalık güncelleştirilmiş iştir. Bir işlem, erişim kuralları buna göre güncelleştirilir emin olmak için yerleştirdiniz gerekir.

#### <a name="proxy-authentication"></a>Proxy kimlik doğrulaması

Proxy kimlik doğrulaması şu anda desteklenmiyor. Bizim geçerli Internet hedeflere bağlayıcı anonim erişime izin vermek için önerilir.

#### <a name="proxy-ports"></a>Proxy bağlantı noktaları

Bağlayıcı BAĞLAN yöntemini kullanarak giden SSL tabanlı bağlantılar sağlar. Bu yöntem temelde giden proxy üzerinden tünel ayarlar. Bağlantı noktaları için 443 ve 80 tünel izin vermek için proxy sunucusunu yapılandırın.

>[!NOTE]
>Hizmet veri yolu HTTPS üzerinden çalıştığında, 443 numaralı bağlantı noktasını kullanır. Ancak, varsayılan olarak, hizmet veri yolu doğrudan TCP bağlantıları çalışır ve yalnızca doğrudan bağlantı başarısız olursa HTTPS'ye geri döner.

Hizmet veri yolu trafiği de giden proxy sunucu üzerinden gönderilen emin olmak için bağlayıcı 9350, 9352 ve 5671 bağlantı noktaları için Azure hizmetlerine doğrudan bağlanamıyor emin olun.

#### <a name="ssl-inspection"></a>SSL denetleme
Bağlayıcı trafiği için sorunlara neden olduğu SSL denetleme bağlayıcı trafiği için kullanmayın.

## <a name="troubleshoot-connector-proxy-problems-and-service-connectivity-issues"></a>Bağlayıcı proxy sorunları ve hizmet bağlantı sorunlarını giderme
Şimdi proxy akan tüm trafiği görmeniz gerekir. Sorunlarınız varsa, aşağıdaki sorun giderme bilgileri yardımcı olmalıdır.

Tanımlamak ve bağlayıcı bağlantı sorunlarını gidermek için en iyi yolu bir ağ yakalama bağlayıcı hizmetini bağlayıcı hizmeti başlatılırken almaktır. Bu zorlu bir görev olabilir, bu nedenle yakalama ve ağ izlemelerini filtreleme hızlı ipuçları bakalım.

Tercih ettiğiniz izleme aracını kullanabilirsiniz. Bu makalede amaçları doğrultusunda, Microsoft Network Monitor 3.4 kullandık. Yapabilecekleriniz [Microsoft'tan indirmeniz](https://www.microsoft.com/download/details.aspx?id=4865).

Aşağıdaki bölümlerde kullanırız filtreleri ve örnekler Ağ İzleyicisi belirli, ancak herhangi bir analiz aracı ilkeleri uygulanabilir.

### <a name="take-a-capture-by-using-network-monitor"></a>Ağ İzleyicisi'ni kullanarak bir görüntüsü alın

Bir yakalama başlatmak için:

1. Ağ İzleyicisi'ni açın ve tıklatın **yeni yakalama**.
2. Tıklatın **Başlat** düğmesi.

   ![Ağ İzleyicisi penceresi](./media/application-proxy-working-with-proxy-servers/network-capture.png)

Bir yakalama tamamladıktan sonra tıklayın **durdurmak** onu sonuna düğmesi.

### <a name="take-a-capture-of-connector-traffic"></a>Bağlayıcı trafik görüntüsü alın

İlk sorun giderme için aşağıdaki adımları gerçekleştirin:

1. Services.msc Azure AD uygulama ara sunucusu Bağlayıcısı hizmetini durdurun.
2. Ağ Yakalama başlatın.
3. Azure AD uygulama ara sunucusu Bağlayıcısı hizmetini başlatın.
4. Ağ yakalama işlemini durdurun.

   ![Services.msc Azure AD uygulama ara sunucusu Bağlayıcısı hizmetinde](./media/application-proxy-working-with-proxy-servers/services-local.png)

### <a name="look-at-the-requests-from-the-connector-to-the-proxy-server"></a>Proxy sunucusuna bir bağlayıcı isteklerinin arayın

Bir ağ yakalama olduğuna göre onu filtrelemek hazırsınız. İzleme sırasında arayan anahtarını yakalama filtreleme anlamaktır.

Bir filtre (8080 proxy hizmet bağlantı noktası olduğu) aşağıdaki gibidir:

**(http. İstek veya http. Yanıt) ve tcp.port==8080**

Bu filtre girerseniz, **görüntüleme filtresi** penceresini açın ve select **Uygula**, filtreye bağlı yakalanan trafik filtreleri.

Önceki filtresinin denetleyicisinden proxy bağlantı noktası yalnızca HTTP istekleri ve yanıtları gösterir. Bağlayıcı bir proxy sunucu kullanmak için yapılandırıldığı bağlayıcı başlangıç filtresi şöyle bir şey gösterir:

 ![Filtrelenmiş HTTP istekleri ve yanıtları örnek listesi](./media/application-proxy-working-with-proxy-servers/http-requests.png)

Şimdi özellikle proxy sunucusu ile iletişim Göster CONNECT isteklerini aradığınız. Başarı bir HTTP Tamam (200) yanıt alın.

407 veya 502, gibi diğer yanıt kodlarını görürseniz proxy kimlik doğrulaması gerektiren veya başka bir nedenle trafiğe izin verilmez. Bu noktada, proxy sunucusu destek ekibinize göster.

### <a name="identify-failed-tcp-connection-attempts"></a>TCP bağlantı girişimleri başarısız tanımlayın

İlginizi çekebilir bir ortak senaryoyu bağlayıcıyı doğrudan bağlanmak çalışıyor, ancak başarısız olduğu durumdur.

Bu sorunu kolayca tanımlamaya yardımcı olan başka bir Ağ İzleyicisi filtredir:

**özellik. TCPSynRetransmit**

Bir TCP bağlantı kurmak üzere gönderilen ilk paket Eşitlemeye pakettir. Bu paket yanıt döndürmezse Eşitlemeye reattempted. Yeniden aktarılan tüm SYN isteklerini görmek için yukarıdaki filtresini kullanabilirsiniz. Ardından, bu SYN istekleri Bağlayıcısı ile ilgili tüm trafik için karşılık gelen olup olmadığını kontrol edebilirsiniz.

Aşağıdaki örnek, 9352 adlı hizmet veri yolu bağlantı başarısız bağlantı girişimi gösterir:

 ![Başarısız bağlantı denemesi için örnek yanıt](./media/application-proxy-working-with-proxy-servers/failed-connection-attempt.png)

Önceki yanıt şöyle görürseniz, bağlayıcı doğrudan Azure Service Bus hizmeti ile iletişim kurmaya çalışıyor. Azure hizmetlerine doğrudan bağlantı bağlayıcı bekliyorsanız, bu yanıt, bir ağ veya güvenlik duvarı sorunu olduğunu NET bir belirti ' dir.

>[!NOTE]
>Bir proxy sunucu kullanacak şekilde yapılandırıldıysa, bu yanıt hizmet veri yolu bağlantı HTTPS üzerinden çalışıyor geçmeden önce doğrudan bir TCP bağlantı çalışıyor anlamına gelebilir.
>

Ağ izleme çözümleme herkes için değil. Ancak, ağ ile neler olup bittiğini hakkında hızlı bilgi almak için değerli bir araç olabilir.

Bağlayıcı bağlantı sorunları güçlük Devam ederseniz, bir bilet destek ekibimiz ile oluşturun. Takım daha fazla sorun giderme konusunda yardımcı olabilir.

Uygulama Ara sunucusu Bağlayıcısı ile hataları çözümleme hakkında daha fazla bilgi için bkz: [sorun giderme uygulaması proxy'si](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-troubleshoot).

## <a name="next-steps"></a>Sonraki adımlar

[Azure AD uygulama proxy'si bağlayıcılar anlama](application-proxy-understand-connectors.md)<br>
[Azure AD uygulama ara sunucusu Bağlayıcısı sessiz yükleme](active-directory-application-proxy-silent-installation.md)
