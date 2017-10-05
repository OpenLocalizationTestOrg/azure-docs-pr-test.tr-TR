---
title: "Başlatılamaz rolleri sorunlarını giderme | Microsoft Docs"
description: "Neden bir bulut hizmeti rolü başlatılamayabilir bazı yaygın nedenler şunlardır. Bu sorunların çözümlerini de sağlanır."
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 674b2faf-26d7-4f54-99ea-a9e02ef0eb2f
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: 7d956192e8b9c3688b8b6f0108bd9296f66fbd62
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshoot-cloud-service-roles-that-fail-to-start"></a><span data-ttu-id="063b8-104">Başlatılamaz bulut hizmeti rolleriyle ilgili sorunları giderme</span><span class="sxs-lookup"><span data-stu-id="063b8-104">Troubleshoot Cloud Service roles that fail to start</span></span>
<span data-ttu-id="063b8-105">Çözümleri Azure bulut hizmetlerine başlatılamaz rolleri ilgili ve bazı yaygın sorunlar şunlardır.</span><span class="sxs-lookup"><span data-stu-id="063b8-105">Here are some common problems and solutions related to Azure Cloud Services roles that fail to start.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="missing-dlls-or-dependencies"></a><span data-ttu-id="063b8-106">Eksik DLL'leri veya bağımlılıkları</span><span class="sxs-lookup"><span data-stu-id="063b8-106">Missing DLLs or dependencies</span></span>
<span data-ttu-id="063b8-107">Yanıt vermeyen rolleri ve arasında geçiş yapma rolleri **başlatılıyor**, **meşgul**, ve **durdurma** durumları DLL'leri veya derlemeleri eksik kaynaklanabilir.</span><span class="sxs-lookup"><span data-stu-id="063b8-107">Unresponsive roles and roles that are cycling between **Initializing**, **Busy**, and **Stopping** states can be caused by missing DLLs or assemblies.</span></span>

<span data-ttu-id="063b8-108">DLL'leri veya derlemeleri eksik Belirtiler şunlar olabilir:</span><span class="sxs-lookup"><span data-stu-id="063b8-108">Symptoms of missing DLLs or assemblies can be:</span></span>

* <span data-ttu-id="063b8-109">Rol örneği dolaşma **başlatılıyor**, **meşgul**, ve **durdurma** durumları.</span><span class="sxs-lookup"><span data-stu-id="063b8-109">Your role instance is cycling through **Initializing**, **Busy**, and **Stopping** states.</span></span>
* <span data-ttu-id="063b8-110">Rol örneği için geçmiştir **hazır** ancak web uygulamanıza giderseniz, sayfa görünmez.</span><span class="sxs-lookup"><span data-stu-id="063b8-110">Your role instance has moved to **Ready** but if you navigate to your web application, the page does not appear.</span></span>

<span data-ttu-id="063b8-111">Bu sorunları incelemeye için önerilen çeşitli yöntemler vardır.</span><span class="sxs-lookup"><span data-stu-id="063b8-111">There are several recommended methods for investigating these issues.</span></span>

## <a name="diagnose-missing-dll-issues-in-a-web-role"></a><span data-ttu-id="063b8-112">Web rolü eksik DLL sorunları tanılama</span><span class="sxs-lookup"><span data-stu-id="063b8-112">Diagnose missing DLL issues in a web role</span></span>
<span data-ttu-id="063b8-113">Dağıtılan bir Web sitesine gidin, bir web rolü ve tarayıcı aşağıdakine benzer bir sunucu hatası görüntüler, DLL eksik olduğunu gösteriyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="063b8-113">When you navigate to a website that is deployed in a web role, and the browser displays a server error similar to the following, it may indicate that a DLL is missing.</span></span>

!['/' Uygulamasında sunucu hatası.](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503388.png)

## <a name="diagnose-issues-by-turning-off-custom-errors"></a><span data-ttu-id="063b8-115">Özel hatalar devre dışı bırakarak sorunlarını tanılamak</span><span class="sxs-lookup"><span data-stu-id="063b8-115">Diagnose issues by turning off custom errors</span></span>
<span data-ttu-id="063b8-116">Daha ayrıntılı hata bilgileri özel hata modu kapalı olarak ayarlamak web rolü için web.config yapılandırma ve hizmet dağıtarak görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="063b8-116">More complete error information can be viewed by configuring the web.config for the web role to set the custom error mode to Off and redeploying the service.</span></span>

