---
title: "toostart başarısız aaaTroubleshoot rolleri | Microsoft Docs"
description: "Bir bulut hizmeti rolü toostart neden başarısız olabileceği bazı yaygın nedenler şunlardır. Çözümler toothese sorunlar de sağlanmıştır."
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
ms.openlocfilehash: e2fbecb08a10984add79dfc74e73de6869bb314f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-cloud-service-roles-that-fail-toostart"></a><span data-ttu-id="4115e-104">Toostart başarısız bulut hizmeti rolleriyle ilgili sorunları giderme</span><span class="sxs-lookup"><span data-stu-id="4115e-104">Troubleshoot Cloud Service roles that fail toostart</span></span>
<span data-ttu-id="4115e-105">Bazı yaygın sorunlar ve toostart başarısız çözümleri ilgili tooAzure bulut Hizmetleri rolleri aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="4115e-105">Here are some common problems and solutions related tooAzure Cloud Services roles that fail toostart.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="missing-dlls-or-dependencies"></a><span data-ttu-id="4115e-106">Eksik DLL'leri veya bağımlılıkları</span><span class="sxs-lookup"><span data-stu-id="4115e-106">Missing DLLs or dependencies</span></span>
<span data-ttu-id="4115e-107">Yanıt vermeyen rolleri ve arasında geçiş yapma rolleri **başlatılıyor**, **meşgul**, ve **durdurma** durumları DLL'leri veya derlemeleri eksik kaynaklanabilir.</span><span class="sxs-lookup"><span data-stu-id="4115e-107">Unresponsive roles and roles that are cycling between **Initializing**, **Busy**, and **Stopping** states can be caused by missing DLLs or assemblies.</span></span>

<span data-ttu-id="4115e-108">DLL'leri veya derlemeleri eksik Belirtiler şunlar olabilir:</span><span class="sxs-lookup"><span data-stu-id="4115e-108">Symptoms of missing DLLs or assemblies can be:</span></span>

* <span data-ttu-id="4115e-109">Rol örneği dolaşma **başlatılıyor**, **meşgul**, ve **durdurma** durumları.</span><span class="sxs-lookup"><span data-stu-id="4115e-109">Your role instance is cycling through **Initializing**, **Busy**, and **Stopping** states.</span></span>
* <span data-ttu-id="4115e-110">Rol örneği çok taşındı**hazır** ancak tooyour web uygulaması giderseniz, hello sayfası görünmez.</span><span class="sxs-lookup"><span data-stu-id="4115e-110">Your role instance has moved too**Ready** but if you navigate tooyour web application, hello page does not appear.</span></span>

<span data-ttu-id="4115e-111">Bu sorunları incelemeye için önerilen çeşitli yöntemler vardır.</span><span class="sxs-lookup"><span data-stu-id="4115e-111">There are several recommended methods for investigating these issues.</span></span>

## <a name="diagnose-missing-dll-issues-in-a-web-role"></a><span data-ttu-id="4115e-112">Web rolü eksik DLL sorunları tanılama</span><span class="sxs-lookup"><span data-stu-id="4115e-112">Diagnose missing DLL issues in a web role</span></span>
<span data-ttu-id="4115e-113">Bir web rolünde dağıtılan tooa Web sitesine gidin ve bir sunucu hatası benzer toohello aşağıdaki hello tarayıcı görüntüler, DLL eksik olduğunu gösteriyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="4115e-113">When you navigate tooa website that is deployed in a web role, and hello browser displays a server error similar toohello following, it may indicate that a DLL is missing.</span></span>

!['/' Uygulamasında sunucu hatası.](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503388.png)

## <a name="diagnose-issues-by-turning-off-custom-errors"></a><span data-ttu-id="4115e-115">Özel hatalar devre dışı bırakarak sorunlarını tanılamak</span><span class="sxs-lookup"><span data-stu-id="4115e-115">Diagnose issues by turning off custom errors</span></span>
<span data-ttu-id="4115e-116">Daha ayrıntılı hata bilgileri hello web.config hello web rolü tooset hello özel hata modu tooOff için yapılandırma ve hello hizmet dağıtarak görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="4115e-116">More complete error information can be viewed by configuring hello web.config for hello web role tooset hello custom error mode tooOff and redeploying hello service.</span></span>

<span data-ttu-id="4115e-117">tooview daha tamamlamak hataları Uzak Masaüstü'nü kullanmadan:</span><span class="sxs-lookup"><span data-stu-id="4115e-117">tooview more complete errors without using Remote Desktop:</span></span>

