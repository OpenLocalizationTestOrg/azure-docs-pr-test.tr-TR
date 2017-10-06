---
title: "aaaCreate Azure App Service'te Socket.IO ile bir Node.js sohbet uygulaması"
description: "Öğretici, Azure üzerinde barındırılan bir node.js web uygulamasında Socket.IO kullanmayı gösterir."
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: c4c4af36-3ecf-4619-b586-ca90d53ce35b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 3bd7867ccc297dc0a21c7a00cc9db06358877f5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-nodejs-chat-application-with-socketio-in-azure-app-service"></a>Azure App Service’te Socket.IO ile bir Node.js sohbet uygulaması oluşturma
Socket.IO WebSockets kullanan istemciler ve node.js sunucu arasında gerçek zamanlı iletişim sağlar. Eski tarayıcıyla iş geri dönüş tooother taşımaları (örneğin, uzun yoklama) da destekler. Bu öğretici bir temel Socket.IO sohbet uygulaması Azure web uygulaması olarak barındırma aracılığıyla yol ve nasıl tooscale hello kullanarak uygulama Göster [Azure Redis önbelleği]. Socket.IO ile ilgili daha fazla bilgi için bkz: <http://socket.io/>.

> [!NOTE]
> Bu görevde Hello yordamları uygulamak çok[App Service Web Apps]; bulut Hizmetleri için bkz: [bir Node.js sohbet uygulaması Socket.IO ile bir Azure bulut hizmeti oluşturma].
> 
> 

## <a name="download-hello-chat-example"></a>Merhaba sohbet örneği indirin
Bu proje için hello sohbet hello örnekten kullanacağız [Socket.IO GitHub deposunu]. Aşağıdaki adımları toodownload hello örneğine hello gerçekleştirmek ve daha önce oluşturduğunuz toohello proje ekleyin.

1. Karşıdan bir [ZIP veya GZ Arşivlenen Sürüm] hello Socket.IO projesinin (sürüm 1.3.5 için bu belgenin kullanıldı)
2. Merhaba Arşiv ve kopyalama hello ayıklamak **örnekler\\sohbet** dizin tooa yeni konumu. Örneğin,  **\\düğümü\\sohbet**.

## <a name="modify-appjs-and-install-modules"></a>App.js'yi değiştirme ve modülleri yükleme
1. Merhaba yeniden adlandırma **index.js** çok dosya**app.js**. Bu, Azure toodetect bir Node.js uygulaması budur sağlar.
2. Açık hello **app.js** dosyasını bir metin düzenleyicisinde. Değişiklik hello satırını içeren `var io = require('../..')(server);` aşağıda gösterildiği gibi:
   
       var express = require('express');
       var app = express();
       var server = require('http').createServer(app);
       // var io = require('../..')(server);
       // New:
       var io = require('socket.io')(server);
       var port = process.env.PORT || 3000;
3. Açık hello **package.json** dosyası ve bir başvuru toosocket.io altında ekleyin `dependencies`, aşağıda gösterildiği gibi:
   
        "dependencies": {
          "express": "3.4.8",
          "socket.io": "1.3.5"
        }
4. Komut satırı Hello toohello değiştirme  **\\düğümü\\sohbet** bu uygulama tarafından istenen dizin ve kullanım npm tooinstall hello modülleri:
   
        npm install
   
    Bu hello modülleri adlı bir alt klasöre yükler **node_modules**.

## <a name="create-an-azure-web-app"></a>Bir Azure Web uygulaması oluşturma
Bu adımları toocreate Azure web uygulaması izleyin, Git yayımlamayı etkinleştirmek ve hello web uygulaması WebSocket desteği etkinleştirin.

> [!NOTE]
> toocomplete Bu öğretici bir Azure hesabınızın olması gerekir. Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz. Ayrıntılı bilgi için bkz. <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A7171371E" target="_blank">Azure Ücretsiz Deneme Sürümü</a>.
> 
> 

1. Hello Azure komut satırı arabirimi (Azure CLI) yükleyin ve tooyour Azure aboneliğine bağlayın. Bkz: [hello Azure CLI yükleyip](../cli-install-nodejs.md).
2. İlk zaman ayarınız Azure deposunu varsa toocreate oturum açma kimlik bilgileri gerekir. Hello Azure CLI hello aşağıdaki komutu girin:
   
        azure site deployment user set [username] [password]
