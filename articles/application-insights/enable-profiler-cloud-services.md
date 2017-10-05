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
# <a name="enable-application-insights-profiler-on-an-azure-cloud-services-resource"></a>Bir Azure Cloud Services kaynakta uygulama Öngörüler profil oluşturucu etkinleştir

Bu kılavuz, Azure uygulama Öngörüler profil oluşturucu Azure Cloud Services kaynak tarafından barındırılan bir ASP.NET uygulamasını etkinleştirmek gösterilmiştir. Azure sanal makineler, sanal makine ölçek kümeleri ve Azure Service Fabric desteği örnekler. Tüm örnekler Azure Resource Manager dağıtım modelini destekleyen şablonlarını kullanır. Dağıtım modeli hakkında daha fazla bilgi için gözden [Azure Resource Manager ve klasik dağıtım: dağıtım modelleri ve kaynaklarınızın durumunu anlamak](/azure-resource-manager/resource-manager-deployment-model).

## <a name="overview"></a>Genel Bakış

Aşağıdaki diyagramda, Azure Cloud Services kaynaklar için profil oluşturucu nasıl çalıştığı gösterilmektedir. Bir Azure sanal makinesi bir örnek olarak kullanır.

![Genel Bakış](./media/enable-profiler-compute/overview.png) Azure Portalı'nda işleme ve görüntü bilgi toplamak için Azure Cloud Services kaynaklar için tanılama aracı bileşeni yüklemeniz gerekir. Kalan örnekler yüklemek ve uygulama Öngörüler profil oluşturucu etkinleştirmek için tanılama aracısını yapılandırmak hakkında yönergeler sağlar.

## <a name="prerequisites-for-the-walkthrough"></a>İzlenecek yol için Önkoşullar

* Profil Oluşturucu aracıları sanal makinelerin yükleyen bir dağıtım Resource Manager şablonu ([WindowsVirtualMachine.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json)) veya ölçekleme kümeleri ([WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json)).

