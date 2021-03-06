# This is my ![image](https://user-images.githubusercontent.com/83614613/122271531-bc0b2880-ce9c-11eb-8d1a-bd0d3381ae7e.png) Repository

## TypeScript Basics
### Variable Declarations
```ts
let thisIsANumber: number = 1;
let thisIsAString: string = "Diego";
const constant: "constant" = "constant";
let thisIsAnAny;
thisIsAnAny = 2;
thisIsAnAny = "Enrique";
```
### Arrays & Tuples
```ts
// Array and Tuples declarations
let arr1: number[] = [];
let arr2: string[] = [];
let arr3: any[] = [];

let array: number[] = [];
array.push( 1 );
array.push( 2 );

//This is not allowed because is not a number, it is a string rather.
array.push( "abc" );

// Even if we declare an array with a value, the type of that 
// value is going to be the one the array is going to take.

1 typeof = Number

let array2 = [1];
array2.push( 2 );
array2.push( 3 );

// This is not allowed because our array2 cointains number values
array.push( "def" );

let tuple: [ number, string, string, number ] = [
  123,
  "Lourdes Colón",
  "Villa Lourdes",
  321
];

// This is going to throw an error because a tuple cannot be reassigned
tuple = [ 1,2,3 ];

// We can do this, because our tuple can receive numbers and strings
tuple.push( 5,4,3,2,1 );

const tuple2 = [ 7, 8 ];
const tuple3: [ number, number ] = [ 7, 8 ];
```
### Object Types & Interfaces
```ts
// This is how we can declare an object
let obj: { houseNumber: number ; streetName: string };
obj = {
  streetName: "Manuel Enrique Araujo"
  houseNumber: 22
};

// When using the question mark, we are saying that object value
// is optional to use. So there is no problem if we no declare it
let obj2: { houseNumber: number ; streetName?: string };
obj2: {
  houseNumber: 22,
  streeName: "",
  // We cannot do this because x is not declared above in its declaration
  x: 145
};

// This is how we work with the interface data structure
interface Address {
  houseNumber: number;
  streetName?: string;
}

let interfaceA: Adress = { houseNumber: 22 };
// This is optional, there is not going to be any problem
// If we declare it or not
let interfaceB: Adress = { streetName: "Juan Pabloo II" };
```
### Intersection & Union Types
```ts
// Here we are exporting our interfaces
export interface HasPhoneNumber {
  name: string;
  phone: number;
}

export interface HasEmail {
  name: string;
  phone: number;
}

// Intersection Operator -> |
let contactInfo : HasEmail | HasPhoneNumber =
Math.random() > 0.5
  ? {
      // It can be assigned to HasPhoneNumber
      name: "Diego",
      phone: 7964630212
    }
  : {
      // or to HasEmail
      name: "Enrique",
      email: "diego@elaniin.com"
    }

// We can only access to the name value, because is the one
// that exists in both interfaces
contactInfo.name;

// Union Operator -> &
let otherContactInfo: HasEmail & HasPhoneNumber = {
  // Here we will assign the values we have in both interfaces
  // Those are: name, email and phone
  name: "Diego",
  email: "diego@elaniin.com",
  phone: 7964630212
}

// We can access to the 3 values because they are linked
// in both interfaces
otherContactInfo.name;
otherContactInfo.email;
otherContactInfo.phone;
```
### Type Systems & Object Shapes
![image](https://user-images.githubusercontent.com/83614613/122273280-7ea79a80-ce9e-11eb-991b-56e060eaa6fd.png)

### Functions
```ts
// A normal TypeScript function
function sendEmail ( to: HasEmail ) : { recipient: string ; body: string } {
  return {
    recipient: `${ to.name } <${ to.email }>`,
    // The result is the variables' values we create in the interfaces above
    // Diego <diego@elaniin.com>
    body: "You are pre-qualified for a loan!"
  };
}

// An arrow TypeScript function
const sendTextMessage = ( 
  to: HasPhoneNumber 
   ) : { recipient: string ; body: string } =>
    return {
      recipient: `${ to.name } <${ to.email }>`,
      // The result is the variables' values we create in the interfaces above
      // Diego <diego@elaniin.com>
      body: "You are pre-qualified for a loan!"
    };
}

// An inferred TypeScript function
function getNameParts ( contact: { name: string } ) { /* Process */ };

// Rest Params
const sum = ( ...vals: number[] ) => vals.reduce( ( sum, x ) => sum + x );
console.log( sum( 3,4,6 ) );
// 13
```
## Interface Type Basics
## Type Alias
```ts
type StringOrNumber = string | number;
// This is the only time a type is assigned on the right hand side
type HasName = { name: string };

// Examples:
const x = [ 1,2,3, [ 1,2,3 ] ];
type NumVal = 1 | 2 | 3 | NumArr;
type NumArr = NumVal[];
interface NumArr extends Array< NumVal > {}

// Interfaces can extend from other interfaces
export interface HasInternationalPhoneNumber extends HasPhoneNumber {
  countryCode: string;
}
```
## Call and Construct Sigantures
```ts
// This is a function signature
interface ContactMessenger1 {
  ( contact: HasEmail | HasPhoneNumber, message: string ) void;
}

type ContactMessenger2 = (
  contact: HasEmail | HasPhoneNumber,
  message: string
) => void;

// Contextual Inference
const emailer: ContactMessenger1 = ( _contact, _message ) => { /* code */ };

// Construc Signatures
interface ContactConstructor {
  new ( ...args: any[] ): HaEmail | HasPhone;
};
```
## Dictionary Objects & Index Signatures
```ts
interface PhoneNumberDict {
  // arr[ 0 ], foo[ 'myProp' ]
  [ numberName: string ]:
    | undefined
    | {
        areaCode: number;
        num: number;
      };
}

const d: PhoneNumberDict = {};
if ( typeof d.abc === "string" ) {
  d.abc
}

const phoneDic: PhoneNumberDict = {
  office: { areaCode: 321, num: 5551212 },
  // If we misspelt something, TypeScript is going to warn us
  home: { areCode: 321, num: 5550010 }
};
```
## Combining Interfaces
```ts
interface PhoneNumberDict {
  home: {
    /*
      Interfaces are open, meaning any declarations of the same name are merged
     */
     areaCode: number;
     num: number;
  };
  office: {
     areaCode: number;
     num: number;
  };
  
  phoneDict.home; // This one would be present
  phoneDict.office; // This one would be present too
  phoneDict.mobile; This one maybe would be present
}

// To wrap up:
// Type Aliases are eaguer, flexible
// Iterfaces are lazy and those are types we can find instead of primitive values
```
### Classes
```ts
// In TypeScript we use "implements" instead of "extends" as we do in JavaScript
export class Contact implements HasEmail {
  email: string;
  name: string;
  constructor ( name: string, email: string ) {
    this.email = email;
    this.name = name;
  }
}
```
### Access Modifiers & Initialization
Access modifier keywords:
- public - everyone
- protected - me and subclasses
- private - only me
```ts
class ParamPropContact implements HasEmail {
  constructor(
    public name: string,
    public email: string = "no email"
  )
}

const x = new ParamPropContact( 'a','b' );
x.a = value
x.b = value

// But if we declare email as protected:
protected email: string = "no email"
// We will no have access to the x.b value

// Default values
class OtherContact implements HasEmail, HasPhoneNumber {
  public age = 0;
  constructor(
    public name: string,
    public email: string,
    public phone: number
  ) {
      this.age = 35;
    }
}
```
