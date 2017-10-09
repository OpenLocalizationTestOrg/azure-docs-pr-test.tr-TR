---
title: "aaaGetting başlatılan Azure Otomasyonu DSC'ye | Microsoft Docs"
description: "Açıklama ve hello en yaygın görevleri de Azure Otomasyonu istenen durum yapılandırması (DSC) örnekleri"
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
ms.openlocfilehash: 82910c96e928b9264c2e1b52a5c98dc47273dcc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-automation-dsc"></a><span data-ttu-id="f1ddc-103">Azure Otomasyonu DSC ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="f1ddc-103">Getting started with Azure Automation DSC</span></span>
<span data-ttu-id="f1ddc-104">Bu konu, nasıl toodo hello ile Azure Otomasyonu istenen durum yapılandırması (oluşturma, alma ve yapılandırmaları, onboarding makineleri çok yönetmek, derleme ve raporları görüntüleme gibi DSC), en yaygın görevleri açıklar.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-104">This topic explains how toodo hello most common tasks with Azure Automation Desired State Configuration (DSC), such as creating, importing, and compiling configurations, onboarding machines too manage, and viewing reports.</span></span> <span data-ttu-id="f1ddc-105">Hangi Azure Otomasyonu DSC genel bir bakış için bkz: [Azure Automation DSC genel bakış](automation-dsc-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f1ddc-105">For an overview of what Azure Automation DSC is, see [Azure Automation DSC Overview](automation-dsc-overview.md).</span></span> <span data-ttu-id="f1ddc-106">DSC belgeler için bkz: [Windows PowerShell istenen durum yapılandırması genel bakış](https://msdn.microsoft.com/PowerShell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="f1ddc-106">For DSC documentation, see [Windows PowerShell Desired State Configuration Overview](https://msdn.microsoft.com/PowerShell/dsc/overview).</span></span>

<span data-ttu-id="f1ddc-107">Bu konu hakkında adım adım kılavuzu toousing Azure Otomasyonu DSC sağlar.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-107">This topic provides a step-by-step guide toousing Azure Automation DSC.</span></span> <span data-ttu-id="f1ddc-108">Zaten bu konuda açıklanan başlangıç adımları uymadan ayarlanmış bir örnek ortamı istiyorsanız kullanabileceğiniz [hello ARM şablonu](https://github.com/azureautomation/automation-packs/tree/master/102-sample-automation-setup).</span><span class="sxs-lookup"><span data-stu-id="f1ddc-108">If you want a sample environment that is already set up without following hello steps described in this topic, you can use [hello following ARM template](https://github.com/azureautomation/automation-packs/tree/master/102-sample-automation-setup).</span></span> <span data-ttu-id="f1ddc-109">Bu şablon tamamlanmış bir Azure Otomasyonu DSC ortam, Azure Otomasyonu DSC tarafından yönetilen bir Azure VM dahil olmak üzere ayarlar.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-109">This template sets up a completed Azure Automation DSC environment, including an Azure VM that is managed by Azure Automation DSC.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f1ddc-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="f1ddc-110">Prerequisites</span></span>
<span data-ttu-id="f1ddc-111">Bu konudaki toocomplete hello örnekleri, hello aşağıdaki gereklidir:</span><span class="sxs-lookup"><span data-stu-id="f1ddc-111">toocomplete hello examples in this topic, hello following are required:</span></span>

* <span data-ttu-id="f1ddc-112">Azure Otomasyonu hesabı.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-112">An Azure Automation account.</span></span> <span data-ttu-id="f1ddc-113">Bir Azure Otomasyonu Garklı Çalıştır hesabı oluşturma yönergeleri için bkz. [Azure Farklı Çalıştır Hesabı](automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="f1ddc-113">For instructions on creating an Azure Automation Run As account, see [Azure Run As Account](automation-sec-configure-azure-runas-account.md).</span></span>
* <span data-ttu-id="f1ddc-114">Bir Azure Kaynak Yöneticisi'ni VM (Klasik değil) Windows Server 2008 R2 çalıştıran veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-114">An Azure Resource Manager VM (not Classic) running Windows Server 2008 R2 or later.</span></span> <span data-ttu-id="f1ddc-115">Bir VM oluşturma ile ilgili yönergeler için bkz: [hello Azure portalında, ilk Windows sanal makine oluşturma](../virtual-machines/virtual-machines-windows-hero-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="f1ddc-115">For instructions on creating a VM, see [Create your first Windows virtual machine in hello Azure portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md)</span></span>

## <a name="creating-a-dsc-configuration"></a><span data-ttu-id="f1ddc-116">DSC yapılandırması oluşturma</span><span class="sxs-lookup"><span data-stu-id="f1ddc-116">Creating a DSC configuration</span></span>
<span data-ttu-id="f1ddc-117">Basit bir oluşturacağız [DSC Yapılandırması](https://msdn.microsoft.com/powershell/dsc/configurations) hello varlığının veya yokluğunun hello sağlar **Web sunucusu** Windows özelliği (düğümler nasıl atadığınız bağlı olarak IIS).</span><span class="sxs-lookup"><span data-stu-id="f1ddc-117">We will create a simple [DSC configuration](https://msdn.microsoft.com/powershell/dsc/configurations) that ensures either hello presence or absence of hello **Web-Server** Windows Feature (IIS), depending on how you assign nodes.</span></span>

1. <span data-ttu-id="f1ddc-118">Windows PowerShell ISE Hello (veya herhangi bir metin düzenleyicisi) başlatın.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-118">Start hello Windows PowerShell ISE (or any text editor).</span></span>
2. <span data-ttu-id="f1ddc-119">Metin aşağıdaki hello yazın:</span><span class="sxs-lookup"><span data-stu-id="f1ddc-119">Type hello following text:</span></span>
   
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
3. <span data-ttu-id="f1ddc-120">Merhaba dosyası olarak kaydetmeniz `TestConfig.ps1`.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-120">Save hello file as `TestConfig.ps1`.</span></span>

<span data-ttu-id="f1ddc-121">Bu yapılandırma bir kaynak her düğümü blok hello çağırır [WindowsFeature kaynak](https://msdn.microsoft.com/powershell/dsc/windowsfeatureresource), hello varlığının veya yokluğunun hello sağlar **Web sunucusu** özelliği.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-121">This configuration calls one resource in each node block, hello [WindowsFeature resource](https://msdn.microsoft.com/powershell/dsc/windowsfeatureresource), that ensures either hello presence or absence of hello **Web-Server** feature.</span></span>

## <a name="importing-a-configuration-into-azure-automation"></a><span data-ttu-id="f1ddc-122">Bir yapılandırma Azure Automation'a içeri aktarma</span><span class="sxs-lookup"><span data-stu-id="f1ddc-122">Importing a configuration into Azure Automation</span></span>
<span data-ttu-id="f1ddc-123">Ardından, biz Otomasyon hesabı hello hello yapılandırma aktaracaksınız.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-123">Next, we'll import hello configuration into hello Automation account.</span></span>

1. <span data-ttu-id="f1ddc-124">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f1ddc-124">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f1ddc-125">Merhaba Hub menüsünde **tüm kaynakları** ve ardından hello Otomasyon hesabınızın adını.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-125">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="f1ddc-126">Merhaba üzerinde **Otomasyon hesabı** dikey penceresinde tıklatın **DSC yapılandırmaları**.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-126">On hello **Automation account** blade, click **DSC Configurations**.</span></span>
4. <span data-ttu-id="f1ddc-127">Merhaba üzerinde **DSC yapılandırmaları** dikey penceresinde tıklatın **bir yapılandırma eklemek**.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-127">On hello **DSC Configurations** blade, click **Add a configuration**.</span></span>
5. <span data-ttu-id="f1ddc-128">Merhaba üzerinde **alma Yapılandırması** dikey penceresinde, Gözat toohello `TestConfig.ps1` dosyayı bilgisayarınıza.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-128">On hello **Import Configuration** blade, browse toohello `TestConfig.ps1` file on your computer.</span></span>
   
    ![Ekran görüntüsü hello ** alma yapılandırma ** dikey penceresi](./media/automation-dsc-getting-started/AddConfig.png)
6. <span data-ttu-id="f1ddc-130">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-130">Click **OK**.</span></span>

## <a name="viewing-a-configuration-in-azure-automation"></a><span data-ttu-id="f1ddc-131">Azure Otomasyonu'nda bir yapılandırmayı görüntüleme</span><span class="sxs-lookup"><span data-stu-id="f1ddc-131">Viewing a configuration in Azure Automation</span></span>
<span data-ttu-id="f1ddc-132">Bir yapılandırma içe aktardıktan sonra hello Azure portal görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-132">After you have imported a configuration, you can view it in hello Azure portal.</span></span>

1. <span data-ttu-id="f1ddc-133">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f1ddc-133">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f1ddc-134">Merhaba Hub menüsünde **tüm kaynakları** ve ardından hello Otomasyon hesabınızın adını.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-134">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="f1ddc-135">Merhaba üzerinde **Otomasyon hesabı** dikey penceresinde tıklatın **DSC yapılandırmaları**</span><span class="sxs-lookup"><span data-stu-id="f1ddc-135">On hello **Automation account** blade, click **DSC Configurations**</span></span>
4. <span data-ttu-id="f1ddc-136">Merhaba üzerinde **DSC yapılandırmaları** dikey penceresinde tıklatın **TestConfig** (Bu hello aldığınız hello yapılandırma hello önceki yordamda adıdır).</span><span class="sxs-lookup"><span data-stu-id="f1ddc-136">On hello **DSC Configurations** blade, click **TestConfig** (this is hello name of hello configuration you imported in hello previous procedure).</span></span>
5. <span data-ttu-id="f1ddc-137">Merhaba üzerinde **TestConfig yapılandırma** dikey penceresinde tıklatın **yapılandırma kaynağı görüntüle**.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-137">On hello **TestConfig Configuration** blade, click **View configuration source**.</span></span>
   
    ![Merhaba TestConfig yapılandırma dikey penceresinin ekran görüntüsü](./media/automation-dsc-getting-started/ViewConfigSource.png)
   
    <span data-ttu-id="f1ddc-139">A **TestConfig yapılandırma kaynağı** hello PowerShell kodu hello yapılandırması için görüntüleme dikey penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-139">A **TestConfig Configuration source** blade opens, displaying hello PowerShell code for hello configuration.</span></span>

## <a name="compiling-a-configuration-in-azure-automation"></a><span data-ttu-id="f1ddc-140">Bir Azure Otomasyonu yapılandırmasında derleme</span><span class="sxs-lookup"><span data-stu-id="f1ddc-140">Compiling a configuration in Azure Automation</span></span>
<span data-ttu-id="f1ddc-141">İstenen durumu tooa düğümü uygulayabilmeniz için önce bu duruma tanımlama DSC yapılandırması bir veya daha fazla düğüm yapılandırmaları (MOF belge) derlenmiş ve gerekir Automation DSC çekme sunucusuna hello üzerinde yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-141">Before you can apply a desired state tooa node, a DSC configuration defining that state must be compiled into one or more node configurations (MOF document), and placed on hello Automation DSC Pull Server.</span></span> <span data-ttu-id="f1ddc-142">Azure Otomasyonu DSC yapılandırmalarında derleme daha ayrıntılı açıklaması için bkz: [Azure Otomasyonu DSC yapılandırmalarında derleme](automation-dsc-compile.md).</span><span class="sxs-lookup"><span data-stu-id="f1ddc-142">For a more detailed description of compiling configurations in Azure Automation DSC, see [Compiling configurations in Azure Automation DSC](automation-dsc-compile.md).</span></span> <span data-ttu-id="f1ddc-143">Derleme yapılandırmaları hakkında daha fazla bilgi için bkz: [DSC yapılandırmaları](https://msdn.microsoft.com/PowerShell/DSC/configurations).</span><span class="sxs-lookup"><span data-stu-id="f1ddc-143">For more information about compiling configurations, see [DSC Configurations](https://msdn.microsoft.com/PowerShell/DSC/configurations).</span></span>

1. <span data-ttu-id="f1ddc-144">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f1ddc-144">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f1ddc-145">Merhaba Hub menüsünde **tüm kaynakları** ve ardından hello Otomasyon hesabınızın adını.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-145">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="f1ddc-146">Merhaba üzerinde **Otomasyon hesabı** dikey penceresinde tıklatın **DSC yapılandırmaları**</span><span class="sxs-lookup"><span data-stu-id="f1ddc-146">On hello **Automation account** blade, click **DSC Configurations**</span></span>
4. <span data-ttu-id="f1ddc-147">Merhaba üzerinde **DSC yapılandırmaları** dikey penceresinde tıklatın **TestConfig** (Merhaba hello adı önceden aktarılmış yapılandırma).</span><span class="sxs-lookup"><span data-stu-id="f1ddc-147">On hello **DSC Configurations** blade, click **TestConfig** (hello name of hello previously imported configuration).</span></span>
5. <span data-ttu-id="f1ddc-148">Merhaba üzerinde **TestConfig yapılandırma** dikey penceresinde tıklatın **derleme**ve ardından **Evet**.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-148">On hello **TestConfig Configuration** blade, click **Compile**, and then click **Yes**.</span></span> <span data-ttu-id="f1ddc-149">Bu derleme işi başlatır.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-149">This starts a compilation job.</span></span>
   
    ![Derleme düğmesi vurgulama hello TestConfig yapılandırma dikey penceresinin ekran görüntüsü](./media/automation-dsc-getting-started/CompileConfig.png)

> [!NOTE]
> <span data-ttu-id="f1ddc-151">Bir Azure Otomasyonu yapılandırmasında derlerken herhangi oluşturulan düğümü yapılandırma MOF dosyalarından toohello çekme sunucusuna otomatik olarak dağıtır.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-151">When you compile a configuration in Azure Automation, it automatically deploys any created node configuration MOFs toohello pull server.</span></span>
> 
> 

## <a name="viewing-a-compilation-job"></a><span data-ttu-id="f1ddc-152">Derleme işi görüntüleme</span><span class="sxs-lookup"><span data-stu-id="f1ddc-152">Viewing a compilation job</span></span>
<span data-ttu-id="f1ddc-153">Bir derleme başlattıktan sonra hello görüntüleyebilirsiniz **derleme işleri** döşeme hello **yapılandırma** dikey.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-153">After you start a compilation, you can view it in hello **Compilation jobs** tile in hello **Configuration** blade.</span></span> <span data-ttu-id="f1ddc-154">Merhaba **derleme işleri** döşeme şu anda çalışan gösterir, tamamlandı ve işleri başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-154">hello **Compilation jobs** tile shows currently running, completed, and failed jobs.</span></span> <span data-ttu-id="f1ddc-155">Bir derleme iş dikey penceresi açtığınızda, herhangi bir hata veya uyarı karşılaştı dahil olmak üzere bu iş hakkındaki bilgileri gösterir, giriş parametreleri hello yapılandırma ve derleme günlükleri kullanılan.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-155">When you open a compilation job blade, it shows information about that job including any errors or warnings encountered, input parameters used in hello configuration, and compilation logs.</span></span>

1. <span data-ttu-id="f1ddc-156">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f1ddc-156">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f1ddc-157">Merhaba Hub menüsünde **tüm kaynakları** ve ardından hello Otomasyon hesabınızın adını.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-157">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="f1ddc-158">Merhaba üzerinde **Otomasyon hesabı** dikey penceresinde tıklatın **DSC yapılandırmaları**.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-158">On hello **Automation account** blade, click **DSC Configurations**.</span></span>
4. <span data-ttu-id="f1ddc-159">Merhaba üzerinde **DSC yapılandırmaları** dikey penceresinde tıklatın **TestConfig** (Merhaba hello adı önceden aktarılmış yapılandırma).</span><span class="sxs-lookup"><span data-stu-id="f1ddc-159">On hello **DSC Configurations** blade, click **TestConfig** (hello name of hello previously imported configuration).</span></span>
5. <span data-ttu-id="f1ddc-160">Merhaba üzerinde **derleme işleri** hello parçasına **TestConfig yapılandırma** dikey penceresinde, listelenen hello işlerin birini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-160">On hello **Compilation jobs** tile of hello **TestConfig Configuration** blade, click on any of hello jobs listed.</span></span> <span data-ttu-id="f1ddc-161">A **derleme işi** dikey penceresi açılır ve derleme işi hello hello tarihle etiketli başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-161">A **Compilation Job** blade opens, labeled with hello date that hello compilation job was started.</span></span>
   
    ![Merhaba derleme işi dikey penceresinin ekran görüntüsü](./media/automation-dsc-getting-started/CompilationJob.png)
6. <span data-ttu-id="f1ddc-163">Merhaba herhangi bir kutucuğu tıklayın **derleme işi** dikey toosee daha fazla hello işi hakkında ayrıntılar.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-163">Click on any tile in hello **Compilation Job** blade toosee further details about hello job.</span></span>

## <a name="viewing-node-configurations"></a><span data-ttu-id="f1ddc-164">Düğüm yapılandırmaları görüntüleme</span><span class="sxs-lookup"><span data-stu-id="f1ddc-164">Viewing node configurations</span></span>
<span data-ttu-id="f1ddc-165">Derleme işi başarılı şekilde tamamlandığını bir veya daha fazla yeni düğüm yapılandırmaları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-165">Successful completion of a compilation job creates one or more new node configurations.</span></span> <span data-ttu-id="f1ddc-166">Düğüm yapılandırması dağıtılan toohello çekme sunucu ve çekilen ve bir veya daha fazla düğüm tarafından uygulanan hazır toobe MOF belgedir.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-166">A node configuration is a MOF document that is deployed toohello pull server and ready toobe pulled and applied by one or more nodes.</span></span> <span data-ttu-id="f1ddc-167">Otomasyon hesabınızda hello hello düğüm yapılandırmaları görüntüleyebileceği **DSC düğüm yapılandırmaları** dikey.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-167">You can view hello node configurations in your Automation account in hello **DSC Node Configurations** blade.</span></span> <span data-ttu-id="f1ddc-168">Düğüm yapılandırması hello form ile bir ada sahip *ConfigurationName*. *NodeName*.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-168">A node configuration has a name with hello form *ConfigurationName*.*NodeName*.</span></span>

1. <span data-ttu-id="f1ddc-169">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f1ddc-169">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f1ddc-170">Merhaba Hub menüsünde **tüm kaynakları** ve ardından hello Otomasyon hesabınızın adını.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-170">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="f1ddc-171">Merhaba üzerinde **Otomasyon hesabı** dikey penceresinde tıklatın **DSC düğüm yapılandırmaları**.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-171">On hello **Automation account** blade, click **DSC Node Configurations**.</span></span>
   
    ![Merhaba DSC düğüm yapılandırmaları dikey penceresinin ekran görüntüsü](./media/automation-dsc-getting-started/NodeConfigs.png)

## <a name="onboarding-an-azure-vm-for-management-with-azure-automation-dsc"></a><span data-ttu-id="f1ddc-173">Azure Otomasyonu DSC ile bir Azure VM yönetimi için hazırlanma</span><span class="sxs-lookup"><span data-stu-id="f1ddc-173">Onboarding an Azure VM for management with Azure Automation DSC</span></span>
<span data-ttu-id="f1ddc-174">Azure Otomasyonu DSC toomanage Azure VM'ler (Klasik ve Resource Manager), şirket içi sanal makineleri, Linux makineler, AWS VM'ler ve şirket içi fiziksel makineleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-174">You can use Azure Automation DSC toomanage Azure VMs (both Classic and Resource Manager), on-premises VMs, Linux machines, AWS VMs, and on-premises physical machines.</span></span> <span data-ttu-id="f1ddc-175">Bu konuda, biz kapak nasıl tooonboard yalnızca Azure Kaynak Yöneticisi Vm'leri.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-175">In this topic, we cover how tooonboard only Azure Resource Manager VMs.</span></span> <span data-ttu-id="f1ddc-176">Ekleme hakkında bilgi için bkz: diğer türleri makine [Azure Otomasyonu DSC tarafından Yönetim için hazırlama makineler](automation-dsc-onboarding.md).</span><span class="sxs-lookup"><span data-stu-id="f1ddc-176">For information about onboarding other types of machines, see [Onboarding machines for management by Azure Automation DSC](automation-dsc-onboarding.md).</span></span>

### <a name="tooonboard-an-azure-resource-manager-vm-for-management-by-azure-automation-dsc"></a><span data-ttu-id="f1ddc-177">Azure Otomasyonu DSC tarafından Yönetim için bir Azure Kaynak Yöneticisi'ni VM tooonboard</span><span class="sxs-lookup"><span data-stu-id="f1ddc-177">tooonboard an Azure Resource Manager VM for management by Azure Automation DSC</span></span>
1. <span data-ttu-id="f1ddc-178">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f1ddc-178">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f1ddc-179">Merhaba Hub menüsünde **tüm kaynakları** ve ardından hello Otomasyon hesabınızın adını.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-179">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="f1ddc-180">Merhaba üzerinde **Otomasyon hesabı** dikey penceresinde tıklatın **DSC düğümleri**.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-180">On hello **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="f1ddc-181">Merhaba, **DSC düğümleri** dikey penceresinde tıklatın **eklemek Azure VM**.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-181">In hello **DSC Nodes** blade, click **Add Azure VM**.</span></span>
   
    ![Hello Azure VM Ekle düğmesi vurgulama hello DSC düğümleri dikey penceresinin ekran görüntüsü](./media/automation-dsc-getting-started/OnboardVM.png)
5. <span data-ttu-id="f1ddc-183">Merhaba, **eklemek Azure VM'ler** dikey penceresinde'ı tıklatın **seçin sanal makineleri tooonboard**.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-183">In hello **Add Azure VMs** blade, click **Select virtual machines tooonboard**.</span></span>
6. <span data-ttu-id="f1ddc-184">Merhaba, **seçin VM'ler** dikey penceresinde, select hello tooonboard istediğiniz ve tıklatın VM **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-184">In hello **Select VMs** blade, select hello VM you want tooonboard, and click **OK**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="f1ddc-185">Bu Windows Server 2008 R2 çalıştıran bir Azure Kaynak Yöneticisi'ni VM olmalıdır veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-185">This must be an Azure Resource Manager VM running Windows Server 2008 R2 or later.</span></span>
   > 
   > 
7. <span data-ttu-id="f1ddc-186">Merhaba, **eklemek Azure VM'ler** dikey penceresinde tıklatın **kayıt verilerini yapılandırmak**.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-186">In hello **Add Azure VMs** blade, click **Configure registration data**.</span></span>
8. <span data-ttu-id="f1ddc-187">Merhaba, **kayıt** dikey penceresinde hello adı girin hello içinde tooapply toohello VM istediğiniz hello düğüm yapılandırmasını **düğüm yapılandırma adı** kutusu.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-187">In hello **Registration** blade, enter hello name of hello node configuration you want tooapply toohello VM in hello **Node Configuration Name** box.</span></span> <span data-ttu-id="f1ddc-188">Bu Otomasyon hesabı hello düğümlü bir yapılandırmada hello adı tam olarak eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-188">This must exactly match hello name of a node configuration in hello Automation account.</span></span> <span data-ttu-id="f1ddc-189">Bu noktada sağlayan bir adı isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-189">Providing a name at this point is optional.</span></span> <span data-ttu-id="f1ddc-190">Onboarding hello düğümü sonra atanan hello düğüm yapılandırmasını değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-190">You can change hello assigned node configuration after onboarding hello node.</span></span>
   <span data-ttu-id="f1ddc-191">Denetleme **gerekirse düğümü yeniden**ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-191">Check **Reboot Node if Needed**, and then click **OK**.</span></span>
   
    ![Merhaba kayıt dikey penceresinin ekran görüntüsü](./media/automation-dsc-getting-started/RegisterVM.png)
   
    <span data-ttu-id="f1ddc-193">Belirttiğiniz hello düğüm yapılandırması hello tarafından belirtilen aralıklarla uygulanan toohello VM olacaktır **yapılandırma modu sıklığı**, ve hello VM için güncelleştirmeleri toohello düğüm yapılandırması hellotarafındanbelirtilenaralıklarladenetleyecek **Yenileme sıklığı**.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-193">hello node configuration you specified will be applied toohello VM at intervals specified by hello **Configuration Mode Frequency**, and hello VM will check for updates toohello node configuration at intervals specified by hello **Refresh Frequency**.</span></span> <span data-ttu-id="f1ddc-194">Bu değerleri nasıl kullanıldığı konusunda daha fazla bilgi için bkz: [yapılandırma hello yerel Configuration Manager](https://msdn.microsoft.com/PowerShell/DSC/metaConfig).</span><span class="sxs-lookup"><span data-stu-id="f1ddc-194">For more information about how these values are used, see [Configuring hello Local Configuration Manager](https://msdn.microsoft.com/PowerShell/DSC/metaConfig).</span></span>
9. <span data-ttu-id="f1ddc-195">Merhaba, **eklemek Azure VM'ler** dikey penceresinde tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-195">In hello **Add Azure VMs** blade, click **Create**.</span></span>

<span data-ttu-id="f1ddc-196">Azure ekleme hello VM hello işlemi başlar.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-196">Azure will start hello process of onboarding hello VM.</span></span> <span data-ttu-id="f1ddc-197">Bu tamamlandığında hello VM hello görünecek **DSC düğümleri** dikey penceresinde hello Automation hesabı.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-197">When it is complete, hello VM will show up in hello **DSC Nodes** blade in hello Automation account.</span></span>

## <a name="viewing-hello-list-of-dsc-nodes"></a><span data-ttu-id="f1ddc-198">DSC düğümleri Hello listesini görüntüleme</span><span class="sxs-lookup"><span data-stu-id="f1ddc-198">Viewing hello list of DSC nodes</span></span>
<span data-ttu-id="f1ddc-199">Otomasyon hesabınızda hello Yönetimi edildi kaldırılmış tüm makinelerin hello listesini görüntüleyebileceğiniz **DSC düğümleri** dikey.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-199">You can view hello list of all machines that have been onboarded for management in your Automation account in hello **DSC Nodes** blade.</span></span>

1. <span data-ttu-id="f1ddc-200">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f1ddc-200">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f1ddc-201">Merhaba Hub menüsünde **tüm kaynakları** ve ardından hello Otomasyon hesabınızın adını.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-201">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="f1ddc-202">Merhaba üzerinde **Otomasyon hesabı** dikey penceresinde tıklatın **DSC düğümleri**.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-202">On hello **Automation account** blade, click **DSC Nodes**.</span></span>

## <a name="viewing-reports-for-dsc-nodes"></a><span data-ttu-id="f1ddc-203">DSC düğüm raporları görüntüleme</span><span class="sxs-lookup"><span data-stu-id="f1ddc-203">Viewing reports for DSC nodes</span></span>
<span data-ttu-id="f1ddc-204">Azure Otomasyonu DSC yönetilen bir düğüm üzerinde tutarlılık denetimi gerçekleştirir her zaman hello düğüm durumu rapor geri toohello çekme sunucusuna gönderir.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-204">Each time Azure Automation DSC performs a consistency check on a managed node, hello node sends a status report back toohello pull server.</span></span> <span data-ttu-id="f1ddc-205">Merhaba dikey penceresinde bu düğüm için bu raporları görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-205">You can view these reports on hello blade for that node.</span></span>

1. <span data-ttu-id="f1ddc-206">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f1ddc-206">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f1ddc-207">Merhaba Hub menüsünde **tüm kaynakları** ve ardından hello Otomasyon hesabınızın adını.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-207">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="f1ddc-208">Merhaba üzerinde **Otomasyon hesabı** dikey penceresinde tıklatın **DSC düğümleri**.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-208">On hello **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="f1ddc-209">Merhaba üzerinde **raporları** döşeme, herhangi bir hello listesinde hello Raporlar'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-209">On hello **Reports** tile, click on any of hello reports in hello list.</span></span>
   
    ![Merhaba rapor dikey penceresinin ekran görüntüsü](./media/automation-dsc-getting-started/NodeReport.png)

<span data-ttu-id="f1ddc-211">Merhaba dikey penceresinde tek tek bir rapor, durum bilgisi hello karşılık gelen tutarlılık için aşağıdaki hello denetleyin görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f1ddc-211">On hello blade for an individual report, you can see hello following status information for hello corresponding consistency check:</span></span>

* <span data-ttu-id="f1ddc-212">Merhaba rapor durumu — hello düğümdür "Uyumlu", "Başarısız" Merhaba yapılandırma ya da hello düğümdür "Uyumlu olmayan" (Merhaba düğümü olduğunda **applyandmonitor** modu ve hello makine istenen hello durumda değil).</span><span class="sxs-lookup"><span data-stu-id="f1ddc-212">hello report status — whether hello node is "Compliant", hello configuration "Failed", or hello node is "Not Compliant" (when hello node is in **applyandmonitor** mode and hello machine is not in hello desired state).</span></span>
* <span data-ttu-id="f1ddc-213">Merhaba tutarlılık denetimi için Hello başlangıç saati.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-213">hello start time for hello consistency check.</span></span>
* <span data-ttu-id="f1ddc-214">Merhaba toplam çalışma zamanı hello tutarlılığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-214">hello total runtime for hello consistency check.</span></span>
* <span data-ttu-id="f1ddc-215">Tutarlılık Hello türünü kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-215">hello type of consistency check.</span></span>
* <span data-ttu-id="f1ddc-216">Merhaba hata kodu ve hata iletisi de dahil olmak üzere tüm hatalar.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-216">Any errors, including hello error code and error message.</span></span> 
* <span data-ttu-id="f1ddc-217">Merhaba yapılandırması ve hello durumu (Merhaba düğümü bu kaynak için istenen hello durumunda olup) her bir kaynağın kullanılan DSC kaynakları — tıklayabilirsiniz her kaynak tooget daha ayrıntılı bilgi kaynağı için.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-217">Any DSC resources used in hello configuration, and hello state of each resource (whether hello node is in hello desired state for that resource) — you can click on each resource tooget more detailed information for that resource.</span></span>
* <span data-ttu-id="f1ddc-218">Merhaba adı, IP adresi ve hello düğümünün yapılandırma modu.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-218">hello name, IP address, and configuration mode of hello node.</span></span>

<span data-ttu-id="f1ddc-219">Tıklatarak **görüntülemek ham rapor** toohello sunucu düğümü hello toosee hello gerçek verileri gönderir.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-219">You can also click **View raw report** toosee hello actual data that hello node sends toohello server.</span></span> <span data-ttu-id="f1ddc-220">Bu verileri kullanma hakkında daha fazla bilgi için bkz: [DSC rapor sunucusu kullanarak](https://msdn.microsoft.com/powershell/dsc/reportserver).</span><span class="sxs-lookup"><span data-stu-id="f1ddc-220">For more information about using that data, see [Using a DSC report server](https://msdn.microsoft.com/powershell/dsc/reportserver).</span></span>

<span data-ttu-id="f1ddc-221">Merhaba ilk rapor kullanılabilir olmadan önce bir düğümü edildi sonra biraz zaman alabilir.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-221">It can take some time after a node is onboarded before hello first report is available.</span></span> <span data-ttu-id="f1ddc-222">Toowait too30 dakika yukarı hello ilk rapor için sonra yerleşik bir düğüm gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-222">You might need toowait up too30 minutes for hello first report after you onboard a node.</span></span>

## <a name="reassigning-a-node-tooa-different-node-configuration"></a><span data-ttu-id="f1ddc-223">Bir düğüm tooa farklı düğüm yapılandırması yeniden atama</span><span class="sxs-lookup"><span data-stu-id="f1ddc-223">Reassigning a node tooa different node configuration</span></span>
<span data-ttu-id="f1ddc-224">Bir başlangıçta atanan hello daha farklı düğüm yapılandırması düğüme toouse atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-224">You can assign a node toouse a different node configuration than hello one you initially assigned.</span></span>

1. <span data-ttu-id="f1ddc-225">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f1ddc-225">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f1ddc-226">Merhaba Hub menüsünde **tüm kaynakları** ve ardından hello Otomasyon hesabınızın adını.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-226">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="f1ddc-227">Merhaba üzerinde **Otomasyon hesabı** dikey penceresinde tıklatın **DSC düğümleri**.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-227">On hello **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="f1ddc-228">Merhaba üzerinde **DSC düğümleri** dikey penceresinde hello adına tıklayın hello düğümünün tooreassign istiyor.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-228">On hello **DSC Nodes** blade, click on hello name of hello node you want tooreassign.</span></span>
5. <span data-ttu-id="f1ddc-229">Bu düğüm için Hello dikey penceresinde **Ata düğümü**.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-229">On hello blade for that node, click **Assign node**.</span></span>
   
    ![Merhaba atamak düğüm düğmesini vurgulama hello düğümü dikey penceresinin ekran görüntüsü](./media/automation-dsc-getting-started/AssignNode.png)
6. <span data-ttu-id="f1ddc-231">Merhaba üzerinde **atamak düğüm yapılandırması** dikey penceresinde, tooassign hello düğümü istediğiniz ve ardından select hello düğüm yapılandırması toowhich **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-231">On hello **Assign Node Configuration** blade, select hello node configuration toowhich you want tooassign hello node, and then click **OK**.</span></span>
   
    ![Merhaba atamak düğüm yapılandırması dikey penceresinin ekran görüntüsü](./media/automation-dsc-getting-started/AssignNodeConfig.png)

## <a name="unregistering-a-node"></a><span data-ttu-id="f1ddc-233">Bir düğümün kaydı silinirken</span><span class="sxs-lookup"><span data-stu-id="f1ddc-233">Unregistering a node</span></span>
<span data-ttu-id="f1ddc-234">Azure Otomasyonu DSC tarafından yönetilen bir düğüm toobe artık istemiyorsanız kaydını kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-234">If you no longer want a node toobe managed by Azure Automation DSC, you can unregister it.</span></span>

1. <span data-ttu-id="f1ddc-235">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f1ddc-235">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f1ddc-236">Merhaba Hub menüsünde **tüm kaynakları** ve ardından hello Otomasyon hesabınızın adını.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-236">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="f1ddc-237">Merhaba üzerinde **Otomasyon hesabı** dikey penceresinde tıklatın **DSC düğümleri**.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-237">On hello **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="f1ddc-238">Merhaba üzerinde **DSC düğümleri** dikey penceresinde hello adına tıklayın hello düğümünün toounregister istiyor.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-238">On hello **DSC Nodes** blade, click on hello name of hello node you want toounregister.</span></span>
5. <span data-ttu-id="f1ddc-239">Bu düğüm için Hello dikey penceresinde **Unregister**.</span><span class="sxs-lookup"><span data-stu-id="f1ddc-239">On hello blade for that node, click **Unregister**.</span></span>
   
    ![Merhaba Unregister düğmesi vurgulama hello düğümü dikey penceresinin ekran görüntüsü](./media/automation-dsc-getting-started/UnregisterNode.png)

## <a name="related-articles"></a><span data-ttu-id="f1ddc-241">İlgili makaleler</span><span class="sxs-lookup"><span data-stu-id="f1ddc-241">Related Articles</span></span>
* [<span data-ttu-id="f1ddc-242">Azure Otomasyonu DSC genel bakış</span><span class="sxs-lookup"><span data-stu-id="f1ddc-242">Azure Automation DSC overview</span></span>](automation-dsc-overview.md)
* [<span data-ttu-id="f1ddc-243">Azure Otomasyonu DSC tarafından Yönetim için hazırlama makineler</span><span class="sxs-lookup"><span data-stu-id="f1ddc-243">Onboarding machines for management by Azure Automation DSC</span></span>](automation-dsc-onboarding.md)
* [<span data-ttu-id="f1ddc-244">Windows PowerShell istenen durum yapılandırması genel bakış</span><span class="sxs-lookup"><span data-stu-id="f1ddc-244">Windows PowerShell Desired State Configuration Overview</span></span>](https://msdn.microsoft.com/powershell/dsc/overview)
* [<span data-ttu-id="f1ddc-245">Azure Otomasyonu DSC cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="f1ddc-245">Azure Automation DSC cmdlets</span></span>](/powershell/module/azurerm.automation/#automation)
* [<span data-ttu-id="f1ddc-246">Azure Otomasyonu DSC fiyatlandırması</span><span class="sxs-lookup"><span data-stu-id="f1ddc-246">Azure Automation DSC pricing</span></span>](https://azure.microsoft.com/pricing/details/automation/)

