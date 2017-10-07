---
title: "Hizmet Yönetimi Bağlayıcısı OMS içinde aaaIT | Microsoft Docs"
description: "Hello BT Hizmet Yönetimi Bağlayıcısı toocentrally İzleyicisi'ni kullanın ve OMS hello ITSM iş öğelerini yönetmek ve hızlı bir şekilde tüm sorunları giderin."
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
ms.openlocfilehash: 33ed5d432591b836eb41ba982c66c96f22879444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="centrally-manage-itsm-work-items-using-it-service-management-connector-preview"></a>ITSM iş öğelerini BT Hizmet Yönetimi Bağlayıcısı (Önizleme) kullanarak merkezi olarak yönetme

![BT Hizmet Yönetimi Bağlayıcısı simgesi](./media/log-analytics-itsmc/itsmc-symbol.png)

OMS günlük analizi toocentrally İzleyicisi'nde hello BT Hizmet Yönetimi Bağlayıcısı (ITSMC) kullanın ve iş öğeleri ITSM ürünler/hizmetlerinizi yönetebilirsiniz.

Merhaba BT Hizmet Yönetimi Bağlayıcısı var olan BT Hizmet Yönetimi (ITSM) ürünleri ve Hizmetleri OMS günlük analizi ile tümleşir.  ITSM ürünler/hizmetler ile çift yönlü tümleştirme Hello çözümü vardır, OMS kullanıcılar bir seçenek toocreate olaylar, uyarılar veya ITSM çözüm olayların sağladığı burada hello. Merhaba bağlayıcı da olaylar gibi verileri içe aktaran ve OMS günlük analizi ITSM çözümden değişiklik istekleri.

BT Hizmet Yönetimi Bağlayıcısı ile şunları yapabilirsiniz:

  - Merkezi olarak izlemek ve iş öğeleri için ITSM ürünler/hizmetler kuruluşunuz genelinde kullanılan yönetin.
  - ITSM iş öğeleri (örneğin, uyarı, olay, olay) içinde ITSM OMS uyarılardan ve günlük arama aracılığıyla oluşturun.
  - Olayları okuma ve ITSM çözümünüzden değişiklik istekleri ve ilgili günlük veri günlük analizi çalışma alanındaki ile ilişkilendirilmesi.
  - Beklenmeyen ve olağan dışı olayları bulmak ve hatta hello son kullanıcıların çağırın ve toohello Yardım Masası rapor önce bunları çözün.
  - İş öğeleri veri günlük analizi alabilir ve ana performans göstergesi (KPI) raporları oluşturabilirsiniz.  Bu raporları kullanarak, tanımlayabilir, değerlendirmek ve kötü amaçlı yazılım değerlendirmesi gibi birkaç önemli öğe hareket.
  - Daha ayrıntılı Öngörüler için seçkin panolar üzerinde olayları görüntülemek için değişiklik istekleri ve etkilenen sistemler.
  - Daha hızlı hello günlük analizi çalışma alanındaki diğer yönetim çözümleri ile ilişkilendirilmesi yoluyla sorunlarını giderin.


## <a name="prerequisites"></a>Ön koşullar

tooimport hello ITSM iş öğeleri OMS günlük analizi içine hello çözüm hello OMS hello BT Hizmet Yönetimi Bağlayıcısı ile Merhaba BT SM Ürün/hizmet hello çalışma öğelerini içeri aktarma arasında bir bağlantı gerektirir.


## <a name="configuration"></a>Yapılandırma

Açıklanan başlangıç işlemini kullanarak Ekle hello BT Hizmet Yönetimi Bağlayıcısı çözüm tooyour OMS çalışma alanı, [hello Çözümleri Galerisi eklemek günlük analizi çözümleri](log-analytics-add-solutions.md).

BT Hizmet Yönetimi Bağlayıcısı hello çözümleri Galerisi'nde gördüğünüz gibi döşeme:

