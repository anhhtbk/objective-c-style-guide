# Objective-C-Style-Guide

## Dot Notation Syntax
Dot notation is RECOMMENDED over bracket notation for getting and setting properties.

**For Example:**
```Objective-C
view.backgroundColor = [UIColor orangeColor];
[UIApplication sharedApplication].delegate;
```
**Not:**
```Objective-C
[view setBackgroundColor:[UIColor orangeColor]];
UIApplication.sharedApplication.delegate;
```
## Spacing
- Indentation MUST use 4 spaces. Never indent with tabs. Be sure to set this preference in Xcode.
- Method braces and other braces (```if```/```else```/```switch```/```while``` etc.) MUST open on the same line as the statement. Braces MUST close on a new line.
**For Example:**
```Objective-C
if (user.isHappy) {
    // Do something
}
else {
    // Do something else
}
```
- There SHOULD be exactly one blank line between methods to aid in visual clarity and organization.
- Whitespace within methods MAY separate functionality, though this inclination often indicates an opportunity to split the method into several, smaller methods. In methods with long or verbose names, a single line of whitespace MAY be used to provide visual separation before the method’s body.
- ```@synthesize``` and ```@dynamic``` MUST each be declared on new lines in the implementation.

## Conditionals
**For example:**
```Objective-C
if (!error) {
    return success;
}
```
**Not:**
```Objective-C
if (!error)
    return success;
```
or
```Objective-C
if (!error) return success;
```
## Error Handling
When methods return an error parameter by reference, code MUST switch on the returned value and MUST NOT switch on the error variable.

**For example:**
```Objective-C
NSError *error;
if (![self trySomethingWithError:&error]) {
    // Handle Error
}
```
**Not:**
```Objective-C
NSError *error;
[self trySomethingWithError:&error];
if (error) {
    // Handle Error
}
```
Some of Apple’s APIs write garbage values to the error parameter (if non-NULL) in successful cases, so switching on the error can cause false negatives (and subsequently crash).
## Methods
In method signatures, there SHOULD be a space after the scope (```-``` or ```+``` symbol). There SHOULD be a space between the method segments.

**For example:**
```Objective-C
- (void)setExampleText:(NSString *)text image:(UIImage *)image;
```
## Variables

## CGRect Functions
When accessing the ```x```, ```y```, ```width```, or ```height``` of a ```CGRect```, code MUST use the ```CGGeometry``` functions instead of direct struct member access. From Apple's CGGeometry reference:
>All functions described in this reference that take CGRect data structures as inputs implicitly standardize those
>rectangles before calculating their results. For this reason, your applications should avoid directly reading and writing >the data stored in the CGRect data structure. Instead, use the functions described here to manipulate rectangles and to >retrieve their characteristics.

**For example:**
```Objective-C
CGRect frame = self.view.frame;

CGFloat x = CGRectGetMinX(frame);
CGFloat y = CGRectGetMinY(frame);
CGFloat width = CGRectGetWidth(frame);
CGFloat height = CGRectGetHeight(frame);
```
**Not:**
```Objective-C
CGRect frame = self.view.frame;

CGFloat x = frame.origin.x;
CGFloat y = frame.origin.y;
CGFloat width = frame.size.width;
CGFloat height = frame.size.height;
```
## Booleans

Values MUST NOT be compared directly to ```YES```, because ```YES``` is defined as 1, and a ```BOOL``` in Objective-C is a ```CHAR``` type that is 8 bits long (so a value of ```11111110``` will return ```NO``` if compared to ```YES```).

For an object pointer:
```Objective-C
if (!someObject) {
}

if (someObject == nil) {
}
```
For a BOOL value:
```Objective-C
if (isAwesome)
if (!someNumber.boolValue)
if (someNumber.boolValue == NO)
```
Not:
```Objective-C
if (isAwesome == YES) // Never do this.
```
