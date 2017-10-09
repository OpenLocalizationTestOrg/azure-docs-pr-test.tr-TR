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
# <a name="code-and-test-azure-functions-locally"></a>Kod ve yerel olarak Azure işlevlerini test etme

Merhaba sırasında [Azure portal] geliştirmek için Araçlar tam kümesi ve test Azure işlevleri, geliştiricilerin çoğu tercih yerel geliştirme deneyimi sağlar. Azure işlevleri kolay toouse kılar sevdiğiniz Kod Düzenleyicisi'ni ve yerel geliştirme araçları toodevelop ve yerel bilgisayarınızda işlevlerinizi test. İşlevlerinizi Azure olayları tetikleyebilir ve yerel bilgisayarınızda, C# ve JavaScript işlevleri ayıklayabilirsiniz. 

Visual Studio C# Geliştirici, Azure işlevleri de olup olmadığını [Visual Studio 2017 ile tümleşir](functions-develop-vs.md).

## <a name="install-hello-azure-functions-core-tools"></a>Hello Azure işlevleri çekirdek araçlarını yükleme

Azure işlevleri çekirdek araçları, yerel Windows bilgisayarınızda çalıştırabilirsiniz hello Azure işlevleri çalışma zamanı, yerel bir sürümüdür. Bir öykünücü veya benzetici değil. Bunu sahip hello aynı çalışma zamanı bu powers Azure işlevlerinde.

