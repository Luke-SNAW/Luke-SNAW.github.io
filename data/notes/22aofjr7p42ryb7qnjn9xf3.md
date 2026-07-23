
> https://youdontneedamodalwindow.dev/

Just make a separate page.

Maybe you have a master/detail setup on your web app. There's a list of products/documents/whatever, and clicking on one brings up the details.

Close **XYZ-489**

## Example 2

Lorem ipsum dolor, sit amet consectetur adipisicing elit. Doloremque blanditiis nulla consectetur labore expedita corrupti nihil saepe iste perferendis exercitationem praesentium, possimus iusto itaque numquam vel ut officiis explicabo enim.

| ID      | Name      |
| ------- | --------- | ------------------------------------------------ |
| XYZ-173 | Example 1 | [Details](https://youdontneedamodalwindow.dev/#) |
| XYZ-489 | Example 2 | [Details](https://youdontneedamodalwindow.dev/#) |

Don't open the details in a modal window. Have it be a separate page.

**Modal windows can't be bookmarked or shared as links.** Deep linking can be added to modals, but it's complex. What will show up in the background when the link is followed? How much application state needs to be restored? How will the user be confident that it will work?

**Modal windows can't be opened in a new tab.** Even if you implement this, you'll be forcing users to duplicate the page underneath.

**Modal windows make the Back button confusing.** Will it close the modal and return to the page in the background, or return to the page you were before that?

**Modal windows are hard to get right.** The "final boss of accessibility". If you have access to `<dialog>`, it's easier — if you need to support older browsers, good luck. There's a very good chance the modal window you have in production has dealbreaking bugs.

Consider if the modal window is really the best choice. There are many reasons modal dialogs are used when they're not appropriate:

**To compensate for slow page load**

Web apps should pass the "refresh test": If I sneak up behind your user and refresh their tab, their frustration should be negligible and no data should be lost.

**Because it seems easy**

Many UI toolkits offer modals out-of-the-box. A developer might be tempted to reach for it to _zhoozh up_ the app. Really _make it pop_, you know.

**Because it looked good in the mockup**

You're designing a website, not a Figma artboard.

Modal windows can be used for views that don't constitute a "resource" or correspond to a domain entity:

- Alerts
- Confirmation dialogs
- Forms for creating/updating entities

Bonus: RESTful UI

---

## [fzaninotto](https://news.ycombinator.com/user?id=fzaninotto)

> https://marmelab.com/react-admin-demo/#/reviews

When clicking on a review, the detail appear on the same page. This allows to quickly browse through reviews, and preview some before doing batch edition. It's super effective.

Notice that you can bookmark any review detail, too.
