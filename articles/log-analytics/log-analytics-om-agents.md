---
title: aaaConnect Operations Manager tooLog Analytics | Microsoft Docs
description: "toomaintain varolan yatırımınızı System Center Operations Manager ve kullanım günlük analizi özellikleriyle genişletilmiş, OMS çalışma alanınızla Operations Manager tümleştirebilirsiniz."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 245ef71e-15a2-4be8-81a1-60101ee2f6e6
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: magoedte
ms.openlocfilehash: b2841c7aa209fec7357dc4c8b1ff4325fdaa37ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-operations-manager-toolog-analytics"></a>Operations Manager tooLog Analytics Bağlan
toomaintain varolan yatırımınızı System Center Operations Manager ve kullanım günlük analizi özellikleriyle genişletilmiş, OMS çalışma alanınızla Operations Manager tümleştirebilirsiniz.  Operations Manager toouse devam ederken OMS hello fırsatlarını yararlanan böylece için:

* Operations Manager ile BT Hizmetleri Hello durumunu izlemeye devam
* Olay ve sorun yönetimi destekleyen ITSM çözümlerinizi ile tümleştirme koru
* Merhaba yaşam döngüsü dağıtılan aracılar tooon içi ve Operations Manager ile izleme genel bulut Iaas sanal makineleri yönetme

System Center Operations Manager ile tümleştirme, değer tooyour hizmet işlemleri stratejisi hello hızı ve toplamak, depolamak ve Operations Manager'dan veri çözümleme OMS verimliliğini kullanarak ekler.  OMS ilişkilendirmenize yardımcı olur ve hello hataları sorunları tanımlamak ve varolan sorun yönetimi işleminizi desteklemek tekrarları görünmesini doğru çalışır.   Merhaba arama motoru tooexamine performans, olay ve uyarı verilerini, zengin panolarla esnekliğini hello ve yetenekleri tooexpose raporlama bu verileri anlamlı şekillerde gösterir hello gücü Operations Manager complimenting OMS getirir.

Merhaba aracıları toohello Operations Manager yönetim grubu raporlama hello günlük analizi veri kaynakları ve OMS aboneliğinizde etkin çözümleri göre sunucularınızdan veri toplar.  Etkinleştirdiğiniz hello bağlı olarak, bu çözümlerin verilerden toohello OMS web hizmeti veya nedeniyle hello hello aracıyla yönetilen sistemde, toplanan verilerin hacmi doğrudan gönderilir ya da doğrudan bir Operations Manager yönetim sunucusundan gönderilen çözümdür Merhaba Aracısı tooOMS web hizmetinden. toohello OMS web doğrudan hizmet hello yönetim sunucusu hello OMS veri iletir; hiçbir zaman toohello OperationsManager veya OperationsManagerDW veritabanı yazılmış olmalıdır.  Bir yönetim sunucusu hello OMS web hizmetiyle bağlantı kaybettiğinde, yerel olarak iletişim OMS ile yeniden kurulur kurulmaz kadar hello verileri önbelleğe alır.  Hello yönetim sunucusu tooplanned Bakım veya planlanmamış kesinti çevrimdışıysa hello yönetim grubundaki başka bir yönetim sunucusu bağlantısı OMS ile sürdürür.  

Merhaba Aşağıdaki diyagramda hello bağlantı hello yönetim sunucuları ve System Center Operations Manager yönetim grubu ve OMS hello yönü ve bağlantı noktaları da dahil olmak üzere, aracılar arasındaki gösterilmektedir.   

![OMS-işlemleri-manager-tümleştirme-diyagram](./media/log-analytics-om-agents/oms-operations-manager-connection.png)

BT güvenlik ilkelerinizi ağ tooconnect toohello Internet bilgisayarları izin vermiyorsa, yönetim sunucuları yapılandırılmış tooconnect toohello OMS ağ geçidi tooreceive yapılandırma bilgilerini ve değiştirebilirsiniz hello çözüm üzerinde bağlı olarak toplanan verileri gönder etkinleştirdiniz.  Daha fazla bilgi ve tooconfigure, Operations Manager yönetim grubu toocommunicate bir OMS ağ geçidi toohello OMS hizmeti aracılığıyla nasıl görürüm adımlar [hello OMS ağ geçidi kullanarak bilgisayarları tooOMS bağlanmak](log-analytics-oms-gateway.md).  

