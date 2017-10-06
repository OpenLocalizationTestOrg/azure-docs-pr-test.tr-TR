---
title: "Azure Active Directory etki alanı Hizmetleri: yönetilen bir etki alanını yönetme | Microsoft Docs"
description: "Azure Active Directory etki alanı Hizmetleri yönetilen etki alanlarını yönetme"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: d4fdbc75-3e6b-4e20-8494-5dcc3bf2220a
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 11acc79e06163e3193b1aa981f2cd28af812789d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="administer-an-azure-active-directory-domain-services-managed-domain"></a>Azure Active Directory Etki Alanı Hizmetleri tarafından yönetilen etki alanını yönetme
Bu makalede tooadminister bir Azure Active Directory (AD) etki alanı Hizmetleri etki alanı nasıl yönetileceğini gösterir.

## <a name="before-you-begin"></a>Başlamadan önce
Bu makalede listelenen tooperform hello görevleri, aşağıdakiler gerekir:

1. Geçerli bir **Azure aboneliği**.
2. Bir **Azure AD dizini** -ya da bir şirket içi dizin veya bir yalnızca bulut dizini ile eşitlenir.
3. **Azure AD etki alanı Hizmetleri** hello Azure AD dizini için etkinleştirilmesi gerekir. Bunu yapmadıysanız, hello özetlenen tüm hello görevleri izleyin [Getting Started guide](active-directory-ds-getting-started.md).
4. A **sanal makine etki alanına katılmış** , yönettiğiniz gelen hello Azure AD etki alanı Hizmetleri yönetilen etki alanı. Bu tür bir sanal makine yoksa, başlıklı hello makalesinde ana hatlarıyla tüm hello görevleri izleyin [Windows sanal makine tooa yönetilen etki alanına Katıl](active-directory-ds-admin-guide-join-windows-vm.md).
5. Hello kimlik bilgilerini gereken bir **kullanıcı hesabına ait toohello 'AAD DC Yöneticiler' grubu** dizininizde, tooadminister yönetilen etki alanınızı.

<br>

## <a name="administrative-tasks-you-can-perform-on-a-managed-domain"></a>Yönetilen bir etki alanı üzerinde gerçekleştirdiğiniz yönetim görevleri
Merhaba 'AAD DC Yöneticiler' grubunun üyeleri gibi tooperform görevler etkinleştirmek ayrıcalıklar hello yönetilen etki alanında verilir:

* Makineler toohello yönetilen etki alanına katılın.
* Merhaba yerleşik GPO hello 'AADDC bilgisayarlar' ve 'AADDC kullanıcılar' kapsayıcıları için hello yönetilen etki alanında yapılandırın.
* Merhaba yönetilen etki alanı DNS yönetme.
* Oluşturabilir ve özel kuruluş birimlerini (OU) hello yönetilen etki alanı üzerinde yönetebilir.
* Kazanç yönetimsel erişim toocomputers toohello yönetilen etki alanına katıldı.

## <a name="administrative-privileges-you-do-not-have-on-a-managed-domain"></a>Yönetilen bir etki alanında olmayan yönetici ayrıcalıkları
Merhaba etki alanı, düzeltme eki uygulama için izleme ve diğer yedeklemeleri gerçekleştirmek gibi etkinlikler dahil olmak üzere Microsoft tarafından yönetilir. Bu nedenle, hello etki alanı kilitli ve da ayrıcalıkları tooperform belirli yönetim görevlerinin hello etki alanında yok. Görevler, gerçekleştiremezsiniz bazı örnekleri aşağıda verilmiştir.

* Merhaba yönetilen etki alanı için etki alanı yöneticisi veya kuruluş yöneticisi ayrıcalıkları verilmez.
* Merhaba şema hello yönetilen etki alanının genişletemezsiniz.
* Uzak Masaüstü kullanarak hello yönetilen etki alanı için toodomain denetleyicileri bağlanamıyor.
* Etki alanı denetleyicileri toohello yönetilen etki alanı ekleyemezsiniz.

