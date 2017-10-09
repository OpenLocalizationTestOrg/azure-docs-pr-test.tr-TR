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
# <a name="enable-application-insights-profiler-on-an-azure-cloud-services-resource"></a>Bir Azure Cloud Services kaynakta uygulama Öngörüler profil oluşturucu etkinleştir

Bu kılavuz, nasıl ASP.NET uygulaması üzerinde Azure uygulama Öngörüler profil oluşturucu tooenable bir Azure Cloud Services kaynak tarafından barındırılan gösterir. Merhaba, Azure sanal makineler, sanal makine ölçek kümeleri ve Azure Service Fabric desteği örnekler. Merhaba örnekler tüm hello Azure Resource Manager dağıtım modelini destekleyen şablonlarını kullanır. Merhaba dağıtım modeli hakkında daha fazla bilgi için gözden [Azure Resource Manager ve klasik dağıtım: dağıtım modellerini anlama ve hello kaynaklarınızın durumunu](/azure-resource-manager/resource-manager-deployment-model).

## <a name="overview"></a>Genel Bakış

Diyagram aşağıdaki hello hello profil oluşturucu için Azure Cloud Services kaynakları nasıl çalıştığı gösterilmektedir. Bir Azure sanal makinesi bir örnek olarak kullanır.

![Genel Bakış](./media/enable-profiler-compute/overview.png) toocollect bilgi işlem ve ekranınızda için Azure portal Merhaba, hello Tanılama Aracı bileşeni hello Azure Cloud Services kaynaklar için yüklemeniz gerekir. Hello hello izlenecek geri kalanı rehberlik sağlar tooinstall ve hello Tanılama Aracı tooenable uygulama Öngörüler profil oluşturucu yapılandırın.

## <a name="prerequisites-for-hello-walkthrough"></a>Merhaba gözden geçirme için Önkoşullar

* Hello profil oluşturucu aracıları hello VM'ler üzerinde yükleyen bir dağıtım Resource Manager şablonu ([WindowsVirtualMachine.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json)) veya ölçekleme kümeleri ([WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json)).