<span data-ttu-id="063b8-117">Uzak Masaüstü'nü kullanmadan daha ayrıntılı hataları görüntülemek için:</span><span class="sxs-lookup"><span data-stu-id="063b8-117">To view more complete errors without using Remote Desktop:</span></span>

1. <span data-ttu-id="063b8-118">Microsoft Visual Studio çözümü açın.</span><span class="sxs-lookup"><span data-stu-id="063b8-118">Open the solution in Microsoft Visual Studio.</span></span>
2. <span data-ttu-id="063b8-119">İçinde **Çözüm Gezgini**, web.config dosyasını bulun ve açın.</span><span class="sxs-lookup"><span data-stu-id="063b8-119">In the **Solution Explorer**, locate the web.config file and open it.</span></span>
3. <span data-ttu-id="063b8-120">Web.config dosyasında system.web bölümünü bulun ve aşağıdaki satırı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="063b8-120">In the web.config file, locate the system.web section and add the following line:</span></span>

    ```xml
    <customErrors mode="Off" />
    ```
4. <span data-ttu-id="063b8-121">Dosyayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="063b8-121">Save the file.</span></span>
5. <span data-ttu-id="063b8-122">Yeniden paketleyin ve hizmeti yeniden dağıtın.</span><span class="sxs-lookup"><span data-stu-id="063b8-122">Repackage and redeploy the service.</span></span>

<span data-ttu-id="063b8-123">Hizmet imzalanmasını sonra eksik derleme veya DLL adı ile bir hata iletisi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="063b8-123">Once the service is redeployed, you will see an error message with the name of the missing assembly or DLL.</span></span>

## <a name="diagnose-issues-by-viewing-the-error-remotely"></a><span data-ttu-id="063b8-124">Uzaktan hata görüntüleyerek sorunlarını tanılamak</span><span class="sxs-lookup"><span data-stu-id="063b8-124">Diagnose issues by viewing the error remotely</span></span>
<span data-ttu-id="063b8-125">Rol erişmek ve daha ayrıntılı hata bilgileri uzaktan görüntülemek için Uzak Masaüstü'nü kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="063b8-125">You can use Remote Desktop to access the role and view more complete error information remotely.</span></span> <span data-ttu-id="063b8-126">Uzak Masaüstü'nü kullanarak hataları görüntülemek için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="063b8-126">Use the following steps to view the errors by using Remote Desktop:</span></span>

1. <span data-ttu-id="063b8-127">Azure SDK 1.3 veya üstü yüklü olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="063b8-127">Ensure that Azure SDK 1.3 or later is installed.</span></span>
2. <span data-ttu-id="063b8-128">Visual Studio kullanarak çözüm dağıtımı sırasında "Yapılandırma Uzak Masaüstü bağlantıları için..." seçin.</span><span class="sxs-lookup"><span data-stu-id="063b8-128">During the deployment of the solution by using Visual Studio, choose to “Configure Remote Desktop connections…”.</span></span> <span data-ttu-id="063b8-129">Uzak Masaüstü bağlantısı yapılandırma hakkında daha fazla bilgi için bkz: [Azure rolleri ile Uzak Masaüstü kullanarak](../vs-azure-tools-remote-desktop-roles.md).</span><span class="sxs-lookup"><span data-stu-id="063b8-129">For more information on configuring the Remote Desktop connection, see [Using Remote Desktop with Azure Roles](../vs-azure-tools-remote-desktop-roles.md).</span></span>
3. <span data-ttu-id="063b8-130">Örnek bir durumu gösterir sonra Microsoft Azure Klasik portalında, **hazır**, rol örnekleri birine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="063b8-130">In the Microsoft Azure classic portal, once the instance shows a status of **Ready**, click one of the role instances.</span></span>
4. <span data-ttu-id="063b8-131">Tıklatın **Bağlan** simgesine **uzaktan erişim** Şerit alanı.</span><span class="sxs-lookup"><span data-stu-id="063b8-131">Click the **Connect** icon in the **Remote Access** area of the ribbon.</span></span>
5. <span data-ttu-id="063b8-132">Sanal makineye uzak masaüstü yapılandırması sırasında belirtilen kimlik bilgilerini kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="063b8-132">Sign in to the virtual machine by using the credentials that were specified during the Remote Desktop configuration.</span></span>
6. <span data-ttu-id="063b8-133">Bir komut penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="063b8-133">Open a command window.</span></span>
7. <span data-ttu-id="063b8-134">`IPconfig` yazın.</span><span class="sxs-lookup"><span data-stu-id="063b8-134">Type `IPconfig`.</span></span>
8. <span data-ttu-id="063b8-135">IPv4 adresi değerini not edin.</span><span class="sxs-lookup"><span data-stu-id="063b8-135">Note the IPV4 Address value.</span></span>
9. <span data-ttu-id="063b8-136">Internet Explorer'ı açın.</span><span class="sxs-lookup"><span data-stu-id="063b8-136">Open Internet Explorer.</span></span>
10. <span data-ttu-id="063b8-137">Adres ve web uygulamasının adını yazın.</span><span class="sxs-lookup"><span data-stu-id="063b8-137">Type the address and the name of the web application.</span></span> <span data-ttu-id="063b8-138">Örneğin, `http://<IPV4 Address>/default.aspx`.</span><span class="sxs-lookup"><span data-stu-id="063b8-138">For example, `http://<IPV4 Address>/default.aspx`.</span></span>

