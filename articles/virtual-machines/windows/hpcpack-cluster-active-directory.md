---
title: "aaaHPC paketi küme Azure Active Directory ile | Microsoft Docs"
description: "Azure Active Directory ile Azure toointegrate bir HPC Pack 2016 nasıl kümesi öğrenin"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
ms.assetid: 9edf9559-db02-438b-8268-a6cba7b5c8b7
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 11/14/2016
ms.author: danlep
ms.openlocfilehash: 0806e544a468e27ca0567e18c55554811584fbc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-hpc-pack-cluster-in-azure-using-azure-active-directory"></a><span data-ttu-id="299ec-103">Azure Active Directory'yi kullanarak Azure HPC Pack kümede yönetme</span><span class="sxs-lookup"><span data-stu-id="299ec-103">Manage an HPC Pack cluster in Azure using Azure Active Directory</span></span>
<span data-ttu-id="299ec-104">[Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) ile tümleştirmeyi destekleyen [Azure Active Directory](../../active-directory/index.md) (Azure AD) Azure HPC Pack kümede dağıtmak Yöneticiler için.</span><span class="sxs-lookup"><span data-stu-id="299ec-104">[Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) supports integration with [Azure Active Directory](../../active-directory/index.md) (Azure AD) for administrators who deploy an HPC Pack cluster in Azure.</span></span>



<span data-ttu-id="299ec-105">Yüksek düzey görevler aşağıdaki hello için bu makaledeki Hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="299ec-105">Follow hello steps in this article for hello following high level tasks:</span></span> 
* <span data-ttu-id="299ec-106">HPC Pack kümenizi Azure AD kiracınıza el ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="299ec-106">Manually integrate your HPC Pack cluster with your Azure AD tenant</span></span>
* <span data-ttu-id="299ec-107">Yönetmek ve azure'da HPC Pack kümenizdeki işlerini zamanla</span><span class="sxs-lookup"><span data-stu-id="299ec-107">Manage and schedule jobs in your HPC Pack cluster in Azure</span></span> 

<span data-ttu-id="299ec-108">HPC Pack küme çözümünü Azure AD ile tümleştirme, diğer uygulamalar ve hizmetler standart adımları toointegrate izler.</span><span class="sxs-lookup"><span data-stu-id="299ec-108">Integrating an HPC Pack cluster solution with Azure AD follows standard steps toointegrate other applications and services.</span></span> <span data-ttu-id="299ec-109">Bu makale, Azure AD'de temel kullanıcı yönetimi ile bildiğinizi varsayar.</span><span class="sxs-lookup"><span data-stu-id="299ec-109">This article assumes you are familiar with basic user management in Azure AD.</span></span> <span data-ttu-id="299ec-110">Daha fazla bilgi ve arka plan için hello bkz [Azure Active Directory belgelerindeki](../../active-directory/index.md) ve hello aşağıdaki bölümü.</span><span class="sxs-lookup"><span data-stu-id="299ec-110">For more information and background, see hello [Azure Active Directory documentation](../../active-directory/index.md) and hello following section.</span></span>

## <a name="benefits-of-integration"></a><span data-ttu-id="299ec-111">Tümleştirme yararları</span><span class="sxs-lookup"><span data-stu-id="299ec-111">Benefits of integration</span></span>


<span data-ttu-id="299ec-112">Azure Active Directory (Azure AD), toocloud çözümleri çoklu oturum açma (SSO) erişimi sağlayan bir çok kiracılı bulut tabanlı dizin ve kimlik yönetimi hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="299ec-112">Azure Active Directory (Azure AD) is a multi-tenant cloud-based directory and identity management service that provides single sign-on (SSO) access toocloud solutions.</span></span>

<span data-ttu-id="299ec-113">HPC Pack küme Azure AD ile tümleştirilmesi hedeflerini izleyerek hello elde yardımcı olabilir:</span><span class="sxs-lookup"><span data-stu-id="299ec-113">Integration of an HPC Pack cluster with Azure AD can help you achieve hello following goals:</span></span>

