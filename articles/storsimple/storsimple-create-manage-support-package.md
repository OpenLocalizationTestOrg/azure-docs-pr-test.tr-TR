---
title: "Bir StorSimple destek paketi oluştur | Microsoft Docs"
description: "Oluşturma, şifresini ve StorSimple cihazınız için bir destek paketi düzenleme öğrenin."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: eac76f5f-5db1-4c92-af8c-54053b91e66c
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 32d20e7a8adcfc646c592213fe7395b87a93c985
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-a-storsimple-support-package"></a><span data-ttu-id="092cd-103">Oluşturma ve StorSimple destek paketi yönetme</span><span class="sxs-lookup"><span data-stu-id="092cd-103">Create and manage a StorSimple support package</span></span>
## <a name="overview"></a><span data-ttu-id="092cd-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="092cd-104">Overview</span></span>
<span data-ttu-id="092cd-105">Bir StorSimple destek paketi Microsoft Support StorSimple cihaz sorunları gidermenize yardımcı olacak tüm ilgili günlükleri toplayan bir kullanımı kolay mekanizmasıdır.</span><span class="sxs-lookup"><span data-stu-id="092cd-105">A StorSimple support package is an easy-to-use mechanism that collects all relevant logs to assist Microsoft Support with troubleshooting any StorSimple device issues.</span></span> <span data-ttu-id="092cd-106">Toplanan günlükleri şifrelenmiş ve sıkıştırılmış.</span><span class="sxs-lookup"><span data-stu-id="092cd-106">The collected logs are encrypted and compressed.</span></span>

<span data-ttu-id="092cd-107">Bu öğretici oluşturmak ve Destek Paketi yönetmek için adım adım yönergeler içerir.</span><span class="sxs-lookup"><span data-stu-id="092cd-107">This tutorial includes step-by-step instructions to create and manage the support package.</span></span>

## <a name="create-and-upload-a-support-package-in-the-azure-classic-portal"></a><span data-ttu-id="092cd-108">Oluşturma ve Azure Klasik portalında bir destek paketi yükleme</span><span class="sxs-lookup"><span data-stu-id="092cd-108">Create and upload a support package in the Azure classic portal</span></span>
<span data-ttu-id="092cd-109">Oluşturma ve Destek paketi Microsoft Support sitesini karşıya yükleme **Bakım** Klasik Azure portalı hizmetinde sayfası.</span><span class="sxs-lookup"><span data-stu-id="092cd-109">You can create and upload a support package to the Microsoft Support site through the **Maintenance** page of the service in the Azure classic portal.</span></span>

> [!NOTE]
> <span data-ttu-id="092cd-110">Karşıya yükleme desteği geçiş gerektirir.</span><span class="sxs-lookup"><span data-stu-id="092cd-110">The upload requires a support passkey.</span></span> <span data-ttu-id="092cd-111">Destek mühendisinize Bu size bir e-postayla sağlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="092cd-111">Your support engineer should provide this to you in an email.</span></span>
> 
> 

<span data-ttu-id="092cd-112">Şifrelenmiş ve sıkıştırılmış Destek Paketi (.cab dosyası) oluşturulur ve Destek siteye yüklenir.</span><span class="sxs-lookup"><span data-stu-id="092cd-112">An encrypted and compressed support package (.cab file) is created and uploaded to the Support site.</span></span> <span data-ttu-id="092cd-113">Destek mühendisine bu paket sorun giderme desteği sitesinden sonra alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="092cd-113">The support engineer can then retrieve this package from the Support site for troubleshooting the issue.</span></span>

<span data-ttu-id="092cd-114">Bir destek paketi oluşturmak için Klasik portalında aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="092cd-114">Perform the following steps in the classic portal to create a support package.</span></span>

