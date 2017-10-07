---
title: aaaHow tooconfigure bir bulut hizmeti (Klasik portal) | Microsoft Docs
description: "Tooconfigure bulut Azure hizmetleri nasıl öğrenin. Uzaktan erişim toorole örnekleri yapılandırmak ve tooupdate hello bulut hizmeti yapılandırması öğrenin."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 4902f79d-ea91-41ca-89a4-7c818180ee5f
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 1ea2320f97f667153f7984e4d61d373a6344cf6d
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

Merhaba Klasik Azure portalında bir bulut hizmeti için en yaygın olarak kullanılan hello ayarlarını yapılandırabilirsiniz. Veya tooupdate isterseniz yapılandırma dosyalarını doğrudan bir hizmet yapılandırma dosyası tooupdate indirin ve güncelleştirilmiş hello dosya ve güncelleştirme hello bulut hizmetiyle hello yapılandırma değişiklikleri karşıya yükleyin. Her iki durumda da hello yapılandırma güncelleştirmeleri tooall rol örnekleri atılır.

Merhaba Klasik Azure portalı de çok tanır[bir rolde Azure bulut Hizmetleri için Uzak Masaüstü Bağlantısı etkinleştir](cloud-services-role-enable-remote-desktop.md)

Her rol için en az iki rol örneği varsa, azure yalnızca 99,95 yüzde hizmet kullanılabilirliği hello sırasında yapılandırma güncelleştirmeleri emin olabilirsiniz. Merhaba diğer güncelleştirilirken, bir sanal makine tooprocess istemci isteklerini etkinleştirir. Daha fazla bilgi için bkz: [hizmet düzeyi sözleşmeleri](https://azure.microsoft.com/support/legal/sla/).

## <a name="change-a-cloud-service"></a>Bir bulut hizmeti değiştirme
1. Merhaba, [Klasik Azure portalı](http://manage.windowsazure.com/), tıklatın **bulut Hizmetleri**hello bulut hizmeti hello adına tıklayın ve ardından **yapılandırma**.
   
    ![Yapılandırma sayfası](./media/cloud-services-how-to-configure/CloudServices_ConfigurePage1.png)
   
    Merhaba üzerinde **yapılandırma** sayfasında, izleme, güncelleştirme rol ayarlarını yapılandırmak ve hello konuk işletim sistemi ve rol örnekleri için ailesi seçin. 
2. İçinde **izleme**, düzey tooVerbose izleme kümesi hello veya en az ve ayrıntılı izleme için gerekli olan hello tanılama bağlantı dizelerini yapılandırın.
3. (Role göre gruplandırılmış) hizmeti roller için ayarlar aşağıdaki hello güncelleştirebilirsiniz:
   
    * **Ayarları** hello belirtilen çeşitli yapılandırma ayarlarının hello değerleri değiştirmek *ConfigurationSettings* öğeleri hello hizmetin yapılandırma (.cscfg) dosyası.

    * **Sertifikalar**  
        Bir rol için kullanılan SSL şifreleme hello sertifika parmak izi değiştirin. bir sertifika toochange hello yeni sertifika ilk karşıya gerekir (Merhaba üzerinde **sertifikaları** sayfası). Ardından hello parmak izi hello rol ayarlarında görüntülendiği hello sertifika dizesinde güncelleştirin.
4. İçinde **işletim sistemi**, hello işletim sistemi ailesi veya rol örnekleri için sürüm değiştirme veya seçme **otomatik** tooenable otomatik güncelleştirmeler hello geçerli işletim sistemi sürümü. Merhaba işletim sistemi ayarlarını tooweb rolleri ve çalışan rolleri geçerlidir, ancak sanal makineleri etkilemez.
   
    Dağıtım işlemi sırasında tüm rol örneklerinde hello en son işletim sistemi sürümü yüklenir ve hello işletim sistemleri, varsayılan olarak otomatik olarak güncelleştirilir. 
   
    Farklı işletim sistemi sürümünü, bulut hizmeti toorun uyumluluk gereksinimleri nedeniyle, kodunuzda ihtiyacınız varsa, bir işletim sistemi ailesi ve sürümü seçebilirsiniz. Belirli işletim sistemi sürümü seçtiğinizde hello bulut hizmeti için otomatik işletim sistemi güncelleştirmelerini askıya alınır. Tooensure gerekir hello işletim sistemi güncelleştirmeleri alırsınız.
   
    Uygulamalarınızı hello en son işletim sistemi sürümü ile yüklü tüm uyumluluk sorunları gidermek, otomatik işletim sistemi güncelleştirmelerini ayarı hello işletim sistemi sürümüne göre çok etkinleştirebilirsiniz**otomatik**. 
   
    ![İşletim sistemi ayarları](./media/cloud-services-how-to-configure/CloudServices_ConfigurePage_OSSettings.png)
5. toosave yapılandırma ayarlarınızı ve bunları toohello rol örnekleri gönderme, tıklatın **kaydetmek**. (Tıklatın **atmak** toocancel hello değişiklikleri.) **Kaydet** ve **atmak** bir ayarı değiştirdikten sonra toohello komut çubuğu eklenir.

## <a name="update-a-cloud-service-configuration-file"></a>Bir bulut hizmeti yapılandırma dosyasını güncelleştir
1. Merhaba yapılandırmasına bir bulut hizmet yapılandırma dosyası (.cscfg) indirin. Merhaba üzerinde **yapılandırma** sayfasında hello bulut hizmeti için **karşıdan**. Ardından **kaydetmek**, veya **Kaydet** toosave hello dosya.
2. Hello hizmet yapılandırma dosyası güncelleştirdikten sonra karşıya yükleme ve hello yapılandırma güncelleştirmeleri uygulayın:
   
   1. Merhaba üzerinde **yapılandırma** sayfasında, **karşıya**.
      
       ![Yapılandırma karşıya yükle](./media/cloud-services-how-to-configure/CloudServices_UploadConfigFile.png)
   2. İçinde **yapılandırma dosyası**, kullanın **Gözat** tooselect hello .cscfg dosyası güncelleştirildi.
   3. Bulut hizmetinizi yalnızca bir örneğine sahip herhangi bir rol içeriyorsa, hello seçin **bir veya daha fazla rol tek bir örnek içeriyor olsa bile yapılandırma uygulamak** hello rolleri tooproceed için onay kutusunu tooenable hello yapılandırma güncelleştirmeleri.
      
       Her rolün en az iki örneğinin tanımlamadığınız sürece Azure en az 99,95 yüzde garanti edemez, bulut hizmeti kullanılabilirlik hizmet yapılandırma güncelleştirmeleri sırasında. Daha fazla bilgi için bkz: [hizmet düzeyi sözleşmeleri](https://azure.microsoft.com/support/legal/sla/).
   4. Tıklatın **Tamam** (onay işareti). 

## <a name="next-steps"></a>Sonraki adımlar
* Nasıl çok öğrenin[bir bulut hizmetinin dağıtılacağı](cloud-services-how-to-create-deploy.md).
* Yapılandırma bir [özel etki alanı adı](cloud-services-custom-domain-name.md).
* [Bulut hizmetinizi yönetme](cloud-services-how-to-manage.md).
* [Azure bulut Hizmetleri rolünde için Uzak Masaüstü Bağlantısı etkinleştir](cloud-services-role-enable-remote-desktop.md)
* Yapılandırma [ssl sertifikalarını](cloud-services-configure-ssl-certificate.md).

