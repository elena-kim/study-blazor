# Blazor

### `Nuget Package`
- [MudBlazor](#mudblazor)
- [BlazoredModal](#blazoredmodal)

### `Reference`
- [Route](#route)
- [Validation](#validation)
- [Javascript](#javascript)
- [Components](#components)
- [Navigate](#navigate)

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

## BlazoredModal

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

***

## Route
- [Pass Route Parameters between Blazor Pages](https://wellsb.com/csharp/aspnet/pass-route-parameters-between-blazor-pages)
- [ASP.NET Core Blazor 라우팅 및 탐색](https://docs.microsoft.com/ko-kr/aspnet/core/blazor/fundamentals/routing?view=aspnetcore-6.0)
 
<br>

## Validation
- [Blazor form validation](https://www.pragimtech.com/blog/blazor/blazor-form-validation/)
- [How to use Blazor EditForm for Model Validation](https://executecommands.com/blazor-editform-model-validation-aspnetcore-5/)
 
<br>

## Javascript
- [JavaScript 함수 호출](https://docs.microsoft.com/ko-kr/aspnet/core/blazor/javascript-interoperability/call-javascript-from-dotnet?view=aspnetcore-6.0)

<br>

## Components
- [Introduction To Templated Components In Blazor](https://www.c-sharpcorner.com/article/introduction-to-templated-components-in-blazor/)

<br>

## Navigate
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
<a href="/counter" target="blank"></a>
```
