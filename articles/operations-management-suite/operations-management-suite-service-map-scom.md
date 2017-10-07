---
title: "aaaService System Center Operations Manager ile tümleştirme Haritası | Microsoft Docs"
description: "Linux sistemleri ve haritalar Hizmetleri arasındaki iletişimi hello ve hizmet Haritası Windows uygulama bileşenleri otomatik olarak bulur bir Operations Management Suite çözümüdür. Hizmet eşlemesi kullanarak bu makalede ele tooautomatically Operations Manager'da dağıtılmış uygulama diyagramları oluşturun."
services: operations-management-suite
documentationcenter: 
author: daveirwin1
manager: jwhit
editor: tysonn
ms.assetid: e8614a5a-9cf8-4c81-8931-896d358ad2cb
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/21/2017
ms.author: bwren;dairwin
ms.openlocfilehash: cff9cce2559448ec3a5fd14087b867f314716560
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="service-map-integration-with-system-center-operations-manager"></a>System Center Operations Manager ile hizmet Haritası tümleştirme
  > [!NOTE]
  > Bu özellik genel önizlemede değil.
  > 
  
Operations Management Suite hizmet Haritası otomatik olarak sistemlerde, Windows ve Linux uygulama bileşenleri bulur ve Hizmetleri arasındaki hello iletişim eşler. Hizmet eşlemesi tooview Kritik hizmetler sunan birbirine bağlı sistemler olarak düşündüğünüz birini sunucuları hello yolunuzu sağlar. Hizmet eşlemesi herhangi TCP bağlı mimarisi hello yanı sıra bir aracının yüklenmesi gereken herhangi bir yapılandırma boyunca sunucuları, işlemleri ve bağlantı noktaları arasındaki bağlantıları gösterir. Daha fazla bilgi için bkz: Merhaba [hizmet Haritası belgelerine](operations-management-suite-service-map.md).

İle tümleştirme arasında hizmet Haritası ve System Center Operations Manager, Operations Manager'da, hizmet eşlemesinde hello dinamik bağımlılık eşlemeleri temel alan dağıtılmış uygulama diyagramları otomatik olarak oluşturabilirsiniz.

