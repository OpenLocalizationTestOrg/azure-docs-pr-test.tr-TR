---
title: "Azure Remoteapp'te SQL Server Management Studio kullanarak veritabanı aaaConnect tooSQL | Microsoft Docs"
description: "Bu öğretici toolearn kullanma toouse SQL Server Management Studio'da Azure RemoteApp üzerinde güvenlik ve tooSQL veritabanına bağlanırken performansı"
services: sql-database
documentationcenter: 
author: adhurwit
manager: jhubbard
ms.assetid: 1052c83c-e7f5-4736-922f-216194d8874b
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: adhurwit
ms.openlocfilehash: 73994f9a1eb3e48efa5d7c4f976b00cfcbc88d75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-sql-server-management-studio-in-azure-remoteapp-tooconnect-toosql-database"></a><span data-ttu-id="48dcb-103">Azure RemoteApp tooconnect tooSQL veritabanı SQL Server Management Studio'yu kullanın</span><span class="sxs-lookup"><span data-stu-id="48dcb-103">Use SQL Server Management Studio in Azure RemoteApp tooconnect tooSQL Database</span></span>

> [!IMPORTANT]
> <span data-ttu-id="48dcb-104">Azure RemoteApp kullanımdan kaldırılıyor.</span><span class="sxs-lookup"><span data-stu-id="48dcb-104">Azure RemoteApp is being discontinued.</span></span> <span data-ttu-id="48dcb-105">Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="48dcb-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
>

## <a name="introduction"></a><span data-ttu-id="48dcb-106">Giriş</span><span class="sxs-lookup"><span data-stu-id="48dcb-106">Introduction</span></span>
<span data-ttu-id="48dcb-107">Bu öğretici şunların nasıl yapıldığını gösterir Azure RemoteApp tooconnect tooSQL veritabanı içinde toouse SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="48dcb-107">This tutorial shows you how toouse SQL Server Management Studio (SSMS) in Azure RemoteApp tooconnect tooSQL Database.</span></span> <span data-ttu-id="48dcb-108">SQL Server Management Studio'da Azure RemoteApp kurma hello işlem size yol göstermektedir, hello avantajlar açıklanır ve Azure Active Directory'de kullanabileceğiniz güvenlik özellikleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="48dcb-108">It walks you through hello process of setting up SQL Server Management Studio in Azure RemoteApp, explains hello benefits, and shows security features that you can use in Azure Active Directory.</span></span>

<span data-ttu-id="48dcb-109">**Zaman toocomplete tahmini:** 45 dakika</span><span class="sxs-lookup"><span data-stu-id="48dcb-109">**Estimated time toocomplete:** 45 minutes</span></span>

