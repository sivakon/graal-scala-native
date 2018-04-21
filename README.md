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

## Another way to build a native executable
- Create a new project using `sbt new sbt/scala-seed.g8` (SBT >= 1.0)
- Create main method in `example.Hello`
- Run the command to build the executable 
Executable size is considerably low without any `-H` flags. (~5 MB)

```
native-image -jar target/scala-2.12/hello_2.12-0.1.0-SNAPSHOT.jar -cp /usr/local/lib/scala-library-2.12.4.jar -H:Class=example.Hello
```

## Another way to build a native executable
- Build a fat deployable jar using `sbt assembly`
- Run the command to build the executable (executable is 5MB in size). Bypassing the need to add all the relevant classpaths (good thing).
```
native-image -jar target/scala-2.12/Hello-assembly-0.1.0-SNAPSHOT.jar
```

More things. Need to compare the run time performance of `scala-native` and `graal-scala-native`.

