---
title: aaaAzure IOT paketi ve Azure Active Directory | Microsoft Docs
description: "Azure IOT paketi Azure Active Directory toomanage izinleri nasıl kullandığını açıklar."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 246228ba-954a-4d96-b6d6-e53e4590cb4f
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/09/2017
ms.author: dobett
ms.openlocfilehash: 4768630f2de4bb431731fbd4e8929232bc80b9f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="permissions-on-hello-azureiotsuitecom-site"></a>Merhaba azureiotsuite.com sitesindeki izinler

## <a name="what-happens-when-you-sign-in"></a>Oturum açtığınızda ne olur

Merhaba, oturum açtığınızda ilk kez [azureiotsuite.com][lnk-azureiotsuite], hello site belirler sahip hello üzerinde şu anda hello izin düzeyleri seçili Azure Active Directory (AAD) kiracısına ve Azure aboneliği.

1. İlk olarak, toopopulate hello listesi görülen kiracılar sonraki tooyour kullanıcıadı hello site Azure'dan hangi AAD kiracılarına ait olduğunuz öğrenir. Şu anda hello site aynı anda yalnızca bir kiracı için kullanıcı belirteçleri alabilir. Merhaba açılır hello sağ üst köşedeki kullanarak kiracılar geçiş yaptığınızda, bu nedenle, hello siteyi, toothat Kiracı tooobtain hello belirteçlerinde bu Kiracı için günlüğe kaydeder.

2. Kiracı hello ile ilişkili abonelikleri seçili Azure'dan ardından, hello site öğrenir. Yeni bir önceden yapılandırılmış çözümü oluşturduğunuzda hello kullanılabilir abonelikleri görürsünüz.

3. Son olarak, tüm hello kaynakları hello Aboneliklerde hello site alır ve kaynak grupları önceden yapılandırılmış çözümler olarak etiketlenmiş ve hello hello giriş sayfasındaki kutucukları doldurur.

Aşağıdaki bölümlerde hello erişim toohello önceden yapılandırılmış çözümleri denetlemek hello roller açıklanmıştır.

## <a name="aad-roles"></a>AAD rolleri

Merhaba AAD rolleri hello özelliği önceden yapılandırılmış çözümleri sağlama denetlemek ve önceden yapılandırılmış bir çözümdeki kullanıcıları yönetme.

AAD'de yönetici rolleri hakkında daha fazla bilgi bulabilirsiniz [Azure AD'de yönetici rolleri atama][lnk-aad-admin]. Merhaba geçerli makale üzerinde hello odaklanır **genel yönetici** ve hello **kullanıcı** hello tarafından kullanılan directory rolleri önceden yapılandırılmış çözümleri.

### <a name="global-administrator"></a>Genel yönetici

AAD kiracısı başına çok sayıda genel yönetici olabilir:

* Bir AAD kiracısı oluşturduğunuzda varsayılan hello genel yönetici, Kiracı tarafından olduğunuz.
* Merhaba genel yönetici önceden yapılandırılmış bir çözüm sağlayabilir ve atanmış bir **yönetici** hello uygulamanın AAD kiracısının içinde rol.
* Başka bir kullanıcı aynı Merhaba, AAD kiracısı bir uygulama oluşturur, hello varsayılan rol toohello genel yönetici verilir **salt okunur**.
* Genel yönetici hello kullanan uygulamalar için kullanıcıların tooroles atayabilirsiniz [Azure portal][lnk-portal].

### <a name="domain-user"></a>Etki alanı kullanıcısı

AAD kiracısı başına çok sayıda etki alanı kullanıcı olabilir:

* Bir etki alanı kullanıcısı hello üzerinden önceden yapılandırılmış bir çözüm sağlayabilir [azureiotsuite.com] [ lnk-azureiotsuite] site. Varsayılan olarak, hello hello etki alanı kullanıcı izni **yönetici** hello rolünde sağlanan uygulama.
* Bir etki alanı kullanıcısı hello hello build.cmd komut dosyası kullanarak bir uygulama oluşturabilirsiniz [azure-iot-remote-monitoring][lnk-rm-github-repo], [azure-iot-predictive-maintenance] [ lnk-pm-github-repo], veya [azure-IOT-bağlı-Fabrika] [ lnk-cf-github-repo] deposu. Ancak, hello varsayılan rol toohello etki alanı kullanıcısı verilir **salt okunur**, çünkü bir etki alanı kullanıcı izni tooassign rolleri yok.
* Merhaba AAD kiracısında başka bir kullanıcı bir uygulama oluşturduğunda hello etki alanı kullanıcısı hello atanan **ReadOnly** rolü bu uygulama için varsayılan.
* Bir etki alanı kullanıcısı uygulamalar için roller atayamazsınız; Bu nedenle bunlar olsa bile bir etki alanı kullanıcısı kullanıcıları veya bir uygulama için kullanıcıların rollerini ekleyemezsiniz.

### <a name="guest-user"></a>Konuk kullanıcı

