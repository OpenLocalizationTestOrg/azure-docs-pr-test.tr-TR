---
title: aaaHow tooconfigure bir bulut hizmeti (portal) | Microsoft Docs
description: "Tooconfigure bulut Azure hizmetleri nasıl öğrenin. Uzaktan erişim toorole örnekleri yapılandırmak ve tooupdate hello bulut hizmeti yapılandırması öğrenin. Bu örnekler hello Azure portalını kullanın."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 7308f3c0-825e-499d-bfa5-c60f86371921
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/07/2016
ms.author: adegeo
ms.openlocfilehash: 969a08558473e8c79153192942bfda587eb5ada5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-cloud-services"></a>TooConfigure Cloud Services nasıl
> [!div class="op_single_selector"]
> * [Azure portal](cloud-services-how-to-configure-portal.md)
> * [Klasik Azure Portalı](cloud-services-how-to-configure.md)
>
>

Hello Azure portalında bir bulut hizmeti için en yaygın olarak kullanılan hello ayarlarını yapılandırabilirsiniz. Veya tooupdate isterseniz yapılandırma dosyalarını doğrudan bir hizmet yapılandırma dosyası tooupdate indirin ve güncelleştirilmiş hello dosya ve güncelleştirme hello bulut hizmetiyle hello yapılandırma değişiklikleri karşıya yükleyin. Her iki durumda da hello yapılandırma güncelleştirmeleri tooall rol örnekleri atılır.

Ayrıca hello örneğine, bulut hizmeti rollerinizi ya da Uzak Masaüstü bunları yönetebilirsiniz.

