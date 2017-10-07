---
title: "aaaOn içi veri ağ geçidi | Microsoft Docs"
description: "Bir şirket içi ağ geçidi, Azure Analysis Services sunucunuzun tooon içi veri kaynaklarına bağlanacak ise gereklidir."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: cd596155-b608-4a34-935e-e45c95d884a9
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/21/2017
ms.author: owend
ms.openlocfilehash: fc7b9c69e6f81b41deb7a5d6d963225593845d84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-tooon-premises-data-sources-with-azure-on-premises-data-gateway"></a>Azure şirket içi veri ağ geçidi ile tooon içi veri kaynaklarına bağlanma
Merhaba şirket içi veri ağ geçidi, şirket içi veri kaynakları ve Azure Analysis Services sunucularınızı hello bulutta arasında güvenli veri aktarımını sağlayan bir köprü gibi davranır. Toplama tooworking hello birden çok Azure Analysis Services sunucusu ile aynı bölgede, hello hello ağ geçidinin en son sürümünü de Azure Logic Apps, Power BI, güç uygulamaları ve Microsoft Flow ile çalışır. Birden çok Hizmetleri'nde hello ilişkilendirebilirsiniz tek bir ağ geçidi ile aynı bölgede. 

 Azure Analysis Services gerektiren bir ağ geçidi kaynağı hello aynı bölgede. Örneğin, Azure Analysis Services sunucuları hello Doğu ABD 2 bölgede varsa, bir ağ geçidi kaynağı hello Doğu ABD 2 bölgesindeki gerekir. Doğu ABD 2 birden çok sunucuya hello kullanabilirsiniz aynı ağ geçidi.

İlk kez hello ağ geçidi hello ile kurulumun tamamlanmasında dört bölümden oluşan bir işlemdir:

- **Kurulumunu indirin ve çalıştırın** -Bu adım, kuruluşunuzdaki bir bilgisayarda bir ağ geçidi hizmeti yükler.

- **Ağ geçidini kaydetmek** - Bu adımda, bir ad belirtin ve kurtarma anahtarı, ağ geçidiniz için ve ağ geçidiniz hello ağ geçidi bulut hizmeti ile kaydetme bir bölge seçin.

- **Bir ağ geçidi kaynağı oluşturma** -Bu adımda, Azure aboneliğinizde bir ağ geçidi kaynağı oluşturun.

- **Sunucuları tooyour ağ geçidi kaynağına bağlanmasına** -aboneliğinizde bir ağ geçidi kaynağına sahip olduğunda, sunucuları tooit bağlanma başlayabilirsiniz.

Aboneliğiniz için yapılandırılmış bir ağ geçidi kaynağına sahip olduğunda, birden çok sunucu ve diğer hizmetleri tooit bağlanabilir. Yalnızca tooinstall faklı bir ağ geçidi gerekir ve farklı bir bölgede sunucuları veya diğer hizmetler varsa ek ağ geçidi kaynakları oluşturun.

hemen kullanmaya tooget bkz [yüklemek ve şirket içi veri ağ geçidi yapılandırma](analysis-services-gateway-install.md).

## <a name="how-it-works"></a>Nasıl çalışır?
bir bilgisayara yüklemeniz, kuruluşunuzda hello ağ geçidi çalıştıran bir Windows hizmeti olarak **şirket içi veri ağ geçidi**. Bu yerel hizmet hello Azure Service Bus aracılığıyla ağ geçidi bulut hizmetine kayıtlı. Ardından Azure aboneliğiniz için bir ağ geçidi kaynağı ağ geçidi bulut hizmeti oluşturun. Ardından sunuculardır, Azure Analysis Services tooyour ağ geçidi kaynağına bağlandı. İçi sunucu ihtiyacını tooconnect tooyour modellerinde sorgular veya işlem için veri kaynakları, bir sorgu ve veri akış ilişkilerinden geçen hello ağ geçidi kaynağı, Azure Service Bus, yerel şirket içi veri ağ geçidi hizmeti ve veri kaynaklarınızı hello. 

![Nasıl çalışır?](./media/analysis-services-gateway/aas-gateway-how-it-works.png)

Sorgular ve veri akış:

