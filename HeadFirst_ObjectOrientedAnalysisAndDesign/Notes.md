## Ch -1 well-designed apps rock

Great Software in 3 easy steps

1. **Make sure your software does what the customer wants it to do.**
    This step focuses on the customer, Make sure the does what it's supposed to do first. This where getting good requirements  and doing some analysis comes in.
    
    Tried to fix search functionality to add enums instead of comparing by lowercase.
    Added functionality to search returns List of guitars.
    


2. **Apply basics OO principles to add flexibility.**
    Once your software works, you can look for any duplicate code that might have slipped in, using OO techniques.
    
    Encapsulated out the guitar properties in Guitar Spec , and made sure we can add new properties easily. So that we have proper object for comparision.
    


3. **Strive for a maintainable, reusable design.**
    Apply patterns and principles to make sure your software is read to use for years to come.
    
    Added delegation so that our objects are less dependent upon each other, and can reused easily.
    Moved compare logic from Inventory class search to direct GuitarSpec class so that we don't need to change multiple classes(Inventory, Guitar) if some properties added in guitarSpec and can reuse logic in other places also.
     