1. <span data-ttu-id="4115e-118">Merhaba çözümü Microsoft Visual Studio'da açın.</span><span class="sxs-lookup"><span data-stu-id="4115e-118">Open hello solution in Microsoft Visual Studio.</span></span>
2. <span data-ttu-id="4115e-119">Merhaba, **Çözüm Gezgini**, hello web.config dosyasını bulun ve açın.</span><span class="sxs-lookup"><span data-stu-id="4115e-119">In hello **Solution Explorer**, locate hello web.config file and open it.</span></span>
3. <span data-ttu-id="4115e-120">Merhaba web.config dosyasında hello system.web bölümünü bulun ve hello aşağıdaki satırı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="4115e-120">In hello web.config file, locate hello system.web section and add hello following line:</span></span>

    ```xml
    <customErrors mode="Off" />
    ```
4. <span data-ttu-id="4115e-121">Merhaba dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="4115e-121">Save hello file.</span></span>
5. <span data-ttu-id="4115e-122">Yeniden paketleyin ve hello hizmeti yeniden dağıtın.</span><span class="sxs-lookup"><span data-stu-id="4115e-122">Repackage and redeploy hello service.</span></span>

<span data-ttu-id="4115e-123">Merhaba hizmet imzalanmasını sonra eksik derleme veya DLL hello hello adı ile bir hata iletisi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="4115e-123">Once hello service is redeployed, you will see an error message with hello name of hello missing assembly or DLL.</span></span>

## <a name="diagnose-issues-by-viewing-hello-error-remotely"></a><span data-ttu-id="4115e-124">Merhaba hata uzaktan görüntüleyerek sorunlarını tanılamak</span><span class="sxs-lookup"><span data-stu-id="4115e-124">Diagnose issues by viewing hello error remotely</span></span>
<span data-ttu-id="4115e-125">Uzak Masaüstü tooaccess hello rolünü kullanın ve Uzaktan daha eksiksiz hata bilgilerini görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="4115e-125">You can use Remote Desktop tooaccess hello role and view more complete error information remotely.</span></span> <span data-ttu-id="4115e-126">Uzak Masaüstü'nü kullanarak aşağıdaki adımları tooview hello hatalar hello kullan:</span><span class="sxs-lookup"><span data-stu-id="4115e-126">Use hello following steps tooview hello errors by using Remote Desktop:</span></span>

1. <span data-ttu-id="4115e-127">Azure SDK 1.3 veya üstü yüklü olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="4115e-127">Ensure that Azure SDK 1.3 or later is installed.</span></span>
2. <span data-ttu-id="4115e-128">Visual Studio kullanarak hello çözüm Hello dağıtımı sırasında çok seçin "yapılandırma Uzak Masaüstü bağlantıları...".</span><span class="sxs-lookup"><span data-stu-id="4115e-128">During hello deployment of hello solution by using Visual Studio, choose too“Configure Remote Desktop connections…”.</span></span> <span data-ttu-id="4115e-129">Merhaba Uzak Masaüstü bağlantısı yapılandırma hakkında daha fazla bilgi için bkz: [Azure rolleri ile Uzak Masaüstü kullanarak](../vs-azure-tools-remote-desktop-roles.md).</span><span class="sxs-lookup"><span data-stu-id="4115e-129">For more information on configuring hello Remote Desktop connection, see [Using Remote Desktop with Azure Roles](../vs-azure-tools-remote-desktop-roles.md).</span></span>
3. <span data-ttu-id="4115e-130">Merhaba örneği durumunu gösterir sonra hello Microsoft Azure Klasik Portalı'nda, **hazır**, hello rol örnekleri birine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4115e-130">In hello Microsoft Azure classic portal, once hello instance shows a status of **Ready**, click one of hello role instances.</span></span>
4. <span data-ttu-id="4115e-131">Merhaba tıklatın **Bağlan** hello simgesinde **uzaktan erişim** hello Şerit alanı.</span><span class="sxs-lookup"><span data-stu-id="4115e-131">Click hello **Connect** icon in hello **Remote Access** area of hello ribbon.</span></span>
5. <span data-ttu-id="4115e-132">Toohello sanal makinede hello uzak masaüstü yapılandırması sırasında belirtilen hello kimlik bilgilerini kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="4115e-132">Sign in toohello virtual machine by using hello credentials that were specified during hello Remote Desktop configuration.</span></span>
6. <span data-ttu-id="4115e-133">Bir komut penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="4115e-133">Open a command window.</span></span>
7. <span data-ttu-id="4115e-134">`IPconfig` yazın.</span><span class="sxs-lookup"><span data-stu-id="4115e-134">Type `IPconfig`.</span></span>
8. <span data-ttu-id="4115e-135">Başlangıç IPv4 adresi değerini not edin.</span><span class="sxs-lookup"><span data-stu-id="4115e-135">Note hello IPV4 Address value.</span></span>
9. <span data-ttu-id="4115e-136">Internet Explorer'ı açın.</span><span class="sxs-lookup"><span data-stu-id="4115e-136">Open Internet Explorer.</span></span>
10. <span data-ttu-id="4115e-137">Başlangıç adresi ve hello hello web uygulamasının adını yazın.</span><span class="sxs-lookup"><span data-stu-id="4115e-137">Type hello address and hello name of hello web application.</span></span> <span data-ttu-id="4115e-138">Örneğin, `http://<IPV4 Address>/default.aspx`.</span><span class="sxs-lookup"><span data-stu-id="4115e-138">For example, `http://<IPV4 Address>/default.aspx`.</span></span>

