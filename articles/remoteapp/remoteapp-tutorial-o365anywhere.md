---
title: "aaaGet hello Azure RemoteApp ile herhangi bir cihazda aynı Office 365 deneyimini | Microsoft Docs"
description: "Bilgi nasıl tooshare kullanıcılarınız Azure RemoteApp kullanarak herhangi bir Office 365 uygulama."
services: remoteapp
documentationcenter: 
author: guscatalano
manager: mbaldwin
editor: 
ms.assetid: 0c971ce9-7d45-4cfb-9737-15b6706047e8
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 11/23/2016
ms.author: guscatal;elizapo
ms.openlocfilehash: 140056c22c8c69b9ec605318e35a72b144da07eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-same-office-365-experience-on-any-device-with-azure-remoteapp"></a><span data-ttu-id="ec25b-103">Get hello aynı Azure RemoteApp ile herhangi bir cihazda Office 365 deneyimini</span><span class="sxs-lookup"><span data-stu-id="ec25b-103">Get hello same Office 365 experience on any device with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ec25b-104">Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="ec25b-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="ec25b-105">Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="ec25b-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="ec25b-106">Bu makalede ele alınacaktır nasıl toodeploy Office 365 şirket içinde herhangi bir cihazda.</span><span class="sxs-lookup"><span data-stu-id="ec25b-106">This article will cover how toodeploy Office 365 on any device in your company.</span></span> <span data-ttu-id="ec25b-107">Kullanıcılarınızın aynı yetenekleri hello alabilir ve kullanıcı Arabirimi, Android, Apple ve Windows deneyimi.</span><span class="sxs-lookup"><span data-stu-id="ec25b-107">Your users can get hello same capabilities and UI experience on Android, Apple and Windows.</span></span>

<span data-ttu-id="ec25b-108">Bunu Azure’da kullanıcıların bağlanabileceği ölçeklenebilir sanal makinelerde Office 365’i barındırmak için Azure RemoteApp kullanarak yapabiliriz.</span><span class="sxs-lookup"><span data-stu-id="ec25b-108">We will accomplish this using Azure RemoteApp by hosting Office 365 on scale-able virtual machines in Azure that users can connect to.</span></span> <span data-ttu-id="ec25b-109">Bu sanal makineler kümesi "bulut koleksiyonu" olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="ec25b-109">This set of virtual machines we call a "cloud collection".</span></span>

## <a name="create-a-cloud-collection"></a><span data-ttu-id="ec25b-110">Bulut koleksiyonu oluşturma</span><span class="sxs-lookup"><span data-stu-id="ec25b-110">Create a cloud collection</span></span>
<span data-ttu-id="ec25b-111">Bir Azure hesabı oluşturduktan sonra ilk çok gidin**RemoteApp** yan sol hello hello bağlantısına tıklayarak.</span><span class="sxs-lookup"><span data-stu-id="ec25b-111">First after you have created an Azure account, navigate too**RemoteApp** by clicking on hello link on hello left side.</span></span>
<span data-ttu-id="ec25b-112">![Azure Portal hello üzerinde Azure RemoteApp gösteriliyor](./media/remoteapp-tutorial-o365anywhere/1-menu.png)</span><span class="sxs-lookup"><span data-stu-id="ec25b-112">![Showing Azure RemoteApp on hello Azure Portal](./media/remoteapp-tutorial-o365anywhere/1-menu.png)</span></span>

<span data-ttu-id="ec25b-113">Tıklayarak devam **yeni** hello alt ve "Hızlı oluşturma" bir koleksiyon.</span><span class="sxs-lookup"><span data-stu-id="ec25b-113">Then continue by clicking **new** on hello bottom and "quick creating" a collection.</span></span> <span data-ttu-id="ec25b-114">Ad, hello bölge, hello abonelik, hello plan ve sağlamış olduğumuz "Office Proffesional 2013" hello görüntü sağlar.</span><span class="sxs-lookup"><span data-stu-id="ec25b-114">Provide a name, hello region, hello subscription, hello plan and hello image "Office Proffesional 2013" that we provide.</span></span>
<span data-ttu-id="ec25b-115">![Oluştur İletişim Kutusu](./media/remoteapp-tutorial-o365anywhere/2-quickcreate.png)</span><span class="sxs-lookup"><span data-stu-id="ec25b-115">![Create Dialog](./media/remoteapp-tutorial-o365anywhere/2-quickcreate.png)</span></span>

<span data-ttu-id="ec25b-116">İşiniz bittiğinde hello form hello koleksiyon oluşturma süreci başlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="ec25b-116">Once you finish hello form hello collection creation process should start.</span></span> <span data-ttu-id="ec25b-117">Bu tooan saat veya bunu sürebilir.</span><span class="sxs-lookup"><span data-stu-id="ec25b-117">This may take up tooan hour or so.</span></span>

![Bekleniyor](./media/remoteapp-tutorial-o365anywhere/3-waiting.png)

