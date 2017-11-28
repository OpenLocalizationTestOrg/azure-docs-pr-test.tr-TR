---
title: "aaaHow toouse sanal makinelerinde Azure tanılama | Microsoft Docs"
description: "Azure tanılama toogather verilerini Azure sanal makineleri gelen hata ayıklama, performans, izleme, trafik analizi ve daha fazla ölçmek için kullanma."
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
ms.openlocfilehash: 54cdfd30d7bbbb71af449826e90234faf5ecdf44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-diagnostics-in-azure-virtual-machines"></a><span data-ttu-id="5fc0d-103">Azure sanal makinelerde tanılama etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="5fc0d-103">Enabling Diagnostics in Azure Virtual Machines</span></span>
<span data-ttu-id="5fc0d-104">Bkz: [Azure tanılama genel bakış](../monitoring-and-diagnostics/azure-diagnostics.md) bir arka planda Azure tanılama için.</span><span class="sxs-lookup"><span data-stu-id="5fc0d-104">See [Azure Diagnostics Overview](../monitoring-and-diagnostics/azure-diagnostics.md) for a background on Azure Diagnostics.</span></span>

## <a name="how-tooenable-diagnostics-in-a-virtual-machine"></a><span data-ttu-id="5fc0d-105">Nasıl tooEnable bir sanal makinede tanılama</span><span class="sxs-lookup"><span data-stu-id="5fc0d-105">How tooEnable Diagnostics in a Virtual Machine</span></span>
<span data-ttu-id="5fc0d-106">Bu ilerlemesi üzerinden nasıl tooremotely yükleme tanılama tooan Azure sanal makinesi bir geliştirme bilgisayardan açıklar.</span><span class="sxs-lookup"><span data-stu-id="5fc0d-106">This walk through describes how tooremotely install Diagnostics tooan Azure virtual machine from a development computer.</span></span> <span data-ttu-id="5fc0d-107">Nasıl tooimplement, Azure sanal makinede çalışan ve telemetri verilerini kullanarak yayar bir uygulama hello .NET da bilgi [EventSource sınıfı][EventSource Class].</span><span class="sxs-lookup"><span data-stu-id="5fc0d-107">You also learn how tooimplement an application that runs on that Azure virtual machine and emits telemetry data using hello .NET [EventSource Class][EventSource Class].</span></span> <span data-ttu-id="5fc0d-108">Azure tanılama kullanılan toocollect hello telemetri olduğundan ve bir Azure depolama hesabında saklayın.</span><span class="sxs-lookup"><span data-stu-id="5fc0d-108">Azure Diagnostics is used toocollect hello telemetry and store it in an Azure storage account.</span></span>

### <a name="pre-requisites"></a><span data-ttu-id="5fc0d-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="5fc0d-109">Pre-requisites</span></span>
<span data-ttu-id="5fc0d-110">Bir Azure aboneliğiniz varsa ve Visual Studio 2017 hello Azure SDK'sı ile kullanıyorsanız bu ilerlemesi aracılığıyla varsayar.</span><span class="sxs-lookup"><span data-stu-id="5fc0d-110">This walk through assumes you have an Azure subscription and are using Visual Studio 2017 with hello Azure SDK.</span></span> <span data-ttu-id="5fc0d-111">Bir Azure aboneliğiniz yoksa, hello için kaydolabilirsiniz [ücretsiz deneme][Free Trial].</span><span class="sxs-lookup"><span data-stu-id="5fc0d-111">If you do not have an Azure subscription, you can sign up for hello [Free Trial][Free Trial].</span></span> <span data-ttu-id="5fc0d-112">Emin olun çok[yükleyin ve Azure PowerShell sürüm 0.8.7 yapılandırın veya daha sonra][Install and configure Azure PowerShell version 0.8.7 or later].</span><span class="sxs-lookup"><span data-stu-id="5fc0d-112">Make sure too[Install and configure Azure PowerShell version 0.8.7 or later][Install and configure Azure PowerShell version 0.8.7 or later].</span></span>

