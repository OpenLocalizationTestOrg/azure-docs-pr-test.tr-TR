---
title: "aaaHow toouse hello Azure bağımlı Hudson sürekli tümleştirme ile eklenti | Microsoft Docs"
description: "Nasıl toouse hello Azure bağımlı Hudson sürekli tümleştirme ile eklenti açıklar."
services: virtual-machines-linux
documentationcenter: 
author: rmcmurray
manager: wpickett
editor: 
ms.assetid: b2083d1c-4de8-4a19-a615-ccc9d9b6e1d9
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: cd6e67ad71c208aa56746aa8b70ba507da20bee9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-slave-plug-in-with-hudson-continuous-integration"></a><span data-ttu-id="b0149-103">Nasıl toouse hello Azure bağımlı Hudson sürekli tümleştirme ile eklentisi</span><span class="sxs-lookup"><span data-stu-id="b0149-103">How toouse hello Azure slave plug-in with Hudson Continuous Integration</span></span>
<span data-ttu-id="b0149-104">Dağıtılmış çalışan oluşturduğunda hello Azure bağımlı Hudson için eklenti tooprovision bağımlı düğümlerin Azure üzerinde sağlar.</span><span class="sxs-lookup"><span data-stu-id="b0149-104">hello Azure slave plug-in for Hudson enables you tooprovision slave nodes on Azure when running distributed builds.</span></span>

## <a name="install-hello-azure-slave-plug-in"></a><span data-ttu-id="b0149-105">Hello Azure bağımlı eklentisini yükleme</span><span class="sxs-lookup"><span data-stu-id="b0149-105">Install hello Azure Slave plug-in</span></span>
1. <span data-ttu-id="b0149-106">Hello Hudson Pano, tıklatın **yönetmek Hudson**.</span><span class="sxs-lookup"><span data-stu-id="b0149-106">In hello Hudson dashboard, click **Manage Hudson**.</span></span>
2. <span data-ttu-id="b0149-107">Merhaba, **yönetmek Hudson** sayfasında, tıklatın **eklentileri yönetme**.</span><span class="sxs-lookup"><span data-stu-id="b0149-107">In hello **Manage Hudson** page, click on **Manage Plugins**.</span></span>
3. <span data-ttu-id="b0149-108">Merhaba tıklatın **kullanılabilir** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="b0149-108">Click hello **Available** tab.</span></span>
4. <span data-ttu-id="b0149-109">Tıklatın **arama** ve türü **Azure** toolimit hello listesi toorelevant eklentileri.</span><span class="sxs-lookup"><span data-stu-id="b0149-109">Click **Search** and type **Azure** toolimit hello list toorelevant plug-ins.</span></span>
   
    <span data-ttu-id="b0149-110">Kullanılabilir eklentiler hello listesi aracılığıyla tooscroll seçerseniz, hello Azure bağımlı hello altında eklenti bulacaksınız **küme yönetimi ve dağıtılmış yapı** hello bölümünde **başkalarının** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="b0149-110">If you opt tooscroll through hello list of available plug-ins, you will find hello Azure slave plug-in under hello **Cluster Management and Distributed Build** section in hello **Others** tab.</span></span>
5. <span data-ttu-id="b0149-111">Merhaba onay kutusunu seçip **Azure bağımlı eklentisi**.</span><span class="sxs-lookup"><span data-stu-id="b0149-111">Select hello checkbox for **Azure Slave Plugin**.</span></span>
6. <span data-ttu-id="b0149-112">**Yükle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b0149-112">Click **Install**.</span></span>
7. <span data-ttu-id="b0149-113">Hudson yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="b0149-113">Restart Hudson.</span></span>

<span data-ttu-id="b0149-114">Bu hello eklentisi yüklü artık hello sonraki adımlar tooconfigure hello toocreate hello VM hello ikincil düğüm için oluşturmada kullanılacak bir şablon ve Azure abonelik profiliyle eklenti olacaktır.</span><span class="sxs-lookup"><span data-stu-id="b0149-114">Now that hello plug-in is installed, hello next steps would be tooconfigure hello plug-in with your Azure subscription profile and toocreate a template that will be used in creating hello VM for hello slave node.</span></span>

