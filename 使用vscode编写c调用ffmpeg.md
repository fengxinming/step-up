# 使用vscode编写c调用ffmpeg

## 新增debug配置
**launch.json**
```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "clang",
      "type": "cppdbg",
      "request": "launch",
      "program": "${fileDirname}/${fileBasenameNoExtension}",
      "args": [],
      "stopAtEntry": true,
      "cwd": "${workspaceFolder}",
      "environment": [],
      "externalConsole": false,
      "MIMode": "lldb",
      "preLaunchTask": "clang build active file"
    }
  ]
}
```
**tasks.json**
```json
{
  "version": "2.0.0",
  "tasks": [
    {
      "type": "shell",
      "label": "clang build active file",
      "command": "/usr/bin/clang",
      "args": [
        "-std=c11",
        "-g",
        "${file}",
        "-I",
        "${workspaceFolder}/include",
        "-L",
        "${workspaceFolder}/lib",
        "-o",
        "${fileDirname}/${fileBasenameNoExtension}",
        "-lavutil",//依赖
        "-lavcodec"//依赖
      ],
      "options": {
        "cwd": "${workspaceFolder}"
      },
      "problemMatcher": [
        "$gcc"
      ],
      "group": {
        "kind": "build",
        "isDefault": true
      }
    }
  ]
}
```
**c_cpp_properties.json**(非必要配置)
```json
{
    "configurations": [
        {
            "name": "Mac",
            "browse": {
                "path": [
                    "${workspaceFolder}/**"
                ],
                "limitSymbolsToIncludedHeaders": true,
                "databaseFilename": ""
            },
            "includePath": [
                "${workspaceFolder}/**"
            ],
            "defines": [],
            "macFrameworkPath": [
                "/Library/Developer/CommandLineTools/SDKs/MacOSX.sdk/System/Library/Frameworks"
            ],
            "compilerPath": "/usr/bin/clang",
            "cStandard": "c11",
            "cppStandard": "c++17",
            "intelliSenseMode": "clang-x64"
        }
    ],
    "version": 4
}
```