* <span data-ttu-id="299ec-114">Merhaba geleneksel Active Directory etki alanı denetleyicisi hello HPC Pack kümeden kaldırın.</span><span class="sxs-lookup"><span data-stu-id="299ec-114">Remove hello traditional Active Directory domain controller from hello HPC Pack cluster.</span></span> <span data-ttu-id="299ec-115">Bu, bu, iş ve faturalamak hello dağıtım işlemi için gerekli değilse hello küme koruma hello maliyetlerini azaltmaya yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="299ec-115">This can help reduce hello costs of maintaining hello cluster if this is not necessary for your business, and speed-up hello deployment process.</span></span>
* <span data-ttu-id="299ec-116">Azure AD tarafından yapılmadan avantajları aşağıdaki hello yararlanın:</span><span class="sxs-lookup"><span data-stu-id="299ec-116">Leverage hello following benefits that are brought by Azure AD:</span></span>
    *   <span data-ttu-id="299ec-117">Çoklu oturum açma</span><span class="sxs-lookup"><span data-stu-id="299ec-117">Single sign-on</span></span> 
    *   <span data-ttu-id="299ec-118">Azure'da hello HPC paketi küme için bir yerel AD kimliği kullanma</span><span class="sxs-lookup"><span data-stu-id="299ec-118">Using a local AD identity for hello HPC Pack cluster in Azure</span></span> 

    ![Azure Active Directory ortamı](./media/hpcpack-cluster-active-directory/aad.png)


