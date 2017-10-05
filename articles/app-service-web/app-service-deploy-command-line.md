---
title: "Komut satırı araçları ile Azure uygulamanızı dağıtımını otomatik hale getirme | Microsoft Docs"
description: "Komut satırından Azure uygulamanızı nasıl dağıtılacağı hakkında daha fazla bilgi Bul"
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
ms.openlocfilehash: e0e2e65557911bcac06d4dc355f47e9331934f8a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="automate-deployment-of-your-azure-app-with-command-line-tools"></a>Komut satırı araçları ile Azure uygulamanızı dağıtımını otomatik hale getirme
Azure uygulamalarınızı komut satırı araçları ile dağıtımını otomatik hale getirebilirsiniz. Bu makalede, araçları ve dağıtım iş akışınızda kullanma Göster yararlı bağlantılar listelenmektedir. 

## <a name="msbuild"></a>MSBuild ile dağıtımı otomatik hale getir
Kullanırsanız [Visual Studio IDE](#vs) geliştirme için kullandığınız [MSBuild](http://msbuildbook.com/) IDE içinde yapabileceğiniz her şeyi otomatik hale getirmek için. MSBuild kullanın ya da yapılandırabilirsiniz [Web dağıtımı](#webdeploy) veya [FTP/FTPS](#ftp) kopyalamak için dosyaları. Web dağıtımı da veritabanları dağıtma gibi birçok diğer dağıtım görevlerini otomatik hale getirebilirsiniz.

MSBuild kullanarak komut satırı dağıtımı hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

* [Visual Studio kullanarak ASP.NET Web Dağıtımı: komut satırı dağıtım](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/command-line-deployment). Onuncu öğreticileri Visual Studio kullanarak Azure dağıtımı hakkında bir dizi. Visual Studio'da profilleri ayarlama yayımladıktan sonra dağıtmak için komut satırını kullanmayı gösterir.
* [Microsoft Build Engine içinde: MSBuild ve Team Foundation derlemesi kullanarak](http://msbuildbook.com/). Bölüm dağıtımı için MSBuild kullanma hakkında içerir Defterini Kopyala sabit.

## <a name="powershell"></a>Windows PowerShell ile dağıtımı otomatik hale getir
MSBuild veya FTP dağıtım işlevleri gerçekleştirebilirsiniz [Windows PowerShell](http://msdn.microsoft.com/library/dd835506.aspx). Bunu yaparsanız, Azure REST yönetim API çağrısı kolaylaştırmak Windows PowerShell cmdlet'leri koleksiyonu de kullanabilirsiniz.

Daha fazla bilgi için aşağıdaki kaynaklara bakın:

* [Bir GitHub deposuna bağlı bir web uygulaması dağıtma](app-service-web-arm-from-github-provision.md)
* [Bir SQL veritabanı ile bir web uygulaması sağla](app-service-web-arm-with-sql-database-provision.md)
* [Sağlama ve mikro beklendiği azure'da dağıtma](app-service-deploy-complex-application-predictably.md)
* [Azure ile-gerçek bulut uygulamaları derleme otomatikleştirmek her şeyi](http://asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything). Windows PowerShell komut dosyalarını e-kitap gösterilen örnek uygulamayı bir Azure test ortamı oluşturma ve dağıtma için nasıl kullandığını açıklar E-kitap bölüm. Bkz: [kaynakları](http://asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything#resources) bölümü ek Azure PowerShell belgelere bağlantıları için.
* [Geliştirme ve Test ortamları için yayımlamak için Windows PowerShell betiklerini kullanarak](../vs-azure-tools-publishing-using-powershell-scripts.md). Windows PowerShell kullanmak için dağıtım betiklerini nasıl Visual Studio oluşturur.

## <a name="api"></a>.NET Yönetim API'si ile dağıtımı otomatik hale getirme
Dağıtım için MSBuild veya FTP işlevleri gerçekleştirmek için C# kod yazabilirsiniz. Bunu yaparsanız, Azure yönetim sitesi yönetim işlevleri gerçekleştirmek için REST API erişebilirsiniz.

Daha fazla bilgi için aşağıdaki kaynağa bakın:

* [Her şeyi Azure yönetim kitaplıklarını ve .NET ile otomatikleştirme](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx). .NET Yönetim API'si ve daha fazla belgelere bağlantıları giriş.

## <a name="cli"></a>Azure'dan dağıtmak komut satırı arabirimi (Azure CLI)
FTP kullanarak dağıtmak için Windows, Mac veya Linux makinelerde komut satırını kullanabilirsiniz. Bunu yaparsanız, Azure REST yönetim API'si Azure CLI kullanarak da erişebilirsiniz.

Daha fazla bilgi için aşağıdaki kaynağa bakın:

* [Azure komut satırı araçları](https://azure.microsoft.com/downloads/). Komut satırı aracı bilgileri için portal sayfası Azure.com içinde.

## <a name="webdeploy"></a>Web dağıtımı komut satırından dağıtma
[Web dağıtımı](http://www.iis.net/downloads/microsoft/web-deploy) dağıtım Akıllı Dosya eşitleme yalnızca sağlayan IIS için Microsoft yazılım özellikleri, ancak aynı zamanda gerçekleştirebilir veya FTP kullandığınızda, otomatikleştirilemez birçok diğer dağıtım ile ilgili görevleri koordine değil. Örneğin, Web dağıtımı yeni bir veritabanı veya veritabanı güncelleştirmelerini web uygulamanızı birlikte dağıtabilirsiniz. Web dağıtımı da var olan bir site yalnızca değiştirilen dosyaların akıllıca kopyalayabilirsiniz beri güncelleştirmek için gereken süreyi en aza indirebilirsiniz. Microsoft Visual Studio ve Team Foundation Server için Web dağıtımı yerleşik destek vardır, ancak aynı zamanda Web dağıtımı doğrudan komut satırından dağıtım otomatikleştirmek için kullanabilirsiniz. Web dağıtımı komutları çok güçlü ancak öğrenme eğrisi hızı yüksek olabilir.

## <a name="more-resources"></a>Diğer kaynaklar
Komut satırı otomasyonu için başka bir dağıtım seçeneği bulut tabanlı bir hizmete gibi kullanmaktır [Octopus dağıtmak](http://en.wikipedia.org/wiki/Octopus_Deploy). Daha fazla bilgi için bkz: [dağıtmak ASP.NET uygulamaları için Azure Web siteleri](https://octopusdeploy.com/blog/deploy-aspnet-applications-to-azure-websites).

Komut satırı araçları hakkında daha fazla bilgi için aşağıdaki kaynağa bakın:

* [Basit Web Apps: Dağıtım](https://azure.microsoft.com/blog/2014/07/28/simple-azure-websites-deployment/). Web dağıtımı kullanabilmeniz kolaylaştırmak için şöyle yazıyor bir araç hakkında David Ebbo tarafından blogu.
* [Web dağıtım aracı](http://technet.microsoft.com/library/dd568996). Microsoft TechNet sitesindeki resmi belgeleri. Başlatmak için hala uygun bir yerdir tarihli.
* [Web dağıtmanızı](http://www.iis.net/learn/publish/using-web-deploy). Microsoft IIS.NET sitesindeki resmi belgeleri. Ayrıca başlatmak için iyi bir yerdir tarihli.
* [Visual Studio kullanarak ASP.NET Web Dağıtımı: komut satırı dağıtım](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/command-line-deployment). MSBuild Visual Studio tarafından kullanılan yapı altyapısıdır ve web uygulamalarını Web uygulamalarını dağıtmak için komut satırından da da kullanılabilir. Bu öğretici çoğunlukla Visual Studio dağıtımı hakkında serinin bir parçasıdır.

