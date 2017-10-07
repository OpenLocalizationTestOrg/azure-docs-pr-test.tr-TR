---
title: "aaaInstall şirket içi veri ağ geçidi - Azure Logic Apps | Microsoft Docs"
description: "Şirket içi veri kaynaklarına erişim önce hızlı veri aktarımı ve şirket içi veri kaynakları ve mantıksal uygulamalar arasında şifreleme için hello şirket içi veri ağ geçidi yükleyin"
keywords: "Şirket içi veri aktarımı, şifreleme, veri kaynakları veri erişimi"
services: logic-apps
documentationcenter: 
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 47e3024e-88a0-4017-8484-8f392faec89d
ms.service: logic-apps
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/13/2017
ms.author: LADocs; dimazaid; estfan
ms.openlocfilehash: 01386a904d856ff545f2eca8eb1b008dcdc08574
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-hello-on-premises-data-gateway-for-azure-logic-apps"></a>Azure mantıksal uygulamaları için Hello şirket içi veri ağ geçidi yükleyin

Mantıksal uygulamalarınızı şirket içi veri kaynaklarına erişebilmesi için yükleme ve hello şirket içi veri ağ geçidi kurun. Merhaba ağ geçidi hızlı veri aktarımı ve şirket içi sistemleri ve logic apps arasında şifreleme sağlayan köprü gibi davranır. Merhaba ağ geçidi şifrelenmiş kanalda hello Azure Service Bus aracılığıyla şirket içi kaynaklardan veri aktarır. Güvenli giden trafiği hello ağ geçidi aracısından olarak tüm trafiğin kaynaklandığı. Daha fazla bilgi edinmek [hello veri ağ geçidi nasıl çalıştığını](#gateway-cloud-service).

Merhaba ağ geçidi bağlantıları toothese veri kaynakları şirket içinde destekler:

*   BizTalk Server 2016
*   DB2  
*   Dosya Sistemi
*   Informix
*   MQ
*   MySQL
*   Oracle Veritabanı
*   PostgreSQL
*   SAP uygulama sunucusu 
*   SAP ileti sunucusu
*   SharePoint
*   SQL Server
*   Teradata

Bu adımları nasıl toofirst yükleme hello veri ağ geçidi, önce şirket içi Göster [hello ağ geçidi ve logic apps arasında bir bağlantı ayarlayın](./logic-apps-gateway-connection.md). Desteklenen bağlayıcılar hakkında daha fazla bilgi için bkz: [Azure Logic Apps bağlayıcılarının](https://docs.microsoft.com/azure/connectors/apis-list). 

Nasıl toouse hello diğer hizmetler ile ağ geçidi hakkında daha fazla bilgi için bu makalelere bakın:

*   [Microsoft Power BI şirket içi veri ağ geçidi](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem/)
*   [Azure Analysis Services veri ağ geçidi şirket içi](../analysis-services/analysis-services-gateway.md)
*   [Microsoft Flow şirket içi veri ağ geçidi](https://flow.microsoft.com/documentation/gateway-manage/)
*   [Microsoft PowerApps şirket içi veri ağ geçidi](https://powerapps.microsoft.com/tutorials/gateway-management/)

<a name="requirements"></a>
## <a name="requirements"></a>Gereksinimler

**Minimum**:

* .NET 4.5 framework
* Windows 7 veya Windows Server 2008 R2 64-bit sürümünü (veya üstü)

**Önerilen**:

* 8 çekirdekli CPU
* 8 GB bellek
* 64 bit sürümü Windows 2012 R2'in (veya üstü)

**İle ilgili önemli noktalar**:

* Merhaba şirket içi veri ağ geçidi yalnızca yerel bir bilgisayara yükleyin.
Merhaba ağ geçidi etki alanı denetleyicisine yükleyemezsiniz.

   > [!TIP]
   > Merhaba üzerinde tooinstall hello ağ geçidi yok veri kaynağınız ile aynı bilgisayara. toominimize gecikme, olası tooyour veri kaynağı olarak ya da hello aynı kapatmak gibi hello ağ geçidi yükleyebilirsiniz izinleri olduğunu varsayarak bilgisayar.

* Merhaba ağ geçidi kapanmadan toosleep geçip geçmeyeceğini veya hello ağ geçidi bu koşullarda çalıştığından toohello Internet bağlanmıyor bir bilgisayarda yüklemeyin. Ayrıca, kablosuz ağ üzerinden ağ geçidi performansı düşebilir.

* Yükleme sırasında bilgileriyle oturum açmalıdır bir [iş veya Okul hesabı](https://docs.microsoft.com/azure/active-directory/sign-up-organization) Azure Active Directory tarafından (Azure AD), bir Microsoft hesabı yönetilir. 

  Merhaba aynı iş veya Okul hesabı daha sonra da hello Azure toouse sahip oluşturduğunuzda ve bir ağ geçidi kaynağı ile ağ geçidi yüklemenizi ilişkilendirmek portal. Logic app ve hello şirket içi veri kaynağınız arasında hello bağlantı oluşturduğunuzda, ardından bu ağ geçidi kaynağı seçin. [Neden gerekir t bir Azure AD iş veya Okul hesabı?](#why-azure-work-school-account)

  > [!TIP]
  > Bir Office 365 teklif için kaydolan ve gerçek iş e-sağlamadı, oturum açma adresinizi nasıl görünebileceği jeff@contoso.onmicrosoft.com. 

* 14.16.6317.4 sürümden daha eski bir yükleyici ile ayarladığınız mevcut bir ağ geçidi varsa, ağ geçidinizin konum çalışan hello son yükleyici tarafından değiştirilemiyor. Ancak, bunun yerine istediğiniz başlangıç konumu ile Merhaba son yükleyici tooset yeni bir ağ geçidi yukarı kullanabilirsiniz.
  
  14.16.6317.4 sürümden daha eski bir ağ geçidi yükleyicisi varsa, ancak ağ geçidiniz yüklemediniz henüz indirebilir ve hello son yükleyiciyi kullanın.

<a name="install-gateway"></a>

## <a name="install-hello-data-gateway"></a>Merhaba data gateway yükleyin

1.  [Karşıdan yükle ve yerel bilgisayarda hello ağ geçidi yükleyicisi çalıştırın](http://go.microsoft.com/fwlink/?LinkID=820931&clcid=0x409).

2. Gözden geçirin ve kullanım ve gizlilik bildirimini hello koşullarını kabul edin.

3. Merhaba yolu, yerel bilgisayarınızda tooinstall hello ağ geçidi istediğiniz yeri belirtin.

4. İstendiğinde, Azure iş veya Okul hesabı, bir Microsoft hesabı ile oturum açın.

   ![Oturum oturum Azure iş veya Okul hesabı](./media/logic-apps-gateway-install/sign-in-gateway-install.png)

5. Yüklü ağ geçidiniz ile Merhaba kaydettirmek [ağ geçidi bulut Hizmeti'ne](#gateway-cloud-service). Seçin **bu bilgisayarda yeni bir ağ geçidini kaydetmek**.

   Merhaba ağ geçidi bulut Hizmeti'ne şifreler ve veri kaynağı kimlik bilgilerini ve ağ geçidi ayrıntıları depolar. 
   Merhaba hizmeti, şirket içinde sorguları ve sonuçları mantıksal uygulamanızı, hello şirket içi veri ağ geçidi ve veri kaynağınız arasında da yönlendirir.

6. Ağ geçidi yüklemeniz için bir ad sağlayın. Bir kurtarma anahtarı oluşturun, sonra kurtarma anahtarını doğrulayın. 

   > [!IMPORTANT] 
   > Kurtarma anahtarı en az sekiz karakter içermelidir. Kaydet ve başlangıç anahtarı güvenli bir yerde sakladığınızdan emin olun. Toomigrate, istediğinizde de bu anahtarı ihtiyacınız geri yüklemek veya mevcut bir ağ geçidi alın.

   1. Merhaba ağ geçidi bulut Hizmeti'ne ve ağ geçidi yüklemenizi tarafından kullanılan Azure Service Bus toochange hello varsayılan bölgesini seçin **değişikliğin bölgesini**.

      ![Değişiklik bölgesi](./media/logic-apps-gateway-install/change-region-gateway-install.png)

      Merhaba varsayılan bölge, Azure AD Kiracı ile ilişkilendirilen hello bölgedir.

   2. Merhaba Hello sonraki bölmesinde açmak **seçin bölge** çok farklı bir bölge seçin.

      ![Başka bir bölge seçin](./media/logic-apps-gateway-install/select-region-gateway-install.png)

      Örneğin, select mantıksal uygulamanızı aynı bölgede hello ya da select hello bölgeye en yakın tooyour şirket içi veri kaynağı gecikme süresini azaltmak için. Ağ geçidi kaynak ve mantıksal uygulamanızı farklı konumlarda olabilir.

      > [!IMPORTANT]
      > Yükleme sonrasında bu bölgeyi değiştiremezsiniz. Bu bölge ayrıca belirler ve hello Azure kaynak ağ geçidiniz için oluşturabileceğiniz hello konumu kısıtlar. Bu nedenle, ağ geçidi kaynağı Azure'da oluşturduğunuzda, hello kaynak konumu ağ geçidi yüklemesi sırasında seçilen hello bölge eşleştiğinden emin olun.
      > 
      > Ağ geçidiniz için daha sonra farklı bir bölgeye toouse istiyorsanız, yeni bir ağ geçidi kurun ayarlamanız gerekir.

   3. Hazır olduğunuzda, seçin **Bitti**.

7. Şimdi, böylece hello Azure Portalı'nda aşağıdaki adımları izleyin [ağ geçidiniz için bir Azure kaynağı oluşturma](../logic-apps/logic-apps-gateway-connection.md). 

Daha fazla bilgi edinmek [hello veri ağ geçidi nasıl çalıştığını](#gateway-cloud-service).

## <a name="migrate-restore-or-take-over-an-existing-gateway"></a>Geçirme, geri yüklemek veya mevcut bir ağ geçidi alın

Bu görevler tooperform hello ağ geçidi yüklendiğinde, belirttiğiniz hello kurtarma anahtarı olması gerekir.

1. Bilgisayarınızın Başlat menüsünden seçin **şirket içi veri ağ geçidi**.

2. Merhaba yükleyici açılır oturumu ile sonra hello aynı Azure iş veya tooinstall hello ağ geçidi önceden Okul hesabı kullanılır.

3. Seçin **geçirme, geri yükleme veya mevcut bir ağ geçidi üzerinden Al**.

4. Üzerinden toomigrate, restore veya Al istediğiniz hello ağ geçidi için Hello adı ve kurtarma anahtarı sağlayın.

<a name="restart-gateway"></a>
## <a name="restart-hello-gateway"></a>Merhaba ağ geçidini yeniden başlatın

Merhaba ağ geçidi, bir Windows hizmet olarak çalışır. Diğer Windows hizmeti gibi başlatın ve birden çok yolla hello hizmetini durdurun. Örneğin, hello ağ geçidi çalıştığı hello bilgisayarda yükseltilmiş izinleri olan bir komut istemi açın ve ya da şu komutları çalıştırın:

* toostop hello hizmeti, şu komutu çalıştırın:
  
    `net stop PBIEgwService`

* toostart hello hizmeti, şu komutu çalıştırın:
  
    `net start PBIEgwService`

### <a name="windows-service-account"></a>Windows hizmet hesabı

Merhaba şirket içi veri ağ geçidi toouse ayarlanmış `NT SERVICE\PBIEgwService` hello Windows hizmeti oturum açma kimlik bilgileri. Varsayılan olarak, hello ağ geçidi yüklediğiniz hello ağ geçidi hello "hizmet olarak oturum aç" hakkına hello makine sahiptir.

> [!NOTE]
> Okul hesabı toosign toocloud Hizmetleri'nde kullanılan veya Hello Windows hizmet hesabını tooon içi veri kaynaklarına bağlanmak için kullanılan hello hesabından ve hello Azure çalışma alanından farklı.

## <a name="configure-a-firewall-or-proxy"></a>Bir güvenlik duvarı veya proxy yapılandırma

Merhaba ağ geçidi oluşturur giden bir bağlantıyı çok [Azure Service Bus](https://azure.microsoft.com/services/service-bus/). tooprovide proxy bilgi, ağ geçidi için [proxy ayarlarını yapılandırma](https://powerbi.microsoft.com/documentation/powerbi-gateway-proxy/).

toocheck güvenlik duvarı veya proxy bağlantıları, engelleyebilecek olup olmadığını doğrulayın makinenizin toohello gerçekten bağlanıp bağlanamayacağını Internet ve hello [Azure Service Bus](https://azure.microsoft.com/services/service-bus/). Bir PowerShell isteminden şu komutu çalıştırın:

`Test-NetConnection -ComputerName watchdog.servicebus.windows.net -Port 9350`

> [!NOTE]
> Bu komut, yalnızca bir ağ bağlantısı ve bağlantı toohello Azure Service Bus'test eder. Merhaba komutu herhangi bir şey yok şekilde hello ağ geçidi veya şifreler ve kimlik bilgilerinizi ve ağ geçidi ayrıntıları depolayan hello ağ geçidi bulut hizmeti ile toodo. 
>
> Ayrıca, bu komut yalnızca Windows Server 2012 R2 veya daha sonra kullanılabilir ve Windows 8.1 veya üzeri. Önceki işletim sistemi sürümlerinde, Telnet kullanabileceğiniz çok bağlantısını test edin. Daha fazla bilgi edinmek [Azure Service Bus ve karma çözümleri](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).

Sonuçlarınızı benzer toothis örnek gibi görünmelidir:

```text
ComputerName           : watchdog.servicebus.windows.net
RemoteAddress          : 70.37.104.240
RemotePort             : 5672
InterfaceAlias         : vEthernet (Broadcom NetXtreme Gigabit Ethernet - Virtual Switch)
SourceAddress          : 10.120.60.105
PingSucceeded          : False
PingReplyDetails (RTT) : 0 ms
TcpTestSucceeded       : True
```

Varsa **TcpTestSucceeded** çok ayarlanmadı**doğru**, güvenlik duvarı tarafından engellenmiş olabilir. Toobe kapsamlı istiyorsanız hello yerine **ComputerName** ve **bağlantı noktası** altında listelenen değerleri hello değerlerle [bağlantı noktalarını yapılandırma](#configure-ports) bu konuda.

Merhaba Güvenlik Duvarı'nı Azure Service Bus toohello Azure veri merkezleri yapar, hello bağlantıları engelliyor olabilir. Bu senaryo durumda Onayla (engelini kaldırma) tüm IP adresleri için bu veri merkezleri, bölgenizdeki hello. Bu IP adresleri için [get hello Azure IP adreslerinin listesi burada](https://www.microsoft.com/download/details.aspx?id=41653).

## <a name="configure-ports"></a>Bağlantı noktalarını yapılandırma

Merhaba ağ geçidi oluşturur giden bir bağlantıyı çok[Azure Service Bus](https://azure.microsoft.com/services/service-bus/) ve giden bağlantı noktaları iletişim kurar: TCP 443 (varsayılan), 5671, 5672, 9354 aracılığıyla 9350. Merhaba ağ geçidi gelen bağlantı noktalarının gerektirmez. Daha fazla bilgi edinmek [Azure Service Bus ve karma çözümleri](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).

| ETKİ ALANI ADLARI | GİDEN BAĞLANTI NOKTALARI | AÇIKLAMA |
| --- | --- | --- |
| *. analysis.windows.net | 443 | HTTPS | 
| *. login.windows.net | 443 | HTTPS | 
| *. servicebus.windows.net | 5671-5672 | Gelişmiş Message Queuing Protokolü (AMQP) | 
| *. servicebus.windows.net | 443, 9350-9354 | Hizmet veri yolu geçişi (erişim denetimi belirteci alımı için 443'ü gerektirir) TCP üzerinden üzerindeki dinleyicileri | 
| *. frontend.clouddatahub.net | 443 | HTTPS | 
| *. core.windows.net | 443 | HTTPS | 
| Login.microsoftonline.com | 443 | HTTPS | 
| *. msftncsi.com | 443 | Merhaba ağ geçidi hello Power BI hizmeti tarafından erişilemiyor tootest internet bağlantısı kullanılır. | 

Merhaba etki alanları yerine tooapprove IP adresine sahip değilse, indirin ve hello kullan [Microsoft Azure veri merkezi IP aralıkları listesi](https://www.microsoft.com/download/details.aspx?id=41653). Bazı durumlarda, tam etki alanı adı yerine IP adresi ile hello Azure hizmet veri yolu bağlantıları hale getirilir.

<a name="gateway-cloud-service"></a>
## <a name="how-does-hello-data-gateway-work"></a>Merhaba veri ağ geçidi nasıl çalışır?

Merhaba veri ağ geçidi mantıksal uygulamanızı, hello ağ geçidi bulut Hizmeti'ne ve şirket içi veri kaynağınız arasında hızlı ve güvenli iletişimi kolaylaştırır. 

![Diagram-for-on-Premises-Data-Gateway-Flow](./media/logic-apps-gateway-install/how-on-premises-data-gateway-works-flow-diagram.png)

Bu nedenle zaman hello kullanıcı hello bulutta tooyour bağlı olduğu bir öğesiyle etkileşim veri kaynağı şirket içi:

1. Merhaba ağ geçidi bulut Hizmeti'ne hello şifrelenmiş kimlik bilgileri hello veri kaynağı için birlikte bir sorgu oluşturur ve hello sorgu toohello sıra hello ağ geçidi tooprocess için gönderir.

2. Merhaba ağ geçidi bulut Hizmeti'ne hello sorgu analiz eder ve hello isteği toohello Azure Service Bus iter.

3. Merhaba şirket içi veri ağ geçidi hello Azure hizmet veri yolu için bekleyen istekler yoklar.

4. Merhaba ağ geçidi hello sorgu alır, hello kimlik şifresini çözer ve söz konusu kimlik bilgileriyle toohello veri kaynağına bağlanır.

5. Merhaba ağ geçidi hello sorgu toohello veri kaynağı için yürütme gönderir.

6. Merhaba sonuçları hello veri kaynağı, geri toohello ağ geçidi ve toohello ağ geçidi bulut Hizmeti'ne sonra gönderilir. Merhaba ağ geçidi bulut Hizmeti'ne sonra hello sonuçları kullanır.

<a name="faq"></a>
## <a name="frequently-asked-questions"></a>Sık sorulan sorular

### <a name="general"></a>Genel

**Q**: bir ağ geçidi için SQL Azure gibi hello bulut veri kaynaklarında ihtiyacım var? <br/>
**A**: Hayır Bir ağ geçidi tooon içi veri kaynakları yalnızca bağlanır.

**Q**: hello ağ geçidi aynı makine hello veri kaynağı olarak hello yüklü toobe sahip mi? <br/>
**A**: Hayır Merhaba ağ geçidi sağlanan hello bağlantı bilgilerini kullanarak toohello veri kaynağına bağlanır. Bu bağlamda bir istemci uygulaması olarak Hello ağ geçidi göz önünde bulundurun. Merhaba ağ geçidi yalnızca sağlanan hello yetenek tooconnect toohello sunucu adı gerekiyor.

<a name="why-azure-work-school-account"></a>

**Q**: neden gerekir t bir Azure okul veya iş hesabı toosign? <br/>
**A**: yalnızca Azure bir iş veya Okul hesabınız hello şirket içi veri ağ geçidi yüklediğinizde. Oturum açma hesabınızın Azure Active Directory (Azure AD) tarafından yönetilen bir kiracı depolanır. Genellikle, Azure AD hesabınızın kullanıcı asıl adı (UPN) hello e-posta adresi ile eşleşir.

**Q**: kimlik bilgilerimi depolandığı? <br/>
**A**: bir veri kaynağı için girdiğiniz hello kimlik bilgileri şifrelenir ve hello ağ geçidi bulut hizmetinde depolanır. Merhaba kimlik hello şirket içi veri ağ geçidi şifresi çözülür.

**Q**: ağ bant genişliği için tüm gereksinimleri vardır? <br/>
**A**: ağ bağlantısı iyi üretilen işi olan öneririz. Her ortam farklıdır ve gönderilen verilerin miktarını hello hello sonuçları etkiler. ExpressRoute kullanarak şirket içi ve hello Azure veri merkezleri arasında işleme düzeyini tooguarantee yardımcı olabilir.
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
**A**: Services'de hello ağ geçidi Power BI kurumsal ağ geçidi hizmeti olarak adlandırılır.

**Q**: ağ geçidi Windows hizmeti bir Azure Active Directory hesap ile çalıştırmak hello? <br/>
**A**: Hayır Merhaba Windows hizmeti geçerli bir Windows hesabı olması gerekir. Varsayılan olarak, hello ile hizmet SID, NT SERVICE\PBIEgwService hello hizmeti çalışır.

### <a name="high-availability-and-disaster-recovery"></a>Yüksek kullanılabilirlik ve olağanüstü durum kurtarma

**Q**: olağanüstü durum kurtarma için kullanılabilir seçenekleri nelerdir? <br/>
**A**: hello kurtarma anahtarı toorestore kullanın veya bir ağ geçidi taşıyın. Merhaba ağ geçidi yüklediğinizde hello kurtarma anahtarını belirtin.

**Q**: hello kurtarma anahtarı hello avantajı nedir? <br/>
**A**: hello kurtarma anahtarı bir şekilde toomigrate sağlar veya ağ geçidi ayarlarınızı sonra bir olağanüstü durum kurtarma.

**Q**: hello ağ geçidi ile yüksek kullanılabilirlik senaryolarını etkinleştirmek için herhangi bir plan vardır? <br/>
**A**: hello yol haritası üzerinde bu senaryolar verilmiştir ancak henüz bir zaman çizelgesi bulunmuyor.

## <a name="troubleshooting"></a>Sorun giderme

[!INCLUDE [existing-gateway-location-changed](../../includes/logic-apps-existing-gateway-location-changed.md)]

**Q**: nasıl sorguları toohello şirket içi veri kaynağına gönderilen görebilir? <br/>
**A**: gönderilen hello sorgular sorgu izlemeyi etkinleştirebilirsiniz. Sorun giderme tamamlanınca toohello özgün değeri geri izleme toochange sorgu unutmayın. Sorgu izlemesi açık bırakarak daha büyük günlükleri oluşturur.

Ayrıca, izleme sorguları için veri kaynağınız olan araçlar da bakabilirsiniz. Örneğin, SQL Server ve Analysis Services için genişletilmiş olaylar veya SQL Profiler kullanabilirsiniz.

**Q**: hello gateway günlükleri nerede? <br/>
**A**: Bu konunun ilerleyen bölümlerinde bkz araçları.

### <a name="update-toohello-latest-version"></a>Güncelleştirme toohello en son sürümü

Merhaba ağ geçidi sürümü güncel olmayan hale geldiğinde birçok sorunları ortaya. Genel iyi uygulama olarak, hello en son sürümünü kullandığınızdan emin olun. Merhaba ağ geçidi için ayda bir veya daha uzun güncelleştirmediyseniz hello hello ağ geçidinin en son sürümünü yüklemeyi göz önünde bulundurun ve hello sorunu yeniden bakın.

### <a name="error-failed-tooadd-user-toogroup--2147463168-pbiegwservice-performance-log-users"></a>Hata: tooadd kullanıcı toogroup başarısız oldu. (-2147463168 PBIEgwService performans günlük kullanıcılar)

Desteklenmeyen bir etki alanı denetleyicisinde tooinstall hello ağ geçidi çalışırsanız, bu hatayı alabilirsiniz. Bir etki alanı denetleyicisi olmayan bir makineyi hello geçidinde dağıttığınızdan emin olun.

## <a name="tools"></a>Araçlar

### <a name="collect-logs-from-hello-gateway-configurer"></a>Merhaba ağ geçidi configurer günlüklerini toplayın

Merhaba ağ geçidi için birkaç günlüklerini toplayabilir. Her zaman hello günlükleri ile başlayın!

#### <a name="installer-logs"></a>Yükleyici günlükleri

`%localappdata%\Temp\Power_BI_Gateway_–Enterprise.log`

#### <a name="configuration-logs"></a>Yapılandırma günlükleri

`%localappdata%\Microsoft\Power BI Enterprise Gateway\GatewayConfigurator.log`

#### <a name="enterprise-gateway-service-logs"></a>Kurumsal ağ geçidi hizmeti günlükleri

`C:\Users\PBIEgwService\AppData\Local\Microsoft\Power BI Enterprise Gateway\EnterpriseGateway.log`

#### <a name="event-logs"></a>Olay günlükleri

Veri Yönetimi ağ geçidi ve PowerBIGateway günlüklerini altında hello bulabilirsiniz **uygulama ve hizmet günlükleri**.

### <a name="fiddler-trace"></a>Fiddler'ı izleme

[Fiddler](http://www.telerik.com/fiddler) HTTP trafiği izler telerik'ten ücretsiz bir araçtır. Merhaba hello istemci makineden Power BI hizmeti ile bu trafiği görebilirsiniz. Bu hizmet, hataları ve diğer ilgili bilgileri gösterebilir.

## <a name="next-steps"></a>Sonraki adımlar
    
* [Mantığı uygulamalardan tooon içi verilere bağlanma](../logic-apps/logic-apps-gateway-connection.md)
* [Kurumsal tümleştirme özellikleri](../logic-apps/logic-apps-enterprise-integration-overview.md)
* [Azure mantıksal uygulamaları için bağlayıcılar](../connectors/apis-list.md)
