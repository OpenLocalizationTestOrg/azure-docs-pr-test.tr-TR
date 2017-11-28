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
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services"></a><span data-ttu-id="c61db-103">Azure bulut Hizmetleri rolünde için Uzak Masaüstü Bağlantısı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="c61db-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c61db-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="c61db-104">Azure portal</span></span>](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [<span data-ttu-id="c61db-105">Klasik Azure Portalı</span><span class="sxs-lookup"><span data-stu-id="c61db-105">Azure classic portal</span></span>](cloud-services-role-enable-remote-desktop.md)
> * [<span data-ttu-id="c61db-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c61db-106">PowerShell</span></span>](cloud-services-role-enable-remote-desktop-powershell.md)
> * [<span data-ttu-id="c61db-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c61db-107">Visual Studio</span></span>](../vs-azure-tools-remote-desktop-roles.md)

<span data-ttu-id="c61db-108">Hizmet tanımında hello Uzak Masaüstü modüller ekleyerek geliştirme sırasında rolde bir Uzak Masaüstü Bağlantısı etkinleştirebilirsiniz veya tooenable Uzak Masaüstü hello Uzak Masaüstü uzantısı aracılığıyla seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c61db-108">You can enable a Remote Desktop connection in your role during development by including hello Remote Desktop modules in your service definition or you can choose tooenable Remote Desktop through hello Remote Desktop Extension.</span></span> <span data-ttu-id="c61db-109">Uygulamanızı tooredeploy gerek kalmadan Merhaba uygulaması bile dağıtıldıktan sonra Uzak Masaüstü etkinleştirebilirsiniz gibi hello tercih edilen yaklaşım toouse hello Uzak Masaüstü uzantısıdır.</span><span class="sxs-lookup"><span data-stu-id="c61db-109">hello preferred approach is toouse hello Remote Desktop extension as you can enable Remote Desktop even after hello application is deployed without having tooredeploy your application.</span></span>

## <a name="configure-remote-desktop-from-hello-azure-classic-portal"></a><span data-ttu-id="c61db-110">Klasik Azure portalı hello Uzak Masaüstü'nü yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c61db-110">Configure Remote Desktop from hello Azure classic portal</span></span>
<span data-ttu-id="c61db-111">Merhaba Klasik Azure portalı hello Uzak Masaüstü uzantısı yaklaşımı kullanır, bu nedenle bile hello uygulama dağıtıldıktan sonra Uzak Masaüstü etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c61db-111">hello Azure classic portal uses hello Remote Desktop Extension approach so you can enable Remote Desktop even after hello application is deployed.</span></span> <span data-ttu-id="c61db-112">Merhaba **yapılandırma** sayfası bulut hizmetiniz için Uzak Masaüstü tooenable sağlar, değişiklik hello yerel yönetici hesabı kullanılan tooconnect toohello sanal makineler, hello sertifika kimlik doğrulamasında kullanılan ve hello ayarlayın sona erme tarihi.</span><span class="sxs-lookup"><span data-stu-id="c61db-112">hello **Configure** page for your cloud service allows you tooenable Remote Desktop, change hello local Administrator account used tooconnect toohello virtual machines, hello certificate used in authentication and set hello expiration date.</span></span>

1. <span data-ttu-id="c61db-113">Tıklatın **bulut Hizmetleri**hello bulut hizmeti hello adına tıklayın ve ardından **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="c61db-113">Click **Cloud Services**, click hello name of hello cloud service, and then click **Configure**.</span></span>
2. <span data-ttu-id="c61db-114">Merhaba tıklatın **uzak** hello altındaki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c61db-114">Click hello **Remote** button at hello bottom.</span></span>

    ![Uzak bulut Hizmetleri](./media/cloud-services-role-enable-remote-desktop/CloudServices_Remote.png)

   > [!WARNING]
   > <span data-ttu-id="c61db-116">İlk olarak Uzak Masaüstü'nü etkinleştirin ve (onay işareti) Tamam'ı tıklatın, tüm rol örneklerini yeniden başlatılır.</span><span class="sxs-lookup"><span data-stu-id="c61db-116">All role instances will be restarted when you first enable Remote Desktop and click OK (checkmark).</span></span> <span data-ttu-id="c61db-117">tooprevent yeniden başlatma, hello sertifika kullanılan tooencrypt hello parolası hello rolünün yüklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="c61db-117">tooprevent a reboot, hello certificate used tooencrypt hello password must be installed on hello role.</span></span> <span data-ttu-id="c61db-118">tooprevent bir yeniden başlatma [hello bulut hizmeti için bir sertifika karşıya](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) ve toothis iletişim döndürür.</span><span class="sxs-lookup"><span data-stu-id="c61db-118">tooprevent a restart, [upload a certificate for hello cloud service](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) and then return toothis dialog.</span></span>

3. <span data-ttu-id="c61db-119">İçinde **rolleri**seçin tooupdate istediğiniz ya da seçin hello rol **tüm** tüm rolleri için.</span><span class="sxs-lookup"><span data-stu-id="c61db-119">In **Roles**, select hello role you want tooupdate or select **All** for all roles.</span></span>
4. <span data-ttu-id="c61db-120">Aşağıdaki değişiklikler hello yapın:</span><span class="sxs-lookup"><span data-stu-id="c61db-120">Make any of hello following changes:</span></span>

   * <span data-ttu-id="c61db-121">Uzak Masaüstü'nü seçin hello tooenable **Uzak Masaüstü'nü etkinleştirme** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="c61db-121">tooenable Remote Desktop, select hello **Enable Remote Desktop** check box.</span></span> <span data-ttu-id="c61db-122">Uzak Masaüstü'nü Temizle hello onay kutusunu toodisable.</span><span class="sxs-lookup"><span data-stu-id="c61db-122">toodisable Remote Desktop, clear hello check box.</span></span>
   * <span data-ttu-id="c61db-123">Bir hesap toouse Uzak Masaüstü bağlantılarını toohello rol örneği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c61db-123">Create an account toouse in Remote Desktop connections toohello role instances.</span></span>
   * <span data-ttu-id="c61db-124">Merhaba hello mevcut hesap parolasını güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="c61db-124">Update hello password for hello existing account.</span></span>
   * <span data-ttu-id="c61db-125">Kimlik doğrulaması için yüklenen sertifikanın toouse seçin (karşıya yükleme hello sertifikayı kullanarak **karşıya** hello üzerinde **sertifikaları** sayfa) veya yeni bir sertifika oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c61db-125">Select an uploaded certificate toouse for authentication (upload hello certificate using **Upload** on hello **Certificates** page) or create a new certificate.</span></span>
   * <span data-ttu-id="c61db-126">Merhaba Uzak Masaüstü yapılandırmasının Hello sona erme tarihini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="c61db-126">Change hello expiration date for hello Remote Desktop configuration.</span></span>

5. <span data-ttu-id="c61db-127">Tamamladığınızda, yapılandırmayı güncelleştirmelerinizi tıklatın **Tamam** (onay işareti).</span><span class="sxs-lookup"><span data-stu-id="c61db-127">When you finish your configuration updates, click **OK** (checkmark).</span></span>

## <a name="remote-into-role-instances"></a><span data-ttu-id="c61db-128">Uzaktan rol örnekleri içine</span><span class="sxs-lookup"><span data-stu-id="c61db-128">Remote into role instances</span></span>
<span data-ttu-id="c61db-129">Uzak Masaüstü hello rollerinde etkinleştirildikten sonra uzak bir rol örneği çeşitli araçları aracılığıyla içine gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c61db-129">Once Remote Desktop is enabled on hello roles you can remote into a role instance through various tools.</span></span>

<span data-ttu-id="c61db-130">Merhaba Klasik Azure Portalı'ndan tooconnect tooa rol örneği:</span><span class="sxs-lookup"><span data-stu-id="c61db-130">tooconnect tooa role instance from hello Azure classic portal:</span></span>

1. <span data-ttu-id="c61db-131">Tıklatın **örnekleri** tooopen hello **örnekleri** sayfası.</span><span class="sxs-lookup"><span data-stu-id="c61db-131">Click **Instances** tooopen hello **Instances** page.</span></span>
2. <span data-ttu-id="c61db-132">Yapılandırılmış Uzak Masaüstü sahip rol örneği seçin.</span><span class="sxs-lookup"><span data-stu-id="c61db-132">Select a role instance that has Remote Desktop configured.</span></span>
3. <span data-ttu-id="c61db-133">Tıklatın **Bağlan**ve hello yönergeleri tooopen hello Masaüstü izleyin.</span><span class="sxs-lookup"><span data-stu-id="c61db-133">Click **Connect**, and follow hello instructions tooopen hello desktop.</span></span>
4. <span data-ttu-id="c61db-134">Tıklatın **açık** ve ardından **Bağlan** toostart hello Uzak Masaüstü Bağlantısı.</span><span class="sxs-lookup"><span data-stu-id="c61db-134">Click **Open** and then **Connect** toostart hello Remote Desktop connection.</span></span>

### <a name="use-visual-studio-tooremote-into-a-role-instance"></a><span data-ttu-id="c61db-135">Visual Studio tooremote bir rol örneğine kullanın</span><span class="sxs-lookup"><span data-stu-id="c61db-135">Use Visual Studio tooremote into a role instance</span></span>
<span data-ttu-id="c61db-136">Visual Studio'da, Sunucu Gezgini:</span><span class="sxs-lookup"><span data-stu-id="c61db-136">In Visual Studio, Server Explorer:</span></span>

1. <span data-ttu-id="c61db-137">Merhaba genişletin **Azure** > **bulut Hizmetleri** > **[bulut hizmet adı]** düğümü.</span><span class="sxs-lookup"><span data-stu-id="c61db-137">Expand hello **Azure** > **Cloud Services** > **[cloud service name]** node.</span></span>
2. <span data-ttu-id="c61db-138">Genişletin **hazırlama** veya **üretim**.</span><span class="sxs-lookup"><span data-stu-id="c61db-138">Expand either **Staging** or **Production**.</span></span>
3. <span data-ttu-id="c61db-139">Merhaba tek rol genişletin.</span><span class="sxs-lookup"><span data-stu-id="c61db-139">Expand hello individual role.</span></span>
4. <span data-ttu-id="c61db-140">Hello rol örnekleri birine sağ tıklayın, **Uzak Masaüstü kullanarak bağlan...** ve ardından hello kullanıcı adı ve parolayı girin.</span><span class="sxs-lookup"><span data-stu-id="c61db-140">Right-click one of hello role instances, click **Connect using Remote Desktop...**, and then enter hello user name and password.</span></span>

![Sunucu Gezgini Uzak Masaüstü](./media/cloud-services-role-enable-remote-desktop/ServerExplorer_RemoteDesktop.png)

### <a name="use-powershell-tooget-hello-rdp-file"></a><span data-ttu-id="c61db-142">PowerShell tooget hello RDP dosyası kullanın</span><span class="sxs-lookup"><span data-stu-id="c61db-142">Use PowerShell tooget hello RDP file</span></span>
<span data-ttu-id="c61db-143">Merhaba kullanabilirsiniz [Get-AzureRemoteDesktopFile](https://msdn.microsoft.com/library/azure/dn495261.aspx) cmdlet tooretrieve hello RDP dosyası.</span><span class="sxs-lookup"><span data-stu-id="c61db-143">You can use hello [Get-AzureRemoteDesktopFile](https://msdn.microsoft.com/library/azure/dn495261.aspx) cmdlet tooretrieve hello RDP file.</span></span> <span data-ttu-id="c61db-144">Uzak Masaüstü Bağlantısı tooaccess hello bulut hizmeti ile Merhaba RDP dosyasını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c61db-144">You can then use hello RDP file with Remote Desktop Connection tooaccess hello cloud service.</span></span>

### <a name="programmatically-download-hello-rdp-file-through-hello-service-management-rest-api"></a><span data-ttu-id="c61db-145">Program aracılığıyla hello Hizmet Yönetimi REST API'si aracılığıyla hello RDP dosyası indirilemedi</span><span class="sxs-lookup"><span data-stu-id="c61db-145">Programmatically download hello RDP file through hello Service Management REST API</span></span>
<span data-ttu-id="c61db-146">Merhaba kullanabilirsiniz [RDP dosyasını karşıdan](https://msdn.microsoft.com/library/jj157183.aspx) REST işlemi toodownload hello RDP dosyası.</span><span class="sxs-lookup"><span data-stu-id="c61db-146">You can use hello [Download RDP File](https://msdn.microsoft.com/library/jj157183.aspx) REST operation toodownload hello RDP file.</span></span>

## <a name="tooconfigure-remote-desktop-in-hello-service-definition-file"></a><span data-ttu-id="c61db-147">tooconfigure hello hizmet tanımı dosyasında Uzak Masaüstü</span><span class="sxs-lookup"><span data-stu-id="c61db-147">tooconfigure Remote Desktop in hello service definition file</span></span>
<span data-ttu-id="c61db-148">Bu yöntem hello uygulama geliştirme sırasında için Uzak Masaüstü tooenable sağlar.</span><span class="sxs-lookup"><span data-stu-id="c61db-148">This method allows you tooenable Remote Desktop for hello application during development.</span></span> <span data-ttu-id="c61db-149">Bu yaklaşım şifrelenmiş parolalar gerektirir saklanmasını Merhaba uygulaması çözümünüzün yeniden dağıtımını hizmeti yapılandırmanızı dosya ve tüm güncelleştirmeleri toohello uzak masaüstü yapılandırması gerektirir.</span><span class="sxs-lookup"><span data-stu-id="c61db-149">This approach requires encrypted passwords be stored in your service configuration file and any updates toohello remote desktop configuration would require a redeployment of hello application.</span></span> <span data-ttu-id="c61db-150">Merhaba Uzak Masaüstü uzantısı kullanması gereken bu downsides yukarıda açıklanan yaklaşım bağlı olarak tooavoid istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="c61db-150">If you want tooavoid these downsides you should use hello remote desktop extension based approach described above.</span></span>  

<span data-ttu-id="c61db-151">Visual Studio kullanabileceğine[bir Uzak Masaüstü Bağlantısı etkinleştirmek](../vs-azure-tools-remote-desktop-roles.md) hello hizmet tanımı dosyası yaklaşımı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="c61db-151">You can use Visual Studio too[enable a remote desktop connection](../vs-azure-tools-remote-desktop-roles.md) using hello service definition file approach.</span></span>  
<span data-ttu-id="c61db-152">Merhaba değişiklikleri gerekli toohello hizmet modeli dosyaları tooenable Uzak Masaüstü Hello adımları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="c61db-152">hello steps below describe hello changes needed toohello service model files tooenable remote desktop.</span></span> <span data-ttu-id="c61db-153">Visual Studio otomatik olarak yapar bu değişiklikleri yayımlarken.</span><span class="sxs-lookup"><span data-stu-id="c61db-153">Visual Studio will automatically makes these changes when publishing.</span></span>

### <a name="set-up-hello-connection-in-hello-service-model"></a><span data-ttu-id="c61db-154">Merhaba hizmet modelinde hello bağlantı kurma</span><span class="sxs-lookup"><span data-stu-id="c61db-154">Set up hello connection in hello service model</span></span>
<span data-ttu-id="c61db-155">Kullanım hello **içeri aktarmalar** öğesi tooimport hello **RemoteAccess** modülü ve hello **RemoteForwarder** modülü toohello [ServiceDefinition.csdef](cloud-services-model-and-package.md#csdef) dosya.</span><span class="sxs-lookup"><span data-stu-id="c61db-155">Use hello **Imports** element tooimport hello **RemoteAccess** module and hello **RemoteForwarder** module toohello [ServiceDefinition.csdef](cloud-services-model-and-package.md#csdef) file.</span></span>

<span data-ttu-id="c61db-156">Merhaba hizmet tanımı dosyası hello örnekle aşağıdaki benzer toohello olmalıdır `<Imports>` öğe eklendi.</span><span class="sxs-lookup"><span data-stu-id="c61db-156">hello service definition file should be similar toohello following example with hello `<Imports>` element added.</span></span>

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
<span data-ttu-id="c61db-157">Merhaba [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#cscfg) dosya olması aşağıdaki örneğine benzer toohello, Not hello `<ConfigurationSettings>` ve `<Certificates>` öğeleri.</span><span class="sxs-lookup"><span data-stu-id="c61db-157">hello [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#cscfg) file should be similar toohello following example, note hello `<ConfigurationSettings>` and `<Certificates>` elements.</span></span> <span data-ttu-id="c61db-158">Belirtilen sertifika Hello olmalıdır [toohello bulut hizmeti karşıya](cloud-services-how-to-create-deploy.md#how-to-upload-a-certificate-for-a-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="c61db-158">hello Certificate specified must be [uploaded toohello cloud service](cloud-services-how-to-create-deploy.md#how-to-upload-a-certificate-for-a-cloud-service).</span></span>

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


## <a name="additional-resources"></a><span data-ttu-id="c61db-159">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="c61db-159">Additional Resources</span></span>
<span data-ttu-id="c61db-160">[Nasıl tooConfigure bulut Hizmetleri](cloud-services-how-to-configure.md)
[bulut SSS - Uzak Masaüstü Hizmetleri](cloud-services-faq.md)</span><span class="sxs-lookup"><span data-stu-id="c61db-160">[How tooConfigure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md)</span></span>
