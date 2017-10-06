---
title: "aaaManage toplu işlem hesabı hello istemci kitaplığı için .NET - Azure kaynaklarıyla | Microsoft Docs"
description: "Oluşturma, silme ve Azure Batch hesabı kaynaklarını hello Batch yönetimi .NET kitaplığı ile değiştirin."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 16279b23-60ff-4b16-b308-5de000e4c028
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/24/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 638d8129f3841ffcfb2e10f5d531a319bcbb7701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-batch-accounts-and-quotas-with-hello-batch-management-client-library-for-net"></a>.NET için Batch hesaplarını ve kotalarını hello Batch Yönetimi istemci kitaplığı ile yönetme

> [!div class="op_single_selector"]
> * [Azure portal](batch-account-create-portal.md)
> * [Batch Yönetimi .NET](batch-management-dotnet.md)
> 
> 

Bakım yükü Azure Batch uygulamalarınızda hello kullanarak düşürün [Batch yönetimi .NET] [ api_mgmt_net] kitaplığı tooautomate Batch hesabı oluşturma, silme, anahtar yönetimi ve kota bulma.

* **Oluşturma ve toplu işlem hesaplarını silme** hiçbir bölge içinde. İçinde her ayrı bir toplu işlem hesabı faturalama amacıyla atanır, istemciler için bir hizmet, örneğin, bir bağımsız yazılım satıcısı (ISV) sağlarsanız, hesap oluşturma ve silme özellikleri tooyour müşteri portalı ekleyebilirsiniz.
* **Almak ve hesabı anahtarlarını yeniden** program aracılığıyla toplu hesaplarınızdan herhangi birinin için. Düzenli geçiş veya hesabı anahtarları süre sonu zorlayan güvenlik ilkeleriyle uyumlu yardımcı olabilir. Çeşitli Azure bölgelerinde birçok Batch hesapları varsa, bu geçiş işlemi Otomasyon çözümünüzün verimliliğini artırır.
* **Hesap kotalarını denetleyin** ve hangi sınırları hangi Batch hesaplarınızın belirleme dışında hello deneme yanılma konusunda güvenilir bilgiler gerçekleştirin. İşler başlamadan önce hesap kotalarını denetleyerek, havuzları oluşturma veya işlem düğümleri eklemek, where proaktif olarak ayarlayabilir veya bu işlem kaynakları oluşturulur. Bu hesapların ek kaynakları ayırma önce kota artırır hangi hesapların gerektirdiği belirleyebilirsiniz.
* **Diğer Azure hizmetleriyle özelliklerini birleştirme** Batch yönetimi .NET kullanarak tam özellikli yönetim deneyimi-- [Azure Active Directory][aad_about]ve hello [Azure Resource Manager] [ resman_overview] hello bir araya aynı uygulama. Bu özellikler ve bunların API'lerini kullanarak, uyumlu kimlik doğrulama deneyimi sağlamak, özelliği toocreate hello ve kaynak grupları ve uçtan uca yönetim çözümünü için yukarıda açıklanan hello özellikleri silin.

> [!NOTE]
> Bu makalede toplu hesaplar, anahtarları ve kotalar hello programlı yönetimini odaklanmakla birlikte, birçok bu etkinliklerin hello kullanarak gerçekleştirebilirsiniz [Azure portal][azure_portal]. Daha fazla bilgi için bkz: [hello Azure portal kullanarak bir Azure Batch hesabı oluşturma](batch-account-create-portal.md) ve [hello Azure Batch hizmeti için kotalar ve sınırlar](batch-quota-limit.md).
> 
> 

## <a name="create-and-delete-batch-accounts"></a>Oluşturma ve toplu işlem hesaplarını silme
Belirtildiği gibi hello birincil özelliklerinden biri hello Batch yönetim API'si toocreate olduğundan ve bir Azure bölgesi toplu hesaplarında silin. Bu nedenle, toodo kullanmak [BatchManagementClient.Account.CreateAsync] [ net_create] ve [DeleteAsync][net_delete], ya da zaman uyumlu dekiler.

Merhaba aşağıdaki kod parçacığını bir hesabı oluşturur, yeni hesabı Batch hizmeti hello oluşturulan hello alır ve ardından siler. Bu parçacığında bulunan ve diğerlerinin bu makalede, hello `batchManagementClient` tamamen başlatılmış bir örneğinin [BatchManagementClient][net_mgmt_client].

