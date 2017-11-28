### <a name="create-a-console-application"></a><span data-ttu-id="ca4c6-101">Konsol uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="ca4c6-101">Create a console application</span></span>

<span data-ttu-id="ca4c6-102">İlk olarak Visual Studio'yu başlatın ve yeni bir **Konsol Uygulaması (.NET Framework)** projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ca4c6-102">First, launch Visual Studio and create a new **Console App (.NET Framework)** project.</span></span>

### <a name="add-the-relay-nuget-package"></a><span data-ttu-id="ca4c6-103">Geçiş NuGet paketini ekleme</span><span class="sxs-lookup"><span data-stu-id="ca4c6-103">Add the Relay NuGet package</span></span>

1. <span data-ttu-id="ca4c6-104">Yeni oluşturulan projeye sağ tıklayın ve **NuGet Paketlerini Yönet**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ca4c6-104">Right-click the newly created project and then click **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="ca4c6-105">**Gözat** sekmesine tıklayın, ardından "Microsoft.Azure.Relay" ifadesini aratın ve **Microsoft Azure Geçiş** öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="ca4c6-105">Click the **Browse** tab, then search for "Microsoft.Azure.Relay" and select the **Microsoft Azure Relay** item.</span></span> <span data-ttu-id="ca4c6-106">Yüklemeyi tamamlamak için **Yükle**'ye tıklayın, ardından bu iletişim kutusunu kapatın.</span><span class="sxs-lookup"><span data-stu-id="ca4c6-106">Click **Install** to complete the installation, then close this dialog box.</span></span>

### <a name="write-some-code-to-send-messages"></a><span data-ttu-id="ca4c6-107">İleti göndermek için bazı kodlar yazma</span><span class="sxs-lookup"><span data-stu-id="ca4c6-107">Write some code to send messages</span></span>

1. <span data-ttu-id="ca4c6-108">Program.cs dosyasının üst tarafındaki `using` deyimlerini aşağıdaki `using` deyimleriyle değiştirin:</span><span class="sxs-lookup"><span data-stu-id="ca4c6-108">Replace the existing `using` statements at the top of the Program.cs file with the following `using` statements:</span></span>
   
    ```csharp
    using System;
    using System.IO;
    using System.Threading;
    using System.Threading.Tasks;
    using Microsoft.Azure.Relay;
    ```
2. <span data-ttu-id="ca4c6-109">Karma bağlantı ayrıntıları için sabitleri `Program` sınıfına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ca4c6-109">Add constants to the `Program` class for the hybrid connection details.</span></span> <span data-ttu-id="ca4c6-110">Köşeli ayraçlar içindeki yer tutucuları karma bağlantı oluşturulurken aldığınız uygun değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="ca4c6-110">Replace the placeholders in brackets with the values you obtained when creating the hybrid connection.</span></span> <span data-ttu-id="ca4c6-111">Tam ad alanı adını kullandığınızdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="ca4c6-111">Be sure to use the fully qualified namespace name:</span></span>
   
    ```csharp
    private const string RelayNamespace = "{RelayNamespace}.servicebus.windows.net";
    private const string ConnectionName = "{HybridConnectionName}";
    private const string KeyName = "{SASKeyName}";
    private const string Key = "{SASKey}";
    ```
