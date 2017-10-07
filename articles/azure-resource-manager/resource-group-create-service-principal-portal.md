---
title: "Azure portal uygulaması aaaCreate kimlik | Microsoft Docs"
description: "Toocreate yeni bir Azure Active Directory uygulaması ve hizmet sorumlusu Azure Resource Manager toomanage hello rol tabanlı erişim denetimi ile kullanılabilecek tooresources nasıl erişim açıklar."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 7068617b-ac5e-47b3-a1de-a18c918297b6
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 9624715ac612f42df6f9e9e67b8233bd4b914174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-portal-toocreate-an-azure-active-directory-application-and-service-principal-that-can-access-resources"></a>Bir Azure Active Directory Uygulama ve kaynaklarına erişebilir hizmet sorumlusu Portal toocreate kullanın

Kaynakları göremeyen veya tooaccess gereken bir uygulamanız varsa, Azure Active Directory (AD) uygulama ayarlama ve gerekli hello izinleri tooit atamanız gerekir. Bu yaklaşım tercih toorunning hello uygulama kendi kimlik bilgileri altında nedeni:

* Kendi izinlerinizi farklı toohello uygulama kimliği izinleri atayabilirsiniz. Genellikle, bu kısıtlı tooexactly hangi hello uygulamanın toodo ihtiyacı izinlerdir.
* Sizin Sorumluluklarınız değiştirirseniz toochange hello uygulamanın kimlik bilgileri yok. 
* Katılımsız betik yürütülürken, bir sertifika tooautomate kimlik doğrulaması kullanabilirsiniz.

Bu konuda tooperform olanlar nasıl adımları aracılığıyla gösterilmektedir hello portal. Merhaba uygulaması yalnızca bir kuruluş içinde hedeflenen toorun olduğu bir tek kiracılı uygulama odaklanır. Genellikle tek Kiracı uygulamalar, kuruluşunuzun içinde çalışan satır iş kolu uygulamaları için kullanılır.
 
## <a name="required-permissions"></a>Gerekli izinler
toocomplete Bu konu, yeterli izinleri tooregister bir uygulama ile Azure AD kiracınıza sahip ve Azure aboneliğinizde hello uygulama tooa rolünü atamanız gerekir. Şimdi bu adımları hello doğru izinleri tooperform olduğundan emin olun.

