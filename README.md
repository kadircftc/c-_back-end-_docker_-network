Önemli!!
program.js e uygulama başlatıldığı anda migration işlemi yapılması için bu kodu eklemelisiniz! Kullandığınız Context ismi değişebilir.
```csharp
public static void Main(string[] args)
{
    var host = CreateHostBuilder(args).Build();
    using (var scope = host.Services.CreateScope())
    {
        var services = scope.ServiceProvider;
        try
        {
            var context = services.GetRequiredService<MsDbContext>();
            context.Database.Migrate();
            Console.WriteLine("Database migration completed.");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Migration error: {ex.Message}");
        }
    }
    CreateHostBuilder(args).Build().Run();
}

 
