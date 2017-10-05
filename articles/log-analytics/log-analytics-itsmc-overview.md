---
title: "BT Hizmet Yönetimi Bağlayıcısı OMS | Microsoft Docs"
description: "Tüm sorunların hızla çözülmesine ve BT Hizmet Yönetimi Bağlayıcısı merkezi olarak izlemek ve OMS ITSM iş öğelerini yönetmek için kullanın."
services: log-analytics
documentationcenter: 
author: JYOTHIRMAISURI
manager: riyazp
editor: 
ms.assetid: 0b1414d9-b0a7-4e4e-a652-d3a6ff1118c4
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: v-jysur
ms.openlocfilehash: 54974ef06efdae69ddbfa12b1ba9278b48b113d3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="centrally-manage-itsm-work-items-using-it-service-management-connector-preview"></a>ITSM iş öğelerini BT Hizmet Yönetimi Bağlayıcısı (Önizleme) kullanarak merkezi olarak yönetme

![BT Hizmet Yönetimi Bağlayıcısı simgesi](./media/log-analytics-itsmc/itsmc-symbol.png)

Merkezi olarak izlemek ve ITSM ürünler/hizmetlerinizi arasında iş öğelerini yönetmek için OMS günlük analizi BT Hizmet Yönetimi Bağlayıcısı'nı (ITSMC) kullanın.

BT Hizmet Yönetimi Bağlayıcısı var olan BT Hizmet Yönetimi (ITSM) ürünleri ve Hizmetleri OMS günlük analizi ile tümleşir.  Çözümü OMS kullanıcılar ITSM çözümde olaylar, uyarılar ya da olaylar oluşturmak için bir seçenek sağladığı ITSM ürünler/hizmetler ile çift yönlü tümleştirme vardır. Bağlayıcı da olaylar gibi verileri içe aktaran ve OMS günlük analizi ITSM çözümden değişiklik istekleri.

BT Hizmet Yönetimi Bağlayıcısı ile şunları yapabilirsiniz:

  - Merkezi olarak izlemek ve iş öğeleri için ITSM ürünler/hizmetler kuruluşunuz genelinde kullanılan yönetin.
  - ITSM iş öğeleri (örneğin, uyarı, olay, olay) içinde ITSM OMS uyarılardan ve günlük arama aracılığıyla oluşturun.
  - Olayları okuma ve ITSM çözümünüzden değişiklik istekleri ve ilgili günlük veri günlük analizi çalışma alanındaki ile ilişkilendirilmesi.
  - Beklenmeyen ve olağan dışı olayları bulmak ve son kullanıcılar çağırın ve Yardım için rapor bile önce bunları çözün.
  - İş öğeleri veri günlük analizi alabilir ve ana performans göstergesi (KPI) raporları oluşturabilirsiniz.  Bu raporları kullanarak, tanımlayabilir, değerlendirmek ve kötü amaçlı yazılım değerlendirmesi gibi birkaç önemli öğe hareket.
  - Daha ayrıntılı Öngörüler için seçkin panolar üzerinde olayları görüntülemek için değişiklik istekleri ve etkilenen sistemler.
  - Daha hızlı günlük analizi çalışma alanındaki diğer yönetim çözümleri ile ilişkilendirilmesi yoluyla sorunlarını giderin.


## <a name="prerequisites"></a>Ön koşullar

OMS günlük analizi ITSM iş öğelerini almak için çözüm OMS BT Hizmet Yönetimi bağlayıcıda ve iş öğeleri içeri aktarma BT SM Ürün/hizmet arasında bir bağlantı gerektirir.


## <a name="configuration"></a>Yapılandırma

BT Hizmet Yönetimi Bağlayıcısı çözüm açıklanan işlemi kullanarak OMS çalışma alanınıza ekleyin [Çözümleri Galerisi eklemek günlük analizi çözümleri](log-analytics-add-solutions.md).

BT Hizmet Yönetimi Bağlayıcısı çözümleri Galerisi'nde gördüğünüz gibi döşeme:

![Bağlayıcı döşeme](./media/log-analytics-itsmc/itsmc-solutions-tile.png)

Başarılı ayrıca sonra BT Hizmet Yönetimi Bağlayıcısı altında görürsünüz **OMS** > **ayarları** > **bağlı kaynakları.**

![Bağlı ITSMC](./media/log-analytics-itsmc/itsmc-overview-solution-in-connected-sources.png)

> [!NOTE]

> Varsayılan olarak, BT Hizmet Yönetimi Bağlayıcısı her 24 saatte bağlantının verileri yeniler. Hemen tüm düzenlemeler veya şablon için bağlantının verileri yenilemek için bağlantınızı yanında görüntülenen Yenile düğmesini tıklatın yaptığınız güncelleştirir.

 ![ITSMC Yenile](./media/log-analytics-itsmc/itsmc-connection-refresh.png)

