---
title: "Bulut Hizmetleri kaynak Azure uygulama Öngörüler profil oluşturucu etkinleştirme | Microsoft Docs"
description: "Bir Azure Cloud Services kaynak tarafından barındırılan bir ASP.NET uygulamasına profil oluşturucu ayarlanacağını öğrenin."
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
ms.openlocfilehash: 5ff062ac81dca9d8b205cec966d2a9c11a4005b6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="enable-application-insights-profiler-on-an-azure-cloud-services-resource"></a><span data-ttu-id="402dc-103">Bir Azure Cloud Services kaynakta uygulama Öngörüler profil oluşturucu etkinleştir</span><span class="sxs-lookup"><span data-stu-id="402dc-103">Enable Application Insights Profiler on an Azure Cloud Services resource</span></span>

<span data-ttu-id="402dc-104">Bu kılavuz, Azure uygulama Öngörüler profil oluşturucu Azure Cloud Services kaynak tarafından barındırılan bir ASP.NET uygulamasını etkinleştirmek gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="402dc-104">This walkthrough demonstrates how to enable Azure Application Insights Profiler on an ASP.NET application hosted by an Azure Cloud Services resource.</span></span> <span data-ttu-id="402dc-105">Azure sanal makineler, sanal makine ölçek kümeleri ve Azure Service Fabric desteği örnekler.</span><span class="sxs-lookup"><span data-stu-id="402dc-105">The examples include support for Azure Virtual Machines, virtual machine scale sets, and Azure Service Fabric.</span></span> <span data-ttu-id="402dc-106">Tüm örnekler Azure Resource Manager dağıtım modelini destekleyen şablonlarını kullanır.</span><span class="sxs-lookup"><span data-stu-id="402dc-106">The examples all rely on templates that support the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="402dc-107">Dağıtım modeli hakkında daha fazla bilgi için gözden [Azure Resource Manager ve klasik dağıtım: dağıtım modelleri ve kaynaklarınızın durumunu anlamak](/azure-resource-manager/resource-manager-deployment-model).</span><span class="sxs-lookup"><span data-stu-id="402dc-107">For more information about the deployment model, review [Azure Resource Manager vs. classic deployment: Understand deployment models and the state of your resources](/azure-resource-manager/resource-manager-deployment-model).</span></span>

## <a name="overview"></a><span data-ttu-id="402dc-108">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="402dc-108">Overview</span></span>

<span data-ttu-id="402dc-109">Aşağıdaki diyagramda, Azure Cloud Services kaynaklar için profil oluşturucu nasıl çalıştığı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="402dc-109">The following diagram illustrates how the profiler works for Azure Cloud Services resources.</span></span> <span data-ttu-id="402dc-110">Bir Azure sanal makinesi bir örnek olarak kullanır.</span><span class="sxs-lookup"><span data-stu-id="402dc-110">It uses an Azure virtual machine as an example.</span></span>

<span data-ttu-id="402dc-111">![Genel Bakış](./media/enable-profiler-compute/overview.png) Azure Portalı'nda işleme ve görüntü bilgi toplamak için Azure Cloud Services kaynaklar için tanılama aracı bileşeni yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="402dc-111">![Overview](./media/enable-profiler-compute/overview.png) To collect information for processing and display on the Azure portal, you must install the Diagnostics Agent component for the Azure Cloud Services resources.</span></span> <span data-ttu-id="402dc-112">Kalan örnekler yüklemek ve uygulama Öngörüler profil oluşturucu etkinleştirmek için tanılama aracısını yapılandırmak hakkında yönergeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="402dc-112">The rest of the walkthrough provides guidance on how to install and configure the Diagnostics Agent to enable Application Insights Profiler.</span></span>

## <a name="prerequisites-for-the-walkthrough"></a><span data-ttu-id="402dc-113">İzlenecek yol için Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="402dc-113">Prerequisites for the walkthrough</span></span>

