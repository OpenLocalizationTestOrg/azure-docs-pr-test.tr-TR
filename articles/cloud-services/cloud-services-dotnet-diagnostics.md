---
title: "aaaHow toouse bulut Hizmetleri ile Azure tanılama (.NET) | Microsoft Docs"
description: "Azure tanılama toogather kullanarak verileri azure'dan hata ayıklama, performans, izleme, trafik analizi ve daha fazla ölçme bulut Hizmetleri."
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: 
ms.assetid: 89623a0e-4e78-4b67-a446-7d19a35a44be
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/22/2017
ms.author: robb
ms.openlocfilehash: 1525eac1e85955d8f05aa21a9805e0a80d0e4bca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-azure-diagnostics-in-azure-cloud-services"></a><span data-ttu-id="5e669-103">Azure Cloud Services, Azure Tanılama'yı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="5e669-103">Enabling Azure Diagnostics in Azure Cloud Services</span></span>
<span data-ttu-id="5e669-104">Bkz: [Azure tanılama genel bakış](../azure-diagnostics.md) bir arka planda Azure tanılama için.</span><span class="sxs-lookup"><span data-stu-id="5e669-104">See [Azure Diagnostics Overview](../azure-diagnostics.md) for a background on Azure Diagnostics.</span></span>

## <a name="how-tooenable-diagnostics-in-a-worker-role"></a><span data-ttu-id="5e669-105">Nasıl tooEnable çalışan rolü tanılamada</span><span class="sxs-lookup"><span data-stu-id="5e669-105">How tooEnable Diagnostics in a Worker Role</span></span>
<span data-ttu-id="5e669-106">Bu kılavuzda nasıl tooimplement telemetri verilerini kullanarak gösterdiği Azure çalışan rolüne hello .NET EventSource sınıfı açıklar.</span><span class="sxs-lookup"><span data-stu-id="5e669-106">This walkthrough describes how tooimplement an Azure worker role that emits telemetry data using hello .NET EventSource class.</span></span> <span data-ttu-id="5e669-107">Azure tanılama kullanılan toocollect hello telemetri verilerinin ve bir Azure depolama hesabında depolamak.</span><span class="sxs-lookup"><span data-stu-id="5e669-107">Azure Diagnostics is used toocollect hello telemetry data and store it in an Azure storage account.</span></span> <span data-ttu-id="5e669-108">Çalışan rolü oluştururken, Visual Studio tanılama 1.0 Azure SDK'ları ve önceki sürümler için .NET 2.4 hello çözümde bir parçası olarak otomatik olarak etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="5e669-108">When creating a worker role, Visual Studio automatically enables Diagnostics 1.0 as part of hello solution in Azure SDKs for .NET 2.4 and earlier.</span></span> <span data-ttu-id="5e669-109">Merhaba aşağıdaki yönergeleri hello çalışan rolü hello çözümden tanılama 1.0 devre dışı bırakma ve tanılama 1.2 dağıtma veya 1.3 tooyour çalışan rolü oluşturmak için hello işlemi açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="5e669-109">hello following instructions describe hello process for creating hello worker role, disabling Diagnostics 1.0 from hello solution, and deploying Diagnostics 1.2 or 1.3 tooyour worker role.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="5e669-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="5e669-110">Prerequisites</span></span>
<span data-ttu-id="5e669-111">Bu makale bir Azure aboneliğiniz varsa ve hello Azure SDK ile Visual Studio'ya varsayar.</span><span class="sxs-lookup"><span data-stu-id="5e669-111">This article assumes you have an Azure subscription and are using Visual Studio with hello Azure SDK.</span></span> <span data-ttu-id="5e669-112">Bir Azure aboneliğiniz yoksa, hello için kaydolabilirsiniz [ücretsiz deneme][Free Trial].</span><span class="sxs-lookup"><span data-stu-id="5e669-112">If you do not have an Azure subscription, you can sign up for hello [Free Trial][Free Trial].</span></span> <span data-ttu-id="5e669-113">Emin olun çok[yükleyin ve Azure PowerShell sürüm 0.8.7 yapılandırın veya daha sonra][Install and configure Azure PowerShell version 0.8.7 or later].</span><span class="sxs-lookup"><span data-stu-id="5e669-113">Make sure too[Install and configure Azure PowerShell version 0.8.7 or later][Install and configure Azure PowerShell version 0.8.7 or later].</span></span>

