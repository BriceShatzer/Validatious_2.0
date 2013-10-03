#Validatious 2.0
Originally from [Christian Johansen](http://cjohansen.no/). [Duplicated](https://github.com/cjohansen/validatious) for posterity. Also, I felt the the orginal repository was too verbose and found the [documentation site](http://validatious.org/) to be suffering from network performance issues.
The versions that are included in this repo were created from [here](http://validatious.org/download/latest) and contains:
- Standalone Library in english
- Validators: alpha, alphanum, confirmation-of, email, max-length, max-val, min-length, min-val, numeric, required, url, word
- Extensions: HTML, Reporting
Minified: 21.1 KB
Normal: 67.2 KB
### 
 
##Add validators
Adding validators is as simple as adding validator names as class names to input/select/textarea elements:

    <input type="text" name="email" id="email" class="required email" />  

##Reasonable default error messages
Validatious guesses field names from label elements to make default error messages more usable:

    <label for="name">Name</label>  
    <input type="text" name="name" id="name" class="required">  

...yields "Name is required". So does this:

    <label for="name" title="Name">Enter name:</label>  
    <input type="text" name="name" id="name" class="required">  

##Validate radio buttons
You can add validators to a set of radio buttons by adding class names to only one element in the group:

    <ul class="inputs">  
      <li>  
        <input type="radio" name="fruit" id="apple" value="apple" class="required">  
        <label for="apple">Apple</label>  
      </li>  
      <li>  
        <input type="radio" name="fruit" id="orange" value="orange">  
        <label for="orange">Orange</label>  
      </li>  
      <li>  
        <input type="radio" name="fruit" id="pear" value="pear">  
        <label for="pear">Pear</label>  
      </li>  
    </ul>

##Validate checkboxes
Checkboxes can be validated just like radio buttons, however, they need to be explicitly grouped first, by giving all input elements a class name like g_:

    <ul class="inputs">  
      <li>  
        <input type="checkbox" name="vegetabel_onion" title="Please select atleast 2 vegetables" id="onion    " class="g_vegetables min-length_2">  
        <label for="onion">Onion</label>  
      </li>  
      <li>  
        <input type="checkbox" name="vegetable_potato" id="potato" class="g_vegetables">  
        <label for="potato">Potato</label>  
      </li>  
      <li>  
        <input type="checkbox" name="vegetable_tomato" id="tomato" class="g_vegetables">  
        <label for="tomato">Tomato</label>  
      </li>  
    </ul>  

##Styling errors
By default, Validatious will display all messages (one per validator/field combination that fails) above the failing field:

    <div class="field error">  
      <ul class="messages">  
        <li>Name is required</li>  
      </ul>  
      <label for="name">First name</label>  
      <input type="text" name="name" id="name" class="required">  
    </div>  


##Validators

alpha
>Validates that a value contans only letters.

alphanum
>Validates that a value only contains letters and numbers.

car-regnum-nor
>Validates that a value is a valid norwegian car registration number (as in license plates).

confirmation-of
>Validates that a value is a confirmation of another field.

email
>Validates a value as an email address.

max-length
>Validates the length of a field; the first parameter sets the maximum allowed length. The length parameter is available in error messages as ${max}.

max-val
>Validates that a value is no bigger than params[0]. Mostly for numbers, but also works for strings. The value parameter is available in error messages as ${max}.

min-length
>Validate the length of a field; the first parameter sets the minimum length required. The length parameter is available in error messages as ${min}.

min-val
>Validates that a value is bigger than params[0]. Mostly for numbers, but it'll work for strings as well. The value parameter is available in error messages as ${min}.

numeric
>Validates that a value only contains numbers.

phone-nor
>Validates that a value is a valid norwegian telephone number.

required
>Validates that a field has a value.

ssn-nor
>Validates that a value is a valid norwegian social security number.

url
>Validates that a value is a valid URL.

word
>Validates that a value contains only letters, numbers, spaces, tabs, underscores and dashes.


##Configuration settings
Set config settings after the validation script is called
    
    <script src="validatious.min.js"></script>
    <script> 
    	v2.Field.prototype.instant=true;
    	v2.Field.prototype.failureClass='broken';
    </script>
...this turns on instant validation and changes the class that is applied when an error occurs from 'error' to 'broken'   
    

v2.Field.prototype.validateHidden
>Decides if Validatious will validate a field when it is not visible. If this setting is true then fields will be validated even if it or one of it's parents are not visible.
*Default value is false*

v2.Field.prototype.instant
>If true, then each field will be instantly validated whenever the user changes/enters/selects a value.
*Default value is false*

v2.Field.prototype.instantWhenValidated
>If true, then each field will be instantly validated whenever the user changes/enters/selects a value, after the form has been validated once (ie by clicking the submit button).
*Default value is true*

v2.FieldValidator.prototype.invert
>If true, all validators will be inverted, and thus will only pass when they are invalid. This setting is most useful for single instances in some cases where the inverse is needed.
*Default value is false*

v2.Validator.prefix
>Sets a prefix for validator class names. By default there is no prefix, meaning that class="required" will resolve to the required validator. With a prefix of v2_, the previous example yields no validator, however class="v2_required" will.
*Default value is no prefix*

v2.Form.autoValidateClass
>The class name by which forms are selected for validation by the HTML extension.
*Default value is 'validate'*

v2.Form.actionButtonClass
>The class name by which buttons are selected to trigger validation by the HTML extension.
*Default value is 'action'*

v2.html.validateAnyClass
>The class name by which div and fieldset elements are selected for grouped validation where all validators are required to pass by the HTML extension.
*Default value is 'validate_any'*

v2.html.validateAllClass
>The class name by which div and fieldset elements are selected for grouped validation where only one validator is required to pass by the HTML extension.
*Default value is 'validate_all'*

v2.Field.prototype.displayErrors
>The number of errors to display per field.
*Default value is -1, ie all*

v2.Field.prototype.displayErrorsAbove
>If true, the errors list will be appended as the first element in the fields parent element. Otherwise it will be included last in the parent.
*Default value is true*

v2.Field.prototype.failureClass
>The class name that is appended to the fields parent element when the field fails validation.
*Default value is 'error'*

v2.Field.prototype.successClass
>The class name that is appended to the fields parent element when the field passes validation.
*Default value is '', ie no class is appended on success*

v2.Field.prototype.messagesClass
>The class name for the ul element that contains the error messages when validation fails.
*Default value is 'messages'*

v2.Fieldset.prototype.displayErrors
>The number of errors to display per fieldset.
*Default value is -1, ie all*

v2.Fieldset.prototype.displayErrorsAbove
>If true, the errors list will be appended as the first element in the fieldset/div element. Otherwise it will be included last child.
*Default value is true*

v2.Fieldset.prototype.failureClass
>The class name that is appended to the fieldset/div element when the collection fails validation.
*Default value is 'error'*

v2.Fieldset.prototype.successClass
>The class name that is appended to the fieldset/div element when the collection passes validation.
*Default value is '', ie no class is appended on success*

v2.Fieldset.prototype.messagesClass
>The class name for the ul element that contains the error messages when validation fails.
*Default value is 'messages'*

v2.Form.prototype.scrollToFirstWhenFail
>If true, then the page will scroll down to the first field that failed when a form is submitted with invalid fields.
*Default value is true*