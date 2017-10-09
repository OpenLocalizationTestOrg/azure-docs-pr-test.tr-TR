---
title: "aaaContainer Azure günlük analizi izleme çözümüne | Microsoft Docs"
description: "Hello günlük analizi kapsayıcı izleme çözümünde görüntülemenize ve Docker ve Windows yönetmenize yardımcı olur kapsayıcı konakları tek bir konumda."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: e1e4b52b-92d5-4bfa-8a09-ff8c6b5a9f78
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: magoedte;banders
ms.openlocfilehash: 2eed1dd81c22faef78a375fca3ebece9e5300c09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="container-monitoring-solution-in-log-analytics"></a><span data-ttu-id="edd79-103">Kapsayıcı izleme çözümüne günlük analizi</span><span class="sxs-lookup"><span data-stu-id="edd79-103">Container Monitoring solution in Log Analytics</span></span>

![Kapsayıcıları simgesi](./media/log-analytics-containers/containers-symbol.png)

<span data-ttu-id="edd79-105">Tooset ayarlama ve kullanma görüntülemenize ve Docker ve Windows yönetmenize yardımcı olan günlük analizi kapsayıcı izleme çözümünde nasıl hello bu makalede tek bir konumda kapsayıcı konakları.</span><span class="sxs-lookup"><span data-stu-id="edd79-105">This article describes how tooset up and use hello Container Monitoring solution in Log Analytics, which helps you view and manage your Docker and Windows container hosts in a single location.</span></span> <span data-ttu-id="edd79-106">Docker olan yazılım sanallaştırma sistemi kullanılan yazılım dağıtım tootheir BT otomatikleştirmek toocreate kapsayıcıları altyapı.</span><span class="sxs-lookup"><span data-stu-id="edd79-106">Docker is a software virtualization system used toocreate containers that automate software deployment tootheir IT infrastructure.</span></span>

<span data-ttu-id="edd79-107">Merhaba, çalışan kapsayıcılar, çalıştırdıkları, hangi kapsayıcı görüntü çözüm gösterir ve kapsayıcıları çalıştırdığı.</span><span class="sxs-lookup"><span data-stu-id="edd79-107">hello solution shows which containers are running, what container image they’re running, and where containers are running.</span></span> <span data-ttu-id="edd79-108">Kapsayıcılar ile kullanılan komutları gösteren ayrıntılı denetim bilgileri görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="edd79-108">You can view detailed audit information showing commands used with containers.</span></span> <span data-ttu-id="edd79-109">Ve görüntüleme ve tooremotely görünümü Docker veya Windows konakları gerek kalmadan merkezi günlükleri arama yaparak kapsayıcıları giderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="edd79-109">And, you can troubleshoot containers by viewing and searching centralized logs without having tooremotely view Docker or Windows hosts.</span></span> <span data-ttu-id="edd79-110">Bir ana bilgisayar üzerindeki gürültülü ve alan üst limiti aşan kaynakları olabilir kapsayıcıları bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="edd79-110">You can find containers that may be noisy and consuming excess resources on a host.</span></span> <span data-ttu-id="edd79-111">Ve merkezi CPU, bellek, depolama ve ağ kullanımı ve performans bilgilerini kapsayıcıları için görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="edd79-111">And, you can view centralized CPU, memory, storage, and network usage and performance information for containers.</span></span> <span data-ttu-id="edd79-112">Windows çalıştıran bilgisayarlarda, merkezileştirme ve Windows Server günlüklerinden karşılaştırmak Hyper-V ve Docker kapsayıcıları.</span><span class="sxs-lookup"><span data-stu-id="edd79-112">On computers running Windows, you can centralize and compare logs from Windows Server, Hyper-V, and Docker containers.</span></span> <span data-ttu-id="edd79-113">Merhaba çözüm kapsayıcı orchestrators aşağıdaki hello destekler:</span><span class="sxs-lookup"><span data-stu-id="edd79-113">hello solution supports hello following container orchestrators:</span></span>

- <span data-ttu-id="edd79-114">Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="edd79-114">Docker Swarm</span></span>
- <span data-ttu-id="edd79-115">DC/OS</span><span class="sxs-lookup"><span data-stu-id="edd79-115">DC/OS</span></span>
- <span data-ttu-id="edd79-116">Kubernetes</span><span class="sxs-lookup"><span data-stu-id="edd79-116">Kubernetes</span></span>
- <span data-ttu-id="edd79-117">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="edd79-117">Service Fabric</span></span>
- <span data-ttu-id="edd79-118">Red Hat OpenShift</span><span class="sxs-lookup"><span data-stu-id="edd79-118">Red Hat OpenShift</span></span>


<span data-ttu-id="edd79-119">Merhaba Aşağıdaki diyagramda çeşitli kapsayıcı konakları ve OMS aracılarla arasında hello ilişkiler gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="edd79-119">hello following diagram shows hello relationships between various container hosts and agents with OMS.</span></span>

![Kapsayıcıları diyagramı](./media/log-analytics-containers/containers-diagram.png)

## <a name="system-requirements"></a><span data-ttu-id="edd79-121">Sistem gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="edd79-121">System requirements</span></span>

<span data-ttu-id="edd79-122">Başlamadan önce hello önkoşulları karşılaması ayrıntıları tooverify aşağıdaki hello gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="edd79-122">Before starting, review hello following details tooverify you meet hello prerequisites.</span></span>

### <a name="container-monitoring-solution-support-for-docker-orchestrator-and-os-platform"></a><span data-ttu-id="edd79-123">Kapsayıcı izleme çözümü desteklemek için Docker Orchestrator ve işletim sistemi platformu</span><span class="sxs-lookup"><span data-stu-id="edd79-123">Container monitoring solution support for Docker Orchestrator and OS platform</span></span>
<span data-ttu-id="edd79-124">Merhaba aşağıdaki tabloda ana hatlarını Docker düzenleme ve işletim sistemi izleme desteği kapsayıcı envanter, performans ve günlük analizi ile günlükleri hello.</span><span class="sxs-lookup"><span data-stu-id="edd79-124">hello following table outlines hello Docker orchestration and operating system monitoring support of container inventory, performance, and logs with Log Analytics.</span></span>   

