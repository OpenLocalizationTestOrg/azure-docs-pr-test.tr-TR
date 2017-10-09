---
title: "aaaGet başlatılan bir Azure günlük analizi çalışma alanı ile | Microsoft Docs"
description: "Log Analytics içindeki bir çalışma alanını birkaç dakika içinde kullanmaya başlayabilirsiniz."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 508716de-72d3-4c06-9218-1ede631f23a6
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/08/2017
ms.author: magoedte
ms.openlocfilehash: 442a9258a37ee79e8f0b45759ef24b5e3dae0130
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-a-log-analytics-workspace"></a>Log Analytics çalışma alanını kullanmaya başlama
IT altyapınızdan toplanan çalışma bilgilerini değerlendirmenize yardımcı olan Azure Log Analytics’i birkaç dakika içinde kullanmaya başlayabilirsiniz. Bu makaleyi kullanarak, *ücretsiz olarak* topladığınız verileri keşfetmeye, analiz etmeye ve üzerinde işlem yapmaya kolayca başlayabilirsiniz.

Bu makalede bir giriş tooLog kısa bir öğretici toowalk kullanarak Analytics, Azure en az bir dağıtımda aracılığıyla hizmet hello hizmetini kullanarak başlatabilirsiniz. Merhaba mantıksal kapsayıcı Yönetimi verilerinizi Azure depolandığı bir çalışma alanı adı verilir. Bu bilgileri gözden geçirdikten ve kendi değerlendirme tamamlandıktan sonra hello Değerlendirme çalışma kaldırabilirsiniz. Bu makale bir öğretici olduğu için, iş gereksinimlerini, planlamayı veya mimari yönergelerini ele almaz.

