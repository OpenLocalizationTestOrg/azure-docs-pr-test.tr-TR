---
title: "aaaDeploy Azure erişim paneli uzantısı için bir GPO kullanarak IE | Microsoft Docs"
description: "Toouse Grup nasıl hello My uygulamaları portal için ilke toodeploy hello Internet Explorer eklentisi."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 7c2d49c8-5be0-4e7e-abac-332f9dfda736
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: markvi
ms.reviewer: asteen
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 926f15950bbe81d2fbfe1b0b856470da40880d7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-hello-access-panel-extension-for-internet-explorer-using-group-policy"></a>Nasıl tooDeploy hello erişim paneli uzantısı Grup İlkesi'ni kullanarak Internet Explorer için
Bu öğretici nasıl toouse Grup İlkesi tooremotely yükleme hello erişim paneli uzantısı Internet Explorer için kullanıcılarınızın makinelerde gösterir. Bu uzantı toosign kullanılarak yapılandırılmış olan uygulamalara gereksinim duyan Internet Explorer kullanıcıların gereklidir [parola tabanlı çoklu oturum açma](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).

Yöneticiler'in bu uzantı hello dağıtımını otomatik hale getirmek önerilir. Aksi takdirde, kullanıcılar toodownload sahip ve hangi yatkın toouser hata ve yönetici izinleri gerektiren hello uzantısı kendileri yükleyin. Bu öğretici, Grup İlkesi kullanarak yazılım dağıtımlarını otomatikleştirme bir yöntem kapsar. [Grup İlkesi hakkında daha fazla bilgi edinin.](https://technet.microsoft.com/windowsserver/bb310732.aspx)