## <a name="task-1---provision-a-domain-joined-windows-server-virtual-machine-tooremotely-administer-hello-managed-domain"></a>Görev 1 - sağlama etki alanına katılmış Windows Server sanal makine tooremotely yönetmek hello yönetilen etki alanı
Azure AD etki alanı Hizmetleri yönetilen etki alanları hello Active Directory Yönetim Merkezi (ADAC) veya AD PowerShell gibi bilinen Active Directory yönetim araçları kullanılarak yönetilebilir. Kiracı yöneticileri ayrıcalıkları tooconnect toodomain denetleyicileri hello Uzak Masaüstü aracılığıyla yönetilen etki alanında yok. Bu nedenle, 'AAD DC Yöneticiler' grubu yönetebilirsiniz hello üyeleri etki alanları uzaktan yönetilen etki alanına katılmış toohello bir Windows Server/istemci bilgisayardan AD yönetim araçlarını kullanarak yönetilen. Windows Server ve istemci makinelerde hello Uzak Sunucu Yönetim Araçları (RSAT) isteğe bağlı özellik parçası toohello yönetilen etki alanına katılmış olarak AD Yönetim Araçları yüklenebilir.

Merhaba ilk tooset birleştirilmiş toohello yönetilen etki alanında Windows Server sanal makineyi bir adımdır. Yönergeler için başlıklı toohello makalesine başvurun [Windows Server sanal makine tooan Azure AD etki alanı Hizmetleri yönetilen etki alanına Katıl](active-directory-ds-admin-guide-join-windows-vm.md).

### <a name="remotely-administer-hello-managed-domain-from-a-client-computer-for-example-windows-10"></a>Merhaba yönetilen etki alanı bir istemci bilgisayardan (örneğin, Windows 10) uzaktan yönetme
Bu makalede kullanılan bir Windows Server sanal makine tooadminister hello AAD DS Hello yönergeleri etki alanı yönetilen. Ancak, ayrıca toouse bir Windows istemci (örneğin, Windows 10) sanal makine toodo şekilde tercih edebilirsiniz.