### <a name="step-1-create-a-worker-role"></a><span data-ttu-id="5e669-114">1. adım: Çalışan rolü oluşturma</span><span class="sxs-lookup"><span data-stu-id="5e669-114">Step 1: Create a Worker Role</span></span>
1. <span data-ttu-id="5e669-115">**Visual Studio**’yu başlatın.</span><span class="sxs-lookup"><span data-stu-id="5e669-115">Launch **Visual Studio**.</span></span>
2. <span data-ttu-id="5e669-116">Oluşturma bir **Azure bulut hizmeti** hello projeden **bulut** .NET Framework 4. 5'i hedefleyen şablonu.</span><span class="sxs-lookup"><span data-stu-id="5e669-116">Create an **Azure Cloud Service** project from hello **Cloud** template that targets .NET Framework 4.5.</span></span>  <span data-ttu-id="5e669-117">Merhaba projeyi "WadExample" olarak adlandırın ve Tamam'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="5e669-117">Name hello project "WadExample" and click Ok.</span></span>
3. <span data-ttu-id="5e669-118">Seçin **çalışan rolü** ve Tamam'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="5e669-118">Select **Worker Role** and click Ok.</span></span> <span data-ttu-id="5e669-119">başlangıç projesi oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="5e669-119">hello project will be created.</span></span>
4. <span data-ttu-id="5e669-120">İçinde **Çözüm Gezgini**, hello çift **WorkerRole1** özellikleri dosya.</span><span class="sxs-lookup"><span data-stu-id="5e669-120">In **Solution Explorer**, double-click hello **WorkerRole1** properties file.</span></span>
5. <span data-ttu-id="5e669-121">Merhaba, **yapılandırma** sekmesinde, kaldırma onay **tanılamayı etkinleştir** toodisable tanılama 1.0 (Azure SDK 2.4 ve önceki).</span><span class="sxs-lookup"><span data-stu-id="5e669-121">In hello **Configuration** tab, un-check **Enable Diagnostics** toodisable Diagnostics 1.0 (Azure SDK 2.4 and earlier).</span></span>
6. <span data-ttu-id="5e669-122">Çözüm tooverify yapı hata vardır.</span><span class="sxs-lookup"><span data-stu-id="5e669-122">Build your solution tooverify that you have no errors.</span></span>

### <a name="step-2-instrument-your-code"></a><span data-ttu-id="5e669-123">2. adım: kodunuzu izleme</span><span class="sxs-lookup"><span data-stu-id="5e669-123">Step 2: Instrument your code</span></span>
<span data-ttu-id="5e669-124">WorkerRole.cs Merhaba içeriğine koddan hello ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="5e669-124">Replace hello contents of WorkerRole.cs with hello following code.</span></span> <span data-ttu-id="5e669-125">Merhaba devralınan sınıfı SampleEventSourceWriter, hello [EventSource sınıfı][EventSource Class], dört günlük yöntemlerini uygular: **SendEnums**, **MessageMethod** , **SetOther** ve **HighFreq**.</span><span class="sxs-lookup"><span data-stu-id="5e669-125">hello class SampleEventSourceWriter, inherited from hello [EventSource Class][EventSource Class], implements four logging methods: **SendEnums**, **MessageMethod**, **SetOther** and **HighFreq**.</span></span> <span data-ttu-id="5e669-126">İlk parametre toohello hello **WriteEvent** yöntemi hello ilgili olay hello kimliği tanımlar.</span><span class="sxs-lookup"><span data-stu-id="5e669-126">hello first parameter toohello **WriteEvent** method defines hello ID for hello respective event.</span></span> <span data-ttu-id="5e669-127">Merhaba Run yöntemi uygulayan her hello hello uygulanan günlük yöntemlerini çağıran sonsuz bir döngüde **SampleEventSourceWriter** 10 saniyede sınıfı.</span><span class="sxs-lookup"><span data-stu-id="5e669-127">hello Run method implements an infinite loop that calls each of hello logging methods implemented in hello **SampleEventSourceWriter** class every 10 seconds.</span></span>

