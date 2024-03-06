# AuthenticationIn.Net8

 Authentication implementation steps

  Visual Studio 2022 - SQL SERVER
 1- Create new project: ASP.NET Core Web API
 2- Add DataContext class and inherite from IdentityDbContext
 3- Add AddDbContext to Program.cs class to use SqlServer using the corresponding connection string
 4- Add connection string to appsetting.json file
 5- Add migrations via this command: dotnet ef migrations add Initial. (if ef is not installed use this command: dotnet tool install --global dotnet-ef)
 6- Update database via this command: dotnet ef database update
 7- Add following lines after AddDbContext (inside Program.cs): 
    builder.Services.AddAuthorization();
    builder.Services.AddIdentityApiEndpoints<IdentityUser>()
      .AddEntityFrameworkStores<DataContext>();

    app.MapIdentityApi<IdentityUser>();

 8- In Program.cs class builder.Services.AddSwaggerGen() change to:
    builder.Services.AddSwaggerGen(options =>
    {
      options.AddSecurityDefinition("oauth2", new OpenApiSecurityScheme
      {
        In = ParameterLocation.Header,
        Name = "Authorization",
        Type = SecuritySchemeType.ApiKey,
    });
    options.OperationFilter<SecurityRequirementsOperationFilter>();
});

9- Add 'Authorize' attribute in controllers for example (WeatherForecastController)
10- Build and Use :-) 
