---
title: "Azure Batch kullanıcı hesaplarında aaaRun görevleri | Microsoft Docs"
description: "Azure toplu işlemde çalışan görevler için kullanıcı hesaplarını yapılandırma"
services: batch
author: tamram
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.openlocfilehash: 13d7d76451d89a3cca090c4ef24ed0ed781bbf09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-tasks-under-user-accounts-in-batch"></a><span data-ttu-id="62af6-103">Toplu işlemde kullanıcı hesapları görevleri Çalıştır</span><span class="sxs-lookup"><span data-stu-id="62af6-103">Run tasks under user accounts in Batch</span></span>

<span data-ttu-id="62af6-104">Azure Batch görevinde her zaman bir kullanıcı hesabı altında çalışır.</span><span class="sxs-lookup"><span data-stu-id="62af6-104">A task in Azure Batch always runs under a user account.</span></span> <span data-ttu-id="62af6-105">Varsayılan olarak, standart kullanıcı hesapları, yönetici izinleri olmayan altında görevlerini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="62af6-105">By default, tasks run under standard user accounts, without administrator permissions.</span></span> <span data-ttu-id="62af6-106">Bu varsayılan kullanıcı hesabı ayarları genellikle yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="62af6-106">These default user account settings are typically sufficient.</span></span> <span data-ttu-id="62af6-107">Bazı senaryolarda, ancak yararlı toobe mümkün tooconfigure hello kullanıcı hesabı altında görev toorun istediğiniz olur.</span><span class="sxs-lookup"><span data-stu-id="62af6-107">For certain scenarios, however, it's useful toobe able tooconfigure hello user account under which you want a task toorun.</span></span> <span data-ttu-id="62af6-108">Bu makalede, kullanıcı hesapları ve nasıl bunları senaryonuz için yapılandırabilirsiniz hello türleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="62af6-108">This article discusses hello types of user accounts and how you can configure them for your scenario.</span></span>

## <a name="types-of-user-accounts"></a><span data-ttu-id="62af6-109">Kullanıcı hesabı türleri</span><span class="sxs-lookup"><span data-stu-id="62af6-109">Types of user accounts</span></span>

<span data-ttu-id="62af6-110">Azure toplu işlem, görevleri çalıştırmak için iki tür kullanıcı hesabı sağlar:</span><span class="sxs-lookup"><span data-stu-id="62af6-110">Azure Batch provides two types of user accounts for running tasks:</span></span>

- <span data-ttu-id="62af6-111">**Otomatik kullanıcı hesapları.**</span><span class="sxs-lookup"><span data-stu-id="62af6-111">**Auto-user accounts.**</span></span> <span data-ttu-id="62af6-112">Otomatik kullanıcı hesapları hello Batch hizmeti tarafından otomatik olarak oluşturulan yerleşik kullanıcı hesaplarıdır.</span><span class="sxs-lookup"><span data-stu-id="62af6-112">Auto-user accounts are built-in user accounts that are created automatically by hello Batch service.</span></span> <span data-ttu-id="62af6-113">Varsayılan olarak, görevler bir otomatik kullanıcı hesabı altında çalışır.</span><span class="sxs-lookup"><span data-stu-id="62af6-113">By default, tasks run under an auto-user account.</span></span> <span data-ttu-id="62af6-114">Merhaba otomatik kullanıcı belirtimi altında hangi otomatik kullanıcı hesabın bir görevin çalışması gereken bir görev tooindicate için yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="62af6-114">You can configure hello auto-user specification for a task tooindicate under which auto-user account a task should run.</span></span> <span data-ttu-id="62af6-115">Merhaba otomatik kullanıcı belirtimi toospecify hello ayrıcalık düzeyinde ve kapsam hello görev çalıştıracak hello otomatik kullanıcı hesabının sağlar.</span><span class="sxs-lookup"><span data-stu-id="62af6-115">hello auto-user specification allows you toospecify hello elevation level and scope of hello auto-user account that will run hello task.</span></span> 

