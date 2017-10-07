---
title: "Azure anahtar kasası yukarı aaaSet uçtan uca anahtar döndürme ve Denetim ile | Microsoft Docs"
description: "Anahtar rotasyonu ve izleme anahtar kasası günlükleri ayarlamak bu nasıl tootoohelp kullanın."
services: key-vault
documentationcenter: 
author: swgriffith
manager: mbaldwin
tags: 
ms.assetid: 9cd7e15e-23b8-41c0-a10a-06e6207ed157
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: jodehavi;stgriffi
ms.openlocfilehash: e0c393873077e3b91adc9fa7f39128bc1b6abe26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-azure-key-vault-with-end-to-end-key-rotation-and-auditing"></a>Azure Anahtar Kasası’nı uçtan uca döndürme ve denetleme ile ayarlama
## <a name="introduction"></a>Giriş
Anahtar kasası oluşturduktan sonra o kasa toostore anahtarları ve gizli anahtarları kullanarak mümkün toostart olacaktır. Uygulamalarınızı artık toopersist anahtar veya gizli gerekir, ancak bunun yerine bunları hello anahtar Kasası'nı gerektiğinde isteyecek. Bu, tooupdate anahtarlar ve gizli anahtarı ve gizli yönetim olanakları derecesini açar uygulamanızın hello davranışını etkilemeden sağlar.

Bu makalede Azure anahtar kasası toostore kullanma örneği bu durumda, bir uygulama tarafından erişilebilen bir Azure depolama hesabı anahtarı bir gizlilik anlatılmaktadır. Ayrıca, bu depolama hesabı anahtarı zamanlanmış dönüşünü uyarlamasını gösterir. Son olarak, nasıl toomonitor anahtar kasası denetim günlüklerini hello ve beklenmeyen istekler yapıldığında uyarı verileceğini Tanıtımı anlatılmaktadır.

> [!NOTE]
> Bu öğretici hedeflenen tooexplain ayrıntı hello ilk kurulumunda anahtar kasanızı değil. Bu bilgi için bkz. [Azure Anahtar Kasası ile çalışmaya başlama](key-vault-get-started.md). Platformlar arası komut satırı arabirimi yönergeleri için bkz: [anahtar kasası CLI kullanarak yönetme](key-vault-manage-with-cli2.md).
>
>

## <a name="set-up-key-vault"></a>Anahtar Kasası ayarlama
tooenable uygulama tooretrieve bir gizli anahtar Kasası'nı öncelikle hello gizli anahtar oluşturma ve tooyour kasası karşıya yükleyin. Bu, bir Azure PowerShell oturumu başlatarak ve tooyour içinde Azure hesabı komutu aşağıdaki hello ile imzalama gerçekleştirilebilir:

```powershell
Login-AzureRmAccount
```

Merhaba açılır tarayıcı penceresinde Azure hesabı kullanıcı adınızı ve parolanızı girin. PowerShell Bu hesapla ilişkili tüm hello abonelikleri alır. PowerShell kullanan varsayılan olarak birinci hello.

Birden çok aboneliğiniz varsa, kullanılan toocreate olan bir anahtar kasanızı hello toospecify olabilir. Hesabınız için toosee hello abonelikleri aşağıdaki hello girin:

```powershell
Get-AzureRmSubscription
```

günlüğünü tutacağınız, hello anahtar kasasıyla ilişkili toospecify hello abonelik girin:

```powershell
Set-AzureRmContext -SubscriptionId <subscriptionID>
```

Bu makalede, bir depolama hesabı anahtarı gizli depolama gösterilmektedir olduğundan, bu depolama hesabı anahtarı edinmeniz gerekir.

```powershell
Get-AzureRmStorageAccountKey -ResourceGroupName <resourceGroupName> -Name <storageAccountName>
```

Gizli (Bu durumda, depolama hesabı anahtarınızı) aldıktan sonra o tooa güvenli dize dönüştürme ve anahtar kasanızı'da bu değerle bir gizli anahtar oluşturmanız gerekir.

