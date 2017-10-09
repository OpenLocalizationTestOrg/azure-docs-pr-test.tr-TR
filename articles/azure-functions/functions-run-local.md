---
title: "aaaDevelop ve çalışma Azure işlevleri yerel olarak | Microsoft Docs"
description: "Nasıl toocode ve test Azure işlevleri, yerel bilgisayarınızda Azure işlevlerini çalıştırmadan önce öğrenin."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
ms.assetid: 242736be-ec66-4114-924b-31795fd18884
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: multiple
ms.topic: article
ms.date: 07/12/2017
ms.author: glenga
ms.openlocfilehash: 342ed4d6df41a2d2df9067948e19e347bb52c844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="code-and-test-azure-functions-locally"></a><span data-ttu-id="41d8a-103">Kod ve yerel olarak Azure işlevlerini test etme</span><span class="sxs-lookup"><span data-stu-id="41d8a-103">Code and test Azure functions locally</span></span>

<span data-ttu-id="41d8a-104">Merhaba sırasında [Azure portal] geliştirmek için Araçlar tam kümesi ve test Azure işlevleri, geliştiricilerin çoğu tercih yerel geliştirme deneyimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="41d8a-104">While hello [Azure portal] provides a full set of tools for developing and testing Azure Functions, many developers prefer a local development experience.</span></span> <span data-ttu-id="41d8a-105">Azure işlevleri kolay toouse kılar sevdiğiniz Kod Düzenleyicisi'ni ve yerel geliştirme araçları toodevelop ve yerel bilgisayarınızda işlevlerinizi test.</span><span class="sxs-lookup"><span data-stu-id="41d8a-105">Azure Functions makes it easy toouse your favorite code editor and local development tools toodevelop and test your functions on your local computer.</span></span> <span data-ttu-id="41d8a-106">İşlevlerinizi Azure olayları tetikleyebilir ve yerel bilgisayarınızda, C# ve JavaScript işlevleri ayıklayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="41d8a-106">Your functions can trigger on events in Azure, and you can debug your C# and JavaScript functions on your local computer.</span></span> 

<span data-ttu-id="41d8a-107">Visual Studio C# Geliştirici, Azure işlevleri de olup olmadığını [Visual Studio 2017 ile tümleşir](functions-develop-vs.md).</span><span class="sxs-lookup"><span data-stu-id="41d8a-107">If you are a Visual Studio C# developer, Azure Functions also [integrates with Visual Studio 2017](functions-develop-vs.md).</span></span>

## <a name="install-hello-azure-functions-core-tools"></a><span data-ttu-id="41d8a-108">Hello Azure işlevleri çekirdek araçlarını yükleme</span><span class="sxs-lookup"><span data-stu-id="41d8a-108">Install hello Azure Functions Core Tools</span></span>

<span data-ttu-id="41d8a-109">Azure işlevleri çekirdek araçları, yerel Windows bilgisayarınızda çalıştırabilirsiniz hello Azure işlevleri çalışma zamanı, yerel bir sürümüdür.</span><span class="sxs-lookup"><span data-stu-id="41d8a-109">Azure Functions Core Tools is a local version of hello Azure Functions runtime that you can run on your local Windows computer.</span></span> <span data-ttu-id="41d8a-110">Bir öykünücü veya benzetici değil.</span><span class="sxs-lookup"><span data-stu-id="41d8a-110">It's not an emulator or simulator.</span></span> <span data-ttu-id="41d8a-111">Bunu sahip hello aynı çalışma zamanı bu powers Azure işlevlerinde.</span><span class="sxs-lookup"><span data-stu-id="41d8a-111">It's hello same runtime that powers Functions in Azure.</span></span>

