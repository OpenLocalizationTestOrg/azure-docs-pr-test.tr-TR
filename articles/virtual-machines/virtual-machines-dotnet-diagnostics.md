---
title: "Sanal makinelerin Azure Tanılama'yı kullanma | Microsoft Docs"
description: "Hata ayıklama, performans, izleme, trafik analizi ve daha fazla ölçmek için Azure sanal makinelerden veri toplamak üzere Azure Tanılama'yı kullanarak."
services: virtual-machines
documentationcenter: .net
author: davidmu1
manager: 
editor: 
ms.assetid: dfaabc7a-23e7-4af0-8369-f504d2915b3d
ms.service: virtual-machines
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/16/2016
ms.author: davidmu
ms.openlocfilehash: 8ff6b9825212359617b748aba1c78ed789b130dd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="enabling-diagnostics-in-azure-virtual-machines"></a><span data-ttu-id="3a64a-103">Azure sanal makinelerde tanılama etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="3a64a-103">Enabling Diagnostics in Azure Virtual Machines</span></span>
<span data-ttu-id="3a64a-104">Bkz: [Azure tanılama genel bakış](../monitoring-and-diagnostics/azure-diagnostics.md) bir arka planda Azure tanılama için.</span><span class="sxs-lookup"><span data-stu-id="3a64a-104">See [Azure Diagnostics Overview](../monitoring-and-diagnostics/azure-diagnostics.md) for a background on Azure Diagnostics.</span></span>

## <a name="how-to-enable-diagnostics-in-a-virtual-machine"></a><span data-ttu-id="3a64a-105">Bir sanal makinede tanılamayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="3a64a-105">How to Enable Diagnostics in a Virtual Machine</span></span>
<span data-ttu-id="3a64a-106">Bu ilerlemesi aracılığıyla uzaktan tanılama bir Azure sanal makinesi için bir geliştirme bilgisayardan nasıl yükleneceğini açıklar.</span><span class="sxs-lookup"><span data-stu-id="3a64a-106">This walk through describes how to remotely install Diagnostics to an Azure virtual machine from a development computer.</span></span> <span data-ttu-id="3a64a-107">Bu Azure sanal makine üzerinde çalışan ve .NET ile telemetri verilerini yayar uygulamanın uygulama da bilgi [EventSource sınıfı][EventSource Class].</span><span class="sxs-lookup"><span data-stu-id="3a64a-107">You also learn how to implement an application that runs on that Azure virtual machine and emits telemetry data using the .NET [EventSource Class][EventSource Class].</span></span> <span data-ttu-id="3a64a-108">Azure tanılama telemetri toplamak ve bir Azure depolama hesabında depolamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3a64a-108">Azure Diagnostics is used to collect the telemetry and store it in an Azure storage account.</span></span>

### <a name="pre-requisites"></a><span data-ttu-id="3a64a-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="3a64a-109">Pre-requisites</span></span>
<span data-ttu-id="3a64a-110">Bir Azure aboneliğiniz varsa ve Azure SDK ile Visual Studio 2017 kullanıyorsanız bu ilerlemesi aracılığıyla varsayar.</span><span class="sxs-lookup"><span data-stu-id="3a64a-110">This walk through assumes you have an Azure subscription and are using Visual Studio 2017 with the Azure SDK.</span></span> <span data-ttu-id="3a64a-111">Bir Azure aboneliğiniz yoksa için kaydolabilirsiniz [ücretsiz deneme][Free Trial].</span><span class="sxs-lookup"><span data-stu-id="3a64a-111">If you do not have an Azure subscription, you can sign up for the [Free Trial][Free Trial].</span></span> <span data-ttu-id="3a64a-112">Emin olun [yükleyin ve Azure PowerShell sürüm 0.8.7 yapılandırın veya daha sonra][Install and configure Azure PowerShell version 0.8.7 or later].</span><span class="sxs-lookup"><span data-stu-id="3a64a-112">Make sure to [Install and configure Azure PowerShell version 0.8.7 or later][Install and configure Azure PowerShell version 0.8.7 or later].</span></span>

