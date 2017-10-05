---
title: "Azure Remoteapp'te SQL Server Management Studio'yu kullanarak SQL veritabanına bağlanma | Microsoft Docs"
description: "SQL Server Management Studio Azure Remoteapp'te güvenlik ve performans için SQL veritabanına bağlanırken kullanmayı öğrenmek için bu öğreticiyi kullanın"
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
ms.openlocfilehash: ae1f2fa38d38fe6c10bc7960fddb07ae330d1eeb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-sql-server-management-studio-in-azure-remoteapp-to-connect-to-sql-database"></a><span data-ttu-id="72eea-103">Azure RemoteApp SQL veritabanına bağlanmak için SQL Server Management Studio'yu kullanın</span><span class="sxs-lookup"><span data-stu-id="72eea-103">Use SQL Server Management Studio in Azure RemoteApp to connect to SQL Database</span></span>

> [!IMPORTANT]
> <span data-ttu-id="72eea-104">Azure RemoteApp kullanımdan kaldırılıyor.</span><span class="sxs-lookup"><span data-stu-id="72eea-104">Azure RemoteApp is being discontinued.</span></span> <span data-ttu-id="72eea-105">Ayrıntılı bilgi için [duyuruyu](https://go.microsoft.com/fwlink/?linkid=821148) okuyun.</span><span class="sxs-lookup"><span data-stu-id="72eea-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
>

## <a name="introduction"></a><span data-ttu-id="72eea-106">Giriş</span><span class="sxs-lookup"><span data-stu-id="72eea-106">Introduction</span></span>
<span data-ttu-id="72eea-107">Bu öğretici, SQL Server Management Studio (SSMS) Azure Remoteapp'te SQL veritabanına bağlanmak için nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="72eea-107">This tutorial shows you how to use SQL Server Management Studio (SSMS) in Azure RemoteApp to connect to SQL Database.</span></span> <span data-ttu-id="72eea-108">Azure RemoteApp SQL Server Management Studio'da ayarlama işleminde size yol göstermektedir, yararlarını açıklar ve Azure Active Directory'de kullanabileceğiniz güvenlik özellikleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="72eea-108">It walks you through the process of setting up SQL Server Management Studio in Azure RemoteApp, explains the benefits, and shows security features that you can use in Azure Active Directory.</span></span>

<span data-ttu-id="72eea-109">**Tahmini tamamlanma süresi:** 45 dakika</span><span class="sxs-lookup"><span data-stu-id="72eea-109">**Estimated time to complete:** 45 minutes</span></span>

## <a name="ssms-in-azure-remoteapp"></a><span data-ttu-id="72eea-110">Azure RemoteApp SSMS</span><span class="sxs-lookup"><span data-stu-id="72eea-110">SSMS in Azure RemoteApp</span></span>
<span data-ttu-id="72eea-111">Azure RemoteApp, uygulamalar sunuyor Azure RDS hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="72eea-111">Azure RemoteApp is an RDS service in Azure that delivers applications.</span></span> <span data-ttu-id="72eea-112">Daha fazla bilgi aşağıda öğrenebilirsiniz: [RemoteApp nedir?](../remoteapp/remoteapp-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="72eea-112">You can learn more about it here: [What is RemoteApp?](../remoteapp/remoteapp-whatis.md)</span></span>

<span data-ttu-id="72eea-113">Azure Remoteapp'te çalıştıran SSMS SSMS yerel olarak çalışan olarak aynı deneyimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="72eea-113">SSMS running in Azure RemoteApp gives you the same experience as running SSMS locally.</span></span>

![Azure Remoteapp'te çalıştıran SSMS gösteren ekran görüntüsü][1]

## <a name="benefits"></a><span data-ttu-id="72eea-115">Avantajlar</span><span class="sxs-lookup"><span data-stu-id="72eea-115">Benefits</span></span>
<span data-ttu-id="72eea-116">Azure Remoteapp'te SSMS kullanarak birçok avantajları vardır dahil olmak üzere:</span><span class="sxs-lookup"><span data-stu-id="72eea-116">There are many benefits to using SSMS in Azure RemoteApp, including:</span></span>

* <span data-ttu-id="72eea-117">Azure SQL Server 1433 numaralı bağlantı noktasını (Azure dışında) harici olarak gösterilmesine izin yok.</span><span class="sxs-lookup"><span data-stu-id="72eea-117">Port 1433 on Azure SQL server does not have to be exposed externally (outside of Azure).</span></span>
* <span data-ttu-id="72eea-118">Ekleme ve IP adreslerini Azure SQL server Güvenlik Duvarı'nda kaldırma tutmak gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="72eea-118">No need to keep adding and removing IP addresses in the Azure SQL server firewall.</span></span>
* <span data-ttu-id="72eea-119">Tüm Azure RemoteApp bağlantıları HTTPS üzerinden gerçekleşmesi 443 numaralı bağlantı noktasını kullanarak şifrelenmiş Uzak Masaüstü Protokolü</span><span class="sxs-lookup"><span data-stu-id="72eea-119">All Azure RemoteApp connections occur over HTTPS on port 443 using encrypted Remote Desktop protocol</span></span>
* <span data-ttu-id="72eea-120">Çok kullanıcılı ve ölçeklendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="72eea-120">It is multi-user and can scale.</span></span>
* <span data-ttu-id="72eea-121">SQL veritabanı ile aynı bölgede SSMS sahip öğesinden bir performans kazancı yoktur.</span><span class="sxs-lookup"><span data-stu-id="72eea-121">There is a performance gain from having SSMS in the same region as the SQL Database.</span></span>
* <span data-ttu-id="72eea-122">Azure RemoteApp kullanımı kullanıcı etkinlik raporları olan Azure Active Directory Premium sürümü ile denetleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="72eea-122">You can audit use of Azure RemoteApp with the Premium edition of Azure Active Directory which has user activity reports.</span></span>
* <span data-ttu-id="72eea-123">Çok faktörlü kimlik doğrulamasını (MFA) etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="72eea-123">You can enable multi-factor authentication (MFA).</span></span>
* <span data-ttu-id="72eea-124">Herhangi bir yerden herhangi bir iOS, Android, Mac, Windows Phone ve Windows bilgisayarın içeren desteklenen Azure RemoteApp istemcisinde kullanırken SSMS erişim.</span><span class="sxs-lookup"><span data-stu-id="72eea-124">Access SSMS anywhere when using any of the supported Azure RemoteApp clients which includes iOS, Android, Mac, Windows Phone, and Windows PC’s.</span></span>

## <a name="create-the-azure-remoteapp-collection"></a><span data-ttu-id="72eea-125">Azure RemoteApp koleksiyonu oluşturun</span><span class="sxs-lookup"><span data-stu-id="72eea-125">Create the Azure RemoteApp collection</span></span>
<span data-ttu-id="72eea-126">Azure RemoteApp koleksiyonunuzun SSMS ile oluşturmak için adımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="72eea-126">Here are the steps to create your Azure RemoteApp collection with SSMS:</span></span>

### <a name="1-create-a-new-windows-vm-from-image"></a><span data-ttu-id="72eea-127">1. Yeni bir Windows VM görüntüsünü oluşturma</span><span class="sxs-lookup"><span data-stu-id="72eea-127">1. Create a new Windows VM from Image</span></span>
<span data-ttu-id="72eea-128">"Windows Server Uzak Masaüstü Oturumu Ana bilgisayar Windows Server 2012 R2" görüntü galeriden yeni VM yapmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="72eea-128">Use the "Windows Server Remote Desktop Session Host Windows Server 2012 R2" Image from the Gallery to make your new VM.</span></span>

### <a name="2-install-ssms-from-sql-express"></a><span data-ttu-id="72eea-129">2. SSMS SQL hızlı yükleme</span><span class="sxs-lookup"><span data-stu-id="72eea-129">2. Install SSMS from SQL Express</span></span>
<span data-ttu-id="72eea-130">Yeni VM gidin ve bu indirme sayfasına gidin: [Microsoft® SQL Server® 2014 Express](https://www.microsoft.com/download/details.aspx?id=42299)</span><span class="sxs-lookup"><span data-stu-id="72eea-130">Go onto the new VM and navigate to this download page: [Microsoft® SQL Server® 2014 Express](https://www.microsoft.com/download/details.aspx?id=42299)</span></span>

<span data-ttu-id="72eea-131">Yalnızca SSMS indirmek için bir seçenek yoktur.</span><span class="sxs-lookup"><span data-stu-id="72eea-131">There is an option to only download SSMS.</span></span> <span data-ttu-id="72eea-132">Yükleme sonra yükleme dizinine gidin ve SSMS yüklemek için Kurulumu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="72eea-132">After download, go into the install directory and run Setup to install SSMS.</span></span>

<span data-ttu-id="72eea-133">Ayrıca SQL Server 2014 Service Pack 1 yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="72eea-133">You also need to install SQL Server 2014 Service Pack 1.</span></span> <span data-ttu-id="72eea-134">Buradan indirebilirsiniz: [Microsoft SQL Server 2014 Service Pack 1 (SP1)](https://www.microsoft.com/download/details.aspx?id=46694)</span><span class="sxs-lookup"><span data-stu-id="72eea-134">You can download it here: [Microsoft SQL Server 2014 Service Pack 1 (SP1)](https://www.microsoft.com/download/details.aspx?id=46694)</span></span>

<span data-ttu-id="72eea-135">SQL Server 2014 Service Pack 1 Azure SQL veritabanı ile çalışmak için gerekli işlevselliği içerir.</span><span class="sxs-lookup"><span data-stu-id="72eea-135">SQL Server 2014 Service Pack 1 includes essential functionality for working with Azure SQL Database.</span></span>

### <a name="3-run-validate-script-and-sysprep"></a><span data-ttu-id="72eea-136">3. Doğrulama betiği çalıştırma ve Sysprep</span><span class="sxs-lookup"><span data-stu-id="72eea-136">3. Run Validate script and Sysprep</span></span>
<span data-ttu-id="72eea-137">VM masaüstünde bir PowerShell Betiği doğrula adı verilir.</span><span class="sxs-lookup"><span data-stu-id="72eea-137">On the desktop of the VM is a PowerShell script called Validate.</span></span> <span data-ttu-id="72eea-138">Bu, çift tıklayarak dosyayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="72eea-138">Run this by double-clicking.</span></span> <span data-ttu-id="72eea-139">VM uzak uygulamaları barındırmak için kullanıma hazır olduğunu doğrular.</span><span class="sxs-lookup"><span data-stu-id="72eea-139">It will verify that the VM is ready to be used for remote hosting of applications.</span></span> <span data-ttu-id="72eea-140">Doğrulama tamamlandıktan sonra ister Sysprep'i-çalıştırmak seçin.</span><span class="sxs-lookup"><span data-stu-id="72eea-140">When verification is complete, it will ask to run sysprep - choose to run it.</span></span>

<span data-ttu-id="72eea-141">Sysprep tamamlandığında VM kapatma.</span><span class="sxs-lookup"><span data-stu-id="72eea-141">When sysprep completes, it will shut down the VM.</span></span>

<span data-ttu-id="72eea-142">Azure RemoteApp görüntüsü oluşturma hakkında daha fazla bilgi için bkz: [Azure RemoteApp şablon görüntüsü oluşturma](http://blogs.msdn.com/b/rds/archive/2015/03/17/how-to-create-a-remoteapp-template-image-in-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="72eea-142">To learn more about creating a Azure RemoteApp image, see: [How to create a RemoteApp template image in Azure](http://blogs.msdn.com/b/rds/archive/2015/03/17/how-to-create-a-remoteapp-template-image-in-azure.aspx)</span></span>

### <a name="4-capture-image"></a><span data-ttu-id="72eea-143">4. Yansıma Yakalama</span><span class="sxs-lookup"><span data-stu-id="72eea-143">4. Capture image</span></span>
<span data-ttu-id="72eea-144">VM çalışmayı durdurdu geçerli portalında bulun ve yakalayın.</span><span class="sxs-lookup"><span data-stu-id="72eea-144">When the VM has stopped running, find it in the current portal and capture it.</span></span>

<span data-ttu-id="72eea-145">Yansıma yakalama hakkında daha fazla bilgi için bkz: [Klasik dağıtım modeli kullanılarak oluşturulmuş bir Azure Windows sanal makine bir görüntüsünü yakalama](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="72eea-145">To learn more about capturing an image, see [Capture an image of an Azure Windows virtual machine created with the classic deployment model](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

### <a name="5-add-to-azure-remoteapp-template-images"></a><span data-ttu-id="72eea-146">5. Azure RemoteApp şablon görüntüleri ekleme</span><span class="sxs-lookup"><span data-stu-id="72eea-146">5. Add to Azure RemoteApp Template images</span></span>
<span data-ttu-id="72eea-147">Geçerli portal Azure RemoteApp bölümünde, şablon görüntüleri sekmesine gidin ve Ekle'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="72eea-147">In the Azure RemoteApp section of the current portal, go to the Template Images tab and click Add.</span></span> <span data-ttu-id="72eea-148">Açılır kutusunda "bir görüntü, sanal makineleri kitaplıktan Al" seçin ve ardından yeni oluşturduğunuz görüntüyü seçin.</span><span class="sxs-lookup"><span data-stu-id="72eea-148">In the pop-up box, select "Import an image from your Virtual Machines library" and then choose the Image that you just created.</span></span>

### <a name="6-create-cloud-collection"></a><span data-ttu-id="72eea-149">6. Bulut koleksiyonu oluşturma</span><span class="sxs-lookup"><span data-stu-id="72eea-149">6. Create cloud collection</span></span>
<span data-ttu-id="72eea-150">Geçerli portalında yeni bir Azure RemoteApp bulut koleksiyonu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="72eea-150">In the current portal, create a new Azure RemoteApp Cloud Collection.</span></span> <span data-ttu-id="72eea-151">Yeni içeri aktardığınız şablon görüntüsü yüklü SSMS ile seçin.</span><span class="sxs-lookup"><span data-stu-id="72eea-151">Choose the Template Image that you just imported with SSMS installed on it.</span></span>

![Yeni bulut koleksiyonu oluşturma][2]

### <a name="7-publish-ssms"></a><span data-ttu-id="72eea-153">7. SSMS yayımlama</span><span class="sxs-lookup"><span data-stu-id="72eea-153">7. Publish SSMS</span></span>
<span data-ttu-id="72eea-154">Yayımlama, yeni bulut koleksiyonu seçme sekmesinde Başlat menüsünden uygulama yayımlama ve SSMS listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="72eea-154">On the Publishing tab of your new cloud collection, select Publish an application from the Start Menu and then choose SSMS from the list.</span></span>

![Uygulama yayımlama][5]

### <a name="8-add-users"></a><span data-ttu-id="72eea-156">8. Kullanıcı ekle</span><span class="sxs-lookup"><span data-stu-id="72eea-156">8. Add users</span></span>
<span data-ttu-id="72eea-157">Kullanıcı erişim sekmesinde yalnızca SSMS içeren bu Azure RemoteApp koleksiyonu erişebilecek kullanıcıları seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="72eea-157">On the User Access tab you can select the users that will have access to this Azure RemoteApp collection which only includes SSMS.</span></span>

![Kullanıcı Ekleme][6]

### <a name="9-install-the-azure-remoteapp-client-application"></a><span data-ttu-id="72eea-159">9. Azure RemoteApp istemci uygulaması yükleme</span><span class="sxs-lookup"><span data-stu-id="72eea-159">9. Install the Azure RemoteApp client application</span></span>
<span data-ttu-id="72eea-160">Bir Azure RemoteApp istemcisini yükleyip: [karşıdan | Azure RemoteApp](https://www.remoteapp.windowsazure.com/en/clients.aspx)</span><span class="sxs-lookup"><span data-stu-id="72eea-160">You can download and install a Azure RemoteApp client here: [Download | Azure RemoteApp](https://www.remoteapp.windowsazure.com/en/clients.aspx)</span></span>

## <a name="configure-azure-sql-server"></a><span data-ttu-id="72eea-161">Azure SQL server yapılandırma</span><span class="sxs-lookup"><span data-stu-id="72eea-161">Configure Azure SQL server</span></span>
<span data-ttu-id="72eea-162">Gerekli yalnızca Azure Hizmetleri için güvenlik duvarını etkinleştirildiğinden emin olmak için yapılandırmadır.</span><span class="sxs-lookup"><span data-stu-id="72eea-162">The only configuration needed is to ensure that Azure Services is enabled for the firewall.</span></span> <span data-ttu-id="72eea-163">Ardından bu çözümü kullanıyorsanız, Güvenlik Duvarı'nı açmak için herhangi bir IP adresi eklemek gerekmez.</span><span class="sxs-lookup"><span data-stu-id="72eea-163">If you use this solution, then you do not need to add any IP addresses to open the firewall.</span></span> <span data-ttu-id="72eea-164">SQL Server için izin verilen ağ trafiği Azure hizmetlerinden tutulur.</span><span class="sxs-lookup"><span data-stu-id="72eea-164">The network traffic that is allowed to the SQL Server is from other Azure services.</span></span>

![Azure izin ver][4]

## <a name="multi-factor-authentication-mfa"></a><span data-ttu-id="72eea-166">Çok faktörlü kimlik doğrulaması (MFA)</span><span class="sxs-lookup"><span data-stu-id="72eea-166">Multi-Factor Authentication (MFA)</span></span>
<span data-ttu-id="72eea-167">MFA bu uygulama için özel olarak etkinleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="72eea-167">MFA can be enabled for this application specifically.</span></span> <span data-ttu-id="72eea-168">Azure Active Directory'yi uygulamalar sekmesine gidin.</span><span class="sxs-lookup"><span data-stu-id="72eea-168">Go to the Applications tab of your Azure Active Directory.</span></span> <span data-ttu-id="72eea-169">Microsoft Azure RemoteApp için bir giriş bulacaksınız.</span><span class="sxs-lookup"><span data-stu-id="72eea-169">You will find an entry for Microsoft Azure RemoteApp.</span></span> <span data-ttu-id="72eea-170">Bu uygulama'yı tıklatın ve ardından yapılandırın, bu uygulama için MFA etkinleştirebilirsiniz sayfası aşağıdaki görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="72eea-170">If you click that application and then configure, you will see the page below where you can enable MFA for this application.</span></span>

![MFA'yı etkinleştirin][3]

## <a name="audit-user-activity-with-azure-active-directory-premium"></a><span data-ttu-id="72eea-172">Azure Active Directory Premium ile kullanıcı etkinliğini denetleyin</span><span class="sxs-lookup"><span data-stu-id="72eea-172">Audit user activity with Azure Active Directory Premium</span></span>
<span data-ttu-id="72eea-173">Azure AD Premium yoksa dizininize lisansları bölümünde Aç sahip.</span><span class="sxs-lookup"><span data-stu-id="72eea-173">If you do not have Azure AD Premium, then you have to turn it on in the Licenses section of your directory.</span></span> <span data-ttu-id="72eea-174">Etkin Premium ile Premium düzeyine kullanıcılar atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="72eea-174">With Premium enabled, you can assign users to the Premium level.</span></span>

<span data-ttu-id="72eea-175">Azure Active Directory'de bir kullanıcıya gidin, sonra Azure RemoteApp için oturum açma bilgilerini görmek için etkinlik sekmesini gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="72eea-175">When you go to a user in your Azure Active Directory, you can then go to the Activity tab to see login information to Azure RemoteApp.</span></span>

## <a name="next-steps"></a><span data-ttu-id="72eea-176">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="72eea-176">Next steps</span></span>
<span data-ttu-id="72eea-177">Yukarıdaki adımları tamamladıktan sonra Azure RemoteApp istemci çalıştırılabilir ve oturum açma atanmış bir kullanıcı ile olacaktır.</span><span class="sxs-lookup"><span data-stu-id="72eea-177">After completing all the above steps, you will be able to run the Azure RemoteApp client and log-in with an assigned user.</span></span> <span data-ttu-id="72eea-178">SSMS ile uygulamalarınızı biri olarak sunulur ve Azure SQL sunucusuna erişimi olan bilgisayarınızda yüklenmişse, gibi çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="72eea-178">You will be presented with SSMS as one of your applications, and you can run it as you would if it were installed on your computer with access to Azure SQL server.</span></span>

<span data-ttu-id="72eea-179">SQL veritabanına bağlantı yapma hakkında daha fazla bilgi için bkz: [SQL Server Management Studio ile SQL veritabanına bağlanma ve örnek T-SQL sorgusu gerçekleştirmeyi](sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="72eea-179">For more information on how to make the connection to SQL Database, see [Connect to SQL Database with SQL Server Management Studio and perform a sample T-SQL query](sql-database-connect-query-ssms.md).</span></span>

<span data-ttu-id="72eea-180">Her şeyi şimdilik olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="72eea-180">That's everything for now.</span></span> <span data-ttu-id="72eea-181">Keyfini çıkarın!</span><span class="sxs-lookup"><span data-stu-id="72eea-181">Enjoy!</span></span>

<!--Image references-->
[1]: ./media/sql-database-ssms-remoteapp/ssms.png
[2]: ./media/sql-database-ssms-remoteapp/newcloudcollection.png
[3]: ./media/sql-database-ssms-remoteapp/mfa.png
[4]: ./media/sql-database-ssms-remoteapp/allowazure.png
[5]: ./media/sql-database-ssms-remoteapp/publish.png
[6]: ./media/sql-database-ssms-remoteapp/user.png