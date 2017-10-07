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
# <a name="how-toodeploy-hello-access-panel-extension-for-internet-explorer-using-group-policy"></a><span data-ttu-id="ade67-103">Nasıl tooDeploy hello erişim paneli uzantısı Grup İlkesi'ni kullanarak Internet Explorer için</span><span class="sxs-lookup"><span data-stu-id="ade67-103">How tooDeploy hello Access Panel Extension for Internet Explorer using Group Policy</span></span>
<span data-ttu-id="ade67-104">Bu öğretici nasıl toouse Grup İlkesi tooremotely yükleme hello erişim paneli uzantısı Internet Explorer için kullanıcılarınızın makinelerde gösterir.</span><span class="sxs-lookup"><span data-stu-id="ade67-104">This tutorial shows how toouse group policy tooremotely install hello Access Panel extension for Internet Explorer on your users' machines.</span></span> <span data-ttu-id="ade67-105">Bu uzantı toosign kullanılarak yapılandırılmış olan uygulamalara gereksinim duyan Internet Explorer kullanıcıların gereklidir [parola tabanlı çoklu oturum açma](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="ade67-105">This extension is required for Internet Explorer users who need toosign into apps that are configured using [password-based single sign-on](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).</span></span>

<span data-ttu-id="ade67-106">Yöneticiler'in bu uzantı hello dağıtımını otomatik hale getirmek önerilir.</span><span class="sxs-lookup"><span data-stu-id="ade67-106">It is recommended that admins automate hello deployment of this extension.</span></span> <span data-ttu-id="ade67-107">Aksi takdirde, kullanıcılar toodownload sahip ve hangi yatkın toouser hata ve yönetici izinleri gerektiren hello uzantısı kendileri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="ade67-107">Otherwise, users have toodownload and install hello extension themselves, which is prone toouser error and requires administrator permissions.</span></span> <span data-ttu-id="ade67-108">Bu öğretici, Grup İlkesi kullanarak yazılım dağıtımlarını otomatikleştirme bir yöntem kapsar.</span><span class="sxs-lookup"><span data-stu-id="ade67-108">This tutorial covers one method of automating software deployments by using group policy.</span></span> [<span data-ttu-id="ade67-109">Grup İlkesi hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="ade67-109">Learn more about group policy.</span></span>](https://technet.microsoft.com/windowsserver/bb310732.aspx)

