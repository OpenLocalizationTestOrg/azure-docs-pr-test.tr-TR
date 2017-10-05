---
title: "Azure erişim paneli uzantısı için bir GPO kullanarak IE dağıtma | Microsoft Docs"
description: "My uygulamaları portal için Internet Explorer eklentisi dağıtmak için Grup İlkesi kullanma"
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
ms.openlocfilehash: b402ae326ab34ec71ad9de966e22be00045fee3e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-deploy-the-access-panel-extension-for-internet-explorer-using-group-policy"></a><span data-ttu-id="dca25-103">Grup İlkesi'ni kullanarak Internet Explorer için erişim paneli uzantısı dağıtma</span><span class="sxs-lookup"><span data-stu-id="dca25-103">How to Deploy the Access Panel Extension for Internet Explorer using Group Policy</span></span>
<span data-ttu-id="dca25-104">Bu öğretici, Grup İlkesi uzaktan erişim paneli uzantısı Internet Explorer için kullanıcılarınızın makinelere yüklemeniz için nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="dca25-104">This tutorial shows how to use group policy to remotely install the Access Panel extension for Internet Explorer on your users' machines.</span></span> <span data-ttu-id="dca25-105">Bu uzantı kullanılarak yapılandırılmış olan uygulamalarda oturum açmak için gereken Internet Explorer kullanıcılar için gerekli [parola tabanlı çoklu oturum açma](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="dca25-105">This extension is required for Internet Explorer users who need to sign into apps that are configured using [password-based single sign-on](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).</span></span>

<span data-ttu-id="dca25-106">Yöneticiler'in bu uzantı dağıtımını otomatik hale getirmek önerilir.</span><span class="sxs-lookup"><span data-stu-id="dca25-106">It is recommended that admins automate the deployment of this extension.</span></span> <span data-ttu-id="dca25-107">Aksi takdirde, kullanıcılar yükleyip uzantısı kendileri hangi kullanıcı hataya ve yönetici izinlerine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="dca25-107">Otherwise, users have to download and install the extension themselves, which is prone to user error and requires administrator permissions.</span></span> <span data-ttu-id="dca25-108">Bu öğretici, Grup İlkesi kullanarak yazılım dağıtımlarını otomatikleştirme bir yöntem kapsar.</span><span class="sxs-lookup"><span data-stu-id="dca25-108">This tutorial covers one method of automating software deployments by using group policy.</span></span> [<span data-ttu-id="dca25-109">Grup İlkesi hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="dca25-109">Learn more about group policy.</span></span>](https://technet.microsoft.com/windowsserver/bb310732.aspx)

