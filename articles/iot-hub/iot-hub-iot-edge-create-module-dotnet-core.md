---
title: "Bir Azure IOT kenar modülü C# ile oluşturma | Microsoft Docs"
description: "Bu öğretici nasıl en son Azure IOT kenar NuGet paketleri, Visual Studio Code ve C# kullanarak bir bırak veri dönüştürücü modülü yazılacağını gösterir."
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
ms.openlocfilehash: 7175ffc8de2c043593d61143b402484d33e4a8cc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-azure-iot-edge-module-with-cx23"></a><span data-ttu-id="20afc-104">Bir Azure IOT kenar modülü C & #x23 oluşturun;</span><span class="sxs-lookup"><span data-stu-id="20afc-104">Create an Azure IoT Edge Module with C&#x23;</span></span>

<span data-ttu-id="20afc-105">Bu öğretici için bir modül oluşturma paylaşan `Azure IoT Edge` kullanarak `Visual Studio Code` ve `C#`.</span><span class="sxs-lookup"><span data-stu-id="20afc-105">This tutorial showcases how to create a module for `Azure IoT Edge` using `Visual Studio Code` and `C#`.</span></span>

<span data-ttu-id="20afc-106">Ortam kurulumu ve nasıl yazılacağını Bu öğreticide, biz yol bir [bırak](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) en son kullanılarak veri dönüştürücü Modülü `Azure IoT Edge NuGet` paketler.</span><span class="sxs-lookup"><span data-stu-id="20afc-106">In this tutorial, we walk through environment set-up and how to write a [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) data converter module using the latest `Azure IoT Edge NuGet` packages.</span></span> 

>[!NOTE]
<span data-ttu-id="20afc-107">Bu öğretici kullanarak `.NET Core SDK`, platformlar arası uyumluluk destekler.</span><span class="sxs-lookup"><span data-stu-id="20afc-107">This tutorial is using the `.NET Core SDK`, which supports cross-platform compatibility.</span></span> <span data-ttu-id="20afc-108">Aşağıdaki öğreticide kullanılarak yazılmış `Windows 10` işletim sistemi.</span><span class="sxs-lookup"><span data-stu-id="20afc-108">The following tutorial is written using the `Windows 10` operating system.</span></span> <span data-ttu-id="20afc-109">Bu öğretici komutlarda bazıları bağlı olarak farklı olabilir, `development environment`.</span><span class="sxs-lookup"><span data-stu-id="20afc-109">Some of the commands in this tutorial may be different depending on your `development environment`.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="20afc-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="20afc-110">Prerequisites</span></span>

<span data-ttu-id="20afc-111">Bu bölümde, biz Kurulum ortamınız için `Azure IoT Edge` modülü geliştirme.</span><span class="sxs-lookup"><span data-stu-id="20afc-111">In this section, we set-up your environment for `Azure IoT Edge` module development.</span></span> <span data-ttu-id="20afc-112">Her ikisi de geçerli **64-bit Windows** ve **64-bit Linux (Ubuntu/Debian 8)** işletim sistemleri.</span><span class="sxs-lookup"><span data-stu-id="20afc-112">It applies to both **64-bit Windows** and **64-bit Linux (Ubuntu/Debian 8)** operating systems.</span></span>

<span data-ttu-id="20afc-113">Aşağıdaki yazılımlar gereklidir:</span><span class="sxs-lookup"><span data-stu-id="20afc-113">The following software is required:</span></span>

