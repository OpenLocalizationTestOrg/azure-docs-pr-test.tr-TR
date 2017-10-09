<span data-ttu-id="11b37-101">Azure Storage’daki her blob bir kapsayıcıda yer almalıdır.</span><span class="sxs-lookup"><span data-stu-id="11b37-101">Every blob in Azure storage must reside in a container.</span></span> <span data-ttu-id="11b37-102">Merhaba kapsayıcı forms bölümü hello blob adı.</span><span class="sxs-lookup"><span data-stu-id="11b37-102">hello container forms part of hello blob name.</span></span> <span data-ttu-id="11b37-103">Örneğin, `mycontainer` Bu örnek blob Urı'lerinde hello kapsayıcısında hello adıdır:</span><span class="sxs-lookup"><span data-stu-id="11b37-103">For example, `mycontainer` is hello name of hello container in these sample blob URIs:</span></span>

    https://storagesample.blob.core.windows.net/mycontainer/blob1.txt
    https://storagesample.blob.core.windows.net/mycontainer/photos/myphoto.jpg

<span data-ttu-id="11b37-104">Bir kapsayıcı adı geçerli bir DNS adı olan adlandırma kuralları aşağıdaki uyumlu toohello olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="11b37-104">A container name must be a valid DNS name, conforming toohello following naming rules:</span></span>

1. <span data-ttu-id="11b37-105">Kapsayıcı adları bir harf veya sayı ile başlamalı ve yalnızca harf, rakam ve tire (-) karakterinden hello içerebilir.</span><span class="sxs-lookup"><span data-stu-id="11b37-105">Container names must start with a letter or number, and can contain only letters, numbers, and hello dash (-) character.</span></span>
2. <span data-ttu-id="11b37-106">Her tire (-) karakterinin hemen önünde ve arkasında bir harf veya rakam bulunmalıdır; kapsayıcı adlarında art arda tirelere izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="11b37-106">Every dash (-) character must be immediately preceded and followed by a letter or number; consecutive dashes are not permitted in container names.</span></span>
3. <span data-ttu-id="11b37-107">Kapsayıcı adındaki tüm harfler küçük harf olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="11b37-107">All letters in a container name must be lowercase.</span></span>
4. <span data-ttu-id="11b37-108">Kapsayıcı adları 3-63 karakter arası uzunlukta olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="11b37-108">Container names must be from 3 through 63 characters long.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="11b37-109">Bu hello Not kapsayıcı adının her zaman küçük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="11b37-109">Note that hello name of a container must always be lowercase.</span></span> <span data-ttu-id="11b37-110">Kapsayıcı adına bir büyük harf eklemek ya da aksi takdirde hello kapsayıcı adlandırma kurallarını ihlal 400 hatası (Hatalı istek) alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="11b37-110">If you include an upper-case letter in a container name, or otherwise violate hello container naming rules, you may receive a 400 error (Bad Request).</span></span> 
> 
> 

