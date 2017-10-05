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
# <a name="code-and-test-azure-functions-locally"></a>Kod ve yerel olarak Azure işlevlerini test etme

Sırada [Azure portal] geliştirmek için Araçlar tam kümesi ve test Azure işlevleri, geliştiricilerin çoğu tercih yerel geliştirme deneyimi sağlar. Azure işlevleri geliştirmek ve yerel bilgisayarınızda işlevlerinizi test etmek için sık kullanılan kod düzenleyicisini ve yerel geliştirme araçları kullanın kolaylaştırır. İşlevlerinizi Azure olayları tetikleyebilir ve yerel bilgisayarınızda, C# ve JavaScript işlevleri ayıklayabilirsiniz. 

Visual Studio C# Geliştirici, Azure işlevleri de olup olmadığını [Visual Studio 2017 ile tümleşir](functions-develop-vs.md).

## <a name="install-the-azure-functions-core-tools"></a>Azure işlevleri çekirdek Araçları'nı yükleme

Azure işlevleri çekirdek araçları, yerel Windows bilgisayarınızda çalıştırabilirsiniz Azure işlevleri çalışma zamanı, yerel bir sürümüdür. Bir öykünücü veya benzetici değil. Powers Azure işlevleri çalışma zamanı olur.

[Azure işlevleri çekirdek Araçları] npm paket olarak sağlanır. Öncelikle [NodeJS yükleme](https://docs.npmjs.com/getting-started/installing-node), npm içerir.  

>[!NOTE]
>Şu anda Azure işlevleri çekirdek araçları paketini yalnızca Windows bilgisayarlara yüklenebilir. İşlevler konakta geçici bir sınırlama nedeniyle bu kısıtlaması yoktur.

[Azure işlevleri çekirdek Araçları] aşağıdaki komut diğer adları ekler:
* **FUNC**
* **azfun**
* **azurefunctions**

Tüm bu diğer adı yerine kullanılabilir `func` bu konudaki örnekler gösterilmektedir.

## <a name="create-a-local-functions-project"></a>Bir yerel işlevler projesi oluşturma

Yerel olarak çalıştırırken, işlevleri proje dosyalarını host.json ve local.settings.json sahip bir dizindir. Bu dizinde bir işlev uygulaması Azure eşdeğeridir. Azure işlevleri klasör yapısı hakkında daha fazla bilgi için bkz: [Azure işlevleri Geliştirici Kılavuzu](functions-reference.md#folder-structure).

Bir komut isteminde aşağıdaki komutu çalıştırın:

```
func init MyFunctionProj
```

Çıktı aşağıdaki gibi görünür:

```
Writing .gitignore
Writing host.json
Writing local.settings.json
Created launch.json
Initialized empty Git repository in D:/Code/Playground/MyFunctionProj/.git/
```

Git deposu oluşturuluyor dışında kabul etmek için seçeneği kullanın. `--no-source-control [-n]`.

<a name="local-settings"></a>

## <a name="local-settings-file"></a>Yerel ayarlar dosyası

Dosya local.settings.json uygulama ayarları, bağlantı dizeleri ve Azure işlevleri çekirdek araçları ayarlarını saklar. Aşağıdaki yapı vardır:

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
| Ayar      | Açıklama                            |
| ------------ | -------------------------------------- |
| **Isencrypted** | Ayarlandığında **doğru**, tüm değerleri yerel makine anahtarı kullanılarak şifrelenir. İle kullanılan `func settings` komutları. Varsayılan değer **false**. |
| **Değerleri** | Uygulama ayarlarını yerel olarak çalıştırırken kullanılan koleksiyonu. Bu nesne için uygulamanızın ayarlarını ekleyin.  |
| **AzureWebJobsStorage** | Azure işlevleri çalışma zamanı tarafından dahili olarak kullanılır Azure depolama hesabı bağlantı dizesini ayarlar. Depolama hesabı, işlevin Tetikleyicileri destekler. Bu depolama hesabı bağlantı ayarı tetiklenen HTTP işlevler hariç tüm işlevleri için gereklidir.  |
| **AzureWebJobsDashboard** | İşlev günlükleri depolamak için kullanılan Azure depolama hesabı bağlantı dizesini ayarlar. Bu isteğe bağlı değeri günlükleri Portalı'nda erişilebilir hale getirir.|
| **Ana bilgisayar** | Bu bölümdeki ayarlarını işlevleri ana bilgisayar işlemi yerel olarak çalıştırırken özelleştirin. | 
| **LocalHttpPort** | Yerel işlevler ana çalıştırırken kullanılan varsayılan bağlantı noktasını ayarlar (`func host start` ve `func run`). `--port` Komut satırı seçeneği bu değerin üzerine göre önceliklidir. |
| **CORS** | İzin verilen çıkış noktası tanımlar [çıkış noktaları arası kaynak paylaşımı (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing). Çıkış boşluk virgülle ayrılmış bir liste olarak sağlanır. Joker karakter değeri (**\***) desteklenir, her türlü kaynağa gelen isteklere izin verir. |
| **ConnectionStrings** | İşlevlerinizi için veritabanı bağlantı dizelerini içerir. Bu nesne bağlantı dizeleri, sağlayıcı türü ortamıyla eklenir **System.Data.SqlClient**.  | 

Çoğu Tetikleyicileri ve bağlamaları sahip bir **bağlantı** bir ortam değişkeni veya uygulama ayarı adı için eşleşen özellik. Her bağlantı özelliği için uygulama ayarı local.settings.json dosyasında tanımlanmış olmalıdır. 

Bu ayarlar, ortam değişkenleri olarak kodunuzda de okunabilir. C# ' ta kullanmak [System.Environment.GetEnvironmentVariable](https://msdn.microsoft.com/library/system.environment.getenvironmentvariable(v=vs.110).aspx) veya [ConfigurationManager.AppSettings](https://msdn.microsoft.com/library/system.configuration.configurationmanager.appsettings%28v=vs.110%29.aspx). JavaScript'te, kullanmak `process.env`. Sistem ortam değişkeni olarak belirtilen ayarları local.settings.json dosyasındaki değerleri daha önceliklidir. 

Local.settings.json dosyasındaki ayarları, yalnızca yerel olarak çalıştırırken işlevleri araçları tarafından kullanılır. Projeyi Azure'a yayımlandığında varsayılan olarak, bu ayarlar otomatik olarak geçirilmez. Kullanım `--publish-local-settings` geçiş [yayımladığınızda](#publish) bu ayarlar, azure'da işlev uygulaması eklenir emin olmak için.

İçin hiç geçerli bir depolama bağlantı dizesi ayarlandığında **AzureWebJobsStorage**, aşağıdaki hata iletisi gösterilir:  

>Local.settings.json eksik değeri AzureWebJobsStorage için. Bu, HTTP dışındaki tüm tetikleyiciler için gereklidir. Çalıştırabilirsiniz ' func azure functionary fetch-app-settings <functionAppName>' veya local.settings.json içinde bir bağlantı dizesini belirtin.
  
[!INCLUDE [Note to not use local storage](../../includes/functions-local-settings-note.md)]

### <a name="configure-app-settings"></a>Uygulama ayarlarını yapılandırma

Bağlantı dizeleri için bir değer ayarlamak için aşağıdakilerden birini yapabilirsiniz:
* Bağlantı dizesi girin [Azure Storage Gezgini](http://storageexplorer.com/).
* Aşağıdaki komutlardan birini kullanın:

    ```
    func azure functionapp fetch-app-settings <FunctionAppName>
    ```
    ```
    func azure functionapp storage fetch-connection-string <StorageAccountName>
    ```
    Her iki komutlar için ilk oturum açma Azure gerektirir.

## <a name="create-a-function"></a>İşlev oluşturma

Bir işlev oluşturmak için aşağıdaki komutu çalıştırın:

```
func new
``` 
`func new`Aşağıdaki isteğe bağlı bağımsız değişkenler destekler:

| Bağımsız değişken     | Açıklama                            |
| ------------ | -------------------------------------- |
| **`--language -l`** | Dil C#, F # ve JavaScript gibi programlama şablonu. |
| **`--template -t`** | Şablon adı. |
| **`--name -n`** | İşlev adı. |

Örneğin, bir JavaScript HTTP tetikleyicisi oluşturmak için çalıştırın:

```
func new --language JavaScript --template HttpTrigger --name MyHttpTrigger
```

Sıra tetiklenen bir işlev oluşturmak için çalıştırın:

```
func new --language JavaScript --template QueueTrigger --name QueueTriggerJS
```

## <a name="run-functions-locally"></a>İşlevler yerel olarak çalıştırma

İşlevler proje çalıştırmak için işlevleri konak çalıştırın. Ana bilgisayar için projedeki tüm işlevleri Tetikleyicileri sağlar:

```
func host start
```

`func host start`Aşağıdaki seçenekleri destekler:

| Seçenek     | Açıklama                            |
| ------------ | -------------------------------------- |
|**`--port -p`** | Dinlemenin yapılacağı yerel bağlantı noktası. Varsayılan değer: 7071. |
| **`--debug <type>`** | Seçenekler şunlardır: `VSCode` ve `VS`. |
| **`--cors`** | Boşluk CORS çıkış noktası virgülle ayrılmış listesi. |
| **`--nodeDebugPort -n`** | Kullanmak düğüm hata ayıklayıcı için bağlantı noktası. Varsayılan: Launch.json'u veya 5858 arasında bir değer. |
| **`--debugLevel -d`** | Konsol izleme düzeyini (kapalı, ayrıntılı, bilgi, uyarı veya hata). Varsayılan: bilgisi.|
| **`--timeout -t`** | İşlevler konak t o başlangıç, saniye cinsinden zaman aşımı. Varsayılan: 20 saniye.|
| **`--useHttps`** | Https://localhost için bağlayın: {port} yerine http://localhost: {port}. Varsayılan olarak, bu seçenek bilgisayarınızda güvenilen bir sertifika oluşturur.|
| **`--pause-on-error`** | İşlem çıkmadan önce ek giriş duraklatılıyor. Azure işlevleri çekirdek araçları bir tümleşik geliştirme ortamı (IDE) başlatılırken yararlıdır.|

İşlevler ana bilgisayar başladığında, URL, HTTP tetiklemeli işlevleri çıkarır:

```
Found the following functions:
Host.Functions.MyHttpTrigger

ob host started
Http Function MyHttpTrigger: http://localhost:7071/api/MyHttpTrigger
```

### <a name="debug-in-vs-code-or-visual-studio"></a>VS Code'u veya Visual Studio'da hata ayıklama

Bir hata ayıklayıcısı eklemeniz için geçmesi `--debug` bağımsız değişkeni. JavaScript işlevleri hata ayıklamak için Visual Studio Code kullanın. C# işlevleri için Visual Studio'yu kullanın.

C# işlevleri hata ayıklamak için kullanmak `--debug vs`. Aynı zamanda [Azure işlevleri Visual Studio 2017 Araçları](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/). 

Ana bilgisayar'ı başlatın ve JavaScript hata ayıklama kurulumu için çalıştırın:

```
func host start --debug vscode
```

Ardından, Visual Studio Code içinde **hata ayıklama** görünümü, select **eklemek için Azure işlevleri**. Kesme noktaları ekleme, değişkenleri inceleyin ve kod üzerinden adım.

![Visual Studio Code ile JavaScript hata ayıklama](./media/functions-run-local/vscode-javascript-debugging.png)

### <a name="passing-test-data-to-a-function"></a>Bir işlev için test veri geçirme

Bir işlev doğrudan kullanarak da çağırabilirsiniz `func run <FunctionName>` ve işlevi için giriş verileri sağlar. Bu komut işlevini kullanarak çalıştırmaya benzer **Test** Azure portalında sekmesi. Bu komut tüm işlevler ana bilgisayarı başlatır.

`func run`Aşağıdaki seçenekleri destekler:

| Seçenek     | Açıklama                            |
| ------------ | -------------------------------------- |
| **`--content -c`** | Satır içi içeriği. |
| **`--debug -d`** | Bir hata ayıklayıcısı işlevi çalıştırmadan önce ana bilgisayar işleme iliştirilemiyor.|
| **`--timeout -t`** | Yerel işlevler ana hazır olana kadar (saniye cinsinden) beklenecek süre.|
| **`--file -f`** | İçerik kullanılacak dosya adı.|
| **`--no-interactive`** | Giriş istemez. Otomasyon senaryoları için kullanışlıdır.|

Örneğin, bir HTTP tetiklemeli işlevini çağırın ve İçerik gövdesi geçirmek için aşağıdaki komutu çalıştırın:

```
func run MyHttpTrigger -c '{\"name\": \"Azure\"}'
```

## <a name="publish"></a>Azure'a yayımlama

Bir işlev uygulaması Azure işlevleri proje yayımlamak için kullanın `publish` komutu:

```
func azure functionapp publish <FunctionAppName>
```

Aşağıdaki seçenekleri kullanabilirsiniz:

| Seçenek     | Açıklama                            |
| ------------ | -------------------------------------- |
| **`--publish-local-settings -i`** |  Yayımlama ayarları local.settings.json üzerine isteyen Azure içinde ayarı zaten mevcut.|
| **`--overwrite-settings -y`** | İle birlikte kullanılmalıdır `-i`. Azure AppSettings farklı olması durumunda ile yerel değerin üzerine yazar. Komut istemi varsayılandır.|

`publish` Komutu işlevleri proje dizininin içeriğini yükler. Dosyaları yerel olarak silerseniz `publish` komutu silinmez Azure'dan. Azure dosyaları kullanarak silebilirsiniz [Kudu aracı](functions-how-to-use-azure-function-app-settings.md#kudu) içinde [Azure portal].

## <a name="next-steps"></a>Sonraki adımlar

Azure işlevleri çekirdek Araçları [kaynak açın ve GitHub üzerinde barındırılan](https://github.com/azure/azure-functions-cli).  
Bir hata veya özellik isteği dosyasına [GitHub sorunu açmak](https://github.com/azure/azure-functions-cli/issues). 

<!-- LINKS -->

[Azure işlevleri çekirdek Araçları]: https://www.npmjs.com/package/azure-functions-core-tools
[Azure portal]: https://portal.azure.com 
