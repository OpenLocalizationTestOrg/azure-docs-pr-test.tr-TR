---
title: "Azure DevTest Labs VM'de aaaDiagnose yapı hataları | Microsoft Docs"
description: "Bilgi nasıl DevTest Labs de tootroubleshoot yapı hataları"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 115e0086-3293-4adf-8738-9f639f31f918
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: tarcher
ms.openlocfilehash: 40b3cea72cf071cc5d9a6d002d309d923c3d3084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-artifact-failures-in-hello-lab"></a><span data-ttu-id="1e89f-103">Merhaba laboratuarda yapı hataları tanılama</span><span class="sxs-lookup"><span data-stu-id="1e89f-103">Diagnose artifact failures in hello lab</span></span> 
<span data-ttu-id="1e89f-104">Bir yapı oluşturduktan sonra başarılı veya başarısız olmadığını toosee kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1e89f-104">After you have created an artifact, you can check toosee if it succeeded or failed.</span></span> <span data-ttu-id="1e89f-105">DevTest Labs yapı günlükleri toodiagnose bir yapı hatası kullanabileceğiniz bilgiler sağlar.</span><span class="sxs-lookup"><span data-stu-id="1e89f-105">Artifact logs in DevTest Labs provide information you can use toodiagnose an artifact failure.</span></span> <span data-ttu-id="1e89f-106">Bir Windows VM hello yapı günlük bilgilerini görüntüleyebilirsiniz birkaç farklı yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="1e89f-106">There are a couple different ways you can view hello artifact log information for a Windows VM.</span></span>

> [!NOTE]
> <span data-ttu-id="1e89f-107">hataları doğru şekilde tanımlanır ve açıklanan, hello yapı düzgün yapılandırılmış önemlidir, tooensure.</span><span class="sxs-lookup"><span data-stu-id="1e89f-107">tooensure that failures are correctly identified and explained, it is important that hello artifact is properly structured.</span></span> <span data-ttu-id="1e89f-108">Nasıl bir yapı oluşturmak toocorrectly hakkında daha fazla bilgi için bkz: [özel yapılar oluşturma](devtest-lab-artifact-author.md).</span><span class="sxs-lookup"><span data-stu-id="1e89f-108">For information about how toocorrectly construct an artifact, see [Create custom artifacts](devtest-lab-artifact-author.md).</span></span> <span data-ttu-id="1e89f-109">Ve toosee örnek olarak düzgün yapılandırılmış bir yapı, bu denetleyin [Test parametre türleri](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts/windows-test-paramtypes) yapı.</span><span class="sxs-lookup"><span data-stu-id="1e89f-109">And toosee an example of a properly structured artifact, check out this [Test Parameter Types](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts/windows-test-paramtypes) artifact.</span></span>

## <a name="troubleshoot-artifact-failures-using-hello-azure-portal"></a><span data-ttu-id="1e89f-110">Hello Azure portal kullanarak yapı hatalarını giderme</span><span class="sxs-lookup"><span data-stu-id="1e89f-110">Troubleshoot artifact failures using hello Azure portal</span></span>
<span data-ttu-id="1e89f-111">toouse hello Azure portal toodiagnose hataları, yapı oluşturma sırasında şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="1e89f-111">toouse hello Azure portal toodiagnose failures during artifact creation, follow these steps:</span></span>

1. <span data-ttu-id="1e89f-112">Laboratuvarınızı kaynaklar Hello listesinden seçin.</span><span class="sxs-lookup"><span data-stu-id="1e89f-112">From hello list of resources, select your lab.</span></span>

2. <span data-ttu-id="1e89f-113">Merhaba tooinvestigate istediğiniz hello yapı içeren bir Windows VM seçin.</span><span class="sxs-lookup"><span data-stu-id="1e89f-113">Choose hello Windows VM that includes hello artifact you want tooinvestigate.</span></span>

3. <span data-ttu-id="1e89f-114">Altında hello sol panelinde **genel**, seçin **yapıları**.</span><span class="sxs-lookup"><span data-stu-id="1e89f-114">In hello left panel under **GENERAL**, choose **Artifacts**.</span></span> <span data-ttu-id="1e89f-115">Bu VM ile ilişkili yapıları listesi görüntülenir, belirten hello yapı ve durumunu hello adı.</span><span class="sxs-lookup"><span data-stu-id="1e89f-115">A list of artifacts associated with that VM appears, indicating hello name of hello artifact and its status.</span></span>

   ![Yapı git deposuna örnek](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifacts-failure.png)

4. <span data-ttu-id="1e89f-117">Bir durumunu gösteren bir yapı seçin **başarısız**.</span><span class="sxs-lookup"><span data-stu-id="1e89f-117">Choose an artifact that shows a status of **Failed**.</span></span> <span data-ttu-id="1e89f-118">Merhaba yapı açılır ve hello yapısı hello hata ayrıntılarını içeren bir uzantı iletisi gösterir.</span><span class="sxs-lookup"><span data-stu-id="1e89f-118">hello artifact opens and shows an extension message that includes details about hello failure of hello artifact.</span></span>

   ![Yapı git deposuna örnek](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifact-error.png)


## <a name="troubleshoot-artifact-failures-from-within-hello-vm"></a><span data-ttu-id="1e89f-120">Merhaba VM yapıt hatalarını giderme</span><span class="sxs-lookup"><span data-stu-id="1e89f-120">Troubleshoot artifact failures from within hello VM</span></span>
<span data-ttu-id="1e89f-121">tooview hello yapı günlükleri hello sanal makine içinde şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="1e89f-121">tooview hello artifact logs from within hello virtual machine, follow these steps:</span></span>

1. <span data-ttu-id="1e89f-122">Toohello toodiagnose istediğiniz hello yapı içeren VM oturum açın.</span><span class="sxs-lookup"><span data-stu-id="1e89f-122">Log in toohello VM that contains hello artifact you want toodiagnose.</span></span>

2. <span data-ttu-id="1e89f-123">Burada "1.9 hello CSE sürüm numarasıdır. tooC:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.9\Status gidin</span><span class="sxs-lookup"><span data-stu-id="1e89f-123">Navigate tooC:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.9\Status where "1.9 is hello CSE version number.</span></span>

   ![Yapı git deposuna örnek](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifact-error-vm-status.png)

3. <span data-ttu-id="1e89f-125">Açık hello **durum** dosya yardımcı o VM için yapı hataları tanılamak tooview bilgileri.</span><span class="sxs-lookup"><span data-stu-id="1e89f-125">Open hello **status** file tooview information that helps diagnose artifact failures for that VM.</span></span>




[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="1e89f-126">İlgili blog gönderileri</span><span class="sxs-lookup"><span data-stu-id="1e89f-126">Related blog posts</span></span>
* [<span data-ttu-id="1e89f-127">VM tooexisting AD Azure DevTest Labs'de resource manager şablonu kullanarak etki alanına katılma</span><span class="sxs-lookup"><span data-stu-id="1e89f-127">Join a VM tooexisting AD Domain using a resource manager template in Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)

## <a name="next-steps"></a><span data-ttu-id="1e89f-128">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1e89f-128">Next steps</span></span>
* <span data-ttu-id="1e89f-129">Nasıl çok öğrenin[Git deposu tooa Laboratuvar ekleme](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="1e89f-129">Learn how too[add a Git repository tooa lab](devtest-lab-add-artifact-repo.md).</span></span>

