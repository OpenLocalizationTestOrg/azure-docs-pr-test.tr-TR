---
title: "Geliştirme ve Test ortamları için yayımlamak için Windows PowerShell betikleri kullanma | Microsoft Docs"
description: "Windows PowerShell komut dosyalarını Visual Studio'dan yayımlamak için geliştirme ve test ortamları için nasıl kullanılacağını öğrenin."
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
ms.openlocfilehash: d4c39eb7a8bc97a980061872ba0f32f375e6976f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="using-windows-powershell-scripts-to-publish-to-dev-and-test-environments"></a><span data-ttu-id="ce241-103">Geliştirme ve test ortamlarında yayımlama için Windows PowerShell betiklerini kullanma</span><span class="sxs-lookup"><span data-stu-id="ce241-103">Using Windows PowerShell scripts to publish to dev and test environments</span></span>
<span data-ttu-id="ce241-104">Visual Studio'da bir web uygulaması oluşturduğunuzda, daha sonra Azure Web sitenizi yayımlama bir Web uygulamasını Azure App Service veya bir sanal makine olarak otomatikleştirmek için kullanabileceğiniz bir Windows PowerShell komut dosyası oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ce241-104">When you create a web application in Visual Studio, you can generate a Windows PowerShell script that you can use later to automate the publishing of your website to Azure as a Web App in Azure App Service or a virtual machine.</span></span> <span data-ttu-id="ce241-105">Düzenle ve Windows PowerShell komut dosyasını gereksinimlerinize uyacak şekilde Visual Studio düzenleyicisinde genişletin veya komut dosyasını varolan derleme, test ve komut dosyaları yayımlama ile tümleştirin.</span><span class="sxs-lookup"><span data-stu-id="ce241-105">You can edit and extend the Windows PowerShell script in the Visual Studio editor to suit your requirements, or integrate the script with existing build, test, and publishing scripts.</span></span>