### <a name="step-1-create-a-virtual-machine"></a><span data-ttu-id="3a64a-113">1. adım: bir sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="3a64a-113">Step 1: Create a Virtual Machine</span></span>
1. <span data-ttu-id="3a64a-114">Geliştirme bilgisayarınızda Visual Studio 2017 başlatın.</span><span class="sxs-lookup"><span data-stu-id="3a64a-114">On your development computer, launch Visual Studio 2017.</span></span>
2. <span data-ttu-id="3a64a-115">Visual Studio'da **Sunucu Gezgini** genişletin **Azure**, sağ **sanal makineleri** seçip **sanal makine oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="3a64a-115">In the Visual Studio **Server Explorer** expand **Azure**, right-click **Virtual Machines** then select **Create Virtual Machine**.</span></span>
3. <span data-ttu-id="3a64a-116">Azure aboneliğinizde seçin **bir abonelik seçin** tıklayın ve iletişim **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="3a64a-116">Select your Azure subscription in the **Choose a Subscription** dialog and click **Next**.</span></span>
4. <span data-ttu-id="3a64a-117">Seçin **Windows Server 2012 R2 Datacenter, Haziran 2017** içinde **bir sanal makine görüntüsü seçin** tıklayın ve iletişim **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="3a64a-117">Select **Windows Server 2012 R2 Datacenter, June 2017** in the **Select a Virtual Machine Image** dialog and click **Next**.</span></span>
5. <span data-ttu-id="3a64a-118">İçinde **sanal makine temel ayarlarını**, sanal makine adı "wadexample" olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="3a64a-118">In the **Virtual Machine Basic Settings**, set the virtual machine name to "wadexample".</span></span> <span data-ttu-id="3a64a-119">Yönetici kullanıcı adı ve parola ayarlayın ve tıklayın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="3a64a-119">Set your Administrator user name and password and click **Next**.</span></span>
6. <span data-ttu-id="3a64a-120">İçinde **bulut hizmeti ayarlarını** "wadexampleVM" adlı yeni bir bulut hizmeti Oluştur iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="3a64a-120">In the **Cloud Service Settings** dialog create a new cloud service named "wadexampleVM".</span></span> <span data-ttu-id="3a64a-121">"Wadexample" adlı yeni bir depolama hesabı oluşturmak ve tıklayın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="3a64a-121">Create a new Storage account named "wadexample" and click **Next**.</span></span>
7. <span data-ttu-id="3a64a-122">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3a64a-122">Click **Create**.</span></span>

### <a name="step-2-create-your-application"></a><span data-ttu-id="3a64a-123">2. adım: uygulamanızı oluşturma</span><span class="sxs-lookup"><span data-stu-id="3a64a-123">Step 2: Create your Application</span></span>
1. <span data-ttu-id="3a64a-124">Geliştirme bilgisayarınızda Visual Studio 2017 başlatın.</span><span class="sxs-lookup"><span data-stu-id="3a64a-124">On your development computer, launch Visual Studio 2017.</span></span>
2. <span data-ttu-id="3a64a-125">Yeni bir Visual C# konsol .NET Framework 4. 5'i hedefleyen uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3a64a-125">Create a new Visual C# Console Application that targets .NET Framework 4.5.</span></span> <span data-ttu-id="3a64a-126">Projeyi "WadExampleVM" olarak adlandırın.</span><span class="sxs-lookup"><span data-stu-id="3a64a-126">Name the project "WadExampleVM".</span></span>

   ![CloudServices_diag_new_project](./media/virtual-machines-dotnet-diagnostics/NewProject.png)
