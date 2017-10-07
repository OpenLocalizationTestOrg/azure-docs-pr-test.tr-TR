---
title: "Azure AD Connect eşitleme: bir yapılandırma değişikliği Azure AD Connect eşitleme yaptığınızda | Microsoft Docs"
description: "Toomake toohello yapılandırmasını değiştirme Azure AD CONNECT'te nasıl eşitleme aracılığıyla anlatılmaktadır."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 7b9df836-e8a5-4228-97da-2faec9238b31
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 78e96d9166831a668439c2b8aa6a0022bc472da4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-how-toomake-a-change-toohello-default-configuration"></a>Azure AD Connect eşitleme: nasıl toomake değişiklik toohello varsayılan yapılandırması
Bu konuda Hello amacı toowalk size nasıl toomake Azure AD Connect eşitleme toohello Varsayılan yapılandırmada değiştirir. Bu, bazı ortak senaryolar için adımları sağlar. Bu bilgiyle, bazı basit değişiklikler tooyour kendi kendi iş kurallarına göre yapılandırma mümkün toomake olmalıdır.

## <a name="synchronization-rules-editor"></a>Eşitleme kuralları Düzenleyicisi
Merhaba eşitleme kuralları Düzenleyicisi kullanılan toosee ve değişiklik hello varsayılan yapılandırmadır. Merhaba Başlat menüsü hello altında bulabilirsiniz **Azure AD Connect** grubu.  
![Başlat menüsü ile eşitleme kural Düzenleyicisi](./media/active-directory-aadconnectsync-change-the-configuration/startmenu2.png)

Açtığınızda, hello varsayılan out-of-box kuralları bakın.

![Eşitleme kuralı Düzenleyicisi](./media/active-directory-aadconnectsync-change-the-configuration/sre2.png)

### <a name="navigating-in-hello-editor"></a>Merhaba Düzenleyicisi'nde gezinme
Merhaba aşağı açılan listeler hello Düzenleyicisi hello üstündeki tooquickly Bul belirli bir kural izin verin. Örneğin, hello özniteliği proxyAddresses dahil olduğu toosee hello kuralları istiyorsanız hello aşağı açılan listeler toohello aşağıdakileri değiştirin:  
![SRE filtreleme](./media/active-directory-aadconnectsync-change-the-configuration/filtering.png)  
tooreset filtreleme ve yük yeni bir yapılandırma basın **F5** hello klavyede.

sağ toohello üst, bir düğmeye sahip **Yeni Kural Ekle**. Bu düğme kullanılan toocreate kendi özel kuralıdır.

Merhaba altındaki bir seçili eşitleme kuralı hareket düğmelerini sahip. **Düzen** ve **silmek** onlara beklediğiniz yapın. **Dışarı aktarma** hello eşitleme kuralı yeniden oluşturmak için bir PowerShell Betiği oluşturur. Bu yordam toomove bir sunucu tooanother eşitleme kuraldan verir.

## <a name="create-your-first-custom-rule"></a>İlk, özel bir kural oluşturun
Merhaba en yaygın değişiklikler toohello öznitelik akışları değişikliktir. Merhaba veri kaynağı dizininizde Azure AD olduğu gibi olmayabilir. Bu bölümdeki Hello örnekte toomake hello verilen ad, bir kullanıcının her zaman içinde olmasını istediğiniz **uygun durumda**.

### <a name="disable-hello-scheduler"></a>Merhaba Zamanlayıcısı'nı devre dışı bırak
Merhaba [Zamanlayıcı](active-directory-aadconnectsync-feature-scheduler.md) varsayılan olarak 30 dakikada bir çalışır. Değişiklik yapmadan ve yeni kurallarınızı sorun giderme, başlangıç değil emin toomake istiyor. tootemporarily hello Zamanlayıcısı'nı devre dışı bırakmak, PowerShell'i başlatın ve çalıştırın`Set-ADSyncScheduler -SyncCycleEnabled $false`