- <span data-ttu-id="62af6-116">**Adlı bir kullanıcı hesabı.**</span><span class="sxs-lookup"><span data-stu-id="62af6-116">**A named user account.**</span></span> <span data-ttu-id="62af6-117">Merhaba havuz oluşturduğunuzda havuz için bir veya daha fazla adlandırılmış kullanıcı hesapları belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="62af6-117">You can specify one or more named user accounts for a pool when you create hello pool.</span></span> <span data-ttu-id="62af6-118">Her kullanıcı hesabı hello havuzunun her bir düğümde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="62af6-118">Each user account is created on each node of hello pool.</span></span> <span data-ttu-id="62af6-119">Ayrıca toohello hesap adı, hello kullanıcı hesabı parolası, ayrıcalık düzeyi ve Linux havuzları, hello SSH özel anahtar belirtin.</span><span class="sxs-lookup"><span data-stu-id="62af6-119">In addition toohello account name, you specify hello user account password, elevation level, and, for Linux pools, hello SSH private key.</span></span> <span data-ttu-id="62af6-120">Bir görev eklediğinizde, kullanıcı hesabı altında bu görevin çalışması gerektiğini adlı hello belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="62af6-120">When you add a task, you can specify hello named user account under which that task should run.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="62af6-121">Bu sürüm, kod toocall güncelleştirmenin gerektirdiği önemli bir değişiklik Hello Batch hizmeti sürümü 2017 01 01.4.0 tanıtır.</span><span class="sxs-lookup"><span data-stu-id="62af6-121">hello Batch service version 2017-01-01.4.0 introduces a breaking change that requires that you update your code toocall that version.</span></span> <span data-ttu-id="62af6-122">Geçirme koddan toplu daha eski bir sürümü varsa, o hello Not **runElevated** özelliği hello REST API veya toplu istemci kitaplıkları artık desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="62af6-122">If you are migrating code from an older version of Batch, note that hello **runElevated** property is no longer supported in hello REST API or Batch client libraries.</span></span> <span data-ttu-id="62af6-123">Kullanım hello yeni **Userıdentity** görev toospecify ayrıcalık düzeyi özelliği.</span><span class="sxs-lookup"><span data-stu-id="62af6-123">Use hello new **userIdentity** property of a task toospecify elevation level.</span></span> <span data-ttu-id="62af6-124">Başlıklı hello bölümüne bakın [kod toohello en son toplu istemci Kitaplığı ', güncelleştirme](#update-your-code-to-the-latest-batch-client-library) hello istemci kitaplıklarından birini kullanıyorsanız, toplu kodunuzu güncelleştirmek için hızlı yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="62af6-124">See hello section titled [Update your code toohello latest Batch client library](#update-your-code-to-the-latest-batch-client-library) for quick guidelines for updating your Batch code if you are using one of hello client libraries.</span></span>
>
>

> [!NOTE] 
> <span data-ttu-id="62af6-125">Bu makalede açıklanan hello kullanıcı hesaplarına Uzak Masaüstü Protokolü (RDP) veya güvenli Kabuk (SSH), güvenlik nedenleriyle desteklemez.</span><span class="sxs-lookup"><span data-stu-id="62af6-125">hello user accounts discussed in this article do not support Remote Desktop Protocol (RDP) or Secure Shell (SSH), for security reasons.</span></span> 
>
> <span data-ttu-id="62af6-126">tooconnect tooa düğüm çalışan hello Linux sanal makine yapılandırması, SSH aracılığıyla bkz [kullanım Uzak Masaüstü tooa Azure Linux VM'de](../virtual-machines/virtual-machines-linux-use-remote-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="62af6-126">tooconnect tooa node running hello Linux virtual machine configuration via SSH, see [Use Remote Desktop tooa Linux VM in Azure](../virtual-machines/virtual-machines-linux-use-remote-desktop.md).</span></span> <span data-ttu-id="62af6-127">RDP aracılığıyla Windows çalıştıran tooconnect toonodes bkz [tooa Windows Server VM bağlanmak](../virtual-machines/windows/connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="62af6-127">tooconnect toonodes running Windows via RDP, see [Connect tooa Windows Server VM](../virtual-machines/windows/connect-logon.md).</span></span><br /><br />
> <span data-ttu-id="62af6-128">tooconnect tooa düğümünde çalışan hello bulut hizmeti aracılığıyla yapılandırmaya RDP, bkz: [bir rolde Azure bulut Hizmetleri için Uzak Masaüstü Bağlantısı etkinleştirmek](../cloud-services/cloud-services-role-enable-remote-desktop-new-portal.md).</span><span class="sxs-lookup"><span data-stu-id="62af6-128">tooconnect tooa node running hello cloud service configuration via RDP, see [Enable Remote Desktop Connection for a Role in Azure Cloud Services](../cloud-services/cloud-services-role-enable-remote-desktop-new-portal.md).</span></span>
>
>

## <a name="user-account-access-toofiles-and-directories"></a><span data-ttu-id="62af6-129">Kullanıcı hesabı erişimi toofiles ve dizinler</span><span class="sxs-lookup"><span data-stu-id="62af6-129">User account access toofiles and directories</span></span>

<span data-ttu-id="62af6-130">Bir otomatik kullanıcı hesabı ve adlı bir kullanıcı hesabı okuma/yazma erişimi toohello görevin çalışma dizini, paylaşılan dizine ve çok örnekli görevler dizini vardır.</span><span class="sxs-lookup"><span data-stu-id="62af6-130">Both an auto-user account and a named user account have read/write access toohello task’s working directory, shared directory, and multi-instance tasks directory.</span></span> <span data-ttu-id="62af6-131">Her iki türdeki hesaba okuma erişimi toohello başlangıç ve iş hazırlama dizinler sahiptir.</span><span class="sxs-lookup"><span data-stu-id="62af6-131">Both types of accounts have read access toohello startup and job preparation directories.</span></span>

<span data-ttu-id="62af6-132">Bir görev hello altında çalışıyorsa, çalıştırmak için bir başlangıç görevi, hello görev kullanılan aynı hesap okuma-yazma erişimi toohello başlangıç görevi dizini vardır.</span><span class="sxs-lookup"><span data-stu-id="62af6-132">If a task runs under hello same account that was used for running a start task, hello task has read-write access toohello start task directory.</span></span> <span data-ttu-id="62af6-133">Benzer şekilde, aynı görevin altında çalışıyorsa hello çalıştırmak için bir iş hazırlama görevi, hello görev kullanılan hesap okuma-yazma erişimi toohello iş hazırlama görevi dizini vardır.</span><span class="sxs-lookup"><span data-stu-id="62af6-133">Similarly, if a task runs under hello same account that was used for running a job preparation task, hello task has read-write access toohello job preparation task directory.</span></span> <span data-ttu-id="62af6-134">Bir görev hello başlangıç görevi veya iş hazırlama görevi farklı bir hesap altında çalışıyorsa, hello görevin yalnızca okuma erişimi toohello ilgili dizini vardır.</span><span class="sxs-lookup"><span data-stu-id="62af6-134">If a task runs under a different account than hello start task or job preparation task, then hello task has only read access toohello respective directory.</span></span>

<span data-ttu-id="62af6-135">Dosyalar ve dizinler görevden erişme hakkında daha fazla bilgi için bkz: [geliştirme büyük ölçekli paralel işlem çözümleri yığın](batch-api-basics.md#files-and-directories).</span><span class="sxs-lookup"><span data-stu-id="62af6-135">For more information on accessing files and directories from a task, see [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md#files-and-directories).</span></span>

## <a name="elevated-access-for-tasks"></a><span data-ttu-id="62af6-136">Görevler için yükseltilmiş erişim</span><span class="sxs-lookup"><span data-stu-id="62af6-136">Elevated access for tasks</span></span> 

<span data-ttu-id="62af6-137">Hello kullanıcı hesabının ayrıcalık düzeyi, bir görevin yükseltilmiş erişim ile çalışıp çalışmayacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="62af6-137">hello user account's elevation level indicates whether a task runs with elevated access.</span></span> <span data-ttu-id="62af6-138">Bir otomatik kullanıcı hesabı ve adlı bir kullanıcı hesabı ile yükseltilmiş erişim çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="62af6-138">Both an auto-user account and a named user account can run with elevated access.</span></span> <span data-ttu-id="62af6-139">ayrıcalık düzeyi için iki seçenek Hello şunlardır:</span><span class="sxs-lookup"><span data-stu-id="62af6-139">hello two options for elevation level are:</span></span>

- <span data-ttu-id="62af6-140">**NonAdmin:** hello görev, yükseltilmiş erişimi olmayan standart bir kullanıcı olarak çalışır.</span><span class="sxs-lookup"><span data-stu-id="62af6-140">**NonAdmin:** hello task runs as a standard user without elevated access.</span></span> <span data-ttu-id="62af6-141">Toplu kullanıcı hesabı için Hello varsayılan ayrıcalık düzeyi olduğundan her zaman **NonAdmin**.</span><span class="sxs-lookup"><span data-stu-id="62af6-141">hello default elevation level for a Batch user account is always **NonAdmin**.</span></span>
- <span data-ttu-id="62af6-142">**Yönetici:** hello görevi yükseltilmiş erişimi bir kullanıcı olarak çalışır ve tam yönetici izinlerine sahip çalışır.</span><span class="sxs-lookup"><span data-stu-id="62af6-142">**Admin:** hello task runs as a user with elevated access and operates with full Administrator permissions.</span></span> 

## <a name="auto-user-accounts"></a><span data-ttu-id="62af6-143">Otomatik kullanıcı hesapları</span><span class="sxs-lookup"><span data-stu-id="62af6-143">Auto-user accounts</span></span>

<span data-ttu-id="62af6-144">Varsayılan olarak, görevler yükseltilmiş erişimi olmadan ve görev kapsamlı standart bir kullanıcı olarak bir otomatik kullanıcı hesabı altında toplu işlemde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="62af6-144">By default, tasks run in Batch under an auto-user account, as a standard user without elevated access, and with task scope.</span></span> <span data-ttu-id="62af6-145">Merhaba otomatik kullanıcı belirtimi görev kapsam için yapılandırıldığında, hello Batch hizmeti yalnızca bu görev için bir otomatik kullanıcı hesabı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="62af6-145">When hello auto-user specification is configured for task scope, hello Batch service creates an auto-user account for that task only.</span></span>

<span data-ttu-id="62af6-146">Merhaba alternatif tootask kapsam havuzu kapsamıdır.</span><span class="sxs-lookup"><span data-stu-id="62af6-146">hello alternative tootask scope is pool scope.</span></span> <span data-ttu-id="62af6-147">Merhaba otomatik kullanıcı belirtimi bir görev için havuz kapsam için yapılandırıldığında, hello görev hello havuzunda kullanılabilir tooany görev bir otomatik kullanıcı hesabı altında çalışır.</span><span class="sxs-lookup"><span data-stu-id="62af6-147">When hello auto-user specification for a task is configured for pool scope, hello task runs under an auto-user account that is available tooany task in hello pool.</span></span> <span data-ttu-id="62af6-148">Başlıklı hello bölüme havuzu kapsamı hakkında daha fazla bilgi için bkz [otomatik kullanıcı havuzu kapsamlı hello gibi bir görevi çalıştırmayı](#run-a-task-as-the-autouser-with-pool-scope).</span><span class="sxs-lookup"><span data-stu-id="62af6-148">For more information about pool scope, see hello section titled [Run a task as hello auto-user with pool scope](#run-a-task-as-the-autouser-with-pool-scope).</span></span>   

<span data-ttu-id="62af6-149">Windows ve Linux düğümlerinde Hello varsayılan kapsam farklıdır:</span><span class="sxs-lookup"><span data-stu-id="62af6-149">hello default scope is different on Windows and Linux nodes:</span></span>

- <span data-ttu-id="62af6-150">Windows düğümlerinde görevler varsayılan olarak görev kapsam altında çalışır.</span><span class="sxs-lookup"><span data-stu-id="62af6-150">On Windows nodes, tasks run under task scope by default.</span></span>
- <span data-ttu-id="62af6-151">Linux düğümleri havuzu kapsam altında her zaman çalışır.</span><span class="sxs-lookup"><span data-stu-id="62af6-151">Linux nodes always run under pool scope.</span></span>

<span data-ttu-id="62af6-152">Her biri tooa benzersiz otomatik kullanıcı hesabına karşılık gelen hello otomatik kullanıcı belirtimi için dört olası yapılandırmaları vardır:</span><span class="sxs-lookup"><span data-stu-id="62af6-152">There are four possible configurations for hello auto-user specification, each of which corresponds tooa unique auto-user account:</span></span>

- <span data-ttu-id="62af6-153">Yönetici olmayan erişim görev kapsamlı (Merhaba varsayılan otomatik kullanıcı belirtimi)</span><span class="sxs-lookup"><span data-stu-id="62af6-153">Non-admin access with task scope (hello default auto-user specification)</span></span>
- <span data-ttu-id="62af6-154">Görev kapsamlı yönetici (yükseltilmiş) erişimi</span><span class="sxs-lookup"><span data-stu-id="62af6-154">Admin (elevated) access with task scope</span></span>
- <span data-ttu-id="62af6-155">Havuz kapsamlı yönetici olmayan erişim</span><span class="sxs-lookup"><span data-stu-id="62af6-155">Non-admin access with pool scope</span></span>
- <span data-ttu-id="62af6-156">Havuz kapsamlı yönetici erişimi</span><span class="sxs-lookup"><span data-stu-id="62af6-156">Admin access with pool scope</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="62af6-157">Görev kapsam altında çalışan görevler gerçek erişim tooother görevleri bir düğümde sahip değilsiniz.</span><span class="sxs-lookup"><span data-stu-id="62af6-157">Tasks running under task scope do not have de facto access tooother tasks on a node.</span></span> <span data-ttu-id="62af6-158">Ancak, kötü niyetli bir kullanıcı erişimi toohello hesabıyla yönetici ayrıcalıklarıyla çalıştırır ve diğer görev dizinleri erişen bir görev göndererek bu kısıtlamaya işe yarayabilir.</span><span class="sxs-lookup"><span data-stu-id="62af6-158">However, a malicious user with access toohello account could work around this restriction by submitting a task that runs with administrator privileges and accesses other task directories.</span></span> <span data-ttu-id="62af6-159">Kötü niyetli bir kullanıcının RDP veya SSH tooconnect tooa düğümünü de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="62af6-159">A malicious user could also use RDP or SSH tooconnect tooa node.</span></span> <span data-ttu-id="62af6-160">Önemli tooprotect erişim tooyour Batch hesabı anahtarları tooprevent böyle bir senaryo değil.</span><span class="sxs-lookup"><span data-stu-id="62af6-160">It's important tooprotect access tooyour Batch account keys tooprevent such a scenario.</span></span> <span data-ttu-id="62af6-161">Hesabınızı tehlikeye şüpheleniyorsanız emin tooregenerate anahtarlarınızı olabilir.</span><span class="sxs-lookup"><span data-stu-id="62af6-161">If you suspect your account may have been compromised, be sure tooregenerate your keys.</span></span>
>
>

### <a name="run-a-task-as-an-auto-user-with-elevated-access"></a><span data-ttu-id="62af6-162">Yükseltilmiş erişimi olan bir otomatik kullanıcı olarak bir görevi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="62af6-162">Run a task as an auto-user with elevated access</span></span>

<span data-ttu-id="62af6-163">Toorun yükseltilmiş erişimi olan bir task gerektiğinde Merhaba otomatik kullanıcı belirtimi için yönetici ayrıcalıkları yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="62af6-163">You can configure hello auto-user specification for administrator privileges when you need toorun a task with elevated access.</span></span> <span data-ttu-id="62af6-164">Örneğin, bir başlangıç görevi hello düğümünde yükseltilmiş erişim tooinstall yazılımı gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="62af6-164">For example, a start task may need elevated access tooinstall software on hello node.</span></span>

> [!NOTE] 
> <span data-ttu-id="62af6-165">Genel olarak, en iyi toouse yükseltilmiş erişim yalnızca gerekli olduğunda.</span><span class="sxs-lookup"><span data-stu-id="62af6-165">In general, it's best toouse elevated access only when necessary.</span></span> <span data-ttu-id="62af6-166">En iyi yöntemler hello en düşük ayrıcalık gerekli tooachieve hello istenen sonuca verme öneririz.</span><span class="sxs-lookup"><span data-stu-id="62af6-166">Best practices recommend granting hello minimum privilege necessary tooachieve hello desired outcome.</span></span> <span data-ttu-id="62af6-167">Örneğin, bir başlangıç görevi hello geçerli kullanıcıya yönelik yazılımları yerine tüm kullanıcılar için yüklerse yükseltilmiş erişim tootasks verme mümkün tooavoid olabilir.</span><span class="sxs-lookup"><span data-stu-id="62af6-167">For example, if a start task installs software for hello current user, instead of for all users, you may be able tooavoid granting elevated access tootasks.</span></span> <span data-ttu-id="62af6-168">Merhaba otomatik kullanıcı belirtimi hello aynı hello başlangıç görevi de dahil olmak üzere hesabı altında toorun gereken tüm görevler için havuz kapsamı ve yönetici olmayan erişim için yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="62af6-168">You can configure hello auto-user specification for pool scope and non-admin access for all tasks that need toorun under hello same account, including hello start task.</span></span> 
>
>

<span data-ttu-id="62af6-169">Aşağıdaki kod parçacıkları hello nasıl tooconfigure hello otomatik kullanıcı belirtimi gösterir.</span><span class="sxs-lookup"><span data-stu-id="62af6-169">hello following code snippets show how tooconfigure hello auto-user specification.</span></span> <span data-ttu-id="62af6-170">Merhaba örnekler set hello ayrıcalık düzeyi çok`Admin` ve kapsam çok hello`Task`.</span><span class="sxs-lookup"><span data-stu-id="62af6-170">hello examples set hello elevation level too`Admin` and hello scope too`Task`.</span></span> <span data-ttu-id="62af6-171">Görev kapsam hello varsayılan ayar, ancak örnek hello artırmak amacıyla için buraya dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="62af6-171">Task scope is hello default setting, but is included here for hello sake of example.</span></span>

#### <a name="batch-net"></a><span data-ttu-id="62af6-172">Batch .NET</span><span class="sxs-lookup"><span data-stu-id="62af6-172">Batch .NET</span></span>

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin, scope: AutoUserScope.Task));
```
#### <a name="batch-java"></a><span data-ttu-id="62af6-173">Batch Java</span><span class="sxs-lookup"><span data-stu-id="62af6-173">Batch Java</span></span>

```java
taskToAdd.withId(taskId)
        .withUserIdentity(new UserIdentity()
            .withAutoUser(new AutoUserSpecification()
                .withElevationLevel(ElevationLevel.ADMIN))
                .withScope(AutoUserScope.TASK));
        .withCommandLine("cmd /c echo hello");                        
```

#### <a name="batch-python"></a><span data-ttu-id="62af6-174">Batch Python</span><span class="sxs-lookup"><span data-stu-id="62af6-174">Batch Python</span></span>

```python
user = batchmodels.UserIdentity(
    auto_user=batchmodels.AutoUserSpecification(
        elevation_level=batchmodels.ElevationLevel.admin,
        scope=batchmodels.AutoUserScope.task))
task = batchmodels.TaskAddParameter(
    id='task_1',
    command_line='cmd /c "echo hello world"',
    user_identity=user)
batch_client.task.add(job_id=jobid, task=task)
```

### <a name="run-a-task-as-an-auto-user-with-pool-scope"></a><span data-ttu-id="62af6-175">Otomatik kullanıcı havuzu kapsamlı olarak bir görevi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="62af6-175">Run a task as an auto-user with pool scope</span></span>

<span data-ttu-id="62af6-176">Bir düğüm sağlandığında, iki havuzu genelinde otomatik-kullanıcı hesapları hello havuzdaki her düğüme, yükseltilmiş erişim biriyle ve yükseltilmiş erişimi olmadan bir oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="62af6-176">When a node is provisioned, two pool-wide auto-user accounts are created on each node in hello pool, one with elevated access, and one without elevated access.</span></span> <span data-ttu-id="62af6-177">Belirli bir görev için Hello otomatik kullanıcının kapsam toopool kapsamı ayarlama hello görev bu iki havuzu genelinde otomatik-kullanıcı hesaplarından birini altında çalışır.</span><span class="sxs-lookup"><span data-stu-id="62af6-177">Setting hello auto-user's scope toopool scope for a given task runs hello task under one of these two pool-wide auto-user accounts.</span></span> 

<span data-ttu-id="62af6-178">Hello otomatik-kullanıcının havuzu kapsamını belirttiğinizde, yönetici erişimine sahip çalışan tüm görevler hello altında Çalıştır aynı havuzu genelinde otomatik-kullanıcı hesabı.</span><span class="sxs-lookup"><span data-stu-id="62af6-178">When you specify pool scope for hello auto-user, all tasks that run with administrator access run under hello same pool-wide auto-user account.</span></span> <span data-ttu-id="62af6-179">Benzer şekilde, yönetici izinleri olmadan çalışan görevler de tek havuzu genelinde otomatik-kullanıcı hesabı altında çalışır.</span><span class="sxs-lookup"><span data-stu-id="62af6-179">Similarly, tasks that run without administrator permissions also run under a single pool-wide auto-user account.</span></span> 

> [!NOTE] 
> <span data-ttu-id="62af6-180">Merhaba iki havuzu genelinde otomatik-kullanıcı hesapları ayrı hesaplarıdır.</span><span class="sxs-lookup"><span data-stu-id="62af6-180">hello two pool-wide auto-user accounts are separate accounts.</span></span> <span data-ttu-id="62af6-181">Merhaba havuzu genelinde yönetici hesabı altında çalışan görevler hello standart hesap altında ve tersi yönde çalışan görevler ile verileri paylaşamaz.</span><span class="sxs-lookup"><span data-stu-id="62af6-181">Tasks running under hello pool-wide administrative account cannot share data with tasks running under hello standard account, and vice versa.</span></span> 
>
>

<span data-ttu-id="62af6-182">aynı otomatik kullanıcı hesabı olan hello üzerinde çalışan diğer görevleri mümkün tooshare verilerle görevlerdir hello altında avantajı toorunning hello aynı düğüm.</span><span class="sxs-lookup"><span data-stu-id="62af6-182">hello advantage toorunning under hello same auto-user account is that tasks are able tooshare data with other tasks running on hello same node.</span></span>

<span data-ttu-id="62af6-183">Çalışan görevlerin hello iki havuzu genelinde otomatik-kullanıcı hesaplarından birini altında yararlı olduğu bir senaryo gizli görevler arasında paylaşımıdır.</span><span class="sxs-lookup"><span data-stu-id="62af6-183">Sharing secrets between tasks is one scenario where running tasks under one of hello two pool-wide auto-user accounts is useful.</span></span> <span data-ttu-id="62af6-184">Örneğin, bir başlangıç görevi tooprovision diğer görevleri kullanabilirsiniz hello düğüm üzerine bir gizlilik gerektiğini varsayalım.</span><span class="sxs-lookup"><span data-stu-id="62af6-184">For example, suppose a start task needs tooprovision a secret onto hello node that other tasks can use.</span></span> <span data-ttu-id="62af6-185">Merhaba Windows Data Protection API (DPAPI) kullanabilirsiniz, ancak yönetici ayrıcalıkları gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="62af6-185">You could use hello Windows Data Protection API (DPAPI), but it requires administrator privileges.</span></span> <span data-ttu-id="62af6-186">Bunun yerine, hello gizli hello kullanıcı düzeyinde koruyabilir.</span><span class="sxs-lookup"><span data-stu-id="62af6-186">Instead, you can protect hello secret at hello user level.</span></span> <span data-ttu-id="62af6-187">Aynı kullanıcı hesabı erişebilir hello altında çalışan görevler hello yükseltilmiş erişimi olmadan gizli anahtarı.</span><span class="sxs-lookup"><span data-stu-id="62af6-187">Tasks running under hello same user account can access hello secret without elevated access.</span></span>

<span data-ttu-id="62af6-188">Başka bir senaryo toorun görevleri havuzu kapsamlı bir otomatik kullanıcı hesabı altında bozuk bir ileti geçirme arabirimi (MPI) dosyası istediğiniz paylaşır.</span><span class="sxs-lookup"><span data-stu-id="62af6-188">Another scenario where you may want toorun tasks under an auto-user account with pool scope is a Message Passing Interface (MPI) file share.</span></span> <span data-ttu-id="62af6-189">Bir MPI dosya paylaşımı, aynı dosya verilerini hello MPI görev gerek toowork üzerinde Hello düğümler hello yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="62af6-189">An MPI file share is useful when hello nodes in hello MPI task need toowork on hello same file data.</span></span> <span data-ttu-id="62af6-190">Merhaba baş düğümü oluşturur hello altında çalışıyorsa, hello alt düğümleri erişebileceği bir dosya paylaşımı aynı otomatik kullanıcı hesabı.</span><span class="sxs-lookup"><span data-stu-id="62af6-190">hello head node creates a file share that hello child nodes can access if they are running under hello same auto-user account.</span></span> 

<span data-ttu-id="62af6-191">Aşağıdaki kod parçacığını hello hello otomatik kullanıcının kapsam toopool kapsamını bir görev için Batch .NET içinde ayarlar.</span><span class="sxs-lookup"><span data-stu-id="62af6-191">hello following code snippet sets hello auto-user's scope toopool scope for a task in Batch .NET.</span></span> <span data-ttu-id="62af6-192">Merhaba görev hello standart havuzu genelinde otomatik-kullanıcı hesabı altında çalışır şekilde hello ayrıcalık düzeyi atlandı.</span><span class="sxs-lookup"><span data-stu-id="62af6-192">hello elevation level is omitted, so hello task runs under hello standard pool-wide auto-user account.</span></span>

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(scope: AutoUserScope.Pool));
```

## <a name="named-user-accounts"></a><span data-ttu-id="62af6-193">Adlı kullanıcı hesapları</span><span class="sxs-lookup"><span data-stu-id="62af6-193">Named user accounts</span></span>

<span data-ttu-id="62af6-194">Bir havuz oluşturduğunuzda, adlandırılmış kullanıcı hesapları tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="62af6-194">You can define named user accounts when you create a pool.</span></span> <span data-ttu-id="62af6-195">Adlı bir kullanıcı hesabı adı ve sağladığınız parola sahiptir.</span><span class="sxs-lookup"><span data-stu-id="62af6-195">A named user account has a name and password that you provide.</span></span> <span data-ttu-id="62af6-196">Adlı bir kullanıcı hesabı için hello ayrıcalık düzeyi belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="62af6-196">You can specify hello elevation level for a named user account.</span></span> <span data-ttu-id="62af6-197">Linux düğümleri için bir SSH özel anahtarı da sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="62af6-197">For Linux nodes, you can also provide an SSH private key.</span></span>

<span data-ttu-id="62af6-198">Merhaba havuzundaki tüm düğümlerde adlı bir kullanıcı hesabı var ve bu düğümlerde çalışan kullanılabilir tooall görevleri.</span><span class="sxs-lookup"><span data-stu-id="62af6-198">A named user account exists on all nodes in hello pool and is available tooall tasks running on those nodes.</span></span> <span data-ttu-id="62af6-199">Adlandırılmış kullanıcılar bir havuz için herhangi bir sayıda tanımlayabilir.</span><span class="sxs-lookup"><span data-stu-id="62af6-199">You may define any number of named users for a pool.</span></span> <span data-ttu-id="62af6-200">Bir görevi veya görev koleksiyon eklediğinizde hello havuzunda tanımlanan kullanıcı hesapları adlı hello birini hello görev çalıştığı belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="62af6-200">When you add a task or task collection, you can specify that hello task runs under one of hello named user accounts defined on hello pool.</span></span>

<span data-ttu-id="62af6-201">Adlı bir kullanıcı hesabı yararlıdır toorun istediğinizde işteki tüm görevler altında hello aynı kullanıcı hesabı, ancak diğer işleri Merhaba, çalışan görevleri birbirlerinden ayrı tutmak aynı anda.</span><span class="sxs-lookup"><span data-stu-id="62af6-201">A named user account is useful when you want toorun all tasks in a job under hello same user account, but isolate them from tasks running in other jobs at hello same time.</span></span> <span data-ttu-id="62af6-202">Örneğin, her iş için adlandırılmış bir kullanıcı oluşturun ve her iş görevlerinin bu adlı bir kullanıcı hesabı altında çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="62af6-202">For example, you can create a named user for each job, and run each job's tasks under that named user account.</span></span> <span data-ttu-id="62af6-203">Her bir iş, daha sonra kendi görevleri ile ancak diğer işlerin görevleri bir gizlilik paylaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="62af6-203">Each job can then share a secret with its own tasks, but not with tasks running in other jobs.</span></span>

<span data-ttu-id="62af6-204">Adlı kullanıcı hesabı toorun dosya paylaşımları gibi dış kaynaklara izinlerini ayarlar, bir görev de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="62af6-204">You can also use a named user account toorun a task that sets permissions on external resources such as file shares.</span></span> <span data-ttu-id="62af6-205">Adlı bir kullanıcı hesabı ile Merhaba kullanıcı kimliğini denetlemek ve bu kullanıcı kimliğini tooset izinleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="62af6-205">With a named user account, you control hello user identity and can use that user identity tooset permissions.</span></span>  

<span data-ttu-id="62af6-206">Adlı kullanıcı hesapları parola daha az SSH Linux düğümleri arasında sağlar.</span><span class="sxs-lookup"><span data-stu-id="62af6-206">Named user accounts enable password-less SSH between Linux nodes.</span></span> <span data-ttu-id="62af6-207">Toorun çok örnekli görevler gereken Linux düğümleri adlı bir kullanıcı hesabı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="62af6-207">You can use a named user account with Linux nodes that need toorun multi-instance tasks.</span></span> <span data-ttu-id="62af6-208">Merhaba havuzdaki her düğüme görevleri hello tüm havuzu üzerinde tanımlı bir kullanıcı hesabı altında çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="62af6-208">Each node in hello pool can run tasks under a user account defined on hello whole pool.</span></span> <span data-ttu-id="62af6-209">Çok örnekli görevler hakkında daha fazla bilgi için bkz: [çoklu kullanmak\-örneği görevleri toorun MPI uygulamaları](batch-mpi.md).</span><span class="sxs-lookup"><span data-stu-id="62af6-209">For more information about multi-instance tasks, see [Use multi\-instance tasks toorun MPI applications](batch-mpi.md).</span></span>

### <a name="create-named-user-accounts"></a><span data-ttu-id="62af6-210">Adlı kullanıcı hesapları oluşturma</span><span class="sxs-lookup"><span data-stu-id="62af6-210">Create named user accounts</span></span>

<span data-ttu-id="62af6-211">Toplu işlem, kullanıcı hesaplarında adlı toocreate kullanıcı hesapları toohello havuzu koleksiyonu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="62af6-211">toocreate named user accounts in Batch, add a collection of user accounts toohello pool.</span></span> <span data-ttu-id="62af6-212">Merhaba aşağıdaki kod parçacıkları nasıl toocreate kullanıcı hesaplarında .NET, Java ve Python adlı gösterir.</span><span class="sxs-lookup"><span data-stu-id="62af6-212">hello following code snippets show how toocreate named user accounts in .NET, Java, and Python.</span></span> <span data-ttu-id="62af6-213">Bu kod parçacıkları Göster nasıl toocreate yönetici ve bir havuz hesaplarında adlı yönetici olmayan.</span><span class="sxs-lookup"><span data-stu-id="62af6-213">These code snippets show how toocreate both admin and non-admin named accounts on a pool.</span></span> <span data-ttu-id="62af6-214">Hello örnekler hello bulut hizmet yapılandırması'nı kullanarak havuzları oluşturma, ancak aynı hello Sanal Makine Yapılandırması'nı kullanarak bir Windows veya Linux havuzu oluştururken yaklaşımını hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="62af6-214">hello examples create pools using hello cloud service configuration, but you use hello same approach when creating a Windows or Linux pool using hello virtual machine configuration.</span></span>

#### <a name="batch-net-example-windows"></a><span data-ttu-id="62af6-215">Batch .NET örnek (Windows)</span><span class="sxs-lookup"><span data-stu-id="62af6-215">Batch .NET example (Windows)</span></span>

```csharp
CloudPool pool = null;
Console.WriteLine("Creating pool [{0}]...", poolId);

// Create a pool using hello cloud service configuration.
pool = batchClient.PoolOperations.CreatePool(
    poolId: poolId,
    targetDedicatedComputeNodes: 3,                                                         
    virtualMachineSize: "small",                                                
    cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "5"));   

// Add named user accounts.
pool.UserAccounts = new List<UserAccount>
{
    new UserAccount("adminUser", "xyz123", ElevationLevel.Admin),
    new UserAccount("nonAdminUser", "123xyz", ElevationLevel.NonAdmin),
};

// Commit hello pool.
await pool.CommitAsync();
```

#### <a name="batch-net-example-linux"></a><span data-ttu-id="62af6-216">Batch .NET örnek (Linux)</span><span class="sxs-lookup"><span data-stu-id="62af6-216">Batch .NET example (Linux)</span></span>

```csharp
CloudPool pool = null;

// Obtain a collection of all available node agent SKUs.
List<NodeAgentSku> nodeAgentSkus =
    batchClient.PoolOperations.ListNodeAgentSkus().ToList();

// Define a delegate specifying properties of hello VM image toouse.
Func<ImageReference, bool> isUbuntu1404 = imageRef =>
    imageRef.Publisher == "Canonical" &&
    imageRef.Offer == "UbuntuServer" &&
    imageRef.Sku.Contains("14.04");

// Obtain hello first node agent SKU in hello collection that matches
// Ubuntu Server 14.04. 
NodeAgentSku ubuntuAgentSku = nodeAgentSkus.First(sku =>
    sku.VerifiedImageReferences.Any(isUbuntu1404));

// Select an ImageReference from those available for node agent.
ImageReference imageReference =
    ubuntuAgentSku.VerifiedImageReferences.First(isUbuntu1404);

// Create hello virtual machine configuration toouse toocreate hello pool.
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration(imageReference, ubuntuAgentSku.Id);

Console.WriteLine("Creating pool [{0}]...", poolId);

// Create hello unbound pool.
pool = batchClient.PoolOperations.CreatePool(
    poolId: poolId,
    targetDedicatedComputeNodes: 3,                                             
    virtualMachineSize: "Standard_A1",                                      
    virtualMachineConfiguration: virtualMachineConfiguration);                  

// Add named user accounts.
pool.UserAccounts = new List<UserAccount>
{
    new UserAccount(
        name: "adminUser",
        password: "xyz123",
        elevationLevel: ElevationLevel.Admin,
        linuxUserConfiguration: new LinuxUserConfiguration(
            uid: 12345,
            gid: 98765,
            sshPrivateKey: new Guid().ToString()
            )),
    new UserAccount(
        name: "nonAdminUser",
        password: "123xyz",
        elevationLevel: ElevationLevel.NonAdmin,
        linuxUserConfiguration: new LinuxUserConfiguration(
            uid: 45678,
            gid: 98765,
            sshPrivateKey: new Guid().ToString()
            )),
};

// Commit hello pool.
await pool.CommitAsync();
```


#### <a name="batch-java-example"></a><span data-ttu-id="62af6-217">Batch Java örneği</span><span class="sxs-lookup"><span data-stu-id="62af6-217">Batch Java example</span></span>

```java
List<UserAccount> userList = new ArrayList<>();
userList.add(new UserAccount().withName(adminUserAccountName).withPassword(adminPassword).withElevationLevel(ElevationLevel.ADMIN));
userList.add(new UserAccount().withName(nonAdminUserAccountName).withPassword(nonAdminPassword).withElevationLevel(ElevationLevel.NONADMIN));
PoolAddParameter addParameter = new PoolAddParameter()
        .withId(poolId)
        .withTargetDedicatedNodes(POOL_VM_COUNT)
        .withVmSize(POOL_VM_SIZE)
        .withCloudServiceConfiguration(configuration)
        .withUserAccounts(userList);
batchClient.poolOperations().createPool(addParameter);
```

#### <a name="batch-python-example"></a><span data-ttu-id="62af6-218">Batch Python örneği</span><span class="sxs-lookup"><span data-stu-id="62af6-218">Batch Python example</span></span>

```python
users = [
    batchmodels.UserAccount(
        name='pool-admin',
        password='******',
        elevation_level=batchmodels.ElevationLevel.admin)
    batchmodels.UserAccount(
        name='pool-nonadmin',
        password='******',
        elevation_level=batchmodels.ElevationLevel.nonadmin)
]
pool = batchmodels.PoolAddParameter(
    id=pool_id,
    user_accounts=users,
    virtual_machine_configuration=batchmodels.VirtualMachineConfiguration(
        image_reference=image_ref_to_use,
        node_agent_sku_id=sku_to_use),
    vm_size=vm_size,
    target_dedicated=vm_count)
batch_client.pool.add(pool)
```

### <a name="run-a-task-under-a-named-user-account-with-elevated-access"></a><span data-ttu-id="62af6-219">Yükseltilmiş erişimle görevi adlı bir kullanıcı hesabı altında çalıştırma</span><span class="sxs-lookup"><span data-stu-id="62af6-219">Run a task under a named user account with elevated access</span></span>

<span data-ttu-id="62af6-220">toorun bir görev bir yükseltilmiş kullanıcının, ayarlanmış hello görevi olarak **Userıdentity** ile oluşturulan kullanıcı hesabı adlı özellik tooa kendi **ElevationLevel** çok ayarlanan özelliği`Admin`.</span><span class="sxs-lookup"><span data-stu-id="62af6-220">toorun a task as an elevated user, set hello task's **UserIdentity** property tooa named user account that was created with its **ElevationLevel** property set too`Admin`.</span></span>

<span data-ttu-id="62af6-221">Bu kod parçacığını hello görev adlı bir kullanıcı hesabı altında çalışması gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="62af6-221">This code snippet specifies that hello task should run under a named user account.</span></span> <span data-ttu-id="62af6-222">Merhaba havuzu oluşturulduğunda bu adlı bir kullanıcı hesabı hello havuzunda tanımlandı.</span><span class="sxs-lookup"><span data-stu-id="62af6-222">This named user account was defined on hello pool when hello pool was created.</span></span> <span data-ttu-id="62af6-223">Bu durumda, kullanıcı hesabı adlı hello yönetici izinlerine sahip oluşturuldu:</span><span class="sxs-lookup"><span data-stu-id="62af6-223">In this case, hello named user account was created with admin permissions:</span></span>

```csharp
CloudTask task = new CloudTask("1", "cmd.exe /c echo 1");
task.UserIdentity = new UserIdentity(AdminUserAccountName);
```

## <a name="update-your-code-toohello-latest-batch-client-library"></a><span data-ttu-id="62af6-224">Kod toohello en son toplu istemci Kitaplığı ', güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="62af6-224">Update your code toohello latest Batch client library</span></span>

<span data-ttu-id="62af6-225">Merhaba Batch hizmeti sürümü 2017 01 01.4.0 tanıtır hello değiştirme önemli bir değişiklik, **runElevated** özelliği hello ile önceki sürümlerde kullanılabilir **Userıdentity** özelliği.</span><span class="sxs-lookup"><span data-stu-id="62af6-225">hello Batch service version 2017-01-01.4.0 introduces a breaking change, replacing hello **runElevated** property available in earlier versions with hello **userIdentity** property.</span></span> <span data-ttu-id="62af6-226">tabloları aşağıdaki Merhaba, eşleme bir basit tooupdate kodunuzu hello istemci kitaplıkları önceki sürümlerinden kullanabileceği sağlar.</span><span class="sxs-lookup"><span data-stu-id="62af6-226">hello following tables provide a simple mapping that you can use tooupdate your code from earlier versions of hello client libraries.</span></span>

### <a name="batch-net"></a><span data-ttu-id="62af6-227">Batch .NET</span><span class="sxs-lookup"><span data-stu-id="62af6-227">Batch .NET</span></span>

| <span data-ttu-id="62af6-228">Kodunuzu kullanıyorsa...</span><span class="sxs-lookup"><span data-stu-id="62af6-228">If your code uses...</span></span>                  | <span data-ttu-id="62af6-229">Buna güncelleştirme...</span><span class="sxs-lookup"><span data-stu-id="62af6-229">Update it to....</span></span>                                                                                                 |
|---------------------------------------|------------------------------------------------------------------------------------------------------------------|
| `CloudTask.RunElevated = true;`       | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin));`    |
| `CloudTask.RunElevated = false;`      | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.NonAdmin));` |
| <span data-ttu-id="62af6-230">`CloudTask.RunElevated`belirtilmemiş.</span><span class="sxs-lookup"><span data-stu-id="62af6-230">`CloudTask.RunElevated` not specified</span></span> | <span data-ttu-id="62af6-231">Güncelleştirme gerekmiyor</span><span class="sxs-lookup"><span data-stu-id="62af6-231">No update required</span></span>                                                                                               |

