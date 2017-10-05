---
title: "Bulut için kesintisiz teslim hizmetleri Azure içinde TFS ile | Microsoft Docs"
description: "Azure bulut uygulamaları için sürekli teslimini ayarlayın öğrenin. MSBuild komut satırı deyimleri ve PowerShell komut dosyaları için kod örnekleri."
services: cloud-services
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 4f3c93c6-5c82-4779-9d19-7404a01e82ca
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/12/2017
ms.author: kraigb
ms.openlocfilehash: 0979722b9ec715e91825c7aba74657451df6e83f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="continuous-delivery-for-cloud-services-in-azure"></a><span data-ttu-id="90201-104">Azure bulut Hizmetleri için devamlı teslim</span><span class="sxs-lookup"><span data-stu-id="90201-104">Continuous Delivery for Cloud Services in Azure</span></span>
<span data-ttu-id="90201-105">Bu makalede açıklanan işlemi Azure bulut uygulamaları için sürekli teslimini ayarlayın gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="90201-105">The process described in this article shows you how to set up continuous delivery for Azure cloud apps.</span></span> <span data-ttu-id="90201-106">Bu işlem, her kod iadesinden sonra paketleri otomatik olarak oluşturmanıza ve paketi Azure'da dağıtmanıza olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="90201-106">This process enables you to automatically create packages and deploy the package to Azure after every code check-in.</span></span> <span data-ttu-id="90201-107">Bu makalede açıklanan paket oluşturma işlemi eşdeğerdir **paket** Visual Studio komut ve yayımlama adımlarını eşdeğer **Yayımla** Visual Studio'da komutu.</span><span class="sxs-lookup"><span data-stu-id="90201-107">The package build process described in this article is equivalent to the **Package** command in Visual Studio, and the publishing steps are equivalent to the **Publish** command in Visual Studio.</span></span>
<span data-ttu-id="90201-108">Makale bir yapı sunucu MSBuild komut satırı deyimleri ve Windows PowerShell komut dosyaları oluşturmak için kullandığınız yöntemleri kapsar ve ayrıca isteğe bağlı olarak Visual Studio Team Foundation Server - ekip tanımları kullanacak şekilde yapılandırmak nasıl gösterir MSBuild komutlar ve PowerShell komut dosyaları.</span><span class="sxs-lookup"><span data-stu-id="90201-108">The article covers the methods you would use to create a build server with MSBuild command-line statements and Windows PowerShell scripts, and it also demonstrates how to optionally configure Visual Studio Team Foundation Server - Team Build definitions to use the MSBuild commands and PowerShell scripts.</span></span> <span data-ttu-id="90201-109">Yapı ortamı ve Azure hedef ortamları için özelleştirilebilir işlemidir.</span><span class="sxs-lookup"><span data-stu-id="90201-109">The process is customizable for your build environment and Azure target environments.</span></span>

<span data-ttu-id="90201-110">Visual Studio Team Services, bunu daha kolay yapmak için Azure üzerinde barındırılan TFS sürümünü de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90201-110">You can also use Visual Studio Team Services, a version of TFS that is hosted in Azure, to do this more easily.</span></span> 

<span data-ttu-id="90201-111">Başlamadan önce uygulamanızı Visual Studio'dan yayımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="90201-111">Before you start, you should publish your application from Visual Studio.</span></span>
<span data-ttu-id="90201-112">Bu tüm kaynakların kullanılabilir ve başlatılmış olduğundan emin olmak için yayın işlemini otomatikleştirmek çalıştığınızda.</span><span class="sxs-lookup"><span data-stu-id="90201-112">This will ensure that all the resources are available and initialized when you attempt to automate the publication process.</span></span>

## <a name="1-configure-the-build-server"></a><span data-ttu-id="90201-113">1: derleme sunucusunu yapılandırın</span><span class="sxs-lookup"><span data-stu-id="90201-113">1: Configure the Build Server</span></span>
<span data-ttu-id="90201-114">MSBuild kullanarak bir Azure paketi oluşturabilmeniz için önce yapı sunucuda gerekli yazılım ve araçları yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="90201-114">Before you can create an Azure package by using MSBuild, you must install the required software and tools on the build server.</span></span>

<span data-ttu-id="90201-115">Visual Studio derleme sunucuya yüklenmesi gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="90201-115">Visual Studio is not required to be installed on the build server.</span></span> <span data-ttu-id="90201-116">Team Foundation Yapı Hizmeti yapı sunucunuzu yönetmek için kullanmak istiyorsanız,'ndaki yönergeleri izleyin [Team Foundation Yapı Hizmeti] [ Team Foundation Build Service] belgeleri.</span><span class="sxs-lookup"><span data-stu-id="90201-116">If you want to use Team Foundation Build Service to manage your build server, follow the instructions in the [Team Foundation Build Service][Team Foundation Build Service] documentation.</span></span>

