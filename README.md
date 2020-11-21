# Disclaimer

The code provided is "as is" and will not be supported.

## About

C# Shellcode Runner to execute shellcode via CreateRemoteThread and SetThreadContext to evade Get-InjectedThread



# CSharp SetThreadContext Shellcode Runner Example

This project is a C# port of the work @xpn did in his blog post here:

https://blog.xpnsec.com/undersanding-and-evading-get-injectedthread/

We only tackle the SetThreadContext portion here, though the building blocks to perform all three tasks are here.

This project first determines a suitable executable to spawn, decrypts shellcode using a predefined key, then uses CreateRemoteThread and SetThreadContext to ensure that the remote thread is backed by a file on disk, effectively evading `Get-InjectedThread`.

## Usage

The solution file is in `Cryptor\ThreadContextRunner.sln`. Open this and view the two projects. If you wish to change the encryption key, you'll need to change it both in `Cryptor` and `Runner` projects.

Right click `Cryptor` in the solution pane and click "Build". This will build the executable, `Cryptor.exe`, that will encrypt your shellcode. Run this by: `Cryptor.exe C:\Path\To\Shellcode.bin`. This generates a new file, `encrypted.bin`.

Next, right click the `Runner` project in the Solution Explorer on the right hand side and click "Properties". Go to Resources then add a new File resource. Navigate to the folder where `encrypted.bin` was generated and add it as a resource. Then, click this new resource in the Solution Explorer and ensure that the Build Action is set to "Embedded Resource".

Now you can rebuild the entire solution. `Runner.exe` will be generated and should be suitable to run your shellcode when double clicked.

## Special Thanks

@xpn and @its_a_feature for their excellent blog and teaching me C/C++ respectively.

<details class="details-reset details-overlay details-overlay-dark " style="box-sizing: border-box; display: block;"><summary class="float-right" role="button" style="box-sizing: border-box; display: list-item; cursor: pointer; float: right !important; list-style: none;"><div class="link-gray pt-1 pl-2" style="box-sizing: border-box; color: var(--color-text-secondary) !important; padding-top: 4px !important; padding-left: 8px !important;"><svg aria-label="Edit repository metadata" class="octicon octicon-gear float-right" height="16" viewBox="0 0 16 16" version="1.1" width="16" role="img"><path fill-rule="evenodd" d="M7.429 1.525a6.593 6.593 0 011.142 0c.036.003.108.036.137.146l.289 1.105c.147.56.55.967.997 1.189.174.086.341.183.501.29.417.278.97.423 1.53.27l1.102-.303c.11-.03.175.016.195.046.219.31.41.641.573.989.014.031.022.11-.059.19l-.815.806c-.411.406-.562.957-.53 1.456a4.588 4.588 0 010 .582c-.032.499.119 1.05.53 1.456l.815.806c.08.08.073.159.059.19a6.494 6.494 0 01-.573.99c-.02.029-.086.074-.195.045l-1.103-.303c-.559-.153-1.112-.008-1.529.27-.16.107-.327.204-.5.29-.449.222-.851.628-.998 1.189l-.289 1.105c-.029.11-.101.143-.137.146a6.613 6.613 0 01-1.142 0c-.036-.003-.108-.037-.137-.146l-.289-1.105c-.147-.56-.55-.967-.997-1.189a4.502 4.502 0 01-.501-.29c-.417-.278-.97-.423-1.53-.27l-1.102.303c-.11.03-.175-.016-.195-.046a6.492 6.492 0 01-.573-.989c-.014-.031-.022-.11.059-.19l.815-.806c.411-.406.562-.957.53-1.456a4.587 4.587 0 010-.582c.032-.499-.119-1.05-.53-1.456l-.815-.806c-.08-.08-.073-.159-.059-.19a6.44 6.44 0 01.573-.99c.02-.029.086-.075.195-.045l1.103.303c.559.153 1.112.008 1.529-.27.16-.107.327-.204.5-.29.449-.222.851-.628.998-1.189l.289-1.105c.029-.11.101-.143.137-.146zM8 0c-.236 0-.47.01-.701.03-.743.065-1.29.615-1.458 1.261l-.29 1.106c-.017.066-.078.158-.211.224a5.994 5.994 0 00-.668.386c-.123.082-.233.09-.3.071L3.27 2.776c-.644-.177-1.392.02-1.82.63a7.977 7.977 0 00-.704 1.217c-.315.675-.111 1.422.363 1.891l.815.806c.05.048.098.147.088.294a6.084 6.084 0 000 .772c.01.147-.038.246-.088.294l-.815.806c-.474.469-.678 1.216-.363 1.891.2.428.436.835.704 1.218.428.609 1.176.806 1.82.63l1.103-.303c.066-.019.176-.011.299.071.213.143.436.272.668.386.133.066.194.158.212.224l.289 1.106c.169.646.715 1.196 1.458 1.26a8.094 8.094 0 001.402 0c.743-.064 1.29-.614 1.458-1.26l.29-1.106c.017-.066.078-.158.211-.224a5.98 5.98 0 00.668-.386c.123-.082.233-.09.3-.071l1.102.302c.644.177 1.392-.02 1.82-.63.268-.382.505-.789.704-1.217.315-.675.111-1.422-.364-1.891l-.814-.806c-.05-.048-.098-.147-.088-.294a6.1 6.1 0 000-.772c-.01-.147.039-.246.088-.294l.814-.806c.475-.469.679-1.216.364-1.891a7.992 7.992 0 00-.704-1.218c-.428-.609-1.176-.806-1.82-.63l-1.103.303c-.066.019-.176.011-.299-.071a5.991 5.991 0 00-.668-.386c-.133-.066-.194-.158-.212-.224L10.16 1.29C9.99.645 9.444.095 8.701.031A8.094 8.094 0 008 0zm1.5 8a1.5 1.5 0 11-3 0 1.5 1.5 0 013 0zM11 8a3 3 0 11-6 0 3 3 0 016 0z"></path></svg></div></summary></details>





