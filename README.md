# Vue Cookies Warning

That annoying little bar at the page footer, wrapped into Vue component


## Props

### cookie_name
**Type**: _Boolean_  
**Default**: `cookies-accepted`   
Cookie name that will store the users choice



### expires
**Type**: _String_  
**Default**: `Fri, 31 Dec 9999 23:59:59 GMT`   
Cookie expiration date



### animate
**Type**: _Boolean_  
**Default**: `true`   
To disable expand/collapse animation:   
```html
<CookiesWarning animate></CookiesWarning>
```



### theme
**Type**: _String_  
**Default**: `default`   
Warning custom style class   
```html
<CookiesWarning theme="my-custom-style"></CookiesWarning>
<style>
   .my-custom-style {
      padding: 10px;
      font-size: 50px;
      background-color: magenta;
   }
</style>
```





## Events

### accepted
Fires right after the user clicks whatever you place inside `acceptButton` slot 


## Usage

```html
<CookiesWarning>
   We are using cookies for blah-blah-blah. It helps us to blah-blah-blah our service. Please, 
   <template v-slot:acceptButton>
      ACCEPT EVERYTHING THE HELL WE WANT!
   </template>
</CookiesWarning>
````

