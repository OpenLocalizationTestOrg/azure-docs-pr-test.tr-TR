---
title: "aaaKey Kasa .NET 2.x API Sürüm Notları | Microsoft Docs"
description: ".NET geliştiricileri için Azure anahtar kasası bu API toocode kullanır"
services: key-vault
author: BrucePerlerMS
manager: mbaldwin
editor: bruceper
ms.assetid: 1cccf21b-5be9-4a49-8145-483b695124ba
ms.service: key-vault
ms.devlang: CSharp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/02/2017
ms.author: bruceper
ms.openlocfilehash: d95b84cf73c155f117f37e93893f27b02a75855c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-net-20---release-notes-and-migration-guide"></a><span data-ttu-id="9c222-103">Azure anahtar kasası .NET 2.0 - sürüm notları ve Geçiş Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="9c222-103">Azure Key Vault .NET 2.0 - Release Notes and Migration Guide</span></span>
<span data-ttu-id="9c222-104">Merhaba aşağıdaki notları ve rehberlik Azure anahtar kasası .NET ile birlikte çalışan geliştiricilere içindir / C# Kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="9c222-104">hello following notes and guidance are for developers working with Azure Key Vault .NET / C# library.</span></span> <span data-ttu-id="9c222-105">Geçiş Hello hello 1.0 sürümü toohello 2.0 sürümünden güncelleştirme sayısı, hello işlevsel iyileştirmeler toobenefit sırada kodunuzu geçiş işlerinde gerektirir ve ekler gibi özellik bu işlem yapıldı **anahtar kasası sertifikaları** destekler.</span><span class="sxs-lookup"><span data-stu-id="9c222-105">In hello transition from hello 1.0 version toohello 2.0 version, a number of updates have been made that will require migration work in your code in order for you toobenefit from hello functional improvements and feature additions such as **Key Vault certificates** support.</span></span>

## <a name="key-vault-certificates"></a><span data-ttu-id="9c222-106">Anahtar kasası sertifikaları</span><span class="sxs-lookup"><span data-stu-id="9c222-106">Key Vault certificates</span></span>

<span data-ttu-id="9c222-107">Anahtar kasası sertifikaları destek sağlar, x509 yönetimi için sertifikaları ve davranışları aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="9c222-107">Key Vault certificates support provides for management of your x509 certificates and hello following behaviors:</span></span>  

* <span data-ttu-id="9c222-108">Bir sertifika sahibinin toocreate bir anahtar kasası oluşturma işlemi veya varolan bir sertifikayı hello alma aracılığıyla bir sertifika sağlar.</span><span class="sxs-lookup"><span data-stu-id="9c222-108">Allows a certificate owner toocreate a certificate through a Key Vault creation process or through hello import of an existing certificate.</span></span> <span data-ttu-id="9c222-109">Bu otomatik olarak imzalanan hem de içerir ve sertifika yetkilisi sertifikaları oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="9c222-109">This includes both self-signed and Certificate Authority generated certificates.</span></span>
* <span data-ttu-id="9c222-110">Bir anahtar kasası sertifika sahibinin tooimplement güvenli depolama ve Yönetimi X509 verir sertifikaları özel anahtar malzemesi etkileşim olmadan.</span><span class="sxs-lookup"><span data-stu-id="9c222-110">Allows a Key Vault certificate owner tooimplement secure storage and management of X509 certificates without interaction with private key material.</span></span>  
* <span data-ttu-id="9c222-111">Bir sertifika sahibinin toocreate anahtar kasası toomanage hello yaşam döngüsü, bir sertifikanın yönlendiren bir ilke sağlar.</span><span class="sxs-lookup"><span data-stu-id="9c222-111">Allows a certificate owner toocreate a policy that directs Key Vault toomanage hello life-cycle of a certificate.</span></span>  
* <span data-ttu-id="9c222-112">Sertifika sahipleri tooprovide kişi hakkında bilgi için bildirim yaşam döngüsü olayları geçerlilik süresi ve sertifikanın yenilenmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="9c222-112">Allows certificate owners tooprovide contact information for notification about life-cycle events of expiration and renewal of certificate.</span></span>  
* <span data-ttu-id="9c222-113">Otomatik olarak yenilenmesi destekler seçili verenler - anahtar kasası iş ortağı X509 ile sertifika sağlayıcıları / sertifika yetkilileri.</span><span class="sxs-lookup"><span data-stu-id="9c222-113">Supports automatic renewal with selected issuers - Key Vault partner X509 certificate providers / certificate authorities.</span></span>
  
  * <span data-ttu-id="9c222-114">Not - ortaklık olmayan sağlayıcıları/yetkilileri de izin verilir ancak hello otomatik yenileme özelliği desteklemez.</span><span class="sxs-lookup"><span data-stu-id="9c222-114">NOTE - Non-partnered providers/authorities are also allowed but, will not support hello auto renewal feature.</span></span>

