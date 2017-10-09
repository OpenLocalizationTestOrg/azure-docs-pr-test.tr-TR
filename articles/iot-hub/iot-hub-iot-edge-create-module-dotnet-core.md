---
title: "aaaCreate bir C# ile Azure IOT kenar Modülü | Microsoft Docs"
description: "Bu öğretici, nasıl bir bırak veri dönüştürücü modülünü kullanarak toowrite hello en son Azure IOT kenar NuGet paketleri, Visual Studio Code ve C# gösterir."
services: iot-hub
author: jeffreyCline
manager: timlt
keywords: "Azure IOT, öğretici, modül, nuget, vscode, csharp, sınır"
ms.service: iot-hub
ms.devlang: csharp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: jcline
ms.openlocfilehash: b104609c05d1613e21acc7d7bed547f311179151
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-iot-edge-module-with-cx23"></a><span data-ttu-id="9d5a7-104">Bir Azure IOT kenar modülü C & #x23 oluşturun;</span><span class="sxs-lookup"><span data-stu-id="9d5a7-104">Create an Azure IoT Edge Module with C&#x23;</span></span>

<span data-ttu-id="9d5a7-105">Bu öğretici paylaşan nasıl modül için bir toocreate `Azure IoT Edge` kullanarak `Visual Studio Code` ve `C#`.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-105">This tutorial showcases how toocreate a module for `Azure IoT Edge` using `Visual Studio Code` and `C#`.</span></span>

<span data-ttu-id="9d5a7-106">Bu öğreticide, biz ortamı ayarı yol ve nasıl toowrite bir [bırak](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) veri dönüştürücü modülünü kullanarak hello son `Azure IoT Edge NuGet` paketleri.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-106">In this tutorial, we walk through environment set-up and how toowrite a [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) data converter module using hello latest `Azure IoT Edge NuGet` packages.</span></span> 

>[!NOTE]
<span data-ttu-id="9d5a7-107">Bu öğretici hello kullanarak `.NET Core SDK`, platformlar arası uyumluluk destekler.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-107">This tutorial is using hello `.NET Core SDK`, which supports cross-platform compatibility.</span></span> <span data-ttu-id="9d5a7-108">Merhaba aşağıdaki öğretici hello kullanarak yazılır `Windows 10` işletim sistemi.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-108">hello following tutorial is written using hello `Windows 10` operating system.</span></span> <span data-ttu-id="9d5a7-109">Bu öğreticide hello komutları bazıları bağlı olarak farklı olabilir, `development environment`.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-109">Some of hello commands in this tutorial may be different depending on your `development environment`.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="9d5a7-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="9d5a7-110">Prerequisites</span></span>

<span data-ttu-id="9d5a7-111">Bu bölümde, biz Kurulum ortamınız için `Azure IoT Edge` modülü geliştirme.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-111">In this section, we set-up your environment for `Azure IoT Edge` module development.</span></span> <span data-ttu-id="9d5a7-112">Tooboth geçerlidir **64-bit Windows** ve **64-bit Linux (Ubuntu/Debian 8)** işletim sistemleri.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-112">It applies tooboth **64-bit Windows** and **64-bit Linux (Ubuntu/Debian 8)** operating systems.</span></span>

<span data-ttu-id="9d5a7-113">yazılımı aşağıdaki hello gereklidir:</span><span class="sxs-lookup"><span data-stu-id="9d5a7-113">hello following software is required:</span></span>

