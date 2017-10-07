---
title: "Azure Batch kullanıcı hesaplarında aaaRun görevleri | Microsoft Docs"
description: "Azure toplu işlemde çalışan görevler için kullanıcı hesaplarını yapılandırma"
services: batch
author: tamram
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.openlocfilehash: 13d7d76451d89a3cca090c4ef24ed0ed781bbf09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-tasks-under-user-accounts-in-batch"></a>Toplu işlemde kullanıcı hesapları görevleri Çalıştır

Azure Batch görevinde her zaman bir kullanıcı hesabı altında çalışır. Varsayılan olarak, standart kullanıcı hesapları, yönetici izinleri olmayan altında görevlerini çalıştırın. Bu varsayılan kullanıcı hesabı ayarları genellikle yeterlidir. Bazı senaryolarda, ancak yararlı toobe mümkün tooconfigure hello kullanıcı hesabı altında görev toorun istediğiniz olur. Bu makalede, kullanıcı hesapları ve nasıl bunları senaryonuz için yapılandırabilirsiniz hello türleri açıklanmaktadır.

## <a name="types-of-user-accounts"></a>Kullanıcı hesabı türleri

Azure toplu işlem, görevleri çalıştırmak için iki tür kullanıcı hesabı sağlar:

- **Otomatik kullanıcı hesapları.** Otomatik kullanıcı hesapları hello Batch hizmeti tarafından otomatik olarak oluşturulan yerleşik kullanıcı hesaplarıdır. Varsayılan olarak, görevler bir otomatik kullanıcı hesabı altında çalışır. Merhaba otomatik kullanıcı belirtimi altında hangi otomatik kullanıcı hesabın bir görevin çalışması gereken bir görev tooindicate için yapılandırabilirsiniz. Merhaba otomatik kullanıcı belirtimi toospecify hello ayrıcalık düzeyinde ve kapsam hello görev çalıştıracak hello otomatik kullanıcı hesabının sağlar. 

- **Adlı bir kullanıcı hesabı.** Merhaba havuz oluşturduğunuzda havuz için bir veya daha fazla adlandırılmış kullanıcı hesapları belirtebilirsiniz. Her kullanıcı hesabı hello havuzunun her bir düğümde oluşturulur. Ayrıca toohello hesap adı, hello kullanıcı hesabı parolası, ayrıcalık düzeyi ve Linux havuzları, hello SSH özel anahtar belirtin. Bir görev eklediğinizde, kullanıcı hesabı altında bu görevin çalışması gerektiğini adlı hello belirtebilirsiniz.

