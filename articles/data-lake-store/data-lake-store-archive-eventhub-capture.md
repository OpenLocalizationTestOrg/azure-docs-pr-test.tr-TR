---
title: Azure Data Lake Store Event Hubs'a aaaCapture verilerden | Microsoft Docs
description: "Olay hub'ları kullanmak Azure Data Lake Store toocapture verileri"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/28/2017
ms.author: nitinme
ms.openlocfilehash: 09b17bd0b47043bd2c83dba72c01a8064f206a0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-data-lake-store-toocapture-data-from-event-hubs"></a><span data-ttu-id="deee9-103">Olay hub'ları kullanmak Azure Data Lake Store toocapture verileri</span><span class="sxs-lookup"><span data-stu-id="deee9-103">Use Azure Data Lake Store toocapture data from Event Hubs</span></span>

<span data-ttu-id="deee9-104">Azure Event Hubs tarafından nasıl toouse Azure Data Lake Store toocapture veri alınan öğrenin.</span><span class="sxs-lookup"><span data-stu-id="deee9-104">Learn how toouse Azure Data Lake Store toocapture data received by Azure Event Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="deee9-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="deee9-105">Prerequisites</span></span>

* <span data-ttu-id="deee9-106">**Bir Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="deee9-106">**An Azure subscription**.</span></span> <span data-ttu-id="deee9-107">Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="deee9-107">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="deee9-108">**Bir Azure Data Lake Store hesabı**.</span><span class="sxs-lookup"><span data-stu-id="deee9-108">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="deee9-109">Yönergeler için toocreate bir, bkz: [Azure Data Lake Store ile çalışmaya başlama](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="deee9-109">For instructions on how toocreate one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md).</span></span>

