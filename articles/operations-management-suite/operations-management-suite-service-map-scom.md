---
title: "System Center Operations Manager ile hizmet Haritası tümleştirme | Microsoft Docs"
description: "Hizmet eşlemesi otomatik olarak sistemlerde, Windows ve Linux uygulama bileşenleri bulur ve Hizmetleri arasındaki iletişimi eşleyen bir Operations Management Suite çözümüdür. Bu makalede dağıtılmış uygulama diyagramları Operations Manager'da otomatik olarak oluşturmak için hizmet eşlemesi kullanarak anlatılmaktadır."
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
ms.openlocfilehash: af1f683f08ff6b70b23ff265f39b9a76f92f4be2
ms.sourcegitcommit: 8aa014454fc7947f1ed54d380c63423500123b4a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/23/2017
---
# <a name="service-map-integration-with-system-center-operations-manager"></a>System Center Operations Manager ile hizmet Haritası tümleştirme
  > [!NOTE]
  > Bu özellik genel önizlemede değil.
  > 
  
Operations Management Suite hizmet Haritası otomatik olarak sistemlerde, Windows ve Linux uygulama bileşenleri bulur ve Hizmetleri arasındaki iletişimi eşler. Hizmet eşlemesi, bunları, kritik hizmet sunmak birbirine bağlı sistemler olarak düşünme yolu sunucularınızı görüntülemenizi sağlar. Hizmet eşlemesi herhangi TCP bağlı mimarisi yanı sıra bir aracının yüklenmesi gereken herhangi bir yapılandırma boyunca sunucuları, işlemleri ve bağlantı noktaları arasındaki bağlantıları gösterir. Daha fazla bilgi için bkz: [hizmet Haritası belgelerine](operations-management-suite-service-map.md).

İle tümleştirme arasında hizmet Haritası ve System Center Operations Manager, Operations Manager'da, hizmet eşlemesinde dinamik bağımlılık eşlemeleri temel alan dağıtılmış uygulama diyagramları otomatik olarak oluşturabilirsiniz.

