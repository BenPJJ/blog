# 配置tsconfig.json

``` json
{
  "compilerOptions": {
    /* Visit https://aka.ms/tsconfig.json to read more about this file */

    /* Basic Options */
    // "incremental": true,                   /* Enable incremental compilation. */
    "target": "es5",                          /* Specify ECMAScript target version: 'ES3' (default), 'ES5', 'ES2015', 'ES2016', 'ES2017', 'ES2018', 'ES2019', 'ES2020', or 'ESNEXT'. */
    "module": "commonjs",                     /* Specify module code generation: 'none', 'commonjs', 'amd', 'system', 'umd', 'es2015', 'es2020', or 'ESNext'. */
    // "lib": [],                             /* Specify library files to be included in the compilation. */
    // "allowJs": true,                       /* Allow javascript files to be compiled. */
    // "checkJs": true,                       /* Report errors in .js files. */
    // "jsx": "preserve",                     /* Specify JSX code generation: 'preserve', 'react-native', or 'react'. */
    // "declaration": true,                   /* Generates corresponding '.d.ts' file. */
    // "declarationMap": true,                /* Generates a sourcemap for each corresponding '.d.ts' file. */
    // "sourceMap": true,                     /* Generates corresponding '.map' file. */
    // "outFile": "./",                       /* Concatenate and emit output to single file. */
    // "outDir": "./",                        /* Redirect output structure to the directory. */
    // "rootDir": "./",                       /* Specify the root directory of input files. Use to control the output directory structure with --outDir. */
    // "composite": true,                     /* Enable project compilation */
    // "tsBuildInfoFile": "./",               /* Specify file to store incremental compilation information */
    // "removeComments": true,                /* Do not emit comments to output. */
    // "noEmit": true,                        /* Do not emit outputs. */
    // "importHelpers": true,                 /* Import emit helpers from 'tslib'. */
    // "downlevelIteration": true,            /* Provide full support for iterables in 'for-of', spread, and destructuring when targeting 'ES5' or 'ES3'. */
    // "isolatedModules": true,               /* Transpile each file as a separate module (similar to 'ts.transpileModule'). */

    /* Strict Type-Checking Options */
    "strict": true,                           /* Enable all strict type-checking options. */
    // "noImplicitAny": true,                 /* Raise error on expressions and declarations with an implied 'any' type. */
    // "strictNullChecks": true,              /* Enable strict null checks. */
    // "strictFunctionTypes": true,           /* Enable strict checking of function types. */
    // "strictBindCallApply": true,           /* Enable strict 'bind', 'call', and 'apply' methods on functions. */
    // "strictPropertyInitialization": true,  /* Enable strict checking of property initialization in classes. */
    // "noImplicitThis": true,                /* Raise error on 'this' expressions with an implied 'any' type. */
    // "alwaysStrict": true,                  /* Parse in strict mode and emit "use strict" for each source file. */

    /* Additional Checks */
    // "noUnusedLocals": true,                /* Report errors on unused locals. */
    // "noUnusedParameters": true,            /* Report errors on unused parameters. */
    // "noImplicitReturns": true,             /* Report error when not all code paths in function return a value. */
    // "noFallthroughCasesInSwitch": true,    /* Report errors for fallthrough cases in switch statement. */

    /* Module Resolution Options */
    // "moduleResolution": "node",            /* Specify module resolution strategy: 'node' (Node.js) or 'classic' (TypeScript pre-1.6). */
    // "baseUrl": "./",                       /* Base directory to resolve non-absolute module names. */
    // "paths": {},                           /* A series of entries which re-map imports to lookup locations relative to the 'baseUrl'. */
    // "rootDirs": [],                        /* List of root folders whose combined content represents the structure of the project at runtime. */
    // "typeRoots": [],                       /* List of folders to include type definitions from. */
    // "types": [],                           /* Type declaration files to be included in compilation. */
    // "allowSyntheticDefaultImports": true,  /* Allow default imports from modules with no default export. This does not affect code emit, just typechecking. */
    "esModuleInterop": true,                  /* Enables emit interoperability between CommonJS and ES Modules via creation of namespace objects for all imports. Implies 'allowSyntheticDefaultImports'. */
    // "preserveSymlinks": true,              /* Do not resolve the real path of symlinks. */
    // "allowUmdGlobalAccess": true,          /* Allow accessing UMD globals from modules. */

    /* Source Map Options */
    // "sourceRoot": "",                      /* Specify the location where debugger should locate TypeScript files instead of source locations. */
    // "mapRoot": "",                         /* Specify the location where debugger should locate map files instead of generated locations. */
    // "inlineSourceMap": true,               /* Emit a single file with source maps instead of having a separate file. */
    // "inlineSources": true,                 /* Emit the source alongside the sourcemaps within a single file; requires '--inlineSourceMap' or '--sourceMap' to be set. */

    /* Experimental Options */
    // "experimentalDecorators": true,        /* Enables experimental support for ES7 decorators. */
    // "emitDecoratorMetadata": true,         /* Enables experimental support for emitting type metadata for decorators. */

    /* Advanced Options */
    "skipLibCheck": true,                     /* Skip type checking of declaration files. */
    "forceConsistentCasingInFileNames": true  /* Disallow inconsistently-cased references to the same file. */
  }
}
```

