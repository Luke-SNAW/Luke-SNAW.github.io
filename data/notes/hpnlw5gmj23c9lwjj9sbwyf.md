
> https://adamsilver.io/blog/form-design-from-zero-to-hero-all-in-one-blog-post/

## [Don’t mark required fields with an asterisk](https://adamsilver.io/blog/how-to-highlight-required-and-optional-form-fields/)

Highlight optional fields instead. To do this, add ‘(optional)’ to the label of any optional field.

Highlighting optional fields only reduces noise. Minimal noise. Maximum clarity.

But the best forms avoid optional fields altogether.

## [How to avoid optional form fields with a conditional reveal](https://adamsilver.io/blog/how-to-avoid-optional-form-fields-with-a-conditional-reveal/)

Start by asking the user if they want to get delivery updates. And if they say yes ask for the mobile phone number:
Conditionally revealing a form field based on selected radio buttons

Now there’s no optional fields. And no risk of users missing the chance to get delivery updates by text message.

---

Hi there. If we haven’t met before, I’m Adam and I’m obsessed with designing forms. And I have been for almost 20 years.

What is it about forms then?

Every meaningful interaction on the web is achieved by a form of some sort. Whether it’s letting users renew their passport, send an email or buy something.

Basically anything that isn’t just reading content.

What’s interesting though is that on first glance, forms are easy. In a few minutes you can have text boxes and radio buttons on screen and working.

But look around the internet for a minute, and you’ll find a million and one usability issues revolving around forms.

I’m pretty sure I’ve come across every single one of them. And spent hours solving each one in a way that works for everyone.

And some forms have more than just fields and buttons. They can contain complex interactions or form part of a wider journey—both of which need due care and attention.

So, if I was designing a new form, I’d want to know how to avoid the common issues. And to use my time to solve newer and perhaps more difficult problems.

Seriously, who wants to spend time solving something that’s already been solved?

That’s right—nobody.

## A note before we begin

Much of what I’m going to say might sound obvious and boring. But [boring is good](https://capwatkins.com/blog/the-boring-designer), we don’t need to over complicate matters.

So if you’re looking for new and innovative ways to design forms, this is not for you.

This is about designing forms that everyone can use and complete as quickly as possible. Because nobody actually wants to use your form. They just want the outcome of having used it.

This guide is quick and to the point—a whistle stop tour of the knowledge I’ve accrued in my years of form design. It’s not exhaustive, but rather an entry point, designed to save you time on the basics.

Many points I make link off to other articles. If you read each of them, you’ll be more than equipped to make simple and accessible forms that get out of the user’s way.

Let’s begin.

## Don’t mess with labels

[Every input needs a label](https://adamsilver.io/blog/always-use-a-label/).

[Placeholders suck](https://adamsilver.io/blog/the-problem-with-placeholders-and-what-to-do-instead/) and [float labels suck too](https://adamsilver.io/blog/the-problem-with-float-labels-and-what-to-do-instead/).

Seriously, don’t mess with labels.

## Crafting questions

Only ask for information you need.

Avoid double-barrelled questions because they’re hard to understand.

[Don’t mark required fields, mark optional ones](https://adamsilver.io/blog/how-to-highlight-required-and-optional-form-fields/). Better yet, [avoid optional fields](https://adamsilver.io/blog/how-to-avoid-optional-form-fields-with-a-conditional-reveal/).

Use hint text to tell users why you’re asking them for certain information—it’s not always obvious. Or if the user has to satisfy a complex set of password rules.

Error messages should be a last resort.

## Style and microcopy

Inputs are not for entertainment so make inputs look like inputs.

Make your inputs 44px in height or more.

The width of an input gives users a clue about the length of content required. So don’t make all inputs the same size for aesthetic purposes.

Avoid [multi column form layouts](https://baymard.com/blog/avoid-multi-column-forms). They’re error prone, slower to use and can cause abandonment.

Make buttons look like buttons and [put them in the correct position](https://adamsilver.io/blog/where-to-put-buttons-on-forms/).

[Use sentence case for labels, hint text and errors](https://medium.com/@jsaito/making-a-case-for-letter-case-19d09f653c98) because it’s easier to read and spot nouns.

[Use verbs for button text](https://adamsilver.io/blog/3-common-examples-of-button-text-that-degrades-ux-and-how-to-rewrite-them-so-theyre-clear/).

## Form validation

[Don’t disable buttons](https://adamsilver.io/blog/the-problem-with-disabled-buttons-and-what-to-do-instead/).

[Don’t validate as the user types](https://adamsilver.io/blog/the-problem-with-live-validation-and-what-to-do-instead/).

[Don’t use default validation](http://adrianroselli.com/2019/02/avoid-default-field-validation.html),

[Avoid the `maxlength` attribute](https://adamsilver.io/blog/dont-use-the-maxlength-attribute-to-stop-users-from-exceeding-the-limit/).

Validate on submit.

Forgive trivial mistakes like extra spaces.

[Show errors above the input, not below](http://adrianroselli.com/2017/01/avoid-messages-under-fields.html).

Colour errors red and use a warning icon to provide a comparable experience for colour blind users.

Error messages should be clear and concise.

## Flow

[Start by putting each question onto a page of its own](https://www.smashingmagazine.com/2017/05/better-form-design-one-thing-per-page/).

Put [back links in the top left of the page](https://adamsilver.io/blog/where-to-put-buttons-on-forms/#put-the-back-button-above-the-form). Avoid putting links within the body of the form as it [disrupts the tab sequence](https://adamsilver.io/blog/where-to-put-buttons-on-forms/#put-tangentially-related-actions-above-the-form).

Let users [check their answers and make changes before submission](https://design-system.service.gov.uk/patterns/check-answers/).

After submission show users a confirmation page and send them an email.

Now’s the best time to let your brand shine through because this is the beginning of the relationship—not the end.

## Optimise

Use the [browser’s autofill routine](https://www.smashingmagazine.com/2017/03/improve-billing-form-ux/) to stop users from typing data manually and avoid typos.

Use `autocapitalize="none"`, `autocorrect="off"` and `spellcheck="false"` to stop browsers automatically changing user input on fields that expect grammatically incorrect data—like email addresses and passwords.

## Use the right input type

Don’t mix up radio buttons and checkboxes. Remember [you can include more than 7 options](https://uxmyths.com/post/931925744/myth-23-choices-should-always-be-limited-to-seven).

[Select boxes should be a last resort](https://www.youtube.com/watch?v=CUkMCQR4TpY) because they’re hard to use.

Don’t use `datalist` as it’s [buggy and lacks support](https://caniuse.com/#feat=datalist). Use an [accessible autocomplete instead](https://adamsilver.io/blog/building-an-accessible-autocomplete-control/).

Use three separate text boxes for dates. Only use a date picker when users need to find a date in relation to another, or if they need to know the day, week or month that the date relates to. Date pickers are really tricky so roll up your sleeves.

Use a [stepper component](https://nostyle.onrender.com/components/stepper) to help users make small numerical adjustments quickly and easily.

[Avoid multi-input fields](https://adamsilver.io/blog/form-design-multiple-inputs-versus-one-input) like when asking for a sort code.

File uploads: accept large files; accept as many file types as you can; don’t rely on the `multiple` attribute because it lacks support and only allows users to select files from a single directory.

That probably took you about 2.5 minutes to read.

But if you’d like to master form design and have 2.5 hours to spare, you might like my course, Form Design Mastery:

[https://formdesignmastery.com](https://formdesignmastery.com/)
