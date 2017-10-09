---
title: "aaaRunbook ayarları | Microsoft Docs"
description: "Azure Automation runbook Hello yapılandırma ayarlarını açıklar ve nasıl her ikisini de kullanarak bunları hello Azure Yönetim Portalı ve Windows PowerShell toochange."
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: a726f20c-a952-48b8-88ee-36d76aa3ac61
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/11/2016
ms.author: bwren
ms.openlocfilehash: 6f0ef09c148355a351464424c22c33df9300f0dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-settings"></a><span data-ttu-id="0471c-103">Runbook ayarları</span><span class="sxs-lookup"><span data-stu-id="0471c-103">Runbook settings</span></span>
<span data-ttu-id="0471c-104">Azure Otomasyonu içindeki her runbook'un günlüğe kaydetme davranışını tanımlanan toobe ve toochange yardımcı birden çok ayara sahiptir.</span><span class="sxs-lookup"><span data-stu-id="0471c-104">Each runbook in Azure Automation has multiple settings that help it toobe identified and toochange its logging behavior.</span></span> <span data-ttu-id="0471c-105">Bu ayarların her biri aşağıda hakkında yordamlar tarafından izlenen açıklanan toomodify bunları.</span><span class="sxs-lookup"><span data-stu-id="0471c-105">Each of these settings is described below followed by procedures on how toomodify them.</span></span>

## <a name="settings"></a><span data-ttu-id="0471c-106">Ayarlar</span><span class="sxs-lookup"><span data-stu-id="0471c-106">Settings</span></span>
### <a name="name-and-description"></a><span data-ttu-id="0471c-107">Ad ve açıklama</span><span class="sxs-lookup"><span data-stu-id="0471c-107">Name and description</span></span>
<span data-ttu-id="0471c-108">Oluşturulduktan sonra bir runbook hello adını değiştiremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="0471c-108">You cannot change hello name of a runbook after it has been created.</span></span> <span data-ttu-id="0471c-109">Merhaba Açıklama isteğe bağlıdır ve too512 karakter olabilir.</span><span class="sxs-lookup"><span data-stu-id="0471c-109">hello Description is optional and can be up too512 characters.</span></span>

### <a name="tags"></a><span data-ttu-id="0471c-110">Etiketler</span><span class="sxs-lookup"><span data-stu-id="0471c-110">Tags</span></span>
<span data-ttu-id="0471c-111">Etiketler, tooassign ayrı sözcükleri ve tümcecikleri toohelp bir runbook'u tanımlamaya izin verir.</span><span class="sxs-lookup"><span data-stu-id="0471c-111">Tags allow you tooassign distinct words and phrases toohelp identify a runbook.</span></span> <span data-ttu-id="0471c-112">Örneğin, ne zaman gönderdiğiniz bir runbook toohello [PowerShell Galerisi](https://www.powershellgallery.com/), belirli etiketleri tooidentify kategorilerini hello runbook listelenen belirtin.</span><span class="sxs-lookup"><span data-stu-id="0471c-112">For example, when you submit a runbook toohello [PowerShell Gallery](https://www.powershellgallery.com/), you specify particular tags tooidentify which categories hello runbook should be listed in.</span></span> <span data-ttu-id="0471c-113">Bir runbook için birden çok etiket virgül ile ayırarak belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0471c-113">You can specify multiple tags for a runbook by separating them with commas.</span></span>

### <a name="logging"></a><span data-ttu-id="0471c-114">Günlüğe kaydetme</span><span class="sxs-lookup"><span data-stu-id="0471c-114">Logging</span></span>
<span data-ttu-id="0471c-115">Varsayılan olarak, ayrıntılı ve ilerleme durumu kayıtlarını toojob geçmişine yazılmaz.</span><span class="sxs-lookup"><span data-stu-id="0471c-115">By default, Verbose and Progress records are not written toojob history.</span></span> <span data-ttu-id="0471c-116">Bu kayıtları belirli runbook toolog hello ayarlarını değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0471c-116">You can change hello settings for a particular runbook toolog these records.</span></span> <span data-ttu-id="0471c-117">Bu kayıtlar hakkında daha fazla bilgi için bkz: [Runbook çıkışı ve iletileri](automation-runbook-output-and-messages.md).</span><span class="sxs-lookup"><span data-stu-id="0471c-117">For more information on these records, see [Runbook Output and Messages](automation-runbook-output-and-messages.md).</span></span>

## <a name="changing-runbook-settings"></a><span data-ttu-id="0471c-118">Runbook ayarlarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="0471c-118">Changing runbook settings</span></span>