<span data-ttu-id="ec25b-119">Merhaba işlem tamamlandığında, aşağıdakine benzer görünecektir.</span><span class="sxs-lookup"><span data-stu-id="ec25b-119">Once hello process is done, it will look something like this.</span></span> <span data-ttu-id="ec25b-120">**Yayımlama**’ya tıkladığımızda, çoğu Office uygulamasının bizim için zaten yayımlandığını görebiliriz.</span><span class="sxs-lookup"><span data-stu-id="ec25b-120">If we click **Publishing** we can see that most Office applications have been published for us already.</span></span>
<span data-ttu-id="ec25b-121">![Oluşturulan koleksiyon](./media/remoteapp-tutorial-o365anywhere/4-done.png)</span><span class="sxs-lookup"><span data-stu-id="ec25b-121">![Collection created](./media/remoteapp-tutorial-o365anywhere/4-done.png)</span></span>

![Yayımlanan uygulamalar](./media/remoteapp-tutorial-o365anywhere/5-publish.png)

<span data-ttu-id="ec25b-123">Bu noktada ayrıca tıklayarak erişim toothis koleksiyonuna sahip daha fazla kullanıcı ekleyebilirsiniz **kullanıcı erişimini**.</span><span class="sxs-lookup"><span data-stu-id="ec25b-123">At this point you can also add more users that have access toothis collection by clicking **User Access**.</span></span>
<span data-ttu-id="ec25b-124">![Kullanıcı erişimini yapılandırma](./media/remoteapp-tutorial-o365anywhere/6-user.png)</span><span class="sxs-lookup"><span data-stu-id="ec25b-124">![Configure user access](./media/remoteapp-tutorial-o365anywhere/6-user.png)</span></span>

<span data-ttu-id="ec25b-125">Şimdi tooOffice 365 bağlanmayı deneyelim!</span><span class="sxs-lookup"><span data-stu-id="ec25b-125">Now let's try out connecting tooOffice 365!</span></span>

## <a name="connect-toooffice-365"></a><span data-ttu-id="ec25b-126">TooOffice 365 Bağlan</span><span class="sxs-lookup"><span data-stu-id="ec25b-126">Connect tooOffice 365</span></span>
<span data-ttu-id="ec25b-127">Biz üzerinden çok head[https://www.remoteapp.windowsazure.com/](https://www.remoteapp.windowsazure.com/), aşağı kaydırın ve tıklayın **istemcileri indir** kullandığınız hello aygıttaki tooinstall hello Azure RemoteApp istemcisi.</span><span class="sxs-lookup"><span data-stu-id="ec25b-127">We'll head over too[https://www.remoteapp.windowsazure.com/](https://www.remoteapp.windowsazure.com/), scroll down  and click **Download clients** tooinstall hello Azure RemoteApp client on hello device you're on.</span></span> <span data-ttu-id="ec25b-128">Merhaba ekran görüntüleri Windows içindir.</span><span class="sxs-lookup"><span data-stu-id="ec25b-128">hello screenshots below are for Windows.</span></span>

<span data-ttu-id="ec25b-129">Merhaba uygulaması başladıktan sonra (eski adıyla "Live ID") Microsoft hesabınızla oturum toosign istenir, kullanım hello aynı Azure hesabınızda şu an için.</span><span class="sxs-lookup"><span data-stu-id="ec25b-129">Once hello application starts you'll be asked toosign in with your Microsoft account (formerly called a "Live ID"), use hello same one as your Azure account for now.</span></span> <span data-ttu-id="ec25b-130">Oturum açtığınızda yeni davetlerle ilgili bir bildirim görürsünüz, buna tıkladığınızda aşağıdakine benzer bir liste görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="ec25b-130">When you're signed in you should see a notification about new invitations, click there and you should see a list like one below.</span></span> <span data-ttu-id="ec25b-131">Azure hesabı sahibinin e-posta ile eşleşen hello daveti kabul edin.</span><span class="sxs-lookup"><span data-stu-id="ec25b-131">Accept hello invitation that matches your Azure account owner email.</span></span>

![Yeni davet](./media/remoteapp-tutorial-o365anywhere/7-araclient.png)

<span data-ttu-id="ec25b-133">Yeni davetler olduğunda bu şekilde görünür.</span><span class="sxs-lookup"><span data-stu-id="ec25b-133">What it looks like when there are new invitations.</span></span>

![Uygulama kabul etme](./media/remoteapp-tutorial-o365anywhere/8-invitation.png)

<span data-ttu-id="ec25b-135">Merhaba daveti kabul ettikten sonra hello Azure RemoteApp istemcisindeki tüm hello Office uygulamalarını görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ec25b-135">Once you accept hello invitation you should see all hello Office apps in hello Azure RemoteApp client.</span></span>

![Uygulama listesi](./media/remoteapp-tutorial-o365anywhere/9-work.png)

<span data-ttu-id="ec25b-137">Bu Merhaba uygulaması hiçbirinde tıklattığınızda üzerinde hello Azure sanal makinesi ile başlamalı ve, hepsi bu kadar!</span><span class="sxs-lookup"><span data-stu-id="ec25b-137">When you click on any of these hello application should start on hello Azure virtual machine and you should be all set!</span></span> <span data-ttu-id="ec25b-138">Keyfini çıkarın!</span><span class="sxs-lookup"><span data-stu-id="ec25b-138">Enjoy!</span></span>

![başlatma](./media/remoteapp-tutorial-o365anywhere/10-arastart.png)

![powerpoint](./media/remoteapp-tutorial-o365anywhere/11-pp.png)

