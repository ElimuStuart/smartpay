Build & Style The UI
Step 1
Style the BODY element with a white background color.

Within the BODY tag, create a DIV and give it a data-cart-info attribute. Inside this DIV, create a HEADING element with mdc-typography--headline4" as its CSS class.

The HEADING element should have 2 SPAN children elements. The First SPAN element displays a shopping cart by setting it's CSS class to material-icons and its content to shopping_cart. The second SPAN element should have a data-bill attribute and will be used to display the total figure the user is trying to pay on the app.

Create another DIV just after the data-cart-info DIV. Give this new DIV a data-credit-card attribute and set its class to mdc-card and mdc-card--outlined . Within the data-credit-card DIV you just created, add a new DIV with a class of mdc-card__primary-action. These elements will be styled with the look and feel of an actual credit card. Brace yourself!

Within the .mdc-card__primary-action DIV, create an IMAGE with an attribute of data-card-type and set its source to [https://placehold.it/120x60.png?text=Card](https://placehold.it/120x60.png?text=Card). This IMAGE will be used to display the credit card type (Visa or MasterCard), based on the series of numbers entered by the user.

Right after the IMAGE and still within the mdc-card__primary-action DIV, create a new DIV with an attribute of data-cc-digits. It should contain four INPUT text fields, each with a size of 4 and a placeholder of ---- (4 dashes). These fields will be used to collect the credit card numbers from the user.

Create a DIV with an attribute of data-cc-info as a sibling to the data-cc-digits DIV. This new DIV should have two INPUT text fields, one for entering the card holder's name while the other will be for the card's expiry date. The first field should have a size of 20 and a placeholder of Name Surname. The expiry date field should have a size of 6 and a placeholder of MM/YY - indicating the expiry date format.

We are now done with the structure of the credit card component. Let's make a button to allow the user make payment with the card details

Create a BUTTON as a sibling to the data-credit-card DIV. Set the BUTTON's class to mdc-button and give it a data-pay-btn attribute. It should have Pay Now as its display text. After the user enters details of the card and clicks on this button, the app will strike-though the card details that are in-valid, if any.
Step 2
While we might have the right structure in place, the app visually tells a different story. Time to make the app look good and usable.

The SPAN elements within the data-cart-info DIV should be displayed as inline block elements and their vertical-align set to middle. The .material-icons SPAN should have a 150 pixels size of font.

Give the data-credit-card DIV 435px width, 240px minimum height, 10px rounded borders, and a #5d6874 background colour.

Display the data-card-type IMAGE as a block element. Give it a 120px width and a 60px height.

The data-cc-digits DIV should have a 2em top margin.

INPUT elements in the data-cc-digits DIV should have a white color, 2em font size and line height, no border or background, and a right margin of 0.5em;

The data-cc-info DIV should have a 1em top margin.

INPUT elements in the data-cc-info DIV should have a white color, 1.2em font size, no border and no background. The second input should also have a right padding of 10px and be floated to the right of the viewport.

The data-pay-btn BUTTON should have a fixed position, 90% width, a solid border of 1px and positioned 20px from the bottom of the viewport.

Your app should look better at this point. Ideally, the 4 input fields within the data-cc-digits DIV should all be on a single horzontal line.


SmartPay 
Challenge 2 of 4
Get The Bill
Write all Javascript strictly in ES6 syntax. This means use arrow functions instead of the function keyword. Declare variables and functions with const or let. Use const by default, and only use let if you are sure you need to re-assign values to the said variable. Use the Selector API instead of the getElementBy... or getElementsBy... APIs.

Install the JSON Viewer Chrome extension, open a new tab and go to this API endpoint. You will be making HTTP requests to the API, so spend some time looking at the structure of the response data.

Step 1
Within the SCRIPT element and just after the billHype function, create an appState variable and assign it an empty Object literal. This variable will hold data for the app.

Create a formatAsMoney function. It should take in an amount and a buyerCountry parameter. It will use these parameters to format the user's bill as a proper currency.

Create detectCardType, validateCardExpiryDate, and validateCardHolderName functions. detectCardType should be declared to accept first4Digits as a parameter represneting the first four digits of the 16-digit long credit card number. As implied by their names, these functions will play major roles in validating various aspects of the card being used for payment

Create a uiCanInteract function. It will be called to setup the UI, including adding event handlers to enable interactions with the app.

Create a displayCartTotal function. It should expect a parameter and should use object de-structuring to obtain the results property of the given parameter. This function will be called with the data from an API call and it will display the total bill to be paid.

Step 2
Update the fetchBill function. It should then use the browser's fetch function to make a HTTP request to apiEndpoint. Using an arrow function in a .then call to the fetch function, return the response after converting it to JSON. Using another .then call to the first one, pass the JSON data to displayCartTotal. Make sure to handle errors that may occur, e.g by showing a warning message in the console.

Call the fetchBill function from inside the startApp. This should be the only code or function call within startApp.

Step 3
In the body of the displayCartTotal function, de-structure the first item in the results array parameter into a data variable. Next, use object de-structuring to obtain the itemsInCart and buyerCountry properties from data. You might want to install the JSONViewer Chrome extension, open a new tab and navigate to https://randomapi.com/api/006b08a801d82d0c9824dcfdfdfa3b3c to see the shape of the JSON data we are dealing with.

Next, displayCartTotal should set appState.items to itemsInCart and appState.country to buyerCountry.

Use the Array .reduce function to calculate the total bill from itemsInCart Note that each item has a qty property indicating how many of that item the user bought. Assign the calculated bill to appState.bill

Go back to the formatAsMoney function. Use the in-built javascript .toLocaleString function on the amount and buyerCountry parameters to format amount as a currency with the currency symbol of buyerCountry. The countries and their currency symbols are in the countries array you got in your starter code. If the buyerCountry is not in countries, then use United States as the country and format the currency accordingly.

Continuing from where you left off in displayCartTotal, use the formatAsMoney function to set appState.billFormatted to the formatted total bill. The already assigned appState.bill and appState.country should be handy for this task!

Set the text content of the data-bill SPAN element to the formatted bill saved in appState.billFormatted

Assign an array literal to appState.cardDigits

Finally, call uiCanInteract to wrap up displayCartTotal

Run your app (click the play button) and see if the correct total bill is displayed in the UI with the right currency format. Next, we will allow input and interaction so that users can provide payment information.


SmartPay 
Challenge 3 of 4
Handle Simple Validation
Step 1
Create a flagIfInvalid function just after formatAsMoney function. This function is used to mark an input entry as invalid (strike-though) nor not. It should take a field and isValid parameters. If isValid is true, it should remove the is-invalid class from field, otherwise it should add it to field.

Just after flagIfInvalid function, create a expiryDateFormatIsValid function which takes a field parameter representing the card's expiry date field. It should return true if the field's value complies with the MM/YY format, otherwise it should return false.

With the above utility functions out of the way, go back to the validateCardExpiryDate function. This function should return true if the value provided matches the MM/YY format (hint: delegate to expiryDateFormatIsValid) AND if the date is in the future. In either case, it should use the flagIfInvalid function to mark the field as valid or not. It then has to return true or false depending on if the validation requirements are met or not.

Now to the validateCardHolderName function. Recall that its placeholder already suggests the required format, which is Name Surname (2 names separated by space). Each name should be at least 3 characters long. It should use the flagIfInvalid function to mark the field as valid or not and then return true or false depending on if the validation requirements are met or not.

Step 2
Create validateCardNumber and validatePayment functions above the uiCanInteract function.

In validatePayment, call validateCardNumber, validateCardHolderName, and validateCardExpiryDate functions in that order.

After that, create a smartInput function with event and fieldIndex as parameters. If you already created a acceptCardNumbers function, rename it to smartInput.

In the uiCanInteract function, give input focus to the first credit card number input field, then set validatePayment as the click event listener for the data-pay-btn BUTTON. Finally, end the uiCanInteract function (for now) by calling the billHype function

Try filling in the card holer's name and expiry date into the UI then click the Pay Now BUTTON to see if the details are correctly marked as invalid or not.

Try clicking on the shopping cart icon or the displayed total bill. Do you hear someone hyping how much you are about to pay?

SmartPay 
Challenge 4 of 4
Validate Payment Details
To have gotten here, you learnt a lot and demosntrated very good grasp of Web technologies. Respect!



This is where it gets even more interesting. This challenge will push you, but we believe you have built the muscle for it. We hope you will find this last challenge inspiring, thought provoking, ambitious but solvable.

When all four numbered buttons on the left of the screen get ticked off with a check icon, then you have completed this assessment. You can take a screenshot or capture a <= 2 minute video of your working app and share on Twitter with these hashtags: #150DaysOfALC4 #MyGradr #GrowWithGoogle

Step 1
Create a smartCursor function with event, fieldIndex, and fields as parameters. If you already created a typeAhead function, rename it to smartCursor.

Create a enableSmartTyping function. No parameters are required.

At the end of the uiCanInteract function, call the enableSmartTyping function.

The enableSmartTyping function should collect all the input fields into an array and use .forEach to iterate over them with an inline arrow function that takes field, index, and fields as parameters. The goal is to iteratively set a keydown event listener on each field in the collection.

On each field in the iteration with .forEach, add a keydown listener with an inline arrow function that takes in an event parameter. The function should call smartInput passing it the event object as event, the index of the given field as index, and the collection of the input fields as fields.
Step 2
You are going to implement a smarter and more secure credit card number input system with smartInput. Ideally, the user's credit card number should not be displayed in the open on the app. Just like password fields in forms, newly typed digits should only be displayed temporarily (for half a second) as the user types them. Only the last 4 digits are displayed perpertually. How sweet!

As the user types into the card number input fields, our keydown event listener is invoked and it calls smartInput with these parameters: (1) event - a keydown event that is fired as the user types into input fields

(2)    `fieldIndex` - from the collection of input fields, this is the zero-based index of the field trigeering the event.

(3)    `fields` - the collection of input fields you are iterating over
Implement smartInput as below :

smartInput will be called for every entry on every input field. You want to proceed only for valid entries and preventing the rest. So that you user can navigate around the fields and delete entries as well, you should allow the Tab, Shift, Backspace/Delete and Arrow keys as well as the actual valid input for each type of field, i.e the credit card fields vs the card holder's name field vs the expiry date

Every valid new entry for the card number fields should only be displayed for half a second, after which the character should be masked to conceal it from prying eyes. You can mask characters with #, $, or %.

Also for the card number fields since you will need the actual values the user entered (not the masked one in the UI), they should be saved as integer arrays in the right slot in the appState.cardDigits array. This means appState.cardDigits will be an array of arrays, corresponding to the values from the four card number fields. E.g appState.cardDigits[1] should be an array of the integers entered as value for the second card number field.

The final thing to do when you have a valid entry on a given field, is to make a call to smartCursor with the needed parameters so it do its job.

You are going to implement a smart type-ahead system with smartCursor. The input fileds in the app all have designated sizes, e.g all the credit card number fields have their size set to 4. Once a user has typed up to the size of such a field, input focus should move to the next field. How sweet!

By the time smartCursor is called by smartInput, the user has entered a valid character into the given field. Depending on what was set as the size attribute for the field, smartCursor should determine if the last entry has been recorded and if so, it should give input focus to the next field in the sequence - after half a second. We want to be smart about this, such that the last field is not trying to set focus on a non-existent field after it. Note that smartCursor has the following parameters :
event - a keyup event that is fired as the user types into input fields
fieldIndex - from the collection of input fields in the app, this is the zero-based index of the field trigeering the event.
fields - the collection of input fields
Step 3
The detectCardType function displays a Visa or MasterCard logo depending on the card number entered by the user. For simplicity sake, our Visa card numbers begin with 4 and MasterCard numbers begin with 5. These are the only supported credit cards in the SmartPay platform

Call detectCardType within smartInput. You can decide what the appropriate call location should be, but ideally you want this to be :

after you are sure the new entry is valid
only when the user is editing the first credit card input field
within the same invocation that is delayed for half a second to mask inputs
If detectCardType detects a Visa card, it should add is-visa to the data-credit-card DIV, else it should remove it and add is-mastercard if it detects a MasterCard. This gives the card a somewhat branded feel. To display the right card logo, it should set the source of the data-card-type IMAGE using the data URLs provided in the supportedCards object. Finally, it needs to return the is-visa or is-mastercard value depending on the type of card detected.

Step 4
You will be implementing the The Luhn Algorithm to validate 16-digit credit card numbers (See here for more details, but follow the instructions below for more clarity and simplicity.

Given a series of up to 16 digits, from the right to left, double every other digit starting with the second to last digit:

1714
=> [1*, 7, 1*, 4]
=> [2, 7, 2, 4]
If a resulting doubled number is greater than 9, replace it with either the sum of its own digits, or 9 subtracted from it.

[8, 18*, 1] 
=> [8, (1+8), 1]
OR
=> [8, (18-9), 1]
Resulting in:
=> [8, 9, 1]
Sum all of the final digits:

[8, 9, 1] 
=> 8+9+1 
=> 18
Finally, take that sum and divide it by 10. If there is no remainder, the original credit card number is valid, else it is not valid.

Sample valid card numbers for your tests:

4556372551434601
4916337563926287
4716361721613449

5130752529459529
5250457226640843
5330664490375584
Create a validateWithLuhn function above the validateCardNumber function. It should take a digits parameter which will represent the credit card numbers as an array of integers. It should return true or false depending on if the digits represent a valid credit card number or not.

Implement the validateCardNumber function to validate the card numbers entered by the user. It delegates to the validateWithLuhn function for the actual validation and returns the true or false value it gets from validateWithLuhn. Before returning the outcome of the validation, it should also add or remove the is-invalid class to the data-cc-digits DIV depending on the validity of the card number.

Recall that validateWithLuhn expects to be called with an array of integers, but we have an array of nested integer arrays in appState.cardDigits. Use the new .flat() array function on appState.cardDigits and assign the outcome of the call to a digits variable. This is what should be passed to validateWithLuhn for it to do its job. See flat/flatMap

If you have followed closely and implemented the requirements up to ths point, your SmartPay app should be fully functional now. Try entering valid / invalid values into the input fields in the UI and click the Pay Now BUTTON. How smart is your SmartPay afterall?

If all four numbered buttons on the left of the screen are ticked off with a check icon, then you have completed this assessment. You can take a screenshot or capture a <= 2 minute video of your working app and share on Twitter with these hashtags: #150DaysOfALC4 #MyGradr #GrowWithGoogle