## <a name="configure-hello-azure-slave-plug-in-with-your-subscription-profile"></a><span data-ttu-id="b0149-115">Abonelik profilinizle Hello Azure bağımlı eklentisi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b0149-115">Configure hello Azure Slave plug-in with your subscription profile</span></span>
<span data-ttu-id="b0149-116">Bir abonelik profili de yayımlama başvurulan tooas ayarları, güvenli kimlik bilgileri ve geliştirme ortamınızda Azure ile toowork gerekir bazı ek bilgiler içeren bir XML dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="b0149-116">A subscription profile, also referred tooas publish settings, is an XML file that contains secure credentials and some additional information you'll need toowork with Azure in your development environment.</span></span> <span data-ttu-id="b0149-117">tooconfigure hello Azure bağımlı eklentisi, şunlar gerekir:</span><span class="sxs-lookup"><span data-stu-id="b0149-117">tooconfigure hello Azure slave plug-in, you need:</span></span>

* <span data-ttu-id="b0149-118">Abonelik kimliği</span><span class="sxs-lookup"><span data-stu-id="b0149-118">Your subscription id</span></span>
* <span data-ttu-id="b0149-119">Aboneliğiniz için bir yönetim sertifikası</span><span class="sxs-lookup"><span data-stu-id="b0149-119">A management certificate for your subscription</span></span>

<span data-ttu-id="b0149-120">Bunlar bulunabilir, [abonelik profili].</span><span class="sxs-lookup"><span data-stu-id="b0149-120">These can be found in your [subscription profile].</span></span> <span data-ttu-id="b0149-121">Aşağıda, bir abonelik profili örneğidir.</span><span class="sxs-lookup"><span data-stu-id="b0149-121">Below is an example of a subscription profile.</span></span>

    <?xml version="1.0" encoding="utf-8"?>

        <PublishData>

          <PublishProfile SchemaVersion="2.0" PublishMethod="AzureServiceManagementAPI">

        <Subscription

              ServiceManagementUrl="https://management.core.windows.net"

              Id="<Subscription ID>"

              Name="Pay-As-You-Go"
            ManagementCertificate="<Management certificate value>" />

          </PublishProfile>

    </PublishData>

<span data-ttu-id="b0149-122">Abonelik profilinizi oluşturduktan sonra bu adımları tooconfigure hello Azure bağımlı eklenti izleyin.</span><span class="sxs-lookup"><span data-stu-id="b0149-122">Once you have your subscription profile, follow these steps tooconfigure hello Azure slave plug-in.</span></span>

1. <span data-ttu-id="b0149-123">Hello Hudson Pano, tıklatın **yönetmek Hudson**.</span><span class="sxs-lookup"><span data-stu-id="b0149-123">In hello Hudson dashboard, click **Manage Hudson**.</span></span>
2. <span data-ttu-id="b0149-124">Tıklatın **sistem yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="b0149-124">Click **Configure System**.</span></span>
3. <span data-ttu-id="b0149-125">Merhaba sayfa toofind hello aşağı **bulut** bölümü.</span><span class="sxs-lookup"><span data-stu-id="b0149-125">Scroll down hello page toofind hello **Cloud** section.</span></span>
4. <span data-ttu-id="b0149-126">Tıklatın **yeni bulut Ekle > Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="b0149-126">Click **Add new cloud > Microsoft Azure**.</span></span>
   
    ![Yeni bulut ekleme][add new cloud]
   
    <span data-ttu-id="b0149-128">Bu abonelik ayrıntılarınızı hello alanları tooenter gereken yeri gösterir.</span><span class="sxs-lookup"><span data-stu-id="b0149-128">This will show hello fields where you need tooenter your subscription details.</span></span>
   
    ![profili yapılandırma][configure profile]
5. <span data-ttu-id="b0149-130">Abonelik profilinizden Hello abonelik kimliği ve yönetim sertifikası kopyalayın ve bunları hello uygun alanlara yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="b0149-130">Copy hello subscription id and management certificate from your subscription profile and paste them in hello appropriate fields.</span></span>
   
    <span data-ttu-id="b0149-131">Merhaba abonelik kimliği ve yönetim sertifikası, kopyalarken **sağlamadığı** hello değerlerini alın hello tırnak işaretleri içine.</span><span class="sxs-lookup"><span data-stu-id="b0149-131">When copying hello subscription id and management certificate, **do not** include hello quotes that enclose hello values.</span></span>
