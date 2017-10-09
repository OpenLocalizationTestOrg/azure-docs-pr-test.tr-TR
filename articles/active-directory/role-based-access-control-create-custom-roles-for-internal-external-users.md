---
title: "aaaCreate özel rol tabanlı erişim denetimi rolleri ve toointernal ve azure'da dış kullanıcılar atayın | Microsoft Docs"
description: "İç ve dış kullanıcılar için PowerShell ve CLI kullanılarak oluşturulan özel RBAC Rolleri Ata"
services: active-directory
documentationcenter: 
author: andreicradu
manager: catadinu
editor: kgremban
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/10/2017
ms.author: a-crradu
ms.openlocfilehash: 26793a66d6ca2f771338eed87d10ce2b3b431841
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
## <a name="intro-on-role-based-access-control"></a>Giriş rol tabanlı erişim denetimi hakkında

Rol tabanlı erişim denetimi belirli kaynak kapsamları ortamlarında yönetebilen tooassign ayrıntılı rolleri tooother kullanıcıların bir abonelik hello sahipleri vererek bir Azure portal yalnızca özelliğidir.

Dış ortak çalışanları, satıcılar veya ortamınızda ancak mutlaka toohello tüm altyapının veya herhangi bir toospecific kaynaklara erişim freelancers ile çalışma RBAC büyük kuruluşlarda ve SMB'ler için daha iyi güvenlik yönetimi sağlar Faturalama ilgili kapsamlar. RBAC hello yönetici hesabı (Hizmet Yöneticisi rolü bir abonelik düzeyinde) tarafından yönetilen bir Azure aboneliğine sahip hello esnekliği sağlar ve sahip birden çok kullanıcıları davet toowork altında hello aynı aboneliği olmadan herhangi Yönetim Bu hakları. Yönetim ve fatura perspektifi hello RBAC Özelliği Azure çeşitli senaryolarda kullanmak için saat ve yönetim verimli bir seçenek toobe kanıtlar.

## <a name="prerequisites"></a>Ön koşullar
RBAC hello Azure ortamı kullanmanız gerekir:

* Tek başına sahip Azure aboneliği toohello kullanıcı (abonelik rolü) sahibi olarak atanmış.
* Merhaba sahibi hello Azure aboneliği rolünüz
* Erişim toohello sahip [Azure portalı](https://portal.azure.com)
* Kaynak sağlayıcıları aşağıdaki toohave hello hello kullanıcı abonelik için kayıtlı olduğundan emin olun: **Microsoft.Authorization**. Nasıl tooregister hello kaynak sağlayıcıları ile ilgili daha fazla bilgi için bkz: [Resource Manager sağlayıcıları, bölgeleri, API sürümleri ve şemaları](/azure-resource-manager/resource-manager-supported-services.md).

> [!NOTE]
> Office 365 aboneliği veya Azure Active Directory lisansları (örneğin: tooAzure Active Directory erişimi) portal yok kalitesi RBAC kullanarak hello O365 sağlandı.

## <a name="how-can-rbac-be-used"></a>RBAC nasıl kullanılabileceğini
RBAC, Azure üç farklı kapsamlar adresindeki uygulanabilir. Merhaba yüksek kapsam toohello düşük bir, bunlar şu şekildedir:

* Abonelik (yüksek)
* Kaynak grubu
* Kaynak kapsamı (tooan tek başına bir Azure kaynak kapsam hedeflenen izinleri sunumu hello düşük erişim düzeyi)

## <a name="assign-rbac-roles-at-hello-subscription-scope"></a>Merhaba abonelik kapsamında RBAC Rolleri Ata
RBAC kullanılan (ancak bunlarla sınırlı olmamak kaydıyla olduğunda) iki ortak örnekler vardır:

* Dış kullanıcılar hello kuruluşların (Merhaba yönetici kullanıcının Azure Active Directory Kiracı parçası değil) sahip toomanage belirli kaynaklar veya hello tüm abonelik davet
* Merhaba kuruluş (bunlar hello kullanıcının Azure Active Directory Kiracı parçası olan), ancak farklı ekipler veya ayrıntılı erişmeniz gruplarını parçası içindeki kullanıcılarla ya da toohello çalışma, tüm abonelik veya toocertain kaynak grupları veya kaynak hello kapsamları ortamı

## <a name="grant-access-at-a-subscription-level-for-a-user-outside-of-azure-active-directory"></a>Azure Active Directory dışındaki bir kullanıcı için erişim izni ver abonelik düzeyinde
RBAC rolleri olanağı verilir yalnızca **sahipleri** hello aboneliği, bu nedenle hello yönetici kullanıcı, önceden atanmış bu rolü veya hello Azure aboneliği oluşturduğu bir kullanıcı adıyla oturum açmış olmanız gerekir.

Hello Azure portal sonra oturum açma yönetici, seçin "Abonelikleri" ve seçtiğiniz hello bir istenen.
![Azure portalında abonelik dikey penceresinde](./media/role-based-access-control-create-custom-roles-for-internal-external-users/0.png) hello yönetici kullanıcı hello Azure aboneliği satın aldıysa varsayılan olarak, hello kullanıcı olarak görüntülenecek **Hesap Yöneticisi**, bu hello abonelik rol bırakılıyor. Hello Azure aboneliği rolleri hakkında daha fazla bilgi için bkz: [hello abonelik ya da hizmetleri yönetmek ekleme veya değiştirme Azure yönetici rolleri](/billing/billing-add-change-azure-subscription-administrator.md).

Bu örnekte, kullanıcı hello "alflanigan@outlook.com" Merhaba olan **sahibi** "Ücretsiz deneme" hello hello AAD abonelikte Kiracı "varsayılan Kiracı Azure". Bu kullanıcı hello Azure aboneliği hello ile Merhaba oluşturan olduğundan Microsoft Account "Outlook" ilk (Microsoft Account Outlook, Canlı vb. =) bu Kiracı eklenen diğer tüm kullanıcılar için hello varsayılan etki alanı adı olacaktır **"@alflaniganuoutlook.onmicrosoft.com"**. Tasarım gereği, birlikte hello Kiracı ve ekleme hello uzantısı oluşturan hello kullanıcının hello kullanıcı adı ve etki alanı adı koyarak hello sözdizimi hello yeni etki alanının biçimlendirildiğinden **". onmicrosoft.com"**.
Ayrıca, kullanıcıların oturum hello Kiracı içinde bir özel etki alanı adıyla ekleme ve hello yeni Kiracı için doğruladıktan sonra açma. Tooverify bir Azure Active Directory Kiracı özel etki alanı adının nasıl görürüm hakkında daha fazla ayrıntı için [bir özel etki alanı adı tooyour dizin eklemek](/active-directory/active-directory-add-domain).

Bu örnekte, yalnızca hello etki alanı adına sahip kullanıcılar hello "varsayılan Kiracı Azure" dizinini içeren "@alflanigan.onmicrosoft.com".

Merhaba abonelik seçtikten sonra hello yönetici kullanıcı tıklatmalısınız **erişim denetimi (IAM)** ve ardından **yeni rol ekleme**.





![erişim denetimi IAM Özelliği Azure portalında](./media/role-based-access-control-create-custom-roles-for-internal-external-users/1.png)





![erişim denetimi IAM Özelliği Azure portalında yeni kullanıcı Ekle](./media/role-based-access-control-create-custom-roles-for-internal-external-users/2.png)

Merhaba sonraki atanan tooselect hello rol toobe ve hello RBAC rolü atandı hello kullanıcıyı adımdır. Merhaba, **rol** açılır menü hello yönetici kullanıcı Azure'da kullanılabilen yalnızca hello yerleşik RBAC rolleri görür. Her rol ve bunların atanabilir kapsamların açıklamalarını ayrıntılı için bkz: [Azure rol tabanlı erişim denetimi için yerleşik roller](/active-directory/role-based-access-built-in-roles.md).

Merhaba yönetici kullanıcı ardından hello dış kullanıcı tooadd hello e-posta adresi gerekiyor. Merhaba hello dış kullanıcı toonot görünecektir Kiracı varolan hello için davranış bekleniyordu. Merhaba dış kullanıcı davet sonra kendisinin altında görünür olacak **abonelikleri > erişim denetimi (IAM)** hello abonelik kapsamını bir RBAC rolü atanmış olan tüm hello geçerli kullanıcılar ile.





![izinleri toonew RBAC rolü Ekle](./media/role-based-access-control-create-custom-roles-for-internal-external-users/3.png)





![Abonelik düzeyinde RBAC rollerinin listesi](./media/role-based-access-control-create-custom-roles-for-internal-external-users/4.png)

Merhaba kullanıcı "chessercarlton@gmail.com" davet edilen toobe bırakıldı bir **sahibi** hello "Ücretsiz deneme" aboneliği için. Hello davet gönderdikten sonra hello dış kullanıcı etkinleştirme bağlantısı ile bir e-posta onayı alacaksınız.
![e-posta daveti RBAC rolü için](./media/role-based-access-control-create-custom-roles-for-internal-external-users/5.png)

Dış toohello kuruluş olmasının, hello yeni kullanıcı varolan öznitelikleri hello "varsayılan Kiracı Azure" dizininde yok. Merhaba dış kullanıcı onayı toobe kendisine bir role atanan hello aboneliği ile ilişkili olan hello dizinde kayıtlı verdiği sonra bunlar oluşturulur.





![RBAC rolü için e-posta davet iletisi](./media/role-based-access-control-create-custom-roles-for-internal-external-users/6.png)

Merhaba dış kullanıcı hello Azure Active Directory Kiracı şu andan itibaren dış kullanıcı olarak gösterilir ve bu hello Azure portalına hem hello Klasik Portalı'nda görüntülenebilir.





![Kullanıcılar dikey azure active Directory'yi Azure portalı](./media/role-based-access-control-create-custom-roles-for-internal-external-users/7.png)





![Kullanıcılar dikey azure active directory Klasik Azure portalı](./media/role-based-access-control-create-custom-roles-for-internal-external-users/8.png)

Merhaba, **kullanıcılar** hem portalları hello dış kullanıcılar görünümünde tarafından tanımasını:

* hello Azure portal Hello farklı simge türü
* başlangıç noktası hello Klasik Portalı'ndaki kaynak Hizmeti'nden farklı

Ancak, verme **sahibi** veya **katkıda bulunan** hello kullanıcıya erişim tooan dış **abonelik** kapsam, hello erişim toohello yönetici kullanıcının dizin izin vermiyor sürece hello **genel yönetici** verir. Merhaba kullanıcı proprieties içinde hello **kullanıcı türü** iki ortak parametreleri olan **üye** ve **Konuk** tanımlanabilir. Konuk kullanıcı davet toohello directory bir dış kaynaktan olsa da, hello dizinde kayıtlı bir kullanıcı bir üyesidir. Daha fazla bilgi için bkz: [nasıl Azure Active Directory yöneticileri ekleyin B2B işbirliği kullanıcılar](/active-directory/active-directory-b2b-admin-add-users).

> [!NOTE]
> Merhaba Portalı'nda Hello kimlik bilgilerini girdikten sonra hello dış kullanıcı hello doğru dizinde toosign-için seçtiği emin olun. Merhaba aynı kullanıcı erişim toomultiple dizinler sahiptir ve ya da bunlardan birini üst sağ taraftaki hello Azure portal hello hello kullanıcı tıklayarak seçebilir ve ardından hello uygun dizin hello açılır listeden seçin.

Merhaba dizinde Konuk olmasının, çalışırken hello dış kullanıcı hello Azure aboneliği için tüm kaynakları yönetebilir, ancak hello dizinine erişilemiyor.





![kısıtlı tooazure active Directory'yi Azure portalına erişim](./media/role-based-access-control-create-custom-roles-for-internal-external-users/9.png)

Azure Active Directory ve Azure aboneliği bir üst-alt ilişkisi gibi diğer Azure kaynaklarına sahip (örneğin: sanal makineler, sanal ağlar, web uygulamaları, depolama vb.) ile Azure aboneliğiniz yok. Tüm hello ikinci oluşturulur, yönetilen ve bir Azure aboneliği kullanılan toomanage hello erişim tooan Azure directory olsa da bir Azure aboneliği altında faturalandırılır. Daha fazla ayrıntı için bkz: [nasıl bir Azure aboneliği olan ilgili tooAzure AD](/active-directory/active-directory-how-subscriptions-associated-directory).

Tüm rollerden hello yerleşik RBAC, **sahibi** ve **katkıda bulunan** tooall kaynaklarında hello ortamı, katılımcı oluşturulamıyor hello fark olan ve yeni Sil tam yönetim erişimi sağlar RBAC rolleri. Merhaba diğer yerleşik roller ister **sanal makine Katılımcısı** tam yönetim erişimi yalnızca hello bakılmaksızın hello adıyla belirtilen toohello kaynakları sunan **kaynak grubu** bunlar oluşturuluyor .

Atama hello yerleşik RBAC rolü **sanal makine Katılımcısı** abonelik düzeyinde o hello kullanıcıya atanan hello rol anlamına gelir:

* Tüm sanal makineleri bakılmaksızın parçası olan kendi dağıtım tarihi ve hello kaynak grupları görüntüleyebilirsiniz
* Tam yönetim erişimi toohello sanal makineye hello abonelikte sahiptir
* Başka bir kaynak türleri hello abonelikte görüntüleyemezsiniz
* Fatura perspektifi değişiklikler çalıştırılamıyor

> [!NOTE]
> RBAC, Azure portal yalnızca özelliği olan erişim toohello Klasik portal izni vermez.

## <a name="assign-a-built-in-rbac-role-tooan-external-user"></a>Yerleşik RBAC rolü tooan dış kullanıcı atama
Bu test farklı bir senaryo için dış kullanıcı hello "alflanigan@gmail.com" olarak eklenen bir **sanal makine Katılımcısı**.




![sanal makine katkıda bulunan yerleşik rolü](./media/role-based-access-control-create-custom-roles-for-internal-external-users/11.png)

Bu yerleşik rolü bu dış kullanıcı için normal davranışı Hello toosee olduğu ve yalnızca sanal makineler ve bitişik kaynak yöneticisi yalnızca kaynaklarını dağıtırken gereken yönetin. Tasarım gereği, kısıtlı bu rolleri erişim hello Azure portalında oluşturulan yalnızca tootheir karşılık düşen kaynakları sunar, ne olursa olsun bazı hala hello Klasik Portalı'nda da dağıtılabilir (örneğin: sanal makineler).





![azure portalında sanal makine Katılımcısı rolüne genel bakış](./media/role-based-access-control-create-custom-roles-for-internal-external-users/12.png)

## <a name="grant-access-at-a-subscription-level-for-a-user-in-hello-same-directory"></a>GRANT erişim hello bir kullanıcı için bir abonelik düzeyinde aynı dizin
Merhaba işlem akışı aynı tooadding hem erişim toohello rolü verilmeden hello kullanıcı yanı sıra hello Yöneticisi perspektif izni veriliyor hello RBAC rolü bir dış kullanıcı olur. Merhaba burada oturum açtıktan sonra hello abonelik içindeki tüm hello kaynak kapsamları hello panosunda kullanılabilir olacak şekilde bu davet hello kullanıcının e-posta Davetleri almaz farktır.

## <a name="assign-rbac-roles-at-hello-resource-group-scope"></a>Merhaba Kaynak Grup kapsamı RBAC rollerini atama
Bir RBAC rolü atama bir **kaynak grubu** kapsamı hello abonelik düzeyinde, her iki tür kullanıcı - harici veya dahili hello rol atama için benzer bir işlem var (Merhaba parçası aynı dizinde). Merhaba hello RBAC rolü atanmış kullanıcılar olan kullanıcıların, ortamlarında toosee hello kaynak grubu, erişim hello atanmış yalnızca **kaynak grupları** hello Azure Portalı'ndaki simgesini.

## <a name="assign-rbac-roles-at-hello-resource-scope"></a>Merhaba kaynak kapsamda RBAC Rolleri Ata
Bir kaynak kapsamda Azure RBAC rolü atama hello rol hello abonelik düzeyinde veya hello kaynak grubu düzeyinde atamak için özdeş bir işlemi varsa, aşağıdaki hello aynı her iki senaryo için iş akışı. Merhaba RBAC rolü atanan hello kullanıcılar yalnızca, erişim için ya da hello atanmış olduğunu hello öğeleri yeniden görebilirsiniz **tüm kaynakları** sekmesini veya doğrudan kendi Pano.

RBAC hem kaynak grup kapsamı veya kaynak kapsamı için önemli bir yönü hello kullanıcılar toomake emin toosign bileşenini toohello doğru dizinidir.





![Azure portalında Directory oturum açma](./media/role-based-access-control-create-custom-roles-for-internal-external-users/13.png)

## <a name="assign-rbac-roles-for-an-azure-active-directory-group"></a>Bir Azure Active Directory grubu için RBAC Rolleri Ata
Merhaba üç farklı kapsamlarda yönetme, dağıtma ve hello olmayan atanmış bir kullanıcı olarak çeşitli kaynakları yönetme Azure teklifi hello ayrıcalık RBAC kullanarak tüm hello senaryoları, kişisel abonelik yönetebilme gerekir. Abonelik, kaynak grubu veya kaynak kapsamı için bakılmaksızın hello RBAC rolü atanmış, burada hello kullanıcıların erişimi hello bir Azure aboneliği altında hakkında daha fazla hello atanmış kullanıcılar tarafından oluşturulan tüm hello kaynakları faturalandırılır. Bu şekilde hello faturalama, tüm Azure aboneliğiniz için yönetici izinlerine sahip kullanıcılar sahip hello kaynakları yöneten bir eksiksiz bir genel bakış hello tüketim, ne olursa olsun.

Büyük kuruluşlar için RBAC rolleri uygulanabilir hello hello perspektif hello yönetici kullanıcının dikkate Azure Active Directory grupları ile aynı şekilde toogrant hello ayrıntılı erişim için ekipler veya değil ayrı ayrı her bir kullanıcı için tüm Departmanlar böylece istiyor son derece saat ve yönetim verimli isteğe bağlı olarak düşünebilirsiniz. tooillustrate Bu örnek, hello **katkıda bulunan** rol hello kiracısında hello abonelik düzeyinde hello gruplarının tooone eklendi.





![AAD grupları için RBAC rolü Ekle](./media/role-based-access-control-create-custom-roles-for-internal-external-users/14.png)

Bu grupları sağlanan ve yalnızca Azure Active Directory içinde yönetilen güvenlik gruplarıdır.

## <a name="create-a-custom-rbac-role-tooopen-support-requests-using-powershell"></a>Bir özel RBAC rolü tooopen destek istekleri PowerShell kullanarak oluşturma
Azure'da kullanılabilen hello yerleşik RBAC rolleri hello kullanılabilir kaynakları hello ortamında göre belirli izin düzeyleri emin olun. Ancak, bu rollerin hiçbiri hello yönetici kullanıcının gereksinimlerinize uygun değilse, hello seçeneği toolimit erişimi daha da olan en fazla özel RBAC rolleri oluşturarak yoktur.

Özel RBAC rolleri oluşturmak için bir yerleşik rol tootake gerekir, düzenlemek ve hello Ortamı'nda içeri aktarın. Merhaba indirme ve karşıya yükleme hello rolünün PowerShell veya CLI kullanarak yönetilir.

Merhaba abonelik düzeyinde ayrıntılı erişim vermek ve ayrıca destek isteği açma davet hello kullanıcı hello esneklik izin özel bir rol oluşturma önemli toounderstand hello Önkoşullar olur.

Bu örnek hello yerleşik rol için **okuyucu** hello kaynağın tüm kullanıcılara erişim tooview sağlayan değil tooedit bunları kapsamları veya yenilerini oluşturun bırakıldı destek isteği açma tooallow hello kullanıcı hello seçeneği özelleştirilmiş.

Merhaba verme işleminin ilk eylemin Hello **okuyucu** PowerShell'de tamamlandı rol gereksinimlerini toobe yönetici olarak yükseltilmiş izinlerle çalıştı.

```
Login-AzureRMAccount

Get-AzureRMRoleDefinition -Name "Reader"

Get-AzureRMRoleDefinition -Name "Reader" | ConvertTo-Json | Out-File C:\rbacrole2.json

```





![Okuyucu RBAC rolü için PowerShell ekran görüntüsü](./media/role-based-access-control-create-custom-roles-for-internal-external-users/15.png)

Daha sonra tooextract hello JSON şablonunu hello rolünün gerekir.





![Özel okuyucu RBAC rolü için JSON şablonunu](./media/role-based-access-control-create-custom-roles-for-internal-external-users/16.png)

Tipik bir RBAC rolü üç ana bölüm dışında oluşan **Eylemler**, **NotActions** ve **AssignableScopes**.

Merhaba, **eylem** bölümde listelenen tüm bu rol için izin verilen işlemler hello. Bu, her eylemin kaynak sağlayıcısından atandığı önemli toounderstand olur. Bu durumda, destek biletlerini hello oluşturmak için **Microsoft.Support** kaynak sağlayıcısı listelenmesi gerekir.

toobe mümkün toosee tüm kaynak sağlayıcıları kullanılabilir ve aboneliğinizde kayıtlı Merhaba, PowerShell'i kullanabilirsiniz.
```
Get-AzureRMResourceProvider

```
Ayrıca, tüm hello kullanılabilir PowerShell cmdlet'leri toomanage hello kaynak sağlayıcıları için hello kontrol edebilirsiniz.
    ![Kaynak sağlayıcısı yönetimi için PowerShell ekran görüntüsü](./media/role-based-access-control-create-custom-roles-for-internal-external-users/17.png)

Tüm eylemler için belirli bir RBAC rolü olan kaynak sağlayıcıları hello bölümü altında listelenen hello toorestrict **NotActions**.
Son olarak, bu hello RBAC rolü hello açık abonelik kullanıldığı kimlikleri içeriyor zorunludur. Merhaba abonelik kimlikleri hello altında listelenen **AssignableScopes**, aksi takdirde, tooimport hello rol aboneliğinizde izin verilmez.

Oluşturma ve hello RBAC rolü özelleştirme sonra toobe alınan geri hello ortamın gerekir.

```
New-AzureRMRoleDefinition -InputFile "C:\rbacrole2.json"

```

Bu örnekte, hello özel bu RBAC rolü için "Merhaba abonelik yanı sıra tooopen destek istekleri hello kullanıcı tooview her şeyi sağlayan okuyucu destek biletleri erişim düzeyi" adıdır.

> [!NOTE]
> Merhaba destek isteği açma hello eylemi izin verme yalnızca iki yerleşik RBAC rolleridir **sahibi** ve **katkıda bulunan**. Tüm destek isteklerini bir Azure aboneliğine yönelik temel alınarak oluşturulur çünkü bir kullanıcı toobe mümkün tooopen destek istekleri için kendisinin RBAC rolü yalnızca kapsamda hello abonelik, atanmış olması gerekir.

Bu yeni özel rolü hello tooan kullanıcıdan atanan aynı dizin.





![hello Azure portal içeri özel RBAC rolü ekran görüntüsü](./media/role-based-access-control-create-custom-roles-for-internal-external-users/18.png)





![Merhaba, içeri aktarılan özel RBAC rolü toouser atama ekran aynı dizinde](./media/role-based-access-control-create-custom-roles-for-internal-external-users/19.png)





![Özel alınan RBAC rolü izinlerini ekran görüntüsü](./media/role-based-access-control-create-custom-roles-for-internal-external-users/20.png)

Merhaba örneği daha fazla gibi ayrıntılı tooemphasize hello sınırları bu özel RBAC rolü bırakıldı:
* Yeni destek istekleri oluşturabilirsiniz
* Yeni kaynak kapsamlar oluşturulamıyor (örneğin: sanal makine)
* Yeni kaynak grupları oluşturulamıyor





![Özel RBAC rolü destek istekleri oluşturma ekran görüntüsü](./media/role-based-access-control-create-custom-roles-for-internal-external-users/21.png)





![ekran görüntüsü özel RBAC rolü erişilemiyor toocreate VM'ler](./media/role-based-access-control-create-custom-roles-for-internal-external-users/22.png)





![ekran görüntüsü özel RBAC rolü erişilemiyor toocreate yeni RGs](./media/role-based-access-control-create-custom-roles-for-internal-external-users/23.png)

## <a name="create-a-custom-rbac-role-tooopen-support-requests-using-azure-cli"></a>Bir özel RBAC rolü tooopen destek istekleri Azure CLI kullanarak oluşturma
Mac'te ve erişim tooPowerShell kalmadan, Azure CLI hello yolu toogo çalışıyor.

aynı, CLI kullanarak hello rol bir JSON şablonu, ancak bunu karşıdan yüklenemediğini hello tek özel durum ile Merhaba CLI görüntülenebilir hello Hello adımları toocreate özel bir rol var.

Bu örnek için ı hello yerleşik rolü seçtiniz **yedekleme okuyucu**.

```

azure role show "backup reader" --json

```





![CLI ekran görüntüsü yedekleme okuyucu rolüne Göster](./media/role-based-access-control-create-custom-roles-for-internal-external-users/24.png)

Visual Studio'da Hello rol bir JSON şablonu hello proprieties kopyaladıktan sonra düzenleme hello **Microsoft.Support** kaynak sağlayıcısı hello eklendi **Eylemler** bu kullanıcı açabileceği bölümler toobe hello yedekleme kasalarını için bir okuyucu devam ederken destek istekleri. Yeniden bu rolü hello nerede kullanılacak gerekli tooadd hello abonelik kimliği olan **AssignableScopes** bölümü.

```

azure role create --inputfile <path>

```





![Özel RBAC rolü alma CLI ekran görüntüsü](./media/role-based-access-control-create-custom-roles-for-internal-external-users/25.png)

Merhaba yeni rol hello Azure portalında kullanılabilir ve hello atamasını işlemi olduğundan hello aynı hello önceki örneklerde olduğu gibi.





![CLI 1.0 kullanılarak oluşturulan özel RBAC rolü Azure portal ekran görüntüsü](./media/role-based-access-control-create-custom-roles-for-internal-external-users/26.png)

İtibariyle Hello son yapı 2017, hello Azure bulut Kabuk genel kullanıma açıktır. Azure bulut Kabuk tamamlama tooIDE ve hello Azure Portal ' dir. Bu hizmeti ile kimlik doğrulaması ve Azure içinde barındırılan ve tarayıcı tabanlı bir kabuk alın ve makinenize yüklü CLI yerine kullanın.





![Azure bulut Kabuğu](./media/role-based-access-control-create-custom-roles-for-internal-external-users/27.png)