<span data-ttu-id="ce241-106">Bu komut dosyalarını kullanarak, siteniz geçici kullanım için özelleştirilmiş sürümleri (geliştirme ve test ortamları olarak da bilinir) sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ce241-106">Using these scripts, you can provision customized versions (also known as dev and test environments) of your site for temporary use.</span></span> <span data-ttu-id="ce241-107">Örneğin, Web sitenizi bir Azure sanal makine ya da test paketi çalıştırmak, bir hatayı yeniden, önerilen bir değişikliğin hata düzeltmesi, deneme test veya bir tanıtım veya sunumu için özel bir ortam ayarlamak için bir Web sitesinde hazırlama yuvası belirli bir sürümü ayarlayabilir.</span><span class="sxs-lookup"><span data-stu-id="ce241-107">For example, you might set up a particular version of your website on an Azure virtual machine or on the staging slot on a website to run a test suite, reproduce a bug, test a bug fix, trial a proposed change, or set up a custom environment for a demo or presentation.</span></span> <span data-ttu-id="ce241-108">Projenizi yayımlayan bir komut dosyası oluşturduktan sonra aynı ortamları betik gerektiği gibi yeniden çalıştırarak yeniden veya kendi yapı testi için özel bir ortam oluşturmak için web uygulamanızın komut dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ce241-108">After you've created a script that publishes your project, you can recreate identical environments by re-running the script as needed, or run the script with your own build of your web application to create a custom environment for testing.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="ce241-109">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="ce241-109">What you need</span></span>
* <span data-ttu-id="ce241-110">Azure SDK 2.3 veya üzeri.</span><span class="sxs-lookup"><span data-stu-id="ce241-110">Azure SDK 2.3 or later.</span></span> <span data-ttu-id="ce241-111">Bkz: [Visual Studio indirmeleri](http://go.microsoft.com/fwlink/?LinkID=624384) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="ce241-111">See [Visual Studio Downloads](http://go.microsoft.com/fwlink/?LinkID=624384) for more information.</span></span>

<span data-ttu-id="ce241-112">Web projeleri için komut dosyaları oluşturmak için Azure SDK'sını gerekmez.</span><span class="sxs-lookup"><span data-stu-id="ce241-112">You do not need the Azure SDK to generate the scripts for web projects.</span></span> <span data-ttu-id="ce241-113">Bu özellik web projeleri, olmayan bulut Hizmetleri web rolleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ce241-113">This feature is for web projects, not web roles in cloud services.</span></span>

* <span data-ttu-id="ce241-114">Azure PowerShell 0.7.4 veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="ce241-114">Azure PowerShell 0.7.4 or later.</span></span> <span data-ttu-id="ce241-115">Bkz: [Azure PowerShell'i yükleme ve yapılandırma nasıl](/powershell/azure/overview) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="ce241-115">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span>
* <span data-ttu-id="ce241-116">[Windows PowerShell 3.0](http://go.microsoft.com/?linkid=9811175) veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="ce241-116">[Windows PowerShell 3.0](http://go.microsoft.com/?linkid=9811175) or later.</span></span>

## <a name="additional-tools"></a><span data-ttu-id="ce241-117">Ek araçlar</span><span class="sxs-lookup"><span data-stu-id="ce241-117">Additional tools</span></span>
<span data-ttu-id="ce241-118">Ek araçlar ve kaynaklar Azure geliştirme için Visual Studio de PowerShell ile çalışmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ce241-118">Additional tools and resources for working with PowerShell in Visual Studio for Azure development are available.</span></span> <span data-ttu-id="ce241-119">Bkz: [Visual Studio için PowerShell Araçları](http://go.microsoft.com/fwlink/?LinkId=404012).</span><span class="sxs-lookup"><span data-stu-id="ce241-119">See [PowerShell Tools for Visual Studio](http://go.microsoft.com/fwlink/?LinkId=404012).</span></span>

## <a name="generating-the-publish-scripts"></a><span data-ttu-id="ce241-120">Yayımlama betikleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="ce241-120">Generating the publish scripts</span></span>
<span data-ttu-id="ce241-121">Yayımlama betikleri izleyerek yeni bir proje oluşturduğunuzda, Web sitenizi barındıran bir sanal makine için oluşturabileceğiniz [bu yönergeleri](virtual-machines/windows/classic/web-app-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ce241-121">You can generate the publish scripts for a virtual machine that hosts your website when you create a new project by following [these instructions](virtual-machines/windows/classic/web-app-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="ce241-122">Ayrıca [oluşturmak betikler web uygulamaları için Azure App Service'te yayımlama](app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="ce241-122">You can also [generate publish scripts for web apps in Azure App Service](app-service-web/app-service-web-get-started-dotnet.md).</span></span>

## <a name="scripts-that-visual-studio-generates"></a><span data-ttu-id="ce241-123">Visual Studio'nun oluşturduğu komut dosyaları</span><span class="sxs-lookup"><span data-stu-id="ce241-123">Scripts that Visual Studio generates</span></span>
<span data-ttu-id="ce241-124">Visual Studio'nun oluşturduğu adlı bir çözüm düzeyi klasör **PublishScripts** iki Windows PowerShell dosyaları, sanal makinenize veya Web sitesi ve kullanabileceğiniz işlevleri içeren bir modül için bir yayımlama komut dosyasını içerir komut dosyaları.</span><span class="sxs-lookup"><span data-stu-id="ce241-124">Visual Studio generates a solution-level folder called **PublishScripts** that contains two Windows PowerShell files, a publish script for your virtual machine or website, and a module that contains functions that you can use in the scripts.</span></span> <span data-ttu-id="ce241-125">Visual Studio, aynı zamanda, dağıttığınız proje ayrıntılarını belirtir JSON biçiminde bir dosya oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ce241-125">Visual Studio also generates a file in the JSON format that specifies the details of the project you are deploying.</span></span>

### <a name="windows-powershell-publish-script"></a><span data-ttu-id="ce241-126">Windows PowerShell komut dosyası yayımlama</span><span class="sxs-lookup"><span data-stu-id="ce241-126">Windows PowerShell publish script</span></span>
<span data-ttu-id="ce241-127">Yayımla komut dosyası için bir Web sitesi veya sanal makine dağıtımı için belirli Yayımla adımları içerir.</span><span class="sxs-lookup"><span data-stu-id="ce241-127">The publish script contains specific publish steps for deploying to a website or virtual machine.</span></span> <span data-ttu-id="ce241-128">Visual Studio için Windows PowerShell geliştirme renklendirme sözdizimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="ce241-128">Visual Studio provides syntax coloring for Windows PowerShell development.</span></span> <span data-ttu-id="ce241-129">İşlevlerin kullanılabilir ve değişen gereksinimlerinize uyacak şekilde betik işlevlerde serbestçe düzenleyebilirsiniz için Yardım.</span><span class="sxs-lookup"><span data-stu-id="ce241-129">Help for the functions is available, and you can freely edit the functions in the script to suit your changing requirements.</span></span>

### <a name="windows-powershell-module"></a><span data-ttu-id="ce241-130">Windows PowerShell Modülü</span><span class="sxs-lookup"><span data-stu-id="ce241-130">Windows PowerShell module</span></span>
<span data-ttu-id="ce241-131">Visual Studio'nun oluşturduğu Windows PowerShell modülü Yayımla komut dosyası kullanan işlevler içerir.</span><span class="sxs-lookup"><span data-stu-id="ce241-131">The Windows PowerShell module that Visual Studio generates contains functions that the publish script uses.</span></span> <span data-ttu-id="ce241-132">Bunlar Azure PowerShell işlevleri ve değiştirilecek amaçlanmamıştır.</span><span class="sxs-lookup"><span data-stu-id="ce241-132">These are Azure PowerShell functions and are not intended to be modified.</span></span> <span data-ttu-id="ce241-133">Bkz: [Azure PowerShell'i yükleme ve yapılandırma nasıl](/powershell/azure/overview) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="ce241-133">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span>

### <a name="json-configuration-file"></a><span data-ttu-id="ce241-134">JSON yapılandırma dosyası</span><span class="sxs-lookup"><span data-stu-id="ce241-134">JSON configuration file</span></span>
<span data-ttu-id="ce241-135">JSON dosyası oluşturulur **yapılandırmaları** klasör ve Azure'a dağıtmak için tam olarak hangi kaynaklara belirtir yapılandırma verilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="ce241-135">The JSON file is created in the **Configurations** folder and contains configuration data that specifies exactly which resources to deploy to Azure.</span></span> <span data-ttu-id="ce241-136">Proje-adı-WAWS-bir sanal makine oluşturduysanız, bir Web sitesi ya da proje adı-VM-dev.json oluşturduysanız dev.json Visual Studio'nun oluşturduğu dosyasının adıdır.</span><span class="sxs-lookup"><span data-stu-id="ce241-136">The name of the file that Visual Studio generates is project-name-WAWS-dev.json if you created a website, or project name-VM-dev.json if you created a virtual machine.</span></span> <span data-ttu-id="ce241-137">Bir Web sitesi oluşturduğunuzda oluşturan bir JSON yapılandırma dosyası bir örneği burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ce241-137">Here's an example of a JSON configuration file that's generated when you create a website.</span></span> <span data-ttu-id="ce241-138">Değerleri çoğu kendinden açıklamalıdır.</span><span class="sxs-lookup"><span data-stu-id="ce241-138">Most of the values are self-explanatory.</span></span> <span data-ttu-id="ce241-139">Projenizin adına eşleşmeyebilir şekilde Web sitesi adı Azure tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="ce241-139">The website name is generated by Azure, so it might not match your project name.</span></span>

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
<span data-ttu-id="ce241-140">Bir sanal makine oluşturduğunuzda, JSON yapılandırma dosyası aşağıdakine benzer.</span><span class="sxs-lookup"><span data-stu-id="ce241-140">When you create a virtual machine, the JSON configuration file looks similar to the following.</span></span> <span data-ttu-id="ce241-141">Bir bulut hizmeti, sanal makine için bir kapsayıcı olarak oluşturulduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ce241-141">Note that a cloud service is created as a container for the virtual machine.</span></span> <span data-ttu-id="ce241-142">Sanal makine için yerel makine, Uzak Masaüstü ve Windows PowerShell Web sitesine yayımlamak imkan tanıyan Web dağıtımı, uç nokta yanı sıra her zamanki uç noktaları için HTTP ve HTTPS üzerinden web access içerir.</span><span class="sxs-lookup"><span data-stu-id="ce241-142">The virtual machine contains the usual endpoints for web access through HTTP and HTTPS, as well as endpoints for Web Deploy, which lets you publish to the website from your local machine, Remote Desktop, and Windows PowerShell.</span></span>

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

<span data-ttu-id="ce241-143">Yayımlama betikleri çalıştırdığınızda neler değiştirmek için JSON yapılandırma düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ce241-143">You can edit the JSON configuration to change what happens when you run the publish scripts.</span></span> <span data-ttu-id="ce241-144">`cloudService` Ve `virtualMachine` bölümleri gereklidir, ancak silebilirsiniz `databases` ihtiyaç duymuyorsanız bölüm.</span><span class="sxs-lookup"><span data-stu-id="ce241-144">The `cloudService` and `virtualMachine` sections are required, but you can delete the `databases` section if you don't need it.</span></span> <span data-ttu-id="ce241-145">Visual Studio'nun oluşturduğu varsayılan yapılandırma dosyası boş özellikleri isteğe bağlıdır; varsayılan yapılandırma dosyasında değerleri olan gereklidir.</span><span class="sxs-lookup"><span data-stu-id="ce241-145">The properties that are empty in the default configuration file that Visual Studio generates are optional; those that have values in the default configuration file are required.</span></span>

<span data-ttu-id="ce241-146">Azure'da tek üretim site yerine birden çok dağıtım ortamı (yuvaları da bilinir) sahip bir Web sitesi varsa, Web sitesi adına yuva adı JSON yapılandırma dosyasında içerebilir.</span><span class="sxs-lookup"><span data-stu-id="ce241-146">If you have a website that has multiple deployment environments (known as slots) instead of a single production site in Azure, you can include the slot name in the name of the website in the JSON configuration file.</span></span> <span data-ttu-id="ce241-147">Adlı bir Web sitesi varsa, örneğin, **Sitem** ve onu adlı yuvasını **test** URI Sitem test.cloudapp.net olmakla birlikte yapılandırma dosyasında kullanılacak doğru adı mysite(test) sonra.</span><span class="sxs-lookup"><span data-stu-id="ce241-147">For example, if you have a website that's named **mysite** and a slot for it named **test** then the URI is mysite-test.cloudapp.net, but the correct name to use in the configuration file is mysite(test).</span></span> <span data-ttu-id="ce241-148">Bu, Web sitesi yalnızca gerçekleştirebilir ve yuvaları aboneliğinizde zaten mevcut.</span><span class="sxs-lookup"><span data-stu-id="ce241-148">You can only do this if the website and slots already exist in your subscription.</span></span> <span data-ttu-id="ce241-149">Yoksa, Web sitesi oluşturma yuva belirtmeden betiği çalıştırarak, ardından yuvada oluşturun [Klasik Azure portalı](http://go.microsoft.com/fwlink/?LinkID=213885), ve bundan sonra komut dosyasının değiştirilmiş Web sitesi adı ile çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ce241-149">If they don't exist, create the website by running the script without specifying the slot, then create the slot in the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), and thereafter run the script with the modified website name.</span></span> <span data-ttu-id="ce241-150">Web uygulamaları için dağıtım yuvası hakkında daha fazla bilgi için bkz: [hazırlık Azure App Service'deki web uygulamaları için ortamları ayarlama](app-service-web/web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="ce241-150">For more information about deployment slots for web apps, see [Set up staging environments for web apps in Azure App Service](app-service-web/web-sites-staged-publishing.md).</span></span>

## <a name="how-to-run-the-publish-scripts"></a><span data-ttu-id="ce241-151">Yayımlama betikleri çalıştırma</span><span class="sxs-lookup"><span data-stu-id="ce241-151">How to run the publish scripts</span></span>
<span data-ttu-id="ce241-152">Önce bir Windows PowerShell Betiği çalıştırılmadı, önce çalıştırılacak betikleri etkinleştirmek için yürütme ilkesi ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ce241-152">If you have never run a Windows PowerShell script before, you must first set the execution policy to enable scripts to run.</span></span> <span data-ttu-id="ce241-153">Bu kullanıcıların kötü amaçlı yazılım veya komut dosyaları yürütme içeren virüslere karşı savunmasız, Windows PowerShell komut dosyalarını çalıştırmasını engellemek için bir güvenlik özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="ce241-153">This is a security feature to prevent users from running Windows PowerShell scripts if they're vulnerable to malware or viruses that involve executing scripts.</span></span>

### <a name="run-the-script"></a><span data-ttu-id="ce241-154">Komut dosyasını çalıştır</span><span class="sxs-lookup"><span data-stu-id="ce241-154">Run the script</span></span>
1. <span data-ttu-id="ce241-155">Projeniz için Web dağıtımı paketi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ce241-155">Create the Web Deploy package for your project.</span></span> <span data-ttu-id="ce241-156">Bir Web Dağıtımı Web sitesi ya da sanal makineyi kopyalamak istediğiniz dosyaları içeren sıkıştırılmış bir arşiv (.zip dosyası) paketidir.</span><span class="sxs-lookup"><span data-stu-id="ce241-156">A Web Deploy package is a compressed archive (.zip file) that contain files that you want to copy to your website or virtual machine.</span></span> <span data-ttu-id="ce241-157">Visual Studio'da Web dağıtımı paketleri için herhangi bir web uygulaması oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ce241-157">You can create Web Deploy packages in Visual Studio for any web application.</span></span>

![Web oluşturma paketini dağıtma](./media/vs-azure-tools-publishing-using-powershell-scripts/IC767885.png)

<span data-ttu-id="ce241-159">Daha fazla bilgi için bkz: [nasıl yapılır: Visual Studio'da bir Web dağıtım paketi oluşturma](https://msdn.microsoft.com/library/dd465323.aspx).</span><span class="sxs-lookup"><span data-stu-id="ce241-159">For more information, see [How to: Create a Web Deployment Package in Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span></span> <span data-ttu-id="ce241-160">Web dağıtımı paketi oluşturulmasını bölümde açıklandığı gibi otomatikleştirebilirsiniz **özelleştirme ve yayımlama betikleri genişletme** bu konuda daha sonra.</span><span class="sxs-lookup"><span data-stu-id="ce241-160">You can also automate the creation of your Web Deploy package, as described in the section **Customizing and extending the publish scripts** later in this topic.</span></span>

1. <span data-ttu-id="ce241-161">İçinde **Çözüm Gezgini**betik bağlam menüsünü açın ve ardından **PowerShell ISE ile açmak**.</span><span class="sxs-lookup"><span data-stu-id="ce241-161">In **Solution Explorer**, open the context menu for the script, and then choose **Open with PowerShell ISE**.</span></span>
2. <span data-ttu-id="ce241-162">Bu bilgisayarda Windows PowerShell komut dosyalarını çalıştırmak ilk kez kullanıyorsanız, yönetici ayrıcalıklarıyla bir komut istemi penceresi açın ve aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="ce241-162">If this is the first time you've run Windows PowerShell scripts on this computer, open a command prompt window with Administrator privileges and type the following command:</span></span>

    ```powershell
    Set-ExecutionPolicy RemoteSigned
    ```

3. <span data-ttu-id="ce241-163">Aşağıdaki komutu kullanarak Azure'da oturum açın.</span><span class="sxs-lookup"><span data-stu-id="ce241-163">Sign in to Azure by using the following command.</span></span>

    ```powershell
    Add-AzureAccount
    ```

    <span data-ttu-id="ce241-164">İstendiğinde, kullanıcı adı ve parola sağlayın.</span><span class="sxs-lookup"><span data-stu-id="ce241-164">When prompted, supply your username and password.</span></span>

    <span data-ttu-id="ce241-165">Komut dosyası Otomasyon gerçekleştirirken Azure kimlik bilgileri sağlama bu yöntem çalışmaz unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ce241-165">Note that when you automate the script, this method of providing Azure credentials won't work.</span></span> <span data-ttu-id="ce241-166">Bunun yerine, kimlik bilgilerini sağlamak için .publishsettings dosyasını kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ce241-166">Instead, you should use the .publishsettings file to provide credentials.</span></span> <span data-ttu-id="ce241-167">Komut, size yalnızca bir kez kullanın **Get-AzurePublishSettingsFile** Azure'dan dosyasını indirin ve bundan sonra kullanmak için **Import-AzurePublishSettingsFile** dosya içeri aktarılamıyor.</span><span class="sxs-lookup"><span data-stu-id="ce241-167">One time only, you use the command **Get-AzurePublishSettingsFile** to download the file from Azure, and thereafter use **Import-AzurePublishSettingsFile** to import the file.</span></span> <span data-ttu-id="ce241-168">Ayrıntılı yönergeler için bkz: [Azure PowerShell'i yükleme ve yapılandırma nasıl](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ce241-168">For detailed instructions, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

4. <span data-ttu-id="ce241-169">(İsteğe bağlı) Sanal makine gibi Azure kaynakları oluşturmak istiyorsanız, veritabanı ve web uygulamanızı yayımlamayı olmadan Web sitesi kullanmak **Yayımla WebApplication.ps1** komutunu **-yapılandırma**bağımsız değişkenini JSON yapılandırma dosyasına ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="ce241-169">(Optional) If you want to create Azure resources such as the virtual machine, database, and website without publishing your web application, use the **Publish-WebApplication.ps1** command with the **-Configuration** argument set to the JSON configuration file.</span></span> <span data-ttu-id="ce241-170">Bu komut satırı JSON yapılandırma dosyası oluşturmak için hangi kaynak belirlemek için kullanır.</span><span class="sxs-lookup"><span data-stu-id="ce241-170">This command line uses the JSON configuration file to determine which resources to create.</span></span> <span data-ttu-id="ce241-171">Diğer komut satırı bağımsız değişkenleri için varsayılan ayarları kullandığından, kaynakları oluşturur, ancak web uygulamanızı yayımlamak değil.</span><span class="sxs-lookup"><span data-stu-id="ce241-171">Because it uses the default settings for other command-line arguments, it creates the resources, but doesn't publish your web application.</span></span> <span data-ttu-id="ce241-172">Verbose seçeneği neler hakkında daha fazla bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="ce241-172">The –Verbose option gives you more information about what's happening.</span></span>

    ```powershell
    Publish-WebApplication.ps1 -Verbose –Configuration C:\Path\WebProject-WAWS-dev.json
    ```

5. <span data-ttu-id="ce241-173">Kullanım **Yayımla WebApplication.ps1** komutu bir komut dosyası çağırma ve web uygulamanızı yayımlamak için aşağıdaki örnekleri gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="ce241-173">Use the **Publish-WebApplication.ps1** command as shown in one of the following examples to invoke the script and publish your web application.</span></span> <span data-ttu-id="ce241-174">Abonelik adı gibi diğer bağımsız değişkenlerden biri için varsayılan ayarları geçersiz kılacak gerekiyorsa paket adı, sanal makine kimlik bilgileri veya veritabanı sunucusu kimlik bilgileri yayımlama, bu parametreleri belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ce241-174">If you need to override the default settings for any of the other arguments, such as the subscription name, publish package name, virtual machine credentials, or database server credentials, you can specify those parameters.</span></span> <span data-ttu-id="ce241-175">Kullanım **– ayrıntılı** yayımlama işleminin ilerleme durumu hakkında daha fazla bilgi için seçeneği.</span><span class="sxs-lookup"><span data-stu-id="ce241-175">Use the **–Verbose** option to see more information about the progress of the publishing process.</span></span>

    ```powershell
    Publish-WebApplication.ps1 –Configuration C:\Path\WebProject-WAWS-dev-json `
    –SubscriptionName Contoso `
    -WebDeployPackage C:\Documents\Azure\ADWebApp.zip `
    -DatabaseServerPassword @{Name="dbServerName";Password="adminPassword"} `
    -Verbose
    ```

    <span data-ttu-id="ce241-176">Bir sanal makine oluşturuyorsanız, komut aşağıdaki gibi görünür.</span><span class="sxs-lookup"><span data-stu-id="ce241-176">If you're creating a virtual machine, the command looks like the following.</span></span> <span data-ttu-id="ce241-177">Bu örnek ayrıca birden çok veritabanı için kimlik bilgilerini belirleme konusunda gösterir.</span><span class="sxs-lookup"><span data-stu-id="ce241-177">This example also shows how to specify the credentials for multiple databases.</span></span> <span data-ttu-id="ce241-178">Bu komut dosyaları oluşturmak sanal makineler'ne için SSL sertifikası bir güvenilen kök yetkilisi değil.</span><span class="sxs-lookup"><span data-stu-id="ce241-178">For the virtual machines that these scripts create, the SSL certificate is not from a trusted root authority.</span></span> <span data-ttu-id="ce241-179">Bu nedenle, kullanmanıza gerek **– AllowUntrusted** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="ce241-179">Therefore, you need to use the **–AllowUntrusted** option.</span></span>

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

    <span data-ttu-id="ce241-180">Komut dosyası veritabanları oluşturabilirsiniz, ancak veritabanı sunucuları oluşturmaz.</span><span class="sxs-lookup"><span data-stu-id="ce241-180">The script can create databases, but it doesn't create database servers.</span></span> <span data-ttu-id="ce241-181">Bir veritabanı sunucusu oluşturmak istiyorsanız, kullanabileceğiniz **yeni AzureSqlDatabaseServer** Azure modülünde işlevi.</span><span class="sxs-lookup"><span data-stu-id="ce241-181">If you want to create a database server, you can use the **New-AzureSqlDatabaseServer** function in the Azure module.</span></span>

## <a name="customizing-and-extending-the-publish-scripts"></a><span data-ttu-id="ce241-182">Özelleştirme ve yayımlama betikleri genişletme</span><span class="sxs-lookup"><span data-stu-id="ce241-182">Customizing and extending the publish scripts</span></span>
<span data-ttu-id="ce241-183">Yayımla betiği ve JSON yapılandırma dosyası özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ce241-183">You can customize the publish script and JSON configuration file.</span></span> <span data-ttu-id="ce241-184">Windows PowerShell modülünü işlevlerde **AzureWebAppPublishModule.psm1** değiştirilecek amaçlanmamıştır.</span><span class="sxs-lookup"><span data-stu-id="ce241-184">The functions in the Windows PowerShell module **AzureWebAppPublishModule.psm1** are not intended to be modified.</span></span> <span data-ttu-id="ce241-185">Yalnızca farklı bir veritabanı belirtin veya sanal makinenin özelliklerini değiştirmek istiyorsanız, JSON yapılandırma dosyasını düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="ce241-185">If you just want to specify a different database or change some of the properties of the virtual machine, edit the JSON configuration file.</span></span> <span data-ttu-id="ce241-186">Derleme ve dağıtım projenizi sınamayı otomatikleştirmek için komut dosyası işlevselliğini genişletmek istiyorsanız, işlevi saplamalar uygulayabilirsiniz **Yayımla WebApplication.ps1**.</span><span class="sxs-lookup"><span data-stu-id="ce241-186">If you want to extend the functionality of the script to automate building and testing your project, you can implement function stubs in **Publish-WebApplication.ps1**.</span></span>

<span data-ttu-id="ce241-187">Projenizi derleme otomatikleştirmek için MSBuild için çağıran kodu eklemek `New-WebDeployPackage` Bu kod örneğinde gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="ce241-187">To automate building your project, add code that calls MSBuild to `New-WebDeployPackage` as shown in this code example.</span></span> <span data-ttu-id="ce241-188">MSBuild komut yolu yüklediğiniz Visual Studio sürümüne bağlı olarak farklı olur.</span><span class="sxs-lookup"><span data-stu-id="ce241-188">The path to the MSBuild command is different depending on the version of Visual Studio you have installed.</span></span> <span data-ttu-id="ce241-189">Doğru yolu almak için işlevini kullanabilirsiniz **Get-MSBuildCmd**, bu örnekte gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="ce241-189">To get the correct path, you can use the function **Get-MSBuildCmd**, as shown in this example.</span></span>

### <a name="to-automate-building-your-project"></a><span data-ttu-id="ce241-190">Projenizi derleme otomatik hale getirmek için</span><span class="sxs-lookup"><span data-stu-id="ce241-190">To automate building your project</span></span>
1. <span data-ttu-id="ce241-191">Ekleme `$ProjectFile` genel param bölümünde parametresi.</span><span class="sxs-lookup"><span data-stu-id="ce241-191">Add the `$ProjectFile` parameter in the global param section.</span></span>

    ```powershell
    [Parameter(Mandatory = $false)]
    [ValidateScript({Test-Path $_ -PathType Leaf})]
    [String]
    $ProjectFile,
    ```

2. <span data-ttu-id="ce241-192">Copy işlevi `Get-MSBuildCmd` komut dosyanızı içine.</span><span class="sxs-lookup"><span data-stu-id="ce241-192">Copy the function `Get-MSBuildCmd` into your script file.</span></span>

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

3. <span data-ttu-id="ce241-193">Değiştir `New-WebDeployPackage` ile aşağıdaki kod ve satır oluştururken yer tutucuları değiştirmek `$msbuildCmd`.</span><span class="sxs-lookup"><span data-stu-id="ce241-193">Replace `New-WebDeployPackage` with the following code and replace the placeholders in the line constructing `$msbuildCmd`.</span></span> <span data-ttu-id="ce241-194">Visual Studio 2015 için kodudur.</span><span class="sxs-lookup"><span data-stu-id="ce241-194">This code is for Visual Studio 2015.</span></span> <span data-ttu-id="ce241-195">Visual Studio 2013 kullanıyorsanız, değiştirme **VisualStudioVersion** aşağıda özelliğine `12.0`.</span><span class="sxs-lookup"><span data-stu-id="ce241-195">If you're using Visual Studio 2013, change the **VisualStudioVersion** property below to `12.0`.</span></span>

    ```powershell
    function New-WebDeployPackage
    {
        #Write a function to build and package your web application
    ```

    <span data-ttu-id="ce241-196">Web uygulamanızı oluşturmak için MsBuild.exe kullanın.</span><span class="sxs-lookup"><span data-stu-id="ce241-196">To build your web application, use MsBuild.exe.</span></span> <span data-ttu-id="ce241-197">MSBuild komut satırı başvurusu, Yardım için bkz: [http://go.microsoft.com/fwlink/?LinkId=391339](http://go.microsoft.com/fwlink/?LinkId=391339)</span><span class="sxs-lookup"><span data-stu-id="ce241-197">For help, see MSBuild Command-Line Reference at: [http://go.microsoft.com/fwlink/?LinkId=391339](http://go.microsoft.com/fwlink/?LinkId=391339)</span></span>

    ```powershell
    Write-VerboseWithTime 'Build-WebDeployPackage: Start'

    $msbuildCmd = '"{0}" "{1}" /T:Rebuild;Package /P:VisualStudioVersion=14.0 /p:OutputPath="{2}\MSBuildOutputPath" /flp:logfile=msbuild.log,v=d' -f (Get-MSBuildCmd), $ProjectFile, $scriptDirectory

    Write-VerboseWithTime ('Build-WebDeployPackage: ' + $msbuildCmd)
    ```

### <a name="start-execution-of-the-build-command"></a><span data-ttu-id="ce241-198">Yapı komutu yürütme Başlat</span><span class="sxs-lookup"><span data-stu-id="ce241-198">Start execution of the build command</span></span>

```powershell
$job = Start-Process cmd.exe -ArgumentList('/C "' + $msbuildCmd + '"') -WindowStyle Normal -Wait -PassThru

if ($job.ExitCode -ne 0) {
    throw('MsBuild exited with an error. ExitCode:' + $job.ExitCode)
}

#Obtain the project name
$projectName = (Get-Item $ProjectFile).BaseName

#Construct the path to web deploy zip package
$DeployPackageDir =  '.\MSBuildOutputPath\_PublishedWebsites\{0}_Package\{0}.zip' -f $projectName

#Get the full path for the web deploy zip package. This is required for MSDeploy to work
$WebDeployPackage = Resolve-Path –LiteralPath $DeployPackageDir

Write-VerboseWithTime 'Build-WebDeployPackage: End'

return $WebDeployPackage
}
```

1. <span data-ttu-id="ce241-199">Çağrı `New-WebDeployPackage` bu satırı önce işlevin: `$Config = Read-ConfigFile $Configuration` web uygulamaları için veya `$Config = Read-ConfigFile $Configuration -HasWebDeployPackage:([Bool]$WebDeployPackage)` sanal makineler için.</span><span class="sxs-lookup"><span data-stu-id="ce241-199">Call the `New-WebDeployPackage` function before this line: `$Config = Read-ConfigFile $Configuration` for web apps or `$Config = Read-ConfigFile $Configuration -HasWebDeployPackage:([Bool]$WebDeployPackage)` for virtual machines.</span></span>

    ```powershell
    if($ProjectFile)
    {
    $WebDeployPackage = New-WebDeployPackage
    }
    ```

2. <span data-ttu-id="ce241-200">Özelleştirilmiş komut dosyası geçirme kullanarak komut satırından çağırma `$Project` olduğu gibi aşağıdaki örnek komut satırı bağımsız değişkeni.</span><span class="sxs-lookup"><span data-stu-id="ce241-200">Invoke the customized script from command line using passing the `$Project` argument, as in the following example command line.</span></span>

    ```powershell
    .\Publish-WebApplicationVM.ps1 -Configuration .\Configurations\WebApplication5-VM-dev.json `
    -ProjectFile ..\WebApplication5\WebApplication5.csproj `
    -VMPassword @{Name="VMUser";Password="Test.123"} `
    -AllowUntrusted `
    -Verbose
    ```

    <span data-ttu-id="ce241-201">Uygulamanızın veya testleri otomatikleştirmek için kodu ekleyin `Test-WebApplication`.</span><span class="sxs-lookup"><span data-stu-id="ce241-201">To automate testing of your application, add code to `Test-WebApplication`.</span></span> <span data-ttu-id="ce241-202">Satırları açıklamadan çıkarın özen **Yayımla WebApplication.ps1** burada bu işlevler adı verilir.</span><span class="sxs-lookup"><span data-stu-id="ce241-202">Be sure to uncomment the lines in **Publish-WebApplication.ps1** where these functions are called.</span></span> <span data-ttu-id="ce241-203">Uygulaması sağlamazsanız, projenizi Visual Studio ile el ile oluşturun ve Azure'a yayımlamak için Yayımla betiğini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ce241-203">If you don't provide an implementation, you can manually build your project with Visual Studio, and then run the publish script to publish to Azure.</span></span>

## <a name="publishing-function-summary"></a><span data-ttu-id="ce241-204">Özet yayımlama işlevi</span><span class="sxs-lookup"><span data-stu-id="ce241-204">Publishing function summary</span></span>
<span data-ttu-id="ce241-205">Windows PowerShell komut isteminde kullanabileceğiniz işlevleri için Yardım almak için komut kullanmak `Get-Help function-name`.</span><span class="sxs-lookup"><span data-stu-id="ce241-205">To get help for functions you can use at the Windows PowerShell command prompt, use the command `Get-Help function-name`.</span></span> <span data-ttu-id="ce241-206">Yardım parametre Yardım ve örnekler içerir.</span><span class="sxs-lookup"><span data-stu-id="ce241-206">The help includes parameter help and examples.</span></span> <span data-ttu-id="ce241-207">Aynı Yardım metni de betik kaynak dosyaları, **AzureWebAppPublishModule.psm1** ve **Yayımla WebApplication.ps1**.</span><span class="sxs-lookup"><span data-stu-id="ce241-207">The same help text is also in the script source files, **AzureWebAppPublishModule.psm1** and **Publish-WebApplication.ps1**.</span></span> <span data-ttu-id="ce241-208">Komut dosyası ve Yardım Visual Studio dilinizde yerelleştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ce241-208">The script and help are localized in your Visual Studio language.</span></span>

<span data-ttu-id="ce241-209">**AzureWebAppPublishModule**</span><span class="sxs-lookup"><span data-stu-id="ce241-209">**AzureWebAppPublishModule**</span></span>

| <span data-ttu-id="ce241-210">İşlev adı</span><span class="sxs-lookup"><span data-stu-id="ce241-210">Function name</span></span> | <span data-ttu-id="ce241-211">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ce241-211">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ce241-212">Ekleme AzureSQLDatabase</span><span class="sxs-lookup"><span data-stu-id="ce241-212">Add-AzureSQLDatabase</span></span> |<span data-ttu-id="ce241-213">Yeni bir Azure SQL veritabanı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ce241-213">Creates a new Azure SQL database.</span></span> |
| <span data-ttu-id="ce241-214">Ekleme AzureSQLDatabases</span><span class="sxs-lookup"><span data-stu-id="ce241-214">Add-AzureSQLDatabases</span></span> |<span data-ttu-id="ce241-215">Azure SQL veritabanları değerlerin Visual Studio'nun oluşturduğu JSON yapılandırma dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ce241-215">Creates Azure SQL databases from the values in the JSON configuration file that Visual Studio generates.</span></span> |
| <span data-ttu-id="ce241-216">Add-AzureVM</span><span class="sxs-lookup"><span data-stu-id="ce241-216">Add-AzureVM</span></span> |<span data-ttu-id="ce241-217">Bir Azure sanal makine oluşturur ve dağıtılan VM URL'sini döndürür.</span><span class="sxs-lookup"><span data-stu-id="ce241-217">Creates a Azure virtual machine and returns the URL of the deployed VM.</span></span> <span data-ttu-id="ce241-218">İşlev önkoşulların ayarlar ve ardından çağırır **New-AzureVM** yeni bir sanal makine oluşturmak için işlevi (Azure Modülü).</span><span class="sxs-lookup"><span data-stu-id="ce241-218">The function sets up the prerequisites and then calls the **New-AzureVM** function (Azure module) to create a new virtual machine.</span></span> |
| <span data-ttu-id="ce241-219">Ekleme AzureVMEndpoints</span><span class="sxs-lookup"><span data-stu-id="ce241-219">Add-AzureVMEndpoints</span></span> |<span data-ttu-id="ce241-220">Yeni giriş uç noktaları bir sanal makineye ekler ve yeni uç nokta ile sanal makine döndürür.</span><span class="sxs-lookup"><span data-stu-id="ce241-220">Adds new input endpoints to a virtual machine and returns the virtual machine with the new endpoint.</span></span> |
| <span data-ttu-id="ce241-221">Ekleme AzureVMStorage</span><span class="sxs-lookup"><span data-stu-id="ce241-221">Add-AzureVMStorage</span></span> |<span data-ttu-id="ce241-222">Yeni bir Azure depolama hesabı geçerli abonelikte oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ce241-222">Creates a new Azure storage account in the current subscription.</span></span> <span data-ttu-id="ce241-223">Hesap adını "benzersiz bir alfasayısal dize tarafından izlenen devtest" ile başlar.</span><span class="sxs-lookup"><span data-stu-id="ce241-223">The name of the account begins with "devtest" followed by a unique alphanumeric string.</span></span> <span data-ttu-id="ce241-224">İşlevi yeni depolama hesabı adını döndürür.</span><span class="sxs-lookup"><span data-stu-id="ce241-224">The function returns the name of the new storage account.</span></span> <span data-ttu-id="ce241-225">Bir konumu veya yeni depolama hesabı için bir benzeşim grubu belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ce241-225">You must specify either a location or an affinity group for the new storage account.</span></span> |
| <span data-ttu-id="ce241-226">Ekleme AzureWebsite</span><span class="sxs-lookup"><span data-stu-id="ce241-226">Add-AzureWebsite</span></span> |<span data-ttu-id="ce241-227">Bir Web sitesi belirtilen adı ve konumu ile oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ce241-227">Creates a website with the specified name and location.</span></span> <span data-ttu-id="ce241-228">Bu işlev çağrılarını **yeni AzureWebsite** Azure modülünde işlevi.</span><span class="sxs-lookup"><span data-stu-id="ce241-228">This function calls the **New-AzureWebsite** function in the Azure module.</span></span> <span data-ttu-id="ce241-229">Abonelik zaten belirtilen adda bir Web sitesi içermiyorsa, bu işlev Web sitesi oluşturur ve bir Web sitesi nesnesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="ce241-229">If the subscription doesn't already include a website with the specified name, this function creates the website and returns a website object.</span></span> <span data-ttu-id="ce241-230">Aksi takdirde, döndürür `$null`.</span><span class="sxs-lookup"><span data-stu-id="ce241-230">Otherwise, it returns `$null`.</span></span> |
| <span data-ttu-id="ce241-231">Yedekleme abonelik</span><span class="sxs-lookup"><span data-stu-id="ce241-231">Backup-Subscription</span></span> |<span data-ttu-id="ce241-232">Geçerli Azure aboneliğindeki kaydeder `$Script:originalSubscription` betik kapsamında değişken. Bu işlev geçerli Azure aboneliği kaydeder (ile alınan `Get-AzureSubscription -Current`) ve depolama hesabı ve bu komut dosyası tarafından değiştirilen abonelik (değişkeninde depolanan `$UserSpecifiedSubscription`) ve betik kapsamında, depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="ce241-232">Saves the current Azure subscription in the `$Script:originalSubscription` variable in script scope.This function saves the current Azure subscription (as obtained by `Get-AzureSubscription -Current`) and its storage account, and the subscription that is changed by this script (stored in the variable `$UserSpecifiedSubscription`) and its storage account, in script scope.</span></span> <span data-ttu-id="ce241-233">Değerleri kaydederek bir işlev gibi kullanabileceğiniz `Restore-Subscription`, geçerli durum değiştiyse özgün geçerli abonelik ve depolama hesabı geçerli durumuna geri yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="ce241-233">By saving the values, you can use a function, such as `Restore-Subscription`, to restore the original current subscription and storage account to current status if the current status has changed.</span></span> |
| <span data-ttu-id="ce241-234">Bul-AzureVM</span><span class="sxs-lookup"><span data-stu-id="ce241-234">Find-AzureVM</span></span> |<span data-ttu-id="ce241-235">Belirtilen Azure sanal makine alır.</span><span class="sxs-lookup"><span data-stu-id="ce241-235">Gets the specified Azure virtual machine.</span></span> |
| <span data-ttu-id="ce241-236">Biçim DevTestMessageWithTime</span><span class="sxs-lookup"><span data-stu-id="ce241-236">Format-DevTestMessageWithTime</span></span> |<span data-ttu-id="ce241-237">Tarih ve saat için bir ileti başına.</span><span class="sxs-lookup"><span data-stu-id="ce241-237">Prepends the date and time to a message.</span></span> <span data-ttu-id="ce241-238">Bu işlev, hata ve ayrıntı akışlara yazılan iletileri için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="ce241-238">This function is designed for messages written to the Error and Verbose streams.</span></span> |
| <span data-ttu-id="ce241-239">Get-AzureSQLDatabaseConnectionString</span><span class="sxs-lookup"><span data-stu-id="ce241-239">Get-AzureSQLDatabaseConnectionString</span></span> |<span data-ttu-id="ce241-240">Bir Azure SQL veritabanına bağlanmak için bir bağlantı dizesi derler.</span><span class="sxs-lookup"><span data-stu-id="ce241-240">Assembles a connection string to connect to an Azure SQL database.</span></span> |
| <span data-ttu-id="ce241-241">Get-AzureVMStorage</span><span class="sxs-lookup"><span data-stu-id="ce241-241">Get-AzureVMStorage</span></span> |<span data-ttu-id="ce241-242">İlk Depolama hesabı adı deseni ile adını döndürür "devtest*" (büyük küçük harfe duyarlı) belirtilen konum veya benzeşim grubu. Varsa "devtest*" depolama hesabı konumu ya da benzeşim grubu eşleşmiyor, işlevi yok sayar.</span><span class="sxs-lookup"><span data-stu-id="ce241-242">Returns the name of the first storage account with the name pattern "devtest*" (case insensitive) in the specified location or affinity group. If the "devtest*" storage account doesn't match the location or affinity group, the function ignores it.</span></span> <span data-ttu-id="ce241-243">Bir konumu veya bir benzeşim grubu belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ce241-243">You must specify either a location or an affinity group.</span></span> |
| <span data-ttu-id="ce241-244">Get-MSDeployCmd</span><span class="sxs-lookup"><span data-stu-id="ce241-244">Get-MSDeployCmd</span></span> |<span data-ttu-id="ce241-245">MsDeploy.exe aracını çalıştırmak için bir komut döndürür.</span><span class="sxs-lookup"><span data-stu-id="ce241-245">Returns a command to run the MsDeploy.exe tool.</span></span> |
| <span data-ttu-id="ce241-246">AzureVMEnvironment yeni</span><span class="sxs-lookup"><span data-stu-id="ce241-246">New-AzureVMEnvironment</span></span> |<span data-ttu-id="ce241-247">Bulur veya bir sanal makine JSON yapılandırma dosyasındaki değerleri eşleşen abonelik oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ce241-247">Finds or creates a virtual machine in the subscription that matches the values in the JSON configuration file.</span></span> |
| <span data-ttu-id="ce241-248">Yayımlama WebPackage</span><span class="sxs-lookup"><span data-stu-id="ce241-248">Publish-WebPackage</span></span> |<span data-ttu-id="ce241-249">MsDeploy.exe kullanır ve bir web paketi yayımlayın. Kaynakları bir Web sitesine dağıtmak için zip dosyası.</span><span class="sxs-lookup"><span data-stu-id="ce241-249">Uses MsDeploy.exe and a web publish package .Zip file to deploy resources to a website.</span></span> <span data-ttu-id="ce241-250">Bu işlev, herhangi bir çıktı üretmez.</span><span class="sxs-lookup"><span data-stu-id="ce241-250">This function doesn't generate any output.</span></span> <span data-ttu-id="ce241-251">MSDeploy.exe çağrısı başarısız olursa, işlev özel durum oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ce241-251">If the call to MSDeploy.exe fails, the function throws an exception.</span></span> <span data-ttu-id="ce241-252">Daha ayrıntılı çıktı elde etmek için kullanın **-Verbose** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="ce241-252">To get more detailed output, use the **-Verbose** option.</span></span> |
| <span data-ttu-id="ce241-253">Yayımlama WebPackageToVM</span><span class="sxs-lookup"><span data-stu-id="ce241-253">Publish-WebPackageToVM</span></span> |<span data-ttu-id="ce241-254">Parametre değerleri doğrular ve ardından çağırır **Yayımla WebPackage** işlevi.</span><span class="sxs-lookup"><span data-stu-id="ce241-254">Verifies the parameter values, and then calls the **Publish-WebPackage** function.</span></span> |
| <span data-ttu-id="ce241-255">Okuma ConfigFile</span><span class="sxs-lookup"><span data-stu-id="ce241-255">Read-ConfigFile</span></span> |<span data-ttu-id="ce241-256">JSON yapılandırma dosyası doğrular ve seçili değerlerinin bir karma tablosu döndürür.</span><span class="sxs-lookup"><span data-stu-id="ce241-256">Validates the JSON configuration file and returns a hash table of selected values.</span></span> |
| <span data-ttu-id="ce241-257">Geri yükleme-abonelik</span><span class="sxs-lookup"><span data-stu-id="ce241-257">Restore-Subscription</span></span> |<span data-ttu-id="ce241-258">Geçerli aboneliğe özgün abonelik sıfırlar.</span><span class="sxs-lookup"><span data-stu-id="ce241-258">Resets the current subscription to the original subscription.</span></span> |
| <span data-ttu-id="ce241-259">Test-AzureModule</span><span class="sxs-lookup"><span data-stu-id="ce241-259">Test-AzureModule</span></span> |<span data-ttu-id="ce241-260">Döndürür `$true` yüklü Azure Modül sürümü 0.7.4 ise veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="ce241-260">Returns `$true` if the installed Azure module version is 0.7.4 or later.</span></span> <span data-ttu-id="ce241-261">Döndürür `$false` Modülü yüklü değil veya önceki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="ce241-261">Returns `$false` if the module isn't installed or is an earlier version.</span></span> <span data-ttu-id="ce241-262">Bu işlev hiç parametre yok.</span><span class="sxs-lookup"><span data-stu-id="ce241-262">This function has no parameters.</span></span> |
| <span data-ttu-id="ce241-263">Test-AzureModuleVersion</span><span class="sxs-lookup"><span data-stu-id="ce241-263">Test-AzureModuleVersion</span></span> |<span data-ttu-id="ce241-264">Döndürür `$true` Azure modülü sürümü 0.7.4 ise veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="ce241-264">Returns `$true` if the version of the Azure module is 0.7.4 or later.</span></span> <span data-ttu-id="ce241-265">Döndürür `$false` Modülü yüklü değil veya önceki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="ce241-265">Returns `$false` if the module isn't installed or is an earlier version.</span></span> <span data-ttu-id="ce241-266">Bu işlev hiç parametre yok.</span><span class="sxs-lookup"><span data-stu-id="ce241-266">This function has no parameters.</span></span> |
| <span data-ttu-id="ce241-267">Test-HttpsUrl</span><span class="sxs-lookup"><span data-stu-id="ce241-267">Test-HttpsUrl</span></span> |<span data-ttu-id="ce241-268">Giriş URL'SİNİN System.Uri nesnesine dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="ce241-268">Converts the input URL to a System.Uri object.</span></span> <span data-ttu-id="ce241-269">Döndürür `$True` URL mutlak ve kendi şeması https ise.</span><span class="sxs-lookup"><span data-stu-id="ce241-269">Returns `$True` if the URL is absolute and its scheme is https.</span></span> <span data-ttu-id="ce241-270">Döndürür `$false` URL göreli kendi şeması HTTPS değil veya giriş dizesini bir URL dönüştürülemiyor.</span><span class="sxs-lookup"><span data-stu-id="ce241-270">Returns `$false` if the URL is relative, its scheme isn't HTTPS, or the input string can't be converted to a URL.</span></span> |
| <span data-ttu-id="ce241-271">Test-üyesi</span><span class="sxs-lookup"><span data-stu-id="ce241-271">Test-Member</span></span> |<span data-ttu-id="ce241-272">Döndürür `$true` bir özelliği veya yöntemi nesnenin üyesiyse.</span><span class="sxs-lookup"><span data-stu-id="ce241-272">Returns `$true` if a property or method is a member of the object.</span></span> <span data-ttu-id="ce241-273">Aksi takdirde, döndürür `$false`.</span><span class="sxs-lookup"><span data-stu-id="ce241-273">Otherwise, returns `$false`.</span></span> |
| <span data-ttu-id="ce241-274">Yazma ErrorWithTime</span><span class="sxs-lookup"><span data-stu-id="ce241-274">Write-ErrorWithTime</span></span> |<span data-ttu-id="ce241-275">Geçerli saati ile önekli bir hata iletisi yazar.</span><span class="sxs-lookup"><span data-stu-id="ce241-275">Writes an error message prefixed with the current time.</span></span> <span data-ttu-id="ce241-276">Bu işlev çağrılarını **biçimi DevTestMessageWithTime** ileti hata akışı yazmadan önce saat başına işlevi.</span><span class="sxs-lookup"><span data-stu-id="ce241-276">This function calls the **Format-DevTestMessageWithTime** function to prepend the time before writing the message to the Error stream.</span></span> |
| <span data-ttu-id="ce241-277">Yazma HostWithTime</span><span class="sxs-lookup"><span data-stu-id="ce241-277">Write-HostWithTime</span></span> |<span data-ttu-id="ce241-278">Ana bilgisayar programı bir ileti yazar (**Write-Host**) ile geçerli saati öneki.</span><span class="sxs-lookup"><span data-stu-id="ce241-278">Writes a message to the host program (**Write-Host**) prefixed with the current time.</span></span> <span data-ttu-id="ce241-279">Ana bilgisayar programı yazma etkisini değişir.</span><span class="sxs-lookup"><span data-stu-id="ce241-279">The effect of writing to the host program varies.</span></span> <span data-ttu-id="ce241-280">Çoğu program barındıran Windows PowerShell için standart çıktı bu iletiler yazma.</span><span class="sxs-lookup"><span data-stu-id="ce241-280">Most programs that host Windows PowerShell write these messages to standard output.</span></span> |
| <span data-ttu-id="ce241-281">Yazma VerboseWithTime</span><span class="sxs-lookup"><span data-stu-id="ce241-281">Write-VerboseWithTime</span></span> |<span data-ttu-id="ce241-282">Geçerli saati ile önek ayrıntılı bir ileti yazar.</span><span class="sxs-lookup"><span data-stu-id="ce241-282">Writes a verbose message prefixed with the current time.</span></span> <span data-ttu-id="ce241-283">Çağırır çünkü **Write-Verbose**, iletisini görüntüler yalnızca zaman komut dosyasını çalıştırır **ayrıntılı** parametresi veya ne zaman **VerbosePreference** tercih içinayarlama **Devam**.</span><span class="sxs-lookup"><span data-stu-id="ce241-283">Because it calls **Write-Verbose**, the message displays only when the script runs with the **Verbose** parameter or when the **VerbosePreference** preference is set to **Continue**.</span></span> |

<span data-ttu-id="ce241-284">**Yayımlama WebApplication**</span><span class="sxs-lookup"><span data-stu-id="ce241-284">**Publish-WebApplication**</span></span>

| <span data-ttu-id="ce241-285">İşlev adı</span><span class="sxs-lookup"><span data-stu-id="ce241-285">Function name</span></span> | <span data-ttu-id="ce241-286">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ce241-286">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ce241-287">AzureWebApplicationEnvironment yeni</span><span class="sxs-lookup"><span data-stu-id="ce241-287">New-AzureWebApplicationEnvironment</span></span> |<span data-ttu-id="ce241-288">Bir Web sitesi veya sanal makine gibi Azure kaynakları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ce241-288">Creates Azure resources, such as a website or virtual machine.</span></span> |
| <span data-ttu-id="ce241-289">WebDeployPackage yeni</span><span class="sxs-lookup"><span data-stu-id="ce241-289">New-WebDeployPackage</span></span> |<span data-ttu-id="ce241-290">Bu işlev uygulanmadı.</span><span class="sxs-lookup"><span data-stu-id="ce241-290">This function isn't implemented.</span></span> <span data-ttu-id="ce241-291">Projenizi yapılandırmak için bu işlevde komutları ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ce241-291">You can add commands in this function to build your project.</span></span> |
| <span data-ttu-id="ce241-292">Yayımlama AzureWebApplication</span><span class="sxs-lookup"><span data-stu-id="ce241-292">Publish-AzureWebApplication</span></span> |<span data-ttu-id="ce241-293">Azure web uygulaması yayımlar.</span><span class="sxs-lookup"><span data-stu-id="ce241-293">Publishes a web application to Azure.</span></span> |
| <span data-ttu-id="ce241-294">Yayımlama WebApplication</span><span class="sxs-lookup"><span data-stu-id="ce241-294">Publish-WebApplication</span></span> |<span data-ttu-id="ce241-295">Oluşturur ve Web uygulamaları, sanal makineler, SQL veritabanları ve depolama hesapları için bir Visual Studio web projesini dağıtır.</span><span class="sxs-lookup"><span data-stu-id="ce241-295">Creates and deploys Web Apps, virtual machines, SQL databases, and storage accounts for a Visual Studio web project.</span></span> |
| <span data-ttu-id="ce241-296">Test-WebApplication</span><span class="sxs-lookup"><span data-stu-id="ce241-296">Test-WebApplication</span></span> |<span data-ttu-id="ce241-297">Bu işlev uygulanmadı.</span><span class="sxs-lookup"><span data-stu-id="ce241-297">This function isn't implemented.</span></span> <span data-ttu-id="ce241-298">Uygulamanızı test etmek için bu işlevde komutları ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ce241-298">You can add commands in this function to test your application.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ce241-299">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ce241-299">Next steps</span></span>
<span data-ttu-id="ce241-300">PowerShell okuyarak komut dosyası hakkında daha fazla bilgi [ile Windows PowerShell komut dosyası](https://technet.microsoft.com/library/bb978526.aspx) ve diğer Azure PowerShell komut dosyalarını en [Komut Merkezi](https://azure.microsoft.com/documentation/scripts/).</span><span class="sxs-lookup"><span data-stu-id="ce241-300">Learn more about PowerShell scripting by reading [Scripting with Windows PowerShell](https://technet.microsoft.com/library/bb978526.aspx) and see other Azure PowerShell scripts at the [Script Center](https://azure.microsoft.com/documentation/scripts/).</span></span>
