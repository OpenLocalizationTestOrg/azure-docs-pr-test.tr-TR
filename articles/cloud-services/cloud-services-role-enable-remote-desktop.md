---
title: "bir Azure bulut hizmetindeki, Uzak Masaüstü'nü aaaEnable | Microsoft Docs"
description: "Nasıl tooconfigure azure bulut hizmeti uygulama tooallow Uzak Masaüstü bağlantıları"
services: cloud-services
documentationcenter: 
author: thraka
manager: timlt
editor: 
ms.assetid: d3110ee8-6526-4585-aba5-d0bc9a713e9b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: b3c0180bf5ad29cb77e5303ccbd6f9ccc44b7b0a
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

Hizmet tanımında hello Uzak Masaüstü modüller ekleyerek geliştirme sırasında rolde bir Uzak Masaüstü Bağlantısı etkinleştirebilirsiniz veya tooenable Uzak Masaüstü hello Uzak Masaüstü uzantısı aracılığıyla seçebilirsiniz. Uygulamanızı tooredeploy gerek kalmadan Merhaba uygulaması bile dağıtıldıktan sonra Uzak Masaüstü etkinleştirebilirsiniz gibi hello tercih edilen yaklaşım toouse hello Uzak Masaüstü uzantısıdır.

## <a name="configure-remote-desktop-from-hello-azure-classic-portal"></a>Klasik Azure portalı hello Uzak Masaüstü'nü yapılandırma
Merhaba Klasik Azure portalı hello Uzak Masaüstü uzantısı yaklaşımı kullanır, bu nedenle bile hello uygulama dağıtıldıktan sonra Uzak Masaüstü etkinleştirebilirsiniz. Merhaba **yapılandırma** sayfası bulut hizmetiniz için Uzak Masaüstü tooenable sağlar, değişiklik hello yerel yönetici hesabı kullanılan tooconnect toohello sanal makineler, hello sertifika kimlik doğrulamasında kullanılan ve hello ayarlayın sona erme tarihi.

1. Tıklatın **bulut Hizmetleri**hello bulut hizmeti hello adına tıklayın ve ardından **yapılandırma**.
2. Merhaba tıklatın **uzak** hello altındaki düğmesi.

    ![Uzak bulut Hizmetleri](./media/cloud-services-role-enable-remote-desktop/CloudServices_Remote.png)

   > [!WARNING]
   > İlk olarak Uzak Masaüstü'nü etkinleştirin ve (onay işareti) Tamam'ı tıklatın, tüm rol örneklerini yeniden başlatılır. tooprevent yeniden başlatma, hello sertifika kullanılan tooencrypt hello parolası hello rolünün yüklenmesi gerekir. tooprevent bir yeniden başlatma [hello bulut hizmeti için bir sertifika karşıya](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) ve toothis iletişim döndürür.

3. İçinde **rolleri**seçin tooupdate istediğiniz ya da seçin hello rol **tüm** tüm rolleri için.
4. Aşağıdaki değişiklikler hello yapın:

   * Uzak Masaüstü'nü seçin hello tooenable **Uzak Masaüstü'nü etkinleştirme** onay kutusu. Uzak Masaüstü'nü Temizle hello onay kutusunu toodisable.
   * Bir hesap toouse Uzak Masaüstü bağlantılarını toohello rol örneği oluşturun.
   * Merhaba hello mevcut hesap parolasını güncelleştirin.
   * Kimlik doğrulaması için yüklenen sertifikanın toouse seçin (karşıya yükleme hello sertifikayı kullanarak **karşıya** hello üzerinde **sertifikaları** sayfa) veya yeni bir sertifika oluşturun.
   * Merhaba Uzak Masaüstü yapılandırmasının Hello sona erme tarihini değiştirin.

5. Tamamladığınızda, yapılandırmayı güncelleştirmelerinizi tıklatın **Tamam** (onay işareti).

## <a name="remote-into-role-instances"></a>Uzaktan rol örnekleri içine
Uzak Masaüstü hello rollerinde etkinleştirildikten sonra uzak bir rol örneği çeşitli araçları aracılığıyla içine gerçekleştirebilirsiniz.

Merhaba Klasik Azure Portalı'ndan tooconnect tooa rol örneği:

1. Tıklatın **örnekleri** tooopen hello **örnekleri** sayfası.
2. Yapılandırılmış Uzak Masaüstü sahip rol örneği seçin.
3. Tıklatın **Bağlan**ve hello yönergeleri tooopen hello Masaüstü izleyin.
4. Tıklatın **açık** ve ardından **Bağlan** toostart hello Uzak Masaüstü Bağlantısı.

### <a name="use-visual-studio-tooremote-into-a-role-instance"></a>Visual Studio tooremote bir rol örneğine kullanın
Visual Studio'da, Sunucu Gezgini:

1. Merhaba genişletin **Azure** > **bulut Hizmetleri** > **[bulut hizmet adı]** düğümü.
2. Genişletin **hazırlama** veya **üretim**.
3. Merhaba tek rol genişletin.
4. Hello rol örnekleri birine sağ tıklayın, **Uzak Masaüstü kullanarak bağlan...** ve ardından hello kullanıcı adı ve parolayı girin.

