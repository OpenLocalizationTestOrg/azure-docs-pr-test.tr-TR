---
title: "Azure Active Directory etki alanı Hizmetleri: RHEL VM tooa yönetilen etki alanına Katıl | Microsoft Docs"
description: "Red Hat Enterprise Linux sanal makine birleştirme tooAzure AD etki alanı Hizmetleri"
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
ms.openlocfilehash: 41ca2aaf2eefbf9c403d2b834d61a1aa0943d950
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-red-hat-enterprise-linux-7-virtual-machine-tooa-managed-domain"></a><span data-ttu-id="f41d8-103">Red Hat Enterprise Linux 7 sanal makine tooa yönetilen etki alanına Katıl</span><span class="sxs-lookup"><span data-stu-id="f41d8-103">Join a Red Hat Enterprise Linux 7 virtual machine tooa managed domain</span></span>
<span data-ttu-id="f41d8-104">Bu makalede toojoin Red Hat Enterprise Linux (RHEL) 7 sanal makine tooan Azure AD etki alanı Hizmetleri etki alanı nasıl yönetileceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="f41d8-104">This article shows you how toojoin a Red Hat Enterprise Linux (RHEL) 7 virtual machine tooan Azure AD Domain Services managed domain.</span></span>

## <a name="provision-a-red-hat-enterprise-linux-virtual-machine"></a><span data-ttu-id="f41d8-105">Red Hat Enterprise Linux sanal makine sağlama</span><span class="sxs-lookup"><span data-stu-id="f41d8-105">Provision a Red Hat Enterprise Linux virtual machine</span></span>
<span data-ttu-id="f41d8-106">Hello Azure portal kullanarak adımları tooprovision RHEL 7 sanal makine aşağıdaki hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="f41d8-106">Perform hello following steps tooprovision a RHEL 7 virtual machine using hello Azure portal.</span></span>

1. <span data-ttu-id="f41d8-107">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f41d8-107">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

    ![Azure portalı panosunun](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-dashboard.png)
2. <span data-ttu-id="f41d8-109">Tıklatın **yeni** sol bölmesinde ve türü hello üzerinde **Red Hat** hello ekran aşağıdaki gösterildiği gibi hello arama çubuğunu içine.</span><span class="sxs-lookup"><span data-stu-id="f41d8-109">Click **New** on hello left pane and type **Red Hat** into hello search bar as shown in hello following screenshot.</span></span> <span data-ttu-id="f41d8-110">Red Hat Enterprise Linux girişleri hello arama sonuçlarında görünür.</span><span class="sxs-lookup"><span data-stu-id="f41d8-110">Entries for Red Hat Enterprise Linux appear in hello search results.</span></span> <span data-ttu-id="f41d8-111">Tıklatın **Red Hat Enterprise Linux 7.2**.</span><span class="sxs-lookup"><span data-stu-id="f41d8-111">Click **Red Hat Enterprise Linux 7.2**.</span></span>

    ![RHEL sonuçlarında seçin](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-find-rhel-image.png)
3. <span data-ttu-id="f41d8-113">Merhaba arama sonuçları hello **her şeyi** bölmesinde hello Red Hat Enterprise Linux 7.2 görüntü listesinde.</span><span class="sxs-lookup"><span data-stu-id="f41d8-113">hello search results in hello **Everything** pane should list hello Red Hat Enterprise Linux 7.2 image.</span></span> <span data-ttu-id="f41d8-114">Tıklatın **Red Hat Enterprise Linux 7.2** tooview hello sanal makine görüntüsü hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="f41d8-114">Click **Red Hat Enterprise Linux 7.2** tooview more information about hello virtual machine image.</span></span>

    ![RHEL sonuçlarında seçin](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-rhel-image.png)
4. <span data-ttu-id="f41d8-116">Merhaba, **Red Hat Enterprise Linux 7.2** bölmesinde hello sanal makine görüntüsü hakkında daha fazla bilgi görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f41d8-116">In hello **Red Hat Enterprise Linux 7.2** pane, you should see more information about hello virtual machine image.</span></span> <span data-ttu-id="f41d8-117">Merhaba, **dağıtım modeli seçin** açılan listesinde, select **Klasik**.</span><span class="sxs-lookup"><span data-stu-id="f41d8-117">In hello **Select a deployment model** dropdown, select **Classic**.</span></span> <span data-ttu-id="f41d8-118">Merhaba ardından **oluşturma** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f41d8-118">Then click hello **Create** button.</span></span>

    ![Görüntü ayrıntıları görüntüle](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-clicked.png)