![Merhaba Zamanlayıcısı'nı devre dışı bırak](./media/active-directory-aadconnectsync-change-the-configuration/schedulerdisable.png)  

### <a name="create-hello-rule"></a>Merhaba kuralı oluşturma
1. Tıklatın **Yeni Kural Ekle**.
2. Merhaba üzerinde **açıklama** sayfa hello aşağıdakileri girin:  
   ![Filtreleme kuralını gelen](./media/active-directory-aadconnectsync-change-the-configuration/description2.png)  
   * Ad: hello kural açıklayıcı bir ad verin.
   * Açıklama: birisi hangi hello kural anlamaları için bazı açıklama içindir.
   * Bağlı sistem: hello sistem hello nesnesi bulunabilir. Bu durumda, hello Active Directory bağlayıcısını seçin.
   * Bağlı sistem/meta veri deposu nesne türü: Seçin **kullanıcı** ve **kişi** sırasıyla.
   * Bağlantı türü: Bu değeri çok değiştirmek**katılma**.
   * Öncelik: hello sistemde benzersiz olan bir değer sağlayın. Daha yüksek önceliği daha düşük bir sayısal değer belirtir.
   * Etiket: boş bırakın. Yalnızca out-of-box kuralları Microsoft'tan bir değerle doldurulmuş bu kutu olması gerekir.
3. Merhaba üzerinde **Scoping filtre** want **givenName ISNOTNULL**.  
   ![Gelen kuralı kapsamı filtresi](./media/active-directory-aadconnectsync-change-the-configuration/scopingfilter.png)  
   Bu bölüm, hangi nesnelerin hello kuralın geçerli olacağı kullanılan toodefine değildir. Boş bırakılırsa, hello kural tooall kullanıcı nesnelerinin geçerli olur. Ancak, konferans odaları, hizmet hesapları ve diğer kişiler olmayan kullanıcı nesneleri içerir.
4. Merhaba üzerinde **katılma kuralları**, bu alanı boş bırakın.
5. Merhaba üzerinde **dönüşümleri** sayfasında, hello FlowType çok değiştirme**ifade**. Select hello Target özniteliği **givenName**ve kaynağında girin `PCase([givenName])`.
   ![Gelen kuralı dönüşümleri](./media/active-directory-aadconnectsync-change-the-configuration/transformations.png)  
   Merhaba eşitleme altyapısı, hem de hello işlev adı ve hello hello özniteliğin adını duyarlıdır. Bir sorun yazarsanız, hello kural eklediğinizde, bir uyarı görürsünüz. Merhaba Düzenleyicisi toosave sağlar ve tooreopen hello kuralı ve doğru hello kuralı olması gereken şekilde, devam edin.
6. Tıklatın **Ekle** toosave hello kuralı.

Yeni özel kuralın hello ile diğer görünmesi gereken hello sistemde eşitleme kuralları.

### <a name="verify-hello-change"></a>Merhaba değişikliği doğrulayın
Bu yeni değişiklikle toomake hataları atma değil ve beklendiği gibi çalıştığından emin istiyor. Sahip olduğunuz nesneleri Hello sayısına bağlı olarak, bu adımı iki farklı şekilde toodo vardır.

1. Tüm nesneler üzerinde tam bir eşitleme çalıştırın
2. Tek bir nesne üzerinde bir önizleme ve tam eşitleme çalıştırma

Başlat **eşitleme hizmeti** hello Başlat menüsünden. Merhaba Bu bölümde bu araç tüm adımlardır.

1. **Tüm nesneler üzerinde tam eşitleme**  
   Seçin **Bağlayıcılar** hello üstünde. Merhaba, bir değişiklik tooin hello önceki bölümde yaptığınız bağlayıcı tanımlamak, bu durumda Active Directory etki alanı Hizmetleri hello ve seçin. Seçin **çalıştırmak** Eylemler ve select **tam eşitleme** ve **Tamam**.
   ![Tam eşitleme](./media/active-directory-aadconnectsync-change-the-configuration/fullsync.png)  
   Merhaba nesneler artık hello meta veri deposunda güncelleştirilir. Şimdi toolook hello nesnede hello meta dizesinde istiyorsunuz.
2. **Önizleme ve tek bir nesne üzerinde tam eşitleme**  
   Seçin **Bağlayıcılar** hello üstünde. Merhaba, bir değişiklik tooin hello önceki bölümde yaptığınız bağlayıcı tanımlamak, bu durumda Active Directory etki alanı Hizmetleri hello ve seçin. Seçin **bağlayıcı alanı arama**. Kapsam toofind toouse tootest hello değiştirmek istediğiniz bir nesne kullanın. Merhaba nesnesi seçin ve tıklatın **Önizleme**. Merhaba yeni ekranında şunları seçin **Commit Önizleme**.  
   ![Önizleme Yürüt](./media/active-directory-aadconnectsync-change-the-configuration/commitpreview.png)  
   Merhaba değişiklik taahhüt toohello meta veri deposu sunulmuştur.

**Merhaba meta veri deposu hello nesnesinde bakın**  
Şimdi birkaç örnek nesneleri toomake emin hello değer beklenen toopick ve o hello kural istiyorsunuz. Seçin **meta veri deposu arama** hello üstten. Toofind hello ilgili nesneleri gereken herhangi bir filtre ekleyin. Merhaba Arama sonuçlarından nesneyi açın. Merhaba öznitelik değerleri arayın ve ayrıca hello doğrulayın **eşitleme kuralları** beklendiği gibi kural hello sütun.  
![Meta veri deposu arama](./media/active-directory-aadconnectsync-change-the-configuration/mvsearch.png)  

### <a name="enable-hello-scheduler"></a>Merhaba Zamanlayıcısını Etkinleştir
Her şeyin beklendiği gibi ise, hello Zamanlayıcı yeniden etkinleştirebilirsiniz. PowerShell çalıştırmak `Set-ADSyncScheduler -SyncCycleEnabled $true`.

## <a name="other-common-attribute-flow-changes"></a>Diğer ortak öznitelik akışı değişiklikleri
toomake tooan öznitelik akışı nasıl değiştiğini Hello önceki bölümde açıklanan. Bu bölümde, bazı ek örnekler verilmiştir. toocreate hello eşitleme kuralı nasıl kısaltılmıştır Merhaba adımları, ancak hello tam adımlar hello önceki bölümünde bulabilirsiniz.

### <a name="use-another-attribute-than-hello-default"></a>Başka bir öznitelik hello varsayılan kullanın
Fabrikam'daki, hello yerel alfabe verilen ad, Soyadı ve görünen ad için kullanıldığı bir orman yoktur. Merhaba bu öznitelikler Latin karakterlerini gösterimini hello uzantı öznitelikleri bulunabilir. Azure AD'de Hello genel adres listesi oluşturulurken ve Office 365 hello kuruluşunuzda kullanılan bunun yerine bu öznitelikler toobe.

Varsayılan yapılandırma ile bir nesne hello yerel ormandaki şöyle görünür:  
![Öznitelik akışı 1](./media/active-directory-aadconnectsync-change-the-configuration/attributeflowjp1.png)

toocreate diğer öznitelik akışları sahip bir kural hello aşağıdaki:

* Başlat **Synchronization Rule Editor** hello Başlat menüsünden.
* İle **gelen** hala seçili toohello sol, hello düğmesini **Yeni Kural Ekle**.
* Merhaba kuralı, bir ad ve açıklama verin. Merhaba şirket içi Active Directory ve hello ilgili nesne türlerini seçin. İçinde **bağlantı türü**seçin **katılma**. Öncelik, başka bir kural tarafından kullanılmayan bir sayı seçin. Bu örnekte Hello değeri 50 kullanılabilmesi için hello out-of-box kuralları 100 ile başlatın.
  ![Öznitelik akışı 2](./media/active-directory-aadconnectsync-change-the-configuration/attributeflowjp2.png)
* Kapsam boş bırakın getirin (diğer bir deyişle, hello ormanındaki tooall kullanıcı nesnelerinin geçerli).
* (Out-of-box kural tanıtıcı birleşimlerin hello izin veren olan) katılma kurallarını boş bırakın.
* Dönüşümleri, akışları aşağıdaki hello oluşturun:  
  ![Öznitelik akışı 3](./media/active-directory-aadconnectsync-change-the-configuration/attributeflowjp3.png)
* Tıklatın **Ekle** toosave hello kuralı.
* Çok Git**Eşitleme Hizmeti Yöneticisi'ni**. Üzerinde **Bağlayıcılar**, select hello hello kural eklediğimiz burada bağlayıcı. Seçin **çalıştırmak**, ve **tam eşitleme**. Tam eşitleme hello geçerli kurallarını kullanarak tüm nesneleri yeniden hesaplar.

Bu özel bu kuralla aynı nesne hello hello sonucu.  
![Öznitelik akışı 4](./media/active-directory-aadconnectsync-change-the-configuration/attributeflowjp4.png)

### <a name="length-of-attributes"></a>Öznitelikleri uzunluğu
Dize özniteliklerin varsayılan kümesi toobe tarafından dizine ve hello en fazla 448 karakter uzunluğundadır. Daha fazla bilgi içerebilir dizesi öznitelikleri ile çalışıyorsanız, emin tooinclude hello aşağıdaki hello öznitelik akışı olun:  
`attributeName` <- `Left([attributeName],448)`

### <a name="changing-hello-userprincipalsuffix"></a>Merhaba userPrincipalSuffix değiştirme
Merhaba userPrincipalName özniteliği Active Directory'de her zaman hello kullanıcılar tarafından bilinmiyor ve oturum açma kimliği hello gibi uygun olmayabilir. Hello Azure AD Connect eşitleme Yükleme Sihirbazı'nı farklı bir öznitelik çekme sağlar örneğin posta. Ancak bazı durumlarda hello özniteliği hesaplanması gerekir. Örneğin, iki Azure AD dizini, bir üretim için ve test etmek için bir hello şirket Contoso sahiptir. Kiracı toouse hello oturum açma kimliği başka bir soneki hello kullanıcılar kendi test istedikleri  
`userPrincipalName` <- `Word([userPrincipalName],1,"@") & "@contosotest.com"`

Bu ifadede, her şeyi sol Merhaba ilk Al @-sign (Word) ve sabit bir dize ile Birleştir.

### <a name="convert-a-multi-value-tooa-single-value"></a>Bir çoklu değer tooa tek değerli Dönüştür
Active Directory Kullanıcıları ve Bilgisayarları'nda değerli tek Ara olsa bile Active Directory'de bazı öznitelikler hello şemada birden çok değerli. Merhaba Açıklama özniteliği örneğidir.  
`description` <- `IIF(IsNullOrEmpty([description]),NULL,Left(Trim(Item([description],1)),448))`

Bu ifade hello özniteliği hello özniteliğinde hello ilk öğe (öğe) ele bir değere sahip durumda kaldırın baştaki ve sondaki boşlukları (kırpma) ve ardından canlı hello hello dizedeki ilk 448 karakter (soldaki).

### <a name="do-not-flow-an-attribute"></a>Bir öznitelik akışı değil
Merhaba senaryo Bu bölüm için arka plan için bkz: [kontrol hello öznitelik akış süreci](active-directory-aadconnectsync-understanding-declarative-provisioning.md#control-the-attribute-flow-process).

Toonot bir öznitelik akışı iki yolu vardır. Merhaba ilk hello Yükleme Sihirbazı'nda kullanılabilir ve çok verir[seçili öznitelikleri kaldırmak](active-directory-aadconnect-get-started-custom.md#azure-ad-app-and-attribute-filtering). Merhaba özniteliği önce hiçbir zaman uyumlu yaptıysanız bu seçenek çalışır. Ancak, toosynchronize bu öznitelik başlamış olması ve daha sonra bu özelliğiyle çıkarırsanız, ardından hello eşitleme altyapısı hello özniteliği yönetme durdurur ve hello varolan değerleri Azure AD içinde kalır.

Tooremove hello özniteliğin değerini istediğiniz ve hello gelecekteki akış değil emin olun, bunun yerine özel bir kural oluşturun.

Fabrikam'daki, biz biz toohello eşitleme öznitelikleri bulut hello bazıları var olmamalıdır, gerçekleştirilmiş. Bu öznitelikler Azure AD'den kaldırılır emin toomake istiyoruz.  
![Hatalı uzantı öznitelikleri](./media/active-directory-aadconnectsync-change-the-configuration/badextensionattribute.png)

* Yeni bir gelen eşitleme kuralı oluşturmak ve hello açıklama doldurmak ![açıklamaları](./media/active-directory-aadconnectsync-change-the-configuration/syncruledescription.png)
* Öznitelik akışları türü oluşturma **ifade** ve hello kaynağıyla **AuthoritativeNull**. değişmez değer Hello **AuthoritativeNull** toopopulate hello değerini daha düşük bir öncelik eşitleme kuralı çalıştığında olsa bile hello değeri hello MV boş olması gerektiğini gösterir.
  ![Uzantı öznitelikleri dönüşümü](./media/active-directory-aadconnectsync-change-the-configuration/syncruletransformations.png)
* Merhaba eşitleme kuralı kaydedin. Başlat **eşitleme hizmeti**, hello bağlayıcı bulmak, seçmek **çalıştırmak**, ve **tam eşitleme**. Bu adım, tüm öznitelik akışları yeniden hesaplar.
* Bu hello değişiklikleri hello bağlayıcı alanı arama yaparak dışarı toobe hakkında yöneliktir doğrulayın.
  ![Hazırlanan Sil](./media/active-directory-aadconnectsync-change-the-configuration/deletetobeexported.png)

## <a name="create-rules-with-powershell"></a>PowerShell ile kuralları oluşturma
Yalnızca birkaç değişiklik toomake sahip olduğunuzda hello eşitleme kuralı Düzenleyicisi'ni kullanarak düzgün çalışır. Birden çok değişikliği toomake gerekiyorsa, PowerShell daha iyi bir seçenek olabilir. Gelişmiş özellikler yalnızca PowerShell ile kullanılabilir.

### <a name="get-hello-powershell-script-for-an-out-of-box-rule"></a>Merhaba PowerShell komut dosyası için bir out-of-box kuralını Al
toosee hello out-of-box kural, select hello kural hello eşitleme oluşturulan PowerShell komut dosyası kuralları Düzenleyicisi ve tıklatın **verme**. PowerShell hello bu eylemi sağlar, oluşturulan hello kural komut dosyası.

### <a name="advanced-precedence"></a>Gelişmiş önceliği
Merhaba out-of-box eşitleme kuralları öncelik değeri 100 ile başlatın. Birçok ormanlar varsa ve toomake gereken birçok özel değişiklikler sonra 99 eşitleme kuralları yeterli olmayabilir.

Merhaba hello out-of-box kurallardan önce eklenen ek kurallar istediğiniz eşitleme altyapısı söyleyebilirsiniz. tooget Bu davranış, şu adımları izleyin:

1. İşareti hello ilk out-of-box eşitleme kuralı (Merhaba bu kuralıdır **içinde AD kullanıcı katılma gelen**) hello eşitleme kuralı Düzenleyicisi'ni seçip **verme**. Merhaba SR tanımlayıcı değeri kopyalayın.  
![PowerShell değişikliği öncesinde](./media/active-directory-aadconnectsync-change-the-configuration/powershell1.png)  
2. Merhaba yeni eşitleme kuralı oluşturun. Merhaba eşitleme kuralı Düzenleyicisi toocreate kullanabilirsiniz. Merhaba kural tooa PowerShell betiğini dışarı aktarın.
3. Merhaba özelliğinde **PrecedenceBefore**, hello out-of-box kuraldan hello tanımlayıcı değeri ekleyin. Set hello **öncelik** çok**0**. Merhaba tanımlayıcı özniteliği benzersiz olduğundan ve başka bir kural adresinden bir GUID yeniden kullanma değil emin olun. Ayrıca bu hello emin olun **ImmutableTag** özelliği ayarlı değil; Bu özellik yalnızca bir out-of-box kuralı için ayarlamanız gerekir. Merhaba PowerShell komut dosyasını kaydedin ve çalıştırın. Merhaba, özel kural hello öncelik değeri 100 atanır ve diğer tüm out-of-box kurallar artırılır sonucudur.  
![Değişiklikten sonra PowerShell](./media/active-directory-aadconnectsync-change-the-configuration/powershell2.png)  

Aynı hello kullanarak birçok özel eşitleme kuralları olabilir **PrecedenceBefore** değer gerektiğinde.


## <a name="enable-synchronization-of-preferreddatalocation"></a>PreferredDataLocation eşitlemeyi etkinleştir
Azure AD Connect destekleyen hello eşitlenmesi **PreferredDataLocation** için öznitelik **kullanıcı** sürüm 1.1.524.0 ve sonra nesneleri. Daha açık belirtmek gerekirse, aşağıdaki değişiklikleri sunulmuştur:

* Merhaba şema hello nesne türünün **kullanıcı** hello Azure AD Bağlayıcısı türü dize olan ve tek değerli tooinclude PreferredDataLocation özniteliği genişletilir.

* Merhaba şema hello nesne türünün **kişi** hello meta veri türü dize olan ve tek değerli tooinclude PreferredDataLocation özniteliği genişletilir.

Şirket içi Active Directory içinde karşılık gelen bir PreferredDataLocation öznitelik olduğundan varsayılan olarak, eşitlemede hello PreferredDataLocation özniteliği etkin değil. Eşitleme el ile etkinleştirmeniz gerekir.

> [!IMPORTANT]
> Şu anda Azure AD hello PreferredDataLocation öznitelikte eşitlenmiş kullanıcı nesneleri hem bulut doğrudan Azure AD PowerShell kullanılarak yapılandırılan kullanıcı nesneleri toobe sağlar. Merhaba PreferredDataLocation öznitelik eşitlemesi etkinleştirildiğinde, Azure AD PowerShell tooconfigure hello özniteliğini kullanarak durdurmalısınız **kullanıcı nesneleri eşitlenen** Azure AD Connect bunları göre geçersiz kılar Şirket içi Active Directory'de Hello kaynak öznitelik değerleri.

> [!IMPORTANT]
> 1 Eylül 2017 üzerinde Azure AD artık hello PreferredDataLocation özniteliği üzerinde sağlayacak **kullanıcı nesneleri eşitlenen** toobe doğrudan Azure AD PowerShell kullanılarak yapılandırılmış. Kullanıcı nesneleri tooconfigure PreferredLocation öznitelikte eşitlenen, yalnızca Azure AD Connect kullanmanız gerekir.

Eşitleme hello PreferredDataLocation özniteliğinin etkinleştirmeden önce aşağıdakileri yapmalısınız:

 * İlk olarak, hello kaynak özniteliği kullanılan hangi şirket içi Active Directory öznitelik toobe karar verin. Türünde olmalı **dize** ve **tek değerli**.

 * Daha önce hello PreferredDataLocation özniteliği üzerinde yapılandırdıysanız Azure AD PowerShell kullanarak Azure AD içinde eşzamanlı kullanıcı nesneleri varolan, gerekir **backport** hello öznitelik değerleri toohello karşılık gelen kullanıcı nesneleri Şirket içi Active Directory'de.
 
    > [!IMPORTANT]
    > Değil backport hello öznitelik değerleri toohello ilgili kullanıcı şirket içi Active Directory içindeki nesneleri bunu yaparsanız, Azure AD Connect eşitleme hello PreferredDataLocation özniteliği için olduğunda Azure AD'de hello varolan öznitelik değerlerini kaldırın etkin.

 * Merhaba kaynak özniteliği yapılandırmanız önerilir daha sonra doğrulama için kullanılabilecek artık, şirket içi en az bir birkaç AD kullanıcı nesneleri.
 
Merhaba adımları tooenable eşitleme hello PreferredDataLocation özniteliğinin olarak özetlenebilir:

1. Eşitleme Zamanlayıcı'yı devre dışı bırakın ve devam eden bir eşitleme doğrulayın

2. Merhaba kaynak özniteliği toohello şirket içi AD Bağlayıcısı eklemek şeması

3. PreferredDataLocation toohello Azure AD Bağlayıcısı şema ekleyin

4. Şirket içi Active Directory'den gelen eşitleme kuralı tooflow hello öznitelik değeri oluşturun

5. Bir giden eşitleme kuralı tooflow hello öznitelik değeri tooAzure AD oluşturma

6. Tam eşitleme döngüsü çalıştırın

7. Eşitleme Zamanlayıcı etkinleştir

> [!NOTE]
> Bu bölümde Hello kalan adımları ayrıntıları ele alınmaktadır. Özel eşitleme kuralları olmadan tek orman topolojisi ile Azure AD dağıtımının hello bağlamda açıklanmıştır. Çoklu orman topolojisini varsa, özel eşitleme kuralları yapılandırılmış veya bir hazırlama sunucusunda, buna göre tooadjust hello adımları gerekir.

### <a name="step-1-disable-sync-scheduler-and-verify-there-is-no-synchronization-in-progress"></a>1. adım: Eşitleme Zamanlayıcısı'nı devre dışı bırakın ve devam eden bir eşitleme doğrulayın
Eşitleme güncelleştirme hello ortadaki durumdayken eşitleme kurulur olun kuralları tooavoid istenmeyen değişiklikler olma tooAzure AD dışarı. toodisable hello yerleşik eşitleme Zamanlayıcı:

 1. Hello Azure AD Connect sunucusunda PowerShell oturumu başlatın.

 2. Zamanlanan eşitleme cmdlet'ini çalıştırarak devre dışı bırakın:`Set-ADSyncScheduler -SyncCycleEnabled $false`
 
 3. Merhaba Başlat **Eşitleme Hizmeti Yöneticisi'ni** giderek tooSTART → tarafından eşitleme hizmeti.
 
 4. Toohello Git **Operations** sekmesinde ve durumu olan işlem yok onaylayın *"sürüyor."*

![Eşitleme Hizmeti Yöneticisi - devam eden hiçbir işlemleri denetleyin](./media/active-directory-aadconnectsync-change-the-configuration/preferredDataLocation-step1.png)

### <a name="step-2-add-hello-source-attribute-toohello-on-premises-ad-connector-schema"></a>2. adım: hello kaynak özniteliği toohello şirket içi AD Bağlayıcısı ekleme şeması
Tüm AD öznitelikleri içine aktarılır hello şirket içi AD bağlayıcı alanı. tooadd hello kaynak öznitelik toohello listesini hello öznitelikleri alındı:

 1. Toohello Git **Bağlayıcılar** hello Eşitleme Hizmeti Yöneticisi'ni sekmesindedir.
 
 2. Merhaba üzerinde sağ **şirket içi AD Bağlayıcısı** seçip **özellikleri**.
 
 3. Merhaba açılan iletişim kutusunda toohello Git **öznitelikleri Seç** sekmesi.
 
 4. Merhaba kaynak özniteliği hello öznitelik listesinde işaretli olduğundan emin olun.
 
 5. Tıklatın **Tamam** toosave.

![Kaynak özniteliği tooon içi eklemek AD Bağlayıcısı şeması](./media/active-directory-aadconnectsync-change-the-configuration/preferredDataLocation-step2.png)

### <a name="step-3-add-preferreddatalocation-toohello-azure-ad-connector-schema"></a>3. adım: PreferredDataLocation toohello Azure AD Bağlayıcısı şema ekleme
Varsayılan olarak, hello PreferredDataLocation özniteliği hello Azure AD Connect alanı alınan değil. içeri aktarılan özniteliklerin tooadd hello PreferredDataLocation öznitelik toohello listesi:

 1. Toohello Git **Bağlayıcılar** hello Eşitleme Hizmeti Yöneticisi'ni sekmesindedir.

 2. Merhaba üzerinde sağ **Azure AD Bağlayıcısı** seçip **özellikleri**.

 3. Merhaba açılan iletişim kutusunda toohello Git **öznitelikleri Seç** sekmesi.

 4. Merhaba PreferredDataLocation özniteliği hello öznitelik listesinde işaretli olduğundan emin olun.

 5. Tıklatın **Tamam** toosave.

![Kaynak özniteliği tooAzure AD Bağlayıcısı şema ekleyin](./media/active-directory-aadconnectsync-change-the-configuration/preferredDataLocation-step3.png)

### <a name="step-4-create-an-inbound-synchronization-rule-tooflow-hello-attribute-value-from-on-premises-active-directory"></a>4. adım: şirket içi Active Directory'den gelen eşitleme kuralı tooflow hello öznitelik değerini oluşturma
Merhaba gelen eşitleme kuralını hello öznitelik değeri tooflow şirket içi Active Directory toohello meta veri deposu gelen hello kaynak özniteliğinden verir:

1. Merhaba Başlat **eşitleme kuralları Düzenleyicisi** giderek tooSTART → tarafından Düzenleyicisi eşitleme kuralları.

2. Set hello arama filtresi **yönü** toobe **gelen**.

3. Tıklatın **Yeni Kural Ekle** düğmesini toocreate yeni bir gelen kuralı.

4. Merhaba altında **açıklama** sekmesinde, yapılandırma aşağıdaki hello sağlayın:
 
    | Öznitelik | Değer | Ayrıntılar |
    | --- | --- | --- |
    | Ad | *Bir ad sağlayın* | Örneğin, *"içinde AD'den – kullanıcı PreferredDataLocation"* |
    | Açıklama | *Bir açıklama belirtin* |  |
    | Bağlı sistem | *Merhaba şirket içi çekme AD Bağlayıcısı* |  |
    | Bağlı sistem nesne türü | **Kullanıcı** |  |
    | Meta veri deposu nesne türü | **Kişi** |  |
    | Bağlantı türü | **Birleştir** |  |
    | Önceliği | *1-99 arasında bir sayı seçin* | 1-99 özel eşitleme kuralları için ayrılmıştır. Başka bir eşitleme kuralı tarafından kullanılan bir değer seçmesi değil. |

5. Toohello Git **Scoping filtre** sekmesinde ve ekleme bir **yan tümcesi aşağıdaki hello tek kapsam filtresi grubuyla**:
 
    | Öznitelik | işleci | Değer |
    | --- | --- | --- |
    | adminDescription | NOTSTARTWITH | Kullanıcı\_ | 
 
    Kapsam filtresi, bu gelen eşitleme kuralını uygulandığı AD nesnelerini şirket içi belirler. Bu örnekte, aynı kapsam filtre olarak kullanılan hello kullanırız *"içinde AD'den – kullanıcı ortak"* hello eşitleme kuralı engeller OOB eşitleme kuralı uygulanan Azure AD kullanıcı geri yazma oluşturulan tooUser nesneler özelliği. Tootweak hello kapsam filtresi tooyour Azure AD Connect dağıtım göre gerekebilir.

6. Toohello Git **dönüştürme sekmesi** ve dönüştürme kuralı aşağıdaki hello uygulayın:
 
    | Akış türü | Target özniteliği | Kaynak | Bir kez Uygula | Birleştirme türü |
    | --- | --- | --- | --- | --- |
    | Doğrudan | PreferredDataLocation | Merhaba kaynak özniteliği seçin | İşaretli | Güncelleştirme |

7. Tıklatın **Ekle** toocreate hello gelen kuralı.

![Gelen eşitleme kuralı oluşturma](./media/active-directory-aadconnectsync-change-the-configuration/preferredDataLocation-step4.png)

### <a name="step-5-create-an-outbound-synchronization-rule-tooflow-hello-attribute-value-tooazure-ad"></a>5. adım: bir giden eşitleme kuralı tooflow hello öznitelik değeri tooAzure AD oluşturma
Merhaba giden eşitleme kuralını hello öznitelik değeri tooflow hello meta veri deposu toohello PreferredDataLocation özniteliğinden Azure AD'de verir:

1. Toohello Git **eşitleme kuralları** Düzenleyici.

2. Set hello arama filtresi **yönü** toobe **giden**.

3. Tıklatın **Yeni Kural Ekle** düğmesi.

4. Merhaba altında **açıklama** sekmesinde, yapılandırma aşağıdaki hello sağlayın:

    | Öznitelik | Değer | Ayrıntılar |
    | --- | --- | --- |
    | Ad | *Bir ad sağlayın* | Örneğin, "tooAAD Out – kullanıcı PreferredDataLocation" |
    | Açıklama | *Bir açıklama belirtin* |
    | Bağlı sistem | *Merhaba AAD bağlayıcıyı seçin* |
    | Bağlı sistem nesne türü | Kullanıcı ||
    | Meta veri deposu nesne türü | **Kişi** ||
    | Bağlantı türü | **Birleştir** ||
    | Önceliği | *1-99 arasında bir sayı seçin* | 1-99 özel eşitleme kuralları için ayrılmıştır. YDo olmayan başka bir eşitleme kuralı tarafından kullanılan bir değer seçin. |

5. Toohello Git **Scoping filtre** sekmesinde ve ekleme bir **tek bir kapsam filtresi grubunu iki maddeleri**:
 
    | Öznitelik | işleci | Değer |
    | --- | --- | --- |
    | sourceObjectType | EŞİTTİR | Kullanıcı |
    | cloudMastered | EŞİT DEĞİLDİR | True |

    Kapsam Filtresi hangi Azure AD bu giden eşitleme kuralının uygulandığı nesneleri belirler. Merhaba kullandığımız Bu örnekte, "Out tooAD – kullanıcı kimliği" aynı kapsam filtresi OOB eşitleme kuralı. Bunu hello eşitleme kuralı şirket içi Active Directory'den eşitlenmez uygulanan tooUser nesneleri engeller. Tootweak hello kapsam filtresi tooyour Azure AD Connect dağıtım göre gerekebilir.
    
6. Toohello Git **dönüştürme** sekmesinde ve dönüştürme kuralı aşağıdaki hello uygulayın:

    | Akış türü | Target özniteliği | Kaynak | Bir kez Uygula | Birleştirme türü |
    | --- | --- | --- | --- | --- |
    | Doğrudan | PreferredDataLocation | PreferredDataLocation | İşaretli | Güncelleştirme |

7. Kapat **Ekle** toocreate hello giden kuralı.

![Giden eşitleme kuralı oluştur](./media/active-directory-aadconnectsync-change-the-configuration/preferredDataLocation-step5.png)

### <a name="step-6-run-full-synchronization-cycle"></a>6. adım: Çalıştır tam eşitleme döngüsü
Genel olarak, biz eklenen yeni öznitelikler tooboth hello AD ve Azure AD Bağlayıcısı şema ve özel eşitleme kuralları sunulan bu yana tam eşitleme döngüsü gereklidir. Merhaba değişiklikleri tooAzure AD dışarı aktarmadan önce doğrulamanız önerilir. Bir tam eşitleme döngüsü yapmak hello adımları el ile çalışırken aşağıdaki adımları tooverify hello değişiklikler hello kullanabilirsiniz. 

1. Çalıştırma **tam alma** hello adımında **şirket içi AD Bağlayıcısı**:

   1. Toohello Git **Operations** hello Eşitleme Hizmeti Yöneticisi'ni sekmesindedir.

   2. Merhaba üzerinde sağ **şirket içi AD Bağlayıcısı** seçip **Çalıştır...**

   3. Merhaba açılan iletişim kutusunda seçin **tam içeri aktarma** tıklatıp **Tamam**.
    
   4. İşlem toocomplete bekleyin.

    > [!NOTE]
    > Üzerinde tam içeri aktarma atlayabilirsiniz hello şirket içi AD Bağlayıcısı hello kaynak özniteliği hello içeri aktarılan öznitelikleri listesinde zaten varsa. Diğer bir deyişle, toomake sırasında herhangi bir değişiklik yok [2. adım: hello kaynak özniteliği toohello şirket içi AD Bağlayıcısı eklemek şema](#step-2-add-the-source-attribute-to-the-on-premises-ad-connector-schema).

2. Çalıştırma **tam alma** hello adımında **Azure AD Bağlayıcısı**:

   1. Merhaba üzerinde sağ **Azure AD Bağlayıcısı** seçip **Çalıştır...**

   2. Merhaba açılan iletişim kutusunda seçin **tam içeri aktarma** tıklatıp **Tamam**.
   
   3. İşlem toocomplete bekleyin.

3. Var olan bir kullanıcı nesnesi üzerindeki Hello eşitleme kuralı değişiklikleri doğrulayın:

Şirket içi Active Directory ve Azure AD'den PreferredDataLocation içine alınmamış içinden Hello kaynak özniteliği, ilgili bağlayıcıyı alanı hello. Tam eşitleme adımla devam etmeden önce bunu yapmanız önerilir bir **Önizleme** üzerinde var olan bir kullanıcı hello nesnesinde AD bağlayıcı alanı şirket. Seçtiğiniz hello nesnesi doldurulmuş hello kaynak özniteliği olmalıdır. Başarılı bir **Önizleme** ile Merhaba hello meta veri deposu doldurulmuş PreferredDataLocation hello eşitleme kuralları doğru şekilde yapılandırdığınız iyi bir göstergesidir. Hakkında bilgi için toodo bir **Önizleme**, toosection başvuran [hello değişikliği doğrulayın](#verify-the-change).

4. Çalıştırma **tam eşitleme** hello adımında **şirket içi AD Bağlayıcısı**:

   1. Merhaba üzerinde sağ **şirket içi AD Bağlayıcısı** seçip **Çalıştır...**
  
   2. Merhaba açılan iletişim kutusunda seçin **tam eşitleme** tıklatıp **Tamam**.
   
   3. İşlem toocomplete bekleyin.

5. Doğrulama **bekleyen dışarı aktarmalar** tooAzure AD:

   1. Merhaba üzerinde sağ **Azure AD Bağlayıcısı** seçip **arama bağlayıcı alanı**.

   2. Merhaba arama bağlayıcı alanı açılan iletişim kutusunda:

      1. Ayarlama **kapsam** çok**bekleyen dışarı**.
      
      2. Dahil olmak üzere, tüm üç checkboxes denetleyin **ekleme, değiştirme ve silme**.
      
      3. Merhaba tıklatın **arama** düğmesini tooget hello değişiklikleri toobe dışarı aktarılan nesnelerle listesi. belirli bir nesne için tooexamine hello değişiklikleri hello nesne çift tıklayın.
      
      4. Merhaba değişiklikleri beklenen doğrulayın.

6. Çalıştırma **verme** hello adımında **Azure AD Bağlayıcısı**
      
   1. Sağ hello **Azure AD Bağlayıcısı** seçip **Çalıştır...**
   
   2. Merhaba çalıştırmak bağlayıcı açılan iletişim kutusunda, seçin **verme** tıklatıp **Tamam**.
   
   3. Dışarı aktarma tooAzure AD toocomplete için bekleyin.

> [!NOTE]
> Merhaba adımları hello tam eşitleme adım ve dışa aktarma adımını hello Azure AD Bağlayıcısı üzerinde içermez fark edebilirsiniz. Merhaba adımları Hello öznitelik değerleri şirket içi Active Directory tooAzure AD yalnızca akan gerekli değildir.

### <a name="step-7-re-enable-sync-scheduler"></a>7. adım: Eşitleme Zamanlayıcısı'nı yeniden etkinleştirin
Merhaba yerleşik Eşitleme Zamanlayıcısı'nı yeniden etkinleştirin:

1. PowerShell oturumu başlatın.

2. Zamanlanan eşitleme cmdlet'ini çalıştırarak yeniden etkinleştirin:`Set-ADSyncScheduler -SyncCycleEnabled $true`



## <a name="next-steps"></a>Sonraki adımlar
* Merhaba yapılandırma modeli hakkında daha fazla bilgiyi [anlama bildirim temelli hazırlama](active-directory-aadconnectsync-understanding-declarative-provisioning.md).
* Merhaba ifade dili hakkında daha fazla bilgiyi [anlama bildirim temelli hazırlama ifadelerini](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md).

**Genel bakış konuları**

* [Azure AD Connect eşitleme: anlamak ve eşitleme özelleştirme](active-directory-aadconnectsync-whatis.md)
* [Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md)