| 配置项                       | 说明                                                         |
| ---------------------------- | ------------------------------------------------------------ |
| Basic Options                |                                                              |
| target                       | target用于指定编译之后的版本目标: 'ES3' (default), 'ES5', 'ES2015', 'ES2016', 'ES2017', 'ES2018', 'ES2019' or 'ESNEXT' |
| module                       | 用来指定要使用的模块标准: 'none', 'commonjs', 'amd', 'system', 'umd', 'es2015', or 'ESNext' |
| lib                          | lib用于指定要包含在编译中的库文件                            |
| allowJs                      | allowJs设置的值为true或false，用来指定是否允许编译js文件，默认是false，即不编译js文件 |
| checkJs                      | checkJs的值为true或false，用来指定是否检查和报告js文件中的错误，默认是false |
| jsx                          | 指定jsx代码用于的开发环境: 'preserve', 'react-native', or 'react' |
| declaration                  | declaration的值为true或false，用来指定是否在编译的时候生成相应的".d.ts"声明文件。如果设为true，编译每个ts文件之后会生成一个js文件和一个声明文件。但是declaration和allowJs不能同时设为true |
| declarationMap               | 值为true或false，指定是否为声明文件.d.ts生成map文件          |
| sourceMap                    | sourceMap的值为true或false，用来指定编译时是否生成.map文件   |
| outFile                      | outFile用于指定将输出文件合并为一个文件，它的值为一个文件路径名。比如设置为"./dist/main.js"，则输出的文件为一个main.js文件。但是要注意，只有设置module的值为amd和system模块时才支持这个配置 |
| outDir                       | outDir用来指定输出文件夹，值为一个文件夹路径字符串，输出的文件都将放置在这个文件夹 |
| rootDir                      | 用来指定编译文件的根目录，编译器会在根目录查找入口文件，如果编译器发现以rootDir的值作为根目录查找入口文件并不会把所有文件加载进去的话会报错，但是不会停止编译 |
| composite                    | 是否编译构建引用项目                                         |
| incremental                  | 是否启用增量编译                                             |
| tsBuildInfoFile              | 指定文件用来存储增量编译信息                                 |
| removeComments               | removeComments的值为true或false，用于指定是否将编译后的文件中的注释删掉，设为true的话即删掉注释，默认为false |
| noEmit                       | 不生成编译文件，这个一般比较少用                             |
| importHelpers                | importHelpers的值为true或false，指定是否引入tslib里的辅助工具函数，默认为false |
| downlevelIteration           | 当target为'ES5' or 'ES3'时，为'for-of', spread, and destructuring'中的迭代器提供完全支持 |
| isolatedModules              | isolatedModules的值为true或false，指定是否将每个文件作为单独的模块，默认为true，它不可以和declaration同时设定 |
|                              |                                                              |
| Strict Type-Checking Options |                                                              |
| strict                       | strict的值为true或false，用于指定是否启动所有类型检查，如果设为true则会同时开启下面这几个严格类型检查，默认为false |
| noImplicitAny                | noImplicitAny的值为true或false，如果我们没有为一些值设置明确的类型，编译器会默认认为这个值为any，如果noImplicitAny的值为true的话。则没有明确的类型会报错。默认值为false |
| strictNullChecks             | strictNullChecks为true时，null和undefined值不能赋给非这两种类型的值，别的类型也不能赋给他们，除了any类型。还有个例外就是undefined可以赋值给void类型 |
| strictFunctionTypes          | strictFunctionTypes的值为true或false，用于指定是否使用函数参数双向协变检查 |
| strictBindCallApply          | 设为true后会对bind、call和apply绑定的方法的参数的检测是严格检测的 |
| strictPropertyInitialization | 设为true后会检查类的非undefined属性是否已经在构造函数里初始化，如果要开启这项，需要同时开启strictNullChecks，默认为false |
| noImplicitThis               | 当this表达式的值为any类型的时候，生成一个错误                |
| alwaysStrict                 | alwaysStrict的值为true或false，指定始终以严格模式检查每个模块，并且在编译之后的js文件中加入"use strict"字符串，用来告诉浏览器该js为严格模式 |
|                              |                                                              |
| Additional Checks            |                                                              |
| noUnusedLocals               | 用于检查是否有定义了但是没有使用的变量，对于这一点的检测，使用eslint可以在你书写代码的时候做提示，你可以配合使用。它的默认值为false |
| noUnusedParameters           | 用于检查是否有在函数体中没有使用的参数，这个也可以配合eslint来做检查，默认为false |
| noImplicitReturns            | 用于检查函数是否有返回值，设为true后，如果函数没有返回值则会提示，默认为false |
| noFallthroughCasesInSwitch   | 用于检查switch中是否有case没有使用break跳出switch，默认为false |
|                              |                                                              |
| Module Resolution Options    |                                                              |
| moduleResolution             | 用于选择模块解析策略，有'node'和'classic'两种类型'           |
| baseUrl                      | baseUrl用于设置解析非相对模块名称的基本目录，相对模块不会受baseUrl的影响 |
| paths                        | 用于设置模块名称到基于baseUrl的路径映射                      |
| rootDirs                     | rootDirs可以指定一个路径列表，在构建时编译器会将这个路径列表中的路径的内容都放到一个文件夹中 |
| typeRoots                    | typeRoots用来指定声明文件或文件夹的路径列表，如果指定了此项，则只有在这里列出的声明文件才会被加载 |
| types                        | types用来指定需要包含的模块，只有在这里列出的模块的声明文件才会被加载进来 |
| allowSyntheticDefaultImports | 用来指定允许从没有默认导出的模块中默认导入                   |
| esModuleInterop              | 通过为导入内容创建命名空间，实现CommonJS和ES模块之间的互操作性 |
| preserveSymlinks             | 不把符号链接解析为其真实路径，具体可以了解下webpack和nodejs的symlink相关知识 |
| allowUmdGlobalAccess         | 允许从模块访问UMD全局参数                                    |
|                              |                                                              |
| Source Map Options           |                                                              |
| sourceRoot                   | sourceRoot用于指定调试器应该找到TypeScript文件而不是源文件位置，这个值会被写进.map文件里 |
| mapRoot                      | mapRoot用于指定调试器找到映射文件而非生成文件的位置，指定map文件的根路径，该选项会影响.map文件中的sources属性 |
| inlineSourceMap              | 指定是否将map文件的内容和js文件编译在同一个js文件中，如果设为true，则map的内容会以//# sourceMappingURL=然后拼接base64字符串的形式插入在js文件底部 |
| inlineSources                | 用于指定是否进一步将.ts文件的内容也包含到输入文件中          |
|                              |                                                              |
| Experimental Options         |                                                              |
| experimentalDecorators       | 用于指定是否启用实验性的装饰器特性                           |
| emitDecoratorMetadata        | 用于指定是否为装饰器提供元数据支持，关于元数据，也是ES6的新标准，可以通过Reflect提供的静态方法获取元数据，如果需要使用Reflect的一些方法，需要引入ES2015.Reflect这个库 |
|                              |                                                              |

