---
title: SAP S/4HANA veya BW/4HANA Azure VM'de aaaDeploy | Microsoft Docs
description: "SAP S/4HANA veya BW/4HANA Azure VM'de dağıtın"
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 44bbd2b6-a376-4b5c-b824-e76917117fa9
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 09/15/2016
ms.author: hermannd
ms.openlocfilehash: 7e57f7daa7667b7c7dbcb86f6892a54e4295b74c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-sap-s4hana-or-bw4hana-on-azure"></a><span data-ttu-id="2e583-103">SAP S/4HANA veya BW/4HANA azure'da dağıtmak</span><span class="sxs-lookup"><span data-stu-id="2e583-103">Deploy SAP S/4HANA or BW/4HANA on Azure</span></span>
<span data-ttu-id="2e583-104">Bu makalede nasıl kullanarak toodeploy S/4HANA azure'da hello SAP bulut Gereci kitaplığı (SAP CAL) 3.0 açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="2e583-104">This article describes how toodeploy S/4HANA on Azure by using hello SAP Cloud Appliance Library (SAP CAL) 3.0.</span></span> <span data-ttu-id="2e583-105">toodeploy hello BW/4HANA gibi diğer SAP HANA tabanlı çözümleri uygulayın aynı adımları.</span><span class="sxs-lookup"><span data-stu-id="2e583-105">toodeploy other SAP HANA-based solutions, such as BW/4HANA, follow hello same steps.</span></span>