### <a name="batch-java"></a><span data-ttu-id="62af6-232">Batch Java</span><span class="sxs-lookup"><span data-stu-id="62af6-232">Batch Java</span></span>

| <span data-ttu-id="62af6-233">Kodunuzu kullanıyorsa...</span><span class="sxs-lookup"><span data-stu-id="62af6-233">If your code uses...</span></span>                      | <span data-ttu-id="62af6-234">Buna güncelleştirme...</span><span class="sxs-lookup"><span data-stu-id="62af6-234">Update it to....</span></span>                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `CloudTask.withRunElevated(true);`        | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.ADMIN));`    |
| `CloudTask.withRunElevated(false);`       | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.NONADMIN));` |
| <span data-ttu-id="62af6-235">`CloudTask.withRunElevated`belirtilmemiş.</span><span class="sxs-lookup"><span data-stu-id="62af6-235">`CloudTask.withRunElevated` not specified</span></span> | <span data-ttu-id="62af6-236">Güncelleştirme gerekmiyor</span><span class="sxs-lookup"><span data-stu-id="62af6-236">No update required</span></span>                                                                                                                     |

### <a name="batch-python"></a><span data-ttu-id="62af6-237">Batch Python</span><span class="sxs-lookup"><span data-stu-id="62af6-237">Batch Python</span></span>