AAD kiracısı başına çok sayıda Konuk kullanıcı olabilir. Konuk kullanıcılar hello AAD kiracısında sınırlı bir haklar kümesine sahiptir. Sonuç olarak, Konuk kullanıcılar hello AAD kiracısında önceden yapılandırılmış bir çözüm sağlayamaz.

Kullanıcılar ve roller aad'de hakkında daha fazla bilgi için kaynakları aşağıdaki hello bakın:

* [Azure AD'de kullanıcı oluşturma][lnk-create-edit-users]
* [Kullanıcıların tooapps atayın][lnk-assign-app-roles]

## <a name="azure-subscription-administrator-roles"></a>Azure abonelik yöneticisi rolleri

Hello Azure yönetici rolleri hello özelliği toomap bir Azure aboneliği tooan AD Kiracı denetler.

Merhaba makalede hello Azure yöneticisi rolleri hakkında daha fazla bilgi [nasıl tooadd veya Azure ortak yönetici, Hizmet Yöneticisi ve Hesap Yöneticisi değiştirme][lnk-admin-roles].

## <a name="application-roles"></a>Uygulama rolleri

Merhaba uygulama rolleri önceden yapılandırılmış çözümünüzdeki erişim toodevices denetler.

İki tanımlanmış rol ve sağlanan bir uygulamada bir örtük rol mevcuttur:

* **Yönetici:** yönetmek, cihazları kaldırın ve ayarlarını değiştirme tam denetim tooadd sahiptir.
* **Salt okunur:** aygıtlar, kurallar, Eylemler, işleri ve telemetri görüntüleyebilirsiniz.

Merhaba izinlerine hello tooeach rolünde bulabilirsiniz [RolePermissions.cs] [ lnk-resource-cs] kaynak dosyası.

### <a name="changing-application-roles-for-a-user"></a>Bir kullanıcının uygulama rollerini değiştirme

Aşağıdaki yordam toomake bir kullanıcı Active Directory'de yönetici önceden yapılandırılmış çözümünüzün hello kullanabilirsiniz.

Bir kullanıcı için bir AAD genel Yöneticisi toochange rolleri olması gerekir:

1. Toohello Git [Azure portal][lnk-portal].
2. Seçin **Azure Active Directory**.
3. Çözümünüzü sağlarken azureiotsuite.com üzerinde seçtiğiniz hello dizin kullandığınızdan emin olun. Aboneliğinizle ilişkili birden fazla dizine sahipseniz, bunları hesap adınızı hello sağ üst hello Portal'ı tıklatırsanız arasında geçiş yapabilirsiniz.
4. Tıklatın **kurumsal uygulamalar**, ardından **tüm uygulamaları**.
4. Göster **tüm uygulamaları** ile **herhangi** durumu. Ardından, önceden yapılandırılmış çözümünüz ada sahip bir uygulama arayın.
5. Merhaba, önceden yapılandırılmış çözümünüzün adıyla eşleşen hello uygulamanın adını tıklatın.
6. tıklatın **kullanıcılar ve gruplar**.
7. Tooswitch rolleri hello kullanıcıyı seçin.
8. ' I tıklatın **atamak** ve select hello rolü (gibi **yönetici**) tooassign toohello kullanıcı istediğiniz hello onay işaretine tıklayın.

## <a name="faq"></a>SSS

### <a name="im-a-service-administrator-and-id-like-toochange-hello-directory-mapping-between-my-subscription-and-a-specific-aad-tenant-how-do-i-complete-this-task"></a>Bir hizmet yöneticisiyim ve Aboneliğim ile belirli bir AAD kiracısı arasında toochange hello dizin eşlemesini istiyorum. Bu görevi nasıl tamamlamak?

1. Toohello Git [Klasik Azure portalı][lnk-classic-portal], tıklatın **ayarları** hello hello sol taraftaki Hizmet listesinde.
2. Toochange hello dizin eşlemesi için istediğiniz hello aboneliği seçin.
3. **Dizini Düzenle**’ye tıklayın.
4. Select hello **Directory** hello açılır toouse istersiniz. Merhaba İleri okuna tıklayın.
5. Merhaba dizin eşlemesini doğrulayın ve etkilenen ortak yöneticileri. Başka bir dizinden taşıyorsanız, hello özgün dizindeki tüm hello ortak Yöneticiler kaldırılır.

### <a name="im-a-domain-usermember-on-hello-aad-tenant-and-ive-created-a-preconfigured-solution-how-do-i-get-assigned-a-role-for-my-application"></a>Merhaba AAD kiracısı üzerinde etki alanı kullanıcısı/üyesi ben ve önceden yapılandırılmış bir çözüm oluşturduğunuzu düşünün. Uygulamam için bana nasıl rol atanır?

Genel yönetici toomake hello AAD genel bir yönetici, Kiracı ve rolleri toousers kendinize atayın isteyin. Alternatif olarak, bir genel yönetici tooassign isteyin, doğrudan bir rolü. Önceden yapılandırılmış çözümünüzün dağıtıldı toochange hello AAD kiracısı isterseniz hello sonraki soruya bakın.

### <a name="how-do-i-switch-hello-aad-tenant-my-remote-monitoring-preconfigured-solution-and-application-are-assigned-to"></a>My önceden yapılandırılmış Uzaktan izleme çözümü ve uygulama atandığını hello AAD kiracısına nasıl geçiş yapabilirim?

<https://github.com/Azure/azure-iot-remote-monitoring> adresinden bir bulut dağıtımını yeniden çalıştırabilir ve yeni oluşturulan bir AAD kiracısı ile yeniden dağıtabilirsiniz. Varsayılan olarak, bir AAD kiracısı oluşturduğunuzda, bir genel yönetici olduğu için tooadd kullanıcıların izinlere sahip ve toothose kullanıcı rolleri atayın.

1. Hello bir AAD dizini oluşturun [Azure portal][lnk-portal].
2. Çok Git<https://github.com/Azure/azure-iot-remote-monitoring>.
3. `build.cmd cloud [debug | release] {name of previously deployed remote monitoring solution}` komutunu çalıştırın (Örneğin, `build.cmd cloud debug myRMSolution`)
4. İstendiğinde, hello ayarlamak **tenantıd** toobe değerini önceki kiracınız yerine yeni oluşturduğunuz Kiracı.

### <a name="i-want-toochange-a-service-administrator-or-co-administrator-when-logged-in-with-an-organisational-account"></a>Bir Hizmet Yöneticisi veya bir hesabıyla oturum açtığımda ortak yöneticiyi toochange istiyorum

Merhaba destek makalesine bakın [değiştirme Hizmet Yöneticisi ve bir hesabıyla oturum açtığımda ortak yöneticiyi][lnk-service-admins].

### <a name="why-am-i-seeing-this-error-your-account-does-not-have-hello-proper-permissions-toocreate-a-solution-please-check-with-your-account-administrator-or-try-with-a-different-account"></a>Bu hatayı neden görüyorum? "Hesabınız hello uygun izinleri toocreate bir çözüm yok. Lütfen hesap yöneticinize başvurun veya farklı bir hesap ile deneyin."

Diyagram Kılavuzu izleyerek hello bakın:

![][img-flowchart]

> [!NOTE]
> Toosee hello hata devam ederse doğrulandıktan sonra hello AAD kiracısında genel yönetici ve hello abonelik ortak yönetici demektir, hesap yöneticinize hello kullanıcıyı kaldırabilir ve gerekli izinleri şu sırayla yeniden atamanız gerekir. İlk olarak, hello kullanıcı genel yönetici olarak ekleyin ve sonra hello Azure aboneliğinin ortak yönetici olarak kullanıcı ekleyin. Sorun devam ederse başvurun [Yardım ve Destek][lnk-help-support].

### <a name="why-am-i-seeing-this-error-when-i-have-an-azure-subscription-an-azure-subscription-is-required-toocreate-pre-configured-solutions-you-can-create-a-free-trial-account-in-just-a-couple-of-minutes"></a>Bir Azure aboneliğim varken bu hatayı neden görüyorum? "Azure aboneliği gerekli toocreate önceden yapılandırılmış çözümleri 'dir. Ücretsiz bir deneme hesabı yalnızca birkaç dakika içinde oluşturabileceğiniz."

Bir Azure aboneliğinizin olduğundan eminseniz aboneliğinizin eşleme hello Kiracı doğrulayın ve hello doğru Kiracı hello açılır listede seçildiğinden emin olun. Doğrulanacak hello Kiracı doğru istenen, diyagram önceki hello izleyin ve aboneliğiniz ile bu AAD kiracısının hello eşleme doğrulayın.

## <a name="next-steps"></a>Sonraki adımlar
IOT paketi hakkında öğrenme toocontinue bkz nasıl [önceden yapılandırılmış çözümü özelleştirme][lnk-customize].

[img-flowchart]: media/iot-suite-permissions/flowchart.png

[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-rm-github-repo]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-pm-github-repo]: https://github.com/Azure/azure-iot-predictive-maintenance
[lnk-cf-github-repo]: https://github.com/Azure/azure-iot-connected-factory
[lnk-aad-admin]: ../active-directory/active-directory-assign-admin-roles.md
[lnk-classic-portal]: https://manage.windowsazure.com/
[lnk-portal]: https://portal.azure.com/
[lnk-create-edit-users]: ../active-directory/active-directory-create-users.md
[lnk-assign-app-roles]: ../active-directory/active-directory-coreapps-assign-user-azure-portal.md
[lnk-service-admins]: https://azure.microsoft.com/support/changing-service-admin-and-co-admin/
[lnk-admin-roles]: ../billing/billing-add-change-azure-subscription-administrator.md
[lnk-resource-cs]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/DeviceAdministration/Web/Security/RolePermissions.cs
[lnk-help-support]: https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
