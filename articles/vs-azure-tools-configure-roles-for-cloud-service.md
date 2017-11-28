---
title: "aaaConfigure hello rolleri bir Azure için bulut hizmeti Visual Studio ile | Microsoft Docs"
description: "Bilgi nasıl tooset ayarlama ve rolleri Visual Studio kullanarak Azure bulut Hizmetleri için yapılandırın."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: d397ef87-64e5-401a-aad5-7f83f1022e16
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: d3c62eb57040ebe987787e73b17b468bb82122bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-cloud-service-roles-with-visual-studio"></a><span data-ttu-id="6b6c4-103">Azure bulut hizmeti rollerinizi ile Visual Studio'yu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="6b6c4-103">Configure Azure cloud service roles with Visual Studio</span></span>
<span data-ttu-id="6b6c4-104">Bir Azure bulut hizmeti bir veya daha fazla çalışan ya da web rolleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-104">An Azure cloud service can have one or more worker or web roles.</span></span> <span data-ttu-id="6b6c4-105">Her rol için bu rol nasıl ayarlanacağını toodefine gerekir ve ayrıca bu rolü nasıl çalışacağını yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-105">For each role, you need toodefine how that role is set up and also configure how that role runs.</span></span> <span data-ttu-id="6b6c4-106">Bulut Hizmetleri rolleri hakkında daha fazla toolearn bkz hello video [giriş tooAzure bulut Hizmetleri](https://channel9.msdn.com/Series/Windows-Azure-Cloud-Services-Tutorials/Introduction-to-Windows-Azure-Cloud-Services).</span><span class="sxs-lookup"><span data-stu-id="6b6c4-106">toolearn more about roles in cloud services, see hello video [Introduction tooAzure Cloud Services](https://channel9.msdn.com/Series/Windows-Azure-Cloud-Services-Tutorials/Introduction-to-Windows-Azure-Cloud-Services).</span></span> 

<span data-ttu-id="6b6c4-107">Merhaba bilgileri bulut hizmetiniz için aşağıdaki dosyaları hello depolanır:</span><span class="sxs-lookup"><span data-stu-id="6b6c4-107">hello information for your cloud service is stored in hello following files:</span></span>

- <span data-ttu-id="6b6c4-108">**ServiceDefinition.csdef** -hello hizmet tanımı dosyası Bulut hizmeti hangi rollerin gerekli dahil olmak üzere, uç noktaları ve sanal makine boyutu hello çalışma zamanı ayarlarını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-108">**ServiceDefinition.csdef** - hello service definition file defines hello runtime settings for your cloud service including what roles are required, endpoints, and virtual machine size.</span></span> <span data-ttu-id="6b6c4-109">Depolanan hello veri hiçbiri `ServiceDefinition.csdef` rolünüze çalıştırırken değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-109">None of hello data stored in `ServiceDefinition.csdef` can be changed when your role is running.</span></span>
- <span data-ttu-id="6b6c4-110">**ServiceConfiguration.cscfg** - hello hizmet yapılandırma dosyası yapılandırır kaç bir rolün örnekleri çalıştırmak ve hello ayarlarının hello değerleri bir rol için tanımlanan.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-110">**ServiceConfiguration.cscfg** - hello service configuration file configures how many instances of a role are run and hello values of hello settings defined for a role.</span></span> <span data-ttu-id="6b6c4-111">Merhaba depolanan verileri `ServiceConfiguration.cscfg` rolünüze çalışırken değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-111">hello data stored in `ServiceConfiguration.cscfg` can be changed while your role is running.</span></span>

<span data-ttu-id="6b6c4-112">bir rolü nasıl çalışacağını denetleyen hello ayarlarını toostore farklı değerleri, birden çok hizmet yapılandırması tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-112">toostore different values for hello settings that control how a role runs, you can define multiple service configurations.</span></span> <span data-ttu-id="6b6c4-113">Her dağıtım ortamı için farklı hizmet yapılandırması kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-113">You can use a different service configuration for each deployment environment.</span></span> <span data-ttu-id="6b6c4-114">Örneğin, bir yerel hizmet yapılandırma, depolama hesabı bağlantı dizesi toouse hello yerel Azure storage öykünücüsü belirleyebilir ve başka bir hizmet yapılandırması toouse Azure depolama hello bulutta oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-114">For example, you can set your storage account connection string toouse hello local Azure storage emulator in a local service configuration and create another service configuration toouse Azure storage in hello cloud.</span></span>

<span data-ttu-id="6b6c4-115">Visual Studio'da bir Azure bulut hizmeti oluşturduğunuzda, iki hizmet yapılandırması otomatik olarak oluşturulur ve tooyour Azure projesi eklenir:</span><span class="sxs-lookup"><span data-stu-id="6b6c4-115">When you create an Azure cloud service in Visual Studio, two service configurations are automatically created and added tooyour Azure project:</span></span>

- `ServiceConfiguration.Cloud.cscfg`
- `ServiceConfiguration.Local.cscfg`

## <a name="configure-an-azure-cloud-service"></a><span data-ttu-id="6b6c4-116">Bir Azure bulut hizmeti yapılandırın</span><span class="sxs-lookup"><span data-stu-id="6b6c4-116">Configure an Azure cloud service</span></span>
<span data-ttu-id="6b6c4-117">Visual Studio'da Çözüm Gezgini'nden bir Azure bulut hizmeti aşağıdaki adımları hello gösterildiği gibi yapılandırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6b6c4-117">You can configure an Azure cloud service from Solution Explorer in Visual Studio, as shown in hello following steps:</span></span>

1. <span data-ttu-id="6b6c4-118">Oluşturun veya bir Azure bulut hizmeti projesini Visual Studio'da açın.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-118">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="6b6c4-119">İçinde **Çözüm Gezgini**hello projesine sağ tıklayın ve, hello bağlam menüsünden seçin **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-119">In **Solution Explorer**, right-click hello project, and, from hello context menu, select **Properties**.</span></span>
   
    ![Çözüm Gezgini proje bağlam menüsü](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-project-context-menu.png)

1. <span data-ttu-id="6b6c4-121">Merhaba Hello projenin Özellikler sayfasında, seçin **geliştirme** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-121">In hello project's properties page, select hello **Development** tab.</span></span> 

    ![Proje Özellikleri sayfası - geliştirme sekmesi](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-development-tab.png)

1. <span data-ttu-id="6b6c4-123">Merhaba, **hizmet yapılandırmasını** listesi, tooedit istediğiniz hello hizmet yapılandırmasının select hello adı.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-123">In hello **Service Configuration** list, select hello name of hello service configuration that you want tooedit.</span></span> <span data-ttu-id="6b6c4-124">(Toomake tooall hello hizmet yapılandırması bu rol için değişiklikler istiyorsanız seçin **tüm yapılandırmaları**.)</span><span class="sxs-lookup"><span data-stu-id="6b6c4-124">(If you want toomake changes tooall hello service configurations for this role, select **All Configurations**.)</span></span>
   
    > [!IMPORTANT]
    > <span data-ttu-id="6b6c4-125">Belirli hizmet yapılandırmasını seçerseniz, tüm yapılandırmalar için yalnızca ayarlanamadığı için bazı özellikler devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-125">If you choose a specific service configuration, some properties are disabled because they can only be set for all configurations.</span></span> <span data-ttu-id="6b6c4-126">tooedit seçmeniz gerekir, bu özellikler **tüm yapılandırmaları**.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-126">tooedit these properties, you must select **All Configurations**.</span></span>
    > 
    > 
   
    ![Bir Azure bulut hizmeti için hizmet yapılandırmasını listesi](./media/vs-azure-tools-configure-roles-for-cloud-service/cloud-service-service-configuration-property.png)

## <a name="change-hello-number-of-role-instances"></a><span data-ttu-id="6b6c4-128">Merhaba rol örneklerinin sayısını değiştirme</span><span class="sxs-lookup"><span data-stu-id="6b6c4-128">Change hello number of role instances</span></span>
<span data-ttu-id="6b6c4-129">tooimprove hello performansını bulut hizmetinizin Merhaba, kullanıcılar ya da belirli bir rol için beklenen hello yük hello sayısına dayalı olarak çalıştırılan bir rol örneklerinin sayısını değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-129">tooimprove hello performance of your cloud service, you can change hello number of instances of a role that are running, based on hello number of users or hello load expected for a particular role.</span></span> <span data-ttu-id="6b6c4-130">Merhaba bulut hizmeti Azure içinde çalıştığında ayrı bir sanal makine rol her örneği için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-130">A separate virtual machine is created for each instance of a role when hello cloud service runs in Azure.</span></span> <span data-ttu-id="6b6c4-131">Bu bulut hizmeti dağıtımının hello hello faturalama etkiler.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-131">This affects hello billing for hello deployment of this cloud service.</span></span> <span data-ttu-id="6b6c4-132">Faturalama hakkında daha fazla bilgi için bkz: [faturanızı anlamak için Microsoft Azure](billing/billing-understand-your-bill.md).</span><span class="sxs-lookup"><span data-stu-id="6b6c4-132">For more information about billing, see [Understand your bill for Microsoft Azure](billing/billing-understand-your-bill.md).</span></span>

1. <span data-ttu-id="6b6c4-133">Oluşturun veya bir Azure bulut hizmeti projesini Visual Studio'da açın.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-133">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="6b6c4-134">İçinde **Çözüm Gezgini**, başlangıç projesi düğümünü genişletin.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-134">In **Solution Explorer**, expand hello project node.</span></span> <span data-ttu-id="6b6c4-135">Merhaba altında **rolleri** düğümü, tooupdate isterseniz ve, hello bağlam menüsünden seçin sağ hello rol **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-135">Under hello **Roles** node, right-click hello role you want tooupdate, and, from hello context menu, select **Properties**.</span></span>

    ![Çözüm Gezgini Azure rol bağlam menüsü](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="6b6c4-137">Select hello **yapılandırma** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-137">Select hello **Configuration** tab.</span></span>

    ![Yapılandırma sekmesi](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page.png)

1. <span data-ttu-id="6b6c4-139">Merhaba, **hizmet yapılandırmasını** listesi, select hello hizmet yapılandırmasını tooupdate istiyor.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-139">In hello **Service Configuration** list, select hello service configuration that you want tooupdate.</span></span>
   
    ![Hizmet yapılandırma listesi](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page-select-configuration.png)

1. <span data-ttu-id="6b6c4-141">Merhaba, **örnek sayısını** metin kutusunda, bu rol için toostart istediğiniz örnekleri hello sayısını girin.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-141">In hello **Instance count** text box, enter hello number of instances that you want toostart for this role.</span></span> <span data-ttu-id="6b6c4-142">Merhaba bulut hizmeti tooAzure yayımladığınızda, her bir örneği farklı bir sanal makinede çalışır.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-142">Each instance runs on a separate virtual machine when you publish hello cloud service tooAzure.</span></span>

    ![Güncelleştirme hello örnek sayısı](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page-instance-count.png)

1. <span data-ttu-id="6b6c4-144">Visual Studio hello gelen araç, select **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-144">From hello Visual Studio, toolbar, select **Save**.</span></span>

## <a name="manage-connection-strings-for-storage-accounts"></a><span data-ttu-id="6b6c4-145">Depolama hesapları için bağlantı dizelerini Yönet</span><span class="sxs-lookup"><span data-stu-id="6b6c4-145">Manage connection strings for storage accounts</span></span>
<span data-ttu-id="6b6c4-146">Ekleyin, kaldırın veya bağlantı dizeleri, hizmet yapılandırması için değiştirin.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-146">You can add, remove, or modify connection strings for your service configurations.</span></span> <span data-ttu-id="6b6c4-147">Örneğin, bir yerel bağlantı dizesi değerine sahip bir yerel hizmet yapılandırması için isteyebilirsiniz `UseDevelopmentStorage=true`.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-147">For example, you might want a local connection string for a local service configuration that has a value of `UseDevelopmentStorage=true`.</span></span> <span data-ttu-id="6b6c4-148">Tooconfigure Azure'da bir depolama hesabını kullanan bir bulut hizmeti yapılandırması da isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-148">You might also want tooconfigure a cloud service configuration that uses a storage account in Azure.</span></span>

> [!WARNING]
> <span data-ttu-id="6b6c4-149">Bir depolama hesabı bağlantı dizesi için hello Azure depolama hesabı anahtar bilgileri girdiğinizde, bu bilgileri yerel olarak hello hizmet yapılandırma dosyasında depolanır.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-149">When you enter hello Azure storage account key information for a storage account connection string, this information is stored locally in hello service configuration file.</span></span> <span data-ttu-id="6b6c4-150">Ancak, bu bilgileri şu anda şifreli metin olarak depolanmaz.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-150">However, this information is currently not stored as encrypted text.</span></span>
> 
> 

<span data-ttu-id="6b6c4-151">Her hizmet yapılandırması için farklı bir değer kullanarak, değil toouse farklı bağlantı dizeleri, bulut hizmeti olan veya Bulut hizmeti tooAzure yayımladığınızda, kodunuzu değiştirin.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-151">By using a different value for each service configuration, you do not have toouse different connection strings in your cloud service or modify your code when you publish your cloud service tooAzure.</span></span> <span data-ttu-id="6b6c4-152">Bulut hizmetinizi derlerken veya yayımladığınızda seçin hello hizmet yapılandırmasını temel alarak hello bağlantı dizesinde kodu ve hello değer için aynı adı farklı hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-152">You can use hello same name for hello connection string in your code and hello value is different, based on hello service configuration that you select when you build your cloud service or when you publish it.</span></span>

1. <span data-ttu-id="6b6c4-153">Oluşturun veya bir Azure bulut hizmeti projesini Visual Studio'da açın.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-153">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="6b6c4-154">İçinde **Çözüm Gezgini**, başlangıç projesi düğümünü genişletin.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-154">In **Solution Explorer**, expand hello project node.</span></span> <span data-ttu-id="6b6c4-155">Merhaba altında **rolleri** düğümü, tooupdate isterseniz ve, hello bağlam menüsünden seçin sağ hello rol **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-155">Under hello **Roles** node, right-click hello role you want tooupdate, and, from hello context menu, select **Properties**.</span></span>

    ![Çözüm Gezgini Azure rol bağlam menüsü](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="6b6c4-157">Select hello **ayarları** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-157">Select hello **Settings** tab.</span></span>

    ![Ayarlar sekmesi](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab.png)

1. <span data-ttu-id="6b6c4-159">Merhaba, **hizmet yapılandırmasını** listesi, select hello hizmet yapılandırmasını tooupdate istiyor.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-159">In hello **Service Configuration** list, select hello service configuration that you want tooupdate.</span></span>

    ![Hizmet yapılandırması](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-select-configuration.png)

1. <span data-ttu-id="6b6c4-161">tooadd bir bağlantı dizesi seçin **ayar Ekle**.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-161">tooadd a connection string, select **Add Setting**.</span></span>

    ![Bağlantı dizesi Ekle](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting.png)

1. <span data-ttu-id="6b6c4-163">Merhaba yeni ayar toohello listesi eklendikten sonra hello listesindeki hello satır hello gerekli bilgilerle güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-163">Once hello new setting has been added toohello list, update hello row in hello list with hello necessary information.</span></span>

    ![Yeni bağlantı dizesi](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting-new-setting.png)

    - <span data-ttu-id="6b6c4-165">**Ad** -toouse hello bağlantı dizesi için istediğiniz hello adını girin.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-165">**Name** - Enter hello name that you want toouse for hello connection string.</span></span>
    - <span data-ttu-id="6b6c4-166">**Tür** - seçin **bağlantı dizesi** hello aşağı açılan listeden.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-166">**Type** - Select **Connection String** from hello drop-down list.</span></span>
    - <span data-ttu-id="6b6c4-167">**Değer** -hello bağlantı dizesi doğrudan hello girebilirsiniz **değeri** hücre veya select hello üç nokta (...) toowork hello içinde **depolama bağlantı dizesi oluştur** iletişim.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-167">**Value** - You can either enter hello connection string directly into hello **Value** cell, or select hello ellipsis (...) toowork in hello **Create Storage Connection String** dialog.</span></span>  

1. <span data-ttu-id="6b6c4-168">Merhaba, **depolama bağlantı dizesi oluştur** iletişim kutusunda bir seçenek için **bağlanırken**.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-168">In hello **Create Storage Connection String** dialog, select an option for **Connect using**.</span></span> <span data-ttu-id="6b6c4-169">Ardından, hello seçeneği hello yönergeleri izleyin:</span><span class="sxs-lookup"><span data-stu-id="6b6c4-169">Then follow hello instructions for hello option you select:</span></span>

    - <span data-ttu-id="6b6c4-170">**Microsoft Azure storage öykünücüsü** -bu seçeneği seçerseniz, yalnızca tooAzure uygulamak gibi hello kalan ayarları hello iletişim kutusundaki devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-170">**Microsoft Azure storage emulator** - If you select this option, hello remaining settings on hello dialog are disabled as they apply only tooAzure.</span></span> <span data-ttu-id="6b6c4-171">**Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-171">Select **OK**.</span></span>
    - <span data-ttu-id="6b6c4-172">**Aboneliğinizi** - bu seçenek, kullanım hello açılır liste tooeither seçin ve oturum bir Microsoft hesabı seçin ya da bir Microsoft hesabı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-172">**Your subscription** - If you select this option, use hello dropdown list tooeither select and sign into a Microsoft account, or add a Microsoft account.</span></span> <span data-ttu-id="6b6c4-173">Bir Azure aboneliği ve depolama hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-173">Select an Azure subscription and storage account.</span></span> <span data-ttu-id="6b6c4-174">**Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-174">Select **OK**.</span></span>
    - <span data-ttu-id="6b6c4-175">**Kimlik bilgileri'el ile girilen** - hello depolama hesabı adı girin ve ya da birincil veya ikinci anahtarı hello.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-175">**Manually entered credentials** - Enter hello storage account name, and either hello primary or second key.</span></span> <span data-ttu-id="6b6c4-176">Bir seçenek belirleyin **bağlantı** (HTTPS çoğu senaryolar için önerilir.) **Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-176">Select an option for **Connection** (HTTPS is recommended for most scenarios.) Select **OK**.</span></span>

1. <span data-ttu-id="6b6c4-177">bir bağlantı dizesi toodelete hello bağlantı dizesi seçin ve ardından **Kaldır ayarını**.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-177">toodelete a connection string, select hello connection string, and then select **Remove Setting**.</span></span>

1. <span data-ttu-id="6b6c4-178">Visual Studio hello gelen araç, select **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-178">From hello Visual Studio, toolbar, select **Save**.</span></span>

## <a name="programmatically-access-a-connection-string"></a><span data-ttu-id="6b6c4-179">Bir bağlantı dizesi programlamayla erişme</span><span class="sxs-lookup"><span data-stu-id="6b6c4-179">Programmatically access a connection string</span></span>

<span data-ttu-id="6b6c4-180">Merhaba aşağıdaki adımlar nasıl tooprogrammatically erişim C# kullanarak bir bağlantı dizesi gösterir.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-180">hello following steps show how tooprogrammatically access a connection string using C#.</span></span>

1. <span data-ttu-id="6b6c4-181">Merhaba aşağıdakileri ekleyin nerede bulacağınızı toouse hello ayarı yönergeleri tooa C# dosyasını kullanarak:</span><span class="sxs-lookup"><span data-stu-id="6b6c4-181">Add hello following using directives tooa C# file where you are going toouse hello setting:</span></span>

    ```csharp
    using Microsoft.WindowsAzure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.ServiceRuntime;
    ```

1. <span data-ttu-id="6b6c4-182">Merhaba aşağıdaki kod örnek nasıl gösterilmiştir tooaccess bir bağlantı dizesi.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-182">hello following code illustrates an example of how tooaccess a connection string.</span></span> <span data-ttu-id="6b6c4-183">Hello yerine &lt;ConnectionStringName > yer tutucu hello uygun değere sahip.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-183">Replace hello &lt;ConnectionStringName> placeholder with hello appropriate value.</span></span> 

    ```csharp
    // Setup hello connection tooAzure Storage
    var storageAccount = CloudStorageAccount.Parse(RoleEnvironment.GetConfigurationSettingValue("<ConnectionStringName>"));
    ```

## <a name="add-custom-settings-toouse-in-your-azure-cloud-service"></a><span data-ttu-id="6b6c4-184">Azure bulut hizmetinize özel ayarları toouse Ekle</span><span class="sxs-lookup"><span data-stu-id="6b6c4-184">Add custom settings toouse in your Azure cloud service</span></span>
<span data-ttu-id="6b6c4-185">Hello hizmet yapılandırma dosyalarında özel ayarlar bir ad ve bir özel hizmet yapılandırması için bir dize değeri eklemenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-185">Custom settings in hello service configuration file let you add a name and value for a string for a specific service configuration.</span></span> <span data-ttu-id="6b6c4-186">Bir özellik başlangıç değeri okuyarak bulut hizmetinizde hello ayarlama ve bu değer toocontrol hello mantığı kodunuzda kullanarak bu ayarı tooconfigure toouse seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-186">You might choose toouse this setting tooconfigure a feature in your cloud service by reading hello value of hello setting and using this value toocontrol hello logic in your code.</span></span> <span data-ttu-id="6b6c4-187">Hizmet paketi toorebuild kalmadan veya Bulut hizmetiniz çalıştırırken bu hizmeti yapılandırma değerlerini değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-187">You can change these service configuration values without having toorebuild your service package or when your cloud service is running.</span></span> <span data-ttu-id="6b6c4-188">Kodunuzu bildirimleri için bir ayar değiştiğinde kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-188">Your code can check for notifications of when a setting changes.</span></span> <span data-ttu-id="6b6c4-189">Bkz: [RoleEnvironment.Changing olay](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx).</span><span class="sxs-lookup"><span data-stu-id="6b6c4-189">See [RoleEnvironment.Changing Event](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx).</span></span>

<span data-ttu-id="6b6c4-190">Ekleyin, kaldırın veya hizmet yapılandırmalarınızı için özel ayarları değiştirin.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-190">You can add, remove, or modify custom settings for your service configurations.</span></span> <span data-ttu-id="6b6c4-191">Bu dizeler için farklı hizmet yapılandırması için farklı değerler isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-191">You might want different values for these strings for different service configurations.</span></span>

<span data-ttu-id="6b6c4-192">Her hizmet yapılandırması için farklı bir değer kullanarak, değil toouse farklı dizeleri, bulut hizmeti olan veya Bulut hizmeti tooAzure yayımladığınızda, kodunuzu değiştirin.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-192">By using a different value for each service configuration, you do not have toouse different strings in your cloud service or modify your code when you publish your cloud service tooAzure.</span></span> <span data-ttu-id="6b6c4-193">Bulut hizmetinizi derlerken veya yayımladığınızda seçin hello hizmet yapılandırmasını temel alarak, kod ve hello değerindeki hello dizesi için aynı adı farklı hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-193">You can use hello same name for hello string in your code and hello value is different, based on hello service configuration that you select when you build your cloud service or when you publish it.</span></span>

1. <span data-ttu-id="6b6c4-194">Oluşturun veya bir Azure bulut hizmeti projesini Visual Studio'da açın.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-194">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="6b6c4-195">İçinde **Çözüm Gezgini**, başlangıç projesi düğümünü genişletin.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-195">In **Solution Explorer**, expand hello project node.</span></span> <span data-ttu-id="6b6c4-196">Merhaba altında **rolleri** düğümü, tooupdate isterseniz ve, hello bağlam menüsünden seçin sağ hello rol **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-196">Under hello **Roles** node, right-click hello role you want tooupdate, and, from hello context menu, select **Properties**.</span></span>

    ![Çözüm Gezgini Azure rol bağlam menüsü](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="6b6c4-198">Select hello **ayarları** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-198">Select hello **Settings** tab.</span></span>

    ![Ayarlar sekmesi](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab.png)

1. <span data-ttu-id="6b6c4-200">Merhaba, **hizmet yapılandırmasını** listesi, select hello hizmet yapılandırmasını tooupdate istiyor.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-200">In hello **Service Configuration** list, select hello service configuration that you want tooupdate.</span></span>

    ![Hizmet yapılandırma listesi](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-select-configuration.png)

1. <span data-ttu-id="6b6c4-202">tooadd özel bir ayar seçin **ayar Ekle**.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-202">tooadd a custom setting, select **Add Setting**.</span></span>

    ![Özel ayar Ekle](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting.png)

1. <span data-ttu-id="6b6c4-204">Merhaba yeni ayar toohello listesi eklendikten sonra hello listesindeki hello satır hello gerekli bilgilerle güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-204">Once hello new setting has been added toohello list, update hello row in hello list with hello necessary information.</span></span>

    ![Yeni özel ayar](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting-new-setting.png)

    - <span data-ttu-id="6b6c4-206">**Ad** -hello ayarı hello adını girin.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-206">**Name** - Enter hello name of hello setting.</span></span>
    - <span data-ttu-id="6b6c4-207">**Tür** - seçin **dize** hello aşağı açılan listeden.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-207">**Type** - Select **String** from hello drop-down list.</span></span>
    - <span data-ttu-id="6b6c4-208">**Değer** -hello ayarı hello değeri girin.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-208">**Value** - Enter hello value of hello setting.</span></span> <span data-ttu-id="6b6c4-209">Merhaba değeri doğrudan hello girebilirsiniz **değeri** hücre veya select hello üç nokta (...) tooenter hello hello değerinde **dize Düzenle** iletişim.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-209">You can either enter hello value directly into hello **Value** cell, or select hello ellipsis (...) tooenter hello value in hello **Edit String** dialog.</span></span>  

1. <span data-ttu-id="6b6c4-210">toodelete özel bir ayar hello ayarı seçin ve ardından **Kaldır ayarını**.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-210">toodelete a custom setting, select hello setting, and then select **Remove Setting**.</span></span>

1. <span data-ttu-id="6b6c4-211">Visual Studio hello gelen araç, select **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-211">From hello Visual Studio, toolbar, select **Save**.</span></span>

## <a name="programmatically-access-a-custom-settings-value"></a><span data-ttu-id="6b6c4-212">Özel bir ayarın değerini programlamayla erişme</span><span class="sxs-lookup"><span data-stu-id="6b6c4-212">Programmatically access a custom setting's value</span></span>
 
<span data-ttu-id="6b6c4-213">Merhaba aşağıdaki adımlar nasıl tooprogrammatically erişim C# kullanarak özel bir ayar gösterir.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-213">hello following steps show how tooprogrammatically access a custom setting using C#.</span></span>

1. <span data-ttu-id="6b6c4-214">Merhaba aşağıdakileri ekleyin nerede bulacağınızı toouse hello ayarı yönergeleri tooa C# dosyasını kullanarak:</span><span class="sxs-lookup"><span data-stu-id="6b6c4-214">Add hello following using directives tooa C# file where you are going toouse hello setting:</span></span>

    ```csharp
    using Microsoft.WindowsAzure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.ServiceRuntime;
    ```

1. <span data-ttu-id="6b6c4-215">Merhaba aşağıdaki kod örnek nasıl gösterilmiştir tooaccess özel bir ayar.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-215">hello following code illustrates an example of how tooaccess a custom setting.</span></span> <span data-ttu-id="6b6c4-216">Hello yerine &lt;SettingName > yer tutucu hello uygun değere sahip.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-216">Replace hello &lt;SettingName> placeholder with hello appropriate value.</span></span> 
    
    ```csharp
    var settingValue = RoleEnvironment.GetConfigurationSettingValue("<SettingName>");
    ```

## <a name="manage-local-storage-for-each-role-instance"></a><span data-ttu-id="6b6c4-217">Her rol örneği için yerel depolama yönetin</span><span class="sxs-lookup"><span data-stu-id="6b6c4-217">Manage local storage for each role instance</span></span>
<span data-ttu-id="6b6c4-218">Her bir rol örneği için yerel dosya sistemi depolama ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-218">You can add local file system storage for each instance of a role.</span></span> <span data-ttu-id="6b6c4-219">Depolama erişilebilir değil, diğer örnekler için hangi hello veriler hello rolünün tarafından veya diğer rolleri tarafından depolanan hello verileri.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-219">hello data stored in that storage is not accessible by other instances of hello role for which hello data is stored, or by other roles.</span></span>  

1. <span data-ttu-id="6b6c4-220">Oluşturun veya bir Azure bulut hizmeti projesini Visual Studio'da açın.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-220">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="6b6c4-221">İçinde **Çözüm Gezgini**, başlangıç projesi düğümünü genişletin.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-221">In **Solution Explorer**, expand hello project node.</span></span> <span data-ttu-id="6b6c4-222">Merhaba altında **rolleri** düğümü, tooupdate isterseniz ve, hello bağlam menüsünden seçin sağ hello rol **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-222">Under hello **Roles** node, right-click hello role you want tooupdate, and, from hello context menu, select **Properties**.</span></span>

    ![Çözüm Gezgini Azure rol bağlam menüsü](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="6b6c4-224">Select hello **yerel depolama** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-224">Select hello **Local Storage** tab.</span></span>

    ![Yerel depolama sekmesi](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab.png)

1. <span data-ttu-id="6b6c4-226">Merhaba, **hizmet yapılandırmasını** listesinde **tüm yapılandırmaları** hello yerel depolama ayarlarını tooall hizmet yapılandırması geçerli olarak seçilen.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-226">In hello **Service Configuration** list, ensure that **All Configurations** is selected as hello local storage settings apply tooall service configurations.</span></span> <span data-ttu-id="6b6c4-227">Başka bir değer devre dışı bırakılıyor hello sayfasında tüm hello giriş alanları sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-227">Any other value results in all hello input fields on hello page being disabled.</span></span> 

    ![Hizmet yapılandırma listesi](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-service-configuration.png)

1. <span data-ttu-id="6b6c4-229">tooadd bir yerel depolama girdisi seçin **yerel depolama alanı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-229">tooadd a local storage entry, select **Add Local Storage**.</span></span>

    ![Yerel depolama ekleyin](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-add-local-storage.png)

1. <span data-ttu-id="6b6c4-231">Merhaba yeni yerel depolama girdisi toohello listesi eklendikten sonra hello listesindeki hello satır hello gerekli bilgilerle güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-231">Once hello new local storage entry has been added toohello list, update hello row in hello list with hello necessary information.</span></span>

    ![Yeni yerel depolama girdisi](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-new-local-storage.png)

    - <span data-ttu-id="6b6c4-233">**Ad** -toouse hello yeni yerel depolama için istediğiniz hello adını girin.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-233">**Name** - Enter hello name that you want toouse for hello new local storage.</span></span>
    - <span data-ttu-id="6b6c4-234">**Boyut (MB)** -hello yeni yerel depolama için gereksinim duyduğunuz MB hello boyutu girin.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-234">**Size (MB)** - Enter hello size in MB that you need for hello new local storage.</span></span>
    - <span data-ttu-id="6b6c4-235">**Rol geri dönüşüm üzerinde temiz** -hello sanal makine hello rol için geri dönüştürüldüğünde hello yeni yerel depolama bu seçeneği tooremove hello verileri seçin.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-235">**Clean on role recycle** - Select this option tooremove hello data in hello new local storage when hello virtual machine for hello role is recycled.</span></span>

1. <span data-ttu-id="6b6c4-236">toodelete bir yerel depolama girdisi hello girişi seçin ve ardından **kaldırmak yerel depolama**.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-236">toodelete a local storage entry, select hello entry, and then select **Remove Local Storage**.</span></span>

1. <span data-ttu-id="6b6c4-237">Visual Studio hello gelen araç, select **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-237">From hello Visual Studio, toolbar, select **Save**.</span></span>

## <a name="programmatically-accessing-local-storage"></a><span data-ttu-id="6b6c4-238">Program aracılığıyla yerel depolamaya erişme</span><span class="sxs-lookup"><span data-stu-id="6b6c4-238">Programmatically accessing local storage</span></span>

<span data-ttu-id="6b6c4-239">Bu bölümde nasıl tooprogrammatically erişim kullanarak C# test metin dosyası yazarak yerel depolama anlatılacaktır `MyLocalStorageTest.txt`.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-239">This section illustrates how tooprogrammatically access local storage using C# by writing a test text file `MyLocalStorageTest.txt`.</span></span>  

### <a name="write-a-text-file-toolocal-storage"></a><span data-ttu-id="6b6c4-240">Bir metin dosyası toolocal depolama yazma</span><span class="sxs-lookup"><span data-stu-id="6b6c4-240">Write a text file toolocal storage</span></span>

<span data-ttu-id="6b6c4-241">koddan hello nasıl toowrite bir metin dosyası toolocal depolama örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-241">hello following code shows an example of how toowrite a text file toolocal storage.</span></span> <span data-ttu-id="6b6c4-242">Hello yerine &lt;LocalStorageName > yer tutucu hello uygun değere sahip.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-242">Replace hello &lt;LocalStorageName> placeholder with hello appropriate value.</span></span> 

    ```csharp
    // Retrieve an object that points toohello local storage resource
    LocalResource localResource = RoleEnvironment.GetLocalResource("<LocalStorageName>");
    
    //Define hello file name and path
    string[] paths = { localResource.RootPath, "MyLocalStorageTest.txt" };
    String filePath = Path.Combine(paths);
    
    using (FileStream writeStream = File.Create(filePath))
    {
        Byte[] textToWrite = new UTF8Encoding(true).GetBytes("Testing Web role storage");
        writeStream.Write(textToWrite, 0, textToWrite.Length);
    }

    ```

### <a name="find-a-file-written-toolocal-storage"></a><span data-ttu-id="6b6c4-243">Toolocal depolama yazılmış bir dosya bulunamadı</span><span class="sxs-lookup"><span data-stu-id="6b6c4-243">Find a file written toolocal storage</span></span>

<span data-ttu-id="6b6c4-244">Merhaba önceki bölümdeki hello kodu tarafından oluşturulan tooview hello dosyasını aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="6b6c4-244">tooview hello file created by hello code in hello previous section, follow these steps:</span></span>
    
1.  <span data-ttu-id="6b6c4-245">Buna Windows bildirim alanındaki hello hello Azure simgesini sağ tıklatın ve, hello bağlam menüsünden seçin **Göster işlem öykünücüsü kullanıcı Arabiriminde**.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-245">In hello Windows notification area, right-click hello Azure icon, and, from hello context menu, select **Show Compute Emulator UI**.</span></span> 

    ![Azure işlem öykünücüsünü Göster](./media/vs-azure-tools-configure-roles-for-cloud-service/show-compute-emulator.png)

1. <span data-ttu-id="6b6c4-247">Merhaba web rolü seçin.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-247">Select hello web role.</span></span>

    ![Azure işlem öykünücüsü](./media/vs-azure-tools-configure-roles-for-cloud-service/compute-emulator.png)

1. <span data-ttu-id="6b6c4-249">Merhaba üzerinde **Microsoft Azure işlem öykünücüsü** menüsünde, select **Araçları** > **açık yerel deposu**.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-249">On hello **Microsoft Azure Compute Emulator** menu, select **Tools** > **Open local store**.</span></span>

    ![Açık yerel deposu menü öğesi](./media/vs-azure-tools-configure-roles-for-cloud-service/compute-emulator-open-local-store-menu.png)

1. <span data-ttu-id="6b6c4-251">Merhaba Windows Gezgini penceresi açıldığında, girin ' MyLocalStorageTest.txt'' hello içine **arama** metin kutusu ve select **Enter** toostart hello arama.</span><span class="sxs-lookup"><span data-stu-id="6b6c4-251">When hello Windows Explorer window opens, enter `MyLocalStorageTest.txt`\` into hello **Search** text box, and select **Enter** toostart hello search.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="6b6c4-252">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6b6c4-252">Next steps</span></span>
<span data-ttu-id="6b6c4-253">Visual Studio'da Azure projeler hakkında daha fazla bilgi okuyarak [bir Azure projesi yapılandırma](vs-azure-tools-configuring-an-azure-project.md).</span><span class="sxs-lookup"><span data-stu-id="6b6c4-253">Learn more about Azure projects in Visual Studio by reading [Configuring an Azure Project](vs-azure-tools-configuring-an-azure-project.md).</span></span> <span data-ttu-id="6b6c4-254">Okuyarak hello bulut hizmeti şeması hakkında daha fazla bilgi [şema başvurusu](https://msdn.microsoft.com/library/azure/dd179398).</span><span class="sxs-lookup"><span data-stu-id="6b6c4-254">Learn more about hello cloud service schema by reading [Schema Reference](https://msdn.microsoft.com/library/azure/dd179398).</span></span>

