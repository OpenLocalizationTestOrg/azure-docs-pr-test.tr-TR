---
title: "aaaCreate CI/CD ardışık düzen Team Services ile azure'da | Microsoft Docs"
description: "Nasıl toocreate bir Visual Studio Team Services kanal sürekli tümleştirme ve bir web uygulaması tooIIS Windows VM üzerinde dağıtır teslimi için bilgi edinin"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: b758a124c4742854dd3b543f747fd8700f954414
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-continuous-integration-pipeline-with-visual-studio-team-services-and-iis"></a><span data-ttu-id="ab1d8-103">Visual Studio Team Services ve IIS ile sürekli tümleştirme işlem hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ab1d8-103">Create a continuous integration pipeline with Visual Studio Team Services and IIS</span></span>
<span data-ttu-id="ab1d8-104">tooautomate hello derleme, test ve dağıtım aşamaları uygulama geliştirme, sürekli tümleştirme ve dağıtım (CI/CD) ardışık düzen kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-104">tooautomate hello build, test, and deployment phases of application development, you can use a continuous integration and deployment (CI/CD) pipeline.</span></span> <span data-ttu-id="ab1d8-105">Bu öğreticide, Visual Studio Team Services ve Windows sanal makine (VM), IIS çalıştıran Azure kullanarak bir CI/CD işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-105">In this tutorial, you create a CI/CD pipeline using Visual Studio Team Services and a Windows virtual machine (VM) in Azure that runs IIS.</span></span> <span data-ttu-id="ab1d8-106">Aşağıdakileri nasıl yapacağınızı öğrenirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ab1d8-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ab1d8-107">Bir ASP.NET web uygulaması tooa Team Services projesini Yayımla</span><span class="sxs-lookup"><span data-stu-id="ab1d8-107">Publish an ASP.NET web application tooa Team Services project</span></span>
> * <span data-ttu-id="ab1d8-108">Kod tamamlama tarafından tetiklenen bir yapı tanımı oluşturun</span><span class="sxs-lookup"><span data-stu-id="ab1d8-108">Create a build definition that is triggered by code commits</span></span>
> * <span data-ttu-id="ab1d8-109">IIS yükle ve azure'da bir sanal makinede Yapılandır</span><span class="sxs-lookup"><span data-stu-id="ab1d8-109">Install and configure IIS on a virtual machine in Azure</span></span>
> * <span data-ttu-id="ab1d8-110">Team Services içinde Hello IIS örnek tooa dağıtım grubu Ekle</span><span class="sxs-lookup"><span data-stu-id="ab1d8-110">Add hello IIS instance tooa deployment group in Team Services</span></span>
> * <span data-ttu-id="ab1d8-111">Bir yayın tanımı toopublish yeni web Oluştur paketleri tooIIS dağıtma</span><span class="sxs-lookup"><span data-stu-id="ab1d8-111">Create a release definition toopublish new web deploy packages tooIIS</span></span>
> * <span data-ttu-id="ab1d8-112">Test hello CI/CD ardışık düzen</span><span class="sxs-lookup"><span data-stu-id="ab1d8-112">Test hello CI/CD pipeline</span></span>

