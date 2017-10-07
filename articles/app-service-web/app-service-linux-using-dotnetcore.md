---
title: ".NET Core Linux üzerinde Web uygulamasında aaaUse | Microsoft Docs"
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
ms.openlocfilehash: 9b7fb7185dff2c99ed88e7937d455177504937b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-net-core-in-an-azure-web-app-on-linux"></a>.NET Core Linux Azure web uygulaması kullanın #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

[Web uygulaması](https://docs.microsoft.com/azure/app-service-web/app-service-linux-intro) Linux'ta hello Linux işletim sistemi kullanan bir düzeyde ölçeklenebilir, otomatik olarak düzeltme eki uygulama web barındırma hizmeti sağlar. Bu öğretici gösteren adım adım yönergeler içerir nasıl toocreate bir [.NET Core](https://docs.microsoft.com/aspnet/core/) Linux Azure web uygulaması üzerinde uygulama. 

![Linux üzerinde Web Uygulaması][10]

Mac, Windows veya Linux makine kullanarak aşağıda hello adımları izleyebilirsiniz.

## <a name="prerequisites"></a>Ön koşullar ##

toocomplete Bu öğretici: 

* Merhaba yüklemek [.NET Core SDK](https://www.microsoft.com/net/download/core).
* Yükleme [Git](https://git-scm.com/downloads).

[!INCLUDE [Free trial note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-local-net-core-application"></a>Yerel bir .NET Core uygulama oluşturma ##

Yeni bir terminal oturumu başlatın. Adlı bir dizin oluşturun `hellodotnetcore`ve hello geçerli dizin tooit değiştirin. Merhaba aşağıdakileri yazın: 

```
dotnet new web
``` 

  Bu komut dosyaları üç oluşturur (*hellodotnetcore.csproj*, *Program.cs*, ve *haline*) ve bir boş klasör (*wwwroot /*) Merhaba geçerli dizinin altında. Merhaba içeriğini `.csproj` dosya hello aşağıdaki gibi görünmelidir: 

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

Bu uygulama bir web uygulaması olduğundan, ASP.NET Core paketi olan otomatik olarak bir başvuru tooan toohello eklenen *hellodotnetcore.csproj* dosya. Merhaba paketin Hello sürüm numarası framework seçilen toohello göre ayarlanır. .NET Core 1.1 kullanılmakta olduğu için bu örnek ASP.NET Core sürüm 1.1.2 başvuruyor.

## <a name="build-and-test-hello-application-locally"></a>Derleme ve hello uygulama yerel olarak test ##

Derleme ve .NET Core uygulamanızı hello ile çalıştırma `dotnet restore` hello tarafından izlenen komutu `dotnet run` aşağıda gösterildiği gibi komut:

```
dotnet restore
dotnet run
```


Merhaba uygulaması başlatıldığında hello uygulama tooincoming isteklerini bir bağlantı noktasında dinleme belirten bir ileti görüntüler. 

```bash
Hosting environment: Production
Content root path: C:\hellodotnetcore
Now listening on: http://localhost:5000
Application started. Press Ctrl+C tooshut down.
```

Çok göz atarak test`http://localhost:5000/` tarayıcınızla. Her şeyi düzgün çalışır, "Hello World!" konusuna bakın Merhaba sonucu metin olarak.

![Tarayıcı ile test][7]

## <a name="create-a-net-core-app-in-hello-azure-portal"></a>Hello Azure portalı bir .NET Core uygulaması oluşturma ##

İlk toocreate boş web uygulaması gerekir. İçinde toohello oturum [Azure portal](https://portal.azure.com/) ve yeni bir [Linux üzerinde Web uygulaması](https://portal.azure.com/#create/Microsoft.AppSvcLinux).

![Bir web uygulaması oluşturma][1]

Ne zaman hello **oluşturma** sayfası açılır, web uygulamanız hakkında ayrıntılar verilmektedir:

![Bir .NET çekirdeği çalışma zamanı yığını seçme][2]

Kullanım hello aşağıdaki tablo Kılavuzu toofill hello çıkış olarak **oluşturma** sayfasında sonra seçin **Tamam** ve **oluşturma** toocreate hello uygulama.

| Ayar      | Önerilen değer  | Açıklama                                        |
| ------------ | ---------------- | -------------------------------------------------- |
| Uygulama adı | hellodotnetcore  | Merhaba, uygulamanızın adıdır. Bu ad benzersiz olmalıdır. |
| Abonelik | Var olan bir abonelik seçin | Hello Azure aboneliği. |
| Kaynak Grubu | myResourceGroup |  Hello Azure kaynak grubu toocontain hello web uygulaması. |
| App Service Planı | Var olan uygulama hizmeti planı adı |  Uygulama hizmeti planı hello.  |
| Kapsayıcı yapılandırın | .NET core 1.1 | Bu web uygulaması için kapsayıcı türü Hello: yerleşik, Docker veya özel kayıt defteri. |
| Görüntü kaynağı  | Yerleşik  |  Merhaba görüntü Hello kaynağı. |
| Çalışma zamanı yığını  | .NET core 1.1  | Merhaba çalışma zamanı yığını ve sürüm.  |

## <a name="deploy-your-application-via-git"></a>Git aracılığıyla uygulamanızı dağıtma ##

Git toodeploy hello .NET Core uygulama tooAzure App Service Web uygulaması Linux'ta kullanın.

yapılandırılmış Git dağıtımı Hello yeni Azure web uygulaması zaten var. Web uygulaması adı ekledikten sonra URL aşağıdaki toohello giderek hello Git dağıtım URL'si bulacaksınız:

```https://{your web app name}.scm.azurewebsites.net/api/scm/info```

Merhaba Git URL'si, web uygulaması adınıza göre form aşağıdaki hello sahiptir:

```https://{your web app name}.scm.azurewebsites.net/{your web app name}.git```

Aşağıdaki komutları toodeploy hello yerel uygulama tooyour Azure web uygulaması hello çalıştırın: 
 
```bash
git init
git remote add azure <Git deployment URL from above>
git add *.csproj *.cs
git commit -m "Initial deployment commit"
git push azure master
```

Altındaki tüm dosyalar toopush gerekmeyen *bin /* veya *obj /* dizinleri uygulamanızı hello bulutta oluşturulduğundan zaman hello uygulamanın kaynak dosyaları tooAzure gönderilir. Merhaba oluşturma işlemi tamamlandıktan sonra ikili dosyaları hello uygulamanın dizininde içine kopyalanır */home/site/wwwroot/*.

Merhaba uzak dağıtım işlemlerini Başarı Raporu onaylayın. Gönderme işlemleri paket çözümleme itibaren sürebilir ve derleme hello bulutta çalışan işlemi olabilir. Olanları dosyaları kopyalandığını belirten dahil olmak üzere, birkaç durum iletilerini görürsünüz. Merhaba çıkış benzer toohello aşağıdaki gibi görünmelidir:

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
toohttps://hellodotnetcore.scm.azurewebsites.net/
 * [new branch]           master -> master

```

Merhaba dağıtım tamamlandıktan sonra web uygulamanız hello dağıtım tootake etkisi için yeniden başlatın. toodo bunu toohello Azure portalına gidin ve toohello gidin **genel bakış** sayfası, web uygulamanızın. Select hello **yeniden** hello sayfasında düğmesini. Açılan pencerede görüntülenir, seçin **Evet** tooconfirm. Ardından, aşağıda gösterildiği gibi web uygulamanızın göz atabilirsiniz:

![Uygulama tooAzure uygulama hizmeti Linux üzerinde dağıtılan .NET Core gözatma][10]

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a>Sonraki adımlar
* [Azure App Service Web uygulaması Linux SSS](./app-service-linux-faq.md)

[1]: ./media/app-service-linux-using-dotnetcore/top-level-create.png
[2]: ./media/app-service-linux-using-dotnetcore/dotnet-new-webapp.png
[7]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-local.png
[10]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-azure.png