*  <span data-ttu-id="deee9-110">**Bir olay hub'ları ad alanı**.</span><span class="sxs-lookup"><span data-stu-id="deee9-110">**An Event Hubs namespace**.</span></span> <span data-ttu-id="deee9-111">Yönergeler için bkz: [bir olay hub'ları ad alanı oluşturma](../event-hubs/event-hubs-create.md#create-an-event-hubs-namespace).</span><span class="sxs-lookup"><span data-stu-id="deee9-111">For instructions, see [Create an Event Hubs namespace](../event-hubs/event-hubs-create.md#create-an-event-hubs-namespace).</span></span> <span data-ttu-id="deee9-112">Merhaba Data Lake Store hesabı ve hello olay hub'ları ad hello olduğundan emin olun aynı Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="deee9-112">Make sure hello Data Lake Store account and hello Event Hubs namespace are in hello same Azure subscription.</span></span>


## <a name="assign-permissions-tooevent-hubs"></a><span data-ttu-id="deee9-113">İzinleri tooEvent hub'ları atayın</span><span class="sxs-lookup"><span data-stu-id="deee9-113">Assign permissions tooEvent Hubs</span></span>

<span data-ttu-id="deee9-114">Bu bölümde, olay hub'ları toocapture hello verileri istediğiniz bir klasörde hello hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="deee9-114">In this section, you create a folder within hello account where you want toocapture hello data from Event Hubs.</span></span> <span data-ttu-id="deee9-115">Böylece bir Data Lake Store hesabına veri yazabilirsiniz tooEvent hub'ları da izinleri atayın.</span><span class="sxs-lookup"><span data-stu-id="deee9-115">You also assign permissions tooEvent Hubs so that it can write data into a Data Lake Store account.</span></span> 

1. <span data-ttu-id="deee9-116">Burada Event Hubs toocapture verilerini istediğiniz ve tıklayın hello Data Lake Store hesabını açın **Veri Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="deee9-116">Open hello Data Lake Store account where you want toocapture data from Event Hubs and then click on **Data Explorer**.</span></span>

    <span data-ttu-id="deee9-117">![Data Lake Store Veri Gezgini](./media/data-lake-store-archive-eventhub-capture/data-lake-store-open-data-explorer.png "Data Lake Store Veri Gezgini")</span><span class="sxs-lookup"><span data-stu-id="deee9-117">![Data Lake Store data explorer](./media/data-lake-store-archive-eventhub-capture/data-lake-store-open-data-explorer.png "Data Lake Store data explorer")</span></span>

2.  <span data-ttu-id="deee9-118">Tıklatın **yeni klasör** ve toocapture hello veri klasörü için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="deee9-118">Click **New Folder** and then enter a name for folder where you want toocapture hello data.</span></span>

    <span data-ttu-id="deee9-119">![Data Lake Store içinde yeni bir klasör oluşturun](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-new-folder.png "Data Lake Store içinde yeni bir klasör oluşturun")</span><span class="sxs-lookup"><span data-stu-id="deee9-119">![Create a new folder in Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-new-folder.png "Create a new folder in Data Lake Store")</span></span>

3. <span data-ttu-id="deee9-120">Merhaba Data Lake Store hello kökündeki izinleri atayın.</span><span class="sxs-lookup"><span data-stu-id="deee9-120">Assign permissions at hello root of hello Data Lake Store.</span></span> 

    <span data-ttu-id="deee9-121">a.</span><span class="sxs-lookup"><span data-stu-id="deee9-121">a.</span></span> <span data-ttu-id="deee9-122">Tıklatın **Veri Gezgini**hello kökündeki hello Data Lake Store hesabını seçin ve ardından **erişim**.</span><span class="sxs-lookup"><span data-stu-id="deee9-122">Click **Data Explorer**, select hello root of hello Data Lake Store account, and then click **Access**.</span></span>

    <span data-ttu-id="deee9-123">![Data Lake Store kök izinlerini atamak](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-root.png "Data Lake Store kök izinlerini atama")</span><span class="sxs-lookup"><span data-stu-id="deee9-123">![Assign permissions for Data Lake Store root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-root.png "Assign permissions for Data Lake Store root")</span></span>

    <span data-ttu-id="deee9-124">b.</span><span class="sxs-lookup"><span data-stu-id="deee9-124">b.</span></span> <span data-ttu-id="deee9-125">Altında **erişim**, tıklatın **Ekle**, tıklatın **kullanıcı veya Grup Seç**, arayın ve sonra `Microsoft.EventHubs`.</span><span class="sxs-lookup"><span data-stu-id="deee9-125">Under **Access**, click **Add**, click **Select User or Group**, and then search for `Microsoft.EventHubs`.</span></span> 

    <span data-ttu-id="deee9-126">![Data Lake Store kök izinlerini atamak](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Data Lake Store kök izinlerini atama")</span><span class="sxs-lookup"><span data-stu-id="deee9-126">![Assign permissions for Data Lake Store root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Assign permissions for Data Lake Store root")</span></span>
    
    <span data-ttu-id="deee9-127">**Seç**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="deee9-127">Click **Select**.</span></span>

    <span data-ttu-id="deee9-128">c.</span><span class="sxs-lookup"><span data-stu-id="deee9-128">c.</span></span> <span data-ttu-id="deee9-129">Altında **izinleri atamak**, tıklatın **Select izinleri**.</span><span class="sxs-lookup"><span data-stu-id="deee9-129">Under **Assign Permissions**, click **Select Permissions**.</span></span> <span data-ttu-id="deee9-130">Ayarlama **izinleri** çok**yürütme**.</span><span class="sxs-lookup"><span data-stu-id="deee9-130">Set **Permissions** too**Execute**.</span></span> <span data-ttu-id="deee9-131">Ayarlama **eklemek** çok**bu klasör ve tüm alt öğeleri**.</span><span class="sxs-lookup"><span data-stu-id="deee9-131">Set **Add to** too**This folder and all children**.</span></span> <span data-ttu-id="deee9-132">Ayarlama **olarak eklemek** çok**erişim izni girdisi ve varsayılan izin girdisi**.</span><span class="sxs-lookup"><span data-stu-id="deee9-132">Set **Add as** too**An access permission entry and a default permission entry**.</span></span>

    <span data-ttu-id="deee9-133">![Data Lake Store kök izinlerini atamak](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp1.png "Data Lake Store kök izinlerini atama")</span><span class="sxs-lookup"><span data-stu-id="deee9-133">![Assign permissions for Data Lake Store root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp1.png "Assign permissions for Data Lake Store root")</span></span>

    <span data-ttu-id="deee9-134">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="deee9-134">Click **OK**.</span></span>

4. <span data-ttu-id="deee9-135">Data Lake Store hesabı altında toocapture verilerin istediğiniz hello klasör izinlerini atayın.</span><span class="sxs-lookup"><span data-stu-id="deee9-135">Assign permissions for hello folder under Data Lake Store account where you want toocapture data.</span></span>

    <span data-ttu-id="deee9-136">a.</span><span class="sxs-lookup"><span data-stu-id="deee9-136">a.</span></span> <span data-ttu-id="deee9-137">Tıklatın **Veri Gezgini**hello Data Lake Store hesabına başlangıç klasörü seçin ve ardından **erişim**.</span><span class="sxs-lookup"><span data-stu-id="deee9-137">Click **Data Explorer**, select hello folder in hello Data Lake Store account, and then click **Access**.</span></span>

    <span data-ttu-id="deee9-138">![Data Lake Store klasör izinlerini atamak](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-folder.png "Data Lake Store klasörün izinlerini atama")</span><span class="sxs-lookup"><span data-stu-id="deee9-138">![Assign permissions for Data Lake Store folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-folder.png "Assign permissions for Data Lake Store folder")</span></span>

    <span data-ttu-id="deee9-139">b.</span><span class="sxs-lookup"><span data-stu-id="deee9-139">b.</span></span> <span data-ttu-id="deee9-140">Altında **erişim**, tıklatın **Ekle**, tıklatın **kullanıcı veya Grup Seç**, arayın ve sonra `Microsoft.EventHubs`.</span><span class="sxs-lookup"><span data-stu-id="deee9-140">Under **Access**, click **Add**, click **Select User or Group**, and then search for `Microsoft.EventHubs`.</span></span> 

    <span data-ttu-id="deee9-141">![Data Lake Store klasör izinlerini atamak](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Data Lake Store klasörün izinlerini atama")</span><span class="sxs-lookup"><span data-stu-id="deee9-141">![Assign permissions for Data Lake Store folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Assign permissions for Data Lake Store folder")</span></span>
    
    <span data-ttu-id="deee9-142">**Seç**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="deee9-142">Click **Select**.</span></span>

    <span data-ttu-id="deee9-143">c.</span><span class="sxs-lookup"><span data-stu-id="deee9-143">c.</span></span> <span data-ttu-id="deee9-144">Altında **izinleri atamak**, tıklatın **Select izinleri**.</span><span class="sxs-lookup"><span data-stu-id="deee9-144">Under **Assign Permissions**, click **Select Permissions**.</span></span> <span data-ttu-id="deee9-145">Ayarlama **izinleri** çok**okuma, yazma,** ve **yürütme**.</span><span class="sxs-lookup"><span data-stu-id="deee9-145">Set **Permissions** too**Read, Write,** and **Execute**.</span></span> <span data-ttu-id="deee9-146">Ayarlama **eklemek** çok**bu klasör ve tüm alt öğeleri**.</span><span class="sxs-lookup"><span data-stu-id="deee9-146">Set **Add to** too**This folder and all children**.</span></span> <span data-ttu-id="deee9-147">Son olarak, ayarlamak **olarak eklemek** çok**erişim izni girdisi ve varsayılan izin girdisi**.</span><span class="sxs-lookup"><span data-stu-id="deee9-147">Finally, set **Add as** too**An access permission entry and a default permission entry**.</span></span>

    <span data-ttu-id="deee9-148">![Data Lake Store klasör izinlerini atamak](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp-folder.png "Data Lake Store klasörün izinlerini atama")</span><span class="sxs-lookup"><span data-stu-id="deee9-148">![Assign permissions for Data Lake Store folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp-folder.png "Assign permissions for Data Lake Store folder")</span></span>
    
    <span data-ttu-id="deee9-149">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="deee9-149">Click **OK**.</span></span> 

## <a name="configure-event-hubs-toocapture-data-toodata-lake-store"></a><span data-ttu-id="deee9-150">Olay hub'ları toocapture veri tooData Lake deposu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="deee9-150">Configure Event Hubs toocapture data tooData Lake Store</span></span>

<span data-ttu-id="deee9-151">Bu bölümde, bir olay hub'ları ad alanı içindeki bir Event Hub oluşturun.</span><span class="sxs-lookup"><span data-stu-id="deee9-151">In this section, you create an Event Hub within an Event Hubs namespace.</span></span> <span data-ttu-id="deee9-152">Merhaba olay hub'ı toocapture veri tooan Azure Data Lake Store hesabını yapılandırmanız da.</span><span class="sxs-lookup"><span data-stu-id="deee9-152">You also configure hello Event Hub toocapture data tooan Azure Data Lake Store account.</span></span> <span data-ttu-id="deee9-153">Bu bölümde, bir olay hub'ları ad alanı zaten oluşturduğunuzu varsayar.</span><span class="sxs-lookup"><span data-stu-id="deee9-153">This section assumes that you have already created an Event Hubs namespace.</span></span>

2. <span data-ttu-id="deee9-154">Merhaba gelen **genel bakış** hello olay hub'ları ad alanının bölmesi **+ olay hub'ı**.</span><span class="sxs-lookup"><span data-stu-id="deee9-154">From hello **Overview** pane of hello Event Hubs namespace, click **+ Event Hub**.</span></span>

    <span data-ttu-id="deee9-155">![Olay hub'ı oluşturma](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-event-hub.png "olay hub'ı Oluştur")</span><span class="sxs-lookup"><span data-stu-id="deee9-155">![Create Event Hub](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-event-hub.png "Create Event Hub")</span></span>

3. <span data-ttu-id="deee9-156">Tooconfigure olay hub'ları toocapture veri tooData Lake deposu Hello aşağıdaki değerleri belirtin.</span><span class="sxs-lookup"><span data-stu-id="deee9-156">Provide hello following values tooconfigure Event Hubs toocapture data tooData Lake Store.</span></span>

    <span data-ttu-id="deee9-157">![Olay hub'ı oluşturma](./media/data-lake-store-archive-eventhub-capture/data-lake-store-configure-eventhub.png "olay hub'ı Oluştur")</span><span class="sxs-lookup"><span data-stu-id="deee9-157">![Create Event Hub](./media/data-lake-store-archive-eventhub-capture/data-lake-store-configure-eventhub.png "Create Event Hub")</span></span>

    <span data-ttu-id="deee9-158">a.</span><span class="sxs-lookup"><span data-stu-id="deee9-158">a.</span></span> <span data-ttu-id="deee9-159">Merhaba Event Hub için bir ad sağlayın.</span><span class="sxs-lookup"><span data-stu-id="deee9-159">Provide a name for hello Event Hub.</span></span>
    
    <span data-ttu-id="deee9-160">b.</span><span class="sxs-lookup"><span data-stu-id="deee9-160">b.</span></span> <span data-ttu-id="deee9-161">Bu öğretici için ayarlanmış **bölüm sayısı** ve **ileti bekletme** toohello varsayılan değerleri.</span><span class="sxs-lookup"><span data-stu-id="deee9-161">For this tutorial, set **Partition Count** and **Message Retention** toohello default values.</span></span>
    
    <span data-ttu-id="deee9-162">c.</span><span class="sxs-lookup"><span data-stu-id="deee9-162">c.</span></span> <span data-ttu-id="deee9-163">Ayarlama **yakalama** çok**üzerinde**.</span><span class="sxs-lookup"><span data-stu-id="deee9-163">Set **Capture** too**On**.</span></span> <span data-ttu-id="deee9-164">Set hello **zaman penceresi** (ne sıklıkta toocapture) ve **boyutu penceresi** (veri boyutu toocapture).</span><span class="sxs-lookup"><span data-stu-id="deee9-164">Set hello **Time Window** (how frequently toocapture) and **Size Window** (data size toocapture).</span></span> 
    
    <span data-ttu-id="deee9-165">d.</span><span class="sxs-lookup"><span data-stu-id="deee9-165">d.</span></span> <span data-ttu-id="deee9-166">İçin **yakalama sağlayıcısı**seçin **Azure Data Lake Store** ve hello seçin hello daha önce oluşturduğunuz Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="deee9-166">For **Capture Provider**, select **Azure Data Lake Store** and hello select hello Data Lake Store you created earlier.</span></span> <span data-ttu-id="deee9-167">İçin **Data Lake yolu**, hello hello Data Lake Store hesabı oluşturduğunuz hello klasörün adını girin.</span><span class="sxs-lookup"><span data-stu-id="deee9-167">For **Data Lake Path**, enter hello name of hello folder you created in hello Data Lake Store account.</span></span> <span data-ttu-id="deee9-168">Yalnızca tooprovide hello göreli yol toohello klasörü gerekir.</span><span class="sxs-lookup"><span data-stu-id="deee9-168">You only need tooprovide hello relative path toohello folder.</span></span>

    <span data-ttu-id="deee9-169">e.</span><span class="sxs-lookup"><span data-stu-id="deee9-169">e.</span></span> <span data-ttu-id="deee9-170">Merhaba bırakın **örnek yakalama dosyası adı biçimlerini** toohello varsayılan değeri.</span><span class="sxs-lookup"><span data-stu-id="deee9-170">Leave hello **Sample capture file name formats** toohello default value.</span></span> <span data-ttu-id="deee9-171">Bu seçenek hello yakalama klasörü altında oluşturulan hello klasör yapısını yönetir.</span><span class="sxs-lookup"><span data-stu-id="deee9-171">This option governs hello folder structure that is created under hello capture folder.</span></span>

    <span data-ttu-id="deee9-172">f.</span><span class="sxs-lookup"><span data-stu-id="deee9-172">f.</span></span> <span data-ttu-id="deee9-173">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="deee9-173">Click **Create**.</span></span>

## <a name="test-hello-setup"></a><span data-ttu-id="deee9-174">Test hello Kurulumu</span><span class="sxs-lookup"><span data-stu-id="deee9-174">Test hello setup</span></span>

<span data-ttu-id="deee9-175">Şimdi veri toohello Azure olay hub'ı göndererek hello çözüm test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="deee9-175">You can now test hello solution by sending data toohello Azure Event Hub.</span></span> <span data-ttu-id="deee9-176">Merhaba yönergeleri izleyin [tooAzure olay hub'ları olayları göndermek](../event-hubs/event-hubs-dotnet-framework-getstarted-send.md).</span><span class="sxs-lookup"><span data-stu-id="deee9-176">Follow hello instructions at [Send events tooAzure Event Hubs](../event-hubs/event-hubs-dotnet-framework-getstarted-send.md).</span></span> <span data-ttu-id="deee9-177">Merhaba veri göndermeye başla sonra belirttiğiniz hello klasör yapısını kullanarak Data Lake Store'da yansıtılan hello veri bakın.</span><span class="sxs-lookup"><span data-stu-id="deee9-177">Once you start sending hello data, you see hello data reflected in Data Lake Store using hello folder structure you specified.</span></span> <span data-ttu-id="deee9-178">Örneğin, bir klasör yapısı hello ekran, Data Lake Store aşağıdaki gösterildiği gibi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="deee9-178">For example, you see a folder structure, as shown in hello following screenshot, in your Data Lake Store.</span></span>

<span data-ttu-id="deee9-179">![Data Lake Store'da EventHub veri örneği](./media/data-lake-store-archive-eventhub-capture/data-lake-store-eventhub-data-sample.png "Data Lake Store'da örnek EventHub veri")</span><span class="sxs-lookup"><span data-stu-id="deee9-179">![Sample EventHub data in Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-eventhub-data-sample.png "Sample EventHub data in Data Lake Store")</span></span>

> [!NOTE]
> <span data-ttu-id="deee9-180">Event Hubs'a gelen iletileri yoksa bile, olay hub'ları yalnızca hello üstbilgileri boş dosyalarıyla Data Lake Store hesabı hello yazar.</span><span class="sxs-lookup"><span data-stu-id="deee9-180">Even if you do not have messages coming into Event Hubs, Event Hubs writes empty files with just hello headers into hello Data Lake Store account.</span></span> <span data-ttu-id="deee9-181">Merhaba dosyaları hello aynı yazılır hello olay hub'ları oluştururken sağladığınız zaman aralığı.</span><span class="sxs-lookup"><span data-stu-id="deee9-181">hello files are written at hello same time interval that you provided while creating hello Event Hubs.</span></span>
> 
>

## <a name="analyze-data-in-data-lake-store"></a><span data-ttu-id="deee9-182">Data Lake Store'da verileri analiz etme</span><span class="sxs-lookup"><span data-stu-id="deee9-182">Analyze data in Data Lake Store</span></span>

<span data-ttu-id="deee9-183">Merhaba veri Data Lake Store içinde olduğunda tooprocess ve crunch hello veri analitik işleri çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="deee9-183">Once hello data is in Data Lake Store, you can run analytical jobs tooprocess and crunch hello data.</span></span> <span data-ttu-id="deee9-184">Bkz: [USQL Avro örnek](https://github.com/Azure/usql/tree/master/Examples/AvroExamples) nasıl toodo bu Azure Data Lake Analytics'i kullanarak.</span><span class="sxs-lookup"><span data-stu-id="deee9-184">See [USQL Avro Example](https://github.com/Azure/usql/tree/master/Examples/AvroExamples) on how toodo this using Azure Data Lake Analytics.</span></span>
  

## <a name="see-also"></a><span data-ttu-id="deee9-185">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="deee9-185">See also</span></span>
* [<span data-ttu-id="deee9-186">Data Lake Store'da verilerin güvenliğini sağlama</span><span class="sxs-lookup"><span data-stu-id="deee9-186">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="deee9-187">Azure Storage Blobları tooData Lake Mağazası'ndan veri kopyalama</span><span class="sxs-lookup"><span data-stu-id="deee9-187">Copy data from Azure Storage Blobs tooData Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