Yapabilecekleriniz [Uzak Sunucu Yönetim Araçları (RSAT) yüklemek](http://social.technet.microsoft.com/wiki/contents/articles/2202.remote-server-administration-tools-rsat-for-windows-client-and-windows-server-dsforum2wiki.aspx) TechNet'teki hello yönergeleri izleyerek bir Windows istemci sanal makine üzerinde.

## <a name="task-2---install-active-directory-administration-tools-on-hello-virtual-machine"></a>Görev 2 - hello sanal makineye yükleme Active Directory Yönetim Araçları
Adımları tooinstall hello Active Directory yönetim araçlarını hello etki alanına katılmış sanal makinede aşağıdaki hello gerçekleştirin. TechNet daha fazla bilgi için bkz: [yükleme ve uzak sunucu yönetim araçları kullanarak bilgi](https://technet.microsoft.com/library/hh831501.aspx).

1. Çok gidin**sanal makineleri** hello Klasik Azure portalı düğümünde. Görev 1'de oluşturduğunuz Hello sanal makineyi seçin ve tıklatın **Bağlan** hello hello pencerenin hello altındaki komut çubuğunda.

    ![TooWindows sanal makineye bağlanma](./media/active-directory-domain-services-admin-guide/connect-windows-vm.png)
2. Merhaba Klasik portal tooopen komut istemleri veya kullanılan tooconnect toohello sanal makine olduğu '.rdp' uzantılı bir dosyayı kaydedin. Yükleme tamamlandığında tooopen hello dosyasına tıklayın.
3. Merhaba oturum açma isteminde hello toohello 'AAD DC Yöneticiler' grubuna ait olan bir kullanıcı kimlik bilgilerini kullanın. Örneğin, kullandığımız 'bob@domainservicespreview.onmicrosoft.com' bizim durumda.
4. Merhaba başlangıç ekranından açmak **Sunucu Yöneticisi'ni**. Tıklatın **rol ve Özellik Ekle** hello merkezi bölmesinde hello Sunucu Yöneticisi penceresi.

    ![Sanal makine üzerinde Sunucu Yöneticisi'ni başlatın](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager.png)
5. Merhaba üzerinde **başlamadan önce** hello sayfasının **Ekle roller ve Özellikler Sihirbazı**, tıklatın **sonraki**.

    ![Başlamadan önce sayfası](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-begin.png)
6. Merhaba üzerinde **yükleme türü** sayfasında, hello bırakın **rol tabanlı veya özellik tabanlı yükleme** işaretli seçeneğini ve tıklayın **sonraki**.

    ![Yükleme türü sayfası](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-type.png)
7. Merhaba üzerinde **sunucu seçimi** sayfasında hello sunucu havuzundan hello geçerli sanal makine seçin ve tıklatın **sonraki**.

    ![Sunucu seçimi sayfası](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-server.png)
8. Merhaba üzerinde **sunucu rolleri** sayfasında, **sonraki**. Biz herhangi bir rol hello sunucusuna yüklemiyorsanız beri Biz bu sayfayı atla.
9. Merhaba üzerinde **özellikleri** tooexpand hello sayfasında, **Uzak Sunucu Yönetim Araçları** düğümü ve tooexpand hello ardından **Rol Yönetim Araçları** düğümü. Seçin **AD DS ve AD LDS Araçları** Rol Yönetim Araçları'nın hello listeden özelliği.

    ![Özellikler sayfası](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-ad-tools.png)
10. Merhaba üzerinde **onay** sayfasında, **yükleme** tooinstall hello AD ve AD LDS Araçları özelliği hello sanal makinede. Özellik yükleme işlemi başarıyla tamamlandığında tıklatın **Kapat** tooexit hello **rol ve Özellik Ekle** Sihirbazı.

    ![Onay sayfası](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-confirmation.png)

## <a name="task-3---connect-tooand-explore-hello-managed-domain"></a>Görev 3 - tooand bağlanmak hello yönetilen etki alanı keşfedin
Merhaba AD Yönetimsel Araçlar yüklediniz hello üzerinde sanal makine etki alanına katılmış, biz Bu araçlar tooexplore kullanın ve hello yönetilen etki alanını yönetme.

> [!NOTE]
> Toobe üyesi ihtiyacınız hello 'AAD DC yöneticileri' grubunun tooadminister hello yönetilen etki alanı.
>
>

1. Merhaba başlangıç ekranından tıklatın **Yönetimsel Araçlar**. Merhaba AD Yönetimsel Araçlar hello sanal makinede yüklü görmeniz gerekir.

    ![Sunucuda yüklü Yönetim Araçları](./media/active-directory-domain-services-admin-guide/install-rsat-admin-tools-installed.png)
2. Tıklatın **Active Directory Yönetim Merkezi**.

    ![Active Directory Yönetim Merkezi](./media/active-directory-domain-services-admin-guide/adac-overview.png)
3. tooexplore hello etki alanı, hello etki alanı adı hello sol bölmesinde (örneğin, ' contoso100.com')'yi tıklatın. 'AADDC bilgisayarlar' ve 'AADDC kullanıcılar' sırasıyla adlı iki kapsayıcı dikkat edin.

    ![ADAC - görünüm etki alanı](./media/active-directory-domain-services-admin-guide/adac-domain-view.png)
4. Adlı hello kapsayıcıya tıklatın **AADDC kullanıcılar** toosee tüm kullanıcılar ve gruplar toohello ait yönetilen etki alanı. Kullanıcı hesapları görmeniz gerekir ve grupları, Azure AD'den Kiracı bu kapsayıcıda Göster ayarlama. Bu örnekte dikkat edin, hello kullanıcı 'Kemal' adlı ve 'AAD DC Yöneticiler' adlı bir grup için bir kullanıcı hesabı, bu kapsayıcı içinde kullanılabilir.

    ![ADAC - etki alanı kullanıcıları](./media/active-directory-domain-services-admin-guide/adac-aaddc-users.png)
5. Adlı hello kapsayıcıya tıklatın **AADDC bilgisayarlar** toosee hello bilgisayarlar toothis yönetilen etki alanına katılmış. Merhaba geçerli sanal birleştirilmiş toohello etki alanı olan makine için bir giriş görmeniz gerekir. Tüm bilgisayarlar için bilgisayar hesaplarını toohello Azure AD etki alanı Hizmetleri yönetilen etki alanı, bu 'AADDC bilgisayarlar' kapsayıcısında depolanır katıldı.

    ![ADAC - etki alanına katılmış bilgisayarlar](./media/active-directory-domain-services-admin-guide/adac-aaddc-computers.png)

<br>

## <a name="related-content"></a>İlgili İçerik
* [Azure AD etki alanı Hizmetleri - başlangıç kılavuzu](active-directory-ds-getting-started.md)
* [Windows Server sanal makine tooan Azure AD etki alanı Hizmetleri yönetilen etki alanına Katıl](active-directory-ds-admin-guide-join-windows-vm.md)
* [Uzak Sunucu Yönetim Araçları dağıtma](https://technet.microsoft.com/library/hh831501.aspx)
