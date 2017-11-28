---
title: "aaaDeploy SAP ERP 6.0 Azure üzerinde IDE EHP7 SP3 SAP | Microsoft Docs"
description: "Azure üzerinde SAP ERP 6.0 için SAP IDE EHP7 SP3 dağıtma"
services: virtual-machines-windows
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 626c1523-1026-478f-bd8a-22c83b869231
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 09/16/2016
ms.author: hermannd
ms.openlocfilehash: 26d88c7b48a91d35602464c4f89ca7a30502c4b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-sap-ides-ehp7-sp3-for-sap-erp-60-on-azure"></a><span data-ttu-id="3abc0-103">Azure üzerinde SAP ERP 6.0 için SAP IDE EHP7 SP3 dağıtma</span><span class="sxs-lookup"><span data-stu-id="3abc0-103">Deploy SAP IDES EHP7 SP3 for SAP ERP 6.0 on Azure</span></span>
<span data-ttu-id="3abc0-104">Bu makalede nasıl toodeploy bir SAP hello Windows işletim sistemi ve SQL Server ile SAP bulut Gereci kitaplığı (SAP CAL) 3.0 hello Azure üzerinde çalışan IDE sistem.</span><span class="sxs-lookup"><span data-stu-id="3abc0-104">This article describes how toodeploy an SAP IDES system running with SQL Server and hello Windows operating system on Azure via hello SAP Cloud Appliance Library (SAP CAL) 3.0.</span></span> <span data-ttu-id="3abc0-105">Merhaba ekran görüntüleri hello işlem adım adım göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="3abc0-105">hello screenshots show hello step-by-step process.</span></span> <span data-ttu-id="3abc0-106">farklı bir çözüme toodeploy izleyin hello aynı adımları.</span><span class="sxs-lookup"><span data-stu-id="3abc0-106">toodeploy a different solution, follow hello same steps.</span></span>