Merhaba erişim paneli uzantısı için kullanılabilir de [Chrome](https://go.microsoft.com/fwLink/?LinkID=311859) ve [Firefox](https://go.microsoft.com/fwLink/?LinkID=626998), kümelesini yönetici izinleri tooinstall gerektirir.

## <a name="prerequisites"></a>Ön koşullar
* Ayarlamış olduğunuz [Active Directory etki alanı Hizmetleri](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), ve kullanıcılarınızın makineler tooyour etki alanına katılmış.
* Merhaba "ayarlarını Düzenle" izni tooedit hello Grup İlkesi nesnesi (GPO) olması gerekir. Varsayılan olarak, güvenlik grupları aşağıdaki hello üyeleri bu izne sahip: etki alanı yöneticileri, kuruluş yöneticileri ve Group Policy Creator Owners. [Daha fazla bilgi edinin.](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx)

## <a name="step-1-create-hello-distribution-point"></a>1. adım: hello dağıtım noktası oluşturma
İlk olarak, üzerinde tooremotely yükleme hello uzantısı istediğiniz hello makineler tarafından erişilebilen bir ağ konumu üzerinde hello Yükleyici paketi yerleştirmeniz gerekir. toodo Bu, şu adımları izleyin:

1. Toohello sunucuda yönetici olarak oturum açın
2. Merhaba, **Sunucu Yöneticisi'ni** penceresinde çok Git**dosya ve depolama hizmetleri**.
   
    ![Açık dosyaları ve depolama hizmetleri](./media/active-directory-saas-ie-group-policy/files-services.png)
3. Toohello Git **paylaşımları** sekmesi. Ardından **görevleri** > **yeni paylaşım...**
   
    ![Açık dosyaları ve depolama hizmetleri](./media/active-directory-saas-ie-group-policy/shares.png)
4. Tam hello **yeni paylaşım Sihirbazı'nı** ve kümesi izinleri tooensure kullanıcılarınızın makinelerden erişilebilir. [Paylaşımları hakkında daha fazla bilgi edinin.](https://technet.microsoft.com/library/cc753175.aspx)
5. Microsoft Windows Installer paketini (.msi dosyası) aşağıdaki hello indirin: [erişim paneli Extension.msi](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access Panel Extension.msi)
6. Merhaba paylaşımında Hello Yükleyici paketi tooa istenen konuma kopyalayın.
   
    ![Merhaba .msi dosyası toohello paylaşımına kopyalayın.](./media/active-directory-saas-ie-group-policy/copy-package.png)
7. İstemci makineleriniz mümkün tooaccess hello Yükleyici paketi hello paylaşımından olduğunu doğrulayın. 

## <a name="step-2-create-hello-group-policy-object"></a>2. adım: hello Grup İlkesi nesnesi oluşturma
1. Active Directory etki alanı Hizmetleri (AD DS) yüklemenizi barındıran toohello sunucusunda oturum açın.
2. Hello Sunucu Yöneticisi, çok Git**Araçları** > **Grup İlkesi Yönetimi**.
   
    ![TooTools Git > Grup İlkesi Yönetimi](./media/active-directory-saas-ie-group-policy/tools-gpm.png)
3. Merhaba sol bölmesinde hello **Grup İlkesi Yönetimi** penceresinde, kuruluş birimi (OU) hiyerarşinizi görüntülemek ve hangi kapsamda tooapply hello Grup İlkesi ister misiniz belirleyin. Örneğin, toopick küçük bir OU toodeploy tooa test etmek için birkaç kullanıcı karar verebilir veya bir üst düzey OU toodeploy tooyour tüm kuruluş çekme.
   
   > [!NOTE]
   > Toocreate ister veya kuruluş birimlerini (OU) düzenleme, geri toohello Sunucu Yöneticisi'ni geçin ve çok Git**Araçları** > **Active Directory Kullanıcıları ve Bilgisayarları**.
   > 
   > 
4. Bir OU seçtikten sonra sağ tıklatın ve seçin **bu etki alanında GPO oluştur ve buraya bağla...**
   
    ![Yeni bir GPO oluşturun](./media/active-directory-saas-ie-group-policy/create-gpo.png)
5. Merhaba, **yeni GPO** komut isteminde, yeni Grup İlkesi nesnesi hello için bir ad yazın.
   
    ![Merhaba yeni GPO adı](./media/active-directory-saas-ie-group-policy/name-gpo.png)
6. Sağ hello oluşturulan ve seçin Grup İlkesi nesnesi **Düzenle**.
   
    ![Merhaba yeni GPO'yu düzenleyin](./media/active-directory-saas-ie-group-policy/edit-gpo.png)

## <a name="step-3-assign-hello-installation-package"></a>3. adım: hello yükleme paketini atayın
1. Temel toodeploy hello uzantısı isteyip istemediğinizi belirleyin **Bilgisayar Yapılandırması** veya **Kullanıcı Yapılandırması**. Kullanırken [Bilgisayar Yapılandırması](https://technet.microsoft.com/library/cc736413%28v=ws.10%29.aspx), hello uzantısı kullanıcılar bağımsız olarak tooit üzerinde oturum hello bilgisayara yüklenir. İle [Kullanıcı Yapılandırması](https://technet.microsoft.com/library/cc781953%28v=ws.10%29.aspx), kullanıcılar bunları bağımsız olarak, hangi bilgisayarların oturum açmak için yüklü hello uzantısı.
2. Merhaba sol bölmesinde hello **Grup İlkesi Yönetimi Düzenleyicisi** penceresinde, hangi yapılandırma türüne bağlı olarak, seçtiğiniz klasör yolları aşağıdaki Merhaba, Git tooeither:
   
   * `Computer Configuration/Policies/Software Settings/`
   * `User Configuration/Policies/Software Settings/`
3. Sağ **yazılım yükleme**seçeneğini belirleyip **yeni** > **paket...**
   
    ![Yeni bir yazılım yükleme paketi oluşturun.](./media/active-directory-saas-ie-group-policy/new-package.png)
4. Hello Yükleyici paketi içeren paylaşılan bir klasöre gidin toohello [1. adım: hello dağıtım noktası oluşturma](#step-1-create-the-distribution-point)hello .msi dosyasını seçin ve tıklatın **açık**.
   
   > [!IMPORTANT]
   > Merhaba paylaşımı bu aynı sunucuda bulunuyorsa, hello yerel dosya yolu yerine hello ağ dosya yolu hello .msi eriştiğiniz doğrulayın.
   > 
   > 
   
    ![Merhaba paylaşılan klasörden Hello yükleme paketini seçin.](./media/active-directory-saas-ie-group-policy/select-package.png)
5. Merhaba, **Yazılımı Dağıt** komut istemi, select **atanan** dağıtım yönteminize için. Daha sonra, **Tamam**'a tıklayın.
   
    ![Atanan belirleyin ve ardından Tamam'ı tıklatın.](./media/active-directory-saas-ie-group-policy/deployment-method.png)

Merhaba uzantısı dağıtılan toohello seçtiğiniz OU sunulmuştur. [Grup İlkesi Yazılım yükleme hakkında daha fazla bilgi edinin.](https://technet.microsoft.com/library/cc738858%28v=ws.10%29.aspx)

## <a name="step-4-auto-enable-hello-extension-for-internet-explorer"></a>4. adım: Otomatik etkinleştir hello için Internet Explorer uzantısı
Buna ek olarak kullanılabilmesi için önce toorunning hello yükleyici, Internet Explorer için her uzantısını açıkça etkinleştirilmelidir. Merhaba adımları tooenable altındaki Grup İlkesi kullanarak erişim paneli uzantısı hello:

1. Merhaba, **Grup İlkesi Yönetimi Düzenleyicisi** penceresinde, hangi yapılandırma türüne bağlı olarak, seçtiğiniz içinde yolları aşağıdaki Merhaba, Git tooeither [3. adım: Ata hello yükleme paketini](#step-3-assign-the-installation-package):
   
   * `Computer Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/Security Features/Add-on Management`
   * `User Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/Security Features/Add-on Management`
2. Sağ **eklenti listesi**seçip **Düzenle**.
    ![Eklenti Listesi düzenleyin.](./media/active-directory-saas-ie-group-policy/edit-add-on-list.png)
3. Merhaba, **eklenti listesi** penceresinde, seçin **etkin**. Ardından, hello altında **seçenekleri** 'yi tıklatın **göster... **.
   
    ![Etkinleştir'i tıklatın ve ardından göster...](./media/active-directory-saas-ie-group-policy/edit-add-on-list-window.png)
4. Merhaba, **içeriğini göster** penceresinde hello aşağıdaki adımları gerçekleştirin:
   
   1. Hello ilk sütun için (Merhaba **değer adı** alanı), kopyalama ve sınıf kimliği aşağıdaki hello yapıştırın:`{030E9A3F-7B18-4122-9A60-B87235E4F59E}`
   2. Merhaba ikinci sütun için (Merhaba **değeri** alanı), aşağıdaki değeri hello yazın:`1`
   3. Tıklatın **Tamam** tooclose hello **içeriğini göster** penceresi.
      
      ![Yukarıda belirtildiği gibi hello değerlerini doldurun.](./media/active-directory-saas-ie-group-policy/show-contents.png)
5. Tıklatın **Tamam** tooapply değişiklikleriniz ve Kapat hello **eklenti listesi** penceresi.

Merhaba uzantısı artık seçili hello hello makinelerin etkinleştirilmelidir OU. [Grup İlkesi tooenable kullanma hakkında daha fazla bilgi edinin veya Internet Explorer eklentileri devre dışı bırakın.](https://technet.microsoft.com/library/dn454941.aspx)

## <a name="step-5-optional-disable-remember-password-prompt"></a>Adım 5 (isteğe bağlı): "Parolayı anımsa" istemi devre dışı bırak
Soran "gibi toostore parolanızı musunuz?" Göster hello aşağıdaki Hello erişim paneli uzantısı kullanarak kullanıcıların oturum açma toowebsites, Internet Explorer zaman sor

![](./media/active-directory-saas-ie-group-policy/remember-password-prompt.png)

Bu istemi görmesini, kullanıcılarınızın tooprevent isterseniz tooprevent otomatik tamamlama hello adımları hatırlamaya parolalardan izleyin:

1. Merhaba, **Grup İlkesi Yönetimi Düzenleyicisi** penceresinde, aşağıda listelenen gidin toohello yolu. Bu yapılandırma ayarının yalnızca altında kullanılabilir **Kullanıcı Yapılandırması**.
   
   * `User Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/`
2. Adlı hello ayar Bul **hello otomatik tamamlama özelliğini kullanıcı adları ve parolalar formlarında için**.
   
   > [!NOTE]
   > Active Directory önceki sürümlerinde bu ayar hello ada sahip listesinde **otomatik tamamlama toosave parolaları izin verme**. Bu ayar için Hello yapılandırma hello Bu öğreticide açıklanan ayarından farklıdır.
   > 
   > 
   
    ![Toolook bu kullanıcı ayarları altında unutmayın.](./media/active-directory-saas-ie-group-policy/disable-auto-complete.png)
3. Merhaba ayarı yukarıda sağ tıklatın ve seçin **Düzenle**.
4. Başlıklı hello pencerede **hello otomatik tamamlama özelliğini kullanıcı adları ve parolalar formlarında için**seçin **devre dışı**.
   
    ![Devre dışı bırak seçin](./media/active-directory-saas-ie-group-policy/disable-passwords.png)
5. Tıklatın **Tamam** tooapply bu değişiklikler ve Kapat hello penceresi.

Kullanıcılar artık mümkün toostore kendi kimlik bilgileri olması veya otomatik tamamlama tooaccess daha önce depolanan kimlik bilgileri kullanın. Ancak, bu ilkeyi form alanları, arama alanları gibi diğer türleri için otomatik olarak tamamlamak kullanıcılar toocontinue toouse izin vermez.

> [!WARNING]
> Kullanıcılar bazı kimlik bilgileri toostore seçtikten sonra bu ilke etkinleştirildiğinde, bu ilkeyi olacak *değil* zaten depolanmış hello kimlik bilgilerini temizleyin.
> 
> 

## <a name="step-6-testing-hello-deployment"></a>6. adım: hello dağıtımı test etme
Merhaba uzantı dağıtımı başarılı olduysa tooverify hello adımları izleyin:

1. Kullanarak dağıttıysanız **Bilgisayar Yapılandırması**, toohello içinde seçili OU'ya ait bir istemci makine içine oturum [2. adım: hello Grup İlkesi nesnesi oluşturmak](#step-2-create-the-group-policy-object). Kullanarak dağıttıysanız **Kullanıcı Yapılandırması**, toothat OU ait bir kullanıcı olarak içinde emin toosign olun.
2. Birkaç oturum sürebilir hello Grup İlkesi bileşenleri bu makineyle toofully güncelleştirme değiştirir. tooforce hello güncelleştirme, açık bir **komut istemi** penceresini açın ve aşağıdaki komutu çalıştırın hello:`gpupdate /force`
3. Merhaba makine hello yükleme tootake bağlantısı için yeniden başlatmanız gerekir. Önyükleme hello uzantısı sırasında normal yükler önemli ölçüde daha uzun sürebilir.
4. Yeniden başlattıktan sonra açmak **Internet Explorer**. Üzerinde Hello sağ üst köşesinde hello penceresinin tıklatın **Araçları** (Merhaba dişli simgesi) ve ardından **eklentileri yönetme**.
   
    ![TooTools Git > Eklentileri Yönet](./media/active-directory-saas-ie-group-policy/manage-add-ons.png)
5. Merhaba, **Eklentileri Yönet** penceresi, o hello doğrulayın **erişim paneli uzantısı** yüklendi ve kendi **durum** çok ayarlamak**etkin**.
   
    ![Erişim paneli uzantısı yüklü ve etkin bu hello doğrulayın.](./media/active-directory-saas-ie-group-policy/verify-install.png)

## <a name="related-articles"></a>İlgili makaleler
* [Azure Active Directory'de Uygulama Yönetimi için Makale Dizini](active-directory-apps-index.md)
* [Uygulama erişimi ve Azure Active Directory ile çoklu oturum açma](active-directory-appssoaccess-whatis.md)
* [Merhaba erişim paneli uzantısı Internet Explorer için sorun giderme](active-directory-saas-ie-troubleshooting.md)