# CSharp SetThreadContext Shellcode Runner示例

**C＃Shellcode Runner**通过`CreateRemoteThread`和`SetThreadContext` `执行Shellcode`逃避`Get-InjectedThread`



这个项目是`@xpn`在他的博客文章中所做的工作的C＃端口：

https://blog.xpnsec.com/undersanding-and-evading-get-injectedthread/

尽管这里执行所有三个任务的构建块都在这里，但我们只处理`SetThreadContext`部分。

该项目首先确定要生成的`合适可执行文件`，`使用预定义的密钥` `解密shellcode`，然后使用`CreateRemoteThread`和`SetThreadContext`确保远程线程`由磁盘上的文件支持`，从而有效地逃避了`Get-InjectedThread`。

## 用法

解决方案文件位于中`Cryptor\ThreadContextRunner.sln`。打开它并查看两个项目。如果要更改加密密钥，则需要在`Cryptor`和`Runner`项目中都进行更改。

`Cryptor`在解决方案窗格中右键单击，然后单击“构建”。这将构建可执行文件，该文件`Cryptor.exe`将对您的shellcode进行加密。通过运行这个：`Cryptor.exe C:\Path\To\Shellcode.bin`。这将生成一个新文件`encrypted.bin`。

接下来，在右侧`Runner`的解决方案资源管理器中右键单击该项目，然后单击“属性”。转到资源，然后添加一个新的文件资源。导航到`encrypted.bin`生成文件夹，并将其添加为资源。然后，在解决方案资源管理器中单击此新资源，并确保将“生成操作”设置为“嵌入式资源”。

现在，您可以重建整个解决方案。`Runner.exe`将会生成，并且应该适合双击运行您的shellcode。

## 特别感谢

**@xpn**和**@its_a_feature**是他们出色的博客，并分别教我**C / C ++**。

