##自定义脚本

Gradle构建脚本的标准名称是build.gradle，在一个多项目构建的环境中，你想自定义你的构建脚本名称来显得高大上一点，因为多个项目有相同的构建脚本名称可能会混淆，接下来介绍如何使用自定义的脚本名称。

还是之前那个例子，假设所有的子项目路径都是以todo-开头，比如web子项目就是在todo-web目录下，构建脚本名称应该清晰的表示它的作用，如下图所示：

![](/images/dag47.png)

要使这个结构起作用关键点就是settings文件，它提供了除了包含哪个子目录的其他功能，实际上设置文件是一个构建脚本，它会在构建生命周期的评估阶段执行，通过Gradle提供的API来添加自定义的逻辑，如下所示：

	//通过目录来添加子项目
	include 'todo-model', 'todo-repository', 'todo-web'

	//设置根项目的名字
	rootProject.name = 'todo'

	//迭代访问所有根目录下的子项目，设置自定义的构建脚本名称
	rootProject.children.each {
		it.buildFileName = it.name + '.gradle' - 'todo-'
	}