## <a name="system-requirements"></a>Sistem gereksinimleri
Başlamadan önce aşağıdaki önkoşulları karşıladığından ayrıntıları tooverify hello gözden geçirin.

* OMS yalnızca Operations Manager 2016, Operations Manager 2012 SP1 UR6 destekler ve daha büyük ve Operations Manager 2012 R2 UR2 büyük.  Operations Manager 2012 SP1 UR7 ve Operations Manager 2012 R2 UR3'e ara sunucu desteği eklenmiştir.
* Tüm Operations Manager aracıları, minimum destek gereksinimlerini karşılaması gerekir. Aracıları hello minimum güncelleştirmeyi, aksi takdirde Windows Aracısı trafiği başarısız olabilir ve birçok hata hello Operations Manager olay günlüğünü doldurma olduğundan emin olun.
* Bir OMS abonelik.  Daha fazla bilgi için gözden [günlük Analytics ile çalışmaya başlama](log-analytics-get-started.md).

### <a name="network"></a>Ağ
Merhaba Operations Manager Aracısı, yönetim sunucuları ve Operations Konsolu toocommunicate OMS ile gerekli listesi hello proxy ve güvenlik duvarı yapılandırma bilgilerini altındaki Hello bilgi.  Ağ toohello OMS hizmetinizden her bileşenin trafik gidendir.     

|Kaynak | Bağlantı noktası numarası| Atlama HTTP denetleme|  
|---------|------|-----------------------|  
|**Aracı**|||  
|\*.ods.opinsights.azure.com| 443 |Evet|  
|\*.oms.opinsights.azure.com| 443|Evet|  
|\*.blob.core.windows.net| 443|Evet|  
|\*.azure-automation.net| 443|Evet|  
|**Yönetim sunucusu**|||  
|\*.service.opinsights.azure.com| 443||  
|\*.blob.core.windows.net| 443| Evet|  
|\*.ods.opinsights.azure.com| 443| Evet|  
|*.azure-automation.net | 443| Evet|  
|**Operations Manager Konsolu tooOMS**|||  
|service.systemcenteradvisor.com| 443||  
|\*.service.opinsights.azure.com| 443||  
|\*.live.com| 80 ve 443||  
|\*.microsoft.com| 80 ve 443||  
|\*.microsoftonline.com| 80 ve 443||  
|\*.mms.microsoft.com| 80 ve 443||  
|login.windows.net| 80 ve 443||  


## <a name="connecting-operations-manager-toooms"></a>Operations Manager tooOMS bağlanma
Aşağıdaki adımları tooconfigure dizi Merhaba, Operations Manager yönetim grubu tooconnect tooone OMS alanlarınızın gerçekleştirin.

1. Merhaba Operations Manager konsolunda hello seçin **Yönetim** çalışma.
2. Merhaba Operations Management Suite düğümünü genişletin ve tıklatın **bağlantı**.
3. Merhaba tıklatın **tooOperations yönetim paketine kaydetmeniz** bağlantı.
4. Merhaba üzerinde **Operations Management Suite Ekleme Sihirbazı: kimlik doğrulaması** sayfasında hello e-posta adresi veya telefon numarasını ve OMS aboneliğinizle ilişkili hello yönetici hesabının parolasını girin ve tıklayın **Oturum**.
5. Başarılı bir şekilde, üzerinde hello doğrulandıktan sonra **Operations Management Suite Ekleme Sihirbazı: çalışma alanı seçin** olduğunuz sayfa, OMS çalışma alanınızı tooselect istenir.  Birden fazla çalışma alanı varsa, select hello hello Operations Manager yönetim grubu hello aşağı açılan listeden tooregister istiyor ve ardından çalışma **sonraki**.
   
   > [!NOTE]
   > Operations Manager, aynı anda yalnızca bir OMS çalışma destekler. Hello bağlantı ve hello önceki çalışma alanı ile kayıtlı tooOMS olan hello bilgisayarları OMS kaldırılır.
   > 
   > 