#### <a name="to-create-a-support-package-in-the-azure-classic-portal"></a><span data-ttu-id="092cd-115">Klasik Azure portalında bir destek paketi oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="092cd-115">To create a support package in the Azure classic portal</span></span>
1. <span data-ttu-id="092cd-116">Seçin **aygıtları** > **Bakım**.</span><span class="sxs-lookup"><span data-stu-id="092cd-116">Select **Devices** > **Maintenance**.</span></span>
2. <span data-ttu-id="092cd-117">İçinde **destek paketi** bölümünde, select **oluşturma ve karşıya yükleme destek paketi**.</span><span class="sxs-lookup"><span data-stu-id="092cd-117">In the **Support package** section, select **Create and upload support package**.</span></span>
3. <span data-ttu-id="092cd-118">İçinde **oluşturma ve karşıya yükleme destek paketi** iletişim kutusunda, aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="092cd-118">In the **Create and upload support package** dialog box, do the following:</span></span>
   
    ![Destek Paketi Oluştur](./media/storsimple-create-manage-support-package/IC740923.png)
   
   * <span data-ttu-id="092cd-120">İçinde **destek geçiş** metin kutusuna, geçiş anahtarını girin.</span><span class="sxs-lookup"><span data-stu-id="092cd-120">In the **Support Passkey** text box, enter the passkey.</span></span> <span data-ttu-id="092cd-121">Microsoft destek mühendisinize bu geçiş, e-posta göndermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="092cd-121">Your Microsoft support engineer should send this passkey to you in email.</span></span>
   * <span data-ttu-id="092cd-122">Onay sağlamak için bu onay kutusunu işaretleyin destek paketi Microsoft Support sitesini otomatik olarak yüklenecek.</span><span class="sxs-lookup"><span data-stu-id="092cd-122">Select the check box to provide consent to automatically upload the support package to the Microsoft Support site.</span></span>
   * <span data-ttu-id="092cd-123">Onay simgesine tıklayarak</span><span class="sxs-lookup"><span data-stu-id="092cd-123">Click the check icon</span></span> ![Onay simgesi](./media/storsimple-create-manage-support-package/IC740895.png)<span data-ttu-id="092cd-125">.</span><span class="sxs-lookup"><span data-stu-id="092cd-125">.</span></span>

## <a name="manually-create-a-support-package"></a><span data-ttu-id="092cd-126">El ile bir destek paketi oluştur</span><span class="sxs-lookup"><span data-stu-id="092cd-126">Manually create a support package</span></span>
<span data-ttu-id="092cd-127">Bazı durumlarda, StorSimple için Windows PowerShell aracılığıyla destek paketi el ile oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="092cd-127">In some cases, you'll need to manually create the support package through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="092cd-128">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="092cd-128">For example:</span></span>

* <span data-ttu-id="092cd-129">Microsoft Support paylaşımı önce günlük dosyalarınızı hassas bilgileri kaldırmak gerekiyorsa.</span><span class="sxs-lookup"><span data-stu-id="092cd-129">If you need to remove sensitive information from your log files prior to sharing with Microsoft Support.</span></span>
* <span data-ttu-id="092cd-130">Bağlantı sorunları nedeniyle paketi karşıya zorluk yaşıyorsanız.</span><span class="sxs-lookup"><span data-stu-id="092cd-130">If you are having difficulty uploading the package due to connectivity issues.</span></span>

<span data-ttu-id="092cd-131">E-posta Microsoft Support el ile oluşturulan destek paketinizi paylaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="092cd-131">You can share your manually generated support package with Microsoft Support over email.</span></span> <span data-ttu-id="092cd-132">StorSimple için Windows PowerShell içinde bir destek paketi oluşturmak için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="092cd-132">Perform the following steps to create a support package in Windows PowerShell for StorSimple.</span></span>

#### <a name="to-create-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="092cd-133">StorSimple için Windows PowerShell içinde bir destek paketi oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="092cd-133">To create a support package in Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="092cd-134">StorSimple Cihazınızı bağlamak için kullanılan uzak bilgisayarda yönetici olarak bir Windows PowerShell oturumu başlatmak için aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="092cd-134">To start a Windows PowerShell session as an administrator on the remote computer that's used to connect to your StorSimple device, enter the following command:</span></span>
   
    `Start PowerShell`