<span data-ttu-id="dca25-110">Erişim paneli uzantısı da kullanılabilir [Chrome](https://go.microsoft.com/fwLink/?LinkID=311859) ve [Firefox](https://go.microsoft.com/fwLink/?LinkID=626998), kümelesini yüklemek için yönetici izinleri gerektirir.</span><span class="sxs-lookup"><span data-stu-id="dca25-110">The Access Panel extension is also available for [Chrome](https://go.microsoft.com/fwLink/?LinkID=311859) and [Firefox](https://go.microsoft.com/fwLink/?LinkID=626998), neither of which require administrator permissions to install.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dca25-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="dca25-111">Prerequisites</span></span>
* <span data-ttu-id="dca25-112">Ayarlamış olduğunuz [Active Directory etki alanı Hizmetleri](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), ve kullanıcılarınızın makineler, etki alanına.</span><span class="sxs-lookup"><span data-stu-id="dca25-112">You have set up [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), and you have joined your users' machines to your domain.</span></span>
* <span data-ttu-id="dca25-113">Grup İlkesi nesnesi (GPO) düzenlemek için "Ayarları düzenleme" izni olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="dca25-113">You must have the "Edit settings" permission to edit the Group Policy Object (GPO).</span></span> <span data-ttu-id="dca25-114">Varsayılan olarak, aşağıdaki güvenlik gruplarının üyeleri bu izne sahip: etki alanı yöneticileri, kuruluş yöneticileri ve Group Policy Creator Owners.</span><span class="sxs-lookup"><span data-stu-id="dca25-114">By default, members of the following security groups have this permission: Domain Administrators, Enterprise Administrators, and Group Policy Creator Owners.</span></span> [<span data-ttu-id="dca25-115">Daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="dca25-115">Learn more.</span></span>](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx)

## <a name="step-1-create-the-distribution-point"></a><span data-ttu-id="dca25-116">1. adım: dağıtım noktası oluşturma</span><span class="sxs-lookup"><span data-stu-id="dca25-116">Step 1: Create the Distribution Point</span></span>
<span data-ttu-id="dca25-117">İlk olarak, uzantı uzaktan yüklemek istediğiniz makineler tarafından erişilebilir bir ağ konumu üzerinde yükleyici paketi yerleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="dca25-117">First, you must place the installer package on a network location that can be accessed by the machines that you wish to remotely install the extension on.</span></span> <span data-ttu-id="dca25-118">Bunu yapmak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="dca25-118">To do this, follow these steps:</span></span>

1. <span data-ttu-id="dca25-119">Sunucuya bir yönetici olarak oturum açın</span><span class="sxs-lookup"><span data-stu-id="dca25-119">Log on to the server as an administrator</span></span>
2. <span data-ttu-id="dca25-120">İçinde **Sunucu Yöneticisi'ni** penceresinde, Git **dosya ve depolama hizmetleri**.</span><span class="sxs-lookup"><span data-stu-id="dca25-120">In the **Server Manager** window, go to **Files and Storage Services**.</span></span>
   
    ![Açık dosyaları ve depolama hizmetleri](./media/active-directory-saas-ie-group-policy/files-services.png)
3. <span data-ttu-id="dca25-122">Git **paylaşımları** sekmesi. Ardından **görevleri** > **yeni paylaşım...**</span><span class="sxs-lookup"><span data-stu-id="dca25-122">Go to the **Shares** tab. Then click **Tasks** > **New Share...**</span></span>
   
    ![Açık dosyaları ve depolama hizmetleri](./media/active-directory-saas-ie-group-policy/shares.png)
4. <span data-ttu-id="dca25-124">Tamamlamak **yeni paylaşım Sihirbazı'nı** ve kullanıcılarınızın makinelerden erişilebildiğinden emin olmak için izinleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="dca25-124">Complete the **New Share Wizard** and set permissions to ensure that it can be accessed from your users' machines.</span></span> [<span data-ttu-id="dca25-125">Paylaşımları hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="dca25-125">Learn more about shares.</span></span>](https://technet.microsoft.com/library/cc753175.aspx)
5. <span data-ttu-id="dca25-126">Aşağıdaki Microsoft Windows Installer paketini (.msi dosyası) indirin: [erişim paneli Extension.msi](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access Panel Extension.msi)</span><span class="sxs-lookup"><span data-stu-id="dca25-126">Download the following Microsoft Windows Installer package (.msi file): [Access Panel Extension.msi](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access Panel Extension.msi)</span></span>
6. <span data-ttu-id="dca25-127">Yükleyici paketi paylaşımdaki istediğiniz bir konuma kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="dca25-127">Copy the installer package to a desired location on the share.</span></span>
   
    ![.Msi dosya paylaşımına kopyalayın.](./media/active-directory-saas-ie-group-policy/copy-package.png)
7. <span data-ttu-id="dca25-129">İstemci makineleriniz Yükleyici paketi paylaşımından erişebilir olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="dca25-129">Verify that your client machines are able to access the installer package from the share.</span></span> 

## <a name="step-2-create-the-group-policy-object"></a><span data-ttu-id="dca25-130">Adım 2: Grup İlkesi nesnesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="dca25-130">Step 2: Create the Group Policy Object</span></span>
1. <span data-ttu-id="dca25-131">Active Directory etki alanı Hizmetleri (AD DS) yüklemenizi barındıran sunucu için oturum açın.</span><span class="sxs-lookup"><span data-stu-id="dca25-131">Log on to the server that hosts your Active Directory Domain Services (AD DS) installation.</span></span>
2. <span data-ttu-id="dca25-132">Sunucu Yöneticisi'nde Git **Araçları** > **Grup İlkesi Yönetimi**.</span><span class="sxs-lookup"><span data-stu-id="dca25-132">In the Server Manager, go to **Tools** > **Group Policy Management**.</span></span>
   
    ![İçin Araçlar > Grup İlkesi Yönetimi](./media/active-directory-saas-ie-group-policy/tools-gpm.png)
3. <span data-ttu-id="dca25-134">Sol bölmesinde **Grup İlkesi Yönetimi** penceresinde, kuruluş birimi (OU) hiyerarşinizi görüntülemek ve hangi kapsamda grup ilkesini uygulamak istediğiniz belirleyin.</span><span class="sxs-lookup"><span data-stu-id="dca25-134">In the left pane of the **Group Policy Management** window, view your Organizational Unit (OU) hierarchy and determine at which scope you would like to apply the group policy.</span></span> <span data-ttu-id="dca25-135">Örneğin, test etmek için birkaç kullanıcılara dağıtmak için küçük bir OU çekme karar verebilir veya kuruluşunuzun tümüne dağıtmak için en üst düzey bir OU çekme.</span><span class="sxs-lookup"><span data-stu-id="dca25-135">For instance, you may decide to pick a small OU to deploy to a few users for testing, or you may pick a top-level OU to deploy to your entire organization.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="dca25-136">İsterseniz oluşturma veya kuruluş birimlerini (OU) düzenleme, Sunucu Yöneticisi geçiş ve Git **Araçları** > **Active Directory Kullanıcıları ve Bilgisayarları**.</span><span class="sxs-lookup"><span data-stu-id="dca25-136">If you would like to create or edit your Organization Units (OUs), switch back to the Server Manager and go to **Tools** > **Active Directory Users and Computers**.</span></span>
   > 
   > 
4. <span data-ttu-id="dca25-137">Bir OU seçtikten sonra sağ tıklatın ve seçin **bu etki alanında GPO oluştur ve buraya bağla...**</span><span class="sxs-lookup"><span data-stu-id="dca25-137">Once you have selected an OU, right-click it and select **Create a GPO in this domain, and Link it here...**</span></span>
   
    ![Yeni bir GPO oluşturun](./media/active-directory-saas-ie-group-policy/create-gpo.png)
5. <span data-ttu-id="dca25-139">İçinde **yeni GPO** istemi, yeni Grup İlkesi nesnesi için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="dca25-139">In the **New GPO** prompt, type in a name for the new Group Policy Object.</span></span>
   
    ![Yeni GPO adı](./media/active-directory-saas-ie-group-policy/name-gpo.png)
6. <span data-ttu-id="dca25-141">Oluşturulan ve seçin Grup İlkesi nesnesi sağ **Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="dca25-141">Right-click the Group Policy Object that you created, and select **Edit**.</span></span>
   
    ![Yeni GPO düzenleme](./media/active-directory-saas-ie-group-policy/edit-gpo.png)

## <a name="step-3-assign-the-installation-package"></a><span data-ttu-id="dca25-143">3. adım: yükleme paketini atama</span><span class="sxs-lookup"><span data-stu-id="dca25-143">Step 3: Assign the Installation Package</span></span>
1. <span data-ttu-id="dca25-144">Temel uzantısı dağıtmak isteyip istemediğinizi belirleyin **Bilgisayar Yapılandırması** veya **Kullanıcı Yapılandırması**.</span><span class="sxs-lookup"><span data-stu-id="dca25-144">Determine whether you would like to deploy the extension based on **Computer Configuration** or **User Configuration**.</span></span> <span data-ttu-id="dca25-145">Kullanırken [Bilgisayar Yapılandırması](https://technet.microsoft.com/library/cc736413%28v=ws.10%29.aspx), uzantı hangi kullanıcıların oturum açın, bağımsız olarak bilgisayara yüklenir.</span><span class="sxs-lookup"><span data-stu-id="dca25-145">When using [computer configuration](https://technet.microsoft.com/library/cc736413%28v=ws.10%29.aspx), the extension is installed on the computer regardless of which users log on to it.</span></span> <span data-ttu-id="dca25-146">İle [Kullanıcı Yapılandırması](https://technet.microsoft.com/library/cc781953%28v=ws.10%29.aspx), kullanıcılar bunları bağımsız olarak, hangi bilgisayarların oturum açmak için yüklü uzantısı.</span><span class="sxs-lookup"><span data-stu-id="dca25-146">With [user configuration](https://technet.microsoft.com/library/cc781953%28v=ws.10%29.aspx), users have the extension installed for them regardless of which computers they log on to.</span></span>
2. <span data-ttu-id="dca25-147">Sol bölmesinde **Grup İlkesi Yönetimi Düzenleyicisi** penceresinde, seçtiğiniz hangi yapılandırma türüne bağlı olarak aşağıdaki klasör yollarını birini gidin:</span><span class="sxs-lookup"><span data-stu-id="dca25-147">In the left pane of the **Group Policy Management Editor** window, go to either of the following folder paths, depending on which type of configuration you chose:</span></span>
   
   * `Computer Configuration/Policies/Software Settings/`
   * `User Configuration/Policies/Software Settings/`
3. <span data-ttu-id="dca25-148">Sağ **yazılım yükleme**seçeneğini belirleyip **yeni** > **paket...**</span><span class="sxs-lookup"><span data-stu-id="dca25-148">Right-click **Software installation**, then select **New** > **Package...**</span></span>
   
    ![Yeni bir yazılım yükleme paketi oluşturun.](./media/active-directory-saas-ie-group-policy/new-package.png)
4. <span data-ttu-id="dca25-150">Yükleyici paketinden içeren paylaşılan klasöre gidin [1. adım: dağıtım noktası oluşturma](#step-1-create-the-distribution-point).msi dosyasını seçin ve tıklatın **açık**.</span><span class="sxs-lookup"><span data-stu-id="dca25-150">Go to the shared folder that contains the installer package from [Step 1: Create the Distribution Point](#step-1-create-the-distribution-point), select the .msi file, and click **Open**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="dca25-151">Paylaşım bu aynı sunucuda bulunuyorsa, yerel dosya yolu yerine ağ dosya yolu .msi eriştiğiniz doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="dca25-151">If the share is located on this same server, verify that you are accessing the .msi through the network file path, rather than the local file path.</span></span>
   > 
   > 
   
    ![Paylaşılan klasörden yükleme paketini seçin.](./media/active-directory-saas-ie-group-policy/select-package.png)
5. <span data-ttu-id="dca25-153">İçinde **Yazılımı Dağıt** komut istemi, select **atanan** dağıtım yönteminize için.</span><span class="sxs-lookup"><span data-stu-id="dca25-153">In the **Deploy Software** prompt, select **Assigned** for your deployment method.</span></span> <span data-ttu-id="dca25-154">Daha sonra, **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="dca25-154">Then click **OK**.</span></span>
   
    ![Atanan belirleyin ve ardından Tamam'ı tıklatın.](./media/active-directory-saas-ie-group-policy/deployment-method.png)

<span data-ttu-id="dca25-156">Uzantı, seçili OU'ya şimdi dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="dca25-156">The extension is now deployed to the OU that you selected.</span></span> [<span data-ttu-id="dca25-157">Grup İlkesi Yazılım yükleme hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="dca25-157">Learn more about Group Policy Software Installation.</span></span>](https://technet.microsoft.com/library/cc738858%28v=ws.10%29.aspx)

## <a name="step-4-auto-enable-the-extension-for-internet-explorer"></a><span data-ttu-id="dca25-158">4. adım: Otomatik etkinleştirmek için Internet Explorer uzantısı</span><span class="sxs-lookup"><span data-stu-id="dca25-158">Step 4: Auto-Enable the Extension for Internet Explorer</span></span>
<span data-ttu-id="dca25-159">Kullanılabilmesi için önce yükleyicinin çalıştırmanın yanı sıra, her uzantısını Internet Explorer için açıkça etkinleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="dca25-159">In addition to running the installer, every extension for Internet Explorer must be explicitly enabled before it can be used.</span></span> <span data-ttu-id="dca25-160">Grup İlkesi kullanarak erişim paneli uzantısı etkinleştirmek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="dca25-160">Follow the steps below to enable the Access Panel Extension using group policy:</span></span>

1. <span data-ttu-id="dca25-161">İçinde **Grup İlkesi Yönetimi Düzenleyicisi** penceresinde, hangi yapılandırma türüne bağlı olarak, seçtiğiniz içinde aşağıdaki yollardan birini gidin [adım 3: yükleme paketini atamak](#step-3-assign-the-installation-package):</span><span class="sxs-lookup"><span data-stu-id="dca25-161">In the **Group Policy Management Editor** window, go to either of the following paths, depending on which type of configuration you chose in [Step 3: Assign the Installation Package](#step-3-assign-the-installation-package):</span></span>
   
   * `Computer Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/Security Features/Add-on Management`
   * `User Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/Security Features/Add-on Management`
2. <span data-ttu-id="dca25-162">Sağ **eklenti listesi**seçip **Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="dca25-162">Right-click **Add-on List**, and select **Edit**.</span></span>
    <span data-ttu-id="dca25-163">![Eklenti Listesi düzenleyin.](./media/active-directory-saas-ie-group-policy/edit-add-on-list.png)</span><span class="sxs-lookup"><span data-stu-id="dca25-163">![Edit Add-on List.](./media/active-directory-saas-ie-group-policy/edit-add-on-list.png)</span></span>
3. <span data-ttu-id="dca25-164">İçinde **eklenti listesi** penceresinde, seçin **etkin**.</span><span class="sxs-lookup"><span data-stu-id="dca25-164">In the **Add-on List** window, select **Enabled**.</span></span> <span data-ttu-id="dca25-165">Ardından, altında **seçenekleri** 'yi tıklatın **göster...** .</span><span class="sxs-lookup"><span data-stu-id="dca25-165">Then, under the **Options** section, click **Show...**.</span></span>
   
    ![Etkinleştir'i tıklatın ve ardından göster...](./media/active-directory-saas-ie-group-policy/edit-add-on-list-window.png)
4. <span data-ttu-id="dca25-167">İçinde **içeriğini göster** penceresinde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="dca25-167">In the **Show Contents** window, perform the following steps:</span></span>
   
   1. <span data-ttu-id="dca25-168">İlk sütun için ( **değer adı** alanı), kopyalama ve yapıştırma aşağıdaki sınıf kimliği:`{030E9A3F-7B18-4122-9A60-B87235E4F59E}`</span><span class="sxs-lookup"><span data-stu-id="dca25-168">For the first column (the **Value Name** field), copy and paste the following Class ID: `{030E9A3F-7B18-4122-9A60-B87235E4F59E}`</span></span>
   2. <span data-ttu-id="dca25-169">İkinci sütun için ( **değeri** alanı), aşağıdaki değeri türü:`1`</span><span class="sxs-lookup"><span data-stu-id="dca25-169">For the second column (the **Value** field), type in the following value: `1`</span></span>
   3. <span data-ttu-id="dca25-170">Tıklatın **Tamam** kapatmak için **içeriğini göster** penceresi.</span><span class="sxs-lookup"><span data-stu-id="dca25-170">Click **OK** to close the **Show Contents** window.</span></span>
      
      ![Yukarıda belirtildiği gibi değerlerini doldurun.](./media/active-directory-saas-ie-group-policy/show-contents.png)
5. <span data-ttu-id="dca25-172">Tıklatın **Tamam** değişikliklerinizi uygulamak ve kapatmak için **eklenti listesi** penceresi.</span><span class="sxs-lookup"><span data-stu-id="dca25-172">Click **OK** to apply your changes and close the **Add-on List** window.</span></span>

<span data-ttu-id="dca25-173">Seçili OU'da makineler için şimdi Uzantının etkinleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="dca25-173">The extension should now be enabled for the machines in the selected OU.</span></span> [<span data-ttu-id="dca25-174">Etkinleştirmek veya Internet Explorer eklentileri devre dışı bırakmak için Grup İlkesi'ni kullanma hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="dca25-174">Learn more about using group policy to enable or disable Internet Explorer add-ons.</span></span>](https://technet.microsoft.com/library/dn454941.aspx)

## <a name="step-5-optional-disable-remember-password-prompt"></a><span data-ttu-id="dca25-175">Adım 5 (isteğe bağlı): "Parolayı anımsa" istemi devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="dca25-175">Step 5 (Optional): Disable "Remember Password" Prompt</span></span>
<span data-ttu-id="dca25-176">Kullanıcılar oturum erişim paneli uzantısı kullanılarak Web siteleri açma, Internet Explorer "parolanızı saklamak ister misiniz?" sorusunu sorarken aşağıdaki istemi Göster</span><span class="sxs-lookup"><span data-stu-id="dca25-176">When users sign-in to websites using the Access Panel Extension, Internet Explorer may show the following prompt asking "Would you like to store your password?"</span></span>

![](./media/active-directory-saas-ie-group-policy/remember-password-prompt.png)

<span data-ttu-id="dca25-177">Bu istemi görmesini, kullanıcılarınızın engellemek istiyorsanız, parolaları anımsama otomatik tamamlama önlemek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="dca25-177">If you wish to prevent your users from seeing this prompt, then follow the steps below to prevent auto-complete from remembering passwords:</span></span>

1. <span data-ttu-id="dca25-178">İçinde **Grup İlkesi Yönetimi Düzenleyicisi** penceresi, aşağıda listelenen yoluna gidin.</span><span class="sxs-lookup"><span data-stu-id="dca25-178">In the **Group Policy Management Editor** window, go to the path listed below.</span></span> <span data-ttu-id="dca25-179">Bu yapılandırma ayarının yalnızca altında kullanılabilir **Kullanıcı Yapılandırması**.</span><span class="sxs-lookup"><span data-stu-id="dca25-179">This configuration setting is only available under **User Configuration**.</span></span>
   
   * `User Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/`
2. <span data-ttu-id="dca25-180">Adlı ayar Bul **kullanıcı adları ve parolalar formlarında için Otomatik Tamamlama özelliğini**.</span><span class="sxs-lookup"><span data-stu-id="dca25-180">Find the setting named **Turn on the auto-complete feature for user names and passwords on forms**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="dca25-181">Active Directory önceki sürümlerinde bu ayar adı olarak listesinde **parolaları kaydetmek için otomatik tamamlama izin verme**.</span><span class="sxs-lookup"><span data-stu-id="dca25-181">Previous versions of Active Directory may list this setting with the name **Do not allow auto-complete to save passwords**.</span></span> <span data-ttu-id="dca25-182">Bu öğreticide açıklanan ayarı configuration Bu ayar için farklıdır.</span><span class="sxs-lookup"><span data-stu-id="dca25-182">The configuration for that setting differs from the setting described in this tutorial.</span></span>
   > 
   > 
   
    ![Kullanıcı Ayarları altında şunun unutmayın.](./media/active-directory-saas-ie-group-policy/disable-auto-complete.png)
3. <span data-ttu-id="dca25-184">Yukarıdaki ayar sağ tıklatın ve seçin **Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="dca25-184">Right click the above setting, and select **Edit**.</span></span>
4. <span data-ttu-id="dca25-185">Başlıklı pencerede **kullanıcı adları ve parolalar formlarında için Otomatik Tamamlama özelliğini**seçin **devre dışı**.</span><span class="sxs-lookup"><span data-stu-id="dca25-185">In the window titled **Turn on the auto-complete feature for user names and passwords on forms**, select **Disabled**.</span></span>
   
    ![Devre dışı bırak seçin](./media/active-directory-saas-ie-group-policy/disable-passwords.png)
5. <span data-ttu-id="dca25-187">Tıklatın **Tamam** pencereyi kapatın ve bu değişiklikleri uygulamak için.</span><span class="sxs-lookup"><span data-stu-id="dca25-187">Click **OK** to apply these changes and close the window.</span></span>

<span data-ttu-id="dca25-188">Kullanıcıları artık kendi kimlik bilgilerini veya kullanım otomatik tamamlama önceden depolanan kimlik bilgileri erişmek için depolama mümkün olacaktır.</span><span class="sxs-lookup"><span data-stu-id="dca25-188">Users will no longer be able to store their credentials or use auto-complete to access previously stored credentials.</span></span> <span data-ttu-id="dca25-189">Ancak, bu ilke otomatik tamamlama, form alanları, arama alanları gibi diğer türleri için kullanmaya devam etmek kullanıcıların izin vermez.</span><span class="sxs-lookup"><span data-stu-id="dca25-189">However, this policy does allow users to continue to use auto-complete for other types of form fields, such as search fields.</span></span>

> [!WARNING]
> <span data-ttu-id="dca25-190">Kullanıcıların bazı kimlik bilgileri, bu ilke işlem depolamak seçtikten sonra bu ilke etkinleştirildiğinde *değil* zaten depolanmış kimlik bilgilerini temizleyin.</span><span class="sxs-lookup"><span data-stu-id="dca25-190">If this policy is enabled after users have chosen to store some credentials, this policy will *not* clear the credentials that have already been stored.</span></span>
> 
> 

## <a name="step-6-testing-the-deployment"></a><span data-ttu-id="dca25-191">6. adım: dağıtımı test etme</span><span class="sxs-lookup"><span data-stu-id="dca25-191">Step 6: Testing the Deployment</span></span>
<span data-ttu-id="dca25-192">Uzantı dağıtımı başarılı olup olmadığını doğrulamak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="dca25-192">Follow the steps below to verify if the extension deployment was successful:</span></span>

1. <span data-ttu-id="dca25-193">Kullanarak dağıttıysanız **Bilgisayar Yapılandırması**, oturum açın, seçili OU'ya ait bir istemci makine [adım 2: Grup İlkesi nesnesi oluşturmak](#step-2-create-the-group-policy-object).</span><span class="sxs-lookup"><span data-stu-id="dca25-193">If you deployed using **Computer Configuration**, sign into a client machine that belongs to the OU that you selected in [Step 2: Create the Group Policy Object](#step-2-create-the-group-policy-object).</span></span> <span data-ttu-id="dca25-194">Kullanarak dağıttıysanız **Kullanıcı Yapılandırması**, ilgili OU'ya ait olan bir kullanıcı olarak oturum açmak emin olun.</span><span class="sxs-lookup"><span data-stu-id="dca25-194">If you deployed using **User Configuration**, make sure to sign in as a user who belongs to that OU.</span></span>
2. <span data-ttu-id="dca25-195">Bileşenler değişiklikler Grup İlkesi için tam olarak için güncelleştirme birkaç oturum sürebilir bu makine ile.</span><span class="sxs-lookup"><span data-stu-id="dca25-195">It may take a couple sign ins for the group policy changes to fully update with this machine.</span></span> <span data-ttu-id="dca25-196">Güncelleştirmeyi uygulamak için açık bir **komut istemi** penceresini açın ve aşağıdaki komutu çalıştırın:`gpupdate /force`</span><span class="sxs-lookup"><span data-stu-id="dca25-196">To force the update, open a **Command Prompt** window and run the following command: `gpupdate /force`</span></span>
3. <span data-ttu-id="dca25-197">Yüklemenin gerçekleşmesi makine yeniden başlatmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="dca25-197">You must restart the machine for the installation to take place.</span></span> <span data-ttu-id="dca25-198">Önyükleme uzantısı sırasında normal yükler önemli ölçüde daha uzun sürebilir.</span><span class="sxs-lookup"><span data-stu-id="dca25-198">Bootup may take significantly more time than usual while the extension installs.</span></span>
4. <span data-ttu-id="dca25-199">Yeniden başlattıktan sonra açmak **Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="dca25-199">After restarting, open **Internet Explorer**.</span></span> <span data-ttu-id="dca25-200">Pencerenin sağ üst köşesinde tıklatın **Araçları** (dişli simgesi) ve ardından **eklentileri yönetme**.</span><span class="sxs-lookup"><span data-stu-id="dca25-200">On the upper-right corner of the window, click **Tools** (the gear icon), and then select **Manage add-ons**.</span></span>
   
    ![İçin Araçlar > eklentileri yönetme](./media/active-directory-saas-ie-group-policy/manage-add-ons.png)
5. <span data-ttu-id="dca25-202">İçinde **Eklentileri Yönet** penceresinde doğrulayın **erişim paneli uzantısı** yüklendi ve kendi **durum** ayarlandığından **etkin**.</span><span class="sxs-lookup"><span data-stu-id="dca25-202">In the **Manage Add-ons** window, verify that the **Access Panel Extension** has been installed and that its **Status** has been set to **Enabled**.</span></span>
   
    ![Erişim paneli uzantısı yüklü ve etkin olduğunu doğrulayın.](./media/active-directory-saas-ie-group-policy/verify-install.png)

## <a name="related-articles"></a><span data-ttu-id="dca25-204">İlgili makaleler</span><span class="sxs-lookup"><span data-stu-id="dca25-204">Related Articles</span></span>
* [<span data-ttu-id="dca25-205">Azure Active Directory'de Uygulama Yönetimi için Makale Dizini</span><span class="sxs-lookup"><span data-stu-id="dca25-205">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="dca25-206">Uygulama erişimi ve Azure Active Directory ile çoklu oturum açma</span><span class="sxs-lookup"><span data-stu-id="dca25-206">Application access and single sign-on with Azure Active Directory</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="dca25-207">Erişim paneli uzantısı Internet Explorer için sorun giderme</span><span class="sxs-lookup"><span data-stu-id="dca25-207">Troubleshooting the Access Panel Extension for Internet Explorer</span></span>](active-directory-saas-ie-troubleshooting.md)