```powershell
$secretvalue = ConvertTo-SecureString <storageAccountKey> -AsPlainText -Force

Set-AzureKeyVaultSecret -VaultName <vaultName> -Name <secretName> -SecretValue $secretvalue
```
Ardından, oluşturduğunuz hello gizliliğini hello URI alın. Gizli hello anahtar kasası tooretrieve çağırdığınızda bu bir sonraki adımda kullanılır. Merhaba aşağıdaki PowerShell komutunu çalıştırın ve hello parolası URI hello kimliği değeri not edin:

```powershell
Get-AzureKeyVaultSecret –VaultName <vaultName>
```

## <a name="set-up-hello-application"></a>Merhaba uygulama ayarlama
Depolanan gizli sahip olduğunuza göre kod tooretrieve kullanın ve bunu kullanın. Vardır birkaç adımları gerekli tooachieve bu. Hello ilk ve en önemli adım Azure Active Directory ile uygulamanızı kaydetme ve böylece uygulamanız gelen istekleri izin verebilir anahtar kasası, uygulama bilgilerinizi belirtiyor.

> [!NOTE]
> Uygulamanızın üzerinde hello aynı oluşturulmalıdır anahtar kasanızı olarak Azure Active Directory kiracısı.
>
>

Azure Active Directory Hello uygulamalar sekmesini açın.

