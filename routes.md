Routing
- Conventional routing typically used with controllers and views.
- Attribute routing used with REST APIs. 


Conventional Routing
- Conventional routing is used with controllers and views. The default route:
- in program.cs
app.MapControllerRoute(
    name: "default",
    pattern: "{controller=Home}/{action=Index}/{id?}");
    

- Produces the route values { controller = Home, action = Index }.
- The first path segment, {controller=Home}, maps to the controller name.
- The second segment, {action=Index}, maps to the action name.
- The third segment, {id?} is used for an optional id. The ? in {id?} makes it optional. id is used to map to a model entity.

- {controller=Home} defines Home as the default controller.

- {action=Index} defines Index as the default action.

- The ? character in {id?} defines id as optional.

- Default and optional route parameters don't need to be present in the URL path for a match. See Route Template Reference for a detailed description of route template syntax.
- Matches the URL path /.

