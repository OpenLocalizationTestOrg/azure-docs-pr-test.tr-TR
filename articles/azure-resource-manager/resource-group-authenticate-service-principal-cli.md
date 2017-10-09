---
title: "Azure CLI ile Azure uygulaması için aaaCreate kimlik | Microsoft Docs"
description: "Toouse Azure CLI toocreate bir Azure Active Directory uygulaması ve hizmet sorumlusu ve rol tabanlı erişim, erişim tooresources nasıl kontrol açıklar. Bunu gösterir nasıl tooauthenticate uygulamayla bir parola veya sertifika."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: c224a189-dd28-4801-b3e3-26991b0eb24d
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 0d693ec801d4f4d6c24ec420580776e73014b325
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-cli-toocreate-a-service-principal-tooaccess-resources"></a>Bir hizmet asıl tooaccess kaynakları Azure CLI toocreate kullanın

Bir uygulama ya da tooaccess kaynakları gereken komut dosyası varsa, kendi kimlik bilgileriyle hello uygulamanın kimlik doğrulamasını ve hello uygulama için bir kimlik ayarlayın. Bu kimlik, bir hizmet sorumlusu bilinir. Bu yaklaşım sağlar:

* İzinleri kendi izinlerinizi farklı toohello uygulama kimliği atayın. Genellikle, bu kısıtlı tooexactly hangi hello uygulamanın toodo ihtiyacı izinlerdir.
* Sertifika kimlik doğrulaması için Katılımsız betik yürütülürken kullanın.

Bu makale size nasıl gösterir toouse [Azure CLI 1.0](../cli-install-nodejs.md) tooset kendi kimlik bilgilerini ve kimlik altında bir uygulama toorun ayarlama. Merhaba en son sürümünü yüklemek [Azure CLI 1.0](../cli-install-nodejs.md) toomake ortamınızı bu makaledeki örneklerde hello eşleştiğinden emin.

## <a name="required-permissions"></a>Gerekli izinler
toocomplete bu konuda, Azure Active Directory ve Azure aboneliğinize yeterli izniniz olması gerekir. Özellikle, mümkün toocreate hello Azure Active Directory içinde bir uygulama olabilir. ve hello hizmet asıl tooa rolünü atamanız gerekir. 