<span data-ttu-id="063b8-139">Web sitesine giderek daha açık hata iletileri artık döndürür:</span><span class="sxs-lookup"><span data-stu-id="063b8-139">Navigating to the website will now return more explicit error messages:</span></span>

* <span data-ttu-id="063b8-140">'/' Uygulamasında sunucu hatası.</span><span class="sxs-lookup"><span data-stu-id="063b8-140">Server Error in '/' Application.</span></span>
* <span data-ttu-id="063b8-141">Açıklama: Geçerli web isteğinin yürütülmesi sırasında işlenmemiş bir özel durum oluştu.</span><span class="sxs-lookup"><span data-stu-id="063b8-141">Description: An unhandled exception occurred during the execution of the current web request.</span></span> <span data-ttu-id="063b8-142">Lütfen hata hakkındaki ve kodda geldiği daha fazla bilgi için yığın izlemesi gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="063b8-142">Please review the stack trace for more information about the error and where it originated in the code.</span></span>
* <span data-ttu-id="063b8-143">Özel durum ayrıntıları: System.IO.FIleNotFoundException: dosya veya derleme yüklenemedi ' Microsoft.WindowsAzure.StorageClient, sürüm 1.1.0.0, Culture = neutral, PublicKeyToken = 31bf856ad364e35 =' ya da bağımlılıklarından biri.</span><span class="sxs-lookup"><span data-stu-id="063b8-143">Exception Details: System.IO.FIleNotFoundException: Could not load file or assembly ‘Microsoft.WindowsAzure.StorageClient, Version=1.1.0.0, Culture=neutral, PublicKeyToken=31bf856ad364e35’ or one of its dependencies.</span></span> <span data-ttu-id="063b8-144">Sistem belirtilen dosyayı bulamıyor.</span><span class="sxs-lookup"><span data-stu-id="063b8-144">The system cannot find the file specified.</span></span>

<span data-ttu-id="063b8-145">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="063b8-145">For example:</span></span>

!['/' Uygulamasında açık sunucu hatası](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503389.png)

## <a name="diagnose-issues-by-using-the-compute-emulator"></a><span data-ttu-id="063b8-147">İşlem öykünücüsü kullanarak sorunları tanılamak</span><span class="sxs-lookup"><span data-stu-id="063b8-147">Diagnose issues by using the compute emulator</span></span>
<span data-ttu-id="063b8-148">Microsoft Azure işlem öykünücüsü tanılamak ve bağımlılıklar ve web.config hataları eksik sorunlarını gidermek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="063b8-148">You can use the Microsoft Azure compute emulator to diagnose and troubleshoot issues of missing dependencies and web.config errors.</span></span>

<span data-ttu-id="063b8-149">Tanılama bu yöntemi kullanmanın en iyi sonuçlar için bir bilgisayarı veya Windows temiz bir yüklemesini sanal makine kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="063b8-149">For best results in using this method of diagnosis, you should use a computer or virtual machine that has a clean installation of Windows.</span></span> <span data-ttu-id="063b8-150">En iyi Azure ortamının benzetimini yapmak için Windows Server 2008 R2 x64 kullanın.</span><span class="sxs-lookup"><span data-stu-id="063b8-150">To best simulate the Azure environment, use Windows Server 2008 R2 x64.</span></span>