<span data-ttu-id="3abc0-107">Merhaba SAP CAL, Git toohello ile toostart [SAP bulut Gereci Kitaplığı](https://cal.sap.com/) Web sitesi.</span><span class="sxs-lookup"><span data-stu-id="3abc0-107">toostart with hello SAP CAL, go toohello [SAP Cloud Appliance Library](https://cal.sap.com/) website.</span></span> <span data-ttu-id="3abc0-108">SAP de sahip bir blog hello hakkında yeni [SAP bulut Gereci kitaplığı 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span><span class="sxs-lookup"><span data-stu-id="3abc0-108">SAP also has a blog about hello new [SAP Cloud Appliance Library 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span></span> 

> [!NOTE]
<span data-ttu-id="3abc0-109">29 Mayıs 2017 hello Azure Resource Manager dağıtım modeli kullanabileceğiniz gibi ayrıca toohello daha az tercih edilen Klasik dağıtım modeli toodeploy hello SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="3abc0-109">As of May 29, 2017, you can use hello Azure Resource Manager deployment model in addition toohello less-preferred classic deployment model toodeploy hello SAP CAL.</span></span> <span data-ttu-id="3abc0-110">Merhaba yeni Resource Manager dağıtım modeli kullanır ve hello Klasik dağıtım modeli göz ardı öneririz.</span><span class="sxs-lookup"><span data-stu-id="3abc0-110">We recommend that you use hello new Resource Manager deployment model and disregard hello classic deployment model.</span></span>

<span data-ttu-id="3abc0-111">Merhaba Klasik modeli kullanan bir SAP CAL hesabı zaten oluşturduysanız *başka bir SAP CAL hesabı toocreate gerek*.</span><span class="sxs-lookup"><span data-stu-id="3abc0-111">If you already created an SAP CAL account that uses hello classic model, *you need toocreate another SAP CAL account*.</span></span> <span data-ttu-id="3abc0-112">Bu hesap tooexclusively olmalıdır hello Resource Manager modelini kullanarak Azure'a dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3abc0-112">This account needs tooexclusively deploy into Azure by using hello Resource Manager model.</span></span>

<span data-ttu-id="3abc0-113">Toohello SAP CAL oturumu sonra hello ilk sayfa genellikle toohello sizi **çözümleri** sayfası.</span><span class="sxs-lookup"><span data-stu-id="3abc0-113">After you sign in toohello SAP CAL, hello first page usually leads you toohello **Solutions** page.</span></span> <span data-ttu-id="3abc0-114">tooscroll bir bit, istediğiniz toofind hello çözüm gerekebilecek şekilde hello SAP CAL üzerinde sunulan hello çözümleri sürekli olarak artmaktadır.</span><span class="sxs-lookup"><span data-stu-id="3abc0-114">hello solutions offered on hello SAP CAL are steadily increasing, so you might need tooscroll quite a bit toofind hello solution you want.</span></span> <span data-ttu-id="3abc0-115">özel olarak Azure üzerinde kullanılabilir vurgulanmış hello SAP IDE Windows tabanlı çözüm hello dağıtım süreci gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="3abc0-115">hello highlighted Windows-based SAP IDES solution that is available exclusively on Azure demonstrates hello deployment process:</span></span>

![SAP CAL çözümleri](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic1.jpg)

### <a name="create-an-account-in-hello-sap-cal"></a><span data-ttu-id="3abc0-117">Merhaba SAP CAL bir hesap oluşturun</span><span class="sxs-lookup"><span data-stu-id="3abc0-117">Create an account in hello SAP CAL</span></span>
1. <span data-ttu-id="3abc0-118">hello için SAP CAL toohello toosign ilk kez SAP S kullanıcı veya SAP ile kayıtlı başka bir kullanıcı kullanın.</span><span class="sxs-lookup"><span data-stu-id="3abc0-118">toosign in toohello SAP CAL for hello first time, use your SAP S-User or other user registered with SAP.</span></span> <span data-ttu-id="3abc0-119">Ardından azure'da hello SAP CAL toodeploy cihazları tarafından kullanılan bir SAP CAL hesap tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="3abc0-119">Then define an SAP CAL account that is used by hello SAP CAL toodeploy appliances on Azure.</span></span> <span data-ttu-id="3abc0-120">Merhaba hesap tanımında şunları yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="3abc0-120">In hello account definition, you need to:</span></span>

    <span data-ttu-id="3abc0-121">a.</span><span class="sxs-lookup"><span data-stu-id="3abc0-121">a.</span></span> <span data-ttu-id="3abc0-122">(Resource Manager veya Klasik) azure'da Hello dağıtım modelini seçin.</span><span class="sxs-lookup"><span data-stu-id="3abc0-122">Select hello deployment model on Azure (Resource Manager or classic).</span></span>

    <span data-ttu-id="3abc0-123">b.</span><span class="sxs-lookup"><span data-stu-id="3abc0-123">b.</span></span> <span data-ttu-id="3abc0-124">Azure aboneliğiniz girin.</span><span class="sxs-lookup"><span data-stu-id="3abc0-124">Enter your Azure subscription.</span></span> <span data-ttu-id="3abc0-125">Bir SAP CAL hesabı yalnızca tooone abonelik atanabilir.</span><span class="sxs-lookup"><span data-stu-id="3abc0-125">An SAP CAL account can be assigned tooone subscription only.</span></span> <span data-ttu-id="3abc0-126">Birden fazla abonelik ihtiyacınız varsa, başka bir SAP CAL hesabı toocreate gerekir.</span><span class="sxs-lookup"><span data-stu-id="3abc0-126">If you need more than one subscription, you need toocreate another SAP CAL account.</span></span>
    
    <span data-ttu-id="3abc0-127">c.</span><span class="sxs-lookup"><span data-stu-id="3abc0-127">c.</span></span> <span data-ttu-id="3abc0-128">Merhaba SAP CAL izni toodeploy Azure aboneliğinize verin.</span><span class="sxs-lookup"><span data-stu-id="3abc0-128">Give hello SAP CAL permission toodeploy into your Azure subscription.</span></span>

    > [!NOTE]
    <span data-ttu-id="3abc0-129">Merhaba sonraki adımlar nasıl toocreate bir SAP CAL hesap Resource Manager dağıtımları için gösterir.</span><span class="sxs-lookup"><span data-stu-id="3abc0-129">hello next steps show how toocreate an SAP CAL account for Resource Manager deployments.</span></span> <span data-ttu-id="3abc0-130">Bağlantılı toohello Klasik dağıtım modeli, SAP CAL hesabınız zaten varsa, *gerek* toofollow bu adımları toocreate yeni bir SAP CAL hesabı.</span><span class="sxs-lookup"><span data-stu-id="3abc0-130">If you already have an SAP CAL account that is linked toohello classic deployment model, you *need* toofollow these steps toocreate a new SAP CAL account.</span></span> <span data-ttu-id="3abc0-131">Merhaba yeni SAP CAL hesabı hello Resource Manager modelinde toodeploy gerekir.</span><span class="sxs-lookup"><span data-stu-id="3abc0-131">hello new SAP CAL account needs toodeploy in hello Resource Manager model.</span></span>

2. <span data-ttu-id="3abc0-132">toocreate yeni bir SAP CAL hesabı, hello **hesapları** sayfa, Azure için iki seçenek gösterir:</span><span class="sxs-lookup"><span data-stu-id="3abc0-132">toocreate a new SAP CAL account, hello **Accounts** page shows two choices for Azure:</span></span> 

    <span data-ttu-id="3abc0-133">a.</span><span class="sxs-lookup"><span data-stu-id="3abc0-133">a.</span></span> <span data-ttu-id="3abc0-134">**Microsoft Azure (Klasik)** hello Klasik dağıtım modeli ve artık tercih edilir.</span><span class="sxs-lookup"><span data-stu-id="3abc0-134">**Microsoft Azure (classic)** is hello classic deployment model and is no longer preferred.</span></span>

    <span data-ttu-id="3abc0-135">b.</span><span class="sxs-lookup"><span data-stu-id="3abc0-135">b.</span></span> <span data-ttu-id="3abc0-136">**Microsoft Azure** hello yeni Resource Manager dağıtım modeli.</span><span class="sxs-lookup"><span data-stu-id="3abc0-136">**Microsoft Azure** is hello new Resource Manager deployment model.</span></span>

    ![SAP CAL hesapları](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic-2a.PNG)

    <span data-ttu-id="3abc0-138">Merhaba Resource Manager modelinde toodeploy seçin **Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="3abc0-138">toodeploy in hello Resource Manager model, select **Microsoft Azure**.</span></span>

    ![SAP CAL hesapları](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic3c.PNG)

3. <span data-ttu-id="3abc0-140">Hello Azure girin **abonelik kimliği** hello Azure portalı üzerinde bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="3abc0-140">Enter hello Azure **Subscription ID** that can be found on hello Azure portal.</span></span> 

    ![SAP CAL abonelik kimliği](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic3c.PNG)

4. <span data-ttu-id="3abc0-142">tanımladığınız tooauthorize hello SAP CAL toodeploy hello Azure aboneliği içine, tıklatın **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="3abc0-142">tooauthorize hello SAP CAL toodeploy into hello Azure subscription you defined, click **Authorize**.</span></span> <span data-ttu-id="3abc0-143">Sayfa aşağıdaki hello hello tarayıcı sekmesinde görünür:</span><span class="sxs-lookup"><span data-stu-id="3abc0-143">hello following page appears in hello browser tab:</span></span>

    ![Oturum açma Internet Explorer bulut Hizmetleri](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic4c.PNG)

5. <span data-ttu-id="3abc0-145">Birden fazla kullanıcı listeleniyorsa, hello Microsoft bağlantılı toobe hello Abonelikteki hello Seçtiğiniz Azure aboneliği olan bir hesap seçin.</span><span class="sxs-lookup"><span data-stu-id="3abc0-145">If more than one user is listed, choose hello Microsoft account that is linked toobe hello coadministrator of hello Azure subscription you selected.</span></span> <span data-ttu-id="3abc0-146">Sayfa aşağıdaki hello hello tarayıcı sekmesinde görünür:</span><span class="sxs-lookup"><span data-stu-id="3abc0-146">hello following page appears in hello browser tab:</span></span>

    ![Internet Explorer bulut Hizmetleri onayı](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic5a.PNG)

6. <span data-ttu-id="3abc0-148">Tıklatın **kabul**.</span><span class="sxs-lookup"><span data-stu-id="3abc0-148">Click **Accept**.</span></span> <span data-ttu-id="3abc0-149">Merhaba Yetkilendirme başarılı olursa yeniden hello SAP CAL hesabı tanımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="3abc0-149">If hello authorization is successful, hello SAP CAL account definition displays again.</span></span> <span data-ttu-id="3abc0-150">Kısa bir süre sonra bir ileti hello yetkilendirme işleminin başarılı olduğunu onaylar.</span><span class="sxs-lookup"><span data-stu-id="3abc0-150">After a short time, a message confirms that hello authorization process was successful.</span></span>

7. <span data-ttu-id="3abc0-151">Yeni oluşturulan SAP CAL hesabı tooyour kullanıcı tooassign Merhaba, girin, **kullanıcı kimliği** hello hello sağ taraftaki metin kutusu ve tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="3abc0-151">tooassign hello newly created SAP CAL account tooyour user, enter your **User ID** in hello text box on hello right and click **Add**.</span></span> 

    ![Hesap toouser ilişkilendirme](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic8a.PNG)

8. <span data-ttu-id="3abc0-153">Merhaba kullanıcı toohello SAP CAL toosign kullanmak hesabınızla tooassociate tıklatın **gözden**.</span><span class="sxs-lookup"><span data-stu-id="3abc0-153">tooassociate your account with hello user that you use toosign in toohello SAP CAL, click **Review**.</span></span> 

9. <span data-ttu-id="3abc0-154">Kullanıcı ve yeni oluşturulan hello SAP CAL hesabı arasında toocreate hello ilişkilendirme tıklayın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="3abc0-154">toocreate hello association between your user and hello newly created SAP CAL account, click **Create**.</span></span>

    ![Kullanıcı tooaccount ilişkilendirme](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic9b.PNG)

<span data-ttu-id="3abc0-156">Olduğu bir SAP CAL hesabı başarıyla oluşturuldu:</span><span class="sxs-lookup"><span data-stu-id="3abc0-156">You successfully created an SAP CAL account that is able to:</span></span>

- <span data-ttu-id="3abc0-157">Merhaba Resource Manager dağıtım modeli kullanır.</span><span class="sxs-lookup"><span data-stu-id="3abc0-157">Use hello Resource Manager deployment model.</span></span>
- <span data-ttu-id="3abc0-158">SAP sistemleri Azure aboneliğinize dağıtın.</span><span class="sxs-lookup"><span data-stu-id="3abc0-158">Deploy SAP systems into your Azure subscription.</span></span>

> [!NOTE]
<span data-ttu-id="3abc0-159">Windows ve SQL Server göre hello SAP IDE çözüm dağıtabilmeniz için önce bir SAP CAL abonelik kaydınızı toosign gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="3abc0-159">Before you can deploy hello SAP IDES solution based on Windows and SQL Server, you might need toosign up for an SAP CAL subscription.</span></span> <span data-ttu-id="3abc0-160">Aksi takdirde hello çözümü olarak gösterebilir **kilitli** hello genel bakış sayfasında.</span><span class="sxs-lookup"><span data-stu-id="3abc0-160">Otherwise, hello solution might show up as **Locked** on hello overview page.</span></span>

### <a name="deploy-a-solution"></a><span data-ttu-id="3abc0-161">Bir çözüm dağıtma</span><span class="sxs-lookup"><span data-stu-id="3abc0-161">Deploy a solution</span></span>
1. <span data-ttu-id="3abc0-162">Bir SAP CAL hesabı kurduktan sonra seçin **SAP IDE çözüm Windows ve SQL Server üzerinde hello** çözümü.</span><span class="sxs-lookup"><span data-stu-id="3abc0-162">After you set up an SAP CAL account, select **hello SAP IDES solution on Windows and SQL Server** solution.</span></span> <span data-ttu-id="3abc0-163">Tıklatın **örnek Oluştur**ve hello kullanım ve koşulları koşullar onaylayın.</span><span class="sxs-lookup"><span data-stu-id="3abc0-163">Click **Create Instance**, and confirm hello usage and terms conditions.</span></span> 

2. <span data-ttu-id="3abc0-164">Merhaba üzerinde **temel mod: Örnek Oluştur** sayfasında gerekir:</span><span class="sxs-lookup"><span data-stu-id="3abc0-164">On hello **Basic Mode: Create Instance** page, you need to:</span></span>

    <span data-ttu-id="3abc0-165">a.</span><span class="sxs-lookup"><span data-stu-id="3abc0-165">a.</span></span> <span data-ttu-id="3abc0-166">Bir örnek girmek **adı**.</span><span class="sxs-lookup"><span data-stu-id="3abc0-166">Enter an instance **Name**.</span></span>

    <span data-ttu-id="3abc0-167">b.</span><span class="sxs-lookup"><span data-stu-id="3abc0-167">b.</span></span> <span data-ttu-id="3abc0-168">Bir Azure seçin **bölge**.</span><span class="sxs-lookup"><span data-stu-id="3abc0-168">Select an Azure **Region**.</span></span> <span data-ttu-id="3abc0-169">Birden çok Azure bölgeleri sunulan bir SAP CAL abonelik tooget gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="3abc0-169">You might need an SAP CAL subscription tooget multiple Azure regions offered.</span></span>

    <span data-ttu-id="3abc0-170">c.</span><span class="sxs-lookup"><span data-stu-id="3abc0-170">c.</span></span>  <span data-ttu-id="3abc0-171">Hello Yöneticisi girin **parola** gösterildiği gibi hello çözüm:</span><span class="sxs-lookup"><span data-stu-id="3abc0-171">Enter hello master **Password** for hello solution, as shown:</span></span>

    ![SAP CAL Basic modu: Örnek oluşturma](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic10a.png)

3. <span data-ttu-id="3abc0-173">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3abc0-173">Click **Create**.</span></span> <span data-ttu-id="3abc0-174">Bir süre sonra hello boyutu ve karmaşıklığı (hello) SAP CAL tahmini sağlar, hello çözümün bağlı olarak hello durumu etkin ve kullanım için hazır olarak gösterilir:</span><span class="sxs-lookup"><span data-stu-id="3abc0-174">After some time, depending on hello size and complexity of hello solution (hello SAP CAL provides an estimate), hello status is shown as active and ready for use:</span></span> 

    ![SAP CAL örnekleri](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic12a.png)

4. <span data-ttu-id="3abc0-176">toofind hello kaynak grubu ve tarafından oluşturulan tüm nesnelerini SAP CAL Merhaba, toohello Azure portalına gidin.</span><span class="sxs-lookup"><span data-stu-id="3abc0-176">toofind hello resource group and all its objects that were created by hello SAP CAL, go toohello Azure portal.</span></span> <span data-ttu-id="3abc0-177">Merhaba sanal makine aynı hello SAP CAL verilen adı örneği hello başlayarak bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="3abc0-177">hello virtual machine can be found starting with hello same instance name that was given in hello SAP CAL.</span></span>

    ![Kaynak grubu nesneleri](./media/cal-ides-erp6-ehp7-sp3-sql/ides_resource_group.PNG)

5. <span data-ttu-id="3abc0-179">Dağıtılan toohello örnekleri Hello SAP CAL portalında gidin ve tıklayın **Bağlan**.</span><span class="sxs-lookup"><span data-stu-id="3abc0-179">On hello SAP CAL portal, go toohello deployed instances and click **Connect**.</span></span> <span data-ttu-id="3abc0-180">açılır pencere aşağıdaki hello görünür:</span><span class="sxs-lookup"><span data-stu-id="3abc0-180">hello following pop-up window appears:</span></span> 

    ![Toohello örneğine bağlanma](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic14a.PNG)

6. <span data-ttu-id="3abc0-182">Merhaba seçenekleri tooconnect dağıtılan toohello sistemlerinden birini kullanmadan önce tıklatın **Başlarken Kılavuzu**.</span><span class="sxs-lookup"><span data-stu-id="3abc0-182">Before you can use one of hello options tooconnect toohello deployed systems, click **Getting Started Guide**.</span></span> <span data-ttu-id="3abc0-183">Merhaba belgelerine adları kullanıcıların her hello bağlantı yöntemleri için hello.</span><span class="sxs-lookup"><span data-stu-id="3abc0-183">hello documentation names hello users for each of hello connectivity methods.</span></span> <span data-ttu-id="3abc0-184">Merhaba parolaları olan kullanıcılar için tanımladığınız toohello ana parola hello hello dağıtım işleminin başında ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="3abc0-184">hello passwords for those users are set toohello master password you defined at hello beginning of hello deployment process.</span></span> <span data-ttu-id="3abc0-185">Merhaba belgelerinde kullanabileceğiniz parolalarını ile daha işlevsel diğer kullanıcılar listelenir toohello toosign dağıtılan sistem.</span><span class="sxs-lookup"><span data-stu-id="3abc0-185">In hello documentation, other more functional users are listed with their passwords, which you can use toosign in toohello deployed system.</span></span>

    ![SAP Hoş Geldiniz belgeleri](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic15.jpg)

<span data-ttu-id="3abc0-187">Birkaç saat içinde sağlıklı bir SAP IDE sistem Azure'da dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="3abc0-187">Within a few hours, a healthy SAP IDES system is deployed in Azure.</span></span>

<span data-ttu-id="3abc0-188">Bir SAP CAL abonelik satın aldıysanız, SAP dağıtımlarınızı hello SAP CAL aracılığıyla Azure üzerinde tam olarak destekler.</span><span class="sxs-lookup"><span data-stu-id="3abc0-188">If you bought an SAP CAL subscription, SAP fully supports deployments through hello SAP CAL on Azure.</span></span> <span data-ttu-id="3abc0-189">Merhaba destek BC VCM CAL sırasıdır.</span><span class="sxs-lookup"><span data-stu-id="3abc0-189">hello support queue is BC-VCM-CAL.</span></span>

