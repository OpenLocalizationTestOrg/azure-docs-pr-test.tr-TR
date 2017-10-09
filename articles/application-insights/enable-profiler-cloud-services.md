---
title: "Bulut Hizmetleri kaynak üzerinde Azure uygulama Öngörüler profil oluşturucu aaaEnable | Microsoft Docs"
description: "Nasıl tooset hello profil oluşturucu üzerinde bir ASP.NET uygulaması oluşturan bir Azure Cloud Services kaynak tarafından barındırılan öğrenin."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: bwren
ms.openlocfilehash: b9ac3bca513bf4518f44780389a9f2945f6ccc98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-application-insights-profiler-on-an-azure-cloud-services-resource"></a><span data-ttu-id="6e33f-103">Bir Azure Cloud Services kaynakta uygulama Öngörüler profil oluşturucu etkinleştir</span><span class="sxs-lookup"><span data-stu-id="6e33f-103">Enable Application Insights Profiler on an Azure Cloud Services resource</span></span>

<span data-ttu-id="6e33f-104">Bu kılavuz, nasıl ASP.NET uygulaması üzerinde Azure uygulama Öngörüler profil oluşturucu tooenable bir Azure Cloud Services kaynak tarafından barındırılan gösterir.</span><span class="sxs-lookup"><span data-stu-id="6e33f-104">This walkthrough demonstrates how tooenable Azure Application Insights Profiler on an ASP.NET application hosted by an Azure Cloud Services resource.</span></span> <span data-ttu-id="6e33f-105">Merhaba, Azure sanal makineler, sanal makine ölçek kümeleri ve Azure Service Fabric desteği örnekler.</span><span class="sxs-lookup"><span data-stu-id="6e33f-105">hello examples include support for Azure Virtual Machines, virtual machine scale sets, and Azure Service Fabric.</span></span> <span data-ttu-id="6e33f-106">Merhaba örnekler tüm hello Azure Resource Manager dağıtım modelini destekleyen şablonlarını kullanır.</span><span class="sxs-lookup"><span data-stu-id="6e33f-106">hello examples all rely on templates that support hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="6e33f-107">Merhaba dağıtım modeli hakkında daha fazla bilgi için gözden [Azure Resource Manager ve klasik dağıtım: dağıtım modellerini anlama ve hello kaynaklarınızın durumunu](/azure-resource-manager/resource-manager-deployment-model).</span><span class="sxs-lookup"><span data-stu-id="6e33f-107">For more information about hello deployment model, review [Azure Resource Manager vs. classic deployment: Understand deployment models and hello state of your resources](/azure-resource-manager/resource-manager-deployment-model).</span></span>

## <a name="overview"></a><span data-ttu-id="6e33f-108">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="6e33f-108">Overview</span></span>

<span data-ttu-id="6e33f-109">Diyagram aşağıdaki hello hello profil oluşturucu için Azure Cloud Services kaynakları nasıl çalıştığı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="6e33f-109">hello following diagram illustrates how hello profiler works for Azure Cloud Services resources.</span></span> <span data-ttu-id="6e33f-110">Bir Azure sanal makinesi bir örnek olarak kullanır.</span><span class="sxs-lookup"><span data-stu-id="6e33f-110">It uses an Azure virtual machine as an example.</span></span>

<span data-ttu-id="6e33f-111">![Genel Bakış](./media/enable-profiler-compute/overview.png) toocollect bilgi işlem ve ekranınızda için Azure portal Merhaba, hello Tanılama Aracı bileşeni hello Azure Cloud Services kaynaklar için yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="6e33f-111">![Overview](./media/enable-profiler-compute/overview.png) toocollect information for processing and display on hello Azure portal, you must install hello Diagnostics Agent component for hello Azure Cloud Services resources.</span></span> <span data-ttu-id="6e33f-112">Hello hello izlenecek geri kalanı rehberlik sağlar tooinstall ve hello Tanılama Aracı tooenable uygulama Öngörüler profil oluşturucu yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="6e33f-112">hello rest of hello walkthrough provides guidance on how tooinstall and configure hello Diagnostics Agent tooenable Application Insights Profiler.</span></span>

## <a name="prerequisites-for-hello-walkthrough"></a><span data-ttu-id="6e33f-113">Merhaba gözden geçirme için Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="6e33f-113">Prerequisites for hello walkthrough</span></span>

