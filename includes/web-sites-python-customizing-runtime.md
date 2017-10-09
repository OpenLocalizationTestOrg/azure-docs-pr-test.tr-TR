<span data-ttu-id="e7d44-101">Azure sanal ortam için Python toouse hello sürümü öncelik aşağıdaki hello ile belirler:</span><span class="sxs-lookup"><span data-stu-id="e7d44-101">Azure will determine hello version of Python toouse for its virtual environment with hello following priority:</span></span>

1. <span data-ttu-id="e7d44-102">Merhaba kök klasöründe Runtime.txt belirtilen sürüm</span><span class="sxs-lookup"><span data-stu-id="e7d44-102">version specified in runtime.txt in hello root folder</span></span>
2. <span data-ttu-id="e7d44-103">Merhaba web uygulaması yapılandırmasında Python tarafından belirtilen sürüm (Merhaba **ayarları** > **uygulama ayarları** web uygulamanızda hello Azure Portal dikey penceresinde)</span><span class="sxs-lookup"><span data-stu-id="e7d44-103">version specified by Python setting in hello web app configuration (hello **Settings** > **Application Settings** blade for your web app in hello Azure Portal)</span></span>
3. <span data-ttu-id="e7d44-104">Yukarıdaki hello hiçbiri belirtilmemişse python 2.7 hello varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="e7d44-104">python-2.7 is hello default if none of hello above are specified</span></span>

<span data-ttu-id="e7d44-105">Merhaba içeriğine için geçerli değerler</span><span class="sxs-lookup"><span data-stu-id="e7d44-105">Valid values for hello contents of</span></span> 

    \runtime.txt

<span data-ttu-id="e7d44-106">içeriği için geçerli değerler:</span><span class="sxs-lookup"><span data-stu-id="e7d44-106">are:</span></span>

* <span data-ttu-id="e7d44-107">python-2.7</span><span class="sxs-lookup"><span data-stu-id="e7d44-107">python-2.7</span></span>
* <span data-ttu-id="e7d44-108">python-3.4</span><span class="sxs-lookup"><span data-stu-id="e7d44-108">python-3.4</span></span>

<span data-ttu-id="e7d44-109">Varsa hello mikro sürüm (üçüncü basamak) belirtilmişse göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="e7d44-109">If hello micro version (third digit) is specified, it is ignored.</span></span>