### <a name="step-1-create-a-virtual-machine"></a><span data-ttu-id="5fc0d-113">1. adım: bir sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="5fc0d-113">Step 1: Create a Virtual Machine</span></span>
1. <span data-ttu-id="5fc0d-114">Geliştirme bilgisayarınızda Visual Studio 2017 başlatın.</span><span class="sxs-lookup"><span data-stu-id="5fc0d-114">On your development computer, launch Visual Studio 2017.</span></span>
2. <span data-ttu-id="5fc0d-115">Merhaba Visual Studio içinde **Sunucu Gezgini** genişletin **Azure**, sağ **sanal makineleri** seçip **sanal makine oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="5fc0d-115">In hello Visual Studio **Server Explorer** expand **Azure**, right-click **Virtual Machines** then select **Create Virtual Machine**.</span></span>
3. <span data-ttu-id="5fc0d-116">Hello Azure aboneliğinizi seçin **bir abonelik seçin** tıklayın ve iletişim **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="5fc0d-116">Select your Azure subscription in hello **Choose a Subscription** dialog and click **Next**.</span></span>
4. <span data-ttu-id="5fc0d-117">Seçin **Windows Server 2012 R2 Datacenter, Haziran 2017** hello içinde **bir sanal makine görüntüsü seçin** tıklayın ve iletişim **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="5fc0d-117">Select **Windows Server 2012 R2 Datacenter, June 2017** in hello **Select a Virtual Machine Image** dialog and click **Next**.</span></span>
5. <span data-ttu-id="5fc0d-118">Merhaba, **sanal makine temel ayarlarını**, hello sanal makine adı çok Ayarla "wadexample".</span><span class="sxs-lookup"><span data-stu-id="5fc0d-118">In hello **Virtual Machine Basic Settings**, set hello virtual machine name too"wadexample".</span></span> <span data-ttu-id="5fc0d-119">Yönetici kullanıcı adı ve parola ayarlayın ve tıklayın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="5fc0d-119">Set your Administrator user name and password and click **Next**.</span></span>
6. <span data-ttu-id="5fc0d-120">Merhaba, **bulut hizmeti ayarlarını** "wadexampleVM" adlı yeni bir bulut hizmeti Oluştur iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="5fc0d-120">In hello **Cloud Service Settings** dialog create a new cloud service named "wadexampleVM".</span></span> <span data-ttu-id="5fc0d-121">"Wadexample" adlı yeni bir depolama hesabı oluşturmak ve tıklayın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="5fc0d-121">Create a new Storage account named "wadexample" and click **Next**.</span></span>
7. <span data-ttu-id="5fc0d-122">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5fc0d-122">Click **Create**.</span></span>

### <a name="step-2-create-your-application"></a><span data-ttu-id="5fc0d-123">2. adım: uygulamanızı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5fc0d-123">Step 2: Create your Application</span></span>
1. <span data-ttu-id="5fc0d-124">Geliştirme bilgisayarınızda Visual Studio 2017 başlatın.</span><span class="sxs-lookup"><span data-stu-id="5fc0d-124">On your development computer, launch Visual Studio 2017.</span></span>
2. <span data-ttu-id="5fc0d-125">Yeni bir Visual C# konsol .NET Framework 4. 5'i hedefleyen uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5fc0d-125">Create a new Visual C# Console Application that targets .NET Framework 4.5.</span></span> <span data-ttu-id="5fc0d-126">Merhaba projeyi "WadExampleVM" olarak adlandırın.</span><span class="sxs-lookup"><span data-stu-id="5fc0d-126">Name hello project "WadExampleVM".</span></span>

   ![CloudServices_diag_new_project](./media/virtual-machines-dotnet-diagnostics/NewProject.png)
