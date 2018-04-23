# How to redirect a user to a separate webpage, according to the selected appointment


<p>This example illustrates how to redirect an end user to a separate webpage when the custom appointment menu item is clicked. Note that the technique from the <a href="https://www.devexpress.com/Support/Center/p/E291">How to change default menu items and actions in the popup menu</a> code example is used to add a custom menu action in the following manner:<br />
</p>

```cs
    protected void ASPxScheduler1_PopupMenuShowing(object sender, PopupMenuShowingEventArgs e) {
        if (e.Menu.Id.Equals(SchedulerMenuItemId.AppointmentMenu)) {
            MenuItem item = new MenuItem("Redirect", "RedirectItem");

            e.Menu.Items.Insert(0, item);
            e.Menu.ClientSideEvents.ItemClick = String.Format("function(s, e) {{ AppointmentMenuHandler({0}, s, e); }}", ASPxScheduler1.ClientInstanceName);
        }
    }

```



```js
        function AppointmentMenuHandler(scheduler, s, args) {
            if (args.item.GetItemCount() <= 0) {
                if (args.item.name == "RedirectItem")
                    window.location = 'NewPage.aspx?aptId=' + scheduler.GetSelectedAppointmentIds()[0];
                else
                    scheduler.RaiseCallback("MNUAPT|" + args.item.name);
            }
        }

```

<p>As you can see, the actual redirection is accomplished on the client side by modifying the <a href="http://www.w3schools.com/jsref/obj_location.asp"><u>window.location</u></a> attribute. The selected appointment Id is passed to a separate page via the <strong>aptId </strong>URL parameter.</p><p>In addition, page caching for the webpage with the ASPxScheduler control is disabled (see the <strong>DisablePageCaching</strong><strong>()</strong> method in the Default.aspx.cs code-behind file) because it might not operate correctly in some browsers when reloaded from the cache if you click the back button on the browser to return from the NewPage.aspx to the Default.aspx webpage.</p><p><strong>See Also:</strong><br />
<a href="http://documentation.devexpress.com/#AspNet/DevExpressWebASPxSchedulerScriptsASPxClientSchedulerMembersTopicAll"><u>ASPxClientScheduler Members</u></a></p>

<br/>

