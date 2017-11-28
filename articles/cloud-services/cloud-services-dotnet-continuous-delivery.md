---
title: "Bulut için aaaContinuous teslim hizmetleri Azure içinde TFS ile | Microsoft Docs"
description: "Bilgi nasıl tooset Azure için sürekli teslimini bulut uygulamaları. MSBuild komut satırı deyimleri ve PowerShell komut dosyaları için kod örnekleri."
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
ms.openlocfilehash: c0e5e72ffbd3c05b84ce1733068e92c528bcc4b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-for-cloud-services-in-azure"></a><span data-ttu-id="09454-104">Azure bulut Hizmetleri için devamlı teslim</span><span class="sxs-lookup"><span data-stu-id="09454-104">Continuous Delivery for Cloud Services in Azure</span></span>
<span data-ttu-id="09454-105">Merhaba bu makalede açıklanan işlemi şunların nasıl yapıldığını gösterir Azure bulut uygulamaları için sürekli teslimini tooset.</span><span class="sxs-lookup"><span data-stu-id="09454-105">hello process described in this article shows you how tooset up continuous delivery for Azure cloud apps.</span></span> <span data-ttu-id="09454-106">Bu işlem, paketleri otomatik olarak oluşturun ve kod her iade sonra hello paket tooAzure dağıtmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="09454-106">This process enables you to automatically create packages and deploy hello package tooAzure after every code check-in.</span></span> <span data-ttu-id="09454-107">Merhaba paket oluşturma işlemi bu makalede açıklanan olan eşdeğer toohello **paket** Visual Studio komut ve yayımlama adımlarını olan eşdeğer toohello **Yayımla** Visual Studio'da komutu.</span><span class="sxs-lookup"><span data-stu-id="09454-107">hello package build process described in this article is equivalent toohello **Package** command in Visual Studio, and the publishing steps are equivalent toohello **Publish** command in Visual Studio.</span></span>
<span data-ttu-id="09454-108">Merhaba makale kapsar hello metodu toocreate yapı sunucusu MSBuild komut satırı deyimleri ve Windows PowerShell betikleri ve bu da kullanacağınız gösterir nasıl toooptionally yapılandırmak Visual Studio Team Foundation Server - ekip tanımları toouse hello MSBuild komutlar ve PowerShell komut dosyaları.</span><span class="sxs-lookup"><span data-stu-id="09454-108">hello article covers hello methods you would use toocreate a build server with MSBuild command-line statements and Windows PowerShell scripts, and it also demonstrates how toooptionally configure Visual Studio Team Foundation Server - Team Build definitions toouse hello MSBuild commands and PowerShell scripts.</span></span> <span data-ttu-id="09454-109">Merhaba yapı ortamı ve Azure hedef ortamları için özelleştirilebilir bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="09454-109">hello process is customizable for your build environment and Azure target environments.</span></span>

<span data-ttu-id="09454-110">Visual Studio Team Services, olan TFS sürümü ayrıca kullanabileceğiniz daha kolay bu toodo Azure üzerinde barındırılan.</span><span class="sxs-lookup"><span data-stu-id="09454-110">You can also use Visual Studio Team Services, a version of TFS that is hosted in Azure, toodo this more easily.</span></span> 

<span data-ttu-id="09454-111">Başlamadan önce uygulamanızı Visual Studio'dan yayımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="09454-111">Before you start, you should publish your application from Visual Studio.</span></span>
<span data-ttu-id="09454-112">Bu tüm hello kaynakların kullanılabilir ve başlatılmış olduğundan emin olmak için tooautomate hello yayın işlem çalıştığınızda.</span><span class="sxs-lookup"><span data-stu-id="09454-112">This will ensure that all hello resources are available and initialized when you attempt tooautomate hello publication process.</span></span>

## <a name="1-configure-hello-build-server"></a><span data-ttu-id="09454-113">1: hello yapı sunucu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="09454-113">1: Configure hello Build Server</span></span>
<span data-ttu-id="09454-114">MSBuild kullanarak bir Azure paketi oluşturabilmeniz için önce hello yapı sunucuya hello gerekli yazılım ve araçları yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="09454-114">Before you can create an Azure package by using MSBuild, you must install hello required software and tools on hello build server.</span></span>

<span data-ttu-id="09454-115">Visual Studio gerekli toobe hello yapı sunucuda yüklü değil.</span><span class="sxs-lookup"><span data-stu-id="09454-115">Visual Studio is not required toobe installed on hello build server.</span></span> <span data-ttu-id="09454-116">Yapı sunucunuz toouse Team Foundation Yapı Hizmeti toomanage istiyorsanız hello hello yönergeleri izleyin [Team Foundation Yapı Hizmeti] [ Team Foundation Build Service] belgeleri.</span><span class="sxs-lookup"><span data-stu-id="09454-116">If you want toouse Team Foundation Build Service toomanage your build server, follow hello instructions in hello [Team Foundation Build Service][Team Foundation Build Service] documentation.</span></span>