<span data-ttu-id="4115e-139">Web sitesi, toohello gezinme şimdi daha açık hata iletileri döndürür:</span><span class="sxs-lookup"><span data-stu-id="4115e-139">Navigating toohello website will now return more explicit error messages:</span></span>

* <span data-ttu-id="4115e-140">'/' Uygulamasında sunucu hatası.</span><span class="sxs-lookup"><span data-stu-id="4115e-140">Server Error in '/' Application.</span></span>
* <span data-ttu-id="4115e-141">Açıklama: Hello geçerli web isteği hello yürütülmesi sırasında işlenmemiş bir özel durum oluştu.</span><span class="sxs-lookup"><span data-stu-id="4115e-141">Description: An unhandled exception occurred during hello execution of hello current web request.</span></span> <span data-ttu-id="4115e-142">Lütfen hello hata hakkında daha fazla bilgi için hello yığın izleme ve hello kodda geldiği gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="4115e-142">Please review hello stack trace for more information about hello error and where it originated in hello code.</span></span>
* <span data-ttu-id="4115e-143">Özel durum ayrıntıları: System.IO.FIleNotFoundException: dosya veya derleme yüklenemedi ' Microsoft.WindowsAzure.StorageClient, sürüm 1.1.0.0, Culture = neutral, PublicKeyToken = 31bf856ad364e35 =' ya da bağımlılıklarından biri.</span><span class="sxs-lookup"><span data-stu-id="4115e-143">Exception Details: System.IO.FIleNotFoundException: Could not load file or assembly ‘Microsoft.WindowsAzure.StorageClient, Version=1.1.0.0, Culture=neutral, PublicKeyToken=31bf856ad364e35’ or one of its dependencies.</span></span> <span data-ttu-id="4115e-144">Merhaba Sistem belirtilen hello dosyası bulunamıyor.</span><span class="sxs-lookup"><span data-stu-id="4115e-144">hello system cannot find hello file specified.</span></span>

<span data-ttu-id="4115e-145">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="4115e-145">For example:</span></span>

!['/' Uygulamasında açık sunucu hatası](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503389.png)

## <a name="diagnose-issues-by-using-hello-compute-emulator"></a><span data-ttu-id="4115e-147">Merhaba işlem öykünücüsü kullanarak sorunları tanılamak</span><span class="sxs-lookup"><span data-stu-id="4115e-147">Diagnose issues by using hello compute emulator</span></span>
<span data-ttu-id="4115e-148">Merhaba Microsoft Azure işlem öykünücüsü toodiagnose ve bağımlılıklar ve web.config hataları eksik sorunlarını giderme kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4115e-148">You can use hello Microsoft Azure compute emulator toodiagnose and troubleshoot issues of missing dependencies and web.config errors.</span></span>

<span data-ttu-id="4115e-149">Tanılama bu yöntemi kullanmanın en iyi sonuçlar için bir bilgisayarı veya Windows temiz bir yüklemesini sanal makine kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4115e-149">For best results in using this method of diagnosis, you should use a computer or virtual machine that has a clean installation of Windows.</span></span> <span data-ttu-id="4115e-150">toobest hello Azure ortamı benzetimini yapmak için Windows Server 2008 R2 x64 kullanın.</span><span class="sxs-lookup"><span data-stu-id="4115e-150">toobest simulate hello Azure environment, use Windows Server 2008 R2 x64.</span></span>

