---
title: "Azure yedekleme sunucusu VMware sunucularıyla yukarı aaaBack | Microsoft Docs"
description: "Azure yedekleme sunucusu tooback bir VMware vCenter/ESXi sunucuları tooAzure veya disk kullanın. Bu makalede adımı sağlar yedekleme (veya koruma) için adım adım yönerge = VMware iş yükleri."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
ms.assetid: 6b131caf-de85-4eba-b8e6-d8a04545cd9d
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/24/2017
ms.author: markgal;
ms.openlocfilehash: 3edb6880a526ed0b18605fee0fac27196a608e7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-vmware-server-tooazure"></a><span data-ttu-id="b7b0e-104">VMware server tooAzure yedekleyin</span><span class="sxs-lookup"><span data-stu-id="b7b0e-104">Back up a VMware server tooAzure</span></span>

<span data-ttu-id="b7b0e-105">Bu makalede korunmasına nasıl yardımcı tooconfigure Azure yedekleme sunucusu toohelp VMware sunucu iş yükleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-105">This article explains how tooconfigure Azure Backup Server toohelp protect VMware server workloads.</span></span> <span data-ttu-id="b7b0e-106">Bu makalede Azure yedekleme sunucusu zaten olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-106">This article assumes you already have Azure Backup Server installed.</span></span> <span data-ttu-id="b7b0e-107">Azure yedekleme sunucusu sahip değilseniz, bkz: [tooback Azure yedekleme sunucusu kullanarak iş yüklerini hazırlama](backup-azure-microsoft-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="b7b0e-107">If you don't have Azure Backup Server installed, see [Prepare tooback up workloads using Azure Backup Server](backup-azure-microsoft-azure-backup.md).</span></span>

<span data-ttu-id="b7b0e-108">Azure yedekleme sunucusu yedeklemek veya VMware vCenter Server sürüm 6.5, 6.0 ve 5.5 korunmasına yardımcı olma.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-108">Azure Backup Server can back up, or help protect, VMware vCenter Server version 6.5, 6.0 and 5.5.</span></span>


## <a name="create-a-secure-connection-toohello-vcenter-server"></a><span data-ttu-id="b7b0e-109">Güvenli bağlantı toohello vCenter sunucusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="b7b0e-109">Create a secure connection toohello vCenter Server</span></span>

<span data-ttu-id="b7b0e-110">Varsayılan olarak, Azure yedekleme sunucusu her bir HTTPS kanaldan vCenter Server ile iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-110">By default, Azure Backup Server communicates with each vCenter Server via an HTTPS channel.</span></span> <span data-ttu-id="b7b0e-111">tooturn hello güvenli iletişimi Azure yedekleme sunucusuna hello VMware sertifika yetkilisi (CA) sertifikası yüklemeniz önerilir.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-111">tooturn on hello secure communication, we recommend that you install hello VMware Certificate Authority (CA) certificate on Azure Backup Server.</span></span> <span data-ttu-id="b7b0e-112">Güvenli iletişim gerektirmez ve toodisable hello HTTPS gereksinimi tercih ediyorsanız, bkz: [devre dışı bırak güvenli iletişim protokolü](backup-azure-backup-server-vmware.md#disable-secure-communication-protocol).</span><span class="sxs-lookup"><span data-stu-id="b7b0e-112">If you don't require secure communication, and would prefer toodisable hello HTTPS requirement, see [Disable secure communication protocol](backup-azure-backup-server-vmware.md#disable-secure-communication-protocol).</span></span> <span data-ttu-id="b7b0e-113">Azure yedekleme sunucusu hello vCenter sunucusu arasında güvenli bir bağlantı toocreate hello Azure yedekleme sunucusu güvenilen sertifika içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-113">toocreate a secure connection between Azure Backup Server and hello vCenter Server, import hello trusted certificate on Azure Backup Server.</span></span>

<span data-ttu-id="b7b0e-114">Genellikle, hello vSphere Web istemcisi aracılığıyla hello Azure yedekleme sunucusu makine tooconnect toohello vCenter Server sunucusunda bir tarayıcı kullanın.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-114">Typically, you use a browser on hello Azure Backup Server machine tooconnect toohello vCenter Server via hello vSphere Web Client.</span></span> <span data-ttu-id="b7b0e-115">Merhaba hello Azure yedekleme sunucusu tarayıcı tooconnect toohello vCenter sunucusu, ilk kullanışınızda hello bağlantı güvenli değil.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-115">hello first time you use hello Azure Backup Server browser tooconnect toohello vCenter Server, hello connection isn't secure.</span></span> <span data-ttu-id="b7b0e-116">Görüntü aşağıdaki hello hello güvenli bağlantı gösterir.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-116">hello following image shows hello unsecured connection.</span></span>

![Güvenli bağlantı tooVMware sunucusu örneği](./media/backup-azure-backup-server-vmware/unsecure-url.png)

<span data-ttu-id="b7b0e-118">toofix Bu sorun ve güvenli bir bağlantı oluşturmak, hello güvenilen kök CA sertifikaları indirin.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-118">toofix this issue, and create a secure connection, download hello trusted root CA certificates.</span></span>

1. <span data-ttu-id="b7b0e-119">Azure yedekleme sunucusu üzerinde Hello tarayıcıda hello URL toohello vSphere Web istemcisi girin.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-119">In hello browser on Azure Backup Server, enter hello URL toohello vSphere Web Client.</span></span> <span data-ttu-id="b7b0e-120">Merhaba vSphere Web istemci oturum açma sayfası görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-120">hello vSphere Web Client login page appears.</span></span>

    ![vSphere Web istemcisi](./media/backup-azure-backup-server-vmware/vsphere-web-client.png)

    <span data-ttu-id="b7b0e-122">Yöneticiler ve geliştiriciler için hello bilgiler Hello altındaki hello bulun **indirme güvenilen kök CA sertifikaları** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-122">At hello bottom of hello information for administrators and developers, locate hello **Download trusted root CA certificates** link.</span></span>

    ![Bağlantı toodownload hello güvenilen kök CA sertifikaları](./media/backup-azure-backup-server-vmware/vmware-download-ca-cert-prompt.png)

  <span data-ttu-id="b7b0e-124">Merhaba vSphere Web istemci oturum açma sayfası görmüyorsanız, tarayıcınızın proxy ayarlarını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-124">If you don't see hello vSphere Web Client login page, check your browser's proxy settings.</span></span>

2. <span data-ttu-id="b7b0e-125">Tıklatın **indirme güvenilen kök CA sertifikaları**.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-125">Click **Download trusted root CA certificates**.</span></span>

    <span data-ttu-id="b7b0e-126">Merhaba vCenter Server dosya tooyour yerel bilgisayara yükler.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-126">hello vCenter Server downloads a file tooyour local computer.</span></span> <span data-ttu-id="b7b0e-127">Merhaba dosya adının adlı **karşıdan**.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-127">hello file's name is named **download**.</span></span> <span data-ttu-id="b7b0e-128">Tarayıcınıza bağlı olarak, aldığınız soran bir ileti olup olmadığını tooopen veya hello dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-128">Depending on your browser, you receive a message that asks whether tooopen or save hello file.</span></span>

    ![sertifikaları indirildiğinde iletiyi yükle](./media/backup-azure-backup-server-vmware/download-certs.png)

3. <span data-ttu-id="b7b0e-130">Merhaba dosya tooa konumu Azure yedekleme sunucusuna kaydedin.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-130">Save hello file tooa location on Azure Backup Server.</span></span> <span data-ttu-id="b7b0e-131">Merhaba dosyasını kaydettiğinizde, hello .zip dosya adı uzantısına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-131">When you save hello file, add hello .zip file name extension.</span></span>

    <span data-ttu-id="b7b0e-132">Merhaba, hello hello sertifikalar hakkında bilgi içeren bir .zip dosyası dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-132">hello file is a .zip file that contains hello information about hello certificates.</span></span> <span data-ttu-id="b7b0e-133">Merhaba .zip uzantısı ile Merhaba ayıklama araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-133">With hello .zip extension, you can use hello extraction tools.</span></span>

4. <span data-ttu-id="b7b0e-134">Sağ **download.zip**ve ardından **tümünü Ayıkla** tooextract hello içeriği.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-134">Right-click **download.zip**, and then select **Extract All** tooextract hello contents.</span></span>

    <span data-ttu-id="b7b0e-135">Merhaba .zip dosyasını ayıklar adlı içeriği tooa klasörü **sertifikaları**.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-135">hello .zip file extracts its contents tooa folder named **certs**.</span></span> <span data-ttu-id="b7b0e-136">İki tür dosyası hello sertifikaları klasöründe yer alır.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-136">Two types of files appear in hello certs folder.</span></span> <span data-ttu-id="b7b0e-137">Merhaba kök sertifika dosyasını.0 ve.1 gibi numaralı bir dizi ile başlayan bir uzantı var.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-137">hello root certificate file has an extension that begins with a numbered sequence like .0 and .1.</span></span>
    
    <span data-ttu-id="b7b0e-138">Merhaba CRL dosyası .r0 veya .r1 gibi bir dizi ile başlayan bir uzantı var.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-138">hello CRL file has an extension that begins with a sequence like .r0 or .r1.</span></span> <span data-ttu-id="b7b0e-139">Merhaba CRL dosyası bir sertifika ile ilişkilidir.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-139">hello CRL file is associated with a certificate.</span></span>

    ![<span data-ttu-id="b7b0e-140">Yerel olarak ayıklanan dosyasını indirin</span><span class="sxs-lookup"><span data-stu-id="b7b0e-140">Download file extracted locally</span></span> ](./media/backup-azure-backup-server-vmware/extracted-files-in-certs-folder.png)

5. <span data-ttu-id="b7b0e-141">Merhaba, **sertifikaları** klasörünü hello kök sertifika dosyasını sağ tıklatın ve ardından **yeniden adlandırma**.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-141">In hello **certs** folder, right-click hello root certificate file, and then click **Rename**.</span></span>

    ![<span data-ttu-id="b7b0e-142">Kök sertifikayı yeniden adlandırma</span><span class="sxs-lookup"><span data-stu-id="b7b0e-142">Rename root certificate</span></span> ](./media/backup-azure-backup-server-vmware/rename-cert.png)

    <span data-ttu-id="b7b0e-143">Merhaba kök sertifikanın uzantısı too.crt değiştirin.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-143">Change hello root certificate's extension too.crt.</span></span> <span data-ttu-id="b7b0e-144">Toochange hello uzantısı istediğinizden eminseniz tıklatın sorulduğunda **Evet** veya **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-144">When you're asked if you're sure you want toochange hello extension, click **Yes** or **OK**.</span></span> <span data-ttu-id="b7b0e-145">Aksi takdirde hello dosyanın hedeflenen işlevini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-145">Otherwise, you change hello file's intended function.</span></span> <span data-ttu-id="b7b0e-146">bir kök sertifikası temsil eden hello dosya değişiklikleri tooan simgesi Hello simgesi.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-146">hello icon for hello file changes tooan icon that represents a root certificate.</span></span>

6. <span data-ttu-id="b7b0e-147">Merhaba kök sertifikayı sağ tıklatın ve hello açılır menüsünden seçin **sertifikayı yükle**.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-147">Right-click hello root certificate and from hello pop-up menu, select **Install Certificate**.</span></span>

    <span data-ttu-id="b7b0e-148">Merhaba **Sertifika Alma Sihirbazı'nı** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-148">hello **Certificate Import Wizard** dialog box appears.</span></span>

7. <span data-ttu-id="b7b0e-149">Merhaba, **Sertifika Alma Sihirbazı'nı** iletişim kutusunda **yerel makine** hello sertifika ve ardından hello hedefi olarak **sonraki** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-149">In hello **Certificate Import Wizard** dialog box, select **Local Machine** as hello destination for hello certificate, and then click **Next** toocontinue.</span></span>

    ![<span data-ttu-id="b7b0e-150">Sertifika Depolama Hedef seçenekleri</span><span class="sxs-lookup"><span data-stu-id="b7b0e-150">Certificate storage destination options</span></span> ](./media/backup-azure-backup-server-vmware/certificate-import-wizard1.png)

    <span data-ttu-id="b7b0e-151">Tooallow değişiklikleri toohello bilgisayar isteyip istemediğinizi sorulursa tıklatın **Evet** veya **Tamam**, tooall hello değişiklikleri.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-151">If you're asked if you want tooallow changes toohello computer, click **Yes** or **OK**, tooall hello changes.</span></span>

8. <span data-ttu-id="b7b0e-152">Merhaba üzerinde **sertifika deposu** sayfasında, **tüm sertifikaları deposu aşağıdaki hello Yerleştir**ve ardından **Gözat** toochoose hello sertifika deposu.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-152">On hello **Certificate Store** page, select **Place all certificates in hello following store**, and then click **Browse** toochoose hello certificate store.</span></span>

    ![Bir özel depolama nokta sertifikaları Yerleştir](./media/backup-azure-backup-server-vmware/cert-import-wizard-local-store.png)

    <span data-ttu-id="b7b0e-154">Merhaba **sertifika deposu Seç** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-154">hello **Select Certificate Store** dialog box appears.</span></span>

    ![Sertifika depolama klasör hiyerarşisi](./media/backup-azure-backup-server-vmware/cert-store.png)

9. <span data-ttu-id="b7b0e-156">Seçin **güvenilen kök sertifika yetkilileri** hello sertifikaları ve ardından için hello hedef klasör olarak **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-156">Select **Trusted Root Certification Authorities** as hello destination folder for hello certificates, and then click **OK**.</span></span>

    ![Sertifika hedef klasör](./media/backup-azure-backup-server-vmware/certificate-store-selected.png)

    <span data-ttu-id="b7b0e-158">Merhaba **güvenilen kök sertifika yetkilileri** klasörü hello sertifika deposu olarak onaylandı.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-158">hello **Trusted Root Certification Authorities** folder is confirmed as hello certificate store.</span></span> <span data-ttu-id="b7b0e-159">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-159">Click **Next**.</span></span>

    ![Sertifika Deposu klasörü](./media/backup-azure-backup-server-vmware/certificate-import-wizard2.png)

10. <span data-ttu-id="b7b0e-161">Merhaba üzerinde **Sertifika Alma Sihirbazı Tamamlanıyor hello** sayfasında, bu hello sertifika hello istenen klasöründe olduğunu doğrulayın ve ardından **son**.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-161">On hello **Completing hello Certificate Import Wizard** page, verify that hello certificate is in hello desired folder, and then click **Finish**.</span></span>

    ![Sertifika hello uygun klasöründe olduğunu doğrulayın](./media/backup-azure-backup-server-vmware/cert-wizard-final-screen.png)

    <span data-ttu-id="b7b0e-163">Bir iletişim kutusu görüntülenirse, hello başarılı sertifika alma doğrulanır.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-163">A dialog box appears, hello successful certificate import is confirmed.</span></span>

11. <span data-ttu-id="b7b0e-164">Toohello vCenter Server tooconfirm, bağlantının güvenli olduğunu oturum açın.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-164">Sign in toohello vCenter Server tooconfirm that your connection is secure.</span></span>

  <span data-ttu-id="b7b0e-165">Merhaba sertifika içeri aktarma başarılı değil ve güvenli bir bağlantı kurulamıyor, hello VMware vSphere üzerinde belgelerine [sunucu sertifikaları alma](http://pubs.vmware.com/vsphere-60/index.jsp#com.vmware.wssdk.dsg.doc/sdk_sg_server_certificate_Appendixes.6.4.html).</span><span class="sxs-lookup"><span data-stu-id="b7b0e-165">If hello certificate import is not successful, and you cannot establish a secure connection, consult hello VMware vSphere documentation on [obtaining server certificates](http://pubs.vmware.com/vsphere-60/index.jsp#com.vmware.wssdk.dsg.doc/sdk_sg_server_certificate_Appendixes.6.4.html).</span></span>

  <span data-ttu-id="b7b0e-166">Kuruluşunuz içinde güvenli sınırları olan ve hello HTTPS protokolünü üzerinde tooturn istemiyorsanız, aşağıdaki yordamı toodisable hello güvenli iletişim hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-166">If you have secure boundaries within your organization, and don't want tooturn on hello HTTPS protocol, use hello following procedure toodisable hello secure communications.</span></span>

### <a name="disable-secure-communication-protocol"></a><span data-ttu-id="b7b0e-167">Güvenli iletişim protokolü devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="b7b0e-167">Disable secure communication protocol</span></span>

<span data-ttu-id="b7b0e-168">Kuruluşunuz hello HTTPS protokolünü gerek yoksa, aşağıdaki adımları toodisable HTTPS hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-168">If your organization doesn't require hello HTTPS protocol, use hello following steps toodisable HTTPS.</span></span> <span data-ttu-id="b7b0e-169">toodisable Merhaba varsayılan davranışı, hello varsayılan davranışı yoksayar bir kayıt defteri anahtarı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-169">toodisable hello default behavior, create a registry key that ignores hello default behavior.</span></span>

1. <span data-ttu-id="b7b0e-170">Metin bir .txt dosyasına aşağıdaki hello kopyalayıp yeniden açın.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-170">Copy and paste hello following text into a .txt file.</span></span>

  ```
  Windows Registry Editor Version 5.00
  [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager\VMWare]
  "IgnoreCertificateValidation"=dword:00000001
  ```

2. <span data-ttu-id="b7b0e-171">Merhaba dosya tooyour Azure yedekleme sunucusu bilgisayara kaydedin.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-171">Save hello file tooyour Azure Backup Server computer.</span></span> <span data-ttu-id="b7b0e-172">Merhaba dosya adı için DisableSecureAuthentication.reg kullanın.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-172">For hello file name, use DisableSecureAuthentication.reg.</span></span>

3. <span data-ttu-id="b7b0e-173">Merhaba dosya tooactivate hello kayıt defteri girişini çift tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-173">Double-click hello file tooactivate hello registry entry.</span></span>


## <a name="create-a-role-and-user-account-on-hello-vcenter-server"></a><span data-ttu-id="b7b0e-174">Merhaba vCenter Server bir rol ve kullanıcı hesabı oluşturun</span><span class="sxs-lookup"><span data-stu-id="b7b0e-174">Create a role and user account on hello vCenter Server</span></span>

<span data-ttu-id="b7b0e-175">Merhaba vCenter sunucusu, bir önceden tanımlanmış bir dizi ayrıcalık rolüdür.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-175">On hello vCenter Server, a role is a predefined set of privileges.</span></span> <span data-ttu-id="b7b0e-176">Bir vCenter sunucusu Yöneticisi hello rolü oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-176">A vCenter Server administrator creates hello roles.</span></span> <span data-ttu-id="b7b0e-177">tooassign izinleri Merhaba yönetici rol olan kullanıcı hesaplarını çiftleri.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-177">tooassign permissions, hello administrator pairs user accounts with a role.</span></span> <span data-ttu-id="b7b0e-178">tooestablish hello gerekli kullanıcı kimlik bilgilerini tooback hello vCenter Server bilgisayarınızı belirli ayrıcalıklarına sahip bir rol oluşturmak ve ardından hello kullanıcı hesabı hello rolü ile ilişkilendir.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-178">tooestablish hello necessary user credentials tooback up hello vCenter Server computer, create a role with specific privileges, and then associate hello user account with hello role.</span></span>

<span data-ttu-id="b7b0e-179">Azure yedekleme sunucusu kullanıcı adı ve parola tooauthenticate hello vCenter Server ile kullanır.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-179">Azure Backup Server uses a username and password tooauthenticate with hello vCenter Server.</span></span> <span data-ttu-id="b7b0e-180">Azure Backup sunucusu bu kimlik bilgileri tüm yedekleme işlemleri için kimlik doğrulaması olarak kullanır.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-180">Azure Backup Server uses these credentials as authentication for all backup operations.</span></span>

<span data-ttu-id="b7b0e-181">tooadd bir vCenter sunucusu rolü ve kendi ayrıcalıklarını bir yedekleme Yöneticisi için:</span><span class="sxs-lookup"><span data-stu-id="b7b0e-181">tooadd a vCenter Server role and its privileges for a backup administrator:</span></span>

1. <span data-ttu-id="b7b0e-182">Oturum toohello vCenter Server ve ardından hello vcenter Server'daki **Gezgini** öğesine tıklayın **Yönetim**.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-182">Sign in toohello vCenter Server, and then in hello vCenter Server **Navigator** panel, click **Administration**.</span></span>

    ![VCenter Server gezinti panelinde yönetim seçeneği](./media/backup-azure-backup-server-vmware/vmware-navigator-panel.png)

2. <span data-ttu-id="b7b0e-184">İçinde **Yönetim** seçin **rolleri**ve ardından hello **rolleri** paneli tıklatın hello rol simgesi (Merhaba + simgesi) ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-184">In **Administration** select **Roles**, and then in hello **Roles** panel click hello add role icon (hello + symbol).</span></span>

    ![Rol Ekle](./media/backup-azure-backup-server-vmware/vmware-define-new-role.png)

    <span data-ttu-id="b7b0e-186">Merhaba **Rol Oluştur** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-186">hello **Create Role** dialog box appears.</span></span>

    ![Rolü oluşturma](./media/backup-azure-backup-server-vmware/vmware-define-new-role-priv.png)

3. <span data-ttu-id="b7b0e-188">Merhaba, **Rol Oluştur** iletişim kutusunda hello **rol adı** kutusuna *BackupAdminRole*.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-188">In hello **Create Role** dialog box, in hello **Role name** box, enter *BackupAdminRole*.</span></span> <span data-ttu-id="b7b0e-189">Merhaba rol adı ne olursa olsun, ister olabilir, ancak hello rolün amaçla tanınabilir olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-189">hello role name can be whatever you like, but it should be recognizable for hello role's purpose.</span></span>

4. <span data-ttu-id="b7b0e-190">VCenter'ün uygun sürümüne hello Hello ayrıcalıklarını seçin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-190">Select hello privileges for hello appropriate version of vCenter, and then click **OK**.</span></span> <span data-ttu-id="b7b0e-191">Aşağıdaki tablonun hello vCenter 6.0 ve vCenter 5.5 için gerekli hello ayrıcalıkları tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-191">hello following table identifies hello required privileges for vCenter 6.0 and vCenter 5.5.</span></span>

  <span data-ttu-id="b7b0e-192">Merhaba ayrıcalıkları seçtiğinizde hello simgesi sonraki toohello üst etiket tooexpand hello üst ve görünüm hello alt ayrıcalıkları'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-192">When you select hello privileges, click hello icon next toohello parent label tooexpand hello parent and view hello child privileges.</span></span> <span data-ttu-id="b7b0e-193">tooselect hello VirtualMachine ayrıcalıkları, gereksinim duyduğunuz toogo hello birkaç düzeylerine üst alt hiyerarşisi.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-193">tooselect hello VirtualMachine privileges, you need toogo several levels into hello parent child hierarchy.</span></span> <span data-ttu-id="b7b0e-194">Tooselect üst ayrıcalık içindeki tüm alt ayrıcalıklar gerekmez.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-194">You don't need tooselect all child privileges within a parent privilege.</span></span>

  ![Üst alt ayrıcalık hiyerarşisi](./media/backup-azure-backup-server-vmware/cert-add-privilege-expand.png)

  <span data-ttu-id="b7b0e-196">Tıklattıktan sonra **Tamam**, hello yeni rol görünür hello rolleri panelindeki hello listesinde.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-196">After you click **OK**, hello new role appears in hello list on hello Roles panel.</span></span>

|<span data-ttu-id="b7b0e-197">VCenter 6.0 için ayrıcalıkları</span><span class="sxs-lookup"><span data-stu-id="b7b0e-197">Privileges for vCenter 6.0</span></span>| <span data-ttu-id="b7b0e-198">VCenter 5.5 için ayrıcalıkları</span><span class="sxs-lookup"><span data-stu-id="b7b0e-198">Privileges for vCenter 5.5</span></span>|
|--------------------------|---------------------------|
|<span data-ttu-id="b7b0e-199">Datastore.AllocateSpace</span><span class="sxs-lookup"><span data-stu-id="b7b0e-199">Datastore.AllocateSpace</span></span>   | <span data-ttu-id="b7b0e-200">Datastore.AllocateSpace</span><span class="sxs-lookup"><span data-stu-id="b7b0e-200">Datastore.AllocateSpace</span></span>|
|<span data-ttu-id="b7b0e-201">Global.ManageCustomFields</span><span class="sxs-lookup"><span data-stu-id="b7b0e-201">Global.ManageCustomFields</span></span> | <span data-ttu-id="b7b0e-202">Global.ManageCustomerFields</span><span class="sxs-lookup"><span data-stu-id="b7b0e-202">Global.ManageCustomerFields</span></span>|
|<span data-ttu-id="b7b0e-203">Global.SetCustomFields</span><span class="sxs-lookup"><span data-stu-id="b7b0e-203">Global.SetCustomFields</span></span>    |   |
|<span data-ttu-id="b7b0e-204">Host.Local.CreateVM</span><span class="sxs-lookup"><span data-stu-id="b7b0e-204">Host.Local.CreateVM</span></span>       | <span data-ttu-id="b7b0e-205">Network.Assign</span><span class="sxs-lookup"><span data-stu-id="b7b0e-205">Network.Assign</span></span> |
|<span data-ttu-id="b7b0e-206">Network.Assign</span><span class="sxs-lookup"><span data-stu-id="b7b0e-206">Network.Assign</span></span>            |  |
|<span data-ttu-id="b7b0e-207">Resource.AssignVMToPool</span><span class="sxs-lookup"><span data-stu-id="b7b0e-207">Resource.AssignVMToPool</span></span>   |  |
|<span data-ttu-id="b7b0e-208">VirtualMachine.Config.AddNewDisk</span><span class="sxs-lookup"><span data-stu-id="b7b0e-208">VirtualMachine.Config.AddNewDisk</span></span>  | <span data-ttu-id="b7b0e-209">VirtualMachine.Config.AddNewDisk</span><span class="sxs-lookup"><span data-stu-id="b7b0e-209">VirtualMachine.Config.AddNewDisk</span></span>   |
|<span data-ttu-id="b7b0e-210">VirtualMachine.Config.AdvanceConfig</span><span class="sxs-lookup"><span data-stu-id="b7b0e-210">VirtualMachine.Config.AdvanceConfig</span></span>| <span data-ttu-id="b7b0e-211">VirtualMachine.Config.AdvancedConfig</span><span class="sxs-lookup"><span data-stu-id="b7b0e-211">VirtualMachine.Config.AdvancedConfig</span></span>|
|<span data-ttu-id="b7b0e-212">VirtualMachine.Config.ChangeTracking</span><span class="sxs-lookup"><span data-stu-id="b7b0e-212">VirtualMachine.Config.ChangeTracking</span></span>| <span data-ttu-id="b7b0e-213">VirtualMachine.Config.ChangeTracking</span><span class="sxs-lookup"><span data-stu-id="b7b0e-213">VirtualMachine.Config.ChangeTracking</span></span> |
|<span data-ttu-id="b7b0e-214">VirtualMachine.Config.HostUSBDevice</span><span class="sxs-lookup"><span data-stu-id="b7b0e-214">VirtualMachine.Config.HostUSBDevice</span></span>||
|<span data-ttu-id="b7b0e-215">VirtualMachine.Config.QueryUnownedFiles</span><span class="sxs-lookup"><span data-stu-id="b7b0e-215">VirtualMachine.Config.QueryUnownedFiles</span></span>|    |
|<span data-ttu-id="b7b0e-216">VirtualMachine.Config.SwapPlacement</span><span class="sxs-lookup"><span data-stu-id="b7b0e-216">VirtualMachine.Config.SwapPlacement</span></span>| <span data-ttu-id="b7b0e-217">VirtualMachine.Config.SwapPlacement</span><span class="sxs-lookup"><span data-stu-id="b7b0e-217">VirtualMachine.Config.SwapPlacement</span></span> |
|<span data-ttu-id="b7b0e-218">VirtualMachine.Interact.PowerOff</span><span class="sxs-lookup"><span data-stu-id="b7b0e-218">VirtualMachine.Interact.PowerOff</span></span>| <span data-ttu-id="b7b0e-219">VirtualMachine.Interact.PowerOff</span><span class="sxs-lookup"><span data-stu-id="b7b0e-219">VirtualMachine.Interact.PowerOff</span></span> |
|<span data-ttu-id="b7b0e-220">VirtualMachine.Inventory.Create</span><span class="sxs-lookup"><span data-stu-id="b7b0e-220">VirtualMachine.Inventory.Create</span></span>| <span data-ttu-id="b7b0e-221">VirtualMachine.Inventory.Create</span><span class="sxs-lookup"><span data-stu-id="b7b0e-221">VirtualMachine.Inventory.Create</span></span> |
|<span data-ttu-id="b7b0e-222">VirtualMachine.Provisioning.DiskRandomAccess</span><span class="sxs-lookup"><span data-stu-id="b7b0e-222">VirtualMachine.Provisioning.DiskRandomAccess</span></span>| |
|<span data-ttu-id="b7b0e-223">VirtualMachine.Provisioning.DiskRandomRead</span><span class="sxs-lookup"><span data-stu-id="b7b0e-223">VirtualMachine.Provisioning.DiskRandomRead</span></span>|<span data-ttu-id="b7b0e-224">VirtualMachine.Provisioning.DiskRandomRead</span><span class="sxs-lookup"><span data-stu-id="b7b0e-224">VirtualMachine.Provisioning.DiskRandomRead</span></span> |
|<span data-ttu-id="b7b0e-225">VirtualMachine.State.CreateSnapshot</span><span class="sxs-lookup"><span data-stu-id="b7b0e-225">VirtualMachine.State.CreateSnapshot</span></span>| <span data-ttu-id="b7b0e-226">VirtualMachine.State.CreateSnapshot</span><span class="sxs-lookup"><span data-stu-id="b7b0e-226">VirtualMachine.State.CreateSnapshot</span></span>|
|<span data-ttu-id="b7b0e-227">VirtualMachine.State.RemoveSnapshot</span><span class="sxs-lookup"><span data-stu-id="b7b0e-227">VirtualMachine.State.RemoveSnapshot</span></span>|<span data-ttu-id="b7b0e-228">VirtualMachine.State.RemoveSnapshot</span><span class="sxs-lookup"><span data-stu-id="b7b0e-228">VirtualMachine.State.RemoveSnapshot</span></span> |
</br>



## <a name="create-a-vcenter-server-user-account-and-permissions"></a><span data-ttu-id="b7b0e-229">Bir vCenter Server kullanıcı hesabı ve izinler oluşturma</span><span class="sxs-lookup"><span data-stu-id="b7b0e-229">Create a vCenter Server user account and permissions</span></span>

<span data-ttu-id="b7b0e-230">Merhaba rol ayrıcalıklarıyla ayarladıktan sonra bir kullanıcı hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-230">After hello role with privileges is set up, create a user account.</span></span> <span data-ttu-id="b7b0e-231">Merhaba kullanıcı hesabı adı ve parola kimlik doğrulaması için kullanılan hello kimlik bilgilerini sağlar sahiptir.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-231">hello user account has a name and password, which provides hello credentials that are used for authentication.</span></span>

1. <span data-ttu-id="b7b0e-232">bir kullanıcı hesabında hello vCenter Server toocreate **Gezgini** öğesine tıklayın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-232">toocreate a user account, in hello vCenter Server **Navigator** panel, click **Users and Groups**.</span></span>

    ![Kullanıcılar ve gruplar seçeneği](./media/backup-azure-backup-server-vmware/vmware-userandgroup-panel.png)

    <span data-ttu-id="b7b0e-234">Merhaba **vCenter kullanıcılar ve gruplar** panelinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-234">hello **vCenter Users and Groups** panel appears.</span></span>

    ![vCenter kullanıcılar ve gruplar paneli](./media/backup-azure-backup-server-vmware/usersandgroups.png)

2. <span data-ttu-id="b7b0e-236">Merhaba, **vCenter kullanıcılar ve gruplar** paneli, select hello **kullanıcılar** sekmesini ve sonra hello kullanıcılar simgesini (Merhaba + simgesi) ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-236">In hello **vCenter Users and Groups** panel, select hello **Users** tab, and then click hello add users icon (hello + symbol).</span></span>

    <span data-ttu-id="b7b0e-237">Merhaba **yeni kullanıcı** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-237">hello **New User** dialog box appears.</span></span>

3. <span data-ttu-id="b7b0e-238">Merhaba, **yeni kullanıcı** iletişim kutusunda, hello kullanıcının bilgileri ekleyin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-238">In hello **New User** dialog box, add hello user's information and then click **OK**.</span></span> <span data-ttu-id="b7b0e-239">Bu yordamda BackupAdmin hello kullanıcı adınızdır.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-239">In this procedure, hello username is BackupAdmin.</span></span>

    ![Yeni kullanıcı iletişim kutusu](./media/backup-azure-backup-server-vmware/vmware-new-user-account.png)

    <span data-ttu-id="b7b0e-241">Merhaba yeni kullanıcı hesabı hello listesinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-241">hello new user account appears in hello list.</span></span>

4. <span data-ttu-id="b7b0e-242">Merhaba rolünde hello tooassociate hello kullanıcı hesabıyla **Gezgini** öğesine tıklayın **genel izinleri**.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-242">tooassociate hello user account with hello role, in hello **Navigator** panel, click **Global Permissions**.</span></span> <span data-ttu-id="b7b0e-243">Merhaba, **genel izinleri** paneli, select hello **Yönet** sekmesini ve sonra hello simgesini (Merhaba + simgesi) ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-243">In hello **Global Permissions** panel, select hello **Manage** tab, and then click hello add icon (hello + symbol).</span></span>

    ![Genel izinleri paneli](./media/backup-azure-backup-server-vmware/vmware-add-new-perms.png)

    <span data-ttu-id="b7b0e-245">Merhaba **genel izinleri kök - ekleme izni** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-245">hello **Global Permissions Root - Add Permission** dialog box appears.</span></span>

5. <span data-ttu-id="b7b0e-246">Merhaba, **genel izin kök - ekleme izni** iletişim kutusu, tıklatın **Ekle** toochoose hello kullanıcı veya grup.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-246">In hello **Global Permission Root - Add Permission** dialog box, click **Add** toochoose hello user or group.</span></span>

    ![Kullanıcı veya grup seçin](./media/backup-azure-backup-server-vmware/vmware-add-new-global-perm.png)

    <span data-ttu-id="b7b0e-248">Merhaba **kullanıcıları/Grupları Seç** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-248">hello **Select Users/Groups** dialog box appears.</span></span>

6. <span data-ttu-id="b7b0e-249">Merhaba, **kullanıcıları/Grupları Seç** iletişim kutusunda, seçin **BackupAdmin** ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-249">In hello **Select Users/Groups** dialog box, choose **BackupAdmin** and then click **Add**.</span></span>

    <span data-ttu-id="b7b0e-250">İçinde **kullanıcılar**, hello *etki alanı\kullanıcı adı* biçiminde hello kullanıcı hesabı için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-250">In **Users**, hello *domain\username* format is used for hello user account.</span></span> <span data-ttu-id="b7b0e-251">Farklı bir etki alanı toouse istiyorsanız, hello tercih **etki alanı** listesi.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-251">If you want toouse a different domain, choose it from hello **Domain** list.</span></span>

    ![BackupAdmin kullanıcı ekleme](./media/backup-azure-backup-server-vmware/vmware-assign-account-to-role.png)

    <span data-ttu-id="b7b0e-253">Tıklatın **Tamam** tooadd hello seçili kullanıcıların toohello **ekleme izni** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-253">Click **OK** tooadd hello selected users toohello **Add Permission** dialog box.</span></span>

7. <span data-ttu-id="b7b0e-254">Merhaba kullanıcı tanımladınız, hello kullanıcı toohello rolü atayın.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-254">Now that you've identified hello user, assign hello user toohello role.</span></span> <span data-ttu-id="b7b0e-255">İçinde **atanan rolü**, hello aşağı açılan listeden seçin **BackupAdminRole**ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-255">In **Assigned Role**, from hello drop-down list, select **BackupAdminRole**, and then click **OK**.</span></span>

    ![Kullanıcı toorole atayın](./media/backup-azure-backup-server-vmware/vmware-choose-role.png)

  <span data-ttu-id="b7b0e-257">Merhaba üzerinde **Yönet** hello sekmesinde **genel izinleri** panelinde, hello yeni kullanıcı hesabı ve ilişkili hello rol hello listesinde görünür.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-257">On hello **Manage** tab in hello **Global Permissions** panel, hello new user account and hello associated role appear in hello list.</span></span>


## <a name="establish-vcenter-server-credentials-on-azure-backup-server"></a><span data-ttu-id="b7b0e-258">VCenter sunucusu kimlik bilgilerini Azure yedekleme sunucusu kurma</span><span class="sxs-lookup"><span data-stu-id="b7b0e-258">Establish vCenter Server credentials on Azure Backup Server</span></span>

<span data-ttu-id="b7b0e-259">Merhaba VMware server tooAzure yedekleme sunucusu eklemeden önce yükleme [Azure yedekleme sunucusu için Güncelleştirme 1](https://support.microsoft.com/help/3175529/update-1-for-microsoft-azure-backup-server).</span><span class="sxs-lookup"><span data-stu-id="b7b0e-259">Before you add hello VMware server tooAzure Backup Server, install [Update 1 for Azure Backup Server](https://support.microsoft.com/help/3175529/update-1-for-microsoft-azure-backup-server).</span></span>

1. <span data-ttu-id="b7b0e-260">Azure yedekleme sunucusu tooopen hello Azure yedekleme sunucusu masaüstünde hello simgesini çift tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-260">tooopen Azure Backup Server, double-click hello icon on hello Azure Backup Server desktop.</span></span>

    ![Azure yedekleme sunucusu simgesi](./media/backup-azure-backup-server-vmware/mabs-icon.png)

    <span data-ttu-id="b7b0e-262">Merhaba masaüstünde hello simgesi bulamazsanız, Azure yedekleme sunucusu hello yüklü uygulamalar listesinden açın.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-262">If you can't find hello icon on hello desktop, open Azure Backup Server from hello list of installed apps.</span></span> <span data-ttu-id="b7b0e-263">Hello Azure yedekleme sunucusu uygulama adı, Microsoft Azure yedekleme denir.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-263">hello Azure Backup Server app name is called Microsoft Azure Backup.</span></span>

2. <span data-ttu-id="b7b0e-264">Hello Azure yedekleme sunucusu konsolunda **Yönetim**, tıklatın **üretim sunucuları**ve hello araç şeridinde, ardından **yönetmek VMware**.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-264">In hello Azure Backup Server console, click **Management**, click **Production Servers**, and then on hello tool ribbon, click **Manage VMware**.</span></span>

    ![Azure yedekleme sunucusu konsol](./media/backup-azure-backup-server-vmware/add-vmware-credentials.png)

    <span data-ttu-id="b7b0e-266">Merhaba **kimlik bilgilerini Yönet** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-266">hello **Manage Credentials** dialog box appears.</span></span>

    ![Azure yedekleme sunucusu kimlik bilgilerini Yönet iletişim kutusu](./media/backup-azure-backup-server-vmware/mabs-manage-credentials-dialog.png)

3. <span data-ttu-id="b7b0e-268">Merhaba, **kimlik bilgilerini Yönet** iletişim kutusu, tıklatın **Ekle** tooopen hello **kimlik bilgileri Ekle** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-268">In hello **Manage Credentials** dialog box, click **Add** tooopen hello **Add Credential** dialog box.</span></span>

4. <span data-ttu-id="b7b0e-269">Merhaba, **kimlik bilgileri Ekle** iletişim kutusunda, bir ad ve hello yeni kimlik bilgisi için bir açıklama girin.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-269">In hello **Add Credential** dialog box, enter a name and a description for hello new credential.</span></span> <span data-ttu-id="b7b0e-270">Ardından hello kullanıcı adı ve parola belirtin.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-270">Then specify hello username and password.</span></span> <span data-ttu-id="b7b0e-271">Merhaba adı *Contoso Vcenter kimlik bilgisi* kullanılan hello sonraki yordamda tooidentify hello kimlik bilgisi.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-271">hello name, *Contoso Vcenter credential* is used tooidentify hello credential in hello next procedure.</span></span> <span data-ttu-id="b7b0e-272">Kullanım hello aynı kullanıcı adı ve için kullanılan parola hello vCenter Server.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-272">Use hello same username and password that is used for hello vCenter Server.</span></span> <span data-ttu-id="b7b0e-273">Merhaba vCenter Server ve Azure yedekleme sunucusu içinde değilse hello aynı etki alanı **kullanıcı adı**, hello etki alanını belirtin.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-273">If hello vCenter Server and Azure Backup Server are not in hello same domain, in **User name**, specify hello domain.</span></span>

    ![Azure yedekleme sunucusu kimlik bilgileri Ekle iletişim kutusu](./media/backup-azure-backup-server-vmware/mabs-add-credential-dialog2.png)

    <span data-ttu-id="b7b0e-275">Tıklatın **Ekle** tooadd hello yeni kimlik bilgisi tooAzure yedekleme sunucusu.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-275">Click **Add** tooadd hello new credential tooAzure Backup Server.</span></span> <span data-ttu-id="b7b0e-276">Yeni bir kimlik bilgisi Hello görünür hello hello listesinde **kimlik bilgilerini Yönet** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-276">hello new credential appears in hello list in hello **Manage Credentials** dialog box.</span></span>
    
    ![Azure yedekleme sunucusu kimlik bilgilerini Yönet iletişim kutusu](./media/backup-azure-backup-server-vmware/new-list-of-mabs-creds.png)

5. <span data-ttu-id="b7b0e-278">tooclose hello **kimlik bilgilerini Yönet** iletişim kutusunda, hello **X** hello sağ üst köşedeki.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-278">tooclose hello **Manage Credentials** dialog box, click hello **X** in hello upper-right corner.</span></span>


## <a name="add-hello-vcenter-server-tooazure-backup-server"></a><span data-ttu-id="b7b0e-279">Merhaba vCenter Server tooAzure Yedekleme Sunucusu Ekle</span><span class="sxs-lookup"><span data-stu-id="b7b0e-279">Add hello vCenter Server tooAzure Backup Server</span></span>

<span data-ttu-id="b7b0e-280">Üretim Sunucusu Ekleme Sihirbazı'nı kullanılan tooadd hello vCenter Server tooAzure yedekleme sunucusu olur.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-280">Production Server Addition Wizard is used tooadd hello vCenter Server tooAzure Backup Server.</span></span>

<span data-ttu-id="b7b0e-281">Üretim Sunucusu Ekleme Sihirbazı, aşağıdaki yordamın tam hello tooopen:</span><span class="sxs-lookup"><span data-stu-id="b7b0e-281">tooopen Production Server Addition Wizard, complete hello following procedure:</span></span>

1. <span data-ttu-id="b7b0e-282">Hello Azure yedekleme sunucusu konsolunda **Yönetim**, tıklatın **üretim sunucuları**ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-282">In hello Azure Backup Server console, click **Management**, click **Production Servers**, and then click **Add**.</span></span>

    ![Açık Üretim Sunucusu Ekleme Sihirbazı](./media/backup-azure-backup-server-vmware/add-vcenter-to-mabs.png)

    <span data-ttu-id="b7b0e-284">Merhaba **Üretim Sunucusu Ekleme Sihirbazı'nı** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-284">hello **Production Server Addition Wizard** dialog box appears.</span></span>

    ![Üretim Sunucusu Ekleme Sihirbazı](./media/backup-azure-backup-server-vmware/production-server-add-wizard.png)

2. <span data-ttu-id="b7b0e-286">Merhaba üzerinde **üretim sunucusu seçin türü** sayfasında **VMware sunucuları**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-286">On hello **Select Production Server type** page, select **VMware Servers**, and then click **Next**.</span></span>

3. <span data-ttu-id="b7b0e-287">İçinde **sunucu adı/IP adresi**, hello tam etki alanı adı (FQDN) veya hello VMware sunucusunun IP adresini belirtin.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-287">In **Server Name/IP Address**, specify hello fully qualified domain name (FQDN) or IP address of hello VMware server.</span></span> <span data-ttu-id="b7b0e-288">Tüm hello ESXi sunucuları hello tarafından yönetiliyorsa aynı vCenter hello vCenter adı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-288">If all hello ESXi servers are managed by hello same vCenter, you can use hello vCenter name.</span></span>

    ![VMware server FQDN veya IP adresi belirtin](./media/backup-azure-backup-server-vmware/add-vmware-server-provide-server-name.png)

4. <span data-ttu-id="b7b0e-290">İçinde **SSL bağlantı noktası**, hello kullanılan toocommunicate hello VMware sunucusuyla bağlantı noktasını girin.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-290">In **SSL Port**, enter hello port that is used toocommunicate with hello VMware server.</span></span> <span data-ttu-id="b7b0e-291">Farklı bir bağlantı gerekli olduğunu bilmiyorsanız hello varsayılan bağlantı noktası, bağlantı noktası 443'ü kullanın.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-291">Use port 443, which is hello default port, unless you know that a different port is required.</span></span>

5. <span data-ttu-id="b7b0e-292">İçinde **kimlik bilgisi belirtin**, hello daha önce oluşturduğunuz kimlik bilgisi seçin.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-292">In **Specify Credential**, select hello credential that you created earlier.</span></span>

    ![Kimlik bilgisi belirtin](./media/backup-azure-backup-server-vmware/identify-creds.png)

6. <span data-ttu-id="b7b0e-294">Tıklatın **Ekle** tooadd hello VMware sunucu toohello listesi **eklenen VMware sunucuları**ve ardından **sonraki** toomove toohello sonraki sayfaya hello Sihirbazı.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-294">Click **Add** tooadd hello VMware server toohello list of **Added VMware Servers**, and then click **Next** toomove toohello next page in hello wizard.</span></span>

    ![VMWare server ve kimlik bilgisi Ekle](./media/backup-azure-backup-server-vmware/add-vmware-server-credentials.png)

7. <span data-ttu-id="b7b0e-296">Merhaba, **Özet** sayfasında, **Ekle** tooadd hello belirtilen VMware server tooAzure yedekleme sunucusu.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-296">In hello **Summary** page, click **Add** tooadd hello specified VMware server tooAzure Backup Server.</span></span>

    ![VMware server tooAzure Yedekleme Sunucusu Ekle](./media/backup-azure-backup-server-vmware/tasks-screen.png)

  <span data-ttu-id="b7b0e-298">Merhaba VMware server yedekleme aracısız yedeğidir ve hello yeni sunucu hemen eklenir.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-298">hello VMware server backup is an agentless backup, and hello new server is added immediately.</span></span> <span data-ttu-id="b7b0e-299">Merhaba **son** sayfasında sonuçları hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-299">hello **Finish** page shows you hello results.</span></span>

  ![Son sayfası](./media/backup-azure-backup-server-vmware/summary-screen.png)

  <span data-ttu-id="b7b0e-301">vCenter Server tooAzure yedekleme sunucusu, yineleme hello önceki birden çok örneğini bu bölümdeki adımları tooadd.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-301">tooadd multiple instances of vCenter Server tooAzure Backup Server, repeat hello previous steps in this section.</span></span>

<span data-ttu-id="b7b0e-302">Merhaba vCenter Server tooAzure yedekleme sunucusu ekledikten sonra hello sonraki toocreate bir koruma grubu adımdır.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-302">After you add hello vCenter Server tooAzure Backup Server, hello next step is toocreate a protection group.</span></span> <span data-ttu-id="b7b0e-303">Merhaba koruma grubu kısa veya uzun vadeli bekletme için çeşitli detayları hello ve burada tanımlayın ve hello yedekleme ilkesini uygulamak olduğunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-303">hello protection group specifies hello various details for short or long-term retention, and it is where you define and apply hello backup policy.</span></span> <span data-ttu-id="b7b0e-304">Merhaba yedekleme İlkesi, yedeklemeler olduğunda ve ne yedeklenir hello zamanlamadır.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-304">hello backup policy is hello schedule for when backups occur, and what is backed up.</span></span>


## <a name="configure-a-protection-group"></a><span data-ttu-id="b7b0e-305">Bir koruma grubunu yapılandırın</span><span class="sxs-lookup"><span data-stu-id="b7b0e-305">Configure a protection group</span></span>

<span data-ttu-id="b7b0e-306">System Center Data Protection Manager veya Azure yedekleme sunucusu önce kullanmadıysanız bkz [planlama disk yedeklemeleri](https://technet.microsoft.com/library/hh758026.aspx) tooprepare donanım ortamınızı.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-306">If you have not used System Center Data Protection Manager or Azure Backup Server before, see [Plan for disk backups](https://technet.microsoft.com/library/hh758026.aspx) tooprepare your hardware environment.</span></span> <span data-ttu-id="b7b0e-307">Uygun depolama alanına sahip denetledikten sonra hello yeni koruma grubu oluşturma Sihirbazı'nı tooadd VMware sanal makineleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-307">After you check that you have proper storage, use hello Create New Protection Group wizard tooadd VMware virtual machines.</span></span>

1. <span data-ttu-id="b7b0e-308">Hello Azure yedekleme sunucusu konsolunda **koruma**, hello araç şeridinde tıklatıp **yeni** tooopen hello yeni koruma grubu oluşturma Sihirbazı.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-308">In hello Azure Backup Server console, click **Protection**, and in hello tool ribbon, click **New** tooopen hello Create New Protection Group wizard.</span></span>

    ![Açık hello yeni koruma grubu oluşturma Sihirbazı](./media/backup-azure-backup-server-vmware/open-protection-wizard.png)

    <span data-ttu-id="b7b0e-310">Merhaba **yeni koruma grubu oluşturma** Sihirbazı iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-310">hello **Create New Protection Group** wizard dialog box appears.</span></span>

    ![Yeni koruma grubu oluşturma Sihirbazı iletişim kutusu](./media/backup-azure-backup-server-vmware/protection-wizard.png)

    <span data-ttu-id="b7b0e-312">Tıklatın **sonraki** tooadvance toohello **koruma grubu türünü seçin** sayfası.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-312">Click **Next** tooadvance toohello **Select protection group type** page.</span></span>

2. <span data-ttu-id="b7b0e-313">Merhaba üzerinde **seçin koruma grubu türünü** sayfasında **sunucuları** ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-313">On hello **Select Protection group type** page, select **Servers** and then click **Next**.</span></span> <span data-ttu-id="b7b0e-314">Merhaba **grup üyelerini seçin** sayfası görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-314">hello **Select group members** page appears.</span></span>

3. <span data-ttu-id="b7b0e-315">Merhaba üzerinde **grup üyelerini seçin** sayfası, hello kullanılabilir üyeler ve seçili hello üyeleri görünür.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-315">On hello **Select group members** page, hello available members and hello selected members appear.</span></span> <span data-ttu-id="b7b0e-316">Tooprotect istediğiniz ve ardından hello üyeleri seçin **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-316">Select hello members that you want tooprotect, and then click **Next**.</span></span>

    ![Grup üyelerini seçin](./media/backup-azure-backup-server-vmware/server-add-selected-members.png)

    <span data-ttu-id="b7b0e-318">Diğer klasörlere veya sanal makineleri içeren bir klasör seçerseniz bir üye seçin, bu klasör ve VM'ler da seçilir.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-318">When you select a member, if you select a folder that contains other folders or VMs, those folders and VMs are also selected.</span></span> <span data-ttu-id="b7b0e-319">Merhaba ekleme hello klasör ve VM'ler hello üst klasörde klasör düzeyinde koruma adı verilir.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-319">hello inclusion of hello folders and VMs in hello parent folder is called folder-level protection.</span></span> <span data-ttu-id="b7b0e-320">tooremove bir klasör veya VM, Temizle hello onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-320">tooremove a folder or VM, clear hello check box.</span></span>

    <span data-ttu-id="b7b0e-321">Bir VM veya bir VM'yi içeren bir klasör zaten korumalı tooAzure ise, bu VM yeniden seçemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-321">If a VM, or a folder containing a VM, is already protected tooAzure, you cannot select that VM again.</span></span> <span data-ttu-id="b7b0e-322">Bir VM korumalı tooAzure olduktan sonra diğer bir deyişle, onu yeniden yinelenen kurtarma noktaları için bir VM oluşturulmasını engeller korunamaz.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-322">That is, after a VM is protected tooAzure, it cannot be protected again, which prevents duplicate recovery points from being created for one VM.</span></span> <span data-ttu-id="b7b0e-323">Hangi Azure yedekleme sunucusu örneği zaten koruyan bir üye, noktası toohello üye toosee hello sunucusunu koruyan hello adını toosee istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-323">If you want toosee which Azure Backup Server instance already protects a member, point toohello member toosee hello name of hello protecting server.</span></span>

4. <span data-ttu-id="b7b0e-324">Merhaba üzerinde **veri koruma yöntemini seçin** sayfasında, hello koruma grubu için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-324">On hello **Select Data Protection Method** page, enter a name for hello protection group.</span></span> <span data-ttu-id="b7b0e-325">Kısa vadeli koruma (toodisk) ve çevrimiçi koruma seçilir.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-325">Short-term protection (toodisk) and online protection are selected.</span></span> <span data-ttu-id="b7b0e-326">Toouse çevrimiçi koruma (tooAzure) isterseniz, kısa vadeli koruma toodisk kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-326">If you want toouse online protection (tooAzure), you must use short-term protection toodisk.</span></span> <span data-ttu-id="b7b0e-327">Tıklatın **sonraki** tooproceed toohello kısa vadeli koruma aralık.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-327">Click **Next** tooproceed toohello short-term protection range.</span></span>

    ![Veri koruma yöntemini seçin](./media/backup-azure-backup-server-vmware/name-protection-group.png)

5. <span data-ttu-id="b7b0e-329">Merhaba üzerinde **kısa vadeli hedefleri belirtin** sayfası için **bekletme aralığı**, hello tooretain kurtarma noktaları istediğiniz gün sayısını belirtin *depolanan toodisk*.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-329">On hello **Specify Short-Term Goals** page, for **Retention Range**, specify hello number of days that you want tooretain recovery points that are *stored toodisk*.</span></span> <span data-ttu-id="b7b0e-330">Toochange hello zaman ve ne zaman kurtarma noktaları alınır gün istiyorsanız, **Değiştir**.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-330">If you want toochange hello time and days when recovery points are taken, click **Modify**.</span></span> <span data-ttu-id="b7b0e-331">Merhaba kısa vadeli kurtarma noktaları tam yedeklemeler edilir.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-331">hello short-term recovery points are full backups.</span></span> <span data-ttu-id="b7b0e-332">Artımlı yedeklemeler değiller.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-332">They are not incremental backups.</span></span> <span data-ttu-id="b7b0e-333">Merhaba kısa vadeli hedefleri ile memnun kaldığınızda, tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-333">When you are satisfied with hello short-term goals, click **Next**.</span></span>

    ![Kısa vadeli hedefleri belirtin](./media/backup-azure-backup-server-vmware/short-term-goals.png)

6. <span data-ttu-id="b7b0e-335">Merhaba üzerinde **Disk ayırmayı gözden** sayfasında, gözden geçirin ve gerekirse hello VM'ler için hello disk alanını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-335">On hello **Review Disk Allocation** page, review and if necessary, modify hello disk space for hello VMs.</span></span> <span data-ttu-id="b7b0e-336">Merhaba önerilen disk ayırmaları hello belirtilen hello bekletme aralığı temel **kısa vadeli hedefleri belirtin** sayfasında, iş yükü hello türü ve hello hello boyutunu korunan verileri (3. adımda tanımlanan).</span><span class="sxs-lookup"><span data-stu-id="b7b0e-336">hello recommended disk allocations are based on hello retention range that is specified in hello **Specify Short-Term Goals** page, hello type of workload, and hello size of hello protected data (identified in step 3).</span></span>  

  - <span data-ttu-id="b7b0e-337">**Veri boyutu:** hello koruma grubundaki hello verilerin boyutu.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-337">**Data size:** Size of hello data in hello protection group.</span></span>
  - <span data-ttu-id="b7b0e-338">**Disk alanı:** hello hello koruma grubu için disk alanı miktarını önerilir.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-338">**Disk space:** hello recommended amount of disk space for hello protection group.</span></span> <span data-ttu-id="b7b0e-339">Bu ayar toomodify istiyorsanız, her veri kaynağı büyür tahmin hello miktardan biraz daha büyük toplam alan ayırın.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-339">If you want toomodify this setting, you should allocate total space that is slightly larger than hello amount that you estimate each data source grows.</span></span>
  - <span data-ttu-id="b7b0e-340">**Verileri birlikte bulundurma:** üzerinde birlikte bulundurmaya kapatırsanız, birden çok veri kaynağı hello koruma tooa tek çoğaltma ve kurtarma noktası birimi eşleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-340">**Colocate data:** If you turn on colocation, multiple data sources in hello protection can map tooa single replica and recovery point volume.</span></span> <span data-ttu-id="b7b0e-341">Birlikte bulundurma, tüm iş yükleri için desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-341">Colocation isn't supported for all workloads.</span></span>
  - <span data-ttu-id="b7b0e-342">**Otomatik olarak Büyüt:** hello ilk ayırma hello korumalı gruptaki veri boyutunu aşarsa bu ayarı üzerinde kapatma, System Center Data Protection Manager tooincrease hello disk boyutu yüzde 25 ile çalışır..</span><span class="sxs-lookup"><span data-stu-id="b7b0e-342">**Automatically grow:** If you turn on this setting, if data in hello protected group outgrows hello initial allocation, System Center Data Protection Manager tries tooincrease hello disk size by 25 percent.</span></span>
  - <span data-ttu-id="b7b0e-343">**Depolama havuzu ayrıntıları:** hello depolama havuzu kalan disk boyutu ve toplam dahil hello durumunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-343">**Storage pool details:** Shows hello status of hello storage pool, including total and remaining disk size.</span></span>

    ![Disk ayırmayı İncele](./media/backup-azure-backup-server-vmware/review-disk-allocation.png)

    <span data-ttu-id="b7b0e-345">Merhaba alanı ayırma ile memnun kaldığınızda, tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-345">When you are satisfied with hello space allocation, click **Next**.</span></span>

7. <span data-ttu-id="b7b0e-346">Merhaba üzerinde **çoğaltma oluşturma yöntemini seçin** sayfasında, nasıl toogenerate hello ilk kopyalama ya da Azure yedekleme sunucusu üzerindeki hello korumalı verilere yönelik çoğaltma istediğinizi belirtin.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-346">On hello **Choose Replica Creation Method** page, specify how you want toogenerate hello initial copy, or replica, of hello protected data on Azure Backup Server.</span></span>

    <span data-ttu-id="b7b0e-347">Merhaba varsayılandır **hello ağ üzerinden otomatik olarak** ve **şimdi**.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-347">hello default is **Automatically over hello network** and **Now**.</span></span> <span data-ttu-id="b7b0e-348">Merhaba varsayılan kullanırsanız, yoğun olmayan bir zamanı belirtin öneririz.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-348">If you use hello default, we recommend that you specify an off-peak time.</span></span> <span data-ttu-id="b7b0e-349">Seçin **sonra** ve gününü ve saatini belirtin.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-349">Choose **Later** and specify a day and time.</span></span>

    <span data-ttu-id="b7b0e-350">Büyük miktarlarda veri veya en iyi durumdan daha az ağ koşulları için Çıkarılabilir medya kullanarak çevrimdışı hello veri çoğaltmayı düşünebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-350">For large amounts of data or less-than-optimal network conditions, consider replicating hello data offline by using removable media.</span></span>

    <span data-ttu-id="b7b0e-351">Seçimlerinizi yaptıktan sonra tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-351">After you have made your choices, click **Next**.</span></span>

    ![Çoğaltma oluşturma yöntemini seçin](./media/backup-azure-backup-server-vmware/replica-creation.png)

8. <span data-ttu-id="b7b0e-353">Merhaba üzerinde **tutarlılık denetimi seçenekleri** nasıl ve ne zaman tooautomate hello tutarlılık denetimlerinin sayfasında, seçin.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-353">On hello **Consistency Check Options** page, select how and when tooautomate hello consistency checks.</span></span> <span data-ttu-id="b7b0e-354">Çoğaltma verileri tutarsız hale geldiğinde veya belirlenmiş bir zamanlamaya üzerinde tutarlılık denetimleri çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-354">You can run consistency checks when replica data becomes inconsistent, or on a set schedule.</span></span>

    <span data-ttu-id="b7b0e-355">Tooconfigure otomatik tutarlılık denetimlerinin istemiyorsanız, el ile denetim çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-355">If you don't want tooconfigure automatic consistency checks, you can run a manual check.</span></span> <span data-ttu-id="b7b0e-356">Merhaba koruma bölmesinde hello Azure yedekleme sunucusu konsolunun hello koruma grubuna sağ tıklayın ve ardından **tutarlılık denetimi gerçekleştir**.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-356">In hello protection area of hello Azure Backup Server console, right-click hello protection group and then select **Perform Consistency Check**.</span></span>

    <span data-ttu-id="b7b0e-357">Tıklatın **sonraki** toomove toohello sonraki sayfa.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-357">Click **Next** toomove toohello next page.</span></span>

9. <span data-ttu-id="b7b0e-358">Merhaba üzerinde **çevrimiçi koruma verilerini belirtin** sayfasında, tooprotect istediğiniz bir veya daha fazla veri kaynağını seçin.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-358">On hello **Specify Online Protection Data** page, select one or more data sources that you want tooprotect.</span></span> <span data-ttu-id="b7b0e-359">Merhaba üyeleri ayrı ayrı seçin veya tıklatın **Tümünü Seç** toochoose tüm üyeleri.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-359">You can select hello members individually, or click **Select All** toochoose all members.</span></span> <span data-ttu-id="b7b0e-360">Merhaba üyeleri seçtikten sonra tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-360">After you choose hello members, click **Next**.</span></span>

    ![Çevrimiçi koruma verilerini belirtin](./media/backup-azure-backup-server-vmware/select-data-to-protect.png)

10. <span data-ttu-id="b7b0e-362">Merhaba üzerinde **çevrimiçi yedekleme zamanlamasını belirtin** sayfasında, hello disk yedeğinden hello zamanlama toogenerate kurtarma noktalarını belirtin.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-362">On hello **Specify Online Backup Schedule** page, specify hello schedule toogenerate recovery points from hello disk backup.</span></span> <span data-ttu-id="b7b0e-363">Merhaba kurtarma noktası oluşturulduktan sonra Azure kurtarma Hizmetleri kasasına aktarılan toohello var.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-363">After hello recovery point is generated, it is transferred toohello Recovery Services vault in Azure.</span></span> <span data-ttu-id="b7b0e-364">İle çevrimiçi yedekleme zamanlamasını hello memnun kaldığınızda, tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-364">When you are satisfied with hello online backup schedule, click **Next**.</span></span>

    ![Çevrimiçi Yedekleme zamanlamasını belirtin](./media/backup-azure-backup-server-vmware/online-backup-schedule.png)

11. <span data-ttu-id="b7b0e-366">Merhaba üzerinde **çevrimiçi bekletme ilkesini belirtin** sayfasında, ne kadar süreyle tooretain hello yedek verileri Azure istediğinizi belirtin.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-366">On hello **Specify Online Retention Policy** page, indicate how long you want tooretain hello backup data in Azure.</span></span> <span data-ttu-id="b7b0e-367">Hello İlkesi tanımlandıktan sonra tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-367">After hello policy is defined, click **Next**.</span></span>

    ![Çevrimiçi bekletme ilkesini belirtin](./media/backup-azure-backup-server-vmware/retention-policy.png)

    <span data-ttu-id="b7b0e-369">Ne kadar veri Azure'da tutabilirsiniz için süre sınırı yoktur.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-369">There is no time limit for how long you can keep data in Azure.</span></span> <span data-ttu-id="b7b0e-370">Kurtarma noktası verilerini Azure'da depoladığınızda hello yalnızca korumalı örneği başına birden fazla 9999 kurtarma noktaları olamaz sınırıdır.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-370">When you store recovery point data in Azure, hello only limit is that you cannot have more than 9999 recovery points per protected instance.</span></span> <span data-ttu-id="b7b0e-371">Bu örnekte, hello korumalı örneği hello VMware sunucusudur.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-371">In this example, hello protected instance is hello VMware server.</span></span>

12. <span data-ttu-id="b7b0e-372">Merhaba üzerinde **Özet** sayfasında, ayarları ve koruma grubu üyeleri için hello ayrıntılarını gözden geçirin ve ardından **Grup Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="b7b0e-372">On hello **Summary** page, review hello details for your protection group members and settings, and then click **Create Group**.</span></span>

    ![Koruma grubu üyesi ve ayar özeti](./media/backup-azure-backup-server-vmware/protection-group-summary.png)

## <a name="next-steps"></a><span data-ttu-id="b7b0e-374">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b7b0e-374">Next steps</span></span>
<span data-ttu-id="b7b0e-375">Azure yedekleme sunucusu tooprotect VMware iş yükleri kullanırsanız, Azure yedekleme sunucusu toohelp korumak kullanarak ilgilenebilirsiniz bir [Microsoft Exchange server](./backup-azure-exchange-mabs.md), [Microsoft SharePoint grubu](./backup-azure-backup-sharepoint-mabs.md), veya bir [SQL Server veritabanı](./backup-azure-sql-mabs.md).</span><span class="sxs-lookup"><span data-stu-id="b7b0e-375">If you use Azure Backup Server tooprotect VMware workloads, you may be interested in using Azure Backup Server toohelp protect a [Microsoft Exchange server](./backup-azure-exchange-mabs.md), a [Microsoft SharePoint farm](./backup-azure-backup-sharepoint-mabs.md), or a [SQL Server database](./backup-azure-sql-mabs.md).</span></span>

<span data-ttu-id="b7b0e-376">Merhaba aracısını kaydetmeden sorunları hakkında daha fazla bilgi için bkz: hello koruma grubu yapılandırma veya işler, yedekleme [sorun giderme Azure yedekleme sunucusu](./backup-azure-mabs-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="b7b0e-376">For information on problems with registering hello agent, configuring hello protection group, or backing up jobs, see [Troubleshoot Azure Backup Server](./backup-azure-mabs-troubleshoot.md).</span></span>