1. <span data-ttu-id="90201-117">Yapı sunucuya yüklemek [.NET Framework 4.5.2][.NET Framework 4.5.2], MSBuild içerir.</span><span class="sxs-lookup"><span data-stu-id="90201-117">On the build server, install the [.NET Framework 4.5.2][.NET Framework 4.5.2], which includes MSBuild.</span></span>
2. <span data-ttu-id="90201-118">En son yükleme [.NET için Azure yazma araçları](https://azure.microsoft.com/develop/net/).</span><span class="sxs-lookup"><span data-stu-id="90201-118">Install the latest [Azure Authoring Tools for .NET](https://azure.microsoft.com/develop/net/).</span></span>
3. <span data-ttu-id="90201-119">Yükleme [.NET için Azure kitaplıkları](http://go.microsoft.com/fwlink/?LinkId=623519).</span><span class="sxs-lookup"><span data-stu-id="90201-119">Install the [Azure Libraries for .NET](http://go.microsoft.com/fwlink/?LinkId=623519).</span></span>
4. <span data-ttu-id="90201-120">Microsoft.WebApplication.targets dosyasını Visual Studio yüklemesinden yapı sunucuya kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="90201-120">Copy the Microsoft.WebApplication.targets file from a Visual Studio installation to the build server.</span></span>

   <span data-ttu-id="90201-121">Visual Studio'nun yüklü olan bir bilgisayarda bu dosyayı C: dizininde bulunan\\Program Files(x86)\\MSBuild\\Microsoft\\Visual Studio\\v14.0\\Web.</span><span class="sxs-lookup"><span data-stu-id="90201-121">On a computer with Visual Studio installed, this file is located in the directory C:\\Program Files(x86)\\MSBuild\\Microsoft\\VisualStudio\\v14.0\\WebApplications.</span></span> <span data-ttu-id="90201-122">Derleme sunucusundaki aynı dizine kopyalamalısınız.</span><span class="sxs-lookup"><span data-stu-id="90201-122">You should copy it to the same directory on the build server.</span></span>
5. <span data-ttu-id="90201-123">Yükleme [Visual Studio için Azure Araçları](https://www.visualstudio.com/features/azure-tools-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="90201-123">Install the [Azure Tools for Visual Studio](https://www.visualstudio.com/features/azure-tools-vs.aspx).</span></span>

## <a name="2-build-a-package-using-msbuild-commands"></a><span data-ttu-id="90201-124">2: MSBuild komutları kullanarak bir paket oluşturun</span><span class="sxs-lookup"><span data-stu-id="90201-124">2: Build a Package using MSBuild Commands</span></span>
<span data-ttu-id="90201-125">Bu bölümde, bir Azure paketi derlemeler MSBuild komut oluşturmak açıklar.</span><span class="sxs-lookup"><span data-stu-id="90201-125">This section describes how to construct an MSBuild command that builds an Azure package.</span></span> <span data-ttu-id="90201-126">Bu adımı her şeyin doğru şekilde yapılandırıldığını ve MSBuild komut ne yapmak istiyorsunuz yaptığını doğrulamak için yapı sunucusunda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="90201-126">Run this step on the build server to verify that everything is configured correctly and that the MSBuild command does what you want it to do.</span></span> <span data-ttu-id="90201-127">Ya da bu komut satırı derleme sunucusundaki mevcut derleme betiklerini ekleyebileceğiniz veya komut satırı derleme TFS tanımında, sonraki bölümde açıklandığı gibi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90201-127">You can either add this command line to existing build scripts on the build server, or you can use the command line in a TFS Build Definition, as described in the next section.</span></span> <span data-ttu-id="90201-128">Komut satırı parametreleri ve MSBuild hakkında daha fazla bilgi için bkz: [MSBuild komut satırı başvurusu](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="90201-128">For more information about command-line parameters and MSBuild, see [MSBuild Command Line Reference](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span></span>

1. <span data-ttu-id="90201-129">Visual Studio derleme sunucuda yüklüyse, bulun ve seçin **Visual Studio komut istemi** içinde **Visual Studio Araçları** Windows klasörü.</span><span class="sxs-lookup"><span data-stu-id="90201-129">If Visual Studio is installed on the build server, locate and choose **Visual Studio Command Prompt** in the **Visual Studio Tools** folder in Windows.</span></span>

   <span data-ttu-id="90201-130">Visual Studio derleme sunucuda yüklü değilse, bir komut istemi açın ve MSBuild.exe yola erişilebilir olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="90201-130">If Visual Studio is not installed on the build server, open a command prompt and make sure that MSBuild.exe is accessible on the path.</span></span> <span data-ttu-id="90201-131">MSBuild yolu % WINDIR % .NET Framework yüklenmiş\\Microsoft.NET\\Framework\\*sürüm*.</span><span class="sxs-lookup"><span data-stu-id="90201-131">MSBuild is installed with the .NET Framework in the path %WINDIR%\\Microsoft.NET\\Framework\\*Version*.</span></span> <span data-ttu-id="90201-132">Örneğin, .NET Framework 4 yüklü olduğunda MSBuild.exe PATH ortam değişkenine eklemek için komut istemine aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="90201-132">For example, to add MSBuild.exe to the PATH environment variable when you have .NET Framework 4 installed, type the following command at the command prompt:</span></span>

       set PATH=%PATH%;"C:\Windows\Microsoft.NET\Framework\v4.0.30319"
2. <span data-ttu-id="90201-133">Komut isteminde, oluşturmak istediğiniz Azure proje dosyasını içeren klasöre gidin.</span><span class="sxs-lookup"><span data-stu-id="90201-133">At the command prompt, navigate to the folder containing the Azure project file that you want to build.</span></span>
3. <span data-ttu-id="90201-134">/ Target ile MSBuild çalıştırın: Aşağıdaki örnekte olduğu gibi seçeneği yayımlama:</span><span class="sxs-lookup"><span data-stu-id="90201-134">Run MSBuild with the /target:Publish option as in the following example:</span></span>

       MSBuild /target:Publish

   <span data-ttu-id="90201-135">Bu seçenek /t kısaltılır: yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="90201-135">This option can be abbreviated as /t:Publish.</span></span> <span data-ttu-id="90201-136">Azure SDK yüklü olduğunda MSBuild /t:Publish seçeneğinde Visual Studio'da kullanılabilen Yayımla komutları ile karıştırılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="90201-136">The /t:Publish option in MSBuild should not be confused with the Publish commands available in Visual Studio when you have the Azure SDK installed.</span></span> <span data-ttu-id="90201-137">/T: seçeneği yalnızca derlemeleri Azure paketleri yayımlama.</span><span class="sxs-lookup"><span data-stu-id="90201-137">The /t:Publish option only builds the Azure packages.</span></span> <span data-ttu-id="90201-138">Visual Studio'da yayımlama komutları gibi paketleri dağıtmaz.</span><span class="sxs-lookup"><span data-stu-id="90201-138">It does not deploy the packages as the Publish commands in Visual Studio do.</span></span>

   <span data-ttu-id="90201-139">İsteğe bağlı olarak, bir MSBuild parametresi olarak proje adı belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90201-139">Optionally, you can specify the project name as an MSBuild parameter.</span></span> <span data-ttu-id="90201-140">Belirtilmezse, geçerli dizin kullanılır.</span><span class="sxs-lookup"><span data-stu-id="90201-140">If not specified, the current directory is used.</span></span> <span data-ttu-id="90201-141">MSBuild komut satırı seçenekleri hakkında daha fazla bilgi için bkz: [MSBuild komut satırı başvurusu](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="90201-141">For more information about MSBuild command line options, see [MSBuild Command Line Reference](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span></span>
4. <span data-ttu-id="90201-142">Çıktı bulun.</span><span class="sxs-lookup"><span data-stu-id="90201-142">Locate the output.</span></span> <span data-ttu-id="90201-143">Varsayılan olarak, bu komut bir dizin projenin kök klasörüne göre gibi oluşturur *ProjectDir*\\bin\\*yapılandırma*\\app.publish \\.</span><span class="sxs-lookup"><span data-stu-id="90201-143">By default, this command creates a directory in relation to the root folder for the project, such as *ProjectDir*\\bin\\*Configuration*\\app.publish\\.</span></span> <span data-ttu-id="90201-144">Bir Azure projesi derlerken, iki dosya, paket dosyası ve eşlik eden yapılandırma dosyası oluşturun:</span><span class="sxs-lookup"><span data-stu-id="90201-144">When you build an Azure project, you generate two files, the package file itself and the accompanying configuration file:</span></span>

   * <span data-ttu-id="90201-145">Project.cspkg</span><span class="sxs-lookup"><span data-stu-id="90201-145">Project.cspkg</span></span>
   * <span data-ttu-id="90201-146">ServiceConfiguration. *TargetProfile*.cscfg</span><span class="sxs-lookup"><span data-stu-id="90201-146">ServiceConfiguration.*TargetProfile*.cscfg</span></span>

   <span data-ttu-id="90201-147">Varsayılan olarak, her Azure projesi yerel (hata ayıklama) yapılar ve bulut (hazırlık veya üretim) yapılar için başka bir hizmet yapılandırma dosyası (.cscfg dosyası) içerir, ancak ekleyip gerektiği gibi hizmet yapılandırma dosyalarını kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90201-147">By default, each Azure project includes one service configuration file (.cscfg file) for local (debugging) builds and another for cloud (staging or production) builds, but you can add or remove service configuration files as needed.</span></span> <span data-ttu-id="90201-148">Visual Studio içinde bir paket yapılandırdığınızda, paket dahil etmek için hangi hizmet yapılandırma dosyası istenir.</span><span class="sxs-lookup"><span data-stu-id="90201-148">When you build a package within Visual Studio, you will be asked which service configuration file to include alongside the package.</span></span>
5. <span data-ttu-id="90201-149">Hizmet yapılandırma dosyası belirtin.</span><span class="sxs-lookup"><span data-stu-id="90201-149">Specify the service configuration file.</span></span> <span data-ttu-id="90201-150">MSBuild kullanarak bir paket oluşturduğunuzda, yerel hizmet yapılandırma dosyası varsayılan olarak dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="90201-150">When you build a package by using MSBuild, the local service configuration file is included by default.</span></span> <span data-ttu-id="90201-151">Farklı hizmet yapılandırma dosyası eklemek için aşağıdaki örnekte olduğu gibi MSBuild komut TargetProfile özelliğini ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="90201-151">To include a different service configuration file, set the TargetProfile property of the MSBuild command, as in the following example:</span></span>

       MSBuild /t:Publish /p:TargetProfile=Cloud
6. <span data-ttu-id="90201-152">Çıktı konumunu belirtin.</span><span class="sxs-lookup"><span data-stu-id="90201-152">Specify the location for the output.</span></span> <span data-ttu-id="90201-153">/P:PublishDir kullanarak yolunu ayarlama =*Directory* \\ seçeneği, aşağıdaki örnekte olduğu gibi sondaki eğik çizgi ayırıcı dahil olmak üzere:</span><span class="sxs-lookup"><span data-stu-id="90201-153">Set the path by using the /p:PublishDir=*Directory*\\ option, including the trailing backslash separator, as in the following example:</span></span>

       MSBuild /target:Publish /p:PublishDir=\\myserver\drops\

   <span data-ttu-id="90201-154">Oluşturulan ve projelerinizi oluşturma ve bunları Azure bir pakete birleştirmek için uygun bir MSBuild komut satırı test sonra bu komut satırı derleme komutlarınızı ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90201-154">Once you've constructed and tested an appropriate MSBuild command line to build your projects and combine them into an Azure package, you can add this command line to your build scripts.</span></span> <span data-ttu-id="90201-155">Yapı sunucunuz özel komut dosyaları kullanıyorsa, bu işlem, özel derleme işlem ayrıntılarını bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="90201-155">If your build server uses custom scripts, this process will depend on the specifics of your custom build process.</span></span> <span data-ttu-id="90201-156">Ardından bir yapı ortamı olarak TFS kullanıyorsanız, yapı işleminizin Azure paketi yapı eklemek için yönergeleri sonraki adımda izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90201-156">If you are using TFS as a build environment, then you can follow the instructions in the next step to add the Azure package build to your build process.</span></span>

## <a name="3-build-a-package-using-tfs-team-build"></a><span data-ttu-id="90201-157">3: TFS ekip kullanarak bir paket oluşturun</span><span class="sxs-lookup"><span data-stu-id="90201-157">3: Build a Package using TFS Team Build</span></span>
<span data-ttu-id="90201-158">Varsa Team Foundation Server (TFS) bir yapı denetleyicisi ve yapı server ayarlanmış bir TFS yapı makine olarak ayarlayın, sonra Azure paketiniz için otomatikleştirilmiş bir yapıyı isteğe bağlı olarak ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90201-158">If you have Team Foundation Server (TFS) set up as a build controller and the build server set up as a TFS build machine, then you can optionally set up an automated build for your Azure package.</span></span> <span data-ttu-id="90201-159">Ayarlama ve Team Foundation server yapı sistem olarak kullanma konusunda daha fazla bilgi için bkz: [derleme sisteminiz genişletme][Scale out your build system].</span><span class="sxs-lookup"><span data-stu-id="90201-159">For information on how to set up and use Team Foundation server as a build system, see [Scale out your build system][Scale out your build system].</span></span> <span data-ttu-id="90201-160">Özellikle, aşağıdaki yordamda açıklandığı gibi yapı sunucunuz yapılandırdığınız varsayılmaktadır [dağıtma ve bir yapı sunucusunu yapılandırmak][Deploy and configure a build server], ve bir takım projesi oluşturduğunuz Bulutu oluşturulmuş takım projesinde hizmet projesi.</span><span class="sxs-lookup"><span data-stu-id="90201-160">In particular, the following procedure assumes that you have configured your build server as described in [Deploy and configure a build server][Deploy and configure a build server], and that you have created a team project, created a cloud service project in the team project.</span></span>

<span data-ttu-id="90201-161">Azure paketleri oluşturmak için TFS yapılandırmak için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="90201-161">To configure TFS to build Azure packages, perform the following steps:</span></span>

1. <span data-ttu-id="90201-162">Visual Studio geliştirme bilgisayarınızda, Görünüm menüsünde seçin **Takım Gezgini**, veya Ctrl + seçin\\, Ctrl + M.</span><span class="sxs-lookup"><span data-stu-id="90201-162">In Visual Studio on your development computer, on the View menu, choose **Team Explorer**, or choose Ctrl+\\, Ctrl+M.</span></span> <span data-ttu-id="90201-163">Takım Gezgini penceresinde **derlemeler** düğümü veya seçin **derlemeler** sayfasında ve seçin **yeni yapı tanımı**.</span><span class="sxs-lookup"><span data-stu-id="90201-163">In the Team Explorer window, expand the **Builds** node or choose the **Builds** page, and choose **New Build Definition**.</span></span>

   ![Yeni bir yapı tanımı seçeneği][0]
2. <span data-ttu-id="90201-165">Seçin **tetikleyici** sekmesini tıklatın ve oluşturulacak paket istediğinizde için istenen koşulları belirtin.</span><span class="sxs-lookup"><span data-stu-id="90201-165">Choose the **Trigger** tab, and specify the desired conditions for when you want the package to be built.</span></span> <span data-ttu-id="90201-166">Örneğin, **sürekli tümleştirme** bir kaynak denetim her giriş paketi oluşturmak için oluşur.</span><span class="sxs-lookup"><span data-stu-id="90201-166">For example, specify **Continuous Integration** to build the package whenever a source control check-in occurs.</span></span>
3. <span data-ttu-id="90201-167">Seçin **kaynak ayarları** sekmesinde ve proje klasörünüzdeki listelendiğinden emin olun **kaynak denetimi klasörü** sütun ve durum **etkin**.</span><span class="sxs-lookup"><span data-stu-id="90201-167">Choose the **Source Settings** tab, and make sure your project folder is listed in the **Source Control Folder** column, and the status is **Active**.</span></span>
4. <span data-ttu-id="90201-168">Seçin **Yapı Varsayılanları** sekmesini tıklatın ve yapı denetleyicisi altında yapı sunucu adını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="90201-168">Choose the **Build Defaults** tab, and under Build controller, verify the name of the build server.</span></span>  <span data-ttu-id="90201-169">Ayrıca, seçeneği **kopyalama yapı çıktısını aşağıdaki bırakma klasörüne** ve istenilen bırakma konumu belirtin.</span><span class="sxs-lookup"><span data-stu-id="90201-169">Also, choose the option **Copy build output to the following drop folder** and specify the desired drop location.</span></span>
5. <span data-ttu-id="90201-170">Seçin **işlem** sekmesi. İşlem sekmesinde altında varsayılan şablonu seçin **yapı**, zaten seçili değilse ve genişletin, proje seçme **Gelişmiş** bölümüne **yapı** bölümü kılavuzunun.</span><span class="sxs-lookup"><span data-stu-id="90201-170">Choose the **Process** tab. On the Process tab, choose the default template, under **Build**, choose the project if it is not already selected, and expand the **Advanced** section in the **Build** section of the grid.</span></span>
6. <span data-ttu-id="90201-171">Seçin **MSBuild bağımsız değişkenleri**, yukarıda 2. adımda açıklandığı gibi uygun MSBuild komut satırı bağımsız değişkenleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="90201-171">Choose **MSBuild Arguments**, and set the appropriate MSBuild command line arguments as described in Step 2 above.</span></span> <span data-ttu-id="90201-172">Örneğin **/t: /p:PublishDir yayımlama =\\\\myserver\\bırakır\\**  bir paket oluşturmak ve paket dosyaları konumuna kopyalamak için \\ \\ myserver\\bırakır\\:</span><span class="sxs-lookup"><span data-stu-id="90201-172">For example, enter **/t:Publish /p:PublishDir=\\\\myserver\\drops\\** to build a package and copy the package files to the location \\\\myserver\\drops\\:</span></span>

   ![MSBuild bağımsız değişkenleri][2]

   > [!NOTE]
   > <span data-ttu-id="90201-174">Bir genel paylaşıma dosyaları kopyalanıyor geliştirme bilgisayarınıza paketlerinden el ile dağıtmak kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="90201-174">Copying the files to a public share makes it easier to manually deploy the packages from your development computer.</span></span>
7. <span data-ttu-id="90201-175">Projeniz için bir değişiklik denetleyerek test, derleme adımının başarılı ya da yeni bir yapıyı sıraya.</span><span class="sxs-lookup"><span data-stu-id="90201-175">Test the success of your build step by checking in a change to your project, or queue up a new build.</span></span> <span data-ttu-id="90201-176">Takım Gezgini'nde, yeni bir derleme kuyruğuna sağ **tüm yapı tanımlarını** ve ardından **yeni yapıyı sıraya al**.</span><span class="sxs-lookup"><span data-stu-id="90201-176">To queue up a new build, in the Team Explorer, right-click **All Build Definitions,** and then choose **Queue New Build**.</span></span>

## <a name="4-publish-a-package-using-a-powershell-script"></a><span data-ttu-id="90201-177">4: bir PowerShell komut dosyası kullanarak bir paket yayımlama</span><span class="sxs-lookup"><span data-stu-id="90201-177">4: Publish a Package using a PowerShell Script</span></span>
<span data-ttu-id="90201-178">Bu bölüm, bulut uygulama paketi çıktı isteğe bağlı parametreleri kullanarak Azure'a yayımlayacak bir Windows PowerShell betiği oluşturmak açıklar.</span><span class="sxs-lookup"><span data-stu-id="90201-178">This section describes how to construct a Windows PowerShell script that will publish the Cloud app package output to Azure using optional parameters.</span></span> <span data-ttu-id="90201-179">Bu komut dosyası derleme adım sonra özel derleme otomasyonunuz çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="90201-179">This script can be called after the build step in your custom build automation.</span></span> <span data-ttu-id="90201-180">Ayrıca, Visual Studio TFS takım yapısı içinde işlem şablonu iş akışı etkinliklerden de çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="90201-180">It can also be called from Process Template workflow activities in Visual Studio TFS Team Build.</span></span>

1. <span data-ttu-id="90201-181">Yükleme [Azure PowerShell cmdlet'lerini] [ Azure PowerShell cmdlets] (v0.6.1 ya da daha yüksek).</span><span class="sxs-lookup"><span data-stu-id="90201-181">Install the [Azure PowerShell cmdlets][Azure PowerShell cmdlets] (v0.6.1 or higher).</span></span>
   <span data-ttu-id="90201-182">Bir ek yüklemek cmdlet kurulumu aşamasında seçin.</span><span class="sxs-lookup"><span data-stu-id="90201-182">During the cmdlet setup phase, choose to install as a snap-in.</span></span> <span data-ttu-id="90201-183">Önceki sürümler 2.x.x numaralı ancak bu resmi olarak desteklenen sürüm CodePlex sunulan eski sürümün yerine geçer unutmayın.</span><span class="sxs-lookup"><span data-stu-id="90201-183">Note that this officially supported version replaces the older version offered through CodePlex, although the previous versions were numbered 2.x.x.</span></span>
2. <span data-ttu-id="90201-184">Başlat menüsünü kullanarak Azure PowerShell'i başlatın veya başlangıç sayfası.</span><span class="sxs-lookup"><span data-stu-id="90201-184">Start Azure PowerShell using the Start menu or Start page.</span></span> <span data-ttu-id="90201-185">Bu yolla başlatırsanız, Azure PowerShell cmdlet'leri yüklenir.</span><span class="sxs-lookup"><span data-stu-id="90201-185">If you start in this way, the Azure PowerShell cmdlets will be loaded.</span></span>
3. <span data-ttu-id="90201-186">PowerShell komut isteminde, PowerShell cmdlet'leri kısmi komutunu girerek yüklendiğini doğrulamak `Get-Azure` ve deyim tamamlama için SEKME tuşuna basarak.</span><span class="sxs-lookup"><span data-stu-id="90201-186">At the PowerShell prompt, verify that the PowerShell cmdlets are loaded by entering the partial command `Get-Azure` and then pressing the Tab key for statement completion.</span></span>

   <span data-ttu-id="90201-187">Art arda SEKME tuşuna basın, çeşitli Azure PowerShell komutlarını görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="90201-187">If you press the Tab key repeatedly, you should see various Azure PowerShell commands.</span></span>
4. <span data-ttu-id="90201-188">Azure aboneliğinize .publishsettings dosyasından abonelik bilgilerinizi içe aktararak bağlanabildiğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="90201-188">Verify that you can connect to your Azure subscription by importing your subscription information from the .publishsettings file.</span></span>

   `Import-AzurePublishSettingsFile c:\scripts\WindowsAzure\default.publishsettings`

   <span data-ttu-id="90201-189">Komutunu girin</span><span class="sxs-lookup"><span data-stu-id="90201-189">Then enter the command</span></span>

   `Get-AzureSubscription`

   <span data-ttu-id="90201-190">Bu aboneliğiniz hakkında bilgi gösterir.</span><span class="sxs-lookup"><span data-stu-id="90201-190">This shows information about your subscription.</span></span> <span data-ttu-id="90201-191">Her şeyin doğru olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="90201-191">Verify that everything is correct.</span></span>
5. <span data-ttu-id="90201-192">Komut dosyaları klasörünüze c: olarak bu makalenin sonunda sağlanan komut dosyası şablonu kaydetmek\\betikleri\\WindowsAzure\\**PublishCloudService.ps1**.</span><span class="sxs-lookup"><span data-stu-id="90201-192">Save the script template provided at the end of this article to your scripts folder as c:\\scripts\\WindowsAzure\\**PublishCloudService.ps1**.</span></span>
6. <span data-ttu-id="90201-193">Komut parametreleri bölümünü gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="90201-193">Review the parameters section of the script.</span></span> <span data-ttu-id="90201-194">Ekleyin veya herhangi bir varsayılan değeri değiştirin.</span><span class="sxs-lookup"><span data-stu-id="90201-194">Add or modify any default values.</span></span> <span data-ttu-id="90201-195">Bu değerler, her zaman açık parametreleri geçirerek kılınabilir.</span><span class="sxs-lookup"><span data-stu-id="90201-195">These values can always be overridden by passing in explicit parameters.</span></span>
7. <span data-ttu-id="90201-196">Geçerli bulut hizmeti ve depolama hesapları Yayımla komut dosyası tarafından hedeflenebilir aboneliğinizde oluşturulur sağlamak.</span><span class="sxs-lookup"><span data-stu-id="90201-196">Ensure there are valid cloud service and storage accounts created in your subscription that can be targeted by the publish script.</span></span> <span data-ttu-id="90201-197">Depolama hesabı (blob depolama), karşıya yükleme ve dağıtım oluşturulurken dağıtım paketini ve yapılandırma dosyası geçici olarak depolamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="90201-197">The storage account (blob storage) will be used to upload and temporarily store the deployment package and config file while the deployment is being created.</span></span>

   * <span data-ttu-id="90201-198">Yeni bir bulut hizmeti oluşturmak için bu komut dosyasını çağırın veya kullanmak [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="90201-198">To create a new cloud service, you can call this script or use the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="90201-199">Bulut hizmeti adı tam etki alanı adının öneki olarak kullanılacak ve bu nedenle benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="90201-199">The cloud service name will be used as a prefix in a fully qualified domain name and hence it must be unique.</span></span>

         New-AzureService -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
   * <span data-ttu-id="90201-200">Yeni bir depolama hesabı oluşturmak için bu komut dosyasını çağırın veya kullanmak [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="90201-200">To create a new storage account, you can call this script or use the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="90201-201">Depolama hesabı adı tam etki alanı adının öneki olarak kullanılacak ve bu nedenle benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="90201-201">The storage account name will be used as a prefix in a fully qualified domain name and hence it must be unique.</span></span> <span data-ttu-id="90201-202">Bulut hizmeti olarak aynı adı kullanarak deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90201-202">You can try using the same name as the cloud service.</span></span>

         New-AzureStorageAccount -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
8. <span data-ttu-id="90201-203">Bu komut dosyasını, paket yapıdan sonra gerçekleşecek şekilde, ana bilgisayar derleme Otomasyon kablo bağlantılarını veya doğrudan Azure Powershell'den komut dosyasını çağırın.</span><span class="sxs-lookup"><span data-stu-id="90201-203">Call the script directly from Azure PowerShell, or wire up this script to your host build automation to occur after the package build.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="90201-204">Komut dosyası her zaman silin veya bunlar algılanırsa, var olan dağıtımlar varsayılan olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="90201-204">The script will always delete or replace your existing deployments by default if they are detected.</span></span> <span data-ttu-id="90201-205">Bu hiçbir kullanıcıdan mümkün olduğu Otomasyon sürekli teslimat etkinleştirmek gereklidir.</span><span class="sxs-lookup"><span data-stu-id="90201-205">This is necessary to enable continuous delivery from automation where no user prompting is possible.</span></span>
   >
   >

   <span data-ttu-id="90201-206">**Örnek Senaryo 1:** hazırlama ortamına bir hizmetin sürekli dağıtımı:</span><span class="sxs-lookup"><span data-stu-id="90201-206">**Example scenario 1:** continuous deployment to the staging environment of a service:</span></span>

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Staging -serviceName mycloudservice -storageAccountName mystoragesaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   <span data-ttu-id="90201-207">Bu genellikle doğrulama ve bir VIP takası testi tarafından izlendiğinden.</span><span class="sxs-lookup"><span data-stu-id="90201-207">This is typically followed up by test run verification and a VIP swap.</span></span> <span data-ttu-id="90201-208">VIP takas aracılığıyla yapılabilir [Azure portal](https://portal.azure.com) veya Move-Deployment cmdlet'ini kullanarak.</span><span class="sxs-lookup"><span data-stu-id="90201-208">The VIP swap can be done via the [Azure portal](https://portal.azure.com) or by using the Move-Deployment cmdlet.</span></span>

   <span data-ttu-id="90201-209">**Örnek Senaryo 2:** üretim ortamına ayrılmış sınama hizmetin sürekli dağıtım</span><span class="sxs-lookup"><span data-stu-id="90201-209">**Example scenario 2:** continuous deployment to the production environment of a dedicated test service</span></span>

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Production -enableDeploymentUpgrade 1 -serviceName mycloudservice -storageAccountName mystorageaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   <span data-ttu-id="90201-210">**Uzak Masaüstü:**</span><span class="sxs-lookup"><span data-stu-id="90201-210">**Remote Desktop:**</span></span>

   <span data-ttu-id="90201-211">Bu komut dosyası tarafından hedeflenen tüm bulut hizmetlerine doğru bulut hizmet sertifikası karşıya sağlamak için tek seferlik ek adımlar gerçekleştirmesi gerekir, Azure projenizdeki Uzak Masaüstü etkinleştirilirse.</span><span class="sxs-lookup"><span data-stu-id="90201-211">If Remote Desktop is enabled in your Azure project you will need to perform additional one-time steps to ensure the correct Cloud Service Certificate is uploaded to all cloud services targeted by this script.</span></span>

   <span data-ttu-id="90201-212">Rolleri tarafından beklenen sertifika parmak izi değerlerini bulun.</span><span class="sxs-lookup"><span data-stu-id="90201-212">Locate the certificate thumbprint values expected by your roles.</span></span> <span data-ttu-id="90201-213">Parmak izi değerleri bulut yapılandırma dosyasının (yani ServiceConfiguration.Cloud.cscfg) sertifikaları bölümünde görünür.</span><span class="sxs-lookup"><span data-stu-id="90201-213">The thumbprint values are visible in the Certificates section of the cloud config file (i.e. ServiceConfiguration.Cloud.cscfg).</span></span> <span data-ttu-id="90201-214">Görüntülediğinizde, aynı zamanda Visual Studio'da uzak masaüstü yapılandırması iletişim kutusu görünür seçenekleri ve Görünüm Seçili sertifika.</span><span class="sxs-lookup"><span data-stu-id="90201-214">It is also visible in the Remote Desktop Configuration dialog in Visual Studio when you Show Options and view the selected certificate.</span></span>

       <Certificates>
             <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption" thumbprint="C33B6C432C25581601B84C80F86EC2809DC224E8" thumbprintAlgorithm="sha1" />
       </Certificates>

   <span data-ttu-id="90201-215">Uzak Masaüstü sertifikaları, aşağıdaki cmdlet komut dosyası kullanarak bir kerelik Kurulum adım olarak karşıya yükle:</span><span class="sxs-lookup"><span data-stu-id="90201-215">Upload Remote Desktop certificates as a one-time setup step using the following cmdlet script:</span></span>

       Add-AzureCertificate -serviceName <CLOUDSERVICENAME> -certToDeploy (get-item cert:\CurrentUser\MY\<THUMBPRINT>)

   <span data-ttu-id="90201-216">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="90201-216">For example:</span></span>

       Add-AzureCertificate -serviceName 'mytestcloudservice' -certToDeploy (get-item cert:\CurrentUser\MY\C33B6C432C25581601B84C80F86EC2809DC224E8

   <span data-ttu-id="90201-217">Alternatif olarak özel anahtara sahip sertifika dosyasını PFX dışa aktarmak ve her hedef bulut kullanan hizmet sertifikalarını karşıya yükleme [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="90201-217">Alternatively you can export the certificate file PFX with private key and upload certificates to each target cloud service using the [Azure portal](https://portal.azure.com).</span></span>

   <!---
   Fixing broken links for Azure content migration from ACOM to DOCS. I'm unable to find a replacement links, so I'm commenting out this reference for now. The author can investigate in the future. "Read the following article to learn more: http://msdn.microsoft.com/library/windowsazure/gg443832.aspx.
   -->
   <span data-ttu-id="90201-218">**Dağıtım vs yükseltin. Dağıtım - Sil\> yeni dağıtım**</span><span class="sxs-lookup"><span data-stu-id="90201-218">**Upgrade Deployment vs. Delete Deployment -\> New Deployment**</span></span>

   <span data-ttu-id="90201-219">Komut dosyasını bir yükseltme dağıtımı varsayılan olarak gerçekleştireceği ($enableDeploymentUpgrade = 1) ne zaman hiçbir parametre geçirilen veya 1 değerini açıkça geçirilir.</span><span class="sxs-lookup"><span data-stu-id="90201-219">The script will by default perform an Upgrade Deployment ($enableDeploymentUpgrade = 1) when no parameter is passed in or the value 1 is passed explicitly.</span></span> <span data-ttu-id="90201-220">Tek örnekleri için tam dağıtımını daha az zaman ayırdığınız avantajı vardır.</span><span class="sxs-lookup"><span data-stu-id="90201-220">For single instances this has the advantage of taking less time than a full deployment.</span></span> <span data-ttu-id="90201-221">Bu ayrıca diğerlerinde çalıştıran bazı örnekleri bırakarak avantajı vardır, yüksek kullanılabilirlik gerektiren örnekleri (, güncelleştirme etki alanının yürütülmesi) yükseltilir, artı, VIP silinmeyecek için.</span><span class="sxs-lookup"><span data-stu-id="90201-221">For instances that require high availability this also has the advantage of leaving some instances running while others are upgraded (walking your update domain), plus your VIP will not be deleted.</span></span>

   <span data-ttu-id="90201-222">Yükseltme dağıtımı devre dışı bırakılabilir komut dosyasında ($enableDeploymentUpgrade = 0) veya geçirerek *- enableDeploymentUpgrade 0* bir parametre olarak, hangi değiştirir önce tüm mevcut dağıtımı silin ve yenisini oluşturmak için komut dosyası davranışı dağıtımı.</span><span class="sxs-lookup"><span data-stu-id="90201-222">Upgrade Deployment can be disabled in the script ($enableDeploymentUpgrade = 0) or by passing *-enableDeploymentUpgrade 0* as a parameter, which alters the script behavior to first delete any existing deployment and then create a new deployment.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="90201-223">Komut dosyası her zaman silin veya bunlar algılanırsa, var olan dağıtımlar varsayılan olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="90201-223">The script will always delete or replace your existing deployments by default if they are detected.</span></span> <span data-ttu-id="90201-224">Hiçbir kullanıcı/işleci isteyen mümkün olduğu Otomasyon sürekli teslimat etkinleştirmek için gereken budur.</span><span class="sxs-lookup"><span data-stu-id="90201-224">This is necessary to enable continuous delivery from automation where no user/operator prompting is possible.</span></span>
   >
   >

## <a name="5-publish-a-package-using-tfs-team-build"></a><span data-ttu-id="90201-225">5: TFS ekip kullanarak paket yayımlama</span><span class="sxs-lookup"><span data-stu-id="90201-225">5: Publish a Package using TFS Team Build</span></span>
<span data-ttu-id="90201-226">Bu isteğe bağlı adım, TFS yayımlama Azure paketi yapı işleyen ekip 4. adımda oluşturduğunuz betiğin bağlanır.</span><span class="sxs-lookup"><span data-stu-id="90201-226">This optional step connects TFS Team Build to the script created in step 4, which handles publishing of the package build to Azure.</span></span> <span data-ttu-id="90201-227">Bu, iş akışının sonunda bir yayımlama etkinliği çalışır, yapı tanımı tarafından kullanılan işlem şablonunu değiştirme kapsar.</span><span class="sxs-lookup"><span data-stu-id="90201-227">This entails modifying the Process Template used by your build definition so that it runs a Publish activity at the end of the workflow.</span></span> <span data-ttu-id="90201-228">Yayımla etkinlik parametrelerinde derlemeden geçirme, PowerShell komutunu çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="90201-228">The Publish activity will execute your PowerShell command passing in parameters from the build.</span></span> <span data-ttu-id="90201-229">MSBuild çıktısını hedefler ve komut dosyası yayımlama standart yapı çıktı yöneltilen.</span><span class="sxs-lookup"><span data-stu-id="90201-229">Output of the MSBuild targets and publish script will be piped into the standard build output.</span></span>

1. <span data-ttu-id="90201-230">Yapı tanımı sorumlu Düzenle sürekli dağıtın.</span><span class="sxs-lookup"><span data-stu-id="90201-230">Edit the Build Definition responsible for continuous deploy.</span></span>
2. <span data-ttu-id="90201-231">Seçin **işlem** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="90201-231">Select the **Process** tab.</span></span>
3. <span data-ttu-id="90201-232">İzleyin [bu yönergeleri](http://msdn.microsoft.com/library/dd647551.aspx) derleme işlem şablonu için bir etkinlik projesi eklemek için varsayılan şablonunu indirebilir, projeye ekleyin ve iade etme.</span><span class="sxs-lookup"><span data-stu-id="90201-232">Follow [these instructions](http://msdn.microsoft.com/library/dd647551.aspx) to add an Activity project for the build process template, download the default template, add it to the project and check it in.</span></span> <span data-ttu-id="90201-233">Derleme işlem şablonu AzureBuildProcessTemplate gibi yeni bir ad verin.</span><span class="sxs-lookup"><span data-stu-id="90201-233">Give the build process template a new name, such as AzureBuildProcessTemplate.</span></span>
4. <span data-ttu-id="90201-234">Geri dönüp **işlem** sekmesini tıklatın ve kullanmak **ayrıntıları göster** kullanılabilir yapı işlem şablonları listesini gösterme.</span><span class="sxs-lookup"><span data-stu-id="90201-234">Return to the **Process** tab, and use **Show Details** to show a list of available build process templates.</span></span> <span data-ttu-id="90201-235">Seçin **yeni...**  düğmesine tıklayın ve yalnızca eklenir ve iade projesine gidin.</span><span class="sxs-lookup"><span data-stu-id="90201-235">Choose the **New...** button, and navigate to the project you just added and checked in.</span></span> <span data-ttu-id="90201-236">Yeni oluşturduğunuz şablonu bulun ve seçin **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="90201-236">Locate the template you just created and choose **OK**.</span></span>
5. <span data-ttu-id="90201-237">Düzenleme için seçilen işlem şablonunu açın.</span><span class="sxs-lookup"><span data-stu-id="90201-237">Open the selected Process Template for editing.</span></span> <span data-ttu-id="90201-238">İş Akışı Tasarımcısı'nda doğrudan veya XML Düzenleyicisi'ni XAML ile çalışmak için açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90201-238">You can open directly in the Workflow designer or in the XML editor to work with the XAML.</span></span>
6. <span data-ttu-id="90201-239">İş Akışı Tasarımcısı'nın bağımsız değişkenleri sekmesinden ayrı satırı öğeleri olarak yeni bağımsız değişkenleri aşağıdaki listeye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="90201-239">Add the following list of new arguments as separate line items in the arguments tab of the workflow designer.</span></span> <span data-ttu-id="90201-240">Tüm bağımsız değişkenler yönü olması gerekir, = ve türü = String.</span><span class="sxs-lookup"><span data-stu-id="90201-240">All arguments should have direction=In and type=String.</span></span> <span data-ttu-id="90201-241">Bu akış parametrelerinin iş akışına yapı tanımından sonra Yayımla betik çağırmak için kullanılan kullanılır.</span><span class="sxs-lookup"><span data-stu-id="90201-241">These will be used to flow parameters from the build definition into the workflow, which then get used to call the publish script.</span></span>

       SubscriptionName
       StorageAccountName
       CloudConfigLocation
       PackageLocation
       Environment
       SubscriptionDataFileLocation
       PublishScriptLocation
       ServiceName

   ![Bağımsız değişkenler listesi][3]

   <span data-ttu-id="90201-243">Karşılık gelen XAML şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="90201-243">The corresponding XAML looks like this:</span></span>

       <Activity  _ />
         <x:Members>
           <x:Property Name="BuildSettings" Type="InArgument(mtbwa:BuildSettings)" />
           <x:Property Name="TestSpecs" Type="InArgument(mtbwa:TestSpecList)" />
           <x:Property Name="BuildNumberFormat" Type="InArgument(x:String)" />
           <x:Property Name="CleanWorkspace" Type="InArgument(mtbwa:CleanWorkspaceOption)" />
           <x:Property Name="RunCodeAnalysis" Type="InArgument(mtbwa:CodeAnalysisOption)" />
           <x:Property Name="SourceAndSymbolServerSettings" Type="InArgument(mtbwa:SourceAndSymbolServerSettings)" />
           <x:Property Name="AgentSettings" Type="InArgument(mtbwa:AgentSettings)" />
           <x:Property Name="AssociateChangesetsAndWorkItems" Type="InArgument(x:Boolean)" />
           <x:Property Name="CreateWorkItem" Type="InArgument(x:Boolean)" />
           <x:Property Name="DropBuild" Type="InArgument(x:Boolean)" />
           <x:Property Name="MSBuildArguments" Type="InArgument(x:String)" />
           <x:Property Name="MSBuildPlatform" Type="InArgument(mtbwa:ToolPlatform)" />
           <x:Property Name="PerformTestImpactAnalysis" Type="InArgument(x:Boolean)" />
           <x:Property Name="CreateLabel" Type="InArgument(x:Boolean)" />
           <x:Property Name="DisableTests" Type="InArgument(x:Boolean)" />
           <x:Property Name="GetVersion" Type="InArgument(x:String)" />
           <x:Property Name="PrivateDropLocation" Type="InArgument(x:String)" />
           <x:Property Name="Verbosity" Type="InArgument(mtbw:BuildVerbosity)" />
           <x:Property Name="Metadata" Type="mtbw:ProcessParameterMetadataCollection" />
           <x:Property Name="SupportedReasons" Type="mtbc:BuildReason" />
           <x:Property Name="SubscriptionName" Type="InArgument(x:String)" />
           <x:Property Name="StorageAccountName" Type="InArgument(x:String)" />
           <x:Property Name="CloudConfigLocation" Type="InArgument(x:String)" />
           <x:Property Name="PackageLocation" Type="InArgument(x:String)" />
           <x:Property Name="Environment" Type="InArgument(x:String)" />
           <x:Property Name="SubscriptionDataFileLocation" Type="InArgument(x:String)" />
           <x:Property Name="PublishScriptLocation" Type="InArgument(x:String)" />
           <x:Property Name="ServiceName" Type="InArgument(x:String)" />
         </x:Members>

         <this:Process.MSBuildArguments>
7. <span data-ttu-id="90201-244">Yeni bir sıra Aracısını Çalıştır sonuna ekleyin:</span><span class="sxs-lookup"><span data-stu-id="90201-244">Add a new sequence at the end of Run On Agent:</span></span>

   1. <span data-ttu-id="90201-245">Geçerli komut dosyası için denetlemek için bir If ifadesinden etkinlik ekleyerek başlayın.</span><span class="sxs-lookup"><span data-stu-id="90201-245">Start by adding an If Statement activity to check for a valid script file.</span></span> <span data-ttu-id="90201-246">Koşul için bu değeri ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="90201-246">Set the condition to this value:</span></span>

          Not String.IsNullOrEmpty(PublishScriptLocation)
   2. <span data-ttu-id="90201-247">Ardından bu durumda yeni bir dizi etkinlik varsa deyiminin ekleyin.</span><span class="sxs-lookup"><span data-stu-id="90201-247">In the Then case of the If Statement, add a new Sequence activity.</span></span> <span data-ttu-id="90201-248">'Başlangıç Yayımla' görünen adını ayarlayın</span><span class="sxs-lookup"><span data-stu-id="90201-248">Set the display name to 'Start publish'</span></span>
   3. <span data-ttu-id="90201-249">Halen seçili dizisi ile başlangıç yayımlama, ayrı satırı öğeleri değişkenleri sekmesi iş akışı Tasarımcısı'nın olarak aşağıdaki yeni değişkenleri listesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="90201-249">With the Start publish sequence still selected, add the following list of new variables as separate line items in the variables tab of the workflow designer.</span></span> <span data-ttu-id="90201-250">Tüm değişkenleri değişken türü olmalıdır = dize ve kapsam başlangıç = yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="90201-250">All variables should have Variable type =String and Scope=Start publish.</span></span> <span data-ttu-id="90201-251">Bu akış parametrelerinin iş akışına yapı tanımından sonra Yayımla betik çağırmak için kullanılan kullanılır.</span><span class="sxs-lookup"><span data-stu-id="90201-251">These will be used to flow parameters from the build definition into the workflow, which then get used to call the publish script.</span></span>

      * <span data-ttu-id="90201-252">Dize türünde SubscriptionDataFilePath</span><span class="sxs-lookup"><span data-stu-id="90201-252">SubscriptionDataFilePath, of type String</span></span>
      * <span data-ttu-id="90201-253">Dize türünde PublishScriptFilePath</span><span class="sxs-lookup"><span data-stu-id="90201-253">PublishScriptFilePath, of type String</span></span>

        ![Yeni değişkenleri][4]
   4. <span data-ttu-id="90201-255">TFS 2012 veya önceki bir sürümünü kullanıyorsanız, yeni sıra başında ConvertWorkspaceItem etkinliği ekleyin.</span><span class="sxs-lookup"><span data-stu-id="90201-255">If you are using TFS 2012 or earlier, add a ConvertWorkspaceItem activity at the beginning of the new Sequence.</span></span> <span data-ttu-id="90201-256">TFS 2013 veya üzeri kullanıyorsanız, yeni sıra başında GetLocalPath etkinliği ekleyin.</span><span class="sxs-lookup"><span data-stu-id="90201-256">If you are using TFS 2013 or later, add a GetLocalPath activity at the beginning of the new sequence.</span></span> <span data-ttu-id="90201-257">Bir ConvertWorkspaceItem için özellikleri aşağıdaki gibi ayarlayın: yönü ServerToLocal, DisplayName = 'Dönüştürme Yayımla betik filename' = giriş 'PublishScriptLocation', sonuç = 'PublishScriptFilePath', çalışma alanı = = 'Çalışma alanı'.</span><span class="sxs-lookup"><span data-stu-id="90201-257">For a ConvertWorkspaceItem, set the properties as follows: Direction=ServerToLocal, DisplayName='Convert publish script filename', Input=' PublishScriptLocation', Result='PublishScriptFilePath', Workspace='Workspace'.</span></span> <span data-ttu-id="90201-258">GetLocalPath etkinliği için 'PublishScriptLocation' IncomingPath ve sonucu 'PublishScriptFilePath' özelliğini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="90201-258">For a GetLocalPath activity, set the property IncomingPath to 'PublishScriptLocation', and the Result to 'PublishScriptFilePath'.</span></span> <span data-ttu-id="90201-259">Bu etkinlik konumlardan TFS sunucusu (varsa) standart yerel disk yoluna Yayımla betik yolu dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="90201-259">This activity converts the path to the publish script from TFS server locations (if applicable) to a standard local disk path.</span></span>
   5. <span data-ttu-id="90201-260">TFS 2012 veya önceki bir sürümünü kullanıyorsanız, başka bir ConvertWorkspaceItem etkinlik yeni sırası sonuna ekleyin.</span><span class="sxs-lookup"><span data-stu-id="90201-260">If you are using TFS 2012 or earlier, add another ConvertWorkspaceItem activity at the end of the new Sequence.</span></span> <span data-ttu-id="90201-261">Yön ServerToLocal, DisplayName = 'abonelik filename Dönüştür' = giriş 'SubscriptionDataFileLocation', sonuç = 'SubscriptionDataFilePath', çalışma alanı = = 'Çalışma alanı'.</span><span class="sxs-lookup"><span data-stu-id="90201-261">Direction=ServerToLocal, DisplayName='Convert subscription filename', Input=' SubscriptionDataFileLocation', Result= 'SubscriptionDataFilePath', Workspace='Workspace'.</span></span> <span data-ttu-id="90201-262">TFS 2013 veya üzeri kullanıyorsanız, başka bir GetLocalPath ekleyin.</span><span class="sxs-lookup"><span data-stu-id="90201-262">If you are using TFS 2013 or later, add another GetLocalPath.</span></span> <span data-ttu-id="90201-263">IncomingPath 'SubscriptionDataFileLocation' = ve sonuç 'SubscriptionDataFilePath.' =</span><span class="sxs-lookup"><span data-stu-id="90201-263">IncomingPath='SubscriptionDataFileLocation', and Result='SubscriptionDataFilePath.'</span></span>
   6. <span data-ttu-id="90201-264">InvokeProcess aktivite yeni sırası sonuna ekleyin.</span><span class="sxs-lookup"><span data-stu-id="90201-264">Add an InvokeProcess activity at the end of the new Sequence.</span></span>
      <span data-ttu-id="90201-265">Bu etkinlik, derleme tanımına göre geçirilen bağımsız değişkenlerle PowerShell.exe çağırır.</span><span class="sxs-lookup"><span data-stu-id="90201-265">This activity calls PowerShell.exe with the arguments passed in by the Build Definition.</span></span>

      + <span data-ttu-id="90201-266">Bağımsız değişkenler String.Format = ("-""{0}" "- serviceName {1} - storageAccountName {2} - packageLocation""{3}" "- cloudConfigLocation""{4}" "- subscriptionDataFile""{5}" "- selectedSubscription {6} dosya-ortam""{7}" "",  PublishScriptFilePath, ServiceName, StorageAccountName, PackageLocation, CloudConfigLocation, SubscriptionDataFilePath, varlığıyla SubscriptionName, ortamı)</span><span class="sxs-lookup"><span data-stu-id="90201-266">Arguments = String.Format(" -File ""{0}"" -serviceName {1}  -storageAccountName {2} -packageLocation ""{3}""  -cloudConfigLocation ""{4}"" -subscriptionDataFile ""{5}""  -selectedSubscription {6} -environment ""{7}""",  PublishScriptFilePath, ServiceName, StorageAccountName,  PackageLocation, CloudConfigLocation,  SubscriptionDataFilePath, SubscriptionName, Environment)</span></span>
      + <span data-ttu-id="90201-267">DisplayName Execute = betik yayımlama</span><span class="sxs-lookup"><span data-stu-id="90201-267">DisplayName = Execute publish script</span></span>
      + <span data-ttu-id="90201-268">FileName = "PowerShell" (tırnak işaretleri dahil)</span><span class="sxs-lookup"><span data-stu-id="90201-268">FileName = "PowerShell" (include the quotes)</span></span>
      + <span data-ttu-id="90201-269">OutputEncoding System.Text.Encoding.GetEncoding(System.Globalization.CultureInfo.InstalledUICulture.TextInfo.OEMCodePage) =</span><span class="sxs-lookup"><span data-stu-id="90201-269">OutputEncoding=  System.Text.Encoding.GetEncoding(System.Globalization.CultureInfo.InstalledUICulture.TextInfo.OEMCodePage)</span></span>
   7. <span data-ttu-id="90201-270">İçinde **işlemek standart çıktı** bölümünde InvokeProcess textbox, 'data' textbox değerine ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="90201-270">In the **Handle Standard Output** section textbox of the InvokeProcess, set the textbox value to 'data'.</span></span> <span data-ttu-id="90201-271">Bu standart çıktı verilerini depolamak üzere bir değişkendir.</span><span class="sxs-lookup"><span data-stu-id="90201-271">This is a variable to store the standard output data.</span></span>
   8. <span data-ttu-id="90201-272">WriteBuildMessage etkinlik eklemek yalnızca aşağıda **işlemek standart çıktı** bölümü.</span><span class="sxs-lookup"><span data-stu-id="90201-272">Add a WriteBuildMessage activity just below the **Handle Standard Output** section.</span></span> <span data-ttu-id="90201-273">Önem düzeyini belirlemek = 'Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High' ve ileti = 'data'.</span><span class="sxs-lookup"><span data-stu-id="90201-273">Set the Importance = 'Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High' and the Message='data'.</span></span> <span data-ttu-id="90201-274">Bu komut dosyasının standart çıktı yapı çıktı yazılmış sağlar.</span><span class="sxs-lookup"><span data-stu-id="90201-274">This ensures the standard output of the script will get written to the build output.</span></span>
   9. <span data-ttu-id="90201-275">İçinde **hata çıkış işleme** bölümünde InvokeProcess textbox, 'data' textbox değerine ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="90201-275">In the **Handle Error Output** section textbox of the InvokeProcess, set the textbox value to 'data'.</span></span> <span data-ttu-id="90201-276">Bu standart hata verileri depolamak için bir değişkendir.</span><span class="sxs-lookup"><span data-stu-id="90201-276">This is a variable to store the standard error data.</span></span>
   10. <span data-ttu-id="90201-277">WriteBuildError etkinlik eklemek yalnızca aşağıda **hata çıkış işleme** bölümü.</span><span class="sxs-lookup"><span data-stu-id="90201-277">Add a WriteBuildError activity just below the **Handle Error Output** section.</span></span> <span data-ttu-id="90201-278">İleti Ayarla = 'data'.</span><span class="sxs-lookup"><span data-stu-id="90201-278">Set the Message='data'.</span></span> <span data-ttu-id="90201-279">Bu komut dosyasının standart hatalar yapı hata çıktısı yazılan sağlar.</span><span class="sxs-lookup"><span data-stu-id="90201-279">This ensures the standard errors of the script will get written to the build error output.</span></span>
   11. <span data-ttu-id="90201-280">Mavi ünlem işaretleri tarafından belirtilen tüm hataları düzeltin.</span><span class="sxs-lookup"><span data-stu-id="90201-280">Correct any errors, indicated by blue exclamation marks.</span></span> <span data-ttu-id="90201-281">Hata hakkında bir ipucu almak için ünlem işaretleri üzerine gelerek.</span><span class="sxs-lookup"><span data-stu-id="90201-281">Hover over the exclamation marks to get a hint about the error.</span></span> <span data-ttu-id="90201-282">Hataları temizlemek için iş akışını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="90201-282">Save the workflow to clear errors.</span></span>

   <span data-ttu-id="90201-283">Yayımla iş akışı etkinlikleri sonucunu Tasarımcısı'nda şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="90201-283">The final result of the publish workflow activities will look like this in the designer:</span></span>

   ![İş akışı etkinlikleri][5]

   <span data-ttu-id="90201-285">Yayımla iş akışı etkinlikleri sonucunu XAML'de şuna benzeyecektir:</span><span class="sxs-lookup"><span data-stu-id="90201-285">The final result of the publish workflow activities will look like this in XAML:</span></span>

       <If Condition="[Not String.IsNullOrEmpty(PublishScriptLocation)]" sap2010:WorkflowViewState.IdRef="If_1">
           <If.Then>
             <Sequence DisplayName="Start Publish" sap2010:WorkflowViewState.IdRef="Sequence_4">
               <Sequence.Variables>
                 <Variable x:TypeArguments="x:String" Name="SubscriptionDataFilePath" />
                 <Variable x:TypeArguments="x:String" Name="PublishScriptFilePath" />
               </Sequence.Variables>
               <mtbwa:ConvertWorkspaceItem DisplayName="Convert publish script filename" sap2010:WorkflowViewState.IdRef="ConvertWorkspaceItem_1" Input="[PublishScriptLocation]" Result="[PublishScriptFilePath]" Workspace="[Workspace]" />
               <mtbwa:ConvertWorkspaceItem DisplayName="Convert subscription filename" sap2010:WorkflowViewState.IdRef="ConvertWorkspaceItem_2" Input="[SubscriptionDataFileLocation]" Result="[SubscriptionDataFilePath]" Workspace="[Workspace]" />
               <mtbwa:InvokeProcess Arguments="[String.Format(&quot; -File &quot;&quot;{0}&quot;&quot; -serviceName {1}&#xD;&#xA;            -storageAccountName {2} -packageLocation &quot;&quot;{3}&quot;&quot;&#xD;&#xA;            -cloudConfigLocation &quot;&quot;{4}&quot;&quot; -subscriptionDataFile &quot;&quot;{5}&quot;&quot;&#xD;&#xA;            -selectedSubscription {6} -environment &quot;&quot;{7}&quot;&quot;&quot;,&#xD;&#xA;            PublishScriptFilePath, ServiceName, StorageAccountName,&#xD;&#xA;            PackageLocation, CloudConfigLocation,&#xD;&#xA;            SubscriptionDataFilePath, SubscriptionName, Environment)]" DisplayName="'Execute Publish Script'" FileName="[PowerShell]" sap2010:WorkflowViewState.IdRef="InvokeProcess_1">
                 <mtbwa:InvokeProcess.ErrorDataReceived>
                   <ActivityAction x:TypeArguments="x:String">
                     <ActivityAction.Argument>
                       <DelegateInArgument x:TypeArguments="x:String" Name="data" />
                     </ActivityAction.Argument>
                     <mtbwa:WriteBuildError Message="{x:Null}" sap2010:WorkflowViewState.IdRef="WriteBuildError_1" />
                   </ActivityAction>
                 </mtbwa:InvokeProcess.ErrorDataReceived>
                 <mtbwa:InvokeProcess.OutputDataReceived>
                   <ActivityAction x:TypeArguments="x:String">
                     <ActivityAction.Argument>
                       <DelegateInArgument x:TypeArguments="x:String" Name="data" />
                     </ActivityAction.Argument>
                     <mtbwa:WriteBuildMessage sap2010:WorkflowViewState.IdRef="WriteBuildMessage_2" Importance="[Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High]" Message="[data]" mva:VisualBasic.Settings="Assembly references and imported namespaces serialized as XML namespaces" />
                   </ActivityAction>
                 </mtbwa:InvokeProcess.OutputDataReceived>
               </mtbwa:InvokeProcess>
             </Sequence>
           </If.Then>
         </If>
       </Sequence>
8. <span data-ttu-id="90201-286">Yapı işlem şablonu iş akışı ve iade etme Bu dosyayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="90201-286">Save the build process template workflow and Check In this file.</span></span>
9. <span data-ttu-id="90201-287">Derleme tanımını Düzenle (kapatın, zaten açıksa) ve seçin **yeni** işlem şablonları yeni şablona henüz görmüyorsanız düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="90201-287">Edit the build definition (close it if it is already open), and select the **New** button if you do not yet see the new template in the list of Process Templates.</span></span>
10. <span data-ttu-id="90201-288">Parametre özellik değerleri diğer bölümünde aşağıdaki gibi ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="90201-288">Set the parameter property values in the Misc section as follows:</span></span>

    1. <span data-ttu-id="90201-289">CloudConfigLocation ='c:\\bırakır\\app.publish\\ServiceConfiguration.Cloud.cscfg' *bu değer türetilir: ($PublishDir)ServiceConfiguration.Cloud.cscfg*</span><span class="sxs-lookup"><span data-stu-id="90201-289">CloudConfigLocation ='c:\\drops\\app.publish\\ServiceConfiguration.Cloud.cscfg' *This value is derived from: ($PublishDir)ServiceConfiguration.Cloud.cscfg*</span></span>
    2. <span data-ttu-id="90201-290">PackageLocation = ' c:\\bırakır\\app.publish\\ContactManager.Azure.cspkg' *bu değer türetilir: ($PublishDir)($ProjectName) .cspkg*</span><span class="sxs-lookup"><span data-stu-id="90201-290">PackageLocation = 'c:\\drops\\app.publish\\ContactManager.Azure.cspkg' *This value is derived from: ($PublishDir)($ProjectName).cspkg*</span></span>
    3. <span data-ttu-id="90201-291">PublishScriptLocation = ' c:\\betikleri\\WindowsAzure\\PublishCloudService.ps1'</span><span class="sxs-lookup"><span data-stu-id="90201-291">PublishScriptLocation = 'c:\\scripts\\WindowsAzure\\PublishCloudService.ps1'</span></span>
    4. <span data-ttu-id="90201-292">ServiceName = 'mycloudservicename' *uygun bulut hizmeti adını buraya kullanın*</span><span class="sxs-lookup"><span data-stu-id="90201-292">ServiceName = 'mycloudservicename' *Use the appropriate cloud service name here*</span></span>
    5. <span data-ttu-id="90201-293">Ortam 'Hazırlama' =</span><span class="sxs-lookup"><span data-stu-id="90201-293">Environment = 'Staging'</span></span>
    6. <span data-ttu-id="90201-294">StorageAccountName 'mystorageaccountname' = *uygun depolama hesabı adı burada kullanın*</span><span class="sxs-lookup"><span data-stu-id="90201-294">StorageAccountName = 'mystorageaccountname' *Use the appropriate storage account name here*</span></span>
    7. <span data-ttu-id="90201-295">SubscriptionDataFileLocation = ' c:\\betikleri\\WindowsAzure\\Subscription.xml'</span><span class="sxs-lookup"><span data-stu-id="90201-295">SubscriptionDataFileLocation = 'c:\\scripts\\WindowsAzure\\Subscription.xml'</span></span>
    8. <span data-ttu-id="90201-296">Varlığıyla SubscriptionName = 'varsayılan'</span><span class="sxs-lookup"><span data-stu-id="90201-296">SubscriptionName = 'default'</span></span>

    ![Parametre özellik değerleri][6]
11. <span data-ttu-id="90201-298">Yapı tanımı için değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="90201-298">Save the changes to the Build Definition.</span></span>
12. <span data-ttu-id="90201-299">Her iki paketi yapı yürütün ve yayımlamak için bir yapıyı sıraya al.</span><span class="sxs-lookup"><span data-stu-id="90201-299">Queue a Build to execute both the package build and publish.</span></span> <span data-ttu-id="90201-300">Sürekli tümleştirme için ayarlanmış bir tetikleyici varsa, her iade Bu davranış yürütülür.</span><span class="sxs-lookup"><span data-stu-id="90201-300">If you have a trigger set to Continuous Integration, you will execute this behavior on every check-in.</span></span>

### <a name="publishcloudserviceps1-script-template"></a><span data-ttu-id="90201-301">PublishCloudService.ps1 komut dosyası şablonu</span><span class="sxs-lookup"><span data-stu-id="90201-301">PublishCloudService.ps1 script template</span></span>
```
Param(  $serviceName = "",
        $storageAccountName = "",
        $packageLocation = "",
        $cloudConfigLocation = "",
        $environment = "Staging",
        $deploymentLabel = "ContinuousDeploy to $servicename",
        $timeStampFormat = "g",
        $alwaysDeleteExistingDeployments = 1,
        $enableDeploymentUpgrade = 1,
        $selectedsubscription = "default",
        $subscriptionDataFile = ""
     )


function Publish()
{
    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot -ErrorVariable a -ErrorAction silentlycontinue
    if ($a[0] -ne $null)
    {
        Write-Output "$(Get-Date -f $timeStampFormat) - No deployment is detected. Creating a new deployment. "
    }
    #check for existing deployment and then either upgrade, delete + deploy, or cancel according to $alwaysDeleteExistingDeployments and $enableDeploymentUpgrade boolean variables
    if ($deployment.Name -ne $null)
    {
        switch ($alwaysDeleteExistingDeployments)
        {
            1
            {
                switch ($enableDeploymentUpgrade)
                {
                    1  #Update deployment inplace (usually faster, cheaper, won't destroy VIP)
                    {
                        Write-Output "$(Get-Date -f $timeStampFormat) - Deployment exists in $servicename.  Upgrading deployment."
                        UpgradeDeployment
                    }
                    0  #Delete then create new deployment
                    {
                        Write-Output "$(Get-Date -f $timeStampFormat) - Deployment exists in $servicename.  Deleting deployment."
                        DeleteDeployment
                        CreateNewDeployment

                    }
                } # switch ($enableDeploymentUpgrade)
            }
            0
            {
                Write-Output "$(Get-Date -f $timeStampFormat) - ERROR: Deployment exists in $servicename.  Script execution cancelled."
                exit
            }
        } #switch ($alwaysDeleteExistingDeployments)
    } else {
            CreateNewDeployment
    }
}

function CreateNewDeployment()
{
    write-progress -id 3 -activity "Creating New Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Creating New Deployment: In progress"

    $opstat = New-AzureDeployment -Slot $slot -Package $packageLocation -Configuration $cloudConfigLocation -label $deploymentLabel -ServiceName $serviceName

    $completeDeployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $completeDeploymentID = $completeDeployment.deploymentid

    write-progress -id 3 -activity "Creating New Deployment" -completed -Status "Complete"
    Write-Output "$(Get-Date -f $timeStampFormat) - Creating New Deployment: Complete, Deployment ID: $completeDeploymentID"

    StartInstances
}

function UpgradeDeployment()
{
    write-progress -id 3 -activity "Upgrading Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Upgrading Deployment: In progress"

    # perform Update-Deployment
    $setdeployment = Set-AzureDeployment -Upgrade -Slot $slot -Package $packageLocation -Configuration $cloudConfigLocation -label $deploymentLabel -ServiceName $serviceName -Force

    $completeDeployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $completeDeploymentID = $completeDeployment.deploymentid

    write-progress -id 3 -activity "Upgrading Deployment" -completed -Status "Complete"
    Write-Output "$(Get-Date -f $timeStampFormat) - Upgrading Deployment: Complete, Deployment ID: $completeDeploymentID"
}

function DeleteDeployment()
{

    write-progress -id 2 -activity "Deleting Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Deleting Deployment: In progress"

    #WARNING - always deletes with force
    $removeDeployment = Remove-AzureDeployment -Slot $slot -ServiceName $serviceName -Force

    write-progress -id 2 -activity "Deleting Deployment: Complete" -completed -Status $removeDeployment
    Write-Output "$(Get-Date -f $timeStampFormat) - Deleting Deployment: Complete"

}

function StartInstances()
{
    write-progress -id 4 -activity "Starting Instances" -status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instances: In progress"

    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $runstatus = $deployment.Status

    if ($runstatus -ne 'Running')
    {
        $run = Set-AzureDeployment -Slot $slot -ServiceName $serviceName -Status Running
    }
    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $oldStatusStr = @("") * $deployment.RoleInstanceList.Count

    while (-not(AllInstancesRunning($deployment.RoleInstanceList)))
    {
        $i = 1
        foreach ($roleInstance in $deployment.RoleInstanceList)
        {
            $instanceName = $roleInstance.InstanceName
            $instanceStatus = $roleInstance.InstanceStatus

            if ($oldStatusStr[$i - 1] -ne $roleInstance.InstanceStatus)
            {
                $oldStatusStr[$i - 1] = $roleInstance.InstanceStatus
                Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instance '$instanceName': $instanceStatus"
            }

            write-progress -id (4 + $i) -activity "Starting Instance '$instanceName'" -status "$instanceStatus"
            $i = $i + 1
        }

        sleep -Seconds 1

        $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    }

    $i = 1
    foreach ($roleInstance in $deployment.RoleInstanceList)
    {
        $instanceName = $roleInstance.InstanceName
        $instanceStatus = $roleInstance.InstanceStatus

        if ($oldStatusStr[$i - 1] -ne $roleInstance.InstanceStatus)
        {
            $oldStatusStr[$i - 1] = $roleInstance.InstanceStatus
            Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instance '$instanceName': $instanceStatus"
        }

        $i = $i + 1
    }

    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $opstat = $deployment.Status

    write-progress -id 4 -activity "Starting Instances" -completed -status $opstat
    Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instances: $opstat"
}

function AllInstancesRunning($roleInstanceList)
{
    foreach ($roleInstance in $roleInstanceList)
    {
        if ($roleInstance.InstanceStatus -ne "ReadyRole")
        {
            return $false
        }
    }

    return $true
}

#configure powershell with Azure 1.7 modules
Import-Module Azure

#configure powershell with publishsettings for your subscription
$pubsettings = $subscriptionDataFile
Import-AzurePublishSettingsFile $pubsettings
Set-AzureSubscription -CurrentStorageAccountName $storageAccountName -SubscriptionName $selectedsubscription
Select-AzureSubscription $selectedsubscription

#set remaining environment variables for Azure cmdlets
$subscription = Get-AzureSubscription $selectedsubscription
$subscriptionname = $subscription.subscriptionname
$subscriptionid = $subscription.subscriptionid
$slot = $environment

#main driver - publish & write progress to activity log
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script started."
Write-Output "$(Get-Date -f $timeStampFormat) - Preparing deployment of $deploymentLabel for $subscriptionname with Subscription ID $subscriptionid."

Publish

$deployment = Get-AzureDeployment -slot $slot -serviceName $servicename
$deploymentUrl = $deployment.Url

Write-Output "$(Get-Date -f $timeStampFormat) - Created Cloud Service with URL $deploymentUrl."
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script finished."
```

## <a name="next-steps"></a><span data-ttu-id="90201-302">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="90201-302">Next steps</span></span>
<span data-ttu-id="90201-303">Kesintisiz teslim kullanırken uzaktan hata ayıklamayı etkinleştirmek için bkz: [kesintisiz teslim için Azure yayımlama için kullanırken uzaktan hata ayıklamayı etkinleştirme](cloud-services-virtual-machines-dotnet-continuous-delivery-remote-debugging.md).</span><span class="sxs-lookup"><span data-stu-id="90201-303">To enable remote debugging when using continuous delivery, see [Enable remote debugging when using continuous delivery to publish to Azure](cloud-services-virtual-machines-dotnet-continuous-delivery-remote-debugging.md).</span></span>

[Team Foundation Build Service]: https://msdn.microsoft.com/library/ee259687.aspx
[.NET Framework 4]: https://www.microsoft.com/download/details.aspx?id=17851
[.NET Framework 4.5]: https://www.microsoft.com/download/details.aspx?id=30653
[.NET Framework 4.5.2]: https://www.microsoft.com/download/details.aspx?id=42643
[Scale out your build system]: https://msdn.microsoft.com/library/dd793166.aspx
[Deploy and configure a build server]: https://msdn.microsoft.com/library/ms181712.aspx
[Azure PowerShell cmdlets]: /powershell/azureps-cmdlets-docs
[the .publishsettings file]: https://manage.windowsazure.com/download/publishprofile.aspx?wa=wsignin1.0
[0]: ./media/cloud-services-dotnet-continuous-delivery/tfs-01bc.png
[2]: ./media/cloud-services-dotnet-continuous-delivery/tfs-02.png
[3]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-03.png
[4]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-04.png
[5]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-05.png
[6]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-06.png
