---
title: "kullanarak aaaConnect bilgisayarlar tooOMS hello OMS ağ geçidi | Microsoft Docs"
description: "Internet erişimi olmadığında, OMS tarafından yönetilen cihazlar ve Operations Manager izlenen bilgisayarlar hello OMS ağ geçidi toosend veri toohello OMS hizmetiyle bağlayın."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: ae9a1623-d2ba-41d3-bd97-36e65d3ca119
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: magoedte
ms.openlocfilehash: 0cfa8f2fb66016e494f22c780e328be472b5fdee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-computers-without-internet-access-toooms-using-hello-oms-gateway"></a>Internet erişimi tooOMS hello OMS ağ geçidi kullanarak bilgisayarları bağlama

Bu belgede, Internet erişimi olmadığında nasıl OMS tarafından yönetilen ve System Center Operations Manager izlenen bilgisayarlar veri toohello OMS Hizmeti'nin gönderebileceği açıklanmaktadır. Merhaba OMS HTTP tüneli destekleyen bir HTTP iletme proxy'si, ağ geçidi, veri toplamak ve onların adına toohello OMS hizmetine iletebilirsiniz HTTP BAĞLAMAK hello komutunu kullanarak.  

Merhaba OMS ağ geçidi destekler:

* Azure Otomasyon karma Runbook çalışanları  
* Windows bilgisayarları hello Microsoft İzleme Aracısı ile doğrudan bağlı tooan OMS çalışma
* Linux için OMS aracısının hello Linux bilgisayarlarla tooan OMS çalışma doğrudan bağlı  
* System Center Operations Manager 2012 SP1 UR7, Operations Manager 2012 R2 UR3 veya Operations Manager 2016 yönetim grubu ile OMS ile tümleşiktir.  

BT güvenlik ilkelerinizi bilgisayarlar noktası (POS) satış aygıtları veya BT Hizmetleri destekleyen sunucular gibi ağ tooconnect toohello Internet üzerinde izin vermez ancak tooconnect gerekiyorsa bunları tooOMS toomanage ve bunları izleme, bunlar yapılandırılabilir toocommunicate hello OMS ağ geçidi tooreceive yapılandırma ve verileri şirket adına ile doğrudan.  Bu bilgisayarlar hello OMS Aracısı toodirectly ile yapılandırılmışsa tooan OMS çalışma, tüm bilgisayarlar yerine hello OMS ağ geçidi ile iletişim kuracak bağlayın.  Merhaba aracıları tooOMS verileri Hello ağ geçidi doğrudan aktarır, bunu herhangi bir aktarım hello verileri analiz etmez.

Bir Operations Manager yönetim grubu OMS ile tümleştirildiğinde hello yönetim sunucuları yapılandırılmış tooconnect toohello OMS ağ geçidi tooreceive yapılandırma bilgilerini olması ve etkinleştirdiğiniz hello çözümüne bağlı olarak toplanan verileri gönderin.  Operations Manager aracıları Operations Manager uyarıları, yapılandırma değerlendirmesi, örnek alanı ve kapasite veri toohello yönetim sunucusu gibi bazı verileri gönderin. IIS günlükleri, performans ve güvenlik olayları gibi diğer yüksek hacimli verileri doğrudan toohello OMS ağ geçidi gönderilir.  Bir veya daha fazla Operations Manager ağ geçidi sunucusu güvenilmeyen sistemleri DMZ veya diğer yalıtılmış ağ toomonitor dağıtılmış, OMS ağ geçidi ile iletişim kuramıyor.  Operations Manager Ağ Geçidi sunucuları yalnızca rapor tooa yönetim sunucusu olabilir.  Bir Operations Manager yönetim grubu hello OMS ağ geçidi ile yapılandırılmış toocommunicate, hello proxy yapılandırma bilgilerini günlük analizi için yapılandırılmış toocollect verilerini otomatik olarak dağıtılmış tooevery aracıyla yönetilen bilgisayar olduğunda bile Merhaba ayarı boştur.    