- [<span data-ttu-id="9d5a7-114">Git istemci</span><span class="sxs-lookup"><span data-stu-id="9d5a7-114">Git Client</span></span>](https://git-scm.com/downloads)
- [<span data-ttu-id="9d5a7-115">.NET Core SDK</span><span class="sxs-lookup"><span data-stu-id="9d5a7-115">.NET Core SDK</span></span>](https://www.microsoft.com/net/core#windowscmd)
- [<span data-ttu-id="9d5a7-116">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="9d5a7-116">Visual Studio Code</span></span>](https://code.visualstudio.com/)

<span data-ttu-id="9d5a7-117">Bu örnek için tooclone hello depodaki gerekmez, ancak tüm hello Bu öğreticide ele alınan kod örnek depo aşağıdaki hello bulunur:</span><span class="sxs-lookup"><span data-stu-id="9d5a7-117">You do not need tooclone hello repo for this sample, however all of hello sample code discussed in this tutorial is located in hello following repository:</span></span>

- <span data-ttu-id="9d5a7-118">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-118">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span></span>
- `cd iot-edge-samples/dotnetcore/simulated_ble`

## <a name="getting-started"></a><span data-ttu-id="9d5a7-119">Başlarken</span><span class="sxs-lookup"><span data-stu-id="9d5a7-119">Getting started</span></span>

1. <span data-ttu-id="9d5a7-120">Yükleme `.NET Core SDK`.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-120">Install `.NET Core SDK`.</span></span>
2. <span data-ttu-id="9d5a7-121">Yükleme `Visual Studio Code` ve hello `C# extension` hello Visual Studio kod Market gelen.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-121">Install `Visual Studio Code` and hello `C# extension` from hello Visual Studio Code Marketplace.</span></span>

<span data-ttu-id="9d5a7-122">Bu görünümü, [hızlı videosu](https://channel9.msdn.com/Blogs/dotnet/Get-started-VSCode-Csharp-NET-Core-Windows) tooget nasıl kullanmaya hakkında `Visual Studio Code` ve hello `.NET Core SDK`.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-122">View this [quick video tutorial](https://channel9.msdn.com/Blogs/dotnet/Get-started-VSCode-Csharp-NET-Core-Windows) about how tooget started using `Visual Studio Code` and hello `.NET Core SDK`.</span></span>

## <a name="creating-hello-azure-iot-edge-converter-module"></a><span data-ttu-id="9d5a7-123">Hello Azure IOT kenar dönüştürücü modül oluşturma</span><span class="sxs-lookup"><span data-stu-id="9d5a7-123">Creating hello Azure IoT Edge converter module</span></span>

1. <span data-ttu-id="9d5a7-124">Yeni bir başlatma `.NET Core` sınıf kitaplığı C# projesi:</span><span class="sxs-lookup"><span data-stu-id="9d5a7-124">Initialize a new `.NET Core` class library C# project:</span></span>
    - <span data-ttu-id="9d5a7-125">Bir komut istemi açın (`Windows + R` -> `cmd` -> `enter`).</span><span class="sxs-lookup"><span data-stu-id="9d5a7-125">Open a command prompt (`Windows + R` -> `cmd` -> `enter`).</span></span>
    - <span data-ttu-id="9d5a7-126">Burada gibi toocreate hello toohello klasörüne gidin `C#` projesi.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-126">Navigate toohello folder where you'd like toocreate hello `C#` project.</span></span>
    - <span data-ttu-id="9d5a7-127">Tür **dotnet yeni classlib -o IoTEdgeConverterModule -f netstandard1.3**.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-127">Type **dotnet new classlib -o IoTEdgeConverterModule -f netstandard1.3**.</span></span> 
    - <span data-ttu-id="9d5a7-128">Bu komut adlı boş bir sınıf oluşturur `Class1.cs` projeleri dizininizde.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-128">This command creates an empty class called `Class1.cs` in your projects directory.</span></span>
2. <span data-ttu-id="9d5a7-129">Burada yeni oluşturduğumuz hello sınıf kitaplığı proje yazarak toohello klasörüne gidin **cd IoTEdgeConverterModule**.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-129">Navigate toohello folder where we just created hello class library project by typing **cd IoTEdgeConverterModule**.</span></span>
3. <span data-ttu-id="9d5a7-130">Açık hello projesinde `Visual Studio Code` yazarak **kodu.**.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-130">Open hello project in `Visual Studio Code` by typing **code .**.</span></span>
4. <span data-ttu-id="9d5a7-131">Başlangıç projesi olarak açıldıktan sonra `Visual Studio Code`, üzerinde hello tıklatın **IoTEdgeConverterModule.csproj** hello görüntü aşağıdaki gösterildiği gibi tooopen hello dosyası:</span><span class="sxs-lookup"><span data-stu-id="9d5a7-131">Once hello project is opened in `Visual Studio Code`, click on hello **IoTEdgeConverterModule.csproj** tooopen hello file as shown in hello following image:</span></span>

    ![Visual Studio Code düzenleme penceresi](media/iot-hub-iot-edge-create-module/vscode-edit-csproj.png)

5. <span data-ttu-id="9d5a7-133">Merhaba Ekle `XML` hello kapanış arasında kod parçacığını aşağıdaki hello gösterilen blob `PropertyGroup` etiketi ve kapanış hello `Project` etiketi; altı görüntü önceki hello içinde satır ve tuşlarına basarak hello dosyasını kaydedin `Ctrl`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-133">Insert hello `XML` blob shown in hello following code snippet between hello closing `PropertyGroup` tag and hello closing `Project` tag; line six in hello preceding image and save hello file by pressing `Ctrl` + `S`.</span></span>

   ```xml
     <ItemGroup>
       <PackageReference Include="Microsoft.Azure.Devices.Gateway.Module.NetStandard" Version="1.0.5" />
       <PackageReference Include="System.Threading.Thread" Version="4.3.0" />
       <PackageReference Include="Newtonsoft.Json" Version="10.0.2" />
     </ItemGroup> 
   ```

6. <span data-ttu-id="9d5a7-134">Merhaba kaydettikten sonra `.csproj` dosyası `Visual Studio Code` sizinle ister bir `unresolved dependencies` görüntü aşağıdaki hello görülen iletişim:</span><span class="sxs-lookup"><span data-stu-id="9d5a7-134">Once you save hello `.csproj` file, `Visual Studio Code` should prompt you with an `unresolved dependencies` dialog as seen in hello following image:</span></span> 

    ![Visual Studio Code geri yükleme bağımlılıkları iletişim kutusu](media/iot-hub-iot-edge-create-module/vscode-restore.png)

    <span data-ttu-id="9d5a7-136">bir) tıklatın `Restore` tüm hello başvurular hello projelerinde toorestore `.csproj` hello dahil olmak üzere dosya `PackageReferences` ekledik.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-136">a) Click `Restore` toorestore all of hello references in hello projects `.csproj` file including hello `PackageReferences` we have added.</span></span> 

    <span data-ttu-id="9d5a7-137">b) `Visual Studio Code` hello otomatik olarak oluşturur `project.assets.json` projelerinizi dosyasında `obj` klasör.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-137">b) `Visual Studio Code` automatically creates hello `project.assets.json` file in your projects `obj` folder.</span></span> <span data-ttu-id="9d5a7-138">Bu dosya, projenizin bağımlılıkları toomake sonraki geri yüklemeler daha hızlı hakkında bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-138">This file contains information about your project's dependencies toomake subsequent restores quicker.</span></span>
 
    >[!NOTE]
    <span data-ttu-id="9d5a7-139">`.NET Core Tools`MSBuild tabanlı sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-139">`.NET Core Tools` are now MSBuild-based.</span></span> <span data-ttu-id="9d5a7-140">Anlamına gelen bir `.csproj` proje dosyası oluşturuldu. yerine bir `project.json`.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-140">Which means a `.csproj` project file is created instead of a `project.json`.</span></span>

    - <span data-ttu-id="9d5a7-141">Varsa `Visual Studio Code` Tamam, sizden istemez biz el ile yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-141">If `Visual Studio Code` does not prompt you that is ok, we can do it manually.</span></span> <span data-ttu-id="9d5a7-142">Açık hello `Visual Studio Code` tuşuna basarak hello tarafından tümleşik terminal penceresi `Ctrl`  +  `backtick` anahtarları veya hello menüleri kullanarak `View`  ->  `Integrated Terminal`.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-142">Open hello `Visual Studio Code` integrated terminal window by pressing hello `Ctrl` + `backtick` keys or using hello menus `View` -> `Integrated Terminal`.</span></span>
    - <span data-ttu-id="9d5a7-143">Merhaba, `Integrated Terminal` pencere türü **dotnet geri yükleme**.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-143">In hello `Integrated Terminal` window type **dotnet restore**.</span></span>
    
7. <span data-ttu-id="9d5a7-144">Merhaba yeniden adlandırma `Class1.cs` çok dosya`BleConverterModule.cs`.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-144">Rename hello `Class1.cs` file too`BleConverterModule.cs`.</span></span> 

    <span data-ttu-id="9d5a7-145">bir) toorename hello dosya ilk hello dosyada tıklatın ardından basın hello `F2` anahtarı.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-145">a) toorename hello file first click on hello file then press hello `F2` key.</span></span>
    
    <span data-ttu-id="9d5a7-146">b) hello yeni adı yazın **BleConverterModule**, görüntü aşağıdaki hello görüldüğü gibi:</span><span class="sxs-lookup"><span data-stu-id="9d5a7-146">b) Type in hello new name **BleConverterModule**, as seen in hello following image:</span></span>

    ![Visual Studio Code bir sınıfı yeniden adlandırma](media/iot-hub-iot-edge-create-module/vscode-rename.png)

