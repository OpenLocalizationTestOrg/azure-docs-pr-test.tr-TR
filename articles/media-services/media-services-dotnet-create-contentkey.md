---
title: .NET ile ContentKeys aaaCreate
description: "TooAssets nasıl erişim güvenli sağlayan toocreate içerik anahtarları hakkında bilgi edinin."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 225b05e5-7d30-409c-b5b7-3ef0634310c7
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 35909c64e8393e228be75c464a034ffc40122952
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-contentkeys-with-net"></a><span data-ttu-id="7ef6e-103">.NET ile ContentKeys oluşturma</span><span class="sxs-lookup"><span data-stu-id="7ef6e-103">Create ContentKeys with .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7ef6e-104">REST</span><span class="sxs-lookup"><span data-stu-id="7ef6e-104">REST</span></span>](media-services-rest-create-contentkey.md)
> * [<span data-ttu-id="7ef6e-105">.NET</span><span class="sxs-lookup"><span data-stu-id="7ef6e-105">.NET</span></span>](media-services-dotnet-create-contentkey.md)
> 
> 

<span data-ttu-id="7ef6e-106">Media Services toocreate sağlar ve şifrelenmiş varlıklar gönderin.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-106">Media Services enables you toocreate and deliver encrypted assets.</span></span> <span data-ttu-id="7ef6e-107">A **ContentKey** güvenli erişim tooyour sağlar **varlık**s.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-107">A **ContentKey** provides secure access tooyour **Asset**s.</span></span> 

<span data-ttu-id="7ef6e-108">Yeni bir varlık oluşturduğunuzda (örneğin, önce [dosyaları karşıya yükleme](media-services-dotnet-upload-files.md)), şifreleme seçenekleri aşağıdaki hello belirtebilirsiniz: **StorageEncrypted**, **CommonEncryptionProtected**, veya **EnvelopeEncryptionProtected**.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-108">When you create a new asset (for example, before you [upload files](media-services-dotnet-upload-files.md)), you can specify hello following encryption options: **StorageEncrypted**, **CommonEncryptionProtected**, or **EnvelopeEncryptionProtected**.</span></span> 

<span data-ttu-id="7ef6e-109">Tooyour istemcileri varlıklar iletirken yapabilecekleriniz [dinamik olarak şifrelenmiş varlıklar toobe için yapılandırma](media-services-dotnet-configure-asset-delivery-policy.md) iki şifrelemeleri aşağıdaki hello biriyle: **DynamicEnvelopeEncryption** veya  **DynamicCommonEncryption**.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-109">When you deliver assets tooyour clients, you can [configure for assets toobe dynamically encrypted](media-services-dotnet-configure-asset-delivery-policy.md) with one of hello following two encryptions: **DynamicEnvelopeEncryption** or **DynamicCommonEncryption**.</span></span>

<span data-ttu-id="7ef6e-110">Şifrelenmiş varlıklar sahip ilişkili toobe **ContentKey**s.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-110">Encrypted assets have toobe associated with **ContentKey**s.</span></span> <span data-ttu-id="7ef6e-111">Bu makalede nasıl toocreate bir içerik anahtarı.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-111">This article describes how toocreate a content key.</span></span>

> [!NOTE]
> <span data-ttu-id="7ef6e-112">Yeni bir oluştururken **StorageEncrypted** varlık kullanarak hello Media Services .NET SDK hello **ContentKey** otomatik olarak oluşturulan ve hello varlık ile bağlanır.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-112">When creating a new **StorageEncrypted** asset using hello Media Services .NET SDK , hello **ContentKey** is automatically created and linked with hello asset.</span></span>
> 
> 