1. Bir sorgu hello şirket içi veri kaynağı için hello şifreli kimlik bilgileriyle hello bulut hizmeti tarafından oluşturulur. Ardından, tooa sıra hello ağ geçidi tooprocess için de gönderdi.
2. Merhaba ağ geçidi bulut Hizmeti'ne hello sorgu analiz eder ve hello isteği toohello iter [Azure Service Bus](https://azure.microsoft.com/documentation/services/service-bus/).
3. Merhaba şirket içi veri ağ geçidi hello Azure hizmet veri yolu için bekleyen istekler yoklar.
4. Hello ağ geçidi hello sorgu alır, hello kimlik şifresini çözer ve toohello veri kaynakları söz konusu kimlik bilgileriyle bağlanır.
5. Merhaba ağ geçidi hello sorgu toohello veri kaynağı için yürütme gönderir.
6. Merhaba sonuçları hello veri kaynağından geri toohello ağ geçidi, ardından hello bulut hizmeti ve sunucunuz üzerine gönderilir.

## <a name="windows-service-account"></a>Windows hizmet hesabı
Merhaba şirket içi veri ağ geçidi olduğu yapılandırılmış toouse *NT SERVICE\PBIEgwService* hello Windows hizmeti oturum açma kimlik bilgileri için. Varsayılan olarak, bir hizmet olarak oturum açmada sağ hello sahiptir; Merhaba ağ geçidi yüklüyorsanız hello makine Hello bağlamında. Bu kimlik bilgileri, aynı kullanılan hesap tooconnect tooon içi veri kaynakları veya Azure hesabınızda hello değil.  

Proxy sunucunuzu sorunlarla karşılaşırsanız tooauthentication, hello Windows hizmet hesabı tooa etki alanı kullanıcı ya da yönetilen toochange isteyebilir hizmet hesabı.

## <a name="ports"></a>Bağlantı noktaları
Merhaba ağ geçidi giden bağlantı tooAzure hizmet veri yolu oluşturur. Giden bağlantı noktaları iletişim kurar: TCP 443 (varsayılan), 5671, 5672, 9354 aracılığıyla 9350.  Merhaba ağ geçidi gelen bağlantı noktalarının gerektirmez.

Beyaz liste hello IP adresleri, Güvenlik Duvarı'nda, veri bölgesinin öneririz. Merhaba indirebilirsiniz [Microsoft Azure veri merkezi IP listesi](https://www.microsoft.com/download/details.aspx?id=41653). Bu liste haftalık güncelleştirilir.