8. <span data-ttu-id="9d5a7-148">Merhaba Hello varolan kodla `BleConverterModule.cs` dosya kopyalama ve yapıştırma hello içine kod parçacığını aşağıdaki tarafından `BleConverterModule.cs` dosya.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-148">Replace hello existing code in hello `BleConverterModule.cs` file by copying and pasting hello following code snippet into your `BleConverterModule.cs` file.</span></span>

   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Globalization;
   using System.Linq;
   using System.Text;
   using System.Threading;
   using System.Threading.Tasks;
   using Microsoft.Azure.Devices.Gateway;
   using Newtonsoft.Json;
   
   namespace IoTEdgeConverterModule
   {
       public class BleConverterModule : IGatewayModule, IGatewayModuleStart
       {
           private Broker broker;
           private string configuration;
           private int messageCount;

           public void Create(Broker broker, byte[] configuration)
           {
               this.broker = broker;
               this.configuration = System.Text.Encoding.UTF8.GetString(configuration);
           }
   
           public void Start()
           {
           }

           public void Destroy()
           {
           }

           public void Receive(Message received_message)
           {
               string recMsg = Encoding.UTF8.GetString(received_message.Content, 0, received_message.Content.Length);
               BleData receivedData = JsonConvert.DeserializeObject<BleData>(recMsg);

               float temperature = float.Parse(receivedData.Temperature, CultureInfo.InvariantCulture.NumberFormat); 
               Dictionary<string, string> receivedProperties = received_message.Properties;
            
               Dictionary<string, string> properties = new Dictionary<string, string>();
               properties.Add("source", receivedProperties["source"]);
               properties.Add("macAddress", receivedProperties["macAddress"]);
               properties.Add("temperatureAlert", temperature > 30 ? "true" : "false");
   
               String content = String.Format("{0} \"deviceId\": \"Intel NUC Gateway\", \"messageId\": {1}, \"temperature\": {2} {3}", "{", ++this.messageCount, temperature, "}");
               Message messageToPublish = new Message(content, properties);
   
               this.broker.Publish(messageToPublish);
           }
       }
   }
   ```

9. <span data-ttu-id="9d5a7-149">Tuşlarına basarak Hello dosyasını kaydedin `Ctrl`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-149">Save hello file by pressing `Ctrl` + `S`.</span></span>

10. <span data-ttu-id="9d5a7-150">Adlı yeni bir dosya oluşturun `Untitled-1` tuşuna basarak hello tarafından `Ctrl`  +  `N` anahtarları görüntü aşağıdaki hello görüldüğü gibi:</span><span class="sxs-lookup"><span data-stu-id="9d5a7-150">Create a new file called `Untitled-1` by pressing hello `Ctrl` + `N` keys as seen in hello following image:</span></span>

    ![Visual Studio Code yeni dosya](media/iot-hub-iot-edge-create-module/vscode-new-file.png)

11. <span data-ttu-id="9d5a7-152">toodeserialize hello `JSON` benzetimli hello aldığımız nesne `BLE` aygıt, hello koddan kopyalama hello `Untitled-1` dosya kod düzenleyici penceresini.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-152">toodeserialize hello `JSON` object that we receive from hello simulated `BLE` device, copy hello following code into hello `Untitled-1` file code editor window.</span></span> 

   ```csharp
   using System;
   using Newtonsoft.Json;

   namespace IoTEdgeConverterModule
   {
       public class BleData
       {
           [JsonProperty(PropertyName = "temperature")]
           public string Temperature { get; set; }
       }
   }
   ```

12. <span data-ttu-id="9d5a7-153">Merhaba dosyası olarak kaydetmeniz `BleData.cs` basarak `Ctrl`  +  `Shift`  +  `S` anahtarları.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-153">Save hello file as `BleData.cs` by pressing `Ctrl` + `Shift` + `S` keys.</span></span>
    - <span data-ttu-id="9d5a7-154">Merhaba üzerinde Kaydet iletişim kutusunda hello olarak `Save as Type` açılır menüsünde, select `C# (*.cs;*.csx)` görüntü aşağıdaki hello görüldüğü gibi:</span><span class="sxs-lookup"><span data-stu-id="9d5a7-154">On hello save as dialog box, in hello `Save as Type` dropdown menu, select `C# (*.cs;*.csx)` as seen in hello following image:</span></span>

    ![Visual Studio Code iletişim kutusu olarak Kaydet](media/iot-hub-iot-edge-create-module/vscode-save-as.png)

