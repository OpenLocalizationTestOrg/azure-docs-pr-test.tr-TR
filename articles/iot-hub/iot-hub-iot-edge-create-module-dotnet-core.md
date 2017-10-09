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
# <a name="create-an-azure-iot-edge-module-with-cx23"></a>Bir Azure IOT kenar modülü C & #x23 oluşturun;

Bu öğretici paylaşan nasıl modül için bir toocreate `Azure IoT Edge` kullanarak `Visual Studio Code` ve `C#`.

Bu öğreticide, biz ortamı ayarı yol ve nasıl toowrite bir [bırak](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) veri dönüştürücü modülünü kullanarak hello son `Azure IoT Edge NuGet` paketleri. 

>[!NOTE]
Bu öğretici hello kullanarak `.NET Core SDK`, platformlar arası uyumluluk destekler. Merhaba aşağıdaki öğretici hello kullanarak yazılır `Windows 10` işletim sistemi. Bu öğreticide hello komutları bazıları bağlı olarak farklı olabilir, `development environment`. 

## <a name="prerequisites"></a>Ön koşullar

Bu bölümde, biz Kurulum ortamınız için `Azure IoT Edge` modülü geliştirme. Tooboth geçerlidir **64-bit Windows** ve **64-bit Linux (Ubuntu/Debian 8)** işletim sistemleri.

yazılımı aşağıdaki hello gereklidir:

- [Git istemci](https://git-scm.com/downloads)
- [.NET Core SDK](https://www.microsoft.com/net/core#windowscmd)
- [Visual Studio Code](https://code.visualstudio.com/)

Bu örnek için tooclone hello depodaki gerekmez, ancak tüm hello Bu öğreticide ele alınan kod örnek depo aşağıdaki hello bulunur:

- `git clone https://github.com/Azure-Samples/iot-edge-samples.git`.
- `cd iot-edge-samples/dotnetcore/simulated_ble`

## <a name="getting-started"></a>Başlarken

1. Yükleme `.NET Core SDK`.
2. Yükleme `Visual Studio Code` ve hello `C# extension` hello Visual Studio kod Market gelen.

Bu görünümü, [hızlı videosu](https://channel9.msdn.com/Blogs/dotnet/Get-started-VSCode-Csharp-NET-Core-Windows) tooget nasıl kullanmaya hakkında `Visual Studio Code` ve hello `.NET Core SDK`.

## <a name="creating-hello-azure-iot-edge-converter-module"></a>Hello Azure IOT kenar dönüştürücü modül oluşturma

1. Yeni bir başlatma `.NET Core` sınıf kitaplığı C# projesi:
    - Bir komut istemi açın (`Windows + R` -> `cmd` -> `enter`).
    - Burada gibi toocreate hello toohello klasörüne gidin `C#` projesi.
    - Tür **dotnet yeni classlib -o IoTEdgeConverterModule -f netstandard1.3**. 
    - Bu komut adlı boş bir sınıf oluşturur `Class1.cs` projeleri dizininizde.
2. Burada yeni oluşturduğumuz hello sınıf kitaplığı proje yazarak toohello klasörüne gidin **cd IoTEdgeConverterModule**.
3. Açık hello projesinde `Visual Studio Code` yazarak **kodu.**.
4. Başlangıç projesi olarak açıldıktan sonra `Visual Studio Code`, üzerinde hello tıklatın **IoTEdgeConverterModule.csproj** hello görüntü aşağıdaki gösterildiği gibi tooopen hello dosyası:

    ![Visual Studio Code düzenleme penceresi](media/iot-hub-iot-edge-create-module/vscode-edit-csproj.png)

5. Merhaba Ekle `XML` hello kapanış arasında kod parçacığını aşağıdaki hello gösterilen blob `PropertyGroup` etiketi ve kapanış hello `Project` etiketi; altı görüntü önceki hello içinde satır ve tuşlarına basarak hello dosyasını kaydedin `Ctrl`  +  `S`.

   ```xml
     <ItemGroup>
       <PackageReference Include="Microsoft.Azure.Devices.Gateway.Module.NetStandard" Version="1.0.5" />
       <PackageReference Include="System.Threading.Thread" Version="4.3.0" />
       <PackageReference Include="Newtonsoft.Json" Version="10.0.2" />
     </ItemGroup> 
   ```

6. Merhaba kaydettikten sonra `.csproj` dosyası `Visual Studio Code` sizinle ister bir `unresolved dependencies` görüntü aşağıdaki hello görülen iletişim: 

    ![Visual Studio Code geri yükleme bağımlılıkları iletişim kutusu](media/iot-hub-iot-edge-create-module/vscode-restore.png)

    bir) tıklatın `Restore` tüm hello başvurular hello projelerinde toorestore `.csproj` hello dahil olmak üzere dosya `PackageReferences` ekledik. 

    b) `Visual Studio Code` hello otomatik olarak oluşturur `project.assets.json` projelerinizi dosyasında `obj` klasör. Bu dosya, projenizin bağımlılıkları toomake sonraki geri yüklemeler daha hızlı hakkında bilgi içerir.
 
    >[!NOTE]
    `.NET Core Tools`MSBuild tabanlı sunulmuştur. Anlamına gelen bir `.csproj` proje dosyası oluşturuldu. yerine bir `project.json`.

    - Varsa `Visual Studio Code` Tamam, sizden istemez biz el ile yapabilirsiniz. Açık hello `Visual Studio Code` tuşuna basarak hello tarafından tümleşik terminal penceresi `Ctrl`  +  `backtick` anahtarları veya hello menüleri kullanarak `View`  ->  `Integrated Terminal`.
    - Merhaba, `Integrated Terminal` pencere türü **dotnet geri yükleme**.
    
7. Merhaba yeniden adlandırma `Class1.cs` çok dosya`BleConverterModule.cs`. 

    bir) toorename hello dosya ilk hello dosyada tıklatın ardından basın hello `F2` anahtarı.
    
    b) hello yeni adı yazın **BleConverterModule**, görüntü aşağıdaki hello görüldüğü gibi:

    ![Visual Studio Code bir sınıfı yeniden adlandırma](media/iot-hub-iot-edge-create-module/vscode-rename.png)