- [<span data-ttu-id="20afc-114">Git istemci</span><span class="sxs-lookup"><span data-stu-id="20afc-114">Git Client</span></span>](https://git-scm.com/downloads)
- [<span data-ttu-id="20afc-115">.NET Core SDK</span><span class="sxs-lookup"><span data-stu-id="20afc-115">.NET Core SDK</span></span>](https://www.microsoft.com/net/core#windowscmd)
- [<span data-ttu-id="20afc-116">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="20afc-116">Visual Studio Code</span></span>](https://code.visualstudio.com/)

<span data-ttu-id="20afc-117">Bu öğreticide ele alınan tüm örnek kodları bulunur ancak aşağıdaki depoya Bu örnek, depoyu kopyalama gerekmez:</span><span class="sxs-lookup"><span data-stu-id="20afc-117">You do not need to clone the repo for this sample, however all of the sample code discussed in this tutorial is located in the following repository:</span></span>

- <span data-ttu-id="20afc-118">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span><span class="sxs-lookup"><span data-stu-id="20afc-118">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span></span>
- `cd iot-edge-samples/dotnetcore/simulated_ble`

## <a name="getting-started"></a><span data-ttu-id="20afc-119">Başlarken</span><span class="sxs-lookup"><span data-stu-id="20afc-119">Getting started</span></span>

1. <span data-ttu-id="20afc-120">Yükleme `.NET Core SDK`.</span><span class="sxs-lookup"><span data-stu-id="20afc-120">Install `.NET Core SDK`.</span></span>
2. <span data-ttu-id="20afc-121">Yükleme `Visual Studio Code` ve `C# extension` Visual Studio kod Marketi'nden.</span><span class="sxs-lookup"><span data-stu-id="20afc-121">Install `Visual Studio Code` and the `C# extension` from the Visual Studio Code Marketplace.</span></span>

<span data-ttu-id="20afc-122">Bu görünümü, [hızlı videosu](https://channel9.msdn.com/Blogs/dotnet/Get-started-VSCode-Csharp-NET-Core-Windows) kullanmaya başlamak nasıl hakkında `Visual Studio Code` ve `.NET Core SDK`.</span><span class="sxs-lookup"><span data-stu-id="20afc-122">View this [quick video tutorial](https://channel9.msdn.com/Blogs/dotnet/Get-started-VSCode-Csharp-NET-Core-Windows) about how to get started using `Visual Studio Code` and the `.NET Core SDK`.</span></span>

## <a name="creating-the-azure-iot-edge-converter-module"></a><span data-ttu-id="20afc-123">Azure IOT kenar dönüştürücü modül oluşturma</span><span class="sxs-lookup"><span data-stu-id="20afc-123">Creating the Azure IoT Edge converter module</span></span>

1. <span data-ttu-id="20afc-124">Yeni bir başlatma `.NET Core` sınıf kitaplığı C# projesi:</span><span class="sxs-lookup"><span data-stu-id="20afc-124">Initialize a new `.NET Core` class library C# project:</span></span>
    - <span data-ttu-id="20afc-125">Bir komut istemi açın (`Windows + R` -> `cmd` -> `enter`).</span><span class="sxs-lookup"><span data-stu-id="20afc-125">Open a command prompt (`Windows + R` -> `cmd` -> `enter`).</span></span>
    - <span data-ttu-id="20afc-126">Burada istediğinizi oluşturmak klasöre gidin `C#` projesi.</span><span class="sxs-lookup"><span data-stu-id="20afc-126">Navigate to the folder where you'd like to create the `C#` project.</span></span>
    - <span data-ttu-id="20afc-127">Tür **dotnet yeni classlib -o IoTEdgeConverterModule -f netstandard1.3**.</span><span class="sxs-lookup"><span data-stu-id="20afc-127">Type **dotnet new classlib -o IoTEdgeConverterModule -f netstandard1.3**.</span></span> 
    - <span data-ttu-id="20afc-128">Bu komut adlı boş bir sınıf oluşturur `Class1.cs` projeleri dizininizde.</span><span class="sxs-lookup"><span data-stu-id="20afc-128">This command creates an empty class called `Class1.cs` in your projects directory.</span></span>
2. <span data-ttu-id="20afc-129">Burada yeni oluşturduğumuz sınıf kitaplığı proje yazarak klasöre gidin **cd IoTEdgeConverterModule**.</span><span class="sxs-lookup"><span data-stu-id="20afc-129">Navigate to the folder where we just created the class library project by typing **cd IoTEdgeConverterModule**.</span></span>
3. <span data-ttu-id="20afc-130">Projeyi `Visual Studio Code` yazarak **kodu.**.</span><span class="sxs-lookup"><span data-stu-id="20afc-130">Open the project in `Visual Studio Code` by typing **code .**.</span></span>
4. <span data-ttu-id="20afc-131">Proje içinde açıldıktan sonra `Visual Studio Code`, tıklayın **IoTEdgeConverterModule.csproj** aşağıdaki görüntüde gösterildiği gibi dosyayı açmak için:</span><span class="sxs-lookup"><span data-stu-id="20afc-131">Once the project is opened in `Visual Studio Code`, click on the **IoTEdgeConverterModule.csproj** to open the file as shown in the following image:</span></span>

    ![Visual Studio Code düzenleme penceresi](media/iot-hub-iot-edge-create-module/vscode-edit-csproj.png)

5. <span data-ttu-id="20afc-133">INSERT `XML` kapatma arasındaki aşağıdaki kod parçacığında gösterildiği blob `PropertyGroup` etiketi ve kapanış `Project` etiketi; altı önceki görüntüde satır ve tuşlarına basarak dosyayı kaydedin `Ctrl`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="20afc-133">Insert the `XML` blob shown in the following code snippet between the closing `PropertyGroup` tag and the closing `Project` tag; line six in the preceding image and save the file by pressing `Ctrl` + `S`.</span></span>

   ```xml
     <ItemGroup>
       <PackageReference Include="Microsoft.Azure.Devices.Gateway.Module.NetStandard" Version="1.0.5" />
       <PackageReference Include="System.Threading.Thread" Version="4.3.0" />
       <PackageReference Include="Newtonsoft.Json" Version="10.0.2" />
     </ItemGroup> 
   ```

6. <span data-ttu-id="20afc-134">Kaydettikten sonra `.csproj` dosyası `Visual Studio Code` sizinle ister bir `unresolved dependencies` aşağıdaki resimde görüldüğü gibi iletişim:</span><span class="sxs-lookup"><span data-stu-id="20afc-134">Once you save the `.csproj` file, `Visual Studio Code` should prompt you with an `unresolved dependencies` dialog as seen in the following image:</span></span> 

    ![Visual Studio Code geri yükleme bağımlılıkları iletişim kutusu](media/iot-hub-iot-edge-create-module/vscode-restore.png)

    <span data-ttu-id="20afc-136">bir) tıklatın `Restore` tüm projelerdeki başvuruları geri yüklemek için `.csproj` dosyası dahil `PackageReferences` ekledik.</span><span class="sxs-lookup"><span data-stu-id="20afc-136">a) Click `Restore` to restore all of the references in the projects `.csproj` file including the `PackageReferences` we have added.</span></span> 

    <span data-ttu-id="20afc-137">b) `Visual Studio Code` otomatik olarak oluşturur `project.assets.json` projelerinizi dosyasında `obj` klasör.</span><span class="sxs-lookup"><span data-stu-id="20afc-137">b) `Visual Studio Code` automatically creates the `project.assets.json` file in your projects `obj` folder.</span></span> <span data-ttu-id="20afc-138">Bu dosya sonraki geri yüklemeler daha hızlı hale getirmek için projenizin bağımlılıkları hakkında bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="20afc-138">This file contains information about your project's dependencies to make subsequent restores quicker.</span></span>
 
    >[!NOTE]
    <span data-ttu-id="20afc-139">`.NET Core Tools`MSBuild tabanlı sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="20afc-139">`.NET Core Tools` are now MSBuild-based.</span></span> <span data-ttu-id="20afc-140">Anlamına gelen bir `.csproj` proje dosyası oluşturuldu. yerine bir `project.json`.</span><span class="sxs-lookup"><span data-stu-id="20afc-140">Which means a `.csproj` project file is created instead of a `project.json`.</span></span>

    - <span data-ttu-id="20afc-141">Varsa `Visual Studio Code` Tamam, sizden istemez biz el ile yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="20afc-141">If `Visual Studio Code` does not prompt you that is ok, we can do it manually.</span></span> <span data-ttu-id="20afc-142">Açık `Visual Studio Code` basarak tümleşik terminal penceresi `Ctrl`  +  `backtick` anahtarları veya menüleri kullanarak `View`  ->  `Integrated Terminal`.</span><span class="sxs-lookup"><span data-stu-id="20afc-142">Open the `Visual Studio Code` integrated terminal window by pressing the `Ctrl` + `backtick` keys or using the menus `View` -> `Integrated Terminal`.</span></span>
    - <span data-ttu-id="20afc-143">İçinde `Integrated Terminal` pencere türü **dotnet geri yükleme**.</span><span class="sxs-lookup"><span data-stu-id="20afc-143">In the `Integrated Terminal` window type **dotnet restore**.</span></span>
    