13. <span data-ttu-id="9d5a7-156">Adlı yeni bir dosya oluşturun `Untitled-1` tuşuna basarak hello tarafından `Ctrl`  +  `N` anahtarları.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-156">Create a new file called `Untitled-1` by pressing hello `Ctrl` + `N` keys.</span></span>

14. <span data-ttu-id="9d5a7-157">Kod parçacığı hello aşağıdaki hello kopyalayıp `Untitled-1` dosya.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-157">Copy and paste hello following code snippet into hello `Untitled-1` file.</span></span> <span data-ttu-id="9d5a7-158">Bu sınıf, bir `Azure IoT Edge` toooutput hello veri aldı kullanırız modülü bizim `BleConverterModule`.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-158">This class is a `Azure IoT Edge` module, which we use toooutput hello data received from our `BleConverterModule`.</span></span>

   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Linq;
   using System.Text;
   using System.Threading.Tasks;
   using Microsoft.Azure.Devices.Gateway;
   using Newtonsoft.Json;
   
   namespace PrinterModule
   {
       public class DotNetPrinterModule : IGatewayModule
       {
           private string configuration;
           public void Create(Broker broker, byte[] configuration)
           {
               this.configuration = System.Text.Encoding.UTF8.GetString(configuration);
           }
   
           public void Destroy()
           {
           }
   
           public void Receive(Message received_message)
           {
               string recMsg = System.Text.Encoding.UTF8.GetString(received_message.Content, 0, received_message.Content.Length);
               Dictionary<string, string> receivedProperties = received_message.Properties;
               
               BleConverterData receivedData = JsonConvert.DeserializeObject<BleConverterData>(recMsg);
   
               Console.WriteLine();
               Console.WriteLine("Module           : [DotNetPrinterModule]");
               Console.WriteLine("received_message : {0}", recMsg);
   
               if(received_message.Properties["source"] == "bleTelemetry")
               {
                   Console.WriteLine("Source           : {0}", receivedProperties["source"]);
                   Console.WriteLine("MAC address      : {0}", receivedProperties["macAddress"]);
                   Console.WriteLine("Temperature Alert: {0}", receivedProperties["temperatureAlert"]);
                   Console.WriteLine("Deserialized Obj : [BleConverterData]");
                   Console.WriteLine("  DeviceId       : {0}", receivedData.DeviceId);
                   Console.WriteLine("  MessageId      : {0}", receivedData.MessageId);
                   Console.WriteLine("  Temperature    : {0}", receivedData.Temperature);
               }
   
               Console.WriteLine();
           }
       }
   }
   ```

15. <span data-ttu-id="9d5a7-159">Merhaba dosyası olarak kaydetmeniz `DotNetPrinterModule.cs` basarak `Ctrl`  +  `Shift`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-159">Save hello file as `DotNetPrinterModule.cs` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="9d5a7-160">Merhaba üzerinde Kaydet iletişim kutusunda hello olarak `Save as Type` açılır menüsünde, select `C# (*.cs;*.csx)`.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-160">On hello save as dialog box, in hello `Save as Type` dropdown menu, select `C# (*.cs;*.csx)`.</span></span>

