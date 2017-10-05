---
title: "Azure Active Directory ile HPC paketi küme | Microsoft Docs"
description: "Azure HPC Pack 2016 kümede Azure Active Directory ile tümleştirme öğrenin"
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
ms.openlocfilehash: c5a06a9c810349b1bcce01c7f73563941a5af0ed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-an-hpc-pack-cluster-in-azure-using-azure-active-directory"></a><span data-ttu-id="202de-103">Azure Active Directory'yi kullanarak Azure HPC Pack kümede yönetme</span><span class="sxs-lookup"><span data-stu-id="202de-103">Manage an HPC Pack cluster in Azure using Azure Active Directory</span></span>
<span data-ttu-id="202de-104">[Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) ile tümleştirmeyi destekleyen [Azure Active Directory](../../active-directory/index.md) (Azure AD) Azure HPC Pack kümede dağıtmak Yöneticiler için.</span><span class="sxs-lookup"><span data-stu-id="202de-104">[Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) supports integration with [Azure Active Directory](../../active-directory/index.md) (Azure AD) for administrators who deploy an HPC Pack cluster in Azure.</span></span>



<span data-ttu-id="202de-105">Aşağıdaki yüksek düzey görevler için bu makaledeki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="202de-105">Follow the steps in this article for the following high level tasks:</span></span> 
* <span data-ttu-id="202de-106">HPC Pack kümenizi Azure AD kiracınıza el ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="202de-106">Manually integrate your HPC Pack cluster with your Azure AD tenant</span></span>
* <span data-ttu-id="202de-107">Yönetmek ve azure'da HPC Pack kümenizdeki işlerini zamanla</span><span class="sxs-lookup"><span data-stu-id="202de-107">Manage and schedule jobs in your HPC Pack cluster in Azure</span></span> 

<span data-ttu-id="202de-108">HPC Pack küme çözümünü Azure AD ile tümleştirme, diğer uygulamalar ve hizmetler tümleştirmek için standart adımları izler.</span><span class="sxs-lookup"><span data-stu-id="202de-108">Integrating an HPC Pack cluster solution with Azure AD follows standard steps to integrate other applications and services.</span></span> <span data-ttu-id="202de-109">Bu makale, Azure AD'de temel kullanıcı yönetimi ile bildiğinizi varsayar.</span><span class="sxs-lookup"><span data-stu-id="202de-109">This article assumes you are familiar with basic user management in Azure AD.</span></span> <span data-ttu-id="202de-110">Daha fazla bilgi ve arka plan için bkz: [Azure Active Directory belgelerindeki](../../active-directory/index.md) ve aşağıdaki bölümü.</span><span class="sxs-lookup"><span data-stu-id="202de-110">For more information and background, see the [Azure Active Directory documentation](../../active-directory/index.md) and the following section.</span></span>

## <a name="benefits-of-integration"></a><span data-ttu-id="202de-111">Tümleştirme yararları</span><span class="sxs-lookup"><span data-stu-id="202de-111">Benefits of integration</span></span>


<span data-ttu-id="202de-112">Azure Active Directory (Azure AD) olduğu bulut çözümleri çoklu oturum açma (SSO) erişimi sağlayan bir çok kiracılı bulut tabanlı dizin ve Kimlik Yönetimi Hizmeti.</span><span class="sxs-lookup"><span data-stu-id="202de-112">Azure Active Directory (Azure AD) is a multi-tenant cloud-based directory and identity management service that provides single sign-on (SSO) access to cloud solutions.</span></span>

<span data-ttu-id="202de-113">HPC Pack küme Azure AD ile tümleştirilmesi, aşağıdaki hedeflere ulaşmak yardımcı olabilir:</span><span class="sxs-lookup"><span data-stu-id="202de-113">Integration of an HPC Pack cluster with Azure AD can help you achieve the following goals:</span></span>