## <a name="management-packs"></a>Yönetim paketleri
Bu çözüm, herhangi bir Yönetim Paketi gerektirmez.

## <a name="connected-sources"></a>Bağlı kaynaklar

Aşağıdaki ITSM ürünler/hizmetler BT Hizmet Yönetimi Bağlayıcısı tarafından desteklenir:

- [System Center Service Manager (SCSM)](log-analytics-itsmc-connections.md#connect-system-center-service-manager-to-it-service-management-connector-in-oms)

- [ServiceNow](log-analytics-itsmc-connections.md#connect-servicenow-to-it-service-management-connector-in-oms)

- [Provance](log-analytics-itsmc-connections.md#connect-provance-to-it-service-management-connector-in-oms)  

- [Cherwell](log-analytics-itsmc-connections.md#connect-cherwell-to-it-service-management-connector-in-oms)

## <a name="using-the-solution"></a>Çözümü kullanma

OMS BT Hizmet Yönetimi Bağlayıcısı ITSM hizmetiniz ile bağladıktan sonra günlük analizi Hizmetleri başlatılır bağlı ITSM ürünler/hizmetinden veri toplama.

> [!NOTE]
> - BT Hizmet Yönetimi Bağlayıcısı çözümü tarafından alınan veri olayların adlı günlük analizi görünür **ServiceDesk_CL**.
- Olay adında bir alan içeriyor **ServiceDeskWorkItemType_s**. hangi olay değeri alın veya değişiklik isteği içinde yer alan iş öğesi verilerine bağlı olarak **ServiceDesk_CL** olay.

## <a name="input-data"></a>Giriş verisi
İş öğeleri ITSM ürünler/hizmetlerinden içeri aktarılan.

Aşağıdaki bilgiler BT Hizmet Yönetimi Bağlayıcısı tarafından toplanan veri örnekleri gösterilmektedir:

> [!NOTE]
> İş öğesi türüne bağlı olarak günlük analizi içeri **ServiceDesk_CL** aşağıdaki alanları içerir:

**İş öğesi:** **olaylar**  
ServiceDeskWorkItemType_s "Olay" =

**Alanları**

- ServiceDeskConnectionName
- Hizmet Masası kimliği
- Durum
- Aciliyet
- Etkisi
- Öncelik
- Yükseltme
- Tarafından oluşturulan
- Çözümleyen
- Tarafından kapatıldı
- Kaynak
- Atanan
- Kategori
- Başlık
- Açıklama
- Oluşturulma tarihi
- Kapatılma tarihi
- Çözümlenme tarihi
- Son değiştirilme tarihi
- Bilgisayar


**İş öğesi:** **değişiklik istekleri**

ServiceDeskWorkItemType_s "ChangeRequest" =

**Alanları**
- ServiceDeskConnectionName
- Hizmet Masası kimliği
- Tarafından oluşturulan
- Tarafından kapatıldı
- Kaynak
- Atanan
- Başlık
- Tür
- Kategori
- Durum
- Yükseltme
- Çakışma durumu
- Aciliyet
- Öncelik
- Riski
- Etkisi
- Atanan
- Oluşturulma tarihi
- Kapatılma tarihi
- Son değiştirilme tarihi
- İstenen tarih
- Planlanan başlangıç tarihi
- Planlanan bitiş tarihi
- İş başlangıç tarihi
- İş bitiş tarihi
- Açıklama
- Bilgisayar

## <a name="output-data-for-a-servicenow-incident"></a>ServiceNow olay için çıktı verileri

| OMS alan | ITSM alan |
|:--- |:--- |
| ServiceDeskId_s| Sayı |
| IncidentState_s | Durum |
| Urgency_s |Aciliyet |
| Impact_s |Etkisi|
| Priority_s | Öncelik |
| CreatedBy_s | Tarafından açılmış |
| ResolvedBy_s | Çözümleyen|
| ClosedBy_s  | Tarafından kapatıldı |
| Source_s| İlgili kişi türü |
| AssignedTo_s | Atanan  |
| Category_s | Kategori |
| Title_s|  Kısa açıklama |
| Description_s|  Notlar |
| CreatedDate_t|  Açılan |
| ClosedDate_t| Kapalı|
| ResolvedDate_t|Çözümlendi|
| Bilgisayar  | Yapılandırma öğesi |

## <a name="output-data-for-a-servicenow-change-request"></a>Çıktı verileri bir ServiceNow için değişiklik isteği

| OMS alan | ITSM alan |
|:--- |:--- |
| ServiceDeskId_s| Sayı |
| CreatedBy_s | Tarafından istenen |
| ClosedBy_s | Tarafından kapatıldı |
| AssignedTo_s | Atanan  |
| Title_s|  Kısa açıklama |
| Type_s|  Tür |
| Category_s|  Catgory |
| CRState_s|  Durum|
| Urgency_s|  Aciliyet |
| Priority_s| Öncelik|
| Risk_s| Riski|
| Impact_s| Etkisi|
| RequestedDate_t  | Tarihe göre istendi |
| ClosedDate_t | Kapatılma tarihi |
| PlannedStartDate_t  |     Planlanan başlangıç tarihi |
| PlannedEndDate_t  |   Planlanan bitiş tarihi |
| WorkStartDate_t  | Gerçek başlangıç tarihi |
| WorkEndDate_t | Gerçek bitiş tarihi|
| Description_s | Açıklama |
| Bilgisayar  | Yapılandırma öğesi |

**Örnek günlük analizi ekran ITSM verileri için:**

![Günlük analizi ekranı](./media/log-analytics-itsmc/itsmc-overview-sample-log-analytics.png)

## <a name="it-service-management-connector--integration-with-other-oms-solutions"></a>BT Hizmet Yönetimi Bağlayıcısı – diğer OMS çözümleri ile tümleştirme

BT Hizmet Yönetimi Bağlayıcısı, şu anda hizmet Haritası çözümüyle tümleştirmeyi destekler.

Hizmet eşlemesi otomatik olarak sistemlerde, Windows ve Linux uygulama bileşenleri bulur ve Hizmetleri arasındaki iletişimi eşler. Bunları – Kritik hizmetler sunan birbirine bağlı sistemler olarak düşündüğünüz sunucularınızı görüntülemenize izin verir. Bir aracı yüklemesini dışında hiçbir yapılandırma TCP bağlı mimarisiyle arasında bağlantı noktaları gerekli ve hizmet Haritası sunucuları, işlemleri arasındaki bağlantıları gösterir. Daha fazla bilgi: [hizmet Haritası](../operations-management-suite/operations-management-suite-service-map.md).

İle tümleştirme, aşağıdaki örnekte gösterildiği gibi ITSM çözümlerinde oluşturulan hizmet Masası öğeleri görüntüleyebilirsiniz:

![Tümleşik çözüm ](./media/log-analytics-itsmc/itsmc-overview-integrated-solutions.png)
## <a name="create-itsm-work-items-for-oms-alerts"></a>OMS uyarılar için ITSM iş öğeleri oluşturma

OMS uyarılar için bağlı ITSM kaynaklarında ilişkili iş öğeleri oluşturabilirsiniz.  Bunu yapmak için aşağıdaki yordamı kullanın:

1. Gelen **günlük arama** penceresinde verileri görüntülemek için bir günlük arama sorgusunu çalıştırın. Sorgu sonuçları, iş öğeleri için kaynaktır.
2. İçinde **günlük arama**, tıklatın **uyarı** açmak için **uyarı kuralı Ekle** sayfası.

    ![Günlük analizi ekranı](./media/log-analytics-itsmc/itsmc-work-items-for-oms-alerts.png)

3. Üzerinde **uyarı kuralı Ekle** penceresinde sağlamak için gerekli ayrıntıları **adı**, **önem**, **arama sorgusu**, ve **uyarı Ölçüt** (zaman penceresi/ölçü ölçüm).
4. Seçin **Evet** için **ITSM Eylemler**.
5. ITSM bağlantınızı seçin **seçin bağlantı** listesi.
6. Gerekli ayrıntıları belirtin.
7. Bu uyarının her günlük girişinin için ayrı iş öğesi oluşturmak için seçin **her günlük girişinin için tek tek iş öğeleri oluşturma** onay kutusu.

    Veya

    Bu onay kutusunu günlük girişlerini bu uyarı altında herhangi bir sayıda için yalnızca bir iş öğesi oluşturmak için seçili bırakın.

7. **Kaydet** düğmesine tıklayın.

OMS uyarı altında oluşturulan **uyarıları**. Belirtilen uyarının koşulu karşılandığında karşılık gelen ITSM bağlantı çalışma öğeleri oluşturulur.

## <a name="create-itsm-work-items-from-oms-logs"></a>OMS günlüklerinden ITSM iş öğeleri oluşturma

OMS günlük arama kullanarak bağlı ITSM kaynaklarında iş öğeleri oluşturabilirsiniz. Bunu yapmak için aşağıdaki yordamı kullanın:

1. Gelen **günlük arama**, gerekli verileri arama, ayrıntı seçin ve tıklatın **oluşturma çalışma öğesini**.

    **Oluşturma ITSM iş öğesi** penceresi görüntülenir:

    ![Günlük analizi ekranı](media/log-analytics-itsmc/itsmc-work-items-from-oms-logs.png)

2.   Aşağıdaki ayrıntıları ekleyin:

  - **İş öğesi başlık**: iş öğesi için başlık.
  - **İş öğesi tanımı**: yeni çalışma öğesi için bir açıklama.
  - **Bilgisayar etkilenen**: Bu günlük verileri nerede bulundu bilgisayarın adı.
  - **Bağlantıyı seçin**: Bu iş öğesi oluşturmak istediğiniz ITSM bağlantı.
  - **İş öğesi**: iş öğesi türü.

3. Bir olay için var olan bir iş öğesi şablonunu kullanmak için tıklatın **Evet** altında **Generate iş öğesi şablona dayalı** seçeneğini ve ardından **oluşturma**.

    Veya

    Tıklatın **Hayır** özelleştirilmiş değerlerinizi sağlamak istiyorsanız.

4. Uygun değerleri sağlayın **kişi türündeki**, **etkisi**, **aciliyet**, **kategori**, ve **alt kategori** metin kutuları ve ardından **oluşturma**.

İş öğesi içinde OMS de görüntüleyebilirsiniz ITSM içinde oluşturulacak.

## <a name="troubleshoot-itsm-connections-in-oms"></a>OMS ITSM bağlantı sorunlarını giderme
1.  Bağlantı başarısız bağlı kaynağın kullanıcı Arabiriminden ve elde **bağlantı kaydetmede hata** iletisi, aşağıdakileri yapın:
 - ServiceNow, Cherwell ve Provance bağlantıları olması durumunda, doğru kullanıcı adı/parola ve istemci kimliği/istemci gizli anahtarı bağlantıların her biri için girdiğiniz emin olun. Sorun devam ederse, bağlantıyı kurmak için karşılık gelen ITSM üründe yeterli ayrıcalıkları olup olmadığını denetleyin.
 - Service Manager durumunda, Web uygulaması başarıyla dağıtılır ve karma bağlantı oluşturulan emin olun. Şirket içi Service Manager makineyle bağlantı kuran başarıyla doğrulamak için Web uygulaması URL'si yapma belgelerindeki ayrıntılı olarak ziyaret [karma bağlantı](log-analytics-itsmc-connections.md#configure-the-hybrid-connection).

2.  ServiceNow verileri OMS eşitlenmedi, örneği değil uykuda ServiceNow emin olun. Bu süre ServiceNow geliştirme durumlarda boşta olduğunda meydana gelir. Aksi takdirde, sorunu bildirin.
3.  OMS uyarıları tetiklenir ancak iş öğelerini ITSM içinde oluşturulan ürün veya yapılandırma öğeleri oluşturulan/iş öğeleri ya da herhangi bir genel bilgi için aşağıdakileri yapın bağlantılı almıyorsa:
 -  BT Hizmet Yönetimi Bağlayıcısı çözüm OMS portalında bağlantıları/iş öğeleri/bilgisayarların vb. özetini almak için kullanılabilir. Durum dikey penceresinde hata iletisi'ı tıklatın, gitmek **günlük arama** ve hata iletisinde ayrıntıları kullanarak hatalı bağlantı görüntüleyin.
 - doğrudan hataları ve ilgili bilgileri görüntüleyebileceğiniz **günlük arama** kullanarak sayfa *türü ServiceDeskLog_CL =*.

## <a name="troubleshoot-service-manager-web-app-deployment"></a>Service Manager Web uygulama dağıtım sorunlarını gider
1.  Web uygulama dağıtımına herhangi bir sorun olması durumunda, kaynakları oluşturun/dağıtmak için belirtilen abonelik yeterli izinlere sahip olun.
2.  Varsa **nesne bir nesnenin örneğine ayarlı değil referansı** hata iletisi görüntüleniyor çalıştırılırken [betik](log-analytics-itsmc-service-manager-script.md) altında geçerli değerler girdiğinizden emin olun **Kullanıcı Yapılandırması** bölüm.
3.  Service bus geçiş ad alanı oluşturma başarısız olursa, gereken kaynak sağlayıcısı abonelikte kayıtlı olduğundan emin olun. El ile kayıtlı değil, Azure portalından oluşturun. Bunu sırasında da oluşturabilirsiniz [karma bağlantı oluşturma](log-analytics-itsmc-connections.md#configure-the-hybrid-connection) Azure portalından.


## <a name="contact-us"></a>Bizimle iletişim kurun

Tüm sorgular veya BT Hizmet Yönetimi Bağlayıcısı geribildirim için adresinden bize başvurun [ omsitsmfeedback@microsoft.com ](mailto:omsitsmfeedback@microsoft.com).

## <a name="next-steps"></a>Sonraki adımlar
[BT Hizmet Yönetimi Bağlayıcısı için ITSM ürünler/hizmetler eklemek](log-analytics-itsmc-connections.md).