16. <span data-ttu-id="9d5a7-161">Adlı yeni bir dosya oluşturun `Untitled-1` tuşuna basarak hello tarafından `Ctrl`  +  `N` anahtarları.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-161">Create a new file called `Untitled-1` by pressing hello `Ctrl` + `N` keys.</span></span>

17. <span data-ttu-id="9d5a7-162">toodeserialize hello `JSON` hello aldığımız nesne `BleConverterModule`, Kopyala ve Yapıştır hello aşağıdaki kod parçacığını hello içine `Untitled-1` dosya.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-162">toodeserialize hello `JSON` object that we receive from hello `BleConverterModule`, Copy and paste hello following code snippet into hello `Untitled-1` file.</span></span> 

   ```csharp
   using System;
   using Newtonsoft.Json;

   namespace PrinterModule
   {
       public class BleConverterData
       {
           [JsonProperty(PropertyName = "deviceId")]
           public string DeviceId { get; set; }
   
           [JsonProperty(PropertyName = "messageId")]
           public string MessageId { get; set; }
   
           [JsonProperty(PropertyName = "temperature")]
           public string Temperature { get; set; }
       }
   }
   ```

18. <span data-ttu-id="9d5a7-163">Merhaba dosyası olarak kaydetmeniz `BleConverterData.cs` basarak `Ctrl`  +  `Shift`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-163">Save hello file as `BleConverterData.cs` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="9d5a7-164">Merhaba üzerinde Kaydet iletişim kutusunda hello olarak `Save as Type` açılır menüsünde, select `C# (*.cs;*.csx)`.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-164">On hello save as dialog box, in hello `Save as Type` dropdown menu, select `C# (*.cs;*.csx)`.</span></span>