3. <span data-ttu-id="3a64a-128">Program.cs içeriğini aşağıdaki kodla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="3a64a-128">Replace the contents of Program.cs with the following code.</span></span> <span data-ttu-id="3a64a-129">Sınıf **SampleEventSourceWriter** dört günlük yöntemlerini uygular: **SendEnums**, **MessageMethod**, **SetOther** ve  **HighFreq**.</span><span class="sxs-lookup"><span data-stu-id="3a64a-129">The class **SampleEventSourceWriter** implements four logging methods: **SendEnums**, **MessageMethod**, **SetOther** and **HighFreq**.</span></span> <span data-ttu-id="3a64a-130">İlk parametre WriteEvent yöntemi olarak ilgili olay kimliği tanımlar.</span><span class="sxs-lookup"><span data-stu-id="3a64a-130">The first parameter to the WriteEvent method defines the ID for the respective event.</span></span> <span data-ttu-id="3a64a-131">Run yöntemi uygulanan günlük yöntemlerin her biri çağırır sonsuz bir döngüde uygulayan **SampleEventSourceWriter** 10 saniyede sınıfı.</span><span class="sxs-lookup"><span data-stu-id="3a64a-131">The Run method implements an infinite loop that calls each of the logging methods implemented in the **SampleEventSourceWriter** class every 10 seconds.</span></span>

    ```csharp
     using System;
     using System.Diagnostics;
     using System.Diagnostics.Tracing;
     using System.Threading;

     namespace WadExampleVM
     {
       sealed class SampleEventSourceWriter : EventSource {
         public static SampleEventSourceWriter Log = new SampleEventSourceWriter();
         public void SendEnums(MyColor color, MyFlags flags) { if (IsEnabled())  WriteEvent(1, (int)color, (int)flags); } // Cast enums to int for efficient logging.
         public void MessageMethod(string Message) { if (IsEnabled())  WriteEvent(2, Message); }
         public void SetOther(bool flag, int myInt) { if (IsEnabled())  WriteEvent(3, flag, myInt); }
         public void HighFreq(int value) { if (IsEnabled()) WriteEvent(4, value); }
       }

       enum MyColor {
         Red,
         Blue,
         Green
       }

       [Flags]
       enum MyFlags {
         Flag1 = 1,
         Flag2 = 2,
         Flag3 = 4
       }

       class Program
       {
         static void Main(string[] args) {
         Trace.TraceInformation("My application entry point called");

         int value = 0;

         while (true) {
             Thread.Sleep(10000);
             Trace.TraceInformation("Working");

             // Emit several events every time we go through the loop
             for (int i = 0; i < 6; i++) {
                 SampleEventSourceWriter.Log.SendEnums(MyColor.Blue, MyFlags.Flag2 | MyFlags.Flag3);
             }

             for (int i = 0; i < 3; i++) {
                 SampleEventSourceWriter.Log.MessageMethod("This is a message.");
                 SampleEventSourceWriter.Log.SetOther(true, 123456789);
             }

             if (value == int.MaxValue) value = 0;
             SampleEventSourceWriter.Log.HighFreq(value++);
         }

        }
      }
     }
     ```
4. <span data-ttu-id="3a64a-132">Dosyayı kaydedin ve seçin **yapı çözümü** gelen **yapı** kodunuzu oluşturmak için menüsü.</span><span class="sxs-lookup"><span data-stu-id="3a64a-132">Save the file and select **Build Solution** from the **Build** menu to build your code.</span></span>

### <a name="step-3-deploy-your-application"></a><span data-ttu-id="3a64a-133">3. adım: uygulamanızı dağıtma</span><span class="sxs-lookup"><span data-stu-id="3a64a-133">Step 3: Deploy your Application</span></span>
1. <span data-ttu-id="3a64a-134">Sağ tıklayın **WadExampleVM** proje **Çözüm Gezgini** ve **dosya Gezgini'nde klasör Aç**.</span><span class="sxs-lookup"><span data-stu-id="3a64a-134">Right-click on the **WadExampleVM** project in **Solution Explorer** and choose **Open Folder in File Explorer**.</span></span>
2. <span data-ttu-id="3a64a-135">Gidin *bin\Debug* klasör ve tüm dosyalar (WadExampleVM.*) kopyalayın</span><span class="sxs-lookup"><span data-stu-id="3a64a-135">Navigate to the *bin\Debug* folder and copy all the files (WadExampleVM.*)</span></span>
3. <span data-ttu-id="3a64a-136">İçinde **Sunucu Gezgini** sanal makineye sağ tıklayın ve seçin **Uzak Masaüstü kullanarak bağlanmak**.</span><span class="sxs-lookup"><span data-stu-id="3a64a-136">In **Server Explorer** right-click on the virtual machine and choose **Connect using Remote Desktop**.</span></span>
4. <span data-ttu-id="3a64a-137">VM bağlandıktan sonra WadExampleVM ve uygulamanızı klasöre dosyaları Yapıştır adlı bir klasör oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3a64a-137">Once connected to the VM create a folder named WadExampleVM and paste your application files into the folder.</span></span>
5. <span data-ttu-id="3a64a-138">Uygulama WadExampleVM.exe başlatın.</span><span class="sxs-lookup"><span data-stu-id="3a64a-138">Launch the application WadExampleVM.exe.</span></span> <span data-ttu-id="3a64a-139">Boş konsol penceresini görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="3a64a-139">You should see a blank console window.</span></span>