* <span data-ttu-id="202de-114">Geleneksel Active Directory etki alanı denetleyicisi HPC Pack kümeden kaldırın.</span><span class="sxs-lookup"><span data-stu-id="202de-114">Remove the traditional Active Directory domain controller from the HPC Pack cluster.</span></span> <span data-ttu-id="202de-115">Bu, bu, iş ve faturalamak dağıtım işlemi için gerekli değilse, küme koruma maliyetlerini azaltmaya yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="202de-115">This can help reduce the costs of maintaining the cluster if this is not necessary for your business, and speed-up the deployment process.</span></span>
* <span data-ttu-id="202de-116">Azure AD tarafından yapılmadan aşağıdaki yararları yararlanın:</span><span class="sxs-lookup"><span data-stu-id="202de-116">Leverage the following benefits that are brought by Azure AD:</span></span>
    *   <span data-ttu-id="202de-117">Çoklu oturum açma</span><span class="sxs-lookup"><span data-stu-id="202de-117">Single sign-on</span></span> 
    *   <span data-ttu-id="202de-118">Azure HPC paketi küme için bir yerel AD kimliği kullanma</span><span class="sxs-lookup"><span data-stu-id="202de-118">Using a local AD identity for the HPC Pack cluster in Azure</span></span> 

    ![Azure Active Directory ortamı](./media/hpcpack-cluster-active-directory/aad.png)