7. <span data-ttu-id="20afc-144">Yeniden Adlandır `Class1.cs` dosyasını `BleConverterModule.cs`.</span><span class="sxs-lookup"><span data-stu-id="20afc-144">Rename the `Class1.cs` file to `BleConverterModule.cs`.</span></span> 

    <span data-ttu-id="20afc-145">bir) yeniden adlandırmak için dosyanın ilk tıklatın dosyada tuşuna basarak `F2` anahtarı.</span><span class="sxs-lookup"><span data-stu-id="20afc-145">a) To rename the file first click on the file then press the `F2` key.</span></span>
    
    <span data-ttu-id="20afc-146">(b) yeni adı yazın **BleConverterModule**, aşağıdaki resimde görüldüğü gibi:</span><span class="sxs-lookup"><span data-stu-id="20afc-146">b) Type in the new name **BleConverterModule**, as seen in the following image:</span></span>

    ![Visual Studio Code bir sınıfı yeniden adlandırma](media/iot-hub-iot-edge-create-module/vscode-rename.png)

8. <span data-ttu-id="20afc-148">Varolan kodla `BleConverterModule.cs` içine aşağıdaki kod parçacığını yapıştırarak dosya, `BleConverterModule.cs` dosya.</span><span class="sxs-lookup"><span data-stu-id="20afc-148">Replace the existing code in the `BleConverterModule.cs` file by copying and pasting the following code snippet into your `BleConverterModule.cs` file.</span></span>

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

