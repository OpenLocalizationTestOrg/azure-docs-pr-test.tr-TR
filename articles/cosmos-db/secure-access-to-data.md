---
title: "aaaLearn nasıl toosecure erişim Azure Cosmos veritabanı toodata | Microsoft Docs"
description: "Azure Cosmos veritabanı ana anahtarları, salt okunur anahtarları, kullanıcılar ve izinler de dahil olmak üzere, erişim denetimi kavramları hakkında bilgi edinin."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 8641225d-e839-4ba6-a6fd-d6314ae3a51c
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: mimig
ms.openlocfilehash: fef7f8e14b488f6ceab0f2aa279a1e99d4416f08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="securing-access-tooazure-cosmos-db-data"></a><span data-ttu-id="db405-103">Erişim tooAzure Cosmos DB verilerin güvenliğini sağlama</span><span class="sxs-lookup"><span data-stu-id="db405-103">Securing access tooAzure Cosmos DB data</span></span>
<span data-ttu-id="db405-104">Bu makalede depolanan erişim toodata güvenli hale getirme genel bir bakış sağlar [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="db405-104">This article provides an overview of securing access toodata stored in [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span>

<span data-ttu-id="db405-105">Azure Cosmos DB anahtarları tooauthenticate kullanıcılar iki tür kullanır ve tooits verilere erişmek ve kaynaklar sağlar.</span><span class="sxs-lookup"><span data-stu-id="db405-105">Azure Cosmos DB uses two types of keys tooauthenticate users and provide access tooits data and resources.</span></span> 

|<span data-ttu-id="db405-106">Anahtar türü</span><span class="sxs-lookup"><span data-stu-id="db405-106">Key type</span></span>|<span data-ttu-id="db405-107">Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="db405-107">Resources</span></span>|
|---|---|
|[<span data-ttu-id="db405-108">Ana anahtarları</span><span class="sxs-lookup"><span data-stu-id="db405-108">Master keys</span></span>](#master-keys) |<span data-ttu-id="db405-109">Yönetim kaynaklar için kullanılan: veritabanı hesapları, veritabanları, kullanıcılar ve izinler</span><span class="sxs-lookup"><span data-stu-id="db405-109">Used for administrative resources: database accounts, databases, users, and permissions</span></span>|
|[<span data-ttu-id="db405-110">Kaynak belirteçleri</span><span class="sxs-lookup"><span data-stu-id="db405-110">Resource tokens</span></span>](#resource-tokens)|<span data-ttu-id="db405-111">Uygulama kaynakları için kullanılan: koleksiyonlar, belgeler, ekleri, saklı yordamlar, tetikleyiciler ve UDF'ler</span><span class="sxs-lookup"><span data-stu-id="db405-111">Used for application resources: collections, documents, attachments, stored procedures, triggers, and UDFs</span></span>|

<a id="master-keys"></a>

## <a name="master-keys"></a><span data-ttu-id="db405-112">Ana anahtarları</span><span class="sxs-lookup"><span data-stu-id="db405-112">Master keys</span></span> 

<span data-ttu-id="db405-113">Ana anahtarları erişim toohello hello veritabanı hesabı için tüm hello yönetim kaynaklar sağlar.</span><span class="sxs-lookup"><span data-stu-id="db405-113">Master keys provide access toohello all hello administrative resources for hello database account.</span></span> <span data-ttu-id="db405-114">Ana anahtarları:</span><span class="sxs-lookup"><span data-stu-id="db405-114">Master keys:</span></span>  
- <span data-ttu-id="db405-115">Erişim tooaccounts, veritabanları, kullanıcılar ve izinler sağlar.</span><span class="sxs-lookup"><span data-stu-id="db405-115">Provide access tooaccounts, databases, users, and permissions.</span></span> 
- <span data-ttu-id="db405-116">Kullanılan tooprovide ayrıntılı erişim toocollections ve belgeleri olamaz.</span><span class="sxs-lookup"><span data-stu-id="db405-116">Cannot be used tooprovide granular access toocollections and documents.</span></span>
- <span data-ttu-id="db405-117">Bir hesap Hello oluşturma sırasında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="db405-117">Are created during hello creation of an account.</span></span>
- <span data-ttu-id="db405-118">Herhangi bir zamanda yeniden oluşturulacak.</span><span class="sxs-lookup"><span data-stu-id="db405-118">Can be regenerated at any time.</span></span>

<span data-ttu-id="db405-119">Her hesap iki ana anahtarları oluşur: bir birincil anahtar ve ikincil anahtar.</span><span class="sxs-lookup"><span data-stu-id="db405-119">Each account consists of two Master keys: a primary key and secondary key.</span></span> <span data-ttu-id="db405-120">çift anahtarları hello amacı, böylelikle yeniden oluşturmak veya sürekli erişim tooyour hesabı ve verileri sağlayan, anahtarları alma.</span><span class="sxs-lookup"><span data-stu-id="db405-120">hello purpose of dual keys is so that you can regenerate, or roll keys, providing continuous access tooyour account and data.</span></span> 

<span data-ttu-id="db405-121">Toplama toohello iki ana anahtarları'hello Cosmos DB hesabı için iki salt okunur anahtar vardır.</span><span class="sxs-lookup"><span data-stu-id="db405-121">In addition toohello two master keys for hello Cosmos DB account, there are two read-only keys.</span></span> <span data-ttu-id="db405-122">Bu salt okunur anahtarları yalnızca okuma işlemleri hello hesabındaki izin verir.</span><span class="sxs-lookup"><span data-stu-id="db405-122">These read-only keys only allow read operations on hello account.</span></span> <span data-ttu-id="db405-123">Salt okunur anahtarları tooread izinleri kaynaklara erişim sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="db405-123">Read-only keys do not provide access tooread permissions resources.</span></span>

<span data-ttu-id="db405-124">Birincil, ikincil, salt okunur ve okuma-yazma ana anahtarları alınabilir ve hello Azure portal kullanarak yeniden oluşturulacak.</span><span class="sxs-lookup"><span data-stu-id="db405-124">Primary, secondary, read only, and read-write master keys can be retrieved and regenerated using hello Azure portal.</span></span> <span data-ttu-id="db405-125">Yönergeler için bkz: [görüntüleme, kopyalama ve yeniden oluşturma erişim tuşları](manage-account.md#keys).</span><span class="sxs-lookup"><span data-stu-id="db405-125">For instructions, see [View, copy, and regenerate access keys](manage-account.md#keys).</span></span>

![Erişim denetimi (IAM) hello Azure portal - gösterilmesi NoSQL veritabanı güvenliği](./media/secure-access-to-data/nosql-database-security-master-key-portal.png)

<span data-ttu-id="db405-127">Ana anahtarınızı döndürme hello basit işlemidir.</span><span class="sxs-lookup"><span data-stu-id="db405-127">hello process of rotating your master key is simple.</span></span> <span data-ttu-id="db405-128">İkincil anahtarınızı toohello Azure portal tooretrieve gidin ikincil anahtarınızı uygulamanızda birincil anahtarınızı değiştirin, sonra hello Azure portalında birincil anahtarda hello döndür.</span><span class="sxs-lookup"><span data-stu-id="db405-128">Navigate toohello Azure portal tooretrieve your secondary key, then replace your primary key with your secondary key in your application, then rotate hello primary key in hello Azure portal.</span></span>

![Merhaba NoSQL veritabanı güvenliği gösteren Azure portal - ana anahtar dönüşü](./media/secure-access-to-data/nosql-database-security-master-key-rotate-workflow.png)

### <a name="code-sample-toouse-a-master-key"></a><span data-ttu-id="db405-130">Örnek toouse bir ana anahtar kodu</span><span class="sxs-lookup"><span data-stu-id="db405-130">Code sample toouse a master key</span></span>

<span data-ttu-id="db405-131">Merhaba aşağıdaki kod örneği nasıl toouse Cosmos DB uç noktası ve ana anahtar tooinstantiate bir DocumentClient hesap ve bir veritabanı oluşturmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="db405-131">hello following code sample illustrates how toouse a Cosmos DB account endpoint and master key tooinstantiate a DocumentClient and create a database.</span></span> 

```csharp
//Read hello Azure Cosmos DB endpointUrl and authorization keys from config.
//These values are available from hello Azure portal on hello Azure Cosmos DB account blade under "Keys".
//NB > Keep these values in a safe and secure location. Together they provide Administrative access tooyour DocDB account.

private static readonly string endpointUrl = ConfigurationManager.AppSettings["EndPointUrl"];
private static readonly SecureString authorizationKey = ToSecureString(ConfigurationManager.AppSettings["AuthorizationKey"]);

client = new DocumentClient(new Uri(endpointUrl), authorizationKey);

// Create Database
Database database = await client.CreateDatabaseAsync(
    new Database
    {
        Id = databaseName
    });
```

<a id="resource-tokens"></a>

## <a name="resource-tokens"></a><span data-ttu-id="db405-132">Kaynak belirteçleri</span><span class="sxs-lookup"><span data-stu-id="db405-132">Resource tokens</span></span>

<span data-ttu-id="db405-133">Kaynak belirteçleri, bir veritabanı içinde toohello uygulama kaynaklarına erişim sağlamak.</span><span class="sxs-lookup"><span data-stu-id="db405-133">Resource tokens provide access toohello application resources within a database.</span></span> <span data-ttu-id="db405-134">Kaynak belirteçleri:</span><span class="sxs-lookup"><span data-stu-id="db405-134">Resource tokens:</span></span>
- <span data-ttu-id="db405-135">Erişim toospecific koleksiyonları, bölüm anahtarlarını, belgeler, ekleri, saklı yordamlar, tetikleyiciler ve UDF'ler sağlar.</span><span class="sxs-lookup"><span data-stu-id="db405-135">Provide access toospecific collections, partition keys, documents, attachments, stored procedures, triggers, and UDFs.</span></span>
- <span data-ttu-id="db405-136">Ne zaman oluşturulan bir [kullanıcı](#users) verilir [izinleri](#permissions) tooa belirli kaynak.</span><span class="sxs-lookup"><span data-stu-id="db405-136">Are created when a [user](#users) is granted [permissions](#permissions) tooa specific resource.</span></span>
- <span data-ttu-id="db405-137">İzni kaynak bağlı POST, GET ve PUT çağrısı tarafından çalıştırıldığı zaman yeniden oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="db405-137">Are recreated when a permission resource is acted upon on by POST, GET, or PUT call.</span></span>
- <span data-ttu-id="db405-138">Merhaba kullanıcı, kaynak ve izni için özel olarak oluşturulan bir karma kaynak belirteci kullanın.</span><span class="sxs-lookup"><span data-stu-id="db405-138">Use a hash resource token specifically constructed for hello user, resource, and permission.</span></span>
- <span data-ttu-id="db405-139">Özelleştirilebilir geçerlilik süresi ile ilişkili zamanı.</span><span class="sxs-lookup"><span data-stu-id="db405-139">Are time bound with a customizable validity period.</span></span> <span data-ttu-id="db405-140">Merhaba varsayılan geçerli timespan bir saattir.</span><span class="sxs-lookup"><span data-stu-id="db405-140">hello default valid timespan is one hour.</span></span> <span data-ttu-id="db405-141">Belirteç ömrü, ancak açıkça, tooa en fazla beş saat belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="db405-141">Token lifetime, however, may be explicitly specified, up tooa maximum of five hours.</span></span>
- <span data-ttu-id="db405-142">Güvenli bir alternatif toogiving hello ana anahtar çıkışı sağlar.</span><span class="sxs-lookup"><span data-stu-id="db405-142">Provide a safe alternative toogiving out hello master key.</span></span> 
- <span data-ttu-id="db405-143">İstemciler tooread, yazma ve silme kaynakları verilen toohello izinler göre hello Cosmos DB hesabındaki etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="db405-143">Enable clients tooread, write, and delete resources in hello Cosmos DB account according toohello permissions they've been granted.</span></span>

<span data-ttu-id="db405-144">Kaynak belirteci (Cosmos DB kullanıcılar ve izinler oluşturarak) kullanabileceğiniz tooa istemci tooprovide erişim tooresources Cosmos DB'de hesabı istediğinizde hello ana anahtar ile güvenilir olamaz.</span><span class="sxs-lookup"><span data-stu-id="db405-144">You can use a resource token (by creating Cosmos DB users and permissions) when you want tooprovide access tooresources in your Cosmos DB account tooa client that cannot be trusted with hello master key.</span></span>  

<span data-ttu-id="db405-145">Cosmos DB kaynak belirteçleri istemciler tooread, yazma ve silme kaynakların verilen toohello izinler göre Cosmos DB hesabınızda ve her iki ana gerek kalmadan sağlayan güvenli bir alternatif sunar veya yalnızca anahtar okuyun.</span><span class="sxs-lookup"><span data-stu-id="db405-145">Cosmos DB resource tokens provide a safe alternative that enables clients tooread, write, and delete resources in your Cosmos DB account according toohello permissions you've granted, and without need for either a master or read only key.</span></span>

<span data-ttu-id="db405-146">Adlı kaynak belirteçleri istenen, oluşturulan ve tooclients teslim tipik tasarım deseni şöyledir:</span><span class="sxs-lookup"><span data-stu-id="db405-146">Here is a typical design pattern whereby resource tokens may be requested, generated, and delivered tooclients:</span></span>

1. <span data-ttu-id="db405-147">Orta katman hizmet tooserve bir mobil uygulama tooshare kullanıcı fotoğrafı ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="db405-147">A mid-tier service is set up tooserve a mobile application tooshare user photos.</span></span> 
2. <span data-ttu-id="db405-148">Merhaba orta katman hizmet hello ana anahtarı hello Cosmos DB hesabı sahip olur.</span><span class="sxs-lookup"><span data-stu-id="db405-148">hello mid-tier service possesses hello master key of hello Cosmos DB account.</span></span>
3. <span data-ttu-id="db405-149">Merhaba fotoğraf uygulaması son kullanıcı mobil cihazlarda yüklü.</span><span class="sxs-lookup"><span data-stu-id="db405-149">hello photo app is installed on end-user mobile devices.</span></span> 
4. <span data-ttu-id="db405-150">Oturum açma hello fotoğraf uygulaması hello hello Orta katmanda hizmeti ile Merhaba kullanıcının kimliğini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="db405-150">On login, hello photo app establishes hello identity of hello user with hello mid-tier service.</span></span> <span data-ttu-id="db405-151">Bu kimlik kuruluş tamamen toohello uygulamayı oluşturan mekanizmadır.</span><span class="sxs-lookup"><span data-stu-id="db405-151">This mechanism of identity establishment is purely up toohello application.</span></span>
5. <span data-ttu-id="db405-152">Merhaba kimlik kurulduktan sonra hello orta katman hizmet hello kimliğine göre izinleri ister.</span><span class="sxs-lookup"><span data-stu-id="db405-152">Once hello identity is established, hello mid-tier service requests permissions based on hello identity.</span></span>
6. <span data-ttu-id="db405-153">Merhaba Orta katmanda hizmeti kaynak belirteci geri toohello telefon uygulaması gönderir.</span><span class="sxs-lookup"><span data-stu-id="db405-153">hello mid-tier service sends a resource token back toohello phone app.</span></span>
7. <span data-ttu-id="db405-154">Hello telefon uygulaması toouse hello kaynak belirteci toodirectly Cosmos DB erişimine hello kaynak belirteci tarafından ve hello kaynak belirteci tarafından izin verilen hello aralığı için tanımlanan hello izinlerle devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="db405-154">hello phone app can continue toouse hello resource token toodirectly access Cosmos DB resources with hello permissions defined by hello resource token and for hello interval allowed by hello resource token.</span></span> 
8. <span data-ttu-id="db405-155">Merhaba kaynak belirtecinin süresi dolduğunda, sonraki istekler bir 401 Yetkisiz özel alırsınız.</span><span class="sxs-lookup"><span data-stu-id="db405-155">When hello resource token expires, subsequent requests receive a 401 unauthorized exception.</span></span>  <span data-ttu-id="db405-156">Bu noktada, hello telefon uygulaması hello kimliği yeniden oluşturur ve yeni bir kaynak belirteci ister.</span><span class="sxs-lookup"><span data-stu-id="db405-156">At this point, hello phone app re-establishes hello identity and requests a new resource token.</span></span>

    ![İş akışı Azure Cosmos DB kaynak belirteçleri](./media/secure-access-to-data/resourcekeyworkflow.png)

<span data-ttu-id="db405-158">Kaynak belirteci oluşturma ve yönetim hello yerel Cosmos DB istemci kitaplıkları tarafından işlenir; Ancak, REST kullanırsanız hello istek/kimlik doğrulama üstbilgileri oluşturmalıdır.</span><span class="sxs-lookup"><span data-stu-id="db405-158">Resource token generation and management is handled by hello native Cosmos DB client libraries; however, if you use REST you must construct hello request/authentication headers.</span></span> <span data-ttu-id="db405-159">İçin REST kimlik doğrulama üstbilgileri oluşturma hakkında daha fazla bilgi için bkz: [Cosmos DB kaynaklarda erişim denetimi](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources) veya hello [bizim SDK'ları için kaynak kodu](https://github.com/Azure/azure-documentdb-node/blob/master/source/lib/auth.js).</span><span class="sxs-lookup"><span data-stu-id="db405-159">For more information on creating authentication headers for REST, see [Access Control on Cosmos DB Resources](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources) or hello [source code for our SDKs](https://github.com/Azure/azure-documentdb-node/blob/master/source/lib/auth.js).</span></span>

<span data-ttu-id="db405-160">Orta katman hizmet örneği toogenerate veya Aracısı kaynak belirteçleri kullanılan hello bakın [ResourceTokenBroker uygulama](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker/Controllers).</span><span class="sxs-lookup"><span data-stu-id="db405-160">For an example of a middle tier service used toogenerate or broker resource tokens, see hello [ResourceTokenBroker app](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker/Controllers).</span></span>

<a id="users"></a>

## <a name="users"></a><span data-ttu-id="db405-161">Kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="db405-161">Users</span></span>
<span data-ttu-id="db405-162">Cosmos DB kullanıcılar Cosmos DB veritabanı ile ilişkilidir.</span><span class="sxs-lookup"><span data-stu-id="db405-162">Cosmos DB users are associated with a Cosmos DB database.</span></span>  <span data-ttu-id="db405-163">Her veritabanı sıfır veya daha fazla Cosmos DB kullanıcılar içerebilir.</span><span class="sxs-lookup"><span data-stu-id="db405-163">Each database can contain zero or more Cosmos DB users.</span></span>  <span data-ttu-id="db405-164">kodun örnek gösterdiği nasıl aşağıdaki hello toocreate Cosmos DB kullanıcı kaynağı.</span><span class="sxs-lookup"><span data-stu-id="db405-164">hello following code sample shows how toocreate a Cosmos DB user resource.</span></span>

```csharp
//Create a user.
User docUser = new User
{
    Id = "mobileuser"
};

docUser = await client.CreateUserAsync(UriFactory.CreateDatabaseUri("db"), docUser);
```

> [!NOTE]
> <span data-ttu-id="db405-165">Her Cosmos DB kullanıcı kullanılan tooretrieve hello listesi olabilecek PermissionsLink özelliğine [izinleri](#permissions) hello kullanıcıyla ilişkili.</span><span class="sxs-lookup"><span data-stu-id="db405-165">Each Cosmos DB user has a PermissionsLink property that can be used tooretrieve hello list of [permissions](#permissions) associated with hello user.</span></span>
> 
> 

<a id="permissions"></a>

## <a name="permissions"></a><span data-ttu-id="db405-166">İzinler</span><span class="sxs-lookup"><span data-stu-id="db405-166">Permissions</span></span>
<span data-ttu-id="db405-167">Cosmos DB izni kaynak Cosmos DB kullanıcıyla ilişkili değil.</span><span class="sxs-lookup"><span data-stu-id="db405-167">A Cosmos DB permission resource is associated with a Cosmos DB user.</span></span>  <span data-ttu-id="db405-168">Her bir kullanıcı, sıfır veya daha fazla Cosmos DB izinleri içerebilir.</span><span class="sxs-lookup"><span data-stu-id="db405-168">Each user may contain zero or more Cosmos DB permissions.</span></span>  <span data-ttu-id="db405-169">Bir izin kaynak kullanıcı gereksinimlerini tooaccess çalışırken bir özel uygulama kaynağı hello erişim tooa güvenlik belirteci sağlar.</span><span class="sxs-lookup"><span data-stu-id="db405-169">A permission resource provides access tooa security token that hello user needs when trying tooaccess a specific application resource.</span></span>
<span data-ttu-id="db405-170">İzni kaynak tarafından sağlanan iki kullanılabilir erişim düzeyleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="db405-170">There are two available access levels that may be provided by a permission resource:</span></span>

* <span data-ttu-id="db405-171">Tümü: hello kullanıcının hello kaynaktaki tam izinleri vardır.</span><span class="sxs-lookup"><span data-stu-id="db405-171">All: hello user has full permission on hello resource.</span></span>
* <span data-ttu-id="db405-172">Şunu okuyun: hello kullanıcı hello kaynak Merhaba içeriğine yalnızca okuyabilir, ancak yazma, güncelleştirme veya silme işlemleri hello kaynakta gerçekleştiremez.</span><span class="sxs-lookup"><span data-stu-id="db405-172">Read: hello user can only read hello contents of hello resource but cannot perform write, update, or delete operations on hello resource.</span></span>

> [!NOTE]
> <span data-ttu-id="db405-173">Sipariş toorun Cosmos DB saklı yordamlar hello kullanıcı hello hangi hello saklı yordam çalıştırılacak hello koleksiyonunda tüm izninizin olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="db405-173">In order toorun Cosmos DB stored procedures hello user must have hello All permission on hello collection in which hello stored procedure will be run.</span></span>
> 
> 

### <a name="code-sample-toocreate-permission"></a><span data-ttu-id="db405-174">Kod örnek toocreate izni</span><span class="sxs-lookup"><span data-stu-id="db405-174">Code sample toocreate permission</span></span>

<span data-ttu-id="db405-175">Merhaba aşağıdaki kod örneği nasıl toocreate okuma izni kaynak hello hello izni kaynağının kaynak belirteci ve hello izinleri hello ile ilişkilendirmek gösterir [kullanıcı](#users) yukarıda oluşturduğunuz.</span><span class="sxs-lookup"><span data-stu-id="db405-175">hello following code sample shows how toocreate a permission resource, read hello resource token of hello permission resource, and associate hello permissions with hello [user](#users) created above.</span></span>

```csharp
// Create a permission.
Permission docPermission = new Permission
{
    PermissionMode = PermissionMode.Read,
    ResourceLink = documentCollection.SelfLink,
    Id = "readperm"
};
  
docPermission = await client.CreatePermissionAsync(UriFactory.CreateUserUri("db", "user"), docPermission);
Console.WriteLine(docPermission.Id + " has token of: " + docPermission.Token);
```

<span data-ttu-id="db405-176">Koleksiyon, belge ve ek kaynaklar için sonra hello izni koleksiyonunuz için bir bölüm anahtarı de dahil etmelisiniz belirtilmişse ResourcePartitionKey toplama toohello ResourceLink hello.</span><span class="sxs-lookup"><span data-stu-id="db405-176">If you have specified a partition key for your collection, then hello permission for collection, document, and attachment resources must also include hello ResourcePartitionKey in addition toohello ResourceLink.</span></span>

### <a name="code-sample-tooread-permissions-for-user"></a><span data-ttu-id="db405-177">Örnek tooread kullanıcının izinlerini kod</span><span class="sxs-lookup"><span data-stu-id="db405-177">Code sample tooread permissions for user</span></span>

<span data-ttu-id="db405-178">belirli bir kullanıcı ile ilişkili tüm izni kaynakları tooeasily elde etmek için Cosmos DB kullanılabilir hale getirir izin her kullanıcı nesnesi için akış.</span><span class="sxs-lookup"><span data-stu-id="db405-178">tooeasily obtain all permission resources associated with a particular user, Cosmos DB makes available a permission feed for each user object.</span></span>  <span data-ttu-id="db405-179">Hello aşağıdaki kod parçacığını nasıl tooretrieve hello izni, yukarıda oluşturduğunuz hello kullanıcıyla ilişkilendirilmiş izin listesini oluşturmak ve hello kullanıcı adına yeni bir DocumentClient örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="db405-179">hello following code snippet shows how tooretrieve hello permission associated with hello user created above, construct a permission list, and instantiate a new DocumentClient on behalf of hello user.</span></span>

```csharp
//Read a permission feed.
FeedResponse<Permission> permFeed = await client.ReadPermissionFeedAsync(
  UriFactory.CreateUserUri("db", "myUser"));
 List<Permission> permList = new List<Permission>();

foreach (Permission perm in permFeed)
{
    permList.Add(perm);
}

DocumentClient userClient = new DocumentClient(new Uri(endpointUrl), permList);
```

## <a name="next-steps"></a><span data-ttu-id="db405-180">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="db405-180">Next steps</span></span>
* <span data-ttu-id="db405-181">toolearn Cosmos DB veritabanı güvenliği hakkında daha fazla bilgi görmek [Cosmos DB: Veritabanı Güvenlik](database-security.md).</span><span class="sxs-lookup"><span data-stu-id="db405-181">toolearn more about Cosmos DB database security, see [Cosmos DB: Database security](database-security.md).</span></span>
* <span data-ttu-id="db405-182">ana ve salt okunur anahtarlarını yönetme hakkında toolearn bkz [nasıl toomanage bir Azure Cosmos DB hesap](manage-account.md#keys).</span><span class="sxs-lookup"><span data-stu-id="db405-182">toolearn about managing master and read-only keys, see [How toomanage an Azure Cosmos DB account](manage-account.md#keys).</span></span>
* <span data-ttu-id="db405-183">tooconstruct Azure Cosmos DB yetkilendirme belirteçleri nasıl görürüm toolearn [Azure Cosmos DB kaynaklarda erişim denetimi](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources).</span><span class="sxs-lookup"><span data-stu-id="db405-183">toolearn how tooconstruct Azure Cosmos DB authorization tokens, see [Access Control on Azure Cosmos DB Resources](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources).</span></span>
