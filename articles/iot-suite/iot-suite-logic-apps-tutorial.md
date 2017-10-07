---
title: aaaAzure IOT paketi ve Logic Apps | Microsoft Docs
description: "Bir öğretici nasıl toohook Logic Apps tooAzure IOT paketi iş sürecini için ayarlama."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 4629a7af-56ca-4b21-a769-5fa18bc3ab07
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: corywink
ms.openlocfilehash: 6ef7311ac38f4e2ddb032cff0fb73591da5f76c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-connect-logic-app-tooyour-azure-iot-suite-remote-monitoring-preconfigured-solution"></a>Öğretici: Mantıksal uygulama tooyour Azure IOT paketi uzaktan önceden yapılandırılmış izleme çözümü bağlantı
Merhaba [Microsoft Azure IOT paketi] [ lnk-internetofthings] Uzaktan izleme çözümü mükemmel şekilde tooget hızlı bir şekilde bir IOT çözüm exemplifies bir uçtan uca özellik kümesi ile başlatıldı. Bu öğreticide nasıl tooadd mantıksal uygulama tooyour Microsoft Azure IOT paketi çözümünün önceden yapılandırılmış Uzaktan izleme aracılığıyla açıklanmaktadır. Bu adımları tooa iş sürecini bağlanarak daha IOT çözümünüzü nasıl yararlanabileceğinizi gösterir.

*Tooprovision Uzaktan izleme çözümü nasıl önceden yapılandırılmış üzerinde bir kılavuz arıyorsanız bkz [Öğreticisi: Merhaba IOT önceden yapılandırılmış çözümleri kullanmaya başlama][lnk-getstarted].*

Bu öğretici başlamadan önce aşağıdakileri yapmanız gerekir:

