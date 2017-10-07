---
title: "Azure AD Connect eşitleme: filtrelemeyi yapılandırma | Microsoft Docs"
description: "Açıklar nasıl tooconfigure Azure AD Connect eşitleme filtreleme."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 880facf6-1192-40e9-8181-544c0759d506
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 97979b508c560a6de6cb091b1b621bc1d51b25c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-configure-filtering"></a>Azure AD Connect Eşitleme: Filtrelemeyi yapılandırma
Filtreleme kullanarak, hangi nesnelerin Azure Active Directory (Azure AD) görüneceğini şirket içi dizininizden denetleyebilirsiniz. Merhaba varsayılan yapılandırmasını yapılandırılmış hello ormandaki tüm etki alanlarındaki tüm nesneleri alır. Genel olarak, önerilen yapılandırması hello budur. E-posta gönderin ve herkesin çağırmak için Exchange Online ve Skype Kurumsal, gibi Office 365 iş yükleri kullanarak kullanıcıların tam genel adres listesinden yararlanır. Merhaba varsayılan yapılandırma ile kullanıcılar bir şirket içi Exchange veya Lync uygulamasıyla sahip aynı deneyimi hello gerekir.

Bazı durumlarda ancak, gerekli bazı değişiklikler toohello varsayılan yapılandırmasını yapın. İşte bazı örnekler:

