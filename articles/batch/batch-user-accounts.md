---
title: "Kullanıcı hesapları görevleri Azure Batch'de çalıştırma | Microsoft Docs"
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
ms.openlocfilehash: d408c0565c0ed81fc97cc2b3976a4fc233e31302
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="run-tasks-under-user-accounts-in-batch"></a><span data-ttu-id="94869-103">Toplu işlemde kullanıcı hesapları görevleri Çalıştır</span><span class="sxs-lookup"><span data-stu-id="94869-103">Run tasks under user accounts in Batch</span></span>

<span data-ttu-id="94869-104">Azure Batch görevinde her zaman bir kullanıcı hesabı altında çalışır.</span><span class="sxs-lookup"><span data-stu-id="94869-104">A task in Azure Batch always runs under a user account.</span></span> <span data-ttu-id="94869-105">Varsayılan olarak, standart kullanıcı hesapları, yönetici izinleri olmayan altında görevlerini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="94869-105">By default, tasks run under standard user accounts, without administrator permissions.</span></span> <span data-ttu-id="94869-106">Bu varsayılan kullanıcı hesabı ayarları genellikle yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="94869-106">These default user account settings are typically sufficient.</span></span> <span data-ttu-id="94869-107">Bazı senaryolarda, ancak altında çalıştırmak için bir görev istediğiniz kullanıcı hesabını yapılandırmak yararlı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="94869-107">For certain scenarios, however, it's useful to be able to configure the user account under which you want a task to run.</span></span> <span data-ttu-id="94869-108">Bu makalede, kullanıcı hesapları ve nasıl bunları senaryonuz için yapılandırabilirsiniz türleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="94869-108">This article discusses the types of user accounts and how you can configure them for your scenario.</span></span>

## <a name="types-of-user-accounts"></a><span data-ttu-id="94869-109">Kullanıcı hesabı türleri</span><span class="sxs-lookup"><span data-stu-id="94869-109">Types of user accounts</span></span>

<span data-ttu-id="94869-110">Azure toplu işlem, görevleri çalıştırmak için iki tür kullanıcı hesabı sağlar:</span><span class="sxs-lookup"><span data-stu-id="94869-110">Azure Batch provides two types of user accounts for running tasks:</span></span>

- <span data-ttu-id="94869-111">**Otomatik kullanıcı hesapları.**</span><span class="sxs-lookup"><span data-stu-id="94869-111">**Auto-user accounts.**</span></span> <span data-ttu-id="94869-112">Otomatik kullanıcı hesapları Batch hizmeti tarafından otomatik olarak oluşturulan yerleşik kullanıcı hesaplarıdır.</span><span class="sxs-lookup"><span data-stu-id="94869-112">Auto-user accounts are built-in user accounts that are created automatically by the Batch service.</span></span> <span data-ttu-id="94869-113">Varsayılan olarak, görevler bir otomatik kullanıcı hesabı altında çalışır.</span><span class="sxs-lookup"><span data-stu-id="94869-113">By default, tasks run under an auto-user account.</span></span> <span data-ttu-id="94869-114">Bir görev hangi otomatik bir kullanıcı hesabı altında çalışması gerektiğini belirtmek bir görev için otomatik kullanıcı belirtimi yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="94869-114">You can configure the auto-user specification for a task to indicate under which auto-user account a task should run.</span></span> <span data-ttu-id="94869-115">Otomatik kullanıcı belirtimi ayrıcalık düzeyinde ve kapsam görevin çalışacağını otomatik kullanıcı hesabının belirtmenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="94869-115">The auto-user specification allows you to specify the elevation level and scope of the auto-user account that will run the task.</span></span> 

