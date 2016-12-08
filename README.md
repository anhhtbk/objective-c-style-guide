# Objective-C-Style-Guide

### Dot Notation Syntax
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
### Spacing
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

### Conditionals
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
### Error Handling
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
### Methods
In method signatures, there SHOULD be a space after the scope (```-``` or ```+``` symbol). There SHOULD be a space between the method segments.

**For example:**
```Objective-C
- (void)setExampleText:(NSString *)text image:(UIImage *)image;
```
### Variables
