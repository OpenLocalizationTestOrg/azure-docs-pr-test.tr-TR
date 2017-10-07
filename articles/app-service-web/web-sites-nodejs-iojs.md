---
title: Azure App Service Web Apps ile aaaHow toouse io.js
description: "Bilgi nasıl toouse io.js ile Azure App Service'te bir web uygulaması."
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: d6320725-ffcb-4ad7-ba63-fc72fa2f2808
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 5dfdac37546b36bc91ab43d9e0a39c2126b4fa9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-iojs-with-azure-app-service-web-apps"></a>Nasıl Azure App Service Web Apps ile io.js toouse
Merhaba popüler düğümü çatalı [io.js] daha açık bir idare modeli, daha hızlı bir yayın döngüsü ve yeni ve Deneysel JavaScript özellikleri daha hızlı benimsenmesi dahil olmak üzere çeşitli farklar tooJoyent'ın Node.js proje özellikleri.

Sırada [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web uygulamaları birçok Node.js sürümleri önceden yüklenmiş olan, aynı zamanda için bir kullanıcı tarafından sağlanan Node.js ikili sağlar. App Service Web Apps üzerinde io.js hello kullanımını etkinleştirme iki yöntem bu makalede ele: hello Azure toouse hello en son kullanılabilir io.js sürümünü otomatik olarak yapılandırır ve genişletilmiş dağıtım betiğini de kullanımı gibi hello io.js ikili el ile karşıya yükleme. 

<a id="deploymentscript"></a>

## <a name="using-a-deployment-script"></a>Bir dağıtım komut dosyası kullanma
Bir Node.js uygulaması dağıtımı sırasında App Service Web Apps ortamı hello tooensure'nın düzgün yapılandırıldığından küçük komutlarının sayısı çalışır. Bir dağıtım komut dosyası kullanarak, bu işlem özelleştirilmiş tooinclude hello indirme ve io.js yapılandırması olabilir.

Merhaba [io.js dağıtım betiği](https://github.com/felixrieseberg/iojs-azure) Github'da kullanılabilir. web uygulamanızdan tooenable io.js sadece kopyalayın **.deployment**, **deploy.cmd** ve **IISNode.yml** toohello kök uygulama klasörünüzün tooWeb uygulamalar ve dağıtın.  

Merhaba ilk dosya **.deployment**, Web uygulamaları toorun bildirir **deploy.cmd** dağıtım bağlıdır. Bu komut dosyasını bir Node.js uygulaması için tüm hello normal adımları çalışır, ancak ayrıca hello io.js en son sürümünü yükler. Son olarak, **IISNode.yml** Web Apps toouse indirilen yalnızca hello io.js önceden yüklenmiş bir Node.js ikili yerine ikili yapılandırır.

> [!NOTE]
> io.js ikili tooupdate hello kullanılan, yalnızca uygulamanız dağıtmanız - hello betik her tek seferde hello uygulamanın dağıtıldığını io.js yeni sürümü indirir.
> 
> 

<a id="manualinstallation"></a>

## <a name="using-manual-installation"></a>El ile yükleme kullanma
Merhaba el ile yüklemesi özel io.js sürümü, yalnızca iki adımı içerir. İlk olarak, hello karşıdan **win x64** hello doğrudan ikili [io.js dağıtım]. Gerekli olan iki dosyalar - **iojs.exe** ve **iojs.lib**. Kaydet hem dosyaları, web uygulamanızın tooa klasöre örneğin **bin/iojs**.

tooconfigure Web Apps toouse **iojs.exe** oluşturmak yerine önceden yüklenmiş bir düğüm sürüm, bir **IISNode.yml** dosya hello uygulamanızı kökünde ve satır aşağıdaki hello ekleyin.

    nodeProcessCommandLine: "D:\home\site\wwwroot\bin\iojs\iojs.exe"

<a id="nextsteps"></a>

## <a name="next-steps"></a>Sonraki Adımlar
Bu makalede nasıl el ile yükleme yanı sıra dağıtım betikleri toouse io.js her ikisini de kullanarak App Service Web Apps ile sağlanan öğrendiniz. 

> [!NOTE]
> io.js ağır Geliştiriliyor ve Node.js daha sık güncelleştirilir. Node.js modüllerini sayısı ile io.js - Lütfen belgelere bakın işe yaramayabilir [github'da io.js] sorun giderme.
> 
> 

## <a name="whats-changed"></a>Yapılan değişiklikler
* Web siteleri tooApp hizmet değişikliği Kılavuzu toohello için bkz: [Azure App Service ve mevcut Azure hizmetlerine etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)

> [!NOTE]
> Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz. Kredi kartı ve taahhüt gerekmez.
> 
> 

[io.js]: https://iojs.org
[io.js dağıtım]: https://iojs.org/dist/
[github'da io.js]: https://github.com/iojs/io.js
[io.js Deployment Script]: https://github.com/felixrieseberg/iojs-azure