Merhaba [Azure işlevleri çekirdek Araçları] npm paket olarak sağlanır. Öncelikle [NodeJS yükleme](https://docs.npmjs.com/getting-started/installing-node), npm içerir.  

>[!NOTE]
>Şu anda hello Azure işlevleri çekirdek araçları paketini yalnızca Windows bilgisayarlara yüklenebilir. Merhaba işlevleri konaktaki tooa geçici sınırlaması nedeniyle bu kısıtlaması yoktur.

[Azure işlevleri çekirdek Araçları] komut diğer adları aşağıdaki hello ekler:
* **FUNC**
* **azfun**
* **azurefunctions**

Tüm bu diğer adı yerine kullanılabilir `func` bu konudaki hello örnekleri gösterilmektedir.

## <a name="create-a-local-functions-project"></a>Bir yerel işlevler projesi oluşturma

Yerel olarak çalıştırırken, işlevleri proje hello dosyaları host.json ve local.settings.json sahip bir dizindir. Bu dizin olan hello Azure işlevi uygulamada eşdeğeridir. toolearn hello Azure işlevleri klasör yapısı hakkında daha fazla bilgi görmek hello [Azure işlevleri Geliştirici Kılavuzu](functions-reference.md#folder-structure).

Bir komut isteminde hello aşağıdaki komutu çalıştırın:

```
func init MyFunctionProj
```

Merhaba çıktı hello örnek aşağıdaki gibi görünür:

```
Writing .gitignore
Writing host.json
Writing local.settings.json
Created launch.json
Initialized empty Git repository in D:/Code/Playground/MyFunctionProj/.git/
```

bir Git deposu, kullanım hello seçeneği oluşturma dışında tooopt `--no-source-control [-n]`.

<a name="local-settings"></a>

## <a name="local-settings-file"></a>Yerel ayarlar dosyası

Uygulama ayarları, bağlantı dizeleri ve ayarları için Azure işlevleri çekirdek araçları Hello dosya local.settings.json depolar. Yapı izlenerek hello sahiptir:

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
| **Isencrypted** | Ayarlandığında çok**doğru**, tüm değerleri yerel makine anahtarı kullanılarak şifrelenir. İle kullanılan `func settings` komutları. Varsayılan değer **false**. |
| **Değerleri** | Uygulama ayarlarını yerel olarak çalıştırırken kullanılan koleksiyonu. Uygulama ayarları toothis nesnenizin ekleyin.  |
| **AzureWebJobsStorage** | Ayarlar, bağlantı dizesi toohello hello Azure işlevleri çalışma zamanı tarafından dahili olarak kullanılır Azure depolama hesabı hello. Merhaba depolama hesabı, işlevin Tetikleyicileri destekler. Bu depolama hesabı bağlantı ayarı tetiklenen HTTP işlevler hariç tüm işlevleri için gereklidir.  |
| **AzureWebJobsDashboard** | Kullanılan toostore hello işlev günlükleri olan hello bağlantı dizesi toohello Azure depolama hesabı ayarlar. Bu isteğe bağlı değeri hello günlükleri hello Portalı'nda erişilebilir hale getirir.|
| **Ana bilgisayar** | Bu bölümdeki ayarlarını hello işlevleri ana bilgisayar işlemi yerel olarak çalıştırırken özelleştirin. | 
| **LocalHttpPort** | Ayarlar hello hello yerel işlevler ana çalıştırırken kullanılan varsayılan bağlantı noktası (`func host start` ve `func run`). Merhaba `--port` komut satırı seçeneği bu değerin üzerine göre önceliklidir. |
| **CORS** | İzin verilen hello kaynakları tanımlayan [çıkış noktaları arası kaynak paylaşımı (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing). Çıkış boşluk virgülle ayrılmış bir liste olarak sağlanır. Merhaba joker karakter değeri (**\***) desteklenir, her türlü kaynağa gelen isteklere izin verir. |
| **ConnectionStrings** | İşlevlerinizi için Hello veritabanı bağlantı dizelerini içerir. Bu nesne bağlantı dizeleri hello sağlayıcısı türü toohello ortamıyla eklenen **System.Data.SqlClient**.  | 

Çoğu Tetikleyicileri ve bağlamaları sahip bir **bağlantı** ortam değişkeni veya uygulama ayarını toohello adı eşlemeleri özelliği. Her bağlantı özelliği için uygulama ayarı local.settings.json dosyasında tanımlanmış olmalıdır. 

Bu ayarlar, ortam değişkenleri olarak kodunuzda de okunabilir. C# ' ta kullanmak [System.Environment.GetEnvironmentVariable](https://msdn.microsoft.com/library/system.environment.getenvironmentvariable(v=vs.110).aspx) veya [ConfigurationManager.AppSettings](https://msdn.microsoft.com/library/system.configuration.configurationmanager.appsettings%28v=vs.110%29.aspx). JavaScript'te, kullanmak `process.env`. Sistem ortam değişkeni olarak belirtilen ayarları hello local.settings.json dosyasındaki değerleri daha önceliklidir. 

Merhaba local.settings.json dosyasındaki ayarları, yalnızca yerel olarak çalıştırırken işlevleri araçları tarafından kullanılır. Merhaba proje yayımlanan tooAzure olduğunda varsayılan olarak, bu ayarlar otomatik olarak geçirilmez. Kullanım hello `--publish-local-settings` geçiş [yayımladığınızda](#publish) toomake emin bu ayarlar, Azure'da toohello işlev uygulaması eklenir.

İçin hiç geçerli bir depolama bağlantı dizesi ayarlandığında **AzureWebJobsStorage**, aşağıdaki hata iletisini hello gösterilir:  

>Local.settings.json eksik değeri AzureWebJobsStorage için. Bu, HTTP dışındaki tüm tetikleyiciler için gereklidir. Çalıştırabilirsiniz ' func azure functionary fetch-app-settings <functionAppName>' veya local.settings.json içinde bir bağlantı dizesini belirtin.
  
[!INCLUDE [Note toonot use local storage](../../includes/functions-local-settings-note.md)]

### <a name="configure-app-settings"></a>Uygulama ayarlarını yapılandırma

bağlantı dizeleri için bir değer tooset hello aşağıdakilerden birini yapabilirsiniz:
* Merhaba bağlantı dizesinden girin [Azure Storage Gezgini](http://storageexplorer.com/).
* Aşağıdaki komutları hello birini kullanın:

    ```
    func azure functionapp fetch-app-settings <FunctionAppName>
    ```
    ```
    func azure functionapp storage fetch-connection-string <StorageAccountName>
    ```
    Her iki komutlar, toofirst oturum açma tooAzure gerektirir.

## <a name="create-a-function"></a>İşlev oluşturma

bir işlev toocreate hello aşağıdaki komutu çalıştırın:

```
func new
``` 
`func new`İsteğe bağlı bağımsız değişkenler aşağıdaki hello destekler:

| Bağımsız değişken     | Açıklama                            |
| ------------ | -------------------------------------- |
| **`--language -l`** | programlama dili C#, F # ve JavaScript gibi hello şablonu. |
| **`--template -t`** | Merhaba şablon adı. |
| **`--name -n`** | Merhaba işlev adı. |

Çalıştırma gibi toocreate bir JavaScript HTTP tetikleyici:

```
func new --language JavaScript --template HttpTrigger --name MyHttpTrigger
```

toocreate sıra tetiklenen bir işlev çalıştırın:

```
func new --language JavaScript --template QueueTrigger --name QueueTriggerJS
```

## <a name="run-functions-locally"></a>İşlevler yerel olarak çalıştırma

toorun işlevleri proje Hello işlevleri konak çalıştırın. Merhaba konak hello projedeki tüm işlevler için Tetikleyicileri sağlar:

```
func host start
```

`func host start`Seçenekler aşağıdaki hello destekler:

| Seçenek     | Açıklama                            |
| ------------ | -------------------------------------- |
|**`--port -p`** | Merhaba yerel bağlantı noktası toolisten üzerinde. Varsayılan değer: 7071. |
| **`--debug <type>`** | Başlangıç Seçenekleri `VSCode` ve `VS`. |
| **`--cors`** | Boşluk CORS çıkış noktası virgülle ayrılmış listesi. |
| **`--nodeDebugPort -n`** | Merhaba düğümü hata ayıklayıcı toouse için başlangıç bağlantı noktası. Varsayılan: Launch.json'u veya 5858 arasında bir değer. |
| **`--debugLevel -d`** | Merhaba konsol izleme düzeyini (kapalı, ayrıntılı, bilgi, uyarı veya hata). Varsayılan: bilgisi.|
| **`--timeout -t`** | Merhaba işlevleri konak t o başlangıç, saniye cinsinden Hello zaman aşımına uğradı. Varsayılan: 20 saniye.|
| **`--useHttps`** | Toohttps://localhost bağlayın: {bağlantı noktası} toohttp://localhost yerine: {port}. Varsayılan olarak, bu seçenek bilgisayarınızda güvenilen bir sertifika oluşturur.|
| **`--pause-on-error`** | Merhaba işlem çıkmadan önce ek giriş duraklatılıyor. Azure işlevleri çekirdek araçları bir tümleşik geliştirme ortamı (IDE) başlatılırken yararlıdır.|

Merhaba işlevleri ana bilgisayar başlatıldığında hello URL, HTTP tetiklemeli işlevleri çıkarır:

```
Found hello following functions:
Host.Functions.MyHttpTrigger

ob host started
Http Function MyHttpTrigger: http://localhost:7071/api/MyHttpTrigger
```

### <a name="debug-in-vs-code-or-visual-studio"></a>VS Code'u veya Visual Studio'da hata ayıklama

tooattach bir hata ayıklayıcısı geçirmek hello `--debug` bağımsız değişkeni. toodebug JavaScript işlevleri, Visual Studio Code kullanın. C# işlevleri için Visual Studio'yu kullanın.

toodebug C# işlevlerini kullanmak `--debug vs`. Aynı zamanda [Azure işlevleri Visual Studio 2017 Araçları](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/). 

toolaunch hello konak ve JavaScript hata ayıklama, yedekleme kümesi çalıştırın:

```
func host start --debug vscode
```

Ardından Visual Studio Code hello **hata ayıklama** görünümü, select **Attach tooAzure işlevler**. Kesme noktaları ekleme, değişkenleri inceleyin ve kod üzerinden adım.

![Visual Studio Code ile JavaScript hata ayıklama](./media/functions-run-local/vscode-javascript-debugging.png)

### <a name="passing-test-data-tooa-function"></a>Geçirme test veri tooa işlevi

Bir işlev doğrudan kullanarak da çağırabilirsiniz `func run <FunctionName>` ve hello işlevi için giriş verileri sağlar. Bu komut benzer toorunning hello kullanarak bir işlevdir **Test** hello Azure portal sekmesindedir. Bu komut hello tüm işlevler konak başlatır.

`func run`Seçenekler aşağıdaki hello destekler:

| Seçenek     | Açıklama                            |
| ------------ | -------------------------------------- |
| **`--content -c`** | Satır içi içeriği. |
| **`--debug -d`** | Hata ayıklayıcı toohello ana bilgisayar işlemi hello işlevi çalıştırmadan önce ekleyin.|
| **`--timeout -t`** | Merhaba yerel işlevler ana kadar zaman toowait (saniye cinsinden) hazırdır.|
| **`--file -f`** | Dosya adı toouse içeriği olarak hello.|
| **`--no-interactive`** | Giriş istemez. Otomasyon senaryoları için kullanışlıdır.|

Örneğin, toocall bir HTTP tetiklemeli işlevin ve geçişi İçerik gövdesi, hello aşağıdaki komutu çalıştırın:

```
func run MyHttpTrigger -c '{\"name\": \"Azure\"}'
```

## <a name="publish"></a>TooAzure yayımlama

toopublish işlevleri proje tooa işlev uygulaması Azure, kullanım hello `publish` komutu:

```
func azure functionapp publish <FunctionAppName>
```

Hello aşağıdaki seçenekleri kullanabilirsiniz:

| Seçenek     | Açıklama                            |
| ------------ | -------------------------------------- |
| **`--publish-local-settings -i`** |  Yayımlama hello ayarı zaten varsa toooverwrite isteyen local.settings.json tooAzure içinde ayarları.|
| **`--overwrite-settings -y`** | İle birlikte kullanılmalıdır `-i`. Azure AppSettings farklı olması durumunda ile yerel değerin üzerine yazar. Komut istemi varsayılandır.|

Merhaba `publish` komutu hello hello işlevleri proje dizininin içeriğini yükler. Dosyaları yerel olarak silerseniz, hello `publish` komutu silinmez Azure'dan. Hello kullanarak Azure dosyaları silebilirsiniz [Kudu aracı](functions-how-to-use-azure-function-app-settings.md#kudu) hello içinde [Azure portal].

## <a name="next-steps"></a>Sonraki adımlar

Azure işlevleri çekirdek Araçları [kaynak açın ve GitHub üzerinde barındırılan](https://github.com/azure/azure-functions-cli).  
bir hata veya özellik isteği toofile [GitHub sorunu açmak](https://github.com/azure/azure-functions-cli/issues). 

<!-- LINKS -->

[Azure işlevleri çekirdek Araçları]: https://www.npmjs.com/package/azure-functions-core-tools
[Azure portal]: https://portal.azure.com 
