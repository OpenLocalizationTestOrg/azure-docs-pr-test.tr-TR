---
title: aaaWeb Express (Node.js) ile uygulama | Microsoft Docs
description: "Merhaba bulut hizmeti öğretici oluşturur ve nasıl toouse hello Express modülü gösteren bir öğretici."
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 24f8e7ef-e90d-4554-9b1e-a9b31d5824e5
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 91921bfbe137eeca9a110d4cb18eb57b46b0060e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-web-application-using-express-on-an-azure-cloud-service"></a>Bir Azure bulut hizmeti Express kullanarak bir Node.js web uygulaması oluşturma
Node.js hello çekirdek çalışma zamanı en az bir işlev kümesi içerir.
Geliştiriciler genellikle bir Node.js uygulaması geliştirilirken 3 taraf modülleri tooprovide ek işlevini kullanın. Bu öğreticide hello kullanarak yeni bir uygulama oluşturacaksınız [Express] [ Express] modül Node.js web uygulamaları oluşturmak için bir MVC çerçevesi sağlar.

Tamamlanan hello uygulamasının ekran görüntüsü aşağıda verilmiştir:

![Hoş Geldiniz tooExpress Azure'da gösteren bir web tarayıcısı](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="create-a-cloud-service-project"></a>Bir bulut hizmeti projesi oluşturma
[!INCLUDE [install-dev-tools](../../includes/install-dev-tools.md)]

Hello aşağıdaki gerçekleştirme adımları toocreate yeni bir bulut hizmeti projesi 'expressapp' adlı:

1. Merhaba gelen **Başlat menüsü** veya **Başlat ekranında**, arama **Windows PowerShell**. Son olarak, sağ **Windows PowerShell** seçip **yönetici olarak çalıştır**.
   
    ![Azure PowerShell simgesi](./media/cloud-services-nodejs-develop-deploy-express-app/azure-powershell-start.png)
2. Değiştirme dizinleri toohello **c:\\düğümü** dizin ve aşağıdaki komutları toocreate adlı yeni bir çözüm hello enter **expressapp** ve adında bir web rolü **WebRole1** :
   
        PS C:\node> New-AzureServiceProject expressapp
        PS C:\Node\expressapp> Add-AzureNodeWebRole
        PS C:\Node\expressapp> Set-AzureServiceProjectRole WebRole1 Node 0.10.21
   
    > [!NOTE]
    > Varsayılan olarak, **Add-AzureNodeWebRole** Node.js daha eski bir sürümü kullanır. Merhaba **kümesi AzureServiceProjectRole** deyimi yukarıdaki Azure toouse v0.10.21 düğümünün bildirir.  Not hello parametreleri büyük/küçük harfe duyarlıdır.  Merhaba doğru Node.js sürümünü hello denetleyerek seçilmiş doğrulayabilirsiniz **motorları** özelliğinde **WebRole1\package.json**.
    > 
    > 

## <a name="install-express"></a>Hızlı yükleme
1. Merhaba hızlı Oluşturucu komutu aşağıdaki hello vererek yükleyin:
   
        PS C:\node\expressapp> npm install express-generator -g
   
    Merhaba hello npm komutunun çıkışını benzer toohello sonuç aşağıdaki gibi görünmelidir. 
   
    ![Windows PowerShell görüntüleme hello çıktısını hello npm express komutu yükleyin.](./media/cloud-services-nodejs-develop-deploy-express-app/express-g.png)
2. Değiştirme dizinleri toohello **WebRole1** dizin ve kullanım hello express komutu toogenerate yeni bir uygulama:
   
        PS C:\node\expressapp\WebRole1> express
   
    İstendiğinde toooverwrite önceki uygulamanızı olacaktır. Girin **y** veya **Evet** toocontinue. Hızlı Başlangıç app.js dosya ve uygulamanızı oluşturmak için bir klasör yapısı oluşturur.
   
    ![Merhaba hello express komutunun çıktısı](./media/cloud-services-nodejs-develop-deploy-express-app/node23.png)
3. Merhaba package.json dosyasında tanımlanan tooinstall ek bağımlılıklar hello aşağıdaki komutu girin:
   
       PS C:\node\expressapp\WebRole1> npm install
   
   ![Merhaba npm Hello çıktısını yükleme komutu](./media/cloud-services-nodejs-develop-deploy-express-app/node26.png)
4. Kullanım hello şu komutu toocopy hello **bin/www** çok dosya**server.js**. Merhaba bulut hizmeti, bu uygulama için hello giriş noktası bulabilmesi budur.
   
       PS C:\node\expressapp\WebRole1> copy bin/www server.js
   
   Bu komut tamamlandıktan sonra olmalıdır bir **server.js** hello WebRole1 dizindeki dosyayı.
5. Merhaba değiştirme **server.js** tooremove hello birini '.' hello satır aşağıdaki karakterler.
   
       var app = require('../app');
   
   Bu değişikliği yaptıktan sonra hello satırı aşağıdaki gibi görünmelidir.
   
       var app = require('./app');
   
   Biz hello dosya taşınmış olduğundan bu değişikliği gerekli değildir (önceki adıyla **bin/www**,) toohello gerektiği hello uygulama dosyası ile aynı dizinde. Bu değişikliği yaptıktan sonra hello Kaydet **server.js** dosya.
6. Komut toorun hello hello Azure öykünücüsü uygulamasında aşağıdaki hello kullan:
   
       PS C:\node\expressapp\WebRole1> Start-AzureEmulator -launch
   
    ![Hoş Geldiniz tooexpress içeren bir web sayfası.](./media/cloud-services-nodejs-develop-deploy-express-app/node28.png)

## <a name="modifying-hello-view"></a>Merhaba görünümü değiştirme
Şimdi "Hoş Geldiniz tooExpress Azure" Merhaba iletiyi hello görüntüle toodisplay değiştirin.

1. Aşağıdaki komut tooopen hello index.jade dosyasına hello girin:
   
       PS C:\node\expressapp\WebRole1> notepad views/index.jade
   
   ![Merhaba index.jade dosyasının içeriğini başlangıç.](./media/cloud-services-nodejs-develop-deploy-express-app/getting-started-19.png)
   
   Jade Express uygulamaları tarafından kullanılan hello varsayılan görünüm altyapısıdır. Merhaba Jade görünüm altyapısı hakkında daha fazla bilgi için bkz: [http://jade-lang.com][http://jade-lang.com].
2. Metnin son satırını Hello ekleyerek değiştirmek **azure'da**.
   
   ![Merhaba son satırında Hello index.jade dosyasını okur: p Hoş Geldiniz çok\#{title} Azure'da](./media/cloud-services-nodejs-develop-deploy-express-app/node31.png)
3. Merhaba dosyayı kaydedip Not Defteri'nden çıkın.
4. Tarayıcınızı yenileyin ve değişikliklerinizi görürsünüz.
   
   ![Bir tarayıcı penceresinde hello sayfası Azure Hoş Geldiniz tooExpress içerir.](./media/cloud-services-nodejs-develop-deploy-express-app/node32.png)

Sınama hello uygulamadan sonra hello kullan **Stop-AzureEmulator** cmdlet toostop hello öykünücüsü.

## <a name="publishing-hello-application-tooazure"></a>Yayımlama hello uygulama tooAzure
Hello Azure PowerShell penceresinde hello kullan **Publish-AzureServiceProject** cmdlet toodeploy hello uygulama tooa bulut hizmeti

    PS C:\node\expressapp\WebRole1> Publish-AzureServiceProject -ServiceName myexpressapp -Location "East US" -Launch

Merhaba dağıtım işlemi tamamlandıktan sonra tarayıcınızı açın ve hello web sayfasını görüntüleyin.

![Merhaba Express sayfasını gösteren bir web tarayıcısı. artık Azure üzerinde barındırılan Hello URL gösterir.](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla bilgi için bkz: Merhaba [Node.js Geliştirici Merkezi](/develop/nodejs/).

[Node.js Web Application]: http://www.windowsazure.com/develop/nodejs/tutorials/getting-started/
[Express]: http://expressjs.com/
[http://jade-lang.com]: http://jade-lang.com