### <a name="step-4-create-your-diagnostics-configuration-and-install-the-extension"></a><span data-ttu-id="3a64a-140">4. adım: Tanılama yapılandırmanızı oluşturun ve uzantısını yükle</span><span class="sxs-lookup"><span data-stu-id="3a64a-140">Step 4: Create your Diagnostics configuration and install the Extension</span></span>
1. <span data-ttu-id="3a64a-141">Genel yapılandırma dosyası şeması tanımı aşağıdaki PowerShell komutunu yürüterek geliştirme bilgisayarınıza indirin:</span><span class="sxs-lookup"><span data-stu-id="3a64a-141">Download the public configuration file schema definition to your development computer by executing the following PowerShell command:</span></span>

     <span data-ttu-id="3a64a-142">(Get-AzureServiceAvailableExtension - UzantıAdı 'PaaSDiagnostics' - ProviderNamespace 'Microsoft.Azure.Diagnostics'). PublicConfigurationSchema | Out-File-kodlama utf8 - FilePath 'WadConfig.xsd'</span><span class="sxs-lookup"><span data-stu-id="3a64a-142">(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'</span></span>
2. <span data-ttu-id="3a64a-143">Visual Studio'da, zaten açık veya Visual Studio'da örnek projesinde açık projeler ile ya da yeni bir XML dosyası açın.</span><span class="sxs-lookup"><span data-stu-id="3a64a-143">Open a new XML file in Visual Studio, either in a project you already have open or in a Visual Studio instance with no open projects.</span></span> <span data-ttu-id="3a64a-144">Visual Studio'da seçin **Ekle** -> **yeni öğe...**</span><span class="sxs-lookup"><span data-stu-id="3a64a-144">In Visual Studio, select **Add** -> **New Item…**</span></span><span data-ttu-id="3a64a-145"> -> **Visual C# öğeleri** -> **veri** -> **XML dosyası**.</span><span class="sxs-lookup"><span data-stu-id="3a64a-145"> -> **Visual C# items** -> **Data** -> **XML File**.</span></span> <span data-ttu-id="3a64a-146">"WadExample.xml" dosya adı</span><span class="sxs-lookup"><span data-stu-id="3a64a-146">Name the file "WadExample.xml"</span></span>
3. <span data-ttu-id="3a64a-147">WadConfig.xsd yapılandırma dosyası ile ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="3a64a-147">Associate the WadConfig.xsd with the configuration file.</span></span> <span data-ttu-id="3a64a-148">Etkin pencereyi WadExample.xml Düzenleyicisi penceresini olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="3a64a-148">Make sure the WadExample.xml editor window is the active window.</span></span> <span data-ttu-id="3a64a-149">Tuşuna **F4** açmak için **özellikleri** penceresi.</span><span class="sxs-lookup"><span data-stu-id="3a64a-149">Press **F4** to open the **Properties** window.</span></span> <span data-ttu-id="3a64a-150">Tıklayın **şemaları** özelliğinde **özellikleri** penceresi.</span><span class="sxs-lookup"><span data-stu-id="3a64a-150">Click on the **Schemas** property in the **Properties** window.</span></span> <span data-ttu-id="3a64a-151">Tıklatın **...**</span><span class="sxs-lookup"><span data-stu-id="3a64a-151">Click the **…**</span></span> <span data-ttu-id="3a64a-152">içinde **şemaları** özelliği.</span><span class="sxs-lookup"><span data-stu-id="3a64a-152">in the **Schemas** property.</span></span> <span data-ttu-id="3a64a-153">**Ekle…** düğmesine</span><span class="sxs-lookup"><span data-stu-id="3a64a-153">Click the **Add…**</span></span> <span data-ttu-id="3a64a-154">düğmesini ve XSD dosyasını kaydettiğiniz konuma gidin ve WadConfig.xsd dosyasını seçin.</span><span class="sxs-lookup"><span data-stu-id="3a64a-154">button and navigate to the location where you saved the XSD file and select the file WadConfig.xsd.</span></span> <span data-ttu-id="3a64a-155">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3a64a-155">Click **OK**.</span></span>
4. <span data-ttu-id="3a64a-156">Aşağıdaki XML WadExample.xml yapılandırma dosyasının içeriğini değiştirin ve dosyayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="3a64a-156">Replace the contents of the WadExample.xml configuration file with the following XML and save the file.</span></span> <span data-ttu-id="3a64a-157">Bu yapılandırma dosyasını toplamak için birkaç performans sayaçlarını tanımlar: CPU kullanımı, diğeri bellek kullanımı için.</span><span class="sxs-lookup"><span data-stu-id="3a64a-157">This configuration file defines a couple performance counters to collect: one for CPU utilization and one for memory utilization.</span></span> <span data-ttu-id="3a64a-158">Ardından yapılandırmasını SampleEventSourceWriter sınıftaki yöntemlerin karşılık gelen dört olayları tanımlar.</span><span class="sxs-lookup"><span data-stu-id="3a64a-158">Then the configuration defines the four events corresponding to the methods in the SampleEventSourceWriter class.</span></span>

```
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

### <a name="step-5-remotely-install-diagnostics-on-your-azure-virtual-machine"></a><span data-ttu-id="3a64a-159">5. adım: Azure sanal makinenize tanılama uzaktan yükleyin.</span><span class="sxs-lookup"><span data-stu-id="3a64a-159">Step 5: Remotely install Diagnostics on your Azure Virtual Machine</span></span>
<span data-ttu-id="3a64a-160">Bir VM'de tanılama yönetmek için PowerShell cmdlet'leri şunlardır: Set-AzureVMDiagnosticsExtension, Get-AzureVMDiagnosticsExtension ve Kaldır-AzureVMDiagnosticsExtension.</span><span class="sxs-lookup"><span data-stu-id="3a64a-160">The PowerShell cmdlets for managing Diagnostics on a VM are: Set-AzureVMDiagnosticsExtension, Get-AzureVMDiagnosticsExtension, and Remove-AzureVMDiagnosticsExtension.</span></span>

1. <span data-ttu-id="3a64a-161">Geliştirici bilgisayarınızda Azure PowerShell açın.</span><span class="sxs-lookup"><span data-stu-id="3a64a-161">On your developer computer, open Azure PowerShell.</span></span>
2. <span data-ttu-id="3a64a-162">Tanılama VM üzerinde uzaktan yüklemek için komut dosyası yürütme (Değiştir `<user>` kullanıcı dizin adı.</span><span class="sxs-lookup"><span data-stu-id="3a64a-162">Execute the script to remotely install Diagnostics on your VM (Replace `<user>` with your user directory name.</span></span> <span data-ttu-id="3a64a-163">Değiştir `<StorageAccountKey>` wadexamplevm depolama hesabınız için depolama hesabınızın anahtarıyla):</span><span class="sxs-lookup"><span data-stu-id="3a64a-163">Replace `<StorageAccountKey>` with the storage account key for your wadexamplevm storage account):</span></span>
```
     $storage_name = "wadexamplevm"
     $key = "<StorageAccountKey>"
     $config_path="c:\users\<user>\documents\visual studio 2017\Projects\WadExampleVM\WadExampleVM\WadExample.xml"
     $service_name="wadexamplevm"
     $vm_name="WadExample"
     $storageContext = New-AzureStorageContext -StorageAccountName $storage_name -StorageAccountKey $key
     $VM1 = Get-AzureVM -ServiceName $service_name -Name $vm_name
     $VM2 = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $config_path -Version "1.*" -VM $VM1 -StorageContext $storageContext
     $VM3 = Update-AzureVM -ServiceName $service_name -Name $vm_name -VM $VM2.VM
```
### <a name="step-6-look-at-your-telemetry-data"></a><span data-ttu-id="3a64a-164">6. adım: Telemetri verilerinizi bakma</span><span class="sxs-lookup"><span data-stu-id="3a64a-164">Step 6: Look at your telemetry data</span></span>
<span data-ttu-id="3a64a-165">Visual Studio'da **Sunucu Gezgini** wadexample depolama hesabınıza gidin.</span><span class="sxs-lookup"><span data-stu-id="3a64a-165">In the Visual Studio **Server Explorer** navigate to the wadexample storage account.</span></span> <span data-ttu-id="3a64a-166">VM yaklaşık 5 dakika yürütüldükten sonra tabloları görmelisiniz **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**,  **WADPerformanceCountersTable** ve **WADSetOtherTable**.</span><span class="sxs-lookup"><span data-stu-id="3a64a-166">After the VM has been running about 5 minutes you should see the tables **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** and **WADSetOtherTable**.</span></span> <span data-ttu-id="3a64a-167">Toplanan telemetri görüntülemek için tablolar birine çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3a64a-167">Double-click on one of the tables to view the telemetry that has been collected.</span></span>

![CloudServices_diag_wadexamplevm_tables](./media/virtual-machines-dotnet-diagnostics/WadExampleVMTables.png)

## <a name="configuration-file-schema"></a><span data-ttu-id="3a64a-169">Yapılandırma dosyası şeması</span><span class="sxs-lookup"><span data-stu-id="3a64a-169">Configuration file schema</span></span>
<span data-ttu-id="3a64a-170">Tanılama yapılandırma dosyası Tanılama aracı başladığında tanılama yapılandırma ayarlarını başlatmak için kullanılan değerleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="3a64a-170">The Diagnostics configuration file defines values that are used to initialize diagnostic configuration settings when the diagnostics agent starts.</span></span> <span data-ttu-id="3a64a-171">Bkz: [en son şema başvurusu](https://msdn.microsoft.com/library/azure/mt634524.aspx) geçerli değerler ve örnekler için.</span><span class="sxs-lookup"><span data-stu-id="3a64a-171">See the [latest schema reference](https://msdn.microsoft.com/library/azure/mt634524.aspx) for valid values and examples.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="3a64a-172">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="3a64a-172">Troubleshooting</span></span>
<span data-ttu-id="3a64a-173">Bkz: [sorun giderme Azure tanılama](../monitoring-and-diagnostics/azure-diagnostics-troubleshooting.md) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="3a64a-173">See [Troubleshooting Azure Diagnostics](../monitoring-and-diagnostics/azure-diagnostics-troubleshooting.md) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3a64a-174">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3a64a-174">Next steps</span></span>
<span data-ttu-id="3a64a-175">[Bkz: sanal makine listesini makaleler Azure tanılama](../monitoring-and-diagnostics/azure-diagnostics.md#virtual-machines-using-azure-diagnostics) toplama verileri değiştirmek için ilgili sorunları giderme veya Tanılama hakkında daha fazla genel bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="3a64a-175">[See a list of virtual machine related Azure Diagnostics articles](../monitoring-and-diagnostics/azure-diagnostics.md#virtual-machines-using-azure-diagnostics) to change the data you are collecting, troubleshoot problems or learn more about diagnostics in general.</span></span>

[EventSource Class]: http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource(v=vs.110).aspx

[Debugging an Azure Application]: http://msdn.microsoft.com/library/windowsazure/ee405479.aspx   
[Collect Logging Data by Using Azure Diagnostics]: http://msdn.microsoft.com/library/windowsazure/gg433048.aspx
[Free Trial]: http://azure.microsoft.com/pricing/free-trial/
[Install and configure Azure PowerShell version 0.8.7 or later]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/