2. <span data-ttu-id="092cd-135">Windows PowerShell oturumunda Cihazınızı SSAdmin Konsola bağlan:</span><span class="sxs-lookup"><span data-stu-id="092cd-135">In the Windows PowerShell session, connect to the SSAdmin Console of your device:</span></span>
   
   * <span data-ttu-id="092cd-136">Komut isteminde girin:</span><span class="sxs-lookup"><span data-stu-id="092cd-136">At the command prompt, enter:</span></span>
     
       `$MS = New-PSSession -ComputerName <IP address for DATA 0> -Credential SSAdmin -ConfigurationName "SSAdminConsole"`
   * <span data-ttu-id="092cd-137">Açılan iletişim kutusunda, cihaz Yöneticisi parolasını girin.</span><span class="sxs-lookup"><span data-stu-id="092cd-137">In the dialog box that opens, enter your device administrator password.</span></span> <span data-ttu-id="092cd-138">Varsayılan paroladır:</span><span class="sxs-lookup"><span data-stu-id="092cd-138">The default password is:</span></span>
     
      `Password1`
     
      ![PowerShell kimlik bilgisi iletişim kutusu](./media/storsimple-create-manage-support-package/IC740962.png)
   * <span data-ttu-id="092cd-140">**Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="092cd-140">Select **OK**.</span></span>
   * <span data-ttu-id="092cd-141">Komut isteminde girin:</span><span class="sxs-lookup"><span data-stu-id="092cd-141">At the command prompt, enter:</span></span>
     
      `Enter-PSSession $MS`
3. <span data-ttu-id="092cd-142">Açılan oturumda uygun komutunu girin.</span><span class="sxs-lookup"><span data-stu-id="092cd-142">In the session that opens, enter the appropriate command.</span></span>
   
   * <span data-ttu-id="092cd-143">Parola korumalı ağ paylaşımları için girin:</span><span class="sxs-lookup"><span data-stu-id="092cd-143">For network shares that are password protected, enter:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" –Credential "Username" -Force`
     
       <span data-ttu-id="092cd-144">(Destek Paketi şifrelendiğinden) bir ağ paylaşılan klasörüne ve bir şifreleme parolası yoluna bir parola istenir.</span><span class="sxs-lookup"><span data-stu-id="092cd-144">You'll be prompted for a password, a path to the network shared folder, and an encryption passphrase (because the support package is encrypted).</span></span> <span data-ttu-id="092cd-145">Bir destek paketi sonra belirtilen klasörde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="092cd-145">A support package is then created in the specified folder.</span></span>
   * <span data-ttu-id="092cd-146">Parola korumalı olmayan paylaşımlar için ihtiyacınız olmayan `-Credential` parametresi.</span><span class="sxs-lookup"><span data-stu-id="092cd-146">For shares that are not password protected, you do not need the `-Credential` parameter.</span></span> <span data-ttu-id="092cd-147">Aşağıdakileri girin:</span><span class="sxs-lookup"><span data-stu-id="092cd-147">Enter the following:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" -Force`
     
       <span data-ttu-id="092cd-148">Destek paketini hem denetleyicileri belirtilen ağ paylaşılan klasöründe oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="092cd-148">The support package is created for both controllers in the specified network shared folder.</span></span> <span data-ttu-id="092cd-149">Bu sorun giderme için Microsoft Support gönderilebilecek bir şifrelenmiş ve sıkıştırılmış dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="092cd-149">It's an encrypted, compressed file that can be sent to Microsoft Support for troubleshooting.</span></span> <span data-ttu-id="092cd-150">Daha fazla bilgi için bkz: [Microsoft Destek birimine başvurun](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="092cd-150">For more information, see [Contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>

### <a name="the-export-hcssupportpackage-cmdlet-parameters"></a><span data-ttu-id="092cd-151">Dışarı aktarma HcsSupportPackage cmdlet parametreleri</span><span class="sxs-lookup"><span data-stu-id="092cd-151">The Export-HcsSupportPackage cmdlet parameters</span></span>
<span data-ttu-id="092cd-152">Dışarı aktarma HcsSupportPackage cmdlet'iyle şu parametreleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="092cd-152">You can use the following parameters with the Export-HcsSupportPackage cmdlet.</span></span>