6. Merhaba üzerinde **Operations Management Suite Ekleme Sihirbazı: Özet** sayfasında, ayarlarınızı doğrulayın ve doğru olmaları durumunda tıklayın **oluşturma**.
7. Merhaba üzerinde **Operations Management Suite Ekleme Sihirbazı: son** sayfasında, **Kapat**.

### <a name="add-agent-managed-computers"></a>Aracıyla yönetilen bilgisayarlar Ekle
Tümleştirme OMS çalışma alanınızla yapılandırma sonra bu yalnızca OMS ile bir bağlantı kurar, tooyour yönetim grubuna raporlama hello aracılardan hiçbir veri toplanmadı. Hangi belirli aracıyla yönetilen bilgisayarlar için günlük analizi veri toplar yapılandırdıktan sonra bu kadar gerçekleşmez. Merhaba bilgisayar nesneleri tek tek seçebileceğiniz veya Windows bilgisayar nesnelerini içeren bir grup seçebilirsiniz. Mantıksal diskleri veya SQL veritabanları gibi başka bir sınıfın örneklerini içeren bir grup seçemezsiniz.

1. Açık hello Operations Manager konsolunu ve select hello **Yönetim** çalışma.
2. Merhaba Operations Management Suite düğümünü genişletin ve tıklatın **bağlantı**.
3. Merhaba tıklatın **bilgisayar/Grup Ekle** hello Eylemler altındaki bağlantı hello sağ tarafında hello bölmenin başlık.
4. Merhaba, **bilgisayar arama** iletişim kutusu, arayabilirsiniz bilgisayarları veya grupları Operations Manager tarafından izlenen. Bilgisayarları veya grupları tooonboard tooOMS seçin, **Ekle**ve ardından **Tamam**.

Bilgisayarları görüntüleyebilir ve grupları hello hello yönetilen bilgisayarlar Operations Management Suite düğümünde toocollect verileri yapılandırılmış **Yönetim** hello Operations konsolunun çalışma.  Buradan, ekleyin veya gerektiğinde bilgisayarları ve grupları kaldırın.

### <a name="configure-oms-proxy-settings-in-hello-operations-console"></a>Merhaba Operations konsolunda OMS proxy ayarlarını yapılandırın
Merhaba hello yönetim grubu ve OMS web hizmeti arasında bir iç proxy sunucu ise, aşağıdaki adımları gerçekleştirin.  Bu ayarlar, hello yönetim grubu ve hello kapsam toocollect verileri için OMS dahil edilen dağıtılmış tooagent yönetilen sistemlerden merkezi olarak yönetilir.  Bu, tooOMS web hizmeti doğrudan zaman belirli çözümleri hello yönetim sunucusu ve gönderme veri atlamak için faydalıdır.

1. Açık hello Operations Manager konsolunu ve select hello **Yönetim** çalışma.
2. Operations Management Suite genişletin ve ardından **bağlantıları**.
3. Hello OMS bağlantısı görünümü,'ı tıklatın **Proxy sunucusunu yapılandırma**.
4. Üzerinde **Operations Management Suite Sihirbazı: Proxy sunucusu** sayfasında, **bir proxy sunucu tooaccess hello Operations Management Suite kullanmak**, ve ardından başlangıç bağlantı noktası numarası, örneğin, http:// ile Merhaba URL'sini yazın corpproxy:80 ve ardından **son**.

Proxy sunucusu kimlik doğrulaması gerektiriyorsa, gerçekleştirmek hello aşağıdaki adımları tooconfigure kimlik bilgileri ve tooOMS hello yönetim grubundaki raporları toopropagate toomanaged bilgisayarlara gereken ayarları.