> [!IMPORTANT] 
> Bu sürüm, kod toocall güncelleştirmenin gerektirdiği önemli bir değişiklik Hello Batch hizmeti sürümü 2017 01 01.4.0 tanıtır. Geçirme koddan toplu daha eski bir sürümü varsa, o hello Not **runElevated** özelliği hello REST API veya toplu istemci kitaplıkları artık desteklenmiyor. Kullanım hello yeni **Userıdentity** görev toospecify ayrıcalık düzeyi özelliği. Başlıklı hello bölümüne bakın [kod toohello en son toplu istemci Kitaplığı ', güncelleştirme](#update-your-code-to-the-latest-batch-client-library) hello istemci kitaplıklarından birini kullanıyorsanız, toplu kodunuzu güncelleştirmek için hızlı yönergeler için.
>
>

> [!NOTE] 
> Bu makalede açıklanan hello kullanıcı hesaplarına Uzak Masaüstü Protokolü (RDP) veya güvenli Kabuk (SSH), güvenlik nedenleriyle desteklemez. 
>
> tooconnect tooa düğüm çalışan hello Linux sanal makine yapılandırması, SSH aracılığıyla bkz [kullanım Uzak Masaüstü tooa Azure Linux VM'de](../virtual-machines/virtual-machines-linux-use-remote-desktop.md). RDP aracılığıyla Windows çalıştıran tooconnect toonodes bkz [tooa Windows Server VM bağlanmak](../virtual-machines/windows/connect-logon.md).<br /><br />
> tooconnect tooa düğümünde çalışan hello bulut hizmeti aracılığıyla yapılandırmaya RDP, bkz: [bir rolde Azure bulut Hizmetleri için Uzak Masaüstü Bağlantısı etkinleştirmek](../cloud-services/cloud-services-role-enable-remote-desktop-new-portal.md).
>
>

## <a name="user-account-access-toofiles-and-directories"></a>Kullanıcı hesabı erişimi toofiles ve dizinler

Bir otomatik kullanıcı hesabı ve adlı bir kullanıcı hesabı okuma/yazma erişimi toohello görevin çalışma dizini, paylaşılan dizine ve çok örnekli görevler dizini vardır. Her iki türdeki hesaba okuma erişimi toohello başlangıç ve iş hazırlama dizinler sahiptir.

Bir görev hello altında çalışıyorsa, çalıştırmak için bir başlangıç görevi, hello görev kullanılan aynı hesap okuma-yazma erişimi toohello başlangıç görevi dizini vardır. Benzer şekilde, aynı görevin altında çalışıyorsa hello çalıştırmak için bir iş hazırlama görevi, hello görev kullanılan hesap okuma-yazma erişimi toohello iş hazırlama görevi dizini vardır. Bir görev hello başlangıç görevi veya iş hazırlama görevi farklı bir hesap altında çalışıyorsa, hello görevin yalnızca okuma erişimi toohello ilgili dizini vardır.

Dosyalar ve dizinler görevden erişme hakkında daha fazla bilgi için bkz: [geliştirme büyük ölçekli paralel işlem çözümleri yığın](batch-api-basics.md#files-and-directories).

## <a name="elevated-access-for-tasks"></a>Görevler için yükseltilmiş erişim 

Hello kullanıcı hesabının ayrıcalık düzeyi, bir görevin yükseltilmiş erişim ile çalışıp çalışmayacağını gösterir. Bir otomatik kullanıcı hesabı ve adlı bir kullanıcı hesabı ile yükseltilmiş erişim çalıştırabilirsiniz. ayrıcalık düzeyi için iki seçenek Hello şunlardır:

- **NonAdmin:** hello görev, yükseltilmiş erişimi olmayan standart bir kullanıcı olarak çalışır. Toplu kullanıcı hesabı için Hello varsayılan ayrıcalık düzeyi olduğundan her zaman **NonAdmin**.
- **Yönetici:** hello görevi yükseltilmiş erişimi bir kullanıcı olarak çalışır ve tam yönetici izinlerine sahip çalışır. 

## <a name="auto-user-accounts"></a>Otomatik kullanıcı hesapları

Varsayılan olarak, görevler yükseltilmiş erişimi olmadan ve görev kapsamlı standart bir kullanıcı olarak bir otomatik kullanıcı hesabı altında toplu işlemde çalıştırın. Merhaba otomatik kullanıcı belirtimi görev kapsam için yapılandırıldığında, hello Batch hizmeti yalnızca bu görev için bir otomatik kullanıcı hesabı oluşturur.

Merhaba alternatif tootask kapsam havuzu kapsamıdır. Merhaba otomatik kullanıcı belirtimi bir görev için havuz kapsam için yapılandırıldığında, hello görev hello havuzunda kullanılabilir tooany görev bir otomatik kullanıcı hesabı altında çalışır. Başlıklı hello bölüme havuzu kapsamı hakkında daha fazla bilgi için bkz [otomatik kullanıcı havuzu kapsamlı hello gibi bir görevi çalıştırmayı](#run-a-task-as-the-autouser-with-pool-scope).   

Windows ve Linux düğümlerinde Hello varsayılan kapsam farklıdır:

- Windows düğümlerinde görevler varsayılan olarak görev kapsam altında çalışır.
- Linux düğümleri havuzu kapsam altında her zaman çalışır.

Her biri tooa benzersiz otomatik kullanıcı hesabına karşılık gelen hello otomatik kullanıcı belirtimi için dört olası yapılandırmaları vardır:

- Yönetici olmayan erişim görev kapsamlı (Merhaba varsayılan otomatik kullanıcı belirtimi)
- Görev kapsamlı yönetici (yükseltilmiş) erişimi
- Havuz kapsamlı yönetici olmayan erişim
- Havuz kapsamlı yönetici erişimi

> [!IMPORTANT] 
> Görev kapsam altında çalışan görevler gerçek erişim tooother görevleri bir düğümde sahip değilsiniz. Ancak, kötü niyetli bir kullanıcı erişimi toohello hesabıyla yönetici ayrıcalıklarıyla çalıştırır ve diğer görev dizinleri erişen bir görev göndererek bu kısıtlamaya işe yarayabilir. Kötü niyetli bir kullanıcının RDP veya SSH tooconnect tooa düğümünü de kullanabilirsiniz. Önemli tooprotect erişim tooyour Batch hesabı anahtarları tooprevent böyle bir senaryo değil. Hesabınızı tehlikeye şüpheleniyorsanız emin tooregenerate anahtarlarınızı olabilir.
>
>

### <a name="run-a-task-as-an-auto-user-with-elevated-access"></a>Yükseltilmiş erişimi olan bir otomatik kullanıcı olarak bir görevi çalıştırma

Toorun yükseltilmiş erişimi olan bir task gerektiğinde Merhaba otomatik kullanıcı belirtimi için yönetici ayrıcalıkları yapılandırabilirsiniz. Örneğin, bir başlangıç görevi hello düğümünde yükseltilmiş erişim tooinstall yazılımı gerekebilir.

> [!NOTE] 
> Genel olarak, en iyi toouse yükseltilmiş erişim yalnızca gerekli olduğunda. En iyi yöntemler hello en düşük ayrıcalık gerekli tooachieve hello istenen sonuca verme öneririz. Örneğin, bir başlangıç görevi hello geçerli kullanıcıya yönelik yazılımları yerine tüm kullanıcılar için yüklerse yükseltilmiş erişim tootasks verme mümkün tooavoid olabilir. Merhaba otomatik kullanıcı belirtimi hello aynı hello başlangıç görevi de dahil olmak üzere hesabı altında toorun gereken tüm görevler için havuz kapsamı ve yönetici olmayan erişim için yapılandırabilirsiniz. 
>
>

Aşağıdaki kod parçacıkları hello nasıl tooconfigure hello otomatik kullanıcı belirtimi gösterir. Merhaba örnekler set hello ayrıcalık düzeyi çok`Admin` ve kapsam çok hello`Task`. Görev kapsam hello varsayılan ayar, ancak örnek hello artırmak amacıyla için buraya dahil edilir.

#### <a name="batch-net"></a>Batch .NET

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin, scope: AutoUserScope.Task));
```
#### <a name="batch-java"></a>Batch Java

```java
taskToAdd.withId(taskId)
        .withUserIdentity(new UserIdentity()
            .withAutoUser(new AutoUserSpecification()
                .withElevationLevel(ElevationLevel.ADMIN))
                .withScope(AutoUserScope.TASK));
        .withCommandLine("cmd /c echo hello");                        
```

#### <a name="batch-python"></a>Batch Python

```python
user = batchmodels.UserIdentity(
    auto_user=batchmodels.AutoUserSpecification(
        elevation_level=batchmodels.ElevationLevel.admin,
        scope=batchmodels.AutoUserScope.task))
task = batchmodels.TaskAddParameter(
    id='task_1',
    command_line='cmd /c "echo hello world"',
    user_identity=user)
batch_client.task.add(job_id=jobid, task=task)
```

### <a name="run-a-task-as-an-auto-user-with-pool-scope"></a>Otomatik kullanıcı havuzu kapsamlı olarak bir görevi çalıştırma

Bir düğüm sağlandığında, iki havuzu genelinde otomatik-kullanıcı hesapları hello havuzdaki her düğüme, yükseltilmiş erişim biriyle ve yükseltilmiş erişimi olmadan bir oluşturulur. Belirli bir görev için Hello otomatik kullanıcının kapsam toopool kapsamı ayarlama hello görev bu iki havuzu genelinde otomatik-kullanıcı hesaplarından birini altında çalışır. 

Hello otomatik-kullanıcının havuzu kapsamını belirttiğinizde, yönetici erişimine sahip çalışan tüm görevler hello altında Çalıştır aynı havuzu genelinde otomatik-kullanıcı hesabı. Benzer şekilde, yönetici izinleri olmadan çalışan görevler de tek havuzu genelinde otomatik-kullanıcı hesabı altında çalışır. 

> [!NOTE] 
> Merhaba iki havuzu genelinde otomatik-kullanıcı hesapları ayrı hesaplarıdır. Merhaba havuzu genelinde yönetici hesabı altında çalışan görevler hello standart hesap altında ve tersi yönde çalışan görevler ile verileri paylaşamaz. 
>
>

aynı otomatik kullanıcı hesabı olan hello üzerinde çalışan diğer görevleri mümkün tooshare verilerle görevlerdir hello altında avantajı toorunning hello aynı düğüm.

Çalışan görevlerin hello iki havuzu genelinde otomatik-kullanıcı hesaplarından birini altında yararlı olduğu bir senaryo gizli görevler arasında paylaşımıdır. Örneğin, bir başlangıç görevi tooprovision diğer görevleri kullanabilirsiniz hello düğüm üzerine bir gizlilik gerektiğini varsayalım. Merhaba Windows Data Protection API (DPAPI) kullanabilirsiniz, ancak yönetici ayrıcalıkları gerekiyor. Bunun yerine, hello gizli hello kullanıcı düzeyinde koruyabilir. Aynı kullanıcı hesabı erişebilir hello altında çalışan görevler hello yükseltilmiş erişimi olmadan gizli anahtarı.

Başka bir senaryo toorun görevleri havuzu kapsamlı bir otomatik kullanıcı hesabı altında bozuk bir ileti geçirme arabirimi (MPI) dosyası istediğiniz paylaşır. Bir MPI dosya paylaşımı, aynı dosya verilerini hello MPI görev gerek toowork üzerinde Hello düğümler hello yararlıdır. Merhaba baş düğümü oluşturur hello altında çalışıyorsa, hello alt düğümleri erişebileceği bir dosya paylaşımı aynı otomatik kullanıcı hesabı. 

Aşağıdaki kod parçacığını hello hello otomatik kullanıcının kapsam toopool kapsamını bir görev için Batch .NET içinde ayarlar. Merhaba görev hello standart havuzu genelinde otomatik-kullanıcı hesabı altında çalışır şekilde hello ayrıcalık düzeyi atlandı.

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(scope: AutoUserScope.Pool));
```

## <a name="named-user-accounts"></a>Adlı kullanıcı hesapları

Bir havuz oluşturduğunuzda, adlandırılmış kullanıcı hesapları tanımlayabilirsiniz. Adlı bir kullanıcı hesabı adı ve sağladığınız parola sahiptir. Adlı bir kullanıcı hesabı için hello ayrıcalık düzeyi belirtebilirsiniz. Linux düğümleri için bir SSH özel anahtarı da sağlayabilir.

Merhaba havuzundaki tüm düğümlerde adlı bir kullanıcı hesabı var ve bu düğümlerde çalışan kullanılabilir tooall görevleri. Adlandırılmış kullanıcılar bir havuz için herhangi bir sayıda tanımlayabilir. Bir görevi veya görev koleksiyon eklediğinizde hello havuzunda tanımlanan kullanıcı hesapları adlı hello birini hello görev çalıştığı belirtebilirsiniz.

Adlı bir kullanıcı hesabı yararlıdır toorun istediğinizde işteki tüm görevler altında hello aynı kullanıcı hesabı, ancak diğer işleri Merhaba, çalışan görevleri birbirlerinden ayrı tutmak aynı anda. Örneğin, her iş için adlandırılmış bir kullanıcı oluşturun ve her iş görevlerinin bu adlı bir kullanıcı hesabı altında çalıştırın. Her bir iş, daha sonra kendi görevleri ile ancak diğer işlerin görevleri bir gizlilik paylaşabilirsiniz.

Adlı kullanıcı hesabı toorun dosya paylaşımları gibi dış kaynaklara izinlerini ayarlar, bir görev de kullanabilirsiniz. Adlı bir kullanıcı hesabı ile Merhaba kullanıcı kimliğini denetlemek ve bu kullanıcı kimliğini tooset izinleri kullanabilirsiniz.  

Adlı kullanıcı hesapları parola daha az SSH Linux düğümleri arasında sağlar. Toorun çok örnekli görevler gereken Linux düğümleri adlı bir kullanıcı hesabı kullanabilirsiniz. Merhaba havuzdaki her düğüme görevleri hello tüm havuzu üzerinde tanımlı bir kullanıcı hesabı altında çalışabilir. Çok örnekli görevler hakkında daha fazla bilgi için bkz: [çoklu kullanmak\-örneği görevleri toorun MPI uygulamaları](batch-mpi.md).

### <a name="create-named-user-accounts"></a>Adlı kullanıcı hesapları oluşturma

Toplu işlem, kullanıcı hesaplarında adlı toocreate kullanıcı hesapları toohello havuzu koleksiyonu ekleyin. Merhaba aşağıdaki kod parçacıkları nasıl toocreate kullanıcı hesaplarında .NET, Java ve Python adlı gösterir. Bu kod parçacıkları Göster nasıl toocreate yönetici ve bir havuz hesaplarında adlı yönetici olmayan. Hello örnekler hello bulut hizmet yapılandırması'nı kullanarak havuzları oluşturma, ancak aynı hello Sanal Makine Yapılandırması'nı kullanarak bir Windows veya Linux havuzu oluştururken yaklaşımını hello kullanın.

#### <a name="batch-net-example-windows"></a>Batch .NET örnek (Windows)

```csharp
CloudPool pool = null;
Console.WriteLine("Creating pool [{0}]...", poolId);

// Create a pool using hello cloud service configuration.
pool = batchClient.PoolOperations.CreatePool(
    poolId: poolId,
    targetDedicatedComputeNodes: 3,                                                         
    virtualMachineSize: "small",                                                
    cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "5"));   

// Add named user accounts.
pool.UserAccounts = new List<UserAccount>
{
    new UserAccount("adminUser", "xyz123", ElevationLevel.Admin),
    new UserAccount("nonAdminUser", "123xyz", ElevationLevel.NonAdmin),
};

// Commit hello pool.
await pool.CommitAsync();
```

#### <a name="batch-net-example-linux"></a>Batch .NET örnek (Linux)

```csharp
CloudPool pool = null;

// Obtain a collection of all available node agent SKUs.
List<NodeAgentSku> nodeAgentSkus =
    batchClient.PoolOperations.ListNodeAgentSkus().ToList();

// Define a delegate specifying properties of hello VM image toouse.
Func<ImageReference, bool> isUbuntu1404 = imageRef =>
    imageRef.Publisher == "Canonical" &&
    imageRef.Offer == "UbuntuServer" &&
    imageRef.Sku.Contains("14.04");

// Obtain hello first node agent SKU in hello collection that matches
// Ubuntu Server 14.04. 
NodeAgentSku ubuntuAgentSku = nodeAgentSkus.First(sku =>
    sku.VerifiedImageReferences.Any(isUbuntu1404));

// Select an ImageReference from those available for node agent.
ImageReference imageReference =
    ubuntuAgentSku.VerifiedImageReferences.First(isUbuntu1404);

// Create hello virtual machine configuration toouse toocreate hello pool.
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration(imageReference, ubuntuAgentSku.Id);

Console.WriteLine("Creating pool [{0}]...", poolId);

// Create hello unbound pool.
pool = batchClient.PoolOperations.CreatePool(
    poolId: poolId,
    targetDedicatedComputeNodes: 3,                                             
    virtualMachineSize: "Standard_A1",                                      
    virtualMachineConfiguration: virtualMachineConfiguration);                  

// Add named user accounts.
pool.UserAccounts = new List<UserAccount>
{
    new UserAccount(
        name: "adminUser",
        password: "xyz123",
        elevationLevel: ElevationLevel.Admin,
        linuxUserConfiguration: new LinuxUserConfiguration(
            uid: 12345,
            gid: 98765,
            sshPrivateKey: new Guid().ToString()
            )),
    new UserAccount(
        name: "nonAdminUser",
        password: "123xyz",
        elevationLevel: ElevationLevel.NonAdmin,
        linuxUserConfiguration: new LinuxUserConfiguration(
            uid: 45678,
            gid: 98765,
            sshPrivateKey: new Guid().ToString()
            )),
};

// Commit hello pool.
await pool.CommitAsync();
```


#### <a name="batch-java-example"></a>Batch Java örneği

```java
List<UserAccount> userList = new ArrayList<>();
userList.add(new UserAccount().withName(adminUserAccountName).withPassword(adminPassword).withElevationLevel(ElevationLevel.ADMIN));
userList.add(new UserAccount().withName(nonAdminUserAccountName).withPassword(nonAdminPassword).withElevationLevel(ElevationLevel.NONADMIN));
PoolAddParameter addParameter = new PoolAddParameter()
        .withId(poolId)
        .withTargetDedicatedNodes(POOL_VM_COUNT)
        .withVmSize(POOL_VM_SIZE)
        .withCloudServiceConfiguration(configuration)
        .withUserAccounts(userList);
batchClient.poolOperations().createPool(addParameter);
```

#### <a name="batch-python-example"></a>Batch Python örneği

```python
users = [
    batchmodels.UserAccount(
        name='pool-admin',
        password='******',
        elevation_level=batchmodels.ElevationLevel.admin)
    batchmodels.UserAccount(
        name='pool-nonadmin',
        password='******',
        elevation_level=batchmodels.ElevationLevel.nonadmin)
]
pool = batchmodels.PoolAddParameter(
    id=pool_id,
    user_accounts=users,
    virtual_machine_configuration=batchmodels.VirtualMachineConfiguration(
        image_reference=image_ref_to_use,
        node_agent_sku_id=sku_to_use),
    vm_size=vm_size,
    target_dedicated=vm_count)
batch_client.pool.add(pool)
```

### <a name="run-a-task-under-a-named-user-account-with-elevated-access"></a>Yükseltilmiş erişimle görevi adlı bir kullanıcı hesabı altında çalıştırma

toorun bir görev bir yükseltilmiş kullanıcının, ayarlanmış hello görevi olarak **Userıdentity** ile oluşturulan kullanıcı hesabı adlı özellik tooa kendi **ElevationLevel** çok ayarlanan özelliği`Admin`.

Bu kod parçacığını hello görev adlı bir kullanıcı hesabı altında çalışması gerektiğini belirtir. Merhaba havuzu oluşturulduğunda bu adlı bir kullanıcı hesabı hello havuzunda tanımlandı. Bu durumda, kullanıcı hesabı adlı hello yönetici izinlerine sahip oluşturuldu:

```csharp
CloudTask task = new CloudTask("1", "cmd.exe /c echo 1");
task.UserIdentity = new UserIdentity(AdminUserAccountName);
```

## <a name="update-your-code-toohello-latest-batch-client-library"></a>Kod toohello en son toplu istemci Kitaplığı ', güncelleştirme

Merhaba Batch hizmeti sürümü 2017 01 01.4.0 tanıtır hello değiştirme önemli bir değişiklik, **runElevated** özelliği hello ile önceki sürümlerde kullanılabilir **Userıdentity** özelliği. tabloları aşağıdaki Merhaba, eşleme bir basit tooupdate kodunuzu hello istemci kitaplıkları önceki sürümlerinden kullanabileceği sağlar.

### <a name="batch-net"></a>Batch .NET

| Kodunuzu kullanıyorsa...                  | Buna güncelleştirme...                                                                                                 |
|---------------------------------------|------------------------------------------------------------------------------------------------------------------|
| `CloudTask.RunElevated = true;`       | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin));`    |
| `CloudTask.RunElevated = false;`      | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.NonAdmin));` |
| `CloudTask.RunElevated`belirtilmemiş. | Güncelleştirme gerekmiyor                                                                                               |