* Toouse hello planlama [birden çok Azure AD directory topolojisi](active-directory-aadconnect-topologies.md#each-object-only-once-in-an-azure-ad-tenant). Daha sonra tooapply eşitlenmiş tooa belirli Azure AD directory nesneleridir bir filtre toocontrol gerekir.
* Azure veya Office 365 için bir pilot çalıştırın ve Azure AD içinde yalnızca bir kullanıcı alt kümesini istiyor. Merhaba küçük pilot, önemli toohave eksiksiz bir genel adres listesi toodemonstrate hello işlevselliği değil.
* Çok sayıda hizmet hesapları ve Azure AD içinde istemediğiniz nonpersonal diğer hesapları var.
* Uyumluluk nedenleriyle, tüm kullanıcı hesapları şirket içi silmeyin. Yalnızca bunları devre dışı. Ancak Azure AD'de yalnızca etkin hesapları toobe mevcut istiyorsunuz.

Bu makalede, nasıl tooconfigure hello farklı filtreleme yöntemlerinden yer almaktadır.

> [!IMPORTANT]
> Microsoft, değiştirme veya Azure AD Connect eşitleme resmi olarak belgelenen hello Eylemler dışında işletim desteklemiyor. Bu eylemlerden herhangi birini bir Azure AD Connect eşitleme tutarsız veya desteklenmeyen durumda neden olabilir. Sonuç olarak, Microsoft teknik destek böyle dağıtımlarda sağlayamaz.

## <a name="basics-and-important-notes"></a>Temel kavramları ve önemli notlar
Azure AD Connect eşitleme herhangi bir zamanda filtreleme etkinleştirebilirsiniz. Dizin eşitleme, varsayılan yapılandırmayla başlatma ve filtrelemeyi yapılandırma, filtrelenir hello artık eşitlenmiş tooAzure AD nesnelerdir. Bu değişikliği nedeniyle, Azure AD'de daha önce eşitlendi, ancak ardından filtre tüm nesnelerin Azure AD'de silinir.

Değişiklikleri toofiltering yapmaya başlamadan önce emin olun, [hello zamanlanmış görevi devre dışı](#disable-scheduled-task) toobe doğru henüz doğrulamadınız değişiklikleri yanlışlıkla vermeyin şekilde.

Filtreleme hello birçok nesneleri kaldırmak için aynı zaman, istediğiniz herhangi bir dışarı aktarma başlamadan önce yeni filtrelerinizi doğruluğundan emin toomake tooAzure AD değiştirir. Merhaba yapılandırma adımlarını tamamladıktan sonra hello uymanızı öneririz [doğrulama adımları](#apply-and-verify-changes) dışarı aktarma ve değişiklikleri tooAzure AD yapmak için önce.

birçok silme sizden nesnelerini yanlışlıkla, hello tooprotect özelliği "[yanlışlıkla silmeleri engelleme](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md)" varsayılan olarak açıktır. Son birçok nesne silerseniz, bu makale tooallow hello toofollow hello adımlarda ihtiyacınız toofiltering (500) varsayılan olarak toogo tooAzure AD aracılığıyla siler.

Kasım 2015 önce bir yapı kullanıyorsanız ([1.0.9125](active-directory-aadconnect-version-history.md#1091250)) tooa filtre yapılandırmasını değiştirme olun ve yeniden hello yapılandırmasını tamamladıktan sonra tam eşitleme tüm parolaların tootrigger gerekiyor parola eşitleme, kullanın. Nasıl tootrigger parola tam eşitleme ile ilgili adımlar için bkz: [tüm parolaların tam eşitlemesi](active-directory-aadconnectsync-troubleshoot-password-synchronization.md#trigger-a-full-sync-of-all-passwords). Yapı 1.0.9125 üzerinde olduğunuz ya da daha sonra ardından hello normal **tam eşitleme** eylemi de hesaplar parolalarını eşitlenmiş olması gerektiği ve bu ek adım artık gerekli olup olmadığını.

Varsa **kullanıcı** yanlışlıkla silinen nesneleri Azure AD'de bir filtre hatası nedeniyle, hello kullanıcı nesnelerini filtreleme yapılandırmalarınızın kaldırarak Azure AD'de yeniden oluşturabilirsiniz. Ardından, dizinleri yeniden eşitleyebilirsiniz. Bu eylemin hello kullanıcılar Azure AD'de hello Geri Dönüşüm Kutusu'ndan geri yükler. Ancak, diğer nesne türleri geri alamazsınız. Örneğin, yanlışlıkla bir güvenlik grubunu silmek ve kullanılan tooACL bir kaynak olup olmadığını hello grubu ve onun ACL'ler kurtarılamıyor.

Azure AD Connect yalnızca toobe kapsamında bir kez kabul olduğunu nesneleri siler. Başka bir eşitleme altyapısı tarafından oluşturulan nesneleri Azure AD'de vardır ve bu nesnelerin kapsamında değil, filtreleme ekleyerek bunları kaldırmaz. Örneğin, tüm dizin tam bir kopyasını Azure AD'de oluşturulan bir DirSync sunucunuz ile başlayın ve paralel hello baştan etkin filtreleme ile yeni bir Azure AD Connect eşitleme sunucusu yüklerseniz, Azure AD Connect hello fazladan kaldırmaz DirSync tarafından oluşturulan nesneleri.

yüklediğinizde veya Azure AD Connect tooa daha yeni sürüm yükseltme filtreleme yapılandırması hello korunur. Her zaman yapılandırma hello en iyi bir yöntem tooverify yanlışlıkla hello ilk eşitleme döngüsü çalıştırmadan önce bir yükseltme tooa daha yeni sürümünü sonra değiştirilen değildi.

Birden çok orman sonra bu konuda tooevery ormanda açıklanan yapılandırmaları filtreleme hello uygulamanız gerekir (aynı hello istediğiniz varsayılarak bunların tümünün yapılandırması).

### <a name="disable-hello-scheduled-task"></a>Merhaba zamanlanmış görevini devre dışı bırakın
bir eşitleme döngüsü 30 dakikada tetikler toodisable hello yerleşik Zamanlayıcı şu adımları izleyin:

1. Tooa PowerShell komut isteminde gidin.
2. Çalıştırma `Set-ADSyncScheduler -SyncCycleEnabled $False` toodisable hello Zamanlayıcı.
3. Bu makalede belgelenen hello değişiklikleri yapın.
4. Çalıştırma `Set-ADSyncScheduler -SyncCycleEnabled $True` tooenable hello yeniden Zamanlayıcı.

**Bir Azure AD Connect yapı 1.1.105.0 önce kullanıyorsanız**  
bir eşitleme döngüsü üç saatte tetikler toodisable hello zamanlanmış görev şu adımları izleyin:

1. Başlat **Görev Zamanlayıcı** hello gelen **Başlat** menüsü.
2. Doğrudan altında **Görev Zamanlayıcı Kitaplığı**, adında Bul hello görev **Azure AD Sync Scheduler**, sağ tıklatın ve seçin **devre dışı**.  
   ![Görev Zamanlayıcısı](./media/active-directory-aadconnectsync-configure-filtering/taskscheduler.png)  
3. Artık yapılandırma değişikliklerini yapın ve hello eşitleme altyapısı hello el ile çalıştırabilirsiniz **Eşitleme Hizmeti Yöneticisi'ni** konsol.

Tüm filtre değişiklikleri tamamladıktan sonra geri toocome unutmayın ve **etkinleştirmek** yeniden hello görev.

## <a name="filtering-options"></a>Filtreleme seçenekleri
Filtreleme yapılandırma türleri toohello dizin eşitleme aracı aşağıdaki hello uygulayabilirsiniz:

* [**Grup tabanlı**](#group-based-filtering): tek bir grup göre filtreleme yalnızca yapılandırılabilir ilk yüklemesinde hello Yükleme Sihirbazı'nı kullanarak.
* [**Etki alanı tabanlı**](#domain-based-filtering): Bu seçeneği kullanarak, hangi etki alanlarının tooAzure AD eşitleme seçebilirsiniz. Ayrıca, ekleyebilir ve Azure AD Connect eşitleme yükledikten sonra değişiklikleri tooyour şirket içi altyapı yaptığınızda etki alanları hello eşitleme altyapısı yapılandırmasından kaldırın.
* [**Kuruluş birimi (OU) – temel**](#organizational-unitbased-filtering): Bu seçeneği kullanarak, hangi OU'lar seçebilirsiniz tooAzure AD eşitleyin. Bu seçenek, seçili OU içindeki tüm nesne türleri için kullanılır.
* [**Öznitelik tabanlı**](#attribute-based-filtering): Bu seçeneği kullanarak nesneleri hello nesneleri öznitelik değerlerine göre filtreleyebilirsiniz. Ayrıca, farklı nesne türleri için farklı filtreler de olabilir.

Merhaba birden çok filtre seçeneklerini kullanabilirsiniz aynı anda. Örneğin, OU tabanlı filtreleme kullanabilirsiniz tooonly bir OU'da nesneleri içerir. AT hello aynı zaman, kullanabileceğiniz özniteliği tabanlı filtreleme toofilter hello nesneleri daha fazla. Birden çok filtre yöntemi kullandığınızda, hello filtreleri hello filtreler arasında mantıksal "ve" kullanın.

## <a name="domain-based-filtering"></a>Etki alanı tabanlı filtreleme
Bu bölümde, etki alanı filtre ile Merhaba adımları tooconfigure sağlar. Eklenen veya Azure AD Connect yüklendikten sonra ormanda etki alanları kaldırıldı, filtreleme yapılandırması tooupdate hello de.

Merhaba tercih edilen yol toochange etki alanı tabanlı filtreleme olduğundan hello Yükleme Sihirbazı'nı çalıştıran ve değiştirme [etki alanı ve OU filtreleme](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering). Merhaba Yükleme Sihirbazı'nı bu konuda belgelenmiştir tüm hello görevlerini otomatikleştirir.

Herhangi bir nedenden dolayı oluşturulamıyor toorun hello Yükleme Sihirbazı'nı iseniz yalnızca aşağıdaki adımları izlemelisiniz.

Etki alanı tabanlı filtreleme yapılandırması aşağıdaki adımlardan oluşur:

1. [Merhaba etki alanlarını seçin](#select-domains-to-be-synchronized) hello eşitlemede tooinclude istiyor.
2. Her eklenebilir ve etki alanı kaldırılabilir için hello Ayarla [çalıştırma profili](#update-run-profiles).
3. [Uygulama ve değişiklikleri doğrulamak](#apply-and-verify-changes).

### <a name="select-hello-domains-toobe-synchronized"></a>Select hello etki alanları toobe eşitlendi
tooset hello etki alanı filtre, adımları hello:

1. Azure AD Connect eşitleme hello üyesi olan bir hesabı kullanarak çalışan toohello Server'da oturum **ADSyncAdmins** güvenlik grubu.
2. Başlat **eşitleme hizmeti** hello gelen **Başlat** menüsü.
3. Seçin **Bağlayıcılar**ve hello **Bağlayıcılar** listesinde, hello bağlayıcı hello türüyle seçin **Active Directory etki alanı Hizmetleri**. İçinde **Eylemler**seçin **özellikleri**.  
   ![Bağlayıcı özellikleri](./media/active-directory-aadconnectsync-configure-filtering/connectorproperties.png)  
4. Tıklatın **dizin bölümlerini Yapılandır**.
5. Merhaba, **dizin bölümlerini Seç** listesinden seçin ve gerektiğinde etki alanları seçimini kaldırın. Toosynchronize istediğiniz yalnızca hello bölümleri'nin seçili olduğunu doğrulayın.  
   ![Bölümler](./media/active-directory-aadconnectsync-configure-filtering/connectorpartitions.png)  
   Şirket içi Active Directory altyapınızı değişti ve ekledikten veya hello ormandan etki alanları kaldırıldı, hello'ı tıklatın **yenileme** düğmesini tooget güncelleştirilmiş bir listesi. Yenilediğinizde, kimlik bilgileri sorulur. Okuma erişimi tooWindows Server Active Directory ile tüm kimlik bilgilerini sağlayın. Merhaba iletişim kutusunda önceden doldurulmaz toobe hello kullanıcı yok.  
   ![Yenileme gerekiyor](./media/active-directory-aadconnectsync-configure-filtering/refreshneeded.png)  
6. İşiniz bittiğinde, hello kapatmak **özellikleri** tıklatarak iletişim **Tamam**. Merhaba ormandan etki alanları kaldırdıysanız, açılır ileti bir etki alanı kaldırıldı ve bu yapılandırma temizlenecek söyler.
7. Tooadjust hello devam [çalıştırma profili](#update-run-profiles).

### <a name="update-hello-run-profiles"></a>Çalıştırma hello profilleri güncelleştir
Etki alanı filtre güncelleştirdik, tooupdate çalıştırmak hello profilleri de gerekir.

1. Merhaba, **Bağlayıcılar** listesinde, bu hello hello önceki adımda değiştirdiğiniz bağlayıcıyı seçili olduğundan emin olun. İçinde **Eylemler**seçin **çalıştırma profillerini Yapılandır**.  
   ![Çalıştırma profilleri 1 Bağlayıcısı](./media/active-directory-aadconnectsync-configure-filtering/connectorrunprofiles1.png)  
2. Bul ve hello profilleri aşağıdaki belirleyin:
    * Tam içeri aktarma
    * Tam eşitleme
    * Delta içeri aktarma
    * Delta eşitleme
    * Dışarı Aktarma
3. Her bir profil için hello ayarlamak **eklenen** ve **kaldırılan** etki alanları.
    1. Her beş hello profilleri için adımları izleyerek her biri için hello **eklenen** etki alanı:
        1. Merhaba çalıştırma profilini seçin ve'ı tıklatın **yeni adım**.
        2. Merhaba üzerinde **yapılandırma adımı** sayfasında hello **türü** olduğunuz açılır menüsünde, select hello adım türü hello hello profil gibi aynı ad ile yapılandırma. Ardından **İleri**'ye tıklayın.  
        ![Çalıştırma profilleri 2 Bağlayıcısı](./media/active-directory-aadconnectsync-configure-filtering/runprofilesnewstep1.png)  
        3. Merhaba üzerinde **Bağlayıcı yapılandırması** sayfasında hello **bölüm** açılır menü, select hello tooyour etki alanı filtre eklediğiniz hello etki alanının adını.  
        ![Çalıştırma profilleri 3 Bağlayıcısı](./media/active-directory-aadconnectsync-configure-filtering/runprofilesnewstep2.png)  
        4. tooclose hello **çalıştırma profilini Yapılandır** iletişim kutusunda, tıklatın **son**.
    2. Her beş hello profilleri için adımları izleyerek her biri için hello **kaldırılan** etki alanı:
        1. Merhaba çalıştırma profilini seçin.
        2. Merhaba, **değeri** Merhaba, **bölüm** özniteliktir GUID, adım ve tıklatın çalıştırmak select hello **silmek adım**.  
        ![Çalıştırma profilleri 4 Bağlayıcısı](./media/active-directory-aadconnectsync-configure-filtering/runprofilesdeletestep.png)  
    3. Değişikliğiniz doğrulayın. Toosynchronize istediğiniz her bir etki alanı, her çalıştırma profili bir adım olarak listelenmesi gerekir.
4. tooclose hello **çalıştırma profillerini Yapılandır** iletişim kutusunda, tıklatın **Tamam**.
5.  toocomplete hello yapılandırma toorun gereken bir **tam alma** ve **Delta eşitleme**. Merhaba bölüm okuma devam [Uygula ve değişiklikleri doğrulamak](#apply-and-verify-changes).

## <a name="organizational-unitbased-filtering"></a>Kuruluş birimi tabanlı filtreleme
Merhaba tercih edilen yol toochange OU tabanlı filtreleme olduğundan hello Yükleme Sihirbazı'nı çalıştıran ve değiştirme [etki alanı ve OU filtreleme](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering). Merhaba Yükleme Sihirbazı'nı bu konuda belgelenmiştir tüm hello görevlerini otomatikleştirir.

Herhangi bir nedenden dolayı oluşturulamıyor toorun hello Yükleme Sihirbazı'nı iseniz yalnızca aşağıdaki adımları izlemelisiniz.

tooconfigure kuruluş birimi tabanlı filtreleme, adımları hello:

1. Azure AD Connect eşitleme hello üyesi olan bir hesabı kullanarak çalışan toohello Server'da oturum **ADSyncAdmins** güvenlik grubu.
2. Başlat **eşitleme hizmeti** hello gelen **Başlat** menüsü.
3. Seçin **Bağlayıcılar**ve hello **Bağlayıcılar** listesinde, hello bağlayıcı hello türüyle seçin **Active Directory etki alanı Hizmetleri**. İçinde **Eylemler**seçin **özellikleri**.  
   ![Bağlayıcı özellikleri](./media/active-directory-aadconnectsync-configure-filtering/connectorproperties.png)  
4. Tıklatın **dizin bölümlerini Yapılandır**seçin tooconfigure istediğiniz ve ardından hello etki alanı **kapsayıcıları**.
5. İstendiğinde, okuma erişimi tooyour ile şirket içi Active Directory kimlik bilgilerini sağlayın. Merhaba iletişim kutusunda önceden doldurulmaz toobe hello kullanıcı yok.
6. Merhaba, **kapsayıcıları Seç** iletişim kutusu, yoksa hello bulut diziniyle toosynchronize istediğiniz ve ardından, Temizle hello OU'lar **Tamam**.  
   ![Merhaba kapsayıcıları Seç iletişim kutusunda OU'lar](./media/active-directory-aadconnectsync-configure-filtering/ou.png)  
   * Merhaba **bilgisayarlar** Windows 10 bilgisayarları toobe tooAzure AD başarıyla eşitlendi için kapsayıcı seçilmelidir. Etki alanına katılmış bilgisayarlarınızı diğer OU'larda bulunuyorsa, bunlar seçildiğinden emin olun.
   * Merhaba **ForeignSecurityPrincipals** Güvenleri ile birden çok ormanınız varsa, kapsayıcı seçilmelidir. Bu kapsayıcı çözülmüş ormanlar arası güvenlik grubu üyeliği toobe sağlar.
   * Merhaba **RegisteredDevices** hello cihaz geri yazma özelliği etkinleştirilmişse, OU seçilmelidir. Başka bir geri yazma özelliğini kullanırsanız, grup geri yazma gibi bu konumları seçildiğinden emin olun.
   * Kullanıcılar, iNetOrgPersons, gruplar, kişiler ve bilgisayarlar bulunduğu OU seçin. Merhaba resimde bu OU'lar hello ManagedObjects OU bulunur.
   * Grup tabanlı filtreleme kullanırsanız, hello hello Grup bulunduğu OU'ya dahil edilmelidir.
   * Merhaba filtreleme yapılandırması tamamlandıktan sonra eklenen yeni OU'lar eşitlenen veya eşitlenmemiş olmadığını yapılandırabilirsiniz unutmayın. Ayrıntılar için Hello sonraki bölüme bakın.
7. İşiniz bittiğinde, hello kapatmak **özellikleri** tıklatarak iletişim **Tamam**.
8. toocomplete hello yapılandırma toorun gereken bir **tam alma** ve **Delta eşitleme**. Merhaba bölüm okuma devam [Uygula ve değişiklikleri doğrulamak](#apply-and-verify-changes).

### <a name="synchronize-new-ous"></a>Yeni OU'lar Eşitle
Varsayılan olarak filtreleme yapılandırıldıktan sonra oluşturulan yeni OU'lar eşitlenir. Bu durum, seçili bir onay kutusu tarafından belirtilir. Ayrıca, bazı alt kuruluş birimlerini işaretini kaldırabilirsiniz. tooget Bu davranış, mavi onay işaretiyle (varsayılan durumuna) beyaz oluncaya kadar hello kutusuna tıklayın. Ardından toosynchronize istemediğiniz alt OU seçimini kaldırın.

Tüm alt OU'lar eşitlenir, hello kutusunu mavi bir onay işareti ile beyaz olur.  
![Seçili tüm kutuları ile OU](./media/active-directory-aadconnectsync-configure-filtering/ousyncnewall.png)

Bazı alt kuruluş birimlerini seçilmemiş olsa, hello kutu gri beyaz onay işaretine sahip olur.  
![Bazı alt-seçili OU'ları ile OU](./media/active-directory-aadconnectsync-configure-filtering/ousyncnew.png)

Bu yapılandırma ile ManagedObjects altında oluşturulan yeni bir OU eşitlenir.

Hello Azure AD Connect Yükleme Sihirbazı'nı her zaman bu yapılandırma oluşturur.

### <a name="dont-synchronize-new-ous"></a>Yeni OU'lar eşitleme
Merhaba eşitleme yapılandırabilirsiniz altyapısı toonot hello filtreleme yapılandırması tamamlandıktan sonra yeni OU'lar eşitleyin. Bu durum hello UI hello kutusunda onay işareti ile düz gri görünen tarafından belirtilir. tooget Bu davranış, hiçbir onay işaretiyle beyaz oluncaya kadar hello kutusuna tıklayın. Ardından hello alt-OU'lar toosynchronize istediğinizi seçin.

![Seçili hello kök ile OU](./media/active-directory-aadconnectsync-configure-filtering/oudonotsyncnew.png)

Bu yapılandırma ile ManagedObjects altında oluşturulan yeni bir OU eşitlenmemiş.

## <a name="attribute-based-filtering"></a>Öznitelik tabanlı filtreleme
Kasım 2015 hello kullandığınızdan emin olun ([1.0.9125](active-directory-aadconnect-version-history.md#1091250)) veya sonraki derleme için bu adımları toowork.

Öznitelik tabanlı filtreleme hello en esnek şekilde toofilter nesneleri durumdadır. Merhaba gücünü kullanabilirsiniz [bildirim temelli hazırlama](active-directory-aadconnectsync-understanding-declarative-provisioning.md) toocontrol tooAzure AD nesne olduğunda, neredeyse her açıdan eşitlenir.

Uygulayabileceğiniz [gelen](#inbound-filtering) Active Directory toohello meta veri deposu filtreleme ve [giden](#outbound-filtering) hello meta veri deposu tooAzure AD filtreleme. Merhaba kolay toomaintain olduğu için gelen filtreleme uygulamanızı öneririz. Yalnızca hello değerlendirme gerçekleştirilebildiği önce birden çok orman toojoin nesnelerden istedi, giden filtreleme kullanmanız gerekir.

### <a name="inbound-filtering"></a>Filtreleme gelen
Gelen filtreleme hello varsayılan yapılandırma, tooAzure AD giderek nesneleri eşitlenen tooa değeri toobe ayarlanmadı hello meta veri deposu özniteliği cloudFiltered burada olmalıdır kullanır. Bu özniteliğin değeri çok ayarlarsanız**doğru**, hello nesne eşitlenmemiş sonra. Çok ayarlanmamalıdır**yanlış**, tasarım. diğer kurallardan hello özelliği toocontribute bir değer olmasını toomake, bu öznitelik yalnızca beklenen toohave hello değerleri **True** veya **NULL** (yok).

Filtreleme gelen, hello gücünü kullanın **kapsam** toosynchronize nesneleri veya değil eşitleme toodetermine. Burada, kendi kuruluşunuzun gereksinimlerine ayarlamalar toofit olun budur. Merhaba kapsam modülü bir **grup** ve **yan tümcesi** bir eşitleme kuralının kapsamda olduğunda toodetermine. Bir veya daha çok yan tümceleri içeren bir grubu. Birden çok yan tümcesi birden çok gruplar arasındaki mantıksal "veya" arasındaki mantıksal "ve" yoktur.

Bize bir örneğe bakın:  
![Kapsam](./media/active-directory-aadconnectsync-configure-filtering/scope.png)  
Bu olarak okunmalıdır **(departman = BT) veya (departman = satış ve c = US)**.

İçinde aşağıdaki hello örnekleri ve adımları, hello kullanıcı nesnesi bir örnek olarak kullanabilirsiniz, ancak tüm nesne türleri için bunu kullanabilirsiniz.

Örnekleri aşağıdaki hello hello öncelik değeri 50 ile başlar. Bu, kullanılmayan herhangi bir sayı olabilir, ancak 100'den daha az olmalıdır.

#### <a name="negative-filtering-do-not-sync-these"></a>Negatif filtreleme: "Bu eşitleme değil"
Aşağıdaki örneğine hello filtrelemek (eşitleme değil) tüm kullanıcılar nerede **extensionAttribute15** hello değerine sahip **NoSync**.

1. Azure AD Connect eşitleme hello üyesi olan bir hesabı kullanarak çalışan toohello Server'da oturum **ADSyncAdmins** güvenlik grubu.
2. Başlat **eşitleme kuralları Düzenleyicisi** hello gelen **Başlat** menüsü.
3. Emin olun **gelen** seçilir ve tıklatın **Yeni Kural Ekle**.
4. Merhaba kuralına gibi açıklayıcı bir ad verin "*içinde AD'den – kullanıcı DoNotSyncFilter*". Select hello doğru orman, select **kullanıcı** hello olarak **CS Nesne türü**seçip **kişi** hello olarak **MV nesne türü**. İçinde **bağlantı türü**seçin **katılma**. İçinde **öncelik**, şu anda başka bir eşitleme kuralı (örneğin, 50) tarafından kullanılmayan bir değer yazın ve ardından **sonraki**.  
   ![Gelen 1 açıklaması](./media/active-directory-aadconnectsync-configure-filtering/inbound1.png)  
5. İçinde **Scoping filtre**, tıklatın **Grup Ekle**, tıklatıp **yan tümce Ekle**. İçinde **özniteliği**seçin **ExtensionAttribute15**. Olduğundan emin olun **işleci** çok ayarlanır**eşit**ve tür hello değer **NoSync** hello içinde **değeri** kutusu. **İleri**’ye tıklayın.  
   ![2 kapsam gelen](./media/active-directory-aadconnectsync-configure-filtering/inbound2.png)  
6. Merhaba bırakın **katılma** boş kuralları ve ardından **sonraki**.
7. Tıklatın **ekleme dönüşümünü**seçin hello **FlowType** olarak **sabit**seçip **cloudFiltered** hello olarak  **Hedef öznitelik**. Merhaba, **kaynak** metin kutusunda, **doğru**. Tıklatın **Ekle** toosave hello kuralı.  
   ![3 dönüştürme gelen](./media/active-directory-aadconnectsync-configure-filtering/inbound3.png)
8. toocomplete hello yapılandırma toorun gereken bir **tam eşitleme**. Merhaba bölüm okuma devam [Uygula ve değişiklikleri doğrulamak](#apply-and-verify-changes).

#### <a name="positive-filtering-only-sync-these"></a>Pozitif filtreleme: "bunlar yalnızca eşitleme"
Pozitif filtreleme ifade belirgin toobe, örneğin konferans odaları eşitlenmiş değil tooconsider nesnelerden de olduğundan daha zor olabilir. Ayrıca giderek toooverride hello varsayılan filtre hello out-of-box kuralında olan **içinde AD'den - kullanıcı katılma**. Özel filtre oluşturduğunuzda, toonot kritik sistem nesneleri, yineleme çakışma nesneleri, özel posta kutuları ve hello hizmet hesapları için Azure AD Connect eklediğinizden emin olun.

Merhaba pozitif filtreleme seçeneği iki eşitleme kuralı gerektirir. Merhaba doğru nesneleri toosynchronize kapsamla bir kural (veya birkaç) gerekir. Ayrıca, eşitlenmesi gereken bir nesne olarak henüz tanımlanmış henüz tüm nesneleri filtreleyen ikinci bir catch tüm eşitleme kuralı gerekir.

Aşağıdaki örneğine hello, yalnızca kullanıcı nesneleri hello departmanı özniteliği hello değeri olduğu eşitleme **satış**.

1. Azure AD Connect eşitleme hello üyesi olan bir hesabı kullanarak çalışan toohello Server'da oturum **ADSyncAdmins** güvenlik grubu.
2. Başlat **eşitleme kuralları Düzenleyicisi** hello gelen **Başlat** menüsü.
3. Emin olun **gelen** seçilir ve tıklatın **Yeni Kural Ekle**.
4. Merhaba kuralına gibi açıklayıcı bir ad verin "*AD'den – kullanıcı satış senkronize*". Select hello doğru orman, select **kullanıcı** hello olarak **CS Nesne türü**seçip **kişi** hello olarak **MV nesne türü**. İçinde **bağlantı türü**seçin **katılma**. İçinde **öncelik**, şu anda başka bir eşitleme kuralı (örneğin 51) tarafından kullanılmayan bir değer yazın ve ardından **sonraki**.  
   ![4 açıklama gelen](./media/active-directory-aadconnectsync-configure-filtering/inbound4.png)  
5. İçinde **Scoping filtre**, tıklatın **Grup Ekle**, tıklatıp **yan tümce Ekle**. İçinde **özniteliği**seçin **departmanı**. İşleç çok ayarlandığından emin olun**eşit**ve tür hello değer **satış** hello içinde **değeri** kutusu. **İleri**’ye tıklayın.  
   ![5 kapsam gelen](./media/active-directory-aadconnectsync-configure-filtering/inbound5.png)  
6. Merhaba bırakın **katılma** boş kuralları ve ardından **sonraki**.
7. Tıklatın **ekleme dönüşümünü**seçin **sabit** hello olarak **FlowType**ve select hello **cloudFiltered** hello olarak  **Hedef öznitelik**. Merhaba, **kaynak** kutusuna **False**. Tıklatın **Ekle** toosave hello kuralı.  
   ![6 dönüştürme gelen](./media/active-directory-aadconnectsync-configure-filtering/inbound6.png)  
   Bu açıkça ayarladığınız cloudFiltered çok özel bir durumdur**False**.
8. Şimdi sahip olduğumuz toocreate hello catch tüm eşitleme kuralı. Merhaba kuralına gibi açıklayıcı bir ad verin "*içinde AD'den – kullanıcı Catch-tüm filtre*". Select hello doğru orman, select **kullanıcı** hello olarak **CS Nesne türü**seçip **kişi** hello olarak **MV nesne türü**. İçinde **bağlantı türü**seçin **katılma**. İçinde **öncelik**, şu anda başka bir eşitleme kuralı (örneğin 99) tarafından kullanılmayan bir değer yazın. Yüksek (daha düşük önceliğe) hello önceki eşitleme kuralı bir öncelik değeri seçtiniz. Ancak ek departmanlar eşitleme toostart istediğinizde daha fazla filtreleme eşitleme kurallarını daha sonra ekleyeceği bazı yer de bırakmış olabilirsiniz. **İleri**’ye tıklayın.  
   ![7 açıklama gelen](./media/active-directory-aadconnectsync-configure-filtering/inbound7.png)  
9. Bırakın **Scoping filtre** boş öğesini tıklatıp **sonraki**. Boş bir filtre, hello kural uygulanan toobe tooall nesneleri gösterir.
10. Merhaba bırakın **katılma** boş kuralları ve ardından **sonraki**.
11. Tıklatın **ekleme dönüşümünü**seçin **sabit** hello olarak **FlowType**seçip **cloudFiltered** hello olarak  **Hedef öznitelik**. Merhaba, **kaynak** kutusuna **doğru**. Tıklatın **Ekle** toosave hello kuralı.  
    ![3 dönüştürme gelen](./media/active-directory-aadconnectsync-configure-filtering/inbound3.png)  
12. toocomplete hello yapılandırma toorun gereken bir **tam eşitleme**. Merhaba bölüm okuma devam [Uygula ve değişiklikleri doğrulamak](#apply-and-verify-changes).

Gerekiyorsa, hello ilk türü burada daha çok nesne hello eşitlemeye dahil daha fazla kural oluşturabilirsiniz.

### <a name="outbound-filtering"></a>Giden filtreleme
Bazı durumlarda bu gerekli toodo hello hello nesneleri hello meta veri deposunda yalnızca katıldıktan sonra filtreleme olur. Örneğin, hello posta özniteliğinin hello kaynak ormandaki ve hello hesap ormanı, bir nesne eşitlenmesi gerektiği varsa toodetermine hello userPrincipalName özniteliği gerekli toolook olması olabilir. Bu durumlarda, hello giden kuralı üzerinde filtreleme hello oluşturun.

Bu örnekte, böylece yalnızca kullanıcılar, posta ve userPrincipalName biten sahip hello filtreleme değiştirmek @contoso.com eşitlenir:

1. Azure AD Connect eşitleme hello üyesi olan bir hesabı kullanarak çalışan toohello Server'da oturum **ADSyncAdmins** güvenlik grubu.
2. Başlat **eşitleme kuralları Düzenleyicisi** hello gelen **Başlat** menüsü.
3. Altında **kuralları türü**, tıklatın **giden**.
4. Adlı Bul hello kuralını **tooAAD – kullanıcı katılma çıkışı**, tıklatıp **Düzenle**.
5. Merhaba açılır pencerede yanıt **Evet** toocreate hello kuralın bir kopyası.
6. Merhaba üzerinde **açıklama** sayfasında, değişiklik **öncelik** tooan 50 gibi kullanılmayan değeri.
7. Tıklatın **Scoping filtre** üzerinde hello sol gezinti ve ardından **Ekle yan tümcesi**. İçinde **özniteliği**seçin **posta**. İçinde **işleci**seçin **ENDSWITH**. İçinde **değeri**, türü  **@contoso.com** ve ardından **Ekle yan tümcesi**. İçinde **özniteliği**seçin **userPrincipalName**. İçinde **işleci**seçin **ENDSWITH**. İçinde **değeri**, türü  **@contoso.com** .
8. **Kaydet** düğmesine tıklayın.
9. toocomplete hello yapılandırma toorun gereken bir **tam eşitleme**. Merhaba bölüm okuma devam [Uygula ve değişiklikleri doğrulamak](#apply-and-verify-changes).

## <a name="apply-and-verify-changes"></a>Uygulama ve değişiklikleri doğrulayın
Yapılandırma değişikliklerini yaptıktan sonra zaten hello sistemde toohello nesneleri uygulamanız gerekir. Şu anda hello eşitleme altyapısı olmayan hello nesneleri işlenmesi gerektiğini de olabilir (ve hello eşitleme altyapısı gerekiyor tooread hello kaynak sistemi yeniden tooverify içeriği).

Kullanarak hello yapılandırması değiştiyse **etki alanı** veya **kuruluş birimi** yeniden toodo gerekiyor filtreleme bir **tam alma**, ardından **Delta Eşitleme**.

Kullanarak hello yapılandırması değiştiyse **özniteliği** yeniden toodo gerekiyor filtreleme bir **tam eşitleme**.

Adımları hello:

1. Başlat **eşitleme hizmeti** hello gelen **Başlat** menüsü.
2. Seçin **Bağlayıcılar**. Merhaba, **Bağlayıcılar** listesinde, hello bağlayıcı bir yapılandırma değişikliği daha önce yaptığınız yeri seçin. İçinde **Eylemler**seçin **çalıştırmak**.  
   ![Bağlayıcı çalıştırın](./media/active-directory-aadconnectsync-configure-filtering/connectorrun.png)  
3. İçinde **çalıştırma profili**, hello önceki bölümde belirtildiği hello işlemi seçin. Toorun iki eylem ihtiyacınız varsa, ikinci hello sonra çalışma hello birinci bitirdi. (Merhaba **durumu** sütunu **boşta** seçili hello Bağlayıcısı için.)

Başlangıç eşitlemesinden sonra tüm değişiklikler dışarı hazırlanmış toobe alınır. Azure AD'de gerçekten hello değişiklik yapmadan önce bu değişiklikleri doğru tooverify istiyorsunuz.

1. Bir komut istemi başlatın ve çok gidin`%Program Files%\Microsoft Azure AD Sync\bin`.
2. `csexport "Name of Connector" %temp%\export.xml /f:x` öğesini çalıştırın.  
   Eşitleme hizmeti Hello hello Bağlayıcısı adıdır. Bu ad benzer too"contoso.com – AAD için Azure AD var."
3. `CSExportAnalyzer %temp%\export.xml > %temp%\export.csv` öğesini çalıştırın.
4. Artık Microsoft Excel'de incelenebilir export.csv adlı % temp % içinde bir dosyanız var. Bu dosya dışarı toobe hakkında tüm hello değişikliklerini içerir.
5. Toohello veri Hello gerekli değişiklikleri yapın ya da yapılandırma ve çalıştırma adımları yeniden (içeri aktarma, eşitleme ve doğrula) kadar dışarı toobe hakkında değişikliklerini hello beklediğiniz.

Memnun kaldığınızda, hello değişiklikleri tooAzure AD verin.

1. Seçin **Bağlayıcılar**. Merhaba, **Bağlayıcılar** listesinde, hello Azure AD bağlayıcısını seçin. İçinde **Eylemler**seçin **çalıştırmak**.
2. İçinde **çalıştırma profili**seçin **verme**.
3. Daha sonra yapılandırma değişikliklerinizi birçok nesne silerseniz, hello sayı (varsayılan değer 500) hello yapılandırılan eşik değerinden daha fazla olduğunda hello verme hata bakın. Bu hatayı görmek sonra tootemporarily devre dışı bırak hello gerekir "[yanlışlıkla silmeleri engelleme](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md)" özelliği.

Bu zaman tooenable hello Zamanlayıcı yeniden sunulmuştur.

1. Başlat **Görev Zamanlayıcı** hello gelen **Başlat** menüsü.
2. Doğrudan altında **Görev Zamanlayıcı Kitaplığı**, adında Bul hello görev **Azure AD Sync Scheduler**, sağ tıklatın ve seçin **etkinleştirmek**.

## <a name="group-based-filtering"></a>Grup tabanlı filtreleme
Grup tabanlı filtreleme hello kullanarak Azure AD Connect yükleme ilk kez yapılandırabilirsiniz [özel yükleme](active-directory-aadconnect-get-started-custom.md#sync-filtering-based-on-groups). Cihazın kullanılması amaçlanan eşitlenmiş nesneleri toobe küçük bir kümesini istediğiniz pilot dağıtımı. Grup tabanlı filtreleme devre dışı bıraktığınızda, yeniden etkinleştirilemez. Bunun *desteklenmiyor* toouse grup tabanlı bir özel yapılandırmasında filtreleme. Merhaba Yükleme Sihirbazı'nı kullanarak bu özelliği yalnızca tooconfigure desteklenir. Pilot uygulamanızı tamamladıktan sonra ardından hello diğer filtreleme seçenekleri bu konudaki kullanın. OU dayalı birlikte grup tabanlı ile filtreleme kullanırken hello hello grubu ve üyelerini bulunduğu OU(s) dahil edilmelidir.

Birden fazla AD ormanına eşitlerken her AD Bağlayıcısı için farklı bir grubu belirterek grup tabanlı filtreleme yapılandırabilirsiniz. Bir kullanıcı bir AD ormanında toosynchronize istiyor ve hello aynı kullanıcı varsa veya diğer AD ormanlarda daha ilgili FSP (yabancı güvenlik sorumlusu) nesneleri, söz konusu hello kullanıcı nesne ve tüm ilgili emin olmalısınız FSP nesneleri Grup tabanlı içinde olur Filtre kapsamı. Grup tabanlı filtreleme tarafından bir veya daha fazla hello FSP nesneleri hariç, hello kullanıcı nesnesi eşitlenmiş tooAzure AD olmaz.

## <a name="next-steps"></a>Sonraki adımlar
- Daha fazla bilgi edinmek [Azure AD Connect eşitleme](active-directory-aadconnectsync-whatis.md) yapılandırma.
- Daha fazla bilgi edinmek [şirket içi kimliklerinizi Azure AD ile tümleştirme](active-directory-aadconnect.md).
