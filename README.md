# Blazor

### `Nuget Package`
- [MudBlazor](#mudblazor)
- [BlazoredModal](#blazoredmodal-)

### `Docs`
- [Route](#route-)
- [Parameter](#parameter-)
- [Validation](#validation-)
- [Javascript](#javascript-)
- [NPM](#npm-)
- [Components](#components-)
- [Navigate](#navigate-)
- [Syntax](#syntax-)
- [HttpContext](#httpcontext-)
- [File Upload](#file-upload-)
- [File Download](#file-download-)

### `Error`
- [Blazor Server Disconnected](#blazor-server-disconnected-)

<br>

## MudBlazor

> MudBlazor는 Blazor를 위한 Material Design 컴포넌트 프레임워크입니다.

- [MudBlazor Official Site](https://mudblazor.com/)  
- [MudBlazor GitHub](https://github.com/MudBlazor/MudBlazor)

## Getting Started

#### 1. 패키지 설치
Nuget Package Manager에서 `MudBlazor` 패키지를 찾아 설치하거나, 아래 명령을 입력해 설치합니다.
```
dotnet add package MudBlazor
```

#### 2. Imports 추가
**`_Imports.razor`** 파일 안에 MudBlazor를 추가합니다.
```cshtml
@using MudBlazor
```

#### 3. Style 추가
**`index.html`** 혹은 **`_Layout.cshtml`** / **`_Host.cshtml`** 파일의 head 태그 안에 아래 내용을 추가합니다.
```html
<link href="https://fonts.googleapis.com/css?family=Roboto:300,400,500,700&display=swap" rel="stylesheet" />
<link href="_content/MudBlazor/MudBlazor.min.css" rel="stylesheet" />
```

예시: **`_Layout.cshtml`**
```html
<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    ...
    
    @*MudBlazor Style Reference*@
    <link href="https://fonts.googleapis.com/css?family=Roboto:300,400,500,700&display=swap" rel="stylesheet" />
    <link href="_content/MudBlazor/MudBlazor.min.css" rel="stylesheet" />
</head>
```

#### 4. script 추가
앞서 Style을 추가한 파일과 동일한 파일에 MudBlazor js file을 추가합니다. Blazor의 기본 스크립트 위치와 동일해야 합니다.
```html
<script src="_content/MudBlazor/MudBlazor.min.js"></script>
```

예시: **`_Layout.cshtml`**
```html
<body>
    ...
    <script src="_framework/blazor.server.js"></script>
    
    @*MudBlazor Script Reference*@
    <script src="/_content/MudBlazor/MudBlazor.min.js"></script>
</head> 
```

#### 5. 서비스 등록
**`Program.cs`** 파일에 아래 내용을 추가합니다. _(.NET 6 기준)_
```csharp
using MudBlazor.Services;

builder.Services.AddMudServices();
```

#### 6. 컴포넌트 추가
**`MainLayout.razor`** 파일 안에 아래 컴포넌트들을 추가합니다. `ThemeProvider`는 MudBlazor 사용을 위해 필수로 있어야 하지만, 나머지는 선택적으로 사용할 수 있습니다.
```razor
<MudThemeProvider/>
<MudDialogProvider/>
<MudSnackbarProvider/>
```
<br/>

## BlazoredModal [🔝](#blazor)

![image](https://user-images.githubusercontent.com/74305823/162673011-bbc021e7-914d-48c2-ac87-c373df727981.png)

- [BlazoredModal GitHub](https://github.com/Blazored/Modal)

## Getting Started
> Blazor Server 앱 기준

#### 1. 패키지 설치
Nuget Package Manager에서 `Blazored.Modal` 패키지를 찾아 설치하거나, 아래 명령을 입력해 설치합니다.
```
dotnet add package Blazored.Modal
```

#### 2. Imports 추가
**`_Imports.razor`** 파일 안에 Blazored.Modal을 추가합니다.
```cshtml
@using Blazored  
@using Blazored.Modal  
@using Blazored.Modal.Services 
```

#### 3. Style 추가
**`_Layout.cshtml`** 또는 **`_Host.cshtml`** 파일의 head 태그 안에 아래 내용을 추가합니다.
```html
<link href="_content/Blazored.Modal/blazored-modal.css" rel="stylesheet" />
```

예시: **`_Layout.cshtml`**
```html
<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <base href="~/" />
    ...
    
    @*BlazoredModal Style Reference*@
    <link href="_content/Blazored.Modal/blazored-modal.css" rel="stylesheet" />
</head>
```

#### 4. script 추가
앞서 Style을 추가한 파일과 동일한 파일에 Blazored Modal js file을 추가합니다. Blazor의 기본 스크립트 위치와 동일해야 합니다.
```html
<script src="_content/Blazored.Modal/blazored.modal.js"></script>
```

예시: **`_Layout.cshtml`**
```html
<body>
    ...
    <script src="_framework/blazor.server.js"></script>
    
    @*BlazoredModal Script Reference*@
    <script src="_content/Blazored.Modal/blazored.modal.js"></script>
</head> 
```

#### 5. 서비스 등록
**`Program.cs`** 파일에 아래 내용을 추가합니다. _(.NET 6 기준)_
```csharp
using Blazored.Modal;

builder.Services.AddBlazoredModal();
```

#### 6. CascadingBlazoredModal 컴포넌트 추가
**`App.razor`** 파일에 `<CascadingBlazoredModal />` 컴포넌트를 추가합니다.

```cshtml
<CascadingBlazoredModal>
    <Router AppAssembly="@typeof(App).Assembly">
        <Found Context="routeData">
            <AuthorizeRouteView RouteData="@routeData" DefaultLayout="@typeof(MainLayout)" />
            <FocusOnNavigate RouteData="@routeData" Selector="h1" />
        </Found>
        <NotFound>
            <PageTitle>Not found</PageTitle>
            <LayoutView Layout="@typeof(MainLayout)">
                <p role="alert">Sorry, there's nothing at this address.</p>
            </LayoutView>
        </NotFound>
    </Router>
</CascadingBlazoredModal>
```

<br/>

## Demo

### Modal
```cshtml
@page "/delete"

<style>
    .blazored-modal{
        width: 300px;
        max-height: 185px;
    }
    .blazored-modal-title{
        font-size: 20px;
        font-weight: bold;
        margin: 6px 0px 0px -5px;
    }
    .blazored-modal-header{
        padding: 0px 0 0.5rem 0;
    }
</style>

<div style="margin: 10px 0px;">
    <MudText Typo="Typo.subtitle1" Style="font-weight: 600;">삭제하시겠습니까?</MudText>
    <div style="display: inline-flex; margin-top: 20px;">
        <MudButton Variant="Variant.Filled" Color="Color.Error" Class="btn-default" OnClick="Delete">삭제</MudButton>
        <MudButton Variant="Variant.Text" Color="Color.Error" Class="btn-default btn-cancel" OnClick="Cancel">취소</MudButton>
    </div>
</div>

@code {
    [CascadingParameter] BlazoredModalInstance ModalInstance { get; set; }

    private void Delete()
    {
        ModalInstance.CloseAsync(ModalResult.Ok("delete"));
    }

    private void Cancel()
    {
        ModalInstance.CancelAsync();
    }
}
```

### Modal 호출
Modal을 호출하기 위해서는 `IModalService`를 inject 해줘야 합니다.

```cshtml
@page "/Issue/{id}"
@inject IModalService Modal 
@inject CommonService Service

<div>
    <MudButton Color="Color.Error" Size="Size.Medium" Variant="Variant.Filled" StartIcon="@Icons.Material.Filled.Delete" 
               Style="margin-left: 10px;" OnClick="ShowDeleteModal">삭제</MudButton>
</div>
  
@code {

    protected override async Task OnInitializedAsync()
    {
        issue = Service.db.Board.Where(x => x.Id.ToString() == Id).FirstOrDefault();
    }

    async Task ShowDeleteModal()
    {
        var options = new ModalOptions(){ DisableBackgroundCancel = true };  // Background 선택 시 Modal Cancel 되는 것 방지
        var formModal = Modal.Show<DeletePopup>("이슈 삭제", options);
        var result = await formModal.Result;

        if (result.Data != null)
        {
            if (result.Data.ToString() == "delete")
            {
                issue.IsDelete = true;
                issue.UpdatedTime = DateTime.Now;
                Service.db.SaveChanges();
            }
        }
    }
}
```

![image](https://user-images.githubusercontent.com/74305823/162677027-de49a5fb-c48d-41a9-ba4d-95154e161a2b.png)

<br>

***

## Route [🔝](#blazor)
- [Pass Route Parameters between Blazor Pages](https://wellsb.com/csharp/aspnet/pass-route-parameters-between-blazor-pages)

    ```razor
    <h2>First Page</h2>
    <input type="number" @bind="age" /><br />
    <a href="/page2/@age.ToString()" >
    Go to Page 2
    </a>

    @code {
        int age = 0;
    }
    ```

    ```razor
    @page "/page2/{age}"
    <h2>Second Page</h2>
    <p>You are @Age years old.</p>

    @code {
        [Parameter]
        public string Age { get; set; }
    }
    ```

- [ASP.NET Core Blazor 라우팅 및 탐색](https://docs.microsoft.com/ko-kr/aspnet/core/blazor/fundamentals/routing?view=aspnetcore-6.0)
 
<br>

## Parameter [🔝](#blazor)
- [Blazor cascading values and parameters](https://www.pragimtech.com/blog/blazor/blazor-cascading-values-parameters/)
- [ASP.NET Core Blazor 연계 값 및 매개 변수](https://docs.microsoft.com/ko-kr/aspnet/core/blazor/components/cascading-values-and-parameters?view=aspnetcore-6.0)
    
    #### `ParentComponent.razor`
    ```razor
    <h1 style="@Style">Parent Component Text</h1>

    <CascadingValue Value="@Style" Name="ColorStyle" IsFixed="true">
        <ChildComponent></ChildComponent>
    </CascadingValue>

    @code {
        public string Style { get; set; } = "color:red";
    }
    ```
    
    #### `ChildComponent.razor`
    ```razor
    <h1 style="@ElementStyle">-Child Component Text</h1>

    @code {
        [CascadingParameter(Name = "ColorStyle")]
        public string ElementStyle { get; set; }
    }
    ```

<br>

## Validation [🔝](#blazor)
- [Blazor form validation](https://www.pragimtech.com/blog/blazor/blazor-form-validation/)
- [How to use Blazor EditForm for Model Validation](https://executecommands.com/blazor-editform-model-validation-aspnetcore-5/)
 
    #### Add Validation and Error Messages
    ```csharp
    using System;
    using System.ComponentModel.DataAnnotations;
    
    namespace BlazorEditFormSample.Data
    {
        public class Person
        {
            public int Id { get; set; }
            
            [Required(ErrorMessage = "Name Field is required")]
            public string Name { get; set; }

            [EmailAddress(ErrorMessage = "유효한 이메일 형식이 아닙니다.")]
            public string Email { get; set; }
        }
    }
    ```
    
    #### EditForm 
    ```razor
    <EditForm Model="@Person" OnValidSubmit="Save">
    
        <DataAnnotationsValidator />
        
        <div class="row col-md-6">
             <div class="form-item col-md-7">
                <lable class="search-label">이름</lable>
                <input class="input-text" @bind-value="@Person.Name"/>
                <ValidationMessage For="@(()=>Person.Name)" />     
            </div>
            <div class="form-item col-md-7">
                <lable class="search-label">이메일</lable>
                <input class="input-text" @bind-value="@Person.Email"/>
                <ValidationMessage For="@(()=>Person.Email)" />  
            </div>
            ...
        </div>
        <MudButton ButtonType="ButtonType.Submit" Variant="Variant.Filled" Color="Color.Primary">Save</MudButton>
    </EditForm>
    ```
 
<br>

## Javascript [🔝](#blazor)
- [JavaScript 함수 호출](https://docs.microsoft.com/ko-kr/aspnet/core/blazor/javascript-interoperability/call-javascript-from-dotnet?view=aspnetcore-6.0)

<br>

## NPM [🔝](#blazor)
- [Using NPM Packages in Blazor](https://brianlagunas.com/using-npm-packages-in-blazor/)

<br>

## Components [🔝](#blazor)
- [Introduction To Templated Components In Blazor](https://www.c-sharpcorner.com/article/introduction-to-templated-components-in-blazor/)

- Custom ToggleButton
    #### `ToggleSwitch.razor`
    ```razor
    <style>
        .input-toggle {
            cursor: pointer;
            position: relative;
            height: 20px;
            width: 40px;
            -webkit-appearance: none;
            background: darkgray;
            outline: none;
            border-radius: 15px;
        }

        .input-toggle:before {
            cursor: pointer;
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 20px;
            height: 20px;
            transform: scale(0.85);
            border-radius: 50%;
            background: white;
            transition: .3s;
        }

        .input-toggle:checked {
            background: #1b6ec2;
        }

        .input-toggle:checked:before {
            left: 20px;
        }
    </style>

    <input class="input-toggle" type="checkbox" @bind="Value" />

    @code {
        [Parameter]
        public EventCallback<bool> ValueChanged { get; set; }

        private bool _value;
        [Parameter]
        public bool Value
        {
            get { return _value; }
            set
            {
                if(_value != value)
                {
                    _value = value;
                    ValueChanged.InvokeAsync(_value);
                }
            }
        }
    }
    ```
    
    #### `Index.razor`
    ```razor
    <ToggleSwitch Value="@context.EmailConfirmed" ValueChanged="@((bool e) => ConfirmedChanged(e, context.Id))"/>
    
    @code {
        private void ConfirmedChanged(bool useYN, string id)
        {
            var user = LabC.db.Users.Where(x => x.Id == id).SingleOrDefault();
            user.EmailConfirmed = useYN;
            LabC.db.SaveChanges();
        }
    }
    ```

<br>

## Navigate [🔝](#blazor)
- [Open a page in a new tab](https://docs.microsoft.com/en-us/answers/questions/217767/blazor-open-a-page-in-a-new-browser-tab-using-navi.html)

    #### `JSRuntime`
    ```razor
    @inject IJSRuntime jsRuntime

    <button @onclick="NavigateToNewTab">New Tab Navigation</button>

    @code {

        public async Task NavigateToNewTab()
        {
            string url = "/counter";
            await jsRuntime.InvokeAsync<object>("open", url, "_blank");
        }
    }
    ```

    #### `'a' tag` 
    ```html
    <a href="/counter" target="_blank"></a>
    ```

- [NavigationManager Cheatsheet](https://stackoverflow.com/questions/50102726/get-current-url-in-a-blazor-component/53448294#53448294)
    ```razor
    @inject NavigationManager MyNavigationManager
    ```

    ```python
    MyNavigationManager.Uri
    #> https://localhost:5001/counter/3?q=hi

    MyNavigationManager.BaseUri
    #> https://localhost:5001/

    MyNavigationManager.NavigateTo("http://new location")
    #> Navigates to new location

    MyNavigationManager.LocationChanged
    #> An event that fires when the navigation location has changed.

    MyNavigationManager.ToAbsoluteUri("pepe")
    #> https://localhost:5001/pepe

    MyNavigationManager.ToBaseRelativePath(MyNavigationManager.Uri)
    #> counter/3?q=hi
    ```

<br>

## Syntax [🔝](#blazor)
- [Use ternary operator in razor](https://stackoverflow.com/questions/4091831/how-to-use-ternary-operator-in-razor-specifically-on-html-attributes)

    ```razor
    <a class="@(User.Identity.IsAuthenticated ? "auth" : "anon")">My link here</a>
    ```

<br>

## HttpContext [🔝](#blazor)
- [Using the HttpContext in Blazor Server the right way](https://www.youtube.com/watch?v=Eh4xPgP5PsM)

<br>

## File Upload [🔝](#blazor)
- [ASP.NET Core Blazor 파일 업로드](https://docs.microsoft.com/ko-kr/aspnet/core/blazor/file-uploads?view=aspnetcore-6.0&pivots=server)

    ```razor
    @inject IWebHostEnvironment Env
    
    <InputFile OnChange="@OnInputFileChanged" multiple />
    
    @code {
        private async Task OnInputFileChanged(InputFileChangeEventArgs e)
        {
            foreach(var file in e.GetMultipleFiles())
            {
                var newFileName = String.Concat(Convert.ToString(Guid.NewGuid()), Path.GetExtension(file.Name));
                var folder = Path.Combine(Env.WebRootPath, "files");
                var filePath = folder + $@"\{newFileName}";

                if (!Directory.Exists(folder))
                {
                    Directory.CreateDirectory(folder);
                }

                await using FileStream fs = new(filePath, FileMode.Create);
                await file.OpenReadStream().CopyToAsync(fs);  
            }
        }
    }
    ```
    
    > **OpenReadStream enforces a maximum size** in bytes of its Stream. Reading one file or multiple files **larger than 512,000 bytes (500 KB) results in an exception**. This limit prevents developers from accidentally reading large files into memory. The maxAllowedSize parameter of OpenReadStream can be used to specify a larger size if required up to a maximum supported size of 2 GB. <br><br>
    > The 2 GB framework file size limit only applies to ASP.NET Core 5.0. **In ASP.NET Core 6.0 or later, the framework doesn't limit the maximum file size.**
<br>

## File Download [🔝](#blazor)
- [ASP.NET Core Blazor 파일 다운로드](https://docs.microsoft.com/ko-kr/aspnet/core/blazor/file-downloads?view=aspnetcore-6.0)
    
    #### `Razor`
    ```razor
    @using System.IO
    @inject IJSRuntime JS
    @inject IWebHostEnvironment Env
    
    <div class="board">
        @foreach (var file in boardFiles)
        {
            <button @onclick="(() => DownloadFileFromStream(file.BoardFiles))">
                @file.Name
            </button>
        }
    </div>
    
    @code {
        private Stream GetFileStream(string path)
        {
            var data = File.ReadAllBytes(path);
            var fileStream = new MemoryStream(data);

            return fileStream;
        }
    
        private async Task DownloadFileFromStream(Contents_Files file)
        {
            var folder = Path.Combine(Env.WebRootPath, "files");
            var filePath = folder + $@"\{file.FileNameSave}";
            var fileStream = GetFileStream(filePath);
            var fileName = file.FileNameOrigin;

            using var streamRef = new DotNetStreamReference(stream: fileStream);

            await JS.InvokeVoidAsync("downloadFileFromStream", fileName, streamRef);
        }
    }
    ```
    
    #### `Javascript`
    ```js
    async function downloadFileFromStream(fileName, contentStreamReference) {
        const arrayBuffer = await contentStreamReference.arrayBuffer();
        const blob = new Blob([arrayBuffer]);
        const url = URL.createObjectURL(blob);

        triggerFileDownload(fileName, url);

        URL.revokeObjectURL(url);
    }

    function triggerFileDownload(fileName, url) {
        const anchorElement = document.createElement('a');
        anchorElement.href = url;
        anchorElement.download = fileName ?? '';
        anchorElement.click();
        anchorElement.remove();
    }
    ```

<br>

***

## Blazor Server Disconnected [🔝](#blazor)

- [large amount of contents cause blazor to disconnect](https://github.com/tinymce/tinymce-blazor/issues/8)

#### `Program.cs`
```csharp
builder.Services.AddServerSideBlazor().AddHubOptions(o =>
{
    o.MaximumReceiveMessageSize = 10 * 1024 * 1024; // 10MB
});
```

> base64가 포함된 이미지 문자열이 있을 때 Blazor 서버 연결이 끊기는 경우가 발생함.