## <a name="net-support"></a><span data-ttu-id="9c222-115">.NET desteği</span><span class="sxs-lookup"><span data-stu-id="9c222-115">.NET support</span></span>

* <span data-ttu-id="9c222-116">**.NET 4.0** hello Azure anahtar kasası .NET hello 2.0 sürümü tarafından desteklenmeyen / C# Kitaplığı</span><span class="sxs-lookup"><span data-stu-id="9c222-116">**.NET 4.0** is not supported by hello 2.0 version of hello Azure Key Vault .NET/C# library</span></span>
* <span data-ttu-id="9c222-117">**.NET core** hello Azure anahtar kasası .NET hello 2.0 sürümü tarafından desteklenen / C# Kitaplığı</span><span class="sxs-lookup"><span data-stu-id="9c222-117">**.NET Core** is supported by hello 2.0 version of hello Azure Key Vault .NET/C# library</span></span>

## <a name="namespaces"></a><span data-ttu-id="9c222-118">ad alanları</span><span class="sxs-lookup"><span data-stu-id="9c222-118">Namespaces</span></span>

* <span data-ttu-id="9c222-119">ad alanı için hello **modelleri** değiştirilirse **Microsoft.Azure.KeyVault** çok**Microsoft.Azure.KeyVault.Models**.</span><span class="sxs-lookup"><span data-stu-id="9c222-119">hello namespace for **models** is changed from **Microsoft.Azure.KeyVault** too**Microsoft.Azure.KeyVault.Models**.</span></span>
* <span data-ttu-id="9c222-120">Merhaba **Microsoft.Azure.KeyVault.Internal** ad alanı bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="9c222-120">hello **Microsoft.Azure.KeyVault.Internal** namespace is dropped.</span></span>
* <span data-ttu-id="9c222-121">Hello Azure SDK'sı bağımlılıkları ad alanı değiştirildi **Hyak.Common** ve **Hyak.Common.Internals** çok**Microsoft.Rest** ve  **Microsoft.Rest.Serialization**</span><span class="sxs-lookup"><span data-stu-id="9c222-121">hello Azure SDK dependencies namespace are changed from **Hyak.Common** and **Hyak.Common.Internals** too**Microsoft.Rest** and **Microsoft.Rest.Serialization**</span></span>

## <a name="type-changes"></a><span data-ttu-id="9c222-122">Türü değişiklikleri</span><span class="sxs-lookup"><span data-stu-id="9c222-122">Type changes</span></span>

* <span data-ttu-id="9c222-123">*Gizli* çok değiştirilen*SecretBundle*</span><span class="sxs-lookup"><span data-stu-id="9c222-123">*Secret* changed too*SecretBundle*</span></span>
* <span data-ttu-id="9c222-124">*Sözlük* çok değiştirilen*IDictionary*</span><span class="sxs-lookup"><span data-stu-id="9c222-124">*Dictionary* changed too*IDictionary*</span></span>
* <span data-ttu-id="9c222-125">*Liste<T>, string []* çok değiştirilen*IList<T>*</span><span class="sxs-lookup"><span data-stu-id="9c222-125">*List<T>, string []* changed too*IList<T>*</span></span>
* <span data-ttu-id="9c222-126">*NextList* çok değiştirilen *NextPageLink*</span><span class="sxs-lookup"><span data-stu-id="9c222-126">*NextList* changed too *NextPageLink*</span></span>

## <a name="return-types"></a><span data-ttu-id="9c222-127">Dönüş türleri</span><span class="sxs-lookup"><span data-stu-id="9c222-127">Return types</span></span>

* <span data-ttu-id="9c222-128">**KeyList** ve **SecretList** döndürülecek *IPage<T>*  yerine *ListKeysResponseMessage*</span><span class="sxs-lookup"><span data-stu-id="9c222-128">**KeyList** and **SecretList** will return *IPage<T>* instead of *ListKeysResponseMessage*</span></span>
* <span data-ttu-id="9c222-129">oluşturulan hello **BackupKeyAsync** döndürülecek *BackupKeyResult* içeren *değeri* (Yedekleme blob).</span><span class="sxs-lookup"><span data-stu-id="9c222-129">hello generated **BackupKeyAsync** will return *BackupKeyResult* which contains *Value* (back-up blob).</span></span> <span data-ttu-id="9c222-130">Merhaba önce yöntemi Sarmalanan ve döndürmeyi yalnızca hello değeri idi.</span><span class="sxs-lookup"><span data-stu-id="9c222-130">Before hello method was wrapped and returning only hello value.</span></span>

## <a name="exceptions"></a><span data-ttu-id="9c222-131">Özel durumlar</span><span class="sxs-lookup"><span data-stu-id="9c222-131">Exceptions</span></span>