3. <span data-ttu-id="5fc0d-128">Program.cs içeriğini Hello koddan hello ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="5fc0d-128">Replace hello contents of Program.cs with hello following code.</span></span> <span data-ttu-id="5fc0d-129">Merhaba sınıfı **SampleEventSourceWriter** dört günlük yöntemlerini uygular: **SendEnums**, **MessageMethod**, **SetOther** ve  **HighFreq**.</span><span class="sxs-lookup"><span data-stu-id="5fc0d-129">hello class **SampleEventSourceWriter** implements four logging methods: **SendEnums**, **MessageMethod**, **SetOther** and **HighFreq**.</span></span> <span data-ttu-id="5fc0d-130">Merhaba ilk parametre toohello WriteEvent yöntemi hello ilgili olay hello kimliği tanımlar.</span><span class="sxs-lookup"><span data-stu-id="5fc0d-130">hello first parameter toohello WriteEvent method defines hello ID for hello respective event.</span></span> <span data-ttu-id="5fc0d-131">Merhaba Run yöntemi uygulayan her hello hello uygulanan günlük yöntemlerini çağıran sonsuz bir döngüde **SampleEventSourceWriter** 10 saniyede sınıfı.</span><span class="sxs-lookup"><span data-stu-id="5fc0d-131">hello Run method implements an infinite loop that calls each of hello logging methods implemented in hello **SampleEventSourceWriter** class every 10 seconds.</span></span>

    ```csharp
     using System;
     using System.Diagnostics;
     using System.Diagnostics.Tracing;
     using System.Threading;

     namespace WadExampleVM
     {
       sealed class SampleEventSourceWriter : EventSource {
         public static SampleEventSourceWriter Log = new SampleEventSourceWriter();
         public void SendEnums(MyColor color, MyFlags flags) { if (IsEnabled())  WriteEvent(1, (int)color, (int)flags); } // Cast enums tooint for efficient logging.
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

             // Emit several events every time we go through hello loop
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
4. <span data-ttu-id="5fc0d-132">Merhaba dosyayı kaydedin ve seçin **yapı çözümü** hello gelen **yapı** menü toobuild kodunuzu.</span><span class="sxs-lookup"><span data-stu-id="5fc0d-132">Save hello file and select **Build Solution** from hello **Build** menu toobuild your code.</span></span>

### <a name="step-3-deploy-your-application"></a><span data-ttu-id="5fc0d-133">3. adım: uygulamanızı dağıtma</span><span class="sxs-lookup"><span data-stu-id="5fc0d-133">Step 3: Deploy your Application</span></span>
1. <span data-ttu-id="5fc0d-134">Hello üzerinde sağ **WadExampleVM** proje **Çözüm Gezgini** ve **dosya Gezgini'nde klasör Aç**.</span><span class="sxs-lookup"><span data-stu-id="5fc0d-134">Right-click on hello **WadExampleVM** project in **Solution Explorer** and choose **Open Folder in File Explorer**.</span></span>
2. <span data-ttu-id="5fc0d-135">Toohello gidin *bin\Debug* klasörünü ve tüm hello kopyalama dosyaları (WadExampleVM.*)</span><span class="sxs-lookup"><span data-stu-id="5fc0d-135">Navigate toohello *bin\Debug* folder and copy all hello files (WadExampleVM.*)</span></span>
3. <span data-ttu-id="5fc0d-136">İçinde **Sunucu Gezgini** hello sanal makineye sağ tıklayın ve seçin **Uzak Masaüstü kullanarak bağlanmak**.</span><span class="sxs-lookup"><span data-stu-id="5fc0d-136">In **Server Explorer** right-click on hello virtual machine and choose **Connect using Remote Desktop**.</span></span>
4. <span data-ttu-id="5fc0d-137">Toohello VM bağlandıktan sonra WadExampleVM adlı bir klasör oluşturun ve uygulama dosyalarınızı hello klasöre yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="5fc0d-137">Once connected toohello VM create a folder named WadExampleVM and paste your application files into hello folder.</span></span>
5. <span data-ttu-id="5fc0d-138">Merhaba uygulaması WadExampleVM.exe başlatın.</span><span class="sxs-lookup"><span data-stu-id="5fc0d-138">Launch hello application WadExampleVM.exe.</span></span> <span data-ttu-id="5fc0d-139">Boş konsol penceresini görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="5fc0d-139">You should see a blank console window.</span></span>

### <a name="step-4-create-your-diagnostics-configuration-and-install-hello-extension"></a><span data-ttu-id="5fc0d-140">4. adım: Tanılama yapılandırmanızı oluşturun ve hello uzantısını yükleyin</span><span class="sxs-lookup"><span data-stu-id="5fc0d-140">Step 4: Create your Diagnostics configuration and install hello Extension</span></span>
1. <span data-ttu-id="5fc0d-141">Hello ortak yapılandırma dosyası şeması tanımı tooyour geliştirme bilgisayarınızda hello aşağıdaki PowerShell komutunu yürüterek yükleyin:</span><span class="sxs-lookup"><span data-stu-id="5fc0d-141">Download hello public configuration file schema definition tooyour development computer by executing hello following PowerShell command:</span></span>

     <span data-ttu-id="5fc0d-142">(Get-AzureServiceAvailableExtension - UzantıAdı 'PaaSDiagnostics' - ProviderNamespace 'Microsoft.Azure.Diagnostics'). PublicConfigurationSchema | Out-File-kodlama utf8 - FilePath 'WadConfig.xsd'</span><span class="sxs-lookup"><span data-stu-id="5fc0d-142">(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'</span></span>
2. <span data-ttu-id="5fc0d-143">Visual Studio'da, zaten açık veya Visual Studio'da örnek projesinde açık projeler ile ya da yeni bir XML dosyası açın.</span><span class="sxs-lookup"><span data-stu-id="5fc0d-143">Open a new XML file in Visual Studio, either in a project you already have open or in a Visual Studio instance with no open projects.</span></span> <span data-ttu-id="5fc0d-144">Visual Studio'da seçin **Ekle** -> **yeni öğe...**</span><span class="sxs-lookup"><span data-stu-id="5fc0d-144">In Visual Studio, select **Add** -> **New Item…**</span></span><span data-ttu-id="5fc0d-145"> -> **Visual C# öğeleri** -> **veri** -> **XML dosyası**.</span><span class="sxs-lookup"><span data-stu-id="5fc0d-145"> -> **Visual C# items** -> **Data** -> **XML File**.</span></span> <span data-ttu-id="5fc0d-146">"WadExample.xml" Merhaba dosya adı</span><span class="sxs-lookup"><span data-stu-id="5fc0d-146">Name hello file "WadExample.xml"</span></span>
3. <span data-ttu-id="5fc0d-147">Merhaba WadConfig.xsd hello yapılandırma dosyası ile ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="5fc0d-147">Associate hello WadConfig.xsd with hello configuration file.</span></span> <span data-ttu-id="5fc0d-148">Merhaba WadExample.xml Düzenleyicisi penceresinde hello etkin pencereyi olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="5fc0d-148">Make sure hello WadExample.xml editor window is hello active window.</span></span> <span data-ttu-id="5fc0d-149">Tuşuna **F4** tooopen hello **özellikleri** penceresi.</span><span class="sxs-lookup"><span data-stu-id="5fc0d-149">Press **F4** tooopen hello **Properties** window.</span></span> <span data-ttu-id="5fc0d-150">Tıklatın hello üzerinde **şemaları** hello özelliğinde **özellikleri** penceresi.</span><span class="sxs-lookup"><span data-stu-id="5fc0d-150">Click on hello **Schemas** property in hello **Properties** window.</span></span> <span data-ttu-id="5fc0d-151">Merhaba tıklatın **...**</span><span class="sxs-lookup"><span data-stu-id="5fc0d-151">Click hello **…**</span></span> <span data-ttu-id="5fc0d-152">Merhaba, **şemaları** özelliği.</span><span class="sxs-lookup"><span data-stu-id="5fc0d-152">in hello **Schemas** property.</span></span> <span data-ttu-id="5fc0d-153">Merhaba tıklatın **Ekle...**</span><span class="sxs-lookup"><span data-stu-id="5fc0d-153">Click hello **Add…**</span></span> <span data-ttu-id="5fc0d-154">düğme ve hello XSD dosyası ve select hello dosya WadConfig.xsd kaydettiğiniz toohello konuma gidin.</span><span class="sxs-lookup"><span data-stu-id="5fc0d-154">button and navigate toohello location where you saved hello XSD file and select hello file WadConfig.xsd.</span></span> <span data-ttu-id="5fc0d-155">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5fc0d-155">Click **OK**.</span></span>
4. <span data-ttu-id="5fc0d-156">Merhaba WadExample.xml yapılandırma dosyası Hello içeriğini hello dosyayı Kaydet XML aşağıdaki hello ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="5fc0d-156">Replace hello contents of hello WadExample.xml configuration file with hello following XML and save hello file.</span></span> <span data-ttu-id="5fc0d-157">Bu yapılandırma dosyası birkaç performans sayaçları toocollect tanımlar: CPU kullanımı, diğeri bellek kullanımı için.</span><span class="sxs-lookup"><span data-stu-id="5fc0d-157">This configuration file defines a couple performance counters toocollect: one for CPU utilization and one for memory utilization.</span></span> <span data-ttu-id="5fc0d-158">Ardından hello yapılandırmasını hello SampleEventSourceWriter sınıfı toohello yöntemleri karşılık gelen hello dört olayları tanımlar.</span><span class="sxs-lookup"><span data-stu-id="5fc0d-158">Then hello configuration defines hello four events corresponding toohello methods in hello SampleEventSourceWriter class.</span></span>

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

### <a name="step-5-remotely-install-diagnostics-on-your-azure-virtual-machine"></a><span data-ttu-id="5fc0d-159">5. adım: Azure sanal makinenize tanılama uzaktan yükleyin.</span><span class="sxs-lookup"><span data-stu-id="5fc0d-159">Step 5: Remotely install Diagnostics on your Azure Virtual Machine</span></span>
<span data-ttu-id="5fc0d-160">Merhaba bir VM'de tanılama yönetmek için PowerShell cmdlet'leri şunlardır: Set-AzureVMDiagnosticsExtension, Get-AzureVMDiagnosticsExtension ve Kaldır-AzureVMDiagnosticsExtension.</span><span class="sxs-lookup"><span data-stu-id="5fc0d-160">hello PowerShell cmdlets for managing Diagnostics on a VM are: Set-AzureVMDiagnosticsExtension, Get-AzureVMDiagnosticsExtension, and Remove-AzureVMDiagnosticsExtension.</span></span>

1. <span data-ttu-id="5fc0d-161">Geliştirici bilgisayarınızda Azure PowerShell açın.</span><span class="sxs-lookup"><span data-stu-id="5fc0d-161">On your developer computer, open Azure PowerShell.</span></span>
2. <span data-ttu-id="5fc0d-162">Merhaba betik tooremotely yükleme tanılama VM üzerinde yürütme (Değiştir `<user>` kullanıcı dizin adı.</span><span class="sxs-lookup"><span data-stu-id="5fc0d-162">Execute hello script tooremotely install Diagnostics on your VM (Replace `<user>` with your user directory name.</span></span> <span data-ttu-id="5fc0d-163">Değiştir `<StorageAccountKey>` hello depolama hesabınızın anahtarıyla wadexamplevm depolama hesabınız için):</span><span class="sxs-lookup"><span data-stu-id="5fc0d-163">Replace `<StorageAccountKey>` with hello storage account key for your wadexamplevm storage account):</span></span>
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
### <a name="step-6-look-at-your-telemetry-data"></a><span data-ttu-id="5fc0d-164">6. adım: Telemetri verilerinizi bakma</span><span class="sxs-lookup"><span data-stu-id="5fc0d-164">Step 6: Look at your telemetry data</span></span>
<span data-ttu-id="5fc0d-165">Merhaba Visual Studio içinde **Sunucu Gezgini** toohello wadexample depolama hesabına gidin.</span><span class="sxs-lookup"><span data-stu-id="5fc0d-165">In hello Visual Studio **Server Explorer** navigate toohello wadexample storage account.</span></span> <span data-ttu-id="5fc0d-166">VM yaklaşık 5 dakika çalışıyor hello sonra hello tabloları görmelisiniz **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**,  **WADPerformanceCountersTable** ve **WADSetOtherTable**.</span><span class="sxs-lookup"><span data-stu-id="5fc0d-166">After hello VM has been running about 5 minutes you should see hello tables **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** and **WADSetOtherTable**.</span></span> <span data-ttu-id="5fc0d-167">Toplanan hello tabloları tooview hello telemetri birine çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5fc0d-167">Double-click on one of hello tables tooview hello telemetry that has been collected.</span></span>

![CloudServices_diag_wadexamplevm_tables](./media/virtual-machines-dotnet-diagnostics/WadExampleVMTables.png)

## <a name="configuration-file-schema"></a><span data-ttu-id="5fc0d-169">Yapılandırma dosyası şeması</span><span class="sxs-lookup"><span data-stu-id="5fc0d-169">Configuration file schema</span></span>
<span data-ttu-id="5fc0d-170">Merhaba tanılama yapılandırma dosyası hello Tanılama aracı başladığında kullanılan tooinitialize tanılama yapılandırma ayarlarının değerleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="5fc0d-170">hello Diagnostics configuration file defines values that are used tooinitialize diagnostic configuration settings when hello diagnostics agent starts.</span></span> <span data-ttu-id="5fc0d-171">Merhaba bkz [en son şema başvurusu](https://msdn.microsoft.com/library/azure/mt634524.aspx) geçerli değerler ve örnekler için.</span><span class="sxs-lookup"><span data-stu-id="5fc0d-171">See hello [latest schema reference](https://msdn.microsoft.com/library/azure/mt634524.aspx) for valid values and examples.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="5fc0d-172">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="5fc0d-172">Troubleshooting</span></span>
<span data-ttu-id="5fc0d-173">Bkz: [sorun giderme Azure tanılama](../monitoring-and-diagnostics/azure-diagnostics-troubleshooting.md) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="5fc0d-173">See [Troubleshooting Azure Diagnostics](../monitoring-and-diagnostics/azure-diagnostics-troubleshooting.md) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5fc0d-174">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5fc0d-174">Next steps</span></span>
<span data-ttu-id="5fc0d-175">[Bkz: sanal makine listesini makaleler Azure tanılama](../monitoring-and-diagnostics/azure-diagnostics.md#virtual-machines-using-azure-diagnostics) toochange hello verileri toplama, sorunları gidermek veya Tanılama hakkında daha fazla genel bilgi.</span><span class="sxs-lookup"><span data-stu-id="5fc0d-175">[See a list of virtual machine related Azure Diagnostics articles](../monitoring-and-diagnostics/azure-diagnostics.md#virtual-machines-using-azure-diagnostics) toochange hello data you are collecting, troubleshoot problems or learn more about diagnostics in general.</span></span>

[EventSource Class]: http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource(v=vs.110).aspx

[Debugging an Azure Application]: http://msdn.microsoft.com/library/windowsazure/ee405479.aspx   
[Collect Logging Data by Using Azure Diagnostics]: http://msdn.microsoft.com/library/windowsazure/gg433048.aspx
[Free Trial]: http://azure.microsoft.com/pricing/free-trial/
[Install and configure Azure PowerShell version 0.8.7 or later]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/