>[!NOTE]
>Microsoft Azure kamu bulut hello kullanıyorsanız [Azure kamu izleme + Yönetimi belgeleri](https://docs.microsoft.com/azure/azure-government/documentation-government-services-monitoringandmanagement#log-analytics) yerine.

Aşağıda, başlatılan hello kullanılan işlem tooget hızlı bir bakış verilmiştir:

![işlem diyagramı](./media/log-analytics-get-started/onboard-oms.png)

## <a name="1-create-an-azure-account-and-sign-in"></a>1 Bir Azure hesabı oluşturup oturum açın

Zaten bir Azure hesabınız yoksa, toocreate bir toouse günlük analizi gerekir. Herhangi bir Azure hizmetine 30 gün boyunca erişmenizi sağlayan [ücretsiz bir hesap](https://azure.microsoft.com/free/) oluşturabilirsiniz.

### <a name="toocreate-a-free-account-and-sign-in"></a>toocreate ücretsiz bir hesap ve oturum açma
1. Merhaba yönergeleri izleyin [ücretsiz Azure hesabınızı oluşturmak](https://azure.microsoft.com/free/).
2. Toohello Git [Azure portal](https://portal.azure.com) ve oturum açın.

## <a name="2-create-a-workspace"></a>2 Çalışma alanı oluşturun

Merhaba sonraki toocreate bir çalışma alanı adımdır.

1. Merhaba Market hizmet hello listesini Hello Azure portal, arama için *günlük analizi*ve ardından **günlük analizi**.  
    ![Azure portal](./media/log-analytics-get-started/log-analytics-portal.png)
2. Tıklatın **oluşturma**, aşağıdaki öğelerindeki hello için seçenekleri seçin:
   * **OMS Çalışma Alanı** - Çalışma alanınız için bir ad yazın.
   * **Abonelik** - tooassociate hello yeni çalışma alanı ile istediğiniz hello seçin, birden çok aboneliğiniz varsa.
   * **Kaynak grubu**
   * **Konum**
   * **Fiyatlandırma katmanı**  
       ![hızlı oluşturma](./media/log-analytics-get-started/oms-onboard-quick-create.png)
3. Tıklatın **Tamam** toosee alanlarınızı listesi.
4. Bir çalışma alanı toosee hello Azure portal ayrıntılarını seçin.       
    ![çalışma alanı ayrıntıları](./media/log-analytics-get-started/oms-onboard-workspace-details.png)         

## <a name="3-upgrade-workspace-toonew-log-search"></a>3 yükseltme çalışma toonew günlük arama
Yeni bir günlük analizi sorgu dili serbest ve sipariş tootake faydalanılabileceği, çalışma alanınızı tooconvert gerekir.  Çalışma alanınız içinde barındırılan hello bölge yükselttiyseniz tooconvert davet çalışma alanınızı hello üstte mor başlık görmeniz gerekir. Merhaba yükseltme sağlanmaz ve günlük analizi ve eklediğiniz tüm çözümleri çalışma deneyiminizi etkilemez.  

Daha fazla bilgi toounderstand hello fayda, ilgili önemli noktalar ve işlem tooupgrade için bkz [yükseltme Azure günlük analizi toonew günlük arama](log-analytics-log-search-upgrade.md).  

## <a name="4-add-solutions-and-solution-offerings"></a>4 Çözüm ve çözüm teklifleri ekleme

Ardından, yönetim çözümleri ve çözüm teklifleri ekleyin. Yönetim çözümleri belirli bir sorun alanına odaklanan ölçümler sağlayan mantık, görselleştirme ve veri alımı kural koleksiyonudur. Çözüm teklifi ise bir yönetim çözümleri paketidir.

Çözümleri tooyour çalışma ekleme günlük analizi toocollect çeşitli aracıları kullanarak bağlı tooyour çalışma bilgisayarları verileri sağlar. Aracı ekleme işlemi daha sonra ele alınacaktır.

### <a name="tooadd-solutions-and-solution-offerings"></a>tooadd çözümleri ve çözümü teklifleri

1. Azure portalında tıklatın **yeni** ve ardından hello **arama hello Market** kutusuna **etkinlik günlük analizi** yazıp ENTER tuşuna basın.
2. İçindeki her şeyi hello dikey penceresinde, select **etkinlik günlük analizi** ve ardından **oluşturma**.  
    ![Activity Log Analytics](./media/log-analytics-get-started/activity-log-analytics.png)  
3. Merhaba, *yönetim çözümü adı* dikey penceresinde hello yönetim çözümüyle tooassociate istediğiniz çalışma alanı seçin.
4. **Oluştur**'a tıklayın.  
    ![çözüm çalışma alanı](./media/log-analytics-get-started/solution-workspace.png)  
5. 1-4 arası adımları tooadd Yinele:
    - Merhaba **güvenlik ve Uyumluluk** hizmeti ile Merhaba kötü amaçlı yazılımdan koruma değerlendirme ve güvenlik ve denetim çözümler sunar.
    - Merhaba **otomasyon ve Denetim** hello Otomasyon karma çalışanı, değişiklik izleme ve Sistem Güncelleştirmesi (güncelleştirme yönetimi olarak da bilinir) değerlendirmesi çözümleri sunarak hizmet. Merhaba çözüm sunan eklediğinizde, Automation hesabı oluşturmanız gerekir.  
        ![Otomasyon hesabı](./media/log-analytics-get-started/automation-account.png)  
6. Çok giderek tooyour çalışma eklenen hello yönetim çözümleri görüntüleyebilirsiniz**günlük analizi** > **abonelikleri** > ***çalışma alanı adı***  >  **Genel bakış**. Eklediğiniz hello yönetim çözümleri için kutucukları gösterilir.  
    >[!NOTE]
    >Biz henüz herhangi bir aracıları toohello çalışma bağlı olmayan çünkü eklediğiniz hello çözümleri için herhangi bir veri görmezsiniz.  

    ![veri olmadan çözüm kutucukları](./media/log-analytics-get-started/solutions-no-data.png)

## <a name="4-create-a-vm-and-onboard-an-agent"></a>4 VM oluşturma ve aracı ekleme

Ardından, Azure’da basit bir sanal makine oluşturun. VM, yerleşik hello OMS Aracısı tooenable oluşturduktan sonra. Etkinleştirme hello Aracısı VM hello veri toplamayı başlatır ve veri tooLog Analytics gönderir.

### <a name="toocreate-a-virtual-machine"></a>toocreate bir sanal makine

- Merhaba yönergeleri izleyin [hello Azure portalında, ilk Windows sanal makine oluşturma](../virtual-machines/virtual-machines-windows-hero-tutorial.md) ve hello yeni bir sanal makine başlatın.

### <a name="connect-hello-virtual-machine-toolog-analytics"></a>Merhaba sanal makine tooLog Analytics Bağlan

- Merhaba yönergeleri izleyin [bağlanmak Azure sanal makineleri tooLog Analytics](log-analytics-azure-vm-extension.md) tooconnect hello VM tooLog analizi kullanarak hello Azure portalı.

## <a name="6-view-and-act-on-data"></a>6 Verileri görüntüleme ve üzerinde işlem yapma

Daha önce hello etkinlik günlüğü analiz çözümü ve hello güvenlik ve uyumluluk ve otomasyon ve denetim hizmet teklifleri etkin. Bundan sonra, çözümler tarafından toplanan verilere ve günlük aramalarındaki sonuçlara bakmaya başlayacağız.

toostart, çözüm içinde görüntülenen verileri bakın. Ardından, günlük aramalarından erişilen bazı günlük aramalarına bakın. Günlük arar ve ortamınızda birden fazla kaynaktan herhangi bir makine verilerin bağıntısını toocombine izin verin. Daha fazla bilgi için bkz: [günlük analizi aramaları oturum](log-analytics-log-searches.md) veya çalışma toohello yeni sorgu dilini dönüştürülürse, bkz. [anlama günlük arar günlük analizi](log-analytics-log-search-new.md). 

### <a name="tooview-antimalware-data"></a>tooview kötü amaçlı yazılımdan koruma verileri

1. İçinde Azure portal Merhaba, çok gidin**günlük analizi** > ***çalışma alanınızı***.
2. Çalışma alanınız için hello dikey altında **genel**, tıklatın **genel bakış**.  
    ![Genel Bakış](./media/log-analytics-get-started/overview.png)
3. Merhaba tıklatın **kötü amaçlı yazılımdan koruma değerlendirme** döşeme. Bu örnekte bir bilgisayara Windows Defender’ın yüklü olduğunu, ancak imzasının eski olduğunu görebilirsiniz.  
    ![Kötü Amaçlı Yazılımdan Koruma](./media/log-analytics-get-started/solution-antimalware.png)
4. Bu örneğin altında **koruma durumu**, tıklatın **imza güncel** tooopen günlük arama ile ilgili ayrıntıları görüntülemenin güncel imzalara sahip olduğunu hello bilgisayarlar. Bu örnekte, bu hello bilgisayar adlandırılan Not *getstarted*. Güncel imzalara sahip birden çok bilgisayar varsa, bunlar tüm hello günlük arama sonuçları görüntülenir.  
    ![Kötü amaçlı yazılımdan koruma eski](./media/log-analytics-get-started/antimalware-search.png)

### <a name="tooview-security-and-audit-data"></a>tooview güvenlik ve denetim verileri

1. Çalışma alanınız için hello dikey altında **genel**, tıklatın **genel bakış**.  
2. Merhaba tıklatın **güvenlik ve Denetim** döşeme. Bu örnekte, öne çıkan iki sorun olduğunu görebilirsiniz: kritik güncelleştirmeleri eksik olan bir bilgisayar ve koruması yetersiz olan bir bilgisayar vardır.  
    ![Güvenlik ve Denetim](./media/log-analytics-get-started/security-audit.png)
3. Bu örneğin altında **önem düzeyindeki sorunlar**, tıklatın **kritik güncelleştirmeleri eksik olan bilgisayarlar** tooopen günlük arama ile ilgili ayrıntıları görüntülemenin kritik güncelleştirmeleri eksik olan bilgisayarlar. Bu örnekte, bir kritik güncelleştirme ve 63 diğer güncelleştirme eksiktir.  
    ![Güvenlik ve Denetim Günlük Araması](./media/log-analytics-get-started/security-audit-log-search.png)

### <a name="tooview-and-act-on-system-update-data"></a>tooview ve sistem güncelleştirmesi veri vermemizi

1. Çalışma alanınız için hello dikey altında **genel**, tıklatın **genel bakış**.  
2. Merhaba tıklatın **Sistem Güncelleştirme değerlendirmesi** döşeme. Bu örnekte, kritik güncelleştirme gerektiren *getstarted* adlı bir Windows bilgisayarın ve tanım güncelleştirmeleri gerektiren bir bilgisayarın olduğunu görebilirsiniz.  
    ![Sistem Güncelleştirmeleri](./media/log-analytics-get-started/system-updates.png)
3. Bu örneğin altında **eksik güncelleştirmeleri**, tıklatın **kritik güncelleştirmeler** tooopen günlük arama ile ilgili ayrıntıları görüntülemenin kritik güncelleştirmeleri eksik olan bilgisayarlar. Bu örnekte, bir eksik güncelleştirme ve bir gerekli güncelleştirme vardır.  
    ![Sistem Güncelleştirmeleri Günlük Araması](./media/log-analytics-get-started/system-updates-log-search.png)
4. Toohello Git [Operations Management Suite](http://microsoft.com/oms) Web sitesi ve Azure hesabınızla oturum açın. Oturum zaman hello çözüm bilgileri hello Azure portalına bakın benzer toowhat olduğuna dikkat edin.  
    ![OMS portalı](./media/log-analytics-get-started/oms-portal.png)
5. Merhaba tıklatın **güncelleştirme yönetimi** döşeme.
6. Merhaba güncelleştirme yönetimi panosunda hello sistem güncelleştirmesi bilgileri benzer toohello sistem güncelleştirmesi bilgileri hello Azure portalında gördüğünüz olduğuna dikkat edin. Ancak, hello **güncelleştirme dağıtımları yönetmek** döşeme yenidir. Merhaba tıklatın **güncelleştirme dağıtımları yönetmek** döşeme.  
    ![Güncelleştirme Yönetimi kutucuğu](./media/log-analytics-get-started/update-management.png)
7. Merhaba üzerinde **güncelleştirme dağıtımları** sayfasında, **Ekle** toocreate bir *güncelleştirme çalışması*.  
    ![Güncelleştirme Dağıtımları](./media/log-analytics-get-started/update-management-update-deployments.png)
8.  Merhaba üzerinde **yeni güncelleştirme dağıtımını** sayfasında hello güncelleştirme dağıtımı için bir ad yazın, bilgisayarları tooupdate seçin (Bu örnekte, *getstarted*), bir zamanlamayı seçin ve ardından **Kaydet**.  
    ![Yeni Dağıtım](./media/log-analytics-get-started/new-deployment.png)  
    Merhaba güncelleştirme dağıtımı kaydettikten sonra zamanlanmış hello bkz güncelleştirin.  
    ![zamanlanmış güncelleştirme](./media/log-analytics-get-started/scheduled-update.png)  
    Merhaba güncelleştirme çalışması tamamlandıktan sonra hello durumu **tamamlandı**.
    ![biten güncelleştirme](./media/log-analytics-get-started/completed-update.png)
9. Merhaba güncelleştirme çalışması bittikten sonra hello çalıştırmak veya başarılı oldu ve hangi güncelleştirmelerin uygulanmış burada ilgili ayrıntıları görüntüleyebilirsiniz olup olmadığını görüntüleyebilirsiniz.

## <a name="after-evaluation"></a>Değerlendirme sonrasında

Bu öğreticide bir sanal makineye aracı yükleyip hızlıca çalışmaya başladınız. izlediğiniz hello adımları hızlı ve kolay. Ancak, çoğu büyük kuruluş ve işletme, karmaşık şirket içi BT altyapılarına sahiptir. Başlangıç Öğreticisi daha bu nedenle, bu karmaşık ortamlarından verileri toplama ek planlama ve çaba alır. Bağlantılar toohelpful makaleler için sonraki adımlar bölümüne aşağıdaki hello Hello bilgileri gözden geçirin.

İsteğe bağlı olarak bu öğreticiyle oluşturulan hello çalışma kaldırabilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar
* Bağlanma hakkında bilgi edinin [Windows aracıları](log-analytics-windows-agents.md) tooLog Analytics.
* Bağlanma hakkında bilgi edinin [Operations Manager aracıları](log-analytics-om-agents.md) tooLog Analytics.
* [Günlük analizi çözümleri Çözümleri Galerisi hello eklemek](log-analytics-add-solutions.md) tooadd işlevselliği ve toplama verileri.
* İle tanışın [oturum aramaları](log-analytics-log-searches.md) tooview ayrıntılı çözümler tarafından toplanan bilgiler.