## <a name="prerequisites"></a><span data-ttu-id="202de-120">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="202de-120">Prerequisites</span></span>
* <span data-ttu-id="202de-121">**Azure sanal makinelerinde dağıtılan HPC Pack 2016 küme** - adımları için bkz: [Azure HPC Pack 2016 kümede dağıtmak](hpcpack-2016-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="202de-121">**HPC Pack 2016 cluster deployed in Azure virtual machines** - For steps, see [Deploy an HPC Pack 2016 cluster in Azure](hpcpack-2016-cluster.md).</span></span> <span data-ttu-id="202de-122">Baş düğüm DNS adını ve bu makaledeki adımları tamamlamak için bir Küme Yöneticisi kimlik bilgileri gerekir.</span><span class="sxs-lookup"><span data-stu-id="202de-122">You need the DNS name of the head node and the credentials of a cluster administrator to complete the steps in this article.</span></span>

  > [!NOTE]
  > <span data-ttu-id="202de-123">Azure Active Directory Tümleştirme HPC Pack HPC Pack 2016 önce sürümlerinde desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="202de-123">Azure Active Directory integration is not supported in versions of HPC Pack before HPC Pack 2016.</span></span>



* <span data-ttu-id="202de-124">**İstemci bilgisayar** -HPC Pack istemci yardımcı programları çalıştırmak için bir Windows veya Windows Server istemci bilgisayar gerekir.</span><span class="sxs-lookup"><span data-stu-id="202de-124">**Client computer** - You need a Windows or Windows Server client computer to  run HPC Pack client utilities.</span></span> <span data-ttu-id="202de-125">Yalnızca iş göndermek için HPC Pack web portalı veya REST API'yi kullanmak istiyorsanız, tercih ettiğiniz herhangi bir istemci bilgisayarı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="202de-125">If you only want to use the HPC Pack web portal or REST API to submit jobs, you can use any client computer of your choice.</span></span>

* <span data-ttu-id="202de-126">**HPC Pack istemci yardımcı programları** -HPC Pack istemci yardımcı programları Microsoft Download Center'dan gelen kullanılabilir boş yükleme paketini kullanarak istemci bilgisayara yükleyin.</span><span class="sxs-lookup"><span data-stu-id="202de-126">**HPC Pack client utilities** - Install the HPC Pack client utilities on the client computer, using the free installation package available from the Microsoft Download Center.</span></span>


## <a name="step-1-register-the-hpc-cluster-server-with-your-azure-ad-tenant"></a><span data-ttu-id="202de-127">1. adım: Azure AD kiracınıza HPC küme sunucusu kaydetme</span><span class="sxs-lookup"><span data-stu-id="202de-127">Step 1: Register the HPC cluster server with your Azure AD tenant</span></span>
1. <span data-ttu-id="202de-128">[Klasik Azure portalında](https://manage.windowsazure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="202de-128">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="202de-129">Tıklatın **Active Directory** soldaki menüde ve istenen dizin aboneliğinizde'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="202de-129">Click **Active Directory** in the left menu, and then click the desired directory in your subscription.</span></span> <span data-ttu-id="202de-130">Dizindeki kaynaklara erişim izni olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="202de-130">You must have permission to access resources in the directory.</span></span>
3. <span data-ttu-id="202de-131">Tıklatın **kullanıcılar**ve kullanıcı hesapları zaten oluşturuldu veya yapılandırılmış olmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="202de-131">Click **Users**, and make sure there are user accounts already created or configured.</span></span>
4. <span data-ttu-id="202de-132">Tıklatın **uygulamaları** > **Ekle**ve ardından **kuruluşumun geliştirmekte olduğu bir uygulama Ekle**.</span><span class="sxs-lookup"><span data-stu-id="202de-132">Click **Applications** > **Add**, and then click **Add an application my organization is developing**.</span></span> <span data-ttu-id="202de-133">Sihirbazı'nda aşağıdaki bilgileri girin:</span><span class="sxs-lookup"><span data-stu-id="202de-133">Enter the following information in the wizard:</span></span>
    * <span data-ttu-id="202de-134">**Ad** -HPCPackClusterServer</span><span class="sxs-lookup"><span data-stu-id="202de-134">**Name** - HPCPackClusterServer</span></span>
    * <span data-ttu-id="202de-135">**Tür** - seçin **Web uygulaması ve/veya Web API'si**</span><span class="sxs-lookup"><span data-stu-id="202de-135">**Type** - Select **Web Application and/or Web API**</span></span>
    * <span data-ttu-id="202de-136">**URL oturum açma**-varsayılan örnek için temel URL`https://hpcserver`</span><span class="sxs-lookup"><span data-stu-id="202de-136">**Sign-on URL**- The base URL for the sample, which is by default `https://hpcserver`</span></span>
    * <span data-ttu-id="202de-137">**Uygulama Kimliği URI'si** - `https://<Directory_name>/<application_name>`.</span><span class="sxs-lookup"><span data-stu-id="202de-137">**App ID URI** - `https://<Directory_name>/<application_name>`.</span></span> <span data-ttu-id="202de-138">Değiştir `<Directory_name`> Azure AD kiracınız, örneğin, tam adıyla `hpclocal.onmicrosoft.com`ve yerine `<application_name>` daha önce seçtiğiniz ada sahip.</span><span class="sxs-lookup"><span data-stu-id="202de-138">Replace `<Directory_name`> with the full name of your Azure AD tenant, for example, `hpclocal.onmicrosoft.com`, and replace `<application_name>` with the name you chose previously.</span></span>

5. <span data-ttu-id="202de-139">Uygulama eklendikten sonra tıklatın **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="202de-139">After the app is added, click **Configure**.</span></span> <span data-ttu-id="202de-140">Aşağıdaki özellikleri yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="202de-140">Configure the following properties:</span></span>
    * <span data-ttu-id="202de-141">Seçin **Evet** için **uygulamasıdır çok kiracılı**</span><span class="sxs-lookup"><span data-stu-id="202de-141">Select **Yes** for **Application is multi-tenant**</span></span>
    * <span data-ttu-id="202de-142">Seçin **Evet** için **uygulamaya erişmek için gerekli kullanıcı ataması**.</span><span class="sxs-lookup"><span data-stu-id="202de-142">Select **Yes** for **User assignment required to access app**.</span></span>

6. <span data-ttu-id="202de-143">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="202de-143">Click **Save**.</span></span> <span data-ttu-id="202de-144">Kaydetme tamamlandığında tıklayın **yönetmek bildirim**.</span><span class="sxs-lookup"><span data-stu-id="202de-144">When saving completes, click **Manage Manifest**.</span></span> <span data-ttu-id="202de-145">Bu eylem, uygulamanızın bildirim JavaScript nesne gösterimi (JSON) dosyası indirir.</span><span class="sxs-lookup"><span data-stu-id="202de-145">This action downloads your application’s manifest JavaScript object notation (JSON) file.</span></span> <span data-ttu-id="202de-146">İndirilen bildirimi bularak Düzenle `appRoles` ayarlama ve aşağıdaki uygulama rolü ekleme:</span><span class="sxs-lookup"><span data-stu-id="202de-146">Edit the downloaded manifest by locating the `appRoles` setting and adding the following application role:</span></span>
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
7. <span data-ttu-id="202de-147">Dosyayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="202de-147">Save the file.</span></span> <span data-ttu-id="202de-148">Portalda, ardından **yönetmek bildirim** > **karşıya bildirim**.</span><span class="sxs-lookup"><span data-stu-id="202de-148">Then in the portal, click **Manage Manifest** > **Upload Manifest**.</span></span> <span data-ttu-id="202de-149">Düzenlenen bildirimi ardından karşıya yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="202de-149">You can then upload the edited manifest.</span></span>
8. <span data-ttu-id="202de-150">Tıklatın **kullanıcılar**, bir kullanıcı seçin ve ardından **atamak**.</span><span class="sxs-lookup"><span data-stu-id="202de-150">Click **Users**, select a user, and then click **Assign**.</span></span> <span data-ttu-id="202de-151">Kullanılabilir roller (HpcUsers veya HpcAdminMirror) birini kullanıcıya atayın.</span><span class="sxs-lookup"><span data-stu-id="202de-151">Assign one of the available roles (HpcUsers or HpcAdminMirror) to the user.</span></span> <span data-ttu-id="202de-152">Dizinde ek kullanıcılar ile bu adımı yineleyin.</span><span class="sxs-lookup"><span data-stu-id="202de-152">Repeat this step with additional users in the directory.</span></span> <span data-ttu-id="202de-153">Küme kullanıcılar hakkında bilgi için bkz: [küme kullanıcıları yönetme](https://technet.microsoft.com/library/ff919335(v=ws.11).aspx).</span><span class="sxs-lookup"><span data-stu-id="202de-153">For background information about cluster users, see [Managing Cluster Users](https://technet.microsoft.com/library/ff919335(v=ws.11).aspx).</span></span>

   > [!NOTE] 
   > <span data-ttu-id="202de-154">Kullanıcıları yönetmek için Azure Active Directory Önizleme dikey penceresinde kullanmanızı öneririz [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="202de-154">To manage users, we recommend using the Azure Active Directory preview blade in the [Azure portal](https://portal.azure.com).</span></span>
   >


## <a name="step-2-register-the-hpc-cluster-client-with-your-azure-ad-tenant"></a><span data-ttu-id="202de-155">2. adım: Azure AD kiracınıza HPC küme istemci Kaydet</span><span class="sxs-lookup"><span data-stu-id="202de-155">Step 2: Register the HPC cluster client with your Azure AD tenant</span></span>

1. <span data-ttu-id="202de-156">[Klasik Azure portalında](https://manage.windowsazure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="202de-156">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="202de-157">Tıklatın **Active Directory** soldaki menüde ve istenen dizin aboneliğinizde'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="202de-157">Click **Active Directory** in the left menu, and then click the desired directory in your subscription.</span></span> <span data-ttu-id="202de-158">Dizindeki kaynaklara erişim izni olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="202de-158">You must have permission to access resources in the directory.</span></span>
3. <span data-ttu-id="202de-159">Tıklatın **uygulamaları** > **Ekle**ve ardından **kuruluşumun geliştirmekte olduğu bir uygulama Ekle**.</span><span class="sxs-lookup"><span data-stu-id="202de-159">Click **Applications** > **Add**, and then click **Add an application my organization is developing**.</span></span> <span data-ttu-id="202de-160">Sihirbazı'nda aşağıdaki bilgileri girin:</span><span class="sxs-lookup"><span data-stu-id="202de-160">Enter the following information in the wizard:</span></span>

    * <span data-ttu-id="202de-161">**Ad** -HPCPackClusterClient</span><span class="sxs-lookup"><span data-stu-id="202de-161">**Name** - HPCPackClusterClient</span></span>
    * <span data-ttu-id="202de-162">**Tür** - seçin **yerel istemci uygulaması**</span><span class="sxs-lookup"><span data-stu-id="202de-162">**Type** - Select **Native Client Application**</span></span>
    * <span data-ttu-id="202de-163">**Yeniden yönlendirme URI'si** - `http://hpcclient`</span><span class="sxs-lookup"><span data-stu-id="202de-163">**Redirect URI** - `http://hpcclient`</span></span>

4. <span data-ttu-id="202de-164">Uygulama eklendikten sonra tıklatın **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="202de-164">After the app is added, click **Configure**.</span></span> <span data-ttu-id="202de-165">Kopya **istemci kimliği** değer ve kaydedin.</span><span class="sxs-lookup"><span data-stu-id="202de-165">Copy the **Client ID** value and save it.</span></span> <span data-ttu-id="202de-166">Bu daha sonra uygulamanızın yapılandırırken gerekir.</span><span class="sxs-lookup"><span data-stu-id="202de-166">You need this later when configuring your application.</span></span>

5. <span data-ttu-id="202de-167">İçinde **diğer uygulamalara izinler**, tıklatın **uygulama Ekle**.</span><span class="sxs-lookup"><span data-stu-id="202de-167">In **Permissions to other applications**, click **Add Application**.</span></span> <span data-ttu-id="202de-168">Arayın ve (1. adımda oluşturduğunuz) HpcPackClusterServer uygulama ekleyin.</span><span class="sxs-lookup"><span data-stu-id="202de-168">Search and add the  HpcPackClusterServer application (created in Step 1).</span></span>

6. <span data-ttu-id="202de-169">İçinde **izinlere temsilci** açılan listesinde, select **erişim HpcClusterServer**.</span><span class="sxs-lookup"><span data-stu-id="202de-169">In the **Delegated Permissions** dropdown, select **Access HpcClusterServer**.</span></span> <span data-ttu-id="202de-170">Daha sonra **Kaydet**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="202de-170">Then click **Save**.</span></span>


## <a name="step-3-configure-the-hpc-cluster"></a><span data-ttu-id="202de-171">3. adım: HPC küme yapılandırma</span><span class="sxs-lookup"><span data-stu-id="202de-171">Step 3: Configure the HPC cluster</span></span>

1. <span data-ttu-id="202de-172">Azure HPC Pack 2016 baş düğümünde bağlayın.</span><span class="sxs-lookup"><span data-stu-id="202de-172">Connect to the HPC Pack 2016 head node in Azure.</span></span>

2. <span data-ttu-id="202de-173">HPC PowerShell'i başlatın.</span><span class="sxs-lookup"><span data-stu-id="202de-173">Start HPC PowerShell.</span></span>

3. <span data-ttu-id="202de-174">Şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="202de-174">Run the following command:</span></span>

    ```powershell

    Set-HpcClusterRegistry -SupportAAD true -AADInstance https://login.microsoftonline.com/ -AADAppName HpcClusterServer -AADTenant <your AAD tenant name> -AADClientAppId <client ID> -AADClientAppRedirectUri http://hpcclient
    ```
    <span data-ttu-id="202de-175">Burada</span><span class="sxs-lookup"><span data-stu-id="202de-175">where</span></span>

    * <span data-ttu-id="202de-176">`AADTenant`Azure AD Kiracı adı gibi belirtir`hpclocal.onmicrosoft.com`</span><span class="sxs-lookup"><span data-stu-id="202de-176">`AADTenant` specifies the Azure AD tenant name, such as `hpclocal.onmicrosoft.com`</span></span>
    * <span data-ttu-id="202de-177">`AADClientAppId`2. adımda oluşturduğunuz uygulama istemci Kimliğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="202de-177">`AADClientAppId` specifies the client ID for the app created in Step 2.</span></span>

4. <span data-ttu-id="202de-178">HpcSchedulerStateful hizmetini yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="202de-178">Restart the HpcSchedulerStateful service.</span></span>

    <span data-ttu-id="202de-179">Birden çok baş düğümü olan bir kümede baş düğüm birincil çoğaltma HpcSchedulerStateful hizmeti için geçiş yapmak için aşağıdaki PowerShell komutları çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="202de-179">In a cluster with multiple head nodes, you can run the following PowerShell commands on the head node to switch the primary replica for the HpcSchedulerStateful service:</span></span>

    ```powershell
    Connect-ServiceFabricCluster

    Move-ServiceFabricPrimaryReplica –ServiceName “fabric:/HpcApplication/SchedulerStatefulService”

    ```

## <a name="step-4-manage-and-submit-jobs-from-the-client"></a><span data-ttu-id="202de-180">Adım 4: Yönetmek ve istemciden işleri gönderme</span><span class="sxs-lookup"><span data-stu-id="202de-180">Step 4: Manage and submit jobs from the client</span></span>

<span data-ttu-id="202de-181">HPC Pack istemci yardımcı programları bilgisayarınıza yüklemek için Microsoft Download Center'dan gelen HPC Pack 2016 Kurulum dosyaları (tam yükleme) indirin.</span><span class="sxs-lookup"><span data-stu-id="202de-181">To install the HPC Pack client utilities on your computer, download the HPC Pack 2016 setup files (full installation) from the Microsoft Download Center.</span></span> <span data-ttu-id="202de-182">Yüklemeye başlamak için kurulum seçeneğini seçin **HPC Pack istemci yardımcı programları**.</span><span class="sxs-lookup"><span data-stu-id="202de-182">When you begin the installation, choose the setup option for the **HPC Pack client utilities**.</span></span>

<span data-ttu-id="202de-183">Yükleme sırasında kullanılan sertifika istemci bilgisayarı hazırlamak için [HPC Küme kurulumu](hpcpack-2016-cluster.md) istemci bilgisayardaki.</span><span class="sxs-lookup"><span data-stu-id="202de-183">To prepare the client computer, install the certificate used during [HPC cluster setup](hpcpack-2016-cluster.md) on the client computer.</span></span> <span data-ttu-id="202de-184">Ortak sertifikayı yüklemek için standart Windows sertifika yönetimi yordamları kullanın **Sertifikalar – Geçerli kullanıcı** > **güvenilen kök sertifika yetkilileri** depolar.</span><span class="sxs-lookup"><span data-stu-id="202de-184">Use standard Windows certificate management procedures to install the public certificate to the **Certificates – Current user** > **Trusted Root Certification Authorities** store.</span></span> 

<span data-ttu-id="202de-185">Şimdi, HPC Pack komutları çalıştırmak veya HPC Pack İş Yöneticisi'ni GUI göndermek ve Azure AD hesabının kullanarak küme işlerini yönetmek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="202de-185">You can now run the HPC Pack commands or use the HPC Pack Job manager GUI to submit and manage cluster jobs by using the Azure AD account.</span></span> <span data-ttu-id="202de-186">İş gönderme seçenekleri için bkz: [bir HPC paketi için gönderme HPC işleri küme Azure'da](hpcpack-cluster-submit-jobs.md#step-3-run-test-jobs-on-the-cluster).</span><span class="sxs-lookup"><span data-stu-id="202de-186">For job submission options, see [Submit HPC jobs to an HPC Pack cluster in Azure](hpcpack-cluster-submit-jobs.md#step-3-run-test-jobs-on-the-cluster).</span></span>

> [!NOTE]
> <span data-ttu-id="202de-187">İlk olarak Azure HPC Pack kümede bağlanmaya çalıştığında, açılır pencereleri görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="202de-187">When you try to connect to the HPC Pack cluster in Azure for the first time, a popup windows appears.</span></span> <span data-ttu-id="202de-188">Oturum açmak için Azure AD kimlik bilgilerinizi girin.</span><span class="sxs-lookup"><span data-stu-id="202de-188">Enter your Azure AD credentials to log in.</span></span> <span data-ttu-id="202de-189">Belirteç sonra önbelleğe alınır.</span><span class="sxs-lookup"><span data-stu-id="202de-189">The token is then cached.</span></span> <span data-ttu-id="202de-190">Kimlik doğrulaması değişiklikleri veya önbelleğe alınmış temizlenmediği sürece Azure kümedeki sonraki bağlantılar önbelleğe alınmış belirteci kullanın.</span><span class="sxs-lookup"><span data-stu-id="202de-190">Later connections to the cluster in Azure use the cached token unless authentication changes or the cached is cleared.</span></span>
>
  
<span data-ttu-id="202de-191">Örneğin, yukarıdaki adımları tamamladıktan sonra bir şirket içi istemci işlerden şu şekilde sorgulayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="202de-191">For example, after completing the previous steps, you can query for jobs from an on-premises client as follows:</span></span>

```powershell 
Get-HpcJob –State All –Scheduler https://<Azure load balancer DNS name> -Owner <Azure AD account>
```

## <a name="useful-cmdlets-for-job-submission-with-azure-ad-integration"></a><span data-ttu-id="202de-192">Azure AD tümleştirmesiyle iş gönderme için kullanışlı cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="202de-192">Useful cmdlets for job submission with Azure AD integration</span></span> 

### <a name="manage-the-local-token-cache"></a><span data-ttu-id="202de-193">Yerel belirteç önbelleği yönetme</span><span class="sxs-lookup"><span data-stu-id="202de-193">Manage the local token cache</span></span>

<span data-ttu-id="202de-194">HPC Pack 2016 yerel belirteç önbelleği yönetmek için iki yeni HPC PowerShell cmdlet'lerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="202de-194">HPC Pack 2016 provides two new HPC PowerShell cmdlets to manage the local token cache.</span></span> <span data-ttu-id="202de-195">Bu cmdlet, işleri etkileşimsiz göndermek için faydalıdır.</span><span class="sxs-lookup"><span data-stu-id="202de-195">These cmdlets are useful for submitting jobs non-interactively.</span></span> <span data-ttu-id="202de-196">Aşağıdaki örneğe bakın:</span><span class="sxs-lookup"><span data-stu-id="202de-196">See the following example:</span></span>

```powershell
Remove-HpcTokenCache

$SecurePassword = "<password>" | ConvertTo-SecureString -AsPlainText -Force

Set-HpcTokenCache -UserName <AADUsername> -Password $SecurePassword -scheduler https://<Azure load balancer DNS name> 
```

### <a name="set-the-credentials-for-submitting-jobs-using-the-azure-ad-account"></a><span data-ttu-id="202de-197">Azure AD hesabının kullanarak işleri göndermek için kimlik bilgilerini ayarlayın</span><span class="sxs-lookup"><span data-stu-id="202de-197">Set the credentials for submitting jobs using the Azure AD account</span></span> 

<span data-ttu-id="202de-198">Bazı durumlarda, işi HPC küme kullanıcıdan (çalıştıran bir etki alanı kullanıcısı olarak; baş düğümünde bir yerel kullanıcı olarak çalıştırılan bir etki alanına katılmış HPC Kümesi için bir etki alanına katılmış HPC küme) altında çalıştırmak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="202de-198">Sometimes, you may want to run the job under the HPC cluster user (for a domain-joined HPC cluster, run as one domain user; for a non-domain-joined HPC cluster, run as one local user on the head node).</span></span>

1. <span data-ttu-id="202de-199">Kimlik bilgilerini ayarlamak için aşağıdaki komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="202de-199">Use the following commands to set the credentials:</span></span>

    ```powershell
    $localUser = “<username>”

    $localUserPassword=”<password>”

    $secpasswd = ConvertTo-SecureString $localUserPassword -AsPlainText -Force

    $mycreds = New-Object System.Management.Automation.PSCredential ($localUser, $secpasswd)

    Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name>
    ```

2. <span data-ttu-id="202de-200">Ardından işi şu şekilde gönderin.</span><span class="sxs-lookup"><span data-stu-id="202de-200">Then submit the job as follows.</span></span> <span data-ttu-id="202de-201">İş/görevi $localUser altında işlem düğümlerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="202de-201">The job/task runs under $localUser on the compute nodes.</span></span>

    ```powershell
    $emptycreds = New-Object System.Management.Automation.PSCredential ($localUser, (new-object System.Security.SecureString))
    ...
    $job = New-HpcJob –Scheduler https://<Azure load balancer DNS name>

    Add-HpcTask -Job $job -CommandLine "ping localhost" -Scheduler https://<Azure load balancer DNS name>

    Submit-HpcJob -Job $job -Scheduler https://<Azure load balancer DNS name> -Credential $emptycreds
    ```
    
   <span data-ttu-id="202de-202">Varsa `–Credential` ile belirtilmemiş `Submit-HpcJob`, iş veya görevi yerel eşlenen kullanıcı olarak Azure AD hesabının altında çalışır.</span><span class="sxs-lookup"><span data-stu-id="202de-202">If `–Credential` is not specified with `Submit-HpcJob`, the job or task runs under a local mapped user as the Azure AD account.</span></span> <span data-ttu-id="202de-203">(HPC küme görevi çalıştırmak için Azure AD hesabının aynı ada sahip yerel bir kullanıcı oluşturur.)</span><span class="sxs-lookup"><span data-stu-id="202de-203">(The HPC cluster creates a local user with the same name as the Azure AD account to run the task.)</span></span>
    
3. <span data-ttu-id="202de-204">Azure AD hesabı için genişletilmiş veri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="202de-204">Set extended data for the Azure AD account.</span></span> <span data-ttu-id="202de-205">Bu, bir MPI işi Azure AD hesabının kullanarak Linux düğümleri üzerinde çalışırken yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="202de-205">This is useful when running an MPI job on Linux nodes using the Azure AD account.</span></span>

   * <span data-ttu-id="202de-206">Azure AD hesabı için genişletilmiş veri kümesi</span><span class="sxs-lookup"><span data-stu-id="202de-206">Set extended data for the Azure AD account itself</span></span>

      ```powershell
      Set-HpcJobCredential -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data> -AadUser
      ```
      
   * <span data-ttu-id="202de-207">Genişletilmiş veri kümesi ve HPC küme kullanıcı olarak çalıştırın</span><span class="sxs-lookup"><span data-stu-id="202de-207">Set extended data and run as HPC cluster user</span></span>
   
      ```powershell
      Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data>
      ```