> [!NOTE]
<span data-ttu-id="2e583-106">Merhaba SAP CAL hakkında daha fazla bilgi için toohello Git [SAP bulut Gereci Kitaplığı](https://cal.sap.com/) Web sitesi.</span><span class="sxs-lookup"><span data-stu-id="2e583-106">For more information about hello SAP CAL, go toohello [SAP Cloud Appliance Library](https://cal.sap.com/) website.</span></span> <span data-ttu-id="2e583-107">SAP de sahip bir blog hello hakkında [SAP bulut Gereci kitaplığı 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span><span class="sxs-lookup"><span data-stu-id="2e583-107">SAP also has a blog about hello [SAP Cloud Appliance Library 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span></span>

> [!NOTE]
<span data-ttu-id="2e583-108">29 Mayıs 2017 hello Azure Resource Manager dağıtım modeli kullanabileceğiniz gibi ayrıca toohello daha az tercih edilen Klasik dağıtım modeli toodeploy hello SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="2e583-108">As of May 29, 2017, you can use hello Azure Resource Manager deployment model in addition toohello less-preferred classic deployment model toodeploy hello SAP CAL.</span></span> <span data-ttu-id="2e583-109">Merhaba yeni Resource Manager dağıtım modeli kullanır ve hello Klasik dağıtım modeli göz ardı öneririz.</span><span class="sxs-lookup"><span data-stu-id="2e583-109">We recommend that you use hello new Resource Manager deployment model and disregard hello classic deployment model.</span></span>

## <a name="step-by-step-process-toodeploy-hello-solution"></a><span data-ttu-id="2e583-110">Adım adım işlemi toodeploy hello çözümü</span><span class="sxs-lookup"><span data-stu-id="2e583-110">Step-by-step process toodeploy hello solution</span></span>

<span data-ttu-id="2e583-111">Aşağıdaki ekran görüntüleri bir dizi hello nasıl kullanarak toodeploy S/4HANA azure'da hello SAP CAL gösterir.</span><span class="sxs-lookup"><span data-stu-id="2e583-111">hello following sequence of screenshots shows you how toodeploy S/4HANA on Azure by using hello SAP CAL.</span></span> <span data-ttu-id="2e583-112">Merhaba işlemin çalıştığını hello BW/4HANA gibi diğer çözümleri için aynı şekilde.</span><span class="sxs-lookup"><span data-stu-id="2e583-112">hello process works hello same way for other solutions, such as BW/4HANA.</span></span>

<span data-ttu-id="2e583-113">Merhaba **çözümleri** sayfası gösterir hello bazıları SAP CAL HANA tabanlı çözümler kullanılabilir Azure üzerinde.</span><span class="sxs-lookup"><span data-stu-id="2e583-113">hello **Solutions** page shows some of hello SAP CAL HANA-based solutions available on Azure.</span></span> <span data-ttu-id="2e583-114">**SAP S/4HANA 1610 FPS01, Fully-Activated Gereci** hello Orta sırada:</span><span class="sxs-lookup"><span data-stu-id="2e583-114">**SAP S/4HANA 1610 FPS01, Fully-Activated Appliance** is in hello middle row:</span></span>

![SAP CAL çözümleri](./media/cal-s4h/s4h-pic-1c.png)

### <a name="create-an-account-in-hello-sap-cal"></a><span data-ttu-id="2e583-116">Merhaba SAP CAL bir hesap oluşturun</span><span class="sxs-lookup"><span data-stu-id="2e583-116">Create an account in hello SAP CAL</span></span>
1. <span data-ttu-id="2e583-117">hello için SAP CAL toohello toosign ilk kez SAP S kullanıcı veya SAP ile kayıtlı başka bir kullanıcı kullanın.</span><span class="sxs-lookup"><span data-stu-id="2e583-117">toosign in toohello SAP CAL for hello first time, use your SAP S-User or other user registered with SAP.</span></span> <span data-ttu-id="2e583-118">Ardından azure'da hello SAP CAL toodeploy cihazları tarafından kullanılan bir SAP CAL hesap tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="2e583-118">Then define an SAP CAL account that is used by hello SAP CAL toodeploy appliances on Azure.</span></span> <span data-ttu-id="2e583-119">Merhaba hesap tanımında şunları yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="2e583-119">In hello account definition, you need to:</span></span>

    <span data-ttu-id="2e583-120">a.</span><span class="sxs-lookup"><span data-stu-id="2e583-120">a.</span></span> <span data-ttu-id="2e583-121">(Resource Manager veya Klasik) azure'da Hello dağıtım modelini seçin.</span><span class="sxs-lookup"><span data-stu-id="2e583-121">Select hello deployment model on Azure (Resource Manager or classic).</span></span>

    <span data-ttu-id="2e583-122">b.</span><span class="sxs-lookup"><span data-stu-id="2e583-122">b.</span></span> <span data-ttu-id="2e583-123">Azure aboneliğiniz girin.</span><span class="sxs-lookup"><span data-stu-id="2e583-123">Enter your Azure subscription.</span></span> <span data-ttu-id="2e583-124">Bir SAP CAL hesabı yalnızca tooone abonelik atanabilir.</span><span class="sxs-lookup"><span data-stu-id="2e583-124">An SAP CAL account can be assigned tooone subscription only.</span></span> <span data-ttu-id="2e583-125">Birden fazla abonelik ihtiyacınız varsa, başka bir SAP CAL hesabı toocreate gerekir.</span><span class="sxs-lookup"><span data-stu-id="2e583-125">If you need more than one subscription, you need toocreate another SAP CAL account.</span></span>

    <span data-ttu-id="2e583-126">c.</span><span class="sxs-lookup"><span data-stu-id="2e583-126">c.</span></span> <span data-ttu-id="2e583-127">Merhaba SAP CAL izni toodeploy Azure aboneliğinize verin.</span><span class="sxs-lookup"><span data-stu-id="2e583-127">Give hello SAP CAL permission toodeploy into your Azure subscription.</span></span>

    > [!NOTE]
    <span data-ttu-id="2e583-128">Merhaba sonraki adımlar nasıl toocreate bir SAP CAL hesap Resource Manager dağıtımları için gösterir.</span><span class="sxs-lookup"><span data-stu-id="2e583-128">hello next steps show how toocreate an SAP CAL account for Resource Manager deployments.</span></span> <span data-ttu-id="2e583-129">Bağlantılı toohello Klasik dağıtım modeli, SAP CAL hesabınız zaten varsa, *gerek* toofollow bu adımları toocreate yeni bir SAP CAL hesabı.</span><span class="sxs-lookup"><span data-stu-id="2e583-129">If you already have an SAP CAL account that is linked toohello classic deployment model, you *need* toofollow these steps toocreate a new SAP CAL account.</span></span> <span data-ttu-id="2e583-130">Merhaba yeni SAP CAL hesabı hello Resource Manager modelinde toodeploy gerekir.</span><span class="sxs-lookup"><span data-stu-id="2e583-130">hello new SAP CAL account needs toodeploy in hello Resource Manager model.</span></span>

2. <span data-ttu-id="2e583-131">Yeni bir SAP CAL hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2e583-131">Create a new SAP CAL account.</span></span> <span data-ttu-id="2e583-132">Merhaba **hesapları** sayfa, Azure için üç seçeneğiniz gösterir:</span><span class="sxs-lookup"><span data-stu-id="2e583-132">hello **Accounts** page shows three choices for Azure:</span></span> 

    <span data-ttu-id="2e583-133">a.</span><span class="sxs-lookup"><span data-stu-id="2e583-133">a.</span></span> <span data-ttu-id="2e583-134">**Microsoft Azure (Klasik)** hello Klasik dağıtım modeli ve artık tercih edilir.</span><span class="sxs-lookup"><span data-stu-id="2e583-134">**Microsoft Azure (classic)** is hello classic deployment model and is no longer preferred.</span></span>

    <span data-ttu-id="2e583-135">b.</span><span class="sxs-lookup"><span data-stu-id="2e583-135">b.</span></span> <span data-ttu-id="2e583-136">**Microsoft Azure** hello yeni Resource Manager dağıtım modeli.</span><span class="sxs-lookup"><span data-stu-id="2e583-136">**Microsoft Azure** is hello new Resource Manager deployment model.</span></span>

    <span data-ttu-id="2e583-137">c.</span><span class="sxs-lookup"><span data-stu-id="2e583-137">c.</span></span> <span data-ttu-id="2e583-138">**Windows Azure 21Vianet tarafından işletilen** hello Klasik dağıtım modelini kullanan Çin'de bir seçenektir.</span><span class="sxs-lookup"><span data-stu-id="2e583-138">**Windows Azure operated by 21Vianet** is an option in China that uses hello classic deployment model.</span></span>

    <span data-ttu-id="2e583-139">Merhaba Resource Manager modelinde toodeploy seçin **Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="2e583-139">toodeploy in hello Resource Manager model, select **Microsoft Azure**.</span></span>

    ![SAP CAL hesap ayrıntıları](./media/cal-s4h/s4h-pic-2a.png)

3. <span data-ttu-id="2e583-141">Hello Azure girin **abonelik kimliği** hello Azure portalı üzerinde bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="2e583-141">Enter hello Azure **Subscription ID** that can be found on hello Azure portal.</span></span>

   ![SAP CAL hesapları](./media/cal-s4h/s4h-pic3c.png)

4. <span data-ttu-id="2e583-143">tanımladığınız tooauthorize hello SAP CAL toodeploy hello Azure aboneliği içine, tıklatın **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="2e583-143">tooauthorize hello SAP CAL toodeploy into hello Azure subscription you defined, click **Authorize**.</span></span> <span data-ttu-id="2e583-144">Sayfa aşağıdaki hello hello tarayıcı sekmesinde görünür:</span><span class="sxs-lookup"><span data-stu-id="2e583-144">hello following page appears in hello browser tab:</span></span>

   ![Oturum açma Internet Explorer bulut Hizmetleri](./media/cal-s4h/s4h-pic4c.png)

5. <span data-ttu-id="2e583-146">Birden fazla kullanıcı listeleniyorsa, hello Microsoft bağlantılı toobe hello Abonelikteki hello Seçtiğiniz Azure aboneliği olan bir hesap seçin.</span><span class="sxs-lookup"><span data-stu-id="2e583-146">If more than one user is listed, choose hello Microsoft account that is linked toobe hello coadministrator of hello Azure subscription you selected.</span></span> <span data-ttu-id="2e583-147">Sayfa aşağıdaki hello hello tarayıcı sekmesinde görünür:</span><span class="sxs-lookup"><span data-stu-id="2e583-147">hello following page appears in hello browser tab:</span></span>

   ![Internet Explorer bulut Hizmetleri onayı](./media/cal-s4h/s4h-pic5a.png)

6. <span data-ttu-id="2e583-149">Tıklatın **kabul**.</span><span class="sxs-lookup"><span data-stu-id="2e583-149">Click **Accept**.</span></span> <span data-ttu-id="2e583-150">Merhaba Yetkilendirme başarılı olursa yeniden hello SAP CAL hesabı tanımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="2e583-150">If hello authorization is successful, hello SAP CAL account definition displays again.</span></span> <span data-ttu-id="2e583-151">Kısa bir süre sonra bir ileti hello yetkilendirme işleminin başarılı olduğunu onaylar.</span><span class="sxs-lookup"><span data-stu-id="2e583-151">After a short time, a message confirms that hello authorization process was successful.</span></span>

7. <span data-ttu-id="2e583-152">Yeni oluşturulan SAP CAL hesabı tooyour kullanıcı tooassign Merhaba, girin, **kullanıcı kimliği** hello hello sağ taraftaki metin kutusu ve tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="2e583-152">tooassign hello newly created SAP CAL account tooyour user, enter your **User ID** in hello text box on hello right and click **Add**.</span></span>

   ![Hesap toouser ilişkilendirme](./media/cal-s4h/s4h-pic8a.png)

8. <span data-ttu-id="2e583-154">Merhaba kullanıcı toohello SAP CAL toosign kullanmak hesabınızla tooassociate tıklatın **gözden**.</span><span class="sxs-lookup"><span data-stu-id="2e583-154">tooassociate your account with hello user that you use toosign in toohello SAP CAL, click **Review**.</span></span> 
 
9. <span data-ttu-id="2e583-155">Kullanıcı ve yeni oluşturulan hello SAP CAL hesabı arasında toocreate hello ilişkilendirme tıklayın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="2e583-155">toocreate hello association between your user and hello newly created SAP CAL account, click **Create**.</span></span>

   ![Kullanıcı tooSAP CAL hesabı ilişkisi](./media/cal-s4h/s4h-pic9b.png)

<span data-ttu-id="2e583-157">Olduğu bir SAP CAL hesabı başarıyla oluşturuldu:</span><span class="sxs-lookup"><span data-stu-id="2e583-157">You successfully created an SAP CAL account that is able to:</span></span>

- <span data-ttu-id="2e583-158">Merhaba Resource Manager dağıtım modeli kullanır.</span><span class="sxs-lookup"><span data-stu-id="2e583-158">Use hello Resource Manager deployment model.</span></span>
- <span data-ttu-id="2e583-159">SAP sistemleri Azure aboneliğinize dağıtın.</span><span class="sxs-lookup"><span data-stu-id="2e583-159">Deploy SAP systems into your Azure subscription.</span></span>

<span data-ttu-id="2e583-160">Şimdi kullanıcı aboneliğinizde Azure içine toodeploy S/4HANA başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2e583-160">Now you can start toodeploy S/4HANA into your user subscription in Azure.</span></span>

> [!NOTE]
<span data-ttu-id="2e583-161">Devam etmeden önce Azure H-serisi VM'ler için Azure çekirdek kotaları yüklü olup olmadığını belirler.</span><span class="sxs-lookup"><span data-stu-id="2e583-161">Before you continue, determine whether you have Azure core quotas for Azure H-Series VMs.</span></span> <span data-ttu-id="2e583-162">Merhaba şu anda, H-serisi VM'ler Azure toodeploy hello SAP CAL kullanan bazı hello SAP HANA tabanlı çözümler.</span><span class="sxs-lookup"><span data-stu-id="2e583-162">At hello moment, hello SAP CAL uses H-Series VMs of Azure toodeploy some of hello SAP HANA-based solutions.</span></span> <span data-ttu-id="2e583-163">Azure aboneliğiniz H-seri için hiçbir H-serisi çekirdek kota sahip olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="2e583-163">Your Azure subscription might not have any H-Series core quotas for H-Series.</span></span> <span data-ttu-id="2e583-164">Bu durumda, toocontact Azure destek tooget en az 16 H-serisi çekirdek kotası gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="2e583-164">If so, you might need toocontact Azure support tooget a quota of at least 16 H-Series cores.</span></span>

> [!NOTE]
<span data-ttu-id="2e583-165">Bir çözümde azure'da hello SAP CAL dağıttığınızda, yalnızca bir Azure bölgesi seçebilirsiniz bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2e583-165">When you deploy a solution on Azure in hello SAP CAL, you might find that you can choose only one Azure region.</span></span> <span data-ttu-id="2e583-166">toodeploy Azure bölgeleri hello dışında bir SAP CAL hello tarafından önerilen, toopurchase SAP CAL abonelikten gerekir.</span><span class="sxs-lookup"><span data-stu-id="2e583-166">toodeploy into Azure regions other than hello one suggested by hello SAP CAL, you need toopurchase a CAL subscription from SAP.</span></span> <span data-ttu-id="2e583-167">Azure bölgeleri hello Başlangıçta önerilen olanlar dışındaki CAL hesap etkinleştirildi toodeliver tooopen SAP toohave içeren bir ileti da gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="2e583-167">You also might need tooopen a message with SAP toohave your CAL account enabled toodeliver into Azure regions other than hello ones initially suggested.</span></span>

### <a name="deploy-a-solution"></a><span data-ttu-id="2e583-168">Bir çözüm dağıtma</span><span class="sxs-lookup"><span data-stu-id="2e583-168">Deploy a solution</span></span>

<span data-ttu-id="2e583-169">Şimdi hello bir çözüm dağıtma **çözümleri** hello SAP CAL sayfası.</span><span class="sxs-lookup"><span data-stu-id="2e583-169">Let's deploy a solution from hello **Solutions** page of hello SAP CAL.</span></span> <span data-ttu-id="2e583-170">Merhaba SAP CAL iki sıraları toodeploy sahiptir:</span><span class="sxs-lookup"><span data-stu-id="2e583-170">hello SAP CAL has two sequences toodeploy:</span></span>

- <span data-ttu-id="2e583-171">Dağıtılan bir sayfa toodefine hello sistem toobe kullanan bir temel sıralı</span><span class="sxs-lookup"><span data-stu-id="2e583-171">A basic sequence that uses one page toodefine hello system toobe deployed</span></span>
- <span data-ttu-id="2e583-172">Gelişmiş dizisi VM boyutlarını belirli seçenekler sunar</span><span class="sxs-lookup"><span data-stu-id="2e583-172">An advanced sequence that gives you certain choices on VM sizes</span></span> 

<span data-ttu-id="2e583-173">Biz hello temel yolu buraya toodeployment göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="2e583-173">We demonstrate hello basic path toodeployment here.</span></span>

1. <span data-ttu-id="2e583-174">Merhaba üzerinde **hesap ayrıntıları** sayfasında gerekir:</span><span class="sxs-lookup"><span data-stu-id="2e583-174">On hello **Account Details** page, you need to:</span></span>

    <span data-ttu-id="2e583-175">a.</span><span class="sxs-lookup"><span data-stu-id="2e583-175">a.</span></span> <span data-ttu-id="2e583-176">SAP CAL hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="2e583-176">Select an SAP CAL account.</span></span> <span data-ttu-id="2e583-177">(Merhaba Resource Manager dağıtım modeli ile ilişkili toodeploy olan bir hesap kullanın.)</span><span class="sxs-lookup"><span data-stu-id="2e583-177">(Use an account that is associated toodeploy with hello Resource Manager deployment model.)</span></span>

    <span data-ttu-id="2e583-178">b.</span><span class="sxs-lookup"><span data-stu-id="2e583-178">b.</span></span> <span data-ttu-id="2e583-179">Bir örnek girmek **adı**.</span><span class="sxs-lookup"><span data-stu-id="2e583-179">Enter an instance **Name**.</span></span>

    <span data-ttu-id="2e583-180">c.</span><span class="sxs-lookup"><span data-stu-id="2e583-180">c.</span></span> <span data-ttu-id="2e583-181">Bir Azure seçin **bölge**.</span><span class="sxs-lookup"><span data-stu-id="2e583-181">Select an Azure **Region**.</span></span> <span data-ttu-id="2e583-182">Merhaba SAP CAL bir bölge önerir.</span><span class="sxs-lookup"><span data-stu-id="2e583-182">hello SAP CAL suggests a region.</span></span> <span data-ttu-id="2e583-183">Başka bir Azure bölgesi gerekir ve bir SAP CAL aboneliğiniz yoksa, SAP tooorder bir CAL abonelikle gerekir.</span><span class="sxs-lookup"><span data-stu-id="2e583-183">If you need another Azure region and you don't have an SAP CAL subscription, you need tooorder a CAL subscription with SAP.</span></span>

    <span data-ttu-id="2e583-184">d.</span><span class="sxs-lookup"><span data-stu-id="2e583-184">d.</span></span> <span data-ttu-id="2e583-185">Asıl girin **parola** hello çözüm sekiz veya dokuz karakter.</span><span class="sxs-lookup"><span data-stu-id="2e583-185">Enter a master **Password** for hello solution of eight or nine characters.</span></span> <span data-ttu-id="2e583-186">Merhaba parola hello farklı bileşenleri hello Yöneticiler için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2e583-186">hello password is used for hello administrators of hello different components.</span></span>

   ![SAP CAL Basic modu: Örnek oluşturma](./media/cal-s4h/s4h-pic10a.png)

2. <span data-ttu-id="2e583-188">Tıklatın **oluşturma**, görüntülenen hello ileti kutusunda tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="2e583-188">Click **Create**, and in hello message box that appears, click **OK**.</span></span>

   ![SAP CAL VM boyutları desteklenir](./media/cal-s4h/s4h-pic10b.png)

3. <span data-ttu-id="2e583-190">Merhaba, **özel anahtar** iletişim kutusu, tıklatın **deposu** toostore hello özel anahtar hello SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="2e583-190">In hello **Private Key** dialog box, click **Store** toostore hello private key in hello SAP CAL.</span></span> <span data-ttu-id="2e583-191">Merhaba özel anahtar için toouse parola koruması **karşıdan**.</span><span class="sxs-lookup"><span data-stu-id="2e583-191">toouse password protection for hello private key, click **Download**.</span></span> 

   ![SAP CAL özel anahtar](./media/cal-s4h/s4h-pic10c.png)

4. <span data-ttu-id="2e583-193">Okuma hello SAP CAL **uyarı** tıklayın ve ileti **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="2e583-193">Read hello SAP CAL **Warning** message, and click **OK**.</span></span>

   ![SAP CAL uyarı](./media/cal-s4h/s4h-pic10d.png)

    <span data-ttu-id="2e583-195">Şimdi hello dağıtım gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="2e583-195">Now hello deployment takes place.</span></span> <span data-ttu-id="2e583-196">Bir süre sonra hello boyutu ve karmaşıklığı (hello) SAP CAL tahmini sağlar, hello çözümün bağlı olarak hello durumu etkin ve kullanım için hazır olarak gösterilir.</span><span class="sxs-lookup"><span data-stu-id="2e583-196">After some time, depending on hello size and complexity of hello solution (hello SAP CAL provides an estimate), hello status is shown as active and ready for use.</span></span>

5. <span data-ttu-id="2e583-197">toofind hello sanal makineler ile toplanan diğer ilişkili kaynakları bir kaynak grubunda Merhaba, toohello Azure portalına gidin:</span><span class="sxs-lookup"><span data-stu-id="2e583-197">toofind hello virtual machines collected with hello other associated resources in one resource group, go toohello Azure portal:</span></span> 

   ![Dağıtılan Hello yeni portalında SAP CAL nesneler](./media/cal-s4h/sapcaldeplyment_portalview.png)

6. <span data-ttu-id="2e583-199">Merhaba SAP CAL portalında olarak hello durumu görünür **etkin**.</span><span class="sxs-lookup"><span data-stu-id="2e583-199">On hello SAP CAL portal, hello status appears as **Active**.</span></span> <span data-ttu-id="2e583-200">tooconnect toohello çözüm tıklatın **Bağlan**.</span><span class="sxs-lookup"><span data-stu-id="2e583-200">tooconnect toohello solution, click **Connect**.</span></span> <span data-ttu-id="2e583-201">Farklı seçenekler tooconnect toohello farklı bileşenleri bu çözüm içinde dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="2e583-201">Different options tooconnect toohello different components are deployed within this solution.</span></span>

   ![SAP CAL örnekleri](./media/cal-s4h/active_solution.png)

7. <span data-ttu-id="2e583-203">Merhaba seçenekleri tooconnect dağıtılan toohello sistemlerinden birini kullanmadan önce tıklatın **Başlarken Kılavuzu**.</span><span class="sxs-lookup"><span data-stu-id="2e583-203">Before you can use one of hello options tooconnect toohello deployed systems, click **Getting Started Guide**.</span></span> 

   ![Toohello örneğine bağlanma](./media/cal-s4h/connect_to_solution.png)

    <span data-ttu-id="2e583-205">Merhaba belgelerine adları kullanıcıların her hello bağlantı yöntemleri için hello.</span><span class="sxs-lookup"><span data-stu-id="2e583-205">hello documentation names hello users for each of hello connectivity methods.</span></span> <span data-ttu-id="2e583-206">Merhaba parolaları olan kullanıcılar için tanımladığınız toohello ana parola hello hello dağıtım işleminin başında ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="2e583-206">hello passwords for those users are set toohello master password you defined at hello beginning of hello deployment process.</span></span> <span data-ttu-id="2e583-207">Merhaba belgelerinde kullanabileceğiniz parolalarını ile daha işlevsel diğer kullanıcılar listelenir toohello toosign dağıtılan sistem.</span><span class="sxs-lookup"><span data-stu-id="2e583-207">In hello documentation, other more functional users are listed with their passwords, which you can use toosign in toohello deployed system.</span></span> 

    <span data-ttu-id="2e583-208">Merhaba Windows Uzak Masaüstü makinede hello önceden yüklenmiş olarak SAP GUI kullanırsanız, örneğin, hello S/4 sistem şuna benzeyebilir:</span><span class="sxs-lookup"><span data-stu-id="2e583-208">For example, if you use hello SAP GUI that's preinstalled on hello Windows Remote Desktop machine, hello S/4 system might look like this:</span></span>

   ![Merhaba SM50 SAP GUI önceden yüklenmiş](./media/cal-s4h/gui_sm50.png)

    <span data-ttu-id="2e583-210">Veya hello DBACockpit kullanırsanız, hello örnek şuna benzeyebilir:</span><span class="sxs-lookup"><span data-stu-id="2e583-210">Or if you use hello DBACockpit, hello instance might look like this:</span></span>

   ![Merhaba DBACockpit SAP GUI SM50](./media/cal-s4h/dbacockpit.png)

<span data-ttu-id="2e583-212">Birkaç saat içinde sağlıklı bir SAP S/4 Gereci Azure'da dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="2e583-212">Within a few hours, a healthy SAP S/4 appliance is deployed in Azure.</span></span>

<span data-ttu-id="2e583-213">Bir SAP CAL abonelik satın aldıysanız, SAP dağıtımlarınızı hello SAP CAL aracılığıyla Azure üzerinde tam olarak destekler.</span><span class="sxs-lookup"><span data-stu-id="2e583-213">If you bought an SAP CAL subscription, SAP fully supports deployments through hello SAP CAL on Azure.</span></span> <span data-ttu-id="2e583-214">Merhaba destek BC VCM CAL sırasıdır.</span><span class="sxs-lookup"><span data-stu-id="2e583-214">hello support queue is BC-VCM-CAL.</span></span>