3. Değiştirme toohello  **\\node\chat** dizin ve kullanım hello aşağıdaki yeni bir Azure web uygulaması ve bir yerel Git deposu toocreate komutu. Bu komut ayrıca bir Git Uzak adlandırılmış 'azure' oluşturur.
   
        azure site create mysitename --git
   
    Web uygulamanız için benzersiz bir ad ile 'mysitename' değiştirmeniz gerekir.
4. Hello varolan dosyaları toohello yerel deposu, komutları aşağıdaki hello kullanarak kaydedin:
   
        git add .
        git commit -m "Initial commit"
5. Merhaba dosyaları toohello Azure Web Apps deposu komutu aşağıdaki hello ile gönderin:
   
        git push azure master
   
    İstendiğinde, adım 2 kimlik bilgilerinizi girin. Merhaba sunucuda modülleri içeri aktarılmış olarak durum iletilerini alacaktır. Bu işlem tamamlandıktan sonra Merhaba uygulaması Azure web uygulamanızın üzerinde barındırılan.
   
   > [!NOTE]
   > Modülü yükleme sırasında hatalarla karşılaşabilirsiniz, ' hello... alınan proje bulunamadı '. Bunlar güvenle yoksayılabilir.
   > 
   > 
6. Azure üzerinde varsayılan olarak etkinleştirilmez WebSockets Socket.IO kullanır. tooenable web yuvalarını hello aşağıdaki komutu kullanın:
   
        azure site set -w
   
    İstenirse, hello hello web uygulaması adını girin.
   
   > [!NOTE]
   > 'azure sitesine -w set' komutu yalnızca sürümüyle 0.7.4 iş ya da üst hello Azure komut satırı arabirimi sürümünü hello. Hello kullanarak WebSocket desteği de etkinleştirebilirsiniz [Azure Portal](https://portal.azure.com).
   > 
   > WebSockets tooenable kullanarak Azure Portal Merhaba, hello Web uygulamaları dikey hello web uygulamasından tıklatın, **tüm ayarları** > **uygulama ayarları**. Altında **Web yuvalarını**, tıklatın **üzerinde**. Daha sonra **Kaydet**'e tıklayın.
   > 
   > 
7. Azure, kullanım hello aşağıdaki tooview hello web uygulamasında toolaunch web tarayıcınız komut ve toohello barındırılan web uygulamasına gidin:
   
        azure site browse

Uygulamanız artık Azure üzerinde çalışan ve Sohbet iletilerini Socket.IO kullanarak farklı istemciler arasında geçiş.

## <a name="scale-out"></a>Ölçeği genişletme
Socket.IO uygulamalar ölçeklendirilmiş çıkışı kullanarak bir **bağdaştırıcısı** toodistribute iletileri ve birden çok uygulama örnekleri arasında olaylar. Kullanılabilir birkaç bağdaştırıcısı varken hello [Socket.IO redis] bağdaştırıcısı hello Azure Redis önbelleği özelliğiyle kolayca da kullanılabilir.

> [!NOTE]
> Yapışkan oturumları desteği Socket.IO çözüm ölçeklendirmeye yönelik ek bir gereksinimdir. Yapışkan oturumları, Azure isteği Yönlendirme aracılığıyla Azure Web uygulamaları için varsayılan olarak etkinleştirilir. Daha fazla bilgi için bkz: [örneğine benzeşimi, Azure Web siteleri].
> 
> 

### <a name="create-a-redis-cache"></a>Redis önbelleği oluşturma
Merhaba adımlarını gerçekleştirin [Azure Redis Önbelleği'nde bir önbellek oluşturma] toocreate yeni bir önbellek.

> [!NOTE]
> Merhaba Kaydet **ana bilgisayar adı** ve **birincil anahtar** bunlar içinde gerekli şekilde önbelleğiniz için sonraki adımlar hello.
> 
> 

### <a name="add-hello-redis-and-socketio-redis-modules"></a>Merhaba redis ve Socket.IO redis modülleri ekleme
1. Bir komut satırından, toohello değiştirmek  **\\düğümü\\sohbet** komutu aşağıdaki dizin ve kullanım hello.
   
        npm install socket.io-redis@0.1.4 redis@0.12.1 --save
   
   > [!NOTE]
   > Bu komutta belirtilen hello sürümleri, bu makalede test edilirken kullanılan hello sürümleridir.
   > 
   > 
2. Merhaba değiştirme **app.js** dosya tooadd hello aşağıdaki satırları hemen sonra`var io = require('socket.io')(server);`
   
        var pub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
        var sub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
   
        var redis = require('socket.io-redis');
        io.adapter(redis({pubClient: pub, subClient: sub}));
   
    Değiştir **redishostname** ve **rediskey** hello ana bilgisayar adı ve Redis önbelleği için anahtar.
   
    Bu bir yayımlama oluşturun ve istemci toohello daha önce oluşturduğunuz Redis önbelleği abone olun. Merhaba istemciler daha sonra hello bağdaştırıcısı tooconfigure Socket.IO toouse hello Redis önbelleği iletileri ve olayları, uygulamanızın örnekleri arasında geçirmek için kullanılır
   
   > [!NOTE]
   > Merhaba sırasında **Socket.IO redis** bağdaştırıcısı doğrudan tooRedis iletişim, hello geçerli sürümü hello kimlik doğrulaması Azure Redis önbelleği tarafından gerekli desteklemez. Merhaba ilk bağlantı hello kullanılarak oluşturulan şekilde **redis** modülü, ardından hello istemci toohello geçirilir **Socket.IO redis** bağdaştırıcısı.
   > 
   > Azure Redis önbelleği bağlantı noktası 6380 kullanarak güvenli bağlantı desteklerken, bu örnekte kullanılan hello modülleri 14/7/2014 sürümünden itibaren güvenli bağlantılarını desteklemez. kod yukarıda Hello hello varsayılan, 6379 güvenli olmayan bağlantı noktasını kullanır.
   > 
   > 
3. Değiştirilen Kaydet hello **app.js**

### <a name="commit-changes-and-redeploy"></a>Değişiklikleri Kaydet ve yeniden dağıtın
Merhaba hello komut satırı gelen  **\\düğümü\\sohbet** dizin, aşağıdaki komutları toocommit değişiklikler hello kullanın ve hello uygulama yeniden dağıtın.

    git add .
    git commit -m "implementing scale out"
    git push azure master

Merhaba değişiklikleri toohello sunucu gönderildikten sonra komutu aşağıdaki hello kullanarak siteniz arasında birden çok örneği ölçeklendirebilirsiniz.

    azure site scale instances --instances #

Burada  **#**  örnekleri toocreate hello sayısıdır.

Doğru tooall istemcileri gönderilen iletileri birden çok tarayıcılar veya bilgisayarlar tooverify tooyour web uygulaması bağlanabilir.

## <a name="troubleshooting"></a>Sorun giderme
### <a name="connection-limits"></a>Bağlantı sınırları
Azure Web Apps hello kaynakları kullanılabilir tooyour site belirleyen birden çok SKU içinde kullanılabilir. Bu, izin verilen WebSocket bağlantı hello sayısını içerir. Daha fazla bilgi için bkz: Merhaba [Web Apps Fiyatlandırma sayfasında].

### <a name="messages-arent-being-sent-using-websockets"></a>WebSockets kullanarak iletilerinin gönderilme değil
İstemci tarayıcıları WebSockets kullanmak yerine yoklama toolong geri dönmeden tutmak, hello aşağıdakilerden biri nedeniyle olabilir.

* **Merhaba aktarım toojust WebSockets görüntülemeyi deneyin**
  
    Socket.IO toouse WebSockets aktarım Mesajlaşma hello olarak hello sunucu ve istemci WebSockets'a desteklemesi gerekir. Bir ya da diğer hello yoksa, Socket.IO uzun yoklama gibi başka bir aktarım anlaşmaları. taşımalar Socket.IO tarafından kullanılan varsayılan listesi Hello ` websocket, htmlfile, xhr-polling, jsonp-polling`. Tooonly kullanım WebSockets kod toohello aşağıdaki hello ekleyerek zorlayabilirsiniz **app.js** hello satırını içeren sonra dosya `, nicknames = {};`.
  
        io.configure(function() {
          io.set('transports', ['websocket']);
        });
  
  > [!NOTE]
  > Yalnızca iletişimi tooWebSockets sınırlar gibi hello kodu yukarıdaki, etkinken WebSockets desteklemeyen eski tarayıcılar mümkün tooconnect toohello site olmayacağını unutmayın.
  > 
  > 
* **SSL kullan**
  
    WebSockets dayanır bazı küçük kullanılan HTTP üst bilgileri, hello gibi **yükseltme** üstbilgi. Web proxy gibi bazı ara ağ aygıtlarını bu üstbilgileri kaldırabilirsiniz. tooavoid Bu sorun, SSL üzerinden hello WebSocket bağlantısı kurabilirsiniz.
  
    Kolay bir yolu tooaccomplish tooconfigure Socket.IO çok budur`match origin protocol`. HTTP/HTTPS kaynaklanan hello aynı hello web sayfası için istek Socket.IO toosecure WebSockets iletişim hello bildirir. Bir tarayıcı Web sitenizi bir HTTPS URL'si toovisit kullanıyorsa, sonraki WebSocket iletişimleri Socket.IO ile SSL üzerinden güvenli.
  
    toomodify Bu örnek tooenable bu yapılandırma, kod toohello aşağıdaki hello eklemek **app.js** hello satırını içeren sonra dosyayı `, nicknames = {};`.
  
        io.configure(function() {
          io.set('match origin protocol', true);
        });
* **Web.config ayarlarını doğrulayın**
  
    Node.js uygulamaları barındırmak azure web uygulamaları kullanın hello **web.config** dosya tooroute gelen istekleri toohello Node.js uygulaması. Node.js uygulamaları ile düzgün şekilde WebSockets toofunction için hello **web.config** girişi aşağıdaki hello içermesi gerekir.
  
        <webSocket enabled="false"/>
  
    Bu, kendi uygulaması WebSockets ve Node.js belirli WebSocket modüllerini Socket.IO gibi çakışıyor içerir hello IIS WebSockets modülü devre dışı bırakır. Bu satırı mevcut değil veya çok ayarlamak`true`, bu, uygulamanız için hello WebSocket taşıma çalışmıyor hello neden olabilir.
  
    Normalde, Node.js uygulamalarını içermeyen bir **web.config** dosya şekilde dağıtıldığında, bunlar Azure Web siteleri otomatik olarak Node.js uygulamaları için bir tane oluşturur. Bu dosya hello sunucuda otomatik olarak oluşturulan olduğundan, bu dosya için Web sitesi tooview hello FTP veya FTPS URL kullanmanız gerekir. Merhaba FTP ve FTPS URL'leri siteniz için hello Klasik portalında web uygulamanızı seçerek bulabilir ve ardından hello **Pano** bağlantı. Merhaba URL'leri hello görüntülenen **Hızlı Bakış** bölümü.
  
  > [!NOTE]
  > Merhaba **web.config** uygulamanız bir sağlamıyorsa dosya Azure Web siteleri tarafından yalnızca oluşturulamaz. Sağlarsanız bir **web.config** dosya uygulama projenizin hello kök bunu Azure Web uygulamaları tarafından kullanılır.
  > 
  > 
  
    Merhaba girişi mevcut değil veya tooa değerinin ayarlanması, `true`, oluşturup bir **web.config** Merhaba, Node.js uygulamanızın kök ve değerini belirtin `false`.  Başvuru için aşağıdaki hello bir varsayılandır **web.config** kullanan bir uygulama için **app.js** hello giriş noktası olarak.
  
        <?xml version="1.0" encoding="utf-8"?>
        <!--
             This configuration file is required if iisnode is used toorun node processes behind
             IIS or IIS Express.  For more information, visit:
  
             https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config
        -->
  
        <configuration>
          <system.webServer>
            <!-- Visit http://blogs.msdn.com/b/windowsazure/archive/2013/11/14/introduction-to-websockets-on-windows-azure-web-sites.aspx for more information on WebSocket support -->
            <webSocket enabled="false" />
            <handlers>
              <!-- Indicates that hello server.js file is a node.js web app toobe handled by hello iisnode module -->
              <add name="iisnode" path="app.js" verb="*" modules="iisnode"/>
            </handlers>
            <rewrite>
              <rules>
                <!-- Do not interfere with requests for node-inspector debugging -->
                <rule name="NodeInspector" patternSyntax="ECMAScript" stopProcessing="true">
                  <match url="^app.js\/debug[\/]?" />
                </rule>
  
                <!-- First we consider whether hello incoming URL matches a physical file in hello /public folder -->
                <rule name="StaticContent">
                  <action type="Rewrite" url="public{REQUEST_URI}"/>
                </rule>
  
                <!-- All other URLs are mapped toohello node.js web app entry point -->
                <rule name="DynamicContent">
                  <conditions>
                    <add input="{REQUEST_FILENAME}" matchType="IsFile" negate="True"/>
                  </conditions>
                  <action type="Rewrite" url="app.js"/>
                </rule>
              </rules>
            </rewrite>
            <!--
              You can control how Node is hosted within IIS using hello following options:
                * watchedFiles: semi-colon separated list of files that will be watched for changes toorestart hello server
                * node_env: will be propagated toonode as NODE_ENV environment variable
                * debuggingEnabled - controls whether hello built-in debugger is enabled
  
              See https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config for a full list of options
            -->
            <!--<iisnode watchedFiles="web.config;*.js"/>-->
          </system.webServer>
        </configuration>
  
    Uygulamanız bir giriş noktası dışındaki kullanıyorsa **app.js**, tüm oluşumlarını değiştirmelisiniz **app.js** giriş noktası ile Merhaba düzeltin. Örneğin, değiştirme **app.js** ile **server.js**.

> [!NOTE]
> Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin], burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz. Kredi kartı ve taahhüt gerekmez.
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
Bu öğreticide nasıl toocreate bir Azure web uygulamasında bir sohbet uygulaması barındırılan öğrendiniz. Bu uygulamayı bir Azure bulut hizmeti olarak da barındırabilir. Adımları için tooaccomplish buna ek olarak, bkz: [bir Node.js sohbet uygulaması Socket.IO ile bir Azure bulut hizmeti oluşturma].

Daha fazla bilgi için hello Ayrıca bkz. [Node.js Geliştirici Merkezi].

## <a name="whats-changed"></a>Yapılan değişiklikler
* Web siteleri tooApp hizmet değişikliği Kılavuzu toohello için bkz: [Azure App Service ve mevcut Azure hizmetlerine etkileri].

<!-- URL List -->

[Azure Redis önbelleği]: /documentation/services/redis-cache/
[App Service Web Apps]: http://go.microsoft.com/fwlink/?LinkId=529714
[Web Apps Fiyatlandırma sayfasında]: http://go.microsoft.com/fwlink/?LinkId=511643
[bir Node.js sohbet uygulaması Socket.IO ile bir Azure bulut hizmeti oluşturma]: ../cloud-services/cloud-services-nodejs-chat-app-socketio.md
[Install and Configure hello Azure CLI]: ../cli-install-nodejs.md
[Azure App Service ve mevcut Azure hizmetlerine etkileri]: http://go.microsoft.com/fwlink/?LinkId=529714
[Node.js Geliştirici Merkezi]: /develop/nodejs/
[App Service'i deneyin]: https://azure.microsoft.com/try/app-service/
[örneğine benzeşimi, Azure Web siteleri]: https://azure.microsoft.com/blog/2013/11/18/disabling-arrs-instance-affinity-in-windows-azure-web-sites/
[Azure Redis Önbelleği'nde bir önbellek oluşturma]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md

[Socket.IO redis]: https://github.com/socketio/socket.io-redis
[Socket.IO GitHub deposunu]: https://github.com/socketio/socket.io
[ZIP veya GZ Arşivlenen Sürüm]: https://github.com/socketio/socket.io/releases

<!-- IMG List -->

[chat-example-view]: ./media/web-sites-nodejs-chat-app-socketio/socketio-2.png
[npm-output]: ./media/web-sites-nodejs-chat-app-socketio/socketio-7.png
[completed-app]: ./media/web-sites-nodejs-chat-app-socketio/websitesocketcomplete.png