8. Merhaba Hello varolan kodla `BleConverterModule.cs` dosya kopyalama ve yapıştırma hello içine kod parçacığını aşağıdaki tarafından `BleConverterModule.cs` dosya.

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

9. Tuşlarına basarak Hello dosyasını kaydedin `Ctrl`  +  `S`.

10. Adlı yeni bir dosya oluşturun `Untitled-1` tuşuna basarak hello tarafından `Ctrl`  +  `N` anahtarları görüntü aşağıdaki hello görüldüğü gibi:

    ![Visual Studio Code yeni dosya](media/iot-hub-iot-edge-create-module/vscode-new-file.png)

11. toodeserialize hello `JSON` benzetimli hello aldığımız nesne `BLE` aygıt, hello koddan kopyalama hello `Untitled-1` dosya kod düzenleyici penceresini. 

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

12. Merhaba dosyası olarak kaydetmeniz `BleData.cs` basarak `Ctrl`  +  `Shift`  +  `S` anahtarları.
    - Merhaba üzerinde Kaydet iletişim kutusunda hello olarak `Save as Type` açılır menüsünde, select `C# (*.cs;*.csx)` görüntü aşağıdaki hello görüldüğü gibi:

    ![Visual Studio Code iletişim kutusu olarak Kaydet](media/iot-hub-iot-edge-create-module/vscode-save-as.png)

13. Adlı yeni bir dosya oluşturun `Untitled-1` tuşuna basarak hello tarafından `Ctrl`  +  `N` anahtarları.

14. Kod parçacığı hello aşağıdaki hello kopyalayıp `Untitled-1` dosya. Bu sınıf, bir `Azure IoT Edge` toooutput hello veri aldı kullanırız modülü bizim `BleConverterModule`.

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

15. Merhaba dosyası olarak kaydetmeniz `DotNetPrinterModule.cs` basarak `Ctrl`  +  `Shift`  +  `S`.
    - Merhaba üzerinde Kaydet iletişim kutusunda hello olarak `Save as Type` açılır menüsünde, select `C# (*.cs;*.csx)`.

16. Adlı yeni bir dosya oluşturun `Untitled-1` tuşuna basarak hello tarafından `Ctrl`  +  `N` anahtarları.

17. toodeserialize hello `JSON` hello aldığımız nesne `BleConverterModule`, Kopyala ve Yapıştır hello aşağıdaki kod parçacığını hello içine `Untitled-1` dosya. 

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

18. Merhaba dosyası olarak kaydetmeniz `BleConverterData.cs` basarak `Ctrl`  +  `Shift`  +  `S`.
    - Merhaba üzerinde Kaydet iletişim kutusunda hello olarak `Save as Type` açılır menüsünde, select `C# (*.cs;*.csx)`.

19. Adlı yeni bir dosya oluşturun `Untitled-1` tuşuna basarak hello tarafından `Ctrl`  +  `N` anahtarları.

20. Kod parçacığı hello aşağıdaki hello kopyalayıp `Untitled-1` dosya.

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