19. <span data-ttu-id="9d5a7-165">Adlı yeni bir dosya oluşturun `Untitled-1` tuşuna basarak hello tarafından `Ctrl`  +  `N` anahtarları.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-165">Create a new file called `Untitled-1` by pressing hello `Ctrl` + `N` keys.</span></span>

20. <span data-ttu-id="9d5a7-166">Kod parçacığı hello aşağıdaki hello kopyalayıp `Untitled-1` dosya.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-166">Copy and paste hello following code snippet into hello `Untitled-1` file.</span></span>

   ```json
   {
       "loaders": [
           {
               "type": "dotnetcore",
               "name": "dotnetcore",
               "configuration": {
                   "binding.path": "dotnetcore.dll",
                   "binding.coreclrpath": "C:\\Program Files\\dotnet\\shared\\Microsoft.NETCore.App\\1.1.1\\coreclr.dll",
                   "binding.trustedplatformassemblieslocation": "C:\\Program Files\\dotnet\\shared\\Microsoft.NETCore.App\\1.1.1\\"
               }
           }
       ],
          "modules": [
           {
               "name": "simulated_device",
               "loader": {
                   "name": "native",
                   "entrypoint": {
                       "module.path": "simulated_device.dll"
                   }
               },
               "args": {
                   "macAddress": "01:02:03:03:02:01",
                   "messagePeriod": 500
               }
           },
           {
               "name": "ble_converter_module",
               "loader": {
                   "name": "dotnetcore",
                   "entrypoint": {
                       "assembly.name": "IoTEdgeConverterModule",
                       "entry.type": "IoTEdgeConverterModule.BleConverterModule"
                   }
               },
               "args": ""
           },
           {
               "name": "printer_module",
               "loader": {
                   "name": "dotnetcore",
                   "entrypoint": {
                       "assembly.name": "IoTEdgeConverterModule",
                       "entry.type": "PrinterModule.DotNetPrinterModule"
                   }
               },
               "args": ""
           }
       ],
       "links": [
           {
               "source": "simulated_device", "sink": "ble_converter_module"
           },
           {
               "source": "ble_converter_module", "sink": "printer_module"
           }
   ]
   }
   ```

21. <span data-ttu-id="9d5a7-167">Merhaba dosyası olarak kaydetmeniz `gw-config.json` basarak `Ctrl`  +  `Shift`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-167">Save hello file as `gw-config.json` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="9d5a7-168">Merhaba üzerinde Kaydet iletişim kutusunda hello olarak `Save as Type` açılır menüsünde, select `JSON (*.json;*.bowerrc;*.jshintrc;*.jscsrc;*.eslintrc;*.babelrc;*webmanifest)`.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-168">On hello save as dialog box, in hello `Save as Type` dropdown menu, select `JSON (*.json;*.bowerrc;*.jshintrc;*.jscsrc;*.eslintrc;*.babelrc;*webmanifest)`.</span></span>