* <span data-ttu-id="402dc-114">Profil Oluşturucu aracıları sanal makinelerin yükleyen bir dağıtım Resource Manager şablonu ([WindowsVirtualMachine.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json)) veya ölçekleme kümeleri ([WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json)).</span><span class="sxs-lookup"><span data-stu-id="402dc-114">A deployment Resource Manager template that installs the profiler agents on the VMs ([WindowsVirtualMachine.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json)) or scale sets ([WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json)).</span></span>

* <span data-ttu-id="402dc-115">Profil oluşturma için etkinleştirilmiş bir Application Insights örneği.</span><span class="sxs-lookup"><span data-stu-id="402dc-115">An Application Insights instance enabled for profiling.</span></span> <span data-ttu-id="402dc-116">Yönergeler için bkz: [profilini etkinleştirmek](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-profiler#enable-the-profiler).</span><span class="sxs-lookup"><span data-stu-id="402dc-116">For instructions, see [Enable the profile](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-profiler#enable-the-profiler).</span></span>

* <span data-ttu-id="402dc-117">.NET framework 4.6.1 veya hedef Azure Cloud Services kaynak sonraki bir sürümü yüklü.</span><span class="sxs-lookup"><span data-stu-id="402dc-117">.NET Framework 4.6.1 or later installed on the target Azure Cloud Services resource.</span></span>

## <a name="create-a-resource-group-in-your-azure-subscription"></a><span data-ttu-id="402dc-118">Azure aboneliğinizde bir kaynak grubu oluştur</span><span class="sxs-lookup"><span data-stu-id="402dc-118">Create a resource group in your Azure subscription</span></span>
<span data-ttu-id="402dc-119">Aşağıdaki örnek, bir PowerShell komut dosyası kullanarak bir kaynak grubu oluşturmak gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="402dc-119">The following example demonstrates how to create a resource group by using a PowerShell script:</span></span>

```
New-AzureRmResourceGroup -Name "Replace_With_Resource_Group_Name" -Location "Replace_With_Resource_Group_Location"
```

## <a name="create-an-application-insights-resource-in-the-resource-group"></a><span data-ttu-id="402dc-120">Kaynak grubunda bir Application Insights kaynağı oluşturma</span><span class="sxs-lookup"><span data-stu-id="402dc-120">Create an Application Insights resource in the resource group</span></span>
<span data-ttu-id="402dc-121">Üzerinde **Application Insights** dikey penceresinde, bu örnekte gösterildiği gibi kaynak için bilgileri girin:</span><span class="sxs-lookup"><span data-stu-id="402dc-121">On the **Application Insights** blade, enter the information for your resource, as shown in this example:</span></span> 

![Uygulama Öngörüler dikey penceresi](./media/enable-profiler-compute/createai.png)

## <a name="apply-an-application-insights-instrumentation-key-in-the-azure-resource-manager-template"></a><span data-ttu-id="402dc-123">Azure Resource Manager şablonunda bir Application Insights izleme anahtarı Uygula</span><span class="sxs-lookup"><span data-stu-id="402dc-123">Apply an Application Insights instrumentation key in the Azure Resource Manager template</span></span>

1. <span data-ttu-id="402dc-124">Şablon henüz yüklemediyseniz, indirin [GitHub](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json).</span><span class="sxs-lookup"><span data-stu-id="402dc-124">If you haven't downloaded the template yet, download it from [GitHub](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json).</span></span>

2. <span data-ttu-id="402dc-125">Application Insights anahtarını bulun.</span><span class="sxs-lookup"><span data-stu-id="402dc-125">Find the Application Insights key.</span></span>
   
   ![Anahtar konumu](./media/enable-profiler-compute/copyaikey.png)

3. <span data-ttu-id="402dc-127">Şablon değeri değiştirin.</span><span class="sxs-lookup"><span data-stu-id="402dc-127">Replace the template value.</span></span>
   
   ![Şablonda yerini değeri](./media/enable-profiler-compute/copyaikeytotemplate.png)

## <a name="create-an-azure-vm-to-host-the-web-application"></a><span data-ttu-id="402dc-129">Web uygulamasını barındırmak için bir Azure VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="402dc-129">Create an Azure VM to host the web application</span></span>
1. <span data-ttu-id="402dc-130">Parola kaydetmek için güvenli bir dize oluşturun.</span><span class="sxs-lookup"><span data-stu-id="402dc-130">Create a secure string to save the password.</span></span>

   ```
   $password = ConvertTo-SecureString -String "Replace_With_Your_Password" -AsPlainText -Force
   ```

2. <span data-ttu-id="402dc-131">Azure Resource Manager şablonu dağıtma.</span><span class="sxs-lookup"><span data-stu-id="402dc-131">Deploy the Azure Resource Manager template.</span></span>

   <span data-ttu-id="402dc-132">PowerShell konsolundaki dizin Kaynak Yöneticisi şablonunuzu içeren klasör olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="402dc-132">Change the directory in the PowerShell console to the folder that contains your Resource Manager template.</span></span> <span data-ttu-id="402dc-133">Şablonu dağıtmak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="402dc-133">To deploy the template, run the following command:</span></span>

   ```
   New-AzureRmResourceGroupDeployment -ResourceGroupName "Replace_With_Resource_Group_Name" -TemplateFile .\WindowsVirtualMachine.json -adminUsername "Replace_With_your_user_name" -adminPassword $password -dnsNameForPublicIP "Replace_WIth_your_DNS_Name" -Verbose
   ```

<span data-ttu-id="402dc-134">Komut dosyası başarıyla çalıştıktan sonra adlandırılmış bir VM'nin bulmalısınız **MyWindowsVM** kaynak grubunuzdaki.</span><span class="sxs-lookup"><span data-stu-id="402dc-134">After the script runs successfully, you should find a VM named **MyWindowsVM** in your resource group.</span></span>

## <a name="configure-web-deploy-on-the-vm"></a><span data-ttu-id="402dc-135">Web yapılandırma VM dağıtma</span><span class="sxs-lookup"><span data-stu-id="402dc-135">Configure Web Deploy on the VM</span></span>
<span data-ttu-id="402dc-136">Web uygulamanızı Visual Studio'dan yayımlamak için VM Web Dağıtımı'nin etkin olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="402dc-136">Make sure that Web Deploy is enabled on your VM so you can publish your web application from Visual Studio.</span></span>

<span data-ttu-id="402dc-137">Web dağıtımı bir VM'de Webpı aracılığıyla el ile yüklemek için bkz [yükleme ve IIS 8. 0 veya daha sonra Web dağıtımı yapılandırma](https://docs.microsoft.com/en-us/iis/install/installing-publishing-technologies/installing-and-configuring-web-deploy-on-iis-80-or-later).</span><span class="sxs-lookup"><span data-stu-id="402dc-137">To install Web Deploy on a VM manually via WebPI, see [Installing and Configuring Web Deploy on IIS 8.0 or Later](https://docs.microsoft.com/en-us/iis/install/installing-publishing-technologies/installing-and-configuring-web-deploy-on-iis-80-or-later).</span></span> <span data-ttu-id="402dc-138">Bir Azure Resource Manager şablonu kullanarak Web dağıtımı yükleme otomatik hale getirmek nasıl bir örnek için bkz: [oluşturma, yapılandırma ve bir Azure VM için bir web uygulaması dağıtma](https://azure.microsoft.com/en-us/resources/templates/201-web-app-vm-dsc/).</span><span class="sxs-lookup"><span data-stu-id="402dc-138">For an example of how to automate installing Web Deploy by using an Azure Resource Manager template, see [Create, configure, and deploy a web application to an Azure VM](https://azure.microsoft.com/en-us/resources/templates/201-web-app-vm-dsc/).</span></span>

<span data-ttu-id="402dc-139">Git Sunucu Yöneticisi, bir ASP.NET MVC uygulaması dağıtıyorsanız seçin **rol ve Özellik Ekle** > **Web sunucusu (IIS)** > **Web sunucusu**  >  **Uygulama geliştirme**ve ASP.NET 4.5 sunucunuzda etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="402dc-139">If you are deploying an ASP.NET MVC application, go to Server Manager, select **Add Roles and Features** > **Web Server (IIS)** > **Web Server** > **Application Development**, and enable ASP.NET 4.5 on your server.</span></span>

![ASP.NET Ekle](./media/enable-profiler-compute/addaspnet45.png)

## <a name="install-the-azure-application-insights-sdk-for-your-project"></a><span data-ttu-id="402dc-141">Projeniz için Azure Application Insights SDK'sı yükleyin</span><span class="sxs-lookup"><span data-stu-id="402dc-141">Install the Azure Application Insights SDK for your project</span></span>
1. <span data-ttu-id="402dc-142">ASP.NET web uygulamanızı Visual Studio'da açın.</span><span class="sxs-lookup"><span data-stu-id="402dc-142">Open your ASP.NET web application in Visual Studio.</span></span>

2. <span data-ttu-id="402dc-143">Projeye sağ tıklayın ve seçin **Ekle** > **bağlantılı Hizmetler**.</span><span class="sxs-lookup"><span data-stu-id="402dc-143">Right-click the project and select **Add** > **Connected Services**.</span></span>

3. <span data-ttu-id="402dc-144">Seçin **Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="402dc-144">Select **Application Insights**.</span></span>

4. <span data-ttu-id="402dc-145">Sayfasındaki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="402dc-145">Follow the instructions on the page.</span></span> <span data-ttu-id="402dc-146">Daha önce oluşturduğunuz Application Insights kaynağı seçin.</span><span class="sxs-lookup"><span data-stu-id="402dc-146">Select the Application Insights resource that you created earlier.</span></span>

5. <span data-ttu-id="402dc-147">Seçin **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="402dc-147">Select the **Register** button.</span></span>


## <a name="publish-the-project-to-an-azure-vm"></a><span data-ttu-id="402dc-148">Bir Azure VM projeyi yayımlama</span><span class="sxs-lookup"><span data-stu-id="402dc-148">Publish the project to an Azure VM</span></span>
<span data-ttu-id="402dc-149">Bir Azure VM için bir uygulama yayımlamak için birkaç yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="402dc-149">There are several ways to publish an application to an Azure VM.</span></span> <span data-ttu-id="402dc-150">Visual Studio 2017 kullanan bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="402dc-150">One way is to use Visual Studio 2017.</span></span>

1. <span data-ttu-id="402dc-151">Projeye sağ tıklayın ve seçin **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="402dc-151">Right-click the project and select **Publish**.</span></span>

2. <span data-ttu-id="402dc-152">Seçin **Microsoft Azure sanal makineleri** Yayımla olarak hedef ve aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="402dc-152">Select **Microsoft Azure Virtual Machines** as the publish target and follow the steps.</span></span>

   ![Yayımlama FromVS](./media/enable-profiler-compute/publishtoVM.png)

3. <span data-ttu-id="402dc-154">Bir yük testi karşı uygulamanızı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="402dc-154">Run a load test against your application.</span></span> <span data-ttu-id="402dc-155">Application Insights örnek portal Web sayfasına sonuçları görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="402dc-155">You should see results on the Application Insights instance portal webpage.</span></span>


## <a name="enable-the-profiler"></a><span data-ttu-id="402dc-156">Profil Oluşturucu etkinleştir</span><span class="sxs-lookup"><span data-stu-id="402dc-156">Enable the profiler</span></span>
1. <span data-ttu-id="402dc-157">Application Insights gidin **performans** dikey penceresinde ve select **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="402dc-157">Go to your Application Insights **Performance** blade and select **Configure**.</span></span>
   
   ![Yapılandırma simgesi](./media/enable-profiler-compute/enableprofiler1.png)
 
2. <span data-ttu-id="402dc-159">Seçin **etkinleştirmek profil oluşturucu**.</span><span class="sxs-lookup"><span data-stu-id="402dc-159">Select **Enable Profiler**.</span></span>
   
   ![Profil Oluşturucu simgesi etkinleştir](./media/enable-profiler-compute/enableprofiler2.png)

## <a name="add-a-performance-test-to-your-application"></a><span data-ttu-id="402dc-161">Uygulamanıza bir performans testi ekleyin</span><span class="sxs-lookup"><span data-stu-id="402dc-161">Add a performance test to your application</span></span>
<span data-ttu-id="402dc-162">Uygulama Öngörüler Profiler görüntülenecek bazı örnek veriler topladığımız için şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="402dc-162">Follow these steps so we can collect some sample data to be displayed in Application Insights Profiler:</span></span>

1. <span data-ttu-id="402dc-163">Daha önce oluşturduğunuz Application Insights kaynağı göz atın.</span><span class="sxs-lookup"><span data-stu-id="402dc-163">Browse to the Application Insights resource that you created earlier.</span></span> 

2. <span data-ttu-id="402dc-164">Git **kullanılabilirlik** dikey ve uygulama URL'nize web istekleri gönderir bir performans testi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="402dc-164">Go to the **Availability** blade and add a performance test that sends web requests to your application URL.</span></span> 

   ![Performans testi ekleyin](./media/enable-profiler-compute/AvailabilityTest.png)

## <a name="view-your-performance-data"></a><span data-ttu-id="402dc-166">Performans verileri görünümü</span><span class="sxs-lookup"><span data-stu-id="402dc-166">View your performance data</span></span>

1. <span data-ttu-id="402dc-167">Toplamak ve verileri çözümlemek profil oluşturucu 10-15 dakika bekleyin.</span><span class="sxs-lookup"><span data-stu-id="402dc-167">Wait 10-15 minutes for the profiler to collect and analyze the data.</span></span> 

2. <span data-ttu-id="402dc-168">Git **performans** dikey penceresinde nasıl uygulamanızı gerçekleştirip yük altında olduğunda, Görünüm ve Application Insights kaynağı.</span><span class="sxs-lookup"><span data-stu-id="402dc-168">Go to the **Performance** blade in your Application Insights resource and view how your application is performing when it's under load.</span></span>

   ![Performans görüntüleme](./media/enable-profiler-compute/aiperformance.png)

3. <span data-ttu-id="402dc-170">Simgenin altında seçin **örnekler** açmak için **izleme görünümü** dikey.</span><span class="sxs-lookup"><span data-stu-id="402dc-170">Select the icon under **Examples** to open the **Trace View** blade.</span></span>

   ![İzleme Görünümü Dikey penceresini açma](./media/enable-profiler-compute/traceview.png)


## <a name="work-with-an-existing-template"></a><span data-ttu-id="402dc-172">Var olan bir şablonu ile çalışma</span><span class="sxs-lookup"><span data-stu-id="402dc-172">Work with an existing template</span></span>

1. <span data-ttu-id="402dc-173">Azure tanılama kaynak bildirimi dağıtım şablonunuzda bulun.</span><span class="sxs-lookup"><span data-stu-id="402dc-173">Locate the Azure Diagnostics resource declaration in your deployment template.</span></span>
   
   <span data-ttu-id="402dc-174">Bir bildirim yoksa, aşağıdaki örnekte bildirim benzeyen bir oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="402dc-174">If you don't have a declaration, you can create one that resembles the declaration in the following example.</span></span> <span data-ttu-id="402dc-175">Şablondan güncelleştirebilirsiniz [Azure kaynak Gezgini Web sitesi](https://resources.azure.com).</span><span class="sxs-lookup"><span data-stu-id="402dc-175">You can update the template from the [Azure Resource Explorer website](https://resources.azure.com).</span></span>

2. <span data-ttu-id="402dc-176">Yayımcıdan değiştirme `Microsoft.Azure.Diagnostics` için `AIP.Diagnostics.Test`.</span><span class="sxs-lookup"><span data-stu-id="402dc-176">Change the publisher from `Microsoft.Azure.Diagnostics` to `AIP.Diagnostics.Test`.</span></span>

3. <span data-ttu-id="402dc-177">İçin `typeHandlerVersion`, kullanmak `0.0`.</span><span class="sxs-lookup"><span data-stu-id="402dc-177">For `typeHandlerVersion`, use `0.0`.</span></span>

4. <span data-ttu-id="402dc-178">Olduğundan emin olun `autoUpgradeMinorVersion` ayarlanır `true`.</span><span class="sxs-lookup"><span data-stu-id="402dc-178">Make sure that `autoUpgradeMinorVersion` is set to `true`.</span></span>

5. <span data-ttu-id="402dc-179">Yeni Ekle `ApplicationInsightsProfiler` havuz örneğinde `WadCfg` ayarları nesnesi, aşağıdaki örnekte gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="402dc-179">Add the new `ApplicationInsightsProfiler` sink instance in the `WadCfg` settings object, as shown in the following example:</span></span>

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
                      "ApplicationInsightsProfiler": "Enter the Application Insights instance instrumentation key guid here"
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

## <a name="enable-the-profiler-on-virtual-machine-scale-sets"></a><span data-ttu-id="402dc-180">Sanal makine ölçek kümeleri üzerinde profil oluşturucu etkinleştir</span><span class="sxs-lookup"><span data-stu-id="402dc-180">Enable the profiler on virtual machine scale sets</span></span>
<span data-ttu-id="402dc-181">Profil Oluşturucu etkinleştirme görmek için indirme [WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json) şablonu.</span><span class="sxs-lookup"><span data-stu-id="402dc-181">To see how to enable the profiler, download the [WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json) template.</span></span> <span data-ttu-id="402dc-182">Tanılama uzantısını kaynağa sanal makine ölçek kümesi için bir VM şablonu aynı değişiklikleri uygulayın.</span><span class="sxs-lookup"><span data-stu-id="402dc-182">Apply the same changes in a VM template to the diagnostics extension resource for the virtual machine scale set.</span></span>

<span data-ttu-id="402dc-183">Ölçek kümesindeki her örneği internet erişimi olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="402dc-183">Make sure that each instance in the scale set has access to the internet.</span></span> <span data-ttu-id="402dc-184">Profil Oluşturucu aracı sonra toplanan örnekleri Application Insights'a görüntülemek ve çözümlemek için gönderebilir.</span><span class="sxs-lookup"><span data-stu-id="402dc-184">The Profiler Agent can then send the collected samples to Application Insights for display and analysis.</span></span>

## <a name="enable-the-profiler-on-service-fabric-applications"></a><span data-ttu-id="402dc-185">Profil Oluşturucu Service Fabric uygulamaları etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="402dc-185">Enable the profiler on Service Fabric applications</span></span>
1. <span data-ttu-id="402dc-186">Profil Oluşturucu aracı yükler Azure tanılama uzantısını sağlamak için Service Fabric kümesi sağlayın.</span><span class="sxs-lookup"><span data-stu-id="402dc-186">Provision the Service Fabric cluster to have the Azure Diagnostics extension that installs the Profiler Agent.</span></span>

2. <span data-ttu-id="402dc-187">Projeye Application Insights SDK'sı yükleyin ve Application Insights anahtar yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="402dc-187">Install the Application Insights SDK in the project and configure the Application Insights key.</span></span>

3. <span data-ttu-id="402dc-188">Uygulama kodu Gereci telemetri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="402dc-188">Add application code to instrument telemetry.</span></span>

### <a name="provision-the-service-fabric-cluster-to-have-the-azure-diagnostics-extension-that-installs-the-profiler-agent"></a><span data-ttu-id="402dc-189">Profil Oluşturucu aracı yükler Azure tanılama uzantısını sağlamak için Service Fabric kümesi sağlama</span><span class="sxs-lookup"><span data-stu-id="402dc-189">Provision the Service Fabric cluster to have the Azure Diagnostics extension that installs the Profiler Agent</span></span>
<span data-ttu-id="402dc-190">Service Fabric kümesi güvenli veya güvenli olmayan olabilir.</span><span class="sxs-lookup"><span data-stu-id="402dc-190">A Service Fabric cluster can be secure or non-secure.</span></span> <span data-ttu-id="402dc-191">Güvenli olmayan erişim için bir sertifika gerektirmez şekilde olması için bir ağ geçidi kümesi ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="402dc-191">You can set one gateway cluster to be non-secure so it doesn't require a certificate for access.</span></span> <span data-ttu-id="402dc-192">İş mantığı ve verileri konak kümeleri güvenli olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="402dc-192">Clusters that host business logic and data should be secure.</span></span> <span data-ttu-id="402dc-193">Profil Oluşturucu hem güvenli hem de güvenli olmayan Service Fabric kümeleri üzerinde etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="402dc-193">You can enable the profiler on both secure and non-secure Service Fabric clusters.</span></span> <span data-ttu-id="402dc-194">Bu kılavuzda güvenli olmayan bir küme hangi değişiklikleri profil oluşturucu etkinleştirmek için gerekli olan açıklamak için örnek olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="402dc-194">This walkthrough uses a non-secure cluster as an example to explain what changes are required to enable the profiler.</span></span> <span data-ttu-id="402dc-195">Aynı şekilde güvenli küme sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="402dc-195">You can provision a secure cluster in the same way.</span></span>

1. <span data-ttu-id="402dc-196">Karşıdan [ServiceFabricCluster.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/ServiceFabricCluster.json).</span><span class="sxs-lookup"><span data-stu-id="402dc-196">Download [ServiceFabricCluster.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/ServiceFabricCluster.json).</span></span> <span data-ttu-id="402dc-197">VM'ler ve sanal makine ölçek kümeleri için yaptığınız gibi değiştirmek `Application_Insights_Key` Application Insights anahtarınız ile:</span><span class="sxs-lookup"><span data-stu-id="402dc-197">As you did for VMs and virtual machine scale sets, replace `Application_Insights_Key` with your Application Insights key:</span></span>

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

2. <span data-ttu-id="402dc-198">Şablonu bir PowerShell komut dosyası kullanarak dağıtın:</span><span class="sxs-lookup"><span data-stu-id="402dc-198">Deploy the template by using a PowerShell script:</span></span>

   ```
   Login-AzureRmAccount
   New-AzureRmResourceGroup -Name [Your_Resource_Group_Name] -Location [Your_Resource_Group_Location] -Verbose -Force
   New-AzureRmResourceGroupDeployment -Name [Choose_An_Arbitrary_Name] -ResourceGroupName [Your_Resource_Group_Name] -TemplateFile [Path_To_Your_Template]

   ```

### <a name="install-the-application-insights-sdk-in-the-project-and-configure-the-application-insights-key"></a><span data-ttu-id="402dc-199">Projeye Application Insights SDK'sı yükleyin ve Application Insights anahtar yapılandırın</span><span class="sxs-lookup"><span data-stu-id="402dc-199">Install the Application Insights SDK in the project and configure the Application Insights key</span></span>
<span data-ttu-id="402dc-200">Gelen Application Insights SDK'sı yükleme [NuGet paketi](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span><span class="sxs-lookup"><span data-stu-id="402dc-200">Install the Application Insights SDK from the [NuGet package](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span></span> <span data-ttu-id="402dc-201">2.3 ya da daha yeni bir kararlı sürümünü yüklediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="402dc-201">Make sure that you install a stable version, 2.3 or later.</span></span> 

<span data-ttu-id="402dc-202">Application Insights projelerinizde yapılandırma hakkında daha fazla bilgi için bkz: [kullanarak Service Fabric Application Insights ile](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/blob/dev/appinsights/ApplicationInsights.md).</span><span class="sxs-lookup"><span data-stu-id="402dc-202">For information about configuring Application Insights in your projects, see [Using Service Fabric with Application Insights](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/blob/dev/appinsights/ApplicationInsights.md).</span></span>

### <a name="add-application-code-to-instrument-telemetry"></a><span data-ttu-id="402dc-203">Uygulama kodu Gereci telemetri ekleyin</span><span class="sxs-lookup"><span data-stu-id="402dc-203">Add application code to instrument telemetry</span></span>
1. <span data-ttu-id="402dc-204">İzleme, bir kullanarak eklemek istediğiniz kod herhangi bir parçasının çevresinde deyimi.</span><span class="sxs-lookup"><span data-stu-id="402dc-204">For any piece of code that you want to instrument, add a using statement around it.</span></span> 

   <span data-ttu-id="402dc-205">Aşağıdaki örnekte, `RunAsync` yöntemi bazı iş yapılması ve `telemetryClient` sınıfı başladıktan sonra telemetri yakalar.</span><span class="sxs-lookup"><span data-stu-id="402dc-205">In the following  example, the `RunAsync` method is doing some work, and the `telemetryClient` class captures the telemetry after it starts.</span></span> <span data-ttu-id="402dc-206">Olay uygulama arasında benzersiz bir adı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="402dc-206">The event needs a unique name across the application.</span></span>

   ```
   protected override async Task RunAsync(CancellationToken cancellationToken)
       {
           // TODO: Replace the following sample code with your own logic
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

2. <span data-ttu-id="402dc-207">Service Fabric kümesi uygulamanıza dağıtın.</span><span class="sxs-lookup"><span data-stu-id="402dc-207">Deploy your application to the Service Fabric cluster.</span></span> <span data-ttu-id="402dc-208">10 dakika çalıştırmak için uygulamayı bekleyin.</span><span class="sxs-lookup"><span data-stu-id="402dc-208">Wait for the app to run for 10 minutes.</span></span> <span data-ttu-id="402dc-209">Daha iyi efekti için uygulama üzerinde bir yük testi çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="402dc-209">For better effect, you can run a load test on the app.</span></span> <span data-ttu-id="402dc-210">Application Insights Portalı'nın gidin **performans** dikey penceresinde ve profil oluşturma izlemeleri görünür örnekleri görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="402dc-210">Go to the Application Insights portal's **Performance** blade, and you should see examples of profiling traces appear.</span></span>

<!---
Commenting out these sections for now
## Enable the Profiler on Cloud Services applications
[TODO]
## Enable the Profiler on classic Azure Virtual Machines
[TODO]
## Enable the Profiler on on-premise servers
[TODO]
--->

## <a name="next-steps"></a><span data-ttu-id="402dc-211">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="402dc-211">Next steps</span></span>

- <span data-ttu-id="402dc-212">Profil Oluşturucu sorunlarını giderme konusunda Yardım bulmak [sorun giderme profil oluşturucu](app-insights-profiler.md#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="402dc-212">Find help with troubleshooting profiler issues in [Profiler troubleshooting](app-insights-profiler.md#troubleshooting).</span></span>

- <span data-ttu-id="402dc-213">Profil Oluşturucusu'nda hakkında daha fazla bilgiyi [uygulama Öngörüler profil oluşturucu](app-insights-profiler.md).</span><span class="sxs-lookup"><span data-stu-id="402dc-213">Read more about the profiler in [Application Insights Profiler](app-insights-profiler.md).</span></span>