<span data-ttu-id="ab1d8-113">Bu öğretici hello Azure PowerShell modülü 3,6 veya sonraki bir sürümü gerektiriyor.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-113">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="ab1d8-114">Çalıştırma `Get-Module -ListAvailable AzureRM` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-114">Run `Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="ab1d8-115">Tooupgrade gerekirse bkz [yükleme Azure PowerShell Modülü](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="ab1d8-115">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="create-project-in-team-services"></a><span data-ttu-id="ab1d8-116">Team Services içinde projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="ab1d8-116">Create project in Team Services</span></span>
<span data-ttu-id="ab1d8-117">Şirket içi kodu yönetim çözümünü korumadan kolay işbirliği ve geliştirme için Visual Studio Team Services sağlar.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-117">Visual Studio Team Services allows for easy collaboration and development without maintaining an on-premises code management solution.</span></span> <span data-ttu-id="ab1d8-118">Team Services kodu bulut test, yapı ve application ınsights sağlar.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-118">Team Services provides cloud code testing, build, and application insights.</span></span> <span data-ttu-id="ab1d8-119">Sürüm denetim deposunu ve kod geliştirme en uygun IDE seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-119">You can choose a version control repo and IDE that best fits your code development.</span></span> <span data-ttu-id="ab1d8-120">Bu öğretici için ücretsiz hesap toocreate temel bir ASP.NET web uygulama ve CI/CD ardışık düzen kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-120">For this tutorial, you can use a free account toocreate a basic ASP.NET web app and CI/CD pipeline.</span></span> <span data-ttu-id="ab1d8-121">Bir Team Services hesabı zaten yoksa [oluşturmak](http://go.microsoft.com/fwlink/?LinkId=307137).</span><span class="sxs-lookup"><span data-stu-id="ab1d8-121">If you do not already have a Team Services account, [create one](http://go.microsoft.com/fwlink/?LinkId=307137).</span></span>

<span data-ttu-id="ab1d8-122">toomanage hello kod kaydetme işlemi, tanımları, derleme ve tanımları sürüm, Team Services içinde aşağıdaki gibi bir proje oluşturun:</span><span class="sxs-lookup"><span data-stu-id="ab1d8-122">toomanage hello code commit process, build definitions, and release definitions, create a project in Team Services as follows:</span></span>

1. <span data-ttu-id="ab1d8-123">Team Services panonuz bir web tarayıcısında açın ve seçin **yeni proje**.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-123">Open your Team Services dashboard in a web browser and choose **New project**.</span></span>
2. <span data-ttu-id="ab1d8-124">Girin *mywebapp şeklindedir* hello için **proje adı**.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-124">Enter *myWebApp* for hello **Project name**.</span></span> <span data-ttu-id="ab1d8-125">Tüm diğer varsayılan değerleri toouse bırakın *Git* sürüm denetimi ve *Çevik* iş öğesi işlemi.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-125">Leave all other default values toouse *Git* version control and *Agile* work item process.</span></span>
3. <span data-ttu-id="ab1d8-126">Çok olarak Hello seçeneği**paylaşmak** *ekip üyelerinin*seçeneğini belirleyip **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-126">Choose hello option too**Share with** *Team Members*, then select **Create**.</span></span>
5. <span data-ttu-id="ab1d8-127">Projeniz oluşturulduktan sonra hello çok seçeneği**bir benioku veya gitignore başlatma**, ardından **başlatma**.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-127">Once your project has been created, choose hello option too**Initialize with a README or gitignore**, then **Initialize**.</span></span>
6. <span data-ttu-id="ab1d8-128">Yeni projeniz içinde seçin **panolar** hello üstte seçip **Visual Studio'da Aç**.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-128">Inside your new project, choose **Dashboards** across hello top, then select **Open in Visual Studio**.</span></span>


## <a name="create-aspnet-web-application"></a><span data-ttu-id="ab1d8-129">ASP.NET web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="ab1d8-129">Create ASP.NET web application</span></span>
<span data-ttu-id="ab1d8-130">Hello önceki adımda, bir proje Team Services ile oluşturulmuş.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-130">In hello previous step, you created a project in Team Services.</span></span> <span data-ttu-id="ab1d8-131">Merhaba son adım, yeni projeniz Visual Studio'da açılır.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-131">hello final step opens your new project in Visual Studio.</span></span> <span data-ttu-id="ab1d8-132">Merhaba içinde kod tamamlama yönetmek **Takım Gezgini** penceresi.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-132">You manage your code commits in hello **Team Explorer** window.</span></span> <span data-ttu-id="ab1d8-133">Yeni projeniz yerel bir kopyasını oluşturun, sonra bir ASP.NET web uygulaması gibi bir şablondan oluşturun:</span><span class="sxs-lookup"><span data-stu-id="ab1d8-133">Create a local copy of your new project, then create an ASP.NET web application from a template as follows:</span></span>

1. <span data-ttu-id="ab1d8-134">Seçin **kopya** toocreate Team Services projenizin yerel git deposu.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-134">Select **Clone** toocreate a local git repo of your Team Services project.</span></span>
    
    ![Team Services projeden depoyu kopyalama](media/tutorial-vsts-iis-cicd/clone_repo.png)

2. <span data-ttu-id="ab1d8-136">Altında **çözümleri**seçin **yeni**.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-136">Under **Solutions**, select **New**.</span></span>

    ![Web uygulaması çözümü oluşturun](media/tutorial-vsts-iis-cicd/new_solution.png)

3. <span data-ttu-id="ab1d8-138">Seçin **Web** şablonları ve ardından hello **ASP.NET Web uygulaması** şablonu.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-138">Select **Web** templates, and then choose hello **ASP.NET Web Application** template.</span></span>
    1. <span data-ttu-id="ab1d8-139">Gibi uygulamanız için bir ad girin *mywebapp şeklindedir*ve hello kutusunun işaretini kaldırın **çözüm için dizin oluştur**.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-139">Enter a name for your application, such as *myWebApp*, and uncheck hello box for **Create directory for solution**.</span></span>
    2. <span data-ttu-id="ab1d8-140">Merhaba seçeneği kullanılabilir durumdaysa, çok hello kutunun işaretini**Application Insights Ekle tooproject**.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-140">If hello option is available, uncheck hello box too**Add Application Insights tooproject**.</span></span> <span data-ttu-id="ab1d8-141">Application Insights web uygulamanızı Azure Application Insights ile tooauthorize gerektirir.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-141">Application Insights requires you tooauthorize your web application with Azure Application Insights.</span></span> <span data-ttu-id="ab1d8-142">tookeep bu işlem Bu öğreticide, basit atlayın.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-142">tookeep it simple in this tutorial, skip this process.</span></span>
    3. <span data-ttu-id="ab1d8-143">**Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-143">Select **OK**.</span></span>
4. <span data-ttu-id="ab1d8-144">Seçin **MVC** hello şablonu listesinden.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-144">Choose **MVC** from hello template list.</span></span>
    1. <span data-ttu-id="ab1d8-145">Seçin **kimlik doğrulamayı Değiştir**, seçin **doğrulaması yok**seçeneğini belirleyip **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-145">Select **Change Authentication**, choose **No Authentication**, then select **OK**.</span></span>
    2. <span data-ttu-id="ab1d8-146">Seçin **Tamam** toocreate çözümünüzü.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-146">Select **OK** toocreate your solution.</span></span>
5. <span data-ttu-id="ab1d8-147">Merhaba, **Takım Gezgini** penceresinde, seçin **değişiklikleri**.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-147">In hello **Team Explorer** window, choose **Changes**.</span></span>

    ![Yerel değişiklikler tooTeam Hizmetleri git deposuna uygulayın](media/tutorial-vsts-iis-cicd/commit_changes.png)

6. <span data-ttu-id="ab1d8-149">Bir ileti gibi Hello yürütme metin kutusuna girin *ilk yürütme*.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-149">In hello commit text box, enter a message such as *Initial commit*.</span></span> <span data-ttu-id="ab1d8-150">Seçin **Commit tüm ve eşitleme** hello açılan menüsünden.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-150">Choose **Commit All and Sync** from hello drop-down menu.</span></span>


## <a name="create-build-definition"></a><span data-ttu-id="ab1d8-151">Yapı tanımı oluşturun</span><span class="sxs-lookup"><span data-stu-id="ab1d8-151">Create build definition</span></span>
<span data-ttu-id="ab1d8-152">Team Services içinde uygulamanızı nasıl yerleşik bir yapı tanımı toooutline kullanın.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-152">In Team Services, you use a build definition toooutline how your application should be built.</span></span> <span data-ttu-id="ab1d8-153">Bu öğreticide, bizim kaynak kodu hello çözüm oluşturur, ardından web oluşturur alır toorun hello web uygulaması bir IIS sunucusunda kullanabilirsiniz paketini dağıtmak bir temel tanımı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-153">In this tutorial, we create a basic definition that takes our source code, builds hello solution, then creates web deploy package we can use toorun hello web app on an IIS server.</span></span>

1. <span data-ttu-id="ab1d8-154">Team Services projenizde seçin **yapı & yayın** hello üstte seçip **derlemeler**.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-154">In your Team Services project, choose **Build & Release** across hello top, then select **Builds**.</span></span>
3. <span data-ttu-id="ab1d8-155">Seçin **+ yeni tanımı**.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-155">Select **+ New definition**.</span></span>
4. <span data-ttu-id="ab1d8-156">Merhaba seçin **ASP.NET (Önizleme)** şablonu ve select **Uygula**.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-156">Choose hello **ASP.NET (PREVIEW)** template and select **Apply**.</span></span>
5. <span data-ttu-id="ab1d8-157">Tüm hello varsayılan görev değerleri bırakın.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-157">Leave all hello default task values.</span></span> <span data-ttu-id="ab1d8-158">Altında **alma kaynakları**, o hello olun *mywebapp şeklindedir* depo ve *ana* şube seçilir.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-158">Under **Get sources**, ensure that hello *myWebApp* repository and *master* branch are selected.</span></span>

    ![Yapı tanımı Team Services projesi oluşturun](media/tutorial-vsts-iis-cicd/create_build_definition.png)

6. <span data-ttu-id="ab1d8-160">Merhaba üzerinde **Tetikleyicileri** sekmesinde, hello kaydırıcıyı **Bu tetikleyici etkinleştirmek** çok*etkin*.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-160">On hello **Triggers** tab, move hello slider for **Enable this trigger** too*Enabled*.</span></span>
7. <span data-ttu-id="ab1d8-161">Merhaba derleme tanımı ve sıra seçerek yeni bir yapı Kaydet **sıraya & Kaydet** , ardından **sıraya & Kaydet** yeniden.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-161">Save hello build definition and queue a new build by selecting **Save & queue** , then **Save & queue** again.</span></span> <span data-ttu-id="ab1d8-162">Merhaba Varsayılanları bırakabilir ve seçin **sıra**.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-162">Leave hello defaults and select **Queue**.</span></span>

<span data-ttu-id="ab1d8-163">Merhaba derleme üzerinde barındırılan bir aracısı, zamanlanmış olarak izleme toobuild sonra başlar.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-163">Watch as hello build is scheduled on a hosted agent, then begins toobuild.</span></span> <span data-ttu-id="ab1d8-164">Merhaba, benzer toohello aşağıdaki örneğine çıktı:</span><span class="sxs-lookup"><span data-stu-id="ab1d8-164">hello output is similar toohello following example:</span></span>

![Team Services projesinin başarılı derleme](media/tutorial-vsts-iis-cicd/successful_build.png)


## <a name="create-virtual-machine"></a><span data-ttu-id="ab1d8-166">Sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="ab1d8-166">Create virtual machine</span></span>
<span data-ttu-id="ab1d8-167">tooprovide platform toorun ASP.NET web uygulamanızı IIS çalışan bir Windows sanal makine gerekir.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-167">tooprovide a platform toorun your ASP.NET web app, you need a Windows virtual machine that runs IIS.</span></span> <span data-ttu-id="ab1d8-168">Team Services kullanan bir aracı toointeract hello IIS örneğiyle kod tamamlama ve derlemeleri tetiklenen.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-168">Team Services uses an agent toointeract with hello IIS instance as you commit code and builds are triggered.</span></span>

<span data-ttu-id="ab1d8-169">Kullanarak bir Windows Server 2016 VM oluşturma [bu komut dosyası örneği](../scripts/virtual-machines-windows-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ab1d8-169">Create a Windows Server 2016 VM using [this script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json).</span></span> <span data-ttu-id="ab1d8-170">Merhaba betik toorun birkaç dakika sürer ve hello VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-170">It takes a few minutes for hello script toorun and create hello VM.</span></span> <span data-ttu-id="ab1d8-171">Merhaba VM oluşturulduktan sonra bağlantı noktası 80 web trafiği için açık [Ekle AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.resources/new-azurermresourcegroup) gibi:</span><span class="sxs-lookup"><span data-stu-id="ab1d8-171">Once hello VM has been created, open port 80 for web traffic with [Add-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.resources/new-azurermresourcegroup) as follows:</span></span>

```powershell
Get-AzureRmNetworkSecurityGroup `
  -ResourceGroupName $resourceGroup `
  -Name "myNetworkSecurityGroup" | `
Add-AzureRmNetworkSecurityRuleConfig `
  -Name "myNetworkSecurityGroupRuleWeb" `
  -Protocol "Tcp" `
  -Direction "Inbound" `
  -Priority "1001" `
  -SourceAddressPrefix "*" `
  -SourcePortRange "*" `
  -DestinationAddressPrefix "*" `
  -DestinationPortRange "80" `
  -Access "Allow" | `
Set-AzureRmNetworkSecurityGroup
```

