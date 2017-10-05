---
title: "Azure Active Directory etki alanı Hizmetleri: Grup İlkesi, yönetilen etki alanlarını yönetme | Microsoft Docs"
description: "Yönetici Grup İlkesi Azure Active Directory etki alanı Hizmetleri, yönetilen etki alanları"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 299e09ef1bb1b1db9d64447bf4537c7c3a3cfd5f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="administer-group-policy-on-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="a6597-103">Grup İlkesi, bir Azure AD etki alanı Hizmetleri yönetilen etki alanını yönetme</span><span class="sxs-lookup"><span data-stu-id="a6597-103">Administer Group Policy on an Azure AD Domain Services managed domain</span></span>
<span data-ttu-id="a6597-104">Azure Active Directory etki alanı Hizmetleri için 'AADDC kullanıcılar' ve 'AADDC Bilgisayarları' kapsayıcı yerleşik Grup İlkesi nesneleri (GPO'lar) içerir.</span><span class="sxs-lookup"><span data-stu-id="a6597-104">Azure Active Directory Domain Services includes built-in Group Policy Objects (GPOs) for the 'AADDC Users' and 'AADDC Computers' containers.</span></span> <span data-ttu-id="a6597-105">Yönetilen etki alanında Grup İlkesi yapılandırmak için bu yerleşik GPO'ları özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a6597-105">You can customize these built-in GPOs to configure Group Policy on the managed domain.</span></span> <span data-ttu-id="a6597-106">Ayrıca, 'AAD DC Yöneticiler' grubunun üyeleri yönetilen etki alanında özel kendi OU'ları oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a6597-106">Additionally, members of the 'AAD DC Administrators' group can create their own custom OUs in the managed domain.</span></span> <span data-ttu-id="a6597-107">Bunlar ayrıca özel GPO'ları oluşturmak ve bunları bu özel OU'lara bağlayın.</span><span class="sxs-lookup"><span data-stu-id="a6597-107">They can also create custom GPOs and link them to these custom OUs.</span></span> <span data-ttu-id="a6597-108">'AAD DC Yöneticiler' gruba ait kullanıcılar yönetilen etki alanı Grup İlkesi yönetim ayrıcalıkları verilir.</span><span class="sxs-lookup"><span data-stu-id="a6597-108">Users who belong to the 'AAD DC Administrators' group are granted Group Policy administration privileges on the managed domain.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a6597-109">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="a6597-109">Before you begin</span></span>
<span data-ttu-id="a6597-110">Bu makalede listelenen görevleri gerçekleştirmek için gerekir:</span><span class="sxs-lookup"><span data-stu-id="a6597-110">To perform the tasks listed in this article, you need:</span></span>

1. <span data-ttu-id="a6597-111">Geçerli bir **Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="a6597-111">A valid **Azure subscription**.</span></span>
2. <span data-ttu-id="a6597-112">Bir **Azure AD dizini** -ya da bir şirket içi dizin veya bir yalnızca bulut dizini ile eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="a6597-112">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span></span>
3. <span data-ttu-id="a6597-113">**Azure AD etki alanı Hizmetleri** Azure AD dizini için etkinleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="a6597-113">**Azure AD Domain Services** must be enabled for the Azure AD directory.</span></span> <span data-ttu-id="a6597-114">Bunu yapmadıysanız, özetlenen tüm görevleri izleyin [Getting Started guide](active-directory-ds-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="a6597-114">If you haven't done so, follow all the tasks outlined in the [Getting Started guide](active-directory-ds-getting-started.md).</span></span>
4. <span data-ttu-id="a6597-115">A **sanal makine etki alanına katılmış** Azure AD etki alanı Hizmetleri yönetilen etki yönettiğiniz.</span><span class="sxs-lookup"><span data-stu-id="a6597-115">A **domain-joined virtual machine** from which you administer the Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="a6597-116">Bu tür bir sanal makine yoksa, başlıklı makalede açıklanan tüm görevleri izleyin [Windows sanal makinesini yönetilen bir etki alanına katma](active-directory-ds-admin-guide-join-windows-vm.md).</span><span class="sxs-lookup"><span data-stu-id="a6597-116">If you don't have such a virtual machine, follow all the tasks outlined in the article titled [Join a Windows virtual machine to a managed domain](active-directory-ds-admin-guide-join-windows-vm.md).</span></span>
5. <span data-ttu-id="a6597-117">Kimlik bilgilerini gereken bir **'AAD DC Yöneticiler' grubuna ait olan kullanıcı hesabı** dizininizde yönetilen etki alanınız için Grup İlkesi yönetmek için.</span><span class="sxs-lookup"><span data-stu-id="a6597-117">You need the credentials of a **user account belonging to the 'AAD DC Administrators' group** in your directory, to administer Group Policy for your managed domain.</span></span>

<br>

## <a name="task-1---provision-a-domain-joined-virtual-machine-to-remotely-administer-group-policy-for-the-managed-domain"></a><span data-ttu-id="a6597-118">Görev 1 - Grup İlkesi yönetilen etki alanı için uzaktan yönetmek için bir etki alanına katılmış sanal makine sağlama</span><span class="sxs-lookup"><span data-stu-id="a6597-118">Task 1 - Provision a domain-joined virtual machine to remotely administer Group Policy for the managed domain</span></span>
<span data-ttu-id="a6597-119">Azure AD etki alanı Hizmetleri yönetilen etki alanları, Active Directory Yönetim Merkezi (ADAC) veya AD PowerShell gibi bilinen Active Directory yönetim araçlarını kullanarak uzaktan yönetilebilir.</span><span class="sxs-lookup"><span data-stu-id="a6597-119">Azure AD Domain Services managed domains can be managed remotely using familiar Active Directory administrative tools such as the Active Directory Administrative Center (ADAC) or AD PowerShell.</span></span> <span data-ttu-id="a6597-120">Benzer şekilde, Grup İlkesi yönetilen etki alanı için Grup İlkesi yönetim araçları kullanarak uzaktan yönetilebilir.</span><span class="sxs-lookup"><span data-stu-id="a6597-120">Similarly, Group Policy for the managed domain can be administered remotely using the Group Policy administration tools.</span></span>

<span data-ttu-id="a6597-121">Yöneticiler, Azure AD dizini, Uzak Masaüstü aracılığıyla yönetilen etki alanında etki alanı denetleyicisine bağlanmak için ayrıcalıklara sahip değil.</span><span class="sxs-lookup"><span data-stu-id="a6597-121">Administrators in your Azure AD directory do not have privileges to connect to domain controllers on the managed domain via Remote Desktop.</span></span> <span data-ttu-id="a6597-122">'AAD DC Yöneticiler' grubunun üyeleri, Grup İlkesi yönetilen etki alanları için uzaktan yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a6597-122">Members of the 'AAD DC Administrators' group can administer Group Policy for managed domains remotely.</span></span> <span data-ttu-id="a6597-123">Bunlar, yönetilen etki alanına katılmış bir Windows Server/istemci bilgisayarda Grup İlkesi araçları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a6597-123">They can use Group Policy tools on a Windows Server/client computer joined to the managed domain.</span></span> <span data-ttu-id="a6597-124">Grup İlkesi araçları, Windows Server ve yönetilen etki alanına katılan istemci makineleri üzerinde Grup İlkesi Yönetimi isteğe bağlı özellik bir parçası olarak yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="a6597-124">Group Policy tools can be installed as part of the Group Policy Management optional feature on Windows Server and client machines joined to the managed domain.</span></span>

<span data-ttu-id="a6597-125">İlk yönetilen etki alanına katılmış bir Windows Server sanal makine sağlamak için bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="a6597-125">The first task is to provision a Windows Server virtual machine that is joined to the managed domain.</span></span> <span data-ttu-id="a6597-126">Yönergeler için başlıklı makaleye bakın [bir Windows Server sanal makine bir Azure AD etki alanı Hizmetleri yönetilen etki alanına katılmak](active-directory-ds-admin-guide-join-windows-vm.md).</span><span class="sxs-lookup"><span data-stu-id="a6597-126">For instructions, refer to the article titled [join a Windows Server virtual machine to an Azure AD Domain Services managed domain](active-directory-ds-admin-guide-join-windows-vm.md).</span></span>

## <a name="task-2---install-group-policy-tools-on-the-virtual-machine"></a><span data-ttu-id="a6597-127">Görev 2 - sanal makineye yükleme Grup İlkesi Araçları</span><span class="sxs-lookup"><span data-stu-id="a6597-127">Task 2 - Install Group Policy tools on the virtual machine</span></span>
<span data-ttu-id="a6597-128">Etki alanına katılmış sanal makinede Grup İlkesi Yönetim Araçları'nı yüklemek için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="a6597-128">Perform the following steps to install the Group Policy Administration tools on the domain joined virtual machine.</span></span>

1. <span data-ttu-id="a6597-129">Gidin **sanal makineleri** Azure Klasik Portalı'ndaki düğüm.</span><span class="sxs-lookup"><span data-stu-id="a6597-129">Navigate to **Virtual Machines** node in the Azure classic portal.</span></span> <span data-ttu-id="a6597-130">Görev 1'de oluşturduğunuz sanal makineyi seçin ve tıklatın **Bağlan** pencerenin altındaki komut çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="a6597-130">Select the virtual machine you created in Task 1 and click **Connect** on the command bar at the bottom of the window.</span></span>

    ![Windows sanal makineye bağlanma](./media/active-directory-domain-services-admin-guide/connect-windows-vm.png)
2. <span data-ttu-id="a6597-132">Klasik Portalı'nı açın ya da sanal makineye bağlanmak için kullanılan bir '.rdp' uzantısına sahip bir dosyayı kaydetmek isteyip istemediğinizi sorar.</span><span class="sxs-lookup"><span data-stu-id="a6597-132">The classic portal prompts you to open or save a file with a '.rdp' extension, which is used to connect to the virtual machine.</span></span> <span data-ttu-id="a6597-133">Yükleme tamamlandığında dosyayı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="a6597-133">Click the file when it has finished downloading.</span></span>
3. <span data-ttu-id="a6597-134">Oturum açma isteminde 'AAD DC Yöneticiler' grubuna ait olan bir kullanıcının kimlik bilgilerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="a6597-134">At the login prompt, use the credentials of a user belonging to the 'AAD DC Administrators' group.</span></span> <span data-ttu-id="a6597-135">Örneğin, kullandığımız 'bob@domainservicespreview.onmicrosoft.com' bizim durumda.</span><span class="sxs-lookup"><span data-stu-id="a6597-135">For example, we use 'bob@domainservicespreview.onmicrosoft.com' in our case.</span></span>
4. <span data-ttu-id="a6597-136">Başlangıç ekranından açmak **Sunucu Yöneticisi'ni**.</span><span class="sxs-lookup"><span data-stu-id="a6597-136">From the Start screen, open **Server Manager**.</span></span> <span data-ttu-id="a6597-137">Tıklatın **rol ve Özellik Ekle** merkezi bölmesinde Sunucu Yöneticisi penceresi.</span><span class="sxs-lookup"><span data-stu-id="a6597-137">Click **Add Roles and Features** in the central pane of the Server Manager window.</span></span>

    ![Sanal makine üzerinde Sunucu Yöneticisi'ni başlatın](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager.png)
5. <span data-ttu-id="a6597-139">Üzerinde **başlamadan önce** sayfasında **Ekle roller ve Özellikler Sihirbazı**, tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="a6597-139">On the **Before You Begin** page of the **Add Roles and Features Wizard**, click **Next**.</span></span>

    ![Başlamadan önce sayfası](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-begin.png)
6. <span data-ttu-id="a6597-141">Üzerinde **yükleme türü** sayfasında, bırakın **rol tabanlı veya özellik tabanlı yükleme** işaretli seçeneğini ve tıklayın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="a6597-141">On the **Installation Type** page, leave the **Role-based or feature-based installation** option checked and click **Next**.</span></span>

    ![Yükleme türü sayfası](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-type.png)
7. <span data-ttu-id="a6597-143">Üzerinde **sunucu seçimi** sayfasında, sunucu havuzundan geçerli sanal makine seçin ve tıklayın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="a6597-143">On the **Server Selection** page, select the current virtual machine from the server pool, and click **Next**.</span></span>

    ![Sunucu seçimi sayfası](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-server.png)
8. <span data-ttu-id="a6597-145">Üzerinde **sunucu rolleri** sayfasında, **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="a6597-145">On the **Server Roles** page, click **Next**.</span></span> <span data-ttu-id="a6597-146">Biz herhangi bir rol sunucuda yüklemiyorsanız beri Biz bu sayfayı atla.</span><span class="sxs-lookup"><span data-stu-id="a6597-146">We skip this page since we are not installing any roles on the server.</span></span>
9. <span data-ttu-id="a6597-147">Üzerinde **özellikleri** sayfasında, **Grup İlkesi Yönetimi** özelliği.</span><span class="sxs-lookup"><span data-stu-id="a6597-147">On the **Features** page, select the **Group Policy Management** feature.</span></span>

    ![Özellikler sayfası](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-gp-management.png)
10. <span data-ttu-id="a6597-149">Üzerinde **onay** sayfasında, **yükleme** sanal makineye Grup İlkesi Yönetimi özelliğini yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="a6597-149">On the **Confirmation** page, click **Install** to install the Group Policy Management feature on the virtual machine.</span></span> <span data-ttu-id="a6597-150">Özellik yükleme işlemi başarıyla tamamlandığında tıklatın **Kapat** çıkmak için **rol ve Özellik Ekle** Sihirbazı.</span><span class="sxs-lookup"><span data-stu-id="a6597-150">When feature installation completes successfully, click **Close** to exit the **Add Roles and Features** wizard.</span></span>

    ![Onay sayfası](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-gp-management-confirmation.png)

## <a name="task-3---launch-the-group-policy-management-console-to-administer-group-policy"></a><span data-ttu-id="a6597-152">Görev 3 - Grup İlkesi yönetmek için Grup İlkesi Yönetim Konsolu'nu başlatın</span><span class="sxs-lookup"><span data-stu-id="a6597-152">Task 3 - Launch the Group Policy management console to administer Group Policy</span></span>
<span data-ttu-id="a6597-153">Grup İlkesi yönetilen etki alanı yönetmek için etki alanına katılmış sanal makinede Grup İlkesi Yönetim Konsolu'nu kullanın.</span><span class="sxs-lookup"><span data-stu-id="a6597-153">You can use the Group Policy management console on the domain-joined virtual machine to administer Group Policy on the managed domain.</span></span>

> [!NOTE]
> <span data-ttu-id="a6597-154">Grup İlkesi yönetilen etki alanı yönetmek için 'AAD DC Yöneticiler' grubunun bir üyesi olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a6597-154">You need to be a member of the 'AAD DC Administrators' group, to administer Group Policy on the managed domain.</span></span>
>
>

1. <span data-ttu-id="a6597-155">Başlangıç ekranından tıklatın **Yönetimsel Araçlar**.</span><span class="sxs-lookup"><span data-stu-id="a6597-155">From the Start screen, click **Administrative Tools**.</span></span> <span data-ttu-id="a6597-156">Görmeniz gerekir **Grup İlkesi Yönetimi** sanal makinede yüklü konsol.</span><span class="sxs-lookup"><span data-stu-id="a6597-156">You should see the **Group Policy Management** console installed on the virtual machine.</span></span>

    ![Başlatma Grup İlkesi Yönetimi](./media/active-directory-domain-services-admin-guide/gp-management-installed.png)
2. <span data-ttu-id="a6597-158">Tıklatın **Grup İlkesi Yönetimi** Grup İlkesi Yönetim Konsolu'nu başlatın.</span><span class="sxs-lookup"><span data-stu-id="a6597-158">Click **Group Policy Management** to launch the Group Policy Management console.</span></span>

    ![Grup İlkesi konsolu](./media/active-directory-domain-services-admin-guide/gp-management-console.png)

## <a name="task-4---customize-built-in-group-policy-objects"></a><span data-ttu-id="a6597-160">Görev 4 - yerleşik Grup İlkesi nesnelerini özelleştirme</span><span class="sxs-lookup"><span data-stu-id="a6597-160">Task 4 - Customize built-in Group Policy Objects</span></span>
<span data-ttu-id="a6597-161">İki yerleşik Grup İlkesi nesneleri (GPO'lar) - her biri için yönetilen etki alanınız 'AADDC bilgisayarlar' ve 'AADDC kullanıcılar' kapsayıcılarındaki vardır.</span><span class="sxs-lookup"><span data-stu-id="a6597-161">There are two built-in Group Policy Objects (GPOs) - one each for the 'AADDC Computers' and 'AADDC Users' containers in your managed domain.</span></span> <span data-ttu-id="a6597-162">Bu GPO'ları yönetilen etki alanında Grup İlkesi yapılandırmak için özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a6597-162">You can customize these GPOs to configure group policy on the managed domain.</span></span>

1. <span data-ttu-id="a6597-163">İçinde **Grup İlkesi Yönetimi** konsolu, genişletmek için tıklatın **orman: contoso100.com** ve **etki alanları** yönetilen etki alanınız için Grup İlkeleri görmek için düğümleri.</span><span class="sxs-lookup"><span data-stu-id="a6597-163">In the **Group Policy Management** console, click to expand the **Forest: contoso100.com** and **Domains** nodes to see the group policies for your managed domain.</span></span>

    ![Yerleşik GPO'ları](./media/active-directory-domain-services-admin-guide/builtin-gpos.png)
2. <span data-ttu-id="a6597-165">Yönetilen etki alanınızda grup ilkeleri yapılandırmak için bu yerleşik GPO özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a6597-165">You can customize these built-in GPOs to configure group policies on your managed domain.</span></span> <span data-ttu-id="a6597-166">GPO'yu sağ tıklatın ve **Düzenle...**  yerleşik GPO özelleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="a6597-166">Right-click the GPO and click **Edit...** to customize the built-in GPO.</span></span> <span data-ttu-id="a6597-167">Grup İlkesi yapılandırma Düzenleyicisi araç GPO özelleştirmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="a6597-167">The Group Policy Configuration Editor tool enables you to customize the GPO.</span></span>

    ![Yerleşik bir GPO'yu düzenleyin](./media/active-directory-domain-services-admin-guide/edit-builtin-gpo.png)
3. <span data-ttu-id="a6597-169">Artık kullanabilirsiniz **Grup İlkesi Yönetimi Düzenleyicisi** yerleşik bir GPO'yu düzenlemek için konsol.</span><span class="sxs-lookup"><span data-stu-id="a6597-169">You can now use the **Group Policy Management Editor** console to edit the built-in GPO.</span></span> <span data-ttu-id="a6597-170">Örneğin, aşağıdaki ekran görüntüsünde yerleşik 'AADDC bilgisayarlar' GPO özelleştirme gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="a6597-170">For instance, the following screenshot shows how to customize the built-in 'AADDC Computers' GPO.</span></span>

    ![GPO özelleştirme](./media/active-directory-domain-services-admin-guide/gp-editor.png)

## <a name="task-5---create-a-custom-group-policy-object-gpo"></a><span data-ttu-id="a6597-172">Görev 5 - bir özel Grup İlkesi nesnesi (GPO) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a6597-172">Task 5 - Create a custom Group Policy Object (GPO)</span></span>
<span data-ttu-id="a6597-173">Oluşturun veya kendi özel Grup İlkesi nesneleri içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="a6597-173">You can create or import your own custom group policy objects.</span></span> <span data-ttu-id="a6597-174">Ayrıca, özel GPO'ları, yönetilen etki alanında oluşturulan özel bir OU bağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a6597-174">You can also link custom GPOs to a custom OU you have created in your managed domain.</span></span> <span data-ttu-id="a6597-175">Özel Kuruluş birimi oluşturma hakkında daha fazla bilgi için bkz: [yönetilen bir etki alanına özel bir OU oluşturmanız](active-directory-ds-admin-guide-create-ou.md).</span><span class="sxs-lookup"><span data-stu-id="a6597-175">For more information on creating custom organizational units, see [create a custom OU on a managed domain](active-directory-ds-admin-guide-create-ou.md).</span></span>

> [!NOTE]
> <span data-ttu-id="a6597-176">Grup İlkesi yönetilen etki alanı yönetmek için 'AAD DC Yöneticiler' grubunun bir üyesi olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a6597-176">You need to be a member of the 'AAD DC Administrators' group, to administer Group Policy on the managed domain.</span></span>
>
>

1. <span data-ttu-id="a6597-177">İçinde **Grup İlkesi Yönetimi** konsolu, özel, kuruluş birimi (OU) seçmek için tıklatın.</span><span class="sxs-lookup"><span data-stu-id="a6597-177">In the **Group Policy Management** console, click to select your custom organizational unit (OU).</span></span> <span data-ttu-id="a6597-178">OU'yu sağ tıklatın ve **bu etki alanında GPO oluştur ve buraya bağla...** .</span><span class="sxs-lookup"><span data-stu-id="a6597-178">Right-click the OU and click **Create a GPO in this domain, and Link it here...**.</span></span>

    ![Özel bir GPO oluşturun](./media/active-directory-domain-services-admin-guide/gp-create-gpo.png)
2. <span data-ttu-id="a6597-180">Yeni GPO ve tıklatın için bir ad belirtin **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="a6597-180">Specify a name for the new GPO and click **OK**.</span></span>

    ![GPO için bir ad belirtin](./media/active-directory-domain-services-admin-guide/gp-specify-gpo-name.png)
3. <span data-ttu-id="a6597-182">Yeni bir GPO oluşturulur ve özel OU'ya bağlı.</span><span class="sxs-lookup"><span data-stu-id="a6597-182">A new GPO is created and linked to your custom OU.</span></span> <span data-ttu-id="a6597-183">GPO'yu sağ tıklatın ve **Düzenle...**  menüsünde.</span><span class="sxs-lookup"><span data-stu-id="a6597-183">Right-click the GPO and click **Edit...** from the menu.</span></span>

    ![Yeni oluşturulmuş GPO](./media/active-directory-domain-services-admin-guide/gp-gpo-created.png)
4. <span data-ttu-id="a6597-185">Yeni oluşturulan GPO kullanarak özelleştirebileceğiniz **Grup İlkesi Yönetimi Düzenleyicisi**.</span><span class="sxs-lookup"><span data-stu-id="a6597-185">You can customize the newly created GPO using the **Group Policy Management Editor**.</span></span>

    ![Yeni GPO özelleştirme](./media/active-directory-domain-services-admin-guide/gp-customize-gpo.png)


<span data-ttu-id="a6597-187">Kullanma hakkında daha fazla bilgi [Grup İlkesi Yönetim Konsolu](https://technet.microsoft.com/library/cc753298.aspx) Technet üzerindeki kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a6597-187">More information about using [Group Policy Management Console](https://technet.microsoft.com/library/cc753298.aspx) is available on Technet.</span></span>

## <a name="related-content"></a><span data-ttu-id="a6597-188">İlgili İçerik</span><span class="sxs-lookup"><span data-stu-id="a6597-188">Related Content</span></span>
* [<span data-ttu-id="a6597-189">Azure AD etki alanı Hizmetleri - başlangıç kılavuzu</span><span class="sxs-lookup"><span data-stu-id="a6597-189">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="a6597-190">Bir Windows Server sanal makine bir Azure AD etki alanı Hizmetleri yönetilen etki alanına katılma</span><span class="sxs-lookup"><span data-stu-id="a6597-190">Join a Windows Server virtual machine to an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* [<span data-ttu-id="a6597-191">Azure AD Domain Services tarafından yönetilen etki alanını yönetme</span><span class="sxs-lookup"><span data-stu-id="a6597-191">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="a6597-192">Grup İlkesi Yönetim Konsolu</span><span class="sxs-lookup"><span data-stu-id="a6597-192">Group Policy Management Console</span></span>](https://technet.microsoft.com/library/cc753298.aspx)