1. <span data-ttu-id="4115e-151">Merhaba Hello tek başına sürümünü yüklemek [Azure SDK'sı](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="4115e-151">Install hello standalone version of hello [Azure SDK](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="4115e-152">Merhaba geliştirme makinenizde hello bulut hizmeti projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4115e-152">On hello development machine, build hello cloud service project.</span></span>
3. <span data-ttu-id="4115e-153">Windows Gezgini'nde hello bulut hizmeti projesi, toohello klasörüne gidin.</span><span class="sxs-lookup"><span data-stu-id="4115e-153">In Windows Explorer, navigate toohello bin\debug folder of hello cloud service project.</span></span>
4. <span data-ttu-id="4115e-154">Merhaba .csx klasörünü ve toodebug hello sorunları kullandığınız .cscfg dosya toohello bilgisayara kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="4115e-154">Copy hello .csx folder and .cscfg file toohello computer that you are using toodebug hello issues.</span></span>
5. <span data-ttu-id="4115e-155">Temiz makine Hello üzerinde bir Azure SDK komut istemi penceresi açıp `csrun.exe /devstore:start`.</span><span class="sxs-lookup"><span data-stu-id="4115e-155">On hello clean machine, open an Azure SDK Command Prompt window and type `csrun.exe /devstore:start`.</span></span>
6. <span data-ttu-id="4115e-156">Merhaba komut istemine yazın `run csrun <path too.csx folder> <path too.cscfg file> /launchBrowser`.</span><span class="sxs-lookup"><span data-stu-id="4115e-156">At hello command prompt, type `run csrun <path too.csx folder> <path too.cscfg file> /launchBrowser`.</span></span>
7. <span data-ttu-id="4115e-157">Merhaba rol başladığında, Internet Explorer'da ayrıntılı hata bilgileri görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="4115e-157">When hello role starts, you will see detailed error information in Internet Explorer.</span></span> <span data-ttu-id="4115e-158">Standart Windows sorun giderme araçları da kullanabilirsiniz toofurther hello sorunu tanılamak.</span><span class="sxs-lookup"><span data-stu-id="4115e-158">You can also use standard Windows troubleshooting tools toofurther diagnose hello problem.</span></span>

## <a name="diagnose-issues-by-using-intellitrace"></a><span data-ttu-id="4115e-159">IntelliTrace kullanarak sorunları tanılamak</span><span class="sxs-lookup"><span data-stu-id="4115e-159">Diagnose issues by using IntelliTrace</span></span>
<span data-ttu-id="4115e-160">Çalışan ve .NET Framework 4 kullanan web rolleri için kullanabileceğiniz [IntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx), Microsoft Visual Studio Enterprise'da kullanılabilir olduğu.</span><span class="sxs-lookup"><span data-stu-id="4115e-160">For worker and web roles that use .NET Framework 4, you can use [IntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx), which is available in Microsoft Visual Studio Enterprise.</span></span>

<span data-ttu-id="4115e-161">Bu adımları toodeploy hello hizmeti etkin IntelliTrace ile izleyin:</span><span class="sxs-lookup"><span data-stu-id="4115e-161">Follow these steps toodeploy hello service with IntelliTrace enabled:</span></span>

1. <span data-ttu-id="4115e-162">Azure SDK 1.3 veya üstü yüklü olduğunu onaylayın.</span><span class="sxs-lookup"><span data-stu-id="4115e-162">Confirm that Azure SDK 1.3 or later is installed.</span></span>
2. <span data-ttu-id="4115e-163">Visual Studio kullanarak Hello çözümü dağıtın.</span><span class="sxs-lookup"><span data-stu-id="4115e-163">Deploy hello solution by using Visual Studio.</span></span> <span data-ttu-id="4115e-164">Dağıtım sırasında hello denetleyin **.NET 4 rolleri için IntelliTrace'i etkinleştirin** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="4115e-164">During deployment, check hello **Enable IntelliTrace for .NET 4 roles** check box.</span></span>
3. <span data-ttu-id="4115e-165">Merhaba örneği başlatır, hello açın **Sunucu Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="4115e-165">Once hello instance starts, open hello **Server Explorer**.</span></span>
4. <span data-ttu-id="4115e-166">Merhaba genişletin **Azure\\bulut Hizmetleri** düğümü ve hello dağıtımını bulun.</span><span class="sxs-lookup"><span data-stu-id="4115e-166">Expand hello **Azure\\Cloud Services** node and locate hello deployment.</span></span>
5. <span data-ttu-id="4115e-167">Merhaba dağıtım hello rol örnekleri görene kadar genişletin.</span><span class="sxs-lookup"><span data-stu-id="4115e-167">Expand hello deployment until you see hello role instances.</span></span> <span data-ttu-id="4115e-168">Merhaba örnekleri birine sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4115e-168">Right-click on one of hello instances.</span></span>
6. <span data-ttu-id="4115e-169">Seçin **görünüm IntelliTrace günlüklerini**.</span><span class="sxs-lookup"><span data-stu-id="4115e-169">Choose **View IntelliTrace logs**.</span></span> <span data-ttu-id="4115e-170">Merhaba **IntelliTrace Özet** açılır.</span><span class="sxs-lookup"><span data-stu-id="4115e-170">hello **IntelliTrace Summary** will open.</span></span>
7. <span data-ttu-id="4115e-171">Merhaba özel durumlar hello Özet bölümünü bulun.</span><span class="sxs-lookup"><span data-stu-id="4115e-171">Locate hello exceptions section of hello summary.</span></span> <span data-ttu-id="4115e-172">Özel durumlar varsa, hello bölüm etiketli **özel durum verileri**.</span><span class="sxs-lookup"><span data-stu-id="4115e-172">If there are exceptions, hello section will be labeled **Exception Data**.</span></span>
8. <span data-ttu-id="4115e-173">Merhaba genişletin **özel durum verileri** ve Ara **System.IO.FileNotFoundException** benzer toohello aşağıdaki hatalar:</span><span class="sxs-lookup"><span data-stu-id="4115e-173">Expand hello **Exception Data** and look for **System.IO.FileNotFoundException** errors similar toohello following:</span></span>

![Özel durum verileri, eksik dosya veya derleme](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503390.png)

## <a name="address-missing-dlls-and-assemblies"></a><span data-ttu-id="4115e-175">Adres eksik DLL'ler ve derlemeler</span><span class="sxs-lookup"><span data-stu-id="4115e-175">Address missing DLLs and assemblies</span></span>
<span data-ttu-id="4115e-176">DLL ve derleme hatalarını eksik tooaddress şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="4115e-176">tooaddress missing DLL and assembly errors, follow these steps:</span></span>

1. <span data-ttu-id="4115e-177">Merhaba çözümü Visual Studio'da açın.</span><span class="sxs-lookup"><span data-stu-id="4115e-177">Open hello solution in Visual Studio.</span></span>
2. <span data-ttu-id="4115e-178">İçinde **Çözüm Gezgini**açın hello **başvuruları** klasör.</span><span class="sxs-lookup"><span data-stu-id="4115e-178">In **Solution Explorer**, open hello **References** folder.</span></span>
3. <span data-ttu-id="4115e-179">Merhaba hata tanımlanan hello derleme'yi tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4115e-179">Click hello assembly identified in hello error.</span></span>
4. <span data-ttu-id="4115e-180">Merhaba, **özellikleri** bölmesinde bulun **kopya yerel özellik** ve hello değeri çok**doğru**.</span><span class="sxs-lookup"><span data-stu-id="4115e-180">In hello **Properties** pane, locate **Copy Local property** and set hello value too**True**.</span></span>
5. <span data-ttu-id="4115e-181">Merhaba bulut hizmeti yeniden dağıtın.</span><span class="sxs-lookup"><span data-stu-id="4115e-181">Redeploy hello cloud service.</span></span>

<span data-ttu-id="4115e-182">Tüm hataları düzelttikten olduğunu doğruladıktan sonra hello denetlemeden hello hizmeti dağıtabilirsiniz **.NET 4 rolleri için IntelliTrace'i etkinleştirin** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="4115e-182">Once you have verified that all errors have been corrected, you can deploy hello service without checking hello **Enable IntelliTrace for .NET 4 roles** check box.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4115e-183">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4115e-183">Next steps</span></span>
<span data-ttu-id="4115e-184">Daha fazla bilgi görüntülemek [sorun giderme makalelerini](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) bulut Hizmetleri için.</span><span class="sxs-lookup"><span data-stu-id="4115e-184">View more [troubleshooting articles](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) for cloud services.</span></span>

<span data-ttu-id="4115e-185">tootroubleshoot bulut hizmet rolü nasıl sorunları Azure PaaS bilgisayar tanılama verilerini kullanarak toolearn bkz [Kevin Williamson'ın blog dizisini](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span><span class="sxs-lookup"><span data-stu-id="4115e-185">toolearn how tootroubleshoot cloud service role issues by using Azure PaaS computer diagnostics data, see [Kevin Williamson's blog series](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span></span>