![Sunucu Gezgini Uzak Masaüstü](./media/cloud-services-role-enable-remote-desktop/ServerExplorer_RemoteDesktop.png)

### <a name="use-powershell-tooget-hello-rdp-file"></a>PowerShell tooget hello RDP dosyası kullanın
Merhaba kullanabilirsiniz [Get-AzureRemoteDesktopFile](https://msdn.microsoft.com/library/azure/dn495261.aspx) cmdlet tooretrieve hello RDP dosyası. Uzak Masaüstü Bağlantısı tooaccess hello bulut hizmeti ile Merhaba RDP dosyasını kullanabilirsiniz.

### <a name="programmatically-download-hello-rdp-file-through-hello-service-management-rest-api"></a>Program aracılığıyla hello Hizmet Yönetimi REST API'si aracılığıyla hello RDP dosyası indirilemedi
Merhaba kullanabilirsiniz [RDP dosyasını karşıdan](https://msdn.microsoft.com/library/jj157183.aspx) REST işlemi toodownload hello RDP dosyası.

## <a name="tooconfigure-remote-desktop-in-hello-service-definition-file"></a>tooconfigure hello hizmet tanımı dosyasında Uzak Masaüstü
Bu yöntem hello uygulama geliştirme sırasında için Uzak Masaüstü tooenable sağlar. Bu yaklaşım şifrelenmiş parolalar gerektirir saklanmasını Merhaba uygulaması çözümünüzün yeniden dağıtımını hizmeti yapılandırmanızı dosya ve tüm güncelleştirmeleri toohello uzak masaüstü yapılandırması gerektirir. Merhaba Uzak Masaüstü uzantısı kullanması gereken bu downsides yukarıda açıklanan yaklaşım bağlı olarak tooavoid istiyorsanız.  

Visual Studio kullanabileceğine[bir Uzak Masaüstü Bağlantısı etkinleştirmek](../vs-azure-tools-remote-desktop-roles.md) hello hizmet tanımı dosyası yaklaşımı kullanarak.  
Merhaba değişiklikleri gerekli toohello hizmet modeli dosyaları tooenable Uzak Masaüstü Hello adımları açıklanmaktadır. Visual Studio otomatik olarak yapar bu değişiklikleri yayımlarken.

### <a name="set-up-hello-connection-in-hello-service-model"></a>Merhaba hizmet modelinde hello bağlantı kurma
Kullanım hello **içeri aktarmalar** öğesi tooimport hello **RemoteAccess** modülü ve hello **RemoteForwarder** modülü toohello [ServiceDefinition.csdef](cloud-services-model-and-package.md#csdef) dosya.

Merhaba hizmet tanımı dosyası hello örnekle aşağıdaki benzer toohello olmalıdır `<Imports>` öğe eklendi.

```xml
<ServiceDefinition name="<name-of-cloud-service>" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition" schemaVersion="2013-03.2.0">
    <WebRole name="WebRole1" vmsize="Small">
        <Sites>
            <Site name="Web">
                <Bindings>
                    <Binding name="Endpoint1" endpointName="Endpoint1" />
                </Bindings>
            </Site>
        </Sites>
        <Endpoints>
            <InputEndpoint name="Endpoint1" protocol="http" port="80" />
        </Endpoints>
        <Imports>
            <Import moduleName="Diagnostics" />
            <Import moduleName="RemoteAccess" />
            <Import moduleName="RemoteForwarder" />
        </Imports>
    </WebRole>
</ServiceDefinition>
```
Merhaba [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#cscfg) dosya olması aşağıdaki örneğine benzer toohello, Not hello `<ConfigurationSettings>` ve `<Certificates>` öğeleri. Belirtilen sertifika Hello olmalıdır [toohello bulut hizmeti karşıya](cloud-services-how-to-create-deploy.md#how-to-upload-a-certificate-for-a-cloud-service).

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceConfiguration serviceName="<name-of-cloud-service>" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="3" osVersion="*" schemaVersion="2013-03.2.0">
    <Role name="WebRole1">
        <Instances count="2" />
        <ConfigurationSettings>
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.Enabled" value="true" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.AccountUsername" value="[name-of-user-account]" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.AccountEncryptedPassword" value="[base-64-encrypted-user-password]" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.AccountExpiration" value="[certificate-expiration]" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteForwarder.Enabled" value="true" />
        </ConfigurationSettings>
        <Certificates>
            <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption" thumbprint="[certificate-thumbprint]" thumbprintAlgorithm="sha1" />
        </Certificates>
    </Role>
</ServiceConfiguration>
```


## <a name="additional-resources"></a>Ek Kaynaklar
[Nasıl tooConfigure bulut Hizmetleri](cloud-services-how-to-configure.md)
[bulut SSS - Uzak Masaüstü Hizmetleri](cloud-services-faq.md)
