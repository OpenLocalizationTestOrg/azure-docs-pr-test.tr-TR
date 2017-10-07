---
title: "aaaUsing Windows PowerShell betikleri tooPublish tooDev ve Test ortamları | Microsoft Docs"
description: "Nasıl Visual Studio toopublish toodevelopment ve test ortamları toouse Windows PowerShell komut dosyaları hakkında bilgi edinin."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5fff1301-5469-4d97-be88-c85c30f837c1
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 491a058f96255576afa74f6156f20ae9559bb9f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-windows-powershell-scripts-toopublish-toodev-and-test-environments"></a><span data-ttu-id="e9d39-103">Windows PowerShell kullanarak toopublish toodev ve test ortamları komut dosyaları</span><span class="sxs-lookup"><span data-stu-id="e9d39-103">Using Windows PowerShell scripts toopublish toodev and test environments</span></span>
<span data-ttu-id="e9d39-104">Visual Studio'da bir web uygulaması oluşturduğunuzda, bir Web uygulamasını Azure App Service veya bir sanal makine olarak Web sitesi tooAzure sonraki tooautomate hello yayımlanmasıyla kullanabileceğiniz bir Windows PowerShell Betiği oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="e9d39-104">When you create a web application in Visual Studio, you can generate a Windows PowerShell script that you can use later tooautomate hello publishing of your website tooAzure as a Web App in Azure App Service or a virtual machine.</span></span> <span data-ttu-id="e9d39-105">Düzenle ve gereksinimlerinizi hello Visual Studio Düzenleyicisi toosuit hello Windows PowerShell betik genişletin veya hello betik varolan derleme, test ve yayımlama betikleri ile tümleştirin.</span><span class="sxs-lookup"><span data-stu-id="e9d39-105">You can edit and extend hello Windows PowerShell script in hello Visual Studio editor toosuit your requirements, or integrate hello script with existing build, test, and publishing scripts.</span></span>