6. <span data-ttu-id="b0149-132">Tıklayın **doğrulama yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="b0149-132">Click on **Verify configuration**.</span></span>
7. <span data-ttu-id="b0149-133">Merhaba yapılandırması başarıyla doğrulandığında tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="b0149-133">When hello configuration is verified successfully, click **Save**.</span></span>

## <a name="set-up-a-virtual-machine-template-for-hello-azure-slave-plug-in"></a><span data-ttu-id="b0149-134">Bir sanal makine şablonu hello Azure bağımlı için eklenti ayarlayın</span><span class="sxs-lookup"><span data-stu-id="b0149-134">Set up a virtual machine template for hello Azure Slave plug-in</span></span>
<span data-ttu-id="b0149-135">Bir sanal makine şablonu hello parametrelerini tanımlar hello eklenti toocreate ikincil düğüm Azure üzerinde kullanır.</span><span class="sxs-lookup"><span data-stu-id="b0149-135">A virtual machine template defines hello parameters hello plug-in will use toocreate a slave node on Azure.</span></span> <span data-ttu-id="b0149-136">Aşağıdaki adımları hello şablonu için bir Ubuntu VM oluşturuluyor.</span><span class="sxs-lookup"><span data-stu-id="b0149-136">In hello following steps we'll be creating template for an Ubuntu VM.</span></span>

1. <span data-ttu-id="b0149-137">Hello Hudson Pano, tıklatın **yönetmek Hudson**.</span><span class="sxs-lookup"><span data-stu-id="b0149-137">In hello Hudson dashboard, click **Manage Hudson**.</span></span>
2. <span data-ttu-id="b0149-138">Tıklayın **sistem yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="b0149-138">Click on **Configure System**.</span></span>
3. <span data-ttu-id="b0149-139">Merhaba sayfa toofind hello aşağı **bulut** bölümü.</span><span class="sxs-lookup"><span data-stu-id="b0149-139">Scroll down hello page toofind hello **Cloud** section.</span></span>
4. <span data-ttu-id="b0149-140">Merhaba içinde **bulut** bölümünde, bulma **Azure sanal makine şablonu ekleme** hello tıklatıp **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="b0149-140">Within hello **Cloud** section, find **Add Azure Virtual Machine Template** and click hello **Add** button.</span></span>
   
    ![VM şablonu Ekle][add vm template]