* <span data-ttu-id="9c222-132">*KeyVaultClientException* çok değiştirilir*KeyVaultErrorException*</span><span class="sxs-lookup"><span data-stu-id="9c222-132">*KeyVaultClientException* is changed too*KeyVaultErrorException*</span></span>
* <span data-ttu-id="9c222-133">Merhaba hizmet hatası değiştirildiğinde *özel durum. Hata* çok*özel durum. Body.Error.Message*.</span><span class="sxs-lookup"><span data-stu-id="9c222-133">hello service error is changed from *exception.Error* too*exception.Body.Error.Message*.</span></span>
* <span data-ttu-id="9c222-134">Ek bilgi için hata iletisini hello kaldırıldı **[JsonExtensionData]**.</span><span class="sxs-lookup"><span data-stu-id="9c222-134">Removed additional info from hello error message for **[JsonExtensionData]**.</span></span>

## <a name="constructors"></a><span data-ttu-id="9c222-135">Oluşturucular</span><span class="sxs-lookup"><span data-stu-id="9c222-135">Constructors</span></span>

* <span data-ttu-id="9c222-136">Kabul yerine bir *HttpClient* oluşturucu bağımsız değişkeni olarak yalnızca hello Oluşturucusu kabul *HttpClientHandler* veya *DelegatingHandler []*.</span><span class="sxs-lookup"><span data-stu-id="9c222-136">Instead of accepting an *HttpClient* as a constructor argument, hello constructor only accepts *HttpClientHandler* or *DelegatingHandler[]*.</span></span>

## <a name="downloaded-packages"></a><span data-ttu-id="9c222-137">İndirilen paketler</span><span class="sxs-lookup"><span data-stu-id="9c222-137">Downloaded packages</span></span>

<span data-ttu-id="9c222-138">Bir istemci üzerinde bir bağımlılık işlerken anahtar kasası hello aşağıdaki yüklenen</span><span class="sxs-lookup"><span data-stu-id="9c222-138">When a client is processing a  dependency on Key Vault hello following were downloaded</span></span>

### <a name="previous-package-list"></a><span data-ttu-id="9c222-139">Önceki paket listesi</span><span class="sxs-lookup"><span data-stu-id="9c222-139">Previous package list</span></span>

* <span data-ttu-id="9c222-140">id="Hyak.Common paketini" Sürüm "1.0.2" = targetFramework "net45" =</span><span class="sxs-lookup"><span data-stu-id="9c222-140">package id="Hyak.Common" version="1.0.2" targetFramework="net45"</span></span>
* <span data-ttu-id="9c222-141">id="Microsoft.Azure.Common paketini" Sürüm "2.0.4" = targetFramework "net45" =</span><span class="sxs-lookup"><span data-stu-id="9c222-141">package id="Microsoft.Azure.Common" version="2.0.4" targetFramework="net45"</span></span>
* <span data-ttu-id="9c222-142">id="Microsoft.Azure.common.Dependencies paketini" Sürüm "1.0.0" = targetFramework "net45" =</span><span class="sxs-lookup"><span data-stu-id="9c222-142">package id="Microsoft.Azure.Common.Dependencies" version="1.0.0" targetFramework="net45"</span></span>
* <span data-ttu-id="9c222-143">id="Microsoft.Azure.KeyVault paketini" Sürüm "1.0.0" = targetFramework "net45" =</span><span class="sxs-lookup"><span data-stu-id="9c222-143">package id="Microsoft.Azure.KeyVault" version="1.0.0" targetFramework="net45"</span></span>
* <span data-ttu-id="9c222-144">id="Microsoft.BCL paketini" Sürüm "1.1.9" = targetFramework "net45" =</span><span class="sxs-lookup"><span data-stu-id="9c222-144">package id="Microsoft.Bcl" version="1.1.9" targetFramework="net45"</span></span>
* <span data-ttu-id="9c222-145">id="Microsoft.BCL.Async paketini" Sürüm "1.0.168" = targetFramework "net45" =</span><span class="sxs-lookup"><span data-stu-id="9c222-145">package id="Microsoft.Bcl.Async" version="1.0.168" targetFramework="net45"</span></span>
* <span data-ttu-id="9c222-146">id="Microsoft.BCL.Build paketini" Sürüm "1.0.14" = targetFramework "net45" =</span><span class="sxs-lookup"><span data-stu-id="9c222-146">package id="Microsoft.Bcl.Build" version="1.0.14" targetFramework="net45"</span></span>
* <span data-ttu-id="9c222-147">id="Microsoft.NET.http paketini" Sürüm "2.2.22" = targetFramework "net45" =</span><span class="sxs-lookup"><span data-stu-id="9c222-147">package id="Microsoft.Net.Http" version="2.2.22" targetFramework="net45"</span></span>