* <span data-ttu-id="6e33f-114">Hello profil oluşturucu aracıları hello VM'ler üzerinde yükleyen bir dağıtım Resource Manager şablonu ([WindowsVirtualMachine.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json)) veya ölçekleme kümeleri ([WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json)).</span><span class="sxs-lookup"><span data-stu-id="6e33f-114">A deployment Resource Manager template that installs hello profiler agents on hello VMs ([WindowsVirtualMachine.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json)) or scale sets ([WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json)).</span></span>

* <span data-ttu-id="6e33f-115">Profil oluşturma için etkinleştirilmiş bir Application Insights örneği.</span><span class="sxs-lookup"><span data-stu-id="6e33f-115">An Application Insights instance enabled for profiling.</span></span> <span data-ttu-id="6e33f-116">Yönergeler için bkz: [etkinleştirmek hello profil](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-profiler#enable-the-profiler).</span><span class="sxs-lookup"><span data-stu-id="6e33f-116">For instructions, see [Enable hello profile](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-profiler#enable-the-profiler).</span></span>

* <span data-ttu-id="6e33f-117">.NET framework 4.6.1 veya sonrası yüklü hello Azure Cloud Services kaynak hedefleyin.</span><span class="sxs-lookup"><span data-stu-id="6e33f-117">.NET Framework 4.6.1 or later installed on hello target Azure Cloud Services resource.</span></span>

## <a name="create-a-resource-group-in-your-azure-subscription"></a><span data-ttu-id="6e33f-118">Azure aboneliğinizde bir kaynak grubu oluştur</span><span class="sxs-lookup"><span data-stu-id="6e33f-118">Create a resource group in your Azure subscription</span></span>
<span data-ttu-id="6e33f-119">Aşağıdaki örnek hello nasıl toocreate bir kaynak grubunda bir PowerShell komut dosyası kullanarak gösterir:</span><span class="sxs-lookup"><span data-stu-id="6e33f-119">hello following example demonstrates how toocreate a resource group by using a PowerShell script:</span></span>

```
New-AzureRmResourceGroup -Name "Replace_With_Resource_Group_Name" -Location "Replace_With_Resource_Group_Location"
```

## <a name="create-an-application-insights-resource-in-hello-resource-group"></a><span data-ttu-id="6e33f-120">Merhaba kaynak grubunda bir Application Insights kaynağı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6e33f-120">Create an Application Insights resource in hello resource group</span></span>
<span data-ttu-id="6e33f-121">Merhaba üzerinde **Application Insights** dikey penceresinde, bu örnekte gösterildiği gibi kaynak için hello bilgileri girin:</span><span class="sxs-lookup"><span data-stu-id="6e33f-121">On hello **Application Insights** blade, enter hello information for your resource, as shown in this example:</span></span> 

![Uygulama Öngörüler dikey penceresi](./media/enable-profiler-compute/createai.png)

## <a name="apply-an-application-insights-instrumentation-key-in-hello-azure-resource-manager-template"></a><span data-ttu-id="6e33f-123">Bir Application Insights izleme anahtarı hello Azure Resource Manager Şablonu Uygula</span><span class="sxs-lookup"><span data-stu-id="6e33f-123">Apply an Application Insights instrumentation key in hello Azure Resource Manager template</span></span>

1. <span data-ttu-id="6e33f-124">Merhaba şablonu henüz yüklemediyseniz, indirin [GitHub](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json).</span><span class="sxs-lookup"><span data-stu-id="6e33f-124">If you haven't downloaded hello template yet, download it from [GitHub](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json).</span></span>

2. <span data-ttu-id="6e33f-125">Merhaba Application Insights anahtarını bulun.</span><span class="sxs-lookup"><span data-stu-id="6e33f-125">Find hello Application Insights key.</span></span>
   
   ![Merhaba anahtar konumu](./media/enable-profiler-compute/copyaikey.png)

3. <span data-ttu-id="6e33f-127">Merhaba şablon değeri değiştirin.</span><span class="sxs-lookup"><span data-stu-id="6e33f-127">Replace hello template value.</span></span>
   
   ![Merhaba şablonunda yerini değeri](./media/enable-profiler-compute/copyaikeytotemplate.png)

## <a name="create-an-azure-vm-toohost-hello-web-application"></a><span data-ttu-id="6e33f-129">Bir Azure VM toohost Merhaba web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="6e33f-129">Create an Azure VM toohost hello web application</span></span>
1. <span data-ttu-id="6e33f-130">Bir güvenli dize toosave hello parola oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6e33f-130">Create a secure string toosave hello password.</span></span>

   ```
   $password = ConvertTo-SecureString -String "Replace_With_Your_Password" -AsPlainText -Force
   ```

2. <span data-ttu-id="6e33f-131">Hello Azure Resource Manager şablonu dağıtma.</span><span class="sxs-lookup"><span data-stu-id="6e33f-131">Deploy hello Azure Resource Manager template.</span></span>

   <span data-ttu-id="6e33f-132">Resource Manager şablonu içeren hello PowerShell konsol toohello klasöründe Hello dizini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="6e33f-132">Change hello directory in hello PowerShell console toohello folder that contains your Resource Manager template.</span></span> <span data-ttu-id="6e33f-133">toodeploy hello şablonu, hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="6e33f-133">toodeploy hello template, run hello following command:</span></span>

   ```
   New-AzureRmResourceGroupDeployment -ResourceGroupName "Replace_With_Resource_Group_Name" -TemplateFile .\WindowsVirtualMachine.json -adminUsername "Replace_With_your_user_name" -adminPassword $password -dnsNameForPublicIP "Replace_WIth_your_DNS_Name" -Verbose
   ```

<span data-ttu-id="6e33f-134">Merhaba komut dosyası başarıyla çalıştıktan sonra adlandırılmış bir VM'nin bulmalısınız **MyWindowsVM** kaynak grubunuzdaki.</span><span class="sxs-lookup"><span data-stu-id="6e33f-134">After hello script runs successfully, you should find a VM named **MyWindowsVM** in your resource group.</span></span>

## <a name="configure-web-deploy-on-hello-vm"></a><span data-ttu-id="6e33f-135">Web dağıtımı hello VM üzerinde yapılandırma</span><span class="sxs-lookup"><span data-stu-id="6e33f-135">Configure Web Deploy on hello VM</span></span>
<span data-ttu-id="6e33f-136">Web uygulamanızı Visual Studio'dan yayımlamak için VM Web Dağıtımı'nin etkin olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="6e33f-136">Make sure that Web Deploy is enabled on your VM so you can publish your web application from Visual Studio.</span></span>

<span data-ttu-id="6e33f-137">tooinstall Web dağıtımı Webpı, kullanarak el ile bir VM'de bkz [yükleme ve IIS 8. 0 veya daha sonra Web dağıtımı yapılandırma](https://docs.microsoft.com/en-us/iis/install/installing-publishing-technologies/installing-and-configuring-web-deploy-on-iis-80-or-later).</span><span class="sxs-lookup"><span data-stu-id="6e33f-137">tooinstall Web Deploy on a VM manually via WebPI, see [Installing and Configuring Web Deploy on IIS 8.0 or Later](https://docs.microsoft.com/en-us/iis/install/installing-publishing-technologies/installing-and-configuring-web-deploy-on-iis-80-or-later).</span></span> <span data-ttu-id="6e33f-138">Nasıl bir örneği için bir Azure Resource Manager şablonu kullanarak Web dağıtımı yükleme tooautomate bkz [oluşturun, yapılandırma ve bir web uygulaması tooan Azure VM dağıtma](https://azure.microsoft.com/en-us/resources/templates/201-web-app-vm-dsc/).</span><span class="sxs-lookup"><span data-stu-id="6e33f-138">For an example of how tooautomate installing Web Deploy by using an Azure Resource Manager template, see [Create, configure, and deploy a web application tooan Azure VM](https://azure.microsoft.com/en-us/resources/templates/201-web-app-vm-dsc/).</span></span>

<span data-ttu-id="6e33f-139">Bir ASP.NET MVC uygulaması dağıtıyorsanız, tooServer Yöneticisi, select Git **rol ve Özellik Ekle** > **Web sunucusu (IIS)** > **Web sunucusu**  >  **Uygulama geliştirme**ve ASP.NET 4.5 sunucunuzda etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="6e33f-139">If you are deploying an ASP.NET MVC application, go tooServer Manager, select **Add Roles and Features** > **Web Server (IIS)** > **Web Server** > **Application Development**, and enable ASP.NET 4.5 on your server.</span></span>

![ASP.NET Ekle](./media/enable-profiler-compute/addaspnet45.png)

## <a name="install-hello-azure-application-insights-sdk-for-your-project"></a><span data-ttu-id="6e33f-141">Projeniz için Hello Azure Application Insights SDK'sı yükleyin</span><span class="sxs-lookup"><span data-stu-id="6e33f-141">Install hello Azure Application Insights SDK for your project</span></span>
1. <span data-ttu-id="6e33f-142">ASP.NET web uygulamanızı Visual Studio'da açın.</span><span class="sxs-lookup"><span data-stu-id="6e33f-142">Open your ASP.NET web application in Visual Studio.</span></span>

2. <span data-ttu-id="6e33f-143">Merhaba projesine sağ tıklatın ve **Ekle** > **bağlantılı Hizmetler**.</span><span class="sxs-lookup"><span data-stu-id="6e33f-143">Right-click hello project and select **Add** > **Connected Services**.</span></span>

3. <span data-ttu-id="6e33f-144">Seçin **Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="6e33f-144">Select **Application Insights**.</span></span>

4. <span data-ttu-id="6e33f-145">Merhaba sayfasındaki Hello yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="6e33f-145">Follow hello instructions on hello page.</span></span> <span data-ttu-id="6e33f-146">Daha önce oluşturduğunuz hello Application Insights kaynağı seçin.</span><span class="sxs-lookup"><span data-stu-id="6e33f-146">Select hello Application Insights resource that you created earlier.</span></span>

5. <span data-ttu-id="6e33f-147">Select hello **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="6e33f-147">Select hello **Register** button.</span></span>


## <a name="publish-hello-project-tooan-azure-vm"></a><span data-ttu-id="6e33f-148">Yayımlama Hello proje tooan Azure VM</span><span class="sxs-lookup"><span data-stu-id="6e33f-148">Publish hello project tooan Azure VM</span></span>
<span data-ttu-id="6e33f-149">Bir uygulama tooan Azure VM birkaç yolu toopublish vardır.</span><span class="sxs-lookup"><span data-stu-id="6e33f-149">There are several ways toopublish an application tooan Azure VM.</span></span> <span data-ttu-id="6e33f-150">Visual Studio 2017 toouse bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="6e33f-150">One way is toouse Visual Studio 2017.</span></span>

1. <span data-ttu-id="6e33f-151">Merhaba projesine sağ tıklatın ve **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="6e33f-151">Right-click hello project and select **Publish**.</span></span>

2. <span data-ttu-id="6e33f-152">Seçin **Microsoft Azure sanal makineleri** hello olarak hedef yayımlama ve hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="6e33f-152">Select **Microsoft Azure Virtual Machines** as hello publish target and follow hello steps.</span></span>

   ![Yayımlama FromVS](./media/enable-profiler-compute/publishtoVM.png)

3. <span data-ttu-id="6e33f-154">Bir yük testi karşı uygulamanızı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="6e33f-154">Run a load test against your application.</span></span> <span data-ttu-id="6e33f-155">Merhaba Application Insights örnek portal Web sayfasında sonuçları görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="6e33f-155">You should see results on hello Application Insights instance portal webpage.</span></span>


## <a name="enable-hello-profiler"></a><span data-ttu-id="6e33f-156">Hello profil oluşturucu etkinleştir</span><span class="sxs-lookup"><span data-stu-id="6e33f-156">Enable hello profiler</span></span>
1. <span data-ttu-id="6e33f-157">Tooyour Application Insights Git **performans** dikey penceresinde ve select **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="6e33f-157">Go tooyour Application Insights **Performance** blade and select **Configure**.</span></span>
   
   ![Yapılandırma simgesi](./media/enable-profiler-compute/enableprofiler1.png)
 
2. <span data-ttu-id="6e33f-159">Seçin **etkinleştirmek profil oluşturucu**.</span><span class="sxs-lookup"><span data-stu-id="6e33f-159">Select **Enable Profiler**.</span></span>
   
   ![Profil Oluşturucu simgesi etkinleştir](./media/enable-profiler-compute/enableprofiler2.png)

## <a name="add-a-performance-test-tooyour-application"></a><span data-ttu-id="6e33f-161">Performans testi tooyour uygulama ekleme</span><span class="sxs-lookup"><span data-stu-id="6e33f-161">Add a performance test tooyour application</span></span>
<span data-ttu-id="6e33f-162">Uygulama Öngörüler Profil Oluşturucusu'nda görüntülenen bazı örnek veri toobe topladığımız için şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="6e33f-162">Follow these steps so we can collect some sample data toobe displayed in Application Insights Profiler:</span></span>

1. <span data-ttu-id="6e33f-163">Daha önce oluşturduğunuz toohello Application Insights kaynağı göz atın.</span><span class="sxs-lookup"><span data-stu-id="6e33f-163">Browse toohello Application Insights resource that you created earlier.</span></span> 

2. <span data-ttu-id="6e33f-164">Toohello Git **kullanılabilirlik** dikey ve web istekleri tooyour uygulama URL'si gönderir bir performans testi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6e33f-164">Go toohello **Availability** blade and add a performance test that sends web requests tooyour application URL.</span></span> 

   ![Performans testi ekleyin](./media/enable-profiler-compute/AvailabilityTest.png)

## <a name="view-your-performance-data"></a><span data-ttu-id="6e33f-166">Performans verileri görünümü</span><span class="sxs-lookup"><span data-stu-id="6e33f-166">View your performance data</span></span>

1. <span data-ttu-id="6e33f-167">Hello profil oluşturucu toocollect 10-15 dakika bekleyin ve hello verileri analiz edin.</span><span class="sxs-lookup"><span data-stu-id="6e33f-167">Wait 10-15 minutes for hello profiler toocollect and analyze hello data.</span></span> 

2. <span data-ttu-id="6e33f-168">Toohello Git **performans** dikey penceresinde nasıl uygulamanızı gerçekleştirip yük altında olduğunda, Görünüm ve Application Insights kaynağı.</span><span class="sxs-lookup"><span data-stu-id="6e33f-168">Go toohello **Performance** blade in your Application Insights resource and view how your application is performing when it's under load.</span></span>

   ![Performans görüntüleme](./media/enable-profiler-compute/aiperformance.png)

3. <span data-ttu-id="6e33f-170">Select hello simgesi altında **örnekler** tooopen hello **izleme görünümü** dikey.</span><span class="sxs-lookup"><span data-stu-id="6e33f-170">Select hello icon under **Examples** tooopen hello **Trace View** blade.</span></span>

   ![Merhaba izleme görünümü dikey penceresini açma](./media/enable-profiler-compute/traceview.png)


## <a name="work-with-an-existing-template"></a><span data-ttu-id="6e33f-172">Var olan bir şablonu ile çalışma</span><span class="sxs-lookup"><span data-stu-id="6e33f-172">Work with an existing template</span></span>

1. <span data-ttu-id="6e33f-173">Hello Azure tanılama kaynak bildirimi dağıtım şablonunuzda bulun.</span><span class="sxs-lookup"><span data-stu-id="6e33f-173">Locate hello Azure Diagnostics resource declaration in your deployment template.</span></span>
   
   <span data-ttu-id="6e33f-174">Bir bildirim yoksa, aşağıdaki örneğine hello hello bildiriminde benzeyen bir oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6e33f-174">If you don't have a declaration, you can create one that resembles hello declaration in hello following example.</span></span> <span data-ttu-id="6e33f-175">Merhaba hello şablondan güncelleştirebilirsiniz [Azure kaynak Gezgini Web sitesi](https://resources.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6e33f-175">You can update hello template from hello [Azure Resource Explorer website](https://resources.azure.com).</span></span>

2. <span data-ttu-id="6e33f-176">Değişiklik hello yayımcıdan `Microsoft.Azure.Diagnostics` çok`AIP.Diagnostics.Test`.</span><span class="sxs-lookup"><span data-stu-id="6e33f-176">Change hello publisher from `Microsoft.Azure.Diagnostics` too`AIP.Diagnostics.Test`.</span></span>

3. <span data-ttu-id="6e33f-177">İçin `typeHandlerVersion`, kullanmak `0.0`.</span><span class="sxs-lookup"><span data-stu-id="6e33f-177">For `typeHandlerVersion`, use `0.0`.</span></span>

4. <span data-ttu-id="6e33f-178">Olduğundan emin olun `autoUpgradeMinorVersion` çok ayarlanır`true`.</span><span class="sxs-lookup"><span data-stu-id="6e33f-178">Make sure that `autoUpgradeMinorVersion` is set too`true`.</span></span>

5. <span data-ttu-id="6e33f-179">Merhaba yeni Ekle `ApplicationInsightsProfiler` hello havuz örneğinde `WadCfg` hello aşağıdaki örnekte gösterildiği gibi ayarları nesnesi:</span><span class="sxs-lookup"><span data-stu-id="6e33f-179">Add hello new `ApplicationInsightsProfiler` sink instance in hello `WadCfg` settings object, as shown in hello following example:</span></span>

```
"resources": [
        {
          "type": "extensions",
          "name": "Microsoft.Insights.VMDiagnosticsSettings",
          "apiVersion": "2016-03-30",
          "properties": {
            "publisher": "AIP.Diagnostics.Test",
            "type": "IaaSDiagnostics",
            "typeHandlerVersion": "0.0",
            "autoUpgradeMinorVersion": true,
            "settings": {
              "WadCfg": {
                "SinksConfig": {
                  "Sink": [
                    {
                      "name": "Give a descriptive short name. E.g.: MyApplicationInsightsProfilerSink",
                      "ApplicationInsightsProfiler": "Enter hello Application Insights instance instrumentation key guid here"
                    }
                  ]
                },
                "DiagnosticMonitorConfiguration": {
                    ...
                }
                ...
              }
              ...
            }
            ...
          }
          ...
]
```

## <a name="enable-hello-profiler-on-virtual-machine-scale-sets"></a><span data-ttu-id="6e33f-180">Sanal makine ölçek kümeleri üzerinde Hello profil oluşturucu etkinleştir</span><span class="sxs-lookup"><span data-stu-id="6e33f-180">Enable hello profiler on virtual machine scale sets</span></span>
<span data-ttu-id="6e33f-181">toosee tooenable hello nasıl profil oluşturucu, indirme hello [WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json) şablonu.</span><span class="sxs-lookup"><span data-stu-id="6e33f-181">toosee how tooenable hello profiler, download hello [WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json) template.</span></span> <span data-ttu-id="6e33f-182">Merhaba aynı hello sanal makine ölçek kümesi için bir VM şablonu toohello tanılama uzantısını kaynak değişiklikleri uygulayın.</span><span class="sxs-lookup"><span data-stu-id="6e33f-182">Apply hello same changes in a VM template toohello diagnostics extension resource for hello virtual machine scale set.</span></span>

<span data-ttu-id="6e33f-183">Merhaba ölçek kümesindeki her örneği erişim toohello sahip olduğundan emin olun Internet.</span><span class="sxs-lookup"><span data-stu-id="6e33f-183">Make sure that each instance in hello scale set has access toohello internet.</span></span> <span data-ttu-id="6e33f-184">Hello Profil Oluşturucu aracı, sonra tooApplication Öngörüler görüntüleme ve analiz için toplanan hello örnekleri gönderebilir.</span><span class="sxs-lookup"><span data-stu-id="6e33f-184">hello Profiler Agent can then send hello collected samples tooApplication Insights for display and analysis.</span></span>

## <a name="enable-hello-profiler-on-service-fabric-applications"></a><span data-ttu-id="6e33f-185">Service Fabric uygulamaları Hello profil oluşturucu etkinleştir</span><span class="sxs-lookup"><span data-stu-id="6e33f-185">Enable hello profiler on Service Fabric applications</span></span>
1. <span data-ttu-id="6e33f-186">Sağlama hello hello Profil Oluşturucu aracı yükleyen Service Fabric kümesi toohave hello Azure tanılama uzantısını.</span><span class="sxs-lookup"><span data-stu-id="6e33f-186">Provision hello Service Fabric cluster toohave hello Azure Diagnostics extension that installs hello Profiler Agent.</span></span>

2. <span data-ttu-id="6e33f-187">Merhaba projesinde Hello Application Insights SDK'sı yükleyin ve hello Application Insights anahtar yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="6e33f-187">Install hello Application Insights SDK in hello project and configure hello Application Insights key.</span></span>

3. <span data-ttu-id="6e33f-188">Uygulama kodu tooinstrument telemetri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6e33f-188">Add application code tooinstrument telemetry.</span></span>

### <a name="provision-hello-service-fabric-cluster-toohave-hello-azure-diagnostics-extension-that-installs-hello-profiler-agent"></a><span data-ttu-id="6e33f-189">Sağlama hello Service Fabric kümesi toohave hello hello Profil Oluşturucu aracı yükler Azure tanılama uzantısını</span><span class="sxs-lookup"><span data-stu-id="6e33f-189">Provision hello Service Fabric cluster toohave hello Azure Diagnostics extension that installs hello Profiler Agent</span></span>
<span data-ttu-id="6e33f-190">Service Fabric kümesi güvenli veya güvenli olmayan olabilir.</span><span class="sxs-lookup"><span data-stu-id="6e33f-190">A Service Fabric cluster can be secure or non-secure.</span></span> <span data-ttu-id="6e33f-191">Erişim için bir sertifika gerektirmez şekilde güvenli olmayan bir ağ geçidi küme toobe ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6e33f-191">You can set one gateway cluster toobe non-secure so it doesn't require a certificate for access.</span></span> <span data-ttu-id="6e33f-192">İş mantığı ve verileri konak kümeleri güvenli olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="6e33f-192">Clusters that host business logic and data should be secure.</span></span> <span data-ttu-id="6e33f-193">Hello profil oluşturucu hem güvenli hem de güvenli olmayan Service Fabric kümeleri üzerinde etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6e33f-193">You can enable hello profiler on both secure and non-secure Service Fabric clusters.</span></span> <span data-ttu-id="6e33f-194">Bu kılavuzda, güvenli olmayan bir küme gerekli tooenable hello profil oluşturucu hangi değişiklikleri olan bir örnek tooexplain kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6e33f-194">This walkthrough uses a non-secure cluster as an example tooexplain what changes are required tooenable hello profiler.</span></span> <span data-ttu-id="6e33f-195">Merhaba güvenli bir kümede sağlayabilirsiniz aynı şekilde.</span><span class="sxs-lookup"><span data-stu-id="6e33f-195">You can provision a secure cluster in hello same way.</span></span>

1. <span data-ttu-id="6e33f-196">Karşıdan [ServiceFabricCluster.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/ServiceFabricCluster.json).</span><span class="sxs-lookup"><span data-stu-id="6e33f-196">Download [ServiceFabricCluster.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/ServiceFabricCluster.json).</span></span> <span data-ttu-id="6e33f-197">VM'ler ve sanal makine ölçek kümeleri için yaptığınız gibi değiştirmek `Application_Insights_Key` Application Insights anahtarınız ile:</span><span class="sxs-lookup"><span data-stu-id="6e33f-197">As you did for VMs and virtual machine scale sets, replace `Application_Insights_Key` with your Application Insights key:</span></span>

   ```
   "publisher": "AIP.Diagnostics.Test",
                 "settings": {
                   "WadCfg": {
                     "SinksConfig": {
                       "Sink": [
                         {
                           "name": "MyApplicationInsightsProfilerSinkVMSS",
                           "ApplicationInsightsProfiler": "[Application_Insights_Key]"
                         }
                       ]
                     },
   ```

2. <span data-ttu-id="6e33f-198">Merhaba şablonu, bir PowerShell komut dosyası kullanarak dağıtın:</span><span class="sxs-lookup"><span data-stu-id="6e33f-198">Deploy hello template by using a PowerShell script:</span></span>

   ```
   Login-AzureRmAccount
   New-AzureRmResourceGroup -Name [Your_Resource_Group_Name] -Location [Your_Resource_Group_Location] -Verbose -Force
   New-AzureRmResourceGroupDeployment -Name [Choose_An_Arbitrary_Name] -ResourceGroupName [Your_Resource_Group_Name] -TemplateFile [Path_To_Your_Template]

   ```

### <a name="install-hello-application-insights-sdk-in-hello-project-and-configure-hello-application-insights-key"></a><span data-ttu-id="6e33f-199">Merhaba projesinde Hello Application Insights SDK'sı yükleyin ve hello Application Insights anahtar yapılandırın</span><span class="sxs-lookup"><span data-stu-id="6e33f-199">Install hello Application Insights SDK in hello project and configure hello Application Insights key</span></span>
<span data-ttu-id="6e33f-200">Hello Hello Application Insights SDK'sı yükleme [NuGet paketi](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span><span class="sxs-lookup"><span data-stu-id="6e33f-200">Install hello Application Insights SDK from hello [NuGet package](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span></span> <span data-ttu-id="6e33f-201">2.3 ya da daha yeni bir kararlı sürümünü yüklediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="6e33f-201">Make sure that you install a stable version, 2.3 or later.</span></span> 

<span data-ttu-id="6e33f-202">Application Insights projelerinizde yapılandırma hakkında daha fazla bilgi için bkz: [kullanarak Service Fabric Application Insights ile](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/blob/dev/appinsights/ApplicationInsights.md).</span><span class="sxs-lookup"><span data-stu-id="6e33f-202">For information about configuring Application Insights in your projects, see [Using Service Fabric with Application Insights](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/blob/dev/appinsights/ApplicationInsights.md).</span></span>

### <a name="add-application-code-tooinstrument-telemetry"></a><span data-ttu-id="6e33f-203">Uygulama kodu tooinstrument telemetri ekleyin</span><span class="sxs-lookup"><span data-stu-id="6e33f-203">Add application code tooinstrument telemetry</span></span>
1. <span data-ttu-id="6e33f-204">İçin herhangi bir tooinstrument istediğiniz kod kullanarak bir ekleme deyimi çevresinde.</span><span class="sxs-lookup"><span data-stu-id="6e33f-204">For any piece of code that you want tooinstrument, add a using statement around it.</span></span> 

   <span data-ttu-id="6e33f-205">Aşağıdaki örneğine hello hello `RunAsync` yöntemi bazı iş yapılması ve hello `telemetryClient` sınıfı başladıktan sonra hello telemetri yakalar.</span><span class="sxs-lookup"><span data-stu-id="6e33f-205">In hello following  example, hello `RunAsync` method is doing some work, and hello `telemetryClient` class captures hello telemetry after it starts.</span></span> <span data-ttu-id="6e33f-206">Merhaba olay hello uygulama arasında benzersiz bir ad gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="6e33f-206">hello event needs a unique name across hello application.</span></span>

   ```
   protected override async Task RunAsync(CancellationToken cancellationToken)
       {
           // TODO: Replace hello following sample code with your own logic
           //       or remove this RunAsync override if it's not needed in your service.

           while (true)
           {
               using( var operation = telemetryClient.StartOperation<RequestTelemetry>("[Insert_Event_Unique_Name]"))
               {
                   cancellationToken.ThrowIfCancellationRequested();

                   ++this.iterations;

                   ServiceEventSource.Current.ServiceMessage(this.Context, "Working-{0}", this.iterations);

                   await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
               }

           }
       }
   ```

2. <span data-ttu-id="6e33f-207">Uygulama toohello Service Fabric kümesi dağıtın.</span><span class="sxs-lookup"><span data-stu-id="6e33f-207">Deploy your application toohello Service Fabric cluster.</span></span> <span data-ttu-id="6e33f-208">Merhaba uygulama toorun için 10 dakika bekleyin.</span><span class="sxs-lookup"><span data-stu-id="6e33f-208">Wait for hello app toorun for 10 minutes.</span></span> <span data-ttu-id="6e33f-209">Daha iyi efekti hello uygulama üzerinde bir yük testi çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6e33f-209">For better effect, you can run a load test on hello app.</span></span> <span data-ttu-id="6e33f-210">Git toohello Application Insights Portalı'nın **performans** dikey penceresinde ve profil oluşturma izlemeleri görünür örnekleri görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="6e33f-210">Go toohello Application Insights portal's **Performance** blade, and you should see examples of profiling traces appear.</span></span>

<!---
Commenting out these sections for now
## Enable hello Profiler on Cloud Services applications
[TODO]
## Enable hello Profiler on classic Azure Virtual Machines
[TODO]
## Enable hello Profiler on on-premise servers
[TODO]
--->

## <a name="next-steps"></a><span data-ttu-id="6e33f-211">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6e33f-211">Next steps</span></span>

- <span data-ttu-id="6e33f-212">Profil Oluşturucu sorunlarını giderme konusunda Yardım bulmak [sorun giderme profil oluşturucu](app-insights-profiler.md#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="6e33f-212">Find help with troubleshooting profiler issues in [Profiler troubleshooting](app-insights-profiler.md#troubleshooting).</span></span>

- <span data-ttu-id="6e33f-213">Hello Profil Oluşturucusu'nda hakkında daha fazla bilgiyi [uygulama Öngörüler profil oluşturucu](app-insights-profiler.md).</span><span class="sxs-lookup"><span data-stu-id="6e33f-213">Read more about hello profiler in [Application Insights Profiler](app-insights-profiler.md).</span></span>