Her rol için en az iki rol örneği varsa, azure yalnızca 99,95 yüzde hizmet kullanılabilirliği hello sırasında yapılandırma güncelleştirmeleri emin olabilirsiniz. Merhaba diğer güncelleştirilirken, bir sanal makine tooprocess istemci isteklerini etkinleştirir. Daha fazla bilgi için bkz: [hizmet düzeyi sözleşmeleri](https://azure.microsoft.com/support/legal/sla/).

## <a name="change-a-cloud-service"></a>Bir bulut hizmeti değiştirme
Açılış hello sonra [Azure portal](https://portal.azure.com/), tooyour bulut hizmetine gidin. Buradan, birçok özelliklerini yönetebilir.

![Ayarları sayfası](./media/cloud-services-how-to-configure-portal/cloud-service.png)

Merhaba **ayarları** veya **tüm ayarları** bağlantılar hello açılır **ayarları** hello değiştirebileceğiniz dikey **özellikleri**, hello değiştirme **Yapılandırma**, hello yönetmek **sertifikaları**, Kurulum **uyarı kuralları**ve hello yönetmek **kullanıcılar** kimlerin erişimi Bulut hizmeti toothis.

![Azure bulut hizmeti ayarlar dikey penceresi](./media/cloud-services-how-to-configure-portal/cs-settings-blade.png)

### <a name="manage-guest-os-version"></a>Konuk işletim sistemi sürümü yönetme

Varsayılan olarak, Azure konuk işletim sistemi toohello en son desteklenen görüntünüzü Merhaba, hizmet yapılandırma (.cscfg), belirttiğiniz işletim sistemi ailesi içinde düzenli aralıklarla Windows Server 2016 gibi güncelleştirir.

Belirli bir işletim sistemi sürümü tootarget gerekiyorsa, hello ayarlayabilirsiniz **yapılandırma** dikey.

![Küme işletim sistemi sürümü](./media/cloud-services-how-to-configure-portal/cs-settings-config-guestosversion.png)


>[!IMPORTANT]
> Belirli bir işletim sistemi sürümüne otomatik işletim sistemi devre dışı bırakır seçme güncelleştirir ve sizin sorumluluğunuzdadır düzeltme eki uygulama yapar. Rolü örneklerinizi güncelleştirmeleri almakta veya uygulama toosecurity açıkları getirebilir emin olmalısınız.

## <a name="monitoring"></a>İzleme
Uyarıları tooyour bulut hizmeti ekleyebilirsiniz. Tıklatın **ayarları** > **uyarı kuralları** > **uyarı Ekle**.

![](./media/cloud-services-how-to-configure-portal/cs-alerts.png)

Buradan, bir uyarı ayarlayabilirsiniz. Merhaba ile **ölçüm** açılan kutusu, veri türleri aşağıdaki hello için uyarı ayarlayabilirsiniz.

* Disk okuma
* Disk yazma
* Ağ içine
* Ağ dışına
* CPU yüzdesi

![](./media/cloud-services-how-to-configure-portal/cs-alert-item.png)

### <a name="configure-monitoring-from-a-metric-tile"></a>Bir ölçüm kutucuğunda İzlemeyi Yapılandır
Kullanmak yerine **ayarları** > **uyarı kuralları**, ölçüm döşemeleri hello hello birinde tıklayabilirsiniz **izleme** hello bölümünü **bulut Hizmet** dikey.

![Bulut hizmeti izleme](./media/cloud-services-how-to-configure-portal/cs-monitoring.png)

Buradan hello döşeme ile kullanılan hello grafiği özelleştirme veya bir uyarı kuralı ekleyin.

## <a name="reboot-reimage-or-remote-desktop"></a>Yeniden başlatma, yeniden görüntü oluşturma ya da Uzak Masaüstü
Şu anda Uzak Masaüstü'nü hello kullanarak yapılandıramazsınız **Azure portal**. Ancak, bunu hello ayarlayabilirsiniz [Klasik Azure portalı](cloud-services-role-enable-remote-desktop.md), [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md), aracılığıyla veya [Visual Studio](../vs-azure-tools-remote-desktop-roles.md).

İlk olarak, hello bulut hizmeti örneğinde'ı tıklatın.

![Bulut hizmeti örneği](./media/cloud-services-how-to-configure-portal/cs-instance.png)

Açılan dikey Hello Uzak Masaüstü bağlantısı başlatmak, uzaktan hello örneğini veya Uzaktan yeniden görüntü oluşturma (Başlangıç yeni bir görüntü ile) Merhaba örneğini yeniden başlatın.

![Bulut hizmeti örneği düğmeleri](./media/cloud-services-how-to-configure-portal/cs-instance-buttons.png)

## <a name="reconfigure-your-cscfg"></a>.cscfg yeniden yapılandırın
Bulut hizmetinizi hello aracılığıyla tooreconfigure gerekebilir [hizmet yapılandırma (cscfg)](cloud-services-model-and-package.md#cscfg) dosyası. Öncelikle, .cscfg toodownload gerekir dosya, değiştirin ve sonra bunu yükleyin.

1. Tıklatın hello üzerinde **ayarları** simgesini veya hello **tüm ayarları** tooopen hello yukarı bağlantı **ayarları** dikey.

    ![Ayarları sayfası](./media/cloud-services-how-to-configure-portal/cloud-service.png)
2. Tıklatın hello üzerinde **yapılandırma** öğesi.

    ![Yapılandırma dikey penceresi](./media/cloud-services-how-to-configure-portal/cs-settings-config.png)
3. Tıklatın hello üzerinde **karşıdan** düğmesi.

    ![İndir](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-download.png)
4. Hello hizmet yapılandırma dosyası güncelleştirdikten sonra karşıya yükleme ve hello yapılandırma güncelleştirmeleri uygulayın:

    ![Karşıya Yükle](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-upload.png)
5. Merhaba .cscfg dosyasını tıklatıp **Tamam**.

## <a name="next-steps"></a>Sonraki adımlar
* Nasıl çok öğrenin[bir bulut hizmetinin dağıtılacağı](cloud-services-how-to-create-deploy-portal.md).
* Yapılandırma bir [özel etki alanı adı](cloud-services-custom-domain-name-portal.md).
* [Bulut hizmetinizi yönetme](cloud-services-how-to-manage-portal.md).
* Yapılandırma [ssl sertifikalarını](cloud-services-configure-ssl-certificate-portal.md).