### <a name="current-package-list"></a><span data-ttu-id="9c222-148">Geçerli paket listesi</span><span class="sxs-lookup"><span data-stu-id="9c222-148">Current package list</span></span>

* <span data-ttu-id="9c222-149">id="Microsoft.Azure.KeyVault paketini" Sürüm "2.0.0-preview" targetFramework = "net45" =</span><span class="sxs-lookup"><span data-stu-id="9c222-149">package id="Microsoft.Azure.KeyVault" version="2.0.0-preview" targetFramework="net45"</span></span>
* <span data-ttu-id="9c222-150">id="Microsoft.REST.ClientRuntime paketini" Sürüm "2.2.0" = targetFramework "net45" =</span><span class="sxs-lookup"><span data-stu-id="9c222-150">package id="Microsoft.Rest.ClientRuntime" version="2.2.0" targetFramework="net45"</span></span>
* <span data-ttu-id="9c222-151">id="Microsoft.REST.ClientRuntime.Azure paketini" Sürüm "3.2.0" = targetFramework "net45" =</span><span class="sxs-lookup"><span data-stu-id="9c222-151">package id="Microsoft.Rest.ClientRuntime.Azure" version="3.2.0" targetFramework="net45"</span></span>

## <a name="class-changes"></a><span data-ttu-id="9c222-152">Sınıf değişiklikleri</span><span class="sxs-lookup"><span data-stu-id="9c222-152">Class changes</span></span>

* <span data-ttu-id="9c222-153">**UnixEpoch** sınıfı kaldırıldı</span><span class="sxs-lookup"><span data-stu-id="9c222-153">**UnixEpoch** class has been removed</span></span>
* <span data-ttu-id="9c222-154">**Base64UrlConverter** sınıfı çok yeniden**Base64UrlJsonConverter**</span><span class="sxs-lookup"><span data-stu-id="9c222-154">**Base64UrlConverter** class is renamed too**Base64UrlJsonConverter**</span></span>

## <a name="other-changes"></a><span data-ttu-id="9c222-155">Diğer değişiklikler</span><span class="sxs-lookup"><span data-stu-id="9c222-155">Other changes</span></span>

* <span data-ttu-id="9c222-156">Merhaba API sürümü toothis KV işlemi geçici hataları yeniden deneme ilkesi hello yapılandırması için destek eklendi.</span><span class="sxs-lookup"><span data-stu-id="9c222-156">Support for hello configuration of KV operation retry policy on transient failures has been added toothis version of hello API.</span></span>

## <a name="microsoftazuremanagementkeyvault-nuget"></a><span data-ttu-id="9c222-157">Microsoft.Azure.Management.KeyVault NuGet</span><span class="sxs-lookup"><span data-stu-id="9c222-157">Microsoft.Azure.Management.KeyVault NuGet</span></span>

* <span data-ttu-id="9c222-158">Döndürülen hello işlemleri için bir *kasa*, hello dönüş türü olan bir kasa özelliği bulunan bir sınıf.</span><span class="sxs-lookup"><span data-stu-id="9c222-158">For hello operations that returned a *vault*, hello return type was a class that contained a Vault property.</span></span> <span data-ttu-id="9c222-159">Merhaba dönüş türü sunulmuştur *kasa*.</span><span class="sxs-lookup"><span data-stu-id="9c222-159">hello return type is now *Vault*.</span></span>
* <span data-ttu-id="9c222-160">*PermissionsToKeys* ve *PermissionsToSecrets* artık *Permissions.Keys* ve *Permissions.Secrets*</span><span class="sxs-lookup"><span data-stu-id="9c222-160">*PermissionsToKeys* and *PermissionsToSecrets* are now *Permissions.Keys* and *Permissions.Secrets*</span></span>
* <span data-ttu-id="9c222-161">Merhaba bazıları toohello kontrol-düzlemi de türleri değişiklikleri uygulamak döndür.</span><span class="sxs-lookup"><span data-stu-id="9c222-161">Some of hello return types changes apply toohello control-plane as well.</span></span>

## <a name="microsoftazurekeyvaultextensions-nuget"></a><span data-ttu-id="9c222-162">Microsoft.Azure.KeyVault.Extensions NuGet</span><span class="sxs-lookup"><span data-stu-id="9c222-162">Microsoft.Azure.KeyVault.Extensions NuGet</span></span>

* <span data-ttu-id="9c222-163">Merhaba paket parçalara çok**Microsoft.Azure.KeyVault.Extensions** ve **Microsoft.Azure.KeyVault.Cryptography** hello şifreleme işlemleri için.</span><span class="sxs-lookup"><span data-stu-id="9c222-163">hello package is broken up too**Microsoft.Azure.KeyVault.Extensions** and **Microsoft.Azure.KeyVault.Cryptography** for hello cryptography operations.</span></span>