| <span data-ttu-id="092cd-153">Parametre</span><span class="sxs-lookup"><span data-stu-id="092cd-153">Parameter</span></span> | <span data-ttu-id="092cd-154">Gerekli/isteğe bağlı</span><span class="sxs-lookup"><span data-stu-id="092cd-154">Required/Optional</span></span> | <span data-ttu-id="092cd-155">Açıklama</span><span class="sxs-lookup"><span data-stu-id="092cd-155">Description</span></span> |
| --- | --- | --- |
| `-Path` |<span data-ttu-id="092cd-156">Gerekli</span><span class="sxs-lookup"><span data-stu-id="092cd-156">Required</span></span> |<span data-ttu-id="092cd-157">Destek paketini yerleştirildiği ağ paylaşılan klasörün konumunu belirtmek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="092cd-157">Use to provide the location of the network shared folder in which the support package is placed.</span></span> |
| `-EncryptionPassphrase` |<span data-ttu-id="092cd-158">Gerekli</span><span class="sxs-lookup"><span data-stu-id="092cd-158">Required</span></span> |<span data-ttu-id="092cd-159">Destek Paketi şifrelemek yardımcı olmak için bir parola sağlamak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="092cd-159">Use to provide a passphrase to help encrypt the support package.</span></span> |
| `-Credential` |<span data-ttu-id="092cd-160">İsteğe bağlı</span><span class="sxs-lookup"><span data-stu-id="092cd-160">Optional</span></span> |<span data-ttu-id="092cd-161">Ağ paylaşılan klasörüne erişim kimlik bilgileri sağlamak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="092cd-161">Use to supply access credentials for the network shared folder.</span></span> |
| `-Force` |<span data-ttu-id="092cd-162">İsteğe bağlı</span><span class="sxs-lookup"><span data-stu-id="092cd-162">Optional</span></span> |<span data-ttu-id="092cd-163">Şifreleme parolası onayı adımı atlamak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="092cd-163">Use to skip the encryption passphrase confirmation step.</span></span> |
| `-PackageTag` |<span data-ttu-id="092cd-164">İsteğe bağlı</span><span class="sxs-lookup"><span data-stu-id="092cd-164">Optional</span></span> |<span data-ttu-id="092cd-165">Bir dizini altında belirtmek için kullanın *yolu* destek paketi yerleştirildiği içinde.</span><span class="sxs-lookup"><span data-stu-id="092cd-165">Use to specify a directory under *Path* in which the support package is placed.</span></span> <span data-ttu-id="092cd-166">Varsayılan değer [aygıt adı]-[geçerli tarih ve time:yyyy-MM-dd-HH-mm-ss].</span><span class="sxs-lookup"><span data-stu-id="092cd-166">The default is [device name]-[current date and time:yyyy-MM-dd-HH-mm-ss].</span></span> |
| `-Scope` |<span data-ttu-id="092cd-167">İsteğe bağlı</span><span class="sxs-lookup"><span data-stu-id="092cd-167">Optional</span></span> |<span data-ttu-id="092cd-168">Olarak belirttiğiniz **küme** hem denetleyicileri için bir destek paketi oluşturmak için (varsayılan).</span><span class="sxs-lookup"><span data-stu-id="092cd-168">Specify as **Cluster** (default) to create a support package for both controllers.</span></span> <span data-ttu-id="092cd-169">Geçerli denetleyici için yalnızca bir paketi oluşturmak istiyorsanız, belirtin **denetleyicisi**.</span><span class="sxs-lookup"><span data-stu-id="092cd-169">If you want to create a package only for the current controller, specify **Controller**.</span></span> |

## <a name="edit-a-support-package"></a><span data-ttu-id="092cd-170">Destek paketini Düzenle</span><span class="sxs-lookup"><span data-stu-id="092cd-170">Edit a support package</span></span>
<span data-ttu-id="092cd-171">Bir destek paketi oluşturduktan sonra hassas bilgileri kaldırmak için paketi düzenleyin gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="092cd-171">After you have generated a support package, you might need to edit the package to remove sensitive information.</span></span> <span data-ttu-id="092cd-172">Bu, birim adları, cihaz IP adresleri ve günlük dosyalarını yedekleme adlarından içerebilir.</span><span class="sxs-lookup"><span data-stu-id="092cd-172">This can include volume names, device IP addresses, and backup names from the log files.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="092cd-173">Yalnızca StorSimple için Windows PowerShell aracılığıyla oluşturulan bir destek paketi düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="092cd-173">You can only edit a support package that was generated through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="092cd-174">StorSimple Yöneticisi hizmetiyle Azure Klasik portalında oluşturulan bir paket düzenleyemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="092cd-174">You can't edit a package created in the Azure classic portal with StorSimple Manager service.</span></span>
> 
> 

