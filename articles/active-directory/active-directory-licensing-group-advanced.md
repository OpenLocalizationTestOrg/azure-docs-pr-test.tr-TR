---
title: "Active Directory grup tabanlı ilave senaryolar lisans aaaAzure | Microsoft Docs"
description: "Azure Active Directory grup tabanlı lisans için daha fazla senaryoları"
services: active-directory
keywords: Azure AD lisanslama
documentationcenter: 
author: curtand
manager: femila
editor: piotrci
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/02/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 782b7c9aa1c062a55c1241d69af673466f7a849c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="scenarios-limitations-and-known-issues-using-groups-toomanage-licensing-in-azure-active-directory"></a>Senaryoları, sınırlamaları ve bilinen sorunlar grupları toomanage Azure Active Directory'de Lisansı'nı kullanma

Bilgi ve örnekler toogain grup tabanlı Azure Active Directory (Azure AD) lisanslama'nın daha gelişmiş bir anlayış aşağıdaki hello kullanın.

## <a name="usage-location"></a>Kullanım konumu

Bazı Microsoft Hizmetleri tüm konumlarda kullanılabilir değil. Bir lisans tooa kullanıcı atanabilmesi için önce Merhaba yönetici toospecify hello sahip **kullanım konumu** hello kullanıcı özelliği. İçinde [Azure portal hello](https://portal.azure.com), belirleyebilirsiniz **kullanıcı** &gt; **profil** &gt; **ayarları**.

Grup lisans atama için belirtilen bir kullanım konumu olmayan tüm kullanıcılar hello dizininin hello konumu devralır. Birden çok konumda kullanıcılar varsa, emin tooreflect, doğru kullanıcı nesnelerinizi lisansına sahip kullanıcılar toogroups eklemeden önce yapın.

> [!NOTE]
> Grup lisans atamasını hiçbir zaman bir kullanıcı için kullanım konumu var olan bir değerle değiştirecek. Her zaman kullanım konumu, kullanıcı oluşturma akışının bir parçası lisans atamasını hello sonucu her zaman doğru olduğundan ve kullanıcıların olmayan konumlarda Hizmetleri almıyorsunuz sağlayacak Azure ad (örneğin AAD Connect yapılandırması aracılığıyla) - ayarlamanızı öneririz izin verilir.

## <a name="use-group-based-licensing-with-dynamic-groups"></a>Grup tabanlı dinamik gruplarla lisans kullanın

Azure AD dinamik gruplarla birleştirilebilir yani herhangi bir güvenlik grubuyla grup tabanlı lisans kullanabilirsiniz. Kullanıcı nesnesi öznitelik tooautomatically karşı kuralları çalıştırmak dinamik grupların ekleyin ve kullanıcıların gruplardan kaldırın.

Örneğin, dinamik bir grup oluşturabilirsiniz bazı ürün kümesi için tooassign toousers istiyor. Her grup, kullanıcı tarafından öznitelikleriyle ekleme kuralı tarafından doldurulur ve bunları tooreceive istediğiniz atanan hello lisans her grubudur. Merhaba özniteliği şirket içi atayın ve Azure AD ile eşitleme veya doğrudan hello bulutta hello özniteliği yönetebilirsiniz.

Kısa süre içinde toohello grubuna eklendikten sonra toohello kullanıcı lisansı atanır. Merhaba öznitelik değiştiğinde hello kullanıcı hello grupları bırakır ve hello lisansları kaldırılır.

### <a name="example"></a>Örnek

Hangi kullanıcıların erişim tooMicrosoft web hizmetleri olmalıdır karar bir şirket içi kimlik yönetimi çözümü Hello örneği göz önünde bulundurun. Kullandığı **extensionAttribute1** toostore bir dize değeri temsil eden hello lisansları hello kullanıcı olmalıdır. Azure AD Connect, Azure AD ile eşitlenir.

Kullanıcılar bir gerekebilir ancak olmayan başka bir lisans ya da her ikisini de gerekebilir. Office 365 Kurumsal E5 ve Enterprise Mobility dağıtıyorsanız + (EMS) güvenlik gruplarındaki toousers lisansları bir örnek aşağıda verilmiştir:

#### <a name="office-365-enterprise-e5-base-services"></a>Office 365 Kurumsal E5: temel Hizmetleri

![Ekran Office 365 Kurumsal E5 temel Hizmetleri](media/active-directory-licensing-group-advanced/o365-e5-base-services.png)

#### <a name="enterprise-mobility--security-licensed-users"></a>Enterprise Mobility + Security: lisanslı kullanıcılar

![Ekran görüntüsü, Enterprise Mobility + Security kullanıcıları lisanslı](media/active-directory-licensing-group-advanced/o365-e5-licensed-users.png)

Bu örnek için bir kullanıcı değiştirebilir ve kendi extensionAttribute1 toohello değerini `EMS;E5_baseservices;` hem lisans hello kullanıcı toohave istiyorsanız. Bu değişikliği yapmak şirket içi. Merhaba sonra eşitlemeler hello bulut ile değiştirmek, hello kullanıcı tooboth grupları otomatik olarak eklenir ve lisansları atanır.

![Nasıl tooset hello kullanıcının extensionAttribute1 gösteren ekran görüntüsü](media/active-directory-licensing-group-advanced/user-set-extensionAttribute1.png)

> [!WARNING]
> Varolan bir grubun üyeliğini kuralını değiştirirken dikkatli olun. Bir kural değiştirildiğinde, hello hello grup üyeliğini tekrar değerlendirilir olacaktır ve artık eşleşmeyen kullanıcılar hello yeni kural kaldırılır (hala hello yeni kural eşleşen kullanıcılar etkilenmez bu işlem sırasında). Bu kullanıcılar hizmet kaybı veya bazı durumlarda sonuçlanabilir hello işlemi sırasında veri kaybı kaldırılan lisanslarını sahip olacaktır.

> Lisans atama için bağımlı büyük dinamik bir grup varsa, daha küçük bir test grubu üzerinde önemli değişikliklere toohello ana grup uygulamadan önce doğrulama göz önünde bulundurun.

## <a name="multiple-groups-and-multiple-licenses"></a>Birden çok grubu ve birden çok lisans

Bir kullanıcı lisansları sahip birden fazla grup üyesi olabilir. Bazı şeyleri tooconsider şunlardır:

- Aynı ürün binebilir hello ve yol için birden çok lisans tüm uygulanan toohello kullanıcı olan hizmetler etkinleştirilmiş. Merhaba aşağıdaki örnekte iki lisans gruplarını gösterir: *E3 temel Hizmetleri* hello foundation Hizmetleri toodeploy ilk tooall kullanıcıları içerir. Ve *Hizmetleri genişletilmiş E3* ek hizmetler (Sway ve Planlayıcısı) toodeploy yalnızca toosome kullanıcıları içerir. Bu örnekte, hello kullanıcı tooboth grupları eklendi:

  ![Etkin hizmetleri ekran görüntüsü](media/active-directory-licensing-group-advanced/view-enabled-services.png)

  Sonuç olarak, hello kullanıcı 7 hello 12 hizmetlerinin etkin, bu ürün için yalnızca bir lisans kullanırken hello ürün sahiptir.

- Seçme hello *E3* lisans grupları hakkında hello kullanıcı için etkinleştirilip hangi Hizmetleri toobe neden bilgi dahil daha fazla ayrıntı gösterir.

  ![Grup tarafından etkinleştirilmiş hizmetler ekran görüntüsü](media/active-directory-licensing-group-advanced/view-enabled-service-by-group.png)

## <a name="direct-licenses-coexist-with-group-licenses"></a>Grup lisans doğrudan lisansları bir arada var

Bir kullanıcı bir lisans bir gruptan devralır olduğunda, doğrudan kaldıramaz veya hello kullanıcının özelliklerini bu lisans atamasını değiştirmek. Değişiklikler hello grubunda yapılmalıdır ve tooall kullanıcılar yayılır.

Mümkündür, ancak tooassign hello aynı Ürün lisans lisans toohello kullanıcı, toplama toohello devralınan doğrudan. Diğer kullanıcıları etkilemeden hello üründen ek hizmetler yalnızca bir kullanıcı için etkinleştirebilirsiniz.

Atanan lisansları kaldırılabilir ve etkilemeyen doğrudan lisansları devralınmış. Bir gruptan bir Office 365 Kurumsal E3 lisans devralır hello kullanıcının göz önünde bulundurun.

1. Başlangıçta, hello kullanıcı hello lisans yalnızca hello devralır *E3 temel Hizmetleri* gösterildiği gibi dört hizmet planları sağlayan Grup:

  ![Ekran görüntüsü, E3 etkin bir grup Hizmetleri](media/active-directory-licensing-group-advanced/e3-group-enabled-services.png)

2. Seçebileceğiniz **atamak** toodirectly E3 lisans toohello kullanıcı atayın. Bu durumda, Yammer kuruluş tüm hizmet planları toodisable kalacaklarını:

  ![Ekran görüntüsü nasıl tooassign bir lisans doğrudan tooa kullanıcı](media/active-directory-licensing-group-advanced/assign-license-to-user.png)

3. Sonuç olarak, hello kullanıcı hala hello E3 ürünün yalnızca bir lisans kullanır. Ancak hello yalnızca o kullanıcı için Yammer Kurumsal hizmeti hello doğrudan atanmasını sağlar. Hangi hizmetlerin hello grup üyeliği hello doğrudan atama karşı tarafından etkinleştirilen görebilirsiniz:

  ![Ekran görüntüsü karşı doğrudan atanmasına devralınan](media/active-directory-licensing-group-advanced/direct-vs-inherited-assignment.png)

4. Doğrudan atanmasına kullandığınızda, aşağıdaki işlemleri hello izin verilir:

  - Yammer Kurumsal hello kullanıcı nesnesi üzerinde doğrudan kapatılabilir. Merhaba **açık/kapalı** geçiş hello çizimde, bu hizmet için karşılıklı toohello diğer etkinleştirildiğini hizmet değiştirir. Merhaba hizmeti doğrudan hello kullanıcı etkinleştirilmiş olduğu için değiştirilebilir.
  - Ek hizmetler de hello doğrudan lisans atanmış bir parçası olarak etkinleştirilebilir.
  - Merhaba **kaldırmak** düğmesi kullanılan tooremove hello doğrudan lisans hello kullanıcıdan olabilir. Merhaba kullanıcı artık yalnızca hello devralınan Grup lisans sahiptir ve yalnızca hello özgün Hizmetleri etkin kalmaya devam görebilirsiniz:

    ![Nasıl tooremove doğrudan atama gösteren ekran görüntüsü](media/active-directory-licensing-group-advanced/remove-direct-license.png)

## <a name="managing-new-services-added-tooproducts"></a>Tooproducts eklenen yeni hizmetlerini yönetme
Microsoft yeni bir hizmet tooa ürün eklediğinde, varsayılan olarak tüm grupları toowhich atamış etkinleştirilecek hello Ürün lisans. Ürün değişiklikler hakkında abone toonotifications olan kullanıcılar kiracınızda hello yaklaşan hizmet eklemeleri hakkında bilgilendirmek önceden e-postaları alır.

Yönetici olarak hello değişiklikten etkilenen tüm grupları gözden geçirin ve hello yeni hizmet her grubunda devre dışı bırakma gibi eylemi gerçekleştirin. Örneğin, yalnızca belirli hizmetleri dağıtımı için hedef grupları oluşturduysanız, bu grupları yeniden ziyaret ve eklenmiş herhangi bir yeni hizmetlerin devre dışı olduğundan emin olun.

Bu işlem neye benzediğini örneği şöyledir:

1. İlk olarak, hello atanan *Office 365 Kurumsal E5* ürün tooseveral grupları. Adlı bu gruplara birini *O365 E5 - yalnızca Exchange* tasarlanmış tooenable yalnızca hello edildi *Exchange Online (2 planlama)* üyeleri için hizmet.

2. Ürün ile yeni bir hizmet - genişletilmiş E5 hello Microsoft'tan bir bildirim alındı *Microsoft Stream*. Merhaba hizmet kiracınızda kullanılabilir hale geldiğinde yapabileceğiniz hello aşağıdaki:

3. Toohello Git [ **Azure Active Directory > lisansları > tüm ürünleri** ](https://portal.azure.com/#blade/Microsoft_AAD_IAM/LicensesMenuBlade/Products) dikey penceresinde ve select *Office 365 Kurumsal E5*seçeneğini belirleyip **lisans grupları**  tooview Bu ürünle birlikte tüm grupları listesi.

4. Tıklatın tooreview istediğiniz hello grubunda (Bu durumda, *O365 E5 - yalnızca Exchange*). Bu hello açar **lisansları** sekmesi. Merhaba E5 lisansı tıklandığında, tüm etkin hizmetleri listeleme bir dikey pencere açılır.
> [!NOTE]
> Merhaba *Microsoft Stream* hizmet olduğundan otomatik olarak eklenir ve bu gruba eklenmesini toohello etkin *Exchange Online* hizmeti:

  ![Yeni hizmet ekran tooa Grup lisans eklendi](media/active-directory-licensing-group-advanced/manage-new-services.png)

5. Bu gruptaki toodisable hello yeni hizmet isterseniz, hello tıklatın **açık/kapalı** geçiş sonraki toohello hizmet ve Başlangıç'ı tıklatın **kaydetmek** düğmesini tooconfirm hello değişiklik. Azure AD hello Grup tooapply hello değişikliği tüm kullanıcıların artık işleyecek; tüm yeni kullanıcılar toohello Grup hello sahip olmaz eklenen *Microsoft Stream* hizmetinin etkinleştirilmiş.

  > [!NOTE]
  > Kullanıcılar hala hello hizmetinin bazı diğer lisans atamasını (başka bir grup üyeleri veya doğrudan lisans atamasını oldukları) etkinleştirilmiş olabilir.

6. Gerekirse, bu ürünü olan diğer gruplar için aynı adımları atanan hello gerçekleştirin.

## <a name="use-powershell-toosee-who-has-inherited-and-direct-licenses"></a>Devralınan izinlere sahip PowerShell toosee kullanın ve lisansları doğrudan
Kullanıcıların doğrudan atanmış veya gruptan devralınan bir lisansınız varsa, bir PowerShell komut dosyası toocheck kullanabilirsiniz.

1. Merhaba çalıştırmak `connect-msolservice` cmdlet tooauthenticate ve tooyour Kiracı bağlanın.

2. `Get-MsolAccountSku`kullanılan toodiscover hello Kiracı tüm sağlanan ürün lisansları olabilir.

  ![Merhaba Get-döndürülüp cmdlet'inin ekran görüntüsü](media/active-directory-licensing-group-advanced/get-msolaccountsku-cmdlet.png)

3. Kullanım hello *AccountSkuId* ile ilgilenen hello lisans için değer [bu PowerShell Betiği](./active-directory-licensing-ps-examples.md#check-if-user-license-is-assigned-directly-or-inherited-from-a-group). Bu, bu lisans hello lisans nasıl atanacağını hakkında hello bilgilerle sahip kullanıcıların listesini oluşturur.

## <a name="use-audit-logs-toomonitor-group-based-licensing-activity"></a>Denetim günlükleri toomonitor grup tabanlı lisans etkinliği kullanın

Kullanabileceğiniz [Azure AD denetim günlüklerini](./active-directory-reporting-activity-audit-logs.md#audit-logs) toosee tüm etkinlik ilgili toogroup tabanlı lisans, dahil olmak üzere:
- kimin lisans grupları değişti mi
- Merhaba sistem Grup lisans değişikliği işleme başlatıldığında ve onu bittiğinde
- bir Grup lisans atamasını sonucunda tooa kullanıcı hangi lisans değişiklikler yapıldı.

>[!NOTE]
> Denetim günlüklerini çoğu Kanatlar hello Azure Active Directory bölüm hello portalı içinde kullanılabilir. Filtreler, bunları eriştiğiniz yere bağlı olarak, önceden uygulanan tooonly Göster etkinlik ilgili toohello hello dikey bağlamında olabilir. Beklediğiniz hello sonuçları görmüyorsanız, inceleyin [filtreleme seçeneklerini hello](./active-directory-reporting-activity-audit-logs.md#filtering-audit-logs) veya filtrelenmemiş hello denetim günlüklerini altında erişim [ **Azure Active Directory > etkinlik > Denetim günlüklerini** ](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Audit).

### <a name="find-out-who-modified-a-group-license"></a>Kimin bir Grup lisans değiştiren çıkışı Bul

1. Set hello **etkinlik** çok filtre*kümesi Grup lisans* tıklatıp **Uygula**.
2. Merhaba sonuçları lisanslarını ayarlayın veya gruplarında değiştiren tüm örneklerini içerir.
>[!TIP]
> Merhaba grubunun hello adı hello yazabilirsiniz *hedef* tooscope hello sonuçlarını filtreleme.

3. Nelerin değiştiğini, hello liste görünümü toosee hello ayrıntılarını bir öğeyi tıklatın. Altında *değiştirilmiş Özellikler* hello lisans atamasını hem eski hem de yeni değerleri listelenir.

Ayrıntılarla son Grup lisans değişiklikleri bir örneği burada verilmiştir:

![Ekran Grup lisans değişiklikleri](media/active-directory-licensing-group-advanced/audit-group-license-change.png)

### <a name="find-out-when-group-changes-started-and-finished-processing"></a>Grup değişikliklerini başlatıldığında ve işleme tamamlandı öğrenin

Bir lisans grubu üzerinde değiştiğinde, Azure AD hello değişiklikleri tooall kullanıcılar uygulama başlar.

1. grupları işlemi başlatıldığında toosee ayarlamak hello **etkinlik** çok filtre*göre grubundaki lisans toousers uygulama Başlat*. Hello işlemi için bu hello aktör Not *Microsoft Azure AD grup tabanlı lisans* -bir sistem hesabı tüm Grup lisans değişiklikleri kullanılan tooexecute değil.
>[!TIP]
> Merhaba listesi toosee hello bir öğeyi tıklatın *değiştirilmiş Özellikler* alan - işleme için çekilen hello lisans değişiklikleri gösterir. Bu, birden çok değişiklikleri tooa grubu yapılan ve hangisinin işlenmiş emin değilseniz kullanışlıdır.

2. Benzer şekilde, işleme, kullanım hello filtre değeri grupları bitirdikten sonra toosee *göre grubundaki lisans toousers uygulama son*.
>[!TIP]
> Bu durumda, hello *değiştirilmiş Özellikler* alan içerir hello sonuçlarının özetini - işleme hatalarını oluştuysa bu yararlı tooquickly denetleyin. Örnek çıktı:
> ```
Modified Properties
...
Name : Result
Old Value : []
New Value : [Users successfully assigned licenses: 6, Users for whom license assignment failed: 0.];
> ```

3. nasıl bir grubu, tüm kullanıcı değişiklikleri de dahil olmak üzere işlenmiş toosee hello tam günlük filtreleri aşağıdaki hello ayarlayın:
  - **(Aktör) tarafından başlatılan**: "Microsoft Azure AD grup tabanlı lisans"
  - **Tarih aralığı** (isteğe bağlı): belirli bir grup bildiğinizde için özel aralık başlatıldı ve işleme tamamlandı

Bu örnek çıktı kullanıcı değişiklikleri ve hello işlenmesini son işlem, tüm sonuç hello başlangıcını gösterir.

![Ekran Grup lisans değişiklikleri](media/active-directory-licensing-group-advanced/audit-group-processing-log.png)

>[!TIP]
> Çok ilgili öğeleri tıklatarak*değişiklik kullanıcı lisansı* lisans uygulanan değişiklikler tooeach tek tek kullanıcı için Ayrıntılar gösterilir.

## <a name="limitations-and-known-issues"></a>Sınırlamalar ve bilinen sorunlar

Grup tabanlı Lisansı'nı kullanın, bu iyi bir fikir toofamiliarize kendiniz sınırlamalar ve bilinen sorunlar listesi aşağıdaki hello ile olur.

- Grup tabanlı şu anda lisans diğer gruplar (iç içe geçmiş gruplar) içeren grupları desteklemez. Bir lisans tooa iç içe geçmiş Grup uygularsanız, yalnızca hello hemen birinci düzey kullanıcı grubunun üyeleri, hello uygulanan hello lisansınız yok.

- Merhaba özelliği yalnızca güvenlik grupları ile kullanılabilir. Office grupları şu anda desteklenmez ve mümkün toouse olmaz hello lisans atama işleminin bunları.

- Merhaba [Office 365 Yönetici portalı](https://portal.office.com ) grup tabanlı lisans şu anda desteklemiyor. Bir kullanıcı bir lisans bir gruptan devralır. Bu lisans normal kullanıcı lisansı hello Office Yönetim Portalı'nda görüntülenir. Lisans ya da tooremove hello lisans deneyin toomodify çalışırsanız, hello portalı bir hata iletisi döndürür. Devralınan Grup lisansları doğrudan bir kullanıcı olarak değiştirilemez.

- Bir kullanıcı bir gruptan kaldırılır ve hello lisans kaybederse, (örneğin, SharePoint Online) lisans hello hizmet planlarından tooa ayarlanan **askıya** durumu. Merhaba hizmet planları ayarlanmaz tooa son, durumu devre dışı. Bir yönetim grubu üyeliği Yönetimi'nde bir hata yaparsa bu önlem, kullanıcı verilerinin yanlışlıkla kaldırma önleyebilirsiniz.

- Lisansları atanmış veya büyük bir grup için (örneğin, 100.000 kullanıcı) değiştiren performansını etkileyebilir. Özellikle, Azure AD Otomasyon tarafından üretilen değişikliklerin hello hacmi, Azure AD arasında dizin eşitlemesi hello performansını olumsuz etkileyebilir ve şirket içi sistemler.

- Lisans Yönetimi Otomasyonu hello ortamında değişiklik tooall türlerini otomatik olarak tepki vermez. Örneğin, lisansları dışında bazı kullanıcılar toobe bir hata durumunda çalıştırarak. toofree hello kullanılabilir lisans sayısı yukarı diğer kullanıcıların bazı doğrudan atanan lisansları kaldırabilirsiniz. Ancak, hello sistem otomatik olarak toothis değişiklik tepki ve kullanıcılara, hata durumunda düzeltin.

  Sınırlamaları, bir geçici çözüm toothese türleri olarak toohello gidebilirsiniz **grup** dikey Azure AD'de tıklatıp **yeniden işleyin**. Bu komut, o gruptaki tüm kullanıcılar işler ve hello hata durumları, mümkünse giderir.

- Bir lisans tooa kullanıcı tooa yinelenen proxy adresi yapılandırma Exchange Online'da son atanamadı olduğunda grup tabanlı lisans hataları kaydetmez; Bu tür kullanıcıların Lisans atama sırasında atlanır. Hakkında daha fazla bilgi için tooidentify ve bu sorunu çözmek için bkz: [Bu bölümde](./active-directory-licensing-group-problem-resolution-azure-portal.md#license-assignment-fails-silently-for-a-user-due-to-duplicate-proxy-addresses-in-exchange-online).

## <a name="next-steps"></a>Sonraki adımlar

Grup tabanlı lisans aracılığıyla lisans yönetimi için diğer senaryolar hakkında daha fazla toolearn bakın:

* [Grup tabanlı Azure Active Directory lisanslaması nedir?](active-directory-licensing-whatis-azure-portal.md)
* [Azure Active Directory'de lisansları tooa grup atama](active-directory-licensing-group-assignment-azure-portal.md)
* [Azure Active Directory'deki bir gruba lisans sorunlarını tanımlama ve](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [Toomigrate tek tek kullanıcılar toogroup tabanlı Azure Active Directory'de lisanslama nasıl lisanslı](active-directory-licensing-group-migration-azure-portal.md)