5. <span data-ttu-id="f41d8-120">Merhaba, **Temelleri** hello sayfasının **sanal makine oluşturma** Sihirbazı'nı hello girin **ana bilgisayar adı** hello yeni sanal makine için.</span><span class="sxs-lookup"><span data-stu-id="f41d8-120">In hello **Basics** page of hello **Create virtual machine** wizard, enter hello **Host Name** for hello new virtual machine.</span></span> <span data-ttu-id="f41d8-121">Ayrıca bir yerel yönetici kullanıcı adı hello belirtin **kullanıcı adı** alan ve **parola**.</span><span class="sxs-lookup"><span data-stu-id="f41d8-121">Also specify a local administrator user name in hello **User name** field and a **Password**.</span></span> <span data-ttu-id="f41d8-122">SSH anahtar tooauthenticate hello yerel yönetici kullanıcı toouse de seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f41d8-122">You may also choose toouse an SSH key tooauthenticate hello local administrator user.</span></span> <span data-ttu-id="f41d8-123">Ayrıca bir **fiyatlandırma katmanı** hello sanal makine için.</span><span class="sxs-lookup"><span data-stu-id="f41d8-123">Also select a **Pricing Tier** for hello virtual machine.</span></span>

    ![VM - temelleri sayfa oluşturma](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-basic-details.png)
6. <span data-ttu-id="f41d8-125">Merhaba, **boyutu** hello sayfasının **sanal makine oluşturma** hello sanal makinenin seçin hello boyutu.</span><span class="sxs-lookup"><span data-stu-id="f41d8-125">In hello **Size** page of hello **Create virtual machine** wizard, select hello size for hello virtual machine.</span></span>

    ![VM - select boyutu oluşturun](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-vm-size.png)

7. <span data-ttu-id="f41d8-127">Merhaba, **ayarları** hello sayfasının **sanal makine oluşturma** seçin hello hello sanal makinesi için depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="f41d8-127">In hello **Settings** page of hello **Create virtual machine** wizard, select hello storage account for hello virtual machine.</span></span> <span data-ttu-id="f41d8-128">Tıklatın **sanal ağ** tooselect hello sanal ağ toowhich hello Linux VM dağıtılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f41d8-128">Click **Virtual Network** tooselect hello virtual network toowhich hello Linux VM should be deployed.</span></span> <span data-ttu-id="f41d8-129">Merhaba, **sanal ağ** dikey penceresinde, select hello sanal ağ içinde Azure AD etki alanı Hizmetleri kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f41d8-129">In hello **Virtual Network** blade, select hello virtual network in which Azure AD Domain Services is available.</span></span> <span data-ttu-id="f41d8-130">Bu örnekte, hello 'MyPreviewVNet' sanal ağ seçin.</span><span class="sxs-lookup"><span data-stu-id="f41d8-130">In this example, we pick hello 'MyPreviewVNet' virtual network.</span></span>

    ![VM oluşturma - sanal ağı seçin](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-select-vnet.png)
8. <span data-ttu-id="f41d8-132">Merhaba üzerinde **Özet** hello sayfasının **sanal makine oluşturma** Sihirbazı, gözden geçirme ve tıklatın hello **Tamam** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f41d8-132">On hello **Summary** page of hello **Create virtual machine** wizard, review and click hello **OK** button.</span></span>

    ![VM - seçilen sanal ağ oluşturma](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-vnet-selected.png)
9. <span data-ttu-id="f41d8-134">Merhaba yeni sanal makine hello RHEL 7.2 görüntüyü temel alarak dağıtımını başlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f41d8-134">Deployment of hello new virtual machine based on hello RHEL 7.2 image should start.</span></span>

    ![VM - Dağıtım başladı oluşturma](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployment-started.png)
10. <span data-ttu-id="f41d8-136">Birkaç dakika sonra hello sanal makine başarıyla dağıtılan ve kullanılmaya hazır olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f41d8-136">After a few minutes, hello virtual machine should be deployed successfully and ready for use.</span></span>

    ![Dağıtılan VM - oluşturma](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployed.png)