<span data-ttu-id="e9d39-106">Bu komut dosyalarını kullanarak, siteniz geçici kullanım için özelleştirilmiş sürümleri (geliştirme ve test ortamları olarak da bilinir) sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e9d39-106">Using these scripts, you can provision customized versions (also known as dev and test environments) of your site for temporary use.</span></span> <span data-ttu-id="e9d39-107">Örneğin, olabilir Web sitenizi belirli bir sürümü hazırlık yuvasındaki Web sitesi toorun üzerinde hello veya bir Azure sanal makinesi üzerinde bir test paketine ayarlayın, bir hatayı yeniden, önerilen bir değişikliğin hata düzeltmesi, deneme test veya bir tanıtım veya sunumu için özel bir ortamı ayarlama.</span><span class="sxs-lookup"><span data-stu-id="e9d39-107">For example, you might set up a particular version of your website on an Azure virtual machine or on hello staging slot on a website toorun a test suite, reproduce a bug, test a bug fix, trial a proposed change, or set up a custom environment for a demo or presentation.</span></span> <span data-ttu-id="e9d39-108">Projenizi yayımlayan bir komut dosyası oluşturduktan sonra aynı ortamları hello betik gerektiği gibi yeniden çalıştırarak yeniden veya hello betiği, kendi web uygulama toocreate yapı ile test etmek için özel bir ortam çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e9d39-108">After you've created a script that publishes your project, you can recreate identical environments by re-running hello script as needed, or run hello script with your own build of your web application toocreate a custom environment for testing.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="e9d39-109">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="e9d39-109">What you need</span></span>
* <span data-ttu-id="e9d39-110">Azure SDK 2.3 veya üzeri.</span><span class="sxs-lookup"><span data-stu-id="e9d39-110">Azure SDK 2.3 or later.</span></span> <span data-ttu-id="e9d39-111">Bkz: [Visual Studio indirmeleri](http://go.microsoft.com/fwlink/?LinkID=624384) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="e9d39-111">See [Visual Studio Downloads](http://go.microsoft.com/fwlink/?LinkID=624384) for more information.</span></span>

<span data-ttu-id="e9d39-112">Web projeleri için hello Azure SDK'sı toogenerate hello betikleri gerekmez.</span><span class="sxs-lookup"><span data-stu-id="e9d39-112">You do not need hello Azure SDK toogenerate hello scripts for web projects.</span></span> <span data-ttu-id="e9d39-113">Bu özellik web projeleri, olmayan bulut Hizmetleri web rolleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e9d39-113">This feature is for web projects, not web roles in cloud services.</span></span>

* <span data-ttu-id="e9d39-114">Azure PowerShell 0.7.4 veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="e9d39-114">Azure PowerShell 0.7.4 or later.</span></span> <span data-ttu-id="e9d39-115">Bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="e9d39-115">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span>
* <span data-ttu-id="e9d39-116">[Windows PowerShell 3.0](http://go.microsoft.com/?linkid=9811175) veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="e9d39-116">[Windows PowerShell 3.0](http://go.microsoft.com/?linkid=9811175) or later.</span></span>

## <a name="additional-tools"></a><span data-ttu-id="e9d39-117">Ek araçlar</span><span class="sxs-lookup"><span data-stu-id="e9d39-117">Additional tools</span></span>
<span data-ttu-id="e9d39-118">Ek araçlar ve kaynaklar Azure geliştirme için Visual Studio de PowerShell ile çalışmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e9d39-118">Additional tools and resources for working with PowerShell in Visual Studio for Azure development are available.</span></span> <span data-ttu-id="e9d39-119">Bkz: [Visual Studio için PowerShell Araçları](http://go.microsoft.com/fwlink/?LinkId=404012).</span><span class="sxs-lookup"><span data-stu-id="e9d39-119">See [PowerShell Tools for Visual Studio](http://go.microsoft.com/fwlink/?LinkId=404012).</span></span>

## <a name="generating-hello-publish-scripts"></a><span data-ttu-id="e9d39-120">Komut dosyaları yayımlama Hello oluşturma</span><span class="sxs-lookup"><span data-stu-id="e9d39-120">Generating hello publish scripts</span></span>
<span data-ttu-id="e9d39-121">Merhaba oluşturabileceğiniz izleyerek yeni bir proje oluşturduğunuzda, Web sitenizi barındıran bir sanal makine için komut dosyaları yayımlama [bu yönergeleri](virtual-machines/windows/classic/web-app-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e9d39-121">You can generate hello publish scripts for a virtual machine that hosts your website when you create a new project by following [these instructions](virtual-machines/windows/classic/web-app-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="e9d39-122">Ayrıca [oluşturmak betikler web uygulamaları için Azure App Service'te yayımlama](app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="e9d39-122">You can also [generate publish scripts for web apps in Azure App Service](app-service-web/app-service-web-get-started-dotnet.md).</span></span>

## <a name="scripts-that-visual-studio-generates"></a><span data-ttu-id="e9d39-123">Visual Studio'nun oluşturduğu komut dosyaları</span><span class="sxs-lookup"><span data-stu-id="e9d39-123">Scripts that Visual Studio generates</span></span>
<span data-ttu-id="e9d39-124">Visual Studio'nun oluşturduğu adlı bir çözüm düzeyi klasör **PublishScripts** sanal makineniz veya Web sitesi ve hello kullanabileceğiniz işlevleri içeren bir modül için bir yayımlama komut dosyası iki Windows PowerShell dosyaları içerir komut dosyaları.</span><span class="sxs-lookup"><span data-stu-id="e9d39-124">Visual Studio generates a solution-level folder called **PublishScripts** that contains two Windows PowerShell files, a publish script for your virtual machine or website, and a module that contains functions that you can use in hello scripts.</span></span> <span data-ttu-id="e9d39-125">Visual Studio, ayrıca, dağıttığınız hello proje hello ayrıntılarını belirtir hello JSON biçiminde bir dosya oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e9d39-125">Visual Studio also generates a file in hello JSON format that specifies hello details of hello project you are deploying.</span></span>

### <a name="windows-powershell-publish-script"></a><span data-ttu-id="e9d39-126">Windows PowerShell komut dosyası yayımlama</span><span class="sxs-lookup"><span data-stu-id="e9d39-126">Windows PowerShell publish script</span></span>
<span data-ttu-id="e9d39-127">komut dosyası yayımlama Hello belirli içeren tooa Web sitesi ya da sanal makineyi dağıtma adımları yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="e9d39-127">hello publish script contains specific publish steps for deploying tooa website or virtual machine.</span></span> <span data-ttu-id="e9d39-128">Visual Studio için Windows PowerShell geliştirme renklendirme sözdizimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="e9d39-128">Visual Studio provides syntax coloring for Windows PowerShell development.</span></span> <span data-ttu-id="e9d39-129">Merhaba işlevler kullanılabilir ve değişen gereksinimlerinizi hello betik toosuit hello işlevlerde serbestçe düzenleyebilirsiniz için Yardım.</span><span class="sxs-lookup"><span data-stu-id="e9d39-129">Help for hello functions is available, and you can freely edit hello functions in hello script toosuit your changing requirements.</span></span>

### <a name="windows-powershell-module"></a><span data-ttu-id="e9d39-130">Windows PowerShell Modülü</span><span class="sxs-lookup"><span data-stu-id="e9d39-130">Windows PowerShell module</span></span>
<span data-ttu-id="e9d39-131">Merhaba Visual Studio'nun oluşturduğu modülü hello işlevleri içeren Windows PowerShell komut dosyası kullanan yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="e9d39-131">hello Windows PowerShell module that Visual Studio generates contains functions that hello publish script uses.</span></span> <span data-ttu-id="e9d39-132">Bunlar Azure PowerShell işlevleri ve değiştiren hedeflenen toobe değildir.</span><span class="sxs-lookup"><span data-stu-id="e9d39-132">These are Azure PowerShell functions and are not intended toobe modified.</span></span> <span data-ttu-id="e9d39-133">Bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="e9d39-133">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span>

### <a name="json-configuration-file"></a><span data-ttu-id="e9d39-134">JSON yapılandırma dosyası</span><span class="sxs-lookup"><span data-stu-id="e9d39-134">JSON configuration file</span></span>
<span data-ttu-id="e9d39-135">Merhaba JSON dosyası hello oluşturulan **yapılandırmaları** klasörü ve tam olarak hangi kaynaklara toodeploy tooAzure belirtir yapılandırma verilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="e9d39-135">hello JSON file is created in hello **Configurations** folder and contains configuration data that specifies exactly which resources toodeploy tooAzure.</span></span> <span data-ttu-id="e9d39-136">Merhaba Visual Studio'nun oluşturduğu hello dosya proje-adı-WAWS-bir sanal makine oluşturduysanız, bir Web sitesi ya da proje adı-VM-dev.json oluşturduysanız dev.json adıdır.</span><span class="sxs-lookup"><span data-stu-id="e9d39-136">hello name of hello file that Visual Studio generates is project-name-WAWS-dev.json if you created a website, or project name-VM-dev.json if you created a virtual machine.</span></span> <span data-ttu-id="e9d39-137">Bir Web sitesi oluşturduğunuzda oluşturan bir JSON yapılandırma dosyası bir örneği burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e9d39-137">Here's an example of a JSON configuration file that's generated when you create a website.</span></span> <span data-ttu-id="e9d39-138">Merhaba değerleri çoğu kendinden açıklamalıdır.</span><span class="sxs-lookup"><span data-stu-id="e9d39-138">Most of hello values are self-explanatory.</span></span> <span data-ttu-id="e9d39-139">projenizin adına eşleşmeyebilir şekilde hello Web sitesi adı Azure tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e9d39-139">hello website name is generated by Azure, so it might not match your project name.</span></span>

```json
{
    "environmentSettings": {
        "webSite": {
            "name": "WebApplication26632",
            "location": "West US"
        },
        "databases": [{
            "connectionStringName": "DefaultConnection",
            "databaseName": "WebApplication26632_db",
            "serverName": "YourDatabaseServerName",
            "user": "sqluser2",
            "password": "",
            "edition": "",
            "size": "",
            "collation": "",
            "location": "West US"
        }]
    }
}
```
<span data-ttu-id="e9d39-140">Bir sanal makine oluşturduğunuzda, hello JSON yapılandırma dosyası benzer toohello aşağıdaki görünür.</span><span class="sxs-lookup"><span data-stu-id="e9d39-140">When you create a virtual machine, hello JSON configuration file looks similar toohello following.</span></span> <span data-ttu-id="e9d39-141">Bir bulut hizmeti hello sanal makine için bir kapsayıcı olarak oluşturulduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="e9d39-141">Note that a cloud service is created as a container for hello virtual machine.</span></span> <span data-ttu-id="e9d39-142">Hello sanal makine için yerel makine, Uzak Masaüstü ve Windows PowerShell toohello Web sitesi yayımlama imkan tanıyan Web dağıtımı, uç nokta yanı sıra hello normal uç noktaları için HTTP ve HTTPS üzerinden web access içerir.</span><span class="sxs-lookup"><span data-stu-id="e9d39-142">hello virtual machine contains hello usual endpoints for web access through HTTP and HTTPS, as well as endpoints for Web Deploy, which lets you publish toohello website from your local machine, Remote Desktop, and Windows PowerShell.</span></span>

```json
{
    "environmentSettings": {
        "cloudService": {
            "name": "myusernamevm1",
            "affinityGroup": "",
            "location": "West US",
            "virtualNetwork": "",
            "subnet": "",
            "availabilitySet": "",
            "virtualMachine": {
                "name": "myusernamevm1",
                "vhdImage": "a699494373c04fc0bc8f2bb1389d6106__Win2K8R2SP1-Datacenter-201403.01-en.us-127GB.vhd",
                "size": "Small",
                "user": "vmuser1",
                "password": "",
                "enableWebDeployExtension": true,
                "endpoints": [{
                        "name": "Http",
                        "protocol": "TCP",
                        "publicPort": "80",
                        "privatePort": "80"
                    },
                    {
                        "name": "Https",
                        "protocol": "TCP",
                        "publicPort": "443",
                        "privatePort": "443"
                    },
                    {
                        "name": "WebDeploy",
                        "protocol": "TCP",
                        "publicPort": "8172",
                        "privatePort": "8172"
                    },
                    {
                        "name": "Remote Desktop",
                        "protocol": "TCP",
                        "publicPort": "3389",
                        "privatePort": "3389"
                    },
                    {
                        "name": "Powershell",
                        "protocol": "TCP",
                        "publicPort": "5986",
                        "privatePort": "5986"
                    }
                ]
            }
        },
        "databases": [{
            "connectionStringName": "",
            "databaseName": "",
            "serverName": "",
            "user": "",
            "password": ""
        }],
        "webDeployParameters": {
            "iisWebApplicationName": "Default Web Site"
        }
    }
}
```

<span data-ttu-id="e9d39-143">Merhaba çalıştırdığınızda neler hello JSON yapılandırma toochange düzenleyebilirsiniz betikleri yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="e9d39-143">You can edit hello JSON configuration toochange what happens when you run hello publish scripts.</span></span> <span data-ttu-id="e9d39-144">Merhaba `cloudService` ve `virtualMachine` bölümleri gereklidir, ancak hello silebilirsiniz `databases` ihtiyaç duymuyorsanız bölüm.</span><span class="sxs-lookup"><span data-stu-id="e9d39-144">hello `cloudService` and `virtualMachine` sections are required, but you can delete hello `databases` section if you don't need it.</span></span> <span data-ttu-id="e9d39-145">Visual Studio oluşturan hello varsayılan yapılandırma dosyasında boş hello özellikleri isteğe bağlıdır; Merhaba varsayılan yapılandırma dosyasında değerleri olan gereklidir.</span><span class="sxs-lookup"><span data-stu-id="e9d39-145">hello properties that are empty in hello default configuration file that Visual Studio generates are optional; those that have values in hello default configuration file are required.</span></span>

<span data-ttu-id="e9d39-146">Azure'da tek üretim site yerine birden çok dağıtım ortamı (yuvaları da bilinir) sahip bir Web sitesi varsa, hello Web hello JSON yapılandırma dosyasında hello adı hello yuva adı dahil edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e9d39-146">If you have a website that has multiple deployment environments (known as slots) instead of a single production site in Azure, you can include hello slot name in hello name of hello website in hello JSON configuration file.</span></span> <span data-ttu-id="e9d39-147">Adlı bir Web sitesi varsa, örneğin, **Sitem** ve onu adlı yuvasını **test** hello URI Sitem test.cloudapp.net, ancak hello doğru adı toouse hello yapılandırma dosyasında mysite(test) sonra .</span><span class="sxs-lookup"><span data-stu-id="e9d39-147">For example, if you have a website that's named **mysite** and a slot for it named **test** then hello URI is mysite-test.cloudapp.net, but hello correct name toouse in hello configuration file is mysite(test).</span></span> <span data-ttu-id="e9d39-148">Merhaba Web sitesi ve yuvaları aboneliğinizde zaten varsa yalnızca bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e9d39-148">You can only do this if hello website and slots already exist in your subscription.</span></span> <span data-ttu-id="e9d39-149">Yoksa, hello yuvası belirtmeden hello komut dosyası çalıştırarak hello Web sitesi oluşturun, sonra oluşturmak hello hello yuvasına [Klasik Azure portalı](http://go.microsoft.com/fwlink/?LinkID=213885), ve bundan sonra hello betik hello değiştirilmiş Web sitesi adı ile çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e9d39-149">If they don't exist, create hello website by running hello script without specifying hello slot, then create hello slot in hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), and thereafter run hello script with hello modified website name.</span></span> <span data-ttu-id="e9d39-150">Web uygulamaları için dağıtım yuvası hakkında daha fazla bilgi için bkz: [hazırlık Azure App Service'deki web uygulamaları için ortamları ayarlama](app-service-web/web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="e9d39-150">For more information about deployment slots for web apps, see [Set up staging environments for web apps in Azure App Service](app-service-web/web-sites-staged-publishing.md).</span></span>

## <a name="how-toorun-hello-publish-scripts"></a><span data-ttu-id="e9d39-151">Nasıl toorun hello yayımlama betikleri</span><span class="sxs-lookup"><span data-stu-id="e9d39-151">How toorun hello publish scripts</span></span>
<span data-ttu-id="e9d39-152">Önce bir Windows PowerShell Betiği çalıştırılmadı, hello yürütme İlkesi tooenable betikleri toorun ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e9d39-152">If you have never run a Windows PowerShell script before, you must first set hello execution policy tooenable scripts toorun.</span></span> <span data-ttu-id="e9d39-153">Güvenlik Açığı toomalware veya komut dosyaları yürütme içeren virüslere iseniz Windows PowerShell komut dosyası çalıştırarak bir güvenlik özelliği tooprevent kullanıcıların budur.</span><span class="sxs-lookup"><span data-stu-id="e9d39-153">This is a security feature tooprevent users from running Windows PowerShell scripts if they're vulnerable toomalware or viruses that involve executing scripts.</span></span>

### <a name="run-hello-script"></a><span data-ttu-id="e9d39-154">Merhaba komut dosyasını çalıştır</span><span class="sxs-lookup"><span data-stu-id="e9d39-154">Run hello script</span></span>
1. <span data-ttu-id="e9d39-155">Projeniz için Hello Web dağıtım paketi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e9d39-155">Create hello Web Deploy package for your project.</span></span> <span data-ttu-id="e9d39-156">Bir Web dağıtımı toocopy tooyour Web sitesi ya da sanal makineyi istediğiniz dosyaları içeren sıkıştırılmış bir arşiv (.zip dosyası) paketidir.</span><span class="sxs-lookup"><span data-stu-id="e9d39-156">A Web Deploy package is a compressed archive (.zip file) that contain files that you want toocopy tooyour website or virtual machine.</span></span> <span data-ttu-id="e9d39-157">Visual Studio'da Web dağıtımı paketleri için herhangi bir web uygulaması oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e9d39-157">You can create Web Deploy packages in Visual Studio for any web application.</span></span>

![Web oluşturma paketini dağıtma](./media/vs-azure-tools-publishing-using-powershell-scripts/IC767885.png)

<span data-ttu-id="e9d39-159">Daha fazla bilgi için bkz: [nasıl yapılır: Visual Studio'da bir Web dağıtım paketi oluşturma](https://msdn.microsoft.com/library/dd465323.aspx).</span><span class="sxs-lookup"><span data-stu-id="e9d39-159">For more information, see [How to: Create a Web Deployment Package in Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span></span> <span data-ttu-id="e9d39-160">Merhaba, Web dağıtımı paketi oluşturulmasını hello bölümde açıklandığı gibi otomatikleştirebilirsiniz **özelleştirme ve hello genişletme yayımlama betikleri** bu konuda daha sonra.</span><span class="sxs-lookup"><span data-stu-id="e9d39-160">You can also automate hello creation of your Web Deploy package, as described in hello section **Customizing and extending hello publish scripts** later in this topic.</span></span>

1. <span data-ttu-id="e9d39-161">İçinde **Çözüm Gezgini**hello betik hello bağlam menüsünü açın ve ardından **PowerShell ISE ile açmak**.</span><span class="sxs-lookup"><span data-stu-id="e9d39-161">In **Solution Explorer**, open hello context menu for hello script, and then choose **Open with PowerShell ISE**.</span></span>
2. <span data-ttu-id="e9d39-162">Bu hello bu bilgisayarda Windows PowerShell komut dosyalarını çalıştırmak ilk kez kullanıyorsanız, komutu aşağıdaki türü hello ve yönetici ayrıcalıkları ile bir komut istemi penceresi açın:</span><span class="sxs-lookup"><span data-stu-id="e9d39-162">If this is hello first time you've run Windows PowerShell scripts on this computer, open a command prompt window with Administrator privileges and type hello following command:</span></span>

    ```powershell
    Set-ExecutionPolicy RemoteSigned
    ```

3. <span data-ttu-id="e9d39-163">İçinde tooAzure komutu aşağıdaki hello kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="e9d39-163">Sign in tooAzure by using hello following command.</span></span>

    ```powershell
    Add-AzureAccount
    ```

    <span data-ttu-id="e9d39-164">İstendiğinde, kullanıcı adı ve parola sağlayın.</span><span class="sxs-lookup"><span data-stu-id="e9d39-164">When prompted, supply your username and password.</span></span>

    <span data-ttu-id="e9d39-165">Merhaba betik Otomasyon gerçekleştirirken Azure kimlik bilgileri sağlama bu yöntem çalışmaz unutmayın.</span><span class="sxs-lookup"><span data-stu-id="e9d39-165">Note that when you automate hello script, this method of providing Azure credentials won't work.</span></span> <span data-ttu-id="e9d39-166">Bunun yerine, hello .publishsettings dosyasını tooprovide kimlik bilgileri kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e9d39-166">Instead, you should use hello .publishsettings file tooprovide credentials.</span></span> <span data-ttu-id="e9d39-167">Merhaba komutu, yalnızca bir kez kullanın **Get-AzurePublishSettingsFile** toodownload hello dosya Azure'dan ve bundan sonra kullanın **Import-AzurePublishSettingsFile** tooimport hello dosya.</span><span class="sxs-lookup"><span data-stu-id="e9d39-167">One time only, you use hello command **Get-AzurePublishSettingsFile** toodownload hello file from Azure, and thereafter use **Import-AzurePublishSettingsFile** tooimport hello file.</span></span> <span data-ttu-id="e9d39-168">Ayrıntılı yönergeler için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e9d39-168">For detailed instructions, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

4. <span data-ttu-id="e9d39-169">(İsteğe bağlı) Toocreate Azure istiyorsanız hello sanal makine, veritabanı ve web uygulamanızı yayımlamayı olmadan Web sitesi gibi kaynakları hello kullan **Yayımla WebApplication.ps1** hello komutunu **-yapılandırma** değişkenini toohello JSON yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="e9d39-169">(Optional) If you want toocreate Azure resources such as hello virtual machine, database, and website without publishing your web application, use hello **Publish-WebApplication.ps1** command with hello **-Configuration** argument set toohello JSON configuration file.</span></span> <span data-ttu-id="e9d39-170">Bu komut satırı hello JSON yapılandırma dosyası toodetermine hangi kaynaklara toocreate kullanır.</span><span class="sxs-lookup"><span data-stu-id="e9d39-170">This command line uses hello JSON configuration file toodetermine which resources toocreate.</span></span> <span data-ttu-id="e9d39-171">Diğer komut satırı bağımsız değişkenleri hello varsayılan ayarları kullandığından, hello kaynakları oluşturur, ancak web uygulamanızı yayımlamak değil.</span><span class="sxs-lookup"><span data-stu-id="e9d39-171">Because it uses hello default settings for other command-line arguments, it creates hello resources, but doesn't publish your web application.</span></span> <span data-ttu-id="e9d39-172">Merhaba – ayrıntılı seçeneği, neler hakkında daha fazla bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="e9d39-172">hello –Verbose option gives you more information about what's happening.</span></span>

    ```powershell
    Publish-WebApplication.ps1 -Verbose –Configuration C:\Path\WebProject-WAWS-dev.json
    ```

5. <span data-ttu-id="e9d39-173">Kullanım hello **Yayımla WebApplication.ps1** komut örnekleri tooinvoke hello betik aşağıdaki hello birinde gösterildiği gibi ve web uygulamanızı yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="e9d39-173">Use hello **Publish-WebApplication.ps1** command as shown in one of hello following examples tooinvoke hello script and publish your web application.</span></span> <span data-ttu-id="e9d39-174">Toooverride hello varsayılan ayarları herhangi bir hello için hello abonelik adı gibi diğer bağımsız değişkenler gerekiyorsa paket adı, sanal makine kimlik bilgileri veya veritabanı sunucusu kimlik bilgileri yayımlama, bu parametreleri belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e9d39-174">If you need toooverride hello default settings for any of hello other arguments, such as hello subscription name, publish package name, virtual machine credentials, or database server credentials, you can specify those parameters.</span></span> <span data-ttu-id="e9d39-175">Kullanım hello **– ayrıntılı** hello ilerleme durumu hakkında daha fazla bilgi işlem yayımlama hello toosee seçeneği.</span><span class="sxs-lookup"><span data-stu-id="e9d39-175">Use hello **–Verbose** option toosee more information about hello progress of hello publishing process.</span></span>

    ```powershell
    Publish-WebApplication.ps1 –Configuration C:\Path\WebProject-WAWS-dev-json `
    –SubscriptionName Contoso `
    -WebDeployPackage C:\Documents\Azure\ADWebApp.zip `
    -DatabaseServerPassword @{Name="dbServerName";Password="adminPassword"} `
    -Verbose
    ```

    <span data-ttu-id="e9d39-176">Bir sanal makine oluşturuyorsanız, hello komutu hello aşağıdaki gibi görünür.</span><span class="sxs-lookup"><span data-stu-id="e9d39-176">If you're creating a virtual machine, hello command looks like hello following.</span></span> <span data-ttu-id="e9d39-177">Bu örnek ayrıca nasıl toospecify hello birden çok veritabanı için kimlik bilgilerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="e9d39-177">This example also shows how toospecify hello credentials for multiple databases.</span></span> <span data-ttu-id="e9d39-178">Merhaba bu komut dosyaları oluşturmak için sanal makinelerde, hello SSL sertifikası bir güvenilen kök yetkilisi değil.</span><span class="sxs-lookup"><span data-stu-id="e9d39-178">For hello virtual machines that these scripts create, hello SSL certificate is not from a trusted root authority.</span></span> <span data-ttu-id="e9d39-179">Bu nedenle, toouse hello gerekir **– AllowUntrusted** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="e9d39-179">Therefore, you need toouse hello **–AllowUntrusted** option.</span></span>

    ```powershell
    Publish-WebApplication.ps1 `
    -Configuration C:\Path\ADVM-VM-test.json `
    -SubscriptionName Contoso `
    -WebDeployPackage C:\Path\ADVM.zip `
    -AllowUntrusted `
    -VMPassword @{name = "vmUserName"; password = "YourPasswordHere"} `
    -DatabaseServerPassword @{Name="server1";Password="adminPassword1"}, @{Name="server2";Password="adminPassword2"} `
    -Verbose
    ```

    <span data-ttu-id="e9d39-180">Merhaba betik veritabanları oluşturabilirsiniz, ancak veritabanı sunucuları oluşturmaz.</span><span class="sxs-lookup"><span data-stu-id="e9d39-180">hello script can create databases, but it doesn't create database servers.</span></span> <span data-ttu-id="e9d39-181">Bir veritabanı sunucusu toocreate istiyorsanız hello kullanabilirsiniz **yeni AzureSqlDatabaseServer** hello Azure modülü işlevinde.</span><span class="sxs-lookup"><span data-stu-id="e9d39-181">If you want toocreate a database server, you can use hello **New-AzureSqlDatabaseServer** function in hello Azure module.</span></span>

## <a name="customizing-and-extending-hello-publish-scripts"></a><span data-ttu-id="e9d39-182">Özelleştirme ve hello genişletme betikleri yayımlama</span><span class="sxs-lookup"><span data-stu-id="e9d39-182">Customizing and extending hello publish scripts</span></span>
<span data-ttu-id="e9d39-183">Merhaba özelleştirebilirsiniz komut dosyası ve JSON yapılandırma dosyası yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="e9d39-183">You can customize hello publish script and JSON configuration file.</span></span> <span data-ttu-id="e9d39-184">Merhaba hello Windows PowerShell modülü işlevlerde **AzureWebAppPublishModule.psm1** değiştiren hedeflenen toobe değildir.</span><span class="sxs-lookup"><span data-stu-id="e9d39-184">hello functions in hello Windows PowerShell module **AzureWebAppPublishModule.psm1** are not intended toobe modified.</span></span> <span data-ttu-id="e9d39-185">Yalnızca toospecify farklı bir veritabanı veya bazı hello hello sanal makinenin özelliklerini değiştirmek istiyorsanız, hello JSON yapılandırma dosyasını düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="e9d39-185">If you just want toospecify a different database or change some of hello properties of hello virtual machine, edit hello JSON configuration file.</span></span> <span data-ttu-id="e9d39-186">Derleme ve dağıtım projenizi sınamayı hello betik tooautomate tooextend hello işlevselliğini istiyorsanız işlevi saplamalar uygulayabilirsiniz **Yayımla WebApplication.ps1**.</span><span class="sxs-lookup"><span data-stu-id="e9d39-186">If you want tooextend hello functionality of hello script tooautomate building and testing your project, you can implement function stubs in **Publish-WebApplication.ps1**.</span></span>

<span data-ttu-id="e9d39-187">tooautomate, projenizi derleme ekleyin MSBuild çok çağıran kodu`New-WebDeployPackage` Bu kod örneğinde gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="e9d39-187">tooautomate building your project, add code that calls MSBuild too`New-WebDeployPackage` as shown in this code example.</span></span> <span data-ttu-id="e9d39-188">Hello yolu toohello MSBuild komut yüklediğiniz Visual Studio hello sürümüne bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="e9d39-188">hello path toohello MSBuild command is different depending on hello version of Visual Studio you have installed.</span></span> <span data-ttu-id="e9d39-189">tooget hello doğru yolu, hello işlevi kullanabilirsiniz **Get-MSBuildCmd**, bu örnekte gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="e9d39-189">tooget hello correct path, you can use hello function **Get-MSBuildCmd**, as shown in this example.</span></span>

### <a name="tooautomate-building-your-project"></a><span data-ttu-id="e9d39-190">projenizi derleme tooautomate</span><span class="sxs-lookup"><span data-stu-id="e9d39-190">tooautomate building your project</span></span>
1. <span data-ttu-id="e9d39-191">Merhaba eklemek `$ProjectFile` hello genel param bölümünde parametresi.</span><span class="sxs-lookup"><span data-stu-id="e9d39-191">Add hello `$ProjectFile` parameter in hello global param section.</span></span>

    ```powershell
    [Parameter(Mandatory = $false)]
    [ValidateScript({Test-Path $_ -PathType Leaf})]
    [String]
    $ProjectFile,
    ```

2. <span data-ttu-id="e9d39-192">Copy Hello işlevi `Get-MSBuildCmd` komut dosyanızı içine.</span><span class="sxs-lookup"><span data-stu-id="e9d39-192">Copy hello function `Get-MSBuildCmd` into your script file.</span></span>

    ```powershell
    function Get-MSBuildCmd
    {
            process
    {

                $path =  Get-ChildItem "HKLM:\SOFTWARE\Microsoft\MSBuild\ToolsVersions\" |
                                    Sort-Object {[double]$_.PSChildName} -Descending |
                                    Select-Object -First 1 |
                                    Get-ItemProperty -Name MSBuildToolsPath |
                                    Select -ExpandProperty MSBuildToolsPath

                $path = (Join-Path -Path $path -ChildPath 'msbuild.exe')

            return Get-Item $path
        }
    }
    ```

3. <span data-ttu-id="e9d39-193">Değiştir `New-WebDeployPackage` aşağıdaki kod ve satır hello oluştururken hello yer tutucuları değiştirmek hello ile `$msbuildCmd`.</span><span class="sxs-lookup"><span data-stu-id="e9d39-193">Replace `New-WebDeployPackage` with hello following code and replace hello placeholders in hello line constructing `$msbuildCmd`.</span></span> <span data-ttu-id="e9d39-194">Visual Studio 2015 için kodudur.</span><span class="sxs-lookup"><span data-stu-id="e9d39-194">This code is for Visual Studio 2015.</span></span> <span data-ttu-id="e9d39-195">Visual Studio 2013 kullanıyorsanız, hello değiştirme **VisualStudioVersion** özelliği aşağıdaki çok`12.0`.</span><span class="sxs-lookup"><span data-stu-id="e9d39-195">If you're using Visual Studio 2013, change hello **VisualStudioVersion** property below too`12.0`.</span></span>

    ```powershell
    function New-WebDeployPackage
    {
        #Write a function toobuild and package your web application
    ```

    <span data-ttu-id="e9d39-196">toobuild, web uygulaması, MsBuild.exe kullanın.</span><span class="sxs-lookup"><span data-stu-id="e9d39-196">toobuild your web application, use MsBuild.exe.</span></span> <span data-ttu-id="e9d39-197">MSBuild komut satırı başvurusu, Yardım için bkz: [http://go.microsoft.com/fwlink/?LinkId=391339](http://go.microsoft.com/fwlink/?LinkId=391339)</span><span class="sxs-lookup"><span data-stu-id="e9d39-197">For help, see MSBuild Command-Line Reference at: [http://go.microsoft.com/fwlink/?LinkId=391339](http://go.microsoft.com/fwlink/?LinkId=391339)</span></span>

    ```powershell
    Write-VerboseWithTime 'Build-WebDeployPackage: Start'

    $msbuildCmd = '"{0}" "{1}" /T:Rebuild;Package /P:VisualStudioVersion=14.0 /p:OutputPath="{2}\MSBuildOutputPath" /flp:logfile=msbuild.log,v=d' -f (Get-MSBuildCmd), $ProjectFile, $scriptDirectory

    Write-VerboseWithTime ('Build-WebDeployPackage: ' + $msbuildCmd)
    ```

### <a name="start-execution-of-hello-build-command"></a><span data-ttu-id="e9d39-198">Merhaba yapı komutu yürütme Başlat</span><span class="sxs-lookup"><span data-stu-id="e9d39-198">Start execution of hello build command</span></span>

```powershell
$job = Start-Process cmd.exe -ArgumentList('/C "' + $msbuildCmd + '"') -WindowStyle Normal -Wait -PassThru

if ($job.ExitCode -ne 0) {
    throw('MsBuild exited with an error. ExitCode:' + $job.ExitCode)
}

#Obtain hello project name
$projectName = (Get-Item $ProjectFile).BaseName

#Construct hello path tooweb deploy zip package
$DeployPackageDir =  '.\MSBuildOutputPath\_PublishedWebsites\{0}_Package\{0}.zip' -f $projectName

#Get hello full path for hello web deploy zip package. This is required for MSDeploy toowork
$WebDeployPackage = Resolve-Path –LiteralPath $DeployPackageDir

Write-VerboseWithTime 'Build-WebDeployPackage: End'

return $WebDeployPackage
}
```

1. <span data-ttu-id="e9d39-199">Merhaba çağrısı `New-WebDeployPackage` bu satırı önce işlevin: `$Config = Read-ConfigFile $Configuration` web uygulamaları için veya `$Config = Read-ConfigFile $Configuration -HasWebDeployPackage:([Bool]$WebDeployPackage)` sanal makineler için.</span><span class="sxs-lookup"><span data-stu-id="e9d39-199">Call hello `New-WebDeployPackage` function before this line: `$Config = Read-ConfigFile $Configuration` for web apps or `$Config = Read-ConfigFile $Configuration -HasWebDeployPackage:([Bool]$WebDeployPackage)` for virtual machines.</span></span>

    ```powershell
    if($ProjectFile)
    {
    $WebDeployPackage = New-WebDeployPackage
    }
    ```

2. <span data-ttu-id="e9d39-200">Özelleştirilmiş hello betik geçirme hello kullanarak komut satırından çağırma `$Project` olduğu gibi hello aşağıdaki örnek komut satırı bağımsız değişkeni.</span><span class="sxs-lookup"><span data-stu-id="e9d39-200">Invoke hello customized script from command line using passing hello `$Project` argument, as in hello following example command line.</span></span>

    ```powershell
    .\Publish-WebApplicationVM.ps1 -Configuration .\Configurations\WebApplication5-VM-dev.json `
    -ProjectFile ..\WebApplication5\WebApplication5.csproj `
    -VMPassword @{Name="VMUser";Password="Test.123"} `
    -AllowUntrusted `
    -Verbose
    ```

    <span data-ttu-id="e9d39-201">tooautomate uygulamanızın veya test ekleme kodu çok`Test-WebApplication`.</span><span class="sxs-lookup"><span data-stu-id="e9d39-201">tooautomate testing of your application, add code too`Test-WebApplication`.</span></span> <span data-ttu-id="e9d39-202">Merhaba satırlarında emin toouncomment olması **Yayımla WebApplication.ps1** burada bu işlevler adı verilir.</span><span class="sxs-lookup"><span data-stu-id="e9d39-202">Be sure toouncomment hello lines in **Publish-WebApplication.ps1** where these functions are called.</span></span> <span data-ttu-id="e9d39-203">Uygulaması sağlamazsanız, projenizi Visual Studio ile el ile oluşturabilir ve sonra çalışma hello yayımlama betik toopublish tooAzure.</span><span class="sxs-lookup"><span data-stu-id="e9d39-203">If you don't provide an implementation, you can manually build your project with Visual Studio, and then run hello publish script toopublish tooAzure.</span></span>

## <a name="publishing-function-summary"></a><span data-ttu-id="e9d39-204">Özet yayımlama işlevi</span><span class="sxs-lookup"><span data-stu-id="e9d39-204">Publishing function summary</span></span>
<span data-ttu-id="e9d39-205">Merhaba Windows PowerShell komut isteminde kullanabileceğiniz işlevleri tooget yardımını hello komutunu kullanın `Get-Help function-name`.</span><span class="sxs-lookup"><span data-stu-id="e9d39-205">tooget help for functions you can use at hello Windows PowerShell command prompt, use hello command `Get-Help function-name`.</span></span> <span data-ttu-id="e9d39-206">Merhaba Yardımı parametre Yardım ve örnekler içerir.</span><span class="sxs-lookup"><span data-stu-id="e9d39-206">hello help includes parameter help and examples.</span></span> <span data-ttu-id="e9d39-207">aynı Yardım metni, ayrıca hello betik kaynak dosyalarında hello **AzureWebAppPublishModule.psm1** ve **Yayımla WebApplication.ps1**.</span><span class="sxs-lookup"><span data-stu-id="e9d39-207">hello same help text is also in hello script source files, **AzureWebAppPublishModule.psm1** and **Publish-WebApplication.ps1**.</span></span> <span data-ttu-id="e9d39-208">Visual Studio dilinizde Hello komut dosyası ve Yardım yerelleştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e9d39-208">hello script and help are localized in your Visual Studio language.</span></span>

<span data-ttu-id="e9d39-209">**AzureWebAppPublishModule**</span><span class="sxs-lookup"><span data-stu-id="e9d39-209">**AzureWebAppPublishModule**</span></span>

| <span data-ttu-id="e9d39-210">İşlev adı</span><span class="sxs-lookup"><span data-stu-id="e9d39-210">Function name</span></span> | <span data-ttu-id="e9d39-211">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e9d39-211">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e9d39-212">Ekleme AzureSQLDatabase</span><span class="sxs-lookup"><span data-stu-id="e9d39-212">Add-AzureSQLDatabase</span></span> |<span data-ttu-id="e9d39-213">Yeni bir Azure SQL veritabanı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e9d39-213">Creates a new Azure SQL database.</span></span> |
| <span data-ttu-id="e9d39-214">Ekleme AzureSQLDatabases</span><span class="sxs-lookup"><span data-stu-id="e9d39-214">Add-AzureSQLDatabases</span></span> |<span data-ttu-id="e9d39-215">Visual Studio'nun oluşturduğu hello JSON yapılandırma dosyası hello değerlerinden Azure SQL veritabanı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e9d39-215">Creates Azure SQL databases from hello values in hello JSON configuration file that Visual Studio generates.</span></span> |
| <span data-ttu-id="e9d39-216">Add-AzureVM</span><span class="sxs-lookup"><span data-stu-id="e9d39-216">Add-AzureVM</span></span> |<span data-ttu-id="e9d39-217">Bir Azure sanal makine oluşturur ve VM hello hello URL'sini dağıtılan döndürür.</span><span class="sxs-lookup"><span data-stu-id="e9d39-217">Creates a Azure virtual machine and returns hello URL of hello deployed VM.</span></span> <span data-ttu-id="e9d39-218">Merhaba işlevi hello önkoşulları ve ardından çağrıları hello ayarlar **New-AzureVM** (Azure Modülü) toocreate yeni bir sanal makine işlev.</span><span class="sxs-lookup"><span data-stu-id="e9d39-218">hello function sets up hello prerequisites and then calls hello **New-AzureVM** function (Azure module) toocreate a new virtual machine.</span></span> |
| <span data-ttu-id="e9d39-219">Ekleme AzureVMEndpoints</span><span class="sxs-lookup"><span data-stu-id="e9d39-219">Add-AzureVMEndpoints</span></span> |<span data-ttu-id="e9d39-220">Yeni bir giriş uç noktaları tooa sanal makine ekler ve hello yeni uç nokta ile Merhaba sanal makine döndürür.</span><span class="sxs-lookup"><span data-stu-id="e9d39-220">Adds new input endpoints tooa virtual machine and returns hello virtual machine with hello new endpoint.</span></span> |
| <span data-ttu-id="e9d39-221">Ekleme AzureVMStorage</span><span class="sxs-lookup"><span data-stu-id="e9d39-221">Add-AzureVMStorage</span></span> |<span data-ttu-id="e9d39-222">Yeni bir Azure depolama hesabı hello geçerli abonelikte oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e9d39-222">Creates a new Azure storage account in hello current subscription.</span></span> <span data-ttu-id="e9d39-223">Merhaba hello hesap adını "benzersiz bir alfasayısal dize tarafından izlenen devtest" ile başlar.</span><span class="sxs-lookup"><span data-stu-id="e9d39-223">hello name of hello account begins with "devtest" followed by a unique alphanumeric string.</span></span> <span data-ttu-id="e9d39-224">Merhaba işlevi hello hello yeni depolama hesabı adını döndürür.</span><span class="sxs-lookup"><span data-stu-id="e9d39-224">hello function returns hello name of hello new storage account.</span></span> <span data-ttu-id="e9d39-225">Bir konumu veya hello yeni depolama hesabı için bir benzeşim grubu belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e9d39-225">You must specify either a location or an affinity group for hello new storage account.</span></span> |
| <span data-ttu-id="e9d39-226">Ekleme AzureWebsite</span><span class="sxs-lookup"><span data-stu-id="e9d39-226">Add-AzureWebsite</span></span> |<span data-ttu-id="e9d39-227">Merhaba belirtilen adı ve konumu ile bir Web sitesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e9d39-227">Creates a website with hello specified name and location.</span></span> <span data-ttu-id="e9d39-228">Bu işlev hello çağırır **yeni AzureWebsite** hello Azure modülü işlevinde.</span><span class="sxs-lookup"><span data-stu-id="e9d39-228">This function calls hello **New-AzureWebsite** function in hello Azure module.</span></span> <span data-ttu-id="e9d39-229">Merhaba abonelik hello belirtilen ada sahip bir Web sitesi içermiyorsa, bu işlev hello Web sitesi oluşturur ve bir Web sitesi nesnesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="e9d39-229">If hello subscription doesn't already include a website with hello specified name, this function creates hello website and returns a website object.</span></span> <span data-ttu-id="e9d39-230">Aksi takdirde, döndürür `$null`.</span><span class="sxs-lookup"><span data-stu-id="e9d39-230">Otherwise, it returns `$null`.</span></span> |
| <span data-ttu-id="e9d39-231">Yedekleme abonelik</span><span class="sxs-lookup"><span data-stu-id="e9d39-231">Backup-Subscription</span></span> |<span data-ttu-id="e9d39-232">Kaydeder hello hello Azure geçerli abonelikte `$Script:originalSubscription` betik kapsamında değişken. Bu işlev hello geçerli Azure aboneliği kaydeder (ile alınan `Get-AzureSubscription -Current`) ve depolama hesabı ve bu komut dosyası tarafından değiştirilen hello abonelik (Merhaba değişkeninde depolanan `$UserSpecifiedSubscription`) ve betik kapsamında, depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="e9d39-232">Saves hello current Azure subscription in hello `$Script:originalSubscription` variable in script scope.This function saves hello current Azure subscription (as obtained by `Get-AzureSubscription -Current`) and its storage account, and hello subscription that is changed by this script (stored in hello variable `$UserSpecifiedSubscription`) and its storage account, in script scope.</span></span> <span data-ttu-id="e9d39-233">Merhaba değerleri kaydederek bir işlev gibi kullanabileceğiniz `Restore-Subscription`, hello geçerli durumu değişirse toorestore hello özgün geçerli abonelik ve depolama hesabı toocurrent durumu.</span><span class="sxs-lookup"><span data-stu-id="e9d39-233">By saving hello values, you can use a function, such as `Restore-Subscription`, toorestore hello original current subscription and storage account toocurrent status if hello current status has changed.</span></span> |
| <span data-ttu-id="e9d39-234">Bul-AzureVM</span><span class="sxs-lookup"><span data-stu-id="e9d39-234">Find-AzureVM</span></span> |<span data-ttu-id="e9d39-235">Alır hello Azure sanal makine belirtildi.</span><span class="sxs-lookup"><span data-stu-id="e9d39-235">Gets hello specified Azure virtual machine.</span></span> |
| <span data-ttu-id="e9d39-236">Biçim DevTestMessageWithTime</span><span class="sxs-lookup"><span data-stu-id="e9d39-236">Format-DevTestMessageWithTime</span></span> |<span data-ttu-id="e9d39-237">Başlangıç tarihi ve saati tooa ileti başına.</span><span class="sxs-lookup"><span data-stu-id="e9d39-237">Prepends hello date and time tooa message.</span></span> <span data-ttu-id="e9d39-238">Bu işlev toohello hata ve ayrıntı akışları yazılan iletilerin için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="e9d39-238">This function is designed for messages written toohello Error and Verbose streams.</span></span> |
| <span data-ttu-id="e9d39-239">Get-AzureSQLDatabaseConnectionString</span><span class="sxs-lookup"><span data-stu-id="e9d39-239">Get-AzureSQLDatabaseConnectionString</span></span> |<span data-ttu-id="e9d39-240">Bir bağlantı dizesi tooconnect tooan Azure SQL veritabanı derler.</span><span class="sxs-lookup"><span data-stu-id="e9d39-240">Assembles a connection string tooconnect tooan Azure SQL database.</span></span> |
| <span data-ttu-id="e9d39-241">Get-AzureVMStorage</span><span class="sxs-lookup"><span data-stu-id="e9d39-241">Get-AzureVMStorage</span></span> |<span data-ttu-id="e9d39-242">Döndürür hello hello ilk depolama hesabıyla hello adı deseni adını "devtest*" (büyük küçük harfe duyarlı) hello belirtilen konumda veya benzeşim grubunda. Merhaba, "devtest*" Merhaba konumu ya da benzeşim grubu depolama hesabı eşleşmiyor, hello işlevi yoksayar.</span><span class="sxs-lookup"><span data-stu-id="e9d39-242">Returns hello name of hello first storage account with hello name pattern "devtest*" (case insensitive) in hello specified location or affinity group. If hello "devtest*" storage account doesn't match hello location or affinity group, hello function ignores it.</span></span> <span data-ttu-id="e9d39-243">Bir konumu veya bir benzeşim grubu belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e9d39-243">You must specify either a location or an affinity group.</span></span> |
| <span data-ttu-id="e9d39-244">Get-MSDeployCmd</span><span class="sxs-lookup"><span data-stu-id="e9d39-244">Get-MSDeployCmd</span></span> |<span data-ttu-id="e9d39-245">Bir komut toorun hello MsDeploy.exe aracını döndürür.</span><span class="sxs-lookup"><span data-stu-id="e9d39-245">Returns a command toorun hello MsDeploy.exe tool.</span></span> |
| <span data-ttu-id="e9d39-246">AzureVMEnvironment yeni</span><span class="sxs-lookup"><span data-stu-id="e9d39-246">New-AzureVMEnvironment</span></span> |<span data-ttu-id="e9d39-247">Bulur veya hello JSON yapılandırma dosyası hello değerlerle eşleştiğini hello Abonelikteki bir sanal makine oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e9d39-247">Finds or creates a virtual machine in hello subscription that matches hello values in hello JSON configuration file.</span></span> |
| <span data-ttu-id="e9d39-248">Yayımlama WebPackage</span><span class="sxs-lookup"><span data-stu-id="e9d39-248">Publish-WebPackage</span></span> |<span data-ttu-id="e9d39-249">MsDeploy.exe kullanır ve bir web paketi yayımlayın. Zip dosyası toodeploy kaynakları tooa Web sitesi.</span><span class="sxs-lookup"><span data-stu-id="e9d39-249">Uses MsDeploy.exe and a web publish package .Zip file toodeploy resources tooa website.</span></span> <span data-ttu-id="e9d39-250">Bu işlev, herhangi bir çıktı üretmez.</span><span class="sxs-lookup"><span data-stu-id="e9d39-250">This function doesn't generate any output.</span></span> <span data-ttu-id="e9d39-251">Merhaba çağrısı tooMSDeploy.exe başarısız olursa, hello işlevi bir özel durum oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e9d39-251">If hello call tooMSDeploy.exe fails, hello function throws an exception.</span></span> <span data-ttu-id="e9d39-252">daha ayrıntılı çıktı, kullanım hello tooget **-Verbose** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="e9d39-252">tooget more detailed output, use hello **-Verbose** option.</span></span> |
| <span data-ttu-id="e9d39-253">Yayımlama WebPackageToVM</span><span class="sxs-lookup"><span data-stu-id="e9d39-253">Publish-WebPackageToVM</span></span> |<span data-ttu-id="e9d39-254">Merhaba parametre değerlerini doğrular ve hello çağırır **Yayımla WebPackage** işlevi.</span><span class="sxs-lookup"><span data-stu-id="e9d39-254">Verifies hello parameter values, and then calls hello **Publish-WebPackage** function.</span></span> |
| <span data-ttu-id="e9d39-255">Okuma ConfigFile</span><span class="sxs-lookup"><span data-stu-id="e9d39-255">Read-ConfigFile</span></span> |<span data-ttu-id="e9d39-256">Merhaba JSON yapılandırma dosyası doğrular ve seçili değerlerinin bir karma tablosu döndürür.</span><span class="sxs-lookup"><span data-stu-id="e9d39-256">Validates hello JSON configuration file and returns a hash table of selected values.</span></span> |
| <span data-ttu-id="e9d39-257">Geri yükleme-abonelik</span><span class="sxs-lookup"><span data-stu-id="e9d39-257">Restore-Subscription</span></span> |<span data-ttu-id="e9d39-258">Merhaba geçerli abonelik toohello özgün abonelik sıfırlar.</span><span class="sxs-lookup"><span data-stu-id="e9d39-258">Resets hello current subscription toohello original subscription.</span></span> |
| <span data-ttu-id="e9d39-259">Test-AzureModule</span><span class="sxs-lookup"><span data-stu-id="e9d39-259">Test-AzureModule</span></span> |<span data-ttu-id="e9d39-260">Döndürür `$true` yüklü hello Azure Modül sürümü 0.7.4 ise veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="e9d39-260">Returns `$true` if hello installed Azure module version is 0.7.4 or later.</span></span> <span data-ttu-id="e9d39-261">Döndürür `$false` hello Modülü yüklü değil veya önceki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="e9d39-261">Returns `$false` if hello module isn't installed or is an earlier version.</span></span> <span data-ttu-id="e9d39-262">Bu işlev hiç parametre yok.</span><span class="sxs-lookup"><span data-stu-id="e9d39-262">This function has no parameters.</span></span> |
| <span data-ttu-id="e9d39-263">Test-AzureModuleVersion</span><span class="sxs-lookup"><span data-stu-id="e9d39-263">Test-AzureModuleVersion</span></span> |<span data-ttu-id="e9d39-264">Döndürür `$true` hello Azure modülü hello sürümü 0.7.4 ise veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="e9d39-264">Returns `$true` if hello version of hello Azure module is 0.7.4 or later.</span></span> <span data-ttu-id="e9d39-265">Döndürür `$false` hello Modülü yüklü değil veya önceki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="e9d39-265">Returns `$false` if hello module isn't installed or is an earlier version.</span></span> <span data-ttu-id="e9d39-266">Bu işlev hiç parametre yok.</span><span class="sxs-lookup"><span data-stu-id="e9d39-266">This function has no parameters.</span></span> |
| <span data-ttu-id="e9d39-267">Test-HttpsUrl</span><span class="sxs-lookup"><span data-stu-id="e9d39-267">Test-HttpsUrl</span></span> |<span data-ttu-id="e9d39-268">Merhaba giriş URL tooa System.Uri nesnesi dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="e9d39-268">Converts hello input URL tooa System.Uri object.</span></span> <span data-ttu-id="e9d39-269">Döndürür `$True` hello URL mutlak ve kendi şeması https ise.</span><span class="sxs-lookup"><span data-stu-id="e9d39-269">Returns `$True` if hello URL is absolute and its scheme is https.</span></span> <span data-ttu-id="e9d39-270">Döndürür `$false` hello URL göreli kendi şeması HTTPS değil veya hello giriş dizesi dönüştürülmüş tooa URL olamaz.</span><span class="sxs-lookup"><span data-stu-id="e9d39-270">Returns `$false` if hello URL is relative, its scheme isn't HTTPS, or hello input string can't be converted tooa URL.</span></span> |
| <span data-ttu-id="e9d39-271">Test-üyesi</span><span class="sxs-lookup"><span data-stu-id="e9d39-271">Test-Member</span></span> |<span data-ttu-id="e9d39-272">Döndürür `$true` bir özellik veya yöntem hello nesnesinin bir üyesi ise.</span><span class="sxs-lookup"><span data-stu-id="e9d39-272">Returns `$true` if a property or method is a member of hello object.</span></span> <span data-ttu-id="e9d39-273">Aksi takdirde, döndürür `$false`.</span><span class="sxs-lookup"><span data-stu-id="e9d39-273">Otherwise, returns `$false`.</span></span> |
| <span data-ttu-id="e9d39-274">Yazma ErrorWithTime</span><span class="sxs-lookup"><span data-stu-id="e9d39-274">Write-ErrorWithTime</span></span> |<span data-ttu-id="e9d39-275">Geçerli saat ile Merhaba önekli bir hata iletisi yazar.</span><span class="sxs-lookup"><span data-stu-id="e9d39-275">Writes an error message prefixed with hello current time.</span></span> <span data-ttu-id="e9d39-276">Bu işlev hello çağırır **biçimi DevTestMessageWithTime** hello ileti toohello hata akışı yazmadan önce işlevi tooprepend hello zaman.</span><span class="sxs-lookup"><span data-stu-id="e9d39-276">This function calls hello **Format-DevTestMessageWithTime** function tooprepend hello time before writing hello message toohello Error stream.</span></span> |
| <span data-ttu-id="e9d39-277">Yazma HostWithTime</span><span class="sxs-lookup"><span data-stu-id="e9d39-277">Write-HostWithTime</span></span> |<span data-ttu-id="e9d39-278">Bir ileti toohello ana bilgisayar programı yazar (**Write-Host**) ile Merhaba geçerli saati öneki.</span><span class="sxs-lookup"><span data-stu-id="e9d39-278">Writes a message toohello host program (**Write-Host**) prefixed with hello current time.</span></span> <span data-ttu-id="e9d39-279">Merhaba etkisini toohello ana bilgisayar programı yazma değişir.</span><span class="sxs-lookup"><span data-stu-id="e9d39-279">hello effect of writing toohello host program varies.</span></span> <span data-ttu-id="e9d39-280">Çoğu program barındıran Windows PowerShell Bu iletiler toostandard çıktı yazma.</span><span class="sxs-lookup"><span data-stu-id="e9d39-280">Most programs that host Windows PowerShell write these messages toostandard output.</span></span> |
| <span data-ttu-id="e9d39-281">Yazma VerboseWithTime</span><span class="sxs-lookup"><span data-stu-id="e9d39-281">Write-VerboseWithTime</span></span> |<span data-ttu-id="e9d39-282">Geçerli saat ile Merhaba önekli ayrıntılı bir ileti yazar.</span><span class="sxs-lookup"><span data-stu-id="e9d39-282">Writes a verbose message prefixed with hello current time.</span></span> <span data-ttu-id="e9d39-283">Çağırır çünkü **Write-Verbose**, selamlama iletisine görüntüler yalnızca hello betik ile Merhaba çalıştığında **ayrıntılı** parametresi veya ne zaman hello **VerbosePreference** tercih olduğu çok ayarlamak**devam**.</span><span class="sxs-lookup"><span data-stu-id="e9d39-283">Because it calls **Write-Verbose**, hello message displays only when hello script runs with hello **Verbose** parameter or when hello **VerbosePreference** preference is set too**Continue**.</span></span> |

<span data-ttu-id="e9d39-284">**Yayımlama WebApplication**</span><span class="sxs-lookup"><span data-stu-id="e9d39-284">**Publish-WebApplication**</span></span>

| <span data-ttu-id="e9d39-285">İşlev adı</span><span class="sxs-lookup"><span data-stu-id="e9d39-285">Function name</span></span> | <span data-ttu-id="e9d39-286">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e9d39-286">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e9d39-287">AzureWebApplicationEnvironment yeni</span><span class="sxs-lookup"><span data-stu-id="e9d39-287">New-AzureWebApplicationEnvironment</span></span> |<span data-ttu-id="e9d39-288">Bir Web sitesi veya sanal makine gibi Azure kaynakları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e9d39-288">Creates Azure resources, such as a website or virtual machine.</span></span> |
| <span data-ttu-id="e9d39-289">WebDeployPackage yeni</span><span class="sxs-lookup"><span data-stu-id="e9d39-289">New-WebDeployPackage</span></span> |<span data-ttu-id="e9d39-290">Bu işlev uygulanmadı.</span><span class="sxs-lookup"><span data-stu-id="e9d39-290">This function isn't implemented.</span></span> <span data-ttu-id="e9d39-291">Projenizi bu işlevi toobuild komutları ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e9d39-291">You can add commands in this function toobuild your project.</span></span> |
| <span data-ttu-id="e9d39-292">Yayımlama AzureWebApplication</span><span class="sxs-lookup"><span data-stu-id="e9d39-292">Publish-AzureWebApplication</span></span> |<span data-ttu-id="e9d39-293">Bir web uygulaması tooAzure yayımlar.</span><span class="sxs-lookup"><span data-stu-id="e9d39-293">Publishes a web application tooAzure.</span></span> |
| <span data-ttu-id="e9d39-294">Yayımlama WebApplication</span><span class="sxs-lookup"><span data-stu-id="e9d39-294">Publish-WebApplication</span></span> |<span data-ttu-id="e9d39-295">Oluşturur ve Web uygulamaları, sanal makineler, SQL veritabanları ve depolama hesapları için bir Visual Studio web projesini dağıtır.</span><span class="sxs-lookup"><span data-stu-id="e9d39-295">Creates and deploys Web Apps, virtual machines, SQL databases, and storage accounts for a Visual Studio web project.</span></span> |
| <span data-ttu-id="e9d39-296">Test-WebApplication</span><span class="sxs-lookup"><span data-stu-id="e9d39-296">Test-WebApplication</span></span> |<span data-ttu-id="e9d39-297">Bu işlev uygulanmadı.</span><span class="sxs-lookup"><span data-stu-id="e9d39-297">This function isn't implemented.</span></span> <span data-ttu-id="e9d39-298">Uygulamanız bu işlevi tootest komutları ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e9d39-298">You can add commands in this function tootest your application.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e9d39-299">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e9d39-299">Next steps</span></span>
<span data-ttu-id="e9d39-300">PowerShell okuyarak komut dosyası hakkında daha fazla bilgi [ile Windows PowerShell komut dosyası](https://technet.microsoft.com/library/bb978526.aspx) ve diğer Azure PowerShell betikleri hello adresindeki [Komut Merkezi](https://azure.microsoft.com/documentation/scripts/).</span><span class="sxs-lookup"><span data-stu-id="e9d39-300">Learn more about PowerShell scripting by reading [Scripting with Windows PowerShell](https://technet.microsoft.com/library/bb978526.aspx) and see other Azure PowerShell scripts at hello [Script Center](https://azure.microsoft.com/documentation/scripts/).</span></span>
