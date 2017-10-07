---
title: "aaaCreate hello Azure portalında bir Batch hesabında | Microsoft Docs"
description: "Nasıl toocreate bir Azure Batch hesabı hello Azure portal toorun hello bulutta büyük ölçekli paralel iş yüklerini öğrenin"
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: 3fbae545-245f-4c66-aee2-e25d7d5d36db
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2176f88ba0a1a3298023de8f520d46ef28a664b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-batch-account-with-hello-azure-portal"></a>Hello Azure portal ile bir toplu işlem hesabı oluşturun

> [!div class="op_single_selector"]
> * [Azure portal](batch-account-create-portal.md)
> * [Batch Yönetimi .NET](batch-management-dotnet.md)
>
>

Nasıl toocreate bir Azure Batch hesabı hello öğrenin [Azure portal][azure_portal]ve işlem senaryonuzun sığacak hello hesap Özellikler'i seçin. Burada gibi erişim anahtarlarını ve hesap URL'leri toofind önemli hesap özelliklerini öğrenin.

Toplu işlem hesaplarını ve senaryoları hakkında arka plan için hello bkz [genel bakış özellik](batch-api-basics.md).



## <a name="create-a-batch-account"></a>Batch hesabı oluşturma

Merhaba portal toocreate toplu işlem hesabı hello iki birini kullanın *havuzu ayırma modları*: **Batch hizmeti** modu ya da daha yeni hello **kullanıcı aboneliği** daha fazlasını gerektiriyor modu yapılandırma. Bu iki modları hakkında daha fazla bilgi için bkz: Merhaba [genel bakış özellik](batch-api-basics.md#account). Ayrıca bkz: hello hello kullanıcı abonelik modunun özellikleri [blog gönderisi](https://blogs.technet.microsoft.com/windowshpc/2017/03/17/azure-batch-vnet-and-custom-image-support-for-virtual-machine-pools/).

## <a name="batch-service-mode"></a>Batch hizmeti modu



1. İçinde toohello oturum [Azure portal][azure_portal].
2. **Yeni** > **İşlem** > **Batch Hizmeti**'ne tıklayın.

    ![Toplu işlemde hello Market][marketplace_portal]
3. Merhaba **yeni toplu işlem hesabı** dikey penceresi görüntülenir. Her bir dikey pencere öğesinin Hello açıklamaları aşağıda konusuna bakın.

    ![Batch hesabı oluşturma][account_portal]

    a. **Hesap adı**: hello toplu işlem hesabı adı seçtiğiniz hello hesabın oluşturulduğu Azure bölgesinde hello içinde benzersiz olmalıdır (bkz **konumu** aşağıda). Merhaba hesap adı yalnızca küçük harf karakterler ya da sayı içerebilir ve 3-24 karakter uzunluğunda olmalıdır.

    b. **Abonelik**: Merhaba hangi toocreate hello toplu işlem hesabı abonelikte. Yalnızca bir aboneliğiniz varsa, varsayılan olarak seçilidir.

    c. **Havuz ayırma modu**: **Batch hizmeti**’ni seçin.

    c. **Kaynak grubu**: Yeni Batch hesabınız için mevcut bir kaynak grubu seçebilir ya da isterseniz yeni bir tane oluşturabilirsiniz.

    d. **Konum**: hangi toocreate hello toplu işlem hesabı Azure bölgesinde hello. Yalnızca abonelik ve kaynak grubu tarafından desteklenen hello bölgeler seçenek olarak görüntülenir.

    e. **Depolama hesabı** (isteğe bağlı): Batch hesabınızla ilişkilendireceğiniz genel amaçlı depolama hesabı. Çoğu Batch hesabı için önerilen seçenek budur. Daha fazla bilgi için bu makalenin sonraki bölümlerinde [Bağlı Azure Depolama hesabı](#linked-azure-storage-account) konusuna bakın.

4. Tıklatın **oluşturma** toocreate hello hesabı.

   Merhaba portal dağıtımı devam ediyor gösterir. İşlem tamamlandıktan sonra **Bildirimler** bölümünde **Dağıtım başarılı** bildirimi görünür.

## <a name="user-subscription-mode"></a>Kullanıcı aboneliği modu

### <a name="allow-azure-batch-tooaccess-hello-subscription-one-time-operation"></a>Azure Batch tooaccess hello abonelik (bir defalık işlem) izin ver
İlk Batch hesabınıza kullanıcı abonelik modunda oluştururken, aşağıdaki adımları tooregister hello toplu aboneliğinizle gerçekleştirin. (Daha önce bu kaldırdıysanız, toohello sonraki bölüme atlayın.)

1. İçinde toohello oturum [Azure portal][azure_portal].

2. Tıklatın **daha Hizmetleri** > **abonelikleri**, hello abonelik istediğiniz toouse hello toplu işlem hesabı için'a tıklayın.

3. Merhaba, **abonelik** dikey penceresinde tıklatın **erişim denetimi (IAM)** > **Ekle**.

    ![Abonelik erişim denetimi][subscription_access]

4. Merhaba üzerinde **izinleri eklemek** dikey penceresinde, select hello **katkıda bulunan** rolü, toplu işlem API hello arayın. Arama hello API bulana kadar bu dizelerin her biri için:
    1. **MicrosoftAzureBatch**.
    2. **Microsoft Azure Batch**. Daha yeni Azure AD kiracıları bu adı kullanıyor olabilir.
    3. **ddbf3205-c6bd-46ae-8127-60eb93363864** hello toplu API hello kimliğidir. 

5. Hello toplu API bulduktan sonra onu seçin ve tıklatın **kaydetmek**.

    ![Batch izinleri ekleme][add_permission]

### <a name="create-a-key-vault"></a>Bir anahtar kasası oluşturma
Azure anahtar kasası kullanıcı abonelik modunda gerekli olan toothe ait aynı kaynak grubunda oluşturulan hello toplu işlem hesabı toobe. Merhaba kaynak grubu toplu olduğu bir bölgede olduğundan emin olun [kullanılabilir](https://azure.microsoft.com/regions/services/) ve aboneliğinizi destekleyen.

1. Merhaba, [Azure portal][azure_portal], tıklatın **yeni** > **güvenlik + kimlik** > **anahtar kasası** .

2. Merhaba, **anahtar kasası oluşturma** dikey penceresinde hello anahtar kasası için bir ad girin ve toplu işlem hesabı için istediğiniz hello bölgede bulunan bir kaynak grubu oluşturun. Varsayılan değerleri ayarları kalan hello bırakın ve ardından **oluşturma**.

### <a name="create-a-batch-account"></a>Batch hesabı oluşturma

1. Merhaba, [Azure portal][azure_portal], tıklatın **yeni** > **işlem** > **Batch hizmeti**.

    ![Toplu işlemde hello Market][marketplace_portal]
3. Merhaba **yeni toplu işlem hesabı** dikey penceresi görüntülenir. Her bir dikey pencere öğesinin Hello açıklamaları aşağıda konusuna bakın.

    ![Batch hesabı oluşturma][account_portal_byos]

    a. **Hesap adı**: hello toplu işlem hesabı adı seçtiğiniz hello hesabın oluşturulduğu Azure bölgesinde hello içinde benzersiz olmalıdır (bkz **konumu** aşağıda). Merhaba hesap adı yalnızca küçük harf karakterler ya da sayı içerebilir ve 3-24 karakter uzunluğunda olmalıdır.

    b. **Abonelik**: birden fazla aboneliğiniz varsa, Batch hizmeti hello ile kayıtlı hello aboneliği seçin.

    c. **Havuzu ayırma modu**: **Kullanıcı aboneliği**’ni seçin.

    d. **Anahtar kasası**: Batch hesabınızın hello önceki bölümde oluşturduğunuz Select hello anahtar kasası. İsteğe bağlı olarak, yeni bir anahtar kasası oluşturun. Merhaba kasası seçtikten sonra hello onay kutusunu toogrant Azure Batch erişim toohello anahtar kasası seçin.

    c. **Kaynak grubu**: hello anahtar kasası oluşturulan Select hello kaynak grubu.

    d. **Konum**: hello anahtar kasası hello toplu işlem hesabı için oluşturulan Azure bölgesi hello.

    e. **Depolama hesabı** (isteğe bağlı): Batch hesabınızla ilişkilendireceğiniz genel amaçlı depolama hesabı. Çoğu Batch hesabı için önerilen seçenek budur. Daha fazla bilgi için aşağıdaki [Bağlı Azure Storage hesabı](#linked-azure-storage-account) konusuna bakın.

4. Tıklatın **oluşturma** toocreate hello hesabı.

   Merhaba portal dağıtımı devam ediyor gösterir. İşlem tamamlandıktan sonra **Bildirimler** bölümünde **Dağıtım başarılı** bildirimi görünür.



## <a name="view-batch-account-properties"></a>Batch hesabı özelliklerini görüntüleme
Merhaba hesabı oluşturulduktan sonra hello açabilirsiniz **Batch hesabı dikey** tooaccess kendi ayarları ve özellikleri. Tüm hesap ayarları ve özellikleri hello Batch hesabı dikey penceresinde, soldaki menüden hello kullanarak erişebilirsiniz.

![Azure portalında Batch hesabı dikey penceresi][account_blade]

* **Batch hesabı URL'si**: hello sahip bir uygulama geliştirirken [Batch API'lerini](batch-apis-tools.md#azure-accounts-for-batch-development), bir hesap URL tooaccess Batch kaynaklarınız ihtiyacınız vardır. Bir Batch hesabı URL'si biçimi aşağıdaki hello sahiptir:

    `https://<account_name>.<region>.batch.azure.com`

![Portalda Batch hesabı URL’si][account_url]

* **Erişim tuşları** (toplu işlem hizmeti mod): tooauthenticate erişim tooyour toplu işlem hesabı uygulamanızdan, hesap erişim anahtarı gerekir. (Bu ayar, Azure Active Directory kimlik doğrulamasını kullandığınız kullanıcı aboneliği modunda mevcut değildir.)

    Batch hesabınızın erişim anahtarlarını tooview veya yeniden girin `keys` hello soldaki menüde **arama** kutusunda hello Batch hesabı dikey penceresinde, ardından seçin **anahtarları**.

    ![Azure portalında Batch hesabı anahtarları][account_keys]

[!INCLUDE [batch-pricing-include](../../includes/batch-pricing-include.md)]

## <a name="linked-azure-storage-account"></a>Bağlı Azure Storage hesabı

Genel amaçlı bir Azure depolama hesabı tooyour toplu işlem hesabı isteğe bağlı olarak bağlayabilirsiniz. Merhaba [uygulama paketleri](batch-application-packages.md) toplu özelliği hello yaptığı gibi Azure Blob Depolama kullanır [toplu iş dosyası kuralları .NET](batch-task-output.md) kitaplığı. Bu isteğe bağlı özellikler, toplu görevlerinizin çalıştığı hello uygulamaları dağıtma ve oluşturdukları kalıcı hello veri yardımcı.

Yalnızca Batch hesabınız tarafından kullanılacak yeni bir Depolama hesabı oluşturmanız önerilir.

![Genel amaçlı depolama hesabı oluşturma][storage_account]

> [!NOTE]
> Azure toplu işlem şu anda yalnızca hello genel amaçlı depolama hesabı türünü destekler. Bu hesap türü [Azure depolama hesapları hakkında](../storage/common/storage-create-storage-account.md) belgesinin 5. adımında [Depolama hesabı oluşturma] (../storage/common/storage-create-storage-account.md#create-a-storage-account) açıklanmıştır.
>
>

> [!WARNING]
> Merhaba, bağlantılı bir depolama hesabının erişim anahtarlarını yeniden oluştururken dikkatli olun. Yalnızca bir depolama hesabı anahtarı yeniden oluşturmak ve tıklayın **anahtarları Eşitle** depolama hesabı dikey penceresinde hello üzerinde bağlı. Gerekirse diğer anahtarı hello tooallow hello anahtarları toopropagate toohello işlem düğümleri, havuzlar, ardından yeniden ve eşitleme beş dakika bekleyin. Her ikisini de yeniden oluşturursanız hello aynı anahtarları süresi, işlem düğümleriniz mümkün toosynchronize ya da anahtar olmayacak ve erişim toohello depolama hesabı kaybedersiniz.
>
>

![Depolama hesabı anahtarlarını yeniden oluşturma][4]

## <a name="batch-service-quotas-and-limits"></a>Batch hizmet kotaları ve limitleri
Lütfen olması olarak Azure aboneliğinize ve diğer Azure hizmetlerini kullanan, belirli [kotalar ve sınırlar](batch-quota-limit.md) tooBatch hesapları uygulayın. Bir toplu işlem hesabı için geçerli kotalar görünür hello hesabındaki hello portalında **özellikleri**.

![Azure portalında Batch hesabı kotaları][quotas]



Ayrıca, bu kotalar çoğunu hello Azure portal yalnızca bir ücretsiz ürün destek isteği gönderildi ile artırılabilir. Bkz: [hello Azure Batch hizmeti için kotalar ve sınırlar](batch-quota-limit.md) kota artar isteme ile ilgili ayrıntılar için.

## <a name="other-batch-account-management-options"></a>Diğer Batch hesabı yönetim seçenekleri
Ayrıca toousing Merhaba Azure portal, da oluşturabilir ve hello aşağıdaki Batch hesaplarıyla yönetebilirsiniz:

* [Batch PowerShell cmdlet’leri](batch-powershell-cmdlets-get-started.md)
* [Azure CLI](batch-cli-get-started.md)
* [Batch Yönetimi .NET](batch-management-dotnet.md)

## <a name="next-steps"></a>Sonraki adımlar
* Merhaba bkz [Batch özelliklerine genel bakış](batch-api-basics.md) toolearn Batch hizmeti kavramları ve özellikler hakkında daha fazla bilgi. Merhaba makale havuzlar, işlem düğümleri, işler ve görevler gibi birincil Batch kaynaklarını hello açıklanır ve büyük ölçekli işlem iş yükü yürütmeye hizmetin özellikleri hello genel bir bakış sağlar.
* Hello kullanarak Batch özellikli bir uygulama geliştirme hello temellerini öğrenin [Batch .NET istemci kitaplığını](batch-dotnet-get-started.md) veya [Python](batch-python-tutorial.md). Bu Tanıtım makaleler hello Batch hizmeti tooexecute bir iş yükü birden çok işlem düğümlerinde kullanır ve iş yükü dosyası hazırlama ve alma için Azure Storage kullanmayı da içeren çalışan bir uygulama size kılavuzluk eder.

[api_net]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[api_rest]: https://msdn.microsoft.com/library/azure/Dn820158.aspx

[azure_portal]: https://portal.azure.com
[batch_pricing]: https://azure.microsoft.com/pricing/details/batch/

[4]: ./media/batch-account-create-portal/batch_acct_04.png "Depolama hesabı anahtarlarını yeniden oluşturma"
[marketplace_portal]: ./media/batch-account-create-portal/marketplace_batch.PNG
[account_blade]: ./media/batch-account-create-portal/batch_blade.png
[account_portal]: ./media/batch-account-create-portal/batch_acct_portal.png
[account_keys]: ./media/batch-account-create-portal/account_keys.PNG
[account_url]: ./media/batch-account-create-portal/account_url.png
[storage_account]: ./media/batch-account-create-portal/storage_account.png
[quotas]: ./media/batch-account-create-portal/quotas.png
[subscription_access]: ./media/batch-account-create-portal/subscription_iam.png
[add_permission]: ./media/batch-account-create-portal/add_permission.png
[account_portal_byos]: ./media/batch-account-create-portal/batch_acct_portal_byos.png