22. <span data-ttu-id="9d5a7-169">çıktı dizini, güncelleştirme hello tooenable hello yapılandırma dosyası toohello kopyalama `IoTEdgeConverterModule.csproj` XML blob aşağıdaki hello ile:</span><span class="sxs-lookup"><span data-stu-id="9d5a7-169">tooenable copying of hello configuration file toohello output directory, update hello `IoTEdgeConverterModule.csproj` with hello following XML blob:</span></span>

   ```xml
     <ItemGroup>
       <None Update="gw-config.json" CopyToOutputDirectory="PreserveNewest" />
     </ItemGroup>
   ```
    
   - <span data-ttu-id="9d5a7-170">güncelleştirilmiş hello `IoTEdgeConverterModule.csproj` hello görünümlü aşağıdaki görüntü:</span><span class="sxs-lookup"><span data-stu-id="9d5a7-170">hello updated `IoTEdgeConverterModule.csproj` should look like hello following image:</span></span>

    ![Visual Studio Code güncelleştirilmiş .csproj dosyası](media/iot-hub-iot-edge-create-module/vscode-update-csproj.png)

23. <span data-ttu-id="9d5a7-172">Adlı yeni bir dosya oluşturun `Untitled-1` tuşuna basarak hello tarafından `Ctrl`  +  `N` anahtarları.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-172">Create a new file called `Untitled-1` by pressing hello `Ctrl` + `N` keys.</span></span>

24. <span data-ttu-id="9d5a7-173">Kod parçacığı hello aşağıdaki hello kopyalayıp `Untitled-1` dosya.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-173">Copy and paste hello following code snippet into hello `Untitled-1` file.</span></span>

   ```powershell
   Copy-Item -Path $env:userprofile\.nuget\packages\microsoft.azure.devices.gateway.native.windows.x64\1.1.3\runtimes\win-x64\native\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.runtime.serialization.formatters\4.3.0\lib\netstandard1.4\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.runtime.serialization.primitives\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\newtonsoft.json\10.0.2\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.componentmodel.typeconverter\4.3.0\lib\netstandard1.5\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.collections.nongeneric\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.collections.specialized\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   ```

25. <span data-ttu-id="9d5a7-174">Merhaba dosyası olarak kaydetmeniz `binplace.ps1` basarak `Ctrl`  +  `Shift`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-174">Save hello file as `binplace.ps1` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="9d5a7-175">Merhaba üzerinde Kaydet iletişim kutusunda hello olarak `Save as Type` açılır menüsünde, select `PowerShell (*.ps1;*.psm1;*.psd1;*.pssc;*.psrc)`.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-175">On hello save as dialog box, in hello `Save as Type` dropdown menu, select `PowerShell (*.ps1;*.psm1;*.psd1;*.pssc;*.psrc)`.</span></span>

26. <span data-ttu-id="9d5a7-176">Tuşuna basarak hello tarafından Merhaba Projeyi derlemek `Ctrl`  +  `Shift`  +  `B` anahtarları.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-176">Build hello project by pressing hello `Ctrl` + `Shift` + `B` keys.</span></span> <span data-ttu-id="9d5a7-177">İlk kez hello için Merhaba projeyi derlerken `Visual Studio Code` ile Merhaba ister `No build task defined.` görüntü aşağıdaki hello görülen iletişim:</span><span class="sxs-lookup"><span data-stu-id="9d5a7-177">When you build hello project for hello first time, `Visual Studio Code` prompts you with hello `No build task defined.` dialog as seen in hello following image:</span></span>

    ![Visual Studio Code yapı görev iletişim kutusu](media/iot-hub-iot-edge-create-module/vscode-build-task.png)

    <span data-ttu-id="9d5a7-179">bir) hello tıklatın `Configure Build Task` düğmesi.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-179">a) Click hello `Configure Build Task` button.</span></span>

    <span data-ttu-id="9d5a7-180">b) içinde hello `Select a Task Runner` iletişim kutusu açılır menüsünde.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-180">b) In hello `Select a Task Runner` dialog dropdown menu.</span></span> <span data-ttu-id="9d5a7-181">Seçin `.NET Core` görüntü aşağıdaki hello görüldüğü gibi:</span><span class="sxs-lookup"><span data-stu-id="9d5a7-181">Select `.NET Core` as seen in hello following image:</span></span> 

    ![Visual Studio Code görev iletişim kutusu seç](media/iot-hub-iot-edge-create-module/vscode-build-task-runner.png)

    <span data-ttu-id="9d5a7-183">c) tıkladığınızda hello `.NET Core` öğesi oluşturur hello `tasks.json` dosyasını, `.vscode` dizin ve açılır hello hello dosyasında `code editor` penceresi.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-183">c) Clicking hello `.NET Core` item creates hello `tasks.json` file in your `.vscode` directory and opens hello file in hello `code editor` window.</span></span> <span data-ttu-id="9d5a7-184">Bu dosya, Kapat hello sekmesini gerek toomodify yoktur.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-184">There is no need toomodify this file, close hello tab.</span></span>