| <span data-ttu-id="62af6-238">Kodunuzu kullanıyorsa...</span><span class="sxs-lookup"><span data-stu-id="62af6-238">If your code uses...</span></span>                      | <span data-ttu-id="62af6-239">Buna güncelleştirme...</span><span class="sxs-lookup"><span data-stu-id="62af6-239">Update it to....</span></span>                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `run_elevated=True`                       | <span data-ttu-id="62af6-240">`user_identity=user`, burada</span><span class="sxs-lookup"><span data-stu-id="62af6-240">`user_identity=user`, where</span></span> <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.admin)) `                |
| `run_elevated=False`                      | <span data-ttu-id="62af6-241">`user_identity=user`, burada</span><span class="sxs-lookup"><span data-stu-id="62af6-241">`user_identity=user`, where</span></span> <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.nonadmin)) `             |
| <span data-ttu-id="62af6-242">`run_elevated`belirtilmemiş.</span><span class="sxs-lookup"><span data-stu-id="62af6-242">`run_elevated` not specified</span></span> | <span data-ttu-id="62af6-243">Güncelleştirme gerekmiyor</span><span class="sxs-lookup"><span data-stu-id="62af6-243">No update required</span></span>                                                                                                                                  |


## <a name="next-steps"></a><span data-ttu-id="62af6-244">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="62af6-244">Next steps</span></span>

### <a name="batch-forum"></a><span data-ttu-id="62af6-245">Toplu işlem Forumu</span><span class="sxs-lookup"><span data-stu-id="62af6-245">Batch Forum</span></span>

<span data-ttu-id="62af6-246">Merhaba [Azure toplu işlem Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch) MSDN'de mükemmel toodiscuss toplu yerleştirin ve hello hizmeti hakkında soru sorun olduğunu.</span><span class="sxs-lookup"><span data-stu-id="62af6-246">hello [Azure Batch Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch) on MSDN is a great place toodiscuss Batch and ask questions about hello service.</span></span> <span data-ttu-id="62af6-247">HEAD üzerinde üzerinden faydalı sabitlenmiş gönderiler için ve Batch çözümlerinizi derleme sırasında çıktıkları anda sorularınızı gönderin.</span><span class="sxs-lookup"><span data-stu-id="62af6-247">Head on over for helpful pinned posts, and post your questions as they arise while you build your Batch solutions.</span></span>