![Azure Active Directory'de açık uygulamalar](./media/keyvault-keyrotation/AzureAD_Header.png)

Seçin **ekleme** tooadd uygulama tooyour Azure Active Directory.

![EKLE'yi seçin](./media/keyvault-keyrotation/Azure_AD_AddApp.png)

Merhaba uygulama türü olarak bırakın **WEB uygulaması ve/veya WEB API** ve uygulamanızı bir ad verin.

![Ad Merhaba uygulaması](./media/keyvault-keyrotation/AzureAD_NewApp1.png)

Uygulamanızı vermek bir **oturum açma URL** ve bir **uygulama kimliği URI'si**. Bunlar bu tanıtım için istediğiniz herhangi bir şey olabilir ve bunlar daha sonra gerekirse değiştirilebilir.

![Gerekli URI'ler sağlar](./media/keyvault-keyrotation/AzureAD_NewApp2.png)

Merhaba uygulaması tooAzure Active Directory eklendikten sonra hello uygulama sayfasına gidersiniz. Merhaba tıklatın **yapılandırma** sekmesini ve ardından bulmak ve kopyalama hello **istemci kimliği** değeri. Sonraki adımlar için hello istemci Kimliğini not edin.

Ardından, Azure Active Directory ile etkileşim kurabilmesi uygulamanız için bir anahtar oluşturun. Bu altında hello oluşturabilir **anahtarları** hello bölümünde **yapılandırma** sekmesi. Bir sonraki adımda kullanmak için Azure Active Directory uygulamanızdan hello yeni oluşturulan anahtarı not edin.

![Azure Active Directory uygulama anahtarları](./media/keyvault-keyrotation/Azure_AD_AppKeys.png)

Merhaba anahtar kasası uygulamanıza gelen tüm çağrıları oluşturmadan önce uygulamanızı ve izinlerini hakkında hello anahtar kasası söylemelisiniz. Merhaba aşağıdaki komutu hello kasa adı ve hello istemci kimliği verir ve Azure Active Directory Uygulama alır **almak** hello uygulama için erişim tooyour anahtar kasası.

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <vaultName> -ServicePrincipalName <clientIDfromAzureAD> -PermissionsToSecrets Get
```

Bu noktada, uygulama çağrılarınızı oluşturmaya hazır toostart var. Uygulamanızda Azure anahtar kasası ve Azure Active Directory ile Merhaba NuGet paketleri gerekli toointeract yüklemeniz gerekir. Merhaba Visual Studio Paket Yöneticisi Konsolu'ndan komutları aşağıdaki hello girin. Tooconfirm hello en son sürümünü istediğiniz ve uygun şekilde güncelleştirmek için bu makalenin hello yazıda hello geçerli hello Azure Active Directory paket 3.10.305231913, sürümüdür.

```powershell
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 3.10.305231913

Install-Package Microsoft.Azure.KeyVault
```

Uygulama kodunuz, Azure Active Directory kimlik doğrulaması için bir sınıf toohold hello yöntemi oluşturun. Bu örnekte, o sınıfın adlı **yardımcı programları**. Merhaba aşağıdaki ekleme deyimini kullanarak:

```csharp
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

Ardından, Azure Active Directory'den yöntemi tooretrieve hello JWT belirteci aşağıdaki hello ekleyin. Bakım için web ya da uygulama yapılandırmanızı toomove hello sabit kodlanmış dize değerlerini isteyebilirsiniz.

```csharp
public async static Task<string> GetToken(string authority, string resource, string scope)
{
    var authContext = new AuthenticationContext(authority);

    ClientCredential clientCred = new ClientCredential("<AzureADApplicationClientID>","<AzureADApplicationClientKey>");

    AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

    if (result == null)

    throw new InvalidOperationException("Failed tooobtain hello JWT token");

    return result.AccessToken;
}
```

Merhaba gerekli kodu toocall anahtar kasası ekleme ve gizli değer alma. İlk hello aşağıdakileri ekleyin deyimi kullanarak:

```csharp
using Microsoft.Azure.KeyVault;
```

Merhaba yöntemi çağrıları tooinvoke anahtar kasası ekleme ve gizli anahtarı alma. Bu yöntemde hello gizli bir önceki adımda kaydettiğiniz URI sağlayın. Not hello hello **GetToken** hello yönteminden **yardımcı programları** daha önce oluşturduğunuz sınıfı.

```csharp
var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

var sec = kv.GetSecretAsync(<SecretID>).Result.Value;
```

Uygulamanızı çalıştırdığınızda, şimdi tooAzure Active Directory ve sonra gizli değer Azure anahtar Kasası'alma kimlik doğrulaması.

## <a name="key-rotation-using-azure-automation"></a>Azure otomasyonu kullanarak anahtar döndürme
Değerleri Azure anahtar kasası gizlilikleri olarak depolamak için bir dönüş stratejisi uygulamaya yönelik çeşitli seçenekleriniz vardır. El ile işleminin bir parçası gizli döndürülüp, bunlar program aracılığıyla API çağrılarını kullanarak döndürülüp ya da bir otomasyon komut dosyası aracılığıyla Döndürülmüş. Bu makalede Hello amaçları doğrultusunda, siz olacaksınız bir Azure depolama hesabı erişim tuşu birleştirilmiş Azure Otomasyonu toochange ile Azure PowerShell'i kullanma. Ardından bu yeni anahtarla bir anahtar kasası gizli anahtarı güncelleştirir.

tooallow Azure Otomasyonu tooset gizli değer anahtar kasanızı hello istemci kimliği, Azure Automation örneğiyle oluşturulduğu AzureRunAsConnection adlı hello bağlantısı için almanız gerekir. Bu kimliği seçerek bulabileceğiniz **varlıklar** , Azure Automation örneğinden. Buradan, seçtiğiniz **bağlantıları** seçip hello **AzureRunAsConnection** hizmet ilkesi. Merhaba not edin **uygulama kimliği**.

![Azure otomasyon istemci kimliği](./media/keyvault-keyrotation/Azure_Automation_ClientID.png)

İçinde **varlıklar**, seçin **modülleri**. Gelen **modülleri**seçin **galeri**, arayın ve sonra ve **alma** güncelleştirilmiş sürümlerini her bir modül aşağıdaki hello:

    Azure
    Azure.Storage
    AzureRM.Profile
    AzureRM.KeyVault
    AzureRM.Automation
    AzureRM.Storage


> [!NOTE]
> Bu makalenin Hello yazıda yalnızca hello gerekli daha önce not ettiğiniz modülleri toobe komut dosyası izleyen hello için güncelleştirildi. Otomasyon işinizi başarısız olduğunu fark ederseniz, gerekli olan tüm modülleri ve bağımlılıklarını içeri aktardığınız onaylayın.
>
>

Azure Otomasyonu bağlantınız için hello uygulama kimliği aldıktan sonra bu uygulama, kasaya erişim tooupdate gizli olduğunu, anahtar kasanızı bildirmeniz gerekir. Bu PowerShell komutunu aşağıdaki hello ile gerçekleştirilebilir:

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <vaultName> -ServicePrincipalName <applicationIDfromAzureAutomation> -PermissionsToSecrets Set
```

Ardından, **Runbook'lar** Azure Automation örneği ve ardından altında **Runbook Ekle**. **Hızlı Oluştur**’u seçin. Runbook'unuzda adlandırın ve seçin **PowerShell** hello runbook türü. Merhaba seçeneği tooadd bir tanıma sahip. Son olarak, tıklatın **oluşturma**.

![Runbook oluşturma](./media/keyvault-keyrotation/Create_Runbook.png)

Yeni runbook'unuz için hello Düzenleyicisi bölmesinde PowerShell Betiği aşağıdaki hello yapıştırın:

```powershell
$connectionName = "AzureRunAsConnection"
try
{
    # Get hello connection "AzureRunAsConnection "
    $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

    "Logging in tooAzure..."
    Add-AzureRmAccount `
        -ServicePrincipal `
        -TenantId $servicePrincipalConnection.TenantId `
        -ApplicationId $servicePrincipalConnection.ApplicationId `
        -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
    "Login complete."
}
catch {
    if (!$servicePrincipalConnection)
    {
        $ErrorMessage = "Connection $connectionName not found."
        throw $ErrorMessage
    } else{
        Write-Error -Message $_.Exception
        throw $_.Exception
    }
}

#Optionally you may set hello following as parameters
$StorageAccountName = <storageAccountName>
$RGName = <storageAccountResourceGroupName>
$VaultName = <keyVaultName>
$SecretName = <keyVaultSecretName>

#Key name. For example key1 or key2 for hello storage account
New-AzureRmStorageAccountKey -ResourceGroupName $RGName -Name $StorageAccountName -KeyName "key2" -Verbose
$SAKeys = Get-AzureRmStorageAccountKey -ResourceGroupName $RGName -Name $StorageAccountName

$secretvalue = ConvertTo-SecureString $SAKeys[1].Value -AsPlainText -Force

$secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $SecretName -SecretValue $secretvalue
```

Merhaba Düzenleyicisi bölmesinden seçin **Test bölmesi** tootest komut. Merhaba komut hatasız çalışmaya başladıktan sonra seçebileceğiniz **Yayımla**, ve daha sonra geri hello runbook yapılandırma Bölmesi'nde hello runbook için bir zamanlama uygulayabilirsiniz.

## <a name="key-vault-auditing-pipeline"></a>Anahtar kasası denetim ardışık düzen
Bir anahtar kasasını ayarladığınızda, toohello anahtar kasası erişim isteklerini toocollect açtığında denetim kapatabilirsiniz. Bu günlükler belirlenmiş bir Azure depolama hesabında depolanır ve çıkışı, izlenen ve analiz çekebilir. hello uygulama kimliği hello web uygulamasının eşleşen bir uygulama parolaları hello kasadan aldığında hello aşağıdaki senaryoyu Azure işlevleri, Azure mantıksal uygulamaları ve anahtar kasası denetim günlüklerini toocreate ardışık düzen toosend bir e-posta kullanır.

İlk olarak, anahtar kasanızı günlüğü etkinleştirmeniz gerekir. Bu PowerShell komutlarını aşağıdaki hello yapılabilir (tam Ayrıntılar adresindeki görülme [anahtar kasası günlüğü](key-vault-logging.md)):

```powershell
$sa = New-AzureRmStorageAccount -ResourceGroupName <resourceGroupName> -Name <storageAccountName> -Type Standard\_LRS -Location 'East US'
$kv = Get-AzureRmKeyVault -VaultName '<vaultName>'
Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent
```

Bu özellik etkinleştirildikten sonra Denetim depolama hesabını belirlenmiş hello toplama başlangıç günlüğe kaydeder. Bu günlükler olayları anahtar kasalarınıza erişilen nasıl ve ne zaman ve kim tarafından içerir.

> [!NOTE]
> Merhaba anahtar kasası işleminden sonra 10 dakika günlük bilgilerinize erişebilir. Genellikle bu değerden daha hızlı olacaktır.
>
>

Merhaba sonraki adımdır çok[bir Azure hizmet veri yolu kuyruğu oluşturma](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md). Anahtar kasası denetim günlüklerini burada gönderilen budur. Merhaba denetim günlüğü iletileri hello sırada olduğunda hello mantıksal uygulama bunları alır ve bunlar üzerinde çalışır. Hizmet veri yolu ile şu adımları hello oluşturun:

1. Hizmet veri yolu ad alanı oluşturma (istediğiniz zaten varsa, bunun için toouse tooStep 2 atlayın).
2. Toohello service bus hello Azure portal ve select hello ad toocreate hello sıra istediğiniz göz atın.
3. Seçin **yeni** ve **hizmet veri yolu > sıra** ve gerekli hello ayrıntılarını girin.
4. Merhaba Service Bus bağlantı bilgilerini hello ad seçme ve tıklatarak seçin **bağlantı bilgilerini**. Merhaba sonraki bölüm için bu bilgilere ihtiyacınız olacaktır.

Ardından, [bir Azure işlevi oluşturma](../azure-functions/functions-create-first-azure-function.md) toopoll anahtar kasası günlükleri içinde hello depolama hesabı ve yeni olayları seçin. Bu bir zamanlamaya göre tetiklenen bir işlev olacaktır.

toocreate bir Azure işlevi seçin **yeni > işlev uygulaması** hello Azure Portalı'nda. Oluşturma sırasında var olan bir barındırma planı kullanın veya yeni bir tane oluşturun. Ayrıca, dinamik barındırmak için tercih. İşlevi barındırma seçenekleri hakkında daha fazla ayrıntı bulunabilir [nasıl tooscale Azure işlevleri](../azure-functions/functions-scale.md).

Hello Azure işlevi oluşturulduğunda tooit gidin ve bir süreölçer işlevi C seçip\#. Ardından **bu işlev oluşturma**.

![Azure işlevleri Başlat dikey penceresi](./media/keyvault-keyrotation/Azure_Functions_Start.png)

Merhaba üzerinde **geliştirme** sekmesinde, hello run.csx kod hello şununla değiştirin:

```csharp
#r "Newtonsoft.Json"

using System;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage.Blob;
using Microsoft.ServiceBus.Messaging;
using System.Text;

public static void Run(TimerInfo myTimer, TextReader inputBlob, TextWriter outputBlob, TraceWriter log)
{
    log.Info("Starting");

    CloudStorageAccount sourceStorageAccount = new CloudStorageAccount(new StorageCredentials("<STORAGE_ACCOUNT_NAME>", "<STORAGE_ACCOUNT_KEY>"), true);

    CloudBlobClient sourceCloudBlobClient = sourceStorageAccount.CreateCloudBlobClient();

    var connectionString = "<SERVICE_BUS_CONNECTION_STRING>";
    var queueName = "<SERVICE_BUS_QUEUE_NAME>";

    var sbClient = QueueClient.CreateFromConnectionString(connectionString, queueName);

    DateTime dtPrev = DateTime.UtcNow;
    if(inputBlob != null)
    {
        var txt = inputBlob.ReadToEnd();

        if(!string.IsNullOrEmpty(txt))
        {
            dtPrev = DateTime.Parse(txt);
            log.Verbose($"SyncPoint: {dtPrev.ToString("O")}");
        }
        else
        {
            dtPrev = DateTime.UtcNow;
            log.Verbose($"Sync point file didnt have a date. Setting toonow.");
        }
    }

    var now = DateTime.UtcNow;

    string blobPrefix = "insights-logs-auditevent/resourceId=/SUBSCRIPTIONS/<SUBSCRIPTION_ID>/RESOURCEGROUPS/<RESOURCE_GROUP_NAME>/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/<KEY_VAULT_NAME>/y=" + now.Year +"/m="+now.Month.ToString("D2")+"/d="+ (now.Day).ToString("D2")+"/h="+(now.Hour).ToString("D2")+"/m=00/";

    log.Info($"Scanning:  {blobPrefix}");

    IEnumerable<IListBlobItem> blobs = sourceCloudBlobClient.ListBlobs(blobPrefix, true);

    log.Info($"found {blobs.Count()} blobs");

    foreach(var item in blobs)
    {
        if (item is CloudBlockBlob)
        {
            CloudBlockBlob blockBlob = (CloudBlockBlob)item;

            log.Info($"Syncing: {item.Uri}");

            string sharedAccessUri = GetContainerSasUri(blockBlob);

            CloudBlockBlob sourceBlob = new CloudBlockBlob(new Uri(sharedAccessUri));

            string text;
            using (var memoryStream = new MemoryStream())
            {
                sourceBlob.DownloadToStream(memoryStream);
                text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
            }

            dynamic dynJson = JsonConvert.DeserializeObject(text);

            //required tooorder by time as they may not be in hello file
            var results = ((IEnumerable<dynamic>) dynJson.records).OrderBy(p => p.time);

            foreach (var jsonItem in results)
            {
                DateTime dt = Convert.ToDateTime(jsonItem.time);

                if(dt>dtPrev){
                    log.Info($"{jsonItem.ToString()}");

                    var payloadStream = new MemoryStream(Encoding.UTF8.GetBytes(jsonItem.ToString()));
                    //When sending tooServiceBus, use hello payloadStream and set keeporiginal tootrue
                    var message = new BrokeredMessage(payloadStream, true);
                    sbClient.Send(message);
                    dtPrev = dt;
                }
            }
        }
    }
    outputBlob.Write(dtPrev.ToString("o"));
}

static string GetContainerSasUri(CloudBlockBlob blob)
{
    SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy();

    sasConstraints.SharedAccessStartTime = DateTime.UtcNow.AddMinutes(-5);
    sasConstraints.SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24);
    sasConstraints.Permissions = SharedAccessBlobPermissions.Read;

    //Generate hello shared access signature on hello container, setting hello constraints directly on hello signature.
    string sasBlobToken = blob.GetSharedAccessSignature(sasConstraints);

    //Return hello URI string for hello container, including hello SAS token.
    return blob.Uri + sasBlobToken;
}
```


> [!NOTE]
> Kod toopoint tooyour depolama hesabı hello anahtar kasası günlükleri yazılacağı önceki hello hello hizmet veri yolu daha önce oluşturduğunuz emin tooreplace hello değişkenleri yapın ve belirli bir yola toohello anahtar kasası depolama günlükleri hello.
>
>

Merhaba işlevi hello anahtar kasası günlükleri, hello son olayları alan bu dosyadan yazılacağı hello en son günlük dosyası hello depolama hesabından seçer ve tooa Service Bus kuyruğuna iter. Tek bir dosyada birden çok olay olabilir beri hello işlevi toodetermine hello çekilmiş yukarı hello son olay zaman damgası da bakan bir sync.txt dosyası oluşturmanız gerekir. Bu, anında yok sağlar birden çok kez aynı olay hello. Bu sync.txt dosya hello son karşılaşılan olayı için bir zaman damgası içeriyor. Merhaba yüklendiğinde, günlükleri, sahip sıralanmış toobe bunlar doğru sıralı hello zaman damgası tooensure üzerinde temel.

Bu işlev için birkaç Azure işlevleri hello kutusunda dışında bulunmayan ek kitaplıklara başvuru. tooinclude bunlar, Azure işlevleri toopull ihtiyacımız bunları NuGet kullanma. Merhaba seçin **dosyaları görüntüle** seçeneği.

![Görünüm dosyaları seçeneği](./media/keyvault-keyrotation/Azure_Functions_ViewFiles.png)

Ve aşağıdaki içeriğe sahip project.json adlı bir dosyaya ekleyin:

```json
    {
      "frameworks": {
        "net46":{
          "dependencies": {
                "WindowsAzure.Storage": "7.0.0",
                "WindowsAzure.ServiceBus":"3.2.2"
          }
        }
       }
    }
```
Bağlı **kaydetmek**, Azure işlevleri, gerekli hello ikili dosyaları indirir.

Geçiş toohello **tümleştir** sekmesinde ve hello Zamanlayıcı parametre anlamlı bir ad toouse hello işlevi içinde verin. İsteğe bağlı olarak kod önceki hello adlı hello Zamanlayıcı toobe bekliyor *myTimer*. Belirtin bir [CRON ifade](../app-service-web/web-sites-create-web-jobs.md#CreateScheduledCRON) gibi: 0 \* \* \* \* \* hello işlevi toorun bir dakika neden olacak hello Zamanlayıcı için.

Üzerinde hello aynı **tümleştir** sekmesinde, hello türündeki bir girdi ekleme **Azure Blob Storage**. Bu en hello işlevi tarafından aranan hello son olay hello zaman damgası içeren toohello sync.txt dosyasını işaret edecek. Bu, hello parametre adı tarafından hello işlevi içinde kullanılabilir olacaktır. Kod önceki hello hello parametre adı toobe hello Azure Blob Storage giriş bekliyor *inputBlob*. Merhaba sync.txt dosya nerede bulunacağı hello depolama hesabını seçin (aynı veya farklı bir depolama hesabı hello olabilir). Merhaba yol alanına nerede {container-name}/path/to/sync.txt. hello biçiminde hello dosya yaşıyor hello yolunu belirtin

Bir çıkış hello türü ekleme *Azure Blob Storage* çıktı. Bu toohello sync.txt dosyası hello girişinde tanımlı noktası. Bu, aranan hello son olay hello işlevi toowrite hello zaman damgası tarafından kullanılır. Merhaba önceki kod bekliyor olarak adlandırılan bu parametre toobe *outputBlob*.

Bu noktada, hello işlevi hazırdır. Emin tooswitch geri toohello olun **geliştirme** sekmesinde ve hello kodu kaydedin. Derleme hataları için Hello çıktı penceresini denetleyin ve uygun şekilde düzeltin. Hello kodu derler, hello kod artık hello anahtar kasası günlükleri dakikada kontrol edilmesi ve Service Bus kuyruğuna hello üzerine yeni olaylar Ftp'den tanımlı. Günlük kaydı bilgileri hello işlevi her başlatılışında toohello günlük penceresindeki yazma görmeniz gerekir.

### <a name="azure-logic-app"></a>Azure mantıksal uygulama
Sonraki hello işlevi toohello Service Bus kuyruğuna Ftp'den, hello içerik ayrıştırır ve eşleşen bir koşula göre bir e-posta gönderir hello olayları seçer bir Azure mantıksal uygulama oluşturmanız gerekir.

[Mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md) çok giderek**yeni > mantıksal uygulama**.

Merhaba mantıksal uygulama oluşturulduktan sonra tooit gidin ve seçin **Düzenle**. Merhaba mantığı uygulama düzenleyicisinde seçin **hizmet veri yolu kuyruğu** ve Service Bus kimlik bilgilerini tooconnect girin, toohello sırası.

![Azure Logic App Service Bus](./media/keyvault-keyrotation/Azure_LogicApp_ServiceBus.png)

Sonraki seçin **bir koşul eklemek**. Merhaba koşulunda Düzenleyicisi Gelişmiş toohello geçin ve aşağıdaki kod, APP_ID hello ile değiştiriliyor hello girin, web uygulamanızın gerçek APP_ID:

```
@equals('<APP_ID>', json(decodeBase64(triggerBody()['ContentData']))['identity']['claim']['appid'])
```

Bu ifade temelde döndürür **false** hello varsa *AppID* olduğundan (Bu hello hello Service Bus ileti gövdesi) gelen olay hello değil hello *AppID* Merhaba, uygulama.

Şimdi, altında bir eylem oluşturun **Öyle değilse, hiçbir şey yapma**.

![Azure mantıksal uygulama eylemi seçin](./media/keyvault-keyrotation/Azure_LogicApp_Condition.png)

Merhaba eylem için **Office 365 - e-postası gönderme**. Merhaba koşul döndürür tanımlandığında hello alanları toocreate bir e-posta toosend doldurun **false**. Office 365 yoksa alternatifleri görünebilir tooachieve hello aynı sonuçları.

Bu noktada yeni anahtar kasası denetim günlükleri için bir dakika benzeyen bir bitiş tooend ardışık vardır. Yeni günlükler tooa hizmet veri yolu kuyruğu bulduğu iter. Yeni bir ileti hello sırada adlandırıldığını zaman hello mantıksal uygulama tetiklenir. Merhaba, *AppID* içinde hello uygulamasını çağıran hello hello uygulama Kimliğini olay eşleşmiyor, bir e-posta gönderir.
