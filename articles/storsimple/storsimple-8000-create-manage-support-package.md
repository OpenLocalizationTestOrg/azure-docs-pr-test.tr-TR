---
title: aaaCreate StorSimple 8000 serisi destek paketi | Microsoft Docs
description: "Nasıl toocreate, şifresini ve StorSimple 8000 serisi cihazınız için bir destek paketini Düzenle öğrenin."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/05/2017
ms.author: alkohli
ms.openlocfilehash: 857555b6ba31b1527f8f00d19818ebbec6005d0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-a-support-package-for-storsimple-8000-series"></a><span data-ttu-id="c63f4-103">Oluşturma ve StorSimple 8000 serisi için bir destek paketi yönetme</span><span class="sxs-lookup"><span data-stu-id="c63f4-103">Create and manage a support package for StorSimple 8000 series</span></span>

## <a name="overview"></a><span data-ttu-id="c63f4-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="c63f4-104">Overview</span></span>

<span data-ttu-id="c63f4-105">Bir StorSimple destek paketi StorSimple cihaz sorunları gidermeye tüm ilgili günlükleri tooassist Microsoft Support toplayan bir kullanımı kolay mekanizmasıdır.</span><span class="sxs-lookup"><span data-stu-id="c63f4-105">A StorSimple support package is an easy-to-use mechanism that collects all relevant logs tooassist Microsoft Support with troubleshooting any StorSimple device issues.</span></span> <span data-ttu-id="c63f4-106">Merhaba toplanan günlükleri şifrelenmiş sıkıştırılmış ve.</span><span class="sxs-lookup"><span data-stu-id="c63f4-106">hello collected logs are encrypted and compressed.</span></span>

