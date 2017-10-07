---
ms.assetid: 
title: "aaaAzure anahtar kasası - toouse yumuşak delete CLI ile nasıl"
description: "Kullanım örneği soft-delete CLI kod parçalarını ile örnekleri"
author: BrucePerlerMS
manager: mbaldwin
ms.service: key-vault
ms.topic: article
ms.workload: identity
ms.date: 08/04/2017
ms.author: bruceper
ms.openlocfilehash: 672f5210ab119c244ca712f0bb80b653b50ea79b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-key-vault-soft-delete-with-cli"></a>Nasıl toouse anahtar kasası soft-delete CLI ile

Azure anahtar Kasası'nın geçici silme özelliği silinen kasalarını ve kasa nesneleri kurtarılmasını sağlar. Özellikle, soft-senaryoları aşağıdaki adresleri hello Sil:

- Bir anahtar kasası kurtarılabilir silinmesini desteği
- Anahtar kasası nesnelerin kurtarılabilir silinmesi desteği; , gizli anahtarları ve sertifikaları

## <a name="prerequisites"></a>Ön koşullar

- Azure CLI, ortamınız için bu kurulumu yoksa 2.0 - bkz [yönetmek anahtar CLI 2.0 kullanan kasası](key-vault-manage-with-cli2.md).

