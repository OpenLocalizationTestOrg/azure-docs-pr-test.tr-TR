---
title: "Geliştirme ve Azure işlevleri yerel olarak çalıştırma | Microsoft Docs"
description: "Kod ve Azure işlevlerini çalıştırmadan önce yerel bilgisayarınızda Azure işlevlerini test öğrenin."
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
ms.openlocfilehash: bbe03973dbd7c70463caa6d1a45efae2ec722c05
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="code-and-test-azure-functions-locally"></a><span data-ttu-id="5cdaa-103">Kod ve yerel olarak Azure işlevlerini test etme</span><span class="sxs-lookup"><span data-stu-id="5cdaa-103">Code and test Azure functions locally</span></span>

<span data-ttu-id="5cdaa-104">Sırada [Azure portal] geliştirmek için Araçlar tam kümesi ve test Azure işlevleri, geliştiricilerin çoğu tercih yerel geliştirme deneyimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-104">While the [Azure portal] provides a full set of tools for developing and testing Azure Functions, many developers prefer a local development experience.</span></span> <span data-ttu-id="5cdaa-105">Azure işlevleri geliştirmek ve yerel bilgisayarınızda işlevlerinizi test etmek için sık kullanılan kod düzenleyicisini ve yerel geliştirme araçları kullanın kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-105">Azure Functions makes it easy to use your favorite code editor and local development tools to develop and test your functions on your local computer.</span></span> <span data-ttu-id="5cdaa-106">İşlevlerinizi Azure olayları tetikleyebilir ve yerel bilgisayarınızda, C# ve JavaScript işlevleri ayıklayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-106">Your functions can trigger on events in Azure, and you can debug your C# and JavaScript functions on your local computer.</span></span> 

<span data-ttu-id="5cdaa-107">Visual Studio C# Geliştirici, Azure işlevleri de olup olmadığını [Visual Studio 2017 ile tümleşir](functions-develop-vs.md).</span><span class="sxs-lookup"><span data-stu-id="5cdaa-107">If you are a Visual Studio C# developer, Azure Functions also [integrates with Visual Studio 2017](functions-develop-vs.md).</span></span>

## <a name="install-the-azure-functions-core-tools"></a><span data-ttu-id="5cdaa-108">Azure işlevleri çekirdek Araçları'nı yükleme</span><span class="sxs-lookup"><span data-stu-id="5cdaa-108">Install the Azure Functions Core Tools</span></span>

<span data-ttu-id="5cdaa-109">Azure işlevleri çekirdek araçları, yerel Windows bilgisayarınızda çalıştırabilirsiniz Azure işlevleri çalışma zamanı, yerel bir sürümüdür.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-109">Azure Functions Core Tools is a local version of the Azure Functions runtime that you can run on your local Windows computer.</span></span> <span data-ttu-id="5cdaa-110">Bir öykünücü veya benzetici değil.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-110">It's not an emulator or simulator.</span></span> <span data-ttu-id="5cdaa-111">Powers Azure işlevleri çalışma zamanı olur.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-111">It's the same runtime that powers Functions in Azure.</span></span>