1. <span data-ttu-id="09454-117">Merhaba Hello yapı sunucuya yüklemek [.NET Framework 4.5.2][.NET Framework 4.5.2], MSBuild içerir.</span><span class="sxs-lookup"><span data-stu-id="09454-117">On hello build server, install hello [.NET Framework 4.5.2][.NET Framework 4.5.2], which includes MSBuild.</span></span>
2. <span data-ttu-id="09454-118">Merhaba son yükleme [.NET için Azure yazma araçları](https://azure.microsoft.com/develop/net/).</span><span class="sxs-lookup"><span data-stu-id="09454-118">Install hello latest [Azure Authoring Tools for .NET](https://azure.microsoft.com/develop/net/).</span></span>
3. <span data-ttu-id="09454-119">Merhaba yüklemek [.NET için Azure kitaplıkları](http://go.microsoft.com/fwlink/?LinkId=623519).</span><span class="sxs-lookup"><span data-stu-id="09454-119">Install hello [Azure Libraries for .NET](http://go.microsoft.com/fwlink/?LinkId=623519).</span></span>
4. <span data-ttu-id="09454-120">Visual Studio yükleme toohello hello Microsoft.WebApplication.targets dosya Kopyala sunucusu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="09454-120">Copy hello Microsoft.WebApplication.targets file from a Visual Studio installation toohello build server.</span></span>

   <span data-ttu-id="09454-121">Visual Studio'nun yüklü olan bir bilgisayarda bu dosyayı C: hello dizininde bulunan\\Program Files(x86)\\MSBuild\\Microsoft\\Visual Studio\\v14.0\\Web.</span><span class="sxs-lookup"><span data-stu-id="09454-121">On a computer with Visual Studio installed, this file is located in hello directory C:\\Program Files(x86)\\MSBuild\\Microsoft\\VisualStudio\\v14.0\\WebApplications.</span></span> <span data-ttu-id="09454-122">Toohello kopyalamalısınız hello yapı sunucudaki aynı dizini.</span><span class="sxs-lookup"><span data-stu-id="09454-122">You should copy it toohello same directory on hello build server.</span></span>
5. <span data-ttu-id="09454-123">Merhaba yüklemek [Visual Studio için Azure Araçları](https://www.visualstudio.com/features/azure-tools-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="09454-123">Install hello [Azure Tools for Visual Studio](https://www.visualstudio.com/features/azure-tools-vs.aspx).</span></span>

## <a name="2-build-a-package-using-msbuild-commands"></a><span data-ttu-id="09454-124">2: MSBuild komutları kullanarak bir paket oluşturun</span><span class="sxs-lookup"><span data-stu-id="09454-124">2: Build a Package using MSBuild Commands</span></span>
<span data-ttu-id="09454-125">Bu bölümde nasıl tooconstruct bir MSBuild komut, açıklanmaktadır Azure bir paket oluşturur.</span><span class="sxs-lookup"><span data-stu-id="09454-125">This section describes how tooconstruct an MSBuild command that builds an Azure package.</span></span> <span data-ttu-id="09454-126">Bu adım, her şeyin doğru şekilde yapılandırıldığını ve ne istediğiniz hello MSBuild komut yapan hello yapı sunucu tooverify üzerinde toodo çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="09454-126">Run this step on hello build server tooverify that everything is configured correctly and that hello MSBuild command does what you want it toodo.</span></span> <span data-ttu-id="09454-127">Hello sonraki bölümde açıklandığı gibi bu komut satırı tooexisting hello yapı sunucuda komut dosyaları derleme veya derleme bir TFS tanımında hello komut satırını kullanabilirsiniz ya da ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09454-127">You can either add this command line tooexisting build scripts on hello build server, or you can use hello command line in a TFS Build Definition, as described in hello next section.</span></span> <span data-ttu-id="09454-128">Komut satırı parametreleri ve MSBuild hakkında daha fazla bilgi için bkz: [MSBuild komut satırı başvurusu](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="09454-128">For more information about command-line parameters and MSBuild, see [MSBuild Command Line Reference](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span></span>

1. <span data-ttu-id="09454-129">Visual Studio hello yapı sunucuda yüklüyse, bulun ve seçin **Visual Studio komut istemi** hello içinde **Visual Studio Araçları** Windows klasörü.</span><span class="sxs-lookup"><span data-stu-id="09454-129">If Visual Studio is installed on hello build server, locate and choose **Visual Studio Command Prompt** in hello **Visual Studio Tools** folder in Windows.</span></span>

   <span data-ttu-id="09454-130">Visual Studio hello yapı sunucuda yüklü değilse, bir komut istemi açın ve MSBuild.exe yola erişilebilir olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="09454-130">If Visual Studio is not installed on hello build server, open a command prompt and make sure that MSBuild.exe is accessible on the path.</span></span> <span data-ttu-id="09454-131">MSBuild hello yolu % WINDIR % hello .NET Framework yüklenmiş\\Microsoft.NET\\Framework\\*sürüm*.</span><span class="sxs-lookup"><span data-stu-id="09454-131">MSBuild is installed with hello .NET Framework in hello path %WINDIR%\\Microsoft.NET\\Framework\\*Version*.</span></span> <span data-ttu-id="09454-132">Örneğin, .NET Framework 4 yüklü olduğunda MSBuild.exe toohello PATH ortam değişkeni eklemek için komut hello komut isteminde aşağıdaki hello yazın:</span><span class="sxs-lookup"><span data-stu-id="09454-132">For example, to add MSBuild.exe toohello PATH environment variable when you have .NET Framework 4 installed, type hello following command at hello command prompt:</span></span>

       set PATH=%PATH%;"C:\Windows\Microsoft.NET\Framework\v4.0.30319"
2. <span data-ttu-id="09454-133">Hello komut isteminde toobuild istediğiniz Azure projesi dosyasını içeren toohello klasörüne gidin.</span><span class="sxs-lookup"><span data-stu-id="09454-133">At hello command prompt, navigate toohello folder containing the Azure project file that you want toobuild.</span></span>
3. <span data-ttu-id="09454-134">MSBuild ile Merhaba/target çalıştırın: yayımlama hello aşağıdaki örneğine olduğu gibi seçeneği:</span><span class="sxs-lookup"><span data-stu-id="09454-134">Run MSBuild with hello /target:Publish option as in hello following example:</span></span>

       MSBuild /target:Publish

   <span data-ttu-id="09454-135">Bu seçenek /t kısaltılır: yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="09454-135">This option can be abbreviated as /t:Publish.</span></span> <span data-ttu-id="09454-136">hello Azure SDK'sı yüklü olduğunda hello /t:Publish MSBuild seçeneğinde Visual Studio'da kullanılabilir hello Yayımla komutları ile karıştırılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="09454-136">hello /t:Publish option in MSBuild should not be confused with hello Publish commands available in Visual Studio when you have hello Azure SDK installed.</span></span> <span data-ttu-id="09454-137">/t hello: derlemeleri Azure paketleri hello yalnızca Publish seçeneği.</span><span class="sxs-lookup"><span data-stu-id="09454-137">hello /t:Publish option only builds hello Azure packages.</span></span> <span data-ttu-id="09454-138">Visual Studio'da Hello Yayımla komutları gibi hello paketleri dağıtmaz.</span><span class="sxs-lookup"><span data-stu-id="09454-138">It does not deploy hello packages as hello Publish commands in Visual Studio do.</span></span>

   <span data-ttu-id="09454-139">İsteğe bağlı olarak, bir MSBuild parametresi olarak hello proje adı belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09454-139">Optionally, you can specify hello project name as an MSBuild parameter.</span></span> <span data-ttu-id="09454-140">Belirtilmezse, geçerli dizin hello kullanılır.</span><span class="sxs-lookup"><span data-stu-id="09454-140">If not specified, hello current directory is used.</span></span> <span data-ttu-id="09454-141">MSBuild komut satırı seçenekleri hakkında daha fazla bilgi için bkz: [MSBuild komut satırı başvurusu](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="09454-141">For more information about MSBuild command line options, see [MSBuild Command Line Reference](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span></span>
4. <span data-ttu-id="09454-142">Merhaba çıkış bulun.</span><span class="sxs-lookup"><span data-stu-id="09454-142">Locate hello output.</span></span> <span data-ttu-id="09454-143">Varsayılan olarak, bu komutu bir ilişkisi toohello kök klasöründe hello projesi için gibi dizini *ProjectDir*\\bin\\*yapılandırma* \\ app.Publish\\.</span><span class="sxs-lookup"><span data-stu-id="09454-143">By default, this command creates a directory in relation toohello root folder for hello project, such as *ProjectDir*\\bin\\*Configuration*\\app.publish\\.</span></span> <span data-ttu-id="09454-144">Bir Azure projesi derlerken, iki dosya, hello paket dosyasının kendisini ve yapılandırma dosyası ile birlikte gelen hello oluştur:</span><span class="sxs-lookup"><span data-stu-id="09454-144">When you build an Azure project, you generate two files, hello package file itself and hello accompanying configuration file:</span></span>

   * <span data-ttu-id="09454-145">Project.cspkg</span><span class="sxs-lookup"><span data-stu-id="09454-145">Project.cspkg</span></span>
   * <span data-ttu-id="09454-146">ServiceConfiguration. *TargetProfile*.cscfg</span><span class="sxs-lookup"><span data-stu-id="09454-146">ServiceConfiguration.*TargetProfile*.cscfg</span></span>

   <span data-ttu-id="09454-147">Varsayılan olarak, her Azure projesi yerel (hata ayıklama) yapılar ve bulut (hazırlık veya üretim) yapılar için başka bir hizmet yapılandırma dosyası (.cscfg dosyası) içerir, ancak ekleyip gerektiği gibi hizmet yapılandırma dosyalarını kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09454-147">By default, each Azure project includes one service configuration file (.cscfg file) for local (debugging) builds and another for cloud (staging or production) builds, but you can add or remove service configuration files as needed.</span></span> <span data-ttu-id="09454-148">Visual Studio içinde bir paket oluşturduğunuzda, hangi hizmet yapılandırma dosyası tooinclude hello paket yanında istenir.</span><span class="sxs-lookup"><span data-stu-id="09454-148">When you build a package within Visual Studio, you will be asked which service configuration file tooinclude alongside hello package.</span></span>
5. <span data-ttu-id="09454-149">Merhaba hizmet yapılandırma dosyası belirtin.</span><span class="sxs-lookup"><span data-stu-id="09454-149">Specify hello service configuration file.</span></span> <span data-ttu-id="09454-150">MSBuild kullanarak bir paket oluşturduğunuzda, hello yerel hizmet yapılandırma dosyası varsayılan olarak dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="09454-150">When you build a package by using MSBuild, hello local service configuration file is included by default.</span></span> <span data-ttu-id="09454-151">tooinclude farklı hizmet yapılandırma dosyası aşağıdaki örneğine hello olduğu gibi hello MSBuild komut TargetProfile özelliğini ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="09454-151">tooinclude a different service configuration file, set the TargetProfile property of hello MSBuild command, as in hello following example:</span></span>

       MSBuild /t:Publish /p:TargetProfile=Cloud
6. <span data-ttu-id="09454-152">Merhaba Çıktı Hello konumunu belirtin.</span><span class="sxs-lookup"><span data-stu-id="09454-152">Specify hello location for hello output.</span></span> <span data-ttu-id="09454-153">/P:PublishDir kullanarak hello yolu ayarla =*Directory* \\ aşağıdaki örneğine hello olduğu gibi ters eğik çizgi ayırıcı sondaki hello dahil olmak üzere seçeneği:</span><span class="sxs-lookup"><span data-stu-id="09454-153">Set hello path by using the /p:PublishDir=*Directory*\\ option, including hello trailing backslash separator, as in hello following example:</span></span>

       MSBuild /target:Publish /p:PublishDir=\\myserver\drops\

   <span data-ttu-id="09454-154">Oluşturulur ve test sonra uygun MSBuild satır toobuild projelerinizi komut ve bunları Azure bir pakete birleştirmek, bu komut satırı tooyour yapı komut dosyaları ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09454-154">Once you've constructed and tested an appropriate MSBuild command line toobuild your projects and combine them into an Azure package, you can add this command line tooyour build scripts.</span></span> <span data-ttu-id="09454-155">Yapı sunucunuz özel komut dosyaları kullanıyorsa, bu işlem, özel derleme işlem ayrıntılarını bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="09454-155">If your build server uses custom scripts, this process will depend on the specifics of your custom build process.</span></span> <span data-ttu-id="09454-156">Ardından bir yapı ortamı olarak TFS kullanıyorsanız, hello sonraki adım tooadd hello Azure paketi yapı tooyour derleme işlemindeki hello yönergeleri izleyebilir.</span><span class="sxs-lookup"><span data-stu-id="09454-156">If you are using TFS as a build environment, then you can follow hello instructions in hello next step tooadd hello Azure package build tooyour build process.</span></span>

## <a name="3-build-a-package-using-tfs-team-build"></a><span data-ttu-id="09454-157">3: TFS ekip kullanarak bir paket oluşturun</span><span class="sxs-lookup"><span data-stu-id="09454-157">3: Build a Package using TFS Team Build</span></span>
<span data-ttu-id="09454-158">Varsa Team Foundation Server (TFS) bir yapı denetleyicisi ve hello sunucu yapı olarak ayarlamak TFS yapı makinesi olarak ayarlamak, ardından Azure paketiniz için otomatikleştirilmiş bir yapıyı isteğe bağlı olarak ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09454-158">If you have Team Foundation Server (TFS) set up as a build controller and hello build server set up as a TFS build machine, then you can optionally set up an automated build for your Azure package.</span></span> <span data-ttu-id="09454-159">Yukarı tooset ve bir yapı sistemi olarak kullanılmasını Team Foundation server nasıl görürüm hakkında bilgi için [derleme sisteminiz genişletme][Scale out your build system].</span><span class="sxs-lookup"><span data-stu-id="09454-159">For information on how tooset up and use Team Foundation server as a build system, see [Scale out your build system][Scale out your build system].</span></span> <span data-ttu-id="09454-160">Özellikle, aşağıdaki yordamda açıklandığı gibi yapı sunucunuz yapılandırdığınız varsayılmaktadır [dağıtma ve bir yapı sunucusunu yapılandırmak][Deploy and configure a build server], ve bir takım projesi oluşturduğunuz Bulutu oluşturulmuş Merhaba takım projesinde hizmet projesi.</span><span class="sxs-lookup"><span data-stu-id="09454-160">In particular, the following procedure assumes that you have configured your build server as described in [Deploy and configure a build server][Deploy and configure a build server], and that you have created a team project, created a cloud service project in hello team project.</span></span>

<span data-ttu-id="09454-161">tooconfigure TFS toobuild Azure paketler hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="09454-161">tooconfigure TFS toobuild Azure packages, perform hello following steps:</span></span>

1. <span data-ttu-id="09454-162">Visual Studio geliştirme bilgisayarınızda hello Görünüm menüsünde seçin **Takım Gezgini**, veya Ctrl + seçin\\, Ctrl + M.</span><span class="sxs-lookup"><span data-stu-id="09454-162">In Visual Studio on your development computer, on hello View menu, choose **Team Explorer**, or choose Ctrl+\\, Ctrl+M.</span></span> <span data-ttu-id="09454-163">Takım Gezgini penceresinde hello genişletin **derlemeler** düğümü veya hello seçin **derlemeler** sayfasında ve seçin **yeni yapı tanımı**.</span><span class="sxs-lookup"><span data-stu-id="09454-163">In the Team Explorer window, expand hello **Builds** node or choose hello **Builds** page, and choose **New Build Definition**.</span></span>

   ![Yeni bir yapı tanımı seçeneği][0]
2. <span data-ttu-id="09454-165">Merhaba seçin **tetikleyici** sekmesini tıklatın ve hello istenen istediğinizde koşulları hello yerleşik paket toobe belirtin.</span><span class="sxs-lookup"><span data-stu-id="09454-165">Choose hello **Trigger** tab, and specify hello desired conditions for when you want hello package toobe built.</span></span> <span data-ttu-id="09454-166">Örneğin, **sürekli tümleştirme** bir kaynak denetim her iade toobuild hello paket oluşur.</span><span class="sxs-lookup"><span data-stu-id="09454-166">For example, specify **Continuous Integration** toobuild hello package whenever a source control check-in occurs.</span></span>
3. <span data-ttu-id="09454-167">Merhaba seçin **kaynak ayarları** sekmesinde ve proje klasörünüzdeki hello listelendiğinden emin olun **kaynak denetimi klasörü** sütun ve hello durumu **etkin**.</span><span class="sxs-lookup"><span data-stu-id="09454-167">Choose hello **Source Settings** tab, and make sure your project folder is listed in hello **Source Control Folder** column, and hello status is **Active**.</span></span>
4. <span data-ttu-id="09454-168">Merhaba seçin **Yapı Varsayılanları** sekmesini tıklatın ve yapı denetleyicisi altında hello hello yapı sunucu adını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="09454-168">Choose hello **Build Defaults** tab, and under Build controller, verify hello name of hello build server.</span></span>  <span data-ttu-id="09454-169">Ayrıca, hello seçeneği **Kopyala derleme çıktı toohello aşağıdaki bırakma klasörü** ve istenen hello bırakma konumu belirtin.</span><span class="sxs-lookup"><span data-stu-id="09454-169">Also, choose hello option **Copy build output toohello following drop folder** and specify hello desired drop location.</span></span>
5. <span data-ttu-id="09454-170">Merhaba seçin **işlem** sekmesi. Merhaba işlem sekmesinde altında hello varsayılan şablonu seçin **yapı**, zaten seçili değilse ve hello genişletin hello proje belirleyin **Gelişmiş** hello bölümünde **Yapı**hello kılavuz bölümü.</span><span class="sxs-lookup"><span data-stu-id="09454-170">Choose hello **Process** tab. On hello Process tab, choose hello default template, under **Build**, choose hello project if it is not already selected, and expand hello **Advanced** section in hello **Build** section of hello grid.</span></span>
6. <span data-ttu-id="09454-171">Seçin **MSBuild bağımsız değişkenleri**, yukarıda 2. adımda açıklandığı gibi hello uygun MSBuild komut satırı bağımsız değişkenleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="09454-171">Choose **MSBuild Arguments**, and set hello appropriate MSBuild command line arguments as described in Step 2 above.</span></span> <span data-ttu-id="09454-172">Örneğin **/t: /p:PublishDir yayımlama =\\\\myserver\\bırakır\\**  toobuild bir paket ve kopyalama hello paket dosyaları toohello konumunu \\ \\myserver\\bırakır\\:</span><span class="sxs-lookup"><span data-stu-id="09454-172">For example, enter **/t:Publish /p:PublishDir=\\\\myserver\\drops\\** toobuild a package and copy hello package files toohello location \\\\myserver\\drops\\:</span></span>

   ![MSBuild bağımsız değişkenleri][2]

   > [!NOTE]
   > <span data-ttu-id="09454-174">Merhaba dosyaları tooa kopyalama ortak paylaşıma kolaylaştırır daha kolay toomanually geliştirme bilgisayarınızda hello paketlerinden dağıtın.</span><span class="sxs-lookup"><span data-stu-id="09454-174">Copying hello files tooa public share makes it easier toomanually deploy hello packages from your development computer.</span></span>
7. <span data-ttu-id="09454-175">Test, derleme adımının Hello başarılı bir değişiklik tooyour projesinde denetleyerek veya yeni bir yapıyı sıraya.</span><span class="sxs-lookup"><span data-stu-id="09454-175">Test hello success of your build step by checking in a change tooyour project, or queue up a new build.</span></span> <span data-ttu-id="09454-176">Takım Gezgini'nde, yeni bir derleme yukarı tooqueue sağ **tüm yapı tanımlarını** ve ardından **yeni yapıyı sıraya al**.</span><span class="sxs-lookup"><span data-stu-id="09454-176">tooqueue up a new build, in the Team Explorer, right-click **All Build Definitions,** and then choose **Queue New Build**.</span></span>

## <a name="4-publish-a-package-using-a-powershell-script"></a><span data-ttu-id="09454-177">4: bir PowerShell komut dosyası kullanarak bir paket yayımlama</span><span class="sxs-lookup"><span data-stu-id="09454-177">4: Publish a Package using a PowerShell Script</span></span>
<span data-ttu-id="09454-178">Bu bölümde, nasıl tooconstruct hello bulut uygulama paketi yayımlayacak bir Windows PowerShell Betiği isteğe bağlı parametreleri kullanarak tooAzure çıkış açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="09454-178">This section describes how tooconstruct a Windows PowerShell script that will publish hello Cloud app package output tooAzure using optional parameters.</span></span> <span data-ttu-id="09454-179">Bu komut dosyası Hello yapı adım sonra özel derleme otomasyonunuz çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="09454-179">This script can be called after hello build step in your custom build automation.</span></span> <span data-ttu-id="09454-180">Ayrıca, Visual Studio TFS takım yapısı içinde işlem şablonu iş akışı etkinliklerden de çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="09454-180">It can also be called from Process Template workflow activities in Visual Studio TFS Team Build.</span></span>

1. <span data-ttu-id="09454-181">Merhaba yüklemek [Azure PowerShell cmdlet'lerini] [ Azure PowerShell cmdlets] (v0.6.1 ya da daha yüksek).</span><span class="sxs-lookup"><span data-stu-id="09454-181">Install hello [Azure PowerShell cmdlets][Azure PowerShell cmdlets] (v0.6.1 or higher).</span></span>
   <span data-ttu-id="09454-182">Merhaba cmdlet kurulumu aşamasında tooinstall bir ek bileşeni seçin.</span><span class="sxs-lookup"><span data-stu-id="09454-182">During hello cmdlet setup phase, choose tooinstall as a snap-in.</span></span> <span data-ttu-id="09454-183">Hello önceki sürümler 2.x.x numaralı ancak bu resmi olarak desteklenen sürüm CodePlex sunulan hello eski sürümün yerine geçer unutmayın.</span><span class="sxs-lookup"><span data-stu-id="09454-183">Note that this officially supported version replaces hello older version offered through CodePlex, although hello previous versions were numbered 2.x.x.</span></span>
2. <span data-ttu-id="09454-184">Azure PowerShell hello Başlat menüsünden veya başlangıç sayfasını kullanarak başlatın.</span><span class="sxs-lookup"><span data-stu-id="09454-184">Start Azure PowerShell using hello Start menu or Start page.</span></span> <span data-ttu-id="09454-185">Bu yolla başlatırsanız, hello Azure PowerShell cmdlet'leri yüklenir.</span><span class="sxs-lookup"><span data-stu-id="09454-185">If you start in this way, hello Azure PowerShell cmdlets will be loaded.</span></span>
3. <span data-ttu-id="09454-186">Merhaba PowerShell isteminde hello PowerShell cmdlet'leri hello kısmi komutunu girerek yüklendiğini doğrulamak `Get-Azure` ve tuşuna basarak hello deyim tamamlama için SEKME tuşunu.</span><span class="sxs-lookup"><span data-stu-id="09454-186">At hello PowerShell prompt, verify that hello PowerShell cmdlets are loaded by entering hello partial command `Get-Azure` and then pressing hello Tab key for statement completion.</span></span>

   <span data-ttu-id="09454-187">Art arda hello SEKME tuşuna basın, çeşitli Azure PowerShell komutlarını görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="09454-187">If you press hello Tab key repeatedly, you should see various Azure PowerShell commands.</span></span>
4. <span data-ttu-id="09454-188">Abonelik bilgilerinizi hello .publishsettings dosyasından içeri aktararak tooyour Azure aboneliği bağlanabildiğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="09454-188">Verify that you can connect tooyour Azure subscription by importing your subscription information from hello .publishsettings file.</span></span>

   `Import-AzurePublishSettingsFile c:\scripts\WindowsAzure\default.publishsettings`

   <span data-ttu-id="09454-189">Merhaba komutu girin</span><span class="sxs-lookup"><span data-stu-id="09454-189">Then enter hello command</span></span>

   `Get-AzureSubscription`

   <span data-ttu-id="09454-190">Bu aboneliğiniz hakkında bilgi gösterir.</span><span class="sxs-lookup"><span data-stu-id="09454-190">This shows information about your subscription.</span></span> <span data-ttu-id="09454-191">Her şeyin doğru olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="09454-191">Verify that everything is correct.</span></span>
5. <span data-ttu-id="09454-192">Bu makalenin betikleri klasörünüze c: olarak hello sonunda sağlanan hello komut dosyası şablonu kaydetme\\betikleri\\WindowsAzure\\**PublishCloudService.ps1**.</span><span class="sxs-lookup"><span data-stu-id="09454-192">Save hello script template provided at hello end of this article to your scripts folder as c:\\scripts\\WindowsAzure\\**PublishCloudService.ps1**.</span></span>
6. <span data-ttu-id="09454-193">Merhaba komut Hello parametreleri bölümü gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="09454-193">Review hello parameters section of hello script.</span></span> <span data-ttu-id="09454-194">Ekleyin veya herhangi bir varsayılan değeri değiştirin.</span><span class="sxs-lookup"><span data-stu-id="09454-194">Add or modify any default values.</span></span> <span data-ttu-id="09454-195">Bu değerler, her zaman açık parametreleri geçirerek kılınabilir.</span><span class="sxs-lookup"><span data-stu-id="09454-195">These values can always be overridden by passing in explicit parameters.</span></span>
7. <span data-ttu-id="09454-196">Geçerli bir bulut hizmeti vardır ve komut dosyası hello tarafından hedeflenebilir aboneliğinizde oluşturulan depolama hesapları yayımlama emin olun.</span><span class="sxs-lookup"><span data-stu-id="09454-196">Ensure there are valid cloud service and storage accounts created in your subscription that can be targeted by hello publish script.</span></span> <span data-ttu-id="09454-197">Depolama hesabı (blob depolama) kullanılan tooupload olmalı ve dağıtım oluşturulurken hello dağıtım paketini ve yapılandırma dosyası geçici olarak depolar.</span><span class="sxs-lookup"><span data-stu-id="09454-197">The storage account (blob storage) will be used tooupload and temporarily store hello deployment package and config file while the deployment is being created.</span></span>

   * <span data-ttu-id="09454-198">toocreate yeni bir bulut hizmeti, bu komut dosyası veya kullanım hello çağırabilir [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="09454-198">toocreate a new cloud service, you can call this script or use hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="09454-199">Merhaba bulut hizmeti adı tam etki alanı adının öneki olarak kullanılır ve bu nedenle benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="09454-199">hello cloud service name will be used as a prefix in a fully qualified domain name and hence it must be unique.</span></span>

         New-AzureService -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
   * <span data-ttu-id="09454-200">toocreate yeni bir depolama hesabı, bu komut dosyası veya kullanım hello çağırabilir [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="09454-200">toocreate a new storage account, you can call this script or use hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="09454-201">Merhaba depolama hesabı adı tam etki alanı adının öneki olarak kullanılır ve bu nedenle benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="09454-201">hello storage account name will be used as a prefix in a fully qualified domain name and hence it must be unique.</span></span> <span data-ttu-id="09454-202">Bulut hizmeti olarak aynı ad hello kullanmayı deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09454-202">You can try using hello same name as the cloud service.</span></span>

         New-AzureStorageAccount -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
8. <span data-ttu-id="09454-203">Bu komut dosyası tooyour konak yapı Otomasyon toooccur hello paket derleme sonrası wire veya doğrudan Azure Powershell'den Hello betik çağırın.</span><span class="sxs-lookup"><span data-stu-id="09454-203">Call hello script directly from Azure PowerShell, or wire up this script tooyour host build automation toooccur after hello package build.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="09454-204">Merhaba komut dosyası her zaman silin veya bunlar algılanırsa, var olan dağıtımlar varsayılan olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="09454-204">hello script will always delete or replace your existing deployments by default if they are detected.</span></span> <span data-ttu-id="09454-205">Bu hiçbir kullanıcıdan mümkün olduğu Otomasyon sürekli teslimat etkinleştirmek gereklidir.</span><span class="sxs-lookup"><span data-stu-id="09454-205">This is necessary to enable continuous delivery from automation where no user prompting is possible.</span></span>
   >
   >

   <span data-ttu-id="09454-206">**Örnek Senaryo 1:** sürekli dağıtım toohello bir hizmeti ortamını hazırlama:</span><span class="sxs-lookup"><span data-stu-id="09454-206">**Example scenario 1:** continuous deployment toohello staging environment of a service:</span></span>

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Staging -serviceName mycloudservice -storageAccountName mystoragesaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   <span data-ttu-id="09454-207">Bu genellikle doğrulama ve bir VIP takası testi tarafından izlendiğinden.</span><span class="sxs-lookup"><span data-stu-id="09454-207">This is typically followed up by test run verification and a VIP swap.</span></span> <span data-ttu-id="09454-208">Merhaba VIP takas hello yapılabilir [Azure portal](https://portal.azure.com) veya hello taşıma dağıtım cmdlet'ini kullanarak.</span><span class="sxs-lookup"><span data-stu-id="09454-208">hello VIP swap can be done via hello [Azure portal](https://portal.azure.com) or by using hello Move-Deployment cmdlet.</span></span>

   <span data-ttu-id="09454-209">**Örnek Senaryo 2:** sürekli dağıtım toohello üretim ortamına ayrılmış sınama hizmeti</span><span class="sxs-lookup"><span data-stu-id="09454-209">**Example scenario 2:** continuous deployment toohello production environment of a dedicated test service</span></span>

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Production -enableDeploymentUpgrade 1 -serviceName mycloudservice -storageAccountName mystorageaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   <span data-ttu-id="09454-210">**Uzak Masaüstü:**</span><span class="sxs-lookup"><span data-stu-id="09454-210">**Remote Desktop:**</span></span>

   <span data-ttu-id="09454-211">Uzak Masaüstü Azure projenizde etkinse, bu komut dosyası tarafından hedeflenen tooall bulut Hizmetleri tooensure hello doğru bulut hizmet sertifikası karşıya tooperform ek tek seferlik adımlar gerekir.</span><span class="sxs-lookup"><span data-stu-id="09454-211">If Remote Desktop is enabled in your Azure project you will need tooperform additional one-time steps tooensure hello correct Cloud Service Certificate is uploaded tooall cloud services targeted by this script.</span></span>

   <span data-ttu-id="09454-212">Rolleri tarafından beklenen hello sertifika parmak izi değerlerini bulun.</span><span class="sxs-lookup"><span data-stu-id="09454-212">Locate hello certificate thumbprint values expected by your roles.</span></span> <span data-ttu-id="09454-213">Parmak izi değerleri bulut yapılandırma dosyasının (yani ServiceConfiguration.Cloud.cscfg) sertifikaları bölümünde hello görülebilir.</span><span class="sxs-lookup"><span data-stu-id="09454-213">The thumbprint values are visible in hello Certificates section of the cloud config file (i.e. ServiceConfiguration.Cloud.cscfg).</span></span> <span data-ttu-id="09454-214">Seçenekleri Göster ve görünüm hello sertifika seçtiğinizde de Visual Studio'da hello uzak masaüstü yapılandırması iletişim kutusu görünür.</span><span class="sxs-lookup"><span data-stu-id="09454-214">It is also visible in hello Remote Desktop Configuration dialog in Visual Studio when you Show Options and view hello selected certificate.</span></span>

       <Certificates>
             <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption" thumbprint="C33B6C432C25581601B84C80F86EC2809DC224E8" thumbprintAlgorithm="sha1" />
       </Certificates>

   <span data-ttu-id="09454-215">Uzak Masaüstü sertifikaları cmdlet komut dosyası izleyen hello kullanarak bir kerelik Kurulum adım olarak karşıya yükle:</span><span class="sxs-lookup"><span data-stu-id="09454-215">Upload Remote Desktop certificates as a one-time setup step using hello following cmdlet script:</span></span>

       Add-AzureCertificate -serviceName <CLOUDSERVICENAME> -certToDeploy (get-item cert:\CurrentUser\MY\<THUMBPRINT>)

   <span data-ttu-id="09454-216">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="09454-216">For example:</span></span>

       Add-AzureCertificate -serviceName 'mytestcloudservice' -certToDeploy (get-item cert:\CurrentUser\MY\C33B6C432C25581601B84C80F86EC2809DC224E8

   <span data-ttu-id="09454-217">Alternatif olarak özel anahtar ve karşıya yükleme sertifikaları tooeach hedef bulut hizmetini kullanarak hello sertifika dosyası PFX dışa aktarabilirsiniz [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="09454-217">Alternatively you can export hello certificate file PFX with private key and upload certificates tooeach target cloud service using the [Azure portal](https://portal.azure.com).</span></span>

   <!---
   Fixing broken links for Azure content migration from ACOM tooDOCS. I'm unable toofind a replacement links, so I'm commenting out this reference for now. hello author can investigate in hello future. "Read hello following article toolearn more: http://msdn.microsoft.com/library/windowsazure/gg443832.aspx.
   -->
   <span data-ttu-id="09454-218">**Dağıtım vs yükseltin. Dağıtım - Sil\> yeni dağıtım**</span><span class="sxs-lookup"><span data-stu-id="09454-218">**Upgrade Deployment vs. Delete Deployment -\> New Deployment**</span></span>

   <span data-ttu-id="09454-219">Merhaba betik varsayılan olarak gerçekleştirecek bir yükseltme dağıtımı ($enableDeploymentUpgrade = 1) ne zaman hiçbir parametre geçirilen veya 1 değerini açıkça geçirilir.</span><span class="sxs-lookup"><span data-stu-id="09454-219">hello script will by default perform an Upgrade Deployment ($enableDeploymentUpgrade = 1) when no parameter is passed in or the value 1 is passed explicitly.</span></span> <span data-ttu-id="09454-220">Tek örnekleri için tam dağıtımını daha az zaman ayırdığınız avantajı vardır.</span><span class="sxs-lookup"><span data-stu-id="09454-220">For single instances this has the advantage of taking less time than a full deployment.</span></span> <span data-ttu-id="09454-221">Ayrıca bazı örnek diğerlerinde çalışıyor bırakarak hello avantajı vardır yüksek kullanılabilirliğin gerektiği örnekleri (, güncelleştirme etki alanının yürütülmesi) yükseltilir, artı, VIP silinmeyecek için.</span><span class="sxs-lookup"><span data-stu-id="09454-221">For instances that require high availability this also has hello advantage of leaving some instances running while others are upgraded (walking your update domain), plus your VIP will not be deleted.</span></span>

   <span data-ttu-id="09454-222">Yükseltme dağıtımı devre dışı bırakılabilir hello komut dosyasında ($enableDeploymentUpgrade = 0) veya geçirerek *- enableDeploymentUpgrade 0* bir parametre olarak varolan tüm dağıtım komut dosyası davranışı toofirst delete değiştirir ve ardından oluşturun bir yeni dağıtım.</span><span class="sxs-lookup"><span data-stu-id="09454-222">Upgrade Deployment can be disabled in hello script ($enableDeploymentUpgrade = 0) or by passing *-enableDeploymentUpgrade 0* as a parameter, which alters the script behavior toofirst delete any existing deployment and then create a new deployment.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="09454-223">Merhaba komut dosyası her zaman silin veya bunlar algılanırsa, var olan dağıtımlar varsayılan olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="09454-223">hello script will always delete or replace your existing deployments by default if they are detected.</span></span> <span data-ttu-id="09454-224">Hiçbir kullanıcı/işleci isteyen mümkün olduğu Otomasyon sürekli teslimat etkinleştirmek için gereken budur.</span><span class="sxs-lookup"><span data-stu-id="09454-224">This is necessary to enable continuous delivery from automation where no user/operator prompting is possible.</span></span>
   >
   >

## <a name="5-publish-a-package-using-tfs-team-build"></a><span data-ttu-id="09454-225">5: TFS ekip kullanarak paket yayımlama</span><span class="sxs-lookup"><span data-stu-id="09454-225">5: Publish a Package using TFS Team Build</span></span>
<span data-ttu-id="09454-226">Bu isteğe bağlı adım yayımlama hello paketi yapı tooAzure, işleyen 4. adımda oluşturduğunuz TFS ekip toohello betik bağlanır.</span><span class="sxs-lookup"><span data-stu-id="09454-226">This optional step connects TFS Team Build toohello script created in step 4, which handles publishing of hello package build tooAzure.</span></span> <span data-ttu-id="09454-227">Bu, değiştirme hello işlem hello hello iş akışının sonunda bir yayımlama etkinliği çalışır, yapı tanımı tarafından kullanılan şablonu kapsar.</span><span class="sxs-lookup"><span data-stu-id="09454-227">This entails modifying hello Process Template used by your build definition so that it runs a Publish activity at hello end of hello workflow.</span></span> <span data-ttu-id="09454-228">Merhaba Yayımla etkinlik parametrelerinde hello yapıdan geçirme, PowerShell komutunu çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="09454-228">hello Publish activity will execute your PowerShell command passing in parameters from hello build.</span></span> <span data-ttu-id="09454-229">MSBuild hedefler ve komut dosyası yayımlama hello çıktısını yöneltilen hello standart yapı çıkış.</span><span class="sxs-lookup"><span data-stu-id="09454-229">Output of hello MSBuild targets and publish script will be piped into hello standard build output.</span></span>

1. <span data-ttu-id="09454-230">Yapı tanımı sorumlu Hello Düzenle sürekli dağıtın.</span><span class="sxs-lookup"><span data-stu-id="09454-230">Edit hello Build Definition responsible for continuous deploy.</span></span>
2. <span data-ttu-id="09454-231">Select hello **işlem** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="09454-231">Select hello **Process** tab.</span></span>
3. <span data-ttu-id="09454-232">İzleyin [bu yönergeleri](http://msdn.microsoft.com/library/dd647551.aspx) tooadd bir etkinlik projesi hello için yapı işlem şablonu, hello varsayılan şablonunu indirebilir, hello projeye ekleyin ve iade etme.</span><span class="sxs-lookup"><span data-stu-id="09454-232">Follow [these instructions](http://msdn.microsoft.com/library/dd647551.aspx) tooadd an Activity project for hello build process template, download hello default template, add it to hello project and check it in.</span></span> <span data-ttu-id="09454-233">Merhaba derleme işlem şablonu AzureBuildProcessTemplate gibi yeni bir ad verin.</span><span class="sxs-lookup"><span data-stu-id="09454-233">Give hello build process template a new name, such as AzureBuildProcessTemplate.</span></span>
4. <span data-ttu-id="09454-234">Toohello iade **işlem** sekmesini tıklatın ve kullanmak **ayrıntıları göster** tooshow kullanılabilir yapı işlem şablonları listesi.</span><span class="sxs-lookup"><span data-stu-id="09454-234">Return toohello **Process** tab, and use **Show Details** tooshow a list of available build process templates.</span></span> <span data-ttu-id="09454-235">Merhaba seçin **yeni...**  düğmesine tıklayın ve yalnızca eklenir ve iade toohello proje gidin.</span><span class="sxs-lookup"><span data-stu-id="09454-235">Choose hello **New...** button, and navigate toohello project you just added and checked in.</span></span> <span data-ttu-id="09454-236">Yeni oluşturduğunuz hello şablonu bulun ve seçin **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="09454-236">Locate hello template you just created and choose **OK**.</span></span>
5. <span data-ttu-id="09454-237">Açık hello düzenleme için işlem şablonu seçili.</span><span class="sxs-lookup"><span data-stu-id="09454-237">Open hello selected Process Template for editing.</span></span> <span data-ttu-id="09454-238">Doğrudan hello iş akışı Tasarımcısı'nda veya hello XML Düzenleyicisi toowork hello XAML ile açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09454-238">You can open directly in hello Workflow designer or in hello XML editor toowork with hello XAML.</span></span>
6. <span data-ttu-id="09454-239">Ayrı satır öğeleri hello bağımsız değişkenleri sekmesi hello iş akışı Tasarımcısı'nın olarak yeni bağımsız değişkenlerinin listesi aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="09454-239">Add hello following list of new arguments as separate line items in hello arguments tab of hello workflow designer.</span></span> <span data-ttu-id="09454-240">Tüm bağımsız değişkenler yönü olması gerekir, = ve türü = String.</span><span class="sxs-lookup"><span data-stu-id="09454-240">All arguments should have direction=In and type=String.</span></span> <span data-ttu-id="09454-241">Bunlar hangi sonra get kullanılan toocall hello betik yayımlama hello akışına hello yapı tanımından kullanılan tooflow parametreleri olacaktır.</span><span class="sxs-lookup"><span data-stu-id="09454-241">These will be used tooflow parameters from hello build definition into hello workflow, which then get used toocall hello publish script.</span></span>

       SubscriptionName
       StorageAccountName
       CloudConfigLocation
       PackageLocation
       Environment
       SubscriptionDataFileLocation
       PublishScriptLocation
       ServiceName

   ![Bağımsız değişkenler listesi][3]

   <span data-ttu-id="09454-243">Merhaba karşılık gelen XAML şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="09454-243">hello corresponding XAML looks like this:</span></span>

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
7. <span data-ttu-id="09454-244">Yeni bir sıra hello Aracısını Çalıştır sonuna ekleyin:</span><span class="sxs-lookup"><span data-stu-id="09454-244">Add a new sequence at hello end of Run On Agent:</span></span>

   1. <span data-ttu-id="09454-245">Geçerli komut dosyası için bir If ifadesinden etkinlik toocheck ekleyerek başlayın.</span><span class="sxs-lookup"><span data-stu-id="09454-245">Start by adding an If Statement activity toocheck for a valid script file.</span></span> <span data-ttu-id="09454-246">Merhaba koşul toothis değeri ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="09454-246">Set hello condition toothis value:</span></span>

          Not String.IsNullOrEmpty(PublishScriptLocation)
   2. <span data-ttu-id="09454-247">Hello hello If ifadesinden sonra bir durumunun, yeni bir dizi etkinlik ekleyin.</span><span class="sxs-lookup"><span data-stu-id="09454-247">In hello Then case of hello If Statement, add a new Sequence activity.</span></span> <span data-ttu-id="09454-248">Set hello görünen adı too'Start Yayımla '</span><span class="sxs-lookup"><span data-stu-id="09454-248">Set hello display name too'Start publish'</span></span>
   3. <span data-ttu-id="09454-249">Başlangıç dizisi seçiliyken yayımlama hello ile yeni değişkenleri aşağıdaki listesini ayrı satırı öğeleri hello iş akışı Tasarımcısı'nın değişkenleri sekmesi olarak ekleyin.</span><span class="sxs-lookup"><span data-stu-id="09454-249">With hello Start publish sequence still selected, add the following list of new variables as separate line items in the variables tab of hello workflow designer.</span></span> <span data-ttu-id="09454-250">Tüm değişkenleri değişken türü olmalıdır = dize ve kapsam başlangıç = yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="09454-250">All variables should have Variable type =String and Scope=Start publish.</span></span> <span data-ttu-id="09454-251">Bu iş akışına hangi sonra get kullanılan toocall hello betik yayımlama hello yapı tanımından kullanılan tooflow parametreleri olacaktır.</span><span class="sxs-lookup"><span data-stu-id="09454-251">These will be used tooflow parameters from hello build definition into the workflow, which then get used toocall hello publish script.</span></span>

      * <span data-ttu-id="09454-252">Dize türünde SubscriptionDataFilePath</span><span class="sxs-lookup"><span data-stu-id="09454-252">SubscriptionDataFilePath, of type String</span></span>
      * <span data-ttu-id="09454-253">Dize türünde PublishScriptFilePath</span><span class="sxs-lookup"><span data-stu-id="09454-253">PublishScriptFilePath, of type String</span></span>

        ![Yeni değişkenleri][4]
   4. <span data-ttu-id="09454-255">Daha önce ConvertWorkspaceItem Etkinlik başına hello Ekle veya TFS 2012 kullanıyorsanız yeni sırası hello.</span><span class="sxs-lookup"><span data-stu-id="09454-255">If you are using TFS 2012 or earlier, add a ConvertWorkspaceItem activity at hello beginning of hello new Sequence.</span></span> <span data-ttu-id="09454-256">TFS 2013 veya üzeri kullanıyorsanız, GetLocalPath etkinlik hello hello yeni sırası başında ekleyin.</span><span class="sxs-lookup"><span data-stu-id="09454-256">If you are using TFS 2013 or later, add a GetLocalPath activity at hello beginning of hello new sequence.</span></span> <span data-ttu-id="09454-257">Bir ConvertWorkspaceItem için hello özellikleri aşağıdaki gibi ayarlayın: yönü ServerToLocal, DisplayName = 'Dönüştürme Yayımla betik filename' = giriş 'PublishScriptLocation', sonuç = 'PublishScriptFilePath', çalışma alanı = = 'Çalışma alanı'.</span><span class="sxs-lookup"><span data-stu-id="09454-257">For a ConvertWorkspaceItem, set hello properties as follows: Direction=ServerToLocal, DisplayName='Convert publish script filename', Input=' PublishScriptLocation', Result='PublishScriptFilePath', Workspace='Workspace'.</span></span> <span data-ttu-id="09454-258">Merhaba özelliği IncomingPath too'PublishScriptLocation bir GetLocalPath etkinliği için ayarlandı ', ve sonuç too'PublishScriptFilePath hello'.</span><span class="sxs-lookup"><span data-stu-id="09454-258">For a GetLocalPath activity, set hello property IncomingPath too'PublishScriptLocation', and hello Result too'PublishScriptFilePath'.</span></span> <span data-ttu-id="09454-259">Bu etkinlik dönüştürür hello yolu toohello yayımlama TFS sunucusu konumlardan komut dosyası (eğer varsa) tooa standart yerel disk yolu.</span><span class="sxs-lookup"><span data-stu-id="09454-259">This activity converts hello path toohello publish script from TFS server locations (if applicable) tooa standard local disk path.</span></span>
   5. <span data-ttu-id="09454-260">Daha önce başka bir ConvertWorkspaceItem etkinlik hello sonuna ekleyin veya TFS 2012 kullanıyorsanız yeni sırası hello.</span><span class="sxs-lookup"><span data-stu-id="09454-260">If you are using TFS 2012 or earlier, add another ConvertWorkspaceItem activity at hello end of hello new Sequence.</span></span> <span data-ttu-id="09454-261">Yön ServerToLocal, DisplayName = 'abonelik filename Dönüştür' = giriş 'SubscriptionDataFileLocation', sonuç = 'SubscriptionDataFilePath', çalışma alanı = = 'Çalışma alanı'.</span><span class="sxs-lookup"><span data-stu-id="09454-261">Direction=ServerToLocal, DisplayName='Convert subscription filename', Input=' SubscriptionDataFileLocation', Result= 'SubscriptionDataFilePath', Workspace='Workspace'.</span></span> <span data-ttu-id="09454-262">TFS 2013 veya üzeri kullanıyorsanız, başka bir GetLocalPath ekleyin.</span><span class="sxs-lookup"><span data-stu-id="09454-262">If you are using TFS 2013 or later, add another GetLocalPath.</span></span> <span data-ttu-id="09454-263">IncomingPath 'SubscriptionDataFileLocation' = ve sonuç 'SubscriptionDataFilePath.' =</span><span class="sxs-lookup"><span data-stu-id="09454-263">IncomingPath='SubscriptionDataFileLocation', and Result='SubscriptionDataFilePath.'</span></span>
   6. <span data-ttu-id="09454-264">InvokeProcess aktivite hello hello sonuna ekle yeni sırası.</span><span class="sxs-lookup"><span data-stu-id="09454-264">Add an InvokeProcess activity at hello end of hello new Sequence.</span></span>
      <span data-ttu-id="09454-265">Bu etkinlik çağrıları PowerShell.exe hello bağımsız değişkenlerle hello yapı tanımı tarafından geçirildi.</span><span class="sxs-lookup"><span data-stu-id="09454-265">This activity calls PowerShell.exe with hello arguments passed in by hello Build Definition.</span></span>

      + <span data-ttu-id="09454-266">Bağımsız değişkenler String.Format = ("-""{0}" "- serviceName {1} - storageAccountName {2} - packageLocation""{3}" "- cloudConfigLocation""{4}" "- subscriptionDataFile""{5}" "- selectedSubscription {6} dosya-ortam""{7}" "",  PublishScriptFilePath, ServiceName, StorageAccountName, PackageLocation, CloudConfigLocation, SubscriptionDataFilePath, varlığıyla SubscriptionName, ortamı)</span><span class="sxs-lookup"><span data-stu-id="09454-266">Arguments = String.Format(" -File ""{0}"" -serviceName {1}  -storageAccountName {2} -packageLocation ""{3}""  -cloudConfigLocation ""{4}"" -subscriptionDataFile ""{5}""  -selectedSubscription {6} -environment ""{7}""",  PublishScriptFilePath, ServiceName, StorageAccountName,  PackageLocation, CloudConfigLocation,  SubscriptionDataFilePath, SubscriptionName, Environment)</span></span>
      + <span data-ttu-id="09454-267">DisplayName Execute = betik yayımlama</span><span class="sxs-lookup"><span data-stu-id="09454-267">DisplayName = Execute publish script</span></span>
      + <span data-ttu-id="09454-268">Dosya adı "PowerShell" = (Merhaba tırnak işaretleri dahil)</span><span class="sxs-lookup"><span data-stu-id="09454-268">FileName = "PowerShell" (include hello quotes)</span></span>
      + <span data-ttu-id="09454-269">OutputEncoding System.Text.Encoding.GetEncoding(System.Globalization.CultureInfo.InstalledUICulture.TextInfo.OEMCodePage) =</span><span class="sxs-lookup"><span data-stu-id="09454-269">OutputEncoding=  System.Text.Encoding.GetEncoding(System.Globalization.CultureInfo.InstalledUICulture.TextInfo.OEMCodePage)</span></span>
   7. <span data-ttu-id="09454-270">Merhaba, **işlemek standart çıktı** hello textbox değeri too'data bölümünde InvokeProcess textbox,'.</span><span class="sxs-lookup"><span data-stu-id="09454-270">In hello **Handle Standard Output** section textbox of the InvokeProcess, set hello textbox value too'data'.</span></span> <span data-ttu-id="09454-271">Bir değişken toostore hello standart çıktı verileri budur.</span><span class="sxs-lookup"><span data-stu-id="09454-271">This is a variable toostore hello standard output data.</span></span>
   8. <span data-ttu-id="09454-272">Merhaba hemen altındaki WriteBuildMessage etkinlik eklemek **işlemek standart çıktı** bölümü.</span><span class="sxs-lookup"><span data-stu-id="09454-272">Add a WriteBuildMessage activity just below hello **Handle Standard Output** section.</span></span> <span data-ttu-id="09454-273">Merhaba önem ayarlamak = 'Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High' ve hello Message = 'data'.</span><span class="sxs-lookup"><span data-stu-id="09454-273">Set hello Importance = 'Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High' and hello Message='data'.</span></span> <span data-ttu-id="09454-274">Bu komut dosyasının hello standart çıktı toohello yapı çıktı yazılmış sağlar.</span><span class="sxs-lookup"><span data-stu-id="09454-274">This ensures hello standard output of the script will get written toohello build output.</span></span>
   9. <span data-ttu-id="09454-275">Merhaba, **hata çıkış işleme** hello textbox değeri too'data bölümünde InvokeProcess textbox,'.</span><span class="sxs-lookup"><span data-stu-id="09454-275">In hello **Handle Error Output** section textbox of the InvokeProcess, set hello textbox value too'data'.</span></span> <span data-ttu-id="09454-276">Bu bir değişken toostore hello standart hata verilerdir.</span><span class="sxs-lookup"><span data-stu-id="09454-276">This is a variable toostore hello standard error data.</span></span>
   10. <span data-ttu-id="09454-277">Merhaba hemen altındaki WriteBuildError etkinlik eklemek **hata çıkış işleme** bölümü.</span><span class="sxs-lookup"><span data-stu-id="09454-277">Add a WriteBuildError activity just below hello **Handle Error Output** section.</span></span> <span data-ttu-id="09454-278">Merhaba ileti Ayarla = 'data'.</span><span class="sxs-lookup"><span data-stu-id="09454-278">Set hello Message='data'.</span></span> <span data-ttu-id="09454-279">Bu, hello standart hatalar hello komut toohello yapı hata çıktısı yazılan sağlar.</span><span class="sxs-lookup"><span data-stu-id="09454-279">This ensures hello standard errors of hello script will get written toohello build error output.</span></span>
   11. <span data-ttu-id="09454-280">Mavi ünlem işaretleri tarafından belirtilen tüm hataları düzeltin.</span><span class="sxs-lookup"><span data-stu-id="09454-280">Correct any errors, indicated by blue exclamation marks.</span></span> <span data-ttu-id="09454-281">Ünlem işaretleri tooget hello hata hakkında bir ipucu gelin.</span><span class="sxs-lookup"><span data-stu-id="09454-281">Hover over the exclamation marks tooget a hint about hello error.</span></span> <span data-ttu-id="09454-282">Hataları temizlemek için hello iş akışını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="09454-282">Save hello workflow to clear errors.</span></span>

   <span data-ttu-id="09454-283">Merhaba Hello sonucunu Yayımla iş akışı etkinlikleri hello Tasarımcısı'nda şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="09454-283">hello final result of hello publish workflow activities will look like this in hello designer:</span></span>

   ![İş akışı etkinlikleri][5]

   <span data-ttu-id="09454-285">İş akışı etkinlikleri XAML'de şuna benzeyecektir yayımlama hello Hello sonucunu:</span><span class="sxs-lookup"><span data-stu-id="09454-285">hello final result of hello publish workflow activities will look like this in XAML:</span></span>

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
8. <span data-ttu-id="09454-286">Merhaba yapı işlem şablonu iş akışı ve iade bu dosyayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="09454-286">Save hello build process template workflow and Check In this file.</span></span>
9. <span data-ttu-id="09454-287">Hello yapı tanımını Düzenle (kapatın, zaten açıksa) ve select hello **yeni** hello yeni şablon olarak işlem şablonlarını hello listesinde henüz görmüyorsanız düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="09454-287">Edit hello build definition (close it if it is already open), and select hello **New** button if you do not yet see hello new template in hello list of Process Templates.</span></span>
10. <span data-ttu-id="09454-288">Hello parametre özellik değerlerini hello çeşitli bölümü aşağıdaki gibi ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="09454-288">Set hello parameter property values in hello Misc section as follows:</span></span>

    1. <span data-ttu-id="09454-289">CloudConfigLocation ='c:\\bırakır\\app.publish\\ServiceConfiguration.Cloud.cscfg' *bu değer türetilir: ($PublishDir)ServiceConfiguration.Cloud.cscfg*</span><span class="sxs-lookup"><span data-stu-id="09454-289">CloudConfigLocation ='c:\\drops\\app.publish\\ServiceConfiguration.Cloud.cscfg' *This value is derived from: ($PublishDir)ServiceConfiguration.Cloud.cscfg*</span></span>
    2. <span data-ttu-id="09454-290">PackageLocation = ' c:\\bırakır\\app.publish\\ContactManager.Azure.cspkg' *bu değer türetilir: ($PublishDir)($ProjectName) .cspkg*</span><span class="sxs-lookup"><span data-stu-id="09454-290">PackageLocation = 'c:\\drops\\app.publish\\ContactManager.Azure.cspkg' *This value is derived from: ($PublishDir)($ProjectName).cspkg*</span></span>
    3. <span data-ttu-id="09454-291">PublishScriptLocation = ' c:\\betikleri\\WindowsAzure\\PublishCloudService.ps1'</span><span class="sxs-lookup"><span data-stu-id="09454-291">PublishScriptLocation = 'c:\\scripts\\WindowsAzure\\PublishCloudService.ps1'</span></span>
    4. <span data-ttu-id="09454-292">ServiceName = 'mycloudservicename' *hello uygun bulut hizmeti adını kullan burada*</span><span class="sxs-lookup"><span data-stu-id="09454-292">ServiceName = 'mycloudservicename' *Use hello appropriate cloud service name here*</span></span>
    5. <span data-ttu-id="09454-293">Ortam 'Hazırlama' =</span><span class="sxs-lookup"><span data-stu-id="09454-293">Environment = 'Staging'</span></span>
    6. <span data-ttu-id="09454-294">StorageAccountName 'mystorageaccountname' = *kullanım hello uygun depolama hesabı adı buraya*</span><span class="sxs-lookup"><span data-stu-id="09454-294">StorageAccountName = 'mystorageaccountname' *Use hello appropriate storage account name here*</span></span>
    7. <span data-ttu-id="09454-295">SubscriptionDataFileLocation = ' c:\\betikleri\\WindowsAzure\\Subscription.xml'</span><span class="sxs-lookup"><span data-stu-id="09454-295">SubscriptionDataFileLocation = 'c:\\scripts\\WindowsAzure\\Subscription.xml'</span></span>
    8. <span data-ttu-id="09454-296">Varlığıyla SubscriptionName = 'varsayılan'</span><span class="sxs-lookup"><span data-stu-id="09454-296">SubscriptionName = 'default'</span></span>

    ![Parametre özellik değerleri][6]
11. <span data-ttu-id="09454-298">Merhaba değişiklikleri toohello yapı tanımı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="09454-298">Save hello changes toohello Build Definition.</span></span>
12. <span data-ttu-id="09454-299">Her ikisi de paket yapı hello ve yayımlama yapı tooexecute sırası.</span><span class="sxs-lookup"><span data-stu-id="09454-299">Queue a Build tooexecute both hello package build and publish.</span></span> <span data-ttu-id="09454-300">TooContinuous tümleştirme ayarlamak tetikleyici varsa, her iade Bu davranış yürütülür.</span><span class="sxs-lookup"><span data-stu-id="09454-300">If you have a trigger set tooContinuous Integration, you will execute this behavior on every check-in.</span></span>

### <a name="publishcloudserviceps1-script-template"></a><span data-ttu-id="09454-301">PublishCloudService.ps1 komut dosyası şablonu</span><span class="sxs-lookup"><span data-stu-id="09454-301">PublishCloudService.ps1 script template</span></span>
```
Param(  $serviceName = "",
        $storageAccountName = "",
        $packageLocation = "",
        $cloudConfigLocation = "",
        $environment = "Staging",
        $deploymentLabel = "ContinuousDeploy too$servicename",
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
    #check for existing deployment and then either upgrade, delete + deploy, or cancel according too$alwaysDeleteExistingDeployments and $enableDeploymentUpgrade boolean variables
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

#main driver - publish & write progress tooactivity log
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script started."
Write-Output "$(Get-Date -f $timeStampFormat) - Preparing deployment of $deploymentLabel for $subscriptionname with Subscription ID $subscriptionid."

Publish

$deployment = Get-AzureDeployment -slot $slot -serviceName $servicename
$deploymentUrl = $deployment.Url

Write-Output "$(Get-Date -f $timeStampFormat) - Created Cloud Service with URL $deploymentUrl."
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script finished."
```

## <a name="next-steps"></a><span data-ttu-id="09454-302">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="09454-302">Next steps</span></span>
<span data-ttu-id="09454-303">tooenable uzaktan kesintisiz teslim kullanılırken hata ayıklama bkz [kesintisiz teslim toopublish tooAzure kullanırken uzaktan hata ayıklamayı etkinleştirme](cloud-services-virtual-machines-dotnet-continuous-delivery-remote-debugging.md).</span><span class="sxs-lookup"><span data-stu-id="09454-303">tooenable remote debugging when using continuous delivery, see [Enable remote debugging when using continuous delivery toopublish tooAzure](cloud-services-virtual-machines-dotnet-continuous-delivery-remote-debugging.md).</span></span>

[Team Foundation Build Service]: https://msdn.microsoft.com/library/ee259687.aspx
[.NET Framework 4]: https://www.microsoft.com/download/details.aspx?id=17851
[.NET Framework 4.5]: https://www.microsoft.com/download/details.aspx?id=30653
[.NET Framework 4.5.2]: https://www.microsoft.com/download/details.aspx?id=42643
[Scale out your build system]: https://msdn.microsoft.com/library/dd793166.aspx
[Deploy and configure a build server]: https://msdn.microsoft.com/library/ms181712.aspx
[Azure PowerShell cmdlets]: /powershell/azureps-cmdlets-docs
[hello .publishsettings file]: https://manage.windowsazure.com/download/publishprofile.aspx?wa=wsignin1.0
[0]: ./media/cloud-services-dotnet-continuous-delivery/tfs-01bc.png
[2]: ./media/cloud-services-dotnet-continuous-delivery/tfs-02.png
[3]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-03.png
[4]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-04.png
[5]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-05.png
[6]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-06.png
