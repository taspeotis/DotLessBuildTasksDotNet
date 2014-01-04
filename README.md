# DotLessBuildTasksDotNet

Use dotless to automatically compile `.less` files to `.css`.

## Installing DotLessBuildTasksDotNet

Use NuGet to install the [`DotLessBuildTasksDotNet`](https://www.nuget.org/packages/DotLessBuildTasksDotNet) package. NuGet 2.5 and later will add the necessary `<Import ...` element to your project file.

> If your project is loaded before the `DotLessBuildTasksDotNet.targets` file is available (i.e. the first time the package is installed or package restore hasn't run yet) you'll need to reload the project for it to be imported.

> NuGet's support for adding MSBuild targets is somewhat nascent. If you're building your project in an environment where you can't reload the project (e.g. continuous integration server) you'll probably want to use `nuget restore` as documented [here](http://blogs.msdn.com/b/dotnet/archive/2013/08/22/improved-package-restore.aspx).

## Using DotLessBuildTasksDotNet

DotLessBuildTasksDotNet adds two custom build actions to your project - `CompileLessFile` and `LessCompiler`.

`CompileLessFile` is used to indicate that a `.less` file should be compiled into a `.css` file.

> A corollary of this is that `dotless` is not run on every single `.less` file in your project - you need to specify which `.less` files to compile. This prevents redundant compilation of shared files like `variables.less`.

DotLessBuildTasksDotNet will run before your project builds and compile each `.less` file into a `.css` file. They are not automatically added to your project, you'll need to do that yourself.

`LessCompiler` allows you to specify the `dotless` compiler executable. If this isn't specified then the executable is assumed to be `dotless.1.4.0.0\tool\dotless.compiler.exe` (found inside the NuGet `packages` folder).

## Miscellaney

If you're using a source control system that can be sensitive to line endings (e.g. Git with `text=auto`) then consider ignoring the output files. `dotless` has been observed to output files with `\n` instead of `\r\n\`.

> If you're using Git and can isolate the output files to one directory (e.g. `MyProject\Less`) then you can quickly ignore all `.css` files by creating a `.gitignore` file in the one directory with the following contents:
>
>     *.css