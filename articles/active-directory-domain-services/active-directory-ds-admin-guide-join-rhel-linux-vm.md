---
title: "Azure Active Directory etki alanı Hizmetleri: RHEL VM yönetilen bir etki alanına katılın. | Microsoft Docs"
description: "Red Hat Enterprise Linux sanal makinesini Azure AD Etki Alanı Hizmetleri'ne ekleme"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 87291c47-1280-43f8-8fb2-da1bd61a4942
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 69f1850bfed90392e9a4695e2443ffaa6bfc746d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="join-a-red-hat-enterprise-linux-7-virtual-machine-to-a-managed-domain"></a><span data-ttu-id="d645c-103">Red Hat Enterprise Linux 7 sanal makinesini yönetilen bir etki alanına ekleme</span><span class="sxs-lookup"><span data-stu-id="d645c-103">Join a Red Hat Enterprise Linux 7 virtual machine to a managed domain</span></span>
<span data-ttu-id="d645c-104">Bu makalede bir Red Hat Enterprise Linux (RHEL) 7 sanal makine bir Azure AD etki alanı Hizmetleri yönetilen etki alanına katılma kullanmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="d645c-104">This article shows you how to join a Red Hat Enterprise Linux (RHEL) 7 virtual machine to an Azure AD Domain Services managed domain.</span></span>

## <a name="provision-a-red-hat-enterprise-linux-virtual-machine"></a><span data-ttu-id="d645c-105">Red Hat Enterprise Linux sanal makine sağlama</span><span class="sxs-lookup"><span data-stu-id="d645c-105">Provision a Red Hat Enterprise Linux virtual machine</span></span>
<span data-ttu-id="d645c-106">Azure Portalı'nı kullanarak bir RHEL 7 sanal makine sağlamak için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="d645c-106">Perform the following steps to provision a RHEL 7 virtual machine using the Azure portal.</span></span>

