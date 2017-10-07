---
title: "Azure Active Directory etki alanı Hizmetleri: Windows Server VM tooa yönetilen etki alanına Katıl | Microsoft Docs"
description: "Bir Windows Server sanal makine birleştirme tooAzure AD etki alanı Hizmetleri"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 74dbdb33-05db-4d47-badc-0d7bb6d0c8cb
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 1e85833b42bd51f3b3df067d6c5b69253459bec5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-windows-server-virtual-machine-tooa-managed-domain"></a>Windows Server sanal makine tooa yönetilen etki alanına Katıl
> [!div class="op_single_selector"]
> * [Klasik Azure portalı - Windows](active-directory-ds-admin-guide-join-windows-vm.md)
> * [PowerShell - Windows](active-directory-ds-admin-guide-join-windows-vm-classic-powershell.md)
>
>

<br>

Bu makalede nasıl toojoin bir sanal makine çalışan Windows Server 2012 R2 tooan Azure AD etki alanı Hizmetleri hello Klasik Azure portalı kullanarak bir etki alanı, yönetilen gösterilmektedir.

## <a name="step-1-create-hello-windows-server-virtual-machine"></a>1. adım: hello Windows Server sanal makine oluşturma
Hello özetlenen hello yönergeleri [Windows hello Klasik Azure portalı çalıştıran bir sanal makine oluşturma](../virtual-machines/windows/classic/tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) Öğreticisi. Bu yeni oluşturulan sanal makine tooensure birleştirilmiş toohello önemlidir Azure AD etki alanı Hizmetleri etkin aynı sanal ağ. Merhaba 'Hızlı Oluştur' seçeneğini, toojoin hello sanal makine tooa sanal ağ etkinleştirmez. Bu nedenle, toouse hello 'Galeri'den' seçeneği toocreate hello sanal makine gerekir.

Gerçekleştirme adımları toocreate içinde etkinleştirdiğiniz Azure AD etki alanı Hizmetleri Windows sanal makine birleştirilmiş toohello sanal ağ hello.

1. Merhaba hello komut çubuğunda hello pencerenin hello altındaki Klasik Azure portalı tıklatın **yeni**.
2. Altında **işlem**, tıklatın **sanal makine**, ardından **Galeri'den**.
3. Merhaba ilk ekran sağlar **bir görüntü seçin** sanal makineniz kullanılabilir görüntüleri hello listesinden için. Merhaba uygun görüntüyü seçin.

    ![Görüntüyü seçin](./media/active-directory-domain-services-admin-guide/create-windows-vm-select-image.png)
4. Merhaba ikinci ekranı, bir bilgisayar adı, boyutu ve yönetici kullanıcı adı ve parola çekme olanak tanır. Merhaba katmanı ve gerekli boyutu toorun uygulama ya da iş yükü kullanın. Burada çekme hello kullanıcı hello makinesinde yerel yönetici kullanıcı adıdır. Burada etki alanı kullanıcı hesabının kimlik bilgilerini girmeyin.

    ![Sanal makine yapılandırma](./media/active-directory-domain-services-admin-guide/create-windows-vm-config.png)
5. Merhaba üçüncü ekranı ağ, depolama ve kullanılabilirlik için kaynakları yapılandırmanızı sağlar. Hello Azure AD Etki Alanı Hizmetleri'nden etkin hello sanal ağ seçin olun **bölge/benzeşim grubu/sanal ağ** açılır. Belirtin bir **bulut hizmeti DNS adı** hello sanal makine için uygun şekilde.

    ![Sanal makine için sanal ağ seçin](./media/active-directory-domain-services-admin-guide/create-windows-vm-select-vnet.png)

   > [!WARNING]
   > Merhaba sanal makine toohello katılma emin olun, etkinleştirdiğiniz Azure AD etki alanı Hizmetleri aynı sanal ağ. Sonuç olarak, hello sanal makine 'hello etki alanı görmek' ve hello etki alanına katılım gibi görevleri gerçekleştirin. Farklı bir sanal ağda toocreate hello sanal makine seçerseniz, Azure AD Etki Alanı Hizmetleri'ni etkinleştirdikten bu sanal ağ toohello sanal bir ağa bağlayın.
   >
   >
6. Merhaba dördüncü ekran hello VM Aracısı yükleyip hello kullanılabilir uzantıları bazıları yapılandırmanıza izin verir.

    ![Bitti](./media/active-directory-domain-services-admin-guide/create-windows-vm-done.png)