| | <span data-ttu-id="edd79-125">ACS</span><span class="sxs-lookup"><span data-stu-id="edd79-125">ACS</span></span> | <span data-ttu-id="edd79-126">Linux</span><span class="sxs-lookup"><span data-stu-id="edd79-126">Linux</span></span> | <span data-ttu-id="edd79-127">Windows</span><span class="sxs-lookup"><span data-stu-id="edd79-127">Windows</span></span> | <span data-ttu-id="edd79-128">Kapsayıcı</span><span class="sxs-lookup"><span data-stu-id="edd79-128">Container</span></span><br><span data-ttu-id="edd79-129">Stok</span><span class="sxs-lookup"><span data-stu-id="edd79-129">Inventory</span></span> | <span data-ttu-id="edd79-130">Görüntü</span><span class="sxs-lookup"><span data-stu-id="edd79-130">Image</span></span><br><span data-ttu-id="edd79-131">Stok</span><span class="sxs-lookup"><span data-stu-id="edd79-131">Inventory</span></span> | <span data-ttu-id="edd79-132">Node</span><span class="sxs-lookup"><span data-stu-id="edd79-132">Node</span></span><br><span data-ttu-id="edd79-133">Stok</span><span class="sxs-lookup"><span data-stu-id="edd79-133">Inventory</span></span> | <span data-ttu-id="edd79-134">Kapsayıcı</span><span class="sxs-lookup"><span data-stu-id="edd79-134">Container</span></span><br><span data-ttu-id="edd79-135">Performans</span><span class="sxs-lookup"><span data-stu-id="edd79-135">Performance</span></span> | <span data-ttu-id="edd79-136">Kapsayıcı</span><span class="sxs-lookup"><span data-stu-id="edd79-136">Container</span></span><br><span data-ttu-id="edd79-137">Olay</span><span class="sxs-lookup"><span data-stu-id="edd79-137">Event</span></span> | <span data-ttu-id="edd79-138">Olay</span><span class="sxs-lookup"><span data-stu-id="edd79-138">Event</span></span><br><span data-ttu-id="edd79-139">Günlük</span><span class="sxs-lookup"><span data-stu-id="edd79-139">Log</span></span> | <span data-ttu-id="edd79-140">Kapsayıcı</span><span class="sxs-lookup"><span data-stu-id="edd79-140">Container</span></span><br><span data-ttu-id="edd79-141">Günlük</span><span class="sxs-lookup"><span data-stu-id="edd79-141">Log</span></span> |
|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|
| <span data-ttu-id="edd79-142">Kubernetes</span><span class="sxs-lookup"><span data-stu-id="edd79-142">Kubernetes</span></span> | <span data-ttu-id="edd79-143">&#8226;</span><span class="sxs-lookup"><span data-stu-id="edd79-143">&#8226;</span></span> | <span data-ttu-id="edd79-144">&#8226;</span><span class="sxs-lookup"><span data-stu-id="edd79-144">&#8226;</span></span> | | <span data-ttu-id="edd79-145">&#8226;</span><span class="sxs-lookup"><span data-stu-id="edd79-145">&#8226;</span></span> | <span data-ttu-id="edd79-146">&#8226;</span><span class="sxs-lookup"><span data-stu-id="edd79-146">&#8226;</span></span> | <span data-ttu-id="edd79-147">&#8226;</span><span class="sxs-lookup"><span data-stu-id="edd79-147">&#8226;</span></span> | <span data-ttu-id="edd79-148">&#8226;</span><span class="sxs-lookup"><span data-stu-id="edd79-148">&#8226;</span></span> | <span data-ttu-id="edd79-149">&#8226;</span><span class="sxs-lookup"><span data-stu-id="edd79-149">&#8226;</span></span> | <span data-ttu-id="edd79-150">&#8226;</span><span class="sxs-lookup"><span data-stu-id="edd79-150">&#8226;</span></span> | <span data-ttu-id="edd79-151">&#8226;</span><span class="sxs-lookup"><span data-stu-id="edd79-151">&#8226;</span></span> |
| <span data-ttu-id="edd79-152">Mesosphere</span><span class="sxs-lookup"><span data-stu-id="edd79-152">Mesosphere</span></span><br><span data-ttu-id="edd79-153">DC/OS</span><span class="sxs-lookup"><span data-stu-id="edd79-153">DC/OS</span></span> | <span data-ttu-id="edd79-154">&#8226;</span><span class="sxs-lookup"><span data-stu-id="edd79-154">&#8226;</span></span> | <span data-ttu-id="edd79-155">&#8226;</span><span class="sxs-lookup"><span data-stu-id="edd79-155">&#8226;</span></span> | | <span data-ttu-id="edd79-156">&#8226;</span><span class="sxs-lookup"><span data-stu-id="edd79-156">&#8226;</span></span> | <span data-ttu-id="edd79-157">&#8226;</span><span class="sxs-lookup"><span data-stu-id="edd79-157">&#8226;</span></span> | <span data-ttu-id="edd79-158">&#8226;</span><span class="sxs-lookup"><span data-stu-id="edd79-158">&#8226;</span></span> | <span data-ttu-id="edd79-159">&#8226;</span><span class="sxs-lookup"><span data-stu-id="edd79-159">&#8226;</span></span>| <span data-ttu-id="edd79-160">&#8226;</span><span class="sxs-lookup"><span data-stu-id="edd79-160">&#8226;</span></span> | <span data-ttu-id="edd79-161">&#8226;</span><span class="sxs-lookup"><span data-stu-id="edd79-161">&#8226;</span></span> | <span data-ttu-id="edd79-162">&#8226;</span><span class="sxs-lookup"><span data-stu-id="edd79-162">&#8226;</span></span> |
| <span data-ttu-id="edd79-163">Docker</span><span class="sxs-lookup"><span data-stu-id="edd79-163">Docker</span></span><br><span data-ttu-id="edd79-164">Swarm</span><span class="sxs-lookup"><span data-stu-id="edd79-164">Swarm</span></span> | <span data-ttu-id="edd79-165">&#8226;</span><span class="sxs-lookup"><span data-stu-id="edd79-165">&#8226;</span></span> | <span data-ttu-id="edd79-166">&#8226;</span><span class="sxs-lookup"><span data-stu-id="edd79-166">&#8226;</span></span> | <span data-ttu-id="edd79-167">&#8226;</span><span class="sxs-lookup"><span data-stu-id="edd79-167">&#8226;</span></span> | <span data-ttu-id="edd79-168">&#8226;</span><span class="sxs-lookup"><span data-stu-id="edd79-168">&#8226;</span></span> | <span data-ttu-id="edd79-169">&#8226;</span><span class="sxs-lookup"><span data-stu-id="edd79-169">&#8226;</span></span> | <span data-ttu-id="edd79-170">&#8226;</span><span class="sxs-lookup"><span data-stu-id="edd79-170">&#8226;</span></span> | <span data-ttu-id="edd79-171">&#8226;</span><span class="sxs-lookup"><span data-stu-id="edd79-171">&#8226;</span></span> | <span data-ttu-id="edd79-172">&#8226;</span><span class="sxs-lookup"><span data-stu-id="edd79-172">&#8226;</span></span> | | <span data-ttu-id="edd79-173">&#8226;</span><span class="sxs-lookup"><span data-stu-id="edd79-173">&#8226;</span></span> |
| <span data-ttu-id="edd79-174">Hizmet</span><span class="sxs-lookup"><span data-stu-id="edd79-174">Service</span></span><br><span data-ttu-id="edd79-175">Yapı</span><span class="sxs-lookup"><span data-stu-id="edd79-175">Fabric</span></span> | | | <span data-ttu-id="edd79-176">&#8226;</span><span class="sxs-lookup"><span data-stu-id="edd79-176">&#8226;</span></span> | <span data-ttu-id="edd79-177">&#8226;</span><span class="sxs-lookup"><span data-stu-id="edd79-177">&#8226;</span></span> | <span data-ttu-id="edd79-178">&#8226;</span><span class="sxs-lookup"><span data-stu-id="edd79-178">&#8226;</span></span> | <span data-ttu-id="edd79-179">&#8226;</span><span class="sxs-lookup"><span data-stu-id="edd79-179">&#8226;</span></span> | <span data-ttu-id="edd79-180">&#8226;</span><span class="sxs-lookup"><span data-stu-id="edd79-180">&#8226;</span></span> | <span data-ttu-id="edd79-181">&#8226;</span><span class="sxs-lookup"><span data-stu-id="edd79-181">&#8226;</span></span> | <span data-ttu-id="edd79-182">&#8226;</span><span class="sxs-lookup"><span data-stu-id="edd79-182">&#8226;</span></span> | <span data-ttu-id="edd79-183">&#8226;</span><span class="sxs-lookup"><span data-stu-id="edd79-183">&#8226;</span></span> |
| <span data-ttu-id="edd79-184">Red Hat Aç</span><span class="sxs-lookup"><span data-stu-id="edd79-184">Red Hat Open</span></span><br><span data-ttu-id="edd79-185">Kaydırma</span><span class="sxs-lookup"><span data-stu-id="edd79-185">Shift</span></span> | | <span data-ttu-id="edd79-186">&#8226;</span><span class="sxs-lookup"><span data-stu-id="edd79-186">&#8226;</span></span> | | <span data-ttu-id="edd79-187">&#8226;</span><span class="sxs-lookup"><span data-stu-id="edd79-187">&#8226;</span></span> | <span data-ttu-id="edd79-188">&#8226;</span><span class="sxs-lookup"><span data-stu-id="edd79-188">&#8226;</span></span>| <span data-ttu-id="edd79-189">&#8226;</span><span class="sxs-lookup"><span data-stu-id="edd79-189">&#8226;</span></span> | <span data-ttu-id="edd79-190">&#8226;</span><span class="sxs-lookup"><span data-stu-id="edd79-190">&#8226;</span></span> | <span data-ttu-id="edd79-191">&#8226;</span><span class="sxs-lookup"><span data-stu-id="edd79-191">&#8226;</span></span> | | <span data-ttu-id="edd79-192">&#8226;</span><span class="sxs-lookup"><span data-stu-id="edd79-192">&#8226;</span></span> |
| <span data-ttu-id="edd79-193">Windows Server</span><span class="sxs-lookup"><span data-stu-id="edd79-193">Windows Server</span></span><br><span data-ttu-id="edd79-194">(tek başına)</span><span class="sxs-lookup"><span data-stu-id="edd79-194">(standalone)</span></span> | | | <span data-ttu-id="edd79-195">&#8226;</span><span class="sxs-lookup"><span data-stu-id="edd79-195">&#8226;</span></span> | <span data-ttu-id="edd79-196">&#8226;</span><span class="sxs-lookup"><span data-stu-id="edd79-196">&#8226;</span></span> | <span data-ttu-id="edd79-197">&#8226;</span><span class="sxs-lookup"><span data-stu-id="edd79-197">&#8226;</span></span> | <span data-ttu-id="edd79-198">&#8226;</span><span class="sxs-lookup"><span data-stu-id="edd79-198">&#8226;</span></span> | <span data-ttu-id="edd79-199">&#8226;</span><span class="sxs-lookup"><span data-stu-id="edd79-199">&#8226;</span></span> | <span data-ttu-id="edd79-200">&#8226;</span><span class="sxs-lookup"><span data-stu-id="edd79-200">&#8226;</span></span> | | <span data-ttu-id="edd79-201">&#8226;</span><span class="sxs-lookup"><span data-stu-id="edd79-201">&#8226;</span></span> |
| <span data-ttu-id="edd79-202">Linux Sunucu</span><span class="sxs-lookup"><span data-stu-id="edd79-202">Linux Server</span></span><br><span data-ttu-id="edd79-203">(tek başına)</span><span class="sxs-lookup"><span data-stu-id="edd79-203">(standalone)</span></span> | | <span data-ttu-id="edd79-204">&#8226;</span><span class="sxs-lookup"><span data-stu-id="edd79-204">&#8226;</span></span> | | <span data-ttu-id="edd79-205">&#8226;</span><span class="sxs-lookup"><span data-stu-id="edd79-205">&#8226;</span></span> | <span data-ttu-id="edd79-206">&#8226;</span><span class="sxs-lookup"><span data-stu-id="edd79-206">&#8226;</span></span> | <span data-ttu-id="edd79-207">&#8226;</span><span class="sxs-lookup"><span data-stu-id="edd79-207">&#8226;</span></span> | <span data-ttu-id="edd79-208">&#8226;</span><span class="sxs-lookup"><span data-stu-id="edd79-208">&#8226;</span></span> | <span data-ttu-id="edd79-209">&#8226;</span><span class="sxs-lookup"><span data-stu-id="edd79-209">&#8226;</span></span> | | <span data-ttu-id="edd79-210">&#8226;</span><span class="sxs-lookup"><span data-stu-id="edd79-210">&#8226;</span></span> |


### <a name="docker-versions-supported-on-linux"></a><span data-ttu-id="edd79-211">Linux üzerinde desteklenen docker sürümleri</span><span class="sxs-lookup"><span data-stu-id="edd79-211">Docker versions supported on Linux</span></span>

- <span data-ttu-id="edd79-212">Docker 1.11 too1.13</span><span class="sxs-lookup"><span data-stu-id="edd79-212">Docker 1.11 too1.13</span></span>
- <span data-ttu-id="edd79-213">Docker CE ve EE v17.06</span><span class="sxs-lookup"><span data-stu-id="edd79-213">Docker CE and EE v17.06</span></span>

### <a name="x64-linux-distributions-supported-as-container-hosts"></a><span data-ttu-id="edd79-214">x64 kapsayıcı konakları olarak desteklenen Linux dağıtımları</span><span class="sxs-lookup"><span data-stu-id="edd79-214">x64 Linux distributions supported as container hosts</span></span>

- <span data-ttu-id="edd79-215">Ubuntu 14.04 LTS ve 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="edd79-215">Ubuntu 14.04 LTS and 16.04 LTS</span></span>
- <span data-ttu-id="edd79-216">CoreOS(stable)</span><span class="sxs-lookup"><span data-stu-id="edd79-216">CoreOS(stable)</span></span>
- <span data-ttu-id="edd79-217">Amazon Linux 2016.09.0</span><span class="sxs-lookup"><span data-stu-id="edd79-217">Amazon Linux 2016.09.0</span></span>
- <span data-ttu-id="edd79-218">openSUSE 13.2</span><span class="sxs-lookup"><span data-stu-id="edd79-218">openSUSE 13.2</span></span>
- <span data-ttu-id="edd79-219">openSUSE LEAP 42.2</span><span class="sxs-lookup"><span data-stu-id="edd79-219">openSUSE LEAP 42.2</span></span>
- <span data-ttu-id="edd79-220">CentOS 7.2 ve 7.3</span><span class="sxs-lookup"><span data-stu-id="edd79-220">CentOS 7.2 and 7.3</span></span>
- <span data-ttu-id="edd79-221">SLES 12</span><span class="sxs-lookup"><span data-stu-id="edd79-221">SLES 12</span></span>
- <span data-ttu-id="edd79-222">RHEL 7.2 ve 7.3</span><span class="sxs-lookup"><span data-stu-id="edd79-222">RHEL 7.2 and 7.3</span></span>
- <span data-ttu-id="edd79-223">Red Hat OpenShift kapsayıcı Platform (OCP) 3.4 ve 3.5</span><span class="sxs-lookup"><span data-stu-id="edd79-223">Red Hat OpenShift Container Platform (OCP) 3.4 and 3.5</span></span>
- <span data-ttu-id="edd79-224">ACS Mesosphere DC/OS 1.7.3 too1.8.8</span><span class="sxs-lookup"><span data-stu-id="edd79-224">ACS Mesosphere DC/OS 1.7.3 too1.8.8</span></span>
- <span data-ttu-id="edd79-225">ACS Kubernetes 1.4.5 too1.6</span><span class="sxs-lookup"><span data-stu-id="edd79-225">ACS Kubernetes 1.4.5 too1.6</span></span>
- <span data-ttu-id="edd79-226">ACS Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="edd79-226">ACS Docker Swarm</span></span>

### <a name="supported-windows-operating-system"></a><span data-ttu-id="edd79-227">Desteklenen Windows işletim sistemi</span><span class="sxs-lookup"><span data-stu-id="edd79-227">Supported Windows operating system</span></span>

- <span data-ttu-id="edd79-228">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="edd79-228">Windows Server 2016</span></span>
- <span data-ttu-id="edd79-229">Windows 10 Anniversary Edition (Professional veya Enterprise)</span><span class="sxs-lookup"><span data-stu-id="edd79-229">Windows 10 Anniversary Edition (Professional or Enterprise)</span></span>

### <a name="docker-versions-supported-on-windows"></a><span data-ttu-id="edd79-230">Windows'da desteklenen docker sürümleri</span><span class="sxs-lookup"><span data-stu-id="edd79-230">Docker versions supported on Windows</span></span>

- <span data-ttu-id="edd79-231">Docker 1.12 ve 1.13</span><span class="sxs-lookup"><span data-stu-id="edd79-231">Docker 1.12 and 1.13</span></span>
- <span data-ttu-id="edd79-232">Docker 17.03.0 ve sonraki sürümler</span><span class="sxs-lookup"><span data-stu-id="edd79-232">Docker 17.03.0 and later</span></span>

## <a name="installing-and-configuring-hello-solution"></a><span data-ttu-id="edd79-233">Yükleme ve yapılandırma hello çözümü</span><span class="sxs-lookup"><span data-stu-id="edd79-233">Installing and configuring hello solution</span></span>
<span data-ttu-id="edd79-234">Bilgi tooinstall aşağıdaki hello kullanın ve hello çözüm yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="edd79-234">Use hello following information tooinstall and configure hello solution.</span></span>

1. <span data-ttu-id="edd79-235">Merhaba kapsayıcı izleme çözümü tooyour OMS çalışma alanından eklemek [Azure Market](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ContainersOMS?tab=Overview) veya açıklanan hello işlemi kullanarak [hello Çözümleri Galerisi eklemek günlük analizi çözümleri](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="edd79-235">Add hello Container Monitoring solution tooyour OMS workspace from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ContainersOMS?tab=Overview) or by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>