tooprovide yüksek kullanılabilirlik için doğrudan bağlı veya OMS ile kullanabileceğiniz hello ağ geçidi üzerinden iletişim kuran, Operations Management grupları Ağ Yük Dengelemesi tooredirect ve hello trafiği birden fazla ağ geçidi sunucusu arasında dağıtma.  Bir ağ geçidi sunucusu kullanılamaz hale gelirse hello yeniden yönlendirilen tooanother kullanılabilir düğüm trafiğidir.  

Merhaba OMS Aracısı hello OMS ağ geçidi yazılım toomonitor hello OMS ağ geçidi çalıştıran hello bilgisayara yükleyin ve performans veya olay verileri çözümlemek önerilir. Ayrıca, hello Aracısı yardımcı hello OMS ağ geçidi ile toocommunicate gereken hello hizmet uç noktaları tanımlayın.

Her bir aracının, ağ bağlantısı tooits geçidi olması gerekir, böylece aracıları otomatik olarak hello ağ geçidi'nden veri tooand aktarabilirsiniz değil. Bir etki alanı denetleyicisinde yükleme hello ağ geçidi önerilmez.

Aşağıdaki diyagramda hello hello ağ geçidi sunucusu kullanarak doğrudan aracıları tooOMS veri akışından gösterir.  Aracıları aynı hello kendi proxy yapılandırması eşleşme olmalıdır bağlantı noktası hello OMS ağ geçidi tooOMS ile yapılandırılmış toocommunicate değil.  

![OMS diyagramı ile doğrudan aracı iletişimi](./media/log-analytics-oms-gateway/oms-omsgateway-agentdirectconnect.png)

Merhaba Aşağıdaki diyagramda bir Operations Manager yönetim grubu tooOMS veri akışından gösterilmektedir.   

![Operations Manager iletişim OMS diyagramı](./media/log-analytics-oms-gateway/oms-omsgateway-opsmgrconnect.png)

## <a name="prerequisites"></a>Ön koşullar

Bir bilgisayar toorun hello OMS ağ geçidi atandığında, bu bilgisayar hello şunlara sahip olmanız gerekir:

* Windows 10, Windows 8.1, Windows 7
* Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008
* .NET framework 4.5
* En az bir 4 çekirdekli işlemci ve 8 GB bellek

### <a name="language-availability"></a>Dil kullanılabilirliği

Merhaba OMS ağ geçidi dilleri aşağıdaki hello kullanılabilir:

- Çince (Basitleştirilmiş)
- Çince (Geleneksel)
- Çekçe
- Hollanda dili
- Türkçe
- Fransızca
- Almanca
- Macarca
- İtalyanca
- Japonca
- Kore dili
- Lehçe
- Portekizce (Brezilya)
- Portekizce (Portekiz)
- Rusça
- İspanyolca (uluslararası)

## <a name="download-hello-oms-gateway"></a>Merhaba OMS ağ geçidi indir

Üç yolu tooget hello en son sürümünü hello OMS ağ geçidi kurulum dosyası vardır.

1. Hello karşıdan [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=54443).

2. Merhaba OMS Portalı'ndan indirin.  Tooyour OMS çalışma alanında oturumu sonra çok gidin**ayarları** > **bağlı kaynakları** > **Windows sunucuları** tıklatıp**Karşıdan OMS ağ geçidi**.