```csharp
using Microsoft.WindowsAzure.ServiceRuntime;
using System;
using System.Diagnostics;
using System.Diagnostics.Tracing;
using System.Net;
using System.Threading;

namespace WorkerRole1
{
    sealed class SampleEventSourceWriter : EventSource
    {
        public static SampleEventSourceWriter Log = new SampleEventSourceWriter();
        public void SendEnums(MyColor color, MyFlags flags) { if (IsEnabled())  WriteEvent(1, (int)color, (int)flags); }// Cast enums tooint for efficient logging.
        public void MessageMethod(string Message) { if (IsEnabled())  WriteEvent(2, Message); }
        public void SetOther(bool flag, int myInt) { if (IsEnabled())  WriteEvent(3, flag, myInt); }
        public void HighFreq(int value) { if (IsEnabled()) WriteEvent(4, value); }

    }

    enum MyColor
    {
        Red,
        Blue,
        Green
    }

    [Flags]
    enum MyFlags
    {
        Flag1 = 1,
        Flag2 = 2,
        Flag3 = 4
    }

    public class WorkerRole : RoleEntryPoint
    {
        public override void Run()
        {
            // This is a sample worker implementation. Replace with your logic.
            Trace.TraceInformation("WorkerRole1 entry point called");

            int value = 0;

            while (true)
            {
                Thread.Sleep(10000);
                Trace.TraceInformation("Working");

                // Emit several events every time we go through hello loop
                for (int i = 0; i < 6; i++)
                {
                    SampleEventSourceWriter.Log.SendEnums(MyColor.Blue, MyFlags.Flag2 | MyFlags.Flag3);
                }

                for (int i = 0; i < 3; i++)
                {
                    SampleEventSourceWriter.Log.MessageMethod("This is a message.");
                    SampleEventSourceWriter.Log.SetOther(true, 123456789);
                }

                if (value == int.MaxValue) value = 0;
                SampleEventSourceWriter.Log.HighFreq(value++);
            }
        }

        public override bool OnStart()
        {
            // Set hello maximum number of concurrent connections
            ServicePointManager.DefaultConnectionLimit = 12;

            // For information on handling configuration changes
            // see hello MSDN topic at http://go.microsoft.com/fwlink/?LinkId=166357.

            return base.OnStart();
        }
    }
}
```


### <a name="step-3-deploy-your-worker-role"></a><span data-ttu-id="5e669-128">Adım 3: çalışan rolünüzün dağıtma</span><span class="sxs-lookup"><span data-stu-id="5e669-128">Step 3: Deploy your Worker Role</span></span>

[!INCLUDE [cloud-services-wad-warning](../../includes/cloud-services-wad-warning.md)]

1. <span data-ttu-id="5e669-129">Merhaba seçerek, çalışan rolü tooAzure gelen Visual Studio içinde dağıtmak **WadExample** sonra Çözüm Gezgini hello bir projede **Yayımla** hello gelen **yapı** menüsü.</span><span class="sxs-lookup"><span data-stu-id="5e669-129">Deploy your worker role tooAzure from within Visual Studio by selecting hello **WadExample** project in hello Solution Explorer then **Publish** from hello **Build** menu.</span></span>
2. <span data-ttu-id="5e669-130">Aboneliğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="5e669-130">Choose your subscription.</span></span>
3. <span data-ttu-id="5e669-131">Merhaba, **Microsoft Azure yayımlama ayarları** iletişim kutusunda **yeni oluştur...** .</span><span class="sxs-lookup"><span data-stu-id="5e669-131">In hello **Microsoft Azure Publish Settings** dialog, select **Create New…**.</span></span>
4. <span data-ttu-id="5e669-132">Merhaba, **bulut hizmeti oluşturma ve depolama hesabı** iletişim kutusunda, girin bir **adı** (örneğin, "WadExample") ve bir bölge veya benzeşim grubu seçin.</span><span class="sxs-lookup"><span data-stu-id="5e669-132">In hello **Create Cloud Service and Storage Account** dialog, enter a **Name** (for example, "WadExample") and select a region or affinity group.</span></span>
5. <span data-ttu-id="5e669-133">Set hello **ortam** çok**hazırlama**.</span><span class="sxs-lookup"><span data-stu-id="5e669-133">Set hello **Environment** too**Staging**.</span></span>
6. <span data-ttu-id="5e669-134">Diğer değiştirme **ayarları** olarak uygun ve tıklatın **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="5e669-134">Modify any other **Settings** as appropriate and click **Publish**.</span></span>
7. <span data-ttu-id="5e669-135">Merhaba, bulut hizmeti olan Azure Portalı'nda dağıtım tamamlandıktan sonra onaylayın bir **çalıştıran** durumu.</span><span class="sxs-lookup"><span data-stu-id="5e669-135">After deployment has completed, verify in hello Azure portal that your cloud service is in a **Running** state.</span></span>

