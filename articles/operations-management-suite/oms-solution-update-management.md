---
title: "aaaUpdate OMS Yönetimi çözümünde | Microsoft Docs"
description: "Hedeflenen toohelp nasıl toouse Bu çözüm toomanage Windows ve Linux bilgisayarlar için güncelleştirmeleri anlayın makaledir."
services: operations-management-suite
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: e33ce6f9-d9b0-4a03-b94e-8ddedcc595d2
ms.service: operations-management-suite
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/27/2017
ms.author: magoedte
ms.openlocfilehash: 2dd321913bf049ab1996fd60a2f74b8417084dcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="update-management-solution-in-oms"></a>OMS’de Güncelleştirme Yönetimi çözümü

![Güncelleştirme Yönetimi sembolü](./media/oms-solution-update-management/update-management-symbol.png)

Merhaba OMS güncelleştirme yönetimi çözümünde toomanage işletim sistemi güvenlik güncelleştirmeleri, Azure'da dağıtılan, Windows ve Linux bilgisayarlar için sağlar ortamları ya da diğer bulut sağlayıcıları şirket içi.  Hızlı bir şekilde tüm aracı bilgisayarlarda kullanılabilir güncelleştirmeleri hello durumunu değerlendirmek ve sunucular için gerekli güncelleştirmeleri yükleme işleminin hello yönetin.


## <a name="solution-overview"></a>Çözüme genel bakış
OMS tarafından yönetilen bilgisayarlar, değerlendirme ve güncelleştirme dağıtımları gerçekleştirmek için hello aşağıdakileri kullanın:

* Windows veya Linux için OMS aracısı
* Linux için PowerShell İstenen Durum Yapılandırması (DSC)
* Otomasyon Karma Runbook Çalışanı
* Windows bilgisayarları için Microsoft Update veya Windows Server Update Hizmetleri

Windows Server ve Linux bilgisayarları bir çalışma alanında nasıl hello çözüm değerlendirir ve güvenlik güncelleştirmeleri tooall geçerlidir ile Merhaba davranış ve veri akışının kavramsal görünümü bağlı diyagramları aşağıdaki hello gösterir.    

#### <a name="windows-server"></a>Windows Server
![Windows Server güncelleştirme yönetimi işlem akışı](media/oms-solution-update-management/update-mgmt-windows-updateworkflow.png)

#### <a name="linux"></a>Linux
![Linux güncelleştirme yönetimi işlem akışı](media/oms-solution-update-management/update-mgmt-linux-updateworkflow.png)

Merhaba bilgisayar, güncelleştirme uyumluluğu için tarama gerçekleştirir sonra hello OMS Aracısı toplu tooOMS hello bilgileri iletir. Bir pencere bilgisayarda hello Uyumluluk taraması, varsayılan olarak her 12 saatte gerçekleştirilir.  Ayrıca toohello tarama zamanlaması, güncelleştirme uyumluluğu için tarama hello hello Microsoft İzleme Aracısı'nı (MMA) yeniden başlatıldı, önceki tooupdate yüklemeyse 15 dakika içinde ve güncelleştirme yüklemesi sonrasında başlatılır.  Bir Linux bilgisayarı ile Merhaba Uyumluluk taraması 3 saatte varsayılan olarak gerçekleştirilir ve hello MMA aracısı yeniden başlatılırsa bir Uyumluluk taraması 15 dakika içinde başlatılır.  

Merhaba uyumluluk bilgileri daha sonra işlenir ve hello çözüm veya kullanıcı tanımlı aranabilir kullanarak veya öncesi dahil hello panolar özetlenir-sorguları tanımlı.  Merhaba çözüm raporları nasıl güncel hello bilgisayar ile yapılandırılmış toosynchronize, hangi kaynak bulunduğunuz dayanır.  Merhaba Windows bilgisayar WSUS en son Microsoft Update ile eşitlenen zaman bağlı olarak yapılandırılmış tooreport tooWSUS ise hello sonuçları ne Microsoft Updates gösterir farklı olabilir.  Merhaba aynı Linux bilgisayarlar için ortak depodaki karşı tooreport tooa Yerel Depodaki yapılandırılmış.   

Dağıtabilir ve yazılım güncelleştirmelerini zamanlanmış dağıtım oluşturarak hello güncelleştirmesini gerektiren bilgisayarlara yükleyin.  Güncelleştirmeleri sınıflandırılmış olarak *isteğe bağlı* hello dağıtım kapsamında Windows bilgisayarları için gerekli güncelleştirmeleri yalnızca dahil edilmez.  Merhaba zamanlanmış dağıtım hangi hedef bilgisayarlara hello geçerli güncelleştirmeleri, açıkça bilgisayar belirtilmesi veya seçerek alacak tanımlayan bir [bilgisayar grubu](../log-analytics/log-analytics-computer-groups.md) belirli bir dizi günlük aramaları dışına dayalı bilgisayarlar.  Ayrıca bir zamanlama tooapprove belirtin ve güncelleştirmeleri yüklü toobe ne zaman izin verilen süreyi belirleyebilirsiniz.  Güncelleştirmeler Azure Automation’daki runbook'lar tarafından yüklenir.  Bu runbook’ları görüntüleyemezsiniz ve bunlar için herhangi bir yapılandırma gerekmez.  Bir güncelleştirme dağıtım oluşturulduğunda başlatır zaman hello bulunan bilgisayarlar için ana güncelleştirme runbook hello sırasında belirtilen bir zamanlama oluşturur.  Bu ana runbook, gerekli güncelleştirmelerin yüklemesini gerçekleştiren her aracıda bir alt runbook başlatır.       

Merhaba tarih ve saatte hello güncelleştirme dağıtımında belirtilen, hello hedef bilgisayarlara hello dağıtım paralel olarak yürütür.  Bir tarama ilk gerçekleştirilen tooverify hello güncelleştirmesidir hala gereklidir ve bunları yükler.  Toonote hello güncelleştirmeleri WSUS, hello güncelleştirme dağıtımı onaylanmazsa WSUS istemci bilgisayarların, başarısız olur önemlidir.  Merhaba uygulanan güncelleştirmeleri Hello sonuçlarını işlenir ve hello panolar veya hello olayları arama hello özetlenen tooOMS toobe iletilir.     