3. <span data-ttu-id="ca4c6-112">`Program` sınıfına aşağıdaki yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ca4c6-112">Add the following method to the `Program` class:</span></span>
   
    ```csharp
    private static async Task RunAsync()
    {
        Console.WriteLine("Enter lines of text to send to the server with ENTER");
   
        // Create a new hybrid connection client
        var tokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(KeyName, Key);
        var client = new HybridConnectionClient(new Uri(String.Format("sb://{0}/{1}", RelayNamespace, ConnectionName)), tokenProvider);
   
        // Initiate the connection
        var relayConnection = await client.CreateConnectionAsync();
   
        // We run two concurrent loops on the connection. One 
        // reads input from the console and writes it to the connection 
        // with a stream writer. The other reads lines of input from the 
        // connection with a stream reader and writes them to the console. 
        // Entering a blank line will shut down the write task after 
        // sending it to the server. The server will then cleanly shut down
        // the connection which will terminate the read task.
   
        var reads = Task.Run(async () => {
            // Initialize the stream reader over the connection
            var reader = new StreamReader(relayConnection);
            var writer = Console.Out;
            do
            {
                // Read a full line of UTF-8 text up to newline
                string line = await reader.ReadLineAsync();
                // if the string is empty or null, we are done.
                if (String.IsNullOrEmpty(line))
                    break;
                // Write to the console
                await writer.WriteLineAsync(line);
            }
            while (true);
        });
   
        // Read from the console and write to the hybrid connection
        var writes = Task.Run(async () => {
            var reader = Console.In;
            var writer = new StreamWriter(relayConnection) { AutoFlush = true };
            do
            {
                // Read a line form the console
                string line = await reader.ReadLineAsync();
                // Write the line out, also when it's empty
                await writer.WriteLineAsync(line);
                // Quit when the line was empty
                if (String.IsNullOrEmpty(line))
                    break;
            }
            while (true);
        });
   
        // Wait for both tasks to complete
        await Task.WhenAll(reads, writes);
        await relayConnection.CloseAsync(CancellationToken.None);
    }
    ```
4. <span data-ttu-id="ca4c6-113">Aşağıdaki kod satırını `Program` sınıfındaki `Main` yöntemine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ca4c6-113">Add the following line of code to the `Main` method in the `Program` class.</span></span>
   
    ```csharp
    RunAsync().GetAwaiter().GetResult();
    ```
   
    <span data-ttu-id="ca4c6-114">Program.cs dosyanız aşağıdaki gibi görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="ca4c6-114">Here is what your Program.cs should look like.</span></span>
   
    ```csharp
    using System;
    using System.IO;
    using System.Threading;
    using System.Threading.Tasks;
    using Microsoft.Azure.Relay;
   
    namespace Client
    {
        class Program
        {
            private const string RelayNamespace = "{RelayNamespace}.servicebus.windows.net";
            private const string ConnectionName = "{HybridConnectionName}";
            private const string KeyName = "{SASKeyName}";
            private const string Key = "{SASKey}";
   
            static void Main(string[] args)
            {
                RunAsync().GetAwaiter().GetResult();
            }
   
            private static async Task RunAsync()
            {
                Console.WriteLine("Enter lines of text to send to the server with ENTER");
   
                // Create a new hybrid connection client
                var tokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(KeyName, Key);
                var client = new HybridConnectionClient(new Uri(String.Format("sb://{0}/{1}", RelayNamespace, ConnectionName)), tokenProvider);
   
                // Initiate the connection
                var relayConnection = await client.CreateConnectionAsync();
   
                // We run two conucrrent loops on the connection. One 
                // reads input from the console and writes it to the connection 
                // with a stream writer. The other reads lines of input from the 
                // connection with a stream reader and writes them to the console. 
                // Entering a blank line will shut down the write task after 
                // sending it to the server. The server will then cleanly shut down
                // the connection which will terminate the read task.
   
                var reads = Task.Run(async () => {
                    // Initialize the stream reader over the connection
                    var reader = new StreamReader(relayConnection);
                    var writer = Console.Out;
                    do
                    {
                        // Read a full line of UTF-8 text up to newline
                        string line = await reader.ReadLineAsync();
                        // If the string is empty or null, we are done.
                        if (String.IsNullOrEmpty(line))
                            break;
                        // Write to the console
                        await writer.WriteLineAsync(line);
                    }
                    while (true);
                });
   
                // Read from the console and write to the hybrid connection
                var writes = Task.Run(async () => {
                    var reader = Console.In;
                    var writer = new StreamWriter(relayConnection) { AutoFlush = true };
                    do
                    {
                        // Read a line form the console
                        string line = await reader.ReadLineAsync();
                        // Write the line out, also when it's empty
                        await writer.WriteLineAsync(line);
                        // Quit when the line was empty
                        if (String.IsNullOrEmpty(line))
                            break;
                    }
                    while (true);
                });
   
                // Wait for both tasks to complete
                await Task.WhenAll(reads, writes);
                await relayConnection.CloseAsync(CancellationToken.None);
            }
        }
    }
    ```