<span data-ttu-id="ade67-110">Merhaba erişim paneli uzantısı için kullanılabilir de [Chrome](https://go.microsoft.com/fwLink/?LinkID=311859) ve [Firefox](https://go.microsoft.com/fwLink/?LinkID=626998), kümelesini yönetici izinleri tooinstall gerektirir.</span><span class="sxs-lookup"><span data-stu-id="ade67-110">hello Access Panel extension is also available for [Chrome](https://go.microsoft.com/fwLink/?LinkID=311859) and [Firefox](https://go.microsoft.com/fwLink/?LinkID=626998), neither of which require administrator permissions tooinstall.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ade67-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ade67-111">Prerequisites</span></span>
* <span data-ttu-id="ade67-112">Ayarlamış olduğunuz [Active Directory etki alanı Hizmetleri](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), ve kullanıcılarınızın makineler tooyour etki alanına katılmış.</span><span class="sxs-lookup"><span data-stu-id="ade67-112">You have set up [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), and you have joined your users' machines tooyour domain.</span></span>
* <span data-ttu-id="ade67-113">Merhaba "ayarlarını Düzenle" izni tooedit hello Grup İlkesi nesnesi (GPO) olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ade67-113">You must have hello "Edit settings" permission tooedit hello Group Policy Object (GPO).</span></span> <span data-ttu-id="ade67-114">Varsayılan olarak, güvenlik grupları aşağıdaki hello üyeleri bu izne sahip: etki alanı yöneticileri, kuruluş yöneticileri ve Group Policy Creator Owners.</span><span class="sxs-lookup"><span data-stu-id="ade67-114">By default, members of hello following security groups have this permission: Domain Administrators, Enterprise Administrators, and Group Policy Creator Owners.</span></span> [<span data-ttu-id="ade67-115">Daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="ade67-115">Learn more.</span></span>](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx)

## <a name="step-1-create-hello-distribution-point"></a><span data-ttu-id="ade67-116">1. adım: hello dağıtım noktası oluşturma</span><span class="sxs-lookup"><span data-stu-id="ade67-116">Step 1: Create hello Distribution Point</span></span>
<span data-ttu-id="ade67-117">İlk olarak, üzerinde tooremotely yükleme hello uzantısı istediğiniz hello makineler tarafından erişilebilen bir ağ konumu üzerinde hello Yükleyici paketi yerleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ade67-117">First, you must place hello installer package on a network location that can be accessed by hello machines that you wish tooremotely install hello extension on.</span></span> <span data-ttu-id="ade67-118">toodo Bu, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="ade67-118">toodo this, follow these steps:</span></span>

1. <span data-ttu-id="ade67-119">Toohello sunucuda yönetici olarak oturum açın</span><span class="sxs-lookup"><span data-stu-id="ade67-119">Log on toohello server as an administrator</span></span>
2. <span data-ttu-id="ade67-120">Merhaba, **Sunucu Yöneticisi'ni** penceresinde çok Git**dosya ve depolama hizmetleri**.</span><span class="sxs-lookup"><span data-stu-id="ade67-120">In hello **Server Manager** window, go too**Files and Storage Services**.</span></span>
   
    ![Açık dosyaları ve depolama hizmetleri](./media/active-directory-saas-ie-group-policy/files-services.png)
3. <span data-ttu-id="ade67-122">Toohello Git **paylaşımları** sekmesi. Ardından **görevleri** > **yeni paylaşım...**</span><span class="sxs-lookup"><span data-stu-id="ade67-122">Go toohello **Shares** tab. Then click **Tasks** > **New Share...**</span></span>
   
    ![Açık dosyaları ve depolama hizmetleri](./media/active-directory-saas-ie-group-policy/shares.png)
4. <span data-ttu-id="ade67-124">Tam hello **yeni paylaşım Sihirbazı'nı** ve kümesi izinleri tooensure kullanıcılarınızın makinelerden erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="ade67-124">Complete hello **New Share Wizard** and set permissions tooensure that it can be accessed from your users' machines.</span></span> [<span data-ttu-id="ade67-125">Paylaşımları hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="ade67-125">Learn more about shares.</span></span>](https://technet.microsoft.com/library/cc753175.aspx)
5. <span data-ttu-id="ade67-126">Microsoft Windows Installer paketini (.msi dosyası) aşağıdaki hello indirin: [erişim paneli Extension.msi](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access Panel Extension.msi)</span><span class="sxs-lookup"><span data-stu-id="ade67-126">Download hello following Microsoft Windows Installer package (.msi file): [Access Panel Extension.msi](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access Panel Extension.msi)</span></span>
6. <span data-ttu-id="ade67-127">Merhaba paylaşımında Hello Yükleyici paketi tooa istenen konuma kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="ade67-127">Copy hello installer package tooa desired location on hello share.</span></span>
   
    ![Merhaba .msi dosyası toohello paylaşımına kopyalayın.](./media/active-directory-saas-ie-group-policy/copy-package.png)
7. <span data-ttu-id="ade67-129">İstemci makineleriniz mümkün tooaccess hello Yükleyici paketi hello paylaşımından olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="ade67-129">Verify that your client machines are able tooaccess hello installer package from hello share.</span></span> 

## <a name="step-2-create-hello-group-policy-object"></a><span data-ttu-id="ade67-130">2. adım: hello Grup İlkesi nesnesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="ade67-130">Step 2: Create hello Group Policy Object</span></span>
1. <span data-ttu-id="ade67-131">Active Directory etki alanı Hizmetleri (AD DS) yüklemenizi barındıran toohello sunucusunda oturum açın.</span><span class="sxs-lookup"><span data-stu-id="ade67-131">Log on toohello server that hosts your Active Directory Domain Services (AD DS) installation.</span></span>
2. <span data-ttu-id="ade67-132">Hello Sunucu Yöneticisi, çok Git**Araçları** > **Grup İlkesi Yönetimi**.</span><span class="sxs-lookup"><span data-stu-id="ade67-132">In hello Server Manager, go too**Tools** > **Group Policy Management**.</span></span>
   
    ![TooTools Git > Grup İlkesi Yönetimi](./media/active-directory-saas-ie-group-policy/tools-gpm.png)
3. <span data-ttu-id="ade67-134">Merhaba sol bölmesinde hello **Grup İlkesi Yönetimi** penceresinde, kuruluş birimi (OU) hiyerarşinizi görüntülemek ve hangi kapsamda tooapply hello Grup İlkesi ister misiniz belirleyin.</span><span class="sxs-lookup"><span data-stu-id="ade67-134">In hello left pane of hello **Group Policy Management** window, view your Organizational Unit (OU) hierarchy and determine at which scope you would like tooapply hello group policy.</span></span> <span data-ttu-id="ade67-135">Örneğin, toopick küçük bir OU toodeploy tooa test etmek için birkaç kullanıcı karar verebilir veya bir üst düzey OU toodeploy tooyour tüm kuruluş çekme.</span><span class="sxs-lookup"><span data-stu-id="ade67-135">For instance, you may decide toopick a small OU toodeploy tooa few users for testing, or you may pick a top-level OU toodeploy tooyour entire organization.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="ade67-136">Toocreate ister veya kuruluş birimlerini (OU) düzenleme, geri toohello Sunucu Yöneticisi'ni geçin ve çok Git**Araçları** > **Active Directory Kullanıcıları ve Bilgisayarları**.</span><span class="sxs-lookup"><span data-stu-id="ade67-136">If you would like toocreate or edit your Organization Units (OUs), switch back toohello Server Manager and go too**Tools** > **Active Directory Users and Computers**.</span></span>
   > 
   > 
4. <span data-ttu-id="ade67-137">Bir OU seçtikten sonra sağ tıklatın ve seçin **bu etki alanında GPO oluştur ve buraya bağla...**</span><span class="sxs-lookup"><span data-stu-id="ade67-137">Once you have selected an OU, right-click it and select **Create a GPO in this domain, and Link it here...**</span></span>
   
    ![Yeni bir GPO oluşturun](./media/active-directory-saas-ie-group-policy/create-gpo.png)
5. <span data-ttu-id="ade67-139">Merhaba, **yeni GPO** komut isteminde, yeni Grup İlkesi nesnesi hello için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="ade67-139">In hello **New GPO** prompt, type in a name for hello new Group Policy Object.</span></span>
   
    ![Merhaba yeni GPO adı](./media/active-directory-saas-ie-group-policy/name-gpo.png)
6. <span data-ttu-id="ade67-141">Sağ hello oluşturulan ve seçin Grup İlkesi nesnesi **Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="ade67-141">Right-click hello Group Policy Object that you created, and select **Edit**.</span></span>
   
    ![Merhaba yeni GPO'yu düzenleyin](./media/active-directory-saas-ie-group-policy/edit-gpo.png)

## <a name="step-3-assign-hello-installation-package"></a><span data-ttu-id="ade67-143">3. adım: hello yükleme paketini atayın</span><span class="sxs-lookup"><span data-stu-id="ade67-143">Step 3: Assign hello Installation Package</span></span>
1. <span data-ttu-id="ade67-144">Temel toodeploy hello uzantısı isteyip istemediğinizi belirleyin **Bilgisayar Yapılandırması** veya **Kullanıcı Yapılandırması**.</span><span class="sxs-lookup"><span data-stu-id="ade67-144">Determine whether you would like toodeploy hello extension based on **Computer Configuration** or **User Configuration**.</span></span> <span data-ttu-id="ade67-145">Kullanırken [Bilgisayar Yapılandırması](https://technet.microsoft.com/library/cc736413%28v=ws.10%29.aspx), hello uzantısı kullanıcılar bağımsız olarak tooit üzerinde oturum hello bilgisayara yüklenir.</span><span class="sxs-lookup"><span data-stu-id="ade67-145">When using [computer configuration](https://technet.microsoft.com/library/cc736413%28v=ws.10%29.aspx), hello extension is installed on hello computer regardless of which users log on tooit.</span></span> <span data-ttu-id="ade67-146">İle [Kullanıcı Yapılandırması](https://technet.microsoft.com/library/cc781953%28v=ws.10%29.aspx), kullanıcılar bunları bağımsız olarak, hangi bilgisayarların oturum açmak için yüklü hello uzantısı.</span><span class="sxs-lookup"><span data-stu-id="ade67-146">With [user configuration](https://technet.microsoft.com/library/cc781953%28v=ws.10%29.aspx), users have hello extension installed for them regardless of which computers they log on to.</span></span>
2. <span data-ttu-id="ade67-147">Merhaba sol bölmesinde hello **Grup İlkesi Yönetimi Düzenleyicisi** penceresinde, hangi yapılandırma türüne bağlı olarak, seçtiğiniz klasör yolları aşağıdaki Merhaba, Git tooeither:</span><span class="sxs-lookup"><span data-stu-id="ade67-147">In hello left pane of hello **Group Policy Management Editor** window, go tooeither of hello following folder paths, depending on which type of configuration you chose:</span></span>
   
   * `Computer Configuration/Policies/Software Settings/`
   * `User Configuration/Policies/Software Settings/`
3. <span data-ttu-id="ade67-148">Sağ **yazılım yükleme**seçeneğini belirleyip **yeni** > **paket...**</span><span class="sxs-lookup"><span data-stu-id="ade67-148">Right-click **Software installation**, then select **New** > **Package...**</span></span>
   
    ![Yeni bir yazılım yükleme paketi oluşturun.](./media/active-directory-saas-ie-group-policy/new-package.png)
4. <span data-ttu-id="ade67-150">Hello Yükleyici paketi içeren paylaşılan bir klasöre gidin toohello [1. adım: hello dağıtım noktası oluşturma](#step-1-create-the-distribution-point)hello .msi dosyasını seçin ve tıklatın **açık**.</span><span class="sxs-lookup"><span data-stu-id="ade67-150">Go toohello shared folder that contains hello installer package from [Step 1: Create hello Distribution Point](#step-1-create-the-distribution-point), select hello .msi file, and click **Open**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="ade67-151">Merhaba paylaşımı bu aynı sunucuda bulunuyorsa, hello yerel dosya yolu yerine hello ağ dosya yolu hello .msi eriştiğiniz doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="ade67-151">If hello share is located on this same server, verify that you are accessing hello .msi through hello network file path, rather than hello local file path.</span></span>
   > 
   > 
   
    ![Merhaba paylaşılan klasörden Hello yükleme paketini seçin.](./media/active-directory-saas-ie-group-policy/select-package.png)
5. <span data-ttu-id="ade67-153">Merhaba, **Yazılımı Dağıt** komut istemi, select **atanan** dağıtım yönteminize için.</span><span class="sxs-lookup"><span data-stu-id="ade67-153">In hello **Deploy Software** prompt, select **Assigned** for your deployment method.</span></span> <span data-ttu-id="ade67-154">Daha sonra, **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ade67-154">Then click **OK**.</span></span>
   
    ![Atanan belirleyin ve ardından Tamam'ı tıklatın.](./media/active-directory-saas-ie-group-policy/deployment-method.png)

<span data-ttu-id="ade67-156">Merhaba uzantısı dağıtılan toohello seçtiğiniz OU sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="ade67-156">hello extension is now deployed toohello OU that you selected.</span></span> [<span data-ttu-id="ade67-157">Grup İlkesi Yazılım yükleme hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="ade67-157">Learn more about Group Policy Software Installation.</span></span>](https://technet.microsoft.com/library/cc738858%28v=ws.10%29.aspx)

## <a name="step-4-auto-enable-hello-extension-for-internet-explorer"></a><span data-ttu-id="ade67-158">4. adım: Otomatik etkinleştir hello için Internet Explorer uzantısı</span><span class="sxs-lookup"><span data-stu-id="ade67-158">Step 4: Auto-Enable hello Extension for Internet Explorer</span></span>
<span data-ttu-id="ade67-159">Buna ek olarak kullanılabilmesi için önce toorunning hello yükleyici, Internet Explorer için her uzantısını açıkça etkinleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="ade67-159">In addition toorunning hello installer, every extension for Internet Explorer must be explicitly enabled before it can be used.</span></span> <span data-ttu-id="ade67-160">Merhaba adımları tooenable altındaki Grup İlkesi kullanarak erişim paneli uzantısı hello:</span><span class="sxs-lookup"><span data-stu-id="ade67-160">Follow hello steps below tooenable hello Access Panel Extension using group policy:</span></span>

1. <span data-ttu-id="ade67-161">Merhaba, **Grup İlkesi Yönetimi Düzenleyicisi** penceresinde, hangi yapılandırma türüne bağlı olarak, seçtiğiniz içinde yolları aşağıdaki Merhaba, Git tooeither [3. adım: Ata hello yükleme paketini](#step-3-assign-the-installation-package):</span><span class="sxs-lookup"><span data-stu-id="ade67-161">In hello **Group Policy Management Editor** window, go tooeither of hello following paths, depending on which type of configuration you chose in [Step 3: Assign hello Installation Package](#step-3-assign-the-installation-package):</span></span>
   
   * `Computer Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/Security Features/Add-on Management`
   * `User Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/Security Features/Add-on Management`
2. <span data-ttu-id="ade67-162">Sağ **eklenti listesi**seçip **Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="ade67-162">Right-click **Add-on List**, and select **Edit**.</span></span>
    <span data-ttu-id="ade67-163">![Eklenti Listesi düzenleyin.](./media/active-directory-saas-ie-group-policy/edit-add-on-list.png)</span><span class="sxs-lookup"><span data-stu-id="ade67-163">![Edit Add-on List.](./media/active-directory-saas-ie-group-policy/edit-add-on-list.png)</span></span>
3. <span data-ttu-id="ade67-164">Merhaba, **eklenti listesi** penceresinde, seçin **etkin**.</span><span class="sxs-lookup"><span data-stu-id="ade67-164">In hello **Add-on List** window, select **Enabled**.</span></span> <span data-ttu-id="ade67-165">Ardından, hello altında **seçenekleri** 'yi tıklatın **göster... **.</span><span class="sxs-lookup"><span data-stu-id="ade67-165">Then, under hello **Options** section, click **Show...**.</span></span>
   
    ![Etkinleştir'i tıklatın ve ardından göster...](./media/active-directory-saas-ie-group-policy/edit-add-on-list-window.png)
4. <span data-ttu-id="ade67-167">Merhaba, **içeriğini göster** penceresinde hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="ade67-167">In hello **Show Contents** window, perform hello following steps:</span></span>
   
   1. <span data-ttu-id="ade67-168">Hello ilk sütun için (Merhaba **değer adı** alanı), kopyalama ve sınıf kimliği aşağıdaki hello yapıştırın:`{030E9A3F-7B18-4122-9A60-B87235E4F59E}`</span><span class="sxs-lookup"><span data-stu-id="ade67-168">For hello first column (hello **Value Name** field), copy and paste hello following Class ID: `{030E9A3F-7B18-4122-9A60-B87235E4F59E}`</span></span>
   2. <span data-ttu-id="ade67-169">Merhaba ikinci sütun için (Merhaba **değeri** alanı), aşağıdaki değeri hello yazın:`1`</span><span class="sxs-lookup"><span data-stu-id="ade67-169">For hello second column (hello **Value** field), type in hello following value: `1`</span></span>
   3. <span data-ttu-id="ade67-170">Tıklatın **Tamam** tooclose hello **içeriğini göster** penceresi.</span><span class="sxs-lookup"><span data-stu-id="ade67-170">Click **OK** tooclose hello **Show Contents** window.</span></span>
      
      ![Yukarıda belirtildiği gibi hello değerlerini doldurun.](./media/active-directory-saas-ie-group-policy/show-contents.png)
5. <span data-ttu-id="ade67-172">Tıklatın **Tamam** tooapply değişiklikleriniz ve Kapat hello **eklenti listesi** penceresi.</span><span class="sxs-lookup"><span data-stu-id="ade67-172">Click **OK** tooapply your changes and close hello **Add-on List** window.</span></span>

<span data-ttu-id="ade67-173">Merhaba uzantısı artık seçili hello hello makinelerin etkinleştirilmelidir OU.</span><span class="sxs-lookup"><span data-stu-id="ade67-173">hello extension should now be enabled for hello machines in hello selected OU.</span></span> [<span data-ttu-id="ade67-174">Grup İlkesi tooenable kullanma hakkında daha fazla bilgi edinin veya Internet Explorer eklentileri devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="ade67-174">Learn more about using group policy tooenable or disable Internet Explorer add-ons.</span></span>](https://technet.microsoft.com/library/dn454941.aspx)

## <a name="step-5-optional-disable-remember-password-prompt"></a><span data-ttu-id="ade67-175">Adım 5 (isteğe bağlı): "Parolayı anımsa" istemi devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="ade67-175">Step 5 (Optional): Disable "Remember Password" Prompt</span></span>
<span data-ttu-id="ade67-176">Soran "gibi toostore parolanızı musunuz?" Göster hello aşağıdaki Hello erişim paneli uzantısı kullanarak kullanıcıların oturum açma toowebsites, Internet Explorer zaman sor</span><span class="sxs-lookup"><span data-stu-id="ade67-176">When users sign-in toowebsites using hello Access Panel Extension, Internet Explorer may show hello following prompt asking "Would you like toostore your password?"</span></span>

![](./media/active-directory-saas-ie-group-policy/remember-password-prompt.png)

<span data-ttu-id="ade67-177">Bu istemi görmesini, kullanıcılarınızın tooprevent isterseniz tooprevent otomatik tamamlama hello adımları hatırlamaya parolalardan izleyin:</span><span class="sxs-lookup"><span data-stu-id="ade67-177">If you wish tooprevent your users from seeing this prompt, then follow hello steps below tooprevent auto-complete from remembering passwords:</span></span>

1. <span data-ttu-id="ade67-178">Merhaba, **Grup İlkesi Yönetimi Düzenleyicisi** penceresinde, aşağıda listelenen gidin toohello yolu.</span><span class="sxs-lookup"><span data-stu-id="ade67-178">In hello **Group Policy Management Editor** window, go toohello path listed below.</span></span> <span data-ttu-id="ade67-179">Bu yapılandırma ayarının yalnızca altında kullanılabilir **Kullanıcı Yapılandırması**.</span><span class="sxs-lookup"><span data-stu-id="ade67-179">This configuration setting is only available under **User Configuration**.</span></span>
   
   * `User Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/`
2. <span data-ttu-id="ade67-180">Adlı hello ayar Bul **hello otomatik tamamlama özelliğini kullanıcı adları ve parolalar formlarında için**.</span><span class="sxs-lookup"><span data-stu-id="ade67-180">Find hello setting named **Turn on hello auto-complete feature for user names and passwords on forms**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="ade67-181">Active Directory önceki sürümlerinde bu ayar hello ada sahip listesinde **otomatik tamamlama toosave parolaları izin verme**.</span><span class="sxs-lookup"><span data-stu-id="ade67-181">Previous versions of Active Directory may list this setting with hello name **Do not allow auto-complete toosave passwords**.</span></span> <span data-ttu-id="ade67-182">Bu ayar için Hello yapılandırma hello Bu öğreticide açıklanan ayarından farklıdır.</span><span class="sxs-lookup"><span data-stu-id="ade67-182">hello configuration for that setting differs from hello setting described in this tutorial.</span></span>
   > 
   > 
   
    ![Toolook bu kullanıcı ayarları altında unutmayın.](./media/active-directory-saas-ie-group-policy/disable-auto-complete.png)
3. <span data-ttu-id="ade67-184">Merhaba ayarı yukarıda sağ tıklatın ve seçin **Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="ade67-184">Right click hello above setting, and select **Edit**.</span></span>
4. <span data-ttu-id="ade67-185">Başlıklı hello pencerede **hello otomatik tamamlama özelliğini kullanıcı adları ve parolalar formlarında için**seçin **devre dışı**.</span><span class="sxs-lookup"><span data-stu-id="ade67-185">In hello window titled **Turn on hello auto-complete feature for user names and passwords on forms**, select **Disabled**.</span></span>
   
    ![Devre dışı bırak seçin](./media/active-directory-saas-ie-group-policy/disable-passwords.png)
5. <span data-ttu-id="ade67-187">Tıklatın **Tamam** tooapply bu değişiklikler ve Kapat hello penceresi.</span><span class="sxs-lookup"><span data-stu-id="ade67-187">Click **OK** tooapply these changes and close hello window.</span></span>

<span data-ttu-id="ade67-188">Kullanıcılar artık mümkün toostore kendi kimlik bilgileri olması veya otomatik tamamlama tooaccess daha önce depolanan kimlik bilgileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="ade67-188">Users will no longer be able toostore their credentials or use auto-complete tooaccess previously stored credentials.</span></span> <span data-ttu-id="ade67-189">Ancak, bu ilkeyi form alanları, arama alanları gibi diğer türleri için otomatik olarak tamamlamak kullanıcılar toocontinue toouse izin vermez.</span><span class="sxs-lookup"><span data-stu-id="ade67-189">However, this policy does allow users toocontinue toouse auto-complete for other types of form fields, such as search fields.</span></span>

> [!WARNING]
> <span data-ttu-id="ade67-190">Kullanıcılar bazı kimlik bilgileri toostore seçtikten sonra bu ilke etkinleştirildiğinde, bu ilkeyi olacak *değil* zaten depolanmış hello kimlik bilgilerini temizleyin.</span><span class="sxs-lookup"><span data-stu-id="ade67-190">If this policy is enabled after users have chosen toostore some credentials, this policy will *not* clear hello credentials that have already been stored.</span></span>
> 
> 

## <a name="step-6-testing-hello-deployment"></a><span data-ttu-id="ade67-191">6. adım: hello dağıtımı test etme</span><span class="sxs-lookup"><span data-stu-id="ade67-191">Step 6: Testing hello Deployment</span></span>
<span data-ttu-id="ade67-192">Merhaba uzantı dağıtımı başarılı olduysa tooverify hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="ade67-192">Follow hello steps below tooverify if hello extension deployment was successful:</span></span>

1. <span data-ttu-id="ade67-193">Kullanarak dağıttıysanız **Bilgisayar Yapılandırması**, toohello içinde seçili OU'ya ait bir istemci makine içine oturum [2. adım: hello Grup İlkesi nesnesi oluşturmak](#step-2-create-the-group-policy-object).</span><span class="sxs-lookup"><span data-stu-id="ade67-193">If you deployed using **Computer Configuration**, sign into a client machine that belongs toohello OU that you selected in [Step 2: Create hello Group Policy Object](#step-2-create-the-group-policy-object).</span></span> <span data-ttu-id="ade67-194">Kullanarak dağıttıysanız **Kullanıcı Yapılandırması**, toothat OU ait bir kullanıcı olarak içinde emin toosign olun.</span><span class="sxs-lookup"><span data-stu-id="ade67-194">If you deployed using **User Configuration**, make sure toosign in as a user who belongs toothat OU.</span></span>
2. <span data-ttu-id="ade67-195">Birkaç oturum sürebilir hello Grup İlkesi bileşenleri bu makineyle toofully güncelleştirme değiştirir.</span><span class="sxs-lookup"><span data-stu-id="ade67-195">It may take a couple sign ins for hello group policy changes toofully update with this machine.</span></span> <span data-ttu-id="ade67-196">tooforce hello güncelleştirme, açık bir **komut istemi** penceresini açın ve aşağıdaki komutu çalıştırın hello:`gpupdate /force`</span><span class="sxs-lookup"><span data-stu-id="ade67-196">tooforce hello update, open a **Command Prompt** window and run hello following command: `gpupdate /force`</span></span>
3. <span data-ttu-id="ade67-197">Merhaba makine hello yükleme tootake bağlantısı için yeniden başlatmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ade67-197">You must restart hello machine for hello installation tootake place.</span></span> <span data-ttu-id="ade67-198">Önyükleme hello uzantısı sırasında normal yükler önemli ölçüde daha uzun sürebilir.</span><span class="sxs-lookup"><span data-stu-id="ade67-198">Bootup may take significantly more time than usual while hello extension installs.</span></span>
4. <span data-ttu-id="ade67-199">Yeniden başlattıktan sonra açmak **Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="ade67-199">After restarting, open **Internet Explorer**.</span></span> <span data-ttu-id="ade67-200">Üzerinde Hello sağ üst köşesinde hello penceresinin tıklatın **Araçları** (Merhaba dişli simgesi) ve ardından **eklentileri yönetme**.</span><span class="sxs-lookup"><span data-stu-id="ade67-200">On hello upper-right corner of hello window, click **Tools** (hello gear icon), and then select **Manage add-ons**.</span></span>
   
    ![TooTools Git > Eklentileri Yönet](./media/active-directory-saas-ie-group-policy/manage-add-ons.png)
5. <span data-ttu-id="ade67-202">Merhaba, **Eklentileri Yönet** penceresi, o hello doğrulayın **erişim paneli uzantısı** yüklendi ve kendi **durum** çok ayarlamak**etkin**.</span><span class="sxs-lookup"><span data-stu-id="ade67-202">In hello **Manage Add-ons** window, verify that hello **Access Panel Extension** has been installed and that its **Status** has been set too**Enabled**.</span></span>
   
    ![Erişim paneli uzantısı yüklü ve etkin bu hello doğrulayın.](./media/active-directory-saas-ie-group-policy/verify-install.png)

## <a name="related-articles"></a><span data-ttu-id="ade67-204">İlgili makaleler</span><span class="sxs-lookup"><span data-stu-id="ade67-204">Related Articles</span></span>
* [<span data-ttu-id="ade67-205">Azure Active Directory'de Uygulama Yönetimi için Makale Dizini</span><span class="sxs-lookup"><span data-stu-id="ade67-205">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="ade67-206">Uygulama erişimi ve Azure Active Directory ile çoklu oturum açma</span><span class="sxs-lookup"><span data-stu-id="ade67-206">Application access and single sign-on with Azure Active Directory</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="ade67-207">Merhaba erişim paneli uzantısı Internet Explorer için sorun giderme</span><span class="sxs-lookup"><span data-stu-id="ade67-207">Troubleshooting hello Access Panel Extension for Internet Explorer</span></span>](active-directory-saas-ie-troubleshooting.md)

