# Favorite Extract Tool
FE - 解包FVP引擎文件


用法：

	fvp -d input.hcb output.txt
	fvp -split strings.txt
	fvp -c [-ww charlimit] strings.txt script.txt output.hcb
	fvp -decode input [output]
	fvp -encode input [output]

-------------

使用"-d"转储给定hcb文件的操作码并将字符串转储到单独的文件。

使用"-split"将字符串文件拆分为多个部分。这些部分需要按以下方式手动声明：

\<part name="Shinku Route" filename="shinku_route.txt"\> <br>
... <br>
Strings <br>
... <br>
\</part\>

使用"-c"从字符串文件和字节码文件重建一个新的hcb文件。 如果你拆分你的字符串脚本到不同的部分或使用上述拆分机制，你可以使用构建脚本而不是完整的第一个参数的字符串文件。 例如，假设您已将共通线分成几章。 一起构建脚本然后看起来会像这样：

\<part filename="chapter_1.txt"\> <br>
\<part filename="chapter_2.txt"\> <br>
\<part filename="chapter_3.txt"\> <br>
\<part filename="chapter_4.txt"\> <br>
...

（允许绝对路径和相对路径）


使用"-decode"模式将NVSG图像转换为PNG。可以转换单个文件或输入文件夹作为输入，然后将自动转换在该文件夹中找到的所有NVSG图像，可以指定输出名称或文件夹。

使用"-encode"模式将 PNG 图像转换为 NVSG。您可以转换单个文件或输入文件夹作为输入， 然后将自动转换在该文件夹中找到的所有PNG图像，可以指定输出名称或文件夹。
注意：NVSG图像具有硬编码的游戏位置。为此，"-decode"模式会自动写入、维护并更新存储提取位置信息的"pos.dat"文件，你必须使用该工具解码要重新编码的图像，并确保"pos.dat"文件与FS位于同一文件夹中。 

-------------

脚本语法的快速纲要...

注释用#号标记。

标签可以是任何以冒号结尾的单行字符串（区分大小写）。

默认情况下，标签将具有自动生成的名称，你可以随时在脚本中编辑标签名称。在脚本中重命名标签时，一定要进行完整的搜索和替换。

该工具将假定在"initstack"操作时声明了一个函数。在"initstack"之前需要一个标签，否则工具会失败。

"call"操作码使用的标签不能被"jmp"和"jmpcond"操作码使用。

函数指针可以在"pushint"中使用。 示例：pushint LABEL:function_XXX_
这通常用于"syscall ThreadStart"命令。

在文本转储快要结束时，您可以编辑"TITLE"行，其中包含游戏标题栏的文本。
