---
title: "komut satırı araçları ile Azure uygulamanızı aaaAutomate dağıtımı | Microsoft Docs"
description: "Azure komut satırı hello uygulamanızdan nasıl dağıtılacağı hakkında daha fazla bilgi Bul"
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 8b65980c-eb75-44a2-8e0f-f9eb9e617d16
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2017
ms.author: cephalin
ms.openlocfilehash: 3df66cc4bf4e6819ed0eee7278ac79dca2e5daa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-deployment-of-your-azure-app-with-command-line-tools"></a>Komut satırı araçları ile Azure uygulamanızı dağıtımını otomatik hale getirme
Azure uygulamalarınızı komut satırı araçları ile dağıtımını otomatik hale getirebilirsiniz. Bu makalede kullanılabilen araçlar ve bunu nasıl yapacağınızı hello yararlı bağlantılar listelenmektedir toouse dağıtımı iş akışı bunları. 

## <a name="msbuild"></a>MSBuild ile dağıtımı otomatik hale getir
Merhaba kullanırsanız [Visual Studio IDE](#vs) geliştirme için kullandığınız [MSBuild](http://msbuildbook.com/) tooautomate herhangi bir şey IDE içinde yapabilir. MSBuild toouse ya da yapılandırabilirsiniz [Web dağıtımı](#webdeploy) veya [FTP/FTPS](#ftp) toocopy dosyaları. Web dağıtımı da veritabanları dağıtma gibi birçok diğer dağıtım görevlerini otomatik hale getirebilirsiniz.

MSBuild kullanarak komut satırı dağıtımı hakkında daha fazla bilgi için kaynakları aşağıdaki hello bakın:

* [Visual Studio kullanarak ASP.NET Web Dağıtımı: komut satırı dağıtım](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/command-line-deployment). Onuncu öğreticileri Visual Studio kullanarak dağıtım tooAzure hakkında bir dizi. Visual Studio'da yayımlama profillerini nasıl toouse hello komut satırı toodeploy ayarladıktan sonra gösterir.
* [İç hello Microsoft Build Engine: MSBuild kullanma ve Team Foundation Build](http://msbuildbook.com/). Bölüm nasıl içerir Defterini Kopyala sabit toouse MSBuild dağıtımı için.

## <a name="powershell"></a>Windows PowerShell ile dağıtımı otomatik hale getir
MSBuild veya FTP dağıtım işlevleri gerçekleştirebilirsiniz [Windows PowerShell](http://msdn.microsoft.com/library/dd835506.aspx). Bunu yaparsanız, hello Azure REST yönetim API kolay toocall olun Windows PowerShell cmdlet'leri koleksiyonu de kullanabilirsiniz.

Daha fazla bilgi için kaynakları aşağıdaki hello bakın:

* [Bir web bağlantılı uygulama tooa GitHub deposunu dağıtma](app-service-web-arm-from-github-provision.md)
* [Bir SQL veritabanı ile bir web uygulaması sağla](app-service-web-arm-with-sql-database-provision.md)
* [Sağlama ve mikro beklendiği azure'da dağıtma](app-service-deploy-complex-application-predictably.md)
* [Azure ile-gerçek bulut uygulamaları derleme otomatikleştirmek her şeyi](http://asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything). Windows PowerShell komut dosyaları toocreate Azure hello e-kitap gösterilen Merhaba örnek uygulaması nasıl kullandığı açıklanmıştır E-kitap bölüm test ortamı ve tooit dağıtın. Merhaba bkz [kaynakları](http://asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything#resources) Bağlantılar tooadditional Azure PowerShell belgeleri için bölüm.
* [Windows PowerShell betikleri tooPublish tooDev ve Test ortamları kullanarak](../vs-azure-tools-publishing-using-powershell-scripts.md). Nasıl, Visual Studio toouse Windows PowerShell dağıtım komut dosyası oluşturur.

## <a name="api"></a>.NET Yönetim API'si ile dağıtımı otomatik hale getirme
Tooperform MSBuild veya FTP işlevleri dağıtım için C# kod yazabilirsiniz. Bunu yaparsanız, hello Azure Yönetimi REST API tooperform site yönetim işlevleri erişebilirsiniz.

Daha fazla bilgi için kaynak aşağıdaki hello bakın:

* [Her şeyi hello Azure yönetim kitaplıklarını ve .NET ile otomatikleştirme](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx). Giriş toohello .NET Yönetim API'si ve bağlantıları toomore belgeleri.

## <a name="cli"></a>Azure'dan dağıtmak komut satırı arabirimi (Azure CLI)
FTP kullanarak, Windows, Mac veya Linux makineler toodeploy hello komut satırını kullanabilirsiniz. Bunu yaparsanız, hello Azure REST yönetim API'si hello Azure CLI kullanarak da erişebilirsiniz.

Daha fazla bilgi için kaynak aşağıdaki hello bakın:

* [Azure komut satırı araçları](https://azure.microsoft.com/downloads/). Komut satırı aracı bilgileri için portal sayfası Azure.com içinde.

## <a name="webdeploy"></a>Web dağıtımı komut satırından dağıtma
[Web dağıtımı](http://www.iis.net/downloads/microsoft/web-deploy) akıllı dosya yalnızca sağlayan dağıtım tooIIS eşitleme özellikleri ancak aynı zamanda gerçekleştirebilir veya FTP kullandığınızda, otomatikleştirilemez birçok diğer dağıtım ile ilgili görevleri koordine etmek için Microsoft yazılımdır. Örneğin, Web dağıtımı yeni bir veritabanı veya veritabanı güncelleştirmelerini web uygulamanızı birlikte dağıtabilirsiniz. Yalnızca değiştirilen dosyaların akıllıca kopyalayabilirsiniz beri web dağıtımı da hello gereken süre tooupdate var olan bir site en aza indirebilirsiniz. Microsoft Visual Studio ve Team Foundation Server için Web dağıtımı yerleşik destek vardır, ancak Ayrıca Web dağıtımı doğrudan hello komut satırı tooautomate dağıtımından kullanabilirsiniz. Web dağıtımı komutları çok güçlü ancak hello öğrenme eğrisi hızı yüksek olabilir.

## <a name="more-resources"></a>Diğer kaynaklar
Başka bir dağıtım seçeneği toocommand satır Otomasyon toouse bulut tabanlı hizmet olduğu gibi [Octopus dağıtmak](http://en.wikipedia.org/wiki/Octopus_Deploy). Daha fazla bilgi için bkz: [dağıtmak ASP.NET uygulamaları tooAzure Web siteleri](https://octopusdeploy.com/blog/deploy-aspnet-applications-to-azure-websites).

Komut satırı araçları hakkında daha fazla bilgi için kaynak aşağıdaki hello bakın:

* [Basit Web Apps: Dağıtım](https://azure.microsoft.com/blog/2014/07/28/simple-azure-websites-deployment/). Bir aracı hakkında David Ebbo tarafından blog şöyle yazıyor toomake bunu daha kolay toouse Web dağıtımı.
* [Web dağıtım aracı](http://technet.microsoft.com/library/dd568996). Merhaba Microsoft TechNet sitesindeki resmi belgeleri. Hala bir iyi toostart tarihli.
* [Web dağıtmanızı](http://www.iis.net/learn/publish/using-web-deploy). Merhaba Microsoft IIS.NET sitesindeki resmi belgeleri. Ayrıca iyi toostart tarihli.
* [Visual Studio kullanarak ASP.NET Web Dağıtımı: komut satırı dağıtım](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/command-line-deployment). MSBuild hello Visual Studio tarafından kullanılan altyapısının yapı ve ayrıca hello komut satırı toodeploy web uygulamaları tooWeb uygulamalar kullanılabilir olur. Bu öğretici çoğunlukla Visual Studio dağıtımı hakkında serinin bir parçasıdır.

