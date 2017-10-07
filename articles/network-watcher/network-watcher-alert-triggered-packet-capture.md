---
title: "aaaUse paket yakalama toodo öngörülü ağ uyarılar ve Azure işlevleri izleme | Microsoft Docs"
description: "Paket yakalama Azure Ağ İzleyicisi ile nasıl toocreate bir uyarı tetikleyen bu makalede"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 75e6e7c4-b3ba-4173-8815-b00d7d824e11
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 4722a831f3a9d5537c0e6f53daba4dfc35d0cf24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-packet-capture-for-proactive-network-monitoring-with-alerts-and-azure-functions"></a>Paket yakalama öngörülü ağ izleme için uyarıları ve Azure işlevleri kullanın

Ağ İzleyicisi paket yakalama yakalama oturumları tootrack trafiği sanal makineleri filtrelemek oluşturur. Merhaba yakalama dosyası tanımlı bir filtre olabilir tootrack yalnızca hello trafiği toomonitor istiyor. Bu veriler, ardından bir depolama blob veya yerel olarak hello Konuk makineye depolanır.

Bu özellik, Azure işlevleri gibi diğer Otomasyon senaryolardan uzaktan başlatılabilir. Paket yakalama verir yetenek toorun öngörülü yakalamaları göre hello ağ anormallikleri tanımlanır. Diğer kullanımlar ağ yetkisiz erişim, hata ayıklama istemci-sunucu iletişimleri ve daha fazlasını hakkında bilgi alma ağ istatistikleri toplama içerir.

Azure'da dağıtılan kaynakları 7/24 çalıştırın. Sizin ve ekibinizin tüm kaynakları 7/24 hello durumu etkin olarak izleyemez. Örneğin, 2'de bir sorun oluşursa ne olur?

Ağ İzleyicisi'ni kullanarak, uyarı ve işlevlerden hello Azure ekosistemi içinde ağınızda önceden hello veri ve araçları toosolve sorunlara yanıt verebilir.

![Senaryo][scenario]

## <a name="prerequisites"></a>Ön koşullar

* Merhaba en son sürümünü [Azure PowerShell](/powershell/azure/install-azurerm-ps).
* Ağ İzleyicisi var olan bir örneği. Zaten yoksa, [Ağ İzleyicisi örneği oluşturun](network-watcher-create.md).
* Merhaba, mevcut bir sanal makine Ağ İzleyicisi Merhaba ile aynı bölgede [Windows uzantısı](../virtual-machines/windows/extensions-nwa.md) veya [Linux sanal makine uzantısı](../virtual-machines/linux/extensions-nwa.md).

## <a name="scenario"></a>Senaryo

Bu örnekte, VM normalden daha çok TCP kesimini gönderme ve uyarı toobe istiyor. TCP kesimini burada bir örnek olarak kullanılır, ancak hiçbir uyarı koşulu kullanabilirsiniz.

Uyarı aldığınızda iletişimi neden artırmıştır tooreceive paket düzeyinde veri toounderstand istiyor. Ardından tooreturn hello sanal makine tooregular iletişimi adımları uygulayabilirsiniz.

Bu senaryo, Ağ İzleyicisi'ni ve geçerli bir sanal makine ile bir kaynak grubu mevcut bir örneği olduğunu varsayar.

liste aşağıdaki hello gerçekleşir hello iş akışına genel bir bakış verilmiştir:

1. Bir uyarı, VM tetiklenir.
1. Merhaba uyarı Azure işlevinizi aracılığıyla bir Web kancası çağırır.
1. Azure işlevinizi hello uyarı işler ve bir Ağ İzleyicisi paket yakalama oturumu başlatır.
1. Merhaba paket yakalama hello VM üzerinde çalışır ve trafik toplar.
1. Merhaba paket yakalama dosyasını karşıya tooa inceleme ve tanılama depolama hesabı.

tooautomate bu işlem, biz oluşturabilir ve hello olay gerçekleştiğinde bir uyarı bizim VM tootrigger bağlayabilirsiniz. Ayrıca bir işlev toocall Ağ İzleyicisi oluşturuyoruz.

