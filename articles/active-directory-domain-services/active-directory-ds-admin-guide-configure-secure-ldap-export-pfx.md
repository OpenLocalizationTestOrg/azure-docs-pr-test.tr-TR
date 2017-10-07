---
title: "Güvenli LDAP (LDAPS) Azure AD Etki Alanı Hizmetleri'nde aaaConfigure | Microsoft Docs"
description: "Güvenli LDAP (LDAPS) bir Azure AD etki alanı Hizmetleri yönetilen etki alanını yapılandırın"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c6da94b6-4328-4230-801a-4b646055d4d7
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: maheshu
ms.openlocfilehash: 356b28f8392b0e203df9c81177ec842d52866c4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="ba70f-103">Güvenli LDAP (LDAPS) Azure AD etki alanı Hizmetleri yönetilen etki alanı için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ba70f-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ba70f-104">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="ba70f-104">Before you begin</span></span>
<span data-ttu-id="ba70f-105">Tamamlandı olun [görev 1 - güvenli LDAP için bir sertifika edinin](active-directory-ds-admin-guide-configure-secure-ldap.md).</span><span class="sxs-lookup"><span data-stu-id="ba70f-105">Ensure you've completed [Task 1 - obtain a certificate for secure LDAP](active-directory-ds-admin-guide-configure-secure-ldap.md).</span></span>


## <a name="task-2---export-hello-secure-ldap-certificate-tooa-pfx-file"></a><span data-ttu-id="ba70f-106">Görev 2 - hello güvenli LDAP sertifika tooa dışarı aktarma. PFX dosyası</span><span class="sxs-lookup"><span data-stu-id="ba70f-106">Task 2 - export hello secure LDAP certificate tooa .PFX file</span></span>
<span data-ttu-id="ba70f-107">Bu görev başlamadan önce bir ortak sertifika yetkilisinden hello güvenli LDAP sertifikayı aldıktan veya otomatik olarak imzalanan bir sertifika oluşturduysanız emin olun.</span><span class="sxs-lookup"><span data-stu-id="ba70f-107">Before you start this task, ensure that you have obtained hello secure LDAP certificate from a public certification authority or have created a self-signed certificate.</span></span>

<span data-ttu-id="ba70f-108">Aşağıdaki adımları hello gerçekleştirmek, tooexport hello LDAPS sertifika tooa. PFX dosyası.</span><span class="sxs-lookup"><span data-stu-id="ba70f-108">Perform hello following steps, tooexport hello LDAPS certificate tooa .PFX file.</span></span>

1. <span data-ttu-id="ba70f-109">Tuşuna hello **Başlat** düğmesi ve türü **R**. Merhaba, **çalıştırmak** iletişim, türü **mmc** tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="ba70f-109">Press hello **Start** button and type **R**. In hello **Run** dialog, type **mmc** and click **OK**.</span></span>

    ![Merhaba MMC konsolunu başlatın](./media/active-directory-domain-services-admin-guide/secure-ldap-start-run.png)
2. <span data-ttu-id="ba70f-111">Merhaba üzerinde **kullanıcı hesabı denetimi** İste'ye tıklayın **Evet** toolaunch MMC (Microsoft Yönetim Konsolu) yönetici olarak.</span><span class="sxs-lookup"><span data-stu-id="ba70f-111">On hello **User Account Control** prompt, click **YES** toolaunch MMC (Microsoft Management Console) as administrator.</span></span>
3. <span data-ttu-id="ba70f-112">Merhaba gelen **dosya** menüsünde tıklatın **Ekle/Kaldır ek bileşenini...** .</span><span class="sxs-lookup"><span data-stu-id="ba70f-112">From hello **File** menu, click **Add/Remove Snap-in...**.</span></span>

    ![Ek bileşenini tooMMC konsoluna ekleyin](./media/active-directory-domain-services-admin-guide/secure-ldap-add-snapin.png)
4. <span data-ttu-id="ba70f-114">Merhaba, **Ekle veya Kaldır ek bileşenler** iletişim, select hello **sertifikaları** ek bileşenini hello tıklatıp **Ekle >** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ba70f-114">In hello **Add or Remove Snap-ins** dialog, select hello **Certificates** snap-in, and click hello **Add >** button.</span></span>

    ![Sertifikalar ek bileşenini tooMMC konsoluna ekleyin](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin.png)
5. <span data-ttu-id="ba70f-116">Merhaba, **Sertifikalar ek bileşenini** seçin **bilgisayar hesabı** tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="ba70f-116">In hello **Certificates snap-in** wizard, select **Computer account** and click **Next**.</span></span>

    ![Sertifikalar ek bileşenini bilgisayar hesabı ekleme](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-computer-account.png)
