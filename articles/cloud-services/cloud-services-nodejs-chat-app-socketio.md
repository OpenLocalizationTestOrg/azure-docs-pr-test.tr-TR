---
title: "Socket.IO kullanarak aaaNode.js uygulaması | Microsoft Docs"
description: "Nasıl bir node.js uygulamasında toouse Socket.IO Azure üzerinde barındırılan öğrenin."
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 7f9435e0-7732-4aa1-a4df-ea0e894b847f
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 47c6c4a748938959315b880340f41f31faab4ea9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-chat-application-with-socketio-on-an-azure-cloud-service"></a>Bir Azure bulut hizmeti Socket.IO ile bir Node.js sohbet uygulaması oluşturma
Socket.IO node.js sunucunuz ve istemcileriniz arasında arasında gerçek zamanlı iletişim sağlar. Bu öğretici bir yuva barındırma aracılığıyla yol gösterir. G/ç Azure sohbet uygulamaya dayalı. Socket.IO ile ilgili daha fazla bilgi için bkz: <http://socket.io/>.

Tamamlanan hello uygulamasının ekran görüntüsü aşağıda verilmiştir:

![Azure üzerinde barındırılan hello hizmet gösteren bir tarayıcı penceresi][completed-app]  

## <a name="prerequisites"></a>Ön koşullar
Ürünler aşağıdaki o hello emin olun ve bu makaledeki yüklü toosuccessfully tam hello örnek sürümleri:

* [Visual Studio](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx)'yu yükleme
* [Node.js](https://nodejs.org/download/)’yi yükleme
* Yükleme [Python sürümü 2.7.10](https://www.python.org/)

## <a name="create-a-cloud-service-project"></a>Bir bulut hizmeti projesi oluşturma
Merhaba aşağıdaki adımları Merhaba Socket.IO uygulaması barındıracak hello bulut hizmeti projesi oluşturun.

1. Merhaba gelen **Başlat menüsü** veya **Başlat ekranında**, arama **Windows PowerShell**. Son olarak, sağ **Windows PowerShell** seçip **yönetici olarak çalıştır**.
   
    ![Azure PowerShell simgesi][powershell-menu]
2. Adlı bir dizin oluşturun **c:\\düğümü**. 
   
        PS C:\> md node
3. Değiştirme dizinleri toohello **c:\\düğümü** dizini
   
        PS C:\> cd node
4. Aşağıdaki komutları toocreate adlı yeni bir çözüm hello girin **chatapp** ve adlı çalışan rolü **WorkerRole1**:
   
        PS C:\node> New-AzureServiceProject chatapp
        PS C:\Node> Add-AzureNodeWorkerRole
   
    Yanıt aşağıdaki hello görürsünüz:
   
    ![Merhaba yeni-azureservice ve ekleme azurenodeworkerrolecmdlets Hello çıktısı](./media/cloud-services-nodejs-chat-app-socketio/socketio-1.png)

## <a name="download-hello-chat-example"></a>Merhaba sohbet örnek indirme
Bu proje için hello sohbet hello örnekten kullanacağız [Socket.IO GitHub deposunu]. Aşağıdaki adımları toodownload hello örneğine hello gerçekleştirmek ve daha önce oluşturduğunuz toohello proje ekleyin.

1. Hello kullanarak hello deposu yerel bir kopyasını oluşturma **kopya** düğmesi. Merhaba de kullanabilir **ZIP** düğmesini toodownload hello projesi.
   
   ![Bir tarayıcı penceresinde hello ZIP indirme simge vurgulanmış ile https://github.com/LearnBoost/Socket.io/Tree/master/examples/Chat, görüntüleme][chat-example-view]
2. Hello gelmesini kadar hello yerel deposu hello dizin yapısını gidin **örnekler\\sohbet** dizin. Bu dizin toothe Hello içeriğini kopyalayın **C:\\düğümü\\chatapp\\WorkerRole1** daha önce oluşturduğunuz dizin.
   
   ![Merhaba örnekler Hello içeriğini görüntüleme explorer\\hello arşivinden ayıklanan sohbet dizini][chat-contents]
   
   Merhaba vurgulanan hello ekran görüntüsü yukarıdaki hello kopyalanan hello dosya öğeleridir **örnekler\\sohbet** dizini
3. Merhaba, **C:\\düğümü\\chatapp\\WorkerRole1** dizin, delete hello **server.js** dosya ve hello yeniden adlandırma **app.js**çok dosya**server.js**. Bu hello varsayılan kaldırır **server.js** hello tarafından daha önce oluşturduğunuz dosya **Ekle AzureNodeWorkerRole** cmdlet'i ve Merhaba uygulaması ile dosya değiştirir hello sohbet örnek.

### <a name="modify-serverjs-and-install-modules"></a>Server.js değiştirmek ve modülleri yükleme
Sınama hello uygulamada önce hello Azure öykünücüsü, biz bazı küçük değişiklikler yapmanız gerekir. Aşağıdaki adımları toothe server.js dosyasına hello gerçekleştirin:

1. Açık hello **server.js** Visual Studio veya herhangi bir metin düzenleyicisi dosyası.
2. Hello bulur **modülü bağımlılıkları** bölümünde hello server.js başında ve hello satırını içeren değiştirme **SIO require('.. = //.. lib//Socket.io')** çok**SIO require('socket.io') =** aşağıda gösterildiği gibi:
   
       var express = require('express')
         , stylus = require('stylus')
         , nib = require('nib')
       //, sio = require('..//..//lib//socket.io'); //Original
         , sio = require('socket.io');                //Updated
         var port = process.env.PORT || 3000;         //Updated
3. Merhaba doğru bağlantı noktası üzerinde dinleyen tooensure hello uygulama, Not Defteri veya tercih ettiğiniz Düzenleyicisi server.js açın ve ardından değiştirerek aşağıdaki satırı değiştirin **3000** ile **process.env.port** gösterildiği gibi Aşağıda:
   
       //app.listen(3000, function () {            //Original
       app.listen(process.env.port, function () {  //Updated
         var addr = app.address();
         console.log('   app listening on http://' + addr.address + ':' + addr.port);
       });

Merhaba değişiklikleri çok kaydetme sonra**server.js**, gerekli modüllerini yüklemek için aşağıdaki adımları hello kullanın ve Azure öykünücüsünde hello uygulamayı test etme:

1. Kullanarak **Azure PowerShell**, dizinleri toohello değiştirme **C:\\düğümü\\chatapp\\WorkerRole1** komutu tooinstall hello aşağıdaki dizin ve kullanım hello Bu uygulama tarafından istenen modüller:
   
       PS C:\node\chatapp\WorkerRole1> npm install
   
   Bu hello package.json dosyasında listelenen hello modüllerini yükler. Merhaba komutu tamamlandığında, çıkış benzer toothe aşağıdaki görmeniz gerekir:
   
   ![Merhaba npm Hello çıktısını yükleme komutu][The-output-of-the-npm-install-command]
2. Bu örnekte, ilk olarak hello Socket.IO GitHub deposunu bir parçası olan ve doğrudan hello Socket.IO kitaplığı göreli yolu tarafından başvurulan olduğundan, biz komutu aşağıdaki hello vererek yüklemeniz gerekir böylece Socket.IO hello package.json dosyasında başvurulmadı:
   
       PS C:\node\chatapp\WorkerRole1> npm install socket.io --save

### <a name="test-and-deploy"></a>Test etme ve dağıtma
1. Merhaba öykünücüsü komutu aşağıdaki hello vererek başlatın:
   
       PS C:\node\chatapp\WorkerRole1> Start-AzureEmulator -Launch
   
   > [!NOTE]
   > Öykünücü, örneğin başlatma sorunlar karşılaşırsanız.: Başlangıç AzureEmulator: beklenmeyen bir hata oluştu.  Ayrıntılar: Karşılaştı hello Faulted durumunda olduğundan System.ServiceModel.Channels.ServiceChannel, bir beklenmeyen bir hata hello iletişim nesnesi iletişimi için kullanılamaz.
   
      AzureAuthoringTools v 2.7.1 ve AzureComputeEmulator v 2.7 yeniden - o eşleştiğinden emin olun.
   >
   >


2. Bir tarayıcı açın ve çok gidin**http://127.0.0.1**.
3. Merhaba tarayıcı penceresi açıldığında, takma ad girin ve ardından ENTER tuşuna basın.
   Bu, toopost iletileri belirli bir takma olanak tanır. tootest çok kullanıcı işlevselliği, aynı URL'yi kullanarak ek tarayıcı pencerelerini açın ve farklı takma adlar girin.
   
   ![İki tarayıcı pencerelerini Kullanıcı1 ve kullanıcı2 sohbet iletileri görüntüleme](./media/cloud-services-nodejs-chat-app-socketio/socketio-8.png)
4. Sınama hello uygulamadan sonra aşağıdaki komutu gönderdikten hello öykünücüsü durdurun:
   
       PS C:\node\chatapp\WorkerRole1> Stop-AzureEmulator
5. toodeploy hello uygulama tooAzure, kullanım **Publish-AzureServiceProject** cmdlet'i. Örneğin:
   
       PS C:\node\chatapp\WorkerRole1> Publish-AzureServiceProject -ServiceName mychatapp -Location "East US" -Launch
   
   > [!IMPORTANT]
   > Emin toouse benzersiz bir ad olmalıdır, aksi takdirde hello yayımlama işlemi başarısız olur. Merhaba dağıtım tamamlandıktan sonra hello tarayıcısı açın ve dağıtılmış toohello hizmet gidin.
   > 
   > Abonelik adı içeri hello yok Bu hello sağlanan belirten bir hata alırsanız, yayımlama profili, indirin ve tooAzure dağıtmadan önce aboneliğinizin hello yayımlama profilini içeri aktarma. Merhaba bkz **hello uygulama tooAzure dağıtma** bölümünü [derleme ve bir Node.js uygulaması tooan Azure bulut hizmeti dağıtma](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)
   > 
   > 
   
   ![Azure üzerinde barındırılan hello hizmet gösteren bir tarayıcı penceresi][completed-app]
   
   > [!NOTE]
   > Abonelik adı içeri hello yok Bu hello sağlanan belirten bir hata alırsanız, yayımlama profili, indirin ve tooAzure dağıtmadan önce aboneliğinizin hello yayımlama profilini içeri aktarma. Merhaba bkz **hello uygulama tooAzure dağıtma** bölümünü [derleme ve bir Node.js uygulaması tooan Azure bulut hizmeti dağıtma](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)
   > 
   > 

Uygulamanız artık Azure üzerinde çalışan ve Sohbet iletilerini Socket.IO kullanarak farklı istemciler arasında geçiş.

> [!NOTE]
> Kolaylık olması için bu kullanıcıları bağlı toohello arasında sınırlı toochatting örnektir aynı örneği. Bu iki çalışan rolü örnekleri hello bulut hizmeti oluşturur, kullanıcılar yalnızca mümkün olacaktır başkalarıyla toochat bağlı toohello aynı çalışan rolü örneği. tooscale hello uygulama toowork birden fazla rol örneği ile Service Bus tooshare hello Socket.IO deposu durumu gibi bir teknoloji örneklerinde kullanabilirsiniz. Merhaba hello Service Bus kuyrukları ve konularından kullanım örnekleri örnekler için bkz [Node.js GitHub deposunu için Azure SDK](https://github.com/WindowsAzure/azure-sdk-for-node).
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
Bu öğreticide nasıl toocreate bir temel sohbet uygulaması bir Azure bulut hizmetinde barındırılan öğrendiniz. toolearn nasıl toohost bu uygulamayı bir Azure Web sitesinde bkz [bir Azure Web sitesinde Socket.IO ile bir Node.js sohbet uygulaması derleme][chatwebsite].

Daha fazla bilgi için hello Ayrıca bkz. [Node.js Geliştirici Merkezi](/develop/nodejs/).

[chatwebsite]: /develop/nodejs/tutorials/website-using-socketio/

[Azure SLA]: http://www.windowsazure.com/support/sla/
[Azure SDK for Node.js GitHub repository]: https://github.com/WindowsAzure/azure-sdk-for-node
[completed-app]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-10.png
[Azure SDK for Node.js]: https://www.windowsazure.com/develop/nodejs/
[Node.js Web Application]: https://www.windowsazure.com/develop/nodejs/tutorials/getting-started/
[Socket.IO GitHub deposunu]: https://github.com/LearnBoost/socket.io/tree/0.9.14
[Azure Considerations]: #windowsazureconsiderations
[Hosting hello Chat Example in a Worker Role]: #hostingthechatexampleinawebrole
[Summary and Next Steps]: #summary
[powershell-menu]: ./media/cloud-services-nodejs-chat-app-socketio/azure-powershell-start.png

[chat example]: https://github.com/LearnBoost/socket.io/tree/master/examples/chat
[chat-example-view]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-22.png


[chat-contents]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-5.png
[The-output-of-the-npm-install-command]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-7.png
[hello output of hello Publish-AzureService command]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-9.png