### <a name="changing-runbook-settings-with-hello-azure-portal"></a><span data-ttu-id="0471c-119">Hello Azure portalı ile runbook ayarlarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="0471c-119">Changing runbook settings with hello Azure portal</span></span>
<span data-ttu-id="0471c-120">Hello hello Azure Portalı'nda bir runbook ayarlarını değiştirebilirsiniz **ayarları** dikey penceresinde hello runbook için.</span><span class="sxs-lookup"><span data-stu-id="0471c-120">You can change settings for a runbook in hello Azure portal from hello **Settings** blade for hello runbook.</span></span>

1. <span data-ttu-id="0471c-121">Hello Azure portal, seçin **Otomasyon** ve ardından bir Otomasyon hesabı hello adını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="0471c-121">In hello Azure portal, select **Automation** and then then click hello name of an automation account.</span></span>
2. <span data-ttu-id="0471c-122">Select hello **Runbook'lar** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="0471c-122">Select hello **Runbooks** tab.</span></span>
3. <span data-ttu-id="0471c-123">Bir runbook'un Hello adına tıklayın ve yönlendirilmiş toohello ayarları dikey penceresinde hello runbook.</span><span class="sxs-lookup"><span data-stu-id="0471c-123">Click hello name of a runbook and you are directed toohello settings blade for hello runbook.</span></span> <span data-ttu-id="0471c-124">Buradan belirtin veya etiketleri değiştirebilir, runbook açıklaması Merhaba, günlüğe kaydetme ve izleme ayarlarını yapılandırın ve sorunları çözmek Destek Araçları toohelp erişim.</span><span class="sxs-lookup"><span data-stu-id="0471c-124">From here you can specify or modify tags, hello runbook description, configure logging and tracing settings, and access support tools toohelp you solve problems.</span></span>     

### <a name="changing-runbook-settings-with-windows-powershell"></a><span data-ttu-id="0471c-125">Windows PowerShell ile runbook ayarlarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="0471c-125">Changing runbook settings with Windows PowerShell</span></span>
<span data-ttu-id="0471c-126">Merhaba kullanabilirsiniz [kümesi AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603786.aspx) bir runbook için cmdlet toochange hello ayarları.</span><span class="sxs-lookup"><span data-stu-id="0471c-126">You can use hello [Set-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603786.aspx) cmdlet toochange hello settings for a runbook.</span></span> <span data-ttu-id="0471c-127">Birden çok etiket toospecify istiyorsanız, virgülle ayrılmış değerler toohello etiketleri parametresi ile bir dizi veya tek bir dize ya da sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="0471c-127">If you want toospecify multiple tags, you can either provide an array or a single string with comma delimited values toohello Tags parameter.</span></span> <span data-ttu-id="0471c-128">Merhaba geçerli hello etiketleriyle alabilirsiniz [Get-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603728.aspx).</span><span class="sxs-lookup"><span data-stu-id="0471c-128">You can get hello current tags with hello [Get-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603728.aspx).</span></span>

<span data-ttu-id="0471c-129">Aşağıdaki örnek komutlar hello tooset hello bir runbook'un özelliklerinin nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="0471c-129">hello following sample commands show how tooset hello properties for a runbook.</span></span> <span data-ttu-id="0471c-130">Bu örnek toohello varolan etiketleri ve ayrıntılı kayıtları günlüğe kaydedileceğini belirtir üç etiketleri ekler.</span><span class="sxs-lookup"><span data-stu-id="0471c-130">This sample adds three tags toohello existing tags and specifies that verbose records should be logged.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    $tags = (Get-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName).Tags
    $tags += "Tag1,Tag2,Tag3"
    Set-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName –LogVerbose $true –Tags $tags

## <a name="next-steps"></a><span data-ttu-id="0471c-131">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0471c-131">Next steps</span></span>
* <span data-ttu-id="0471c-132">toocreate ve alma çıkış ve hata iletileri, runbook'lardan nasıl görürüm toolearn [Runbook çıkışı ve iletileri](automation-runbook-output-and-messages.md)</span><span class="sxs-lookup"><span data-stu-id="0471c-132">toolearn how toocreate and retrieve output and error messages from runbooks, see [Runbook Output and Messages](automation-runbook-output-and-messages.md)</span></span> 
* <span data-ttu-id="0471c-133">tooadd hello topluluk veya başka kaynak veya toocreate kendi runbook zaten geliştirilmiştir bir runbook nasıl görürüm toounderstand [oluşturma veya bir Runbook'u içeri aktarma](automation-creating-importing-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="0471c-133">toounderstand how tooadd a runbook that was already developed by hello community or other source, or toocreate your own runbook see [Creating or Importing a Runbook](automation-creating-importing-runbook.md)</span></span> 