5. <span data-ttu-id="b0149-142">Bir bulut hizmet adı hello belirtmeniz **adı** alan.</span><span class="sxs-lookup"><span data-stu-id="b0149-142">Specify a cloud service name in hello **Name** field.</span></span> <span data-ttu-id="b0149-143">Belirttiğiniz hello ad bulut hizmeti varolan tooan başvuruyorsa, bu hizmeti hello VM sağlanacak.</span><span class="sxs-lookup"><span data-stu-id="b0149-143">If hello name you specify refers tooan existing cloud service, hello VM will be provisioned in that service.</span></span> <span data-ttu-id="b0149-144">Aksi takdirde, Azure yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b0149-144">Otherwise, Azure will create a new one.</span></span>
6. <span data-ttu-id="b0149-145">Merhaba, **açıklama** alan, hello şablonu oluşturuyorsanız açıklayan metin girin.</span><span class="sxs-lookup"><span data-stu-id="b0149-145">In hello **Description** field, enter text that describes hello template you are creating.</span></span> <span data-ttu-id="b0149-146">Bu bilgiler yalnızca documentary amaçlıdır ve bir VM sağlama kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="b0149-146">This information is only for documentary purposes and is not used in provisioning a VM.</span></span>
7. <span data-ttu-id="b0149-147">Merhaba, **etiketleri** alanına, **linux**.</span><span class="sxs-lookup"><span data-stu-id="b0149-147">In hello **Labels** field, enter **linux**.</span></span> <span data-ttu-id="b0149-148">Bu etiket kullanılan tooidentify hello şablonu oluşturduğunuz ve sonradan kullanılan tooreference hello şablonu Hudson işi oluştururken.</span><span class="sxs-lookup"><span data-stu-id="b0149-148">This label is used tooidentify hello template you are creating and is subsequently used tooreference hello template when creating a Hudson job.</span></span>
8. <span data-ttu-id="b0149-149">Merhaba VM oluşturulacağı bir bölge seçin.</span><span class="sxs-lookup"><span data-stu-id="b0149-149">Select a region where hello VM will be created.</span></span>
9. <span data-ttu-id="b0149-150">Merhaba uygun VM boyutunu seçin.</span><span class="sxs-lookup"><span data-stu-id="b0149-150">Select hello appropriate VM size.</span></span>
10. <span data-ttu-id="b0149-151">Merhaba VM oluşturulacağı bir depolama hesabı belirtin.</span><span class="sxs-lookup"><span data-stu-id="b0149-151">Specify a storage account where hello VM will be created.</span></span> <span data-ttu-id="b0149-152">Hello olduğundan emin olun, kullanıyor hello bulut hizmeti ile aynı bölgeye.</span><span class="sxs-lookup"><span data-stu-id="b0149-152">Make sure that it is in hello same region as hello cloud service you'll be using.</span></span> <span data-ttu-id="b0149-153">Oluşturulan yeni depolama toobe istiyorsanız bu alanı boş bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b0149-153">If you want new storage toobe created, you can leave this field blank.</span></span>
11. <span data-ttu-id="b0149-154">Bekletme süresini dakika boşta bir ikincil Hudson siler önce hello sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="b0149-154">Retention time specifies hello number of minutes before Hudson deletes an idle slave.</span></span> <span data-ttu-id="b0149-155">Merhaba varsayılan değer 60 olarak bırakın.</span><span class="sxs-lookup"><span data-stu-id="b0149-155">Leave this at hello default value of 60.</span></span>
12. <span data-ttu-id="b0149-156">İçinde **kullanım**, bu ikincil düğüm kullanıldığında hello uygun koşulu seçin.</span><span class="sxs-lookup"><span data-stu-id="b0149-156">In **Usage**, select hello appropriate condition when this slave node will be used.</span></span> <span data-ttu-id="b0149-157">Şimdilik, seçin **bu düğüm mümkün olduğunca kullanma**.</span><span class="sxs-lookup"><span data-stu-id="b0149-157">For now, select **Utilize this node as much as possible**.</span></span>
    
     <span data-ttu-id="b0149-158">Bu noktada, formunuz biraz benzer toothis görünür:</span><span class="sxs-lookup"><span data-stu-id="b0149-158">At this point, your form would look somewhat similar toothis:</span></span>
    
     ![Şablon yapılandırma][template config]
13. <span data-ttu-id="b0149-160">İçinde **görüntü ailesi veya kimliği** hangi sistem görüntüsü de kendi VM'nizi yüklenecek toospecify sahip.</span><span class="sxs-lookup"><span data-stu-id="b0149-160">In **Image Family or Id** you have toospecify what system image will be installed on your VM.</span></span> <span data-ttu-id="b0149-161">Görüntü aileleri listesinden seçin veya özel bir görüntü belirtin.</span><span class="sxs-lookup"><span data-stu-id="b0149-161">You can either select from a list of image families or specify a custom image.</span></span>
    
     <span data-ttu-id="b0149-162">Görüntü aileleri listesinden tooselect istiyorsanız, hello ilk karakteri (büyük küçük harfe duyarlı) hello görüntü ailesi adı girin.</span><span class="sxs-lookup"><span data-stu-id="b0149-162">If you want tooselect from a list of image families, enter hello first character (case-sensitive) of hello image family name.</span></span> <span data-ttu-id="b0149-163">Örneğin, yazarak **U** Ubuntu Server ailelerinin listesini getirir.</span><span class="sxs-lookup"><span data-stu-id="b0149-163">For instance, typing **U** will bring up a list of Ubuntu Server families.</span></span> <span data-ttu-id="b0149-164">Merhaba listeden seçtikten sonra Jenkins VM ayrılırken hello bu aile, sistem görüntüsünü en son sürümünü kullanır.</span><span class="sxs-lookup"><span data-stu-id="b0149-164">Once you select from hello list, Jenkins will use hello latest version of that system image from that family when provisioning your VM.</span></span>
    
     ![İşletim sistemi ailesi listesi][OS family list]
    
     <span data-ttu-id="b0149-166">Bunun yerine toouse istediğiniz özel bir görüntü varsa, bu özel görüntü hello adını girin.</span><span class="sxs-lookup"><span data-stu-id="b0149-166">If you have a custom image that you want toouse instead, enter hello name of that custom image.</span></span> <span data-ttu-id="b0149-167">Bu nedenle gerekir özel resim adları bir listede adı hello tooensure doğru girildiğini gösterilmez.</span><span class="sxs-lookup"><span data-stu-id="b0149-167">Custom image names are not shown in a list so you have tooensure that hello name is entered correctly.</span></span>    
    
     <span data-ttu-id="b0149-168">Bu öğretici için yazın **U** Ubuntu görüntüleri seçin ve bir liste toobring **Ubuntu Server 14.04 LTS**.</span><span class="sxs-lookup"><span data-stu-id="b0149-168">For this tutorial, type **U** toobring up a list of Ubuntu images and select **Ubuntu Server 14.04 LTS**.</span></span>
