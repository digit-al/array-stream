# array-stream
Allows arrays to be turned into a stream of objects and then run asynchronous map, filter, and reduce operations against them.

The module exposes methods to create three types of stream:
- **Reader**: read stream that turns an array into a stream of objects;
- **Transformer**: transform stream that can perform map or filter like operations against a stream of objects;
- **Reducer**: transform stream the turns a stream of objects into one object.

API
---
`createReader(array)`
---
This is the function used to transform an array into a stream. The function returns a *read* stream that operates in *object mode*.
Each read of the stream will return one object from the original array.

`createTransformer(cb[, stringify])`
---
This returns a transform stream that applies the supplied callback function to each object in the stream. You can simulate
*map* operations by having the callback function transform the object in some way before returning it and you can simulate
*filter* operations by returning *null* or *undefined* for any object that you don't want to be included in the output. 

The *cb* parameter is the callback. This should be a function that accepts an object as the single parameter and returns an
object that will be inserted into the output stream.

The *stringify* parameter is a boolean value. If set to true the objects will be turned into JSON strings before being added to
the output. This allows the stream to be piped directly to streams that do not suport objects. This parameter defaults to false.

**Important Note**: One important difference between this and Array.map is that the latter allows *null* or *undefined* items
to be included in the 
