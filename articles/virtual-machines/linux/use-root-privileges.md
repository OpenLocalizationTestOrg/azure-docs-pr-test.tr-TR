---
title: "Linux sanal makinelerde aaaUse kök ayrıcalıkları | Microsoft Docs"
description: "Azure'da bir Linux sanal makinede nasıl toouse kök ayrıcalıkları öğrenin."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: a2c106a2-dceb-43a3-9dd1-50ed77685952
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 9411588c5fd0c86c4c73b3e44fbb56ab150013d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-root-privileges-on-linux-virtual-machines-in-azure"></a><span data-ttu-id="640ed-103">Azure'daki Linux sanal makinelerinde kök ayrıcalıkları kullanma</span><span class="sxs-lookup"><span data-stu-id="640ed-103">Using root privileges on Linux virtual machines in Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="640ed-104">Varsayılan olarak, hello `root` kullanıcı azure'daki Linux sanal makinelerde devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="640ed-104">By default, hello `root` user is disabled on Linux virtual machines in Azure.</span></span> <span data-ttu-id="640ed-105">Kullanıcılar çalışma komutları yükseltilmiş ayrıcalıklarla hello kullanarak `sudo` komutu.</span><span class="sxs-lookup"><span data-stu-id="640ed-105">Users can run commands with elevated privileges by using hello `sudo` command.</span></span> <span data-ttu-id="640ed-106">Ancak, hello deneyimi nasıl hello sistem sağlanan bağlı olarak değişebilir.</span><span class="sxs-lookup"><span data-stu-id="640ed-106">However, hello experience may vary depending on how hello system was provisioned.</span></span>

1. <span data-ttu-id="640ed-107">**SSH anahtarı ve parola veya parola yalnızca** -hello sanal makine ya da bir sertifika ile sağlanan (`.CER` dosyası) veya SSH anahtarı hem de bir parola veya yalnızca bir kullanıcı adı ve parola.</span><span class="sxs-lookup"><span data-stu-id="640ed-107">**SSH key and password OR password only** - hello virtual machine was provisioned with either a certificate (`.CER` file) or SSH key as well as a password, or just a user name and password.</span></span> <span data-ttu-id="640ed-108">Bu durumda `sudo` hello kullanıcının parolasını hello komutu yürütmeden önce sizden onay ister.</span><span class="sxs-lookup"><span data-stu-id="640ed-108">In this case `sudo` will prompt for hello user's password before executing hello command.</span></span>
2. <span data-ttu-id="640ed-109">**SSH anahtarı yalnızca** -hello sanal makine bir sertifika ile sağlanan (`.cer`, `.pem`, veya `.pub` dosya) veya SSH anahtarı ancak parola yok.</span><span class="sxs-lookup"><span data-stu-id="640ed-109">**SSH key only** - hello virtual machine was provisioned with a certificate (`.cer`, `.pem`, or `.pub` file) or SSH key, but no password.</span></span>  <span data-ttu-id="640ed-110">Bu durumda `sudo` **almayacak** hello kullanıcının parolasını hello komutu yürütmeden önce sor.</span><span class="sxs-lookup"><span data-stu-id="640ed-110">In this case `sudo` **will not** prompt for hello user's password before executing hello command.</span></span>

## <a name="ssh-key-and-password-or-password-only"></a><span data-ttu-id="640ed-111">SSH anahtarı ve parola veya parola yalnızca</span><span class="sxs-lookup"><span data-stu-id="640ed-111">SSH Key and Password, or Password Only</span></span>
<span data-ttu-id="640ed-112">Merhaba Linux SSH anahtarı veya parola kimlik doğrulaması kullanarak sanal makine oturum açın, sonra kullanarak komutları çalıştırmak `sudo`, örneğin:</span><span class="sxs-lookup"><span data-stu-id="640ed-112">Log into hello Linux virtual machine using SSH key or password authentication, then run commands using `sudo`, for example:</span></span>

    # sudo <command>
    [sudo] password for azureuser:

<span data-ttu-id="640ed-113">Bu durumda hello kullanıcı için bir parola istenir.</span><span class="sxs-lookup"><span data-stu-id="640ed-113">In this case hello user will be prompted for a password.</span></span> <span data-ttu-id="640ed-114">Merhaba parola girdikten sonra `sudo` hello komutuyla çalışacak `root` ayrıcalıkları.</span><span class="sxs-lookup"><span data-stu-id="640ed-114">After entering hello password `sudo` will run hello command with `root` privileges.</span></span>

<span data-ttu-id="640ed-115">Merhaba düzenleyerek passwordless sudo etkinleştirebilirsiniz `/etc/sudoers.d/waagent` dosya, örneğin:</span><span class="sxs-lookup"><span data-stu-id="640ed-115">You can also enable passwordless sudo by editing hello `/etc/sudoers.d/waagent` file, for example:</span></span>

    #/etc/sudoers.d/waagent
    azureuser ALL = (ALL) NOPASSWD: ALL

<span data-ttu-id="640ed-116">Bu değişiklik, "azureuser" Merhaba kullanıcı tarafından passwordless sudo için izin verir.</span><span class="sxs-lookup"><span data-stu-id="640ed-116">This change will allow for passwordless sudo by hello user "azureuser".</span></span>

## <a name="ssh-key-only"></a><span data-ttu-id="640ed-117">SSH yalnızca anahtar</span><span class="sxs-lookup"><span data-stu-id="640ed-117">SSH Key Only</span></span>
<span data-ttu-id="640ed-118">Merhaba Linux SSH anahtar kimlik doğrulaması kullanarak sanal makine oturum açın, sonra kullanarak komutları çalıştırmak `sudo`, örneğin:</span><span class="sxs-lookup"><span data-stu-id="640ed-118">Log into hello Linux virtual machine using SSH key authentication, then run commands using `sudo`, for example:</span></span>

    # sudo <command>

<span data-ttu-id="640ed-119">Bu durumda hello kullanıcı olacak **değil** için bir parola istenir.</span><span class="sxs-lookup"><span data-stu-id="640ed-119">In this case hello user will **not** be prompted for a password.</span></span> <span data-ttu-id="640ed-120">Tuşlarına basarak sonra `<enter>`, `sudo` hello komutuyla çalışacak `root` ayrıcalıkları.</span><span class="sxs-lookup"><span data-stu-id="640ed-120">After pressing `<enter>`, `sudo` will run hello command with `root` privileges.</span></span>