14. <span data-ttu-id="b0149-169">İçin **başlatma yöntemi**seçin **SSH**.</span><span class="sxs-lookup"><span data-stu-id="b0149-169">For **Launch method**, select **SSH**.</span></span>
15. <span data-ttu-id="b0149-170">Aşağıda başlangıç betiği kopyalayıp hello **Init betik** alan.</span><span class="sxs-lookup"><span data-stu-id="b0149-170">Copy hello script below and paste in hello **Init script** field.</span></span>
    
         # Install Java
    
         sudo apt-get -y update
    
         sudo apt-get install -y openjdk-7-jdk
    
         sudo apt-get -y update --fix-missing
    
         sudo apt-get install -y openjdk-7-jdk
    
         # Install git
    
         sudo apt-get install -y git
    
         #Install ant
    
         sudo apt-get install -y ant
    
         sudo apt-get -y update --fix-missing
    
         sudo apt-get install -y ant
    
     <span data-ttu-id="b0149-171">Merhaba **Init betik** VM oluşturulduğunda hello sonra yürütülür.</span><span class="sxs-lookup"><span data-stu-id="b0149-171">hello **Init script** will be executed after hello VM is created.</span></span> <span data-ttu-id="b0149-172">Bu örnekte, Java, git ve ant hello betik yükler.</span><span class="sxs-lookup"><span data-stu-id="b0149-172">In this example, hello script installs Java, git, and ant.</span></span>
16. <span data-ttu-id="b0149-173">Merhaba, **kullanıcıadı** ve **parola** alanları, VM üzerinde oluşturulacak hello yönetici hesabı için tercih edilen değerlerinizi girin.</span><span class="sxs-lookup"><span data-stu-id="b0149-173">In hello **Username** and **Password** fields, enter your preferred values for hello administrator account that will be created on your VM.</span></span>
17. <span data-ttu-id="b0149-174">Tıklayın **doğrulayın şablonu** belirttiğiniz başlangıç parametreleri geçerliyse toocheck.</span><span class="sxs-lookup"><span data-stu-id="b0149-174">Click on **Verify Template** toocheck if hello parameters you specified are valid.</span></span>
18. <span data-ttu-id="b0149-175">**Kaydet**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b0149-175">Click on **Save**.</span></span>

## <a name="create-a-hudson-job-that-runs-on-a-slave-node-on-azure"></a><span data-ttu-id="b0149-176">Azure üzerinde bir ikincil düğüm üzerinde çalışan bir Hudson iş oluşturma</span><span class="sxs-lookup"><span data-stu-id="b0149-176">Create a Hudson job that runs on a slave node on Azure</span></span>
<span data-ttu-id="b0149-177">Bu bölümde, Azure üzerinde bir ikincil düğüm üzerinde çalışacak Hudson görev oluşturma.</span><span class="sxs-lookup"><span data-stu-id="b0149-177">In this section, you'll be creating a Hudson task that will run on a slave node on Azure.</span></span>

