---
title: "aaaSpecifying Node.js sürümünü"
description: "Nasıl toospecify hello Azure Web siteleri ve bulut Hizmetleri tarafından kullanılan Node.js sürümünü öğrenin"
services: 
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: d0e15278-2ab4-4ec8-8256-913839c6d5ef
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 09c27bfc43c132b6d66f9a2943179e06ee75bedc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-a-nodejs-version-in-an-azure-application"></a>Bir Azure uygulamasında Node.js sürümünü belirtme
Bir Node.js uygulaması barındırdığında, uygulamanızın belirli bir Node.js sürümünü kullandığı tooensure isteyebilirsiniz. Vardır birkaç yolu tooaccomplish bu Azure üzerinde barındırılan uygulamalar için.

## <a name="default-versions"></a>Varsayılan sürümleri
Azure tarafından sağlanan hello Node.js sürümleri sürekli olarak güncelleştirilir. Aksi belirtilmediği sürece hello belirtilen varsayılan sürüm hello `WEBSITE_NODE_DEFAULT_VERSION` ortam değişkeni kullanılır. toooverride hello adımları bu makalenin aşağıdaki bölümlerde bu varsayılan değeri

> [!NOTE]
> Azure bulut hizmeti (web veya çalışan rolü) uygulamanızı barındırma ve ilk kez hello uygulama dağıtılan hello ise, Azure toouse deneyecek, geliştirme ortamınızı yüklediğiniz gibi aynı Node.js sürümünü Merhaba, Azure üzerinde kullanılabilir hello varsayılan sürümlerinden birini eşleşir.
>
>

## <a name="versioning-with-packagejson"></a>Package.json sürüm oluşturma
Node.js toobe tooyour aşağıdaki hello ekleyerek kullanılan hello sürümü belirtebilirsiniz **package.json** dosyası:

    "engines":{"node":version}

Burada *sürüm* hello belirli bir sürüm numarası toouse değil. Sürüm, daha karmaşık koşulları belirtebilirsiniz:

    "engines":{"node": "0.6.22 || 0.8.x"}

0.6.22 hello sürümlerinden barındırma ortamı hello kullanılabilir olmadığından, hello yüksek kullanılabilir serisi olacaktır hello 0,8 yerine - 0.8.4 kullanılan sürümü.

## <a name="versioning-websites-with-app-settings"></a>Uygulama ayarları ile Web siteleri sürüm oluşturma
Merhaba uygulamada bir Web sitesi barındırıyorsanız, hello ortam değişkeni ayarlayabilirsiniz **WEBSITE_NODE_DEFAULT_VERSION** toohello istediğiniz sürümü.

## <a name="versioning-cloud-services-with-powershell"></a>PowerShell ile sürüm bulut Hizmetleri
Bir bulut hizmeti hello uygulamada barındırma ve Azure PowerShell kullanarak hello uygulama dağıtıyorsanız, hello kullanarak hello varsayılan Node.js sürümünü kılabilirsiniz **kümesi AzureServiceProjectRole** PowerShell cmdlet'i. Örneğin:

    Set-AzureServiceProjectRole WebRole1 Node 0.8.4

Hello deyimi yukarıda Not hello parametreleri büyük/küçük harfe duyarlıdır.  Merhaba doğru Node.js sürümünü hello denetleyerek seçilmiş doğrulayabilirsiniz **motorları** , rolün özelliğinde **package.json**.

Merhaba de kullanabilirsiniz **Get-AzureServiceProjectRoleRuntime** tooretrieve bulut hizmet olarak barındırılan uygulamalar için kullanılabilir Node.js sürümlerinin bir listesi.  Her zaman bu listede projenizi bağlıdır Node.js hello sürümü olduğunu doğrulayın.

## <a name="using-a-custom-version-with-azure-websites"></a>Özel bir sürüm ile Azure Web siteleri kullanma
Azure Node.js birkaç varsayılan sürümü sağlarken toouse varsayılan olarak sağlanmayan bir sürümünü isteyebilirsiniz. Uygulamanız bir Azure Web sitesi olarak barındırılıyorsa, bunu hello kullanarak gerçekleştirebilirsiniz **iisnode.yml** dosya. Merhaba aşağıdaki adımlar bir Azure Web sitesi özel bir Node.Js sürümünü kullanarak hello işleminde size rehberlik:

1. Yeni bir dizin oluşturun ve ardından oluşturun bir **server.js** hello dizini içindeki dosya. Merhaba **server.js** dosya hello şunları içermelidir:

        var http = require('http');
        http.createServer(function(req,res) {
          res.writeHead(200, {'Content-Type': 'text/html'});
          res.end('Hello from Azure running node version: ' + process.version + '</br>');
        }).listen(process.env.PORT || 3000);

    Bu hello Web sitesine göz atarken kullanılan hello Node.js sürümünü görüntüler.
2. Yeni Web sitesi ve Not hello hello sitenin adını oluşturun. Örneğin, hello aşağıdaki hello kullanır [Azure komut satırı araçları] toocreate adlı yeni bir Azure Web **numaralı**ve ardından hello Web sitesi için Git deposu etkinleştirin.

        azure site create mywebsite --git
3. Adlı yeni bir dizin oluşturun **bin** hello içeren hello dizinin alt **server.js** dosya.
4. Merhaba belirli sürümünü indirin **node.exe** (Merhaba Windows sürümü) ile uygulamanızı toouse istiyor. Örneğin, kullanır hello **curl** toodownload sürüm 0.8.1:

        curl -O http://nodejs.org/dist/v0.8.1/node.exe

    Merhaba Kaydet **node.exe** hello dosyasına **bin** daha önce oluşturduğunuz klasör.
5. Oluşturma bir **iisnode.yml** hello aynı dosyayı hello olarak dizin **server.js** dosya ve ardından içerik toohello aşağıdaki hello ekleyin **iisnode.yml** dosyası:

        nodeProcessCommandLine: "D:\home\site\wwwroot\bin\node.exe"

    Bu yol hello burada olduğu **node.exe** , Azure Web uygulaması toohello yayımladıktan sonra proje dosyasında bulunan olacaktır.
6. Uygulamanızı yayımlayın. Örneğin, yeni bir Web sitesi hello--git parametresiyle önceki oluşturduğum olduğundan, hello aşağıdaki komutları hello uygulama dosyaları toomy yerel Git deposu ekleyin ve bunları toohello Web sitesi deposu gönderme:

        git add .
        git commit -m "testing node v0.8.1"
        git push azure master

    Merhaba uygulaması yayımladıktan sonra hello Web sitesini bir tarayıcıda açın. Belirten iletiyi görmelisiniz "Merhaba Azure çalışan düğümü sürümünden: v0.8.1".

## <a name="next-steps"></a>Sonraki Adımlar
Nasıl toospecify hello Node.js sürümü, uygulamanız tarafından kullanılan anladığınıza göre nasıl çok öğrenin[modüllerle çalışma], [bir Node.js Web sitenizi oluşturup dağıtacak](app-service-web/app-service-web-get-started-nodejs.md), ve [nasıl toouse hello Azure Mac ve Linux için komut satırı araçları].

Daha fazla bilgi için bkz: Merhaba [Node.js Geliştirici Merkezi](https://azure.microsoft.com/develop/nodejs/).

[nasıl toouse hello Azure Mac ve Linux için komut satırı araçları]:cli-install-nodejs.md
[Azure komut satırı araçları]:cli-install-nodejs.md
[modüllerle çalışma]: nodejs-use-node-modules-azure-apps.md
[build and deploy a Node.js Web Site]: app-service-web/app-service-web-get-started-nodejs.md
