---
title: "Azure Otomasyonu DSC ile çalışmaya başlama | Microsoft Docs"
description: "Açıklama ve en yaygın görevleri de Azure Otomasyonu istenen durum yapılandırması (DSC) örnekleri"
services: automation
documentationcenter: na
author: eslesar
manager: carmonm
editor: tysonn
ms.assetid: a3816593-70a3-403b-9a43-d5555fd2cee2
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: na
ms.date: 11/21/2016
ms.author: magoedte;eslesar
ms.openlocfilehash: 8a10d961ad7c107c68b57c64ee6c88544ff8832b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-azure-automation-dsc"></a><span data-ttu-id="306e1-103">Azure Otomasyonu DSC ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="306e1-103">Getting started with Azure Automation DSC</span></span>
<span data-ttu-id="306e1-104">Bu konu ile Azure Otomasyonu istenen durum yapılandırması (oluşturma, alma ve yapılandırmaları, onboarding makineleri yönetmek için derleme ve raporları görüntüleme gibi DSC), en yaygın görevlerin nasıl yapılacağını açıklar.</span><span class="sxs-lookup"><span data-stu-id="306e1-104">This topic explains how to do the most common tasks with Azure Automation Desired State Configuration (DSC), such as creating, importing, and compiling configurations, onboarding machines to manage, and viewing reports.</span></span> <span data-ttu-id="306e1-105">Hangi Azure Otomasyonu DSC genel bir bakış için bkz: [Azure Automation DSC genel bakış](automation-dsc-overview.md).</span><span class="sxs-lookup"><span data-stu-id="306e1-105">For an overview of what Azure Automation DSC is, see [Azure Automation DSC Overview](automation-dsc-overview.md).</span></span> <span data-ttu-id="306e1-106">DSC belgeler için bkz: [Windows PowerShell istenen durum yapılandırması genel bakış](https://msdn.microsoft.com/PowerShell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="306e1-106">For DSC documentation, see [Windows PowerShell Desired State Configuration Overview](https://msdn.microsoft.com/PowerShell/dsc/overview).</span></span>

<span data-ttu-id="306e1-107">Bu konu Azure Otomasyonu DSC kullanarak adım adım yönergeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="306e1-107">This topic provides a step-by-step guide to using Azure Automation DSC.</span></span> <span data-ttu-id="306e1-108">Zaten bu konuda açıklanan adımları izleyerek olmadan ayarlanmış bir örnek ortamı istiyorsanız kullanabileceğiniz [aşağıdaki ARM şablonu](https://github.com/azureautomation/automation-packs/tree/master/102-sample-automation-setup).</span><span class="sxs-lookup"><span data-stu-id="306e1-108">If you want a sample environment that is already set up without following the steps described in this topic, you can use [the following ARM template](https://github.com/azureautomation/automation-packs/tree/master/102-sample-automation-setup).</span></span> <span data-ttu-id="306e1-109">Bu şablon tamamlanmış bir Azure Otomasyonu DSC ortam, Azure Otomasyonu DSC tarafından yönetilen bir Azure VM dahil olmak üzere ayarlar.</span><span class="sxs-lookup"><span data-stu-id="306e1-109">This template sets up a completed Azure Automation DSC environment, including an Azure VM that is managed by Azure Automation DSC.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="306e1-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="306e1-110">Prerequisites</span></span>
<span data-ttu-id="306e1-111">Bu konudaki örnekler tamamlamak için aşağıdakiler gereklidir:</span><span class="sxs-lookup"><span data-stu-id="306e1-111">To complete the examples in this topic, the following are required:</span></span>

* <span data-ttu-id="306e1-112">Bir Azure Otomasyonu hesabı.</span><span class="sxs-lookup"><span data-stu-id="306e1-112">An Azure Automation account.</span></span> <span data-ttu-id="306e1-113">Bir Azure Automation farklı çalıştır hesabı oluşturma ile ilgili yönergeler için bkz: [Azure farklı çalıştır hesabını](automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="306e1-113">For instructions on creating an Azure Automation Run As account, see [Azure Run As Account](automation-sec-configure-azure-runas-account.md).</span></span>
* <span data-ttu-id="306e1-114">Bir Azure Kaynak Yöneticisi'ni VM (Klasik değil) Windows Server 2008 R2 çalıştıran veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="306e1-114">An Azure Resource Manager VM (not Classic) running Windows Server 2008 R2 or later.</span></span> <span data-ttu-id="306e1-115">Bir VM oluşturma ile ilgili yönergeler için bkz: [Azure portalında, ilk Windows sanal makine oluşturma](../virtual-machines/virtual-machines-windows-hero-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="306e1-115">For instructions on creating a VM, see [Create your first Windows virtual machine in the Azure portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md)</span></span>

## <a name="creating-a-dsc-configuration"></a><span data-ttu-id="306e1-116">DSC yapılandırması oluşturma</span><span class="sxs-lookup"><span data-stu-id="306e1-116">Creating a DSC configuration</span></span>
<span data-ttu-id="306e1-117">Basit bir oluşturacağız [DSC Yapılandırması](https://msdn.microsoft.com/powershell/dsc/configurations) varlığının veya yokluğunun sağlar **Web sunucusu** Windows özelliği (düğümler nasıl atadığınız bağlı olarak IIS).</span><span class="sxs-lookup"><span data-stu-id="306e1-117">We will create a simple [DSC configuration](https://msdn.microsoft.com/powershell/dsc/configurations) that ensures either the presence or absence of the **Web-Server** Windows Feature (IIS), depending on how you assign nodes.</span></span>

1. <span data-ttu-id="306e1-118">Windows PowerShell ISE (veya herhangi bir metin düzenleyicisi) başlatın.</span><span class="sxs-lookup"><span data-stu-id="306e1-118">Start the Windows PowerShell ISE (or any text editor).</span></span>
2. <span data-ttu-id="306e1-119">Aşağıdaki metni yazın:</span><span class="sxs-lookup"><span data-stu-id="306e1-119">Type the following text:</span></span>
   
    ```powershell
    configuration TestConfig
    {
        Node WebServer
        {
            WindowsFeature IIS
            {
                Ensure               = 'Present'
                Name                 = 'Web-Server'
                IncludeAllSubFeature = $true
   
            }
        }
   
        Node NotWebServer
        {
            WindowsFeature IIS
            {
                Ensure               = 'Absent'
                Name                 = 'Web-Server'
   
            }
        }
        }
    ```
3. <span data-ttu-id="306e1-120">Dosyayı Farklı Kaydet `TestConfig.ps1`.</span><span class="sxs-lookup"><span data-stu-id="306e1-120">Save the file as `TestConfig.ps1`.</span></span>

<span data-ttu-id="306e1-121">Bu yapılandırma bir kaynak her düğümü blok çağırır [WindowsFeature kaynak](https://msdn.microsoft.com/powershell/dsc/windowsfeatureresource), varlığı veya yokluğuna göre sağlar **Web sunucusu** özelliği.</span><span class="sxs-lookup"><span data-stu-id="306e1-121">This configuration calls one resource in each node block, the [WindowsFeature resource](https://msdn.microsoft.com/powershell/dsc/windowsfeatureresource), that ensures either the presence or absence of the **Web-Server** feature.</span></span>

## <a name="importing-a-configuration-into-azure-automation"></a><span data-ttu-id="306e1-122">Bir yapılandırma Azure Automation'a içeri aktarma</span><span class="sxs-lookup"><span data-stu-id="306e1-122">Importing a configuration into Azure Automation</span></span>
<span data-ttu-id="306e1-123">Ardından, biz yapılandırmayı Otomasyon dikkate almak.</span><span class="sxs-lookup"><span data-stu-id="306e1-123">Next, we'll import the configuration into the Automation account.</span></span>

1. <span data-ttu-id="306e1-124">[Azure Portal](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="306e1-124">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="306e1-125">Hub menüsünde **tüm kaynakları** ve ardından Otomasyon hesabınızın adını.</span><span class="sxs-lookup"><span data-stu-id="306e1-125">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="306e1-126">Üzerinde **Otomasyon hesabı** dikey penceresinde tıklatın **DSC yapılandırmaları**.</span><span class="sxs-lookup"><span data-stu-id="306e1-126">On the **Automation account** blade, click **DSC Configurations**.</span></span>
4. <span data-ttu-id="306e1-127">Üzerinde **DSC yapılandırmaları** dikey penceresinde tıklatın **bir yapılandırma eklemek**.</span><span class="sxs-lookup"><span data-stu-id="306e1-127">On the **DSC Configurations** blade, click **Add a configuration**.</span></span>
5. <span data-ttu-id="306e1-128">Üzerinde **alma Yapılandırması** dikey penceresinde, Gözat ' `TestConfig.ps1` dosyayı bilgisayarınıza.</span><span class="sxs-lookup"><span data-stu-id="306e1-128">On the **Import Configuration** blade, browse to the `TestConfig.ps1` file on your computer.</span></span>
   
    ![Ekran görüntüsü ** alma yapılandırma ** dikey penceresi](./media/automation-dsc-getting-started/AddConfig.png)
6. <span data-ttu-id="306e1-130">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="306e1-130">Click **OK**.</span></span>

## <a name="viewing-a-configuration-in-azure-automation"></a><span data-ttu-id="306e1-131">Azure Otomasyonu'nda bir yapılandırmayı görüntüleme</span><span class="sxs-lookup"><span data-stu-id="306e1-131">Viewing a configuration in Azure Automation</span></span>
<span data-ttu-id="306e1-132">Bir yapılandırma içe aktardıktan sonra Azure Portalı'nda görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="306e1-132">After you have imported a configuration, you can view it in the Azure portal.</span></span>

1. <span data-ttu-id="306e1-133">[Azure Portal](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="306e1-133">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="306e1-134">Hub menüsünde **tüm kaynakları** ve ardından Otomasyon hesabınızın adını.</span><span class="sxs-lookup"><span data-stu-id="306e1-134">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="306e1-135">Üzerinde **Otomasyon hesabı** dikey penceresinde tıklatın **DSC yapılandırmaları**</span><span class="sxs-lookup"><span data-stu-id="306e1-135">On the **Automation account** blade, click **DSC Configurations**</span></span>
4. <span data-ttu-id="306e1-136">Üzerinde **DSC yapılandırmaları** dikey penceresinde tıklatın **TestConfig** (Bu önceki yordamda içeri aktardığınız yapılandırma adıdır).</span><span class="sxs-lookup"><span data-stu-id="306e1-136">On the **DSC Configurations** blade, click **TestConfig** (this is the name of the configuration you imported in the previous procedure).</span></span>
5. <span data-ttu-id="306e1-137">Üzerinde **TestConfig yapılandırma** dikey penceresinde tıklatın **yapılandırma kaynağı görüntüle**.</span><span class="sxs-lookup"><span data-stu-id="306e1-137">On the **TestConfig Configuration** blade, click **View configuration source**.</span></span>
   
    ![TestConfig yapılandırma dikey penceresinin ekran görüntüsü](./media/automation-dsc-getting-started/ViewConfigSource.png)
   
    <span data-ttu-id="306e1-139">A **TestConfig yapılandırma kaynağı** dikey penceresi açılır ve yapılandırması için PowerShell kodu görüntüleme.</span><span class="sxs-lookup"><span data-stu-id="306e1-139">A **TestConfig Configuration source** blade opens, displaying the PowerShell code for the configuration.</span></span>

## <a name="compiling-a-configuration-in-azure-automation"></a><span data-ttu-id="306e1-140">Bir Azure Otomasyonu yapılandırmasında derleme</span><span class="sxs-lookup"><span data-stu-id="306e1-140">Compiling a configuration in Azure Automation</span></span>
<span data-ttu-id="306e1-141">Bir düğüme istenilen durumu uygulayabilmeniz için önce bu duruma tanımlama DSC yapılandırması bir veya daha fazla düğüm yapılandırmaları (MOF belge) derlenmiş ve gerekir Automation DSC çekme sunucusuna yerleştirilen.</span><span class="sxs-lookup"><span data-stu-id="306e1-141">Before you can apply a desired state to a node, a DSC configuration defining that state must be compiled into one or more node configurations (MOF document), and placed on the Automation DSC Pull Server.</span></span> <span data-ttu-id="306e1-142">Azure Otomasyonu DSC yapılandırmalarında derleme daha ayrıntılı açıklaması için bkz: [Azure Otomasyonu DSC yapılandırmalarında derleme](automation-dsc-compile.md).</span><span class="sxs-lookup"><span data-stu-id="306e1-142">For a more detailed description of compiling configurations in Azure Automation DSC, see [Compiling configurations in Azure Automation DSC](automation-dsc-compile.md).</span></span> <span data-ttu-id="306e1-143">Derleme yapılandırmaları hakkında daha fazla bilgi için bkz: [DSC yapılandırmaları](https://msdn.microsoft.com/PowerShell/DSC/configurations).</span><span class="sxs-lookup"><span data-stu-id="306e1-143">For more information about compiling configurations, see [DSC Configurations](https://msdn.microsoft.com/PowerShell/DSC/configurations).</span></span>

1. <span data-ttu-id="306e1-144">[Azure Portal](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="306e1-144">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="306e1-145">Hub menüsünde **tüm kaynakları** ve ardından Otomasyon hesabınızın adını.</span><span class="sxs-lookup"><span data-stu-id="306e1-145">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="306e1-146">Üzerinde **Otomasyon hesabı** dikey penceresinde tıklatın **DSC yapılandırmaları**</span><span class="sxs-lookup"><span data-stu-id="306e1-146">On the **Automation account** blade, click **DSC Configurations**</span></span>
4. <span data-ttu-id="306e1-147">Üzerinde **DSC yapılandırmaları** dikey penceresinde tıklatın **TestConfig** (daha önce içe aktarılan yapılandırma adı).</span><span class="sxs-lookup"><span data-stu-id="306e1-147">On the **DSC Configurations** blade, click **TestConfig** (the name of the previously imported configuration).</span></span>
5. <span data-ttu-id="306e1-148">Üzerinde **TestConfig yapılandırma** dikey penceresinde tıklatın **derleme**ve ardından **Evet**.</span><span class="sxs-lookup"><span data-stu-id="306e1-148">On the **TestConfig Configuration** blade, click **Compile**, and then click **Yes**.</span></span> <span data-ttu-id="306e1-149">Bu derleme işi başlatır.</span><span class="sxs-lookup"><span data-stu-id="306e1-149">This starts a compilation job.</span></span>
   
    ![Derleme düğmesi vurgulama TestConfig yapılandırma dikey penceresinin ekran görüntüsü](./media/automation-dsc-getting-started/CompileConfig.png)

> [!NOTE]
> <span data-ttu-id="306e1-151">Bir Azure Otomasyonu yapılandırmasında derlerken çekme sunucusuna otomatik olarak tüm oluşturulan düğüm yapılandırması MOF dosyalarından dağıtır.</span><span class="sxs-lookup"><span data-stu-id="306e1-151">When you compile a configuration in Azure Automation, it automatically deploys any created node configuration MOFs to the pull server.</span></span>
> 
> 

## <a name="viewing-a-compilation-job"></a><span data-ttu-id="306e1-152">Derleme işi görüntüleme</span><span class="sxs-lookup"><span data-stu-id="306e1-152">Viewing a compilation job</span></span>
<span data-ttu-id="306e1-153">Bir derleme başlattıktan sonra içinde görüntüleyebilirsiniz **derleme işleri** parçasında **yapılandırma** dikey.</span><span class="sxs-lookup"><span data-stu-id="306e1-153">After you start a compilation, you can view it in the **Compilation jobs** tile in the **Configuration** blade.</span></span> <span data-ttu-id="306e1-154">**Derleme işleri** döşeme şu anda çalışan gösterir, tamamlandı ve işleri başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="306e1-154">The **Compilation jobs** tile shows currently running, completed, and failed jobs.</span></span> <span data-ttu-id="306e1-155">Bir derleme iş dikey penceresi açtığınızda, herhangi bir hata veya uyarı karşılaştı dahil olmak üzere bu iş hakkındaki bilgileri gösterir, kullanılan yapılandırma ve derleme günlükleri giriş parametreleri.</span><span class="sxs-lookup"><span data-stu-id="306e1-155">When you open a compilation job blade, it shows information about that job including any errors or warnings encountered, input parameters used in the configuration, and compilation logs.</span></span>

1. <span data-ttu-id="306e1-156">[Azure Portal](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="306e1-156">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="306e1-157">Hub menüsünde **tüm kaynakları** ve ardından Otomasyon hesabınızın adını.</span><span class="sxs-lookup"><span data-stu-id="306e1-157">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="306e1-158">Üzerinde **Otomasyon hesabı** dikey penceresinde tıklatın **DSC yapılandırmaları**.</span><span class="sxs-lookup"><span data-stu-id="306e1-158">On the **Automation account** blade, click **DSC Configurations**.</span></span>
4. <span data-ttu-id="306e1-159">Üzerinde **DSC yapılandırmaları** dikey penceresinde tıklatın **TestConfig** (daha önce içe aktarılan yapılandırma adı).</span><span class="sxs-lookup"><span data-stu-id="306e1-159">On the **DSC Configurations** blade, click **TestConfig** (the name of the previously imported configuration).</span></span>
5. <span data-ttu-id="306e1-160">Üzerinde **derleme işleri** , döşeme **TestConfig yapılandırma** dikey penceresinde, listelenen işleri birini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="306e1-160">On the **Compilation jobs** tile of the **TestConfig Configuration** blade, click on any of the jobs listed.</span></span> <span data-ttu-id="306e1-161">A **derleme işi** derleme işi başlatıldı tarihle etiketli dikey penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="306e1-161">A **Compilation Job** blade opens, labeled with the date that the compilation job was started.</span></span>
   
    ![Derleme işi dikey penceresinin ekran görüntüsü](./media/automation-dsc-getting-started/CompilationJob.png)
6. <span data-ttu-id="306e1-163">Herhangi bir kutucuğu tıklayın **derleme işi** dikey penceresini görmek için daha fazla iş hakkında ayrıntılar.</span><span class="sxs-lookup"><span data-stu-id="306e1-163">Click on any tile in the **Compilation Job** blade to see further details about the job.</span></span>

## <a name="viewing-node-configurations"></a><span data-ttu-id="306e1-164">Düğüm yapılandırmaları görüntüleme</span><span class="sxs-lookup"><span data-stu-id="306e1-164">Viewing node configurations</span></span>
<span data-ttu-id="306e1-165">Derleme işi başarılı şekilde tamamlandığını bir veya daha fazla yeni düğüm yapılandırmaları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="306e1-165">Successful completion of a compilation job creates one or more new node configurations.</span></span> <span data-ttu-id="306e1-166">Düğüm yapılandırması çekme sunucusuna ve çekilen ve bir veya daha fazla düğüm tarafından uygulanan hazır dağıtılan bir MOF belgedir.</span><span class="sxs-lookup"><span data-stu-id="306e1-166">A node configuration is a MOF document that is deployed to the pull server and ready to be pulled and applied by one or more nodes.</span></span> <span data-ttu-id="306e1-167">Otomasyon hesabınızda düğüm yapılandırmaları görüntüleyebileceği **DSC düğüm yapılandırmaları** dikey.</span><span class="sxs-lookup"><span data-stu-id="306e1-167">You can view the node configurations in your Automation account in the **DSC Node Configurations** blade.</span></span> <span data-ttu-id="306e1-168">Düğüm yapılandırması form ile bir ada sahip *ConfigurationName*. *NodeName*.</span><span class="sxs-lookup"><span data-stu-id="306e1-168">A node configuration has a name with the form *ConfigurationName*.*NodeName*.</span></span>

1. <span data-ttu-id="306e1-169">[Azure Portal](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="306e1-169">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="306e1-170">Hub menüsünde **tüm kaynakları** ve ardından Otomasyon hesabınızın adını.</span><span class="sxs-lookup"><span data-stu-id="306e1-170">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="306e1-171">Üzerinde **Otomasyon hesabı** dikey penceresinde tıklatın **DSC düğüm yapılandırmaları**.</span><span class="sxs-lookup"><span data-stu-id="306e1-171">On the **Automation account** blade, click **DSC Node Configurations**.</span></span>
   
    ![DSC düğüm yapılandırmaları dikey penceresinin ekran görüntüsü](./media/automation-dsc-getting-started/NodeConfigs.png)

## <a name="onboarding-an-azure-vm-for-management-with-azure-automation-dsc"></a><span data-ttu-id="306e1-173">Azure Otomasyonu DSC ile bir Azure VM yönetimi için hazırlanma</span><span class="sxs-lookup"><span data-stu-id="306e1-173">Onboarding an Azure VM for management with Azure Automation DSC</span></span>
<span data-ttu-id="306e1-174">Azure Otomasyonu DSC, Azure Vm'leri (Klasik ve Resource Manager), şirket içi sanal makineleri, Linux makineler, AWS VM'ler ve şirket içi fiziksel makineleri yönetmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="306e1-174">You can use Azure Automation DSC to manage Azure VMs (both Classic and Resource Manager), on-premises VMs, Linux machines, AWS VMs, and on-premises physical machines.</span></span> <span data-ttu-id="306e1-175">Bu konuda, biz kapak yerleşik yalnızca Azure Kaynak Yöneticisi Vm'leri nasıl.</span><span class="sxs-lookup"><span data-stu-id="306e1-175">In this topic, we cover how to onboard only Azure Resource Manager VMs.</span></span> <span data-ttu-id="306e1-176">Ekleme hakkında bilgi için bkz: diğer türleri makine [Azure Otomasyonu DSC tarafından Yönetim için hazırlama makineler](automation-dsc-onboarding.md).</span><span class="sxs-lookup"><span data-stu-id="306e1-176">For information about onboarding other types of machines, see [Onboarding machines for management by Azure Automation DSC](automation-dsc-onboarding.md).</span></span>

### <a name="to-onboard-an-azure-resource-manager-vm-for-management-by-azure-automation-dsc"></a><span data-ttu-id="306e1-177">Onboarding için Azure Otomasyonu DSC tarafından Yönetim için bir Azure Kaynak Yöneticisi'ni VM</span><span class="sxs-lookup"><span data-stu-id="306e1-177">To onboard an Azure Resource Manager VM for management by Azure Automation DSC</span></span>
1. <span data-ttu-id="306e1-178">[Azure Portal](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="306e1-178">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="306e1-179">Hub menüsünde **tüm kaynakları** ve ardından Otomasyon hesabınızın adını.</span><span class="sxs-lookup"><span data-stu-id="306e1-179">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="306e1-180">Üzerinde **Otomasyon hesabı** dikey penceresinde tıklatın **DSC düğümleri**.</span><span class="sxs-lookup"><span data-stu-id="306e1-180">On the **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="306e1-181">İçinde **DSC düğümleri** dikey penceresinde tıklatın **eklemek Azure VM**.</span><span class="sxs-lookup"><span data-stu-id="306e1-181">In the **DSC Nodes** blade, click **Add Azure VM**.</span></span>
   
    ![Azure VM Ekle düğmesi vurgulama DSC düğümleri dikey penceresinin ekran görüntüsü](./media/automation-dsc-getting-started/OnboardVM.png)
5. <span data-ttu-id="306e1-183">İçinde **eklemek Azure Vm'leri** dikey penceresinde tıklatın **giriş için sanal makine Seç**.</span><span class="sxs-lookup"><span data-stu-id="306e1-183">In the **Add Azure VMs** blade, click **Select virtual machines to onboard**.</span></span>
6. <span data-ttu-id="306e1-184">İçinde **seçin VM'ler** dikey penceresinde, istediğiniz yerleşik VM seçin ve tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="306e1-184">In the **Select VMs** blade, select the VM you want to onboard, and click **OK**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="306e1-185">Bu Windows Server 2008 R2 çalıştıran bir Azure Kaynak Yöneticisi'ni VM olmalıdır veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="306e1-185">This must be an Azure Resource Manager VM running Windows Server 2008 R2 or later.</span></span>
   > 
   > 
7. <span data-ttu-id="306e1-186">İçinde **eklemek Azure Vm'leri** dikey penceresinde tıklatın **kayıt verileri yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="306e1-186">In the **Add Azure VMs** blade, click **Configure registration data**.</span></span>
8. <span data-ttu-id="306e1-187">İçinde **kayıt** dikey penceresinde, VM için uygulamak istediğiniz düğüm yapılandırmasının adı girin **düğüm yapılandırma adı** kutusu.</span><span class="sxs-lookup"><span data-stu-id="306e1-187">In the **Registration** blade, enter the name of the node configuration you want to apply to the VM in the **Node Configuration Name** box.</span></span> <span data-ttu-id="306e1-188">Bu Otomasyon hesabında bir düğüm yapılandırmasının adı tam olarak eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="306e1-188">This must exactly match the name of a node configuration in the Automation account.</span></span> <span data-ttu-id="306e1-189">Bu noktada sağlayan bir adı isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="306e1-189">Providing a name at this point is optional.</span></span> <span data-ttu-id="306e1-190">Onboarding düğüm sonra atanan düğüm yapılandırmasını değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="306e1-190">You can change the assigned node configuration after onboarding the node.</span></span>
   <span data-ttu-id="306e1-191">Denetleme **gerekirse düğümü yeniden**ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="306e1-191">Check **Reboot Node if Needed**, and then click **OK**.</span></span>
   
    ![Kayıt dikey penceresinin ekran görüntüsü](./media/automation-dsc-getting-started/RegisterVM.png)
   
    <span data-ttu-id="306e1-193">Belirtilen düğüm yapılandırması tarafından belirtilen aralıklarla VM'ye uygulanacak olan **yapılandırma modu sıklığı**, ve VM tarafından belirlenen aralıklarla düğüm yapılandırması için güncelleştirmeleri kontrol eder **yenileme sıklığı**.</span><span class="sxs-lookup"><span data-stu-id="306e1-193">The node configuration you specified will be applied to the VM at intervals specified by the **Configuration Mode Frequency**, and the VM will check for updates to the node configuration at intervals specified by the **Refresh Frequency**.</span></span> <span data-ttu-id="306e1-194">Bu değerleri nasıl kullanıldığı konusunda daha fazla bilgi için bkz: [yerel Configuration Manager Yapılandırma](https://msdn.microsoft.com/PowerShell/DSC/metaConfig).</span><span class="sxs-lookup"><span data-stu-id="306e1-194">For more information about how these values are used, see [Configuring the Local Configuration Manager](https://msdn.microsoft.com/PowerShell/DSC/metaConfig).</span></span>
9. <span data-ttu-id="306e1-195">İçinde **eklemek Azure Vm'leri** dikey penceresinde tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="306e1-195">In the **Add Azure VMs** blade, click **Create**.</span></span>

<span data-ttu-id="306e1-196">Azure VM ekleme işlemi başlar.</span><span class="sxs-lookup"><span data-stu-id="306e1-196">Azure will start the process of onboarding the VM.</span></span> <span data-ttu-id="306e1-197">Tamamlandığında, VM görünecek **DSC düğümleri** dikey penceresinde Otomasyon hesabı.</span><span class="sxs-lookup"><span data-stu-id="306e1-197">When it is complete, the VM will show up in the **DSC Nodes** blade in the Automation account.</span></span>

## <a name="viewing-the-list-of-dsc-nodes"></a><span data-ttu-id="306e1-198">DSC düğümleri listesini görüntüleme</span><span class="sxs-lookup"><span data-stu-id="306e1-198">Viewing the list of DSC nodes</span></span>
<span data-ttu-id="306e1-199">Otomasyon hesabınızda Yönetimi edildi kaldırılmış tüm makinelerin listesini görüntüleyebileceğiniz **DSC düğümleri** dikey.</span><span class="sxs-lookup"><span data-stu-id="306e1-199">You can view the list of all machines that have been onboarded for management in your Automation account in the **DSC Nodes** blade.</span></span>

1. <span data-ttu-id="306e1-200">[Azure Portal](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="306e1-200">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="306e1-201">Hub menüsünde **tüm kaynakları** ve ardından Otomasyon hesabınızın adını.</span><span class="sxs-lookup"><span data-stu-id="306e1-201">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="306e1-202">Üzerinde **Otomasyon hesabı** dikey penceresinde tıklatın **DSC düğümleri**.</span><span class="sxs-lookup"><span data-stu-id="306e1-202">On the **Automation account** blade, click **DSC Nodes**.</span></span>

## <a name="viewing-reports-for-dsc-nodes"></a><span data-ttu-id="306e1-203">DSC düğüm raporları görüntüleme</span><span class="sxs-lookup"><span data-stu-id="306e1-203">Viewing reports for DSC nodes</span></span>
<span data-ttu-id="306e1-204">Azure Otomasyonu DSC yönetilen bir düğüm üzerinde tutarlılık denetimi gerçekleştirir her zaman düğüm bir durum raporu çekme sunucusuna geri gönderir.</span><span class="sxs-lookup"><span data-stu-id="306e1-204">Each time Azure Automation DSC performs a consistency check on a managed node, the node sends a status report back to the pull server.</span></span> <span data-ttu-id="306e1-205">Bu düğüm için dikey penceresinde, bu raporları görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="306e1-205">You can view these reports on the blade for that node.</span></span>

1. <span data-ttu-id="306e1-206">[Azure Portal](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="306e1-206">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="306e1-207">Hub menüsünde **tüm kaynakları** ve ardından Otomasyon hesabınızın adını.</span><span class="sxs-lookup"><span data-stu-id="306e1-207">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="306e1-208">Üzerinde **Otomasyon hesabı** dikey penceresinde tıklatın **DSC düğümleri**.</span><span class="sxs-lookup"><span data-stu-id="306e1-208">On the **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="306e1-209">Üzerinde **raporları** kutucuğu, listedeki raporların birini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="306e1-209">On the **Reports** tile, click on any of the reports in the list.</span></span>
   
    ![Rapor dikey penceresinin ekran görüntüsü](./media/automation-dsc-getting-started/NodeReport.png)

<span data-ttu-id="306e1-211">Dikey penceresinde bir tek tek raporu, karşılık gelen tutarlılık denetimi için aşağıdaki durum bilgileri görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="306e1-211">On the blade for an individual report, you can see the following status information for the corresponding consistency check:</span></span>

* <span data-ttu-id="306e1-212">Rapor durumu — "Uyumlu", "Başarısız" yapılandırma düğümdür ya da "Uyumlu" bir düğümdür (düğüm olduğunda **applyandmonitor** modu ve makine istenilen durumda değil).</span><span class="sxs-lookup"><span data-stu-id="306e1-212">The report status — whether the node is "Compliant", the configuration "Failed", or the node is "Not Compliant" (when the node is in **applyandmonitor** mode and the machine is not in the desired state).</span></span>
* <span data-ttu-id="306e1-213">Tutarlılık denetimi için başlangıç saati.</span><span class="sxs-lookup"><span data-stu-id="306e1-213">The start time for the consistency check.</span></span>
* <span data-ttu-id="306e1-214">Tutarlılık denetimi için toplam çalışma zamanı.</span><span class="sxs-lookup"><span data-stu-id="306e1-214">The total runtime for the consistency check.</span></span>
* <span data-ttu-id="306e1-215">Tutarlılık denetimi türü.</span><span class="sxs-lookup"><span data-stu-id="306e1-215">The type of consistency check.</span></span>
* <span data-ttu-id="306e1-216">Hata iletisi ve hata kodu da dahil olmak üzere tüm hatalar.</span><span class="sxs-lookup"><span data-stu-id="306e1-216">Any errors, including the error code and error message.</span></span> 
* <span data-ttu-id="306e1-217">Yapılandırma ve durum (düğüm bu kaynak için istenen durumunda olup) her bir kaynağın kullanılan DSC kaynakları; kaynağı için daha ayrıntılı bilgi almak için her bir kaynağın tıklatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="306e1-217">Any DSC resources used in the configuration, and the state of each resource (whether the node is in the desired state for that resource) — you can click on each resource to get more detailed information for that resource.</span></span>
* <span data-ttu-id="306e1-218">Adı, IP adresi ve düğümün yapılandırma modu.</span><span class="sxs-lookup"><span data-stu-id="306e1-218">The name, IP address, and configuration mode of the node.</span></span>

<span data-ttu-id="306e1-219">Tıklatarak **görüntülemek ham rapor** düğümü sunucuya gönderdiği gerçek verileri görmek için.</span><span class="sxs-lookup"><span data-stu-id="306e1-219">You can also click **View raw report** to see the actual data that the node sends to the server.</span></span> <span data-ttu-id="306e1-220">Bu verileri kullanma hakkında daha fazla bilgi için bkz: [DSC rapor sunucusu kullanarak](https://msdn.microsoft.com/powershell/dsc/reportserver).</span><span class="sxs-lookup"><span data-stu-id="306e1-220">For more information about using that data, see [Using a DSC report server](https://msdn.microsoft.com/powershell/dsc/reportserver).</span></span>

<span data-ttu-id="306e1-221">İlk rapor kullanılabilir olmadan önce bir düğümü edildi sonra biraz zaman alabilir.</span><span class="sxs-lookup"><span data-stu-id="306e1-221">It can take some time after a node is onboarded before the first report is available.</span></span> <span data-ttu-id="306e1-222">İlk rapor için 30 dakika sonra yerleşik bir düğüm beklemeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="306e1-222">You might need to wait up to 30 minutes for the first report after you onboard a node.</span></span>

## <a name="reassigning-a-node-to-a-different-node-configuration"></a><span data-ttu-id="306e1-223">Farklı düğüm yapılandırması düğüme yeniden atama</span><span class="sxs-lookup"><span data-stu-id="306e1-223">Reassigning a node to a different node configuration</span></span>
<span data-ttu-id="306e1-224">Başlangıçta atanan olandan farklı bir düğüme yapılandırmasını kullanmak için bir düğüm atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="306e1-224">You can assign a node to use a different node configuration than the one you initially assigned.</span></span>

1. <span data-ttu-id="306e1-225">[Azure Portal](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="306e1-225">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="306e1-226">Hub menüsünde **tüm kaynakları** ve ardından Otomasyon hesabınızın adını.</span><span class="sxs-lookup"><span data-stu-id="306e1-226">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="306e1-227">Üzerinde **Otomasyon hesabı** dikey penceresinde tıklatın **DSC düğümleri**.</span><span class="sxs-lookup"><span data-stu-id="306e1-227">On the **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="306e1-228">Üzerinde **DSC düğümleri** dikey penceresinde atamak istediğiniz düğümün adını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="306e1-228">On the **DSC Nodes** blade, click on the name of the node you want to reassign.</span></span>
5. <span data-ttu-id="306e1-229">Bu düğüm için dikey penceresinde **Ata düğümü**.</span><span class="sxs-lookup"><span data-stu-id="306e1-229">On the blade for that node, click **Assign node**.</span></span>
   
    ![Ata düğüm düğmesini vurgulama düğümü dikey penceresinin ekran görüntüsü](./media/automation-dsc-getting-started/AssignNode.png)
6. <span data-ttu-id="306e1-231">Üzerinde **atamak düğüm yapılandırması** dikey penceresinde, düğüm atayın ve ardından istediğiniz düğüm yapılandırması **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="306e1-231">On the **Assign Node Configuration** blade, select the node configuration to which you want to assign the node, and then click **OK**.</span></span>
   
    ![Düğüm yapılandırması atayın dikey penceresinin ekran görüntüsü](./media/automation-dsc-getting-started/AssignNodeConfig.png)

## <a name="unregistering-a-node"></a><span data-ttu-id="306e1-233">Bir düğümün kaydı silinirken</span><span class="sxs-lookup"><span data-stu-id="306e1-233">Unregistering a node</span></span>
<span data-ttu-id="306e1-234">Azure Otomasyonu DSC tarafından yönetilmek üzere bir düğümü artık istemiyorsanız kaydını kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="306e1-234">If you no longer want a node to be managed by Azure Automation DSC, you can unregister it.</span></span>

1. <span data-ttu-id="306e1-235">[Azure Portal](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="306e1-235">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="306e1-236">Hub menüsünde **tüm kaynakları** ve ardından Otomasyon hesabınızın adını.</span><span class="sxs-lookup"><span data-stu-id="306e1-236">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="306e1-237">Üzerinde **Otomasyon hesabı** dikey penceresinde tıklatın **DSC düğümleri**.</span><span class="sxs-lookup"><span data-stu-id="306e1-237">On the **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="306e1-238">Üzerinde **DSC düğümleri** dikey penceresinde, kaydını kaldırmak istediğiniz düğümün adını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="306e1-238">On the **DSC Nodes** blade, click on the name of the node you want to unregister.</span></span>
5. <span data-ttu-id="306e1-239">Bu düğüm için dikey penceresinde **Unregister**.</span><span class="sxs-lookup"><span data-stu-id="306e1-239">On the blade for that node, click **Unregister**.</span></span>
   
    ![Unregister düğmesi vurgulama düğümü dikey penceresinin ekran görüntüsü](./media/automation-dsc-getting-started/UnregisterNode.png)

## <a name="related-articles"></a><span data-ttu-id="306e1-241">İlgili makaleler</span><span class="sxs-lookup"><span data-stu-id="306e1-241">Related Articles</span></span>
* [<span data-ttu-id="306e1-242">Azure Otomasyonu DSC genel bakış</span><span class="sxs-lookup"><span data-stu-id="306e1-242">Azure Automation DSC overview</span></span>](automation-dsc-overview.md)
* [<span data-ttu-id="306e1-243">Azure Otomasyonu DSC tarafından Yönetim için hazırlama makineler</span><span class="sxs-lookup"><span data-stu-id="306e1-243">Onboarding machines for management by Azure Automation DSC</span></span>](automation-dsc-onboarding.md)
* [<span data-ttu-id="306e1-244">Windows PowerShell istenen durum yapılandırması genel bakış</span><span class="sxs-lookup"><span data-stu-id="306e1-244">Windows PowerShell Desired State Configuration Overview</span></span>](https://msdn.microsoft.com/powershell/dsc/overview)
* [<span data-ttu-id="306e1-245">Azure Otomasyonu DSC cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="306e1-245">Azure Automation DSC cmdlets</span></span>](/powershell/module/azurerm.automation/#automation)
* [<span data-ttu-id="306e1-246">Azure Otomasyonu DSC fiyatlandırması</span><span class="sxs-lookup"><span data-stu-id="306e1-246">Azure Automation DSC pricing</span></span>](https://azure.microsoft.com/pricing/details/automation/)