![Bağlayıcı döşeme](./media/log-analytics-itsmc/itsmc-solutions-tile.png)

Göreceğiniz başarılı ayrıca sonra BT Hizmet Yönetimi Bağlayıcısı altında hello **OMS** > **ayarları** > **bağlı kaynakları.**

![Bağlı ITSMC](./media/log-analytics-itsmc/itsmc-overview-solution-in-connected-sources.png)

> [!NOTE]

> Varsayılan olarak, BT Hizmet Yönetimi Bağlayıcısı hello 24 saatte bir kez hello bağlantının verileri yeniler. toorefresh hello Yenile düğmesini görüntülenen sonraki tooyour Bağlantısı'nı tıklatın, yaptığınız herhangi bir düzenlemeler veya şablon için anında, bağlantının verileri güncelleştirir.

 ![ITSMC Yenile](./media/log-analytics-itsmc/itsmc-connection-refresh.png)

## <a name="management-packs"></a>Yönetim paketleri
Bu çözüm, herhangi bir Yönetim Paketi gerektirmez.

## <a name="connected-sources"></a>Bağlı kaynaklar

Merhaba aşağıdaki ITSM ürünler/hizmetler hello BT Hizmet Yönetimi Bağlayıcısı tarafından desteklenir:

- [System Center Service Manager (SCSM)](log-analytics-itsmc-connections.md#connect-system-center-service-manager-to-it-service-management-connector-in-oms)

- [ServiceNow](log-analytics-itsmc-connections.md#connect-servicenow-to-it-service-management-connector-in-oms)

- [Provance](log-analytics-itsmc-connections.md#connect-provance-to-it-service-management-connector-in-oms)  

- [Cherwell](log-analytics-itsmc-connections.md#connect-cherwell-to-it-service-management-connector-in-oms)

## <a name="using-hello-solution"></a>Merhaba çözümünü kullanarak

ITSM hizmeti ile Merhaba OMS BT Hizmet Yönetimi Bağlayıcısı bağlandıktan sonra hello günlük analizi Hizmetleri başlatılır bağlı hello ITSM Ürün/hizmet hello veri toplama.

> [!NOTE]
> - BT Hizmet Yönetimi Bağlayıcısı çözümü tarafından alınan veri olayların adlı günlük analizi görünür **ServiceDesk_CL**.
- Olay adında bir alan içeriyor **ServiceDeskWorkItemType_s**. hangi değer olay olarak ele veya değişiklik isteği, yapabilirsiniz hello bağlı olarak iş öğesi hello bulunan verileri **ServiceDesk_CL** olay.

## <a name="input-data"></a>Giriş verisi
İş öğeleri Hello ITSM ürünler/hizmetlerinden içeri aktarılan.

Merhaba aşağıdaki bilgileri hello BT Hizmet Yönetimi Bağlayıcısı tarafından toplanan veri örnekleri gösterilmektedir:

> [!NOTE]
> İş öğesi türü günlük analizi içeri Hello bağlı olarak **ServiceDesk_CL** alanları izleyen hello içerir:

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
| AssignedTo_s | Çok atanan |
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
| AssignedTo_s | Çok atanan |
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

BT Hizmet Yönetimi Bağlayıcısı, şu anda hello hizmet Haritası çözümü ile tümleştirmeyi destekler.

Hizmet eşlemesi uygulama bileşenleri Windows hello ve Linux sistemleri ve haritalar Hizmetleri arasındaki iletişimi hello otomatik olarak bulur. Sunucularınızın siz bunları – Kritik hizmetler sunan birbirine bağlı sistemler olarak düşündüğünüz tooview sağlar. Bir aracı yüklemesini dışında hiçbir yapılandırma TCP bağlı mimarisiyle arasında bağlantı noktaları gerekli ve hizmet Haritası sunucuları, işlemleri arasındaki bağlantıları gösterir. Daha fazla bilgi: [hizmet Haritası](../operations-management-suite/operations-management-suite-service-map.md).

İle tümleştirme, hello aşağıdaki örnekte gösterildiği gibi hello ITSM çözümlerinde oluşturulan hello hizmet Masası öğeleri görüntüleyebilirsiniz:

![Tümleşik çözüm ](./media/log-analytics-itsmc/itsmc-overview-integrated-solutions.png)
## <a name="create-itsm-work-items-for-oms-alerts"></a>OMS uyarılar için ITSM iş öğeleri oluşturma

Merhaba OMS uyarılar için bağlı hello ITSM kaynaklarında ilişkili iş öğeleri oluşturabilirsiniz.  toodo aşağıdaki yordamın bu, kullanım hello:

1. Gelen **günlük arama** penceresinde bir günlük arama sorgusu tooview verilerini çalıştırın. Sorgu sonuçları, iş öğeleri için hello kaynağıdır.
2. İçinde **günlük arama**, tıklatın **uyarı** tooopen hello **uyarı kuralı Ekle** sayfası.

    ![Günlük analizi ekranı](./media/log-analytics-itsmc/itsmc-work-items-for-oms-alerts.png)

3. Hello üzerinde **uyarı kuralı Ekle** penceresinde hello gerekli ayrıntılarını sağlamak **adı**, **önem**, **arama sorgusu**, ve  **Uyarı ölçütleri** (zaman penceresi/ölçü ölçüm).
4. Seçin **Evet** için **ITSM Eylemler**.
5. Hello ITSM bağlantınızı seçin **seçin bağlantı** listesi.
6. Gerekli Hello ayrıntıları belirtin.
7. Bu uyarı, select hello her günlük girdisi için ayrı iş öğesi toocreate **her günlük girişinin için tek tek iş öğeleri oluşturma** onay kutusu.

    Veya

    Bu uyarı altında günlük girişlerini herhangi bir sayıda için bu onay kutusu seçili toocreate yalnızca bir iş öğesi bırakın.

7. **Kaydet** düğmesine tıklayın.

Merhaba OMS uyarı altında oluşturulacak **uyarıları**. Merhaba karşılık gelen ITSM bağlantının iş Hello belirtilen uyarının koşulu karşılandığında öğeleri oluşturulur.

## <a name="create-itsm-work-items-from-oms-logs"></a>OMS günlüklerinden ITSM iş öğeleri oluşturma

OMS günlük arama kullanarak bağlı hello ITSM kaynaklarında iş öğeleri oluşturabilirsiniz. toodo aşağıdaki yordamın bu, kullanım hello:

1. Gelen **günlük arama**, gerekli hello veri arama, hello ayrıntı seçin ve'ı tıklatın **oluşturma çalışma öğesini**.

    Merhaba **oluşturma ITSM iş öğesi** penceresi görüntülenir:

    ![Günlük analizi ekranı](media/log-analytics-itsmc/itsmc-work-items-from-oms-logs.png)

2.   Aşağıdaki ayrıntılara hello ekleyin:

  - **İş öğesi başlık**: hello iş öğesi için başlık.
  - **İş öğesi tanımı**: hello yeni iş öğesi için bir açıklama.
  - **Bilgisayar etkilenen**: Bu günlük verileri nerede bulundu hello bilgisayarın adı.
  - **Bağlantıyı seçin**: ITSM bağlantı istediğiniz toocreate bu iş öğesi.
  - **İş öğesi**: iş öğesi türü.

3. toouse var olan bir iş öğesi şablonunu bir olay için tıklatın **Evet** altında **Generate iş öğesi hello şablona dayalı** seçeneğini ve ardından **oluşturma**.

    Veya

    Tıklatın **Hayır** özelleştirilmiş değerlerinizi tooprovide istiyorsanız.

4. Merhaba Hello uygun değerleri sağlayın **kişi türündeki**, **etkisi**, **aciliyet**, **kategori**, ve **alt kategori**  metin kutuları ve ardından **oluşturma**.

Merhaba iş öğesi hello OMS içinde de görüntüleyebilirsiniz ITSM içinde oluşturulacak.

## <a name="troubleshoot-itsm-connections-in-oms"></a>OMS ITSM bağlantı sorunlarını giderme
1.  Bağlantı başarısız bağlı kaynağın kullanıcı Arabiriminden ve hello alma **bağlantı kaydetmede hata** iletisi, aşağıdaki hello:
 - ServiceNow, Cherwell ve Provance bağlantıları durumunda doğru girilen hello kullanıcı adı/parola ve istemci kimliği/istemci parolası hello bağlantıların her biri için olun. Merhaba hata devam ederse hello karşılık gelen ITSM ürün toomake hello bağlantısında yeterli ayrıcalıkları olup olmadığını denetleyin.
 - Service Manager durumunda hello Web uygulaması başarıyla dağıtılır ve karma bağlantı oluşturulan emin olun. Merhaba Web uygulaması URL'si hello sağlama hello belgelerinde ayrıntılı olarak ziyaret edin hello şirket içi Service Manager makineyle tooverify hello bağlantı kuran başarıyla [karma bağlantı](log-analytics-itsmc-connections.md#configure-the-hybrid-connection).

2.  ServiceNow verileri OMS eşitlenmedi, bu hello ServiceNow örneğinin değil uykuda emin olun. Bu süre hello ServiceNow geliştirme örnekleri, boşta kalma zaman meydana gelir. Başka rapor hello sorun.
3.  OMS uyarıları tetiklenir iş öğelerini ITSM üründe oluşturulmaz veya yapılandırma öğeleri toowork oluşturulan ve bağlantılı öğeler alamıyorsanız ancak veya herhangi bir genel bilgi için aşağıdaki hello:
 -  OMS portalı BT Hizmet Yönetimi Bağlayıcısı çözümde kullanılan tooget bağlantıları/iş öğeleri/bilgisayarların vb. özetini olabilir. Merhaba durum dikey penceresinde Hello hata iletisi'ı tıklatın, çok gidin**günlük arama** ve hello hata iletisinde hello ayrıntıları kullanarak hello hatalı hello bağlantı görüntüleyin.
 - hello doğrudan hello hataları ve ilgili bilgileri görüntüleyebilirsiniz **günlük arama** kullanarak sayfa *türü ServiceDeskLog_CL =*.

## <a name="troubleshoot-service-manager-web-app-deployment"></a>Service Manager Web uygulama dağıtım sorunlarını gider
1.  Web uygulama dağıtımına herhangi bir sorun olması durumunda hello abonelikte yeterli izinlere sahip olduğundan emin olun toocreate ve dağıtma kaynakları belirtiliyor.
2.  Varsa **nesne başvurusu bir nesnenin tooinstance ayarlanmamış** hata iletisi görüntüleniyor hello çalıştırılırken [betik](log-analytics-itsmc-service-manager-script.md) altında geçerli değerler girdiğinizden emin olun **Kullanıcı Yapılandırması**bölümü.
3.  Toocreate hizmet veri yolu geçişi ad başarısız olursa, o hello kaynak sağlayıcısı hello abonelikte kayıtlı gerekli emin olun. El ile kayıtlı değil, Azure portal hello oluşturun. Bunu sırasında da oluşturabilirsiniz [hello karma bağlantı oluşturma](log-analytics-itsmc-connections.md#configure-the-hybrid-connection) hello Azure Portalı'ndan.


## <a name="contact-us"></a>Bizimle iletişim kurun

Tüm sorgular veya hello BT Hizmet Yönetimi Bağlayıcısı geribildirim için adresinden bize başvurun [ omsitsmfeedback@microsoft.com ](mailto:omsitsmfeedback@microsoft.com).

## <a name="next-steps"></a>Sonraki adımlar
[ITSM ürünler/hizmetler tooIT Hizmet Yönetimi Bağlayıcısı eklemek](log-analytics-itsmc-connections.md).