* Profil oluşturma için etkinleştirilmiş bir Application Insights örneği. Yönergeler için bkz: [profilini etkinleştirmek](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-profiler#enable-the-profiler).

* .NET framework 4.6.1 veya hedef Azure Cloud Services kaynak sonraki bir sürümü yüklü.

## <a name="create-a-resource-group-in-your-azure-subscription"></a>Azure aboneliğinizde bir kaynak grubu oluştur
Aşağıdaki örnek, bir PowerShell komut dosyası kullanarak bir kaynak grubu oluşturmak gösterilmiştir:

```
New-AzureRmResourceGroup -Name "Replace_With_Resource_Group_Name" -Location "Replace_With_Resource_Group_Location"
```

## <a name="create-an-application-insights-resource-in-the-resource-group"></a>Kaynak grubunda bir Application Insights kaynağı oluşturma
Üzerinde **Application Insights** dikey penceresinde, bu örnekte gösterildiği gibi kaynak için bilgileri girin: 

![Uygulama Öngörüler dikey penceresi](./media/enable-profiler-compute/createai.png)

## <a name="apply-an-application-insights-instrumentation-key-in-the-azure-resource-manager-template"></a>Azure Resource Manager şablonunda bir Application Insights izleme anahtarı Uygula

1. Şablon henüz yüklemediyseniz, indirin [GitHub](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json).

2. Application Insights anahtarını bulun.
   
   ![Anahtar konumu](./media/enable-profiler-compute/copyaikey.png)

3. Şablon değeri değiştirin.
   
   ![Şablonda yerini değeri](./media/enable-profiler-compute/copyaikeytotemplate.png)

## <a name="create-an-azure-vm-to-host-the-web-application"></a>Web uygulamasını barındırmak için bir Azure VM oluşturma
1. Parola kaydetmek için güvenli bir dize oluşturun.

   ```
   $password = ConvertTo-SecureString -String "Replace_With_Your_Password" -AsPlainText -Force
   ```

2. Azure Resource Manager şablonu dağıtma.

   PowerShell konsolundaki dizin Kaynak Yöneticisi şablonunuzu içeren klasör olarak değiştirin. Şablonu dağıtmak için aşağıdaki komutu çalıştırın:

   ```
   New-AzureRmResourceGroupDeployment -ResourceGroupName "Replace_With_Resource_Group_Name" -TemplateFile .\WindowsVirtualMachine.json -adminUsername "Replace_With_your_user_name" -adminPassword $password -dnsNameForPublicIP "Replace_WIth_your_DNS_Name" -Verbose
   ```

Komut dosyası başarıyla çalıştıktan sonra adlandırılmış bir VM'nin bulmalısınız **MyWindowsVM** kaynak grubunuzdaki.

## <a name="configure-web-deploy-on-the-vm"></a>Web yapılandırma VM dağıtma
Web uygulamanızı Visual Studio'dan yayımlamak için VM Web Dağıtımı'nin etkin olduğundan emin olun.

Web dağıtımı bir VM'de Webpı aracılığıyla el ile yüklemek için bkz [yükleme ve IIS 8. 0 veya daha sonra Web dağıtımı yapılandırma](https://docs.microsoft.com/en-us/iis/install/installing-publishing-technologies/installing-and-configuring-web-deploy-on-iis-80-or-later). Bir Azure Resource Manager şablonu kullanarak Web dağıtımı yükleme otomatik hale getirmek nasıl bir örnek için bkz: [oluşturma, yapılandırma ve bir Azure VM için bir web uygulaması dağıtma](https://azure.microsoft.com/en-us/resources/templates/201-web-app-vm-dsc/).

Git Sunucu Yöneticisi, bir ASP.NET MVC uygulaması dağıtıyorsanız seçin **rol ve Özellik Ekle** > **Web sunucusu (IIS)** > **Web sunucusu**  >  **Uygulama geliştirme**ve ASP.NET 4.5 sunucunuzda etkinleştirin.

![ASP.NET Ekle](./media/enable-profiler-compute/addaspnet45.png)

## <a name="install-the-azure-application-insights-sdk-for-your-project"></a>Projeniz için Azure Application Insights SDK'sı yükleyin
1. ASP.NET web uygulamanızı Visual Studio'da açın.

2. Projeye sağ tıklayın ve seçin **Ekle** > **bağlantılı Hizmetler**.

3. Seçin **Application Insights**.

4. Sayfasındaki yönergeleri izleyin. Daha önce oluşturduğunuz Application Insights kaynağı seçin.

5. Seçin **kaydetmek** düğmesi.


## <a name="publish-the-project-to-an-azure-vm"></a>Bir Azure VM projeyi yayımlama
Bir Azure VM için bir uygulama yayımlamak için birkaç yolu vardır. Visual Studio 2017 kullanan bir yoludur.

1. Projeye sağ tıklayın ve seçin **Yayımla**.

2. Seçin **Microsoft Azure sanal makineleri** Yayımla olarak hedef ve aşağıdaki adımları izleyin.

   ![Yayımlama FromVS](./media/enable-profiler-compute/publishtoVM.png)

3. Bir yük testi karşı uygulamanızı çalıştırın. Application Insights örnek portal Web sayfasına sonuçları görmeniz gerekir.


## <a name="enable-the-profiler"></a>Profil Oluşturucu etkinleştir
1. Application Insights gidin **performans** dikey penceresinde ve select **yapılandırma**.
   
   ![Yapılandırma simgesi](./media/enable-profiler-compute/enableprofiler1.png)
 
2. Seçin **etkinleştirmek profil oluşturucu**.
   
   ![Profil Oluşturucu simgesi etkinleştir](./media/enable-profiler-compute/enableprofiler2.png)

## <a name="add-a-performance-test-to-your-application"></a>Uygulamanıza bir performans testi ekleyin
Uygulama Öngörüler Profiler görüntülenecek bazı örnek veriler topladığımız için şu adımları izleyin:

1. Daha önce oluşturduğunuz Application Insights kaynağı göz atın. 

2. Git **kullanılabilirlik** dikey ve uygulama URL'nize web istekleri gönderir bir performans testi ekleyin. 

   ![Performans testi ekleyin](./media/enable-profiler-compute/AvailabilityTest.png)

## <a name="view-your-performance-data"></a>Performans verileri görünümü

1. Toplamak ve verileri çözümlemek profil oluşturucu 10-15 dakika bekleyin. 

2. Git **performans** dikey penceresinde nasıl uygulamanızı gerçekleştirip yük altında olduğunda, Görünüm ve Application Insights kaynağı.

   ![Performans görüntüleme](./media/enable-profiler-compute/aiperformance.png)

3. Simgenin altında seçin **örnekler** açmak için **izleme görünümü** dikey.

   ![İzleme Görünümü Dikey penceresini açma](./media/enable-profiler-compute/traceview.png)


## <a name="work-with-an-existing-template"></a>Var olan bir şablonu ile çalışma

1. Azure tanılama kaynak bildirimi dağıtım şablonunuzda bulun.
   
   Bir bildirim yoksa, aşağıdaki örnekte bildirim benzeyen bir oluşturabilirsiniz. Şablondan güncelleştirebilirsiniz [Azure kaynak Gezgini Web sitesi](https://resources.azure.com).

2. Yayımcıdan değiştirme `Microsoft.Azure.Diagnostics` için `AIP.Diagnostics.Test`.

3. İçin `typeHandlerVersion`, kullanmak `0.0`.

4. Olduğundan emin olun `autoUpgradeMinorVersion` ayarlanır `true`.

5. Yeni Ekle `ApplicationInsightsProfiler` havuz örneğinde `WadCfg` ayarları nesnesi, aşağıdaki örnekte gösterildiği gibi:

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

## <a name="enable-the-profiler-on-virtual-machine-scale-sets"></a>Sanal makine ölçek kümeleri üzerinde profil oluşturucu etkinleştir
Profil Oluşturucu etkinleştirme görmek için indirme [WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json) şablonu. Tanılama uzantısını kaynağa sanal makine ölçek kümesi için bir VM şablonu aynı değişiklikleri uygulayın.

Ölçek kümesindeki her örneği internet erişimi olduğundan emin olun. Profil Oluşturucu aracı sonra toplanan örnekleri Application Insights'a görüntülemek ve çözümlemek için gönderebilir.

## <a name="enable-the-profiler-on-service-fabric-applications"></a>Profil Oluşturucu Service Fabric uygulamaları etkinleştirme
1. Profil Oluşturucu aracı yükler Azure tanılama uzantısını sağlamak için Service Fabric kümesi sağlayın.

2. Projeye Application Insights SDK'sı yükleyin ve Application Insights anahtar yapılandırın.

3. Uygulama kodu Gereci telemetri ekleyin.

### <a name="provision-the-service-fabric-cluster-to-have-the-azure-diagnostics-extension-that-installs-the-profiler-agent"></a>Profil Oluşturucu aracı yükler Azure tanılama uzantısını sağlamak için Service Fabric kümesi sağlama
Service Fabric kümesi güvenli veya güvenli olmayan olabilir. Güvenli olmayan erişim için bir sertifika gerektirmez şekilde olması için bir ağ geçidi kümesi ayarlayabilirsiniz. İş mantığı ve verileri konak kümeleri güvenli olması gerekir. Profil Oluşturucu hem güvenli hem de güvenli olmayan Service Fabric kümeleri üzerinde etkinleştirebilirsiniz. Bu kılavuzda güvenli olmayan bir küme hangi değişiklikleri profil oluşturucu etkinleştirmek için gerekli olan açıklamak için örnek olarak kullanılır. Aynı şekilde güvenli küme sağlayabilirsiniz.

1. Karşıdan [ServiceFabricCluster.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/ServiceFabricCluster.json). VM'ler ve sanal makine ölçek kümeleri için yaptığınız gibi değiştirmek `Application_Insights_Key` Application Insights anahtarınız ile:

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

2. Şablonu bir PowerShell komut dosyası kullanarak dağıtın:

   ```
   Login-AzureRmAccount
   New-AzureRmResourceGroup -Name [Your_Resource_Group_Name] -Location [Your_Resource_Group_Location] -Verbose -Force
   New-AzureRmResourceGroupDeployment -Name [Choose_An_Arbitrary_Name] -ResourceGroupName [Your_Resource_Group_Name] -TemplateFile [Path_To_Your_Template]

   ```

### <a name="install-the-application-insights-sdk-in-the-project-and-configure-the-application-insights-key"></a>Projeye Application Insights SDK'sı yükleyin ve Application Insights anahtar yapılandırın
Gelen Application Insights SDK'sı yükleme [NuGet paketi](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/). 2.3 ya da daha yeni bir kararlı sürümünü yüklediğinizden emin olun. 

Application Insights projelerinizde yapılandırma hakkında daha fazla bilgi için bkz: [kullanarak Service Fabric Application Insights ile](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/blob/dev/appinsights/ApplicationInsights.md).

### <a name="add-application-code-to-instrument-telemetry"></a>Uygulama kodu Gereci telemetri ekleyin
1. İzleme, bir kullanarak eklemek istediğiniz kod herhangi bir parçasının çevresinde deyimi. 

   Aşağıdaki örnekte, `RunAsync` yöntemi bazı iş yapılması ve `telemetryClient` sınıfı başladıktan sonra telemetri yakalar. Olay uygulama arasında benzersiz bir adı olmalıdır.

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

2. Service Fabric kümesi uygulamanıza dağıtın. 10 dakika çalıştırmak için uygulamayı bekleyin. Daha iyi efekti için uygulama üzerinde bir yük testi çalıştırabilirsiniz. Application Insights Portalı'nın gidin **performans** dikey penceresinde ve profil oluşturma izlemeleri görünür örnekleri görmeniz gerekir.

<!---
Commenting out these sections for now
## Enable the Profiler on Cloud Services applications
[TODO]
## Enable the Profiler on classic Azure Virtual Machines
[TODO]
## Enable the Profiler on on-premise servers
[TODO]
--->

## <a name="next-steps"></a>Sonraki adımlar

- Profil Oluşturucu sorunlarını giderme konusunda Yardım bulmak [sorun giderme profil oluşturucu](app-insights-profiler.md#troubleshooting).

- Profil Oluşturucusu'nda hakkında daha fazla bilgiyi [uygulama Öngörüler profil oluşturucu](app-insights-profiler.md).
