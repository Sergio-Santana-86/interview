ASP.NET MVC Interview
=====================

- What is **ASP.NET MVC**?

ASP.NET MVC **is a web application Framework**, It is light weight and highly testatable Framework. MVC separates ppliation into 3 components Model, View and Controller

- What is a **Model**?

**Model** are usually **used to transfer data back and foth between controllers and views**. It is a business entity and it is used to represent the appliation data.

**View** are **responsible for rendering of the appropriate UI**.

**Controller** is the **application logic**.
A controller is a set of Action Methods.

- Explain the page life cycle of MVC?

* App initialization

* routing

* Instantiate and execute controller

* Locate and invoke controller action

* Instantiate and render view

- How are registered the routes in ASP.NET MVC?
in **App_Start/RouteConfig.cs** are defined the route patters
`public static void RegisterRoutes(RouteCollection routes) {
  routes.IgnoreRoute("{resourse}.axd/{xpathInfo});
  routes.MapRoute({
    name:"Default",
    url:"{controller}/{action}/{id}",
    defaults: new { controller = "Home", action = "Index", id=UrlParameter.Optional }
  });
}`
in **Global.asax** are registered when the application start
`protected void Application_Start(object sender, EventArgs e)
{
  AreaRegistration.RegisterAllAreas();
  FilterConfig.RegisterGlobalFilters(GlobalFilters.Filters);
  RouteConfig.RegisterRoutes(RouteTable.Routes);
}`

- What is **(SoC) Separation of Concerns** in ASP.NET MVC?

It's the process of **breaking the program into varios distinct features which overlaps in functionality as little as possible**.
MVC patter concerns on separating the content from presentation and data-processing from content.

- What is **Razor View Engine**?

Razor is the first major update to render HTML in ASP.NET MVC 3. **Razon was designed specifically for view engine syntax**
Main focus of this would be to simply and code-focused templating for HTML generation.

`@model ASP.Net MVCMusicStore.Models.Customer
@{
  ViewBag.Title = "Get customers";
}
<h1>@Model.CustomerName</h1>`

- What are **Action Selectors**?

**Are attributes that can be applied to an action in a controller** and are used to control or incluence which Action Method get Invoked

- What is **ActionName Selector**?

**Is an action selector that is used to invoke an action method with different name**.

`public class HomeController : Controller
{
  [ActionName("List")]
  public string Index()
  {
    return "Index action method invoked";
  }
}`

- What are **Action Filters**?

**Are used to implement logic that gets executed before and after a _controller action executes_**

**Action filters allow us to add PRE and POST processing logic to an action method**. They allow us to modify the way in chich an action is executed.

Are attirbutes that can be applied either on a contoller action method or an a controller. When applied at the controller level, they are applicable for all actions within that controller.


- Name a few **action filters** in mvc?

* Authorize 

By default, all the controller action methods are accesible to both anonymous and authenticated users. If you want **action methods to be available only for authenticated and authorised users** then use Authorize attribute.

* ChildActionOnly

* HandleError

`[HandledError]
public class ActionFilterDemoController : Controller
{
  public ActionResult Index()
  {
    throw new NullReferenceException();
  }
  public ActionResult About()
  {
    return View();
  }
}`

* OutputCache 

`[HttpGet]
[OutputCache(Duration=10)]`
public string Index()
{
  return DateTime.Now.ToString("T");
}

* RequireHttps

* ValidateInput

* ValidateAntiForgeryToken 

- What are **Result Filters**?
**Perform some operation before or after the execution of the _view result_**.

- What are **Action Result**?

**Action result represent a coomand that the framework performs on behalf of the action method**.

Action Result is a result of action methods or return types of action methods. Action result is an abstract class. It is a base class for all type of action results. 


- Which are the **Types of Action Results**?

* **View Result**

`public ViewResult About() {
  return View();
}`

* **Partial View Result**

`public PartialViewResult Index() {
  return PartialView("_PartialView");
}`

* **Redirect Result** redirect to specific URL

`public RedirectResult Index() {
  return Redirect("Home/Contact");
}`

* **Redirect to Action Result** redirect to a specified controler and action method.

`public ActionIndex() {
  return RedirectToAction("Login", "Account");
}`

* **JSON Result** return a simple text in json format

`public ActionResult Index() {
  return Json(persons, JsonRequestBehavior.AllowGet);
}`

* **File Result **

`public ActionResult Index() {
  return File("Web.Config", "text");
}`

* **Content Result** returns different content's format to the view

`public ActionResult Contact() {
  return Content("<script>alert('Welcome To All');</script>");
}`

ASP.NET MVC - State Management
------------------------------

ASP.NET MVC provides state management techniques that can help us to maintain the data when redirecting from one page to other page or in the same page after reloading.

There are several ways to do this in ASP.NET MVC

* **Hidden Field**

**Hidden field is used to hide your data on client side**. It is not directly visible to the user on UI but we can see the value in the page source. So, this is not recommended if you want to store a sensitive data. It’s only used to store a small amount of data which is frequently changed.

`@Html.HiddenFor(x=>x.Id)`
 
* **Cookies**

**Cookies are used for storing the data** but that data should be small. It is like a small text file where we can store our data. The good thing is that a cookie is created on client side memory in the browser. Most of the times, we use a cookie for storing the user information after login with some expiry time. 
Basically, a** cookie is created by the server and sent to the browser in response. The browser saves it in client-side memory**.

`HttpCookie cookie = new HttpCookie("TestCookie");  
cookie.Value = "This is test cookie";  
this.ControllerContext.HttpContext.Response.Cookies.Add(cookie);`

* **Query String**

**query string** is used to pass the value(s) from one page to another page using the url.

url?parm1=1&parm2=2

`http://localhost:49985/home/editemployee?name=TestValue`

* **ViewData**

It helps us to maintain your data when sending the **data from Controller to View**. **It is a dictionary** object and derived from ViewDataDictionary. As it is a dictionary object, it takes the data in a key-value pair.

`ViewData["Message"] = "this is ViewData";
viewData["EmployeeName"] = "Sergio Santana";`

* **ViewBag**

Is the same as viewdata to **send data from controller to the view**, the difference is that **it use dynamic properties** introduced in C# v4

`ViewBag.Message = "this is ViewBag";
ViewBag.Year = 2019;`

* **TempData**

**TempData** is also a dictoniary object as ViewData and stores values in key/value pair. It is derived from tempDataDictionary.

It is mainly used **to transfer the data from one request to another request** or we can say subsequent request.

** IF DATA IN TEMPDATA IS READ THEN IT WOULD NOT BE AVAILABLE FOR THE SUBSEQUENT REQUESTS**.

- What are **Area** in ASP.NET MVC?

**Area is used to store the details of the modules of our project**. This is really helpful for big applications, where controllers, views and models are all in main controller, view and models folders and it is very difficult to manage.