1. <span data-ttu-id="063b8-151">Tek başına bir sürümünü yüklemek [Azure SDK'sı](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="063b8-151">Install the standalone version of the [Azure SDK](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="063b8-152">Geliştirme makinenizde bulut hizmeti projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="063b8-152">On the development machine, build the cloud service project.</span></span>
3. <span data-ttu-id="063b8-153">Windows Gezgini'nde klasörüne bulut hizmeti projesine gidin.</span><span class="sxs-lookup"><span data-stu-id="063b8-153">In Windows Explorer, navigate to the bin\debug folder of the cloud service project.</span></span>
4. <span data-ttu-id="063b8-154">.Csx klasörü ve .cscfg dosyasını sorunları hata ayıklamak için kullanmakta olduğunuz bilgisayara kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="063b8-154">Copy the .csx folder and .cscfg file to the computer that you are using to debug the issues.</span></span>
5. <span data-ttu-id="063b8-155">Temiz makinede bir Azure SDK komut istemi penceresi açıp `csrun.exe /devstore:start`.</span><span class="sxs-lookup"><span data-stu-id="063b8-155">On the clean machine, open an Azure SDK Command Prompt window and type `csrun.exe /devstore:start`.</span></span>
6. <span data-ttu-id="063b8-156">Komut isteminde `run csrun <path to .csx folder> <path to .cscfg file> /launchBrowser`.</span><span class="sxs-lookup"><span data-stu-id="063b8-156">At the command prompt, type `run csrun <path to .csx folder> <path to .cscfg file> /launchBrowser`.</span></span>
7. <span data-ttu-id="063b8-157">Rol başladığında, Internet Explorer'da ayrıntılı hata bilgileri görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="063b8-157">When the role starts, you will see detailed error information in Internet Explorer.</span></span> <span data-ttu-id="063b8-158">Daha fazla sorunu tanılamak için standart Windows sorun giderme araçları da kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="063b8-158">You can also use standard Windows troubleshooting tools to further diagnose the problem.</span></span>

## <a name="diagnose-issues-by-using-intellitrace"></a><span data-ttu-id="063b8-159">IntelliTrace kullanarak sorunları tanılamak</span><span class="sxs-lookup"><span data-stu-id="063b8-159">Diagnose issues by using IntelliTrace</span></span>
<span data-ttu-id="063b8-160">Çalışan ve .NET Framework 4 kullanan web rolleri için kullanabileceğiniz [IntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx), Microsoft Visual Studio Enterprise'da kullanılabilir olduğu.</span><span class="sxs-lookup"><span data-stu-id="063b8-160">For worker and web roles that use .NET Framework 4, you can use [IntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx), which is available in Microsoft Visual Studio Enterprise.</span></span>

<span data-ttu-id="063b8-161">Hizmet etkin IntelliTrace ile dağıtmak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="063b8-161">Follow these steps to deploy the service with IntelliTrace enabled:</span></span>

1. <span data-ttu-id="063b8-162">Azure SDK 1.3 veya üstü yüklü olduğunu onaylayın.</span><span class="sxs-lookup"><span data-stu-id="063b8-162">Confirm that Azure SDK 1.3 or later is installed.</span></span>
2. <span data-ttu-id="063b8-163">Çözüm, Visual Studio kullanarak dağıtın.</span><span class="sxs-lookup"><span data-stu-id="063b8-163">Deploy the solution by using Visual Studio.</span></span> <span data-ttu-id="063b8-164">Dağıtım sırasında kontrol **.NET 4 rolleri için IntelliTrace'i etkinleştirin** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="063b8-164">During deployment, check the **Enable IntelliTrace for .NET 4 roles** check box.</span></span>
3. <span data-ttu-id="063b8-165">Bir örneğini başlatır, açın **Sunucu Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="063b8-165">Once the instance starts, open the **Server Explorer**.</span></span>
4. <span data-ttu-id="063b8-166">Genişletme **Azure\\bulut Hizmetleri** düğümü ve dağıtımını bulun.</span><span class="sxs-lookup"><span data-stu-id="063b8-166">Expand the **Azure\\Cloud Services** node and locate the deployment.</span></span>
5. <span data-ttu-id="063b8-167">Dağıtım rol örnekleri görene kadar genişletin.</span><span class="sxs-lookup"><span data-stu-id="063b8-167">Expand the deployment until you see the role instances.</span></span> <span data-ttu-id="063b8-168">Örneklerden birini sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="063b8-168">Right-click on one of the instances.</span></span>
6. <span data-ttu-id="063b8-169">Seçin **görünüm IntelliTrace günlüklerini**.</span><span class="sxs-lookup"><span data-stu-id="063b8-169">Choose **View IntelliTrace logs**.</span></span> <span data-ttu-id="063b8-170">**IntelliTrace Özet** açılır.</span><span class="sxs-lookup"><span data-stu-id="063b8-170">The **IntelliTrace Summary** will open.</span></span>
7. <span data-ttu-id="063b8-171">Özet özel durumlara bölümünü bulun.</span><span class="sxs-lookup"><span data-stu-id="063b8-171">Locate the exceptions section of the summary.</span></span> <span data-ttu-id="063b8-172">Özel durumlar varsa, bölüm etiketli **özel durum verileri**.</span><span class="sxs-lookup"><span data-stu-id="063b8-172">If there are exceptions, the section will be labeled **Exception Data**.</span></span>
8. <span data-ttu-id="063b8-173">Genişletme **özel durum verileri** ve Ara **System.IO.FileNotFoundException** hatalarla aşağıdakine benzer:</span><span class="sxs-lookup"><span data-stu-id="063b8-173">Expand the **Exception Data** and look for **System.IO.FileNotFoundException** errors similar to the following:</span></span>

![Özel durum verileri, eksik dosya veya derleme](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503390.png)

## <a name="address-missing-dlls-and-assemblies"></a><span data-ttu-id="063b8-175">Adres eksik DLL'ler ve derlemeler</span><span class="sxs-lookup"><span data-stu-id="063b8-175">Address missing DLLs and assemblies</span></span>
<span data-ttu-id="063b8-176">Eksik DLL ve derleme hataları gidermek için şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="063b8-176">To address missing DLL and assembly errors, follow these steps:</span></span>

1. <span data-ttu-id="063b8-177">Çözümü Visual Studio'da açın.</span><span class="sxs-lookup"><span data-stu-id="063b8-177">Open the solution in Visual Studio.</span></span>
2. <span data-ttu-id="063b8-178">İçinde **Çözüm Gezgini**, açık **başvuruları** klasör.</span><span class="sxs-lookup"><span data-stu-id="063b8-178">In **Solution Explorer**, open the **References** folder.</span></span>
3. <span data-ttu-id="063b8-179">Hata tanımlanan derleme'yi tıklayın.</span><span class="sxs-lookup"><span data-stu-id="063b8-179">Click the assembly identified in the error.</span></span>
4. <span data-ttu-id="063b8-180">İçinde **özellikleri** bölmesinde bulun **kopya yerel özellik** ve değerine **doğru**.</span><span class="sxs-lookup"><span data-stu-id="063b8-180">In the **Properties** pane, locate **Copy Local property** and set the value to **True**.</span></span>
5. <span data-ttu-id="063b8-181">Bulut hizmeti yeniden dağıtın.</span><span class="sxs-lookup"><span data-stu-id="063b8-181">Redeploy the cloud service.</span></span>

<span data-ttu-id="063b8-182">Tüm hataları düzelttikten olduğunu doğruladıktan sonra hizmet denetlemeden dağıtabileceğiniz **.NET 4 rolleri için IntelliTrace'i etkinleştirin** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="063b8-182">Once you have verified that all errors have been corrected, you can deploy the service without checking the **Enable IntelliTrace for .NET 4 roles** check box.</span></span>

## <a name="next-steps"></a><span data-ttu-id="063b8-183">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="063b8-183">Next steps</span></span>
<span data-ttu-id="063b8-184">Daha fazla bilgi görüntülemek [sorun giderme makalelerini](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) bulut Hizmetleri için.</span><span class="sxs-lookup"><span data-stu-id="063b8-184">View more [troubleshooting articles](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) for cloud services.</span></span>

<span data-ttu-id="063b8-185">Azure PaaS bilgisayar tanılama verilerini kullanarak bulut hizmeti rolü sorunlarını giderme konusunda bilgi almak için bkz: [Kevin Williamson'ın blog dizisini](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span><span class="sxs-lookup"><span data-stu-id="063b8-185">To learn how to troubleshoot cloud service role issues by using Azure PaaS computer diagnostics data, see [Kevin Williamson's blog series](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span></span>
