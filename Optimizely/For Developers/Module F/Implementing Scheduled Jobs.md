#Devs  #ModuleF 

Scheduled jobs are often used to run arbitrary code within the system.
You can implement a scheduled job with this minimal example:
```c#
using EPiServer.PlugIn;
[ScheduledPlugIn(DisplayName = "Minimal Scheduled Job")]
public class MinimalScheduledJob {
	public static string Execute() { return "Done!"; }
}
```

There is also a recommended implementation, which includes features like stopping jobs, etc.
```c#
[ScheduledPlugIn(DisplayName = "Recommended Scheduled Job", GUID = "1234...", SortIndex = 100)]
public class RecommendedScheduledJob : ScheduledJobBase
```

### Testing jobs
Scheduled jobs run within the context of the logged in user. So you can't test jobs by running them manually through the admin interface, since the job would then be granted admin rights. You would have to test the job by setting a time, ***and by running it manually***.