* Sağlama hello Uzaktan izleme çözümü Azure aboneliğinizde.
* SendGrid hesap tooenable oluşturmak, iş sürecini tetikleyen bir e-posta toosend. Ücretsiz bir deneme hesabı için kaydolabilirsiniz [SendGrid](https://sendgrid.com/) tıklayarak **ücretsiz deneyin**. Ücretsiz deneme hesabınız için kaydettikten sonra toocreate gereken bir [API anahtarı](https://sendgrid.com/docs/User_Guide/Settings/api_keys.html) toosend posta izinler veren SendGrid içinde. Daha sonra hello Öğreticide bu API anahtarı gerekir.

toocomplete Bu öğreticide, Visual Studio 2015 veya Visual Studio 2017 toomodify hello eylemlerinde hello önceden yapılandırılmış çözüm arka ucu gerekir.

Önceden yapılandırılmış Çözüm zaten sağladığınız Uzaktan izleme varsayıldığında, bu çözümde hello toohello kaynak grubunun gidin [Azure portal][lnk-azureportal]. Merhaba kaynak grubuna sahip aynı adı hello çözüm adı gibi hello Uzaktan izleme çözümünüz ne zaman sağladığınız seçtiniz. Merhaba kaynak grubunda Azure kaynaklarını hello hello Klasik Azure portalı bulabilirsiniz Azure Active Directory Uygulama dışında çözümünüz için tüm hello sağlanan görebilirsiniz. Merhaba aşağıdaki ekran görüntüsünde gösteren bir örnek **kaynak grubu** Uzaktan izleme için dikey önceden yapılandırılmış çözüm:

![](media/iot-suite-logic-apps-tutorial/resourcegroup.png)

toobegin, çözüm hello mantığı uygulama toouse hello ile ayarlama önceden yapılandırılmış.

## <a name="set-up-hello-logic-app"></a>Mantıksal uygulama Hello ayarlayın
1. Tıklatın **Ekle** , kaynak grubu dikey penceresinde hello Azure Portalı'ndaki hello üstünde.
2. Arama **mantıksal uygulama**, onu seçin ve ardından **oluşturma**.
3. Merhaba dolgu **adı** ve kullanım hello aynı **abonelik** ve **kaynak grubu** Uzaktan izleme çözümünüzü sağlarken kullanılan. **Oluştur**'a tıklayın.
   
    ![](media/iot-suite-logic-apps-tutorial/createlogicapp.png)
4. Dağıtımınız tamamlandığında, bir kaynak olarak mantıksal uygulama listelenen hello kaynak grubunuzdaki görebilirsiniz.
5. Tıklatın hello mantıksal uygulama toonavigate toohello mantıksal uygulama dikey penceresinde, select hello **boş mantıksal uygulama** şablonu tooopen hello **Logic Apps Tasarımcısı**.
   
    ![](media/iot-suite-logic-apps-tutorial/logicappsdesigner.png)
6. Seçin **isteği**. Bu eylem, gelen HTTP isteğiyle belirli bir JSON yükü davranır tetikleyici olarak biçimlendirilmiş belirtir.
7. İstek gövdesi JSON şeması hello koddan hello yapıştırın:
   
    ```json
    {
      "$schema": "http://json-schema.org/draft-04/schema#",
      "id": "/",
      "properties": {
        "DeviceId": {
          "id": "DeviceId",
          "type": "string"
        },
        "measuredValue": {
          "id": "measuredValue",
          "type": "integer"
        },
        "measurementName": {
          "id": "measurementName",
          "type": "string"
        }
      },
      "required": [
        "DeviceId",
        "measurementName",
        "measuredValue"
      ],
      "type": "object"
    }
    ```
   
   > [!NOTE]
   > Merhaba mantıksal uygulama kaydedebilir, ancak öncelikle bir eylem eklemeniz gerekir sonra hello HTTP post hello URL'sini kopyalayabilirsiniz.
   > 
   > 
8. Tıklatın **+ yeni adım** el ile tetikleyici altında. Ardından **Eylem Ekle**.
   
    ![](media/iot-suite-logic-apps-tutorial/logicappcode.png)
9. Arama **SendGrid - e-postası gönderme** ve tıklatın.
   
    ![](media/iot-suite-logic-apps-tutorial/logicappaction.png)
10. Merhaba bağlantı için bir ad girin **SendGridConnection**, hello girin **SendGrid API anahtarı** SendGrid hesabınızı ayarlama'ı tıklattığınızda, oluşturduğunuz **oluşturma**.
    
    ![](media/iot-suite-logic-apps-tutorial/sendgridconnection.png)
11. E-posta adresleri, kendi tooboth hello eklemek **gelen** ve **için** alanları. Ekleme **Uzaktan izleme uyarı [DeviceID]** toohello **konu** alan. Merhaba, **e-posta gövdesi** alanında, eklemek **aygıt [DeviceID], [measurementName] [measuredValue] değerle bildirdi.** Ekleyebileceğiniz **[DeviceID]**, **[measurementName]**, ve **[measuredValue]** hello tıklayarak **önceki adımlarıveriekleyebilirsiniz**bölümü.
    
    ![](media/iot-suite-logic-apps-tutorial/sendgridaction.png)
12. Tıklatın **kaydetmek** hello üst menüde.
13. Merhaba tıklatın **isteği** tetikleyici ve kopyalama hello **Http Post toothis URL** değeri. Bu URL'yi daha sonra Bu öğreticide gerekir.

> [!NOTE]
> Logic Apps etkinleştirmek, toorun [farklı türlerde eylem] [ lnk-logic-apps-actions] Office 365'te Eylemler dahil olmak üzere. 
> 
> 

## <a name="set-up-hello-eventprocessor-web-job"></a>EventProcessor Web işi Hello ayarlayın
Bu bölümde, önceden yapılandırılmış çözüm toohello mantıksal oluşturduğunuz uygulama bağlayın. toocomplete bu görev, bir cihaz algılayıcı değeri bir eşiği aştığında harekete hello URL tootrigger hello mantıksal uygulama toohello eylem ekleme.

1. Git istemci tooclone hello en son sürümüne hello kullan [azure-iot-remote-monitoring github deposunu][lnk-rmgithub]. Örneğin:
   
    ```cmd
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```
2. Visual Studio'da hello açın **RemoteMonitoring.sln** kopyasından hello yerel hello deposu.
3. Açık hello **ActionRepository.cs** hello dosyasında **altyapı\\depo** klasör.
4. Güncelleştirme hello **actionIds** hello sözlüğüyle **Http Post toothis URL** mantığı uygulamanızdan gibi Not:
   
    ```csharp
    private Dictionary<string,string> actionIds = new Dictionary<string, string>()
    {
        { "Send Message", "<Http Post toothis URL>" },
        { "Raise Alarm", "<Http Post toothis URL>" }
    };
    ```
5. Çözümde Hello değişiklikleri kaydedin ve Visual Studio çıkın.

## <a name="deploy-from-hello-command-line"></a>Merhaba komut satırından dağıtma
Bu bölümde, güncelleştirilmiş sürümü şu anda Azure'da çalışan hello Uzaktan izleme çözümü tooreplace hello dağıtın.

1. Merhaba aşağıdaki [geliştirme Kurulum] [ lnk-devsetup] ortamınızı dağıtımı için yönergeler tooset.
2. yerel olarak toodeploy izleyin hello [yerel dağıtım] [ lnk-localdeploy] yönergeler.
3. toodeploy toohello Bulut ve var olan bulut dağıtımınızı güncelleştirmek, hello izleyin [bulut dağıtımı] [ lnk-clouddeploy] yönergeler. Merhaba dağıtım adı olarak özgün dağıtımınızın Hello adı kullanın. Merhaba özgün dağıtım çağrıldı örneğin **demologicapp**, komutu aşağıdaki hello kullanın:
   
   ```cmd
   build.cmd cloud release demologicapp
   ```
   
   Merhaba komut dosyasını çalıştırır derlerken toouse aynı hello emin olun Azure hesabınız, abonelik, bölgeye ve hello çözüm sağladığında kullanılan Active Directory örneğini.

## <a name="see-your-logic-app-in-action"></a>Mantıksal uygulamanızı eylem bakın
Merhaba Uzaktan izleme çözümü bir çözüm sağladığınızda, varsayılan olarak ayarlanan iki kuralları vardır. Merhaba üzerinde hem kurallardır **SampleDevice001** aygıt:

* Sıcaklık > 38.00
* Nem > 48.00

Merhaba sıcaklık kuralını tetikler hello **yükseltmek Alarm** eylem ve hello nem kuralını tetikler hello **SendMessage** eylem. Kullandığınız varsayılarak hello aynı URL için her iki Eylemler hello **ActionRepository** sınıfı, her iki kural için logic app Tetikleyicileri. SendGrid toosend bir e-posta toohello hem kurallarıyla **için** hello uyarı ayrıntılarını adresiyle.

> [!NOTE]
> Merhaba eşiğine her zaman hello mantıksal uygulama tootrigger devam eder. tooavoid gereksiz e-postalar, ya da devre dışı bırakabilirsiniz hello kuralları, çözüm portalı veya devre dışı bırakma hello mantıksal uygulama hello içinde [Azure portal][lnk-azureportal].
> 
> 

Merhaba Portalı'nda Hello mantıksal uygulama çalıştığında, ayrıca tooreceiving e-postalar, de görebilirsiniz:

![](media/iot-suite-logic-apps-tutorial/logicapprun.png)

## <a name="next-steps"></a>Sonraki adımlar
Bir mantıksal uygulama tooconnect hello önceden yapılandırılmış çözüm tooa iş sürecini kullanmış olduğunuz, hello önceden yapılandırılmış çözümleri özelleştirme hello seçenekleri hakkında daha fazla bilgi edinebilirsiniz:

* [Dinamik telemetri hello Uzaktan izleme çözümü ile kullanma][lnk-dynamic]
* [Cihaz bilgi meta verilerde hello Uzaktan izleme çözümü][lnk-devinfo]

[lnk-dynamic]: iot-suite-dynamic-telemetry.md
[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[lnk-internetofthings]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-getstarted]: iot-suite-getstarted-preconfigured-solutions.md
[lnk-azureportal]: https://portal.azure.com
[lnk-logic-apps-actions]: ../connectors/apis-list.md
[lnk-rmgithub]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-devsetup]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/dev-setup.md
[lnk-localdeploy]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/local-deployment.md
[lnk-clouddeploy]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/cloud-deployment.md