1. Açık hello Operations Manager konsolunu ve select hello **Yönetim** çalışma.
2. **RunAs Yapılandırması** altında, **Profiller**'i seçin.
3. Açık hello **System Center Advisor farklı çalıştır profili proxy'si** profili.
4. Hello farklı çalıştır profili Sihirbazı, bir farklı çalıştır hesabı Ekle toouse'ı tıklatın. Oluşturabileceğiniz bir [farklı çalıştır hesabı](https://technet.microsoft.com/library/hh321655.aspx) veya var olan bir hesap kullanın. Bu hesap toohave yeterli izinleri toopass hello proxy sunucu üzerinden olmalıdır.
5. tooset hesap toomanage Merhaba, seçin **seçilen sınıf, Grup veya nesne**, tıklatın **seçin...** ve ardından **grup...** tooopen hello **grup arama** kutusu.
6. İçin arama yapın ve ardından **Microsoft System Center Advisor Monitoring Server grubu**.  Tıklatın **Tamam** hello Grup tooclose hello seçtikten sonra **grup arama** kutusu.
7. Tıklatın **Tamam** tooclose hello **bir farklı çalıştır hesabı ekleyin** kutusu.
8. Tıklatın **kaydetmek** toocomplete hello Sihirbazı ve değişikliklerinizi kaydedin.

Merhaba bağlantısı oluşturulur ve hangi Aracıların toplamak ve veri tooOMS rapor yapılandırdıktan sonra hello aşağıdaki yapılandırma hello yönetim grubundaki mutlaka sırayla uygulanır:

* Merhaba farklı çalıştır hesabı **Microsoft.SystemCenter.Advisor.RunAsAccount.Certificate** oluşturulur.  Farklı Çalıştır hello profiliyle ilişkilendirildiği **Microsoft System Center Advisor çalıştırmak olarak profili Blob** ve iki sınıf - hedefleme **toplama sunucusuna** ve **Operations Manager yönetim grubu** .
* İki bağlayıcı oluşturulur.  Merhaba ilk adlandırılan **Microsoft.SystemCenter.Advisor.DataConnector** ve hello yönetim grubu tooOMS günlük tüm sınıfların örneklerinden üretilen tüm uyarılarını iletir bir abonelik ile otomatik olarak yapılandırılır Çözümlemeleri. Merhaba ikinci Bağlayıcıdır **Advisor Bağlayıcısı**, OMS web hizmeti ile iletişim ve veri paylaşımını sorumlu olduğu.
* Aracılar ve hello yönetim grubunda seçilmiş toocollect veri grupları toohello eklenen **Microsoft System Center Advisor Monitoring Server grubu**.

## <a name="management-pack-updates"></a>Yönetim Paketi güncelleştirmeleri
Yapılandırma tamamlandıktan sonra hello Operations Manager yönetim grubu hello OMS hizmeti ile bir bağlantı kurar.  Merhaba yönetim sunucusu hello web hizmeti ile eşitlenir ve hello formunda yönetim paketlerinin Operations Manager ile tümleştirerek etkinleştirdiğiniz hello çözümleri için güncelleştirilmiş yapılandırma bilgilerini almak.   Operations Manager, güncelleştirmeleri bu yönetim paketlerinin ve otomatik olarak denetler indirin ve kullanılabilir olduğunda bunları alır.  İki kurallar vardır özellikle, bu davranışı denetlemek:

* **Microsoft.SystemCenter.Advisor.MPUpdate** -hello temel OMS yönetim paketleri güncelleştirir. Varsayılan olarak her 12 saatte çalışır.
* **Microsoft.SystemCenter.Advisor.Core.GetIntelligencePacksRule** -çalışma alanınızda etkin çözüm yönetim paketleri güncelleştirir. Varsayılan olarak beş (5) dakikada bir çalışır.