9. <span data-ttu-id="20afc-149">Tuşlarına basarak dosyayı kaydedin `Ctrl`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="20afc-149">Save the file by pressing `Ctrl` + `S`.</span></span>

10. <span data-ttu-id="20afc-150">Adlı yeni bir dosya oluşturun `Untitled-1` basarak `Ctrl`  +  `N` anahtarları aşağıdaki resimde görüldüğü gibi:</span><span class="sxs-lookup"><span data-stu-id="20afc-150">Create a new file called `Untitled-1` by pressing the `Ctrl` + `N` keys as seen in the following image:</span></span>

    ![Visual Studio Code yeni dosya](media/iot-hub-iot-edge-create-module/vscode-new-file.png)

11. <span data-ttu-id="20afc-152">Seri durumdan çıkarılacak `JSON` benzetimli aldığımız nesne `BLE` aygıt, aşağıdaki kodu kopyalayın `Untitled-1` dosya kod düzenleyici penceresini.</span><span class="sxs-lookup"><span data-stu-id="20afc-152">To deserialize the `JSON` object that we receive from the simulated `BLE` device, copy the following code into the `Untitled-1` file code editor window.</span></span> 

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

12. <span data-ttu-id="20afc-153">Dosyayı Farklı Kaydet `BleData.cs` basarak `Ctrl`  +  `Shift`  +  `S` anahtarları.</span><span class="sxs-lookup"><span data-stu-id="20afc-153">Save the file as `BleData.cs` by pressing `Ctrl` + `Shift` + `S` keys.</span></span>
    - <span data-ttu-id="20afc-154">Farklı Kaydet iletişim kutusu, şirket içinde `Save as Type` açılır menüsünde, select `C# (*.cs;*.csx)` aşağıdaki resimde görüldüğü gibi:</span><span class="sxs-lookup"><span data-stu-id="20afc-154">On the save as dialog box, in the `Save as Type` dropdown menu, select `C# (*.cs;*.csx)` as seen in the following image:</span></span>

    ![Visual Studio Code iletişim kutusu olarak Kaydet](media/iot-hub-iot-edge-create-module/vscode-save-as.png)

13. <span data-ttu-id="20afc-156">Adlı yeni bir dosya oluşturun `Untitled-1` basarak `Ctrl`  +  `N` anahtarları.</span><span class="sxs-lookup"><span data-stu-id="20afc-156">Create a new file called `Untitled-1` by pressing the `Ctrl` + `N` keys.</span></span>