Bu senaryo aşağıdaki hello:

* Paket yakalama başlatır Azure bir işlev oluşturur.
* Bir sanal makinede bir uyarı kuralı oluşturur ve hello uyarı kuralı toocall hello Azure işlevi yapılandırır.

## <a name="create-an-azure-function"></a>Bir Azure işlevi oluşturma

Merhaba ilk adımı toocreate bir Azure işlevi tooprocess hello uyarı ve paket yakalama oluşturma.

1. Merhaba, [Azure portal](https://portal.azure.com)seçin **yeni** > **işlem** > **işlev uygulaması**.

    ![Bir işlev uygulaması oluşturma][1-1]

2. Merhaba üzerinde **işlev uygulaması** dikey penceresinde hello aşağıdaki değerleri girin ve ardından **Tamam** toocreate hello uygulama:

    |**Ayar** | **Değer** | **Ayrıntılar** |
    |---|---|---|
    |**Uygulama adı**|PacketCaptureExample|Merhaba işlev uygulaması Hello adı.|
    |**Abonelik**|[Aboneliğinizi] hello hangi toocreate hello işlev uygulaması için aboneliği.||
    |**Kaynak Grubu**|PacketCaptureRG|Merhaba kaynak grubu toocontain hello işlev uygulaması.|
    |**Barındırma planı**|Tüketim planı| Merhaba türü, işlev uygulaması kullanır planlayın. Seçenekler şunlardır tüketimi veya Azure uygulama hizmeti planı. |
    |**Konum**|Orta ABD| hangi toocreate hello işlev uygulaması bölgede Hello.|
    |**Depolama hesabı**|{otomatik olarak oluşturulur}| Azure işlevleri için genel amaçlı depolama alanı ihtiyaçlarınızı hello depolama hesabı.|

3. Merhaba üzerinde **PacketCaptureExample işlev uygulamalarının** dikey penceresinde, select **işlevleri** > **özel işlevi**  >  **+**.

4. Seçin **HttpTrigger Powershell**ve ardından bilgi kalan hello girin. Son olarak, toocreate hello işlevi, select **oluşturma**.

    |**Ayar** | **Değer** | **Ayrıntılar** |
    |---|---|---|
    |**Senaryo**|Deneysel|Tür senaryosu|
    |**İşlevinizi adlandırın**|AlertPacketCapturePowerShell|Merhaba işlevin adı|
    |**Yetkilendirme düzeyi**|İşlevi|Merhaba işlevi için yetkilendirme düzeyi|

![İşlevleri örneği][functions1]

> [!NOTE]
> Merhaba PowerShell şablon Deneysel ve tam desteğine sahip değil.

Özelleştirmeleri bu örnek için gereklidir ve aşağıdaki adımları hello açıklanmıştır.

### <a name="add-modules"></a>Modüller ekleme

toouse Ağ İzleyicisi PowerShell cmdlet'leri hello en yeni PowerShell modülü toohello işlevi uygulamasını karşıya yükleyin.

1. Yerel makinenizde hello yüklü en son Azure PowerShell modülleri, hello aşağıdaki PowerShell komutunu çalıştırın:

    ```powershell
    (Get-Module AzureRM.Network).Path
    ```

    Bu örnek, Azure PowerShell modülü yerel yol hello olanağı sağlar. Bu klasörler, bir sonraki adımda kullanılır. Bu senaryoda kullanılan hello modülleri şunlardır:

    * AzureRM.Network

    * AzureRM.Profile

    * AzureRM.Resources

    ![PowerShell klasörleri][functions5]

1. Seçin **işlev uygulaması ayarları** > **tooApp Hizmet Düzenleyicisi Git**.

    ![İşlev uygulama ayarları][functions2]

1. Sağ hello **AlertPacketCapturePowershell** klasörünü ve ardından adlı bir klasör oluşturun **azuremodules**. 

4. Gereksinim duyduğunuz her modül için bir alt klasör oluşturun.

    ![Klasör ve alt klasörleri][functions3]

    * AzureRM.Network

    * AzureRM.Profile

    * AzureRM.Resources

1. Sağ hello **AzureRM.Network** alt ve ardından **dosya yükleme**. 

6. Tooyour Azure Git modüller. Merhaba yerel **AzureRM.Network** klasörü, tüm hello dosyaları hello klasörü seçin. Ardından **Tamam**. 

7. İçin bu adımları yineleyin **AzureRM.Profile** ve **AzureRM.Resources**.

    ![Dosyaları karşıya yükleme][functions6]

1. Tamamlandı sonra her klasör hello PowerShell modülü yerel makinenize dosyalarından sahip olmalıdır.

    ![PowerShell dosyaları][functions7]

### <a name="authentication"></a>Kimlik Doğrulaması

toouse hello PowerShell cmdlet'leri, kimlik doğrulaması gerekir. Merhaba işlevi uygulamasında kimlik doğrulamasını yapılandırın. tooconfigure kimlik doğrulaması, ortam değişkenleri yapılandırmanız ve şifrelenmiş anahtar dosyası toohello işlevi uygulama yüklemeniz gerekir.

> [!NOTE]
> Bu senaryoyu nasıl sadece bir örnek sağlar Azure işlevleri ile tooimplement kimlik doğrulaması. Vardır diğer yolları toodo bu.

#### <a name="encrypted-credentials"></a>Şifrelenmiş kimlik bilgileri

PowerShell Betiği aşağıdaki hello adlı bir anahtar dosyası oluşturur **PassEncryptKey.key**. Ayrıca, sağlanan hello parola şifreli sürümünü sağlar. Merhaba bu paroladır hello Azure Active Directory kimlik doğrulaması için kullanılan bir uygulama için tanımlanmış aynı parola.

```powershell
#Variables
$keypath = "C:\temp\PassEncryptKey.key"
$AESKey = New-Object Byte[] 32
$Password = "<insert a password here>"

#Keys
[Security.Cryptography.RNGCryptoServiceProvider]::Create().GetBytes($AESKey) 
Set-Content $keypath $AESKey

#Get encrypted password
$secPw = ConvertTo-SecureString -AsPlainText $Password -Force
$AESKey = Get-content $KeyPath
$Encryptedpassword = $secPw | ConvertFrom-SecureString -Key $AESKey
$Encryptedpassword
```

Hello hello işlev uygulaması App Service Düzenleyicisi, adlı bir klasör oluşturun **anahtarları** altında **AlertPacketCapturePowerShell**. Merhaba karşıya yükleme **PassEncryptKey.key** hello önceki PowerShell örneğinde oluşturulan dosyası.

![İşlevler anahtarı][functions8]

### <a name="retrieve-values-for-environment-variables"></a>Ortam değişkenleri için değerleri alma

Merhaba son tooset kimlik doğrulaması için gerekli tooaccess hello değerler hello ortam değişkenlerini ayarlama gereksinimdir. Merhaba aşağıdaki listede oluşturulan hello ortam değişkenleri gösterilmektedir:

* AzureClientID

* AzureTenant

* AzureCredPassword


#### <a name="azureclientid"></a>AzureClientID

Merhaba istemci hello Azure Active Directory'de bir uygulamanın uygulama Kimliğini kimliğidir.

1. Bir uygulama toouse zaten sahip değilseniz, örnek toocreate aşağıdaki hello bir uygulamayı çalıştırın.

    ```powershell
    $app = New-AzureRmADApplication -DisplayName "ExampleAutomationAccount_MF" -HomePage "https://exampleapp.com" -IdentifierUris "https://exampleapp1.com/ExampleFunctionsAccount" -Password "<same password as defined earlier>"
    New-AzureRmADServicePrincipal -ApplicationId $app.ApplicationId
    Start-Sleep 15
    New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $app.ApplicationId
    ```

   > [!NOTE]
   > Merhaba uygulaması oluşturma hello olmalıdır kullandığınız hello parola hello anahtar dosyası kaydedilirken daha önce oluşturduğunuz aynı parola.

1. Hello Azure portal, seçin **abonelikleri**. Merhaba abonelik toouse seçin ve ardından **erişim denetimi (IAM)**.

    ![İşlevler IAM][functions9]

1. Merhaba hesap toouse seçin ve ardından **özellikleri**. Kopya hello uygulama kimliği

    ![İşlevleri uygulama kimliği][functions10]

#### <a name="azuretenant"></a>AzureTenant

PowerShell örnek aşağıdaki hello çalıştırarak Hello Kiracı kimliği alın:

```powershell
(Get-AzureRmSubscription -SubscriptionName "<subscriptionName>").TenantId
```

#### <a name="azurecredpassword"></a>AzureCredPassword

Merhaba hello AzureCredPassword ortam değişkeninin değerini PowerShell örnek aşağıdaki hello çalışmasını alma hello değerdir. Bu örnek aynı hello önceki gösterilen hello olan **şifrelenmiş kimlik bilgileri** bölümü. Merhaba gerekli olan değer hello hello çıkışıdır `$Encryptedpassword` değişkeni.  Bu hello PowerShell Betiği kullanılarak şifrelenmiş hello hizmet asıl paroladır.

```powershell
#Variables
$keypath = "C:\temp\PassEncryptKey.key"
$AESKey = New-Object Byte[] 32
$Password = "<insert a password here>"

#Keys
[Security.Cryptography.RNGCryptoServiceProvider]::Create().GetBytes($AESKey) 
Set-Content $keypath $AESKey

#Get encrypted password
$secPw = ConvertTo-SecureString -AsPlainText $Password -Force
$AESKey = Get-content $KeyPath
$Encryptedpassword = $secPw | ConvertFrom-SecureString -Key $AESKey
$Encryptedpassword
```

### <a name="store-hello-environment-variables"></a>Depolama hello ortam değişkenleri

1. Toohello işlev uygulaması gidin. Ardından **işlev uygulaması ayarları** > **uygulaması ayarlarını yapılandır**.

    ![Uygulama ayarlarını yapılandırma][functions11]

1. Merhaba ortam değişkenlerini ve değerleri toohello uygulama ayarlarına ekleyin ve ardından **kaydetmek**.

    ![Uygulama ayarları][functions12]

### <a name="add-powershell-toohello-function"></a>Add PowerShell toohello işlevi

Ağ İzleyicisi ' içine hello Azure işlevi içinde zaman toomake çağırır artık olur. Merhaba gereksinimlerine bağlı olarak, bu işlevin hello uygulama farklılık gösterebilir. Ancak, hello genel akış hello kod aşağıdaki gibidir:

1. İşlem giriş parametreleri.
2. Sorgu varolan paket tooverify sınırları yakalar ve adı çakışmalarını.
3. Paket yakalama uygun parametrelerle oluşturun.
4. Yoklama paket düzenli aralıklarla tamamlanana kadar yakalayın.
5. Merhaba paket yakalama oturumu tamamlandıktan Hello kullanıcıyı bilgilendirir.

Merhaba aşağıdaki örnek, hello işlevinde kullanılabilir PowerShell kodu bulunur. İçin yerini toobe gereken değerler **Subscriptionıd**, **resourceGroupName**, ve **storageAccountName**.

```powershell
            #Import Azure PowerShell modules required toomake calls tooNetwork Watcher
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Profile\AzureRM.Profile.psd1" -Global
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Network\AzureRM.Network.psd1" -Global
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Resources\AzureRM.Resources.psd1" -Global

            #Process alert request body
            $requestBody = Get-Content $req -Raw | ConvertFrom-Json

            #Storage account ID toosave captures in
            $storageaccountid = "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{storageAccountName}"

            #Packet capture vars
            $packetcapturename = "PSAzureFunction"
            $packetCaptureLimit = 10
            $packetCaptureDuration = 10

            #Credentials
            $tenant = $env:AzureTenant
            $pw = $env:AzureCredPassword
            $clientid = $env:AzureClientId
            $keypath = "D:\home\site\wwwroot\AlertPacketCapturePowerShell\keys\PassEncryptKey.key"

            #Authentication
            $secpassword = $pw | ConvertTo-SecureString -Key (Get-Content $keypath)
            $credential = New-Object System.Management.Automation.PSCredential ($clientid, $secpassword)
            Add-AzureRMAccount -ServicePrincipal -Tenant $tenant -Credential $credential #-WarningAction SilentlyContinue | out-null


            #Get hello VM that fired hello alert
            if($requestBody.context.resourceType -eq "Microsoft.Compute/virtualMachines")
            {
                Write-Output ("Subscription ID: {0}" -f $requestBody.context.subscriptionId)
                Write-Output ("Resource Group:  {0}" -f $requestBody.context.resourceGroupName)
                Write-Output ("Resource Name:  {0}" -f $requestBody.context.resourceName)
                Write-Output ("Resource Type:  {0}" -f $requestBody.context.resourceType)

                #Get hello Network Watcher in hello VM's region
                $nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $requestBody.context.resourceRegion}
                $networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

                #Get existing packetCaptures
                $packetCaptures = Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher

                #Remove existing packet capture created by hello function (if it exists)
                $packetCaptures | %{if($_.Name -eq $packetCaptureName)
                { 
                    Remove-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName $packetCaptureName
                }}

                #Initiate packet capture on hello VM that fired hello alert
                if ((Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher).Count -lt $packetCaptureLimit){
                    echo "Initiating Packet Capture"
                    New-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -TargetVirtualMachineId $requestBody.context.resourceId -PacketCaptureName $packetCaptureName -StorageAccountId $storageaccountid -TimeLimitInSeconds $packetCaptureDuration
                    Out-File -Encoding Ascii -FilePath $res -inputObject "Packet Capture created on ${requestBody.context.resourceID}"
                }
            } 
 ``` 
#### <a name="retrieve-hello-function-url"></a>Merhaba işlevi URL'sini alın 
1. İşlevinizi oluşturduktan sonra hello işlev ile ilişkili uyarı toocall hello URL'nizi yapılandırın. tooget bu değer, kopyalama hello işlevi işlevi uygulamanızı URL'den.

    ![Merhaba işlevi URL bulma][functions13]

2. İşlev uygulamanız için Hello işlevi URL'sini kopyalayın.

    ![Merhaba işlevi URL kopyalanması][2]

Özel özellikler hello Web kancası POST isteğinin hello yükte gerektiriyorsa, çok başvurmak[bir Web kancası Azure ölçüm uyarıyı yapılandırmak](../monitoring-and-diagnostics/insights-webhooks-alerts.md).

## <a name="configure-an-alert-on-a-vm"></a>Bir VM üzerinde bir uyarı yapılandırmak

Uyarılar, yapılandırılmış toonotify kişiler olabilir, belirli bir ölçüyü atanmış bir eşik kestiği zaman tooit. Bu örnekte, hello üzerinde hello gönderilen TCP kesimini uyarısıdır, ancak diğer birçok ölçümlerini hello uyarı tetiklenebilir. Bu örnekte, bir uyarı yapılandırılmış toocall bir Web kancası toocall hello işlevi ' dir.

### <a name="create-hello-alert-rule"></a>Merhaba uyarı kuralı oluştur

Tooan varolan sanal makine gidin ve ardından bir uyarı kuralı ekleyin. Uyarıları yapılandırma hakkında daha ayrıntılı belgeler bulunabilir [oluşturma uyarıları Azure İzleyicisi'nde için Azure services - Azure portalında](../monitoring-and-diagnostics/insights-alerts-portal.md). Merhaba değerleri aşağıdaki hello girin **uyarı kuralı** dikey ve ardından **Tamam**.

  |**Ayar** | **Değer** | **Ayrıntılar** |
  |---|---|---|
  |**Ad**|TCP_Segments_Sent_Exceeded|Merhaba uyarı kuralının adı.|
  |**Açıklama**|TCP kesimini aşıldı eşik gönderilen|Merhaba uyarı kuralı Hello açıklaması.||
  |**Ölçüm**|Gönderilen TCP kesimleri| Merhaba ölçüm toouse tootrigger hello uyarı. |
  |**Koşul**|Şu değerden fazla:| Koşul toouse hello ölçüm değerlendirirken hello.|
  |**Eşik**|100| Merhaba uyarıyı tetikleyen hello ölçüm Hello değeri. Bu değer, ortamınız için geçerli değer tooa ayarlamanız gerekir.|
  |**Süresi**|Merhaba son beş dakika içinde| Hangi toolook Hello dönemde hello ölçüm hello eşiğine için belirler.|
  |**Web kancası**|[işlev uygulaması URL'SİNDEN Web kancası]| Merhaba önceki adımlarda oluşturduğunuz hello işlevi uygulamadan Hello Web kancası URL'si.|

> [!NOTE]
> Merhaba TCP kesimleri ölçümü varsayılan olarak etkin değildir. Hakkında daha fazla bilgi şu adresi ziyaret ederek tooenable ek ölçümler [izleme ve tanılama](../monitoring-and-diagnostics/insights-how-to-use-diagnostics.md).

## <a name="review-hello-results"></a>Merhaba sonuçlarını gözden geçirin

Merhaba ölçütlerine sonra hello uyarı tetikleyiciler, bir paket yakalama oluşturulur. TooNetwork İzleyici gidin ve ardından **paket yakalama**. Bu sayfada hello paket yakalama dosyası bağlantı toodownload hello paket yakalama seçebilirsiniz.

![Görünüm paket yakalama][functions14]

Merhaba yakalama dosyasını yerel olarak depolanıyorsa, toohello sanal makinede oturum açarak alabilirsiniz.

Azure depolama hesaplarından dosyalarını yükleme hakkında yönergeler için bkz: [.NET kullanarak Azure Blob storage'ı kullanmaya başlama](../storage/blobs/storage-dotnet-how-to-use-blobs.md). Kullanabileceğiniz başka bir araçtır [Depolama Gezgini](http://storageexplorer.com/).

Yakalama yüklendikten sonra okuyabilir herhangi bir aracı kullanarak görüntüleyebilirsiniz bir **.cap** dosya. Bu araçların bağlantılar tootwo şunlardır:

- [Microsoft Message Analyzer](https://technet.microsoft.com/library/jj649776.aspx)
- [WireShark](https://www.wireshark.org/)

## <a name="next-steps"></a>Sonraki adımlar

Nasıl tooview ziyaret ederek, paket yakalar öğrenin [paket yakalama çözümlemesini Wireshark ile](network-watcher-deep-packet-inspection.md).


[1]: ./media/network-watcher-alert-triggered-packet-capture/figure1.png
[1-1]: ./media/network-watcher-alert-triggered-packet-capture/figure1-1.png
[2]: ./media/network-watcher-alert-triggered-packet-capture/figure2.png
[3]: ./media/network-watcher-alert-triggered-packet-capture/figure3.png
[functions1]:./media/network-watcher-alert-triggered-packet-capture/functions1.png
[functions2]:./media/network-watcher-alert-triggered-packet-capture/functions2.png
[functions3]:./media/network-watcher-alert-triggered-packet-capture/functions3.png
[functions4]:./media/network-watcher-alert-triggered-packet-capture/functions4.png
[functions5]:./media/network-watcher-alert-triggered-packet-capture/functions5.png
[functions6]:./media/network-watcher-alert-triggered-packet-capture/functions6.png
[functions7]:./media/network-watcher-alert-triggered-packet-capture/functions7.png
[functions8]:./media/network-watcher-alert-triggered-packet-capture/functions8.png
[functions9]:./media/network-watcher-alert-triggered-packet-capture/functions9.png
[functions10]:./media/network-watcher-alert-triggered-packet-capture/functions10.png
[functions11]:./media/network-watcher-alert-triggered-packet-capture/functions11.png
[functions12]:./media/network-watcher-alert-triggered-packet-capture/functions12.png
[functions13]:./media/network-watcher-alert-triggered-packet-capture/functions13.png
[functions14]:./media/network-watcher-alert-triggered-packet-capture/functions14.png
[scenario]:./media/network-watcher-alert-triggered-packet-capture/scenario.png
