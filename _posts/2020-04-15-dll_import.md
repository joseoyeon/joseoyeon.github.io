---
layout: post
title:  "Dll import 방법"
date:   2020-04-08 13:51:28
categories: [All, others]
---

```c
# include<stdio.h>
# include<string.h>
#include "Decryptor.h"

#pragma comment(lib, "Decryptor.lib")

extern "C" __declspec(dllimport) void Decryptor(Byte* in, Byte* out);
```


![image](https://user-images.githubusercontent.com/46625602/79340594-7afc4900-7f65-11ea-8679-211d914f8a23.png)
`C:\Users\User\Desktop\Debug;%(AdditionalIncludeDirectories)`

![image](https://user-images.githubusercontent.com/46625602/79340642-8f404600-7f65-11ea-90d1-16d4760b0a68.png)
`C:\Users\User\Desktop\Debug;%(AdditionalLibraryDirectories)`

![image](https://user-images.githubusercontent.com/46625602/79340680-a2ebac80-7f65-11ea-8ce3-52e2ebd58ffc.png)
`Decryptor.lib;%(AdditionalDependencies)`

![image](https://user-images.githubusercontent.com/46625602/79340732-bb5bc700-7f65-11ea-9eb6-ecdcfcb6d808.png)
`xcopy /y /d "C:\Users\User\Desktop\Debug\Decryptor.dll" "$(OutDir)"`


---

**[Reference]**

[1]  [https://docs.microsoft.com/ko-kr/cpp/build/walkthrough-creating-and-using-a-dynamic-link-library-cpp?view=vs-2019](https://docs.microsoft.com/ko-kr/cpp/build/walkthrough-creating-and-using-a-dynamic-link-library-cpp?view=vs-2019)