7. Merhaba sanal makine oluşturulduktan sonra hello Klasik portal hello altında yeni sanal makine hello listeler **sanal makineleri** düğümü. Merhaba sanal makine ve bulut hizmeti başlatıldığında otomatik olarak ve durumlarını olarak listelenen **çalıştıran**.

    ![Sanal makine çalışır durumda](./media/active-directory-domain-services-admin-guide/create-windows-vm-running.png)

## <a name="step-2-connect-toohello-windows-server-virtual-machine-using-hello-local-administrator-account"></a>2. adım: hello yerel yönetici hesabı kullanarak toohello Windows Server sanal makine bağlanma
Şimdi, biz toohello yeni oluşturulan Windows Server sanal makine, toojoin bağlanmak, toohello etki alanı. Merhaba sanal makine, tooconnect tooit oluşturulurken belirtilen hello yerel yönetici kimlik bilgilerini kullan.

Aşağıdaki adımları tooconnect toohello sanal makine hello gerçekleştirin.

1. Çok gidin**sanal makineleri** hello Klasik Portalı'ndaki düğüm. 1. adımda oluşturduğunuz Hello sanal makineyi seçin ve tıklatın **Bağlan** hello hello pencerenin hello altındaki komut çubuğunda.

    ![TooWindows sanal makineye bağlanma](./media/active-directory-domain-services-admin-guide/connect-windows-vm.png)
2. Merhaba Klasik portal tooopen komut istemleri veya kullanılan tooconnect toohello sanal makine olduğu '.rdp' uzantılı bir dosyayı kaydedin. Yükleme tamamlandığında tooopen hello dosyasına tıklayın.
3. Merhaba oturum açma isteminde girin, **yerel yönetici kimlik bilgilerini**, hello sanal makine oluşturulurken belirtilen. Bu örnekte, örneğin, 'localhost\mahesh' kullandığımız.

Bu noktada, yerel yönetici kimlik bilgilerini kullanarak Windows sanal makine yeni oluşturulan toohello içinde günlüğe. Merhaba sonraki adıma toojoin hello sanal makine toohello etki alanıdır.

## <a name="step-3-join-hello-windows-server-virtual-machine-toohello-aad-ds-managed-domain"></a>3. adım: hello Windows Server sanal makine toohello AAD DS yönetilen etki alanına katılma
Aşağıdaki adımları toojoin hello Windows Server sanal makine toohello AAD DS yönetilen etki alanı hello gerçekleştirin.