<span data-ttu-id="ab1d8-172">tooconnect tooyour VM elde hello ortak IP adresiyle [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) gibi:</span><span class="sxs-lookup"><span data-stu-id="ab1d8-172">tooconnect tooyour VM, obtain hello public IP address with [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) as follows:</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName $resourceGroup | Select IpAddress
```

<span data-ttu-id="ab1d8-173">Uzak Masaüstü oturumu tooyour VM oluşturun:</span><span class="sxs-lookup"><span data-stu-id="ab1d8-173">Create a remote desktop session tooyour VM:</span></span>

```cmd
mstsc /v:<publicIpAddress>
```

<span data-ttu-id="ab1d8-174">Hello VM, açık bir **yönetici PowerShell** komut istemi.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-174">On hello VM, open an **Administrator PowerShell** command prompt.</span></span> <span data-ttu-id="ab1d8-175">IIS ve gerekli .NET özellikleri gibi yükleyin:</span><span class="sxs-lookup"><span data-stu-id="ab1d8-175">Install IIS and required .NET features as follows:</span></span>

```powershell
Install-WindowsFeature Web-Server,Web-Asp-Net45,NET-Framework-Features
```


## <a name="create-deployment-group"></a><span data-ttu-id="ab1d8-176">Dağıtım grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="ab1d8-176">Create deployment group</span></span>
<span data-ttu-id="ab1d8-177">Merhaba web çıkışı toopush paket toohello IIS sunucusu dağıtabilir, Team Services içinde bir dağıtım grubu tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-177">toopush out hello web deploy package toohello IIS server, you define a deployment group in Team Services.</span></span> <span data-ttu-id="ab1d8-178">Bu grup, hizmetleri ve derlemeleri tamamlanan kodu tooTeam commit olarak hangi sunucuların yeni yapılar hello hedefinin olduğunu toospecify sağlar.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-178">This group allows you toospecify which servers are hello target of new builds as you commit code tooTeam Services and builds are completed.</span></span>

1. <span data-ttu-id="ab1d8-179">Team Services içinde seçin **yapı & yayın** ve ardından **dağıtım grupları**.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-179">In Team Services, choose **Build & Release** and then select **Deployment groups**.</span></span>
2. <span data-ttu-id="ab1d8-180">Seçin **eklemek dağıtım grubu**.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-180">Choose **Add Deployment group**.</span></span>
3. <span data-ttu-id="ab1d8-181">Merhaba grubu için bir ad girin *myIIS*seçeneğini belirleyip **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-181">Enter a name for hello group, such as *myIIS*, then select **Create**.</span></span>
4. <span data-ttu-id="ab1d8-182">Merhaba, **kaydetmek makineler** bölümünde, sağlamak *Windows* seçilir ve ardından çok olarak hello kutuyu**kişisel erişim belirteci hello komut dosyasındaki kimlik doğrulaması için kullanmak**.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-182">In hello **Register machines** section, ensure *Windows* is selected, then check hello box too**Use a personal access token in hello script for authentication**.</span></span>
5. <span data-ttu-id="ab1d8-183">Seçin **kopyalama komut dosyası tooclipboard**.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-183">Select **Copy script tooclipboard**.</span></span>


### <a name="add-iis-vm-toohello-deployment-group"></a><span data-ttu-id="ab1d8-184">IIS VM toohello dağıtım grubu Ekle</span><span class="sxs-lookup"><span data-stu-id="ab1d8-184">Add IIS VM toohello deployment group</span></span>
<span data-ttu-id="ab1d8-185">Oluşturulan hello dağıtım grubuyla her IIS örneği toohello grubuna ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-185">With hello deployment group created, add each IIS instance toohello group.</span></span> <span data-ttu-id="ab1d8-186">Team Services yükler ve yeni web aldığı VM dağıtmak hello üzerinde bir aracı yapılandıran bir komut dosyası oluşturduğu paketleri sonra tooIIS uygular.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-186">Team Services generates a script that downloads and configures an agent on hello VM that receives new web deploy packages then applies it tooIIS.</span></span>

1. <span data-ttu-id="ab1d8-187">Merhaba edilene **yönetici PowerShell** , VM oturum yapıştırın ve Team Services kopyalanan hello komut dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-187">Back in hello **Administrator PowerShell** session on your VM, paste and run hello script copied from Team Services.</span></span>
2. <span data-ttu-id="ab1d8-188">Merhaba aracısına yönelik, istendiğinde tooconfigure etiketleri seçtiğinizde *Y* ve girin *web*.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-188">When prompted tooconfigure tags for hello agent, choose *Y* and enter *web*.</span></span>
3. <span data-ttu-id="ab1d8-189">Merhaba kullanıcı hesabı için istendiğinde basın *dönmek* tooaccept hello Varsayılanları.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-189">When prompted for hello user account, press *Return* tooaccept hello defaults.</span></span>
4. <span data-ttu-id="ab1d8-190">Merhaba betik toofinish bir iletiyle bekleyin *hizmet vstsagent.account.computername başarıyla başlatıldı*.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-190">Wait for hello script toofinish with a message *Service vstsagent.account.computername started successfully*.</span></span>
5. <span data-ttu-id="ab1d8-191">Merhaba, **dağıtım grupları** hello sayfasının **yapı & yayın** menüsü, açık hello *myIIS* dağıtım grubu.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-191">In hello **Deployment groups** page of hello **Build & Release** menu, open hello *myIIS* deployment group.</span></span> <span data-ttu-id="ab1d8-192">Merhaba üzerinde **makineler** sekmesinde, VM'yi listelenmiş olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-192">On hello **Machines** tab, verify that your VM is listed.</span></span>

    ![VM tooTeam Hizmetleri dağıtım grubuna başarıyla eklendi](media/tutorial-vsts-iis-cicd/deployment_group.png)


## <a name="create-release-definition"></a><span data-ttu-id="ab1d8-194">Yayın tanımı oluşturun</span><span class="sxs-lookup"><span data-stu-id="ab1d8-194">Create release definition</span></span>
<span data-ttu-id="ab1d8-195">toopublish derlemeleriniz, Team Services içinde bir yayın tanımı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-195">toopublish your builds, you create a release definition in Team Services.</span></span> <span data-ttu-id="ab1d8-196">Bu tanım, uygulamanızın başarılı bir yapı tarafından otomatik olarak başlatılır.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-196">This definition is triggered automatically by a successful build of your application.</span></span> <span data-ttu-id="ab1d8-197">Merhaba dağıtım grubu toopush, web dağıtımı için paketi seçin ve hello uygun IIS ayarlarını tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-197">You choose hello deployment group toopush your web deploy package to, and define hello appropriate IIS settings.</span></span>

1. <span data-ttu-id="ab1d8-198">Seçin **yapı & yayın**seçeneğini belirleyip **derlemeler**.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-198">Choose **Build & Release**, then select **Builds**.</span></span> <span data-ttu-id="ab1d8-199">Bir önceki adımda oluşturduğunuz hello derleme tanımı seçin.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-199">Choose hello build definition created in a previous step.</span></span>
2. <span data-ttu-id="ab1d8-200">Altında **yakın zamanda tamamlandı**hello en son yapı seçin, ardından seçin **sürüm**.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-200">Under **Recently completed**, choose hello most recent build, then select **Release**.</span></span>
3. <span data-ttu-id="ab1d8-201">Seçin **Evet** toocreate yayın tanımı.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-201">Choose **Yes** toocreate a release definition.</span></span>
4. <span data-ttu-id="ab1d8-202">Merhaba seçin **boş** şablonu, ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-202">Choose hello **Empty** template, then select **Next**.</span></span>
5. <span data-ttu-id="ab1d8-203">Merhaba proje ve kaynak yapı tanımı, projenizi ile doldurulur doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-203">Verify hello project and source build definition are populated with your project.</span></span>
6. <span data-ttu-id="ab1d8-204">Select hello **sürekli dağıtım** onay kutusunu işaretleyin ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-204">Select hello **Continuous deployment** check box, then select **Create**.</span></span>
7. <span data-ttu-id="ab1d8-205">Merhaba açılan kutudan sonraki çok seçin**+ görev ekleme** ve *bir dağıtım grubu aşaması eklemek*.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-205">Select hello drop-down box next too**+ Add tasks** and choose *Add a deployment group phase*.</span></span>
    
    ![Team Services içinde görev toorelease tanımı Ekle](media/tutorial-vsts-iis-cicd/add_release_task.png)

8. <span data-ttu-id="ab1d8-207">Seçin **Ekle** sonraki çok**IIS Web uygulama Deploy(Preview)**seçeneğini belirleyip **Kapat**.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-207">Choose **Add** next too**IIS Web App Deploy(Preview)**, then select **Close**.</span></span>
9. <span data-ttu-id="ab1d8-208">Select hello **dağıtım grubu üzerinde çalışan** üst görev.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-208">Select hello **Run on deployment group** parent task.</span></span>
    1. <span data-ttu-id="ab1d8-209">İçin **dağıtım grubu**seçin hello dağıtım grubunu daha önce olduğu gibi oluşturulan *myIIS*.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-209">For **Deployment Group**, select hello deployment group you created earlier, such as *myIIS*.</span></span>
    2. <span data-ttu-id="ab1d8-210">Merhaba, **makine etiketleri** kutusunda **Ekle** ve hello seçin *web* etiketi.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-210">In hello **Machine tags** box, select **Add** and choose hello *web* tag.</span></span>
    
    ![IIS için yayın tanımı dağıtım grubu görevi](media/tutorial-vsts-iis-cicd/release_definition_iis.png)
 
11. <span data-ttu-id="ab1d8-212">Select hello **Dağıt: IIS Web uygulamasını dağıtmak** görev tooconfigure IIS örneği aşağıdaki gibi ayarları:</span><span class="sxs-lookup"><span data-stu-id="ab1d8-212">Select hello **Deploy: IIS Web App Deploy** task tooconfigure your IIS instance settings as follows:</span></span>
    1. <span data-ttu-id="ab1d8-213">İçin **Web sitesi adı**, girin *varsayılan Web sitesi*.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-213">For **Website Name**, enter *Default Web Site*.</span></span>
    2. <span data-ttu-id="ab1d8-214">Tüm hello diğer varsayılan ayarları bırakın.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-214">Leave all hello other default settings.</span></span>
12. <span data-ttu-id="ab1d8-215">Seçin **kaydetmek**seçeneğini belirleyip **Tamam** iki kez.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-215">Choose **Save**, then select **OK** twice.</span></span>


## <a name="create-a-release-and-publish"></a><span data-ttu-id="ab1d8-216">Sürüm oluşturma ve yayımlama</span><span class="sxs-lookup"><span data-stu-id="ab1d8-216">Create a release and publish</span></span>
<span data-ttu-id="ab1d8-217">Şimdi web gönderebilir paket yeni bir sürüm olarak dağıtın.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-217">You can now push your web deploy package as a new release.</span></span> <span data-ttu-id="ab1d8-218">Bu adım hello dağıtım grubunun parçası olduğundan, hello web iter her örneği hello Aracısı ile iletişim kurar paket dağıtın ve ardından IIS toorun güncelleştirilmiş Merhaba web uygulaması yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-218">This step communicates with hello agent on each instance that is part of hello deployment group, pushes hello web deploy package, then configures IIS toorun hello updated web application.</span></span>

1. <span data-ttu-id="ab1d8-219">Yayın tanımınızı seçin **+ yayın**, ardından **oluşturma yayın**.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-219">In your release definition, select **+ Release**, then choose **Create Release**.</span></span>
2. <span data-ttu-id="ab1d8-220">İle birlikte Hello son yapı hello aşağı açılan listesinde seçili olduğunu doğrulayın **dağıtım otomatik: sürüm oluşturulduktan sonra**.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-220">Verify that hello latest build is selected in hello drop-down list, along with **Automated deployment: After release creation**.</span></span> <span data-ttu-id="ab1d8-221">**Oluştur**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-221">Select **Create**.</span></span>
3. <span data-ttu-id="ab1d8-222">Küçük bir başlık yayın tanımınızı hello üstte gibi görünen *yayın 'Sürüm 1' oluşturulan*.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-222">A small banner appears across hello top of your release definition, such as *Release 'Release-1' has been created*.</span></span> <span data-ttu-id="ab1d8-223">Select hello yayın bağlantısı.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-223">Select hello release link.</span></span>
4. <span data-ttu-id="ab1d8-224">Açık hello **günlükleri** sekmesinde toowatch hello yayın devam ediyor.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-224">Open hello **Logs** tab toowatch hello release progress.</span></span>
    
    ![Paket gönderme dağıtımı ve başarılı Team Services sürüm](media/tutorial-vsts-iis-cicd/successful_release.png)

5. <span data-ttu-id="ab1d8-226">Merhaba yayın tamamlandıktan sonra bir web tarayıcısı açın ve VM hello ortak işlenen madde adresini girin.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-226">After hello release is complete, open a web browser and enter hello public IIP address of your VM.</span></span> <span data-ttu-id="ab1d8-227">ASP.NET web uygulamanız çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-227">Your ASP.NET web application is running.</span></span>

    ![IIS VM üzerinde çalışan ASP.NET web uygulaması](media/tutorial-vsts-iis-cicd/running_web_app.png)


## <a name="test-hello-whole-cicd-pipeline"></a><span data-ttu-id="ab1d8-229">Test hello tüm CI/CD ardışık düzen</span><span class="sxs-lookup"><span data-stu-id="ab1d8-229">Test hello whole CI/CD pipeline</span></span>
<span data-ttu-id="ab1d8-230">IIS üzerinde çalışan web uygulamanız ile Merhaba tüm CI/CD ardışık şimdi deneyin.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-230">With your web application running on IIS, now try hello whole CI/CD pipeline.</span></span> <span data-ttu-id="ab1d8-231">Visual Studio ve güncelleştirilmiş web sürümü tetikleyen bir yapı kodunuzu tetiklenir yürütme değişikliği yaptıktan sonra paketi tooIIS dağıtın:</span><span class="sxs-lookup"><span data-stu-id="ab1d8-231">After you make a change in Visual Studio and commit your code, a build is triggered which then triggers a release of your updated web deploy package tooIIS:</span></span>

1. <span data-ttu-id="ab1d8-232">Visual Studio'da hello açın **Çözüm Gezgini** penceresi.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-232">In Visual Studio, open hello **Solution Explorer** window.</span></span>
2. <span data-ttu-id="ab1d8-233">Tooand açık gidin *mywebapp şeklindedir | Görünümleri | Giriş | Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="ab1d8-233">Navigate tooand open *myWebApp | Views | Home | Index.cshtml*</span></span>
3. <span data-ttu-id="ab1d8-234">Satır 6 tooread düzenleyin:</span><span class="sxs-lookup"><span data-stu-id="ab1d8-234">Edit line 6 tooread:</span></span>

    `<h1>ASP.NET with VSTS and CI/CD!</h1>`

4. <span data-ttu-id="ab1d8-235">Merhaba dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-235">Save hello file.</span></span>
5. <span data-ttu-id="ab1d8-236">Açık hello **Takım Gezgini** penceresinde, select hello *mywebapp şeklindedir* proje sonra seçin **değişiklikleri**.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-236">Open hello **Team Explorer** window, select hello *myWebApp* project, then choose **Changes**.</span></span>
6. <span data-ttu-id="ab1d8-237">Bir kaydetme iletisi gibi girin *sınama CI/CD ardışık düzen*, ardından seçin **tamamlama tüm ve eşitleme** hello açılan menüsünden.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-237">Enter a commit message, such as *Testing CI/CD pipeline*, then choose **Commit All and Sync** from hello drop-down menu.</span></span>
7. <span data-ttu-id="ab1d8-238">Team Services çalışma alanında, yeni bir yapı hello kod tamamlama tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-238">In Team Services workspace, a new build is triggered from hello code commit.</span></span> 
    - <span data-ttu-id="ab1d8-239">Seçin **yapı & yayın**seçeneğini belirleyip **derlemeler**.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-239">Choose **Build & Release**, then select **Builds**.</span></span> 
    - <span data-ttu-id="ab1d8-240">Yapı tanımı seçin ve ardından hello **sıraya alınan & çalışan** yapı toowatch hello olarak yapı ilerler.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-240">Choose your build definition, then select hello **Queued & running** build toowatch as hello build progresses.</span></span>
9. <span data-ttu-id="ab1d8-241">Merhaba derleme başarılı olduktan sonra yeni bir sürüm tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-241">Once hello build is successful, a new release is triggered.</span></span>
    - <span data-ttu-id="ab1d8-242">Seçin **yapı & yayın**, ardından **sürümleri** toosee hello web dağıtım paketi tooyour IIS VM gönderilir.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-242">Choose **Build & Release**, then **Releases** toosee hello web deploy package pushed tooyour IIS VM.</span></span> 
    - <span data-ttu-id="ab1d8-243">Select hello **yenileme** simgesi tooupdate hello durumu.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-243">Select hello **Refresh** icon tooupdate hello status.</span></span> <span data-ttu-id="ab1d8-244">Ne zaman hello *ortamları* sütunda yeşil bir onay işareti görüntülenir, hello yayın tooIIS başarıyla dağıtılan.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-244">When hello *Environments* column shows a green check mark, hello release has successfully deployed tooIIS.</span></span>
11. <span data-ttu-id="ab1d8-245">Değişikliklerinizi toosee uygulanan, IIS Web tarayıcısında yenileyin.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-245">toosee your changes applied, refresh your IIS website in a browser.</span></span>

    ![IIS VM'de CI/CD ardışık düzen tarafından çalıştırılan ASP.NET web uygulaması](media/tutorial-vsts-iis-cicd/running_web_app_cicd.png)


## <a name="next-steps"></a><span data-ttu-id="ab1d8-247">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ab1d8-247">Next steps</span></span>

<span data-ttu-id="ab1d8-248">Bu öğreticide, bir ASP.NET web uygulamasını Team Services içinde oluşturulan ve yapılandırılan derleme ve sürüm tanımlarını toodeploy yeni web paketleri tooIIS her kod tamamlama üzerinde dağıtın.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-248">In this tutorial, you created an ASP.NET web application in Team Services and configured build and release definitions toodeploy new web deploy packages tooIIS on each code commit.</span></span> <span data-ttu-id="ab1d8-249">Şunları öğrendiniz:</span><span class="sxs-lookup"><span data-stu-id="ab1d8-249">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ab1d8-250">Bir ASP.NET web uygulaması tooa Team Services projesini Yayımla</span><span class="sxs-lookup"><span data-stu-id="ab1d8-250">Publish an ASP.NET web application tooa Team Services project</span></span>
> * <span data-ttu-id="ab1d8-251">Kod tamamlama tarafından tetiklenen bir yapı tanımı oluşturun</span><span class="sxs-lookup"><span data-stu-id="ab1d8-251">Create a build definition that is triggered by code commits</span></span>
> * <span data-ttu-id="ab1d8-252">IIS yükle ve azure'da bir sanal makinede Yapılandır</span><span class="sxs-lookup"><span data-stu-id="ab1d8-252">Install and configure IIS on a virtual machine in Azure</span></span>
> * <span data-ttu-id="ab1d8-253">Team Services içinde Hello IIS örnek tooa dağıtım grubu Ekle</span><span class="sxs-lookup"><span data-stu-id="ab1d8-253">Add hello IIS instance tooa deployment group in Team Services</span></span>
> * <span data-ttu-id="ab1d8-254">Bir yayın tanımı toopublish yeni web Oluştur paketleri tooIIS dağıtma</span><span class="sxs-lookup"><span data-stu-id="ab1d8-254">Create a release definition toopublish new web deploy packages tooIIS</span></span>
> * <span data-ttu-id="ab1d8-255">Test hello CI/CD ardışık düzen</span><span class="sxs-lookup"><span data-stu-id="ab1d8-255">Test hello CI/CD pipeline</span></span>

<span data-ttu-id="ab1d8-256">Toohello sonraki öğretici toolearn nasıl ilerlemek toosecure bir web sunucusu SSL sertifikaları ile.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-256">Advance toohello next tutorial toolearn how toosecure a web server with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ab1d8-257">SSL ile güvenli web sunucusu</span><span class="sxs-lookup"><span data-stu-id="ab1d8-257">Secure web server with SSL</span></span>](tutorial-secure-web-server.md)