14. <span data-ttu-id="20afc-157">İçine aşağıdaki kod parçacığını kopyalayıp `Untitled-1` dosya.</span><span class="sxs-lookup"><span data-stu-id="20afc-157">Copy and paste the following code snippet into the `Untitled-1` file.</span></span> <span data-ttu-id="20afc-158">Bu sınıf, bir `Azure IoT Edge` alınan veri çıkışı için kullanırız modülü bizim `BleConverterModule`.</span><span class="sxs-lookup"><span data-stu-id="20afc-158">This class is a `Azure IoT Edge` module, which we use to output the data received from our `BleConverterModule`.</span></span>

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

15. <span data-ttu-id="20afc-159">Dosyayı Farklı Kaydet `DotNetPrinterModule.cs` basarak `Ctrl`  +  `Shift`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="20afc-159">Save the file as `DotNetPrinterModule.cs` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="20afc-160">Farklı Kaydet iletişim kutusu, şirket içinde `Save as Type` açılır menüsünde, select `C# (*.cs;*.csx)`.</span><span class="sxs-lookup"><span data-stu-id="20afc-160">On the save as dialog box, in the `Save as Type` dropdown menu, select `C# (*.cs;*.csx)`.</span></span>

16. <span data-ttu-id="20afc-161">Adlı yeni bir dosya oluşturun `Untitled-1` basarak `Ctrl`  +  `N` anahtarları.</span><span class="sxs-lookup"><span data-stu-id="20afc-161">Create a new file called `Untitled-1` by pressing the `Ctrl` + `N` keys.</span></span>

17. <span data-ttu-id="20afc-162">Seri durumdan çıkarılacak `JSON` gelen aldığımız nesne `BleConverterModule`, Kopyala ve Yapıştır aşağıdaki kod parçacığını içine `Untitled-1` dosya.</span><span class="sxs-lookup"><span data-stu-id="20afc-162">To deserialize the `JSON` object that we receive from the `BleConverterModule`, Copy and paste the following code snippet into the `Untitled-1` file.</span></span> 

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

18. <span data-ttu-id="20afc-163">Dosyayı Farklı Kaydet `BleConverterData.cs` basarak `Ctrl`  +  `Shift`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="20afc-163">Save the file as `BleConverterData.cs` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="20afc-164">Farklı Kaydet iletişim kutusu, şirket içinde `Save as Type` açılır menüsünde, select `C# (*.cs;*.csx)`.</span><span class="sxs-lookup"><span data-stu-id="20afc-164">On the save as dialog box, in the `Save as Type` dropdown menu, select `C# (*.cs;*.csx)`.</span></span>

19. <span data-ttu-id="20afc-165">Adlı yeni bir dosya oluşturun `Untitled-1` basarak `Ctrl`  +  `N` anahtarları.</span><span class="sxs-lookup"><span data-stu-id="20afc-165">Create a new file called `Untitled-1` by pressing the `Ctrl` + `N` keys.</span></span>

20. <span data-ttu-id="20afc-166">İçine aşağıdaki kod parçacığını kopyalayıp `Untitled-1` dosya.</span><span class="sxs-lookup"><span data-stu-id="20afc-166">Copy and paste the following code snippet into the `Untitled-1` file.</span></span>

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

21. <span data-ttu-id="20afc-167">Dosyayı Farklı Kaydet `gw-config.json` basarak `Ctrl`  +  `Shift`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="20afc-167">Save the file as `gw-config.json` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="20afc-168">Farklı Kaydet iletişim kutusu, şirket içinde `Save as Type` açılır menüsünde, select `JSON (*.json;*.bowerrc;*.jshintrc;*.jscsrc;*.eslintrc;*.babelrc;*webmanifest)`.</span><span class="sxs-lookup"><span data-stu-id="20afc-168">On the save as dialog box, in the `Save as Type` dropdown menu, select `JSON (*.json;*.bowerrc;*.jshintrc;*.jscsrc;*.eslintrc;*.babelrc;*webmanifest)`.</span></span>