## <a name="prerequisites"></a>Ön koşullar
* Sunucular kümesi yönetme bir Operations Manager yönetim grubu.
* Bir Operations Management Suite çalışma alanı hello etkin hizmet Haritası çözüm ile.
* Operations Manager ve gönderen veri tooService eşleme tarafından yönetilen sunucular kümesi (en az bir tane). Windows ve Linux sunucuları desteklenir.
* Bir hizmet sorumlusu erişim toohello hello Operations Management Suite çalışma alanıyla ilişkili Azure aboneliği ile. Daha fazla bilgi için çok Git[bir hizmet sorumlusu oluşturma](#creating-a-service-principal).

## <a name="install-hello-service-map-management-pack"></a>Merhaba hizmet Haritası Yönetimi paketini yükleyin
Operations Manager ile hizmet Haritası arasında hello tümleştirme hello Microsoft.SystemCenter.ServiceMap Yönetim Paketi grubu (Microsoft.SystemCenter.ServiceMap.mpb) alarak etkinleştirin. Merhaba paket yönetim paketleri aşağıdaki hello içerir:
* Microsoft hizmet eşlemesi uygulama görünümleri
* Microsoft System Center hizmet Haritası iç
* Microsoft System Center hizmeti harita geçersiz kılmaları
* Microsoft System Center hizmet eşlemesi

## <a name="configure-hello-service-map-integration"></a>Merhaba hizmet Haritası tümleştirmesini yapılandırma
Merhaba hizmet Haritası Yönetim Paketi, yeni bir düğüm yükledikten sonra **hizmet Haritası**, altında görüntülenen **Operations Management Suite** hello içinde **Yönetim** bölmesi. 

tooconfigure hizmet Haritası tümleştirme hello aşağıdaki:

1. tooopen hello Yapılandırma Sihirbazı ' nda hello **hizmet eşlemesi genel bakış** bölmesinde tıklatın **çalışma Ekle**.  

    ![Hizmet eşlemesi genel bakış bölmesinde](media/oms-service-map/scom-configuration.png)

2. Merhaba, **bağlantı yapılandırması** penceresinde hello Kiracı adı veya kimliği, uygulama kimliği (Merhaba kullanıcı adı veya istemci kimliği olarak da bilinir) ve hello hizmet sorumlusu parolasını girin ve ardından **sonraki**. Daha fazla bilgi için çok Git[bir hizmet sorumlusu oluşturma](#creating-a-service-principal).

    ![Merhaba Bağlantı Yapılandırması penceresi](media/oms-service-map/scom-config-spn.png)

3. Merhaba, **abonelik seçimi** penceresinde hello Azure abonelik, Azure kaynak grubu (Merhaba hello Operations Management Suite çalışma içeren bir) ve Operations Management Suite çalışma alanı seçin ve ardından **Sonraki**.

    ![Merhaba Operations Manager yapılandırma çalışma alanı](media/oms-service-map/scom-config-workspace.png)

4. Merhaba, **makine Grup Seçimi** penceresinde, hangi hizmet eşlemesi makine grupları seçin toosync tooOperations Yöneticisi istiyor. Tıklatın **Ekle/Kaldır makine grupları**, grupları hello listesinden seçim **kullanılabilir makine grupları**, tıklatıp **Ekle**.  Grupları seçmek bittiğinde tıklatın **Tamam** toofinish.
    
    ![Merhaba Operations Manager yapılandırma makine grupları](media/oms-service-map/scom-config-machine-groups.png)
    
5. Merhaba, **sunucu seçimi** penceresinde, yapılandırdığınız hello hizmet eşlemesi sunucuları grubu toosync Operations Manager ve hizmet eşlemesi arasında istediğiniz hello sunucularıyla. Tıklatın **sunucuları Ekle/Kaldır**.   
    
    Merhaba tümleştirme toobuild için bir sunucu için bir dağıtılmış uygulama diyagram hello sunucu olması gerekir:

    * Operations Manager tarafından yönetilen
    * Hizmet eşlemesi tarafından yönetilen
    * Merhaba hizmet eşlemesi sunucuları grubu listelenen

    ![Merhaba Operations Manager Yapılandırma grubu](media/oms-service-map/scom-config-group.png)

6. İsteğe bağlı: Hello yönetim sunucusu kaynak havuzu toocommunicate Operations Management Suite ile seçin ve ardından **çalışma alanı Ekle**.

    ![Merhaba Operations Manager yapılandırma kaynak havuzu](media/oms-service-map/scom-config-pool.png)

    Dakika tooconfigure ele ve hello Operations Management Suite çalışma kaydetmek. Bunu yapılandırıldıktan sonra Operations Manager Operations Management Suite hello ilk hizmet Haritası eşitleme başlatır.

    ![Merhaba Operations Manager yapılandırma kaynak havuzu](media/oms-service-map/scom-config-success.png)


## <a name="monitor-service-map"></a>İzleyici hizmet eşlemesi
Merhaba Operations Management Suite çalışma bağlandıktan sonra yeni bir klasör, hizmet Haritası hello görüntülenir **izleme** hello Operations Manager konsolunun bölmesinde.

![Hello bölmesini Operations Manager izleme](media/oms-service-map/scom-monitoring.png)

dört düğüm Hello hizmet Haritası klasör içerir:
* **Etkin uyarılar**: tüm hello etkin uyarıları Operations Manager hizmet Haritası arasında hello iletişimi hakkında listeler.  Bu uyarılar eşitlenen tooOperations yöneticisi olan Operations Management Suite uyarıları olmadığına dikkat edin. 

* **Sunucuları**: listeleri hello izlenen sunucular toosync hizmet eşlemesinden yapılandırılmış.

    ![Merhaba Operations Manager izleme sunucuları bölmesi](media/oms-service-map/scom-monitoring-servers.png)

* **Makine grubu bağımlılık görünümleri**: hizmet eşlemesinden eşitlenen tüm makine grupları listeler. Dağıtılmış uygulama diyagramı hiçbir grup tooview tıklayabilirsiniz.

    ![Merhaba Operations Manager dağıtılmış uygulama diyagramı](media/oms-service-map/scom-group-dad.png)

* **Server bağımlılık görünümleri**: hizmet eşlemesinden eşitlenen tüm sunucuları listeler. Dağıtılmış uygulama diyagramı tüm sunucu tooview tıklayabilirsiniz.

    ![Merhaba Operations Manager dağıtılmış uygulama diyagramı](media/oms-service-map/scom-dad.png)

## <a name="edit-or-delete-hello-workspace"></a>Düzenleme veya silme hello çalışma
Düzenleme veya yapılandırılmış hello çalışma hello aracılığıyla silme **hizmet eşlemesi genel bakış** bölmesinde (**Yönetim** bölmesinde > **Operations Management Suite**  >  **Hizmet eşlemesi**). Şu an için yalnızca bir Operations Management Suite çalışma yapılandırabilirsiniz.

![Merhaba Operations Manager çalışma alanını Düzenle bölmesi](media/oms-service-map/scom-edit-workspace.png)

## <a name="configure-rules-and-overrides"></a>Kuralları ve geçersiz kılmalar yapılandırın
Bir kural _Microsoft.SystemCenter.ServiceMapImport.Rule_, tooperiodically fetch bilgi hizmeti eşlemesinden oluşturulur. toochange eşitleme zamanlamalarını, geçersiz kılmalar hello kuralının yapılandırabilirsiniz (**yazma** bölmesinde > **kuralları** > **Microsoft.SystemCenter.ServiceMapImport.Rule**).

![Merhaba Operations Manager geçersiz kılan özellikler penceresi](media/oms-service-map/scom-overrides.png)

* **Etkin**: etkinleştirmek veya Otomatik Güncelleştirmeler devre dışı. 
* **IntervalMinutes**: sıfırlama güncelleştirmeler arasındaki hello süre. Merhaba varsayılan zaman aralığı bir saattir. Toosync sunucu eşlemeleri daha sık isterseniz hello değeri değiştirebilirsiniz.
* **TimeoutSeconds**: hello isteği zaman aşımına uğramadan önce hello süreyi Sıfırla. 
* **TimeWindowMinutes**: veri sorgulama için sıfırlama hello zaman penceresi. Varsayılan değer 60 dakikalık ' dir. Hizmet eşlemesi tarafından izin verilen hello en büyük değer 60 dakikadır.

## <a name="known-issues-and-limitations"></a>Bilinen sorunlar ve sınırlamalar

Merhaba geçerli tasarım sunar hello aşağıdaki sorunlar ve sınırlamalar:
* Yalnızca tooa tek Operations Management Suite çalışma bağlanabilir.
* Sunucuları toohello hizmet eşlemesi sunucuları grubu hello el ile eklemesi mümkün olsa da **yazma** bölmesinde, bu sunucular için hello eşlemeleri olmayan eşitlenen hemen.  Bunlar hizmet eşlemesinden hello sonraki eşitleme döngüsü sırasında senkronize edilir.
* Toohello dağıtılmış uygulama hello Yönetim Paketi tarafından oluşturulan diyagramları herhangi bir değişiklik yaparsanız, bu değişiklikleri olasılıkla hello sonraki eşitleme ile hizmet eşlemesi üzerinde üzerine yazılır.

## <a name="create-a-service-principal"></a>Hizmet sorumlusu oluşturma
Bir hizmet sorumlusu oluşturma hakkında daha fazla resmi Azure belgeler için bkz:
* [PowerShell kullanarak bir hizmet sorumlusu oluşturma](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [Azure CLI kullanarak bir hizmet sorumlusu oluşturma](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli)
* [Hello Azure portal kullanarak bir hizmet sorumlusu oluşturma](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal)

### <a name="feedback"></a>Geri Bildirim
Tüm geri bildirim bize hizmet haritası veya bu belge hakkında var? Ziyaret bizim [kullanıcı sesi sayfa](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map), buradan özellikleri önermek veya varolan önerilere oy verin.