### <a name="check-azure-active-directory-permissions"></a>Azure Active Directory izinlerini denetleyin
1. Tooyour Azure hesabı hello aracılığıyla oturum [Azure portal](https://portal.azure.com).
2. Seçin **Azure Active Directory**.

     ![Azure active Directory'yi seçin](./media/resource-group-create-service-principal-portal/select-active-directory.png)
3. Azure Active Directory'de seçin **kullanıcı ayarlarını**.

     ![kullanıcı ayarlarını seçin](./media/resource-group-create-service-principal-portal/select-user-settings.png)
4. Merhaba denetleyin **uygulama kayıtlar** ayarı. Varsa çok ayarlamak**Evet**, yönetici olmayan kullanıcıların AD uygulamaları kaydolabilir. Bu ayar hello Azure AD kiracısı içinde herhangi bir kullanıcı bir uygulama kaydedebilirsiniz anlamına gelir. Çok geçebilmeniz[denetleyin Azure abonelik izinleri](#check-azure-subscription-permissions).

     ![Uygulama kayıtları görüntüle](./media/resource-group-create-service-principal-portal/view-app-registrations.png)
5. Ayarı hello uygulama kayıtlar ayarlanır, çok**Hayır**, yalnızca yönetici kullanıcılar uygulamaların kaydedebilirsiniz. Hello Azure AD kiracısı için yönetici hesabınız olup olmadığını toocheck gerekir. Seçin **genel bakış** ve **kullanıcı Bul** hızlı görevleri.

     ![Kullanıcı Bul](./media/resource-group-create-service-principal-portal/find-user.png)
6. Hesabınız için arama yapın ve bunu bulduğunuzda seçin.

     ![arama kullanıcı](./media/resource-group-create-service-principal-portal/show-user.png)
7. Hesabınız için seçin **dizin rolünü**. 

     ![dizin rolü](./media/resource-group-create-service-principal-portal/select-directory-role.png)
8. Atanmış dizini rolünüze Azure AD'de görüntüleyin. Hesabınıza toohello kullanıcı rolüne atanan hello uygulama kayıt ayarından (adımları önceki hello) sınırlı tooadmin kullanıcılar varsa, yönetici tooeither atamak, tooan Yönetici rolü ya da tooenable kullanıcılar tooregister uygulamaları isteyin.

     ![Görünüm rolü](./media/resource-group-create-service-principal-portal/view-role.png)

### <a name="check-azure-subscription-permissions"></a>Azure abonelik izinlerinizi denetleyin
Azure aboneliğinizde, hesabınızın olması gerekir `Microsoft.Authorization/*/Write` tooassign bir AD uygulama tooa rolü erişim. Bu eylemin hello verilir [sahibi](../active-directory/role-based-access-built-in-roles.md#owner) rol veya [kullanıcı erişimi Yöneticisi](../active-directory/role-based-access-built-in-roles.md#user-access-administrator) rol. Hesabınızı toohello atanmışsa **katkıda bulunan** rolü, yeterli izniniz yok. Tooassign hello hizmet asıl tooa rolü çalışırken bir hata alırsınız. 

toocheck abonelik izinlerinizi:

1. Zaten Azure AD hesabınızla adımları önceki hello aradığınız değil, seçin **Azure Active Directory** hello sol bölmesinden.

2. Azure AD hesabınıza bulun. Seçin **genel bakış** ve **kullanıcı Bul** hızlı görevleri.

     ![Kullanıcı Bul](./media/resource-group-create-service-principal-portal/find-user.png)
2. Hesabınız için arama yapın ve bunu bulduğunuzda seçin.

     ![arama kullanıcı](./media/resource-group-create-service-principal-portal/show-user.png) 
     
3. Seçin **Azure kaynaklarını**.

     ![kaynakları seçin](./media/resource-group-create-service-principal-portal/select-azure-resources.png) 
3. Atanan rollerinizi görüntüleyin ve bir AD uygulama tooa rolü yeterli izinlere tooassign olup olmadığını belirlemelisiniz. Aksi takdirde, abonelik yönetici tooadd isteyin, tooUser erişim Yönetici rolü. Görüntü aşağıdaki hello hello kullanıcı kullanıcının yeterli izinlere sahip anlamına gelir atanan toohello sahip iki abonelikler için rolüdür. 

     ![izinleri göster](./media/resource-group-create-service-principal-portal/view-assigned-roles.png)

## <a name="create-an-azure-active-directory-application"></a>Azure Active Directory Uygulama oluşturma
1. Tooyour Azure hesabı hello aracılığıyla oturum [Azure portal](https://portal.azure.com).
2. Seçin **Azure Active Directory**.

     ![Azure active Directory'yi seçin](./media/resource-group-create-service-principal-portal/select-active-directory.png)

4. Seçin **uygulama kayıtlar**.   

     ![Uygulama kayıtlar seçin](./media/resource-group-create-service-principal-portal/select-app-registrations.png)
5. **Add (Ekle)** seçeneğini belirleyin.

     ![Uygulama Ekle](./media/resource-group-create-service-principal-portal/select-add-app.png)

6. Merhaba uygulaması için bir ad ve URL sağlayın. Şunlardan birini seçin **Web uygulaması / API** veya **yerel** hello uygulama türünün toocreate istiyor. Merhaba değerleri ayarladıktan sonra Seç **oluşturma**.

     ![Uygulama adı](./media/resource-group-create-service-principal-portal/create-app.png)

Uygulamanızı oluşturdunuz.

## <a name="get-application-id-and-authentication-key"></a>Uygulama kimliği ile kimlik doğrulama anahtarı alma
Program aracılığıyla oturum açarken uygulamanız ve bir kimlik doğrulama anahtarı için hello kimliği gerekir. Bu değerleri, aşağıdaki adımları kullanın hello tooget:

1. Gelen **uygulama kayıtlar** uygulamanızı Azure Active Directory'de seçin.

     ![Uygulama seçin](./media/resource-group-create-service-principal-portal/select-app.png)
2. Kopya hello **uygulama kimliği** ve uygulama kodunuzda saklayın. Merhaba hello uygulamalarda [örnek uygulamaları](#sample-applications) toothis değeri hello istemci kimliği olarak bölümüne bakın.

     ![istemci kimliği](./media/resource-group-create-service-principal-portal/copy-app-id.png)
3. toogenerate bir kimlik doğrulama anahtarı seçin **anahtarları**.

     ![anahtarları seçin](./media/resource-group-create-service-principal-portal/select-keys.png)
4. Merhaba anahtarı ve bir süre hello anahtarı için bir açıklama sağlayın. İşiniz bittiğinde, seçin **kaydetmek**.

     ![anahtarı Kaydet](./media/resource-group-create-service-principal-portal/save-key.png)

     Başlangıç anahtarı kaydedildikten sonra hello anahtarın hello değeri görüntülenir. Bu değer, değil mümkün tooretrieve hello anahtarı daha sonra olduğundan kopyalayın. Merhaba anahtar değeri Merhaba uygulaması hello uygulama kimliği toolog sağlar. Burada, uygulamanızın alabildiği hello anahtar değer deposu.

     ![anahtar kaydedildi](./media/resource-group-create-service-principal-portal/copy-key.png)

## <a name="get-tenant-id"></a>Kiracı Kimliğinizi alma
Program aracılığıyla oturum açarken, kimlik doğrulama isteği ile toopass hello Kiracı kimliği gerekir. 

1. tooget hello Kiracı kimliği, select **özellikleri** Azure AD kiracınız için. 

     ![Azure AD Özellikler'i seçin](./media/resource-group-create-service-principal-portal/select-ad-properties.png)

2. Kopya hello **dizin kimliği**. Bu değer, Kiracı kimliğidir.

     ![Kiracı kimliği](./media/resource-group-create-service-principal-portal/copy-directory-id.png)

## <a name="assign-application-toorole"></a>Uygulama toorole atayın
tooaccess kaynakları aboneliğinizde hello uygulama tooa rolünü atamanız gerekir. Merhaba uygulaması hello doğru izinleri rolünü karar verin. toolearn hello kullanılabilir rolleri hakkında bkz [RBAC: yerleşik roller](../active-directory/role-based-access-built-in-roles.md).

Merhaba kapsam hello abonelik, kaynak grubu ya da kaynak hello düzeyinde ayarlayabilirsiniz. Kapsam düzeyleri devralınan toolower izinlerdir. Örneğin, bir kaynak grubu için bir uygulama toohello okuyucu rolüne geldiğini ekleme hello kaynak grubu ve içerdiği tüm kaynaklar okuyabilir.

1. Toohello tooassign hello uygulamaya istediğiniz kapsam düzeyine gidin. Örneğin, tooassign hello abonelik kapsamında bir rol seçin **abonelikleri**. Bunun yerine, bir kaynak grubu veya kaynak seçebilirsiniz.

     ![Abonelik seç](./media/resource-group-create-service-principal-portal/select-subscription.png)

2. Merhaba belirli abonelik (kaynak grubu veya kaynak) tooassign hello uygulamaya seçin.

     ![atama için abonelik seçin](./media/resource-group-create-service-principal-portal/select-one-subscription.png)

3. Seçin **erişim denetimi (IAM)**.

     ![erişim seçin](./media/resource-group-create-service-principal-portal/select-access-control.png)

4. **Add (Ekle)** seçeneğini belirleyin.

     ![Select ekleme](./media/resource-group-create-service-principal-portal/select-add.png)
6. Tooassign toohello uygulama istediğiniz hello rolü seçin. Merhaba aşağıdaki resimde gösterilmiştir hello **okuyucu** rol.

     ![Rol Seç](./media/resource-group-create-service-principal-portal/select-role.png)

8. Uygulamanız için arayın ve seçin.

     ![uygulamayı arayın](./media/resource-group-create-service-principal-portal/search-app.png)
9. Seçin **Tamam** toofinish hello rol atama. Merhaba listesinde uygulamanızın tooa rolü bu kapsamı için atanan kullanıcılar veya bakın.

## <a name="log-in-as-hello-application"></a>Merhaba uygulaması oturum açın

Uygulamanız artık Azure Active Directory'de ayarlanır. Bir kimliği ve Merhaba uygulaması oturum açmak için anahtar toouse var. Merhaba uygulaması, belirli eylemleri verir tooa rolü atanır. Farklı platformlarda üzerinden hello uygulama olarak oturum açma hakkında daha fazla bilgi için bkz:

* [PowerShell](resource-group-authenticate-service-principal.md#provide-credentials-through-powershell)
* [Azure CLI](resource-group-authenticate-service-principal-cli.md#provide-credentials-through-azure-cli)
* [REST](/rest/api/#create-the-request)
* [.NET](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [Java](/java/azure/java-sdk-azure-authenticate)
* [Node.js](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [Python](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [Ruby](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)


## <a name="next-steps"></a>Sonraki adımlar
* çok kiracılı uygulamasının tooset bkz [Geliştirici Kılavuzu tooauthorization hello Azure Kaynak Yöneticisi API'si ile](resource-manager-api-authentication.md).
* güvenlik ilkeleri belirtme hakkında toolearn bkz [Azure rol tabanlı erişim denetimi](../active-directory/role-based-access-control-configure.md).  
* Verilen veya toousers reddedilen kullanılabilir eylemler listesi için bkz: [Azure Resource Manager kaynak sağlayıcısı işlemleri](../active-directory/role-based-access-control-resource-provider-operations.md).