<span data-ttu-id="092cd-175">Microsoft Support sitesinde karşıya yüklemeden önce bir destek paketi düzenlemek, ilk destek paketi şifresini, dosyaları düzenleyin ve yeniden şifrelemek için.</span><span class="sxs-lookup"><span data-stu-id="092cd-175">To edit a support package before uploading it on the Microsoft Support site, first decrypt the support package, edit the files, and then re-encrypt it.</span></span> <span data-ttu-id="092cd-176">Aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="092cd-176">Perform the following steps.</span></span>

#### <a name="to-edit-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="092cd-177">StorSimple için Windows PowerShell desteği paketinde düzenlemek için</span><span class="sxs-lookup"><span data-stu-id="092cd-177">To edit a support package in Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="092cd-178">Açıklandığı gibi daha önce bir destek paketi oluştur [StorSimple için Windows PowerShell içinde bir destek paketi oluşturmak için](#to-create-a-support-package-in-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="092cd-178">Generate a support package as described earlier, in [To create a support package in Windows PowerShell for StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).</span></span>
2. <span data-ttu-id="092cd-179">[Komut dosyasını karşıdan](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) istemciniz yerel olarak.</span><span class="sxs-lookup"><span data-stu-id="092cd-179">[Download the script](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) locally on your client.</span></span>
3. <span data-ttu-id="092cd-180">Windows PowerShell modülünü içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="092cd-180">Import the Windows PowerShell module.</span></span> <span data-ttu-id="092cd-181">Komut dosyası karşıdan yerel klasörün yolunu belirtin.</span><span class="sxs-lookup"><span data-stu-id="092cd-181">Specify the path to the local folder in which you downloaded the script.</span></span> <span data-ttu-id="092cd-182">Modülü içeri aktarmak için şunu girin:</span><span class="sxs-lookup"><span data-stu-id="092cd-182">To import the module, enter:</span></span>
   
    `Import-module <Path to the folder that contains the Windows PowerShell script>`
4. <span data-ttu-id="092cd-183">Tüm dosyalar *.aes* sıkıştırılmış ve şifrelenmiş dosyalar.</span><span class="sxs-lookup"><span data-stu-id="092cd-183">All the files are *.aes* files that are compressed and encrypted.</span></span> <span data-ttu-id="092cd-184">Sıkıştırmasını açın ve dosyaların şifresini çözmek için şunu girin:</span><span class="sxs-lookup"><span data-stu-id="092cd-184">To decompress and decrypt files, enter:</span></span>
   
    `Open-HcsSupportPackage <Path to the folder that contains support package files>`
   
    <span data-ttu-id="092cd-185">Gerçek dosya uzantıları için tüm dosyalar artık görüntülendiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="092cd-185">Note that the actual file extensions are now displayed for all the files.</span></span>
   
    ![Destek paketini Düzenle](./media/storsimple-create-manage-support-package/IC750706.png)
5. <span data-ttu-id="092cd-187">Şifreleme parolası istendiğinde, destek paketi oluştururken kullandığınız parolayı girin.</span><span class="sxs-lookup"><span data-stu-id="092cd-187">When you're prompted for the encryption passphrase, enter the passphrase that you used when the support package was created.</span></span>
   
        cmdlet Open-HcsSupportPackage at command pipeline position 1
   
        Supply values for the following parameters:EncryptionPassphrase: ****