## <a name="connect-remotely-toohello-newly-provisioned-linux-virtual-machine"></a><span data-ttu-id="f41d8-138">Yeni sağlanan toohello Linux sanal makine uzaktan bağlanma</span><span class="sxs-lookup"><span data-stu-id="f41d8-138">Connect remotely toohello newly provisioned Linux virtual machine</span></span>
<span data-ttu-id="f41d8-139">Azure'da Hello RHEL 7.2 sanal makine sağlandı.</span><span class="sxs-lookup"><span data-stu-id="f41d8-139">hello RHEL 7.2 virtual machine has been provisioned in Azure.</span></span> <span data-ttu-id="f41d8-140">Merhaba sonraki görevdir tooconnect uzaktan toohello sanal makine.</span><span class="sxs-lookup"><span data-stu-id="f41d8-140">hello next task is tooconnect remotely toohello virtual machine.</span></span>

<span data-ttu-id="f41d8-141">**Toohello RHEL 7.2 sanal makineye bağlanmak** hello makalede hello yönergeleri izleyerek [nasıl toolog Linux çalıştıran tooa sanal makine üzerinde](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f41d8-141">**Connect toohello RHEL 7.2 virtual machine** Follow hello instructions in hello article [How toolog on tooa virtual machine running Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="f41d8-142">Merhaba adımları Hello kalan varsayalım hello PuTTY SSH istemcisini tooconnect toohello RHEL sanal makine kullanın.</span><span class="sxs-lookup"><span data-stu-id="f41d8-142">hello rest of hello steps assume you use hello PuTTY SSH client tooconnect toohello RHEL virtual machine.</span></span> <span data-ttu-id="f41d8-143">Daha fazla bilgi için bkz: Merhaba [PuTTY indirme sayfası](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="f41d8-143">For more information, see hello [PuTTY Download page](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

1. <span data-ttu-id="f41d8-144">Açık hello PuTTY program.</span><span class="sxs-lookup"><span data-stu-id="f41d8-144">Open hello PuTTY program.</span></span>
2. <span data-ttu-id="f41d8-145">Merhaba girin **ana bilgisayar adı** RHEL sanal makine yeni oluşturulan hello için.</span><span class="sxs-lookup"><span data-stu-id="f41d8-145">Enter hello **Host Name** for hello newly created RHEL virtual machine.</span></span> <span data-ttu-id="f41d8-146">Bu örnekte, sanal makine hello ana bilgisayar adı 'contoso-rhel.cloudapp .net' sahiptir.</span><span class="sxs-lookup"><span data-stu-id="f41d8-146">In this example, our virtual machine has hello host name 'contoso-rhel.cloudapp.net'.</span></span> <span data-ttu-id="f41d8-147">Vm'nizin ana bilgisayar adı hello emin değilseniz, toohello VM hello Azure portal panosunda bakın.</span><span class="sxs-lookup"><span data-stu-id="f41d8-147">If you are not sure of hello host name of your VM, refer toohello VM dashboard on hello Azure portal.</span></span>

    ![PuTTY Bağlan](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-connect.png)
3. <span data-ttu-id="f41d8-149">Toohello sanal makineyi hello sanal makineyi oluşturduğunuzda belirttiğiniz hello yerel yönetici kimlik bilgilerini kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="f41d8-149">Log on toohello virtual machine using hello local administrator credentials you specified when hello virtual machine was created.</span></span> <span data-ttu-id="f41d8-150">Bu örnekte, "mahesh" Merhaba yerel yönetici hesabı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f41d8-150">In this example, we used hello local administrator account "mahesh".</span></span>

    ![PuTTY oturum açma](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-login.png)

## <a name="install-required-packages-on-hello-linux-virtual-machine"></a><span data-ttu-id="f41d8-152">Gerekli paketler hello Linux sanal makineye yükleme</span><span class="sxs-lookup"><span data-stu-id="f41d8-152">Install required packages on hello Linux virtual machine</span></span>
<span data-ttu-id="f41d8-153">Bağlantı toohello sanal makine sonra hello sonraki tooinstall paketleri hello sanal makine üzerinde etki alanına katılma için gerekli bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="f41d8-153">After connecting toohello virtual machine, hello next task is tooinstall packages required for domain join on hello virtual machine.</span></span> <span data-ttu-id="f41d8-154">Merhaba aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="f41d8-154">Perform hello following steps:</span></span>

1. <span data-ttu-id="f41d8-155">**Realmd yükleyin:** hello realmd paket etki alanına katılma için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f41d8-155">**Install realmd:** hello realmd package is used for domain join.</span></span> <span data-ttu-id="f41d8-156">PuTTY terminalinizde hello aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="f41d8-156">In your PuTTY terminal, type hello following command:</span></span>

    <span data-ttu-id="f41d8-157">sudo yum yükleme realmd</span><span class="sxs-lookup"><span data-stu-id="f41d8-157">sudo yum install realmd</span></span>

    ![Realmd yükleyin](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-realmd.png)

    <span data-ttu-id="f41d8-159">Birkaç dakika sonra hello realmd paket hello sanal makinede yüklü.</span><span class="sxs-lookup"><span data-stu-id="f41d8-159">After a few minutes, hello realmd package should get installed on hello virtual machine.</span></span>

    ![yüklü realmd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-installed.png)
2. <span data-ttu-id="f41d8-161">**Sssd yükleyin:** hello realmd paket sssd tooperform etki alanına katılma işlemleri bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="f41d8-161">**Install sssd:** hello realmd package depends on sssd tooperform domain join operations.</span></span> <span data-ttu-id="f41d8-162">PuTTY terminalinizde hello aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="f41d8-162">In your PuTTY terminal, type hello following command:</span></span>

    <span data-ttu-id="f41d8-163">sudo yum yükleme sssd</span><span class="sxs-lookup"><span data-stu-id="f41d8-163">sudo yum install sssd</span></span>

    ![Sssd yükleyin](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-sssd.png)

    <span data-ttu-id="f41d8-165">Birkaç dakika sonra hello sssd paket hello sanal makinede yüklü.</span><span class="sxs-lookup"><span data-stu-id="f41d8-165">After a few minutes, hello sssd package should get installed on hello virtual machine.</span></span>

    ![yüklü realmd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-sssd-installed.png)
3. <span data-ttu-id="f41d8-167">**Kerberos yükleyin:** PuTTY terminalinizde hello aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="f41d8-167">**Install kerberos:** In your PuTTY terminal, type hello following command:</span></span>

    <span data-ttu-id="f41d8-168">sudo yum yükleme krb5 iş istasyonu krb5-kitaplıklar</span><span class="sxs-lookup"><span data-stu-id="f41d8-168">sudo yum install krb5-workstation krb5-libs</span></span>

    ![Kerberos yükleyin](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-kerberos.png)

    <span data-ttu-id="f41d8-170">Birkaç dakika sonra hello realmd paket hello sanal makinede yüklü.</span><span class="sxs-lookup"><span data-stu-id="f41d8-170">After a few minutes, hello realmd package should get installed on hello virtual machine.</span></span>

    ![Kerberos yüklü](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kerberos-installed.png)

## <a name="join-hello-linux-virtual-machine-toohello-managed-domain"></a><span data-ttu-id="f41d8-172">Merhaba Linux sanal makine toohello yönetilen etki alanına katılma</span><span class="sxs-lookup"><span data-stu-id="f41d8-172">Join hello Linux virtual machine toohello managed domain</span></span>
<span data-ttu-id="f41d8-173">Merhaba Linux sanal makinede yüklü gerekli hello paketlerini, hello sonraki görev toojoin hello sanal makine toohello yönetilen etki alanıdır.</span><span class="sxs-lookup"><span data-stu-id="f41d8-173">Now that hello required packages are installed on hello Linux virtual machine, hello next task is toojoin hello virtual machine toohello managed domain.</span></span>

1. <span data-ttu-id="f41d8-174">Merhaba AAD etki alanı Hizmetleri yönetilen etki bulur.</span><span class="sxs-lookup"><span data-stu-id="f41d8-174">Discover hello AAD Domain Services managed domain.</span></span> <span data-ttu-id="f41d8-175">PuTTY terminalinizde hello aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="f41d8-175">In your PuTTY terminal, type hello following command:</span></span>

    <span data-ttu-id="f41d8-176">sudo bölge CONTOSO100.COM Bul</span><span class="sxs-lookup"><span data-stu-id="f41d8-176">sudo realm discover CONTOSO100.COM</span></span>

    ![Bölge Bul](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-discover.png)

    <span data-ttu-id="f41d8-178">Varsa **bölge Bul** oluşturulamıyor toofind, yönetilen etki alanıdır hello etki hello sanal makineden (try ping) erişilebilir olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="f41d8-178">If **realm discover** is unable toofind your managed domain, ensure that hello domain is reachable from hello virtual machine (try ping).</span></span> <span data-ttu-id="f41d8-179">Ayrıca hello sanal makinede dağıtılan toohello gerçekten açıldı olun aynı sanal ağda hangi hello yönetilen etki alanı kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f41d8-179">Also ensure that hello virtual machine has indeed been deployed toohello same virtual network in which hello managed domain is available.</span></span>
2. <span data-ttu-id="f41d8-180">Kerberos başlatır.</span><span class="sxs-lookup"><span data-stu-id="f41d8-180">Initialize kerberos.</span></span> <span data-ttu-id="f41d8-181">PuTTY terminalinizde hello aşağıdaki komutu yazın.</span><span class="sxs-lookup"><span data-stu-id="f41d8-181">In your PuTTY terminal, type hello following command.</span></span> <span data-ttu-id="f41d8-182">Toohello 'AAD DC Yöneticiler' grubuna üye olduğu bir kullanıcı belirttiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="f41d8-182">Ensure that you specify a user who belongs toohello 'AAD DC Administrators' group.</span></span> <span data-ttu-id="f41d8-183">Yalnızca bu kullanıcılar, bilgisayarlar toohello yönetilen etki alanına eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="f41d8-183">Only these users can join computers toohello managed domain.</span></span>

    <span data-ttu-id="f41d8-184">kinitbob@CONTOSO100.COM</span><span class="sxs-lookup"><span data-stu-id="f41d8-184">kinit bob@CONTOSO100.COM</span></span>

    ![Kinit](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kinit.png)

    <span data-ttu-id="f41d8-186">Büyük harflerle hello etki alanı adı belirtin, başka kinit başarısız emin olun.</span><span class="sxs-lookup"><span data-stu-id="f41d8-186">Ensure that you specify hello domain name in capital letters, else kinit fails.</span></span>
3. <span data-ttu-id="f41d8-187">Merhaba makine toohello etki alanına katılın.</span><span class="sxs-lookup"><span data-stu-id="f41d8-187">Join hello machine toohello domain.</span></span> <span data-ttu-id="f41d8-188">PuTTY terminalinizde hello aşağıdaki komutu yazın.</span><span class="sxs-lookup"><span data-stu-id="f41d8-188">In your PuTTY terminal, type hello following command.</span></span> <span data-ttu-id="f41d8-189">Merhaba belirtin aynı kullanıcı hello önceki adım ('kinit') belirtildi.</span><span class="sxs-lookup"><span data-stu-id="f41d8-189">Specify hello same user you specified in hello preceding step ('kinit').</span></span>

    <span data-ttu-id="f41d8-190">sudo bölge birleştirme--ayrıntılı CONTOSO100.COM -U 'bob@CONTOSO100.COM'</span><span class="sxs-lookup"><span data-stu-id="f41d8-190">sudo realm join --verbose CONTOSO100.COM -U 'bob@CONTOSO100.COM'</span></span>

    ![Bölge birleştirme](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-join.png)

<span data-ttu-id="f41d8-192">("Başarılı bir şekilde kaydedilen makine bölgedeki") bir ileti almalısınız hello makine başarıyla katıldı toohello yönetilen etki alanında olduğunda.</span><span class="sxs-lookup"><span data-stu-id="f41d8-192">You should get a message ("Successfully enrolled machine in realm") when hello machine is successfully joined toohello managed domain.</span></span>

## <a name="verify-domain-join"></a><span data-ttu-id="f41d8-193">Etki alanına katılma doğrulayın</span><span class="sxs-lookup"><span data-stu-id="f41d8-193">Verify domain join</span></span>
<span data-ttu-id="f41d8-194">Hızlı bir şekilde hello makine başarıyla katıldı toohello yönetilen etki alanı olup olmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="f41d8-194">You can quickly verify whether hello machine has been successfully joined toohello managed domain.</span></span> <span data-ttu-id="f41d8-195">Toohello bağlanmak yeni RHEL hello kullanıcı hesabının doğru şekilde giderilip giderilmediğini SSH ve bir etki alanı kullanıcı hesabı ve ardından onay toosee kullanarak VM etki alanına katıldı.</span><span class="sxs-lookup"><span data-stu-id="f41d8-195">Connect toohello newly domain joined RHEL VM using SSH and a domain user account and then check toosee if hello user account is resolved correctly.</span></span>

1. <span data-ttu-id="f41d8-196">PuTTY içinde terminal, komut tooconnect toohello yeni aşağıdaki türü hello SSH kullanarak RHEL sanal makine etki alanına katıldı.</span><span class="sxs-lookup"><span data-stu-id="f41d8-196">In your PuTTY terminal, type hello following command tooconnect toohello newly domain joined RHEL virtual machine using SSH.</span></span> <span data-ttu-id="f41d8-197">Toohello yönetilen etki alanına ait bir etki alanı hesabı kullanın (örneğin, 'bob@CONTOSO100.COM' Bu durumda.)</span><span class="sxs-lookup"><span data-stu-id="f41d8-197">Use a domain account that belongs toohello managed domain (for example, 'bob@CONTOSO100.COM' in this case.)</span></span>

    <span data-ttu-id="f41d8-198">SSH -l bob@CONTOSO100.COM contoso rhel.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="f41d8-198">ssh -l bob@CONTOSO100.COM contoso-rhel.cloudapp.net</span></span>
2. <span data-ttu-id="f41d8-199">PuTTY terminalinizde hello giriş dizini doğru başlatılmadı komutu toosee izlemeyi hello yazın.</span><span class="sxs-lookup"><span data-stu-id="f41d8-199">In your PuTTY terminal, type hello following command toosee if hello home directory was initialized correctly.</span></span>

    <span data-ttu-id="f41d8-200">pwd</span><span class="sxs-lookup"><span data-stu-id="f41d8-200">pwd</span></span>
3. <span data-ttu-id="f41d8-201">PuTTY terminalinizde hello grup üyeliklerini doğru çözüldüğünü komutu toosee izlemeyi hello yazın.</span><span class="sxs-lookup"><span data-stu-id="f41d8-201">In your PuTTY terminal, type hello following command toosee if hello group memberships are being resolved correctly.</span></span>

    <span data-ttu-id="f41d8-202">id</span><span class="sxs-lookup"><span data-stu-id="f41d8-202">id</span></span>

<span data-ttu-id="f41d8-203">Bu komutların örnek bir çıktı aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="f41d8-203">A sample output of these commands follows:</span></span>

![Etki alanına katılma doğrulayın](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-verify-domain-join.png)

## <a name="troubleshooting-domain-join"></a><span data-ttu-id="f41d8-205">Sorun giderme etki alanına katılma</span><span class="sxs-lookup"><span data-stu-id="f41d8-205">Troubleshooting domain join</span></span>
<span data-ttu-id="f41d8-206">Toohello başvuran [sorun giderme etki alanına katılma](active-directory-ds-admin-guide-join-windows-vm.md#troubleshooting-domain-join) makalesi.</span><span class="sxs-lookup"><span data-stu-id="f41d8-206">Refer toohello [Troubleshooting domain join](active-directory-ds-admin-guide-join-windows-vm.md#troubleshooting-domain-join) article.</span></span>

## <a name="related-content"></a><span data-ttu-id="f41d8-207">İlgili İçerik</span><span class="sxs-lookup"><span data-stu-id="f41d8-207">Related Content</span></span>
* [<span data-ttu-id="f41d8-208">Azure AD etki alanı Hizmetleri - başlangıç kılavuzu</span><span class="sxs-lookup"><span data-stu-id="f41d8-208">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="f41d8-209">Windows Server sanal makine tooan Azure AD etki alanı Hizmetleri yönetilen etki alanına Katıl</span><span class="sxs-lookup"><span data-stu-id="f41d8-209">Join a Windows Server virtual machine tooan Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* <span data-ttu-id="f41d8-210">[Nasıl toolog Linux çalıştıran tooa sanal makine üzerinde](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f41d8-210">[How toolog on tooa virtual machine running Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* [<span data-ttu-id="f41d8-211">Kerberos yükleme</span><span class="sxs-lookup"><span data-stu-id="f41d8-211">Installing Kerberos</span></span>](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Managing_Smart_Cards/installing-kerberos.html)
* [<span data-ttu-id="f41d8-212">Red Hat Enterprise Linux 7 - Windows tümleştirme Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="f41d8-212">Red Hat Enterprise Linux 7 - Windows Integration Guide</span></span>](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Windows_Integration_Guide/index.html)