- <span data-ttu-id="94869-116">**Adlı bir kullanıcı hesabı.**</span><span class="sxs-lookup"><span data-stu-id="94869-116">**A named user account.**</span></span> <span data-ttu-id="94869-117">Havuz oluşturduğunuzda havuz için bir veya daha fazla adlandırılmış kullanıcı hesapları belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="94869-117">You can specify one or more named user accounts for a pool when you create the pool.</span></span> <span data-ttu-id="94869-118">Her kullanıcı hesabı havuzunun her bir düğümde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="94869-118">Each user account is created on each node of the pool.</span></span> <span data-ttu-id="94869-119">Hesap adı yanı sıra, kullanıcı hesabının parolasını ayrıcalık düzeyi ve, Linux havuzları, SSH özel anahtar için belirtin.</span><span class="sxs-lookup"><span data-stu-id="94869-119">In addition to the account name, you specify the user account password, elevation level, and, for Linux pools, the SSH private key.</span></span> <span data-ttu-id="94869-120">Bir görev eklediğinizde, bu görev, altında çalışması gerektiğini adlı bir kullanıcı hesabı belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="94869-120">When you add a task, you can specify the named user account under which that task should run.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="94869-121">Batch hizmeti sürümü 2017 01 01.4.0 sürümünün çağırmak için kodunuzu güncelleştirin gerektiren önemli bir değişiklik tanıtır.</span><span class="sxs-lookup"><span data-stu-id="94869-121">The Batch service version 2017-01-01.4.0 introduces a breaking change that requires that you update your code to call that version.</span></span> <span data-ttu-id="94869-122">Geçirme koddan toplu daha eski bir sürümü olup olmadığını unutmayın **runElevated** özelliği REST API veya toplu istemci kitaplıkları artık desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="94869-122">If you are migrating code from an older version of Batch, note that the **runElevated** property is no longer supported in the REST API or Batch client libraries.</span></span> <span data-ttu-id="94869-123">Yeni **Userıdentity** ayrıcalık düzeyini belirtmek için bir görev özelliği.</span><span class="sxs-lookup"><span data-stu-id="94869-123">Use the new **userIdentity** property of a task to specify elevation level.</span></span> <span data-ttu-id="94869-124">Başlıklı bölüme bakın [en son toplu istemci Kitaplığı'na kodunuzu güncelleştirin](#update-your-code-to-the-latest-batch-client-library) istemci kitaplıklarından birini kullanıyorsanız, toplu kodunuzu güncelleştirmek için hızlı yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="94869-124">See the section titled [Update your code to the latest Batch client library](#update-your-code-to-the-latest-batch-client-library) for quick guidelines for updating your Batch code if you are using one of the client libraries.</span></span>
>
>

> [!NOTE] 
> <span data-ttu-id="94869-125">Bu makalede ele alınan kullanıcı hesapları Uzak Masaüstü Protokolü (RDP) veya güvenli Kabuk (SSH), güvenlik nedenleriyle desteklemez.</span><span class="sxs-lookup"><span data-stu-id="94869-125">The user accounts discussed in this article do not support Remote Desktop Protocol (RDP) or Secure Shell (SSH), for security reasons.</span></span> 
>
> <span data-ttu-id="94869-126">Linux sanal makine yapılandırması SSH yoluyla çalıştıran bir düğüme bağlanmak için bkz: [azure'da bir Linux VM için Uzak Masaüstü kullanım](../virtual-machines/virtual-machines-linux-use-remote-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="94869-126">To connect to a node running the Linux virtual machine configuration via SSH, see [Use Remote Desktop to a Linux VM in Azure](../virtual-machines/virtual-machines-linux-use-remote-desktop.md).</span></span> <span data-ttu-id="94869-127">RDP aracılığıyla Windows çalışan düğümlerine bağlanmak için bkz: [bir Windows Server VM Bağlan](../virtual-machines/windows/connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="94869-127">To connect to nodes running Windows via RDP, see [Connect to a Windows Server VM](../virtual-machines/windows/connect-logon.md).</span></span><br /><br />
> <span data-ttu-id="94869-128">RDP aracılığıyla bulut hizmeti yapılandırması çalıştıran bir düğüme bağlanmak için bkz: [bir rolde Azure bulut Hizmetleri için Uzak Masaüstü Bağlantısı etkinleştirmek](../cloud-services/cloud-services-role-enable-remote-desktop-new-portal.md).</span><span class="sxs-lookup"><span data-stu-id="94869-128">To connect to a node running the cloud service configuration via RDP, see [Enable Remote Desktop Connection for a Role in Azure Cloud Services](../cloud-services/cloud-services-role-enable-remote-desktop-new-portal.md).</span></span>
>
>

## <a name="user-account-access-to-files-and-directories"></a><span data-ttu-id="94869-129">Dosyalar ve dizinler için kullanıcı hesabı erişimi</span><span class="sxs-lookup"><span data-stu-id="94869-129">User account access to files and directories</span></span>

<span data-ttu-id="94869-130">Bir otomatik kullanıcı hesabı ve adlı bir kullanıcı hesabı görevin çalışma dizini, paylaşılan dizine ve çok örnekli görevler dizin okuma/yazma erişimi.</span><span class="sxs-lookup"><span data-stu-id="94869-130">Both an auto-user account and a named user account have read/write access to the task’s working directory, shared directory, and multi-instance tasks directory.</span></span> <span data-ttu-id="94869-131">Her iki hesap türü başlangıç ve iş hazırlama dizinlerinin okuma erişimi.</span><span class="sxs-lookup"><span data-stu-id="94869-131">Both types of accounts have read access to the startup and job preparation directories.</span></span>

<span data-ttu-id="94869-132">Bir görev, bir başlangıç görevi çalıştırmak için kullanılan aynı hesap altında çalışıyorsa, görev Başlat görev dizininde okuma-yazma erişimi vardır.</span><span class="sxs-lookup"><span data-stu-id="94869-132">If a task runs under the same account that was used for running a start task, the task has read-write access to the start task directory.</span></span> <span data-ttu-id="94869-133">Benzer şekilde, bir görev iş hazırlama görevi çalıştırmak için kullanılan aynı hesap altında çalışıyorsa, görev iş hazırlama görevi dizini okuma-yazma erişimi vardır.</span><span class="sxs-lookup"><span data-stu-id="94869-133">Similarly, if a task runs under the same account that was used for running a job preparation task, the task has read-write access to the job preparation task directory.</span></span> <span data-ttu-id="94869-134">Bir görev başlangıç görevi veya iş hazırlama görevi farklı bir hesap altında çalışıyorsa, görev yalnızca ilgili dizine okuma erişimi vardır.</span><span class="sxs-lookup"><span data-stu-id="94869-134">If a task runs under a different account than the start task or job preparation task, then the task has only read access to the respective directory.</span></span>

<span data-ttu-id="94869-135">Dosyalar ve dizinler görevden erişme hakkında daha fazla bilgi için bkz: [geliştirme büyük ölçekli paralel işlem çözümleri yığın](batch-api-basics.md#files-and-directories).</span><span class="sxs-lookup"><span data-stu-id="94869-135">For more information on accessing files and directories from a task, see [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md#files-and-directories).</span></span>

## <a name="elevated-access-for-tasks"></a><span data-ttu-id="94869-136">Görevler için yükseltilmiş erişim</span><span class="sxs-lookup"><span data-stu-id="94869-136">Elevated access for tasks</span></span> 

<span data-ttu-id="94869-137">Kullanıcı hesabının ayrıcalık düzeyi, bir görevin yükseltilmiş erişim ile çalışıp çalışmayacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="94869-137">The user account's elevation level indicates whether a task runs with elevated access.</span></span> <span data-ttu-id="94869-138">Bir otomatik kullanıcı hesabı ve adlı bir kullanıcı hesabı ile yükseltilmiş erişim çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="94869-138">Both an auto-user account and a named user account can run with elevated access.</span></span> <span data-ttu-id="94869-139">Ayrıcalık düzeyi için iki seçenek şunlardır:</span><span class="sxs-lookup"><span data-stu-id="94869-139">The two options for elevation level are:</span></span>

- <span data-ttu-id="94869-140">**NonAdmin:** yükseltilmiş erişimi olmayan standart bir kullanıcı olarak görev çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="94869-140">**NonAdmin:** The task runs as a standard user without elevated access.</span></span> <span data-ttu-id="94869-141">Toplu kullanıcı hesabı için varsayılan ayrıcalık düzeyi her zaman olduğu **NonAdmin**.</span><span class="sxs-lookup"><span data-stu-id="94869-141">The default elevation level for a Batch user account is always **NonAdmin**.</span></span>
- <span data-ttu-id="94869-142">**Yönetici:** görevi yükseltilmiş erişimi bir kullanıcı olarak çalışır ve tam yönetici izinlerine sahip çalışır.</span><span class="sxs-lookup"><span data-stu-id="94869-142">**Admin:** The task runs as a user with elevated access and operates with full Administrator permissions.</span></span> 

## <a name="auto-user-accounts"></a><span data-ttu-id="94869-143">Otomatik kullanıcı hesapları</span><span class="sxs-lookup"><span data-stu-id="94869-143">Auto-user accounts</span></span>

<span data-ttu-id="94869-144">Varsayılan olarak, görevler yükseltilmiş erişimi olmadan ve görev kapsamlı standart bir kullanıcı olarak bir otomatik kullanıcı hesabı altında toplu işlemde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="94869-144">By default, tasks run in Batch under an auto-user account, as a standard user without elevated access, and with task scope.</span></span> <span data-ttu-id="94869-145">Otomatik kullanıcı belirtimi görev kapsam için yapılandırıldığında, Batch hizmeti yalnızca bu görev için bir otomatik kullanıcı hesabı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="94869-145">When the auto-user specification is configured for task scope, the Batch service creates an auto-user account for that task only.</span></span>

<span data-ttu-id="94869-146">Görev kapsamına havuzu kapsam alternatiftir.</span><span class="sxs-lookup"><span data-stu-id="94869-146">The alternative to task scope is pool scope.</span></span> <span data-ttu-id="94869-147">Bir görev için otomatik kullanıcı belirtimi havuzu kapsam için yapılandırıldığında, görev havuzdaki herhangi bir görev için kullanılabilir olan bir otomatik kullanıcı hesabı altında çalışır.</span><span class="sxs-lookup"><span data-stu-id="94869-147">When the auto-user specification for a task is configured for pool scope, the task runs under an auto-user account that is available to any task in the pool.</span></span> <span data-ttu-id="94869-148">Havuz kapsamı hakkında daha fazla bilgi için başlıklı bölüme bakın [havuzu kapsamlı otomatik kullanıcı olarak bir görevi çalıştırmayı](#run-a-task-as-the-autouser-with-pool-scope).</span><span class="sxs-lookup"><span data-stu-id="94869-148">For more information about pool scope, see the section titled [Run a task as the auto-user with pool scope](#run-a-task-as-the-autouser-with-pool-scope).</span></span>   

<span data-ttu-id="94869-149">Varsayılan kapsamı, Windows ve Linux düğümlerinde farklıdır:</span><span class="sxs-lookup"><span data-stu-id="94869-149">The default scope is different on Windows and Linux nodes:</span></span>

- <span data-ttu-id="94869-150">Windows düğümlerinde görevler varsayılan olarak görev kapsam altında çalışır.</span><span class="sxs-lookup"><span data-stu-id="94869-150">On Windows nodes, tasks run under task scope by default.</span></span>
- <span data-ttu-id="94869-151">Linux düğümleri havuzu kapsam altında her zaman çalışır.</span><span class="sxs-lookup"><span data-stu-id="94869-151">Linux nodes always run under pool scope.</span></span>

<span data-ttu-id="94869-152">Her biri benzersiz otomatik kullanıcı hesabına karşılık gelen otomatik kullanıcı belirtimi için dört olası yapılandırmaları vardır:</span><span class="sxs-lookup"><span data-stu-id="94869-152">There are four possible configurations for the auto-user specification, each of which corresponds to a unique auto-user account:</span></span>

- <span data-ttu-id="94869-153">Yönetici olmayan erişim görev kapsamlı (varsayılan otomatik kullanıcı belirtimi)</span><span class="sxs-lookup"><span data-stu-id="94869-153">Non-admin access with task scope (the default auto-user specification)</span></span>
- <span data-ttu-id="94869-154">Görev kapsamlı yönetici (yükseltilmiş) erişimi</span><span class="sxs-lookup"><span data-stu-id="94869-154">Admin (elevated) access with task scope</span></span>
- <span data-ttu-id="94869-155">Havuz kapsamlı yönetici olmayan erişim</span><span class="sxs-lookup"><span data-stu-id="94869-155">Non-admin access with pool scope</span></span>
- <span data-ttu-id="94869-156">Havuz kapsamlı yönetici erişimi</span><span class="sxs-lookup"><span data-stu-id="94869-156">Admin access with pool scope</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="94869-157">Görev kapsam altında çalışan görevler gerçek diğer görevler için bir düğümde erişimi.</span><span class="sxs-lookup"><span data-stu-id="94869-157">Tasks running under task scope do not have de facto access to other tasks on a node.</span></span> <span data-ttu-id="94869-158">Ancak, kötü niyetli bir kullanıcı hesabı erişimi olan yönetici ayrıcalıklarıyla çalıştırır ve diğer görev dizinleri erişen bir görev göndererek bu kısıtlamaya işe yarayabilir.</span><span class="sxs-lookup"><span data-stu-id="94869-158">However, a malicious user with access to the account could work around this restriction by submitting a task that runs with administrator privileges and accesses other task directories.</span></span> <span data-ttu-id="94869-159">Kötü niyetli bir kullanıcı, bir düğüme bağlanmak için RDP veya SSH da kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="94869-159">A malicious user could also use RDP or SSH to connect to a node.</span></span> <span data-ttu-id="94869-160">Böyle bir senaryo önlemek için Batch hesabı anahtarları erişimi korumak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="94869-160">It's important to protect access to your Batch account keys to prevent such a scenario.</span></span> <span data-ttu-id="94869-161">Hesabınızı tehlikeye şüpheleniyorsanız, anahtarlarınızı yeniden emin olun.</span><span class="sxs-lookup"><span data-stu-id="94869-161">If you suspect your account may have been compromised, be sure to regenerate your keys.</span></span>
>
>

### <a name="run-a-task-as-an-auto-user-with-elevated-access"></a><span data-ttu-id="94869-162">Yükseltilmiş erişimi olan bir otomatik kullanıcı olarak bir görevi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="94869-162">Run a task as an auto-user with elevated access</span></span>

<span data-ttu-id="94869-163">Yükseltilmiş erişimi bir görev çalıştırmanız gerektiğinde yönetici ayrıcalıkları otomatik kullanıcı belirtimi yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="94869-163">You can configure the auto-user specification for administrator privileges when you need to run a task with elevated access.</span></span> <span data-ttu-id="94869-164">Örneğin, bir başlangıç görevi yazılım düğümüne yüklemek için yükseltilmiş erişmeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="94869-164">For example, a start task may need elevated access to install software on the node.</span></span>

> [!NOTE] 
> <span data-ttu-id="94869-165">Genel olarak, yalnızca gerekli olduğunda yükseltilmiş erişimi kullanmak en iyisidir.</span><span class="sxs-lookup"><span data-stu-id="94869-165">In general, it's best to use elevated access only when necessary.</span></span> <span data-ttu-id="94869-166">En iyi yöntemler, istenen sonucu elde etmek gerekli en düşük ayrıcalık verilmesi önerilir.</span><span class="sxs-lookup"><span data-stu-id="94869-166">Best practices recommend granting the minimum privilege necessary to achieve the desired outcome.</span></span> <span data-ttu-id="94869-167">Örneğin, bir başlangıç görevi geçerli kullanıcıya yönelik yazılımları yerine tüm kullanıcılar için yüklerse görevlere yükseltilmiş erişimi vermekten kaçının mümkün olabilir.</span><span class="sxs-lookup"><span data-stu-id="94869-167">For example, if a start task installs software for the current user, instead of for all users, you may be able to avoid granting elevated access to tasks.</span></span> <span data-ttu-id="94869-168">Başlangıç görevi de dahil olmak üzere aynı hesabı altında çalıştırmak için gereken tüm görevler için havuz kapsamı ve yönetici olmayan erişim için otomatik kullanıcı belirtimi yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="94869-168">You can configure the auto-user specification for pool scope and non-admin access for all tasks that need to run under the same account, including the start task.</span></span> 
>
>

<span data-ttu-id="94869-169">Aşağıdaki kod parçacıkları, otomatik kullanıcı belirtimine yapılandırılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="94869-169">The following code snippets show how to configure the auto-user specification.</span></span> <span data-ttu-id="94869-170">Örnekler ayrıcalık düzeyini set `Admin` ve kapsamını `Task`.</span><span class="sxs-lookup"><span data-stu-id="94869-170">The examples set the elevation level to `Admin` and the scope to `Task`.</span></span> <span data-ttu-id="94869-171">Görev kapsamı varsayılan ayar, ancak örnek açısından buraya dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="94869-171">Task scope is the default setting, but is included here for the sake of example.</span></span>

#### <a name="batch-net"></a><span data-ttu-id="94869-172">Batch .NET</span><span class="sxs-lookup"><span data-stu-id="94869-172">Batch .NET</span></span>

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin, scope: AutoUserScope.Task));
```
#### <a name="batch-java"></a><span data-ttu-id="94869-173">Batch Java</span><span class="sxs-lookup"><span data-stu-id="94869-173">Batch Java</span></span>

```java
taskToAdd.withId(taskId)
        .withUserIdentity(new UserIdentity()
            .withAutoUser(new AutoUserSpecification()
                .withElevationLevel(ElevationLevel.ADMIN))
                .withScope(AutoUserScope.TASK));
        .withCommandLine("cmd /c echo hello");                        
```

#### <a name="batch-python"></a><span data-ttu-id="94869-174">Batch Python</span><span class="sxs-lookup"><span data-stu-id="94869-174">Batch Python</span></span>

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

### <a name="run-a-task-as-an-auto-user-with-pool-scope"></a><span data-ttu-id="94869-175">Otomatik kullanıcı havuzu kapsamlı olarak bir görevi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="94869-175">Run a task as an auto-user with pool scope</span></span>

<span data-ttu-id="94869-176">Bir düğüm sağlandığında, iki havuzu genelinde otomatik-kullanıcı hesapları havuzu, yükseltilmiş erişim biriyle ve yükseltilmiş erişimi olmadan bir içindeki her bir düğümde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="94869-176">When a node is provisioned, two pool-wide auto-user accounts are created on each node in the pool, one with elevated access, and one without elevated access.</span></span> <span data-ttu-id="94869-177">Belirli bir görev için havuz kapsamına otomatik kullanıcının kapsamı ayarlama, bu iki havuzu genelinde otomatik-kullanıcı hesaplarından birini altında görev çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="94869-177">Setting the auto-user's scope to pool scope for a given task runs the task under one of these two pool-wide auto-user accounts.</span></span> 

<span data-ttu-id="94869-178">Ne zaman otomatik-kullanıcı, aynı havuz genelinde otomatik-kullanıcı hesabı altında çalışacak yönetici erişimi olan çalışan tüm görevler için havuz kapsam belirtin.</span><span class="sxs-lookup"><span data-stu-id="94869-178">When you specify pool scope for the auto-user, all tasks that run with administrator access run under the same pool-wide auto-user account.</span></span> <span data-ttu-id="94869-179">Benzer şekilde, yönetici izinleri olmadan çalışan görevler de tek havuzu genelinde otomatik-kullanıcı hesabı altında çalışır.</span><span class="sxs-lookup"><span data-stu-id="94869-179">Similarly, tasks that run without administrator permissions also run under a single pool-wide auto-user account.</span></span> 

> [!NOTE] 
> <span data-ttu-id="94869-180">İki havuzu genelinde otomatik-kullanıcı hesapları ayrı hesaplarıdır.</span><span class="sxs-lookup"><span data-stu-id="94869-180">The two pool-wide auto-user accounts are separate accounts.</span></span> <span data-ttu-id="94869-181">Havuzu genelinde yönetici hesabı altında çalışan görevler standart hesap altında ve tersi yönde çalışan görevler ile verileri paylaşamaz.</span><span class="sxs-lookup"><span data-stu-id="94869-181">Tasks running under the pool-wide administrative account cannot share data with tasks running under the standard account, and vice versa.</span></span> 
>
>

<span data-ttu-id="94869-182">Aynı otomatik kullanıcı hesabı altında çalışan yararınıza görevleri aynı düğüm üzerinde çalışan diğer görevleri ile verileri paylaşamaz olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="94869-182">The advantage to running under the same auto-user account is that tasks are able to share data with other tasks running on the same node.</span></span>

<span data-ttu-id="94869-183">Çalışan görevlerin iki havuzu genelinde otomatik-kullanıcı hesaplarından birini altında yararlı olduğu bir senaryo gizli görevler arasında paylaşımıdır.</span><span class="sxs-lookup"><span data-stu-id="94869-183">Sharing secrets between tasks is one scenario where running tasks under one of the two pool-wide auto-user accounts is useful.</span></span> <span data-ttu-id="94869-184">Örneğin, diğer görevleri kullanabilirsiniz düğüm üzerine bir gizlilik sağlamak bir başlangıç görevi gerektiğini varsayalım.</span><span class="sxs-lookup"><span data-stu-id="94869-184">For example, suppose a start task needs to provision a secret onto the node that other tasks can use.</span></span> <span data-ttu-id="94869-185">Windows Data Protection API (DPAPI) kullanabilirsiniz, ancak yönetici ayrıcalıkları gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="94869-185">You could use the Windows Data Protection API (DPAPI), but it requires administrator privileges.</span></span> <span data-ttu-id="94869-186">Bunun yerine, gizli kullanıcı düzeyinde koruyabilir.</span><span class="sxs-lookup"><span data-stu-id="94869-186">Instead, you can protect the secret at the user level.</span></span> <span data-ttu-id="94869-187">Aynı kullanıcı hesabı altında çalışan görevler yükseltilmiş erişimi olmadan gizli erişebilir.</span><span class="sxs-lookup"><span data-stu-id="94869-187">Tasks running under the same user account can access the secret without elevated access.</span></span>

<span data-ttu-id="94869-188">Başka bir senaryo havuzu kapsamlı bir otomatik kullanıcı hesabı altında görevleri çalıştırmak istediğiniz bir ileti geçirme arabirimi (MPI) dosya paylaşımıdır.</span><span class="sxs-lookup"><span data-stu-id="94869-188">Another scenario where you may want to run tasks under an auto-user account with pool scope is a Message Passing Interface (MPI) file share.</span></span> <span data-ttu-id="94869-189">Bir MPI dosya paylaşımı, MPI görev düğümler aynı dosya verileri üzerinde çalışması gereken yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="94869-189">An MPI file share is useful when the nodes in the MPI task need to work on the same file data.</span></span> <span data-ttu-id="94869-190">Baş düğüm aynı otomatik kullanıcı hesabı altında çalışıyorsa, alt düğümleri erişebileceği bir dosya paylaşımı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="94869-190">The head node creates a file share that the child nodes can access if they are running under the same auto-user account.</span></span> 

<span data-ttu-id="94869-191">Aşağıdaki kod parçacığını otomatik kullanıcının kapsam Batch .NET içinde bir görev için havuz kapsamı için ayarlar.</span><span class="sxs-lookup"><span data-stu-id="94869-191">The following code snippet sets the auto-user's scope to pool scope for a task in Batch .NET.</span></span> <span data-ttu-id="94869-192">Görev standart havuzu genelinde otomatik-kullanıcı hesabı altında çalışan şekilde ayrıcalık düzeyi atlandı.</span><span class="sxs-lookup"><span data-stu-id="94869-192">The elevation level is omitted, so the task runs under the standard pool-wide auto-user account.</span></span>

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(scope: AutoUserScope.Pool));
```

## <a name="named-user-accounts"></a><span data-ttu-id="94869-193">Adlı kullanıcı hesapları</span><span class="sxs-lookup"><span data-stu-id="94869-193">Named user accounts</span></span>

<span data-ttu-id="94869-194">Bir havuz oluşturduğunuzda, adlandırılmış kullanıcı hesapları tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="94869-194">You can define named user accounts when you create a pool.</span></span> <span data-ttu-id="94869-195">Adlı bir kullanıcı hesabı adı ve sağladığınız parola sahiptir.</span><span class="sxs-lookup"><span data-stu-id="94869-195">A named user account has a name and password that you provide.</span></span> <span data-ttu-id="94869-196">Adlı bir kullanıcı hesabı için ayrıcalık düzeyi belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="94869-196">You can specify the elevation level for a named user account.</span></span> <span data-ttu-id="94869-197">Linux düğümleri için bir SSH özel anahtarı da sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="94869-197">For Linux nodes, you can also provide an SSH private key.</span></span>

<span data-ttu-id="94869-198">Adlı bir kullanıcı hesabı havuzdaki tüm düğümlerde var ve bu düğümler üzerinde çalışan tüm görevler için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="94869-198">A named user account exists on all nodes in the pool and is available to all tasks running on those nodes.</span></span> <span data-ttu-id="94869-199">Adlandırılmış kullanıcılar bir havuz için herhangi bir sayıda tanımlayabilir.</span><span class="sxs-lookup"><span data-stu-id="94869-199">You may define any number of named users for a pool.</span></span> <span data-ttu-id="94869-200">Bir görevi veya görev koleksiyonu eklediğinizde, görevin havuzunda tanımlanan adlı kullanıcı hesaplarından birini altında çalıştığı belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="94869-200">When you add a task or task collection, you can specify that the task runs under one of the named user accounts defined on the pool.</span></span>

<span data-ttu-id="94869-201">Adlı bir kullanıcı hesabı, aynı kullanıcı hesabı altında bir işteki tüm görevler çalıştırabilir, ancak diğer işleri aynı anda çalışan görevleri birbirlerinden ayrı tutmak istediğiniz yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="94869-201">A named user account is useful when you want to run all tasks in a job under the same user account, but isolate them from tasks running in other jobs at the same time.</span></span> <span data-ttu-id="94869-202">Örneğin, her iş için adlandırılmış bir kullanıcı oluşturun ve her iş görevlerinin bu adlı bir kullanıcı hesabı altında çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="94869-202">For example, you can create a named user for each job, and run each job's tasks under that named user account.</span></span> <span data-ttu-id="94869-203">Her bir iş, daha sonra kendi görevleri ile ancak diğer işlerin görevleri bir gizlilik paylaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="94869-203">Each job can then share a secret with its own tasks, but not with tasks running in other jobs.</span></span>

<span data-ttu-id="94869-204">Adlı bir kullanıcı hesabı, dosya paylaşımları gibi dış kaynaklar üzerinde izinlerini ayarlar bir görevi çalıştırmak için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="94869-204">You can also use a named user account to run a task that sets permissions on external resources such as file shares.</span></span> <span data-ttu-id="94869-205">Adlı bir kullanıcı hesabı ile kullanıcı kimliğini denetlemek ve kullanıcı kimliği izinlerini ayarlamak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="94869-205">With a named user account, you control the user identity and can use that user identity to set permissions.</span></span>  

<span data-ttu-id="94869-206">Adlı kullanıcı hesapları parola daha az SSH Linux düğümleri arasında sağlar.</span><span class="sxs-lookup"><span data-stu-id="94869-206">Named user accounts enable password-less SSH between Linux nodes.</span></span> <span data-ttu-id="94869-207">Çok örnekli görevleri çalıştırmak için gereken Linux düğümleri adlı bir kullanıcı hesabı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="94869-207">You can use a named user account with Linux nodes that need to run multi-instance tasks.</span></span> <span data-ttu-id="94869-208">Havuzdaki her düğüme görevleri tüm havuzu üzerinde tanımlı bir kullanıcı hesabı altında çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="94869-208">Each node in the pool can run tasks under a user account defined on the whole pool.</span></span> <span data-ttu-id="94869-209">Çok örnekli görevler hakkında daha fazla bilgi için bkz: [çoklu kullanmak\-örneği MPI uygulamaları çalıştırmak için görevleri](batch-mpi.md).</span><span class="sxs-lookup"><span data-stu-id="94869-209">For more information about multi-instance tasks, see [Use multi\-instance tasks to run MPI applications](batch-mpi.md).</span></span>

### <a name="create-named-user-accounts"></a><span data-ttu-id="94869-210">Adlı kullanıcı hesapları oluşturma</span><span class="sxs-lookup"><span data-stu-id="94869-210">Create named user accounts</span></span>

<span data-ttu-id="94869-211">Toplu işlemde adlı kullanıcı hesaplarını oluşturmak için kullanıcı hesapları topluluğu havuzuna ekleyin.</span><span class="sxs-lookup"><span data-stu-id="94869-211">To create named user accounts in Batch, add a collection of user accounts to the pool.</span></span> <span data-ttu-id="94869-212">Aşağıdaki kod parçacıkları .NET, Java ve Python adlandırılmış kullanıcı hesaplarını oluşturmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="94869-212">The following code snippets show how to create named user accounts in .NET, Java, and Python.</span></span> <span data-ttu-id="94869-213">Bu kod parçacıkları yönetici ve bir havuz hesaplarında adlı yönetici olmayan nasıl oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="94869-213">These code snippets show how to create both admin and non-admin named accounts on a pool.</span></span> <span data-ttu-id="94869-214">Bulut Hizmeti Yapılandırması'nı kullanarak havuzları örnekleri oluşturma, ancak sanal makine Yapılandırması'nı kullanarak bir Windows veya Linux havuzu oluştururken aynı yaklaşımı kullanın.</span><span class="sxs-lookup"><span data-stu-id="94869-214">The examples create pools using the cloud service configuration, but you use the same approach when creating a Windows or Linux pool using the virtual machine configuration.</span></span>

#### <a name="batch-net-example-windows"></a><span data-ttu-id="94869-215">Batch .NET örnek (Windows)</span><span class="sxs-lookup"><span data-stu-id="94869-215">Batch .NET example (Windows)</span></span>

```csharp
CloudPool pool = null;
Console.WriteLine("Creating pool [{0}]...", poolId);

// Create a pool using the cloud service configuration.
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

// Commit the pool.
await pool.CommitAsync();
```

#### <a name="batch-net-example-linux"></a><span data-ttu-id="94869-216">Batch .NET örnek (Linux)</span><span class="sxs-lookup"><span data-stu-id="94869-216">Batch .NET example (Linux)</span></span>

```csharp
CloudPool pool = null;

// Obtain a collection of all available node agent SKUs.
List<NodeAgentSku> nodeAgentSkus =
    batchClient.PoolOperations.ListNodeAgentSkus().ToList();

// Define a delegate specifying properties of the VM image to use.
Func<ImageReference, bool> isUbuntu1404 = imageRef =>
    imageRef.Publisher == "Canonical" &&
    imageRef.Offer == "UbuntuServer" &&
    imageRef.Sku.Contains("14.04");

// Obtain the first node agent SKU in the collection that matches
// Ubuntu Server 14.04. 
NodeAgentSku ubuntuAgentSku = nodeAgentSkus.First(sku =>
    sku.VerifiedImageReferences.Any(isUbuntu1404));

// Select an ImageReference from those available for node agent.
ImageReference imageReference =
    ubuntuAgentSku.VerifiedImageReferences.First(isUbuntu1404);

// Create the virtual machine configuration to use to create the pool.
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration(imageReference, ubuntuAgentSku.Id);

Console.WriteLine("Creating pool [{0}]...", poolId);

// Create the unbound pool.
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

// Commit the pool.
await pool.CommitAsync();
```


#### <a name="batch-java-example"></a><span data-ttu-id="94869-217">Batch Java örneği</span><span class="sxs-lookup"><span data-stu-id="94869-217">Batch Java example</span></span>

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

#### <a name="batch-python-example"></a><span data-ttu-id="94869-218">Batch Python örneği</span><span class="sxs-lookup"><span data-stu-id="94869-218">Batch Python example</span></span>

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

### <a name="run-a-task-under-a-named-user-account-with-elevated-access"></a><span data-ttu-id="94869-219">Yükseltilmiş erişimle görevi adlı bir kullanıcı hesabı altında çalıştırma</span><span class="sxs-lookup"><span data-stu-id="94869-219">Run a task under a named user account with elevated access</span></span>

<span data-ttu-id="94869-220">Görevin yükseltilmiş bir kullanıcı olarak bir görevi çalıştırmayı ayarlayın **Userıdentity** ile oluşturulmuş bir adlı bir kullanıcı hesabı özelliğine kendi **ElevationLevel** özelliğini `Admin`.</span><span class="sxs-lookup"><span data-stu-id="94869-220">To run a task as an elevated user, set the task's **UserIdentity** property to a named user account that was created with its **ElevationLevel** property set to `Admin`.</span></span>

<span data-ttu-id="94869-221">Bu kod parçacığını görev adlı bir kullanıcı hesabı altında çalışması gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="94869-221">This code snippet specifies that the task should run under a named user account.</span></span> <span data-ttu-id="94869-222">Havuz oluşturduğunuzda bu adlı bir kullanıcı hesabı havuzunda tanımlandı.</span><span class="sxs-lookup"><span data-stu-id="94869-222">This named user account was defined on the pool when the pool was created.</span></span> <span data-ttu-id="94869-223">Bu durumda, adlı bir kullanıcı hesabı yönetici izinlerine sahip oluşturuldu:</span><span class="sxs-lookup"><span data-stu-id="94869-223">In this case, the named user account was created with admin permissions:</span></span>

```csharp
CloudTask task = new CloudTask("1", "cmd.exe /c echo 1");
task.UserIdentity = new UserIdentity(AdminUserAccountName);
```

## <a name="update-your-code-to-the-latest-batch-client-library"></a><span data-ttu-id="94869-224">En son toplu istemci Kitaplığı'na kodunuzu güncelleştirin</span><span class="sxs-lookup"><span data-stu-id="94869-224">Update your code to the latest Batch client library</span></span>

<span data-ttu-id="94869-225">Batch hizmeti sürümü 2017 01 01.4.0 önemli bir değişiklik tanıtır değiştirme **runElevated** ile önceki sürümlerde kullanılabilir özellik **Userıdentity** özelliği.</span><span class="sxs-lookup"><span data-stu-id="94869-225">The Batch service version 2017-01-01.4.0 introduces a breaking change, replacing the **runElevated** property available in earlier versions with the **userIdentity** property.</span></span> <span data-ttu-id="94869-226">Aşağıdaki tablolar, kodunuzu istemci kitaplıkları önceki sürümlerinden güncelleştirmek için kullanabileceğiniz basit bir eşleme sağlar.</span><span class="sxs-lookup"><span data-stu-id="94869-226">The following tables provide a simple mapping that you can use to update your code from earlier versions of the client libraries.</span></span>

### <a name="batch-net"></a><span data-ttu-id="94869-227">Batch .NET</span><span class="sxs-lookup"><span data-stu-id="94869-227">Batch .NET</span></span>

| <span data-ttu-id="94869-228">Kodunuzu kullanıyorsa...</span><span class="sxs-lookup"><span data-stu-id="94869-228">If your code uses...</span></span>                  | <span data-ttu-id="94869-229">Buna güncelleştirme...</span><span class="sxs-lookup"><span data-stu-id="94869-229">Update it to....</span></span>                                                                                                 |
|---------------------------------------|------------------------------------------------------------------------------------------------------------------|
| `CloudTask.RunElevated = true;`       | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin));`    |
| `CloudTask.RunElevated = false;`      | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.NonAdmin));` |
| <span data-ttu-id="94869-230">`CloudTask.RunElevated`belirtilmemiş.</span><span class="sxs-lookup"><span data-stu-id="94869-230">`CloudTask.RunElevated` not specified</span></span> | <span data-ttu-id="94869-231">Güncelleştirme gerekmiyor</span><span class="sxs-lookup"><span data-stu-id="94869-231">No update required</span></span>                                                                                               |