<span data-ttu-id="c63f4-107">Bu öğretici hakkında adım adım yönergeler toocreate içerir ve StorSimple 8000 serisi cihazınız için hello destek paketi yönetin.</span><span class="sxs-lookup"><span data-stu-id="c63f4-107">This tutorial includes step-by-step instructions toocreate and manage hello support package for your StorSimple 8000 series device.</span></span> <span data-ttu-id="c63f4-108">Bir StorSimple sanal dizisi ile çalışıyorsanız, çok Git[günlük paketi oluşturmak](storsimple-ova-web-ui-admin.md#generate-a-log-package).</span><span class="sxs-lookup"><span data-stu-id="c63f4-108">If you are working with a StorSimple Virtual Array, go too[generate a log package](storsimple-ova-web-ui-admin.md#generate-a-log-package).</span></span>

## <a name="create-a-support-package"></a><span data-ttu-id="c63f4-109">Bir destek paketi oluştur</span><span class="sxs-lookup"><span data-stu-id="c63f4-109">Create a support package</span></span>

<span data-ttu-id="c63f4-110">Bazı durumlarda, gerekir toomanually StorSimple için Windows PowerShell üzerinden hello destek paketi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c63f4-110">In some cases, you'll need toomanually create hello support package through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="c63f4-111">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="c63f4-111">For example:</span></span>

* <span data-ttu-id="c63f4-112">Tooremove hassas bilgileri, günlüğünden gerekirse Microsoft Support önceki toosharing dosyaları.</span><span class="sxs-lookup"><span data-stu-id="c63f4-112">If you need tooremove sensitive information from your log files prior toosharing with Microsoft Support.</span></span>
* <span data-ttu-id="c63f4-113">Merhaba paket tooconnectivity sorunları nedeniyle karşıya zorluk yaşıyorsanız.</span><span class="sxs-lookup"><span data-stu-id="c63f4-113">If you are having difficulty uploading hello package due tooconnectivity issues.</span></span>

<span data-ttu-id="c63f4-114">E-posta Microsoft Support el ile oluşturulan destek paketinizi paylaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c63f4-114">You can share your manually generated support package with Microsoft Support over email.</span></span> <span data-ttu-id="c63f4-115">StorSimple için Windows PowerShell desteği paketinde adımları toocreate aşağıdaki hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="c63f4-115">Perform hello following steps toocreate a support package in Windows PowerShell for StorSimple.</span></span>

#### <a name="toocreate-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="c63f4-116">toocreate StorSimple için Windows PowerShell desteği paketinde</span><span class="sxs-lookup"><span data-stu-id="c63f4-116">toocreate a support package in Windows PowerShell for StorSimple</span></span>

1. <span data-ttu-id="c63f4-117">toostart tooconnect tooyour StorSimple cihazı kullandığı hello uzak bilgisayarda yönetici olarak Windows PowerShell oturumu bir hello aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="c63f4-117">toostart a Windows PowerShell session as an administrator on hello remote computer that's used tooconnect tooyour StorSimple device, enter hello following command:</span></span>
   
    `Start PowerShell`
2. <span data-ttu-id="c63f4-118">Merhaba Windows PowerShell oturumunda toohello Cihazınızı SSAdmin konsoluna Bağlan:</span><span class="sxs-lookup"><span data-stu-id="c63f4-118">In hello Windows PowerShell session, connect toohello SSAdmin Console of your device:</span></span>
   
   1. <span data-ttu-id="c63f4-119">Merhaba komut isteminde girin:</span><span class="sxs-lookup"><span data-stu-id="c63f4-119">At hello command prompt, enter:</span></span>
     
       `$MS = New-PSSession -ComputerName <IP address for DATA 0> -Credential SSAdmin -ConfigurationName "SSAdminConsole"`
   2. <span data-ttu-id="c63f4-120">Açılan hello iletişim kutusunda, cihaz Yönetici parolanızı girin.</span><span class="sxs-lookup"><span data-stu-id="c63f4-120">In hello dialog box that opens, enter your device administrator password.</span></span> <span data-ttu-id="c63f4-121">Merhaba varsayılan parola _Parola1_.</span><span class="sxs-lookup"><span data-stu-id="c63f4-121">hello default password is _Password1_.</span></span>
     
      ![PowerShell kimlik bilgisi iletişim kutusu](./media/storsimple-8000-create-manage-support-package/IC740962.png)
   3. <span data-ttu-id="c63f4-123">**Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="c63f4-123">Select **OK**.</span></span>
   4. <span data-ttu-id="c63f4-124">Merhaba komut isteminde girin:</span><span class="sxs-lookup"><span data-stu-id="c63f4-124">At hello command prompt, enter:</span></span>
     
      `Enter-PSSession $MS`
3. <span data-ttu-id="c63f4-125">Açılır hello oturumunda hello uygun komutu girin.</span><span class="sxs-lookup"><span data-stu-id="c63f4-125">In hello session that opens, enter hello appropriate command.</span></span>
   
   * <span data-ttu-id="c63f4-126">Parola korumalı ağ paylaşımları için girin:</span><span class="sxs-lookup"><span data-stu-id="c63f4-126">For network shares that are password protected, enter:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" –Credential "Username" -Force`
     
       <span data-ttu-id="c63f4-127">(Merhaba destek paketi şifrelendiğinden) bir parola, bir yol toohello ağ paylaşılan klasörüne ve bir şifreleme parolası istenir.</span><span class="sxs-lookup"><span data-stu-id="c63f4-127">You'll be prompted for a password, a path toohello network shared folder, and an encryption passphrase (because hello support package is encrypted).</span></span> <span data-ttu-id="c63f4-128">Bir destek paketi sonra hello belirtilen klasörde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c63f4-128">A support package is then created in hello specified folder.</span></span>
   * <span data-ttu-id="c63f4-129">Parola korumalı olmayan paylaşımlar için hello gerekmez `-Credential` parametresi.</span><span class="sxs-lookup"><span data-stu-id="c63f4-129">For shares that are not password protected, you do not need hello `-Credential` parameter.</span></span> <span data-ttu-id="c63f4-130">Merhaba aşağıdakileri girin:</span><span class="sxs-lookup"><span data-stu-id="c63f4-130">Enter hello following:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" -Force`
     
       <span data-ttu-id="c63f4-131">Merhaba destek paketi hem denetleyicileri hello belirtilen ağ paylaşılan klasöründe oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c63f4-131">hello support package is created for both controllers in hello specified network shared folder.</span></span> <span data-ttu-id="c63f4-132">Bu sorun giderme için tooMicrosoft destek gönderilebilecek bir şifrelenmiş ve sıkıştırılmış dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="c63f4-132">It's an encrypted, compressed file that can be sent tooMicrosoft Support for troubleshooting.</span></span> <span data-ttu-id="c63f4-133">Daha fazla bilgi için bkz: [Microsoft Destek birimine başvurun](storsimple-8000-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="c63f4-133">For more information, see [Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>

### <a name="hello-export-hcssupportpackage-cmdlet-parameters"></a><span data-ttu-id="c63f4-134">Merhaba verme HcsSupportPackage cmdlet parametreleri</span><span class="sxs-lookup"><span data-stu-id="c63f4-134">hello Export-HcsSupportPackage cmdlet parameters</span></span>

<span data-ttu-id="c63f4-135">Şu parametreler hello verme HcsSupportPackage cmdlet ile Merhaba kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c63f4-135">You can use hello following parameters with hello Export-HcsSupportPackage cmdlet.</span></span>

| <span data-ttu-id="c63f4-136">Parametre</span><span class="sxs-lookup"><span data-stu-id="c63f4-136">Parameter</span></span> | <span data-ttu-id="c63f4-137">Gerekli/isteğe bağlı</span><span class="sxs-lookup"><span data-stu-id="c63f4-137">Required/Optional</span></span> | <span data-ttu-id="c63f4-138">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c63f4-138">Description</span></span> |
| --- | --- | --- |
| `-Path` |<span data-ttu-id="c63f4-139">Gerekli</span><span class="sxs-lookup"><span data-stu-id="c63f4-139">Required</span></span> |<span data-ttu-id="c63f4-140">Merhaba ağ paylaşılan klasörüne hangi hello destek paketi yerleştirilir tooprovide hello konumu kullanın.</span><span class="sxs-lookup"><span data-stu-id="c63f4-140">Use tooprovide hello location of hello network shared folder in which hello support package is placed.</span></span> |
| `-EncryptionPassphrase` |<span data-ttu-id="c63f4-141">Gerekli</span><span class="sxs-lookup"><span data-stu-id="c63f4-141">Required</span></span> |<span data-ttu-id="c63f4-142">Kullanım tooprovide parola toohelp hello destek paketi şifreleyin.</span><span class="sxs-lookup"><span data-stu-id="c63f4-142">Use tooprovide a passphrase toohelp encrypt hello support package.</span></span> |
| `-Credential` |<span data-ttu-id="c63f4-143">İsteğe bağlı</span><span class="sxs-lookup"><span data-stu-id="c63f4-143">Optional</span></span> |<span data-ttu-id="c63f4-144">Toosupply erişim kimlik bilgileri hello ağ paylaşılan klasör için kullanın.</span><span class="sxs-lookup"><span data-stu-id="c63f4-144">Use toosupply access credentials for hello network shared folder.</span></span> |
| `-Force` |<span data-ttu-id="c63f4-145">İsteğe bağlı</span><span class="sxs-lookup"><span data-stu-id="c63f4-145">Optional</span></span> |<span data-ttu-id="c63f4-146">Tooskip hello şifreleme parolası onayı adımını kullanın.</span><span class="sxs-lookup"><span data-stu-id="c63f4-146">Use tooskip hello encryption passphrase confirmation step.</span></span> |
| `-PackageTag` |<span data-ttu-id="c63f4-147">İsteğe bağlı</span><span class="sxs-lookup"><span data-stu-id="c63f4-147">Optional</span></span> |<span data-ttu-id="c63f4-148">Bir dizini altında toospecify kullanmak *yol* hangi hello destek paketi yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="c63f4-148">Use toospecify a directory under *Path* in which hello support package is placed.</span></span> <span data-ttu-id="c63f4-149">Merhaba varsayılandır [aygıt adı]-[geçerli tarih ve time:yyyy-MM-dd-HH-mm-ss].</span><span class="sxs-lookup"><span data-stu-id="c63f4-149">hello default is [device name]-[current date and time:yyyy-MM-dd-HH-mm-ss].</span></span> |
| `-Scope` |<span data-ttu-id="c63f4-150">İsteğe bağlı</span><span class="sxs-lookup"><span data-stu-id="c63f4-150">Optional</span></span> |<span data-ttu-id="c63f4-151">Olarak belirttiğiniz **küme** (varsayılan) toocreate hem denetleyicileri için bir destek paketi.</span><span class="sxs-lookup"><span data-stu-id="c63f4-151">Specify as **Cluster** (default) toocreate a support package for both controllers.</span></span> <span data-ttu-id="c63f4-152">Yalnızca hello geçerli denetleyici için bir paket toocreate istiyorsanız belirtin **denetleyicisi**.</span><span class="sxs-lookup"><span data-stu-id="c63f4-152">If you want toocreate a package only for hello current controller, specify **Controller**.</span></span> |

## <a name="edit-a-support-package"></a><span data-ttu-id="c63f4-153">Destek paketini Düzenle</span><span class="sxs-lookup"><span data-stu-id="c63f4-153">Edit a support package</span></span>

<span data-ttu-id="c63f4-154">Bir destek paketi oluşturduktan sonra tooedit hello paket tooremove hassas bilgileri gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="c63f4-154">After you have generated a support package, you might need tooedit hello package tooremove sensitive information.</span></span> <span data-ttu-id="c63f4-155">Bu, birim adları, cihaz IP adresleri ve hello günlük dosyalarındaki yedek adları içerebilir.</span><span class="sxs-lookup"><span data-stu-id="c63f4-155">This can include volume names, device IP addresses, and backup names from hello log files.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c63f4-156">Yalnızca StorSimple için Windows PowerShell aracılığıyla oluşturulan bir destek paketi düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c63f4-156">You can only edit a support package that was generated through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="c63f4-157">Merhaba StorSimple cihaz Yöneticisi hizmeti Azure portalıyla oluşturulan bir paket düzenleyemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="c63f4-157">You can't edit a package created in hello Azure portal with StorSimple Device Manager service.</span></span>

<span data-ttu-id="c63f4-158">tooedit hello Microsoft Support sitesini üzerinde karşıya yüklemeden önce bir destek paketi ilk hello destek paketi şifresini, hello dosyaları düzenleyin ve yeniden şifrelemek.</span><span class="sxs-lookup"><span data-stu-id="c63f4-158">tooedit a support package before uploading it on hello Microsoft Support site, first decrypt hello support package, edit hello files, and then re-encrypt it.</span></span> <span data-ttu-id="c63f4-159">Merhaba aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="c63f4-159">Perform hello following steps.</span></span>

#### <a name="tooedit-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="c63f4-160">tooedit StorSimple için Windows PowerShell desteği paketinde</span><span class="sxs-lookup"><span data-stu-id="c63f4-160">tooedit a support package in Windows PowerShell for StorSimple</span></span>

1. <span data-ttu-id="c63f4-161">Açıklandığı gibi daha önce bir destek paketi oluştur [toocreate StorSimple için Windows PowerShell desteği paketinde](#to-create-a-support-package-in-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="c63f4-161">Generate a support package as described earlier, in [toocreate a support package in Windows PowerShell for StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).</span></span>
2. <span data-ttu-id="c63f4-162">[Karşıdan yükleme Hello komut](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) istemciniz yerel olarak.</span><span class="sxs-lookup"><span data-stu-id="c63f4-162">[Download hello script](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) locally on your client.</span></span>
3. <span data-ttu-id="c63f4-163">Merhaba Windows PowerShell modülünü içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="c63f4-163">Import hello Windows PowerShell module.</span></span> <span data-ttu-id="c63f4-164">Merhaba yolu toohello yerel klasör hello betiği indirildi belirtin.</span><span class="sxs-lookup"><span data-stu-id="c63f4-164">Specify hello path toohello local folder in which you downloaded hello script.</span></span> <span data-ttu-id="c63f4-165">tooimport hello modülü girin:</span><span class="sxs-lookup"><span data-stu-id="c63f4-165">tooimport hello module, enter:</span></span>
   
    `Import-module <Path toohello folder that contains hello Windows PowerShell script>`
4. <span data-ttu-id="c63f4-166">Tüm hello dosyalar *.aes* sıkıştırılmış ve şifrelenmiş dosyalar.</span><span class="sxs-lookup"><span data-stu-id="c63f4-166">All hello files are *.aes* files that are compressed and encrypted.</span></span> <span data-ttu-id="c63f4-167">toodecompress ve şifre çözme dosyaları girin:</span><span class="sxs-lookup"><span data-stu-id="c63f4-167">toodecompress and decrypt files, enter:</span></span>
   
    `Open-HcsSupportPackage <Path toohello folder that contains support package files>`
   
    <span data-ttu-id="c63f4-168">Hello gerçek dosya uzantıları için tüm hello dosyaları şimdi görüntülenen unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c63f4-168">Note that hello actual file extensions are now displayed for all hello files.</span></span>
   
    ![Destek paketini Düzenle](./media/storsimple-8000-create-manage-support-package/IC750706.png)
5. <span data-ttu-id="c63f4-170">Merhaba şifreleme parolası istendiğinde hello destek paketi oluştururken kullandığınız hello parola girin.</span><span class="sxs-lookup"><span data-stu-id="c63f4-170">When you're prompted for hello encryption passphrase, enter hello passphrase that you used when hello support package was created.</span></span>
   
        cmdlet Open-HcsSupportPackage at command pipeline position 1
   
        Supply values for hello following parameters:EncryptionPassphrase: ****
6. <span data-ttu-id="c63f4-171">Merhaba günlük dosyalarını içeren toohello klasörüne göz atın.</span><span class="sxs-lookup"><span data-stu-id="c63f4-171">Browse toohello folder that contains hello log files.</span></span> <span data-ttu-id="c63f4-172">Merhaba günlük dosyalarının şimdi sıkıştırması açılmış ve şifresi çünkü bunlar özgün dosya uzantılarını sahip olur.</span><span class="sxs-lookup"><span data-stu-id="c63f4-172">Because hello log files are now decompressed and decrypted, these will have original file extensions.</span></span> <span data-ttu-id="c63f4-173">Bu dosyaları tooremove birim adları ve cihaz IP adresleri gibi herhangi bir müşteriye özgü bilgisi değiştirin ve hello dosyalarını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="c63f4-173">Modify these files tooremove any customer-specific information, such as volume names and device IP addresses, and save hello files.</span></span>
7. <span data-ttu-id="c63f4-174">Kapat hello dosyaları toocompress gzip ile bunları ve AES 256 ile şifreleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c63f4-174">Close hello files toocompress them with gzip and encrypt them with AES-256.</span></span> <span data-ttu-id="c63f4-175">Bu hız ve hello destek paketi bir ağ üzerinden aktarılması güvenliği içindir.</span><span class="sxs-lookup"><span data-stu-id="c63f4-175">This is for speed and security in transferring hello support package over a network.</span></span> <span data-ttu-id="c63f4-176">toocompress ve dosyaları şifrelemek, hello aşağıdakileri girin:</span><span class="sxs-lookup"><span data-stu-id="c63f4-176">toocompress and encrypt files, enter hello following:</span></span>
   
    `Close-HcsSupportPackage <Path toohello folder that contains support package files>`
   
    ![Destek paketini Düzenle](./media/storsimple-8000-create-manage-support-package/IC750707.png)
8. <span data-ttu-id="c63f4-178">İstendiğinde, bir şifreleme parolası hello değiştirilmiş destek paketi için belirtin.</span><span class="sxs-lookup"><span data-stu-id="c63f4-178">When prompted, provide an encryption passphrase for hello modified support package.</span></span>
   
        cmdlet Close-HcsSupportPackage at command pipeline position 1
        Supply values for hello following parameters:EncryptionPassphrase: ****
9. <span data-ttu-id="c63f4-179">Microsoft istendiğinde Support paylaşmanızı sağlayan hello yeni parolayı not ettiğinizden.</span><span class="sxs-lookup"><span data-stu-id="c63f4-179">Write down hello new passphrase, so that you can share it with Microsoft Support when requested.</span></span>

### <a name="example-editing-files-in-a-support-package-on-a-password-protected-share"></a><span data-ttu-id="c63f4-180">Örnek: parola korumalı bir paylaşılan bir destek paketi dosyalarını düzenleme</span><span class="sxs-lookup"><span data-stu-id="c63f4-180">Example: Editing files in a support package on a password-protected share</span></span>

<span data-ttu-id="c63f4-181">Aşağıdaki örneğine hello nasıl toodecrypt, düzenlemek ve bir destek paketi yeniden şifrele gösterir.</span><span class="sxs-lookup"><span data-stu-id="c63f4-181">hello following example shows how toodecrypt, edit, and re-encrypt a support package.</span></span>

        PS C:\WINDOWS\system32> Import-module C:\Users\Default\StorSimple\SupportPackage\HCSSupportPackageTools.psm1

        PS C:\WINDOWS\system32> Open-HcsSupportPackage \\hcsfs\Logs\TD48\TD48Logs\C0-A\etw

        cmdlet Open-HcsSupportPackage at command pipeline position 1

        Supply values for hello following parameters:

        EncryptionPassphrase: ****

        PS C:\WINDOWS\system32> Close-HcsSupportPackage \\hcsfs\Logs\TD48\TD48Logs\C0-A\etw

        cmdlet Close-HcsSupportPackage at command pipeline position 1

        Supply values for hello following parameters:

        EncryptionPassphrase: ****

        PS C:\WINDOWS\system32>

## <a name="next-steps"></a><span data-ttu-id="c63f4-182">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c63f4-182">Next steps</span></span>

* <span data-ttu-id="c63f4-183">Merhaba hakkında bilgi edinin [hello destek paketi toplanan bilgiler](https://support.microsoft.com/help/3193606/storsimple-support-packages-and-device-logs)</span><span class="sxs-lookup"><span data-stu-id="c63f4-183">Learn about hello [information collected in hello Support package](https://support.microsoft.com/help/3193606/storsimple-support-packages-and-device-logs)</span></span>
* <span data-ttu-id="c63f4-184">Nasıl çok öğrenin[kullanma desteği paketler ve cihaz oturum tootroubleshoot aygıt dağıtımınızı](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="c63f4-184">Learn how too[use support packages and device logs tootroubleshoot your device deployment](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).</span></span>
* <span data-ttu-id="c63f4-185">Nasıl çok öğrenin[kullanım StorSimple Cihazınızı StorSimple cihaz Yöneticisi hizmeti tooadminister hello](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="c63f4-185">Learn how too[use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

