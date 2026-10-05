Phase 1: Interactive Profile Header & Favorite Button

A StatelessWidget is used when the widget does not need to keep track of changing data. A StatefulWidget is used when the widget needs to maintain data that can change while the app is running.

For the FavoriteButton, I used a StatefulWidget because the button needs to remember whether it has been favorited. The _isFavorited boolean is stored in the button's state and changes when the user taps the button.

A StatelessWidget would not be a good choice for this button because it does not have its own mutable state. Simply changing a variable would not cause the widget to rebuild with the new icon and color. With setState(), Flutter knows that the state changed and rebuilds the widget so the star changes between the grey outlined star and the amber filled star.

I kept the favorite state inside FavoriteButton because no other part of the application needs to use this information. This makes it an example of ephemeral or local state.