```csharp
// Create a new Batch account
await batchManagementClient.Account.CreateAsync("MyResourceGroup",
    "mynewaccount",
    new BatchAccountCreateParameters() { Location = "West US" });

// Get hello new account from hello Batch service
AccountResource account = await batchManagementClient.Account.GetAsync(
    "MyResourceGroup",
    "mynewaccount");

// Delete hello account
await batchManagementClient.Account.DeleteAsync("MyResourceGroup", account.Name);
```

> [!NOTE]
> Merhaba Batch yönetimi .NET kitaplığı ve onun BatchManagementClient sınıfını kullanan uygulamaları gerektiren **Hizmet Yöneticisi** veya **Abonelikteki** erişim hello sahibi toohello abonelik Toplu işlem hesabı toobe yönetilen. Merhaba daha fazla bilgi için bkz: [Azure Active Directory](#azure-active-directory) bölümü ve hello [AccountManagement] [ acct_mgmt_sample] kod örneği.
> 
> 

## <a name="retrieve-and-regenerate-account-keys"></a>Almak ve hesabı anahtarlarını yeniden oluştur
Kullanarak birincil ve ikincil hesabı anahtarları, abonelik içindeki herhangi bir toplu işlem hesabı elde [ListKeysAsync][net_list_keys]. Bu anahtarlar kullanarak yeniden [RegenerateKeyAsync][net_regenerate_keys].

```csharp
// Get and print hello primary and secondary keys
BatchAccountListKeyResult accountKeys =
    await batchManagementClient.Account.ListKeysAsync(
        "MyResourceGroup",
        "mybatchaccount");
Console.WriteLine("Primary key:   {0}", accountKeys.Primary);
Console.WriteLine("Secondary key: {0}", accountKeys.Secondary);

// Regenerate hello primary key
BatchAccountRegenerateKeyResponse newKeys =
    await batchManagementClient.Account.RegenerateKeyAsync(
        "MyResourceGroup",
        "mybatchaccount",
        new BatchAccountRegenerateKeyParameters() {
            KeyName = AccountKeyType.Primary
            });
```

> [!TIP]
> Yönetim uygulamalarınız için kolaylaştırılmış bağlantı iş akışı oluşturabilirsiniz. İlk olarak, toomanage ile istediğiniz hesap anahtarı hello toplu işlem hesabı için elde [ListKeysAsync][net_list_keys]. Ardından, bu anahtarı hello Batch .NET kitaplığın başlatırken kullanmak [BatchSharedKeyCredentials] [ net_sharedkeycred] başlatılırken kullanılan sınıf [BatchClient] [net_batch_client].
> 
> 

## <a name="check-azure-subscription-and-batch-account-quotas"></a>Azure aboneliği ve toplu işlem hesabı kotası denetleyin
Azure abonelikleri ve tüm toplu gibi hello tek tek Azure Hizmetleri belirli varlıkları hello sayısı sınırı varsayılan kotalar sahiptir. Azure aboneliklerinin Hello varsayılan kotaları için bkz: [Azure aboneliği ve hizmet sınırları, kotaları ve kısıtlamaları](../azure-subscription-service-limits.md). Varsayılan kotaları Hello hello Batch hizmeti için bkz: [hello Azure Batch hizmeti için kotalar ve sınırlar](batch-quota-limit.md). Merhaba Batch yönetimi .NET kitaplığını kullanarak uygulamalarınızı bu kotalar kontrol edebilirsiniz. Hesapları ekleyin veya işlem kaynaklarını havuzları gibi ve işlem düğümleri önce bu toomake ayırma kararları sağlar.

### <a name="check-an-azure-subscription-for-batch-account-quotas"></a>Azure aboneliği toplu işlem hesabı kotası için denetleyin
Bir bölgede bir toplu işlem hesabı oluşturmadan önce Azure aboneliği toosee mümkün tooadd bu bölgede bulunan bir hesap olup denetleyebilirsiniz.

Merhaba aşağıdaki kod parçacığında, ilk kullanırız [BatchManagementClient.Account.ListAsync] [ net_mgmt_listaccounts] tooget bir abonelik içinde olan tüm Batch hesaplarının bir koleksiyon. Bu koleksiyon elde sonra hello hedef bölgede kaç hesaplardır belirler. Kullanırız sonra [BatchManagementClient.Subscriptions] [ net_mgmt_subscriptions] tooobtain toplu işlem hesabı kotası hello ve bu bölgede kaç hesapları (varsa) oluşturulabilir belirleyin.

```csharp
// Get a collection of all Batch accounts within hello subscription
BatchAccountListResponse listResponse =
        await batchManagementClient.Account.ListAsync(new AccountListParameters());
IList<AccountResource> accounts = listResponse.Accounts;
Console.WriteLine("Total number of Batch accounts under subscription id {0}:  {1}",
    creds.SubscriptionId,
    accounts.Count);

// Get a count of all accounts within hello target region
string region = "westus";
int accountsInRegion = accounts.Count(o => o.Location == region);

// Get hello account quota for hello specified region
SubscriptionQuotasGetResponse quotaResponse = await batchManagementClient.Subscriptions.GetSubscriptionQuotasAsync(region);
Console.WriteLine("Account quota for {0} region: {1}", region, quotaResponse.AccountQuota);

// Determine how many accounts can be created in hello target region
Console.WriteLine("Accounts in {0}: {1}", region, accountsInRegion);
Console.WriteLine("You can create {0} accounts in hello {1} region.", quotaResponse.AccountQuota - accountsInRegion, region);
```

Yukarıdaki hello parçacığında bulunan `creds` örneği [TokenCloudCredentials][azure_tokencreds]. Bu nesne oluşturma örneği toosee hello bkz [AccountManagement] [ acct_mgmt_sample] kodu örneği github'daki.

### <a name="check-a-batch-account-for-compute-resource-quotas"></a>Bir Batch hesabında işlem kaynak kotaları denetleyin
Batch çözümündeki işlem kaynakları artırmadan önce tooallocate hello hesabın kotaları aşan olmaz istediğiniz tooensure hello kaynakların kontrol edebilirsiniz. Merhaba aşağıdaki kod parçacığında, biz hello kota bilgileri hello adlı toplu işlem hesabı için yazdırma `mybatchaccount`. Kendi uygulamanızda Hello hesap oluşturulan hello ek kaynaklar toobe işleyip işleyemediğine gibi bilgileri toodetermine kullanabilirsiniz.

```csharp
// First obtain hello Batch account
BatchAccountGetResponse getResponse =
    await batchManagementClient.Account.GetAsync("MyResourceGroup", "mybatchaccount");
AccountResource account = getResponse.Resource;

// Now print hello compute resource quotas for hello account
Console.WriteLine("Core quota: {0}", account.Properties.CoreQuota);
Console.WriteLine("Pool quota: {0}", account.Properties.PoolQuota);
Console.WriteLine("Active job and job schedule quota: {0}", account.Properties.ActiveJobAndJobScheduleQuota);
```

> [!IMPORTANT]
> Azure abonelikleri ve Hizmetleri için varsayılan kotaları olsa da, bu sınırları çoğunu hello istekte vererek yükseltilebilir [Azure portal][azure_portal]. Örneğin, [hello Azure Batch hizmeti için kotalar ve sınırlar](batch-quota-limit.md) toplu işlem hesabı kotası artırma hakkında yönergeler için.
> 
> 

## <a name="use-azure-ad-with-batch-management-net"></a>Azure AD Batch yönetimi .NET ile kullanma

Merhaba Batch yönetimi .NET kitaplığı bir Azure kaynak sağlayıcısı istemci ve ile birlikte kullanılan [Azure Resource Manager] [ resman_overview] toomanage kaynakları program aracılığıyla hesap. Azure AD olduğu ve hello Batch yönetimi .NET kitaplığı dahil olmak üzere tüm Azure kaynak sağlayıcısı istemci aracılığıyla yapılan gerekli tooauthenticate istekleri [Azure Resource Manager][resman_overview]. Azure AD hello Batch yönetimi .NET kitaplığı ile kullanma hakkında daha fazla bilgi için bkz: [kullanım Azure Active Directory tooauthenticate Batch çözümleri](batch-aad-auth.md). 

## <a name="sample-project-on-github"></a>Github'da örnek proje

toosee Batch yönetimi .NET eylem denetleyin hello [AccountManagment] [ acct_mgmt_sample] örnek proje github'da. Merhaba AccountManagment örnek uygulama işlemleri aşağıdaki hello gösterir:

1. Kullanarak Azure AD'den bir güvenlik belirtecini almak [ADAL][aad_adal]. Merhaba kullanıcı zaten oturum açmamış varsa, bunlar Azure kullanıcılardan kimlik bilgileri istenir.
2. Azure AD'den alınan hello güvenlik belirteciyle oluşturma bir [SubscriptionClient] [ resman_subclient] tooquery Azure hello hesabıyla ilişkilendirilmiş abonelik listesi. birden fazla aboneliğiniz varsa hello kullanıcı hello listesinden bir abonelik seçebilirsiniz.
3. Seçili hello abonelikle ilişkili kimlik bilgilerini alın.
4. Oluşturma bir [ResourceManagementClient] [ resman_client] hello kimlik bilgilerini kullanarak nesne.
5. Kullanım bir [ResourceManagementClient] [ resman_client] toocreate bir kaynak grubu nesnesi.
6. Kullanım bir [BatchManagementClient] [ net_mgmt_client] tooperform birkaç toplu hesap işlemleri nesnesi:
   * Toplu işlem hesabı hello yeni kaynak grubu oluşturun.
   * Hesabı Batch hizmeti hello yeni oluşturulan hello alın.
   * Merhaba hesabı anahtarları hello yeni hesap için yazdırın.
   * Merhaba hesabı için yeni bir birincil anahtar yeniden oluşturun.
   * Merhaba kota bilgileri hello hesabı için yazdırın.
   * Merhaba hello aboneliği için kota bilgilerini yazdırın.
   * Merhaba abonelik içindeki tüm hesapları yazdırın.
   * Yeni oluşturulan hesabı silin.
7. Merhaba kaynak grubunu silin.

Yeni oluşturulan hello toplu işlem hesabı ve kaynak grubu silmeden önce bunları hello görüntüleyebileceğiniz [Azure portal][azure_portal]:

toorun hello örnek uygulama başarıyla öncelikle bunu Azure AD kiracınızda hello Azure portal ve grant izinleri toohello Azure Kaynak Yöneticisi API'si ile kaydetmeniz gerekir. Sağlanan hello adımları [Active Directory ile kimlik doğrulaması toplu yönetim çözümleri](batch-aad-auth-management.md).


[aad_about]: ../active-directory/active-directory-whatis.md "Azure Active Directory nedir?"
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Azure AD için kimlik doğrulama senaryoları"
[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Uygulamaları Azure Active Directory ile tümleştirme"
[acct_mgmt_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/AccountManagement
[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_mgmt_net]: https://msdn.microsoft.com/library/azure/mt463120.aspx
[azure_portal]: http://portal.azure.com
[azure_storage]: https://azure.microsoft.com/services/storage/
[azure_tokencreds]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.tokencloudcredentials.aspx
[batch_explorer_project]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[net_batch_client]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_list_keys]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.accountoperationsextensions.listkeysasync.aspx
[net_create]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.accountoperationsextensions.createasync.aspx
[net_delete]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.accountoperationsextensions.deleteasync.aspx
[net_regenerate_keys]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.accountoperationsextensions.regeneratekeyasync.aspx
[net_sharedkeycred]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.auth.batchsharedkeycredentials.aspx
[net_mgmt_client]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.batchmanagementclient.aspx
[net_mgmt_subscriptions]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.batchmanagementclient.subscriptions.aspx
[net_mgmt_listaccounts]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.iaccountoperations.listasync.aspx
[resman_api]: https://msdn.microsoft.com/library/azure/mt418626.aspx
[resman_client]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.resources.resourcemanagementclient.aspx
[resman_subclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.subscriptions.subscriptionclient.aspx
[resman_overview]: ../azure-resource-manager/resource-group-overview.md

[1]: ./media/batch-management-dotnet/portal-01.png
[2]: ./media/batch-management-dotnet/portal-02.png
[3]: ./media/batch-management-dotnet/portal-03.png