### <a name="step-4-create-your-diagnostics-configuration-file-and-install-hello-extension"></a><span data-ttu-id="5e669-136">4. adım: Tanılama yapılandırma dosyanızı oluşturun ve hello uzantısını yükle</span><span class="sxs-lookup"><span data-stu-id="5e669-136">Step 4: Create your Diagnostics configuration file and install hello extension</span></span>
1. <span data-ttu-id="5e669-137">Merhaba ortak yapılandırma dosyası şeması tanımı hello aşağıdaki PowerShell komutunu yürüterek yükleyin:</span><span class="sxs-lookup"><span data-stu-id="5e669-137">Download hello public configuration file schema definition by executing hello following PowerShell command:</span></span>

    ```powershell
    (Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'
    ```
2. <span data-ttu-id="5e669-138">Bir XML dosyası tooyour ekleme **WorkerRole1** hello üzerinde sağ tıklanarak proje **WorkerRole1** proje ve seçin **Ekle** -> **yeni öğe...**</span><span class="sxs-lookup"><span data-stu-id="5e669-138">Add an XML file tooyour **WorkerRole1** project by right-clicking on hello **WorkerRole1** project and select **Add** -> **New Item…**</span></span><span data-ttu-id="5e669-139"> -> **Visual C# öğeleri** -> **veri** -> **XML dosyası**.</span><span class="sxs-lookup"><span data-stu-id="5e669-139"> -> **Visual C# items** -> **Data** -> **XML File**.</span></span> <span data-ttu-id="5e669-140">"WadExample.xml" Merhaba dosya adı.</span><span class="sxs-lookup"><span data-stu-id="5e669-140">Name hello file "WadExample.xml".</span></span>

   ![CloudServices_diag_add_xml](./media/cloud-services-dotnet-diagnostics/AddXmlFile.png)
3. <span data-ttu-id="5e669-142">Merhaba WadConfig.xsd hello yapılandırma dosyası ile ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="5e669-142">Associate hello WadConfig.xsd with hello configuration file.</span></span> <span data-ttu-id="5e669-143">Merhaba WadExample.xml Düzenleyicisi penceresinde hello etkin pencereyi olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="5e669-143">Make sure hello WadExample.xml editor window is hello active window.</span></span> <span data-ttu-id="5e669-144">Tuşuna **F4** tooopen hello **özellikleri** penceresi.</span><span class="sxs-lookup"><span data-stu-id="5e669-144">Press **F4** tooopen hello **Properties** window.</span></span> <span data-ttu-id="5e669-145">Merhaba tıklatın **şemaları** hello özelliğinde **özellikleri** penceresi.</span><span class="sxs-lookup"><span data-stu-id="5e669-145">Click hello **Schemas** property in hello **Properties** window.</span></span> <span data-ttu-id="5e669-146">Merhaba tıklatın **...**</span><span class="sxs-lookup"><span data-stu-id="5e669-146">Click hello **…**</span></span> <span data-ttu-id="5e669-147">Merhaba, **şemaları** özelliği.</span><span class="sxs-lookup"><span data-stu-id="5e669-147">in hello **Schemas** property.</span></span> <span data-ttu-id="5e669-148">Merhaba tıklatın **Ekle...**</span><span class="sxs-lookup"><span data-stu-id="5e669-148">Click hello **Add…**</span></span> <span data-ttu-id="5e669-149">düğme ve hello XSD dosyası ve select hello dosya WadConfig.xsd kaydettiğiniz toohello konuma gidin.</span><span class="sxs-lookup"><span data-stu-id="5e669-149">button and navigate toohello location where you saved hello XSD file and select hello file WadConfig.xsd.</span></span> <span data-ttu-id="5e669-150">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5e669-150">Click **OK**.</span></span>