CLI için anahtar kasası belirli başvuru bilgileri için bkz: [Azure CLI 2.0 anahtar kasası başvuru](https://docs.microsoft.com/cli/azure/keyvault).

## <a name="required-permissions"></a>Gerekli izinler

Anahtar kasası işlemleri ayrı olarak aracılığıyla rol tabanlı erişim denetimi (RBAC) izinleri gibi yönetilen:

| İşlem | Açıklama | Kullanıcı izni |
|:--|:--|:--|
|Liste|Listeleri anahtar kasalarını silindi.|Microsoft.KeyVault/deletedVaults/read|
|Kurtar|Silinen bir anahtar kasası geri yükler.|Microsoft.KeyVault/vaults/write|
|Temizle|Kalıcı olarak silinmiş bir anahtar kasası ve tüm içeriğini kaldırır.|Microsoft.KeyVault/locations/deletedVaults/purge/action|

İzinler ve erişim denetimi hakkında daha fazla bilgi için bkz: [anahtar kasanızı güvenli](key-vault-secure-your-key-vault.md).

## <a name="enabling-soft-delete"></a>Etkinleştirme soft-Sil

Silinen bir anahtar kasası ya da bir anahtar olarak depolanan nesneler toobe mümkün toorecover kasa, önce bu anahtar kasası için geçici silme etkinleştirmeniz gerekir.

### <a name="existing-key-vault"></a>Varolan anahtar kasası

ContosoVault adlı bir var olan anahtar kasasının için geçici silme gibi etkinleştirin. 

>[!NOTE]
>Şu anda toouse Azure Resource Manager kaynak işleme toodirectly yazma hello gereksiniminiz *enableSoftDelete* özelliği toohello anahtar kasası kaynak.

```azurecli
az resource update --id $(az keyvault show --name ContosoVault -o tsv | awk '{print $1}') --set properties.enableSoftDelete=true
```

### <a name="new-key-vault"></a>Yeni anahtar kasası

Yeni bir anahtar kasası için geçici silmeyi etkinleştirme yapılır tooyour hello soft-delete etkinleştirme bayrağını ekleyerek oluşturma zamanında komutu oluşturun.

```azurecli
az keyvault create --name ContosoVault --resource-group ContosoRG --enable-soft-delete true --location westus
```

### <a name="verify-soft-delete-enablement"></a>Soft-delete etkinleştirme doğrulayın

bir anahtar kasası soft-delete etkin olan tooverify çalışma hello *Göster* komut ve Merhaba 'Yumuşak silme etkin?' arayın özniteliği ve onun ayarı true veya false.

```azurecli
az keyvault show --name ContosoVault
```

## <a name="deleting-a-key-vault-protected-by-soft-delete"></a>Soft-delete tarafından korunan bir anahtar kasasını silme

Merhaba komutu toodelete (veya kaldırma) bir anahtar kasası aynı ancak etkinleştirilip bağlı olarak, davranış değişiklikleri yumuşak veya silme hello kalır.

```azurecli
az keyvault delete --name ContosoVault
```

> [!IMPORTANT]
>Soft-delete etkin olmayan bir anahtar kasası için hello önceki komutu çalıştırırsanız, bu anahtar kasası ve tüm içeriğini kurtarma seçenekleri olmadan kalıcı olarak siler.

### <a name="how-soft-delete-protects-your-key-vaults"></a>Soft-delete anahtar kasalarınıza nasıl korur

Soft-delete ile etkin:

- Bir anahtar kasası silindiğinde, kendi kaynak grubundan kaldırılmış olduğundan ve yalnızca ayrılmış bir ad alanında yerleştirildiğinden onu oluşturulduğu hello konumu ile ilişkili. 
- Silinen anahtar nesneleri gibi anahtarları, gizli ve sertifikalar erişilemeyen kasa ve bunların içeren anahtar kasası silinmiş hello durumundayken bunu kalır. 
- aynı ada sahip yeni bir anahtar kasası oluşturulamıyor şekilde hello DNS adı silinmiş bir durumda bir anahtar kasası için ayrılmış olarak kalır.  

Merhaba aşağıdaki komutu kullanarak, aboneliğinizle ilişkili silinen durumu anahtar kasalarını görüntüleyebilirsiniz:

```azurecli
az keyvault list-deleted
```

Merhaba *kaynak kimliği* hello çıktı toohello özgün kaynak kimliği bu kasasının başvuruyor. Bu anahtar kasasında şimdi silinmiş durumda olduğundan, bu kaynak kimliği ile hiçbir kaynak yok Merhaba *kimliği* alan kurtarma ya da temizleme kullanılan tooidentify hello kaynak olabilir. Merhaba *temizleme tarih zamanlanmış* alan gösterir hello kasası zaman kalıcı olarak silinecek (temizlendi) bu silinen kasa için bir eylem varsa. Merhaba varsayılan saklama dönemi, kullanılan toocalculate hello *temizleme tarih zamanlanmış*, 90 gündür.

## <a name="recovering-a-key-vault"></a>Bir anahtar kasası kurtarma

toorecover bir anahtar kasası, toospecify hello anahtar kasası adı, kaynak grubunu ve konumu gerekir. Bu bir anahtar kasası kurtarma işlemi için gerek duyduğunuz hello konum ve hello kaynak grubu silinmiş hello anahtar kasasının unutmayın.

```azurecli
az keyvault recover --location westus --name ContosoVault
```

Bir anahtar kasası kurtarıldığında hello sonuç hello anahtar kasasının özgün kaynak kimliğiyle yeni bir kaynak değildir Burada hello anahtar kasası var hello kaynak grubu kaldırdıysanız hello anahtar kasası kurtarılabilir önce aynı ada sahip yeni bir kaynak grubu oluşturulmalıdır.

## <a name="key-vault-objects-and-soft-delete"></a>Anahtar kasası nesneleri ve soft-Sil

İçin bir anahtar, 'ContosoFirstKey' yumuşak Sil ' ContosoVault etkin' adlı bir anahtar kasasının içinde burada nasıl, bu anahtarı silmeniz.

```azurecli
az keyvault key delete --name ContosoFirstKey --vault-name ContosoVault
```

İçin geçici silme etkin anahtar kasanız ile silinen anahtar görünmeye devam eder dışında silinmiş gibi açıkça listelemek veya silinen anahtarlarını alma. Merhaba silinmiş durumda bir anahtar üzerindeki çoğu işlemi silinen anahtar listeleme, bu kurtarma veya onu temizleme dışında başarısız olur. 

Örneğin, toorequest silinmiş toolist anahtarları bir anahtar Kasası'hello aşağıdaki komutu kullanın:

```azurecli
az keyvault key list-deleted --vault-name ContosoVault
```

### <a name="transition-state"></a>Durum geçişi 

Bir anahtar kasasına bir anahtar soft-etkin delete ile sildiğinizde, hello geçiş toocomplete birkaç saniye sürebilir. Bu durum geçişi sırasında bu hello anahtarı hello etkin veya hello silinmiş durumda değil görünebilir. Bu komut tüm silinen anahtarlarında 'ContosoVault' adlı anahtar kasanızı listeler.

```azurecli
az keyvault key list-deleted --vault-name ContosoVault
```

### <a name="using-soft-delete-with-key-vault-objects"></a>Anahtar kasası nesneleriyle Soft-delete kullanma

Kurtarma ya da onu temizleyebilirsiniz sürece yalnızca anahtar kasalarını, silinen bir anahtar gibi gizli veya, sertifika too90 günlerini silinmiş durumda kalır. 

#### <a name="keys"></a>Anahtarlar

Silinen bir anahtar toorecover:

```azurecli
az keyvault key recover --name ContosoFirstKey --vault-name ContosoVault
```

toopermanently bir anahtarı silin:

```azurecli
az keyvault key purge --name ContosoFirstKey --vault-name ContosoVault
```

>[!NOTE]
>Bir anahtar temizleme kalıcı olarak, kurtarılabilir olmaz anlamı silinir.

Merhaba **kurtarmak** ve **Temizleme** Eylemler bir anahtar kasası erişim ilkesinde ilişkili kendi izinlere sahiptir. Kullanıcı veya hizmet asıl toobe mümkün tooexecute için bir **kurtarmak** veya **Temizleme** gerekir iznine sahip oldukları hello ilgili (anahtar veya gizli) Bu nesne için hello anahtar kasası erişim ilkesinde eylem. Varsayılan olarak, hello **Temizleme** izni hello 'all' kısayol kullanılan toogrant olduğunda tooa anahtar kasasının erişim ilkesi eklenmez tüm izinleri tooa kullanıcı. Açıkça vermelidir **Temizleme** izni. Örneğin, aşağıdaki komut verir hello user@contoso.com izin tooperform anahtarlarında üzerinde çeşitli işlemler *ContosoVault* dahil olmak üzere **Temizleme**.

#### <a name="set-a-key-vault-access-policy"></a>Bir anahtar kasası erişim ilkesi ayarlama

```azurecli
az keyvault set-policy --name ContosoVault --key-permissions get create delete list update import backup restore recover purge
```

>[!NOTE] 
> Yalnızca etkin soft-delete oluşmuş olan bir anahtar kasası varsa, olmayabilir **kurtarmak** ve **Temizleme** izinleri.

#### <a name="secrets"></a>Gizli Diziler

Anahtarları gibi bir anahtar kasasına gizli anahtarları üzerinde kendi komutları ile çalıştırılan örnekleridir. Aşağıdaki, silme, listeleme, kurtarma ve gizli anahtarları Temizleme için hello komutlardır.

- SQLPassword adlı bir gizli anahtarı silin: 
```azurecli
az keyvault secret delete --vault-name ContosoVault -name SQLPassword
```

- Tüm silinen gizli bir anahtar kasasına listesi: 
```azurecli
az keyvault secret list-deleted --vault-name ContosoVault
```

- Bir gizli anahtar hello silinmiş durumda kurtarma: 
```azurecli
az keyvault secret recover --name SQLPassword --vault-name ContosoVault
```

- Bir gizli anahtar silinmiş durumda temizleme: 
```azurecli
az keyvault secret purge --name SQLPAssword --vault-name ContosoVault
```

>[!NOTE]
>Gizli temizleme kalıcı olarak, kurtarılabilir olmaz anlamı silinir.

## <a name="purging-and-key-vaults"></a>Temizleme ve anahtar kasalarını

### <a name="key-vault-objects"></a>Anahtar kasası nesneleri

Bir anahtar temizleme, gizli veya, sertifika kalıcı olarak, kurtarılabilir olmaz anlamına silinir. Merhaba anahtar Kasası'nda tüm diğer nesnelerin gibi hello Silinmiş nesne içeriyor hello anahtar kasası ancak değişmeden kalır. 

### <a name="key-vaults-as-containers"></a>Anahtar kapsayıcıları kasaları
Bir anahtar kasası temizlenir, tüm içeriğini anahtarları, gizli ve sertifikalar dahil olmak üzere kalıcı olarak silinir. toopurge bir anahtar kasası kullanan hello `az keyvault purge` komutu. Aboneliğinizin silinen anahtar kasalarını hello komutunu kullanarak hello konum bulabilir `az keyvault list-deleted`.

```azurecli
az keyvault purge --location westus --name ContosoVault
```

>[!NOTE]
>Bir anahtar kasası temizleme kalıcı olarak, kurtarılabilir olmaz anlamı silinir.

### <a name="purge-permissions-required"></a>Gerekli izinler Temizle
- toopurge silinmiş bir anahtar kasası, hello kasası ve tüm içeriğini kalıcı olarak kaldırılır şekilde hello kullanıcının ihtiyacı RBAC izni tooperform bir *Microsoft.KeyVault/locations/deletedVaults/purge/action* işlemi. 
- toolist silinmiş hello anahtar hello kasası kullanıcı gereken RBAC izni tooperform *Microsoft.KeyVault/deletedVaults/read* izni. 
- Varsayılan olarak yalnızca bir abonelik yöneticisinin bu izinlere sahiptir. 

### <a name="scheduled-purge"></a>Zamanlanmış temizleme

Silinen anahtar kasası nesneleri listeleme anahtar kasası tarafından temizlendi schedled toobe olduklarında gösterir. Merhaba *temizleme tarih zamanlanmış* alan gösterir ne zaman bir anahtar kasası nesnesi kalıcı olarak silinecek, hiçbir işlem yapılmadı. Varsayılan olarak, silinen anahtar kasası nesne hello saklama süresi 90 gündür.

>[!NOTE]
>Tarafından tetiklenen silinen kasası nesne, kendi *temizleme tarih zamanlanmış* alan, kalıcı olarak silinir. Kurtarılabilir değil.

## <a name="other-resources"></a>Diğer kaynaklar

- Anahtar Kasası'nın soft-delete özelliğine genel bakış için bkz: [Azure anahtar kasası soft-delete genel bakış](key-vault-ovw-soft-delete.md).
- Azure anahtar kasası kullanımı genel bir bakış için bkz: [Azure anahtar kasası ile çalışmaya başlama](key-vault-get-started.md).

