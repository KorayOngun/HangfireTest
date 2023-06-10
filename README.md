# Hangfire

### Hangfire, arkada asenkron olarak çalışan, yani kullanıcıyı bekletmeyen (Background job) olarak tanımladığımız işler için kullanılan bir tooldur. Mutlaka bir depolama alanına, yani DB’ye ihtiyaç duyar. Depolama alanı olarak, birçok veritabanını destekler (SQL Server, MSMQ, Redis) gibi. Genellikle Time Schedule şeklinde tekrarlayan belli zaman aralıkları ile çalışan işlerde kullanılsalar da, birçok farklı kullanım şekilleri vardır.


#### "hello world from hangfire" & MVC

` Install-Package Hangfire.Core`

` Install-Package Hangfire.SqlServer`

` Install-Package Hangfire.AspNet`

` Install-Package Microsoft.Data.SqlClient`

## program.cs

builder.Services.AddHangfire(x =>

{

    x.UseSqlServerStorage("<db_path>"); // hangfire belirtilen db_path'de gerekli tabloları oluşturur
    
    RecurringJob.AddOrUpdate<Job>(j => j.HangfireControl(), "* * * * *"); //<job> => job.cs

  });

  builder.Services.AddHangfireServer();

app.UseHangfireDashboard();

## Job.cs

{

    public class Job
    
    {
    
        public void HangfireControl()
        {
        
            Console.WriteLine("hello world from hangfire");     
        }

    }
    
}

#### hangfire zamanı
 
https://crontab.cronhub.io/
 
`* * * * *	Every minute`

`0 * * * *	Every hour`

`0 0 * * *	Every day at 12:00 AM`

`0 0 * * FRI	At 12:00 AM, only on Friday`

`0 0 1 * *	At 12:00 AM, on day 1 of the month`


https://www.hangfire.io/

https://medium.com/devopsturkiye/asp-net-core-hangfire-ile-arka-plan-i%CC%87%C5%9Flemleri-986790c37cf3


