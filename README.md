# Asp Side-by-Side

Demonstrate a C# Asp.net project loading controllers and views from an F# Asp.Net project.

This will help migrate from C# controllers to F# controllers

Leaned heavily on on Asp.net documentation
- https://learn.microsoft.com/en-us/aspnet/core/mvc/advanced/app-parts?view=aspnetcore-9.0
- https://github.com/dotnet/AspNetCore.Docs/tree/main/aspnetcore/mvc/advanced/app-parts/3.0sample1



In short it comes down to 
- Making the views embedded resources
- Registering an embedded file provider for the F# assembly
- Registering an application part for the F# assembly

In Mvc.FSharp.fsproj
```xml
  <ItemGroup>
    <EmbeddedResource Include="Views/**/*.cshtml" />
  </ItemGroup>
```

In Mvc.CSharp > Program.cs

```cs
builder.Services
    .AddControllersWithViews()
    .AddApplicationPart(fsharpAssembly)
    .AddRazorRuntimeCompilation();


builder.Services.Configure<MvcRazorRuntimeCompilationOptions>(options =>
{ options.FileProviders.Add(new EmbeddedFileProvider(fsharpAssembly)); });
```
