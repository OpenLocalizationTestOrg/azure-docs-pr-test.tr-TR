---
title: "Uzak Masaüstü bağlantısı için Azure bulut Hizmetleri rolünde aaaEnable | Microsoft Docs"
description: "Nasıl tooconfigure azure bulut hizmeti uygulama tooallow Uzak Masaüstü bağlantıları"
services: cloud-services
documentationcenter: 
author: mmccrory
manager: timlt
editor: 
ms.assetid: 73ea1d64-1529-4d72-b58e-f6c10499e6bb
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: mmccrory
ms.openlocfilehash: 55d7043df571c2e88b04aa9ef01dc8ae1d6784f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services"></a>Azure bulut Hizmetleri rolünde için Uzak Masaüstü Bağlantısı etkinleştir
> [!div class="op_single_selector"]
> * [Azure portal](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [Klasik Azure Portalı](cloud-services-role-enable-remote-desktop.md)
> * [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md)
> * [Visual Studio](../vs-azure-tools-remote-desktop-roles.md)
>
>

Uzak Masaüstü tooaccess hello Masaüstü Azure'da çalışan bir rolün sağlar. Çalışırken uygulamanız ile sorunları tanılamak ve Uzak Masaüstü Bağlantısı tootroubleshoot kullanın.

Hizmet tanımında hello Uzak Masaüstü modüller ekleyerek geliştirme sırasında rolde bir Uzak Masaüstü Bağlantısı etkinleştirebilirsiniz veya tooenable Uzak Masaüstü hello Uzak Masaüstü uzantısı aracılığıyla seçebilirsiniz. Uygulamanızı tooredeploy gerek kalmadan Merhaba uygulaması bile dağıtıldıktan sonra Uzak Masaüstü etkinleştirebilirsiniz gibi hello tercih edilen yaklaşım toouse hello Uzak Masaüstü uzantısıdır.

## <a name="configure-remote-desktop-from-hello-azure-portal"></a>Azure portal hello Uzak Masaüstü'nü yapılandırma
hello Azure portal hello Uzak Masaüstü uzantısı yaklaşımı kullanır, bu nedenle bile hello uygulama dağıtıldıktan sonra Uzak Masaüstü etkinleştirebilirsiniz. Merhaba **Uzak Masaüstü** bulut hizmetinizin dikey tooenable Uzak Masaüstü sağlar, değişiklik hello yerel yönetici hesabı kullanılan tooconnect toohello sanal makineler, hello sertifika kimlik doğrulamasında kullanılan ve hello ayarlayın sona erme tarihi.

1. Tıklatın **bulut Hizmetleri**hello bulut hizmeti hello adına tıklayın ve ardından **Uzak Masaüstü**.

    ![Bulut Hizmetleri Uzak Masaüstü](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop.png)

2. Uzak Masaüstü tooenable tüm rolleri veya tek bir rol için istediğiniz sonra hello değiştirici hello değerini çok değiştirme olup olmadığını seçin**etkin**.

3. Kullanıcı adı, parola, süre sonu ve sertifika hello gerekli alanları doldurun.

    ![Bulut Hizmetleri Uzak Masaüstü](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Details.png)

   > [!WARNING]
   > İlk olarak Uzak Masaüstü'nü etkinleştirin ve (onay işareti) Tamam'ı tıklatın, tüm rol örneklerini yeniden başlatılır. tooprevent yeniden başlatma, hello sertifika kullanılan tooencrypt hello parolası hello rolünün yüklenmesi gerekir. tooprevent bir yeniden başlatma [hello bulut hizmeti için bir sertifika karşıya](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) ve toothis iletişim döndürür.
   >
   >
3. İçinde **rolleri**seçin tooupdate istediğiniz ya da seçin hello rol **tüm** tüm rolleri için.

4. Tamamladığınızda, yapılandırmayı güncelleştirmelerinizi tıklatın **kaydetmek**. Rolü örneklerinizi hazır tooreceive bağlantıları önce birkaç dakika sürebilir.

## <a name="remote-into-role-instances"></a>Uzaktan rol örnekleri içine
Uzak Masaüstü hello rollerinde etkinleştirildikten sonra bir bağlantıdan doğrudan hello Azure Portal başlatabilirsiniz:

1. Tıklatın **örnekleri** tooopen hello **örnekleri** dikey.
2. Yapılandırılmış Uzak Masaüstü sahip rol örneği seçin.
3. Tıklatın **Bağlan** toodownload bir RDP dosyası hello rol örneği için.

    ![Bulut Hizmetleri Uzak Masaüstü](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Connect.png)

4. Tıklatın **açık** ve ardından **Bağlan** toostart hello Uzak Masaüstü Bağlantısı.

>[!NOTE]
> Bulut hizmetiniz bir NSG durduğunu değilse, bağlantı noktalarında trafiğine izin veren toocreate kuralları gerekebilir **3389** ve **20000**.  Uzak Masaüstü bağlantı noktasını kullanır **3389**.  Bulut hizmeti örnekleri yükü dengelenmiş, olduğundan, hangi örneğinin tooconnect doğrudan denetleyemezsiniz.  Merhaba *RemoteForwarder* ve *RemoteAccess* aracıları RDP trafiği yönetmek ve hello istemci toosend bir RDP izin ver ve bir tek tek örnek tooconnect belirtin.  Merhaba *RemoteForwarder* ve *RemoteAccess* aracıları gerektiren bu bağlantı noktasını **20000*** açılıp, hangi engellenmiş olabilir bir NSG varsa.

## <a name="additional-resources"></a>Ek kaynaklar

[Nasıl tooConfigure bulut Hizmetleri](cloud-services-how-to-configure.md)
[bulut SSS - Uzak Masaüstü Hizmetleri](cloud-services-faq.md)