1. <span data-ttu-id="d645c-107">[Azure Portal](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="d645c-107">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

    ![Azure portalı panosunun](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-dashboard.png)
2. <span data-ttu-id="d645c-109">Tıklatın **yeni** türü ve sol bölmede **Red Hat** aşağıdaki ekran görüntüsünde gösterildiği gibi arama çubuğunu içine.</span><span class="sxs-lookup"><span data-stu-id="d645c-109">Click **New** on the left pane and type **Red Hat** into the search bar as shown in the following screenshot.</span></span> <span data-ttu-id="d645c-110">Red Hat Enterprise Linux girişleri arama sonuçlarında görünür.</span><span class="sxs-lookup"><span data-stu-id="d645c-110">Entries for Red Hat Enterprise Linux appear in the search results.</span></span> <span data-ttu-id="d645c-111">Tıklatın **Red Hat Enterprise Linux 7.2**.</span><span class="sxs-lookup"><span data-stu-id="d645c-111">Click **Red Hat Enterprise Linux 7.2**.</span></span>

    ![RHEL sonuçlarında seçin](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-find-rhel-image.png)
3. <span data-ttu-id="d645c-113">Arama sonuçlarının **her şeyi** bölmesinde Red Hat Enterprise Linux 7.2 görüntü listesinde.</span><span class="sxs-lookup"><span data-stu-id="d645c-113">The search results in the **Everything** pane should list the Red Hat Enterprise Linux 7.2 image.</span></span> <span data-ttu-id="d645c-114">Tıklatın **Red Hat Enterprise Linux 7.2** sanal makine görüntüsüne hakkında daha fazla bilgi görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="d645c-114">Click **Red Hat Enterprise Linux 7.2** to view more information about the virtual machine image.</span></span>

    ![RHEL sonuçlarında seçin](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-rhel-image.png)
4. <span data-ttu-id="d645c-116">İçinde **Red Hat Enterprise Linux 7.2** bölmesinde, sanal makine görüntüsüne hakkında daha fazla bilgi görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d645c-116">In the **Red Hat Enterprise Linux 7.2** pane, you should see more information about the virtual machine image.</span></span> <span data-ttu-id="d645c-117">İçinde **dağıtım modeli seçin** açılan listesinde, select **Klasik**.</span><span class="sxs-lookup"><span data-stu-id="d645c-117">In the **Select a deployment model** dropdown, select **Classic**.</span></span> <span data-ttu-id="d645c-118">Ardından **oluşturma** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d645c-118">Then click the **Create** button.</span></span>

    ![Görüntü ayrıntıları görüntüle](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-clicked.png)
5. <span data-ttu-id="d645c-120">İçinde **Temelleri** sayfasında **sanal makine oluşturma** Sihirbazı'nı girin **ana bilgisayar adı** yeni bir sanal makine için.</span><span class="sxs-lookup"><span data-stu-id="d645c-120">In the **Basics** page of the **Create virtual machine** wizard, enter the **Host Name** for the new virtual machine.</span></span> <span data-ttu-id="d645c-121">Ayrıca bir yerel yönetici kullanıcı adı belirtin **kullanıcı adı** alan ve **parola**.</span><span class="sxs-lookup"><span data-stu-id="d645c-121">Also specify a local administrator user name in the **User name** field and a **Password**.</span></span> <span data-ttu-id="d645c-122">Yerel yönetici kullanıcının kimliğini doğrulamak için bir SSH anahtarı kullanmayı seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d645c-122">You may also choose to use an SSH key to authenticate the local administrator user.</span></span> <span data-ttu-id="d645c-123">Ayrıca bir **fiyatlandırma katmanı** sanal makine için.</span><span class="sxs-lookup"><span data-stu-id="d645c-123">Also select a **Pricing Tier** for the virtual machine.</span></span>

    ![VM - temelleri sayfa oluşturma](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-basic-details.png)
6. <span data-ttu-id="d645c-125">İçinde **boyutu** sayfasında **sanal makine oluşturma** Sihirbazı, sanal makine boyutunu seçin.</span><span class="sxs-lookup"><span data-stu-id="d645c-125">In the **Size** page of the **Create virtual machine** wizard, select the size for the virtual machine.</span></span>

    ![VM - select boyutu oluşturun](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-vm-size.png)

7. <span data-ttu-id="d645c-127">İçinde **ayarları** sayfasında **sanal makine oluşturma** depolama hesabı için sanal makine Sihirbazı'nı seçin.</span><span class="sxs-lookup"><span data-stu-id="d645c-127">In the **Settings** page of the **Create virtual machine** wizard, select the storage account for the virtual machine.</span></span> <span data-ttu-id="d645c-128">Tıklatın **sanal ağ** için Linux VM dağıtılmalıdır sanal ağ seçmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="d645c-128">Click **Virtual Network** to select the virtual network to which the Linux VM should be deployed.</span></span> <span data-ttu-id="d645c-129">İçinde **sanal ağ** sanal ağ hangi Azure AD Etki Alanı Hizmetleri'nde kullanılabilir dikey penceresinde, seçin.</span><span class="sxs-lookup"><span data-stu-id="d645c-129">In the **Virtual Network** blade, select the virtual network in which Azure AD Domain Services is available.</span></span> <span data-ttu-id="d645c-130">Bu örnekte 'MyPreviewVNet' sanal ağı seçin.</span><span class="sxs-lookup"><span data-stu-id="d645c-130">In this example, we pick the 'MyPreviewVNet' virtual network.</span></span>

    ![VM oluşturma - sanal ağı seçin](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-select-vnet.png)
8. <span data-ttu-id="d645c-132">Üzerinde **Özet** sayfasında **sanal makine oluşturma** Sihirbazı, gözden geçirme ve tıklatın **Tamam** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d645c-132">On the **Summary** page of the **Create virtual machine** wizard, review and click the **OK** button.</span></span>

    ![VM - seçilen sanal ağ oluşturma](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-vnet-selected.png)
9. <span data-ttu-id="d645c-134">RHEL 7.2 görüntüyü temel alarak yeni bir sanal makine dağıtımı başlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d645c-134">Deployment of the new virtual machine based on the RHEL 7.2 image should start.</span></span>

    ![VM - Dağıtım başladı oluşturma](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployment-started.png)
10. <span data-ttu-id="d645c-136">Birkaç dakika sonra sanal makine başarıyla ve hazır kullanılmak üzere dağıtılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d645c-136">After a few minutes, the virtual machine should be deployed successfully and ready for use.</span></span>

    ![Dağıtılan VM - oluşturma](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployed.png)

## <a name="connect-remotely-to-the-newly-provisioned-linux-virtual-machine"></a><span data-ttu-id="d645c-138">Uzaktan yeni sağlandı Linux sanal makineye bağlanma</span><span class="sxs-lookup"><span data-stu-id="d645c-138">Connect remotely to the newly provisioned Linux virtual machine</span></span>
<span data-ttu-id="d645c-139">RHEL 7.2 sanal makine Azure'da sağlandı.</span><span class="sxs-lookup"><span data-stu-id="d645c-139">The RHEL 7.2 virtual machine has been provisioned in Azure.</span></span> <span data-ttu-id="d645c-140">Sonraki görev sanal makineye uzaktan bağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="d645c-140">The next task is to connect remotely to the virtual machine.</span></span>

<span data-ttu-id="d645c-141">**RHEL 7.2 sanal makineye bağlanma** makalesindeki yönergeleri izleyin [Linux çalıştıran bir sanal makine için oturum açma](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d645c-141">**Connect to the RHEL 7.2 virtual machine** Follow the instructions in the article [How to log on to a virtual machine running Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="d645c-142">Geri kalan adımlara varsayalım RHEL sanal makineye bağlanmak için PuTTY SSH istemcisini kullanın.</span><span class="sxs-lookup"><span data-stu-id="d645c-142">The rest of the steps assume you use the PuTTY SSH client to connect to the RHEL virtual machine.</span></span> <span data-ttu-id="d645c-143">Daha fazla bilgi için bkz: [PuTTY indirme sayfası](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="d645c-143">For more information, see the [PuTTY Download page](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

1. <span data-ttu-id="d645c-144">PuTTY programını açın.</span><span class="sxs-lookup"><span data-stu-id="d645c-144">Open the PuTTY program.</span></span>
2. <span data-ttu-id="d645c-145">Girin **ana bilgisayar adı** yeni oluşturulan RHEL sanal makine için.</span><span class="sxs-lookup"><span data-stu-id="d645c-145">Enter the **Host Name** for the newly created RHEL virtual machine.</span></span> <span data-ttu-id="d645c-146">Bu örnekte, sanal makine ana bilgisayar adı 'contoso-rhel.cloudapp .net' sahiptir.</span><span class="sxs-lookup"><span data-stu-id="d645c-146">In this example, our virtual machine has the host name 'contoso-rhel.cloudapp.net'.</span></span> <span data-ttu-id="d645c-147">VM ana bilgisayar adından emin değilseniz, Azure Portal'daki VM panoya bakın.</span><span class="sxs-lookup"><span data-stu-id="d645c-147">If you are not sure of the host name of your VM, refer to the VM dashboard on the Azure portal.</span></span>

    ![PuTTY Bağlan](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-connect.png)
3. <span data-ttu-id="d645c-149">Sanal makineye sanal makinenin oluşturulduğu belirtilen yerel yönetici kimlik bilgilerini kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="d645c-149">Log on to the virtual machine using the local administrator credentials you specified when the virtual machine was created.</span></span> <span data-ttu-id="d645c-150">Bu örnekte, "mahesh" yerel yönetici hesabı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d645c-150">In this example, we used the local administrator account "mahesh".</span></span>

    ![PuTTY oturum açma](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-login.png)

## <a name="install-required-packages-on-the-linux-virtual-machine"></a><span data-ttu-id="d645c-152">Gerekli paketler Linux sanal makineye yükleme</span><span class="sxs-lookup"><span data-stu-id="d645c-152">Install required packages on the Linux virtual machine</span></span>
<span data-ttu-id="d645c-153">Sanal makineye bağlandıktan sonra sonraki görev sanal makinede etki alanına katılma için gerekli paketleri yüklemek için uygundur.</span><span class="sxs-lookup"><span data-stu-id="d645c-153">After connecting to the virtual machine, the next task is to install packages required for domain join on the virtual machine.</span></span> <span data-ttu-id="d645c-154">Aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d645c-154">Perform the following steps:</span></span>

1. <span data-ttu-id="d645c-155">**Realmd yükleyin:** realmd paketi etki alanına katılma için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d645c-155">**Install realmd:** The realmd package is used for domain join.</span></span> <span data-ttu-id="d645c-156">PuTTY terminalinizde aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="d645c-156">In your PuTTY terminal, type the following command:</span></span>

    <span data-ttu-id="d645c-157">sudo yum yükleme realmd</span><span class="sxs-lookup"><span data-stu-id="d645c-157">sudo yum install realmd</span></span>

    ![Realmd yükleyin](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-realmd.png)

    <span data-ttu-id="d645c-159">Birkaç dakika sonra realmd paket sanal makinede yüklü.</span><span class="sxs-lookup"><span data-stu-id="d645c-159">After a few minutes, the realmd package should get installed on the virtual machine.</span></span>

    ![yüklü realmd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-installed.png)
2. <span data-ttu-id="d645c-161">**Sssd yükleyin:** realmd paket etki alanı birleştirme işlemleri gerçekleştirme sssd bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="d645c-161">**Install sssd:** The realmd package depends on sssd to perform domain join operations.</span></span> <span data-ttu-id="d645c-162">PuTTY terminalinizde aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="d645c-162">In your PuTTY terminal, type the following command:</span></span>

    <span data-ttu-id="d645c-163">sudo yum yükleme sssd</span><span class="sxs-lookup"><span data-stu-id="d645c-163">sudo yum install sssd</span></span>

    ![Sssd yükleyin](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-sssd.png)

    <span data-ttu-id="d645c-165">Birkaç dakika sonra sssd paket sanal makinede yüklü.</span><span class="sxs-lookup"><span data-stu-id="d645c-165">After a few minutes, the sssd package should get installed on the virtual machine.</span></span>

    ![yüklü realmd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-sssd-installed.png)
3. <span data-ttu-id="d645c-167">**Kerberos yükleyin:** PuTTY terminalinizde aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="d645c-167">**Install kerberos:** In your PuTTY terminal, type the following command:</span></span>

    <span data-ttu-id="d645c-168">sudo yum yükleme krb5 iş istasyonu krb5-kitaplıklar</span><span class="sxs-lookup"><span data-stu-id="d645c-168">sudo yum install krb5-workstation krb5-libs</span></span>

    ![Kerberos yükleyin](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-kerberos.png)

    <span data-ttu-id="d645c-170">Birkaç dakika sonra realmd paket sanal makinede yüklü.</span><span class="sxs-lookup"><span data-stu-id="d645c-170">After a few minutes, the realmd package should get installed on the virtual machine.</span></span>

    ![Kerberos yüklü](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kerberos-installed.png)

## <a name="join-the-linux-virtual-machine-to-the-managed-domain"></a><span data-ttu-id="d645c-172">Linux sanal makinesini yönetilen bir etki alanına katılma</span><span class="sxs-lookup"><span data-stu-id="d645c-172">Join the Linux virtual machine to the managed domain</span></span>
<span data-ttu-id="d645c-173">Gerekli paketleri Linux sanal makinede yüklü olan, sonraki görev sanal makineyi yönetilen etki alanına belirlemektir.</span><span class="sxs-lookup"><span data-stu-id="d645c-173">Now that the required packages are installed on the Linux virtual machine, the next task is to join the virtual machine to the managed domain.</span></span>

1. <span data-ttu-id="d645c-174">AAD etki alanı Hizmetleri yönetilen etki bulur.</span><span class="sxs-lookup"><span data-stu-id="d645c-174">Discover the AAD Domain Services managed domain.</span></span> <span data-ttu-id="d645c-175">PuTTY terminalinizde aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="d645c-175">In your PuTTY terminal, type the following command:</span></span>

    <span data-ttu-id="d645c-176">sudo bölge CONTOSO100.COM Bul</span><span class="sxs-lookup"><span data-stu-id="d645c-176">sudo realm discover CONTOSO100.COM</span></span>

    ![Bölge Bul](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-discover.png)

    <span data-ttu-id="d645c-178">Varsa **bölge Bul** , yönetilen etki alanını bulmak, etki alanı sanal makine (try ping) erişilebilir olduğundan emin olun alamıyor.</span><span class="sxs-lookup"><span data-stu-id="d645c-178">If **realm discover** is unable to find your managed domain, ensure that the domain is reachable from the virtual machine (try ping).</span></span> <span data-ttu-id="d645c-179">Ayrıca sanal makinenin yönetilen etki alanı kullanılamıyor aynı sanal ağa gerçekten dağıtılmış olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="d645c-179">Also ensure that the virtual machine has indeed been deployed to the same virtual network in which the managed domain is available.</span></span>
2. <span data-ttu-id="d645c-180">Kerberos başlatır.</span><span class="sxs-lookup"><span data-stu-id="d645c-180">Initialize kerberos.</span></span> <span data-ttu-id="d645c-181">PuTTY terminalinizde aşağıdaki komutu yazın.</span><span class="sxs-lookup"><span data-stu-id="d645c-181">In your PuTTY terminal, type the following command.</span></span> <span data-ttu-id="d645c-182">'AAD DC Yöneticiler' grubuna ait bir kullanıcı belirttiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="d645c-182">Ensure that you specify a user who belongs to the 'AAD DC Administrators' group.</span></span> <span data-ttu-id="d645c-183">Yalnızca bu kullanıcıların bilgisayarları yönetilen etki alanına katılmasını sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="d645c-183">Only these users can join computers to the managed domain.</span></span>

    <span data-ttu-id="d645c-184">kinitbob@CONTOSO100.COM</span><span class="sxs-lookup"><span data-stu-id="d645c-184">kinit bob@CONTOSO100.COM</span></span>

    ![Kinit](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kinit.png)

    <span data-ttu-id="d645c-186">Büyük harflerle etki alanı adı belirtin, başka kinit başarısız emin olun.</span><span class="sxs-lookup"><span data-stu-id="d645c-186">Ensure that you specify the domain name in capital letters, else kinit fails.</span></span>
3. <span data-ttu-id="d645c-187">Makine etki alanına katılın.</span><span class="sxs-lookup"><span data-stu-id="d645c-187">Join the machine to the domain.</span></span> <span data-ttu-id="d645c-188">PuTTY terminalinizde aşağıdaki komutu yazın.</span><span class="sxs-lookup"><span data-stu-id="d645c-188">In your PuTTY terminal, type the following command.</span></span> <span data-ttu-id="d645c-189">Önceki adımda ('kinit') belirtilen aynı kullanıcı belirtin.</span><span class="sxs-lookup"><span data-stu-id="d645c-189">Specify the same user you specified in the preceding step ('kinit').</span></span>

    <span data-ttu-id="d645c-190">sudo bölge birleştirme--ayrıntılı CONTOSO100.COM -U 'bob@CONTOSO100.COM'</span><span class="sxs-lookup"><span data-stu-id="d645c-190">sudo realm join --verbose CONTOSO100.COM -U 'bob@CONTOSO100.COM'</span></span>

    ![Bölge birleştirme](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-join.png)

<span data-ttu-id="d645c-192">("Başarılı bir şekilde kaydedilen makine bölgedeki") bir ileti almalısınız zaman makine başarıyla katılırsa yönetilen etki.</span><span class="sxs-lookup"><span data-stu-id="d645c-192">You should get a message ("Successfully enrolled machine in realm") when the machine is successfully joined to the managed domain.</span></span>

## <a name="verify-domain-join"></a><span data-ttu-id="d645c-193">Etki alanına katılma doğrulayın</span><span class="sxs-lookup"><span data-stu-id="d645c-193">Verify domain join</span></span>
<span data-ttu-id="d645c-194">Hızlı bir şekilde makineyi yönetilen bir etki alanına başarıyla katıldı olup olmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="d645c-194">You can quickly verify whether the machine has been successfully joined to the managed domain.</span></span> <span data-ttu-id="d645c-195">Bağlanmak yeni RHEL kullanıcı hesabının doğru şekilde giderilip giderilmediğini görmek için SSH ve bir etki alanı kullanıcı hesabı ve ardından onay kullanarak VM etki alanına katıldı.</span><span class="sxs-lookup"><span data-stu-id="d645c-195">Connect to the newly domain joined RHEL VM using SSH and a domain user account and then check to see if the user account is resolved correctly.</span></span>

1. <span data-ttu-id="d645c-196">PuTTY terminalinizde bağlanmak için aşağıdaki komutu yazın yeni SSH kullanarak RHEL sanal makine etki alanına katıldı.</span><span class="sxs-lookup"><span data-stu-id="d645c-196">In your PuTTY terminal, type the following command to connect to the newly domain joined RHEL virtual machine using SSH.</span></span> <span data-ttu-id="d645c-197">Yönetilen etki alanına ait bir etki alanı hesabı kullanın (örneğin, 'bob@CONTOSO100.COM' Bu durumda.)</span><span class="sxs-lookup"><span data-stu-id="d645c-197">Use a domain account that belongs to the managed domain (for example, 'bob@CONTOSO100.COM' in this case.)</span></span>

    <span data-ttu-id="d645c-198">SSH -l bob@CONTOSO100.COM contoso rhel.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="d645c-198">ssh -l bob@CONTOSO100.COM contoso-rhel.cloudapp.net</span></span>
2. <span data-ttu-id="d645c-199">PuTTY terminalinizde giriş dizini doğru başlatılmadı görmek için aşağıdaki komutu yazın.</span><span class="sxs-lookup"><span data-stu-id="d645c-199">In your PuTTY terminal, type the following command to see if the home directory was initialized correctly.</span></span>

    <span data-ttu-id="d645c-200">pwd</span><span class="sxs-lookup"><span data-stu-id="d645c-200">pwd</span></span>
3. <span data-ttu-id="d645c-201">PuTTY terminalinizde grup üyeliklerini doğru çözüldüğünü olmadığını görmek için aşağıdaki komutu yazın.</span><span class="sxs-lookup"><span data-stu-id="d645c-201">In your PuTTY terminal, type the following command to see if the group memberships are being resolved correctly.</span></span>

    <span data-ttu-id="d645c-202">id</span><span class="sxs-lookup"><span data-stu-id="d645c-202">id</span></span>

<span data-ttu-id="d645c-203">Bu komutların örnek bir çıktı aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="d645c-203">A sample output of these commands follows:</span></span>

![Etki alanına katılma doğrulayın](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-verify-domain-join.png)

## <a name="troubleshooting-domain-join"></a><span data-ttu-id="d645c-205">Sorun giderme etki alanına katılma</span><span class="sxs-lookup"><span data-stu-id="d645c-205">Troubleshooting domain join</span></span>
<span data-ttu-id="d645c-206">Başvurmak [sorun giderme etki alanına katılma](active-directory-ds-admin-guide-join-windows-vm.md#troubleshooting-domain-join) makalesi.</span><span class="sxs-lookup"><span data-stu-id="d645c-206">Refer to the [Troubleshooting domain join](active-directory-ds-admin-guide-join-windows-vm.md#troubleshooting-domain-join) article.</span></span>

## <a name="related-content"></a><span data-ttu-id="d645c-207">İlgili İçerik</span><span class="sxs-lookup"><span data-stu-id="d645c-207">Related Content</span></span>
* [<span data-ttu-id="d645c-208">Azure AD etki alanı Hizmetleri - başlangıç kılavuzu</span><span class="sxs-lookup"><span data-stu-id="d645c-208">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="d645c-209">Bir Windows Server sanal makine bir Azure AD etki alanı Hizmetleri yönetilen etki alanına katılma</span><span class="sxs-lookup"><span data-stu-id="d645c-209">Join a Windows Server virtual machine to an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* <span data-ttu-id="d645c-210">[Linux çalıştıran bir sanal makine için oturum açma](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d645c-210">[How to log on to a virtual machine running Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* [<span data-ttu-id="d645c-211">Kerberos yükleme</span><span class="sxs-lookup"><span data-stu-id="d645c-211">Installing Kerberos</span></span>](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Managing_Smart_Cards/installing-kerberos.html)
* [<span data-ttu-id="d645c-212">Red Hat Enterprise Linux 7 - Windows tümleştirme Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="d645c-212">Red Hat Enterprise Linux 7 - Windows Integration Guide</span></span>](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Windows_Integration_Guide/index.html)