6. <span data-ttu-id="092cd-188">Günlük dosyalarını içeren klasöre gidin.</span><span class="sxs-lookup"><span data-stu-id="092cd-188">Browse to the folder that contains the log files.</span></span> <span data-ttu-id="092cd-189">Günlük dosyalarının şimdi sıkıştırması açılmış ve şifresi çünkü bunlar özgün dosya uzantılarını sahip olur.</span><span class="sxs-lookup"><span data-stu-id="092cd-189">Because the log files are now decompressed and decrypted, these will have original file extensions.</span></span> <span data-ttu-id="092cd-190">Birim adları ve cihaz IP adresleri gibi herhangi bir müşteriye özgü bilgileri kaldırmak için bu dosyalarda değişiklik ve dosyaları kaydedebilir.</span><span class="sxs-lookup"><span data-stu-id="092cd-190">Modify these files to remove any customer-specific information, such as volume names and device IP addresses, and save the files.</span></span>
7. <span data-ttu-id="092cd-191">Gzip ile sıkıştırmak ve AES 256 ile şifrelemek için dosyaları kapatın.</span><span class="sxs-lookup"><span data-stu-id="092cd-191">Close the files to compress them with gzip and encrypt them with AES-256.</span></span> <span data-ttu-id="092cd-192">Bu hız ve Destek paketi bir ağ üzerinden aktarılması güvenliği içindir.</span><span class="sxs-lookup"><span data-stu-id="092cd-192">This is for speed and security in transferring the support package over a network.</span></span> <span data-ttu-id="092cd-193">Sıkıştır ve dosyaları şifrelemek için aşağıdakileri girin:</span><span class="sxs-lookup"><span data-stu-id="092cd-193">To compress and encrypt files, enter the following:</span></span>
   
    `Close-HcsSupportPackage <Path to the folder that contains support package files>`
   
    ![Destek paketini Düzenle](./media/storsimple-create-manage-support-package/IC750707.png)
8. <span data-ttu-id="092cd-195">İstendiğinde, bir şifreleme parolası değiştirilmiş destek paketi için belirtin.</span><span class="sxs-lookup"><span data-stu-id="092cd-195">When prompted, provide an encryption passphrase for the modified support package.</span></span>
   
        cmdlet Close-HcsSupportPackage at command pipeline position 1
        Supply values for the following parameters:EncryptionPassphrase: ****
9. <span data-ttu-id="092cd-196">Microsoft istendiğinde Support paylaşmanızı sağlayan yeni parolayı not yazın.</span><span class="sxs-lookup"><span data-stu-id="092cd-196">Write down the new passphrase, so that you can share it with Microsoft Support when requested.</span></span>

### <a name="example-editing-files-in-a-support-package-on-a-password-protected-share"></a><span data-ttu-id="092cd-197">Örnek: parola korumalı bir paylaşılan bir destek paketi dosyalarını düzenleme</span><span class="sxs-lookup"><span data-stu-id="092cd-197">Example: Editing files in a support package on a password-protected share</span></span>
<span data-ttu-id="092cd-198">Aşağıdaki örnek, şifre çözme, düzenleme ve Destek paketi yeniden şifrele gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="092cd-198">The following example shows how to decrypt, edit, and re-encrypt a support package.</span></span>

        PS C:\WINDOWS\system32> Import-module C:\Users\Default\StorSimple\SupportPackage\HCSSupportPackageTools.psm1

        PS C:\WINDOWS\system32> Open-HcsSupportPackage \\hcsfs\Logs\TD48\TD48Logs\C0-A\etw

        cmdlet Open-HcsSupportPackage at command pipeline position 1

        Supply values for the following parameters:

        EncryptionPassphrase: ****

        PS C:\WINDOWS\system32> Close-HcsSupportPackage \\hcsfs\Logs\TD48\TD48Logs\C0-A\etw

        cmdlet Close-HcsSupportPackage at command pipeline position 1

        Supply values for the following parameters:

        EncryptionPassphrase: ****

        PS C:\WINDOWS\system32>

## <a name="next-steps"></a><span data-ttu-id="092cd-199">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="092cd-199">Next steps</span></span>
* <span data-ttu-id="092cd-200">Bilgi nasıl [aygıt dağıtımınızı gidermek için destek paketler ve cihaz günlükleri kullanan](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="092cd-200">Learn how to [use support packages and device logs to troubleshoot your device deployment](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).</span></span>
* <span data-ttu-id="092cd-201">Bilgi edinmek için nasıl [StorSimple Cihazınızı yönetmek için StorSimple Yöneticisi hizmetini kullanma](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="092cd-201">Learn how to [use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