* Profil oluşturma için etkinleştirilmiş bir Application Insights örneği. Yönergeler için bkz: [etkinleştirmek hello profil](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-profiler#enable-the-profiler).

* .NET framework 4.6.1 veya sonrası yüklü hello Azure Cloud Services kaynak hedefleyin.

## <a name="create-a-resource-group-in-your-azure-subscription"></a>Azure aboneliğinizde bir kaynak grubu oluştur
Aşağıdaki örnek hello nasıl toocreate bir kaynak grubunda bir PowerShell komut dosyası kullanarak gösterir:

```
New-AzureRmResourceGroup -Name "Replace_With_Resource_Group_Name" -Location "Replace_With_Resource_Group_Location"
```

## <a name="create-an-application-insights-resource-in-hello-resource-group"></a>Merhaba kaynak grubunda bir Application Insights kaynağı oluşturma
Merhaba üzerinde **Application Insights** dikey penceresinde, bu örnekte gösterildiği gibi kaynak için hello bilgileri girin: 

![Uygulama Öngörüler dikey penceresi](./media/enable-profiler-compute/createai.png)

## <a name="apply-an-application-insights-instrumentation-key-in-hello-azure-resource-manager-template"></a>Bir Application Insights izleme anahtarı hello Azure Resource Manager Şablonu Uygula

1. Merhaba şablonu henüz yüklemediyseniz, indirin [GitHub](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json).

2. Merhaba Application Insights anahtarını bulun.
   
   ![Merhaba anahtar konumu](./media/enable-profiler-compute/copyaikey.png)

3. Merhaba şablon değeri değiştirin.
   
   ![Merhaba şablonunda yerini değeri](./media/enable-profiler-compute/copyaikeytotemplate.png)

## <a name="create-an-azure-vm-toohost-hello-web-application"></a>Bir Azure VM toohost Merhaba web uygulaması oluşturma
1. Bir güvenli dize toosave hello parola oluşturun.

   ```
   $password = ConvertTo-SecureString -String "Replace_With_Your_Password" -AsPlainText -Force
   ```

2. Hello Azure Resource Manager şablonu dağıtma.

   Resource Manager şablonu içeren hello PowerShell konsol toohello klasöründe Hello dizini değiştirin. toodeploy hello şablonu, hello aşağıdaki komutu çalıştırın:

   ```
   New-AzureRmResourceGroupDeployment -ResourceGroupName "Replace_With_Resource_Group_Name" -TemplateFile .\WindowsVirtualMachine.json -adminUsername "Replace_With_your_user_name" -adminPassword $password -dnsNameForPublicIP "Replace_WIth_your_DNS_Name" -Verbose
   ```

Merhaba komut dosyası başarıyla çalıştıktan sonra adlandırılmış bir VM'nin bulmalısınız **MyWindowsVM** kaynak grubunuzdaki.

## <a name="configure-web-deploy-on-hello-vm"></a>Web dağıtımı hello VM üzerinde yapılandırma
Web uygulamanızı Visual Studio'dan yayımlamak için VM Web Dağıtımı'nin etkin olduğundan emin olun.

tooinstall Web dağıtımı Webpı, kullanarak el ile bir VM'de bkz [yükleme ve IIS 8. 0 veya daha sonra Web dağıtımı yapılandırma](https://docs.microsoft.com/en-us/iis/install/installing-publishing-technologies/installing-and-configuring-web-deploy-on-iis-80-or-later). Nasıl bir örneği için bir Azure Resource Manager şablonu kullanarak Web dağıtımı yükleme tooautomate bkz [oluşturun, yapılandırma ve bir web uygulaması tooan Azure VM dağıtma](https://azure.microsoft.com/en-us/resources/templates/201-web-app-vm-dsc/).

Bir ASP.NET MVC uygulaması dağıtıyorsanız, tooServer Yöneticisi, select Git **rol ve Özellik Ekle** > **Web sunucusu (IIS)** > **Web sunucusu**  >  **Uygulama geliştirme**ve ASP.NET 4.5 sunucunuzda etkinleştirin.

![ASP.NET Ekle](./media/enable-profiler-compute/addaspnet45.png)

## <a name="install-hello-azure-application-insights-sdk-for-your-project"></a>Projeniz için Hello Azure Application Insights SDK'sı yükleyin
1. ASP.NET web uygulamanızı Visual Studio'da açın.

2. Merhaba projesine sağ tıklatın ve **Ekle** > **bağlantılı Hizmetler**.

3. Seçin **Application Insights**.

4. Merhaba sayfasındaki Hello yönergeleri izleyin. Daha önce oluşturduğunuz hello Application Insights kaynağı seçin.

5. Select hello **kaydetmek** düğmesi.


## <a name="publish-hello-project-tooan-azure-vm"></a>Yayımlama Hello proje tooan Azure VM
Bir uygulama tooan Azure VM birkaç yolu toopublish vardır. Visual Studio 2017 toouse bir yoludur.

1. Merhaba projesine sağ tıklatın ve **Yayımla**.

2. Seçin **Microsoft Azure sanal makineleri** hello olarak hedef yayımlama ve hello adımları izleyin.

   ![Yayımlama FromVS](./media/enable-profiler-compute/publishtoVM.png)

3. Bir yük testi karşı uygulamanızı çalıştırın. Merhaba Application Insights örnek portal Web sayfasında sonuçları görmeniz gerekir.


## <a name="enable-hello-profiler"></a>Hello profil oluşturucu etkinleştir
1. Tooyour Application Insights Git **performans** dikey penceresinde ve select **yapılandırma**.
   
   ![Yapılandırma simgesi](./media/enable-profiler-compute/enableprofiler1.png)
 
2. Seçin **etkinleştirmek profil oluşturucu**.
   
   ![Profil Oluşturucu simgesi etkinleştir](./media/enable-profiler-compute/enableprofiler2.png)

## <a name="add-a-performance-test-tooyour-application"></a>Performans testi tooyour uygulama ekleme
Uygulama Öngörüler Profil Oluşturucusu'nda görüntülenen bazı örnek veri toobe topladığımız için şu adımları izleyin:

1. Daha önce oluşturduğunuz toohello Application Insights kaynağı göz atın. 

2. Toohello Git **kullanılabilirlik** dikey ve web istekleri tooyour uygulama URL'si gönderir bir performans testi ekleyin. 

   ![Performans testi ekleyin](./media/enable-profiler-compute/AvailabilityTest.png)

## <a name="view-your-performance-data"></a>Performans verileri görünümü

1. Hello profil oluşturucu toocollect 10-15 dakika bekleyin ve hello verileri analiz edin. 

2. Toohello Git **performans** dikey penceresinde nasıl uygulamanızı gerçekleştirip yük altında olduğunda, Görünüm ve Application Insights kaynağı.

   ![Performans görüntüleme](./media/enable-profiler-compute/aiperformance.png)

3. Select hello simgesi altında **örnekler** tooopen hello **izleme görünümü** dikey.

   ![Merhaba izleme görünümü dikey penceresini açma](./media/enable-profiler-compute/traceview.png)


## <a name="work-with-an-existing-template"></a>Var olan bir şablonu ile çalışma

1. Hello Azure tanılama kaynak bildirimi dağıtım şablonunuzda bulun.
   
   Bir bildirim yoksa, aşağıdaki örneğine hello hello bildiriminde benzeyen bir oluşturabilirsiniz. Merhaba hello şablondan güncelleştirebilirsiniz [Azure kaynak Gezgini Web sitesi](https://resources.azure.com).

2. Değişiklik hello yayımcıdan `Microsoft.Azure.Diagnostics` çok`AIP.Diagnostics.Test`.

3. İçin `typeHandlerVersion`, kullanmak `0.0`.

4. Olduğundan emin olun `autoUpgradeMinorVersion` çok ayarlanır`true`.

5. Merhaba yeni Ekle `ApplicationInsightsProfiler` hello havuz örneğinde `WadCfg` hello aşağıdaki örnekte gösterildiği gibi ayarları nesnesi:

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

## <a name="enable-hello-profiler-on-virtual-machine-scale-sets"></a>Sanal makine ölçek kümeleri üzerinde Hello profil oluşturucu etkinleştir
toosee tooenable hello nasıl profil oluşturucu, indirme hello [WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json) şablonu. Merhaba aynı hello sanal makine ölçek kümesi için bir VM şablonu toohello tanılama uzantısını kaynak değişiklikleri uygulayın.

Merhaba ölçek kümesindeki her örneği erişim toohello sahip olduğundan emin olun Internet. Hello Profil Oluşturucu aracı, sonra tooApplication Öngörüler görüntüleme ve analiz için toplanan hello örnekleri gönderebilir.

## <a name="enable-hello-profiler-on-service-fabric-applications"></a>Service Fabric uygulamaları Hello profil oluşturucu etkinleştir
1. Sağlama hello hello Profil Oluşturucu aracı yükleyen Service Fabric kümesi toohave hello Azure tanılama uzantısını.

2. Merhaba projesinde Hello Application Insights SDK'sı yükleyin ve hello Application Insights anahtar yapılandırın.

3. Uygulama kodu tooinstrument telemetri ekleyin.

### <a name="provision-hello-service-fabric-cluster-toohave-hello-azure-diagnostics-extension-that-installs-hello-profiler-agent"></a>Sağlama hello Service Fabric kümesi toohave hello hello Profil Oluşturucu aracı yükler Azure tanılama uzantısını
Service Fabric kümesi güvenli veya güvenli olmayan olabilir. Erişim için bir sertifika gerektirmez şekilde güvenli olmayan bir ağ geçidi küme toobe ayarlayabilirsiniz. İş mantığı ve verileri konak kümeleri güvenli olması gerekir. Hello profil oluşturucu hem güvenli hem de güvenli olmayan Service Fabric kümeleri üzerinde etkinleştirebilirsiniz. Bu kılavuzda, güvenli olmayan bir küme gerekli tooenable hello profil oluşturucu hangi değişiklikleri olan bir örnek tooexplain kullanılır. Merhaba güvenli bir kümede sağlayabilirsiniz aynı şekilde.

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

2. Merhaba şablonu, bir PowerShell komut dosyası kullanarak dağıtın:

   ```
   Login-AzureRmAccount
   New-AzureRmResourceGroup -Name [Your_Resource_Group_Name] -Location [Your_Resource_Group_Location] -Verbose -Force
   New-AzureRmResourceGroupDeployment -Name [Choose_An_Arbitrary_Name] -ResourceGroupName [Your_Resource_Group_Name] -TemplateFile [Path_To_Your_Template]

   ```

### <a name="install-hello-application-insights-sdk-in-hello-project-and-configure-hello-application-insights-key"></a>Merhaba projesinde Hello Application Insights SDK'sı yükleyin ve hello Application Insights anahtar yapılandırın
Hello Hello Application Insights SDK'sı yükleme [NuGet paketi](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/). 2.3 ya da daha yeni bir kararlı sürümünü yüklediğinizden emin olun. 

Application Insights projelerinizde yapılandırma hakkında daha fazla bilgi için bkz: [kullanarak Service Fabric Application Insights ile](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/blob/dev/appinsights/ApplicationInsights.md).

### <a name="add-application-code-tooinstrument-telemetry"></a>Uygulama kodu tooinstrument telemetri ekleyin
1. İçin herhangi bir tooinstrument istediğiniz kod kullanarak bir ekleme deyimi çevresinde. 

   Aşağıdaki örneğine hello hello `RunAsync` yöntemi bazı iş yapılması ve hello `telemetryClient` sınıfı başladıktan sonra hello telemetri yakalar. Merhaba olay hello uygulama arasında benzersiz bir ad gerekiyor.

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

2. Uygulama toohello Service Fabric kümesi dağıtın. Merhaba uygulama toorun için 10 dakika bekleyin. Daha iyi efekti hello uygulama üzerinde bir yük testi çalıştırabilirsiniz. Git toohello Application Insights Portalı'nın **performans** dikey penceresinde ve profil oluşturma izlemeleri görünür örnekleri görmeniz gerekir.

<!---
Commenting out these sections for now
## Enable hello Profiler on Cloud Services applications
[TODO]
## Enable hello Profiler on classic Azure Virtual Machines
[TODO]
## Enable hello Profiler on on-premise servers
[TODO]
--->

## <a name="next-steps"></a>Sonraki adımlar

- Profil Oluşturucu sorunlarını giderme konusunda Yardım bulmak [sorun giderme profil oluşturucu](app-insights-profiler.md#troubleshooting).

- Hello Profil Oluşturucusu'nda hakkında daha fazla bilgiyi [uygulama Öngörüler profil oluşturucu](app-insights-profiler.md).