4. <span data-ttu-id="5e669-151">Merhaba WadExample.xml yapılandırma dosyası Hello içeriğini hello dosyayı Kaydet XML aşağıdaki hello ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="5e669-151">Replace hello contents of hello WadExample.xml configuration file with hello following XML and save hello file.</span></span> <span data-ttu-id="5e669-152">Bu yapılandırma dosyası birkaç performans sayaçları toocollect tanımlar: CPU kullanımı, diğeri bellek kullanımı için.</span><span class="sxs-lookup"><span data-stu-id="5e669-152">This configuration file defines a couple performance counters toocollect: one for CPU utilization and one for memory utilization.</span></span> <span data-ttu-id="5e669-153">Ardından hello yapılandırmasını hello SampleEventSourceWriter sınıfı toohello yöntemleri karşılık gelen hello dört olayları tanımlar.</span><span class="sxs-lookup"><span data-stu-id="5e669-153">Then hello configuration defines hello four events corresponding toohello methods in hello SampleEventSourceWriter class.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <WadCfg>
    <DiagnosticMonitorConfiguration overallQuotaInMB="25000">
      <PerformanceCounters scheduledTransferPeriod="PT1M">
        <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT1M" unit="percent" />
        <PerformanceCounterConfiguration counterSpecifier="\Memory\Committed Bytes" sampleRate="PT1M" unit="bytes"/>
      </PerformanceCounters>
      <EtwProviders>
        <EtwEventSourceProviderConfiguration provider="SampleEventSourceWriter" scheduledTransferPeriod="PT5M">
          <Event id="1" eventDestination="EnumsTable"/>
          <Event id="2" eventDestination="MessageTable"/>
          <Event id="3" eventDestination="SetOtherTable"/>
          <Event id="4" eventDestination="HighFreqTable"/>
          <DefaultEvents eventDestination="DefaultTable" />
        </EtwEventSourceProviderConfiguration>
      </EtwProviders>
    </DiagnosticMonitorConfiguration>
  </WadCfg>
