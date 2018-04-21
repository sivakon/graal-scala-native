# graal-scala-native

- Create `Hello.scala`
- Compile the scala file using `scalac Hello.scala -d target`. This generates all the class files with target folder.
- Create native binary using `native-image` command.

```
native-image --no-server -cp /usr/local/lib/scala-library-2.12.4.jar:./target -H:-MultiThreaded -H:Class=Hello -H:Debug=2 -H:-AOTInline -H:SourceSearchPath=./
```
Refer to [polyglot-native-demo](https://github.com/vjovanov/polyglot-native-demo)

This command also works
```
native-image --no-server -cp /usr/local/lib/scala-library-2.12.4.jar:./target -H:-MultiThreaded -H:Class=Hello -H:Debug=2 -H:-AOTInline
```
Make sure the classpath contains `Main` method. `-H:Class=Hello` in the command tells the compiler to look for the main class in the classpath.


- For shared library
```
native-image --no-server -cp /usr/local/lib/scala-library-2.12.4.jar -H:Name=libhello -H:Path=./target -H:Debug=2 -H:-AOTInline -H:Kind=SHARED_LIBRARY
```