hesabınızın yeterli izinlere sahip olup olmadığı hello portalıdır hello en kolay yolu toocheck. Bkz. [Portalda gerekli izinleri denetleme](resource-group-create-service-principal-portal.md#required-permissions).

Şimdi, tooa bölüm için ya da devam [parola](#create-service-principal-with-password) veya [sertifika](#create-service-principal-with-certificate) kimlik doğrulaması.

## <a name="create-service-principal-with-password"></a>Parola ile hizmet sorumlusu oluşturma
Bu bölümdeki hello adımları toocreate hello AD uygulaması bir parola ile gerçekleştirmek ve hello okuyucu rolü toohello hizmet sorumlusu atayın.

1. Tooyour hesabında oturum açın.
   
   ```azurecli
   azure login
   ```
2. toocreate bir uygulama kimliği sağlayın hello uygulamasının hello adı ve parola hello komutu aşağıdaki gösterildiği gibi:
     
   ```azurecli
   azure ad sp create -n exampleapp -p {your-password}
   ```
     
   Merhaba yeni hizmet sorumlusu döndürülür. izin verme Hello nesne kimliği gereklidir. Hizmet asıl adları Merhaba ile listelenmiş hello GUID açarken gereklidir. Merhaba bu GUID'dir hello uygulama kimliği ile aynı değeri. Merhaba örnek uygulamalarda, bu değer başvurulan tooas hello: `Client ID`. 
     
   ```azurecli
   info:    Executing command ad sp create
     
   Creating application exampleapp
     / Creating service principal for application 7132aca4-1bdb-4238-ad81-996ff91d8db+
     data:    Object Id:               ff863613-e5e2-4a6b-af07-fff6f2de3f4e
     data:    Display Name:            exampleapp
     data:    Service Principal Names:
     data:                             7132aca4-1bdb-4238-ad81-996ff91d8db4
     data:                             https://www.contoso.org/example
     info:    ad sp create command OK
   ```

3. Merhaba, aboneliğinizin hizmet asıl izinleri verin. Bu örnekte, izni tooread hello Abonelikteki tüm kaynaklar veren hello hizmet asıl toohello okuyucu rolü, ekleyin. Diğer roller için bkz: [RBAC: yerleşik roller](../active-directory/role-based-access-built-in-roles.md). Merhaba objectID parametresi için hello Merhaba uygulaması oluşturulurken kullanılan nesne kimliği sağlayın. Bu komutu çalıştırmadan önce biraz zaman hello yeni hizmet asıl toopropagate Azure Active Directory boyunca izin vermesi gerekir. Genellikle, bu komutları el ile çalıştırdığınızda görevleri arasında yeterli bir süre geçti. Bir komut dosyasında bir adım toosleep hello komutları arasında eklemeniz gerekir (gibi `sleep 15`). Belirten bir hata hello asıl hello dizininde yok görürseniz, hello komutu yeniden çalıştırın.
   
   ```azurecli
   azure role assignment create --objectId ff863613-e5e2-4a6b-af07-fff6f2de3f4e -o Reader -c /subscriptions/{subscriptionId}/
   ```
   
İşte bu kadar! AD uygulaması ve hizmet sorumlusu ayarlanır. Merhaba sonraki bölümde hello oturum toolog Azure CLI aracılığıyla nasıl kimlik bilgisi gösterilir. Kod uygulamanızda toouse hello kimlik bilgisi istiyorsanız, bu konu ile toocontinue gerekmez. Toohello atlayabilirsiniz [örnek uygulamaları](#sample-applications) uygulama kimliği ve parola oturum açma örnekleri için. 

### <a name="provide-credentials-through-azure-cli"></a>Azure CLI aracılığıyla kimlik bilgilerini sağlayın
Şimdi, hello uygulaması tooperform işlemleri toolog de gerekir.

1. Bir hizmet sorumlusu oturum olduğunda, AD uygulamanız için hello dizininin tooprovide hello Kiracı kimliği gerekir. Bir kiracı, Azure Active Directory örneğidir. şu anda kimliği doğrulanmış aboneliğiniz, kullanım için tooretrieve hello Kiracı kimliği:
   
   ```azurecli
   azure account show
   ```
   
   Hangi döndürür:
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
     Başka bir abonelik tooget hello Kiracı kimliği gerekiyorsa, komutu aşağıdaki hello kullanın:
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. Oturum açma için tooretrieve hello istemci kimliği toouse gerekiyorsa kullanın:
   
   ```azurecli
   azure ad sp show -c exampleapp --json
   ```
   
     oturum açma için hello değeri toouse hello hizmet asıl adları listelenen hello GUID'dir.
   
   ```azurecli
   [
     {
       "objectId": "ff863613-e5e2-4a6b-af07-fff6f2de3f4e",
       "objectType": "ServicePrincipal",
       "displayName": "exampleapp",
       "appId": "7132aca4-1bdb-4238-ad81-996ff91d8db4",
       "servicePrincipalNames": [
         "https://www.contoso.org/example",
         "7132aca4-1bdb-4238-ad81-996ff91d8db4"
       ]
     }
   ]
   ```
3. Asıl Hello hizmet olarak oturum açın.
   
   ```azurecli
   azure login -u 7132aca4-1bdb-4238-ad81-996ff91d8db4 --service-principal --tenant {tenant-id}
   ```
   
    Merhaba parolayı girmeniz istenir. Merhaba AD uygulaması oluştururken, belirtilen hello parolasını belirtin.
   
   ```azurecli
   info:    Executing command login
   Password: ********
   ```

Şimdi, oluşturduğunuz hello hizmet sorumlusu için hello hizmet sorumlusu olarak doğrulanır.

Alternatif olarak, REST işlemlerini hello komut satırı toolog çağırabilirsiniz. Merhaba kimlik doğrulaması yanıttan hello erişim belirteci diğer işlemleri ile kullanılmak üzere alabilir. REST işlemlerini çağırarak hello erişim belirteci alma bir örnek için bkz: [bir erişim belirteci oluşturma](resource-manager-rest-api.md#generating-an-access-token).

## <a name="create-service-principal-with-certificate"></a>Sertifika ile hizmet sorumlusu oluşturma
Bu bölümde, hello adımları gerçekleştirin:

* Otomatik olarak imzalanan sertifika oluşturma
* hello sertifika ve hello hizmet sorumlusu Hello AD uygulaması oluşturma
* Merhaba okuyucu rolü toohello hizmet sorumlusu atayın

Aşağıdaki adımları toocomplete olmalıdır [OpenSSL](http://www.openssl.org/) yüklü.

1. Kendinden imzalı bir sertifika oluşturun.
   
   ```
   openssl req -x509 -days 3650 -newkey rsa:2048 -out cert.pem -nodes -subj '/CN=exampleapp'
   ```

2. Önceki adımda oluşturulan iki dosya - privkey.pem ve cert.pem hello. Merhaba ortak ve özel anahtarlar, tek bir dosya halinde birleştirin.

   ```
   cat privkey.pem cert.pem > examplecert.pem
   ```

3. Açık hello **examplecert.pem** dosya ve hello karakter arasında uzun bir sıra arayın **---başlangıç sertifika---** ve **---son SERTİFİKAYI---**. Merhaba sertifika verileri kopyalayın. Hizmet sorumlusu hello oluştururken, bu verileri bir parametre olarak geçirir.

4. Tooyour hesabında oturum açın.

   ```azurecli
   azure login
   ```
5. toocreate hello hizmet sorumlusu hello komutu aşağıdaki gösterildiği gibi hello uygulamanın ve hello sertifika verileri hello adı girin:
     
   ```azurecli
   azure ad sp create -n exampleapp --cert-value {certificate data}
   ```
     
   Merhaba yeni hizmet sorumlusu döndürülür. izin verme Hello nesne kimliği gereklidir. Hizmet asıl adları Merhaba ile listelenmiş hello GUID açarken gereklidir. Merhaba bu GUID'dir hello uygulama kimliği ile aynı değeri. Merhaba örnek uygulamalarda, bu değer başvurulan tooas hello istemci kimliği: 
     
   ```azurecli
   info:    Executing command ad sp create
     
   Creating service principal for application 4fd39843-c338-417d-b549-a545f584a74+
     data:    Object Id:        7dbc8265-51ed-4038-8e13-31948c7f4ce7
     data:    Display Name:     exampleapp
     data:    Service Principal Names:
     data:                      4fd39843-c338-417d-b549-a545f584a745
     data:                      https://www.contoso.org/example
     info:    ad sp create command OK
   ```
6. Merhaba, aboneliğinizin hizmet asıl izinleri verin. Bu örnekte, izni tooread hello Abonelikteki tüm kaynaklar veren hello hizmet asıl toohello okuyucu rolü, ekleyin. Diğer roller için bkz: [RBAC: yerleşik roller](../active-directory/role-based-access-built-in-roles.md). Merhaba objectID parametresi için hello Merhaba uygulaması oluşturulurken kullanılan nesne kimliği sağlayın. Bu komutu çalıştırmadan önce biraz zaman hello yeni hizmet asıl toopropagate Azure Active Directory boyunca izin vermesi gerekir. Genellikle, bu komutları el ile çalıştırdığınızda görevleri arasında yeterli bir süre geçti. Bir komut dosyasında bir adım toosleep hello komutları arasında eklemeniz gerekir (gibi `sleep 15`). Belirten bir hata hello asıl hello dizininde yok görürseniz, hello komutu yeniden çalıştırın.
   
   ```azurecli
   azure role assignment create --objectId 7dbc8265-51ed-4038-8e13-31948c7f4ce7 -o Reader -c /subscriptions/{subscriptionId}/
   ```
  
### <a name="provide-certificate-through-automated-azure-cli-script"></a>Otomatik Azure CLI komut dosyası aracılığıyla sertifikası sağlayın
Şimdi, hello uygulaması tooperform işlemleri toolog de gerekir.

1. Bir hizmet sorumlusu oturum olduğunda, AD uygulamanız için hello dizininin tooprovide hello Kiracı kimliği gerekir. Bir kiracı, Azure Active Directory örneğidir. şu anda kimliği doğrulanmış aboneliğiniz, kullanım için tooretrieve hello Kiracı kimliği:
   
   ```azurecli
   azure account show
   ```
   
   Hangi döndürür:
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
   Başka bir abonelik tooget hello Kiracı kimliği gerekiyorsa, komutu aşağıdaki hello kullanın:
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. tooretrieve sertifika parmak izi hello ve gereksiz karakterleri kaldırmak için kullanın:
   
   ```
   openssl x509 -in "C:\certificates\examplecert.pem" -fingerprint -noout | sed 's/SHA1 Fingerprint=//g'  | sed 's/://g'
   ```
   
   Hangi parmak izi değeri benzer döndürür:
   
   ```
   30996D9CE48A0B6E0CD49DBB9A48059BF9355851
   ```
3. Oturum açma için tooretrieve hello istemci kimliği toouse gerekiyorsa kullanın:
   
   ```azurecli
   azure ad sp show -c exampleapp
   ```
   
   oturum açma için hello değeri toouse hello hizmet asıl adları listelenen hello GUID'dir.
     
   ```azurecli
   [
     {
       "objectId": "7dbc8265-51ed-4038-8e13-31948c7f4ce7",
       "objectType": "ServicePrincipal",
       "displayName": "exampleapp",
       "appId": "4fd39843-c338-417d-b549-a545f584a745",
       "servicePrincipalNames": [
         "https://www.contoso.org/example",
         "4fd39843-c338-417d-b549-a545f584a745"
       ]
     }
   ]
   ```
4. Asıl Hello hizmet olarak oturum açın.
   
   ```azurecli
   azure login --service-principal --tenant {tenant-id} -u 4fd39843-c338-417d-b549-a545f584a745 --certificate-file C:\certificates\examplecert.pem --thumbprint {thumbprint}
   ```

Şimdi hello hizmet sorumlusu hello oluşturulan Azure Active Directory uygulaması için olarak doğrulanır.

## <a name="change-credentials"></a>Kimlik bilgilerini değiştirme

kimlik bilgileri güvenliğinin aşılması veya bir kimlik bilgisi sona erme nedeniyle, bir AD uygulaması toochange hello kullanın `azure ad app set`.

toochange bir parola kullanın:

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --password p@ssword
```

toochange sertifika değerini kullanın:

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --cert-value {certificate data}
```

## <a name="debug"></a>Hata ayıklama

Bir hizmet sorumlusu oluşturma sırasında aşağıdaki hatalar hello karşılaşabilirsiniz:

* **"Authentication_Unauthorized"** veya **"abonelik hello bağlamda bulunamadı."** -Hesabınızı hello olmadığında bu hatayı gördüğünüz [gerekli izinleri](#required-permissions) hello Azure Active Directory tooregister bir uygulama üzerinde. Yalnızca yönetici kullanıcıların Azure Active Directory'de uygulamaları kaydedebilirsiniz ve hesabınızın bir yönetici değil, bu hata genellikle, bakın Yönetici tooeither atamak, tooan Yönetici rolü ya da tooenable kullanıcılar tooregister uygulamaları isteyin.

* Hesabınızı **"yetkilendirme tooperform eylemi 'Microsoft.Authorization/roleAssignments/write' kapsamı üzerinde '/ subscriptions / {GUID}' yok."**  -Hesabınızı rol tooan kimlik yeterli izinleri tooassign olmadığında bu hatayı bakın. Abonelik Yöneticisi tooadd isteyin, tooUser erişim Yönetici rolü.

## <a name="sample-applications"></a>Örnek uygulamalar
Farklı platformlarda üzerinden hello uygulama olarak oturum açma hakkında daha fazla bilgi için bkz:

* [.NET](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [Java](/java/azure/java-sdk-azure-authenticate)
* [Node.js](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [Python](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [Ruby](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a>Sonraki adımlar
* Kaynakları yönetmek için Azure'da bir uygulamayı tümleştirme ayrıntılı adımlar için bkz: [Geliştirici Kılavuzu tooauthorization hello Azure Kaynak Yöneticisi API'si ile](resource-manager-api-authentication.md).
* Sertifikalar ve Azure CLI kullanma hakkında daha fazla bilgi tooget bkz [sertifika tabanlı kimlik doğrulaması Azure hizmet asıl adı ile Linux komut satırından](http://blogs.msdn.com/b/arsen/archive/2015/09/18/certificate-based-auth-with-azure-service-principals-from-linux-command-line.aspx). 
* Verilen veya toousers reddedilen kullanılabilir eylemler listesi için bkz: [Azure Resource Manager kaynak sağlayıcısı işlemleri](../active-directory/role-based-access-control-resource-provider-operations.md).