## <a name="contentkeytype"></a><span data-ttu-id="7ef6e-113">ContentKeyType</span><span class="sxs-lookup"><span data-stu-id="7ef6e-113">ContentKeyType</span></span>
<span data-ttu-id="7ef6e-114">Ne zaman ayarlamalısınız hello değerlerden biri oluşturma içerik anahtarıdır hello içerik anahtar türü.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-114">One of hello values that you must set when create a content key is hello content key type.</span></span> <span data-ttu-id="7ef6e-115">Değerleri aşağıdaki hello birini seçin.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-115">Choose from one of hello following values.</span></span> 

    public enum ContentKeyType
    {
        /// <summary>
        /// Specifies a content key for common encryption.
        /// </summary>
        /// <remarks>This is hello default value.</remarks>
        CommonEncryption = 0,

        /// <summary>
        /// Specifies a content key for storage encryption.
        /// </summary>
        StorageEncryption = 1,

        /// <summary>
        /// Specifies a content key for configuration encryption.
        /// </summary>
        ConfigurationEncryption = 2,

        /// <summary>
        /// Specifies a content key for Envelope encryption.  Only used internally.
        /// </summary>
        EnvelopeEncryption = 4
    }

## <span data-ttu-id="7ef6e-116"><a id="envelope_contentkey"></a>Zarf türü ContentKey oluşturma</span><span class="sxs-lookup"><span data-stu-id="7ef6e-116"><a id="envelope_contentkey"></a>Create envelope type ContentKey</span></span>
<span data-ttu-id="7ef6e-117">Merhaba aşağıdaki kod parçacığını bir içerik anahtarı hello Zarf şifreleme türü oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-117">hello following code snippet creates a content key of hello envelope encryption type.</span></span> <span data-ttu-id="7ef6e-118">Ardından hello anahtar hello belirtilen varlık ile ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-118">It then associates hello key with hello specified asset.</span></span>

    static public IContentKey CreateEnvelopeTypeContentKey(IAsset asset)
    {
        // Create envelope encryption content key
        Guid keyId = Guid.NewGuid();
        byte[] contentKey = GetRandomBuffer(16);

        IContentKey key = _context.ContentKeys.Create(
                                keyId,
                                contentKey,
                                "ContentKey",
                                ContentKeyType.EnvelopeEncryption);

        asset.ContentKeys.Add(key);

        return key;
    }

    static private byte[] GetRandomBuffer(int size)
    {
        byte[] randomBytes = new byte[size];
        using (RNGCryptoServiceProvider rng = new RNGCryptoServiceProvider())
        {
            rng.GetBytes(randomBytes);
        }

        return randomBytes;
    }

<span data-ttu-id="7ef6e-119">Arama</span><span class="sxs-lookup"><span data-stu-id="7ef6e-119">call</span></span>

    IContentKey key = CreateEnvelopeTypeContentKey(encryptedsset);



## <span data-ttu-id="7ef6e-120"><a id="common_contentkey"></a>Ortak tür ContentKey oluşturma</span><span class="sxs-lookup"><span data-stu-id="7ef6e-120"><a id="common_contentkey"></a>Create common type ContentKey</span></span>
<span data-ttu-id="7ef6e-121">Merhaba aşağıdaki kod parçacığını bir içerik anahtarı hello ortak şifreleme türü oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-121">hello following code snippet creates a content key of hello common encryption type.</span></span> <span data-ttu-id="7ef6e-122">Ardından hello anahtar hello belirtilen varlık ile ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="7ef6e-122">It then associates hello key with hello specified asset.</span></span>

    static public IContentKey CreateCommonTypeContentKey(IAsset asset)
    {
        // Create common encryption content key
        Guid keyId = Guid.NewGuid();
        byte[] contentKey = GetRandomBuffer(16);

        IContentKey key = _context.ContentKeys.Create(
                                keyId,
                                contentKey,
                                "ContentKey",
                                ContentKeyType.CommonEncryption);

        // Associate hello key with hello asset.
        asset.ContentKeys.Add(key);

        return key;
    }

    static private byte[] GetRandomBuffer(int length)
    {
        var returnValue = new byte[length];

        using (var rng =
            new System.Security.Cryptography.RNGCryptoServiceProvider())
        {
            rng.GetBytes(returnValue);
        }

        return returnValue;
    }
<span data-ttu-id="7ef6e-123">Arama</span><span class="sxs-lookup"><span data-stu-id="7ef6e-123">call</span></span>

    IContentKey key = CreateCommonTypeContentKey(encryptedsset); 


## <a name="media-services-learning-paths"></a><span data-ttu-id="7ef6e-124">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="7ef6e-124">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="7ef6e-125">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="7ef6e-125">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

