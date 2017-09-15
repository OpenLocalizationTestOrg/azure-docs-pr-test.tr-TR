
<!--
includes/sql-data-warehouse-include-pause-description.md

Latest Freshness check:  2016-04-22 , barbkess.

As of circa 2016-04-22, the following topics might include this include:
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks.md
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks-powershell.md
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks-rest-api.md

-->
<span data-ttu-id="f81f1-101">Maliyet tasarrufu sağlamak duraklatma ve sürdürme işlem kaynakları isteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="f81f1-101">To save costs, you can pause and resume compute resources on-demand.</span></span> <span data-ttu-id="f81f1-102">Örneğin, veritabanı gece sırasında ve hafta sonları kullandığınız olmaz, bu saatlerde duraklatma ve gün boyunca sürdürün.</span><span class="sxs-lookup"><span data-stu-id="f81f1-102">For example, if you won't be using the database during the night and on weekends, you can pause it during those times, and resume it during the day.</span></span> <span data-ttu-id="f81f1-103">Veritabanı duraklatıldığında Dwu için sizden ücret olmaz.</span><span class="sxs-lookup"><span data-stu-id="f81f1-103">You won't be charged for DWUs while the database is paused.</span></span>

<span data-ttu-id="f81f1-104">Ne zaman bir veritabanı duraklatılamadı:</span><span class="sxs-lookup"><span data-stu-id="f81f1-104">When you pause a database:</span></span>

* <span data-ttu-id="f81f1-105">İşlem ve bellek kaynakları veri merkezindeki kullanılabilir kaynak havuzu döndürülürsünüz</span><span class="sxs-lookup"><span data-stu-id="f81f1-105">Compute and memory resources are returned to the pool of available resources in the data center</span></span>
* <span data-ttu-id="f81f1-106">DWU maliyetleri duraklatma süresi için sıfırdır.</span><span class="sxs-lookup"><span data-stu-id="f81f1-106">DWU costs are zero for the duration of the pause.</span></span>
* <span data-ttu-id="f81f1-107">Veri depolama etkilenmez ve verileriniz olduğu gibi kalır.</span><span class="sxs-lookup"><span data-stu-id="f81f1-107">Data storage is not affected and your data stays intact.</span></span> 
* <span data-ttu-id="f81f1-108">SQL veri ambarı çalışan ya da sıraya alınan tüm işlemleri iptal eder.</span><span class="sxs-lookup"><span data-stu-id="f81f1-108">SQL Data Warehouse cancels all running or queued operations.</span></span>