## <a name="ssms-in-azure-remoteapp"></a><span data-ttu-id="48dcb-110">Azure RemoteApp SSMS</span><span class="sxs-lookup"><span data-stu-id="48dcb-110">SSMS in Azure RemoteApp</span></span>
<span data-ttu-id="48dcb-111">Azure RemoteApp, uygulamalar sunuyor Azure RDS hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="48dcb-111">Azure RemoteApp is an RDS service in Azure that delivers applications.</span></span> <span data-ttu-id="48dcb-112">Daha fazla bilgi aşağıda öğrenebilirsiniz: [RemoteApp nedir?](../remoteapp/remoteapp-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="48dcb-112">You can learn more about it here: [What is RemoteApp?](../remoteapp/remoteapp-whatis.md)</span></span>

<span data-ttu-id="48dcb-113">Azure RemoteApp verir çalıştıran SSMS SSMS yerel olarak çalışan olarak aynı deneyimi hello.</span><span class="sxs-lookup"><span data-stu-id="48dcb-113">SSMS running in Azure RemoteApp gives you hello same experience as running SSMS locally.</span></span>

![Azure Remoteapp'te çalıştıran SSMS gösteren ekran görüntüsü][1]

## <a name="benefits"></a><span data-ttu-id="48dcb-115">Avantajlar</span><span class="sxs-lookup"><span data-stu-id="48dcb-115">Benefits</span></span>
<span data-ttu-id="48dcb-116">Birçok avantajları toousing Azure RemoteApp SSMS vardır dahil olmak üzere:</span><span class="sxs-lookup"><span data-stu-id="48dcb-116">There are many benefits toousing SSMS in Azure RemoteApp, including:</span></span>

* <span data-ttu-id="48dcb-117">Azure SQL Server 1433 numaralı bağlantı noktasını (Azure dışında) dışarıdan kullanıma sunulan toobe yok.</span><span class="sxs-lookup"><span data-stu-id="48dcb-117">Port 1433 on Azure SQL server does not have toobe exposed externally (outside of Azure).</span></span>
* <span data-ttu-id="48dcb-118">Ekleme ve IP adreslerini hello Azure SQL server Güvenlik Duvarı'nı kaldırma hiçbir gerek tookeep.</span><span class="sxs-lookup"><span data-stu-id="48dcb-118">No need tookeep adding and removing IP addresses in hello Azure SQL server firewall.</span></span>
* <span data-ttu-id="48dcb-119">Tüm Azure RemoteApp bağlantıları HTTPS üzerinden gerçekleşmesi 443 numaralı bağlantı noktasını kullanarak şifrelenmiş Uzak Masaüstü Protokolü</span><span class="sxs-lookup"><span data-stu-id="48dcb-119">All Azure RemoteApp connections occur over HTTPS on port 443 using encrypted Remote Desktop protocol</span></span>
* <span data-ttu-id="48dcb-120">Çok kullanıcılı ve ölçeklendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48dcb-120">It is multi-user and can scale.</span></span>
* <span data-ttu-id="48dcb-121">SSMS hello sahip öğesinden bir performans kazancı yoktur hello SQL veritabanı ile aynı bölgeye.</span><span class="sxs-lookup"><span data-stu-id="48dcb-121">There is a performance gain from having SSMS in hello same region as hello SQL Database.</span></span>
* <span data-ttu-id="48dcb-122">Azure RemoteApp kullanımı hello Premium edition kullanıcı etkinlik raporları olan Azure Active Directory ile denetleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48dcb-122">You can audit use of Azure RemoteApp with hello Premium edition of Azure Active Directory which has user activity reports.</span></span>
* <span data-ttu-id="48dcb-123">Çok faktörlü kimlik doğrulamasını (MFA) etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48dcb-123">You can enable multi-factor authentication (MFA).</span></span>
* <span data-ttu-id="48dcb-124">Erişim herhangi bir yere hello birini kullanırken SSMS, iOS, Android, Mac, Windows Phone ve Windows bilgisayarın içeren Azure RemoteApp istemcileri desteklenir.</span><span class="sxs-lookup"><span data-stu-id="48dcb-124">Access SSMS anywhere when using any of hello supported Azure RemoteApp clients which includes iOS, Android, Mac, Windows Phone, and Windows PC’s.</span></span>

## <a name="create-hello-azure-remoteapp-collection"></a><span data-ttu-id="48dcb-125">Hello Azure RemoteApp koleksiyonu oluşturun</span><span class="sxs-lookup"><span data-stu-id="48dcb-125">Create hello Azure RemoteApp collection</span></span>
<span data-ttu-id="48dcb-126">Azure RemoteApp koleksiyonunuzun SSMS ile Merhaba adımları toocreate şunlardır:</span><span class="sxs-lookup"><span data-stu-id="48dcb-126">Here are hello steps toocreate your Azure RemoteApp collection with SSMS:</span></span>

### <a name="1-create-a-new-windows-vm-from-image"></a><span data-ttu-id="48dcb-127">1. Yeni bir Windows VM görüntüsünü oluşturma</span><span class="sxs-lookup"><span data-stu-id="48dcb-127">1. Create a new Windows VM from Image</span></span>
<span data-ttu-id="48dcb-128">Merhaba "Windows Server Uzak Masaüstü Oturumu Ana bilgisayar Windows Server 2012 R2" Merhaba galeri toomake görüntüden yeni VM'nin kullanın.</span><span class="sxs-lookup"><span data-stu-id="48dcb-128">Use hello "Windows Server Remote Desktop Session Host Windows Server 2012 R2" Image from hello Gallery toomake your new VM.</span></span>

### <a name="2-install-ssms-from-sql-express"></a><span data-ttu-id="48dcb-129">2. SSMS SQL hızlı yükleme</span><span class="sxs-lookup"><span data-stu-id="48dcb-129">2. Install SSMS from SQL Express</span></span>
<span data-ttu-id="48dcb-130">Üzerine gidin yeni VM hello ve toothis indirme sayfasına gidin: [Microsoft® SQL Server® 2014 Express](https://www.microsoft.com/download/details.aspx?id=42299)</span><span class="sxs-lookup"><span data-stu-id="48dcb-130">Go onto hello new VM and navigate toothis download page: [Microsoft® SQL Server® 2014 Express](https://www.microsoft.com/download/details.aspx?id=42299)</span></span>

<span data-ttu-id="48dcb-131">Bir seçenek tooonly indirme SSMS yoktur.</span><span class="sxs-lookup"><span data-stu-id="48dcb-131">There is an option tooonly download SSMS.</span></span> <span data-ttu-id="48dcb-132">Yükleme sonra hello yükleme dizinine gidin ve Kurulum tooinstall SSMS çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="48dcb-132">After download, go into hello install directory and run Setup tooinstall SSMS.</span></span>

<span data-ttu-id="48dcb-133">Ayrıca SQL Server 2014 Service Pack 1 tooinstall gerekir.</span><span class="sxs-lookup"><span data-stu-id="48dcb-133">You also need tooinstall SQL Server 2014 Service Pack 1.</span></span> <span data-ttu-id="48dcb-134">Buradan indirebilirsiniz: [Microsoft SQL Server 2014 Service Pack 1 (SP1)](https://www.microsoft.com/download/details.aspx?id=46694)</span><span class="sxs-lookup"><span data-stu-id="48dcb-134">You can download it here: [Microsoft SQL Server 2014 Service Pack 1 (SP1)](https://www.microsoft.com/download/details.aspx?id=46694)</span></span>

<span data-ttu-id="48dcb-135">SQL Server 2014 Service Pack 1 Azure SQL veritabanı ile çalışmak için gerekli işlevselliği içerir.</span><span class="sxs-lookup"><span data-stu-id="48dcb-135">SQL Server 2014 Service Pack 1 includes essential functionality for working with Azure SQL Database.</span></span>

### <a name="3-run-validate-script-and-sysprep"></a><span data-ttu-id="48dcb-136">3. Doğrulama betiği çalıştırma ve Sysprep</span><span class="sxs-lookup"><span data-stu-id="48dcb-136">3. Run Validate script and Sysprep</span></span>
<span data-ttu-id="48dcb-137">Üzerinde Hello hello VM masaüstünün doğrulama adlı bir PowerShell komut dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="48dcb-137">On hello desktop of hello VM is a PowerShell script called Validate.</span></span> <span data-ttu-id="48dcb-138">Bu, çift tıklayarak dosyayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="48dcb-138">Run this by double-clicking.</span></span> <span data-ttu-id="48dcb-139">Bu hello VM uzak uygulamaları barındırmak için kullanılan hazır toobe olduğunu doğrular.</span><span class="sxs-lookup"><span data-stu-id="48dcb-139">It will verify that hello VM is ready toobe used for remote hosting of applications.</span></span> <span data-ttu-id="48dcb-140">Doğrulama tamamlandığında toorun sysprep - ister toorun seçin.</span><span class="sxs-lookup"><span data-stu-id="48dcb-140">When verification is complete, it will ask toorun sysprep - choose toorun it.</span></span>

<span data-ttu-id="48dcb-141">Sysprep tamamlandığında VM hello kapanır.</span><span class="sxs-lookup"><span data-stu-id="48dcb-141">When sysprep completes, it will shut down hello VM.</span></span>

<span data-ttu-id="48dcb-142">bir Azure RemoteApp görüntüsü oluşturma hakkında daha fazla toolearn bakın: [nasıl toocreate RemoteApp şablon görüntüsü ile Azure](http://blogs.msdn.com/b/rds/archive/2015/03/17/how-to-create-a-remoteapp-template-image-in-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="48dcb-142">toolearn more about creating a Azure RemoteApp image, see: [How toocreate a RemoteApp template image in Azure](http://blogs.msdn.com/b/rds/archive/2015/03/17/how-to-create-a-remoteapp-template-image-in-azure.aspx)</span></span>

### <a name="4-capture-image"></a><span data-ttu-id="48dcb-143">4. Yansıma Yakalama</span><span class="sxs-lookup"><span data-stu-id="48dcb-143">4. Capture image</span></span>
<span data-ttu-id="48dcb-144">Ne zaman VM, durdu hello hello geçerli portalında bulun ve yakalayın.</span><span class="sxs-lookup"><span data-stu-id="48dcb-144">When hello VM has stopped running, find it in hello current portal and capture it.</span></span>

<span data-ttu-id="48dcb-145">bir görüntü yakalama hakkında daha fazla toolearn bakın [hello Klasik dağıtım modeli kullanılarak oluşturulmuş bir Azure Windows sanal makine bir görüntüsünü yakalama](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="48dcb-145">toolearn more about capturing an image, see [Capture an image of an Azure Windows virtual machine created with hello classic deployment model](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

### <a name="5-add-tooazure-remoteapp-template-images"></a><span data-ttu-id="48dcb-146">5. TooAzure RemoteApp şablon görüntüleri ekleme</span><span class="sxs-lookup"><span data-stu-id="48dcb-146">5. Add tooAzure RemoteApp Template images</span></span>
<span data-ttu-id="48dcb-147">Hello hello geçerli portal Azure RemoteApp bölümü, toohello şablon görüntüleri sekmesine gidin ve Ekle'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="48dcb-147">In hello Azure RemoteApp section of hello current portal, go toohello Template Images tab and click Add.</span></span> <span data-ttu-id="48dcb-148">Hello açılır kutusunda "bir görüntü, sanal makineleri kitaplıktan Al" seçin ve ardından hello oluşturduğunuz görüntü seçin.</span><span class="sxs-lookup"><span data-stu-id="48dcb-148">In hello pop-up box, select "Import an image from your Virtual Machines library" and then choose hello Image that you just created.</span></span>

### <a name="6-create-cloud-collection"></a><span data-ttu-id="48dcb-149">6. Bulut koleksiyonu oluşturma</span><span class="sxs-lookup"><span data-stu-id="48dcb-149">6. Create cloud collection</span></span>
<span data-ttu-id="48dcb-150">Hello geçerli Portalı'nda, yeni Azure RemoteApp bulut koleksiyonu oluşturma.</span><span class="sxs-lookup"><span data-stu-id="48dcb-150">In hello current portal, create a new Azure RemoteApp Cloud Collection.</span></span> <span data-ttu-id="48dcb-151">Merhaba şablon görüntüsü yüklü SSMS ile aktardığınız seçin.</span><span class="sxs-lookup"><span data-stu-id="48dcb-151">Choose hello Template Image that you just imported with SSMS installed on it.</span></span>

![Yeni bulut koleksiyonu oluşturma][2]

### <a name="7-publish-ssms"></a><span data-ttu-id="48dcb-153">7. SSMS yayımlama</span><span class="sxs-lookup"><span data-stu-id="48dcb-153">7. Publish SSMS</span></span>
<span data-ttu-id="48dcb-154">Yeni bulut koleksiyonunuzu select Yayımla sekmesinde bir uygulama yayımlama hello üzerinde Başlat menüsü hello ve SSMS hello listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="48dcb-154">On hello Publishing tab of your new cloud collection, select Publish an application from hello Start Menu and then choose SSMS from hello list.</span></span>

![Uygulama yayımlama][5]

### <a name="8-add-users"></a><span data-ttu-id="48dcb-156">8. Kullanıcı ekle</span><span class="sxs-lookup"><span data-stu-id="48dcb-156">8. Add users</span></span>
<span data-ttu-id="48dcb-157">Merhaba kullanıcı erişimini sekmesinde yalnızca SSMS içeren erişim toothis Azure RemoteApp koleksiyonu vardır hello kullanıcılar seçebilir.</span><span class="sxs-lookup"><span data-stu-id="48dcb-157">On hello User Access tab you can select hello users that will have access toothis Azure RemoteApp collection which only includes SSMS.</span></span>

![Kullanıcı Ekleme][6]

### <a name="9-install-hello-azure-remoteapp-client-application"></a><span data-ttu-id="48dcb-159">9. Merhaba Azure RemoteApp istemci uygulaması yükleme</span><span class="sxs-lookup"><span data-stu-id="48dcb-159">9. Install hello Azure RemoteApp client application</span></span>
<span data-ttu-id="48dcb-160">Bir Azure RemoteApp istemcisini yükleyip: [karşıdan | Azure RemoteApp](https://www.remoteapp.windowsazure.com/en/clients.aspx)</span><span class="sxs-lookup"><span data-stu-id="48dcb-160">You can download and install a Azure RemoteApp client here: [Download | Azure RemoteApp](https://www.remoteapp.windowsazure.com/en/clients.aspx)</span></span>

## <a name="configure-azure-sql-server"></a><span data-ttu-id="48dcb-161">Azure SQL server yapılandırma</span><span class="sxs-lookup"><span data-stu-id="48dcb-161">Configure Azure SQL server</span></span>
<span data-ttu-id="48dcb-162">Azure Hizmetleri tooensure gerekli yapılandırma, yalnızca hello hello Güvenlik Duvarı etkin.</span><span class="sxs-lookup"><span data-stu-id="48dcb-162">hello only configuration needed is tooensure that Azure Services is enabled for hello firewall.</span></span> <span data-ttu-id="48dcb-163">Ardından bu çözümü kullanıyorsanız tooadd tüm IP adresleri tooopen hello Güvenlik Duvarı'nı gerekmez.</span><span class="sxs-lookup"><span data-stu-id="48dcb-163">If you use this solution, then you do not need tooadd any IP addresses tooopen hello firewall.</span></span> <span data-ttu-id="48dcb-164">SQL Server toohello izin hello ağ trafiği Azure hizmetlerinden tutulur.</span><span class="sxs-lookup"><span data-stu-id="48dcb-164">hello network traffic that is allowed toohello SQL Server is from other Azure services.</span></span>

![Azure izin ver][4]

## <a name="multi-factor-authentication-mfa"></a><span data-ttu-id="48dcb-166">Çok faktörlü kimlik doğrulaması (MFA)</span><span class="sxs-lookup"><span data-stu-id="48dcb-166">Multi-Factor Authentication (MFA)</span></span>
<span data-ttu-id="48dcb-167">MFA bu uygulama için özel olarak etkinleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="48dcb-167">MFA can be enabled for this application specifically.</span></span> <span data-ttu-id="48dcb-168">Azure Active Directory'yi toohello uygulamalar sekmesine gidin.</span><span class="sxs-lookup"><span data-stu-id="48dcb-168">Go toohello Applications tab of your Azure Active Directory.</span></span> <span data-ttu-id="48dcb-169">Microsoft Azure RemoteApp için bir giriş bulacaksınız.</span><span class="sxs-lookup"><span data-stu-id="48dcb-169">You will find an entry for Microsoft Azure RemoteApp.</span></span> <span data-ttu-id="48dcb-170">Bu uygulama'yı tıklatın ve ardından yapılandırma hello sayfası aşağıdaki burada bu uygulama için MFA etkinleştirebilirsiniz görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="48dcb-170">If you click that application and then configure, you will see hello page below where you can enable MFA for this application.</span></span>

![MFA'yı etkinleştirin][3]

## <a name="audit-user-activity-with-azure-active-directory-premium"></a><span data-ttu-id="48dcb-172">Azure Active Directory Premium ile kullanıcı etkinliğini denetleyin</span><span class="sxs-lookup"><span data-stu-id="48dcb-172">Audit user activity with Azure Active Directory Premium</span></span>
<span data-ttu-id="48dcb-173">Tooturn sahip sonra Azure AD Premium, yoksa, üzerinde hello dizininizin lisansları bölümü.</span><span class="sxs-lookup"><span data-stu-id="48dcb-173">If you do not have Azure AD Premium, then you have tooturn it on in hello Licenses section of your directory.</span></span> <span data-ttu-id="48dcb-174">Etkin Premium ile toohello Premium düzeyi kullanıcılar atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48dcb-174">With Premium enabled, you can assign users toohello Premium level.</span></span>

<span data-ttu-id="48dcb-175">Azure Active Directory'yi tooa kullanıcı olduğunuzda, ardından toohello etkinlik sekmesini toosee oturum açma bilgileri tooAzure RemoteApp gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48dcb-175">When you go tooa user in your Azure Active Directory, you can then go toohello Activity tab toosee login information tooAzure RemoteApp.</span></span>

## <a name="next-steps"></a><span data-ttu-id="48dcb-176">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="48dcb-176">Next steps</span></span>
<span data-ttu-id="48dcb-177">Tüm hello yukarıdaki adımları tamamladıktan sonra mümkün toorun hello Azure RemoteApp istemcisi ve olması atanmış bir kullanıcı ile oturum aç.</span><span class="sxs-lookup"><span data-stu-id="48dcb-177">After completing all hello above steps, you will be able toorun hello Azure RemoteApp client and log-in with an assigned user.</span></span> <span data-ttu-id="48dcb-178">SSMS ile uygulamalarınızı biri olarak sunulur ve bilgisayarınızda erişim tooAzure SQL server ile yüklenmişse, gibi çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48dcb-178">You will be presented with SSMS as one of your applications, and you can run it as you would if it were installed on your computer with access tooAzure SQL server.</span></span>

<span data-ttu-id="48dcb-179">Nasıl toomake hello bağlantı tooSQL veritabanı ile ilgili daha fazla bilgi için bkz: [tooSQL veritabanı SQL Server Management Studio ile bağlanma ve örnek T-SQL sorgusu gerçekleştirmeyi](sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="48dcb-179">For more information on how toomake hello connection tooSQL Database, see [Connect tooSQL Database with SQL Server Management Studio and perform a sample T-SQL query](sql-database-connect-query-ssms.md).</span></span>

<span data-ttu-id="48dcb-180">Her şeyi şimdilik olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="48dcb-180">That's everything for now.</span></span> <span data-ttu-id="48dcb-181">Keyfini çıkarın!</span><span class="sxs-lookup"><span data-stu-id="48dcb-181">Enjoy!</span></span>

<!--Image references-->
[1]: ./media/sql-database-ssms-remoteapp/ssms.png
[2]: ./media/sql-database-ssms-remoteapp/newcloudcollection.png
[3]: ./media/sql-database-ssms-remoteapp/mfa.png
[4]: ./media/sql-database-ssms-remoteapp/allowazure.png
[5]: ./media/sql-database-ssms-remoteapp/publish.png
[6]: ./media/sql-database-ssms-remoteapp/user.png