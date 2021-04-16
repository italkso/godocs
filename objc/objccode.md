## Objective-C

### NSLog() 

```objective-c
NSLog ( @"The current date and time is: %@", [NSDate date] );
```



### Calling Methods

The **`id`** type means that the `myObject` variable can refer to any kind of object.

```objective-c
[object method];
[object methodWithInput:input];
output = [object methodWithOutput];
output = [object methodWithInputAndOutput:input];

id myObject = [NSString string];
NSString* myString = [NSString string];
```

In Objective-C, **nested method** or function calls look like this:

```objective-c
[NSString stringWithFormat:[prefs format]];
```

**Multi-Input Methods** in Objective-C :

```objective-c
//	In the header
-(BOOL)writeToFile:(NSString *)path atomically:(BOOL)useAuxiliaryFile;

//	Call this method
BOOL result = [myData writeToFile:@"/tmp/log.txt" atomically:NO];
```



### Accessors

All instance variables are private in Objective-C by default, so you should use accessors to get and set values in most cases.

```objective-c
//	Traditional 1.x syntax
[photo setCaption:@"Day at the Beach"];
output = [photo caption];

//	Dot syntax ( Objective-C 2.0, only be used setters and getters)
photo.caption = @"Day at the Beach";
output = photo.caption;
```



### Creating Objects

```objective-c
//	Create an autoreleased object
NSString* myString = [NSString string];

//	Create an object using the manual style
NSString* myString = [[NSString alloc] init];
NSNumber* value = [[NSNumber alloc] initWithFloat:1.0];
```



### Memory Management

Objective-C's memory management system is called **reference counting**. You need to keep track of your references, and the runtime does the actual freeing of memory for you. 

In simplest terms, you *alloc* an object, maybe *retain* it at some point, then send one *release* for each alloc/retain you sent. So if you used alloc once and then retain once, you need to release twice.

If you create an object using the manual *`alloc`* style, you need to *`release`* the object later. 

```objective-c
// string1 will be released automatically
NSString* string1 = [NSString string];

// must release this when done
NSString* string2 = [[NSString alloc] init];
[string2 release];
```



### Designing a Class Interface

#### Class Interface

```objective-c
//	ClassName.h
#import <Cocoa/Cocoa.h>
    
@interface Photo : NSObject {
    //	Properties
    NSString* caption;
    NSString* photographer;
    
    //	Getters
    - (NSString*) caption;
    - (NSString*) photographer;
    
    //	Setters
    - (void) setCaption: (NSString*)input;
	- (void) setPhotographer: (NSString*)input;
}
@end
```

#### Class Implementation

```objective-c
//	ClassName.m
#import "Photo.h"

@implementation Photo
    
//	Implementation of getters
- (NSString*) caption {
    return caption;
}

- (NSString*) photographer {
    return photographer;
}

//	Implementation of setters
- (void) setCaption: (NSString*)input
{
    [caption autorelease];
    caption = [input retain];
    //	In a garbage collected environment, you can set the new value directly.
    // caption = input;
}

- (void) setPhotographer: (NSString*)input
{
    [photographer autorelease];
    photographer = [input retain];
}
@end
```



#### Init

```objective-c
- (id) init
{
    if ( self = [super init] )
    {
        [self setCaption:@"Default Caption"];
        [self setPhotographer:@"Default Photographer"];
    }
    return self;
}
```



#### Dealloc

```objective-c
- (void) dealloc
{
    [caption release];
    [photographer release];
    [super dealloc];
}
```



### Categories

A category allows you to add methods to an existing class without subclassing it or needing to know any of the details of how it's implemented. 

This is particularly useful because you can add methods to built-in objects. 

```objective-c
//	
#import <Cocoa/Cocoa.h>
            
@interface NSString (Utilities)
- (BOOL) isURL;
@end
    #import "NSString-Utilities.h"
    
//             
@implementation NSString (Utilities)

- (BOOL) isURL
{
    if ( [self hasPrefix:@"http://"] )
        return YES;
    else
        return NO;
}

@end
```



***Reference***

[Learn Objective-C](http://cocoadevcentral.com/d/learn_objectivec/) ( Cocoa Dev Central )