3. Hello karşıdan [Azure portal](https://portal.azure.com).  Sonra oturum açın:  

   1. Merhaba hizmetlerin listesini bulun ve seçin **günlük analizi**.  
   2. Bir çalışma alanı seçin.
   3. Çalışma alanı dikey penceresinde altında **genel**, tıklatın **Hızlı Başlangıç**.
   4. Altında **bir veri kaynağı tooconnect toohello çalışma alanı seçin**, tıklatın **bilgisayarlar**.
   5. Merhaba, **doğrudan Aracısı** dikey penceresinde tıklatın **OMS ağ geçidi indirme**.<br><br> ![OMS ağ geçidini indirin](./media/log-analytics-oms-gateway/download-gateway.png)


## <a name="install-hello-oms-gateway"></a>Merhaba OMS ağ geçidi yükleyin

bir ağ geçidi tooinstall hello aşağıdaki adımları gerçekleştirin.  Önceki bir sürümü yüklü değilse adıysa *günlük analizi iletici*, olacak toothis sürüm yükseltme.  

1. Merhaba hedef klasöründen çift **OMS Gateway.msi**.
2. Merhaba üzerinde **Hoş Geldiniz** sayfasında, **sonraki**.<br><br> ![Ağ geçidi Kurulum Sihirbazı](./media/log-analytics-oms-gateway/gateway-wizard01.png)<br>
3. Merhaba üzerinde **Lisans Sözleşmesi'ni** sayfasında, **hello Lisans Sözleşmesi'hello koşullarını kabul ediyorum** tooagree toohello EULA'yı ve ardından **sonraki**.
4. Merhaba üzerinde **bağlantı noktası ve proxy adresi** sayfa:
   1. Türü hello TCP bağlantı noktası numarası toobe hello ağ geçidi için kullanılır. Kurulum, Windows Güvenlik Duvarı'nda bu bağlantı noktası numarasına sahip bir gelen kuralı yapılandırır.  8080 Hello varsayılan değerdir.
      Merhaba geçerli başlangıç bağlantı noktası numarası 1-65535 aralığındadır. Merhaba giriş bu aralığa uymazsa bir hata iletisi görüntülenir.
   2. Hello hello ağ geçidi olduğu sunucusu gereksinimlerini toocommunicate bir proxy üzerinden yüklediyseniz, isteğe bağlı olarak, burada tooconnect hello bir ağ geçidi oluşturulmalıdır hello proxy adresini yazın. Örneğin, `http://myorgname.corp.contoso.com:80`.  Boşsa, hello ağ geçidi tooconnect toohello Internet doğrudan deneyin.  Proxy sunucusu kimlik doğrulaması gerektiriyorsa, kullanıcı adı ve parola girin.<br><br> ![Ağ geçidi Sihirbazı proxy yapılandırması](./media/log-analytics-oms-gateway/gateway-wizard02.png)<br>   
   3. **İleri**’ye tıklayın.
5. Microsoft Update etkinleştirilmişse yoksa tooenable seçebileceğiniz hello Microsoft Update sayfası görüntülenir. Bir seçim yapın ve ardından **sonraki**. Aksi durumda, toohello sonraki adıma devam edin.
6. Merhaba üzerinde **hedef klasörü** sayfasında, ya da bırakın nerede tooinstall ağ geçidi istediğiniz ve ardından hello varsayılan klasör C:\Program Files\OMS ağ geçidi veya türü hello konumu **sonraki**.
7. Merhaba üzerinde **hazır tooinstall** sayfasında, **yükleme**. Kullanıcı hesabı denetimi isteme izni tooinstall görünebilir. Öyleyse **Evet**.
8. Kurulum tamamlandıktan sonra **son**. Hello hizmeti hello services.msc ek bileşenini açarak çalıştıran ve doğrulayın doğrulayabilirsiniz **OMS ağ geçidi** durum Hizmetleri ve hello listesinde görünür olan **çalıştıran**.<br><br> ![Hizmetleri – OMS ağ geçidi](./media/log-analytics-oms-gateway/gateway-service.png)  

## <a name="configure-network-load-balancing"></a>Ağ Yükü Dengeleme yapılandırma
Ağ Yükü Dengeleme (NLB Microsoft Ağ Yükü Dengeleme (NLB) veya donanım tabanlı yük dengeleyici kullanarak) kullanarak yüksek kullanılabilirlik için hello ağ geçidini yapılandırabilirsiniz.  Merhaba yük dengeleyici trafiği yönlendirerek yönetir hello kendi düğümlere hello OMS Aracısı bağlantılarından veya Operations Manager yönetim sunucuları istenen. Bir ağ geçidi sunucusu kullanılamaz hale gelirse hello trafiği yeniden yönlendirilen tooother düğümleri alır.

toolearn nasıl toodesign ve bir Windows Server 2016 Ağ Yükü Dengeleme kümesi dağıtma, bkz: [Ağ Yükü Dengeleme](https://technet.microsoft.com/windows-server-docs/networking/technologies/network-load-balancing).  Merhaba aşağıdaki adımlar nasıl tooconfigure Microsoft Ağ Yükü Dengeleme kümesini açıklar.  

1.  Merhaba Windows yönetici hesabıyla hello NLB kümesinin bir üyesi olan bir sunucuya oturum açın.  
2.  Sunucu Yöneticisi'nde Ağ Yükü Dengeleme Yöneticisi'ni açın, **Araçları**ve ardından **Ağ Yükü Dengeleme Yöneticisi**.
3. tooconnect bir OMS ağ geçidi sunucusu hello yüklü, Microsoft İzleme Aracısı ile Merhaba kümenin IP adresine sağ tıklayın ve ardından **ana bilgisayar Ekle tooCluster**.<br><br> ![Ağ Yükü Dengeleme Yöneticisi – konak tooCluster ekleyin](./media/log-analytics-oms-gateway/nlb02.png)<br>
4. Merhaba tooconnect istediğiniz hello Ağ Geçidi sunucusunun IP adresini girin.<br><br> ![Ağ Yükü Dengeleme Yöneticisi'ni – konak tooCluster ekleyin: bağlanma](./media/log-analytics-oms-gateway/nlb03.png)

## <a name="configure-oms-agent-and-operations-manager-management-group"></a>OMS aracısı ve Operations Manager yönetim grubu yapılandırma
Merhaba aşağıdaki bölümde nasıl tooconfigure doğrudan OMS Aracısı, bir Operations Manager yönetim grubu ya da Azure Otomasyon karma Runbook çalışanları hello OMS ağ geçidi toocommunicate OMS ile ile bağlı adımlar içerir.  

bkz: toounderstand gereksinimleri ve nasıl tooinstall hello OMS Aracısı'nı Windows bilgisayarlar tooOMS, doğrudan bağlanan adımlar [bağlanmak Windows bilgisayarları tooOMS](log-analytics-windows-agents.md) veya Linux bilgisayarları bakın [bağlanmak Linux bilgisayarları tooOMS](log-analytics-linux-agents.md).

### <a name="configuring-hello-oms-agent-and-operations-manager-toouse-hello-oms-gateway-as-a-proxy-server"></a>Merhaba OMS aracısı ve Operations Manager toouse hello OMS ağ geçidi bir proxy sunucusu olarak yapılandırma

### <a name="configure-standalone-oms-agent"></a>Tek başına OMS Aracısı'nı yapılandırma
Bkz: [hello Microsoft İzleme Aracısı ile proxy ve güvenlik duvarı ayarlarını yapılandırma](log-analytics-proxy-firewall.md) Aracısı toouse hello ağ geçidi bu durumda olduğu bir proxy sunucusu yapılandırma hakkında bilgi.  Ağ Yük Dengeleyici arkasında birden çok ağ geçidi sunucusu dağıttıysanız, hello OMS Aracısı proxy yapılandırmasını hello hello NLB sanal IP adresi şöyledir:<br><br> ![Microsoft İzleme Aracısı Özellikleri – Proxy ayarları](./media/log-analytics-oms-gateway/nlb04.png)

### <a name="configure-operations-manager---all-agents-use-hello-same-proxy-server"></a>Operations Manager yapılandırma - tüm aracıların hello kullan aynı proxy sunucu
Operations Manager tooadd hello ağ geçidi sunucusu yapılandırın.  Merhaba ayarı boş olsa bile hello proxy yapılandırmasını otomatik olarak Operations Manager tooOperations Yöneticisi, raporlama tooall aracıları uygulanır.

toouse hello ağ geçidi toosupport Operations Manager, bilmeniz gerekir:

* Microsoft Monitoring Agent (aracı sürümü – **8.0.10900.0** ve sonraki sürümler) hello Ağ Geçidi sunucusunda yüklenir ve toocommunicate istediğiniz hello OMS çalışma alanları için yapılandırılır.
* Hello ağ geçidi, Internet bağlantınız veya mu bağlı tooa proxy sunucusu olması gerekir.

> [!NOTE]
> Merhaba ağ geçidi için bir değer belirtmezseniz, boş değerler tooall aracıları atılır.


1. Açık hello Operations Manager konsolunu ve altında **Operations Management Suite**, tıklatın **bağlantı** ve ardından **Proxy sunucusunu yapılandırma**.<br><br> ![Operations Manager – Proxy sunucusunu yapılandırın](./media/log-analytics-oms-gateway/scom01.png)<br>
2. Seçin **bir proxy sunucu tooaccess hello Operations Management Suite kullanmak** ve başlangıç IP adresi hello OMS ağ geçidi sunucusu ya da hello NLB sanal IP adresini yazın. Merhaba ile başlatıldığından emin olmak `http://` öneki.<br><br> ![Operations Manager – proxy sunucusu adresi](./media/log-analytics-oms-gateway/scom02.png)<br>
3. **Son**'a tıklayın. Operations Manager sunucunuza bağlı tooyour OMS çalışma alanıdır.

### <a name="configure-operations-manager---specific-agents-use-proxy-server"></a>Operations Manager yapılandırma - belirli aracıları proxy sunucusu kullan
Büyük veya karmaşık ortamları için belirli sunucuları (veya gruplar) toouse hello OMS ağ geçidi sunucusu yalnızca isteyebilirsiniz.  Bu sunucular için hello Operations Manager Aracısı hello yönetim grubu için genel hello değeriyle doğrudan bu değeri olarak yazılır güncelleştirilemiyor.  Bunun yerine bu değerleri toooverride hello kullanılan kural toopush gerekir.

> [!NOTE]
> Aynı yapılandırma tekniği olabilir, birden çok OMS ağ geçidi sunucusu tooallow hello kullan ortamınızda kullanılan.  Örneğin, bir bölge başına temelinde belirtilen belirli OMS Ağ Geçidi sunucuları toobe gerektirebilir.

1. Açık hello Operations Manager konsolunu ve select hello **yazma** çalışma.  
2. Merhaba yazma çalışma alanında seçin **kuralları** hello tıklatıp **kapsam** hello Operations Manager araç çubuğunda. Bu düğme kullanılamıyorsa, toomake hello izleme bölmesinde bir nesne seçili bir klasör değil sahip olduğunuzdan emin denetleyin. Merhaba **kapsam Yönetim Paketi nesneleri** iletişim kutusunda ortak hedeflenen sınıfları, grupları veya nesneleri listesini görüntüler.
3. Tür **sistem durumu hizmeti** hello içinde **Ara** alan ve hello listeden seçin.  **Tamam** düğmesine tıklayın.  
4. Merhaba kuralını arayın **Danışmanı Proxy ayarı kural** ve hello Operations konsolu araç çubuğunda **geçersiz kılar** gelin ve ardından çok**geçersiz kılma hello Rule\For sınıfın belirli bir nesnesi: sistem durumu Hizmet** ve belirli bir nesneyi hello listeden seçin.  İsteğe bağlı olarak, hello sistem durumu hizmeti nesnesi içeren özel bir grup oluşturabilirsiniz hello sunucularının bu geçersiz kılma tooand tooapply istediğiniz sonra hello geçersiz kılma toothat grubu uygulayın.
5. Merhaba, **geçersiz kılma özellikleri** iletişim kutusunda, tooplace hello onay işareti **geçersiz kılma** sütun sonraki toohello **WebProxyAddress** parametresi.  Merhaba, **geçersiz kılma değeri** hello ile başlayan hello OMS ağ geçidi sunucusu sağlamaya hello URL alanına, `http://` öneki.
   >[!NOTE]
   > Bunu zaten otomatik olarak hello Microsoft System Center Advisor Monitoring Server grubu hedefleme hello Microsoft System Center Advisor Güvenli başvuru geçersiz kılma Yönetim Paketi içinde yer alan bir geçersiz kılma ile yönetilen olarak tooenable hello kuralı gerekmez.
   >
6. Merhaba Yönetim Paketi seçin **hedef Yönetim Paketi seçin** listelemek veya tıklatarak yeni bir korumasız Yönetim Paketi oluşturun **yeni**.
7. Değişikliklerinizi tamamladığınızda tıklatın **Tamam**.

### <a name="configure-for-automation-hybrid-workers"></a>Otomasyon karma çalışanları için yapılandırma
Ortamınızda Otomasyon karma Runbook çalışanları varsa, aşağıdaki adımları hello sağlamak el ile geçici geçici çözümler tooconfigure hello ağ geçidi toosupport bunları.

Aşağıdaki adımları hello tooknow hello hello Otomasyon hesabı bulunduğu Azure bölgesi gerekir. toolocate hello konumu:

1. İçinde toohello oturum [Azure portal](https://portal.azure.com/).
2. Hello Azure Otomasyon hizmetine seçin.
3. Merhaba uygun Azure Otomasyon hesabı seçin.
4. Kendi bölge altında görüntülemek **konumu**.<br><br> ![Azure portal – Otomasyon hesabı konumu](./media/log-analytics-oms-gateway/location.png)  

Her konum için tabloları tooidentify hello URL aşağıdaki hello kullan:

**İş çalışma zamanı veri hizmeti URL'leri**

| **konum** | **URL** |
| --- | --- |
| Orta Kuzey ABD |ncus-jobruntimedata-üretim-su1.azure-automation.net |
| Batı Avrupa |we-jobruntimedata-prod-su1.azure-automation.net |
| Orta Güney ABD |scus-jobruntimedata-prod-su1.azure-automation.net |
| Doğu ABD 2 |eus2-jobruntimedata-prod-su1.azure-automation.net |
| Orta Kanada |cc-jobruntimedata-prod-su1.azure-automation.net |
| Kuzey Avrupa |ne-jobruntimedata-prod-su1.azure-automation.net |
| Güneydoğu Asya |sea-jobruntimedata-prod-su1.azure-automation.net |
| Orta Hindistan |cid-jobruntimedata-prod-su1.azure-automation.net |
| Japonya |jpe-jobruntimedata-prod-su1.azure-automation.net |
| Avustralya |ase-jobruntimedata-prod-su1.azure-automation.net |

**Aracı hizmeti URL'leri**

| **konum** | **URL** |
| --- | --- |
| Orta Kuzey ABD |ncus-agentservice-üretim-1.azure-automation.net |
| Batı Avrupa |Biz-agentservice-üretim-1.azure-automation.net |
| Orta Güney ABD |scus-agentservice-üretim-1.azure-automation.net |
| Doğu ABD 2 |eus2-agentservice-üretim-1.azure-automation.net |
| Orta Kanada |cc-agentservice-üretim-1.azure-automation.net |
| Kuzey Avrupa |ne-agentservice-üretim-1.azure-automation.net |
| Güneydoğu Asya |SEA-agentservice-üretim-1.azure-automation.net |
| Orta Hindistan |CID-agentservice-üretim-1.azure-automation.net |
| Japonya |jpe-agentservice-üretim-1.azure-automation.net |
| Avustralya |Ana-agentservice-üretim-1.azure-automation.net |

Bilgisayarınızı bir karma Runbook çalışanı olarak otomatik olarak hello güncelleştirme yönetimi çözümü kullanarak düzeltme eki uygulama için kayıtlı değilse, aşağıdaki adımları izleyin:

1. Merhaba iş çalışma zamanı veri hizmeti URL'leri toohello izin verilen ana bilgisayar listesi hello OMS ağ geçidi üzerinde ekleyin. Örneğin, `Add-OMSGatewayAllowedHost we-jobruntimedata-prod-su1.azure-automation.net`
2. Merhaba OMS ağ geçidi hizmeti hello aşağıdaki PowerShell cmdlet'ini kullanarak yeniden başlatın:`Restart-Service OMSGatewayService`

Bilgisayarınız dahil edilmiş tooAzure Otomasyon hello karma Runbook çalışanı kayıt cmdlet'ini kullanarak ise, şu adımları izleyin:

1. Hello Aracısı hizmeti kayıt URL toohello izin konak listesi hello OMS ağ geçidi üzerinde ekleyin. Örneğin, `Add-OMSGatewayAllowedHost ncus-agentservice-prod-1.azure-automation.net`
2. Merhaba iş çalışma zamanı veri hizmeti URL'leri toohello izin verilen ana bilgisayar listesi hello OMS ağ geçidi üzerinde ekleyin. Örneğin, `Add-OMSGatewayAllowedHost we-jobruntimedata-prod-su1.azure-automation.net`
3. Merhaba OMS ağ geçidi hizmeti yeniden başlatın.
    `Restart-Service OMSGatewayService`

## <a name="useful-powershell-cmdlets"></a>Yararlı PowerShell cmdlet'leri
Cmdlet gerekli tooupdate hello OMS ağ geçidi yapılandırma ayarları görevleri tamamlamanıza yardımcı olabilir. Kullanmadan önce emin olun:

1. Merhaba OMS ağ geçidi (MSI) yükleyin.
2. Bir PowerShell konsol penceresi açın.
3. tooimport hello modülü, bu komutu yazın:`Import-Module OMSGateway`
4. Merhaba önceki adımda herhangi bir hata oluştu, hello modülü başarıyla içeri aktarıldı ve hello cmdlet'leri kullanılabilir. Türü`Get-Module OMSGateway`
5. Merhaba cmdlet'lerini kullanarak değişiklikleri yaptıktan sonra hello ağ geçidi hizmeti yeniden emin olun.

3. adımında bir hata alırsanız, hello modülü içeri değildi. PowerShell oluşturulamıyor toofind hello modülü olduğunda hello hata oluşabilir. Merhaba ağ geçidi yükleme yolunda bulabilirsiniz: *C:\Program Files\Microsoft OMS Gateway\PowerShell*.

| **Cmdlet'i** | **Parametreler** | **Açıklama** | **Örnek** |
| --- | --- | --- | --- |  
| `Get-OMSGatewayConfig` |Anahtar |Merhaba hizmetinin başlangıç yapılandırmasını alır |`Get-OMSGatewayConfig` |  
| `Set-OMSGatewayConfig` |Anahtarı (gerekli) <br> Değer |Değişiklikleri hello hizmetinin yapılandırmasını hello |`Set-OMSGatewayConfig -Name ListenPort -Value 8080` |  
| `Get-OMSGatewayRelayProxy` | |Geçiş (Yukarı Akış) proxy Hello adresini alır |`Get-OMSGatewayRelayProxy` |  
| `Set-OMSGatewayRelayProxy` |Adres<br> Kullanıcı adı<br> Parola |Merhaba adresini (ve kimlik bilgileri) geçiş (Yukarı Akış) proxy'si ayarlar |1. Bir geçiş proxy ve kimlik bilgilerini ayarlayın:<br> `Set-OMSGatewayRelayProxy`<br>`-Address http://www.myproxy.com:8080`<br>`-Username user1 -Password 123` <br><br> 2. Kimlik doğrulama gerekmez geçiş proxy ayarlayın:`Set-OMSGatewayRelayProxy`<br> `-Address http://www.myproxy.com:8080` <br><br> 3. Clear hello geçiş proxy ayarı:<br> `Set-OMSGatewayRelayProxy` <br> `-Address ""` |  
| `Get-OMSGatewayAllowedHost` | |(Merhaba yerel olarak yapılandırılmış izin verilen ana içermez yalnızca otomatik olarak indirilen izin verilen ana bilgisayarları) şu anda izin verilen ana bilgisayar alır hello |`Get-OMSGatewayAllowedHost` |
| `Add-OMSGatewayAllowedHost` |Ana bilgisayar (gerekli) |İzin verilen listesine hello konak toohello ekler |`Add-OMSGatewayAllowedHost -Host www.test.com` |  
| `Remove-OMSGatewayAllowedHost` |Ana bilgisayar (gerekli) |İzin verilen listesine hello Hello konak kaldırır |`Remove-OMSGatewayAllowedHost`<br> `-Host www.test.com` |  
| `Add-OMSGatewayAllowedClientCertificate` |Konu (gerekli) |Merhaba istemci sertifikası konu toohello izin verilen listesine ekler |`Add-OMSGatewayAllowed`<br>`ClientCertificate` <br> `-Subject mycert` |  
| `Remove-OMSGatewayAllowedClientCertificate` |Konu (gerekli) |İzin verilen listesine hello Hello istemci sertifikası konu kaldırır |`Remove-OMSGatewayAllowed` <br> `ClientCertificate` <br> `-Subject mycert` |  
| `Get-OMSGatewayAllowedClientCertificate` | |Alır hello sertifika konuları istemci şu anda izin verilen (izin verilen konuları hello yerel olarak yapılandırılmış yalnızca otomatik olarak indirilen izin verilen konuları içermez) |`Get-`<br>`OMSGatewayAllowed`<br>`ClientCertificate` |  

## <a name="troubleshooting"></a>Sorun giderme
Merhaba ağ geçidi tarafından günlüğe kaydedilen toocollect olaylar tooalso ihtiyacınız hello OMS aracısının yüklü olması.<br><br> ![Olay Görüntüleyicisi'ni – OMS ağ geçidi günlük](./media/log-analytics-oms-gateway/event-viewer.png)

**OMS ağ geçidi olay kimlikleri ve açıklamaları**

Merhaba aşağıdaki tabloda gösterildiği olay kimlikleri ve açıklamaları OMS ağ geçidi günlük olayları için hello.

| **ID** | **Açıklama** |
| --- | --- |
| 400 |Belirli bir Kimliğe sahip olmayan herhangi bir uygulama hatası |
| 401 |Yanlış yapılandırma. Örneğin: listenPort tamsayı yerine "metin" = |
| 402 |TLS el sıkışma iletileri ayrıştırılırken bir özel durum |
| 403 |Ağ hatası. Örneğin: tootarget sunucusuna bağlanamıyor |
| 100 |Genel bilgiler |
| 101 |Hizmeti başlatıldı |
| 102 |Hizmeti durdu |
| 103 |Bir HTTP BAĞLAMAK komutu istemciden alınan |
| 104 |Olmayan bir HTTP BAĞLAMAK komutu |
| 105 |Hedef sunucuda izin verilen listesindeki değil veya hello hedef bağlantı noktası güvenli bağlantı noktası (443) değil <br> <br> Bu hello MMA aracı, ağ geçidi sunucunuzda emin olun ve ağ geçidi hello ile iletişim kurmasını hello aracılardır bağlı toohello aynı günlük analizi çalışma alanı. |
| 105 |HATA TcpConnection – geçersiz bir istemci sertifikası: CN = ağ geçidi <br><br> Emin olun: <br>    <br> &#149; 1.0.395.0 sürüm numarasına sahip bir ağ geçidi kullanarak veya daha büyük. <br> &#149; Merhaba MMA Aracısı'nı, ağ geçidi sunucusu ve ağ geçidi hello ile iletişim kurmasını hello aracıları bağlı toohello olan aynı günlük analizi çalışma alanı. |
| 106 |Şüpheli ve reddedilen hello TLS oturumu herhangi bir nedenle |
| 107 |Merhaba TLS oturumu doğrulandı |

**Performans sayaçları toocollect**

Merhaba aşağıdaki tabloda hello OMS ağ geçidi için kullanılabilen hello performans sayaçlarını gösterir. Performans İzleyicisi'ni kullanarak hello sayaçlar ekleyebilirsiniz.

| **Ad** | **Açıklama** |
| --- | --- |
| OMS ağ geçidi/etkin istemci bağlantısı |Etkin istemci (TCP) ağ bağlantısı sayısı |
| OMS ağ geçidi/hata sayısı |Hata sayısı |
| OMS ağ geçidi ve bağlı istemci |Bağlı istemci sayısı |
| OMS ağ geçidi/reddetme sayısı |Tooany TLS doğrulama hatası nedeniyle reddi sayısı |

![OMS ağ geçidi performans sayaçları](./media/log-analytics-oms-gateway/counters.png)

## <a name="get-assistance"></a>Yardım alın
Oturum açmış Azure portal toohello olduğunuzda, Yardım için bir istek hello OMS ağ geçidi veya herhangi başka Azure hizmeti veya özellik, bir hizmetin ile oluşturabilirsiniz.
toorequest Yardım hello soru işareti sembolü hello sağ üst köşesinde hello portal'ı tıklatın ve ardından **yeni destek isteği**. Ardından, hello yeni destek isteği formu tamamlayın.

![Yeni destek isteği](./media/log-analytics-oms-gateway/support.png)

Merhaba, OMS veya günlük analizi hakkında geri bildirim de bırakabilirsiniz [Microsoft Azure geri bildirim Forumunda](https://feedback.azure.com/forums/267889).

## <a name="next-steps"></a>Sonraki adımlar
* [Veri kaynakları ekleyin](log-analytics-data-sources.md) toocollect verilerden bağlı kaynakları OMS çalışma alanınızdaki hello ve hello OMS deposunda saklayın.