2. <span data-ttu-id="edd79-236">Yükleyin ve Docker bir OMS Aracısı ile kullanın.</span><span class="sxs-lookup"><span data-stu-id="edd79-236">Install and use Docker with an OMS agent.</span></span>  <span data-ttu-id="edd79-237">İşletim sistemi temelinde, yöntemleri aşağıdaki hello seçebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="edd79-237">Based on your operating system, you can choose from hello following methods:</span></span>

  * <span data-ttu-id="edd79-238">Desteklenen Linux işletim sistemlerinde yüklemek ve Docker çalıştırın ve ardından yükleyin ve hello yapılandırın [Linux için OMS aracısının](log-analytics-agent-linux.md).</span><span class="sxs-lookup"><span data-stu-id="edd79-238">On supported Linux operating systems, install and run Docker and then install and configure hello [OMS Agent for Linux](log-analytics-agent-linux.md).</span></span>  
  * <span data-ttu-id="edd79-239">CoreOS üzerinde Linux için hello OMS Aracısı çalıştırılamıyor.</span><span class="sxs-lookup"><span data-stu-id="edd79-239">On CoreOS, you cannot run hello OMS Agent for Linux.</span></span> <span data-ttu-id="edd79-240">Bunun yerine, Linux için hello OMS Aracısı kapsayıcılı sürümünü çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="edd79-240">Instead, you run a containerized version of hello OMS Agent for Linux.</span></span> <span data-ttu-id="edd79-241">Gözden geçirme [CoreOS dahil olmak üzere Linux kapsayıcı konakları](#for-all-linux-container-hosts-including-coreos) veya [CoreOS dahil olmak üzere Azure kamu Linux kapsayıcı konakları](#for-all-azure-government-linux-container-hosts-including-coreos) Azure Bulutu kapsayıcılarında ile çalışıyorsanız.</span><span class="sxs-lookup"><span data-stu-id="edd79-241">Review [Linux container hosts including CoreOS](#for-all-linux-container-hosts-including-coreos) or [Azure Government Linux container hosts including CoreOS](#for-all-azure-government-linux-container-hosts-including-coreos) if you are working with containers in Azure Government Cloud.</span></span>
  * <span data-ttu-id="edd79-242">Windows Server 2016 ve Windows 10, hello Docker altyapısına ve istemcisi yükleme Aracısı toogather bilgi bağlanın ve tooLog Analytics gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="edd79-242">On Windows Server 2016 and Windows 10, install hello Docker Engine and client then connect an agent toogather information and send it tooLog Analytics.</span></span>  

### <a name="container-services"></a><span data-ttu-id="edd79-243">Kapsayıcı hizmetlerini</span><span class="sxs-lookup"><span data-stu-id="edd79-243">Container services</span></span>

- <span data-ttu-id="edd79-244">Red Hat OpenShift ortamınız varsa, gözden [bir OMS Aracısı Red Hat OpenShift için yapılandırma](#configure-an-oms-agent-for-red-hat-openshift).</span><span class="sxs-lookup"><span data-stu-id="edd79-244">If you have a Red Hat OpenShift environment, review [Configure an OMS agent for Red Hat OpenShift](#configure-an-oms-agent-for-red-hat-openshift).</span></span>
- <span data-ttu-id="edd79-245">Hello Azure kapsayıcı hizmeti kullanarak Kubernetes kümeniz varsa, gözden [Microsoft Operations Management Suite (OMS) Azure kapsayıcı hizmeti kümesini izlemek](../container-service/kubernetes/container-service-kubernetes-oms.md).</span><span class="sxs-lookup"><span data-stu-id="edd79-245">If you have a Kubernetes cluster using hello Azure Container Service, review [Monitor an Azure Container Service cluster with Microsoft Operations Management Suite (OMS)](../container-service/kubernetes/container-service-kubernetes-oms.md).</span></span>
- <span data-ttu-id="edd79-246">Bir Azure kapsayıcı hizmeti DC/OS kümeniz varsa, altında daha fazla bilgi [Operations Management Suite ile Azure kapsayıcı hizmeti DC/OS kümesi izlemek](../container-service/dcos-swarm/container-service-monitoring-oms.md).</span><span class="sxs-lookup"><span data-stu-id="edd79-246">If you have an Azure Container Service DC/OS cluster, learn more at [Monitor an Azure Container Service DC/OS cluster with Operations Management Suite](../container-service/dcos-swarm/container-service-monitoring-oms.md).</span></span>
- <span data-ttu-id="edd79-247">Bir Docker Swarm modu ortamınız varsa, altında daha fazla bilgi [Docker Swarm için bir OMS Aracısı Yapılandırma](#configure-an-oms-agent-for-docker-swarm).</span><span class="sxs-lookup"><span data-stu-id="edd79-247">If you have a Docker Swarm mode environment, learn more at [Configure an OMS agent for Docker Swarm](#configure-an-oms-agent-for-docker-swarm).</span></span>
- <span data-ttu-id="edd79-248">Service Fabric ile kapsayıcılar kullanıyorsa, hakkında daha fazla bilgi edinin [Azure Service Fabric genel bakış](../service-fabric/service-fabric-overview.md).</span><span class="sxs-lookup"><span data-stu-id="edd79-248">If you use containers with Service Fabric, learn more at [Overview of Azure Service Fabric](../service-fabric/service-fabric-overview.md).</span></span>
- <span data-ttu-id="edd79-249">Gözden geçirme hello [Docker altyapısına Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon) hakkında ek bilgi için makalenin tooinstall ve Windows çalıştıran bilgisayarlarda, Docker altyapılarını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="edd79-249">Review hello [Docker Engine on Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon) article for additional information about how tooinstall and configure your Docker Engines on computers running Windows.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="edd79-250">Docker çalıştırmalıdır **önce** hello yüklemek [Linux için OMS aracısının](log-analytics-agent-linux.md) kapsayıcı konaklarda.</span><span class="sxs-lookup"><span data-stu-id="edd79-250">Docker must be running **before** you install hello [OMS Agent for Linux](log-analytics-agent-linux.md) on your container hosts.</span></span> <span data-ttu-id="edd79-251">Docker yüklemeden önce hello Aracısı zaten yüklediyseniz, Linux için tooreinstall hello OMS Aracısı gerekir.</span><span class="sxs-lookup"><span data-stu-id="edd79-251">If you've already installed hello agent before installing Docker, you need tooreinstall hello OMS Agent for Linux.</span></span> <span data-ttu-id="edd79-252">Merhaba Docker hakkında daha fazla bilgi için bkz: [Docker Web sitesi](https://www.docker.com).</span><span class="sxs-lookup"><span data-stu-id="edd79-252">For more information about Docker, see hello [Docker website](https://www.docker.com).</span></span>


## <a name="linux-container-hosts"></a><span data-ttu-id="edd79-253">Linux kapsayıcı konakları</span><span class="sxs-lookup"><span data-stu-id="edd79-253">Linux container hosts</span></span>

<span data-ttu-id="edd79-254">Docker yükledikten sonra kapsayıcı konak tooconfigure hello aracınızı Docker ile kullanılmak için ayarları aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="edd79-254">After you've installed Docker, use hello following settings for your container host tooconfigure hello agent for use with Docker.</span></span> <span data-ttu-id="edd79-255">Öncelikle, OMS çalışma alanı kimliği ve hello Azure portalında bulabilirsiniz anahtarınızı gerekir.</span><span class="sxs-lookup"><span data-stu-id="edd79-255">First you need your OMS workspace ID and key, which you can find in hello Azure portal.</span></span> <span data-ttu-id="edd79-256">Çalışma alanınızda tıklatın **Hızlı Başlangıç** > **bilgisayarlar** tooview, **çalışma alanı kimliği** ve **birincil anahtar**.</span><span class="sxs-lookup"><span data-stu-id="edd79-256">In your workspace, click **Quick Start** > **Computers** tooview your **Workspace ID** and **Primary Key**.</span></span>  <span data-ttu-id="edd79-257">Kopyalayın ve her ikisi de, sık kullanılan düzenleyicisine yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="edd79-257">Copy and paste both into your favorite editor.</span></span>

### <a name="for-all-linux-container-hosts-except-coreos"></a><span data-ttu-id="edd79-258">Tüm Linux kapsayıcı ana bilgisayarlar için CoreOS dışında</span><span class="sxs-lookup"><span data-stu-id="edd79-258">For all Linux container hosts except CoreOS</span></span>

- <span data-ttu-id="edd79-259">Daha fazla bilgi ve nasıl tooinstall hello OMS Aracısı Linux için adımlar için bkz: [, Linux bilgisayarları tooOperations Yönetim Paketi (OMS) bağlantı](log-analytics-agent-linux.md).</span><span class="sxs-lookup"><span data-stu-id="edd79-259">For more information and steps on how tooinstall hello OMS Agent for Linux, see [Connect your Linux Computers tooOperations Management Suite (OMS)](log-analytics-agent-linux.md).</span></span>

### <a name="for-all-linux-container-hosts-including-coreos"></a><span data-ttu-id="edd79-260">CoreOS dahil olmak üzere tüm Linux kapsayıcı ana bilgisayarlar için</span><span class="sxs-lookup"><span data-stu-id="edd79-260">For all Linux container hosts including CoreOS</span></span>

<span data-ttu-id="edd79-261">Merhaba OMS kapsayıcı toomonitor istediğiniz başlatın.</span><span class="sxs-lookup"><span data-stu-id="edd79-261">Start hello OMS container that you want toomonitor.</span></span> <span data-ttu-id="edd79-262">Değiştirin ve aşağıdaki örneğine hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="edd79-262">Modify and use hello following example:</span></span>

```
sudo docker run --privileged -d -v /var/run/docker.sock:/var/run/docker.sock -e WSID="your workspace id" -e KEY="your key" -h=`hostname` -p 127.0.0.1:25225:25225 --name="omsagent" --restart=always microsoft/oms
```

### <a name="for-all-azure-government-linux-container-hosts-including-coreos"></a><span data-ttu-id="edd79-263">CoreOS dahil olmak üzere tüm Azure kamu Linux kapsayıcı ana bilgisayarlar için</span><span class="sxs-lookup"><span data-stu-id="edd79-263">For all Azure Government Linux container hosts including CoreOS</span></span>

<span data-ttu-id="edd79-264">Merhaba OMS kapsayıcı toomonitor istediğiniz başlatın.</span><span class="sxs-lookup"><span data-stu-id="edd79-264">Start hello OMS container that you want toomonitor.</span></span> <span data-ttu-id="edd79-265">Değiştirin ve aşağıdaki örneğine hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="edd79-265">Modify and use hello following example:</span></span>

```
sudo docker run --privileged -d -v /var/run/docker.sock:/var/run/docker.sock -v /var/log:/var/log -e WSID="your workspace id" -e KEY="your key" -e DOMAIN="opinsights.azure.us" -p 127.0.0.1:25225:25225 -p 127.0.0.1:25224:25224/udp --name="omsagent" -h=`hostname` --restart=always microsoft/oms
```

### <a name="switching-from-using-an-installed-linux-agent-tooone-in-a-container"></a><span data-ttu-id="edd79-266">Bir kapsayıcıda yüklü bir Linux Aracısı tooone kullanarak değiştirme</span><span class="sxs-lookup"><span data-stu-id="edd79-266">Switching from using an installed Linux agent tooone in a container</span></span>
<span data-ttu-id="edd79-267">Daha önce yüklenmiş doğrudan hello Aracısı kullanılan ve isterseniz önce yapmalısınız bir kapsayıcıda çalışan bir aracının tooinstead kullanmak Linux için hello OMS Aracısı kaldırın.</span><span class="sxs-lookup"><span data-stu-id="edd79-267">If you previously used hello directly-installed agent and want tooinstead use an agent running in a container, you must first remove hello OMS Agent for Linux.</span></span> <span data-ttu-id="edd79-268">Bkz: [kaldırma hello Linux için OMS aracısının](log-analytics-agent-linux.md#uninstalling-the-oms-agent-for-linux) nasıl toosuccessfully kaldırma toounderstand hello Aracısı.</span><span class="sxs-lookup"><span data-stu-id="edd79-268">See [Uninstalling hello OMS Agent for Linux](log-analytics-agent-linux.md#uninstalling-the-oms-agent-for-linux) toounderstand how toosuccessfully uninstall hello agent.</span></span>  

### <a name="configure-an-oms-agent-for-docker-swarm"></a><span data-ttu-id="edd79-269">Docker Swarm için OMS Aracısı'nı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="edd79-269">Configure an OMS agent for Docker Swarm</span></span>

<span data-ttu-id="edd79-270">Docker Swarm hakkında genel bir hizmet olarak hello OMS Aracısı çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="edd79-270">You can run hello OMS Agent as a global service on Docker Swarm.</span></span> <span data-ttu-id="edd79-271">Bilgi toocreate bir OMS Aracısı hizmeti aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="edd79-271">Use hello following information toocreate an OMS Agent service.</span></span> <span data-ttu-id="edd79-272">Tooinsert OMS çalışma alanı kimliği ve birincil anahtar gerekir.</span><span class="sxs-lookup"><span data-stu-id="edd79-272">You need tooinsert your OMS Workspace ID and Primary Key.</span></span>

- <span data-ttu-id="edd79-273">Merhaba aşağıdaki hello ana düğümde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="edd79-273">Run hello following on hello master node.</span></span>

    ```
    sudo docker service create  --name omsagent --mode global  --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock  -e WSID="<WORKSPACE ID>" -e KEY="<PRIMARY KEY>" -p 25225:25225 -p 25224:25224/udp  --restart-condition=on-failure microsoft/oms
    ```

### <a name="configure-an-oms-agent-for-red-hat-openshift"></a><span data-ttu-id="edd79-274">Red Hat OpenShift bir OMS Aracısı'nı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="edd79-274">Configure an OMS Agent for Red Hat OpenShift</span></span>
<span data-ttu-id="edd79-275">Üç yolu tooadd hello OMS Aracısı tooRed Hat OpenShift toostart kapsayıcı izleme veri toplama vardır.</span><span class="sxs-lookup"><span data-stu-id="edd79-275">There are three ways tooadd hello OMS Agent tooRed Hat OpenShift toostart collecting container monitoring data.</span></span>

* <span data-ttu-id="edd79-276">[Linux için Hello OMS Aracısı yükleme](log-analytics-agent-linux.md) doğrudan her bir düğümde OpenShift</span><span class="sxs-lookup"><span data-stu-id="edd79-276">[Install hello OMS Agent for Linux](log-analytics-agent-linux.md) directly on each OpenShift node</span></span>  
* <span data-ttu-id="edd79-277">[Log Analytics VM uzantısı etkinleştirmek](log-analytics-azure-vm-extension.md) Azure'da bulunan her bir OpenShift düğümüne</span><span class="sxs-lookup"><span data-stu-id="edd79-277">[Enable Log Analytics VM Extension](log-analytics-azure-vm-extension.md) on each OpenShift node residing in Azure</span></span>  
* <span data-ttu-id="edd79-278">Bir OpenShift arka plan programı kümesi olarak Hello OMS Aracısı yükleme</span><span class="sxs-lookup"><span data-stu-id="edd79-278">Install hello OMS Agent as a OpenShift daemon-set</span></span>  

<span data-ttu-id="edd79-279">Bu bölümde biz bir OpenShift arka plan programı kümesi olarak hello adımları gerekli tooinstall hello OMS Aracısı kapsar.</span><span class="sxs-lookup"><span data-stu-id="edd79-279">In this section we cover hello steps required tooinstall hello OMS Agent as an OpenShift daemon-set.</span></span>  

1. <span data-ttu-id="edd79-280">Toohello OpenShift ana düğüm ve kopyalama hello yaml dosya üzerinde oturum [ocp omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-omsagent.yaml) github'dan tooyour ana düğüm ve hello değerini OMS çalışma alanı Kimliğinizi ve birincil anahtarınız ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="edd79-280">Sign on toohello OpenShift master node and copy hello yaml file [ocp-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-omsagent.yaml) from GitHub tooyour master node and modify hello value with your OMS Workspace ID and with your Primary Key.</span></span>
2. <span data-ttu-id="edd79-281">Aşağıdaki komutları toocreate hello bir proje için OMS çalıştırın ve hello kullanıcı hesabı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="edd79-281">Run hello following commands toocreate a project for OMS and set hello user account.</span></span>

    ```
    oadm new-project omslogging --node-selector='zone=default'
    oc project omslogging  
    oc create serviceaccount omsagent  
    oadm policy add-cluster-role-to-user cluster-reader   system:serviceaccount:omslogging:omsagent  
    oadm policy add-scc-to-user privileged system:serviceaccount:omslogging:omsagent  
    ```

4. <span data-ttu-id="edd79-282">toodeploy hello arka plan programı kümesi hello aşağıdakileri çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="edd79-282">toodeploy hello daemon-set, run hello following:</span></span>

    `oc create -f ocp-omsagent.yaml`

5. <span data-ttu-id="edd79-283">yapılandırıldığı tooverify ve doğru şekilde çalıştığını hello aşağıdakileri yazın:</span><span class="sxs-lookup"><span data-stu-id="edd79-283">tooverify it is configured and working correctly, type hello following:</span></span>

    `oc describe daemonset omsagent`  

    <span data-ttu-id="edd79-284">ve hello çıktı aşağıdakine benzemelidir:</span><span class="sxs-lookup"><span data-stu-id="edd79-284">and hello output should resemble:</span></span>

    ```
    [ocpadmin@khm-0 ~]$ oc describe ds oms  
    Name:           oms  
    Image(s):       microsoft/oms  
    Selector:       name=omsagent  
    Node-Selector:  zone=default  
    Labels:         agentVersion=1.4.0-12  
                    dockerProviderVersion=10.0.0-25  
                    name=omsagent  
    Desired Number of Nodes Scheduled: 3  
    Current Number of Nodes Scheduled: 3  
    Number of Nodes Misscheduled: 0  
    Pods Status:    3 Running / 0 Waiting / 0 Succeeded / 0 Failed  
    No events.  
    ```

<span data-ttu-id="edd79-285">Toouse gizli toosecure OMS çalışma alanı kimliği ve birincil anahtar hello OMS Aracısı arka plan programı kümesi yaml dosyası kullanıldığında isterseniz, hello aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="edd79-285">If you want toouse secrets toosecure your OMS Workspace ID and Primary Key when using hello OMS Agent daemon-set yaml file, perform hello following steps.</span></span>

1. <span data-ttu-id="edd79-286">Toohello OpenShift ana düğüm ve kopyalama hello yaml dosya üzerinde oturum [ocp ds omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-ds-omsagent.yaml) ve komut dosyası oluşturuluyor gizli [ocp secretgen.sh](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-secretgen.sh) github'dan.</span><span class="sxs-lookup"><span data-stu-id="edd79-286">Sign on toohello OpenShift master node and copy hello yaml file [ocp-ds-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-ds-omsagent.yaml) and secret generating script [ocp-secretgen.sh](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-secretgen.sh) from GitHub.</span></span>  <span data-ttu-id="edd79-287">Bu komut dosyası için OMS çalışma alanı kimliği ve birincil anahtar toosecure hello gizli yaml dosyası oluşturur, bilgi secrete.</span><span class="sxs-lookup"><span data-stu-id="edd79-287">This script will generate hello secrets yaml file for OMS Workspace ID and Primary Key toosecure your secrete information.</span></span>  
2. <span data-ttu-id="edd79-288">Aşağıdaki komutları toocreate hello bir proje için OMS çalıştırın ve hello kullanıcı hesabı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="edd79-288">Run hello following commands toocreate a project for OMS and set hello user account.</span></span> <span data-ttu-id="edd79-289">komut dosyası oluşturuluyor hello gizli ister OMS çalışma alanı Kimliğiniz için <WSID> ve birincil anahtar <KEY> ve isteğe bağlı olarak tamamlandıktan sonra hello ocp-secret.yaml dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="edd79-289">hello secret generating script asks for your OMS Workspace ID <WSID> and Primary Key <KEY> and upon completion, it creates hello ocp-secret.yaml file.</span></span>  

    ```
    oadm new-project omslogging --node-selector='zone=default'  
    oc project omslogging  
    oc create serviceaccount omsagent  
    oadm policy add-cluster-role-to-user cluster-reader   system:serviceaccount:omslogging:omsagent  
    oadm policy add-scc-to-user privileged system:serviceaccount:omslogging:omsagent  
    ```

4. <span data-ttu-id="edd79-290">Merhaba gizli dosya hello aşağıdakini çalıştırarak dağıtın:</span><span class="sxs-lookup"><span data-stu-id="edd79-290">Deploy hello secret file by running hello following:</span></span>

    `oc create -f ocp-secret.yaml`

5. <span data-ttu-id="edd79-291">Dağıtım hello aşağıdakini çalıştırarak doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="edd79-291">Verify deployment by running hello following:</span></span>

    `oc describe secret omsagent-secret`  

    <span data-ttu-id="edd79-292">ve hello çıktı aşağıdakine benzemelidir:</span><span class="sxs-lookup"><span data-stu-id="edd79-292">and hello  output should resemble:</span></span>  

    ```
    [ocpadmin@khocp-master-0 ~]$ oc describe ds oms  
    Name:           oms  
    Image(s):       microsoft/oms  
    Selector:       name=omsagent  
    Node-Selector:  zone=default  
    Labels:         agentVersion=1.4.0-12  
                    dockerProviderVersion=10.0.0-25  
                    name=omsagent  
    Desired Number of Nodes Scheduled: 3  
    Current Number of Nodes Scheduled: 3  
    Number of Nodes Misscheduled: 0  
    Pods Status:    3 Running / 0 Waiting / 0 Succeeded / 0 Failed  
    No events.  
    ```

6. <span data-ttu-id="edd79-293">Merhaba OMS Aracısı arka plan programı kümesi yaml dosya hello aşağıdakini çalıştırarak dağıtın:</span><span class="sxs-lookup"><span data-stu-id="edd79-293">Deploy hello OMS Agent daemon-set yaml file by running hello following:</span></span>

    `oc create -f ocp-ds-omsagent.yaml`  

7. <span data-ttu-id="edd79-294">Dağıtım hello aşağıdakini çalıştırarak doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="edd79-294">Verify deployment by running hello following:</span></span>

    `oc describe ds oms`

    <span data-ttu-id="edd79-295">ve hello çıktı aşağıdakine benzemelidir:</span><span class="sxs-lookup"><span data-stu-id="edd79-295">and hello output should resemble:</span></span>

    ```
    [ocpadmin@khocp-master-0 ~]$ oc describe secret omsagent-secret  
    Name:           omsagent-secret  
    Namespace:      omslogging  
    Labels:         <none>  
    Annotations:    <none>  

    Type:   Opaque  

     Data  
     ====  
     KEY:    89 bytes  
     WSID:   37 bytes  
    ```

### <a name="secure-your-secret-information-for-docker-swarm-and-kubernetes"></a><span data-ttu-id="edd79-296">Gizli bilgilerinizi Docker Swarm ve Kubernetes için güvenli</span><span class="sxs-lookup"><span data-stu-id="edd79-296">Secure your secret information for Docker Swarm and Kubernetes</span></span>

<span data-ttu-id="edd79-297">Docker Swarm ve Kubernetes kapsayıcı hizmetlerini için gizli OMS çalışma alanı Kimliğinizi ve birincil anahtarlar güvenliğini sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="edd79-297">You can secure your secret OMS Workspace ID and Primary Keys for Docker Swarm and Kubernetes container services.</span></span>

#### <a name="secure-secrets-for-docker-swarm"></a><span data-ttu-id="edd79-298">Docker Swarm için güvenli parolaları</span><span class="sxs-lookup"><span data-stu-id="edd79-298">Secure secrets for Docker Swarm</span></span>

<span data-ttu-id="edd79-299">Çalışma alanı kimliği ve birincil anahtar için Hello gizli anahtar oluşturulduktan sonra Docker Swarm için hello çalıştırabilirsiniz OMSagent için hello Docker hizmeti oluşturun.</span><span class="sxs-lookup"><span data-stu-id="edd79-299">For Docker Swarm, once hello secret for Workspace ID and Primary Key is created, you can run hello create hello Docker service for OMSagent.</span></span> <span data-ttu-id="edd79-300">Bilgi toocreate aşağıdaki hello gizli bilgilerinizi kullanın.</span><span class="sxs-lookup"><span data-stu-id="edd79-300">Use hello following information toocreate your secret information.</span></span>

1. <span data-ttu-id="edd79-301">Merhaba aşağıdaki hello ana düğümde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="edd79-301">Run hello following on hello master node.</span></span>

    ```
    echo "WSID" | docker secret create WSID -
    echo "KEY" | docker secret create KEY -
    ```

2. <span data-ttu-id="edd79-302">Gizli düzgün bir şekilde oluşturulduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="edd79-302">Verify that secrets were created properly.</span></span>

    ```
    keiko@swarmm-master-13957614-0:/run# sudo docker secret ls
    ```

    ```
    ID                          NAME                CREATED             UPDATED
    j2fj153zxy91j8zbcitnjxjiv   WSID                43 minutes ago      43 minutes ago
    l9rh3n987g9c45zffuxdxetd9   KEY                 38 minutes ago      38 minutes ago
    ```

3. <span data-ttu-id="edd79-303">Komut toomount hello gizli toohello aşağıdaki çalışma hello OMS Aracısı kapsayıcılı.</span><span class="sxs-lookup"><span data-stu-id="edd79-303">Run hello following command toomount hello secrets toohello containerized OMS Agent.</span></span>

    ```
    sudo docker service create  --name omsagent --mode global  --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock --secret source=WSID,target=WSID --secret source=KEY,target=KEY  -p 25225:25225 -p 25224:25224/udp --restart-condition=on-failure microsoft/oms
    ```

#### <a name="secure-secrets-for-kubernetes-with-yaml-files"></a><span data-ttu-id="edd79-304">Yaml dosyalarla Kubernetes için güvenli parolaları</span><span class="sxs-lookup"><span data-stu-id="edd79-304">Secure secrets for Kubernetes with yaml files</span></span>

<span data-ttu-id="edd79-305">Kubernetes için çalışma alanı kimliği ve birincil anahtar için bir komut toogenerate hello gizli yaml dosyasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="edd79-305">For Kubernetes, you use a script toogenerate hello secrets yaml file for your Workspace ID and Primary Key.</span></span> <span data-ttu-id="edd79-306">Merhaba, [OMS Docker Kubernetes GitHub](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes) sayfasında, gizli bilgileri olan veya olmayan kullanabileceğiniz dosyaları vardır.</span><span class="sxs-lookup"><span data-stu-id="edd79-306">At hello [OMS Docker Kubernetes GitHub](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes) page, there are files that you can use with or without your secret information.</span></span>

- <span data-ttu-id="edd79-307">Merhaba varsayılan OMS Aracısı DaemonSet gizli bilgileri (omsagent.yaml) yok</span><span class="sxs-lookup"><span data-stu-id="edd79-307">hello Default OMS Agent DaemonSet does not have secret information (omsagent.yaml)</span></span>
- <span data-ttu-id="edd79-308">Merhaba OMS Aracısı DaemonSet yaml dosya gizli oluşturma betikleri toogenerate hello gizli yaml (omsagentsecret.yaml) dosyası ile gizli bilgileri (omsagent-ds-secrets.yaml) kullanır.</span><span class="sxs-lookup"><span data-stu-id="edd79-308">hello OMS Agent DaemonSet yaml file uses secret information (omsagent-ds-secrets.yaml) with secret generation scripts toogenerate hello secrets yaml (omsagentsecret.yaml) file.</span></span>

<span data-ttu-id="edd79-309">Toocreate omsagent DaemonSets ile veya olmadan gizli seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="edd79-309">You can choose toocreate omsagent DaemonSets with or without secrets.</span></span>

##### <a name="default-omsagent-daemonset-yaml-file-without-secrets"></a><span data-ttu-id="edd79-310">Varsayılan OMSagent DaemonSet yaml dosya gizlilikler olmadan</span><span class="sxs-lookup"><span data-stu-id="edd79-310">Default OMSagent DaemonSet yaml file without secrets</span></span>

- <span data-ttu-id="edd79-311">Merhaba varsayılan OMS Aracısı DaemonSet yaml dosyası için hello yerine `<WSID>` ve `<KEY>` tooyour WSID ve anahtarı.</span><span class="sxs-lookup"><span data-stu-id="edd79-311">For hello default OMS Agent DaemonSet yaml file, replace hello `<WSID>` and `<KEY>` tooyour WSID and KEY.</span></span> <span data-ttu-id="edd79-312">Merhaba dosya tooyour ana düğümü ve çalışma hello aşağıdakileri kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="edd79-312">Copy hello file tooyour master node and run hello following:</span></span>

    ```
    sudo kubectl create -f omsagent.yaml
    ```

##### <a name="default-omsagent-daemonset-yaml-file-with-secrets"></a><span data-ttu-id="edd79-313">Varsayılan OMSagent DaemonSet yaml dosya gizli</span><span class="sxs-lookup"><span data-stu-id="edd79-313">Default OMSagent DaemonSet yaml file with secrets</span></span>

1. <span data-ttu-id="edd79-314">toouse OMS Aracısı gizli bilgileri kullanarak DaemonSet hello gizli önce oluşturun.</span><span class="sxs-lookup"><span data-stu-id="edd79-314">toouse OMS Agent DaemonSet using secret information, create hello secrets first.</span></span>
    1. <span data-ttu-id="edd79-315">Hello komut dosyası ve gizli şablon dosyası kopyalayabilir ve üzerinde hello olduklarından emin olmak aynı dizin.</span><span class="sxs-lookup"><span data-stu-id="edd79-315">Copy hello script and secret template file and make sure they are on hello same directory.</span></span>
        - <span data-ttu-id="edd79-316">Komut dosyası - gizli gen.sh üretiliyor gizli</span><span class="sxs-lookup"><span data-stu-id="edd79-316">Secret generating script - secret-gen.sh</span></span>
        - <span data-ttu-id="edd79-317">Gizli şablon - gizli template.yaml</span><span class="sxs-lookup"><span data-stu-id="edd79-317">secret template - secret-template.yaml</span></span>
    2. <span data-ttu-id="edd79-318">Aşağıdaki örnek hello gibi Hello komut dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="edd79-318">Run hello script, like hello following example.</span></span> <span data-ttu-id="edd79-319">OMS çalışma alanı kimliği ve birincil anahtar Hello betik Merhaba sorar ve bunları girdikten sonra onu çalıştırabilmeniz için hello betik gizli yaml dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="edd79-319">hello script asks for hello OMS Workspace ID and Primary Key and after you enter them, hello script creates a secret yaml file so you can run it.</span></span>   

        ```
        #> sudo bash ./secret-gen.sh
        ```

    3. <span data-ttu-id="edd79-320">Merhaba gizli pod hello aşağıdakini çalıştırarak oluşturun:</span><span class="sxs-lookup"><span data-stu-id="edd79-320">Create hello secrets pod by running hello following:</span></span>
        ```
        sudo kubectl create -f omsagentsecret.yaml
        ```

    4. <span data-ttu-id="edd79-321">tooverify, Hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="edd79-321">tooverify, run hello following:</span></span>

        ```
        keiko@ubuntu16-13db:~# sudo kubectl get secrets
        ```

        <span data-ttu-id="edd79-322">Çıktı aşağıdakine benzemelidir:</span><span class="sxs-lookup"><span data-stu-id="edd79-322">Output should resemble:</span></span>

        ```
        NAME                  TYPE                                  DATA      AGE
        default-token-gvl91   kubernetes.io/service-account-token   3         50d
        omsagent-secret       Opaque                                2         1d
        ```

        ```
        keiko@ubuntu16-13db:~# sudo kubectl describe secrets omsagent-secret
        ```

        <span data-ttu-id="edd79-323">Çıktı aşağıdakine benzemelidir:</span><span class="sxs-lookup"><span data-stu-id="edd79-323">Output should resemble:</span></span>

        ```
        Name:           omsagent-secret
        Namespace:      default
        Labels:         <none>
        Annotations:    <none>

        Type:   Opaque

        Data
        ====
        WSID:   36 bytes
        KEY:    88 bytes
        ```

    5. <span data-ttu-id="edd79-324">Arka plan programı kümesi çalıştırarak, omsagent oluşturma``` sudo kubectl create -f omsagent-ds-secrets.yaml ```</span><span class="sxs-lookup"><span data-stu-id="edd79-324">Create your omsagent daemon-set by running ``` sudo kubectl create -f omsagent-ds-secrets.yaml ```</span></span>

2. <span data-ttu-id="edd79-325">OMS Aracısı DaemonSet çalıştığından, o hello aşağıdaki benzer toohello doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="edd79-325">Verify that hello OMS Agent DaemonSet is running, similar toohello following:</span></span>

    ```
    keiko@ubuntu16-13db:~# sudo kubectl get ds omsagent
    ```

    ```
    NAME       DESIRED   CURRENT   NODE-SELECTOR   AGE
    omsagent   3         3         <none>          1h
    ```


<span data-ttu-id="edd79-326">Kubernetes için çalışma alanı kimliği ve birincil anahtar için bir komut dosyası toogenerate hello gizli yaml dosyasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="edd79-326">For Kubernetes, use a script toogenerate hello secrets yaml file for Workspace ID and Primary Key.</span></span> <span data-ttu-id="edd79-327">Merhaba örnek bilgilerle aşağıdaki kullanım hello [omsagent yaml dosya](https://github.com/Microsoft/OMS-docker/blob/master/Kubernetes/omsagent.yaml) toosecure gizli bilgilerinizi.</span><span class="sxs-lookup"><span data-stu-id="edd79-327">Use hello following example information with hello [omsagent yaml file](https://github.com/Microsoft/OMS-docker/blob/master/Kubernetes/omsagent.yaml) toosecure your secret information.</span></span>

```
keiko@ubuntu16-13db:~# sudo kubectl describe secrets omsagent-secret
Name:           omsagent-secret
Namespace:      default
Labels:         <none>
Annotations:    <none>

Type:   Opaque

Data
====
WSID:   36 bytes
KEY:    88 bytes
```

## <a name="windows-container-hosts"></a><span data-ttu-id="edd79-328">Windows kapsayıcı konakları</span><span class="sxs-lookup"><span data-stu-id="edd79-328">Windows container hosts</span></span>

### <a name="preparation-before-installing-windows-agents"></a><span data-ttu-id="edd79-329">Windows aracıları yüklemeden önce hazırlama</span><span class="sxs-lookup"><span data-stu-id="edd79-329">Preparation before installing Windows agents</span></span>

<span data-ttu-id="edd79-330">Windows çalıştıran bilgisayarlarda aracılar yüklemeden önce tooconfigure hello Docker hizmet gerekir.</span><span class="sxs-lookup"><span data-stu-id="edd79-330">Before you install agents on computers running Windows, you need tooconfigure hello Docker service.</span></span> <span data-ttu-id="edd79-331">Hello yapılandırma, izleme için Docker TCP yuva hello aracıları hello Docker arka plan programı uzaktan erişebilmesi için hello Windows aracı veya hello günlük analizi sanal makine uzantısı toouse hello ve toocapture verileri sağlar.</span><span class="sxs-lookup"><span data-stu-id="edd79-331">hello configuration allows hello Windows agent or hello Log Analytics virtual machine extension toouse hello Docker TCP socket so that hello agents can access hello Docker daemon remotely and toocapture data for monitoring.</span></span>

#### <a name="toostart-docker-and-verify-its-configuration"></a><span data-ttu-id="edd79-332">toostart Docker ve yapılandırmasını doğrulayın</span><span class="sxs-lookup"><span data-stu-id="edd79-332">toostart Docker and verify its configuration</span></span>

<span data-ttu-id="edd79-333">Windows Server için adlandırılmış TCP yukarı adımlar tooset vardır:</span><span class="sxs-lookup"><span data-stu-id="edd79-333">There are steps needed tooset up TCP named pipe for Windows Server:</span></span>

1. <span data-ttu-id="edd79-334">Windows PowerShell'de TCP kanal ve adlandırılmış kanal etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="edd79-334">In Windows PowerShell, enable TCP pipe and named pipe.</span></span>

    ```
    Stop-Service docker
    dockerd --unregister-service
    dockerd --register-service -H npipe:// -H 0.0.0.0:2375  
    Start-Service docker
    ```

2. <span data-ttu-id="edd79-335">Docker hello yapılandırma dosyası TCP kanal için yapılandırmak ve adlandırılmış.</span><span class="sxs-lookup"><span data-stu-id="edd79-335">Configure Docker with hello configuration file for TCP pipe and named pipe.</span></span> <span data-ttu-id="edd79-336">Merhaba yapılandırma dosyası C:\ProgramData\docker\config\daemon.json bulunur.</span><span class="sxs-lookup"><span data-stu-id="edd79-336">hello configuration file is located at C:\ProgramData\docker\config\daemon.json.</span></span>

    <span data-ttu-id="edd79-337">Merhaba daemon.json dosyasında hello aşağıdaki gerekir:</span><span class="sxs-lookup"><span data-stu-id="edd79-337">In hello daemon.json file, you will need hello following:</span></span>

    ```
    {
    "hosts": ["tcp://0.0.0.0:2375", "npipe://"]
    }
    ```

<span data-ttu-id="edd79-338">İle Windows kapsayıcıları kullanılan hello Docker arka plan programı yapılandırma hakkında daha fazla bilgi için bkz: [Docker altyapısına Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon).</span><span class="sxs-lookup"><span data-stu-id="edd79-338">For more information about hello Docker daemon configuration used with Windows Containers, see [Docker Engine on Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon).</span></span>


### <a name="install-windows-agents"></a><span data-ttu-id="edd79-339">Windows aracılarını yükleme</span><span class="sxs-lookup"><span data-stu-id="edd79-339">Install Windows agents</span></span>

<span data-ttu-id="edd79-340">tooenable Windows ve Hyper-V kapsayıcı izleme, kapsayıcı konaklar Windows bilgisayarlarda hello Microsoft İzleme Aracısı'nı (MMA) yükleyin.</span><span class="sxs-lookup"><span data-stu-id="edd79-340">tooenable Windows and Hyper-V container monitoring, install hello Microsoft Monitoring Agent (MMA) on Windows computers that are container hosts.</span></span> <span data-ttu-id="edd79-341">Şirket içi ortamınızda Windows çalıştıran bilgisayarlar için bkz: [bağlanmak Windows bilgisayarları tooLog Analytics](log-analytics-windows-agents.md).</span><span class="sxs-lookup"><span data-stu-id="edd79-341">For computers running Windows in your on-premises environment, see [Connect Windows computers tooLog Analytics](log-analytics-windows-agents.md).</span></span> <span data-ttu-id="edd79-342">Sanal makineler için Azure'da çalışan bağlanmak bunları tooLog Analytics hello kullanarak [sanal makine uzantısı](log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="edd79-342">For virtual machines running in Azure, connect them tooLog Analytics using hello [virtual machine extension](log-analytics-azure-vm-extension.md).</span></span>

<span data-ttu-id="edd79-343">Service Fabric üzerinde çalışan Windows kapsayıcıları izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="edd79-343">You can monitor Windows containers running on Service Fabric.</span></span> <span data-ttu-id="edd79-344">Ancak, yalnızca [Azure'da çalışan sanal makineler](log-analytics-azure-vm-extension.md) ve [şirket içi ortamınızda Windows çalıştıran bilgisayarlar](log-analytics-windows-agents.md) için Service Fabric şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="edd79-344">However, only [virtual machines running in Azure](log-analytics-azure-vm-extension.md) and [computers running Windows in your on-premises environment](log-analytics-windows-agents.md) are currently supported for Service Fabric.</span></span>

<span data-ttu-id="edd79-345">Bu hello kapsayıcı izlemesi çözümü Windows için doğru ayarlandığını doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="edd79-345">You can verify that hello Container Monitoring solution is set correctly for Windows.</span></span> <span data-ttu-id="edd79-346">Merhaba Yönetim Paketi yükleme düzgün olup toocheck arayın *ContainerManagement.xxx*.</span><span class="sxs-lookup"><span data-stu-id="edd79-346">toocheck whether hello management pack was download properly, look for *ContainerManagement.xxx*.</span></span> <span data-ttu-id="edd79-347">Merhaba dosyaları hello C:\Program Files\Microsoft Monitoring Agent\Agent\Health hizmet State\Management paketleri klasörde olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="edd79-347">hello files should be in hello C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs folder.</span></span>


## <a name="solution-components"></a><span data-ttu-id="edd79-348">Çözüm bileşenleri</span><span class="sxs-lookup"><span data-stu-id="edd79-348">Solution components</span></span>

<span data-ttu-id="edd79-349">Windows aracılarının kullanıyorsanız, bu çözüme ekleyin ardından hello aşağıdaki Yönetim Paketi her bilgisayara bir aracı ile yüklenir.</span><span class="sxs-lookup"><span data-stu-id="edd79-349">If you are using Windows agents, then hello following management pack is installed on each computer with an agent when you add this solution.</span></span> <span data-ttu-id="edd79-350">Hiçbir yapılandırma ve Bakım hello Yönetim Paketi için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="edd79-350">No configuration or maintenance is required for hello management pack.</span></span>

- <span data-ttu-id="edd79-351">*ContainerManagement.xxx* C:\Program Files\Microsoft Monitoring Agent\Agent\Health hizmet State\Management paketlerinde yüklü</span><span class="sxs-lookup"><span data-stu-id="edd79-351">*ContainerManagement.xxx* installed in C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs</span></span>

## <a name="container-data-collection-details"></a><span data-ttu-id="edd79-352">Kapsayıcı veri toplama ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="edd79-352">Container data collection details</span></span>
<span data-ttu-id="edd79-353">Merhaba kapsayıcı izlemesi çözümü kapsayıcı konakları ve etkinleştirmeniz aracıları kullanarak kapsayıcıları çeşitli performans ölçümleri ve günlük verilerini toplar.</span><span class="sxs-lookup"><span data-stu-id="edd79-353">hello Container Monitoring solution collects various performance metrics and log data from container hosts and containers using agents that you enable.</span></span>

<span data-ttu-id="edd79-354">Verileri üç dakikada şu Aracısı türlerini hello tarafından toplanır.</span><span class="sxs-lookup"><span data-stu-id="edd79-354">Data is collected every three minutes by hello following agent types.</span></span>

- [<span data-ttu-id="edd79-355">Linux için OMS Aracısı</span><span class="sxs-lookup"><span data-stu-id="edd79-355">OMS Agent for Linux</span></span>](log-analytics-linux-agents.md)
- [<span data-ttu-id="edd79-356">Windows Aracısı</span><span class="sxs-lookup"><span data-stu-id="edd79-356">Windows agent</span></span>](log-analytics-windows-agents.md)
- [<span data-ttu-id="edd79-357">Log Analytics VM uzantısı</span><span class="sxs-lookup"><span data-stu-id="edd79-357">Log Analytics VM extension</span></span>](log-analytics-azure-vm-extension.md)


### <a name="container-records"></a><span data-ttu-id="edd79-358">Kapsayıcı kayıtlarını</span><span class="sxs-lookup"><span data-stu-id="edd79-358">Container records</span></span>

<span data-ttu-id="edd79-359">Merhaba aşağıdaki tabloda hello kapsayıcı izlemesi çözümü ve günlük arama sonuçlarında görünecek hello veri türleri tarafından toplanan kayıtları örnekleri gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="edd79-359">hello following table shows examples of records collected by hello Container Monitoring solution and hello data types that appear in log search results.</span></span>

| <span data-ttu-id="edd79-360">Veri türü</span><span class="sxs-lookup"><span data-stu-id="edd79-360">Data type</span></span> | <span data-ttu-id="edd79-361">Günlük arama veri türü</span><span class="sxs-lookup"><span data-stu-id="edd79-361">Data type in Log Search</span></span> | <span data-ttu-id="edd79-362">Alanları</span><span class="sxs-lookup"><span data-stu-id="edd79-362">Fields</span></span> |
| --- | --- | --- |
| <span data-ttu-id="edd79-363">Konaklar ve kapsayıcıları için performans</span><span class="sxs-lookup"><span data-stu-id="edd79-363">Performance for hosts and containers</span></span> | `Type=Perf` | <span data-ttu-id="edd79-364">Bilgisayar, ObjectName, CounterName &#40; % işlemci zamanı, Disk MB okur, MB, bellek kullanımı MB Disk Yazar ağ Al bayt, ağ gönderme bayt, işlemci kullanımı sn, ağ &#41; CounterValue, TimeGenerated, sayaç yolu, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="edd79-364">Computer, ObjectName, CounterName &#40;%Processor Time, Disk Reads MB, Disk Writes MB, Memory Usage MB, Network Receive Bytes, Network Send Bytes, Processor Usage sec, Network&#41;, CounterValue,TimeGenerated, CounterPath, SourceSystem</span></span> |
| <span data-ttu-id="edd79-365">Kapsayıcı envanteri</span><span class="sxs-lookup"><span data-stu-id="edd79-365">Container inventory</span></span> | `Type=ContainerInventory` | <span data-ttu-id="edd79-366">TimeGenerated, bilgisayar, ContainerHostname, görüntü, ImageTag, ContainerState, ExitCode, EnvironmentVar, komutu, CreatedTime, StartedTime, FinishedTime, SourceSystem, Containerıd, ImageID kapsayıcı adı</span><span class="sxs-lookup"><span data-stu-id="edd79-366">TimeGenerated, Computer, container name, ContainerHostname, Image, ImageTag, ContainerState, ExitCode, EnvironmentVar, Command, CreatedTime, StartedTime, FinishedTime, SourceSystem, ContainerID, ImageID</span></span> |
| <span data-ttu-id="edd79-367">Kapsayıcı görüntü envanteri</span><span class="sxs-lookup"><span data-stu-id="edd79-367">Container image inventory</span></span> | `Type=ContainerImageInventory` | <span data-ttu-id="edd79-368">TimeGenerated, bilgisayar, görüntü, ImageTag, ImageSize, VirtualSize, duraklatıldı, çalışıyor, durduruldu, başarısız, SourceSystem, ImageID, TotalContainer</span><span class="sxs-lookup"><span data-stu-id="edd79-368">TimeGenerated, Computer, Image, ImageTag, ImageSize, VirtualSize, Running, Paused, Stopped, Failed, SourceSystem, ImageID, TotalContainer</span></span> |
| <span data-ttu-id="edd79-369">Kapsayıcı günlük</span><span class="sxs-lookup"><span data-stu-id="edd79-369">Container log</span></span> | `Type=ContainerLog` | <span data-ttu-id="edd79-370">TimeGenerated, bilgisayar, görüntü kimliği, LogEntrySource, LogEntry, SourceSystem, Containerıd kapsayıcı adı</span><span class="sxs-lookup"><span data-stu-id="edd79-370">TimeGenerated, Computer, image ID, container name, LogEntrySource, LogEntry, SourceSystem, ContainerID</span></span> |
| <span data-ttu-id="edd79-371">Kapsayıcı hizmeti oturum açma</span><span class="sxs-lookup"><span data-stu-id="edd79-371">Container service log</span></span> | `Type=ContainerServiceLog`  | <span data-ttu-id="edd79-372">TimeGenerated, bilgisayar, TimeOfCommand, görüntü, komutu, SourceSystem, Containerıd</span><span class="sxs-lookup"><span data-stu-id="edd79-372">TimeGenerated, Computer, TimeOfCommand, Image, Command, SourceSystem, ContainerID</span></span> |
| <span data-ttu-id="edd79-373">Kapsayıcı düğümü envanteri</span><span class="sxs-lookup"><span data-stu-id="edd79-373">Container node inventory</span></span> | `Type=ContainerNodeInventory_CL`| <span data-ttu-id="edd79-374">TimeGenerated, bilgisayar, ClassName_s, DockerVersion_s, OperatingSystem_s, Volume_s, Network_s, NodeRole_s, OrchestratorType_s, InstanceID_g, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="edd79-374">TimeGenerated, Computer, ClassName_s, DockerVersion_s, OperatingSystem_s, Volume_s, Network_s, NodeRole_s, OrchestratorType_s, InstanceID_g, SourceSystem</span></span>|
| <span data-ttu-id="edd79-375">Kubernetes envanteri</span><span class="sxs-lookup"><span data-stu-id="edd79-375">Kubernetes inventory</span></span> | `Type=KubePodInventory_CL` | <span data-ttu-id="edd79-376">TimeGenerated, bilgisayar, PodLabel_deployment_s, PodLabel_deploymentconfig_s, PodLabel_docker_registry_s, Name_s, Namespace_s, PodStatus_s, PodIp_s, PodUid_g, PodCreationTimeStamp_t, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="edd79-376">TimeGenerated, Computer, PodLabel_deployment_s, PodLabel_deploymentconfig_s, PodLabel_docker_registry_s, Name_s, Namespace_s, PodStatus_s, PodIp_s, PodUid_g, PodCreationTimeStamp_t, SourceSystem</span></span> |
| <span data-ttu-id="edd79-377">Kapsayıcı işlemi</span><span class="sxs-lookup"><span data-stu-id="edd79-377">Container process</span></span> | `Type=ContainerProcess_CL` | <span data-ttu-id="edd79-378">TimeGenerated, bilgisayar, Pod_s, Namespace_s, ClassName_s, InstanceID_s, Uid_s, PID_s, PPID_s, C_s, STIME_s, Tty_s, TIME_s, Cmd_s, Id_s, Name_s, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="edd79-378">TimeGenerated, Computer, Pod_s, Namespace_s, ClassName_s, InstanceID_s, Uid_s, PID_s, PPID_s, C_s, STIME_s, Tty_s, TIME_s, Cmd_s, Id_s, Name_s, SourceSystem</span></span> |
| <span data-ttu-id="edd79-379">Kubernetes olayları</span><span class="sxs-lookup"><span data-stu-id="edd79-379">Kubernetes events</span></span> | `Type=KubeEvents_CL` | <span data-ttu-id="edd79-380">TimeGenerated, bilgisayar, Name_s, ObjectKind_s, Namespace_s, Reason_s, Type_s, SourceComponent_s, SourceSystem, ileti</span><span class="sxs-lookup"><span data-stu-id="edd79-380">TimeGenerated, Computer, Name_s, ObjectKind_s, Namespace_s, Reason_s, Type_s, SourceComponent_s, SourceSystem, Message</span></span> |

<span data-ttu-id="edd79-381">Etiketleri eklenmiş çok*PodLabel* veri türleridir kendi özel etiketler.</span><span class="sxs-lookup"><span data-stu-id="edd79-381">Labels appended too*PodLabel* data types are your own custom labels.</span></span> <span data-ttu-id="edd79-382">Merhaba eklenmiş PodLabel etiketleri hello tabloda gösterilen örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="edd79-382">hello appended PodLabel labels shown in hello table are examples.</span></span> <span data-ttu-id="edd79-383">Bu nedenle, `PodLabel_deployment_s`, `PodLabel_deploymentconfig_s`, `PodLabel_docker_registry_s` ortamınızı ait veri kümesinde farklı ve genel benzer `PodLabel_yourlabel_s`.</span><span class="sxs-lookup"><span data-stu-id="edd79-383">So, `PodLabel_deployment_s`, `PodLabel_deploymentconfig_s`, `PodLabel_docker_registry_s` will differ in your environment's data set and generically resemble `PodLabel_yourlabel_s`.</span></span>


## <a name="monitor-containers"></a><span data-ttu-id="edd79-384">İzleyici kapsayıcıları</span><span class="sxs-lookup"><span data-stu-id="edd79-384">Monitor containers</span></span>
<span data-ttu-id="edd79-385">Merhaba OMS portalında etkin hello çözüm aldıktan sonra hello **kapsayıcıları** döşeme kapsayıcı konakları ve ana bilgisayarlarda çalışan Merhaba kapsayıcılara hakkındaki özet bilgileri gösterir.</span><span class="sxs-lookup"><span data-stu-id="edd79-385">After you have hello solution enabled in hello OMS portal, hello **Containers** tile shows summary information about your container hosts and hello containers running in hosts.</span></span>

![Kapsayıcıları döşeme](./media/log-analytics-containers/containers-title.png)

<span data-ttu-id="edd79-387">Hello kutucuğu çalışıyor veya durdurulmuştur hello ortamı ve olup bunların başarısız, elinizde kaç kapsayıcıları genel bir bakış gösterilir.</span><span class="sxs-lookup"><span data-stu-id="edd79-387">hello tile shows an overview of how many containers you have in hello environment and whether they're failed, running, or stopped.</span></span>

### <a name="using-hello-containers-dashboard"></a><span data-ttu-id="edd79-388">Merhaba kapsayıcılara panosunu kullanma</span><span class="sxs-lookup"><span data-stu-id="edd79-388">Using hello Containers dashboard</span></span>
<span data-ttu-id="edd79-389">Merhaba tıklatın **kapsayıcıları** döşeme.</span><span class="sxs-lookup"><span data-stu-id="edd79-389">Click hello **Containers** tile.</span></span> <span data-ttu-id="edd79-390">Buradan düzenlenmiş görünümler görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="edd79-390">From there you'll see views organized by:</span></span>

- <span data-ttu-id="edd79-391">**Kapsayıcı olayları** -kapsayıcı durumu ve başarısız kapsayıcıları sahip bilgisayarları gösterir.</span><span class="sxs-lookup"><span data-stu-id="edd79-391">**Container Events** - Shows container status and computers with failed containers.</span></span>
- <span data-ttu-id="edd79-392">**Kapsayıcı günlükleri** -kapsayıcı günlük dosyalarının zaman ve bilgisayarların bir listesini hello en yüksek sayıda günlük dosyaları ile oluşturulan bir grafik gösterir.</span><span class="sxs-lookup"><span data-stu-id="edd79-392">**Container Logs** - Shows a chart of container log files generated over time and a list of computers with hello highest number of log files.</span></span>
- <span data-ttu-id="edd79-393">**Kubernetes olayları** -zaman ve neden pod'ları oluşturulan hello olayları hello nedenleri listesini oluşturulan Kubernetes olayları bir grafiğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="edd79-393">**Kubernetes Events** - Shows a chart of Kubernetes events generated over time and a list of hello reasons why pods generated hello events.</span></span> <span data-ttu-id="edd79-394">*Bu veri kümesi yalnızca Linux ortamlarda kullanılır.*</span><span class="sxs-lookup"><span data-stu-id="edd79-394">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="edd79-395">**Kubernetes Namespace stok** - gösterir hello sayısı ad alanları ve pod'ları ve hiyerarşileri gösterir.</span><span class="sxs-lookup"><span data-stu-id="edd79-395">**Kubernetes Namespace Inventory** - Shows hello number of namespaces and pods and shows their hierarchy.</span></span> <span data-ttu-id="edd79-396">*Bu veri kümesi yalnızca Linux ortamlarda kullanılır.*</span><span class="sxs-lookup"><span data-stu-id="edd79-396">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="edd79-397">**Kapsayıcı düğümü stok** -kapsayıcı düğümlerini/ana bilgisayarda kullanılan orchestration türleri hello sayısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="edd79-397">**Container Node Inventory** - Shows hello number of orchestration types used on container nodes/hosts.</span></span> <span data-ttu-id="edd79-398">Merhaba bilgisayar/ana bilgisayar düğümleri de Merhaba kapsayıcılara sayısıyla listelenir.</span><span class="sxs-lookup"><span data-stu-id="edd79-398">hello computer nodes/hosts are also listed by hello number of containers.</span></span> <span data-ttu-id="edd79-399">*Bu veri kümesi yalnızca Linux ortamlarda kullanılır.*</span><span class="sxs-lookup"><span data-stu-id="edd79-399">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="edd79-400">**Kapsayıcı görüntüleri stok** -hello kullanılan kapsayıcı görüntüleri toplam sayısı ve resim türleri sayısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="edd79-400">**Container Images Inventory** - Shows hello total number of container images used and number of image types.</span></span> <span data-ttu-id="edd79-401">Görüntü Hello sayısını da hello resim etiketi listelenir.</span><span class="sxs-lookup"><span data-stu-id="edd79-401">hello number of images are also listed by hello image tag.</span></span>
- <span data-ttu-id="edd79-402">**Kapsayıcıları durum** -çalışan kapsayıcılar olan düğümler/ana bilgisayarlar kapsayıcısı hello toplam sayısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="edd79-402">**Containers Status** - Shows hello total number of container nodes/host computers that have running containers.</span></span> <span data-ttu-id="edd79-403">Bilgisayarları da ana çalışan hello sayısı tarafından listelenir.</span><span class="sxs-lookup"><span data-stu-id="edd79-403">Computers are also listed by hello number of running hosts.</span></span>
- <span data-ttu-id="edd79-404">**Kapsayıcı işlem** -kapsayıcı işlemlerin zaman içinde çalışan bir çizgi grafiği gösterir.</span><span class="sxs-lookup"><span data-stu-id="edd79-404">**Container Process** - Shows a line chart of container processes running over time.</span></span> <span data-ttu-id="edd79-405">Kapsayıcılar, çalıştırarak da listelenen komutu/işlemi kapsayıcıları içinde.</span><span class="sxs-lookup"><span data-stu-id="edd79-405">Containers are also listed by running command/process within containers.</span></span> <span data-ttu-id="edd79-406">*Bu veri kümesi yalnızca Linux ortamlarda kullanılır.*</span><span class="sxs-lookup"><span data-stu-id="edd79-406">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="edd79-407">**Kapsayıcı CPU performans** -hello ortalama CPU kullanımı düğümleri/barındıran bilgisayar için zaman içinde bir çizgi grafiği gösterir.</span><span class="sxs-lookup"><span data-stu-id="edd79-407">**Container CPU Performance** - Shows a line chart of hello average CPU utilization over time for computer nodes/hosts.</span></span> <span data-ttu-id="edd79-408">Ayrıca listeleri hello bilgisayar düğümleri/ortalama CPU kullanımı tabanlı.</span><span class="sxs-lookup"><span data-stu-id="edd79-408">Also lists hello computer nodes/hosts based on average CPU utilization.</span></span>
- <span data-ttu-id="edd79-409">**Kapsayıcı bellek performansı** -zaman içinde bir çizgi grafiği bellek kullanımını gösterir.</span><span class="sxs-lookup"><span data-stu-id="edd79-409">**Container Memory Performance** - Shows a line chart of memory usage over time.</span></span> <span data-ttu-id="edd79-410">Ayrıca bilgisayar bellek kullanımı örneği adına göre listeler.</span><span class="sxs-lookup"><span data-stu-id="edd79-410">Also lists computer memory utilization based on instance name.</span></span>
- <span data-ttu-id="edd79-411">**Bilgisayar performansı** -gösterir hello Yüzde CPU performans zaman içerisinde, çizgi grafiklerde zaman ve megabayt boş disk alanı üzerinden bellek kullanımı yüzdesi Zamanla.</span><span class="sxs-lookup"><span data-stu-id="edd79-411">**Computer Performance** - Shows line charts of hello percent of CPU performance over time, percent of memory usage over time, and megabytes of free disk space over time.</span></span> <span data-ttu-id="edd79-412">Her satırda bir grafik tooview üzerinde daha fazla ayrıntı gelebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="edd79-412">You can hover over any line in a chart tooview more details.</span></span>


<span data-ttu-id="edd79-413">Her hello Pano görsel bir toplanan veriler üzerinde çalıştırılan bir arama alanıdır.</span><span class="sxs-lookup"><span data-stu-id="edd79-413">Each area of hello dashboard is a visual representation of a search that is run on collected data.</span></span>

![Kapsayıcıları Panosu](./media/log-analytics-containers/containers-dash01.png)

![Kapsayıcıları Panosu](./media/log-analytics-containers/containers-dash02.png)

<span data-ttu-id="edd79-416">Merhaba, **kapsayıcı durumu** alanında, aşağıda gösterildiği gibi hello üst bölmesinde tıklatın.</span><span class="sxs-lookup"><span data-stu-id="edd79-416">In hello **Container Status** area, click hello top area, as shown below.</span></span>

![Kapsayıcı durumu](./media/log-analytics-containers/containers-status.png)

<span data-ttu-id="edd79-418">Kapsayıcılarınızı hello durumu hakkındaki bilgileri görüntüleyen günlük arama açılır.</span><span class="sxs-lookup"><span data-stu-id="edd79-418">Log Search opens, displaying information about hello state of your containers.</span></span>

![Günlük arama kapsayıcıları için](./media/log-analytics-containers/containers-log-search.png)

<span data-ttu-id="edd79-420">Buradan, hello arama sorgusu toomodify düzenleyebilirsiniz, ilgilendiğiniz toofind hello özel bilgiler.</span><span class="sxs-lookup"><span data-stu-id="edd79-420">From here, you can edit hello search query toomodify it toofind hello specific information you're interested in.</span></span> <span data-ttu-id="edd79-421">Günlük aramaları hakkında daha fazla bilgi için bkz: [günlük analizi aramaları oturum](log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="edd79-421">For more information about Log Searches, see [Log searches in Log Analytics](log-analytics-log-searches.md).</span></span>

## <a name="troubleshoot-by-finding-a-failed-container"></a><span data-ttu-id="edd79-422">Başarısız bir kapsayıcı bulma ile ilgili sorunları giderme</span><span class="sxs-lookup"><span data-stu-id="edd79-422">Troubleshoot by finding a failed container</span></span>

<span data-ttu-id="edd79-423">Günlük analizi kapsayıcı olarak işaretler **başarısız** sıfır olmayan çıkış kodu ile çıkıldı durumunda.</span><span class="sxs-lookup"><span data-stu-id="edd79-423">Log Analytics marks a container as **Failed** if it has exited with a non-zero exit code.</span></span> <span data-ttu-id="edd79-424">Hello hataları ve hataları hello hello ortamında özetini görebilirsiniz **başarısız kapsayıcıları** alanı.</span><span class="sxs-lookup"><span data-stu-id="edd79-424">You can see an overview of hello errors and failures in hello environment in hello **Failed Containers** area.</span></span>

### <a name="toofind-failed-containers"></a><span data-ttu-id="edd79-425">toofind kapsayıcıları başarısız oldu</span><span class="sxs-lookup"><span data-stu-id="edd79-425">toofind failed containers</span></span>
1. <span data-ttu-id="edd79-426">Merhaba tıklatın **kapsayıcı durumu** alanı.</span><span class="sxs-lookup"><span data-stu-id="edd79-426">Click hello **Container Status** area.</span></span>  
   <span data-ttu-id="edd79-427">![kapsayıcı durumu](./media/log-analytics-containers/containers-status.png)</span><span class="sxs-lookup"><span data-stu-id="edd79-427">![containers status](./media/log-analytics-containers/containers-status.png)</span></span>
2. <span data-ttu-id="edd79-428">Günlük arama açar ve Merhaba, kapsayıcıları durumunu izleyen benzer toohello görüntüler.</span><span class="sxs-lookup"><span data-stu-id="edd79-428">Log Search opens and displays hello state of your containers, similar toohello following.</span></span>  
   ![kapsayıcı durumu](./media/log-analytics-containers/containers-log-search.png)
3. <span data-ttu-id="edd79-430">Ardından, başarısız kapsayıcıları tooview ek bilgiler toplanır hello değerini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="edd79-430">Next, click hello aggregated value of failed containers tooview additional information.</span></span> <span data-ttu-id="edd79-431">Genişletme **daha fazla Göster** tooview hello görüntü kimliği</span><span class="sxs-lookup"><span data-stu-id="edd79-431">Expand **show more** tooview hello image ID.</span></span>  
   <span data-ttu-id="edd79-432">![başarısız kapsayıcıları](./media/log-analytics-containers/containers-state-failed.png)</span><span class="sxs-lookup"><span data-stu-id="edd79-432">![failed containers](./media/log-analytics-containers/containers-state-failed.png)</span></span>  
4. <span data-ttu-id="edd79-433">Ardından, hello aşağıdaki hello arama sorgusu yazın.</span><span class="sxs-lookup"><span data-stu-id="edd79-433">Next, type hello following in hello search query.</span></span> <span data-ttu-id="edd79-434">`Type=ContainerInventory <ImageID>`görüntü boyutu ve durduruldu ve başarısız resimlerinin sayısı gibi hello görüntü ayrıntılarını toosee.</span><span class="sxs-lookup"><span data-stu-id="edd79-434">`Type=ContainerInventory <ImageID>` toosee details about hello image such as image size and number of stopped and failed images.</span></span>  
   <span data-ttu-id="edd79-435">![başarısız kapsayıcıları](./media/log-analytics-containers/containers-failed04.png)</span><span class="sxs-lookup"><span data-stu-id="edd79-435">![failed containers](./media/log-analytics-containers/containers-failed04.png)</span></span>

## <a name="search-logs-for-container-data"></a><span data-ttu-id="edd79-436">Kapsayıcı verileri için arama günlüklerini</span><span class="sxs-lookup"><span data-stu-id="edd79-436">Search logs for container data</span></span>
<span data-ttu-id="edd79-437">Belirli bir hata gidermeye çalışıyorsanız, ortamınızda oluştuğu toosee yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="edd79-437">When you're troubleshooting a specific error, it can help toosee where it is occurring in your environment.</span></span> <span data-ttu-id="edd79-438">şu günlük türlerini hello tooreturn hello bilgileri sorgular oluşturmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="edd79-438">hello following log types will help you create queries tooreturn hello information you want.</span></span>


- <span data-ttu-id="edd79-439">**ContainerImageInventory** – resim kimlikleri veya boyutları gibi görüntü ve tooview görüntü bilgileri tarafından düzenlenmiş toofind bilgileri çalışırken bu türü kullanın.</span><span class="sxs-lookup"><span data-stu-id="edd79-439">**ContainerImageInventory** – Use this type when you're trying toofind information organized by image and tooview image information such as image IDs or sizes.</span></span>
- <span data-ttu-id="edd79-440">**ContainerInventory** – kapsayıcı konumunu, adlarını nedir ve ne hakkında bilgi almak istediğinizde bu türü kullanın çalıştırma kaynağınız görüntüler.</span><span class="sxs-lookup"><span data-stu-id="edd79-440">**ContainerInventory** – Use this type when you want information about container location, what their names are, and what images they're running.</span></span>
- <span data-ttu-id="edd79-441">**ContainerLog** – toofind belirli hata günlüğü bilgilerini ve girişleri istediğinizde bu türü kullanın.</span><span class="sxs-lookup"><span data-stu-id="edd79-441">**ContainerLog** – Use this type when you want toofind specific error log information and entries.</span></span>
- <span data-ttu-id="edd79-442">**ContainerNodeInventory_CL** kapsayıcıları burada bulunan konak/düğüm hakkında hello bilgi istediğinizde bu türü kullanın.</span><span class="sxs-lookup"><span data-stu-id="edd79-442">**ContainerNodeInventory_CL**  Use this type when you want hello information about host/node where containers are residing.</span></span> <span data-ttu-id="edd79-443">Bu, Docker sürüm, orchestration türünü, depolama ve ağ bilgilerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="edd79-443">It provides you Docker version, orchestration type, storage, and network information.</span></span>
- <span data-ttu-id="edd79-444">**ContainerProcess_CL** kullanma Bu tür tooquickly hello kapsayıcıda çalıştırılan hello işlemi konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="edd79-444">**ContainerProcess_CL** Use this type tooquickly see hello process running within hello container.</span></span>
- <span data-ttu-id="edd79-445">**ContainerServiceLog** – hello Docker arka plan programı, Başlat, Durdur, silmek veya çekme komutları için toofind denetim izi bilgilerini çalışırken bu türü kullanın.</span><span class="sxs-lookup"><span data-stu-id="edd79-445">**ContainerServiceLog** – Use this type when you're trying toofind audit trail information for hello Docker daemon, such as start, stop, delete, or pull commands.</span></span>
- <span data-ttu-id="edd79-446">**KubeEvents_CL** bu tür toosee hello Kubernetes olayları kullanın.</span><span class="sxs-lookup"><span data-stu-id="edd79-446">**KubeEvents_CL**  Use this type toosee hello Kubernetes events.</span></span>
- <span data-ttu-id="edd79-447">**KubePodInventory_CL** toounderstand hello küme hiyerarşisi bilgileri istediğinizde bu türü kullanın.</span><span class="sxs-lookup"><span data-stu-id="edd79-447">**KubePodInventory_CL**  Use this type when you want toounderstand hello cluster hierarchy information.</span></span>


### <a name="toosearch-logs-for-container-data"></a><span data-ttu-id="edd79-448">kapsayıcı verilerini toosearch günlükleri</span><span class="sxs-lookup"><span data-stu-id="edd79-448">toosearch logs for container data</span></span>
* <span data-ttu-id="edd79-449">Bildiğiniz bir görüntüyü yakın zamanda başarısız oldu ve hello Hata günlüklerini bulabilmelerini seçin.</span><span class="sxs-lookup"><span data-stu-id="edd79-449">Choose an image that you know has failed recently and find hello error logs for it.</span></span> <span data-ttu-id="edd79-450">Başlat, görüntü ile çalışan bir kapsayıcı adı bularak bir **ContainerInventory** arama.</span><span class="sxs-lookup"><span data-stu-id="edd79-450">Start by finding a container name that is running that image with a **ContainerInventory** search.</span></span> <span data-ttu-id="edd79-451">Örneğin, arama`Type=ContainerInventory ubuntu Failed`</span><span class="sxs-lookup"><span data-stu-id="edd79-451">For example, search for `Type=ContainerInventory ubuntu Failed`</span></span>  
    <span data-ttu-id="edd79-452">![Ubuntu kapsayıcıları için arama](./media/log-analytics-containers/search-ubuntu.png)</span><span class="sxs-lookup"><span data-stu-id="edd79-452">![Search for Ubuntu containers](./media/log-analytics-containers/search-ubuntu.png)</span></span>

  <span data-ttu-id="edd79-453">Merhaba kapsayıcının adını sonraki çok hello**adı**ve bu günlükleri arayın.</span><span class="sxs-lookup"><span data-stu-id="edd79-453">hello name of hello container next too**Name**, and search for those logs.</span></span> <span data-ttu-id="edd79-454">Bu örnekte bu değer `Type=ContainerLog cranky_stonebreaker`’dur.</span><span class="sxs-lookup"><span data-stu-id="edd79-454">In this example, it is `Type=ContainerLog cranky_stonebreaker`.</span></span>

<span data-ttu-id="edd79-455">**Performans bilgilerini görüntüleme**</span><span class="sxs-lookup"><span data-stu-id="edd79-455">**View performance information**</span></span>

<span data-ttu-id="edd79-456">Tooconstruct sorguları başlayan olduğunda, ilk olası nedir toosee yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="edd79-456">When you're beginning tooconstruct queries, it can help toosee what's possible first.</span></span> <span data-ttu-id="edd79-457">Örneğin, tüm performans verileri, yazarak geniş bir sorgu hello aşağıdaki try arama toosee sorgu.</span><span class="sxs-lookup"><span data-stu-id="edd79-457">For example, toosee all performance data, try a broad query by typing hello following search query.</span></span>

```
Type=Perf
```

![kapsayıcıları performansı](./media/log-analytics-containers/containers-perf01.png)

<span data-ttu-id="edd79-459">Merhaba performans verileri, tooa belirli bir kapsayıcıya hello adını yazarak sorgunuzun sağ toohello görüyorsunuz kapsamını belirleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="edd79-459">You can scope hello performance data you're seeing tooa specific container by typing hello name of it toohello right of your query.</span></span>

```
Type=Perf <containerName>
```

<span data-ttu-id="edd79-460">Tek bir kapsayıcı için toplanan performans ölçümleri hello listesini gösterir.</span><span class="sxs-lookup"><span data-stu-id="edd79-460">That shows hello list of performance metrics that are collected for an individual container.</span></span>

![kapsayıcıları performansı](./media/log-analytics-containers/containers-perf03.png)

## <a name="example-log-search-queries"></a><span data-ttu-id="edd79-462">Örnek günlük arama sorguları</span><span class="sxs-lookup"><span data-stu-id="edd79-462">Example log search queries</span></span>
<span data-ttu-id="edd79-463">Genellikle yararlı toobuild ortamınızın bir örnek veya iki ile başlayan ve bunları toofit değiştirme sorgular.</span><span class="sxs-lookup"><span data-stu-id="edd79-463">It's often useful toobuild queries starting with an example or two and then modifying them toofit your environment.</span></span> <span data-ttu-id="edd79-464">Bir başlangıç noktası olarak ile Merhaba deneyebilirsiniz **örnek sorgular** alanı toohelp daha gelişmiş sorgular oluşturun.</span><span class="sxs-lookup"><span data-stu-id="edd79-464">As a starting point, you can experiment with hello **Sample Queries** area toohelp you build more advanced queries.</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Kapsayıcıları sorguları](./media/log-analytics-containers/containers-queries.png)


## <a name="saving-log-search-queries"></a><span data-ttu-id="edd79-466">Arama sorguları günlük kaydetme</span><span class="sxs-lookup"><span data-stu-id="edd79-466">Saving log search queries</span></span>
<span data-ttu-id="edd79-467">Sorguları kaydetme günlük analizi standart bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="edd79-467">Saving queries is a standard feature in Log Analytics.</span></span> <span data-ttu-id="edd79-468">Bunları kaydederek yararlı buldunuz o gerekir gelecekte kullanım için kullanışlı.</span><span class="sxs-lookup"><span data-stu-id="edd79-468">By saving them, you'll have those that you've found useful handy for future use.</span></span>

<span data-ttu-id="edd79-469">Size kullanışlı bir sorgu oluşturduktan sonra tıklayarak Kaydet **Sık Kullanılanlar** hello sayfanın üst kısmındaki hello günlük arama.</span><span class="sxs-lookup"><span data-stu-id="edd79-469">After you create a query that you find useful, save it by clicking **Favorites** at hello top of hello Log Search page.</span></span> <span data-ttu-id="edd79-470">Kolayca daha sonra hello erişebildiğinizi sonra **My Pano** sayfası.</span><span class="sxs-lookup"><span data-stu-id="edd79-470">Then you can easily access it later from hello **My Dashboard** page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="edd79-471">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="edd79-471">Next steps</span></span>
* <span data-ttu-id="edd79-472">[Arama günlüklerini](log-analytics-log-searches.md) tooview ayrıntılı kapsayıcı verileri kaydeder.</span><span class="sxs-lookup"><span data-stu-id="edd79-472">[Search logs](log-analytics-log-searches.md) tooview detailed container data records.</span></span>