Tooeither önlemek otomatik yükleme devre dışı bırakarak bu iki kural geçersiz kılma veya yeni bir yönetim paketi varsa ve indirilmesi ne sıklıkla hello yönetim sunucusu ile OMS toodetermine eşitleneceğini hello sıklığını değiştirin.  Merhaba adımları [nasıl tooOverride bir kural veya İzleyici](https://technet.microsoft.com/library/hh212869.aspx) toomodify hello **sıklığı** saniye toochange değerinde parametresiyle hello eşitleme zamanlaması veya hello değiştirmek **etkin**  parametresi toodisable hello kuralları.  Hedef hello Operations Manager yönetim grubu sınıfın tooall nesneleri geçersiz kılar.

Üretim yönetim grubunuzdaki Yönetim Paketi sürümleri denetlemek için var olan değişiklik denetimi işlemi aşağıdaki toocontinue istiyorsanız, hello kurallarını devre dışı bırakın ve bunları ne zaman güncelleştirmelerine izin belirli zamanlarda etkinleştirin. Ortamınızda bir geliştirme veya QA yönetim grubu olması ve Internet bağlantısı toohello sahipse, bu yönetim grubu bu senaryo bir OMS çalışma toosupport ile yapılandırabilirsiniz.  Bu tooreview verir ve üretim yönetim grubuna serbest bırakmadan önce hello yinelemeli hello OMS yönetim paketleri sürümlerini değerlendirin.

## <a name="switch-an-operations-manager-group-tooa-new-oms-workspace"></a>Bir Operations Manager Grup tooa geçiş yeni bir OMS çalışma alanı
1. Tooyour OMS abonelikte oturum ve bir çalışma alanında oluşturmak [Microsoft Operations Management Suite](http://oms.microsoft.com/).
2. Merhaba Operations Manager Yöneticiler rolünün ve select hello bir üyesi olan bir hesapla Operations Manager konsolunu Aç hello **Yönetim** çalışma.
3. Operations Management Suite genişletin ve seçin **bağlantıları**.
4. Select hello **yeniden yapılandırma işlemi Yönetim Paketi** hello Orta-tarafındaki hello bölmesini bağlantı.
5. Merhaba izleyin **Operations Management Suite Ekleme Sihirbazı** hello e-posta adresi veya telefon numarası ve yeni OMS çalışma alanınızla ilişkilendirilen hello yönetici hesabının parolasını girin.
   
   > [!NOTE]
   > Merhaba **Operations Management Suite Ekleme Sihirbazı: çalışma alanı seçin** sayfa kullanımda olan bir çalışma hello gösterir.
   > 
   > 

## <a name="validate-operations-manager-integration-with-oms"></a>OMS ile Operations Manager tümleştirmesini doğrula
OMS tooOperations Manager tümleştirmesi başarılı olduğunu doğrulamak birkaç farklı yolu vardır.

### <a name="tooconfirm-integration-from-hello-oms-portal"></a>Merhaba OMS Portalı'ndan tooconfirm tümleştirme
1. Merhaba OMS portalında hello tıklatın **ayarları** döşeme
2. Seçin **bağlı kaynakları**.
3. Merhaba System Center Operations Manager bölümü altındaki Hello tabloda hello veri son alındığında hello sayısıyla aracıları ve durum listelenen hello yönetim grubunun adını görmeniz gerekir.
   
   ![OMS ayarları connectedsources](./media/log-analytics-om-agents/oms-settings-connectedsources.png)
4. Not hello **çalışma alanı kimliği** hello sol taraftaki hello ayarları sayfasının altında değeri.  Bu Operations Manager yönetim grubunuzu karşı aşağıdaki doğrulayın.  

### <a name="tooconfirm-integration-from-hello-operations-console"></a>Merhaba Operations konsolundan tooconfirm tümleştirme
1. Açık hello Operations Manager konsolunu ve select hello **Yönetim** çalışma.
2. Seçin **yönetim paketleri** ve hello **arayın:** metin kutusuna **Danışmanı** veya **Intelligence**.
3. Etkinleştirdiğiniz hello çözümleri bağlı olarak, hello arama sonuçları listesinde karşılık gelen bir Yönetim Paketi bakın.  Örneğin, hello uyarı yönetimi çözümü etkinleştirilirse, hello Yönetim Paketi Microsoft System Center Advisor uyarı yönetim hello listesinde yerini alır.
4. Merhaba gelen **izleme** görüntülemek için toohello gidin **Operations Management Suite\Health durumu** görünümü.  Merhaba altında bir yönetim sunucusu seçin **yönetim sunucusu durumu** bölmesinde ve hello **ayrıntı görünümü** bölmesinde Onayla hello değer özelliği için **kimlik doğrulama hizmeti URI'si** Merhaba OMS çalışma alanı kimliği ile eşleşir
   
   ![OMS-OpsMgr-MG-authsvcuri-Property-MS](./media/log-analytics-om-agents/oms-opsmgr-mg-authsvcuri-property-ms.png)

## <a name="remove-integration-with-oms"></a>OMS ile tümleştirme Kaldır
Operations Manager yönetim grubu ve OMS çalışma arasında tümleştirme artık ihtiyaç duymadığınızda, birkaç gerekli adımları tooproperly Kaldır hello bağlantısını ve yapılandırmasını hello yönetim grubundaki vardır. Merhaba aşağıdaki yordam, yönetim grubunuzun hello başvuru silerek, OMS çalışma güncelleştirmek, hello OMS bağlayıcılarını silip ve OMS destekleyen yönetim paketlerini silin sahiptir.   

Operations Manager ile tümleştirerek etkinleştirdiğiniz hello çözümleri için yönetim paketleri ve hello OMS hizmeti ile Merhaba yönetim paketlerini gerekli toosupport tümleştirme kolayca hello yönetim grubundan silinemez.  Merhaba OMS yönetim paketlerinden başka ilgili yönetim paketlerine bağımlılıkları olan olmasıdır.  başka yönetim paketlerine bir bağımlılığa sahip toodelete yönetim paketlerini karşıdan hello betik [bağımlılıkları olan bir Yönetim paketini kaldırmak](https://gallery.technet.microsoft.com/scriptcenter/Script-to-remove-a-84f6873e) TechNet Komut Merkezi.  

1. Merhaba Operations Manager komut kabuğu hello Operations Manager Yöneticiler rolünün bir üyesi olan bir hesap ile açın.
   
    > [!WARNING]
    > Tüm özel yönetim paketlerinde hello word Danışmanı veya IntelligencePack ile devam etmeden önce hello adı sahip değilse, aksi takdirde aşağıdaki adımları hello bunları hello yönetim grubundan silin doğrulayın.
    > 

2. Merhaba komut kabuğu isteminde yazın`Get-SCOMManagementPack -name "*Advisor*" | Remove-SCOMManagementPack -ErrorAction SilentlyContinue`
3. Sonraki türü`Get-SCOMManagementPack -name “*IntelligencePack*” | Remove-SCOMManagementPack -ErrorAction SilentlyContinue`
4. diğer System Center Advisor yönetim bağımlılığı olan kalan herhangi bir Yönetim Paketi tooremove paketleri, hello komut dosyası kullanma *RecursiveRemove.ps1* önceki hello TechNet Komut Merkezi indirilir.  
 
    > [!NOTE]
    > Merhaba Microsoft System Center Danışmanı veya Microsoft System Center Advisor iç Yönetim Paketi silmeyin.  
    >  

5. Merhaba Operations Manager Yöneticiler rolünün bir üyesi olan bir hesapla Hello Operations Manager işletim konsolunu açın.
6. Altında **Yönetim**seçin hello **yönetim paketleri** düğümü ve hello **arayın:** kutusuna **Danışmanı** ve hello doğrulayın aşağıdaki yönetim paketleri hala yönetim grubunuza içeri:
   
   * Microsoft System Center Danışmanı
   * Microsoft System Center Advisor iç
7. Merhaba OMS portalında hello tıklatın **ayarları** döşeme.
8. Seçin **bağlı kaynakları**.
9. Merhaba System Center Operations Manager bölümü altındaki Hello tabloda hello adı görmelisiniz hello yönetim grubunun hello çalışma alanından tooremove istiyor.  Merhaba sütununun altında **son veri**, tıklatın **kaldırmak**.  
   
    > [!NOTE]
    > Merhaba **kaldırmak** bağlantı kullanılamayacak kadar 14 gün sonra hello bağlı yönetim grubundan algılanan etkinlik yoksa.  
    > 

10. Merhaba kaldırma ile tooproceed istediğiniz tooconfirm isteyen bir pencere görüntülenir.  Tıklatın **Evet** tooproceed. 

toodelete iki bağlayıcı - Microsoft.SystemCenter.Advisor.DataConnector ve Advisor Bağlayıcısı Merhaba, tooyour bilgisayar aşağıdaki hello PowerShell Betiği kaydedin ve örnek hello kullanarak yürütün:

```
    .\OM2012_DeleteConnector.ps1 “Advisor Connector” <ManagementServerName>
    .\OM2012_DeleteConnectors.ps1 “Microsoft.SytemCenter.Advisor.DataConnector” <ManagementServerName>
```

> [!NOTE]
> bir yönetim sunucusu değilse, bu komut dosyasını çalıştırmak hello bilgisayar hello Operations Manager komut kabuğu bağlı olarak, yönetim grubunuzun hello sürümünün yüklü olması gerekir.
> 
> 

```
    `param(
    [String] $connectorName,
    [String] $msName="localhost"
    )
    $mg = new-object Microsoft.EnterpriseManagement.ManagementGroup $msName
    $admin = $mg.GetConnectorFrameworkAdministration()
    ##########################################################################################
    # Configures a connector with hello specified name.
    ##########################################################################################
    function New-Connector([String] $name)
    {
         $connectorForTest = $null;
         foreach($connector in $admin.GetMonitoringConnectors())
    {
    if($connectorName.Name -eq ${name})
    {
         $connectorForTest = Get-SCOMConnector -id $connector.id
    }
    }
    if ($connectorForTest -eq $null)
    {
         $testConnector = New-Object Microsoft.EnterpriseManagement.ConnectorFramework.ConnectorInfo
         $testConnector.Name = $name
         $testConnector.Description = "${name} Description"
         $testConnector.DiscoveryDataIsManaged = $false
         $connectorForTest = $admin.Setup($testConnector)
         $connectorForTest.Initialize();
    }
    return $connectorForTest
    }
    ##########################################################################################
    # Removes a connector with hello specified name.
    ##########################################################################################
    function Remove-Connector([String] $name)
    {
        $testConnector = $null
        foreach($connector in $admin.GetMonitoringConnectors())
       {
        if($connector.Name -eq ${name})
       {
         $testConnector = Get-SCOMConnector -id $connector.id
       }
      }
     if ($testConnector -ne $null)
     {
        if($testConnector.Initialized)
     {
     foreach($alert in $testConnector.GetMonitoringAlerts())
     {
       $alert.ConnectorId = $null;
       $alert.Update("Delete Connector");
     }
     $testConnector.Uninitialize()
     }
     $connectorIdForTest = $admin.Cleanup($testConnector)
     }
    }
    ##########################################################################################
    # Delete a connector's Subscription
    ##########################################################################################
    function Delete-Subscription([String] $name)
    {
      foreach($testconnector in $admin.GetMonitoringConnectors())
      {
      if($testconnector.Name -eq $name)
      {
        $connector = Get-SCOMConnector -id $testconnector.id
      }
    }
    $subs = $admin.GetConnectorSubscriptions()
    foreach($sub in $subs)
    {
      if($sub.MonitoringConnectorId -eq $connector.id)
      {
        $admin.DeleteConnectorSubscription($admin.GetConnectorSubscription($sub.Id))
      }
     }
    }
    #New-Connector $connectorName
    write-host "Delete-Subscription"
    Delete-Subscription $connectorName
    write-host "Remove-Connector"
    Remove-Connector $connectorName
```

Merhaba gelecekteki, yönetim grubu tooan OMS çalışma ihtimalleri planlıyorsanız toore alma hello gerekir `Microsoft.SystemCenter.Advisor.Resources.\<Language>\.mpb` Yönetim Paketi hello en son güncelleştirme paketi dosyasından uygulanan tooyour yönetim grubu.  Bu dosyayı hello bulabilirsiniz `%ProgramFiles%\Microsoft System Center 2012` veya hello `System Center 2012 R2\Operations Manager\Server\Management Packs for Update Rollups` klasör.

## <a name="next-steps"></a>Sonraki adımlar
bkz: tooadd işlevselliği ve veri toplama, [hello Çözümleri Galerisi eklemek günlük analizi çözümleri](log-analytics-add-solutions.md).


