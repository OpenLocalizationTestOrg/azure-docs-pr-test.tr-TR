---
title: "Geliştirmek ve Azure IOT kenarına Azure işlevleri dağıtmak için Visual Studio Code kullanma | Microsoft Docs"
description: "Geliştirme ve bağlam geçmeden bir C# Azure işlevleri VS code'da Azure IOT kenarıyla dağıtma"
services: iot-edge
keywords: 
author: shizn
manager: timlt
ms.author: xshi
ms.date: 12/20/2017
ms.topic: article
ms.service: iot-edge
ms.openlocfilehash: 219474a4577a76f5ceb9a9efaa3c349d633de047
ms.sourcegitcommit: 28178ca0364e498318e2630f51ba6158e4a09a89
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/24/2018
---
# <a name="use-visual-studio-code-to-develop-and-deploy-azure-functions-to-azure-iot-edge"></a>Visual Studio Code geliştirmek ve Azure IOT kenarına Azure işlevleri dağıtmak için kullanın

Bu makalede kullanmaya yönelik ayrıntılı yönergeler sağlanmaktadır [Visual Studio Code](https://code.visualstudio.com/) geliştirmek ve IOT kenar Azure işlevlerini dağıtmak için ana geliştirme aracı olarak. 

## <a name="prerequisites"></a>Önkoşullar
Bu öğretici, bir bilgisayar veya geliştirme makine olarak Windows veya Linux çalıştıran sanal makine kullandığınızı varsayar. IOT sınır cihazı başka bir fiziksel aygıt olabilir veya geliştirme makinenizde IOT kenar Cihazınızı benzetimini yapabilirsiniz.

Bu kılavuza başlamadan önce aşağıdaki öğreticiler tamamlanmış olduğundan emin olun.
- Sanal bir cihaz üzerinde Azure IOT kenar dağıtmak [Windows](https://docs.microsoft.com/azure/iot-edge/tutorial-simulate-device-windows) veya [Linux](https://docs.microsoft.com/azure/iot-edge/tutorial-simulate-device-linux)
- [Azure İşlevleri’ni dağıtma](https://docs.microsoft.com/azure/iot-edge/tutorial-deploy-function)

Önceki öğreticileri tamamladıktan sonra olmalıdır öğeleri gösteren bir denetim listesi aşağıda verilmiştir.

- [Visual Studio Code](https://code.visualstudio.com/). 
- [Visual Studio Code için Azure IOT kenar uzantısı](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.azure-iot-edge). 
- [C# Visual Studio Code (OmniSharp tarafından desteklenen) uzantısı](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp). 
- [Docker](https://docs.docker.com/engine/installation/)
- [.NET 2.0 SDK çekirdek](https://www.microsoft.com/net/core#windowscmd). 
- [Python 2.7](https://www.python.org/downloads/)
- [IOT kenar denetim komut dosyası](https://pypi.python.org/pypi/azure-iot-edge-runtime-ctl)
- AzureIoTEdgeFunction şablonu (`dotnet new -i Microsoft.Azure.IoT.Edge.Function`)
- Etkin bir IOT hub ile en az bir IOT sınır cihazı.

Yüklemek için de önerilen [VS Code Docker desteği](https://marketplace.visualstudio.com/items?itemName=PeterJausovec.vscode-docker) modülü görüntüler ve kapsayıcıları daha iyi yönetebilmek için.

> [!NOTE]
> Şu anda IOT kenar Azure işlevleri yalnızca C# destekler.

## <a name="deploy-azure-iot-functions-in-vs-code"></a>VS code'da Azure IOT işlevleri dağıtma
Öğreticideki [dağıtmak Azure işlevleri](https://docs.microsoft.com/azure/iot-edge/tutorial-deploy-function), güncelleştirme, yapı, VS Code'da işlev modülü görüntülerinizi yayımlama ve Azure işlevleri dağıtmak için Azure portalını ziyaret edin. Bu bölüm, dağıtmak ve Azure işlevleri izlemek için VS Code kullanma tanıtır.

### <a name="start-a-local-docker-registry"></a>Bir yerel docker kayıt defteri Başlat
Bu öğretici için Docker uyumlu kayıt kullanabilirsiniz. İki popüler Docker kayıt defteri hizmetlerinin kullanılabilir bulutta [Azure kapsayıcı kayıt defteri](https://docs.microsoft.com/azure/container-registry/) ve [Docker hub'a](https://docs.docker.com/docker-hub/repos/#viewing-repository-tags). Bu bölümde kullanan bir [yerel Docker kayıt](https://docs.docker.com/registry/deploying/), erken geliştirme sırasında amacı test etmek için daha kolay olduğu.
VS code'da **tümleşik terminal**(Ctrl + '), komutları yerel bir kayıt defteri başlatmak için aşağıdaki Çalıştır.  

```cmd/sh
docker run -d -p 5000:5000 --name registry registry:2 
```

> [!NOTE]
> Yukarıdaki örnekte yalnızca test etmek için uygun kayıt defteri yapılandırmaları gösterilmiştir. Üretime hazır kayıt defteri TLS tarafından korunması gerekir ve bir erişim denetim mekanizmasını ideal kullanmanız gerekir. Şunu kullanmanızı öneririz [Azure kapsayıcı kayıt defteri](https://docs.microsoft.com/azure/container-registry/) veya [Docker hub'a](https://docs.docker.com/docker-hub/repos/#viewing-repository-tags) üretime hazır IOT kenar modülleri dağıtmak için.

### <a name="create-a-function-project"></a>Bir işlev projesi oluşturma
Bir IOT kenar modülü oluşturmak için .NET tabanlı nasıl 2.0 kullanarak Visual Studio Code ve Azure IOT kenar uzantısı çekirdek aşağıdaki adımları gösterir. Bu bölümde önceki öğreticide tamamladıysanız, güvenli bir şekilde bu bölümü atlayabilirsiniz.

1. Visual Studio kod seçin **Görünüm** > **tümleşik Terminal** VS Code tümleşik Terminali açın.
2. Yüklemek (veya güncelleştirmek için) **AzureIoTEdgeFunction** şablonunda dotnet, tümleşik terminale aşağıdaki komutu çalıştırın:

   ```cmd/sh
   dotnet new -i Microsoft.Azure.IoT.Edge.Function
   ```
3. Yeni modül için bir proje oluşturun. Aşağıdaki komut proje klasörünü oluşturur **FilterFunction**, geçerli çalışma klasörü içinde:

   ```cmd/sh
   dotnet new aziotedgefunction -n FilterFunction
   ```
 
4. Seçin **Dosya > klasörünü Aç**, ardından gözatın **FilterFunction** klasörü ve VS code'da Proje Aç.
5. Gözat **FilterFunction** klasörü ve tıklatın **klasörü seçin** proje VS Code'da açın.
6. VS Code Explorer'da genişletin **EdgeHubTrigger Csharp** klasörünü açın **run.csx** dosya.
7. Dosyasının içeriğini aşağıdaki kodla değiştirin:

   ```csharp
   #r "Microsoft.Azure.Devices.Client"
   #r "Newtonsoft.Json"

   using System.IO;
   using Microsoft.Azure.Devices.Client;
   using Newtonsoft.Json;

   // Filter messages based on the temperature value in the body of the message and the temperature threshold value.
   public static async Task Run(Message messageReceived, IAsyncCollector<Message> output, TraceWriter log)
   {
        const int temperatureThreshold = 25;
        byte[] messageBytes = messageReceived.GetBytes();
        var messageString = System.Text.Encoding.UTF8.GetString(messageBytes);

        if (!string.IsNullOrEmpty(messageString))
        {
            // Get the body of the message and deserialize it
            var messageBody = JsonConvert.DeserializeObject<MessageBody>(messageString);

            if (messageBody != null && messageBody.machine.temperature > temperatureThreshold)
            {
                // Send the message to the output as the temperature value is greater than the threashold
                var filteredMessage = new Message(messageBytes);
                // Copy the properties of the original message into the new Message object
                foreach (KeyValuePair<string, string> prop in messageReceived.Properties)
                {
                    filteredMessage.Properties.Add(prop.Key, prop.Value);
                }
                // Add a new property to the message to indicate it is an alert
                filteredMessage.Properties.Add("MessageType", "Alert");
                // Send the message        
                await output.AddAsync(filteredMessage);
                log.Info("Received and transferred a message with temperature above the threshold");
            }
        }
    }

    //Define the expected schema for the body of incoming messages
    class MessageBody
    {
        public Machine machine {get;set;}
        public Ambient ambient {get; set;}
        public string timeCreated {get; set;}
    }
    class Machine
    {
       public double temperature {get; set;}
       public double pressure {get; set;}         
    }
    class Ambient
    {
       public double temperature {get; set;}
       public int humidity {get; set;}         
    }
   ```

8. Dosyayı kaydedin.

### <a name="create-a-docker-image-and-publish-it-to-your-registry"></a>Docker görüntü oluşturma ve kayıt defterine yayımlama

1. VS Code Explorer'da genişletin **Docker** klasör. Kapsayıcı platformunuz için klasör ya da genişletin **linux x64** veya **windows nano**.
2. Sağ **Dockerfile** dosya ve tıklayın **yapı IOT kenar modülü Docker görüntü**. 

    ![Docker yansıması oluştur](./media/how-to-vscode-develop-csharp-function/build-docker-image.png)

3. Gidin **FilterFunction** proje klasörünü ve tıklatın **EXE_DIR olarak klasör seç**. 
4. VS Code pencerenin üstündeki açılır metin kutusuna görüntü adı girin. Örneğin: `<your container registry address>/filterfunction:latest`. Yerel kayıt defterine dağıtıyorsanız, olmalıdır `localhost:5000/filterfunction:latest`.
5. Görüntü Docker deponuza iletin. Kullanım **kenar: anında IOT kenar modülü Docker görüntü** komut ve VS Code pencerenin üstündeki açılır metin kutusuna resim URL'si girin. Yukarıdaki adım içinde kullanılan aynı resim URL'si kullanın.
    ![Anında iletme docker görüntüsü](./media/how-to-vscode-develop-csharp-function/push-image.png)

### <a name="deploy-your-function-to-iot-edge"></a>IOT kenarına işlevinizi dağıtma

1. Açık `deployment.json` dosya, yerine **modülleri** altındaki içerik bölümü ile:
   ```json
   "tempSensor": {
      "version": "1.0",
      "type": "docker",
      "status": "running",
      "restartPolicy": "always",
      "settings": {
         "image": "microsoft/azureiotedge-simulated-temperature-sensor:1.0-preview",
         "createOptions": ""
      }
   },
   "filterfunction": {
      "version": "1.0",
      "type": "docker",
      "status": "running",
      "restartPolicy": "always",
      "settings": {
         "image": "localhost:5000/filterfunction:latest",
         "createOptions": ""
      }
   }
   ```

2. Değiştir **yollar** altındaki içerik bölümü ile:
   ```json
       "routes":{
           "sensorToFilter":"FROM /messages/modules/tempSensor/outputs/temperatureOutput INTO BrokeredEndpoint(\"/modules/filterfunction/inputs/input1\")",
           "filterToIoTHub":"FROM /messages/modules/filterfunction/outputs/* INTO $upstream"
       }
   ```
   > [!NOTE]
   > Burada bu iletileri akış çalışma zamanında bildirim temelli kuralları tanımlar. Bu öğreticide, iki yol gerekir. İlk yol FilterMessages işleyici ile yapılandırılmış uç noktası olduğu sıcaklık algılayıcısı iletilerden "input1" uç noktası aracılığıyla filtre işlevine taşımaları. İkinci yol filtre işlevi iletilerden IOT Hub'ına taşımaları. Bu rotadaki kenar Hub'ın IOT Hub'ına iletileri göndermek için söyler özel bir hedef Yukarı Akış.

3. Bu dosyayı kaydedin.
4. Komut Palette seçin **kenar: sınır cihazı için dağıtımı oluşturma**. Ardından IOT kenar cihaz Kimliğinizi bir dağıtım oluşturmak için seçin. Cihaz kimliği aygıt listesinde sağ tıklatın ve seçin **sınır cihazı için dağıtımı oluşturma**.

    ![Dağıtım oluşturma](./media/how-to-vscode-develop-csharp-function/create-deployment.png)

5. Seçin `deployment.json` , güncelleştirildi. Çıktı penceresinde dağıtımınız için karşılık gelen çıkışları görebilirsiniz.
6. Edge çalışma zamanı komutu Palette başlatın. **Edge: Başlangıç köşesi**
7. Benzetimli algılayıcı ve filtre işleviyle Docker Explorer'da çalıştırma başlatın, IOT kenar çalışma zamanı görebilirsiniz.

    ![Çalışan çözümü](./media/how-to-vscode-develop-csharp-function/solution-running.png)

8. Edge cihaz Kimliğinizi sağ tıklayın ve VS code'da D2C iletileri izleyebilirsiniz.

    ![İzleme iletileri](./media/how-to-vscode-develop-csharp-function/monitor-d2c-messages.png)


## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide bir Azure işlevi IOT kenarına oluşturulan ve VS code'da IOT sınır cihazı için dağıtılır. VS code'da Azure IOT kenar geliştirirken diğer senaryolar hakkında bilgi edinmek için aşağıdaki öğreticileri herhangi birini açın devam edebilirsiniz.

> [!div class="nextstepaction"]
> [VS code'da Azure işlevlerinde hata ayıklama](how-to-vscode-debug-azure-function.md)