> [!NOTE]
> Merhaba IP hello Azure veri merkezi IP listesinde listelenen CIDR gösteriminde adresleridir. Örneğin, 10.0.0.0/24 10.0.0.24 aracılığıyla 10.0.0.0 anlamına gelmez. Merhaba hakkında daha fazla bilgi [CIDR gösteriminde](http://whatismyipaddress.com/cidr).
>
>

Merhaba, hello ağ geçidi tarafından kullanılan hello tam olarak nitelenmiş etki alanı adlarını verilmiştir.

| Etki alanı adları | Giden bağlantı noktaları | Açıklama |
| --- | --- | --- |
| *. powerbı.com |80 |HTTP toodownload hello yükleyici kullanılır. |
| *. powerbı.com |443 |HTTPS |
| *. analysis.windows.net |443 |HTTPS |
| *. login.windows.net |443 |HTTPS |
| *. servicebus.windows.net |5671-5672 |Gelişmiş Message Queuing Protokolü (AMQP) |
| *. servicebus.windows.net |443, 9350-9354 |Hizmet veri yolu geçişi (erişim denetimi belirteci alımı için 443'ü gerektirir) TCP üzerinden üzerindeki dinleyicileri |
| *. frontend.clouddatahub.net |443 |HTTPS |
| *. core.windows.net |443 |HTTPS |
| Login.microsoftonline.com |443 |HTTPS |
| *. msftncsi.com |443 |Merhaba ağ geçidi hello Power BI hizmeti tarafından erişilemediğinde tootest internet bağlantısı kullanılır. |
| *.microsoftonline p.com |443 |Yapılandırmasına bağlı olarak kimlik doğrulaması için kullanılır. |

### <a name="force-https"></a>Azure Service Bus ile HTTPS iletişimi zorlama
Doğrudan TCP yerine HTTPS kullanarak Azure Service Bus ile Merhaba ağ geçidi toocommunicate zorlayabilirsiniz; Ancak, bunun nedenle performansı büyük ölçüde düşürebilir. Merhaba değiştirebileceğiniz *Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config* başlangıç değerinden değiştirerek dosya `AutoDetect` çok`Https`. Bu genellikle bir dosyadır *C:\Program Files\On içi veri ağ geçidi*.

```
<setting name="ServiceBusSystemConnectivityModeString" serializeAs="String">
    <value>Https</value>
</setting>
```

## <a name="faq"></a>Sık sorulan sorular

### <a name="general"></a>Genel

**Q**: bir ağ geçidi hello bulutta Azure SQL veritabanı gibi veri kaynakları için ihtiyacım var? <br/>
**A**: Hayır Bir ağ geçidi tooon içi veri kaynakları yalnızca bağlanır.

**Q**: hello ağ geçidi aynı makine hello veri kaynağı olarak hello yüklü toobe sahip mi? <br/>
**A**: Hayır Merhaba ağ geçidi sağlanan hello bağlantı bilgilerini kullanarak toohello veri kaynağına bağlanır. Bu bağlamda bir istemci uygulaması olarak Hello ağ geçidi göz önünde bulundurun. Merhaba ağ geçidi yalnızca, genellikle hello üzerinde aynı sağlanan hello yetenek tooconnect toohello sunucu adı gerekiyor ağ.

<a name="why-azure-work-school-account"></a>

**Q**: neden ı toouse bir iş gerekir veya Okul hesabı toosign? <br/>
**A**: yalnızca Azure bir iş veya Okul hesabınız hello şirket içi veri ağ geçidi yüklediğinizde. Oturum açma hesabınızın Azure Active Directory (Azure AD) tarafından yönetilen bir kiracı depolanır. Genellikle, Azure AD hesabınızın kullanıcı asıl adı (UPN) hello e-posta adresi ile eşleşir.

**Q**: kimlik bilgilerimi depolandığı? <br/>
**A**: bir veri kaynağı için girdiğiniz hello kimlik bilgileri şifrelenir ve hello ağ geçidi bulut Hizmeti'ne depolanır. Merhaba kimlik hello şirket içi veri ağ geçidi şifresi çözülür.

**Q**: ağ bant genişliği için tüm gereksinimleri vardır? <br/>
**A**: ağınızı öneririz sahip bağlantısı iyi verimlilik vardır. Her ortam farklıdır ve gönderilen verilerin miktarını hello hello sonuçları etkiler. ExpressRoute kullanarak şirket içi ve hello Azure veri merkezleri arasında işleme düzeyini tooguarantee yardımcı olabilir.
Merhaba üçüncü taraf aracı Azure hızı Test uygulama toohelp ölçer, üretilen iş kullanabilirsiniz.

**Q**: hello gecikmesi çalışan sorguları tooa veri kaynağından hello ağ geçidi nedir? Merhaba en iyi mimarisi nedir? <br/>
**A**: tooreduce ağ gecikmesi, mümkün olduğunca yakın toohello veri kaynağı olarak yükleme hello ağ geçidi. Merhaba gerçek veri kaynağında hello ağ geçidi yükleyebilirsiniz, bu yakınlık sunulan hello gecikme süresi en aza indirir. Merhaba veri merkezleri çok göz önünde bulundurun. Örneğin, hizmetiniz hello Batı ABD datacenter kullanır ve SQL Server'ın bir Azure VM ile barındırılan olması durumunda, Azure VM hello Batı ABD çok olması gerekir. Bu yakınlık gecikme süresi en aza indirir ve çıkış ücretlerini hello Azure VM üzerinde önler.

**Q**: gönderilen sonuçları geri toohello bulut şeklini? <br/>
**A**: sonuçları hello Azure Service Bus gönderilir.

**Q**: tüm gelen bağlantıları toohello ağ geçidi'nden hello bulut vardır? <br/>
**A**: Hayır Merhaba ağ geçidi giden bağlantılar tooAzure hizmet veri yolu kullanır.

**Q**: ne ı giden bağlantıları engelle? Ne tooopen gerekir? <br/>
**A**: hello bağlantı noktaları ve ağ geçidi kullanan hello konakları bakın.

**Q**: ne hello gerçek Windows hizmeti adı verilir?<br/>
**A**: Services'de hello ağ geçidi şirket içi veri ağ geçidi hizmeti olarak adlandırılır.

**Q**: ağ geçidi Windows hizmeti bir Azure Active Directory hesap ile çalıştırmak hello? <br/>
**A**: Hayır Merhaba Windows hizmeti geçerli bir Windows hesabı olması gerekir. Varsayılan olarak, hello ile hizmet SID, NT SERVICE\PBIEgwService hello hizmeti çalışır.

### <a name="high-availability"></a>Yüksek kullanılabilirlik ve olağanüstü durum kurtarma

**Q**: olağanüstü durum kurtarma için kullanılabilir seçenekleri nelerdir? <br/>
**A**: hello kurtarma anahtarı toorestore kullanın veya bir ağ geçidi taşıyın. Merhaba ağ geçidi yüklediğinizde hello kurtarma anahtarını belirtin.

**Q**: hello kurtarma anahtarı hello avantajı nedir? <br/>
**A**: hello kurtarma anahtarı bir şekilde toomigrate sağlar veya ağ geçidi ayarlarınızı sonra bir olağanüstü durum kurtarma.

## <a name="troubleshooting"></a>Sorunlarını giderme

**Q**: nasıl sorguları toohello şirket içi veri kaynağına gönderilen görebilir? <br/>
**A**: gönderilen hello sorgular sorgu izlemeyi etkinleştirebilirsiniz. Sorun giderme tamamlanınca toohello özgün değeri geri izleme toochange sorgu unutmayın. Sorgu izlemesi açık bırakarak daha büyük günlükleri oluşturur.

Ayrıca, izleme sorguları için veri kaynağınız olan araçlar da bakabilirsiniz. Örneğin, SQL Server ve Analysis Services için genişletilmiş olaylar veya SQL Profiler kullanabilirsiniz.

**Q**: hello gateway günlükleri nerede? <br/>
**A**: Bu konunun ilerleyen bölümlerinde günlüklere bakın.

### <a name="update"></a>Güncelleştirme toohello en son sürümü

Merhaba ağ geçidi sürümü güncel olmayan hale geldiğinde birçok sorunları ortaya. Genel iyi uygulama olarak, hello en son sürümünü kullandığınızdan emin olun. Merhaba ağ geçidi için ayda bir veya daha uzun güncelleştirmediyseniz hello hello ağ geçidinin en son sürümünü yüklemeyi göz önünde bulundurun ve hello sorunu yeniden bakın.

### <a name="error-failed-tooadd-user-toogroup--2147463168-pbiegwservice-performance-log-users"></a>Hata: tooadd kullanıcı toogroup başarısız oldu. (-2147463168 PBIEgwService performans günlük kullanıcılar)

Desteklenmeyen bir etki alanı denetleyicisinde tooinstall hello ağ geçidi çalışırsanız, bu hatayı alabilirsiniz. Bir etki alanı denetleyicisi olmayan bir makineyi hello geçidinde dağıttığınızdan emin olun.

## <a name="logs"></a>Günlükleri

Günlük dosyaları bir önemli sorun giderirken kaynaktır.

#### <a name="enterprise-gateway-service-logs"></a>Kurumsal ağ geçidi hizmeti günlükleri

`C:\Users\PBIEgwService\AppData\Local\Microsoft\On-premises data gateway\<yyyyymmdd>.<Number>.log`

#### <a name="configuration-logs"></a>Yapılandırma günlükleri

`C:\Users\<username>\AppData\Local\Microsoft\On-premises data gateway\GatewayConfigurator.log`




#### <a name="event-logs"></a>Olay günlükleri

Veri Yönetimi ağ geçidi ve PowerBIGateway günlüklerini altında hello bulabilirsiniz **uygulama ve hizmet günlükleri**.


## <a name="telemetry"></a>Telemetri
Telemetri, izleme ve sorun giderme için kullanılabilir. Varsayılan olarak

**telemetri üzerinde tooturn**

1.  Merhaba şirket içi veri ağ geçidi istemci dizini hello bilgisayarda denetleyin. Genellikle,. **%SystemDrive%\Program Files\On içi veri ağ geçidi**. Veya, Hizmetler konsolunu açın ve hello yolu tooexecutable denetleyin: hello şirket içi veri ağ geçidi hizmeti bir özelliğidir.
2.  Merhaba Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config dosyasında istemci dizininden. Merhaba SendTelemetry ayarı tootrue değiştirin.
        
    ```
        <setting name="SendTelemetry" serializeAs="String">
                    <value>true</value>
        </setting>
    ```

3.  Yaptığınız değişiklikleri kaydedin ve hello Windows hizmetini yeniden başlatın: şirket içi veri ağ geçidi hizmeti.




## <a name="next-steps"></a>Sonraki adımlar
* [Çözümleme Hizmetleri yönetme](analysis-services-manage.md)
* [Azure Analysis Services Veri Al](analysis-services-connect.md)