1. <span data-ttu-id="b0149-178">Hello Hudson Pano, tıklatın **yeni iş**.</span><span class="sxs-lookup"><span data-stu-id="b0149-178">In hello Hudson dashboard, click **New Job**.</span></span>
2. <span data-ttu-id="b0149-179">Oluşturmakta olduğunuz hello işi için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="b0149-179">Enter a name for hello job you are creating.</span></span>
3. <span data-ttu-id="b0149-180">Merhaba iş türü için **serbest stili yazılım işi yapı**.</span><span class="sxs-lookup"><span data-stu-id="b0149-180">For hello job type, select **Build a free-style software job**.</span></span>
4. <span data-ttu-id="b0149-181">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b0149-181">Click **OK**.</span></span>
5. <span data-ttu-id="b0149-182">Merhaba iş yapılandırma sayfasında, seçin **burada bu proje çalıştırılabilir sınırla**.</span><span class="sxs-lookup"><span data-stu-id="b0149-182">In hello job configuration page, select **Restrict where this project can be run**.</span></span>
6. <span data-ttu-id="b0149-183">Seçin **düğümü ve etiket menü** seçip **linux** (biz Bu etiket hello önceki bölümde hello sanal makine şablonu oluştururken, belirtilen).</span><span class="sxs-lookup"><span data-stu-id="b0149-183">Select **Node and label menu** and select **linux** (we specified this label when creating hello virtual machine template in hello previous section).</span></span>
7. <span data-ttu-id="b0149-184">Merhaba, **yapı** 'yi tıklatın **Ekle derleme adımı** seçip **Kabuk yürütme**.</span><span class="sxs-lookup"><span data-stu-id="b0149-184">In hello **Build** section, click **Add build step** and select **Execute shell**.</span></span>
8. <span data-ttu-id="b0149-185">Aşağıdaki komut, değiştirme hello Düzenle **{github hesap adınız}**, **{projenizin adına}**, ve **{proje dizininiz}** uygun değerleri ile Merhaba yapıştırın komut dosyası görünür hello metin alanında düzenlenebilir.</span><span class="sxs-lookup"><span data-stu-id="b0149-185">Edit hello following script, replacing **{your github account name}**, **{your project name}**, and **{your project directory}** with appropriate values, and paste hello edited script in hello text area that appears.</span></span>
   
        # Clone from git repo
   
        currentDir="$PWD"
   
        if [ -e {your project directory} ]; then
   
              cd {your project directory}
   
              git pull origin master
   
        else
   
              git clone https://github.com/{your github account name}/{your project name}.git
   
        fi
   
        # change directory tooproject
   
        cd $currentDir/{your project directory}
   
        #Execute build task
   
        ant
9. <span data-ttu-id="b0149-186">**Kaydet**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b0149-186">Click on **Save**.</span></span>
10. <span data-ttu-id="b0149-187">Buna Hudson Pano Merhaba, yeni oluşturduğunuz hello işi bulun ve hello üzerinde tıklatın **bir yapı zamanlama** simgesi.</span><span class="sxs-lookup"><span data-stu-id="b0149-187">In hello Hudson dashboard, find hello job you just created and click on hello **Schedule a build** icon.</span></span>

<span data-ttu-id="b0149-188">Hudson sonra hello önceki bölümde oluşturduğunuz hello şablonu kullanarak bir ikincil düğüm oluşturabilir ve bu görev için hello yapı adımında belirtilen hello betiğini yürütün.</span><span class="sxs-lookup"><span data-stu-id="b0149-188">Hudson will then create a slave node using hello template created in hello previous section and execute hello script you specified in hello build step for this task.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b0149-189">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="b0149-189">Next Steps</span></span>
<span data-ttu-id="b0149-190">Azure Java ile kullanma hakkında daha fazla bilgi için bkz: Merhaba [Azure Java Geliştirici Merkezi].</span><span class="sxs-lookup"><span data-stu-id="b0149-190">For more information about using Azure with Java, see hello [Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Geliştirici Merkezi]: https://azure.microsoft.com/develop/java/
[abonelik profili]: http://go.microsoft.com/fwlink/?LinkID=396395

<!-- IMG List -->

[add new cloud]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-addcloud.png
[configure profile]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-configureprofile.png
[add vm template]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-addnewvmtemplate.png
[template config]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-templateconfig1-withdata.png
[OS family list]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-oslist.png