### <a name="batch-java"></a>Batch Java

| Kodunuzu kullanıyorsa...                      | Buna güncelleştirme...                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `CloudTask.withRunElevated(true);`        | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.ADMIN));`    |
| `CloudTask.withRunElevated(false);`       | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.NONADMIN));` |
| `CloudTask.withRunElevated`belirtilmemiş. | Güncelleştirme gerekmiyor                                                                                                                     |

### <a name="batch-python"></a>Batch Python

| Kodunuzu kullanıyorsa...                      | Buna güncelleştirme...                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `run_elevated=True`                       | `user_identity=user`, burada <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.admin)) `                |
| `run_elevated=False`                      | `user_identity=user`, burada <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.nonadmin)) `             |
| `run_elevated`belirtilmemiş. | Güncelleştirme gerekmiyor                                                                                                                                  |


## <a name="next-steps"></a>Sonraki adımlar

### <a name="batch-forum"></a>Toplu işlem Forumu

Merhaba [Azure toplu işlem Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch) MSDN'de mükemmel toodiscuss toplu yerleştirin ve hello hizmeti hakkında soru sorun olduğunu. HEAD üzerinde üzerinden faydalı sabitlenmiş gönderiler için ve Batch çözümlerinizi derleme sırasında çıktıkları anda sorularınızı gönderin.