<span data-ttu-id="41d8a-112">Merhaba [Azure işlevleri çekirdek Araçları] npm paket olarak sağlanır.</span><span class="sxs-lookup"><span data-stu-id="41d8a-112">hello [Azure Functions Core Tools] is provided as an npm package.</span></span> <span data-ttu-id="41d8a-113">Öncelikle [NodeJS yükleme](https://docs.npmjs.com/getting-started/installing-node), npm içerir.</span><span class="sxs-lookup"><span data-stu-id="41d8a-113">You must first [install NodeJS](https://docs.npmjs.com/getting-started/installing-node), which includes npm.</span></span>  

>[!NOTE]
><span data-ttu-id="41d8a-114">Şu anda hello Azure işlevleri çekirdek araçları paketini yalnızca Windows bilgisayarlara yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="41d8a-114">At this time, hello Azure Functions Core Tools package can only be installed on Windows computers.</span></span> <span data-ttu-id="41d8a-115">Merhaba işlevleri konaktaki tooa geçici sınırlaması nedeniyle bu kısıtlaması yoktur.</span><span class="sxs-lookup"><span data-stu-id="41d8a-115">This restriction is due tooa temporary limitation in hello Functions host.</span></span>

<span data-ttu-id="41d8a-116">[Azure işlevleri çekirdek Araçları] komut diğer adları aşağıdaki hello ekler:</span><span class="sxs-lookup"><span data-stu-id="41d8a-116">[Azure Functions Core Tools] adds hello following command aliases:</span></span>
* <span data-ttu-id="41d8a-117">**FUNC**</span><span class="sxs-lookup"><span data-stu-id="41d8a-117">**func**</span></span>
* <span data-ttu-id="41d8a-118">**azfun**</span><span class="sxs-lookup"><span data-stu-id="41d8a-118">**azfun**</span></span>
* <span data-ttu-id="41d8a-119">**azurefunctions**</span><span class="sxs-lookup"><span data-stu-id="41d8a-119">**azurefunctions**</span></span>

<span data-ttu-id="41d8a-120">Tüm bu diğer adı yerine kullanılabilir `func` bu konudaki hello örnekleri gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="41d8a-120">All of these alias can be used instead of `func` shown in hello examples in this topic.</span></span>

## <a name="create-a-local-functions-project"></a><span data-ttu-id="41d8a-121">Bir yerel işlevler projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="41d8a-121">Create a local Functions project</span></span>

<span data-ttu-id="41d8a-122">Yerel olarak çalıştırırken, işlevleri proje hello dosyaları host.json ve local.settings.json sahip bir dizindir.</span><span class="sxs-lookup"><span data-stu-id="41d8a-122">When running locally, a Functions project is a directory that has hello files host.json and local.settings.json.</span></span> <span data-ttu-id="41d8a-123">Bu dizin olan hello Azure işlevi uygulamada eşdeğeridir.</span><span class="sxs-lookup"><span data-stu-id="41d8a-123">This directory is hello equivalent of a function app in Azure.</span></span> <span data-ttu-id="41d8a-124">toolearn hello Azure işlevleri klasör yapısı hakkında daha fazla bilgi görmek hello [Azure işlevleri Geliştirici Kılavuzu](functions-reference.md#folder-structure).</span><span class="sxs-lookup"><span data-stu-id="41d8a-124">toolearn more about hello Azure Functions folder structure, see hello [Azure Functions developers guide](functions-reference.md#folder-structure).</span></span>

<span data-ttu-id="41d8a-125">Bir komut isteminde hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="41d8a-125">At a command prompt, run hello following command:</span></span>

```
func init MyFunctionProj
```

<span data-ttu-id="41d8a-126">Merhaba çıktı hello örnek aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="41d8a-126">hello output looks like hello following example:</span></span>

```
Writing .gitignore
Writing host.json
Writing local.settings.json
Created launch.json
Initialized empty Git repository in D:/Code/Playground/MyFunctionProj/.git/
```

<span data-ttu-id="41d8a-127">bir Git deposu, kullanım hello seçeneği oluşturma dışında tooopt `--no-source-control [-n]`.</span><span class="sxs-lookup"><span data-stu-id="41d8a-127">tooopt out of creating a Git repository, use hello option `--no-source-control [-n]`.</span></span>

<a name="local-settings"></a>

## <a name="local-settings-file"></a><span data-ttu-id="41d8a-128">Yerel ayarlar dosyası</span><span class="sxs-lookup"><span data-stu-id="41d8a-128">Local settings file</span></span>

<span data-ttu-id="41d8a-129">Uygulama ayarları, bağlantı dizeleri ve ayarları için Azure işlevleri çekirdek araçları Hello dosya local.settings.json depolar.</span><span class="sxs-lookup"><span data-stu-id="41d8a-129">hello file local.settings.json stores app settings, connection strings, and settings for Azure Functions Core Tools.</span></span> <span data-ttu-id="41d8a-130">Yapı izlenerek hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="41d8a-130">It has hello following structure:</span></span>

```json
{
  "IsEncrypted": false,   
  "Values": {
    "AzureWebJobsStorage": "<connection string>", 
    "AzureWebJobsDashboard": "<connection string>", 
  },
  "Host": {
    "LocalHttpPort": 7071, 
    "CORS": "*" 
  },
  "ConnectionStrings": {
    "SQLConnectionString": "Value"
  }
}
```
| <span data-ttu-id="41d8a-131">Ayar</span><span class="sxs-lookup"><span data-stu-id="41d8a-131">Setting</span></span>      | <span data-ttu-id="41d8a-132">Açıklama</span><span class="sxs-lookup"><span data-stu-id="41d8a-132">Description</span></span>                            |
| ------------ | -------------------------------------- |
| <span data-ttu-id="41d8a-133">**Isencrypted**</span><span class="sxs-lookup"><span data-stu-id="41d8a-133">**IsEncrypted**</span></span> | <span data-ttu-id="41d8a-134">Ayarlandığında çok**doğru**, tüm değerleri yerel makine anahtarı kullanılarak şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="41d8a-134">When set too**true**, all values are encrypted using a local machine key.</span></span> <span data-ttu-id="41d8a-135">İle kullanılan `func settings` komutları.</span><span class="sxs-lookup"><span data-stu-id="41d8a-135">Used with `func settings` commands.</span></span> <span data-ttu-id="41d8a-136">Varsayılan değer **false**.</span><span class="sxs-lookup"><span data-stu-id="41d8a-136">Default value is **false**.</span></span> |
| <span data-ttu-id="41d8a-137">**Değerleri**</span><span class="sxs-lookup"><span data-stu-id="41d8a-137">**Values**</span></span> | <span data-ttu-id="41d8a-138">Uygulama ayarlarını yerel olarak çalıştırırken kullanılan koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="41d8a-138">Collection of application settings used when running locally.</span></span> <span data-ttu-id="41d8a-139">Uygulama ayarları toothis nesnenizin ekleyin.</span><span class="sxs-lookup"><span data-stu-id="41d8a-139">Add your application settings toothis object.</span></span>  |
| <span data-ttu-id="41d8a-140">**AzureWebJobsStorage**</span><span class="sxs-lookup"><span data-stu-id="41d8a-140">**AzureWebJobsStorage**</span></span> | <span data-ttu-id="41d8a-141">Ayarlar, bağlantı dizesi toohello hello Azure işlevleri çalışma zamanı tarafından dahili olarak kullanılır Azure depolama hesabı hello.</span><span class="sxs-lookup"><span data-stu-id="41d8a-141">Sets hello connection string toohello Azure Storage account that is used internally by hello Azure Functions runtime.</span></span> <span data-ttu-id="41d8a-142">Merhaba depolama hesabı, işlevin Tetikleyicileri destekler.</span><span class="sxs-lookup"><span data-stu-id="41d8a-142">hello storage account supports your function's triggers.</span></span> <span data-ttu-id="41d8a-143">Bu depolama hesabı bağlantı ayarı tetiklenen HTTP işlevler hariç tüm işlevleri için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="41d8a-143">This storage account connection setting is required for all functions except for HTTP triggered functions.</span></span>  |
| <span data-ttu-id="41d8a-144">**AzureWebJobsDashboard**</span><span class="sxs-lookup"><span data-stu-id="41d8a-144">**AzureWebJobsDashboard**</span></span> | <span data-ttu-id="41d8a-145">Kullanılan toostore hello işlev günlükleri olan hello bağlantı dizesi toohello Azure depolama hesabı ayarlar.</span><span class="sxs-lookup"><span data-stu-id="41d8a-145">Sets hello connection string toohello Azure Storage account that is used toostore hello function logs.</span></span> <span data-ttu-id="41d8a-146">Bu isteğe bağlı değeri hello günlükleri hello Portalı'nda erişilebilir hale getirir.</span><span class="sxs-lookup"><span data-stu-id="41d8a-146">This optional value makes hello logs accessible in hello portal.</span></span>|
| <span data-ttu-id="41d8a-147">**Ana bilgisayar**</span><span class="sxs-lookup"><span data-stu-id="41d8a-147">**Host**</span></span> | <span data-ttu-id="41d8a-148">Bu bölümdeki ayarlarını hello işlevleri ana bilgisayar işlemi yerel olarak çalıştırırken özelleştirin.</span><span class="sxs-lookup"><span data-stu-id="41d8a-148">Settings in this section customize hello Functions host process when running locally.</span></span> | 
| <span data-ttu-id="41d8a-149">**LocalHttpPort**</span><span class="sxs-lookup"><span data-stu-id="41d8a-149">**LocalHttpPort**</span></span> | <span data-ttu-id="41d8a-150">Ayarlar hello hello yerel işlevler ana çalıştırırken kullanılan varsayılan bağlantı noktası (`func host start` ve `func run`).</span><span class="sxs-lookup"><span data-stu-id="41d8a-150">Sets hello default port used when running hello local Functions host (`func host start` and `func run`).</span></span> <span data-ttu-id="41d8a-151">Merhaba `--port` komut satırı seçeneği bu değerin üzerine göre önceliklidir.</span><span class="sxs-lookup"><span data-stu-id="41d8a-151">hello `--port` command-line option takes precedence over this value.</span></span> |
| <span data-ttu-id="41d8a-152">**CORS**</span><span class="sxs-lookup"><span data-stu-id="41d8a-152">**CORS**</span></span> | <span data-ttu-id="41d8a-153">İzin verilen hello kaynakları tanımlayan [çıkış noktaları arası kaynak paylaşımı (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing).</span><span class="sxs-lookup"><span data-stu-id="41d8a-153">Defines hello origins allowed for [cross-origin resource sharing (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing).</span></span> <span data-ttu-id="41d8a-154">Çıkış boşluk virgülle ayrılmış bir liste olarak sağlanır.</span><span class="sxs-lookup"><span data-stu-id="41d8a-154">Origins are supplied as a comma-separated list with no spaces.</span></span> <span data-ttu-id="41d8a-155">Merhaba joker karakter değeri (**\***) desteklenir, her türlü kaynağa gelen isteklere izin verir.</span><span class="sxs-lookup"><span data-stu-id="41d8a-155">hello wildcard value (**\***) is supported, which allows requests from any origin.</span></span> |
| <span data-ttu-id="41d8a-156">**ConnectionStrings**</span><span class="sxs-lookup"><span data-stu-id="41d8a-156">**ConnectionStrings**</span></span> | <span data-ttu-id="41d8a-157">İşlevlerinizi için Hello veritabanı bağlantı dizelerini içerir.</span><span class="sxs-lookup"><span data-stu-id="41d8a-157">Contains hello database connection strings for your functions.</span></span> <span data-ttu-id="41d8a-158">Bu nesne bağlantı dizeleri hello sağlayıcısı türü toohello ortamıyla eklenen **System.Data.SqlClient**.</span><span class="sxs-lookup"><span data-stu-id="41d8a-158">Connection strings in this object are added toohello environment with hello provider type of **System.Data.SqlClient**.</span></span>  | 

<span data-ttu-id="41d8a-159">Çoğu Tetikleyicileri ve bağlamaları sahip bir **bağlantı** ortam değişkeni veya uygulama ayarını toohello adı eşlemeleri özelliği.</span><span class="sxs-lookup"><span data-stu-id="41d8a-159">Most triggers and bindings have a **Connection** property that maps toohello name of an environment variable or app setting.</span></span> <span data-ttu-id="41d8a-160">Her bağlantı özelliği için uygulama ayarı local.settings.json dosyasında tanımlanmış olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="41d8a-160">For each connection property, there must be app setting defined in local.settings.json file.</span></span> 

<span data-ttu-id="41d8a-161">Bu ayarlar, ortam değişkenleri olarak kodunuzda de okunabilir.</span><span class="sxs-lookup"><span data-stu-id="41d8a-161">These settings can also be read in your code as environment variables.</span></span> <span data-ttu-id="41d8a-162">C# ' ta kullanmak [System.Environment.GetEnvironmentVariable](https://msdn.microsoft.com/library/system.environment.getenvironmentvariable(v=vs.110).aspx) veya [ConfigurationManager.AppSettings](https://msdn.microsoft.com/library/system.configuration.configurationmanager.appsettings%28v=vs.110%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="41d8a-162">In C#, use [System.Environment.GetEnvironmentVariable](https://msdn.microsoft.com/library/system.environment.getenvironmentvariable(v=vs.110).aspx) or [ConfigurationManager.AppSettings](https://msdn.microsoft.com/library/system.configuration.configurationmanager.appsettings%28v=vs.110%29.aspx).</span></span> <span data-ttu-id="41d8a-163">JavaScript'te, kullanmak `process.env`.</span><span class="sxs-lookup"><span data-stu-id="41d8a-163">In JavaScript, use `process.env`.</span></span> <span data-ttu-id="41d8a-164">Sistem ortam değişkeni olarak belirtilen ayarları hello local.settings.json dosyasındaki değerleri daha önceliklidir.</span><span class="sxs-lookup"><span data-stu-id="41d8a-164">Settings specified as a system environment variable take precedence over values in hello local.settings.json file.</span></span> 

<span data-ttu-id="41d8a-165">Merhaba local.settings.json dosyasındaki ayarları, yalnızca yerel olarak çalıştırırken işlevleri araçları tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="41d8a-165">Settings in hello local.settings.json file are only used by Functions tools when running locally.</span></span> <span data-ttu-id="41d8a-166">Merhaba proje yayımlanan tooAzure olduğunda varsayılan olarak, bu ayarlar otomatik olarak geçirilmez.</span><span class="sxs-lookup"><span data-stu-id="41d8a-166">By default, these settings are not migrated automatically when hello project is published tooAzure.</span></span> <span data-ttu-id="41d8a-167">Kullanım hello `--publish-local-settings` geçiş [yayımladığınızda](#publish) toomake emin bu ayarlar, Azure'da toohello işlev uygulaması eklenir.</span><span class="sxs-lookup"><span data-stu-id="41d8a-167">Use hello `--publish-local-settings` switch [when you publish](#publish) toomake sure these settings are added toohello function app in Azure.</span></span>

<span data-ttu-id="41d8a-168">İçin hiç geçerli bir depolama bağlantı dizesi ayarlandığında **AzureWebJobsStorage**, aşağıdaki hata iletisini hello gösterilir:</span><span class="sxs-lookup"><span data-stu-id="41d8a-168">When no valid storage connection string is set for **AzureWebJobsStorage**, hello following error message is shown:</span></span>  

><span data-ttu-id="41d8a-169">Local.settings.json eksik değeri AzureWebJobsStorage için.</span><span class="sxs-lookup"><span data-stu-id="41d8a-169">Missing value for AzureWebJobsStorage in local.settings.json.</span></span> <span data-ttu-id="41d8a-170">Bu, HTTP dışındaki tüm tetikleyiciler için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="41d8a-170">This is required for all triggers other than HTTP.</span></span> <span data-ttu-id="41d8a-171">Çalıştırabilirsiniz ' func azure functionary fetch-app-settings <functionAppName>' veya local.settings.json içinde bir bağlantı dizesini belirtin.</span><span class="sxs-lookup"><span data-stu-id="41d8a-171">You can run 'func azure functionary fetch-app-settings <functionAppName>' or specify a connection string in local.settings.json.</span></span>
  
[!INCLUDE [Note toonot use local storage](../../includes/functions-local-settings-note.md)]

### <a name="configure-app-settings"></a><span data-ttu-id="41d8a-172">Uygulama ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="41d8a-172">Configure app settings</span></span>

<span data-ttu-id="41d8a-173">bağlantı dizeleri için bir değer tooset hello aşağıdakilerden birini yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="41d8a-173">tooset a value for connection strings, you can do one of hello following:</span></span>
* <span data-ttu-id="41d8a-174">Merhaba bağlantı dizesinden girin [Azure Storage Gezgini](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="41d8a-174">Enter hello connection string from [Azure Storage Explorer](http://storageexplorer.com/).</span></span>
* <span data-ttu-id="41d8a-175">Aşağıdaki komutları hello birini kullanın:</span><span class="sxs-lookup"><span data-stu-id="41d8a-175">Use one of hello following commands:</span></span>

    ```
    func azure functionapp fetch-app-settings <FunctionAppName>
    ```
    ```
    func azure functionapp storage fetch-connection-string <StorageAccountName>
    ```
    <span data-ttu-id="41d8a-176">Her iki komutlar, toofirst oturum açma tooAzure gerektirir.</span><span class="sxs-lookup"><span data-stu-id="41d8a-176">Both commands require you toofirst sign-in tooAzure.</span></span>

## <a name="create-a-function"></a><span data-ttu-id="41d8a-177">İşlev oluşturma</span><span class="sxs-lookup"><span data-stu-id="41d8a-177">Create a function</span></span>

<span data-ttu-id="41d8a-178">bir işlev toocreate hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="41d8a-178">toocreate a function, run hello following command:</span></span>

```
func new
``` 
<span data-ttu-id="41d8a-179">`func new`İsteğe bağlı bağımsız değişkenler aşağıdaki hello destekler:</span><span class="sxs-lookup"><span data-stu-id="41d8a-179">`func new` supports hello following optional arguments:</span></span>

| <span data-ttu-id="41d8a-180">Bağımsız değişken</span><span class="sxs-lookup"><span data-stu-id="41d8a-180">Argument</span></span>     | <span data-ttu-id="41d8a-181">Açıklama</span><span class="sxs-lookup"><span data-stu-id="41d8a-181">Description</span></span>                            |
| ------------ | -------------------------------------- |
| **`--language -l`** | <span data-ttu-id="41d8a-182">programlama dili C#, F # ve JavaScript gibi hello şablonu.</span><span class="sxs-lookup"><span data-stu-id="41d8a-182">hello template programming language, such as C#, F#, or JavaScript.</span></span> |
| **`--template -t`** | <span data-ttu-id="41d8a-183">Merhaba şablon adı.</span><span class="sxs-lookup"><span data-stu-id="41d8a-183">hello template name.</span></span> |
| **`--name -n`** | <span data-ttu-id="41d8a-184">Merhaba işlev adı.</span><span class="sxs-lookup"><span data-stu-id="41d8a-184">hello function name.</span></span> |

<span data-ttu-id="41d8a-185">Çalıştırma gibi toocreate bir JavaScript HTTP tetikleyici:</span><span class="sxs-lookup"><span data-stu-id="41d8a-185">For example, toocreate a JavaScript HTTP trigger, run:</span></span>

```
func new --language JavaScript --template HttpTrigger --name MyHttpTrigger
```

<span data-ttu-id="41d8a-186">toocreate sıra tetiklenen bir işlev çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="41d8a-186">toocreate a queue-triggered function, run:</span></span>

```
func new --language JavaScript --template QueueTrigger --name QueueTriggerJS
```

## <a name="run-functions-locally"></a><span data-ttu-id="41d8a-187">İşlevler yerel olarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="41d8a-187">Run functions locally</span></span>

<span data-ttu-id="41d8a-188">toorun işlevleri proje Hello işlevleri konak çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="41d8a-188">toorun a Functions project, run hello Functions host.</span></span> <span data-ttu-id="41d8a-189">Merhaba konak hello projedeki tüm işlevler için Tetikleyicileri sağlar:</span><span class="sxs-lookup"><span data-stu-id="41d8a-189">hello host enables triggers for all functions in hello project:</span></span>

```
func host start
```

<span data-ttu-id="41d8a-190">`func host start`Seçenekler aşağıdaki hello destekler:</span><span class="sxs-lookup"><span data-stu-id="41d8a-190">`func host start` supports hello following options:</span></span>

| <span data-ttu-id="41d8a-191">Seçenek</span><span class="sxs-lookup"><span data-stu-id="41d8a-191">Option</span></span>     | <span data-ttu-id="41d8a-192">Açıklama</span><span class="sxs-lookup"><span data-stu-id="41d8a-192">Description</span></span>                            |
| ------------ | -------------------------------------- |
|**`--port -p`** | <span data-ttu-id="41d8a-193">Merhaba yerel bağlantı noktası toolisten üzerinde.</span><span class="sxs-lookup"><span data-stu-id="41d8a-193">hello local port toolisten on.</span></span> <span data-ttu-id="41d8a-194">Varsayılan değer: 7071.</span><span class="sxs-lookup"><span data-stu-id="41d8a-194">Default value: 7071.</span></span> |
| **`--debug <type>`** | <span data-ttu-id="41d8a-195">Başlangıç Seçenekleri `VSCode` ve `VS`.</span><span class="sxs-lookup"><span data-stu-id="41d8a-195">hello options are `VSCode` and `VS`.</span></span> |
| **`--cors`** | <span data-ttu-id="41d8a-196">Boşluk CORS çıkış noktası virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="41d8a-196">A comma-separated list of CORS origins, with no spaces.</span></span> |
| **`--nodeDebugPort -n`** | <span data-ttu-id="41d8a-197">Merhaba düğümü hata ayıklayıcı toouse için başlangıç bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="41d8a-197">hello port for hello node debugger toouse.</span></span> <span data-ttu-id="41d8a-198">Varsayılan: Launch.json'u veya 5858 arasında bir değer.</span><span class="sxs-lookup"><span data-stu-id="41d8a-198">Default: A value from launch.json or 5858.</span></span> |
| **`--debugLevel -d`** | <span data-ttu-id="41d8a-199">Merhaba konsol izleme düzeyini (kapalı, ayrıntılı, bilgi, uyarı veya hata).</span><span class="sxs-lookup"><span data-stu-id="41d8a-199">hello console trace level (off, verbose, info, warning, or error).</span></span> <span data-ttu-id="41d8a-200">Varsayılan: bilgisi.</span><span class="sxs-lookup"><span data-stu-id="41d8a-200">Default: Info.</span></span>|
| **`--timeout -t`** | <span data-ttu-id="41d8a-201">Merhaba işlevleri konak t o başlangıç, saniye cinsinden Hello zaman aşımına uğradı.</span><span class="sxs-lookup"><span data-stu-id="41d8a-201">hello time out for hello Functions host t     o start, in seconds.</span></span> <span data-ttu-id="41d8a-202">Varsayılan: 20 saniye.</span><span class="sxs-lookup"><span data-stu-id="41d8a-202">Default: 20 seconds.</span></span>|
| **`--useHttps`** | <span data-ttu-id="41d8a-203">Toohttps://localhost bağlayın: {bağlantı noktası} toohttp://localhost yerine: {port}.</span><span class="sxs-lookup"><span data-stu-id="41d8a-203">Bind toohttps://localhost:{port} rather than toohttp://localhost:{port}.</span></span> <span data-ttu-id="41d8a-204">Varsayılan olarak, bu seçenek bilgisayarınızda güvenilen bir sertifika oluşturur.</span><span class="sxs-lookup"><span data-stu-id="41d8a-204">By default, this option creates a trusted certificate on your computer.</span></span>|
| **`--pause-on-error`** | <span data-ttu-id="41d8a-205">Merhaba işlem çıkmadan önce ek giriş duraklatılıyor.</span><span class="sxs-lookup"><span data-stu-id="41d8a-205">Pause for additional input before exiting hello process.</span></span> <span data-ttu-id="41d8a-206">Azure işlevleri çekirdek araçları bir tümleşik geliştirme ortamı (IDE) başlatılırken yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="41d8a-206">Useful when launching Azure Functions Core Tools from an integrated development environment (IDE).</span></span>|

<span data-ttu-id="41d8a-207">Merhaba işlevleri ana bilgisayar başlatıldığında hello URL, HTTP tetiklemeli işlevleri çıkarır:</span><span class="sxs-lookup"><span data-stu-id="41d8a-207">When hello Functions host starts, it outputs hello URL of HTTP-triggered functions:</span></span>

```
Found hello following functions:
Host.Functions.MyHttpTrigger

ob host started
Http Function MyHttpTrigger: http://localhost:7071/api/MyHttpTrigger
```

### <a name="debug-in-vs-code-or-visual-studio"></a><span data-ttu-id="41d8a-208">VS Code'u veya Visual Studio'da hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="41d8a-208">Debug in VS Code or Visual Studio</span></span>

<span data-ttu-id="41d8a-209">tooattach bir hata ayıklayıcısı geçirmek hello `--debug` bağımsız değişkeni.</span><span class="sxs-lookup"><span data-stu-id="41d8a-209">tooattach a debugger, pass hello `--debug` argument.</span></span> <span data-ttu-id="41d8a-210">toodebug JavaScript işlevleri, Visual Studio Code kullanın.</span><span class="sxs-lookup"><span data-stu-id="41d8a-210">toodebug JavaScript functions, use Visual Studio Code.</span></span> <span data-ttu-id="41d8a-211">C# işlevleri için Visual Studio'yu kullanın.</span><span class="sxs-lookup"><span data-stu-id="41d8a-211">For C# functions, use Visual Studio.</span></span>

<span data-ttu-id="41d8a-212">toodebug C# işlevlerini kullanmak `--debug vs`.</span><span class="sxs-lookup"><span data-stu-id="41d8a-212">toodebug C# functions, use `--debug vs`.</span></span> <span data-ttu-id="41d8a-213">Aynı zamanda [Azure işlevleri Visual Studio 2017 Araçları](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span><span class="sxs-lookup"><span data-stu-id="41d8a-213">You can also use [Azure Functions Visual Studio 2017 Tools](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span></span> 

<span data-ttu-id="41d8a-214">toolaunch hello konak ve JavaScript hata ayıklama, yedekleme kümesi çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="41d8a-214">toolaunch hello host and set up JavaScript debugging, run:</span></span>

```
func host start --debug vscode
```

<span data-ttu-id="41d8a-215">Ardından Visual Studio Code hello **hata ayıklama** görünümü, select **Attach tooAzure işlevler**.</span><span class="sxs-lookup"><span data-stu-id="41d8a-215">Then, in Visual Studio Code, in hello **Debug** view, select **Attach tooAzure Functions**.</span></span> <span data-ttu-id="41d8a-216">Kesme noktaları ekleme, değişkenleri inceleyin ve kod üzerinden adım.</span><span class="sxs-lookup"><span data-stu-id="41d8a-216">You can attach breakpoints, inspect variables, and step through code.</span></span>

![Visual Studio Code ile JavaScript hata ayıklama](./media/functions-run-local/vscode-javascript-debugging.png)

### <a name="passing-test-data-tooa-function"></a><span data-ttu-id="41d8a-218">Geçirme test veri tooa işlevi</span><span class="sxs-lookup"><span data-stu-id="41d8a-218">Passing test data tooa function</span></span>

<span data-ttu-id="41d8a-219">Bir işlev doğrudan kullanarak da çağırabilirsiniz `func run <FunctionName>` ve hello işlevi için giriş verileri sağlar.</span><span class="sxs-lookup"><span data-stu-id="41d8a-219">You can also invoke a function directly by using `func run <FunctionName>` and provide input data for hello function.</span></span> <span data-ttu-id="41d8a-220">Bu komut benzer toorunning hello kullanarak bir işlevdir **Test** hello Azure portal sekmesindedir.</span><span class="sxs-lookup"><span data-stu-id="41d8a-220">This command is similar toorunning a function using hello **Test** tab in hello Azure portal.</span></span> <span data-ttu-id="41d8a-221">Bu komut hello tüm işlevler konak başlatır.</span><span class="sxs-lookup"><span data-stu-id="41d8a-221">This command launches hello entire Functions host.</span></span>

<span data-ttu-id="41d8a-222">`func run`Seçenekler aşağıdaki hello destekler:</span><span class="sxs-lookup"><span data-stu-id="41d8a-222">`func run` supports hello following options:</span></span>

| <span data-ttu-id="41d8a-223">Seçenek</span><span class="sxs-lookup"><span data-stu-id="41d8a-223">Option</span></span>     | <span data-ttu-id="41d8a-224">Açıklama</span><span class="sxs-lookup"><span data-stu-id="41d8a-224">Description</span></span>                            |
| ------------ | -------------------------------------- |
| **`--content -c`** | <span data-ttu-id="41d8a-225">Satır içi içeriği.</span><span class="sxs-lookup"><span data-stu-id="41d8a-225">Inline content.</span></span> |
| **`--debug -d`** | <span data-ttu-id="41d8a-226">Hata ayıklayıcı toohello ana bilgisayar işlemi hello işlevi çalıştırmadan önce ekleyin.</span><span class="sxs-lookup"><span data-stu-id="41d8a-226">Attach a debugger toohello host process before running hello function.</span></span>|
| **`--timeout -t`** | <span data-ttu-id="41d8a-227">Merhaba yerel işlevler ana kadar zaman toowait (saniye cinsinden) hazırdır.</span><span class="sxs-lookup"><span data-stu-id="41d8a-227">Time toowait (in seconds) until hello local Functions host is ready.</span></span>|
| **`--file -f`** | <span data-ttu-id="41d8a-228">Dosya adı toouse içeriği olarak hello.</span><span class="sxs-lookup"><span data-stu-id="41d8a-228">hello file name toouse as content.</span></span>|
| **`--no-interactive`** | <span data-ttu-id="41d8a-229">Giriş istemez.</span><span class="sxs-lookup"><span data-stu-id="41d8a-229">Does not prompt for input.</span></span> <span data-ttu-id="41d8a-230">Otomasyon senaryoları için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="41d8a-230">Useful for automation scenarios.</span></span>|

<span data-ttu-id="41d8a-231">Örneğin, toocall bir HTTP tetiklemeli işlevin ve geçişi İçerik gövdesi, hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="41d8a-231">For example, toocall an HTTP-triggered function and pass content body, run hello following command:</span></span>

```
func run MyHttpTrigger -c '{\"name\": \"Azure\"}'
```

## <span data-ttu-id="41d8a-232"><a name="publish"></a>TooAzure yayımlama</span><span class="sxs-lookup"><span data-stu-id="41d8a-232"><a name="publish"></a>Publish tooAzure</span></span>

<span data-ttu-id="41d8a-233">toopublish işlevleri proje tooa işlev uygulaması Azure, kullanım hello `publish` komutu:</span><span class="sxs-lookup"><span data-stu-id="41d8a-233">toopublish a Functions project tooa function app in Azure, use hello `publish` command:</span></span>

```
func azure functionapp publish <FunctionAppName>
```

<span data-ttu-id="41d8a-234">Hello aşağıdaki seçenekleri kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="41d8a-234">You can use hello following options:</span></span>

| <span data-ttu-id="41d8a-235">Seçenek</span><span class="sxs-lookup"><span data-stu-id="41d8a-235">Option</span></span>     | <span data-ttu-id="41d8a-236">Açıklama</span><span class="sxs-lookup"><span data-stu-id="41d8a-236">Description</span></span>                            |
| ------------ | -------------------------------------- |
| **`--publish-local-settings -i`** |  <span data-ttu-id="41d8a-237">Yayımlama hello ayarı zaten varsa toooverwrite isteyen local.settings.json tooAzure içinde ayarları.</span><span class="sxs-lookup"><span data-stu-id="41d8a-237">Publish settings in local.settings.json tooAzure, prompting toooverwrite if hello setting already exists.</span></span>|
| **`--overwrite-settings -y`** | <span data-ttu-id="41d8a-238">İle birlikte kullanılmalıdır `-i`.</span><span class="sxs-lookup"><span data-stu-id="41d8a-238">Must be used with `-i`.</span></span> <span data-ttu-id="41d8a-239">Azure AppSettings farklı olması durumunda ile yerel değerin üzerine yazar.</span><span class="sxs-lookup"><span data-stu-id="41d8a-239">Overwrites AppSettings in Azure with local value if different.</span></span> <span data-ttu-id="41d8a-240">Komut istemi varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="41d8a-240">Default is prompt.</span></span>|

<span data-ttu-id="41d8a-241">Merhaba `publish` komutu hello hello işlevleri proje dizininin içeriğini yükler.</span><span class="sxs-lookup"><span data-stu-id="41d8a-241">hello `publish` command uploads hello contents of hello Functions project directory.</span></span> <span data-ttu-id="41d8a-242">Dosyaları yerel olarak silerseniz, hello `publish` komutu silinmez Azure'dan.</span><span class="sxs-lookup"><span data-stu-id="41d8a-242">If you delete files locally, hello `publish` command does not delete them from Azure.</span></span> <span data-ttu-id="41d8a-243">Hello kullanarak Azure dosyaları silebilirsiniz [Kudu aracı](functions-how-to-use-azure-function-app-settings.md#kudu) hello içinde [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="41d8a-243">You can delete files in Azure by using hello [Kudu tool](functions-how-to-use-azure-function-app-settings.md#kudu) in hello [Azure portal].</span></span>

## <a name="next-steps"></a><span data-ttu-id="41d8a-244">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="41d8a-244">Next steps</span></span>

<span data-ttu-id="41d8a-245">Azure işlevleri çekirdek Araçları [kaynak açın ve GitHub üzerinde barındırılan](https://github.com/azure/azure-functions-cli).</span><span class="sxs-lookup"><span data-stu-id="41d8a-245">Azure Functions Core Tools is [open source and hosted on GitHub](https://github.com/azure/azure-functions-cli).</span></span>  
<span data-ttu-id="41d8a-246">bir hata veya özellik isteği toofile [GitHub sorunu açmak](https://github.com/azure/azure-functions-cli/issues).</span><span class="sxs-lookup"><span data-stu-id="41d8a-246">toofile a bug or feature request, [open a GitHub issue](https://github.com/azure/azure-functions-cli/issues).</span></span> 

<!-- LINKS -->

[Azure işlevleri çekirdek Araçları]: https://www.npmjs.com/package/azure-functions-core-tools
[Azure portal]: https://portal.azure.com 
