---
title: "aaaAzure sanal makine ölçek ayarlar ile ilgili SSS | Microsoft Docs"
description: "Sanal makine ölçek kümeleri hakkında sorular yanıtlar toofrequently alın."
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/20/2017
ms.author: negat
ms.custom: na
ms.openlocfilehash: 0deb9e2bb79f87f17bbf748397b94dc53070cfbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machine-scale-sets-faqs"></a>Azure sanal makine ölçek SSS ayarlar

Azure'da sanal makine ölçek hakkında sorular toofrequently ayarlar yanıtlar alın.

## <a name="autoscale"></a>Otomatik Ölçeklendirme

### <a name="what-are-best-practices-for-azure-autoscale"></a>Azure otomatik ölçeklendirme için en iyi uygulamalar nelerdir?

Otomatik ölçeklendirme için en iyi yöntemler için bkz: [otomatik ölçeklendirmeyi sanal makineler için en iyi uygulamaları](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-best-practices).

### <a name="where-do-i-find-metric-names-for-autoscaling-that-uses-host-based-metrics"></a>Ana bilgisayar tabanlı ölçümleri kullanan otomatik ölçeklendirme ölçüm adlarını nereden bulabilirim?

Ana bilgisayar tabanlı ölçümleri kullanan otomatik ölçeklendirmeyi için ölçüm adları için bkz: [desteklenen Azure İzleyicisi ile ölçümleri](https://azure.microsoft.com/documentation/articles/monitoring-supported-metrics/).

### <a name="are-there-any-examples-of-autoscaling-based-on-an-azure-service-bus-topic-and-queue-length"></a>Herhangi bir Azure Service Bus konu ve sıra uzunluğuna göre otomatik ölçeklendirmeyi örnekleri bulunur?

Evet. Bir Azure Service Bus konu ve sıra uzunluğuna göre otomatik ölçeklendirmeyi örnekleri için bkz: [Azure İzleyici otomatik ölçeklendirmeyi ortak ölçümleri](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/).

Service Bus kuyruğu için JSON aşağıdaki hello kullan:

```json
"metricName": "MessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue"
```

Bir depolama kuyruğu için JSON aşağıdaki hello kullan:

```json
"metricName": "ApproximateMessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ClassicStorage/storageAccounts/mystorage/services/queue/queues/mystoragequeue"
```

Örnek değerler kaynak Tekdüzen Kaynak Tanımlayıcıları (URI'ler) ile değiştirin.


### <a name="should-i-autoscale-by-using-host-based-metrics-or-a-diagnostics-extension"></a>Mıyım otomatik ölçeklendirme ana bilgisayar tabanlı ölçümleri veya tanılama uzantısını kullanarak?

Otomatik ölçeklendirme ayarı, bir VM toouse ana bilgisayar düzeyinde ölçümleri veya konuk işletim sistemi tabanlı ölçümleri oluşturabilirsiniz.

Desteklenen ölçümleri listesi için bkz: [Azure İzleyici otomatik ölçeklendirmeyi ortak ölçümleri](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-common-metrics). 

Sanal makine ölçek kümeleri için tam bir örnek için bkz: [sanal makine ölçek kümeleri için Resource Manager şablonları kullanarak gelişmiş otomatik ölçeklendirme yapılandırmasını](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-advanced-autoscale-virtual-machine-scale-sets). 

Merhaba örnek hello ana bilgisayar düzeyinde CPU ölçüm ve bir ileti sayısı ölçümü kullanır.



### <a name="how-do-i-set-alert-rules-on-a-virtual-machine-scale-set"></a>Uyarı kuralları bir sanal makine ölçek kümesinde nasıl ayarlarım?

PowerShell veya Azure CLI aracılığıyla sanal makine ölçek kümeleri için ölçümler üzerinde uyarılar oluşturabilirsiniz. Daha fazla bilgi için bkz: [Azure İzleyici PowerShell hızlı başlangıç örnekleri](https://azure.microsoft.com/documentation/articles/insights-powershell-samples/#create-alert-rules) ve [Azure İzleyici platformlar arası CLI hızlı başlangıç örnekleri](https://azure.microsoft.com/documentation/articles/insights-cli-samples/#work-with-alerts).

Merhaba uç noktası Targetresourceıd hello sanal makine ölçek kümesinin şöyle görünür: 

/Subscriptions/yoursubscriptionid/resourceGroups/yourresourcegroup/providers/Microsoft.COMPUTE/virtualMachineScaleSets/yourvmssname

Tüm VM performans sayacı için bir uyarı hello ölçüm tooset seçebilirsiniz. Daha fazla bilgi için bkz: [Resource Manager tabanlı Windows VM'ler için konuk işletim sistemi ölçümleri](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-resource-manager-based-windows-vms) ve [Linux VM'ler için konuk işletim sistemi ölçümleri](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-linux-vms) hello içinde [Azure İzleyici otomatik ölçeklendirmeyi ortak ölçümleri](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/)makalesi.

### <a name="how-do-i-set-up-autoscale-on-a-virtual-machine-scale-set-by-using-powershell"></a>PowerShell kullanarak bir sanal makine ölçek göre otomatik ölçeklendirme nasıl ayarlayabilirim?

PowerShell kullanarak bir sanal makine ölçek göre otomatik ölçeklendirme yukarı tooset hello blog yayınına bakın [nasıl tooadd otomatik ölçeklendirme tooan Azure sanal makine ölçek kümesi](https://msftstack.wordpress.com/2017/03/05/how-to-add-autoscale-to-an-azure-vm-scale-set/).




## <a name="certificates"></a>Sertifikalar

### <a name="how-do-i-securely-ship-a-certificate-toohello-vm-how-do-i-provision-a-virtual-machine-scale-set-toorun-a-website-where-hello-ssl-for-hello-website-is-shipped-securely-from-a-certificate-configuration-hello-common-certificate-rotation-operation-would-be-almost-hello-same-as-a-configuration-update-operation-do-you-have-an-example-of-how-toodo-this"></a>Nasıl bir sertifika toohello VM güvenli bir şekilde sevk? Bir sanal makine ölçek kümesi toorun burada hello hello Web sitesi için SSL güvenli bir şekilde bir sertifikayı yapılandırmasından sevk bir Web sitesi nasıl sağlama? (Merhaba ortak sertifika döndürme işlemi olması neredeyse hello yapılandırmasını güncelleştirme işlemi ile aynı.) Nasıl bir örnek zorunda toodo bu? 

toosecurely sevk sertifika toohello VM, bir müşteri sertifikası, doğrudan bir Windows sertifika deposuna hello Müşteri'nin anahtar Kasası'ndan yükleyebilir.

JSON aşağıdaki hello kullan:

```json
"secrets": [
    {
        "sourceVault": {
            "id": "/subscriptions/{subscriptionid}/resourceGroups/myrg1/providers/Microsoft.KeyVault/vaults/mykeyvault1"
        },
        "vaultCertificates": [
            {
                "certificateUrl": "https://mykeyvault1.vault.azure.net/secrets/{secretname}/{secret-version}",
                "certificateStore": "certificateStoreName"
            }
        ]
    }
]
```

Merhaba kodu, Windows ve Linux destekler.

Daha fazla bilgi için bkz: [oluştur veya güncelleştir bir sanal makine ölçek kümesi](https://msdn.microsoft.com/library/mt589035.aspx).


### <a name="example-of-self-signed-certificate"></a>Otomatik olarak imzalanan sertifika örneği

1.  Kendinden imzalı bir sertifika bir anahtar kasası oluşturun.

    Merhaba aşağıdaki PowerShell komutlarını kullanın:

    ```powershell
    Import-Module "C:\Users\mikhegn\Downloads\Service-Fabric-master\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

    Login-AzureRmAccount

    Invoke-AddCertToKeyVault -SubscriptionId <Your SubID> -ResourceGroupName KeyVault -Location westus -VaultName MikhegnVault -CertificateName VMSSCert -Password VmssCert -CreateSelfSignedCertificate -DnsName vmss.mikhegn.azure.com -OutputPath c:\users\mikhegn\desktop\
    ```

    Bu komut hello Azure Resource Manager şablonu için giriş hello olanağı sağlar.

    Bir örneğini nasıl otomatik olarak imzalanan bir sertifika bir anahtar kasasına toocreate görmek için [Service Fabric kümesi güvenlik senaryoları](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/).

2.  Merhaba Resource Manager şablonu değiştirin.

    Bu özellik çok ekleme**virtualMachineProfile**, hello bir parçası olarak, kaynak sanal makine ölçek kümesi:

    ```json 
    "osProfile": {
        "computerNamePrefix": "[variables('namingInfix')]",
        "adminUsername": "[parameters('adminUsername')]",
        "adminPassword": "[parameters('adminPassword')]",
        "secrets": [
            {
                "sourceVault": {
                    "id": "[resourceId('KeyVault', 'Microsoft.KeyVault/vaults', 'MikhegnVault')]"
                },
                "vaultCertificates": [
                    {
                        "certificateUrl": "https://mikhegnvault.vault.azure.net:443/secrets/VMSSCert/20709ca8faee4abb84bc6f4611b088a4",
                        "certificateStore": "My"
                    }
                ]
            }
        ]
    }
    ```
  

### <a name="can-i-specify-an-ssh-key-pair-toouse-for-ssh-authentication-with-a-linux-virtual-machine-scale-set-from-a-resource-manager-template"></a>SSH kimlik doğrulaması için bir SSH anahtar çifti toouse Resource Manager şablonu ayarlamak Linux sanal makine ölçek ile belirtebilirsiniz?  

Evet. Merhaba REST API için **osProfile** benzer toohello standart VM REST API'dır. 

Dahil **osProfile** şablonunuzda:

```json 
"osProfile": {
    "computerName": "[variables('vmName')]",
    "adminUsername": "[parameters('adminUserName')]",
    "linuxConfiguration": {
        "disablePasswordAuthentication": "true",
        "ssh": {
            "publicKeys": [
                {
                    "path": "[variables('sshKeyPath')]",
                    "keyData": "[parameters('sshKeyData')]"
                }
            ]
        }
    }
}
```
 
Bu JSON bloğu kullanılan [hello 101 vm sshkey GitHub Hızlı Başlangıç şablonu](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).
 
Merhaba işletim sistemi profili de kullanılıyor [hello grelayhost.json GitHub hızlı başlatma şablonunu](https://github.com/ExchMaster/gadgetron/blob/master/Gadgetron/Templates/grelayhost.json).

Daha fazla bilgi için bkz: [oluştur veya güncelleştir bir sanal makine ölçek kümesi](https://msdn.microsoft.com/library/azure/mt589035.aspx#linuxconfiguration).
  

### <a name="how-do-i-remove-deprecated-certificates"></a>Kullanım dışı sertifikaları nasıl kaldırılsın mı? 

tooremove sertifikalar, hello kasası sertifikalar listesinden Kaldır hello eski sertifika kullanım dışı. Bilgisayarınızda hello listesinde tooremain istediğiniz tüm hello sertifikaları bırakın. Bu hello sertifikayı, tüm VM'lerin kaldırmaz. Ayrıca hello sertifika toonew hello sanal makine ölçek kümesindeki oluşturulan VM'ler eklemez. 

Varolan vm'lerden tooremove hello sertifika, sertifika deposundan uzantı toomanually Kaldır hello sertifikaları özel bir komut dosyası yazma.
 
### <a name="how-do-i-inject-an-existing-ssh-public-key-into-hello-virtual-machine-scale-set-ssh-layer-during-provisioning-i-want-toostore-hello-ssh-public-key-values-in-azure-key-vault-and-then-use-them-in-my-resource-manager-template"></a>Nasıl ı mevcut bir SSH ortak anahtarı hello sanal makine ölçek kümesi SSH katmana sağlama sırasında Ekle? Toostore hello SSH ortak anahtarı değerleri Azure anahtar kasası istediğiniz ve bunları my Resource Manager şablonunu kullanın.

Genel SSH anahtarı ile yalnızca bir hello VM'ler sağlıyorsanız tooput hello ortak anahtarlar, anahtar kasasında gerekmez. Ortak anahtarlar gizli değildir.
 
Bir Linux VM oluşturduğunuzda SSH ortak anahtarları düz metin sağlayabilirsiniz:

```json
"linuxConfiguration": {
    "ssh": {
        "publicKeys": [
            {
                "path": "path",
                "keyData": "publickey"
            }
        ]
    }
```
 
linuxConfiguration öğe adı | Gerekli | Tür | Açıklama
--- | --- | --- | --- |  ---
SSH | Hayır | Koleksiyon | Merhaba SSH anahtar yapılandırması Linux işletim sistemi belirtir
Yol | Evet | Dize | Burada hello SSH anahtarlarını veya sertifika yerleştirilmelidir hello Linux dosya yolunu belirtir
anahtar verileri | Evet | Dize | Bir base64 ile kodlanmış SSH ortak anahtarını belirtir

Bir örnek için bkz: [hello 101 vm sshkey GitHub Hızlı Başlangıç şablonu](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).

 
### <a name="when-i-run-update-azurermvmss-after-adding-more-than-one-certificate-from-hello-same-key-vault-i-see-hello-following-message"></a>I çalıştırdığınızda `Update-AzureRmVmss` birden fazla sertifika hello ekledikten sonra aynı kasası, görüyorum anahtarın hello ileti:
 
>Update-AzureRmVmss: /subscriptions/ < my abonelik-kimliği > yinelenen örnekleri listesi gizli içeren / devre dışı bırakılmış resourceGroups/internal-rg-dev/providers/Microsoft.KeyVault/vaults/internal-keyvault-dev.
 
Toore çalışırsanız, bu durum oluşabilir-aynı kasa hello mevcut kaynak kasası için yeni bir kasa sertifika kullanmak yerine hello ekleyin. Merhaba `Add-AzureRmVmssSecret` komutu düzgün çalışmaz ek gizli ekliyorsanız.
 
tooadd hello öğesinden daha fazla gizli aynı anahtar kasası, güncelleştirme hello $vmss.properties.osProfile.secrets[0].vaultCertificates listesi.
 
Giriş yapısında Hello beklenen için bkz: [bir sanal makine oluştur veya güncelleştir kümesi](https://msdn.microsoft.com/library/azure/mt589035.aspx).
 
Merhaba gizli hello anahtar kasasına hello sanal makine ölçek kümesi nesnesi bulabilirsiniz. Ardından, hello kasayla ilişkili sertifikayı başvurusu (Merhaba URL ve hello gizli deposu adı) toohello listenize ekleyin.

> [!NOTE] 
> Şu anda hello sanal makine ölçek kümesi API'sini kullanarak sertifikaları Vm'lerden kaldıramazsınız.
>

Yeni VM'ler hello eski sertifika sahip olmaz. Ancak, hello sertifikası varsa ve hangi zaten dağıtılan VM'ler hello eski sertifika gerekir.
 
### <a name="can-i-push-certificates-toohello-virtual-machine-scale-set-without-providing-hello-password-when-hello-certificate-is-in-hello-secret-store"></a>Sertifikaları toohello sanal makineyi ölçeği hello sertifika hello gizli deposunda olduğunda hello parola sağlamadan Ayarla itme?

Komut dosyaları toohard kod parolalarda gerekmez. Dinamik olarak parolaları almak hello izinlerle toorun hello dağıtım komut dosyası kullanın. Bir sertifika hello gizli deposu anahtar Kasası'nı taşır bir komut dosyası varsa, gizli deposu hello `get certificate` komut ayrıca hello parola hello .pfx dosyasının çıkarır.
 
### <a name="how-does-hello-secrets-property-of-virtualmachineprofileosprofile-for-a-virtual-machine-scale-set-work-why-do-i-need-hello-sourcevault-value-when-i-have-toospecify-hello-absolute-uri-for-a-certificate-by-using-hello-certificateurl-property"></a>Bir sanal makine ölçek virtualMachineProfile.osProfile hello gizli özelliği iş nasıl ayarlamak? Merhaba certificateUrl özelliğini kullanarak bir sertifika için mutlak URI hello toospecify olduğunda neden hello sourceVault değeri gerekiyor? 

Windows Uzaktan Yönetim (WinRM) sertifika başvurusu hello hello işletim sistemi profili gizli özelliği mevcut olması gerekir. 

Merhaba amacı hello kaynak kasası belirten bir kullanıcının Azure bulut hizmeti modeli kayıtlı tooenforce erişim denetimi listesi (ACL) İlkeleri ' dir. Merhaba kaynak kasası belirtilmezse, izinleri toodeploy veya erişim gizli tooa anahtar kasası sahip olmayan kullanıcıların mümkün toothrough işlem kaynak sağlayıcısı (CRP) olacaktır. ACL'ler bile mevcut kaynakları için mevcut.

Yanlış kaynak kasa kimliği geçerli anahtar kasası URL'si ancak sağlarsanız, hello işlemi yoklama zaman bir hata bildirilir.
 
### <a name="if-i-add-secrets-tooan-existing-virtual-machine-scale-set-are-hello-secrets-injected-into-existing-vms-or-only-into-new-ones"></a>Sanal makine ölçek kümesi varolan gizli tooan eklerseniz, hello gizli VM'ler, veya yalnızca yenilerini eklenen? 

Sertifikaları tooall eklenen bile olanları önceden var olan Vm'leriniz. UpgradePolicy özelliği, sanal makine ölçek kümesi çok ayarlanır**el ile**, hello sertifika hello VM üzerinde el ile güncelleştirme gerçekleştirdiğinizde toohello VM eklendi.
 
### <a name="where-do-i-put-certificates-for-linux-vms"></a>Linux VM'ler için burada sertifikaları put?

Linux VM'ler için toodeploy sertifikaları nasıl görürüm toolearn [sertifikaları tooVMs müşteri tarafından yönetilen bir anahtar Kasası'ndan dağıtmak](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/).
  
### <a name="how-do-i-add-a-new-vault-certificate-tooa-new-certificate-object"></a>Yeni kasa sertifika tooa yeni bir sertifika nesnesi nasıl eklenir?

tooadd bir kasa sertifika tooan varolan gizlilik hello aşağıdaki PowerShell örneğine bakın. Yalnızca bir gizli nesnesi kullanın.
 
```powershell
$newVaultCertificate = New-AzureRmVmssVaultCertificateConfig -CertificateStore MY -CertificateUrl https://sansunallapps1.vault.azure.net:443/secrets/dg-private-enc/55fa0332edc44a84ad655298905f1809
 
$vmss.VirtualMachineProfile.OsProfile.Secrets[0].VaultCertificates.Add($newVaultCertificate)
 
Update-AzureRmVmss -VirtualMachineScaleSet $vmss -ResourceGroup $rg -Name $vmssName
```
 
### <a name="what-happens-toocertificates-if-you-reimage-a-vm"></a>Bir VM yeniden görüntü oluşturma toocertificates ne olur?

Bir VM yeniden görüntü oluşturma sertifikaları silinir. Siler hello tüm işletim sistemi diski yeniden görüntüsünü oluşturuyor. 
 
### <a name="what-happens-if-you-delete-a-certificate-from-hello-key-vault"></a>Bir sertifika hello anahtar Kasası'nı silersem ne olur?

Merhaba gizli anahtar Kasası'hello silinir ve ardından çalıştırırsanız `stop deallocate` tüm VM'ler için ve sonra yeniden başlatın, bir hatayla karşılaşırsınız. Merhaba CRP tooretrieve hello gizli hello anahtar Kasası'ndan gerekiyor, ancak bu işlem gerçekleştirilemiyor Hello hatası oluşur. Bu senaryoda, hello sanal makine ölçek kümesi modelden hello sertifikaları silebilirsiniz. 

Merhaba CRP bileşen müşteri gizli kalmaz. Çalıştırırsanız `stop deallocate` hello sanal makine ölçek kümesindeki tüm VM'ler için hello önbellek silinir. Bu senaryoda, gizli anahtar Kasası'hello alınır.

Azure Service Fabric hello gizliliği (modelindeki hello tek doku Kiracı) önbelleğe alınmış bir kopyasını olduğundan ölçeğini olduğunda bu sorunla karşılaştığınızda yok.
 
### <a name="why-do-i-have-toospecify-hello-exact-location-for-hello-certificate-url-httpsname-of-hello-vaultvaultazurenet443secretsexact-location-as-indicated-in-service-fabric-cluster-security-scenarioshttpsazuremicrosoftcomdocumentationarticlesservice-fabric-cluster-security"></a>Neden toospecify hello hello sertifika URL'si için tam olarak konum sahibim (https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>) belirtilen gibi [Service Fabric kümesi güvenlik senaryoları](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/)?
 
Hello Azure anahtar kasası belgelerine hello sürüm belirtilmezse, gizli anahtarı REST API alma hello gizli hello en son sürüm döndürmelidir bu hello belirtir.
 
Yöntem | URL
--- | ---
AL | https://mykeyvault.Vault.Azure.NET/Secrets/ {gizli-adı} / {gizli-version}? api-version = {api-version}

Değiştirin {*gizli anahtarı adı*} hello adı ve Değiştir {*gizli sürüm*} hello hello gizli sürümüyle tooretrieve istiyor. Merhaba gizli sürüm dışarıda. Bu durumda, hello geçerli sürümü alınır.
  
### <a name="why-do-i-have-toospecify-hello-certificate-version-when-i-use-key-vault"></a>Anahtar kasası kullandığınızda neden toospecify hello sertifika sürümü var mı?

Merhaba anahtar kasası gereksinim toospecify hello sertifika sürümü Hello amacı, hangi sertifikanın Vm'leri üzerinde dağıtılan toohello kullanıcı işaretini toomake budur.

Bir VM oluşturun ve ardından hello anahtar kasasına gizli güncelleştirirseniz hello yeni sertifika indirilen tooyour VM'ler değil. Ancak, sanal makineleri ve yeni VM'ler hello yeni parolası mı almak tooreference görünür. tooavoid Bu, gerekli tooreference gizli bir sürümü olan.

### <a name="my-team-works-with-several-certificates-that-are-distributed-toous-as-cer-public-keys-what-is-hello-recommended-approach-for-deploying-these-certificates-tooa-virtual-machine-scale-set"></a>Ekibin toous .cer ortak anahtarlar olarak dağıtılan birkaç sertifika çalışır. Bu sertifikalar tooa sanal makine ölçek kümesini dağıtmak için bir yaklaşım önerilir hello nedir?

toodeploy .cer ortak anahtarları tooa sanal makine ölçek kümesi, yalnızca .cer dosyaları içeren bir .pfx dosyası oluşturabilirsiniz. toodo Bu, kullanım `X509ContentType = Pfx`. Örneğin, C# veya PowerShell x509Certificate2 nesne olarak hello .cer dosyasını yüklemek ve ardından hello yöntemini çağırın. 

Daha fazla bilgi için bkz: [X509Certificate.Export yöntemi (X509ContentType, dize)](https://msdn.microsoft.com/library/24ww6yzk(v=vs.110.aspx)).

### <a name="i-do-not-see-an-option-for-users-toopass-in-certificates-as-base64-strings-most-other-resource-providers-have-this-option"></a>Kullanıcıların toopass sertifikaları için bir seçenek base64 dize olarak görmüyorum. Çoğu diğer kaynak sağlayıcıları bu seçeneğiniz vardır.

bir sertifika bir base64 dizesi olarak geçirme tooemulate hello en son sürümü tutulan URL bir Resource Manager şablonu ayıklayabilirsiniz. Resource Manager şablonu JSON özelliğinde aşağıdaki hello şunları içerir:

```json 
"certificateUrl": "[reference(resourceId(parameters('vaultResourceGroup'), 'Microsoft.KeyVault/vaults/secrets', parameters('vaultName'), parameters('secretName')), '2015-06-01').secretUriWithVersion]"
```
 
### <a name="do-i-have-toowrap-certificates-in-json-objects-in-key-vaults"></a>Toowrap sertifikaları JSON nesnelerindeki anahtar kasalarını içinde gerekiyor?

Sanal makine ölçek kümeleri ve sanal makineleri, sertifikaları JSON nesneleri alınmalıdır. 

Ayrıca hello içerik türü uygulama/x-pkcs12 destekliyoruz. Uygulama/x-pkcs12 kullanma ile ilgili yönergeler için bkz: [Azure anahtar kasası PFX sertifikaları](http://www.rahulpnath.com/blog/pfx-certificate-in-azure-key-vault/).
 
Şu anda .cer dosyaları desteklemiyoruz. toouse .cer, dışarı aktarma dosyaları bunları .pfx kapsayıcılarına.



## <a name="compliance"></a>Uyumluluk

### <a name="are-virtual-machine-scale-sets-pci-compliant"></a>Sanal makine ölçek PCI uyumlu ayarlar misiniz?

Sanal makine ölçek kümeleri hello CRP üstünde basit bir API katmandır. Her iki bileşenin hello işlem platformunda hello Azure hizmeti ağacında bir parçasıdır.

Uyumluluk açısından bakıldığında, sanal makine ölçek kümeleri hello Azure işlem platformu, temel bir parçasıdır. Bir takım, araçları, işlemler, dağıtım yöntemi, güvenlik denetimleri, yalnızca saat (JIT) derleme, izleme, uyarı ve benzeri hello CRP ile kendini paylaştıkları. Sanal makine ölçek kümeleri olan ödeme kartı endüstrisi (PCI)-hello CRP hello geçerli PCI veri güvenliği standardı (DSS) kanıtlama parçası olduğundan uyumlu.

Daha fazla bilgi için bkz: [Microsoft Trust Center hello](https://www.microsoft.com/TrustCenter/Compliance/PCI).






## <a name="extensions"></a>Uzantılar

### <a name="how-do-i-delete-a-virtual-machine-scale-set-extension"></a>Bir sanal makine ölçek kümesi uzantısının nasıl silebilirim?

bir sanal makine ölçek toodelete uzantısı, aşağıdaki PowerShell örneğine kullanım hello ayarlayın:

```powershell
$vmss = Get-AzureRmVmss -ResourceGroupName "resource_group_name" -VMScaleSetName "vmssName" 

$vmss=Remove-AzureRmVmssExtension -VirtualMachineScaleSet $vmss -Name "extensionName"

Update-AzureRmVmss -ResourceGroupName "resource_group_name" -VMScaleSetName "vmssName" -VirtualMacineScaleSet $vmss
```
 
Merhaba UzantıAdı değeri bulun `$vmss`.
   
### <a name="is-there-a-virtual-machine-scale-set-template-example-that-integrates-with-operations-management-suite"></a>Operations Management Suite ile tümleşir şablon örnek bir sanal makine ölçek kümesi var mı?

Operations Management Suite ile tümleşir şablon örnek bir sanal makine ölçek kümesi için hello ikinci örneğe bakın [Azure Service Fabric kümesi dağıtma ve günlük analizi kullanarak izlemeyi etkinleştir](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/ServiceFabric).
   
### <a name="extensions-seem-toorun-in-parallel-on-virtual-machine-scale-sets-this-causes-my-custom-script-extension-toofail-what-can-i-do-toofix-this"></a>Uzantılar, sanal makine ölçek kümeleri üzerinde paralel toorun gibi görünüyor. Bu, my özel betik uzantısı toofail neden olur. Toofix bu ne yapabilirim?

sanal makine ölçek kümesindeki uzantısı sıralama hakkında toolearn bkz [uzantısı sıralaması Azure sanal makine ölçek kümeleri](https://msftstack.wordpress.com/2016/05/12/extension-sequencing-in-azure-vm-scale-sets/).
 
 
### <a name="how-do-i-reset-hello-password-for-vms-in-my-virtual-machine-scale-set"></a>Nasıl ı hello parola VM'ler için my sanal makine ölçek kümesindeki sıfırlama?

tooreset hello Parolada VM'ler için sanal makine ölçek kümesi, VM erişimi uzantılarını kullanın. 

Aşağıdaki PowerShell örneğine hello kullan:

```powershell
$vmssName = "myvmss"
$vmssResourceGroup = "myvmssrg"
$publicConfig = @{"UserName" = "newuser"}
$privateConfig = @{"Password" = "********"}
 
$extName = "VMAccessAgent"
$publisher = "Microsoft.Compute"
$vmss = Get-AzureRmVmss -ResourceGroupName $vmssResourceGroup -VMScaleSetName $vmssName
$vmss = Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmss -Name $extName -Publisher $publisher -Setting $publicConfig -ProtectedSetting $privateConfig -Type $extName -TypeHandlerVersion "2.0" -AutoUpgradeMinorVersion $true
Update-AzureRmVmss -ResourceGroupName $vmssResourceGroup -Name $vmssName -VirtualMachineScaleSet $vmss
```
 
 
### <a name="how-do-i-add-an-extension-tooall-vms-in-my-virtual-machine-scale-set"></a>My sanal makine ölçek kümesindeki nasıl uzantısı tooall VM'ler eklensin mi?

Güncelleştirme ilkesi çok ayarlarsanız**otomatik**, hello şablonla dağıtarak hello yeni uzantısı özellikleri tüm VM'ler güncelleştirir.

Güncelleştirme ilkesi çok ayarlarsanız**el ile**hello uzantısı güncelleştirin ve sonra tüm örneklerde Vm'leriniz el ile güncelleştirin.

  
### <a name="if-hello-extensions-associated-with-an-existing-virtual-machine-scale-set-are-updated-are-existing-vms-affected-that-is-will-hello-vms-not-match-hello-virtual-machine-scale-set-model-or-are-they-ignored-when-an-existing-machine-is-service-healed-or-reimaged-are-hello-scripts-that-are-currently-configured-on-hello-virtual-machine-scale-set-executed-or-are-hello-scripts-that-were-configured-when-hello-vm-was-first-created-used"></a>Varolan bir sanal makine ölçek kümesi ile ilişkilendirilmiş hello uzantılarını güncelleştirilmişse, etkilenen VM'ler mevcut olan? (Diğer bir deyişle, VM'ler hello *değil* eşleşme hello sanal makine ölçek kümesi modelinde?) Veya göz ardı edilir? Var olan bir makine hizmet gösteriyor başlatıldığı ya da şu anda yürütülen hello sanal makine ölçek kümesinde yapılandırılmış hello komut dosyaları veya VM ilk oluşturulduğunda hello kullanıldığında yapılandırılmış hello betiklerdir?

Merhaba uzantısı hello sanal makine ölçek tanımında ayarlarsanız modeli güncelleştirilir ve hello upgradePolicy özelliği çok ayarlayın**otomatik**, hello VM'ler güncelleştirir. Merhaba upgradePolicy özelliği çok ayarlanmışsa**el ile**, uzantıları işaretlenen hello modeli eşleşmeyen olarak. 

Mevcut bir VM'yi hizmet gösteriyor ise, yeniden başlatma görünür ve hello uzantıları değil yeniden çalıştırın. Bunu yeniden, bu gibi ise hello işletim sistemi sürücüsü hello kaynak görüntü değiştirme. Uzantılar gibi hello son modelinden herhangi uzmanlık çalıştırılır.
 
### <a name="how-do-i-join-a-virtual-machine-scale-set-tooan-azure-ad-domain"></a>Nasıl bir sanal makine ölçek kümesi tooan Azure AD etki alanına katılacak mısınız?

bir sanal makine ölçek kümesi tooan Azure Active Directory (Azure AD) etki toojoin, bir uzantı tanımlayabilirsiniz. 

toodefine bir uzantı hello JsonADDomainExtension özelliğini kullanın:

```json
"extensionProfile": {
    "extensions": [
        {
            "name": "joindomain",
            "properties": {
                "publisher": "Microsoft.Compute",
                "type": "JsonADDomainExtension",
                "typeHandlerVersion": "1.3",
                "settings": {
                    "Name": "[parameters('domainName')]",
                    "OUPath": "[variables('ouPath')]",
                    "User": "[variables('domainAndUsername')]",
                    "Restart": "true",
                    "Options": "[variables('domainJoinOptions')]"
                },
                "protectedsettings": {
                    "Password": "[parameters('domainJoinPassword')]"
                }
            }
        }
    ]
}
```
 
### <a name="my-virtual-machine-scale-set-extension-is-trying-tooinstall-something-that-requires-a-reboot-for-example-commandtoexecute-powershellexe--executionpolicy-unrestricted-install-windowsfeature-name-fs-resource-manager-includemanagementtools"></a>My sanal makine ölçek kümesi uzantısı yeniden başlatma gerektiren bir şey tooinstall çalışıyor. Örneğin, "commandToExecute": "powershell.exe - ExecutionPolicy Unrestricted Install-WindowsFeature – AD FS-Resource-Manager – Includemanagementtools"

Sanal makine ölçek kümesi uzantınızı tooinstall bir yeniden başlatma gerektiren bir şey çalışırsa, hello Azure Otomasyonu istenen durum yapılandırması (Automation DSC) uzantısı kullanabilirsiniz. Merhaba işletim sistemi Windows Server 2012 R2 ise, Azure hello Windows Management Framework (WMF) 5.0 Kurulumu, yeniden başlatmalar çeker ve hello yapılandırma ile devam eder. 
 
### <a name="how-do-i-turn-on-antimalware-in-my-virtual-machine-scale-set"></a>My sanal makine ölçek kümesindeki nasıl üzerinde kötü amaçlı yazılımdan koruma dışı?

kötü amaçlı yazılımdan koruma, sanal makine ölçekte üzerinde tooturn ayarlamak, aşağıdaki PowerShell örneğine hello kullanın:

```powershell
$rgname = 'autolap'
$vmssname = 'autolapbr'
$location = 'eastus'
 
# Retrieve hello most recent version number of hello extension.
$allVersions= (Get-AzureRmVMExtensionImage -Location $location -PublisherName "Microsoft.Azure.Security" -Type "IaaSAntimalware").Version
$versionString = $allVersions[($allVersions.count)-1].Split(".")[0] + "." + $allVersions[($allVersions.count)-1].Split(".")[1]
 
$VMSS = Get-AzureRmVmss -ResourceGroupName $rgname -VMScaleSetName $vmssname
echo $VMSS
Add-AzureRmVmssExtension -VirtualMachineScaleSet $VMSS -Name "IaaSAntimalware" -Publisher "Microsoft.Azure.Security" -Type "IaaSAntimalware" -TypeHandlerVersion $versionString
Update-AzureRmVmss -ResourceGroupName $rgname -Name $vmssname -VirtualMachineScaleSet $VMSS 
```

### <a name="i-need-tooexecute-a-custom-script-thats-hosted-in-a-private-storage-account-hello-script-runs-successfully-when-hello-storage-is-public-but-when-i-try-toouse-a-shared-access-signature-sas-it-fails-this-message-is-displayed-missing-mandatory-parameters-for-valid-shared-access-signature-linksas-works-fine-from-my-local-browser"></a>Özel depolama hesabında barındırılan özel bir komut dosyası tooexecute ihtiyacım. Merhaba komut dosyasını başarıyla hello depolama genel olduğunda, ancak toouse bir paylaşılan erişim imzası (SAS) çalıştığınızda çalıştırır, başarısız olur. Bu ileti görüntülenir: "için geçerli paylaşılan erişim imzası zorunlu parametreler eksik". Bağlantı + SAS yerel Bilgisayarım tarayıcıdan düzgün çalışır.

tooexecute özel depolama hesabı, barındırılan özel bir komut dosyası hello depolama hesabı anahtarı ve ad ile korumalı ayarlarını ayarlayın. Daha fazla bilgi için bkz: [için özel betik uzantısı Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/#template-example-for-a-windows-vm-with-protected-settings).







## <a name="networking"></a>Ağ
 
### <a name="is-it-possible-tooassign-a-network-security-group-nsg-tooa-scale-set-so-that-it-will-apply-tooall-hello-vm-nics-in-hello-set"></a>Ağ güvenlik grubu (NSG) tooa ölçek kümesi, olası tooassign, böylelikle hello kümesindeki tooall hello VM NIC'ler uygulanır?

Evet. Merhaba Networkınterfaceconfiguration hello ağ profilinin bölümünde başvurarak tooa ölçek kümesi doğrudan bir ağ güvenlik grubu uygulanabilir. Örnek:

```json
"networkProfile": {
    "networkInterfaceConfigurations": [
        {
            "name": "nic1",
            "properties": {
                "primary": "true",
                "ipConfigurations": [
                    {
                        "name": "ip1",
                        "properties": {
                            "subnet": {
                                "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                            }
                "loadBalancerInboundNatPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                                }
                            ],
                            "loadBalancerBackendAddressPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                                 }
                            ]
                        }
                    }
                ],
                "networkSecurityGroup": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/networkSecurityGroups/', variables('nsgName'))]"
                }
            }
        }
    ]
}
```

### <a name="how-do-i-do-a-vip-swap-for-virtual-machine-scale-sets-in-hello-same-subscription-and-same-region"></a>Ne yapmalıyım bir VIP takası hello aynı sanal makine ölçek ayarlar için abonelik ve aynı bölgede?

Varsa iki sanal makine ölçek Azure yük dengeleyici ön uç ile ayarlar ve bulundukları aynı abonelikte ve bölgede Merhaba, her biri hello ortak IP adreslerini serbest bırakma ve toohello diğer Ata. Bkz: [VIP takası: Mavi yeşil dağıtım Azure Kaynak Yöneticisi'nde](https://msftstack.wordpress.com/2017/02/24/vip-swap-blue-green-deployment-in-azure-resource-manager/) örneğin. Hello kaynakları hello ağ düzeyinde serbest ve ayrılan. ancak bu bir gecikme anlamına gelmez. Toouse Azure uygulama ağ geçidi iki arka uç havuzları ve yönlendirme kuralı ile çok daha hızlı seçenektir. Alternatif olarak, uygulamanız ile barındırabilir [Azure uygulama hizmeti](https://azure.microsoft.com/en-us/services/app-service/) hazırlama ve üretim yuvası arasında hızlı geçişi için destek sağlar.
 
### <a name="how-do-i-specify-a-range-of-private-ip-addresses-toouse-for-static-private-ip-address-allocation"></a>Özel IP adresleri toouse özel statik IP adresi ayırma için bir aralığı nasıl belirtin?

IP adresleri, belirttiğiniz bir alt ağdan seçilir. 

sanal makine ölçek kümesi IP adreslerinin Hello ayırma yöntemi her zaman "dinamik" olmakla birlikte, bu IP adreslerine değiştirebilirsiniz anlamına gelmez. Bu durumda, "dinamik" yalnızca bir PUT İsteği hello IP adresi belirtmeyin anlamına gelir. Merhaba statik Hello alt kullanarak belirtin. 
    
### <a name="how-do-i-deploy-a-virtual-machine-scale-set-tooan-existing-azure-virtual-network"></a>Bir sanal makine ölçek kümesi tooan mevcut Azure sanal ağı nasıl dağıtırım? 

toodeploy bir sanal makine ölçek kümesi tooan mevcut Azure sanal ağı, bkz: [bir sanal makine ölçek kümesi tooan varolan sanal ağı dağıtmak](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-existing-vnet). 

### <a name="how-do-i-add-hello-ip-address-of-hello-first-vm-in-a-virtual-machine-scale-set-toohello-output-of-a-template"></a>Başlangıç IP adresi nasıl ekleyebilirim Merhaba bir sanal makine ölçek ilk VM şablonu toohello çıkış ayarlamak?

bir sanal makine ölçek kümesi toohello çıktıda bir şablonu ilk VM hello tooadd hello IP adresini bakın [ARM: Get VMSS'ın özel IP](http://stackoverflow.com/questions/42790392/arm-get-vmsss-private-ips).

### <a name="can-i-use-scale-sets-with-accelerated-networking"></a>Ölçek kümesi ağ hızlandırılmış kullanabilir miyim?

Evet. Hızlandırılmış toouse ağ iletişimi, Ölçek enableAcceleratedNetworking tootrue kümenin Networkınterfaceconfiguration ayarları ayarlayın. Örneğin
```json
"networkProfile": {
    "networkInterfaceConfigurations": [
    {
        "name": "niconfig1",
        "properties": {
        "primary": true,
        "enableAcceleratedNetworking" : true,
        "ipConfigurations": [
                ]
            }
            }
        ]
        }
    }
    ]
}
```

### <a name="how-can-i-configure-hello-dns-servers-used-by-a-scale-set"></a>Ölçek kümesi tarafından kullanılan hello DNS sunucularının nasıl yapılandırabilir miyim?

toocreate özel bir DNS yapılandırması ile VM ölçek kümesi, bir dnsSettings JSON paket toohello ölçek kümesi Networkınterfaceconfiguration bölüm ekleyin. Örnek:
```json
    "dnsSettings":{
        "dnsServers":["10.0.0.6", "10.0.0.5"]
    }
```

### <a name="how-can-i-configure-a-scale-set-tooassign-a-public-ip-address-tooeach-vm"></a>Ölçek kümesi tooassign ortak bir IP adresi tooeach VM nasıl yapılandırabilir miyim?

VM ölçek kümesi toocreate atar genel bir IP adresi tooeach VM hello Microsoft.Compute/virtualMAchineScaleSets kaynak hello API sürümü 2017-03-30 olduğundan emin olun ve Ekle bir _publicipaddressconfiguration_ JSON paket toohello ölçek Ipconfigurations bölümünde ayarlayın. Örnek:

```json
    "publicipaddressconfiguration": {
        "name": "pub1",
        "properties": {
        "idleTimeoutInMinutes": 15
        }
    }
```

### <a name="can-i-configure-a-scale-set-toowork-with-multiple-application-gateways"></a>Birden çok uygulama ağ geçitleri ile ölçek kümesi toowork yapılandırabilir miyim?

Evet. Merhaba kaynak kimliği için birden çok uygulama ağ geçidi arka uç adres havuzu toohello ekleyebilirsiniz _applicationGatewayBackendAddressPools_ hello listesinde _Ipconfigurations_ ölçek kümenizi bölümü Ağ profili.

## <a name="scale"></a>Ölçek

### <a name="in-what-case-would-i-create-a-virtual-machine-scale-set-with-fewer-than-two-vms"></a>Hangi durumda ı ikiden VM'ler ile ayarlamak bir sanal makine ölçek oluşturacak?

Nedenlerinden biri toocreate toouse hello esnek özelliklerini bir sanal makine ölçek kümesi bir sanal makine ölçek ikiden VM'ler ile ayarlayın. Örneğin, maliyetleri çalıştıran VM ödeme olmadan bir sanal makine ölçek kümesi sıfır VM'ler toodefine ile altyapınızın dağıtabilirsiniz. Hazır toodeploy VM'ler olduğunda, daha sonra hello "kapasitesini" Merhaba sanal makine ölçek kümesi toohello üretim örnek sayısı artırın.

Bir sanal makineyi ölçeği ikiden VM'ler ile Ayarla oluşturabilirsiniz başka bir, kullanılabilirlik ile ayrık VM'ler kümesi kullanarak kullanılabilirlik az endişe olup olmadığınızı nedenidir. Sanal makine ölçek kümeleri, yolu toowork fungible protokole işlem birimleri ile sağlar. Sanal makine ölçek kümeleri kullanılabilirlik kümeleri karşı temel fark yatan unsur bu bütünlüğünü olur. Çok sayıda durum bilgisiz iş yükleri tek tek birim izlemez. Merhaba iş yükü düşerse tooone işlem birimi ölçeklendirmek ve hello iş yükü arttığında toomany ölçeklendirin.

### <a name="how-do-i-change-hello-number-of-vms-in-a-virtual-machine-scale-set"></a>Merhaba bir sanal makine ölçek kümesindeki VM'lerin sayısını nasıl değişiyor?

bir sanal makine ölçek kümesindeki sanal makineleri toochange hello numarasını görmek [değiştirmek, bir sanal makine ölçek kümesinin hello örnek sayısı](https://msftstack.wordpress.com/2016/05/13/change-the-instance-count-of-an-azure-vm-scale-set/).

### <a name="how-do-i-define-custom-alerts-for-when-certain-thresholds-are-reached"></a>Belirli eşikleri dolduğunda özel uyarılar nasıl tanımlamak?

Belirtilen eşikler için uyarıları nasıl işleneceğini bazı esneklik bulunur. Örneğin, özelleştirilmiş Web kancalarını tanımlayabilirsiniz. Aşağıdaki Web kancası örneğine hello Resource Manager şablonu şöyledir:

```json
{
    "type": "Microsoft.Insights/autoscaleSettings",
    "apiVersion": "[variables('insightsApi')]",
    "name": "autoscale",
    "location": "[parameters('resourceLocation')]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]"
    ],
    "properties": {
        "name": "autoscale",
        "targetResourceUri": "[concat('/subscriptions/',subscription().subscriptionId, '/resourceGroups/',  resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]",
        "enabled": true,
        "notifications": [
            {
                "operation": "Scale",
                "email": {
                    "sendToSubscriptionAdministrator": true,
                    "sendToSubscriptionCoAdministrators": true,
                    "customEmails": [
                        "youremail@address.com"
                    ]
                },
                "webhooks": [
                    {
                        "serviceUri": "https://events.pagerduty.com/integration/0b75b57246814149b4d87fa6e1273687/enqueue",
                        "properties": {
                            "key1": "custommetric",
                            "key2": "scalevmss"
                        }
                    }
                ]
            }
        ],
```

Bu örnekte, bir Eşiğe ulaşıldığında uyarı tooPagerduty.com gider.



## <a name="patching-and-operations"></a>Düzeltme eki ve işlemleri

### <a name="how-do-i-create-a-scale-set-in-an-existing-resource-group"></a>Varolan bir kaynak grubundaki bir ölçek nasıl oluşturulur?

Ölçek kümeleri oluşturma var olan bir kaynak grubu henüz hello Azure portal ' mümkün değil, ancak bir ölçek dağıtma bir Azure Resource Manager şablonu ayarladığınızda var olan bir kaynak grubunu belirtebilirsiniz. Varolan bir kaynak grubu, Azure PowerShell veya CLI kullanarak bir ölçek oluştururken de belirtebilirsiniz.

### <a name="can-we-move-a-scale-set-tooanother-resource-group"></a>Tooanother kaynak grubu bir ölçek kümesi taşıyabilir miyim?

Evet, Ölçek kümesi kaynakları tooa yeni abonelik veya kaynak grubu taşıyabilirsiniz.

### <a name="how-tooi-update-my-virtual-machine-scale-set-tooa-new-image-how-do-i-manage-patching"></a>TooI güncelleştirme nasıl tooa yeni görüntüsü my sanal makine ölçek kümesi? Düzeltme eki uygulama nasıl yönetebilirim?

sanal makine ölçek kümesi tooa yeni görüntü ve toomanage düzeltme eki uygulama, tooupdate bkz [bir sanal makine ölçek kümesini yükseltme](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-upgrade-scale-set).

### <a name="can-i-use-hello-reimage-operation-tooreset-a-vm-without-changing-hello-image-that-is-i-want-reset-a-vm-toofactory-settings-rather-than-tooa-new-image"></a>Merhaba yeniden görüntü oluşturma işlemi tooreset VM hello görüntüyü değiştirmeden kullanabilir miyim? (Diğer bir deyişle, bir VM toofactory ayarları sıfırlama istiyorum tooa yeni görüntüsü yerine.)

Evet, hello görüntüyü değiştirmeden hello yeniden görüntü oluşturma işlemi tooreset VM kullanabilirsiniz. Sanal makine ölçek kümesi varsa ancak, platform görüntüsü ile başvuran `version = latest`, VM'yi tooa güncelleştirebilirsiniz sonraki işletim sistemi yansımasını çağırdığınızda `reimage`.

Daha fazla bilgi için bkz: [bir sanal makine ölçek kümesindeki tüm sanal makineleri yönetme](https://docs.microsoft.com/rest/api/virtualmachinescalesets/manage-all-vms-in-a-set).



## <a name="troubleshooting"></a>Sorun giderme

### <a name="how-do-i-turn-on-boot-diagnostics"></a>Önyükleme tanılaması nasıl kapatırım?

önyükleme tanılaması üzerinde tooturn ilk olarak, bir depolama hesabı oluşturun. Ardından, bu JSON bloğu, sanal makine ölçek kümesindeki put **virtualMachineProfile**ve hello sanal makine ölçek kümesini güncelleştir:

```json
"diagnosticsProfile": {
    "bootDiagnostics": {
        "enabled": true,
        "storageUri": "http://yourstorageaccount.blob.core.windows.net"
    }
}
```

Yeni VM oluşturulduğunda, hello hello VM InstanceView özelliği hello ekran görüntüsü vb. için hello ayrıntıları gösterir. Örnek aşağıda verilmiştir:
 
```json
"bootDiagnostics": {
    "consoleScreenshotBlobUri": "https://o0sz3nhtbmkg6geswarm5.blob.core.windows.net/bootdiagnostics-swarmagen-4157d838-8335-4f78-bf0e-b616a99bc8bd/swarm-agent-9574AE92vmss-0_2.4157d838-8335-4f78-bf0e-b616a99bc8bd.screenshot.bmp",
    "serialConsoleLogBlobUri": "https://o0sz3nhtbmkg6geswarm5.blob.core.windows.net/bootdiagnostics-swarmagen-4157d838-8335-4f78-bf0e-b616a99bc8bd/swarm-agent-9574AE92vmss-0_2.4157d838-8335-4f78-bf0e-b616a99bc8bd.serialconsole.log"
  }
```


## <a name="virtual-machine-properties"></a>Sanal makine özellikleri

### <a name="how-do-i-get-property-information-for-each-vm-without-making-multiple-calls-for-example-how-would-i-get-hello-fault-domain-for-each-of-hello-100-vms-in-my-virtual-machine-scale-set"></a>Her VM için özellik bilgilerini birden fazla çağrı yapmadan nasıl sağlarım? Örneğin, hello hata etki alanı her hello için 100 VM'ler my sanal makine ölçek kümesindeki nereden?

birden çok aramaları yapmadan her VM tooget özellik bilgilerini, çağırabilir `ListVMInstanceViews` bir REST API yaparak `GET` kaynak URI'si aşağıdaki hello üzerinde:

/Subscriptions/ < ABONELİK_KİMLİĞİ > /resourceGroups/ < resource_group_name > /providers/Microsoft.Compute/virtualMachineScaleSets/ < scaleset_name > / virtualMachines? $expand = instanceView & $select = instanceView

### <a name="can-i-pass-different-extension-arguments-toodifferent-vms-in-a-virtual-machine-scale-set"></a>Bir sanal makine ölçek kümesindeki toodifferent VM'ler t farklı uzantı bağımsız değişkenler geçirebilirsiniz?

Hayır, farklı uzantı bağımsız bir sanal makine ölçek kümesindeki toodifferent sanal makineleri geçiremezsiniz. Ancak, uzantıları hello benzersiz hello gibi hello makine adı olarak çalışan VM özelliklerini bağlı olarak çalışabilir. Uzantıları hello VM hakkında daha fazla bilgi http://169.254.169.254 tooget örneği meta sorgulama yapabilirsiniz.

### <a name="why-are-there-gaps-between-my-virtual-machine-scale-set-vm-machine-names-and-vm-ids-for-example-0-1-3"></a>Neden my sanal makine ölçek kümesi VM makine adları ve VM kimlikleri arasında boşluklar var mı? Örneğin: 0, 1, 3...

Sanal makine ölçek kümesi için sanal makine ölçek kümesi VM makine adları ve VM kimlikleri arasında boşluklar olan **overprovision** özelliği toohello varsayılan değer olarak ayarlanmış **doğru**. İşleminin çok ayarlanırsa**doğru**, oluşturulan istenenden daha fazla VM'ler. Ek VM'ler silinir. Bu durumda, artırılmış dağıtım güvenilirlik elde ancak hello gider ve bitişik adlandırma bitişik ağ adresi çevirisi (NAT) kuralları. 

Bu özellik çok ayarlayabilirsiniz**false**. Küçük sanal makine ölçek kümeleri için bu dağıtım güvenilirlik önemli ölçüde etkilemez.

### <a name="what-is-hello-difference-between-deleting-a-vm-in-a-virtual-machine-scale-set-and-deallocating-hello-vm-when-should-i-choose-one-over-hello-other"></a>Bir sanal makine ölçek kümesindeki VM silme ve hello VM serbest bırakma arasındaki hello fark nedir? Merhaba diğer üzerinde ne zaman seçmeniz gerekir?

Merhaba bir sanal makine ölçek kümesindeki VM silme ve hello VM serbest bırakma arasındaki temel fark olan `deallocate` hello sanal sabit diskleri (VHD) silmez. İle çalışmaya ilişkin depolama maliyetleri vardır `stop deallocate`. Kullanın ya da diğer nedenler aşağıdaki hello biri için hello:

- İşlem maliyetleri ödeme toostop istiyor, ancak tookeep hello disk hello VM'ler durumunu istiyorsunuz.
- Toostart VM'ler kümesi bir sanal makine ölçek kümesi ölçeklendirme daha hızlı istiyor.
  - İlgili toothis senaryosu, kendi otomatik ölçeklendirme altyapısı ve istediğiniz daha hızlı uçtan uca ölçek oluşturmuş olabileceğiniz.
- Düz olmayan şekilde hata etki alanları veya güncelleştirme etki alanları arasında dağıtılan bir sanal makine ölçek kümesine sahiptir. Bu, seçmeli olarak VM'ler silinmiş veya VM'ler işleminin sonra silindi nedeniyle, olabilir. Çalışan `stop deallocate` arkasından `start` hello sanal makinede ölçeği eşit Ayarla hello VM'ler hata etki alanları veya güncelleştirme etki alanları arasında dağıtır.