6. <span data-ttu-id="ba70f-118">Merhaba üzerinde **Bilgisayar Seç** sayfasında **yerel bilgisayar: (Merhaba bilgisayar bu konsolu çalışıyor)** tıklatıp **son**.</span><span class="sxs-lookup"><span data-stu-id="ba70f-118">On hello **Select Computer** page, select **Local computer: (hello computer this console is running on)** and click **Finish**.</span></span>

    ![Sertifikalar ek bileşenini - select bilgisayar ekleme](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-local-computer.png)
7. <span data-ttu-id="ba70f-120">Merhaba, **Ekle veya Kaldır ek bileşenler** iletişim kutusunda, tıklatın **Tamam** tooadd hello Sertifikalar ek bileşenini tooMMC.</span><span class="sxs-lookup"><span data-stu-id="ba70f-120">In hello **Add or Remove Snap-ins** dialog, click **OK** tooadd hello certificates snap-in tooMMC.</span></span>

    ![Bitti Sertifikalar ek bileşenini tooMMC - Ekle](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin-done.png)
8. <span data-ttu-id="ba70f-122">Merhaba MMC tooexpand penceresinde **konsol kökü**.</span><span class="sxs-lookup"><span data-stu-id="ba70f-122">In hello MMC window, click tooexpand **Console Root**.</span></span> <span data-ttu-id="ba70f-123">Sertifikalar ek bileşenini hello yüklenen görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ba70f-123">You should see hello Certificates snap-in loaded.</span></span> <span data-ttu-id="ba70f-124">Tıklatın **sertifikalar (yerel bilgisayar)** tooexpand.</span><span class="sxs-lookup"><span data-stu-id="ba70f-124">Click **Certificates (Local Computer)** tooexpand.</span></span> <span data-ttu-id="ba70f-125">Tooexpand hello tıklatın **kişisel** hello tarafından izlenen düğümü **sertifikaları** düğümü.</span><span class="sxs-lookup"><span data-stu-id="ba70f-125">Click tooexpand hello **Personal** node, followed by hello **Certificates** node.</span></span>

    ![Açık kişisel sertifikalar deposuna](./media/active-directory-domain-services-admin-guide/secure-ldap-open-personal-store.png)
9. <span data-ttu-id="ba70f-127">Merhaba otomatik olarak imzalanan sertifika oluşturduğumuz görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ba70f-127">You should see hello self-signed certificate we created.</span></span> <span data-ttu-id="ba70f-128">Merhaba sertifika oluşturduğunuzda, bildirilen hello PowerShell windows hello tooensure hello parmak izi sertifikasındaki hello özelliklerini inceleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ba70f-128">You can examine hello properties of hello certificate tooensure hello thumbprint matches that reported on hello PowerShell windows when you created hello certificate.</span></span>
10. <span data-ttu-id="ba70f-129">Merhaba kendinden imzalı bir sertifika seçin ve **sağ tıklatın**.</span><span class="sxs-lookup"><span data-stu-id="ba70f-129">Select hello self-signed certificate and **right click**.</span></span> <span data-ttu-id="ba70f-130">Merhaba sağ tıklatma menüsünden seçin **tüm görevler** seçip **dışarı aktar...** .</span><span class="sxs-lookup"><span data-stu-id="ba70f-130">From hello right-click menu, select **All Tasks** and select **Export...**.</span></span>

    ![Sertifika verme](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert.png)
11. <span data-ttu-id="ba70f-132">Merhaba, **Sertifika Verme Sihirbazı**, tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="ba70f-132">In hello **Certificate Export Wizard**, click **Next**.</span></span>

    ![Dışarı aktarma Sertifika Sihirbazı](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert-wizard.png)
12. <span data-ttu-id="ba70f-134">Merhaba üzerinde **özel anahtarı dışarı** sayfasında, **Evet, hello özel anahtarı dışarı aktar**, tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="ba70f-134">On hello **Export Private Key** page, select **Yes, export hello private key**, and click **Next**.</span></span>

    ![Sertifika özel anahtarı dışarı aktar](./media/active-directory-domain-services-admin-guide/secure-ldap-export-private-key.png)

    > [!WARNING]
    > <span data-ttu-id="ba70f-136">Merhaba sertifika birlikte hello özel anahtarın dışarı aktarmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ba70f-136">You MUST export hello private key along with hello certificate.</span></span> <span data-ttu-id="ba70f-137">Merhaba hello sertifikanın özel anahtarı içermiyor bir PFX sağlarsanız, yönetilen etki alanınız için güvenli LDAP etkinleştirme başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="ba70f-137">If you provide a PFX that does not contain hello private key for hello certificate, enabling secure LDAP for your managed domain fails.</span></span>
    >
    >