## <a name="prerequisites"></a>Ön koşullar
* Merhaba çözüm karşı Windows Server 2008 ve daha yüksek performanslı güncelleştirme değerlendirmeleri destekler ve güncelleştirme dağıtımları Windows Server 2008 R2 SP1 karşı ve daha yüksek.  Sunucu Çekirdeği ve Nano Sunucu yükleme seçenekleri desteklenmez.

    > [!NOTE]
    > Güncelleştirmeleri tooWindows Server 2008 R2 SP1'i dağıtmak için desteği, .NET Framework 4.5 ve WMF 5.0 veya sonrasını gerektirir.
    >  
* Windows istemci işletim sistemleri desteklenmez.  
* Windows aracılarının ya da bir Windows Server Update Services (WSUS) sunucusu ile yapılandırılmış toocommunicate olması veya erişim tooMicrosoft güncelleştirme sahip olmanız gerekir.  

    > [!NOTE]
    > Merhaba Windows Aracısı eşzamanlı olarak System Center Configuration Manager tarafından yönetilemez.  
    >
* CentOS 6 (x86/x64) ve 7 (x64)  
* Red Hat Enterprise 6 (x86/x64) ve 7 (x64)  
* SUSE Linux Enterprise Server 11 (x86/x64) ve 12 (x64)  
* Ubuntu 12.04 LTS ve daha yeni x86/x64   
    > [!NOTE]  
    > Ubuntu üzerinde bir bakım penceresi dışında uygulanmakta tooavoid güncelleştirmeleri Katılımsız Yükseltme paketi toodisable otomatik güncelleştirmeler yeniden yapılandırın. Hakkında bilgi için tooconfigure buna ek olarak, bkz: [hello Ubuntu Server Kılavuzu otomatik güncelleştirmeler konudaki](https://help.ubuntu.com/lts/serverguide/automatic-updates.html).

* Linux aracılarını erişim tooan güncelleştirme deposu olması gerekir.  

    > [!NOTE]
    > Linux tooreport toomultiple OMS çalışma alanları yapılandırılmış için bir OMS Aracısı bu çözüm ile desteklenmiyor.  
    >

Nasıl tooinstall Linux için OMS aracısının hello ve hello en son sürümü karşıdan yüklemek hakkında ek bilgi için çok başvuran[Linux için Operations Management Suite Aracısı](https://github.com/microsoft/oms-agent-for-linux).  Nasıl tooinstall hello için OMS Aracısı Windows hakkında daha fazla bilgi için gözden [Operations Management Suite aracısının for Windows](../log-analytics/log-analytics-windows-agents.md).  

### <a name="permissions"></a>İzinler
Sipariş toocreate güncelleştirme dağıtımları, Automation hesabı ve günlük analizi çalışma alanı hello katkıda bulunan rolü verilen toobe gerekir.  

## <a name="solution-components"></a>Çözüm bileşenleri
Bu çözüm tooyour Otomasyon hesabı ve doğrudan bağlı aracısı veya Operations Manager bağlı yönetim grubuna eklenen kaynaklar aşağıdaki hello oluşur.

### <a name="management-packs"></a>Yönetim paketleri
System Center Operations Manager yönetim grubunuzu bağlı tooan OMS çalışma ise, yönetim paketleri aşağıdaki hello Operations Manager'da yüklenir.  Bu çözüm eklendikten sonra bu yönetim paketleri doğrudan bağlı Windows bilgisayarlarına da yüklenir. Hiçbir şey tooconfigure veya bu yönetim paketleri ile yönetin.

* Microsoft System Center Advisor Update Assessment Intelligence Pack (Microsoft.IntelligencePacks.UpdateAssessment)
* Microsoft.IntelligencePack.UpdateAssessment.Configuration (Microsoft.IntelligencePack.UpdateAssessment.Configuration)
* MP Dağıtımını güncelleştirme

Çözüm yönetim paketleri güncelleştirilme biçimini daha fazla bilgi için bkz: [Operations Manager bağlanmak tooLog Analytics](../log-analytics/log-analytics-om-agents.md).

### <a name="hybrid-worker-groups"></a>Karma Çalışanı grupları
Bu çözüm etkinleştirdikten sonra herhangi bir Windows bilgisayarda OMS çalışma alanını otomatik olarak bu çözümde bulunan bir karma Runbook çalışanı toosupport hello runbook'lar olarak yapılandırılmış tooyour doğrudan bağlı.  Merhaba çözümü tarafından yönetilen her Windows bilgisayar için hello karma Runbook çalışan grupları dikey penceresinde hello adlandırma kuralı aşağıdaki hello Otomasyon hesabının altında listelenecektir *ana bilgisayar adı FQDN_GUID*.  Hesabınızdaki runbook’larla bu grupları hedefleyemezsiniz, aksi takdirde başarısız olur. Bu yalnızca hedeflenen toosupport hello yönetimi çözümü gruplarıdır.   

Ancak, ekleyin hello Windows bilgisayarları tooa karma Runbook çalışanı grubunu, Otomasyon hesabı toosupport Otomasyon runbook'ları hello çözüm ve karma Runbook çalışanı grup üyeliği için aynı hesabı hello kullanmakta olduğunuz sürece.  Bu işlev tooversion 7.2.12024.0 hello karma Runbook çalışanı olarak eklendi.  

## <a name="configuration"></a>Yapılandırma
Aşağıdaki adımları tooadd hello güncelleştirme yönetimi çözümü tooyour OMS çalışma hello gerçekleştirmek ve aracıları raporlama onaylayın. Windows aracılarının zaten bağlı tooyour çalışma ek bir yapılandırma olmadan otomatik olarak eklenir.

Merhaba çözümü yöntemlerini aşağıdaki hello kullanarak dağıtabilirsiniz:

* Azure Marketi'ndeki hello hello otomasyon ve denetim teklifi veya güncelleştirme yönetimi çözümü seçerek Azure portalı
* OMS Çözümleri Galerisi OMS çalışma alanınızdaki Hello

Bir Otomasyon hesabı ve bağlı OMS çalışma zaten varsa hello bir araya aynı kaynak grubunu ve bölge, otomasyon ve denetim seçme yapılandırmanızı doğrulayın ve yalnızca hello çözüm yükleyecek ve her iki hizmet yapılandırın.  Azure Marketi'nden Hello güncelleştirme yönetimi çözümü seçme sunuyor aynı davranışı hello.  Aboneliğinizde dağıtılan ya da hizmetleri yoksa hello hello adımları **yeni çözüm oluşturmak** dikey ve istediğiniz diğer tooinstall hello önceden seçilmiş önerilen çözümleri onaylayın.  İsteğe bağlı olarak, OMS çalışma hello adımları kullanarak açıklanan hello güncelleştirme yönetimi çözümü tooyour ekleyebilirsiniz [eklemek OMS çözümleri](../log-analytics/log-analytics-add-solutions.md) hello Çözümleri Galerisi gelen.  

### <a name="confirm-oms-agents-and-operations-manager-management-group-connected-toooms"></a>OMS aracıları ve Operations Manager yönetim grubu bağlı tooOMS onaylayın

tooconfirm OMS Aracısı Linux için doğrudan bağlı ve Windows OMS ile iletişim kuran birkaç dakika sonra günlük arama aşağıdaki hello çalıştırabilirsiniz:

* Linux - `Type=Heartbeat OSType=Linux | top 500000 | dedup SourceComputerId | Sort Computer | display Table`.  

* Windows - `Type=Heartbeat OSType=Windows | top 500000 | dedup SourceComputerId | Sort Computer | display Table`

Bir Windows bilgisayarda OMS Aracısı bağlanabilirlik tooverify aşağıdaki hello gözden geçirebilirsiniz:

1.  Açık Microsoft Monitoring Agent Denetim Masası'ndaki ve hello üzerinde **Azure günlük analizi (OMS)** sekmesinde, hello Aracısı belirten bir ileti görüntüler: **hello Microsoft İzleme Aracısı toohello Microsoft başarıyla bağlandı Operations Management Suite hizmeti**.   
2.  Merhaba Windows olay günlüğünü açın, çok gidin**uygulama ve Hizmetleri Logs\Operations Yöneticisi** ve hizmet Bağlayıcısı kaynağından olay kimliği 3000 ve 5002 arayın.  Bu olaylar hello bilgisayar hello OMS çalışma alanıyla kayıtlı olan ve yapılandırmayı almayı gösterir.  

Merhaba Aracısı mümkün toocommunicate hello OMS hizmetine sahip değil ve hello ile yapılandırılmış toocommunicate ise bir güvenlik duvarı veya proxy sunucu üzerinden Internet'e onaylayın hello güvenlik duvarı veya proxy sunucusu düzgün yapılandırılmış gözden geçirerek [ağ Windows aracısı için yapılandırma](../log-analytics/log-analytics-windows-agents.md#network) veya [Linux aracısı için ağ yapılandırması](../log-analytics/log-analytics-agent-linux.md#network).

> [!NOTE]
> Linux sistemleridir bir proxy veya OMS ağ geçidi ile yapılandırılmış toocommunicate ve onboarding eminseniz bu çözüm, lütfen hello güncelleştirin *proxy.conf* izinler toogrant hello omiuser grubuna Okuma izni tarafından hello dosyada Aşağıdaki komutları hello gerçekleştirme:  
> `sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/proxy.conf`  
> `sudo chmod 644 /etc/opt/microsoft/omsagent/proxy.conf`


Yeni eklenen Linux aracılarında, değerlendirme yapıldıktan sonra **Güncelleştirildi** durumu gösterilir.  Bu işlem too6 saat sürebilir.

tooconfirm bir Operations Manager yönetim grubu OMS ile iletişim kurmasını bkz [OMS ile Operations Manager tümleştirmesini doğrulama](../log-analytics/log-analytics-om-agents.md#validate-operations-manager-integration-with-oms).

## <a name="data-collection"></a>Veri toplama
### <a name="supported-agents"></a>Desteklenen aracılar
Aşağıdaki tablonun hello bu çözümü tarafından desteklenen hello bağlı kaynakları açıklar.

| Bağlı Kaynak | Destekleniyor | Açıklama |
| --- | --- | --- |
| Windows aracıları |Evet |Merhaba çözüm Windows aracılardan sistem güncelleştirmeleri hakkında bilgi toplar ve gerekli güncelleştirmeleri yüklemesini başlatır. |
| Linux aracıları |Evet |Merhaba çözüm Linux aracılarını sistem güncelleştirmeleri hakkında bilgi toplar ve desteklenen distro'lar gerekli güncelleştirmeleri yüklemesini başlatır. |
| Operations Manager yönetim grubu |Evet |Merhaba çözüm aracıları bağlı Yönetim grubundaki sistem güncelleştirmeleri hakkında bilgi toplar.<br>Merhaba Operations Manager Aracısı tooLog arasında doğrudan bağlantı Analytics gerekli değildir. Veri hello yönetim grubu toohello OMS depodan iletilir. |
| Azure depolama hesabı |Hayır |Azure Storage, sistem güncelleştirmeleri hakkında bilgi içermez. |

### <a name="collection-frequency"></a>Toplama sıklığı
Yönetilen her Windows bilgisayarı için günde iki kez tarama gerçekleştirilir. Her 15 dakikada hello Windows API tooquery hello son güncelleştirme zamanı toodetermine için durumu değişti ve bu durumda bir Uyumluluk taraması başlatılır adı verilir.  Yönetilen her Linux bilgisayarı için 3 saatte bir tarama gerçekleştirilir.

Herhangi bir yere hello Pano güncelleştirilmiş toodisplay veri yönetilen bilgisayarlardan too6 saatlerini 30 dakika sürebilir.   

## <a name="using-hello-solution"></a>Merhaba çözümünü kullanarak
Merhaba güncelleştirme yönetimi çözümü tooyour OMS çalışma eklediğinizde, hello **güncelleştirme yönetimi** döşeme tooyour OMS Pano eklenir. Bu kutucuğu ortamınıza ve güncelleştirme uyumluluklarını sayısı ve grafik gösterimi hello bilgisayarların sayısını görüntüler.<br><br>
![Güncelleştirme Yönetimi Özet Kutucuğu](media/oms-solution-update-management/update-management-summary-tile.png)  


## <a name="viewing-update-assessments"></a>Güncelleştirme değerlendirmelerini görüntüleme
Tıklatın hello üzerinde **güncelleştirme yönetimi** döşeme tooopen hello **güncelleştirme yönetimi** Pano.<br><br> ![Güncelleştirme Yönetimi Özet Panosu](./media/oms-solution-update-management/update-management-dashboard.png)<br>

Bu pano, güncelleştirme durumunun işletim sistemi türüne ve güncelleştirme sınıflandırmasına (kritik, güvenlik ve diğer, örneğin tanım güncelleştirmesi) göre kategorilere ayrılmış, ayrıntılı bir dökümünü sağlar. Bu Panoda her bölme Hello sonuçlarında yalnızca temel hello bilgisayarları eşitleme kaynağına göre dağıtım için onaylanmış güncelleştirmeleri yansıtır.   Merhaba **güncelleştirme dağıtımları** seçildiğinde döşeme, görüntüleyebileceğiniz zamanlamaları, dağıtımları, tamamlanmış dağıtımları, çalışmakta olan veya yeni bir dağıtım zamanlama toohello güncelleştirme dağıtımları sayfasına yönlendirir.  

Belirli bir kategoriye ve önceden tanımlanmış ölçüt için bir sorgu hello belirli döşeme veya toorun tıklayarak tüm kayıtları verir günlük arama çalıştırın, hello altında kullanılabilir hello listeden birini **ortak güncelleştirme sorguları** sütun.    

## <a name="installing-updates"></a>Güncelleştirmeleri yükleme
Güncelleştirmeleri tüm hello Linux ve Windows bilgisayarları çalışma alanınızdaki için uygunluk sonra oluşturarak gerekli güncelleştirmeler yüklü bir *güncelleştirme dağıtımı*.  Güncelleştirme Dağıtımı, bir veya daha fazla bilgisayar için gerekli güncelleştirmelerin zamanlanmış yüklemesidir.  Hello dağıtımı için ayrıca tooa bilgisayar veya grup hello bir dağıtım kapsamında dahil edilmesi gereken bilgisayarların saat ve başlangıç tarihi belirtin.  bilgisayar grupları hakkında daha fazla toolearn bkz [günlük analizi bilgisayar gruplarında](../log-analytics/log-analytics-computer-groups.md).  Bilgisayar grupları güncelleştirme dağıtımınızda eklediğinizde, Grup memnbership zamanlama oluşturma hello aynı anda yalnızca bir kez değerlendirilir.  Sonraki değişiklikler tooa grubu değil yansıtılır.  Bu, geçici toowork zamanlanmış hello güncelleştirme dağıtımı silin ve yeniden oluşturun.

> [!NOTE]
> Windows Azure Marketi varsayılan olarak, Windows Update hizmetinden tooreceive otomatik güncelleştirmeler ayarlanır hello gelen dağıtılan VM'ler.  Bu davranış, bu çözüm ya da Windows VM'ler tooyour çalışma ekledikten sonra değiştirmez.  Bu çözümü ile etkin olarak yönetilen güncelleştirmeleri yapmanız durumunda varsayılan davranış hello (güncelleştirmelerini otomatik olarak uygulama) uygulanır.  

Merhaba isteğe bağlı Red Hat Enterprise Linux (RHEL) görüntülerde kullanılabilir Azure Marketi oluşturulan sanal makineler için kayıtlı tooaccess hello oldukları [Red Hat güncelleştirme altyapısı (RHUI)](../virtual-machines/virtual-machines-linux-update-infrastructure-redhat.md) Azure'da dağıtılabilir.  Başka bir Linux dağıtım desteklenen yöntemleriyle aşağıdaki hello distro'lar çevrimiçi dosya depodan güncelleştirilmesi gerekir.  

### <a name="viewing-update-deployments"></a>Güncelleştirme dağıtımlarını görüntüleme
Merhaba tıklatın **güncelleştirme dağıtımı** döşeme tooview hello var olan güncelleştirme dağıtımları listesi.  Bunlar duruma göre gruplandırılır: **Zamanlanmış**, **Çalışıyor** ve **Tamamlandı**.<br><br> ![Güncelleştirme Dağıtımları Zamanlama Sayfası](./media/oms-solution-update-management/update-updatedeployment-schedule-page.png)<br>  

Aşağıdaki tablonun hello her güncelleştirme dağıtımı için görüntülenen hello özellikleri açıklanmaktadır.

| Özellik | Açıklama |
| --- | --- |
| Ad |Merhaba güncelleştirme dağıtımı adı. |
| Zamanlama |Zamanlama türü.  Sağlanan seçenekler *Bir Kerelik*, *Haftalık Yineleme* ve *Aylık Yineleme*’dir. |
| Başlangıç Zamanı |Güncelleştirme dağıtımı hello tarih ve saat, zamanlanmış toostart olur. |
| Süre |Dakika hello güncelleştirme dağıtımı sayısı toorun izin verilir.  Tüm güncelleştirmeleri bu süre içinde yüklenmemişse, bu güncelleştirmeleri kalan hello kadar beklemeniz gerekir sonra sonraki güncelleştirme dağıtımı hello. |
| Sunucular |Güncelleştirme dağıtımı hello tarafından etkilenen bilgisayar sayısı.  |
| Durum |Merhaba güncelleştirme dağıtımı geçerli durumu.<br><br>Olası değerler şunlardır:<br>- Başlatılmadı<br>- Çalışıyor<br>- Tamamlandı |

Aşağıdaki tablonun hello hello sütunları içeren bir Tamamlanan güncelleştirme dağıtımı tooview hello ayrıntı ekran'ı seçin.  Bu sütun hello güncelleştirme dağıtımı değil varsa doldurulmuş henüz başlatıldı.<br><br> ![Güncelleştirme Dağıtımı Sonuçlarına genel bakış](./media/oms-solution-update-management/update-management-deploymentresults-dashboard.png)

| Sütun | Açıklama |
| --- | --- |
| **Bilgisayarlar Görünümü** | |
| Windows Bilgisayarları |Merhaba hello güncelleştirme dağıtım durumuna göre Windows bilgisayarların sayısını listeler.  Bir durum toorun tüm kayıtları hello güncelleştirme dağıtımı için durumu güncelleştirmek döndüren bir günlük Ara'yı tıklatın. |
| Linux Bilgisayarları |Merhaba hello güncelleştirme dağıtım durumuna göre Linux bilgisayarların sayısını listeler.  Bir durum toorun tüm kayıtları hello güncelleştirme dağıtımı için durumu güncelleştirmek döndüren bir günlük Ara'yı tıklatın. |
| Bilgisayar Yükleme Durumu |Merhaba güncelleştirme dağıtımı söz konusu Hello bilgisayarlar ve başarıyla yüklü güncelleştirmeleri hello yüzdesini listeler. Merhaba girişleri toorun birinde tüm eksik ve kritik güncelleştirmelerin döndüren bir günlük Ara'yı tıklatın. |
| **Güncelleştirmeler Görünümü** | |
| Windows Güncelleştirmeleri |Merhaba güncelleştirme dağıtımını ve bunların yükleme durumunu her güncelleştirme başına dahil Windows güncelleştirmelerini listeler.  Bir güncelleştirme toorun tüm kayıtları belirli bir güncelleştirme için güncelleştirme veya hello durum toorun üzerinde tüm kayıtları hello dağıtımı için güncelleştirme döndüren bir günlük Ara döndüren bir günlük Ara'yı seçin. |
| Linux Güncelleştirmeleri |Merhaba güncelleştirme dağıtımını ve bunların yükleme durumunu her güncelleştirme başına dahil Linux güncelleştirmelerini listeler.  Bir güncelleştirme toorun tüm kayıtları belirli bir güncelleştirme için güncelleştirme veya hello durum toorun üzerinde tüm kayıtları hello dağıtımı için güncelleştirme döndüren bir günlük Ara döndüren bir günlük Ara'yı seçin. |

### <a name="creating-an-update-deployment"></a>Güncelleştirme Dağıtımı oluşturma
Merhaba tıklatarak yeni bir güncelleştirme dağıtımı oluşturmak **Ekle** düğmesi Merhaba ekranında tooopen hello hello üstündeki **yeni güncelleştirme dağıtımı** sayfası.  Aşağıdaki tablonun hello hello özellikleri için değer sağlamalısınız.

| Özellik | Açıklama |
| --- | --- |
| Ad |Benzersiz bir ad tooidentify hello güncelleştirme dağıtımı. |
| Saat Dilimi |Saat dilimi toouse hello başlangıç saati için. |
| Zamanlama Türü | Zamanlama türü.  Sağlanan seçenekler *Bir Kerelik*, *Haftalık Yineleme* ve *Aylık Yineleme*’dir.  
| Başlangıç Zamanı |Tarih ve saat toostart hello güncelleştirme dağıtımı. **Not:** hello dağıtımı çalıştırabilirsiniz en yakın zamanda ise 30 dakika geçerli zamandan toodeploy hemen gerekir. |
| Süre |Dakika hello güncelleştirme dağıtımı sayısı toorun izin verilir.  Tüm güncelleştirmeleri bu süre içinde yüklenmemişse, bu güncelleştirmeleri kalan hello kadar beklemeniz gerekir sonra sonraki güncelleştirme dağıtımı hello. |
| Bilgisayarlar |Bilgisayar veya bilgisayar grupları tooinclude ve hello güncelleştirme dağıtımı hedef adları.  Bir veya daha fazla hello açılır listeden seçin. |

<br><br> ![Yeni Güncelleştirme Dağıtımı Sayfası](./media/oms-solution-update-management/update-newupdaterun-page.png)

### <a name="time-range"></a>Zaman aralığı
Varsayılan olarak, hello güncelleştirme yönetimi çözümü analiz edilen hello veri hello kapsamı içinde hello son 1 günde oluşturulan tüm bağlı yönetim gruplarından ' dir.

Merhaba veri toochange hello zaman aralığını seçin **verileri temel alarak** hello Pano hello üstünde. Oluşturulan veya 1 gün ya da 6 saat olmak üzere son 7 gün içinde hello güncelleştirilmiş kayıtları seçebilirsiniz. Ya da **Özel**’i seçip özel bir tarih aralığı belirtebilirsiniz.

## <a name="log-analytics-records"></a>Log Analytics kayıtları
Merhaba güncelleştirme yönetimi çözümü kayıtları iki tür hello OMS deposunda oluşturur.

### <a name="update-records"></a>Güncelleştirme kayıtları
Her bilgisayara yüklenen veya gerekli olan her bir güncelleştirme için **Güncelleştirme** türünde bir kayıt oluşturulur. Güncelleştirme kayıtları, aşağıdaki tablonun hello hello özelliklere sahiptir.

| Özellik | Açıklama |
| --- | --- |
| Tür |*Güncelleştirme* |
| SourceSystem |Merhaba güncelleştirme yüklemesini onaylanmış hello kaynağı.<br>Olası değerler şunlardır:<br>- Microsoft Update<br>- Windows Update<br>- SCCM<br>- Linux Sunucuları (Paket Yöneticilerinden getirilir) |
| Onaylandı |Merhaba güncelleştirme yüklemesi için onaylanıp onaylanmadığını belirtir.<br> Düzeltme eki uygulama işlemi OMS tarafından yönetilmediğinden, Linux sunucuları için bu seçenek şu anda isteğe bağlıdır. |
| Windows Sınıflandırması |Merhaba güncelleştirme sınıflandırması.<br>Olası değerler şunlardır:<br>-    Uygulamalar<br>- Kritik Güncelleştirmeler<br>- Tanım Güncelleştirmeleri<br>- Özellik Paketleri<br>- Güvenlik Güncelleştirmeleri<br>- Hizmet Paketleri<br>- Güncelleştirme Paketleri<br>- Güncelleştirmeler |
| Linux Sınıflandırması |Merhaba güncelleştirme cassification.<br>Olası değerler şunlardır:<br>- Kritik Güncelleştirmeler<br>- Güvenlik Güncelleştirmeleri<br>- Diğer Güncelleştirmeler |
| Bilgisayar |Merhaba bilgisayarın adı. |
| InstallTimeAvailable |Merhaba yükleme süresini diğer kullanılabilir olup olmadığını yüklü aracıları hello aynı belirtir güncelleştirin. |
| InstallTimePredictionSeconds |Tahmini yükleme süresi diğer dayalı saniye cinsinden yüklü aracıları hello aynı güncelleştirme. |
| KBID |Merhaba güncelleştirmeyi açıklayan hello KB makalesi kimliği. |
| ManagementGroupName |SCOM aracılar için hello yönetim grubunun adı.  Diğer aracılar için bu değer AOI-<workspace ID> şeklindedir. |
| MSRCBulletinID |Merhaba güncelleştirme açıklayan hello Microsoft güvenlik bülteni kimliği. |
| MSRCSeverity |Önem derecesi hello Microsoft Güvenlik Bülteni.<br>Olası değerler şunlardır:<br>- Kritik<br>- Önemli<br>- Orta |
| İsteğe bağlı |Merhaba güncelleştirme isteğe bağlı olup olmadığını belirtir. |
| Ürün |Merhaba ürün hello güncelleştirmesi için adıdır.  Tıklatın **Görünüm** tooopen hello makale bir tarayıcıda. |
| PackageSeverity |Merhaba Linux distro satıcıları tarafından bildirilen şekilde bu güncelleştirmede giderilen hello açığının Hello önem derecesi. |
| PublishDate |Tarih ve saat güncelleştirme hello yüklendi. |
| RebootBehavior |Hello güncelleştirme yeniden başlatma zorlar olmadığını belirtir.<br>Olası değerler şunlardır:<br>- canrequestreboot<br>- neverreboots |
| RevisionNumber |Düzeltme hello güncelleştirme sayısı. |
| SourceComputerId |GUID toouniquely hello bilgisayarı belirleyin. |
| TimeGenerated |Tarih ve saat kaydı hello son güncelleştirildi. |
| Başlık |Merhaba güncelleştirme başlığı. |
| UpdateID |GUID toouniquely hello güncelleştirme tanımlayın. |
| UpdateState |Merhaba güncelleştirme bu bilgisayarda yüklü olup olmadığını belirtir.<br>Olası değerler şunlardır:<br>-Yüklü - hello güncelleştirme bu bilgisayara yüklendi.<br>-Gerekli - hello güncelleştirmesi yüklü değil ve bu bilgisayarda gerekli. |

Türünde bir kayıt döndürür tüm günlük arama yaptığınızda **güncelleştirme** hello seçebileceğiniz **güncelleştirmeleri** bir dizi döşeme hello araması tarafından döndürülen hello güncelleştirmeleri özetlemeye görüntüleyen görünümü. Merhaba hello girişlerinde tıklatabilirsiniz **eksik ve uygulanan güncelleştirmeleri** ve **gerekli ve isteğe bağlı güncelleştirmeler** tooscope hello görünüm toothat güncelleştirmeleri kümesini yerleştirir. Select hello **listesi** veya **tablo** tooreturn hello kayıtları tek tek görüntüleyin.<br>

![Güncelleştirme Kayıt Türü ile Günlük Arama Güncelleştirme Görünümü](./media/oms-solution-update-management/update-la-view-updates.png)  

Merhaba, **tablo** görünümü üzerinde hello tıklatabilirsiniz **KBID** tüm kayıt tooopen bir tarayıcı ile Merhaba KB makalesi için. Bu, tooquickly hello hello belirli güncelleştirme hakkında ayrıntılar sağlar.<br>

![Güncelleştirme Kayıt Türü Kutucukları ile Günlük Arama Tablosu](./media/oms-solution-update-management/update-la-view-table.png)

Merhaba, **listesi** görünümü, hello tıklatın **Görünüm** bağlantı sonraki toohello KBID tooopen hello KB makalesi.<br>

![Güncelleştirme Kayıt Türü Kutucukları ile Günlük Arama Listesi](./media/oms-solution-update-management/update-la-view-list.png)

### <a name="updatesummary-records"></a>UpdateSummary kayıtları
Her Windows aracı bilgisayarı için **UpdateSummary** türünde bir kayıt oluşturulur. Bu kayıt hello bilgisayar taranan her zaman güncelleştirmeleri için güncelleştirilir. **UpdateSummary** kayıtları, aşağıdaki tablonun hello hello özellikleri vardır.

| Özellik | Açıklama |
| --- | --- |
| Tür |UpdateSummary |
| SourceSystem |OpsManager |
| Bilgisayar |Merhaba bilgisayarın adı. |
| CriticalUpdatesMissing |Merhaba bilgisayarda eksik kritik güncelleştirmelerin sayısı. |
| ManagementGroupName |SCOM aracılar için hello yönetim grubunun adı. Diğer aracılar için bu değer AOI-<workspace ID> şeklindedir. |
| NETRuntimeVersion |Merhaba .NET çalışma zamanı hello bilgisayarda yüklü sürümü. |
| OldestMissingSecurityUpdateBucket |Demet toocategorize hello zaman Hello eski eksik güvenlik güncelleştirmesi bu bilgisayarda yayımlandığı tarihten sonra.<br>Olası değerler şunlardır:<br>- Eski<br>-    180 gün önce<br>- 150 gün önce<br>-    120 gün önce<br>- 90 gün önce<br>- 60 gün önce<br>-    30 gün önce<br>-    En Son |
| OldestMissingSecurityUpdateInDays |Merhaba eski eksik güvenlik güncelleştirmesi bu bilgisayarda yayımlandığından bu yana gün sayısı. |
| OsVersion |Merhaba bilgisayarda yüklü hello işletim sistemi sürümü. |
| OtherUpdatesMissing |Merhaba bilgisayarda eksik diğer güncelleştirmeleri sayısı. |
| SecurityUpdatesMissing |Merhaba bilgisayarda eksik güvenlik güncelleştirmelerini sayısı. |
| SourceComputerId |GUID toouniquely hello bilgisayarı belirleyin. |
| TimeGenerated |Tarih ve saat kaydı hello son güncelleştirildi. |
| TotalUpdatesMissing |Merhaba bilgisayarda eksik güncelleştirmelerin toplam sayısı. |
| WindowsUpdateAgentVersion |Merhaba bilgisayarda hello Windows Update Aracısı'nın sürüm numarası. |
| WindowsUpdateSetting |Önemli güncelleştirmeleri hello bilgisayar nasıl yükler için ayarlama.<br>Olası değerler şunlardır:<br>- Devre dışı<br>- Yüklemeden önce bildir<br>- Zamanlanmış yükleme |
| WSUSServer |Merhaba bilgisayarsa URL, WSUS sunucusu toouse bir yapılandırılmış. |

## <a name="sample-log-searches"></a>Örnek günlük aramaları
Aşağıdaki tablonun hello bu çözümü tarafından toplanan güncelleştirme kayıtları için örnek günlük aramaları sağlar.

| Sorgu | Açıklama |
| --- | --- |
| Type:Update OSType!=Linux UpdateState=Needed Optional=false Approved!=false &#124; measure count() by Computer |Güncelleştirmelere gerek duyan Windows tabanlı sunucu bilgisayarları |
| Type:Update OSType=Linux UpdateState!="Not needed" &#124; measure count() by Computer |Güncelleştirmelere gerek duyan Linux sunucuları | 
| Type=Update UpdateState=Needed Optional=false &#124; select Computer,Title,KBID,Classification,UpdateSeverity,PublishedDate |Eksik güncelleştirmeleri olan tüm bilgisayarlar |
| Type=Update UpdateState=Needed Optional=false Computer="COMPUTER01.contoso.com" &#124; select Computer,Title,KBID,Product,UpdateSeverity,PublishedDate |Belirli bir bilgisayarda eksik güncelleştirmeler (değeri kendi bilgisayarınızın adıyla değiştirin)|
| Type=Update UpdateState=Needed Optional=false (Classification="Security Updates" OR Classification="Critical Updates") |Eksik kritik güncelleştirmeleri veya güvenlik güncelleştirmeleri olan tüm bilgisayarlar | 
| Type=Update UpdateState=Needed Optional=false (Classification="Security Updates" OR Classification="Critical Updates") Computer IN {Type=UpdateSummary WindowsUpdateSetting=Manual &#124; Distinct Computer} &#124; Distinct KBID |Güncelleştirmelerin el ile uygulandığı makinelerde gerekli olan kritik güncelleştirmeler veya güvenlik güncelleştirmeleri |
| Type=Event EventLevelName=error Computer IN {Type=Update (Classification="Security Updates" OR Classification="Critical Updates") UpdateState=Needed Optional=false &#124; Distinct Computer} |Kritik güncelleştirmeleri veya gerekli güvenlik güncelleştirmeleri eksik olan makineler için hata olayları |
| Type=Update Optional=false Classification="Update Rollups" UpdateState=Needed &#124; select Computer,Title,KBID,Classification,UpdateSeverity,PublishedDate |Eksik güncelleştirme paketleri olan tüm bilgisayarlar | 
| Type=Update UpdateState=Needed Optional=false &#124; Distinct Title |Tüm bilgisayarlardaki ayrı eksik güncelleştirmeler | 
| Type:UpdateRunProgress InstallationStatus=failed &#124; measure count() by Computer, Title, UpdateRunName |Bir güncelleştirme çalıştırmasında güncelleştirmeleri başarısız olan Windows tabanlı sunucu bilgisayarı | 
| Type:UpdateRunProgress InstallationStatus=failed &#124; measure count() by Computer, Product, UpdateRunName |Bir güncelleştirme çalıştırmasında güncelleştirmeleri başarısız olan Linux sunucusu | 
| Type=UpdateSummary &#124; measure count() by WSUSServer |WSUS bilgisayar üyeliği | 
| Type=UpdateSummary &#124; measure count() by WindowsUpdateSetting |Otomatik güncelleştirme yapılandırması | 
| Type=UpdateSummary WindowsUpdateSetting=Manual |Otomatik güncelleştirmenin devre dışı olduğu bilgisayarlar | 
| Type=Update and OSType=Linux and UpdateState!="Not needed" &#124; measure count() by Computer |Paket güncelleştirme kullanılabilir olan tüm hello Linux makineler listesi | 
| Type=Update and OSType=Linux and UpdateState!="Not needed" and (Classification="Critical Updates" OR Classification="Security Updates") &#124; measure count() by Computer |Kritik Güncelleştirmeler veya güvenlik açığına paket güncelleştirmesi mevcut olan tüm hello Linux makineler listesi | 
| Type=Update and OSType=Linux and UpdateState!="Not needed" |Bir güncelleştirmenin kullanılabilir olduğu tüm paketlerin listesi | 
| Type=Update  and OSType=Linux and UpdateState!="Not needed" and (Classification="Critical Updates" OR Classification="Security Updates") |Kritik veya Güvenlik türünde güvenlik açığını ele alan güncelleştirmeye sahip tüm paketlerin listesi | 
| Type:UpdateRunProgress &#124; measure Count() by UpdateRunName |Hangi dağıtımların bilgisayarlarda değişiklik yaptığını gösteren liste | 
| Type:UpdateRunProgress UpdateRunName="DeploymentName" &#124; measure Count() by Computer |Bu güncelleştirme çalıştırmasında güncelleştirilmiş olan bilgisayarlar (değeri kendi Güncelleştirme Dağıtımı adınızla değiştirin) | 
| Type=Update and OSType=Linux and OSName = Ubuntu &#124; measure count() by Computer |Herhangi bir güncelleştirme tüm hello "Ubuntu" makinelerle listesi | 

## <a name="troubleshooting"></a>Sorun giderme

Bu bölümde toohelp hello güncelleştirme yönetimi çözümü ile ilgili sorunları giderme bilgileri sağlar.  

### <a name="how-do-i-troubleshoot-onboarding-issues"></a>Ekleme sorunlarını nasıl giderebilirim?
Tooonboard hello çözüm ya da bir sanal makine çalışırken sorunlarla karşılaşırsanız, hello denetleyin **uygulama ve Hizmetleri Logs\Operations Yöneticisi** içerenolaykimliği4502veolayiletisiolanolaylariçinolaygünlüğünü**Microsoft.EnterpriseManagement.HealthService.AzureAutomation.HybridAgent**.  Aşağıdaki tablonun hello her biri için özel hata iletileri ve olası bir çözüm vurgular.  

| İleti | Neden | Çözüm |   
|----------|----------|----------|  
| %S tooRegister makine düzeltme eki yönetimi için<br>Kayıt Özel Durumla Başarısız Oldu<br>System.InvalidOperationException: {"Message":"Makine zaten<br>kayıtlı tooa farklı bir hesap. "} | Makine zaten güncelleştirme yönetimi için edildi tooanother çalışma | Tarafından eski yapılarının temizlenmesini [hello karma runbook grubu siliniyor](../automation/automation-hybrid-runbook-worker.md#remove-hybrid-worker-groups)|  
| Unable çok kaydetmek makine düzeltme eki yönetimi için<br>Kayıt Özel Durumla Başarısız Oldu<br>System.Net.Http.HttpRequestException: Hello isteği gönderilirken bir hata oluştu. ---><br>System.Net.WebException: hello arka plandaki bağlantı<br>kapatıldı: Alma işlemi sırasında<br>beklenmeyen bir hata oluştu. ---> System.ComponentModel.Win32Exception:<br>Merhaba istemci ve sunucu iletişim kuramıyor,<br>çünkü ortak bir algoritmaya sahip değiller | Proxy/Ağ Geçidi/Güvenlik Duvarı iletişimi engelliyor | [Ağ gereksinimlerini gözden geçirin](../automation/automation-offering-get-started.md#network-planning)|  
| %S tooRegister makine düzeltme eki yönetimi için<br>Kayıt Özel Durumla Başarısız Oldu<br>Newtonsoft.Json.JsonReaderException: Pozitif sonsuz değer ayrıştırılırken hata oluştu. | Proxy/Ağ Geçidi/Güvenlik Duvarı iletişimi engelliyor | [Ağ gereksinimlerini gözden geçirin](../automation/automation-offering-get-started.md#network-planning)| 
| Merhaba hizmeti tarafından sunulan hello sertifika <wsid>. oms.opinsights.azure.com<br>Microsoft hizmetleri için kullanılan bir sertifika yetkilisi<br>tarafından verilmemiş. Lütfen<br>bir proxy sunucu kullanıyorsanız, ağ yöneticisi toosee durdurur<br>TLS/SSL iletişimini engelleyen bir proxy çalıştırıp çalıştırmadıklarına bakın. |Proxy/Ağ Geçidi/Güvenlik Duvarı iletişimi engelliyor | [Ağ gereksinimlerini gözden geçirin](../automation/automation-offering-get-started.md#network-planning)|  
| %S tooRegister makine düzeltme eki yönetimi için<br>Kayıt Özel Durumla Başarısız Oldu<br>AgentService.HybridRegistration.<br>PowerShell.Certificates.CertificateCreationException:<br>Kendinden imzalı bir sertifika toocreate başarısız oldu. ---><br>System.UnauthorizedAccessException: Erişim reddedildi. | Otomatik olarak imzalanan sertifika oluşturma hatası | Sistem hesabının<br>okuma erişimi toofolder:<br>**C:\ProgramData\Microsoft\**<br>**Crypto\RSA**|  

### <a name="how-do-i-troubleshoot-update-deployments"></a>Güncelleştirme dağıtımlarının sorunlarını nasıl giderebilirim?
Merhaba runbook'un zamanlanmış hello güncelleştirme dağıtımı'ndan hello işler dikey penceresinde hello OMS çalışma Bu çözüm destekleme bağlı Otomasyon hesabınızın dahil hello güncelleştirmeleri dağıtmak için sorumlu hello sonuçlarını görüntüleyebilirsiniz.  runbook hello **düzeltme eki MicrosoftOMSComputer** belirli bir yönetilen bilgisayarı hedefleyen bir alt runbook ve hello ayrıntılı akış gözden geçirme bu dağıtım için ayrıntılı bilgiler düzenleyecek.  Merhaba çıktı, güncelleştirmelerinin geçerli olduğunun gerekli görüntülemek, durumu, yükleme durumu ve ek ayrıntılar indirin.<br><br> ![Güncelleştirme Dağıtımı iş durumu](media/oms-solution-update-management/update-la-patchrunbook-outputstream.png)<br>

Daha fazla bilgi için bkz. [Otomasyon runbook’u çıkışı ve iletileri](../automation/automation-runbook-output-and-messages.md).   

## <a name="next-steps"></a>Sonraki adımlar
* Günlük aramalarda kullanması [günlük analizi](../log-analytics/log-analytics-log-searches.md) tooview ayrıntılı veri güncelleştir.
* Yönetilen bilgisayarlarınızın güncelleştirme uyumluluğunu gösteren [kendi panolarınızı oluşturun](../log-analytics/log-analytics-dashboards.md).
* Bilgisayardan eksik kritik güncelleştirmeler algılandığında veya bilgisayarda otomatik güncelleştirmeler devre dışı olduğunda [uyarılar oluşturun](../log-analytics/log-analytics-alerts.md).  
