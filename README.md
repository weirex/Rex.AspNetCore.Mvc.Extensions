# Rex.AspNetCore.Mvc.Extensions


## 目录
* [更新日志](CHANGELOG.md "更新日志")（2020.5.1）

### 1.跨域
*AppSettings.json*
```JSON
{
  "AppSettings": {
    "origins": "*",
    "headers": "*",
    "methods": "*",
    }
}
```


*[C#]*
```csharp
public void ConfigureServices(IServiceCollection services) {
    services.AddExtCors("AllowCors");
}
public void Configure(IApplicationBuilder app, IWebHostEnvironment env) {
    app.UseCors("AllowCors");
}
```


### 2.使用NewtonsoftJson返回响应结果
*[C#]*
```csharp
public void ConfigureServices(IServiceCollection services) {
    services.AddControllers().AddExtNewtonsoftJson();
}
```


### 3.全局异常捕获
*[C#]*
```csharp
public void ConfigureServices(IServiceCollection services) {
    services.AddMvc(options => {
        options.Filters.Add<ApiExceptionFilter>();
    });
}
```


### 4.统一返回结果
*[C#]*
```csharp
public void ConfigureServices(IServiceCollection services) {
    services.AddMvc(options => {
        options.Filters.Add<ApiResultFilter>();
    });
}
```


### 5.实体参数验证
*[C#]*
```csharp
public void ConfigureServices(IServiceCollection services) {
    services.AddExtValidationModel();
}
```


### 完整代码
*[C#]*
```csharp
public void ConfigureServices(IServiceCollection services) {
    //跨域
    services.AddExtCors("AllowCors");
    //使用NewtonsoftJson返回响应结果
    services.AddControllers().AddExtNewtonsoftJson();
    services.AddMvc(options => {
        //全局异常捕获
        options.Filters.Add<ApiExceptionFilter>();
        //统一返回结果
        options.Filters.Add<ApiResultFilter>();
    });
    //实体参数验证
    services.AddExtValidationModel();
}
public void Configure(IApplicationBuilder app, IWebHostEnvironment env) {
    app.UseCors("AllowCors");
    app.UseRouting();
    app.UseAuthorization();
    app.UseEndpoints(endpoints => {
        endpoints.MapControllers();
    });
}
```