## <a name="prerequisites"></a><span data-ttu-id="299ec-120">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="299ec-120">Prerequisites</span></span>
* <span data-ttu-id="299ec-121">**Azure sanal makinelerinde dağıtılan HPC Pack 2016 küme** - adımları için bkz: [Azure HPC Pack 2016 kümede dağıtmak](hpcpack-2016-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="299ec-121">**HPC Pack 2016 cluster deployed in Azure virtual machines** - For steps, see [Deploy an HPC Pack 2016 cluster in Azure](hpcpack-2016-cluster.md).</span></span> <span data-ttu-id="299ec-122">Hello DNS ad hello baş düğümü ve bu makaledeki hello adımları tamamlamak için bir Küme Yöneticisi kimlik bilgilerini hello gerekir.</span><span class="sxs-lookup"><span data-stu-id="299ec-122">You need hello DNS name of hello head node and hello credentials of a cluster administrator to complete hello steps in this article.</span></span>

  > [!NOTE]
  > <span data-ttu-id="299ec-123">Azure Active Directory Tümleştirme HPC Pack HPC Pack 2016 önce sürümlerinde desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="299ec-123">Azure Active Directory integration is not supported in versions of HPC Pack before HPC Pack 2016.</span></span>



* <span data-ttu-id="299ec-124">**İstemci bilgisayar** -bir Windows veya Windows Server istemci bilgisayar çok çalıştırmak HPC Pack istemci yardımcı programları gerekir.</span><span class="sxs-lookup"><span data-stu-id="299ec-124">**Client computer** - You need a Windows or Windows Server client computer too run HPC Pack client utilities.</span></span> <span data-ttu-id="299ec-125">Yalnızca toouse hello HPC paketi web portalı veya REST API toosubmit işleri istiyorsanız, tercih ettiğiniz herhangi bir istemci bilgisayarı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="299ec-125">If you only want toouse hello HPC Pack web portal or REST API toosubmit jobs, you can use any client computer of your choice.</span></span>

* <span data-ttu-id="299ec-126">**HPC Pack istemci yardımcı programları** -hello HPC Pack istemci yardımcı programları hello istemci bilgisayarda, Microsoft Download Center hello kullanılabilir hello ücretsiz yükleme paketini kullanarak yükleyin.</span><span class="sxs-lookup"><span data-stu-id="299ec-126">**HPC Pack client utilities** - Install hello HPC Pack client utilities on hello client computer, using hello free installation package available from hello Microsoft Download Center.</span></span>


## <a name="step-1-register-hello-hpc-cluster-server-with-your-azure-ad-tenant"></a><span data-ttu-id="299ec-127">1. adım: Azure AD kiracınıza hello HPC küme sunucusu kaydetme</span><span class="sxs-lookup"><span data-stu-id="299ec-127">Step 1: Register hello HPC cluster server with your Azure AD tenant</span></span>
1. <span data-ttu-id="299ec-128">İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="299ec-128">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="299ec-129">Tıklatın **Active Directory** hello soldaki menüden ve aboneliğinizi istenilen dizinde hello'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="299ec-129">Click **Active Directory** in hello left menu, and then click hello desired directory in your subscription.</span></span> <span data-ttu-id="299ec-130">İzni tooaccess kaynakları hello dizinde olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="299ec-130">You must have permission tooaccess resources in hello directory.</span></span>
3. <span data-ttu-id="299ec-131">Tıklatın **kullanıcılar**ve kullanıcı hesapları zaten oluşturuldu veya yapılandırılmış olmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="299ec-131">Click **Users**, and make sure there are user accounts already created or configured.</span></span>
4. <span data-ttu-id="299ec-132">Tıklatın **uygulamaları** > **Ekle**ve ardından **kuruluşumun geliştirmekte olduğu bir uygulama Ekle**.</span><span class="sxs-lookup"><span data-stu-id="299ec-132">Click **Applications** > **Add**, and then click **Add an application my organization is developing**.</span></span> <span data-ttu-id="299ec-133">Başlangıç Sihirbazı'nda bilgisinden hello girin:</span><span class="sxs-lookup"><span data-stu-id="299ec-133">Enter hello following information in hello wizard:</span></span>
    * <span data-ttu-id="299ec-134">**Ad** -HPCPackClusterServer</span><span class="sxs-lookup"><span data-stu-id="299ec-134">**Name** - HPCPackClusterServer</span></span>
    * <span data-ttu-id="299ec-135">**Tür** - seçin **Web uygulaması ve/veya Web API'si**</span><span class="sxs-lookup"><span data-stu-id="299ec-135">**Type** - Select **Web Application and/or Web API**</span></span>
    * <span data-ttu-id="299ec-136">**URL oturum açma**- hello varsayılan olarak hello örnek için ana URL`https://hpcserver`</span><span class="sxs-lookup"><span data-stu-id="299ec-136">**Sign-on URL**- hello base URL for hello sample, which is by default `https://hpcserver`</span></span>
    * <span data-ttu-id="299ec-137">**Uygulama Kimliği URI'si** - `https://<Directory_name>/<application_name>`.</span><span class="sxs-lookup"><span data-stu-id="299ec-137">**App ID URI** - `https://<Directory_name>/<application_name>`.</span></span> <span data-ttu-id="299ec-138">Değiştir `<Directory_name`> Merhaba, Azure AD kiracısıdır, örneğin, tam ad ile `hpclocal.onmicrosoft.com`ve değiştirme `<application_name>` daha önce seçtiğiniz hello ada sahip.</span><span class="sxs-lookup"><span data-stu-id="299ec-138">Replace `<Directory_name`> with hello full name of your Azure AD tenant, for example, `hpclocal.onmicrosoft.com`, and replace `<application_name>` with hello name you chose previously.</span></span>

5. <span data-ttu-id="299ec-139">Merhaba uygulama eklendikten sonra tıklatın **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="299ec-139">After hello app is added, click **Configure**.</span></span> <span data-ttu-id="299ec-140">Aşağıdaki özelliklere hello yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="299ec-140">Configure hello following properties:</span></span>
    * <span data-ttu-id="299ec-141">Seçin **Evet** için **uygulamasıdır çok kiracılı**</span><span class="sxs-lookup"><span data-stu-id="299ec-141">Select **Yes** for **Application is multi-tenant**</span></span>
    * <span data-ttu-id="299ec-142">Seçin **Evet** için **kullanıcı atama gerekli tooaccess uygulama**.</span><span class="sxs-lookup"><span data-stu-id="299ec-142">Select **Yes** for **User assignment required tooaccess app**.</span></span>

6. <span data-ttu-id="299ec-143">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="299ec-143">Click **Save**.</span></span> <span data-ttu-id="299ec-144">Kaydetme tamamlandığında tıklayın **yönetmek bildirim**.</span><span class="sxs-lookup"><span data-stu-id="299ec-144">When saving completes, click **Manage Manifest**.</span></span> <span data-ttu-id="299ec-145">Bu eylem, uygulamanızın bildirim JavaScript nesne gösterimi (JSON) dosyası indirir.</span><span class="sxs-lookup"><span data-stu-id="299ec-145">This action downloads your application’s manifest JavaScript object notation (JSON) file.</span></span> <span data-ttu-id="299ec-146">Merhaba bulma tarafından düzenleme indirilen hello bildirimi `appRoles` ayarlama ve uygulama rolü aşağıdaki hello ekleme:</span><span class="sxs-lookup"><span data-stu-id="299ec-146">Edit hello downloaded manifest by locating hello `appRoles` setting and adding hello following application role:</span></span>
    ```json
    "appRoles": [
        {
        "allowedMemberTypes": [
            "User",
            "Application"
        ],
        "displayName": "HpcAdminMirror",
        "id": "61e10148-16a8-432a-b86d-ef620c3e48ef",
        "isEnabled": true,
        "description": "HpcAdminMirror",
        "value": "HpcAdminMirror"
        },
        {
        "allowedMemberTypes": [
            "User",
            "Application"
        ],
        "description": "HpcUsers",
        "displayName": "HpcUsers",
        "id": "91e10148-16a8-432a-b86d-ef620c3e48ef",
        "isEnabled": true,
        "value": "HpcUsers"
        }
    ],
    ```
7. <span data-ttu-id="299ec-147">Merhaba dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="299ec-147">Save hello file.</span></span> <span data-ttu-id="299ec-148">Merhaba Portalı'nda, ardından **yönetmek bildirim** > **karşıya bildirim**.</span><span class="sxs-lookup"><span data-stu-id="299ec-148">Then in hello portal, click **Manage Manifest** > **Upload Manifest**.</span></span> <span data-ttu-id="299ec-149">Ardından hello düzenlenen bildirimi karşıya yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="299ec-149">You can then upload hello edited manifest.</span></span>
8. <span data-ttu-id="299ec-150">Tıklatın **kullanıcılar**, bir kullanıcı seçin ve ardından **atamak**.</span><span class="sxs-lookup"><span data-stu-id="299ec-150">Click **Users**, select a user, and then click **Assign**.</span></span> <span data-ttu-id="299ec-151">Merhaba kullanılabilir roller (HpcUsers veya HpcAdminMirror) toohello kullanıcı birine atayın.</span><span class="sxs-lookup"><span data-stu-id="299ec-151">Assign one of hello available roles (HpcUsers or HpcAdminMirror) toohello user.</span></span> <span data-ttu-id="299ec-152">Merhaba dizinindeki ek kullanıcılar ile bu adımı yineleyin.</span><span class="sxs-lookup"><span data-stu-id="299ec-152">Repeat this step with additional users in hello directory.</span></span> <span data-ttu-id="299ec-153">Küme kullanıcılar hakkında bilgi için bkz: [küme kullanıcıları yönetme](https://technet.microsoft.com/library/ff919335(v=ws.11).aspx).</span><span class="sxs-lookup"><span data-stu-id="299ec-153">For background information about cluster users, see [Managing Cluster Users](https://technet.microsoft.com/library/ff919335(v=ws.11).aspx).</span></span>

   > [!NOTE] 
   > <span data-ttu-id="299ec-154">hello Azure Active Directory Önizleme dikey penceresinde hello kullanmanızı öneririz toomanage kullanıcılar, [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="299ec-154">toomanage users, we recommend using hello Azure Active Directory preview blade in hello [Azure portal](https://portal.azure.com).</span></span>
   >


## <a name="step-2-register-hello-hpc-cluster-client-with-your-azure-ad-tenant"></a><span data-ttu-id="299ec-155">2. adım: Azure AD kiracınıza hello HPC küme istemci Kaydet</span><span class="sxs-lookup"><span data-stu-id="299ec-155">Step 2: Register hello HPC cluster client with your Azure AD tenant</span></span>

1. <span data-ttu-id="299ec-156">İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="299ec-156">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="299ec-157">Tıklatın **Active Directory** hello soldaki menüden ve aboneliğinizi istenilen dizinde hello'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="299ec-157">Click **Active Directory** in hello left menu, and then click hello desired directory in your subscription.</span></span> <span data-ttu-id="299ec-158">İzni tooaccess kaynakları hello dizinde olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="299ec-158">You must have permission tooaccess resources in hello directory.</span></span>
3. <span data-ttu-id="299ec-159">Tıklatın **uygulamaları** > **Ekle**ve ardından **kuruluşumun geliştirmekte olduğu bir uygulama Ekle**.</span><span class="sxs-lookup"><span data-stu-id="299ec-159">Click **Applications** > **Add**, and then click **Add an application my organization is developing**.</span></span> <span data-ttu-id="299ec-160">Başlangıç Sihirbazı'nda bilgisinden hello girin:</span><span class="sxs-lookup"><span data-stu-id="299ec-160">Enter hello following information in hello wizard:</span></span>

    * <span data-ttu-id="299ec-161">**Ad** -HPCPackClusterClient</span><span class="sxs-lookup"><span data-stu-id="299ec-161">**Name** - HPCPackClusterClient</span></span>
    * <span data-ttu-id="299ec-162">**Tür** - seçin **yerel istemci uygulaması**</span><span class="sxs-lookup"><span data-stu-id="299ec-162">**Type** - Select **Native Client Application**</span></span>
    * <span data-ttu-id="299ec-163">**Yeniden yönlendirme URI'si** - `http://hpcclient`</span><span class="sxs-lookup"><span data-stu-id="299ec-163">**Redirect URI** - `http://hpcclient`</span></span>

4. <span data-ttu-id="299ec-164">Merhaba uygulama eklendikten sonra tıklatın **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="299ec-164">After hello app is added, click **Configure**.</span></span> <span data-ttu-id="299ec-165">Kopya hello **istemci kimliği** değer ve kaydedin.</span><span class="sxs-lookup"><span data-stu-id="299ec-165">Copy hello **Client ID** value and save it.</span></span> <span data-ttu-id="299ec-166">Bu daha sonra uygulamanızın yapılandırırken gerekir.</span><span class="sxs-lookup"><span data-stu-id="299ec-166">You need this later when configuring your application.</span></span>

5. <span data-ttu-id="299ec-167">İçinde **izinleri tooother uygulamaları**, tıklatın **uygulama Ekle**.</span><span class="sxs-lookup"><span data-stu-id="299ec-167">In **Permissions tooother applications**, click **Add Application**.</span></span> <span data-ttu-id="299ec-168">Arayın ve hello HpcPackClusterServer uygulama (1. adımda oluşturduğunuz) ekleyin.</span><span class="sxs-lookup"><span data-stu-id="299ec-168">Search and add hello  HpcPackClusterServer application (created in Step 1).</span></span>

6. <span data-ttu-id="299ec-169">Merhaba, **izinlere temsilci** açılan listesinde, select **erişim HpcClusterServer**.</span><span class="sxs-lookup"><span data-stu-id="299ec-169">In hello **Delegated Permissions** dropdown, select **Access HpcClusterServer**.</span></span> <span data-ttu-id="299ec-170">Daha sonra **Kaydet**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="299ec-170">Then click **Save**.</span></span>


## <a name="step-3-configure-hello-hpc-cluster"></a><span data-ttu-id="299ec-171">3. adım: hello HPC küme yapılandırma</span><span class="sxs-lookup"><span data-stu-id="299ec-171">Step 3: Configure hello HPC cluster</span></span>

1. <span data-ttu-id="299ec-172">Azure'da toohello HPC Pack 2016 baş düğüm bağlayın.</span><span class="sxs-lookup"><span data-stu-id="299ec-172">Connect toohello HPC Pack 2016 head node in Azure.</span></span>

2. <span data-ttu-id="299ec-173">HPC PowerShell'i başlatın.</span><span class="sxs-lookup"><span data-stu-id="299ec-173">Start HPC PowerShell.</span></span>

3. <span data-ttu-id="299ec-174">Merhaba aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="299ec-174">Run hello following command:</span></span>

    ```powershell

    Set-HpcClusterRegistry -SupportAAD true -AADInstance https://login.microsoftonline.com/ -AADAppName HpcClusterServer -AADTenant <your AAD tenant name> -AADClientAppId <client ID> -AADClientAppRedirectUri http://hpcclient
    ```
    <span data-ttu-id="299ec-175">Burada</span><span class="sxs-lookup"><span data-stu-id="299ec-175">where</span></span>

    * <span data-ttu-id="299ec-176">`AADTenant`Hello Azure AD Kiracı adı gibi belirtir`hpclocal.onmicrosoft.com`</span><span class="sxs-lookup"><span data-stu-id="299ec-176">`AADTenant` specifies hello Azure AD tenant name, such as `hpclocal.onmicrosoft.com`</span></span>
    * <span data-ttu-id="299ec-177">`AADClientAppId`2. adımda oluşturulan hello uygulaması Hello istemci Kimliğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="299ec-177">`AADClientAppId` specifies hello client ID for hello app created in Step 2.</span></span>

4. <span data-ttu-id="299ec-178">Merhaba HpcSchedulerStateful hizmetini yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="299ec-178">Restart hello HpcSchedulerStateful service.</span></span>

    <span data-ttu-id="299ec-179">Birden çok baş düğümü olan bir kümede hello baş düğüm tooswitch hello birincil çoğaltmadaki hello HpcSchedulerStateful hizmeti için PowerShell komutlarını aşağıdaki hello çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="299ec-179">In a cluster with multiple head nodes, you can run hello following PowerShell commands on hello head node tooswitch hello primary replica for hello HpcSchedulerStateful service:</span></span>

    ```powershell
    Connect-ServiceFabricCluster

    Move-ServiceFabricPrimaryReplica –ServiceName “fabric:/HpcApplication/SchedulerStatefulService”

    ```

## <a name="step-4-manage-and-submit-jobs-from-hello-client"></a><span data-ttu-id="299ec-180">4. adım: Yönetmek ve işleri hello istemciden gönderin</span><span class="sxs-lookup"><span data-stu-id="299ec-180">Step 4: Manage and submit jobs from hello client</span></span>

<span data-ttu-id="299ec-181">tooinstall hello HPC Pack istemci yardımcı programları, bilgisayarınızda Microsoft Download Center hello HPC Pack 2016 Kurulum dosyaları (tam yükleme) indirin.</span><span class="sxs-lookup"><span data-stu-id="299ec-181">tooinstall hello HPC Pack client utilities on your computer, download the HPC Pack 2016 setup files (full installation) from hello Microsoft Download Center.</span></span> <span data-ttu-id="299ec-182">Merhaba yükleme başladığınızda, hello Kurulum hello için seçeneği **HPC Pack istemci yardımcı programları**.</span><span class="sxs-lookup"><span data-stu-id="299ec-182">When you begin hello installation, choose hello setup option for hello **HPC Pack client utilities**.</span></span>

<span data-ttu-id="299ec-183">tooprepare hello istemci bilgisayar, yükleme sırasında kullanılan hello sertifikası [HPC Küme kurulumu](hpcpack-2016-cluster.md) hello istemci bilgisayarda.</span><span class="sxs-lookup"><span data-stu-id="299ec-183">tooprepare hello client computer, install hello certificate used during [HPC cluster setup](hpcpack-2016-cluster.md) on hello client computer.</span></span> <span data-ttu-id="299ec-184">Kullanım standart Windows sertifika yönetimi yordamları tooinstall hello ortak sertifika toohello **Sertifikalar – Geçerli kullanıcı** > **güvenilen kök sertifika yetkilileri** depolar.</span><span class="sxs-lookup"><span data-stu-id="299ec-184">Use standard Windows certificate management procedures tooinstall hello public certificate toohello **Certificates – Current user** > **Trusted Root Certification Authorities** store.</span></span> 

<span data-ttu-id="299ec-185">Şimdi hello HPC Pack komutları çalıştırmak veya da hello HPC Pack İş Yöneticisi GUI'sini toosubmit kullanın ve küme işleri hello Azure AD hesabı'nı kullanarak yönetin.</span><span class="sxs-lookup"><span data-stu-id="299ec-185">You can now run hello HPC Pack commands or use hello HPC Pack Job manager GUI toosubmit and manage cluster jobs by using hello Azure AD account.</span></span> <span data-ttu-id="299ec-186">İş gönderme seçenekleri için bkz: [gönderme HPC işleri tooan HPC paketi küme Azure'da](hpcpack-cluster-submit-jobs.md#step-3-run-test-jobs-on-the-cluster).</span><span class="sxs-lookup"><span data-stu-id="299ec-186">For job submission options, see [Submit HPC jobs tooan HPC Pack cluster in Azure](hpcpack-cluster-submit-jobs.md#step-3-run-test-jobs-on-the-cluster).</span></span>

> [!NOTE]
> <span data-ttu-id="299ec-187">Itanium tabanlı sistemler için tooconnect toohello HPC paketi küme azure'da hello için ilk kez çalıştığında, açılır pencereleri görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="299ec-187">When you try tooconnect toohello HPC Pack cluster in Azure for hello first time, a popup windows appears.</span></span> <span data-ttu-id="299ec-188">Azure AD kimlik bilgilerini toolog girin.</span><span class="sxs-lookup"><span data-stu-id="299ec-188">Enter your Azure AD credentials toolog in.</span></span> <span data-ttu-id="299ec-189">Merhaba belirteci sonra önbelleğe alınır.</span><span class="sxs-lookup"><span data-stu-id="299ec-189">hello token is then cached.</span></span> <span data-ttu-id="299ec-190">Kimlik doğrulaması değişiklikleri veya önbelleğe alınmış hello temizlenmediği sürece Azure kullanım hello sonraki bağlantıları toohello kümede belirteç önbelleğe alınmış.</span><span class="sxs-lookup"><span data-stu-id="299ec-190">Later connections toohello cluster in Azure use hello cached token unless authentication changes or hello cached is cleared.</span></span>
>
  
<span data-ttu-id="299ec-191">Örneğin, hello önceki adımları tamamladıktan sonra bir şirket içi istemci işlerden şu şekilde sorgulayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="299ec-191">For example, after completing hello previous steps, you can query for jobs from an on-premises client as follows:</span></span>

```powershell 
Get-HpcJob –State All –Scheduler https://<Azure load balancer DNS name> -Owner <Azure AD account>
```

## <a name="useful-cmdlets-for-job-submission-with-azure-ad-integration"></a><span data-ttu-id="299ec-192">Azure AD tümleştirmesiyle iş gönderme için kullanışlı cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="299ec-192">Useful cmdlets for job submission with Azure AD integration</span></span> 

### <a name="manage-hello-local-token-cache"></a><span data-ttu-id="299ec-193">Merhaba yerel belirteç önbelleği yönetme</span><span class="sxs-lookup"><span data-stu-id="299ec-193">Manage hello local token cache</span></span>

<span data-ttu-id="299ec-194">HPC Pack 2016 toomanage hello yerel belirteç önbelleği iki yeni HPC PowerShell cmdlet'leri sağlar.</span><span class="sxs-lookup"><span data-stu-id="299ec-194">HPC Pack 2016 provides two new HPC PowerShell cmdlets toomanage hello local token cache.</span></span> <span data-ttu-id="299ec-195">Bu cmdlet, işleri etkileşimsiz göndermek için faydalıdır.</span><span class="sxs-lookup"><span data-stu-id="299ec-195">These cmdlets are useful for submitting jobs non-interactively.</span></span> <span data-ttu-id="299ec-196">Aşağıdaki örnek hello bakın:</span><span class="sxs-lookup"><span data-stu-id="299ec-196">See hello following example:</span></span>

```powershell
Remove-HpcTokenCache

$SecurePassword = "<password>" | ConvertTo-SecureString -AsPlainText -Force

Set-HpcTokenCache -UserName <AADUsername> -Password $SecurePassword -scheduler https://<Azure load balancer DNS name> 
```

### <a name="set-hello-credentials-for-submitting-jobs-using-hello-azure-ad-account"></a><span data-ttu-id="299ec-197">Hello Azure AD hesabı kullanarak işleri göndermek için hello kimlik bilgilerini ayarlayın</span><span class="sxs-lookup"><span data-stu-id="299ec-197">Set hello credentials for submitting jobs using hello Azure AD account</span></span> 

<span data-ttu-id="299ec-198">Bazen, toorun hello iş hello HPC küme kullanıcı altında isteyebilirsiniz (bir etki alanı kullanıcısı olarak çalıştır etki alanına katılmış HPC Kümesi; hello baş düğümünde bir yerel kullanıcı olarak çalıştırılan bir etki alanına katılmış HPC Kümesi).</span><span class="sxs-lookup"><span data-stu-id="299ec-198">Sometimes, you may want toorun hello job under hello HPC cluster user (for a domain-joined HPC cluster, run as one domain user; for a non-domain-joined HPC cluster, run as one local user on hello head node).</span></span>

1. <span data-ttu-id="299ec-199">Aşağıdaki komutları tooset hello kimlik hello kullan:</span><span class="sxs-lookup"><span data-stu-id="299ec-199">Use hello following commands tooset hello credentials:</span></span>

    ```powershell
    $localUser = “<username>”

    $localUserPassword=”<password>”

    $secpasswd = ConvertTo-SecureString $localUserPassword -AsPlainText -Force

    $mycreds = New-Object System.Management.Automation.PSCredential ($localUser, $secpasswd)

    Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name>
    ```

2. <span data-ttu-id="299ec-200">Ardından aşağıdaki gibi hello işi gönderin.</span><span class="sxs-lookup"><span data-stu-id="299ec-200">Then submit hello job as follows.</span></span> <span data-ttu-id="299ec-201">Merhaba iş/görevi $localUser hello işlem düğümlerinde altında çalışır.</span><span class="sxs-lookup"><span data-stu-id="299ec-201">hello job/task runs under $localUser on hello compute nodes.</span></span>

    ```powershell
    $emptycreds = New-Object System.Management.Automation.PSCredential ($localUser, (new-object System.Security.SecureString))
    ...
    $job = New-HpcJob –Scheduler https://<Azure load balancer DNS name>

    Add-HpcTask -Job $job -CommandLine "ping localhost" -Scheduler https://<Azure load balancer DNS name>

    Submit-HpcJob -Job $job -Scheduler https://<Azure load balancer DNS name> -Credential $emptycreds
    ```
    
   <span data-ttu-id="299ec-202">Varsa `–Credential` ile belirtilmemiş `Submit-HpcJob`, hello iş veya görev Azure AD hesabının hello gibi bir yerel eşlenen kullanıcı altında çalışır.</span><span class="sxs-lookup"><span data-stu-id="299ec-202">If `–Credential` is not specified with `Submit-HpcJob`, hello job or task runs under a local mapped user as hello Azure AD account.</span></span> <span data-ttu-id="299ec-203">(Merhaba HPC küme hello aynı Azure AD hesabı toorun hello görev hello ad ile yerel bir kullanıcı oluşturur.)</span><span class="sxs-lookup"><span data-stu-id="299ec-203">(hello HPC cluster creates a local user with hello same name as hello Azure AD account toorun hello task.)</span></span>
    
3. <span data-ttu-id="299ec-204">Hello Azure AD hesabı için genişletilmiş veri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="299ec-204">Set extended data for hello Azure AD account.</span></span> <span data-ttu-id="299ec-205">Bu, bir MPI işi hello Azure AD hesabı kullanarak Linux düğümleri üzerinde çalışırken yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="299ec-205">This is useful when running an MPI job on Linux nodes using hello Azure AD account.</span></span>

   * <span data-ttu-id="299ec-206">Hello Azure AD hesabının kendisi için genişletilmiş veri kümesi</span><span class="sxs-lookup"><span data-stu-id="299ec-206">Set extended data for hello Azure AD account itself</span></span>

      ```powershell
      Set-HpcJobCredential -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data> -AadUser
      ```
      
   * <span data-ttu-id="299ec-207">Genişletilmiş veri kümesi ve HPC küme kullanıcı olarak çalıştırın</span><span class="sxs-lookup"><span data-stu-id="299ec-207">Set extended data and run as HPC cluster user</span></span>
   
      ```powershell
      Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data>
      ```