### <a name="batch-java"></a><span data-ttu-id="94869-232">Batch Java</span><span class="sxs-lookup"><span data-stu-id="94869-232">Batch Java</span></span>

| <span data-ttu-id="94869-233">Kodunuzu kullanıyorsa...</span><span class="sxs-lookup"><span data-stu-id="94869-233">If your code uses...</span></span>                      | <span data-ttu-id="94869-234">Buna güncelleştirme...</span><span class="sxs-lookup"><span data-stu-id="94869-234">Update it to....</span></span>                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `CloudTask.withRunElevated(true);`        | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.ADMIN));`    |
| `CloudTask.withRunElevated(false);`       | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.NONADMIN));` |
| <span data-ttu-id="94869-235">`CloudTask.withRunElevated`belirtilmemiş.</span><span class="sxs-lookup"><span data-stu-id="94869-235">`CloudTask.withRunElevated` not specified</span></span> | <span data-ttu-id="94869-236">Güncelleştirme gerekmiyor</span><span class="sxs-lookup"><span data-stu-id="94869-236">No update required</span></span>                                                                                                                     |

### <a name="batch-python"></a><span data-ttu-id="94869-237">Batch Python</span><span class="sxs-lookup"><span data-stu-id="94869-237">Batch Python</span></span>

| <span data-ttu-id="94869-238">Kodunuzu kullanıyorsa...</span><span class="sxs-lookup"><span data-stu-id="94869-238">If your code uses...</span></span>                      | <span data-ttu-id="94869-239">Buna güncelleştirme...</span><span class="sxs-lookup"><span data-stu-id="94869-239">Update it to....</span></span>                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `run_elevated=True`                       | <span data-ttu-id="94869-240">`user_identity=user`, burada</span><span class="sxs-lookup"><span data-stu-id="94869-240">`user_identity=user`, where</span></span> <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.admin)) `                |
| `run_elevated=False`                      | <span data-ttu-id="94869-241">`user_identity=user`, burada</span><span class="sxs-lookup"><span data-stu-id="94869-241">`user_identity=user`, where</span></span> <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.nonadmin)) `             |
| <span data-ttu-id="94869-242">`run_elevated`belirtilmemiş.</span><span class="sxs-lookup"><span data-stu-id="94869-242">`run_elevated` not specified</span></span> | <span data-ttu-id="94869-243">Güncelleştirme gerekmiyor</span><span class="sxs-lookup"><span data-stu-id="94869-243">No update required</span></span>                                                                                                                                  |


## <a name="next-steps"></a><span data-ttu-id="94869-244">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="94869-244">Next steps</span></span>

### <a name="batch-forum"></a><span data-ttu-id="94869-245">Toplu işlem Forumu</span><span class="sxs-lookup"><span data-stu-id="94869-245">Batch Forum</span></span>

<span data-ttu-id="94869-246">[Azure toplu işlem Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch) MSDN'de toplu ele almaktadır ve hizmet hakkında sorular sormak için iyi bir yerdir.</span><span class="sxs-lookup"><span data-stu-id="94869-246">The [Azure Batch Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch) on MSDN is a great place to discuss Batch and ask questions about the service.</span></span> <span data-ttu-id="94869-247">HEAD üzerinde üzerinden faydalı sabitlenmiş gönderiler için ve Batch çözümlerinizi derleme sırasında çıktıkları anda sorularınızı gönderin.</span><span class="sxs-lookup"><span data-stu-id="94869-247">Head on over for helpful pinned posts, and post your questions as they arise while you build your Batch solutions.</span></span>