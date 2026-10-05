Phase 1: Interactive Profile Header & Favorite Button

A StatelessWidget is used when the widget does not need to keep track of changing data. A StatefulWidget is used when the widget needs to maintain data that can change while the app is running.

For the FavoriteButton, I used a StatefulWidget because the button needs to remember whether it has been favorited. The _isFavorited boolean is stored in the button's state and changes when the user taps the button.

A StatelessWidget would not be a good choice for this button because it does not have its own mutable state. Simply changing a variable would not cause the widget to rebuild with the new icon and color. With setState(), Flutter knows that the state changed and rebuilds the widget so the star changes between the grey outlined star and the amber filled star.

I kept the favorite state inside FavoriteButton because no other part of the application needs to use this information. This makes it an example of ephemeral or local state.

--------------------------

Phase 2: Profile Input Form & Validation

The GlobalKey<FormState> gives the ProfileForm access to the current state of the Form. I use the key when calling _formKey.currentState!.validate() to tell Flutter to run the validators for the form's input fields.

When validate() is called, Flutter runs the validator function for the TextFormField. If the validator returns a String, Flutter considers the field invalid and displays that String as an error message underneath the field. If the validator returns null, the field is considered valid.

I also used a TextEditingController to retrieve the username entered by the user. The controller is disposed of in the dispose() method because it is no longer needed after the ProfileForm is removed from the widget tree. This helps prevent memory leaks.

The form only displays the SnackBar when the username passes validation. If the username is empty, the validation error is displayed instead.

------------------------

Phase 3: Connecting the Dots — Lifting State Up

The username needed to be moved from ProfileForm to ProfileScreen because the username is now shared between multiple widgets. The UserBanner needs the username to display the greeting, while the ProfileForm needs to update the username. ProfileScreen is their common parent, so it is the appropriate place to store the shared state.

I changed ProfileScreen into a StatefulWidget and added _currentUsername. The _updateUsername() method uses setState() to update the username and rebuild the screen.

I passed the username from the parent down to UserBanner through the username property. I also passed _updateUsername down to ProfileForm as a callback. When the form is successfully submitted, it calls the callback with the username that the user entered.

The FavoriteButton state does not need to be lifted because the rest of the application does not need to know whether the profile is favorited. Only the button uses _isFavorited, so keeping that state inside the FavoriteButton makes the widget self-contained and easier to manage.