13. <span data-ttu-id="ba70f-138">Merhaba üzerinde **dışarı aktarma dosyası biçimi** sayfasında, **kişisel bilgi alış verişi - PKCS #12 (. PFX)** hello dosya biçimi hello için sertifika dışarı gibi.</span><span class="sxs-lookup"><span data-stu-id="ba70f-138">On hello **Export File Format** page, select **Personal Information Exchange - PKCS #12 (.PFX)** as hello file format for hello exported certificate.</span></span>

    ![Sertifika dosya biçimini Dışarı Aktar](./media/active-directory-domain-services-admin-guide/secure-ldap-export-to-pfx.png)

    > [!NOTE]
    > <span data-ttu-id="ba70f-140">Yalnızca hello. PFX dosyasının biçimi desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="ba70f-140">Only hello .PFX file format is supported.</span></span> <span data-ttu-id="ba70f-141">Merhaba sertifika toohello vermeyin. CER dosya biçimi.</span><span class="sxs-lookup"><span data-stu-id="ba70f-141">Do not export hello certificate toohello .CER file format.</span></span>
    >
    >
14. <span data-ttu-id="ba70f-142">Merhaba üzerinde **güvenlik** sayfası, select hello **parola** seçeneği ve parola tooprotect hello yazın. PFX dosyası.</span><span class="sxs-lookup"><span data-stu-id="ba70f-142">On hello **Security** page, select hello **Password** option and type in a password tooprotect hello .PFX file.</span></span> <span data-ttu-id="ba70f-143">Merhaba sonraki görev gerekecek beri bu parolayı unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ba70f-143">Remember this password since it will be needed in hello next task.</span></span> <span data-ttu-id="ba70f-144">Tıklatın **sonraki** tooproceed.</span><span class="sxs-lookup"><span data-stu-id="ba70f-144">Click **Next** tooproceed.</span></span>

    ![<span data-ttu-id="ba70f-145">Sertifika dışarı aktarma için parola</span><span class="sxs-lookup"><span data-stu-id="ba70f-145">Password for certificate export</span></span> ](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-password.png)

    > [!NOTE]
    > <span data-ttu-id="ba70f-146">Bu parolayı not edin.</span><span class="sxs-lookup"><span data-stu-id="ba70f-146">Make a note of this password.</span></span> <span data-ttu-id="ba70f-147">Bu yönetilen etki alanı için güvenli LDAP etkinleştirirken gereken [görev 3 - güvenli LDAP hello yönetilen etki alanı için etkinleştirme](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span><span class="sxs-lookup"><span data-stu-id="ba70f-147">You need it while enabling secure LDAP for this managed domain in [Task 3 - enable secure LDAP for hello managed domain](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span></span>
    >
    >
15. <span data-ttu-id="ba70f-148">Merhaba üzerinde **dosya tooExport** sayfasında, hello dosya adı ve olduğu gibi tooexport hello sertifika konumu belirtin.</span><span class="sxs-lookup"><span data-stu-id="ba70f-148">On hello **File tooExport** page, specify hello file name and location where you'd like tooexport hello certificate.</span></span>

    ![Sertifika dışa aktarma yolu](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-path.png)
16. <span data-ttu-id="ba70f-150">Sayfasında, aşağıdaki Hello üzerinde tıklatın **son** tooexport hello tooa sertifika.pfx dosyası.</span><span class="sxs-lookup"><span data-stu-id="ba70f-150">On hello following page, click **Finish** tooexport hello certificate tooa PFX file.</span></span> <span data-ttu-id="ba70f-151">Merhaba sertifika verildiğinde onay iletişim kutusu görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ba70f-151">You should see confirmation dialog when hello certificate has been exported.</span></span>

    ![Bitti sertifikasını dışarı aktarma](./media/active-directory-domain-services-admin-guide/secure-ldap-exported-as-pfx.png)


## <a name="next-step"></a><span data-ttu-id="ba70f-153">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="ba70f-153">Next step</span></span>
[<span data-ttu-id="ba70f-154">Görev 3 - güvenli LDAP hello yönetilen etki alanı için etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="ba70f-154">Task 3 - enable secure LDAP for hello managed domain</span></span>](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)