## <a name="prerequisites"></a>Ön koşullar
* Bir Operations Manager yönetim grubu (2012 R2 veya sonrası) sunucular kümesi yönetme.
* Bir Operations Management Suite çalışma alanı etkin hizmet Haritası çözümle.
* Operations Manager ve hizmet eşlemesi için verileri gönderilirken tarafından yönetilen sunucular kümesi (en az bir tane). Windows ve Linux sunucuları desteklenir.
* Operations Management Suite çalışma alanı ile ilişkili Azure abonelik erişimi olan bir hizmet sorumlusu. Daha fazla bilgi için Git [bir hizmet sorumlusu oluşturma](#creating-a-service-principal).

## <a name="install-the-service-map-management-pack"></a>Hizmet eşlemesi Yönetimi paketini yükleyin
Operations Manager ile hizmet Haritası arasında tümleştirme Microsoft.SystemCenter.ServiceMap Yönetim Paketi (Microsoft.SystemCenter.ServiceMap.mpb) alarak etkinleştirin. Yönetim Paketi karşıdan yükleyebileceğiniz [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=55763). Paket aşağıdaki yönetim paketlerini içerir:
* Microsoft hizmet eşlemesi uygulama görünümleri
* Microsoft System Center hizmet Haritası iç
* Microsoft System Center hizmeti harita geçersiz kılmaları
* Microsoft System Center hizmet eşlemesi

## <a name="configure-the-service-map-integration"></a>Hizmet eşlemesi tümleştirmesini yapılandırma
Hizmet eşlemesi Yönetim Paketi, yeni bir düğüm yükledikten sonra **hizmet Haritası**, altında görüntülenen **Operations Management Suite** içinde **Yönetim** bölmesi. 

Hizmet eşlemesi tümleştirmesini yapılandırmak için aşağıdakileri yapın:

1. Yapılandırma Sihirbazı'nı açmak için **hizmet eşlemesi genel bakış** bölmesinde tıklatın **çalışma Ekle**.  

    ![Hizmet eşlemesi genel bakış bölmesinde](media/oms-service-map/scom-configuration.png)

2. İçinde **bağlantı yapılandırması** penceresinde, Kiracı adı veya kimliği, uygulama kimliği (kullanıcı adı veya istemci kimliği olarak da bilinir) ve hizmet sorumlusu parolasını girin ve ardından **sonraki**. Daha fazla bilgi için Git [bir hizmet sorumlusu oluşturma](#creating-a-service-principal).

    ![Bağlantı Yapılandırması penceresi](media/oms-service-map/scom-config-spn.png)

3. İçinde **abonelik seçimi** penceresinde, Azure abonelik, Azure kaynak grubu (Operations Management Suite çalışma alanı içeren bir) ve Operations Management Suite çalışma alanı seçin ve ardından**Sonraki**.

    ![Operations Manager yapılandırma çalışma alanı](media/oms-service-map/scom-config-workspace.png)

4. İçinde **makine Grup Seçimi** penceresinde, Operations Manager'a eşitlemek istediğinizden hangi hizmet eşlemesi makine grupları seçin. Tıklatın **Ekle/Kaldır makine grupları**, gruplar listesinden seçim **kullanılabilir makine grupları**, tıklatıp **Ekle**.  Grupları seçmek bittiğinde tıklatın **Tamam** tamamlamak için.
    
    ![Operations Manager yapılandırma makine grupları](media/oms-service-map/scom-config-machine-groups.png)
    
5. İçinde **sunucu seçimi** penceresinde, yapılandırdığınız hizmet eşlemesi sunucuları grubu Operations Manager ile hizmet Haritası arasında eşitlemek istediğiniz sunucuları ile. Tıklatın **sunucuları Ekle/Kaldır**.   
    
    Bir sunucu için bir dağıtılmış uygulama diyagram derleme tümleştirmesi için sunucu olması gerekir:

    * Operations Manager tarafından yönetilen
    * Hizmet eşlemesi tarafından yönetilen
    * Hizmet eşlemesi sunucuları grubu listelenen

    ![Operations Manager Yapılandırma grubu](media/oms-service-map/scom-config-group.png)

6. İsteğe bağlı: Operations Management Suite ile iletişim kurmak için yönetim sunucusu kaynak havuzu seçin ve ardından **çalışma alanı Ekle**.

    ![Operations Manager yapılandırma kaynak havuzu](media/oms-service-map/scom-config-pool.png)

    Yapılandırmak ve Operations Management Suite çalışma alanı kaydetmek için bir dakika sürebilir. Bunu yapılandırıldıktan sonra Operations Manager Operations Management Suite ilk hizmet Haritası eşitlemenin başlatır.

    ![Operations Manager yapılandırma kaynak havuzu](media/oms-service-map/scom-config-success.png)


## <a name="monitor-service-map"></a>İzleyici hizmet eşlemesi
Operations Management Suite çalışma bağlandıktan sonra yeni bir klasör, hizmet Haritası görüntülenen **izleme** Operations Manager Konsolu bölmesi.

![Operations Manager izleme bölmesi](media/oms-service-map/scom-monitoring.png)

Hizmet eşlemesi klasörü dört düğüm vardır:
* **Etkin uyarılar**: tüm etkin uyarıları Operations Manager ve hizmet eşlemesi arasındaki iletişimle ilgili listeler.  Bu uyarılar için Operations Manager eşitlenmiş Operations Management Suite uyarıları olmadığına dikkat edin. 

* **Sunucuları**: yapılandırılmış izlenen sunucuları listeler hizmet eşlemesinden eşitlenecek.

    ![Operations Manager izleme sunucuları bölmesi](media/oms-service-map/scom-monitoring-servers.png)

* **Makine grubu bağımlılık görünümleri**: hizmet eşlemesinden eşitlenen tüm makine grupları listeler. Dağıtılmış uygulama diyagramı görüntülemek için herhangi bir grubu tıklatabilirsiniz.

    ![Operations Manager dağıtılmış uygulama diyagramı](media/oms-service-map/scom-group-dad.png)

* **Server bağımlılık görünümleri**: hizmet eşlemesinden eşitlenen tüm sunucuları listeler. Dağıtılmış uygulama diyagramı görüntülemek için herhangi bir sunucu tıklatabilirsiniz.

    ![Operations Manager dağıtılmış uygulama diyagramı](media/oms-service-map/scom-dad.png)

## <a name="edit-or-delete-the-workspace"></a>Düzenleme veya çalışma alanını silme
Düzenleme veya yapılandırılmış çalışma alanını kullanarak silme **hizmet eşlemesi genel bakış** bölmesinde (**Yönetim** bölmesinde > **Operations Management Suite**  >  **Hizmet eşlemesi**). Şu an için yalnızca bir Operations Management Suite çalışma yapılandırabilirsiniz.

![Operations Manager çalışma alanını Düzenle bölmesi](media/oms-service-map/scom-edit-workspace.png)

## <a name="configure-rules-and-overrides"></a>Kuralları ve geçersiz kılmalar yapılandırın
Bir kural _Microsoft.SystemCenter.ServiceMapImport.Rule_, düzenli olarak bilgi hizmeti eşlemesinden getirmek için oluşturulur. Eşitleme zamanlamalarını değiştirmek için geçersiz kılmaları kural yapılandırabilirsiniz (**yazma** bölmesinde > **kuralları** > **Microsoft.SystemCenter.ServiceMapImport.Rule**) .

![Operations Manager geçersiz kılan özellikler penceresi](media/oms-service-map/scom-overrides.png)

* **Etkin**: etkinleştirmek veya Otomatik Güncelleştirmeler devre dışı. 
* **IntervalMinutes**: güncelleştirmeler arasındaki süre sıfırlayın. Varsayılan zaman aralığı bir saattir. Sunucu eşlemeleri daha sık eşitlemek isterseniz, değeri değiştirebilir.
* **TimeoutSeconds**: İstek zaman aşımına uğramadan önce geçen süreyi sıfırlayın. 
* **TimeWindowMinutes**: veri sorgulama için zaman penceresi sıfırlayın. Varsayılan değer 60 dakikalık ' dir. Hizmet eşlemesi tarafından izin verilen en büyük değer 60 dakikadır.

## <a name="known-issues-and-limitations"></a>Bilinen sorunlar ve sınırlamalar

Geçerli tasarım, aşağıdaki sorunlar ve sınırlamalar sunar:
* Yalnızca tek bir Operations Management Suite çalışma alanına bağlanabilir.
* Hizmet eşlemesi sunucuları grubu için el ile sunucuları ekleyebilseniz **yazma** bölmesinde, bu sunucular için eşlemeleri olmayan eşitlenen hemen.  Bunlar sonraki eşitleme döngüsü sırasında hizmet eşlemesinden eşitlenir.
* Dağıtılmış uygulama Yönetim Paketi tarafından oluşturulan diyagramları için herhangi bir değişiklik yaparsanız, bu değişiklikleri olasılıkla hizmet eşlemesi ile sonraki eşitleme üzerinde üzerine yazılır.

## <a name="create-a-service-principal"></a>Hizmet sorumlusu oluşturma
Bir hizmet sorumlusu oluşturma hakkında daha fazla resmi Azure belgeler için bkz:
* [PowerShell kullanarak bir hizmet sorumlusu oluşturma](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [Azure CLI kullanarak bir hizmet sorumlusu oluşturma](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli)
* [Azure portalını kullanarak bir hizmet sorumlusu oluşturma](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal)

### <a name="feedback"></a>Geri Bildirim
Tüm geri bildirim bize hizmet haritası veya bu belge hakkında var? Ziyaret bizim [kullanıcı sesi sayfa](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map), buradan özellikleri önermek veya varolan önerilere oy verin.