22. <span data-ttu-id="20afc-169">Yapılandırma dosyası çıktı dizinine kopyalama etkinleştirmek için güncelleştirme `IoTEdgeConverterModule.csproj` aşağıdaki XML blob ile:</span><span class="sxs-lookup"><span data-stu-id="20afc-169">To enable copying of the configuration file to the output directory, update the `IoTEdgeConverterModule.csproj` with the following XML blob:</span></span>

   ```xml
     <ItemGroup>
       <None Update="gw-config.json" CopyToOutputDirectory="PreserveNewest" />
     </ItemGroup>
   ```
    
   - <span data-ttu-id="20afc-170">Güncelleştirilmiş `IoTEdgeConverterModule.csproj` aşağıdaki görüntü gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="20afc-170">The updated `IoTEdgeConverterModule.csproj` should look like the following image:</span></span>

    ![Visual Studio Code güncelleştirilmiş .csproj dosyası](media/iot-hub-iot-edge-create-module/vscode-update-csproj.png)

23. <span data-ttu-id="20afc-172">Adlı yeni bir dosya oluşturun `Untitled-1` basarak `Ctrl`  +  `N` anahtarları.</span><span class="sxs-lookup"><span data-stu-id="20afc-172">Create a new file called `Untitled-1` by pressing the `Ctrl` + `N` keys.</span></span>

24. <span data-ttu-id="20afc-173">İçine aşağıdaki kod parçacığını kopyalayıp `Untitled-1` dosya.</span><span class="sxs-lookup"><span data-stu-id="20afc-173">Copy and paste the following code snippet into the `Untitled-1` file.</span></span>

   ```powershell
   Copy-Item -Path $env:userprofile\.nuget\packages\microsoft.azure.devices.gateway.native.windows.x64\1.1.3\runtimes\win-x64\native\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.runtime.serialization.formatters\4.3.0\lib\netstandard1.4\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.runtime.serialization.primitives\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\newtonsoft.json\10.0.2\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.componentmodel.typeconverter\4.3.0\lib\netstandard1.5\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.collections.nongeneric\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.collections.specialized\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   ```

25. <span data-ttu-id="20afc-174">Dosyayı Farklı Kaydet `binplace.ps1` basarak `Ctrl`  +  `Shift`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="20afc-174">Save the file as `binplace.ps1` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="20afc-175">Farklı Kaydet iletişim kutusu, şirket içinde `Save as Type` açılır menüsünde, select `PowerShell (*.ps1;*.psm1;*.psd1;*.pssc;*.psrc)`.</span><span class="sxs-lookup"><span data-stu-id="20afc-175">On the save as dialog box, in the `Save as Type` dropdown menu, select `PowerShell (*.ps1;*.psm1;*.psd1;*.pssc;*.psrc)`.</span></span>

26. <span data-ttu-id="20afc-176">Tuşuna basarak projeyi oluşturun `Ctrl`  +  `Shift`  +  `B` anahtarları.</span><span class="sxs-lookup"><span data-stu-id="20afc-176">Build the project by pressing the `Ctrl` + `Shift` + `B` keys.</span></span> <span data-ttu-id="20afc-177">İlk olarak, projeyi derlerken `Visual Studio Code` ile ister `No build task defined.` aşağıdaki resimde görüldüğü gibi iletişim:</span><span class="sxs-lookup"><span data-stu-id="20afc-177">When you build the project for the first time, `Visual Studio Code` prompts you with the `No build task defined.` dialog as seen in the following image:</span></span>

    ![Visual Studio Code yapı görev iletişim kutusu](media/iot-hub-iot-edge-create-module/vscode-build-task.png)

    <span data-ttu-id="20afc-179">bir) tıklatın `Configure Build Task` düğmesi.</span><span class="sxs-lookup"><span data-stu-id="20afc-179">a) Click the `Configure Build Task` button.</span></span>

    <span data-ttu-id="20afc-180">b) içinde `Select a Task Runner` iletişim kutusu açılır menüsünde.</span><span class="sxs-lookup"><span data-stu-id="20afc-180">b) In the `Select a Task Runner` dialog dropdown menu.</span></span> <span data-ttu-id="20afc-181">Seçin `.NET Core` aşağıdaki resimde görüldüğü gibi:</span><span class="sxs-lookup"><span data-stu-id="20afc-181">Select `.NET Core` as seen in the following image:</span></span> 

    ![Visual Studio Code görev iletişim kutusu seç](media/iot-hub-iot-edge-create-module/vscode-build-task-runner.png)

    <span data-ttu-id="20afc-183">c) tıkladığınızda `.NET Core` öğesi oluşturur `tasks.json` dosyasını, `.vscode` dizin ve dosya açılır `code editor` penceresi.</span><span class="sxs-lookup"><span data-stu-id="20afc-183">c) Clicking the `.NET Core` item creates the `tasks.json` file in your `.vscode` directory and opens the file in the `code editor` window.</span></span> <span data-ttu-id="20afc-184">Bu dosyayı değiştirmek için sekmeyi kapatmak gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="20afc-184">There is no need to modify this file, close the tab.</span></span>