21. Merhaba dosyası olarak kaydetmeniz `gw-config.json` basarak `Ctrl`  +  `Shift`  +  `S`.
    - Merhaba üzerinde Kaydet iletişim kutusunda hello olarak `Save as Type` açılır menüsünde, select `JSON (*.json;*.bowerrc;*.jshintrc;*.jscsrc;*.eslintrc;*.babelrc;*webmanifest)`.

22. çıktı dizini, güncelleştirme hello tooenable hello yapılandırma dosyası toohello kopyalama `IoTEdgeConverterModule.csproj` XML blob aşağıdaki hello ile:

   ```xml
     <ItemGroup>
       <None Update="gw-config.json" CopyToOutputDirectory="PreserveNewest" />
     </ItemGroup>
   ```
    
   - güncelleştirilmiş hello `IoTEdgeConverterModule.csproj` hello görünümlü aşağıdaki görüntü:

    ![Visual Studio Code güncelleştirilmiş .csproj dosyası](media/iot-hub-iot-edge-create-module/vscode-update-csproj.png)

23. Adlı yeni bir dosya oluşturun `Untitled-1` tuşuna basarak hello tarafından `Ctrl`  +  `N` anahtarları.

24. Kod parçacığı hello aşağıdaki hello kopyalayıp `Untitled-1` dosya.

   ```powershell
   Copy-Item -Path $env:userprofile\.nuget\packages\microsoft.azure.devices.gateway.native.windows.x64\1.1.3\runtimes\win-x64\native\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.runtime.serialization.formatters\4.3.0\lib\netstandard1.4\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.runtime.serialization.primitives\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\newtonsoft.json\10.0.2\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.componentmodel.typeconverter\4.3.0\lib\netstandard1.5\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.collections.nongeneric\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.collections.specialized\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   ```

25. Merhaba dosyası olarak kaydetmeniz `binplace.ps1` basarak `Ctrl`  +  `Shift`  +  `S`.
    - Merhaba üzerinde Kaydet iletişim kutusunda hello olarak `Save as Type` açılır menüsünde, select `PowerShell (*.ps1;*.psm1;*.psd1;*.pssc;*.psrc)`.

26. Tuşuna basarak hello tarafından Merhaba Projeyi derlemek `Ctrl`  +  `Shift`  +  `B` anahtarları. İlk kez hello için Merhaba projeyi derlerken `Visual Studio Code` ile Merhaba ister `No build task defined.` görüntü aşağıdaki hello görülen iletişim:

    ![Visual Studio Code yapı görev iletişim kutusu](media/iot-hub-iot-edge-create-module/vscode-build-task.png)

    bir) hello tıklatın `Configure Build Task` düğmesi.

    b) içinde hello `Select a Task Runner` iletişim kutusu açılır menüsünde. Seçin `.NET Core` görüntü aşağıdaki hello görüldüğü gibi: 

    ![Visual Studio Code görev iletişim kutusu seç](media/iot-hub-iot-edge-create-module/vscode-build-task-runner.png)

    c) tıkladığınızda hello `.NET Core` öğesi oluşturur hello `tasks.json` dosyasını, `.vscode` dizin ve açılır hello hello dosyasında `code editor` penceresi. Bu dosya, Kapat hello sekmesini gerek toomodify yoktur.

27.  Açık hello `Visual Studio Code` tuşuna basarak hello tarafından tümleşik terminal penceresi `Ctrl`  +  `backtick` anahtarları veya hello menüleri kullanarak `View`  ->  `Integrated Terminal` ve türü **.\binplace.ps1**hello içine `PowerShell` komut istemi. Bu komut tüm bizim bağımlılıkları toohello çıktı dizinine kopyalar.

28. Merhaba, toohello projeleri çıktı dizinine gidin `Integrated Terminal` yazarak penceresi **cd.\bin\Debug\netstandard1.3**.

29. Merhaba örnek proje yazarak çalıştırırsınız **. \gw.exe gw-config.json** hello içine `Integrated Terminal` penceresi istemi. 
    - Bu öğreticide yakından hello adımları izlediğinizde, şimdi hello çalıştırması `Azure IoT Edge BLE Data Converter Module` görüntü aşağıdaki hello görülen örnek proje:
    
        ![Visual Studio kodda çalıştıran sanal cihaz örneği](media/iot-hub-iot-edge-create-module/vscode-run.png)
    
    - Tooterminate Merhaba uygulaması istiyorsanız hello basın `<Enter>` anahtarı.

>[!IMPORTANT]
Toouse önerilmez `Ctrl`  +  `C` tooterminate hello `IoT Edge` ağ geçidi uygulaması (diğer bir deyişle, **gw.exe**). Bu eylemin hello işlem tooterminate aşırı neden olabilir ve.