1. Adım 2'de gösterildiği gibi toohello Windows Server bağlayın. Merhaba başlangıç ekranından açmak **Sunucu Yöneticisi'ni**.
2. Tıklatın **yerel sunucu** hello Sunucu Yöneticisi'ni penceresinin sol bölmesinde hello.

    ![Sanal makine üzerinde Sunucu Yöneticisi'ni başlatın](./media/active-directory-domain-services-admin-guide/join-domain-server-manager.png)
3. Tıklatın **çalışma grubu** hello altında **özellikleri** bölümü. Merhaba, **Sistem Özellikleri** özellik sayfası tıklatın **değişiklik** toojoin hello etki alanı.

    ![Sistem Özellikleri Sayfası](./media/active-directory-domain-services-admin-guide/join-domain-system-properties.png)
4. Hello Azure AD etki alanı Hizmetleri yönetilen etki alanınızın Hello etki alanı adı belirtin **etki alanı** textbox tıklatıp **Tamam**.

    ![Merhaba etki alanı toobe katılacağını belirtin](./media/active-directory-domain-services-admin-guide/join-domain-system-properties-specify-domain.png)
5. Kimlik bilgileri toojoin hello etki alanınızın istendiğinde tooenter şunlardır. Sağlamak sizin **kullanıcı ait toohello AAD DC Yöneticiler hello kimlik bilgilerini belirtin** grubu. Yalnızca bu grubun üyeleri ayrıcalıkları toojoin makineler toohello yönetilen etki alanı var.

    ![Etki alanına katılma kimlik bilgilerini belirtin](./media/active-directory-domain-services-admin-guide/join-domain-system-properties-specify-credentials.png)
6. Kimlik bilgileri yolları aşağıdaki hello birini belirtebilirsiniz:

   * UPN biçimi: Azure AD içinde yapılandırıldığı gibi hello UPN soneki hello kullanıcı hesabı belirtin. Bu örnekte, hello kullanıcı 'bob' hello UPN soneki eklenir 'bob@domainservicespreview.onmicrosoft.com'.
   * SAMAccountName biçimi: hello SAMAccountName biçiminde hello hesap adını belirtebilirsiniz. Bu örnekte, tooenter 'CONTOSO100\bob' hello kullanıcı 'bob' gerekir.

     > [!NOTE]
     > **Merhaba UPN biçiminde toospecify kimlik kullanmanızı öneririz.** Merhaba SAMAccountName Kullanıcı UPN önek aşırı uzun (örneğin, 'joereallylongnameuser') varsa otomatik oluşturulan olabilir. Birden çok kullanıcı aynı UPN önek (örneğin, ' bob') kiracınızdaki Azure AD, SAMAccountName biçimlerini otomatik hello hizmeti tarafından oluşturulan hello varsa. Bu durumlarda, hello UPN biçimini güvenilir bir şekilde kullanılabilir toohello etki alanındaki toolog.
     >
     >
7. Etki alanına katılma başarılı olduktan sonra toohello etki alanına davet eder iletiden hello bakın. Merhaba etki alanına katılma işlemi toocomplete için Hello sanal makineyi yeniden başlatın.

    ![Hoş Geldiniz toohello etki alanı](./media/active-directory-domain-services-admin-guide/join-domain-done.png)

## <a name="troubleshooting-domain-join"></a>Sorun giderme etki alanına katılma
### <a name="connectivity-issues"></a>Bağlantı sorunları
Merhaba sanal makine oluşturulamıyor toofind hello etki alanı varsa, aşağıdaki sorun giderme adımları toohello bakın:

* Bu hello sanal makineye bağlı toohello olduğundan emin olun aynı sanal ağ, etki alanı Hizmetleri'nde etkin. Yoksa, hello sanal makine oluşturulamıyor tooconnect toohello etki alanıdır ve bu nedenle yüklenemiyor toojoin hello etki alanıdır.
* Merhaba sanal makineye bağlı tooanother sanal ağ ise, bu sanal ağ etki alanı Hizmetleri'ni etkinleştirdikten bağlı toohello sanal ağ olduğundan emin olun.
* Tooping hello etki alanı hello yönetilen etki alanı (örneğin, ' ping contoso100.com') Hello etki alanı adını kullanarak deneyin. Yüklenemiyor toodo şekilde değilseniz, Azure AD Etki Alanı Hizmetleri'ni etkinleştirdiğiniz hello sayfasında görüntülenen hello etki alanı için tooping hello IP adresleri deneyin (örneğin, ' 10.0.0.4 ping'). Mümkün tooping hello IP adresi, ancak hello etki değilseniz, DNS hatalı yapılandırılmış olabilir. Merhaba IP adreslerini hello etki alanının hello sanal ağ için DNS sunucuları olarak yapılandırmış değil.
* Merhaba hello sanal makinedeki (' ipconfig/flushdns") DNS çözümleyicisi önbelleği temizleme deneyin.

Etki alanı kimlik bilgileri toojoin hello ister toohello iletişim kutusu alırsanız, bağlantı sorunları yok.

### <a name="credentials-related-issues"></a>Kimlik bilgileri ile ilgili sorunlar
Aşağıdaki adımları kimlik bilgileriyle konusunda sorun yaşıyoruz ve oluşturamıyor toojoin hello etki toohello bakın.

* Merhaba UPN biçiminde toospecify kimlik bilgilerini kullanmayı deneyin. Merhaba SAMAccountName hesabınız için otomatik-birden çok kullanıcı aynı UPN kiracınızda öneki veya UPN önek aşırı ise uzun hello ile varsa oluşturulması. Bu nedenle, hesabınız için hello SAMAccountName biçimi ne, beklediğiniz veya şirket içi etki alanınızda kullanmayı farklı olabilir.
* Toouse hello toohello 'AAD DC Yöneticiler' grup toojoin makineler toohello yönetilen etki alanına ait bir kullanıcı hesabının kimlik bilgilerini deneyin.
* Sahip olduğundan emin olun [parola eşitleme etkin](active-directory-ds-getting-started-password-sync.md) hello Başlarken Kılavuzu'nda gösterilen hello adımları uygun olarak.
* Azure AD içinde yapılandırıldığı gibi hello hello kullanıcının UPN'sini kullandığınızdan emin olun (örneğin, 'bob@domainservicespreview.onmicrosoft.com') içinde toosign.
* Parola Eşitleme toocomplete hello Başlarken Kılavuzu'nda belirtildiği için yeterince uzun beklenen olun.

## <a name="related-content"></a>İlgili İçerik
* [Azure AD etki alanı Hizmetleri - başlangıç kılavuzu](active-directory-ds-getting-started.md)
* [Azure AD Domain Services tarafından yönetilen etki alanını yönetme](active-directory-ds-admin-guide-administer-domain.md)