27.  <span data-ttu-id="20afc-185">Açık `Visual Studio Code` basarak tümleşik terminal penceresi `Ctrl`  +  `backtick` anahtarları veya menüleri kullanarak `View`  ->  `Integrated Terminal` ve türü **.\binplace.ps1** içine `PowerShell` komut istemi.</span><span class="sxs-lookup"><span data-stu-id="20afc-185">Open the `Visual Studio Code` integrated terminal window by pressing the `Ctrl` + `backtick` keys or using the menus `View` -> `Integrated Terminal` and type **.\binplace.ps1** into the `PowerShell` command prompt.</span></span> <span data-ttu-id="20afc-186">Bu komut, tüm bağımlılıkları çıktı dizinine kopyalar.</span><span class="sxs-lookup"><span data-stu-id="20afc-186">This command copies all our dependencies to the output directory.</span></span>

28. <span data-ttu-id="20afc-187">Proje çıktı dizinine gidin `Integrated Terminal` yazarak penceresi **cd.\bin\Debug\netstandard1.3**.</span><span class="sxs-lookup"><span data-stu-id="20afc-187">Navigate to the projects output directory in the `Integrated Terminal` window by typing **cd .\bin\Debug\netstandard1.3**.</span></span>

29. <span data-ttu-id="20afc-188">Örnek Proje yazarak çalıştırırsınız **. \gw.exe gw-config.json** içine `Integrated Terminal` penceresi istemi.</span><span class="sxs-lookup"><span data-stu-id="20afc-188">Run the sample project by typing **.\gw.exe gw-config.json** into the `Integrated Terminal` window prompt.</span></span> 
    - <span data-ttu-id="20afc-189">Bu öğreticide yakından adımları izlediğinizden, şimdi çalıştırması `Azure IoT Edge BLE Data Converter Module` aşağıdaki resimde görüldüğü gibi örnek proje:</span><span class="sxs-lookup"><span data-stu-id="20afc-189">If you have followed the steps in this tutorial closely, you should now be running the `Azure IoT Edge BLE Data Converter Module` sample project as seen in the following image:</span></span>
    
        ![Visual Studio kodda çalıştıran sanal cihaz örneği](media/iot-hub-iot-edge-create-module/vscode-run.png)
    
    - <span data-ttu-id="20afc-191">Uygulamayı istiyorsanız, basın `<Enter>` anahtarı.</span><span class="sxs-lookup"><span data-stu-id="20afc-191">If you want to terminate the application, press the `<Enter>` key.</span></span>

>[!IMPORTANT]
<span data-ttu-id="20afc-192">Kullanılacak önerilmez `Ctrl`  +  `C` sonlandırmak için `IoT Edge` ağ geçidi uygulaması (diğer bir deyişle, **gw.exe**).</span><span class="sxs-lookup"><span data-stu-id="20afc-192">It is not recommended to use `Ctrl` + `C` to terminate the `IoT Edge` gateway application (that is, **gw.exe**).</span></span> <span data-ttu-id="20afc-193">Bu eylem aşırı ciddiyeti işlemin neden olarak.</span><span class="sxs-lookup"><span data-stu-id="20afc-193">As this action may cause the process to terminate abnormally.</span></span>