27.  <span data-ttu-id="9d5a7-185">Açık hello `Visual Studio Code` tuşuna basarak hello tarafından tümleşik terminal penceresi `Ctrl`  +  `backtick` anahtarları veya hello menüleri kullanarak `View`  ->  `Integrated Terminal` ve türü **.\binplace.ps1**hello içine `PowerShell` komut istemi.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-185">Open hello `Visual Studio Code` integrated terminal window by pressing hello `Ctrl` + `backtick` keys or using hello menus `View` -> `Integrated Terminal` and type **.\binplace.ps1** into hello `PowerShell` command prompt.</span></span> <span data-ttu-id="9d5a7-186">Bu komut tüm bizim bağımlılıkları toohello çıktı dizinine kopyalar.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-186">This command copies all our dependencies toohello output directory.</span></span>

28. <span data-ttu-id="9d5a7-187">Merhaba, toohello projeleri çıktı dizinine gidin `Integrated Terminal` yazarak penceresi **cd.\bin\Debug\netstandard1.3**.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-187">Navigate toohello projects output directory in hello `Integrated Terminal` window by typing **cd .\bin\Debug\netstandard1.3**.</span></span>

29. <span data-ttu-id="9d5a7-188">Merhaba örnek proje yazarak çalıştırırsınız **. \gw.exe gw-config.json** hello içine `Integrated Terminal` penceresi istemi.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-188">Run hello sample project by typing **.\gw.exe gw-config.json** into hello `Integrated Terminal` window prompt.</span></span> 
    - <span data-ttu-id="9d5a7-189">Bu öğreticide yakından hello adımları izlediğinizde, şimdi hello çalıştırması `Azure IoT Edge BLE Data Converter Module` görüntü aşağıdaki hello görülen örnek proje:</span><span class="sxs-lookup"><span data-stu-id="9d5a7-189">If you have followed hello steps in this tutorial closely, you should now be running hello `Azure IoT Edge BLE Data Converter Module` sample project as seen in hello following image:</span></span>
    
        ![Visual Studio kodda çalıştıran sanal cihaz örneği](media/iot-hub-iot-edge-create-module/vscode-run.png)
    
    - <span data-ttu-id="9d5a7-191">Tooterminate Merhaba uygulaması istiyorsanız hello basın `<Enter>` anahtarı.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-191">If you want tooterminate hello application, press hello `<Enter>` key.</span></span>

>[!IMPORTANT]
<span data-ttu-id="9d5a7-192">Toouse önerilmez `Ctrl`  +  `C` tooterminate hello `IoT Edge` ağ geçidi uygulaması (diğer bir deyişle, **gw.exe**).</span><span class="sxs-lookup"><span data-stu-id="9d5a7-192">It is not recommended toouse `Ctrl` + `C` tooterminate hello `IoT Edge` gateway application (that is, **gw.exe**).</span></span> <span data-ttu-id="9d5a7-193">Bu eylemin hello işlem tooterminate aşırı neden olabilir ve.</span><span class="sxs-lookup"><span data-stu-id="9d5a7-193">As this action may cause hello process tooterminate abnormally.</span></span>