</PublicConfig>
```

### <a name="step-5-install-diagnostics-on-your-worker-role"></a><span data-ttu-id="5e669-154">5. adım: Tanılama, çalışan rolü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="5e669-154">Step 5: Install Diagnostics on your Worker Role</span></span>
<span data-ttu-id="5e669-155">Merhaba tanılama bir web veya çalışan rolü yönetmek için PowerShell cmdlet'leri şunlardır: Set-AzureServiceDiagnosticsExtension, Get-AzureServiceDiagnosticsExtension ve Kaldır-AzureServiceDiagnosticsExtension.</span><span class="sxs-lookup"><span data-stu-id="5e669-155">hello PowerShell cmdlets for managing Diagnostics on a web or worker role are: Set-AzureServiceDiagnosticsExtension, Get-AzureServiceDiagnosticsExtension, and Remove-AzureServiceDiagnosticsExtension.</span></span>

1. <span data-ttu-id="5e669-156">Azure PowerShell'i açın.</span><span class="sxs-lookup"><span data-stu-id="5e669-156">Open Azure PowerShell.</span></span>
2. <span data-ttu-id="5e669-157">Çalışan rolünüzün Hello betik tooinstall tanılama yürütme (Değiştir *StorageAccountKey* hello depolama hesabınızın anahtarıyla wadexample depolama hesabınız için ve *config_path* hello yolu ile toohello *WadExample.xml* dosyası):</span><span class="sxs-lookup"><span data-stu-id="5e669-157">Execute hello script tooinstall Diagnostics on your worker role (replace *StorageAccountKey* with hello storage account key for your wadexample storage account and *config_path* with hello path toohello *WadExample.xml* file):</span></span>

```powershell
$storage_name = "wadexample"
$key = "<StorageAccountKey>"
$config_path="c:\users\<user>\documents\visual studio 2013\Projects\WadExample\WorkerRole1\WadExample.xml"
$service_name="wadexample"
$storageContext = New-AzureStorageContext -StorageAccountName $storage_name -StorageAccountKey $key
Set-AzureServiceDiagnosticsExtension -StorageContext $storageContext -DiagnosticsConfigurationPath $config_path -ServiceName $service_name -Slot Staging -Role WorkerRole1
```

### <a name="step-6-look-at-your-telemetry-data"></a><span data-ttu-id="5e669-158">6. adım: Telemetri verilerinizi bakma</span><span class="sxs-lookup"><span data-stu-id="5e669-158">Step 6: Look at your telemetry data</span></span>
<span data-ttu-id="5e669-159">Merhaba Visual Studio içinde **Sunucu Gezgini**, toohello wadexample depolama hesabına gidin.</span><span class="sxs-lookup"><span data-stu-id="5e669-159">In hello Visual Studio **Server Explorer**, navigate toohello wadexample storage account.</span></span> <span data-ttu-id="5e669-160">Yaklaşık beş (5) dakika Hello bulut hizmeti yürütüldükten sonra hello tabloları görmelisiniz **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** ve **WADSetOtherTable**.</span><span class="sxs-lookup"><span data-stu-id="5e669-160">After hello cloud service has been running about five (5) minutes, you should see hello tables **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** and **WADSetOtherTable**.</span></span> <span data-ttu-id="5e669-161">Toplanan hello tabloları tooview hello telemetri birini çift tıklatın.</span><span class="sxs-lookup"><span data-stu-id="5e669-161">Double-click one of hello tables tooview hello telemetry that has been collected.</span></span>

![CloudServices_diag_tables](./media/cloud-services-dotnet-diagnostics/WadExampleTables.png)

## <a name="configuration-file-schema"></a><span data-ttu-id="5e669-163">Yapılandırma dosyası şeması</span><span class="sxs-lookup"><span data-stu-id="5e669-163">Configuration File Schema</span></span>
<span data-ttu-id="5e669-164">Merhaba tanılama yapılandırma dosyası hello Tanılama aracı başladığında kullanılan tooinitialize tanılama yapılandırma ayarlarının değerleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="5e669-164">hello Diagnostics configuration file defines values that are used tooinitialize diagnostic configuration settings when hello diagnostics agent starts.</span></span> <span data-ttu-id="5e669-165">Merhaba bkz [en son şema başvurusu](https://msdn.microsoft.com/library/azure/mt634524.aspx) geçerli değerler ve örnekler için.</span><span class="sxs-lookup"><span data-stu-id="5e669-165">See hello [latest schema reference](https://msdn.microsoft.com/library/azure/mt634524.aspx) for valid values and examples.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="5e669-166">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="5e669-166">Troubleshooting</span></span>
<span data-ttu-id="5e669-167">Konusunda sorun yaşıyorsanız, bkz: [sorun giderme Azure tanılama](../azure-diagnostics-troubleshooting.md) sık karşılaşılan sorunları ile ilgili Yardım.</span><span class="sxs-lookup"><span data-stu-id="5e669-167">If you have trouble, see [Troubleshooting Azure Diagnostics](../azure-diagnostics-troubleshooting.md) for help with common problems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e669-168">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="5e669-168">Next Steps</span></span>
<span data-ttu-id="5e669-169">[İlgili Azure sanal makinesi tanılama makaleler listesini görmek](../monitoring-and-diagnostics/azure-diagnostics.md#cloud-services-using-azure-diagnostics) toochange hello verileri toplama, sorunları gidermek veya Tanılama hakkında daha fazla genel bilgi.</span><span class="sxs-lookup"><span data-stu-id="5e669-169">[See a list of related Azure virtual-machine diagnostic articles](../monitoring-and-diagnostics/azure-diagnostics.md#cloud-services-using-azure-diagnostics) toochange hello data you are collecting, troubleshoot problems or learn more about diagnostics in general.</span></span>

[EventSource Class]: http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource(v=vs.110).aspx

[Debugging an Azure Application]: http://msdn.microsoft.com/library/windowsazure/ee405479.aspx   
[Collect Logging Data by Using Azure Diagnostics]: http://msdn.microsoft.com/library/windowsazure/gg433048.aspx
[Free Trial]: http://azure.microsoft.com/pricing/free-trial/
[Install and configure Azure PowerShell version 0.8.7 or later]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/