<span data-ttu-id="5cdaa-112">[Azure işlevleri çekirdek Araçları] npm paket olarak sağlanır.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-112">The [Azure Functions Core Tools] is provided as an npm package.</span></span> <span data-ttu-id="5cdaa-113">Öncelikle [NodeJS yükleme](https://docs.npmjs.com/getting-started/installing-node), npm içerir.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-113">You must first [install NodeJS](https://docs.npmjs.com/getting-started/installing-node), which includes npm.</span></span>  

>[!NOTE]
><span data-ttu-id="5cdaa-114">Şu anda Azure işlevleri çekirdek araçları paketini yalnızca Windows bilgisayarlara yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-114">At this time, the Azure Functions Core Tools package can only be installed on Windows computers.</span></span> <span data-ttu-id="5cdaa-115">İşlevler konakta geçici bir sınırlama nedeniyle bu kısıtlaması yoktur.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-115">This restriction is due to a temporary limitation in the Functions host.</span></span>

<span data-ttu-id="5cdaa-116">[Azure işlevleri çekirdek Araçları] aşağıdaki komut diğer adları ekler:</span><span class="sxs-lookup"><span data-stu-id="5cdaa-116">[Azure Functions Core Tools] adds the following command aliases:</span></span>
* <span data-ttu-id="5cdaa-117">**FUNC**</span><span class="sxs-lookup"><span data-stu-id="5cdaa-117">**func**</span></span>
* <span data-ttu-id="5cdaa-118">**azfun**</span><span class="sxs-lookup"><span data-stu-id="5cdaa-118">**azfun**</span></span>
* <span data-ttu-id="5cdaa-119">**azurefunctions**</span><span class="sxs-lookup"><span data-stu-id="5cdaa-119">**azurefunctions**</span></span>

<span data-ttu-id="5cdaa-120">Tüm bu diğer adı yerine kullanılabilir `func` bu konudaki örnekler gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-120">All of these alias can be used instead of `func` shown in the examples in this topic.</span></span>

## <a name="create-a-local-functions-project"></a><span data-ttu-id="5cdaa-121">Bir yerel işlevler projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="5cdaa-121">Create a local Functions project</span></span>

<span data-ttu-id="5cdaa-122">Yerel olarak çalıştırırken, işlevleri proje dosyalarını host.json ve local.settings.json sahip bir dizindir.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-122">When running locally, a Functions project is a directory that has the files host.json and local.settings.json.</span></span> <span data-ttu-id="5cdaa-123">Bu dizinde bir işlev uygulaması Azure eşdeğeridir.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-123">This directory is the equivalent of a function app in Azure.</span></span> <span data-ttu-id="5cdaa-124">Azure işlevleri klasör yapısı hakkında daha fazla bilgi için bkz: [Azure işlevleri Geliştirici Kılavuzu](functions-reference.md#folder-structure).</span><span class="sxs-lookup"><span data-stu-id="5cdaa-124">To learn more about the Azure Functions folder structure, see the [Azure Functions developers guide](functions-reference.md#folder-structure).</span></span>

<span data-ttu-id="5cdaa-125">Bir komut isteminde aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="5cdaa-125">At a command prompt, run the following command:</span></span>

```
func init MyFunctionProj
```

<span data-ttu-id="5cdaa-126">Çıktı aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="5cdaa-126">The output looks like the following example:</span></span>

```
Writing .gitignore
Writing host.json
Writing local.settings.json
Created launch.json
Initialized empty Git repository in D:/Code/Playground/MyFunctionProj/.git/
```

<span data-ttu-id="5cdaa-127">Git deposu oluşturuluyor dışında kabul etmek için seçeneği kullanın. `--no-source-control [-n]`.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-127">To opt out of creating a Git repository, use the option `--no-source-control [-n]`.</span></span>

<a name="local-settings"></a>

## <a name="local-settings-file"></a><span data-ttu-id="5cdaa-128">Yerel ayarlar dosyası</span><span class="sxs-lookup"><span data-stu-id="5cdaa-128">Local settings file</span></span>

<span data-ttu-id="5cdaa-129">Dosya local.settings.json uygulama ayarları, bağlantı dizeleri ve Azure işlevleri çekirdek araçları ayarlarını saklar.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-129">The file local.settings.json stores app settings, connection strings, and settings for Azure Functions Core Tools.</span></span> <span data-ttu-id="5cdaa-130">Aşağıdaki yapı vardır:</span><span class="sxs-lookup"><span data-stu-id="5cdaa-130">It has the following structure:</span></span>

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
| <span data-ttu-id="5cdaa-131">Ayar</span><span class="sxs-lookup"><span data-stu-id="5cdaa-131">Setting</span></span>      | <span data-ttu-id="5cdaa-132">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5cdaa-132">Description</span></span>                            |
| ------------ | -------------------------------------- |
| <span data-ttu-id="5cdaa-133">**Isencrypted**</span><span class="sxs-lookup"><span data-stu-id="5cdaa-133">**IsEncrypted**</span></span> | <span data-ttu-id="5cdaa-134">Ayarlandığında **doğru**, tüm değerleri yerel makine anahtarı kullanılarak şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-134">When set to **true**, all values are encrypted using a local machine key.</span></span> <span data-ttu-id="5cdaa-135">İle kullanılan `func settings` komutları.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-135">Used with `func settings` commands.</span></span> <span data-ttu-id="5cdaa-136">Varsayılan değer **false**.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-136">Default value is **false**.</span></span> |
| <span data-ttu-id="5cdaa-137">**Değerleri**</span><span class="sxs-lookup"><span data-stu-id="5cdaa-137">**Values**</span></span> | <span data-ttu-id="5cdaa-138">Uygulama ayarlarını yerel olarak çalıştırırken kullanılan koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-138">Collection of application settings used when running locally.</span></span> <span data-ttu-id="5cdaa-139">Bu nesne için uygulamanızın ayarlarını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-139">Add your application settings to this object.</span></span>  |
| <span data-ttu-id="5cdaa-140">**AzureWebJobsStorage**</span><span class="sxs-lookup"><span data-stu-id="5cdaa-140">**AzureWebJobsStorage**</span></span> | <span data-ttu-id="5cdaa-141">Azure işlevleri çalışma zamanı tarafından dahili olarak kullanılır Azure depolama hesabı bağlantı dizesini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-141">Sets the connection string to the Azure Storage account that is used internally by the Azure Functions runtime.</span></span> <span data-ttu-id="5cdaa-142">Depolama hesabı, işlevin Tetikleyicileri destekler.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-142">The storage account supports your function's triggers.</span></span> <span data-ttu-id="5cdaa-143">Bu depolama hesabı bağlantı ayarı tetiklenen HTTP işlevler hariç tüm işlevleri için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-143">This storage account connection setting is required for all functions except for HTTP triggered functions.</span></span>  |
| <span data-ttu-id="5cdaa-144">**AzureWebJobsDashboard**</span><span class="sxs-lookup"><span data-stu-id="5cdaa-144">**AzureWebJobsDashboard**</span></span> | <span data-ttu-id="5cdaa-145">İşlev günlükleri depolamak için kullanılan Azure depolama hesabı bağlantı dizesini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-145">Sets the connection string to the Azure Storage account that is used to store the function logs.</span></span> <span data-ttu-id="5cdaa-146">Bu isteğe bağlı değeri günlükleri Portalı'nda erişilebilir hale getirir.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-146">This optional value makes the logs accessible in the portal.</span></span>|
| <span data-ttu-id="5cdaa-147">**Ana bilgisayar**</span><span class="sxs-lookup"><span data-stu-id="5cdaa-147">**Host**</span></span> | <span data-ttu-id="5cdaa-148">Bu bölümdeki ayarlarını işlevleri ana bilgisayar işlemi yerel olarak çalıştırırken özelleştirin.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-148">Settings in this section customize the Functions host process when running locally.</span></span> | 
| <span data-ttu-id="5cdaa-149">**LocalHttpPort**</span><span class="sxs-lookup"><span data-stu-id="5cdaa-149">**LocalHttpPort**</span></span> | <span data-ttu-id="5cdaa-150">Yerel işlevler ana çalıştırırken kullanılan varsayılan bağlantı noktasını ayarlar (`func host start` ve `func run`).</span><span class="sxs-lookup"><span data-stu-id="5cdaa-150">Sets the default port used when running the local Functions host (`func host start` and `func run`).</span></span> <span data-ttu-id="5cdaa-151">`--port` Komut satırı seçeneği bu değerin üzerine göre önceliklidir.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-151">The `--port` command-line option takes precedence over this value.</span></span> |
| <span data-ttu-id="5cdaa-152">**CORS**</span><span class="sxs-lookup"><span data-stu-id="5cdaa-152">**CORS**</span></span> | <span data-ttu-id="5cdaa-153">İzin verilen çıkış noktası tanımlar [çıkış noktaları arası kaynak paylaşımı (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing).</span><span class="sxs-lookup"><span data-stu-id="5cdaa-153">Defines the origins allowed for [cross-origin resource sharing (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing).</span></span> <span data-ttu-id="5cdaa-154">Çıkış boşluk virgülle ayrılmış bir liste olarak sağlanır.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-154">Origins are supplied as a comma-separated list with no spaces.</span></span> <span data-ttu-id="5cdaa-155">Joker karakter değeri (**\***) desteklenir, her türlü kaynağa gelen isteklere izin verir.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-155">The wildcard value (**\***) is supported, which allows requests from any origin.</span></span> |
| <span data-ttu-id="5cdaa-156">**ConnectionStrings**</span><span class="sxs-lookup"><span data-stu-id="5cdaa-156">**ConnectionStrings**</span></span> | <span data-ttu-id="5cdaa-157">İşlevlerinizi için veritabanı bağlantı dizelerini içerir.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-157">Contains the database connection strings for your functions.</span></span> <span data-ttu-id="5cdaa-158">Bu nesne bağlantı dizeleri, sağlayıcı türü ortamıyla eklenir **System.Data.SqlClient**.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-158">Connection strings in this object are added to the environment with the provider type of **System.Data.SqlClient**.</span></span>  | 

<span data-ttu-id="5cdaa-159">Çoğu Tetikleyicileri ve bağlamaları sahip bir **bağlantı** bir ortam değişkeni veya uygulama ayarı adı için eşleşen özellik.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-159">Most triggers and bindings have a **Connection** property that maps to the name of an environment variable or app setting.</span></span> <span data-ttu-id="5cdaa-160">Her bağlantı özelliği için uygulama ayarı local.settings.json dosyasında tanımlanmış olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-160">For each connection property, there must be app setting defined in local.settings.json file.</span></span> 

<span data-ttu-id="5cdaa-161">Bu ayarlar, ortam değişkenleri olarak kodunuzda de okunabilir.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-161">These settings can also be read in your code as environment variables.</span></span> <span data-ttu-id="5cdaa-162">C# ' ta kullanmak [System.Environment.GetEnvironmentVariable](https://msdn.microsoft.com/library/system.environment.getenvironmentvariable(v=vs.110).aspx) veya [ConfigurationManager.AppSettings](https://msdn.microsoft.com/library/system.configuration.configurationmanager.appsettings%28v=vs.110%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="5cdaa-162">In C#, use [System.Environment.GetEnvironmentVariable](https://msdn.microsoft.com/library/system.environment.getenvironmentvariable(v=vs.110).aspx) or [ConfigurationManager.AppSettings](https://msdn.microsoft.com/library/system.configuration.configurationmanager.appsettings%28v=vs.110%29.aspx).</span></span> <span data-ttu-id="5cdaa-163">JavaScript'te, kullanmak `process.env`.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-163">In JavaScript, use `process.env`.</span></span> <span data-ttu-id="5cdaa-164">Sistem ortam değişkeni olarak belirtilen ayarları local.settings.json dosyasındaki değerleri daha önceliklidir.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-164">Settings specified as a system environment variable take precedence over values in the local.settings.json file.</span></span> 

<span data-ttu-id="5cdaa-165">Local.settings.json dosyasındaki ayarları, yalnızca yerel olarak çalıştırırken işlevleri araçları tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-165">Settings in the local.settings.json file are only used by Functions tools when running locally.</span></span> <span data-ttu-id="5cdaa-166">Projeyi Azure'a yayımlandığında varsayılan olarak, bu ayarlar otomatik olarak geçirilmez.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-166">By default, these settings are not migrated automatically when the project is published to Azure.</span></span> <span data-ttu-id="5cdaa-167">Kullanım `--publish-local-settings` geçiş [yayımladığınızda](#publish) bu ayarlar, azure'da işlev uygulaması eklenir emin olmak için.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-167">Use the `--publish-local-settings` switch [when you publish](#publish) to make sure these settings are added to the function app in Azure.</span></span>

<span data-ttu-id="5cdaa-168">İçin hiç geçerli bir depolama bağlantı dizesi ayarlandığında **AzureWebJobsStorage**, aşağıdaki hata iletisi gösterilir:</span><span class="sxs-lookup"><span data-stu-id="5cdaa-168">When no valid storage connection string is set for **AzureWebJobsStorage**, the following error message is shown:</span></span>  

><span data-ttu-id="5cdaa-169">Local.settings.json eksik değeri AzureWebJobsStorage için.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-169">Missing value for AzureWebJobsStorage in local.settings.json.</span></span> <span data-ttu-id="5cdaa-170">Bu, HTTP dışındaki tüm tetikleyiciler için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-170">This is required for all triggers other than HTTP.</span></span> <span data-ttu-id="5cdaa-171">Çalıştırabilirsiniz ' func azure functionary fetch-app-settings <functionAppName>' veya local.settings.json içinde bir bağlantı dizesini belirtin.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-171">You can run 'func azure functionary fetch-app-settings <functionAppName>' or specify a connection string in local.settings.json.</span></span>
  
[!INCLUDE [Note to not use local storage](../../includes/functions-local-settings-note.md)]

### <a name="configure-app-settings"></a><span data-ttu-id="5cdaa-172">Uygulama ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5cdaa-172">Configure app settings</span></span>

<span data-ttu-id="5cdaa-173">Bağlantı dizeleri için bir değer ayarlamak için aşağıdakilerden birini yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5cdaa-173">To set a value for connection strings, you can do one of the following:</span></span>
* <span data-ttu-id="5cdaa-174">Bağlantı dizesi girin [Azure Storage Gezgini](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="5cdaa-174">Enter the connection string from [Azure Storage Explorer](http://storageexplorer.com/).</span></span>
* <span data-ttu-id="5cdaa-175">Aşağıdaki komutlardan birini kullanın:</span><span class="sxs-lookup"><span data-stu-id="5cdaa-175">Use one of the following commands:</span></span>

    ```
    func azure functionapp fetch-app-settings <FunctionAppName>
    ```
    ```
    func azure functionapp storage fetch-connection-string <StorageAccountName>
    ```
    <span data-ttu-id="5cdaa-176">Her iki komutlar için ilk oturum açma Azure gerektirir.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-176">Both commands require you to first sign-in to Azure.</span></span>

## <a name="create-a-function"></a><span data-ttu-id="5cdaa-177">İşlev oluşturma</span><span class="sxs-lookup"><span data-stu-id="5cdaa-177">Create a function</span></span>

<span data-ttu-id="5cdaa-178">Bir işlev oluşturmak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="5cdaa-178">To create a function, run the following command:</span></span>

```
func new
``` 
<span data-ttu-id="5cdaa-179">`func new`Aşağıdaki isteğe bağlı bağımsız değişkenler destekler:</span><span class="sxs-lookup"><span data-stu-id="5cdaa-179">`func new` supports the following optional arguments:</span></span>

| <span data-ttu-id="5cdaa-180">Bağımsız değişken</span><span class="sxs-lookup"><span data-stu-id="5cdaa-180">Argument</span></span>     | <span data-ttu-id="5cdaa-181">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5cdaa-181">Description</span></span>                            |
| ------------ | -------------------------------------- |
| **`--language -l`** | <span data-ttu-id="5cdaa-182">Dil C#, F # ve JavaScript gibi programlama şablonu.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-182">The template programming language, such as C#, F#, or JavaScript.</span></span> |
| **`--template -t`** | <span data-ttu-id="5cdaa-183">Şablon adı.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-183">The template name.</span></span> |
| **`--name -n`** | <span data-ttu-id="5cdaa-184">İşlev adı.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-184">The function name.</span></span> |

<span data-ttu-id="5cdaa-185">Örneğin, bir JavaScript HTTP tetikleyicisi oluşturmak için çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="5cdaa-185">For example, to create a JavaScript HTTP trigger, run:</span></span>

```
func new --language JavaScript --template HttpTrigger --name MyHttpTrigger
```

<span data-ttu-id="5cdaa-186">Sıra tetiklenen bir işlev oluşturmak için çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="5cdaa-186">To create a queue-triggered function, run:</span></span>

```
func new --language JavaScript --template QueueTrigger --name QueueTriggerJS
```

## <a name="run-functions-locally"></a><span data-ttu-id="5cdaa-187">İşlevler yerel olarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="5cdaa-187">Run functions locally</span></span>

<span data-ttu-id="5cdaa-188">İşlevler proje çalıştırmak için işlevleri konak çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-188">To run a Functions project, run the Functions host.</span></span> <span data-ttu-id="5cdaa-189">Ana bilgisayar için projedeki tüm işlevleri Tetikleyicileri sağlar:</span><span class="sxs-lookup"><span data-stu-id="5cdaa-189">The host enables triggers for all functions in the project:</span></span>

```
func host start
```

<span data-ttu-id="5cdaa-190">`func host start`Aşağıdaki seçenekleri destekler:</span><span class="sxs-lookup"><span data-stu-id="5cdaa-190">`func host start` supports the following options:</span></span>

| <span data-ttu-id="5cdaa-191">Seçenek</span><span class="sxs-lookup"><span data-stu-id="5cdaa-191">Option</span></span>     | <span data-ttu-id="5cdaa-192">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5cdaa-192">Description</span></span>                            |
| ------------ | -------------------------------------- |
|**`--port -p`** | <span data-ttu-id="5cdaa-193">Dinlemenin yapılacağı yerel bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-193">The local port to listen on.</span></span> <span data-ttu-id="5cdaa-194">Varsayılan değer: 7071.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-194">Default value: 7071.</span></span> |
| **`--debug <type>`** | <span data-ttu-id="5cdaa-195">Seçenekler şunlardır: `VSCode` ve `VS`.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-195">The options are `VSCode` and `VS`.</span></span> |
| **`--cors`** | <span data-ttu-id="5cdaa-196">Boşluk CORS çıkış noktası virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-196">A comma-separated list of CORS origins, with no spaces.</span></span> |
| **`--nodeDebugPort -n`** | <span data-ttu-id="5cdaa-197">Kullanmak düğüm hata ayıklayıcı için bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-197">The port for the node debugger to use.</span></span> <span data-ttu-id="5cdaa-198">Varsayılan: Launch.json'u veya 5858 arasında bir değer.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-198">Default: A value from launch.json or 5858.</span></span> |
| **`--debugLevel -d`** | <span data-ttu-id="5cdaa-199">Konsol izleme düzeyini (kapalı, ayrıntılı, bilgi, uyarı veya hata).</span><span class="sxs-lookup"><span data-stu-id="5cdaa-199">The console trace level (off, verbose, info, warning, or error).</span></span> <span data-ttu-id="5cdaa-200">Varsayılan: bilgisi.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-200">Default: Info.</span></span>|
| **`--timeout -t`** | <span data-ttu-id="5cdaa-201">İşlevler konak t o başlangıç, saniye cinsinden zaman aşımı.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-201">The time out for the Functions host t     o start, in seconds.</span></span> <span data-ttu-id="5cdaa-202">Varsayılan: 20 saniye.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-202">Default: 20 seconds.</span></span>|
| **`--useHttps`** | <span data-ttu-id="5cdaa-203">Https://localhost için bağlayın: {port} yerine http://localhost: {port}.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-203">Bind to https://localhost:{port} rather than to http://localhost:{port}.</span></span> <span data-ttu-id="5cdaa-204">Varsayılan olarak, bu seçenek bilgisayarınızda güvenilen bir sertifika oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-204">By default, this option creates a trusted certificate on your computer.</span></span>|
| **`--pause-on-error`** | <span data-ttu-id="5cdaa-205">İşlem çıkmadan önce ek giriş duraklatılıyor.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-205">Pause for additional input before exiting the process.</span></span> <span data-ttu-id="5cdaa-206">Azure işlevleri çekirdek araçları bir tümleşik geliştirme ortamı (IDE) başlatılırken yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-206">Useful when launching Azure Functions Core Tools from an integrated development environment (IDE).</span></span>|

<span data-ttu-id="5cdaa-207">İşlevler ana bilgisayar başladığında, URL, HTTP tetiklemeli işlevleri çıkarır:</span><span class="sxs-lookup"><span data-stu-id="5cdaa-207">When the Functions host starts, it outputs the URL of HTTP-triggered functions:</span></span>

```
Found the following functions:
Host.Functions.MyHttpTrigger

ob host started
Http Function MyHttpTrigger: http://localhost:7071/api/MyHttpTrigger
```

### <a name="debug-in-vs-code-or-visual-studio"></a><span data-ttu-id="5cdaa-208">VS Code'u veya Visual Studio'da hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="5cdaa-208">Debug in VS Code or Visual Studio</span></span>

<span data-ttu-id="5cdaa-209">Bir hata ayıklayıcısı eklemeniz için geçmesi `--debug` bağımsız değişkeni.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-209">To attach a debugger, pass the `--debug` argument.</span></span> <span data-ttu-id="5cdaa-210">JavaScript işlevleri hata ayıklamak için Visual Studio Code kullanın.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-210">To debug JavaScript functions, use Visual Studio Code.</span></span> <span data-ttu-id="5cdaa-211">C# işlevleri için Visual Studio'yu kullanın.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-211">For C# functions, use Visual Studio.</span></span>

<span data-ttu-id="5cdaa-212">C# işlevleri hata ayıklamak için kullanmak `--debug vs`.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-212">To debug C# functions, use `--debug vs`.</span></span> <span data-ttu-id="5cdaa-213">Aynı zamanda [Azure işlevleri Visual Studio 2017 Araçları](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span><span class="sxs-lookup"><span data-stu-id="5cdaa-213">You can also use [Azure Functions Visual Studio 2017 Tools](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span></span> 

<span data-ttu-id="5cdaa-214">Ana bilgisayar'ı başlatın ve JavaScript hata ayıklama kurulumu için çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="5cdaa-214">To launch the host and set up JavaScript debugging, run:</span></span>

```
func host start --debug vscode
```

<span data-ttu-id="5cdaa-215">Ardından, Visual Studio Code içinde **hata ayıklama** görünümü, select **eklemek için Azure işlevleri**.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-215">Then, in Visual Studio Code, in the **Debug** view, select **Attach to Azure Functions**.</span></span> <span data-ttu-id="5cdaa-216">Kesme noktaları ekleme, değişkenleri inceleyin ve kod üzerinden adım.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-216">You can attach breakpoints, inspect variables, and step through code.</span></span>

![Visual Studio Code ile JavaScript hata ayıklama](./media/functions-run-local/vscode-javascript-debugging.png)

### <a name="passing-test-data-to-a-function"></a><span data-ttu-id="5cdaa-218">Bir işlev için test veri geçirme</span><span class="sxs-lookup"><span data-stu-id="5cdaa-218">Passing test data to a function</span></span>

<span data-ttu-id="5cdaa-219">Bir işlev doğrudan kullanarak da çağırabilirsiniz `func run <FunctionName>` ve işlevi için giriş verileri sağlar.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-219">You can also invoke a function directly by using `func run <FunctionName>` and provide input data for the function.</span></span> <span data-ttu-id="5cdaa-220">Bu komut işlevini kullanarak çalıştırmaya benzer **Test** Azure portalında sekmesi.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-220">This command is similar to running a function using the **Test** tab in the Azure portal.</span></span> <span data-ttu-id="5cdaa-221">Bu komut tüm işlevler ana bilgisayarı başlatır.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-221">This command launches the entire Functions host.</span></span>

<span data-ttu-id="5cdaa-222">`func run`Aşağıdaki seçenekleri destekler:</span><span class="sxs-lookup"><span data-stu-id="5cdaa-222">`func run` supports the following options:</span></span>

| <span data-ttu-id="5cdaa-223">Seçenek</span><span class="sxs-lookup"><span data-stu-id="5cdaa-223">Option</span></span>     | <span data-ttu-id="5cdaa-224">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5cdaa-224">Description</span></span>                            |
| ------------ | -------------------------------------- |
| **`--content -c`** | <span data-ttu-id="5cdaa-225">Satır içi içeriği.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-225">Inline content.</span></span> |
| **`--debug -d`** | <span data-ttu-id="5cdaa-226">Bir hata ayıklayıcısı işlevi çalıştırmadan önce ana bilgisayar işleme iliştirilemiyor.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-226">Attach a debugger to the host process before running the function.</span></span>|
| **`--timeout -t`** | <span data-ttu-id="5cdaa-227">Yerel işlevler ana hazır olana kadar (saniye cinsinden) beklenecek süre.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-227">Time to wait (in seconds) until the local Functions host is ready.</span></span>|
| **`--file -f`** | <span data-ttu-id="5cdaa-228">İçerik kullanılacak dosya adı.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-228">The file name to use as content.</span></span>|
| **`--no-interactive`** | <span data-ttu-id="5cdaa-229">Giriş istemez.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-229">Does not prompt for input.</span></span> <span data-ttu-id="5cdaa-230">Otomasyon senaryoları için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-230">Useful for automation scenarios.</span></span>|

<span data-ttu-id="5cdaa-231">Örneğin, bir HTTP tetiklemeli işlevini çağırın ve İçerik gövdesi geçirmek için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="5cdaa-231">For example, to call an HTTP-triggered function and pass content body, run the following command:</span></span>

```
func run MyHttpTrigger -c '{\"name\": \"Azure\"}'
```

## <span data-ttu-id="5cdaa-232"><a name="publish"></a>Azure'a yayımlama</span><span class="sxs-lookup"><span data-stu-id="5cdaa-232"><a name="publish"></a>Publish to Azure</span></span>

<span data-ttu-id="5cdaa-233">Bir işlev uygulaması Azure işlevleri proje yayımlamak için kullanın `publish` komutu:</span><span class="sxs-lookup"><span data-stu-id="5cdaa-233">To publish a Functions project to a function app in Azure, use the `publish` command:</span></span>

```
func azure functionapp publish <FunctionAppName>
```

<span data-ttu-id="5cdaa-234">Aşağıdaki seçenekleri kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5cdaa-234">You can use the following options:</span></span>

| <span data-ttu-id="5cdaa-235">Seçenek</span><span class="sxs-lookup"><span data-stu-id="5cdaa-235">Option</span></span>     | <span data-ttu-id="5cdaa-236">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5cdaa-236">Description</span></span>                            |
| ------------ | -------------------------------------- |
| **`--publish-local-settings -i`** |  <span data-ttu-id="5cdaa-237">Yayımlama ayarları local.settings.json üzerine isteyen Azure içinde ayarı zaten mevcut.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-237">Publish settings in local.settings.json to Azure, prompting to overwrite if the setting already exists.</span></span>|
| **`--overwrite-settings -y`** | <span data-ttu-id="5cdaa-238">İle birlikte kullanılmalıdır `-i`.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-238">Must be used with `-i`.</span></span> <span data-ttu-id="5cdaa-239">Azure AppSettings farklı olması durumunda ile yerel değerin üzerine yazar.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-239">Overwrites AppSettings in Azure with local value if different.</span></span> <span data-ttu-id="5cdaa-240">Komut istemi varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-240">Default is prompt.</span></span>|

<span data-ttu-id="5cdaa-241">`publish` Komutu işlevleri proje dizininin içeriğini yükler.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-241">The `publish` command uploads the contents of the Functions project directory.</span></span> <span data-ttu-id="5cdaa-242">Dosyaları yerel olarak silerseniz `publish` komutu silinmez Azure'dan.</span><span class="sxs-lookup"><span data-stu-id="5cdaa-242">If you delete files locally, the `publish` command does not delete them from Azure.</span></span> <span data-ttu-id="5cdaa-243">Azure dosyaları kullanarak silebilirsiniz [Kudu aracı](functions-how-to-use-azure-function-app-settings.md#kudu) içinde [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="5cdaa-243">You can delete files in Azure by using the [Kudu tool](functions-how-to-use-azure-function-app-settings.md#kudu) in the [Azure portal].</span></span>

## <a name="next-steps"></a><span data-ttu-id="5cdaa-244">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5cdaa-244">Next steps</span></span>

<span data-ttu-id="5cdaa-245">Azure işlevleri çekirdek Araçları [kaynak açın ve GitHub üzerinde barındırılan](https://github.com/azure/azure-functions-cli).</span><span class="sxs-lookup"><span data-stu-id="5cdaa-245">Azure Functions Core Tools is [open source and hosted on GitHub](https://github.com/azure/azure-functions-cli).</span></span>  
<span data-ttu-id="5cdaa-246">Bir hata veya özellik isteği dosyasına [GitHub sorunu açmak](https://github.com/azure/azure-functions-cli/issues).</span><span class="sxs-lookup"><span data-stu-id="5cdaa-246">To file a bug or feature request, [open a GitHub issue](https://github.com/azure/azure-functions-cli/issues).</span></span> 

<!-- LINKS -->

[Azure işlevleri çekirdek Araçları]: https://www.npmjs.com/package/azure-functions-core-tools
[Azure portal]: https://portal.azure.com 
