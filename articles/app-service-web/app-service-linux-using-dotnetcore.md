---
title: "Linux üzerinde Web uygulamasında .NET Core kullanın | Microsoft Docs"
description: ".NET Core Linux üzerinde Web uygulaması kullanın."
keywords: "Azure uygulama hizmeti, web uygulaması, dotnet, çekirdek, linux, oss"
services: app-service
documentationCenter: 
authors: michimune, rachelappel
manager: erikre
editor: 
ms.assetid: c02959e6-7220-496a-a417-9b2147638e2e
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: aelnably;wesmc;mikono;rachelap
ms.openlocfilehash: 9226dfb90e52ac2cae2cfc4af7c0705a93f56b44
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="use-net-core-in-an-azure-web-app-on-linux"></a>.NET Core Linux Azure web uygulaması kullanın #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

[Web uygulaması](https://docs.microsoft.com/azure/app-service-web/app-service-linux-intro) düzeyde ölçeklenebilir, otomatik olarak düzeltme eki uygulama web barındırma hizmeti Linux işletim sistemini kullanarak Linux'ta sağlar. Bu öğretici nasıl oluşturulacağını gösteren adım adım yönergeler içeren bir [.NET Core](https://docs.microsoft.com/aspnet/core/) Linux Azure web uygulaması üzerinde uygulama. 

![Linux üzerinde Web Uygulaması][10]

Mac, Windows veya Linux makinesi kullanarak aşağıdaki adımları izleyebilirsiniz.

## <a name="prerequisites"></a>Ön koşullar ##

Bu öğreticiyi tamamlamak için: 

* Yükleme [.NET Core SDK](https://www.microsoft.com/net/download/core).
* Yükleme [Git](https://git-scm.com/downloads).

[!INCLUDE [Free trial note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-local-net-core-application"></a>Yerel bir .NET Core uygulama oluşturma ##

Yeni bir terminal oturumu başlatın. Adlı bir dizin oluşturun `hellodotnetcore`ve geçerli dizini değiştirin. Ardından aşağıdaki komutu yazın: 

```
dotnet new web
``` 

  Bu komut dosyaları üç oluşturur (*hellodotnetcore.csproj*, *Program.cs*, ve *haline*) ve bir boş klasör (*wwwroot /*) Geçerli dizinin altında. İçeriği `.csproj` dosya, aşağıdaki gibi görünmelidir: 

```xml
  <!-- Empty lines are omitted. -->

  <Project Sdk="Microsoft.NET.Sdk.Web">
        <PropertyGroup>
        <TargetFramework>netcoreapp1.1</TargetFramework>
        </PropertyGroup>
        <ItemGroup>
        <Folder Include="wwwroot\" />
        </ItemGroup>
        <ItemGroup>
        <PackageReference Include="Microsoft.AspNetCore" Version="1.1.2" />
        </ItemGroup>
  </Project>
```

Bu uygulama bir web uygulaması olduğundan, bir ASP.NET Core paketine başvuru otomatik olarak eklenen *hellodotnetcore.csproj* dosya. Paketin sürüm numarası Seçilen framework göre ayarlanır. .NET Core 1.1 kullanılmakta olduğu için bu örnek ASP.NET Core sürüm 1.1.2 başvuruyor.

## <a name="build-and-test-the-application-locally"></a>Derleme ve uygulamayı yerel olarak test etme ##

Derleme ve .NET Core uygulamanızı çalıştırma `dotnet restore` ve ardından komut `dotnet run` aşağıda gösterildiği gibi komut:

```
dotnet restore
dotnet run
```


Uygulama başlatıldığında, uygulama bir bağlantı noktasında gelen istekleri dinlediği belirten bir ileti görüntüler. 

```bash
Hosting environment: Production
Content root path: C:\hellodotnetcore
Now listening on: http://localhost:5000
Application started. Press Ctrl+C to shut down.
```

Göz atarak test `http://localhost:5000/` tarayıcınızla. Her şeyi düzgün çalışır, "Hello World!" konusuna bakın Sonuç metin olarak.

![Tarayıcı ile test][7]

## <a name="create-a-net-core-app-in-the-azure-portal"></a>Bir .NET oluşturma Azure portalında çekirdek uygulama ##

Önce bir boş web uygulaması oluşturmanız gerekir. Oturum [Azure portal](https://portal.azure.com/) ve yeni bir [Linux üzerinde Web uygulaması](https://portal.azure.com/#create/Microsoft.AppSvcLinux).

![Bir web uygulaması oluşturma][1]

Zaman **oluşturma** sayfası açılır, web uygulamanız hakkında ayrıntılar verilmektedir:

![Bir .NET çekirdeği çalışma zamanı yığını seçme][2]

Doldurmak için bir kılavuz olarak aşağıdaki tabloyu kullanın **oluşturma** sayfasında sonra seçin **Tamam** ve **oluşturma** uygulama oluşturmak için.

| Ayar      | Önerilen değer  | Açıklama                                        |
| ------------ | ---------------- | -------------------------------------------------- |
| Uygulama adı | hellodotnetcore  | Uygulamanızın adı. Bu ad benzersiz olmalıdır. |
| Abonelik | Var olan bir abonelik seçin | Azure aboneliği. |
| Kaynak Grubu | myResourceGroup |  Web uygulaması içeren Azure kaynak grubu. |
| App Service Planı | Var olan uygulama hizmeti planı adı |  Uygulama hizmeti planı.  |
| Kapsayıcı yapılandırın | .NET core 1.1 | Bu web uygulaması için kapsayıcı türü: yerleşik, Docker veya özel kayıt defteri. |
| Görüntü kaynağı  | Yerleşik  |  Görüntünün kaynağı. |
| Çalışma zamanı yığını  | .NET core 1.1  | Çalışma zamanı yığını ve sürüm.  |

## <a name="deploy-your-application-via-git"></a>Git aracılığıyla uygulamanızı dağıtma ##

Azure App Service Web uygulaması Linux'ta .NET Core uygulamayı dağıtmak için Git kullanın.

Yeni Azure web uygulaması zaten yapılandırılmış Git dağıtımı içeriyor. Web uygulaması adı ekledikten sonra aşağıdaki URL'sine giderek Git dağıtım URL'si bulacaksınız:

```https://{your web app name}.scm.azurewebsites.net/api/scm/info```

Git URL'si, web uygulaması adınıza göre aşağıdaki biçime sahiptir:

```https://{your web app name}.scm.azurewebsites.net/{your web app name}.git```

Azure web uygulamanızı yerel uygulamayı dağıtmak için aşağıdaki komutları çalıştırın: 
 
```bash
git init
git remote add azure <Git deployment URL from above>
git add *.csproj *.cs
git commit -m "Initial deployment commit"
git push azure master
```

Altındaki tüm dosyaları anında gerekmez *bin /* veya *obj /* dizinleri uygulamanın kaynak dosyaları için Azure basıldığında uygulamanızı bulutta oluşturulduğundan. Derleme işlemi tamamlandıktan sonra ikili dosyaları uygulamanın dizininde içine kopyalanır */home/site/wwwroot/*.

Uzaktan dağıtım işlemlerini Başarı Raporu onaylayın. Gönderme işlemleri paket çözümleme itibaren sürebilir ve derleme bulutta çalışan işlemi olabilir. Olanları dosyaları kopyalandığını belirten dahil olmak üzere, birkaç durum iletilerini görürsünüz. Çıktı aşağıdakine benzer görünmelidir:

```bash
/* some output has been removed for brevity */
remote: Copying file: 'System.Net.Websockets.dll' 
remote: Copying file: 'System.Runtime.CompilerServices.Unsafe.dll' 
remote: Copying file: 'System.Runtime.Serialization.Primitives.dll' 
remote: Copying file: 'System.Text.Encodings.Web.dll' 
remote: Copying file: 'hellodotnetcore.deps.json' 
remote: Copying file: 'hellodotnetcore.dll' 
remote: Omitting next output lines...
remote: Finished successfully.
remote: Running post deployment commands...
remote: Deployment successful.
To https://hellodotnetcore.scm.azurewebsites.net/
 * [new branch]           master -> master

```

Dağıtım tamamlandıktan sonra web uygulamanızı etkili olması için dağıtım için yeniden başlatın. Bunu yapmak için Azure Portalı'na gidin ve gidin **genel bakış** sayfası, web uygulamanızın. Seçin **yeniden** sayfasının düğmesini. Açılan pencerede görüntülenir, seçin **Evet** onaylamak için. Ardından, aşağıda gösterildiği gibi web uygulamanızın göz atabilirsiniz:

![Azure App Service'e Linux üzerinde dağıtılan .NET Core uygulama gözatma][10]

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a>Sonraki adımlar
* [Azure App Service Web uygulaması Linux SSS](./app-service-linux-faq.md)

[1]: ./media/app-service-linux-using-dotnetcore/top-level-create.png
[2]: ./media/app-service-linux-using-dotnetcore/dotnet-new-webapp.png
[7]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-local.png
[10]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-azure.png
