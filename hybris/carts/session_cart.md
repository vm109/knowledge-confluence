## Questions
1. Why do we use session cart instead of cartId? 
    - since `CartMatchingFilter` match regex to cartId in the url and loads the cartId for the user
    - so retrieving session cart will retrieve the cart for the user.